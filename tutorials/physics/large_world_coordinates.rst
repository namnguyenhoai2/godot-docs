.. _doc_large_world_coordinates:

Tọa độ thế giới lớn
===================

.. note::

    Tọa độ thế giới lớn chủ yếu hữu ích trong các dự án 3D; chúng hiếm khi cần thiết trong các dự án 2D. Ngoài ra, không giống như rendering 3D, rendering 2D hiện không được hưởng lợi từ độ chính xác tăng lên khi bật tọa độ thế giới lớn.

Tại sao sử dụng tọa độ thế giới lớn?
------------------------------------

Trong Godot, cả mô phỏng vật lý và rendering đều dựa vào các số *floating-point*. Tuy nhiên, trong điện toán, các số floating-point có **độ chính xác và phạm vi giới hạn**. Đây có thể là vấn đề đối với các trò chơi có thế giới khổng lồ, chẳng hạn như trò chơi mô phỏng không gian hoặc quy mô hành tinh.

Độ chính xác cao nhất khi giá trị gần ``0.0``. Độ chính xác giảm dần khi giá trị tăng hoặc giảm ra xa ``0.0``. Điều này xảy ra mỗi khi *exponent* của số floating-point tăng, tức là khi số floating-point vượt qua một giá trị lũy thừa của 2 (2, 4, 8, 16, …). Mỗi khi điều này xảy ra, bước tối thiểu của số sẽ *tăng lên*, dẫn đến mất độ chính xác.

Trên thực tế, điều này có nghĩa là khi người chơi di chuyển ra xa gốc thế giới (``Vector2(0, 0)`` trong trò chơi 2D hoặc ``Vector3(0, 0, 0)`` trong trò chơi 3D), độ chính xác sẽ giảm.

Mất độ chính xác có thể khiến các vật thể trông như đang "rung" khi ở xa gốc thế giới, vì vị trí của model sẽ nhảy đến giá trị gần nhất có thể được biểu diễn bằng một số floating-point. Điều này cũng có thể gây ra các lỗi vật lý chỉ xảy ra khi người chơi ở xa gốc thế giới.

Phạm vi xác định các giá trị nhỏ nhất và lớn nhất có thể được lưu trữ trong số đó. Nếu người chơi cố di chuyển vượt quá phạm vi này, họ sẽ đơn giản là không thể làm vậy. Tuy nhiên, trên thực tế, độ chính xác của floating-point hầu như luôn trở thành vấn đề trước khi phạm vi trở thành vấn đề.

Phạm vi và độ chính xác (bước tối thiểu giữa hai khoảng exponent) được xác định bởi kiểu số floating-point. Phạm vi *lý thuyết* cho phép lưu trữ các giá trị cực kỳ lớn trong float độ chính xác đơn, nhưng với độ chính xác rất thấp. Trên thực tế, một kiểu floating-point không thể biểu diễn tất cả các giá trị nguyên không thực sự hữu ích. Ở các giá trị cực lớn, độ chính xác giảm đến mức số đó thậm chí không thể phân biệt hai giá trị *nguyên* riêng biệt với nhau.

Đây là phạm vi mà các giá trị nguyên riêng lẻ có thể được biểu diễn trong một số floating-point:

- **Phạm vi float độ chính xác đơn (biểu diễn tất cả số nguyên):** Từ -16,777,216 đến 16,777,216
- **Phạm vi float độ chính xác kép (biểu diễn tất cả số nguyên):** Từ -9 quadrillion đến 9 quadrillion

+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| Phạm vi          | Bước đơn   | Bước kép              | Chú thích                                                                                                                                      |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [1; 2]           | ~0.0000001 | ~1e-15                | Độ chính xác cao hơn khi gần 0.0 (bảng này đã được rút gọn).                                                                                   |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [2; 4]           | ~0.0000002 | ~1e-15                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [4; 8]           | ~0.0000005 | ~1e-15                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [8; 16]          | ~0.000001  | ~1e-14                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [16; 32]         | ~0.000002  | ~1e-14                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [32; 64]         | ~0.000004  | ~1e-14                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [64; 128]        | ~0.000008  | ~1e-13                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [128; 256]       | ~0.000015  | ~1e-13                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [256; 512]       | ~0.00003   | ~1e-13                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [512; 1024]      | ~0.00006   | ~1e-12                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [1024; 2048]     | ~0.0001    | ~1e-12                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [2048; 4096]     | ~0.0002    | ~1e-12                | Phạm vi độ chính xác đơn *được khuyến nghị* tối đa cho trò chơi 3D góc nhìn thứ nhất mà không có lỗi hiển thị hoặc lỗi vật lý.                 |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [4096; 8192]     | ~0.0005    | ~1e-12                | Phạm vi độ chính xác đơn *được khuyến nghị* tối đa cho trò chơi 3D góc nhìn thứ ba mà không có lỗi hiển thị hoặc lỗi vật lý.                   |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [8192; 16384]    | ~0.001     | ~1e-12                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [16384; 32768]   | ~0.0019    | ~1e-11                | Phạm vi độ chính xác đơn *được khuyến nghị* tối đa cho trò chơi 3D góc nhìn từ trên xuống mà không có lỗi hiển thị hoặc lỗi vật lý.            |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [32768; 65536]   | ~0.0039    | ~1e-11                | Phạm vi độ chính xác đơn *được khuyến nghị* tối đa cho bất kỳ trò chơi 3D nào. Sau mốc này, thường cần độ chính xác kép (tọa độ thế giới lớn). |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [65536; 131072]  | ~0.0078    | ~1e-11                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| [131072; 262144] | ~0.0156    | ~1e-10                |                                                                                                                                                |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
| > 262144         | > ~0.0313  | ~1e-10 (0.0000000001) | Sau giá trị này, độ chính xác kép vẫn chính xác hơn nhiều so với độ chính xác đơn.                                                             |
+------------------+------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

Khi sử dụng float độ chính xác đơn, bạn vẫn có thể vượt qua các phạm vi được đề xuất, nhưng các hiện tượng lỗi hiển thị sẽ dễ nhận thấy hơn và lỗi vật lý sẽ xảy ra thường xuyên hơn (chẳng hạn như người chơi không đi thẳng theo một số hướng nhất định).

.. seealso::

    Xem bài viết `Demystifying Floating Point Precision <https://blog.demofox.org/2017/11/21/>`__ để biết thêm thông tin.

Cách hoạt động của tọa độ thế giới lớn
--------------------------------------

Tọa độ thế giới lớn (còn được gọi là **vật lý độ chính xác kép**) làm tăng mức độ chính xác của tất cả các phép tính dấu phẩy động trong engine.

Theo mặc định, :ref:`class_float` là 64-bit trong GDScript, nhưng :ref:`class_Vector2`,
:ref:`class_Vector3` và :ref:`class_Vector4` là 32-bit. Điều này có nghĩa là độ chính xác của các kiểu vector bị giới hạn hơn nhiều. Để khắc phục, chúng ta có thể tăng số bit được dùng để biểu diễn một số dấu phẩy động trong kiểu Vector. Kết quả là độ chính xác tăng theo *hàm mũ*, nghĩa là giá trị cuối không chỉ chính xác gấp đôi mà ở các giá trị lớn còn có thể chính xác hơn hàng nghìn lần. Giá trị tối đa có thể biểu diễn cũng tăng đáng kể khi chuyển từ float độ chính xác đơn sang float độ chính xác kép.

Để tránh các vấn đề mô hình bị giật khi ở xa gốc thế giới, engine kết xuất 3D của Godot sẽ tăng độ chính xác cho các thao tác kết xuất khi bật tọa độ thế giới lớn. Các shader không sử dụng float độ chính xác kép vì lý do hiệu năng, nhưng một `giải pháp thay thế <https://github.com/godotengine/godot/pull/66178>`__ được dùng để mô phỏng độ chính xác kép cho việc kết xuất bằng các float độ chính xác đơn.

.. note::

    Việc bật tọa độ thế giới lớn phải trả giá bằng hiệu năng và mức sử dụng bộ nhớ, đặc biệt trên CPU 32-bit. Chỉ bật tọa độ thế giới lớn khi bạn thực sự cần.

    Tính năng này hướng đến các nền tảng máy tính để bàn tầm trung/cao cấp. Tọa độ thế giới lớn có thể không hoạt động tốt trên các thiết bị di động cấp thấp, trừ khi bạn thực hiện các bước khác để giảm mức sử dụng CPU (chẳng hạn như giảm số tick vật lý mỗi giây).

    Trên các nền tảng cấp thấp, thay vào đó có thể sử dụng phương pháp *dịch chuyển gốc* để hỗ trợ các thế giới lớn mà không cần dùng vật lý và kết xuất độ chính xác kép. Dịch chuyển gốc hoạt động với các float độ chính xác đơn, nhưng làm tăng độ phức tạp của logic trò chơi, đặc biệt trong các trò chơi nhiều người chơi. Vì vậy, phương pháp dịch chuyển gốc không được trình bày chi tiết trên trang này.

Tọa độ thế giới lớn dành cho ai?
--------------------------------

Tọa độ thế giới lớn thường cần thiết cho không gian 3D hoặc các trò chơi mô phỏng quy mô hành tinh. Điều này cũng áp dụng cho các trò chơi yêu cầu hỗ trợ tốc độ di chuyển *rất* nhanh, nhưng đôi khi cũng có các chuyển động *và* rất chậm, chính xác.

Mặt khác, điều quan trọng là chỉ sử dụng tọa độ thế giới lớn khi thực sự cần (vì lý do hiệu năng). Tọa độ thế giới lớn thường **không** cần thiết cho:

- Các trò chơi 2D, vì các vấn đề về độ chính xác thường ít nhận thấy hơn.
- Các trò chơi có thế giới quy mô nhỏ hoặc trung bình.
- Các trò chơi có thế giới lớn nhưng được chia thành nhiều level khác nhau, giữa các level có các chuỗi tải. Bạn có thể đặt phần của mỗi level quanh gốc thế giới để tránh các vấn đề về độ chính xác mà không làm giảm hiệu năng.
- Các trò chơi thế giới mở có *khu vực có thể đi bộ* không vượt quá 8192×8192 mét (được căn giữa quanh gốc thế giới). Như bảng trên cho thấy, mức độ chính xác vẫn chấp nhận được trong phạm vi đó, ngay cả đối với trò chơi góc nhìn thứ nhất.

**Nếu không chắc chắn**, có lẽ bạn không cần sử dụng tọa độ thế giới lớn trong dự án của mình. Để tham khảo, hầu hết các tựa game thế giới mở AAA hiện đại không sử dụng hệ thống tọa độ thế giới lớn mà vẫn dựa vào các float độ chính xác đơn cho cả kết xuất và vật lý.

Bật tọa độ thế giới lớn
-----------------------

Quy trình này yêu cầu biên dịch lại editor và tất cả binary export template mà bạn định sử dụng. Nếu bạn chỉ định export dự án ở chế độ release, bạn có thể bỏ qua việc biên dịch các debug export template. Trong mọi trường hợp, bạn sẽ cần biên dịch một bản editor để có thể kiểm thử thế giới độ chính xác cao mà không phải export dự án mỗi lần.

Xem phần :ref:`Biên dịch <toc-devel-compiling>` để biết hướng dẫn biên dịch cho từng nền tảng đích. Bạn sẽ cần thêm tùy chọn SCons ``precision=double`` khi biên dịch editor và export template.

Các binary tạo ra sẽ được đặt tên với hậu tố ``.double`` để phân biệt với các binary độ chính xác đơn (không có hậu tố độ chính xác nào). Sau đó, bạn có thể chỉ định các binary này làm custom export template trong export preset của dự án, trong hộp thoại Export.

Tính tương thích giữa các bản build độ chính xác đơn và độ chính xác kép
------------------------------------------------------------------------

Khi lưu tài nguyên *nhị phân* bằng singleton :ref:`class_ResourceSaver`, một cờ đặc biệt sẽ được lưu trong tệp nếu tài nguyên được lưu bằng bản build sử dụng các số độ chính xác kép. Do đó, tất cả tài nguyên nhị phân sẽ thay đổi trên đĩa khi bạn chuyển sang bản build độ chính xác kép và ghi đè lên chúng.

Cả bản build độ chính xác đơn và độ chính xác kép đều hỗ trợ sử dụng
singleton :ref:`class_ResourceLoader` trên các tài nguyên sử dụng cờ đặc biệt này. Điều đó có nghĩa là bản build độ chính xác đơn có thể tải các tài nguyên được lưu bằng bản build độ chính xác kép và ngược lại. Tài nguyên dạng văn bản không lưu cờ độ chính xác kép, vì chúng không cần cờ này để được đọc chính xác.

Các vấn đề không tương thích đã biết
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Trong trò chơi nhiều người chơi qua mạng, server và tất cả client nên sử dụng cùng một loại bản build để đảm bảo độ chính xác nhất quán giữa các client. Việc sử dụng các loại bản build khác nhau *có thể* hoạt động, nhưng nhiều vấn đề khác nhau có thể xảy ra.
- API GDExtension thay đổi theo cách không tương thích trong các bản build độ chính xác kép. Điều này có nghĩa là các extension **bắt buộc** phải được biên dịch lại để hoạt động với các bản build độ chính xác kép. Ở phía nhà phát triển extension, define ``REAL_T_IS_DOUBLE`` được bật khi biên dịch GDExtension với ``precision=double``. ``real_t`` có thể được dùng làm alias cho ``float`` trong các bản build độ chính xác đơn và ``double`` trong các bản build độ chính xác kép.

Giới hạn
--------

Vì các shader kết xuất 3D thực sự không sử dụng float độ chính xác kép, nên có một số giới hạn liên quan đến độ chính xác khi kết xuất 3D:

- :ref:`Ánh xạ Triplanar <doc_standard_material_3d_triplanar_mapping>` không được hưởng lợi từ độ chính xác tăng thêm. Các material sử dụng ánh xạ triplanar sẽ có hiện tượng giật rõ rệt khi ở xa gốc thế giới.
- Các node :ref:`class_GPUParticles3D` có **Local Coords** bị tắt sẽ không được hưởng lợi từ độ chính xác tăng thêm. Điều này có thể khiến hạt bị giật rõ rệt khi ở xa gốc thế giới. Các node có **Local Coords** được bật, cũng như các node :ref:`class_CPUParticles3D`, vẫn được hưởng lợi từ độ chính xác tăng thêm.
- Các shader sử dụng chế độ kết xuất ``skip_vertex_transform`` hoặc ``world_vertex_coords`` không được hưởng lợi từ độ chính xác tăng thêm.
- Trong các bản build độ chính xác kép, tọa độ không gian thế giới trong hàm shader ``fragment()`` không thể được tái dựng từ không gian quan sát, ví dụ:

  .. code-block:: glsl

    vec3 world = (INV_VIEW_MATRIX * vec4(VERTEX, 1.0)).xyz;

  Thay vào đó, hãy tính toán tọa độ trong không gian thế giới trong hàm ``vertex()`` và truyền chúng bằng một :ref:`varying <doc_shading_language_varyings>`, ví dụ:

  .. code-block:: glsl

    varying vec3 world;
    void vertex() {
        world = (MODEL_MATRIX * vec4(VERTEX, 1.0)).xyz;
    }

Hiện tại, kết xuất 2D không được hưởng lợi từ độ chính xác cao hơn khi bật tọa độ thế giới lớn. Điều này có thể khiến mô hình bị giật thấy rõ khi ở xa gốc tọa độ thế giới (bắt đầu từ vài triệu pixel ở các mức thu phóng thông thường). Tuy nhiên, các phép tính vật lý 2D vẫn sẽ được hưởng lợi từ độ chính xác cao hơn.
