:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ModifierBoneTarget3D.xml.

.. _class_ModifierBoneTarget3D:

ModifierBoneTarget3D
====================

**Kế thừa:** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node sao chép động phép biến đổi 3D của một bone trong :ref:`Skeleton3D<class_Skeleton3D>` cha của nó.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này chọn một bone trong :ref:`Skeleton3D<class_Skeleton3D>` và gắn vào bone đó. Điều này có nghĩa là node **ModifierBoneTarget3D** sẽ động sao chép phép biến đổi 3D của bone đã chọn.

Chức năng này tương tự :ref:`BoneAttachment3D<class_BoneAttachment3D>`, nhưng node này sử dụng chu kỳ :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` và được thiết kế để làm target cho một :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` khác.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+-----------------------------------------------------------------+--------+
   | :ref:`int<class_int>`       | :ref:`bone<class_ModifierBoneTarget3D_property_bone>`           | ``-1`` |
   +-----------------------------+-----------------------------------------------------------------+--------+
   | :ref:`String<class_String>` | :ref:`bone_name<class_ModifierBoneTarget3D_property_bone_name>` | ``""`` |
   +-----------------------------+-----------------------------------------------------------------+--------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ModifierBoneTarget3D_property_bone:

.. rst-class:: classref-property

:ref:`int<class_int>` **bone** = ``-1`` :ref:`🔗<class_ModifierBoneTarget3D_property_bone>`

.. rst-class:: classref-property-setget

- |void| **set_bone**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bone**\ (\ )

Chỉ mục của bone được gắn.

.. rst-class:: classref-item-separator

----

.. _class_ModifierBoneTarget3D_property_bone_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **bone_name** = ``""`` :ref:`🔗<class_ModifierBoneTarget3D_property_bone_name>`

.. rst-class:: classref-property-setget

- |void| **set_bone_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_bone_name**\ (\ )

Tên của bone được gắn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
