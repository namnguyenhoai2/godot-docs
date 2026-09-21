:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorToaster.xml.

.. _class_EditorToaster:

EditorToaster
=============

**Kế thừa:** :ref:`HBoxContainer<class_HBoxContainer>` **<** :ref:`BoxContainer<class_BoxContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Quản lý các thông báo toast trong editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng này quản lý chức năng và cách hiển thị các thông báo toast trong editor, bảo đảm người dùng nhận được các cảnh báo tức thời và đầy đủ thông tin.

\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Thay vào đó, hãy truy cập singleton bằng :ref:`EditorInterface.get_editor_toaster()<class_EditorInterface_method_get_editor_toaster>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`push_toast<class_EditorToaster_method_push_toast>`\ (\ message\: :ref:`String<class_String>`, severity\: :ref:`Severity<enum_EditorToaster_Severity>` = 0, tooltip\: :ref:`String<class_String>` = ""\ ) |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_EditorToaster_Severity:

.. rst-class:: classref-enumeration

enum **Severity**: :ref:`🔗<enum_EditorToaster_Severity>`

.. _class_EditorToaster_constant_SEVERITY_INFO:

.. rst-class:: classref-enumeration-constant

:ref:`Severity<enum_EditorToaster_Severity>` **SEVERITY_INFO** = ``0``

Toast sẽ được hiển thị với mức độ INFO.

.. _class_EditorToaster_constant_SEVERITY_WARNING:

.. rst-class:: classref-enumeration-constant

:ref:`Severity<enum_EditorToaster_Severity>` **SEVERITY_WARNING** = ``1``

Toast sẽ được hiển thị với mức độ WARNING và có màu tương ứng.

.. _class_EditorToaster_constant_SEVERITY_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Severity<enum_EditorToaster_Severity>` **SEVERITY_ERROR** = ``2``

Toast sẽ được hiển thị với mức độ ERROR và có màu tương ứng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorToaster_method_push_toast:

.. rst-class:: classref-method

|void| **push_toast**\ (\ message\: :ref:`String<class_String>`, severity\: :ref:`Severity<enum_EditorToaster_Severity>` = 0, tooltip\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_EditorToaster_method_push_toast>`

Đẩy một thông báo toast vào editor để hiển thị.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
