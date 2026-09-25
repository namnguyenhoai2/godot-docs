.. _doc_internationalizing_plugins:

Quốc tế hóa plugin
==================

Tương tự như cách :ref:`doc_internationalizing_games` hoạt động, bạn có thể tạo bản dịch cho các editor plugin. Mọi điều áp dụng cho game cũng áp dụng cho plugin, nhưng quy trình bật bản dịch cho plugin hơi khác một chút.

Sau khi tạo tệp CSV hoặc POT và tạo các bản dịch, bạn không thể chỉ cần tải các bản dịch trong phần cài đặt dự án; thay vào đó, bạn phải thông qua :ref:`class_TranslationServer` để thêm một :ref:`class_TranslationDomain` mới.

.. code-block::

    func _enter_tree():
        var domain = TranslationServer.get_or_add_domain("addons/my_plugin")
        var dir = "res://addons/my_plugin/locale"
        for file in DirAccess.get_files_at(dir):
            var translation = ResourceLoader.load(dir.path_join(file)) as Translation
            if translation:
                domain.add_translation(translation)

        # Đang khởi tạo plugin hiện có...

Đoạn mã trên sẽ tải tất cả bản dịch hiện có cho plugin của bạn, với điều kiện các bản dịch nằm trong thư mục ``addons/my_plugin/locale``. Bạn cũng nên chọn một tên miền bản dịch duy nhất để tránh xung đột với các tên miền khác; sử dụng đường dẫn của plugin làm tên miền sẽ đảm bảo điều này.

Nếu xét dock từ :ref:`doc_making_plugins_custom_dock`, giờ bạn cần cho dock biết sử dụng tên miền bản dịch này:

.. code-block::

    dock.set_translation_domain("addons/my_plugin")

Điều cuối cùng bạn cần làm là xóa tên miền bản dịch khi plugin bị vô hiệu hóa:

.. code-block::

    func _exit_tree():
        # Đang dọn dẹp plugin hiện có...
        TranslationServer.remove_domain("addons/my_plugin")

Sau khi hoàn tất mọi việc, bạn có thể thay đổi ngôn ngữ của editor để kiểm tra các bản dịch.

.. note::

    Bạn sẽ cần vô hiệu hóa rồi bật lại plugin một lần, vì plugin cần gọi
    :ref:`_enter_tree() <class_Node_private_method__enter_tree>` để tải các bản dịch.
