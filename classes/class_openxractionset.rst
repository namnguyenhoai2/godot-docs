:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRActionSet.xml.

.. _class_OpenXRActionSet:

OpenXRActionSet
===============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tập hợp các tài nguyên :ref:`OpenXRAction<class_OpenXRAction>` tạo nên một action set.

.. rst-class:: classref-introduction-group

Mô tả
-----

Trong OpenXR, action set xác định một tập hợp các action có thể được kích hoạt đồng thời. Điều này cho phép game dễ dàng chuyển đổi giữa các trạng thái khác nhau, vốn yêu cầu các input khác nhau hoặc cần diễn giải lại input. Ví dụ: chúng ta có thể có một action set hoạt động khi menu đang mở, một action set hoạt động khi người chơi tự do di chuyển và một action set hoạt động khi người chơi điều khiển phương tiện.

Các action set có thể chứa cùng một action với cùng tên. Nếu các action set đó hoạt động cùng lúc, action set có priority cao nhất sẽ xác định binding nào đang hoạt động.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+----------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`   | :ref:`actions<class_OpenXRActionSet_property_actions>`               | ``[]`` |
   +-----------------------------+----------------------------------------------------------------------+--------+
   | :ref:`String<class_String>` | :ref:`localized_name<class_OpenXRActionSet_property_localized_name>` | ``""`` |
   +-----------------------------+----------------------------------------------------------------------+--------+
   | :ref:`int<class_int>`       | :ref:`priority<class_OpenXRActionSet_property_priority>`             | ``0``  |
   +-----------------------------+----------------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------+
   | |void|                | :ref:`add_action<class_OpenXRActionSet_method_add_action>`\ (\ action\: :ref:`OpenXRAction<class_OpenXRAction>`\ )       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`get_action_count<class_OpenXRActionSet_method_get_action_count>`\ (\ ) |const|                                     |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------+
   | |void|                | :ref:`remove_action<class_OpenXRActionSet_method_remove_action>`\ (\ action\: :ref:`OpenXRAction<class_OpenXRAction>`\ ) |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRActionSet_property_actions:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **actions** = ``[]`` :ref:`🔗<class_OpenXRActionSet_property_actions>`

.. rst-class:: classref-property-setget

- |void| **set_actions**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_actions**\ (\ )

Tập hợp các action của action set này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRActionSet_property_localized_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **localized_name** = ``""`` :ref:`🔗<class_OpenXRActionSet_property_localized_name>`

.. rst-class:: classref-property-setget

- |void| **set_localized_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_localized_name**\ (\ )

Tên đã bản địa hóa của action set này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRActionSet_property_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **priority** = ``0`` :ref:`🔗<class_OpenXRActionSet_property_priority>`

.. rst-class:: classref-property-setget

- |void| **set_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_priority**\ (\ )

Priority của action set này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRActionSet_method_add_action:

.. rst-class:: classref-method

|void| **add_action**\ (\ action\: :ref:`OpenXRAction<class_OpenXRAction>`\ ) :ref:`🔗<class_OpenXRActionSet_method_add_action>`

Thêm một action vào action set này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRActionSet_method_get_action_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_action_count**\ (\ ) |const| :ref:`🔗<class_OpenXRActionSet_method_get_action_count>`

Lấy số lượng action trong action set của chúng ta.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRActionSet_method_remove_action:

.. rst-class:: classref-method

|void| **remove_action**\ (\ action\: :ref:`OpenXRAction<class_OpenXRAction>`\ ) :ref:`🔗<class_OpenXRActionSet_method_remove_action>`

Xóa một action khỏi action set này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
