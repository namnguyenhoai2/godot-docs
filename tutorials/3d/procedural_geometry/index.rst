:allow_comments: False

.. _doc_procedural_geometry:

Hình học thủ tục
================

Có nhiều cách để tạo hình học theo thủ tục trong Godot. Trong loạt hướng dẫn này, chúng ta sẽ khám phá một vài cách trong số đó. Mỗi kỹ thuật đều có ưu điểm và nhược điểm riêng, vì vậy tốt nhất là hiểu từng kỹ thuật và cách nó có thể hữu ích trong một tình huống cụ thể.

.. toctree::
   :maxdepth: 1
   :name: toc-procedural_geometry

   arraymesh
   meshdatatool
   surfacetool
   immediatemesh

.. note::

      Tất cả các phương pháp tạo hình học theo thủ tục được mô tả ở đây đều chạy trên CPU. Godot hiện chưa hỗ trợ tạo hình học trên GPU.

Hình học là gì?
---------------

Geometry là một cách nói hoa mỹ về hình dạng. Trong đồ họa máy tính, geometry thường được biểu diễn bằng một mảng các vị trí gọi là "vertices". Trong Godot, geometry được biểu diễn bằng Mesh.

Mesh là gì?
-----------

Có nhiều thành phần trong Godot có từ mesh trong tên: :ref:`Mesh <class_Mesh>`,
:ref:`ArrayMesh <class_ArrayMesh>`, :ref:`ImmediateMesh <class_ImmediateMesh>`, :ref:`MeshInstance3D <class_MeshInstance3D>`,
:ref:`MultiMesh <class_MultiMesh>` và :ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>`. Mặc dù đều có liên quan với nhau, chúng có công dụng hơi khác nhau.

Meshes và ArrayMeshes là các resource được vẽ bằng node MeshInstance3D. Các resource như Meshes và ArrayMeshes không thể được thêm trực tiếp vào scene. Một MeshInstance3D đại diện cho một instance của mesh trong scene. Bạn có thể tái sử dụng một mesh duy nhất trong nhiều MeshInstance3D để vẽ nó ở các phần khác nhau của scene với các material hoặc phép biến đổi khác nhau (scale, rotation, position, v.v.).

Nếu bạn định vẽ cùng một đối tượng nhiều lần, việc sử dụng MultiMesh cùng với MultiMeshInstance3D có thể hữu ích. MultiMeshInstance3Ds vẽ mesh hàng nghìn lần với chi phí rất thấp bằng cách tận dụng hardware instancing. Nhược điểm khi sử dụng MultiMeshInstance3D là mỗi surface của mesh chỉ được giới hạn ở một material cho tất cả các instance. Nó sử dụng một instance array để lưu trữ các màu sắc và phép biến đổi khác nhau cho từng instance, nhưng tất cả instance của mỗi surface đều sử dụng cùng một material.

Mesh là gì
----------

Một Mesh được cấu thành từ một hoặc nhiều surface. Một surface là một mảng gồm nhiều mảng con chứa vertices, normals, UVs, v.v. Thông thường, quá trình tạo surface và mesh được ẩn khỏi người dùng trong :ref:`RenderingServer <class_RenderingServer>`, nhưng với ArrayMeshes, người dùng có thể tự tạo một Mesh bằng cách truyền vào một mảng chứa thông tin về surface.

Surfaces
~~~~~~~~

Mỗi surface có material riêng. Ngoài ra, bạn có thể ghi đè material cho tất cả surface trong Mesh khi sử dụng MeshInstance3D bằng thuộc tính :ref:`material_override <class_GeometryInstance3D_property_material_override>`.

Mảng surface
~~~~~~~~~~~~

Mảng surface là một mảng có độ dài ``ArrayMesh.ARRAY_MAX``. Mỗi vị trí trong mảng được điền bằng một mảng con chứa thông tin trên từng vertex. Ví dụ, mảng nằm tại ``ArrayMesh.ARRAY_NORMAL`` là một :ref:`PackedVector3Array <class_PackedVector3Array>` của các vertex normal. Xem :ref:`Mesh.ArrayType <enum_Mesh_ArrayType>` để biết thêm thông tin.

Mảng surface có thể được đánh index hoặc không đánh index. Việc tạo một mảng không đánh index đơn giản như không gán một mảng tại index ``ArrayMesh.ARRAY_INDEX``. Mảng không đánh index lưu thông tin vertex riêng biệt cho mỗi triangle, nghĩa là khi hai triangle dùng chung một vertex, vertex đó sẽ được nhân bản trong mảng. Mảng surface được đánh index chỉ lưu thông tin vertex cho mỗi vertex duy nhất, sau đó cũng lưu một mảng index ánh xạ cách tạo các triangle từ mảng vertex. Nhìn chung, sử dụng mảng được đánh index sẽ nhanh hơn, nhưng điều đó có nghĩa là bạn phải chia sẻ dữ liệu vertex giữa các triangle, điều này không phải lúc nào cũng mong muốn (ví dụ: khi bạn muốn có normal riêng cho từng mặt).

Công cụ
-------

Godot cung cấp nhiều cách khác nhau để truy cập và làm việc với geometry. Thông tin chi tiết hơn về từng cách sẽ được cung cấp trong các hướng dẫn tiếp theo.

ArrayMesh
~~~~~~~~~

Resource ArrayMesh mở rộng Mesh để bổ sung một số hàm cải thiện trải nghiệm sử dụng và, quan trọng nhất, khả năng tạo surface của Mesh thông qua scripting.

Để biết thêm thông tin về ArrayMesh, vui lòng xem :ref:`hướng dẫn ArrayMesh <doc_arraymesh>`.

MeshDataTool
~~~~~~~~~~~~

MeshDataTool là một resource chuyển đổi dữ liệu Mesh thành các mảng vertices, faces và edges có thể được chỉnh sửa tại runtime.

Để biết thêm thông tin về MeshDataTool, vui lòng xem :ref:`hướng dẫn MeshDataTool <doc_meshdatatool>`.

SurfaceTool
~~~~~~~~~~~

SurfaceTool cho phép tạo Mesh bằng interface theo phong cách immediate mode của OpenGL 1.x.

Để biết thêm thông tin về SurfaceTool, vui lòng xem :ref:`hướng dẫn SurfaceTool <doc_surfacetool>`.

ImmediateMesh
~~~~~~~~~~~~~

ImmediateMesh là một mesh sử dụng interface theo phong cách immediate mode (giống SurfaceTool) để vẽ các đối tượng. Điểm khác biệt giữa ImmediateMesh và SurfaceTool là ImmediateMesh được vẽ trực tiếp bằng code một cách dynamic, trong khi SurfaceTool được dùng để tạo một Mesh mà bạn có thể tùy ý sử dụng.

ImmediateMesh hữu ích cho việc tạo prototype nhờ API đơn giản, nhưng chậm vì geometry được xây dựng lại mỗi khi bạn thay đổi. Nó hữu ích nhất khi thêm geometry đơn giản để debug trực quan (ví dụ: vẽ các đường để trực quan hóa physics raycast, v.v.).

Để biết thêm thông tin về ImmediateMesh, vui lòng xem :ref:`hướng dẫn ImmediateMesh <doc_immediatemesh>`.

Tôi nên sử dụng cái nào?
------------------------

Cách tiếp cận bạn sử dụng phụ thuộc vào việc bạn đang cố gắng thực hiện điều gì và bạn cảm thấy thoải mái với loại quy trình nào.

Cả SurfaceTool và ArrayMesh đều rất phù hợp để tạo geometry tĩnh (mesh) không thay đổi theo thời gian.

Sử dụng ArrayMesh nhanh hơn một chút so với SurfaceTool, nhưng API khó hơn đôi chút. Ngoài ra, SurfaceTool có một số method cải thiện trải nghiệm sử dụng như ``generate_normals()`` và ``index()``.

ImmediateMesh có nhiều giới hạn hơn cả ArrayMesh lẫn SurfaceTool. Tuy nhiên, nếu geometry của bạn vốn cần thay đổi sau mỗi frame, nó cung cấp một interface dễ sử dụng hơn nhiều và có thể nhanh hơn một chút so với việc tạo ArrayMesh ở mỗi frame.

MeshDataTool không nhanh, nhưng cho phép bạn truy cập mọi loại thuộc tính của mesh mà các công cụ khác không cung cấp (edges, faces, v.v.). Nó cực kỳ hữu ích khi bạn cần loại dữ liệu đó để biến đổi mesh, nhưng không nên sử dụng nếu không cần thông tin bổ sung này. MeshDataTool phù hợp nhất khi bạn định sử dụng một algorithm yêu cầu quyền truy cập vào mảng face hoặc edge.
