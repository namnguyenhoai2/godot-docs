.. _doc_introduction_to_shaders:

Giới thiệu về shader
====================

Trang này giải thích shader là gì và cung cấp cho bạn cái nhìn tổng quan về cách chúng hoạt động trong Godot. Để xem tài liệu tham khảo chi tiết về ngôn ngữ shading của engine, hãy xem
:ref:`doc_shading_language`.

Shader là một loại chương trình đặc biệt chạy trên các Bộ xử lý Đồ họa (GPU). Ban đầu, chúng được sử dụng để tạo bóng cho các cảnh 3D, nhưng ngày nay chúng có thể làm được nhiều hơn thế. Bạn có thể sử dụng chúng để kiểm soát cách engine vẽ hình học và pixel lên màn hình, cho phép bạn tạo ra đủ loại hiệu ứng.

Các engine rendering hiện đại như Godot vẽ mọi thứ bằng shader: card đồ họa có thể chạy hàng nghìn chỉ thị song song, mang lại tốc độ rendering đáng kinh ngạc.

Tuy nhiên, do có tính chất song song, shader không xử lý thông tin theo cách mà một chương trình thông thường vẫn làm. Mã shader chạy trên từng vertex hoặc pixel một cách độc lập. Bạn cũng không thể lưu trữ dữ liệu giữa các frame. Vì vậy, khi làm việc với shader, bạn cần lập trình và tư duy khác với các ngôn ngữ lập trình khác.

Giả sử bạn muốn cập nhật tất cả pixel trong một texture thành một màu nhất định. Trong GDScript, mã của bạn sẽ sử dụng các vòng lặp ``for``:

::

    for x in range(width):
        for y in range(height):
            set_color(x, y, some_color)

Mã của bạn đã là một phần của vòng lặp trong shader, vì vậy mã tương ứng sẽ trông như sau.

.. code-block:: glsl

    shader_type canvas_item;

    void fragment() {
        COLOR = some_color;
    }

.. note::

   Card đồ họa gọi hàm ``fragment()`` một hoặc nhiều lần cho mỗi pixel mà nó phải vẽ. Nội dung này sẽ được giải thích thêm bên dưới.

Shader trong Godot
------------------

Godot cung cấp một ngôn ngữ shading dựa trên OpenGL Shading Language (GLSL) phổ biến nhưng đã được đơn giản hóa. Engine xử lý một phần công việc khởi tạo ở cấp thấp cho bạn, giúp việc viết các shader phức tạp trở nên dễ dàng hơn.

Trong Godot, shader được tạo thành từ các hàm chính gọi là "hàm xử lý" (processor function). Hàm xử lý là điểm bắt đầu để shader của bạn tham gia vào chương trình. Có bảy hàm xử lý khác nhau.

1. Hàm ``vertex()`` chạy trên tất cả vertex trong mesh và thiết lập vị trí của chúng cùng một số biến khác trên mỗi vertex. Được sử dụng trong
   :ref:`canvas_item shaders <doc_canvas_item_shader>` and
   :ref:`spatial shaders <doc_spatial_shader>`.

2. Hàm ``fragment()`` chạy trên mọi pixel được mesh bao phủ. Hàm này sử dụng các giá trị do hàm ``vertex()`` xuất ra và được nội suy giữa các vertex. Được sử dụng trong :ref:`canvas_item shaders <doc_canvas_item_shader>` và
   :ref:`spatial shaders <doc_spatial_shader>`.

3. Hàm ``light()`` chạy trên mọi pixel và với mọi light. Hàm này lấy các biến từ hàm ``fragment()`` và từ những lần chạy trước đó của chính nó. Được sử dụng trong :ref:`canvas_item shaders <doc_canvas_item_shader>` và
   :ref:`spatial shaders <doc_spatial_shader>`.

4. Hàm ``start()`` chạy một lần cho mỗi particle trong một particle system khi particle đó vừa được tạo. Được sử dụng trong
   :ref:`particles shaders <doc_particle_shader>`.

5. Hàm ``process()`` chạy trên mọi particle trong một particle system ở mỗi frame. Được sử dụng trong :ref:`particles shaders <doc_particle_shader>`.

6. Hàm ``sky()`` chạy trên mọi pixel trong radiance cubemap khi radiance cubemap cần được cập nhật, và trên mọi pixel của màn hình hiện tại. Được sử dụng trong :ref:`sky shaders <doc_sky_shader>`.

7. Hàm ``fog()`` chạy trên mọi froxel trong volumetric fog froxel buffer giao với :ref:`FogVolume <class_FogVolume>`. Được sử dụng bởi
   :ref:`fog shaders <doc_fog_shader>`.

.. warning::

    Hàm ``light()`` sẽ không chạy nếu render mode ``vertex_lighting`` được bật, hoặc nếu **Rendering > Quality > Shading > Force Vertex Shading** được bật trong Project Settings. Hàm này được bật theo mặc định trên các nền tảng mobile.

.. note::

   Godot cũng cung cấp một API để người dùng viết các shader GLSL hoàn toàn tùy chỉnh. Để biết thêm thông tin, hãy xem :ref:`doc_compute_shaders`.

Các loại shader
---------------

Thay vì cung cấp một cấu hình đa dụng cho mọi mục đích sử dụng (2D, 3D, particle, sky, fog), bạn phải chỉ định loại shader mà mình đang viết. Các loại khác nhau hỗ trợ các render mode, biến dựng sẵn và hàm xử lý khác nhau.

Trong Godot, tất cả shader cần chỉ định loại của chúng ở dòng đầu tiên, như sau:

.. code-block:: glsl

    shader_type spatial;

Sau đây là các loại hiện có:

* :ref:`spatial <doc_spatial_shader>` cho rendering 3D. * :ref:`canvas_item <doc_canvas_item_shader>` cho rendering 2D. * :ref:`particles <doc_particle_shader>` cho particle system. * :ref:`sky <doc_sky_shader>` để render :ref:`Skies <class_Sky>`. * :ref:`fog <doc_fog_shader>` để render :ref:`FogVolumes <class_FogVolume>`. * :ref:`texture_blit <doc_texture_blit_shader>` để render :ref:`DrawableTexture2Ds <class_DrawableTexture2D>`.

Render mode
-----------

Shader có các render mode tùy chọn mà bạn có thể chỉ định ở dòng thứ hai, sau loại shader, như sau:

.. code-block:: glsl

    shader_type spatial;
    render_mode unshaded, cull_disabled;

Render mode thay đổi cách Godot áp dụng shader. Ví dụ, mode ``unshaded`` khiến engine bỏ qua hàm xử lý light dựng sẵn.

Mỗi loại shader có các render mode khác nhau. Hãy xem tài liệu tham khảo của từng loại shader để biết danh sách đầy đủ các render mode.

Bộ xử lý vertex
~~~~~~~~~~~~~~~

Hàm xử lý ``vertex()`` được gọi một lần cho mỗi vertex trong shader ``spatial`` và ``canvas_item``.

Mỗi vertex trong hình học của thế giới có các thuộc tính như vị trí và màu sắc. Hàm này sửa đổi những giá trị đó và truyền chúng cho hàm fragment. Bạn cũng có thể sử dụng nó để gửi thêm dữ liệu cho hàm fragment bằng varyings.

Theo mặc định, Godot chuyển đổi thông tin vertex cho bạn, điều này cần thiết để chiếu hình học lên màn hình. Bạn có thể sử dụng render mode để tự chuyển đổi dữ liệu; xem :ref:`Spatial shader doc <doc_spatial_shader>` để biết ví dụ.

Bộ xử lý fragment
~~~~~~~~~~~~~~~~~

Hàm xử lý ``fragment()`` được sử dụng để thiết lập các tham số material của Godot cho từng pixel. Mã này chạy trên mọi pixel hiển thị mà object hoặc primitive vẽ ra. Hàm này chỉ khả dụng trong shader ``spatial`` và ``canvas_item``.

Cách sử dụng phổ biến của hàm fragment là thiết lập các thuộc tính material được dùng để tính toán lighting. Ví dụ, bạn sẽ thiết lập các giá trị cho ``ROUGHNESS``, ``RIM`` hoặc ``TRANSMISSION``, để cho hàm light biết các light phản hồi với fragment đó như thế nào. Điều này giúp bạn kiểm soát một pipeline shading phức tạp mà không cần phải viết nhiều mã. Nếu không cần chức năng dựng sẵn này, bạn có thể bỏ qua nó và viết hàm xử lý light của riêng mình, Godot sẽ loại bỏ phần không cần thiết này khi tối ưu. Ví dụ, nếu bạn không ghi giá trị vào ``RIM``, Godot sẽ không tính toán rim lighting. Trong quá trình biên dịch, Godot kiểm tra xem ``RIM`` có được sử dụng hay không; nếu không, engine sẽ loại bỏ toàn bộ mã tương ứng. Do đó, bạn sẽ không lãng phí phép tính cho những hiệu ứng mà mình không sử dụng.

Bộ xử lý light
~~~~~~~~~~~~~~

Bộ xử lý ``light()`` cũng chạy trên từng pixel và chạy một lần cho mỗi light ảnh hưởng đến object. Hàm này không chạy nếu không có light nào ảnh hưởng đến object. Nó tồn tại dưới dạng một hàm được gọi bên trong bộ xử lý ``fragment()`` và thường hoạt động trên các thuộc tính material được thiết lập bên trong hàm ``fragment()``.

Bộ xử lý ``light()`` hoạt động khác nhau trong 2D và 3D; để biết mô tả về cách nó hoạt động trong từng trường hợp, hãy xem tài liệu tương ứng, lần lượt là :ref:`CanvasItem shaders <doc_canvas_item_shader>` và :ref:`Spatial shaders <doc_spatial_shader>`.
