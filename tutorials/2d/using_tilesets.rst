.. _doc_using_tilesets:

Sử dụng TileSet
===============

Giới thiệu
----------

Tilemap là một lưới các tile được dùng để tạo bố cục của một trò chơi. Có một số lợi ích khi sử dụng các node :ref:`TileMapLayer <class_TileMapLayer>` để thiết kế màn chơi. Trước tiên, chúng cho phép bạn vẽ bố cục bằng cách “tô” các tile lên một lưới, nhanh hơn nhiều so với việc đặt từng node :ref:`Sprite2D <class_Sprite2D>` riêng lẻ. Thứ hai, chúng cho phép tạo các màn chơi lớn hơn vì được tối ưu hóa để vẽ số lượng lớn tile. Cuối cùng, chúng cho phép bạn bổ sung nhiều chức năng hơn cho các tile thông qua các hình dạng va chạm, che khuất và điều hướng.

Để sử dụng các node TileMapLayer, trước tiên bạn cần tạo một TileSet. TileSet là một tập hợp các tile có thể được đặt trong node TileMapLayer. Sau khi tạo TileSet, bạn sẽ có thể đặt chúng :ref:`using the TileMap editor <doc_using_tilemaps>`.

Để làm theo hướng dẫn này, bạn sẽ cần một hình ảnh chứa các tile, trong đó mọi tile đều có cùng kích thước (các đối tượng lớn có thể được chia thành nhiều tile). Hình ảnh này được gọi là một *tilesheet*. Các tile không nhất thiết phải có dạng vuông: chúng có thể là hình chữ nhật, hình lục giác hoặc isometric (phối cảnh giả 3D).

Tạo TileSet mới
---------------

.. _doc_creating_tilesets_using_tilesheet:

Sử dụng tilesheet
~~~~~~~~~~~~~~~~~

Phần minh họa này sẽ sử dụng các tile sau, lấy từ gói `Kenney's "Abstract Platformer" pack <https://kenney.nl/assets/abstract-platformer>`__. Chúng ta sẽ sử dụng *tilesheet* cụ thể này trong bộ:

.. figure:: img/using_tilesets_kenney_abstract_platformer_tile_sheet.webp
   :align: center
   :alt: Tilesheet example with 64×64 tiles

   Tilesheet with 64×64 tiles. Credit: `Kenney <https://kenney.nl/assets/abstract-platformer>`__

Tạo một node **TileMapLayer** mới, sau đó chọn node đó và tạo một tài nguyên TileSet mới trong inspector:

.. figure:: img/using_tilesets_create_new_tileset.webp
   :align: center
   :alt: Creating a new TileSet resource within the TileMapLayer node

   Creating a new TileSet resource within the TileMapLayer node

Sau khi tạo tài nguyên TileSet, hãy nhấp vào giá trị đó để mở rộng trong inspector. Hình dạng tile mặc định là Square, nhưng bạn cũng có thể chọn Isometric, Half-Offset Square hoặc Hexagon (tùy thuộc vào hình dạng của hình ảnh tile). Nếu sử dụng hình dạng tile khác Square, bạn cũng có thể cần điều chỉnh các thuộc tính **Tile Layout** và **Tile Offset Axis**. Cuối cùng, bật thuộc tính **Rendering > UV Clipping** có thể hữu ích nếu bạn muốn các tile được cắt theo tọa độ tile của chúng. Điều này đảm bảo các tile không thể vẽ ra ngoài vùng được cấp phát trên tilesheet.

Đặt kích thước tile thành 64×64 trong inspector để khớp với tilesheet mẫu:

.. figure:: img/using_tilesets_specify_size_then_edit.webp
   :align: center
   :alt: Setting the tile size to 64×64 to match the example tilesheet

   Setting the tile size to 64×64 to match the example tilesheet

Nếu dựa vào việc tạo tile tự động (như chúng ta sắp thực hiện ở đây), bạn phải đặt kích thước tile **trước khi** tạo *atlas*. Atlas sẽ xác định những tile nào từ tilesheet có thể được thêm vào node TileMapLayer (vì không phải mọi phần của hình ảnh đều có thể là một tile hợp lệ).

Mở panel **TileSet** ở cuối trình chỉnh sửa, sau đó nhấp và kéo hình ảnh tilesheet vào panel. Bạn sẽ được hỏi có muốn tự động tạo tile hay không. Hãy trả lời **Yes**:

.. figure:: img/using_tilesets_create_tiles_automatically.webp
   :align: center
   :alt: Automatically creating tiles based on tilesheet image content

   Automatically creating tiles based on tilesheet image content

Thao tác này sẽ tự động tạo các tile theo kích thước tile bạn đã chỉ định trước đó trong tài nguyên TileSet. Điều này giúp tăng tốc đáng kể quá trình thiết lập tile ban đầu.

.. note::

    Khi sử dụng tính năng tạo tile tự động dựa trên nội dung hình ảnh, những phần của tilesheet *hoàn toàn* trong suốt sẽ không được tạo tile.

Nếu có những tile từ tilesheet mà bạn không muốn xuất hiện trong atlas, hãy chọn công cụ Eraser ở đầu phần xem trước tileset, sau đó nhấp vào những tile bạn muốn xóa:

.. figure:: img/using_tilesets_eraser_tool.webp
   :align: center
   :alt: Using the Eraser tool to remove unwanted tiles from the TileSet atlas

   Using the Eraser tool to remove unwanted tiles from the TileSet atlas

Bạn cũng có thể nhấp chuột phải vào một tile và chọn **Delete**, thay cho công cụ Eraser.

.. tip::

    Tương tự như trong trình chỉnh sửa 2D và TileMap, bạn có thể di chuyển trong panel TileSet bằng nút chuột giữa hoặc chuột phải, và thu phóng bằng con lăn chuột hoặc các nút ở góc trên bên trái.

Nếu muốn lấy tile từ nhiều hình ảnh tilesheet cho một TileSet duy nhất, hãy tạo thêm các atlas và gán texture cho từng atlas trước khi tiếp tục. Bạn cũng có thể sử dụng một hình ảnh cho mỗi tile theo cách này (mặc dù nên sử dụng tilesheet để dễ thao tác hơn).

Bạn có thể điều chỉnh các thuộc tính của atlas trong cột giữa:

.. figure:: img/using_tilesets_properties.webp
   :align: center
   :alt: Adjusting TileSet atlas properties in the dedicated inspector (part of the TileSet panel)

   Adjusting TileSet atlas properties in the dedicated inspector (part of the TileSet panel)

Có thể điều chỉnh các thuộc tính sau trên atlas:

- **ID:** Mã định danh (duy nhất trong TileSet này), được dùng để sắp xếp. - **Name:** Tên dễ đọc dành cho atlas. Hãy sử dụng một tên mang tính mô tả để phục vụ mục đích tổ chức (chẳng hạn như "terrain", "decoration", v.v.). - **Margins:** Phần lề ở các cạnh của hình ảnh không được phép chọn làm tile (tính bằng pixel). Việc tăng giá trị này có thể hữu ích nếu bạn tải xuống một hình ảnh tilesheet có phần lề ở các cạnh (ví dụ để ghi công). - **Separation:** Khoảng cách giữa mỗi tile trên atlas, tính bằng pixel. Việc tăng giá trị này có thể hữu ích nếu hình ảnh tilesheet bạn đang sử dụng chứa các đường hướng dẫn (chẳng hạn như đường viền giữa mỗi tile). - **Texture Region Size:** Kích thước của mỗi tile trên atlas, tính bằng pixel. Trong hầu hết trường hợp, giá trị này nên khớp với kích thước tile được xác định trong thuộc tính TileMapLayer (mặc dù điều này không bắt buộc). - **Use Texture Padding:** Nếu được chọn, tùy chọn này sẽ thêm một cạnh trong suốt rộng 1 pixel xung quanh mỗi tile để ngăn hiện tượng texture bleeding khi bật tính năng lọc. Bạn nên để tùy chọn này luôn được bật, trừ khi gặp vấn đề hiển thị do texture padding.

Lưu ý rằng việc thay đổi texture margin, separation và region size có thể khiến các tile bị mất (vì một số tile sẽ nằm ngoài tọa độ của hình ảnh atlas). Để tự động tạo lại tile từ tilesheet, hãy sử dụng nút menu có ba dấu chấm dọc ở đầu trình chỉnh sửa TileSet và chọn **Create Tiles in Non-Transparent Texture Regions**:

.. figure:: img/using_tilesets_recreate_tiles_automatically.webp
   :align: center
   :alt: Recreating tiles automatically after changing atlas properties

   Recreating tiles automatically after changing atlas properties

Sử dụng một tập hợp các scene
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn cũng có thể đặt các *scene* thực tế làm tile. Điều này cho phép bạn sử dụng bất kỳ tập hợp node nào làm một tile. Ví dụ, bạn có thể dùng scene tile để đặt các thành phần gameplay, chẳng hạn như các cửa hàng mà người chơi có thể tương tác. Bạn cũng có thể dùng scene tile để đặt các AudioStreamPlayer2D (cho âm thanh môi trường), hiệu ứng hạt và nhiều thành phần khác.

.. warning::

   Scene tile có chi phí hiệu năng cao hơn so với atlas, vì mỗi scene được tạo instance riêng cho từng tile được đặt.

   Bạn chỉ nên sử dụng scene tile khi cần thiết. Để vẽ sprite trong một tile mà không cần bất kỳ thao tác nâng cao nào,
   :ref:`use atlases instead <doc_creating_tilesets_using_tilesheet>`.

Trong ví dụ này, chúng ta sẽ tạo một scene chứa node gốc CPUParticles2D. Lưu scene này vào một tệp scene (tách biệt với scene chứa TileMapLayer), sau đó chuyển sang scene chứa node TileMapLayer. Mở trình chỉnh sửa TileSet và tạo một **Scenes Collection** mới trong cột bên trái:

.. figure:: img/using_tilesets_creating_scene_collection.webp
   :align: center
   :alt: Creating a scenes collection in the TileSet editor

   Creating a scenes collection in the TileSet editor

Sau khi tạo một scenes collection, bạn có thể nhập tên mô tả cho scenes collection trong cột giữa nếu muốn. Chọn scenes collection này, sau đó tạo một scene slot mới:

.. figure:: img/using_tilesets_scene_collection_create_scene_tile.webp
   :align: center
   :alt: Creating a scene tile after selecting the scenes collection in the TileSet editor

   Creating a scene tile after selecting the scenes collection in the TileSet editor

Chọn scene slot này trong cột bên phải, sau đó sử dụng **Quick Load** (hoặc **Load**) để tải tệp scene chứa các hạt:

.. figure:: img/using_tilesets_adding_scene_tile.webp
   :align: center
   :alt: Creating a scene slot, then loading a scene file into it in the TileSet editor

   Creating a scene slot, then loading a scene file into it in the TileSet editor

Bây giờ bạn đã có một scene tile trong TileSet. Khi chuyển sang trình chỉnh sửa TileMap, bạn sẽ có thể chọn scene tile đó từ scenes collection và tô nó như bất kỳ tile nào khác.

Gộp nhiều atlas thành một atlas duy nhất
----------------------------------------

Việc sử dụng nhiều atlas trong một tài nguyên TileSet duy nhất đôi khi có thể hữu ích, nhưng cũng có thể gây bất tiện trong một số tình huống (đặc biệt nếu bạn sử dụng một hình ảnh cho mỗi tile). Godot cho phép bạn gộp nhiều atlas thành một atlas duy nhất để dễ tổ chức hơn.

Để thực hiện việc này, bạn phải có nhiều hơn một atlas được tạo trong tài nguyên TileSet. Sử dụng nút menu "three vertical dots" nằm ở cuối danh sách atlas, sau đó chọn **Open Atlas Merging Tool**:

.. figure:: img/using_tilesets_open_atlas_merging_tool.webp
   :align: center
   :alt: Opening the atlas merging tool after creating multiple atlases

   Opening the atlas merging tool after creating multiple atlases

Thao tác này sẽ mở một hộp thoại, trong đó bạn có thể chọn nhiều atlas bằng cách giữ
:kbd:`Shift` or :kbd:`Ctrl` then clicking on multiple elements:

.. figure:: img/using_tilesets_atlas_merging_tool_dialog.webp
   :align: center
   :alt: Using the atlas merging tool dialog

   Using the atlas merging tool dialog

Chọn **Merge** để gộp các atlas đã chọn thành một hình ảnh atlas duy nhất (tương ứng với một atlas duy nhất trong TileSet). Các atlas chưa được gộp sẽ bị xóa khỏi TileSet, nhưng *các hình ảnh tilesheet gốc sẽ vẫn được giữ trong hệ thống tệp*. Nếu không muốn các atlas chưa được gộp bị xóa khỏi tài nguyên TileSet, hãy chọn **Merge (Keep Original Atlases)** thay thế.

.. tip::

    TileSet có một hệ thống *tile proxy*. Tile proxy là một bảng ánh xạ cho phép thông báo cho TileMap đang sử dụng một TileSet nhất định rằng một tập hợp mã định danh tile nhất định nên được thay thế bằng một tập hợp khác.

    Tile proxy được tự động thiết lập khi gộp các atlas khác nhau, nhưng bạn cũng có thể thiết lập thủ công thông qua hộp thoại **Manage Tile Proxies**, có thể truy cập bằng menu "three vertical dots" đã đề cập ở trên.

    Việc tạo tile proxy thủ công có thể hữu ích khi bạn thay đổi ID của một atlas hoặc muốn thay thế tất cả tile từ một atlas bằng tile từ atlas khác. Lưu ý rằng khi chỉnh sửa một TileMap, bạn có thể thay thế tất cả các ô bằng giá trị ánh xạ tương ứng của chúng.

Thêm va chạm, điều hướng và che khuất vào TileSet
-------------------------------------------------

Bây giờ chúng ta đã tạo thành công một TileSet cơ bản. Chúng ta có thể bắt đầu sử dụng nó trong node TileMapLayer, nhưng hiện tại nó chưa có bất kỳ hình thức phát hiện va chạm nào. Điều này có nghĩa là người chơi và các đối tượng khác có thể đi thẳng xuyên qua sàn hoặc tường.

Nếu bạn sử dụng :ref:`2D navigation <doc_navigation_overview_2d>`, bạn cũng sẽ cần xác định các polygon điều hướng cho tile để tạo một lưới điều hướng mà các agent có thể sử dụng để tìm đường.

Cuối cùng, nếu bạn sử dụng :ref:`doc_2d_lights_and_shadows` hoặc GPUParticles2D, bạn cũng có thể muốn TileSet của mình có khả năng đổ bóng và va chạm với các hạt. Điều này yêu cầu xác định các polygon che khuất cho các tile "solid" trong TileSet.

Để có thể xác định các hình dạng va chạm, điều hướng và che khuất cho từng ô, trước tiên bạn cần tạo một lớp vật lý, điều hướng hoặc che khuất cho tài nguyên TileSet. Để thực hiện việc này, hãy chọn node TileMapLayer, nhấp vào giá trị thuộc tính TileSet trong trình kiểm tra để chỉnh sửa, sau đó mở **Physics Layers** và chọn **Add Element**:

.. figure:: img/using_tilesets_create_physics_layer.webp
   :align: center
   :alt: Creating a physics layer in the TileSet resource inspector (within the TileMapLayer node)

   Creating a physics layer in the TileSet resource inspector (within the TileMapLayer node)

Nếu bạn cũng cần hỗ trợ điều hướng, đây là lúc thích hợp để tạo một lớp điều hướng:

.. figure:: img/using_tilesets_create_navigation_layer.webp
   :align: center
   :alt: Creating a navigation layer in the TileSet resource inspector (within the TileMapLayer node)

   Creating a navigation layer in the TileSet resource inspector (within the TileMapLayer node)

Nếu bạn cần hỗ trợ các vật cản đa giác ánh sáng, đây là lúc thích hợp để tạo một lớp che khuất:

.. figure:: img/using_tilesets_create_occlusion_layer.webp
   :align: center
   :alt: Creating an occlusion layer in the TileSet resource inspector (within the TileMapLayer node)

   Creating an occlusion layer in the TileSet resource inspector (within the TileMapLayer node)

.. note::

    Các bước tiếp theo trong hướng dẫn này tập trung vào việc tạo các đa giác va chạm, nhưng quy trình dành cho điều hướng và che khuất cũng tương tự. Trình chỉnh sửa đa giác tương ứng hoạt động theo cùng một cách, vì vậy các bước này không được lặp lại để tránh dài dòng.

    Điểm cần lưu ý duy nhất là thuộc tính đa giác che khuất của ô nằm trong mục **Rendering** của trình kiểm tra atlas. Hãy mở mục này để bạn có thể chỉnh sửa đa giác.

Sau khi tạo một lớp vật lý, bạn có quyền truy cập vào mục **Physics Layer** trong trình kiểm tra atlas TileSet:

.. figure:: img/using_tilesets_selecting_collision_editor.webp
   :align: center
   :alt: Opening the collision editor while in Select mode

   Opening the collision editor while in Select mode

Bạn có thể nhanh chóng tạo một hình dạng va chạm hình chữ nhật bằng cách nhấn :kbd:`F` khi trình chỉnh sửa TileSet đang được chọn. Nếu phím tắt không hoạt động, hãy thử nhấp vào vùng trống xung quanh trình chỉnh sửa đa giác để lấy tiêu điểm:

.. figure:: img/using_tilesets_using_default_rectangle_collision.webp
   :align: center
   :alt: Using default rectangle collision shape by pressing :kbd:`F`

   Using default rectangle collision shape by pressing :kbd:`F`

Trong trình chỉnh sửa va chạm của ô này, bạn có quyền truy cập vào tất cả các công cụ chỉnh sửa đa giác 2D:

- Sử dụng thanh công cụ phía trên đa giác để chuyển đổi giữa việc tạo đa giác mới, chỉnh sửa đa giác hiện có và xóa các điểm trên đa giác. Nút menu "ba chấm dọc" cung cấp các tùy chọn bổ sung, chẳng hạn như xoay và lật đa giác. - Tạo các điểm mới bằng cách nhấp và kéo một đường giữa hai điểm. - Xóa một điểm bằng cách nhấp chuột phải vào điểm đó (hoặc sử dụng công cụ Remove được mô tả ở trên rồi nhấp chuột trái). - Di chuyển khung nhìn trong trình chỉnh sửa bằng cách nhấp chuột giữa hoặc nhấp chuột phải. (Chỉ có thể sử dụng thao tác di chuyển bằng chuột phải ở những khu vực không có điểm nào ở gần.)

Bạn có thể sử dụng hình chữ nhật mặc định để nhanh chóng tạo một hình dạng va chạm hình tam giác bằng cách xóa một trong các điểm:

.. figure:: img/using_tilesets_creating_triangle_collision.webp
   :align: center
   :alt: Creating a triangle collision shape by right-clicking one of the corners to remove it

   Creating a triangle collision shape by right-clicking one of the corners to remove it

Bạn cũng có thể sử dụng hình chữ nhật làm nền tảng cho các hình dạng phức tạp hơn bằng cách thêm nhiều điểm:

.. figure:: img/using_tilesets_drawing_custom_collision.webp
   :align: center
   :alt: Drawing a custom collision for a complex tile shape

   Drawing a custom collision for a complex tile shape

.. tip::

    Nếu bạn có một tileset lớn, việc chỉ định va chạm cho từng ô riêng lẻ có thể tốn rất nhiều thời gian. Điều này đặc biệt đúng vì TileMap thường có nhiều ô với các mẫu va chạm phổ biến (chẳng hạn như khối đặc hoặc dốc 45 độ). Để nhanh chóng áp dụng một hình dạng va chạm tương tự cho nhiều ô, hãy sử dụng chức năng để
    :ref:`assign properties to multiple tiles at once <doc_using_tilemaps_assigning_properties_to_multiple_tiles>`.

Gán siêu dữ liệu tùy chỉnh cho các ô của TileSet
------------------------------------------------

Bạn có thể gán dữ liệu tùy chỉnh cho từng ô bằng cách sử dụng *custom data layers*. Điều này có thể hữu ích để lưu trữ thông tin dành riêng cho trò chơi của bạn, chẳng hạn như lượng sát thương mà một ô sẽ gây ra khi người chơi chạm vào ô đó, hoặc liệu một ô có thể bị phá hủy bằng vũ khí hay không.

Dữ liệu được liên kết với ô trong TileSet: tất cả các thực thể của ô đã được đặt sẽ sử dụng cùng một dữ liệu tùy chỉnh. Nếu bạn cần tạo một biến thể của ô có dữ liệu tùy chỉnh khác, bạn có thể thực hiện việc này bằng :ref:`creating an alternative tile <doc_using_tilesets_creating_alternative_tiles>` và chỉ thay đổi dữ liệu tùy chỉnh cho ô thay thế.

.. figure:: img/using_tilesets_create_custom_data_layer.webp
   :align: center
   :alt: Creating a custom data layer in the TileSet resource inspector (within the TileMapLayer node)

   Creating a custom data layer in the TileSet resource inspector (within the TileMapLayer node)

.. figure:: img/using_tilesets_custom_data_layers_example.webp
   :align: center
   :alt: Example of configured custom data layers with game-specific properties

   Example of configured custom data layers with game-specific properties

Bạn có thể sắp xếp lại dữ liệu tùy chỉnh mà không làm hỏng siêu dữ liệu hiện có: trình chỉnh sửa TileSet sẽ tự động cập nhật sau khi sắp xếp lại các thuộc tính dữ liệu tùy chỉnh.

Với ví dụ về các lớp dữ liệu tùy chỉnh được hiển thị ở trên, chúng ta đang gán cho một ô siêu dữ liệu ``damage_per_second`` có giá trị ``25`` và siêu dữ liệu ``destructible`` có giá trị ``false``:

.. figure:: img/using_tilesets_edit_custom_data.webp
   :align: center
   :alt: Editing custom data in the TileSet editor while in Select mode

   Editing custom data in the TileSet editor while in Select mode

:ref:`Tile property painting <doc_using_tilemaps_using_tile_property_painting>`
cũng có thể được sử dụng cho dữ liệu tùy chỉnh:

.. figure:: img/using_tilesets_paint_custom_data.webp
   :align: center
   :alt: Assigning custom data in the TileSet editor using tile property painting

   Assigning custom data in the TileSet editor using tile property painting

.. _doc_using_tilesets_creating_terrain_sets:

Tạo các bộ địa hình (tự động lát)
---------------------------------

.. note::

    Chức năng này từng được triển khai dưới một hình thức khác với tên gọi *autotiling* trong Godot 3.x. Về cơ bản, địa hình là một phiên bản thay thế mạnh mẽ hơn của autotile. Không giống autotile, địa hình có thể hỗ trợ chuyển tiếp từ địa hình này sang địa hình khác, vì một ô có thể xác định nhiều địa hình cùng lúc.

    Không giống như trước đây, khi autotile là một loại ô cụ thể, địa hình chỉ là một tập hợp các thuộc tính được gán cho các ô atlas. Sau đó, các thuộc tính này được sử dụng bởi một chế độ vẽ TileMap chuyên dụng, chế độ này lựa chọn các ô có dữ liệu địa hình theo cách thông minh. Điều này có nghĩa là bất kỳ ô địa hình nào cũng có thể được vẽ dưới dạng địa hình hoặc dưới dạng một ô đơn, giống như mọi ô khác.

Một tileset "hoàn thiện" thường có các biến thể mà bạn nên sử dụng ở các góc hoặc cạnh của bục, sàn, v.v. Mặc dù có thể đặt chúng thủ công, việc này nhanh chóng trở nên tẻ nhạt. Xử lý tình huống này với các màn chơi được tạo theo quy trình cũng có thể khó khăn và đòi hỏi nhiều mã.

Godot cung cấp *terrains* để tự động thực hiện kiểu kết nối ô này. Điều này cho phép bạn tự động sử dụng các biến thể ô "đúng".

Các địa hình được nhóm thành các bộ địa hình. Mỗi bộ địa hình được gán một chế độ từ **Match Corners and Sides**, **Match Corners** và **Match sides**. Chúng xác định cách các địa hình được đối sánh với nhau trong một bộ địa hình.

.. note::

    Các chế độ trên tương ứng với các chế độ bitmask trước đây mà autotile sử dụng trong Godot 3.x: 2×2, 3×3 hoặc 3×3 minimal. Điều này cũng tương tự như những gì trình chỉnh sửa `Tiled <https://www.mapeditor.org/>`__ cung cấp.

Chọn node TileMapLayer, đi tới trình kiểm tra và tạo một bộ địa hình mới trong *resource* TileSet:

.. figure:: img/using_tilesets_create_terrain_set.webp
   :align: center
   :alt: Creating a terrain set in the TileSet resource inspector (within the TileMapLayer node)

   Creating a terrain set in the TileSet resource inspector (within the TileMapLayer node)

Sau khi tạo một bộ địa hình, bạn **phải** tạo một hoặc nhiều địa hình *within* bộ địa hình đó:

.. figure:: img/using_tilesets_create_terrain.webp
   :align: center
   :alt: Creating a terrain within the terrain set

   Creating a terrain within the terrain set

Trong trình chỉnh sửa TileSet, chuyển sang chế độ Select và nhấp vào một ô. Trong cột giữa, mở mục **Terrains**, sau đó gán ID bộ địa hình và ID địa hình cho ô. ``-1`` có nghĩa là "không có bộ địa hình" hoặc "không có địa hình", nghĩa là bạn phải đặt **Terrain Set** thành ``0`` hoặc lớn hơn trước khi có thể đặt **Terrain** thành ``0`` hoặc lớn hơn.

.. note::

   ID bộ địa hình và ID địa hình độc lập với nhau. Chúng cũng bắt đầu từ ``0``, không phải ``1``.

.. figure:: img/using_tilesets_configure_terrain_on_tile.webp
   :align: center
   :alt: Configuring terrain on a single tile in the TileSet editor's Select mode

   Configuring terrain on a single tile in the TileSet editor's Select mode

Sau khi thực hiện việc đó, bạn có thể cấu hình mục **Terrain Peering Bits**, mục này sẽ hiển thị trong cột giữa. Các bit liên kết địa hình xác định ô nào sẽ được đặt tùy thuộc vào các ô lân cận. ``-1`` là một giá trị đặc biệt dùng để chỉ khoảng trống.

Ví dụ: nếu một ô có tất cả các bit được đặt thành ``0`` hoặc lớn hơn, ô đó sẽ chỉ xuất hiện nếu *tất cả* 8 ô lân cận đều sử dụng một ô có cùng ID địa hình. Nếu một ô có các bit được đặt thành ``0`` hoặc lớn hơn, nhưng các bit trên-trái, trên và trên-phải được đặt thành ``-1``, ô đó sẽ chỉ xuất hiện nếu phía trên nó có khoảng trống (bao gồm cả theo đường chéo).

.. figure:: img/using_tilesets_configure_terrain_peering_bits.webp
   :align: center
   :alt: Configuring terrain peering bits on a single tile in the TileSet editor's Select mode

   Configuring terrain peering bits on a single tile in the TileSet editor's Select mode

Một cấu hình mẫu cho một tilesheet đầy đủ có thể trông như sau:

.. figure:: img/using_tilesets_terrain_example_tilesheet.webp
   :align: center
   :alt: Example full tilesheet for a sidescrolling game

   Example full tilesheet for a sidescrolling game

.. figure:: img/using_tilesets_terrain_example_tilesheet_configuration.webp
   :align: center
   :alt: Example full tilesheet for a sidescrolling game with terrain peering bits visible

   Example full tilesheet for a sidescrolling game with terrain peering bits visible

.. _doc_using_tilemaps_assigning_properties_to_multiple_tiles:

Gán thuộc tính cho nhiều ô cùng lúc
-----------------------------------

Có hai cách để gán thuộc tính cho nhiều ô cùng lúc. Tùy vào trường hợp sử dụng, một phương pháp có thể nhanh hơn phương pháp còn lại:

Sử dụng tính năng chọn nhiều ô
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn muốn cấu hình nhiều thuộc tính trên nhiều ô cùng lúc, hãy chọn chế độ **Select** ở phía trên trình chỉnh sửa TileSet:

Sau khi thực hiện việc này, bạn có thể chọn nhiều ô trong cột bên phải bằng cách giữ
:kbd:`Shift` then clicking on tiles. You can also perform rectangle selection by
giữ nút chuột trái rồi kéo chuột. Cuối cùng, bạn có thể bỏ chọn các ô đã được chọn (mà không ảnh hưởng đến phần còn lại của vùng chọn) bằng cách giữ :kbd:`Shift` rồi nhấp vào một ô đã chọn.

Sau đó, bạn có thể gán thuộc tính bằng trình kiểm tra trong cột giữa của trình chỉnh sửa TileSet. Chỉ những thuộc tính mà bạn thay đổi ở đây mới được áp dụng cho tất cả các ô đã chọn. Giống như trình kiểm tra của trình chỉnh sửa, các thuộc tính khác nhau giữa những ô đã chọn sẽ vẫn khác nhau cho đến khi bạn chỉnh sửa chúng.

Đối với các thuộc tính dạng số và màu sắc, bạn cũng sẽ thấy bản xem trước giá trị của thuộc tính trên tất cả các ô trong atlas sau khi chỉnh sửa một thuộc tính:

.. figure:: img/using_tilesets_select_and_set_tile_properties.webp
   :align: center
   :alt: Selecting multiple tiles using the Select mode, then applying properties

   Selecting multiple tiles using the Select mode, then applying properties

.. _doc_using_tilemaps_using_tile_property_painting:

Sử dụng tính năng vẽ thuộc tính ô
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn muốn áp dụng một thuộc tính duy nhất cho nhiều ô cùng lúc, bạn có thể sử dụng chế độ *property painting* cho mục đích này.

Cấu hình một thuộc tính cần vẽ trong cột giữa, sau đó nhấp vào các ô (hoặc giữ nút chuột trái) trong cột bên phải để "vẽ" các thuộc tính lên các ô.

.. figure:: img/using_tilesets_paint_tile_properties.webp
   :align: center
   :alt: Painting tile properties using the TileSet editor

   Painting tile properties using the TileSet editor

Tính năng vẽ thuộc tính ô đặc biệt hữu ích với những thuộc tính tốn nhiều thời gian để thiết lập thủ công, chẳng hạn như các hình dạng va chạm:

.. figure:: img/using_tilesets_paint_tile_properties_collision.webp
   :align: center
   :alt: Painting a collision polygon, then left-clicking tiles to apply it

   Painting a collision polygon, then left-clicking tiles to apply it

.. _doc_using_tilesets_creating_alternative_tiles:

Tạo các ô thay thế
------------------

Đôi khi, bạn muốn sử dụng một hình ảnh ô duy nhất (chỉ xuất hiện một lần trong atlas), nhưng được cấu hình theo những cách khác nhau. Ví dụ: bạn có thể muốn sử dụng cùng một hình ảnh ô, nhưng xoay, lật hoặc điều chỉnh màu khác. Bạn có thể thực hiện việc này bằng *alternative tiles*.

.. tip::

      Kể từ Godot 4.2, bạn không còn phải tạo các ô thay thế để xoay hoặc lật ô nữa. Bạn có thể xoay bất kỳ ô nào trong khi đặt ô đó trong trình chỉnh sửa TileMap bằng cách sử dụng các nút xoay/lật trên thanh công cụ của trình chỉnh sửa TileMap.

Để tạo một ô thay thế, hãy nhấp chuột phải vào một ô cơ sở trong atlas được hiển thị bởi trình chỉnh sửa TileSet, sau đó chọn **Create an Alternative Tile**:

.. figure:: img/using_tilesets_create_alternative_tile.webp
   :align: center
   :alt: Creating an alternative tile by right-clicking a base tile in the TileSet editor

   Creating an alternative tile by right-clicking a base tile in the TileSet editor

Nếu hiện đang ở chế độ Select, ô thay thế sẽ được chọn sẵn để chỉnh sửa. Nếu hiện không ở chế độ Select, bạn vẫn có thể tạo các ô thay thế, nhưng bạn sẽ cần chuyển sang chế độ Select và chọn ô thay thế để chỉnh sửa.

Nếu bạn không thấy ô thay thế, hãy di chuyển khung nhìn sang bên phải của hình ảnh atlas, vì các ô thay thế luôn xuất hiện ở bên phải các ô cơ sở của một atlas nhất định trong trình chỉnh sửa TileSet:

.. figure:: img/using_tilesets_configure_alternative_tile.webp
   :align: center
   :alt: Configuring an alternative tile after clicking it in the TileSet editor

   Configuring an alternative tile after clicking it in the TileSet editor

Sau khi chọn một tile thay thế, bạn có thể thay đổi mọi thuộc tính bằng cột giữa giống như trên tile cơ sở. Tuy nhiên, danh sách các thuộc tính được hiển thị khác với tile cơ sở:

- **Alternative ID:** Mã nhận dạng số duy nhất cho tile thay thế này. Việc thay đổi mã này sẽ làm hỏng các TileMap hiện có, vì vậy hãy cẩn thận! Mã này cũng kiểm soát thứ tự sắp xếp trong danh sách các tile thay thế được hiển thị trong trình chỉnh sửa. - **Rendering > Flip H:** Nếu ``true``, tile sẽ được lật theo chiều ngang. - **Rendering > Flip V:** Nếu ``true``, tile sẽ được lật theo chiều dọc. - **Rendering > Transpose:** Nếu ``true``, tile sẽ được xoay 90 độ *ngược chiều kim đồng hồ* rồi lật theo chiều dọc. Trên thực tế, điều này có nghĩa là để xoay tile 90 độ theo chiều kim đồng hồ mà không lật tile, bạn nên bật **Flip H** và **Transpose**. Để xoay tile 180 độ theo chiều kim đồng hồ, hãy bật **Flip H** và **Flip V**. Để xoay tile 270 độ theo chiều kim đồng hồ, hãy bật **Flip V** và **Transpose**. - **Rendering > Texture Origin:** Điểm gốc dùng để vẽ tile. Bạn có thể sử dụng thuộc tính này để tạo độ lệch trực quan cho tile so với tile cơ sở. - **Rendering > Modulate:** Hệ số màu dùng khi kết xuất tile. - **Rendering > Material:** Material dùng cho tile này. Bạn có thể sử dụng thuộc tính này để áp dụng chế độ hòa trộn khác hoặc shader tùy chỉnh cho một tile riêng lẻ. - **Z Index:** Thứ tự sắp xếp của tile này. Các giá trị cao hơn sẽ khiến tile được kết xuất ở phía trước các tile khác trên cùng một lớp. - **Y Sort Origin:** Độ lệch theo chiều dọc dùng để sắp xếp tile dựa trên tọa độ Y của tile (tính bằng pixel). Điều này cho phép sử dụng các lớp như thể chúng nằm ở những độ cao khác nhau trong các game góc nhìn từ trên xuống. Điều chỉnh thuộc tính này có thể giúp giảm các vấn đề khi sắp xếp một số tile nhất định. Chỉ có hiệu lực nếu **Y Sort Enabled** là ``true`` trên node TileMapLayer trong **CanvasItem > Ordering**

Bạn có thể tạo thêm một biến thể tile thay thế bằng cách nhấp vào biểu tượng "+" lớn bên cạnh tile thay thế. Thao tác này tương đương với việc chọn tile cơ sở rồi nhấp chuột phải vào tile đó để chọn lại **Create an Alternative Tile**.

.. note::

    Khi tạo tile thay thế, không thuộc tính nào từ tile cơ sở được kế thừa. Bạn phải thiết lập lại các thuộc tính trên tile thay thế nếu muốn chúng giống hệt nhau giữa tile cơ sở và tile thay thế.
