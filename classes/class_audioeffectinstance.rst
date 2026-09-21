:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectInstance.xml.

.. _class_AudioEffectInstance:

AudioEffectInstance
===================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioEffectSpectrumAnalyzerInstance<class_AudioEffectSpectrumAnalyzerInstance>`

Thao tác với âm thanh mà nó nhận được cho một hiệu ứng nhất định.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một audio effect instance thao tác với âm thanh mà nó nhận được cho một hiệu ứng nhất định. Instance này được :ref:`AudioEffect<class_AudioEffect>` tự động tạo khi được thêm vào một bus và thường không nên được tạo trực tiếp. Nếu cần, có thể lấy instance này trong lúc chạy bằng :ref:`AudioServer.get_bus_effect_instance()<class_AudioServer_method_get_bus_effect_instance>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_process<class_AudioEffectInstance_private_method__process>`\ (\ src_buffer\: ``const void*``, r_dst_buffer\: ``AudioFrame*``, frame_count\: :ref:`int<class_int>`\ ) |virtual| |required| |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`_process_silence<class_AudioEffectInstance_private_method__process_silence>`\ (\ ) |virtual| |const|                                                                                       |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffectInstance_private_method__process:

.. rst-class:: classref-method

|void| **_process**\ (\ src_buffer\: ``const void*``, r_dst_buffer\: ``AudioFrame*``, frame_count\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_AudioEffectInstance_private_method__process>`

Được :ref:`AudioServer<class_AudioServer>` gọi để xử lý hiệu ứng này. Khi :ref:`_process_silence()<class_AudioEffectInstance_private_method__process_silence>` không được override hoặc trả về ``false``, phương thức này chỉ được gọi khi bus đang hoạt động.

\ **Lưu ý:** Override phương thức này trong GDScript hoặc C# không có tác dụng. Chỉ GDExtension mới có thể tận dụng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectInstance_private_method__process_silence:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_process_silence**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioEffectInstance_private_method__process_silence>`

Override phương thức này để tùy chỉnh hành vi xử lý của instance hiệu ứng này.

Nên trả về ``true`` để buộc :ref:`AudioServer<class_AudioServer>` luôn gọi :ref:`_process()<class_AudioEffectInstance_private_method__process>`, ngay cả khi bus đã bị tắt tiếng hoặc không thể nghe thấy vì lý do khác.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
