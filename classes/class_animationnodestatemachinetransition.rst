:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeStateMachineTransition.xml.

.. _class_AnimationNodeStateMachineTransition:

AnimationNodeStateMachineTransition
===================================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A transition within an :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` connecting two :ref:`AnimationRootNode<class_AnimationRootNode>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đường dẫn được tạo khi sử dụng :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>` chỉ giới hạn ở các node được kết nối bởi **AnimationNodeStateMachineTransition**.

Bạn có thể thiết lập chi tiết thời gian và điều kiện của transition.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`StringName<class_StringName>`                                      | :ref:`advance_condition<class_AnimationNodeStateMachineTransition_property_advance_condition>`   | ``&""``   |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`                                              | :ref:`advance_expression<class_AnimationNodeStateMachineTransition_property_advance_expression>` | ``""``    |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` | :ref:`advance_mode<class_AnimationNodeStateMachineTransition_property_advance_mode>`             | ``1``     |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                  | :ref:`break_loop_at_end<class_AnimationNodeStateMachineTransition_property_break_loop_at_end>`   | ``false`` |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                                    | :ref:`priority<class_AnimationNodeStateMachineTransition_property_priority>`                     | ``1``     |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                  | :ref:`reset<class_AnimationNodeStateMachineTransition_property_reset>`                           | ``true``  |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>`   | :ref:`switch_mode<class_AnimationNodeStateMachineTransition_property_switch_mode>`               | ``0``     |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`Curve<class_Curve>`                                                | :ref:`xfade_curve<class_AnimationNodeStateMachineTransition_property_xfade_curve>`               |           |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                                                | :ref:`xfade_time<class_AnimationNodeStateMachineTransition_property_xfade_time>`                 | ``0.0``   |
   +--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_AnimationNodeStateMachineTransition_signal_advance_condition_changed:

.. rst-class:: classref-signal

**advance_condition_changed**\ (\ ) :ref:`🔗<class_AnimationNodeStateMachineTransition_signal_advance_condition_changed>`

Được phát ra khi :ref:`advance_condition<class_AnimationNodeStateMachineTransition_property_advance_condition>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationNodeStateMachineTransition_SwitchMode:

.. rst-class:: classref-enumeration

enum **SwitchMode**: :ref:`🔗<enum_AnimationNodeStateMachineTransition_SwitchMode>`

.. _class_AnimationNodeStateMachineTransition_constant_SWITCH_MODE_IMMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>` **SWITCH_MODE_IMMEDIATE** = ``0``

Chuyển sang state tiếp theo ngay lập tức. State hiện tại sẽ kết thúc và blend vào phần đầu của state mới.

.. _class_AnimationNodeStateMachineTransition_constant_SWITCH_MODE_SYNC:

.. rst-class:: classref-enumeration-constant

:ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>` **SWITCH_MODE_SYNC** = ``1``

Chuyển sang state tiếp theo ngay lập tức, nhưng sẽ seek state mới đến vị trí playback của state cũ.

.. _class_AnimationNodeStateMachineTransition_constant_SWITCH_MODE_AT_END:

.. rst-class:: classref-enumeration-constant

:ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>` **SWITCH_MODE_AT_END** = ``2``

Chờ playback của state hiện tại kết thúc, sau đó chuyển đến phần đầu của animation state tiếp theo.

.. rst-class:: classref-item-separator

----

.. _enum_AnimationNodeStateMachineTransition_AdvanceMode:

.. rst-class:: classref-enumeration

enum **AdvanceMode**: :ref:`🔗<enum_AnimationNodeStateMachineTransition_AdvanceMode>`

.. _class_AnimationNodeStateMachineTransition_constant_ADVANCE_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` **ADVANCE_MODE_DISABLED** = ``0``

Không sử dụng transition này.

.. _class_AnimationNodeStateMachineTransition_constant_ADVANCE_MODE_ENABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` **ADVANCE_MODE_ENABLED** = ``1``

Chỉ sử dụng transition này trong :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>`.

.. _class_AnimationNodeStateMachineTransition_constant_ADVANCE_MODE_AUTO:

.. rst-class:: classref-enumeration-constant

:ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` **ADVANCE_MODE_AUTO** = ``2``

Tự động sử dụng transition này nếu các kiểm tra :ref:`advance_condition<class_AnimationNodeStateMachineTransition_property_advance_condition>` và :ref:`advance_expression<class_AnimationNodeStateMachineTransition_property_advance_expression>` là ``true`` (nếu được gán).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeStateMachineTransition_property_advance_condition:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **advance_condition** = ``&""`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_advance_condition>`

.. rst-class:: classref-property-setget

- |void| **set_advance_condition**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_advance_condition**\ (\ )

Bật auto advance khi điều kiện này được thiết lập. Tên được cung cấp sẽ trở thành một tham số boolean trên :ref:`AnimationTree<class_AnimationTree>` mà bạn có thể điều khiển từ code (xem `Using AnimationTree <../tutorials/animation/animation_tree.html#controlling-from-code>`__). Ví dụ, nếu :ref:`AnimationTree.tree_root<class_AnimationTree_property_tree_root>` là một :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` và :ref:`advance_condition<class_AnimationNodeStateMachineTransition_property_advance_condition>` được đặt thành ``"idle"``:


.. tabs::

 .. code-tab:: gdscript

    $animation_tree.set("parameters/conditions/idle", is_on_floor and (linear_velocity.x == 0))

 .. code-tab:: csharp

    GetNode<AnimationTree>("animation_tree").Set("parameters/conditions/idle", IsOnFloor && (LinearVelocity.X == 0));



.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_advance_expression:

.. rst-class:: classref-property

:ref:`String<class_String>` **advance_expression** = ``""`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_advance_expression>`

.. rst-class:: classref-property-setget

- |void| **set_advance_expression**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_advance_expression**\ (\ )

Sử dụng một expression làm điều kiện cho các transition của state machine. Bạn có thể tạo các điều kiện advance animation phức tạp để chuyển đổi giữa các state, đồng thời có được nhiều tính linh hoạt hơn khi tạo các state machine phức tạp bằng cách giao tiếp trực tiếp với script code.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_advance_mode:

.. rst-class:: classref-property

:ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` **advance_mode** = ``1`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_advance_mode>`

.. rst-class:: classref-property-setget

- |void| **set_advance_mode**\ (\ value\: :ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>`\ ) - :ref:`AdvanceMode<enum_AnimationNodeStateMachineTransition_AdvanceMode>` **get_advance_mode**\ (\ )

Xác định transition sẽ bị vô hiệu hóa, được bật khi sử dụng :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>`, hay được tự động đi qua nếu các kiểm tra :ref:`advance_condition<class_AnimationNodeStateMachineTransition_property_advance_condition>` và :ref:`advance_expression<class_AnimationNodeStateMachineTransition_property_advance_expression>` là ``true`` (nếu được gán).

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_break_loop_at_end:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **break_loop_at_end** = ``false`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_break_loop_at_end>`

.. rst-class:: classref-property-setget

- |void| **set_break_loop_at_end**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_loop_broken_at_end**\ (\ )

Nếu ``true``, ngắt loop ở cuối chu kỳ loop cho transition, ngay cả khi animation đang loop.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **priority** = ``1`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_priority>`

.. rst-class:: classref-property-setget

- |void| **set_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_priority**\ (\ )

Các transition có priority thấp hơn sẽ được ưu tiên khi di chuyển qua tree bằng :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>` hoặc :ref:`advance_mode<class_AnimationNodeStateMachineTransition_property_advance_mode>` được đặt thành :ref:`ADVANCE_MODE_AUTO<class_AnimationNodeStateMachineTransition_constant_ADVANCE_MODE_AUTO>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_reset:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **reset** = ``true`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_reset>`

.. rst-class:: classref-property-setget

- |void| **set_reset**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_reset**\ (\ )

Nếu ``true``, animation đích sẽ được playback từ đầu khi chuyển đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_switch_mode:

.. rst-class:: classref-property

:ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>` **switch_mode** = ``0`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_switch_mode>`

.. rst-class:: classref-property-setget

- |void| **set_switch_mode**\ (\ value\: :ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>`\ ) - :ref:`SwitchMode<enum_AnimationNodeStateMachineTransition_SwitchMode>` **get_switch_mode**\ (\ )

Kiểu transition.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_xfade_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **xfade_curve** :ref:`🔗<class_AnimationNodeStateMachineTransition_property_xfade_curve>`

.. rst-class:: classref-property-setget

- |void| **set_xfade_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_xfade_curve**\ (\ )

Đường cong ease để kiểm soát tốt hơn quá trình cross-fade giữa state này và state tiếp theo. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachineTransition_property_xfade_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **xfade_time** = ``0.0`` :ref:`🔗<class_AnimationNodeStateMachineTransition_property_xfade_time>`

.. rst-class:: classref-property-setget

- |void| **set_xfade_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_xfade_time**\ (\ )

Thời gian để cross-fade giữa state này và state tiếp theo.

\ **Lưu ý:** :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` chuyển state hiện tại ngay sau khi bắt đầu fading. Thời gian còn lại chính xác chỉ có thể được suy ra từ animation chính. Khi :ref:`AnimationNodeOutput<class_AnimationNodeOutput>` được xem là upstream nhất, :ref:`xfade_time<class_AnimationNodeStateMachineTransition_property_xfade_time>` sẽ không được scale tùy theo delta downstream. Xem thêm :ref:`AnimationNodeOneShot.fadeout_time<class_AnimationNodeOneShot_property_fadeout_time>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
