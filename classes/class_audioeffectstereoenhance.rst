:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectStereoEnhance.xml.

.. _class_AudioEffectStereoEnhance:

AudioEffectStereoEnhance
========================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng âm thanh điều chỉnh stereo vào một audio bus.

Điều khiển gain của các kênh side và mở rộng stereo image.

.. rst-class:: classref-introduction-group

Mô tả
-----

Điều chỉnh gain của các kênh trái và phải, đồng thời biến âm thanh mono thành stereo bằng cách dịch pha.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`pan_pullout<class_AudioEffectStereoEnhance_property_pan_pullout>`         | ``1.0`` |
   +---------------------------+---------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`surround<class_AudioEffectStereoEnhance_property_surround>`               | ``0.0`` |
   +---------------------------+---------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`time_pullout_ms<class_AudioEffectStereoEnhance_property_time_pullout_ms>` | ``0.0`` |
   +---------------------------+---------------------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectStereoEnhance_property_pan_pullout:

.. rst-class:: classref-property

:ref:`float<class_float>` **pan_pullout** = ``1.0`` :ref:`🔗<class_AudioEffectStereoEnhance_property_pan_pullout>`

.. rst-class:: classref-property-setget

- |void| **set_pan_pullout**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pan_pullout**\ (\ )

Gain của các kênh side, nếu tồn tại. Giá trị 0 sẽ downmix stereo thành mono. Giá trị có thể nằm trong khoảng từ 0 đến 4.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectStereoEnhance_property_surround:

.. rst-class:: classref-property

:ref:`float<class_float>` **surround** = ``0.0`` :ref:`🔗<class_AudioEffectStereoEnhance_property_surround>`

.. rst-class:: classref-property-setget

- |void| **set_surround**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_surround**\ (\ )

Mở rộng stereo image thông qua việc dịch pha kết hợp với :ref:`time_pullout_ms<class_AudioEffectStereoEnhance_property_time_pullout_ms>`. Chỉ pan âm thanh sang kênh trái nếu :ref:`time_pullout_ms<class_AudioEffectStereoEnhance_property_time_pullout_ms>` là 0. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectStereoEnhance_property_time_pullout_ms:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_pullout_ms** = ``0.0`` :ref:`🔗<class_AudioEffectStereoEnhance_property_time_pullout_ms>`

.. rst-class:: classref-property-setget

- |void| **set_time_pullout**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_pullout**\ (\ )

Mở rộng stereo image thông qua việc dịch pha kết hợp với :ref:`surround<class_AudioEffectStereoEnhance_property_surround>`. Chỉ trì hoãn kênh phải nếu :ref:`surround<class_AudioEffectStereoEnhance_property_surround>` là 0. Giá trị tính bằng mili giây và có thể nằm trong khoảng từ 0 đến 50.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
