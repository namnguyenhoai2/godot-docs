.. _doc_fog_shader:

Shader sương mù
===============

Shader sương mù được dùng để xác định cách sương mù được thêm vào (hoặc loại bỏ khỏi) một cảnh trong một khu vực nhất định. Shader sương mù luôn được sử dụng cùng với
:ref:`FogVolumes <class_FogVolume>` và sương mù thể tích. Shader sương mù chỉ có một hàm xử lý, hàm ``fog()``.

Độ phân giải của shader sương mù phụ thuộc vào độ phân giải của lưới froxel của sương mù thể tích. Do đó, mức độ chi tiết mà shader sương mù có thể thêm vào phụ thuộc vào khoảng cách từ :ref:`FogVolume <class_FogVolume>` đến camera.

Shader sương mù là một dạng đặc biệt của compute shader, được gọi một lần cho mỗi froxel bị chạm bởi hộp giới hạn căn chỉnh theo trục của
:ref:`FogVolume <class_FogVolume>`. Điều này có nghĩa là các froxel chỉ vừa chạm vào một :ref:`FogVolume <class_FogVolume>` nhất định vẫn sẽ được sử dụng.

Các biến dựng sẵn
-----------------

Các giá trị được đánh dấu là ``in`` chỉ được đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lệ. Không thể ghi vào sampler nên chúng không được đánh dấu.

Các biến dựng sẵn toàn cục
--------------------------

Các biến dựng sẵn toàn cục khả dụng ở mọi nơi, kể cả trong các hàm tùy chỉnh.

+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Biến dựng sẵn     | Mô tả                                                                                                                                                            |
+===================+==================================================================================================================================================================+
| in float **TIME** | Thời gian toàn cục tính từ khi engine khởi động, tính bằng giây. Giá trị này lặp lại sau mỗi ``3,600`` giây (có thể thay đổi bằng thiết lập                      |
|                   | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`). Giá trị này bị ảnh hưởng bởi                                          |
|                   | :ref:`time_scale<class_Engine_property_time_scale>` nhưng không bị ảnh hưởng khi tạm dừng. Nếu cần một biến ``TIME`` không bị ảnh hưởng bởi time scale, hãy thêm |
|                   | :ref:`global shader uniform <doc_shading_language_global_uniforms>` của riêng bạn và cập nhật biến đó trong mỗi frame.                                           |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **PI**   | Một hằng số ``PI`` (``3.141592``). Tỷ lệ giữa chu vi và đường kính của một đường tròn, đồng thời là số radian trong nửa vòng tròn.                               |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **TAU**  | Một hằng số ``TAU`` (``6.283185``). Tương đương với ``PI * 2`` và là số radian trong một vòng tròn đầy đủ.                                                       |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in float **E**    | Một hằng số ``E`` (``2.718281``). Số Euler, cơ số của logarit tự nhiên.                                                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Các biến dựng sẵn của sương mù
------------------------------

Tất cả các giá trị đầu ra của các thể tích sương mù đều chồng lấp lên nhau. Điều này cho phép
:ref:`FogVolumes <class_FogVolume>` được kết xuất hiệu quả vì tất cả chúng có thể được vẽ cùng lúc.

+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Biến dựng sẵn               | Mô tả                                                                                                                                                             |
+=============================+===================================================================================================================================================================+
| in vec3 **WORLD_POSITION**  | Vị trí của ô froxel hiện tại trong không gian thế giới.                                                                                                           |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **OBJECT_POSITION** | Vị trí tâm của :ref:`FogVolume <class_FogVolume>` hiện tại trong không gian thế giới.                                                                             |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **UVW**             | UV ba chiều, được dùng để ánh xạ texture 3D vào :ref:`FogVolume <class_FogVolume>` hiện tại.                                                                      |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **SIZE**            | Kích thước của :ref:`FogVolume <class_FogVolume>` hiện tại khi                                                                                                    |
|                             | :ref:`shape<class_FogVolume_property_shape>` có kích thước.                                                                                                       |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **SDF**             | Trường khoảng cách có dấu đến bề mặt của :ref:`FogVolume <class_FogVolume>`. Âm nếu nằm bên trong thể tích, dương trong các trường hợp khác.                      |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| out vec3 **ALBEDO**         | Giá trị màu cơ sở đầu ra, tương tác với ánh sáng để tạo ra màu cuối cùng. Chỉ được ghi vào thể tích sương mù nếu được sử dụng.                                    |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| out float **DENSITY**       | Giá trị mật độ đầu ra. Có thể là số âm để cho phép trừ một thể tích khỏi thể tích khác. Phải sử dụng Density thì shader sương mù mới ghi được bất kỳ dữ liệu nào. |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| out vec3 **EMISSION**       | Giá trị màu phát xạ đầu ra, được thêm vào màu trong lượt truyền ánh sáng để tạo ra màu cuối cùng. Chỉ được ghi vào thể tích sương mù nếu được sử dụng.            |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
