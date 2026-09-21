:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/mp3/doc_classes/AudioStreamMP3.xml.

.. _class_AudioStreamMP3:

AudioStreamMP3
==============

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Trình điều khiển luồng âm thanh MP3.

.. rst-class:: classref-introduction-group

Mô tả
-----

Trình điều khiển luồng âm thanh MP3. Xem :ref:`data<class_AudioStreamMP3_property_data>` nếu bạn muốn tải tệp MP3 tại thời điểm runtime. Có thể tìm thêm thông tin trong :ref:`ResourceImporterMP3<class_ResourceImporterMP3>`.

\ **Lưu ý:** Lớp này có thể tùy chọn hỗ trợ các định dạng MP1 và MP2 cũ, với điều kiện engine được biên dịch cùng tùy chọn SCons ``minimp3_extra_formats=yes``. Các định dạng bổ sung này không được bật theo mặc định.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- :doc:`Runtime file loading and saving <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                         | :ref:`bar_beats<class_AudioStreamMP3_property_bar_beats>`     | ``4``                 |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                         | :ref:`beat_count<class_AudioStreamMP3_property_beat_count>`   | ``0``                 |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                     | :ref:`bpm<class_AudioStreamMP3_property_bpm>`                 | ``0.0``               |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`data<class_AudioStreamMP3_property_data>`               | ``PackedByteArray()`` |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                       | :ref:`loop<class_AudioStreamMP3_property_loop>`               | ``false``             |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                     | :ref:`loop_offset<class_AudioStreamMP3_property_loop_offset>` | ``0.0``               |
   +-----------------------------------------------+---------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamMP3<class_AudioStreamMP3>` | :ref:`load_from_buffer<class_AudioStreamMP3_method_load_from_buffer>`\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |static| |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamMP3<class_AudioStreamMP3>` | :ref:`load_from_file<class_AudioStreamMP3_method_load_from_file>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                              |
   +---------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamMP3_property_bar_beats:

.. rst-class:: classref-property

:ref:`int<class_int>` **bar_beats** = ``4`` :ref:`🔗<class_AudioStreamMP3_property_bar_beats>`

.. rst-class:: classref-property-setget

- |void| **set_bar_beats**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bar_beats**\ (\ )

Số nhịp trong một ô nhịp của track âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_property_beat_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **beat_count** = ``0`` :ref:`🔗<class_AudioStreamMP3_property_beat_count>`

.. rst-class:: classref-property-setget

- |void| **set_beat_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_beat_count**\ (\ )

Độ dài của track âm thanh, tính bằng nhịp. Thời lượng thực tế của tệp âm thanh có thể dài hơn giá trị được chỉ ra bởi thuộc tính này. Thuộc tính này xác định điểm kết thúc của âm thanh để lặp, :ref:`AudioStreamPlaylist<class_AudioStreamPlaylist>`, và :ref:`AudioStreamInteractive<class_AudioStreamInteractive>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_property_bpm:

.. rst-class:: classref-property

:ref:`float<class_float>` **bpm** = ``0.0`` :ref:`🔗<class_AudioStreamMP3_property_bpm>`

.. rst-class:: classref-property-setget

- |void| **set_bpm**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bpm**\ (\ )

Nhịp độ của track âm thanh, được đo bằng số nhịp mỗi phút.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_property_data:

.. rst-class:: classref-property

:ref:`PackedByteArray<class_PackedByteArray>` **data** = ``PackedByteArray()`` :ref:`🔗<class_AudioStreamMP3_property_data>`

.. rst-class:: classref-property-setget

- |void| **set_data**\ (\ value\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) - :ref:`PackedByteArray<class_PackedByteArray>` **get_data**\ (\ )

Chứa dữ liệu âm thanh dưới dạng byte.

Bạn có thể tải tệp mà không cần import tệp trước bằng đoạn mã dưới đây. Hãy nhớ rằng đoạn mã này tải toàn bộ tệp vào bộ nhớ và có thể không phù hợp với các tệp rất lớn (hàng trăm megabyte trở lên).


.. tabs::

 .. code-tab:: gdscript

    func load_mp3(path):
        var file = FileAccess.open(path, FileAccess.READ)
        var sound = AudioStreamMP3.new()
        sound.data = file.get_buffer(file.get_length())
        return sound

 .. code-tab:: csharp

    public AudioStreamMP3 LoadMP3(string path)
    {
        using var file = FileAccess.Open(path, FileAccess.ModeFlags.Read);
        var sound = new AudioStreamMP3();
        sound.Data = file.GetBuffer(file.GetLength());
        return sound;
    }



**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedByteArray<class_PackedByteArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_property_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **loop** = ``false`` :ref:`🔗<class_AudioStreamMP3_property_loop>`

.. rst-class:: classref-property-setget

- |void| **set_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_loop**\ (\ )

Nếu ``true``, luồng sẽ phát lại từ :ref:`loop_offset<class_AudioStreamMP3_property_loop_offset>` được chỉ định khi đến cuối track âm thanh, hoặc khi đến cuối nhịp cuối cùng theo số lượng được chỉ định trong :ref:`beat_count<class_AudioStreamMP3_property_beat_count>`. Hữu ích cho âm thanh môi trường và nhạc nền.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_property_loop_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **loop_offset** = ``0.0`` :ref:`🔗<class_AudioStreamMP3_property_loop_offset>`

.. rst-class:: classref-property-setget

- |void| **set_loop_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_loop_offset**\ (\ )

Thời điểm tính bằng giây mà luồng bắt đầu sau khi được lặp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamMP3_method_load_from_buffer:

.. rst-class:: classref-method

:ref:`AudioStreamMP3<class_AudioStreamMP3>` **load_from_buffer**\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |static| :ref:`🔗<class_AudioStreamMP3_method_load_from_buffer>`

Tạo một instance **AudioStreamMP3** mới từ buffer đã cho. Buffer phải chứa dữ liệu MP3.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamMP3_method_load_from_file:

.. rst-class:: classref-method

:ref:`AudioStreamMP3<class_AudioStreamMP3>` **load_from_file**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_AudioStreamMP3_method_load_from_file>`

Tạo một instance **AudioStreamMP3** mới từ đường dẫn tệp đã cho. Tệp phải ở định dạng MP3.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
