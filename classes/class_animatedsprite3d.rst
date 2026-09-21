:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimatedSprite3D.xml.

.. _class_AnimatedSprite3D:

AnimatedSprite3D
================

**Kế thừa:** :ref:`SpriteBase3D<class_SpriteBase3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node sprite 2D trong thế giới 3D, có thể sử dụng nhiều texture 2D để tạo hoạt ảnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AnimatedSprite3D** tương tự node :ref:`Sprite3D<class_Sprite3D>`, ngoại trừ việc nó chứa nhiều texture dưới dạng các :ref:`sprite_frames<class_AnimatedSprite3D_property_sprite_frames>` của hoạt ảnh. Hoạt ảnh được tạo bằng resource :ref:`SpriteFrames<class_SpriteFrames>`, cho phép bạn import các tệp hình ảnh (hoặc một thư mục chứa những tệp đó) để cung cấp các frame hoạt ảnh cho sprite. Resource :ref:`SpriteFrames<class_SpriteFrames>` có thể được cấu hình trong editor thông qua panel SpriteFrames ở phía dưới.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`2D Sprite animation (also applies to 3D) <../tutorials/2d/2d_sprite_animation>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`StringName<class_StringName>`     | :ref:`animation<class_AnimatedSprite3D_property_animation>`           | ``&"default"`` |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`String<class_String>`             | :ref:`autoplay<class_AnimatedSprite3D_property_autoplay>`             | ``""``         |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`int<class_int>`                   | :ref:`frame<class_AnimatedSprite3D_property_frame>`                   | ``0``          |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>`               | :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>` | ``0.0``        |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>`               | :ref:`speed_scale<class_AnimatedSprite3D_property_speed_scale>`       | ``1.0``        |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+
   | :ref:`SpriteFrames<class_SpriteFrames>` | :ref:`sprite_frames<class_AnimatedSprite3D_property_sprite_frames>`   |                |
   +-----------------------------------------+-----------------------------------------------------------------------+----------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_playing_speed<class_AnimatedSprite3D_method_get_playing_speed>`\ (\ ) |const|                                                                                                             |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`is_playing<class_AnimatedSprite3D_method_is_playing>`\ (\ ) |const|                                                                                                                           |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`pause<class_AnimatedSprite3D_method_pause>`\ (\ )                                                                                                                                             |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`play<class_AnimatedSprite3D_method_play>`\ (\ name\: :ref:`StringName<class_StringName>` = &"", custom_speed\: :ref:`float<class_float>` = 1.0, from_end\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`play_backwards<class_AnimatedSprite3D_method_play_backwards>`\ (\ name\: :ref:`StringName<class_StringName>` = &""\ )                                                                         |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_frame_and_progress<class_AnimatedSprite3D_method_set_frame_and_progress>`\ (\ frame\: :ref:`int<class_int>`, progress\: :ref:`float<class_float>`\ )                                      |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`stop<class_AnimatedSprite3D_method_stop>`\ (\ )                                                                                                                                               |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_AnimatedSprite3D_signal_animation_changed:

.. rst-class:: classref-signal

**animation_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_signal_animation_changed>`

Được phát ra khi :ref:`animation<class_AnimatedSprite3D_property_animation>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_signal_animation_finished:

.. rst-class:: classref-signal

**animation_finished**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_signal_animation_finished>`

Được phát ra khi hoạt ảnh đến cuối, hoặc đến đầu nếu đang phát ngược. Khi hoạt ảnh kết thúc, quá trình phát sẽ tạm dừng.

\ **Lưu ý:** Tín hiệu này không được phát ra nếu hoạt ảnh đang lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_signal_animation_looped:

.. rst-class:: classref-signal

**animation_looped**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_signal_animation_looped>`

Được phát ra khi hoạt ảnh lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_signal_frame_changed:

.. rst-class:: classref-signal

**frame_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_signal_frame_changed>`

Được phát ra khi :ref:`frame<class_AnimatedSprite3D_property_frame>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_signal_sprite_frames_changed:

.. rst-class:: classref-signal

**sprite_frames_changed**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_signal_sprite_frames_changed>`

Được phát ra khi :ref:`sprite_frames<class_AnimatedSprite3D_property_sprite_frames>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimatedSprite3D_property_animation:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **animation** = ``&"default"`` :ref:`🔗<class_AnimatedSprite3D_property_animation>`

.. rst-class:: classref-property-setget

- |void| **set_animation**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_animation**\ (\ )

Hoạt ảnh hiện tại từ resource :ref:`sprite_frames<class_AnimatedSprite3D_property_sprite_frames>`. Nếu giá trị này được thay đổi, bộ đếm :ref:`frame<class_AnimatedSprite3D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>` sẽ được đặt lại.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_property_autoplay:

.. rst-class:: classref-property

:ref:`String<class_String>` **autoplay** = ``""`` :ref:`🔗<class_AnimatedSprite3D_property_autoplay>`

.. rst-class:: classref-property-setget

- |void| **set_autoplay**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_autoplay**\ (\ )

Tên của hoạt ảnh sẽ phát khi scene được tải.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_property_frame:

.. rst-class:: classref-property

:ref:`int<class_int>` **frame** = ``0`` :ref:`🔗<class_AnimatedSprite3D_property_frame>`

.. rst-class:: classref-property-setget

- |void| **set_frame**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_frame**\ (\ )

Chỉ mục của frame hoạt ảnh đang hiển thị. Việc thiết lập thuộc tính này cũng đặt lại :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>`. Nếu không muốn như vậy, hãy sử dụng :ref:`set_frame_and_progress()<class_AnimatedSprite3D_method_set_frame_and_progress>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_property_frame_progress:

.. rst-class:: classref-property

:ref:`float<class_float>` **frame_progress** = ``0.0`` :ref:`🔗<class_AnimatedSprite3D_property_frame_progress>`

.. rst-class:: classref-property-setget

- |void| **set_frame_progress**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_frame_progress**\ (\ )

Giá trị tiến trình từ ``0.0`` đến ``1.0`` cho đến khi frame hiện tại chuyển sang frame tiếp theo. Nếu hoạt ảnh đang phát ngược, giá trị sẽ chuyển từ ``1.0`` đến ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_AnimatedSprite3D_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tỷ lệ điều chỉnh tốc độ. Ví dụ, nếu giá trị này là ``1``, hoạt ảnh sẽ phát ở tốc độ bình thường. Nếu là ``0.5``, hoạt ảnh sẽ phát ở nửa tốc độ. Nếu là ``2``, hoạt ảnh sẽ phát ở tốc độ gấp đôi.

Nếu được đặt thành giá trị âm, hoạt ảnh sẽ phát ngược. Nếu được đặt thành ``0``, hoạt ảnh sẽ không tiến triển.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_property_sprite_frames:

.. rst-class:: classref-property

:ref:`SpriteFrames<class_SpriteFrames>` **sprite_frames** :ref:`🔗<class_AnimatedSprite3D_property_sprite_frames>`

.. rst-class:: classref-property-setget

- |void| **set_sprite_frames**\ (\ value\: :ref:`SpriteFrames<class_SpriteFrames>`\ ) - :ref:`SpriteFrames<class_SpriteFrames>` **get_sprite_frames**\ (\ )

Resource :ref:`SpriteFrames<class_SpriteFrames>` chứa (các) hoạt ảnh. Cho phép bạn tải, chỉnh sửa, xóa, tạo bản sao độc lập và lưu trạng thái của resource :ref:`SpriteFrames<class_SpriteFrames>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimatedSprite3D_method_get_playing_speed:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playing_speed**\ (\ ) |const| :ref:`🔗<class_AnimatedSprite3D_method_get_playing_speed>`

Trả về tốc độ phát thực tế của hoạt ảnh hiện tại hoặc ``0`` nếu không phát. Tốc độ này là thuộc tính :ref:`speed_scale<class_AnimatedSprite3D_property_speed_scale>` nhân với đối số ``custom_speed`` được chỉ định khi gọi phương thức :ref:`play()<class_AnimatedSprite3D_method_play>`.

Trả về giá trị âm nếu hoạt ảnh hiện tại đang phát ngược.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_is_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_playing**\ (\ ) |const| :ref:`🔗<class_AnimatedSprite3D_method_is_playing>`

Trả về ``true`` nếu hiện đang có một hoạt ảnh được phát (ngay cả khi :ref:`speed_scale<class_AnimatedSprite3D_property_speed_scale>` và/hoặc ``custom_speed`` là ``0``).

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_pause:

.. rst-class:: classref-method

|void| **pause**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_method_pause>`

Tạm dừng hoạt ảnh hiện đang phát. :ref:`frame<class_AnimatedSprite3D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>` sẽ được giữ nguyên; việc gọi :ref:`play()<class_AnimatedSprite3D_method_play>` hoặc :ref:`play_backwards()<class_AnimatedSprite3D_method_play_backwards>` không có đối số sẽ tiếp tục hoạt ảnh từ vị trí phát hiện tại.

Xem thêm :ref:`stop()<class_AnimatedSprite3D_method_stop>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_play:

.. rst-class:: classref-method

|void| **play**\ (\ name\: :ref:`StringName<class_StringName>` = &"", custom_speed\: :ref:`float<class_float>` = 1.0, from_end\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AnimatedSprite3D_method_play>`

Phát hoạt ảnh có tên ``name``. Nếu ``custom_speed`` là số âm và ``from_end`` là ``true``, hoạt ảnh sẽ phát ngược (tương đương với việc gọi :ref:`play_backwards()<class_AnimatedSprite3D_method_play_backwards>`).

Nếu phương thức này được gọi với chính hoạt ảnh ``name`` đó hoặc không có tham số ``name``, hoạt ảnh được gán sẽ tiếp tục phát nếu trước đó đã bị tạm dừng.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_play_backwards:

.. rst-class:: classref-method

|void| **play_backwards**\ (\ name\: :ref:`StringName<class_StringName>` = &""\ ) :ref:`🔗<class_AnimatedSprite3D_method_play_backwards>`

Phát ngược hoạt ảnh có tên ``name``.

Phương thức này là cách viết tắt của :ref:`play()<class_AnimatedSprite3D_method_play>` với ``custom_speed = -1.0`` và ``from_end = true``, vì vậy hãy xem phần mô tả của nó để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_set_frame_and_progress:

.. rst-class:: classref-method

|void| **set_frame_and_progress**\ (\ frame\: :ref:`int<class_int>`, progress\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AnimatedSprite3D_method_set_frame_and_progress>`

Đặt :ref:`frame<class_AnimatedSprite3D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>` thành các giá trị đã cho. Không giống như khi đặt :ref:`frame<class_AnimatedSprite3D_property_frame>`, phương thức này không ngầm đặt lại :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>` về ``0.0``.

\ **Ví dụ:** Thay đổi hoạt ảnh trong khi giữ nguyên :ref:`frame<class_AnimatedSprite3D_property_frame>` và :ref:`frame_progress<class_AnimatedSprite3D_property_frame_progress>`:


.. tabs::

 .. code-tab:: gdscript

    var current_frame = animated_sprite.get_frame()
    var current_progress = animated_sprite.get_frame_progress()
    animated_sprite.play("walk_another_skin")
    animated_sprite.set_frame_and_progress(current_frame, current_progress)



.. rst-class:: classref-item-separator

----

.. _class_AnimatedSprite3D_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AnimatedSprite3D_method_stop>`

Dừng hoạt ảnh hiện đang phát. Vị trí hoạt ảnh được đặt lại thành ``0`` và ``custom_speed`` được đặt lại thành ``1.0``. Xem thêm :ref:`pause()<class_AnimatedSprite3D_method_pause>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
