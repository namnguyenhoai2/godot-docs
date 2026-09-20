.. _doc_using_tilemaps:

Sử dụng TileMap
===============

.. seealso::

    Trang này giả định rằng bạn đã tạo hoặc tải xuống một TileSet. Nếu chưa, trước tiên hãy đọc :ref:`doc_using_tilesets` vì bạn sẽ cần một TileSet để tạo TileMap.

Giới thiệu
----------

Tilemap là một lưới các ô được sử dụng để tạo bố cục của trò chơi. Có một số lợi ích khi sử dụng các node :ref:`TileMapLayer <class_TileMapLayer>` để thiết kế màn chơi. Thứ nhất, chúng cho phép vẽ bố cục bằng cách "tô" các ô lên lưới, nhanh hơn nhiều so với việc đặt từng node :ref:`Sprite2D <class_Sprite2D>` riêng lẻ. Thứ hai, chúng cho phép tạo các màn chơi lớn hơn nhiều vì được tối ưu hóa để vẽ số lượng lớn các ô. Cuối cùng, bạn có thể thêm các hình dạng va chạm, che khuất và điều hướng vào các ô, giúp TileMap có thêm nhiều chức năng hơn.

Chỉ định TileSet trong TileMapLayer
-----------------------------------

Nếu bạn đã làm theo trang trước về :ref:`doc_using_tilesets`, bạn sẽ có một tài nguyên TileSet được tích hợp trong node TileMapLayer. Điều này phù hợp cho việc tạo nguyên mẫu, nhưng trong một dự án thực tế, nhìn chung bạn sẽ có nhiều màn chơi cùng sử dụng một tileset.

Cách được khuyến nghị để sử dụng lại cùng một TileSet trong nhiều node TileMapLayer là lưu TileSet thành một tài nguyên bên ngoài. Để thực hiện việc này, hãy nhấp vào danh sách thả xuống bên cạnh tài nguyên TileSet và chọn **Save**:

.. figure:: img/using_tilemaps_save_tileset_to_resource.webp
   :align: center
   :alt: Saving the built-in TileSet resource to an external resource file

   Saving the built-in TileSet resource to an external resource file

Nhiều TileMapLayer và các thiết lập
-----------------------------------

Khi làm việc với tilemap, nhìn chung bạn nên sử dụng nhiều node TileMapLayer khi thích hợp. Việc sử dụng nhiều layer có thể mang lại lợi ích; chẳng hạn, điều này cho phép bạn phân biệt các ô tiền cảnh với các ô hậu cảnh để tổ chức tốt hơn. Bạn có thể đặt một ô trên mỗi layer tại một vị trí nhất định, cho phép chồng nhiều ô lên nhau nếu bạn có nhiều hơn một layer.

Mỗi node TileMapLayer có một số thuộc tính mà bạn có thể điều chỉnh:

- **Enabled:** Nếu ``true``, layer sẽ hiển thị trong trình chỉnh sửa và khi chạy dự án. - **TileSet** Tileset được node TileMapLayer sử dụng.

Kết xuất
~~~~~~~~

- **Y Sort Origin:** Độ lệch theo chiều dọc được sử dụng để sắp xếp theo Y trên mỗi ô (tính bằng pixel). Chỉ có hiệu lực nếu **Y Sort Enabled** trong các thiết lập CanvasItem là ``true``. - **X Draw Order Reversed** Đảo ngược thứ tự vẽ các ô trên trục X. Yêu cầu **Y Sort Enabled** trong các thiết lập CanvasItem là ``true``. - **Rendering Quadrant Size** Một quadrant là một nhóm các ô được vẽ cùng nhau trên một CanvasItem duy nhất nhằm mục đích tối ưu hóa. Thiết lập này xác định độ dài cạnh của một hình vuông trong hệ tọa độ của bản đồ. Kích thước quadrant không áp dụng cho TileMapLayer được sắp xếp theo Y vì trong trường hợp đó, các ô được nhóm theo vị trí Y.

Vật lý
~~~~~~
- **Collision Enabled** Bật hoặc tắt va chạm. - **Use Kinematic Bodies** Khi là true, các hình dạng va chạm của TileMapLayer sẽ được khởi tạo dưới dạng các vật thể động học. - **Collision Visibility Mode** Xác định các hình dạng va chạm của TileMapLayer có hiển thị hay không. Nếu đặt thành mặc định, điều này phụ thuộc vào các thiết lập gỡ lỗi hiển thị va chạm.

Điều hướng
~~~~~~~~~~

- **Navigation Enabled** Xác định các vùng điều hướng có được bật hay không. - **Navigation Visible** Xác định các lưới điều hướng của TileMapLayer có hiển thị hay không. Nếu đặt thành mặc định, điều này phụ thuộc vào các thiết lập gỡ lỗi hiển thị điều hướng.

.. tip::

    Điều hướng tích hợp của TileMap có nhiều hạn chế thực tế, dẫn đến hiệu suất tìm đường và chất lượng bám theo đường đi kém hơn.

    Sau khi thiết kế TileMap, hãy cân nhắc việc nướng nó thành một lưới điều hướng được tối ưu hóa hơn (và tắt TileMap NavigationLayer) bằng cách sử dụng một :ref:`NavigationRegion2D <class_NavigationRegion2D>` hoặc :ref:`NavigationServer2D <class_NavigationServer2D>`. Xem :ref:`doc_navigation_using_navigationmeshes` để biết thêm thông tin.

.. warning::

    Các lưới điều hướng 2D không thể được "xếp lớp" hoặc chồng lên nhau như hình ảnh hoặc hình dạng vật lý. Việc cố gắng chồng các lưới điều hướng trên cùng một bản đồ điều hướng sẽ dẫn đến các lỗi hợp nhất và logic làm hỏng quá trình tìm đường.

Sắp xếp lại các layer
~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sắp xếp lại các layer bằng cách kéo và thả node của chúng trong tab Scene. Bạn cũng có thể chuyển đổi giữa các node TileMapLayer mà mình đang làm việc bằng các nút ở góc trên bên phải của trình chỉnh sửa TileMap.

.. note::

    Bạn có thể tạo, đổi tên hoặc sắp xếp lại các layer trong tương lai mà không ảnh hưởng đến các ô hiện có. Tuy nhiên, hãy cẩn thận vì *xóa* một layer cũng sẽ xóa tất cả các ô đã được đặt trên layer đó.

Mở trình chỉnh sửa TileMap
--------------------------

Chọn node TileMapLayer, sau đó mở bảng TileMap ở cuối trình chỉnh sửa:

.. figure:: img/using_tilemaps_open_tilemap_editor.webp
   :align: center
   :alt: Opening the TileMap panel at the bottom of the editor. The TileMapLayer node must be selected first.

   Opening the TileMap panel at the bottom of the editor. The TileMapLayer node must be selected first.

Chọn các ô để sử dụng khi tô
----------------------------

Trước tiên, nếu bạn đã tạo thêm các layer, hãy đảm bảo rằng bạn đã chọn layer muốn tô lên:

.. figure:: img/using_tilemaps_select_layer.webp
   :align: center
   :alt: Selecting a layer to paint on in the TileMap editor

   Selecting a layer to paint on in the TileMap editor

.. tip::

    Trong trình chỉnh sửa 2D, các layer mà bạn hiện không chỉnh sửa từ cùng một node TileMapLayer sẽ hiển thị mờ đi khi ở trong trình chỉnh sửa TileMap. Bạn có thể tắt hành vi này bằng cách nhấp vào biểu tượng bên cạnh menu chọn layer (chú giải công cụ **Highlight Selected TileMap Layer**).

Bạn có thể bỏ qua bước trên nếu chưa tạo thêm layer, vì layer đầu tiên sẽ tự động được chọn khi vào trình chỉnh sửa TileMap.

Trước khi có thể đặt các ô trong trình chỉnh sửa 2D, bạn phải chọn một hoặc nhiều ô trong bảng TileMap ở cuối trình chỉnh sửa. Để thực hiện việc này, hãy nhấp vào một ô trong bảng TileMap hoặc giữ nút chuột để chọn nhiều ô:

.. figure:: img/using_tilemaps_select_single_tile_from_tileset.webp
   :align: center
   :alt: Selecting a tile in the TileMap editor by clicking it

   Selecting a tile in the TileMap editor by clicking it

.. tip::

    Tương tự như trong trình chỉnh sửa 2D và TileSet, bạn có thể di chuyển vùng nhìn trong bảng TileMap bằng nút chuột giữa hoặc phải, và thu phóng bằng con lăn chuột hoặc các nút ở góc trên bên trái.

Bạn cũng có thể giữ :kbd:`Shift` để thêm vào vùng chọn hiện tại. Khi chọn nhiều hơn một ô, nhiều ô sẽ được đặt mỗi khi bạn thực hiện thao tác tô. Điều này có thể được dùng để tô các cấu trúc gồm nhiều ô chỉ bằng một lần nhấp (chẳng hạn như các nền tảng lớn hoặc cây cối).

Vùng chọn cuối cùng không nhất thiết phải liền nhau: nếu có khoảng trống giữa các ô đã chọn, khoảng trống đó sẽ được giữ nguyên trong mẫu được tô trong trình chỉnh sửa 2D.

.. figure:: img/using_tilemaps_select_multiple_tiles_from_tileset.webp
   :align: center
   :alt: Selecting multiple tiles in the TileMap editor by holding down the left mouse button

   Selecting multiple tiles in the TileMap editor by holding down the left mouse button

Nếu bạn đã tạo các ô thay thế trong TileSet, bạn có thể chọn chúng để tô ở bên phải các ô cơ sở:

.. figure:: img/using_tilemaps_use_alternative_tile.webp
   :align: center
   :alt: Selecting an alternative tile in the TileMap editor

   Selecting an alternative tile in the TileMap editor

Cuối cùng, nếu bạn đã tạo một *scenes collection* trong TileSet, bạn có thể đặt các ô cảnh trong TileMap:

.. figure:: img/using_tilemaps_placing_scene_tiles.webp
   :align: center
   :alt: Placing a scene tile containing particles using the TileMap editor

   Placing a scene tile containing particles using the TileMap editor

Các chế độ và công cụ tô
------------------------

Bằng thanh công cụ ở đầu trình chỉnh sửa TileMap, bạn có thể chọn giữa nhiều chế độ và công cụ tô. Các chế độ này ảnh hưởng đến thao tác khi nhấp trong trình chỉnh sửa 2D, **không phải** chính bảng TileMap.

Từ trái sang phải, các chế độ và công cụ tô bạn có thể chọn là:

Chọn
~~~~

Chọn các ô bằng cách nhấp vào một ô hoặc giữ nút chuột trái để chọn nhiều ô bằng một hình chữ nhật trong trình chỉnh sửa 2D. Lưu ý rằng không thể chọn khoảng trống: nếu bạn tạo vùng chọn hình chữ nhật, chỉ các ô không trống mới được chọn.

Để thêm vào vùng chọn hiện tại, hãy giữ :kbd:`Shift` rồi chọn một ô. Để xóa khỏi vùng chọn hiện tại, hãy giữ :kbd:`Ctrl` rồi chọn một ô.

Sau đó, bạn có thể sử dụng vùng chọn ở bất kỳ chế độ tô nào khác để nhanh chóng tạo các bản sao của một mẫu đã được đặt.

Bạn có thể xóa các ô đã chọn khỏi TileMap bằng cách nhấn :kbd:`Del`.

Bạn có thể tạm thời bật chế độ này khi đang ở chế độ Paint bằng cách giữ :kbd:`Ctrl` rồi thực hiện thao tác chọn.

.. tip::

    Bạn có thể sao chép và dán các ô đã được đặt bằng cách thực hiện thao tác chọn, nhấn :kbd:`Ctrl + C` rồi nhấn :kbd:`Ctrl + V`. Vùng chọn sẽ được dán sau khi nhấp chuột trái. Bạn có thể nhấn
    :kbd:`Ctrl + V` another time to perform more pastes this way.
    Nhấp chuột phải hoặc nhấn :kbd:`Escape` để hủy thao tác dán.

Tô
~~~

Chế độ Paint tiêu chuẩn cho phép bạn đặt các ô bằng cách nhấp hoặc giữ nút chuột trái.

Nếu nhấp chuột phải, ô hiện đang được chọn sẽ bị xóa khỏi tilemap. Nói cách khác, ô đó sẽ được thay thế bằng khoảng trống.

Nếu bạn đã chọn nhiều ô trong TileMap hoặc bằng công cụ Selection, chúng sẽ được đặt mỗi khi bạn nhấp hoặc kéo chuột trong khi giữ nút chuột trái.

.. tip::

    Trong chế độ Paint, bạn có thể vẽ một đường bằng cách giữ :kbd:`Shift` *trước khi* giữ nút chuột trái, sau đó kéo chuột đến điểm cuối của đường. Điều này giống hệt việc sử dụng công cụ Line được mô tả bên dưới.

    Bạn cũng có thể vẽ một hình chữ nhật bằng cách giữ :kbd:`Ctrl` và :kbd:`Shift` *trước khi* giữ nút chuột trái, sau đó kéo chuột đến điểm cuối của hình chữ nhật. Điều này giống hệt việc sử dụng công cụ Rectangle được mô tả bên dưới.

    Cuối cùng, bạn có thể chọn các ô hiện có trong trình chỉnh sửa 2D bằng cách giữ :kbd:`Ctrl` rồi nhấp vào một ô (hoặc giữ và kéo chuột). Thao tác này sẽ chuyển các ô đang được tô thành các ô bạn vừa nhấp. Điều này giống hệt việc sử dụng công cụ Picker được mô tả bên dưới.

Đường
~~~~~

Sau khi chọn chế độ Line Paint, bạn có thể vẽ một đường luôn dày 1 ô (bất kể hướng của đường).

Nếu nhấp chuột phải khi đang ở chế độ Line Paint, bạn sẽ xóa theo một đường.

Nếu bạn đã chọn nhiều ô trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại dọc theo đường.

Bạn có thể tạm thời bật chế độ này khi đang ở chế độ Paint hoặc Eraser bằng cách giữ
:kbd:`Shift` then drawing.

.. figure:: img/using_tilesets_line_tool_multiple_tiles.webp
   :align: center
   :alt: Using the line tool after selecting two tiles to draw platforms diagonally

   Using the line tool after selecting two tiles to draw platforms diagonally

Hình chữ nhật
~~~~~~~~~~~~~

Sau khi chọn chế độ Vẽ hình chữ nhật, bạn có thể vẽ trong một hình chữ nhật thẳng trục.

Nếu nhấp chuột phải khi đang ở chế độ Vẽ hình chữ nhật, bạn sẽ xóa trong một hình chữ nhật thẳng trục.

Nếu đã chọn nhiều ô trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại trong hình chữ nhật.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở chế độ Paint hoặc Eraser bằng cách giữ
:kbd:`Ctrl` and :kbd:`Shift` then drawing.

Bucket Fill
~~~~~~~~~~~

Sau khi chọn chế độ Bucket Fill, bạn có thể chọn giới hạn việc vẽ chỉ trong các khu vực liên thông bằng cách bật hoặc tắt hộp kiểm **Contiguous** xuất hiện ở bên phải thanh công cụ.

Nếu bật **Contiguous** (mặc định), chỉ các ô khớp chạm vào vùng chọn hiện tại mới được thay thế. Kiểm tra tính liên thông này được thực hiện theo chiều ngang và chiều dọc, nhưng *không* theo đường chéo.

Nếu tắt **Contiguous**, tất cả các ô có cùng ID trong toàn bộ TileMap sẽ được thay thế bằng ô hiện được chọn. Nếu chọn một ô trống khi **Contiguous** đang tắt, tất cả các ô trong hình chữ nhật bao quanh vùng hiệu dụng của TileMap sẽ được thay thế.

Nếu nhấp chuột phải khi đang ở chế độ Bucket Fill, bạn sẽ thay thế các ô khớp bằng ô trống.

Nếu đã chọn nhiều ô trong TileMap hoặc bằng công cụ Selection, bạn có thể đặt chúng theo một mẫu lặp lại trong vùng đã tô.

.. figure:: img/using_tilemaps_bucket_fill.webp
   :align: center
   :alt: Using the Bucket Fill tool

   Using the Bucket Fill tool

Picker
~~~~~~

Sau khi chọn chế độ Picker, bạn có thể chọn các ô hiện có trong trình chỉnh sửa 2D bằng cách giữ :kbd:`Ctrl` rồi nhấp vào một ô. Thao tác này sẽ chuyển ô đang được vẽ thành ô bạn vừa nhấp vào. Bạn cũng có thể chọn nhiều ô cùng lúc bằng cách giữ nút chuột trái và tạo vùng chọn hình chữ nhật. Chỉ các ô không trống mới có thể được chọn.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở chế độ Paint bằng cách giữ :kbd:`Ctrl` rồi nhấp hoặc kéo chuột.

Eraser
~~~~~~

Chế độ này được kết hợp với mọi chế độ vẽ khác (Paint, Line, Rectangle, Bucket Fill). Khi bật chế độ Eraser, các ô sẽ được thay thế bằng ô trống thay vì vẽ các đường mới khi nhấp chuột trái.

Bạn có thể tạm thời chuyển sang chế độ này khi đang ở bất kỳ chế độ nào khác bằng cách nhấp chuột phải thay vì nhấp chuột trái.

Vẽ ngẫu nhiên bằng cách rải
---------------------------

Trong khi vẽ, bạn có thể tùy chọn bật tính năng *ngẫu nhiên hóa*. Khi được bật, một ô ngẫu nhiên sẽ được chọn trong số tất cả các ô hiện đang được chọn khi vẽ. Tính năng này được hỗ trợ với các công cụ Paint, Line, Rectangle và Bucket Fill. Để việc ngẫu nhiên hóa khi vẽ có hiệu quả, bạn phải chọn nhiều ô trong trình chỉnh sửa TileMap hoặc sử dụng tính năng rải (có thể kết hợp cả hai cách).

Nếu **Scattering** được đặt thành giá trị lớn hơn 0, sẽ có khả năng không có ô nào được đặt khi vẽ. Tính năng này có thể được dùng để thêm các chi tiết không lặp lại, xuất hiện không thường xuyên vào những khu vực lớn (chẳng hạn như thêm cỏ hoặc vụn bánh mì trên một TileMap nhìn từ trên xuống lớn).

Ví dụ khi sử dụng chế độ Paint:

.. figure:: img/using_tilemaps_scatter_tiles.webp
   :align: center
   :alt: Selecting from several times to randomly choose, then painting by holding down the left mouse button

   Selecting from several times to randomly choose, then painting by holding down the left mouse button

Ví dụ khi sử dụng chế độ Bucket Fill:

.. figure:: img/using_tilemaps_bucket_fill_scatter.webp
   :align: center
   :alt: Using Bucket Fill tool with a single tile, but with randomization and scattering enabled

   Using Bucket Fill tool with a single tile, but with randomization and scattering enabled

.. note::

    Chế độ Eraser không tính đến tính năng ngẫu nhiên hóa và rải. Tất cả các ô trong vùng chọn luôn bị xóa.

Lưu và tải các vị trí ô được tạo sẵn bằng các mẫu
-------------------------------------------------

Mặc dù bạn có thể sao chép và dán các ô khi ở chế độ Select, bạn có thể muốn lưu các *mẫu* ô được tạo sẵn để đặt chúng cùng lúc. Bạn có thể thực hiện việc này cho từng TileMap bằng cách chọn thẻ **Patterns** trong trình chỉnh sửa TileMap.

Để tạo một mẫu mới, chuyển sang chế độ Select, thực hiện việc chọn và nhấn
:kbd:`Ctrl + C`. Click on empty space within the Patterns tab (a blue focus
một hình chữ nhật sẽ xuất hiện quanh khoảng trống), sau đó nhấn :kbd:`Ctrl + V`:

.. figure:: img/using_tilemaps_create_pattern.webp
   :align: center
   :alt: Creating a new pattern from a selection in the TileMap editor

   Creating a new pattern from a selection in the TileMap editor

Để sử dụng một mẫu hiện có, hãy nhấp vào hình ảnh của mẫu trong thẻ **Patterns**, chuyển sang bất kỳ chế độ vẽ nào, sau đó nhấp chuột trái vào một vị trí bất kỳ trong trình chỉnh sửa 2D:

.. figure:: img/using_tilemaps_use_pattern.webp
   :align: center
   :alt: Placing an existing pattern using the TileMap editor

   Placing an existing pattern using the TileMap editor

Giống như các vùng chọn nhiều ô, các mẫu sẽ được lặp lại nếu được sử dụng với các chế độ vẽ Line, Rectangle hoặc Bucket Fill.

.. note::

    Mặc dù được chỉnh sửa trong trình chỉnh sửa TileMap, các mẫu được lưu trong tài nguyên TileSet. Điều này cho phép tái sử dụng các mẫu trong những node TileMapLayer khác sau khi tải một tài nguyên TileSet được lưu vào một tệp bên ngoài.

Tự động xử lý kết nối giữa các ô bằng terrain
---------------------------------------------

Để sử dụng terrain, node TileMapLayer phải có ít nhất một terrain set và một terrain bên trong terrain set này. Xem
:ref:`doc_using_tilesets_creating_terrain_sets` if you haven't created a terrain
set cho TileSet.

Có 3 loại chế độ vẽ khả dụng cho các kết nối terrain:

- **Connect**, trong đó các ô được kết nối với những ô xung quanh trên cùng TileMapLayer. - **Path**, trong đó các ô được kết nối với những ô được vẽ trong cùng một nét vẽ (cho đến khi thả nút chuột). - Các ghi đè dành riêng cho từng ô để giải quyết xung đột hoặc xử lý những tình huống không được hệ thống terrain đề cập.

Chế độ Connect dễ sử dụng hơn, nhưng Path linh hoạt hơn vì cho phép nghệ sĩ kiểm soát nhiều hơn trong quá trình vẽ. Chẳng hạn, Path có thể cho phép các con đường nằm ngay sát nhau mà không kết nối với nhau, trong khi Connect sẽ buộc cả hai con đường phải được kết nối.

.. figure:: img/using_tilemaps_terrain_select_connect_mode.webp
   :align: center
   :alt: Selecting Connect mode in the TileMap editor's Terrains tab

   Selecting Connect mode in the TileMap editor's Terrains tab

.. figure:: img/using_tilemaps_terrain_select_path_mode.webp
   :align: center
   :alt: Selecting Path mode in the TileMap editor's Terrains tab

   Selecting Path mode in the TileMap editor's Terrains tab

Cuối cùng, bạn có thể chọn các ô cụ thể từ terrain để giải quyết xung đột trong một số tình huống nhất định:

.. figure:: img/using_tilemaps_terrain_paint_specific_tiles.webp
   :align: center
   :alt: Painting with specific tiles in the TileMap editor's Terrains tab

   Painting with specific tiles in the TileMap editor's Terrains tab

Bất kỳ ô nào có ít nhất một bit được đặt thành giá trị tương ứng với terrain ID sẽ xuất hiện trong danh sách các ô để chọn.

Xử lý các ô bị thiếu
--------------------

Nếu xóa các ô trong TileSet đang được tham chiếu trong một TileMap, TileMap sẽ hiển thị một phần giữ chỗ để cho biết rằng một tile ID không hợp lệ đã được đặt:

.. figure:: img/using_tilemaps_missing_tiles.webp
   :align: center
   :alt: Missing tiles in the TileMap editor due to the TileSet reference being broken

   Missing tiles in the TileMap editor due to the TileSet reference being broken

Các phần giữ chỗ này **không** hiển thị trong dự án đang chạy, nhưng dữ liệu ô vẫn được lưu vào ổ đĩa. Điều này cho phép bạn đóng và mở lại các cảnh đó một cách an toàn. Khi thêm lại một ô có ID khớp, các ô sẽ hiển thị với hình thức của ô mới.

.. note::

    Các phần giữ chỗ cho ô bị thiếu có thể không hiển thị cho đến khi bạn chọn node TileMapLayer và mở trình chỉnh sửa TileMap.
