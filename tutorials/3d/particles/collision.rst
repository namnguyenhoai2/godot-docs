.. _doc_3d_particles_collision:

Va chạm hạt 3D
--------------

.. figure:: img/particle_collision.webp
   :alt: Va chạm hạt

Vì các hạt GPU được xử lý hoàn toàn trên GPU nên chúng không thể truy cập thế giới vật lý của trò chơi. Nếu cần các hạt va chạm với môi trường, bạn phải thiết lập các node va chạm hạt. Có bốn node: :ref:`class_GPUParticlesCollisionBox3D`, :ref:`class_GPUParticlesCollisionSphere3D`,
:ref:`class_GPUParticlesCollisionSDF3D`, và :ref:`class_GPUParticlesCollisionHeightField3D`.

Các thuộc tính chung
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_collision_common.webp
   :alt: Các thuộc tính va chạm hạt chung
   :align: right

   Các thuộc tính va chạm chung

Có một số thuộc tính mà bạn có thể tìm thấy trên tất cả các node va chạm. Chúng nằm trong phần ``GPUParticlesCollision3D`` của inspector.

Thuộc tính ``Cull Mask`` kiểm soát những hệ thống hạt nào bị ảnh hưởng bởi một node va chạm, dựa trên :ref:`các lớp khả kiến <class_VisualInstance3D>` của từng hệ thống. Một hệ thống hạt chỉ va chạm với node va chạm nếu ít nhất một trong các lớp khả kiến của hệ thống được bật trong cull mask của collider.

Va chạm hộp
~~~~~~~~~~~

.. figure:: img/particle_collision_box_entry.webp
   :alt: Hộp va chạm hạt
   :align: right

   Va chạm hộp trong danh sách node

Các node va chạm hộp có hình dạng như một khối hộp chữ nhật đặc. Bạn điều khiển kích thước của chúng bằng thuộc tính ``Extents``. Độ dài mỗi phía luôn được đo bằng một nửa kích thước giới hạn của hộp, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp rộng 2 mét ở mỗi phía. Các node va chạm hộp hữu ích để mô phỏng hình học sàn và tường mà các hạt cần va chạm vào.

Để tạo một node va chạm hộp, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesCollisionBox3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hộp hoặc gắn nó vào một node đang di chuyển để tạo các hiệu ứng linh động hơn.

.. figure:: img/particle_collision_box.webp
   :alt: Va chạm hộp với các hệ thống hạt

   Hai hệ thống hạt va chạm với một node va chạm hộp

Va chạm cầu
~~~~~~~~~~~

.. figure:: img/particle_collision_sphere_entry.webp
   :alt: Cầu va chạm hạt
   :align: right

   Va chạm cầu trong danh sách node

Các node va chạm cầu có hình dạng như một khối cầu đặc. Thuộc tính ``Radius`` kiểm soát kích thước của khối cầu. Mặc dù các node va chạm hộp không nhất thiết phải là hình lập phương hoàn hảo, các node va chạm cầu luôn là hình cầu. Nếu muốn thiết lập chiều rộng độc lập với chiều cao, bạn phải thay đổi thuộc tính ``Scale`` trong phần ``Node3D``.

Để tạo một node va chạm cầu, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesCollisionSphere3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của khối cầu hoặc gắn nó vào một node đang di chuyển để tạo các hiệu ứng linh động hơn.

.. figure:: img/particle_collision_sphere.webp
   :alt: Va chạm cầu với các hệ thống hạt

   Hai hệ thống hạt va chạm với một node va chạm cầu

Va chạm trường độ cao
~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_collision_height.webp
   :alt: Trường độ cao va chạm hạt
   :align: right

   Va chạm trường độ cao trong danh sách node

Va chạm hạt bằng trường độ cao rất hữu ích cho các khu vực ngoài trời rộng lớn cần va chạm với các hạt. Khi chạy, node sẽ tạo một trường độ cao từ tất cả mesh nằm trong phạm vi của nó và khớp với cull mask của nó. Các hạt va chạm với mesh mà trường độ cao này đại diện. Vì quá trình tạo trường độ cao được thực hiện động, nó có thể di chuyển theo camera của người chơi và phản ứng với các thay đổi trong level. Các thiết lập khác nhau cho mật độ trường độ cao cung cấp nhiều tùy chọn điều chỉnh hiệu năng.

Để tạo một node va chạm trường độ cao, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesCollisionHeightField3D`` từ danh sách các node khả dụng.

Một node va chạm trường độ cao có hình dạng như một khối hộp. Thuộc tính ``Extents`` kiểm soát kích thước của nó. Độ dài mỗi phía luôn được đo bằng một nửa kích thước giới hạn của nó, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp rộng 2 mét ở mỗi phía. Mọi thứ nằm ngoài kích thước giới hạn của node đều bị bỏ qua khi tạo trường độ cao.

Thuộc tính ``Resolution`` kiểm soát mức độ chi tiết của trường độ cao. Độ phân giải thấp hơn giúp xử lý nhanh hơn nhưng phải đánh đổi độ chính xác. Nếu độ phân giải của trường độ cao quá thấp, các hạt có thể trông như xuyên qua hình học của level hoặc bị mắc kẹt giữa không trung trong các sự kiện va chạm. Chúng cũng có thể hoàn toàn bỏ qua một số mesh nhỏ hơn.

.. figure:: img/particle_heightfield_res.webp
   :alt: Độ phân giải trường độ cao

   Ở độ phân giải thấp, va chạm trường độ cao bỏ sót một số chi tiết nhỏ (bên trái)

Thuộc tính ``Update Mode`` kiểm soát thời điểm trường độ cao được tạo lại từ các mesh nằm trong phạm vi của nó. Đặt thuộc tính này thành ``When Moved`` để chỉ làm mới khi node di chuyển. Cách này có hiệu năng tốt và phù hợp với các scene tĩnh không thay đổi thường xuyên. Nếu cần các hạt va chạm với những đối tượng động thường xuyên thay đổi vị trí, bạn có thể chọn ``Always`` để làm mới ở mỗi frame. Việc này làm giảm hiệu năng và chỉ nên được sử dụng khi cần thiết.

.. note::

   Điều quan trọng cần nhớ là khi ``Update Mode`` được đặt thành ``When Moved``, chính *node trường độ cao* di chuyển mới kích hoạt quá trình cập nhật. Trường độ cao không được cập nhật khi một trong các mesh bên trong nó di chuyển.

Khi được bật, thuộc tính ``Follow Camera Enabled`` khiến trường độ cao đi theo camera hiện tại. Nó sẽ được cập nhật mỗi khi camera di chuyển. Có thể sử dụng thuộc tính này để đảm bảo luôn có va chạm hạt xung quanh người chơi, đồng thời không lãng phí hiệu năng cho những khu vực khuất tầm nhìn hoặc ở quá xa.

Va chạm SDF
~~~~~~~~~~~

.. note::

     Va chạm hạt SDF chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. figure:: img/particle_collision_sdf_entry.webp
   :alt: SDF va chạm hạt
   :align: right

   Va chạm SDF trong danh sách node

Các node va chạm SDF tạo ra một `trường khoảng cách có hướng <https://www.reddit.com/r/explainlikeimfive/comments/k2zbos/eli5_what_are_distance_fields_in_graphics>`_ mà các hạt có thể va chạm. Va chạm SDF tương tự va chạm trường độ cao ở chỗ biến nhiều mesh trong phạm vi của nó thành một thể tích va chạm duy nhất cho các hạt. Một điểm khác biệt lớn là trường khoảng cách có hướng có thể biểu diễn các lỗ, đường hầm và phần nhô ra, điều không thể thực hiện chỉ bằng trường độ cao. Chi phí hiệu năng cao hơn so với trường độ cao, vì vậy chúng phù hợp nhất với các môi trường có quy mô nhỏ đến trung bình.

Để tạo một node va chạm SDF, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesCollisionSDF3D`` từ danh sách các node khả dụng. Các node va chạm SDF phải được bake thì mới có tác động đến các hạt trong level. Để thực hiện việc này, hãy nhấp vào nút :button:`Bake SDF` trên thanh công cụ viewport khi node va chạm SDF được chọn, rồi chọn một thư mục để lưu dữ liệu đã bake. Vì va chạm SDF cần được bake trong editor nên nó là tĩnh và không thể thay đổi khi chạy.

.. figure:: img/particle_collision_sdf.webp
   :alt: Va chạm hạt SDF

   Va chạm hạt SDF cho phép tạo các hình dạng va chạm 3 chiều rất chi tiết

Một node va chạm SDF có hình dạng như một khối hộp. Thuộc tính ``Extents`` kiểm soát kích thước của nó. Độ dài mỗi phía luôn được đo bằng một nửa kích thước giới hạn của nó, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp rộng 2 mét ở mỗi phía. Mọi thứ nằm ngoài kích thước giới hạn của node đều bị bỏ qua khi tính va chạm.

Thuộc tính ``Resolution`` kiểm soát mức độ chi tiết của trường khoảng cách. Độ phân giải thấp hơn cho tốc độ xử lý nhanh hơn nhưng làm giảm độ chính xác. Nếu độ phân giải quá thấp, các hạt có thể trông như xuyên qua hình học của level hoặc bị mắc kẹt giữa không trung trong các sự kiện va chạm. Chúng cũng có thể hoàn toàn bỏ qua một số mesh nhỏ hơn.

.. figure:: img/particle_collision_sdf_res.webp
   :alt: So sánh độ phân giải

   Cùng một khu vực được bao phủ bởi trường khoảng cách có hướng ở các độ phân giải khác nhau: 16 (bên trái) và 256 (bên phải)

Thuộc tính ``Thickness`` cung cấp cho trường khoảng cách, vốn thường rỗng ở bên trong, một độ dày để ngăn các hạt xuyên qua khi di chuyển ở tốc độ cao. Nếu bạn thấy một số hạt không va chạm với hình học của level mà thay vào đó bay thẳng xuyên qua, hãy thử đặt thuộc tính này thành giá trị cao hơn.

Thuộc tính ``Bake Mask`` kiểm soát những mesh nào sẽ được xem xét khi SDF được bake. Chỉ các mesh được render trên những layer đang hoạt động trong bake mask mới góp phần tạo va chạm cho hạt.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Để va chạm hạt hoạt động, :ref:`visibility AABB <doc_3d_particles_properties_draw>` của hạt phải chồng lấn với AABB của collider. Nếu va chạm có vẻ không hoạt động dù các collider đã được thiết lập, hãy tạo visibility AABB mới bằng cách chọn node GPUParticles3D rồi chọn **GPUParticles3D > Generate Visibility AABB…** ở đầu viewport trình chỉnh sửa 3D.

Nếu các hạt di chuyển nhanh và collider mỏng. Có hai giải pháp cho vấn đề này:

- Làm collider dày hơn. Chẳng hạn, nếu các hạt không thể đi xuống dưới một sàn đặc, bạn có thể làm collider đại diện cho sàn dày hơn phần thể hiện trực quan thực tế của nó. Collider heightfield tự động xử lý việc này theo thiết kế, vì heightfield không thể biểu diễn va chạm "phòng này chồng lên phòng kia".
- Tăng ``Fixed FPS`` trong node GPUParticles3D, nhờ đó việc kiểm tra va chạm sẽ được thực hiện thường xuyên hơn. Điều này làm giảm hiệu năng, vì vậy tránh đặt giá trị này quá cao.

.. _`signed distance field`: https://www.reddit.com/r/explainlikeimfive/comments/k2zbos/eli5_what_are_distance_fields_in_graphics
