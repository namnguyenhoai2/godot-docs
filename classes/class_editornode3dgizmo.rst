:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorNode3DGizmo.xml.

.. _class_EditorNode3DGizmo:

EditorNode3DGizmo
=================

**Kế thừa:** :ref:`Node3DGizmo<class_Node3DGizmo>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Gizmo để chỉnh sửa các đối tượng :ref:`Node3D<class_Node3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Gizmo được sử dụng để cung cấp chức năng trực quan hóa và chỉnh sửa tùy chỉnh (các handle và subgizmo) cho các đối tượng :ref:`Node3D<class_Node3D>`. Có thể ghi đè để tạo gizmo tùy chỉnh, nhưng đối với các gizmo đơn giản, thông thường nên tạo một :ref:`EditorNode3DGizmoPlugin<class_EditorNode3DGizmoPlugin>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_begin_handle_action<class_EditorNode3DGizmo_private_method__begin_handle_action>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                                                                                        |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_commit_handle<class_EditorNode3DGizmo_private_method__commit_handle>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, restore\: :ref:`Variant<class_Variant>`, cancel\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                         |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_commit_subgizmos<class_EditorNode3DGizmo_private_method__commit_subgizmos>`\ (\ ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, restores\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], cancel\: :ref:`bool<class_bool>`\ ) |virtual|                                                       |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                   | :ref:`_get_handle_name<class_EditorNode3DGizmo_private_method__get_handle_name>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                                                                                                        |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                 | :ref:`_get_handle_value<class_EditorNode3DGizmo_private_method__get_handle_value>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                                                                                                      |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`                         | :ref:`_get_subgizmo_transform<class_EditorNode3DGizmo_private_method__get_subgizmo_transform>`\ (\ id\: :ref:`int<class_int>`\ ) |virtual| |const|                                                                                                                                                                               |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                       | :ref:`_is_handle_highlighted<class_EditorNode3DGizmo_private_method__is_handle_highlighted>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                                                                                                            |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_redraw<class_EditorNode3DGizmo_private_method__redraw>`\ (\ ) |virtual|                                                                                                                                                                                                                                                   |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_set_handle<class_EditorNode3DGizmo_private_method__set_handle>`\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, camera\: :ref:`Camera3D<class_Camera3D>`, point\: :ref:`Vector2<class_Vector2>`\ ) |virtual|                                                                                         |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`_set_subgizmo_transform<class_EditorNode3DGizmo_private_method__set_subgizmo_transform>`\ (\ id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) |virtual|                                                                                                                                    |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`               | :ref:`_subgizmos_intersect_frustum<class_EditorNode3DGizmo_private_method__subgizmos_intersect_frustum>`\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, frustum\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) |virtual| |const|                                                                                     |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                         | :ref:`_subgizmos_intersect_ray<class_EditorNode3DGizmo_private_method__subgizmos_intersect_ray>`\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, point\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                                                                                        |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_collision_segments<class_EditorNode3DGizmo_method_add_collision_segments>`\ (\ segments\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ )                                                                                                                                                                       |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_collision_triangles<class_EditorNode3DGizmo_method_add_collision_triangles>`\ (\ triangles\: :ref:`TriangleMesh<class_TriangleMesh>`\ )                                                                                                                                                                                |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_handles<class_EditorNode3DGizmo_method_add_handles>`\ (\ handles\: :ref:`PackedVector3Array<class_PackedVector3Array>`, material\: :ref:`Material<class_Material>`, ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, billboard\: :ref:`bool<class_bool>` = false, secondary\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_lines<class_EditorNode3DGizmo_method_add_lines>`\ (\ lines\: :ref:`PackedVector3Array<class_PackedVector3Array>`, material\: :ref:`Material<class_Material>`, billboard\: :ref:`bool<class_bool>` = false, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ )                                                 |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_mesh<class_EditorNode3DGizmo_method_add_mesh>`\ (\ mesh\: :ref:`Mesh<class_Mesh>`, material\: :ref:`Material<class_Material>` = null, transform\: :ref:`Transform3D<class_Transform3D>` = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0), skeleton\: :ref:`SkinReference<class_SkinReference>` = null\ )              |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`add_unscaled_billboard<class_EditorNode3DGizmo_method_add_unscaled_billboard>`\ (\ material\: :ref:`Material<class_Material>`, default_scale\: :ref:`float<class_float>` = 1, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ )                                                                                  |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`clear<class_EditorNode3DGizmo_method_clear>`\ (\ )                                                                                                                                                                                                                                                                         |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node3D<class_Node3D>`                                   | :ref:`get_node_3d<class_EditorNode3DGizmo_method_get_node_3d>`\ (\ ) |const|                                                                                                                                                                                                                                                     |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorNode3DGizmoPlugin<class_EditorNode3DGizmoPlugin>` | :ref:`get_plugin<class_EditorNode3DGizmo_method_get_plugin>`\ (\ ) |const|                                                                                                                                                                                                                                                       |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`               | :ref:`get_subgizmo_selection<class_EditorNode3DGizmo_method_get_subgizmo_selection>`\ (\ ) |const|                                                                                                                                                                                                                               |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                       | :ref:`is_subgizmo_selected<class_EditorNode3DGizmo_method_is_subgizmo_selected>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                       |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`set_hidden<class_EditorNode3DGizmo_method_set_hidden>`\ (\ hidden\: :ref:`bool<class_bool>`\ )                                                                                                                                                                                                                             |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`set_node_3d<class_EditorNode3DGizmo_method_set_node_3d>`\ (\ node\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                                             |
   +---------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorNode3DGizmo_private_method__begin_handle_action:

.. rst-class:: classref-method

|void| **_begin_handle_action**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__begin_handle_action>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__commit_handle:

.. rst-class:: classref-method

|void| **_commit_handle**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, restore\: :ref:`Variant<class_Variant>`, cancel\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__commit_handle>`

Ghi đè phương thức này để commit một handle đang được chỉnh sửa (các handle trước đó phải được thêm bằng :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>`). Thông thường, điều này có nghĩa là tạo một action :ref:`UndoRedo<class_UndoRedo>` cho thay đổi, sử dụng giá trị handle hiện tại làm "do" và đối số ``restore`` làm "undo".

Nếu đối số ``cancel`` là ``true``, giá trị ``restore`` phải được thiết lập trực tiếp mà không cần action :ref:`UndoRedo<class_UndoRedo>`.

Đối số ``secondary`` là ``true`` khi handle được commit là handle phụ (xem :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__commit_subgizmos:

.. rst-class:: classref-method

|void| **_commit_subgizmos**\ (\ ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, restores\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], cancel\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__commit_subgizmos>`

Ghi đè phương thức này để commit một nhóm subgizmo đang được chỉnh sửa (xem :ref:`_subgizmos_intersect_ray()<class_EditorNode3DGizmo_private_method__subgizmos_intersect_ray>` và :ref:`_subgizmos_intersect_frustum()<class_EditorNode3DGizmo_private_method__subgizmos_intersect_frustum>`). Thông thường, điều này có nghĩa là tạo một action :ref:`UndoRedo<class_UndoRedo>` cho thay đổi, sử dụng các transform hiện tại làm "do" và các transform ``restores`` làm "undo".

Nếu đối số ``cancel`` là ``true``, các transform ``restores`` phải được thiết lập trực tiếp mà không cần action :ref:`UndoRedo<class_UndoRedo>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__get_handle_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_handle_name**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__get_handle_name>`

Ghi đè phương thức này để trả về tên của một handle đang được chỉnh sửa (các handle trước đó phải được thêm bằng :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>`). Có thể đặt tên cho các handle để người dùng tham chiếu khi chỉnh sửa.

Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__get_handle_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_handle_value**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__get_handle_value>`

Ghi đè phương thức này để trả về giá trị hiện tại của một handle. Giá trị này sẽ được yêu cầu khi bắt đầu chỉnh sửa và được sử dụng làm đối số ``restore`` trong :ref:`_commit_handle()<class_EditorNode3DGizmo_private_method__commit_handle>`.

Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__get_subgizmo_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **_get_subgizmo_transform**\ (\ id\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__get_subgizmo_transform>`

Ghi đè phương thức này để trả về transform hiện tại của một subgizmo. Transform này sẽ được yêu cầu khi bắt đầu chỉnh sửa và được sử dụng làm đối số ``restore`` trong :ref:`_commit_subgizmos()<class_EditorNode3DGizmo_private_method__commit_subgizmos>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__is_handle_highlighted:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_handle_highlighted**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__is_handle_highlighted>`

Ghi đè phương thức này để trả về ``true`` bất cứ khi nào handle đã cho cần được làm nổi bật trong editor.

Đối số ``secondary`` là ``true`` khi handle được yêu cầu là handle phụ (xem :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__redraw:

.. rst-class:: classref-method

|void| **_redraw**\ (\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__redraw>`

Ghi đè phương thức này để thêm tất cả các phần tử gizmo mỗi khi có yêu cầu cập nhật gizmo. Thông thường, bạn sẽ gọi :ref:`clear()<class_EditorNode3DGizmo_method_clear>` ở đầu phương thức này rồi thêm các phần tử trực quan tùy thuộc vào các thuộc tính của node.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__set_handle:

.. rst-class:: classref-method

|void| **_set_handle**\ (\ id\: :ref:`int<class_int>`, secondary\: :ref:`bool<class_bool>`, camera\: :ref:`Camera3D<class_Camera3D>`, point\: :ref:`Vector2<class_Vector2>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__set_handle>`

Ghi đè phương thức này để cập nhật các thuộc tính của node khi người dùng kéo một handle gizmo (trước đó đã được thêm bằng :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>`). ``point`` được cung cấp là vị trí chuột trong tọa độ màn hình và ``camera`` có thể được sử dụng để chuyển đổi nó thành các raycast.

Đối số ``secondary`` là ``true`` khi handle đang được chỉnh sửa là handle phụ (xem :ref:`add_handles()<class_EditorNode3DGizmo_method_add_handles>` để biết thêm thông tin).

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__set_subgizmo_transform:

.. rst-class:: classref-method

|void| **_set_subgizmo_transform**\ (\ id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) |virtual| :ref:`🔗<class_EditorNode3DGizmo_private_method__set_subgizmo_transform>`

Ghi đè phương thức này để cập nhật các thuộc tính của node trong quá trình chỉnh sửa subgizmo (xem :ref:`_subgizmos_intersect_ray()<class_EditorNode3DGizmo_private_method__subgizmos_intersect_ray>` và :ref:`_subgizmos_intersect_frustum()<class_EditorNode3DGizmo_private_method__subgizmos_intersect_frustum>`). ``transform`` được cung cấp trong hệ tọa độ cục bộ của :ref:`Node3D<class_Node3D>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__subgizmos_intersect_frustum:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **_subgizmos_intersect_frustum**\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, frustum\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__subgizmos_intersect_frustum>`

Ghi đè phương thức này để cho phép chọn các subgizmo bằng thao tác kéo hộp chọn bằng chuột. Với một ``camera`` và một ``frustum``, phương thức này phải trả về các subgizmo nằm trong frustum. Đối số ``frustum`` bao gồm một mảng chứa tất cả các :ref:`Plane<class_Plane>`\ s tạo nên frustum lựa chọn. Giá trị trả về phải chứa danh sách các mã định danh subgizmo duy nhất, có thể là bất kỳ giá trị không âm nào và sẽ được sử dụng trong các virtual method khác như :ref:`_get_subgizmo_transform()<class_EditorNode3DGizmo_private_method__get_subgizmo_transform>` hoặc :ref:`_commit_subgizmos()<class_EditorNode3DGizmo_private_method__commit_subgizmos>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_private_method__subgizmos_intersect_ray:

.. rst-class:: classref-method

:ref:`int<class_int>` **_subgizmos_intersect_ray**\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, point\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_EditorNode3DGizmo_private_method__subgizmos_intersect_ray>`

Ghi đè phương thức này để cho phép chọn các subgizmo bằng thao tác nhấp chuột. Với một ``camera`` và một ``point`` trong tọa độ màn hình, phương thức này phải trả về subgizmo cần được chọn. Giá trị trả về phải là một mã định danh subgizmo duy nhất, có thể là bất kỳ giá trị không âm nào và sẽ được sử dụng trong các virtual method khác như :ref:`_get_subgizmo_transform()<class_EditorNode3DGizmo_private_method__get_subgizmo_transform>` hoặc :ref:`_commit_subgizmos()<class_EditorNode3DGizmo_private_method__commit_subgizmos>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_collision_segments:

.. rst-class:: classref-method

|void| **add_collision_segments**\ (\ segments\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_collision_segments>`

Thêm các ``segments`` được chỉ định vào collision shape của gizmo để picking. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_collision_triangles:

.. rst-class:: classref-method

|void| **add_collision_triangles**\ (\ triangles\: :ref:`TriangleMesh<class_TriangleMesh>`\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_collision_triangles>`

Thêm các collision triangle vào gizmo để picking. Cũng có thể tạo :ref:`TriangleMesh<class_TriangleMesh>` từ một :ref:`Mesh<class_Mesh>` thông thường. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_handles:

.. rst-class:: classref-method

|void| **add_handles**\ (\ handles\: :ref:`PackedVector3Array<class_PackedVector3Array>`, material\: :ref:`Material<class_Material>`, ids\: :ref:`PackedInt32Array<class_PackedInt32Array>`, billboard\: :ref:`bool<class_bool>` = false, secondary\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_handles>`

Thêm danh sách các handle (điểm) có thể được sử dụng để chỉnh sửa các thuộc tính của :ref:`Node3D<class_Node3D>` của gizmo. Có thể sử dụng đối số ``ids`` để chỉ định mã định danh tùy chỉnh cho từng handle; nếu truyền vào một mảng rỗng, các id sẽ được tự động gán theo thứ tự của đối số ``handles``.

Đối số ``secondary`` đánh dấu các handle được thêm là handle phụ, nghĩa là chúng thường có độ ưu tiên chọn thấp hơn các handle thông thường. Khi người dùng giữ phím shift, các handle phụ sẽ chuyển sang có độ ưu tiên cao hơn các handle thông thường. Thay đổi độ ưu tiên này có thể được sử dụng để đặt nhiều handle tại cùng một điểm mà vẫn cho phép người dùng kiểm soát lựa chọn của mình.

Có các virtual method sẽ được gọi khi chỉnh sửa những handle này. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_lines:

.. rst-class:: classref-method

|void| **add_lines**\ (\ lines\: :ref:`PackedVector3Array<class_PackedVector3Array>`, material\: :ref:`Material<class_Material>`, billboard\: :ref:`bool<class_bool>` = false, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_lines>`

Thêm các đường thẳng vào gizmo (dưới dạng các tập hợp gồm 2 điểm), cùng với material đã cho. Các đường thẳng được dùng để trực quan hóa gizmo. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_mesh:

.. rst-class:: classref-method

|void| **add_mesh**\ (\ mesh\: :ref:`Mesh<class_Mesh>`, material\: :ref:`Material<class_Material>` = null, transform\: :ref:`Transform3D<class_Transform3D>` = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0), skeleton\: :ref:`SkinReference<class_SkinReference>` = null\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_mesh>`

Thêm một mesh vào gizmo với ``material``, ``transform`` cục bộ và ``skeleton`` được chỉ định. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_add_unscaled_billboard:

.. rst-class:: classref-method

|void| **add_unscaled_billboard**\ (\ material\: :ref:`Material<class_Material>`, default_scale\: :ref:`float<class_float>` = 1, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1)\ ) :ref:`🔗<class_EditorNode3DGizmo_method_add_unscaled_billboard>`

Thêm một billboard không co giãn để trực quan hóa và lựa chọn. Gọi phương thức này trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_EditorNode3DGizmo_method_clear>`

Xóa mọi thứ trong gizmo, bao gồm mesh, collision và handle.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_get_node_3d:

.. rst-class:: classref-method

:ref:`Node3D<class_Node3D>` **get_node_3d**\ (\ ) |const| :ref:`🔗<class_EditorNode3DGizmo_method_get_node_3d>`

Trả về node :ref:`Node3D<class_Node3D>` được liên kết với gizmo này.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_get_plugin:

.. rst-class:: classref-method

:ref:`EditorNode3DGizmoPlugin<class_EditorNode3DGizmoPlugin>` **get_plugin**\ (\ ) |const| :ref:`🔗<class_EditorNode3DGizmo_method_get_plugin>`

Trả về :ref:`EditorNode3DGizmoPlugin<class_EditorNode3DGizmoPlugin>` sở hữu gizmo này. Phương thức này hữu ích để lấy material bằng :ref:`EditorNode3DGizmoPlugin.get_material()<class_EditorNode3DGizmoPlugin_method_get_material>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_get_subgizmo_selection:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_subgizmo_selection**\ (\ ) |const| :ref:`🔗<class_EditorNode3DGizmo_method_get_subgizmo_selection>`

Trả về danh sách các subgizmo hiện đang được chọn. Có thể dùng để làm nổi bật các phần tử đã chọn trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_is_subgizmo_selected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_subgizmo_selected**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorNode3DGizmo_method_is_subgizmo_selected>`

Trả về ``true`` nếu subgizmo đã cho hiện đang được chọn. Có thể dùng để làm nổi bật các phần tử đã chọn trong :ref:`_redraw()<class_EditorNode3DGizmo_private_method__redraw>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_set_hidden:

.. rst-class:: classref-method

|void| **set_hidden**\ (\ hidden\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorNode3DGizmo_method_set_hidden>`

Thiết lập trạng thái ẩn của gizmo. Nếu ``true``, gizmo sẽ bị ẩn. Nếu ``false``, gizmo sẽ được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_EditorNode3DGizmo_method_set_node_3d:

.. rst-class:: classref-method

|void| **set_node_3d**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_EditorNode3DGizmo_method_set_node_3d>`

Thiết lập node :ref:`Node3D<class_Node3D>` tham chiếu cho gizmo. ``node`` phải kế thừa từ :ref:`Node3D<class_Node3D>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
