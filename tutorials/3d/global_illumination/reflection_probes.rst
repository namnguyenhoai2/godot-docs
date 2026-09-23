.. _doc_reflection_probes:

Probe phản chiếu
================

Như đã nêu trong :ref:`doc_standard_material_3d`, các đối tượng có thể hiển thị ánh sáng phản xạ và/hoặc ánh sáng khuếch tán. Probe phản chiếu được dùng làm nguồn ánh sáng môi trường phản xạ *và* cho các đối tượng nằm trong vùng ảnh hưởng của chúng. Chúng có thể cung cấp phản xạ chính xác hơn :ref:`VoxelGI <doc_using_voxel_gi>` và
:ref:`SDFGI <doc_using_sdfgi>` trong khi tiêu tốn tương đối ít tài nguyên hệ thống.

Vì probe phản chiếu cũng có thể lưu trữ ánh sáng môi trường, chúng có thể được dùng làm giải pháp thay thế ở cấp thấp cho VoxelGI và SDFGI khi :ref:`lightmap được bake <doc_using_lightmap_gi>` không khả thi (ví dụ: trong các level được tạo theo quy trình).

Probe phản chiếu cũng có thể được dùng đồng thời với phản xạ không gian màn hình để cung cấp phản xạ cho các đối tượng ngoài màn hình. Trong trường hợp này, Godot sẽ hòa trộn các phản xạ không gian màn hình với các phản xạ từ probe phản chiếu.

.. seealso::

    Không chắc ReflectionProbe có phù hợp với nhu cầu của bạn không? Xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI hiện có trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :align: center
   :alt: Đã tắt probe phản chiếu. Bầu trời của môi trường được dùng làm phương án dự phòng.

   Đã tắt probe phản chiếu. Bầu trời của môi trường được dùng làm phương án dự phòng.

.. figure:: img/gi_none_reflection_probe.webp
   :align: center
   :alt: Đã bật probe phản chiếu.

   Đã bật probe phản chiếu.


.. figure:: img/gi_lightmap_gi_indirect_only_reflection_probe.webp
   :align: center
   :alt: Đã bật probe phản chiếu.

   Đã bật probe phản chiếu cùng lúc với LightmapGI. Lightmap xuất hiện trong phản xạ.

Bằng cách kết hợp probe phản chiếu với phản xạ không gian màn hình, bạn có thể tận dụng ưu điểm của cả hai: phản xạ chất lượng cao cho cấu trúc phòng nói chung (vẫn hiện diện khi nằm ngoài màn hình), đồng thời có phản xạ theo thời gian thực cho các chi tiết nhỏ.

.. figure:: img/reflection_probes_reflection_probe.webp
   :align: center
   :alt: Phản xạ trong một căn phòng chỉ sử dụng ReflectionProbe.

   Phản xạ trong một căn phòng chỉ sử dụng ReflectionProbe. Lưu ý rằng các chi tiết nhỏ không có phản xạ.

.. figure:: img/reflection_probes_ssr.webp
   :align: center
   :alt: Phản xạ trong một căn phòng chỉ sử dụng phản xạ không gian màn hình.

   Phản xạ trong một căn phòng chỉ sử dụng phản xạ không gian màn hình. Lưu ý rằng phản xạ ở hai bên tường phòng bị thiếu một phần vì nằm ngoài màn hình.

.. figure:: img/reflection_probes_reflection_probe_ssr.webp
   :align: center
   :alt: Phản xạ trong một căn phòng sử dụng đồng thời ReflectionProbe và phản xạ không gian màn hình.

   Phản xạ trong một căn phòng sử dụng đồng thời ReflectionProbe và phản xạ không gian màn hình. Các phản xạ không gian màn hình được hòa trộn với probe phản chiếu, đóng vai trò phương án dự phòng trong những tình huống probe phản chiếu không hiển thị được phản xạ.

Thiết lập ReflectionProbe
-------------------------

- Thêm một node :ref:`class_ReflectionProbe`.
- Cấu hình phạm vi của ReflectionProbe trong inspector để phù hợp với cảnh của bạn. Để có phản xạ tương đối chính xác, thông thường bạn nên có một node ReflectionProbe cho mỗi phòng (đôi khi cần nhiều hơn đối với phòng lớn).

.. tip::

    Hãy nhớ rằng phạm vi của ReflectionProbe không nhất thiết phải là hình vuông, và bạn thậm chí có thể xoay node ReflectionProbe để phù hợp với các phòng không thẳng hàng với lưới X/Z. Hãy tận dụng điều này để bao phủ các phòng tốt hơn mà không phải đặt quá nhiều node ReflectionProbe.

Các thuộc tính của ReflectionProbe
----------------------------------

- **Update Mode:** Kiểm soát thời điểm probe phản chiếu cập nhật. **Once** chỉ render cảnh một lần mỗi khi ReflectionProbe được di chuyển. Điều này giúp render nhanh hơn nhiều so với chế độ cập nhật **Always**, chế độ buộc probe render lại mọi thứ xung quanh nó ở mỗi frame. Giữ thuộc tính này ở **Once** (mặc định), trừ khi bạn cần probe phản chiếu cập nhật ở mỗi frame.
- **Intensity:** Độ sáng của phản xạ và ánh sáng môi trường. Thông thường không cần thay đổi giá trị mặc định là ``1.0``, nhưng bạn có thể giảm giá trị này ``1.0`` nếu thấy phản xạ quá mạnh.
- **Max Distance:** Kiểm soát khoảng cách tối đa được camera bên trong của ReflectionProbe sử dụng. Khoảng cách này luôn ít nhất bằng **Extents**, nhưng có thể tăng lên để hiển thị trong phản xạ các đối tượng nằm ngoài phạm vi. *Thuộc tính này không ảnh hưởng đến khoảng cách tối đa mà bản thân ReflectionProbe có thể được nhìn thấy.*
- **Extents:** Vùng chịu ảnh hưởng của ánh sáng và phản xạ từ ReflectionProbe.
- **Origin Offset:** Gốc tọa độ được dùng cho camera bên trong khi render probe phản chiếu. Gốc này luôn phải nằm trong **Extents**. Nếu cần, hãy điều chỉnh để ngăn phản xạ bị che khuất bởi một vật thể rắn nằm chính xác ở tâm của ReflectionProbe.
- **Box Projection:** Kiểm soát việc có sử dụng hiệu chỉnh parallax khi render probe phản chiếu hay không. Tùy chọn này điều chỉnh diện mạo của phản xạ dựa trên vị trí camera (so với probe phản chiếu). Tùy chọn này làm giảm hiệu năng một chút, nhưng mức tăng chất lượng thường rất đáng giá trong các phòng hình hộp. Lưu ý rằng hiệu ứng này không hoạt động tốt bằng trong các phòng có hình dạng kém đều đặn (chẳng hạn như phòng hình elip).
- **Interior:** Nếu bật, ánh sáng môi trường sẽ không lấy từ bầu trời của môi trường, và bầu trời nền sẽ không được render lên probe phản chiếu.
- **Enable Shadows:** Kiểm soát việc có render bóng đổ ánh sáng theo thời gian thực bên trong probe phản chiếu hay không. Bật tùy chọn này để cải thiện chất lượng phản xạ nhưng phải đánh đổi bằng hiệu năng. Nên tắt tùy chọn này đối với các probe phản chiếu ở chế độ **Always**, vì render phản xạ có bóng đổ ở mỗi frame rất tốn tài nguyên. Bóng của :ref:`ánh sáng được bake hoàn toàn <doc_using_lightmap_gi>` không bị ảnh hưởng bởi thiết lập này và sẽ được render trong probe phản chiếu bất kể thiết lập.
- **Cull Mask:** Kiểm soát những đối tượng nào hiển thị trong phản xạ. Có thể dùng tùy chọn này để cải thiện hiệu năng bằng cách loại trừ các đối tượng nhỏ khỏi phản xạ. Tùy chọn này cũng có thể được dùng để ngăn đối tượng xuất hiện lỗi tự phản xạ trong những tình huống không thể sử dụng **Origin Offset**.
- **Mesh LOD Threshold:** Ngưỡng level of detail tự động được dùng để render mesh bên trong phản xạ. Tùy chọn này chỉ ảnh hưởng đến các mesh đã được tạo LOD tự động. Giá trị cao hơn có thể cải thiện hiệu năng bằng cách sử dụng hình học ít chi tiết hơn, đặc biệt đối với các đối tượng ở xa gốc của phản xạ. Khác biệt hình ảnh khi sử dụng các đối tượng ít chi tiết hơn thường không dễ nhận thấy trong lúc chơi, đặc biệt ở các phản xạ thô.

Danh mục Ambient có một số thuộc tính để điều chỉnh ánh sáng môi trường được render bởi ReflectionProbe:

- **Chế độ:** Nếu đặt thành **Disabled**, probe sẽ không thêm ánh sáng môi trường. Nếu đặt thành **Environment**, màu ánh sáng môi trường sẽ được tự động lấy mẫu từ bầu trời môi trường (nếu **Interior** bị tắt) và màu trung bình của reflection. Nếu đặt thành **Constant Color**, màu được chỉ định trong thuộc tính **Color** sẽ được sử dụng thay thế. Có thể sử dụng chế độ **Constant Color** để xấp xỉ ánh sáng vùng.
- **Màu:** Màu được sử dụng khi chế độ ánh sáng môi trường được đặt thành **Constant Mode**.
- **Năng lượng màu:** Hệ số nhân được sử dụng cho **Color** tùy chỉnh của ánh sáng môi trường. Thuộc tính này chỉ có tác dụng khi chế độ ánh sáng môi trường là **Custom Color**.

Blending ReflectionProbe
------------------------

Để làm cho quá trình chuyển tiếp giữa các nguồn reflection mượt mà hơn, Godot hỗ trợ blending probe tự động:

- Có thể blend tối đa 4 ReflectionProbe với nhau tại một vị trí nhất định. ReflectionProbe cũng sẽ mờ dần một cách mượt mà về ánh sáng môi trường khi không chạm vào bất kỳ node ReflectionProbe nào khác.
- SDFGI và VoxelGI sẽ blend mượt mà với ReflectionProbe nếu được sử dụng. Điều này cho phép đặt ReflectionProbe một cách chiến lược để có được reflection chính xác hơn (hoặc hoàn toàn theo thời gian thực) ở những nơi cần thiết, đồng thời vẫn có reflection thô trong vùng ảnh hưởng của VoxelGI hoặc SDFGI.

Để nhiều ReflectionProbe blend với nhau, bạn cần để một phần của mỗi ReflectionProbe chồng lấn lên vùng của các probe còn lại. Các phạm vi mở rộng chỉ nên chồng lấn ít nhất có thể với những reflection probe khác để cải thiện hiệu năng rendering (thường là vài đơn vị trong không gian 3D).

Hạn chế
-------

Khi sử dụng renderer Forward+, Godot dùng phương pháp *clustering* để rendering reflection probe. Có thể thêm bao nhiêu reflection probe tùy ý (miễn là hiệu năng cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered elements* có thể xuất hiện trong khung nhìn hiện tại của camera. Clustered element là omni light, spot light, area light, :ref:`decal <doc_using_decals>`, hoặc một
:ref:`reflection probe <doc_reflection_probes>`. Giới hạn này có thể được tăng lên bằng cách điều chỉnh
:ref:`Max Clustered Elements <class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>` trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng renderer Mobile, chỉ có thể áp dụng 8 reflection probe cho từng *resource* Mesh riêng lẻ. Nếu có nhiều reflection probe ảnh hưởng đến một mesh, không phải tất cả chúng đều được rendering trên mesh đó.

Tương tự, khi sử dụng renderer Compatibility, có thể áp dụng tối đa 2 reflection probe cho mỗi mesh. Nếu có hơn 2 reflection probe ảnh hưởng đến một mesh, các probe bổ sung sẽ không được rendering.
