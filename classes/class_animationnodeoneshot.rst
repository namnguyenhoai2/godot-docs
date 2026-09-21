:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeOneShot.xml.

.. _class_AnimationNodeOneShot:

AnimationNodeOneShot
====================

**Kế thừa:** :ref:`AnimationNodeSync<class_AnimationNodeSync>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Phát một animation một lần trong :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource để thêm vào :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Animation node này sẽ thực thi một sub-animation và trả về khi hoàn tất. Có thể tùy chỉnh thời gian blend để fade in và fade out, cũng như các filter.

Sau khi thiết lập request và thay đổi việc phát animation, one-shot node sẽ tự động xóa request ở frame xử lý tiếp theo bằng cách đặt giá trị ``request`` thành :ref:`ONE_SHOT_REQUEST_NONE<class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_NONE>`.


.. tabs::

 .. code-tab:: gdscript

    # Phát child animation được kết nối với cổng "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE)
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FIRE

    # Hủy child animation được kết nối với cổng "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT)
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_ABORT

    # Hủy child animation với hiệu ứng fade out được kết nối với cổng "shot".
    animation_tree.set("parameters/OneShot/request", AnimationNodeOneShot.ONE_SHOT_REQUEST_FADE_OUT)
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/OneShot/request"] = AnimationNodeOneShot.ONE_SHOT_REQUEST_FADE_OUT

    # Lấy state hiện tại (chỉ đọc).
    animation_tree.get("parameters/OneShot/active")
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/OneShot/active"]

    # Lấy internal state hiện tại (chỉ đọc).
    animation_tree.get("parameters/OneShot/internal_active")
    # Cú pháp thay thế (cho cùng kết quả như trên).
    animation_tree["parameters/OneShot/internal_active"]

 .. code-tab:: csharp

    // Phát child animation được kết nối với cổng "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Fire);

    // Hủy child animation được kết nối với cổng "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.Abort);

    // Hủy child animation với hiệu ứng fade out được kết nối với cổng "shot".
    animationTree.Set("parameters/OneShot/request", (int)AnimationNodeOneShot.OneShotRequest.FadeOut);

    // Lấy state hiện tại (chỉ đọc).
    animationTree.Get("parameters/OneShot/active");

    // Lấy internal state hiện tại (chỉ đọc).
    animationTree.Get("parameters/OneShot/internal_active");



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`abort_on_reset<class_AnimationNodeOneShot_property_abort_on_reset>`                     | ``false`` |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`autorestart<class_AnimationNodeOneShot_property_autorestart>`                           | ``false`` |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`autorestart_delay<class_AnimationNodeOneShot_property_autorestart_delay>`               | ``1.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`autorestart_random_delay<class_AnimationNodeOneShot_property_autorestart_random_delay>` | ``0.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`break_loop_at_end<class_AnimationNodeOneShot_property_break_loop_at_end>`               | ``false`` |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`Curve<class_Curve>`                         | :ref:`fadein_curve<class_AnimationNodeOneShot_property_fadein_curve>`                         |           |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`fadein_time<class_AnimationNodeOneShot_property_fadein_time>`                           | ``0.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`Curve<class_Curve>`                         | :ref:`fadeout_curve<class_AnimationNodeOneShot_property_fadeout_curve>`                       |           |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`fadeout_time<class_AnimationNodeOneShot_property_fadeout_time>`                         | ``0.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+
   | :ref:`MixMode<enum_AnimationNodeOneShot_MixMode>` | :ref:`mix_mode<class_AnimationNodeOneShot_property_mix_mode>`                                 | ``0``     |
   +---------------------------------------------------+-----------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_AnimationNodeOneShot_OneShotRequest:

.. rst-class:: classref-enumeration

enum **OneShotRequest**: :ref:`🔗<enum_AnimationNodeOneShot_OneShotRequest>`

.. _class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`OneShotRequest<enum_AnimationNodeOneShot_OneShotRequest>` **ONE_SHOT_REQUEST_NONE** = ``0``

State mặc định của request. Không thực hiện gì.

.. _class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_FIRE:

.. rst-class:: classref-enumeration-constant

:ref:`OneShotRequest<enum_AnimationNodeOneShot_OneShotRequest>` **ONE_SHOT_REQUEST_FIRE** = ``1``

Request phát animation được kết nối với cổng "shot".

.. _class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_ABORT:

.. rst-class:: classref-enumeration-constant

:ref:`OneShotRequest<enum_AnimationNodeOneShot_OneShotRequest>` **ONE_SHOT_REQUEST_ABORT** = ``2``

Request dừng animation được kết nối với cổng "shot".

.. _class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_FADE_OUT:

.. rst-class:: classref-enumeration-constant

:ref:`OneShotRequest<enum_AnimationNodeOneShot_OneShotRequest>` **ONE_SHOT_REQUEST_FADE_OUT** = ``3``

Request fade out animation được kết nối với cổng "shot".

.. rst-class:: classref-item-separator

----

.. _enum_AnimationNodeOneShot_MixMode:

.. rst-class:: classref-enumeration

enum **MixMode**: :ref:`🔗<enum_AnimationNodeOneShot_MixMode>`

.. _class_AnimationNodeOneShot_constant_MIX_MODE_BLEND:

.. rst-class:: classref-enumeration-constant

:ref:`MixMode<enum_AnimationNodeOneShot_MixMode>` **MIX_MODE_BLEND** = ``0``

Blend hai animation. Xem thêm :ref:`AnimationNodeBlend2<class_AnimationNodeBlend2>`.

.. _class_AnimationNodeOneShot_constant_MIX_MODE_ADD:

.. rst-class:: classref-enumeration-constant

:ref:`MixMode<enum_AnimationNodeOneShot_MixMode>` **MIX_MODE_ADD** = ``1``

Blend hai animation theo phương thức additive. Xem thêm :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_AnimationNodeOneShot_property_abort_on_reset:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **abort_on_reset** = ``false`` :ref:`🔗<class_AnimationNodeOneShot_property_abort_on_reset>`

.. rst-class:: classref-property-setget

- |void| **set_abort_on_reset**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_aborted_on_reset**\ (\ )

Nếu ``true``, sub-animation sẽ bị hủy nếu được tiếp tục với reset sau một lần gián đoạn trước đó.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_autorestart:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autorestart** = ``false`` :ref:`🔗<class_AnimationNodeOneShot_property_autorestart>`

.. rst-class:: classref-property-setget

- |void| **set_autorestart**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_autorestart**\ (\ )

Nếu ``true``, sub-animation sẽ tự động khởi động lại sau khi hoàn tất.

Nói cách khác, để bắt đầu tự động khởi động lại, animation phải được phát một lần với request :ref:`ONE_SHOT_REQUEST_FIRE<class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_FIRE>`. Request :ref:`ONE_SHOT_REQUEST_ABORT<class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_ABORT>` sẽ dừng việc tự động khởi động lại, nhưng không vô hiệu hóa chính :ref:`autorestart<class_AnimationNodeOneShot_property_autorestart>`. Vì vậy, request :ref:`ONE_SHOT_REQUEST_FIRE<class_AnimationNodeOneShot_constant_ONE_SHOT_REQUEST_FIRE>` sẽ lại bắt đầu việc tự động khởi động lại.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_autorestart_delay:

.. rst-class:: classref-property

:ref:`float<class_float>` **autorestart_delay** = ``1.0`` :ref:`🔗<class_AnimationNodeOneShot_property_autorestart_delay>`

.. rst-class:: classref-property-setget

- |void| **set_autorestart_delay**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_autorestart_delay**\ (\ )

Độ trễ trước khi việc tự động khởi động lại được kích hoạt, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_autorestart_random_delay:

.. rst-class:: classref-property

:ref:`float<class_float>` **autorestart_random_delay** = ``0.0`` :ref:`🔗<class_AnimationNodeOneShot_property_autorestart_random_delay>`

.. rst-class:: classref-property-setget

- |void| **set_autorestart_random_delay**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_autorestart_random_delay**\ (\ )

Nếu :ref:`autorestart<class_AnimationNodeOneShot_property_autorestart>` là ``true``, một độ trễ bổ sung ngẫu nhiên (tính bằng giây) từ 0 đến giá trị này sẽ được thêm vào :ref:`autorestart_delay<class_AnimationNodeOneShot_property_autorestart_delay>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_break_loop_at_end:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **break_loop_at_end** = ``false`` :ref:`🔗<class_AnimationNodeOneShot_property_break_loop_at_end>`

.. rst-class:: classref-property-setget

- |void| **set_break_loop_at_end**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_loop_broken_at_end**\ (\ )

Nếu ``true``, ngắt loop ở cuối chu kỳ loop để chuyển tiếp, ngay cả khi animation đang lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_fadein_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **fadein_curve** :ref:`🔗<class_AnimationNodeOneShot_property_fadein_curve>`

.. rst-class:: classref-property-setget

- |void| **set_fadein_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_fadein_curve**\ (\ )

Xác định cách làm mượt quá trình cross-fade giữa các animation. Nếu trống, quá trình chuyển tiếp sẽ tuyến tính. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_fadein_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **fadein_time** = ``0.0`` :ref:`🔗<class_AnimationNodeOneShot_property_fadein_time>`

.. rst-class:: classref-property-setget

- |void| **set_fadein_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fadein_time**\ (\ )

Thời lượng fade-in. Ví dụ, đặt giá trị này thành ``1.0`` cho một animation dài 5 giây sẽ tạo ra cross-fade bắt đầu ở giây 0 và kết thúc ở giây 1 trong animation.

\ **Lưu ý:** **AnimationNodeOneShot** chuyển state hiện tại sau khi fade hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_fadeout_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **fadeout_curve** :ref:`🔗<class_AnimationNodeOneShot_property_fadeout_curve>`

.. rst-class:: classref-property-setget

- |void| **set_fadeout_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_fadeout_curve**\ (\ )

Xác định cách làm mượt quá trình cross-fade giữa các animation. Nếu trống, quá trình chuyển tiếp sẽ tuyến tính. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_fadeout_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **fadeout_time** = ``0.0`` :ref:`🔗<class_AnimationNodeOneShot_property_fadeout_time>`

.. rst-class:: classref-property-setget

- |void| **set_fadeout_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fadeout_time**\ (\ )

Thời lượng fade-out. Ví dụ, đặt giá trị này thành ``1.0`` cho một animation dài 5 giây sẽ tạo ra cross-fade bắt đầu ở giây 4 và kết thúc ở giây 5 trong animation.

\ **Lưu ý:** **AnimationNodeOneShot** chuyển state hiện tại sau khi fade hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeOneShot_property_mix_mode:

.. rst-class:: classref-property

:ref:`MixMode<enum_AnimationNodeOneShot_MixMode>` **mix_mode** = ``0`` :ref:`🔗<class_AnimationNodeOneShot_property_mix_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mix_mode**\ (\ value\: :ref:`MixMode<enum_AnimationNodeOneShot_MixMode>`\ ) - :ref:`MixMode<enum_AnimationNodeOneShot_MixMode>` **get_mix_mode**\ (\ )

Loại blend.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
