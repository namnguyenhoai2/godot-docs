.. _doc_using_jolt_physics:

Sử dụng Jolt Physics
====================

Giới thiệu
----------

Động cơ vật lý Jolt được bổ sung như một lựa chọn thay thế cho động cơ vật lý Godot Physics hiện có trong phiên bản 4.4. Jolt được Jorrit Rouwe phát triển, tập trung vào game và các ứng dụng VR. Trước đây, Jolt có sẵn dưới dạng extension, nhưng hiện đã được tích hợp vào Godot. Theo mặc định, các dự án mới sẽ sử dụng Jolt làm động cơ vật lý.

Extension hiện có nay được xem là đang trong chế độ bảo trì. Điều đó có nghĩa là các bản sửa lỗi sẽ được hợp nhất và extension sẽ được duy trì khả năng tương thích với các phiên bản Godot mới cho đến khi module tích hợp có đầy đủ tính năng như extension. Hiện tại, điểm duy nhất còn thiếu là các joint liên quan, bạn có thể đọc thêm về chúng trên trang này. Extension có thể được tìm thấy `tại đây trên GitHub <https://github.com/godot-jolt/godot-jolt>`_ và trong thư viện tài nguyên của Godot.

Để thay đổi động cơ vật lý 3D thành Jolt Physics, hãy đặt
:ref:`Project Settings > Physics > 3D > Physics Engine <class_ProjectSettings_property_physics/3D/Physics_Engine>` thành ``Jolt Physics``. Sau khi thực hiện xong, hãy nhấp vào nút **Save & Restart**. Khi trình chỉnh sửa mở lại, các cảnh 3D sẽ sử dụng Jolt cho vật lý.

Những khác biệt đáng chú ý so với Godot Physics
-----------------------------------------------

Có nhiều điểm khác biệt giữa động cơ Godot Physics hiện có và Jolt.

Thuộc tính joint
~~~~~~~~~~~~~~~~

Các interface hiện tại của những node joint 3D không hoàn toàn tương ứng với interface của các joint riêng của Jolt. Vì vậy, có một số thuộc tính joint không được hỗ trợ, chủ yếu là các thuộc tính liên quan đến việc cấu hình giới hạn mềm của joint.

Các thuộc tính không được hỗ trợ là:

- PinJoint3D: ``bias``, ``damping``, ``impulse_clamp``
- HingeJoint3D: ``bias``, ``softness``, ``relaxation``
- SliderJoint3D: ``angular_\*``, ``\*_limit/softness``, ``\*_limit/restitution``, ``\*_limit/damping``
- ConeTwistJoint3D: ``bias``, ``relaxation``, ``softness``
- Generic6DOFJoint3D: ``*_limit_*/softness``, ``*_limit_*/restitution``, ``*_limit_*/damping``, ``*_limit_*/erp``

Hiện tại, một cảnh báo sẽ được phát ra nếu bạn đặt các thuộc tính này thành giá trị khác với giá trị mặc định.

Joint một thân
~~~~~~~~~~~~~~

Trong Godot, bạn có thể bỏ qua một trong hai body của joint hai body và thực chất để "thế giới" làm body còn lại. Tuy nhiên, đường dẫn node mà bạn gán body vào (:ref:`node_a<class_Joint3D_property_node_a>` so với :ref:`node_b<class_Joint3D_property_node_b>`) sẽ bị bỏ qua. Godot Physics sẽ luôn hoạt động như thể bạn đã gán nó vào ``node_a``, và vì ``node_a`` cũng xác định hệ quy chiếu cho các giới hạn của joint, bạn sẽ nhận được các giới hạn bị đảo ngược và một hình dạng giới hạn có khả năng kỳ lạ, đặc biệt nếu các giới hạn của bạn cho phép cả bậc tự do tuyến tính và góc.

Jolt sẽ hoạt động như thể bạn đã gán body vào ``node_b`` thay vào đó, với ``node_a`` đại diện cho "thế giới". Có một thiết lập dự án tên là :ref:`Physics > Jolt Physics 3D > Joints > World Node <class_ProjectSettings_property_physics/jolt_physics_3d/joints/world_node>` cho phép bạn bật hoặc tắt hành vi này nếu cần khả năng tương thích với một dự án hiện có.

Biên va chạm
~~~~~~~~~~~~

Jolt (và các động cơ vật lý tương tự khác) sử dụng một thứ mà Jolt gọi là "bán kính lồi" để giúp cải thiện hiệu suất và hành vi của các kiểu phát hiện va chạm mà Jolt dựa vào cho các hình dạng lồi. Các động cơ vật lý khác (bao gồm Godot) có thể gọi chúng là "biên va chạm". Godot cung cấp các giá trị này dưới dạng thuộc tính ``margin`` trên mọi lớp bắt nguồn từ Shape3D, nhưng bản thân Godot Physics không sử dụng chúng cho bất kỳ mục đích nào.

Trong các động cơ khác, các biên va chạm này đôi khi có tác dụng như được mô tả trong tài liệu của Godot: thực chất thêm một "lớp vỏ" xung quanh hình dạng, làm tăng nhẹ kích thước đồng thời bo tròn mọi cạnh/góc. Tuy nhiên, trong Jolt, trước tiên các biên này được dùng để thu nhỏ hình dạng, sau đó "lớp vỏ" được áp dụng, tạo ra các cạnh/góc được bo tròn tương tự nhưng không làm tăng kích thước hình dạng.

Để không phải điều chỉnh thủ công thuộc tính biên này, vì giá trị mặc định của nó có thể gây vấn đề với các hình dạng nhỏ, module Jolt cung cấp một thiết lập dự án tên là :ref:`Physics > Jolt Physics 3D > Collisions > Collision Margin Fraction <class_ProjectSettings_property_physics/jolt_physics_3d/collisions/collision_margin_fraction>`, giá trị này được nhân với trục nhỏ nhất của AABB của hình dạng để tính biên thực tế. Sau đó, thuộc tính biên của hình dạng được dùng làm giới hạn trên.

Trong hầu hết trường hợp sử dụng, các biên này sẽ ít nhiều hoạt động một cách trong suốt, nhưng đôi khi có thể tạo ra các pháp tuyến va chạm bất thường khi thực hiện truy vấn hình dạng. Bạn có thể giảm thiết lập dự án nêu trên để khắc phục một phần vấn đề này, kể cả đặt thành ``0.0``, nhưng biên quá nhỏ cũng có thể gây ra kết quả va chạm bất thường, nên nhìn chung không được khuyến nghị.

Ổn định hóa Baumgarte
~~~~~~~~~~~~~~~~~~~~~

Ổn định hóa Baumgarte là một phương pháp xử lý các body xuyên vào nhau và đẩy chúng về trạng thái vừa chạm nhau. Trong Godot Physics, phương pháp này hoạt động giống như một lò xo. Điều đó có nghĩa là các body có thể tăng tốc, khiến chúng vượt quá vị trí cần thiết rồi tách hẳn ra. Với Jolt, quá trình ổn định hóa chỉ được áp dụng cho vị trí chứ không áp dụng cho vận tốc của body. Điều này có nghĩa là hiện tượng vượt quá sẽ không xảy ra, nhưng có thể mất nhiều thời gian hơn để xử lý phần xuyên vào nhau.

Bạn có thể điều chỉnh độ mạnh của quá trình ổn định hóa này bằng thiết lập dự án
:ref:`Physics > Jolt Physics 3D > Simulation > Baumgarte Stabilization Factor <class_ProjectSettings_property_physics/jolt_physics_3d/simulation/baumgarte_stabilization_factor>`. Đặt thiết lập dự án này thành ``0.0`` sẽ tắt ổn định hóa Baumgarte. Đặt thành ``1.0`` sẽ xử lý phần xuyên vào nhau trong 1 bước mô phỏng. Cách này nhanh nhưng thường cũng không ổn định.

Va chạm ảo
~~~~~~~~~~

Jolt sử dụng hai kỹ thuật để giảm thiểu va chạm ảo, tức các va chạm với những cạnh bên trong của hình dạng/body tạo ra các pháp tuyến va chạm ngược hướng chuyển động.

Kỹ thuật đầu tiên, được gọi là "phát hiện cạnh chủ động", đánh dấu các cạnh của tam giác trong
:ref:`class_ConcavePolygonShape3D` hoặc :ref:`class_HeightMapShape3D` là "chủ động" hoặc "không hoạt động", dựa trên góc với tam giác lân cận. Khi xảy ra va chạm với một cạnh không hoạt động, pháp tuyến va chạm sẽ được thay thế bằng pháp tuyến của tam giác để giảm tác động của va chạm ảo.

Ngưỡng góc cho tính năng phát hiện cạnh chủ động này có thể được cấu hình thông qua thiết lập dự án :ref:`Physics >Jolt Physics 3D > Collisions > Active Edge Threshold <class_ProjectSettings_property_physics/jolt_physics_3d/collisions/active_edge_threshold>`.

Kỹ thuật thứ hai, được gọi là "loại bỏ cạnh bên trong nâng cao", thay vào đó bổ sung các bước kiểm tra tại runtime để phát hiện xem một cạnh là chủ động hay không hoạt động, dựa trên các điểm tiếp xúc của hai body. Kỹ thuật này có ưu điểm là không chỉ áp dụng cho các va chạm với
:ref:`class_ConcavePolygonShape3D` và :ref:`class_HeightMapShape3D`, mà còn áp dụng cho các cạnh giữa mọi hình dạng trong cùng một body.

Có thể bật và tắt tính năng loại bỏ cạnh bên trong nâng cao cho các ngữ cảnh khác nhau mà tính năng này được áp dụng bằng thiết lập dự án :ref:`Physics >Jolt Physics 3D > Simulation > Use Enhanced Internal Edge Removal <class_ProjectSettings_property_physics/jolt_physics_3d/simulation/use_enhanced_internal_edge_removal>`, cùng các thiết lập tương tự cho :ref:`queries<class_ProjectSettings_property_physics/jolt_physics_3d/queries/use_enhanced_internal_edge_removal>` và :ref:`motion queries <class_ProjectSettings_property_physics/jolt_physics_3d/motion_queries/use_enhanced_internal_edge_removal>`.

Lưu ý rằng cả tính năng phát hiện cạnh chủ động lẫn loại bỏ cạnh bên trong nâng cao đều không áp dụng khi xử lý các va chạm ma giữa hai body khác nhau.

Mức sử dụng bộ nhớ
~~~~~~~~~~~~~~~~~~

Jolt sử dụng một bộ cấp phát ngăn xếp cho các vùng nhớ tạm thời trong bước mô phỏng. Bộ cấp phát ngăn xếp này yêu cầu cấp phát trước một lượng bộ nhớ cố định, có thể được cấu hình bằng thiết lập project :ref:`Physics > Jolt Physics 3D > Limits > Temporary Memory Buffer Size <class_ProjectSettings_property_physics/jolt_physics_3d/limits/temporary_memory_buffer_size>`.

Chỉ mục mặt khi ray-cast
~~~~~~~~~~~~~~~~~~~~~~~~

Thuộc tính ``face_index`` được trả về trong kết quả của :ref:`intersect_ray()<class_PhysicsDirectSpaceState3D_method_intersect_ray>` và RayCast3D theo mặc định sẽ luôn là ``-1`` với Jolt. Thiết lập project :ref:`Physics > Jolt Physics 3D > Queries > Enable Ray Cast Face Index <class_ProjectSettings_property_physics/jolt_physics_3d/queries/enable_ray_cast_face_index>` sẽ bật chúng.

Lưu ý rằng việc bật thiết lập này sẽ làm tăng yêu cầu bộ nhớ của :ref:`class_ConcavePolygonShape3D` khoảng 25%.

Các contact của Kinematic RigidBody3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi sử dụng Jolt, một :ref:`class_RigidBody3D` bị đóng băng bằng :ref:`FREEZE_MODE_KINEMATIC<class_RigidBody3D_constant_FREEZE_MODE_KINEMATIC>` theo mặc định sẽ không báo cáo các contact từ va chạm với các body static/kinematic khác, vì lý do hiệu năng, ngay cả khi đặt :ref:`max_contacts_reported<class_RigidBody3D_property_max_contacts_reported>` khác không. Nếu bạn có nhiều body kinematic hoặc các body kinematic lớn chồng lấn với hình học static phức tạp, chẳng hạn như :ref:`class_ConcavePolygonShape3D` hoặc :ref:`class_HeightMapShape3D`, bạn có thể vô tình lãng phí một lượng đáng kể hiệu năng CPU và bộ nhớ.

Vì lý do này, hành vi này được bật tùy chọn thông qua thiết lập project
:ref:`Physics > Jolt Physics 3D > Simulation > Generate All Kinematic Contacts <class_ProjectSettings_property_physics/jolt_physics_3d/simulation/generate_all_kinematic_contacts>`.

Xung lực contact
~~~~~~~~~~~~~~~~

Do những hạn chế nội tại của Jolt, các xung lực contact do :ref:`PhysicsDirectBodyState3D.get_contact_impulse()<class_physicsdirectbodystate3d_method_get_contact_impulse>` cung cấp được ước tính trước dựa trên những yếu tố như contact manifold và vận tốc của các body đang va chạm. Điều này có nghĩa là các xung lực được báo cáo chỉ chính xác trong những trường hợp hai body đang xét không va chạm với bất kỳ body nào khác.

Area3D và SoftBody3D
~~~~~~~~~~~~~~~~~~~~

Jolt hỗ trợ cùng loại tương tác giữa :ref:`class_SoftBody3D` và
:ref:`class_Area3D` như Godot Physics, chẳng hạn như các thuộc tính gió và trọng lực trên :ref:`class_Area3D`. Tuy nhiên, khác với Godot Physics, Jolt cũng hỗ trợ các signal và phương thức overlap khác nhau trên :ref:`class_Area3D`, được dùng khi một :ref:`class_SoftBody3D` đi vào hoặc rời khỏi vùng overlap với nó, chẳng hạn như :ref:`body_entered<class_Area3D_signal_body_entered>`.

Để khôi phục hành vi của Godot Physics, trong đó không có signal overlap nào được phát ra, bạn cần cấu hình :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>` của area sao cho không có vùng overlap với :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` của soft body. Bạn cũng có thể tự lọc bất kỳ :ref:`class_SoftBody3D` nào trong kết nối signal.

WorldBoundaryShape3D
~~~~~~~~~~~~~~~~~~~~

:ref:`class_WorldBoundaryShape3D`, vốn được dùng để biểu diễn một mặt phẳng vô hạn, được triển khai hơi khác trong Jolt so với Godot Physics. Cả hai engine đều có giới hạn trên về kích thước hiệu dụng của mặt phẳng này, nhưng kích thước đó nhỏ hơn nhiều khi sử dụng Jolt để tránh các vấn đề về độ chính xác.

Bạn có thể cấu hình kích thước này bằng thiết lập project :ref:`Physics > Jolt Physics 3D > Limits > World Boundary Shape Size <class_ProjectSettings_Property_physics/jolt_physics_3d/limits/world_boundary_shape_size>`.

Những khác biệt đáng chú ý so với extension Godot Jolt
------------------------------------------------------

Mặc dù module Jolt tích hợp phần lớn là bản port trực tiếp của extension Godot Jolt, vẫn có một vài điểm khác biệt.

Thiết lập project
~~~~~~~~~~~~~~~~~

Tất cả thiết lập project đã được chuyển từ danh mục ``physics/jolt_3d`` sang ``physics/jolt_physics_3d``.

Ngoài ra, một số thiết lập project riêng lẻ cũng đã được đổi tên và tái cấu trúc. Các thay đổi bao gồm:

- ``sleep/enabled`` hiện là ``simulation/allow_sleep.``
- ``sleep/velocity_threshold`` hiện là ``simulation/sleep_velocity_threshold.``
- ``sleep/time_threshold`` hiện là ``simulation/sleep_time_threshold.``
- ``collisions/use_shape_margins`` hiện là ``collisions/collision_margin_fraction``, trong đó giá trị 0 tương đương với việc tắt thiết lập này.
- ``collisions/use_enhanced_internal_edge_removal`` hiện là ``simulation/use_enhanced_internal_edge_removal``.
- ``collisions/areas_detect_static_bodies`` hiện là ``simulation/areas_detect_static_bodies``.
- ``collisions/report_all_kinematic_contacts`` hiện là ``simulation/generate_all_kinematic_contacts``.
- ``collisions/soft_body_point_margin`` hiện là ``simulation/soft_body_point_radius``.
- ``collisions/body_pair_cache_enabled`` hiện là ``simulation/body_pair_contact_cache_enabled``.
- ``collisions/body_pair_cache_distance_threshold`` hiện là ``simulation/body_pair_contact_cache_distance_threshold``.
- ``collisions/body_pair_cache_angle_threshold`` hiện là ``simulation/body_pair_contact_cache_angle_threshold``.
- ``continuous_cd/movement_threshold`` hiện là ``simulation/continuous_cd_movement_threshold``, nhưng được biểu thị dưới dạng phân số thay vì phần trăm.
- ``continuous_cd/max_penetration`` hiện là ``simulation/continuous_cd_max_penetration``, nhưng được biểu thị dưới dạng phân số thay vì phần trăm.
- ``kinematics/use_enhanced_internal_edge_removal`` hiện là ``motion_queries/use_enhanced_internal_edge_removal.``
- ``kinematics/recovery_iterations`` hiện là ``motion_queries/recovery_iterations``, nhưng được biểu thị dưới dạng phân số thay vì phần trăm.
- ``kinematics/recovery_amount`` hiện là ``motion_queries/recovery_amount.``
- ``queries/use_legacy_ray_casting`` đã bị xóa.
- ``solver/position_iterations`` hiện là ``simulation/position_steps.``
- ``solver/velocity_iterations`` hiện là ``simulation/velocity_steps.``
- ``solver/position_correction`` hiện là ``simulation/baumgarte_stabilization_factor``, nhưng được biểu thị dưới dạng phân số thay vì phần trăm.
- ``solver/active_edge_threshold`` hiện là ``collisions/active_edge_threshold.``
- ``solver/bounce_velocity_threshold`` hiện là ``simulation/bounce_velocity_threshold.``
- ``solver/contact_speculative_distance`` hiện là ``simulation/speculative_contact_distance.``
- ``solver/contact_allowed_penetration`` hiện là ``simulation/penetration_slop.``
- ``limits/max_angular_velocity`` hiện được lưu dưới dạng radian.
- ``limits/max_temporary_memory`` hiện là ``limits/temporary_memory_buffer_size.``

Các node joint
~~~~~~~~~~~~~~

Các node joint được cung cấp trong extension Godot Jolt (JoltPinJoint3D, JoltHingeJoint3D, JoltSliderJoint3D, JoltConeTwistJoint3D và JoltGeneric6DOFJoint) không được đưa vào module Jolt.

Tính an toàn luồng
~~~~~~~~~~~~~~~~~~

Khác với extension Godot Jolt, module Jolt có tính an toàn luồng, bao gồm hỗ trợ thiết lập project :ref:`Physics > 3D > Run On Separate Thread <class_ProjectSettings_Property_physics/3d/run_on_separate_thread>`. Tuy nhiên, tính năng này chưa được kiểm thử đầy đủ, vì vậy nên được xem là thử nghiệm.

.. _`here on GitHub`: https://github.com/godot-jolt/godot-jolt
