.. _doc_reflection_probes:

Probe phản xạ
=============

Như đã nêu trong :ref:`doc_standard_material_3d`, các vật thể có thể hiển thị ánh sáng phản xạ và/hoặc ánh sáng khuếch tán. Probe phản xạ được dùng làm nguồn ánh sáng phản xạ *và* ánh sáng môi trường cho các vật thể nằm trong vùng ảnh hưởng của chúng. Chúng có thể được dùng để cung cấp phản xạ chính xác hơn :ref:`VoxelGI <doc_using_voxel_gi>` và
:ref:`SDFGI <doc_using_sdfgi>` while being fairly cheap on system resources.

Vì probe phản xạ cũng có thể lưu trữ ánh sáng môi trường, chúng có thể được dùng làm giải pháp thay thế cấp thấp cho VoxelGI và SDFGI khi :ref:`baked lightmaps <doc_using_lightmap_gi>` không khả thi (ví dụ: trong các level được tạo theo thủ tục).

Probe phản xạ cũng có thể được dùng đồng thời với phản xạ trong không gian màn hình để cung cấp phản xạ cho các vật thể nằm ngoài màn hình. Trong trường hợp này, Godot sẽ hòa trộn phản xạ trong không gian màn hình với phản xạ từ các probe phản xạ.

.. seealso::

    Không chắc ReflectionProbe có phù hợp với nhu cầu của bạn không? Hãy xem :ref:`doc_introduction_to_global_illumination_comparison` để so sánh các kỹ thuật GI có sẵn trong Godot 4.

So sánh trực quan
-----------------

.. figure:: img/gi_none.webp
   :align: center
   :alt: Reflection probe disabled. Environment sky is used as a fallback.

   Reflection probe disabled. Environment sky is used as a fallback.

.. figure:: img/gi_none_reflection_probe.webp
   :align: center
   :alt: Reflection probe enabled.

   Reflection probe enabled.


.. figure:: img/gi_lightmap_gi_indirect_only_reflection_probe.webp
   :align: center
   :alt: Reflection probe enabled.

   Reflection probe enabled with LightmapGI used at the same time. The lightmap appears in the reflection.

Bằng cách kết hợp probe phản xạ với phản xạ trong không gian màn hình, bạn có thể tận dụng ưu điểm của cả hai: phản xạ chất lượng cao cho cấu trúc phòng nói chung (vẫn hiện diện khi nằm ngoài màn hình), đồng thời có phản xạ theo thời gian thực cho các chi tiết nhỏ.

.. figure:: img/reflection_probes_reflection_probe.webp
   :align: center
   :alt: Reflections in a room using ReflectionProbe only.

   Reflections in a room using ReflectionProbe only. Notice how small details
   don't have any reflections.

.. figure:: img/reflection_probes_ssr.webp
   :align: center
   :alt: Reflections in a room using screen-space reflections only.

   Reflections in a room using screen-space reflections only. Notice how the
   reflection on the sides of the room's walls is partly missing due to being
   off-screen.

.. figure:: img/reflection_probes_reflection_probe_ssr.webp
   :align: center
   :alt: Reflections in a room using ReflectionProbe and screen-space reflections together.

   Reflections in a room using ReflectionProbe and screen-space reflections together.
   The screen-space reflections are blended with the reflection probe,
   acting as a fallback in situations where the reflection probe fails to display
   any reflection.

Thiết lập ReflectionProbe
-------------------------

- Thêm một node :ref:`class_ReflectionProbe`. - Cấu hình phạm vi của ReflectionProbe trong inspector để phù hợp với scene của bạn. Để có phản xạ tương đối chính xác, nhìn chung bạn nên có một node ReflectionProbe cho mỗi phòng (đôi khi cần nhiều hơn đối với các phòng lớn).

.. tip::

    Hãy nhớ rằng phạm vi của ReflectionProbe không nhất thiết phải là hình vuông, và bạn thậm chí có thể xoay node ReflectionProbe để phù hợp với các phòng không thẳng hàng với lưới X/Z. Hãy tận dụng điều này để bao phủ các phòng tốt hơn mà không cần đặt quá nhiều node ReflectionProbe.

Các thuộc tính của ReflectionProbe
----------------------------------

- **Update Mode:** Kiểm soát thời điểm probe phản xạ được cập nhật. **Once** chỉ render scene một lần mỗi khi ReflectionProbe được di chuyển. Điều này giúp render nhanh hơn nhiều so với chế độ cập nhật **Always**, chế độ buộc probe phải render lại mọi thứ xung quanh trong mỗi frame. Hãy để thuộc tính này ở **Once** (mặc định), trừ khi bạn cần probe phản xạ được cập nhật trong mỗi frame. - **Intensity:** Độ sáng của phản xạ và ánh sáng môi trường. Thông thường không cần thay đổi giá trị mặc định ``1.0`` của thuộc tính này, nhưng bạn có thể giảm giá trị ``1.0`` nếu thấy phản xạ quá mạnh. - **Max Distance:** Kiểm soát khoảng cách tối đa được camera nội bộ của ReflectionProbe sử dụng. Khoảng cách này luôn ít nhất bằng **Extents**, nhưng có thể tăng lên để các vật thể nằm ngoài phạm vi vẫn hiển thị trong phản xạ. *Thuộc tính này không ảnh hưởng đến khoảng cách tối đa mà tại đó bản thân ReflectionProbe hiển thị.* - **Extents:** Vùng chịu ảnh hưởng bởi ánh sáng và phản xạ của ReflectionProbe. - **Origin Offset:** Gốc tọa độ được dùng cho camera nội bộ phục vụ việc render probe phản xạ. Gốc này luôn phải nằm trong **Extents**. Nếu cần, hãy điều chỉnh để ngăn phản xạ bị che khuất bởi một vật thể rắn nằm đúng tại tâm của ReflectionProbe. - **Box Projection:** Kiểm soát việc có sử dụng hiệu chỉnh thị sai khi render probe phản xạ hay không. Tùy chọn này điều chỉnh hình thức của phản xạ tùy theo vị trí của camera (so với probe phản xạ). Tùy chọn này tiêu tốn một ít hiệu năng, nhưng mức cải thiện chất lượng thường rất đáng giá trong các phòng hình hộp. Lưu ý rằng hiệu ứng này không hoạt động tốt bằng trong các phòng có hình dạng kém đều đặn (chẳng hạn như phòng hình elip). - **Interior:** Nếu được bật, ánh sáng môi trường sẽ không lấy từ bầu trời của environment, và bầu trời nền sẽ không được render lên probe phản xạ. - **Enable Shadows:** Kiểm soát việc bóng đổ của ánh sáng theo thời gian thực có được render bên trong probe phản xạ hay không. Bật tùy chọn này để cải thiện chất lượng phản xạ nhưng sẽ giảm hiệu năng. Nên tắt tùy chọn này đối với các probe phản xạ dùng chế độ **Always**, vì việc render phản xạ có bóng đổ trong mỗi frame rất tốn tài nguyên. Bóng đổ hoàn toàn :ref:`baked light <doc_using_lightmap_gi>` không bị ảnh hưởng bởi thiết lập này và sẽ được render trong probe phản xạ bất kể thiết lập. - **Cull Mask:** Kiểm soát những vật thể nào hiển thị trong phản xạ. Có thể dùng tùy chọn này để cải thiện hiệu năng bằng cách loại trừ các vật thể nhỏ khỏi phản xạ. Tùy chọn này cũng có thể được dùng để ngăn một vật thể xuất hiện các artifact tự phản xạ trong những tình huống không thể sử dụng **Origin Offset**. - **Mesh LOD Threshold:** Ngưỡng level of detail tự động được dùng để render các mesh bên trong phản xạ. Tùy chọn này chỉ ảnh hưởng đến các mesh đã được tạo LOD tự động. Giá trị cao hơn có thể cải thiện hiệu năng bằng cách sử dụng hình học ít chi tiết hơn, đặc biệt đối với các vật thể ở xa gốc của phản xạ. Sự khác biệt về hình ảnh khi sử dụng các vật thể ít chi tiết hơn thường không đáng chú ý trong quá trình chơi, đặc biệt là trong các phản xạ thô.

Danh mục Ambient có một số thuộc tính để điều chỉnh ánh sáng môi trường được render bởi ReflectionProbe:

- **Mode:** Nếu đặt thành **Disabled**, probe sẽ không thêm ánh sáng môi trường. Nếu đặt thành **Environment**, màu ánh sáng môi trường sẽ được tự động lấy mẫu từ bầu trời của environment (nếu **Interior** bị tắt) và màu trung bình của phản xạ. Nếu đặt thành **Constant Color**, màu được chỉ định trong thuộc tính **Color** sẽ được sử dụng thay thế. Chế độ **Constant Color** có thể được dùng để xấp xỉ ánh sáng vùng. - **Color:** Màu được sử dụng khi chế độ ánh sáng môi trường được đặt thành **Constant Mode**. - **Color Energy:** Hệ số nhân được dùng cho **Color** tùy chỉnh của ánh sáng môi trường. Tùy chọn này chỉ có tác dụng khi chế độ ánh sáng môi trường là **Custom Color**.

Hòa trộn ReflectionProbe
------------------------

Để làm cho quá trình chuyển tiếp giữa các nguồn phản xạ mượt mà hơn, Godot hỗ trợ tự động hòa trộn probe:

- Có thể hòa trộn tối đa 4 ReflectionProbe tại một vị trí nhất định. ReflectionProbe cũng sẽ mờ dần một cách mượt mà trở về ánh sáng environment khi nó không tiếp xúc với bất kỳ node ReflectionProbe nào khác. - SDFGI và VoxelGI sẽ hòa trộn mượt mà với ReflectionProbe nếu được sử dụng. Điều này cho phép đặt ReflectionProbe một cách chiến lược để có phản xạ chính xác hơn (hoặc hoàn toàn theo thời gian thực) tại những nơi cần thiết, đồng thời vẫn có phản xạ thô trong vùng ảnh hưởng của VoxelGI hoặc SDFGI.

Để nhiều ReflectionProbe hòa trộn với nhau, bạn cần để một phần phạm vi của mỗi ReflectionProbe chồng lấn lên vùng của các ReflectionProbe khác. Phạm vi chỉ nên chồng lấn ít nhất có thể với các probe phản xạ khác để cải thiện hiệu năng render (thường là vài đơn vị trong không gian 3D).

Giới hạn
--------

Khi sử dụng renderer Forward+, Godot dùng phương pháp *clustering* để render probe phản xạ. Có thể thêm bao nhiêu probe phản xạ tùy ý (miễn là hiệu năng cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered elements* có thể hiện diện trong chế độ xem camera hiện tại. Một clustered element có thể là đèn omni, đèn spot, đèn area, một :ref:`decal <doc_using_decals>`, hoặc một
:ref:`reflection probe <doc_reflection_probes>`. This limit can be increased by adjusting
:ref:`Max Clustered Elements<class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>`
trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng renderer Mobile, chỉ có thể áp dụng 8 probe phản xạ cho mỗi *resource* Mesh riêng lẻ. Nếu có nhiều probe phản xạ ảnh hưởng đến một mesh, không phải tất cả chúng đều được render trên mesh đó.

Tương tự, khi sử dụng renderer Compatibility, có thể áp dụng tối đa 2 probe phản xạ cho mỗi mesh. Nếu có hơn 2 probe phản xạ ảnh hưởng đến một mesh, các probe bổ sung sẽ không được render.
