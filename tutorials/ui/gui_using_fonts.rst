.. _doc_gui_using_fonts:

Sử dụng Font
============

Godot cho phép bạn đặt các font cụ thể cho những node UI khác nhau.

Có ba vị trí khác nhau để thiết lập việc sử dụng font. Đầu tiên là trình chỉnh sửa theme. Chọn node mà bạn muốn đặt font rồi chọn tab font. Thứ hai là trong inspector của các control node, tại **Theme Overrides > Fonts**. Cuối cùng là trong phần cài đặt inspector của theme, tại **Default Font**.

Nếu không có font override nào được chỉ định ở bất kỳ đâu, `Open Sans <https://fonts.google.com/specimen/Open+Sans>`__ SemiBold sẽ được sử dụng làm font mặc định của project.

.. note::

    Kể từ Godot 4.0, kích thước font không còn được xác định trong chính font mà được xác định trong node sử dụng font. Việc này được thực hiện trong mục **Theme Overrides > Font Sizes** của inspector.

    Điều này cho phép thay đổi kích thước font mà không cần nhân bản resource font cho từng kích thước font khác nhau.

Có 2 loại file font: *dynamic* (các định dạng TTF/OTF/WOFF/WOFF2) và *bitmap* (định dạng BMFont ``.fnt`` hoặc hình ảnh monospaced). Dynamic font là lựa chọn được sử dụng phổ biến nhất, vì có thể thay đổi kích thước mà vẫn hiển thị sắc nét ở các kích thước lớn hơn. Nhờ bản chất dựa trên vector, chúng cũng có thể chứa nhiều glyph hơn trong khi vẫn giữ kích thước file hợp lý so với bitmap font. Dynamic font cũng hỗ trợ một số tính năng nâng cao mà bitmap font không hỗ trợ, chẳng hạn như *ligature* (nhiều ký tự biến đổi thành một thiết kế khác duy nhất).

.. tip::

    Bạn có thể tìm các file font được cấp phép tự do trên những website như `Google Fonts <https://fonts.google.com/>`__ và `Font Library <https://fontlibrary.org/>`__.

    Font được bảo vệ bởi bản quyền. Hãy kiểm tra kỹ license của font trước khi sử dụng, vì không phải font nào cũng cho phép sử dụng thương mại mà không cần mua license.

.. seealso::

    Bạn có thể xem cách font hoạt động trên thực tế bằng cách sử dụng `BiDI and Font Features demo project <https://github.com/godotengine/godot-demo-projects/tree/master/gui/bidi_and_font_features>`__.

Dynamic font
------------

Godot hỗ trợ các định dạng dynamic font sau:

- TrueType Font hoặc Collection (``.ttf``, ``.ttc``) - OpenType Font hoặc Collection (``.otf``, ``.otc``) - Web Open Font Format 1 (``.woff``) - Web Open Font Format 2 (``.woff2``)

Mặc dù ``.woff`` và đặc biệt là ``.woff2`` thường cho kích thước file nhỏ hơn, không có định dạng font nào "tốt hơn" một cách tuyệt đối. Trong hầu hết tình huống, bạn nên sử dụng định dạng font được cung cấp trên website của nhà phát triển font.

Bitmap font
-----------

Godot hỗ trợ định dạng bitmap font BMFont (``.fnt``). Đây là định dạng được tạo bởi chương trình `BMFont <https://www.angelcode.com/products/bmfont/>`__. Ngoài ra còn có nhiều chương trình tương thích với BMFont, chẳng hạn như `BMGlyph <https://www.bmglyph.com/>`__ hoặc `fontcutter <https://github.com/fabienbk/fontcutter>`__ trên nền web.

Ngoài ra, bạn có thể import bất kỳ hình ảnh nào để sử dụng làm bitmap font. Để thực hiện việc này, chọn hình ảnh trong dock FileSystem, chuyển đến dock Import, đổi loại import thành **Font Data (Image Font)** rồi nhấp vào **Reimport**:

.. figure:: img/using_fonts_bitmap_font_from_image_import_options.webp
   :align: center
   :alt: Changing import type to Font Data (Image Font)

   Changing import type to **Font Data (Image Font)**

Bố cục bộ ký tự của font có thể theo bất kỳ thứ tự nào, nhưng nên sử dụng thứ tự khớp với Unicode tiêu chuẩn vì sẽ cần ít cấu hình hơn nhiều khi import. Ví dụ, bitmap font bên dưới chứa các ký tự `ASCII <https://en.wikipedia.org/wiki/ASCII>`__ và tuân theo thứ tự ASCII tiêu chuẩn:

.. figure:: img/using_fonts_monospace_bitmap_font_example.webp
   :align: center
   :alt: Bitmap font example

   Credit: `LibreQuake <https://github.com/MissLav/LibreQuake/blob/master/lq1/gfx-wad/CONCHARS.png>`__
   (scaled and cropped to exclude extended range)

Có thể sử dụng các tùy chọn import sau để import thành công hình ảnh font ở trên:

.. figure:: img/using_fonts_bitmap_font_from_image_example_configuration.webp
   :align: center
   :alt: Import options to use for the above example font

   Import options to use for the above example font

Tùy chọn **Character Ranges** là một mảng ánh xạ từng vị trí trên hình ảnh (theo tọa độ tile, không phải pixel). Font atlas được duyệt từ trái sang phải và từ trên xuống dưới. Có thể chỉ định ký tự bằng số thập phân (``127``), số thập lục phân (``0x007f``) hoặc đặt giữa dấu *nháy đơn* (``'~'``). Có thể chỉ định phạm vi bằng dấu gạch nối giữa các ký tự.

Ví dụ, ``0-127`` (hoặc ``0x0000-0x007f``) biểu thị toàn bộ phạm vi ASCII. Một ví dụ khác, ``' '-'~'`` tương đương với ``32-127`` và biểu thị phạm vi các ký tự ASCII *có thể in* (hiển thị được).

Hãy đảm bảo tùy chọn **Character Ranges** không vượt quá số lượng **Columns** × **Rows** đã xác định. Nếu không, font sẽ không import được.

Nếu hình ảnh font của bạn chứa các phần lề không được sử dụng cho glyph font (chẳng hạn như thông tin ghi công), hãy thử điều chỉnh **Image Margin**. Đây là phần lề chỉ được áp dụng một lần quanh toàn bộ hình ảnh.

Nếu hình ảnh font của bạn chứa các đường căn chỉnh (dưới dạng các đường giữa những glyph) hoặc khoảng cách giữa các ký tự có vẻ không chính xác, hãy thử điều chỉnh **Character Margin**. Phần lề này được áp dụng cho từng glyph được import.

Nếu cần kiểm soát khoảng cách giữa các ký tự chi tiết hơn so với những gì các tùy chọn **Character Margin** cung cấp, bạn có thêm các lựa chọn khác.

Trước hết, **Character Ranges** hỗ trợ thêm 3 đối số sau phạm vi ký tự đã chỉ định. Các đối số bổ sung này kiểm soát vị trí và khoảng cách của chúng. Theo thứ tự, chúng biểu thị độ tiến của khoảng trắng, độ lệch trên trục X và độ lệch trên trục Y. Chúng sẽ thay đổi độ tiến của khoảng trắng và độ lệch của từng ký tự theo số pixel được ghi. Độ tiến của khoảng trắng hữu ích nhất khi, chẳng hạn, các chữ cái thường của bạn mảnh hơn các chữ cái hoa.

.. figure:: img/using_fonts_bitmap_font_advance_offsets_diagram.webp
   :align: center
   :alt: Diagram showing the advance and offset values being used in character ranges.

   Do note that the offsets can cause your text to be cropped off the edge of your label boundaries.

Thứ hai, bạn cũng có thể thiết lập **Kerning Pairs** cho từng ký tự. Chỉ định cặp kerning bằng cách nhập hai tập hợp ký tự cách nhau bởi một khoảng trắng, sau đó thêm một khoảng trắng khác và một số để chỉ định số pixel cộng thêm/bớt đi giữa hai tập hợp ký tự đó khi chúng được đặt cạnh nhau.

.. figure:: img/using_fonts_bitmap_kerning_pairs_example.webp

Nếu cần, có thể chỉ định các ký tự trong cặp kerning bằng mã ký tự Unicode bằng cách nhập ``\uXXXX`` trong đó XXXX là giá trị thập lục phân của ký tự Unicode.

Tải file font
-------------

Để tải file font (dynamic hoặc bitmap), sử dụng tùy chọn **Quick Load** hoặc **Load** trong menu thả xuống resource bên cạnh thuộc tính font, sau đó điều hướng đến file font cần dùng:

.. figure:: img/using_fonts_load_font.webp
   :align: center

   Loading a font file

Bạn cũng có thể kéo và thả file font từ dock FileSystem vào thuộc tính inspector chấp nhận resource Font.

.. warning::

   Trong Godot 4.0 trở lên, các thuộc tính texture filter và repeat được xác định tại vị trí texture được sử dụng, thay vì trên chính texture. Điều này cũng áp dụng cho font (cả dynamic font và bitmap font).

   Các font có hình thức pixel art nên tắt bộ lọc bilinear bằng cách đổi thiết lập project **Rendering > Textures > Canvas Textures > Default Texture Filter** thành **Nearest**.

   Kích thước font cũng phải là bội số nguyên của kích thước thiết kế (thay đổi tùy theo từng font), đồng thời Control node sử dụng font cũng phải được scale theo một bội số nguyên. Nếu không, font có thể bị mờ. Kích thước font trong Godot được chỉ định theo pixel (px), không phải point (pt). Hãy lưu ý điều này khi so sánh kích thước font giữa các phần mềm khác nhau.

   Chế độ texture filter cũng có thể được đặt trên từng node kế thừa từ CanvasItem bằng cách đặt :ref:`CanvasItem.texture_filter <class_CanvasItem_property_texture_filter>`.

Viền và bóng của font
---------------------

Có thể sử dụng viền và bóng của font để cải thiện khả năng đọc khi màu nền chưa được biết trước. Ví dụ, trường hợp này xảy ra với các phần tử HUD được vẽ chồng lên scene 2D/3D.

Viền font khả dụng trong hầu hết các node kế thừa từ Control, ngoài :ref:`class_Label3D`.

Để bật viền cho font trên một node cụ thể, hãy cấu hình các theme override **Font Outline Color** và **Outline Size** trong inspector. Kết quả sẽ trông như sau:

.. figure:: img/using_fonts_outline_example.webp
   :align: center
   :alt: Font outline example

   Font outline example

.. note::

   Nếu sử dụng font với MSDF rendering, tùy chọn import **MSDF Pixel Range** phải được đặt ít nhất bằng *hai lần* giá trị của kích thước viền để việc render viền hiển thị chính xác. Nếu không, viền có thể bị cắt sớm hơn dự kiến.

Khả năng hỗ trợ bóng font hạn chế hơn: chúng chỉ khả dụng trong
:ref:`class_Label` and :ref:`class_RichTextLabel`. Additionally, font shadows
luôn có cạnh cứng (nhưng bạn có thể giảm độ mờ để khiến chúng trông nhẹ hơn). Để bật bóng font trên một node cụ thể, hãy cấu hình các theme override **Font Shadow Color**, **Shadow Offset X** và **Shadow Offset Y** tương ứng trong node Label hoặc RichTextLabel:

.. figure:: img/using_fonts_shadow.webp
   :align: center
   :alt: Configuring font shadow in a Label node

   Configuring font shadow in a Label node

Kết quả sẽ trông như sau:

.. figure:: img/using_fonts_shadow_example.webp
   :align: center
   :alt: Font shadow example

   Font shadow example

.. tip::

    Bạn có thể tạo các override cục bộ cho cách hiển thị font trong các node Label bằng cách tạo một
    :ref:`class_LabelSettings` resource that you reuse across Label nodes. This
    resource được ưu tiên hơn :ref:`theme properties <doc_gui_skinning>`.

Tính năng font nâng cao
-----------------------

.. _doc_using_fonts_antialiasing:

Antialiasing
~~~~~~~~~~~~

Bạn có thể điều chỉnh cách làm mượt font khi render bằng cách điều chỉnh *antialiasing* và *hinting*. Đây là các thuộc tính khác nhau, với những trường hợp sử dụng khác nhau.

Antialiasing kiểm soát cách làm mượt các cạnh glyph khi rasterize font. Phương pháp antialiasing mặc định (**Grayscale**) hoạt động tốt trên mọi công nghệ màn hình. Tuy nhiên, ở kích thước nhỏ, antialiasing grayscale có thể khiến font trông bị mờ.

Có thể cải thiện độ sắc nét của antialiasing bằng cách sử dụng tối ưu hóa subpixel LCD, tận dụng các mẫu subpixel của hầu hết màn hình LCD bằng cách offset antialiasing của font theo từng channel (đỏ/xanh lá/xanh dương). Nhược điểm là điều này có thể tạo ra hiện tượng "fringing" ở các cạnh, đặc biệt trên những công nghệ màn hình không sử dụng subpixel RGB tiêu chuẩn (chẳng hạn như màn hình OLED).

Trong hầu hết game, nên giữ antialiasing mặc định **Grayscale**. Đối với các ứng dụng không phải game, tối ưu hóa subpixel LCD là một lựa chọn đáng để thử nghiệm.

.. figure:: img/using_fonts_antialiasing_comparison.webp
   :align: center
   :alt: Font antialiasing comparison

   From top to bottom: Disabled, Grayscale, LCD Subpixel (RGB)

.. note::

    Không thể thay đổi antialiasing trên :ref:`MSDF-rendered fonts <doc_using_fonts_msdf>` – chúng luôn được render bằng antialiasing grayscale.

.. _doc_using_fonts_hinting:

Hinting
~~~~~~~

Hinting kiểm soát mức độ tích cực của việc căn các cạnh glyph theo pixel khi rasterize font. **None** cho kết quả hiển thị mượt nhất, nhưng có thể khiến font trông mờ ở kích thước nhỏ. **Light** (mặc định) sắc nét hơn bằng cách chỉ căn các cạnh glyph theo pixel trên trục Y, còn **Full** thậm chí sắc nét hơn bằng cách căn các cạnh glyph theo pixel trên cả trục X và Y. Tùy theo sở thích cá nhân, bạn có thể thích sử dụng một chế độ hinting hơn chế độ kia.

.. figure:: img/using_fonts_hinting_comparison.webp
   :align: center
   :alt: Font hinting comparison

   From top to bottom: None, Light, Full hinting

.. note::

    Nếu việc thay đổi chế độ hinting không tạo ra hiệu ứng trực quan nào sau khi nhấp vào **Reimport**, nguyên nhân thường là font không chứa các instruction hinting. Bạn có thể khắc phục bằng cách tìm một phiên bản của file font có chứa các instruction hinting, hoặc bật **Force Autohinter** trong Import dock. Tùy chọn này sẽ sử dụng autohinter của `FreeType <https://freetype.org/>`__ để tự động thêm các instruction hinting vào font đã import.

.. _doc_using_fonts_subpixel_positioning:

Định vị subpixel
~~~~~~~~~~~~~~~~

Có thể điều chỉnh định vị subpixel. Đây là một tính năng `FreeType <https://freetype.org/>`__ cho phép render glyph gần hơn với hình dạng dự kiến. Thiết lập mặc định **Auto** sẽ tự động bật định vị subpixel ở các kích thước nhỏ, nhưng tắt tính năng này ở các kích thước font lớn để cải thiện hiệu năng rasterization.

Bạn có thể buộc chế độ định vị subpixel thành **Disabled**, **One half of a pixel** hoặc **One quarter of a pixel**. **One quarter of a pixel** mang lại chất lượng tốt nhất, nhưng thời gian rasterization sẽ lâu hơn.

Việc thay đổi antialiasing, hinting và định vị subpixel có ảnh hưởng trực quan rõ nhất ở các kích thước font nhỏ.

.. warning::

   Các font có giao diện pixel art nên đặt chế độ định vị subpixel thành **Disabled**. Nếu không, font có thể trông như có các kích thước pixel không đồng đều.

   Bước này không bắt buộc đối với bitmap font, vì định vị subpixel chỉ liên quan đến dynamic font (thường được tạo thành từ các phần tử vector).

.. _doc_using_fonts_mipmaps:

Mipmaps
~~~~~~~

Theo mặc định, font không được tạo mipmaps nhằm giảm mức sử dụng bộ nhớ và tăng tốc rasterization. Tuy nhiên, điều này có thể khiến font được thu nhỏ trở nên nhiễu hạt. Hiện tượng này có thể đặc biệt dễ nhận thấy với :ref:`doc_3d_text` không bật **Fixed Size**. Hiện tượng tương tự cũng có thể xảy ra khi hiển thị văn bản bằng font rasterized truyền thống (không phải :ref:`MSDF <doc_using_fonts_msdf>`) trong một Control node có scale thấp hơn ``(1, 1)``.

Sau khi chọn một font trong FileSystem dock, bạn có thể bật **Mipmaps** trong Import dock để cải thiện giao diện hiển thị của font được thu nhỏ.

Bạn cũng có thể bật mipmaps cho MSDF font. Điều này có thể cải thiện một chút chất lượng hiển thị font ở các kích thước nhỏ hơn mặc định, nhưng MSDF font vốn đã chống nhiễu hạt tốt.

.. _doc_using_fonts_msdf:

Render font MSDF
~~~~~~~~~~~~~~~~

Render font bằng multi-channel signed distance field (MSDF) cho phép render font ở mọi kích thước mà không cần rasterize lại khi kích thước thay đổi.

Render font MSDF có 2 ưu điểm so với rasterization font truyền thống, vốn được Godot sử dụng theo mặc định:

- Font sẽ luôn trông sắc nét, ngay cả ở các kích thước rất lớn. - Ít bị giật hơn khi lần đầu render các ký tự *ở kích thước font lớn*, vì không thực hiện rasterization.

Nhược điểm của render font MSDF là:

- Chi phí cơ bản cho việc render font cao hơn. Điều này thường không đáng kể trên các nền tảng desktop, nhưng có thể ảnh hưởng đến các thiết bị di động cấu hình thấp. - Font ở các kích thước nhỏ sẽ không rõ bằng font được rasterize, do thiếu hinting. - Việc render các glyph mới lần đầu *ở kích thước font nhỏ* có thể tốn kém hơn so với font được rasterize truyền thống.
  :ref:`doc_using_fonts_font_prerendering` can be used to alleviate this.
- Không thể bật tối ưu hóa subpixel LCD cho MSDF font. - Font có outline tự giao nhau sẽ không render chính xác ở chế độ MSDF. Nếu nhận thấy vấn đề khi render các font tải xuống từ những website như `Google Fonts <https://fonts.google.com>`__, hãy thử tải font từ website chính thức của tác giả font.

.. figure:: img/using_fonts_rasterized_vs_msdf_comparison.webp
   :align: center
   :alt: Comparison of font rasterization methods

   Comparison of font rasterization methods.
   From top to bottom: rasterized without oversampling, rasterized with oversampling, MSDF

Để bật MSDF rendering cho một font cụ thể, hãy chọn font đó trong FileSystem dock, chuyển đến Import dock, bật **Multichannel Signed Distance Field**, sau đó nhấp vào **Reimport**:

.. figure:: img/using_fonts_msdf_import_options.webp
   :align: center
   :alt: Enabling MSDF in the font's import options

   Enabling MSDF in the font's import options

.. _doc_using_fonts_emoji:

Sử dụng emoji
~~~~~~~~~~~~~

Godot hỗ trợ emoji font ở mức hạn chế:

- CBDT/CBLC (PNG được nhúng) và SVG emoji font được hỗ trợ. - COLR/CPAL emoji font (định dạng vector tùy chỉnh) **không** được hỗ trợ. - EMJC bitmap image compression (được iOS' system emoji font sử dụng) **không** được hỗ trợ. Điều này có nghĩa là để hỗ trợ emoji trên iOS, bạn phải sử dụng font tùy chỉnh dùng SVG hoặc PNG bitmap compression.

Để Godot có thể hiển thị emoji, font được sử dụng (hoặc một trong các
:ref:`fallbacks <doc_using_fonts_font_fallbacks>`) needs to include them.
Nếu không, emoji sẽ không được hiển thị và thay vào đó sẽ xuất hiện các ký tự giữ chỗ "tofu":

.. figure:: img/using_fonts_emoji_placeholder_characters.webp
   :align: center
   :alt: Default appearance when trying to use emoji in a label

   Default appearance when trying to use emoji in a label

Sau khi thêm một font để hiển thị emoji như `Noto Color Emoji <https://fonts.google.com/noto/specimen/Noto+Color+Emoji>`__, bạn sẽ nhận được kết quả như mong đợi:

.. figure:: img/using_fonts_emoji_correct_characters.webp
   :align: center
   :alt: Correct appearance after adding an emoji font to the label

   Correct appearance after adding an emoji font to the label

Để sử dụng font thông thường cùng với emoji, bạn nên chỉ định một
:ref:`fallback font <doc_using_fonts_font_fallbacks>` that points to the
emoji font trong các tùy chọn import nâng cao của font thông thường. Nếu muốn sử dụng font mặc định của project trong khi hiển thị emoji, hãy để trống thuộc tính **Base Font** trong FontVariation khi thêm một font fallback trỏ đến emoji font:

.. tip::

    Emoji font có kích thước khá lớn, vì vậy bạn có thể muốn :ref:`load a system font <doc_using_fonts_system_fonts>` để cung cấp các glyph emoji thay vì đóng gói font cùng project. Điều này cho phép cung cấp đầy đủ hỗ trợ emoji trong project mà không làm tăng kích thước PCK được export. Nhược điểm là emoji sẽ trông khác nhau tùy theo nền tảng, và việc load system font không được hỗ trợ trên mọi nền tảng.

    Bạn cũng có thể sử dụng system font làm fallback font.

Sử dụng icon font
~~~~~~~~~~~~~~~~~

Các công cụ như `Fontello <https://fontello.com/>`__ có thể được sử dụng để tạo các file font chứa vector được import từ file SVG. Bạn có thể dùng cách này để render các phần tử vector tùy chỉnh như một phần của văn bản, hoặc tạo các icon 3D đùn với :ref:`doc_3d_text` và TextMesh.

.. note::

    Hiện tại Fontello không hỗ trợ tạo font nhiều màu (loại font mà Godot có thể render). Tính đến tháng 11 năm 2022, hỗ trợ font nhiều màu trong các công cụ tạo icon font vẫn còn rất hạn chế.

Tùy theo trường hợp sử dụng, cách này có thể mang lại kết quả tốt hơn so với việc sử dụng tag ``img`` trong :ref:`RichTextLabel <doc_bbcode_in_richtextlabel>`. Không giống như bitmap image (bao gồm SVG được Godot rasterize khi import), dữ liệu vector thực có thể được thay đổi kích thước đến bất kỳ kích thước nào mà không làm giảm chất lượng.

Sau khi tải xuống file font đã tạo, hãy load file đó vào project Godot, sau đó chỉ định nó làm custom font cho một node Label, RichTextLabel hoặc Label3D. Chuyển sang giao diện web Fontello, rồi sao chép ký tự bằng cách chọn ký tự đó và nhấn :kbd:`Ctrl + C` (:kbd:`Cmd + C` trên macOS). Dán ký tự vào thuộc tính **Text** của node Label. Ký tự sẽ xuất hiện dưới dạng glyph giữ chỗ trong inspector, nhưng sẽ hiển thị chính xác trong viewport 2D/3D.

Để sử dụng icon font cùng với font truyền thống trong cùng một Control, bạn có thể chỉ định icon font làm :ref:`fallback <doc_using_fonts_font_fallbacks>`. Cách này hoạt động vì icon font sử dụng *private use area* của Unicode, khu vực được dành riêng cho font tùy chỉnh và vốn không chứa các glyph tiêu chuẩn.

.. note::

    Một số icon font hiện đại như `Font Awesome 6 <https://fontawesome.com/download>`__ có một biến thể desktop sử dụng *ligature* để chỉ định icon. Điều này cho phép bạn chỉ định icon bằng cách nhập trực tiếp tên của chúng vào thuộc tính **Text** của bất kỳ node nào có thể hiển thị font. Khi nhập đầy đủ tên của icon dưới dạng văn bản (chẳng hạn như ``house``), tên đó sẽ được thay thế bằng icon.

    Mặc dù dễ sử dụng hơn, cách tiếp cận này không thể dùng với font fallback, vì các ký tự của font chính sẽ được ưu tiên hơn ligature của font fallback.

.. _doc_using_fonts_font_fallbacks:

Font fallback
~~~~~~~~~~~~~

Godot hỗ trợ định nghĩa một hoặc nhiều fallback khi font chính không có glyph cần hiển thị. Có 2 trường hợp sử dụng chính để định nghĩa font fallback:

- Sử dụng một font chỉ hỗ trợ các bộ ký tự Latin, nhưng dùng một font khác để có thể hiển thị văn bản thuộc bộ ký tự khác, chẳng hạn như Cyrillic. - Sử dụng một font để render văn bản và một font khác để render emoji hoặc icon.

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào file font trong FileSystem dock. Bạn cũng có thể chọn font trong FileSystem dock, chuyển đến Import dock rồi chọn **Advanced…** ở phía dưới:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   Import dock

Trong hộp thoại xuất hiện, tìm phần **Fallbacks** trên thanh bên ở bên phải, nhấp vào dòng **Array[Font] (size 0)** để mở rộng thuộc tính, sau đó nhấp vào **Add Element**:

.. figure:: img/using_fonts_font_fallbacks_add.webp
   :align: center

   Adding font fallback

Nhấp vào mũi tên dropdown trên phần tử mới, sau đó chọn một file font bằng tùy chọn **Quick Load** hoặc **Load**:

.. figure:: img/using_fonts_font_fallbacks_load.webp
   :align: center

   Loading font fallback

Bạn có thể thêm font fallback khi sử dụng font mặc định của project. Để thực hiện việc này, hãy để trống thuộc tính **Base Font** trong khi thêm một hoặc nhiều font fallback.

.. note::

    Font fallback cũng có thể được định nghĩa ở cấp cục bộ, tương tự như
    :ref:`doc_using_fonts_opentype_font_features`, but this is not covered here
    vì lý do ngắn gọn.

.. _doc_using_fonts_variable_fonts:

Variable font
~~~~~~~~~~~~~

Godot hỗ trợ đầy đủ `variable fonts <https://variablefonts.io/>`__, cho phép bạn sử dụng một file font duy nhất để biểu diễn nhiều độ đậm và kiểu font khác nhau (regular, bold, italic, …). File font bạn đang sử dụng phải hỗ trợ tính năng này.

Để sử dụng variable font, hãy tạo một resource :ref:`class_FontVariation` tại vị trí bạn dự định sử dụng font, sau đó load một file font bên trong resource FontVariation:

.. figure:: img/using_fonts_font_variation_create.webp
   :align: center

   Creating a FontVariation resource

.. figure:: img/using_fonts_font_variation_load.webp
   :align: center

   Loading a font file into the FontVariation resource

Cuộn xuống phần **Variation** của FontVariation, sau đó nhấp vào dòng chữ **Variation Coordinates** để mở rộng danh sách các trục có thể điều chỉnh:

.. figure:: img/using_fonts_font_variation_variable_font.webp
   :align: center

   List of variation axes

Tập hợp các trục bạn có thể điều chỉnh phụ thuộc vào font đã tải. Một số variable font chỉ hỗ trợ một trục điều chỉnh (thường là *weight* hoặc *slant*), trong khi những font khác có thể hỗ trợ nhiều trục điều chỉnh.

Ví dụ: đây là font `Inter V <https://rsms.me/inter/>`__ với *weight* là ``900`` và *slant* là ``-10``:

.. figure:: img/using_fonts_font_variation_variable_font_example.webp
   :align: center

   Variable font example (Inter V)

.. tip::

    Mặc dù tên và thang đo của các trục variable font chưa được chuẩn hóa, một số quy ước phổ biến thường được các nhà thiết kế font tuân theo. Trục *weight* được chuẩn hóa trong OpenType để hoạt động như sau:

    +------------+--------------------------------+
    | Axis value | Effective font weight          |
    +============+================================+
    | ``100``    | Thin (Hairline)                |
    +------------+--------------------------------+
    | ``200``    | Extra Light (Ultra Light)      |
    +------------+--------------------------------+
    | ``300``    | Light                          |
    +------------+--------------------------------+
    | ``400``    | **Regular (Normal)**           |
    +------------+--------------------------------+
    | ``500``    | Medium                         |
    +------------+--------------------------------+
    | ``600``    | Semi-Bold (Demi-Bold)          |
    +------------+--------------------------------+
    | ``700``    | **Bold**                       |
    +------------+--------------------------------+
    | ``800``    | Extra Bold (Ultra Bold)        |
    +------------+--------------------------------+
    | ``900``    | Black (Heavy)                  |
    +------------+--------------------------------+
    | ``950``    | Extra Black (Ultra Black)      |
    +------------+--------------------------------+

Bạn có thể lưu FontVariation vào một file resource ``.tres`` để sử dụng lại ở những nơi khác:

.. figure:: img/using_fonts_font_variation_save_to_file.webp
   :align: center

   Saving FontVariation to an external resource file

Bold và italic giả lập
~~~~~~~~~~~~~~~~~~~~~~

Khi viết văn bản in đậm hoặc in nghiêng, sử dụng các font variant được thiết kế riêng cho mục đích này sẽ cho kết quả đẹp hơn. Khoảng cách giữa các glyph sẽ nhất quán hơn khi sử dụng font bold, và hình dạng của một số glyph có thể thay đổi hoàn toàn trong các variant italic (hãy so sánh "a" và *"a"*).

Tuy nhiên, các font bold và italic thực sự yêu cầu phân phối thêm nhiều file font, làm tăng kích thước bản phân phối. Cũng có thể sử dụng một file :ref:`variable font <doc_using_fonts_variable_fonts>`, nhưng file này sẽ lớn hơn một font không biến thiên đơn lẻ. Mặc dù kích thước file thường không phải vấn đề đối với các project desktop, đây có thể là mối quan tâm đối với các project mobile/web cần giữ kích thước bản phân phối ở mức thấp nhất có thể.

Để cho phép hiển thị font bold và italic mà không cần phân phối thêm font (hoặc sử dụng variable font có kích thước lớn hơn), Godot hỗ trợ bold và italic *giả lập*.

.. figure:: img/using_fonts_faux_bold_italic_vs_real_bold_italic.webp
   :align: center
   :alt: Faux bold/italic (top), real bold/italic (bottom). Normal font used: Open Sans SemiBold

   Faux bold/italic (top), real bold/italic (bottom). Normal font used: Open Sans SemiBold

Bold và italic giả lập được tự động sử dụng trong các tag bold và italic của :ref:`class_RichTextLabel` nếu không cung cấp font tùy chỉnh cho bold và/hoặc italic.

Để sử dụng bold giả lập, hãy tạo một resource FontVariation trong thuộc tính yêu cầu một resource Font. Đặt **Variation > Embolden** thành giá trị dương để làm font đậm hơn, hoặc giá trị âm để làm font bớt đậm. Các giá trị được khuyến nghị nằm trong khoảng từ ``0.5`` đến ``1.2``, tùy thuộc vào font.

Italic giả lập được tạo bằng cách làm nghiêng văn bản, thông qua việc sửa đổi phép biến đổi của từng ký tự. Tính năng này cũng được cung cấp trong FontVariation thông qua thuộc tính **Variation > Transform**. Đặt component ``yx`` của phép biến đổi ký tự thành giá trị dương sẽ làm văn bản in nghiêng. Các giá trị được khuyến nghị nằm trong khoảng từ ``0.2`` đến ``0.4``, tùy thuộc vào font.

Điều chỉnh khoảng cách của font
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vì mục đích tạo kiểu hoặc để dễ đọc hơn, bạn có thể muốn điều chỉnh cách một font được hiển thị trong Godot.

Hãy tạo một resource FontVariation trong thuộc tính yêu cầu một resource Font. Có 4 thuộc tính trong phần **Variation > Extra Spacing**, chấp nhận các giá trị dương và âm:

- **Glyph:** Khoảng cách bổ sung giữa mỗi glyph. - **Space:** Khoảng cách bổ sung giữa các từ. - **Top:** Khoảng cách bổ sung phía trên glyph. Khoảng cách này được sử dụng cho văn bản nhiều dòng, đồng thời để tính kích thước tối thiểu của các control như :ref:`class_Label` và :ref:`class_Button`. - **Bottom:** Khoảng cách bổ sung phía dưới glyph. Khoảng cách này được sử dụng cho văn bản nhiều dòng, đồng thời để tính kích thước tối thiểu của các control như :ref:`class_Label` và :ref:`class_Button`.

Bạn cũng có thể điều chỉnh thuộc tính **Variation > Transform** để kéo giãn các ký tự theo chiều ngang hoặc chiều dọc. Cụ thể, hãy điều chỉnh các component ``xx`` (tỉ lệ theo chiều ngang) và ``yy`` (tỉ lệ theo chiều dọc). Hãy nhớ điều chỉnh khoảng cách glyph để bù cho mọi thay đổi, vì phép biến đổi glyph không ảnh hưởng đến lượng không gian mà mỗi glyph chiếm trong văn bản. Nên hạn chế sử dụng kiểu scaling không đồng đều này, vì font thường không được thiết kế để hiển thị dưới dạng bị kéo giãn.

.. _doc_using_fonts_opentype_font_features:

Các tính năng của font OpenType
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot hỗ trợ bật các tính năng của font OpenType, đây là một cách được chuẩn hóa để xác định các ký tự thay thế có thể bật mà không cần thay hoàn toàn file font. Mặc dù được gọi là các tính năng của font OpenType, chúng cũng được hỗ trợ trong các file TrueType (``.ttf``) và WOFF/WOFF2.

Mức độ hỗ trợ các tính năng OpenType phụ thuộc rất nhiều vào font được sử dụng. Một số font không hỗ trợ bất kỳ tính năng OpenType nào, trong khi các font khác có thể hỗ trợ hàng chục tính năng có thể bật/tắt.

Có 2 cách sử dụng các tính năng của font OpenType:

**Trên toàn bộ file font**

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào file font trong dock FileSystem. Bạn cũng có thể chọn font trong dock FileSystem, chuyển đến dock Import rồi chọn **Advanced…** ở phía dưới:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   Import dock

Trong hộp thoại xuất hiện, tìm phần **Metadata Overrides > OpenType Features** trên thanh bên phải, nhấp vào dòng chữ **Features (0 of N set)** để mở rộng thuộc tính, sau đó nhấp vào **Add Feature**:

.. figure:: img/using_fonts_advanced_import_settings_opentype_features.webp
   :align: center

   OpenType feature overrides in Advanced Import Settings

**Trong một trường hợp sử dụng font cụ thể (FontVariation)**

Để sử dụng một tính năng của font, hãy tạo một resource FontVariation như cách bạn tạo một
:ref:`variable font <doc_using_fonts_variable_fonts>`, then load a font file
trong resource FontVariation:

.. figure:: img/using_fonts_font_variation_create.webp
   :align: center

   Creating a FontVariation resource

.. figure:: img/using_fonts_font_variation_load.webp
   :align: center

   Loading a font file into a FontVariation resource

Cuộn xuống phần **OpenType Features** của FontVariation, nhấp vào dòng chữ **Features (0 of N set)** để mở rộng thuộc tính, sau đó nhấp vào **Add Feature** và chọn tính năng mong muốn trong danh sách thả xuống:

.. figure:: img/using_fonts_font_variation_opentype_features.webp
   :align: center

   Specifying OpenType features in a FontVariation resource

Ví dụ: đây là font `Inter <https://rsms.me/inter/>`__ không bật tính năng *Slashed Zero* (ở trên), sau đó bật tính năng OpenType *Slashed Zero* (ở dưới):

.. figure:: img/using_fonts_font_variation_slashed_zero.webp
   :align: center

   OpenType feature comparison (Inter)

Bạn có thể tắt ligature và/hoặc kerning cho một font cụ thể bằng cách thêm các tính năng OpenType, sau đó bỏ chọn chúng trong inspector:

.. figure:: img/using_fonts_font_variation_disable_ligatures.webp
   :align: center

   Disabling ligatures and kerning for a font

.. _doc_using_fonts_system_fonts:

Font hệ thống
~~~~~~~~~~~~~

.. warning::

    Chỉ hỗ trợ tải font hệ thống trên Windows, macOS, Linux, Android và iOS.

    Tuy nhiên, việc tải font hệ thống trên Android không đáng tin cậy vì không có API chính thức để thực hiện việc này. Godot phải dựa vào việc phân tích các file cấu hình hệ thống, vốn có thể bị các nhà cung cấp Android bên thứ ba sửa đổi. Điều này có thể khiến việc tải font hệ thống không hoạt động.

Font hệ thống là một loại resource khác so với font đã import. Chúng không bao giờ thực sự được import vào project mà được tải tại runtime. Điều này mang lại 2 lợi ích:

- Font không được đưa vào file PCK đã export, giúp giảm kích thước file của project đã export. - Vì font không được đưa vào project đã export, điều này tránh được các vấn đề về giấy phép có thể phát sinh nếu các font hệ thống độc quyền được phân phối cùng với project.

Engine tự động sử dụng font hệ thống làm font fallback, nhờ đó có thể hiển thị các ký tự CJK và emoji mà không cần tải font tùy chỉnh. Tuy nhiên, có một số hạn chế áp dụng, như đã đề cập trong
:ref:`Using emoji <doc_using_fonts_emoji>` section.

Tạo một resource :ref:`class_SystemFont` tại vị trí bạn muốn sử dụng font hệ thống:

.. figure:: img/using_fonts_system_font_create.webp
   :align: center

   Creating a SystemFont resource

.. figure:: img/using_fonts_system_font_specify.webp
   :align: center

   Specifying a font name to use in a SystemFont resource

Bạn có thể chỉ định rõ một hoặc nhiều tên font (chẳng hạn như ``Arial``), hoặc chỉ định tên của một *alias* font ánh xạ đến một font mặc định "tiêu chuẩn" của hệ thống:

.. Thông tin font Android lấy từ <https://android.googlesource.com/platform/frameworks/base/+/master/data/fonts/fonts.xml>

+----------------+-----------------+----------------+-------------------------+-------------------------+
| Font alias     | Windows         | macOS/iOS      | Linux                   | Android                 |
+================+=================+================+=========================+=========================+
| ``sans-serif`` | Arial           | Helvetica      | *Handled by fontconfig* | Roboto / Noto Sans      |
+----------------+-----------------+----------------+-------------------------+-------------------------+
| ``serif``      | Times New Roman | Times          | *Handled by fontconfig* | Noto Serif              |
+----------------+-----------------+----------------+-------------------------+-------------------------+
| ``monospace``  | Courier New     | Courier        | *Handled by fontconfig* | Droid Sans Mono         |
+----------------+-----------------+----------------+-------------------------+-------------------------+
| ``cursive``    | Comic Sans MS   | Apple Chancery | *Handled by fontconfig* | Dancing Script          |
+----------------+-----------------+----------------+-------------------------+-------------------------+
| ``fantasy``    | Gabriola        | Papyrus        | *Handled by fontconfig* | Droid Sans Mono         |
+----------------+-----------------+----------------+-------------------------+-------------------------+

Trên Android, Roboto được sử dụng cho văn bản Latin/Cyrillic và Noto Sans được sử dụng cho glyph của các ngôn ngữ khác như CJK. Trên các bản phân phối Android của bên thứ ba, font được chọn cụ thể có thể khác.

Nếu chỉ định nhiều font, font đầu tiên được tìm thấy trên hệ thống sẽ được sử dụng (từ trên xuống dưới). Tên font và alias không phân biệt chữ hoa chữ thường trên tất cả các nền tảng.

Giống như với các font variation, bạn có thể lưu cấu hình SystemFont vào một file resource để sử dụng lại ở những nơi khác.

Hãy nhớ rằng các font hệ thống khác nhau có các metric khác nhau, nghĩa là văn bản có thể vừa trong một hình chữ nhật trên nền tảng này nhưng lại không vừa trên nền tảng khác. Trong quá trình phát triển, hãy luôn chừa thêm một khoảng trống để các label có thể mở rộng thêm nếu cần.

.. note::

    Không giống Windows và macOS/iOS, tập hợp font mặc định được cung cấp trên Linux phụ thuộc vào bản phân phối. Điều này có nghĩa là trên các bản phân phối Linux khác nhau, các font khác nhau có thể được hiển thị cho cùng một tên hoặc alias font hệ thống.

Bạn cũng có thể tải font tại runtime ngay cả khi chúng chưa được cài đặt trên hệ thống. Xem :ref:`Runtime loading and saving <doc_runtime_file_loading_and_saving_fonts>` để biết chi tiết.

.. _doc_using_fonts_font_prerendering:

Prerender font
~~~~~~~~~~~~~~

Khi sử dụng font rasterized truyền thống, Godot lưu cache glyph theo từng font và kích thước. Điều này làm giảm hiện tượng giật, nhưng hiện tượng này vẫn có thể xảy ra lần đầu tiên một glyph được hiển thị khi chạy project. Điều này có thể đặc biệt dễ nhận thấy ở kích thước font lớn hơn hoặc trên thiết bị di động.

Khi sử dụng font MSDF, chúng chỉ cần được rasterize một lần vào một texture signed distance field đặc biệt. Điều này có nghĩa là có thể thực hiện caching thuần túy theo từng font mà không cần xét đến kích thước font. Tuy nhiên, lần render đầu tiên của font MSDF chậm hơn so với font rasterized truyền thống ở kích thước trung bình.

Để tránh các vấn đề giật liên quan đến việc render font, bạn có thể *prerender* một số glyph nhất định. Bạn có thể thực hiện việc này cho tất cả glyph dự định sử dụng (để đạt kết quả tối ưu), hoặc chỉ cho các glyph phổ biến có nhiều khả năng xuất hiện trong quá trình chơi game (để giảm kích thước file). Các glyph chưa được prerender sẽ vẫn được rasterize ngay khi cần như bình thường.

.. note::

    Trong cả hai trường hợp (truyền thống và MSDF), việc rasterize font được thực hiện trên CPU. Điều này có nghĩa là hiệu năng GPU không ảnh hưởng đến thời gian rasterize font.

Mở hộp thoại Advanced Import Settings bằng cách nhấp đúp vào tệp font trong FileSystem dock. Bạn cũng có thể chọn font trong FileSystem dock, chuyển đến Import dock rồi chọn **Advanced…** ở dưới cùng:

.. figure:: img/using_fonts_advanced_import_settings.webp
   :align: center

   Import dock

Chuyển đến tab **Pre-render Configurations** của hộp thoại Advanced Import Settings, sau đó thêm một configuration bằng cách nhấp vào biểu tượng "plus":

.. figure:: img/using_fonts_advanced_import_settings_prerender_new_configuration.webp
   :align: center
   :alt: Adding a new prerendering configuration in the Advanced Import Settings dialog

   Adding a new prerendering configuration in the Advanced Import Settings dialog

Sau khi thêm một configuration, hãy đảm bảo configuration đó được chọn bằng cách nhấp một lần vào tên của nó. Bạn cũng có thể đổi tên configuration bằng cách nhấp đúp vào nó.

Có 2 cách để thêm glyph cần được prerender vào một configuration nhất định. Bạn có thể sử dụng cả hai cách theo kiểu cộng dồn:

**Sử dụng văn bản từ bản dịch**

Đối với hầu hết các project, đây là cách thuận tiện nhất, vì nó tự động lấy văn bản từ các bản dịch ngôn ngữ của bạn. Nhược điểm là cách này chỉ có thể được sử dụng nếu project của bạn hỗ trợ
:ref:`internationalization <doc_internationalizing_games>`. Otherwise, stick to
cách tiếp cận "Using custom text" được mô tả bên dưới.

Sau khi thêm các bản dịch vào Project Settings, hãy sử dụng tab **Glyphs from the Translations** để kiểm tra các bản dịch bằng cách nhấp đúp vào chúng, sau đó nhấp vào **Shape All Strings in the Translations and Add Glyphs** ở dưới cùng:

.. figure:: img/using_fonts_advanced_import_settings_prerender_translation.webp
   :align: center
   :alt: Enabling prerendering in the Advanced Import Settings dialog with the Glyphs from the Translations tab

   Enabling prerendering in the Advanced Import Settings dialog with the **Glyphs from the Translations** tab

.. note::

    Danh sách các glyph đã prerender không được tự động cập nhật khi bản dịch thay đổi, vì vậy bạn cần lặp lại quy trình này nếu bản dịch đã thay đổi đáng kể.

**Sử dụng văn bản tùy chỉnh**

Mặc dù yêu cầu chỉ định thủ công văn bản sẽ xuất hiện trong game, đây là cách hiệu quả nhất đối với các game không có chức năng nhập văn bản từ người dùng. Cách này đáng để cân nhắc đối với game mobile nhằm giảm kích thước tệp của app được phân phối.

Để sử dụng văn bản hiện có làm cơ sở cho việc prerender, hãy chuyển đến sub-tab **Glyphs from the Text** của hộp thoại Advanced Import Settings, nhập văn bản vào cửa sổ bên phải, sau đó nhấp vào **Shape Text and Add Glyphs** ở dưới cùng của hộp thoại:

.. figure:: img/using_fonts_advanced_import_settings_prerender_text.webp
   :align: center
   :alt: Enabling prerendering in the Advanced Import Settings dialog, Glyphs from the Text tab

   Enabling prerendering in the Advanced Import Settings dialog with the **Glyphs from the Text** tab

.. tip::

    Nếu project của bạn hỗ trợ :ref:`internationalization <doc_internationalizing_games>`, bạn có thể dán nội dung của các tệp CSV hoặc PO vào ô bên trên để nhanh chóng prerender tất cả ký tự có thể được hiển thị trong quá trình chơi game (không bao gồm các chuỗi do người dùng cung cấp hoặc không cần dịch).

**Bằng cách bật các bộ ký tự**

Phương pháp thứ hai yêu cầu ít cấu hình và ít cập nhật hơn nếu văn bản trong game thay đổi, đồng thời phù hợp hơn với các game nhiều văn bản hoặc game multiplayer có chat. Mặt khác, phương pháp này có thể khiến các glyph không bao giờ xuất hiện trong game vẫn được prerender, kém hiệu quả hơn về kích thước tệp.

Để sử dụng văn bản hiện có làm cơ sở cho việc prerender, hãy chuyển đến sub-tab **Glyphs from the Character Map** của hộp thoại Advanced Import Settings, sau đó *nhấp đúp* vào các bộ ký tự cần bật ở bên phải:

.. figure:: img/using_fonts_advanced_import_settings_prerender_character_map.webp
   :align: center
   :alt: Enabling prerendering in the Advanced Import Settings dialog, Glyphs from the Character Map tab

   Enabling prerendering in the Advanced Import Settings dialog with the **Glyphs from the Character Map** tab

Để đảm bảo prerender đầy đủ, các bộ ký tự bạn cần bật phụ thuộc vào những ngôn ngữ được hỗ trợ trong game. Đối với tiếng Anh, chỉ cần bật **Basic Latin**. Bật thêm **Latin-1 Supplement** sẽ cho phép hỗ trợ đầy đủ nhiều ngôn ngữ hơn, chẳng hạn như tiếng Pháp, tiếng Đức và tiếng Tây Ban Nha. Đối với tiếng Nga, cần bật **Cyrillic**, v.v.

Thuộc tính font mặc định của project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong phần **GUI > Theme** của Project Settings nâng cao, bạn có thể chọn cách font mặc định được render:

- **Default Font Antialiasing:** Kiểm soát
  :ref:`antialiasing <doc_using_fonts_antialiasing>` method used
  cho font mặc định của project. - **Default Font Hinting:** Kiểm soát
  :ref:`hinting <doc_using_fonts_hinting>` method used for
  font mặc định của project. - **Default Font Subpixel Positioning:** Kiểm soát
  :ref:`subpixel positioning <doc_using_fonts_subpixel_positioning>`
  phương pháp cho font mặc định của project. - **Default Font Multichannel Signed Distance Field:** Nếu ``true``, khiến font mặc định của project sử dụng :ref:`MSDF font rendering <doc_using_fonts_msdf>` thay vì rasterization truyền thống. - **Default Font Generate Mipmaps:** Nếu ``true``, bật
  :ref:`mipmap <doc_using_fonts_mipmaps>` generation and
  việc sử dụng đối với font mặc định của project.

.. note::

    Các thiết lập project này *chỉ* ảnh hưởng đến font mặc định của project (font được hardcode trong binary của engine).

    Các thuộc tính của font tùy chỉnh được kiểm soát bởi những tùy chọn import tương ứng của chúng. Bạn có thể sử dụng phần **Import Defaults** trong hộp thoại Project Settings để ghi đè các tùy chọn import mặc định cho font tùy chỉnh.
