.. _doc_internationalizing_games:

Bản địa hóa game
================

Giới thiệu
----------

Mặc dù các game indie hoặc game ngách thường không cần bản địa hóa, những game nhắm đến thị trường đại chúng hơn thường cần được bản địa hóa. Godot cung cấp nhiều công cụ giúp quá trình này trở nên đơn giản hơn, vì vậy hướng dẫn này giống một tập hợp các mẹo và thủ thuật hơn.

Bản địa hóa thường do các studio chuyên trách được thuê để thực hiện. Mặc dù có rất nhiều phần mềm và định dạng tệp phục vụ việc này, cách phổ biến nhất để bản địa hóa cho đến nay vẫn là sử dụng bảng tính. Quy trình tạo và nhập các bảng tính đã được trình bày trong
:ref:`doc_importing_translations` hướng dẫn. Nếu bạn chưa đọc trang Importing translations, chúng tôi khuyên bạn nên đọc trang đó trước khi đọc trang này.

.. note:: Chúng ta sẽ sử dụng bản demo chính thức làm ví dụ; bạn có thể `tải xuống từ Asset Library <https://godotengine.org/asset-library/asset/2776>`_.

.. _doc_internationalizing_games_configuring_imported_translation:

Cấu hình bản dịch đã nhập
-------------------------

Các bản dịch có thể được cập nhật và nhập lại khi thay đổi, nhưng vẫn phải được thêm vào project. Việc này được thực hiện trong
:menu:`Project > Project Settings > Localization > Translations`:

.. image:: img/localization_dialog.webp

Hộp thoại trên được dùng để thêm hoặc xóa bản dịch trên toàn project.

Bản địa hóa tài nguyên
----------------------

Bạn cũng có thể yêu cầu Godot sử dụng các phiên bản thay thế của asset (tài nguyên) tùy theo ngôn ngữ hiện tại. Tính năng này có thể được dùng cho các hình ảnh đã bản địa hóa, chẳng hạn như biển quảng cáo trong game, hoặc giọng nói đã bản địa hóa.

Có thể sử dụng tab :ui:`Remaps` cho việc này:

.. image:: img/localization_remaps.webp

Chọn tài nguyên cần ánh xạ lại, sau đó thêm một số phiên bản thay thế cho từng locale.

.. note::

    Hệ thống ánh xạ lại tài nguyên không được hỗ trợ cho DynamicFonts. Để sử dụng các font khác nhau tùy theo hệ chữ của ngôn ngữ, hãy dùng hệ thống fallback của DynamicFont, cho phép bạn định nghĩa bao nhiêu font fallback tùy ý.

    Ưu điểm của hệ thống fallback của DynamicFont là nó hoạt động bất kể ngôn ngữ hiện tại là gì, nên rất phù hợp với những tính năng như chat nhiều người chơi, nơi ngôn ngữ của văn bản có thể không trùng với ngôn ngữ của client.

Tự động thiết lập ngôn ngữ
--------------------------

Bạn nên mặc định sử dụng ngôn ngữ ưu tiên của người dùng, có thể lấy thông qua :ref:`OS.get_locale_language() <class_OS_method_get_locale_language>`. Nếu game của bạn không có sẵn bằng ngôn ngữ đó, nó sẽ chuyển sang
:ref:`Fallback <class_ProjectSettings_property_internationalization/locale/fallback>` trong :menu:`Project > Project Settings > General > Internationalization > Locale`, hoặc sang ``en`` nếu rỗng. Tuy nhiên, bạn nên cho phép người chơi thay đổi ngôn ngữ trong game vì nhiều lý do (ví dụ: chất lượng bản dịch hoặc sở thích của người chơi).

.. tabs::
 .. code-tab:: gdscript

    var language = "automatic"
    # Tải ngôn ngữ từ tệp cài đặt người dùng tại đây
    if language == "automatic":
       var preferred_language = OS.get_locale_language()
       TranslationServer.set_locale(preferred_language)
    else:
       TranslationServer.set_locale(language)

Locale và ngôn ngữ
------------------

:ref:`locale <doc_locales>` thường là sự kết hợp giữa một ngôn ngữ với một vùng hoặc quốc gia, nhưng cũng có thể chứa thông tin như hệ chữ hoặc biến thể.

Ví dụ:

- ``en``: Ngôn ngữ tiếng Anh
- ``en_GB``: Tiếng Anh tại Vương quốc Anh / English Anh-Anh
- ``en_US``: Tiếng Anh tại Hoa Kỳ / English Mỹ
- ``en_DE``: Tiếng Anh tại Đức

Các game indie nhìn chung chỉ cần quan tâm đến ngôn ngữ, nhưng hãy đọc tiếp để biết thêm thông tin.

Lý do tồn tại của locale có thể được minh họa qua Hoa Kỳ và Vương quốc Anh. Cả hai đều nói cùng một ngôn ngữ (tiếng Anh), nhưng khác nhau ở nhiều khía cạnh:

- Cách viết: ví dụ gray (Hoa Kỳ), grey (Vương quốc Anh)
- Cách dùng từ: ví dụ eggplant (Hoa Kỳ), aubergine (Vương quốc Anh)
- Đơn vị hoặc tiền tệ: ví dụ feet/inches (Hoa Kỳ), metres/cm (Vương quốc Anh)

Tuy nhiên, mọi thứ có thể trở nên phức tạp hơn. Hãy tưởng tượng bạn cung cấp nội dung khác nhau ở châu Âu và Trung Quốc (ví dụ: trong một MMO). Bạn sẽ cần dịch từng biến thể nội dung đó sang nhiều ngôn ngữ, đồng thời lưu trữ và tải chúng tương ứng.

Chuyển key thành văn bản
------------------------

Một số control, chẳng hạn như :ref:`Button <class_Button>` và :ref:`Label <class_Label>`, sẽ tự động lấy bản dịch nếu văn bản của chúng khớp với một key bản dịch. Ví dụ: nếu văn bản của một label là ``MAIN_SCREEN_GREETING1`` và key đó tồn tại trong bản dịch hiện tại, văn bản sẽ tự động được dịch.

Hành vi dịch tự động này có thể không phù hợp trong một số trường hợp. Chẳng hạn, khi dùng một Label để hiển thị tên người chơi, rất có thể bạn không muốn tên người chơi bị dịch nếu nó khớp với một key bản dịch. Để tắt tính năng dịch tự động trên một node cụ thể, hãy đặt :ui:`Auto Translate > Mode` thành ``Disabled`` trong inspector.

Trong code, có thể sử dụng hàm :ref:`Object.tr() <class_Object_method_tr>`. Hàm này chỉ tra cứu văn bản trong các bản dịch và chuyển đổi văn bản nếu tìm thấy:

.. tabs::
 .. code-tab:: gdscript

    level.text = tr("LEVEL_5_NAME")
    status.text = tr("GAME_STATUS_%d" % status_index)

 .. code-tab:: csharp

    level.Text = Tr("LEVEL_5_NAME");
    status.Text = Tr($"GAME_STATUS_{statusIndex}");

.. note::

    Nếu không có văn bản nào được hiển thị sau khi thay đổi ngôn ngữ, hãy thử sử dụng font khác. Font mặc định của project chỉ hỗ trợ một phần của bộ ký tự Latin-1, nên không thể dùng để hiển thị các ngôn ngữ như tiếng Nga hoặc tiếng Trung.

    Một tài nguyên tốt về font đa ngôn ngữ là `Noto Fonts <https://www.google.com/get/noto/>`__. Hãy đảm bảo tải đúng biến thể nếu bạn sử dụng một ngôn ngữ ít phổ biến hơn.

    Sau khi tải font xuống, hãy nạp tệp TTF vào một tài nguyên DynamicFont và sử dụng nó làm custom font cho node Control. Để tái sử dụng tốt hơn, hãy gán một tài nguyên Theme mới cho node Control gốc và định nghĩa DynamicFont làm Default Font trong theme.

Placeholder
~~~~~~~~~~~

Để đưa placeholder vào các chuỗi đã dịch, hãy sử dụng
:ref:`doc_gdscript_printf` hoặc tính năng tương đương trong C#. Điều này cho phép người dịch tự do thay đổi vị trí của placeholder trong chuỗi, giúp bản dịch nghe tự nhiên hơn. Nên sử dụng placeholder có tên với hàm ``String.format()`` bất cứ khi nào có thể, vì chúng cũng cho phép người dịch chọn *thứ tự* xuất hiện của các placeholder:

.. tabs::
 .. code-tab:: gdscript

    # Có thể thay đổi vị trí của placeholder, nhưng không thể thay đổi thứ tự của chúng.
    # Điều này có thể sẽ không đủ cho một số ngôn ngữ đích.
    message.text = tr("%s picked up the %s") % ["Ogre", "Sword"]

    # Có thể thay đổi vị trí và thứ tự của placeholder.
    # Ngoài ra, dạng này cung cấp nhiều ngữ cảnh hơn để người dịch làm việc.
    message.text = tr("{character} picked up the {weapon}").format({character = "Ogre", weapon = "Sword"})

.. _doc_internationalizing_games_translation_contexts:

Ngữ cảnh bản dịch
~~~~~~~~~~~~~~~~~

Nếu bạn sử dụng tiếng Anh thuần túy làm chuỗi nguồn (thay vì mã thông báo ``LIKE_THIS``), bạn có thể gặp phải sự mơ hồ khi cần dịch cùng một chuỗi tiếng Anh thành các chuỗi khác nhau trong một số ngôn ngữ đích. Bạn có thể tùy chọn chỉ định *ngữ cảnh bản dịch* để giải quyết sự mơ hồ này và cho phép các ngôn ngữ đích sử dụng các chuỗi khác nhau, dù chuỗi nguồn giống hệt nhau:

.. tabs::
 .. code-tab:: gdscript

    # "Đóng", theo nghĩa là một hành động (đóng một thứ gì đó).
    button.set_text(tr("Close", "Actions"))

    # "Gần", theo nghĩa là khoảng cách (trái nghĩa với "xa").
    distance_label.set_text(tr("Close", "Distance"))

 .. code-tab:: csharp

    // "Đóng", theo nghĩa là một hành động (đóng một thứ gì đó).
    GetNode<Button>("Button").Text = Tr("Close", "Actions");

    // "Gần", theo nghĩa là khoảng cách (trái nghĩa với "xa").
    GetNode<Label>("Distance").Text = Tr("Close", "Distance");

.. _doc_internationalizing_games_pluralization:

Số nhiều
~~~~~~~~

Hầu hết các ngôn ngữ yêu cầu các chuỗi khác nhau tùy theo một đối tượng ở dạng số ít hay số nhiều. Tuy nhiên, việc hardcode điều kiện "là số nhiều" dựa trên việc có nhiều hơn 1 đối tượng không hợp lệ trong mọi ngôn ngữ.

Một số ngôn ngữ có hơn hai dạng số nhiều, và quy tắc về số lượng đối tượng cần có cho mỗi dạng số nhiều cũng khác nhau. Godot hỗ trợ *số nhiều* để các locale đích có thể tự động xử lý việc này.

Số nhiều chỉ nên được sử dụng với các số nguyên dương (hoặc bằng không). Các giá trị âm và số thực thường biểu thị những thực thể vật lý mà việc áp dụng dạng số ít hay số nhiều không rõ ràng.

.. tabs::
 .. code-tab:: gdscript

    var num_apples = 5
    label.text = tr_n("There is %d apple", "There are %d apples", num_apples) % num_apples

 .. code-tab:: csharp

    int numApples = 5;
    GetNode<Label>("Label").Text = string.Format(TrN("There is {0} apple", "There are {0} apples", numApples), numApples);

Bạn có thể kết hợp tính năng này với một ngữ cảnh nếu cần:

.. tabs::
 .. code-tab:: gdscript

    var num_jobs = 1
    label.text = tr_n("%d job", "%d jobs", num_jobs, "Task Manager") % num_jobs

 .. code-tab:: csharp

    int numJobs = 1;
    GetNode<Label>("Label").Text = string.Format(TrN("{0} job", "{0} jobs", numJobs, "Task Manager"), numJobs);

Cho phép các control thay đổi kích thước
----------------------------------------

Cùng một văn bản trong các ngôn ngữ khác nhau có thể có độ dài chênh lệch đáng kể. Vì vậy, hãy đọc tutorial về :ref:`doc_size_and_anchors`, vì việc điều chỉnh kích thước control một cách linh động có thể hữu ích.
:ref:`Container <class_Container>` cũng có thể hữu ích, cùng với các tùy chọn wrapping văn bản có trong :ref:`Label <class_Label>`.

Để kiểm tra xem UI của bạn có thể hiển thị các bản dịch dài hơn chuỗi gốc hay không, bạn có thể bật :ref:`pseudolocalization <doc_pseudolocalization>` trong Project Settings nâng cao. Tính năng này sẽ thay thế tất cả chuỗi có thể bản địa hóa bằng các phiên bản dài hơn của chúng, đồng thời thay thế một số ký tự trong chuỗi gốc bằng các phiên bản có dấu (nhưng vẫn có thể đọc được). Các placeholder được giữ nguyên để tiếp tục hoạt động khi pseudolocalization được bật.

Ví dụ: chuỗi ``Hello world, this is %s!`` sẽ trở thành ``[Ĥéłłô ŵôŕłd́, ŧh̀íš íš %s!]`` khi pseudolocalization được bật.

Mặc dù ban đầu trông khá lạ, pseudolocalization có một số lợi ích:

- Tính năng này giúp bạn nhanh chóng phát hiện các chuỗi không thể bản địa hóa, để bạn có thể xem xét và biến chúng thành các chuỗi có thể bản địa hóa (nếu phù hợp).
- Tính năng này giúp bạn kiểm tra các phần tử UI không thể chứa các chuỗi dài. Nhiều ngôn ngữ sẽ có bản dịch dài hơn đáng kể so với văn bản nguồn, vì vậy điều quan trọng là phải bảo đảm UI của bạn có thể hiển thị các chuỗi dài hơn bình thường.
- Tính năng này giúp bạn kiểm tra xem font có chứa tất cả các ký tự cần thiết để hỗ trợ nhiều ngôn ngữ hay không. Tuy nhiên, vì mục tiêu của pseudolocalization là giữ cho các chuỗi gốc có thể đọc được, đây không phải là một phép kiểm tra hiệu quả để xác định liệu font có hỗ trợ :abbr:`CJK (tiếng Trung, tiếng Nhật, tiếng Hàn)` hoặc các ngôn ngữ viết từ phải sang trái hay không.

Project Settings cho phép bạn tinh chỉnh hành vi của pseudolocalization, để có thể tắt từng phần nếu muốn.

TranslationServer
-----------------

Godot có một server xử lý việc quản lý bản dịch cấp thấp, được gọi là :ref:`TranslationServer <class_TranslationServer>`. Có thể thêm hoặc xóa bản dịch trong runtime; ngôn ngữ hiện tại cũng có thể được thay đổi trong runtime.

.. _doc_internationalizing_games_bidi:

Văn bản hai chiều và phản chiếu UI
----------------------------------

Tiếng Ả Rập và tiếng Do Thái được viết từ phải sang trái (ngoại trừ các số và từ Latin xen kẽ), đồng thời giao diện người dùng cho các ngôn ngữ này cũng nên được phản chiếu. Trong một số ngôn ngữ, hình dạng của glyph thay đổi tùy theo các ký tự xung quanh.

Việc hỗ trợ các hệ thống chữ viết hai chiều và phản chiếu UI được thực hiện trong suốt; thông thường bạn không cần thay đổi gì hoặc phải hiểu biết về hệ thống chữ viết cụ thể.

Đối với các ngôn ngữ RTL, Godot sẽ tự động thực hiện các thay đổi sau đối với UI:

- Phản chiếu các anchor và margin trái/phải.
- Hoán đổi căn chỉnh văn bản trái và phải.
- Phản chiếu thứ tự ngang của các control con trong container và các mục trong control Tree/ItemList.
- Sử dụng thứ tự phản chiếu của các phần tử control nội bộ (ví dụ: nút dropdown của OptionButton, căn chỉnh CheckBox/CheckButton, thứ tự cột của List, icon TreeItem và căn chỉnh đường nối). Trong một số trường hợp, các control được phản chiếu sử dụng các theme style riêng biệt.
- Hệ tọa độ **không** được phản chiếu.
- Các node không thuộc UI (sprite, v.v.) **không** bị ảnh hưởng.

Bạn có thể ghi đè hướng bố cục văn bản và control bằng các thuộc tính control sau:

- ``text_direction``, thiết lập hướng văn bản cơ sở. Khi được đặt thành "auto", hướng này phụ thuộc vào ký tự định hướng mạnh đầu tiên trong văn bản theo Unicode Bidirectional Algorithm.
- ``language``, ghi đè locale hiện tại của project.
- Thuộc tính ``structured_text_bidi_override`` và callback ``_structured_text_parser`` cho phép xử lý đặc biệt đối với văn bản có cấu trúc.
- ``layout_direction``, ghi đè việc phản chiếu control.

.. image:: img/ui_mirror.png

.. seealso::

    Bạn có thể xem cách dàn chữ từ phải sang trái hoạt động trong thực tế bằng project demo `BiDI and Font Features demo project <https://github.com/godotengine/godot-demo-projects/tree/master/gui/bidi_and_font_features>`__.

Thêm dữ liệu break iterator vào project đã export
-------------------------------------------------

Một số ngôn ngữ được viết không có khoảng trắng. Trong các ngôn ngữ đó, việc ngắt từ và ngắt dòng cần nhiều hơn các quy tắc trên chuỗi ký tự. Godot tích hợp dữ liệu break iterator dựa trên quy tắc và từ điển của ICU, nhưng dữ liệu này không được đưa vào các project đã export theo mặc định.

Để đưa dữ liệu này vào, hãy đi tới :menu:`Project > Project Settings > General > Internationalization > Locale` và bật :ui:`Include Text Server Data`, sau đó export project. Dữ liệu break iterator có kích thước khoảng 4 MB.

Ghi đè BiDi cho văn bản có cấu trúc
-----------------------------------

Thuật toán Unicode BiDi được thiết kế để hoạt động với văn bản tự nhiên và không thể xử lý văn bản có thứ tự ở cấp cao hơn, chẳng hạn như tên tệp, URI, địa chỉ email, regular expression hoặc mã nguồn.

.. image:: img/bidi_override.png

Ví dụ: đường dẫn cho cấu trúc thư mục được minh họa này sẽ hiển thị không chính xác (control "LineEdit" ở trên). Override văn bản có cấu trúc kiểu "File" sẽ chia văn bản thành các đoạn, sau đó áp dụng thuật toán BiDi cho từng đoạn riêng lẻ để hiển thị chính xác tên thư mục bằng mọi ngôn ngữ và giữ đúng thứ tự các thư mục (control "LineEdit" ở dưới).

Custom callback cung cấp một cách để override BiDi cho các kiểu văn bản có cấu trúc khác.

Bản địa hóa số
--------------

Các control được thiết kế riêng cho việc nhập hoặc xuất số (ví dụ: ProgressBar, SpinBox) sẽ tự động sử dụng hệ thống đánh số đã bản địa hóa; đối với các control khác
:ref:`TextServer.format_number(string, language) <class_TextServer_method_format_number>` có thể được dùng để chuyển đổi các chữ số Ả Rập phương Tây (0..9) sang hệ thống đánh số đã bản địa hóa và :ref:`TextServer.parse_number(string, language) <class_TextServer_method_parse_number>` để chuyển đổi ngược lại.

Bản địa hóa biểu tượng và hình ảnh
----------------------------------

Các biểu tượng có mũi tên hướng sang trái và phải có thể cần được đảo ngược đối với locale tiếng Ả Rập và tiếng Hebrew nếu chúng biểu thị chuyển động hoặc hướng (ví dụ: các nút quay lại/tiến tới). Nếu không, chúng có thể được giữ nguyên.

Kiểm thử bản dịch
-----------------

Bạn có thể muốn kiểm thử bản dịch của một project trước khi phát hành. Godot cung cấp ba cách để thực hiện việc này.

Trong :menu:`Project > Project Settings > General > Internationalization > Locale` (khi đã bật các thiết lập nâng cao) có một thuộc tính :ui:`Test`. Hãy đặt thuộc tính này thành mã locale của ngôn ngữ bạn muốn kiểm thử. Godot sẽ chạy project với locale đó khi project được chạy (từ editor hoặc khi được export).

.. image:: img/locale_test.webp

Lưu ý rằng vì đây là một thiết lập của project, nó sẽ xuất hiện trong hệ thống kiểm soát phiên bản khi được đặt thành một giá trị không rỗng. Do đó, cần đặt lại thành giá trị rỗng trước khi commit các thay đổi vào hệ thống kiểm soát phiên bản.

Thứ hai, từ bên trong editor, hãy đi đến thanh trên cùng và nhấp vào :button:`View` trên thanh trên cùng, sau đó đi xuống :ui:`Preview Translation` và chọn ngôn ngữ bạn muốn xem trước.

.. image:: img/locale_editor_preview.webp

Lúc này, toàn bộ văn bản trong các scene ở editor sẽ được hiển thị bằng ngôn ngữ đã chọn.

Bản dịch cũng có thể được kiểm thử khi :ref:`chạy Godot từ dòng lệnh <doc_command_line_tutorial>`. Ví dụ, để kiểm thử game bằng tiếng Pháp, có thể cung cấp đối số sau:

.. code-block:: shell

   godot --language fr

Dịch tên project
----------------

Tên project trở thành tên ứng dụng khi export sang các hệ điều hành và nền tảng khác nhau. Để chỉ định tên project bằng nhiều ngôn ngữ, hãy đi đến :menu:`Project > Project Settings > General > Application > Config`. Từ đây, nhấp vào nút :button:`Localizable String (Size 0)`, sau đó nhấp vào nút :button:`Add Translation`. Bạn sẽ được chuyển đến một trang, tại đó có thể chọn ngôn ngữ (và quốc gia nếu cần) cho bản dịch tên project. Sau đó, bạn có thể nhập tên đã bản địa hóa.

.. image:: img/localized_name.webp

Nếu không chắc chắn về mã ngôn ngữ cần sử dụng, hãy tham khảo
:ref:`danh sách mã locale <doc_locales>`.

.. _`download it from the Asset Library`: https://godotengine.org/asset-library/asset/2776
