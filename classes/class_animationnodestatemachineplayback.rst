:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeStateMachinePlayback.xml.

.. _class_AnimationNodeStateMachinePlayback:

AnimationNodeStateMachinePlayback
=================================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp khả năng điều khiển playback cho một :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cho phép điều khiển các state machine :ref:`AnimationTree<class_AnimationTree>` được tạo bằng :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>`. Lấy đối tượng bằng ``$AnimationTree.get("parameters/playback")``.


.. tabs::

 .. code-tab:: gdscript

    var state_machine = $AnimationTree.get("parameters/playback")
    state_machine.travel("some_state")

 .. code-tab:: csharp

    var stateMachine = GetNode<AnimationTree>("AnimationTree").Get("parameters/playback").As<AnimationNodeStateMachinePlayback>();
    stateMachine.Travel("some_state");



.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+-------------------------+---------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | resource_local_to_scene | ``true`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------+-------------------------+---------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_current_length<class_AnimationNodeStateMachinePlayback_method_get_current_length>`\ (\ ) |const|                                                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                              | :ref:`get_current_node<class_AnimationNodeStateMachinePlayback_method_get_current_node>`\ (\ ) |const|                                                                        |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_current_play_position<class_AnimationNodeStateMachinePlayback_method_get_current_play_position>`\ (\ ) |const|                                                      |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_fading_from_length<class_AnimationNodeStateMachinePlayback_method_get_fading_from_length>`\ (\ ) |const|                                                            |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                              | :ref:`get_fading_from_node<class_AnimationNodeStateMachinePlayback_method_get_fading_from_node>`\ (\ ) |const|                                                                |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_fading_from_play_position<class_AnimationNodeStateMachinePlayback_method_get_fading_from_play_position>`\ (\ ) |const|                                              |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_fading_length<class_AnimationNodeStateMachinePlayback_method_get_fading_length>`\ (\ ) |const|                                                                      |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_fading_position<class_AnimationNodeStateMachinePlayback_method_get_fading_position>`\ (\ ) |const|                                                                  |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_travel_path<class_AnimationNodeStateMachinePlayback_method_get_travel_path>`\ (\ ) |const|                                                                          |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_playing<class_AnimationNodeStateMachinePlayback_method_is_playing>`\ (\ ) |const|                                                                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`next<class_AnimationNodeStateMachinePlayback_method_next>`\ (\ )                                                                                                        |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`start<class_AnimationNodeStateMachinePlayback_method_start>`\ (\ node\: :ref:`StringName<class_StringName>`, reset\: :ref:`bool<class_bool>` = true\ )                  |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`stop<class_AnimationNodeStateMachinePlayback_method_stop>`\ (\ )                                                                                                        |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`travel<class_AnimationNodeStateMachinePlayback_method_travel>`\ (\ to_node\: :ref:`StringName<class_StringName>`, reset_on_teleport\: :ref:`bool<class_bool>` = true\ ) |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_AnimationNodeStateMachinePlayback_signal_state_finished:

.. rst-class:: classref-signal

**state_finished**\ (\ state\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_signal_state_finished>`

Được phát khi ``state`` kết thúc playback. Nếu ``state`` là một state machine được đặt ở chế độ grouped, các signal của nó sẽ được truyền qua với tên của nó làm tiền tố.

Nếu có crossfade, signal này sẽ được phát khi ảnh hưởng của animation :ref:`get_fading_from_node()<class_AnimationNodeStateMachinePlayback_method_get_fading_from_node>` không còn nữa.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_signal_state_started:

.. rst-class:: classref-signal

**state_started**\ (\ state\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_signal_state_started>`

Được phát khi ``state`` bắt đầu playback. Nếu ``state`` là một state machine được đặt ở chế độ grouped, các signal của nó sẽ được truyền qua với tên của nó làm tiền tố.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeStateMachinePlayback_method_get_current_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_current_length**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_current_length>`

Trả về độ dài của state hiện tại.

\ **Lưu ý:** Có thể bất kỳ :ref:`AnimationRootNode<class_AnimationRootNode>` nào cũng là node chứ không chỉ là animation. Điều này có nghĩa là một state có thể chứa nhiều animation. Animation nào được ưu tiên về độ dài phụ thuộc vào các node được kết nối bên trong nó. Ngoài ra, nếu một transition không reset, độ dài còn lại tại thời điểm đó sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_current_node:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_current_node**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_current_node>`

Trả về state animation hiện đang phát.

\ **Lưu ý:** Khi sử dụng cross-fade, state hiện tại sẽ chuyển sang state tiếp theo ngay sau khi cross-fade bắt đầu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_current_play_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_current_play_position**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_current_play_position>`

Trả về vị trí playback trong state animation hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_fading_from_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_fading_from_length**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_fading_from_length>`

Trả về độ dài state playback của node từ :ref:`get_fading_from_node()<class_AnimationNodeStateMachinePlayback_method_get_fading_from_node>`. Trả về ``0`` nếu không có animation fade nào đang diễn ra.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_fading_from_node:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_fading_from_node**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_fading_from_node>`

Trả về state bắt đầu của animation hiện đang fade.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_fading_from_play_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_fading_from_play_position**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_fading_from_play_position>`

Trả về vị trí playback của node từ :ref:`get_fading_from_node()<class_AnimationNodeStateMachinePlayback_method_get_fading_from_node>`. Trả về ``0`` nếu không có animation fade nào đang diễn ra.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_fading_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_fading_length**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_fading_length>`

Trả về độ dài của animation fade hiện tại. Trả về ``0`` nếu không có animation fade nào đang diễn ra.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_fading_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_fading_position**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_fading_position>`

Trả về vị trí playback của animation fade hiện tại. Trả về ``0`` nếu không có animation fade nào đang diễn ra.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_get_travel_path:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_travel_path**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_get_travel_path>`

Trả về đường đi travel hiện tại theo tính toán nội bộ của thuật toán A\*.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_is_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_playing**\ (\ ) |const| :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_is_playing>`

Trả về ``true`` nếu một animation đang phát.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_next:

.. rst-class:: classref-method

|void| **next**\ (\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_next>`

Nếu có đường đi tiếp theo thông qua travel hoặc auto advance, ngay lập tức chuyển từ state hiện tại sang state tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_start:

.. rst-class:: classref-method

|void| **start**\ (\ node\: :ref:`StringName<class_StringName>`, reset\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_start>`

Bắt đầu phát animation đã cho.

Nếu ``reset`` là ``true``, animation sẽ được phát từ đầu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_stop>`

Dừng animation hiện đang phát.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeStateMachinePlayback_method_travel:

.. rst-class:: classref-method

|void| **travel**\ (\ to_node\: :ref:`StringName<class_StringName>`, reset_on_teleport\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AnimationNodeStateMachinePlayback_method_travel>`

Chuyển từ state hiện tại sang một state khác theo đường đi ngắn nhất.

Nếu đường đi không kết nối từ state hiện tại, animation sẽ phát sau khi state dịch chuyển tức thời.

Nếu ``reset_on_teleport`` là ``true``, animation sẽ được phát từ đầu khi travel gây ra việc dịch chuyển tức thời.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
