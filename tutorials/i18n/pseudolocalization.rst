.. _doc_pseudolocalization:

Bản địa hóa giả lập
===================

Giới thiệu
----------

Khi tạo một trò chơi, quy trình bản địa hóa thường bắt đầu sau khi quá trình phát triển đã hoàn tất. Điều này có nghĩa là trong quá trình phát triển chưa có bản dịch để kiểm tra xem dự án đã được quốc tế hóa đúng cách hay chưa.

Godot cung cấp tính năng bản địa hóa giả lập để kiểm tra mức độ ổn định của dự án khi thay đổi locale. Bản địa hóa giả lập mô phỏng những thay đổi có thể xảy ra trong quá trình bản địa hóa. Nhờ đó, mọi vấn đề liên quan đến quốc tế hóa có thể được nhận diện sớm trong quá trình phát triển.

.. seealso::

    Bạn có thể xem bản địa hóa giả lập hoạt động như thế nào qua `dự án demo Pseudolocalizaton <https://github.com/godotengine/godot-demo-projects/tree/master/gui/pseudolocalization>`__.

Bật và cấu hình bản địa hóa giả lập
-----------------------------------

Việc bật bản địa hóa giả lập và các cấu hình liên quan đơn giản như bật một hộp kiểm trong phần cài đặt dự án. Bạn có thể tìm thấy các thiết lập này tại
:menu:`Project > Project Settings > General > Internationalization > Pseudolocalization` sau khi bật công tắc :button:`Advanced` trong hộp thoại cài đặt dự án:

.. image:: img/pseudolocalization_settings.webp

Bạn cũng có thể :ref:`bật hoặc tắt bản địa hóa giả lập trong runtime từ một script <doc_pseudolocalization_runtime>`.

Các cấu hình bản địa hóa giả lập
--------------------------------

Bản địa hóa giả lập trong Godot có thể được thiết lập tùy theo trường hợp sử dụng cụ thể của dự án. Dưới đây là các thuộc tính bản địa hóa giả lập có thể được cấu hình thông qua phần cài đặt dự án:

- ``replace_with_accents``: Thay thế tất cả ký tự trong chuỗi bằng các biến thể có dấu của chúng. *"The quick brown fox jumped over the lazy dog"* sẽ được chuyển thành *"Ŧh̀é q́üíćḱ ḅŕôŵή f́ôx́ ǰüm̀ṕéd́ ôṽéŕ ŧh̀é łáźý d́ôǵ"* khi thiết lập này được bật. Tính năng này có thể được dùng để phát hiện các chuỗi chưa được dịch vì chúng sẽ không có dấu, đồng thời cũng hữu ích để kiểm tra các glyph bị thiếu trong font được dự án sử dụng.
- ``double_vowels``: Nhân đôi tất cả nguyên âm trong chuỗi. Đây là một cách gần đúng tốt để mô phỏng việc văn bản được mở rộng trong quá trình bản địa hóa. Tính năng này có thể được dùng để kiểm tra những văn bản có thể tràn khỏi vùng chứa của chúng, chẳng hạn như các nút.
- ``fake_bidi``: Văn bản hai chiều giả lập (mô phỏng văn bản từ phải sang trái). Tính năng này hữu ích để mô phỏng các hệ chữ viết từ phải sang trái và kiểm tra những vấn đề bố cục tiềm ẩn có thể xảy ra trong các ngôn ngữ sử dụng hệ chữ viết từ phải sang trái.
- ``override``: Thay thế tất cả ký tự trong chuỗi bằng dấu sao (``*``). Tính năng này hữu ích để nhanh chóng tìm ra những văn bản chưa được bản địa hóa.
- ``expansion_ratio``: Có thể được dùng trong những trường hợp việc nhân đôi nguyên âm chưa đủ gần đúng. Thiết lập này thêm dấu gạch dưới (``_``) vào chuỗi và mở rộng chuỗi theo tỷ lệ đã cho. Tỷ lệ mở rộng ``0.3`` là đủ cho hầu hết trường hợp thực tế; tỷ lệ này sẽ tăng độ dài chuỗi lên 30%.
- ``prefix`` và ``suffix``: Các thuộc tính này có thể được dùng để chỉ định tiền tố và hậu tố bao quanh văn bản.
- ``skip_placeholders``: Bỏ qua các placeholder dùng cho việc định dạng chuỗi, chẳng hạn như ``%s`` và ``%f``. Tính năng này hữu ích để xác định những vị trí cần thêm đối số để chuỗi đã định dạng hiển thị chính xác.

Tất cả các thuộc tính này có thể được bật hoặc tắt tùy theo trường hợp sử dụng của dự án.

.. _doc_pseudolocalization_runtime:

Cấu hình bản địa hóa giả lập trong runtime
------------------------------------------

Có thể bật hoặc tắt bản địa hóa giả lập trong runtime bằng
:ref:`pseudolocalization_enabled<class_TranslationServer_property_pseudolocalization_enabled>` thuộc tính trong TranslationServer. Tuy nhiên, nếu cần cấu hình các thuộc tính bản địa hóa giả lập trong runtime, bạn có thể cấu hình trực tiếp bằng
:ref:`ProjectSettings.set_setting(property, value) <class_ProjectSettings_method_set_setting>` rồi gọi
:ref:`TranslationServer.reload_pseudolocalization() <class_TranslationServer_method_reload_pseudolocalization>`, hàm này phân tích lại các thuộc tính bản địa hóa giả lập và tải lại bản địa hóa giả lập. Đoạn mã sau sẽ bật các thuộc tính ``replace_with_accents`` và ``double_vowels``, sau đó gọi ``reload_pseudolocalization()`` để các thay đổi được áp dụng:

::

    ProjectSettings.set_setting("internationalization/pseudolocalization/replace_with_accents", true)
    ProjectSettings.set_setting("internationalization/pseudolocalization/double_vowels", true)
    TranslationServer.reload_pseudolocalization()
