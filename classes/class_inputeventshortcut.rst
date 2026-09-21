:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventShortcut.xml.

.. _class_InputEventShortcut:

InputEventShortcut
==================

**Kế thừa:** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một :ref:`Shortcut<class_Shortcut>` bàn phím đã được kích hoạt.

.. rst-class:: classref-introduction-group

Mô tả
-----

InputEventShortcut là một sự kiện đặc biệt có thể được nhận trong :ref:`Node._input()<class_Node_private_method__input>`, :ref:`Node._shortcut_input()<class_Node_private_method__shortcut_input>` và :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>`. Sự kiện này thường được Command Palette của editor gửi để kích hoạt các action, nhưng cũng có thể được gửi thủ công bằng :ref:`Viewport.push_input()<class_Viewport_method_push_input>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-------------------------------------------------------------+
   | :ref:`Shortcut<class_Shortcut>` | :ref:`shortcut<class_InputEventShortcut_property_shortcut>` |
   +---------------------------------+-------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventShortcut_property_shortcut:

.. rst-class:: classref-property

:ref:`Shortcut<class_Shortcut>` **shortcut** :ref:`🔗<class_InputEventShortcut_property_shortcut>`

.. rst-class:: classref-property-setget

- |void| **set_shortcut**\ (\ value\: :ref:`Shortcut<class_Shortcut>`\ ) - :ref:`Shortcut<class_Shortcut>` **get_shortcut**\ (\ )

:ref:`Shortcut<class_Shortcut>` được sự kiện này đại diện. Phương thức :ref:`Shortcut.matches_event()<class_Shortcut_method_matches_event>` của nó sẽ luôn trả về ``true`` đối với sự kiện này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
