.. _doc_using_voxel_gi:

Sử dụng global illumination bằng voxel
======================================

VoxelGI là một dạng global illumination hoàn toàn theo thời gian thực, предназнач предназнач cho các cảnh 3D quy mô nhỏ/trung bình. VoxelGI khá tốn GPU, vì vậy tốt nhất nên sử dụng khi nhắm đến các card đồ họa chuyên dụng.

.. important::

    VoxelGI chỉ được hỗ trợ khi sử dụng renderer Forward+, không hỗ trợ các renderer Mobile hoặc Compatibility.

.. seealso::

    Không chắc VoxelGI có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :alt: Đã tắt VoxelGI.

   Đã tắt VoxelGI.

.. figure:: img/gi_voxel_gi.webp
   :alt: Đã bật VoxelGI.

   Đã bật VoxelGI.

Thiết lập VoxelGI
-----------------

1. Đảm bảo hình học level tĩnh của bạn được import với tùy chọn Light Baking đặt thành **Static** hoặc **Static Lightmaps** trong dock Import. Đối với các node MeshInstance3D được thêm thủ công, hãy đảm bảo thuộc tính **Global Illumination > Mode** được đặt thành **Static** trong inspector.
2. Tạo một node VoxelGI trong dock Scene tree.
3. Di chuyển node VoxelGI đến trung tâm của khu vực bạn muốn nó bao phủ bằng cách kéo gizmo điều khiển trong viewport 3D. Sau đó điều chỉnh phạm vi của VoxelGI bằng cách kéo các điểm màu đỏ trong viewport 3D (hoặc nhập các giá trị trong inspector). Đảm bảo phạm vi của VoxelGI không lớn hơn cần thiết, nếu không chất lượng sẽ bị ảnh hưởng.
4. Chọn node VoxelGI rồi nhấp vào **Bake** ở đầu viewport trình chỉnh sửa 3D. Quá trình này sẽ mất ít nhất vài giây để hoàn tất (tùy thuộc vào số subdivision của VoxelGI và độ phức tạp của cảnh).

Nếu ít nhất một mesh nằm trong phạm vi của VoxelGI có chế độ global illumination được đặt thành **Static**, bạn sẽ thấy ánh sáng gián tiếp xuất hiện trong cảnh.

.. note::

    Để tránh làm phình các tệp cảnh dạng văn bản với lượng lớn dữ liệu nhị phân, hãy đảm bảo resource VoxelGIData được *always* lưu vào một tệp nhị phân bên ngoài. Tệp này phải được lưu với phần mở rộng ``.res`` (binary resource) thay vì ``.tres`` (text-based resource). Sử dụng resource nhị phân bên ngoài cho VoxelGIData sẽ giúp tệp cảnh dạng văn bản nhỏ gọn, đồng thời đảm bảo tệp được tải và lưu nhanh chóng.

Các thuộc tính của node VoxelGI
-------------------------------

Có thể điều chỉnh các thuộc tính sau trong inspector của node VoxelGI trước khi bake:

- **Subdiv:** Giá trị cao hơn tạo ra ánh sáng gián tiếp chính xác hơn, nhưng phải đánh đổi bằng hiệu năng thấp hơn, thời gian bake lâu hơn và yêu cầu lưu trữ cao hơn.
- **Extents:** Biểu thị kích thước của hộp mà trong đó ánh sáng gián tiếp sẽ được bake. Phạm vi được căn giữa theo origin của node VoxelGI.

Có thể điều chỉnh các thuộc tính sau trong *resource* VoxelGIData nằm trong node VoxelGI sau khi node này được bake:

- **Dynamic Range:** Độ sáng tối đa có thể được biểu diễn trong ánh sáng gián tiếp. Giá trị cao hơn cho phép biểu diễn ánh sáng gián tiếp sáng hơn, nhưng phải đánh đổi bằng độ chính xác thấp hơn (có thể tạo ra hiện tượng phân dải nhìn thấy được). Nếu không chắc chắn, hãy giữ nguyên giá trị này.
- **Energy:** Năng lượng tổng thể của ánh sáng gián tiếp. Điều này cũng ảnh hưởng đến năng lượng của ánh sáng trực tiếp do các mesh có material phát sáng phát ra.
- **Bias:** Độ lệch tùy chọn được thêm vào các phép tra cứu trong voxel buffer khi chạy. Điều này giúp tránh các hiện tượng tự che khuất.
- **Normal Bias:** Tương tự **Bias**, nhưng dịch phép tra cứu trong voxel buffer theo pháp tuyến bề mặt. Điều này cũng giúp tránh các hiện tượng tự che khuất. Giá trị cao hơn làm giảm hiện tượng tự phản chiếu nhìn thấy được trên các material không nhám, nhưng phải đánh đổi bằng hiện tượng rò rỉ ánh sáng rõ hơn và ánh sáng gián tiếp trông phẳng hơn. Để ưu tiên ẩn hiện tượng tự phản chiếu hơn chất lượng ánh sáng, đặt **Bias** thành ``0.0`` và **Normal Bias** thành một giá trị từ ``1.0`` đến ``2.0``.
- **Propagation:** Hệ số năng lượng dùng cho ánh sáng gián tiếp phản xạ. Giá trị cao hơn tạo ra ánh sáng sáng hơn và khuếch tán hơn (có thể trông quá phẳng). Khi **Use Two Bounces** được bật, bạn có thể muốn giảm **Propagation** để bù cho ánh sáng gián tiếp tổng thể sáng hơn.
- **Use Two Bounces:** Khi được bật, ánh sáng sẽ phản xạ hai lần thay vì chỉ một lần. Điều này tạo ra ánh sáng gián tiếp trông thực tế hơn và cũng làm cho ánh sáng gián tiếp hiển thị trong các phản chiếu. Việc bật tùy chọn này nhìn chung không gây ra chi phí hiệu năng đáng kể.
- **Interior:** Khi được bật, ánh sáng bầu trời từ môi trường sẽ không được VoxelGI tính đến. Nên bật tùy chọn này trong các cảnh trong nhà để tránh ánh sáng từ môi trường bị rò rỉ.

Tương tác của VoxelGI với ánh sáng và đối tượng
-----------------------------------------------

Để đảm bảo hình ảnh chính xác khi sử dụng VoxelGI, bạn phải cấu hình các thuộc tính global illumination của mesh và ánh sáng theo *purpose* của chúng trong cảnh (tĩnh hoặc động).

Có 3 chế độ global illumination dành cho mesh:

- **Disabled:** Mesh sẽ không được tính đến khi bake VoxelGI. Mesh sẽ *receive* ánh sáng gián tiếp từ cảnh, nhưng sẽ không *contribute* ánh sáng gián tiếp vào cảnh.
- **Static (default):** Mesh sẽ được tính đến khi bake VoxelGI. Mesh vừa nhận *and* đóng góp ánh sáng gián tiếp vào cảnh. Nếu mesh bị thay đổi theo bất kỳ cách nào sau khi bake, node VoxelGI phải được bake lại. Nếu không, ánh sáng gián tiếp sẽ hiển thị không chính xác.
- **Dynamic:** Mesh sẽ không được tính đến khi bake VoxelGI, nhưng vẫn nhận *and* đóng góp ánh sáng gián tiếp vào cảnh theo thời gian thực. Tùy chọn này chậm hơn nhiều so với **Static**. Chỉ sử dụng chế độ global illumination **Dynamic** trên các mesh lớn sẽ thay đổi đáng kể trong quá trình chơi.

.. note::

    Đối với các mesh có chế độ bake **Static**, hệ thống bake VoxelGI không thể sử dụng shader tùy chỉnh (:ref:`class_ShaderMaterial`). Các mesh này sẽ được xem là hoàn toàn màu đen và chỉ có tác dụng chặn ánh sáng. Bạn có thể khiến VoxelGI tính đến shader tùy chỉnh bằng cách sử dụng chế độ bake **Dynamic** cho các đối tượng này, nhưng điều đó sẽ làm giảm hiệu năng.

    Đối với :ref:`class_BaseMaterial3D`, hiện một số thuộc tính đang bị bỏ qua trong quá trình baking. Điều này có thể ảnh hưởng đến hình ảnh nếu texture albedo hoặc emission của material được thiết kế dựa trên việc sử dụng một số ánh xạ UV nhất định:

    - **UV1 > Offset**
    - **UV1 > Scale**
    - **UV1 > Triplanar**
    - **Emission > On UV2**

Ngoài ra, có 3 chế độ baking khả dụng cho các đèn (DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D):

- **Disabled:** Đèn sẽ không được tính đến khi baking VoxelGI. Đèn sẽ không đóng góp ánh sáng gián tiếp cho cảnh.
- **Static:** Đèn sẽ được tính đến khi baking VoxelGI. Đèn sẽ đóng góp ánh sáng gián tiếp cho cảnh. Nếu đèn bị thay đổi theo bất kỳ cách nào sau khi baking, phải bake lại node VoxelGI, nếu không ánh sáng gián tiếp sẽ hiển thị không chính xác. Nếu không chắc chắn, hãy sử dụng chế độ này cho ánh sáng của level.
- **Dynamic (default):** Đèn sẽ không được tính đến khi baking VoxelGI, nhưng vẫn đóng góp ánh sáng gián tiếp cho cảnh theo thời gian thực. Tùy chọn này chậm hơn so với **Static**. Chỉ sử dụng chế độ global illumination **Dynamic** trên các đèn sẽ thay đổi đáng kể trong quá trình chơi.

.. note::

    Lượng năng lượng gián tiếp do đèn phát ra phụ thuộc vào màu sắc, năng lượng *và* các thuộc tính năng lượng gián tiếp của đèn. Để một đèn cụ thể phát ra nhiều hơn hoặc ít hơn năng lượng gián tiếp mà không ảnh hưởng đến lượng ánh sáng trực tiếp do đèn phát ra, hãy điều chỉnh thuộc tính **Indirect Energy** trong inspector của Light3D.

.. seealso::

    Xem :ref:`doc_introduction_to_global_illumination_gi_mode_recommendations` để biết các khuyến nghị sử dụng chung.

Điều chỉnh hiệu năng và chất lượng VoxelGI
------------------------------------------

Vì VoxelGI tương đối tốn tài nguyên, nó sẽ hoạt động tốt nhất trên các hệ thống có GPU rời đời mới. Trên các GPU rời đời cũ và đồ họa tích hợp, cần tinh chỉnh các thiết lập để đạt hiệu năng hợp lý.

Trong phần **Rendering > Global Illumination** của Project Settings, chất lượng VoxelGI cũng có thể được điều chỉnh theo hai cách:

- **Voxel Gi > Quality:** Nếu được đặt thành **Low** thay vì **High**, voxel cone tracing sẽ chỉ sử dụng 4 mẫu thay vì 6. Điều này tăng tốc quá trình render nhưng làm ambient occlusion kém rõ rệt hơn.
- **Gi > Use Half Resolution:** Khi được bật, cả VoxelGI và SDFGI sẽ render bộ đệm GI ở độ phân giải giảm một nửa. Ví dụ, khi render ở độ phân giải 3840×2160, bộ đệm GI sẽ được tính ở độ phân giải 1920×1080. Bật tùy chọn này giúp tiết kiệm đáng kể thời gian GPU, nhưng có thể tạo ra hiện tượng aliasing rõ rệt xung quanh các chi tiết mảnh.

Lưu ý rằng phải bật nút chuyển **Advanced** trong hộp thoại project settings để các thiết lập trên hiển thị.

Ngoài ra, có thể tắt hoàn toàn VoxelGI bằng cách ẩn node VoxelGI. Bạn có thể dùng cách này để so sánh hoặc cải thiện hiệu năng trên các hệ thống cấp thấp.

Giảm hiện tượng rò rỉ ánh sáng và artifact của VoxelGI
------------------------------------------------------

Sau khi baking VoxelGI, bạn có thể nhận thấy ánh sáng gián tiếp bị rò rỉ tại một số vị trí trong hình học của level. Có thể khắc phục điều này bằng một số cách:

- Đối với cả hiện tượng rò rỉ ánh sáng và artifact, hãy thử di chuyển hoặc xoay node VoxelGI rồi bake lại.
- Để xử lý hiện tượng rò rỉ ánh sáng nói chung, hãy đảm bảo hình học của level được bịt kín hoàn toàn. Cách tốt nhất là thực hiện việc này trong phần mềm 3D modeling được dùng để thiết kế level, nhưng cũng có thể sử dụng các node MeshInstance3D nguyên thủy với chế độ global illumination được đặt thành **Static**.
- Để xử lý hiện tượng rò rỉ ánh sáng với hình học mỏng, bạn nên làm phần hình học đó dày hơn. Nếu không thể, hãy thêm một node MeshInstance3D nguyên thủy với chế độ global illumination được đặt thành **Static**. Bake lại VoxelGI, sau đó ẩn node MeshInstance3D nguyên thủy (node này vẫn được VoxelGI tính đến). Để đạt kết quả tối ưu, MeshInstance3D nên có material với màu khớp với hình học mỏng ban đầu.
- Để xử lý các artifact có thể xuất hiện trên các bề mặt phản chiếu, hãy thử tăng **Bias** và/hoặc **Normal Bias** trong resource VoxelGIData như mô tả ở trên. Không nên tăng các giá trị này quá cao, nếu không hiện tượng rò rỉ ánh sáng sẽ trở nên rõ rệt hơn.

Nếu nhận thấy các node VoxelGI liên tục xuất hiện rồi biến mất khi camera di chuyển, nhiều khả năng là do engine đang render quá nhiều instance VoxelGI cùng lúc. Godot bị giới hạn ở việc render 8 node VoxelGI cùng lúc, nghĩa là có thể có tối đa 8 instance trong vùng nhìn của camera trước khi một số instance bắt đầu nhấp nháy.

Ngoài ra, vì lý do hiệu năng, Godot chỉ có thể blend giữa 2 node VoxelGI tại một pixel nhất định trên màn hình. Nếu có hơn 2 node VoxelGI chồng lấp, global illumination có thể nhấp nháy khi camera di chuyển hoặc xoay.
