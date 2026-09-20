.. _doc_using_decals:

Sử dụng decal
=============

.. note::

    Decal chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong renderer Compatibility.

    Nếu sử dụng renderer Compatibility, hãy cân nhắc dùng Sprite3D làm phương án thay thế để chiếu decal lên các bề mặt (chủ yếu) phẳng.

Decal là các texture được chiếu lên các bề mặt opaque hoặc transparent trong 3D. Việc chiếu này diễn ra theo thời gian thực và không phụ thuộc vào việc tạo mesh. Nhờ đó, bạn có thể di chuyển decal ở mỗi frame với chỉ một tác động nhỏ đến hiệu năng, ngay cả khi áp dụng lên các mesh phức tạp.

Mặc dù decal không thể thêm chi tiết geometry thực tế lên bề mặt được chiếu, decal vẫn có thể sử dụng physically-based rendering để cung cấp các thuộc tính tương tự như các material :abbr:`PBR (Physically-Based Rendering)` đầy đủ.

Trong trang này, bạn sẽ tìm hiểu:

- Cách thiết lập decal trong 3D editor. - Cách tạo decal trong khi gameplay diễn ra trong một 3D scene (chẳng hạn như vết đạn). - Cách cân bằng cấu hình decal giữa hiệu năng và chất lượng.

.. seealso::

    Repository các demo project của Godot có một `3D decals demo <https://github.com/godotengine/godot-demo-projects/tree/master/3d/decals>`__.

    Nếu bạn muốn viết văn bản 3D tùy ý lên trên một bề mặt, hãy sử dụng
    :ref:`doc_3d_text` placed close to a surface instead of a Decal node.

Trường hợp sử dụng
------------------

Trang trí tĩnh
~~~~~~~~~~~~~~

Đôi khi, cách nhanh nhất để thêm chi tiết texture vào một scene là sử dụng decal. Điều này đặc biệt đúng với các chi tiết hữu cơ, chẳng hạn như những mảng đất hoặc cát rải rác trên một bề mặt lớn. Decal có thể giúp phá vỡ sự lặp lại của texture trong scene và khiến các pattern trông tự nhiên hơn. Ở quy mô nhỏ hơn, decal cũng có thể được dùng để tạo ra các biến thể chi tiết cho object. Ví dụ, decal có thể được dùng để thêm đai ốc và bu-lông lên trên geometry hard-surface.

Vì decal có thể đưa các thuộc tính :abbr:`PBR (Physically-Based Rendering)` của riêng chúng lên trên các bề mặt được chiếu, chúng cũng có thể được dùng để tạo dấu chân hoặc vũng nước ướt.

.. figure:: img/decals_dirt.webp
   :align: center
   :alt: Dirt added on top of level geometry using decals

   Dirt added on top of level geometry using decals

Các yếu tố gameplay động
~~~~~~~~~~~~~~~~~~~~~~~~

Decal có thể biểu diễn các hiệu ứng gameplay tạm thời hoặc kéo dài, chẳng hạn như vết đạn và vết cháy do vụ nổ.

Bằng cách sử dụng node AnimationPlayer hoặc một script, decal có thể được cho mờ dần theo thời gian (sau đó được xóa bằng ``queue_free()``) để cải thiện hiệu năng.

Bóng blob
~~~~~~~~~

Bóng blob thường được sử dụng trong các project mobile (hoặc để theo đuổi phong cách nghệ thuật retro), vì lighting theo thời gian thực thường quá tốn kém trên các thiết bị mobile cấp thấp. Tuy nhiên, khi dựa vào lightmap đã bake với các light được bake hoàn toàn, các object động sẽ không đổ *bất kỳ* bóng nào từ những light đó. Điều này khiến các object động trong scene sử dụng lightmap trông phẳng hơn so với lighting theo thời gian thực, gần như khiến các object động trông như đang lơ lửng.

Nhờ bóng blob, các object động vẫn có thể đổ bóng gần đúng. Điều này không chỉ giúp cảm nhận độ sâu trong scene, mà còn có thể trở thành một yếu tố gameplay, đặc biệt trong các game platformer 3D. Có thể kéo dài bóng blob để cho người chơi biết họ sẽ tiếp đất ở đâu nếu rơi thẳng xuống.

Ngay cả với lighting theo thời gian thực, bóng blob vẫn có thể hữu ích như một dạng ambient occlusion trong những tình huống mà SSAO quá tốn kém hoặc quá không ổn định do bản chất screen-space của nó. Ví dụ, bóng bên dưới xe được thể hiện tốt bằng bóng blob.

.. figure:: img/decals_blob_shadow.webp
   :align: center
   :alt: Blob shadow under object comparison

   Blob shadow under object comparison

Hướng dẫn bắt đầu nhanh
-----------------------

Tạo decal trong editor
~~~~~~~~~~~~~~~~~~~~~~

1. Tạo một node Decal trong 3D editor. 2. Trong inspector, mở rộng phần **Textures** và tải một texture vào **Textures > Albedo**. 3. Di chuyển node Decal về phía một object, sau đó xoay node để decal hiển thị (và có đúng hướng). Nếu decal bị phản chiếu, hãy thử xoay nó 180 độ. Bạn có thể kiểm tra lại xem decal có đúng hướng hay không bằng cách tăng **Parameters > Normal Fade** lên 0.5. Việc này sẽ ngăn Decal được chiếu lên các bề mặt không hướng về phía decal. 4. Nếu decal của bạn chỉ nhằm tác động đến các object tĩnh, hãy cấu hình để ngăn decal tác động đến các object động (hoặc ngược lại). Để làm vậy, hãy thay đổi thuộc tính **Cull Mask** của decal nhằm loại trừ một số layer. Sau đó, sửa đổi các node MeshInstance3D của object động để thay đổi visibility layer của chúng. Chẳng hạn, bạn có thể chuyển chúng từ layer 1 sang layer 2, sau đó tắt layer 2 trong thuộc tính **Cull Mask** của decal.

Các thuộc tính của node Decal
-----------------------------

- **Extents:** Kích thước của decal. Trục Y xác định độ dài phần chiếu của decal. Hãy giữ độ dài phần chiếu ngắn nhất có thể để tăng cơ hội culling, từ đó cải thiện hiệu năng.

Textures
~~~~~~~~

- **Albedo:** Map albedo (diffuse/color) được dùng cho decal. Trong hầu hết trường hợp, đây là texture bạn muốn thiết lập trước tiên. Nếu sử dụng map normal hoặc ORM, bắt buộc phải thiết lập map albedo để cung cấp kênh alpha. Kênh alpha này sẽ được dùng làm mask để xác định mức độ ảnh hưởng của các map normal/ORM lên bề mặt bên dưới. - **Normal:** Map normal được dùng cho decal. Có thể dùng map này để tăng chi tiết cảm nhận được trên decal bằng cách thay đổi cách ánh sáng phản ứng với decal. Tác động của texture này được nhân với kênh alpha của texture albedo (nhưng không nhân với **Albedo Mix**). - **ORM:** Map Occlusion/Roughness/Metallic được dùng cho decal. Đây là format được tối ưu để lưu trữ các map material PBR. Map Ambient Occlusion được lưu trong kênh đỏ, map roughness trong kênh xanh lá, map metallic trong kênh xanh dương. Tác động của texture này được nhân với kênh alpha của texture albedo (nhưng không nhân với **Albedo Mix**). - **Emission:** Texture emission được dùng cho decal. Không giống **Albedo**, texture này sẽ phát sáng trong bóng tối.

Parameters
~~~~~~~~~~

- **Emission Energy:** Độ sáng của texture emission. - **Modulate:** Nhân màu của các texture albedo và emission. Dùng thuộc tính này để đổi màu decal (ví dụ: với decal sơn, hoặc để tăng biến thể bằng cách ngẫu nhiên hóa modulation của từng decal). - **Albedo Mix:** Độ mờ của texture albedo. Không giống việc sử dụng texture albedo với kênh alpha trong suốt hơn, giảm giá trị này xuống dưới ``1.0`` *không* làm giảm tác động của texture normal/ORM lên bề mặt bên dưới. Đặt giá trị này thành ``0.0`` khi tạo các decal chỉ có normal/ORM, chẳng hạn như dấu chân hoặc vũng nước ướt. - **Normal Fade:** Làm mờ Decal nếu góc giữa Decal và
  :abbr:`AABB (Axis-Aligned Bounding Box)` and the target surface becomes too large.
  Giá trị ``0.0`` sẽ chiếu decal bất kể góc nào, trong khi giá trị ``0.999`` giới hạn decal vào các bề mặt gần như vuông góc. Việc đặt **Normal Fade** thành giá trị lớn hơn ``0.0`` sẽ gây ra một chi phí hiệu năng nhỏ do phải tính toán thêm góc normal.

Vertical Fade
~~~~~~~~~~~~~

- **Upper Fade:** Đường cong mà decal sẽ mờ dần theo đó khi bề mặt cách xa hơn tâm của :abbr:`AABB (Axis-Aligned Bounding Box)` (về phía góc chiếu của decal). Chỉ các giá trị dương mới hợp lệ. - **Lower Fade:** Đường cong mà decal sẽ mờ dần theo đó khi bề mặt cách xa hơn tâm của :abbr:`AABB (Axis-Aligned Bounding Box)` (ra xa góc chiếu của decal). Chỉ các giá trị dương mới hợp lệ.

Distance Fade
~~~~~~~~~~~~~

- **Enabled:** Kiểm soát việc distance fade (một dạng :abbr:`LOD (Level of Detail)`) có được bật hay không. Decal sẽ mờ dần trong khoảng **Begin + Length**, sau đó sẽ bị cull và hoàn toàn không được gửi đến shader. Dùng thuộc tính này để giảm số lượng decal đang hoạt động trong scene, qua đó cải thiện hiệu năng. - **Begin:** Khoảng cách từ camera tại đó decal bắt đầu mờ đi (theo đơn vị 3D). - **Length:** Khoảng cách mà decal mờ dần (theo đơn vị 3D). Decal sẽ trở nên trong suốt hơn từ từ trong khoảng cách này và hoàn toàn không hiển thị ở cuối khoảng cách. Các giá trị cao hơn tạo ra chuyển tiếp mờ dần mượt hơn, phù hợp hơn khi camera di chuyển nhanh.

Cull Mask
~~~~~~~~~

- **Cull Mask:** Chỉ định các layer VisualInstance3D mà decal này sẽ chiếu lên. Theo mặc định, decal tác động đến tất cả layer. Thuộc tính này được dùng để chỉ định loại object nào sẽ nhận decal và loại nào không. Điều này đặc biệt hữu ích để đảm bảo các object động không vô tình nhận một Decal vốn dành cho địa hình bên dưới chúng.

Thứ tự render decal
-------------------

Theo mặc định, decal được sắp xếp dựa trên kích thước :abbr:`AABB (Axis-Aligned Bounding Box)` của chúng và khoảng cách đến camera. Các AABB gần camera hơn sẽ được render trước, nghĩa là thứ tự render decal đôi khi có vẻ thay đổi tùy theo vị trí camera nếu một số decal nằm cùng vị trí.

Để giải quyết vấn đề này, bạn có thể điều chỉnh thuộc tính **Sorting Offset** trong phần VisualInstance3D của inspector node Decal. Offset này không phải là thứ tự ưu tiên tuyệt đối, mà là một *hướng dẫn* mà renderer sẽ sử dụng, vì kích thước AABB vẫn ảnh hưởng đến cách sắp xếp decal. Do đó, các giá trị cao hơn sẽ *luôn* khiến decal được vẽ bên trên các decal khác có sorting offset thấp hơn.

Nếu muốn đảm bảo một decal luôn được render bên trên các decal khác, bạn cần đặt thuộc tính **Sorting Offset** của decal đó thành một giá trị dương lớn hơn độ dài AABB của decal lớn nhất có thể chồng lên nó. Để decal này được vẽ phía sau các decal khác, hãy đặt **Sorting Offset** thành cùng giá trị nhưng âm.

.. figure:: img/decals_sorting_offset.webp
   :align: center
   :alt: VisualInstance3D Sorting Offset comparison on Decals

   VisualInstance3D Sorting Offset comparison on Decals

Điều chỉnh hiệu năng và chất lượng
----------------------------------

Hiệu năng render decal chủ yếu được quyết định bởi phần diện tích màn hình mà chúng bao phủ, nhưng số lượng decal cũng có ảnh hưởng. Nhìn chung, một vài decal lớn bao phủ phần lớn màn hình sẽ tốn nhiều chi phí render hơn nhiều decal nhỏ được rải rác xung quanh.

Để cải thiện hiệu suất rendering, bạn có thể bật thuộc tính **Distance Fade** như mô tả ở trên. Điều này sẽ khiến các decal ở xa mờ dần khi chúng cách xa camera (và có thể ít hoặc không ảnh hưởng đến việc rendering cảnh cuối cùng). Bằng cách sử dụng node group, bạn cũng có thể ngăn các decal trang trí không thiết yếu được spawn dựa trên cấu hình của người dùng.

Cách các decal được rendering cũng ảnh hưởng đến hiệu suất. Thiết lập project
:ref:`Rendering > Textures > Decals > Filter<class_ProjectSettings_property_rendering/textures/decals/filter>`
nâng cao cho phép bạn kiểm soát cách các texture decal được filter. **Nearest/Linear** không sử dụng mipmap. Tuy nhiên, decal sẽ trông có hạt khi ở xa. **Nearest/Linear Mipmaps** sẽ trông mượt hơn khi ở xa, nhưng decal sẽ bị mờ khi được nhìn từ các góc xiên. Có thể khắc phục điều này bằng cách sử dụng **Nearest/Linear Mipmaps Anisotropic**, tùy chọn này mang lại chất lượng cao nhất nhưng cũng rendering chậm hơn.

Nếu project của bạn có phong cách pixel art, hãy cân nhắc đặt filter thành một trong các giá trị **Nearest** để decal sử dụng nearest-neighbor filtering. Nếu không, hãy dùng **Linear**.

Giới hạn
--------

Decal không thể tác động đến các thuộc tính material khác ngoài những thuộc tính được liệt kê ở trên, chẳng hạn như height (dùng cho parallax mapping).

Vì lý do hiệu suất, decal sử dụng logic rendering hoàn toàn cố định. Điều này có nghĩa là decal không thể sử dụng custom shader. Tuy nhiên, custom shader trên các bề mặt được chiếu có thể đọc thông tin bị decal ghi đè trên chúng, chẳng hạn như roughness và metallic.

Khi sử dụng Forward+ renderer, Godot sử dụng phương pháp *clustering* để rendering decal. Có thể thêm bao nhiêu decal tùy ý (miễn là hiệu suất cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered elements* có thể xuất hiện trong chế độ xem của camera hiện tại. Một clustered element là omni light, spot light, area light, một :ref:`decal <doc_using_decals>`, hoặc một
:ref:`reflection probe <doc_reflection_probes>`. This limit can be increased by adjusting
:ref:`Max Clustered Elements<class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>`
trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng Mobile renderer, chỉ có thể áp dụng 8 decal cho mỗi *resource* Mesh riêng lẻ. Nếu có nhiều decal hơn tác động đến một mesh, không phải tất cả chúng đều được rendering trên mesh đó.
