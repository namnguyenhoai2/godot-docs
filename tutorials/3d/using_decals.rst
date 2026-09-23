.. _doc_using_decals:

Sử dụng decal
=============

.. note::

    Decal chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong renderer Compatibility.

    Nếu sử dụng renderer Compatibility, hãy cân nhắc dùng Sprite3D làm giải pháp thay thế để chiếu decal lên các bề mặt (phần lớn) phẳng.

Decal là các texture được chiếu lên các bề mặt đục hoặc trong suốt trong không gian 3D. Việc chiếu này diễn ra theo thời gian thực và không phụ thuộc vào quá trình tạo mesh. Nhờ đó, bạn có thể di chuyển decal ở mỗi frame với ảnh hưởng nhỏ đến hiệu năng, ngay cả khi áp dụng lên các mesh phức tạp.

Mặc dù decal không thể thêm chi tiết hình học thực tế lên bề mặt được chiếu, chúng vẫn có thể tận dụng phương pháp kết xuất dựa trên vật lý để cung cấp các thuộc tính tương tự như vật liệu :abbr:`PBR (Physically-Based Rendering)` hoàn chỉnh.

Trong trang này, bạn sẽ tìm hiểu:

- Cách thiết lập decal trong trình chỉnh sửa 3D.
- Cách tạo decal trong khi chơi trong một cảnh 3D (chẳng hạn như vết đạn).
- Cách cân bằng cấu hình decal giữa hiệu năng và chất lượng.

.. seealso::

    Kho lưu trữ các dự án demo của Godot có chứa `bản demo decal 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/decals>`__.

    Nếu bạn muốn viết văn bản 3D tùy ý lên trên một bề mặt, hãy sử dụng
    :ref:`doc_3d_text` được đặt gần bề mặt thay vì một node Decal.

Các trường hợp sử dụng
----------------------

Trang trí tĩnh
~~~~~~~~~~~~~~

Đôi khi, cách nhanh nhất để thêm chi tiết texture vào một cảnh là sử dụng decal. Điều này đặc biệt phù hợp với các chi tiết hữu cơ, chẳng hạn như những mảng đất hoặc cát rải rác trên một bề mặt lớn. Decal có thể giúp phá vỡ sự lặp lại của texture trong cảnh và khiến các họa tiết trông tự nhiên hơn. Ở quy mô nhỏ hơn, decal cũng có thể được dùng để tạo các biến thể chi tiết cho vật thể. Ví dụ, decal có thể được dùng để thêm đai ốc và bu-lông lên trên hình học bề mặt cứng.

Vì decal có thể thêm các thuộc tính :abbr:`PBR (Physically-Based Rendering)` riêng lên trên các bề mặt được chiếu, chúng cũng có thể được dùng để tạo dấu chân hoặc vũng nước ướt.

.. figure:: img/decals_dirt.webp
   :align: center
   :alt: Đất được thêm lên trên hình học của màn chơi bằng decal

   Đất được thêm lên trên hình học của màn chơi bằng decal

Các yếu tố gameplay động
~~~~~~~~~~~~~~~~~~~~~~~~

Decal có thể thể hiện các hiệu ứng gameplay tạm thời hoặc lâu dài, chẳng hạn như vết đạn và vết cháy do vụ nổ.

Bằng cách sử dụng node AnimationPlayer hoặc một script, decal có thể được làm mờ dần theo thời gian (sau đó được xóa bằng ``queue_free()``) để cải thiện hiệu năng.

Bóng dạng đốm
~~~~~~~~~~~~~

Bóng dạng đốm thường được sử dụng trong các dự án mobile (hoặc để theo đuổi phong cách nghệ thuật retro), vì chiếu sáng theo thời gian thực thường quá tốn kém trên các thiết bị mobile cấp thấp. Tuy nhiên, khi dựa vào lightmap được bake với ánh sáng được bake hoàn toàn, các vật thể động sẽ không đổ *bất kỳ* bóng nào từ những nguồn sáng đó. Điều này khiến các vật thể động trong những cảnh sử dụng lightmap trông phẳng hơn so với chiếu sáng theo thời gian thực, gần như thể chúng đang lơ lửng.

Nhờ bóng dạng đốm, các vật thể động vẫn có thể đổ bóng gần đúng. Điều này không chỉ giúp cảm nhận chiều sâu trong cảnh mà còn có thể trở thành một yếu tố gameplay, đặc biệt trong các game platformer 3D. Có thể kéo dài bóng dạng đốm để cho người chơi biết họ sẽ tiếp đất ở đâu nếu rơi thẳng xuống.

Ngay cả với chiếu sáng theo thời gian thực, bóng dạng đốm vẫn có thể hữu ích như một dạng ambient occlusion trong những tình huống SSAO quá tốn kém hoặc quá thiếu ổn định do bản chất screen-space của nó. Ví dụ, bóng bên dưới xe được thể hiện khá tốt bằng bóng dạng đốm.

.. figure:: img/decals_blob_shadow.webp
   :align: center
   :alt: So sánh bóng dạng đốm bên dưới vật thể

   So sánh bóng dạng đốm bên dưới vật thể

Hướng dẫn bắt đầu nhanh
-----------------------

Tạo decal trong trình chỉnh sửa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Tạo một node Decal trong trình chỉnh sửa 3D.
2. Trong inspector, mở rộng mục **Textures** và tải một texture vào **Textures > Albedo**.
3. Di chuyển node Decal về phía một vật thể, sau đó xoay nó để decal hiển thị (và có đúng hướng). Nếu decal bị phản chiếu, hãy thử xoay nó 180 độ. Bạn có thể kiểm tra lại hướng của decal bằng cách tăng **Parameters > Normal Fade** lên 0.5. Điều này sẽ ngăn Decal được chiếu lên các bề mặt không hướng về phía decal.
4. Nếu decal của bạn chỉ dành cho các vật thể tĩnh, hãy cấu hình để decal không ảnh hưởng đến các vật thể động (hoặc ngược lại). Để làm vậy, thay đổi thuộc tính **Cull Mask** của decal nhằm loại trừ một số layer nhất định. Sau đó, sửa các node MeshInstance3D của vật thể động để thay đổi visibility layer của chúng. Chẳng hạn, bạn có thể chuyển chúng từ layer 1 sang layer 2, rồi tắt layer 2 trong thuộc tính **Cull Mask** của decal.

Các thuộc tính của node Decal
-----------------------------

- **Extents:** Kích thước của decal. Trục Y xác định độ dài phép chiếu của decal. Hãy giữ độ dài phép chiếu ngắn nhất có thể để tăng cơ hội culling, từ đó cải thiện hiệu năng.

Texture
~~~~~~~

- **Albedo:** Map albedo (diffuse/màu) dùng cho decal. Trong hầu hết các trường hợp, đây là texture bạn nên thiết lập đầu tiên. Nếu sử dụng map normal hoặc ORM, bạn *phải* đặt map albedo để cung cấp kênh alpha. Kênh alpha này sẽ được dùng làm mask nhằm xác định mức độ ảnh hưởng của các map normal/ORM lên bề mặt bên dưới.
- **Normal:** Map normal dùng cho decal. Map này có thể được dùng để tăng chi tiết cảm nhận được trên decal bằng cách thay đổi cách ánh sáng phản ứng với decal. Ảnh hưởng của texture này được nhân với kênh alpha của texture albedo (nhưng không phải **Albedo Mix**).
- **ORM:** Map Occlusion/Roughness/Metallic dùng cho decal. Đây là định dạng được tối ưu để lưu các map vật liệu PBR. Map Ambient Occlusion được lưu trong kênh đỏ, map roughness trong kênh xanh lá và map metallic trong kênh xanh dương. Ảnh hưởng của texture này được nhân với kênh alpha của texture albedo (nhưng không phải **Albedo Mix**).
- **Emission:** Texture emission dùng cho decal. Không giống **Albedo**, texture này sẽ phát sáng trong bóng tối.

Thông số
~~~~~~~~

- **Emission Energy:** Độ sáng của texture emission.
- **Modulate:** Nhân màu của các texture albedo và emission. Dùng tùy chọn này để đổi màu decal (ví dụ: cho decal sơn hoặc để tăng sự đa dạng bằng cách ngẫu nhiên hóa modulation của từng decal).
- **Albedo Mix:** Độ mờ của texture albedo. Không giống như khi sử dụng texture albedo với kênh alpha trong suốt hơn, việc giảm giá trị này xuống dưới ``1.0`` *không* làm giảm ảnh hưởng của texture normal/ORM lên bề mặt bên dưới. Đặt giá trị này thành ``0.0`` khi tạo các decal chỉ có normal/ORM, chẳng hạn như dấu chân hoặc vũng nước ướt.
- **Normal Fade:** Làm mờ Decal nếu góc giữa Decal và
  :abbr:`AABB (Axis-Aligned Bounding Box)` của nó với bề mặt đích trở nên quá lớn. Giá trị ``0.0`` sẽ chiếu decal bất kể góc nào, còn giá trị ``0.999`` sẽ giới hạn decal ở các bề mặt gần như vuông góc. Đặt **Normal Fade** thành giá trị lớn hơn ``0.0`` sẽ gây tốn một ít hiệu năng do phải tính toán thêm góc của normal.

Vertical Fade
~~~~~~~~~~~~~

- **Upper Fade:** Đường cong mà decal sẽ mờ dần khi bề mặt càng cách xa tâm của :abbr:`AABB (Axis-Aligned Bounding Box)` (về phía góc chiếu của decal). Chỉ các giá trị dương mới hợp lệ.
- **Lower Fade:** Đường cong mà decal sẽ mờ dần khi bề mặt càng cách xa tâm của :abbr:`AABB (Axis-Aligned Bounding Box)` (ra xa góc chiếu của decal). Chỉ các giá trị dương mới hợp lệ.

Distance Fade
~~~~~~~~~~~~~

- **Enabled:** Điều khiển việc bật distance fade (một dạng :abbr:`LOD (Level of Detail)`). Decal sẽ mờ dần trong khoảng **Begin + Length**, sau đó sẽ bị loại bỏ và hoàn toàn không được gửi đến shader. Sử dụng tùy chọn này để giảm số decal đang hoạt động trong một scene, từ đó cải thiện hiệu năng.
- **Begin:** Khoảng cách từ camera tại đó decal bắt đầu mờ đi (tính theo đơn vị 3D).
- **Length:** Khoảng cách mà decal mờ dần (tính theo đơn vị 3D). Decal sẽ dần trở nên trong suốt hơn trong khoảng cách này và hoàn toàn không nhìn thấy ở cuối khoảng cách. Giá trị cao hơn tạo ra quá trình chuyển tiếp mờ dần mượt hơn, phù hợp hơn khi camera di chuyển nhanh.

Cull Mask
~~~~~~~~~

- **Cull Mask:** Chỉ định các lớp VisualInstance3D mà decal này sẽ chiếu lên. Theo mặc định, decal ảnh hưởng đến tất cả các lớp. Tùy chọn này cho phép bạn chỉ định loại đối tượng nào nhận decal và loại nào không. Điều này đặc biệt hữu ích để bảo đảm các đối tượng động không vô tình nhận Decal vốn dành cho địa hình bên dưới chúng.

Decal rendering order
---------------------

Theo mặc định, decal được sắp xếp dựa trên kích thước :abbr:`AABB (Axis-Aligned Bounding Box)` và khoảng cách đến camera. Các AABB gần camera hơn được render trước, nghĩa là thứ tự render decal đôi khi có thể thay đổi tùy theo vị trí camera nếu một số decal nằm cùng vị trí.

Để khắc phục điều này, bạn có thể điều chỉnh thuộc tính **Sorting Offset** trong phần VisualInstance3D của trình kiểm tra node Decal. Offset này không phải là thứ tự ưu tiên tuyệt đối, mà là một *guideline* được renderer sử dụng, vì kích thước AABB vẫn ảnh hưởng đến cách sắp xếp decal. Do đó, các giá trị cao hơn sẽ *luôn* khiến decal được vẽ phía trên các decal khác có sorting offset thấp hơn.

Nếu muốn bảo đảm một decal luôn được render phía trên các decal khác, bạn cần đặt thuộc tính **Sorting Offset** của nó thành một giá trị dương lớn hơn độ dài AABB của decal lớn nhất có thể chồng lên nó. Để decal này được vẽ phía sau các decal khác, hãy đặt **Sorting Offset** thành cùng giá trị nhưng âm.

.. figure:: img/decals_sorting_offset.webp
   :align: center
   :alt: So sánh VisualInstance3D Sorting Offset trên các Decal

   So sánh VisualInstance3D Sorting Offset trên các Decal

Điều chỉnh hiệu năng và chất lượng
----------------------------------

Hiệu năng render decal chủ yếu được quyết định bởi phần diện tích chúng chiếm trên màn hình, nhưng số lượng decal cũng ảnh hưởng. Nhìn chung, một vài decal lớn bao phủ phần lớn màn hình sẽ tốn chi phí render hơn nhiều decal nhỏ được phân tán.

Để cải thiện hiệu năng render, bạn có thể bật thuộc tính **Distance Fade** như mô tả ở trên. Điều này sẽ làm các decal ở xa mờ dần khi cách xa camera (và có thể ít hoặc không ảnh hưởng đến kết quả render cuối cùng của scene). Khi sử dụng node groups, bạn cũng có thể ngăn các decal trang trí không thiết yếu được tạo ra dựa trên cấu hình của người dùng.

Cách render decal cũng ảnh hưởng đến hiệu năng. Phần
:ref:`Rendering > Textures > Decals > Filter <class_ProjectSettings_property_rendering/textures/decals/filter>` trong phần cài đặt project nâng cao cho phép bạn kiểm soát cách lọc texture decal. **Nearest/Linear** không sử dụng mipmap. Tuy nhiên, decal sẽ có vẻ nhiễu hạt khi ở xa. **Nearest/Linear Mipmaps** sẽ trông mượt hơn ở xa, nhưng decal sẽ bị mờ khi nhìn từ các góc xiên. Có thể khắc phục điều này bằng cách sử dụng **Nearest/Linear Mipmaps Anisotropic**, tùy chọn cung cấp chất lượng cao nhất nhưng cũng render chậm hơn.

Nếu project của bạn có phong cách pixel art, hãy cân nhắc đặt bộ lọc thành một trong các giá trị **Nearest** để decal sử dụng bộ lọc điểm gần nhất. Nếu không, hãy dùng **Linear**.

Hạn chế
-------

Decal không thể ảnh hưởng đến các thuộc tính vật liệu ngoài những thuộc tính được liệt kê ở trên, chẳng hạn như chiều cao (để lập bản đồ thị sai).

Vì lý do hiệu năng, decal sử dụng logic render cố định hoàn toàn. Điều này có nghĩa là decal không thể sử dụng shader tùy chỉnh. Tuy nhiên, shader tùy chỉnh trên các bề mặt được chiếu có thể đọc thông tin bị decal ghi đè trên chúng, chẳng hạn như độ nhám và tính kim loại.

Khi sử dụng renderer Forward+, Godot dùng phương pháp *clustering* để render decal. Có thể thêm bao nhiêu decal tùy ý (miễn là hiệu năng cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered elements* có thể hiện diện trong chế độ xem hiện tại của camera. Một clustered element có thể là omni light, spot light, area light, một :ref:`decal <doc_using_decals>`, hoặc một
:ref:`reflection probe <doc_reflection_probes>`. Có thể tăng giới hạn này bằng cách điều chỉnh
:ref:`Max Clustered Elements <class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>` trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng renderer Mobile, chỉ có thể áp dụng 8 decal trên mỗi *resource* Mesh riêng lẻ. Nếu có nhiều decal hơn ảnh hưởng đến một mesh, không phải tất cả chúng đều được render trên mesh đó.
