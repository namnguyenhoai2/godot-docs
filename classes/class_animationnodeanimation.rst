:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeAnimation.xml.

.. _class_AnimationNodeAnimation:

AnimationNodeAnimation
======================

**Kế thừa:** :ref:`AnimationRootNode<class_AnimationRootNode>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một animation đầu vào cho :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

A resource to add to an :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Only has one output port using the :ref:`animation<class_AnimationNodeAnimation_property_animation>` property. Used as an input for :ref:`AnimationNode<class_AnimationNode>`\ s that blend animations together.

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

   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                               | :ref:`advance_on_start<class_AnimationNodeAnimation_property_advance_on_start>`       | ``false`` |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`StringName<class_StringName>`                   | :ref:`animation<class_AnimationNodeAnimation_property_animation>`                     | ``&""``   |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`LoopMode<enum_Animation_LoopMode>`              | :ref:`loop_mode<class_AnimationNodeAnimation_property_loop_mode>`                     |           |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>` | :ref:`play_mode<class_AnimationNodeAnimation_property_play_mode>`                     | ``0``     |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`start_offset<class_AnimationNodeAnimation_property_start_offset>`               |           |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                               | :ref:`stretch_time_scale<class_AnimationNodeAnimation_property_stretch_time_scale>`   |           |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`timeline_length<class_AnimationNodeAnimation_property_timeline_length>`         |           |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                               | :ref:`use_custom_timeline<class_AnimationNodeAnimation_property_use_custom_timeline>` | ``false`` |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationNodeAnimation_PlayMode:

.. rst-class:: classref-enumeration

enum **PlayMode**: :ref:`🔗<enum_AnimationNodeAnimation_PlayMode>`

.. _class_AnimationNodeAnimation_constant_PLAY_MODE_FORWARD:

.. rst-class:: classref-enumeration-constant

:ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>` **PLAY_MODE_FORWARD** = ``0``

Phát animation theo hướng tiến.

.. _class_AnimationNodeAnimation_constant_PLAY_MODE_BACKWARD:

.. rst-class:: classref-enumeration-constant

:ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>` **PLAY_MODE_BACKWARD** = ``1``

Phát animation theo hướng lùi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeAnimation_property_advance_on_start:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **advance_on_start** = ``false`` :ref:`🔗<class_AnimationNodeAnimation_property_advance_on_start>`

.. rst-class:: classref-property-setget

- |void| **set_advance_on_start**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_advance_on_start**\ (\ )

Nếu ``true``, khi nhận yêu cầu phát một animation từ đầu, frame đầu tiên sẽ không được hiển thị mà chỉ được xử lý, và quá trình phát bắt đầu từ frame tiếp theo.

Xem thêm ghi chú của :ref:`AnimationPlayer.play()<class_AnimationPlayer_method_play>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_animation:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **animation** = ``&""`` :ref:`🔗<class_AnimationNodeAnimation_property_animation>`

.. rst-class:: classref-property-setget

- |void| **set_animation**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_animation**\ (\ )

Animation được sử dụng làm đầu ra. Đây là một trong các animation do :ref:`AnimationTree.anim_player<class_AnimationTree_property_anim_player>` cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_loop_mode:

.. rst-class:: classref-property

:ref:`LoopMode<enum_Animation_LoopMode>` **loop_mode** :ref:`🔗<class_AnimationNodeAnimation_property_loop_mode>`

.. rst-class:: classref-property-setget

- |void| **set_loop_mode**\ (\ value\: :ref:`LoopMode<enum_Animation_LoopMode>`\ ) - :ref:`LoopMode<enum_Animation_LoopMode>` **get_loop_mode**\ (\ )

Nếu :ref:`use_custom_timeline<class_AnimationNodeAnimation_property_use_custom_timeline>` là ``true``, ghi đè thiết lập lặp của resource :ref:`Animation<class_Animation>` gốc bằng giá trị này.

\ **Lưu ý:** Nếu :ref:`Animation.loop_mode<class_Animation_property_loop_mode>` không được đặt ở chế độ lặp, tùy chọn :ref:`Animation.track_set_interpolation_loop_wrap()<class_Animation_method_track_set_interpolation_loop_wrap>` sẽ không được áp dụng. Nếu không đạt được hành vi mong muốn, hãy cân nhắc nhân bản resource :ref:`Animation<class_Animation>` và thay đổi thiết lập lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_play_mode:

.. rst-class:: classref-property

:ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>` **play_mode** = ``0`` :ref:`🔗<class_AnimationNodeAnimation_property_play_mode>`

.. rst-class:: classref-property-setget

- |void| **set_play_mode**\ (\ value\: :ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>`\ ) - :ref:`PlayMode<enum_AnimationNodeAnimation_PlayMode>` **get_play_mode**\ (\ )

Xác định hướng phát của animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_start_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **start_offset** :ref:`🔗<class_AnimationNodeAnimation_property_start_offset>`

.. rst-class:: classref-property-setget

- |void| **set_start_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_start_offset**\ (\ )

Nếu :ref:`use_custom_timeline<class_AnimationNodeAnimation_property_use_custom_timeline>` là ``true``, điều chỉnh vị trí bắt đầu của animation.

Điều này hữu ích để điều chỉnh chân nào bước trước trong các animation đi bộ 3D.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_stretch_time_scale:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **stretch_time_scale** :ref:`🔗<class_AnimationNodeAnimation_property_stretch_time_scale>`

.. rst-class:: classref-property-setget

- |void| **set_stretch_time_scale**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_stretching_time_scale**\ (\ )

Nếu ``true``, điều chỉnh tỷ lệ thời gian để độ dài được chỉ định trong :ref:`timeline_length<class_AnimationNodeAnimation_property_timeline_length>` tương ứng với một chu kỳ.

Điều này hữu ích để khớp chu kỳ của các animation đi bộ và chạy.

Nếu ``false``, độ dài animation gốc được giữ nguyên. Nếu đặt vòng lặp thành :ref:`loop_mode<class_AnimationNodeAnimation_property_loop_mode>`, animation sẽ lặp trong :ref:`timeline_length<class_AnimationNodeAnimation_property_timeline_length>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_timeline_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **timeline_length** :ref:`🔗<class_AnimationNodeAnimation_property_timeline_length>`

.. rst-class:: classref-property-setget

- |void| **set_timeline_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_timeline_length**\ (\ )

Độ dài của timeline tùy chỉnh.

Nếu :ref:`stretch_time_scale<class_AnimationNodeAnimation_property_stretch_time_scale>` là ``true``, điều chỉnh tỷ lệ animation theo độ dài này.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeAnimation_property_use_custom_timeline:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_custom_timeline** = ``false`` :ref:`🔗<class_AnimationNodeAnimation_property_use_custom_timeline>`

.. rst-class:: classref-property-setget

- |void| **set_use_custom_timeline**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_custom_timeline**\ (\ )

Nếu ``true``, :ref:`AnimationNode<class_AnimationNode>` cung cấp một animation dựa trên resource :ref:`Animation<class_Animation>` với một số tham số được điều chỉnh.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
