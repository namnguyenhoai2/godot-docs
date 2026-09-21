:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectRecord.xml.

.. _class_AudioEffectRecord:

AudioEffectRecord
=================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Hiệu ứng âm thanh dùng để ghi âm thanh từ một audio bus.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cho phép người dùng ghi âm thanh từ một audio bus vào :ref:`AudioStreamWAV<class_AudioStreamWAV>`. Khi được sử dụng trên audio bus Master, hiệu ứng này bao gồm toàn bộ âm thanh do Godot xuất ra.

Không giống :ref:`AudioEffectCapture<class_AudioEffectCapture>`, hiệu ứng này mã hóa bản ghi theo định dạng đã cho (8-bit, 16-bit hoặc nén) thay vì cho phép truy cập vào các mẫu âm thanh thô.

Có thể được sử dụng (với một :ref:`AudioStreamMicrophone<class_AudioStreamMicrophone>`) để ghi âm từ microphone.

\ **Lưu ý:** :ref:`ProjectSettings.audio/driver/enable_input<class_ProjectSettings_property_audio/driver/enable_input>` phải là ``true`` để đầu vào âm thanh hoạt động. Xem thêm phần mô tả của thiết lập đó để biết các lưu ý liên quan đến quyền và cài đặt quyền riêng tư của hệ điều hành.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Recording with microphone <../tutorials/audio/recording_with_microphone>`

- `Audio Microphone Record Demo <https://godotengine.org/asset-library/asset/2760>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------+--------------------------------------------------------+-------+
   | :ref:`Format<enum_AudioStreamWAV_Format>` | :ref:`format<class_AudioEffectRecord_property_format>` | ``1`` |
   +-------------------------------------------+--------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamWAV<class_AudioStreamWAV>` | :ref:`get_recording<class_AudioEffectRecord_method_get_recording>`\ (\ ) |const|                                         |
   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                     | :ref:`is_recording_active<class_AudioEffectRecord_method_is_recording_active>`\ (\ ) |const|                             |
   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | |void|                                      | :ref:`set_recording_active<class_AudioEffectRecord_method_set_recording_active>`\ (\ record\: :ref:`bool<class_bool>`\ ) |
   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectRecord_property_format:

.. rst-class:: classref-property

:ref:`Format<enum_AudioStreamWAV_Format>` **format** = ``1`` :ref:`🔗<class_AudioEffectRecord_property_format>`

.. rst-class:: classref-property-setget

- |void| **set_format**\ (\ value\: :ref:`Format<enum_AudioStreamWAV_Format>`\ ) - :ref:`Format<enum_AudioStreamWAV_Format>` **get_format**\ (\ )

Chỉ định định dạng mà sample sẽ được ghi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffectRecord_method_get_recording:

.. rst-class:: classref-method

:ref:`AudioStreamWAV<class_AudioStreamWAV>` **get_recording**\ (\ ) |const| :ref:`🔗<class_AudioEffectRecord_method_get_recording>`

Trả về sample đã ghi.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectRecord_method_is_recording_active:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_recording_active**\ (\ ) |const| :ref:`🔗<class_AudioEffectRecord_method_is_recording_active>`

Trả về việc bản ghi có đang hoạt động hay không.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectRecord_method_set_recording_active:

.. rst-class:: classref-method

|void| **set_recording_active**\ (\ record\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioEffectRecord_method_set_recording_active>`

Nếu ``true``, âm thanh sẽ được ghi. Lưu ý rằng việc khởi động lại quá trình ghi sẽ xóa sample đã ghi trước đó.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
