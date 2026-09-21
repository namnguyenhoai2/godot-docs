:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFMesh.xml.

.. _class_GLTFMesh:

GLTFMesh
========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

GLTFMesh đại diện cho một mesh glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

GLTFMesh xử lý dữ liệu mesh 3D được import từ các tệp glTF. Nó bao gồm các thuộc tính cho blend channel, blend weight, material của instance và chính mesh đó.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Tải và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`          | :ref:`blend_weights<class_GLTFMesh_property_blend_weights>`           | ``PackedFloat32Array()`` |
   +--------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\] | :ref:`instance_materials<class_GLTFMesh_property_instance_materials>` | ``[]``                   |
   +--------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------+
   | :ref:`ImporterMesh<class_ImporterMesh>`                      | :ref:`mesh<class_GLTFMesh_property_mesh>`                             |                          |
   +--------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------+
   | :ref:`String<class_String>`                                  | :ref:`original_name<class_GLTFMesh_property_original_name>`           | ``""``                   |
   +--------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`get_additional_data<class_GLTFMesh_method_get_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`\ )                                                  |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_additional_data<class_GLTFMesh_method_set_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFMesh_property_blend_weights:

.. rst-class:: classref-property

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **blend_weights** = ``PackedFloat32Array()`` :ref:`🔗<class_GLTFMesh_property_blend_weights>`

.. rst-class:: classref-property-setget

- |void| **set_blend_weights**\ (\ value\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) - :ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_blend_weights**\ (\ )

Một mảng các số thực biểu diễn blend weight của mesh.

**Lưu ý:** Mảng được trả về là một *bản sao* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat32Array<class_PackedFloat32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFMesh_property_instance_materials:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\] **instance_materials** = ``[]`` :ref:`🔗<class_GLTFMesh_property_instance_materials>`

.. rst-class:: classref-property-setget

- |void| **set_instance_materials**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\] **get_instance_materials**\ (\ )

Một mảng các đối tượng Material đại diện cho các material được sử dụng trong mesh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFMesh_property_mesh:

.. rst-class:: classref-property

:ref:`ImporterMesh<class_ImporterMesh>` **mesh** :ref:`🔗<class_GLTFMesh_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`ImporterMesh<class_ImporterMesh>`\ ) - :ref:`ImporterMesh<class_ImporterMesh>` **get_mesh**\ (\ )

Đối tượng :ref:`ImporterMesh<class_ImporterMesh>` đại diện cho chính mesh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFMesh_property_original_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **original_name** = ``""`` :ref:`🔗<class_GLTFMesh_property_original_name>`

.. rst-class:: classref-property-setget

- |void| **set_original_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_original_name**\ (\ )

Tên ban đầu của mesh.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFMesh_method_get_additional_data:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_GLTFMesh_method_get_additional_data>`

Lấy dữ liệu bổ sung tùy ý trong instance **GLTFMesh** này. Dữ liệu này có thể được dùng để lưu state data theo từng node trong các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này rất quan trọng vì chúng stateless.

Đối số phải là tên :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` (không nhất thiết phải khớp với tên extension trong tệp glTF), và giá trị trả về có thể là bất kỳ giá trị nào bạn đặt. Nếu chưa đặt gì, giá trị trả về là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFMesh_method_set_additional_data:

.. rst-class:: classref-method

|void| **set_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GLTFMesh_method_set_additional_data>`

Thiết lập dữ liệu bổ sung tùy ý trong instance **GLTFMesh** này. Dữ liệu này có thể được dùng để lưu state data theo từng node trong các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này rất quan trọng vì chúng stateless.

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
