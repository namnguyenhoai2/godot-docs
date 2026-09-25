.. _doc_sky_shader:

Shader bầu trời
===============

Shader bầu trời là một loại shader đặc biệt được dùng để vẽ nền bầu trời và cập nhật các cubemap bức xạ, vốn được dùng cho ánh sáng dựa trên hình ảnh (IBL). Shader bầu trời chỉ có một hàm xử lý là hàm ``sky()``.

Shader bầu trời được sử dụng ở ba nơi.

* Thứ nhất, shader bầu trời được dùng để vẽ bầu trời khi bạn chọn sử dụng Sky làm nền trong cảnh.
* Thứ hai, shader bầu trời được dùng để cập nhật cubemap bức xạ khi sử dụng Sky cho màu môi trường hoặc phản xạ.
* Thứ ba, shader bầu trời được dùng để vẽ các subpass có độ phân giải thấp hơn, có thể được sử dụng trong pass nền hoặc cubemap có độ phân giải cao.

Tổng cộng, điều này có nghĩa là shader bầu trời có thể chạy tối đa sáu lần trong mỗi khung hình. Tuy nhiên, trên thực tế, số lần chạy sẽ ít hơn nhiều vì cubemap bức xạ không cần được cập nhật trong mọi khung hình và không phải tất cả subpass đều được sử dụng. Bạn có thể thay đổi hành vi của shader dựa trên nơi nó được gọi bằng cách kiểm tra các giá trị boolean ``AT_*_PASS``. Ví dụ:

.. code-block:: glsl

    shader_type sky;

    void sky() {
        if (AT_CUBEMAP_PASS) {
            // Đặt cubemap bức xạ thành một sắc xanh lam đẹp thay vì thực hiện
            // các phép tính bầu trời tốn kém
            COLOR = vec3(0.2, 0.6, 1.0);
        } else {
            // Chỉ thực hiện các phép tính bầu trời tốn kém cho bầu trời nền
            COLOR = get_sky_color(EYEDIR);
        }
    }


Khi sử dụng shader bầu trời để vẽ nền, shader sẽ được gọi cho tất cả fragment không bị che khuất trên màn hình. Tuy nhiên, đối với các subpass của nền, shader sẽ được gọi cho mọi pixel của subpass.

Khi sử dụng shader bầu trời để cập nhật cubemap bức xạ, shader bầu trời sẽ được gọi cho mọi pixel trong cubemap. Mặt khác, shader chỉ được gọi khi cubemap bức xạ cần được cập nhật. Cubemap bức xạ cần được cập nhật khi bất kỳ tham số shader nào được cập nhật. Ví dụ, nếu ``TIME`` được sử dụng trong shader, cubemap bức xạ sẽ được cập nhật trong mỗi khung hình. Những thay đổi sau đây sẽ buộc cubemap bức xạ được cập nhật:

* ``TIME`` được sử dụng.
* ``POSITION`` được sử dụng và vị trí camera thay đổi.
* Nếu bất kỳ thuộc tính ``LIGHTX_*`` nào được sử dụng và bất kỳ
  :ref:`DirectionalLight3D <class_DirectionalLight3D>` nào thay đổi.
* Nếu bất kỳ uniform nào trong shader thay đổi.
* Nếu màn hình được thay đổi kích thước và một trong hai subpass được sử dụng.

Hãy tránh cập nhật cubemap bức xạ một cách không cần thiết. Nếu bạn cần cập nhật cubemap bức xạ trong mỗi khung hình, hãy đảm bảo rằng
:ref:`Chế độ xử lý Sky <class_Sky_property_process_mode>` được đặt thành
:ref:`PROCESS_MODE_REALTIME <class_Sky_constant_PROCESS_MODE_REALTIME>`.

Lưu ý rằng :ref:`chế độ xử lý <class_Sky_property_process_mode>` chỉ ảnh hưởng đến việc kết xuất cubemap bức xạ. Bầu trời hiển thị luôn được kết xuất bằng cách gọi fragment shader cho mọi pixel. Với các fragment shader phức tạp, điều này có thể tạo ra chi phí kết xuất cao. Nếu bầu trời tĩnh (các điều kiện được liệt kê ở trên được đáp ứng) hoặc thay đổi chậm, không cần chạy toàn bộ fragment shader trong mỗi khung hình. Có thể tránh việc này bằng cách kết xuất toàn bộ bầu trời vào cubemap bức xạ và đọc từ cubemap này khi kết xuất bầu trời hiển thị. Với bầu trời hoàn toàn tĩnh, điều đó có nghĩa là bầu trời chỉ cần được kết xuất một lần.

Đoạn mã sau kết xuất toàn bộ bầu trời vào cubemap bức xạ và đọc từ cubemap đó để hiển thị bầu trời nhìn thấy:

.. code-block:: glsl

    shader_type sky;

    void sky() {
        if (AT_CUBEMAP_PASS) {
            vec3 dir = EYEDIR;

            vec4 col = vec4(0.0);

            // Tính toán màu phức tạp

            COLOR = col.xyz;
            ALPHA = 1.0;
        } else {
            COLOR = texture(RADIANCE, EYEDIR).rgb;
        }
    }

Bằng cách này, các phép tính phức tạp chỉ diễn ra trong pass cubemap. Bạn có thể tối ưu pass này bằng cách đặt :ref:`chế độ xử lý <class_Sky_property_process_mode>` của Sky và :ref:`kích thước bức xạ <class_Sky_property_radiance_size>` để đạt được sự cân bằng mong muốn giữa hiệu năng và độ trung thực hình ảnh.

Chế độ kết xuất
---------------

Subpass cho phép bạn thực hiện các phép tính tốn kém hơn ở độ phân giải thấp hơn để tăng tốc shader. Ví dụ, đoạn mã sau kết xuất các đám mây ở độ phân giải thấp hơn phần còn lại của bầu trời:

.. code-block:: glsl

    shader_type sky;
    render_mode use_half_res_pass;

    void sky() {
        if (AT_HALF_RES_PASS) {
            // Chạy phép tính đám mây cho 1/4 số pixel
            vec4 color = generate_clouds(EYEDIR);
            COLOR = color.rgb;
            ALPHA = color.a;
        } else {
            // Trong pass có độ phân giải đầy đủ, trộn bầu trời và các đám mây với nhau
            vec3 color = generate_sky(EYEDIR);
            COLOR = color + HALF_RES_COLOR.rgb * HALF_RES_COLOR.a;
        }
    }

+--------------------------+----------------------------------------------------------------------------+
| Chế độ kết xuất          | Mô tả                                                                      |
+==========================+============================================================================+
| **use_half_res_pass**    | Cho phép shader ghi vào và truy cập pass có độ phân giải bằng một nửa.     |
+--------------------------+----------------------------------------------------------------------------+
| **use_quarter_res_pass** | Cho phép shader ghi vào và truy cập pass có độ phân giải bằng một phần tư. |
+--------------------------+----------------------------------------------------------------------------+
| **disable_fog**          | Nếu được sử dụng, sương mù sẽ không ảnh hưởng đến bầu trời.                |
+--------------------------+----------------------------------------------------------------------------+

Các giá trị dựng sẵn
--------------------

Các giá trị được đánh dấu là ``in`` chỉ có thể đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lý. Không thể ghi vào sampler nên chúng không được đánh dấu.

Các giá trị dựng sẵn toàn cục
-----------------------------

Các giá trị dựng sẵn toàn cục khả dụng ở mọi nơi, bao gồm cả trong các hàm tùy chỉnh.

Có 4 đèn ``LIGHTX``, được truy cập bằng ``LIGHT0``, ``LIGHT1``, ``LIGHT2`` và ``LIGHT3``.


+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Giá trị dựng sẵn                | Mô tả                                                                                                                                                                                                                                                                                          |
+=================================+================================================================================================================================================================================================================================================================================================+
| in float **TIME**               | Thời gian toàn cục tính từ khi engine khởi động, tính bằng giây. Giá trị này lặp lại sau mỗi ``3,600`` giây (có thể thay đổi bằng cài đặt                                                                                                                                                      |
|                                 | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`). Giá trị này chịu ảnh hưởng của :ref:`time_scale<class_Engine_property_time_scale>` nhưng không bị ảnh hưởng khi tạm dừng. Nếu bạn cần một biến ``TIME`` không bị ảnh hưởng bởi time scale, hãy thêm |
|                                 | :ref:`uniform shader toàn cục <doc_shading_language_global_uniforms>` của riêng bạn và cập nhật nó trong mỗi khung hình.                                                                                                                                                                       |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **POSITION**            | Vị trí camera trong không gian thế giới.                                                                                                                                                                                                                                                       |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| samplerCube **RADIANCE**        | Cubemap độ sáng. Chỉ có thể đọc trong background pass. Kiểm tra ``!AT_CUBEMAP_PASS`` trước khi sử dụng.                                                                                                                                                                                        |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_HALF_RES_PASS**    | ``true`` khi render đến half resolution pass.                                                                                                                                                                                                                                                  |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_QUARTER_RES_PASS** | ``true`` khi render đến quarter resolution pass.                                                                                                                                                                                                                                               |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_CUBEMAP_PASS**     | ``true`` khi render đến radiance cubemap.                                                                                                                                                                                                                                                      |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **LIGHTX_ENABLED**      | ``true`` nếu ``LIGHTX`` hiển thị và có trong scene. Nếu ``false``, các thuộc tính khác của light có thể chứa giá trị rác.                                                                                                                                                                      |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **LIGHTX_ENERGY**      | Hệ số nhân năng lượng cho ``LIGHTX``.                                                                                                                                                                                                                                                          |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **LIGHTX_DIRECTION**    | Hướng mà ``LIGHTX`` đang hướng tới.                                                                                                                                                                                                                                                            |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **LIGHTX_COLOR**        | Màu của ``LIGHTX``.                                                                                                                                                                                                                                                                            |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **LIGHTX_SIZE**        | Đường kính góc của ``LIGHTX`` trên bầu trời. Được biểu thị bằng radian. Để tham khảo, Mặt Trời nhìn từ Trái Đất có khoảng .0087 radian (0.5 độ).                                                                                                                                               |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **PI**                 | Một hằng số ``PI`` (``3.141592``). Tỷ số giữa chu vi và đường kính của đường tròn, đồng thời là số radian trong nửa vòng.                                                                                                                                                                      |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **TAU**                | Một hằng số ``TAU`` (``6.283185``). Tương đương với ``PI * 2`` và là số radian trong một vòng tròn đầy đủ.                                                                                                                                                                                     |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **E**                  | Một hằng số ``E`` (``2.718281``). Số Euler, cơ số của logarit tự nhiên.                                                                                                                                                                                                                        |
+---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Các biến dựng sẵn của bầu trời
------------------------------

+-------------------------------+--------------------------------------------------------------------------------------------------------+
| Built-in                      | Description                                                                                            |
+===============================+========================================================================================================+
| in vec3 **EYEDIR**            | Hướng đã chuẩn hóa của pixel hiện tại. Sử dụng hướng này làm hướng cơ bản cho các hiệu ứng procedural. |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| in vec2 **SCREEN_UV**         | Tọa độ UV trên màn hình của pixel hiện tại. Dùng để ánh xạ texture lên toàn màn hình.                  |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| in vec2 **SKY_COORDS**        | UV hình cầu. Dùng để ánh xạ texture panorama lên bầu trời.                                             |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| in vec4 **HALF_RES_COLOR**    | Giá trị màu của pixel tương ứng từ half resolution pass. Sử dụng bộ lọc tuyến tính.                    |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| in vec4 **QUARTER_RES_COLOR** | Giá trị màu của pixel tương ứng từ quarter resolution pass. Sử dụng bộ lọc tuyến tính.                 |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| out vec3 **COLOR**            | Màu đầu ra.                                                                                            |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| out float **ALPHA**           | Giá trị alpha đầu ra, chỉ có thể được sử dụng trong subpass.                                           |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
| out vec4 **FOG**              |                                                                                                        |
+-------------------------------+--------------------------------------------------------------------------------------------------------+
