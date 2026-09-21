:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectFilter.xml.

.. _class_AudioEffectFilter:

AudioEffectFilter
=================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioEffectBandLimitFilter<class_AudioEffectBandLimitFilter>`, :ref:`AudioEffectBandPassFilter<class_AudioEffectBandPassFilter>`, :ref:`AudioEffectHighPassFilter<class_AudioEffectHighPassFilter>`, :ref:`AudioEffectHighShelfFilter<class_AudioEffectHighShelfFilter>`, :ref:`AudioEffectLowPassFilter<class_AudioEffectLowPassFilter>`, :ref:`AudioEffectLowShelfFilter<class_AudioEffectLowShelfFilter>`, :ref:`AudioEffectNotchFilter<class_AudioEffectNotchFilter>`

Lớp cơ sở cho các bộ lọc. Hãy sử dụng các effect kế thừa lớp này thay vì sử dụng trực tiếp lớp này.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một "bộ lọc" điều khiển gain của các tần số, sử dụng :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>` làm ngưỡng tần số. Bộ lọc có thể giúp tạo không gian cho từng âm thanh và tạo ra các effect thú vị.

Có các loại bộ lọc khác nhau kế thừa lớp này:

Shelf filters: :ref:`AudioEffectLowShelfFilter<class_AudioEffectLowShelfFilter>` and :ref:`AudioEffectHighShelfFilter<class_AudioEffectHighShelfFilter>`\

Band-pass and notch filters: :ref:`AudioEffectBandPassFilter<class_AudioEffectBandPassFilter>`, :ref:`AudioEffectBandLimitFilter<class_AudioEffectBandLimitFilter>`, and :ref:`AudioEffectNotchFilter<class_AudioEffectNotchFilter>`\

Bộ lọc low/high-pass: :ref:`AudioEffectLowPassFilter<class_AudioEffectLowPassFilter>` và :ref:`AudioEffectHighPassFilter<class_AudioEffectHighPassFilter>`

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------+--------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                        | :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>` | ``2000.0`` |
   +--------------------------------------------------+--------------------------------------------------------------+------------+
   | :ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` | :ref:`db<class_AudioEffectFilter_property_db>`               | ``0``      |
   +--------------------------------------------------+--------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                        | :ref:`gain<class_AudioEffectFilter_property_gain>`           | ``1.0``    |
   +--------------------------------------------------+--------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                        | :ref:`resonance<class_AudioEffectFilter_property_resonance>` | ``0.5``    |
   +--------------------------------------------------+--------------------------------------------------------------+------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_AudioEffectFilter_FilterDB:

.. rst-class:: classref-enumeration

enum **FilterDB**: :ref:`🔗<enum_AudioEffectFilter_FilterDB>`

.. _class_AudioEffectFilter_constant_FILTER_6DB:

.. rst-class:: classref-enumeration-constant

:ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **FILTER_6DB** = ``0``

Suy giảm 6 dB trên mỗi octave. Một octave có tần số cao hơn gấp đôi :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, hoặc thấp hơn một nửa :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

.. _class_AudioEffectFilter_constant_FILTER_12DB:

.. rst-class:: classref-enumeration-constant

:ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **FILTER_12DB** = ``1``

Suy giảm 12 dB trên mỗi octave. Một octave có tần số cao hơn gấp đôi :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, hoặc thấp hơn một nửa :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

.. _class_AudioEffectFilter_constant_FILTER_18DB:

.. rst-class:: classref-enumeration-constant

:ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **FILTER_18DB** = ``2``

Suy giảm 18 dB trên mỗi octave. Một octave có tần số cao hơn gấp đôi :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, hoặc thấp hơn một nửa :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

.. _class_AudioEffectFilter_constant_FILTER_24DB:

.. rst-class:: classref-enumeration-constant

:ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **FILTER_24DB** = ``3``

Suy giảm 24 dB trên mỗi octave. Một octave có tần số cao hơn gấp đôi :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, hoặc thấp hơn một nửa :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectFilter_property_cutoff_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **cutoff_hz** = ``2000.0`` :ref:`🔗<class_AudioEffectFilter_property_cutoff_hz>`

.. rst-class:: classref-property-setget

- |void| **set_cutoff**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cutoff**\ (\ )

Ngưỡng tần số của bộ lọc, tính bằng Hz. Giá trị có thể nằm trong khoảng từ 1 đến 20500.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectFilter_property_db:

.. rst-class:: classref-property

:ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **db** = ``0`` :ref:`🔗<class_AudioEffectFilter_property_db>`

.. rst-class:: classref-property-setget

- |void| **set_db**\ (\ value\: :ref:`FilterDB<enum_AudioEffectFilter_FilterDB>`\ ) - :ref:`FilterDB<enum_AudioEffectFilter_FilterDB>` **get_db**\ (\ )

Độ dốc của đường cong cutoff theo dB trên mỗi octave (gấp đôi tần số phía trên :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, hoặc bằng một nửa tần số phía dưới :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`), còn được gọi là "bậc" của bộ lọc. Bậc càng cao thì cutoff càng mạnh.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectFilter_property_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **gain** = ``1.0`` :ref:`🔗<class_AudioEffectFilter_property_gain>`

.. rst-class:: classref-property-setget

- |void| **set_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gain**\ (\ )

Gain của các tần số chịu ảnh hưởng bởi bộ lọc. Thuộc tính này chỉ khả dụng cho :ref:`AudioEffectLowShelfFilter<class_AudioEffectLowShelfFilter>` và :ref:`AudioEffectHighShelfFilter<class_AudioEffectHighShelfFilter>`. Giá trị có thể nằm trong khoảng từ 0 đến 4.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectFilter_property_resonance:

.. rst-class:: classref-property

:ref:`float<class_float>` **resonance** = ``0.5`` :ref:`🔗<class_AudioEffectFilter_property_resonance>`

.. rst-class:: classref-property-setget

- |void| **set_resonance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_resonance**\ (\ )

Gain tại hoặc ngay cạnh ngưỡng tần số :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`. Giá trị có thể nằm trong khoảng từ 0 đến 1.

Hành vi chính xác của nó phụ thuộc vào loại bộ lọc được chọn:

- Đối với các bộ lọc shelf, nó làm nổi bật hoặc che bớt bậc bằng cách tăng các tần số ngay cạnh tần số :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>` và giảm các tần số ở phía đối diện.

- Đối với các bộ lọc band-pass và notch, nó mở rộng hoặc thu hẹp bộ lọc tại ngưỡng tần số :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

- Đối với các bộ lọc low/high-pass, nó tăng hoặc giảm các tần số tại ngưỡng tần số :ref:`cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
