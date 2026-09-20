.. _doc_3d_particles_collision:

Va chạm particle 3D
-------------------

.. figure:: img/particle_collision.webp
   :alt: Particle collisions

Vì GPU particle được xử lý hoàn toàn trên GPU nên chúng không thể truy cập thế giới vật lý của trò chơi. Nếu bạn cần particle va chạm với môi trường, bạn phải thiết lập các node particle collision. Có bốn node: :ref:`class_GPUParticlesCollisionBox3D`, :ref:`class_GPUParticlesCollisionSphere3D`,
:ref:`class_GPUParticlesCollisionSDF3D`, and :ref:`class_GPUParticlesCollisionHeightField3D`.

Các thuộc tính chung
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_collision_common.webp
   :alt: Common particle collision properties
   :align: right

   Common collision properties

Có một số thuộc tính bạn có thể tìm thấy trên tất cả các node collision. Chúng nằm trong phần ``GPUParticlesCollision3D`` của inspector.

Thuộc tính ``Cull Mask`` kiểm soát những particle system nào bị ảnh hưởng bởi một node collision dựa trên :ref:`visibility layers <class_VisualInstance3D>` của từng system. Một particle system chỉ va chạm với node collision nếu ít nhất một visibility layer của system đó được bật trong cull mask của collider.

Box collision
~~~~~~~~~~~~~

.. figure:: img/particle_collision_box_entry.webp
   :alt: Particle collision box
   :align: right

   Box collision in the node list

Các node box collision có hình dạng như một khối hộp chữ nhật đặc. Bạn điều khiển kích thước của chúng bằng thuộc tính ``Extents``. Extents của box luôn đo bằng một nửa các cạnh của bounds, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một box rộng 2 mét ở mỗi phía. Các node box collision hữu ích để mô phỏng hình học sàn và tường mà particle cần va chạm.

Để tạo một node box collision, hãy thêm một node con mới vào scene và chọn ``GPUParticlesCollisionBox3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của box hoặc gắn nó vào một node đang di chuyển để tạo các hiệu ứng linh động hơn.

.. figure:: img/particle_collision_box.webp
   :alt: Box collision with particle systems

   Two particle systems collide with a box collision node

Sphere collision
~~~~~~~~~~~~~~~~

.. figure:: img/particle_collision_sphere_entry.webp
   :alt: Particle collision sphere
   :align: right

   Sphere collision in the node list

Các node sphere collision có hình dạng như một hình cầu đặc. Thuộc tính ``Radius`` kiểm soát kích thước của hình cầu. Mặc dù các node box collision không nhất thiết phải là hình lập phương hoàn hảo, các node sphere collision sẽ luôn là hình cầu. Nếu muốn thiết lập chiều rộng độc lập với chiều cao, bạn phải thay đổi thuộc tính ``Scale`` trong phần ``Node3D``.

Để tạo một node sphere collision, hãy thêm một node con mới vào scene và chọn ``GPUParticlesCollisionSphere3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hình cầu hoặc gắn nó vào một node đang di chuyển để tạo các hiệu ứng linh động hơn.

.. figure:: img/particle_collision_sphere.webp
   :alt: Sphere collision with particle systems

   Two particle systems collide with a sphere collision node

Height field collision
~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_collision_height.webp
   :alt: Particle collision height field
   :align: right

   Height field collision in the node list

Height field particle collision rất hữu ích cho các khu vực ngoài trời rộng lớn cần va chạm với particle. Khi runtime, node sẽ tạo một height field từ tất cả mesh nằm trong bounds của nó và khớp với cull mask. Particle sẽ va chạm với mesh mà height field này đại diện. Vì height field được tạo động, nó có thể di chuyển theo camera của người chơi và phản ứng với các thay đổi trong level. Các thiết lập khác nhau cho density của height field mang lại nhiều tùy chọn điều chỉnh performance.

Để tạo một node height field collision, hãy thêm một node con mới vào scene và chọn ``GPUParticlesCollisionHeightField3D`` từ danh sách các node khả dụng.

Node height field collision có hình dạng như một box. Thuộc tính ``Extents`` kiểm soát kích thước của nó. Extents luôn đo bằng một nửa các cạnh của bounds, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một box rộng 2 mét ở mỗi phía. Mọi thứ nằm ngoài extents của node đều bị bỏ qua khi tạo height field.

Thuộc tính ``Resolution`` kiểm soát mức độ chi tiết của height field. Resolution thấp hơn sẽ có performance nhanh hơn nhưng phải đánh đổi độ chính xác. Nếu resolution của height field quá thấp, particle có thể trông như xuyên qua hình học của level hoặc bị kẹt giữa không trung trong các sự kiện va chạm. Chúng cũng có thể hoàn toàn bỏ qua một số mesh nhỏ hơn.

.. figure:: img/particle_heightfield_res.webp
   :alt: Height field resolutions

   At low resolutions, height field collision misses some finer details (left)

Thuộc tính ``Update Mode`` kiểm soát thời điểm height field được tạo lại từ các mesh nằm trong bounds của nó. Đặt thành ``When Moved`` để chỉ làm mới khi nó di chuyển. Cách này có performance tốt và phù hợp với các scene tĩnh không thay đổi thường xuyên. Nếu cần particle va chạm với các object động thường xuyên thay đổi vị trí, bạn có thể chọn ``Always`` để làm mới mỗi frame. Cách này ảnh hưởng đến performance và chỉ nên được sử dụng khi cần thiết.

.. note::

   Điều quan trọng cần nhớ là khi ``Update Mode`` được đặt thành ``When Moved``, chính *height field node* di chuyển mới kích hoạt việc cập nhật. Height field sẽ không được cập nhật khi một trong các mesh bên trong nó di chuyển.

Thuộc tính ``Follow Camera Enabled`` khiến height field bám theo camera hiện tại khi được bật. Nó sẽ cập nhật mỗi khi camera di chuyển. Có thể dùng thuộc tính này để đảm bảo luôn có particle collision xung quanh người chơi, đồng thời không lãng phí performance cho những khu vực khuất tầm nhìn hoặc ở quá xa.

SDF collision
~~~~~~~~~~~~~

.. note::

     Particle SDF collision chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. figure:: img/particle_collision_sdf_entry.webp
   :alt: Particle collision SDF
   :align: right

   SDF collision in the node list

Các node SDF collision tạo một `trường khoảng cách có dấu <https://www.reddit.com/r/explainlikeimfive/comments/k2zbos/eli5_what_are_distance_fields_in_graphics>`_ mà particle có thể va chạm. SDF collision tương tự height field collision ở chỗ biến nhiều mesh nằm trong bounds của nó thành một volume collision duy nhất cho particle. Một điểm khác biệt quan trọng là signed distance field có thể biểu diễn các lỗ, đường hầm và phần nhô ra, điều mà chỉ dùng height field thì không thể thực hiện. Chi phí performance lớn hơn so với height field, vì vậy chúng phù hợp nhất với các môi trường có kích thước nhỏ đến trung bình.

Để tạo một node SDF collision, hãy thêm một node con mới vào scene và chọn ``GPUParticlesCollisionSDF3D`` từ danh sách các node khả dụng. Các node SDF collision phải được bake để có thể tác động đến particle trong level. Để thực hiện việc đó, hãy nhấp vào nút :button:`Bake SDF` trên viewport toolbar khi node SDF collision được chọn, rồi chọn một thư mục để lưu dữ liệu đã bake. Vì SDF collision cần được bake trong editor nên nó là static và không thể thay đổi khi runtime.

.. figure:: img/particle_collision_sdf.webp
   :alt: SDF particle collision

   SDF particle collision allows for very detailed 3-dimensional collision shapes

Node SDF collision có hình dạng như một box. Thuộc tính ``Extents`` kiểm soát kích thước của nó. Extents luôn đo bằng một nửa các cạnh của bounds, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một box rộng 2 mét ở mỗi phía. Mọi thứ nằm ngoài extents của node đều bị bỏ qua khi collision.

Thuộc tính ``Resolution`` kiểm soát mức độ chi tiết của distance field. Resolution thấp hơn sẽ có performance nhanh hơn nhưng phải đánh đổi độ chính xác. Nếu resolution quá thấp, particle có thể trông như xuyên qua hình học của level hoặc bị kẹt giữa không trung trong các sự kiện va chạm. Chúng cũng có thể hoàn toàn bỏ qua một số mesh nhỏ hơn.

.. figure:: img/particle_collision_sdf_res.webp
   :alt: Resolution comparison

   The same area covered by a signed distance field at different resolutions: 16 (left) and 256 (right)

Thuộc tính ``Thickness`` cung cấp cho distance field, vốn thường rỗng ở bên trong, một độ dày để ngăn particle xuyên qua khi di chuyển ở tốc độ cao. Nếu bạn nhận thấy một số particle không va chạm với hình học của level mà thay vào đó bay xuyên thẳng qua, hãy thử đặt thuộc tính này thành giá trị cao hơn.

Thuộc tính ``Bake Mask`` kiểm soát những mesh nào sẽ được xem xét khi SDF được bake. Chỉ các mesh render trên những layer đang hoạt động trong bake mask mới góp phần vào particle collision.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Để particle collision hoạt động, :ref:`visibility AABB <doc_3d_particles_properties_draw>` của particle phải chồng lấp với AABB của collider. Nếu collision có vẻ không hoạt động dù các collider đã được thiết lập, hãy tạo visibility AABB đã cập nhật bằng cách chọn node GPUParticles3D và chọn **GPUParticles3D > Generate Visibility AABB…** ở đầu viewport của 3D editor.

Nếu particle di chuyển nhanh còn collider thì mỏng. Có hai cách giải quyết vấn đề này:

- Làm collider dày hơn. Ví dụ, nếu particle không thể xuống dưới một sàn đặc, bạn có thể làm collider đại diện cho sàn dày hơn phần hiển thị thực tế của nó. Heightfield collider tự động xử lý việc này theo thiết kế, vì heightfield không thể biểu diễn collision kiểu "room over room". - Tăng ``Fixed FPS`` trong node GPUParticles3D, thao tác này sẽ thực hiện kiểm tra collision thường xuyên hơn. Điều này phải đánh đổi performance, vì vậy tránh đặt giá trị này quá cao.
