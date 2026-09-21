:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamGeneratorPlayback.xml.

.. _class_AudioStreamGeneratorPlayback:

AudioStreamGeneratorPlayback
============================

**Kế thừa:** :ref:`AudioStreamPlaybackResampled<class_AudioStreamPlaybackResampled>` **<** :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Phát lại âm thanh được tạo bằng :ref:`AudioStreamGenerator<class_AudioStreamGenerator>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được dùng với :ref:`AudioStreamGenerator<class_AudioStreamGenerator>` để phát lại âm thanh đã tạo theo thời gian thực.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Audio Generator Demo <https://godotengine.org/asset-library/asset/2759>`__

- `Godot 3.2 will get new audio features <https://godotengine.org/article/godot-32-will-get-new-audio-features>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`can_push_buffer<class_AudioStreamGeneratorPlayback_method_can_push_buffer>`\ (\ amount\: :ref:`int<class_int>`\ ) |const|               |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`clear_buffer<class_AudioStreamGeneratorPlayback_method_clear_buffer>`\ (\ )                                                             |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`get_frames_available<class_AudioStreamGeneratorPlayback_method_get_frames_available>`\ (\ ) |const|                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`get_skips<class_AudioStreamGeneratorPlayback_method_get_skips>`\ (\ ) |const|                                                           |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`push_buffer<class_AudioStreamGeneratorPlayback_method_push_buffer>`\ (\ frames\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`push_frame<class_AudioStreamGeneratorPlayback_method_push_frame>`\ (\ frame\: :ref:`Vector2<class_Vector2>`\ )                          |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamGeneratorPlayback_method_can_push_buffer:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_push_buffer**\ (\ amount\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamGeneratorPlayback_method_can_push_buffer>`

Trả về ``true`` nếu một buffer có kích thước ``amount`` có thể được đẩy vào buffer dữ liệu mẫu âm thanh mà không làm tràn buffer, và ``false`` nếu không.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGeneratorPlayback_method_clear_buffer:

.. rst-class:: classref-method

|void| **clear_buffer**\ (\ ) :ref:`🔗<class_AudioStreamGeneratorPlayback_method_clear_buffer>`

Xóa buffer dữ liệu mẫu âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGeneratorPlayback_method_get_frames_available:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_frames_available**\ (\ ) |const| :ref:`🔗<class_AudioStreamGeneratorPlayback_method_get_frames_available>`

Trả về số frame có thể được đẩy vào buffer dữ liệu mẫu âm thanh mà không làm tràn buffer. Nếu kết quả là ``0``, buffer đã đầy.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGeneratorPlayback_method_get_skips:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_skips**\ (\ ) |const| :ref:`🔗<class_AudioStreamGeneratorPlayback_method_get_skips>`

Trả về số lần quá trình phát lại bị bỏ qua do buffer underrun trong dữ liệu mẫu âm thanh. Giá trị này được đặt lại khi bắt đầu phát lại.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGeneratorPlayback_method_push_buffer:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_buffer**\ (\ frames\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_AudioStreamGeneratorPlayback_method_push_buffer>`

Đẩy nhiều frame dữ liệu âm thanh vào buffer. Cách này thường hiệu quả hơn :ref:`push_frame()<class_AudioStreamGeneratorPlayback_method_push_frame>` trong C# và các ngôn ngữ được biên dịch thông qua GDExtension, nhưng :ref:`push_buffer()<class_AudioStreamGeneratorPlayback_method_push_buffer>` có thể *kém* hiệu quả hơn trong GDScript.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamGeneratorPlayback_method_push_frame:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_frame**\ (\ frame\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_AudioStreamGeneratorPlayback_method_push_frame>`

Đẩy một frame dữ liệu âm thanh vào buffer. Cách này thường kém hiệu quả hơn :ref:`push_buffer()<class_AudioStreamGeneratorPlayback_method_push_buffer>` trong C# và các ngôn ngữ được biên dịch thông qua GDExtension, nhưng :ref:`push_frame()<class_AudioStreamGeneratorPlayback_method_push_frame>` có thể *hiệu quả* hơn trong GDScript.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
