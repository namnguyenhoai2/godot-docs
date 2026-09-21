:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRIPBinding.xml.

.. _class_OpenXRIPBinding:

OpenXRIPBinding
===============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Xác định một binding giữa một :ref:`OpenXRAction<class_OpenXRAction>` và một đầu vào hoặc đầu ra XR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource binding này liên kết một :ref:`OpenXRAction<class_OpenXRAction>` với một đầu vào hoặc đầu ra. Vì hầu hết controller đều có phiên bản tay trái và tay phải được xử lý bởi cùng một interaction profile, chúng ta có thể chỉ định nhiều binding. Ví dụ, một action "Fire" có thể được liên kết với cả "/user/hand/left/input/trigger" và "/user/hand/right/input/trigger". Điều này sẽ yêu cầu hai mục binding.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------+--------+
   | :ref:`OpenXRAction<class_OpenXRAction>`           | :ref:`action<class_OpenXRIPBinding_property_action>`                       |        |
   +---------------------------------------------------+----------------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`                         | :ref:`binding_modifiers<class_OpenXRIPBinding_property_binding_modifiers>` | ``[]`` |
   +---------------------------------------------------+----------------------------------------------------------------------------+--------+
   | :ref:`String<class_String>`                       | :ref:`binding_path<class_OpenXRIPBinding_property_binding_path>`           | ``""`` |
   +---------------------------------------------------+----------------------------------------------------------------------------+--------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`paths<class_OpenXRIPBinding_property_paths>`                         |        |
   +---------------------------------------------------+----------------------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`add_path<class_OpenXRIPBinding_method_add_path>`\ (\ path\: :ref:`String<class_String>`\ )                            |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRActionBindingModifier<class_OpenXRActionBindingModifier>` | :ref:`get_binding_modifier<class_OpenXRIPBinding_method_get_binding_modifier>`\ (\ index\: :ref:`int<class_int>`\ ) |const| |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                 | :ref:`get_binding_modifier_count<class_OpenXRIPBinding_method_get_binding_modifier_count>`\ (\ ) |const|                    |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                 | :ref:`get_path_count<class_OpenXRIPBinding_method_get_path_count>`\ (\ ) |const|                                            |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`has_path<class_OpenXRIPBinding_method_has_path>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                    |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`remove_path<class_OpenXRIPBinding_method_remove_path>`\ (\ path\: :ref:`String<class_String>`\ )                      |
   +-----------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRIPBinding_property_action:

.. rst-class:: classref-property

:ref:`OpenXRAction<class_OpenXRAction>` **action** :ref:`🔗<class_OpenXRIPBinding_property_action>`

.. rst-class:: classref-property-setget

- |void| **set_action**\ (\ value\: :ref:`OpenXRAction<class_OpenXRAction>`\ ) - :ref:`OpenXRAction<class_OpenXRAction>` **get_action**\ (\ )

:ref:`OpenXRAction<class_OpenXRAction>` được liên kết với :ref:`binding_path<class_OpenXRIPBinding_property_binding_path>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_property_binding_modifiers:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **binding_modifiers** = ``[]`` :ref:`🔗<class_OpenXRIPBinding_property_binding_modifiers>`

.. rst-class:: classref-property-setget

- |void| **set_binding_modifiers**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_binding_modifiers**\ (\ )

Các binding modifier cho binding này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_property_binding_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **binding_path** = ``""`` :ref:`🔗<class_OpenXRIPBinding_property_binding_path>`

.. rst-class:: classref-property-setget

- |void| **set_binding_path**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_binding_path**\ (\ )

Đường dẫn binding xác định đầu vào hoặc đầu ra được liên kết với :ref:`action<class_OpenXRIPBinding_property_action>`.

\ **Lưu ý:** Đường dẫn binding chỉ là các đề xuất; một XR runtime có thể chọn liên kết action với một đầu vào hoặc đầu ra khác mô phỏng đầu vào hoặc đầu ra này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_property_paths:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **paths** :ref:`🔗<class_OpenXRIPBinding_property_paths>`

.. rst-class:: classref-property-setget

- |void| **set_paths**\ (\ value\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) - :ref:`PackedStringArray<class_PackedStringArray>` **get_paths**\ (\ )

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`binding_path<class_OpenXRIPBinding_property_binding_path>`.

Các đường dẫn xác định những đầu vào hoặc đầu ra được liên kết trên thiết bị.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRIPBinding_method_add_path:

.. rst-class:: classref-method

|void| **add_path**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRIPBinding_method_add_path>`

**Đã deprecated:** Binding chỉ dành cho một đường dẫn.

Thêm một đường dẫn đầu vào/đầu ra vào binding này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_method_get_binding_modifier:

.. rst-class:: classref-method

:ref:`OpenXRActionBindingModifier<class_OpenXRActionBindingModifier>` **get_binding_modifier**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRIPBinding_method_get_binding_modifier>`

Lấy :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` tại chỉ mục này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_method_get_binding_modifier_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_binding_modifier_count**\ (\ ) |const| :ref:`🔗<class_OpenXRIPBinding_method_get_binding_modifier_count>`

Lấy số lượng binding modifier cho binding này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_method_get_path_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_path_count**\ (\ ) |const| :ref:`🔗<class_OpenXRIPBinding_method_get_path_count>`

**Đã deprecated:** Binding chỉ dành cho một đường dẫn.

Lấy số lượng đường dẫn đầu vào/đầu ra trong binding này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_method_has_path:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_path**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_OpenXRIPBinding_method_has_path>`

**Đã deprecated:** Binding chỉ dành cho một đường dẫn.

Trả về ``true`` nếu đường dẫn đầu vào/đầu ra này thuộc binding này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRIPBinding_method_remove_path:

.. rst-class:: classref-method

|void| **remove_path**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_OpenXRIPBinding_method_remove_path>`

**Đã deprecated:** Binding chỉ dành cho một đường dẫn.

Xóa đường dẫn đầu vào/đầu ra này khỏi binding.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
