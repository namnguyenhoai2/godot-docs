:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectSpectrumAnalyzerInstance.xml.

.. _class_AudioEffectSpectrumAnalyzerInstance:

AudioEffectSpectrumAnalyzerInstance
===================================

**Kế thừa:** :ref:`AudioEffectInstance<class_AudioEffectInstance>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Instance có thể truy vấn của một :ref:`AudioEffectSpectrumAnalyzer<class_AudioEffectSpectrumAnalyzer>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Phần runtime của một :ref:`AudioEffectSpectrumAnalyzer<class_AudioEffectSpectrumAnalyzer>`, có thể được dùng để truy vấn độ lớn của một dải tần trên bus chủ của nó.

Có thể lấy một instance của class này bằng :ref:`AudioServer.get_bus_effect_instance()<class_AudioServer_method_get_bus_effect_instance>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

- `Audio Spectrum Visualizer Demo <https://godotengine.org/asset-library/asset/2762>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_magnitude_for_frequency_range<class_AudioEffectSpectrumAnalyzerInstance_method_get_magnitude_for_frequency_range>`\ (\ from_hz\: :ref:`float<class_float>`, to_hz\: :ref:`float<class_float>`, mode\: :ref:`MagnitudeMode<enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode>` = 1\ ) |const| |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode:

.. rst-class:: classref-enumeration

enum **MagnitudeMode**: :ref:`🔗<enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode>`

.. _class_AudioEffectSpectrumAnalyzerInstance_constant_MAGNITUDE_AVERAGE:

.. rst-class:: classref-enumeration-constant

:ref:`MagnitudeMode<enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode>` **MAGNITUDE_AVERAGE** = ``0``

Sử dụng giá trị trung bình trên toàn bộ dải tần làm độ lớn.

.. _class_AudioEffectSpectrumAnalyzerInstance_constant_MAGNITUDE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`MagnitudeMode<enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode>` **MAGNITUDE_MAX** = ``1``

Sử dụng giá trị lớn nhất của dải tần làm độ lớn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffectSpectrumAnalyzerInstance_method_get_magnitude_for_frequency_range:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_magnitude_for_frequency_range**\ (\ from_hz\: :ref:`float<class_float>`, to_hz\: :ref:`float<class_float>`, mode\: :ref:`MagnitudeMode<enum_AudioEffectSpectrumAnalyzerInstance_MagnitudeMode>` = 1\ ) |const| :ref:`🔗<class_AudioEffectSpectrumAnalyzerInstance_method_get_magnitude_for_frequency_range>`

Trả về độ lớn của các tần số từ ``from_hz`` đến ``to_hz`` dưới dạng năng lượng tuyến tính dưới dạng một Vector2. Thành phần ``x`` của giá trị trả về biểu thị kênh stereo trái, còn ``y`` biểu thị kênh phải.

\ ``mode`` xác định cách dải tần sẽ được xử lý.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
