:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectPanner.xml.

.. _class_AudioEffectPanner:

AudioEffectPanner
=================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng panner âm thanh vào một audio bus.

Điều chỉnh âm thanh sang trái hoặc phải.

.. rst-class:: classref-introduction-group

Mô tả
-----

Xác định mức độ tín hiệu âm thanh được gửi đến các kênh trái và phải. Điều này hỗ trợ spatialization âm thanh, giúp các âm thanh có vị trí riêng biệt trong bản phối.

\ :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>` và :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>` tự động xử lý việc điều chỉnh pan, theo vị trí của nguồn âm thanh trên màn hình.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`pan<class_AudioEffectPanner_property_pan>` | ``0.0`` |
   +---------------------------+--------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectPanner_property_pan:

.. rst-class:: classref-property

:ref:`float<class_float>` **pan** = ``0.0`` :ref:`🔗<class_AudioEffectPanner_property_pan>`

.. rst-class:: classref-property-setget

- |void| **set_pan**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pan**\ (\ )

Vị trí pan. Giá trị âm điều chỉnh âm thanh sang trái, giá trị dương điều chỉnh sang phải. Giá trị có thể nằm trong khoảng từ -1 đến 1.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
