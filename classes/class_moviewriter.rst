:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/MovieWriter.xml.

.. _class_MovieWriter:

MovieWriter
===========

**Kế thừa:** :ref:`Object<class_Object>`

Lớp trừu tượng dành cho các encoder ghi video không theo thời gian thực.

.. rst-class:: classref-introduction-group

Mô tả
-----

Godot có thể ghi video bằng mô phỏng không theo thời gian thực. Giống như ``--fixed-fps`` :doc:`đối số dòng lệnh <../tutorials/editor/command_line_tutorial>`, tùy chọn này buộc ``delta`` được báo cáo trong các hàm :ref:`Node._process()<class_Node_private_method__process>` phải giống hệt nhau giữa các frame, bất kể thời gian thực tế cần để render frame là bao lâu. Bạn có thể dùng tùy chọn này để ghi video chất lượng cao với nhịp frame hoàn hảo bất kể khả năng phần cứng của bạn.

Godot có 3 **MovieWriter** tích hợp sẵn\ s:

- Container OGV với Theora cho video và Vorbis cho audio (phần mở rộng tệp ``.ogv``). Nén mất dữ liệu, kích thước tệp trung bình, encoding nhanh. Có thể điều chỉnh chất lượng nén mất dữ liệu bằng cách thay đổi :ref:`ProjectSettings.editor/movie_writer/video_quality<class_ProjectSettings_property_editor/movie_writer/video_quality>` và :ref:`ProjectSettings.editor/movie_writer/ogv/audio_quality<class_ProjectSettings_property_editor/movie_writer/ogv/audio_quality>`. Tệp kết quả có thể được xem trong Godot bằng :ref:`VideoStreamPlayer<class_VideoStreamPlayer>` và hầu hết trình phát video, nhưng không thể xem trong trình duyệt web vì các trình duyệt này không hỗ trợ Theora.

- Container AVI với MJPEG cho video và audio không nén (phần mở rộng tệp ``.avi``). Nén mất dữ liệu, kích thước tệp trung bình, encoding nhanh. Có thể điều chỉnh chất lượng nén mất dữ liệu bằng cách thay đổi :ref:`ProjectSettings.editor/movie_writer/video_quality<class_ProjectSettings_property_editor/movie_writer/video_quality>`. Tệp kết quả có thể được xem trong hầu hết trình phát video, nhưng phải được chuyển đổi sang định dạng khác để xem trên web hoặc bằng Godot với :ref:`VideoStreamPlayer<class_VideoStreamPlayer>`. MJPEG không hỗ trợ độ trong suốt. Đầu ra AVI hiện bị giới hạn ở tệp có kích thước tối đa 4 GB.

- Chuỗi ảnh PNG cho video và WAV cho audio (phần mở rộng tệp ``.png``). Nén không mất dữ liệu, kích thước tệp lớn, encoding chậm. Được thiết kế để encode thành tệp video bằng một công cụ khác như `FFmpeg <https://ffmpeg.org/>`__ sau khi ghi. Hiện chưa hỗ trợ độ trong suốt, ngay cả khi viewport gốc được đặt ở chế độ trong suốt.

Nếu cần encode sang định dạng khác hoặc pipe một stream qua phần mềm của bên thứ ba, bạn có thể mở rộng lớp **MovieWriter** để tạo movie writer của riêng mình. Vì lý do hiệu năng, thông thường bạn nên thực hiện việc này bằng GDExtension.

\ **Sử dụng trong editor:** Có thể chỉ định đường dẫn tệp movie mặc định trong :ref:`ProjectSettings.editor/movie_writer/movie_file<class_ProjectSettings_property_editor/movie_writer/movie_file>`. Ngoài ra, khi chạy các scene riêng lẻ, có thể thêm metadata ``movie_file`` vào node gốc để chỉ định đường dẫn đến tệp movie sẽ được dùng khi ghi scene đó. Sau khi đặt đường dẫn, hãy nhấp vào biểu tượng cuộn phim ở góc trên bên phải của editor để bật chế độ Movie Maker, rồi chạy bất kỳ scene nào như bình thường. Engine sẽ bắt đầu ghi ngay sau khi màn hình splash kết thúc và chỉ dừng ghi khi engine thoát. Nhấp lại vào biểu tượng cuộn phim để tắt chế độ Movie Maker. Lưu ý rằng việc bật hoặc tắt chế độ Movie Maker không ảnh hưởng đến các instance của project đang chạy.

\ **Lưu ý:** MovieWriter có thể được sử dụng cả trong editor và các project đã export, nhưng *không* được thiết kế để người dùng cuối ghi video trong khi chơi. Người chơi muốn ghi video gameplay nên cài đặt các công cụ như `OBS Studio <https://obsproject.com/>`__ hoặc `SimpleScreenRecorder <https://www.maartenbaert.be/simplescreenrecorder/>`__ thay thế.

\ **Lưu ý:** Việc hỗ trợ MJPEG (phần mở rộng tệp ``.avi``) phụ thuộc vào module ``jpg`` được bật trong thời gian compile (hành vi mặc định).

\ **Lưu ý:** Việc hỗ trợ OGV (phần mở rộng tệp ``.ogv``) phụ thuộc vào module ``theora`` được bật trong thời gian compile (hành vi mặc định). Chỉ các binary của editor mới hỗ trợ nén Theora.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`_get_audio_mix_rate<class_MovieWriter_private_method__get_audio_mix_rate>`\ (\ ) |virtual| |required| |const|                                                                                               |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SpeakerMode<enum_AudioServer_SpeakerMode>`  | :ref:`_get_audio_speaker_mode<class_MovieWriter_private_method__get_audio_speaker_mode>`\ (\ ) |virtual| |required| |const|                                                                                       |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`_get_supported_extensions<class_MovieWriter_private_method__get_supported_extensions>`\ (\ ) |virtual| |required| |const|                                                                                   |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`_handles_file<class_MovieWriter_private_method__handles_file>`\ (\ path\: :ref:`String<class_String>`\ ) |virtual| |required| |const|                                                                       |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`_write_begin<class_MovieWriter_private_method__write_begin>`\ (\ movie_size\: :ref:`Vector2i<class_Vector2i>`, fps\: :ref:`int<class_int>`, base_path\: :ref:`String<class_String>`\ ) |virtual| |required| |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`_write_end<class_MovieWriter_private_method__write_end>`\ (\ ) |virtual| |required|                                                                                                                         |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`_write_frame<class_MovieWriter_private_method__write_frame>`\ (\ frame_image\: :ref:`Image<class_Image>`, audio_frame_block\: ``const void*``\ ) |virtual| |required|                                       |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_writer<class_MovieWriter_method_add_writer>`\ (\ writer\: :ref:`MovieWriter<class_MovieWriter>`\ ) |static|                                                                                             |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MovieWriter_private_method__get_audio_mix_rate:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_audio_mix_rate**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MovieWriter_private_method__get_audio_mix_rate>`

Được gọi khi engine yêu cầu sample rate audio được dùng để ghi audio. Giá trị trả về phải được chỉ định theo Hz. Mặc định là 48000 Hz nếu :ref:`_get_audio_mix_rate()<class_MovieWriter_private_method__get_audio_mix_rate>` không được override.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__get_audio_speaker_mode:

.. rst-class:: classref-method

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **_get_audio_speaker_mode**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MovieWriter_private_method__get_audio_speaker_mode>`

Được gọi khi engine yêu cầu speaker mode audio được dùng để ghi audio. Tùy chọn này có thể ảnh hưởng đến số lượng kênh đầu ra trong tệp/stream audio kết quả. Mặc định là :ref:`AudioServer.SPEAKER_MODE_STEREO<class_AudioServer_constant_SPEAKER_MODE_STEREO>` nếu :ref:`_get_audio_speaker_mode()<class_MovieWriter_private_method__get_audio_speaker_mode>` không được override.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__get_supported_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_supported_extensions**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MovieWriter_private_method__get_supported_extensions>`

Trả về danh sách các phần mở rộng tên tệp được hỗ trợ cho các movie được ghi bằng **MovieWriter** này.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__handles_file:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_handles_file**\ (\ path\: :ref:`String<class_String>`\ ) |virtual| |required| |const| :ref:`🔗<class_MovieWriter_private_method__handles_file>`

Được gọi khi engine xác định liệu **MovieWriter** này có thể xử lý tệp tại ``path`` hay không. Phải trả về ``true`` nếu **MovieWriter** này có thể xử lý đường dẫn tệp đã cho, nếu không thì trả về ``false``. Thông thường, :ref:`_handles_file()<class_MovieWriter_private_method__handles_file>` được override như sau để cho phép người dùng ghi tệp tại bất kỳ đường dẫn nào với phần mở rộng tệp đã cho:

::

    func _handles_file(path):
        # Cho phép chỉ định tệp đầu ra với phần mở rộng tệp `.mkv` (không phân biệt chữ hoa chữ thường),
        # either in the Project Settings or with the `--write-movie <path>` command line argument.
        return path.get_extension().to_lower() == "mkv"

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__write_begin:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_write_begin**\ (\ movie_size\: :ref:`Vector2i<class_Vector2i>`, fps\: :ref:`int<class_int>`, base_path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_MovieWriter_private_method__write_begin>`

Được gọi một lần trước khi engine bắt đầu ghi dữ liệu video và audio. ``movie_size`` là chiều rộng và chiều cao của video cần lưu. ``fps`` là số frame mỗi giây được chỉ định trong project settings hoặc bằng ``--fixed-fps <fps>`` :doc:`đối số dòng lệnh <../tutorials/editor/command_line_tutorial>`.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__write_end:

.. rst-class:: classref-method

|void| **_write_end**\ (\ ) |virtual| |required| :ref:`🔗<class_MovieWriter_private_method__write_end>`

Được gọi khi engine hoàn tất việc ghi. Điều này xảy ra khi engine thoát bằng cách nhấn nút đóng của window manager hoặc khi :ref:`SceneTree.quit()<class_SceneTree_method_quit>` được gọi.

\ **Lưu ý:** Nhấn :kbd:`Ctrl + C` trên terminal đang chạy editor/project *không* khiến :ref:`_write_end()<class_MovieWriter_private_method__write_end>` được gọi.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_private_method__write_frame:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_write_frame**\ (\ frame_image\: :ref:`Image<class_Image>`, audio_frame_block\: ``const void*``\ ) |virtual| |required| :ref:`🔗<class_MovieWriter_private_method__write_frame>`

Được gọi ở cuối mỗi frame đã render. Các đối số hàm ``frame_image`` và ``audio_frame_block`` phải được ghi.

.. rst-class:: classref-item-separator

----

.. _class_MovieWriter_method_add_writer:

.. rst-class:: classref-method

|void| **add_writer**\ (\ writer\: :ref:`MovieWriter<class_MovieWriter>`\ ) |static| :ref:`🔗<class_MovieWriter_method_add_writer>`

Thêm một writer để engine có thể sử dụng. Có thể thiết lập các phần mở rộng tệp được hỗ trợ bằng cách override :ref:`_handles_file()<class_MovieWriter_private_method__handles_file>`.

\ **Lưu ý:** Phải gọi :ref:`add_writer()<class_MovieWriter_method_add_writer>` đủ sớm trong quá trình khởi tạo engine để phương thức này hoạt động, vì việc ghi movie được thiết kế để bắt đầu cùng lúc với phần còn lại của engine.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
