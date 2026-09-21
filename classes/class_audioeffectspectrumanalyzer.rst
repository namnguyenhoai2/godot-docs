:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectSpectrumAnalyzer.xml.

.. _class_AudioEffectSpectrumAnalyzer:

AudioEffectSpectrumAnalyzer
===========================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tạo một :ref:`AudioEffectInstance<class_AudioEffectInstance>` thực hiện phân tích tần số và cung cấp các kết quả để truy cập theo thời gian thực.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tính Fourier Transform của tín hiệu âm thanh. Effect này không làm thay đổi âm thanh. Có thể được sử dụng để tạo các hình ảnh trực quan hóa âm thanh theo thời gian thực, chẳng hạn như spectrogram.

Resource này cấu hình một :ref:`AudioEffectSpectrumAnalyzerInstance<class_AudioEffectSpectrumAnalyzerInstance>`, thực hiện quá trình phân tích thực tế trong runtime. Cần lấy một instance bằng :ref:`AudioServer.get_bus_effect_instance()<class_AudioServer_method_get_bus_effect_instance>` để sử dụng effect này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

- `Audio Spectrum Visualizer Demo <https://godotengine.org/asset-library/asset/2762>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------------+--------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                | :ref:`buffer_length<class_AudioEffectSpectrumAnalyzer_property_buffer_length>` | ``2.0`` |
   +----------------------------------------------------------+--------------------------------------------------------------------------------+---------+
   | :ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` | :ref:`fft_size<class_AudioEffectSpectrumAnalyzer_property_fft_size>`           | ``2``   |
   +----------------------------------------------------------+--------------------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_AudioEffectSpectrumAnalyzer_FFTSize:

.. rst-class:: classref-enumeration

enum **FFTSize**: :ref:`🔗<enum_AudioEffectSpectrumAnalyzer_FFTSize>`

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_256:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_256** = ``0``

Sử dụng buffer gồm 256 mẫu cho Fast Fourier transform. Độ trễ thấp nhất nhưng kém ổn định nhất theo thời gian.

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_512:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_512** = ``1``

Sử dụng buffer gồm 512 mẫu cho Fast Fourier transform. Độ trễ thấp nhưng kém ổn định hơn theo thời gian.

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_1024:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_1024** = ``2``

Sử dụng buffer gồm 1024 mẫu cho Fast Fourier transform. Đây là sự cân bằng giữa độ trễ và độ ổn định theo thời gian.

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_2048:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_2048** = ``3``

Sử dụng buffer gồm 2048 mẫu cho Fast Fourier transform. Độ trễ cao nhưng ổn định theo thời gian.

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_4096:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_4096** = ``4``

Sử dụng buffer gồm 4096 mẫu cho Fast Fourier transform. Độ trễ cao nhất nhưng ổn định nhất theo thời gian.

.. _class_AudioEffectSpectrumAnalyzer_constant_FFT_SIZE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **FFT_SIZE_MAX** = ``5``

Biểu diễn kích thước của enum :ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectSpectrumAnalyzer_property_buffer_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **buffer_length** = ``2.0`` :ref:`🔗<class_AudioEffectSpectrumAnalyzer_property_buffer_length>`

.. rst-class:: classref-property-setget

- |void| **set_buffer_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_buffer_length**\ (\ )

Độ dài của buffer cần giữ lại, tính bằng giây. Giá trị cao hơn sẽ giữ dữ liệu lâu hơn nhưng yêu cầu nhiều bộ nhớ hơn. Giá trị có thể nằm trong khoảng từ 0.1 đến 4.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectSpectrumAnalyzer_property_fft_size:

.. rst-class:: classref-property

:ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **fft_size** = ``2`` :ref:`🔗<class_AudioEffectSpectrumAnalyzer_property_fft_size>`

.. rst-class:: classref-property-setget

- |void| **set_fft_size**\ (\ value\: :ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>`\ ) - :ref:`FFTSize<enum_AudioEffectSpectrumAnalyzer_FFTSize>` **get_fft_size**\ (\ )

Kích thước của buffer `Fast Fourier transform <https://en.wikipedia.org/wiki/Fast_Fourier_transform>`__. Giá trị cao hơn làm mượt quá trình phân tích phổ theo thời gian nhưng có độ trễ lớn hơn. Ảnh hưởng của độ trễ cao hơn này đặc biệt dễ nhận thấy khi biên độ thay đổi đột ngột.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
