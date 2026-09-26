.. _doc_bbcode_in_richtextlabel:

BBCode trong RichTextLabel
==========================

Giới thiệu
----------

:ref:`class_Label` node rất phù hợp để hiển thị văn bản cơ bản, nhưng chúng có những hạn chế. Nếu muốn thay đổi màu hoặc căn chỉnh văn bản, bạn chỉ có thể áp dụng cho toàn bộ label. Bạn không thể làm cho một phần văn bản có màu khác hoặc căn giữa một phần văn bản. Để khắc phục những hạn chế này, bạn có thể sử dụng :ref:`class_RichTextLabel`.

:ref:`class_RichTextLabel` cho phép định dạng văn bản phức tạp bằng cú pháp markup hoặc API tích hợp sẵn. Nó sử dụng BBCode cho cú pháp markup, một hệ thống các tag xác định quy tắc định dạng cho một phần văn bản. Có thể bạn đã quen thuộc với chúng nếu từng sử dụng forum (còn được gọi là `bulletin boards`, do đó có "BB" trong "BBCode").

Không giống Label, RichTextLabel còn có thanh cuộn dọc riêng. Thanh cuộn này tự động hiển thị nếu văn bản không vừa với kích thước của control. Bạn có thể tắt thanh cuộn bằng cách bỏ chọn thuộc tính **Scroll Active** trong inspector của RichTextLabel.

Lưu ý rằng các tag BBCode cũng có thể được sử dụng ở một mức độ nhất định cho các trường hợp khác:

- Có thể dùng BBCode để :ref:`định dạng comment trong mã nguồn XML của tài liệu tham chiếu lớp <doc_class_reference_bbcode>`.
- Có thể dùng BBCode trong :ref:`comment tài liệu GDScript <doc_gdscript_documentation_comments_bbcode_and_class_reference>`.
- Có thể dùng BBCode khi :ref:`in văn bản có định dạng phong phú vào panel Output ở dưới cùng <doc_output_panel_printing_rich_text>`.

.. seealso::

    Bạn có thể xem BBCode trong RichTextLabel hoạt động như thế nào qua `project demo Rich Text Label with BBCode <https://github.com/godotengine/godot-demo-projects/tree/master/gui/rich_text_bbcode>`__.

Sử dụng BBCode
--------------

Theo mặc định, :ref:`class_RichTextLabel` hoạt động như một :ref:`class_Label` thông thường. Nó có thuộc tính :ref:`text <class_RichTextLabel_property_text>`, cho phép bạn chỉnh sửa để văn bản được định dạng đồng nhất. Để có thể sử dụng BBCode cho việc định dạng văn bản phong phú, bạn cần bật chế độ BBCode bằng cách đặt :ref:`bbcode_enabled <class_RichTextLabel_property_bbcode_enabled>`. Sau đó, bạn có thể chỉnh sửa thuộc tính :ref:`text <class_RichTextLabel_property_text>` bằng các tag có sẵn. Cả hai thuộc tính đều nằm ở đầu inspector sau khi chọn một node RichTextLabel.

.. image:: img/bbcode_in_richtextlabel_inspector.webp

Ví dụ, ``BBCode [color=green]test[/color]`` sẽ hiển thị từ "test" với màu xanh lục.

.. image:: img/bbcode_in_richtextlabel_basic_example.webp

Hầu hết BBCode gồm 3 phần: tag mở, nội dung và tag đóng. Tag mở đánh dấu phần bắt đầu của đoạn được định dạng, đồng thời có thể chứa một số tùy chọn cấu hình. Một số tag mở, chẳng hạn tag ``color`` được minh họa ở trên, cũng yêu cầu một giá trị để hoạt động. Các tag mở khác có thể nhận nhiều tùy chọn (được phân tách bằng dấu cách bên trong tag mở). Tag đóng đánh dấu phần kết thúc của đoạn được định dạng. Trong một số trường hợp, có thể bỏ qua cả tag đóng và nội dung.

Không giống BBCode trong HTML, khoảng trắng ở đầu/cuối không bị RichTextLabel loại bỏ khi hiển thị. Các khoảng trắng trùng lặp cũng được hiển thị nguyên trạng trong kết quả cuối cùng. Điều này có nghĩa là khi hiển thị một khối code trong RichTextLabel, bạn không cần sử dụng tag văn bản được định dạng sẵn.

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

Xử lý input của người dùng an toàn
----------------------------------

Trong trường hợp người dùng có thể tự do nhập văn bản (chẳng hạn như chat trong game multiplayer), bạn nên đảm bảo người dùng không thể sử dụng các tag BBCode tùy ý được RichTextLabel phân tích. Điều này nhằm tránh việc sử dụng định dạng không phù hợp, có thể gây ra vấn đề nếu RichTextLabel của bạn xử lý các tag ``[url]`` (vì người chơi có thể tạo các liên kết có thể nhấp đến những trang phishing hoặc tương tự).

Bằng cách sử dụng các tag ``[lb]`` và/hoặc ``[rb]`` của RichTextLabel, chúng ta có thể thay thế dấu ngoặc mở và/hoặc đóng của bất kỳ tag BBCode nào trong một message bằng các tag đã escape đó. Điều này ngăn người dùng sử dụng BBCode được phân tích như tag – thay vào đó, BBCode sẽ được hiển thị dưới dạng văn bản.

.. figure:: img/bbcode_in_richtextlabel_escaping_user_input.webp
   :align: center
   :alt: Ví dụ về input người dùng chưa được escape dẫn đến việc chèn BBCode (dòng 2) và input người dùng đã được escape (dòng 3)

   Ví dụ về input người dùng chưa được escape dẫn đến việc chèn BBCode (dòng 2) và input người dùng đã được escape (dòng 3)

Hình ảnh trên được tạo bằng script sau:

.. code-block::

    extends RichTextLabel

    func _ready():
        append_chat_line("Player 1", "Hello world!")
        append_chat_line("Player 2", "Hello [color=red]BBCode injection[/color] (no escaping)!")
        append_chat_line_escaped("Player 2", "Hello [color=red]BBCode injection[/color] (with escaping)!")


    # Trả về BBCode đã được escape và sẽ không được RichTextLabel phân tích dưới dạng tag.
    func escape_bbcode(bbcode_text):
        # Chúng ta chỉ cần thay thế các dấu ngoặc mở để ngăn tag bị phân tích.
        return bbcode_text.replace("[", "[lb]")


    # Nối message của người dùng nguyên trạng, không escape. Điều này rất nguy hiểm!
    func append_chat_line(username, message):
        append_text("%s: [color=green]%s[/color]\n" % [username, message])


    # Nối message của người dùng sau khi escape.
    # Hãy nhớ escape cả tên người chơi và nội dung message.
    func append_chat_line_escaped(username, message):
        append_text("%s: [color=green]%s[/color]\n" % [escape_bbcode(username), escape_bbcode(message)])

Loại bỏ tag BBCode
------------------

Trong một số trường hợp, bạn có thể muốn xóa các tag BBCode khỏi chuỗi. Điều này hữu ích khi hiển thị văn bản của RichTextLabel trong một Control khác không hỗ trợ BBCode (chẳng hạn như tooltip):

.. code::

    extends RichTextLabel

    func _ready():
        var regex = RegEx.new()
        regex.compile("\\[.*?\\]")
        var text_without_tags = regex.sub(text, "", true)
        # `text_without_tags` chứa văn bản đã xóa tất cả tag BBCode.

.. note::

    Không nên xóa hoàn toàn các tag BBCode đối với input của người dùng, vì điều đó có thể sửa đổi văn bản được hiển thị mà người dùng không hiểu tại sao một phần message của họ bị xóa.
    Thay vào đó, nên ưu tiên :ref:`escape input của người dùng <doc_bbcode_in_richtextlabel_handling_user_input_safely>`.

Hiệu năng
---------

Trong hầu hết trường hợp, bạn có thể sử dụng BBCode nguyên trạng vì việc định dạng văn bản hiếm khi là tác vụ nặng. Tuy nhiên, với RichTextLabel đặc biệt lớn (chẳng hạn như log console dài hàng nghìn dòng), bạn có thể gặp hiện tượng giật trong khi chơi game khi văn bản của RichTextLabel được cập nhật.

Có một số cách để giảm vấn đề này:

- Sử dụng hàm ``append_text()`` thay vì nối vào thuộc tính ``text``. Hàm này chỉ phân tích BBCode cho phần văn bản được thêm vào, thay vì phân tích BBCode từ toàn bộ thuộc tính ``text``.
- Sử dụng các hàm ``push_[tag]()`` và ``pop()`` để thêm tag vào RichTextLabel thay vì sử dụng BBCode.
- Bật thuộc tính **Threading > Threaded** trong RichTextLabel. Điều này không làm tăng tốc quá trình xử lý, nhưng sẽ ngăn main thread bị chặn, qua đó tránh hiện tượng giật trong khi chơi game. Chỉ bật threading nếu project của bạn thực sự cần, vì threading có một phần overhead.

.. _doc_bbcode_in_richtextlabel_use_functions:

Sử dụng các hàm push_[tag]() và pop() thay vì BBCode
----------------------------------------------------

Nếu không muốn sử dụng BBCode vì lý do hiệu năng, bạn có thể dùng các hàm do RichTextLabel cung cấp để tạo tag định dạng mà không cần viết BBCode trong văn bản.

Mỗi thẻ BBCode (bao gồm cả các hiệu ứng) đều có một hàm ``push_[tag]()`` (trong đó ``[tag]`` là tên của thẻ). Ngoài ra còn có một số hàm tiện ích, chẳng hạn như ``push_bold_italics()``, kết hợp cả ``push_bold()`` và ``push_italics()`` thành một thẻ duy nhất. Xem
:ref:`tài liệu tham khảo lớp RichTextLabel <class_RichTextLabel>` để xem danh sách đầy đủ các hàm ``push_[tag]()``.

Hàm ``pop()`` được dùng để kết thúc *bất kỳ* thẻ nào. Vì BBCode là một *ngăn xếp* thẻ, việc sử dụng ``pop()`` sẽ đóng các thẻ được bắt đầu gần nhất trước.

Đoạn script sau sẽ cho kết quả hiển thị giống với khi sử dụng ``BBCode [color=green]test [i]example[/i][/color]``:

.. code-block::

    extends RichTextLabel

    func _ready():
        append_text("BBCode ")  # Khoảng trắng ở cuối phân tách các từ với nhau.
        push_color(Color.GREEN)
        append_text("test ")  # Khoảng trắng ở cuối phân tách các từ với nhau.
        push_italics()
        append_text("example")
        pop()  # Kết thúc thẻ được mở bởi `push_italics()`.
        pop()  # Kết thúc thẻ được mở bởi `push_color()`.

.. warning::

    **Không** đặt trực tiếp thuộc tính ``text`` khi sử dụng các hàm định dạng. Việc nối thêm vào thuộc tính ``text`` sẽ xóa mọi thay đổi được thực hiện trên RichTextLabel bằng các hàm ``append_text()``, ``push_[tag]()`` và ``pop()``.

Tham khảo
---------

.. seealso::

    *Một số* thẻ BBCode này có thể được sử dụng trong chú giải công cụ cho các biến ``@export`` script cũng như trong mã nguồn XML của tài liệu tham khảo lớp. Để biết thêm thông tin, hãy xem :ref:`BBCode trong tài liệu tham khảo lớp <doc_class_reference_bbcode>`.

.. list-table::
  :class: wrap-normal
  :width: 100%
  :widths: 60 40

  * - Thẻ
    - Ví dụ

  * - | **b**
      | Khiến ``{text}`` sử dụng phông chữ đậm (hoặc đậm nghiêng) của ``RichTextLabel``.

    - ``[b]{text}[/b]``

  * - | **i**
      | Khiến ``{text}`` sử dụng phông chữ nghiêng (hoặc đậm nghiêng) của ``RichTextLabel``.

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
      | Khiến ``{text}`` sử dụng phông chữ mono của ``RichTextLabel``.

    - ``[code]{text}[/code]``

  * - | **char**
      | Thêm ký tự Unicode với ``{codepoint}`` UTF-32 dạng thập lục phân.

    - ``[char={codepoint}]``

  * - | **p**
      | Thêm đoạn văn mới với ``{text}``. Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_paragraph_options`.

    - | ``[p]{text}[/p]``
      | ``[p {options}]{text}[/p]``

  * - | **br**
      | Thêm ngắt dòng vào văn bản mà không thêm đoạn văn mới. Nếu được sử dụng bên trong danh sách, nó sẽ không tạo mục danh sách mới mà thay vào đó thêm ngắt dòng bên trong mục hiện tại.

    - ``[br]``

  * - | **hr**
      | Thêm một đường kẻ ngang mới để phân tách nội dung. Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_hr_options`.

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
      | Thụt lề ``{text}`` một lần. Độ rộng thụt lề giống với ``[ul]`` hoặc ``[ol]``, nhưng không có dấu đầu dòng.

    - ``[indent]{text}[/indent]``

  * - | **url**
      | Tạo một hyperlink (văn bản được gạch chân và có thể nhấp). Có thể chứa ``{text}`` tùy chọn hoặc hiển thị ``{link}`` nguyên dạng. Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_url_options`.
      | **Phải được xử lý bằng signal "meta_clicked" để có tác dụng,** xem :ref:`doc_bbcode_in_richtextlabel_handling_url_tag_clicks`.

    - | ``[url]{link}[/url]``
      | ``[url={link}]{text}[/url]``
      | ``[url {options}]{text}[/url]``

  * - | **hint**
      | Tạo gợi ý chú giải công cụ được hiển thị khi di chuột lên văn bản. Dù không bắt buộc, bạn nên đặt văn bản chú giải công cụ giữa dấu ngoặc kép hoặc dấu nháy đơn. Lưu ý rằng không thể escape dấu ngoặc kép bằng ``\"`` hoặc ``\'``. Để sử dụng dấu nháy đơn cho dấu nháy đơn trong chuỗi gợi ý, bạn phải dùng dấu ngoặc kép để bao quanh chuỗi.
    - | ``[hint="{tooltip text displayed on hover}"]{text}[/hint]``

  * - | **img**
      | Chèn một hình ảnh từ ``{path}`` (có thể là bất kỳ tài nguyên :ref:`class_Texture2D` hợp lệ nào).
      | Nếu cung cấp ``{width}``, hình ảnh sẽ cố gắng vừa với chiều rộng đó trong khi vẫn giữ nguyên tỷ lệ khung hình.
      | Nếu cung cấp cả ``{width}`` và ``{height}``, hình ảnh sẽ được thay đổi tỷ lệ theo kích thước đó.
      | Thêm ``%`` vào cuối giá trị ``{width}`` hoặc ``{height}`` để chỉ định giá trị đó theo phần trăm chiều rộng của control thay vì pixel.
      | Thêm ``em`` vào cuối giá trị ``{width}`` hoặc ``{height}`` để chỉ định giá trị đó theo tỷ lệ của kích thước phông chữ hiện tại. Ví dụ, ``height=1em`` sẽ khiến hình ảnh cao bằng văn bản xung quanh.
      | Nếu cung cấp cấu hình ``{valign}``, hình ảnh sẽ cố gắng căn chỉnh với văn bản xung quanh, xem :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment`.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_image_options`.

    - | ``[img]{path}[/img]``
      | ``[img={width}]{path}[/img]``
      | ``[img={width}x{height}]{path}[/img]``
      | ``[img={valign}]{path}[/img]``
      | ``[img {options}]{path}[/img]``

  * - | **font**
      | Khiến ``{text}`` sử dụng tài nguyên phông chữ từ ``{path}``.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_font_options`.

    - | ``[font={path}]{text}[/font]``
      | ``[font {options}]{text}[/font]``

  * - | **font_size**
      | Sử dụng cỡ font tùy chỉnh cho ``{text}``.

    - ``[font_size={size}]{text}[/font_size]``

  * - | **dropcap**
      | Sử dụng cỡ font và màu khác cho ``{text}``, đồng thời cho phép nội dung của tag trải dài trên nhiều dòng nếu đủ lớn.
      | `Drop cap <https://www.computerhope.com/jargon/d/dropcap.htm>`__ thường là một ký tự viết hoa, nhưng ``[dropcap]`` hỗ trợ chứa nhiều ký tự. Các giá trị ``margins`` được phân tách bằng dấu phẩy và có thể là số dương, số 0 hoặc số âm. Các giá trị **not** phải được phân tách bằng dấu cách; nếu không, các giá trị sẽ không được phân tích chính xác. Lề trên và lề dưới âm đặc biệt hữu ích để cho phép phần còn lại của đoạn văn hiển thị bên dưới dropcap.

    - ``[dropcap font={font} font_size={size} color={color} outline_size={size} outline_color={color} margins={left},{top},{right},{bottom}]{text}[/dropcap]``

  * - | **opentype_features**
      | Bật các tính năng font OpenType tùy chỉnh cho ``{text}``. Các tính năng phải được cung cấp dưới dạng ``{list}`` phân tách bằng dấu phẩy. Các giá trị **not** phải được phân tách bằng dấu cách; nếu không, danh sách sẽ không được phân tích chính xác.

    - | ``[opentype_features={list}]``
      | ``{text}``
      | ``[/opentype_features]``

  * - | **lang**
      | Ghi đè ngôn ngữ cho ``{text}`` được thiết lập bởi thuộc tính **BiDi > Language** trong :ref:`class_RichTextLabel`. ``{code}`` phải là :ref:`mã ngôn ngữ <doc_locales>` ISO. Có thể dùng tùy chọn này để buộc sử dụng một hệ chữ cụ thể cho một ngôn ngữ mà không cần bắt đầu đoạn văn mới. Một số file font có thể chứa các thay thế dành riêng cho hệ chữ; trong trường hợp đó, chúng sẽ được sử dụng.

    - ``[lang={code}]{text}[/lang]``

  * - | **color**
      | Thay đổi màu của ``{text}``. Màu phải được cung cấp bằng tên thông dụng (xem
        :ref:`doc_bbcode_in_richtextlabel_named_colors`) hoặc sử dụng định dạng HEX (ví dụ: ``#ff00ff``, xem :ref:`doc_bbcode_in_richtextlabel_hex_colors`).

    - ``[color={code/name}]{text}[/color]``

  * - | **bgcolor**
      | Vẽ màu phía sau ``{text}``. Có thể dùng tùy chọn này để làm nổi bật văn bản. Chấp nhận các giá trị giống tag ``color``. Theo mặc định, có một khoảng đệm nhỏ được điều khiển bởi các mục theme ``text_highlight_h_padding`` và ``text_highlight_v_padding`` trong node RichTextLabel. Đặt khoảng đệm thành ``0`` để tránh các vấn đề chồng lấn có thể xảy ra khi các dòng/cột liền kề có màu nền.

    - ``[bgcolor={code/name}]{text}[/bgcolor]``

  * - | **fgcolor**
      | Vẽ màu phía trước ``{text}``. Có thể dùng tùy chọn này để "che" văn bản bằng cách sử dụng màu tiền cảnh đục. Chấp nhận các giá trị giống tag ``color``. Theo mặc định, có một khoảng đệm nhỏ được điều khiển bởi các mục theme ``text_highlight_h_padding`` và ``text_highlight_v_padding`` trong node RichTextLabel. Đặt khoảng đệm thành ``0`` để tránh các vấn đề chồng lấn có thể xảy ra khi các dòng/cột liền kề có màu tiền cảnh.

    - ``[fgcolor={code/name}]{text}[/fgcolor]``

  * - | **outline_size**
      | Sử dụng kích thước viền font tùy chỉnh cho ``{text}``.

    - | ``[outline_size={size}]``
      | ``{text}``
      | ``[/outline_size]``

  * - | **outline_color**
      | Sử dụng màu viền tùy chỉnh cho ``{text}``. Chấp nhận các giá trị giống tag ``color``.

    - | ``[outline_color={code/name}]``
      | ``{text}``
      | ``[/outline_color]``

  * - | **table**
      | Tạo một bảng với ``{number}`` cột. Sử dụng tag ``cell`` để định nghĩa các ô trong bảng.
      | Nếu cung cấp cấu hình ``{valign}``, bảng sẽ cố gắng căn chỉnh theo văn bản xung quanh, xem :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment`.
      | Nếu sử dụng căn chỉnh theo đường cơ sở, bảng sẽ được căn chỉnh theo đường cơ sở của hàng có chỉ mục ``{alignment_row}`` (bắt đầu từ 0).
      | ``{name}`` là tên bảng dành cho các ứng dụng hỗ trợ (trình đọc màn hình).

    - | ``[table={number}]{cells}[/table]``
      | ``[table={number},{valign}]{cells}[/table]``
      | ``[table={number},{valign},{alignment_row}]{cells}[/table]``
      | ``[table={number},{valign},{alignment_row} name={name}]{cells}[/table]``

  * - | **cell**
      | Thêm một ô có ``{text}`` vào bảng.
      | Nếu cung cấp ``{ratio}``, ô sẽ cố gắng mở rộng đến giá trị đó theo tỷ lệ với các ô khác và các giá trị tỷ lệ của chúng.
      | Hỗ trợ các tùy chọn cấu hình, xem :ref:`doc_bbcode_in_richtextlabel_cell_options`.

    - | ``[cell]{text}[/cell]``
      | ``[cell={ratio}]{text}[/cell]``
      | ``[cell {options}]{text}[/cell]``

  * - | **ul**
      | Thêm danh sách không có thứ tự. ``{items}`` của danh sách phải được cung cấp bằng cách đặt mỗi mục trên một dòng văn bản.
      | Có thể tùy chỉnh dấu đầu dòng bằng tham số ``{bullet}``, xem :ref:`doc_bbcode_in_richtextlabel_unordered_list_bullet`.

    - | ``[ul]{items}[/ul]``
      | ``[ul bullet={bullet}]{items}[/ul]``

  * - | **ol**
      | Thêm danh sách có thứ tự (đánh số) gồm ``{type}`` được cung cấp (xem :ref:`doc_bbcode_in_richtextlabel_list_types`). ``{items}`` của danh sách phải được cung cấp bằng cách đặt mỗi mục trên một dòng văn bản.

    - ``[ol type={type}]{items}[/ol]``

  * - | **lb**, **rb**
      | Thêm lần lượt ``[`` và ``]``. Cho phép escape markup BBCode.
      | Đây là các tag tự đóng, nghĩa là bạn không cần đóng chúng (và không có tag đóng ``[/lb]`` hoặc ``[/rb]``).

    - | ``[lb]b[rb]text[lb]/b[rb]`` sẽ hiển thị dưới dạng ``[b]text[/b]``.

  * - | Có thể thêm một số ký tự điều khiển Unicode bằng các tag tự đóng riêng của chúng.
      | Điều này có thể giúp việc bảo trì dễ dàng hơn so với việc dán trực tiếp các
      | ký tự điều khiển đó vào văn bản.

    - | ``[lrm]`` (dấu đánh dấu trái sang phải), ``[rlm]`` (dấu đánh dấu phải sang trái), ``[lre]`` (nhúng trái sang phải),
      | ``[rle]`` (nhúng phải sang trái), ``[lro]`` (ghi đè trái sang phải), ``[rlo]`` (ghi đè phải sang trái),
      | ``[pdf]`` (kết thúc định dạng hướng), ``[alm]`` (dấu chữ Ả Rập), ``[lri]`` (cô lập trái sang phải),
      | ``[rli]`` (cô lập phải sang trái), ``[fsi]`` (cô lập mạnh đầu tiên), ``[pdi]`` (kết thúc cô lập hướng),
      | ``[zwj]`` (bộ nối không độ rộng), ``[zwnj]`` (bộ không nối không độ rộng), ``[wj]`` (bộ nối từ),
      | ``[shy]`` (dấu gạch nối mềm)

.. note::

    Các tag định dạng chữ đậm (``[b]``) và chữ nghiêng (``[i]``) hoạt động tốt nhất nếu các font tùy chỉnh tương ứng được thiết lập trong phần ghi đè theme của RichTextLabelNode. Nếu không định nghĩa font chữ đậm hoặc chữ nghiêng tùy chỉnh, Godot sẽ tạo `font đậm và nghiêng giả <https://fonts.google.com/knowledge/glossary/faux_fake_pseudo_synthesized>`__. Những font này hiếm khi có giao diện đẹp bằng các biến thể font đậm/nghiêng được tạo thủ công.

    Tag monospace (``[code]``) **chỉ** hoạt động nếu một font tùy chỉnh được thiết lập trong phần ghi đè theme của node RichTextLabel. Nếu không, văn bản monospace sẽ sử dụng font thông thường.

    Hiện chưa có tag BBCode nào để điều khiển việc căn giữa theo chiều dọc của văn bản.

    Có thể bỏ qua các tùy chọn đối với tất cả tag.

.. _doc_bbcode_in_richtextlabel_paragraph_options:

Tùy chọn đoạn văn
~~~~~~~~~~~~~~~~~

- **align**

  +-----------+-----------------------------------------------------------------------------------------------+
  | `Values`  | ``left`` (hoặc ``l``), ``center`` (hoặc ``c``), ``right`` (hoặc ``r``), ``fill`` (hoặc ``f``) |
  +-----------+-----------------------------------------------------------------------------------------------+
  | `Default` | ``left``                                                                                      |
  +-----------+-----------------------------------------------------------------------------------------------+

  Căn chỉnh ngang văn bản.

- **bidi_override**, **st**

  +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  | `Values`  | ``default`` (của ``d``), ``uri`` (hoặc ``u``), ``file`` (hoặc ``f``), ``email`` (hoặc ``e``), ``list`` (hoặc ``l``), ``none`` (hoặc ``n``), ``custom`` (hoặc ``c``) |
  +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  | `Default` | ``default``                                                                                                                                                         |
  +-----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

  Ghi đè văn bản có cấu trúc.

- **justification_flags**, **jst**

  +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  | `Values`  | Danh sách các giá trị sau, được phân tách bằng dấu phẩy (không có khoảng trắng sau mỗi dấu phẩy): ``kashida`` (hoặc ``k``), ``word`` (hoặc ``w``), ``trim`` (hoặc ``tr``), ``after_last_tab`` (hoặc ``lt``), ``skip_last`` (hoặc ``sl``), ``skip_last_with_chars`` (hoặc ``sv``),  ``do_not_skip_single`` (hoặc ``ns``). |
  +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  | `Default` | ``word,kashida,skip_last,do_not_skip_single``                                                                                                                                                                                                                                                                            |
  +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

  Tùy chọn justification (căn chỉnh kiểu fill). Xem :ref:`class_TextServer` để biết thêm chi tiết.

- **direction**, **dir**

  +-----------+-------------------------------------------------------------------+
  | `Values`  | ``ltr`` (hoặc ``l``), ``rtl`` (hoặc ``r``), ``auto`` (hoặc ``a``) |
  +-----------+-------------------------------------------------------------------+
  | `Default` | Kế thừa                                                           |
  +-----------+-------------------------------------------------------------------+

  Hướng BiDi cơ sở.

- **language**, **lang**

  +-----------+-----------------------------------------+
  | `Values`  | Mã ngôn ngữ ISO. Xem :ref:`doc_locales` |
  +-----------+-----------------------------------------+
  | `Default` | Kế thừa                                 |
  +-----------+-----------------------------------------+

  Ghi đè locale. Một số tệp font có thể chứa các dạng thay thế dành riêng cho từng hệ chữ; trong trường hợp đó, các dạng thay thế này sẽ được sử dụng.

- **tab_stops**

  +-----------+---------------------------------------------+
  | `Values`  | Danh sách các số thực, ví dụ: ``10.0,30.0`` |
  +-----------+---------------------------------------------+
  | `Default` | Độ rộng của ký tự khoảng trắng trong font   |
  +-----------+---------------------------------------------+

  Ghi đè các offset ngang cho từng ký tự tab. Khi đến cuối danh sách, các điểm dừng tab sẽ lặp lại. Ví dụ: nếu đặt ``tab_stops`` thành ``10.0,30.0``, tab đầu tiên sẽ ở ``10`` pixel, tab thứ hai ở ``10 + 30 = 40`` pixel và tab thứ ba ở ``10 + 30 + 10 = 50`` pixel tính từ gốc của RichTextLabel.

.. _doc_bbcode_in_richtextlabel_handling_url_tag_clicks:

Xử lý thao tác nhấp vào thẻ ``[url]``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, các thẻ ``[url]`` không làm gì khi được nhấp. Điều này cho phép sử dụng linh hoạt các thẻ ``[url]`` thay vì giới hạn chúng chỉ dùng để mở URL trong trình duyệt web.

Để xử lý các thẻ ``[url]`` được nhấp, hãy kết nối phần của node ``RichTextLabel``
tín hiệu :ref:`meta_clicked <class_RichTextLabel_signal_meta_clicked>` với một hàm script.

Ví dụ: có thể kết nối phương thức sau với ``meta_clicked`` để mở các URL được nhấp bằng trình duyệt web mặc định của người dùng:

.. code-block::

    # Điều này giả định rằng tín hiệu `meta_clicked` của RichTextLabel đã được kết nối với
    # hàm bên dưới bằng hộp thoại kết nối tín hiệu.
    func _richtextlabel_on_meta_clicked(meta):
        # `meta` không được đảm bảo là một String, vì vậy hãy chuyển nó thành String
        # để tránh lỗi script khi runtime.
        OS.shell_open(str(meta))

Đối với các trường hợp sử dụng nâng cao hơn, bạn cũng có thể lưu JSON trong tùy chọn của thẻ ``[url]`` và phân tích cú pháp trong hàm xử lý tín hiệu ``meta_clicked``. Ví dụ:

.. code-block:: none

  [url={"example": "value"}]JSON[/url]


.. _doc_bbcode_in_richtextlabel_hr_options:

Tùy chọn đường kẻ ngang
~~~~~~~~~~~~~~~~~~~~~~~

- **color**

  +-----------+----------------------------------+
  | `Values`  | Tên màu hoặc màu ở định dạng HEX |
  +-----------+----------------------------------+
  | `Default` | ``Color(1, 1, 1, 1)``            |
  +-----------+----------------------------------+

  Màu sắc của đường kẻ (điều biến).

- **height**

  +-----------+-----------+
  | `Values`  | Số nguyên |
  +-----------+-----------+
  | `Default` | ``2``     |
  +-----------+-----------+

  Chiều cao mục tiêu của đường kẻ tính bằng pixel; thêm ``%`` vào cuối giá trị để chỉ định theo phần trăm chiều rộng của control thay vì pixel.

- **width**

  +-----------+-----------+
  | `Values`  | Số nguyên |
  +-----------+-----------+
  | `Default` | ``90%``   |
  +-----------+-----------+

  Chiều rộng mục tiêu của đường kẻ tính bằng pixel; thêm ``%`` vào cuối giá trị để chỉ định theo phần trăm chiều rộng của control thay vì pixel.

- **align**

  +-----------+------------------------------------------------------------------------+
  | `Values`  | ``left`` (hoặc ``l``), ``center`` (hoặc ``c``), ``right`` (hoặc ``r``) |
  +-----------+------------------------------------------------------------------------+
  | `Default` | ``center``                                                             |
  +-----------+------------------------------------------------------------------------+

  Căn chỉnh ngang.


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

  +-----------+--------+
  | `Values`  | Chuỗi. |
  +-----------+--------+
  | `Default` |        |
  +-----------+--------+

  Tooltip của URL.

- **href**

  +-----------+--------+
  | `Values`  | Chuỗi. |
  +-----------+--------+
  | `Default` |        |
  +-----------+--------+

  Địa chỉ đích của URL.


.. _doc_bbcode_in_richtextlabel_image_options:

Tùy chọn hình ảnh
~~~~~~~~~~~~~~~~~

- **color**

  +-----------+----------------------------------+
  | `Values`  | Tên màu hoặc màu ở định dạng HEX |
  +-----------+----------------------------------+
  | `Default` | Kế thừa                          |
  +-----------+----------------------------------+

  Màu phủ của hình ảnh (điều biến).

- **height**

  +-----------+------------------+
  | `Values`  | Số dấu phẩy động |
  +-----------+------------------+
  | `Default` | Kế thừa          |
  +-----------+------------------+

  Chiều cao mục tiêu của hình ảnh tính bằng pixel.

  Có thể chỉ định các đơn vị khác pixel:

  - Thêm ``%`` vào cuối giá trị để chỉ định giá trị dưới dạng phần trăm chiều rộng của control thay vì pixel. Ví dụ, ``height=50%`` sẽ làm cho hình ảnh cao bằng một nửa chiều rộng của control.

  - Thêm ``em`` vào cuối giá trị để chỉ định giá trị theo tỷ lệ so với cỡ chữ xung quanh thay vì pixel. Ví dụ, ``height=1em`` sẽ làm cho hình ảnh cao bằng phần văn bản xung quanh.

- **width**

  +-----------+------------------+
  | `Values`  | Số dấu phẩy động |
  +-----------+------------------+
  | `Default` | Kế thừa          |
  +-----------+------------------+

  Chiều rộng mục tiêu của hình ảnh tính bằng pixel.

  Có thể chỉ định các đơn vị khác pixel:

  - Thêm ``%`` vào cuối giá trị để chỉ định giá trị dưới dạng phần trăm chiều rộng của control thay vì pixel. Ví dụ, ``width=50%`` sẽ làm cho hình ảnh chiếm một nửa chiều rộng của control.

  - Thêm ``em`` vào cuối giá trị để chỉ định giá trị theo tỷ lệ so với cỡ chữ xung quanh thay vì pixel. Ví dụ, ``width=1em`` sẽ làm cho hình ảnh rộng bằng chiều cao của phần văn bản xung quanh.

- **region**

  +-----------+----------------------------------+
  | `Values`  | x,y,width,height tính bằng pixel |
  +-----------+----------------------------------+
  | `Default` | Kế thừa                          |
  +-----------+----------------------------------+

  Hình chữ nhật vùng của hình ảnh. Có thể dùng tùy chọn này để hiển thị một hình ảnh đơn từ spritesheet.

- **pad**

  +-----------+--------------------------------------------+
  | `Values`  | ``false``, ``true``                        |
  +-----------+--------------------------------------------+
  | `Default` | ``false``                                  |
  +-----------+--------------------------------------------+

  Nếu được đặt thành ``true`` và hình ảnh nhỏ hơn kích thước được chỉ định bởi ``width`` và ``height``, phần đệm của hình ảnh sẽ được thêm vào để khớp với kích thước thay vì phóng to hình ảnh.

- **tooltip**

  +-----------+-------+
  | `Values`  | Chuỗi |
  +-----------+-------+
  | `Default` |       |
  +-----------+-------+

  Tooltip của hình ảnh.

- **align**

  +-----------+------------------------------------------------------------------+
  | `Values`  | xem :ref:`doc_bbcode_in_richtextlabel_image_and_table_alignment` |
  +-----------+------------------------------------------------------------------+
  | `Default` | ``center,center``                                                |
  +-----------+------------------------------------------------------------------+

  Căn chỉnh hình ảnh với phần văn bản xung quanh.

- **alt**

  +-----------+-------+
  | `Values`  | Chuỗi |
  +-----------+-------+
  | `Default` |       |
  +-----------+-------+

  Mô tả hình ảnh dành cho các ứng dụng hỗ trợ (trình đọc màn hình).

.. _doc_bbcode_in_richtextlabel_image_and_table_alignment:

Căn chỉnh dọc hình ảnh và bảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi cung cấp một giá trị căn chỉnh dọc cùng với thẻ ``[img]`` hoặc ``[table]``, hình ảnh/bảng sẽ cố gắng tự căn chỉnh với phần văn bản xung quanh. Việc căn chỉnh được thực hiện bằng cách sử dụng một điểm dọc trên hình ảnh và một điểm dọc trên văn bản. Có 3 điểm khả dụng trên hình ảnh (``top``, ``center`` và ``bottom``) và 4 điểm khả dụng trên văn bản và bảng (``top``, ``center``, ``baseline`` và ``bottom``), có thể kết hợp theo bất kỳ cách nào.

Để chỉ định cả hai điểm, hãy sử dụng tên đầy đủ hoặc tên viết tắt của chúng làm giá trị của thẻ hình ảnh/bảng:

.. code-block:: none

    text [img=top,bottom]...[/img] text
    text [img=center,center]...[/img] text

.. image:: img/bbcode_in_richtextlabel_image_align.webp

.. code-block:: none

    text [table=3,center]...[/table] text  # Center to center.
    text [table=3,top,bottom]...[/table] text # Top of the table to the bottom of text.
    text [table=3,baseline,baseline,1]...[/table] text # Baseline of the second row (rows use zero-based indexing) to the baseline of text.

.. image:: img/bbcode_in_richtextlabel_table_align.webp

Bạn cũng có thể chỉ định chỉ một giá trị (``top``, ``center`` hoặc ``bottom``) để sử dụng preset tương ứng (``top-top``, ``center-center`` và ``bottom-bottom``).

Tên viết tắt của các giá trị là ``t`` (``top``), ``c`` (``center``), ``l`` (``baseline``) và ``b`` (``bottom``).


.. _doc_bbcode_in_richtextlabel_font_options:

Tùy chọn font
~~~~~~~~~~~~~

- **name**, **n**

  +-----------+---------------------------------------+
  | `Values`  | Một đường dẫn tài nguyên Font hợp lệ. |
  +-----------+---------------------------------------+
  | `Default` | Kế thừa                               |
  +-----------+---------------------------------------+

  Đường dẫn tài nguyên Font.

- **size**, **s**

  +-----------+---------------------+
  | `Values`  | Số tính bằng pixel. |
  +-----------+---------------------+
  | `Default` | Kế thừa             |
  +-----------+---------------------+

  Cỡ font tùy chỉnh.

- **glyph_spacing**, **gl**

  +-----------+---------------------+
  | `Values`  | Số tính bằng pixel. |
  +-----------+---------------------+
  | `Default` | Kế thừa             |
  +-----------+---------------------+

  Khoảng cách bổ sung cho mỗi glyph.

- **space_spacing**, **sp**

  +-----------+---------------------+
  | `Values`  | Số tính bằng pixel. |
  +-----------+---------------------+
  | `Default` | Kế thừa             |
  +-----------+---------------------+

  Khoảng cách bổ sung cho ký tự khoảng trắng.

- **top_spacing**, **top**

  +-----------+---------------------+
  | `Values`  | Số tính bằng pixel. |
  +-----------+---------------------+
  | `Default` | Kế thừa             |
  +-----------+---------------------+

  Khoảng cách bổ sung ở đầu dòng.

- **bottom_spacing**, **bt**

  +-----------+---------------------+
  | `Values`  | Số tính bằng pixel. |
  +-----------+---------------------+
  | `Default` | Kế thừa             |
  +-----------+---------------------+

  Khoảng cách bổ sung ở cuối dòng.

- **embolden**, **emb**

  +-----------+------------------------+
  | `Values`  | Số thực dấu phẩy động. |
  +-----------+------------------------+
  | `Default` | ``0.0``                |
  +-----------+------------------------+

  Độ mạnh embolden của phông chữ; nếu khác không, giá trị này sẽ làm đậm các đường viền của phông chữ. Giá trị âm làm giảm độ dày của đường viền.

- **face_index**, **fi**

  +-----------+------------+
  | `Values`  | Số nguyên. |
  +-----------+------------+
  | `Default` | ``0``      |
  +-----------+------------+

  Chỉ số face đang hoạt động trong bộ sưu tập TrueType / OpenType.

- **slant**, **sln**

  +-----------+------------------------+
  | `Values`  | Số thực dấu phẩy động. |
  +-----------+------------------------+
  | `Default` | ``0.0``                |
  +-----------+------------------------+

  Độ mạnh slant của phông chữ; giá trị dương làm nghiêng glyph sang phải, còn giá trị âm làm nghiêng sang trái.

- **opentype_variation**, **otv**

  +-----------+------------------------------------------------------------------------------------------------------------+
  | `Values`  | Danh sách các tag biến thể OpenType được phân tách bằng dấu phẩy (không có khoảng trắng sau mỗi dấu phẩy). |
  +-----------+------------------------------------------------------------------------------------------------------------+
  | `Default` |                                                                                                            |
  +-----------+------------------------------------------------------------------------------------------------------------+

  Tọa độ biến thể OpenType của phông chữ. Xem `OpenType variation tags <https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg>`__.

  Lưu ý: Giá trị này phải được đặt trong ``"`` để cho phép sử dụng ``=`` bên trong:

.. code-block:: none

    [font otv="wght=200,wdth=400"] # Sets variable font weight and width.

- **opentype_features**, **otf**

  +-----------+-------------------------------------------------------------------------------------------------------------+
  | `Values`  | Danh sách các tag tính năng OpenType được phân tách bằng dấu phẩy (không có khoảng trắng sau mỗi dấu phẩy). |
  +-----------+-------------------------------------------------------------------------------------------------------------+
  | `Default` |                                                                                                             |
  +-----------+-------------------------------------------------------------------------------------------------------------+

  Các tính năng OpenType của phông chữ. Xem `OpenType features tags <https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>`__.

  Lưu ý: Giá trị này phải được đặt trong ``"`` để cho phép sử dụng ``=`` bên trong:

.. code-block:: none

    [font otf="calt=0,zero=1"] # Disable contextual alternates, enable slashed zero.

.. _doc_bbcode_in_richtextlabel_named_colors:

Màu được đặt tên
~~~~~~~~~~~~~~~~

Đối với các tag cho phép chỉ định màu bằng tên, bạn có thể sử dụng tên của các hằng số từ lớp :ref:`class_Color` tích hợp sẵn. Có thể chỉ định màu được đặt tên theo nhiều kiểu viết hoa khác nhau: ``DARK_RED``, ``DarkRed`` và ``darkred`` sẽ cho cùng một kết quả chính xác.

Xem hình ảnh này để biết danh sách các hằng số màu:

.. image:: /img/color_constants.png

`Xem kích thước đầy đủ <https://raw.githubusercontent.com/godotengine/godot-docs/master/img/color_constants.png>`__

.. _doc_bbcode_in_richtextlabel_hex_colors:

Mã màu hệ thập lục phân
~~~~~~~~~~~~~~~~~~~~~~~

Đối với màu RGB không trong suốt, mọi mã hệ thập lục phân 6 chữ số hợp lệ đều được hỗ trợ, ví dụ: ``[color=#ffffff]white[/color]``. Các mã màu RGB viết tắt như ``#6f2`` (tương đương với ``#66ff22``) cũng được hỗ trợ.

Đối với màu RGB trong suốt, có thể sử dụng mọi mã hệ thập lục phân RGBA 8 chữ số, ví dụ: ``[color=#ffffff88]translucent white[/color]``. Lưu ý rằng kênh alpha là thành phần **last** của mã màu, không phải thành phần đầu tiên. Các mã màu RGBA ngắn như ``#6f28`` (tương đương với ``#66ff2288``) cũng được hỗ trợ.

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

  +-----------+-----------+
  | `Values`  | Số nguyên |
  +-----------+-----------+
  | `Default` | 1         |
  +-----------+-----------+

  Tỷ lệ mở rộng của ô. Tùy chọn này xác định những ô nào sẽ cố gắng mở rộng theo tỷ lệ với các ô khác và tỷ lệ mở rộng của chúng.

- **border**

  +-----------+----------------------------------+
  | `Values`  | Tên màu hoặc màu ở định dạng HEX |
  +-----------+----------------------------------+
  | `Default` | Kế thừa                          |
  +-----------+----------------------------------+

  Màu viền của ô.

- **bg**

  +-----------+----------------------------------+
  | `Values`  | Tên màu hoặc màu ở định dạng HEX |
  +-----------+----------------------------------+
  | `Default` | Kế thừa                          |
  +-----------+----------------------------------+

  Màu nền của ô. Để tạo nền xen kẽ cho các hàng lẻ/chẵn, bạn có thể sử dụng ``bg=odd_color,even_color``.

- **padding**

  +-----------+-----------------------------------------------------------------------------------------------+
  | `Values`  | 4 số thực dấu phẩy động được phân tách bằng dấu phẩy (không có khoảng trắng sau mỗi dấu phẩy) |
  +-----------+-----------------------------------------------------------------------------------------------+
  | `Default` | ``0,0,0,0``                                                                                   |
  +-----------+-----------------------------------------------------------------------------------------------+

  Khoảng đệm bên trái, bên trên, bên phải và bên dưới của ô.

.. _doc_bbcode_in_richtextlabel_unordered_list_bullet:

Dấu đầu dòng của danh sách không có thứ tự
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, tag ``[ul]`` sử dụng glyph Unicode ``U+2022`` "Bullet" làm ký tự đầu dòng. Cách hoạt động này tương tự như trong các trình duyệt web. Có thể tùy chỉnh ký tự đầu dòng bằng ``[ul bullet={bullet}]``. Nếu được cung cấp, tham số ``{bullet}`` này phải là một chuỗi không có dấu ngoặc kép bao quanh (ví dụ: ``[bullet=*]``). Bạn có thể thêm khoảng trắng ở cuối sau ký tự đầu dòng để tăng khoảng cách giữa ký tự đầu dòng và văn bản của mục danh sách.

Xem `Bullet (typography) on Wikipedia <https://en.wikipedia.org/wiki/Bullet_(typography)>`__ để biết danh sách các ký tự đầu dòng phổ biến mà bạn có thể dán trực tiếp vào tham số ``bullet``.

.. _doc_bbcode_in_richtextlabel_list_types:

Các kiểu danh sách có thứ tự
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Danh sách có thứ tự có thể được sử dụng để tự động đánh dấu các mục bằng số hoặc chữ cái theo thứ tự tăng dần. Tag này hỗ trợ các tùy chọn kiểu sau:

- ``1`` - Số, sử dụng hệ thống đánh số theo ngôn ngữ nếu có thể.
- ``a``, ``A`` - Chữ cái Latin thường và hoa.
- ``i``, ``I`` - Chữ số La Mã thường và hoa.

Hiệu ứng văn bản
----------------

BBCode cũng có thể được sử dụng để tạo các hiệu ứng văn bản khác nhau, tùy chọn có thể được animated. Một số hiệu ứng có thể tùy chỉnh được cung cấp sẵn, và bạn có thể dễ dàng tạo hiệu ứng của riêng mình. Theo mặc định, các hiệu ứng animated sẽ tạm dừng
:ref:`khi SceneTree bị tạm dừng <doc_pausing_games>`. Bạn có thể thay đổi hành vi này bằng cách điều chỉnh thuộc tính **Process > Mode** của RichTextLabel.

Tất cả các ví dụ bên dưới đều đề cập đến các giá trị mặc định của những tùy chọn trong định dạng thẻ được liệt kê.

.. note::

    Các hiệu ứng văn bản làm thay đổi vị trí của ký tự có thể khiến ký tự bị cắt bởi ranh giới của node RichTextLabel.

    Bạn có thể khắc phục vấn đề này bằng cách tắt **Control > Layout > Clip Contents** trong inspector sau khi chọn node RichTextLabel, hoặc đảm bảo có đủ khoảng đệm xung quanh văn bản bằng cách sử dụng ngắt dòng ở phía trên và phía dưới dòng sử dụng hiệu ứng.

Pulse
~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_pulse.webp

Pulse tạo hiệu ứng nhấp nháy động, nhân độ mờ và màu của từng ký tự. Hiệu ứng này có thể được dùng để thu hút sự chú ý đến văn bản cụ thể. Định dạng thẻ của nó là ``[pulse freq=1.0 color=#ffffff40 ease=-2.0]{text}[/pulse]``.

``freq`` điều khiển tần số của nửa chu kỳ nhấp nháy (giá trị càng cao thì càng nhanh). Một chu kỳ nhấp nháy đầy đủ mất ``2 * (1.0 / freq)`` giây. ``color`` là hệ số màu đích dùng cho việc nhấp nháy. Theo mặc định, văn bản gần như mờ đi hoàn toàn nhưng không biến mất hẳn. ``ease`` là số mũ của hàm easing được sử dụng. Các giá trị âm tạo ra easing in-out, đó là lý do giá trị mặc định là ``-2.0``.

Wave
~~~~

.. image:: img/bbcode_in_richtextlabel_effect_wave.webp

Wave làm cho văn bản chuyển động lên xuống. Định dạng thẻ của nó là ``[wave amp=50.0 freq=5.0 connected=1]{text}[/wave]``.

``amp`` điều khiển mức độ cao và thấp của hiệu ứng, còn ``freq`` điều khiển tốc độ văn bản di chuyển lên xuống. Giá trị ``freq`` bằng ``0`` sẽ không tạo ra sóng nào có thể nhìn thấy, và các giá trị ``freq`` âm cũng không hiển thị sóng. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph được di chuyển riêng lẻ, ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề kết xuất với ligature của font.

Tornado
~~~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_tornado.webp

Tornado làm cho văn bản chuyển động theo một vòng tròn. Định dạng thẻ của nó là ``[tornado radius=10.0 freq=1.0 connected=1]{text}[/tornado]``.

``radius`` là bán kính của vòng tròn điều khiển độ lệch, còn ``freq`` là tốc độ văn bản chuyển động theo vòng tròn. Giá trị ``freq`` bằng ``0`` sẽ tạm dừng hoạt ảnh, trong khi ``freq`` âm sẽ phát hoạt ảnh ngược. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph được di chuyển riêng lẻ, ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề kết xuất với ligature của font.

Shake
~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_shake.webp

Shake làm cho văn bản rung lắc. Định dạng thẻ của nó là ``[shake rate=20.0 level=5 connected=1]{text}[/shake]``.

``rate`` điều khiển tốc độ rung của văn bản, còn ``level`` điều khiển khoảng cách văn bản bị lệch so với gốc. Nếu ``connected`` là ``1`` (mặc định), các glyph có ligature sẽ được di chuyển cùng nhau. Nếu ``connected`` là ``0``, mỗi glyph được di chuyển riêng lẻ, ngay cả khi chúng được nối với nhau bằng ligature. Điều này có thể khắc phục một số vấn đề kết xuất với ligature của font.

Fade
~~~~

.. image:: img/bbcode_in_richtextlabel_effect_fade.webp

Fade tạo hiệu ứng mờ tĩnh, nhân độ mờ của từng ký tự. Định dạng thẻ của nó là ``[fade start=4 length=14]{text}[/fade]``.

``start`` điều khiển vị trí bắt đầu của độ suy giảm so với nơi chèn lệnh fade, còn ``length`` điều khiển hiệu ứng mờ dần diễn ra trong bao nhiêu ký tự.

Rainbow
~~~~~~~

.. image:: img/bbcode_in_richtextlabel_effect_rainbow.webp

Rainbow tạo cho văn bản màu cầu vồng thay đổi theo thời gian. Định dạng thẻ của nó là ``[rainbow freq=1.0 sat=0.8 val=0.8 speed=1.0]{text}[/rainbow]``.

``freq`` xác định cầu vồng trải rộng trên bao nhiêu chữ cái trước khi lặp lại, ``sat`` là độ bão hòa của cầu vồng, còn ``val`` là giá trị của cầu vồng. ``speed`` là số chu kỳ cầu vồng đầy đủ mỗi giây. Giá trị ``speed`` dương sẽ phát hoạt ảnh theo chiều thuận, giá trị ``0`` sẽ tạm dừng hoạt ảnh, còn giá trị ``speed`` âm sẽ phát hoạt ảnh ngược.

Đường viền font *không* bị ảnh hưởng bởi hiệu ứng cầu vồng (chúng giữ nguyên màu ban đầu). Các màu font hiện có sẽ bị hiệu ứng cầu vồng ghi đè. Tuy nhiên, các thuộc tính **Modulate** và **Self Modulate** của CanvasItem sẽ ảnh hưởng đến hình thức của hiệu ứng cầu vồng, vì modulation nhân với các màu cuối cùng của hiệu ứng.

Thẻ BBCode tùy chỉnh và hiệu ứng văn bản
----------------------------------------

Bạn có thể mở rộng kiểu tài nguyên :ref:`class_RichTextEffect` để tạo các thẻ BBCode tùy chỉnh của riêng mình. Tạo một tệp script mới mở rộng kiểu tài nguyên :ref:`class_RichTextEffect` và gán cho script một ``class_name`` để hiệu ứng có thể được chọn trong inspector. Thêm annotation ``@tool`` vào tệp GDScript nếu bạn muốn các hiệu ứng tùy chỉnh này chạy ngay trong editor. RichTextLabel không cần được gắn script, cũng không cần chạy ở chế độ ``tool``. Hiệu ứng mới có thể được đăng ký trong Inspector bằng cách thêm nó vào mảng **Markup > Custom Effects**, hoặc trong code bằng phương thức
:ref:`install_effect() <class_RichTextLabel_method_install_effect>`:​

.. figure:: img/bbcode_in_richtextlabel_selecting_custom_richtexteffect.webp
   :align: center
   :alt: Chọn RichTextEffect tùy chỉnh sau khi lưu một script mở rộng RichTextEffect với một ``class_name``

   Chọn RichTextEffect tùy chỉnh sau khi lưu một script mở rộng RichTextEffect với một ``class_name``

.. warning::

    Nếu hiệu ứng tùy chỉnh không được đăng ký trong thuộc tính **Markup > Custom Effects** của RichTextLabel, sẽ không có hiệu ứng nào hiển thị và thẻ ban đầu sẽ được giữ nguyên.

Chỉ có một hàm mà bạn cần mở rộng: ``_process_custom_fx(char_fx)``. Ngoài ra, bạn cũng có thể cung cấp một mã định danh BBCode tùy chỉnh bằng cách thêm tên thành viên ``bbcode``. Code sẽ tự động kiểm tra thuộc tính ``bbcode`` hoặc sử dụng tên tệp để xác định thẻ BBCode cần dùng.

``_process_custom_fx``
~~~~~~~~~~~~~~~~~~~~~~

Đây là nơi diễn ra logic của từng hiệu ứng; hàm được gọi một lần cho mỗi glyph trong giai đoạn vẽ của quá trình kết xuất văn bản. Hàm này truyền vào một đối tượng :ref:`class_CharFXTransform`, chứa một số biến để điều khiển cách glyph tương ứng được kết xuất:

- ``outline`` là ``true`` nếu hiệu ứng được gọi để vẽ đường viền văn bản.
- ``range`` cho biết bạn đang ở vị trí nào trong một khối hiệu ứng tùy chỉnh nhất định, dưới dạng một chỉ mục.
- ``elapsed_time`` là tổng thời gian hiệu ứng văn bản đã chạy.
- ``visible`` cho biết glyph có hiển thị hay không, đồng thời cho phép bạn ẩn một phần văn bản nhất định.
- ``offset`` là vị trí offset tương đối so với vị trí glyph tương ứng sẽ được kết xuất trong điều kiện bình thường.
- ``color`` là màu của một glyph nhất định.
- ``glyph_index`` và ``font`` lần lượt là glyph đang được vẽ và tài nguyên dữ liệu font được sử dụng để vẽ glyph đó.
- Cuối cùng, ``env`` là một :ref:`class_Dictionary` gồm các tham số được gán cho một hiệu ứng tùy chỉnh nhất định. Bạn có thể sử dụng :ref:`get() <class_Dictionary_method_get>` với một giá trị mặc định tùy chọn để lấy từng tham số, nếu người dùng đã chỉ định tham số đó. Ví dụ, ``[custom_fx spread=0.5 color=#FFFF00]test[/custom_fx]`` sẽ có các tham số float ``spread`` và Color ``color`` trong Dictionary ``env`` của nó. Xem bên dưới để biết thêm các ví dụ sử dụng.

Điều cuối cùng cần lưu ý về hàm này là cần trả về một giá trị boolean ``true`` để xác minh rằng effect đã được xử lý chính xác. Bằng cách này, nếu có vấn đề khi render một glyph cụ thể, hàm sẽ ngừng hoàn toàn việc render các effect tùy chỉnh cho đến khi người dùng sửa lỗi phát sinh trong logic effect tùy chỉnh của họ.

Dưới đây là một số ví dụ về effect tùy chỉnh:

Ghost
~~~~~

.. code-block::

    @tool
    extends RichTextEffect
    class_name RichTextGhost

    # Cú pháp: [ghost freq=5.0 span=10.0][/ghost]

    # Define the tag name.
    var bbcode = "ghost"

    func _process_custom_fx(char_fx):
        # Lấy các tham số hoặc sử dụng giá trị mặc định được cung cấp nếu thiếu.
        var speed = char_fx.env.get("freq", 5.0)
        var span = char_fx.env.get("span", 10.0)

        var alpha = sin(char_fx.elapsed_time * speed + (char_fx.range.x / span)) * 0.5 + 0.5
        char_fx.color.a = alpha
        return true

Matrix
~~~~~~

.. code-block::

    @tool
    extends RichTextEffect
    class_name RichTextMatrix

    # Cú pháp: [matrix clean=2.0 dirty=1.0 span=50][/matrix]

    # Define the tag name.
    var bbcode = "matrix"

    # Lấy TextServer để truy xuất thông tin phông chữ.
    func get_text_server():
        return TextServerManager.get_primary_interface()

    func _process_custom_fx(char_fx):
        # Lấy các tham số hoặc sử dụng giá trị mặc định được cung cấp nếu thiếu.
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

Thao tác này sẽ thêm một vài lệnh BBCode mới, có thể được sử dụng như sau:

.. code-block:: none

    [center][ghost]This is a custom [matrix]effect[/matrix][/ghost] made in
    [pulse freq=5.0 height=2.0][pulse color=#00FFAA freq=2.0]GDScript[/pulse][/pulse].[/center]
