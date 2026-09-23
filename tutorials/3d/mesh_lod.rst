.. _doc_mesh_lod:

Mức độ chi tiết của lưới (LOD)
==============================

Mức độ chi tiết (LOD) là một trong những cách quan trọng nhất để tối ưu hiệu năng kết xuất trong một dự án 3D, cùng với :ref:`doc_occlusion_culling`.

Trong trang này, bạn sẽ tìm hiểu:

- LOD của lưới có thể cải thiện hiệu năng kết xuất của dự án 3D như thế nào.
- Cách thiết lập LOD của lưới trong Godot.
- Cách đo lường hiệu quả của LOD lưới trong dự án (và những giải pháp thay thế bạn có thể thử nếu kết quả không như mong đợi).

.. seealso::

    Bạn có thể xem cách LOD của lưới hoạt động trong thực tế bằng `Occlusion Culling and Mesh LOD demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/occlusion_culling_mesh_lod>`__.

Giới thiệu
----------

Trước đây, mức độ chi tiết trong game 3D thường bao gồm việc tự tạo các lưới có mật độ hình học thấp hơn, sau đó cấu hình các ngưỡng khoảng cách tại đó những lưới ít chi tiết hơn này sẽ được vẽ. Cách tiếp cận này vẫn được sử dụng ngày nay khi cần kiểm soát nhiều hơn.

Tuy nhiên, trong các dự án có nhiều tài sản 3D chi tiết, việc thiết lập LOD thủ công có thể rất tốn thời gian. Do đó, việc giảm số đa giác của lưới và cấu hình LOD tự động ngày càng trở nên phổ biến.

Godot cung cấp cách tự động tạo các lưới ít chi tiết hơn để sử dụng cho LOD trong quá trình import, sau đó tự động sử dụng các lưới LOD này khi cần. Người dùng hoàn toàn không nhận thấy quá trình này. Thư viện `meshoptimizer <https://meshoptimizer.org/>`__ được sử dụng để tạo lưới LOD ở phía sau.

LOD của lưới hoạt động với mọi node vẽ các lưới 3D. Trong đó có MeshInstance3D, MultiMeshInstance3D, GPUParticles3D và CPUParticles3D.

So sánh trực quan
-----------------

Sau đây là ví dụ về các lưới LOD được tạo trong quá trình import. Các lưới ít chi tiết hơn sẽ được sử dụng khi camera ở xa đối tượng:

.. figure:: img/mesh_lod_comparison_shaded.png
   :align: center
   :alt: Từ chi tiết nhất (trái) đến ít chi tiết nhất (phải), chế độ xem tô bóng

   Từ chi tiết nhất (trái) đến ít chi tiết nhất (phải), chế độ xem tô bóng

Sau đây là cùng hình ảnh đó với kết xuất khung dây để dễ thấy quá trình giảm số đa giác hơn:

.. figure:: img/mesh_lod_comparison_wireframe.png
   :align: center
   :alt: Từ chi tiết nhất (trái) đến ít chi tiết nhất (phải), chế độ xem khung dây

   Từ chi tiết nhất (trái) đến ít chi tiết nhất (phải), chế độ xem khung dây

.. seealso::

    Nếu cần cấu hình mức độ chi tiết thủ công với các lưới do nghệ sĩ tạo, hãy sử dụng :ref:`doc_visibility_ranges` thay vì LOD lưới tự động.

Tạo LOD cho lưới
----------------

Theo mặc định, việc tạo LOD cho lưới diễn ra tự động đối với các cảnh 3D được import (glTF, .blend, Collada, FBX). Sau khi các lưới LOD được tạo, chúng sẽ tự động được sử dụng khi kết xuất cảnh. Bạn không cần cấu hình thủ công.

Tuy nhiên, việc tạo LOD cho lưới **not** tự động diễn ra đối với các lưới 3D được import (OBJ). Điều này là do theo mặc định, các tệp OBJ không được import dưới dạng cảnh 3D hoàn chỉnh mà chỉ dưới dạng các tài nguyên lưới riêng lẻ để tải vào node MeshInstance3D (hoặc GPUParticles3D, CPUParticles3D, ...).

Để tạo LOD cho lưới của một tệp OBJ, hãy chọn tệp đó trong dock FileSystem, chuyển đến dock Import, thay đổi tùy chọn **Import As** thành **Scene**, sau đó nhấp vào **Reimport**:

.. figure:: img/mesh_lod_obj_import.png
   :align: center
   :alt: Thay đổi kiểu import trên một tệp OBJ trong dock Import

   Thay đổi kiểu import trên một tệp OBJ trong dock Import

Bạn sẽ cần khởi động lại trình chỉnh sửa sau khi nhấp vào **Reimport**.

.. note::

   Quá trình tạo LOD cho lưới không hoàn hảo và đôi khi có thể gây ra các vấn đề về kết xuất (đặc biệt là với các lưới có skin). Việc tạo LOD cho lưới cũng có thể mất một khoảng thời gian đối với các lưới phức tạp.

   Nếu LOD của lưới khiến một lưới cụ thể hiển thị bị lỗi, bạn có thể tắt việc tạo LOD cho lưới đó trong dock Import. Thao tác này cũng sẽ tăng tốc độ import tài nguyên. Bạn có thể thực hiện việc này trên toàn cục trong các tùy chọn import của cảnh 3D hoặc cho từng lưới bằng hộp thoại Advanced Import Settings.

   Xem :ref:`Importing 3D scenes <doc_importing_3d_scenes_using_the_import_dock>` để biết thêm thông tin.

So sánh hình ảnh và hiệu năng của LOD lưới
------------------------------------------

Để tắt LOD của lưới trong trình chỉnh sửa nhằm mục đích so sánh, hãy sử dụng chế độ vẽ gỡ lỗi nâng cao **Disable Mesh LOD**. Bạn có thể thực hiện việc này bằng menu ở góc trên bên trái của khung nhìn 3D (có nhãn **Perspective** hoặc **Orthogonal** tùy theo chế độ camera):

.. figure:: img/mesh_lod_disable_lod.png
   :align: center
   :alt: Tắt LOD của lưới trong menu ở góc trên bên trái của khung nhìn 3D

   Tắt LOD của lưới trong menu ở góc trên bên trái của khung nhìn 3D

Bật **View Frame Time** trong cùng menu để xem FPS ở góc trên bên phải. Đồng thời bật **View Information** trong cùng menu để xem số primitive (vertex + index) được kết xuất ở góc dưới bên phải.

Nếu LOD của lưới hoạt động chính xác trong cảnh và camera đủ xa lưới, bạn sẽ nhận thấy số primitive được vẽ giảm xuống và FPS tăng lên khi LOD của lưới được bật (trừ khi bạn bị giới hạn bởi CPU).

Để xem quá trình giảm số đa giác của LOD lưới trong thực tế, hãy đổi chế độ vẽ gỡ lỗi thành **Display Wireframe** trong menu được nêu ở trên, sau đó điều chỉnh thiết lập dự án **Rendering > Mesh LOD > LOD Change > Threshold Pixels**.

Cấu hình hiệu năng và chất lượng của LOD lưới
---------------------------------------------

Bạn có thể điều chỉnh mức độ mạnh của các chuyển đổi LOD lưới trong viewport gốc bằng cách thay đổi thiết lập dự án **Rendering > Mesh LOD > LOD Change > Threshold Pixels**. Để thay đổi giá trị này trong runtime, hãy đặt ``mesh_lod_threshold`` trên viewport gốc như sau:

.. tabs::
 .. code-tab:: gdscript

    get_tree().root.mesh_lod_threshold = 4.0

 .. code-tab:: csharp

    GetTree().Root.MeshLodThreshold = 4.0f;

Mỗi viewport có thuộc tính ``mesh_lod_threshold`` riêng, có thể được thiết lập độc lập với các viewport khác.

Ngưỡng LOD lưới mặc định là 1 pixel được tinh chỉnh để trông *perceptually* không suy giảm chất lượng; ngưỡng này mang lại mức tăng hiệu năng đáng kể mà không làm giảm chất lượng một cách dễ nhận thấy. Giá trị cao hơn sẽ khiến các chuyển đổi LOD xảy ra sớm hơn khi camera di chuyển ra xa, mang lại hiệu năng cao hơn nhưng chất lượng thấp hơn.

Nếu cần điều chỉnh mesh LOD theo từng đối tượng, bạn có thể điều chỉnh mức độ mạnh của các chuyển đổi LOD bằng cách điều chỉnh thuộc tính **LOD Bias** trên bất kỳ node nào kế thừa từ GeometryInstance3D. Các giá trị *trên* ``1.0`` sẽ khiến các chuyển đổi LOD diễn ra muộn hơn bình thường (cho chất lượng cao hơn nhưng hiệu suất thấp hơn). Các giá trị *dưới* ``1.0`` sẽ khiến các chuyển đổi LOD diễn ra sớm hơn bình thường (cho chất lượng thấp hơn nhưng hiệu suất cao hơn).

Ngoài ra, các node ReflectionProbe có thuộc tính **Mesh LOD Threshold** riêng, có thể được điều chỉnh để cải thiện hiệu suất kết xuất khi reflection probe cập nhật. Điều này đặc biệt quan trọng đối với các ReflectionProbe sử dụng chế độ cập nhật **Always**.

.. note::

    Khi kết xuất cảnh, việc chọn mesh LOD sử dụng một chỉ số trong không gian màn hình. Điều này có nghĩa là chỉ số này tự động tính đến trường nhìn của camera và độ phân giải viewport. FOV camera cao hơn và độ phân giải viewport thấp hơn sẽ khiến việc chọn LOD trở nên mạnh hơn; engine sẽ hiển thị các model bị giản lược nhiều sớm hơn khi camera di chuyển ra xa.

    Do đó, không giống như :ref:`doc_visibility_ranges`, bạn không cần thực hiện thao tác cụ thể nào trong project để tính đến FOV camera và độ phân giải viewport.

Sử dụng mesh LOD với MultiMesh và particle
------------------------------------------

Để chọn LOD, điểm trên :abbr:`AABB (Axis-Aligned Bounding Box)` của node gần camera nhất sẽ được dùng làm cơ sở. Điều này áp dụng cho mọi loại mesh LOD (bao gồm cả LOD cho từng MeshInstance3D riêng lẻ), nhưng có một số hệ quả đối với các node hiển thị nhiều mesh cùng lúc, chẳng hạn như MultiMeshInstance3D, CPUParticles3D và GPUParticles3D. Quan trọng nhất là điều này có nghĩa tất cả các instance sẽ được vẽ với cùng một cấp độ LOD tại một thời điểm nhất định.

Nếu nhận thấy việc chọn LOD không chính xác với GPUParticles3D, hãy đảm bảo AABB hiển thị của node được cấu hình bằng cách chọn node GPUParticles3D và sử dụng **GPUParticles3D > Generate AABB** ở phía trên viewport 3D.

Nếu có các instance trong một MultiMesh nằm cách xa nhau, bạn nên đặt chúng trong một node MultiMeshInstance3D riêng. Làm vậy cũng sẽ cải thiện hiệu suất kết xuất, vì việc loại bỏ theo frustum và occlusion có thể loại bỏ từng node riêng lẻ (trong khi không thể loại bỏ từng instance riêng lẻ trong một MultiMesh).
