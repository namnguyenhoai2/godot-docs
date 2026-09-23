.. _doc_advanced_import_settings:

Cài đặt nhập nâng cao
=====================

Mặc dù bảng nhập thông thường cung cấp nhiều tùy chọn thiết yếu cho các mô hình 3D được nhập, cài đặt nhập nâng cao cung cấp các tùy chọn cho từng đối tượng, bản xem trước mô hình và bản xem trước animation. Để mở, hãy chọn nút :button:`Advanced...` ở cuối dock nhập.

.. figure:: img/importing_3d_scenes_advanced_import_settings_button.webp
   :align: center

Tính năng này khả dụng cho các mô hình 3D được nhập dưới dạng scene, cũng như các thư viện animation.

.. note::

    Trang này không trình bày các tùy chọn cũng có trong dock nhập hoặc bất kỳ nội dung nào bên ngoài cài đặt nhập nâng cao. Để biết thông tin về những nội dung đó, hãy đọc
    trang :ref:`doc_importing_3d_scenes_import_configuration`.

Sử dụng hộp thoại Cài đặt nhập nâng cao
---------------------------------------

Tab đầu tiên bạn sẽ thấy là tab **Scene**. Các tùy chọn trong bảng bên phải giống hệt dock nhập, nhưng bạn có quyền truy cập vào bản xem trước 3D. Có thể xoay bản xem trước 3D bằng cách giữ nút chuột trái rồi kéo chuột. Có thể điều chỉnh mức thu phóng bằng con lăn chuột.

.. figure:: img/importing_3d_scenes_advanced_import_settings_scene.webp
   :align: center
   :alt: Hộp thoại Cài đặt nhập nâng cao (tab Scene)

   Hộp thoại Cài đặt nhập nâng cao (tab Scene). Tác giả: `Modern Arm Chair 01 - Poly Haven <https://polyhaven.com/a/modern_arm_chair_01>`__

Định cấu hình tùy chọn nhập node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể chọn từng node tạo nên scene trong tab **Scene** bằng chế độ xem cây ở bên trái:

.. figure:: img/importing_3d_scenes_advanced_import_settings_node.webp
   :align: center
   :alt: Chọn một node trong hộp thoại Cài đặt nhập nâng cao (tab Scene)

   Chọn một node trong hộp thoại Cài đặt nhập nâng cao (tab Materials)

Thao tác này hiển thị một số tùy chọn nhập cho từng node:

- **Skip Import:** Nếu được chọn, node sẽ không xuất hiện trong scene được nhập cuối cùng. Việc bật tùy chọn này sẽ vô hiệu hóa tất cả các tùy chọn khác.
- **Generate > Physics:** Nếu được chọn, sẽ tạo một node *parent* PhysicsBody3D với các hình dạng va chạm là *siblings* của node MeshInstance3D.
- **Generate > NavMesh:** Nếu được chọn, sẽ tạo một node *child* NavigationRegion3D cho :ref:`navigation <doc_navigation_overview_3d>`. **Mesh + NavMesh** sẽ giữ mesh gốc ở trạng thái hiển thị, trong khi **NavMesh Only** chỉ nhập navigation mesh (không có biểu diễn trực quan). **NavMesh Only** предназначено для использования, когда вы вручную создали упрощённую mesh для navigation.
- **Generate > Occluder:** Nếu được chọn, sẽ tạo một node *sibling* OccluderInstance3D cho :ref:`occlusion culling <doc_occlusion_culling>`, sử dụng hình học của mesh làm cơ sở cho hình dạng của occluder. **Mesh + Occluder** sẽ giữ mesh gốc ở trạng thái hiển thị, trong khi **Occluder Only** chỉ nhập occluder (không có biểu diễn trực quan). **Occluder Only** được dùng khi bạn đã tự tạo một mesh đơn giản hóa cho occlusion culling.

Các tùy chọn này chỉ hiển thị nếu một số tùy chọn ở trên được bật:

- **Physics > Body Type:** Chỉ hiển thị khi **Generate > Physics** được bật. Điều khiển PhysicsBody3D sẽ được tạo. **Static** tạo một StaticBody3D, **Dynamic** tạo một RigidBody3D, **Area** tạo một Area3D.
- **Physics > Shape Type:** Chỉ hiển thị khi **Generate > Physics** được bật. **Trimesh** cho phép va chạm chính xác đến từng tam giác, nhưng chỉ có thể dùng với kiểu body **Static**. Các kiểu khác kém chính xác hơn và có thể cần cấu hình thủ công, nhưng có thể dùng với mọi kiểu body. Đối với hình học level tĩnh, hãy dùng **Trimesh**. Đối với hình học động, nếu có thể hãy dùng các hình dạng nguyên thủy để đạt hiệu năng tốt hơn, hoặc dùng một trong các chế độ phân rã lồi nếu hình dạng lớn và phức tạp.
- **Decomposition > Advanced:** Chỉ hiển thị khi **Physics > Shape Type** là **Decompose Convex**. Nếu được chọn, cho phép điều chỉnh các tùy chọn phân rã nâng cao. Nếu bị tắt, chỉ có thể điều chỉnh **Precision** đặt sẵn (thường là đủ).
- **Decomposition > Precision:** Chỉ hiển thị khi **Physics > Shape Type** là **Decompose Convex**. Điều khiển độ chính xác dùng cho việc phân rã lồi. Giá trị cao hơn tạo ra va chạm chi tiết hơn, nhưng phải đánh đổi bằng thời gian tạo lâu hơn và mức sử dụng CPU tăng trong quá trình mô phỏng vật lý. Để cải thiện hiệu năng, bạn nên giữ giá trị này ở mức thấp nhất có thể đối với trường hợp sử dụng của mình.
- **Occluder > Simplification Distance:** Chỉ hiển thị khi **Generate > Occluder** được đặt thành **Mesh + Occluder** hoặc **Occluder Only**. Giá trị cao hơn tạo ra mesh occluder có ít đỉnh hơn (giúp giảm mức sử dụng CPU), nhưng phải đánh đổi bằng nhiều vấn đề occlusion culling hơn (chẳng hạn như dương tính giả hoặc âm tính giả). Nếu bạn gặp tình trạng đối tượng biến mất khi không nên biến mất lúc camera ở gần một mesh nhất định, hãy thử giảm giá trị này.

Định cấu hình tùy chọn nhập mesh và material
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong hộp thoại Cài đặt nhập nâng cao, có 2 cách để chọn từng mesh hoặc material:

- Chuyển sang tab **Meshes** hoặc **Materials** ở góc trên bên trái của hộp thoại.
- Ở lại tab **Scene**, nhưng mở rộng các tùy chọn trong chế độ xem cây ở bên trái. Sau khi chọn mesh hoặc material, phần này hiển thị thông tin giống các tab **Meshes** và **Materials**, nhưng ở dạng chế độ xem cây thay vì danh sách.

Nếu bạn chọn một mesh, các tùy chọn khác nhau sẽ xuất hiện trong bảng bên phải:

.. figure:: img/importing_3d_scenes_advanced_import_settings_meshes.webp
   :align: center
   :alt: Hộp thoại Cài đặt nhập nâng cao (tab Meshes)

   Hộp thoại Cài đặt nhập nâng cao (tab Meshes)

Các tùy chọn như sau:

- **Save to File:** Lưu :ref:`class_Mesh` *resource* vào một tệp bên ngoài (đây không phải là tệp scene). Nhìn chung, bạn không cần dùng tùy chọn này để đặt mesh vào scene 3D – thay vào đó, bạn nên instance trực tiếp scene 3D. Tuy nhiên, việc truy cập trực tiếp vào resource Mesh rất hữu ích đối với các node cụ thể, chẳng hạn như :ref:`class_MeshInstance3D`, :ref:`class_MultiMeshInstance3D`,
  :ref:`class_GPUParticles3D` hoặc :ref:`class_CPUParticles3D`.
  - Bạn cũng cần chỉ định đường dẫn đến tệp đầu ra bằng tùy chọn xuất hiện sau khi
  bật **Save to File**. Bạn nên sử dụng phần mở rộng tệp đầu ra ``.res`` để có kích thước tệp nhỏ hơn và tốc độ tải nhanh hơn, vì ``.tres`` không hiệu quả khi ghi lượng dữ liệu lớn.
- **Generate > Shadow Meshes:** Ghi đè theo từng mesh cho tùy chọn import áp dụng trên toàn scene **Meshes > Create Shadow Meshes** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** sẽ sử dụng tùy chọn import áp dụng trên toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể.
- **Generate > Lightmap UV:** Ghi đè theo từng mesh cho tùy chọn import áp dụng trên toàn scene **Meshes > Light Baking** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** sẽ sử dụng tùy chọn import áp dụng trên toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể.
  - Đặt tùy chọn này thành **Enable** trên một scene có chế độ light baking **Static**
  tương đương với việc cấu hình mesh này sử dụng **Static Lightmaps**. Đặt tùy chọn này thành **Disable** trên một scene có chế độ light baking **Static Lightmaps** tương đương với việc cấu hình mesh này sử dụng **Static**.
- **Generate > LODs:** Ghi đè theo từng mesh cho tùy chọn import áp dụng trên toàn scene **Meshes > Generate LODs** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** sẽ sử dụng tùy chọn import áp dụng trên toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể.
- **LODs > Normal Merge Angle:** Độ chênh lệch góc tối thiểu giữa hai đỉnh cần có để giữ lại một cạnh hình học trong quá trình tạo LOD cho mesh. Nếu gặp vấn đề về hiển thị khi tạo LOD, việc giảm giá trị này có thể hữu ích, nhưng sẽ làm quá trình tạo LOD kém hiệu quả hơn.

Nếu bạn chọn một material, chỉ một tùy chọn sẽ xuất hiện trong bảng ở bên phải:

.. figure:: img/importing_3d_scenes_advanced_import_settings_materials.webp
   :align: center
   :alt: Hộp thoại Advanced Import Settings (tab Materials)

   Hộp thoại Advanced Import Settings (tab Materials)

Khi **Use External** được chọn và đã chỉ định đường dẫn đầu ra, tùy chọn này cho phép bạn sử dụng một material bên ngoài thay cho material được chứa trong tệp scene 3D gốc; xem phần bên dưới.

Trích xuất material thành các tệp riêng biệt
--------------------------------------------

Mặc dù Godot có thể import các material được tạo bằng phần mềm dựng hình 3D, cấu hình mặc định có thể không phù hợp với nhu cầu của bạn. Ví dụ:

- Bạn muốn cấu hình các tính năng của material mà ứng dụng 3D không hỗ trợ.
- Bạn muốn sử dụng một chế độ lọc texture khác, vì tùy chọn này được cấu hình trong material (không phải trong image).
- Bạn muốn thay thế một trong các material bằng một material hoàn toàn khác, chẳng hạn như custom shader.

Để có thể chỉnh sửa các material của scene 3D trong trình chỉnh sửa Godot, bạn cần sử dụng các resource material *external*.

Ở góc trên bên trái của hộp thoại Advanced Import Settings, chọn **Actions… > Extract Materials**:

.. figure:: img/importing_3d_scenes_advanced_import_settings_extract_materials.webp
   :align: center
   :alt: Trích xuất tất cả material tích hợp sẵn thành các resource bên ngoài trong hộp thoại Advanced Import Settings

   Trích xuất tất cả material tích hợp sẵn thành các resource bên ngoài trong hộp thoại Advanced Import Settings

Sau khi chọn tùy chọn này, hãy chọn một thư mục để trích xuất các tệp material ``.tres`` vào, rồi xác nhận việc trích xuất:

.. figure:: img/importing_3d_scenes_advanced_import_settings_extract_materials_confirm.webp
   :align: center
   :alt: Xác nhận trích xuất material trong hộp thoại phụ Advanced Import Settings

   Xác nhận trích xuất material trong hộp thoại phụ Advanced Import Settings

.. note::

    Sau khi trích xuất material, scene 3D sẽ tự động được cấu hình để sử dụng các tham chiếu material bên ngoài. Vì vậy, bạn không cần bật thủ công **Use External** trên từng material để material ``.tres`` bên ngoài có hiệu lực.

Khi **Use External** được bật, hãy nhớ rằng hộp thoại Advanced Import Settings vẫn hiển thị các material gốc của mesh (những material được thiết kế trong phần mềm dựng hình 3D). Điều này có nghĩa là các tùy chỉnh của bạn đối với material sẽ không hiển thị trong hộp thoại này. Để xem trước các material đã sửa đổi, bạn cần đặt scene 3D đã import vào một scene khác bằng trình chỉnh sửa.

Godot sẽ không ghi đè các thay đổi được thực hiện trên material đã trích xuất khi scene 3D nguồn được reimport. Tuy nhiên, nếu tên material bị thay đổi trong tệp 3D nguồn, liên kết giữa material gốc và material đã trích xuất sẽ bị mất. Do đó, bạn sẽ cần sử dụng hộp thoại Advanced Import Settings để liên kết material đã đổi tên với material đã trích xuất hiện có.

Bạn có thể thực hiện việc trên trong tab **Materials** của hộp thoại bằng cách chọn material, bật **Save to File**, rồi chỉ định đường dẫn lưu bằng tùy chọn **Path** xuất hiện sau khi bật **Save to File**.

Tùy chọn animation
------------------

Có một số tùy chọn bổ sung dành cho các node :ref:`class_AnimationPlayer` được tạo, cũng như các animation riêng lẻ của chúng khi chúng được chọn trong tab **Scene**.

Optimizer
~~~~~~~~~

Khi animation được import, một optimizer sẽ chạy để giảm đáng kể kích thước của animation. Nhìn chung, tùy chọn này luôn nên được bật, trừ khi bạn nghi ngờ rằng animation có thể bị hỏng do bật tùy chọn này.

Lưu vào tệp
~~~~~~~~~~~

Theo mặc định, animation được lưu dưới dạng tích hợp sẵn. Bạn có thể lưu chúng vào một tệp thay thế. Điều này cho phép thêm các track tùy chỉnh vào animation và giữ lại chúng sau khi reimport.

Slices
~~~~~~

Có thể chỉ định nhiều animation từ một timeline duy nhất dưới dạng các phân đoạn. Để thực hiện việc này, model chỉ được có một animation mang tên ``default``. Để tạo các phân đoạn, hãy thay đổi số lượng phân đoạn thành một giá trị lớn hơn không. Sau đó, bạn có thể đặt tên cho một phân đoạn, chỉ định các frame bắt đầu và kết thúc, cũng như chọn animation có lặp lại hay không.
