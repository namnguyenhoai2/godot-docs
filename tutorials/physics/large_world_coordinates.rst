.. _doc_large_world_coordinates:

Tọa độ thế giới lớn
===================

.. note::

    Tọa độ thế giới lớn chủ yếu hữu ích trong các project 3D; chúng hiếm khi cần thiết trong các project 2D. Ngoài ra, không giống như rendering 3D, rendering 2D hiện tại không được hưởng lợi từ độ chính xác cao hơn khi bật tọa độ thế giới lớn.

Tại sao nên sử dụng tọa độ thế giới lớn?
----------------------------------------

Trong Godot, cả mô phỏng vật lý và rendering đều dựa vào các số *floating-point*. Tuy nhiên, trong điện toán, số floating-point có **độ chính xác và phạm vi giới hạn**. Đây có thể là vấn đề đối với các game có thế giới khổng lồ, chẳng hạn như game mô phỏng không gian hoặc quy mô hành tinh.

Độ chính xác lớn nhất khi giá trị gần với ``0.0``. Độ chính xác giảm dần khi giá trị tăng hoặc giảm ra xa ``0.0``. Điều này xảy ra mỗi khi *exponent* của số floating-point tăng, tức là khi số floating-point vượt qua một giá trị lũy thừa của 2 (2, 4, 8, 16, …). Mỗi khi điều này xảy ra, bước tối thiểu của số sẽ *tăng*, dẫn đến mất độ chính xác.

Trong thực tế, điều này có nghĩa là khi người chơi di chuyển ra xa gốc thế giới (``Vector2(0, 0)`` trong game 2D hoặc ``Vector3(0, 0, 0)`` trong game 3D), độ chính xác sẽ giảm.

Mất độ chính xác này có thể khiến các object trông như đang "rung" khi ở xa gốc thế giới, vì vị trí của model sẽ được snap về giá trị gần nhất có thể được biểu diễn bằng số floating-point. Điều này cũng có thể gây ra các lỗi vật lý chỉ xảy ra khi người chơi ở xa gốc thế giới.

Phạm vi xác định các giá trị tối thiểu và tối đa có thể được lưu trong số đó. Nếu người chơi cố di chuyển vượt quá phạm vi này, họ sẽ đơn giản là không thể di chuyển tiếp. Tuy nhiên, trong thực tế, độ chính xác của floating-point gần như luôn trở thành vấn đề trước khi phạm vi trở thành vấn đề.

Phạm vi và độ chính xác (bước tối thiểu giữa hai khoảng exponent) được xác định bởi kiểu số floating-point. Phạm vi *lý thuyết* cho phép lưu các giá trị cực kỳ lớn trong float độ chính xác đơn, nhưng với độ chính xác rất thấp. Trong thực tế, kiểu floating-point không thể biểu diễn tất cả các giá trị integer không hữu ích lắm. Ở các giá trị cực lớn, độ chính xác trở nên thấp đến mức số đó thậm chí không thể phân biệt hai giá trị *integer* riêng biệt với nhau.

Đây là phạm vi mà các giá trị integer riêng lẻ có thể được biểu diễn trong một số floating-point:

- **Phạm vi float độ chính xác đơn (biểu diễn tất cả số nguyên):** Từ -16,777,216 đến 16,777,216 - **Phạm vi float độ chính xác kép (biểu diễn tất cả số nguyên):** Từ -9 quadrillion đến 9 quadrillion

+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| Range                | Single step           | Double step           | Comment                                                                     |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [1; 2]               | ~0.0000001            | ~1e-15                | Precision becomes greater near 0.0 (this table is abbreviated).             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [2; 4]               | ~0.0000002            | ~1e-15                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [4; 8]               | ~0.0000005            | ~1e-15                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [8; 16]              | ~0.000001             | ~1e-14                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [16; 32]             | ~0.000002             | ~1e-14                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [32; 64]             | ~0.000004             | ~1e-14                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [64; 128]            | ~0.000008             | ~1e-13                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [128; 256]           | ~0.000015             | ~1e-13                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [256; 512]           | ~0.00003              | ~1e-13                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [512; 1024]          | ~0.00006              | ~1e-12                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [1024; 2048]         | ~0.0001               | ~1e-12                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [2048; 4096]         | ~0.0002               | ~1e-12                | Maximum *recommended* single-precision range for a first-person 3D game     |
|                      |                       |                       | without rendering artifacts or physics glitches.                            |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [4096; 8192]         | ~0.0005               | ~1e-12                | Maximum *recommended* single-precision range for a third-person 3D game     |
|                      |                       |                       | without rendering artifacts or physics glitches.                            |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [8192; 16384]        | ~0.001                | ~1e-12                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [16384; 32768]       | ~0.0019               | ~1e-11                | Maximum *recommended* single-precision range for a top-down 3D game         |
|                      |                       |                       | without rendering artifacts or physics glitches.                            |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [32768; 65536]       | ~0.0039               | ~1e-11                | Maximum *recommended* single-precision range for any 3D game. Double        |
|                      |                       |                       | precision (large world coordinates) is usually required past this point.    |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [65536; 131072]      | ~0.0078               | ~1e-11                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| [131072; 262144]     | ~0.0156               | ~1e-10                |                                                                             |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+
| > 262144             | > ~0.0313             | ~1e-10 (0.0000000001) | Double-precision remains far more precise than single-precision             |
|                      |                       |                       | past this value.                                                            |
+----------------------+-----------------------+-----------------------+-----------------------------------------------------------------------------+

Khi sử dụng float độ chính xác đơn, có thể vượt quá các phạm vi được đề xuất, nhưng artifact sẽ dễ nhận thấy hơn và các lỗi vật lý sẽ thường xuyên xảy ra hơn (chẳng hạn như người chơi không đi thẳng theo một số hướng nhất định).

.. seealso::

    Xem bài viết `Demystifying Floating Point Precision <https://blog.demofox.org/2017/11/21/>`__ để biết thêm thông tin.

Cách hoạt động của tọa độ thế giới lớn
--------------------------------------

Tọa độ thế giới lớn (còn được gọi là **vật lý độ chính xác kép**) làm tăng mức độ chính xác của tất cả các phép tính floating-point bên trong engine.

Theo mặc định, :ref:`class_float` là 64-bit trong GDScript, nhưng :ref:`class_Vector2`,
:ref:`class_Vector3` and :ref:`class_Vector4` are 32-bit. This means that the
độ chính xác của các kiểu vector bị giới hạn hơn nhiều. Để khắc phục điều này, chúng ta có thể tăng số bit được sử dụng để biểu diễn một số floating-point trong kiểu Vector. Điều này tạo ra mức tăng độ chính xác *theo cấp số nhân*, nghĩa là giá trị cuối cùng không chỉ chính xác gấp đôi, mà ở các giá trị lớn còn có thể chính xác hơn hàng nghìn lần. Giá trị tối đa có thể được biểu diễn cũng tăng đáng kể khi chuyển từ float độ chính xác đơn sang float độ chính xác kép.

Để tránh các vấn đề model bị snap khi ở xa gốc thế giới, engine rendering 3D của Godot sẽ tăng độ chính xác cho các thao tác rendering khi bật tọa độ thế giới lớn. Các shader không sử dụng float độ chính xác kép vì lý do hiệu năng, nhưng một `alternative solution <https://github.com/godotengine/godot/pull/66178>`__ được sử dụng để mô phỏng độ chính xác kép cho rendering bằng float độ chính xác đơn.

.. note::

    Việc bật tọa độ thế giới lớn đi kèm với cái giá về hiệu năng và mức sử dụng bộ nhớ, đặc biệt trên CPU 32-bit. Chỉ bật tọa độ thế giới lớn nếu bạn thực sự cần chúng.

    Tính năng này hướng đến các platform desktop tầm trung/cao cấp. Tọa độ thế giới lớn có thể hoạt động không tốt trên các thiết bị mobile cấp thấp, trừ khi bạn thực hiện các biện pháp khác để giảm mức sử dụng CPU (chẳng hạn như giảm số physics tick mỗi giây).

    Trên các platform cấp thấp, thay vào đó có thể sử dụng phương pháp *dịch chuyển gốc* để hỗ trợ các thế giới lớn mà không cần dùng vật lý và rendering độ chính xác kép. Dịch chuyển gốc hoạt động với float độ chính xác đơn, nhưng làm tăng độ phức tạp của logic game, đặc biệt trong các game multiplayer. Vì vậy, dịch chuyển gốc không được trình bày chi tiết trên trang này.

Tọa độ thế giới lớn dành cho ai?
--------------------------------

Tọa độ thế giới lớn thường cần thiết cho các game mô phỏng không gian hoặc quy mô hành tinh 3D. Điều này cũng áp dụng cho các game yêu cầu hỗ trợ tốc độ di chuyển *rất* nhanh, nhưng đôi khi cũng yêu cầu chuyển động rất chậm *và* chính xác.

Mặt khác, điều quan trọng là chỉ sử dụng tọa độ thế giới lớn khi thực sự cần thiết (vì lý do hiệu năng). Tọa độ thế giới lớn thường **không** cần thiết cho:

- Game 2D, vì các vấn đề về độ chính xác thường ít dễ nhận thấy hơn. - Game có thế giới quy mô nhỏ hoặc trung bình. - Game có thế giới lớn nhưng được chia thành các level khác nhau với các sequence loading ở giữa. Bạn có thể đặt phần của mỗi level quanh gốc thế giới để tránh các vấn đề về độ chính xác mà không phải chịu tổn thất hiệu năng. - Game open world có *khu vực có thể đi bộ* không vượt quá 8192×8192 mét (tập trung quanh gốc thế giới). Như được trình bày trong bảng trên, mức độ chính xác vẫn ở mức chấp nhận được trong phạm vi đó, ngay cả đối với game góc nhìn thứ nhất.

**Nếu không chắc**, có lẽ bạn không cần sử dụng tọa độ thế giới lớn trong project của mình. Để tham khảo, hầu hết các tựa game open world AAA hiện đại không sử dụng hệ thống tọa độ thế giới lớn mà vẫn dựa vào float độ chính xác đơn cho cả rendering và vật lý.

Bật tọa độ thế giới lớn
-----------------------

Quy trình này yêu cầu biên dịch lại editor và tất cả binary export template mà bạn dự định sử dụng. Nếu bạn chỉ dự định export project ở chế độ release, bạn có thể bỏ qua việc biên dịch debug export template. Trong mọi trường hợp, bạn sẽ cần biên dịch một editor build để có thể kiểm thử thế giới có độ chính xác lớn mà không phải export project mỗi lần.

Xem phần :ref:`Compiling <toc-devel-compiling>` để biết hướng dẫn biên dịch cho từng platform đích. Bạn sẽ cần thêm tùy chọn SCons ``precision=double`` khi biên dịch editor và export template.

Các binary tạo ra sẽ được đặt tên với hậu tố ``.double`` để phân biệt với các binary độ chính xác đơn (không có hậu tố độ chính xác). Sau đó, bạn có thể chỉ định các binary này làm export template tùy chỉnh trong export preset của project, trong hộp thoại Export.

Tính tương thích giữa các build độ chính xác đơn và độ chính xác kép
--------------------------------------------------------------------

Khi lưu một resource *binary* bằng singleton :ref:`class_ResourceSaver`, một cờ đặc biệt sẽ được lưu trong file nếu resource được lưu bằng một build sử dụng các số độ chính xác kép. Do đó, tất cả resource binary sẽ thay đổi trên disk khi bạn chuyển sang build độ chính xác kép và ghi đè lên chúng.

Cả build độ chính xác đơn và độ chính xác kép đều hỗ trợ sử dụng
:ref:`class_ResourceLoader` singleton on resources that use this special flag.
Điều này có nghĩa là build độ chính xác đơn có thể load các resource được lưu bằng build độ chính xác kép và ngược lại. Resource dạng text không lưu cờ độ chính xác kép, vì chúng không cần cờ này để được đọc chính xác.

Các điểm không tương thích đã biết
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Trong game multiplayer network, server và tất cả client nên sử dụng cùng một loại build để đảm bảo độ chính xác nhất quán giữa các client. Việc sử dụng các loại build khác nhau *có thể* hoạt động, nhưng nhiều vấn đề khác nhau có thể xảy ra. - GDExtension API thay đổi theo cách không tương thích trong các build độ chính xác kép. Điều này có nghĩa là các extension **phải** được build lại để hoạt động với các build độ chính xác kép. Ở phía developer của extension, define ``REAL_T_IS_DOUBLE`` được bật khi build một GDExtension với ``precision=double``. ``real_t`` có thể được sử dụng làm alias cho ``float`` trong các build độ chính xác đơn và ``double`` trong các build độ chính xác kép.

Các hạn chế
-----------

Vì shader rendering 3D thực tế không sử dụng float độ chính xác kép, nên có một số hạn chế liên quan đến độ chính xác của rendering 3D:

- :ref:`Triplanar mapping <doc_standard_material_3d_triplanar_mapping>` không được hưởng lợi từ độ chính xác tăng thêm. Các material sử dụng triplanar mapping sẽ xuất hiện hiện tượng jitter rõ rệt khi ở xa gốc thế giới. - Các node :ref:`class_GPUParticles3D` khi tắt **Local Coords** sẽ không được hưởng lợi từ độ chính xác tăng thêm. Điều này có thể khiến particle bị snap rõ rệt khi ở xa gốc thế giới. Các node bật **Local Coords**, cũng như các node :ref:`class_CPUParticles3D`, vẫn sẽ được hưởng lợi từ độ chính xác tăng thêm. - Các shader sử dụng render mode ``skip_vertex_transform`` hoặc ``world_vertex_coords`` không được hưởng lợi từ độ chính xác tăng thêm. - Trong các build độ chính xác kép, không thể tái dựng tọa độ world space trong shader ``fragment()`` từ view space, ví dụ:

  .. code-block:: glsl

    vec3 world = (INV_VIEW_MATRIX * vec4(VERTEX, 1.0)).xyz;

  Thay vào đó, hãy tính tọa độ world space trong hàm ``vertex()`` và truyền chúng bằng một :ref:`varying<doc_shading_language_varyings>`, ví dụ:

  .. code-block:: glsl

    varying vec3 world;
    void vertex() {
        world = (MODEL_MATRIX * vec4(VERTEX, 1.0)).xyz;
    }

Hiện tại, việc render 2D không được hưởng lợi từ độ chính xác tăng lên khi bật tọa độ thế giới lớn. Điều này có thể khiến hiện tượng mô hình bị giật thấy rõ xảy ra khi ở xa gốc tọa độ thế giới (bắt đầu từ vài triệu pixel ở các mức zoom thông thường). Tuy nhiên, các phép tính physics 2D vẫn sẽ được hưởng lợi từ độ chính xác tăng lên.
