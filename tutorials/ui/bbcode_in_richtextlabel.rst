.. _doc_bbcode_in_richtextlabel:

BBCode trong RichTextLabel
==========================

Giới thiệu
----------

:ref:`class_Label` nodes are great for displaying basic text, but they have limitations.
Nếu muốn thay đổi màu văn bản hoặc căn chỉnh văn bản, bạn chỉ có thể áp dụng cho toàn bộ label. Bạn không thể làm cho một phần văn bản có màu khác hoặc căn giữa một phần văn bản. Để khắc phục những hạn chế này, bạn có thể sử dụng :ref:`class_RichTextLabel`.

:ref:`class_RichTextLabel` allows for complex formatting of text using a markup syntax or
API tích hợp sẵn. API này sử dụng BBCode làm cú pháp markup, một hệ thống các tag xác định quy tắc định dạng cho một phần văn bản. Bạn có thể đã quen thuộc với chúng nếu từng sử dụng các diễn đàn (còn được gọi là `bulletin boards`, do đó có "BB" trong "BBCode").

Không giống Label, RichTextLabel cũng có thanh cuộn dọc riêng. Thanh cuộn này tự động hiển thị nếu văn bản không vừa với kích thước của control. Bạn có thể tắt thanh cuộn bằng cách bỏ chọn thuộc tính **Scroll Active** trong inspector của RichTextLabel.

Lưu ý rằng các tag BBCode cũng có thể được sử dụng ở một mức độ nhất định cho các trường hợp sử dụng khác:

- BBCode có thể được sử dụng để :ref:`format comments in the XML source of the class reference <doc_class_reference_bbcode>`. - BBCode có thể được sử dụng trong :ref:`GDScript documentation comments <doc_gdscript_documentation_comments_bbcode_and_class_reference>`. - BBCode có thể được sử dụng khi :ref:`printing rich text to the Output bottom panel <doc_output_panel_printing_rich_text>`.

.. seealso::

    Bạn có thể xem BBCode trong RichTextLabel hoạt động như thế nào qua `Rich Text Label with BBCode demo project <https://github.com/godotengine/godot-demo-projects/tree/master/gui/rich_text_bbcode>`__.

Sử dụng BBCode
--------------

Theo mặc định, :ref:`class_RichTextLabel` hoạt động như một :ref:`class_Label` thông thường. Nó có thuộc tính :ref:`text <class_RichTextLabel_property_text>`, bạn có thể chỉnh sửa thuộc tính này để văn bản được định dạng đồng nhất. Để có thể sử dụng BBCode cho việc định dạng văn bản phong phú, bạn cần bật chế độ BBCode bằng cách đặt :ref:`bbcode_enabled <class_RichTextLabel_property_bbcode_enabled>`. Sau đó, bạn có thể chỉnh sửa thuộc tính :ref:`text <class_RichTextLabel_property_text>` bằng các tag khả dụng. Cả hai thuộc tính đều nằm ở đầu inspector sau khi chọn một node RichTextLabel.

.. image:: img/bbcode_in_richtextlabel_inspector.webp

Ví dụ, ``BBCode [color=green]test[/color]`` sẽ hiển thị từ "test" bằng màu xanh lá.

.. image:: img/bbcode_in_richtextlabel_basic_example.webp

Hầu hết BBCode gồm 3 phần: tag mở, nội dung và tag đóng. Tag mở đánh dấu phần bắt đầu của vùng được định dạng và cũng có thể chứa một số tùy chọn cấu hình. Một số tag mở, như tag ``color`` được minh họa ở trên, cũng yêu cầu một giá trị để hoạt động. Các tag mở khác có thể chấp nhận nhiều tùy chọn (được phân tách bằng khoảng trắng bên trong tag mở). Tag đóng đánh dấu phần kết thúc của vùng được định dạng. Trong một số trường hợp, cả tag đóng và nội dung đều có thể được bỏ qua.

Không giống BBCode trong HTML, khoảng trắng ở đầu/cuối không bị RichTextLabel loại bỏ khi hiển thị. Các khoảng trắng trùng lặp cũng được hiển thị nguyên trạng trong kết quả cuối cùng. Điều này có nghĩa là khi hiển thị một khối mã trong RichTextLabel, bạn không cần sử dụng tag văn bản được định dạng trước.

.. code-block:: none

  [tag]content[/tag]
  [tag=value]content[/tag]
  [tag option1=value1 option2=value2]content[/tag]
  [tag][/tag]
  [tag]

.. note::

    RichTextLabel không hỗ trợ các tag BBCode lồng chéo. Ví dụ, thay vì sử dụng:

    ::

        [b]bold[i]bold italic[/b]italic[/i]

    Hãy sử dụng:

    ::

        [b]bold[i]bold italic[/i][/b][i]italic[/i]

.. _doc_bbcode_in_richtextlabel_handling_user_input_safely:

Xử lý đầu vào của người dùng an toàn
------------------------------------

Trong trường hợp người dùng có thể tự do nhập văn bản (chẳng hạn như chat trong một game nhiều người chơi), bạn nên đảm bảo người dùng không thể sử dụng các tag BBCode tùy ý được RichTextLabel phân tích. Điều này nhằm tránh việc sử dụng định dạng không phù hợp, có thể gây ra vấn đề nếu các tag ``[url]`` được RichTextLabel xử lý (vì người chơi có thể tạo các liên kết có thể nhấp đến các trang web lừa đảo hoặc tương tự).

Bằng cách sử dụng các tag ``[lb]`` và/hoặc ``[rb]`` của RichTextLabel, chúng ta có thể thay thế dấu ngoặc mở và/hoặc đóng của bất kỳ tag BBCode nào trong một message bằng các tag đã escape tương ứng. Điều này ngăn người dùng sử dụng BBCode được phân tích dưới dạng tag – thay vào đó, BBCode sẽ được hiển thị dưới dạng văn bản.

.. figure:: img/bbcode_in_richtextlabel_escaping_user_input.webp
   :align: center
   :alt: Example of unescaped user input resulting in BBCode injection (2nd line) and escaped user input (3rd line)

   Example of unescaped user input resulting in BBCode injection (2nd line) and escaped user input (3rd line)

Hình ảnh trên được tạo bằng script sau:

::

    extends RichTextLabel

    func _ready():
        append_chat_line("Player 1", "Hello world!")
        append_chat_line("Player 2", "Hello [color=red]BBCode injection[/color] (no escaping)!")
        append_chat_line_escaped("Player 2", "Hello [color=red]BBCode injection[/color] (with escaping)!")


    # Trả về BBCode đã escape, không bị RichTextLabel phân tích dưới dạng tag.
    func escape_bbcode(bbcode_text):
        # Chúng ta chỉ cần thay thế các dấu ngoặc mở để ngăn tag bị phân tích.
        return bbcode_text.replace("[", "[lb]")


    # Thêm message của người dùng nguyên trạng, không escape. Điều này rất nguy hiểm!
    func append_chat_line(username, message):
        append_text("%s: [color=green]%s[/color]\n" % [username, message])


    # Thêm message của người dùng sau khi escape.
    # Hãy nhớ escape cả tên người chơi và nội dung message.
    func append_chat_line_escaped(username, message):
        append_text("%s: [color=green]%s[/color]\n" % [escape_bbcode(username), escape_bbcode(message)])

Loại bỏ các tag BBCode
----------------------

Đối với một số trường hợp sử dụng, bạn có thể muốn xóa các tag BBCode khỏi chuỗi. Điều này hữu ích khi hiển thị văn bản của RichTextLabel trong một Control khác không hỗ trợ BBCode (chẳng hạn như tooltip):

.. code::

    extends RichTextLabel

    func _ready():
        var regex = RegEx.new()
        regex.compile("\\[.*?\\]")
        var text_without_tags = regex.sub(text, "", true)
        # `text_without_tags` chứa văn bản đã xóa toàn bộ tag BBCode.

.. note::

    Không nên xóa hoàn toàn các tag BBCode đối với đầu vào của người dùng, vì điều này có thể thay đổi văn bản hiển thị mà người dùng không hiểu tại sao một phần message của họ lại bị xóa.
    :ref:`Escaping user input <doc_bbcode_in_richtextlabel_handling_user_input_safely>`
    thay vào đó nên được ưu tiên sử dụng.

Hiệu năng
---------

Trong hầu hết trường hợp, bạn có thể sử dụng BBCode nguyên trạng vì việc định dạng văn bản hiếm khi là tác vụ nặng. Tuy nhiên, với các RichTextLabel đặc biệt lớn (chẳng hạn như nhật ký console dài hàng nghìn dòng), bạn có thể gặp hiện tượng giật trong lúc chơi game khi văn bản của RichTextLabel được cập nhật.

Có một số cách để giảm vấn đề này:

- Sử dụng hàm ``append_text()`` thay vì nối vào thuộc tính ``text``. Hàm này chỉ phân tích BBCode cho phần văn bản được thêm vào, thay vì phân tích BBCode từ toàn bộ thuộc tính ``text``. - Sử dụng các hàm ``push_[tag]()`` và ``pop()`` để thêm tag vào RichTextLabel thay vì sử dụng BBCode. - Bật thuộc tính **Threading > Threaded** trong RichTextLabel. Điều này không làm tăng tốc quá trình xử lý, nhưng sẽ ngăn main thread bị block, nhờ đó tránh hiện tượng giật trong lúc chơi game. Chỉ bật threading nếu project của bạn thực sự cần, vì threading có một số overhead.

.. _doc_bbcode_in_richtextlabel_use_functions:

Sử dụng các hàm push_[tag]() và pop() thay cho BBCode
-----------------------------------------------------

Nếu không muốn sử dụng BBCode vì lý do hiệu năng, bạn có thể sử dụng các hàm do RichTextLabel cung cấp để tạo các tag định dạng mà không cần viết BBCode trong văn bản.

Mỗi tag BBCode (bao gồm cả effect) đều có một hàm ``push_[tag]()`` (trong đó ``[tag]`` là tên của tag). Ngoài ra còn có một số hàm tiện ích, chẳng hạn như ``push_bold_italics()``, kết hợp cả ``push_bold()`` và ``push_italics()`` thành một tag duy nhất. Xem các hàm
:ref:`RichTextLabel class reference <class_RichTextLabel>` for a complete list of
``push_[tag]()``.

Hàm ``pop()`` được dùng để kết thúc *bất kỳ* tag nào. Vì BBCode là một *stack* tag, việc sử dụng ``pop()`` sẽ đóng các tag được bắt đầu gần nhất trước.

Script sau sẽ cho kết quả hiển thị giống như khi sử dụng ``BBCode [color=green]test [i]example[/i][/color]``:

::

    extends RichTextLabel

    func _ready():
        append_text("BBCode ")  # Khoảng trắng ở cuối phân tách các từ với nhau.
        push_color(Color.GREEN)
        append_text("test ")  # Khoảng trắng ở cuối phân tách các từ với nhau.
        push_italics()
        append_text("example")
        pop()  # Kết thúc tag được mở bởi `push_italics()`.
        pop()  # Kết thúc tag được mở bởi `push_color()`.

.. warning::

    **Không** đặt trực tiếp thuộc tính ``text`` khi sử dụng các hàm định dạng. Việc nối vào thuộc tính ``text`` sẽ xóa mọi thay đổi được thực hiện trên RichTextLabel bằng các hàm ``append_text()``, ``push_[tag]()`` và ``pop()``.

Tham khảo
---------

.. seealso::

    *Một số* tag BBCode này có thể được sử dụng trong tooltip cho các biến script ``@export``, cũng như trong XML source của class reference. Để biết thêm thông tin, hãy xem :ref:`Class reference BBCode <doc_class_reference_bbcode>`.

.. list-table::
  :class: wrap-normal
  :width: 100%
  :widths: 60 40

  * - Tag
    - Ví dụ

  * - | **b**
      | Khiến ``{text}`` sử dụng font đậm (hoặc đậm nghiêng) của ``RichTextLabel``.

    - ``[b]{text}[/b]``

  * - | **i**
      | Khiến ``{text}`` sử dụng font nghiêng (hoặc đậm nghiêng) của ``RichTextLabel``.

    - ``[i]{text}[/i]``

  * - | **u**
      | Gạch chân ``{text}``.

    - ``[u]{text}[/u]``
      ``[u color={color}]{text}[/u]``

  * - | **s**
      | Gạch ngang ``{text}``.

    - ``[s]{text}[/s]``
      ``[s color={color}]{text}[/s]``

  * - | **code**
      | Khiến ``{text}`` sử dụng font mono của ``RichTextLabel``.

    - ``[code]{text}[/code]``

  * - | **char**
      | Thêm ký tự Unicode với ``{codepoint}`` UTF-32 ở dạng thập lục phân.

    - ``[char={codepoint}]``

  * - | **p**
      | Thêm đoạn văn mới với ``{text}``. Hỗ trợ các tùy chọn cấu hình,
        xem :ref:`doc_bbcode_in_richtextlabel_paragraph_options`.

    - | ``[p]{text}[/p]``
      | ``[p {options}]{text}[/p]``

  * - | **br**
      | Thêm ngắt dòng vào văn bản mà không thêm đoạn văn mới.
        Nếu được sử dụng bên trong danh sách, tag này sẽ không tạo mục danh sách mới,
        mà thay vào đó sẽ thêm ngắt dòng bên trong mục hiện tại.

    - ``[br]``

  * - | **hr**
      | Thêm đường kẻ ngang mới để phân tách nội dung. Hỗ trợ các tùy chọn cấu hình,
        xem :ref:`doc_bbcode_in_richtextlabel_hr_options`.

    - | ``[hr]``
      | ``[hr {options}]``

  * - | **center**
      | Căn giữa ``{text}`` theo chiều ngang.
      | Giống ``[p align=center]``.

    - ``[center]{text}[/center]``

  * - | **left**
      | Căn ``{text}`` về bên trái theo chiều ngang.
      | Giống ``[p align=left]``.

    - ``[left]{text}[/left]``

  * - | **right**
      | Căn ``{text}`` về bên phải theo chiều ngang.
      | Giống ``[p align=right]``.

    - ``[right]{text}[/right]``

  * - | **fill**
      | Khiến ``{text}`` lấp đầy toàn bộ chiều rộng của ``RichTextLabel``.
      | Giống ``[p align=fill]``.

    - ``[fill]{text}[/fill]``

  * - | **indent**
      | Thụt lề ``{text}`` một lần.
        Độ rộng thụt lề giống với ``[ul]`` hoặc ``[ol]``, nhưng không có dấu đầu dòng.

    - ``[indent]{text}[/indent]``

  * - | **url**
      | Tạo một siêu liên kết (văn bản được gạch chân và có thể nhấp vào). Có thể chứa tùy chọn
        ``{text}`` hoặc hiển thị ``{link}`` nguyên trạng. Hỗ trợ các tùy chọn cấu hình,
        xem :ref:`doc_bbcode_in_richtextlabel_url_options`.
      | **Phải được xử lý bằng signal "meta_clicked" để có hiệu lực,** xem :ref:`doc_bbcode_in_richtextlabel_handling_url_tag_clicks`.

    - | ``[url]{link}[/url]``
      | ``[url={link}]{text}[/url]``
      | ``[url {options}]{text}[/url]``

  * - | **hint**
      | Tạo một gợi ý tooltip được hiển thị khi di chuột lên văn bản.
        Mặc dù không bắt buộc, bạn nên đặt văn bản tooltip giữa dấu ngoặc kép hoặc dấu nháy đơn.
        Lưu ý rằng không thể escape dấu nháy bằng ``\"`` hoặc ``\'``. Để sử dụng
        dấu nháy đơn cho dấu lược trong chuỗi gợi ý, bạn phải dùng dấu ngoặc kép
        để bao quanh chuỗi.
    - | ``[hint="{tooltip text displayed on hover}"]{text}[/hint]``

  * - | **img**
      | Chèn một hình ảnh từ ``{path}`` (có thể là bất kỳ resource :ref:`class_Texture2D` hợp lệ nào).
      | Nếu cung cấp ``{width}``, hình ảnh sẽ cố gắng vừa với chiều rộng đó trong khi vẫn giữ
        tỷ lệ khung hình.
      | Nếu cung cấp cả ``{width}`` và ``{height}``, hình ảnh sẽ được scale
        theo kích thước đó.
      | Thêm ``%`` vào cuối giá trị ``{width}`` hoặc ``{height}`` để chỉ định giá trị đó theo phần trăm chiều rộng của control thay vì pixel.
      | Thêm ``em`` vào cuối giá trị ``{width}`` hoặc ``{height}`` để chỉ định giá trị đó theo tỷ lệ so với cỡ chữ hiện tại. Ví dụ, ``height=1em`` sẽ làm cho hình ảnh cao bằng văn bản xung quanh.
      | Nếu cung cấp cấu hình ``{valign}``, hình ảnh sẽ cố gắng căn chỉnh với
        văn bản xung quanh, xem :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment`.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_image_options`.

    - | ``[img]{path}[/img]``
      | ``[img={width}]{path}[/img]``
      | ``[img={width}x{height}]{path}[/img]``
      | ``[img={valign}]{path}[/img]``
      | ``[img {options}]{path}[/img]``

  * - | **font**
      | Khiến ``{text}`` sử dụng một font resource từ ``{path}``.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_font_options`.

    - | ``[font={path}]{text}[/font]``
      | ``[font {options}]{text}[/font]``

  * - | **font_size**
      | Sử dụng cỡ chữ tùy chỉnh cho ``{text}``.

    - ``[font_size={size}]{text}[/font_size]``

  * - | **dropcap**
      | Sử dụng cỡ chữ và màu khác cho ``{text}``, đồng thời khiến nội dung của tag
        trải dài qua nhiều dòng nếu đủ lớn.
      | Một `drop cap <https://www.computerhope.com/jargon/d/dropcap.htm>`__ thường là một
        ký tự viết hoa, nhưng ``[dropcap]`` hỗ trợ chứa nhiều ký tự.
        Các giá trị ``margins`` được phân tách bằng dấu phẩy và có thể dương, bằng không hoặc âm.
        Các giá trị **không được** phân tách bằng khoảng trắng; nếu không, chúng sẽ không được phân tích cú pháp chính xác.
        Lề trên và dưới âm đặc biệt hữu ích để cho phép phần còn lại của
        đoạn văn hiển thị bên dưới dropcap.

    - ``[dropcap font={font} font_size={size} color={color} outline_size={size} outline_color={color} margins={left},{top},{right},{bottom}]{text}[/dropcap]``

  * - | **opentype_features**
      | Bật các tính năng font OpenType tùy chỉnh cho ``{text}``. Các tính năng phải được cung cấp dưới dạng
        một ``{list}`` được phân tách bằng dấu phẩy. Các giá trị **không được** phân tách bằng khoảng trắng;
        nếu không, danh sách sẽ không được phân tích cú pháp chính xác.

    - | ``[opentype_features={list}]``
      | ``{text}``
      | ``[/opentype_features]``

  * - | **lang**
      | Ghi đè ngôn ngữ cho ``{text}`` được đặt bởi thuộc tính **BiDi > Language**
        trong :ref:`class_RichTextLabel`. ``{code}`` phải là một :ref:`language code <doc_locales>` ISO.
        Có thể dùng tùy chọn này để buộc sử dụng một script cụ thể cho một ngôn ngữ mà không
        bắt đầu một đoạn văn mới. Một số file font có thể chứa các thay thế dành riêng cho script,
        trong trường hợp đó chúng sẽ được sử dụng.

    - ``[lang={code}]{text}[/lang]``

  * - | **color**
      | Thay đổi màu của ``{text}``. Màu phải được cung cấp bằng một tên thông dụng (xem
        :ref:`doc_bbcode_in_richtextlabel_named_colors`) or using the HEX format (e.g.
        ``#ff00ff``, xem :ref:`doc_bbcode_in_richtextlabel_hex_colors`).

    - ``[color={code/name}]{text}[/color]``

  * - | **bgcolor**
      | Vẽ màu phía sau ``{text}``. Có thể dùng tùy chọn này để làm nổi bật văn bản.
        Chấp nhận các giá trị giống như tag ``color``.
        Theo mặc định, có một khoảng đệm nhỏ được điều khiển bởi
        các theme item ``text_highlight_h_padding`` và ``text_highlight_v_padding``
        trong node RichTextLabel. Đặt padding thành ``0`` để tránh các vấn đề chồng lấn tiềm ẩn
        khi có màu nền trên các dòng/cột liền kề.

    - ``[bgcolor={code/name}]{text}[/bgcolor]``

  * - | **fgcolor**
      | Vẽ màu phía trước ``{text}``. Có thể dùng màu tiền cảnh đục để "che" văn bản.
        Chấp nhận các giá trị giống như tag ``color``.
        Theo mặc định, có một khoảng đệm nhỏ được điều khiển bởi
        các theme item ``text_highlight_h_padding`` và ``text_highlight_v_padding``
        trong node RichTextLabel. Đặt padding thành ``0`` để tránh các vấn đề chồng lấn tiềm ẩn
        khi có màu tiền cảnh trên các dòng/cột liền kề.

    - ``[fgcolor={code/name}]{text}[/fgcolor]``

  * - | **outline_size**
      | Sử dụng kích thước outline font tùy chỉnh cho ``{text}``.

    - | ``[outline_size={size}]``
      | ``{text}``
      | ``[/outline_size]``

  * - | **outline_color**
      | Sử dụng màu outline tùy chỉnh cho ``{text}``. Chấp nhận các giá trị giống như tag ``color``.

    - | ``[outline_color={code/name}]``
      | ``{text}``
      | ``[/outline_color]``

  * - | **table**
      | Tạo một bảng với ``{number}`` cột. Sử dụng tag ``cell`` để định nghĩa
        các ô của bảng.
      | Nếu cung cấp cấu hình ``{valign}``, bảng sẽ cố gắng căn chỉnh với
        văn bản xung quanh, xem :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment`.
      | Nếu sử dụng căn chỉnh theo baseline, bảng sẽ được căn chỉnh theo baseline của hàng có chỉ số ``{alignment_row}`` (bắt đầu từ 0).
      | ``{name}`` là tên bảng dành cho các ứng dụng hỗ trợ (trình đọc màn hình).

    - | ``[table={number}]{cells}[/table]``
      | ``[table={number},{valign}]{cells}[/table]``
      | ``[table={number},{valign},{alignment_row}]{cells}[/table]``
      | ``[table={number},{valign},{alignment_row} name={name}]{cells}[/table]``

  * - | **cell**
      | Thêm một ô có ``{text}`` vào bảng.
      | Nếu cung cấp ``{ratio}``, ô sẽ cố gắng mở rộng theo tỷ lệ đến giá trị đó
        so với các ô khác và các giá trị tỷ lệ của chúng.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_cell_options`.

    - | ``[cell]{text}[/cell]``
      | ``[cell={ratio}]{text}[/cell]``
      | ``[cell {options}]{text}[/cell]``

  * - | **ul**
      | Thêm danh sách không có thứ tự. ``{items}`` của danh sách phải được cung cấp bằng cách đặt mỗi mục trên một
        dòng văn bản.
      | Có thể tùy chỉnh dấu đầu dòng bằng tham số ``{bullet}``,
        xem :ref:`doc_bbcode_in_richtextlabel_unordered_list_bullet`.

    - | ``[ul]{items}[/ul]``
      | ``[ul bullet={bullet}]{items}[/ul]``

  * - | **ol**
      | Thêm danh sách có thứ tự (đánh số) của ``{type}`` đã cho (xem :ref:`doc_bbcode_in_richtextlabel_list_types`).
        ``{items}`` của danh sách phải được cung cấp bằng cách đặt mỗi mục trên một dòng văn bản.

    - ``[ol type={type}]{items}[/ol]``

  * - | **lb**, **rb**
      | Lần lượt thêm ``[`` và ``]``. Cho phép escape markup BBCode.
      | Đây là các tag tự đóng, nghĩa là bạn không cần đóng chúng
        (và không có tag đóng ``[/lb]`` hoặc ``[/rb]``).

    - | ``[lb]b[rb]text[lb]/b[rb]`` sẽ hiển thị dưới dạng ``[b]text[/b]``.

  * - | Có thể thêm một số ký tự điều khiển Unicode bằng các tag tự đóng riêng.
      | Điều này có thể giúp bảo trì dễ dàng hơn so với việc dán trực tiếp các
      ký tự điều khiển đó vào văn bản.

    - | ``[lrm]`` (dấu từ trái sang phải), ``[rlm]`` (dấu từ phải sang trái), ``[lre]`` (nhúng từ trái sang phải),
      | ``[rle]`` (nhúng từ phải sang trái), ``[lro]`` (ghi đè từ trái sang phải), ``[rlo]`` (ghi đè từ phải sang trái),
      | ``[pdf]`` (loại định dạng hướng), ``[alm]`` (dấu chữ Ả Rập), ``[lri]`` (cô lập từ trái sang phải),
      | ``[rli]`` (cô lập từ phải sang trái), ``[fsi]`` (cô lập mạnh đầu tiên), ``[pdi]`` (loại cô lập hướng),
      | ``[zwj]`` (bộ nối độ rộng bằng không), ``[zwnj]`` (bộ không nối độ rộng bằng không), ``[wj]`` (bộ nối từ),
      | ``[shy]`` (dấu gạch nối mềm)

.. note::

    Các thẻ định dạng in đậm (``[b]``) và in nghiêng (``[i]``) hoạt động tốt nhất nếu các font tùy chỉnh tương ứng được thiết lập trong phần ghi đè theme của RichTextLabelNode. Nếu không xác định font in đậm hoặc in nghiêng tùy chỉnh, `faux bold and italic fonts <https://fonts.google.com/knowledge/glossary/faux_fake_pseudo_synthesized>`__ sẽ được Godot tạo. Những font này hiếm khi có hình thức đẹp bằng các biến thể font in đậm/in nghiêng được tạo thủ công.

    Thẻ monospaced (``[code]``) **chỉ** hoạt động nếu một font tùy chỉnh được thiết lập trong phần ghi đè theme của node RichTextLabel. Nếu không, văn bản monospaced sẽ sử dụng font thông thường.

    Hiện chưa có thẻ BBCode để điều khiển việc căn giữa theo chiều dọc của văn bản.

    Có thể bỏ qua các tùy chọn đối với tất cả các thẻ.

.. _doc_bbcode_in_richtextlabel_paragraph_options:

Tùy chọn đoạn văn
~~~~~~~~~~~~~~~~~

- **align**

  +-----------+----------------------------------------------------------------------------------------+
  | `Values`  | ``left`` (or ``l``), ``center`` (or ``c``), ``right`` (or ``r``), ``fill`` (or ``f``)  |
  +-----------+----------------------------------------------------------------------------------------+
  | `Default` | ``left``                                                                               |
  +-----------+----------------------------------------------------------------------------------------+

  Căn chỉnh văn bản theo chiều ngang.

- **bidi_override**, **st**

  +-----------+--------------------------------------------------------------------------------------------------------------+
  | `Values`  | ``default`` (of ``d``), ``uri`` (or ``u``), ``file`` (or ``f``), ``email`` (or ``e``), ``list`` (or ``l``),  |
  |           | ``none`` (or ``n``), ``custom`` (or ``c``)                                                                   |
  +-----------+--------------------------------------------------------------------------------------------------------------+
  | `Default` | ``default``                                                                                                  |
  +-----------+--------------------------------------------------------------------------------------------------------------+

  Ghi đè văn bản có cấu trúc.

- **justification_flags**, **jst**

  +-----------+--------------------------------------------------------------------------------------------------------+
  | `Values`  | Comma-separated list of the following values (no space after each comma):                              |
  |           | ``kashida`` (or ``k``), ``word`` (or ``w``), ``trim`` (or ``tr``), ``after_last_tab`` (or ``lt``),     |
  |           | ``skip_last`` (or ``sl``), ``skip_last_with_chars`` (or ``sv``),  ``do_not_skip_single`` (or ``ns``).  |
  +-----------+--------------------------------------------------------------------------------------------------------+
  | `Default` | ``word,kashida,skip_last,do_not_skip_single``                                                          |
  +-----------+--------------------------------------------------------------------------------------------------------+

  Tùy chọn căn đều (căn lấp đầy). Xem :ref:`class_TextServer` để biết thêm chi tiết.

- **direction**, **dir**

  +-----------+-----------------------------------------------------------------+
  | `Values`  | ``ltr`` (or ``l``), ``rtl`` (or ``r``), ``auto`` (or ``a``)     |
  +-----------+-----------------------------------------------------------------+
  | `Default` | Inherit                                                         |
  +-----------+-----------------------------------------------------------------+

  Hướng BiDi cơ sở.

- **language**, **lang**

  +-----------+--------------------------------------------+
  | `Values`  | ISO language codes. See :ref:`doc_locales` |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Ghi đè locale. Một số tệp font có thể chứa các font thay thế dành riêng cho từng script; trong trường hợp đó, chúng sẽ được sử dụng.

- **tab_stops**

  +-----------+----------------------------------------------------+
  | `Values`  | List of floating-point numbers, e.g. ``10.0,30.0`` |
  +-----------+----------------------------------------------------+
  | `Default` | Width of the space character in the font           |
  +-----------+----------------------------------------------------+

  Ghi đè các độ lệch theo chiều ngang cho từng ký tự tab. Khi đến cuối danh sách, các điểm dừng tab sẽ lặp lại. Ví dụ: nếu bạn đặt ``tab_stops`` thành ``10.0,30.0``, tab đầu tiên sẽ ở vị trí ``10`` pixel, tab thứ hai ở vị trí ``10 + 30 = 40`` pixel và tab thứ ba ở vị trí ``10 + 30 + 10 = 50`` pixel tính từ gốc của RichTextLabel.

.. _doc_bbcode_in_richtextlabel_handling_url_tag_clicks:

Xử lý thao tác nhấp vào thẻ ``[url]``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, các thẻ ``[url]`` không làm gì khi được nhấp vào. Điều này cho phép sử dụng linh hoạt các thẻ ``[url]`` thay vì giới hạn chúng vào việc mở URL trong trình duyệt web.

Để xử lý các thẻ ``[url]`` được nhấp vào, hãy kết nối node ``RichTextLabel`` với
:ref:`meta_clicked <class_RichTextLabel_signal_meta_clicked>` signal to a script function.

Ví dụ: có thể kết nối phương thức sau với ``meta_clicked`` để mở các URL được nhấp vào bằng trình duyệt web mặc định của người dùng:

::

    # Điều này giả định rằng signal `meta_clicked` của RichTextLabel đã được kết nối với
    # hàm bên dưới bằng hộp thoại kết nối signal.
    func _richtextlabel_on_meta_clicked(meta):
        # `meta` không được đảm bảo là một String, vì vậy hãy chuyển đổi nó thành một String
        # để tránh lỗi script trong runtime.
        OS.shell_open(str(meta))

Đối với các trường hợp sử dụng nâng cao hơn, bạn cũng có thể lưu JSON trong tùy chọn của thẻ ``[url]`` và phân tích cú pháp nó trong hàm xử lý signal ``meta_clicked``. Ví dụ:

.. code-block:: none

  [url={"example": "value"}]JSON[/url]


.. _doc_bbcode_in_richtextlabel_hr_options:

Tùy chọn đường kẻ ngang
~~~~~~~~~~~~~~~~~~~~~~~

- **color**

  +-----------+--------------------------------------------+
  | `Values`  | Color name or color in HEX format          |
  +-----------+--------------------------------------------+
  | `Default` | ``Color(1, 1, 1, 1)``                      |
  +-----------+--------------------------------------------+

  Màu sắc của đường kẻ (modulation).

- **height**

  +-----------+--------------------------------------------+
  | `Values`  | Integer number                             |
  +-----------+--------------------------------------------+
  | `Default` | ``2``                                      |
  +-----------+--------------------------------------------+

  Chiều cao mục tiêu của đường kẻ tính bằng pixel; thêm ``%`` vào cuối giá trị để chỉ định dưới dạng phần trăm chiều rộng của control thay vì pixel.

- **width**

  +-----------+--------------------------------------------+
  | `Values`  | Integer number                             |
  +-----------+--------------------------------------------+
  | `Default` | ``90%``                                    |
  +-----------+--------------------------------------------+

  Chiều rộng mục tiêu của đường kẻ tính bằng pixel; thêm ``%`` vào cuối giá trị để chỉ định dưới dạng phần trăm chiều rộng của control thay vì pixel.

- **align**

  +-----------+----------------------------------------------------------------------------------------+
  | `Values`  | ``left`` (or ``l``), ``center`` (or ``c``), ``right`` (or ``r``)                       |
  +-----------+----------------------------------------------------------------------------------------+
  | `Default` | ``center``                                                                             |
  +-----------+----------------------------------------------------------------------------------------+

  Căn chỉnh theo chiều ngang.


.. _doc_bbcode_in_richtextlabel_url_options:

Tùy chọn URL
~~~~~~~~~~~~

- **underline**

  +-----------+--------------------------------------------+
  | `Values`  | ``always``, ``never``, ``hover``           |
  +-----------+--------------------------------------------+
  | `Default` | ``always``                                 |
  +-----------+--------------------------------------------+

  Chế độ gạch chân URL.

- **tooltip**

  +-----------+--------------------------------------------+
  | `Values`  | String.                                    |
  +-----------+--------------------------------------------+
  | `Default` |                                            |
  +-----------+--------------------------------------------+

  Tooltip của URL.

- **href**

  +-----------+--------------------------------------------+
  | `Values`  | String.                                    |
  +-----------+--------------------------------------------+
  | `Default` |                                            |
  +-----------+--------------------------------------------+

  Địa chỉ đích của URL.


.. _doc_bbcode_in_richtextlabel_image_options:

Tùy chọn hình ảnh
~~~~~~~~~~~~~~~~~

- **color**

  +-----------+--------------------------------------------+
  | `Values`  | Color name or color in HEX format          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Màu sắc của hình ảnh (modulation).

- **height**

  +-----------+--------------------------------------------+
  | `Values`  | Floating-point number                      |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Chiều cao mục tiêu của hình ảnh tính bằng pixel.

  Có thể chỉ định các đơn vị thay thế cho pixel:

  - Thêm ``%`` vào cuối giá trị để chỉ định dưới dạng phần trăm chiều rộng của control thay vì pixel. Ví dụ, ``height=50%`` sẽ làm cho hình ảnh cao bằng một nửa chiều rộng của control.

  - Thêm ``em`` vào cuối giá trị để chỉ định dưới dạng tỷ lệ so với cỡ font xung quanh thay vì pixel. Ví dụ, ``height=1em`` sẽ làm cho hình ảnh cao bằng văn bản xung quanh.

- **width**

  +-----------+--------------------------------------------+
  | `Values`  | Floating-point number                      |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Chiều rộng mục tiêu của hình ảnh tính bằng pixel.

  Có thể chỉ định các đơn vị thay thế cho pixel:

  - Thêm ``%`` vào cuối giá trị để chỉ định dưới dạng phần trăm chiều rộng của control thay vì pixel. Ví dụ, ``width=50%`` sẽ làm cho hình ảnh chiếm một nửa chiều rộng của control.

  - Thêm ``em`` vào cuối giá trị để chỉ định dưới dạng tỷ lệ so với cỡ font xung quanh thay vì pixel. Ví dụ, ``width=1em`` sẽ làm cho hình ảnh rộng bằng chiều cao của văn bản xung quanh.

- **region**

  +-----------+--------------------------------------------+
  | `Values`  | x,y,width,height in pixels                 |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Hình chữ nhật vùng của hình ảnh. Có thể dùng tùy chọn này để hiển thị một hình ảnh đơn từ spritesheet.

- **pad**

  +-----------+--------------------------------------------+
  | `Values`  | ``false``, ``true``                        |
  +-----------+--------------------------------------------+
  | `Default` | ``false``                                  |
  +-----------+--------------------------------------------+

  Nếu được đặt thành ``true`` và hình ảnh nhỏ hơn kích thước được chỉ định bởi ``width`` và ``height``, phần đệm của hình ảnh sẽ được thêm vào để khớp kích thước thay vì phóng to.

- **tooltip**

  +-----------+--------------------------------------------+
  | `Values`  | String                                     |
  +-----------+--------------------------------------------+
  | `Default` |                                            |
  +-----------+--------------------------------------------+

  Tooltip của hình ảnh.

- **align**

  +-----------+------------------------------------------------------------------------+
  | `Values`  | see :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment`       |
  +-----------+------------------------------------------------------------------------+
  | `Default` | ``center,center``                                                      |
  +-----------+------------------------------------------------------------------------+

  Căn chỉnh hình ảnh với văn bản xung quanh.

- **alt**

  +-----------+--------------------------------------------+
  | `Values`  | String                                     |
  +-----------+--------------------------------------------+
  | `Default` |                                            |
  +-----------+--------------------------------------------+

  Mô tả hình ảnh dành cho các ứng dụng hỗ trợ (trình đọc màn hình).

.. _doc_bbcode_in_richtextlabel_image_and_table_alignment:

Căn chỉnh theo chiều dọc của hình ảnh và bảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi một giá trị căn chỉnh theo chiều dọc được cung cấp cùng thẻ ``[img]`` hoặc ``[table]``, hình ảnh/bảng sẽ cố gắng tự căn chỉnh với văn bản xung quanh. Việc căn chỉnh được thực hiện bằng cách sử dụng một điểm theo chiều dọc của hình ảnh và một điểm theo chiều dọc của văn bản. Có 3 điểm khả dụng trên hình ảnh (``top``, ``center`` và ``bottom``) và 4 điểm khả dụng trên văn bản và bảng (``top``, ``center``, ``baseline`` và ``bottom``), có thể kết hợp theo bất kỳ cách nào.

Để chỉ định cả hai điểm, hãy sử dụng tên đầy đủ hoặc tên viết tắt của chúng làm giá trị của thẻ hình ảnh/bảng:

.. code-block:: none

    text [img=top,bottom]...[/img] text
    text [img=center,center]...[/img] text

.. image:: img/bbcode_in_richtextlabel_image_align.webp

.. code-block:: none

    text [table=3,center]...[/table] text  # Giữa với giữa.
    text [table=3,top,bottom]...[/table] text # Đầu bảng với cuối văn bản.
    text [table=3,baseline,baseline,1]...[/table] text # Baseline của hàng thứ hai (các hàng được đánh chỉ mục bắt đầu từ 0) với baseline của văn bản.

.. image:: img/bbcode_in_richtextlabel_table_align.webp

Bạn cũng có thể chỉ định chỉ một giá trị (``top``, ``center`` hoặc ``bottom``) để sử dụng preset tương ứng (``top-top``, ``center-center`` và ``bottom-bottom``).

Tên viết tắt của các giá trị là ``t`` (``top``), ``c`` (``center``), ``l`` (``baseline``) và ``b`` (``bottom``).


.. _doc_bbcode_in_richtextlabel_font_options:

Tùy chọn font
~~~~~~~~~~~~~

- **name**, **n**

  +-----------+--------------------------------------------+
  | `Values`  | A valid Font resource path.                |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Đường dẫn tài nguyên font.

- **size**, **s**

  +-----------+--------------------------------------------+
  | `Values`  | Number in pixels.                          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Cỡ font tùy chỉnh.

- **glyph_spacing**, **gl**

  +-----------+--------------------------------------------+
  | `Values`  | Number in pixels.                          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Khoảng cách bổ sung cho từng glyph.

- **space_spacing**, **sp**

  +-----------+--------------------------------------------+
  | `Values`  | Number in pixels.                          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Khoảng cách bổ sung cho ký tự dấu cách.

- **top_spacing**, **top**

  +-----------+--------------------------------------------+
  | `Values`  | Number in pixels.                          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Khoảng cách bổ sung ở phía trên dòng.

- **bottom_spacing**, **bt**

  +-----------+--------------------------------------------+
  | `Values`  | Number in pixels.                          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Khoảng cách bổ sung ở phía dưới dòng.

- **embolden**, **emb**

  +-----------+--------------------------------------------+
  | `Values`  | Floating-point number.                     |
  +-----------+--------------------------------------------+
  | `Default` | ``0.0``                                    |
  +-----------+--------------------------------------------+

  Độ mạnh làm đậm font; nếu khác không, tùy chọn này sẽ làm đậm các đường viền của font. Giá trị âm làm giảm độ dày đường viền.

- **face_index**, **fi**

  +-----------+--------------------------------------------+
  | `Values`  | Integer number.                            |
  +-----------+--------------------------------------------+
  | `Default` | ``0``                                      |
  +-----------+--------------------------------------------+

  Chỉ mục face đang hoạt động trong bộ sưu tập TrueType / OpenType.

- **slant**, **sln**

  +-----------+--------------------------------------------+
  | `Values`  | Floating-point number.                     |
  +-----------+--------------------------------------------+
  | `Default` | ``0.0``                                    |
  +-----------+--------------------------------------------+

  Độ mạnh nghiêng của font; giá trị dương làm nghiêng glyph sang phải, giá trị âm làm nghiêng sang trái.

- **opentype_variation**, **otv**

  +-----------+----------------------------------------------------------------------------------+
  | `Values`  | Comma-separated list of the OpenType variation tags (no space after each comma). |
  +-----------+----------------------------------------------------------------------------------+
  | `Default` |                                                                                  |
  +-----------+----------------------------------------------------------------------------------+

  Tọa độ biến thiên OpenType của font. Xem `OpenType variation tags <https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg>`__.

  Lưu ý: Giá trị phải được đặt trong ``"`` để cho phép sử dụng ``=`` bên trong:

.. code-block:: none

    [font otv="wght=200,wdth=400"] # Thiết lập độ đậm và chiều rộng của font biến thiên.

- **opentype_features**, **otf**

  +-----------+--------------------------------------------------------------------------------+
  | `Values`  | Comma-separated list of the OpenType feature tags (no space after each comma). |
  +-----------+--------------------------------------------------------------------------------+
  | `Default` |                                                                                |
  +-----------+--------------------------------------------------------------------------------+

  Các tính năng OpenType của font. Xem `OpenType features tags <https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>`__.

  Lưu ý: Giá trị phải được đặt trong ``"`` để cho phép sử dụng ``=`` bên trong:

.. code-block:: none

    [font otf="calt=0,zero=1"] # Tắt các biến thể theo ngữ cảnh, bật số 0 có gạch chéo.

.. _doc_bbcode_in_richtextlabel_named_colors:

Tên màu
~~~~~~~

Đối với các thẻ cho phép chỉ định màu theo tên, bạn có thể sử dụng tên của các hằng số trong class :ref:`class_Color` tích hợp sẵn. Có thể chỉ định tên màu theo nhiều kiểu viết hoa khác nhau: ``DARK_RED``, ``DarkRed`` và ``darkred`` sẽ cho cùng một kết quả chính xác.

Xem hình ảnh này để biết danh sách các hằng số màu:

.. image:: /img/color_constants.png

`View at full size <https://raw.githubusercontent.com/godotengine/godot-docs/master/img/color_constants.png>`__

.. _doc_bbcode_in_richtextlabel_hex_colors:

Mã màu thập lục phân
~~~~~~~~~~~~~~~~~~~~

Đối với màu RGB không trong suốt, mọi mã thập lục phân 6 chữ số hợp lệ đều được hỗ trợ, ví dụ: ``[color=#ffffff]white[/color]``. Các mã màu RGB rút gọn như ``#6f2`` (tương đương với ``#66ff22``) cũng được hỗ trợ.

Đối với màu RGB trong suốt, có thể sử dụng mọi mã thập lục phân RGBA 8 chữ số, ví dụ: ``[color=#ffffff88]translucent white[/color]``. Lưu ý rằng kênh alpha là thành phần **cuối cùng** của mã màu, không phải thành phần đầu tiên. Các mã màu RGBA rút gọn như ``#6f28`` (tương đương với ``#66ff2288``) cũng được hỗ trợ.

.. _doc_bbcode_in_richtextlabel_cell_options:

Tùy chọn ô
~~~~~~~~~~

- **shrink**

  +-----------+--------------------------------------------+
  | `Values`  | ``false``, ``true``                        |
  +-----------+--------------------------------------------+
  | `Default` | ``true``                                   |
  +-----------+--------------------------------------------+

  Nếu là ``true``, ô có thể thu nhỏ theo nội dung của nó.

- **expand**

  +-----------+--------------------------------------------+
  | `Values`  | Integer number                             |
  +-----------+--------------------------------------------+
  | `Default` | 1                                          |
  +-----------+--------------------------------------------+

  Tỷ lệ mở rộng ô. Tùy chọn này xác định những ô nào sẽ cố gắng mở rộng theo tỷ lệ với các ô khác và tỷ lệ mở rộng của chúng.

- **border**

  +-----------+--------------------------------------------+
  | `Values`  | Color name or color in HEX format          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Màu đường viền của ô.

- **bg**

  +-----------+--------------------------------------------+
  | `Values`  | Color name or color in HEX format          |
  +-----------+--------------------------------------------+
  | `Default` | Inherit                                    |
  +-----------+--------------------------------------------+

  Màu nền của ô. Để tạo nền cho các hàng lẻ/chẵn xen kẽ, bạn có thể sử dụng ``bg=odd_color,even_color``.

- **padding**

  +-----------+--------------------------------------------------------------------------+
  | `Values`  | 4 comma-separated floating-point numbers (no space after each comma)     |
  +-----------+--------------------------------------------------------------------------+
  | `Default` | ``0,0,0,0``                                                              |
  +-----------+--------------------------------------------------------------------------+

  Khoảng đệm bên trái, bên trên, bên phải và bên dưới của ô.

.. _doc_bbcode_in_richtextlabel_unordered_list_bullet:

Dấu đầu dòng của danh sách không có thứ tự
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, thẻ ``[ul]`` sử dụng ký tự Unicode ``U+2022`` "Bullet" làm ký tự đầu dòng. Cách hoạt động này tương tự các trình duyệt web. Bạn có thể tùy chỉnh ký tự đầu dòng bằng ``[ul bullet={bullet}]``. Nếu được cung cấp, tham số ``{bullet}`` này phải là một chuỗi không có dấu ngoặc kép bao quanh (ví dụ: ``[bullet=*]``). Bạn có thể thêm khoảng trắng ở cuối sau ký tự đầu dòng để tăng khoảng cách giữa ký tự đầu dòng và văn bản của mục.

Xem `Bullet (typography) on Wikipedia <https://en.wikipedia.org/wiki/Bullet_(typography)>`__ để biết danh sách các ký tự đầu dòng phổ biến mà bạn có thể dán trực tiếp vào tham số ``bullet``.

.. _doc_bbcode_in_richtextlabel_list_types:

Các loại danh sách có thứ tự
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Danh sách có thứ tự có thể được sử dụng để tự động đánh dấu các mục bằng số hoặc chữ cái theo thứ tự tăng dần. Thẻ này hỗ trợ các tùy chọn type sau:

- ``1`` - Số, sử dụng hệ thống đánh số riêng của ngôn ngữ nếu có thể. - ``a``, ``A`` - Chữ cái Latin viết thường và viết hoa. - ``i``, ``I`` - Chữ số La Mã viết thường và viết hoa.

Hiệu ứng văn bản
----------------

BBCode cũng có thể được sử dụng để tạo các hiệu ứng văn bản khác nhau, tùy chọn có thể được animate. Một số hiệu ứng có thể tùy chỉnh được cung cấp sẵn, và bạn có thể dễ dàng tạo hiệu ứng của riêng mình. Theo mặc định, các hiệu ứng được animate sẽ tạm dừng
:ref:`when the SceneTree is paused <doc_pausing_games>`. You can change this
hoạt động bằng cách điều chỉnh thuộc tính **Process > Mode** của RichTextLabel.

Tất cả các ví dụ bên dưới đều đề cập đến các giá trị mặc định của những tùy chọn trong định dạng thẻ được liệt kê.

.. note::

    Các hiệu ứng văn bản làm thay đổi vị trí của ký tự có thể khiến ký tự bị cắt theo ranh giới của node RichTextLabel.

    Bạn có thể khắc phục điều này bằng cách tắt **Control > Layout > Clip Contents** trong inspector sau khi chọn node RichTextLabel, hoặc đảm bảo có đủ khoảng cách xung quanh văn bản bằng cách sử dụng ngắt dòng bên trên và bên dưới dòng sử dụng hiệu ứng.

Pulse
~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_pulse.webp

Pulse tạo hiệu ứng nhấp nháy được animate, làm thay đổi độ mờ và màu của từng ký tự. Có thể dùng hiệu ứng này để thu hút sự chú ý vào văn bản cụ thể. Định dạng thẻ của nó là ``[pulse freq=1.0 color=#ffffff40 ease=-2.0]{text}[/pulse]``.

``freq`` kiểm soát tần số của chu kỳ nhấp nháy một nửa (giá trị càng cao thì càng nhanh). Một chu kỳ nhấp nháy đầy đủ mất ``2 * (1.0 / freq)`` giây. ``color`` là hệ số màu mục tiêu dùng cho hiệu ứng nhấp nháy. Theo mặc định, văn bản hầu như mờ đi hoàn toàn, nhưng không hoàn toàn. ``ease`` là số mũ của hàm easing được sử dụng. Các giá trị âm cung cấp easing in-out, đó là lý do giá trị mặc định là ``-2.0``.

Wave
~~~~

.. image:: img/bbcode_in_richtextlabel_effect_wave.webp

Wave làm cho văn bản di chuyển lên xuống. Định dạng thẻ của nó là ``[wave amp=50.0 freq=5.0 connected=1]{text}[/wave]``.

``amp`` kiểm soát độ cao và độ thấp của hiệu ứng, còn ``freq`` kiểm soát tốc độ văn bản di chuyển lên xuống. Giá trị ``freq`` bằng ``0`` sẽ khiến không có sóng nào hiển thị, và các giá trị ``freq`` âm cũng sẽ không hiển thị sóng. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph sẽ được di chuyển riêng lẻ ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề render với font ligature.

Tornado
~~~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_tornado.webp

Tornado làm cho văn bản di chuyển theo vòng tròn. Định dạng thẻ của nó là ``[tornado radius=10.0 freq=1.0 connected=1]{text}[/tornado]``.

``radius`` là bán kính của vòng tròn kiểm soát độ lệch, còn ``freq`` là tốc độ văn bản di chuyển theo vòng tròn. Giá trị ``freq`` bằng ``0`` sẽ tạm dừng animation, còn ``freq`` âm sẽ phát animation theo chiều ngược lại. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph sẽ được di chuyển riêng lẻ ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề render với font ligature.

Shake
~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_shake.webp

Shake làm cho văn bản rung. Định dạng thẻ của nó là ``[shake rate=20.0 level=5 connected=1]{text}[/shake]``.

``rate`` kiểm soát tốc độ rung của văn bản, còn ``level`` kiểm soát độ lệch của văn bản so với gốc. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph sẽ được di chuyển riêng lẻ ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề render với font ligature.

Fade
~~~~

.. image:: img/bbcode_in_richtextlabel_effect_fade.webp

Fade tạo hiệu ứng mờ tĩnh, làm thay đổi độ mờ của từng ký tự. Định dạng thẻ của nó là ``[fade start=4 length=14]{text}[/fade]``.

``start`` kiểm soát vị trí bắt đầu của độ suy giảm so với vị trí chèn lệnh fade, còn ``length`` kiểm soát hiệu ứng mờ dần sẽ diễn ra trong bao nhiêu ký tự.

Rainbow
~~~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_rainbow.webp

Rainbow tạo cho văn bản màu cầu vồng thay đổi theo thời gian. Định dạng thẻ của nó là ``[rainbow freq=1.0 sat=0.8 val=0.8 speed=1.0]{text}[/rainbow]``.

``freq`` xác định số lượng chữ cái mà cầu vồng kéo dài qua trước khi lặp lại, ``sat`` là độ bão hòa của cầu vồng, còn ``val`` là value của cầu vồng. ``speed`` là số chu kỳ cầu vồng đầy đủ mỗi giây. Giá trị ``speed`` dương sẽ phát animation theo chiều thuận, giá trị ``0`` sẽ tạm dừng animation, còn giá trị ``speed`` âm sẽ phát animation theo chiều ngược lại.

Outline của font *không* bị ảnh hưởng bởi hiệu ứng rainbow (chúng giữ nguyên màu ban đầu). Các màu font hiện có sẽ bị hiệu ứng rainbow ghi đè. Tuy nhiên, các thuộc tính **Modulate** và **Self Modulate** của CanvasItem sẽ ảnh hưởng đến hình thức của hiệu ứng rainbow, vì modulation nhân với màu cuối cùng của nó.

Thẻ BBCode và hiệu ứng văn bản tùy chỉnh
----------------------------------------

Bạn có thể mở rộng loại resource :ref:`class_RichTextEffect` để tạo các thẻ BBCode tùy chỉnh của riêng mình. Tạo một file script mới mở rộng loại resource :ref:`class_RichTextEffect` và đặt cho script một ``class_name`` để hiệu ứng có thể được chọn trong inspector. Thêm annotation ``@tool`` vào file GDScript nếu bạn muốn các hiệu ứng tùy chỉnh này chạy ngay trong editor. RichTextLabel không cần gắn script, cũng không cần chạy ở ``tool`` mode. Bạn có thể đăng ký hiệu ứng mới trong Inspector bằng cách thêm nó vào mảng **Markup > Custom Effects**, hoặc trong code bằng
:ref:`install_effect() <class_RichTextLabel_method_install_effect>` method:

.. figure:: img/bbcode_in_richtextlabel_selecting_custom_richtexteffect.webp
   :align: center
   :alt: Selecting a custom RichTextEffect after saving a script that extends RichTextEffect with a ``class_name``

   Selecting a custom RichTextEffect after saving a script that extends RichTextEffect with a ``class_name``

.. warning::

    Nếu hiệu ứng tùy chỉnh chưa được đăng ký trong thuộc tính **Markup > Custom Effects** của RichTextLabel, sẽ không có hiệu ứng nào hiển thị và thẻ gốc sẽ được giữ nguyên.

Chỉ có một function mà bạn cần mở rộng: ``_process_custom_fx(char_fx)``. Ngoài ra, bạn cũng có thể cung cấp một identifier BBCode tùy chỉnh bằng cách thêm member name ``bbcode``. Code sẽ tự động kiểm tra thuộc tính ``bbcode`` hoặc sử dụng tên file để xác định thẻ BBCode.

``_process_custom_fx``
~~~~~~~~~~~~~~~~~~~~~~

Đây là nơi logic của từng hiệu ứng được thực thi và được gọi một lần cho mỗi glyph trong giai đoạn vẽ của quá trình render văn bản. Hàm này truyền vào một object :ref:`class_CharFXTransform`, chứa một số biến để kiểm soát cách glyph tương ứng được render:

- ``outline`` là ``true`` nếu hiệu ứng được gọi để vẽ outline của văn bản. - ``range`` cho biết bạn đã đi được bao xa trong một block hiệu ứng tùy chỉnh nhất định, dưới dạng một index. - ``elapsed_time`` là tổng thời gian hiệu ứng văn bản đã chạy. - ``visible`` cho biết glyph có hiển thị hay không, đồng thời cho phép bạn ẩn một phần văn bản nhất định. - ``offset`` là vị trí offset tương đối so với vị trí glyph tương ứng sẽ render trong điều kiện bình thường. - ``color`` là màu của một glyph. - ``glyph_index`` và ``font`` lần lượt là glyph đang được vẽ và resource dữ liệu font được dùng để vẽ glyph đó. - Cuối cùng, ``env`` là một :ref:`class_Dictionary` các parameter được gán cho một hiệu ứng tùy chỉnh nhất định. Bạn có thể sử dụng :ref:`get() <class_Dictionary_method_get>` cùng với một giá trị mặc định tùy chọn để truy xuất từng parameter, nếu người dùng đã chỉ định. Ví dụ, ``[custom_fx spread=0.5 color=#FFFF00]test[/custom_fx]`` sẽ có các parameter float ``spread`` và Color ``color`` trong Dictionary ``env``. Xem bên dưới để biết thêm các ví dụ sử dụng.

Điều cuối cùng cần lưu ý về function này là bạn cần trả về một giá trị boolean ``true`` để xác nhận rằng hiệu ứng đã được xử lý chính xác. Nhờ đó, nếu có vấn đề khi render một glyph nào đó, hệ thống sẽ ngừng hoàn toàn việc render các hiệu ứng tùy chỉnh cho đến khi người dùng khắc phục lỗi phát sinh trong logic hiệu ứng tùy chỉnh.

Dưới đây là một số ví dụ về hiệu ứng tùy chỉnh:

Ghost
~~~~~

::

    @tool
    extends RichTextEffect
    class_name RichTextGhost

    # Cú pháp: [ghost freq=5.0 span=10.0][/ghost]

    # Xác định tên thẻ.
    var bbcode = "ghost"

    func _process_custom_fx(char_fx):
        # Lấy các parameter hoặc sử dụng giá trị mặc định được cung cấp nếu thiếu.
        var speed = char_fx.env.get("freq", 5.0)
        var span = char_fx.env.get("span", 10.0)

        var alpha = sin(char_fx.elapsed_time * speed + (char_fx.range.x / span)) * 0.5 + 0.5
        char_fx.color.a = alpha
        return true

Matrix
~~~~~~

::

    @tool
    extends RichTextEffect
    class_name RichTextMatrix

    # Cú pháp: [matrix clean=2.0 dirty=1.0 span=50][/matrix]

    # Xác định tên thẻ.
    var bbcode = "matrix"

    # Lấy TextServer để truy xuất thông tin font.
    func get_text_server():
        return TextServerManager.get_primary_interface()

    func _process_custom_fx(char_fx):
        # Lấy các parameter hoặc sử dụng giá trị mặc định được cung cấp nếu thiếu.
        var clear_time = char_fx.env.get("clean", 2.0)
        var dirty_time = char_fx.env.get("dirty", 1.0)
        var text_span = char_fx.env.get("span", 50)

        var value = get_text_server().font_get_char_from_glyph_index(char_fx.font, 1, char_fx.glyph_index)

        var matrix_time = fmod(char_fx.elapsed_time + (char_fx.range.x / float(text_span)), \
                               clear_time + dirty_time)

        matrix_time = 0.0 if matrix_time < clear_time else \
                      (matrix_time - clear_time) / dirty_time

        if matrix_time > 0.0:
            value = int(1 * matrix_time * (126 - 65))
            value %= (126 - 65)
            value += 65
        char_fx.glyph_index = get_text_server().font_get_glyph_index(char_fx.font, 1, value, 0)
        return true

Thao tác này sẽ thêm một số lệnh BBCode mới, có thể được sử dụng như sau:

.. code-block:: none

    [center][ghost]This is a custom [matrix]effect[/matrix][/ghost] made in
    [pulse freq=5.0 height=2.0][pulse color=#00FFAA freq=2.0]GDScript[/pulse][/pulse].[/center]
