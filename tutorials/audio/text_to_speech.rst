.. _doc_text_to_speech:

Chuyển văn bản thành giọng nói
==============================

Cách sử dụng cơ bản
-------------------

Việc sử dụng tính năng chuyển văn bản thành giọng nói cơ bản gồm các bước thực hiện một lần sau:

- Bật TTS trong trình chỉnh sửa Godot cho dự án của bạn
- Truy vấn hệ thống để lấy danh sách các voice có thể sử dụng
- Lưu ID của voice bạn muốn sử dụng

Theo mặc định, cài đặt cấp dự án Godot cho tính năng chuyển văn bản thành giọng nói bị tắt để tránh chi phí xử lý không cần thiết. Để bật tính năng này:

- Đi tới **Project > Project Settings**
- Đảm bảo nút chuyển đổi **Advanced Settings** được bật
- Nhấp vào **Audio > General**
- Đảm bảo tùy chọn **Text to Speech** được chọn
- Khởi động lại Godot nếu được yêu cầu.

Tính năng chuyển văn bản thành giọng nói sử dụng một voice cụ thể. Tùy thuộc vào hệ thống của người dùng, họ có thể đã cài đặt nhiều voice. Khi đã có voice ID, bạn có thể dùng nó để đọc một đoạn văn bản:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Các bước thực hiện một lần.
    # Chọn một voice. Ở đây, chúng ta tùy ý chọn voice tiếng Anh đầu tiên.
    var voices = DisplayServer.tts_get_voices_for_language("en")
    var voice_id = voices[0]

    # Đọc "Hello, world!".
    DisplayServer.tts_speak("Hello, world!", voice_id)

    # Đọc một câu dài hơn, rồi ngắt câu đó.
    # Lưu ý rằng phương thức này là asynchronous: quá trình thực thi ngay lập tức chuyển sang dòng tiếp theo,
    # trước khi voice đọc xong.
    var long_message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur"
    DisplayServer.tts_speak(long_message, voice_id)

    # Ngay lập tức dừng văn bản hiện tại giữa câu và thay vào đó nói lời tạm biệt.
    DisplayServer.tts_stop()
    DisplayServer.tts_speak("Goodbye!", voice_id)

 .. code-tab:: csharp

    // Các bước thực hiện một lần.
    // Chọn một voice. Ở đây, chúng ta tùy ý chọn voice tiếng Anh đầu tiên.
    string[] voices = DisplayServer.TtsGetVoicesForLanguage("en");
    string voiceId = voices[0];

    // Đọc "Hello, world!".
    DisplayServer.TtsSpeak("Hello, world!", voiceId);

    // Đọc một câu dài hơn, rồi ngắt câu đó.
    // Lưu ý rằng phương thức này là asynchronous: quá trình thực thi ngay lập tức chuyển sang dòng tiếp theo,
    // trước khi voice đọc xong.
    string longMessage = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur";
    DisplayServer.TtsSpeak(longMessage, voiceId);

    // Ngay lập tức dừng văn bản hiện tại giữa câu và thay vào đó nói lời tạm biệt.
    DisplayServer.TtsStop();
    DisplayServer.TtsSpeak("Goodbye!", voiceId);


Yêu cầu để tính năng hoạt động
------------------------------

Godot cung cấp chức năng chuyển văn bản thành giọng nói. Bạn có thể tìm thấy các chức năng này trong :ref:`DisplayServer class <class_DisplayServer>`.

Godot phụ thuộc vào các thư viện hệ thống để cung cấp chức năng chuyển văn bản thành giọng nói. Các thư viện này được cài đặt mặc định trên Windows, macOS, Web, Android và iOS, nhưng không có trên mọi bản phân phối Linux. Nếu không có chúng, chức năng chuyển văn bản thành giọng nói sẽ không hoạt động. Cụ thể, ``tts_get_voices()`` method sẽ trả về một danh sách rỗng, cho biết không có voice nào có thể sử dụng.

Cả người dùng Godot trên Linux và người dùng cuối trên Linux chạy game Godot đều cần đảm bảo hệ thống của họ có các thư viện hệ thống cần thiết để tính năng chuyển văn bản thành giọng nói hoạt động. Hãy tham khảo bảng bên dưới hoặc tài liệu của bản phân phối bạn đang dùng để xác định các thư viện cần cài đặt.

Các lệnh một dòng dành riêng cho từng bản phân phối
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+---------------------------------------------------+
| **Arch Linux** | ::                                                |
|                |                                                   |
|                |     pacman -S speech-dispatcher festival espeakup |
+----------------+---------------------------------------------------+

Khắc phục sự cố
---------------

Nếu bạn gặp lỗi `Invalid get index '0' (on base: 'PackedStringArray').` ở dòng `var voice_id = voices[0]`, hãy kiểm tra xem `voices` có mục nào không. Nếu không:

- Tất cả người dùng: đảm bảo bạn đã bật **Text to Speech** trong cài đặt dự án
- Người dùng Linux: đảm bảo bạn đã cài đặt các thư viện dành riêng cho hệ thống để chuyển văn bản thành giọng nói

Các phương pháp hay nhất
------------------------

Xét về trải nghiệm lý tưởng của người chơi khiếm thị, phương pháp tốt nhất cho tính năng chuyển văn bản thành giọng nói là gửi đầu ra đến trình đọc màn hình của người chơi. Cách này giữ nguyên lựa chọn về ngôn ngữ, tốc độ, cao độ, v.v. mà người dùng đã thiết lập, đồng thời cho phép các tính năng nâng cao như cuộn lùi và tiến qua văn bản. Hiện tại, Godot chưa cung cấp mức độ tích hợp này.

Với trạng thái hiện tại của các API chuyển văn bản thành giọng nói trong Godot, các phương pháp hay nhất bao gồm:

- Phát triển game khi đã bật tính năng chuyển văn bản thành giọng nói và đảm bảo mọi thứ đều nghe chính xác
- Cho phép người chơi chọn voice muốn sử dụng và lưu/duy trì lựa chọn đó qua các phiên chơi
- Cho phép người chơi điều chỉnh tốc độ đọc và lưu/duy trì lựa chọn đó qua các phiên chơi

Điều này mang lại cho người chơi khiếm thị sự linh hoạt và thoải mái tối đa khi không sử dụng trình đọc màn hình, đồng thời giảm thiểu khả năng khiến họ thất vọng và cảm thấy bị gạt ra ngoài.

Lưu ý và thông tin khác
-----------------------

- Hãy dự kiến có độ trễ khi gọi `tts_speak` và `tts_stop`. Thời gian trễ thực tế thay đổi tùy thuộc vào cả hệ điều hành lẫn thông số máy của bạn. Điều này đặc biệt quan trọng trên Android và Web, nơi một số voice phụ thuộc vào các dịch vụ web, còn thời gian phát lại thực tế phụ thuộc vào tải máy chủ, độ trễ mạng và các yếu tố khác.
- Văn bản không phải tiếng Anh sẽ hoạt động nếu các voice phù hợp được cài đặt và sử dụng. Trên Windows, bạn có thể tham khảo hướng dẫn trong `this article <this article_>`_ để bật thêm các voice ngôn ngữ trên Windows.
- Các ký tự không phải ASCII, chẳng hạn như ký tự umlaut, sẽ được phát âm chính xác nếu bạn chọn đúng voice.
- Người chơi khiếm thị sử dụng nhiều trình đọc màn hình, bao gồm JAWS, NVDA, VoiceOver, Narrator và các trình đọc khác.
- Các API chuyển văn bản thành giọng nói trên Windows nhìn chung hoạt động tốt hơn các API tương đương trên những hệ thống khác (ví dụ: `tts_stop` theo sau bởi `tts_speak` sẽ đọc ngay thông báo mới).

.. _this article: https://www.ghacks.net/2018/08/11/unlock-all-windows-10-tts-voices-system-wide-to-get-more-of-them/
