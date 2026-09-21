:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFNode.xml.

.. _class_GLTFNode:

GLTFNode
========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp nút glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một nút glTF. Các nút glTF có thể có tên, phép biến đổi, các nút con (những nút glTF khác) và các thuộc tính chuyên biệt hơn (được đại diện bởi các lớp riêng).

Các nút glTF thường tồn tại bên trong :ref:`GLTFState<class_GLTFState>`, thành phần đại diện cho toàn bộ dữ liệu của một tệp glTF. Hầu hết các thuộc tính của GLTFNode là chỉ mục của dữ liệu khác trong tệp glTF. Bạn có thể mở rộng một nút glTF bằng các thuộc tính bổ sung thông qua :ref:`get_additional_data()<class_GLTFNode_method_get_additional_data>` và :ref:`set_additional_data()<class_GLTFNode_method_set_additional_data>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Tải và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `glTF scene and node spec <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_004_ScenesNodes.md">`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`camera<class_GLTFNode_property_camera>`               | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`children<class_GLTFNode_property_children>`           | ``PackedInt32Array()``                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`height<class_GLTFNode_property_height>`               | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`light<class_GLTFNode_property_light>`                 | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`mesh<class_GLTFNode_property_mesh>`                   | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`String<class_String>`                     | :ref:`original_name<class_GLTFNode_property_original_name>` | ``""``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`parent<class_GLTFNode_property_parent>`               | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`position<class_GLTFNode_property_position>`           | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`             | :ref:`rotation<class_GLTFNode_property_rotation>`           | ``Quaternion(0, 0, 0, 1)``                          |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`scale<class_GLTFNode_property_scale>`                 | ``Vector3(1, 1, 1)``                                |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`skeleton<class_GLTFNode_property_skeleton>`           | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`skin<class_GLTFNode_property_skin>`                   | ``-1``                                              |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`visible<class_GLTFNode_property_visible>`             | ``true``                                            |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`           | :ref:`xform<class_GLTFNode_property_xform>`                 | ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` |
   +-------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`append_child_index<class_GLTFNode_method_append_child_index>`\ (\ child_index\: :ref:`int<class_int>`\ )                                                                     |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`   | :ref:`get_additional_data<class_GLTFNode_method_get_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`\ )                                                  |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`get_scene_node_path<class_GLTFNode_method_get_scene_node_path>`\ (\ gltf_state\: :ref:`GLTFState<class_GLTFState>`, handle_skeletons\: :ref:`bool<class_bool>` = true\ )     |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`set_additional_data<class_GLTFNode_method_set_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) |
   +---------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFNode_property_camera:

.. rst-class:: classref-property

:ref:`int<class_int>` **camera** = ``-1`` :ref:`🔗<class_GLTFNode_property_camera>`

.. rst-class:: classref-property-setget

- |void| **set_camera**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_camera**\ (\ )

Nếu nút glTF này là một camera, đây là chỉ mục của :ref:`GLTFCamera<class_GLTFCamera>` trong :ref:`GLTFState<class_GLTFState>`, thành phần mô tả các thuộc tính của camera. Nếu ``-1``, nút này không phải là camera.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_children:

.. rst-class:: classref-property

:ref:`PackedInt32Array<class_PackedInt32Array>` **children** = ``PackedInt32Array()`` :ref:`🔗<class_GLTFNode_property_children>`

.. rst-class:: classref-property-setget

- |void| **set_children**\ (\ value\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) - :ref:`PackedInt32Array<class_PackedInt32Array>` **get_children**\ (\ )

Các chỉ mục của các nút con trong :ref:`GLTFState<class_GLTFState>`. Nếu nút glTF này không có nút con, đây sẽ là một mảng rỗng.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedInt32Array<class_PackedInt32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **height** = ``-1`` :ref:`🔗<class_GLTFNode_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_height**\ (\ )

Độ sâu của nút này trong hệ thống phân cấp nút. Một nút gốc có height bằng 0, các nút con của nó có height bằng 1, v.v. Nếu là -1, height chưa được tính.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_light:

.. rst-class:: classref-property

:ref:`int<class_int>` **light** = ``-1`` :ref:`🔗<class_GLTFNode_property_light>`

.. rst-class:: classref-property-setget

- |void| **set_light**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_light**\ (\ )

Nếu nút glTF này là một nguồn sáng, đây là chỉ mục của :ref:`GLTFLight<class_GLTFLight>` trong :ref:`GLTFState<class_GLTFState>`, thành phần mô tả các thuộc tính của nguồn sáng. Nếu là -1, nút này không phải là nguồn sáng.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_mesh:

.. rst-class:: classref-property

:ref:`int<class_int>` **mesh** = ``-1`` :ref:`🔗<class_GLTFNode_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_mesh**\ (\ )

Nếu nút glTF này là một mesh, đây là chỉ mục của :ref:`GLTFMesh<class_GLTFMesh>` trong :ref:`GLTFState<class_GLTFState>`, thành phần mô tả các thuộc tính của mesh. Nếu là -1, nút này không phải là mesh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_original_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **original_name** = ``""`` :ref:`🔗<class_GLTFNode_property_original_name>`

.. rst-class:: classref-property-setget

- |void| **set_original_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_original_name**\ (\ )

Tên ban đầu của nút.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_parent:

.. rst-class:: classref-property

:ref:`int<class_int>` **parent** = ``-1`` :ref:`🔗<class_GLTFNode_property_parent>`

.. rst-class:: classref-property-setget

- |void| **set_parent**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_parent**\ (\ )

Chỉ mục của nút cha trong :ref:`GLTFState<class_GLTFState>`. Nếu là -1, nút này là một nút gốc.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_GLTFNode_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_position**\ (\ )

Vị trí của nút glTF so với nút cha.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_rotation:

.. rst-class:: classref-property

:ref:`Quaternion<class_Quaternion>` **rotation** = ``Quaternion(0, 0, 0, 1)`` :ref:`🔗<class_GLTFNode_property_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_rotation**\ (\ value\: :ref:`Quaternion<class_Quaternion>`\ ) - :ref:`Quaternion<class_Quaternion>` **get_rotation**\ (\ )

Phép xoay của nút glTF so với nút cha.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_scale:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **scale** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_GLTFNode_property_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scale**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_scale**\ (\ )

Tỷ lệ của nút glTF so với nút cha.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_skeleton:

.. rst-class:: classref-property

:ref:`int<class_int>` **skeleton** = ``-1`` :ref:`🔗<class_GLTFNode_property_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_skeleton**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_skeleton**\ (\ )

Nếu nút glTF này có skeleton, đây là chỉ mục của :ref:`GLTFSkeleton<class_GLTFSkeleton>` trong :ref:`GLTFState<class_GLTFState>`, thành phần mô tả các thuộc tính của skeleton. Nếu là -1, nút này không có skeleton.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_skin:

.. rst-class:: classref-property

:ref:`int<class_int>` **skin** = ``-1`` :ref:`🔗<class_GLTFNode_property_skin>`

.. rst-class:: classref-property-setget

- |void| **set_skin**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_skin**\ (\ )

Nếu nút glTF này có skin, đây là chỉ mục của :ref:`GLTFSkin<class_GLTFSkin>` trong :ref:`GLTFState<class_GLTFState>`, thành phần mô tả các thuộc tính của skin. Nếu là -1, nút này không có skin.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_visible:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **visible** = ``true`` :ref:`🔗<class_GLTFNode_property_visible>`

.. rst-class:: classref-property-setget

- |void| **set_visible**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_visible**\ (\ )

Nếu ``true``, nút GLTF sẽ hiển thị. Nếu ``false``, nút GLTF sẽ không hiển thị. Giá trị này được chuyển đổi thành thuộc tính :ref:`Node3D.visible<class_Node3D_property_visible>` trong scene Godot và được xuất sang ``KHR_node_visibility`` khi ``false``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_property_xform:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **xform** = ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` :ref:`🔗<class_GLTFNode_property_xform>`

.. rst-class:: classref-property-setget

- |void| **set_xform**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_xform**\ (\ )

Phép biến đổi của nút glTF so với nút cha. Thuộc tính này thường không được sử dụng vì các thuộc tính position, rotation và scale được ưu tiên hơn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFNode_method_append_child_index:

.. rst-class:: classref-method

|void| **append_child_index**\ (\ child_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GLTFNode_method_append_child_index>`

Nối chỉ mục nút con đã cho vào mảng :ref:`children<class_GLTFNode_property_children>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_method_get_additional_data:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_GLTFNode_method_get_additional_data>`

Lấy dữ liệu tùy ý bổ sung trong thực thể **GLTFNode** này. Dữ liệu này có thể được dùng để lưu state data theo từng nút trong các lớp :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này quan trọng vì chúng không lưu state.

Đối số phải là tên :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` (không nhất thiết phải khớp với tên extension trong tệp glTF), và giá trị trả về có thể là bất kỳ giá trị nào bạn đặt. Nếu chưa đặt gì, giá trị trả về là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_method_get_scene_node_path:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_scene_node_path**\ (\ gltf_state\: :ref:`GLTFState<class_GLTFState>`, handle_skeletons\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_GLTFNode_method_get_scene_node_path>`

Trả về :ref:`NodePath<class_NodePath>` mà nút GLTF này sẽ có trong scene tree của Godot sau khi được import. Điều này hữu ích khi import các object model pointer của glTF bằng :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>`, để xử lý các extension như ``KHR_animation_pointer`` hoặc ``KHR_interactivity``.

Nếu ``handle_skeletons`` là ``true``, các path đến các nút glTF là bone của skeleton sẽ được resolve chính xác. Ví dụ, một path vốn là ``^"A/B/C/Bone1/Bone2/Bone3"`` nếu ``false`` sẽ trở thành ``^"A/B/C/Skeleton3D:Bone3"``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFNode_method_set_additional_data:

.. rst-class:: classref-method

|void| **set_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GLTFNode_method_set_additional_data>`

Thiết lập dữ liệu tùy ý bổ sung trong thực thể **GLTFNode** này. Dữ liệu này có thể được dùng để lưu state data theo từng nút trong các lớp :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này quan trọng vì chúng không lưu state.

Đối số đầu tiên phải là tên :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` (không nhất thiết phải khớp với tên extension trong tệp glTF), còn đối số thứ hai có thể là bất kỳ giá trị nào bạn muốn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
