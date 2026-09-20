.. _doc_using_jolt_physics:

Sử dụng Jolt Physics
====================

Giới thiệu
----------

Jolt physics engine được thêm vào như một lựa chọn thay thế cho Godot Physics physics engine hiện có trong 4.4. Jolt được Jorrit Rouwe phát triển, tập trung vào game và các ứng dụng VR. Trước đây, nó có sẵn dưới dạng extension nhưng hiện đã được tích hợp vào Godot. Theo mặc định, các project mới sẽ sử dụng nó làm physics engine.

Extension hiện có nay được xem là đang ở chế độ bảo trì. Điều đó có nghĩa là các bản sửa lỗi sẽ được hợp nhất và extension sẽ được duy trì khả năng tương thích với các phiên bản Godot mới cho đến khi module tích hợp có đầy đủ tính năng như extension. Hiện tại, thứ duy nhất còn thiếu là các joint liên quan, bạn có thể đọc thêm về chúng trên trang này. Extension có thể được tìm thấy `here on GitHub <https://github.com/godot-jolt/godot-jolt>`_ và trong asset library của Godot.

Để thay đổi 3D physics engine thành Jolt Physics, hãy đặt
:ref:`Project Settings > Physics > 3D > Physics Engine<class_ProjectSettings_property_physics/3D/Physics_Engine>`
thành ``Jolt Physics``. Sau khi hoàn tất, hãy nhấp vào nút **Save & Restart**. Khi editor mở lại, các cảnh 3D sẽ sử dụng Jolt cho physics.

Những khác biệt đáng chú ý so với Godot Physics
-----------------------------------------------

Có nhiều điểm khác biệt giữa Godot Physics engine hiện có và Jolt.

Các thuộc tính joint
~~~~~~~~~~~~~~~~~~~~

Các interface hiện tại cho những node joint 3D chưa hoàn toàn tương ứng với interface của các joint riêng của Jolt. Vì vậy, có một số thuộc tính joint không được hỗ trợ, chủ yếu là những thuộc tính liên quan đến việc cấu hình các giới hạn mềm của joint.

Các thuộc tính không được hỗ trợ là:

- PinJoint3D: ``bias``, ``damping``, ``impulse_clamp`` - HingeJoint3D: ``bias``, ``softness``, ``relaxation`` - SliderJoint3D: ``angular_\*``, ``\*_limit/softness``, ``\*_limit/restitution``, ``\*_limit/damping`` - ConeTwistJoint3D: ``bias``, ``relaxation``, ``softness`` - Generic6DOFJoint3D: ``*_limit_*/softness``, ``*_limit_*/restitution``, ``*_limit_*/damping``, ``*_limit_*/erp``

Hiện tại, một cảnh báo sẽ được đưa ra nếu bạn đặt các thuộc tính này thành bất kỳ giá trị nào khác giá trị mặc định.

Joint một body
~~~~~~~~~~~~~~

Trong Godot, bạn có thể bỏ qua một trong hai body của một joint hai body và về cơ bản để "world" làm body còn lại. Tuy nhiên, node path mà bạn gán body vào (:ref:`node_a<class_Joint3D_property_node_a>` so với :ref:`node_b<class_Joint3D_property_node_b>`) sẽ bị bỏ qua. Godot Physics sẽ luôn hoạt động như thể bạn đã gán nó vào ``node_a``, và vì ``node_a`` cũng là thứ xác định hệ quy chiếu cho các giới hạn của joint, cuối cùng bạn sẽ có các giới hạn bị đảo ngược và hình dạng giới hạn có thể kỳ lạ, đặc biệt khi các giới hạn của bạn cho phép cả bậc tự do tuyến tính và góc.

Thay vào đó, Jolt sẽ hoạt động như thể bạn đã gán body vào ``node_b``, với ``node_a`` đại diện cho "world". Có một project setting tên là :ref:`Physics > Jolt Physics 3D > Joints > World Node<class_ProjectSettings_property_physics/jolt_physics_3d/joints/world_node>` cho phép bạn bật tắt hành vi này nếu cần khả năng tương thích cho một project hiện có.

Collision margin
~~~~~~~~~~~~~~~~

Jolt (và các physics engine tương tự khác) sử dụng một thứ mà Jolt gọi là "convex radius" để giúp cải thiện hiệu năng và hành vi của các loại collision detection mà Jolt dựa vào cho các convex shape. Những physics engine khác (bao gồm Godot) có thể gọi chúng là "collision margins". Godot cung cấp chúng dưới dạng thuộc tính ``margin`` trên mọi class dẫn xuất từ Shape3D, nhưng bản thân Godot Physics không sử dụng chúng cho bất kỳ mục đích nào.

Những collision margin này đôi khi hoạt động trong các engine khác (như được mô tả trong tài liệu của Godot) bằng cách thêm một "shell" xung quanh shape, làm tăng nhẹ kích thước đồng thời bo tròn mọi cạnh/góc. Tuy nhiên, trong Jolt, các margin này trước tiên được dùng để thu nhỏ shape, sau đó "shell" được áp dụng, khiến các cạnh/góc cũng được bo tròn tương tự nhưng không làm tăng kích thước shape.

Để tránh phải điều chỉnh thủ công thuộc tính margin này, vì giá trị mặc định của nó có thể gây vấn đề với các shape nhỏ, module Jolt cung cấp một project setting tên là :ref:`Physics > Jolt Physics 3D > Collisions > Collision Margin Fraction<class_ProjectSettings_property_physics/jolt_physics_3d/collisions/collision_margin_fraction>`, giá trị này được nhân với trục nhỏ nhất của AABB của shape để tính margin thực tế. Sau đó, thuộc tính margin của shape được dùng làm giới hạn trên.

Trong hầu hết trường hợp sử dụng, các margin này ít nhiều sẽ hoạt động trong suốt, nhưng đôi khi có thể dẫn đến collision normal bất thường khi thực hiện các shape query. Bạn có thể giảm project setting được đề cập ở trên để giảm thiểu một phần hiện tượng này, kể cả đặt nó thành ``0.0``, nhưng margin quá nhỏ cũng có thể gây ra kết quả collision bất thường, vì vậy thường không được khuyến nghị.

Baumgarte stabilization
~~~~~~~~~~~~~~~~~~~~~~~

Baumgarte stabilization là một phương pháp xử lý các body xuyên vào nhau và đẩy chúng về trạng thái vừa chạm nhau. Trong Godot Physics, phương pháp này hoạt động giống như một lò xo. Điều đó có nghĩa là các body có thể tăng tốc và khiến chúng vượt quá vị trí rồi tách ra hoàn toàn. Với Jolt, stabilization chỉ được áp dụng cho vị trí chứ không áp dụng cho vận tốc của body. Điều đó có nghĩa là nó không thể vượt quá vị trí, nhưng có thể mất nhiều thời gian hơn để xử lý phần xuyên vào nhau.

Độ mạnh của stabilization này có thể được điều chỉnh bằng project setting
:ref:`Physics > Jolt Physics 3D > Simulation > Baumgarte Stabilization Factor<class_ProjectSettings_property_physics/jolt_physics_3d/simulation/baumgarte_stabilization_factor>`.
Đặt project setting này thành ``0.0`` sẽ tắt Baumgarte stabilization. Đặt thành ``1.0`` sẽ xử lý phần xuyên vào nhau trong 1 bước mô phỏng. Cách này nhanh nhưng thường cũng không ổn định.

Ghost collision
~~~~~~~~~~~~~~~

Jolt sử dụng hai kỹ thuật để giảm thiểu ghost collision, tức là các collision với những cạnh bên trong của shape/body tạo ra collision normal ngược với hướng chuyển động.

Kỹ thuật đầu tiên, được gọi là "active edge detection", đánh dấu các cạnh của tam giác dựa trên
:ref:`class_ConcavePolygonShape3D` or :ref:`class_HeightMapShape3D` as either "active" or "inactive", based on
góc với tam giác lân cận. Khi xảy ra collision với một cạnh không hoạt động, collision normal sẽ được thay thế bằng normal của tam giác để giảm ảnh hưởng của ghost collision.

Ngưỡng góc cho active edge detection này có thể được cấu hình thông qua project setting :ref:`Physics >Jolt Physics 3D > Collisions > Active Edge Threshold<class_ProjectSettings_property_physics/jolt_physics_3d/collisions/active_edge_threshold>`.

Kỹ thuật thứ hai, được gọi là "enhanced internal edge removal", thay vào đó thêm các bước kiểm tra runtime để phát hiện một cạnh đang hoạt động hay không hoạt động, dựa trên các contact point của hai body. Kỹ thuật này có ưu điểm là không chỉ áp dụng cho các collision với
:ref:`class_ConcavePolygonShape3D` and :ref:`class_HeightMapShape3D`, but also edges between any shapes within
cùng một body.

Enhanced internal edge removal có thể được bật và tắt cho nhiều context mà nó được áp dụng, bằng project setting :ref:`Physics >Jolt Physics 3D > Simulation > Use Enhanced Internal Edge Removal<class_ProjectSettings_property_physics/jolt_physics_3d/simulation/use_enhanced_internal_edge_removal>` và các setting tương tự cho :ref:`queries<class_ProjectSettings_property_physics/jolt_physics_3d/queries/use_enhanced_internal_edge_removal>` và :ref:`motion queries<class_ProjectSettings_property_physics/jolt_physics_3d/motion_queries/use_enhanced_internal_edge_removal>`.

Lưu ý rằng cả active edge detection lẫn enhanced internal edge removal đều không áp dụng khi xử lý ghost collision giữa hai body khác nhau.

Mức sử dụng bộ nhớ
~~~~~~~~~~~~~~~~~~

Jolt sử dụng stack allocator cho các allocation tạm thời trong bước mô phỏng. Stack allocator này yêu cầu cấp phát trước một lượng bộ nhớ cố định, có thể được cấu hình bằng project setting :ref:`Physics > Jolt Physics 3D > Limits > Temporary Memory Buffer Size<class_ProjectSettings_property_physics/jolt_physics_3d/limits/temporary_memory_buffer_size>`.

Face index của ray-cast
~~~~~~~~~~~~~~~~~~~~~~~

Thuộc tính ``face_index`` được trả về trong kết quả của :ref:`intersect_ray()<class_PhysicsDirectSpaceState3D_method_intersect_ray>` và RayCast3D theo mặc định sẽ luôn là ``-1`` với Jolt. Project setting :ref:`Physics > Jolt Physics 3D > Queries > Enable Ray Cast Face Index<class_ProjectSettings_property_physics/jolt_physics_3d/queries/enable_ray_cast_face_index>` sẽ bật chúng.

Lưu ý rằng việc bật setting này sẽ làm tăng yêu cầu bộ nhớ của :ref:`class_ConcavePolygonShape3D` khoảng 25%.

Contact của Kinematic RigidBody3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi sử dụng Jolt, một :ref:`class_RigidBody3D` bị đóng băng bằng :ref:`FREEZE_MODE_KINEMATIC<class_RigidBody3D_constant_FREEZE_MODE_KINEMATIC>` theo mặc định sẽ không báo cáo contact từ các collision với những body static/kinematic khác, vì lý do hiệu năng, ngay cả khi đặt :ref:`max_contacts_reported<class_RigidBody3D_property_max_contacts_reported>` khác không. Nếu bạn có nhiều body kinematic hoặc các body kinematic lớn chồng lấn với hình học static phức tạp, chẳng hạn như :ref:`class_ConcavePolygonShape3D` hoặc :ref:`class_HeightMapShape3D`, bạn có thể vô tình lãng phí đáng kể hiệu năng CPU và bộ nhớ.

Vì lý do này, hành vi này được bật tùy chọn thông qua project setting
:ref:`Physics > Jolt Physics 3D > Simulation > Generate All Kinematic Contacts<class_ProjectSettings_property_physics/jolt_physics_3d/simulation/generate_all_kinematic_contacts>`.

Contact impulse
~~~~~~~~~~~~~~~

Do những hạn chế nội tại của Jolt, các contact impulse do :ref:`PhysicsDirectBodyState3D.get_contact_impulse()<class_physicsdirectbodystate3d_method_get_contact_impulse>` cung cấp được ước tính trước dựa trên những yếu tố như contact manifold và vận tốc của các body va chạm. Điều này có nghĩa là các impulse được báo cáo chỉ chính xác trong những trường hợp hai body đang xét không va chạm với bất kỳ body nào khác.

Area3D và SoftBody3D
~~~~~~~~~~~~~~~~~~~~

Jolt hỗ trợ cùng một kiểu tương tác giữa :ref:`class_SoftBody3D` và
:ref:`class_Area3D` as Godot Physics, such as the wind and gravity properties found
trên :ref:`class_Area3D`. Tuy nhiên, không giống Godot Physics, Jolt cũng hỗ trợ các overlap signal và method khác nhau có trên :ref:`class_Area3D`, khi một :ref:`class_SoftBody3D` đi vào hoặc ra khỏi vùng overlap với nó, chẳng hạn như :ref:`body_entered<class_Area3D_signal_body_entered>`.

Để quay lại hành vi của Godot Physics, trong đó không có overlap signal nào được phát ra, bạn cần cấu hình :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>` của area sao cho không có overlap với :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` của soft body. Bạn cũng có thể tự lọc bất kỳ :ref:`class_SoftBody3D` nào trong kết nối signal.

WorldBoundaryShape3D
~~~~~~~~~~~~~~~~~~~~

:ref:`class_WorldBoundaryShape3D`, which is meant to represent an infinite plane, is
được triển khai hơi khác trong Jolt so với Godot Physics. Cả hai engine đều có giới hạn trên về kích thước hiệu dụng của plane này, nhưng kích thước này nhỏ hơn nhiều khi sử dụng Jolt để tránh các vấn đề về độ chính xác.

Bạn có thể cấu hình kích thước này bằng project setting :ref:`Physics > Jolt Physics 3D > Limits > World Boundary Shape Size<class_ProjectSettings_Property_physics/jolt_physics_3d/limits/world_boundary_shape_size>`.

Những khác biệt đáng chú ý so với Godot Jolt extension
------------------------------------------------------

Mặc dù Jolt module tích hợp phần lớn là bản port trực tiếp của Godot Jolt extension, vẫn có một vài điểm khác biệt.

Project setting
~~~~~~~~~~~~~~~

Tất cả project setting đã được chuyển từ category ``physics/jolt_3d`` sang ``physics/jolt_physics_3d``.

Ngoài ra, các tùy chọn cài đặt riêng lẻ của project cũng đã được đổi tên và refactor. Các tùy chọn này bao gồm:

- ``sleep/enabled`` hiện là ``simulation/allow_sleep.`` - ``sleep/velocity_threshold`` hiện là ``simulation/sleep_velocity_threshold.`` - ``sleep/time_threshold`` hiện là ``simulation/sleep_time_threshold.`` - ``collisions/use_shape_margins`` hiện là ``collisions/collision_margin_fraction``, trong đó giá trị 0 tương đương với việc tắt tùy chọn này. - ``collisions/use_enhanced_internal_edge_removal`` hiện là ``simulation/use_enhanced_internal_edge_removal``. - ``collisions/areas_detect_static_bodies`` hiện là ``simulation/areas_detect_static_bodies``. - ``collisions/report_all_kinematic_contacts`` hiện là ``simulation/generate_all_kinematic_contacts``. - ``collisions/soft_body_point_margin`` hiện là ``simulation/soft_body_point_radius``. - ``collisions/body_pair_cache_enabled`` hiện là ``simulation/body_pair_contact_cache_enabled``. - ``collisions/body_pair_cache_distance_threshold`` hiện là ``simulation/body_pair_contact_cache_distance_threshold``. - ``collisions/body_pair_cache_angle_threshold`` hiện là ``simulation/body_pair_contact_cache_angle_threshold``. - ``continuous_cd/movement_threshold`` hiện là ``simulation/continuous_cd_movement_threshold``, nhưng được biểu diễn dưới dạng phân số thay vì phần trăm. - ``continuous_cd/max_penetration`` hiện là ``simulation/continuous_cd_max_penetration``, nhưng được biểu diễn dưới dạng phân số thay vì phần trăm. - ``kinematics/use_enhanced_internal_edge_removal`` hiện là ``motion_queries/use_enhanced_internal_edge_removal.`` - ``kinematics/recovery_iterations`` hiện là ``motion_queries/recovery_iterations``, nhưng được biểu diễn dưới dạng phân số thay vì phần trăm. - ``kinematics/recovery_amount`` hiện là ``motion_queries/recovery_amount.`` - ``queries/use_legacy_ray_casting`` đã bị xóa. - ``solver/position_iterations`` hiện là ``simulation/position_steps.`` - ``solver/velocity_iterations`` hiện là ``simulation/velocity_steps.`` - ``solver/position_correction`` hiện là ``simulation/baumgarte_stabilization_factor``, nhưng được biểu diễn dưới dạng phân số thay vì phần trăm. - ``solver/active_edge_threshold`` hiện là ``collisions/active_edge_threshold.`` - ``solver/bounce_velocity_threshold`` hiện là ``simulation/bounce_velocity_threshold.`` - ``solver/contact_speculative_distance`` hiện là ``simulation/speculative_contact_distance.`` - ``solver/contact_allowed_penetration`` hiện là ``simulation/penetration_slop.`` - ``limits/max_angular_velocity`` hiện được lưu dưới dạng radian. - ``limits/max_temporary_memory`` hiện là ``limits/temporary_memory_buffer_size.``

Các node khớp
~~~~~~~~~~~~~

Các node khớp được cung cấp trong extension Godot Jolt (JoltPinJoint3D, JoltHingeJoint3D, JoltSliderJoint3D, JoltConeTwistJoint3D và JoltGeneric6DOFJoint) không được đưa vào module Jolt.

Tính an toàn luồng
~~~~~~~~~~~~~~~~~~

Không giống extension Godot Jolt, module Jolt có hỗ trợ thread-safety, bao gồm hỗ trợ cho tùy chọn cài đặt project :ref:`Physics > 3D > Run On Separate Thread<class_ProjectSettings_Property_physics/3d/run_on_separate_thread>`. Tuy nhiên, tính năng này chưa được kiểm thử thật kỹ lưỡng, vì vậy nên được xem là experimental.
