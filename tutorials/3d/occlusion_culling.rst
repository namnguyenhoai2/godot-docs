.. _doc_occlusion_culling:

Occlusion culling
=================

Trong một engine render 3D, **occlusion culling** là quá trình loại bỏ hình học bị che khuất.

Trên trang này, bạn sẽ tìm hiểu:

- Các ưu điểm và hạn chế của occlusion culling. - Cách thiết lập occlusion culling trong Godot. - Cách khắc phục các vấn đề thường gặp với occlusion culling.

.. seealso::

    Bạn có thể xem occlusion culling hoạt động như thế nào trong thực tế bằng cách sử dụng project demo `Occlusion Culling and Mesh LOD <https://github.com/godotengine/godot-demo-projects/tree/master/3d/occlusion_culling_mesh_lod>`__.

Tại sao nên sử dụng occlusion culling
-------------------------------------

Trong scene ví dụ này với hàng trăm căn phòng xếp cạnh nhau, một object động (hình cầu màu đỏ) bị bức tường trong căn phòng được chiếu sáng che khuất (ở bên trái cửa):

.. figure:: img/occlusion_culling_scene_example.png
   :align: center
   :alt: Example scene with an occlusion culling-friendly layout

   Example scene with an occlusion culling-friendly layout

Khi tắt occlusion culling, tất cả các căn phòng phía sau căn phòng được chiếu sáng đều phải được render. Object động cũng phải được render:

.. figure:: img/occlusion_culling_disabled.png
   :align: center
   :alt: Example scene with occlusion culling disabled (wireframe)

   Example scene with occlusion culling **disabled** (wireframe)

Khi bật occlusion culling, chỉ những căn phòng thực sự nhìn thấy mới phải được render. Object động cũng bị bức tường che khuất và do đó không còn phải được render:

.. figure:: img/occlusion_culling_enabled.png
   :align: center
   :alt: Example scene with occlusion culling enabled (wireframe)

   Example scene with occlusion culling **enabled** (wireframe)

Vì engine cần thực hiện ít công việc hơn (ít vertex cần render hơn và ít draw call hơn), hiệu năng sẽ tăng miễn là scene có đủ cơ hội để thực hiện occlusion culling. Điều này có nghĩa là occlusion culling hiệu quả nhất trong các scene trong nhà, tốt nhất là có nhiều căn phòng nhỏ thay vì ít căn phòng lớn. Kết hợp tính năng này với :ref:`doc_mesh_lod` và :ref:`doc_visibility_ranges` để cải thiện hơn nữa mức tăng hiệu năng.

.. note::

    Khi sử dụng renderer Forward+, engine đã thực hiện *depth prepass*. Quá trình này bao gồm việc render một phiên bản chỉ có depth của scene trước khi render các material thực tế của scene. Tính năng này được dùng để đảm bảo mỗi pixel opaque chỉ được shade một lần, giúp giảm đáng kể chi phí overdraw.

    Lợi ích hiệu năng lớn nhất có thể thấy khi sử dụng renderer Mobile, vì renderer này không có depth prepass do lý do hiệu năng. Do đó, occlusion culling sẽ chủ động giảm shading overdraw với renderer này.

    Tuy vậy, ngay cả khi sử dụng depth prepass, occlusion culling vẫn mang lại lợi ích đáng kể trong các scene 3D phức tạp. Tuy nhiên, trong các scene có ít cơ hội để thực hiện occlusion culling, lợi ích này có thể không đáng với công sức thiết lập và mức sử dụng CPU tăng thêm.

Cách occlusion culling hoạt động trong Godot
--------------------------------------------

.. note::

    "occluder" là hình dạng chắn tầm nhìn, còn "occludee" là object bị che khuất.

Trong Godot, occlusion culling hoạt động bằng cách rasterize hình học occluder của scene vào một buffer độ phân giải thấp trên CPU. Việc này được thực hiện bằng thư viện raytracing bằng phần mềm `Embree <https://github.com/embree/embree>`__.

Sau đó, engine sử dụng buffer độ phân giải thấp này để kiểm tra
:abbr:`AABB (Axis-Aligned Bounding Box)` against the occluder shapes.
:abbr:`AABB (Axis-Aligned Bounding Box)` của occludee phải bị hình dạng occluder *che khuất hoàn toàn* thì mới bị loại bỏ.

Do đó, các object nhỏ có khả năng được loại bỏ hiệu quả hơn các object lớn. Các occluder lớn hơn (chẳng hạn như tường) cũng thường hiệu quả hơn nhiều so với các occluder nhỏ hơn (chẳng hạn như các prop trang trí).

Thiết lập occlusion culling
---------------------------

Bước đầu tiên để sử dụng occlusion culling là bật project setting **Rendering > Occlusion Culling > Use Occlusion Culling**. (Hãy đảm bảo toggle **Advanced** được bật trong hộp thoại Project Settings để có thể nhìn thấy mục này.)

Project setting này được áp dụng ngay lập tức, vì vậy bạn không cần khởi động lại editor.

Sau khi bật project setting, bạn vẫn cần tạo một số occluder. Vì lý do hiệu năng, engine không tự động sử dụng toàn bộ hình học có thể nhìn thấy làm cơ sở cho occlusion culling. Thay vào đó, engine yêu cầu một biểu diễn đơn giản hóa của scene, trong đó chỉ các object tĩnh được bake.

Có hai cách để thiết lập occluder trong một scene:

.. _doc_occlusion_culling_baking:

Bake occluder tự động (khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Hiện tại, chỉ các node MeshInstance3D được tính đến trong quá trình bake *occluder*. MultiMeshInstance3D, GPUParticles3D, CPUParticles3D và các node CSG **không** được tính đến khi bake occluder. Nếu muốn chúng được xử lý như occluder, bạn phải tự tạo các hình dạng occluder tương đối khớp với hình học của chúng.

    Kể từ Godot 4.4, các node CSG có thể được tính đến trong quá trình bake nếu chúng được
    :ref:`converted to a MeshInstance3D <doc_csg_tools_converting_to_mesh_instance_3d>`
    trước khi bake occluder.

    Hạn chế này không áp dụng cho *occludee*. Bất kỳ loại node nào kế thừa từ GeometryInstance3D đều có thể bị che khuất.

Sau khi bật project setting occlusion culling đã đề cập ở trên, hãy thêm một node OccluderInstance3D vào scene chứa level 3D của bạn.

Chọn node OccluderInstance3D, sau đó nhấp vào **Bake Occluders** ở phía trên viewport 3D editor. Sau khi bake, node OccluderInstance3D sẽ chứa một resource Occluder3D lưu trữ phiên bản đơn giản hóa của hình học level. Hình học occluder này xuất hiện dưới dạng các đường wireframe màu tím trong chế độ xem 3D (miễn là **View Gizmos** được bật trong menu **Perspective**). Hình học này sau đó được sử dụng để cung cấp occlusion culling cho cả occludee tĩnh và động.

Sau khi bake, bạn có thể nhận thấy các object động (chẳng hạn như player, enemy, v.v…) được đưa vào mesh đã bake. Để ngăn điều này, hãy đặt thuộc tính **Bake > Cull Mask** trên OccluderInstance3D để loại trừ một số visual layer khỏi quá trình bake.

Ví dụ, bạn có thể tắt layer 2 trong cull mask, sau đó cấu hình các node MeshInstance3D của object động để nằm trên visual layer 2 (thay vì layer 1). Để thực hiện việc này, hãy chọn node MeshInstance3D tương ứng, sau đó trong thuộc tính **VisualInstance3D > Layers**, bỏ chọn layer 1 rồi chọn layer 2. Sau khi cấu hình cả cull mask và layer, hãy bake lại occluder bằng cách thực hiện theo quy trình ở trên.

Đặt occluder thủ công
~~~~~~~~~~~~~~~~~~~~~

Cách tiếp cận này phù hợp hơn với các trường hợp sử dụng chuyên biệt, chẳng hạn như tạo occlusion cho các thiết lập MultiMeshInstance3D hoặc node CSG (do hạn chế đã đề cập ở trên).

Sau khi bật project setting occlusion culling đã đề cập ở trên, hãy thêm một node OccluderInstance3D vào scene chứa level 3D của bạn. Chọn node OccluderInstance3D, sau đó chọn loại occluder cần thêm trong thuộc tính **Occluder**:

- QuadOccluder3D (một mặt phẳng) - BoxOccluder3D (một hình hộp chữ nhật) - SphereOccluder3D (một occluder hình cầu) - PolygonOccluder3D (một polygon 2D có số lượng điểm tùy ý)

Ngoài ra còn có ArrayOccluder3D, các điểm của nó không thể được chỉnh sửa trong editor nhưng có thể hữu ích cho việc tạo sinh theo quy trình từ một script.

.. _doc_occlusion_culling_preview:

Xem trước occlusion culling
---------------------------

Bạn có thể bật chế độ debug draw để xem trước những gì occlusion culling thực sự đang "nhìn thấy". Ở góc trên bên trái của viewport 3D editor, hãy nhấp vào nút **Perspective** (hoặc **Orthogonal** tùy thuộc vào chế độ camera hiện tại), sau đó chọn **Display Advanced… > Occlusion Culling Buffer**. Thao tác này sẽ hiển thị buffer độ phân giải thấp được engine sử dụng cho occlusion culling.

Trong cùng menu đó, bạn cũng có thể bật **View Information** và **View Frame Time** để xem số lượng draw call và primitive được render (vertex + index) ở góc dưới bên phải, cùng với số frame mỗi giây được render ở góc trên bên phải.

Nếu bật hoặc tắt occlusion culling trong project settings khi thông tin này đang được hiển thị, bạn có thể thấy occlusion culling cải thiện hiệu năng trong scene của mình đến mức nào. Lưu ý rằng lợi ích hiệu năng phụ thuộc rất nhiều vào góc nhìn của camera 3D editor, vì occlusion culling chỉ hiệu quả nếu có occluder ở phía trước camera.

Để bật hoặc tắt occlusion culling trong runtime, hãy đặt ``use_occlusion_culling`` trên root viewport như sau:

.. tabs::
 .. code-tab:: gdscript

    get_tree().root.use_occlusion_culling = true

 .. code-tab:: csharp

    GetTree().Root.UseOcclusionCulling = true;


Bật hoặc tắt occlusion culling trong runtime rất hữu ích để so sánh hiệu năng trên một project đang chạy.

Các lưu ý về hiệu năng
----------------------

Thiết kế level để tận dụng occlusion culling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Đây là nguyên tắc quan trọng nhất.** Một thiết kế level tốt không chỉ phụ thuộc vào yêu cầu gameplay; level cũng nên được xây dựng có tính đến occlusion.

Đối với môi trường trong nhà, hãy thêm các bức tường opaque để "ngắt" đường nhìn ở các khoảng cách đều nhau và đảm bảo không thể nhìn thấy quá nhiều phần của scene cùng một lúc.

Đối với các scene mở rộng lớn, hãy sử dụng cấu trúc giống hình kim tự tháp cho độ cao của địa hình nếu có thể. Cách này mang lại nhiều cơ hội culling nhất so với bất kỳ hình dạng địa hình nào khác.

Tránh di chuyển các node OccluderInstance3D trong quá trình gameplay
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Điều này bao gồm cả việc di chuyển các parent của node OccluderInstance3D, vì việc này sẽ khiến bản thân các node di chuyển trong global space, từ đó yêu cầu phải xây dựng lại :abbr:`BVH (Bounding Volume Hierarchy)`.

Việc bật hoặc tắt visibility của OccluderInstance3D (hoặc visibility của một trong các parent của nó) không tốn nhiều chi phí như vậy, vì việc cập nhật chỉ cần diễn ra một lần (thay vì liên tục).

Ví dụ, nếu bạn có một cánh cửa trượt hoặc xoay, bạn có thể khiến node OccluderInstance3D không phải là child của chính cánh cửa đó (để occluder không bao giờ di chuyển), nhưng có thể ẩn visibility của OccluderInstance3D ngay khi cửa bắt đầu mở. Sau đó, bạn có thể hiển thị lại OccluderInstance3D khi cửa đóng hoàn toàn.

Nếu thực sự phải di chuyển một node OccluderInstance3D trong quá trình gameplay, hãy sử dụng một hình dạng Occluder3D dạng primitive thay vì một hình dạng phức tạp đã bake.

Sử dụng các hình dạng occluder đơn giản nhất có thể
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn nhận thấy hiệu năng thấp hoặc hiện tượng giật trong các cảnh 3D phức tạp, điều đó có thể có nghĩa là CPU đang bị quá tải do render các occluder chi tiết. Chọn node OccluderInstance3D, tăng thuộc tính **Bake > Simplification**, sau đó bake occluder lại.

Hãy nhớ giữ giá trị simplification ở mức hợp lý. Các giá trị quá cao so với hình học của level có thể khiến việc occlusion culling diễn ra không chính xác, như trong
:ref:`doc_occlusion_culling_troubleshooting_false_negative`.

Nếu cách này vẫn chưa giúp giảm mức sử dụng CPU đủ thấp, bạn có thể thử điều chỉnh thiết lập project **Rendering > Occlusion Culling > BVH Build Quality** và/hoặc giảm **Rendering > Occlusion Culling > Occlusion Rays Per Thread**. Bạn cần bật tùy chọn **Advanced** trong hộp thoại Project Settings để thấy các thiết lập đó.

Khắc phục sự cố
---------------

Occludee của tôi không bị culling khi đáng lẽ phải như vậy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Về phía occluder:**

Trước tiên, hãy kiểm tra lại để đảm bảo thuộc tính **Bake > Cull Mask** trong OccluderInstance3D được thiết lập cho phép bake các mesh bạn muốn. Visibility layer của các node MeshInstance3D phải nằm trong cull mask để mesh được đưa vào quá trình bake.

Cũng lưu ý rằng việc bake occluder chỉ tính đến các mesh có material *opaque*. Các bề mặt có material *transparent* sẽ **không** được đưa vào quá trình bake, ngay cả khi texture được áp dụng trên chúng hoàn toàn opaque.

Cuối cùng, hãy nhớ rằng MultiMeshInstance3D, GPUParticles3D, CPUParticles3D và các node CSG **không** được tính đến khi bake occluder. Để xử lý tạm thời, bạn có thể thêm các node OccluderInstance3D cho chúng theo cách thủ công.

**Về phía occludee:**

Đảm bảo **Extra Cull Margin** được đặt ở mức thấp nhất có thể (thông thường nên là ``0.0``), và **Ignore Occlusion Culling** được tắt trong phần GeometryInstance3D của object.

Ngoài ra, hãy kiểm tra kích thước của AABB (được biểu thị bằng một hộp màu cam khi chọn node). Axis-aligned bounding box này phải bị các shape của occluder *che khuất hoàn toàn* thì occludee mới bị ẩn.

.. _doc_occlusion_culling_troubleshooting_false_negative:

Occludee của tôi bị culling khi không đáng lẽ phải như vậy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nguyên nhân có khả năng nhất là các object được đưa vào quá trình bake occluder đã bị di chuyển sau khi bake occluder. Ví dụ, điều này có thể xảy ra khi di chuyển hình học của level hoặc sắp xếp lại bố cục của level. Để khắc phục, hãy chọn node OccluderInstance3D và bake occluder lại.

Điều này cũng có thể xảy ra vì các object động đã được đưa vào quá trình bake, dù chúng không nên được đưa vào. Hãy sử dụng
:ref:`occlusion culling debug draw mode <doc_occlusion_culling_preview>` to look
cho các shape của occluder không nên hiện diện, sau đó
:ref:`adjust the bake cull mask accordingly <doc_occlusion_culling_baking>`.

Nguyên nhân có thể xảy ra cuối cùng là việc simplification mesh quá mức trong quá trình bake occluder. Chọn node OccluderInstance3D, giảm thuộc tính **Bake > Simplification**, sau đó bake occluder lại.

Nếu không còn cách nào khác, bạn có thể bật thuộc tính **Ignore Occlusion Culling** trên occludee. Điều này sẽ loại bỏ các cải thiện hiệu năng do occlusion culling mang lại cho object đó, nhưng hợp lý khi thực hiện với các object sẽ không bao giờ bị culling (chẳng hạn như first-person view model).
