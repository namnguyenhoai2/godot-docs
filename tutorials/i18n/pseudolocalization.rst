.. _doc_pseudolocalization:

Pseudolocalization
==================

Giới thiệu
----------

Khi tạo một game, quá trình localization thường bắt đầu sau khi quá trình phát triển hoàn tất. Điều này có nghĩa là trong quá trình phát triển không có bản dịch để kiểm tra xem project đã được internationalization đúng cách hay chưa.

Godot cung cấp pseudolocalization như một cách để kiểm tra mức độ vững chắc của project khi thay đổi locale. Pseudolocalization mô phỏng những thay đổi có thể diễn ra trong quá trình localization. Nhờ đó, mọi vấn đề liên quan đến internationalization có thể được nhận diện sớm trong quá trình phát triển.

.. seealso::

    Bạn có thể xem pseudolocalization hoạt động như thế nào trong thực tế bằng cách sử dụng `Pseudolocalizaton demo project <https://github.com/godotengine/godot-demo-projects/tree/master/gui/pseudolocalization>`__.

Bật và cấu hình pseudolocalization
----------------------------------

Việc bật pseudolocalization và các cấu hình liên quan cũng đơn giản như bật một checkbox trong phần cài đặt project. Bạn có thể tìm thấy các cài đặt này trong
:menu:`Project > Project Settings > General > Internationalization > Pseudolocalization`
sau khi bật tùy chọn :button:`Advanced` trong hộp thoại cài đặt project:

.. image:: img/pseudolocalization_settings.webp

Pseudolocalization cũng có thể được :ref:`toggled at runtime from a script <doc_pseudolocalization_runtime>`.

Các cấu hình pseudolocalization
-------------------------------

Pseudolocalization trong Godot có thể được thiết lập tùy theo trường hợp sử dụng cụ thể của project. Dưới đây là các thuộc tính pseudolocalization có thể được cấu hình thông qua phần cài đặt project:

- ``replace_with_accents``: Thay thế tất cả ký tự trong chuỗi bằng các biến thể có dấu của chúng. *"The quick brown fox jumped over the lazy dog"* sẽ được chuyển thành *"Ŧh̀é q́üíćḱ ḅŕôŵή f́ôx́ ǰüm̀ṕéd́ ôṽéŕ ŧh̀é łáźý d́ôǵ"* khi cài đặt này được bật. Có thể dùng tính năng này để phát hiện các chuỗi chưa được dịch vì chúng sẽ không có dấu, đồng thời cũng hữu ích để kiểm tra các glyph bị thiếu trong những font được project sử dụng. - ``double_vowels``: Nhân đôi tất cả nguyên âm trong chuỗi. Đây là một cách gần đúng tốt để mô phỏng việc văn bản mở rộng trong quá trình localization. Có thể dùng tính năng này để kiểm tra những đoạn văn bản sẽ tràn khỏi vùng chứa (chẳng hạn như button). - ``fake_bidi``: Văn bản hai chiều giả (mô phỏng văn bản từ phải sang trái). Tính năng này hữu ích để mô phỏng các hệ thống chữ viết từ phải sang trái và kiểm tra các vấn đề bố cục tiềm ẩn có thể xảy ra trong những ngôn ngữ sử dụng hệ chữ viết từ phải sang trái. - ``override``: Thay thế tất cả ký tự trong chuỗi bằng dấu hoa thị (``*``). Tính năng này hữu ích để nhanh chóng tìm văn bản chưa được localization. - ``expansion_ratio``: Có thể sử dụng trong những trường hợp việc nhân đôi nguyên âm chưa đủ để mô phỏng gần đúng. Cài đặt này thêm các dấu gạch dưới (``_``) vào chuỗi và mở rộng chuỗi theo tỷ lệ đã cho. Tỷ lệ mở rộng ``0.3`` là đủ cho hầu hết trường hợp thực tế; tỷ lệ này sẽ tăng độ dài chuỗi thêm 30%. - ``prefix`` và ``suffix``: Có thể dùng các thuộc tính này để chỉ định tiền tố và hậu tố bao quanh văn bản. - ``skip_placeholders``: Bỏ qua các placeholder dùng cho việc format chuỗi, chẳng hạn như ``%s`` và ``%f``. Tính năng này hữu ích để xác định những vị trí cần thêm đối số nhằm hiển thị chuỗi đã format một cách chính xác.

Tất cả các thuộc tính này có thể được bật hoặc tắt khi cần, tùy theo trường hợp sử dụng của project.

.. _doc_pseudolocalization_runtime:

Cấu hình pseudolocalization trong runtime
-----------------------------------------

Có thể bật hoặc tắt pseudolocalization trong runtime bằng cách sử dụng
:ref:`pseudolocalization_enabled<class_TranslationServer_property_pseudolocalization_enabled>` property
trong TranslationServer. Tuy nhiên, nếu cần cấu hình các thuộc tính pseudolocalization trong runtime, bạn có thể cấu hình trực tiếp bằng cách sử dụng
:ref:`ProjectSettings.set_setting(property, value) <class_ProjectSettings_method_set_setting>`
rồi gọi
:ref:`TranslationServer.reload_pseudolocalization() <class_TranslationServer_method_reload_pseudolocalization>`
hàm này sẽ phân tích lại các thuộc tính pseudolocalization và tải lại pseudolocalization. Đoạn mã sau sẽ bật các thuộc tính ``replace_with_accents`` và ``double_vowels``, sau đó gọi ``reload_pseudolocalization()`` để các thay đổi được áp dụng:

::

    ProjectSettings.set_setting("internationalization/pseudolocalization/replace_with_accents", true)
    ProjectSettings.set_setting("internationalization/pseudolocalization/double_vowels", true)
    TranslationServer.reload_pseudolocalization()
