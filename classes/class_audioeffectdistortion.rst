:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectDistortion.xml.

.. _class_AudioEffectDistortion:

AudioEffectDistortion
=====================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng distortion vào một audio bus.

Ánh xạ lại các mẫu âm thanh bằng một hàm phi tuyến để tạo ra âm thanh bị distortion.

.. rst-class:: classref-introduction-group

Mô tả
-----

Hiệu ứng "distortion" thay đổi dạng sóng thông qua một hàm toán học phi tuyến (xem các hàm hiện có trong :ref:`Mode<enum_AudioEffectDistortion_Mode>`), dựa trên biên độ của các mẫu trong dạng sóng.

\ **Lưu ý:** Trong một hàm phi tuyến, một mẫu đầu vào có giá trị biên độ *x* sẽ có biên độ được tăng hoặc giảm thành giá trị *y*, dựa trên giá trị của hàm tại *x*. Vì vậy, ngay cả khi cùng :ref:`drive<class_AudioEffectDistortion_property_drive>`, âm thanh đầu ra vẫn sẽ thay đổi tùy theo âm lượng đầu vào. Để thay đổi âm lượng mà vẫn giữ nguyên dạng sóng đầu ra, hãy sử dụng :ref:`post_gain<class_AudioEffectDistortion_property_post_gain>`.

Trong hiệu ứng này, mỗi kiểu là một hàm phi tuyến khác nhau. Các kiểu hiện có gồm: clip, atan, lofi (bitcrush), overdrive và waveshape. Mọi kiểu distortion hiện có ở đây đều đối xứng: các giá trị biên độ âm bị tác động theo cùng cách với các giá trị dương.

Mặc dù distortion luôn thay đổi thành phần tần số, thường bằng cách tạo thêm các họa âm cao, những kiểu distortion khác nhau mang lại nhiều chất âm đa dạng; từ "mềm" và "ấm" đến "giòn" và "gắt".

Đối với game, hiệu ứng này có thể mô phỏng rất hiệu quả âm thanh phát ra từ một thiết bị hoặc loa bị bão hòa. Nó cũng có thể giúp âm thanh nổi bật hơn trong một bản phối bằng cách thêm các tần số cao hơn và tăng âm lượng.

\ **Lưu ý:** Mặc dù thường không thể nhận biết, một hiệu ứng distortion đang được bật vẫn sẽ thay đổi âm thanh ngay cả khi :ref:`drive<class_AudioEffectDistortion_property_drive>` được đặt thành 0. Đây không phải là lỗi. Nếu không mong muốn hành vi này, hãy cân nhắc vô hiệu hóa hiệu ứng bằng :ref:`AudioServer.set_bus_effect_enabled()<class_AudioServer_method_set_bus_effect_enabled>`.

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

   +----------------------------------------------+--------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                    | :ref:`drive<class_AudioEffectDistortion_property_drive>`           | ``0.0``     |
   +----------------------------------------------+--------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                    | :ref:`keep_hf_hz<class_AudioEffectDistortion_property_keep_hf_hz>` | ``16000.0`` |
   +----------------------------------------------+--------------------------------------------------------------------+-------------+
   | :ref:`Mode<enum_AudioEffectDistortion_Mode>` | :ref:`mode<class_AudioEffectDistortion_property_mode>`             | ``0``       |
   +----------------------------------------------+--------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                    | :ref:`post_gain<class_AudioEffectDistortion_property_post_gain>`   | ``0.0``     |
   +----------------------------------------------+--------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                    | :ref:`pre_gain<class_AudioEffectDistortion_property_pre_gain>`     | ``0.0``     |
   +----------------------------------------------+--------------------------------------------------------------------+-------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioEffectDistortion_Mode:

.. rst-class:: classref-enumeration

enum **Mode**: :ref:`🔗<enum_AudioEffectDistortion_Mode>`

.. _class_AudioEffectDistortion_constant_MODE_CLIP:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **MODE_CLIP** = ``0``

Làm phẳng dạng sóng tại 0 dB theo cách sắc nét. :ref:`drive<class_AudioEffectDistortion_property_drive>` làm tăng biên độ của các mẫu theo cấp số nhân. Chế độ này hoạt động như một hard clipper nếu :ref:`drive<class_AudioEffectDistortion_property_drive>` được đặt thành 0, và là chế độ duy nhất cắt các tín hiệu âm thanh tại 0 dB.

.. _class_AudioEffectDistortion_constant_MODE_ATAN:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **MODE_ATAN** = ``1``

Làm phẳng dạng sóng theo cách mượt mà, theo một đường cong arctangent. Âm thanh giảm âm lượng trước khi làm phẳng các đỉnh thành ``PI * 4.0`` (giá trị tuyến tính), nếu trước đó đã được chuẩn hóa.

.. _class_AudioEffectDistortion_constant_MODE_LOFI:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **MODE_LOFI** = ``2``

Giảm độ sâu bit của âm thanh để tạo ra tín hiệu âm thanh có độ phân giải thấp, từ 16-bit xuống 2-bit. Có thể dùng để mô phỏng âm thanh của các thiết bị âm thanh kỹ thuật số đời đầu.

.. _class_AudioEffectDistortion_constant_MODE_OVERDRIVE:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **MODE_OVERDRIVE** = ``3``

Mô phỏng distortion ấm do một transistor hiệu ứng trường tạo ra, loại transistor thường được sử dụng trong các bộ khuếch đại nhạc cụ thể rắn. :ref:`drive<class_AudioEffectDistortion_property_drive>` không có tác dụng trong chế độ này.

.. _class_AudioEffectDistortion_constant_MODE_WAVESHAPE:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **MODE_WAVESHAPE** = ``4``

Làm phẳng dạng sóng theo cách mượt mà cho đến khi đạt đỉnh sắc nét tại ``drive = 1``, theo một hàm sigmoid tuyệt đối tổng quát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectDistortion_property_drive:

.. rst-class:: classref-property

:ref:`float<class_float>` **drive** = ``0.0`` :ref:`🔗<class_AudioEffectDistortion_property_drive>`

.. rst-class:: classref-property-setget

- |void| **set_drive**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drive**\ (\ )

Cường độ distortion. Kiểm soát mức độ âm thanh đầu vào bị tác động bởi đường cong distortion bằng cách chuyển từ hàm tuyến tính sang hàm phi tuyến. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDistortion_property_keep_hf_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **keep_hf_hz** = ``16000.0`` :ref:`🔗<class_AudioEffectDistortion_property_keep_hf_hz>`

.. rst-class:: classref-property-setget

- |void| **set_keep_hf_hz**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_keep_hf_hz**\ (\ )

Bộ lọc high-pass, tính bằng Hz. Các tần số cao hơn giá trị này sẽ không bị distortion tác động. Giá trị có thể nằm trong khoảng từ 1 đến 20000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDistortion_property_mode:

.. rst-class:: classref-property

:ref:`Mode<enum_AudioEffectDistortion_Mode>` **mode** = ``0`` :ref:`🔗<class_AudioEffectDistortion_property_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mode**\ (\ value\: :ref:`Mode<enum_AudioEffectDistortion_Mode>`\ ) - :ref:`Mode<enum_AudioEffectDistortion_Mode>` **get_mode**\ (\ )

Kiểu distortion. Thay đổi hàm phi tuyến được sử dụng để làm distortion dạng sóng. Xem :ref:`Mode<enum_AudioEffectDistortion_Mode>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDistortion_property_post_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **post_gain** = ``0.0`` :ref:`🔗<class_AudioEffectDistortion_property_post_gain>`

.. rst-class:: classref-property-setget

- |void| **set_post_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_post_gain**\ (\ )

Gain sau hiệu ứng, tính bằng dB. Giá trị có thể nằm trong khoảng từ -80 đến 24.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDistortion_property_pre_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **pre_gain** = ``0.0`` :ref:`🔗<class_AudioEffectDistortion_property_pre_gain>`

.. rst-class:: classref-property-setget

- |void| **set_pre_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pre_gain**\ (\ )

Gain trước hiệu ứng, tính bằng dB. Giá trị có thể nằm trong khoảng từ -60 đến 60.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
