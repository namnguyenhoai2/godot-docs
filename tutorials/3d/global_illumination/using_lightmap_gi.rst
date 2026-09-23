.. _doc_using_lightmap_gi:

Sử dụng chiếu sáng toàn cục bằng Lightmap
=========================================

Lightmap được bake là một quy trình để thêm ánh sáng gián tiếp (hoặc ánh sáng bake hoàn toàn) vào cảnh. Không giống các phương pháp :ref:`VoxelGI <doc_using_voxel_gi>` và
:ref:`SDFGI <doc_using_sdfgi>`, lightmap được bake hoạt động tốt trên PC cấu hình thấp và thiết bị di động vì hầu như không tiêu tốn tài nguyên trong runtime. Ngoài ra, không giống VoxelGI và SDFGI, lightmap được bake có thể được dùng tùy chọn để lưu trữ ánh sáng trực tiếp, giúp tăng hiệu năng hơn nữa.

Không giống VoxelGI và SDFGI, lightmap được bake hoàn toàn tĩnh. Sau khi bake, chúng không thể được sửa đổi dưới bất kỳ hình thức nào. Chúng cũng không cung cấp phản chiếu cho cảnh, vì vậy cần sử dụng :ref:`doc_reflection_probes` cùng với nó trong các không gian nội thất (hoặc sử dụng Sky ở không gian ngoại thất) để đạt chất lượng tốt.

Vì được bake, chúng gặp ít vấn đề về hiện tượng ánh sáng xuyên hơn VoxelGI và SDFGI, đồng thời ánh sáng gián tiếp thường trông đẹp hơn. Nhược điểm là thời gian bake lightmap lâu hơn so với bake VoxelGI. Trong khi bake VoxelGI có thể hoàn tất chỉ trong vài giây, bake lightmap có thể mất vài phút hoặc lâu hơn. Điều này có thể làm giảm đáng kể tốc độ lặp, vì vậy bạn chỉ nên bake lightmap khi thực sự cần xem các thay đổi về ánh sáng. Lightmap được bake trên GPU, do đó quá trình bake ánh sáng sẽ nhanh hơn nếu bạn có GPU rời tầm trung hoặc cao cấp.

Việc bake lightmap cũng sẽ dành riêng vị trí UV2 của các material đã bake, nghĩa là bạn không thể sử dụng vị trí này cho các mục đích khác trong material (dù là trong
:ref:`doc_standard_material_3d` hay trong shader tùy chỉnh).

Mặc dù kém linh hoạt, lightmap được bake thường mang lại cả chất lượng *và* hiệu năng tốt nhất cùng lúc trong các cảnh (phần lớn) tĩnh. Vì vậy, lightmap vẫn phổ biến trong phát triển game, dù đây là kỹ thuật chiếu sáng toàn cục lâu đời nhất trong trò chơi điện tử.

.. seealso::

    Không chắc LightmapGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI hiện có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: Đã tắt LightmapGI.

   Đã tắt LightmapGI.

.. figure:: img/gi_lightmap_gi_indirect_only.webp
   :alt: Đã bật LightmapGI (chỉ bake ánh sáng gián tiếp).

   Đã bật LightmapGI (chỉ bake ánh sáng gián tiếp). Ánh sáng trực tiếp vẫn là real-time, cho phép có những thay đổi nhỏ trong khi chơi.

.. figure:: img/gi_lightmap_gi_direct_and_indirect.webp
   :alt: Đã bật LightmapGI (bake cả ánh sáng trực tiếp và gián tiếp).

   Đã bật LightmapGI (bake cả ánh sáng trực tiếp và gián tiếp). Hiệu năng tốt nhất nhưng hình ảnh có chất lượng thấp hơn. Hãy chú ý bóng mặt trời mờ hơn ở góc trên bên phải.

Dưới đây là một số so sánh về hình ảnh của LightmapGI và VoxelGI. Hãy chú ý rằng lightmap chính xác hơn, nhưng cũng chịu ảnh hưởng bởi việc ánh sáng nằm trên một texture đã unwrap, nên các vùng chuyển tiếp và độ phân giải có thể không tốt lắm. VoxelGI kém chính xác hơn (vì là một phép xấp xỉ), nhưng nhìn chung mượt hơn.

.. image:: img/lightmap_gi_comparison.png

SDFGI cũng kém chính xác hơn so với LightmapGI. Tuy nhiên, SDFGI có thể hỗ trợ các thế giới mở rộng lớn mà không cần bake.

Thiết lập
---------

.. warning::

    Không hỗ trợ bake lightmap trong các trình chỉnh sửa trên web do các hạn chế của graphics API. Trên nền tảng web, chỉ hỗ trợ lightmap *rendering* đã được bake trên một nền tảng khác.

.. note::

    Node LightmapGI chỉ bake các node nằm cùng cấp với node LightmapGI (các node anh em), hoặc các node là con của node LightmapGI. Điều này cho phép bạn sử dụng nhiều node LightmapGI để bake các phần khác nhau của cảnh một cách độc lập.

Trước hết, trước khi lightmapper có thể thực hiện bất kỳ thao tác nào, các đối tượng cần bake phải có lớp UV2 và kích thước texture. Lớp UV2 là một tập hợp các tọa độ texture phụ, đảm bảo mỗi mặt của đối tượng có vị trí riêng trong UV map. Các mặt không được dùng chung pixel trong texture.

Có một vài cách để đảm bảo đối tượng của bạn có lớp UV2 và kích thước texture riêng:

Unwrap khi import scene (khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong hầu hết trường hợp, đây là cách tiếp cận tốt nhất. Nhược điểm duy nhất là với các model lớn, quá trình unwrap có thể mất một lúc khi import. Tuy vậy, Godot sẽ lưu UV2 vào cache qua các lần reimport, nên UV2 chỉ được tạo lại khi cần.

Chọn scene đã import trong filesystem dock, sau đó đi đến dock **Import**. Tại đó, bạn có thể sửa đổi tùy chọn sau:

.. image:: img/lightmap_gi_import.webp

Tùy chọn **Meshes > Light Baking** phải được đặt thành **Static Lightmaps (VoxelGI/SDFGI/LightmapGI)**:

.. image:: img/lightmap_gi_mesh_import_meshes.webp

Khi unwrap lúc import, bạn có thể điều chỉnh kích thước texture bằng tùy chọn **Meshes > Lightmap Texel Size**. Giá trị *Lower* sẽ tạo ra lightmap chi tiết hơn, có thể cho chất lượng hình ảnh cao hơn nhưng phải đánh đổi bằng thời gian bake lâu hơn và kích thước tệp lightmap lớn hơn. Giá trị mặc định ``0.2`` phù hợp với các scene nhỏ và vừa, nhưng bạn có thể muốn tăng lên ``0.5`` hoặc thậm chí cao hơn đối với các scene lớn hơn. Điều này đặc biệt đúng nếu bạn chỉ bake ánh sáng gián tiếp, vì ánh sáng gián tiếp là dữ liệu tần số thấp (nghĩa là không cần texture độ phân giải cao để biểu diễn chính xác).

Tác động của việc đặt tùy chọn này là tất cả mesh trong scene sẽ được tạo UV2 map đúng cách.

.. warning::

    Khi sử dụng lại một mesh trong scene, hãy nhớ rằng UV sẽ được tạo cho instance đầu tiên được tìm thấy. Nếu mesh được sử dụng lại với các scale khác nhau (và các scale chênh lệch rất lớn, lớn hơn một nửa hoặc gấp đôi), điều này sẽ tạo ra lightmap kém hiệu quả. Để tránh việc này, hãy điều chỉnh thuộc tính **Lightmap Scale** trong phần GeometryInstance3D của node MeshInstance3D. Thuộc tính này cho phép bạn *increase* mức độ chi tiết của lightmap cho các node MeshInstance3D cụ thể (nhưng không thể giảm).

    Ngoài ra, không nên *not* bỏ qua các tệp ``*.unwrap_cache`` trong hệ thống quản lý phiên bản, vì các tệp này đảm bảo rằng UV2 được reimport nhất quán giữa các nền tảng và phiên bản engine.

Unwrap từ trong Godot
~~~~~~~~~~~~~~~~~~~~~

.. warning::

    Nếu thao tác trong menu Mesh này được sử dụng trên một scene 3D đã import, UV2 được tạo sẽ bị mất khi scene được tải lại.

Godot có tùy chọn unwrap mesh và trực quan hóa các kênh UV. Sau khi chọn một node MeshInstance3D, bạn có thể tìm thấy tùy chọn này trong menu **Mesh** ở phía trên viewport của trình chỉnh sửa 3D:

.. image:: img/lightmap_gi_mesh_menu.webp

Thao tác này sẽ tạo một tập hợp tọa độ UV2 thứ hai để dùng cho việc bake. Kích thước texture cũng sẽ được tự động thiết lập.

Unwrap từ phần mềm modeling 3D của bạn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn cuối cùng là thực hiện việc này từ ứng dụng 3D yêu thích của bạn. Cách tiếp cận này nhìn chung **không được khuyến nghị**, nhưng được giải thích để bạn biết rằng nó tồn tại. Ưu điểm chính là đối với các đối tượng phức tạp mà bạn có thể muốn nhập lại nhiều lần, quá trình tạo texture trong Godot có thể khá tốn kém, vì vậy việc unwrap trước khi nhập có thể nhanh hơn.

Chỉ cần thực hiện unwrap trên lớp UV2 thứ hai.

.. image:: img/lightmap_gi_blender.webp

Sau đó, nhập scene 3D như bình thường. Hãy nhớ rằng bạn sẽ cần đặt kích thước texture cho mesh sau khi nhập.

.. image:: img/lightmap_gi_lmsize.webp

Nếu sử dụng các mesh bên ngoài khi nhập, kích thước sẽ được giữ nguyên. Hãy lưu ý rằng hầu hết công cụ unwrap trong phần mềm dựng hình 3D không chú trọng chất lượng vì chúng được thiết kế để hoạt động nhanh. Phần lớn thời gian, bạn sẽ cần sử dụng seams hoặc các kỹ thuật khác để tạo kết quả unwrap tốt hơn.

Tạo UV2 cho mesh nguyên thủy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Tùy chọn này chỉ khả dụng cho các mesh nguyên thủy như :ref:`class_BoxMesh`,
    :ref:`class_CylinderMesh`, :ref:`class_PlaneMesh`, v.v.

Bật UV2 trên các mesh nguyên thủy cho phép chúng nhận và đóng góp vào ánh sáng đã bake. Tùy chọn này có thể được sử dụng trong một số thiết lập ánh sáng nhất định. Ví dụ: bạn có thể ẩn một torus có material phát sáng sau khi bake lightmap để tạo ra một area light bám theo hình dạng của torus.

Theo mặc định, các mesh nguyên thủy không được tạo UV2 để tiết kiệm tài nguyên (vì các mesh này có thể được tạo trong lúc gameplay). Bạn có thể chỉnh sửa mesh nguyên thủy trong inspector và bật **Add UV2** để engine tự động tạo UV2 cho mesh nguyên thủy. Giá trị mặc định của **UV2 Padding** được điều chỉnh để tránh hầu hết hiện tượng lightmap bleeding mà không lãng phí quá nhiều không gian ở các cạnh. Nếu chỉ nhận thấy lightmap bleeding trên một mesh nguyên thủy cụ thể, bạn có thể phải tăng **UV2 Padding**.

**Lightmap Size Hint** biểu thị kích thước mà một mesh chiếm trên texture lightmap, tùy thuộc vào các thuộc tính kích thước của mesh và giá trị **UV2 Padding**. Không nên thay đổi thủ công **Lightmap Size Hint**, vì mọi thay đổi sẽ bị mất khi scene được tải lại.

Tạo UV2 cho các node CSG
~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.4, bạn có thể
:ref:`chuyển đổi một node CSG và các node con của nó thành MeshInstance3D <doc_csg_tools_converting_to_mesh_instance_3d>`. Bạn có thể sử dụng cách này để bake lightmap trên một node CSG bằng cách thực hiện các bước sau:

- Chọn node CSG gốc và chọn **CSG > Bake Mesh Instance** ở đầu viewport của trình chỉnh sửa 3D.
- Ẩn node CSG gốc vừa được bake (node này không tự động bị ẩn).
- Chọn node MeshInstance3D mới được tạo và chọn **Mesh > Unwrap UV2 for Lightmap/AO**.
- Bake lightmap.

.. tip::

    Hãy nhớ giữ node CSG ban đầu trong scene tree để bạn có thể thay đổi hình học sau này nếu cần. Để thay đổi hình học, hãy xóa node MeshInstance3D và hiển thị lại node CSG gốc.

Kiểm tra UV2
~~~~~~~~~~~~

Trong menu **Mesh** đã đề cập trước đó, bạn có thể trực quan hóa các tọa độ texture UV2. Nếu có lỗi, hãy kiểm tra lại để đảm bảo các mesh có những tọa độ UV2 này:

.. image:: img/lightmap_gi_uvchannel.webp

Thiết lập scene
---------------

Trước khi thực hiện bất kỳ việc gì, cần thêm một node **LightmapGI** vào scene. Node này sẽ bật tính năng bake ánh sáng trên tất cả các node (và node con) trong scene đó, kể cả các scene được instance.

.. image:: img/lightmap_gi_scene.webp

Một sub-scene có thể được instance nhiều lần, vì baker hỗ trợ việc này. Mỗi instance sẽ được gán một lightmap riêng. Để tránh các vấn đề do tỷ lệ texel của lightmap không nhất quán, hãy đảm bảo tuân thủ quy tắc về tỷ lệ của mesh đã đề cập trước đó.

Thiết lập mesh
~~~~~~~~~~~~~~

Để một node **MeshInstance3D** tham gia quá trình bake, bake mode của node đó phải được đặt thành **Static**. Các mesh có bake mode được đặt thành **Disabled** hoặc **Dynamic** sẽ bị lightmapper bỏ qua.

.. image:: img/lightmap_gi_use.webp

Khi tự động tạo lightmap trong quá trình nhập scene, tùy chọn này sẽ được bật tự động.

Thiết lập ánh sáng
~~~~~~~~~~~~~~~~~~

Theo mặc định, ánh sáng chỉ được bake với ánh sáng gián tiếp. Điều này có nghĩa là shadowmapping và ánh sáng vẫn mang tính động, đồng thời ảnh hưởng đến các đối tượng chuyển động, nhưng các lần phản xạ ánh sáng từ nguồn sáng đó sẽ được bake.

Có thể tắt ánh sáng (không bake) hoặc bake hoàn toàn (trực tiếp và gián tiếp). Bạn có thể điều khiển tùy chọn này từ menu **Bake Mode** của các nguồn sáng:

.. image:: img/lightmap_gi_bake_mode.webp

Các mode gồm:

Disabled
~~~~~~~~

Nguồn sáng sẽ bị bỏ qua khi bake lightmap. Đây là mode nên sử dụng cho các hiệu ứng ánh sáng động như vụ nổ và hiệu ứng vũ khí.

.. warning::

    Việc ẩn một nguồn sáng không ảnh hưởng đến kết quả bake lightmap. Điều này có nghĩa là bạn phải sử dụng bake mode Disabled thay vì ẩn node Light bằng cách tắt thuộc tính **Visible** của node đó.

Dynamic
~~~~~~~

Đây là mode mặc định và là sự cân bằng giữa hiệu năng với khả năng hoạt động theo thời gian thực. Chỉ ánh sáng gián tiếp được bake. Ánh sáng trực tiếp và bóng vẫn hoạt động theo thời gian thực, giống như khi không có LightmapGI.

Mode này cho phép thực hiện các thay đổi *tinh tế* đối với màu sắc, năng lượng và vị trí của nguồn sáng mà hình ảnh vẫn tương đối chính xác. Ví dụ, bạn có thể dùng mode này để tạo các ngọn đuốc tĩnh nhấp nháy với ánh sáng gián tiếp đã được bake.

Tùy thuộc vào giá trị của **Shadowmask Mode**, vẫn có thể nhận được bóng đã bake ở xa đối với DirectionalLight3D. Điều này cho phép bóng ở gần hoạt động theo thời gian thực và hiển thị các đối tượng động, đồng thời cho phép các đối tượng tĩnh ở xa vẫn đổ bóng.

Static
~~~~~~

Cả ánh sáng gián tiếp và trực tiếp đều sẽ được bake. Vì các bề mặt tĩnh có thể hoàn toàn bỏ qua việc tính toán ánh sáng và bóng, mode này mang lại hiệu năng tốt nhất cùng với bóng mượt không bao giờ mờ dần theo khoảng cách. Ánh sáng theo thời gian thực sẽ không còn ảnh hưởng đến các bề mặt đã bake, nhưng vẫn ảnh hưởng đến các đối tượng động. Khi sử dụng bake mode **All** trên một nguồn sáng, các đối tượng động sẽ không đổ bóng theo thời gian thực lên các bề mặt đã bake, vì vậy bạn cần sử dụng một cách tiếp cận khác, chẳng hạn như blob shadow. Blob shadow có thể được triển khai bằng node Decal.

Nguồn sáng sẽ hoàn toàn không thể điều chỉnh trong gameplay. Việc di chuyển nguồn sáng hoặc thay đổi màu sắc (hay năng lượng) của nó sẽ không ảnh hưởng đến các bề mặt tĩnh.

Vì các chế độ bake có thể được điều chỉnh cho từng đèn, bạn có thể tạo các thiết lập đèn bake kết hợp. Một lựa chọn phổ biến là sử dụng DirectionalLight theo thời gian thực với chế độ bake được đặt thành **Dynamic**, đồng thời sử dụng chế độ bake **Static** cho OmniLight và SpotLight. Cách này mang lại hiệu năng tốt mà vẫn cho phép các đối tượng động đổ bóng theo thời gian thực trong các khu vực ngoài trời.

Các đèn được bake hoàn toàn cũng có thể sử dụng thuộc tính **Size** (omni/spot) hoặc **Angular Distance** (directional) của các light node. Điều này cho phép tạo bóng có vùng nửa tối (penumbra) chân thực, tăng kích thước khi khoảng cách giữa đối tượng đổ bóng và bóng tăng lên. Cách này cũng có chi phí hiệu năng thấp hơn so với bóng PCSS theo thời gian thực, vì chỉ các đối tượng động mới được kết xuất bóng theo thời gian thực.

.. image:: img/lightmap_gi_omnilight_size.png

Baking
------

Để bắt đầu quá trình bake, hãy nhấp vào nút **Bake Lightmaps** ở phía trên viewport trình chỉnh sửa 3D khi chọn node LightmapGI:

.. image:: img/lightmap_gi_bake.webp

Quá trình này có thể mất từ vài giây đến vài phút (hoặc vài giờ), tùy thuộc vào kích thước cảnh, phương pháp bake và chất lượng được chọn.

.. warning::

    Baking lightmap là một quá trình có thể yêu cầu nhiều bộ nhớ video, đặc biệt khi texture kết quả có kích thước lớn. Do các giới hạn nội bộ, engine cũng có thể bị crash nếu kích thước texture được tạo quá lớn (ngay cả trên các hệ thống có nhiều bộ nhớ video).

    Để tránh crash, hãy đảm bảo kích thước texel của lightmap trong dock Import được đặt đủ cao.

Tinh chỉnh
~~~~~~~~~~

- **Quality:** Có bốn chế độ chất lượng bake: Low, Medium, High và Ultra. Chất lượng cao hơn sẽ mất nhiều thời gian hơn, nhưng tạo ra lightmap có hình ảnh đẹp hơn và ít nhiễu hơn. Sự khác biệt đặc biệt dễ nhận thấy với các vật liệu phát sáng hoặc những khu vực nhận rất ít hoặc không nhận ánh sáng trực tiếp. Mỗi chế độ chất lượng bake có thể được điều chỉnh thêm trong Project Settings.
- **Supersampling:** Tùy chọn này tạo lightmap ở độ phân giải cao hơn rồi giảm độ phân giải. Điều này làm giảm nhiễu và hiện tượng rò rỉ ánh sáng, đồng thời tạo ra bóng tốt hơn với các chi tiết có quy mô nhỏ. Tuy nhiên, việc sử dụng tùy chọn này sẽ làm tăng thời gian bake và mức sử dụng bộ nhớ trong quá trình baking lightmap. **Supersampling Factor** thay đổi kích thước mà lightmap được kết xuất trước khi giảm độ phân giải.
- **Bounces:** Số lần bounce được sử dụng cho ánh sáng gián tiếp. Giá trị mặc định (``3``) là sự cân bằng tốt giữa thời gian bake và chất lượng. Giá trị cao hơn sẽ khiến ánh sáng bounce nhiều lần hơn trước khi dừng lại, giúp ánh sáng gián tiếp trông mượt hơn (nhưng cũng có thể sáng hơn, tùy thuộc vào vật liệu và hình học).
- **Bounce Indirect Energy:** Hệ số nhân toàn cục được sử dụng khi bake năng lượng gián tiếp của các đèn. Giá trị này nhân với giá trị **Indirect Energy** riêng của mỗi đèn. Các giá trị khác ``1.0`` không chính xác về mặt vật lý, nhưng có thể được sử dụng cho mục đích nghệ thuật.
- **Directional:** Khi được bật, tùy chọn này lưu thông tin hướng cho lightmap. Điều này cải thiện hình thức của các vật liệu có normal map trên các bề mặt được bake, đặc biệt với các đèn được bake hoàn toàn (vì chúng cũng có ánh sáng trực tiếp được bake). Nhược điểm là lightmap định hướng có chi phí kết xuất cao hơn một chút. Chúng cũng cần nhiều thời gian bake hơn và tạo ra kích thước tệp lớn hơn.
- **Shadowmask Mode:** Nếu được đặt thành chế độ khác **None**, DirectionalLight3D đầu tiên trong cảnh có chế độ global illumination **Dynamic** sẽ có bóng tĩnh được bake vào một texture riêng gọi là *shadowmask*. Tùy chọn này có thể được dùng để cho phép các đối tượng tĩnh ở xa đổ bóng lên các đối tượng tĩnh khác, bất kể khoảng cách đến camera. Xem :ref:`phần về shadowmasking <doc_using_lightmap_gi_shadowmask>` để biết thêm chi tiết.
- **Interior:** Khi được bật, ánh sáng môi trường sẽ không được lấy. Hãy sử dụng tùy chọn này cho các cảnh hoàn toàn trong nhà để tránh rò rỉ ánh sáng.
- **Use Texture for Bounces:** Khi được bật, một texture chứa thông tin ánh sáng sẽ được tạo để tăng tốc quá trình tạo ánh sáng gián tiếp, đổi lại là giảm một phần độ chính xác. Hình học có thể xuất hiện thêm các hiện tượng rò rỉ ánh sáng khi sử dụng lightmap có độ phân giải thấp hoặc UV làm lightmap bị kéo giãn đáng kể trên các bề mặt. Nếu không chắc chắn, hãy để tùy chọn này được bật.
- **Use Denoiser:** Khi được bật, tùy chọn này sử dụng thuật toán khử nhiễu để làm giảm đáng kể nhiễu trong lightmap. Điều này làm tăng thời gian bake và đôi khi có thể tạo ra hiện tượng bất thường, nhưng kết quả thường rất đáng giá. Xem
  :ref:`doc_using_lightmap_gi_denoising` để biết thêm thông tin.
- **Denoiser Strength:** Mức độ mạnh của bước khử nhiễu được áp dụng cho các lightmap được tạo. Giá trị cao hơn loại bỏ nhiễu hiệu quả hơn, nhưng có thể làm giảm chi tiết bóng tĩnh. Chỉ có tác dụng khi tính năng khử nhiễu được bật và phương pháp khử nhiễu là :abbr:`JNLM (Non-Local Means with Joint Filtering)` (:abbr:`OIDN (Open Image Denoise)` không có thiết lập denoiser strength).
- **Bias:** Giá trị offset được sử dụng cho bóng trong các đơn vị 3D. Thông thường bạn không cần thay đổi giá trị này, trừ khi gặp vấn đề với hiện tượng ánh sáng xuyên qua hoặc các điểm tối trong lightmap sau khi bake. Thiết lập này không ảnh hưởng đến bóng theo thời gian thực được đổ lên các bề mặt đã bake (đối với các đèn có chế độ bake **Dynamic**).
- **Max Texture Size:** Kích thước texture tối đa của texture atlas được tạo. Giá trị cao hơn sẽ tạo ra ít lát hơn, nhưng có thể không hoạt động trên mọi phần cứng do giới hạn phần cứng về kích thước texture. Nếu không chắc chắn, hãy giữ giá trị mặc định là ``16384``.
- **Environment > Mode:** Kiểm soát cách lấy ánh sáng môi trường khi baking lightmap. Giá trị mặc định **Scene** phù hợp với các level có những phần bên ngoài hiển thị được. Đối với các cảnh hoàn toàn trong nhà, hãy đặt thành **Disabled** để tránh rò rỉ ánh sáng và tăng tốc quá trình bake. Tùy chọn này cũng có thể được đặt thành **Custom Sky** hoặc **Custom Color** để sử dụng ánh sáng môi trường khác với sky môi trường thực tế của cảnh.
- **Gen Probes > Subdiv:** Xem :ref:`doc_using_lightmap_gi_dynamic_objects`.
- **Data > Light Data:** Xem :ref:`doc_using_lightmap_gi_data`.

.. _doc_using_lightmap_gi_shadowmask:

Sử dụng shadowmasking cho bóng định hướng ở xa
----------------------------------------------

Khi sử dụng DirectionalLight3D, khoảng cách tối đa mà đèn có thể vẽ bóng theo thời gian thực bị giới hạn bởi thuộc tính **Shadow Max Distance**. Đây có thể là vấn đề trong các cảnh lớn, vì các đối tượng ở xa sẽ không có bóng từ DirectionalLight3D. Mặc dù có thể khắc phục bằng cách sử dụng chế độ global illumination **Static** trên DirectionalLight3D, cách này có một số nhược điểm:

- Vì cả ánh sáng trực tiếp và gián tiếp đều được bake, không có cách nào để các đối tượng động đổ bóng lên các bề mặt tĩnh theo cách chân thực. Godot bỏ qua hoàn toàn việc lấy mẫu bóng trong trường hợp này để tránh các hiện tượng "chiếu sáng kép".
- Bóng tĩnh ở khoảng cách gần thiếu chi tiết, vì chúng chỉ dựa vào texture lightmap chứ không dựa vào các cascade bóng theo thời gian thực.

Chúng ta có thể tránh những nhược điểm này mà vẫn hưởng lợi từ bóng ở xa bằng cách sử dụng *shadowmasking*. Mặc dù các đối tượng động sẽ không nhận bóng từ shadowmask, tùy chọn này vẫn cải thiện đáng kể hình ảnh vì hầu hết các cảnh chủ yếu bao gồm các đối tượng tĩnh.

Vì riêng texture lightmap không chứa thông tin bóng, chúng ta có thể bake thông tin bóng này vào một texture riêng có tên là *shadowmask*.

Shadowmasking chỉ ảnh hưởng đến DirectionalLight3D đầu tiên trong scene (được xác định theo thứ tự trong cây) có chế độ global illumination **Dynamic**. Không thể sử dụng shadowmasking với chế độ global illumination **Static**, vì chế độ này hoàn toàn bỏ qua việc lấy mẫu bóng trên các object tĩnh. Điều này là do chế độ global illumination Static bake cả ánh sáng trực tiếp và gián tiếp.

Có ba chế độ shadowmasking:

- **None (mặc định):** Không bake texture shadowmask. Bóng đổ định hướng sẽ không hiển thị bên ngoài phạm vi được chỉ định bởi thuộc tính **Shadow Max Distance** của DirectionalLight3D.
- **Replace:** Bake texture shadowmask và sử dụng texture này để vẽ bóng đổ định hướng khi ở bên ngoài phạm vi được chỉ định bởi thuộc tính **Shadow Max Distance** của DirectionalLight3D. Bóng trong phạm vi này vẫn hoàn toàn theo thời gian thực. Tùy chọn này thường phù hợp nhất với hầu hết scene, vì nó xử lý tốt các object tĩnh có chuyển động nhẹ (ví dụ: bóng của tán lá).
- **Overlay:** Bake texture shadowmask và sử dụng texture này để vẽ bóng đổ định hướng bất kể khoảng cách đến camera. Bóng trong phạm vi thuộc tính **Shadow Max Distance** của DirectionalLight3D sẽ được phủ lên bởi bóng theo thời gian thực. Điều này có thể làm cho quá trình chuyển tiếp giữa bóng theo thời gian thực và bóng đã bake bớt đột ngột, nhưng phải đánh đổi bằng hiệu ứng "smearing" xuất hiện trên bóng của object tĩnh, tùy thuộc vào mật độ texel của lightmap. Ngoài ra, chế độ này xử lý không tốt bằng với các object tĩnh có chuyển động nhẹ (chẳng hạn như tán lá), vì bóng đã bake không thể được animate theo thời gian. Tuy vậy, đối với các scene mà camera di chuyển nhanh, đây có thể là lựa chọn tốt hơn **Replace**.

Dưới đây là so sánh trực quan giữa các chế độ shadowmask trong một scene có **Shadow Max Distance** được đặt rất thấp nhằm phục vụ mục đích so sánh. Các hộp màu xanh là những object động, còn phần còn lại của scene là một object tĩnh. Scene chỉ có một DirectionalLight3D với chế độ global illumination Dynamic:

.. figure:: img/lightmap_gi_shadowmask.webp
   :align: center
   :alt: So sánh giữa các chế độ shadowmask

   So sánh giữa các chế độ shadowmask

.. note::

    Có thể chuyển đổi giữa các chế độ shadowmask **Replace** và **Overlay** mà không cần bake lại lightmap.

Cân bằng thời gian bake và chất lượng
-------------------------------------

Vì quá trình bake chất lượng cao có thể mất rất nhiều thời gian (lên đến hàng chục phút đối với các scene lớn và phức tạp), bạn nên sử dụng các thiết lập chất lượng thấp hơn lúc đầu. Sau đó, khi đã chắc chắn về thiết lập ánh sáng của scene, hãy tăng các thiết lập chất lượng và thực hiện một lần bake "final" trước khi export project.

Việc giảm độ phân giải lightmap bằng cách tăng **Lightmap Texel Size** trên các scene 3D đã import cũng sẽ tăng tốc đáng kể quá trình bake. Tuy nhiên, bạn sẽ phải reimport tất cả scene 3D có lightmap trước khi có thể bake lại lightmap.

.. _doc_using_lightmap_gi_denoising:

Khử nhiễu
---------

Vì quá trình bake lightmap dựa trên raytracing, lightmap đã bake "raw" luôn có nhiễu nhìn thấy được. Nhiễu đặc biệt dễ thấy ở những khu vực khó tiếp cận bởi ánh sáng phản xạ, chẳng hạn như các khu vực trong nhà có những lỗ mở nhỏ nơi ánh nắng có thể chiếu vào. Có thể giảm nhiễu bằng cách tăng chất lượng bake, nhưng việc này sẽ làm tăng đáng kể thời gian bake.

.. figure:: img/lightmap_gi_denoiser_comparison.webp
   :align: center
   :alt: So sánh khi tắt và bật khử nhiễu

   So sánh khi tắt và bật khử nhiễu (với denoiser JNLM mặc định).

Để khắc phục nhiễu mà không làm tăng quá nhiều thời gian bake, có thể sử dụng denoiser. Denoiser là một thuật toán chạy trên lightmap đã bake cuối cùng, phát hiện các mẫu nhiễu và làm mềm chúng đồng thời cố gắng bảo toàn chi tiết tốt nhất có thể. Godot cung cấp hai thuật toán khử nhiễu:

JNLM (Non-Local Means with Joint Filtering)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

JNLM là phương pháp khử nhiễu mặc định và được tích hợp trong Godot. Phương pháp này sử dụng một thuật toán khử nhiễu đơn giản nhưng hiệu quả có tên là *non-local means*. JNLM chạy trên GPU bằng compute shader và tương thích với mọi GPU có thể chạy các renderer dựa trên RenderingDevice của Godot 4. Không cần thiết lập bổ sung.

Có thể điều chỉnh khả năng khử nhiễu của JNLM bằng thuộc tính **Denoiser Strength**, thuộc tính này hiển thị khi **Use Denoiser** được bật. Giá trị cao hơn có thể loại bỏ nhiễu hiệu quả hơn, nhưng phải đánh đổi bằng việc làm mất chi tiết bóng đối với bóng tĩnh.

.. figure:: img/lightmap_gi_denoiser_jnlm_strength.webp
   :align: center
   :alt: So sánh các giá trị cường độ denoiser của JNLM

   So sánh các giá trị cường độ denoiser của JNLM. Giá trị cao hơn có thể làm giảm chi tiết.

OIDN (Open Image Denoise)
~~~~~~~~~~~~~~~~~~~~~~~~~

Không giống JNLM, OIDN sử dụng phương pháp machine learning để khử nhiễu lightmap. OIDN có một model được huấn luyện chuyên biệt để loại bỏ nhiễu khỏi lightmap, đồng thời bảo toàn nhiều chi tiết bóng hơn trong hầu hết scene so với JNLM.

OIDN có thể chạy trên GPU nếu đã cấu hình hardware acceleration. Với GPU cao cấp hiện đại, cách này có thể tăng tốc hơn 50× so với khử nhiễu dựa trên CPU:

- Trên GPU AMD, phải cài đặt và cấu hình HIP.
- Trên GPU NVIDIA, phải cài đặt và cấu hình CUDA. Trình cài đặt NVIDIA có thể tự động thực hiện việc này, nhưng trên Linux, các thư viện CUDA có thể không được cài đặt theo mặc định. Hãy kiểm tra lại để bảo đảm các gói CUDA của bản phân phối Linux đã được cài đặt.
- Trên GPU Intel, phải cài đặt và cấu hình SYCL.

Nếu không có hardware acceleration, OIDN sẽ chuyển sang khử nhiễu dựa trên CPU đa luồng. Để xác nhận khử nhiễu dựa trên GPU có hoạt động hay không, hãy sử dụng công cụ theo dõi mức sử dụng GPU trong khi bake lightmap và quan sát phần trăm sử dụng GPU cũng như mức sử dụng VRAM khi bước khử nhiễu được hiển thị trong trình chỉnh sửa Godot. Công cụ dòng lệnh ``nvidia-smi`` có thể hữu ích cho việc này.

OIDN không được tích hợp trong Godot do kích thước tải xuống tương đối lớn. Bạn có thể tải các gói binary OIDN đã biên dịch sẵn từ `website <https://www.openimagedenoise.org/downloads.html>`__ của OIDN. Giải nén gói vào một vị trí trên PC, sau đó chỉ định đường dẫn đến executable ``oidnDenoise`` trong Editor Settings (**FileSystem > Tools > OIDN > OIDN Denoise Path**). Executable này nằm trong thư mục ``bin`` của gói binary mà bạn đã giải nén.

Sau khi chỉ định đường dẫn đến executable khử nhiễu OIDN, hãy thay đổi phương pháp khử nhiễu trong project settings bằng cách đặt **Rendering > Lightmapping > Denoiser** thành **OIDN**. Thay đổi này sẽ ảnh hưởng đến tất cả lần bake lightmap của project sau khi thiết lập được thay đổi.

.. note::

    Phương pháp khử nhiễu được cấu hình trong cài đặt dự án thay vì cài đặt trình chỉnh sửa. Điều này nhằm đảm bảo các thành viên khác nhau trong nhóm làm việc trên cùng một dự án đều sử dụng cùng một phương pháp khử nhiễu để cho ra kết quả nhất quán.

.. figure:: img/lightmap_gi_denoiser_jnlm_vs_oidn.webp
   :align: center
   :alt: So sánh giữa các trình khử nhiễu JNLM và OIDN

   So sánh giữa các trình khử nhiễu JNLM và OIDN. Lưu ý rằng OIDN bảo toàn chi tiết tốt hơn và giảm các đường nối giữa những đối tượng khác nhau.

.. _doc_using_lightmap_gi_dynamic_objects:

Các đối tượng động
------------------

Không giống VoxelGI và SDFGI, các đối tượng động nhận ánh sáng gián tiếp theo cách khác với các đối tượng tĩnh. Điều này là do lightmapping chỉ được thực hiện trên các đối tượng tĩnh.

Để hiển thị ánh sáng gián tiếp trên các đối tượng động, hệ thống probe 3D được sử dụng, với các light probe được phân bố khắp scene. Khi baking lightmap, lightmapper sẽ tính toán lượng ánh sáng *indirect* mà probe nhận được. Ánh sáng trực tiếp không được lưu trong các light probe, ngay cả đối với những đèn có chế độ bake được đặt thành **Static** (vì các đối tượng động vẫn tiếp tục được chiếu sáng theo thời gian thực).

Có 2 cách để thêm light probe vào scene:

- **Automatic:** Đặt **Gen Probes > Subdiv** thành giá trị khác **Disabled**, sau đó bake lightmap. Giá trị mặc định là ``8``, nhưng bạn có thể chọn giá trị lớn hơn để cải thiện độ chính xác, đổi lại thời gian bake lâu hơn và kích thước tệp đầu ra lớn hơn.
- **Manual:** Ngoài hoặc thay cho việc tự động tạo probe, bạn có thể thêm light probe theo cách thủ công bằng cách thêm các node :ref:`class_LightmapProbe` vào scene. Cách này có thể được dùng để cải thiện chi tiết ánh sáng ở những khu vực mà các đối tượng động thường xuyên di chuyển qua. Sau khi đặt các node LightmapProbe trong scene, bạn phải bake lại lightmap để chúng có hiệu lực.

.. note::

    Sau khi baking lightmap, bạn sẽ thấy các hình cầu màu trắng trong scene 3D, biểu thị cách ánh sáng đã bake sẽ ảnh hưởng đến các đối tượng động. Các hình cầu này **không** xuất hiện trong project đang chạy.

    Nếu muốn ẩn các hình cầu này trong trình chỉnh sửa, hãy bật/tắt **View > Gizmos > LightmapGI** ở phía trên trình chỉnh sửa 3D (biểu tượng "mắt nhắm" cho biết gizmo đang bị ẩn).

.. _doc_using_lightmap_gi_data:

Dữ liệu Lightmap
----------------

Thuộc tính **Data > Light Data** trong node LightmapGI chứa dữ liệu lightmap sau khi baking. Các texture được lưu vào đĩa, nhưng thuộc tính này cũng chứa dữ liệu capture cho các đối tượng động, có thể chiếm nhiều dung lượng. Nếu bạn đang sử dụng scene ở định dạng ``.tscn``, bạn nên lưu resource này vào một tệp nhị phân ``.lmbake`` bên ngoài để tránh làm phình scene ``.tscn`` bằng dữ liệu nhị phân được mã hóa trong Base64.

.. tip::

    Tệp EXR được tạo có thể được xem và thậm chí chỉnh sửa bằng trình chỉnh sửa ảnh để thực hiện hậu xử lý nếu cần. Tuy nhiên, hãy nhớ rằng mọi thay đổi đối với tệp EXR sẽ bị mất khi bake lại lightmap.

Giảm các lỗi hiển thị của LightmapGI
------------------------------------

Nếu nhận thấy các node LightmapGI liên tục xuất hiện rồi biến mất khi camera di chuyển, nhiều khả năng là do engine đang render quá nhiều instance LightmapGI cùng lúc. Godot bị giới hạn ở việc render 8 node LightmapGI cùng lúc, nghĩa là tối đa 8 instance có thể nằm trong chế độ xem của camera trước khi một số instance bắt đầu nhấp nháy.
