.. _doc_introduction_to_shaders:

Giới thiệu về shader
====================

Trang này giải thích shader là gì và cung cấp cho bạn cái nhìn tổng quan về cách chúng hoạt động trong Godot. Để xem tài liệu tham khảo chi tiết về ngôn ngữ shading của engine, hãy xem
:ref:`doc_shading_language`.

Shader là một loại chương trình đặc biệt chạy trên Bộ xử lý đồ họa (GPU). Ban đầu, chúng được dùng để tạo bóng cho các cảnh 3D, nhưng ngày nay chúng có thể làm được nhiều hơn thế. Bạn có thể dùng chúng để kiểm soát cách engine vẽ hình học và pixel trên màn hình, cho phép bạn tạo ra đủ loại hiệu ứng.

Các engine kết xuất hiện đại như Godot vẽ mọi thứ bằng shader: card đồ họa có thể chạy hàng nghìn lệnh song song, mang lại tốc độ kết xuất đáng kinh ngạc.

Tuy nhiên, do có tính chất song song, shader không xử lý thông tin theo cách một chương trình thông thường thực hiện. Mã shader chạy độc lập trên từng vertex hoặc pixel. Bạn cũng không thể lưu trữ dữ liệu giữa các frame. Vì vậy, khi làm việc với shader, bạn cần lập trình và tư duy khác với các ngôn ngữ lập trình khác.

Giả sử bạn muốn cập nhật tất cả pixel trong một texture thành một màu nhất định. Trong GDScript, mã của bạn sẽ sử dụng các vòng lặp ``for``:

::

    for x in range(width):
        for y in range(height):
            set_color(x, y, some_color)

Mã của bạn đã là một phần của vòng lặp trong shader, vì vậy mã tương ứng sẽ như sau.

.. code-block:: glsl

    shader_type canvas_item;

    void fragment() {
        COLOR = some_color;
    }

.. note::

   Card đồ họa gọi hàm ``fragment()`` một hoặc nhiều lần cho mỗi pixel mà nó phải vẽ. Nội dung này sẽ được giải thích thêm bên dưới.

Shader trong Godot
------------------

Godot cung cấp một ngôn ngữ shading dựa trên OpenGL Shading Language (GLSL) phổ biến nhưng được đơn giản hóa. Engine xử lý một phần công việc khởi tạo ở mức thấp cho bạn, giúp việc viết các shader phức tạp dễ dàng hơn.

Trong Godot, shader bao gồm các hàm main được gọi là "hàm xử lý". Hàm xử lý là điểm bắt đầu để shader của bạn đi vào chương trình. Có bảy hàm xử lý khác nhau.

1. Hàm ``vertex()`` chạy trên tất cả vertex trong mesh và thiết lập vị trí của chúng cùng một số biến khác trên từng vertex. Được sử dụng trong
   :ref:`shader canvas_item <doc_canvas_item_shader>` và
   :ref:`shader spatial <doc_spatial_shader>`.

2. Hàm ``fragment()`` chạy trên mọi pixel được mesh phủ lên. Hàm này sử dụng các giá trị do hàm ``vertex()`` xuất ra, được nội suy giữa các vertex. Được sử dụng trong :ref:`shader canvas_item <doc_canvas_item_shader>` và
   :ref:`shader spatial <doc_spatial_shader>`.

3. Hàm ``light()`` chạy trên từng pixel và từng nguồn sáng. Hàm này nhận các biến từ hàm ``fragment()`` và từ những lần chạy trước đó của chính nó. Được sử dụng trong :ref:`shader canvas_item <doc_canvas_item_shader>` và
   :ref:`shader spatial <doc_spatial_shader>`.

4. Hàm ``start()`` chạy một lần cho mỗi particle trong hệ thống particle khi particle đó được tạo lần đầu. Được sử dụng trong
   :ref:`shader particles <doc_particle_shader>`.

5. Hàm ``process()`` chạy trên mỗi particle trong hệ thống particle ở mỗi frame. Được sử dụng trong :ref:`shader particles <doc_particle_shader>`.

6. Hàm ``sky()`` chạy trên mỗi pixel trong radiance cubemap khi radiance cubemap cần được cập nhật, và trên mỗi pixel của màn hình hiện tại. Được sử dụng trong :ref:`shader sky <doc_sky_shader>`.

7. Hàm ``fog()`` chạy trên mỗi froxel trong bộ đệm froxel của volumetric fog giao với :ref:`FogVolume <class_FogVolume>`. Được sử dụng bởi
   :ref:`shader fog <doc_fog_shader>`.

.. warning::

    Hàm ``light()`` sẽ không chạy nếu render mode ``vertex_lighting`` được bật, hoặc nếu **Rendering > Quality > Shading > Force Vertex Shading** được bật trong Project Settings. Tùy chọn này được bật theo mặc định trên các nền tảng di động.

.. note::

   Godot cũng cung cấp một API để người dùng viết các shader GLSL hoàn toàn tùy chỉnh. Để biết thêm thông tin, hãy xem :ref:`doc_compute_shaders`.

Các loại shader
---------------

Thay vì cung cấp một cấu hình dùng chung cho mọi mục đích (2D, 3D, particle, sky, fog), bạn phải chỉ định loại shader mình đang viết. Các loại khác nhau hỗ trợ những render mode, biến tích hợp và hàm xử lý khác nhau.

Trong Godot, tất cả shader cần chỉ định loại của chúng ở dòng đầu tiên, như sau:

.. code-block:: glsl

    shader_type spatial;

Các loại có sẵn gồm:

* :ref:`spatial <doc_spatial_shader>` để kết xuất 3D.
* :ref:`canvas_item <doc_canvas_item_shader>` để kết xuất 2D.
* :ref:`particles <doc_particle_shader>` cho các hệ thống particle.
* :ref:`sky <doc_sky_shader>` để kết xuất :ref:`Skies <class_Sky>`.
* :ref:`fog <doc_fog_shader>` để kết xuất :ref:`FogVolumes <class_FogVolume>`.
* :ref:`texture_blit <doc_texture_blit_shader>` để kết xuất :ref:`DrawableTexture2Ds <class_DrawableTexture2D>`.

Render mode
-----------

Shader có các render mode tùy chọn mà bạn có thể chỉ định ở dòng thứ hai, sau loại shader, như sau:

.. code-block:: glsl

    shader_type spatial;
    render_mode unshaded, cull_disabled;

Render mode thay đổi cách Godot áp dụng shader. Ví dụ, mode ``unshaded`` khiến engine bỏ qua hàm xử lý ánh sáng tích hợp.

Mỗi loại shader có các render mode khác nhau. Hãy xem tài liệu tham khảo của từng loại shader để biết danh sách đầy đủ các render mode.

Bộ xử lý vertex
~~~~~~~~~~~~~~~

Hàm xử lý ``vertex()`` được gọi một lần cho mỗi vertex trong shader ``spatial`` và ``canvas_item``.

Mỗi vertex trong hình học của thế giới có các thuộc tính như vị trí và màu sắc. Hàm này sửa đổi các giá trị đó rồi truyền chúng cho hàm fragment. Bạn cũng có thể dùng nó để gửi thêm dữ liệu cho hàm fragment bằng varying.

Theo mặc định, Godot biến đổi thông tin vertex cho bạn; đây là việc cần thiết để chiếu hình học lên màn hình. Bạn có thể dùng render mode để tự biến đổi dữ liệu; xem :ref:`tài liệu shader Spatial <doc_spatial_shader>` để biết ví dụ.

Bộ xử lý fragment
~~~~~~~~~~~~~~~~~

Hàm xử lý ``fragment()`` được dùng để thiết lập các tham số material của Godot cho từng pixel. Mã này chạy trên mọi pixel hiển thị mà đối tượng hoặc primitive vẽ ra. Hàm này chỉ có trong shader ``spatial`` và ``canvas_item``.

Cách sử dụng tiêu chuẩn của hàm fragment là thiết lập các thuộc tính vật liệu dùng để tính toán ánh sáng. Ví dụ, bạn sẽ thiết lập các giá trị cho ``ROUGHNESS``, ``RIM`` hoặc ``TRANSMISSION``, để cho hàm light biết các ánh sáng phản hồi với fragment đó như thế nào. Điều này cho phép kiểm soát một shading pipeline phức tạp mà không yêu cầu người dùng phải viết nhiều mã. Nếu không cần chức năng tích hợp này, bạn có thể bỏ qua và viết hàm xử lý ánh sáng của riêng mình; Godot sẽ tối ưu hóa để loại bỏ nó. Ví dụ, nếu bạn không ghi giá trị vào ``RIM``, Godot sẽ không tính toán ánh sáng viền. Trong quá trình biên dịch, Godot kiểm tra xem ``RIM`` có được sử dụng hay không; nếu không, nó sẽ loại bỏ toàn bộ mã tương ứng. Do đó, bạn sẽ không lãng phí phép tính cho những hiệu ứng không sử dụng.

Bộ xử lý ánh sáng
~~~~~~~~~~~~~~~~~

Bộ xử lý ``light()`` cũng chạy cho từng pixel và chạy một lần cho mỗi ánh sáng ảnh hưởng đến đối tượng. Nó không chạy nếu không có ánh sáng nào ảnh hưởng đến đối tượng. Bộ xử lý này tồn tại dưới dạng một hàm được gọi bên trong bộ xử lý ``fragment()`` và thường hoạt động trên các thuộc tính vật liệu được thiết lập bên trong hàm ``fragment()``.

Bộ xử lý ``light()`` hoạt động khác nhau trong 2D và 3D; để xem mô tả về cách hoạt động trong từng trường hợp, hãy xem tài liệu tương ứng: :ref:`CanvasItem shaders <doc_canvas_item_shader>` và :ref:`Spatial shaders <doc_spatial_shader>`.
