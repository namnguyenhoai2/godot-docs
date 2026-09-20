.. _doc_using_voxel_gi:

Sử dụng global illumination Voxel
=================================

VoxelGI là một dạng global illumination hoàn toàn theo thời gian thực, được thiết kế để sử dụng cho các cảnh 3D quy mô nhỏ/trung bình. VoxelGI khá ngốn GPU, vì vậy phù hợp nhất khi nhắm đến các card đồ họa chuyên dụng.

.. important::

    VoxelGI chỉ được hỗ trợ khi sử dụng Forward+ renderer, không được hỗ trợ bởi Mobile hoặc Compatibility renderer.

.. seealso::

    Không chắc VoxelGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: VoxelGI disabled.

   VoxelGI disabled.

.. figure:: img/gi_voxel_gi.webp
   :alt: VoxelGI enabled.

   VoxelGI enabled.

Thiết lập VoxelGI
-----------------

1. Hãy đảm bảo hình học level tĩnh của bạn được import với tùy chọn Light Baking đặt thành **Static** hoặc **Static Lightmaps** trong dock Import. Đối với các node MeshInstance3D được thêm thủ công, hãy đảm bảo thuộc tính **Global Illumination > Mode** được đặt thành **Static** trong inspector. 2. Tạo một node VoxelGI trong dock Scene tree. 3. Di chuyển node VoxelGI đến trung tâm khu vực bạn muốn nó bao phủ bằng cách kéo gizmo thao tác trong viewport 3D. Sau đó điều chỉnh extents của VoxelGI bằng cách kéo các điểm màu đỏ trong viewport 3D (hoặc nhập các giá trị trong inspector). Hãy đảm bảo extents của VoxelGI không lớn hơn mức cần thiết, nếu không chất lượng sẽ bị ảnh hưởng. 4. Chọn node VoxelGI và nhấp vào **Bake** ở phía trên viewport của trình chỉnh sửa 3D. Quá trình này sẽ mất ít nhất vài giây để hoàn tất (tùy thuộc vào số lượng subdivision của VoxelGI và độ phức tạp của cảnh).

Nếu ít nhất một mesh nằm trong extents của VoxelGI có chế độ global illumination được đặt thành **Static**, bạn sẽ thấy ánh sáng gián tiếp xuất hiện trong cảnh.

.. note::

    Để tránh làm phình to các scene file dạng văn bản với lượng lớn dữ liệu nhị phân, hãy đảm bảo resource VoxelGIData *luôn* được lưu vào một file nhị phân bên ngoài. File này phải được lưu với phần mở rộng ``.res`` (binary resource) thay vì ``.tres`` (text-based resource). Việc sử dụng resource nhị phân bên ngoài cho VoxelGIData sẽ giúp scene dạng văn bản của bạn nhỏ gọn, đồng thời đảm bảo scene được tải và lưu nhanh chóng.

Các thuộc tính của node VoxelGI
-------------------------------

Có thể điều chỉnh các thuộc tính sau trong inspector của node VoxelGI trước khi bake:

- **Subdiv:** Giá trị cao hơn cho ánh sáng gián tiếp chính xác hơn, nhưng phải đánh đổi bằng hiệu suất thấp hơn, thời gian bake lâu hơn và yêu cầu lưu trữ cao hơn. - **Extents:** Đại diện cho kích thước của hình hộp nơi ánh sáng gián tiếp sẽ được bake. Extents được căn giữa quanh origin của node VoxelGI.

Có thể điều chỉnh các thuộc tính sau trong *resource* VoxelGIData nằm trong node VoxelGI sau khi node này được bake:

- **Dynamic Range:** Độ sáng tối đa có thể được biểu diễn trong ánh sáng gián tiếp. Giá trị cao hơn cho phép biểu diễn ánh sáng gián tiếp sáng hơn, nhưng phải đánh đổi bằng độ chính xác thấp hơn (có thể dẫn đến hiện tượng banding nhìn thấy được). Nếu không chắc chắn, hãy giữ nguyên giá trị này. - **Energy:** Năng lượng tổng thể của ánh sáng gián tiếp. Thuộc tính này cũng ảnh hưởng đến năng lượng của ánh sáng trực tiếp phát ra bởi các mesh có material emissive. - **Bias:** Bias tùy chọn được thêm vào các phép tra cứu trong voxel buffer khi runtime. Điều này giúp tránh các artifact tự che khuất. - **Normal Bias:** Tương tự **Bias**, nhưng offset phép tra cứu trong voxel buffer theo surface normal. Điều này cũng giúp tránh các artifact tự che khuất. Giá trị cao hơn làm giảm các phản xạ trên chính bề mặt nhìn thấy được trong các material không rough, nhưng phải đánh đổi bằng hiện tượng light leaking rõ hơn và ánh sáng gián tiếp trông phẳng hơn. Để ưu tiên ẩn các phản xạ trên chính bề mặt hơn chất lượng ánh sáng, hãy đặt **Bias** thành ``0.0`` và **Normal Bias** thành một giá trị từ ``1.0`` đến ``2.0``. - **Propagation:** Hệ số năng lượng dùng cho ánh sáng gián tiếp dội lại. Giá trị cao hơn sẽ tạo ra ánh sáng sáng hơn, khuếch tán hơn (có thể khiến ánh sáng trông quá phẳng). Khi **Use Two Bounces** được bật, bạn có thể muốn giảm **Propagation** để bù cho ánh sáng gián tiếp tổng thể sáng hơn. - **Use Two Bounces:** Nếu được bật, ánh sáng sẽ dội lại hai lần thay vì chỉ một lần. Điều này tạo ra ánh sáng gián tiếp trông chân thực hơn, đồng thời làm cho ánh sáng gián tiếp xuất hiện trong các phản xạ. Việc bật tùy chọn này thường không gây ảnh hưởng đáng kể đến hiệu suất. - **Interior:** Nếu được bật, ánh sáng từ bầu trời môi trường sẽ không được VoxelGI tính đến. Nên bật tùy chọn này trong các cảnh trong nhà để tránh ánh sáng bị rò rỉ từ môi trường.

Tương tác của VoxelGI với ánh sáng và đối tượng
-----------------------------------------------

Để đảm bảo hình ảnh hiển thị chính xác khi sử dụng VoxelGI, bạn phải cấu hình các thuộc tính global illumination của mesh và light theo *mục đích* của chúng trong cảnh (tĩnh hoặc động).

Có 3 chế độ global illumination cho mesh:

- **Disabled:** Mesh sẽ không được tính đến khi bake VoxelGI. Mesh sẽ *nhận* ánh sáng gián tiếp từ cảnh, nhưng sẽ không *đóng góp* ánh sáng gián tiếp cho cảnh. - **Static (default):** Mesh sẽ được tính đến khi bake VoxelGI. Mesh vừa *nhận* vừa *đóng góp* ánh sáng gián tiếp cho cảnh. Nếu mesh bị thay đổi theo bất kỳ cách nào sau khi bake, node VoxelGI phải được bake lại. Nếu không, ánh sáng gián tiếp sẽ hiển thị không chính xác. - **Dynamic:** Mesh sẽ không được tính đến khi bake VoxelGI, nhưng vẫn *nhận* và *đóng góp* ánh sáng gián tiếp cho cảnh theo thời gian thực. Tùy chọn này chậm hơn nhiều so với **Static**. Chỉ sử dụng chế độ global illumination **Dynamic** trên các mesh lớn sẽ thay đổi đáng kể trong quá trình gameplay.

.. note::

    Đối với các mesh có chế độ bake **Static**, hệ thống baking VoxelGI không thể sử dụng custom shader (:ref:`class_ShaderMaterial`). Các mesh này sẽ được xem như hoàn toàn màu đen và chỉ đóng vai trò chặn ánh sáng. Bạn có thể khiến VoxelGI tính đến custom shader bằng cách sử dụng chế độ bake **Dynamic** cho các đối tượng này, nhưng điều đó sẽ làm giảm hiệu suất.

    Đối với :ref:`class_BaseMaterial3D`, hiện tại một số thuộc tính sẽ bị bỏ qua trong quá trình baking. Điều này có thể ảnh hưởng đến hình ảnh hiển thị nếu texture albedo hoặc emission của material được thiết kế dựa trên việc sử dụng một số UV mapping nhất định:

    - **UV1 > Offset** - **UV1 > Scale** - **UV1 > Triplanar** - **Emission > On UV2**

Ngoài ra, có 3 chế độ bake cho light (DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D):

- **Disabled:** Light sẽ không được tính đến khi bake VoxelGI. Light sẽ không đóng góp ánh sáng gián tiếp cho cảnh. - **Static:** Light sẽ được tính đến khi bake VoxelGI. Light sẽ đóng góp ánh sáng gián tiếp cho cảnh. Nếu light bị thay đổi theo bất kỳ cách nào sau khi bake, node VoxelGI phải được bake lại, nếu không ánh sáng gián tiếp sẽ hiển thị không chính xác. Nếu không chắc chắn, hãy sử dụng chế độ này cho ánh sáng level. - **Dynamic (default):** Light sẽ không được tính đến khi bake VoxelGI, nhưng vẫn đóng góp ánh sáng gián tiếp cho cảnh theo thời gian thực. Tùy chọn này chậm hơn so với **Static**. Chỉ sử dụng chế độ global illumination **Dynamic** trên các light sẽ thay đổi đáng kể trong quá trình gameplay.

.. note::

    Lượng năng lượng gián tiếp phát ra bởi một light phụ thuộc vào các thuộc tính color, energy *và* indirect energy của nó. Để khiến một light cụ thể phát ra nhiều hoặc ít năng lượng gián tiếp hơn mà không ảnh hưởng đến lượng ánh sáng trực tiếp do light phát ra, hãy điều chỉnh thuộc tính **Indirect Energy** trong inspector của Light3D.

.. seealso::

    Xem :ref:`doc_introduction_to_global_illumination_gi_mode_recommendations` để biết các khuyến nghị sử dụng chung.

Điều chỉnh hiệu suất và chất lượng VoxelGI
------------------------------------------

Vì VoxelGI tương đối ngốn tài nguyên, nó sẽ hoạt động tốt nhất trên các hệ thống có GPU chuyên dụng đời mới. Trên các GPU chuyên dụng đời cũ và đồ họa tích hợp, cần tinh chỉnh các thiết lập để đạt hiệu suất hợp lý.

Trong phần **Rendering > Global Illumination** của Project Settings, chất lượng VoxelGI cũng có thể được điều chỉnh theo hai cách:

- **Voxel Gi > Quality:** Nếu đặt thành **Low** thay vì **High**, voxel cone tracing sẽ chỉ sử dụng 4 taps thay vì 6. Điều này tăng tốc độ rendering nhưng phải đánh đổi bằng ambient occlusion kém rõ rệt hơn. - **Gi > Use Half Resolution:** Nếu được bật, cả VoxelGI và SDFGI sẽ render GI buffer ở độ phân giải giảm một nửa. Ví dụ, khi rendering ở 3840×2160, GI buffer sẽ được tính toán ở độ phân giải 1920×1080. Bật tùy chọn này giúp tiết kiệm đáng kể thời gian GPU, nhưng có thể tạo ra aliasing nhìn thấy được xung quanh các chi tiết mảnh.

Lưu ý rằng phải bật toggle **Advanced** trong hộp thoại project settings để các thiết lập trên hiển thị.

Ngoài ra, có thể vô hiệu hóa hoàn toàn VoxelGI bằng cách ẩn node VoxelGI. Điều này có thể được dùng cho mục đích so sánh hoặc để cải thiện hiệu suất trên các hệ thống cấu hình thấp.

Giảm hiện tượng light leaking và artifact của VoxelGI
-----------------------------------------------------

Sau khi bake VoxelGI, bạn có thể nhận thấy ánh sáng gián tiếp bị rò rỉ tại một số vị trí trong hình học level. Có thể khắc phục điều này theo một số cách:

- Đối với cả hiện tượng rò rỉ ánh sáng và artifact, hãy thử di chuyển hoặc xoay node VoxelGI, sau đó bake lại. - Để khắc phục hiện tượng rò rỉ ánh sáng nói chung, hãy đảm bảo geometry của level được bịt kín hoàn toàn. Cách tốt nhất là thực hiện việc này trong phần mềm 3D modeling được dùng để thiết kế level, nhưng cũng có thể sử dụng các node MeshInstance3D nguyên thủy với chế độ global illumination được đặt thành **Static**. - Để khắc phục hiện tượng rò rỉ ánh sáng với geometry mỏng, bạn nên làm cho geometry đó dày hơn. Nếu không thể thực hiện việc này, hãy thêm một node MeshInstance3D nguyên thủy với chế độ global illumination được đặt thành **Static**. Bake VoxelGI lại, sau đó ẩn node MeshInstance3D nguyên thủy (node này vẫn sẽ được VoxelGI tính đến). Để đạt kết quả tối ưu, MeshInstance3D nên có material với màu khớp với geometry mỏng ban đầu. - Để khắc phục các artifact có thể xuất hiện trên bề mặt phản chiếu, hãy thử tăng **Bias** và/hoặc **Normal Bias** trong resource VoxelGIData như mô tả ở trên. Không tăng các giá trị này quá cao, nếu không hiện tượng rò rỉ ánh sáng sẽ trở nên rõ rệt hơn.

Nếu bạn nhận thấy các node VoxelGI liên tục xuất hiện rồi biến mất khi camera di chuyển, nguyên nhân rất có thể là engine đang render quá nhiều instance VoxelGI cùng lúc. Godot bị giới hạn ở việc render 8 node VoxelGI cùng lúc, nghĩa là tối đa 8 instance có thể nằm trong tầm nhìn của camera trước khi một số instance bắt đầu nhấp nháy.

Ngoài ra, vì lý do hiệu năng, Godot chỉ có thể blend giữa 2 node VoxelGI tại mỗi pixel trên màn hình. Nếu có hơn 2 node VoxelGI chồng lấp nhau, global illumination có thể xuất hiện hiện tượng nhấp nháy khi camera di chuyển hoặc xoay.
