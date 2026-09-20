.. _doc_mesh_lod:

Mức độ chi tiết của mesh (LOD)
==============================

Mức độ chi tiết (LOD) là một trong những cách quan trọng nhất để tối ưu hiệu suất rendering trong một dự án 3D, cùng với :ref:`doc_occlusion_culling`.

Trong trang này, bạn sẽ tìm hiểu:

- Mesh LOD có thể cải thiện hiệu suất rendering của dự án 3D như thế nào. - Cách thiết lập mesh LOD trong Godot. - Cách đo lường hiệu quả của mesh LOD trong dự án của bạn (và các phương án thay thế bạn có thể thử nếu kết quả không như mong đợi).

.. seealso::

    Bạn có thể xem mesh LOD hoạt động như thế nào qua `dự án demo Occlusion Culling và Mesh LOD <https://github.com/godotengine/godot-demo-projects/tree/master/3d/occlusion_culling_mesh_lod>`__.

Giới thiệu
----------

Trước đây, level of detail trong game 3D thường liên quan đến việc tự tạo các mesh có mật độ hình học thấp hơn, sau đó cấu hình các ngưỡng khoảng cách tại đó những mesh có ít chi tiết hơn này sẽ được vẽ. Cách tiếp cận này vẫn được sử dụng ngày nay khi cần khả năng kiểm soát cao hơn.

Tuy nhiên, trong các dự án có một lượng lớn asset 3D chi tiết, việc thiết lập LOD thủ công có thể tốn rất nhiều thời gian. Do đó, việc tự động decimation mesh và cấu hình LOD ngày càng trở nên phổ biến.

Godot cung cấp cách tự động tạo các mesh ít chi tiết hơn để sử dụng cho LOD trong quá trình import, sau đó tự động sử dụng các mesh LOD này khi cần. Quy trình này hoàn toàn trong suốt đối với người dùng. Thư viện `meshoptimizer <https://meshoptimizer.org/>`__ được sử dụng để tạo mesh LOD ở phía sau.

Mesh LOD hoạt động với mọi node vẽ mesh 3D. Điều này bao gồm MeshInstance3D, MultiMeshInstance3D, GPUParticles3D và CPUParticles3D.

So sánh trực quan
-----------------

Dưới đây là ví dụ về các mesh LOD được tạo trong quá trình import. Các mesh ít chi tiết hơn sẽ được sử dụng khi camera ở xa object:

.. figure:: img/mesh_lod_comparison_shaded.png
   :align: center
   :alt: From most detailed (left) to least detailed (right), shaded view

   From most detailed (left) to least detailed (right), shaded view

Đây là cùng hình ảnh đó với rendering dạng wireframe để dễ nhìn thấy quá trình decimation hơn:

.. figure:: img/mesh_lod_comparison_wireframe.png
   :align: center
   :alt: From most detailed (left) to least detailed (right), wireframe view

   From most detailed (left) to least detailed (right), wireframe view

.. seealso::

    Nếu cần tự cấu hình level of detail bằng các mesh do artist tạo, hãy sử dụng :ref:`doc_visibility_ranges` thay vì mesh LOD tự động.

Tạo mesh LOD
------------

Theo mặc định, quá trình tạo mesh LOD diễn ra tự động đối với các scene 3D được import (glTF, .blend, Collada, FBX). Sau khi các mesh LOD được tạo, chúng sẽ tự động được sử dụng khi rendering scene. Bạn không cần cấu hình thủ công bất kỳ thứ gì.

Tuy nhiên, quá trình tạo mesh LOD **không** tự động diễn ra đối với các mesh 3D được import (OBJ). Điều này là vì theo mặc định, các file OBJ không được import dưới dạng scene 3D đầy đủ, mà chỉ được import dưới dạng các resource mesh riêng lẻ để load vào một node MeshInstance3D (hoặc GPUParticles3D, CPUParticles3D, ...).

Để tạo mesh LOD cho một file OBJ, hãy chọn file đó trong dock FileSystem, đi đến dock Import, thay đổi tùy chọn **Import As** thành **Scene**, sau đó nhấp vào **Reimport**:

.. figure:: img/mesh_lod_obj_import.png
   :align: center
   :alt: Changing the import type on an OBJ file in the Import dock

   Changing the import type on an OBJ file in the Import dock

Bạn sẽ cần khởi động lại editor sau khi nhấp vào **Reimport**.

.. note::

   Quá trình tạo mesh LOD không hoàn hảo và đôi khi có thể gây ra các vấn đề về rendering (đặc biệt là với skinned mesh). Việc tạo mesh LOD cũng có thể mất một khoảng thời gian đối với các mesh phức tạp.

   Nếu mesh LOD khiến một mesh cụ thể trông bị lỗi, bạn có thể tắt việc tạo LOD cho mesh đó trong dock Import. Điều này cũng sẽ tăng tốc quá trình import resource. Bạn có thể thực hiện việc này trên toàn cục trong các tùy chọn import của scene 3D hoặc trên từng mesh bằng hộp thoại Advanced Import Settings.

   Xem :ref:`Importing 3D scenes <doc_importing_3d_scenes_using_the_import_dock>` để biết thêm thông tin.

So sánh hình ảnh và hiệu suất của mesh LOD
------------------------------------------

Để tắt mesh LOD trong editor nhằm mục đích so sánh, hãy sử dụng chế độ advanced debug draw **Disable Mesh LOD**. Bạn có thể thực hiện việc này bằng menu ở góc trên bên trái của viewport 3D (được gắn nhãn **Perspective** hoặc **Orthogonal** tùy theo chế độ camera):

.. figure:: img/mesh_lod_disable_lod.png
   :align: center
   :alt: Disabling mesh LOD in the 3D viewport's top-left menu

   Disabling mesh LOD in the 3D viewport's top-left menu

Bật **View Frame Time** trong cùng menu để xem FPS ở góc trên bên phải. Đồng thời bật **View Information** trong cùng menu để xem số primitive (vertex + index) được rendering ở góc dưới bên phải.

Nếu mesh LOD hoạt động đúng trong scene của bạn và camera đủ xa mesh, bạn sẽ nhận thấy số primitive được vẽ giảm xuống và FPS tăng lên khi mesh LOD được bật (trừ khi bạn bị giới hạn bởi CPU).

Để xem quá trình decimation của mesh LOD hoạt động, hãy thay đổi chế độ debug draw thành **Display Wireframe** trong menu được chỉ định ở trên, sau đó điều chỉnh project setting **Rendering > Mesh LOD > LOD Change > Threshold Pixels**.

Cấu hình hiệu suất và chất lượng của mesh LOD
---------------------------------------------

Bạn có thể điều chỉnh mức độ mạnh của các chuyển đổi mesh LOD trong viewport gốc bằng cách thay đổi project setting **Rendering > Mesh LOD > LOD Change > Threshold Pixels**. Để thay đổi giá trị này tại runtime, hãy đặt ``mesh_lod_threshold`` trên viewport gốc như sau:

.. tabs::
 .. code-tab:: gdscript

    get_tree().root.mesh_lod_threshold = 4.0

 .. code-tab:: csharp

    GetTree().Root.MeshLodThreshold = 4.0f;

Mỗi viewport có thuộc tính ``mesh_lod_threshold`` riêng, có thể được thiết lập độc lập với các viewport khác.

Ngưỡng mesh LOD mặc định là 1 pixel được điều chỉnh để không thể nhận thấy sự suy giảm về mặt *perceptual*; nó mang lại mức tăng hiệu suất đáng kể mà không làm giảm chất lượng một cách dễ nhận thấy. Các giá trị cao hơn sẽ khiến chuyển đổi LOD diễn ra sớm hơn khi camera di chuyển ra xa, mang lại hiệu suất cao hơn nhưng chất lượng thấp hơn.

Nếu cần điều chỉnh mesh LOD theo từng object, bạn có thể điều chỉnh mức độ mạnh của các chuyển đổi LOD bằng cách điều chỉnh thuộc tính **LOD Bias** trên bất kỳ node nào kế thừa từ GeometryInstance3D. Các giá trị *lớn hơn* ``1.0`` sẽ khiến chuyển đổi LOD diễn ra muộn hơn bình thường (mang lại chất lượng cao hơn nhưng hiệu suất thấp hơn). Các giá trị *nhỏ hơn* ``1.0`` sẽ khiến chuyển đổi LOD diễn ra sớm hơn bình thường (mang lại chất lượng thấp hơn nhưng hiệu suất cao hơn).

Ngoài ra, các node ReflectionProbe có thuộc tính **Mesh LOD Threshold** riêng, có thể được điều chỉnh để cải thiện hiệu suất rendering khi reflection probe được cập nhật. Điều này đặc biệt quan trọng đối với các ReflectionProbe sử dụng chế độ cập nhật **Always**.

.. note::

    Khi rendering scene, việc chọn mesh LOD sử dụng một metric trong không gian màn hình. Điều này có nghĩa là nó tự động tính đến field of view của camera và độ phân giải viewport. FOV camera cao hơn và độ phân giải viewport thấp hơn sẽ khiến việc chọn LOD mạnh hơn; engine sẽ hiển thị các model bị decimation nhiều hơn sớm hơn khi camera di chuyển ra xa.

    Do đó, không giống như :ref:`doc_visibility_ranges`, bạn không cần thực hiện bất kỳ thao tác cụ thể nào trong dự án để tính đến FOV camera và độ phân giải viewport.

Sử dụng mesh LOD với MultiMesh và particles
-------------------------------------------

Để chọn LOD, điểm trên :abbr:`AABB (Axis-Aligned Bounding Box)` của node gần camera nhất sẽ được dùng làm cơ sở. Điều này áp dụng cho mọi loại mesh LOD (bao gồm cả các MeshInstance3D riêng lẻ), nhưng có một số hệ quả đối với các node hiển thị nhiều mesh cùng lúc, chẳng hạn như MultiMeshInstance3D, CPUParticles3D và GPUParticles3D. Quan trọng nhất là điều này có nghĩa tất cả instance sẽ được vẽ với cùng một mức LOD tại một thời điểm.

Nếu nhận thấy việc chọn LOD không chính xác với GPUParticles3D, hãy đảm bảo visibility AABB của node đã được cấu hình bằng cách chọn node GPUParticles3D và sử dụng **GPUParticles3D > Generate AABB** ở đầu viewport 3D.

Nếu các instance trong một MultiMesh nằm cách xa nhau, chúng nên được đặt trong một node MultiMeshInstance3D riêng. Làm như vậy cũng sẽ cải thiện hiệu suất rendering, vì frustum culling và occlusion culling có thể cull từng node riêng lẻ (trong khi chúng không thể cull từng instance riêng lẻ trong một MultiMesh).
