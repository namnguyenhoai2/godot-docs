:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimatedTexture.xml.

.. _class_AnimatedTexture:

AnimatedTexture
===============

**Đã deprecated:** Class này hiện không hoạt động đúng trong các phiên bản hiện tại và có thể bị xóa trong tương lai. Hiện chưa có workaround tương đương.

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture proxy cho các animation đơn giản dựa trên frame.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AnimatedTexture** là một định dạng resource dành cho animation dựa trên frame, trong đó nhiều texture có thể được tự động nối tiếp với khoảng trễ được định trước cho mỗi frame. Không giống :ref:`AnimationPlayer<class_AnimationPlayer>` hoặc :ref:`AnimatedSprite2D<class_AnimatedSprite2D>`, nó không phải là một :ref:`Node<class_Node>`, nhưng có ưu điểm là có thể được sử dụng ở bất kỳ nơi nào có thể sử dụng resource :ref:`Texture2D<class_Texture2D>`, chẳng hạn như trong một :ref:`TileSet<class_TileSet>`.

Việc phát animation được điều khiển bởi thuộc tính :ref:`speed_scale<class_AnimatedTexture_property_speed_scale>`, cũng như thời lượng của từng frame (xem :ref:`set_frame_duration()<class_AnimatedTexture_method_set_frame_duration>`). Animation lặp lại, tức là sẽ tự động bắt đầu lại từ frame 0 sau khi phát frame cuối cùng.

\ **AnimatedTexture** hiện yêu cầu tất cả texture của các frame phải có cùng kích thước; nếu không, các texture lớn hơn sẽ bị crop để khớp với texture nhỏ nhất.

\ **Note:** AnimatedTexture doesn't support using :ref:`AtlasTexture<class_AtlasTexture>`\ s. Each frame needs to be a separate :ref:`Texture2D<class_Texture2D>`.

\ **Cảnh báo:** Implementation hiện tại không hiệu quả đối với các renderer hiện đại.

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`current_frame<class_AnimatedTexture_property_current_frame>` |                                                                                        |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`frames<class_AnimatedTexture_property_frames>`               | ``1``                                                                                  |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`one_shot<class_AnimatedTexture_property_one_shot>`           | ``false``                                                                              |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`pause<class_AnimatedTexture_property_pause>`                 | ``false``                                                                              |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | resource_local_to_scene                                            | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`speed_scale<class_AnimatedTexture_property_speed_scale>`     | ``1.0``                                                                                |
   +---------------------------+--------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`         | :ref:`get_frame_duration<class_AnimatedTexture_method_get_frame_duration>`\ (\ frame\: :ref:`int<class_int>`\ ) |const|                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`get_frame_texture<class_AnimatedTexture_method_get_frame_texture>`\ (\ frame\: :ref:`int<class_int>`\ ) |const|                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                            | :ref:`set_frame_duration<class_AnimatedTexture_method_set_frame_duration>`\ (\ frame\: :ref:`int<class_int>`, duration\: :ref:`float<class_float>`\ )      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                            | :ref:`set_frame_texture<class_AnimatedTexture_method_set_frame_texture>`\ (\ frame\: :ref:`int<class_int>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Constants
---------

.. _class_AnimatedTexture_constant_MAX_FRAMES:

.. rst-class:: classref-constant

**MAX_FRAMES** = ``256`` :ref:`🔗<class_AnimatedTexture_constant_MAX_FRAMES>`

Số frame tối đa được **AnimatedTexture** hỗ trợ. Nếu animation của bạn cần nhiều frame hơn, hãy sử dụng :ref:`AnimationPlayer<class_AnimationPlayer>` hoặc :ref:`AnimatedSprite2D<class_AnimatedSprite2D>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimatedTexture_property_current_frame:

.. rst-class:: classref-property

:ref:`int<class_int>` **current_frame** :ref:`🔗<class_AnimatedTexture_property_current_frame>`

.. rst-class:: classref-property-setget

- |void| **set_current_frame**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_current_frame**\ (\ )

Đặt frame hiện đang hiển thị của texture. Việc đặt frame này trong khi đang phát sẽ reset thời gian của frame hiện tại, vì vậy frame mới được chọn sẽ phát trong toàn bộ thời lượng frame đã cấu hình.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_property_frames:

.. rst-class:: classref-property

:ref:`int<class_int>` **frames** = ``1`` :ref:`🔗<class_AnimatedTexture_property_frames>`

.. rst-class:: classref-property-setget

- |void| **set_frames**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_frames**\ (\ )

Số frame được sử dụng trong animation. Mặc dù bạn có thể tạo các frame độc lập bằng :ref:`set_frame_texture()<class_AnimatedTexture_method_set_frame_texture>`, bạn cần đặt giá trị này để animation tính đến các frame mới. Số frame tối đa là :ref:`MAX_FRAMES<class_AnimatedTexture_constant_MAX_FRAMES>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_property_one_shot:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_shot** = ``false`` :ref:`🔗<class_AnimatedTexture_property_one_shot>`

.. rst-class:: classref-property-setget

- |void| **set_one_shot**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_one_shot**\ (\ )

Nếu ``true``, animation sẽ chỉ phát một lần và không lặp lại từ frame đầu tiên sau khi đi đến cuối. Lưu ý rằng việc đi đến cuối sẽ không đặt :ref:`pause<class_AnimatedTexture_property_pause>` thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_property_pause:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pause** = ``false`` :ref:`🔗<class_AnimatedTexture_property_pause>`

.. rst-class:: classref-property-setget

- |void| **set_pause**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_pause**\ (\ )

Nếu ``true``, animation sẽ tạm dừng tại vị trí hiện tại (tức là tại :ref:`current_frame<class_AnimatedTexture_property_current_frame>`). Animation sẽ tiếp tục từ vị trí đã tạm dừng khi thay đổi thuộc tính này thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_AnimatedTexture_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tốc độ animation được nhân với giá trị này. Nếu được đặt thành giá trị âm, animation sẽ phát ngược.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_AnimatedTexture_method_get_frame_duration:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_frame_duration**\ (\ frame\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimatedTexture_method_get_frame_duration>`

Trả về thời lượng của ``frame`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_method_get_frame_texture:

.. rst-class:: classref-method

:ref:`Texture2D<class_Texture2D>` **get_frame_texture**\ (\ frame\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimatedTexture_method_get_frame_texture>`

Trả về :ref:`Texture2D<class_Texture2D>` của frame đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_method_set_frame_duration:

.. rst-class:: classref-method

|void| **set_frame_duration**\ (\ frame\: :ref:`int<class_int>`, duration\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AnimatedTexture_method_set_frame_duration>`

Đặt thời lượng của ``frame`` đã cho. Thời lượng cuối cùng bị ảnh hưởng bởi :ref:`speed_scale<class_AnimatedTexture_property_speed_scale>`. Nếu được đặt thành ``0``, frame sẽ bị bỏ qua trong quá trình phát.

.. rst-class:: classref-item-separator

----

.. _class_AnimatedTexture_method_set_frame_texture:

.. rst-class:: classref-method

|void| **set_frame_texture**\ (\ frame\: :ref:`int<class_int>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) :ref:`🔗<class_AnimatedTexture_method_set_frame_texture>`

Gán một :ref:`Texture2D<class_Texture2D>` cho frame đã cho. ID của frame bắt đầu từ 0, vì vậy frame đầu tiên có ID 0, còn frame cuối cùng của animation có ID :ref:`frames<class_AnimatedTexture_property_frames>` - 1.

Bạn có thể xác định bất kỳ số lượng texture nào, tối đa :ref:`MAX_FRAMES<class_AnimatedTexture_constant_MAX_FRAMES>`, nhưng hãy nhớ rằng chỉ các frame từ 0 đến :ref:`frames<class_AnimatedTexture_property_frames>` - 1 mới là một phần của animation.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
