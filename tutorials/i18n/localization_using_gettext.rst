.. _doc_localization_using_gettext:

Bản địa hóa bằng gettext (tệp PO)
=================================

Ngoài việc nhập bản dịch ở
:ref:`định dạng CSV <doc_localization_using_spreadsheets>`, Godot còn hỗ trợ tải các tệp bản dịch được viết theo định dạng GNU gettext (dựa trên văn bản ``.po`` và đã biên dịch ``.mo``).

.. note:: Để tìm hiểu nhập môn về gettext, hãy xem `Hướng dẫn nhanh về Gettext <https://www.labri.fr/perso/fleury/posts/programming/a-quick-gettext-tutorial.html>`_. Tài liệu này được viết cho các dự án C, nhưng phần lớn lời khuyên cũng áp dụng cho Godot (ngoại trừ ``xgettext``).

          Để xem tài liệu đầy đủ, hãy xem `GNU Gettext <https://www.gnu.org/software/gettext/manual/gettext.html>`_.

Ưu điểm
-------

- gettext là một định dạng tiêu chuẩn, có thể được chỉnh sửa bằng bất kỳ trình soạn thảo văn bản nào hoặc các trình soạn thảo GUI như `Poedit <https://poedit.net/>`_. Điều này có thể rất hữu ích vì nó cung cấp nhiều công cụ cho người dịch, chẳng hạn như đánh dấu các chuỗi đã lỗi thời, tìm các chuỗi chưa được dịch, v.v.
- gettext được các nền tảng dịch thuật như `Transifex <https://www.transifex.com/>`_ và `Weblate <https://weblate.org/>`_ hỗ trợ, giúp mọi người cộng tác trong việc bản địa hóa dễ dàng hơn.
- So với CSV, các tệp gettext hoạt động tốt hơn với những hệ thống kiểm soát phiên bản như Git, vì mỗi locale có tệp messages riêng.
- Các chuỗi nhiều dòng dễ chỉnh sửa hơn trong tệp PO của gettext so với tệp CSV.

Nhược điểm
----------

- Tệp PO của gettext có định dạng phức tạp hơn CSV và có thể khó nắm bắt hơn đối với những người mới làm quen với việc bản địa hóa phần mềm.
- Những người duy trì các tệp bản địa hóa sẽ phải cài đặt các công cụ gettext trên hệ thống của mình. Tuy nhiên, vì Godot hỗ trợ sử dụng các tệp messages dạng văn bản (``.po``), người dịch có thể kiểm thử công việc của mình mà không cần cài đặt các công cụ gettext.
- Tệp PO của gettext thường sử dụng tiếng Anh làm ngôn ngữ cơ sở. Người dịch sẽ dùng ngôn ngữ cơ sở này để dịch sang các ngôn ngữ khác. Bạn vẫn có thể sử dụng ngôn ngữ khác làm ngôn ngữ cơ sở, nhưng điều này không phổ biến.

Cài đặt các công cụ gettext
---------------------------

Cần có các công cụ gettext trên dòng lệnh để thực hiện các thao tác bảo trì, chẳng hạn như cập nhật các tệp messages. Vì vậy, bạn nên cài đặt chúng.

- **Windows:** Tải trình cài đặt từ `trang này <https://mlocati.github.io/articles/gettext-iconv-windows.html>`_. Mọi kiến trúc và loại binary (shared hoặc static) đều hoạt động; nếu không chắc chắn, hãy chọn trình cài đặt static 64-bit.
- **macOS:** Cài đặt gettext bằng `Homebrew <https://brew.sh/>`_ với lệnh ``brew install gettext``, hoặc bằng `MacPorts <https://www.macports.org/>`_ với lệnh ``sudo port install gettext``.
- **Linux:** Trên hầu hết các bản phân phối, hãy cài đặt gói ``gettext`` từ trình quản lý gói của bản phân phối.

Để sử dụng công cụ GUI, bạn có thể tải Poedit từ `trang web chính thức <https://poedit.net/>`_ của công cụ này. Phiên bản cơ bản là mã nguồn mở và được cung cấp theo giấy phép MIT.

Tạo template PO
---------------

Tự động tạo bằng editor
~~~~~~~~~~~~~~~~~~~~~~~

Editor có thể tự động tạo template PO từ các tệp scene và GDScript được chỉ định. Việc tạo POT này cũng hỗ trợ các context bản dịch và việc số nhiều nếu được sử dụng trong script, với đối số thứ hai tùy chọn của ``tr()`` và phương thức ``tr_n()``.

Mở :menu:`Project > Project Settings > Localization > Template Generation`, sau đó sử dụng
:button:`Add…` để chỉ định đường dẫn đến các scene và script của dự án có chứa các chuỗi có thể bản địa hóa:

.. figure:: img/localization_using_gettext_pot_generation.webp
   :align: center
   :alt: Tạo template PO trong thẻ Localization > Template Generation của Project Settings

   Tạo template PO trong thẻ :menu:`Localization > Template Generation` của :ui:`Project Settings`

Sau khi thêm ít nhất một scene hoặc script, hãy nhấp vào :button:`Generate` ở góc trên bên phải, rồi chỉ định đường dẫn đến tệp đầu ra có phần mở rộng ``pot``. Tệp này có thể được đặt ở bất kỳ đâu trong thư mục dự án, nhưng bạn nên giữ tệp trong một thư mục con như ``locale``, vì mỗi locale sẽ được định nghĩa trong tệp riêng.

Xem :ref:`bên dưới <doc_localization_using_gettext_gdscript>` để biết cách thêm nhận xét cho người dịch hoặc loại trừ một số chuỗi khỏi template PO đối với các tệp GDScript.

Sau đó, bạn có thể chuyển sang
:ref:`tạo tệp messages từ template PO <doc_localization_using_gettext_messages_file>`.

.. note::

    Hãy nhớ tạo lại template PO sau khi thực hiện bất kỳ thay đổi nào đối với các chuỗi có thể bản địa hóa, hoặc sau khi thêm scene hay script mới. Nếu không, các chuỗi mới được thêm sẽ không thể bản địa hóa và người dịch sẽ không thể cập nhật bản dịch cho các chuỗi đã lỗi thời.

Tạo thủ công
~~~~~~~~~~~~

Nếu cách tạo tự động không phù hợp với nhu cầu của bạn, bạn có thể tự tạo template PO trong trình soạn thảo văn bản. Tệp này có thể được đặt ở bất kỳ đâu trong thư mục dự án, nhưng bạn nên giữ tệp trong một thư mục con, vì mỗi locale sẽ được định nghĩa trong tệp riêng.

Tạo một thư mục có tên ``locale`` trong thư mục dự án. Trong thư mục này, lưu một tệp có tên ``messages.pot`` với nội dung sau:

::

    # Don't remove the two lines below, they're required for gettext to work correctly.
    msgid ""
    msgstr ""

    # Example of a regular string.
    msgid "Hello world!"
    msgstr ""

    # Example of a string with pluralization.
    msgid "There is %d apple."
    msgid_plural "There are %d apples."
    msgstr[0] ""
    msgstr[1] ""

    # Example of a string with a translation context.
    msgctxt "Actions"
    msgid "Close"
    msgstr ""

Các message trong gettext được tạo thành từ các cặp ``msgid`` và ``msgstr``. ``msgid`` là chuỗi nguồn (thường bằng tiếng Anh), còn ``msgstr`` là chuỗi đã dịch.

.. warning::

    Giá trị ``msgstr`` trong các tệp template PO (``.pot``) phải **luôn luôn** để trống. Việc bản địa hóa sẽ được thực hiện trong các tệp ``.po`` được tạo ra.

.. _doc_localization_using_gettext_messages_file:

Tạo tệp messages từ template PO
-------------------------------

Lệnh ``msginit`` được dùng để chuyển một template PO thành tệp messages. Ví dụ, để tạo tệp bản địa hóa tiếng Pháp, hãy sử dụng lệnh sau khi đang ở trong thư mục ``locale``:

.. code-block:: shell

    msginit --no-translator --input=messages.pot --locale=fr

Lệnh trên sẽ tạo một tệp có tên ``fr.po`` trong cùng thư mục với template PO.

Ngoài ra, bạn có thể thực hiện việc này bằng giao diện đồ họa với Poedit, hoặc tải tệp POT lên nền tảng web tùy chọn của mình.

Tải tệp messages vào Godot
--------------------------

Để đăng ký một tệp messages làm bản dịch trong dự án, hãy mở
:ui:`Project Settings`, sau đó đi đến :menu:`Localization > Translations`, nhấp vào :button:`Add…` rồi chọn tệp ``.po`` hoặc ``.mo`` trong hộp thoại tệp. Locale sẽ được suy ra từ thuộc tính ``"Language: <code>\n"`` trong tệp messages.

.. note:: Xem :ref:`doc_internationalizing_games` để biết thêm thông tin về cách nhập và kiểm thử bản dịch trong Godot.

Cập nhật các tệp thông báo để tuân theo mẫu PO
----------------------------------------------

Sau khi cập nhật mẫu PO, bạn sẽ phải cập nhật các tệp thông báo để chúng chứa các chuỗi mới, đồng thời xóa các chuỗi không còn xuất hiện trong mẫu PO. Bạn có thể tự động thực hiện việc này bằng công cụ ``msgmerge``:

.. code-block:: shell

    # Thứ tự rất quan trọng: hãy chỉ định tệp thông báo *trước* mẫu PO!
    msgmerge --update --backup=none fr.po messages.pot

Nếu muốn giữ bản sao lưu của tệp thông báo gốc (trong ví dụ này, tệp đó sẽ được lưu dưới dạng ``fr.po~``), hãy xóa đối số ``--backup=none``.

.. note::

    Sau khi chạy ``msgmerge``, các chuỗi đã được sửa đổi trong ngôn ngữ nguồn sẽ có thêm chú thích "fuzzy" ở phía trước trong tệp ``.po``. Chú thích này cho biết bản dịch cần được cập nhật để khớp với chuỗi nguồn mới, vì bản dịch rất có thể sẽ không chính xác cho đến khi được cập nhật.

    Các chuỗi có chú thích "fuzzy" **sẽ không** được Godot đọc cho đến khi bản dịch được cập nhật và chú thích "fuzzy" bị xóa.

Kiểm tra tính hợp lệ của tệp hoặc mẫu PO
----------------------------------------

Bạn có thể kiểm tra xem cú pháp của tệp gettext có hợp lệ hay không.

Nếu mở bằng Poeditor, công cụ sẽ hiển thị các cảnh báo phù hợp nếu có lỗi cú pháp. Bạn cũng có thể xác minh bằng cách chạy lệnh gettext dưới đây:

.. code-block:: shell

    msgfmt fr.po --check

Nếu có lỗi cú pháp hoặc cảnh báo, chúng sẽ được hiển thị trong console. Nếu không, ``msgfmt`` sẽ không xuất ra bất kỳ nội dung nào.

Sử dụng tệp MO nhị phân (chỉ hữu ích cho các dự án lớn)
-------------------------------------------------------

Đối với các dự án lớn có vài nghìn chuỗi cần dịch trở lên, bạn có thể cân nhắc sử dụng các tệp thông báo MO nhị phân (đã biên dịch) thay cho các tệp PO dựa trên văn bản. Tệp MO nhị phân nhỏ hơn và được đọc nhanh hơn các tệp PO tương ứng.

Bạn có thể tạo tệp MO bằng lệnh dưới đây:

.. code-block:: shell

    msgfmt fr.po --no-hash -o fr.mo

Nếu tệp PO hợp lệ, lệnh này sẽ tạo một tệp ``fr.mo`` bên cạnh tệp PO. Sau đó, tệp MO này có thể được tải vào Godot như mô tả ở trên.

Bạn nên lưu tệp PO gốc trong hệ thống quản lý phiên bản để có thể cập nhật bản dịch trong tương lai. Nếu làm mất tệp PO gốc và muốn dịch ngược tệp MO thành tệp PO dựa trên văn bản, bạn có thể thực hiện bằng lệnh:

.. code-block:: shell

    msgunfmt fr.mo > fr.po

Tệp đã dịch ngược sẽ không bao gồm các chú thích hoặc chuỗi fuzzy, vì ngay từ đầu chúng không bao giờ được biên dịch vào tệp MO.

.. _doc_localization_using_gettext_gdscript:

Trích xuất các chuỗi có thể bản địa hóa từ tệp GDScript
-------------------------------------------------------

`Trình bổ trợ editor <https://github.com/godotengine/godot/blob/master/modules/gdscript/editor/gdscript_translation_parser_plugin.h>`_ tích hợp sẵn nhận diện nhiều mẫu khác nhau trong mã nguồn để trích xuất các chuỗi có thể bản địa hóa từ tệp GDScript, bao gồm nhưng không chỉ giới hạn ở các mẫu sau:

- các lệnh gọi ``tr()``, ``tr_n()``, ``atr()`` và ``atr_n()``;”
- gán các thuộc tính ``text``, ``placeholder_text`` và ``tooltip_text``;”
- các lệnh gọi ``add_tab()``, ``add_item()``, ``set_tab_title()`` và các lệnh gọi khác;”
- các bộ lọc ``FileDialog`` như ``"*.png ; PNG Images"``.

.. note::

    Đối số hoặc toán hạng bên phải phải là một chuỗi hằng, nếu không plugin sẽ không thể đánh giá biểu thức và sẽ bỏ qua biểu thức đó.

Nếu plugin trích xuất các chuỗi không cần thiết, bạn có thể bỏ qua chúng bằng chú thích ``NO_TRANSLATE``. Bạn cũng có thể cung cấp thêm thông tin cho người dịch bằng chú thích ``TRANSLATORS:``. Các chú thích này phải được đặt trên cùng dòng với mẫu được nhận diện hoặc ở phía trước mẫu đó.

::

    $CharacterName.text = "???" # NO_TRANSLATE

    # NO_TRANSLATE: Language name.
    $TabContainer.set_tab_title(0, "Python")

    item.text = "Tool" # TRANSLATORS: Up to 10 characters.

    # TRANSLATORS: This is a reference to Lewis Carroll's poem "Jabberwocky",
    # make sure to keep this as it is important to the plot.
    say(tr("He took his vorpal sword in hand. The end?"))

Sử dụng ngữ cảnh
----------------

Có thể sử dụng tham số ``context`` để phân biệt tình huống sử dụng bản dịch hoặc để phân biệt các từ đa nghĩa (những từ có nhiều nghĩa).

Ví dụ:

::

    tr("Start", "Main Menu")
    tr("End", "Main Menu")
    tr("Shop", "Main Menu")
    tr("Shop", "In Game")

Trong tệp PO của gettext, một chuỗi có ngữ cảnh có thể được định nghĩa như sau:

::

    # Example of a string with a translation context.
    msgctxt "Main Menu"
    msgid "Shop"
    msgstr ""

    # A different source string that is identical, but with a different context.
    msgctxt "In Game"
    msgid "Shop"
    msgstr ""

Cập nhật các tệp PO
-------------------

Sớm hay muộn, bạn sẽ thêm nội dung mới vào trò chơi và sẽ có các chuỗi mới cần được dịch. Khi điều này xảy ra, bạn sẽ cần cập nhật các tệp PO hiện có để bao gồm các chuỗi mới.

Trước tiên, hãy tạo một tệp POT mới chứa tất cả các chuỗi hiện có cùng với các chuỗi mới được thêm vào. Sau đó, hợp nhất các tệp PO hiện có với tệp POT mới. Có hai cách để thực hiện việc này:

- Sử dụng một trình soạn thảo gettext; trình soạn thảo này thường có tùy chọn cập nhật tệp PO từ tệp POT.

- Sử dụng công cụ gettext ``msgmerge``:

.. code-block:: shell

    # Thứ tự rất quan trọng: hãy chỉ định tệp thông báo *trước* mẫu PO!
    msgmerge --update --backup=none fr.po messages.pot

Nếu muốn giữ bản sao lưu của tệp thông báo gốc (trong ví dụ này, tệp đó sẽ được lưu dưới dạng ``fr.po~``), hãy xóa đối số ``--backup=none``.

Plugin tùy chỉnh để tạo POT
---------------------------

Nếu bạn cần xử lý thêm một định dạng tệp khác, bạn có thể viết một plugin tùy chỉnh để phân tích cú pháp và trích xuất các chuỗi từ tệp tùy chỉnh đó. Plugin tùy chỉnh này sẽ trích xuất các chuỗi và ghi chúng vào tệp POT khi bạn nhấn **Generate POT**. Để tìm hiểu thêm về cách tạo plugin trình phân tích cú pháp bản dịch, hãy xem
:ref:`EditorTranslationParserPlugin <class_EditorTranslationParserPlugin>`.

.. _`A Quick Gettext Tutorial`: https://www.labri.fr/perso/fleury/posts/programming/a-quick-gettext-tutorial.html
.. _`GNU Gettext`: https://www.gnu.org/software/gettext/manual/gettext.html
.. _`Poedit`: https://poedit.net/
.. _`Transifex`: https://www.transifex.com/
.. _`Weblate`: https://weblate.org/
.. _`this page`: https://mlocati.github.io/articles/gettext-iconv-windows.html
.. _`Homebrew`: https://brew.sh/
.. _`MacPorts`: https://www.macports.org/
.. _`Official website`: https://poedit.net/
.. _`editor plugin`: https://github.com/godotengine/godot/blob/master/modules/gdscript/editor/gdscript_translation_parser_plugin.h
