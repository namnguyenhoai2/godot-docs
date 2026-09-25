.. _doc_compute_shaders:

Sử dụng compute shader
======================

Tutorial này sẽ hướng dẫn bạn từng bước tạo một compute shader tối giản. Nhưng trước tiên, hãy tìm hiểu một chút về compute shader và cách chúng hoạt động với Godot.

.. note::

   Tutorial này giả định rằng bạn đã quen thuộc với shader nói chung. Nếu bạn mới làm quen với shader, hãy đọc :ref:`doc_introduction_to_shaders` và :ref:`shader đầu tiên của bạn <toc-your-first-shader>` trước khi tiếp tục tutorial này.

Compute shader là một loại shader program đặc biệt, hướng đến lập trình đa dụng. Nói cách khác, chúng linh hoạt hơn vertex shader và fragment shader vì không có mục đích cố định (ví dụ: biến đổi vertex hoặc ghi màu vào một hình ảnh). Không giống fragment shader và vertex shader, compute shader có rất ít hoạt động diễn ra ngầm. Mã bạn viết chính là thứ GPU chạy và hầu như không có gì khác. Điều này khiến chúng trở thành một công cụ rất hữu ích để chuyển các phép tính nặng sang GPU.

Bây giờ, hãy bắt đầu bằng cách tạo một compute shader ngắn.

Trước tiên, trong trình soạn thảo văn bản **bên ngoài** mà bạn chọn, hãy tạo một tệp mới có tên ``compute_example.glsl`` trong thư mục dự án. Khi viết compute shader trong Godot, bạn viết trực tiếp bằng GLSL. Ngôn ngữ shader của Godot dựa trên GLSL. Nếu bạn đã quen với shader thông thường trong Godot, cú pháp bên dưới sẽ trông khá quen thuộc.

.. note::

   Compute shader chỉ có thể được sử dụng từ các renderer dựa trên RenderingDevice (renderer Forward+ hoặc Mobile). Để làm theo tutorial này, hãy đảm bảo bạn đang sử dụng renderer Forward+ hoặc Mobile. Thiết lập này nằm ở góc trên bên phải của editor.

   Lưu ý rằng khả năng hỗ trợ compute shader nhìn chung khá kém trên các thiết bị di động (do lỗi driver), ngay cả khi về mặt kỹ thuật chúng được hỗ trợ.

Hãy xem đoạn mã compute shader này:

.. code-block:: glsl

    #[compute]
    #version 450

    // Các invocation trong chiều (x, y, z)
    layout(local_size_x = 2, local_size_y = 1, local_size_z = 1) in;

    // Một binding đến buffer mà chúng ta tạo trong script
    layout(set = 0, binding = 0, std430) restrict buffer MyDataBuffer {
        float data[];
    }
    my_data_buffer;

    // Mã mà chúng ta muốn thực thi trong mỗi invocation
    void main() {
        // gl_GlobalInvocationID.x xác định duy nhất invocation này trên tất cả workgroup
        my_data_buffer.data[gl_GlobalInvocationID.x] *= 2.0;
    }

Đoạn mã này nhận một mảng số thực, nhân mỗi phần tử với 2 rồi lưu kết quả trở lại mảng buffer. Bây giờ, hãy xem xét từng dòng.

.. code-block:: glsl

    #[compute]
    #version 450

Hai dòng này truyền đạt hai điều:

 1. Đoạn mã sau đây là một compute shader. Đây là một gợi ý dành riêng cho Godot, cần thiết để editor có thể import tệp shader đúng cách.
 2. Mã đang sử dụng GLSL phiên bản 450.

Bạn không bao giờ phải thay đổi hai dòng này cho các compute shader tùy chỉnh của mình.

.. code-block:: glsl

    // Các invocation trong chiều (x, y, z)
    layout(local_size_x = 2, local_size_y = 1, local_size_z = 1) in;

Tiếp theo, chúng ta khai báo số lượng invocation sẽ được sử dụng trong mỗi workgroup. Invocation là các instance của shader đang chạy trong cùng một workgroup. Khi khởi chạy compute shader từ CPU, chúng ta cho shader biết cần chạy bao nhiêu workgroup. Các workgroup chạy song song với nhau. Trong khi chạy một workgroup, bạn không thể truy cập thông tin trong workgroup khác. Tuy nhiên, các invocation trong cùng một workgroup có thể truy cập có giới hạn đến các invocation khác.

Hãy hình dung workgroup và invocation như một vòng lặp ``for`` lồng nhau khổng lồ.

.. code-block:: glsl

    for (int x = 0; x < workgroup_size_x; x++) {
      for (int y = 0; y < workgroup_size_y; y++) {
         for (int z = 0; z < workgroup_size_z; z++) {
            // Mỗi workgroup chạy độc lập và song song.
            for (int local_x = 0; local_x < invocation_size_x; local_x++) {
               for (int local_y = 0; local_y < invocation_size_y; local_y++) {
                  for (int local_z = 0; local_z < invocation_size_z; local_z++) {
                     // Compute shader chạy ở đây.
                  }
               }
            }
         }
      }
    }


Workgroup và invocation là một chủ đề nâng cao. Hiện tại, hãy nhớ rằng chúng ta sẽ chạy hai invocation trong mỗi workgroup.

.. code-block:: glsl

    // Một binding đến buffer mà chúng ta tạo trong script
    layout(set = 0, binding = 0, std430) restrict buffer MyDataBuffer {
        float data[];
    }
    my_data_buffer;

Ở đây, chúng ta cung cấp thông tin về vùng nhớ mà compute shader có quyền truy cập. Thuộc tính ``layout`` cho phép chúng ta cho shader biết nơi cần tìm buffer; sau đó, chúng ta sẽ cần khớp các vị trí ``set`` và ``binding`` này ở phía CPU.

Từ khóa ``restrict`` cho shader biết rằng buffer này chỉ được truy cập từ một vị trí trong shader này. Nói cách khác, chúng ta sẽ không binding buffer này ở một chỉ mục ``set`` hoặc ``binding`` khác. Điều này rất quan trọng vì cho phép trình biên dịch shader tối ưu hóa mã shader. Luôn sử dụng ``restrict`` khi có thể.

Đây là một buffer *không có kích thước cố định*, nghĩa là nó có thể có kích thước bất kỳ. Vì vậy, chúng ta cần cẩn thận để không đọc từ một chỉ mục lớn hơn kích thước của buffer.

.. code-block:: glsl

    // Mã mà chúng ta muốn thực thi trong mỗi invocation
    void main() {
        // gl_GlobalInvocationID.x xác định duy nhất invocation này trên tất cả workgroup
        my_data_buffer.data[gl_GlobalInvocationID.x] *= 2.0;
    }

Cuối cùng, chúng ta viết hàm ``main``, nơi diễn ra toàn bộ logic. Chúng ta truy cập một vị trí trong storage buffer bằng các biến dựng sẵn ``gl_GlobalInvocationID``. ``gl_GlobalInvocationID`` cung cấp ID duy nhất toàn cục của invocation hiện tại.

Để tiếp tục, hãy viết đoạn mã ở trên vào tệp ``compute_example.glsl`` mới tạo.

Tạo RenderingDevice cục bộ
--------------------------

Để tương tác với và thực thi một compute shader, chúng ta cần một script. Hãy tạo một script mới bằng ngôn ngữ bạn chọn và gắn nó vào bất kỳ Node nào trong scene.

Bây giờ, để thực thi shader, chúng ta cần một :ref:`class_RenderingDevice` cục bộ, có thể được tạo bằng :ref:`class_RenderingServer`:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo rendering device cục bộ.
    var rd := RenderingServer.create_local_rendering_device()

 .. code-tab:: csharp

    // Tạo rendering device cục bộ.
    var rd = RenderingServer.CreateLocalRenderingDevice();

Sau đó, chúng ta có thể tải tệp shader mới tạo ``compute_example.glsl`` và tạo phiên bản đã biên dịch trước bằng đoạn mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tải shader GLSL
    var shader_file := load("res://compute_example.glsl")
    var shader_spirv: RDShaderSPIRV = shader_file.get_spirv()
    var shader := rd.shader_create_from_spirv(shader_spirv)

 .. code-tab:: csharp

    // Tải shader GLSL
    var shaderFile = GD.Load<RDShaderFile>("res://compute_example.glsl");
    var shaderBytecode = shaderFile.GetSpirV();
    var shader = rd.ShaderCreateFromSpirV(shaderBytecode);

.. warning::

    Không thể debug RenderingDevice cục bộ bằng các công cụ như `RenderDoc <https://renderdoc.org/>`__.

Cung cấp dữ liệu đầu vào
------------------------

Có thể bạn còn nhớ, chúng ta muốn truyền một mảng đầu vào vào shader, nhân mỗi phần tử với 2 và nhận kết quả.

Chúng ta cần tạo một buffer để truyền các giá trị vào compute shader. Vì đang làm việc với một mảng số thực, chúng ta sẽ sử dụng storage buffer cho ví dụ này. Storage buffer nhận một mảng byte và cho phép CPU truyền dữ liệu đến và đi từ GPU.

Vậy hãy khởi tạo một mảng các số thực và tạo một storage buffer:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Chuẩn bị dữ liệu. Chúng ta sử dụng số thực trong shader, vì vậy cần 32 bit.
    var input := PackedFloat32Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
    var input_bytes := input.to_byte_array()

    # Tạo một storage buffer có thể chứa các giá trị số thực.
    # Mỗi số thực có 4 byte (32 bit), vì vậy 10 x 4 = 40 byte
    var buffer := rd.storage_buffer_create(input_bytes.size(), input_bytes)

 .. code-tab:: csharp

    // Chuẩn bị dữ liệu. Chúng ta sử dụng số thực trong shader, vì vậy cần 32 bit.
    float[] input = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    var inputBytes = new byte[input.Length * sizeof(float)];
    Buffer.BlockCopy(input, 0, inputBytes, 0, inputBytes.Length);

    // Tạo một storage buffer có thể chứa các giá trị số thực.
    // Mỗi số thực có 4 byte (32 bit), vì vậy 10 x 4 = 40 byte
    var buffer = rd.StorageBufferCreate((uint)inputBytes.Length, inputBytes);

Sau khi đã có buffer, chúng ta cần cho rendering device biết phải sử dụng buffer này. Để làm vậy, chúng ta cần tạo một uniform (giống như trong các shader thông thường) và gán nó vào một uniform set mà sau đó có thể truyền cho shader.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo một uniform để gán buffer cho rendering device
    var uniform := RDUniform.new()
    uniform.uniform_type = RenderingDevice.UNIFORM_TYPE_STORAGE_BUFFER
    uniform.binding = 0 # điều này cần khớp với "binding" trong tệp shader của chúng ta
    uniform.add_id(buffer)
    var uniform_set := rd.uniform_set_create([uniform], shader, 0) # tham số cuối cùng (giá trị 0) cần khớp với "set" trong tệp shader của chúng ta

 .. code-tab:: csharp

    // Tạo một uniform để gán buffer cho rendering device
    var uniform = new RDUniform
    {
        UniformType = RenderingDevice.UniformType.StorageBuffer,
        Binding = 0
    };
    uniform.AddId(buffer);
    var uniformSet = rd.UniformSetCreate([uniform], shader, 0);


Định nghĩa compute pipeline
---------------------------

Bước tiếp theo là tạo một tập hợp các chỉ dẫn mà GPU có thể thực thi. Để làm vậy, chúng ta cần một pipeline và một compute list.

Các bước cần thực hiện để tính toán kết quả là:

1. Tạo một pipeline mới.
2. Bắt đầu một danh sách các chỉ dẫn để GPU thực thi.
3. Gắn compute list vào pipeline
4. Gắn buffer uniform vào pipeline
5. Chỉ định số workgroup cần sử dụng
6. Kết thúc danh sách các chỉ dẫn

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo một compute pipeline
    var pipeline := rd.compute_pipeline_create(shader)
    var compute_list := rd.compute_list_begin()
    rd.compute_list_bind_compute_pipeline(compute_list, pipeline)
    rd.compute_list_bind_uniform_set(compute_list, uniform_set, 0)
    rd.compute_list_dispatch(compute_list, 5, 1, 1)
    rd.compute_list_end()

 .. code-tab:: csharp

    // Tạo một compute pipeline
    var pipeline = rd.ComputePipelineCreate(shader);
    var computeList = rd.ComputeListBegin();
    rd.ComputeListBindComputePipeline(computeList, pipeline);
    rd.ComputeListBindUniformSet(computeList, uniformSet, 0);
    rd.ComputeListDispatch(computeList, xGroups: 5, yGroups: 1, zGroups: 1);
    rd.ComputeListEnd();

Lưu ý rằng chúng ta đang dispatch compute shader với 5 workgroup trên trục X và 1 workgroup trên mỗi trục còn lại. Vì chúng ta có 2 local invocation trên trục X (được chỉ định trong shader), tổng cộng sẽ có 10 compute shader invocation được khởi chạy. Nếu đọc hoặc ghi vào các chỉ mục nằm ngoài phạm vi của buffer, bạn có thể truy cập vào vùng bộ nhớ nằm ngoài quyền kiểm soát của shader hoặc các phần của biến khác, điều này có thể gây ra sự cố trên một số phần cứng.

Thực thi compute shader
-----------------------

Sau tất cả các bước này, chúng ta gần hoàn tất, nhưng vẫn cần thực thi pipeline. Cho đến lúc này, chúng ta mới chỉ ghi lại những gì muốn GPU thực hiện; chương trình shader thực tế vẫn chưa chạy.

Để thực thi compute shader, chúng ta cần gửi pipeline đến GPU và chờ quá trình thực thi hoàn tất:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Gửi đến GPU và chờ đồng bộ hóa
    rd.submit()
    rd.sync()

 .. code-tab:: csharp

    // Gửi đến GPU và chờ đồng bộ hóa
    rd.Submit();
    rd.Sync();

Lý tưởng nhất là bạn không nên gọi ``sync()`` để đồng bộ hóa RenderingDevice ngay lập tức, vì điều đó sẽ khiến CPU phải chờ GPU hoàn thành công việc. Trong ví dụ này, chúng ta đồng bộ hóa ngay vì muốn dữ liệu sẵn sàng để đọc ngay lập tức. Nhìn chung, bạn nên chờ *ít nhất* 2 hoặc 3 frame trước khi đồng bộ hóa để GPU có thể chạy song song với CPU.

.. warning::

    Các phép tính dài có thể khiến driver đồ họa của Windows "crash" do
    :abbr:`TDR (Timeout Detection and Recovery)` được Windows kích hoạt. Đây là một cơ chế khởi tạo lại driver đồ họa sau khi không có hoạt động nào từ driver đồ họa trong một khoảng thời gian nhất định (thường là 5 đến 10 giây).

    Tùy thuộc vào thời gian thực thi của compute shader, bạn có thể cần chia shader thành nhiều dispatch để giảm thời gian của mỗi dispatch và giảm khả năng kích hoạt TDR. Vì TDR phụ thuộc vào thời gian, các GPU chậm hơn có thể dễ gặp TDR hơn khi chạy một compute shader nhất định so với GPU nhanh hơn.

Truy xuất kết quả
-----------------

Có thể bạn đã nhận thấy rằng trong shader mẫu, chúng ta đã sửa đổi nội dung của storage buffer. Nói cách khác, shader đọc từ mảng của chúng ta rồi lưu dữ liệu trở lại chính mảng đó, vì vậy kết quả đã có sẵn. Hãy truy xuất dữ liệu và in kết quả ra console.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Đọc lại dữ liệu từ buffer
    var output_bytes := rd.buffer_get_data(buffer)
    var output := output_bytes.to_float32_array()
    print("Input: ", input)
    print("Output: ", output)

 .. code-tab:: csharp

    // Đọc lại dữ liệu từ các buffer
    var outputBytes = rd.BufferGetData(buffer);
    var output = new float[input.Length];
    Buffer.BlockCopy(outputBytes, 0, output, 0, outputBytes.Length);
    GD.Print("Input: ", string.Join(", ", input));
    GD.Print("Output: ", string.Join(", ", output));

Giải phóng bộ nhớ
-----------------

Các biến ``buffer``, ``pipeline`` và ``uniform_set`` mà chúng ta đã sử dụng đều là một :ref:`class_RID`. Vì RenderingDevice được thiết kế như một API cấp thấp hơn, các RID không được tự động giải phóng. Điều này có nghĩa là khi sử dụng xong ``buffer`` hoặc bất kỳ RID nào khác, bạn phải tự giải phóng bộ nhớ của nó bằng cách sử dụng
:ref:`free_rid()<class_RenderingDevice_method_free_rid>` method.

Như vậy, bạn đã có mọi thứ cần thiết để bắt đầu làm việc với compute shader.

.. seealso::

   Kho lưu trữ các dự án demo có một `Compute Shader Heightmap demo <https://github.com/godotengine/godot-demo-projects/tree/master/compute/heightmap>`__ Dự án này thực hiện việc tạo ảnh heightmap riêng biệt trên CPU và GPU, cho phép bạn so sánh cách triển khai một thuật toán tương tự theo hai cách khác nhau (trong hầu hết trường hợp, cách triển khai trên GPU sẽ nhanh hơn).
