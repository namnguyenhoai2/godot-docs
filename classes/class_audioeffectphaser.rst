:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectPhaser.xml.

.. _class_AudioEffectPhaser:

AudioEffectPhaser
=================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng âm thanh phaser vào một audio bus.

Tạo nhiều bộ lọc notch và peak quét qua toàn bộ phổ tần số.

.. rst-class:: classref-introduction-group

Mô tả
-----

Hiệu ứng "phaser" tạo một bản sao của âm thanh gốc, trong đó pha được xoay khác nhau trên toàn bộ phổ tần số bằng cách sử dụng một chuỗi các tầng bộ lọc all-pass (6 tầng trong hiệu ứng này). Bản sao này được điều biến bằng một bộ dao động tần số thấp và kết hợp với âm thanh gốc, tạo ra các đỉnh và hõm quét qua phổ tần số.

Hiệu ứng này có thể được dùng để tạo âm thanh "thủy tinh" hoặc "bong bóng".

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`depth<class_AudioEffectPhaser_property_depth>`               | ``1.0``    |
   +---------------------------+--------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`feedback<class_AudioEffectPhaser_property_feedback>`         | ``0.7``    |
   +---------------------------+--------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`range_max_hz<class_AudioEffectPhaser_property_range_max_hz>` | ``1600.0`` |
   +---------------------------+--------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`range_min_hz<class_AudioEffectPhaser_property_range_min_hz>` | ``440.0``  |
   +---------------------------+--------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`rate_hz<class_AudioEffectPhaser_property_rate_hz>`           | ``0.5``    |
   +---------------------------+--------------------------------------------------------------------+------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectPhaser_property_depth:

.. rst-class:: classref-property

:ref:`float<class_float>` **depth** = ``1.0`` :ref:`🔗<class_AudioEffectPhaser_property_depth>`

.. rst-class:: classref-property-setget

- |void| **set_depth**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_depth**\ (\ )

Cường độ của hiệu ứng. Giá trị có thể nằm trong khoảng từ 0.1 đến 4.0.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPhaser_property_feedback:

.. rst-class:: classref-property

:ref:`float<class_float>` **feedback** = ``0.7`` :ref:`🔗<class_AudioEffectPhaser_property_feedback>`

.. rst-class:: classref-property-setget

- |void| **set_feedback**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_feedback**\ (\ )

Tỷ lệ âm lượng của âm thanh đã lọc được đưa trở lại các bộ lọc all-pass. Giá trị càng cao thì các bộ lọc peak do hiệu ứng tạo ra càng sắc nét và lớn hơn. Giá trị có thể nằm trong khoảng từ 0.1 đến 0.9.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPhaser_property_range_max_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **range_max_hz** = ``1600.0`` :ref:`🔗<class_AudioEffectPhaser_property_range_max_hz>`

.. rst-class:: classref-property-setget

- |void| **set_range_max_hz**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_range_max_hz**\ (\ )

Xác định tần số tối đa, tính bằng Hz, chịu ảnh hưởng của các điều biến từ bộ dao động tần số thấp. Giá trị có thể nằm trong khoảng từ 10 đến 10000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPhaser_property_range_min_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **range_min_hz** = ``440.0`` :ref:`🔗<class_AudioEffectPhaser_property_range_min_hz>`

.. rst-class:: classref-property-setget

- |void| **set_range_min_hz**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_range_min_hz**\ (\ )

Xác định tần số tối thiểu, tính bằng Hz, chịu ảnh hưởng của các điều biến từ bộ dao động tần số thấp. Giá trị có thể nằm trong khoảng từ 10 đến 10000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPhaser_property_rate_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **rate_hz** = ``0.5`` :ref:`🔗<class_AudioEffectPhaser_property_rate_hz>`

.. rst-class:: classref-property-setget

- |void| **set_rate_hz**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rate_hz**\ (\ )

Điều chỉnh tốc độ, tính bằng Hz, mà hiệu ứng quét lên và xuống trong dải tần số. Giá trị có thể nằm trong khoảng từ 0.01 đến 20.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
