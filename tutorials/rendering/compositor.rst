.. _doc_compositor:

Compositor
==========

Compositor là một tính năng mới trong Godot 4, cho phép kiểm soát pipeline kết xuất khi kết xuất nội dung của một :ref:`Viewport <class_Viewport>`.

Bạn có thể cấu hình nó trên một node :ref:`WorldEnvironment <class_WorldEnvironment>`, khi đó nó sẽ áp dụng cho tất cả Viewport; hoặc cấu hình trên một :ref:`Camera3D <class_Camera3D>` để chỉ áp dụng cho Viewport sử dụng camera đó.

Resource :ref:`Compositor <class_Compositor>` được dùng để cấu hình compositor. Để bắt đầu, hãy tạo một compositor mới trên node thích hợp:

.. image:: img/new_compositor.webp

.. note::

    Hiện tại, compositor chỉ được hỗ trợ bởi các renderer Mobile và Forward+.

Các hiệu ứng compositor
-----------------------

Các hiệu ứng compositor cho phép bạn chèn logic bổ sung vào pipeline kết xuất ở nhiều giai đoạn khác nhau. Đây là một tính năng nâng cao, đòi hỏi bạn phải hiểu rõ pipeline kết xuất để có thể tận dụng hiệu quả nhất.

Vì logic cốt lõi của hiệu ứng compositor được gọi từ pipeline kết xuất, cần lưu ý rằng logic này sẽ chạy trong thread thực hiện việc kết xuất. Bạn cần cẩn thận để tránh gặp các vấn đề về threading.

Để minh họa cách sử dụng các hiệu ứng compositor, chúng ta sẽ tạo một hiệu ứng post-processing đơn giản, cho phép bạn viết shader code của riêng mình và áp dụng nó lên toàn màn hình thông qua một compute shader. Bạn có thể tìm thấy project demo hoàn chỉnh `here <https://github.com/godotengine/godot-demo-projects/tree/master/compute/post_shader>`_.

Trước tiên, chúng ta tạo một script mới có tên ``post_process_shader.gd``. Chúng ta sẽ biến script này thành một tool script để có thể thấy hiệu ứng compositor hoạt động trong editor. Chúng ta cần mở rộng node từ :ref:`CompositorEffect <class_CompositorEffect>`. Đồng thời, script cũng cần có một class name.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends CompositorEffect
    class_name PostProcessShader

 .. code-tab:: csharp

    [GlobalClass, Tool]
    public partial class PostProcessShader : CompositorEffect

Tiếp theo, chúng ta sẽ định nghĩa một hằng số chứa mã template của shader. Đây là đoạn mã khung giúp compute shader của chúng ta hoạt động.

.. tabs::
 .. code-tab:: gdscript GDScript

    const template_shader: String = """
    #version 450

    // Invocations in the (x, y, z) dimension
    layout(local_size_x = 8, local_size_y = 8, local_size_z = 1) in;

    layout(rgba16f, set = 0, binding = 0) uniform image2D color_image;

    // Our push constant
    layout(push_constant, std430) uniform Params {
        vec2 raster_size;
        vec2 reserved;
    } params;

    // The code we want to execute in each invocation
    void main() {
        ivec2 uv = ivec2(gl_GlobalInvocationID.xy);
        ivec2 size = ivec2(params.raster_size);

        if (uv.x >= size.x || uv.y >= size.y) {
            return;
        }

        vec4 color = imageLoad(color_image, uv);

        #COMPUTE_CODE

        imageStore(color_image, uv, color);
    }
    """

 .. code-tab:: csharp

    private const string _templateShader = @"
    #version 450

    // Các invocation trong chiều (x, y, z)
    layout(local_size_x = 8, local_size_y = 8, local_size_z = 1) in;

    layout(rgba16f, set = 0, binding = 0) uniform image2D color_image;

    // Push constant của chúng ta
    layout(push_constant, std430) uniform Params {
	    vec2 raster_size;
	    vec2 reserved;
    } params;

    // Mã mà chúng ta muốn thực thi trong mỗi invocation
    void main() {
	    ivec2 uv = ivec2(gl_GlobalInvocationID.xy);
	    ivec2 size = ivec2(params.raster_size);

	    if (uv.x >= size.x || uv.y >= size.y) {
		    return;
	    }

	    vec4 color = imageLoad(color_image, uv);

	    #COMPUTE_CODE

	    imageStore(color_image, uv, color);
    }
    ";

Để biết thêm thông tin về cách compute shader hoạt động, hãy xem :ref:`Using compute shaders <doc_compute_shaders>`.

Điểm quan trọng ở đây là với mỗi pixel trên màn hình, hàm ``main`` của chúng ta sẽ được thực thi; bên trong hàm này, chúng ta tải giá trị màu hiện tại của pixel, thực thi mã do người dùng cung cấp, rồi ghi màu đã chỉnh sửa trở lại image màu của chúng ta.

``#COMPUTE_CODE`` sẽ được thay thế bằng mã do người dùng cung cấp.

Để thiết lập mã do người dùng cung cấp, chúng ta cần một biến export. Chúng ta cũng sẽ định nghĩa một vài biến script sẽ sử dụng:

.. tabs::
 .. code-tab:: gdscript GDScript

    @export_multiline var shader_code: String = "":
        set(value):
            mutex.lock()
            shader_code = value
            shader_is_dirty = true
            mutex.unlock()

    var rd: RenderingDevice
    var shader: RID
    var pipeline: RID

    var mutex: Mutex = Mutex.new()
    var shader_is_dirty: bool = true

 .. code-tab:: csharp

    private string _shaderCode = "";
    [Export(PropertyHint.MultilineText)]
    public string ShaderCode
    {
        get { return _shaderCode; }
        set
        {
            _mutex.Lock();
            _shaderCode = value;
            shaderIsDirty = true;
            _mutex.Unlock();
        }
    }

    private RenderingDevice _rd;
    private Rid _shader;
    private Rid _pipeline;

    private Godot.Mutex _mutex = new Godot.Mutex();
    private bool _shaderIsDirty = true;


Lưu ý việc sử dụng :ref:`Mutex <class_Mutex>` trong mã của chúng ta. Phần lớn quá trình triển khai được gọi từ rendering engine và do đó chạy trong rendering thread.

Chúng ta cần đảm bảo thiết lập mã shader mới và đánh dấu mã shader là dirty, nhưng không để render thread truy cập dữ liệu này cùng lúc.

Tiếp theo, chúng ta khởi tạo hiệu ứng.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được gọi khi resource này được khởi tạo.
    func _init():
        effect_callback_type = EFFECT_CALLBACK_TYPE_POST_TRANSPARENT
        rd = RenderingServer.get_rendering_device()

 .. code-tab:: csharp

    // Được gọi khi resource này được khởi tạo.
    public PostProcessShader()
    {
        EffectCallbackType = EffectCallbackTypeEnum.PostTransparent;
        _rd = RenderingServer.GetRenderingDevice();
    }

Điểm chính ở đây là thiết lập ``effect_callback_type``, thông báo cho rendering engine biết cần gọi mã của chúng ta ở giai đoạn nào trong render pipeline.

.. note::

    Hiện tại, chúng ta chỉ có quyền truy cập vào các giai đoạn của 3D rendering pipeline!

Chúng ta cũng nhận được một tham chiếu đến rendering device, thành phần sẽ rất hữu ích.

Chúng ta cũng cần dọn dẹp sau khi hoàn tất; để làm việc này, chúng ta phản hồi notification ``NOTIFICATION_PREDELETE``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Các system notification mà chúng ta muốn phản hồi là notification
    # thông báo rằng chúng ta sắp bị hủy.
    func _notification(what):
        if what == NOTIFICATION_PREDELETE:
            if shader.is_valid():
                # Giải phóng shader cũng sẽ giải phóng mọi đối tượng phụ thuộc, chẳng hạn như pipeline!
                rd.free_rid(shader)

 .. code-tab:: csharp

    // Các system notification mà chúng ta muốn phản hồi là notification
    // thông báo rằng chúng ta sắp bị hủy.
    public override void _Notification(int what)
    {
        if (what == NotificationPredelete)
        {
            if (_shader.IsValid)
            {
                // Giải phóng shader cũng sẽ giải phóng mọi đối tượng phụ thuộc, chẳng hạn như pipeline!
                _rd.FreeRid(_shader);
            }
        }
    }

Lưu ý rằng ở đây chúng ta không sử dụng mutex, dù tạo shader bên trong render thread. Các phương thức trên rendering server đều thread-safe và ``free_rid`` sẽ trì hoãn việc dọn dẹp shader cho đến sau khi mọi frame đang được kết xuất hoàn tất.

Cũng lưu ý rằng chúng ta không giải phóng pipeline. Rendering device thực hiện dependency tracking; vì pipeline phụ thuộc vào shader nên pipeline sẽ được tự động giải phóng khi shader bị hủy.

Kể từ thời điểm này, mã của chúng ta sẽ chạy trên rendering thread.

Bước tiếp theo là một helper function sẽ biên dịch lại shader nếu mã do người dùng cung cấp đã thay đổi.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Kiểm tra xem shader có thay đổi và cần được biên dịch lại hay không.
    func _check_shader() -> bool:
        if not rd:
            return false

        var new_shader_code: String = ""

        # Kiểm tra xem shader có dirty hay không.
        mutex.lock()
        if shader_is_dirty:
            new_shader_code = shader_code
            shader_is_dirty = false
        mutex.unlock()

        # Chúng ta không có shader (mới) sao?
        if new_shader_code.is_empty():
            return pipeline.is_valid()

        # Áp dụng template.
        new_shader_code = _templateShader.replace("#COMPUTE_CODE", new_shader_code);

        # Loại bỏ cái cũ.
        if shader.is_valid():
            rd.free_rid(shader)
            shader = RID()
            pipeline = RID()

        # Đưa cái mới vào.
        var shader_source: RDShaderSource = RDShaderSource.new()
        shader_source.language = RenderingDevice.SHADER_LANGUAGE_GLSL
        shader_source.source_compute = new_shader_code
        var shader_spirv: RDShaderSPIRV = rd.shader_compile_spirv_from_source(shader_source)

        if shader_spirv.compile_error_compute != "":
            push_error(shader_spirv.compile_error_compute)
            push_error("In: " + new_shader_code)
            return false

        shader = rd.shader_create_from_spirv(shader_spirv)
        if not shader.is_valid():
            return false

        pipeline = rd.compute_pipeline_create(shader)
        return pipeline.is_valid()

 .. code-tab:: csharp

    // Kiểm tra xem shader có thay đổi và cần được biên dịch lại hay không.
    public bool CheckShader()
    {
        if (_rd is null)
        {
            return false;
        }

        var newShaderCode = "";

        // Kiểm tra xem shader có dirty hay không.
        _mutex.Lock();
        if (_shaderIsDirty)
        {
            newShaderCode = _shaderCode;
            _shaderIsDirty = false;
        }
        _mutex.Unlock();

        // Chúng ta không có shader (mới) sao?
        if (newShaderCode == "")
        {
            return _pipeline.IsValid;
        }

        // Áp dụng template.
        newShaderCode = _templateShader.Replace("#COMPUTE_CODE", newShaderCode);

        // Loại bỏ cái cũ.
        if (_shader.IsValid)
        {
            _rd.FreeRid(_shader);
            _shader = new Rid();
            _pipeline = new Rid();
        }

        // Đưa cái mới vào.
        RDShaderSource shaderSource = new RDShaderSource();
        shaderSource.Language = RenderingDevice.ShaderLanguage.Glsl;
        shaderSource.SourceCompute = newShaderCode;
        RDShaderSpirV shaderSpirV = _rd.ShaderCompileSpirVFromSource(shaderSource);

        if (shaderSpirV.CompileErrorCompute != "")
        {
            GD.PushError(shaderSpirV.CompileErrorCompute);
            GD.PushError("In: " + newShaderCode);
            return false;
        }
        _shader = _rd.ShaderCreateFromSpirV(shaderSpirV);
        if (!_shader.IsValid)
        {
            return false;
        }

        _pipeline = _rd.ComputePipelineCreate(_shader);
        return _pipeline.IsValid;
    }

Ở đầu phương thức này, chúng ta lại sử dụng mutex để bảo vệ việc truy cập mã shader của người dùng và cờ is dirty. Chúng ta tạo một bản sao cục bộ của mã shader người dùng nếu mã shader người dùng của chúng ta bị dirty.

Nếu không có code fragment mới, chúng ta trả về true nếu đã có một pipeline hợp lệ.

Nếu có code fragment mới, chúng ta nhúng nó vào mã template rồi biên dịch.

.. warning::
    Mã được hiển thị ở đây sẽ biên dịch mã mới của chúng ta trong runtime. Điều này rất hữu ích khi prototype vì chúng ta có thể thấy ngay hiệu ứng của shader đã thay đổi.

    Điều này ngăn shader được biên dịch trước và lưu vào cache, việc có thể gây vấn đề trên một số nền tảng như console. Lưu ý rằng dự án demo đi kèm một ví dụ thay thế, trong đó tệp ``glsl`` chứa toàn bộ compute shader và được sử dụng. Với cách tiếp cận này, Godot có thể biên dịch trước và lưu shader vào cache.

Cuối cùng, chúng ta cần triển khai callback effect; rendering engine sẽ gọi callback này ở giai đoạn thích hợp của quá trình render.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được rendering thread gọi mỗi frame.
    func _render_callback(p_effect_callback_type, p_render_data):
        if rd and p_effect_callback_type == EFFECT_CALLBACK_TYPE_POST_TRANSPARENT and _check_shader():
            # Lấy đối tượng render scene buffers của chúng ta; đối tượng này cho phép truy cập vào các render buffer.
            # Lưu ý rằng implementation khác nhau tùy renderer, do đó cần thực hiện cast.
            var render_scene_buffers: RenderSceneBuffersRD = p_render_data.get_render_scene_buffers()
            if render_scene_buffers:
                # Lấy render size của chúng ta; đây là độ phân giải render 3D!
                var size = render_scene_buffers.get_internal_size()
                if size.x == 0 and size.y == 0:
                    return

                # Có thể sử dụng compute shader ở đây.
                var x_groups = (size.x - 1) / 8 + 1
                var y_groups = (size.y - 1) / 8 + 1
                var z_groups = 1

                # Đẩy push constant.
                var push_constant: PackedFloat32Array = PackedFloat32Array()
                push_constant.push_back(size.x)
                push_constant.push_back(size.y)
                push_constant.push_back(0.0)
                push_constant.push_back(0.0)

                # Duyệt qua các view để đề phòng trường hợp đang thực hiện stereo rendering. Nếu là mono thì không tốn thêm chi phí.
                var view_count = render_scene_buffers.get_view_count()
                for view in range(view_count):
                    # Lấy RID cho color image; chúng ta sẽ đọc và ghi vào image này.
                    var input_image = render_scene_buffers.get_color_layer(view)

                    # Tạo một uniform set.
                    # Uniform set này sẽ được lưu vào cache; cache sẽ bị xóa nếu cấu hình viewport thay đổi.
                    var uniform: RDUniform = RDUniform.new()
                    uniform.uniform_type = RenderingDevice.UNIFORM_TYPE_IMAGE
                    uniform.binding = 0
                    uniform.add_id(input_image)
                    var uniform_set = UniformSetCacheRD.get_cache(shader, 0, [ uniform ])

                    # Chạy compute shader.
                    var compute_list:= rd.compute_list_begin()
                    rd.compute_list_bind_compute_pipeline(compute_list, pipeline)
                    rd.compute_list_bind_uniform_set(compute_list, uniform_set, 0)
                    rd.compute_list_set_push_constant(compute_list, push_constant.to_byte_array(), push_constant.size() * 4)
                    rd.compute_list_dispatch(compute_list, x_groups, y_groups, z_groups)
                    rd.compute_list_end()

 .. code-tab:: csharp

    // Được rendering thread gọi mỗi frame.
    public override void _RenderCallback(int effectCallbackType, RenderData renderData)
    {
        if (_rd is not null && effectCallbackType == (int)EffectCallbackTypeEnum.PostTransparent && CheckShader())
        {
            // Lấy đối tượng render scene buffers của chúng ta; đối tượng này cho phép truy cập vào các render buffer.
            // Lưu ý rằng implementation khác nhau tùy renderer, do đó cần thực hiện cast.

            RenderSceneBuffersRD renderSceneBuffers = renderData.GetRenderSceneBuffers() as RenderSceneBuffersRD;
            if (renderSceneBuffers is not null)
            {
                // Lấy render size của chúng ta; đây là độ phân giải 3D!
                var size = renderSceneBuffers.GetInternalSize();
                if (size.X == 0 && size.Y == 0)
                {
                    return;
                }

                // Có thể sử dụng compute shader ở đây.
                uint xGroups = (uint)((size.X - 1) / 8 + 1);
                uint yGroups = (uint)((size.Y - 1) / 8 + 1);
                uint zGroups = 1;

                // Đẩy Push Constant.
                float[] tempPushConstant = [size.X, size.Y, 0, 0];
                byte[] pushConstant = new byte[tempPushConstant.Length * sizeof(float)];
                Buffer.BlockCopy(tempPushConstant, 0, pushConstant, 0, pushConstant.Length);

                // Duyệt qua các view để đề phòng trường hợp đang thực hiện stereo rendering. Nếu là mono thì không tốn thêm chi phí.
                var viewCount = renderSceneBuffers.GetViewCount();
                for (uint view = 0; view < viewCount; view++)
                {
                    // Lấy RID cho color image; chúng ta sẽ đọc và ghi vào image này.
                    var inputImage = renderSceneBuffers.GetColorLayer(view);

                    // Tạo một uniform set.
                    // Uniform set này sẽ được lưu vào cache; cache sẽ bị xóa nếu cấu hình viewport thay đổi.
                    RDUniform uniform = new RDUniform()
                    {
                        UniformType = RenderingDevice.UniformType.Image,
                        Binding = 0,
                    };
                    uniform.AddId(inputImage);
                    var uniformSet = UniformSetCacheRD.GetCache(_shader, 0, [uniform]);

                    // Chạy compute shader.
                    var computeList = _rd.ComputeListBegin();
                    _rd.ComputeListBindComputePipeline(computeList, _pipeline);
                    _rd.ComputeListBindUniformSet(computeList, uniformSet, 0);
                    _rd.ComputeListSetPushConstant(computeList, pushConstant, (uint)pushConstant.Length);
                    _rd.ComputeListDispatch(computeList, xGroups, yGroups, zGroups);
                    _rd.ComputeListEnd();
            }
        }
    }

Ở đầu phương thức này, chúng ta kiểm tra xem có rendering device hay không, callback type có đúng hay không và có shader hay không.

.. note::

    Việc kiểm tra effect type chỉ là một cơ chế an toàn. Chúng ta đã thiết lập giá trị này trong hàm ``_init``, tuy nhiên người dùng có thể thay đổi giá trị này trong UI.

Tham số ``p_render_data`` cho phép chúng ta truy cập một đối tượng chứa dữ liệu dành riêng cho frame hiện đang được render. Hiện tại chúng ta chỉ quan tâm đến render scene buffers, thành phần cho phép truy cập tất cả buffer nội bộ được rendering engine sử dụng. Lưu ý rằng chúng ta cast thành :ref:`RenderSceneBuffersRD <class_RenderSceneBuffersRD>` để cung cấp toàn bộ API cho dữ liệu này.

Tiếp theo, chúng ta lấy ``internal size``, tức là độ phân giải của các 3D render buffer trước khi được upscale (nếu có); việc upscale diễn ra sau khi các post-process của chúng ta chạy.

Từ kích thước nội bộ, chúng ta tính group size; hãy xem local size trong template shader.

.. UPDATE: Not supported yet. When structs are supported here, update this
.. paragraph.

Chúng ta cũng điền push constant để shader biết kích thước của mình. Godot chưa hỗ trợ struct ở đây **yet**, vì vậy chúng ta sử dụng ``PackedFloat32Array`` để lưu dữ liệu này. Lưu ý rằng chúng ta phải đệm array này để đạt alignment 16 byte. Nói cách khác, độ dài của array phải là bội số của 4.

Bây giờ chúng ta duyệt qua các view, đề phòng trường hợp sử dụng multiview rendering, phù hợp với stereo rendering (XR). Trong hầu hết trường hợp, chúng ta chỉ có một view.

.. note::

    Việc sử dụng multiview cho post-processing ở đây không mang lại lợi ích về hiệu năng; xử lý riêng từng view như thế này vẫn cho phép GPU sử dụng tính song song nếu có lợi.

Tiếp theo, chúng ta lấy color buffer cho view này. Đây là buffer mà 3D scene của chúng ta đã được render vào.

Sau đó, chúng ta chuẩn bị một uniform set để truyền color buffer cho shader.

Lưu ý việc sử dụng :ref:`UniformSetCacheRD <class_UniformSetCacheRD>` cache, giúp chúng ta kiểm tra uniform set ở mỗi frame. Vì color buffer có thể thay đổi từ frame này sang frame khác và uniform cache sẽ tự động dọn dẹp các uniform set khi buffer được giải phóng, đây là cách an toàn để đảm bảo chúng ta không làm rò rỉ bộ nhớ hoặc sử dụng một set đã lỗi thời.

Cuối cùng, chúng ta xây dựng compute list bằng cách bind pipeline, bind uniform set, push dữ liệu push constant và gọi dispatch cho các group.

Sau khi hoàn tất compositor effect, bây giờ chúng ta cần thêm nó vào compositor.

Trong compositor, chúng ta mở rộng thuộc tính compositor effects rồi nhấn ``Add Element``.

Bây giờ chúng ta có thể thêm compositor effect:

.. image:: img/add_compositor_effect.webp

Sau khi chọn ``PostProcessShader``, chúng ta cần đặt user shader code:

.. code-block:: glsl

    float gray = color.r * 0.2125 + color.g * 0.7154 + color.b * 0.0721;
    color.rgb = vec3(gray);

Sau khi hoàn tất, output của chúng ta sẽ ở dạng grayscale.

.. image:: img/post_process_shader.webp

.. note::

    Để xem một ví dụ nâng cao hơn về post effects, hãy xem dự án ví dụ `Radial blur based sky rays <https://github.com/BastiaanOlij/RERadialSunRays>`_ do Bastiaan Olij tạo.

.. _`here`: https://github.com/godotengine/godot-demo-projects/tree/master/compute/post_shader
.. _`Radial blur based sky rays`: https://github.com/BastiaanOlij/RERadialSunRays
