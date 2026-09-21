:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamWAV.xml.

.. _class_AudioStreamWAV:

AudioStreamWAV
==============

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lưu trữ dữ liệu âm thanh được tải từ các tệp WAV.

.. rst-class:: classref-introduction-group

Mô tả
-----

AudioStreamWAV stores sound samples loaded from WAV files. To play the stored sound, use an :ref:`AudioStreamPlayer<class_AudioStreamPlayer>` (for non-positional audio) or :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>`/:ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>` (for positional audio). The sound can be looped.

Lớp này cũng có thể được dùng để lưu trữ dữ liệu âm thanh PCM được tạo động. Xem thêm :ref:`AudioStreamGenerator<class_AudioStreamGenerator>` để biết về việc tạo âm thanh theo thủ tục.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- :doc:`Runtime file loading and saving <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`data<class_AudioStreamWAV_property_data>`             | ``PackedByteArray()`` |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`Format<enum_AudioStreamWAV_Format>`     | :ref:`format<class_AudioStreamWAV_property_format>`         | ``0``                 |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                         | :ref:`loop_begin<class_AudioStreamWAV_property_loop_begin>` | ``0``                 |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                         | :ref:`loop_end<class_AudioStreamWAV_property_loop_end>`     | ``0``                 |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` | :ref:`loop_mode<class_AudioStreamWAV_property_loop_mode>`   | ``0``                 |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                         | :ref:`mix_rate<class_AudioStreamWAV_property_mix_rate>`     | ``44100``             |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                       | :ref:`stereo<class_AudioStreamWAV_property_stereo>`         | ``false``             |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+
   | :ref:`Dictionary<class_Dictionary>`           | :ref:`tags<class_AudioStreamWAV_property_tags>`             | ``{}``                |
   +-----------------------------------------------+-------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamWAV<class_AudioStreamWAV>` | :ref:`load_from_buffer<class_AudioStreamWAV_method_load_from_buffer>`\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`, options\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static| |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamWAV<class_AudioStreamWAV>` | :ref:`load_from_file<class_AudioStreamWAV_method_load_from_file>`\ (\ path\: :ref:`String<class_String>`, options\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static|                              |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`save_to_wav<class_AudioStreamWAV_method_save_to_wav>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                 |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioStreamWAV_Format:

.. rst-class:: classref-enumeration

enum **Format**: :ref:`🔗<enum_AudioStreamWAV_Format>`

.. _class_AudioStreamWAV_constant_FORMAT_8_BITS:

.. rst-class:: classref-enumeration-constant

:ref:`Format<enum_AudioStreamWAV_Format>` **FORMAT_8_BITS** = ``0``

Bộ mã hóa âm thanh PCM 8-bit.

.. _class_AudioStreamWAV_constant_FORMAT_16_BITS:

.. rst-class:: classref-enumeration-constant

:ref:`Format<enum_AudioStreamWAV_Format>` **FORMAT_16_BITS** = ``1``

Bộ mã hóa âm thanh PCM 16-bit.

.. _class_AudioStreamWAV_constant_FORMAT_IMA_ADPCM:

.. rst-class:: classref-enumeration-constant

:ref:`Format<enum_AudioStreamWAV_Format>` **FORMAT_IMA_ADPCM** = ``2``

Âm thanh được nén mất dữ liệu bằng IMA ADPCM.

.. _class_AudioStreamWAV_constant_FORMAT_QOA:

.. rst-class:: classref-enumeration-constant

:ref:`Format<enum_AudioStreamWAV_Format>` **FORMAT_QOA** = ``3``

Âm thanh được nén mất dữ liệu bằng `Quite OK Audio <https://qoaformat.org/>`__.

.. rst-class:: classref-item-separator

----

.. _enum_AudioStreamWAV_LoopMode:

.. rst-class:: classref-enumeration

enum **LoopMode**: :ref:`🔗<enum_AudioStreamWAV_LoopMode>`

.. _class_AudioStreamWAV_constant_LOOP_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **LOOP_DISABLED** = ``0``

Âm thanh không lặp lại.

.. _class_AudioStreamWAV_constant_LOOP_FORWARD:

.. rst-class:: classref-enumeration-constant

:ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **LOOP_FORWARD** = ``1``

Âm thanh lặp lại dữ liệu giữa :ref:`loop_begin<class_AudioStreamWAV_property_loop_begin>` và :ref:`loop_end<class_AudioStreamWAV_property_loop_end>`, chỉ phát theo chiều tiến.

.. _class_AudioStreamWAV_constant_LOOP_PINGPONG:

.. rst-class:: classref-enumeration-constant

:ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **LOOP_PINGPONG** = ``2``

Âm thanh lặp lại dữ liệu giữa :ref:`loop_begin<class_AudioStreamWAV_property_loop_begin>` và :ref:`loop_end<class_AudioStreamWAV_property_loop_end>`, phát tiến và lùi.

.. _class_AudioStreamWAV_constant_LOOP_BACKWARD:

.. rst-class:: classref-enumeration-constant

:ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **LOOP_BACKWARD** = ``3``

Âm thanh lặp lại dữ liệu giữa :ref:`loop_begin<class_AudioStreamWAV_property_loop_begin>` và :ref:`loop_end<class_AudioStreamWAV_property_loop_end>`, chỉ phát theo chiều lùi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamWAV_property_data:

.. rst-class:: classref-property

:ref:`PackedByteArray<class_PackedByteArray>` **data** = ``PackedByteArray()`` :ref:`🔗<class_AudioStreamWAV_property_data>`

.. rst-class:: classref-property-setget

- |void| **set_data**\ (\ value\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) - :ref:`PackedByteArray<class_PackedByteArray>` **get_data**\ (\ )

Chứa dữ liệu âm thanh dưới dạng byte.

\ **Lưu ý:** Nếu :ref:`format<class_AudioStreamWAV_property_format>` được đặt thành :ref:`FORMAT_8_BITS<class_AudioStreamWAV_constant_FORMAT_8_BITS>`, thuộc tính này yêu cầu dữ liệu PCM 8-bit có dấu. Để chuyển đổi từ PCM 8-bit không dấu, hãy trừ 128 khỏi mỗi byte.

\ **Lưu ý:** Nếu :ref:`format<class_AudioStreamWAV_property_format>` được đặt thành :ref:`FORMAT_QOA<class_AudioStreamWAV_constant_FORMAT_QOA>`, thuộc tính này yêu cầu dữ liệu từ một tệp QOA hoàn chỉnh.

**Lưu ý:** Mảng được trả về là một *bản sao* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedByteArray<class_PackedByteArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_format:

.. rst-class:: classref-property

:ref:`Format<enum_AudioStreamWAV_Format>` **format** = ``0`` :ref:`🔗<class_AudioStreamWAV_property_format>`

.. rst-class:: classref-property-setget

- |void| **set_format**\ (\ value\: :ref:`Format<enum_AudioStreamWAV_Format>`\ ) - :ref:`Format<enum_AudioStreamWAV_Format>` **get_format**\ (\ )

Định dạng âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_loop_begin:

.. rst-class:: classref-property

:ref:`int<class_int>` **loop_begin** = ``0`` :ref:`🔗<class_AudioStreamWAV_property_loop_begin>`

.. rst-class:: classref-property-setget

- |void| **set_loop_begin**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_loop_begin**\ (\ )

Điểm bắt đầu lặp (tính theo số mẫu, tương đối với phần đầu của stream).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_loop_end:

.. rst-class:: classref-property

:ref:`int<class_int>` **loop_end** = ``0`` :ref:`🔗<class_AudioStreamWAV_property_loop_end>`

.. rst-class:: classref-property-setget

- |void| **set_loop_end**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_loop_end**\ (\ )

Điểm kết thúc lặp (tính theo số mẫu, tương đối với phần đầu của stream).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_loop_mode:

.. rst-class:: classref-property

:ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **loop_mode** = ``0`` :ref:`🔗<class_AudioStreamWAV_property_loop_mode>`

.. rst-class:: classref-property-setget

- |void| **set_loop_mode**\ (\ value\: :ref:`LoopMode<enum_AudioStreamWAV_LoopMode>`\ ) - :ref:`LoopMode<enum_AudioStreamWAV_LoopMode>` **get_loop_mode**\ (\ )

Chế độ lặp.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_mix_rate:

.. rst-class:: classref-property

:ref:`int<class_int>` **mix_rate** = ``44100`` :ref:`🔗<class_AudioStreamWAV_property_mix_rate>`

.. rst-class:: classref-property-setget

- |void| **set_mix_rate**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_mix_rate**\ (\ )

Tần số lấy mẫu dùng để trộn âm thanh này. Giá trị cao hơn cần nhiều không gian lưu trữ hơn nhưng cho chất lượng tốt hơn.

Trong trò chơi, các tần số lấy mẫu phổ biến được sử dụng là ``11025``, ``16000``, ``22050``, ``32000``, ``44100`` và ``48000``.

Theo `Nyquist-Shannon sampling theorem <https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem>`__, tai người không nhận thấy sự khác biệt về chất lượng khi vượt quá 40.000 Hz (vì hầu hết mọi người chỉ có thể nghe đến khoảng ~20.000 Hz, thường thấp hơn). Nếu bạn sử dụng các âm thanh có cao độ thấp hơn như giọng nói, các tần số lấy mẫu thấp hơn như ``32000`` hoặc ``22050`` có thể được sử dụng mà không làm giảm chất lượng.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_stereo:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **stereo** = ``false`` :ref:`🔗<class_AudioStreamWAV_property_stereo>`

.. rst-class:: classref-property-setget

- |void| **set_stereo**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_stereo**\ (\ )

Nếu ``true``, âm thanh là stereo.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_property_tags:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **tags** = ``{}`` :ref:`🔗<class_AudioStreamWAV_property_tags>`

.. rst-class:: classref-property-setget

- |void| **set_tags**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_tags**\ (\ )

Chứa các tag do người dùng định nghĩa nếu được tìm thấy trong dữ liệu WAV.

Các tag thường được sử dụng gồm ``title``, ``artist``, ``album``, ``tracknumber`` và ``date`` (``date`` không có định dạng ngày tiêu chuẩn).

\ **Lưu ý:** Không có tag nào được *đảm bảo* xuất hiện trong mọi tệp, vì vậy hãy đảm bảo xử lý trường hợp các key không tồn tại.

\ **Lưu ý:** Hiện chỉ hỗ trợ các tệp WAV sử dụng một chunk ``LIST`` có mã định danh ``INFO`` để mã hóa tag.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamWAV_method_load_from_buffer:

.. rst-class:: classref-method

:ref:`AudioStreamWAV<class_AudioStreamWAV>` **load_from_buffer**\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`, options\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static| :ref:`🔗<class_AudioStreamWAV_method_load_from_buffer>`

Tạo một instance **AudioStreamWAV** mới từ buffer đã cho. Buffer phải chứa dữ liệu WAV.

Các key và value của ``options`` khớp với các thuộc tính của :ref:`ResourceImporterWAV<class_ResourceImporterWAV>`. Cách sử dụng ``options`` giống hệt :ref:`load_from_file()<class_AudioStreamWAV_method_load_from_file>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_method_load_from_file:

.. rst-class:: classref-method

:ref:`AudioStreamWAV<class_AudioStreamWAV>` **load_from_file**\ (\ path\: :ref:`String<class_String>`, options\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static| :ref:`🔗<class_AudioStreamWAV_method_load_from_file>`

Tạo một instance **AudioStreamWAV** mới từ đường dẫn tệp đã cho. Tệp phải ở định dạng WAV.

Các key và value của ``options`` khớp với các thuộc tính của :ref:`ResourceImporterWAV<class_ResourceImporterWAV>`.

\ **Ví dụ:** Tải tệp đầu tiên được thả vào dưới dạng WAV và phát tệp đó:

::

    @onready var audio_player = $AudioStreamPlayer

    func _ready():
        get_window().files_dropped.connect(_on_files_dropped)

    func _on_files_dropped(files):
        if files[0].get_extension() == "wav":
            audio_player.stream = AudioStreamWAV.load_from_file(files[0], {
                    "force/max_rate": true,
                    "force/max_rate_hz": 11025
                })
            audio_player.play()

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamWAV_method_save_to_wav:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save_to_wav**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AudioStreamWAV_method_save_to_wav>`

Lưu AudioStreamWAV thành một tệp WAV tại ``path``. Không thể lưu các mẫu ở định dạng IMA ADPCM hoặc Quite OK Audio.

\ **Lưu ý:** Phần mở rộng ``.wav`` sẽ được tự động thêm vào ``path`` nếu bị thiếu.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
