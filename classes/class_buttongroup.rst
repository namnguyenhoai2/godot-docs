:github_url: hide

.. meta::
	:keywords: radio

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ButtonGroup.xml.

.. _class_ButtonGroup:

ButtonGroup
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một nhóm các nút không cho phép nhấn nhiều hơn một nút cùng lúc.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một nhóm các nút dẫn xuất từ :ref:`BaseButton<class_BaseButton>`. Các nút trong **ButtonGroup** được xử lý như các nút radio: Không thể nhấn nhiều hơn một nút cùng lúc. Một số loại nút (chẳng hạn như :ref:`CheckBox<class_CheckBox>`) có thể có giao diện đặc biệt ở trạng thái này.

Mọi thành viên của **ButtonGroup** nên được đặt :ref:`BaseButton.toggle_mode<class_BaseButton_property_toggle_mode>` thành ``true``.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`allow_unpress<class_ButtonGroup_property_allow_unpress>` | ``false``                                                                             |
   +-------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | resource_local_to_scene                                        | ``true`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`BaseButton<class_BaseButton>`\] | :ref:`get_buttons<class_ButtonGroup_method_get_buttons>`\ (\ )               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`BaseButton<class_BaseButton>`                              | :ref:`get_pressed_button<class_ButtonGroup_method_get_pressed_button>`\ (\ ) |
   +------------------------------------------------------------------+------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_ButtonGroup_signal_pressed:

.. rst-class:: classref-signal

**pressed**\ (\ button\: :ref:`BaseButton<class_BaseButton>`\ ) :ref:`🔗<class_ButtonGroup_signal_pressed>`

Được phát ra khi một trong các nút của nhóm được nhấn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ButtonGroup_property_allow_unpress:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **allow_unpress** = ``false`` :ref:`🔗<class_ButtonGroup_property_allow_unpress>`

.. rst-class:: classref-property-setget

- |void| **set_allow_unpress**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_allow_unpress**\ (\ )

Nếu ``true``, bạn có thể bỏ nhấn tất cả các nút trong **ButtonGroup** này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ButtonGroup_method_get_buttons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`BaseButton<class_BaseButton>`\] **get_buttons**\ (\ ) :ref:`🔗<class_ButtonGroup_method_get_buttons>`

Returns an :ref:`Array<class_Array>` of :ref:`Button<class_Button>`\ s who have this as their **ButtonGroup** (see :ref:`BaseButton.button_group<class_BaseButton_property_button_group>`).

.. rst-class:: classref-item-separator

----

.. _class_ButtonGroup_method_get_pressed_button:

.. rst-class:: classref-method

:ref:`BaseButton<class_BaseButton>` **get_pressed_button**\ (\ ) :ref:`🔗<class_ButtonGroup_method_get_pressed_button>`

Trả về nút hiện đang được nhấn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
