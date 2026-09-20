.. _doc_introduction_to_2d:

Giới thiệu về 2D
================

Các công cụ phát triển game 2D của Godot bao gồm một công cụ kết xuất 2D chuyên dụng, hệ thống vật lý và các tính năng được thiết kế riêng để tạo ra trải nghiệm 2D. Bạn có thể thiết kế màn chơi hiệu quả bằng hệ thống TileMap, tạo ảnh động cho nhân vật bằng ảnh sprite 2D hoặc ảnh động Cutout, đồng thời tận dụng ánh sáng 2D để chiếu sáng cảnh một cách linh động. Hệ thống hạt 2D tích hợp sẵn cho phép bạn tạo các hiệu ứng hình ảnh phức tạp, và Godot cũng hỗ trợ shader tùy chỉnh để nâng cao đồ họa. Kết hợp với khả năng hỗ trợ tiếp cận và tính linh hoạt của Godot, những tính năng này tạo nền tảng vững chắc để xây dựng các game 2D hấp dẫn.

.. figure:: img/2d_platformer_demo.webp

   2D Platformer Demo available on the Asset Library.

Trang này sẽ giới thiệu không gian làm việc 2D và cách làm quen với nó.

.. tip:: If you would like to get an introduction to 3D, see :ref:`doc_introduction_to_3d`.

Không gian làm việc 2D
----------------------

Bạn sẽ sử dụng không gian làm việc 2D để làm việc với các cảnh 2D, thiết kế màn chơi hoặc tạo giao diện người dùng. Để chuyển sang không gian làm việc 2D, bạn có thể chọn một nút 2D từ cây cảnh hoặc sử dụng bộ chọn không gian làm việc nằm ở cạnh trên của trình biên tập:

.. image:: img/2d_editor_viewport.webp

Tương tự như 3D, bạn có thể sử dụng các thẻ bên dưới bộ chọn không gian làm việc để chuyển đổi giữa các cảnh đang mở hoặc tạo cảnh mới bằng nút dấu cộng (+). Các dock bên trái và bên phải sẽ quen thuộc nếu bạn đã xem :ref:`editor introduction <toc-editor-interface>`.

Bên dưới bộ chọn cảnh là thanh công cụ chính, và bên dưới thanh công cụ chính là khung nhìn 2D.

Bạn có thể kéo và thả các nút tương thích từ dock FileSystem vào khung nhìn để thêm chúng dưới dạng các nút. Việc kéo và thả sẽ thêm nút được kéo dưới dạng nút anh em của nút đang chọn (nếu nút gốc được chọn thì sẽ thêm dưới dạng nút con). Giữ :kbd:`Shift` khi thả sẽ thêm nút dưới dạng nút con của nút đang chọn. Giữ :kbd:`Alt` khi thả sẽ thêm nút dưới dạng nút con của nút gốc. Nếu giữ :kbd:`Alt + Shift` khi thả, bạn có thể chọn loại nút nếu phù hợp.


Thanh công cụ chính
~~~~~~~~~~~~~~~~~~~

Một số nút trong thanh công cụ chính giống với các nút trong không gian làm việc 3D. Khi di con trỏ chuột lên một nút trong một giây, phần mô tả ngắn sẽ được hiển thị cùng với phím tắt. Một số nút có thể có chức năng bổ sung nếu nhấn thêm một phím khác. Dưới đây là phần tóm tắt chức năng chính của từng nút cùng với phím tắt mặc định, theo thứ tự từ trái sang phải:

.. image:: img/2d_toolbar.webp

- **Select Mode** (:kbd:`Q`): Cho phép chọn các nút trong khung nhìn. Nhấp chuột trái vào một nút trong khung nhìn sẽ chọn nút đó. Nhấp chuột trái và kéo một hình chữ nhật sẽ chọn tất cả các nút nằm trong ranh giới của hình chữ nhật khi thả chuột. Giữ :kbd:`Shift` trong khi chọn để thêm các nút khác vào vùng chọn. Nhấp vào một nút đã chọn trong khi giữ :kbd:`Shift` sẽ bỏ chọn nút đó. Trong chế độ này, bạn có thể kéo các nút đã chọn để di chuyển, nhấn :kbd:`Ctrl` để tạm thời chuyển sang chế độ xoay hoặc sử dụng các vòng tròn màu đỏ để thay đổi tỷ lệ. Nếu chọn nhiều nút, chỉ có thể di chuyển và xoay. Trong chế độ này, thao tác xoay và thay đổi tỷ lệ sẽ không sử dụng các tùy chọn bắt dính nếu tính năng bắt dính được bật. - **Move Mode** (:kbd:`W`): Bật chế độ di chuyển (hoặc tịnh tiến) cho các nút đã chọn. Xem
  :ref:`doc_introduction_to_2d_the_viewport` for more details.
- **Rotate Mode** (:kbd:`E`): Bật chế độ xoay cho các nút đã chọn. Xem
  :ref:`doc_introduction_to_2d_the_viewport` for more details.
- **Scale Mode** (:kbd:`S`): Bật chức năng thay đổi tỷ lệ và hiển thị các tay điều khiển thay đổi tỷ lệ trên cả hai trục cho (các) nút đã chọn. Xem :ref:`doc_introduction_to_2d_the_viewport` để biết thêm chi tiết. - **Show list of selectable nodes at position clicked**: Như mô tả cho biết, tùy chọn này cung cấp danh sách các nút có thể chọn tại vị trí đã nhấp dưới dạng menu ngữ cảnh, nếu có nhiều hơn một nút trong vùng đã nhấp. - **Rotation pivot**: Đặt tâm xoay để xoay (các) nút xung quanh đó. Theo mặc định, một nút được thêm vào có tâm xoay tại ``x: 0``, ``y: 0``, với một số ngoại lệ. Ví dụ: tâm xoay mặc định của :ref:`Sprite2D <class_Sprite2D>` là tâm của nó nếu thuộc tính ``centered`` được đặt thành ``true``. Nếu muốn thay đổi tâm xoay của một nút, hãy nhấp vào nút này rồi nhấp chuột trái để chọn vị trí mới. Nút sẽ xoay quanh điểm này. Nếu chọn nhiều nút, biểu tượng này sẽ thêm một tâm xoay tạm thời được dùng chung cho tất cả các nút đã chọn. Nhấn :kbd:`Shift` và nhấp vào nút này sẽ tạo tâm xoay tại tâm của các nút đã chọn. Nếu bất kỳ tùy chọn bắt dính nào được bật, tâm xoay cũng sẽ bắt dính vào chúng khi được kéo. - **Pan Mode** (:kbd:`G`): Cho phép điều hướng trong khung nhìn mà không vô tình chọn nút nào. Ở các chế độ khác, bạn cũng có thể giữ :kbd:`Space` và kéo bằng nút chuột trái để thực hiện thao tác tương tự. - **Ruler Mode**: Sau khi bật, hãy nhấp vào khung nhìn để hiển thị tọa độ x và y toàn cục hiện tại. Kéo từ một vị trí đến vị trí khác sẽ đo khoảng cách theo pixel. Nếu kéo theo đường chéo, thao tác này sẽ vẽ một tam giác và hiển thị các khoảng cách riêng theo x, y và tổng khoảng cách đến đích, bao gồm cả các góc so với các trục theo đơn vị độ. Phím :kbd:`R` sẽ kích hoạt thước. Nếu bật tính năng bắt dính, thước cũng hiển thị số đo theo số lượng ô lưới:

.. figure:: img/2d_ruler_with_snap.webp

   Using ruler with snapping enabled.

- **Use Smart Snap**: Bật hoặc tắt tính năng bắt dính thông minh cho các chế độ di chuyển, xoay và thay đổi tỷ lệ cũng như tâm xoay; bạn có thể tùy chỉnh tính năng này bằng menu ba dấu chấm bên cạnh các công cụ bắt dính. - **Use Grid Snap**: Bật hoặc tắt tính năng bắt dính vào lưới cho chế độ di chuyển, chế độ thay đổi tỷ lệ, tâm xoay và thước. Bạn có thể tùy chỉnh tính năng này bằng menu ba dấu chấm bên cạnh các công cụ bắt dính.

Bạn có thể tùy chỉnh các thiết lập lưới để chế độ di chuyển, chế độ xoay, chế độ thay đổi tỷ lệ, thước và tâm xoay sử dụng tính năng bắt dính. Hãy sử dụng menu ba dấu chấm cho việc này:

.. image:: img/2d_snapping_options_menu.webp

- **Use Rotation Snap**: Bật hoặc tắt tính năng bắt dính bằng thiết lập xoay đã cấu hình. - **Use Scale Snap**: Bật hoặc tắt tính năng bắt dính bằng thiết lập bước thay đổi tỷ lệ đã cấu hình. - **Snap Relative**: Bật hoặc tắt việc sử dụng tính năng bắt dính dựa trên các giá trị biến đổi hiện tại của nút được chọn. Ví dụ: nếu lưới được đặt thành 32x32 pixel và nút được chọn nằm tại ``x: 1, y: 1``, việc bật tùy chọn này sẽ tạm thời dịch chuyển lưới theo ``x: 1, y: 1``. - **Use Pixel Snap**: Bật hoặc tắt việc sử dụng các pixel phụ khi bắt dính. Nếu bật, các giá trị vị trí sẽ là số nguyên; nếu tắt, có thể di chuyển theo pixel phụ với các giá trị thập phân. Đối với thuộc tính khi chạy, hãy xem xét kiểm tra thuộc tính `Project Settings > Rendering > 2D > Snapping` dành cho các nút Node2D và `Project Settings > GUI > General > Snap Controls to Pixels` dành cho các nút Control. - **Smart Snapping**: Cung cấp một tập hợp các tùy chọn để bắt dính vào những vị trí cụ thể nếu chúng được bật:

  - Snap to Parent: Bắt dính vào các cạnh của nút cha. Ví dụ: khi tùy chọn này được bật, việc thay đổi tỷ lệ của một nút điều khiển con sẽ bắt dính vào các ranh giới của nút cha. - Snap to Node Anchor: Bắt dính vào neo của nút. Ví dụ: nếu các neo của một nút điều khiển được đặt tại những vị trí khác nhau, việc bật tùy chọn này sẽ bắt dính vào các cạnh và góc của neo. - Snap to Node Sides: Bắt dính vào các cạnh của nút, chẳng hạn như khi đặt tâm xoay hoặc vị trí neo. - Snap to Node Center: Bắt dính vào tâm của nút, chẳng hạn như khi đặt tâm xoay hoặc vị trí neo. - Snap to Other Nodes: Bắt dính vào các nút khác khi di chuyển hoặc thay đổi tỷ lệ. Hữu ích để căn chỉnh các nút trong trình biên tập. - Snap to Guides: Bắt dính vào các đường dẫn tùy chỉnh được vẽ bằng thước ngang hoặc dọc. Xem thêm về thước và đường dẫn bên dưới.

.. image:: img/2d_snapping_options.webp

- **Configure Snap**: Mở cửa sổ được hiển thị ở trên, cung cấp một tập hợp các tham số bắt dính.

  - Grid Offset: Cho phép bạn dịch chuyển lưới so với gốc tọa độ. Có thể điều chỉnh riêng ``x`` và ``y``. - Grid Step: Khoảng cách giữa mỗi lưới tính theo pixel. Có thể điều chỉnh riêng ``x`` và ``y``. - Primary Line Every: Số lượng lưới ở giữa để vẽ các đường vô hạn làm dấu hiệu cho các đường chính. - Rotation Offset: Đặt độ lệch để dịch chuyển thao tác bắt dính khi xoay. - Rotation Step: Xác định số độ bắt dính. Ví dụ, 15 nghĩa là nút sẽ xoay và bắt dính theo các bội số của 15 độ nếu tính năng bắt dính khi xoay được bật và chế độ xoay đang được sử dụng. - Scale Step: Xác định hệ số gia số thay đổi tỷ lệ. Ví dụ: nếu giá trị là 0.1, tỷ lệ sẽ thay đổi theo các bước 0.1 nếu tính năng bắt dính khi thay đổi tỷ lệ được bật và chế độ thay đổi tỷ lệ đang được sử dụng.

- **Lock selected nodes** (:kbd:`Ctrl + L`). Khóa các nút đã chọn, ngăn không cho chọn và di chuyển chúng trong khung nhìn. Nhấp lại vào nút (hoặc sử dụng :kbd:`Ctrl + Shift + L`) để mở khóa các nút đã chọn. Các nút bị khóa chỉ có thể được chọn trong cây cảnh. Bạn có thể dễ dàng nhận biết chúng nhờ biểu tượng ổ khóa bên cạnh tên nút trong cây cảnh. Nhấp vào biểu tượng ổ khóa này cũng sẽ mở khóa các nút. - **Group selected nodes** (:kbd:`Ctrl + G`). Cho phép chọn nút gốc nếu bất kỳ nút con nào được chọn. Sử dụng :kbd:`Ctrl + Shift + G` để hủy nhóm chúng. Ngoài ra, nhấp vào nút hủy nhóm trong cây cảnh cũng thực hiện thao tác tương tự. - **Skeleton Options**: Cung cấp các tùy chọn để làm việc với Skeleton2D và Bone2D.

  - Show Bones: Bật hoặc tắt khả năng hiển thị xương của nút đã chọn. - Make Bone2D Node(s) from Node(s): Chuyển đổi (các) nút đã chọn thành Bone2D.

.. seealso:: To learn more about Skeletons, see :ref:`doc_cutout_animation`.

- Menu **View**: Cung cấp các tùy chọn để điều khiển chế độ xem khung nhìn. Vì các tùy chọn của menu phụ thuộc nhiều vào khung nhìn, chúng được trình bày trong phần :ref:`doc_introduction_to_2d_the_viewport`.

Bên cạnh menu View có thể hiển thị thêm các nút khác. Trong hình ảnh thanh công cụ ở đầu chương này, một nút *Sprite2D* bổ sung xuất hiện vì một Sprite2D đang được chọn. Menu này cung cấp một số thao tác và công cụ nhanh để làm việc trên một nút hoặc vùng chọn cụ thể. Ví dụ: khi vẽ một đa giác, menu cung cấp các nút để thêm, chỉnh sửa hoặc xóa các điểm.


Hệ tọa độ
~~~~~~~~~

Trong trình biên tập 2D, không giống như 3D, chỉ có hai trục: ``x`` và ``y``. Ngoài ra, góc nhìn là cố định.

Trong viewport, bạn sẽ thấy hai đường thẳng có hai màu chạy vô tận qua màn hình: màu đỏ cho trục x và màu xanh lá cho trục y. Trong Godot, đi sang phải và đi xuống là các hướng dương. Giao điểm của hai đường thẳng này là gốc tọa độ: ``x: 0, y: 0``.

Một nút gốc sẽ có gốc tọa độ tại vị trí này sau khi được thêm vào. Việc chuyển sang chế độ `move` hoặc `scale` sau khi chọn một nút sẽ hiển thị các gizmo tại vị trí offset của nút. Các gizmo sẽ hướng theo chiều dương của trục x và y. Trong chế độ move, bạn có thể kéo đường màu xanh lá để chỉ di chuyển trên trục ``y``. Tương tự, bạn có thể giữ đường màu đỏ để chỉ di chuyển trên trục ``x``.

Trong chế độ scale, các gizmo sẽ có hình vuông. Bạn có thể giữ và kéo các hình vuông màu xanh lá và đỏ để thay đổi tỷ lệ của các nút trên trục ``y`` hoặc ``x``. Kéo theo hướng âm sẽ lật nút theo chiều ngang hoặc chiều dọc.

.. _doc_introduction_to_2d_the_viewport:

Viewport 2D
~~~~~~~~~~~

Viewport sẽ là khu vực bạn dành nhiều thời gian nhất nếu dự định thiết kế màn chơi hoặc giao diện người dùng bằng hình ảnh:

.. image:: img/2d_editor_viewport_with_viewmenu.webp

Nhấp chuột giữa và kéo chuột sẽ di chuyển khung nhìn. Các thanh cuộn ở bên phải hoặc phía dưới viewport cũng di chuyển khung nhìn. Ngoài ra, bạn có thể sử dụng các phím :kbd:`G` hoặc :kbd:`Space`. Nếu bật `Editor Settings > Editors > Panning > Simple Panning`, bạn có thể kích hoạt thao tác di chuyển khung nhìn trực tiếp chỉ bằng :kbd:`Space`, không cần kéo.

Viewport có các nút ở góc trên bên trái. **Center View** căn giữa (các) nút đã chọn trên màn hình. Tùy chọn này hữu ích khi bạn có một scene lớn với nhiều nút và muốn thấy nút đã chọn trong cây scene. Bên cạnh đó là các điều khiển thu phóng. **-** thu nhỏ, **+** phóng to, còn nhấp vào số phần trăm sẽ đặt về 100%. Ngoài ra, bạn có thể dùng thao tác cuộn chuột giữa để phóng to (cuộn lên) và thu nhỏ (cuộn xuống).

Các thanh màu đen ở cạnh trái và cạnh trên của viewport là **thước đo**. Bạn có thể sử dụng chúng để định hướng trong viewport. Theo mặc định, thước đo sẽ hiển thị tọa độ pixel của viewport, được đánh số theo các khoảng 100 pixel. Thay đổi hệ số thu phóng sẽ thay đổi các giá trị được hiển thị. Bật `Grid Snap` hoặc thay đổi các tùy chọn bắt dính sẽ cập nhật tỷ lệ của thước đo và các giá trị được hiển thị.

Bạn cũng có thể tạo nhiều đường dẫn tùy chỉnh để giúp đo lường hoặc căn chỉnh các nút theo chúng:

.. image:: img/2d_editor_guidelines.webp

Nếu scene có ít nhất một nút, bạn có thể tạo đường dẫn bằng cách kéo từ thước đo ngang hoặc dọc về phía viewport. Một đường dẫn màu tím sẽ xuất hiện, cho biết vị trí của nó và sẽ giữ nguyên tại đó khi bạn thả chuột. Bạn có thể tạo đồng thời cả đường dẫn ngang và dọc bằng cách kéo từ hình vuông màu xám tại giao điểm của các thước đo. Có thể định vị lại đường dẫn bằng cách kéo chúng trở về thước đo tương ứng, và xóa chúng bằng cách kéo hoàn toàn trở lại thước đo.

Bạn cũng có thể bật tính năng bắt dính vào các đường dẫn đã tạo bằng menu `Smart Snap`.

.. note:: If you cannot create a line, or do not see previously created guides, make sure that
          Bạn có thể kiểm tra menu `View` của viewport để xem chúng có hiển thị hay không. :kbd:`Y` bật/tắt khả năng hiển thị của chúng theo mặc định. Ngoài ra, hãy đảm bảo scene có ít nhất một nút.

Tùy thuộc vào công cụ được chọn trên thanh công cụ, nhấp chuột trái sẽ thực hiện một hành động chính trong viewport. Ví dụ, `Select Mode` sẽ chọn nút được nhấp chuột trái trong viewport. Đôi khi, nhấp chuột trái có thể kết hợp với một phím bổ trợ (ví dụ: :kbd:`Ctrl` hoặc :kbd:`Shift`) để thực hiện các hành động phụ. Ví dụ, giữ :kbd:`Shift` trong khi kéo một nút ở chế độ Select hoặc Move sẽ cố gắng bắt dính nút theo một trục duy nhất trong lúc di chuyển.

Nhấp chuột phải trong viewport cung cấp hai tùy chọn để tạo một nút hoặc khởi tạo một scene tại vị trí đã chọn. Nếu có ít nhất một nút được chọn, nhấp chuột phải cũng cung cấp tùy chọn di chuyển (các) nút đã chọn đến vị trí này.


Viewport có menu **View**, cung cấp một số tùy chọn để thay đổi giao diện của viewport:

- **Grid**: Cho phép bạn luôn hiển thị lưới, chỉ hiển thị khi sử dụng tính năng bắt dính hoặc không hiển thị. Bạn cũng có thể bật/tắt lưới bằng tùy chọn được cung cấp. - **Show Helpers**: Bật/tắt việc tạm thời hiển thị đường viền của nút cùng các thuộc tính biến đổi trước đó (vị trí, tỷ lệ hoặc góc xoay) nếu một thao tác biến đổi đã được bắt đầu. Đối với các nút `Control`, tùy chọn này cũng hiển thị các tham số kích thước. Hữu ích để xem độ chênh lệch. - **Show Rulers**: Bật/tắt khả năng hiển thị của thước đo ngang và dọc. Xem
  :ref:`doc_introduction_to_2d_the_viewport` more on rulers.
- **Show Guides**: Bật/tắt khả năng hiển thị của các đường dẫn đã tạo. Xem
  :ref:`doc_introduction_to_2d_the_viewport` for on how to create them.
- **Show Origin**: Bật/tắt hiển thị các đường gốc màu xanh lá và đỏ được vẽ tại ``x: 0, y: 0``. - **Show Viewport**: Bật/tắt khả năng hiển thị viewport mặc định của game, được biểu thị bằng một hình chữ nhật màu chàm. Đây cũng là kích thước cửa sổ mặc định trên các nền tảng máy tính, có thể thay đổi bằng cách đi đến `Project Settings > Display > Window > Size` và đặt `Viewport Width` và `Viewport Height`. - **Gizmos**: Bật/tắt khả năng hiển thị các chỉ báo `Position` (được hiển thị bằng biểu tượng chữ thập), `Lock` (được hiển thị bằng ổ khóa), `Groups` (được hiển thị bằng hai hình vuông) và `Transformation` (được hiển thị bằng các đường màu xanh lá và đỏ). - **Center Selection**: Giống nút **Center View** bên trong viewport. Căn giữa (các) nút đã chọn trong khung nhìn. :kbd:`F` là phím tắt mặc định. - **Frame to Selection**: Tương tự **Center Selection**, nhưng cũng thay đổi hệ số thu phóng để vừa nội dung với màn hình. :kbd:`Shift + F` là phím tắt mặc định. - **Clear Guides**: Xóa tất cả đường dẫn khỏi màn hình. Bạn sẽ cần tạo lại chúng nếu muốn sử dụng về sau. - **Preview Canvas Scale**: Bật/tắt bản xem trước việc thay đổi tỷ lệ canvas trong trình chỉnh sửa khi hệ số thu phóng hoặc khung nhìn của viewport thay đổi. Hữu ích để xem các điều khiển sẽ trông như thế nào sau khi được thay đổi tỷ lệ và di chuyển mà không cần chạy game. - **Preview Theme**: Cho phép chọn trong số các theme có sẵn để thay đổi giao diện của các thành phần điều khiển trong trình chỉnh sửa mà không cần chạy game.


Nút Node2D và Control
---------------------

:ref:`CanvasItem <class_CanvasItem>` is the base node for 2D. :ref:`Node2D <class_Node2D>` is the base node
dành cho các đối tượng game 2D, còn :ref:`Control <class_Control>` là nút cơ sở cho toàn bộ GUI. Đối với 3D, Godot sử dụng nút :ref:`Node3D <class_Node3D>`.

Hiển thị các nút 3D trong 2D
----------------------------

Bạn có thể hiển thị các nút 3D trong một scene 2D bằng cách sử dụng :ref:`SubViewport<class_SubViewport>`. Bạn có thể xem ví dụ này trong bản demo `3D in 2D Viewport <https://godotengine.org/asset-library/asset/2804>`__.

.. image:: img/3d_in_2d_demo_editor.webp


