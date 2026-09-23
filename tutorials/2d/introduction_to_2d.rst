.. _doc_introduction_to_2d:

Giới thiệu về 2D
================

Các công cụ phát triển game 2D của Godot bao gồm một engine kết xuất 2D chuyên dụng, hệ thống vật lý và các tính năng được thiết kế riêng cho việc tạo trải nghiệm 2D. Bạn có thể thiết kế màn chơi hiệu quả với hệ thống TileMap, tạo hoạt ảnh cho nhân vật bằng sprite 2D hoặc hoạt ảnh Cutout, đồng thời tận dụng hệ thống chiếu sáng 2D để chiếu sáng cảnh động. Hệ thống hạt 2D tích hợp sẵn cho phép bạn tạo các hiệu ứng hình ảnh phức tạp, và Godot cũng hỗ trợ shader tùy chỉnh để nâng cao đồ họa. Kết hợp lại, các tính năng này cùng khả năng hỗ trợ khả năng tiếp cận và tính linh hoạt của Godot cung cấp nền tảng vững chắc để tạo ra các game 2D hấp dẫn.

.. figure:: img/2d_platformer_demo.webp

   Bản demo 2D Platformer có trên Asset Library.

Trang này sẽ giới thiệu workspace 2D và cách làm quen với workspace này.

.. tip:: Nếu bạn muốn tìm hiểu về 3D, hãy xem :ref:`doc_introduction_to_3d`.

Workspace 2D
------------

Bạn sẽ sử dụng workspace 2D để làm việc với các scene 2D, thiết kế màn chơi hoặc tạo giao diện người dùng. Để chuyển sang workspace 2D, bạn có thể chọn một node 2D trong scene tree hoặc sử dụng bộ chọn workspace ở cạnh trên của editor:

.. image:: img/2d_editor_viewport.webp

Tương tự như 3D, bạn có thể sử dụng các tab bên dưới bộ chọn workspace để chuyển đổi giữa các scene hiện đang mở hoặc tạo scene mới bằng nút dấu cộng (+). Các dock bên trái và bên phải sẽ quen thuộc nếu bạn đã xem :ref:`phần giới thiệu editor <toc-editor-interface>`.

Bên dưới bộ chọn scene là thanh công cụ chính, và bên dưới thanh công cụ chính là viewport 2D.

Bạn có thể kéo và thả các node tương thích từ dock FileSystem vào viewport để thêm chúng dưới dạng node. Thao tác kéo và thả sẽ thêm node được kéo làm node cùng cấp với node đã chọn (nếu node gốc được chọn thì sẽ thêm làm node con). Giữ :kbd:`Shift` khi thả sẽ thêm node làm node con của node đã chọn. Giữ :kbd:`Alt` khi thả sẽ thêm node làm node con của node gốc. Nếu giữ :kbd:`Alt + Shift` khi thả, bạn có thể chọn loại node nếu phù hợp.


Thanh công cụ chính
~~~~~~~~~~~~~~~~~~~

Một số nút trong thanh công cụ chính giống với các nút trong workspace 3D. Khi di con trỏ chuột lên một nút trong một giây, phần mô tả ngắn kèm phím tắt sẽ được hiển thị. Một số nút có thể có thêm chức năng nếu nhấn thêm một phím khác. Dưới đây là phần tóm tắt chức năng chính của từng nút cùng phím tắt mặc định, theo thứ tự từ trái sang phải:

.. image:: img/2d_toolbar.webp

- **Select Mode** (:kbd:`Q`): Cho phép chọn các node trong viewport. Nhấp chuột trái vào một node trong viewport để chọn node đó. Nhấp chuột trái và kéo một hình chữ nhật sẽ chọn tất cả các node nằm trong ranh giới của hình chữ nhật khi nhả chuột. Giữ :kbd:`Shift` trong khi chọn sẽ thêm các node vào vùng chọn. Nhấp vào một node đã chọn trong khi giữ :kbd:`Shift` sẽ bỏ chọn node đó. Trong chế độ này, bạn có thể kéo các node đã chọn để di chuyển, nhấn :kbd:`Ctrl` để tạm thời chuyển sang chế độ xoay hoặc sử dụng các vòng tròn màu đỏ để scale node. Nếu chọn nhiều node, chỉ có thể di chuyển và xoay. Trong chế độ này, thao tác xoay và scale sẽ không sử dụng các tùy chọn snapping nếu snapping được bật.
- **Move Mode** (:kbd:`W`): Bật chế độ di chuyển (hoặc tịnh tiến) cho các node đã chọn. Xem
  :ref:`doc_introduction_to_2d_the_viewport` để biết thêm chi tiết.
- **Rotate Mode** (:kbd:`E`): Bật chế độ xoay cho các node đã chọn. Xem
  :ref:`doc_introduction_to_2d_the_viewport` để biết thêm chi tiết.
- **Scale Mode** (:kbd:`S`): Bật thao tác scale và hiển thị các gizmo scale trên cả hai trục cho các node đã chọn. Xem :ref:`doc_introduction_to_2d_the_viewport` để biết thêm chi tiết.
- **Show list of selectable nodes at position clicked**: Như mô tả cho thấy, tùy chọn này cung cấp danh sách các node có thể chọn tại vị trí đã nhấp dưới dạng menu ngữ cảnh nếu có nhiều hơn một node trong vùng đã nhấp.
- **Rotation pivot**: Đặt tâm xoay để xoay các node quanh đó. Theo mặc định, node được thêm có tâm xoay tại ``x: 0``, ``y: 0``, với một số ngoại lệ. Ví dụ, tâm xoay mặc định của một :ref:`Sprite2D <class_Sprite2D>` là tâm của nó nếu thuộc tính ``centered`` được đặt thành ``true``. Nếu muốn thay đổi tâm xoay của một node, hãy nhấp vào nút này rồi nhấp chuột trái để chọn vị trí mới. Node sẽ xoay quanh điểm này. Nếu chọn nhiều node, biểu tượng này sẽ thêm một tâm xoay tạm thời được dùng chung cho tất cả node đã chọn. Nhấn :kbd:`Shift` rồi nhấp vào nút này sẽ tạo tâm xoay tại tâm của các node đã chọn. Nếu bật bất kỳ tùy chọn snap nào, tâm xoay cũng sẽ snap theo chúng khi được kéo.
- **Pan Mode** (:kbd:`G`): Cho phép điều hướng trong viewport mà không vô tình chọn node nào. Trong các chế độ khác, bạn cũng có thể giữ :kbd:`Space` và kéo bằng nút chuột trái để thực hiện thao tác tương tự.
- **Ruler Mode**: Sau khi bật, hãy nhấp vào viewport để hiển thị tọa độ x và y toàn cục hiện tại. Kéo từ một vị trí đến vị trí khác sẽ đo khoảng cách theo pixel. Nếu kéo theo đường chéo, thao tác sẽ vẽ một tam giác và hiển thị riêng khoảng cách theo x, y cũng như tổng khoảng cách đến đích, bao gồm các góc với các trục tính theo độ. Phím :kbd:`R` sẽ kích hoạt thước. Nếu bật snapping, thước cũng hiển thị số đo theo số ô lưới:

.. figure:: img/2d_ruler_with_snap.webp

   Sử dụng thước khi đã bật snapping.

- **Use Smart Snap**: Bật hoặc tắt smart snapping cho các chế độ di chuyển, xoay và scale cũng như tâm xoay. Tùy chỉnh bằng menu ba dấu chấm bên cạnh các công cụ snap.
- **Use Grid Snap**: Bật hoặc tắt thao tác snap theo lưới cho chế độ di chuyển và scale, tâm xoay và thước. Tùy chỉnh bằng menu ba dấu chấm bên cạnh các công cụ snap.

Bạn có thể tùy chỉnh các thiết lập lưới để chế độ di chuyển, chế độ xoay, chế độ scale, thước và tâm xoay sử dụng snapping. Hãy sử dụng menu ba dấu chấm để thực hiện việc này:

.. image:: img/2d_snapping_options_menu.webp

- **Use Rotation Snap**: Bật hoặc tắt snapping bằng thiết lập xoay đã cấu hình.
- **Use Scale Snap**: Bật hoặc tắt snapping bằng thiết lập bước scale đã cấu hình.
- **Snap Relative**: Bật hoặc tắt việc sử dụng snapping dựa trên các giá trị transform hiện tại của node đã chọn. Ví dụ, nếu lưới được đặt thành 32x32 pixel và node đã chọn nằm tại ``x: 1, y: 1``, thì khi bật tùy chọn này, lưới sẽ tạm thời được dịch chuyển ``x: 1, y: 1``.
- **Use Pixel Snap**: Bật hoặc tắt việc sử dụng subpixel cho snapping. Nếu bật, các giá trị vị trí sẽ là số nguyên; nếu tắt, thao tác di chuyển subpixel sẽ được bật với các giá trị thập phân. Đối với thuộc tính runtime, hãy xem xét kiểm tra thuộc tính `Project Settings > Rendering > 2D > Snapping` cho các node Node2D và `Project Settings > GUI > General > Snap Controls to Pixels` cho các node Control.
- **Smart Snapping**: Cung cấp một tập hợp các tùy chọn để snap vào những vị trí cụ thể nếu chúng được bật:

  - Snap to Parent: Snap vào các cạnh của node cha. Ví dụ, khi tùy chọn này được bật, việc scale một node control con sẽ snap vào ranh giới của node cha.
  - Snap to Node Anchor: Snap vào anchor của node. Ví dụ, nếu các anchor của một node control được đặt ở những vị trí khác nhau, việc bật tùy chọn này sẽ snap vào các cạnh và góc của anchor.
  - Snap to Node Sides: Snap vào các cạnh của node, chẳng hạn như khi đặt tâm xoay hoặc anchor.
  - Snap to Node Center: Bắt dính vào tâm của node, chẳng hạn như để đặt tâm xoay hoặc vị trí neo.
  - Snap to Other Nodes: Bắt dính vào các node khác khi di chuyển hoặc thay đổi tỷ lệ. Hữu ích để căn chỉnh các node trong editor.
  - Snap to Guides: Bắt dính vào các đường dẫn tùy chỉnh được tạo bằng thước ngang hoặc dọc. Phần bên dưới sẽ nói thêm về thước và đường dẫn.

.. image:: img/2d_snapping_options.webp

- **Configure Snap**: Mở cửa sổ như minh họa ở trên, cung cấp một bộ tham số bắt dính.

  - Grid Offset: Cho phép bạn dịch chuyển các lưới so với gốc tọa độ. Có thể điều chỉnh riêng ``x`` và ``y``.
  - Grid Step: Khoảng cách giữa mỗi lưới tính bằng pixel. Có thể điều chỉnh riêng ``x`` và ``y``.
  - Primary Line Every: Số lượng lưới ở giữa để vẽ các đường vô hạn làm chỉ báo cho các đường chính.
  - Rotation Offset: Đặt độ lệch để dịch chuyển việc bắt dính khi xoay.
  - Rotation Step: Xác định số độ bắt dính. Ví dụ, 15 nghĩa là node sẽ xoay và bắt dính tại các bội số của 15 độ nếu bật bắt dính khi xoay và sử dụng chế độ xoay.
  - Scale Step: Xác định hệ số gia số khi thay đổi tỷ lệ. Ví dụ, nếu giá trị là 0.1, tỷ lệ sẽ thay đổi theo các bước 0.1 nếu bật bắt dính khi thay đổi tỷ lệ và sử dụng chế độ thay đổi tỷ lệ.

- **Lock selected nodes** (:kbd:`Ctrl + L`). Khóa các node đã chọn, ngăn việc chọn và di chuyển chúng trong viewport. Nhấp lại vào nút này (hoặc sử dụng :kbd:`Ctrl + Shift + L`) sẽ mở khóa các node đã chọn. Chỉ có thể chọn các node bị khóa trong scene tree. Có thể dễ dàng nhận biết chúng nhờ biểu tượng ổ khóa bên cạnh tên node trong scene tree. Nhấp vào biểu tượng ổ khóa này cũng sẽ mở khóa các node.
- **Group selected nodes** (:kbd:`Ctrl + G`). Cho phép chọn node gốc nếu bất kỳ node con nào được chọn. Sử dụng :kbd:`Ctrl + Shift + G` để bỏ nhóm chúng. Ngoài ra, nhấp vào nút bỏ nhóm trong scene tree cũng thực hiện thao tác tương tự.
- **Skeleton Options**: Cung cấp các tùy chọn để làm việc với Skeleton2D và Bone2D.

  - Show Bones: Bật hoặc tắt khả năng hiển thị các bone của node đã chọn.
  - Make Bone2D Node(s) from Node(s): Chuyển các node đã chọn thành Bone2D.

.. seealso:: Để tìm hiểu thêm về Skeleton, hãy xem :ref:`doc_cutout_animation`.

- **View** menu: Cung cấp các tùy chọn để điều khiển chế độ xem viewport. Vì các tùy chọn phụ thuộc nhiều vào viewport, phần này được trình bày trong mục :ref:`doc_introduction_to_2d_the_viewport`.

Bên cạnh menu View, có thể sẽ hiển thị thêm các nút. Trong hình ảnh thanh công cụ ở đầu chương này, một nút *Sprite2D* bổ sung xuất hiện vì một Sprite2D đang được chọn. Menu này cung cấp một số thao tác và công cụ nhanh để làm việc trên một node hoặc vùng chọn cụ thể. Ví dụ, khi vẽ một polygon, menu cung cấp các nút để thêm, sửa đổi hoặc xóa các điểm.


Hệ tọa độ
~~~~~~~~~

Trong editor 2D, không giống như 3D, chỉ có hai trục: ``x`` và ``y``. Ngoài ra, góc nhìn là cố định.

Trong viewport, bạn sẽ thấy hai đường có hai màu chạy vô hạn ngang qua màn hình: màu đỏ cho trục x và màu xanh lá cho trục y. Trong Godot, hướng sang phải và hướng xuống là các hướng dương. Giao điểm của hai đường này là gốc tọa độ: ``x: 0, y: 0``.

Một node gốc sẽ có gốc tọa độ tại vị trí này sau khi được thêm vào. Chuyển sang chế độ `move` hoặc `scale` sau khi chọn một node sẽ hiển thị các gizmo tại vị trí lệch của node. Các gizmo sẽ chỉ về các hướng dương của trục x và y. Trong chế độ di chuyển, bạn có thể kéo đường màu xanh lá để chỉ di chuyển trên trục ``y``. Tương tự, bạn có thể giữ và kéo đường màu đỏ để chỉ di chuyển trên trục ``x``.

Trong chế độ thay đổi tỷ lệ, các gizmo sẽ có dạng hình vuông. Bạn có thể giữ và kéo các hình vuông màu xanh lá và đỏ để thay đổi tỷ lệ của các node trên trục ``y`` hoặc ``x``. Kéo theo hướng âm sẽ lật node theo chiều ngang hoặc dọc.

.. _doc_introduction_to_2d_the_viewport:

Viewport 2D
~~~~~~~~~~~

Viewport sẽ là khu vực bạn dành nhiều thời gian nhất nếu dự định thiết kế level hoặc giao diện người dùng theo cách trực quan:

.. image:: img/2d_editor_viewport_with_viewmenu.webp

Nhấp chuột giữa và kéo chuột sẽ di chuyển khung nhìn. Các thanh cuộn ở bên phải hoặc phía dưới viewport cũng di chuyển khung nhìn. Ngoài ra, có thể sử dụng các phím :kbd:`G` hoặc :kbd:`Space`. Nếu bật `Editor Settings > Editors > Panning > Simple Panning`, bạn có thể kích hoạt thao tác di chuyển khung nhìn trực tiếp chỉ bằng :kbd:`Space`, không cần kéo.

Viewport có các nút ở góc trên bên trái. **Center View** căn giữa các node đã chọn trên màn hình. Tùy chọn này hữu ích khi bạn có một scene lớn với nhiều node và muốn xem node đang được chọn trong scene tree. Bên cạnh đó là các điều khiển thu phóng. **-** thu nhỏ, **+** phóng to, còn nhấp vào số phần trăm sẽ đặt về 100%. Ngoài ra, bạn có thể dùng con lăn chuột giữa để phóng to (cuộn lên) và thu nhỏ (cuộn xuống).

Các thanh màu đen ở cạnh trái và cạnh trên của viewport là **rulers**. Bạn có thể sử dụng chúng để định hướng trong viewport. Theo mặc định, các thước hiển thị tọa độ pixel của viewport, được đánh số theo từng bước 100 pixel. Thay đổi hệ số thu phóng sẽ thay đổi các giá trị được hiển thị. Bật `Grid Snap` hoặc thay đổi các tùy chọn bắt dính sẽ cập nhật tỷ lệ của thước và các giá trị được hiển thị.

Bạn cũng có thể tạo nhiều đường dẫn tùy chỉnh để hỗ trợ đo đạc hoặc căn chỉnh các node theo chúng:

.. image:: img/2d_editor_guidelines.webp

Nếu scene có ít nhất một node, bạn có thể tạo đường dẫn bằng cách kéo từ thước ngang hoặc dọc về phía viewport. Một đường dẫn màu tím sẽ xuất hiện, hiển thị vị trí của nó và vẫn ở đó khi bạn thả chuột. Bạn có thể tạo đồng thời cả đường dẫn ngang và dọc bằng cách kéo từ ô vuông màu xám tại giao điểm của các thước. Có thể định vị lại đường dẫn bằng cách kéo chúng trở lại các thước tương ứng, và xóa chúng bằng cách kéo hoàn toàn trở lại thước.

Bạn cũng có thể bật tính năng bắt dính vào các đường dẫn đã tạo bằng menu `Smart Snap`.

.. note:: Nếu không thể tạo đường hoặc không thấy các đường dẫn đã tạo trước đó, hãy đảm bảo chúng đang hiển thị bằng cách kiểm tra menu `View` của viewport. Theo mặc định, :kbd:`Y` sẽ bật hoặc tắt khả năng hiển thị của chúng. Ngoài ra, hãy đảm bảo scene có ít nhất một node.

Tùy thuộc vào công cụ được chọn trên thanh công cụ, nhấp chuột trái sẽ thực hiện một thao tác chính trong viewport. Ví dụ, `Select Mode` sẽ chọn node được nhấp bằng chuột trái trong viewport. Đôi khi, có thể kết hợp thao tác nhấp chuột trái với một phím bổ trợ (ví dụ: :kbd:`Ctrl` hoặc :kbd:`Shift`) để thực hiện các thao tác phụ. Ví dụ, giữ :kbd:`Shift` trong khi kéo một node ở chế độ Select hoặc Move sẽ cố gắng bắt dính node trên một trục duy nhất khi di chuyển.

Nhấp chuột phải trong viewport cung cấp hai tùy chọn để tạo một node hoặc khởi tạo một scene tại vị trí đã chọn. Nếu có ít nhất một node được chọn, nhấp chuột phải cũng cung cấp tùy chọn di chuyển các node đã chọn đến vị trí này.


Viewport có menu **View**, cung cấp một số tùy chọn để thay đổi giao diện của viewport:

- **Grid**: Cho phép bạn luôn hiển thị các lưới, chỉ hiển thị khi sử dụng tính năng bắt dính hoặc không hiển thị. Bạn cũng có thể bật hoặc tắt chúng bằng tùy chọn được cung cấp.
- **Show Helpers**: Bật/tắt tạm thời hiển thị đường bao của node, cùng với các thuộc tính transform trước đó (vị trí, tỷ lệ hoặc phép xoay) nếu một thao tác transform đã được bắt đầu. Đối với các node `Control`, phần này cũng hiển thị các tham số định kích thước. Hữu ích để xem các delta.
- **Show Rulers**: Bật/tắt khả năng hiển thị của thước ngang và dọc. Xem
  :ref:`doc_introduction_to_2d_the_viewport` để biết thêm về thước.
- **Show Guides**: Bật/tắt khả năng hiển thị của các guide đã tạo. Xem
  :ref:`doc_introduction_to_2d_the_viewport` để biết cách tạo chúng.
- **Show Origin**: Bật/tắt hiển thị các đường gốc màu xanh lá và đỏ được vẽ tại ``x: 0, y: 0``.
- **Show Viewport**: Bật/tắt khả năng hiển thị viewport mặc định của game, được biểu thị bằng một hình chữ nhật màu chàm. Đây cũng là kích thước cửa sổ mặc định trên các nền tảng desktop, có thể thay đổi bằng cách đi tới `Project Settings > Display > Window > Size` và thiết lập `Viewport Width` và `Viewport Height`.
- **Gizmos**: Bật/tắt khả năng hiển thị các chỉ báo `Position` (hiển thị bằng biểu tượng dấu thập), `Lock` (hiển thị bằng ổ khóa), `Groups` (hiển thị bằng hai hình vuông) và `Transformation` (hiển thị bằng các đường màu xanh lá và đỏ).
- **Center Selection**: Tương tự nút **Center View** bên trong viewport. Đưa các node đã chọn vào giữa vùng xem. :kbd:`F` là phím tắt mặc định.
- **Frame to Selection**: Tương tự `Center Selection`, nhưng đồng thời thay đổi hệ số zoom để vừa với nội dung trên màn hình. :kbd:`Shift + F` là phím tắt mặc định.
- **Clear Guides**: Xóa tất cả guide khỏi màn hình. Bạn sẽ cần tạo lại chúng nếu dự định sử dụng sau này.
- **Preview Canvas Scale**: Bật/tắt chế độ xem trước việc scale canvas trong editor khi hệ số zoom hoặc chế độ xem viewport thay đổi. Hữu ích để xem các control sẽ trông như thế nào sau khi scale và di chuyển mà không cần chạy game.
- **Preview Theme**: Cho phép chọn từ các theme hiện có để thay đổi giao diện của các mục control trong editor mà không cần chạy game.


Node2D và node Control
----------------------

:ref:`CanvasItem <class_CanvasItem>` là node cơ sở cho 2D. :ref:`Node2D <class_Node2D>` là node cơ sở cho các đối tượng game 2D, còn :ref:`Control <class_Control>` là node cơ sở cho mọi thành phần GUI. Đối với 3D, Godot sử dụng node :ref:`Node3D <class_Node3D>`.

Hiển thị node 3D trong 2D
-------------------------

Có thể hiển thị các node 3D trong một scene 2D bằng cách sử dụng :ref:`SubViewport<class_SubViewport>`. Bạn có thể xem điều này trong bản demo `3D trong Viewport 2D <https://godotengine.org/asset-library/asset/2804>`__.

.. image:: img/3d_in_2d_demo_editor.webp


