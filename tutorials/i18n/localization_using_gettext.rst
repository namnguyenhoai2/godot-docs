.. _doc_localization_using_gettext:

Bản địa hóa bằng gettext (tệp PO)
=================================

Ngoài việc nhập các bản dịch trong
:ref:`CSV format <doc_localization_using_spreadsheets>`, Godot also
hỗ trợ tải các tệp bản dịch được viết theo định dạng GNU gettext (``.po`` dựa trên văn bản và ``.mo`` đã biên dịch).

.. note:: For an introduction to gettext, check out
          `A Quick Gettext Tutorial <https://www.labri.fr/perso/fleury/posts/programming/a-quick-gettext-tutorial.html>`_. Tài liệu này được viết với các dự án C làm trọng tâm, nhưng phần lớn hướng dẫn cũng áp dụng cho Godot (ngoại trừ ``xgettext``).

          Để xem tài liệu đầy đủ, hãy xem `GNU Gettext <https://www.gnu.org/software/gettext/manual/gettext.html>`_.

Ưu điểm
-------

- gettext là một định dạng tiêu chuẩn, có thể được chỉnh sửa bằng bất kỳ trình soạn thảo văn bản nào hoặc các trình soạn thảo GUI như `Poedit <https://poedit.net/>`_. Điều này có thể rất hữu ích vì nó cung cấp nhiều công cụ cho translator, chẳng hạn như đánh dấu các chuỗi đã lỗi thời, tìm các chuỗi chưa được dịch, v.v. - gettext được các nền tảng dịch thuật như `Transifex <https://www.transifex.com/>`_ và `Weblate <https://weblate.org/>`_ hỗ trợ, giúp mọi người dễ dàng cộng tác trong việc bản địa hóa hơn. - So với CSV, các tệp gettext hoạt động tốt hơn với các hệ thống version control như Git, vì mỗi locale có tệp messages riêng. - Các chuỗi nhiều dòng thuận tiện chỉnh sửa hơn trong tệp PO của gettext so với tệp CSV.

Nhược điểm
----------

- Tệp PO của gettext có định dạng phức tạp hơn CSV và có thể khó nắm bắt đối với những người mới làm quen với việc bản địa hóa phần mềm. - Những người duy trì các tệp bản địa hóa sẽ phải cài đặt các công cụ gettext trên hệ thống của mình. Tuy nhiên, vì Godot hỗ trợ sử dụng các tệp messages dựa trên văn bản (``.po``), translator có thể kiểm tra công việc của mình mà không cần cài đặt các công cụ gettext. - Tệp PO của gettext thường sử dụng tiếng Anh làm ngôn ngữ cơ sở. Translator sẽ sử dụng ngôn ngữ cơ sở này để dịch sang các ngôn ngữ khác. Bạn vẫn có thể sử dụng ngôn ngữ khác làm ngôn ngữ cơ sở, nhưng cách này không phổ biến.

Cài đặt các công cụ gettext
---------------------------

Các công cụ gettext dòng lệnh cần thiết để thực hiện các thao tác bảo trì, chẳng hạn như cập nhật các tệp messages. Vì vậy, bạn nên cài đặt chúng.

- **Windows:** Tải trình cài đặt từ `this page <https://mlocati.github.io/articles/gettext-iconv-windows.html>`_. Mọi architecture và binary type (shared hoặc static) đều hoạt động; nếu không chắc chắn, hãy chọn trình cài đặt static 64-bit. - **macOS:** Cài đặt gettext bằng `Homebrew <https://brew.sh/>`_ với lệnh ``brew install gettext``, hoặc bằng `MacPorts <https://www.macports.org/>`_ với lệnh ``sudo port install gettext``. - **Linux:** Trên hầu hết các distribution, hãy cài đặt package ``gettext`` từ package manager của distribution.

Đối với công cụ GUI, bạn có thể lấy Poedit từ `Official website <https://poedit.net/>`_. Phiên bản cơ bản là mã nguồn mở và được cung cấp theo giấy phép MIT.

Tạo template PO
---------------

Tự động tạo bằng editor
~~~~~~~~~~~~~~~~~~~~~~~

Editor có thể tự động tạo template PO từ các tệp scene và GDScript được chỉ định. Việc tạo POT này cũng hỗ trợ translation context và pluralization nếu được sử dụng trong script, với đối số thứ hai tùy chọn của ``tr()`` và method ``tr_n()``.

Mở :menu:`Project > Project Settings > Localization > Template Generation`, sau đó sử dụng
:button:`Add…` button to specify the path to your project's scenes and scripts that
chứa các chuỗi có thể bản địa hóa:

.. figure:: img/localization_using_gettext_pot_generation.webp
   :align: center
   :alt: Creating a PO template in the Localization > Template Generation tab of the Project Settings

   Creating a PO template in the :menu:`Localization > Template Generation` tab of the :ui:`Project Settings`

Sau khi thêm ít nhất một scene hoặc script, hãy nhấp vào :button:`Generate` ở góc trên bên phải, sau đó chỉ định đường dẫn đến tệp đầu ra với phần mở rộng tệp ``pot``. Tệp này có thể được đặt ở bất kỳ đâu trong thư mục dự án, nhưng bạn nên giữ tệp trong một thư mục con như ``locale``, vì mỗi locale sẽ được định nghĩa trong tệp riêng.

Xem :ref:`below <doc_localization_using_gettext_gdscript>` để biết cách thêm comment cho translator hoặc loại trừ một số chuỗi khỏi việc được thêm vào template PO đối với các tệp GDScript.

Sau đó, bạn có thể chuyển sang
:ref:`creating a messages file from a PO template <doc_localization_using_gettext_messages_file>`.

.. note::

    Hãy nhớ tạo lại template PO sau khi thực hiện bất kỳ thay đổi nào đối với các chuỗi có thể bản địa hóa, hoặc sau khi thêm scene hay script mới. Nếu không, các chuỗi mới được thêm sẽ không thể bản địa hóa và translator sẽ không thể cập nhật các bản dịch của những chuỗi đã lỗi thời.

Tạo thủ công
~~~~~~~~~~~~

Nếu cách tạo tự động không đáp ứng nhu cầu của bạn, bạn có thể tự tạo template PO trong trình soạn thảo văn bản. Tệp này có thể được đặt ở bất kỳ đâu trong thư mục dự án, nhưng bạn nên giữ tệp trong một thư mục con, vì mỗi locale sẽ được định nghĩa trong tệp riêng.

Tạo một thư mục có tên ``locale`` trong thư mục dự án. Trong thư mục này, lưu một tệp có tên ``messages.pot`` với nội dung sau:

::

    # Đừng xóa hai dòng bên dưới, chúng cần thiết để gettext hoạt động chính xác.
    msgid ""
    msgstr ""

    # Ví dụ về một chuỗi thông thường.
    msgid "Hello world!"
    msgstr ""

    # Ví dụ về một chuỗi có pluralization.
    msgid "There is %d apple."
    msgid_plural "There are %d apples."
    msgstr[0] ""
    msgstr[1] ""

    # Ví dụ về một chuỗi có translation context.
    msgctxt "Actions"
    msgid "Close"
    msgstr ""

Các message trong gettext được tạo thành từ các cặp ``msgid`` và ``msgstr``. ``msgid`` là chuỗi nguồn (thường bằng tiếng Anh), còn ``msgstr`` sẽ là chuỗi đã dịch.

.. warning::

    Giá trị ``msgstr`` trong các tệp template PO (``.pot``) phải **luôn** để trống. Việc bản địa hóa sẽ được thực hiện trong các tệp ``.po`` được tạo ra.

.. _doc_localization_using_gettext_messages_file:

Tạo tệp messages từ template PO
-------------------------------

Lệnh ``msginit`` được dùng để chuyển một template PO thành tệp messages. Ví dụ, để tạo tệp bản địa hóa tiếng Pháp, hãy sử dụng lệnh sau khi đang ở trong thư mục ``locale``:

.. code-block:: shell

    msginit --no-translator --input=messages.pot --locale=fr

Lệnh trên sẽ tạo một tệp có tên ``fr.po`` trong cùng thư mục với template PO.

Ngoài ra, bạn có thể thực hiện việc này bằng giao diện đồ họa với Poedit hoặc tải tệp POT lên web platform mà bạn chọn.

Tải tệp messages trong Godot
----------------------------

Để đăng ký một tệp messages làm bản dịch trong dự án, hãy mở
:ui:`Project Settings`, then go to :menu:`Localization > Translations`,
nhấp vào :button:`Add…`, sau đó chọn tệp ``.po`` hoặc ``.mo`` trong hộp thoại tệp. Locale sẽ được suy ra từ thuộc tính ``"Language: <code>\n"`` trong tệp messages.

.. note:: See :ref:`doc_internationalizing_games` for more information on
          nhập và kiểm thử các bản dịch trong Godot.

Cập nhật các tệp messages để tuân theo template PO
--------------------------------------------------

Sau khi cập nhật template PO, bạn sẽ phải cập nhật các tệp messages để chúng chứa các chuỗi mới, đồng thời xóa các chuỗi không còn xuất hiện trong template PO. Việc này có thể được thực hiện tự động bằng công cụ ``msgmerge``:

.. code-block:: shell

    # Thứ tự rất quan trọng: hãy chỉ định tệp messages *trước*, sau đó đến template PO!
    msgmerge --update --backup=none fr.po messages.pot

Nếu muốn giữ bản sao lưu của tệp messages gốc (trong ví dụ này sẽ được lưu dưới dạng ``fr.po~``), hãy xóa đối số ``--backup=none``.

.. note::

    Sau khi chạy ``msgmerge``, các chuỗi đã được sửa đổi trong ngôn ngữ nguồn sẽ được thêm comment "fuzzy" ở phía trước trong tệp ``.po``. Comment này cho biết bản dịch cần được cập nhật để khớp với chuỗi nguồn mới, vì bản dịch nhiều khả năng sẽ không chính xác cho đến khi được cập nhật.

    Các chuỗi có comment "fuzzy" sẽ **không** được Godot đọc cho đến khi bản dịch được cập nhật và comment "fuzzy" được xóa.

Kiểm tra tính hợp lệ của tệp hoặc template PO
---------------------------------------------

Bạn có thể kiểm tra xem cú pháp của tệp gettext có hợp lệ hay không.

Nếu mở bằng Poeditor, công cụ sẽ hiển thị các cảnh báo phù hợp nếu có lỗi cú pháp. Bạn cũng có thể xác minh bằng cách chạy lệnh gettext dưới đây:

.. code-block:: shell

    msgfmt fr.po --check

Nếu có lỗi cú pháp hoặc cảnh báo, chúng sẽ được hiển thị trong console. Nếu không, ``msgfmt`` sẽ không xuất ra bất kỳ thông tin nào.

Sử dụng tệp MO nhị phân (chỉ hữu ích cho các dự án lớn)
-------------------------------------------------------

Đối với các dự án lớn có vài nghìn chuỗi cần dịch trở lên, việc sử dụng các tệp messages MO nhị phân (đã biên dịch) thay cho các tệp PO dựa trên văn bản có thể đáng cân nhắc. Tệp MO nhị phân nhỏ hơn và được đọc nhanh hơn các tệp PO tương đương.

Bạn có thể tạo tệp MO bằng lệnh dưới đây:

.. code-block:: shell

    msgfmt fr.po --no-hash -o fr.mo

Nếu tệp PO hợp lệ, lệnh này sẽ tạo một tệp ``fr.mo`` bên cạnh tệp PO. Sau đó, tệp MO này có thể được tải trong Godot như mô tả ở trên.

Nên giữ tệp PO gốc trong version control để bạn có thể cập nhật bản dịch trong tương lai. Nếu làm mất tệp PO gốc và muốn decompile tệp MO thành tệp PO dựa trên văn bản, bạn có thể thực hiện bằng:

.. code-block:: shell

    msgunfmt fr.mo > fr.po

Tệp được decompile sẽ không bao gồm comment hoặc các chuỗi fuzzy, vì ngay từ đầu chúng không bao giờ được biên dịch vào tệp MO.

.. _doc_localization_using_gettext_gdscript:

Trích xuất các chuỗi có thể bản địa hóa từ tệp GDScript
-------------------------------------------------------

`editor plugin <https://github.com/godotengine/godot/blob/master/modules/gdscript/editor/gdscript_translation_parser_plugin.h>`_ tích hợp sẵn nhận diện nhiều pattern trong source code để trích xuất các chuỗi có thể bản địa hóa từ tệp GDScript, bao gồm nhưng không giới hạn ở những pattern sau:

- các lời gọi ``tr()``, ``tr_n()``, ``atr()`` và ``atr_n()``; - gán các property ``text``, ``placeholder_text`` và ``tooltip_text``; - ``add_tab()``, ``add_item()``, ``set_tab_title()`` và các lời gọi khác; - các filter ``FileDialog`` như ``"*.png ; PNG Images"``.

.. note::

    Đối số hoặc toán hạng bên phải phải là một chuỗi hằng, nếu không plugin sẽ không thể đánh giá biểu thức và sẽ bỏ qua chuỗi đó.

Nếu plugin trích xuất các chuỗi không cần thiết, bạn có thể bỏ qua chúng bằng comment ``NO_TRANSLATE``. Bạn cũng có thể cung cấp thêm thông tin cho translator bằng comment ``TRANSLATORS:``. Các comment này phải được đặt trên cùng dòng với pattern được nhận diện hoặc ở phía trước pattern đó.

::

    $CharacterName.text = "???" # NO_TRANSLATE

    # NO_TRANSLATE: Tên ngôn ngữ.
    $TabContainer.set_tab_title(0, "Python")

    item.text = "Tool" # TRANSLATORS: Tối đa 10 ký tự.

    # TRANSLATORS: Đây là một tham chiếu đến bài thơ "Jabberwocky" của Lewis Carroll,
    # hãy đảm bảo giữ nguyên điều này vì nó quan trọng đối với cốt truyện.
    say(tr("He took his vorpal sword in hand. The end?"))

Sử dụng context
---------------

Tham số ``context`` có thể được dùng để phân biệt trường hợp sử dụng bản dịch, hoặc để phân biệt các từ đa nghĩa (những từ có nhiều nghĩa).

Ví dụ:

::

    tr("Start", "Main Menu")
    tr("End", "Main Menu")
    tr("Shop", "Main Menu")
    tr("Shop", "In Game")

Trong tệp gettext PO, một chuỗi có context có thể được định nghĩa như sau:

::

    # Ví dụ về một chuỗi có translation context.
    msgctxt "Main Menu"
    msgid "Shop"
    msgstr ""

    # Một chuỗi nguồn khác giống hệt, nhưng có context khác.
    msgctxt "In Game"
    msgid "Shop"
    msgstr ""

Cập nhật các tệp PO
-------------------

Sớm hay muộn, bạn sẽ thêm nội dung mới vào game của mình và sẽ có các chuỗi mới cần được dịch. Khi điều này xảy ra, bạn sẽ cần cập nhật các tệp PO hiện có để bổ sung các chuỗi mới.

Trước tiên, hãy tạo một tệp POT mới chứa tất cả các chuỗi hiện có cùng với các chuỗi mới được thêm. Sau đó, hợp nhất các tệp PO hiện có với tệp POT mới. Có hai cách để thực hiện việc này:

- Sử dụng trình chỉnh sửa gettext; trình này phải có tùy chọn cập nhật tệp PO từ tệp POT.

- Sử dụng công cụ gettext ``msgmerge``:

.. code-block:: shell

    # Thứ tự rất quan trọng: hãy chỉ định message file *trước*, sau đó mới đến PO template!
    msgmerge --update --backup=none fr.po messages.pot

Nếu bạn muốn giữ bản sao lưu của message file ban đầu (trong ví dụ này, tệp đó sẽ được lưu dưới dạng ``fr.po~``), hãy xóa đối số ``--backup=none``.

Plugin tùy chỉnh để tạo POT
---------------------------

Nếu bạn cần xử lý thêm định dạng tệp nào khác, bạn có thể viết một plugin tùy chỉnh để phân tích cú pháp và trích xuất các chuỗi từ tệp tùy chỉnh đó. Plugin tùy chỉnh này sẽ trích xuất các chuỗi và ghi chúng vào tệp POT khi bạn nhấn **Generate POT**. Để tìm hiểu thêm về cách tạo plugin phân tích cú pháp bản dịch, hãy xem
:ref:`EditorTranslationParserPlugin <class_EditorTranslationParserPlugin>`.
