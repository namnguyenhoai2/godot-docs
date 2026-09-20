.. meta::
    :keywords: optimization

.. _doc_optimizing_3d_performance:

Tối ưu hiệu năng 3D
===================

Culling
-------

Godot sẽ tự động thực hiện view frustum culling để tránh render các đối tượng nằm ngoài viewport. Cách này hoạt động tốt với các game diễn ra trong một khu vực nhỏ, tuy nhiên mọi thứ có thể nhanh chóng trở nên khó kiểm soát ở các level lớn hơn.

Occlusion culling
~~~~~~~~~~~~~~~~~

Ví dụ, khi đi bộ quanh một thị trấn, bạn có thể chỉ nhìn thấy một vài tòa nhà trên con phố mình đang đứng, cùng với bầu trời và một vài chú chim bay phía trên. Tuy nhiên, đối với một renderer ngây thơ, bạn vẫn có thể nhìn thấy toàn bộ thị trấn. Nó không chỉ render các tòa nhà phía trước bạn, mà còn render cả con phố phía sau đó, những người trên con phố ấy, rồi các tòa nhà phía sau nữa. Bạn sẽ nhanh chóng rơi vào tình huống phải render nhiều hơn 10× hoặc 100× so với những gì có thể nhìn thấy.

Mọi thứ không tệ đến mức đó, vì Z-buffer thường cho phép GPU chỉ thực hiện đầy đủ việc shade các đối tượng ở phía trước. Đây được gọi là *depth prepass* và được bật mặc định trong Godot khi sử dụng các phương thức render Forward+ hoặc Compatibility. Tuy nhiên, các đối tượng không cần thiết vẫn làm giảm hiệu năng.

Một cách có thể giúp giảm lượng cần render là **tận dụng occlusion**. Godot cung cấp một phương pháp occlusion culling bằng cách sử dụng các occluder node. Xem :ref:`doc_occlusion_culling` để biết hướng dẫn thiết lập occlusion culling trong scene của bạn.

.. note::

    Trong một số trường hợp, bạn có thể phải điều chỉnh thiết kế level để tạo thêm các cơ hội occlusion. Ví dụ, bạn có thể phải thêm nhiều bức tường hơn để ngăn người chơi nhìn quá xa, nếu không hiệu năng sẽ giảm do bỏ lỡ các cơ hội thực hiện occlusion culling.

Các đối tượng trong suốt
------------------------

Godot sắp xếp các đối tượng theo :ref:`Material <class_Material>` và :ref:`Shader <class_Shader>` để cải thiện hiệu năng. Tuy nhiên, việc này không thể thực hiện với các đối tượng trong suốt. Các đối tượng trong suốt được render từ phía sau ra phía trước để việc blending với phần nằm phía sau hoạt động chính xác. Vì vậy, **hãy cố gắng sử dụng càng ít đối tượng trong suốt càng tốt**. Nếu một đối tượng có một phần nhỏ trong suốt, hãy thử tách phần đó thành một surface riêng với material riêng.

Để biết thêm thông tin, hãy xem tài liệu :ref:`GPU optimizations <doc_gpu_optimization>`.

Mức độ chi tiết (LOD)
---------------------

Trong một số tình huống, đặc biệt là khi ở xa, **thay thế hình học phức tạp bằng các phiên bản đơn giản hơn** có thể là một ý tưởng hay. Người dùng cuối có lẽ sẽ không thể nhận ra nhiều khác biệt. Hãy thử hình dung một số lượng lớn cây ở rất xa. Có một số chiến lược để thay thế model ở các khoảng cách khác nhau. Bạn có thể sử dụng model có ít polygon hơn, hoặc dùng transparency để mô phỏng hình học phức tạp hơn.

Godot 4 cung cấp một số cách để kiểm soát level of detail:

- Một phương pháp tự động khi import mesh bằng :ref:`doc_mesh_lod`. - Một phương pháp thủ công được cấu hình trong node 3D bằng :ref:`doc_visibility_ranges`. - :ref:`Decals <doc_using_decals>` và :ref:`lights <doc_lights_and_shadows>` cũng có thể tận dụng level of detail thông qua các thuộc tính **Distance Fade** tương ứng.

Mặc dù có thể được sử dụng độc lập, các phương pháp này đạt hiệu quả cao nhất khi được sử dụng cùng nhau. Ví dụ, bạn có thể thiết lập các visibility range để ẩn những hiệu ứng particle ở quá xa người chơi khiến họ không thể nhận thấy. Đồng thời, bạn có thể dựa vào mesh LOD để các mesh của hiệu ứng particle được render với ít chi tiết hơn khi ở xa.

Visibility range cũng là một cách hay để thiết lập *impostor* cho hình học ở xa (xem bên dưới).

Billboard và impostor
~~~~~~~~~~~~~~~~~~~~~

Cách đơn giản nhất để sử dụng transparency nhằm xử lý LOD là billboard. Ví dụ, bạn có thể dùng một quad trong suốt duy nhất để biểu diễn một cái cây ở xa. Việc render này có thể rất nhẹ, tất nhiên trừ khi có nhiều cây nằm chồng lên nhau. Trong trường hợp đó, transparency có thể bắt đầu tiêu tốn fill rate (để biết thêm thông tin về fill rate, hãy xem :ref:`doc_gpu_optimization`).

Một lựa chọn khác là không chỉ render một cây, mà render nhiều cây cùng nhau dưới dạng một nhóm. Cách này có thể đặc biệt hiệu quả nếu bạn nhìn thấy một khu vực nhưng không thể tiếp cận nó trong game.

Bạn có thể tạo impostor bằng cách pre-render hình ảnh của một đối tượng từ các góc khác nhau. Hoặc bạn thậm chí có thể tiến thêm một bước, định kỳ render lại hình ảnh của một đối tượng lên một texture để dùng làm impostor. Ở khoảng cách xa, bạn cần di chuyển viewer một khoảng đáng kể thì góc nhìn mới thay đổi rõ rệt. Việc này có thể phức tạp để triển khai, nhưng có thể đáng làm tùy vào loại project bạn đang tạo.

Sử dụng instancing tự động
~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ được triển khai trong renderer Forward+, không có trong Mobile hoặc Compatibility.*

Nếu scene của bạn có nhiều đối tượng giống hệt nhau, bạn có thể sử dụng instancing tự động để giảm số lượng draw call. Việc này tự động xảy ra với các node MeshInstance3D sử dụng cùng mesh và material: không cần thiết lập thủ công.

Để instancing tự động đạt hiệu quả, material phải opaque hoặc được alpha-test (alpha scissor hoặc alpha hash). Các material alpha-blended hoặc depth pre-pass không bao giờ được instancing theo cách này. Thay vào đó, bạn phải sử dụng MultiMesh như mô tả bên dưới.

Sử dụng instancing thủ công (MultiMesh)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu phải vẽ nhiều đối tượng giống hệt nhau tại cùng một vị trí hoặc gần nhau, hãy thử sử dụng :ref:`MultiMesh <class_MultiMesh>` thay thế. MultiMesh cho phép vẽ nhiều nghìn đối tượng với chi phí hiệu năng rất thấp, khiến nó trở nên lý tưởng cho đàn động vật, cỏ, particle và bất kỳ thứ gì khác có hàng nghìn đối tượng giống hệt nhau.

Xem thêm tài liệu :ref:`Using MultiMesh <doc_using_multimesh>`.

Bake lighting
-------------

Chiếu sáng các đối tượng là một trong những thao tác render tốn kém nhất. Lighting theo thời gian thực, shadow (đặc biệt là nhiều light), và
:ref:`global illumination <doc_introduction_to_global_illumination>` are especially
đều tốn kém. Chúng có thể đơn giản là quá nặng để các thiết bị mobile công suất thấp xử lý.

**Hãy cân nhắc sử dụng baked lighting**, đặc biệt là trên mobile. Cách này có thể trông tuyệt đẹp, nhưng có nhược điểm là không dynamic. Đôi khi, đây là một sự đánh đổi đáng chấp nhận.

Xem :ref:`doc_using_lightmap_gi` để biết hướng dẫn sử dụng baked lightmap. Để đạt hiệu năng tốt nhất, bạn nên đặt bake mode của light thành **Static** thay vì mặc định **Dynamic**, vì cách này sẽ bỏ qua lighting theo thời gian thực trên các mesh đã có baked lighting.

Nhược điểm của các light có bake mode **Static** là chúng không thể đổ shadow lên các mesh có baked lighting. Điều này có thể khiến các scene có môi trường ngoài trời và các đối tượng dynamic trông phẳng. Một sự cân bằng tốt giữa hiệu năng và chất lượng là giữ **Dynamic** cho node :ref:`class_DirectionalLight3D`, và sử dụng **Static** cho hầu hết (nếu không phải tất cả) omni light và spot light.

Animation và skinning
---------------------

Animation và vertex animation như skinning và morphing có thể rất tốn kém trên một số platform. Bạn có thể cần giảm đáng kể polycount của các model được animate, hoặc giới hạn số lượng model xuất hiện trên màn hình tại một thời điểm. Bạn cũng có thể giảm animation rate của các mesh ở xa hoặc bị occlude, hoặc tạm dừng hoàn toàn animation nếu người chơi khó có khả năng nhận ra animation đã dừng.

Các node :ref:`class_VisibleOnScreenEnabler3D` và :ref:`class_VisibleOnScreenNotifier3D` có thể hữu ích cho mục đích này.

Các world lớn
-------------

Nếu bạn đang tạo các world lớn, sẽ có những yếu tố cần cân nhắc khác với những gì bạn có thể đã quen thuộc từ các game nhỏ hơn.

Các world lớn có thể cần được xây dựng thành các tile có thể load theo nhu cầu khi bạn di chuyển quanh world. Điều này có thể ngăn việc sử dụng memory tăng vượt kiểm soát, đồng thời giới hạn lượng xử lý cần thiết vào khu vực lân cận.

Ngoài ra, các world lớn có thể gặp lỗi render và physics do sai số floating point. Có thể giải quyết vấn đề này bằng cách sử dụng :ref:`doc_large_world_coordinates`. Nếu việc sử dụng tọa độ world lớn không phải là một lựa chọn, bạn có thể dùng các kỹ thuật như định hướng world xoay quanh người chơi (thay vì ngược lại), hoặc định kỳ dịch chuyển origin để giữ mọi thứ tập trung quanh ``Vector3(0, 0, 0)``.
