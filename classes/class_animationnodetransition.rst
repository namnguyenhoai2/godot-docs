:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeTransition.xml.

.. _class_AnimationNodeTransition:

AnimationNodeTransition
=======================

**Kế thừa:** :ref:`AnimationNodeSync<class_AnimationNodeSync>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A transition within an :ref:`AnimationTree<class_AnimationTree>` connecting two :ref:`AnimationNode<class_AnimationNode>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Máy trạng thái đơn giản dành cho các trường hợp không yêu cầu :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` nâng cao hơn. Có thể kết nối các animation với những đầu vào và chỉ định thời gian chuyển tiếp.

Sau khi thiết lập request và thay đổi quá trình phát animation, transition node sẽ tự động xóa request ở frame xử lý tiếp theo bằng cách đặt giá trị ``transition_request`` thành rỗng.

\ **Lưu ý:** Khi sử dụng cross-fade, ``current_state`` và ``current_index`` sẽ thay đổi sang state tiếp theo ngay sau khi cross-fade bắt đầu.


.. tabs::

 .. code-tab:: gdscript

    # Phát child animation được kết nối với cổng "state_2".
    animation_tree.set("parameters/Transition/transition_request", "state_2")
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/Transition/transition_request"] = "state_2"

    # Lấy tên state hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_state")
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/Transition/current_state"]

    # Lấy chỉ mục state hiện tại (chỉ đọc).
    animation_tree.get("parameters/Transition/current_index")
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/Transition/current_index"]

 .. code-tab:: csharp

    // Phát child animation được kết nối với cổng "state_2".
    animationTree.Set("parameters/Transition/transition_request", "state_2");

    // Lấy tên state hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_state");

    // Lấy chỉ mục state hiện tại (chỉ đọc).
    animationTree.Get("parameters/Transition/current_index");



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`allow_transition_to_self<class_AnimationNodeTransition_property_allow_transition_to_self>` | ``false`` |
   +---------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`     | :ref:`input_count<class_AnimationNodeTransition_property_input_count>`                           | ``0``     |
   +---------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`Curve<class_Curve>` | :ref:`xfade_curve<class_AnimationNodeTransition_property_xfade_curve>`                           |           |
   +---------------------------+--------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`xfade_time<class_AnimationNodeTransition_property_xfade_time>`                             | ``0.0``   |
   +---------------------------+--------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_input_loop_broken_at_end<class_AnimationNodeTransition_method_is_input_loop_broken_at_end>`\ (\ input\: :ref:`int<class_int>`\ ) |const|                           |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_input_reset<class_AnimationNodeTransition_method_is_input_reset>`\ (\ input\: :ref:`int<class_int>`\ ) |const|                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_input_set_as_auto_advance<class_AnimationNodeTransition_method_is_input_set_as_auto_advance>`\ (\ input\: :ref:`int<class_int>`\ ) |const|                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_input_as_auto_advance<class_AnimationNodeTransition_method_set_input_as_auto_advance>`\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_input_break_loop_at_end<class_AnimationNodeTransition_method_set_input_break_loop_at_end>`\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_input_reset<class_AnimationNodeTransition_method_set_input_reset>`\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeTransition_property_allow_transition_to_self:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **allow_transition_to_self** = ``false`` :ref:`🔗<class_AnimationNodeTransition_property_allow_transition_to_self>`

.. rst-class:: classref-property-setget

- |void| **set_allow_transition_to_self**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_allow_transition_to_self**\ (\ )

Nếu ``true``, cho phép chuyển tiếp đến state hiện tại. Khi tùy chọn reset được bật ở đầu vào, animation sẽ được phát lại từ đầu. Nếu ``false``, sẽ không có gì xảy ra khi chuyển tiếp đến state hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_property_input_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **input_count** = ``0`` :ref:`🔗<class_AnimationNodeTransition_property_input_count>`

.. rst-class:: classref-property-setget

- |void| **set_input_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_input_count**\ (\ )

Số lượng cổng đầu vào được bật cho animation node này.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_property_xfade_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **xfade_curve** :ref:`🔗<class_AnimationNodeTransition_property_xfade_curve>`

.. rst-class:: classref-property-setget

- |void| **set_xfade_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_xfade_curve**\ (\ )

Xác định cách làm mượt quá trình cross-fade giữa các animation. Nếu rỗng, quá trình chuyển tiếp sẽ là tuyến tính. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_property_xfade_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **xfade_time** = ``0.0`` :ref:`🔗<class_AnimationNodeTransition_property_xfade_time>`

.. rst-class:: classref-property-setget

- |void| **set_xfade_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_xfade_time**\ (\ )

Thời gian cross-fade (tính bằng giây) giữa mỗi animation được kết nối với các đầu vào.

\ **Lưu ý:** **AnimationNodeTransition** chuyển state hiện tại ngay sau khi bắt đầu fade. Thời gian còn lại chính xác chỉ có thể được suy ra từ animation chính. Khi :ref:`AnimationNodeOutput<class_AnimationNodeOutput>` được xem là upstream nhất, :ref:`xfade_time<class_AnimationNodeTransition_property_xfade_time>` sẽ không được scale tùy theo delta downstream. Xem thêm :ref:`AnimationNodeOneShot.fadeout_time<class_AnimationNodeOneShot_property_fadeout_time>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeTransition_method_is_input_loop_broken_at_end:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_input_loop_broken_at_end**\ (\ input\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeTransition_method_is_input_loop_broken_at_end>`

Trả về liệu animation có ngắt loop ở cuối chu kỳ loop để chuyển tiếp hay không.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_method_is_input_reset:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_input_reset**\ (\ input\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeTransition_method_is_input_reset>`

Trả về liệu animation có khởi động lại khi animation chuyển tiếp từ animation khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_method_is_input_set_as_auto_advance:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_input_set_as_auto_advance**\ (\ input\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeTransition_method_is_input_set_as_auto_advance>`

Trả về ``true`` nếu auto-advance được bật cho ``input`` index đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_method_set_input_as_auto_advance:

.. rst-class:: classref-method

|void| **set_input_as_auto_advance**\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AnimationNodeTransition_method_set_input_as_auto_advance>`

Bật hoặc tắt auto-advance cho ``input`` index đã cho. Nếu được bật, state sẽ chuyển sang input tiếp theo sau khi phát animation một lần. Nếu được bật cho state input cuối cùng, nó sẽ lặp về input đầu tiên.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_method_set_input_break_loop_at_end:

.. rst-class:: classref-method

|void| **set_input_break_loop_at_end**\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AnimationNodeTransition_method_set_input_break_loop_at_end>`

Nếu ``true``, ngắt loop ở cuối chu kỳ loop để chuyển tiếp, ngay cả khi animation đang loop.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeTransition_method_set_input_reset:

.. rst-class:: classref-method

|void| **set_input_reset**\ (\ input\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AnimationNodeTransition_method_set_input_reset>`

Nếu ``true``, animation đích sẽ được khởi động lại khi animation chuyển tiếp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
