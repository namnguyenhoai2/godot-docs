.. _doc_advanced_import_settings:

Cài đặt nhập nâng cao
=====================

Mặc dù bảng nhập thông thường cung cấp nhiều tùy chọn thiết yếu cho các mô hình 3D được nhập, cài đặt nhập nâng cao cung cấp các tùy chọn riêng cho từng đối tượng, bản xem trước mô hình và bản xem trước animation. Để mở, hãy chọn nút :button:`Advanced...` ở cuối dock nhập.

.. figure:: img/importing_3d_scenes_advanced_import_settings_button.webp
   :align: center

Tính năng này khả dụng cho các mô hình 3D được nhập dưới dạng scene, cũng như các thư viện animation.

.. note::

    Trang này không đề cập đến các tùy chọn cũng có trong dock nhập hoặc bất kỳ nội dung nào nằm ngoài cài đặt nhập nâng cao. Để biết thông tin về các tùy chọn đó, hãy đọc
    :ref:`doc_importing_3d_scenes_import_configuration` page.

Sử dụng hộp thoại Cài đặt nhập nâng cao
---------------------------------------

Tab đầu tiên bạn sẽ thấy là tab **Scene**. Các tùy chọn có trong bảng bên phải giống hệt Import dock, nhưng bạn có quyền truy cập vào bản xem trước 3D. Có thể xoay bản xem trước 3D bằng cách giữ nút chuột trái rồi kéo chuột. Có thể điều chỉnh độ thu phóng bằng con lăn chuột.

.. figure:: img/importing_3d_scenes_advanced_import_settings_scene.webp
   :align: center
   :alt: Advanced Import Settings dialog (Scene tab)

   Advanced Import Settings dialog (Scene tab).
   Credit: `Modern Arm Chair 01 - Poly Haven <https://polyhaven.com/a/modern_arm_chair_01>`__

Cấu hình các tùy chọn nhập node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể chọn từng node tạo nên scene trong tab **Scene** bằng chế độ xem dạng cây ở bên trái:

.. figure:: img/importing_3d_scenes_advanced_import_settings_node.webp
   :align: center
   :alt: Selecting a node in the Advanced Import Settings dialog (Scene tab)

   Selecting a node in the Advanced Import Settings dialog (Materials tab)

Thao tác này hiển thị một số tùy chọn nhập riêng cho từng node:

- **Skip Import:** Nếu được chọn, node sẽ không xuất hiện trong scene được nhập cuối cùng. Bật tùy chọn này sẽ vô hiệu hóa tất cả các tùy chọn khác. - **Generate > Physics:** Nếu được chọn, sẽ tạo một node *parent* PhysicsBody3D với các hình dạng va chạm là *sibling* của node MeshInstance3D. - **Generate > NavMesh:** Nếu được chọn, sẽ tạo một node *child* NavigationRegion3D cho :ref:`navigation <doc_navigation_overview_3d>`. **Mesh + NavMesh** sẽ giữ mesh gốc hiển thị, trong khi **NavMesh Only** chỉ nhập navigation mesh (không có biểu diễn trực quan). **NavMesh Only** được dùng khi bạn đã tự tạo một mesh đơn giản hóa cho navigation. - **Generate > Occluder:** Nếu được chọn, sẽ tạo một node *sibling* OccluderInstance3D cho :ref:`occlusion culling <doc_occlusion_culling>` bằng cách sử dụng hình học của mesh làm cơ sở cho hình dạng occluder. **Mesh + Occluder** sẽ giữ mesh gốc hiển thị, trong khi **Occluder Only** chỉ nhập occluder (không có biểu diễn trực quan). **Occluder Only** được dùng khi bạn đã tự tạo một mesh đơn giản hóa cho occlusion culling.

Các tùy chọn này chỉ hiển thị nếu một số tùy chọn ở trên được bật:

- **Physics > Body Type:** Chỉ hiển thị khi **Generate > Physics** được bật. Điều khiển PhysicsBody3D sẽ được tạo. **Static** tạo một StaticBody3D, **Dynamic** tạo một RigidBody3D, còn **Area** tạo một Area3D. - **Physics > Shape Type:** Chỉ hiển thị khi **Generate > Physics** được bật. **Trimesh** cho phép va chạm chính xác theo từng tam giác, nhưng chỉ có thể dùng với kiểu body **Static**. Các kiểu khác kém chính xác hơn và có thể cần cấu hình thủ công, nhưng có thể dùng với bất kỳ kiểu body nào. Đối với hình học level tĩnh, hãy dùng **Trimesh**. Đối với hình học động, nếu có thể hãy dùng các hình dạng nguyên thủy để đạt hiệu năng tốt hơn, hoặc dùng một trong các chế độ phân rã convex nếu hình dạng lớn và phức tạp. - **Decomposition > Advanced:** Chỉ hiển thị khi **Physics > Shape Type** là **Decompose Convex**. Nếu được chọn, cho phép điều chỉnh các tùy chọn phân rã nâng cao. Nếu tắt, chỉ có thể điều chỉnh **Precision** đặt sẵn (thường là đủ dùng). - **Decomposition > Precision:** Chỉ hiển thị khi **Physics > Shape Type** là **Decompose Convex**. Điều khiển độ chính xác dùng cho quá trình phân rã convex. Giá trị cao hơn tạo ra va chạm chi tiết hơn, nhưng việc tạo sẽ chậm hơn và sử dụng nhiều CPU hơn trong quá trình mô phỏng physics. Để cải thiện hiệu năng, bạn nên giữ giá trị này thấp nhất có thể đối với trường hợp sử dụng của mình. - **Occluder > Simplification Distance:** Chỉ hiển thị khi **Generate > Occluder** được đặt thành **Mesh + Occluder** hoặc **Occluder Only**. Giá trị cao hơn tạo ra mesh occluder có ít vertex hơn (giúp giảm mức sử dụng CPU), nhưng làm tăng các vấn đề về occlusion culling (chẳng hạn như dương tính giả hoặc âm tính giả). Nếu bạn gặp tình trạng các đối tượng biến mất khi không nên biến mất lúc camera ở gần một mesh nhất định, hãy thử giảm giá trị này.

Cấu hình các tùy chọn nhập mesh và material
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong hộp thoại Cài đặt nhập nâng cao, có 2 cách để chọn từng mesh hoặc material:

- Chuyển sang tab **Meshes** hoặc **Materials** ở góc trên bên trái của hộp thoại. - Giữ nguyên trong tab **Scene**, nhưng mở rộng các tùy chọn trên chế độ xem dạng cây ở bên trái. Sau khi chọn một mesh hoặc material, cách này hiển thị cùng thông tin như các tab **Meshes** và **Materials**, nhưng ở chế độ xem dạng cây thay vì danh sách.

Nếu bạn chọn một mesh, các tùy chọn khác nhau sẽ xuất hiện trong bảng bên phải:

.. figure:: img/importing_3d_scenes_advanced_import_settings_meshes.webp
   :align: center
   :alt: Advanced Import Settings dialog (Meshes tab)

   Advanced Import Settings dialog (Meshes tab)

Các tùy chọn như sau:

- **Save to File:** Lưu *resource* :ref:`class_Mesh` vào một file bên ngoài (đây không phải file scene). Thông thường, bạn không cần dùng tùy chọn này để đặt mesh vào một scene 3D – thay vào đó, bạn nên instance trực tiếp scene 3D. Tuy nhiên, việc truy cập trực tiếp vào Mesh resource rất hữu ích cho các node cụ thể, chẳng hạn như :ref:`class_MeshInstance3D`, :ref:`class_MultiMeshInstance3D`,
  :ref:`class_GPUParticles3D` or :ref:`class_CPUParticles3D`.
  - Bạn cũng sẽ cần chỉ định đường dẫn file đầu ra bằng tùy chọn xuất hiện sau khi bật **Save to File**. Bạn nên sử dụng phần mở rộng file đầu ra ``.res`` để có kích thước file nhỏ hơn và tốc độ tải nhanh hơn, vì ``.tres`` không hiệu quả khi ghi lượng dữ liệu lớn. - **Generate > Shadow Meshes:** Tùy chọn ghi đè theo từng mesh cho tùy chọn nhập toàn scene **Meshes > Create Shadow Meshes** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** will use the
  tùy chọn nhập toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể. - **Generate > Lightmap UV:** Tùy chọn ghi đè theo từng mesh cho tùy chọn nhập toàn scene **Meshes > Light Baking** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** will use the
  tùy chọn nhập toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể. - Đặt thành **Enable** trên một scene có chế độ light baking **Static** tương đương với việc cấu hình mesh này sử dụng **Static Lightmaps**. Đặt thành **Disable** trên một scene có chế độ light baking **Static Lightmaps** tương đương với việc cấu hình mesh này sử dụng **Static**. - **Generate > LODs:** Tùy chọn ghi đè theo từng mesh cho tùy chọn nhập toàn scene **Meshes > Generate LODs** được mô tả trong
  :ref:`doc_importing_3d_scenes_using_the_import_dock`. **Default** will use the
  tùy chọn nhập toàn scene, trong khi **Enable** hoặc **Disable** có thể buộc bật hoặc tắt hành vi này trên một mesh cụ thể. - **LODs > Normal Merge Angle:** Độ chênh lệch góc tối thiểu giữa hai vertex cần thiết để giữ lại một cạnh hình học trong quá trình tạo mesh LOD. Nếu gặp vấn đề về hình ảnh khi tạo LOD, việc giảm giá trị này có thể giúp ích (đổi lại quá trình tạo LOD sẽ kém hiệu quả hơn).

Nếu bạn chọn một material, chỉ một tùy chọn sẽ xuất hiện trong bảng bên phải:

.. figure:: img/importing_3d_scenes_advanced_import_settings_materials.webp
   :align: center
   :alt: Advanced Import Settings dialog (Materials tab)

   Advanced Import Settings dialog (Materials tab)

Khi **Use External** được chọn và đường dẫn đầu ra được chỉ định, tùy chọn này cho phép bạn sử dụng một material bên ngoài thay cho material có trong file scene 3D gốc; xem phần bên dưới.

Trích xuất material thành các file riêng biệt
---------------------------------------------

Mặc dù Godot có thể nhập các material được tạo trong phần mềm modeling 3D, cấu hình mặc định có thể không phù hợp với nhu cầu của bạn. Ví dụ:

- Bạn muốn cấu hình các tính năng material không được ứng dụng 3D hỗ trợ. - Bạn muốn sử dụng một chế độ lọc texture khác, vì tùy chọn này được cấu hình trong material (chứ không phải trong image). - Bạn muốn thay thế một trong các material bằng một material hoàn toàn khác, chẳng hạn như một custom shader.

Để có thể sửa đổi material của scene 3D trong Godot editor, bạn cần sử dụng các material resource *bên ngoài*.

Ở góc trên bên trái của hộp thoại Cài đặt nhập nâng cao, chọn **Actions… > Extract Materials**:

.. figure:: img/importing_3d_scenes_advanced_import_settings_extract_materials.webp
   :align: center
   :alt: Extracting all built-in materials to external resources in the Advanced Import Settings dialog

   Extracting all built-in materials to external resources in the Advanced Import Settings dialog

Sau khi chọn tùy chọn này, hãy chọn một thư mục để trích xuất các file material ``.tres`` vào, rồi xác nhận việc trích xuất:

.. figure:: img/importing_3d_scenes_advanced_import_settings_extract_materials_confirm.webp
   :align: center
   :alt: Confirming material extraction in the Advanced Import Settings subdialog

   Confirming material extraction in the Advanced Import Settings subdialog

.. note::

    Sau khi trích xuất material, scene 3D sẽ tự động được cấu hình để sử dụng các tham chiếu material bên ngoài. Do đó, bạn không cần bật thủ công **Use External** trên từng material để material ``.tres`` bên ngoài có hiệu lực.

Khi **Use External** được bật, hãy nhớ rằng hộp thoại Cài đặt nhập nâng cao sẽ tiếp tục hiển thị material gốc của mesh (những material được thiết kế trong phần mềm modeling 3D). Điều này có nghĩa là các tùy chỉnh của bạn đối với material sẽ không hiển thị trong hộp thoại này. Để xem trước material đã sửa đổi, bạn cần đặt scene 3D đã nhập vào một scene khác bằng editor.

Godot sẽ không ghi đè các thay đổi được thực hiện trên material đã trích xuất khi scene 3D nguồn được nhập lại. Tuy nhiên, nếu tên material bị thay đổi trong file 3D nguồn, liên kết giữa material gốc và material đã trích xuất sẽ bị mất. Do đó, bạn sẽ cần sử dụng hộp thoại Cài đặt nhập nâng cao để liên kết material đã đổi tên với material đã trích xuất hiện có.

Bạn có thể thực hiện việc trên trong tab **Materials** của hộp thoại bằng cách chọn material, bật **Save to File**, rồi chỉ định đường dẫn lưu bằng tùy chọn **Path** xuất hiện sau khi bật **Save to File**.

Các tùy chọn animation
----------------------

Một số tùy chọn bổ sung khả dụng cho các node :ref:`class_AnimationPlayer` được tạo, cũng như các animation riêng lẻ của chúng khi được chọn trong tab **Scene**.

Optimizer
~~~~~~~~~

Khi các animation được import, một optimizer sẽ được chạy để giảm đáng kể kích thước của animation. Nhìn chung, bạn nên luôn bật tùy chọn này, trừ khi nghi ngờ rằng animation có thể bị hỏng do tùy chọn này được bật.

Lưu vào tệp
~~~~~~~~~~~

Theo mặc định, các animation được lưu dưới dạng tích hợp sẵn. Bạn cũng có thể lưu chúng vào một tệp. Điều này cho phép thêm các track tùy chỉnh vào animation và giữ lại chúng sau khi import lại.

Các đoạn cắt
~~~~~~~~~~~~

Có thể chỉ định nhiều animation từ một timeline duy nhất dưới dạng các đoạn cắt. Để thực hiện việc này, model chỉ được có một animation có tên là ``default``. Để tạo các đoạn cắt, hãy thay đổi số lượng đoạn cắt thành một giá trị lớn hơn 0. Sau đó, bạn có thể đặt tên cho một đoạn cắt, chỉ định các frame bắt đầu và kết thúc, cũng như chọn animation có lặp lại hay không.
