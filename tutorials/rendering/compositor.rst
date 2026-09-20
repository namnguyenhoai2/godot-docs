.. _doc_compositor:

Compositor
==========

Compositor là một tính năng mới trong Godot 4, cho phép kiểm soát rendering pipeline khi render nội dung của một :ref:`Viewport <class_Viewport>`.

Tính năng này có thể được cấu hình trên node :ref:`WorldEnvironment <class_WorldEnvironment>`, khi đó nó áp dụng cho tất cả Viewport; hoặc có thể được cấu hình trên :ref:`Camera3D <class_Camera3D>` và chỉ áp dụng cho Viewport sử dụng camera đó.

Resource :ref:`Compositor <class_Compositor>` được dùng để cấu hình compositor. Để bắt đầu, hãy tạo một compositor mới trên node thích hợp:

.. image:: img/new_compositor.webp

.. note::

    Hiện tại, compositor chỉ được hỗ trợ bởi các renderer Mobile và Forward+.

Compositor effect
-----------------

Compositor effect cho phép bạn chèn logic bổ sung vào rendering pipeline ở nhiều giai đoạn khác nhau. Đây là một tính năng nâng cao, đòi hỏi hiểu biết sâu về rendering pipeline để có thể tận dụng hiệu quả nhất.

Vì logic cốt lõi của compositor effect được gọi từ rendering pipeline, cần lưu ý rằng logic này sẽ chạy trong thread thực hiện việc rendering. Cần cẩn thận để đảm bảo chúng ta không gặp vấn đề về threading.

Để minh họa cách sử dụng compositor effect, chúng ta sẽ tạo một post-processing effect đơn giản, cho phép bạn viết shader code của riêng mình và áp dụng nó trên toàn màn hình thông qua compute shader. Bạn có thể tìm thấy project demo hoàn chỉnh `here <https://github.com/godotengine/godot-demo-projects/tree/master/compute/post_shader>`_.

Trước tiên, chúng ta tạo một script mới có tên ``post_process_shader.gd``. Chúng ta sẽ biến script này thành tool script để có thể thấy compositor effect hoạt động trong editor. Chúng ta cần cho node của mình kế thừa từ :ref:`CompositorEffect <class_CompositorEffect>`. Đồng thời, script cũng phải có class name.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends CompositorEffect
    class_name PostProcessShader

 .. code-tab:: csharp

    [GlobalClass, Tool]
    public partial class PostProcessShader : CompositorEffect

Tiếp theo, chúng ta sẽ định nghĩa một hằng số cho shader template code. Đây là boilerplate code giúp compute shader của chúng ta hoạt động.

.. tabs::
 .. code-tab:: gdscript GDScript

    const template_shader: String = """
    #version 450

    // Các invocation trong chiều (x, y, z)
    layout(local_size_x = 8, local_size_y = 8, local_size_z = 1) in;

    layout(rgba16f, set = 0, binding = 0) uniform image2D color_image;

    // Push constant của chúng ta
    layout(push_constant, std430) uniform Params {
        vec2 raster_size;
        vec2 reserved;
    } params;

    // Code chúng ta muốn thực thi trong mỗi invocation
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

    // Code chúng ta muốn thực thi trong mỗi invocation
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

Điểm quan trọng ở đây là với mỗi pixel trên màn hình, hàm ``main`` của chúng ta sẽ được thực thi. Bên trong hàm này, chúng ta tải giá trị màu hiện tại của pixel, thực thi user code, rồi ghi màu đã được chỉnh sửa trở lại color image.

``#COMPUTE_CODE`` sẽ được thay thế bằng user code của chúng ta.

Để thiết lập user code, chúng ta cần một biến export. Chúng ta cũng sẽ định nghĩa một vài biến của script để sử dụng:

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


Lưu ý việc sử dụng :ref:`Mutex <class_Mutex>` trong code của chúng ta. Phần lớn implementation được gọi từ rendering engine và do đó chạy trong rendering thread.

Chúng ta cần đảm bảo thiết lập shader code mới và đánh dấu shader code là dirty, mà không để render thread truy cập dữ liệu này cùng lúc.

Tiếp theo, chúng ta khởi tạo effect.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được gọi khi resource này được tạo.
    func _init():
        effect_callback_type = EFFECT_CALLBACK_TYPE_POST_TRANSPARENT
        rd = RenderingServer.get_rendering_device()

 .. code-tab:: csharp

    // Được gọi khi resource này được tạo.
    public PostProcessShader()
    {
        EffectCallbackType = EffectCallbackTypeEnum.PostTransparent;
        _rd = RenderingServer.GetRenderingDevice();
    }

Điều quan trọng ở đây là thiết lập ``effect_callback_type``, cho rendering engine biết cần gọi code của chúng ta ở giai đoạn nào trong render pipeline.

.. note::

    Hiện tại, chúng ta chỉ có quyền truy cập vào các giai đoạn của 3D rendering pipeline!

Chúng ta cũng nhận được một reference đến rendering device, thứ sẽ rất hữu ích.

Chúng ta cũng cần dọn dẹp sau khi hoàn tất. Để làm việc này, chúng ta phản hồi ``NOTIFICATION_PREDELETE`` notification:

.. tabs::
 .. code-tab:: gdscript GDScript

    # System notification; chúng ta muốn phản hồi notification cho biết
    # rằng chúng ta sắp bị hủy.
    func _notification(what):
        if what == NOTIFICATION_PREDELETE:
            if shader.is_valid():
                # Việc giải phóng shader cũng sẽ giải phóng mọi dependent như pipeline!
                rd.free_rid(shader)

 .. code-tab:: csharp

    // System notification; chúng ta muốn phản hồi notification cho biết
    // rằng chúng ta sắp bị hủy.
    public override void _Notification(int what)
    {
        if (what == NotificationPredelete)
        {
            if (_shader.IsValid)
            {
                // Việc giải phóng shader cũng sẽ giải phóng mọi dependent như pipeline!
                _rd.FreeRid(_shader);
            }
        }
    }

Lưu ý rằng ở đây chúng ta không sử dụng mutex, dù tạo shader bên trong render thread. Các method trên rendering server đều thread-safe và ``free_rid`` sẽ trì hoãn việc dọn dẹp shader cho đến khi mọi frame đang được render hoàn tất.

Cũng lưu ý rằng chúng ta không giải phóng pipeline. Rendering device thực hiện dependency tracking và vì pipeline phụ thuộc vào shader, nó sẽ tự động được giải phóng khi shader bị hủy.

Từ thời điểm này trở đi, code của chúng ta sẽ chạy trên rendering thread.

Bước tiếp theo là một helper function để biên dịch lại shader nếu user code đã thay đổi.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Kiểm tra xem shader của chúng ta có thay đổi và cần được biên dịch lại hay không.
    func _check_shader() -> bool:
        if not rd:
            return false

        var new_shader_code: String = ""

        # Kiểm tra xem shader của chúng ta có dirty hay không.
        mutex.lock()
        if shader_is_dirty:
            new_shader_code = shader_code
            shader_is_dirty = false
        mutex.unlock()

        # Chúng ta không có shader (mới)?
        if new_shader_code.is_empty():
            return pipeline.is_valid()

        # Áp dụng template.
        new_shader_code = _templateShader.replace("#COMPUTE_CODE", new_shader_code);

        # Loại bỏ shader cũ.
        if shader.is_valid():
            rd.free_rid(shader)
            shader = RID()
            pipeline = RID()

        # Đưa shader mới vào.
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

    // Kiểm tra xem shader của chúng ta có thay đổi và cần được biên dịch lại hay không.
    public bool CheckShader()
    {
        if (_rd is null)
        {
            return false;
        }

        var newShaderCode = "";

        // Kiểm tra xem shader của chúng ta có dirty hay không.
        _mutex.Lock();
        if (_shaderIsDirty)
        {
            newShaderCode = _shaderCode;
            _shaderIsDirty = false;
        }
        _mutex.Unlock();

        // Chúng ta không có shader (mới)?
        if (newShaderCode == "")
        {
            return _pipeline.IsValid;
        }

        // Áp dụng template.
        newShaderCode = _templateShader.Replace("#COMPUTE_CODE", newShaderCode);

        // Loại bỏ shader cũ.
        if (_shader.IsValid)
        {
            _rd.FreeRid(_shader);
            _shader = new Rid();
            _pipeline = new Rid();
        }

        // Đưa shader mới vào.
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

Ở đầu method này, chúng ta lại sử dụng mutex để bảo vệ việc truy cập user shader code và cờ is dirty. Nếu user shader code của chúng ta dirty, chúng ta tạo một bản sao cục bộ của nó.

Nếu không có code fragment mới, chúng ta trả về true nếu đã có một pipeline hợp lệ.

Nếu có code fragment mới, chúng ta nhúng nó vào template code rồi biên dịch.

.. warning::
    Code được hiển thị ở đây biên dịch code mới trong runtime. Điều này rất hữu ích cho việc prototyping, vì chúng ta có thể thấy ngay hiệu ứng của shader đã thay đổi.

    Điều này ngăn việc precompile và caching shader, vốn có thể gây vấn đề trên một số nền tảng như console. Lưu ý rằng project demo đi kèm một ví dụ thay thế, trong đó file ``glsl`` chứa toàn bộ compute shader và được sử dụng. Với cách tiếp cận này, Godot có thể precompile và cache shader.

Cuối cùng, chúng ta cần implement effect callback; rendering engine sẽ gọi callback này ở đúng giai đoạn của quá trình rendering.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được rendering thread gọi mỗi frame.
    func _render_callback(p_effect_callback_type, p_render_data):
        if rd and p_effect_callback_type == EFFECT_CALLBACK_TYPE_POST_TRANSPARENT and _check_shader():
            # Lấy render scene buffers object; object này cho phép chúng ta truy cập render buffers.
            # Note that implementation differs per renderer hence the need for the cast.
            var render_scene_buffers: RenderSceneBuffersRD = p_render_data.get_render_scene_buffers()
            if render_scene_buffers:
                # Lấy render size; đây là độ phân giải 3D render!
                var size = render_scene_buffers.get_internal_size()
                if size.x == 0 and size.y == 0:
                    return

                # Ở đây chúng ta có thể sử dụng compute shader.
                var x_groups = (size.x - 1) / 8 + 1
                var y_groups = (size.y - 1) / 8 + 1
                var z_groups = 1

                # Push constant.
                var push_constant: PackedFloat32Array = PackedFloat32Array()
                push_constant.push_back(size.x)
                push_constant.push_back(size.y)
                push_constant.push_back(0.0)
                push_constant.push_back(0.0)

                # Lặp qua các view phòng trường hợp chúng ta đang thực hiện stereo rendering. Nếu là mono thì không phát sinh chi phí bổ sung.
                var view_count = render_scene_buffers.get_view_count()
                for view in range(view_count):
                    # Lấy RID của color image; chúng ta sẽ đọc và ghi dữ liệu vào image này.
                    var input_image = render_scene_buffers.get_color_layer(view)

                    # Tạo một uniform set.
                    # Uniform set này sẽ được cache; cache sẽ bị xóa nếu cấu hình viewport thay đổi.
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
            // Lấy render scene buffers object; object này cho phép chúng ta truy cập render buffers.
            // Note that implementation differs per renderer hence the need for the cast.

            RenderSceneBuffersRD renderSceneBuffers = renderData.GetRenderSceneBuffers() as RenderSceneBuffersRD;
            if (renderSceneBuffers is not null)
            {
                // Lấy render size; đây là độ phân giải 3D!
                var size = renderSceneBuffers.GetInternalSize();
                if (size.X == 0 && size.Y == 0)
                {
                    return;
                }

                // Ở đây chúng ta có thể sử dụng compute shader.
                uint xGroups = (uint)((size.X - 1) / 8 + 1);
                uint yGroups = (uint)((size.Y - 1) / 8 + 1);
                uint zGroups = 1;

                // Push Constant.
                float[] tempPushConstant = [size.X, size.Y, 0, 0];
                byte[] pushConstant = new byte[tempPushConstant.Length * sizeof(float)];
                Buffer.BlockCopy(tempPushConstant, 0, pushConstant, 0, pushConstant.Length);

                // Lặp qua các view phòng trường hợp chúng ta đang thực hiện stereo rendering. Nếu là mono thì không phát sinh chi phí bổ sung.
                var viewCount = renderSceneBuffers.GetViewCount();
                for (uint view = 0; view < viewCount; view++)
                {
                    // Lấy RID của color image; chúng ta sẽ đọc và ghi dữ liệu vào image này.
                    var inputImage = renderSceneBuffers.GetColorLayer(view);

                    // Tạo một uniform set.
                    // Uniform set này sẽ được cache; cache sẽ bị xóa nếu cấu hình viewport thay đổi.
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

Ở đầu method này, chúng ta kiểm tra xem có rendering device hay không, callback type có chính xác hay không, và có shader hay không.

.. note::

    Việc kiểm tra effect type chỉ là một cơ chế an toàn. Chúng ta đã thiết lập giá trị này trong function ``_init``, tuy nhiên người dùng vẫn có thể thay đổi nó trong UI.

Tham số ``p_render_data`` cho phép chúng ta truy cập một object chứa dữ liệu cụ thể của frame hiện đang được render. Hiện tại, chúng ta chỉ quan tâm đến render scene buffers, vốn cho phép truy cập tất cả buffer nội bộ được rendering engine sử dụng. Lưu ý rằng chúng ta cast tham số này sang :ref:`RenderSceneBuffersRD <class_RenderSceneBuffersRD>` để expose toàn bộ API của dữ liệu này.

Tiếp theo, chúng ta lấy ``internal size``, là độ phân giải của 3D render buffers trước khi được upscale (nếu có). Việc upscaling diễn ra sau khi các post-process của chúng ta chạy.

Từ kích thước nội bộ, chúng ta tính group size; hãy xem local size trong template shader.

.. CẬP NHẬT: Hiện chưa được hỗ trợ. Khi struct được hỗ trợ ở đây, hãy cập nhật đoạn văn này. ..

Chúng ta cũng điền push constant để shader biết kích thước của mình. Godot **vẫn chưa** hỗ trợ struct ở đây, vì vậy chúng ta sử dụng ``PackedFloat32Array`` để lưu dữ liệu này. Lưu ý rằng chúng ta phải pad array này theo alignment 16 byte. Nói cách khác, độ dài của array phải là bội số của 4.

Bây giờ chúng ta lặp qua các view, phòng trường hợp sử dụng multiview rendering, vốn áp dụng cho stereo rendering (XR). Trong hầu hết trường hợp, chúng ta sẽ chỉ có một view.

.. note::

    Ở đây, việc sử dụng multiview cho post processing không mang lại lợi ích về hiệu năng; việc xử lý riêng từng view như thế này vẫn cho phép GPU sử dụng tính song song nếu có lợi.

Tiếp theo, chúng ta lấy color buffer cho view này. Đây là buffer mà scene 3D của chúng ta đã được render vào.

Sau đó, chúng ta chuẩn bị một uniform set để có thể truyền color buffer đến shader.

Lưu ý việc sử dụng cache :ref:`UniformSetCacheRD <class_UniformSetCacheRD>` của chúng ta, giúp đảm bảo rằng chúng ta có thể kiểm tra uniform set ở mỗi frame. Vì color buffer của chúng ta có thể thay đổi từ frame này sang frame khác và uniform cache sẽ tự động dọn dẹp các uniform set khi buffer được giải phóng, đây là cách an toàn để đảm bảo chúng ta không làm rò rỉ bộ nhớ hoặc sử dụng một set đã lỗi thời.

Cuối cùng, chúng ta xây dựng compute list bằng cách binding pipeline, binding uniform set, đẩy dữ liệu push constant và gọi dispatch cho các group.

Sau khi hoàn tất compositor effect, giờ chúng ta cần thêm nó vào compositor.

Trong compositor, chúng ta mở rộng thuộc tính compositor effects và nhấn ``Add Element``.

Bây giờ chúng ta có thể thêm compositor effect của mình:

.. image:: img/add_compositor_effect.webp

Sau khi chọn ``PostProcessShader``, chúng ta cần thiết lập user shader code:

.. code-block:: glsl

    float gray = color.r * 0.2125 + color.g * 0.7154 + color.b * 0.0721;
    color.rgb = vec3(gray);

Sau khi hoàn tất mọi thứ, output của chúng ta ở dạng grayscale.

.. image:: img/post_process_shader.webp

.. note::

    Để xem một ví dụ nâng cao hơn về post effects, hãy tham khảo project mẫu `Radial blur based sky rays <https://github.com/BastiaanOlij/RERadialSunRays>`_ do Bastiaan Olij tạo.
