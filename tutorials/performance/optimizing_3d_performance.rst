.. meta::
    :keywords: tối ưu hóa

.. _doc_optimizing_3d_performance:

Tối ưu hiệu năng 3D
===================

Culling
-------

Godot sẽ tự động thực hiện culling theo frustum của camera để ngăn không cho các đối tượng nằm ngoài viewport được render. Điều này hoạt động tốt với các game diễn ra trong một khu vực nhỏ, tuy nhiên mọi thứ có thể nhanh chóng trở thành vấn đề ở các level lớn hơn.

Occlusion culling
~~~~~~~~~~~~~~~~~

Ví dụ, khi đi bộ quanh một thị trấn, bạn có thể chỉ nhìn thấy vài tòa nhà trên con phố mình đang đứng, cùng với bầu trời và một vài con chim đang bay phía trên. Tuy nhiên, đối với một renderer đơn giản, bạn vẫn có thể nhìn thấy toàn bộ thị trấn. Renderer không chỉ render các tòa nhà phía trước bạn, mà còn render con phố phía sau chúng, những người trên con phố đó và các tòa nhà phía sau nữa. Bạn nhanh chóng rơi vào tình huống phải render nhiều hơn 10× hoặc 100× so với phần đang hiển thị.

Mọi thứ không tệ như vẻ ngoài, vì Z-buffer thường cho phép GPU chỉ thực hiện shading đầy đủ cho các đối tượng ở phía trước. Cách này được gọi là *depth prepass* và được bật mặc định trong Godot khi sử dụng các phương thức render Forward+ hoặc Compatibility. Tuy nhiên, các đối tượng không cần thiết vẫn làm giảm hiệu năng.

Một cách có thể giúp giảm lượng nội dung cần render là **tận dụng occlusion**. Godot cung cấp một phương pháp occlusion culling bằng các node occluder. Xem :ref:`doc_occlusion_culling` để biết hướng dẫn thiết lập occlusion culling trong scene.

.. note::

    Trong một số trường hợp, bạn có thể phải điều chỉnh thiết kế level để tạo thêm cơ hội occlusion. Ví dụ, bạn có thể phải thêm nhiều bức tường hơn để ngăn người chơi nhìn quá xa, điều này sẽ làm giảm hiệu năng do mất đi các cơ hội thực hiện occlusion culling.

Đối tượng trong suốt
--------------------

Godot sắp xếp các đối tượng theo :ref:`Material <class_Material>` và :ref:`Shader <class_Shader>` để cải thiện hiệu năng. Tuy nhiên, việc này không thể thực hiện với các đối tượng trong suốt. Các đối tượng trong suốt được render từ phía sau ra phía trước để việc blend với phần phía sau hoạt động chính xác. Do đó, **hãy cố gắng sử dụng càng ít đối tượng trong suốt càng tốt**. Nếu một đối tượng có một phần nhỏ trong suốt, hãy cố gắng tách phần đó thành một surface riêng với material riêng.

Để biết thêm thông tin, hãy xem tài liệu :ref:`GPU optimizations <doc_gpu_optimization>`.

Mức độ chi tiết (LOD)
---------------------

Trong một số tình huống, đặc biệt là ở khoảng cách xa, bạn nên **thay thế hình học phức tạp bằng các phiên bản đơn giản hơn**. Người dùng cuối có lẽ sẽ không nhận thấy nhiều khác biệt. Hãy thử hình dung một số lượng lớn cây ở rất xa. Có nhiều chiến lược để thay thế model ở các khoảng cách khác nhau. Bạn có thể sử dụng các model có ít polygon hơn hoặc dùng transparency để mô phỏng hình học phức tạp hơn.

Godot 4 cung cấp một số cách để điều khiển level of detail:

- Cách tự động khi import mesh bằng :ref:`doc_mesh_lod`.
- Cách thủ công được cấu hình trong node 3D bằng :ref:`doc_visibility_ranges`.
- :ref:`Decals <doc_using_decals>` và :ref:`lights <doc_lights_and_shadows>` cũng có thể hưởng lợi từ level of detail thông qua các thuộc tính **Distance Fade** tương ứng.

Mặc dù có thể được sử dụng độc lập, các phương pháp này đạt hiệu quả cao nhất khi kết hợp với nhau. Ví dụ, bạn có thể thiết lập các visibility range để ẩn những hiệu ứng particle ở quá xa, khiến người chơi không thể nhận thấy. Đồng thời, bạn có thể dựa vào mesh LOD để khiến mesh của hiệu ứng particle được render với ít chi tiết hơn khi ở xa.

Visibility range cũng là một cách tốt để thiết lập *impostor* cho hình học ở xa (xem bên dưới).

Billboard và imposters
~~~~~~~~~~~~~~~~~~~~~~

Cách đơn giản nhất để sử dụng transparency xử lý LOD là billboard. Ví dụ, bạn có thể dùng một quad trong suốt duy nhất để biểu diễn một cái cây ở xa. Việc render này có thể rất nhẹ, tất nhiên trừ khi có nhiều cây xếp chồng phía trước nhau. Trong trường hợp đó, transparency có thể bắt đầu ảnh hưởng đến fill rate (để biết thêm thông tin về fill rate, xem :ref:`doc_gpu_optimization`).

Một cách khác là không chỉ render một cây mà render một nhóm gồm nhiều cây cùng nhau. Cách này đặc biệt hiệu quả nếu bạn có thể nhìn thấy một khu vực nhưng không thể tiến đến đó trong game.

Bạn có thể tạo impostor bằng cách render trước hình ảnh của một đối tượng ở các góc khác nhau. Hoặc bạn có thể tiến thêm một bước và định kỳ render lại hình ảnh của một đối tượng lên texture để dùng làm impostor. Ở khoảng cách xa, bạn cần di chuyển camera một khoảng đáng kể thì góc nhìn mới thay đổi rõ rệt. Việc này có thể phức tạp để triển khai, nhưng có thể đáng làm tùy thuộc vào loại project bạn đang xây dựng.

Sử dụng instancing tự động
~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ được triển khai trong renderer Forward+, không có trong Mobile hoặc Compatibility.*

Nếu scene của bạn có nhiều đối tượng giống hệt nhau, bạn có thể sử dụng instancing tự động để giảm số lượng draw call. Việc này tự động xảy ra với các node MeshInstance3D sử dụng cùng mesh và material: không cần thiết lập thủ công.

Để instancing tự động đạt hiệu quả, material phải opaque hoặc được alpha-test (alpha scissor hoặc alpha hash). Các material alpha-blended hoặc depth pre-pass sẽ không bao giờ được instancing theo cách này. Thay vào đó, bạn phải sử dụng MultiMesh như mô tả bên dưới.

Sử dụng instancing thủ công (MultiMesh)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu phải vẽ nhiều đối tượng giống hệt nhau tại cùng một vị trí hoặc ở gần nhau, hãy thử sử dụng :ref:`MultiMesh <class_MultiMesh>` thay thế. MultiMesh cho phép vẽ hàng nghìn đối tượng với chi phí hiệu năng rất thấp, vì vậy rất phù hợp cho đàn chim, cỏ, particle và mọi trường hợp khác có hàng nghìn đối tượng giống hệt nhau.

Xem thêm tài liệu :ref:`Using MultiMesh <doc_using_multimesh>`.

Bake lighting
-------------

Chiếu sáng các đối tượng là một trong những thao tác render tốn kém nhất. Lighting realtime, shadow (đặc biệt là nhiều light) và
:ref:`global illumination <doc_introduction_to_global_illumination>` đặc biệt tốn kém. Chúng có thể đơn giản là quá sức đối với các thiết bị di động có công suất thấp.

**Hãy cân nhắc sử dụng baked lighting**, đặc biệt là trên thiết bị di động. Cách này có thể cho hình ảnh tuyệt đẹp, nhưng có nhược điểm là không dynamic. Đôi khi, đây là một sự đánh đổi đáng chấp nhận.

Xem :ref:`doc_using_lightmap_gi` để biết hướng dẫn sử dụng baked lightmap. Để đạt hiệu năng tốt nhất, bạn nên đặt bake mode của các light thành **Static** thay vì **Dynamic** mặc định, vì điều này sẽ bỏ qua lighting realtime trên các mesh đã có baked lighting.

Nhược điểm của các light có bake mode **Static** là chúng không thể đổ shadow lên các mesh có baked lighting. Điều này có thể khiến các scene có môi trường ngoài trời và các đối tượng dynamic trông phẳng. Một sự cân bằng tốt giữa hiệu năng và chất lượng là giữ **Dynamic** cho node :ref:`class_DirectionalLight3D`, và sử dụng **Static** cho hầu hết (nếu không phải tất cả) omni light và spot light.

Animation và skinning
---------------------

Animation và vertex animation như skinning và morphing có thể rất tốn tài nguyên trên một số nền tảng. Bạn có thể cần giảm đáng kể polycount của các model được animate, hoặc giới hạn số lượng model hiển thị trên màn hình tại bất kỳ thời điểm nào. Bạn cũng có thể giảm animation rate cho các mesh ở xa hoặc bị che khuất, hoặc tạm dừng hoàn toàn animation nếu người chơi khó nhận ra animation đã bị dừng.

Các node :ref:`class_VisibleOnScreenEnabler3D` và :ref:`class_VisibleOnScreenNotifier3D` có thể hữu ích cho mục đích này.

Các thế giới lớn
----------------

Nếu bạn đang tạo các thế giới lớn, sẽ có những điểm cần cân nhắc khác với những gì bạn có thể đã quen thuộc từ các game nhỏ hơn.

Các thế giới lớn có thể cần được xây dựng thành các tile có thể được tải theo nhu cầu khi bạn di chuyển trong thế giới. Điều này có thể ngăn mức sử dụng bộ nhớ tăng quá cao, đồng thời giới hạn việc xử lý vào khu vực cục bộ.

Ngoài ra, các thế giới lớn có thể gặp lỗi rendering và physics do sai số floating point. Có thể khắc phục điều này bằng cách sử dụng :ref:`doc_large_world_coordinates`. Nếu không thể sử dụng tọa độ thế giới lớn, bạn có thể dùng các kỹ thuật như định hướng thế giới xoay quanh người chơi (thay vì ngược lại), hoặc định kỳ dịch chuyển gốc tọa độ để giữ mọi thứ tập trung quanh ``Vector3(0, 0, 0)``.
