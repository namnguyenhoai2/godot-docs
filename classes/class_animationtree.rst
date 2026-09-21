:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationTree.xml.

.. _class_AnimationTree:

AnimationTree
=============

**Kế thừa:** :ref:`AnimationMixer<class_AnimationMixer>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node được sử dụng cho các chuyển tiếp animation nâng cao trong một :ref:`AnimationPlayer<class_AnimationPlayer>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node được sử dụng cho các chuyển tiếp animation nâng cao trong một :ref:`AnimationPlayer<class_AnimationPlayer>`.

\ **Note:** When linked with an :ref:`AnimationPlayer<class_AnimationPlayer>`, several properties and methods of the corresponding :ref:`AnimationPlayer<class_AnimationPlayer>` will not function as expected. Playback and transitions should be handled using only the **AnimationTree** and its constituent :ref:`AnimationNode<class_AnimationNode>`\ (s). The :ref:`AnimationPlayer<class_AnimationPlayer>` node should be used solely for adding, deleting, and editing animations.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                                         | :ref:`advance_expression_base_node<class_AnimationTree_property_advance_expression_base_node>` | ``NodePath(".")``                                                                             |
   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                                         | :ref:`anim_player<class_AnimationTree_property_anim_player>`                                   | ``NodePath("")``                                                                              |
   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` | callback_mode_discrete                                                                         | ``2`` (overrides :ref:`AnimationMixer<class_AnimationMixer_property_callback_mode_discrete>`) |
   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                                 | deterministic                                                                                  | ``true`` (overrides :ref:`AnimationMixer<class_AnimationMixer_property_deterministic>`)       |
   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`AnimationRootNode<class_AnimationRootNode>`                                       | :ref:`tree_root<class_AnimationTree_property_tree_root>`                                       |                                                                                               |
   +-----------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>` | :ref:`get_process_callback<class_AnimationTree_method_get_process_callback>`\ (\ ) |const|                                                                              |
   +------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                       | :ref:`set_process_callback<class_AnimationTree_method_set_process_callback>`\ (\ mode\: :ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>`\ ) |
   +------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AnimationTree_signal_animation_player_changed:

.. rst-class:: classref-signal

**animation_player_changed**\ (\ ) :ref:`🔗<class_AnimationTree_signal_animation_player_changed>`

Được phát ra khi :ref:`anim_player<class_AnimationTree_property_anim_player>` được thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_AnimationTree_AnimationProcessCallback:

.. rst-class:: classref-enumeration

enum **AnimationProcessCallback**: :ref:`🔗<enum_AnimationTree_AnimationProcessCallback>`

.. _class_AnimationTree_constant_ANIMATION_PROCESS_PHYSICS:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>` **ANIMATION_PROCESS_PHYSICS** = ``0``

**Không dùng nữa:** Xem :ref:`AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS>`.



.. _class_AnimationTree_constant_ANIMATION_PROCESS_IDLE:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>` **ANIMATION_PROCESS_IDLE** = ``1``

**Không dùng nữa:** Xem :ref:`AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_IDLE<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_IDLE>`.



.. _class_AnimationTree_constant_ANIMATION_PROCESS_MANUAL:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>` **ANIMATION_PROCESS_MANUAL** = ``2``

**Không dùng nữa:** Xem :ref:`AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_MANUAL<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_MANUAL>`.



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationTree_property_advance_expression_base_node:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **advance_expression_base_node** = ``NodePath(".")`` :ref:`🔗<class_AnimationTree_property_advance_expression_base_node>`

.. rst-class:: classref-property-setget

- |void| **set_advance_expression_base_node**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_advance_expression_base_node**\ (\ )

Đường dẫn đến :ref:`Node<class_Node>` được sử dụng để đánh giá :ref:`AnimationNode<class_AnimationNode>` :ref:`Expression<class_Expression>` nếu không được chỉ định rõ ràng ở bên trong.

.. rst-class:: classref-item-separator

----

.. _class_AnimationTree_property_anim_player:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **anim_player** = ``NodePath("")`` :ref:`🔗<class_AnimationTree_property_anim_player>`

.. rst-class:: classref-property-setget

- |void| **set_animation_player**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_animation_player**\ (\ )

Đường dẫn đến :ref:`AnimationPlayer<class_AnimationPlayer>` được sử dụng để tạo animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationTree_property_tree_root:

.. rst-class:: classref-property

:ref:`AnimationRootNode<class_AnimationRootNode>` **tree_root** :ref:`🔗<class_AnimationTree_property_tree_root>`

.. rst-class:: classref-property-setget

- |void| **set_tree_root**\ (\ value\: :ref:`AnimationRootNode<class_AnimationRootNode>`\ ) - :ref:`AnimationRootNode<class_AnimationRootNode>` **get_tree_root**\ (\ )

Node animation gốc của **AnimationTree** này. Xem :ref:`AnimationRootNode<class_AnimationRootNode>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationTree_method_get_process_callback:

.. rst-class:: classref-method

:ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>` **get_process_callback**\ (\ ) |const| :ref:`🔗<class_AnimationTree_method_get_process_callback>`

**Không dùng nữa:** Thay vào đó, hãy sử dụng :ref:`AnimationMixer.callback_mode_process<class_AnimationMixer_property_callback_mode_process>`.

Trả về thông báo process mà tại đó cần cập nhật animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationTree_method_set_process_callback:

.. rst-class:: classref-method

|void| **set_process_callback**\ (\ mode\: :ref:`AnimationProcessCallback<enum_AnimationTree_AnimationProcessCallback>`\ ) :ref:`🔗<class_AnimationTree_method_set_process_callback>`

**Không dùng nữa:** Thay vào đó, hãy sử dụng :ref:`AnimationMixer.callback_mode_process<class_AnimationMixer_property_callback_mode_process>`.

Thiết lập thông báo process mà tại đó cần cập nhật animation.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
