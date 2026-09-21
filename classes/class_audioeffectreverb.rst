:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectReverb.xml.

.. _class_AudioEffectReverb:

AudioEffectReverb
=================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng âm thanh reverberation vào một audio bus.

Mô phỏng tiếng vọng bằng cách phát một phiên bản mờ của âm thanh đầu vào.

.. rst-class:: classref-introduction-group

Mô tả
-----

Hiệu ứng "reverb" liên tục phát lại âm thanh đầu vào, với âm lượng giảm dần theo thời gian. Hiệu ứng này mô phỏng âm thanh trong nhiều loại không gian khác nhau, từ những căn phòng nhỏ đến các hang động lớn.

Xem thêm :ref:`AudioEffectDelay<class_AudioEffectDelay>` để biết về một loại tiếng vọng không bị mờ.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`damping<class_AudioEffectReverb_property_damping>`                     | ``0.5``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dry<class_AudioEffectReverb_property_dry>`                             | ``1.0``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`hipass<class_AudioEffectReverb_property_hipass>`                       | ``0.0``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`predelay_feedback<class_AudioEffectReverb_property_predelay_feedback>` | ``0.4``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`predelay_msec<class_AudioEffectReverb_property_predelay_msec>`         | ``150.0`` |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`room_size<class_AudioEffectReverb_property_room_size>`                 | ``0.8``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`spread<class_AudioEffectReverb_property_spread>`                       | ``1.0``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`wet<class_AudioEffectReverb_property_wet>`                             | ``0.5``   |
   +---------------------------+------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectReverb_property_damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **damping** = ``0.5`` :ref:`🔗<class_AudioEffectReverb_property_damping>`

.. rst-class:: classref-property-setget

- |void| **set_damping**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_damping**\ (\ )

Xác định mức độ phản xạ của các bức tường trong căn phòng giả lập. Tường càng phản xạ, reverb càng có nhiều thành phần tần số cao. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_dry:

.. rst-class:: classref-property

:ref:`float<class_float>` **dry** = ``1.0`` :ref:`🔗<class_AudioEffectReverb_property_dry>`

.. rst-class:: classref-property-setget

- |void| **set_dry**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dry**\ (\ )

Tỷ lệ âm lượng của âm thanh gốc. Ở mức 0, chỉ âm thanh đã được biến đổi được xuất ra. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_hipass:

.. rst-class:: classref-property

:ref:`float<class_float>` **hipass** = ``0.0`` :ref:`🔗<class_AudioEffectReverb_property_hipass>`

.. rst-class:: classref-property-setget

- |void| **set_hpf**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_hpf**\ (\ )

Bộ lọc high-pass cho phép các tần số cao hơn một ngưỡng cắt nhất định đi qua và làm suy giảm các tần số thấp hơn ngưỡng cắt. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_predelay_feedback:

.. rst-class:: classref-property

:ref:`float<class_float>` **predelay_feedback** = ``0.4`` :ref:`🔗<class_AudioEffectReverb_property_predelay_feedback>`

.. rst-class:: classref-property-setget

- |void| **set_predelay_feedback**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_predelay_feedback**\ (\ )

Độ khuếch đại của các bản sao phản xạ sớm. Ở các giá trị cao hơn, các bản sao phản xạ sớm sẽ to hơn và ngân dài hơn. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_predelay_msec:

.. rst-class:: classref-property

:ref:`float<class_float>` **predelay_msec** = ``150.0`` :ref:`🔗<class_AudioEffectReverb_property_predelay_msec>`

.. rst-class:: classref-property-setget

- |void| **set_predelay_msec**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_predelay_msec**\ (\ )

Khoảng thời gian giữa âm thanh gốc và các phản xạ sớm của tín hiệu reverb, tính bằng mili giây. Giá trị có thể nằm trong khoảng từ 20 đến 500.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_room_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **room_size** = ``0.8`` :ref:`🔗<class_AudioEffectReverb_property_room_size>`

.. rst-class:: classref-property-setget

- |void| **set_room_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_room_size**\ (\ )

Kích thước của căn phòng được mô phỏng. Giá trị lớn hơn nghĩa là có nhiều tiếng vọng hơn. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_spread:

.. rst-class:: classref-property

:ref:`float<class_float>` **spread** = ``1.0`` :ref:`🔗<class_AudioEffectReverb_property_spread>`

.. rst-class:: classref-property-setget

- |void| **set_spread**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_spread**\ (\ )

Mở rộng hoặc thu hẹp hình ảnh stereo của phần đuôi reverb. Ở mức 1, hình ảnh được mở rộng tối đa. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectReverb_property_wet:

.. rst-class:: classref-property

:ref:`float<class_float>` **wet** = ``0.5`` :ref:`🔗<class_AudioEffectReverb_property_wet>`

.. rst-class:: classref-property-setget

- |void| **set_wet**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_wet**\ (\ )

Tỷ lệ âm lượng của âm thanh đã được biến đổi. Ở mức 0, chỉ âm thanh gốc được xuất ra. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
