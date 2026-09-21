:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectCapture.xml.

.. _class_AudioEffectCapture:

AudioEffectCapture
==================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các mẫu âm thanh từ một audio bus theo thời gian thực để có thể truy cập chúng dưới dạng dữ liệu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Sao chép tất cả các khung âm thanh, còn được gọi là "samples" hoặc "audio samples", từ audio bus được gắn vào bộ đệm vòng nội bộ. Effect này không làm thay đổi âm thanh. Có thể dùng để lưu trữ dữ liệu âm thanh theo thời gian thực nhằm phát lại và tạo các hình ảnh trực quan hóa âm thanh theo thời gian thực, chẳng hạn như oscilloscope.

Mã ứng dụng nên lấy các khung âm thanh này từ bộ đệm vòng bằng :ref:`get_buffer()<class_AudioEffectCapture_method_get_buffer>` rồi xử lý theo nhu cầu, chẳng hạn như thu thập dữ liệu từ một :ref:`AudioStreamMicrophone<class_AudioStreamMicrophone>`, triển khai các effect do ứng dụng định nghĩa hoặc truyền âm thanh qua mạng. Khi thu thập dữ liệu âm thanh từ microphone, định dạng của các mẫu sẽ là PCM dấu phẩy động stereo 32-bit.

Không giống :ref:`AudioEffectRecord<class_AudioEffectRecord>`, effect này chỉ trả về các mẫu âm thanh thô thay vì mã hóa chúng thành một :ref:`AudioStream<class_AudioStream>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`buffer_length<class_AudioEffectCapture_property_buffer_length>` | ``0.1`` |
   +---------------------------+-----------------------------------------------------------------------+---------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`can_get_buffer<class_AudioEffectCapture_method_can_get_buffer>`\ (\ frames\: :ref:`int<class_int>`\ ) |const| |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_buffer<class_AudioEffectCapture_method_clear_buffer>`\ (\ )                                             |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`get_buffer<class_AudioEffectCapture_method_get_buffer>`\ (\ frames\: :ref:`int<class_int>`\ )                 |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_buffer_length_frames<class_AudioEffectCapture_method_get_buffer_length_frames>`\ (\ ) |const|             |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_discarded_frames<class_AudioEffectCapture_method_get_discarded_frames>`\ (\ ) |const|                     |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_frames_available<class_AudioEffectCapture_method_get_frames_available>`\ (\ ) |const|                     |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_pushed_frames<class_AudioEffectCapture_method_get_pushed_frames>`\ (\ ) |const|                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectCapture_property_buffer_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **buffer_length** = ``0.1`` :ref:`🔗<class_AudioEffectCapture_property_buffer_length>`

.. rst-class:: classref-property-setget

- |void| **set_buffer_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_buffer_length**\ (\ )

Độ dài của bộ đệm vòng nội bộ, tính bằng giây. Giá trị cao hơn sẽ giữ dữ liệu lâu hơn, nhưng cần nhiều bộ nhớ hơn. Giá trị có thể nằm trong khoảng từ 0.01 đến 10.

\ **Lưu ý:** Việc đặt độ dài bộ đệm sẽ không có tác dụng nếu bộ đệm đã được khởi tạo.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffectCapture_method_can_get_buffer:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_get_buffer**\ (\ frames\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioEffectCapture_method_can_get_buffer>`

Trả về ``true`` nếu có ít nhất ``frames`` mẫu để đọc trong bộ đệm vòng nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_clear_buffer:

.. rst-class:: classref-method

|void| **clear_buffer**\ (\ ) :ref:`🔗<class_AudioEffectCapture_method_clear_buffer>`

Xóa bộ đệm vòng nội bộ.

\ **Lưu ý:** Gọi phương thức này trong khi đang thu âm có thể làm mất các mẫu, gây ra tiếng lộp bộp khi phát lại.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_get_buffer:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_buffer**\ (\ frames\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioEffectCapture_method_get_buffer>`

Lấy ``frames`` mẫu tiếp theo từ bộ đệm vòng nội bộ.

Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa chính xác ``frames`` mẫu nếu có đủ, hoặc một :ref:`PackedVector2Array<class_PackedVector2Array>` rỗng nếu không có đủ dữ liệu.

Các mẫu là PCM dấu phẩy động có dấu trong khoảng từ ``-1`` đến ``1``. Bạn sẽ phải scale chúng nếu muốn sử dụng dưới dạng mẫu số nguyên 8 hoặc 16-bit. (``v = 0x7fff * samples[0].x``)

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_get_buffer_length_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_buffer_length_frames**\ (\ ) |const| :ref:`🔗<class_AudioEffectCapture_method_get_buffer_length_frames>`

Trả về tổng kích thước của bộ đệm vòng nội bộ, tính bằng số lượng mẫu.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_get_discarded_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_discarded_frames**\ (\ ) |const| :ref:`🔗<class_AudioEffectCapture_method_get_discarded_frames>`

Trả về số lượng mẫu bị loại bỏ khỏi audio bus do bộ đệm đầy.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_get_frames_available:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_frames_available**\ (\ ) |const| :ref:`🔗<class_AudioEffectCapture_method_get_frames_available>`

Trả về số lượng mẫu có thể đọc bằng :ref:`get_buffer()<class_AudioEffectCapture_method_get_buffer>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCapture_method_get_pushed_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_pushed_frames**\ (\ ) |const| :ref:`🔗<class_AudioEffectCapture_method_get_pushed_frames>`

Trả về số lượng mẫu đã được chèn từ audio bus.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
