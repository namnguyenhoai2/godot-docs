.. _doc_gui_using_fonts:

Sử dụng font
============

Godot cho phép bạn thiết lập các font cụ thể cho những node UI khác nhau.

Có ba vị trí khác nhau để bạn thiết lập việc sử dụng font. Vị trí đầu tiên là trình chỉnh sửa theme. Chọn node mà bạn muốn thiết lập font, sau đó chọn tab font. Vị trí thứ hai là trong inspector của các control node, tại **Theme Overrides > Fonts**. Cuối cùng là trong phần cài đặt inspector của các theme, tại **Default Font**.

Nếu không có font override nào được chỉ định ở bất kỳ đâu, `Open Sans <https://fonts.google.com/specimen/Open+Sans>`__ SemiBold sẽ được sử dụng làm font mặc định của project.

.. note::

    Kể từ Godot 4.0, kích thước font không còn được định nghĩa trong chính font nữa mà được định nghĩa trong node sử dụng font. Việc này được thực hiện trong mục **Theme Overrides > Font Sizes** của inspector.

    Điều này cho phép thay đổi kích thước font mà không phải nhân bản resource font cho từng kích thước font khác nhau.

Có 2 loại file font: *dynamic* (định dạng TTF/OTF/WOFF/WOFF2) và *bitmap* (định dạng BMFont ``.fnt`` hoặc hình ảnh monospace). Dynamic font là lựa chọn được sử dụng phổ biến nhất, vì có thể thay đổi kích thước mà vẫn hiển thị sắc nét ở các kích thước lớn hơn. Nhờ bản chất dựa trên vector, chúng cũng có thể chứa nhiều glyph hơn trong khi vẫn giữ kích thước file hợp lý so với bitmap font. Dynamic font cũng hỗ trợ một số tính năng nâng cao mà bitmap font không hỗ trợ, chẳng hạn như *ligatures* (nhiều ký tự biến đổi thành một thiết kế khác duy nhất).

.. tip::

    Bạn có thể tìm các file font được cấp phép tự do trên những website như `Google Fonts <https://fonts.google.com/>`__ và `Font Library <https://fontlibrary.org/>`__.

    Font được bảo vệ bởi bản quyền. Hãy kiểm tra kỹ giấy phép của font trước khi sử dụng, vì không phải font nào cũng cho phép sử dụng thương mại nếu chưa mua giấy phép.

.. seealso::

    Bạn có thể xem cách font hoạt động trên thực tế bằng `project demo BiDI and Font Features <https://github.com/godotengine/godot-demo-projects/tree/master/gui/bidi_and_font_features>`__.

Dynamic font
------------

Godot hỗ trợ các định dạng dynamic font sau:

- TrueType Font hoặc Collection (``.ttf``, ``.ttc``)
- OpenType Font hoặc Collection (``.otf``, ``.otc``)
- Web Open Font Format 1 (``.woff``)
- Web Open Font Format 2 (``.woff2``)

Mặc dù ``.woff`` và đặc biệt là ``.woff2`` thường tạo ra kích thước file nhỏ hơn, không có định dạng font nào "tốt hơn" một cách tuyệt đối. Trong hầu hết trường hợp, bạn nên sử dụng định dạng font được cung cấp trên website của nhà phát triển font.

Bitmap font
-----------

Godot hỗ trợ định dạng bitmap font BMFont (``.fnt``). Đây là định dạng được tạo bởi chương trình `BMFont <https://www.angelcode.com/products/bmfont/>`__. Ngoài ra còn có nhiều chương trình tương thích với BMFont, chẳng hạn như `BMGlyph <https://www.bmglyph.com/>`__ hoặc `fontcutter <https://github.com/fabienbk/fontcutter>`__ trên nền web.

Ngoài ra, bạn có thể import bất kỳ hình ảnh nào để sử dụng làm bitmap font. Để thực hiện việc này, hãy chọn hình ảnh trong dock FileSystem, chuyển đến dock Import, đổi loại import thành **Font Data (Image Font)**, sau đó nhấp vào **Reimport**:

.. figure:: img/using_fonts_bitmap_font_from_image_import_options.webp
   :align: center
   :alt: Đổi loại import thành Font Data (Image Font)

   Đổi loại import thành **Font Data (Image Font)**

Bố cục character set của font có thể theo bất kỳ thứ tự nào, nhưng nên sử dụng thứ tự khớp với Unicode tiêu chuẩn vì sẽ cần ít cấu hình hơn nhiều khi import. Ví dụ, bitmap font bên dưới chứa các ký tự `ASCII <https://en.wikipedia.org/wiki/ASCII>`__ và tuân theo thứ tự ASCII tiêu chuẩn:

.. figure:: img/using_fonts_monospace_bitmap_font_example.webp
   :align: center
   :alt: Ví dụ về bitmap font

   Nguồn: `LibreQuake <https://github.com/MissLav/LibreQuake/blob/master/lq1/gfx-wad/CONCHARS.png>`__ (đã thay đổi tỷ lệ và cắt để loại bỏ phạm vi mở rộng)

Có thể sử dụng các tùy chọn import sau để import thành công hình ảnh font ở trên:

.. figure:: img/using_fonts_bitmap_font_from_image_example_configuration.webp
   :align: center
   :alt: Các tùy chọn import cần sử dụng cho font ví dụ ở trên

   Các tùy chọn import cần sử dụng cho font ví dụ ở trên

Tùy chọn **Character Ranges** là một mảng ánh xạ từng vị trí trên hình ảnh (theo tọa độ tile, không phải pixel). Font atlas được duyệt từ trái sang phải và từ trên xuống dưới. Có thể chỉ định ký tự bằng số thập phân (``127``), số thập lục phân (``0x007f``) hoặc đặt giữa dấu nháy *đơn* (``'~'``). Có thể chỉ định các phạm vi bằng dấu gạch nối giữa các ký tự.

Ví dụ, ``0-127`` (hoặc ``0x0000-0x007f``) biểu thị toàn bộ phạm vi ASCII. Một ví dụ khác, ``' '-'~'`` tương đương với ``32-127`` và biểu thị phạm vi các ký tự ASCII *in được* (hiển thị được).

Hãy đảm bảo tùy chọn **Character Ranges** không vượt quá số **Columns** × **Rows** đã định nghĩa. Nếu không, font sẽ không import được.

Nếu hình ảnh font của bạn chứa các lề không được sử dụng cho glyph font (chẳng hạn như thông tin ghi công), hãy thử điều chỉnh **Image Margin**. Đây là lề chỉ được áp dụng một lần xung quanh toàn bộ hình ảnh.

Nếu hình ảnh font của bạn chứa các đường dẫn (dưới dạng các đường kẻ giữa những glyph) hoặc nếu khoảng cách giữa các ký tự có vẻ không chính xác, hãy thử điều chỉnh **Character Margin**. Lề này được áp dụng cho từng glyph được import.

Nếu bạn cần kiểm soát khoảng cách giữa các ký tự tinh chỉnh hơn so với những gì các tùy chọn **Character Margin** cung cấp, bạn còn có thêm các tùy chọn khác.

Trước hết, **Character Ranges** hỗ trợ thêm 3 đối số sau phạm vi ký tự đã chỉ định. Các đối số bổ sung này kiểm soát vị trí và khoảng cách của chúng. Theo thứ tự, chúng biểu thị độ tiến của khoảng trắng, độ lệch trên trục X và độ lệch trên trục Y. Chúng sẽ thay đổi độ tiến của khoảng trắng và độ lệch của từng ký tự theo số pixel được ghi. Độ tiến của khoảng trắng hữu ích nhất nếu, chẳng hạn, các chữ cái viết thường của bạn mảnh hơn các chữ cái viết hoa.

.. figure:: img/using_fonts_bitmap_font_advance_offsets_diagram.webp
   :align: center
   :alt: Sơ đồ minh họa các giá trị độ tiến và độ lệch được sử dụng trong các phạm vi ký tự.

   Lưu ý rằng các độ lệch có thể khiến văn bản bị cắt ở mép ranh giới của label.

Thứ hai, bạn cũng có thể thiết lập **Kerning Pairs** cho từng ký tự. Chỉ định cặp kerning bằng cách nhập hai tập hợp ký tự được ngăn cách bằng một khoảng trắng, sau đó thêm một khoảng trắng khác và một số để chỉ định cần thêm/bớt bao nhiêu pixel khoảng cách giữa hai tập hợp ký tự đó khi chúng được đặt cạnh nhau.

.. figure:: img/using_fonts_bitmap_kerning_pairs_example.webp

Nếu cần, bạn có thể chỉ định các ký tự trong cặp kerning bằng mã ký tự Unicode bằng cách nhập ``\uXXXX``, trong đó XXXX là giá trị thập lục phân của ký tự Unicode.

Tải file font
-------------

Để tải file font (dynamic hoặc bitmap), hãy sử dụng tùy chọn **Quick Load** hoặc **Load** trong menu thả xuống resource bên cạnh thuộc tính font, sau đó điều hướng đến file font tương ứng:

.. figure:: img/using_fonts_load_font.webp
   :align: center

   Tải file font

Bạn cũng có thể kéo và thả tệp phông chữ từ dock FileSystem vào thuộc tính inspector chấp nhận tài nguyên Font.

.. warning::

   Trong Godot 4.0 trở lên, các thuộc tính lọc và lặp texture được xác định tại vị trí texture được sử dụng, thay vì trên chính texture đó. Điều này cũng áp dụng cho phông chữ (cả phông chữ động và phông chữ bitmap).

   Các phông chữ có kiểu dáng pixel art nên tắt bộ lọc song tuyến bằng cách thay đổi cài đặt project **Rendering > Textures > Canvas Textures > Default Texture Filter** thành **Nearest**.

   Kích thước phông chữ cũng phải là bội số nguyên của kích thước thiết kế (thay đổi tùy theo từng phông chữ), đồng thời Control node sử dụng phông chữ cũng phải được scale theo một bội số nguyên. Nếu không, phông chữ có thể trông bị mờ. Kích thước phông chữ trong Godot được chỉ định bằng pixel (px), không phải point (pt). Hãy ghi nhớ điều này khi so sánh kích thước phông chữ giữa các phần mềm khác nhau.

   Bạn cũng có thể đặt chế độ lọc texture trên từng node kế thừa từ CanvasItem bằng cách đặt :ref:`CanvasItem.texture_filter <class_CanvasItem_property_texture_filter>`.

Viền và bóng phông chữ
----------------------

Có thể sử dụng viền và bóng phông chữ để cải thiện khả năng đọc khi chưa biết trước màu nền. Ví dụ, đây là trường hợp của các phần tử HUD được vẽ chồng lên một cảnh 2D/3D.

Viền phông chữ khả dụng trong hầu hết các node kế thừa từ Control, ngoài :ref:`class_Label3D`.

Để bật viền cho phông chữ trên một node cụ thể, hãy cấu hình các theme override **Font Outline Color** và **Outline Size** trong inspector. Kết quả sẽ trông như sau:

.. figure:: img/using_fonts_outline_example.webp
   :align: center
   :alt: Ví dụ về viền phông chữ

   Ví dụ về viền phông chữ

.. note::

   Nếu sử dụng phông chữ có kết xuất MSDF, tùy chọn import **MSDF Pixel Range** phải được đặt ít nhất bằng *twice* giá trị kích thước viền để kết xuất viền hiển thị chính xác. Nếu không, viền có thể trông như bị cắt sớm hơn dự định.

Hỗ trợ bóng phông chữ bị giới hạn hơn: chúng chỉ khả dụng trong
:ref:`class_Label` và :ref:`class_RichTextLabel`. Ngoài ra, bóng phông chữ luôn có cạnh cứng (nhưng bạn có thể giảm độ mờ để chúng trông tinh tế hơn). Để bật bóng phông chữ trên một node cụ thể, hãy cấu hình các theme override **Font Shadow Color**, **Shadow Offset X** và **Shadow Offset Y** tương ứng trong node Label hoặc RichTextLabel:

.. figure:: img/using_fonts_shadow.webp
   :align: center
   :alt: Cấu hình bóng phông chữ trong node Label

   Cấu hình bóng phông chữ trong node Label

Kết quả sẽ trông như sau:

.. figure:: img/using_fonts_shadow_example.webp
   :align: center
   :alt: Ví dụ về bóng phông chữ

   Ví dụ về bóng phông chữ

.. tip::

    Bạn có thể tạo các override cục bộ cho cách hiển thị phông chữ trong các node Label bằng cách tạo một
    :ref:`class_LabelSettings` resource mà bạn tái sử dụng trên các node Label. Resource này được ưu tiên hơn :ref:`theme properties <doc_gui_skinning>`.

Các tính năng phông chữ nâng cao
--------------------------------

.. _doc_using_fonts_antialiasing:

Antialiasing
~~~~~~~~~~~~

Bạn có thể điều chỉnh cách làm mượt phông chữ khi kết xuất bằng cách điều chỉnh *antialiasing* và *hinting*. Đây là các thuộc tính khác nhau, phục vụ những trường hợp sử dụng khác nhau.

Antialiasing kiểm soát cách làm mượt các cạnh glyph khi rasterize phông chữ. Phương pháp antialiasing mặc định (**Grayscale**) hoạt động tốt trên mọi công nghệ màn hình. Tuy nhiên, ở kích thước nhỏ, antialiasing grayscale có thể khiến phông chữ trông bị mờ.

Có thể cải thiện độ sắc nét của antialiasing bằng cách sử dụng tối ưu hóa subpixel LCD, tận dụng các mẫu subpixel của hầu hết màn hình LCD bằng cách offset antialiasing của phông chữ theo từng kênh (đỏ/xanh lá/xanh dương). Nhược điểm là cách này có thể tạo ra hiện tượng "viền màu" trên các cạnh, đặc biệt trên những công nghệ màn hình không sử dụng subpixel RGB tiêu chuẩn (chẳng hạn như màn hình OLED).

Trong hầu hết game, bạn nên sử dụng antialiasing mặc định **Grayscale**. Đối với các ứng dụng không phải game, bạn nên thử khám phá tối ưu hóa subpixel LCD.

.. figure:: img/using_fonts_antialiasing_comparison.webp
   :align: center
   :alt: So sánh antialiasing của phông chữ

   Từ trên xuống dưới: Disabled, Grayscale, LCD Subpixel (RGB)

.. note::

    Không thể thay đổi antialiasing trên :ref:`MSDF-rendered fonts <doc_using_fonts_msdf>` – các phông chữ này luôn được kết xuất bằng antialiasing grayscale.

.. _doc_using_fonts_hinting:

Hinting
~~~~~~~

Hinting kiểm soát mức độ mạnh mà các cạnh glyph được snap vào pixel khi rasterize phông chữ. **None** cho hình thức mượt nhất, nhưng có thể khiến phông chữ trông bị mờ ở kích thước nhỏ. **Light** (mặc định) sắc nét hơn nhờ snap các cạnh glyph vào pixel chỉ trên trục Y, trong khi **Full** còn sắc nét hơn nhờ snap các cạnh glyph vào pixel trên cả hai trục X và Y. Tùy theo sở thích cá nhân, bạn có thể thích sử dụng chế độ hinting này hơn chế độ kia.

.. figure:: img/using_fonts_hinting_comparison.webp
   :align: center
   :alt: So sánh hinting của phông chữ

   Từ trên xuống dưới: None, Light, Full hinting

.. note::

    Nếu việc thay đổi chế độ hinting không tạo ra hiệu ứng nhìn thấy được sau khi nhấp vào **Reimport**, nguyên nhân thường là do phông chữ không bao gồm các instruction hinting. Bạn có thể khắc phục bằng cách tìm một phiên bản tệp phông chữ có bao gồm các instruction hinting hoặc bật **Force Autohinter** trong dock Import. Tùy chọn này sẽ sử dụng autohinter của `FreeType <https://freetype.org/>`__ để tự động thêm các instruction hinting vào phông chữ đã import.

.. _doc_using_fonts_subpixel_positioning:

Định vị subpixel
~~~~~~~~~~~~~~~~

Có thể điều chỉnh việc định vị subpixel. Đây là một tính năng của `FreeType <https://freetype.org/>`__, cho phép kết xuất glyph gần với hình dạng dự kiến hơn. Cài đặt mặc định **Auto** sẽ tự động bật định vị subpixel ở kích thước nhỏ, nhưng tắt tính năng này ở kích thước phông chữ lớn để cải thiện hiệu suất rasterization.

Bạn có thể buộc chế độ định vị subpixel thành **Disabled**, **One half of a pixel** hoặc **One quarter of a pixel**. **One quarter of a pixel** cho chất lượng tốt nhất, nhưng thời gian rasterization lâu hơn.

Việc thay đổi antialiasing, hinting và định vị subpixel tạo ra hiệu ứng rõ nhất ở các kích thước phông chữ nhỏ.

.. warning::

   Các phông chữ có kiểu dáng pixel art nên đặt chế độ định vị subpixel thành **Disabled**. Nếu không, phông chữ có thể trông như có các kích thước pixel không đồng đều.

   Bước này không bắt buộc đối với phông chữ bitmap, vì định vị subpixel chỉ liên quan đến phông chữ động (thường được tạo từ các phần tử vector).

.. _doc_using_fonts_mipmaps:

Mipmaps
~~~~~~~

Theo mặc định, font không được tạo mipmap để giảm mức sử dụng bộ nhớ và tăng tốc quá trình rasterization. Tuy nhiên, điều này có thể khiến font được thu nhỏ trở nên nhiễu hạt. Điều này có thể đặc biệt dễ nhận thấy với :ref:`doc_3d_text` không bật **Fixed Size**. Điều này cũng có thể xảy ra khi hiển thị văn bản bằng font rasterized truyền thống (không phải :ref:`MSDF <doc_using_fonts_msdf>`) trong một node Control có scale nhỏ hơn ``(1, 1)``.

Sau khi chọn một font trong dock FileSystem, bạn có thể bật **Mipmaps** trong dock Import để cải thiện hình thức hiển thị của font được thu nhỏ.

Mipmap cũng có thể được bật cho font MSDF. Điều này có thể cải thiện một chút chất lượng hiển thị font ở các kích thước nhỏ hơn mặc định, nhưng font MSDF vốn đã hạn chế hiện tượng nhiễu hạt.

.. _doc_using_fonts_msdf:

Hiển thị font MSDF
~~~~~~~~~~~~~~~~~~

Hiển thị font bằng multi-channel signed distance field (MSDF) cho phép hiển thị font ở bất kỳ kích thước nào mà không cần rasterize lại khi kích thước thay đổi.

Hiển thị font MSDF có 2 ưu điểm so với rasterization font truyền thống, vốn được Godot sử dụng theo mặc định:

- Font luôn trông sắc nét, ngay cả ở kích thước rất lớn.
- Có ít hiện tượng giật hơn khi lần đầu hiển thị các ký tự *ở kích thước font lớn*, vì không cần thực hiện rasterization.

Nhược điểm của việc hiển thị font MSDF là:

- Chi phí cơ bản cao hơn khi hiển thị font. Điều này thường không đáng chú ý trên các nền tảng desktop, nhưng có thể ảnh hưởng đến các thiết bị di động cấp thấp.
- Font ở kích thước nhỏ sẽ không trông rõ bằng font rasterized do không có hinting.
- Việc hiển thị các glyph mới lần đầu *ở kích thước font nhỏ* có thể tốn kém hơn so với font rasterized truyền thống.
  :ref:`doc_using_fonts_font_prerendering` có thể được sử dụng để giảm nhẹ vấn đề này.
- Không thể bật tối ưu hóa subpixel LCD cho font MSDF.
- Font có các đường viền tự giao nhau sẽ không được hiển thị chính xác ở chế độ MSDF. Nếu bạn nhận thấy vấn đề hiển thị ở các font được tải xuống từ những website như `Google Fonts <https://fonts.google.com>`__, hãy thử tải font từ website chính thức của tác giả font.

.. figure:: img/using_fonts_rasterized_vs_msdf_comparison.webp
   :align: center
   :alt: So sánh các phương pháp rasterization font

   So sánh các phương pháp rasterization font. Từ trên xuống dưới: rasterized không oversampling, rasterized có oversampling, MSDF

Để bật hiển thị MSDF cho một font cụ thể, hãy chọn font đó trong dock FileSystem, chuyển đến dock Import, bật **Multichannel Signed Distance Field**, sau đó nhấp **Reimport**:

.. figure:: img/using_fonts_msdf_import_options.webp
   :align: center
   :alt: Bật MSDF trong các tùy chọn import của font

   Bật MSDF trong các tùy chọn import của font

.. _doc_using_fonts_emoji:

Sử dụng emoji
~~~~~~~~~~~~~

Godot hỗ trợ hạn chế đối với font emoji:

- Font emoji CBDT/CBLC (PNG nhúng) và SVG được hỗ trợ.
- Font emoji COLR/CPAL (định dạng vector tùy chỉnh) **không** được hỗ trợ.
- Nén ảnh bitmap EMJC (được font emoji hệ thống của iOS sử dụng) **không** được hỗ trợ. Điều này có nghĩa là để hỗ trợ emoji trên iOS, bạn phải sử dụng font tùy chỉnh dùng phương thức nén bitmap SVG hoặc PNG.

Để Godot có thể hiển thị emoji, font được sử dụng (hoặc một trong các
:ref:`font dự phòng <doc_using_fonts_font_fallbacks>`) cần chứa các emoji đó. Nếu không, emoji sẽ không được hiển thị và thay vào đó sẽ xuất hiện các ký tự giữ chỗ "tofu":

.. figure:: img/using_fonts_emoji_placeholder_characters.webp
   :align: center
   :alt: Giao diện mặc định khi thử sử dụng emoji trong một label

   Giao diện mặc định khi thử sử dụng emoji trong một label

Sau khi thêm một font để hiển thị emoji, chẳng hạn như `Noto Color Emoji <https://fonts.google.com/noto/specimen/Noto+Color+Emoji>`__, bạn sẽ nhận được kết quả mong đợi:

.. figure:: img/using_fonts_emoji_correct_characters.webp
   :align: center
   :alt: Giao diện chính xác sau khi thêm font emoji vào label

   Giao diện chính xác sau khi thêm font emoji vào label

Để sử dụng font thông thường cùng với emoji, bạn nên chỉ định một
:ref:`font dự phòng <doc_using_fonts_font_fallbacks>` trỏ đến font emoji trong các tùy chọn import nâng cao của font thông thường. Nếu muốn sử dụng font mặc định của project trong khi vẫn hiển thị emoji, hãy để thuộc tính **Base Font** trong FontVariation trống, đồng thời thêm một font dự phòng trỏ đến font emoji:

.. tip::

    Font emoji có kích thước khá lớn, vì vậy bạn có thể muốn :ref:`tải font hệ thống <doc_using_fonts_system_fonts>` để cung cấp các glyph emoji thay vì đóng gói font cùng project. Điều này cho phép cung cấp đầy đủ hỗ trợ emoji trong project mà không làm tăng kích thước PCK được export. Nhược điểm là emoji sẽ trông khác nhau tùy theo nền tảng, và không phải nền tảng nào cũng hỗ trợ tải font hệ thống.

    Bạn cũng có thể sử dụng font hệ thống làm font dự phòng.

Sử dụng icon font
~~~~~~~~~~~~~~~~~

Các công cụ như `Fontello <https://fontello.com/>`__ có thể được sử dụng để tạo các file font chứa vector được import từ file SVG. Bạn có thể dùng cách này để hiển thị các phần tử vector tùy chỉnh trong văn bản hoặc tạo các icon 3D đùn với :ref:`doc_3d_text` và TextMesh.

.. note::

    Fontello hiện không hỗ trợ tạo font nhiều màu (mà Godot có thể hiển thị). Tính đến tháng 11 năm 2022, hỗ trợ font nhiều màu trong các công cụ tạo icon font vẫn còn hạn chế.

Tùy theo trường hợp sử dụng, cách này có thể cho kết quả tốt hơn so với việc sử dụng thẻ ``img`` trong :ref:`RichTextLabel <doc_bbcode_in_richtextlabel>`. Không giống ảnh bitmap (bao gồm cả SVG được Godot rasterize khi import), dữ liệu vector thực có thể được thay đổi kích thước tùy ý mà không làm giảm chất lượng.

Sau khi tải xuống file font đã tạo, hãy load file đó vào project Godot rồi chỉ định nó làm font tùy chỉnh cho node Label, RichTextLabel hoặc Label3D. Chuyển sang giao diện web Fontello, sau đó sao chép ký tự bằng cách chọn ký tự rồi nhấn :kbd:`Ctrl + C` (:kbd:`Cmd + C` trên macOS). Dán ký tự vào thuộc tính **Text** của node Label. Ký tự sẽ xuất hiện dưới dạng glyph giữ chỗ trong inspector, nhưng sẽ hiển thị chính xác trong viewport 2D/3D.

Để sử dụng icon font cùng với font truyền thống trong cùng một Control, bạn có thể chỉ định icon font làm :ref:`font dự phòng <doc_using_fonts_font_fallbacks>`. Điều này hoạt động vì icon font sử dụng *vùng dành riêng cho mục đích sử dụng riêng* của Unicode, vốn được dành cho font tùy chỉnh và theo thiết kế không chứa glyph tiêu chuẩn.

.. note::

    Một số icon font hiện đại như `Font Awesome 6 <https://fontawesome.com/download>`__ có biến thể desktop sử dụng *ligature* để chỉ định icon. Điều này cho phép bạn chỉ định icon bằng cách nhập trực tiếp tên của chúng vào thuộc tính **Text** của bất kỳ node nào có thể hiển thị font. Sau khi nhập đầy đủ tên icon dưới dạng văn bản (chẳng hạn như ``house``), tên đó sẽ được thay thế bằng icon.

    Mặc dù dễ sử dụng hơn, cách tiếp cận này không thể dùng với font fallback vì các ký tự của font chính sẽ được ưu tiên hơn ligature của font fallback.

.. _doc_using_fonts_font_fallbacks:

Font fallback
~~~~~~~~~~~~~

Godot hỗ trợ định nghĩa một hoặc nhiều font fallback khi font chính không có glyph cần hiển thị. Có 2 trường hợp sử dụng chính để định nghĩa font fallback:

- Sử dụng một font chỉ hỗ trợ các bộ ký tự Latin, nhưng dùng một font khác để có thể hiển thị văn bản thuộc một bộ ký tự khác, chẳng hạn như Cyrillic.
- Sử dụng một font để hiển thị văn bản và một font khác để hiển thị emoji hoặc biểu tượng.

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào tệp font trong dock FileSystem. Bạn cũng có thể chọn font trong dock FileSystem, chuyển đến dock Import rồi chọn **Advanced…** ở dưới cùng:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   dock Import

Trong hộp thoại xuất hiện, tìm phần **Fallbacks** trên thanh bên ở bên phải, nhấp vào văn bản **Array[Font] (size 0)** để mở rộng thuộc tính, rồi nhấp vào **Add Element**:

.. figure:: img/using_fonts_font_fallbacks_add.webp
   :align: center

   Thêm font fallback

Nhấp vào mũi tên danh sách thả xuống trên phần tử mới, rồi chọn một tệp font bằng tùy chọn **Quick Load** hoặc **Load**:

.. figure:: img/using_fonts_font_fallbacks_load.webp
   :align: center

   Tải font fallback

Bạn cũng có thể thêm font fallback khi sử dụng font mặc định của project. Để làm vậy, hãy để trống thuộc tính **Base Font** trong khi thêm một hoặc nhiều font fallback.

.. note::

    Bạn cũng có thể định nghĩa font fallback ở cấp cục bộ, tương tự như
    :ref:`doc_using_fonts_opentype_font_features`, nhưng ở đây không đề cập đến cách này để nội dung được ngắn gọn.

.. _doc_using_fonts_variable_fonts:

Font biến thiên
~~~~~~~~~~~~~~~

Godot hỗ trợ đầy đủ `variable fonts <https://variablefonts.io/>`__, cho phép bạn dùng một tệp font duy nhất để biểu diễn nhiều độ đậm và kiểu font khác nhau (regular, bold, italic, …). Tệp font bạn sử dụng phải hỗ trợ tính năng này.

Để sử dụng variable font, hãy tạo một :ref:`class_FontVariation` resource tại vị trí bạn định sử dụng font, sau đó tải một tệp font vào resource FontVariation:

.. figure:: img/using_fonts_font_variation_create.webp
   :align: center

   Tạo resource FontVariation

.. figure:: img/using_fonts_font_variation_load.webp
   :align: center

   Tải tệp font vào resource FontVariation

Cuộn xuống phần **Variation** của FontVariation, rồi nhấp vào văn bản **Variation Coordinates** để mở rộng danh sách các trục có thể điều chỉnh:

.. figure:: img/using_fonts_font_variation_variable_font.webp
   :align: center

   Danh sách các trục biến thiên

Tập hợp các trục bạn có thể điều chỉnh phụ thuộc vào font đã tải. Một số variable font chỉ hỗ trợ một trục điều chỉnh (thường là *weight* hoặc *slant*), trong khi những font khác có thể hỗ trợ nhiều trục điều chỉnh.

Ví dụ, đây là font `Inter V <https://rsms.me/inter/>`__ với *weight* bằng ``900`` và *slant* bằng ``-10``:

.. figure:: img/using_fonts_font_variation_variable_font_example.webp
   :align: center

   Ví dụ về variable font (Inter V)

.. tip::

    Mặc dù tên và thang đo của các trục variable font chưa được tiêu chuẩn hóa, các nhà thiết kế font thường tuân theo một số quy ước phổ biến. Trục *weight* được tiêu chuẩn hóa trong OpenType như sau:

    +--------------+---------------------------+
    | Giá trị trục | Độ đậm font hiệu dụng     |
    +==============+===========================+
    | ``100``      | Thin (Hairline)           |
    +--------------+---------------------------+
    | ``200``      | Extra Light (Ultra Light) |
    +--------------+---------------------------+
    | ``300``      | Light                     |
    +--------------+---------------------------+
    | ``400``      | **Regular (Normal)**      |
    +--------------+---------------------------+
    | ``500``      | Medium                    |
    +--------------+---------------------------+
    | ``600``      | Semi-Bold (Demi-Bold)     |
    +--------------+---------------------------+
    | ``700``      | **Bold**                  |
    +--------------+---------------------------+
    | ``800``      | Extra Bold (Ultra Bold)   |
    +--------------+---------------------------+
    | ``900``      | Black (Heavy)             |
    +--------------+---------------------------+
    | ``950``      | Extra Black (Ultra Black) |
    +--------------+---------------------------+

Bạn có thể lưu FontVariation vào tệp resource ``.tres`` để sử dụng lại ở những nơi khác:

.. figure:: img/using_fonts_font_variation_save_to_file.webp
   :align: center

   Lưu FontVariation vào tệp resource bên ngoài

Bold và italic giả lập
~~~~~~~~~~~~~~~~~~~~~~

Khi viết văn bản bằng bold hoặc italic, sử dụng các biến thể font được thiết kế riêng cho mục đích này sẽ cho kết quả đẹp hơn. Khoảng cách giữa các glyph sẽ nhất quán hơn khi dùng font bold, và hình dạng của một số glyph có thể thay đổi hoàn toàn trong các biến thể italic (so sánh "a" và *"a"*).

Tuy nhiên, font bold và italic thực yêu cầu phải phân phối thêm nhiều tệp font, làm tăng kích thước bản phân phối. Cũng có thể sử dụng một tệp :ref:`variable font <doc_using_fonts_variable_fonts>`, nhưng tệp này sẽ lớn hơn một font không biến thiên đơn lẻ. Mặc dù kích thước tệp thường không phải vấn đề đối với các project desktop, đây có thể là mối lo ngại đối với các project mobile/web muốn giữ kích thước bản phân phối ở mức thấp nhất có thể.

Để cho phép hiển thị font bold và italic mà không phải phân phối thêm font (hoặc sử dụng variable font có kích thước lớn hơn), Godot hỗ trợ bold và italic *giả lập*.

.. figure:: img/using_fonts_faux_bold_italic_vs_real_bold_italic.webp
   :align: center
   :alt: Bold/italic giả lập (trên), bold/italic thực (dưới). Font thường được sử dụng: Open Sans SemiBold

   Bold/italic giả lập (trên), bold/italic thực (dưới). Font thường được sử dụng: Open Sans SemiBold

Bold và italic giả lập được tự động sử dụng trong các tag bold và italic của :ref:`class_RichTextLabel` nếu không cung cấp font tùy chỉnh cho bold và/hoặc italic.

Để sử dụng bold giả lập, hãy tạo resource FontVariation trong một thuộc tính yêu cầu resource Font. Đặt **Variation > Embolden** thành một giá trị dương để làm font đậm hơn hoặc thành một giá trị âm để làm font bớt đậm. Các giá trị được khuyến nghị nằm trong khoảng từ ``0.5`` đến ``1.2``, tùy thuộc vào font.

Italic giả được tạo bằng cách làm nghiêng văn bản, thực hiện bằng cách sửa đổi phép biến đổi theo từng ký tự. Tính năng này cũng được cung cấp trong FontVariation thông qua thuộc tính **Variation > Transform**. Đặt thành phần ``yx`` của phép biến đổi ký tự thành một giá trị dương sẽ làm văn bản nghiêng. Các giá trị được khuyến nghị nằm trong khoảng từ ``0.2`` đến ``0.4``, tùy thuộc vào font.

Điều chỉnh khoảng cách font
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để phục vụ mục đích tạo kiểu hoặc giúp dễ đọc hơn, bạn có thể muốn điều chỉnh cách font được hiển thị trong Godot.

Tạo một tài nguyên FontVariation trong thuộc tính yêu cầu tài nguyên Font. Có 4 thuộc tính trong phần **Variation > Extra Spacing**, chấp nhận các giá trị dương và âm:

- **Glyph:** Khoảng cách bổ sung giữa mỗi glyph.
- **Space:** Khoảng cách bổ sung giữa các từ.
- **Top:** Khoảng cách bổ sung phía trên glyph. Khoảng cách này được sử dụng cho văn bản nhiều dòng, đồng thời được dùng để tính kích thước tối thiểu của các control như :ref:`class_Label` và :ref:`class_Button`.
- **Bottom:** Khoảng cách bổ sung phía dưới glyph. Khoảng cách này được sử dụng cho văn bản nhiều dòng, đồng thời được dùng để tính kích thước tối thiểu của các control như :ref:`class_Label` và :ref:`class_Button`.

Bạn cũng có thể điều chỉnh thuộc tính **Variation > Transform** để kéo giãn các ký tự theo chiều ngang hoặc chiều dọc. Cụ thể, hãy điều chỉnh các thành phần ``xx`` (tỷ lệ theo chiều ngang) và ``yy`` (tỷ lệ theo chiều dọc). Hãy nhớ điều chỉnh khoảng cách glyph để tính đến mọi thay đổi, vì phép biến đổi glyph không ảnh hưởng đến lượng không gian mà mỗi glyph chiếm trong văn bản. Nên hạn chế sử dụng kiểu co giãn không đồng đều này, vì font thường không được thiết kế để hiển thị khi bị kéo giãn.

.. _doc_using_fonts_opentype_font_features:

Tính năng font OpenType
~~~~~~~~~~~~~~~~~~~~~~~

Godot hỗ trợ bật các tính năng font OpenType, một cách thức được chuẩn hóa để xác định các ký tự thay thế có thể bật mà không cần thay thế hoàn toàn các tệp font. Mặc dù được gọi là tính năng font OpenType, chúng cũng được hỗ trợ trong các tệp font TrueType (``.ttf``) và WOFF/WOFF2.

Mức độ hỗ trợ các tính năng OpenType phụ thuộc nhiều vào font được sử dụng. Một số font không hỗ trợ bất kỳ tính năng OpenType nào, trong khi các font khác có thể hỗ trợ hàng chục tính năng có thể bật tắt.

Có 2 cách sử dụng các tính năng font OpenType:

**Trên toàn cục trong tệp font**

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào tệp font trong FileSystem dock. Bạn cũng có thể chọn font trong FileSystem dock, chuyển đến Import dock rồi chọn **Advanced…** ở phía dưới:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   Import dock

Trong hộp thoại xuất hiện, tìm phần **Metadata Overrides > OpenType Features** trên thanh bên ở bên phải, nhấp vào dòng chữ **Features (0 of N set)** để mở rộng thuộc tính, rồi nhấp vào **Add Feature**:

.. figure:: img/using_fonts_advanced_import_settings_opentype_features.webp
   :align: center

   Ghi đè tính năng OpenType trong Advanced Import Settings

**Trong một lần sử dụng font cụ thể (FontVariation)**

Để sử dụng một tính năng font, hãy tạo một tài nguyên FontVariation như khi tạo một
:ref:`font biến đổi <doc_using_fonts_variable_fonts>`, sau đó tải một tệp font vào tài nguyên FontVariation:

.. figure:: img/using_fonts_font_variation_create.webp
   :align: center

   Tạo tài nguyên FontVariation

.. figure:: img/using_fonts_font_variation_load.webp
   :align: center

   Tải tệp font vào tài nguyên FontVariation

Cuộn xuống phần **OpenType Features** của FontVariation, nhấp vào dòng chữ **Features (0 of N set)** để mở rộng thuộc tính, rồi nhấp vào **Add Feature** và chọn tính năng mong muốn trong danh sách thả xuống:

.. figure:: img/using_fonts_font_variation_opentype_features.webp
   :align: center

   Chỉ định các tính năng OpenType trong tài nguyên FontVariation

Ví dụ: dưới đây là font `Inter <https://rsms.me/inter/>`__ khi chưa bật tính năng *Slashed Zero* (phía trên), sau đó là khi đã bật tính năng OpenType *Slashed Zero* (phía dưới):

.. figure:: img/using_fonts_font_variation_slashed_zero.webp
   :align: center

   So sánh tính năng OpenType (Inter)

Bạn có thể tắt ligature và/hoặc kerning cho một font cụ thể bằng cách thêm các tính năng OpenType, sau đó bỏ chọn chúng trong inspector:

.. figure:: img/using_fonts_font_variation_disable_ligatures.webp
   :align: center

   Tắt ligature và kerning cho một font

.. _doc_using_fonts_system_fonts:

Font hệ thống
~~~~~~~~~~~~~

.. warning::

    Chỉ hỗ trợ tải font hệ thống trên Windows, macOS, Linux, Android và iOS.

    Tuy nhiên, việc tải font hệ thống trên Android không đáng tin cậy vì không có API chính thức để thực hiện việc này. Godot phải dựa vào việc phân tích các tệp cấu hình hệ thống, vốn có thể bị các nhà cung cấp Android bên thứ ba sửa đổi. Điều này có thể khiến việc tải font hệ thống không hoạt động.

Font hệ thống là một loại tài nguyên khác so với font đã import. Chúng không bao giờ thực sự được import vào project mà được tải khi runtime. Điều này mang lại 2 lợi ích:

- Font không được đưa vào tệp PCK đã export, giúp giảm kích thước tệp của project đã export.
- Vì font không được đưa vào project đã export, điều này tránh được các vấn đề về giấy phép có thể phát sinh nếu các font hệ thống độc quyền được phân phối cùng với project.

Engine tự động sử dụng font hệ thống làm font dự phòng, nhờ đó có thể hiển thị các ký tự CJK và emoji mà không cần tải font tùy chỉnh. Tuy nhiên, có một số hạn chế áp dụng như đã đề cập trong
phần :ref:`Sử dụng emoji <doc_using_fonts_emoji>`.

Tạo một tài nguyên :ref:`class_SystemFont` tại vị trí bạn muốn sử dụng font hệ thống:

.. figure:: img/using_fonts_system_font_create.webp
   :align: center

   Tạo tài nguyên SystemFont

.. figure:: img/using_fonts_system_font_specify.webp
   :align: center

   Chỉ định tên font để sử dụng trong tài nguyên SystemFont

Bạn có thể chỉ định rõ ràng một hoặc nhiều tên font (chẳng hạn như ``Arial``), hoặc chỉ định *alias* của tên font ánh xạ đến một font mặc định "tiêu chuẩn" của hệ thống:

.. Android font information sourced from <https://android.googlesource.com/platform/frameworks/base/+/master/data/fonts/fonts.xml>

+----------------+-----------------+----------------+-------------------------+--------------------+
| Bí danh font   | Windows         | macOS/iOS      | Linux                   | Android            |
+================+=================+================+=========================+====================+
| ``sans-serif`` | Arial           | Helvetica      | *Được fontconfig xử lý* | Roboto / Noto Sans |
+----------------+-----------------+----------------+-------------------------+--------------------+
| ``serif``      | Times New Roman | Times          | *Được fontconfig xử lý* | Noto Serif         |
+----------------+-----------------+----------------+-------------------------+--------------------+
| ``monospace``  | Courier New     | Courier        | *Được fontconfig xử lý* | Droid Sans Mono    |
+----------------+-----------------+----------------+-------------------------+--------------------+
| ``cursive``    | Comic Sans MS   | Apple Chancery | *Được fontconfig xử lý* | Dancing Script     |
+----------------+-----------------+----------------+-------------------------+--------------------+
| ``fantasy``    | Gabriola        | Papyrus        | *Được fontconfig xử lý* | Droid Sans Mono    |
+----------------+-----------------+----------------+-------------------------+--------------------+

Trên Android, Roboto được dùng cho văn bản Latin/Cyrillic và Noto Sans được dùng cho glyph của các ngôn ngữ khác, chẳng hạn như CJK. Trên các bản phân phối Android của bên thứ ba, lựa chọn font chính xác có thể khác.

Nếu chỉ định nhiều font, font đầu tiên được tìm thấy trên hệ thống sẽ được sử dụng (từ trên xuống dưới). Tên font và bí danh không phân biệt chữ hoa chữ thường trên mọi nền tảng.

Tương tự như các biến thể font, bạn có thể lưu bố cục SystemFont vào một tệp tài nguyên để sử dụng lại ở những nơi khác.

Hãy nhớ rằng các font hệ thống khác nhau có các metric khác nhau, nghĩa là văn bản vừa trong một hình chữ nhật trên nền tảng này có thể không vừa trên nền tảng khác. Trong quá trình phát triển, luôn chừa thêm một khoảng trống để các nhãn có thể mở rộng thêm nếu cần.

.. note::

    Không giống Windows và macOS/iOS, tập hợp font mặc định được cung cấp trên Linux phụ thuộc vào bản phân phối. Điều này có nghĩa là trên các bản phân phối Linux khác nhau, các font khác nhau có thể được hiển thị cho một tên hoặc bí danh font hệ thống nhất định.

Bạn cũng có thể tải font tại runtime ngay cả khi chúng chưa được cài đặt trên hệ thống. Xem :ref:`Tải và lưu tại runtime <doc_runtime_file_loading_and_saving_fonts>` để biết thêm chi tiết.

.. _doc_using_fonts_font_prerendering:

Kết xuất trước font
~~~~~~~~~~~~~~~~~~~

Khi sử dụng các font raster truyền thống, Godot sẽ lưu vào bộ nhớ đệm các glyph theo từng font và kích thước. Điều này làm giảm hiện tượng giật, nhưng hiện tượng này vẫn có thể xảy ra lần đầu tiên một glyph được hiển thị khi chạy project. Điều này đặc biệt dễ nhận thấy ở kích thước font lớn hơn hoặc trên thiết bị di động.

Khi sử dụng font MSDF, font chỉ cần được raster hóa một lần thành một texture trường khoảng cách có dấu đặc biệt. Điều này có nghĩa là có thể thực hiện việc lưu vào bộ nhớ đệm hoàn toàn theo từng font mà không cần xét đến kích thước font. Tuy nhiên, quá trình kết xuất ban đầu của font MSDF chậm hơn so với font raster truyền thống ở kích thước trung bình.

Để tránh các vấn đề giật liên quan đến việc kết xuất font, bạn có thể *kết xuất trước* một số glyph nhất định. Bạn có thể thực hiện việc này cho tất cả glyph dự định sử dụng (để đạt kết quả tối ưu) hoặc chỉ cho các glyph phổ biến có nhiều khả năng xuất hiện trong khi chơi game (để giảm kích thước tệp). Các glyph chưa được kết xuất trước sẽ được raster hóa tức thời như thường lệ.

.. note::

    Trong cả hai trường hợp (truyền thống và MSDF), quá trình raster hóa font được thực hiện trên CPU. Điều này có nghĩa là hiệu năng GPU không ảnh hưởng đến thời gian raster hóa font.

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào tệp font trong dock FileSystem. Bạn cũng có thể chọn font trong dock FileSystem, chuyển đến dock Import rồi chọn **Advanced…** ở phía dưới:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   Import dock

Chuyển đến tab **Pre-render Configurations** của hộp thoại Advanced Import Settings, sau đó thêm một cấu hình bằng cách nhấp vào biểu tượng "dấu cộng":

.. figure:: img/using_fonts_advanced_import_settings_prerender_new_configuration.webp
   :align: center
   :alt: Thêm cấu hình kết xuất trước mới trong hộp thoại Advanced Import Settings

   Thêm cấu hình kết xuất trước mới trong hộp thoại Advanced Import Settings

Sau khi thêm cấu hình, hãy đảm bảo cấu hình đó được chọn bằng cách nhấp một lần vào tên của cấu hình. Bạn cũng có thể đổi tên cấu hình bằng cách nhấp đúp vào cấu hình đó.

Có 2 cách để thêm glyph cần kết xuất trước vào một cấu hình nhất định. Bạn có thể kết hợp sử dụng cả hai cách:

**Sử dụng văn bản từ bản dịch**

Đối với hầu hết project, đây là cách thuận tiện nhất vì nó tự động lấy văn bản từ các bản dịch ngôn ngữ của bạn. Nhược điểm là cách này chỉ có thể được sử dụng nếu project của bạn hỗ trợ
:ref:`quốc tế hóa <doc_internationalizing_games>`. Nếu không, hãy dùng cách tiếp cận "Sử dụng văn bản tùy chỉnh" được mô tả bên dưới.

Sau khi thêm các bản dịch vào Project Settings, hãy sử dụng tab **Glyphs from the Translations** để kiểm tra các bản dịch bằng cách nhấp đúp vào chúng, sau đó nhấp vào **Shape All Strings in the Translations and Add Glyphs** ở phía dưới:

.. figure:: img/using_fonts_advanced_import_settings_prerender_translation.webp
   :align: center
   :alt: Bật tính năng kết xuất trước trong hộp thoại Advanced Import Settings với tab Glyphs from the Translations

   Bật tính năng kết xuất trước trong hộp thoại Advanced Import Settings với tab **Glyphs from the Translations**

.. note::

    Danh sách glyph được kết xuất trước không tự động cập nhật khi các bản dịch được cập nhật, vì vậy bạn cần lặp lại quy trình này nếu các bản dịch đã thay đổi đáng kể.

**Sử dụng văn bản tùy chỉnh**

Mặc dù yêu cầu chỉ định thủ công văn bản sẽ xuất hiện trong game, đây là cách hiệu quả nhất đối với các game không có tính năng nhập văn bản của người dùng. Cách này đáng được cân nhắc cho các game di động để giảm kích thước tệp của ứng dụng được phân phối.

Để sử dụng văn bản hiện có làm cơ sở cho việc prerender, hãy đi đến tab phụ **Glyphs from the Text** của hộp thoại Advanced Import Settings, nhập văn bản vào cửa sổ bên phải, sau đó nhấp vào **Shape Text and Add Glyphs** ở cuối hộp thoại:

.. figure:: img/using_fonts_advanced_import_settings_prerender_text.webp
   :align: center
   :alt: Bật prerender trong hộp thoại Advanced Import Settings, tab Glyphs from the Text

   Bật prerender trong hộp thoại Advanced Import Settings với tab **Glyphs from the Text**

.. tip::

    Nếu dự án của bạn hỗ trợ :ref:`internationalization <doc_internationalizing_games>`, bạn có thể dán nội dung của các tệp CSV hoặc PO vào ô bên trên để nhanh chóng prerender mọi ký tự có thể được hiển thị trong quá trình chơi (không bao gồm các chuỗi do người dùng cung cấp hoặc không cần dịch).

**Bằng cách bật các bộ ký tự**

Phương pháp thứ hai yêu cầu ít cấu hình và ít cập nhật hơn nếu văn bản trong game thay đổi, đồng thời phù hợp hơn với các game nhiều văn bản hoặc game multiplayer có chat. Mặt khác, phương pháp này có thể khiến các glyph không bao giờ xuất hiện trong game vẫn được prerender, kém hiệu quả hơn về kích thước tệp.

Để sử dụng văn bản hiện có làm cơ sở cho việc prerender, hãy đi đến tab phụ **Glyphs from the Character Map** của hộp thoại Advanced Import Settings, sau đó *nhấp đúp* vào các bộ ký tự cần bật ở bên phải:

.. figure:: img/using_fonts_advanced_import_settings_prerender_character_map.webp
   :align: center
   :alt: Bật prerender trong hộp thoại Advanced Import Settings, tab Glyphs from the Character Map

   Bật prerender trong hộp thoại Advanced Import Settings với tab **Glyphs from the Character Map**

Để đảm bảo prerender đầy đủ, các bộ ký tự cần bật phụ thuộc vào những ngôn ngữ được game hỗ trợ. Đối với tiếng Anh, chỉ cần bật **Basic Latin**. Bật thêm **Latin-1 Supplement** cho phép hỗ trợ đầy đủ nhiều ngôn ngữ hơn, chẳng hạn như tiếng Pháp, tiếng Đức và tiếng Tây Ban Nha. Đối với tiếng Nga, cần bật **Cyrillic**, v.v.

Thuộc tính font mặc định của dự án
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong phần **GUI > Theme** của Project Settings nâng cao, bạn có thể chọn cách font mặc định được kết xuất:

- **Default Font Antialiasing:** Kiểm soát phương thức
  :ref:`antialiasing <doc_using_fonts_antialiasing>` được sử dụng cho font mặc định của dự án.
- **Default Font Hinting:** Kiểm soát phương thức
  :ref:`hinting <doc_using_fonts_hinting>` được sử dụng cho font mặc định của dự án.
- **Default Font Subpixel Positioning:** Kiểm soát phương thức
  :ref:`subpixel positioning <doc_using_fonts_subpixel_positioning>` cho font mặc định của dự án.
- **Default Font Multichannel Signed Distance Field:** Nếu là ``true``, khiến font mặc định của dự án sử dụng :ref:`MSDF font rendering <doc_using_fonts_msdf>` thay cho rasterization truyền thống.
- **Default Font Generate Mipmaps:** Nếu là ``true``, bật việc
  :ref:`mipmap <doc_using_fonts_mipmaps>` được tạo và sử dụng cho font mặc định của dự án.

.. note::

    Các cài đặt dự án này *chỉ* ảnh hưởng đến font mặc định của dự án (font được hardcode trong binary của engine).

    Các thuộc tính của font tùy chỉnh được kiểm soát bởi các tùy chọn import tương ứng của chúng. Bạn có thể sử dụng phần **Import Defaults** trong hộp thoại Project Settings để ghi đè các tùy chọn import mặc định cho font tùy chỉnh.
