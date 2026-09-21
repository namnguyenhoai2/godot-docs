:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeStateMachine.xml.

.. _class_AnimationNodeStateMachine:

AnimationNodeStateMachine
=========================

**Kế thừa:** :ref:`AnimationRootNode<class_AnimationRootNode>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A state machine with multiple :ref:`AnimationRootNode<class_AnimationRootNode>`\ s, used by :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Contains multiple :ref:`AnimationRootNode<class_AnimationRootNode>`\ s representing animation states, connected in a graph. State transitions can be configured to happen automatically or via code, using a shortest-path algorithm. Retrieve the :ref:`AnimationNodeStateMachinePlayback<class_AnimationNodeStateMachinePlayback>` object from the :ref:`AnimationTree<class_AnimationTree>` node to control it programmatically.


.. tabs::

 .. code-tab:: gdscript

    var state_machine = $AnimationTree.get("parameters/playback")
    state_machine.travel("some_state")

 .. code-tab:: csharp

    var stateMachine = GetNode<AnimationTree>("AnimationTree").Get("parameters/playback") as AnimationNodeStateMachinePlayback;
    stateMachine.Travel("some_state");



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                  | :ref:`allow_transition_to_self<class_AnimationNodeStateMachine_property_allow_transition_to_self>` | ``false`` |
   +--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                  | :ref:`reset_ends<class_AnimationNodeStateMachine_property_reset_ends>`                             | ``false`` |
   +--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------+
   | :ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` | :ref:`state_machine_type<class_AnimationNodeStateMachine_property_state_machine_type>`             | ``0``     |
   +--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`add_node<class_AnimationNodeStateMachine_method_add_node>`\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ )                                               |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`add_transition<class_AnimationNodeStateMachine_method_add_transition>`\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`, transition\: :ref:`AnimationNodeStateMachineTransition<class_AnimationNodeStateMachineTransition>`\ ) |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                         | :ref:`get_graph_offset<class_AnimationNodeStateMachine_method_get_graph_offset>`\ (\ ) |const|                                                                                                                                                                               |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationNode<class_AnimationNode>`                                             | :ref:`get_node<class_AnimationNodeStateMachine_method_get_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                   |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\]                      | :ref:`get_node_list<class_AnimationNodeStateMachine_method_get_node_list>`\ (\ ) |const|                                                                                                                                                                                     |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                                   | :ref:`get_node_name<class_AnimationNodeStateMachine_method_get_node_name>`\ (\ node\: :ref:`AnimationNode<class_AnimationNode>`\ ) |const|                                                                                                                                   |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                         | :ref:`get_node_position<class_AnimationNodeStateMachine_method_get_node_position>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                 |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationNodeStateMachineTransition<class_AnimationNodeStateMachineTransition>` | :ref:`get_transition<class_AnimationNodeStateMachine_method_get_transition>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                      |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                                 | :ref:`get_transition_count<class_AnimationNodeStateMachine_method_get_transition_count>`\ (\ ) |const|                                                                                                                                                                       |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                                   | :ref:`get_transition_from<class_AnimationNodeStateMachine_method_get_transition_from>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                            |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                                   | :ref:`get_transition_to<class_AnimationNodeStateMachine_method_get_transition_to>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                               | :ref:`has_node<class_AnimationNodeStateMachine_method_has_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                   |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                               | :ref:`has_transition<class_AnimationNodeStateMachine_method_has_transition>`\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                             |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`remove_node<class_AnimationNodeStateMachine_method_remove_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                     |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`remove_transition<class_AnimationNodeStateMachine_method_remove_transition>`\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`\ )                                                                                               |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`remove_transition_by_index<class_AnimationNodeStateMachine_method_remove_transition_by_index>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                                                                                      |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`rename_node<class_AnimationNodeStateMachine_method_rename_node>`\ (\ name\: :ref:`StringName<class_StringName>`, new_name\: :ref:`StringName<class_StringName>`\ )                                                                                                     |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`replace_node<class_AnimationNodeStateMachine_method_replace_node>`\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`\ )                                                                                                 |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`set_graph_offset<class_AnimationNodeStateMachine_method_set_graph_offset>`\ (\ offset\: :ref:`Vector2<class_Vector2>`\ )                                                                                                                                               |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                                | :ref:`set_node_position<class_AnimationNodeStateMachine_method_set_node_position>`\ (\ name\: :ref:`StringName<class_StringName>`, position\: :ref:`Vector2<class_Vector2>`\ )                                                                                               |
   +---------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationNodeStateMachine_StateMachineType:

.. rst-class:: classref-enumeration

enum **StateMachineType**: :ref:`🔗<enum_AnimationNodeStateMachine_StateMachineType>`

.. _class_AnimationNodeStateMachine_constant_STATE_MACHINE_TYPE_ROOT:

.. rst-class:: classref-enumeration-constant

:ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` **STATE_MACHINE_TYPE_ROOT** = ``0``

Việc seek đến đầu được xem như phát từ trạng thái bắt đầu. Việc chuyển sang trạng thái kết thúc được xem như thoát khỏi state machine.

.. _class_AnimationNodeStateMachine_constant_STATE_MACHINE_TYPE_NESTED:

.. rst-class:: classref-enumeration-constant

:ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` **STATE_MACHINE_TYPE_NESTED** = ``1``

Việc seek đến đầu được xem như seek đến đầu animation trong trạng thái hiện tại. Việc chuyển sang trạng thái kết thúc, hoặc không có chuyển đổi trong từng trạng thái, được xem như thoát khỏi state machine.

.. _class_AnimationNodeStateMachine_constant_STATE_MACHINE_TYPE_GROUPED:

.. rst-class:: classref-enumeration-constant

:ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` **STATE_MACHINE_TYPE_GROUPED** = ``2``

Đây là một state machine được nhóm, có thể được điều khiển từ một state machine cha. Nó không hoạt động độc lập. Trong node cha hoặc node tổ tiên phải có một state machine với :ref:`state_machine_type<class_AnimationNodeStateMachine_property_state_machine_type>` là :ref:`STATE_MACHINE_TYPE_ROOT<class_AnimationNodeStateMachine_constant_STATE_MACHINE_TYPE_ROOT>` hoặc :ref:`STATE_MACHINE_TYPE_NESTED<class_AnimationNodeStateMachine_constant_STATE_MACHINE_TYPE_NESTED>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeStateMachine_property_allow_transition_to_self:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **allow_transition_to_self** = ``false`` :ref:`🔗<class_AnimationNodeStateMachine_property_allow_transition_to_self>`

.. rst-class:: classref-property-setget

- |void| **set_allow_transition_to_self**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_allow_transition_to_self**\ (\ )

Nếu ``true``, cho phép teleport đến trạng thái self bằng :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>`. Khi tùy chọn reset được bật trong :ref:`AnimationNodeStateMachinePlayback.travel()<class_AnimationNodeStateMachinePlayback_method_travel>`, animation sẽ được khởi động lại. Nếu ``false``, sẽ không có gì xảy ra khi teleport đến trạng thái self.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_property_reset_ends:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **reset_ends** = ``false`` :ref:`🔗<class_AnimationNodeStateMachine_property_reset_ends>`

.. rst-class:: classref-property-setget

- |void| **set_reset_ends**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **are_ends_reset**\ (\ )

Nếu ``true``, xem cross-fade đến các node bắt đầu và kết thúc như một blend với animation RESET.

Trong hầu hết trường hợp, khi thực hiện thêm các cross-fade trong :ref:`AnimationNode<class_AnimationNode>` cha của state machine, việc đặt thuộc tính này thành ``false`` và khớp thời gian cross-fade của :ref:`AnimationNode<class_AnimationNode>` cha với node bắt đầu và node kết thúc của state machine sẽ cho kết quả tốt.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_property_state_machine_type:

.. rst-class:: classref-property

:ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` **state_machine_type** = ``0`` :ref:`🔗<class_AnimationNodeStateMachine_property_state_machine_type>`

.. rst-class:: classref-property-setget

- |void| **set_state_machine_type**\ (\ value\: :ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>`\ ) - :ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>` **get_state_machine_type**\ (\ )

Thuộc tính này có thể xác định quy trình chuyển đổi cho các trường hợp sử dụng khác nhau. Xem thêm :ref:`StateMachineType<enum_AnimationNodeStateMachine_StateMachineType>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeStateMachine_method_add_node:

.. rst-class:: classref-method

|void| **add_node**\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_add_node>`

Thêm một node animation mới vào graph. ``position`` được dùng để hiển thị trong editor.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_add_transition:

.. rst-class:: classref-method

|void| **add_transition**\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`, transition\: :ref:`AnimationNodeStateMachineTransition<class_AnimationNodeStateMachineTransition>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_add_transition>`

Thêm một transition giữa các node animation đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_graph_offset:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_graph_offset**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_graph_offset>`

Trả về draw offset của graph. Được dùng để hiển thị trong editor.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_node:

.. rst-class:: classref-method

:ref:`AnimationNode<class_AnimationNode>` **get_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_node>`

Trả về node animation có tên đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_node_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_node_list**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_node_list>`

Trả về danh sách chứa tên của tất cả node animation trong state machine này.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_node_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_node_name**\ (\ node\: :ref:`AnimationNode<class_AnimationNode>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_node_name>`

Trả về tên của node animation đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_node_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_node_position**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_node_position>`

Trả về tọa độ của node animation đã cho. Được dùng để hiển thị trong editor.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_transition:

.. rst-class:: classref-method

:ref:`AnimationNodeStateMachineTransition<class_AnimationNodeStateMachineTransition>` **get_transition**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_transition>`

Trả về transition đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_transition_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_transition_count**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_transition_count>`

Trả về số lượng kết nối trong graph.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_transition_from:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_transition_from**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_transition_from>`

Trả về node bắt đầu của transition đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_get_transition_to:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_transition_to**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_get_transition_to>`

Trả về node kết thúc của transition đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_has_node:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_has_node>`

Trả về ``true`` nếu graph chứa node animation đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_has_transition:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_transition**\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeStateMachine_method_has_transition>`

Trả về ``true`` nếu có transition giữa các node animation đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_remove_node:

.. rst-class:: classref-method

|void| **remove_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_remove_node>`

Xóa node animation đã cho khỏi graph.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_remove_transition:

.. rst-class:: classref-method

|void| **remove_transition**\ (\ from\: :ref:`StringName<class_StringName>`, to\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_remove_transition>`

Xóa transition giữa hai node animation được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_remove_transition_by_index:

.. rst-class:: classref-method

|void| **remove_transition_by_index**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_remove_transition_by_index>`

Xóa transition đã cho theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_rename_node:

.. rst-class:: classref-method

|void| **rename_node**\ (\ name\: :ref:`StringName<class_StringName>`, new_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_rename_node>`

Đổi tên node animation đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_replace_node:

.. rst-class:: classref-method

|void| **replace_node**\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_replace_node>`

Thay thế node animation đã cho bằng một node animation mới.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_set_graph_offset:

.. rst-class:: classref-method

|void| **set_graph_offset**\ (\ offset\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_set_graph_offset>`

Thiết lập draw offset của graph. Được dùng để hiển thị trong editor.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachine_method_set_node_position:

.. rst-class:: classref-method

|void| **set_node_position**\ (\ name\: :ref:`StringName<class_StringName>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_AnimationNodeStateMachine_method_set_node_position>`

Thiết lập tọa độ của node animation. Được dùng để hiển thị trong editor.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
