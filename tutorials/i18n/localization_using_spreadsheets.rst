.. _doc_localization_using_spreadsheets:

Bản địa hóa bằng bảng tính
==========================

Bảng tính là một trong những định dạng phổ biến nhất để bản địa hóa game. Trong Godot, bảng tính được hỗ trợ thông qua định dạng CSV. Hướng dẫn này giải thích cách làm việc với các tệp CSV.

Các tệp CSV **phải** được lưu bằng mã hóa UTF-8 không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`__.

.. warning::

    Theo mặc định, Microsoft Excel luôn lưu các tệp CSV bằng mã hóa ANSI thay vì UTF-8. Không có cách tích hợp sẵn để thực hiện việc này, nhưng có các giải pháp thay thế như được mô tả `here <https://stackoverflow.com/questions/4221176/excel-to-csv-with-utf8-encoding>`__.

    Thay vào đó, chúng tôi khuyến nghị sử dụng `LibreOffice <https://www.libreoffice.org/>`__ hoặc Google Sheets.

Định dạng
---------

Các tệp CSV phải được định dạng như sau:

+--------+----------+----------+----------+
| keys   | <lang1>  | <lang2>  | <langN>  |
+========+==========+==========+==========+
| KEY1   | string   | string   | string   |
+--------+----------+----------+----------+
| KEY2   | string   | string   | string   |
+--------+----------+----------+----------+
| KEYN   | string   | string   | string   |
+--------+----------+----------+----------+

Các thẻ "lang" phải đại diện cho một ngôn ngữ, ngôn ngữ đó phải là một trong các :ref:`valid locales <doc_locales>` được engine hỗ trợ, hoặc phải bắt đầu bằng dấu gạch dưới (``_``), nghĩa là cột tương ứng được coi là chú thích và sẽ không được nhập. Các thẻ ``KEY`` phải là duy nhất và đại diện cho một chuỗi mang tính phổ quát. Theo quy ước, chúng thường được viết in hoa để phân biệt với các chuỗi khác. Các khóa này sẽ được thay thế lúc runtime bằng chuỗi bản dịch tương ứng. Lưu ý rằng kiểu chữ rất quan trọng: ``KEY1`` và ``Key1`` sẽ là các khóa khác nhau. Ô trên cùng bên trái bị bỏ qua và có thể để trống hoặc chứa bất kỳ nội dung nào. Dưới đây là một ví dụ:

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

Ví dụ tương tự được hiển thị bên dưới dưới dạng tệp văn bản thuần túy, phân tách bằng dấu phẩy; đây sẽ là kết quả khi chỉnh sửa nội dung trên trong một bảng tính. Khi chỉnh sửa phiên bản văn bản thuần túy, hãy đặt trong dấu ngoặc kép mọi thông báo chứa dấu phẩy, dấu ngắt dòng hoặc dấu ngoặc kép, để dấu phẩy không bị phân tích thành dấu phân cách, dấu ngắt dòng không tạo ra mục mới và dấu ngoặc kép không bị phân tích thành ký tự bao quanh. Hãy escape mọi dấu ngoặc kép có thể xuất hiện trong thông báo bằng cách đặt thêm một dấu ngoặc kép trước chúng. Ngoài ra, bạn có thể chọn một dấu phân cách khác dấu phẩy trong các tùy chọn nhập.

.. code-block:: none

    keys,en,es,ja
    GREET,"Hello, friend!","Hola, amigo!",こんにちは
    ASK,How are you?,Cómo está?,元気ですか
    BYE,Goodbye,Adiós,さようなら
    QUOTE,"""Hello"" said the man.","""Hola"" dijo el hombre.",「こんにちは」男は言いました

Chỉ định các dạng số nhiều
~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.6, bạn có thể chỉ định
:ref:`plural forms <doc_internationalizing_games_pluralization>` in CSV files.

Việc này được thực hiện bằng cách thêm một cột có tên ``?plural`` ở bất kỳ vị trí nào trong bảng (ngoại trừ cột đầu tiên, vốn được dành cho các khóa bản dịch). Theo quy ước, bạn nên đặt cột này ở vị trí thứ hai. Lưu ý rằng trong ví dụ bên dưới, cột khóa là cột chứa bản địa hóa tiếng Anh.

.. code-block:: none

    en,?plural,fr,ru,ja,zh
    ?pluralrule,,nplurals=2; plural=(n >= 2);,,
    There is %d apple,There are %d apples,Il y a %d pomme,Есть %d яблоко,リンゴが%d個あります,那里有%d个苹果
    ,,Il y a %d pommes,Есть %d яблока,,
    ,,,Есть %d яблок,,

.. note::

    Bản dịch Control tự động không được hỗ trợ khi sử dụng các dạng số nhiều. Bạn phải dịch chuỗi theo cách thủ công bằng :ref:`tr_n() <class_Object_method_tr_n>`.

Chỉ định ngữ cảnh bản dịch
~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.6, bạn có thể chỉ định
:ref:`translation contexts <doc_internationalizing_games_translation_contexts>`
trong các tệp CSV. Tính năng này có thể được dùng để phân biệt các chuỗi nguồn giống hệt nhau nhưng có ý nghĩa khác nhau. Mặc dù điều này thường không cần thiết khi sử dụng các khóa bản dịch ``LIKE_THIS``, nó rất hữu ích khi dùng văn bản tiếng Anh thuần túy làm khóa bản dịch.

Việc này được thực hiện bằng cách thêm một cột có tên ``?context`` ở bất kỳ vị trí nào trong bảng (ngoại trừ cột đầu tiên, vốn được dành cho các khóa bản dịch). Theo quy ước, bạn nên đặt cột này ở vị trí thứ hai hoặc sau ``?plural`` nếu cũng sử dụng nó. Lưu ý rằng trong ví dụ bên dưới, cột khóa là cột chứa bản địa hóa tiếng Anh.

.. code-block:: none

    en,?context,fr,ru,ja,zh
    Letter,Alphabet,Lettre,Буква,字母,字母
    Letter,Message,Courrier,Письмо,手紙,信件

.. note::

    Bản dịch Control tự động không được hỗ trợ khi sử dụng ngữ cảnh. Bạn phải dịch chuỗi theo cách thủ công bằng :ref:`tr() <class_Object_method_tr>` hoặc :ref:`tr_n() <class_Object_method_tr_n>`.

Trình nhập CSV
--------------

Theo mặc định, Godot sẽ coi các tệp CSV là bản dịch. Godot sẽ nhập chúng và tạo một hoặc nhiều tệp tài nguyên bản dịch đã nén bên cạnh tệp đó.

Việc nhập cũng sẽ thêm bản dịch vào danh sách các bản dịch cần tải khi game chạy, được chỉ định trong project.godot (hoặc phần cài đặt project). Godot cũng cho phép tải và xóa bản dịch trong runtime.

Chọn tệp ``.csv`` và mở dock :ui:`Import` để xác định các tùy chọn nhập. Bạn có thể bật hoặc tắt tính năng nén các bản dịch đã nhập, cũng như chọn dấu phân cách được sử dụng khi phân tích tệp CSV.

.. image:: img/import_csv.webp

Hãy nhớ nhấp vào :button:`Reimport` sau mỗi thay đổi đối với các tùy chọn này.

Tải tệp CSV dưới dạng bản dịch
------------------------------

Sau khi tệp CSV được nhập, tệp này **không** tự động được đăng ký làm nguồn bản dịch cho project. Hãy nhớ làm theo các bước được mô tả trong
:ref:`doc_internationalizing_games_configuring_imported_translation` so that the
bản dịch thực sự được sử dụng khi chạy project.
