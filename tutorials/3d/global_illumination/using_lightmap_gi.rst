.. _doc_using_lightmap_gi:

Sử dụng global illumination bằng Lightmap
=========================================

Lightmap đã bake là một quy trình dùng để thêm ánh sáng gián tiếp (hoặc ánh sáng bake hoàn toàn) vào scene. Không giống :ref:`VoxelGI <doc_using_voxel_gi>` và
:ref:`SDFGI <doc_using_sdfgi>` approaches, baked lightmaps work fine on low-end PCs
và các thiết bị di động, vì chúng gần như không tiêu tốn tài nguyên trong runtime. Ngoài ra, không giống VoxelGI và SDFGI, lightmap đã bake có thể tùy chọn được dùng để lưu ánh sáng trực tiếp, nhờ đó cải thiện hiệu năng hơn nữa.

Không giống VoxelGI và SDFGI, lightmap đã bake hoàn toàn tĩnh. Sau khi bake, chúng không thể được chỉnh sửa dưới bất kỳ hình thức nào. Chúng cũng không cung cấp phản chiếu cho scene, vì vậy việc sử dụng :ref:`doc_reflection_probes` cùng với nó trong các không gian nội thất (hoặc sử dụng Sky trong không gian ngoại thất) là yêu cầu bắt buộc để đạt chất lượng tốt.

Vì được bake, chúng ít gặp vấn đề về light bleeding hơn VoxelGI và SDFGI, đồng thời ánh sáng gián tiếp thường trông đẹp hơn. Nhược điểm là việc bake lightmap mất nhiều thời gian hơn so với bake VoxelGI. Trong khi bake VoxelGI có thể hoàn tất chỉ trong vài giây, bake lightmap có thể mất vài phút hoặc lâu hơn. Điều này có thể làm giảm đáng kể tốc độ lặp, vì vậy bạn chỉ nên bake lightmap khi thực sự cần xem các thay đổi về ánh sáng. Lightmap được bake trên GPU, nên quá trình bake ánh sáng sẽ nhanh hơn nếu bạn có GPU chuyên dụng tầm trung hoặc cao cấp.

Baking lightmap cũng sẽ dành riêng slot UV2 của các material đã bake, nghĩa là bạn không thể sử dụng slot này cho các mục đích khác trong material (dù là trong
:ref:`doc_standard_material_3d` or in custom shaders).

Mặc dù thiếu tính linh hoạt, lightmap đã bake thường mang lại cả chất lượng *và* hiệu năng tốt nhất cùng lúc trong các scene (phần lớn) tĩnh. Vì vậy, lightmap vẫn phổ biến trong phát triển game, dù lightmap là kỹ thuật global illumination lâu đời nhất trong game.

.. seealso::

    Không chắc LightmapGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI hiện có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: LightmapGI disabled.

   LightmapGI disabled.

.. figure:: img/gi_lightmap_gi_indirect_only.webp
   :alt: LightmapGI enabled (with indirect light baked only).

   LightmapGI enabled (with indirect light baked only). Direct light is still
   real-time, allowing for subtle changes during gameplay.

.. figure:: img/gi_lightmap_gi_direct_and_indirect.webp
   :alt: LightmapGI enabled (with direct and indirect light baked).

   LightmapGI enabled (with direct and indirect light baked). Best performance,
   but lower quality visuals. Notice the blurrier sun shadow in the top-right
   corner.

Dưới đây là một số so sánh về hình ảnh của LightmapGI và VoxelGI. Hãy lưu ý rằng lightmap chính xác hơn, nhưng cũng chịu ảnh hưởng bởi việc ánh sáng nằm trên một texture đã unwrap, nên các chuyển tiếp và độ phân giải có thể không được tốt. VoxelGI trông kém chính xác hơn (vì chỉ là một phép xấp xỉ), nhưng nhìn chung mượt hơn.

.. image:: img/lightmap_gi_comparison.png

SDFGI cũng kém chính xác hơn so với LightmapGI. Tuy nhiên, SDFGI có thể hỗ trợ các thế giới mở lớn mà không cần bake.

Thiết lập
---------

.. warning::

    Không hỗ trợ bake lightmap trong các web editor do những hạn chế của graphics API. Trên nền tảng web, chỉ hỗ trợ *render* các lightmap đã được bake trên một nền tảng khác.

.. note::

    Node LightmapGI chỉ bake các node nằm cùng cấp với node LightmapGI (các node sibling), hoặc các node là con của node LightmapGI. Điều này cho phép bạn sử dụng nhiều node LightmapGI để bake các phần khác nhau của scene một cách độc lập.

Trước hết, trước khi lightmapper có thể thực hiện bất kỳ thao tác nào, các object cần bake phải có một layer UV2 và một kích thước texture. Layer UV2 là một tập hợp các tọa độ texture phụ, bảo đảm mỗi face trong object có vị trí riêng trên UV map. Các face không được dùng chung pixel trong texture.

Có một vài cách để bảo đảm object của bạn có layer UV2 và kích thước texture riêng:

Unwrap khi import scene (khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong hầu hết trường hợp, đây là cách tốt nhất để sử dụng. Nhược điểm duy nhất là với các model lớn, thao tác unwrap có thể mất một lúc khi import. Tuy nhiên, Godot sẽ cache UV2 qua các lần reimport, vì vậy UV2 chỉ được tạo lại khi cần.

Chọn scene đã import trong filesystem dock, sau đó chuyển đến **Import** dock. Tại đó, bạn có thể chỉnh sửa tùy chọn sau:

.. image:: img/lightmap_gi_import.webp

Tùy chọn **Meshes > Light Baking** phải được đặt thành **Static Lightmaps (VoxelGI/SDFGI/LightmapGI)**:

.. image:: img/lightmap_gi_mesh_import_meshes.webp

Khi unwrap lúc import, bạn có thể điều chỉnh kích thước texture bằng tùy chọn **Meshes > Lightmap Texel Size**. Giá trị *thấp hơn* sẽ tạo ra lightmap chi tiết hơn, có thể cho chất lượng hình ảnh cao hơn nhưng phải đánh đổi bằng thời gian bake lâu hơn và kích thước file lightmap lớn hơn. Giá trị mặc định ``0.2`` phù hợp với các scene nhỏ/trung bình, nhưng bạn có thể muốn tăng lên ``0.5`` hoặc thậm chí cao hơn đối với các scene lớn hơn. Điều này đặc biệt đúng nếu bạn chỉ bake ánh sáng gián tiếp, vì ánh sáng gián tiếp là dữ liệu tần số thấp (nghĩa là không cần texture độ phân giải cao để được biểu diễn chính xác).

Việc đặt tùy chọn này sẽ khiến tất cả mesh trong scene được tạo UV2 map đúng cách.

.. warning::

    Khi sử dụng lại một mesh trong scene, hãy nhớ rằng UV sẽ được tạo cho instance đầu tiên được tìm thấy. Nếu mesh được sử dụng lại với các scale khác nhau (và các scale chênh lệch rất lớn, lớn hơn một nửa hoặc gấp đôi), điều này sẽ tạo ra lightmap kém hiệu quả. Để tránh điều này, hãy điều chỉnh thuộc tính **Lightmap Scale** trong phần GeometryInstance3D của một node MeshInstance3D. Thuộc tính này cho phép bạn *tăng* mức độ chi tiết của lightmap cho các node MeshInstance3D cụ thể (nhưng không thể giảm).

    Ngoài ra, các file ``*.unwrap_cache`` *không nên* bị bỏ qua trong version control, vì những file này bảo đảm rằng việc reimport UV2 nhất quán giữa các nền tảng và các phiên bản engine.

Unwrap từ bên trong Godot
~~~~~~~~~~~~~~~~~~~~~~~~~

.. warning::

    Nếu thao tác trong menu Mesh này được sử dụng trên một scene 3D đã import, UV2 được tạo sẽ bị mất khi scene được tải lại.

Godot có tùy chọn unwrap mesh và trực quan hóa các kênh UV. Sau khi chọn một node MeshInstance3D, bạn có thể tìm thấy tùy chọn này trong menu **Mesh** ở phía trên viewport của trình chỉnh sửa 3D:

.. image:: img/lightmap_gi_mesh_menu.webp

Thao tác này sẽ tạo một bộ tọa độ UV2 thứ hai để dùng cho việc bake. Nó cũng sẽ tự động đặt kích thước texture.

Unwrap từ phần mềm modeling 3D của bạn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn cuối cùng là thực hiện việc này từ ứng dụng 3D yêu thích của bạn. Cách tiếp cận này nhìn chung **không được khuyến nghị**, nhưng được giải thích để bạn biết nó tồn tại. Ưu điểm chính là đối với các object phức tạp mà bạn có thể muốn re-import nhiều lần, quá trình tạo texture trong Godot có thể khá tốn thời gian, nên unwrap trước khi import có thể nhanh hơn.

Chỉ cần thực hiện unwrap trên layer UV2 thứ hai.

.. image:: img/lightmap_gi_blender.webp

Sau đó import scene 3D như bình thường. Hãy nhớ rằng bạn sẽ cần đặt kích thước texture cho mesh sau khi import.

.. image:: img/lightmap_gi_lmsize.webp

Nếu sử dụng mesh bên ngoài khi import, kích thước sẽ được giữ nguyên. Hãy lưu ý rằng hầu hết công cụ unwrap trong phần mềm modeling 3D không chú trọng chất lượng, vì chúng được thiết kế để hoạt động nhanh. Phần lớn trường hợp, bạn sẽ cần sử dụng seam hoặc các kỹ thuật khác để tạo kết quả unwrap tốt hơn.

Tạo UV2 cho các mesh primitive
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Tùy chọn này chỉ khả dụng cho các mesh primitive như :ref:`class_BoxMesh`,
    :ref:`class_CylinderMesh`, :ref:`class_PlaneMesh`, etc.

Bật UV2 trên các mesh primitive cho phép chúng nhận và đóng góp vào ánh sáng đã bake. Tùy chọn này có thể được sử dụng trong một số thiết lập ánh sáng nhất định. Ví dụ, bạn có thể ẩn một torus có material emissive sau khi bake lightmap để tạo một area light theo hình dạng của torus.

Theo mặc định, mesh primitive không được tạo UV2 để tiết kiệm tài nguyên (vì các mesh này có thể được tạo trong gameplay). Bạn có thể chỉnh sửa một mesh primitive trong inspector và bật **Add UV2** để engine tạo UV2 theo quy trình cho mesh primitive. Giá trị **UV2 Padding** mặc định được tinh chỉnh để tránh hầu hết lightmap bleeding mà không lãng phí quá nhiều không gian ở các cạnh. Nếu bạn chỉ nhận thấy lightmap bleeding trên một mesh primitive cụ thể, có thể bạn sẽ phải tăng **UV2 Padding**.

**Lightmap Size Hint** biểu thị kích thước mà một mesh chiếm trên texture lightmap, kích thước này thay đổi tùy thuộc vào các thuộc tính kích thước của mesh và giá trị **UV2 Padding**. Không nên tự thay đổi **Lightmap Size Hint**, vì mọi sửa đổi sẽ bị mất khi scene được tải lại.

Tạo UV2 cho các node CSG
~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.4, bạn có thể
:ref:`convert a CSG node and its children to a MeshInstance3D <doc_csg_tools_converting_to_mesh_instance_3d>`.
Bạn có thể dùng cách này để bake lightmap trên một node CSG bằng cách thực hiện các bước sau:

- Chọn node CSG gốc và chọn **CSG > Bake Mesh Instance** ở phía trên viewport của trình chỉnh sửa 3D. - Ẩn node CSG gốc vừa được bake (node này không tự động bị ẩn). - Chọn node MeshInstance3D mới được tạo và chọn **Mesh > Unwrap UV2 for Lightmap/AO**. - Bake lightmap.

.. tip::

    Hãy nhớ giữ node CSG gốc trong scene tree để có thể thay đổi hình học sau này nếu cần. Để thay đổi hình học, hãy xóa node MeshInstance3D và hiển thị lại node CSG gốc.

Kiểm tra UV2
~~~~~~~~~~~~

Trong menu **Mesh** đã đề cập trước đó, bạn có thể trực quan hóa các tọa độ texture UV2. Nếu có vấn đề, hãy kiểm tra lại để bảo đảm các mesh có những tọa độ UV2 này:

.. image:: img/lightmap_gi_uvchannel.webp

Thiết lập scene
---------------

Trước khi thực hiện bất kỳ thao tác nào, cần thêm một node **LightmapGI** vào scene. Node này sẽ bật tính năng bake ánh sáng trên tất cả node (và sub-node) trong scene đó, kể cả các scene được instance.

.. image:: img/lightmap_gi_scene.webp

Một sub-scene có thể được instance nhiều lần, vì baker hỗ trợ việc này. Mỗi instance sẽ được gán một lightmap riêng. Để tránh các vấn đề do việc scale texel của lightmap không nhất quán, hãy bảo đảm tuân thủ quy tắc về scale mesh đã đề cập trước đó.

Thiết lập mesh
~~~~~~~~~~~~~~

Để một node **MeshInstance3D** tham gia vào quá trình bake, bake mode của node phải được đặt thành **Static**. Các mesh có bake mode được đặt thành **Disabled** hoặc **Dynamic** sẽ bị lightmapper bỏ qua.

.. image:: img/lightmap_gi_use.webp

Khi tự động tạo lightmap trong lúc nhập scene, tùy chọn này sẽ tự động được bật.

Thiết lập đèn
~~~~~~~~~~~~~

Theo mặc định, đèn chỉ được bake với ánh sáng gián tiếp. Điều này có nghĩa là shadowmapping và lighting vẫn là động và ảnh hưởng đến các đối tượng đang di chuyển, nhưng các lần ánh sáng dội lại từ đèn đó sẽ được bake.

Có thể tắt đèn (không bake) hoặc bake hoàn toàn (trực tiếp và gián tiếp). Bạn có thể điều khiển tùy chọn này từ menu **Bake Mode** của đèn:

.. image:: img/lightmap_gi_bake_mode.webp

Các mode gồm:

Disabled
~~~~~~~~

Đèn sẽ bị bỏ qua khi baking lightmap. Đây là mode nên dùng cho các hiệu ứng lighting động như vụ nổ và hiệu ứng vũ khí.

.. warning::

    Việc ẩn đèn không ảnh hưởng đến lightmap bake thu được. Điều này có nghĩa là bạn phải dùng bake mode Disabled thay vì ẩn Light node bằng cách tắt thuộc tính **Visible** của nó.

Dynamic
~~~~~~~

Đây là mode mặc định, là sự cân bằng giữa hiệu năng và khả năng hoạt động theo thời gian thực. Chỉ lighting gián tiếp được bake. Ánh sáng trực tiếp và bóng vẫn là thời gian thực, giống như khi không có LightmapGI.

Mode này cho phép thực hiện các thay đổi *nhẹ* đối với màu sắc, năng lượng và vị trí của đèn mà hình ảnh vẫn khá chính xác. Ví dụ: bạn có thể dùng mode này để tạo các ngọn đuốc tĩnh nhấp nháy có ánh sáng gián tiếp được bake.

Tùy thuộc vào giá trị của **Shadowmask Mode**, DirectionalLight3D vẫn có thể tạo ra bóng được bake ở xa. Điều này cho phép bóng ở khoảng cách gần được xử lý theo thời gian thực và hiển thị các đối tượng động, đồng thời cho phép các đối tượng tĩnh ở xa vẫn đổ bóng.

Static
~~~~~~

Cả lighting gián tiếp và trực tiếp đều sẽ được bake. Vì các bề mặt tĩnh có thể bỏ qua hoàn toàn việc tính toán lighting và shadow, mode này mang lại hiệu năng tốt nhất cùng với các bóng mượt không bao giờ mờ dần theo khoảng cách. Đèn thời gian thực sẽ không còn ảnh hưởng đến các bề mặt đã bake, nhưng vẫn ảnh hưởng đến các đối tượng động. Khi dùng bake mode **All** trên một đèn, các đối tượng động sẽ không đổ bóng theo thời gian thực lên các bề mặt đã bake, vì vậy bạn cần dùng một cách tiếp cận khác, chẳng hạn như blob shadow. Blob shadow có thể được triển khai bằng Decal node.

Không thể điều chỉnh đèn trong lúc gameplay. Việc di chuyển đèn hoặc thay đổi màu sắc (hoặc năng lượng) của đèn sẽ không có tác dụng lên các bề mặt tĩnh.

Vì bake mode có thể được điều chỉnh cho từng đèn, bạn có thể tạo các thiết lập lighting bake kết hợp. Một lựa chọn phổ biến là dùng DirectionalLight theo thời gian thực với bake mode được đặt thành **Dynamic**, đồng thời dùng bake mode **Static** cho OmniLight và SpotLight. Cách này mang lại hiệu năng tốt mà vẫn cho phép các đối tượng động đổ bóng theo thời gian thực trong các khu vực ngoài trời.

Đèn được bake hoàn toàn cũng có thể sử dụng các thuộc tính **Size** (omni/spot) hoặc **Angular Distance** (directional) của light node. Điều này cho phép tạo bóng có vùng nửa tối (penumbra) chân thực, tăng kích thước khi khoảng cách giữa vật thể đổ bóng và bóng tăng lên. Cách này cũng có chi phí hiệu năng thấp hơn so với bóng PCSS theo thời gian thực, vì chỉ các đối tượng động mới được render bóng theo thời gian thực.

.. image:: img/lightmap_gi_omnilight_size.png

Baking
------

Để bắt đầu quá trình bake, hãy nhấp vào nút **Bake Lightmaps** ở đầu viewport của 3D editor khi chọn LightmapGI node:

.. image:: img/lightmap_gi_bake.webp

Quá trình này có thể mất từ vài giây đến vài phút (hoặc vài giờ), tùy thuộc vào kích thước scene, phương thức bake và chất lượng được chọn.

.. warning::

    Baking lightmap là một quá trình có thể yêu cầu rất nhiều video memory, đặc biệt nếu texture thu được có kích thước lớn. Do các giới hạn nội bộ, engine cũng có thể bị crash nếu kích thước texture được tạo quá lớn (ngay cả trên các hệ thống có nhiều video memory).

    Để tránh crash, hãy đảm bảo kích thước texel của lightmap trong Import dock được đặt đủ lớn.

Tinh chỉnh
~~~~~~~~~~

- **Quality:** Có bốn mode bake quality: Low, Medium, High và Ultra. Chất lượng cao hơn sẽ mất nhiều thời gian hơn, nhưng tạo ra lightmap đẹp hơn với ít noise hơn. Khác biệt này đặc biệt dễ nhận thấy với các vật liệu emissive hoặc những khu vực nhận rất ít hoặc không nhận lighting trực tiếp. Mỗi mode bake quality có thể được điều chỉnh thêm trong Project Settings. - **Supersampling:** Tạo lightmap ở độ phân giải cao hơn rồi downsample. Điều này làm giảm noise và light leaking, đồng thời tạo ra bóng tốt hơn với các chi tiết có quy mô nhỏ. Tuy nhiên, việc sử dụng tùy chọn này sẽ làm tăng thời gian bake và mức sử dụng bộ nhớ trong quá trình baking lightmap. **Supersampling Factor** thay đổi kích thước mà lightmap được render trước khi downsample. - **Bounces:** Số lần dội được dùng cho lighting gián tiếp. Giá trị mặc định (``3``) là sự cân bằng tốt giữa thời gian bake và chất lượng. Giá trị cao hơn sẽ khiến ánh sáng dội qua lại nhiều lần hơn trước khi dừng, làm cho lighting gián tiếp trông mượt hơn (nhưng cũng có thể sáng hơn, tùy thuộc vào vật liệu và hình học). - **Bounce Indirect Energy:** Hệ số nhân toàn cục được dùng khi baking năng lượng gián tiếp của đèn. Hệ số này nhân với giá trị **Indirect Energy** riêng của từng đèn. Các giá trị khác ``1.0`` không chính xác về mặt vật lý, nhưng có thể được dùng cho hiệu ứng nghệ thuật. - **Directional:** Nếu được bật, lưu thông tin directional cho lightmap. Điều này cải thiện diện mạo của các vật liệu có normal map trên các bề mặt đã bake, đặc biệt với đèn được bake hoàn toàn (vì chúng cũng có ánh sáng trực tiếp được bake). Nhược điểm là directional lightmap tốn nhiều chi phí render hơn một chút. Chúng cũng cần nhiều thời gian bake hơn và tạo ra kích thước file lớn hơn. - **Shadowmask Mode:** Nếu được đặt thành mode khác **None**, DirectionalLight3D đầu tiên trong scene có mode global illumination **Dynamic** sẽ có bóng tĩnh được bake vào một texture riêng gọi là *shadowmask*. Có thể dùng tùy chọn này để cho phép các đối tượng tĩnh ở xa đổ bóng lên các đối tượng tĩnh khác bất kể khoảng cách đến camera. Xem :ref:`section on shadowmasking <doc_using_lightmap_gi_shadowmask>` để biết thêm chi tiết. - **Interior:** Nếu được bật, lighting môi trường sẽ không được lấy nguồn. Dùng tùy chọn này cho các scene hoàn toàn trong nhà để tránh light leak. - **Use Texture for Bounces:** Nếu được bật, một texture chứa thông tin lighting sẽ được tạo để tăng tốc quá trình tạo lighting gián tiếp, đổi lại là một phần độ chính xác. Hình học có thể xuất hiện thêm các artifact light leak khi dùng lightmap hoặc UV có độ phân giải thấp làm kéo giãn lightmap đáng kể trên các bề mặt. Nếu không chắc chắn, hãy để tùy chọn này được bật. - **Use Denoiser:** Nếu được bật, sử dụng thuật toán khử noise để làm cho lightmap ít noise hơn đáng kể. Tùy chọn này làm tăng thời gian bake và đôi khi có thể tạo ra artifact, nhưng kết quả thường rất đáng giá. Xem
  :ref:`doc_using_lightmap_gi_denoising` for more information.
- **Denoiser Strength:** Mức độ của bước khử noise được áp dụng cho các lightmap được tạo. Giá trị cao hơn sẽ loại bỏ noise hiệu quả hơn, nhưng có thể làm giảm chi tiết bóng đối với bóng tĩnh. Chỉ có tác dụng nếu tính năng khử noise được bật và phương thức khử noise là :abbr:`JNLM (Non-Local Means with Joint Filtering)` (:abbr:`OIDN (Open Image Denoise)` không có thiết lập denoiser strength). - **Bias:** Giá trị offset được dùng cho bóng trong các đơn vị 3D. Nhìn chung, bạn không cần thay đổi giá trị này, trừ khi gặp vấn đề với light bleeding hoặc các đốm tối trong lightmap sau khi bake. Thiết lập này không ảnh hưởng đến bóng theo thời gian thực được đổ lên các bề mặt đã bake (đối với đèn có bake mode **Dynamic**). - **Max Texture Size:** Kích thước texture tối đa cho texture atlas được tạo. Giá trị cao hơn sẽ tạo ra ít lát hơn, nhưng có thể không hoạt động trên mọi phần cứng do giới hạn phần cứng về kích thước texture. Nếu không chắc chắn, hãy giữ giá trị mặc định là ``16384``. - **Environment > Mode:** Điều khiển cách lấy nguồn lighting môi trường khi baking lightmap. Giá trị mặc định **Scene** phù hợp với các level có phần bên ngoài hiển thị được. Đối với scene hoàn toàn trong nhà, đặt thành **Disabled** để tránh light leak và tăng tốc quá trình bake. Bạn cũng có thể đặt thành **Custom Sky** hoặc **Custom Color** để sử dụng lighting môi trường khác với sky môi trường thực tế của scene. - **Gen Probes > Subdiv:** Xem :ref:`doc_using_lightmap_gi_dynamic_objects`. - **Data > Light Data:** Xem :ref:`doc_using_lightmap_gi_data`.

.. _doc_using_lightmap_gi_shadowmask:

Sử dụng shadowmask cho bóng directional ở xa
--------------------------------------------

Khi sử dụng DirectionalLight3D, khoảng cách tối đa mà nó có thể vẽ bóng theo thời gian thực bị giới hạn bởi thuộc tính **Shadow Max Distance**. Đây có thể là vấn đề trong các scene lớn, vì các đối tượng ở xa sẽ không có bóng từ DirectionalLight3D. Mặc dù có thể giải quyết vấn đề này bằng cách dùng mode global illumination **Static** trên DirectionalLight3D, cách này có một số nhược điểm:

- Vì cả ánh sáng trực tiếp và gián tiếp đều được bake, không có cách nào để các đối tượng động đổ bóng lên các bề mặt tĩnh theo cách chân thực. Godot bỏ qua hoàn toàn việc lấy mẫu bóng trong trường hợp này để tránh artifact "double lighting". - Bóng tĩnh ở khoảng cách gần thiếu chi tiết, vì chúng chỉ dựa vào texture lightmap chứ không dựa vào các cascade bóng theo thời gian thực.

Chúng ta có thể tránh các nhược điểm này mà vẫn hưởng lợi từ bóng ở xa bằng cách sử dụng *shadowmasking*. Mặc dù các đối tượng động sẽ không nhận bóng từ shadowmask, cách này vẫn cải thiện đáng kể hình ảnh vì hầu hết scene chủ yếu bao gồm các đối tượng tĩnh.

Vì chỉ riêng texture lightmap không chứa thông tin bóng, chúng ta có thể bake thông tin bóng này vào một texture riêng gọi là *shadowmask*.

Shadowmasking chỉ ảnh hưởng đến DirectionalLight3D đầu tiên trong scene (được xác định theo thứ tự cây) có chế độ global illumination **Dynamic**. Không thể sử dụng shadowmasking với chế độ global illumination **Static**, vì chế độ này hoàn toàn bỏ qua việc lấy mẫu bóng trên các vật thể tĩnh. Điều này là do chế độ global illumination Static bake cả ánh sáng trực tiếp lẫn gián tiếp.

Có ba chế độ shadowmasking:

- **None (mặc định):** Không bake texture shadowmask. Bóng định hướng sẽ không hiển thị bên ngoài phạm vi được chỉ định bởi thuộc tính **Shadow Max Distance** của DirectionalLight3D. - **Replace:** Bake texture shadowmask và sử dụng texture này để vẽ bóng định hướng khi nằm ngoài phạm vi được chỉ định bởi thuộc tính **Shadow Max Distance** của DirectionalLight3D. Bóng trong phạm vi này vẫn hoàn toàn theo thời gian thực. Tùy chọn này nhìn chung phù hợp nhất với hầu hết scene, vì có thể xử lý tốt các vật thể tĩnh có chuyển động nhỏ (ví dụ: bóng của tán lá). - **Overlay:** Bake texture shadowmask và sử dụng texture này để vẽ bóng định hướng bất kể khoảng cách đến camera. Bóng trong phạm vi thuộc tính **Shadow Max Distance** của DirectionalLight3D sẽ được phủ bằng bóng theo thời gian thực. Điều này có thể làm cho quá trình chuyển tiếp giữa bóng theo thời gian thực và bóng đã bake bớt đột ngột, nhưng phải đánh đổi bằng hiệu ứng "nhòe" xuất hiện trên bóng của vật thể tĩnh, tùy thuộc vào mật độ texel của lightmap. Ngoài ra, chế độ này không xử lý tốt bằng các vật thể tĩnh có chuyển động nhỏ (chẳng hạn như tán lá), vì bóng đã bake không thể được animate theo thời gian. Tuy vậy, đối với các scene mà camera di chuyển nhanh, đây có thể là lựa chọn tốt hơn **Replace**.

Dưới đây là so sánh trực quan giữa các chế độ shadowmask với một scene trong đó **Shadow Max Distance** được đặt rất thấp để phục vụ mục đích so sánh. Các hộp màu xanh là vật thể động, còn phần còn lại của scene là một vật thể tĩnh. Scene chỉ có một DirectionalLight3D duy nhất với chế độ global illumination Dynamic:

.. figure:: img/lightmap_gi_shadowmask.webp
   :align: center
   :alt: Comparison between shadowmask modes

   Comparison between shadowmask modes

.. note::

    Có thể chuyển đổi giữa các chế độ shadowmask **Replace** và **Overlay** mà không cần bake lại lightmap.

Cân bằng thời gian bake và chất lượng
-------------------------------------

Vì quá trình bake chất lượng cao có thể mất rất nhiều thời gian (lên đến hàng chục phút đối với các scene lớn và phức tạp), bạn nên sử dụng các thiết lập chất lượng thấp hơn lúc đầu. Sau đó, khi đã chắc chắn về thiết lập ánh sáng của scene, hãy tăng các thiết lập chất lượng và thực hiện một lần bake "cuối cùng" trước khi export project.

Giảm độ phân giải lightmap bằng cách tăng **Lightmap Texel Size** trên các scene 3D đã import cũng sẽ giúp tăng tốc đáng kể quá trình bake. Tuy nhiên, bạn sẽ phải reimport tất cả scene 3D sử dụng lightmap trước khi có thể bake lại lightmap.

.. _doc_using_lightmap_gi_denoising:

Khử nhiễu
---------

Vì quá trình bake lightmap dựa trên raytracing, lightmap đã bake "thô" sẽ luôn có nhiễu nhìn thấy được. Nhiễu đặc biệt dễ thấy ở những khu vực khó tiếp cận bởi ánh sáng phản xạ, chẳng hạn như các khu vực trong nhà có những khe hở nhỏ nơi ánh sáng mặt trời có thể chiếu vào. Có thể giảm nhiễu bằng cách tăng chất lượng bake, nhưng điều này sẽ làm tăng đáng kể thời gian bake.

.. figure:: img/lightmap_gi_denoiser_comparison.webp
   :align: center
   :alt: Comparison between denoising disabled and enabled

   Comparison between denoising disabled and enabled (with the default JNLM denoiser).

Để khắc phục nhiễu mà không làm thời gian bake tăng quá nhiều, có thể sử dụng denoiser. Denoiser là một thuật toán chạy trên lightmap đã bake cuối cùng, phát hiện các mẫu nhiễu và làm mềm chúng, đồng thời cố gắng bảo toàn chi tiết tốt nhất có thể. Godot cung cấp hai thuật toán khử nhiễu:

JNLM (Non-Local Means with Joint Filtering)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

JNLM là phương pháp khử nhiễu mặc định và được tích hợp trong Godot. Phương pháp này sử dụng một thuật toán khử nhiễu đơn giản nhưng hiệu quả có tên là *non-local means*. JNLM chạy trên GPU bằng compute shader và tương thích với mọi GPU có thể chạy các renderer dựa trên RenderingDevice của Godot 4. Không cần thiết lập bổ sung.

Có thể điều chỉnh khả năng khử nhiễu của JNLM bằng thuộc tính **Denoiser Strength**, thuộc tính này hiển thị khi **Use Denoiser** được bật. Giá trị cao hơn có thể loại bỏ nhiễu hiệu quả hơn, nhưng phải đánh đổi bằng việc làm giảm chi tiết bóng của các bóng tĩnh.

.. figure:: img/lightmap_gi_denoiser_jnlm_strength.webp
   :align: center
   :alt: Comparison between JNLM denoiser strength values

   Comparison between JNLM denoiser strength values. Higher values can reduce detail.

OIDN (Open Image Denoise)
~~~~~~~~~~~~~~~~~~~~~~~~~

Khác với JNLM, OIDN sử dụng phương pháp machine learning để khử nhiễu lightmap. OIDN có một model được huấn luyện riêng để loại bỏ nhiễu khỏi lightmap đồng thời bảo toàn nhiều chi tiết bóng hơn trong hầu hết scene so với JNLM.

OIDN có thể chạy trên GPU nếu đã cấu hình hardware acceleration. Với GPU hiện đại, cao cấp, cách này có thể nhanh hơn hơn 50 lần so với khử nhiễu dựa trên CPU:

- Trên GPU AMD, phải cài đặt và cấu hình HIP. - Trên GPU NVIDIA, phải cài đặt và cấu hình CUDA. Trình cài đặt NVIDIA có thể tự động thực hiện việc này, nhưng trên Linux, các thư viện CUDA có thể không được cài đặt mặc định. Hãy kiểm tra lại để bảo đảm các package CUDA từ bản phân phối Linux của bạn đã được cài đặt. - Trên GPU Intel, phải cài đặt và cấu hình SYCL.

Nếu hardware acceleration không khả dụng, OIDN sẽ chuyển sang khử nhiễu đa luồng dựa trên CPU. Để xác nhận khử nhiễu dựa trên GPU có hoạt động hay không, hãy sử dụng công cụ theo dõi mức sử dụng GPU trong khi bake lightmap và xem phần trăm mức sử dụng GPU cũng như mức sử dụng VRAM trong khi bước khử nhiễu đang được hiển thị trong Godot editor. Công cụ dòng lệnh ``nvidia-smi`` có thể hữu ích cho việc này.

OIDN không được tích hợp trong Godot do dung lượng tải xuống tương đối lớn. Bạn có thể tải các package binary OIDN đã biên dịch sẵn từ `website <https://www.openimagedenoise.org/downloads.html>`__. Giải nén package vào một vị trí trên PC, sau đó chỉ định đường dẫn đến executable ``oidnDenoise`` trong Editor Settings (**FileSystem > Tools > OIDN > OIDN Denoise Path**). Executable này nằm trong thư mục ``bin`` của package binary mà bạn đã giải nén.

Sau khi chỉ định đường dẫn đến executable khử nhiễu OIDN, hãy thay đổi phương pháp khử nhiễu trong project settings bằng cách đặt **Rendering > Lightmapping > Denoiser** thành **OIDN**. Thay đổi này sẽ ảnh hưởng đến tất cả lần bake lightmap của project này sau khi thiết lập được thay đổi.

.. note::

    Phương pháp khử nhiễu được cấu hình trong project settings thay vì editor settings. Cách này bảo đảm các thành viên khác nhau trong team cùng làm việc trên một project sẽ sử dụng cùng một phương pháp khử nhiễu để có kết quả nhất quán.

.. figure:: img/lightmap_gi_denoiser_jnlm_vs_oidn.webp
   :align: center
   :alt: Comparison between JNLM and OIDN denoisers

   Comparison between JNLM and OIDN denoisers.
   Notice how OIDN better preserves detail and reduces seams across different objects.

.. _doc_using_lightmap_gi_dynamic_objects:

Vật thể động
------------

Khác với VoxelGI và SDFGI, các vật thể động nhận ánh sáng gián tiếp theo cách khác với các vật thể tĩnh. Điều này là do lightmapping chỉ được thực hiện trên các vật thể tĩnh.

Để hiển thị ánh sáng gián tiếp trên các vật thể động, hệ thống probe 3D được sử dụng, với các light probe được phân bố khắp scene. Khi bake lightmap, lightmapper sẽ tính toán lượng ánh sáng *gián tiếp* mà probe nhận được. Ánh sáng trực tiếp không được lưu trong light probe, ngay cả đối với những light có bake mode được đặt thành **Static** (vì các vật thể động vẫn tiếp tục được chiếu sáng theo thời gian thực).

Có 2 cách để thêm light probe vào scene:

- **Automatic:** Đặt **Gen Probes > Subdiv** thành một giá trị khác **Disabled**, sau đó bake lightmap. Giá trị mặc định là ``8``, nhưng bạn có thể chọn giá trị lớn hơn để cải thiện độ chính xác, đổi lại thời gian bake lâu hơn và kích thước file đầu ra lớn hơn. - **Manual:** Ngoài hoặc thay cho việc tự động tạo probe, bạn có thể thêm light probe thủ công bằng cách thêm các node :ref:`class_LightmapProbe` vào scene. Cách này có thể được sử dụng để cải thiện chi tiết ánh sáng ở những khu vực thường xuyên có vật thể động đi qua. Sau khi đặt các node LightmapProbe trong scene, bạn phải bake lại lightmap để chúng có hiệu lực.

.. note::

    Sau khi bake lightmap, bạn sẽ thấy các hình cầu màu trắng trong scene 3D, biểu thị cách ánh sáng đã bake sẽ ảnh hưởng đến các vật thể động. Các hình cầu này **không** xuất hiện trong project đang chạy.

    Nếu muốn ẩn các hình cầu này trong editor, hãy bật/tắt **View > Gizmos > LightmapGI** ở đầu 3D editor (biểu tượng "mắt nhắm" cho biết gizmo đang bị ẩn).

.. _doc_using_lightmap_gi_data:

Dữ liệu lightmap
----------------

Thuộc tính **Data > Light Data** trong node LightmapGI chứa dữ liệu lightmap sau khi bake. Texture được lưu vào ổ đĩa, nhưng thuộc tính này cũng chứa dữ liệu capture cho các vật thể động, có thể có dung lượng lớn. Nếu bạn đang sử dụng scene ở định dạng ``.tscn``, bạn nên lưu resource này vào một file binary ``.lmbake`` bên ngoài để tránh làm phình scene ``.tscn`` bằng dữ liệu binary được mã hóa ở dạng Base64.

.. tip::

    File EXR được tạo có thể được xem và thậm chí chỉnh sửa bằng image editor để thực hiện hậu kỳ nếu cần. Tuy nhiên, hãy nhớ rằng mọi thay đổi đối với file EXR sẽ bị mất khi bake lại lightmap.

Giảm artifact của LightmapGI
----------------------------

Nếu nhận thấy các node LightmapGI liên tục xuất hiện rồi biến mất khi camera di chuyển, nguyên nhân rất có thể là engine đang render quá nhiều instance LightmapGI cùng lúc. Godot bị giới hạn ở 8 node LightmapGI được render cùng lúc, nghĩa là tối đa 8 instance có thể nằm trong tầm nhìn của camera trước khi một số instance bắt đầu nhấp nháy.
