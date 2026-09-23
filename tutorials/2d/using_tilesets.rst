.. _doc_using_tilesets:

Sử dụng TileSets
================

Giới thiệu
----------

Tilemap là một lưới gồm các tile được dùng để tạo bố cục của game. Có một số lợi ích khi sử dụng các node :ref:`TileMapLayer <class_TileMapLayer>` để thiết kế level. Trước tiên, chúng cho phép bạn vẽ bố cục bằng cách "tô" các tile lên lưới, nhanh hơn nhiều so với việc đặt từng node :ref:`Sprite2D <class_Sprite2D>` riêng lẻ. Thứ hai, chúng cho phép tạo các level lớn hơn vì được tối ưu hóa để vẽ số lượng lớn tile. Cuối cùng, chúng cho phép bạn bổ sung nhiều chức năng hơn cho các tile bằng các shape collision, occlusion và navigation.

Để sử dụng các node TileMapLayer, trước tiên bạn cần tạo một TileSet. TileSet là một tập hợp các tile có thể được đặt trong node TileMapLayer. Sau khi tạo TileSet, bạn sẽ có thể đặt chúng :ref:`bằng TileMap editor <doc_using_tilemaps>`.

Để làm theo hướng dẫn này, bạn sẽ cần một hình ảnh chứa các tile, trong đó mọi tile đều có cùng kích thước (các đối tượng lớn có thể được tách thành nhiều tile). Hình ảnh này được gọi là *tilesheet*. Tile không nhất thiết phải có dạng hình vuông: chúng có thể có dạng hình chữ nhật, lục giác hoặc isometric (phối cảnh giả 3D).

Tạo TileSet mới
---------------

.. _doc_creating_tilesets_using_tilesheet:

Sử dụng tilesheet
~~~~~~~~~~~~~~~~~

Phần minh họa này sẽ sử dụng các tile sau, lấy từ gói `Kenney's "Abstract Platformer" pack <https://kenney.nl/assets/abstract-platformer>`__. Chúng ta sẽ sử dụng *tilesheet* cụ thể này từ bộ đó:

.. figure:: img/using_tilesets_kenney_abstract_platformer_tile_sheet.webp
   :align: center
   :alt: Ví dụ tilesheet với các tile 64×64

   Tilesheet với các tile 64×64. Tác giả: `Kenney <https://kenney.nl/assets/abstract-platformer>`__

Tạo một node **TileMapLayer** mới, sau đó chọn node đó và tạo một resource TileSet mới trong inspector:

.. figure:: img/using_tilesets_create_new_tileset.webp
   :align: center
   :alt: Tạo resource TileSet mới trong node TileMapLayer

   Tạo resource TileSet mới trong node TileMapLayer

Sau khi tạo resource TileSet, hãy nhấp vào giá trị để mở rộng nó trong inspector. Shape tile mặc định là Square, nhưng bạn cũng có thể chọn Isometric, Half-Offset Square hoặc Hexagon (tùy thuộc vào shape của hình ảnh tile). Nếu sử dụng shape tile khác Square, bạn cũng có thể cần điều chỉnh các thuộc tính **Tile Layout** và **Tile Offset Axis**. Cuối cùng, việc bật thuộc tính **Rendering > UV Clipping** có thể hữu ích nếu bạn muốn các tile bị cắt theo tọa độ tile. Điều này đảm bảo các tile không thể vẽ ra ngoài vùng được cấp phát cho chúng trên tilesheet.

Đặt kích thước tile thành 64×64 trong inspector để khớp với tilesheet mẫu:

.. figure:: img/using_tilesets_specify_size_then_edit.webp
   :align: center
   :alt: Đặt kích thước tile thành 64×64 để khớp với tilesheet mẫu

   Đặt kích thước tile thành 64×64 để khớp với tilesheet mẫu

Nếu dựa vào việc tạo tile tự động (như chúng ta sắp thực hiện ở đây), bạn phải đặt kích thước tile **trước khi** tạo *atlas*. Atlas sẽ xác định những tile nào từ tilesheet có thể được thêm vào node TileMapLayer (vì không phải mọi phần của hình ảnh đều có thể là tile hợp lệ).

Mở panel **TileSet** ở cuối editor, sau đó nhấp và kéo hình ảnh tilesheet vào panel. Bạn sẽ được hỏi có muốn tự động tạo tile hay không. Chọn **Yes**:

.. figure:: img/using_tilesets_create_tiles_automatically.webp
   :align: center
   :alt: Tự động tạo tile dựa trên nội dung hình ảnh tilesheet

   Tự động tạo tile dựa trên nội dung hình ảnh tilesheet

Thao tác này sẽ tự động tạo các tile theo kích thước tile bạn đã chỉ định trước đó trong resource TileSet. Điều này giúp tăng tốc đáng kể quá trình thiết lập tile ban đầu.

.. note::

    Khi sử dụng tính năng tạo tile tự động dựa trên nội dung hình ảnh, các phần của tilesheet hoàn toàn *trong suốt* sẽ không được tạo tile.

Nếu có các tile trong tilesheet mà bạn không muốn xuất hiện trong atlas, hãy chọn công cụ Eraser ở đầu phần xem trước tileset, sau đó nhấp vào các tile bạn muốn xóa:

.. figure:: img/using_tilesets_eraser_tool.webp
   :align: center
   :alt: Sử dụng công cụ Eraser để xóa các tile không mong muốn khỏi atlas TileSet

   Sử dụng công cụ Eraser để xóa các tile không mong muốn khỏi atlas TileSet

Bạn cũng có thể nhấp chuột phải vào một tile và chọn **Delete**, thay cho công cụ Eraser.

.. tip::

    Giống như trong các editor 2D và TileMap, bạn có thể di chuyển khung nhìn trong panel TileSet bằng nút chuột giữa hoặc chuột phải, và zoom bằng con lăn chuột hoặc các nút ở góc trên bên trái.

Nếu muốn lấy tile từ nhiều hình ảnh tilesheet cho một TileSet duy nhất, hãy tạo thêm các atlas và gán texture cho từng atlas trước khi tiếp tục. Theo cách này, bạn cũng có thể sử dụng một hình ảnh cho mỗi tile (mặc dù nên sử dụng tilesheet để có khả năng sử dụng tốt hơn).

Bạn có thể điều chỉnh các thuộc tính của atlas trong cột ở giữa:

.. figure:: img/using_tilesets_properties.webp
   :align: center
   :alt: Điều chỉnh các thuộc tính atlas của TileSet trong inspector chuyên dụng (một phần của panel TileSet)

   Điều chỉnh các thuộc tính atlas của TileSet trong inspector chuyên dụng (một phần của panel TileSet)

Có thể điều chỉnh các thuộc tính sau trên atlas:

- **ID:** Mã định danh (duy nhất trong TileSet này), được dùng để sắp xếp.
- **Name:** Tên dễ đọc dành cho atlas. Hãy sử dụng tên mô tả tại đây để phục vụ mục đích tổ chức (chẳng hạn như "terrain", "decoration", v.v.).
- **Margins:** Phần lề ở các cạnh hình ảnh không được chọn làm tile (tính bằng pixel). Việc tăng giá trị này có thể hữu ích nếu bạn tải xuống một hình ảnh tilesheet có phần lề ở các cạnh (ví dụ: để ghi công).
- **Separation:** Khoảng cách giữa mỗi tile trên atlas, tính bằng pixel. Việc tăng giá trị này có thể hữu ích nếu hình ảnh tilesheet bạn đang sử dụng có chứa các đường hướng dẫn (chẳng hạn như đường viền giữa mọi tile).
- **Texture Region Size:** Kích thước của mỗi tile trên atlas, tính bằng pixel. Trong hầu hết trường hợp, giá trị này nên khớp với kích thước tile được xác định trong thuộc tính TileMapLayer (mặc dù đây không phải yêu cầu bắt buộc).
- **Use Texture Padding:** Nếu được bật, tùy chọn này sẽ thêm một cạnh trong suốt rộng 1 pixel quanh mỗi tile để ngăn texture bleeding khi bật filtering. Bạn nên giữ tùy chọn này luôn bật, trừ khi gặp vấn đề hiển thị do texture padding.

Lưu ý rằng việc thay đổi texture margin, separation và region size có thể khiến các tile bị mất (vì một số tile sẽ nằm ngoài tọa độ của hình ảnh atlas). Để tự động tạo lại tile từ tilesheet, hãy sử dụng nút menu ba dấu chấm dọc ở đầu TileSet editor và chọn **Create Tiles in Non-Transparent Texture Regions**:

.. figure:: img/using_tilesets_recreate_tiles_automatically.webp
   :align: center
   :alt: Tự động tạo lại tile sau khi thay đổi các thuộc tính atlas

   Tự động tạo lại tile sau khi thay đổi các thuộc tính atlas

Sử dụng một tập hợp các scene
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn cũng có thể đặt các *scene* thực tế làm tile. Điều này cho phép bạn sử dụng bất kỳ tập hợp node nào làm tile. Ví dụ: bạn có thể sử dụng scene tile để đặt các thành phần gameplay, chẳng hạn như các cửa hàng mà người chơi có thể tương tác. Bạn cũng có thể sử dụng scene tile để đặt các AudioStreamPlayer2D (cho âm thanh môi trường), hiệu ứng hạt và nhiều thành phần khác.

.. warning::

   Scene tile có chi phí hiệu năng cao hơn so với atlas, vì mỗi scene được khởi tạo riêng cho từng tile được đặt.

   Bạn chỉ nên sử dụng scene tile khi cần thiết. Để vẽ sprite trong một tile mà không cần bất kỳ thao tác nâng cao nào,
   :ref:`thay vào đó hãy sử dụng atlas <doc_creating_tilesets_using_tilesheet>`.

Trong ví dụ này, chúng ta sẽ tạo một scene chứa node gốc CPUParticles2D. Lưu scene này vào một tệp scene (tách biệt với scene chứa TileMapLayer), sau đó chuyển sang scene chứa node TileMapLayer. Mở trình chỉnh sửa TileSet và tạo một **Scenes Collection** mới trong cột bên trái:

.. figure:: img/using_tilesets_creating_scene_collection.webp
   :align: center
   :alt: Tạo một scenes collection trong trình chỉnh sửa TileSet

   Tạo một scenes collection trong trình chỉnh sửa TileSet

Sau khi tạo scenes collection, bạn có thể nhập tên mô tả cho scenes collection ở cột giữa nếu muốn. Chọn scenes collection này, sau đó tạo một scene slot mới:

.. figure:: img/using_tilesets_scene_collection_create_scene_tile.webp
   :align: center
   :alt: Tạo scene tile sau khi chọn scenes collection trong trình chỉnh sửa TileSet

   Tạo scene tile sau khi chọn scenes collection trong trình chỉnh sửa TileSet

Chọn scene slot này ở cột bên phải, sau đó sử dụng **Quick Load** (hoặc **Load**) để tải tệp scene chứa các hạt:

.. figure:: img/using_tilesets_adding_scene_tile.webp
   :align: center
   :alt: Tạo scene slot, sau đó tải một tệp scene vào đó trong trình chỉnh sửa TileSet

   Tạo scene slot, sau đó tải một tệp scene vào đó trong trình chỉnh sửa TileSet

Bây giờ bạn đã có một scene tile trong TileSet. Sau khi chuyển sang trình chỉnh sửa TileMap, bạn có thể chọn scene tile này từ scenes collection và vẽ nó như bất kỳ tile nào khác.

Hợp nhất nhiều atlas thành một atlas duy nhất
---------------------------------------------

Việc sử dụng nhiều atlas trong cùng một tài nguyên TileSet đôi khi hữu ích, nhưng cũng có thể gây bất tiện trong một số tình huống (đặc biệt nếu bạn sử dụng một hình ảnh cho mỗi tile). Godot cho phép bạn hợp nhất nhiều atlas thành một atlas duy nhất để dễ tổ chức hơn.

Để thực hiện việc này, bạn phải có nhiều hơn một atlas được tạo trong tài nguyên TileSet. Sử dụng nút menu "ba dấu chấm dọc" nằm ở cuối danh sách atlas, sau đó chọn **Open Atlas Merging Tool**:

.. figure:: img/using_tilesets_open_atlas_merging_tool.webp
   :align: center
   :alt: Mở công cụ hợp nhất atlas sau khi tạo nhiều atlas

   Mở công cụ hợp nhất atlas sau khi tạo nhiều atlas

Thao tác này sẽ mở một hộp thoại, trong đó bạn có thể chọn nhiều atlas bằng cách giữ
:kbd:`Shift` hoặc :kbd:`Ctrl` rồi nhấp vào nhiều phần tử:

.. figure:: img/using_tilesets_atlas_merging_tool_dialog.webp
   :align: center
   :alt: Sử dụng hộp thoại công cụ hợp nhất atlas

   Sử dụng hộp thoại công cụ hợp nhất atlas

Chọn **Merge** để hợp nhất các atlas đã chọn thành một hình ảnh atlas duy nhất (tương ứng với một atlas duy nhất trong TileSet). Các atlas chưa hợp nhất sẽ bị xóa khỏi TileSet, nhưng *các hình ảnh tilesheet gốc sẽ vẫn được giữ trong hệ thống tệp*. Nếu không muốn các atlas chưa hợp nhất bị xóa khỏi tài nguyên TileSet, hãy chọn **Merge (Keep Original Atlases)** thay thế.

.. tip::

    TileSet có một hệ thống *tile proxy*. Tile proxy là một bảng ánh xạ cho phép thông báo cho TileMap sử dụng một TileSet nhất định rằng một tập hợp mã định danh tile nhất định nên được thay thế bằng một tập hợp khác.

    Tile proxy được tự động thiết lập khi hợp nhất các atlas khác nhau, nhưng bạn cũng có thể thiết lập thủ công bằng hộp thoại **Manage Tile Proxies**, có thể truy cập thông qua menu "ba dấu chấm dọc" đã đề cập ở trên.

    Việc tạo tile proxy thủ công có thể hữu ích khi bạn thay đổi ID atlas hoặc muốn thay thế tất cả tile từ một atlas bằng các tile từ atlas khác. Lưu ý rằng khi chỉnh sửa TileMap, bạn có thể thay thế tất cả cell bằng giá trị ánh xạ tương ứng của chúng.

Thêm collision, navigation và occlusion vào TileSet
---------------------------------------------------

Chúng ta đã tạo thành công một TileSet cơ bản. Bây giờ có thể bắt đầu sử dụng nó trong node TileMapLayer, nhưng hiện tại nó chưa có bất kỳ dạng phát hiện collision nào. Điều này có nghĩa là người chơi và các đối tượng khác có thể đi xuyên qua sàn hoặc tường.

Nếu sử dụng :ref:`2D navigation <doc_navigation_overview_2d>`, bạn cũng cần xác định các polygon navigation cho tile để tạo navigation mesh mà các agent có thể sử dụng cho việc tìm đường.

Cuối cùng, nếu bạn sử dụng :ref:`doc_2d_lights_and_shadows` hoặc GPUParticles2D, bạn cũng có thể muốn TileSet có khả năng đổ bóng và va chạm với các hạt. Điều này yêu cầu xác định các polygon occluder cho những tile "đặc" trong TileSet.

Để có thể xác định các hình dạng collision, navigation và occlusion cho từng tile, trước tiên bạn cần tạo một physics layer, navigation layer hoặc occlusion layer cho tài nguyên TileSet. Để thực hiện việc này, hãy chọn node TileMapLayer, nhấp vào giá trị thuộc tính TileSet trong inspector để chỉnh sửa, sau đó mở rộng **Physics Layers** và chọn **Add Element**:

.. figure:: img/using_tilesets_create_physics_layer.webp
   :align: center
   :alt: Tạo physics layer trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

   Tạo physics layer trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

Nếu cũng cần hỗ trợ navigation, đây là thời điểm thích hợp để tạo một navigation layer:

.. figure:: img/using_tilesets_create_navigation_layer.webp
   :align: center
   :alt: Tạo navigation layer trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

   Tạo navigation layer trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

Nếu cần hỗ trợ cho các light polygon occluder, đây là thời điểm thích hợp để tạo một occlusion layer:

.. figure:: img/using_tilesets_create_occlusion_layer.webp
   :align: center
   :alt: Tạo occlusion layer trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

   Tạo một lớp che khuất trong trình kiểm tra resource TileSet (bên trong node TileMapLayer)

.. note::

    Các bước tiếp theo trong hướng dẫn này tập trung vào việc tạo các polygon va chạm, nhưng quy trình cho navigation và che khuất rất tương tự. Các trình chỉnh sửa polygon tương ứng hoạt động theo cùng một cách, vì vậy để ngắn gọn, các bước này không được lặp lại.

    Điểm cần lưu ý duy nhất là thuộc tính polygon che khuất của tile nằm trong phân mục **Rendering** của trình kiểm tra atlas. Hãy mở rộng phân mục này để bạn có thể chỉnh sửa polygon.

Sau khi tạo một physics layer, bạn có thể truy cập phân mục **Physics Layer** trong trình kiểm tra atlas của TileSet:

.. figure:: img/using_tilesets_selecting_collision_editor.webp
   :align: center
   :alt: Mở trình chỉnh sửa va chạm khi đang ở chế độ Select

   Mở trình chỉnh sửa va chạm khi đang ở chế độ Select

Bạn có thể nhanh chóng tạo một hình va chạm hình chữ nhật bằng cách nhấn :kbd:`F` khi trình chỉnh sửa TileSet đang được focus. Nếu phím tắt không hoạt động, hãy thử nhấp vào vùng trống xung quanh trình chỉnh sửa polygon để focus vùng đó:

.. figure:: img/using_tilesets_using_default_rectangle_collision.webp
   :align: center
   :alt: Sử dụng hình va chạm hình chữ nhật mặc định bằng cách nhấn :kbd:`F`

   Sử dụng hình va chạm hình chữ nhật mặc định bằng cách nhấn :kbd:`F`

Trong trình chỉnh sửa va chạm của tile này, bạn có thể sử dụng tất cả các công cụ chỉnh sửa polygon 2D:

- Sử dụng thanh công cụ phía trên polygon để chuyển đổi giữa việc tạo polygon mới, chỉnh sửa polygon hiện có và xóa các điểm trên polygon. Nút menu "ba dấu chấm dọc" cung cấp thêm các tùy chọn, chẳng hạn như xoay và lật polygon.
- Tạo các điểm mới bằng cách nhấp và kéo một đường nối giữa hai điểm.
- Xóa một điểm bằng cách nhấp chuột phải vào điểm đó (hoặc sử dụng công cụ Remove được mô tả ở trên rồi nhấp chuột trái).
- Di chuyển khung nhìn trong trình chỉnh sửa bằng cách nhấp chuột giữa hoặc nhấp chuột phải. (Chỉ có thể di chuyển khung nhìn bằng chuột phải ở những vùng không có điểm nào ở gần.)

Bạn cũng có thể sử dụng hình chữ nhật mặc định làm cơ sở để nhanh chóng tạo một hình va chạm dạng tam giác bằng cách xóa một trong các điểm:

.. figure:: img/using_tilesets_creating_triangle_collision.webp
   :align: center
   :alt: Tạo hình va chạm dạng tam giác bằng cách nhấp chuột phải vào một trong các góc để xóa góc đó

   Tạo hình va chạm dạng tam giác bằng cách nhấp chuột phải vào một trong các góc để xóa góc đó

Bạn cũng có thể sử dụng hình chữ nhật làm cơ sở cho các hình phức tạp hơn bằng cách thêm nhiều điểm:

.. figure:: img/using_tilesets_drawing_custom_collision.webp
   :align: center
   :alt: Vẽ hình va chạm tùy chỉnh cho một tile có hình dạng phức tạp

   Vẽ hình va chạm tùy chỉnh cho một tile có hình dạng phức tạp

.. tip::

    Nếu bạn có một tileset lớn, việc chỉ định va chạm cho từng tile riêng lẻ có thể tốn rất nhiều thời gian. Điều này đặc biệt đúng vì TileMap thường có nhiều tile với các mẫu va chạm giống nhau (chẳng hạn như các khối đặc hoặc các dốc 45 độ). Để nhanh chóng áp dụng một hình va chạm tương tự cho nhiều tile, hãy sử dụng chức năng
    :ref:`gán thuộc tính cho nhiều tile cùng lúc <doc_using_tilemaps_assigning_properties_to_multiple_tiles>`.

Gán metadata tùy chỉnh cho các tile của TileSet
-----------------------------------------------

Bạn có thể gán dữ liệu tùy chỉnh cho từng tile bằng cách sử dụng *các lớp dữ liệu tùy chỉnh*. Điều này hữu ích để lưu trữ thông tin riêng cho trò chơi của bạn, chẳng hạn như sát thương mà một tile gây ra khi người chơi chạm vào nó, hoặc liệu một tile có thể bị phá hủy bằng vũ khí hay không.

Dữ liệu được liên kết với tile trong TileSet: tất cả các instance của tile đã đặt sẽ sử dụng cùng một dữ liệu tùy chỉnh. Nếu cần tạo một biến thể của tile có dữ liệu tùy chỉnh khác, bạn có thể thực hiện việc này bằng cách :ref:`tạo một tile thay thế <doc_using_tilesets_creating_alternative_tiles>` và chỉ thay đổi dữ liệu tùy chỉnh cho tile thay thế đó.

.. figure:: img/using_tilesets_create_custom_data_layer.webp
   :align: center
   :alt: Tạo một lớp dữ liệu tùy chỉnh trong trình kiểm tra resource TileSet (bên trong node TileMapLayer)

   Tạo một lớp dữ liệu tùy chỉnh trong trình kiểm tra resource TileSet (bên trong node TileMapLayer)

.. figure:: img/using_tilesets_custom_data_layers_example.webp
   :align: center
   :alt: Ví dụ về các lớp dữ liệu tùy chỉnh đã được cấu hình với các thuộc tính riêng cho trò chơi

   Ví dụ về các lớp dữ liệu tùy chỉnh đã được cấu hình với các thuộc tính riêng cho trò chơi

Bạn có thể sắp xếp lại dữ liệu tùy chỉnh mà không làm hỏng metadata hiện có: trình chỉnh sửa TileSet sẽ tự động cập nhật sau khi bạn sắp xếp lại các thuộc tính dữ liệu tùy chỉnh.

Với ví dụ về các lớp dữ liệu tùy chỉnh ở trên, chúng ta đang gán cho một tile metadata ``damage_per_second`` là ``25`` và metadata ``destructible`` là ``false``:

.. figure:: img/using_tilesets_edit_custom_data.webp
   :align: center
   :alt: Chỉnh sửa dữ liệu tùy chỉnh trong trình chỉnh sửa TileSet khi đang ở chế độ Select

   Chỉnh sửa dữ liệu tùy chỉnh trong trình chỉnh sửa TileSet khi đang ở chế độ Select

:ref:`Vẽ thuộc tính tile <doc_using_tilemaps_using_tile_property_painting>` cũng có thể được sử dụng cho dữ liệu tùy chỉnh:

.. figure:: img/using_tilesets_paint_custom_data.webp
   :align: center
   :alt: Gán dữ liệu tùy chỉnh trong trình chỉnh sửa TileSet bằng cách sử dụng tính năng vẽ thuộc tính tile

   Gán dữ liệu tùy chỉnh trong trình chỉnh sửa TileSet bằng cách sử dụng tính năng vẽ thuộc tính tile

.. _doc_using_tilesets_creating_terrain_sets:

Tạo các terrain set (autotiling)
--------------------------------

.. note::

    Tính năng này được triển khai dưới một hình thức khác dưới tên *autotiling* trong Godot 3.x. Terrain về cơ bản là một sự thay thế mạnh mẽ hơn cho autotile. Không giống autotile, terrain có thể hỗ trợ quá trình chuyển đổi từ terrain này sang terrain khác, vì một tile có thể xác định nhiều terrain cùng lúc.

    Không giống như trước đây, khi autotile là một loại tile cụ thể, terrain chỉ là một tập hợp các thuộc tính được gán cho các tile trong atlas. Các thuộc tính này sau đó được một chế độ vẽ TileMap chuyên dụng sử dụng để chọn các tile có dữ liệu terrain theo cách thông minh. Điều này có nghĩa là bất kỳ tile terrain nào cũng có thể được vẽ dưới dạng terrain hoặc dưới dạng một tile đơn lẻ, như mọi tile khác.

Một tileset "được hoàn thiện" thường có các biến thể mà bạn nên sử dụng ở các góc hoặc cạnh của platform, sàn nhà, v.v. Mặc dù có thể đặt chúng theo cách thủ công, việc này nhanh chóng trở nên tẻ nhạt. Việc xử lý tình huống này với các level được tạo theo thủ tục cũng có thể khó khăn và đòi hỏi nhiều code.

Godot cung cấp *terrains* để tự động thực hiện kiểu kết nối ô này. Nhờ đó, các biến thể ô "chính xác" sẽ được tự động sử dụng.

Terrains được nhóm thành các terrain set. Mỗi terrain set được gán một chế độ từ **Match Corners and Sides**, **Match Corners** và **Match sides**. Các chế độ này xác định cách các terrain được đối sánh với nhau trong một terrain set.

.. note::

    Các chế độ trên tương ứng với những chế độ bitmask trước đây mà autotile sử dụng trong Godot 3.x: 2×2, 3×3 hoặc 3×3 minimal. Điều này cũng tương tự với các tính năng của trình chỉnh sửa `Tiled <https://www.mapeditor.org/>`__.

Chọn node TileMapLayer, đi đến inspector và tạo một terrain set mới trong *resource* TileSet:

.. figure:: img/using_tilesets_create_terrain_set.webp
   :align: center
   :alt: Tạo một terrain set trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

   Tạo một terrain set trong inspector tài nguyên TileSet (bên trong node TileMapLayer)

Sau khi tạo terrain set, bạn **phải** tạo một hoặc nhiều terrain *bên trong* terrain set:

.. figure:: img/using_tilesets_create_terrain.webp
   :align: center
   :alt: Tạo một terrain bên trong terrain set

   Tạo một terrain bên trong terrain set

Trong trình chỉnh sửa TileSet, chuyển sang chế độ Select và nhấp vào một ô. Ở cột giữa, mở rộng phần **Terrains**, sau đó gán terrain set ID và terrain ID cho ô. ``-1`` có nghĩa là "không có terrain set" hoặc "không có terrain", tức là bạn phải đặt **Terrain Set** thành ``0`` hoặc lớn hơn trước khi có thể đặt **Terrain** thành ``0`` hoặc lớn hơn.

.. note::

   Terrain set ID và terrain ID độc lập với nhau. Chúng cũng bắt đầu từ ``0``, không phải ``1``.

.. figure:: img/using_tilesets_configure_terrain_on_tile.webp
   :align: center
   :alt: Cấu hình terrain trên một ô trong chế độ Select của trình chỉnh sửa TileSet

   Cấu hình terrain trên một ô trong chế độ Select của trình chỉnh sửa TileSet

Sau đó, bạn có thể cấu hình phần **Terrain Peering Bits** xuất hiện ở cột giữa. Các peering bit xác định ô nào sẽ được đặt tùy theo những ô lân cận. ``-1`` là một giá trị đặc biệt dùng để chỉ khoảng trống.

Ví dụ, nếu tất cả các bit của một ô được đặt thành ``0`` hoặc lớn hơn, ô đó chỉ xuất hiện khi *cả* 8 ô lân cận đều sử dụng một ô có cùng terrain ID. Nếu các bit của một ô được đặt thành ``0`` hoặc lớn hơn, nhưng các bit trên cùng bên trái, trên cùng và trên cùng bên phải được đặt thành ``-1``, ô đó chỉ xuất hiện khi có khoảng trống phía trên nó (bao gồm cả theo đường chéo).

.. figure:: img/using_tilesets_configure_terrain_peering_bits.webp
   :align: center
   :alt: Cấu hình terrain peering bit trên một ô trong chế độ Select của trình chỉnh sửa TileSet

   Cấu hình terrain peering bit trên một ô trong chế độ Select của trình chỉnh sửa TileSet

Một cấu hình mẫu cho toàn bộ tilesheet có thể như sau:

.. figure:: img/using_tilesets_terrain_example_tilesheet.webp
   :align: center
   :alt: Tilesheet đầy đủ mẫu cho một game sidescrolling

   Tilesheet đầy đủ mẫu cho một game sidescrolling

.. figure:: img/using_tilesets_terrain_example_tilesheet_configuration.webp
   :align: center
   :alt: Tilesheet đầy đủ mẫu cho một game sidescrolling với terrain peering bit được hiển thị

   Tilesheet đầy đủ mẫu cho một game sidescrolling với terrain peering bit được hiển thị

.. _doc_using_tilemaps_assigning_properties_to_multiple_tiles:

Gán thuộc tính cho nhiều ô cùng lúc
-----------------------------------

Có hai cách để gán thuộc tính cho nhiều ô cùng lúc. Tùy vào trường hợp sử dụng, một phương pháp có thể nhanh hơn phương pháp còn lại:

Sử dụng tính năng chọn nhiều ô
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu muốn cấu hình nhiều thuộc tính trên nhiều ô cùng lúc, hãy chọn chế độ **Select** ở đầu trình chỉnh sửa TileSet:

Sau đó, bạn có thể chọn nhiều ô ở cột bên phải bằng cách giữ
:kbd:`Shift` rồi nhấp vào các ô. Bạn cũng có thể chọn theo hình chữ nhật bằng cách giữ nút chuột trái rồi kéo chuột. Cuối cùng, bạn có thể bỏ chọn các ô đã được chọn (mà không ảnh hưởng đến phần lựa chọn còn lại) bằng cách giữ :kbd:`Shift` rồi nhấp vào một ô đã chọn.

Sau đó, bạn có thể gán thuộc tính bằng inspector ở cột giữa của trình chỉnh sửa TileSet. Chỉ những thuộc tính bạn thay đổi tại đây mới được áp dụng cho tất cả các ô đã chọn. Giống như trong inspector của trình chỉnh sửa, các thuộc tính khác nhau giữa những ô đã chọn sẽ vẫn khác nhau cho đến khi bạn chỉnh sửa chúng.

Với các thuộc tính số và màu, sau khi chỉnh sửa một thuộc tính, bạn cũng sẽ thấy bản xem trước giá trị của thuộc tính đó trên tất cả các ô trong atlas:

.. figure:: img/using_tilesets_select_and_set_tile_properties.webp
   :align: center
   :alt: Chọn nhiều ô bằng chế độ Select, sau đó áp dụng thuộc tính

   Chọn nhiều ô bằng chế độ Select, sau đó áp dụng thuộc tính

.. _doc_using_tilemaps_using_tile_property_painting:

Sử dụng tính năng tô thuộc tính ô
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu muốn áp dụng một thuộc tính duy nhất cho nhiều ô cùng lúc, bạn có thể sử dụng chế độ *property painting* cho mục đích này.

Cấu hình thuộc tính cần tô ở cột giữa, sau đó nhấp vào các ô (hoặc giữ nút chuột trái) ở cột bên phải để "tô" thuộc tính lên các ô.

.. figure:: img/using_tilesets_paint_tile_properties.webp
   :align: center
   :alt: Tô thuộc tính ô bằng trình chỉnh sửa TileSet

   Tô thuộc tính ô bằng trình chỉnh sửa TileSet

Tính năng tô thuộc tính ô đặc biệt hữu ích với những thuộc tính tốn nhiều thời gian để thiết lập thủ công, chẳng hạn như hình dạng va chạm:

.. figure:: img/using_tilesets_paint_tile_properties_collision.webp
   :align: center
   :alt: Tô một đa giác va chạm, sau đó nhấp chuột trái vào các ô để áp dụng

   Tô một đa giác va chạm, sau đó nhấp chuột trái vào các ô để áp dụng

.. _doc_using_tilesets_creating_alternative_tiles:

Tạo các ô thay thế
------------------

Đôi khi, bạn muốn sử dụng một hình ảnh ô duy nhất (chỉ xuất hiện một lần trong atlas), nhưng được cấu hình theo những cách khác nhau. Ví dụ, bạn có thể muốn sử dụng cùng một hình ảnh ô nhưng xoay, lật hoặc điều chỉnh với một màu khác. Bạn có thể thực hiện việc này bằng *alternative tiles*.

.. tip::

      Kể từ Godot 4.2, bạn không còn phải tạo alternative tiles để xoay hoặc lật ô nữa. Bạn có thể xoay bất kỳ ô nào trong khi đặt ô đó ở trình chỉnh sửa TileMap bằng các nút xoay/lật trên thanh công cụ của trình chỉnh sửa TileMap.

Để tạo một tile thay thế, hãy nhấp chuột phải vào một tile cơ sở trong atlas được hiển thị bởi trình chỉnh sửa TileSet, sau đó chọn **Create an Alternative Tile**:

.. figure:: img/using_tilesets_create_alternative_tile.webp
   :align: center
   :alt: Tạo một tile thay thế bằng cách nhấp chuột phải vào một tile cơ sở trong trình chỉnh sửa TileSet

   Tạo một tile thay thế bằng cách nhấp chuột phải vào một tile cơ sở trong trình chỉnh sửa TileSet

Nếu hiện đang ở chế độ Select, tile thay thế sẽ được chọn sẵn để chỉnh sửa. Nếu không ở chế độ Select, bạn vẫn có thể tạo các tile thay thế, nhưng cần chuyển sang chế độ Select và chọn tile thay thế để chỉnh sửa.

Nếu không thấy tile thay thế, hãy di chuyển khung nhìn sang bên phải của hình ảnh atlas, vì các tile thay thế luôn xuất hiện bên phải các tile cơ sở của một atlas nhất định trong trình chỉnh sửa TileSet:

.. figure:: img/using_tilesets_configure_alternative_tile.webp
   :align: center
   :alt: Cấu hình một tile thay thế sau khi nhấp vào tile đó trong trình chỉnh sửa TileSet

   Cấu hình một tile thay thế sau khi nhấp vào tile đó trong trình chỉnh sửa TileSet

Sau khi chọn một tile thay thế, bạn có thể thay đổi mọi thuộc tính bằng cột ở giữa như khi thực hiện với một tile cơ sở. Tuy nhiên, danh sách các thuộc tính được hiển thị sẽ khác so với tile cơ sở:

- **Alternative ID:** Mã định danh số duy nhất cho tile thay thế này. Việc thay đổi mã này sẽ làm hỏng các TileMap hiện có, vì vậy hãy cẩn thận! Mã này cũng kiểm soát thứ tự sắp xếp trong danh sách các tile thay thế được hiển thị trong trình chỉnh sửa.
- **Rendering > Flip H:** Nếu ``true``, tile được lật theo chiều ngang.
- **Rendering > Flip V:** Nếu ``true``, tile được lật theo chiều dọc.
- **Rendering > Transpose:** Nếu ``true``, tile được xoay 90 độ *ngược chiều kim đồng hồ* rồi lật theo chiều dọc. Trên thực tế, để xoay tile 90 độ theo chiều kim đồng hồ mà không lật, bạn nên bật **Flip H** và **Transpose**. Để xoay tile 180 độ theo chiều kim đồng hồ, hãy bật **Flip H** và **Flip V**. Để xoay tile 270 độ theo chiều kim đồng hồ, hãy bật **Flip V** và **Transpose**.
- **Rendering > Texture Origin:** Vị trí gốc được dùng để vẽ tile. Có thể dùng thuộc tính này để tạo độ lệch hiển thị của tile so với tile cơ sở.
- **Rendering > Modulate:** Bộ nhân màu được dùng khi kết xuất tile.
- **Rendering > Material:** Material được dùng cho tile này. Có thể dùng thuộc tính này để áp dụng blend mode khác hoặc các shader tùy chỉnh cho một tile riêng lẻ.
- **Z Index:** Thứ tự sắp xếp của tile này. Các giá trị cao hơn sẽ khiến tile được kết xuất ở phía trước các tile khác trên cùng một layer.
- **Y Sort Origin:** Độ lệch theo chiều dọc được dùng để sắp xếp tile dựa trên tọa độ Y của tile (tính bằng pixel). Điều này cho phép sử dụng các layer như thể chúng ở những độ cao khác nhau trong các game top-down. Điều chỉnh giá trị này có thể giúp giảm các vấn đề khi sắp xếp một số tile. Chỉ có hiệu lực nếu **Y Sort Enabled** là ``true`` trên node TileMapLayer trong **CanvasItem > Ordering**

Bạn có thể tạo thêm một biến thể tile thay thế bằng cách nhấp vào biểu tượng "+" lớn bên cạnh tile thay thế. Thao tác này tương đương với việc chọn tile cơ sở và nhấp chuột phải vào tile đó để chọn lại **Create an Alternative Tile**.

.. note::

    Khi tạo một tile thay thế, không thuộc tính nào từ tile cơ sở được kế thừa. Bạn phải thiết lập lại các thuộc tính trên tile thay thế nếu muốn chúng giống hệt nhau trên tile cơ sở và tile thay thế.
