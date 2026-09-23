.. _doc_localization_using_spreadsheets:

Bản địa hóa bằng bảng tính
==========================

Bảng tính là một trong những định dạng phổ biến nhất để bản địa hóa game. Trong Godot, bảng tính được hỗ trợ thông qua định dạng CSV. Hướng dẫn này giải thích cách làm việc với các tệp CSV.

Các tệp CSV **must** được lưu với mã hóa UTF-8 mà không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`__.

.. warning::

    Theo mặc định, Microsoft Excel luôn lưu các tệp CSV bằng mã hóa ANSI thay vì UTF-8. Không có cách tích hợp sẵn nào để thực hiện việc này, nhưng có các giải pháp thay thế như được mô tả `here <https://stackoverflow.com/questions/4221176/excel-to-csv-with-utf8-encoding>`__.

    Chúng tôi khuyến nghị sử dụng `LibreOffice <https://www.libreoffice.org/>`__ hoặc Google Sheets thay thế.

Định dạng
---------

Các tệp CSV phải được định dạng như sau:

+------+---------+---------+---------+
| keys | <lang1> | <lang2> | <langN> |
+======+=========+=========+=========+
| KEY1 | string  | string  | string  |
+------+---------+---------+---------+
| KEY2 | string  | string  | string  |
+------+---------+---------+---------+
| KEYN | string  | string  | string  |
+------+---------+---------+---------+

Các thẻ "lang" phải đại diện cho một ngôn ngữ, và ngôn ngữ đó phải là một trong các :ref:`valid locales <doc_locales>` được engine hỗ trợ, hoặc phải bắt đầu bằng dấu gạch dưới (``_``), nghĩa là cột tương ứng được dùng làm chú thích và sẽ không được nhập. Các thẻ ``KEY`` phải là duy nhất và đại diện cho một chuỗi có ý nghĩa trên toàn hệ thống. Theo quy ước, chúng thường được viết in hoa để phân biệt với các chuỗi khác. Các key này sẽ được thay thế trong runtime bằng chuỗi đã dịch tương ứng. Lưu ý rằng kiểu chữ rất quan trọng: ``KEY1`` và ``Key1`` sẽ là các key khác nhau. Ô phía trên cùng bên trái sẽ bị bỏ qua và có thể để trống hoặc chứa bất kỳ nội dung nào. Đây là một ví dụ:

+-------+-----------------------+------------------------+------------------------------+
| keys  | en                    | es                     | ja                           |
+=======+=======================+========================+==============================+
| GREET | Hello, friend!        | Hola, amigo!           | こんにちは                   |
+-------+-----------------------+------------------------+------------------------------+
| ASK   | How are you?          | Cómo está?             | 元気ですか                   |
+-------+-----------------------+------------------------+------------------------------+
| BYE   | Goodbye               | Adiós                  | さようなら                   |
+-------+-----------------------+------------------------+------------------------------+
| QUOTE | "Hello" said the man. | "Hola" dijo el hombre. | 「こんにちは」男は言いました |
+-------+-----------------------+------------------------+------------------------------+

Ví dụ tương tự được hiển thị bên dưới dưới dạng tệp văn bản thuần được phân tách bằng dấu phẩy; đây sẽ là kết quả của việc chỉnh sửa ví dụ trên trong bảng tính. Khi chỉnh sửa phiên bản văn bản thuần, hãy chắc chắn đặt trong dấu ngoặc kép mọi thông báo chứa dấu phẩy, dấu ngắt dòng hoặc dấu ngoặc kép, để dấu phẩy không bị phân tích như dấu phân cách, dấu ngắt dòng không tạo các mục mới và dấu ngoặc kép không bị phân tích như ký tự bao quanh. Hãy chắc chắn escape mọi dấu ngoặc kép mà thông báo có thể chứa bằng cách thêm một dấu ngoặc kép khác ngay trước đó. Ngoài ra, bạn có thể chọn một dấu phân cách khác dấu phẩy trong các tùy chọn nhập.

.. code-block:: none

    keys,en,es,ja
    GREET,"Hello, friend!","Hola, amigo!",こんにちは
    ASK,How are you?,Cómo está?,元気ですか
    BYE,Goodbye,Adiós,さようなら
    QUOTE,"""Hello"" said the man.","""Hola"" dijo el hombre.",「こんにちは」男は言いました

Chỉ định dạng số nhiều
~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.6, bạn có thể chỉ định
:ref:`plural forms <doc_internationalizing_games_pluralization>` trong các tệp CSV.

Việc này được thực hiện bằng cách thêm một cột có tên ``?plural`` vào bất kỳ vị trí nào trong bảng (ngoại trừ cột đầu tiên, vốn được dành cho các key dịch). Theo quy ước, bạn nên đặt cột này ở vị trí thứ hai. Lưu ý rằng trong ví dụ dưới đây, cột key là cột chứa bản địa hóa tiếng Anh.

.. code-block:: none

    en,?plural,fr,ru,ja,zh
    ?pluralrule,,nplurals=2; plural=(n >= 2);,,
    There is %d apple,There are %d apples,Il y a %d pomme,Есть %d яблоко,リンゴが%d個あります,那里有%d个苹果
    ,,Il y a %d pommes,Есть %d яблока,,
    ,,,Есть %d яблок,,

.. note::

    Bản dịch Control tự động không được hỗ trợ khi sử dụng dạng số nhiều. Bạn phải dịch chuỗi theo cách thủ công bằng :ref:`tr_n() <class_Object_method_tr_n>`.

Chỉ định ngữ cảnh bản dịch
~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.6, bạn có thể chỉ định
:ref:`translation contexts <doc_internationalizing_games_translation_contexts>` trong các tệp CSV. Tính năng này có thể được dùng để phân biệt các chuỗi nguồn giống hệt nhau nhưng có ý nghĩa khác nhau. Mặc dù thông thường không cần thiết khi sử dụng translation keys ``LIKE_THIS``, tính năng này hữu ích khi dùng văn bản tiếng Anh thuần làm translation keys.

Việc này được thực hiện bằng cách thêm một cột có tên ``?context`` vào bất kỳ vị trí nào trong bảng (ngoại trừ cột đầu tiên, vốn được dành cho các key dịch). Theo quy ước, bạn nên đặt cột này ở vị trí thứ hai hoặc sau ``?plural`` nếu tùy chọn đó cũng được sử dụng. Lưu ý rằng trong ví dụ dưới đây, cột key là cột chứa bản địa hóa tiếng Anh.

.. code-block:: none

    en,?context,fr,ru,ja,zh
    Letter,Alphabet,Lettre,Буква,字母,字母
    Letter,Message,Courrier,Письмо,手紙,信件

.. note::

    Tính năng dịch Automatic Control không được hỗ trợ khi sử dụng context. Bạn phải dịch chuỗi theo cách thủ công bằng :ref:`tr() <class_Object_method_tr>` hoặc :ref:`tr_n() <class_Object_method_tr_n>`.

Trình nhập CSV
--------------

Theo mặc định, Godot sẽ coi các tệp CSV là bản dịch. Godot sẽ nhập các tệp này và tạo một hoặc nhiều tệp tài nguyên bản dịch được nén bên cạnh chúng.

Thao tác nhập cũng sẽ thêm bản dịch vào danh sách các bản dịch cần tải khi trò chơi chạy, được chỉ định trong project.godot (hoặc phần cài đặt dự án). Godot cũng cho phép tải và xóa các bản dịch trong runtime.

Chọn tệp ``.csv`` và mở dock :ui:`Import` để xác định các tùy chọn nhập. Bạn có thể bật hoặc tắt tính năng nén các bản dịch đã nhập, đồng thời chọn dấu phân cách sẽ dùng khi phân tích tệp CSV.

.. image:: img/import_csv.webp

Hãy nhớ nhấp vào :button:`Reimport` sau bất kỳ thay đổi nào đối với các tùy chọn này.

Tải tệp CSV dưới dạng bản dịch
------------------------------

Sau khi tệp CSV được nhập, tệp này **không** được tự động đăng ký làm nguồn bản dịch cho dự án. Hãy nhớ làm theo các bước được mô tả trong
:ref:`doc_internationalizing_games_configuring_imported_translation`
