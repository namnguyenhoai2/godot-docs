:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimatedSprite2D.xml.

.. _class_AnimatedSprite2D:

AnimatedSprite2D
================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node Sprite chứa nhiều texture dưới dạng các frame để phát animation.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AnimatedSprite2D** tương tự node :ref:`Sprite2D<class_Sprite2D>`, nhưng chứa nhiều texture dưới dạng các frame animation. Animation được tạo bằng resource :ref:`SpriteFrames<class_SpriteFrames>`, cho phép bạn import các tệp hình ảnh (hoặc một thư mục chứa các tệp đó) để cung cấp các frame animation cho sprite. Resource :ref:`SpriteFrames<class_SpriteFrames>` có thể được cấu hình trong editor thông qua panel SpriteFrames ở phía dưới.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`2D Sprite animation <../tutorials/2d/2d_sprite_animation>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`StringName<class_StringName>`     | :ref:`animation<class_AnimatedSprite2D_property_animation>`           | ``&"default"``    |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`String<class_String>`             | :ref:`autoplay<class_AnimatedSprite2D_property_autoplay>`             | ``""``            |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                 | :ref:`centered<class_AnimatedSprite2D_property_centered>`             | ``true``          |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                 | :ref:`flip_h<class_AnimatedSprite2D_property_flip_h>`                 | ``false``         |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                 | :ref:`flip_v<class_AnimatedSprite2D_property_flip_v>`                 | ``false``         |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                   | :ref:`frame<class_AnimatedSprite2D_property_frame>`                   | ``0``             |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`               | :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>` | ``0.0``           |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`           | :ref:`offset<class_AnimatedSprite2D_property_offset>`                 | ``Vector2(0, 0)`` |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`               | :ref:`speed_scale<class_AnimatedSprite2D_property_speed_scale>`       | ``1.0``           |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`SpriteFrames<class_SpriteFrames>` | :ref:`sprite_frames<class_AnimatedSprite2D_property_sprite_frames>`   |                   |
   +-----------------------------------------+-----------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_playing_speed<class_AnimatedSprite2D_method_get_playing_speed>`\ (\ ) |const|                                                                                                             |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`is_playing<class_AnimatedSprite2D_method_is_playing>`\ (\ ) |const|                                                                                                                           |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`pause<class_AnimatedSprite2D_method_pause>`\ (\ )                                                                                                                                             |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`play<class_AnimatedSprite2D_method_play>`\ (\ name\: :ref:`StringName<class_StringName>` = &"", custom_speed\: :ref:`float<class_float>` = 1.0, from_end\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`play_backwards<class_AnimatedSprite2D_method_play_backwards>`\ (\ name\: :ref:`StringName<class_StringName>` = &""\ )                                                                         |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_frame_and_progress<class_AnimatedSprite2D_method_set_frame_and_progress>`\ (\ frame\: :ref:`int<class_int>`, progress\: :ref:`float<class_float>`\ )                                      |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`stop<class_AnimatedSprite2D_method_stop>`\ (\ )                                                                                                                                               |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AnimatedSprite2D_signal_animation_changed:

.. rst-class:: classref-signal

**animation_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_signal_animation_changed>`

Được phát ra khi :ref:`animation<class_AnimatedSprite2D_property_animation>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_signal_animation_finished:

.. rst-class:: classref-signal

**animation_finished**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_signal_animation_finished>`

Được phát ra khi animation đến cuối, hoặc đến đầu nếu được phát ngược. Khi animation kết thúc, quá trình phát sẽ tạm dừng.

\ **Lưu ý:** Signal này không được phát ra nếu animation đang lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_signal_animation_looped:

.. rst-class:: classref-signal

**animation_looped**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_signal_animation_looped>`

Được phát ra khi animation lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_signal_frame_changed:

.. rst-class:: classref-signal

**frame_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_signal_frame_changed>`

Được phát ra khi :ref:`frame<class_AnimatedSprite2D_property_frame>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_signal_sprite_frames_changed:

.. rst-class:: classref-signal

**sprite_frames_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_signal_sprite_frames_changed>`

Được phát ra khi :ref:`sprite_frames<class_AnimatedSprite2D_property_sprite_frames>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimatedSprite2D_property_animation:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **animation** = ``&"default"`` :ref:`🔗<class_AnimatedSprite2D_property_animation>`

.. rst-class:: classref-property-setget

- |void| **set_animation**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_animation**\ (\ )

Animation hiện tại từ resource :ref:`sprite_frames<class_AnimatedSprite2D_property_sprite_frames>`. Nếu giá trị này thay đổi, bộ đếm :ref:`frame<class_AnimatedSprite2D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>` sẽ được đặt lại.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_autoplay:

.. rst-class:: classref-property

:ref:`String<class_String>` **autoplay** = ``""`` :ref:`🔗<class_AnimatedSprite2D_property_autoplay>`

.. rst-class:: classref-property-setget

- |void| **set_autoplay**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_autoplay**\ (\ )

Tên của animation sẽ phát khi scene được tải.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_centered:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **centered** = ``true`` :ref:`🔗<class_AnimatedSprite2D_property_centered>`

.. rst-class:: classref-property-setget

- |void| **set_centered**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_centered**\ (\ )

Nếu ``true``, texture sẽ được căn giữa.

\ **Lưu ý:** Đối với game có phong cách pixel art, texture có thể bị biến dạng khi được căn giữa. Nguyên nhân là vị trí của texture nằm giữa các pixel. Để ngăn điều này, hãy đặt thuộc tính này thành ``false``, hoặc cân nhắc bật :ref:`ProjectSettings.rendering/2d/snap/snap_2d_vertices_to_pixel<class_ProjectSettings_property_rendering/2d/snap/snap_2d_vertices_to_pixel>` và :ref:`ProjectSettings.rendering/2d/snap/snap_2d_transforms_to_pixel<class_ProjectSettings_property_rendering/2d/snap/snap_2d_transforms_to_pixel>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_flip_h:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **flip_h** = ``false`` :ref:`🔗<class_AnimatedSprite2D_property_flip_h>`

.. rst-class:: classref-property-setget

- |void| **set_flip_h**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_flipped_h**\ (\ )

Nếu ``true``, texture sẽ được lật theo chiều ngang.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_flip_v:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **flip_v** = ``false`` :ref:`🔗<class_AnimatedSprite2D_property_flip_v>`

.. rst-class:: classref-property-setget

- |void| **set_flip_v**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_flipped_v**\ (\ )

Nếu ``true``, texture sẽ được lật theo chiều dọc.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_frame:

.. rst-class:: classref-property

:ref:`int<class_int>` **frame** = ``0`` :ref:`🔗<class_AnimatedSprite2D_property_frame>`

.. rst-class:: classref-property-setget

- |void| **set_frame**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_frame**\ (\ )

Chỉ số của frame animation đang hiển thị. Việc đặt thuộc tính này cũng sẽ đặt lại :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>`. Nếu không muốn điều đó, hãy dùng :ref:`set_frame_and_progress()<class_AnimatedSprite2D_method_set_frame_and_progress>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_frame_progress:

.. rst-class:: classref-property

:ref:`float<class_float>` **frame_progress** = ``0.0`` :ref:`🔗<class_AnimatedSprite2D_property_frame_progress>`

.. rst-class:: classref-property-setget

- |void| **set_frame_progress**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_frame_progress**\ (\ )

Giá trị tiến độ nằm giữa ``0.0`` và ``1.0`` cho đến khi frame hiện tại chuyển sang frame tiếp theo. Nếu animation đang phát ngược, giá trị sẽ chuyển từ ``1.0`` đến ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_AnimatedSprite2D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Độ lệch khi vẽ texture.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_AnimatedSprite2D_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tỷ lệ điều chỉnh tốc độ. Ví dụ, nếu giá trị này là ``1``, animation sẽ phát ở tốc độ bình thường. Nếu là ``0.5``, animation sẽ phát ở nửa tốc độ. Nếu là ``2``, animation sẽ phát ở gấp đôi tốc độ.

Nếu được đặt thành giá trị âm, animation sẽ phát ngược. Nếu được đặt thành ``0``, animation sẽ không tiến triển.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_property_sprite_frames:

.. rst-class:: classref-property

:ref:`SpriteFrames<class_SpriteFrames>` **sprite_frames** :ref:`🔗<class_AnimatedSprite2D_property_sprite_frames>`

.. rst-class:: classref-property-setget

- |void| **set_sprite_frames**\ (\ value\: :ref:`SpriteFrames<class_SpriteFrames>`\ ) - :ref:`SpriteFrames<class_SpriteFrames>` **get_sprite_frames**\ (\ )

Resource :ref:`SpriteFrames<class_SpriteFrames>` chứa các animation. Cho phép bạn tải, chỉnh sửa, xóa, tạo bản riêng và lưu trạng thái của resource :ref:`SpriteFrames<class_SpriteFrames>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimatedSprite2D_method_get_playing_speed:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playing_speed**\ (\ ) |const| :ref:`🔗<class_AnimatedSprite2D_method_get_playing_speed>`

Trả về tốc độ phát thực tế của animation hiện tại hoặc ``0`` nếu không phát. Tốc độ này là thuộc tính :ref:`speed_scale<class_AnimatedSprite2D_property_speed_scale>` nhân với đối số ``custom_speed`` được chỉ định khi gọi phương thức :ref:`play()<class_AnimatedSprite2D_method_play>`.

Trả về giá trị âm nếu animation hiện tại đang phát ngược.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_is_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_playing**\ (\ ) |const| :ref:`🔗<class_AnimatedSprite2D_method_is_playing>`

Trả về ``true`` nếu hiện đang có animation phát (ngay cả khi :ref:`speed_scale<class_AnimatedSprite2D_property_speed_scale>` và/hoặc ``custom_speed`` là ``0``).

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_pause:

.. rst-class:: classref-method

|void| **pause**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_method_pause>`

Tạm dừng animation đang phát. :ref:`frame<class_AnimatedSprite2D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>` sẽ được giữ lại, và việc gọi :ref:`play()<class_AnimatedSprite2D_method_play>` hoặc :ref:`play_backwards()<class_AnimatedSprite2D_method_play_backwards>` không có đối số sẽ tiếp tục animation từ vị trí phát hiện tại.

Xem thêm :ref:`stop()<class_AnimatedSprite2D_method_stop>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_play:

.. rst-class:: classref-method

|void| **play**\ (\ name\: :ref:`StringName<class_StringName>` = &"", custom_speed\: :ref:`float<class_float>` = 1.0, from_end\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AnimatedSprite2D_method_play>`

Phát animation có tên ``name``. Nếu ``custom_speed`` là số âm và ``from_end`` là ``true``, animation sẽ phát ngược (tương đương với việc gọi :ref:`play_backwards()<class_AnimatedSprite2D_method_play_backwards>`).

Nếu phương thức này được gọi với chính animation ``name`` đó, hoặc không có tham số ``name``, animation được gán sẽ tiếp tục phát nếu trước đó đang tạm dừng.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_play_backwards:

.. rst-class:: classref-method

|void| **play_backwards**\ (\ name\: :ref:`StringName<class_StringName>` = &""\ ) :ref:`🔗<class_AnimatedSprite2D_method_play_backwards>`

Phát ngược animation có tên ``name``.

Phương thức này là cách viết tắt của :ref:`play()<class_AnimatedSprite2D_method_play>` với ``custom_speed = -1.0`` và ``from_end = true``, vì vậy hãy xem phần mô tả của phương thức đó để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_set_frame_and_progress:

.. rst-class:: classref-method

|void| **set_frame_and_progress**\ (\ frame\: :ref:`int<class_int>`, progress\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AnimatedSprite2D_method_set_frame_and_progress>`

Đặt :ref:`frame<class_AnimatedSprite2D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>` thành các giá trị đã cho. Không giống như việc đặt :ref:`frame<class_AnimatedSprite2D_property_frame>`, phương thức này không ngầm đặt lại :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>` về ``0.0``.

\ **Ví dụ:** Thay đổi animation trong khi giữ nguyên :ref:`frame<class_AnimatedSprite2D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite2D_property_frame_progress>`:


.. tabs::

 .. code-tab:: gdscript

    var current_frame = animated_sprite.get_frame()
    var current_progress = animated_sprite.get_frame_progress()
    animated_sprite.play("walk_another_skin")
    animated_sprite.set_frame_and_progress(current_frame, current_progress)



.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite2D_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AnimatedSprite2D_method_stop>`

Dừng animation đang phát. Vị trí animation được đặt lại thành ``0`` và ``custom_speed`` được đặt lại thành ``1.0``. Xem thêm :ref:`pause()<class_AnimatedSprite2D_method_pause>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
