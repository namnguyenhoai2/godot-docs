:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRAction.xml.

.. _class_OpenXRAction:

OpenXRAction
============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một action OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource này định nghĩa một action OpenXR. Action có thể được dùng cho cả đầu vào (button, joystick, trigger, v.v.) và đầu ra (haptic).

OpenXR tự động chuyển đổi giữa kiểu action và kiểu đầu vào bất cứ khi nào có thể. Do đó, một trigger analog được liên kết với một action boolean sẽ trả về ``false`` khi trigger được nhấn xuống và ``true`` khi được nhấn hết mức.

Action không được liên kết trực tiếp với các thiết bị cụ thể; thay vào đó, OpenXR nhận diện một số lượng giới hạn các đường dẫn cấp cao nhất xác định thiết bị theo cách sử dụng. Chúng ta có thể giới hạn những thiết bị mà một action có thể được liên kết bằng các đường dẫn cấp cao nhất này. Ví dụ, một action chỉ được dùng cho các controller cầm tay có thể liên kết với các đường dẫn cấp cao nhất "/user/hand/left" và "/user/hand/right". Xem `reserved path section in the OpenXR specification <https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#semantic-path-reserved>`__ để biết thêm thông tin về các đường dẫn cấp cao nhất.

Lưu ý rằng tên của resource được dùng để đăng ký action.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------+-------------------------+
   | :ref:`ActionType<enum_OpenXRAction_ActionType>`   | :ref:`action_type<class_OpenXRAction_property_action_type>`       | ``1``                   |
   +---------------------------------------------------+-------------------------------------------------------------------+-------------------------+
   | :ref:`String<class_String>`                       | :ref:`localized_name<class_OpenXRAction_property_localized_name>` | ``""``                  |
   +---------------------------------------------------+-------------------------------------------------------------------+-------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`toplevel_paths<class_OpenXRAction_property_toplevel_paths>` | ``PackedStringArray()`` |
   +---------------------------------------------------+-------------------------------------------------------------------+-------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_OpenXRAction_ActionType:

.. rst-class:: classref-enumeration

enum **ActionType**: :ref:`🔗<enum_OpenXRAction_ActionType>`

.. _class_OpenXRAction_constant_OPENXR_ACTION_BOOL:

.. rst-class:: classref-enumeration-constant

:ref:`ActionType<enum_OpenXRAction_ActionType>` **OPENXR_ACTION_BOOL** = ``0``

Action này cung cấp một giá trị boolean.

.. _class_OpenXRAction_constant_OPENXR_ACTION_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`ActionType<enum_OpenXRAction_ActionType>` **OPENXR_ACTION_FLOAT** = ``1``

Action này cung cấp một giá trị float nằm giữa ``0.0`` và ``1.0`` cho mọi đầu vào analog như trigger.

.. _class_OpenXRAction_constant_OPENXR_ACTION_VECTOR2:

.. rst-class:: classref-enumeration-constant

:ref:`ActionType<enum_OpenXRAction_ActionType>` **OPENXR_ACTION_VECTOR2** = ``2``

Action này cung cấp một giá trị :ref:`Vector2<class_Vector2>` và có thể được liên kết với trackpad tích hợp và joystick.

.. _class_OpenXRAction_constant_OPENXR_ACTION_POSE:

.. rst-class:: classref-enumeration-constant

:ref:`ActionType<enum_OpenXRAction_ActionType>` **OPENXR_ACTION_POSE** = ``3``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRAction_property_action_type:

.. rst-class:: classref-property

:ref:`ActionType<enum_OpenXRAction_ActionType>` **action_type** = ``1`` :ref:`🔗<class_OpenXRAction_property_action_type>`

.. rst-class:: classref-property-setget

- |void| **set_action_type**\ (\ value\: :ref:`ActionType<enum_OpenXRAction_ActionType>`\ ) - :ref:`ActionType<enum_OpenXRAction_ActionType>` **get_action_type**\ (\ )

Kiểu của action.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRAction_property_localized_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **localized_name** = ``""`` :ref:`🔗<class_OpenXRAction_property_localized_name>`

.. rst-class:: classref-property-setget

- |void| **set_localized_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_localized_name**\ (\ )

Mô tả được bản địa hóa của action này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRAction_property_toplevel_paths:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **toplevel_paths** = ``PackedStringArray()`` :ref:`🔗<class_OpenXRAction_property_toplevel_paths>`

.. rst-class:: classref-property-setget

- |void| **set_toplevel_paths**\ (\ value\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) - :ref:`PackedStringArray<class_PackedStringArray>` **get_toplevel_paths**\ (\ )

Một tập hợp các đường dẫn cấp cao nhất mà action này có thể được liên kết với.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
