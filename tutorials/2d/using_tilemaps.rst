.. _doc_using_tilemaps:

Sử dụng TileMap
===============

.. seealso::

    Trang này giả định rằng bạn đã tạo hoặc tải xuống một TileSet. Nếu chưa, trước tiên hãy đọc :ref:`doc_using_tilesets`, vì bạn sẽ cần một TileSet để tạo TileMap.

Giới thiệu
----------

Tilemap là một lưới các tile được dùng để tạo bố cục của trò chơi. Có một số lợi ích khi sử dụng các node :ref:`TileMapLayer <class_TileMapLayer>` để thiết kế level. Trước tiên, chúng cho phép vẽ bố cục bằng cách "tô" các tile lên lưới, nhanh hơn nhiều so với việc đặt từng node :ref:`Sprite2D <class_Sprite2D>` riêng lẻ. Thứ hai, chúng cho phép tạo các level lớn hơn nhiều vì được tối ưu hóa để vẽ số lượng lớn tile. Cuối cùng, bạn có thể thêm các shape collision, occlusion và navigation vào tile, giúp TileMap có thêm nhiều chức năng hơn.

Chỉ định TileSet trong TileMapLayer
-----------------------------------

Nếu bạn đã làm theo trang trước về :ref:`doc_using_tilesets`, bạn sẽ có một resource TileSet được tích hợp trong node TileMapLayer. Điều này phù hợp cho việc tạo prototype, nhưng trong một dự án thực tế, bạn thường sẽ có nhiều level dùng lại cùng một tileset.

Cách được khuyến nghị để dùng lại cùng một TileSet trong nhiều node TileMapLayer là lưu TileSet thành một external resource. Để thực hiện việc này, hãy nhấp vào danh sách thả xuống bên cạnh resource TileSet và chọn **Save**:

.. figure:: img/using_tilemaps_save_tileset_to_resource.webp
   :align: center
   :alt: Lưu resource TileSet tích hợp thành một tệp resource bên ngoài

   Lưu resource TileSet tích hợp thành một tệp resource bên ngoài

Nhiều TileMapLayer và các thiết lập
-----------------------------------

Khi làm việc với tilemap, bạn thường được khuyến nghị sử dụng nhiều node TileMapLayer khi phù hợp. Việc sử dụng nhiều layer có thể mang lại lợi ích; chẳng hạn, điều này cho phép bạn phân biệt các tile tiền cảnh với các tile hậu cảnh để tổ chức tốt hơn. Bạn có thể đặt một tile trên mỗi layer tại một vị trí nhất định, cho phép chồng nhiều tile lên nhau nếu bạn có nhiều hơn một layer.

Mỗi node TileMapLayer có một số thuộc tính mà bạn có thể điều chỉnh:

- **Enabled:** Nếu ``true``, layer sẽ hiển thị trong editor và khi chạy dự án.
- **TileSet** Tileset được node TileMapLayer sử dụng.

Kết xuất
~~~~~~~~

- **Y Sort Origin:** Độ lệch theo chiều dọc được sử dụng để sắp xếp theo Y trên mỗi tile (tính bằng pixel). Chỉ có hiệu lực nếu **Y Sort Enabled** trong các thiết lập CanvasItem là ``true``.
- **X Draw Order Reversed** Đảo ngược thứ tự các tile được vẽ trên trục X. Yêu cầu **Y Sort Enabled** trong các thiết lập CanvasItem là ``true``.
- **Rendering Quadrant Size** Một quadrant là một nhóm tile được vẽ cùng nhau trên một CanvasItem duy nhất nhằm mục đích tối ưu hóa. Thiết lập này xác định độ dài cạnh của một hình vuông trong hệ tọa độ của map. Kích thước quadrant không áp dụng cho TileMapLayer được sắp xếp theo Y, vì trong trường hợp đó các tile được nhóm theo vị trí Y.

Vật lý
~~~~~~
- **Collision Enabled** Bật hoặc tắt collision.
- **Use Kinematic Bodies** Khi là true, các shape collision của TileMapLayer sẽ được khởi tạo dưới dạng kinematic body.
- **Collision Visibility Mode** Xác định các shape collision của TileMapLayer có hiển thị hay không. Nếu đặt thành default, điều này phụ thuộc vào các thiết lập gỡ lỗi hiển thị collision.

Navigation
~~~~~~~~~~

- **Navigation Enabled** Xác định các vùng navigation có được bật hay không.
- **Navigation Visible** Xác định các navigation mesh của TileMapLayer có hiển thị hay không. Nếu đặt thành default, điều này phụ thuộc vào các thiết lập gỡ lỗi hiển thị navigation.

.. tip::

    Navigation tích hợp của TileMap có nhiều hạn chế thực tế, dẫn đến hiệu suất tìm đường và chất lượng theo đường đi kém hơn.

    Sau khi thiết kế TileMap, hãy cân nhắc bake nó thành một navigation mesh được tối ưu hóa hơn (và tắt NavigationLayer của TileMap) bằng cách sử dụng :ref:`NavigationRegion2D <class_NavigationRegion2D>` hoặc :ref:`NavigationServer2D <class_NavigationServer2D>`. Xem :ref:`doc_navigation_using_navigationmeshes` để biết thêm thông tin.

.. warning::

    Các navigation mesh 2D không thể được "xếp lớp" hoặc chồng lên nhau như các hình ảnh trực quan hay shape vật lý. Việc cố chồng các navigation mesh trên cùng một navigation map sẽ gây ra lỗi merge và lỗi logic, làm hỏng quá trình tìm đường.

Sắp xếp lại các layer
~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sắp xếp lại các layer bằng cách kéo và thả node của chúng trong tab Scene. Bạn cũng có thể chuyển đổi giữa các node TileMapLayer đang làm việc bằng cách sử dụng các nút ở góc trên bên phải của TileMap editor.

.. note::

    Bạn có thể tạo, đổi tên hoặc sắp xếp lại các layer trong tương lai mà không ảnh hưởng đến các tile hiện có. Tuy nhiên, hãy cẩn thận, vì *removing* một layer cũng sẽ xóa tất cả tile đã được đặt trên layer đó.

Mở TileMap editor
-----------------

Chọn node TileMapLayer, sau đó mở panel TileMap ở dưới cùng của editor:

.. figure:: img/using_tilemaps_open_tilemap_editor.webp
   :align: center
   :alt: Mở panel TileMap ở dưới cùng của editor. Trước tiên phải chọn node TileMapLayer.

   Mở panel TileMap ở dưới cùng của editor. Trước tiên phải chọn node TileMapLayer.

Chọn các tile để sử dụng khi tô
-------------------------------

Trước tiên, nếu bạn đã tạo thêm các layer ở phía trên, hãy đảm bảo đã chọn layer mà bạn muốn tô:

.. figure:: img/using_tilemaps_select_layer.webp
   :align: center
   :alt: Chọn một layer để tô trong TileMap editor

   Chọn một layer để tô trong TileMap editor

.. tip::

    Trong 2D editor, các layer mà bạn hiện không chỉnh sửa trong cùng node TileMapLayer sẽ hiển thị mờ đi khi ở trong TileMap editor. Bạn có thể tắt hành vi này bằng cách nhấp vào biểu tượng bên cạnh menu chọn layer (tooltip **Highlight Selected TileMap Layer**).

Bạn có thể bỏ qua bước trên nếu chưa tạo thêm layer, vì layer đầu tiên sẽ được tự động chọn khi vào TileMap editor.

Trước khi có thể đặt tile trong 2D editor, bạn phải chọn một hoặc nhiều tile trong panel TileMap nằm ở dưới cùng của editor. Để thực hiện việc này, hãy nhấp vào một tile trong panel TileMap hoặc giữ nút chuột để chọn nhiều tile:

.. figure:: img/using_tilemaps_select_single_tile_from_tileset.webp
   :align: center
   :alt: Chọn một tile trong TileMap editor bằng cách nhấp vào tile đó

   Chọn một tile trong TileMap editor bằng cách nhấp vào tile đó

.. tip::

    Giống như trong các trình chỉnh sửa 2D và TileSet, bạn có thể di chuyển trong bảng TileMap bằng nút chuột giữa hoặc nút chuột phải, và phóng to, thu nhỏ bằng con lăn chuột hoặc các nút ở góc trên bên trái.

Bạn cũng có thể giữ :kbd:`Shift` để thêm vào vùng chọn hiện tại. Khi chọn nhiều hơn một tile, nhiều tile sẽ được đặt mỗi khi bạn thực hiện thao tác vẽ. Bạn có thể dùng cách này để vẽ các cấu trúc gồm nhiều tile chỉ bằng một lần nhấp (chẳng hạn như các nền tảng lớn hoặc cây).

Vùng chọn cuối cùng không nhất thiết phải liền nhau: nếu có khoảng trống giữa các tile đã chọn, khoảng trống đó sẽ được giữ nguyên trong mẫu sẽ được vẽ trong trình chỉnh sửa 2D.

.. figure:: img/using_tilemaps_select_multiple_tiles_from_tileset.webp
   :align: center
   :alt: Chọn nhiều tile trong trình chỉnh sửa TileMap bằng cách giữ nút chuột trái

   Chọn nhiều tile trong trình chỉnh sửa TileMap bằng cách giữ nút chuột trái

Nếu bạn đã tạo các tile thay thế trong TileSet, bạn có thể chọn chúng để vẽ ở bên phải các tile cơ sở:

.. figure:: img/using_tilemaps_use_alternative_tile.webp
   :align: center
   :alt: Chọn một tile thay thế trong trình chỉnh sửa TileMap

   Chọn một tile thay thế trong trình chỉnh sửa TileMap

Cuối cùng, nếu bạn đã tạo một *bộ sưu tập cảnh* trong TileSet, bạn có thể đặt các tile cảnh vào TileMap:

.. figure:: img/using_tilemaps_placing_scene_tiles.webp
   :align: center
   :alt: Đặt một tile cảnh chứa hạt bằng trình chỉnh sửa TileMap

   Đặt một tile cảnh chứa hạt bằng trình chỉnh sửa TileMap

Painting modes and tools
------------------------

Bằng thanh công cụ ở đầu trình chỉnh sửa TileMap, bạn có thể chọn giữa nhiều chế độ và công cụ vẽ. Các chế độ này ảnh hưởng đến thao tác khi nhấp trong trình chỉnh sửa 2D, **không phải** chính bảng TileMap.

Từ trái sang phải, các chế độ và công cụ vẽ bạn có thể chọn là:

Selection
~~~~~~~~~

Chọn tile bằng cách nhấp vào một tile, hoặc giữ nút chuột trái để chọn nhiều tile bằng một hình chữ nhật trong trình chỉnh sửa 2D. Lưu ý rằng không thể chọn khoảng trống: nếu bạn tạo vùng chọn hình chữ nhật, chỉ các tile không rỗng mới được chọn.

Để thêm vào vùng chọn hiện tại, hãy giữ :kbd:`Shift` rồi chọn một tile. Để xóa khỏi vùng chọn hiện tại, hãy giữ :kbd:`Ctrl` rồi chọn một tile.

Sau đó, bạn có thể sử dụng vùng chọn trong bất kỳ chế độ vẽ nào khác để nhanh chóng tạo các bản sao của một mẫu đã được đặt sẵn.

Bạn có thể xóa các tile đã chọn khỏi TileMap bằng cách nhấn :kbd:`Del`.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở chế độ Paint bằng cách giữ :kbd:`Ctrl` rồi thực hiện thao tác chọn.

.. tip::

    Bạn có thể sao chép và dán các tile đã được đặt sẵn bằng cách thực hiện thao tác chọn, nhấn :kbd:`Ctrl + C` rồi nhấn :kbd:`Ctrl + V`. Vùng chọn sẽ được dán sau khi nhấp chuột trái. Bạn có thể nhấn
    :kbd:`Ctrl + V` thêm một lần nữa để tiếp tục dán theo cách này. Nhấp chuột phải hoặc nhấn :kbd:`Escape` để hủy thao tác dán.

Paint
~~~~~

Chế độ Paint tiêu chuẩn cho phép bạn đặt các tile bằng cách nhấp hoặc giữ nút chuột trái.

Nếu nhấp chuột phải, tile hiện được chọn sẽ bị xóa khỏi tilemap. Nói cách khác, tile đó sẽ được thay thế bằng khoảng trống.

Nếu bạn đã chọn nhiều tile trong TileMap hoặc bằng công cụ Selection, chúng sẽ được đặt mỗi khi bạn nhấp hoặc kéo chuột trong khi giữ nút chuột trái.

.. tip::

    Trong chế độ Paint, bạn có thể vẽ một đường bằng cách giữ :kbd:`Shift` *trước khi* giữ nút chuột trái, sau đó kéo chuột đến điểm cuối của đường. Thao tác này giống hệt việc sử dụng công cụ Line được mô tả bên dưới.

    Bạn cũng có thể vẽ một hình chữ nhật bằng cách giữ :kbd:`Ctrl` và :kbd:`Shift` *trước khi* giữ nút chuột trái, sau đó kéo chuột đến điểm cuối của hình chữ nhật. Thao tác này giống hệt việc sử dụng công cụ Rectangle được mô tả bên dưới.

    Cuối cùng, bạn có thể chọn các tile hiện có trong trình chỉnh sửa 2D bằng cách giữ :kbd:`Ctrl` rồi nhấp vào một tile (hoặc giữ và kéo chuột). Thao tác này sẽ chuyển các tile đang được vẽ thành các tile bạn vừa nhấp vào. Thao tác này giống hệt việc sử dụng công cụ Picker được mô tả bên dưới.

Line
~~~~

Sau khi chọn chế độ Line Paint, bạn có thể vẽ một đường luôn dày 1 tile (bất kể hướng của đường).

Nếu nhấp chuột phải trong chế độ Line Paint, bạn sẽ xóa theo một đường.

Nếu bạn đã chọn nhiều tile trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại dọc theo đường.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở chế độ Paint hoặc Eraser bằng cách giữ
:kbd:`Shift` rồi vẽ.

.. figure:: img/using_tilesets_line_tool_multiple_tiles.webp
   :align: center
   :alt: Sử dụng công cụ đường thẳng sau khi chọn hai tile để vẽ các nền tảng theo đường chéo

   Sử dụng công cụ đường thẳng sau khi chọn hai tile để vẽ các nền tảng theo đường chéo

Rectangle
~~~~~~~~~

Sau khi chọn chế độ Rectangle Paint, bạn có thể vẽ một hình chữ nhật song song với các trục.

Nếu nhấp chuột phải trong chế độ Rectangle Paint, bạn sẽ xóa theo một hình chữ nhật song song với các trục.

Nếu bạn đã chọn nhiều tile trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại trong hình chữ nhật.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở chế độ Paint hoặc Eraser bằng cách giữ
:kbd:`Ctrl` và :kbd:`Shift` rồi vẽ.

Bucket Fill
~~~~~~~~~~~

Sau khi chọn chế độ Bucket Fill, bạn có thể chọn việc vẽ có bị giới hạn chỉ trong các vùng liền nhau hay không bằng cách bật hoặc tắt hộp kiểm **Contiguous** xuất hiện ở bên phải thanh công cụ.

Nếu bật **Contiguous** (mặc định), chỉ những tile khớp và tiếp giáp với vùng chọn hiện tại mới được thay thế. Việc kiểm tra tính liền nhau này được thực hiện theo chiều ngang và chiều dọc, nhưng *không* theo đường chéo.

Nếu tắt **Contiguous**, tất cả các tile có cùng ID trong toàn bộ TileMap sẽ được thay thế bằng tile hiện được chọn. Nếu chọn một tile rỗng khi **Contiguous** không được chọn, thay vào đó tất cả các tile trong hình chữ nhật bao phủ vùng hiệu dụng của TileMap sẽ được thay thế.

Nếu nhấp chuột phải trong chế độ Bucket Fill, bạn sẽ thay thế các tile khớp bằng các tile rỗng.

Nếu bạn đã chọn nhiều tile trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại trong vùng được tô.

.. figure:: img/using_tilemaps_bucket_fill.webp
   :align: center
   :alt: Sử dụng công cụ Bucket Fill

   Sử dụng công cụ Bucket Fill

Picker
~~~~~~

Sau khi chọn chế độ Picker, bạn có thể chọn các tile hiện có trong trình chỉnh sửa 2D bằng cách giữ :kbd:`Ctrl` rồi nhấp vào một tile. Tile đang được vẽ sẽ được chuyển thành tile bạn vừa nhấp. Bạn cũng có thể chọn nhiều tile cùng lúc bằng cách giữ nút chuột trái và tạo vùng chọn hình chữ nhật. Chỉ có thể chọn các tile không trống.

Bạn có thể tạm thời bật chế độ này khi đang ở chế độ Paint bằng cách giữ :kbd:`Ctrl` rồi nhấp hoặc kéo chuột.

Eraser
~~~~~~

Chế độ này kết hợp với mọi chế độ vẽ khác (Paint, Line, Rectangle, Bucket Fill). Khi bật chế độ Eraser, các tile sẽ được thay thế bằng tile trống thay vì vẽ các đường mới khi nhấp chuột trái.

Bạn có thể tạm thời bật chế độ này khi đang ở bất kỳ chế độ nào khác bằng cách nhấp chuột phải thay vì nhấp chuột trái.

Vẽ ngẫu nhiên bằng scattering
-----------------------------

Trong khi vẽ, bạn có thể tùy chọn bật *randomization*. Khi được bật, một tile ngẫu nhiên sẽ được chọn trong số tất cả các tile hiện đang được chọn khi vẽ. Tính năng này được hỗ trợ với các công cụ Paint, Line, Rectangle và Bucket Fill. Để randomization khi vẽ đạt hiệu quả, bạn phải chọn nhiều tile trong trình chỉnh sửa TileMap hoặc sử dụng scattering (có thể kết hợp cả hai cách).

Nếu **Scattering** được đặt thành giá trị lớn hơn 0, sẽ có khả năng không có tile nào được đặt khi vẽ. Bạn có thể dùng cách này để thêm các chi tiết không lặp lại một cách ngẫu nhiên vào những khu vực lớn (chẳng hạn như thêm cỏ hoặc vụn bánh vào một TileMap top-down lớn).

Ví dụ khi sử dụng chế độ Paint:

.. figure:: img/using_tilemaps_scatter_tiles.webp
   :align: center
   :alt: Chọn từ nhiều tile để chọn ngẫu nhiên, sau đó vẽ bằng cách giữ nút chuột trái

   Chọn từ nhiều tile để chọn ngẫu nhiên, sau đó vẽ bằng cách giữ nút chuột trái

Ví dụ khi sử dụng chế độ Bucket Fill:

.. figure:: img/using_tilemaps_bucket_fill_scatter.webp
   :align: center
   :alt: Sử dụng công cụ Bucket Fill với một tile duy nhất nhưng đã bật randomization và scattering

   Sử dụng công cụ Bucket Fill với một tile duy nhất nhưng đã bật randomization và scattering

.. note::

    Chế độ Eraser không tính đến randomization và scattering. Tất cả các tile trong vùng chọn luôn bị xóa.

Lưu và tải các vị trí tile tạo sẵn bằng patterns
------------------------------------------------

Mặc dù có thể sao chép và dán các tile khi ở chế độ Select, bạn có thể muốn lưu các *patterns* tile tạo sẵn để đặt cùng lúc. Bạn có thể thực hiện việc này cho từng TileMap bằng cách chọn tab **Patterns** của trình chỉnh sửa TileMap.

Để tạo pattern mới, chuyển sang chế độ Select, thực hiện một vùng chọn rồi nhấn
:kbd:`Ctrl + C`. Nhấp vào khoảng trống trong tab Patterns (một hình chữ nhật tiêu điểm màu xanh lam sẽ xuất hiện quanh khoảng trống), rồi nhấn :kbd:`Ctrl + V`:

.. figure:: img/using_tilemaps_create_pattern.webp
   :align: center
   :alt: Tạo pattern mới từ một vùng chọn trong trình chỉnh sửa TileMap

   Tạo pattern mới từ một vùng chọn trong trình chỉnh sửa TileMap

Để sử dụng một pattern hiện có, hãy nhấp vào hình ảnh của pattern đó trong tab **Patterns**, chuyển sang bất kỳ chế độ vẽ nào, rồi nhấp chuột trái vào một vị trí trong trình chỉnh sửa 2D:

.. figure:: img/using_tilemaps_use_pattern.webp
   :align: center
   :alt: Đặt một pattern hiện có bằng trình chỉnh sửa TileMap

   Đặt một pattern hiện có bằng trình chỉnh sửa TileMap

Giống như các vùng chọn nhiều tile, patterns sẽ được lặp lại nếu được sử dụng với các chế độ vẽ Line, Rectangle hoặc Bucket Fill.

.. note::

    Mặc dù được chỉnh sửa trong trình chỉnh sửa TileMap, patterns được lưu trữ trong tài nguyên TileSet. Điều này cho phép tái sử dụng patterns trong các node TileMapLayer khác sau khi tải tài nguyên TileSet được lưu vào một tệp bên ngoài.

Tự động xử lý kết nối giữa các tile bằng terrains
-------------------------------------------------

Để sử dụng terrains, node TileMapLayer phải có ít nhất một terrain set và một terrain trong terrain set đó. Xem
:ref:`doc_using_tilesets_creating_terrain_sets` nếu bạn chưa tạo terrain set cho TileSet.

Có 3 loại chế độ vẽ khả dụng cho các kết nối terrain:

- **Connect**, trong đó các tile được kết nối với các tile xung quanh trên cùng TileMapLayer.
- **Path**, trong đó các tile được kết nối với những tile được vẽ trong cùng một nét vẽ (cho đến khi thả nút chuột).
- Các tùy chỉnh riêng cho từng tile để giải quyết xung đột hoặc xử lý những tình huống không được hệ thống terrain bao quát.

Chế độ Connect dễ sử dụng hơn, nhưng Path linh hoạt hơn vì cho phép nghệ sĩ kiểm soát nhiều hơn trong quá trình vẽ. Ví dụ, Path có thể cho phép các con đường nằm ngay cạnh nhau mà không kết nối với nhau, trong khi Connect sẽ buộc cả hai con đường phải được kết nối.

.. figure:: img/using_tilemaps_terrain_select_connect_mode.webp
   :align: center
   :alt: Chọn chế độ Connect trong tab Terrains của trình chỉnh sửa TileMap

   Chọn chế độ Connect trong tab Terrains của trình chỉnh sửa TileMap

.. figure:: img/using_tilemaps_terrain_select_path_mode.webp
   :align: center
   :alt: Chọn chế độ Path trong tab Terrains của trình chỉnh sửa TileMap

   Chọn chế độ Path trong tab Terrains của trình chỉnh sửa TileMap

Cuối cùng, bạn có thể chọn các tile cụ thể từ terrain để giải quyết xung đột trong một số tình huống:

.. figure:: img/using_tilemaps_terrain_paint_specific_tiles.webp
   :align: center
   :alt: Vẽ bằng các tile cụ thể trong tab Terrains của trình chỉnh sửa TileMap

   Vẽ bằng các tile cụ thể trong tab Terrains của trình chỉnh sửa TileMap

Bất kỳ tile nào có ít nhất một bit được đặt thành giá trị tương ứng với terrain ID sẽ xuất hiện trong danh sách các tile để lựa chọn.

Xử lý các tile bị thiếu
-----------------------

Nếu bạn xóa các tile trong TileSet đang được tham chiếu trong TileMap, TileMap sẽ hiển thị một placeholder để cho biết rằng một tile ID không hợp lệ đã được đặt:

.. figure:: img/using_tilemaps_missing_tiles.webp
   :align: center
   :alt: Các tile bị thiếu trong trình chỉnh sửa TileMap do tham chiếu TileSet bị hỏng

   Các tile bị thiếu trong trình chỉnh sửa TileMap do tham chiếu TileSet bị hỏng

Các placeholder này **không** hiển thị trong project đang chạy, nhưng dữ liệu tile vẫn được lưu vào ổ đĩa. Điều này cho phép bạn đóng và mở lại các scene như vậy một cách an toàn. Sau khi bạn thêm lại một tile có ID tương ứng, các tile sẽ xuất hiện với hình thức của tile mới.

.. note::

    Các placeholder của tile bị thiếu có thể không hiển thị cho đến khi bạn chọn node TileMapLayer và mở trình chỉnh sửa TileMap.
