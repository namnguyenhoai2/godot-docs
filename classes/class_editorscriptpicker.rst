:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorScriptPicker.xml.

.. _class_EditorScriptPicker:

EditorScriptPicker
==================

**Kế thừa:** :ref:`EditorResourcePicker<class_EditorResourcePicker>` **<** :ref:`HBoxContainer<class_HBoxContainer>` **<** :ref:`BoxContainer<class_BoxContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Control của Godot editor dùng để chọn property ``script`` của một :ref:`Node<class_Node>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tương tự như :ref:`EditorResourcePicker<class_EditorResourcePicker>`, node :ref:`Control<class_Control>` này được dùng trong dock Inspector của editor, nhưng chỉ để chỉnh sửa property ``script`` của một :ref:`Node<class_Node>`. Các tùy chọn mặc định để tạo resource mới thuộc mọi subtype có thể có được thay thế bằng các button chuyên dụng, mở hộp thoại "Attach Node Script". Có thể dùng với :ref:`EditorInspectorPlugin<class_EditorInspectorPlugin>` để tái tạo cùng hành vi.

\ **Lưu ý:** Bạn phải đặt :ref:`script_owner<class_EditorScriptPicker_property_script_owner>` để các mục trong context menu tùy chỉnh hoạt động.

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------+
   | :ref:`Node<class_Node>` | :ref:`script_owner<class_EditorScriptPicker_property_script_owner>` |
   +-------------------------+---------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả property
--------------

.. _class_EditorScriptPicker_property_script_owner:

.. rst-class:: classref-property

:ref:`Node<class_Node>` **script_owner** :ref:`🔗<class_EditorScriptPicker_property_script_owner>`

.. rst-class:: classref-property-setget

- |void| **set_script_owner**\ (\ value\: :ref:`Node<class_Node>`\ ) - :ref:`Node<class_Node>` **get_script_owner**\ (\ )

Owner :ref:`Node<class_Node>` của property script chứa resource đang được chỉnh sửa.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
