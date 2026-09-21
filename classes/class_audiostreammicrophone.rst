:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamMicrophone.xml.

.. _class_AudioStreamMicrophone:

AudioStreamMicrophone
=====================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Phát dữ liệu đầu vào âm thanh theo thời gian thực.

.. rst-class:: classref-introduction-group

Mô tả
-----

Khi được sử dụng trực tiếp trong node :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`, **AudioStreamMicrophone** phát lại đầu vào từ microphone theo thời gian thực. Có thể sử dụng kết hợp với :ref:`AudioEffectCapture<class_AudioEffectCapture>` để xử lý hoặc lưu dữ liệu.

\ **Lưu ý:** :ref:`ProjectSettings.audio/driver/enable_input<class_ProjectSettings_property_audio/driver/enable_input>` phải là ``true`` để đầu vào âm thanh hoạt động. Xem thêm phần mô tả của thiết lập đó để biết các lưu ý liên quan đến quyền và thiết lập quyền riêng tư của hệ điều hành.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- :doc:`Recording with microphone <../tutorials/audio/recording_with_microphone>`

- `Audio Mic Record Demo <https://github.com/godotengine/godot-demo-projects/tree/master/audio/mic_record>`__

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
