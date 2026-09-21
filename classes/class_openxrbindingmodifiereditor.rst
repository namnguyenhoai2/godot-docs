:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRBindingModifierEditor.xml.

.. _class_OpenXRBindingModifierEditor:

OpenXRBindingModifierEditor
===========================

**Kế thừa:** :ref:`PanelContainer<class_PanelContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Trình chỉnh sửa binding modifier.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là trình chỉnh sửa binding modifier mặc định được sử dụng trong action map của OpenXR.

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` | :ref:`get_binding_modifier<class_OpenXRBindingModifierEditor_method_get_binding_modifier>`\ (\ ) |const|                                                                                                     |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`setup<class_OpenXRBindingModifierEditor_method_setup>`\ (\ action_map\: :ref:`OpenXRActionMap<class_OpenXRActionMap>`, binding_modifier\: :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>`\ ) |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_OpenXRBindingModifierEditor_signal_binding_modifier_removed:

.. rst-class:: classref-signal

**binding_modifier_removed**\ (\ binding_modifier_editor\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_OpenXRBindingModifierEditor_signal_binding_modifier_removed>`

Tín hiệu được phát ra khi người dùng nhấn nút xóa binding modifier cho modifier này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRBindingModifierEditor_method_get_binding_modifier:

.. rst-class:: classref-method

:ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` **get_binding_modifier**\ (\ ) |const| :ref:`🔗<class_OpenXRBindingModifierEditor_method_get_binding_modifier>`

Trả về :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` hiện đang được chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRBindingModifierEditor_method_setup:

.. rst-class:: classref-method

|void| **setup**\ (\ action_map\: :ref:`OpenXRActionMap<class_OpenXRActionMap>`, binding_modifier\: :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>`\ ) :ref:`🔗<class_OpenXRBindingModifierEditor_method_setup>`

Thiết lập trình chỉnh sửa này cho ``action_map`` và ``binding_modifier`` được cung cấp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
