:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectPitchShift.xml.

.. _class_AudioEffectPitchShift:

AudioEffectPitchShift
=====================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng thay đổi cao độ âm thanh vào một audio bus.

Tăng hoặc giảm cao độ của âm thanh đầu vào.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cho phép điều chế cao độ mà không thay đổi tốc độ. Tất cả các tần số đều có thể được tăng hoặc giảm với ảnh hưởng tối thiểu đến các transient.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+------------------------------------------------------------------------+---------+
   | :ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` | :ref:`fft_size<class_AudioEffectPitchShift_property_fft_size>`         | ``3``   |
   +----------------------------------------------------+------------------------------------------------------------------------+---------+
   | :ref:`int<class_int>`                              | :ref:`oversampling<class_AudioEffectPitchShift_property_oversampling>` | ``4``   |
   +----------------------------------------------------+------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                          | :ref:`pitch_scale<class_AudioEffectPitchShift_property_pitch_scale>`   | ``1.0`` |
   +----------------------------------------------------+------------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_AudioEffectPitchShift_FFTSize:

.. rst-class:: classref-enumeration

enum **FFTSize**: :ref:`🔗<enum_AudioEffectPitchShift_FFTSize>`

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_256:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_256** = ``0``

Sử dụng buffer gồm 256 sample cho phép biến đổi Fourier nhanh (Fast Fourier transform). Độ trễ thấp nhất nhưng kém ổn định nhất theo thời gian.

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_512:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_512** = ``1``

Sử dụng buffer gồm 512 sample cho phép biến đổi Fourier nhanh (Fast Fourier transform). Độ trễ thấp nhưng kém ổn định hơn theo thời gian.

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_1024:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_1024** = ``2``

Sử dụng buffer gồm 1024 sample cho phép biến đổi Fourier nhanh (Fast Fourier transform). Đây là sự cân bằng giữa độ trễ và độ ổn định theo thời gian.

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_2048:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_2048** = ``3``

Sử dụng buffer gồm 2048 sample cho phép biến đổi Fourier nhanh (Fast Fourier transform). Độ trễ cao nhưng ổn định theo thời gian.

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_4096:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_4096** = ``4``

Sử dụng buffer gồm 4096 sample cho phép biến đổi Fourier nhanh (Fast Fourier transform). Độ trễ cao nhất nhưng ổn định nhất theo thời gian.

.. _class_AudioEffectPitchShift_constant_FFT_SIZE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **FFT_SIZE_MAX** = ``5``

Biểu thị kích thước của enum :ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectPitchShift_property_fft_size:

.. rst-class:: classref-property

:ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **fft_size** = ``3`` :ref:`🔗<class_AudioEffectPitchShift_property_fft_size>`

.. rst-class:: classref-property-setget

- |void| **set_fft_size**\ (\ value\: :ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>`\ ) - :ref:`FFTSize<enum_AudioEffectPitchShift_FFTSize>` **get_fft_size**\ (\ )

Kích thước của buffer `Fast Fourier transform <https://en.wikipedia.org/wiki/Fast_Fourier_transform>`__. Giá trị cao hơn sẽ làm hiệu ứng mượt hơn theo thời gian nhưng có độ trễ lớn hơn. Ảnh hưởng của độ trễ cao hơn này đặc biệt dễ nhận thấy trên các tín hiệu âm thanh có thay đổi biên độ đột ngột.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPitchShift_property_oversampling:

.. rst-class:: classref-property

:ref:`int<class_int>` **oversampling** = ``4`` :ref:`🔗<class_AudioEffectPitchShift_property_oversampling>`

.. rst-class:: classref-property-setget

- |void| **set_oversampling**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_oversampling**\ (\ )

Hệ số oversampling cần sử dụng. Giá trị cao hơn cho chất lượng tốt hơn nhưng đòi hỏi CPU nhiều hơn và có thể gây rè âm thanh nếu CPU không xử lý kịp.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectPitchShift_property_pitch_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **pitch_scale** = ``1.0`` :ref:`🔗<class_AudioEffectPitchShift_property_pitch_scale>`

.. rst-class:: classref-property-setget

- |void| **set_pitch_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pitch_scale**\ (\ )

Hệ số cao độ cần sử dụng. ``1.0`` là cao độ mặc định và phát âm thanh không bị ảnh hưởng. :ref:`pitch_scale<class_AudioEffectPitchShift_property_pitch_scale>` có thể nằm trong khoảng từ 0 (cao độ thấp vô hạn, không thể nghe thấy) đến 16 (cao hơn 16 lần so với cao độ ban đầu).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
