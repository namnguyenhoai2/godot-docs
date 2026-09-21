:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorNode3DGizmoPlugin.xml.

.. _class_EditorNode3DGizmoPlugin:

EditorNode3DGizmoPlugin
=======================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một class được editor sử dụng để định nghĩa các loại gizmo của Node3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorNode3DGizmoPlugin** cho phép bạn định nghĩa một loại Gizmo mới. Có hai cách chính để thực hiện việc này: mở rộng **EditorNode3DGizmoPlugin** để tạo các gizmo đơn giản hơn, hoặc tạo một loại :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` mới. Xem tutorial trong tài liệu để biết thêm thông tin.

Để sử dụng **EditorNode3DGizmoPlugin**, trước tiên hãy đăng ký nó bằng phương thức :ref:`EditorPlugin.add_node_3d_gizmo_plugin()<class_EditorPlugin_method_add_node_3d_gizmo_plugin>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Plugin gizmo của Node3D <../tutorials/plugins/editor/3d_gizmos>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_begin_handle_action<class_EditorNode3DGizmoPlugin_private_method__begin_handle_action>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_can_be_hidden<class_EditorNode3DGizmoPlugin_private_method__can_be_hidden>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                  |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_can_commit_handle_on_click<class_EditorNode3DGizmoPlugin_private_method__can_commit_handle_on_click>`\ (\ ) |virtual| |const|                                                                                                                                                                                                        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_commit_handle<class_EditorNode3DGizmoPlugin_private_method__commit_handle>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, restore\: :ref:`Variant<class_Variant>`, cancel\: :ref:`bool<class_bool>`\ ) |virtual|                            |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_commit_subgizmos<class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, restores\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], cancel\: :ref:`bool<class_bool>`\ ) |virtual| |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`   | :ref:`_create_gizmo<class_EditorNode3DGizmoPlugin_private_method__create_gizmo>`\ (\ for_node_3d\: :ref:`Node3D<class_Node3D>`\ ) |virtual| |const|                                                                                                                                                                                         |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                         | :ref:`_get_gizmo_name<class_EditorNode3DGizmoPlugin_private_method__get_gizmo_name>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                         | :ref:`_get_handle_name<class_EditorNode3DGizmoPlugin_private_method__get_handle_name>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                       | :ref:`_get_handle_value<class_EditorNode3DGizmoPlugin_private_method__get_handle_value>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                                         |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`_get_priority<class_EditorNode3DGizmoPlugin_private_method__get_priority>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                    |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`               | :ref:`_get_subgizmo_transform<class_EditorNode3DGizmoPlugin_private_method__get_subgizmo_transform>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, subgizmo_id\: :ref:`int<class_int>`\ ) |virtual| |const|                                                                                                                |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_has_gizmo<class_EditorNode3DGizmoPlugin_private_method__has_gizmo>`\ (\ for_node_3d\: :ref:`Node3D<class_Node3D>`\ ) |virtual| |const|                                                                                                                                                                                               |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_is_handle_highlighted<class_EditorNode3DGizmoPlugin_private_method__is_handle_highlighted>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                               |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_is_selectable_when_hidden<class_EditorNode3DGizmoPlugin_private_method__is_selectable_when_hidden>`\ (\ ) |virtual| |const|                                                                                                                                                                                                          |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_redraw<class_EditorNode3DGizmoPlugin_private_method__redraw>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`\ ) |virtual|                                                                                                                                                                                             |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_set_handle<class_EditorNode3DGizmoPlugin_private_method__set_handle>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, camera\: :ref:`Camera3D<class_Camera3D>`, screen_pos\: :ref:`Vector2<class_Vector2>`\ ) |virtual|                       |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`_set_subgizmo_transform<class_EditorNode3DGizmoPlugin_private_method__set_subgizmo_transform>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, subgizmo_id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) |virtual|                                                                     |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`_subgizmos_intersect_frustum<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_frustum>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, camera\: :ref:`Camera3D<class_Camera3D>`, frustum_planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) |virtual| |const|                        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`_subgizmos_intersect_ray<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_ray>`\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, camera\: :ref:`Camera3D<class_Camera3D>`, screen_pos\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                             |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_material<class_EditorNode3DGizmoPlugin_method_add_material>`\ (\ name\: :ref:`String<class_String>`, material\: :ref:`StandardMaterial3D<class_StandardMaterial3D>`\ )                                                                                                                                                            |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`create_handle_material<class_EditorNode3DGizmoPlugin_method_create_handle_material>`\ (\ name\: :ref:`String<class_String>`, billboard\: :ref:`bool<class_bool>` = false, texture\: :ref:`Texture2D<class_Texture2D>` = null\ )                                                                                                       |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`create_icon_material<class_EditorNode3DGizmoPlugin_method_create_icon_material>`\ (\ name\: :ref:`String<class_String>`, texture\: :ref:`Texture2D<class_Texture2D>`, on_top\: :ref:`bool<class_bool>` = false, color\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ )                                                              |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`create_material<class_EditorNode3DGizmoPlugin_method_create_material>`\ (\ name\: :ref:`String<class_String>`, color\: :ref:`Color<class_Color>`, billboard\: :ref:`bool<class_bool>` = false, on_top\: :ref:`bool<class_bool>` = false, use_vertex_color\: :ref:`bool<class_bool>` = false\ )                                        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StandardMaterial3D<class_StandardMaterial3D>` | :ref:`get_material<class_EditorNode3DGizmoPlugin_method_get_material>`\ (\ name\: :ref:`String<class_String>`, gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` = null\ )                                                                                                                                                          |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorNode3DGizmoPlugin_private_method__begin_handle_action:

.. rst-class:: classref-method

|void| **_begin_handle_action**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__begin_handle_action>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__can_be_hidden:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_be_hidden**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__can_be_hidden>`

Ghi đè phương thức này để xác định liệu các gizmo do plugin này xử lý có thể bị ẩn hay không. Trả về ``true`` nếu không được ghi đè.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__can_commit_handle_on_click:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_commit_handle_on_click**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__can_commit_handle_on_click>`

Ghi đè phương thức này để xác định liệu các gizmo có nên được commit khi vị trí handle cuối cùng giống với vị trí ban đầu hay không. Trả về ``false`` nếu không được ghi đè.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__commit_handle:

.. rst-class:: classref-method

|void| **_commit_handle**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, restore\: :ref:`Variant<class_Variant>`, cancel\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__commit_handle>`

Ghi đè phương thức này để commit một handle đang được chỉnh sửa (các handle trước đó phải được thêm bằng :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` trong :ref:`_redraw()<class_EditorNode3DGizmoPlugin_private_method__redraw>`). Điều này thường có nghĩa là tạo một action :ref:`UndoRedo<class_UndoRedo>` cho thay đổi, sử dụng giá trị handle hiện tại làm "do" và đối số ``restore`` làm "undo".

Nếu đối số ``cancel`` là ``true``, giá trị ``restore`` phải được thiết lập trực tiếp, không sử dụng action :ref:`UndoRedo<class_UndoRedo>`.

Đối số ``secondary`` là ``true`` khi handle được commit là handle phụ (xem :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos:

.. rst-class:: classref-method

|void| **_commit_subgizmos**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, restores\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], cancel\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos>`

Ghi đè phương thức này để commit một nhóm subgizmo đang được chỉnh sửa (xem :ref:`_subgizmos_intersect_ray()<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_ray>` và :ref:`_subgizmos_intersect_frustum()<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_frustum>`). Điều này thường có nghĩa là tạo một action :ref:`UndoRedo<class_UndoRedo>` cho thay đổi, sử dụng các transform hiện tại làm "do" và các transform ``restores`` làm "undo".

Nếu đối số ``cancel`` là ``true``, các transform ``restores`` phải được thiết lập trực tiếp, không sử dụng action :ref:`UndoRedo<class_UndoRedo>`. Như với mọi phương thức subgizmo, các transform được cung cấp trong local space đối với Node3D của gizmo. Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__create_gizmo:

.. rst-class:: classref-method

:ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` **_create_gizmo**\ (\ for_node_3d\: :ref:`Node3D<class_Node3D>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__create_gizmo>`

Ghi đè phương thức này để trả về một :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` tùy chỉnh cho các node 3D mà bạn chọn; trả về ``null`` cho các node còn lại. Xem thêm :ref:`_has_gizmo()<class_EditorNode3DGizmoPlugin_private_method__has_gizmo>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__get_gizmo_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_gizmo_name**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__get_gizmo_name>`

Ghi đè phương thức này để cung cấp tên sẽ xuất hiện trong menu hiển thị gizmo.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__get_handle_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_handle_name**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__get_handle_name>`

Ghi đè phương thức này để cung cấp tên cho các handle của gizmo. Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin). Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__get_handle_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_handle_value**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__get_handle_value>`

Ghi đè phương thức này để trả về giá trị hiện tại của một handle. Giá trị này sẽ được yêu cầu khi bắt đầu chỉnh sửa và được sử dụng làm đối số ``restore`` trong :ref:`_commit_handle()<class_EditorNode3DGizmoPlugin_private_method__commit_handle>`.

Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__get_priority:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_priority**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__get_priority>`

Ghi đè phương thức này để đặt mức độ ưu tiên của gizmo. Các gizmo có mức độ ưu tiên cao hơn sẽ được ưu tiên khi xử lý các input như chọn handle hoặc subgizmo.

Tất cả gizmo editor tích hợp đều trả về mức độ ưu tiên ``-1``. Nếu không được ghi đè, phương thức này sẽ trả về ``0``, nghĩa là các gizmo tùy chỉnh sẽ tự động có mức độ ưu tiên cao hơn các gizmo tích hợp.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__get_subgizmo_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **_get_subgizmo_transform**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, subgizmo_id\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__get_subgizmo_transform>`

Ghi đè phương thức này để trả về transform hiện tại của một subgizmo. Như với mọi phương thức subgizmo, transform phải ở local space đối với Node3D của gizmo. Transform này sẽ được yêu cầu khi bắt đầu chỉnh sửa và được sử dụng trong đối số ``restore`` của :ref:`_commit_subgizmos()<class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos>`. Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__has_gizmo:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_has_gizmo**\ (\ for_node_3d\: :ref:`Node3D<class_Node3D>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__has_gizmo>`

Ghi đè phương thức này để xác định những node Node3D nào có gizmo từ plugin này. Mỗi khi một node :ref:`Node3D<class_Node3D>` được thêm vào scene, phương thức này sẽ được gọi; nếu trả về ``true``, node sẽ được gán một :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` chung và được thêm vào danh sách các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__is_handle_highlighted:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_handle_highlighted**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__is_handle_highlighted>`

Ghi đè phương thức này để trả về ``true`` bất cứ khi nào handle được cung cấp cần được highlight trong editor. Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin). Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__is_selectable_when_hidden:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_selectable_when_hidden**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__is_selectable_when_hidden>`

Ghi đè phương thức này để xác định liệu Node3D có gizmo này có thể được chọn ngay cả khi gizmo bị ẩn hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__redraw:

.. rst-class:: classref-method

|void| **_redraw**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__redraw>`

Ghi đè phương thức này để thêm tất cả phần tử gizmo mỗi khi yêu cầu cập nhật gizmo. Thông thường, bạn sẽ gọi :ref:`EditorNode3DGizmo.clear()<class_EditorNode3DGizmo_method_clear>` ở đầu phương thức này, sau đó thêm các phần tử trực quan tùy thuộc vào thuộc tính của node.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__set_handle:

.. rst-class:: classref-method

|void| **_set_handle**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, handle_id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, camera\: :ref:`Camera3D<class_Camera3D>`, screen_pos\: :ref:`Vector2<class_Vector2>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__set_handle>`

Ghi đè phương thức này để cập nhật các thuộc tính của node khi người dùng kéo một handle của gizmo (đã được thêm trước đó bằng :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>`). ``screen_pos`` được cung cấp là vị trí chuột trong tọa độ màn hình và ``camera`` có thể được sử dụng để chuyển đổi nó thành raycast.

Đối số ``secondary`` là ``true`` khi handle đang được chỉnh sửa là handle phụ (xem :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__set_subgizmo_transform:

.. rst-class:: classref-method

|void| **_set_subgizmo_transform**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, subgizmo_id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__set_subgizmo_transform>`

Ghi đè phương thức này để cập nhật các thuộc tính của node trong khi chỉnh sửa subgizmo (xem :ref:`_subgizmos_intersect_ray()<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_ray>` và :ref:`_subgizmos_intersect_frustum()<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_frustum>`). ``transform`` được cung cấp trong hệ tọa độ cục bộ của Node3D. Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_frustum:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **_subgizmos_intersect_frustum**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, camera\: :ref:`Camera3D<class_Camera3D>`, frustum_planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_frustum>`

Ghi đè phương thức này để cho phép chọn các subgizmo bằng cách kéo hộp chọn bằng chuột. Với một ``camera`` và ``frustum_planes``, phương thức này sẽ trả về các subgizmo nằm trong các frustum. Đối số ``frustum_planes`` bao gồm một mảng chứa tất cả các :ref:`Plane<class_Plane>`\ s tạo nên frustum chọn. Giá trị trả về phải chứa danh sách các mã định danh subgizmo duy nhất; các mã định danh này có thể là bất kỳ giá trị không âm nào và sẽ được sử dụng trong các phương thức virtual khác như :ref:`_get_subgizmo_transform()<class_EditorNode3DGizmoPlugin_private_method__get_subgizmo_transform>` hoặc :ref:`_commit_subgizmos()<class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos>`. Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_ray:

.. rst-class:: classref-method

:ref:`int<class_int>` **_subgizmos_intersect_ray**\ (\ gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, camera\: :ref:`Camera3D<class_Camera3D>`, screen_pos\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmoPlugin_private_method__subgizmos_intersect_ray>`

Ghi đè phương thức này để cho phép chọn các subgizmo bằng thao tác nhấp chuột. Với một ``camera`` và ``screen_pos`` trong tọa độ màn hình, phương thức này sẽ trả về subgizmo cần được chọn. Giá trị trả về phải là một mã định danh subgizmo duy nhất, có thể là bất kỳ giá trị không âm nào và sẽ được sử dụng trong các phương thức virtual khác như :ref:`_get_subgizmo_transform()<class_EditorNode3DGizmoPlugin_private_method__get_subgizmo_transform>` hoặc :ref:`_commit_subgizmos()<class_EditorNode3DGizmoPlugin_private_method__commit_subgizmos>`. Được gọi cho các gizmo đang hoạt động của plugin này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_method_add_material:

.. rst-class:: classref-method

|void| **add_material**\ (\ name\: :ref:`String<class_String>`, material\: :ref:`StandardMaterial3D<class_StandardMaterial3D>`\ ) :ref:`🔗<class_EditorNode3DGizmoPlugin_method_add_material>`

Thêm một material mới vào danh sách material nội bộ của plugin. Sau đó, material này có thể được truy cập bằng :ref:`get_material()<class_EditorNode3DGizmoPlugin_method_get_material>`. Không nên ghi đè phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_method_create_handle_material:

.. rst-class:: classref-method

|void| **create_handle_material**\ (\ name\: :ref:`String<class_String>`, billboard\: :ref:`bool<class_bool>` = false, texture\: :ref:`Texture2D<class_Texture2D>` = null\ ) :ref:`🔗<class_EditorNode3DGizmoPlugin_method_create_handle_material>`

Tạo một material handle cùng các biến thể của nó (đã chọn và/hoặc có thể chỉnh sửa), rồi thêm chúng vào danh sách material nội bộ. Sau đó, chúng có thể được truy cập bằng :ref:`get_material()<class_EditorNode3DGizmoPlugin_method_get_material>` và sử dụng trong :ref:`EditorNode3DGizmo.add_handles()<class_EditorNode3DGizmo_method_add_handles>`. Không nên ghi đè phương thức này.

Bạn có thể tùy chọn cung cấp một texture để sử dụng thay cho biểu tượng mặc định.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_method_create_icon_material:

.. rst-class:: classref-method

|void| **create_icon_material**\ (\ name\: :ref:`String<class_String>`, texture\: :ref:`Texture2D<class_Texture2D>`, on_top\: :ref:`bool<class_bool>` = false, color\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ ) :ref:`🔗<class_EditorNode3DGizmoPlugin_method_create_icon_material>`

Tạo một icon material cùng các biến thể của nó (đã chọn và/hoặc có thể chỉnh sửa), rồi thêm chúng vào danh sách material nội bộ. Sau đó, chúng có thể được truy cập bằng :ref:`get_material()<class_EditorNode3DGizmoPlugin_method_get_material>` và sử dụng trong :ref:`EditorNode3DGizmo.add_unscaled_billboard()<class_EditorNode3DGizmo_method_add_unscaled_billboard>`. Không nên ghi đè phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_method_create_material:

.. rst-class:: classref-method

|void| **create_material**\ (\ name\: :ref:`String<class_String>`, color\: :ref:`Color<class_Color>`, billboard\: :ref:`bool<class_bool>` = false, on_top\: :ref:`bool<class_bool>` = false, use_vertex_color\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_EditorNode3DGizmoPlugin_method_create_material>`

Tạo một material không được tô bóng cùng các biến thể của nó (đã chọn và/hoặc có thể chỉnh sửa), rồi thêm chúng vào danh sách material nội bộ. Sau đó, chúng có thể được truy cập bằng :ref:`get_material()<class_EditorNode3DGizmoPlugin_method_get_material>` và sử dụng trong :ref:`EditorNode3DGizmo.add_mesh()<class_EditorNode3DGizmo_method_add_mesh>` và :ref:`EditorNode3DGizmo.add_lines()<class_EditorNode3DGizmo_method_add_lines>`. Không nên ghi đè phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmoPlugin_method_get_material:

.. rst-class:: classref-method

:ref:`StandardMaterial3D<class_StandardMaterial3D>` **get_material**\ (\ name\: :ref:`String<class_String>`, gizmo\: :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` = null\ ) :ref:`🔗<class_EditorNode3DGizmoPlugin_method_get_material>`

Lấy material từ danh sách material nội bộ. Nếu cung cấp một :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, phương thức sẽ cố lấy biến thể tương ứng (đã chọn và/hoặc có thể chỉnh sửa).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
