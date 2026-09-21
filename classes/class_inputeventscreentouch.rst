:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventScreenTouch.xml.

.. _class_InputEventScreenTouch:

InputEventScreenTouch
=====================

**Kế thừa:** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Biểu diễn một sự kiện chạm màn hình.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các sự kiện nhấn/thả trong chế độ multi-touch. Hỗ trợ chạm, nhả chạm và :ref:`index<class_InputEventScreenTouch_property_index>` cho số lượng và thứ tự của các lần chạm.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`canceled<class_InputEventScreenTouch_property_canceled>`     | ``false``         |
   +-------------------------------+--------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`double_tap<class_InputEventScreenTouch_property_double_tap>` | ``false``         |
   +-------------------------------+--------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`index<class_InputEventScreenTouch_property_index>`           | ``0``             |
   +-------------------------------+--------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`position<class_InputEventScreenTouch_property_position>`     | ``Vector2(0, 0)`` |
   +-------------------------------+--------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`pressed<class_InputEventScreenTouch_property_pressed>`       | ``false``         |
   +-------------------------------+--------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventScreenTouch_property_canceled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **canceled** = ``false`` :ref:`🔗<class_InputEventScreenTouch_property_canceled>`

.. rst-class:: classref-property-setget

- |void| **set_canceled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_canceled**\ (\ )

Nếu ``true``, sự kiện chạm đã bị hủy.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenTouch_property_double_tap:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **double_tap** = ``false`` :ref:`🔗<class_InputEventScreenTouch_property_double_tap>`

.. rst-class:: classref-property-setget

- |void| **set_double_tap**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_double_tap**\ (\ )

Nếu ``true``, trạng thái của lần chạm là chạm hai lần.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenTouch_property_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **index** = ``0`` :ref:`🔗<class_InputEventScreenTouch_property_index>`

.. rst-class:: classref-property-setget

- |void| **set_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_index**\ (\ )

Chỉ mục của lần chạm trong trường hợp sự kiện multi-touch. Một chỉ mục tương ứng với một ngón tay.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenTouch_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenTouch_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Vị trí chạm trong viewport mà node nằm trong đó, sử dụng hệ tọa độ của viewport này.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenTouch_property_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pressed** = ``false`` :ref:`🔗<class_InputEventScreenTouch_property_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của lần chạm là đang nhấn. Nếu ``false``, trạng thái của lần chạm là đã nhả.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
