:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Camera3D.xml.

.. _class_Camera3D:

Camera3D
========

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`XRCamera3D<class_XRCamera3D>`

Node camera, hiển thị từ một góc nhìn.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Camera3D** là một node đặc biệt, hiển thị những gì có thể nhìn thấy từ vị trí hiện tại của nó. Các camera tự đăng ký với node :ref:`Viewport<class_Viewport>` gần nhất (khi đi ngược lên cây). Mỗi viewport chỉ có thể có một camera hoạt động. Nếu không có viewport nào khả dụng khi đi ngược lên cây, camera sẽ đăng ký với global viewport. Nói cách khác, camera chỉ cung cấp khả năng hiển thị 3D cho một :ref:`Viewport<class_Viewport>`, và nếu không có một node như vậy thì một scene được đăng ký trong :ref:`Viewport<class_Viewport>` đó (hoặc các viewport cao hơn) không thể được hiển thị.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`CameraAttributes<class_CameraAttributes>`       | :ref:`attributes<class_Camera3D_property_attributes>`             |                   |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`Compositor<class_Compositor>`                   | :ref:`compositor<class_Camera3D_property_compositor>`             |                   |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                 | :ref:`cull_mask<class_Camera3D_property_cull_mask>`               | ``1048575``       |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                               | :ref:`current<class_Camera3D_property_current>`                   | ``false``         |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` | :ref:`doppler_tracking<class_Camera3D_property_doppler_tracking>` | ``0``             |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`Environment<class_Environment>`                 | :ref:`environment<class_Camera3D_property_environment>`           |                   |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`far<class_Camera3D_property_far>`                           | ``4000.0``        |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`fov<class_Camera3D_property_fov>`                           | ``75.0``          |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                         | :ref:`frustum_offset<class_Camera3D_property_frustum_offset>`     | ``Vector2(0, 0)`` |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`h_offset<class_Camera3D_property_h_offset>`                 | ``0.0``           |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`KeepAspect<enum_Camera3D_KeepAspect>`           | :ref:`keep_aspect<class_Camera3D_property_keep_aspect>`           | ``1``             |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`near<class_Camera3D_property_near>`                         | ``0.05``          |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`ProjectionType<enum_Camera3D_ProjectionType>`   | :ref:`projection<class_Camera3D_property_projection>`             | ``0``             |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`size<class_Camera3D_property_size>`                         | ``1.0``           |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                             | :ref:`v_offset<class_Camera3D_property_v_offset>`                 | ``0.0``           |
   +-------------------------------------------------------+-------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`clear_current<class_Camera3D_method_clear_current>`\ (\ enable_next\: :ref:`bool<class_bool>` = true\ )                                                                                                |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Projection<class_Projection>`                    | :ref:`get_camera_projection<class_Camera3D_method_get_camera_projection>`\ (\ ) |const|                                                                                                                      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                  | :ref:`get_camera_rid<class_Camera3D_method_get_camera_rid>`\ (\ ) |const|                                                                                                                                    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`                  | :ref:`get_camera_transform<class_Camera3D_method_get_camera_transform>`\ (\ ) |const|                                                                                                                        |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                | :ref:`get_cull_mask_value<class_Camera3D_method_get_cull_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                                                    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] | :ref:`get_frustum<class_Camera3D_method_get_frustum>`\ (\ ) |const|                                                                                                                                          |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                  | :ref:`get_pyramid_shape_rid<class_Camera3D_method_get_pyramid_shape_rid>`\ (\ )                                                                                                                              |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                | :ref:`is_position_behind<class_Camera3D_method_is_position_behind>`\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                               |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                | :ref:`is_position_in_frustum<class_Camera3D_method_is_position_in_frustum>`\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                       |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`make_current<class_Camera3D_method_make_current>`\ (\ )                                                                                                                                                |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`project_local_ray_normal<class_Camera3D_method_project_local_ray_normal>`\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`project_position<class_Camera3D_method_project_position>`\ (\ screen_point\: :ref:`Vector2<class_Vector2>`, z_depth\: :ref:`float<class_float>`\ ) |const|                                             |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`project_ray_normal<class_Camera3D_method_project_ray_normal>`\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                              |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`project_ray_origin<class_Camera3D_method_project_ray_origin>`\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                              |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`set_cull_mask_value<class_Camera3D_method_set_cull_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                                           |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`set_frustum<class_Camera3D_method_set_frustum>`\ (\ size\: :ref:`float<class_float>`, offset\: :ref:`Vector2<class_Vector2>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ ) |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`set_orthogonal<class_Camera3D_method_set_orthogonal>`\ (\ size\: :ref:`float<class_float>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ )                                   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                 | :ref:`set_perspective<class_Camera3D_method_set_perspective>`\ (\ fov\: :ref:`float<class_float>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ )                                  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                          | :ref:`unproject_position<class_Camera3D_method_unproject_position>`\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                               |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Camera3D_ProjectionType:

.. rst-class:: classref-enumeration

enum **ProjectionType**: :ref:`🔗<enum_Camera3D_ProjectionType>`

.. _class_Camera3D_constant_PROJECTION_PERSPECTIVE:

.. rst-class:: classref-enumeration-constant

:ref:`ProjectionType<enum_Camera3D_ProjectionType>` **PROJECTION_PERSPECTIVE** = ``0``

Phép chiếu phối cảnh. Các đối tượng trên màn hình sẽ nhỏ hơn khi ở xa.

.. _class_Camera3D_constant_PROJECTION_ORTHOGONAL:

.. rst-class:: classref-enumeration-constant

:ref:`ProjectionType<enum_Camera3D_ProjectionType>` **PROJECTION_ORTHOGONAL** = ``1``

Phép chiếu trực giao, còn được gọi là orthographic projection. Các đối tượng giữ nguyên kích thước trên màn hình bất kể ở xa đến đâu.

.. _class_Camera3D_constant_PROJECTION_FRUSTUM:

.. rst-class:: classref-enumeration-constant

:ref:`ProjectionType<enum_Camera3D_ProjectionType>` **PROJECTION_FRUSTUM** = ``2``

Phép chiếu frustum. Chế độ này cho phép điều chỉnh :ref:`frustum_offset<class_Camera3D_property_frustum_offset>` để tạo hiệu ứng "tilted frustum".

.. rst-class:: classref-item-separator

----

.. _enum_Camera3D_KeepAspect:

.. rst-class:: classref-enumeration

enum **KeepAspect**: :ref:`🔗<enum_Camera3D_KeepAspect>`

.. _class_Camera3D_constant_KEEP_WIDTH:

.. rst-class:: classref-enumeration-constant

:ref:`KeepAspect<enum_Camera3D_KeepAspect>` **KEEP_WIDTH** = ``0``

Giữ nguyên aspect ratio theo chiều ngang; còn được gọi là scaling Vert-. Đây thường là lựa chọn tốt nhất cho các project chạy ở chế độ dọc, vì aspect ratio cao hơn sẽ được hưởng lợi từ FOV theo chiều dọc rộng hơn.

.. _class_Camera3D_constant_KEEP_HEIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`KeepAspect<enum_Camera3D_KeepAspect>` **KEEP_HEIGHT** = ``1``

Giữ nguyên aspect ratio theo chiều dọc; còn được gọi là scaling Hor+. Đây thường là lựa chọn tốt nhất cho các project chạy ở chế độ ngang, vì aspect ratio rộng hơn sẽ tự động được hưởng lợi từ FOV theo chiều ngang rộng hơn.

.. rst-class:: classref-item-separator

----

.. _enum_Camera3D_DopplerTracking:

.. rst-class:: classref-enumeration

enum **DopplerTracking**: :ref:`🔗<enum_Camera3D_DopplerTracking>`

.. _class_Camera3D_constant_DOPPLER_TRACKING_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` **DOPPLER_TRACKING_DISABLED** = ``0``

Tắt mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ (mặc định).

.. _class_Camera3D_constant_DOPPLER_TRACKING_IDLE_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` **DOPPLER_TRACKING_IDLE_STEP** = ``1``

Mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ bằng cách theo dõi vị trí của các đối tượng được thay đổi trong ``_process``. Những thay đổi về vận tốc tương đối của camera này so với các đối tượng đó sẽ ảnh hưởng đến cách cảm nhận âm thanh (làm thay đổi :ref:`AudioStreamPlayer3D.pitch_scale<class_AudioStreamPlayer3D_property_pitch_scale>` của âm thanh).

.. _class_Camera3D_constant_DOPPLER_TRACKING_PHYSICS_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` **DOPPLER_TRACKING_PHYSICS_STEP** = ``2``

Mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ bằng cách theo dõi vị trí của các đối tượng được thay đổi trong ``_physics_process``. Những thay đổi về vận tốc tương đối của camera này so với các đối tượng đó sẽ ảnh hưởng đến cách cảm nhận âm thanh (làm thay đổi :ref:`AudioStreamPlayer3D.pitch_scale<class_AudioStreamPlayer3D_property_pitch_scale>` của âm thanh).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Camera3D_property_attributes:

.. rst-class:: classref-property

:ref:`CameraAttributes<class_CameraAttributes>` **attributes** :ref:`🔗<class_Camera3D_property_attributes>`

.. rst-class:: classref-property-setget

- |void| **set_attributes**\ (\ value\: :ref:`CameraAttributes<class_CameraAttributes>`\ ) - :ref:`CameraAttributes<class_CameraAttributes>` **get_attributes**\ (\ )

:ref:`CameraAttributes<class_CameraAttributes>` sẽ được sử dụng cho camera này.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_compositor:

.. rst-class:: classref-property

:ref:`Compositor<class_Compositor>` **compositor** :ref:`🔗<class_Camera3D_property_compositor>`

.. rst-class:: classref-property-setget

- |void| **set_compositor**\ (\ value\: :ref:`Compositor<class_Compositor>`\ ) - :ref:`Compositor<class_Compositor>` **get_compositor**\ (\ )

:ref:`Compositor<class_Compositor>` sẽ được sử dụng cho camera này.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **cull_mask** = ``1048575`` :ref:`🔗<class_Camera3D_property_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_cull_mask**\ (\ )

Mặt nạ culling mô tả những :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>` nào được camera này render. Theo mặc định, tất cả 20 layer hiển thị với người dùng đều được render.

\ **Lưu ý:** Vì :ref:`cull_mask<class_Camera3D_property_cull_mask>` cho phép lưu trữ tổng cộng 32 layer, có thêm 12 layer chỉ được engine sử dụng nội bộ và không hiển thị trong editor. Đặt :ref:`cull_mask<class_Camera3D_property_cull_mask>` bằng script cho phép bạn bật/tắt các layer dành riêng đó, điều này có thể hữu ích cho các editor plugin.

Để điều chỉnh :ref:`cull_mask<class_Camera3D_property_cull_mask>` dễ dàng hơn bằng script, hãy sử dụng :ref:`get_cull_mask_value()<class_Camera3D_method_get_cull_mask_value>` và :ref:`set_cull_mask_value()<class_Camera3D_method_set_cull_mask_value>`.

\ **Lưu ý:** :ref:`VoxelGI<class_VoxelGI>`, SDFGI và :ref:`LightmapGI<class_LightmapGI>` sẽ luôn tính đến tất cả layer để xác định những gì đóng góp vào global illumination. Nếu đây là vấn đề, hãy đặt :ref:`GeometryInstance3D.gi_mode<class_GeometryInstance3D_property_gi_mode>` thành :ref:`GeometryInstance3D.GI_MODE_DISABLED<class_GeometryInstance3D_constant_GI_MODE_DISABLED>` cho mesh và :ref:`Light3D.light_bake_mode<class_Light3D_property_light_bake_mode>` thành :ref:`Light3D.BAKE_DISABLED<class_Light3D_constant_BAKE_DISABLED>` cho light để loại trừ chúng khỏi global illumination.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_current:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **current** = ``false`` :ref:`🔗<class_Camera3D_property_current>`

.. rst-class:: classref-property-setget

- |void| **set_current**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_current**\ (\ )

Nếu ``true``, ancestor :ref:`Viewport<class_Viewport>` hiện đang sử dụng camera này.

Nếu scene có nhiều camera, một camera sẽ luôn được đặt làm camera hiện tại. Ví dụ: nếu scene có hai node **Camera3D** và chỉ một node đang là camera hiện tại, việc đặt :ref:`current<class_Camera3D_property_current>` của một camera thành ``false`` sẽ khiến camera còn lại được đặt làm camera hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_doppler_tracking:

.. rst-class:: classref-property

:ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` **doppler_tracking** = ``0`` :ref:`🔗<class_Camera3D_property_doppler_tracking>`

.. rst-class:: classref-property-setget

- |void| **set_doppler_tracking**\ (\ value\: :ref:`DopplerTracking<enum_Camera3D_DopplerTracking>`\ ) - :ref:`DopplerTracking<enum_Camera3D_DopplerTracking>` **get_doppler_tracking**\ (\ )

Nếu không phải :ref:`DOPPLER_TRACKING_DISABLED<class_Camera3D_constant_DOPPLER_TRACKING_DISABLED>`, camera này sẽ mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ cho các đối tượng được thay đổi trong các phương thức ``_process`` cụ thể.

\ **Note:** The Doppler effect will only be heard on :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>`\ s if :ref:`AudioStreamPlayer3D.doppler_tracking<class_AudioStreamPlayer3D_property_doppler_tracking>` is not set to :ref:`AudioStreamPlayer3D.DOPPLER_TRACKING_DISABLED<class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_DISABLED>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_environment:

.. rst-class:: classref-property

:ref:`Environment<class_Environment>` **environment** :ref:`🔗<class_Camera3D_property_environment>`

.. rst-class:: classref-property-setget

- |void| **set_environment**\ (\ value\: :ref:`Environment<class_Environment>`\ ) - :ref:`Environment<class_Environment>` **get_environment**\ (\ )

:ref:`Environment<class_Environment>` sẽ được sử dụng cho camera này.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_far:

.. rst-class:: classref-property

:ref:`float<class_float>` **far** = ``4000.0`` :ref:`🔗<class_Camera3D_property_far>`

.. rst-class:: classref-property-setget

- |void| **set_far**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_far**\ (\ )

Khoảng cách đến ranh giới culling xa của camera này, tính theo trục Z cục bộ của nó. Giá trị cao hơn cho phép camera nhìn xa hơn, trong khi giảm :ref:`far<class_Camera3D_property_far>` có thể cải thiện hiệu năng nếu khiến các đối tượng bị cull một phần hoặc hoàn toàn.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_fov:

.. rst-class:: classref-property

:ref:`float<class_float>` **fov** = ``75.0`` :ref:`🔗<class_Camera3D_property_fov>`

.. rst-class:: classref-property-setget

- |void| **set_fov**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fov**\ (\ )

Góc field of view của camera (tính bằng độ). Chỉ áp dụng ở chế độ phối cảnh. Vì :ref:`keep_aspect<class_Camera3D_property_keep_aspect>` khóa một trục, :ref:`fov<class_Camera3D_property_fov>` đặt góc field of view của trục còn lại.

Để tham khảo, giá trị field of view theo chiều dọc mặc định (``75.0``) tương đương với FOV theo chiều ngang là:

- ~91.31 độ trong viewport 4:3

- ~101.67 độ trong viewport 16:10

- ~107.51 độ trong viewport 16:9

- ~121.63 độ trong viewport 21:9

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_frustum_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **frustum_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Camera3D_property_frustum_offset>`

.. rst-class:: classref-property-setget

- |void| **set_frustum_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_frustum_offset**\ (\ )

Độ lệch frustum của camera. Có thể thay đổi giá trị này từ mặc định để tạo các hiệu ứng "tilted frustum" như `Y-shearing <https://zdoom.org/wiki/Y-shearing>`__.

\ **Lưu ý:** Chỉ có hiệu lực nếu :ref:`projection<class_Camera3D_property_projection>` là :ref:`PROJECTION_FRUSTUM<class_Camera3D_constant_PROJECTION_FRUSTUM>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_h_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **h_offset** = ``0.0`` :ref:`🔗<class_Camera3D_property_h_offset>`

.. rst-class:: classref-property-setget

- |void| **set_h_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_h_offset**\ (\ )

Độ lệch ngang (X) của viewport camera.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_keep_aspect:

.. rst-class:: classref-property

:ref:`KeepAspect<enum_Camera3D_KeepAspect>` **keep_aspect** = ``1`` :ref:`🔗<class_Camera3D_property_keep_aspect>`

.. rst-class:: classref-property-setget

- |void| **set_keep_aspect_mode**\ (\ value\: :ref:`KeepAspect<enum_Camera3D_KeepAspect>`\ ) - :ref:`KeepAspect<enum_Camera3D_KeepAspect>` **get_keep_aspect_mode**\ (\ )

The axis to lock during :ref:`fov<class_Camera3D_property_fov>`/:ref:`size<class_Camera3D_property_size>` adjustments. Can be either :ref:`KEEP_WIDTH<class_Camera3D_constant_KEEP_WIDTH>` or :ref:`KEEP_HEIGHT<class_Camera3D_constant_KEEP_HEIGHT>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_near:

.. rst-class:: classref-property

:ref:`float<class_float>` **near** = ``0.05`` :ref:`🔗<class_Camera3D_property_near>`

.. rst-class:: classref-property-setget

- |void| **set_near**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_near**\ (\ )

Khoảng cách đến ranh giới culling gần của camera này, tính theo trục Z cục bộ của nó. Giá trị thấp hơn cho phép camera nhìn các đối tượng gần gốc của nó hơn, nhưng phải đánh đổi bằng độ chính xác thấp hơn trên *toàn bộ* phạm vi. Các giá trị thấp hơn mặc định có thể dẫn đến hiện tượng Z-fighting gia tăng.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_projection:

.. rst-class:: classref-property

:ref:`ProjectionType<enum_Camera3D_ProjectionType>` **projection** = ``0`` :ref:`🔗<class_Camera3D_property_projection>`

.. rst-class:: classref-property-setget

- |void| **set_projection**\ (\ value\: :ref:`ProjectionType<enum_Camera3D_ProjectionType>`\ ) - :ref:`ProjectionType<enum_Camera3D_ProjectionType>` **get_projection**\ (\ )

Chế độ projection của camera. Ở chế độ :ref:`PROJECTION_PERSPECTIVE<class_Camera3D_constant_PROJECTION_PERSPECTIVE>`, khoảng cách Z của các đối tượng so với không gian cục bộ của camera sẽ làm thay đổi kích thước cảm nhận được của chúng.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **size** = ``1.0`` :ref:`🔗<class_Camera3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_size**\ (\ )

Kích thước của camera tính bằng mét, được đo dưới dạng đường kính của chiều rộng hoặc chiều cao, tùy thuộc vào :ref:`keep_aspect<class_Camera3D_property_keep_aspect>`. Chỉ áp dụng ở chế độ trực giao và frustum.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_property_v_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **v_offset** = ``0.0`` :ref:`🔗<class_Camera3D_property_v_offset>`

.. rst-class:: classref-property-setget

- |void| **set_v_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_v_offset**\ (\ )

Độ lệch dọc (Y) của viewport camera.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Camera3D_method_clear_current:

.. rst-class:: classref-method

|void| **clear_current**\ (\ enable_next\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_Camera3D_method_clear_current>`

Nếu đây là camera hiện tại, hãy xóa camera này khỏi trạng thái hiện tại. Nếu ``enable_next`` là ``true``, yêu cầu đặt camera tiếp theo làm camera hiện tại, nếu có.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_camera_projection:

.. rst-class:: classref-method

:ref:`Projection<class_Projection>` **get_camera_projection**\ (\ ) |const| :ref:`🔗<class_Camera3D_method_get_camera_projection>`

Trả về ma trận projection mà camera này sử dụng để render vào viewport liên kết với nó. Camera phải là một phần của scene tree để hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_camera_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_camera_rid**\ (\ ) |const| :ref:`🔗<class_Camera3D_method_get_camera_rid>`

Trả về RID của camera từ :ref:`RenderingServer<class_RenderingServer>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_camera_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **get_camera_transform**\ (\ ) |const| :ref:`🔗<class_Camera3D_method_get_camera_transform>`

Trả về transform của camera cộng với các độ lệch dọc (:ref:`v_offset<class_Camera3D_property_v_offset>`) và ngang (:ref:`h_offset<class_Camera3D_property_h_offset>`); cùng mọi điều chỉnh khác đối với vị trí và hướng của camera do các camera lớp con như :ref:`XRCamera3D<class_XRCamera3D>` thực hiện.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_cull_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_cull_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Camera3D_method_get_cull_mask_value>`

Trả về việc lớp được chỉ định của :ref:`cull_mask<class_Camera3D_property_cull_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 20.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_frustum:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] **get_frustum**\ (\ ) |const| :ref:`🔗<class_Camera3D_method_get_frustum>`

Returns the camera's frustum planes in world space units as an array of :ref:`Plane<class_Plane>`\ s in the following order: near, far, left, top, right, bottom. Not to be confused with :ref:`frustum_offset<class_Camera3D_property_frustum_offset>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_get_pyramid_shape_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_pyramid_shape_rid**\ (\ ) :ref:`🔗<class_Camera3D_method_get_pyramid_shape_rid>`

Trả về RID của một hình chóp bao quanh frustum chế độ xem của camera, bỏ qua mặt phẳng near của camera. Đỉnh của hình chóp biểu thị vị trí của camera.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_is_position_behind:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_position_behind**\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Camera3D_method_is_position_behind>`

Trả về ``true`` nếu vị trí đã cho nằm phía sau camera (phần màu xanh dương của sơ đồ được liên kết). `See this diagram <https://raw.githubusercontent.com/godotengine/godot-docs/master/img/camera3d_position_frustum.png>`__ để xem tổng quan về các phương thức truy vấn vị trí.

\ **Lưu ý:** Một vị trí trả về ``false`` vẫn có thể nằm ngoài trường nhìn của camera.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_is_position_in_frustum:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_position_in_frustum**\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Camera3D_method_is_position_in_frustum>`

Trả về ``true`` nếu vị trí đã cho nằm trong frustum của camera (phần màu xanh lá cây của sơ đồ được liên kết). `See this diagram <https://raw.githubusercontent.com/godotengine/godot-docs/master/img/camera3d_position_frustum.png>`__ để xem tổng quan về các phương thức truy vấn vị trí.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_make_current:

.. rst-class:: classref-method

|void| **make_current**\ (\ ) :ref:`🔗<class_Camera3D_method_make_current>`

Đặt camera này làm camera hiện tại cho :ref:`Viewport<class_Viewport>` (xem phần mô tả lớp). Nếu node camera nằm ngoài scene tree, nó sẽ cố gắng trở thành camera hiện tại ngay khi được thêm vào.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_project_local_ray_normal:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **project_local_ray_normal**\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Camera3D_method_project_local_ray_normal>`

Trả về một vector pháp tuyến từ vị trí điểm trên màn hình, hướng dọc theo camera. Các camera orthogonal được chuẩn hóa. Các camera perspective tính đến phối cảnh, chiều rộng/chiều cao màn hình, v.v.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_project_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **project_position**\ (\ screen_point\: :ref:`Vector2<class_Vector2>`, z_depth\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Camera3D_method_project_position>`

Trả về điểm 3D trong world space ánh xạ tới tọa độ 2D đã cho trong hình chữ nhật :ref:`Viewport<class_Viewport>` trên một mặt phẳng cách camera một khoảng ``z_depth`` đã cho theo hướng vào scene.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_project_ray_normal:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **project_ray_normal**\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Camera3D_method_project_ray_normal>`

Trả về một vector pháp tuyến trong world space, là kết quả của việc chiếu một điểm trên hình chữ nhật :ref:`Viewport<class_Viewport>` bằng phép chiếu ngược của camera. Điều này hữu ích khi tạo các tia dưới dạng (origin, normal) để giao cắt với đối tượng hoặc picking.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_project_ray_origin:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **project_ray_origin**\ (\ screen_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Camera3D_method_project_ray_origin>`

Trả về một vị trí 3D trong world space, là kết quả của việc chiếu một điểm trên hình chữ nhật :ref:`Viewport<class_Viewport>` bằng phép chiếu ngược của camera. Điều này hữu ích khi tạo các tia dưới dạng (origin, normal) để giao cắt với đối tượng hoặc picking.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_set_cull_mask_value:

.. rst-class:: classref-method

|void| **set_cull_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Camera3D_method_set_cull_mask_value>`

Dựa trên ``value``, bật hoặc tắt lớp được chỉ định trong :ref:`cull_mask<class_Camera3D_property_cull_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 20.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_set_frustum:

.. rst-class:: classref-method

|void| **set_frustum**\ (\ size\: :ref:`float<class_float>`, offset\: :ref:`Vector2<class_Vector2>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Camera3D_method_set_frustum>`

Đặt phép chiếu của camera sang chế độ frustum (xem :ref:`PROJECTION_FRUSTUM<class_Camera3D_constant_PROJECTION_FRUSTUM>`) bằng cách chỉ định một ``size``, một ``offset``, cùng các mặt phẳng cắt ``z_near`` và ``z_far`` theo đơn vị world space. Tham số ``size`` biểu thị kích thước của mặt phẳng near, có thể là chiều rộng hoặc chiều cao tùy thuộc vào giá trị của :ref:`keep_aspect<class_Camera3D_property_keep_aspect>`. Xem thêm :ref:`frustum_offset<class_Camera3D_property_frustum_offset>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_set_orthogonal:

.. rst-class:: classref-method

|void| **set_orthogonal**\ (\ size\: :ref:`float<class_float>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Camera3D_method_set_orthogonal>`

Đặt phép chiếu của camera sang chế độ orthogonal (xem :ref:`PROJECTION_ORTHOGONAL<class_Camera3D_constant_PROJECTION_ORTHOGONAL>`) bằng cách chỉ định một ``size``, cùng các mặt phẳng cắt ``z_near`` và ``z_far`` theo đơn vị world space.

Gợi ý: các game 3D có giao diện trông như 2D thường sử dụng phép chiếu này, với ``size`` được chỉ định theo pixel.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_set_perspective:

.. rst-class:: classref-method

|void| **set_perspective**\ (\ fov\: :ref:`float<class_float>`, z_near\: :ref:`float<class_float>`, z_far\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Camera3D_method_set_perspective>`

Đặt phép chiếu của camera sang chế độ perspective (xem :ref:`PROJECTION_PERSPECTIVE<class_Camera3D_constant_PROJECTION_PERSPECTIVE>`) bằng cách chỉ định góc ``fov`` (field of view) theo độ, cùng các mặt phẳng cắt ``z_near`` và ``z_far`` theo đơn vị world space.

.. rst-class:: classref-item-separator

----

.. _class_Camera3D_method_unproject_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **unproject_position**\ (\ world_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Camera3D_method_unproject_position>`

Trả về tọa độ 2D trong hình chữ nhật :ref:`Viewport<class_Viewport>` ánh xạ tới điểm 3D đã cho trong world space.

\ **Lưu ý:** Khi sử dụng cách này để đặt các phần tử GUI lên trên viewport 3D, hãy sử dụng :ref:`is_position_behind()<class_Camera3D_method_is_position_behind>` để ngăn chúng xuất hiện nếu điểm 3D nằm phía sau camera:

::

    # Khối mã này là một phần của script kế thừa từ Node3D.
    # `control` là một tham chiếu đến một node kế thừa từ Control.
    control.visible = not get_viewport().get_camera_3d().is_position_behind(global_transform.origin)
    control.position = get_viewport().get_camera_3d().unproject_position(global_transform.origin)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
