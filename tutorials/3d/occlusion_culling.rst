.. _doc_occlusion_culling:

Loại bỏ đối tượng bị che khuất
==============================

Trong một engine kết xuất 3D, **occlusion culling** là quá trình loại bỏ hình học bị ẩn.

Trong trang này, bạn sẽ tìm hiểu:

- Ưu điểm và hạn chế của occlusion culling.
- Cách thiết lập occlusion culling trong Godot.
- Khắc phục các vấn đề thường gặp với occlusion culling.

.. seealso::

    Bạn có thể xem occlusion culling hoạt động trong thực tế thông qua `Occlusion Culling and Mesh LOD demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/occlusion_culling_mesh_lod>`__.

Tại sao nên sử dụng occlusion culling
-------------------------------------

Trong cảnh ví dụ này với hàng trăm căn phòng xếp cạnh nhau, một đối tượng động (hình cầu màu đỏ) bị bức tường che khuất trong căn phòng được chiếu sáng (ở bên trái cửa):

.. figure:: img/occlusion_culling_scene_example.png
   :align: center
   :alt: Cảnh ví dụ với bố cục phù hợp cho occlusion culling

   Cảnh ví dụ với bố cục phù hợp cho occlusion culling

Khi tắt occlusion culling, tất cả các căn phòng phía sau căn phòng được chiếu sáng đều phải được kết xuất. Đối tượng động cũng phải được kết xuất:

.. figure:: img/occlusion_culling_disabled.png
   :align: center
   :alt: Cảnh ví dụ khi tắt occlusion culling (wireframe)

   Cảnh ví dụ khi **tắt** occlusion culling (wireframe)

Khi bật occlusion culling, chỉ những căn phòng thực sự nhìn thấy mới phải được kết xuất. Đối tượng động cũng bị bức tường che khuất, vì vậy không còn phải được kết xuất:

.. figure:: img/occlusion_culling_enabled.png
   :align: center
   :alt: Cảnh ví dụ khi bật occlusion culling (wireframe)

   Cảnh ví dụ khi **bật** occlusion culling (wireframe)

Vì engine phải thực hiện ít công việc hơn (ít vertex cần kết xuất hơn và ít draw call hơn), hiệu năng sẽ tăng miễn là cảnh có đủ cơ hội để thực hiện occlusion culling. Điều này có nghĩa là occlusion culling hiệu quả nhất trong các cảnh trong nhà, tốt nhất là có nhiều căn phòng nhỏ thay vì ít căn phòng lớn. Kết hợp tính năng này với :ref:`doc_mesh_lod` và :ref:`doc_visibility_ranges` để cải thiện thêm mức tăng hiệu năng.

.. note::

    Khi sử dụng renderer Forward+, engine đã thực hiện *depth prepass*. Quy trình này kết xuất một phiên bản chỉ có depth của cảnh trước khi kết xuất các material thực tế của cảnh. Việc này đảm bảo mỗi pixel opaque chỉ được shade một lần, giúp giảm đáng kể chi phí overdraw.

    Có thể quan sát lợi ích hiệu năng lớn nhất khi sử dụng renderer Mobile, vì renderer này không có depth prepass vì lý do hiệu năng. Do đó, occlusion culling sẽ chủ động giảm shading overdraw với renderer này.

    Tuy nhiên, ngay cả khi sử dụng depth prepass, occlusion culling vẫn mang lại lợi ích đáng kể trong các cảnh 3D phức tạp. Mặt khác, trong các cảnh có ít cơ hội để thực hiện occlusion culling, lợi ích của occlusion culling có thể không tương xứng với công sức thiết lập và mức sử dụng CPU tăng thêm.

Cách occlusion culling hoạt động trong Godot
--------------------------------------------

.. note::

    "occluder" là hình dạng chặn tầm nhìn, còn "occludee" là đối tượng bị che khuất.

Trong Godot, occlusion culling hoạt động bằng cách rasterize hình học occluder của cảnh vào một buffer độ phân giải thấp trên CPU. Việc này sử dụng thư viện raytracing bằng phần mềm `Embree <https://github.com/embree/embree>`__.

Sau đó, engine sử dụng buffer độ phân giải thấp này để kiểm tra
:abbr:`AABB (Axis-Aligned Bounding Box)` của occludee với các hình dạng occluder. :abbr:`AABB (Axis-Aligned Bounding Box)` của occludee phải bị hình dạng occluder *che khuất hoàn toàn* thì mới được loại bỏ.

Do đó, các đối tượng nhỏ có nhiều khả năng được loại bỏ hiệu quả hơn các đối tượng lớn. Các occluder lớn hơn (chẳng hạn như tường) cũng thường hiệu quả hơn nhiều so với các occluder nhỏ hơn (chẳng hạn như vật trang trí).

Thiết lập occlusion culling
---------------------------

Bước đầu tiên để sử dụng occlusion culling là bật cài đặt project **Rendering > Occlusion Culling > Use Occlusion Culling**. (Hãy đảm bảo bật nút chuyển **Advanced** trong hộp thoại Project Settings để có thể thấy cài đặt này.)

Cài đặt project này được áp dụng ngay lập tức, vì vậy bạn không cần khởi động lại editor.

Sau khi bật cài đặt project, bạn vẫn cần tạo một số occluder. Vì lý do hiệu năng, engine không tự động sử dụng toàn bộ hình học có thể nhìn thấy làm cơ sở cho occlusion culling. Thay vào đó, engine yêu cầu một biểu diễn đơn giản hóa của cảnh, trong đó chỉ các đối tượng tĩnh được bake.

Có hai cách để thiết lập occluder trong một cảnh:

.. _doc_occlusion_culling_baking:

Tự động bake occluder (khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Hiện tại, chỉ các node MeshInstance3D được xét đến trong quá trình bake *occluder*. Các node MultiMeshInstance3D, GPUParticles3D, CPUParticles3D và CSG **không** được xét đến khi bake occluder. Nếu muốn chúng được xử lý như occluder, bạn phải tự tạo các hình dạng occluder khớp gần đúng với hình học của chúng.

    Kể từ Godot 4.4, các node CSG có thể được xét đến trong quá trình bake nếu chúng được
    :ref:`chuyển đổi thành MeshInstance3D <doc_csg_tools_converting_to_mesh_instance_3d>` trước khi bake occluder.

    Hạn chế này không áp dụng cho *occludee*. Bất kỳ loại node nào kế thừa từ GeometryInstance3D đều có thể bị che khuất.

Sau khi bật cài đặt project occlusion culling được đề cập ở trên, hãy thêm một node OccluderInstance3D vào cảnh chứa level 3D của bạn.

Chọn node OccluderInstance3D, sau đó nhấp vào **Bake Occluders** ở đầu viewport của 3D editor. Sau khi bake, node OccluderInstance3D sẽ chứa một resource Occluder3D lưu trữ phiên bản đơn giản hóa của hình học level. Hình học occluder này xuất hiện dưới dạng các đường wireframe màu tím trong chế độ xem 3D (miễn là **View Gizmos** được bật trong menu **Perspective**). Hình học này sau đó được sử dụng để cung cấp occlusion culling cho cả occludee tĩnh và động.

Sau khi bake, bạn có thể nhận thấy các đối tượng động (chẳng hạn như người chơi, kẻ địch, v.v…) được đưa vào mesh đã bake. Để ngăn điều này, hãy đặt thuộc tính **Bake > Cull Mask** trên OccluderInstance3D để loại trừ một số visual layer khỏi quá trình bake.

Ví dụ, bạn có thể vô hiệu hóa layer 2 trên cull mask, sau đó cấu hình các node MeshInstance3D của những đối tượng động để nằm trên visual layer 2 (thay vì layer 1). Để thực hiện việc này, hãy chọn node MeshInstance3D tương ứng, rồi trong thuộc tính **VisualInstance3D > Layers**, bỏ chọn layer 1 rồi chọn layer
2. Sau khi cấu hình cả cull mask và các layer, hãy bake occluder lại bằng cách
làm theo quy trình trên.

Đặt occluder thủ công
~~~~~~~~~~~~~~~~~~~~~

Cách tiếp cận này phù hợp hơn với các trường hợp sử dụng chuyên biệt, chẳng hạn như tạo occlusion cho các thiết lập MultiMeshInstance3D hoặc các node CSG (do hạn chế đã đề cập ở trên).

Sau khi bật project setting về occlusion culling đã đề cập ở trên, hãy thêm một node OccluderInstance3D vào scene chứa level 3D của bạn. Chọn node OccluderInstance3D, rồi chọn loại occluder cần thêm trong thuộc tính **Occluder**:

- QuadOccluder3D (một mặt phẳng đơn)
- BoxOccluder3D (một khối hộp)
- SphereOccluder3D (một occluder hình cầu)
- PolygonOccluder3D (một đa giác 2D có số điểm tùy ý)

Ngoài ra còn có ArrayOccluder3D, có các điểm không thể chỉnh sửa trong editor nhưng có thể hữu ích cho việc sinh hình theo thủ tục từ một script.

.. _doc_occlusion_culling_preview:

Xem trước occlusion culling
---------------------------

Bạn có thể bật chế độ debug draw để xem trước những gì occlusion culling thực sự "nhìn thấy". Ở góc trên bên trái của viewport trình chỉnh sửa 3D, hãy nhấp vào nút **Perspective** (hoặc **Orthogonal** tùy thuộc vào chế độ camera hiện tại), rồi chọn **Display Advanced… > Occlusion Culling Buffer**. Thao tác này sẽ hiển thị buffer có độ phân giải thấp được engine sử dụng cho occlusion culling.

Trong cùng menu đó, bạn cũng có thể bật **View Information** và **View Frame Time** để xem số lượng draw call và primitive được render (vertex + index) ở góc dưới bên phải, cùng với số frame mỗi giây được render ở góc trên bên phải.

Nếu bật hoặc tắt occlusion culling trong project settings khi thông tin này đang được hiển thị, bạn có thể thấy occlusion culling cải thiện hiệu năng trong scene của mình đến mức nào. Lưu ý rằng lợi ích về hiệu năng phụ thuộc rất nhiều vào góc nhìn của camera trong trình chỉnh sửa 3D, vì occlusion culling chỉ hiệu quả khi có occluder ở phía trước camera.

Để bật hoặc tắt occlusion culling trong runtime, hãy đặt ``use_occlusion_culling`` trên root viewport như sau:

.. tabs::
 .. code-tab:: gdscript

    get_tree().root.use_occlusion_culling = true

 .. code-tab:: csharp

    GetTree().Root.UseOcclusionCulling = true;


Bật hoặc tắt occlusion culling trong runtime hữu ích để so sánh hiệu năng khi project đang chạy.

Các cân nhắc về hiệu năng
-------------------------

Thiết kế level để tận dụng occlusion culling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Đây là hướng dẫn quan trọng nhất.** Một thiết kế level tốt không chỉ xoay quanh yêu cầu của gameplay; level cũng nên được xây dựng có tính đến occlusion.

Đối với môi trường trong nhà, hãy thêm các bức tường đục để "ngắt" tầm nhìn ở những khoảng cách đều đặn và đảm bảo không thể nhìn thấy quá nhiều phần của scene cùng một lúc.

Đối với các scene mở rộng lớn, hãy sử dụng cấu trúc giống kim tự tháp cho độ cao của địa hình khi có thể. So với mọi hình dạng địa hình khác, cách này tạo ra nhiều cơ hội culling nhất.

Tránh di chuyển các node OccluderInstance3D trong gameplay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Điều này bao gồm cả việc di chuyển các node cha của node OccluderInstance3D, vì việc đó sẽ khiến bản thân các node di chuyển trong không gian toàn cục, từ đó yêu cầu xây dựng lại :abbr:`BVH (Bounding Volume Hierarchy)`.

Việc bật hoặc tắt visibility của một OccluderInstance3D (hoặc visibility của một trong các node cha của nó) không tốn kém bằng, vì quá trình cập nhật chỉ cần diễn ra một lần (thay vì liên tục).

Ví dụ, nếu bạn có một cánh cửa trượt hoặc xoay, bạn có thể để node OccluderInstance3D không phải là node con của chính cánh cửa đó (để occluder không bao giờ di chuyển), nhưng có thể ẩn visibility của OccluderInstance3D khi cánh cửa bắt đầu mở. Sau đó, bạn có thể hiện lại OccluderInstance3D khi cánh cửa đóng hoàn toàn.

Nếu bắt buộc phải di chuyển một node OccluderInstance3D trong gameplay, hãy sử dụng một hình dạng Occluder3D nguyên thủy cho nó thay vì một hình dạng phức tạp được bake.

Sử dụng hình dạng occluder đơn giản nhất có thể
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu nhận thấy hiệu năng thấp hoặc hiện tượng giật trong các scene 3D phức tạp, có thể CPU đang quá tải do render các occluder có nhiều chi tiết. Hãy chọn node OccluderInstance3D, tăng giá trị thuộc tính **Bake > Simplification**, rồi bake occluder lại.

Hãy nhớ giữ giá trị simplification ở mức hợp lý. Các giá trị quá cao so với hình học của level có thể khiến occlusion culling diễn ra không chính xác, như trong
:ref:`doc_occlusion_culling_troubleshooting_false_negative`.

Nếu cách này vẫn chưa giúp giảm mức sử dụng CPU đủ thấp, bạn có thể thử điều chỉnh project setting **Rendering > Occlusion Culling > BVH Build Quality** và/hoặc giảm **Rendering > Occlusion Culling > Occlusion Rays Per Thread**. Bạn cần bật tùy chọn **Advanced** trong hộp thoại Project Settings để thấy các setting này.

Khắc phục sự cố
---------------

Occludee của tôi không bị culling khi đáng lẽ phải bị culling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Về phía occluder:**

Trước tiên, hãy kiểm tra lại để đảm bảo thuộc tính **Bake > Cull Mask** trong OccluderInstance3D được đặt cho phép bake các mesh bạn muốn. Visibility layer của các node MeshInstance3D phải nằm trong cull mask để mesh được đưa vào quá trình bake.

Ngoài ra, lưu ý rằng quá trình bake occluder chỉ tính đến các mesh có vật liệu *opaque*. Các bề mặt có vật liệu *transparent* sẽ **not** được đưa vào quá trình bake, ngay cả khi texture áp dụng trên chúng hoàn toàn opaque.

Cuối cùng, hãy nhớ rằng các node MultiMeshInstance3D, GPUParticles3D, CPUParticles3D và CSG **not** được tính đến khi bake occluder. Để khắc phục, bạn có thể tự thêm các node OccluderInstance3D cho chúng.

**Về phía occludee:**

Đảm bảo **Extra Cull Margin** được đặt ở mức thấp nhất có thể (thông thường nên là ``0.0``), đồng thời **Ignore Occlusion Culling** đã được tắt trong phần GeometryInstance3D của đối tượng.

Ngoài ra, hãy kiểm tra kích thước của AABB (được biểu thị bằng một hình hộp màu cam khi chọn node). Để đối tượng bị che khuất bị ẩn, bounding box căn chỉnh theo trục này phải bị các hình dạng occluder che khuất *hoàn toàn*.

.. _doc_occlusion_culling_troubleshooting_false_negative:

Đối tượng bị che khuất của tôi bị loại bỏ khi không nên bị loại bỏ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nguyên nhân có khả năng nhất là các đối tượng được đưa vào quá trình bake occluder đã bị di chuyển sau khi bake. Chẳng hạn, điều này có thể xảy ra khi di chuyển hình học của level hoặc sắp xếp lại bố cục của nó. Để khắc phục, hãy chọn node OccluderInstance3D và bake occluder lại.

Điều này cũng có thể xảy ra vì các đối tượng động đã được đưa vào quá trình bake, dù không nên được đưa vào. Hãy sử dụng
:ref:`occlusion culling debug draw mode <doc_occlusion_culling_preview>` để tìm các hình dạng occluder không nên xuất hiện, sau đó
:ref:`điều chỉnh bake cull mask cho phù hợp <doc_occlusion_culling_baking>`.

Nguyên nhân có thể xảy ra cuối cùng là quá trình đơn giản hóa mesh quá mạnh trong khi bake occluder. Hãy chọn node OccluderInstance3D, giảm thuộc tính **Bake > Simplification**, sau đó bake occluder lại.

Trong trường hợp cuối cùng, bạn có thể bật thuộc tính **Ignore Occlusion Culling** trên đối tượng bị che khuất. Điều này sẽ làm mất các cải thiện hiệu năng của occlusion culling đối với đối tượng đó, nhưng hợp lý khi thực hiện với những đối tượng sẽ không bao giờ bị loại bỏ (chẳng hạn như model góc nhìn thứ nhất).
