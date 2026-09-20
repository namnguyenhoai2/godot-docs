:allow_comments: False

.. _doc_procedural_geometry:

Hình học thủ tục
================

Có nhiều cách để tạo hình học thủ tục trong Godot. Trong loạt hướng dẫn này, chúng ta sẽ tìm hiểu một vài cách trong số đó. Mỗi kỹ thuật đều có ưu điểm và nhược điểm riêng, vì vậy tốt nhất là hiểu từng kỹ thuật cũng như cách chúng có thể hữu ích trong một tình huống cụ thể.

.. toctree::
   :maxdepth: 1
   :name: toc-procedural_geometry

   arraymesh
   meshdatatool
   surfacetool
   immediatemesh

.. note::

      Tất cả các phương pháp tạo hình học thủ tục được mô tả ở đây đều chạy trên CPU. Godot hiện chưa hỗ trợ tạo hình học trên GPU.

Hình học là gì?
---------------

Geometry là một cách nói hoa mỹ để chỉ hình dạng. Trong đồ họa máy tính, hình học thường được biểu diễn bằng một mảng các vị trí gọi là "vertices". Trong Godot, hình học được biểu diễn bằng Mesh.

Mesh là gì?
-----------

Nhiều thành phần trong Godot có từ mesh trong tên: :ref:`Mesh <class_Mesh>`,
:ref:`ArrayMesh <class_ArrayMesh>`, the :ref:`ImmediateMesh
<class_ImmediateMesh>`, :ref:`MeshInstance3D <class_MeshInstance3D>`, và
:ref:`MultiMesh <class_MultiMesh>`, and the :ref:`MultiMeshInstance3D
<class_MultiMeshInstance3D>`. Mặc dù đều có liên quan với nhau, chúng có công dụng hơi khác nhau.

Mesh và ArrayMesh là các resource được vẽ bằng node MeshInstance3D. Các resource như Mesh và ArrayMesh không thể được thêm trực tiếp vào scene. Một MeshInstance3D đại diện cho một instance của mesh trong scene. Bạn có thể tái sử dụng một mesh duy nhất trong nhiều MeshInstance3D để vẽ nó ở các phần khác nhau trong scene với các material hoặc phép biến đổi khác nhau (scale, rotation, position, v.v.).

Nếu bạn định vẽ cùng một object nhiều lần, việc sử dụng MultiMesh cùng với MultiMeshInstance3D có thể rất hữu ích. MultiMeshInstance3D vẽ mesh hàng nghìn lần với chi phí rất thấp nhờ tận dụng hardware instancing. Nhược điểm khi sử dụng MultiMeshInstance3D là mỗi surface của mesh chỉ bị giới hạn ở một material cho tất cả các instance. Nó sử dụng một instance array để lưu trữ các màu sắc và phép biến đổi khác nhau cho từng instance, nhưng tất cả instance của mỗi surface đều sử dụng cùng một material.

Mesh là gì
----------

Một Mesh bao gồm một hoặc nhiều surface. Một surface là một array gồm nhiều sub-array chứa vertices, normals, UV, v.v. Thông thường, quá trình xây dựng surface và mesh được ẩn khỏi người dùng trong :ref:`RenderingServer <class_RenderingServer>`, nhưng với ArrayMesh, người dùng có thể tự xây dựng một Mesh bằng cách truyền vào một array chứa thông tin về surface.

Surface
~~~~~~~

Mỗi surface có material riêng. Ngoài ra, bạn có thể override material cho tất cả surface trong Mesh khi sử dụng MeshInstance3D bằng thuộc tính :ref:`material_override <class_GeometryInstance3D_property_material_override>`.

Surface array
~~~~~~~~~~~~~

Surface array là một array có độ dài ``ArrayMesh.ARRAY_MAX``. Mỗi vị trí trong array được điền bằng một sub-array chứa thông tin theo từng vertex. Ví dụ, array nằm tại ``ArrayMesh.ARRAY_NORMAL`` là một :ref:`PackedVector3Array <class_PackedVector3Array>` của các normal của vertex. Xem :ref:`Mesh.ArrayType <enum_Mesh_ArrayType>` để biết thêm thông tin.

Surface array có thể là indexed hoặc non-indexed. Việc tạo một array non-indexed đơn giản chỉ là không gán array tại index ``ArrayMesh.ARRAY_INDEX``. Array non-indexed lưu thông tin vertex duy nhất cho mỗi triangle, nghĩa là khi hai triangle dùng chung một vertex, vertex đó sẽ bị nhân đôi trong array. Surface array indexed chỉ lưu thông tin vertex cho mỗi vertex duy nhất, sau đó cũng lưu một array các index để ánh xạ cách xây dựng các triangle từ vertex array. Nhìn chung, sử dụng array indexed nhanh hơn, nhưng điều đó có nghĩa là bạn phải dùng chung dữ liệu vertex giữa các triangle, việc này không phải lúc nào cũng mong muốn (ví dụ: khi bạn muốn có normal theo từng mặt).

Công cụ
-------

Godot cung cấp nhiều cách khác nhau để truy cập và làm việc với hình học. Thông tin chi tiết hơn về từng cách sẽ được cung cấp trong các hướng dẫn tiếp theo.

ArrayMesh
~~~~~~~~~

Resource ArrayMesh mở rộng Mesh để bổ sung một số hàm cải thiện chất lượng sử dụng và, quan trọng nhất, khả năng xây dựng một surface Mesh thông qua scripting.

Để biết thêm thông tin về ArrayMesh, vui lòng xem :ref:`ArrayMesh tutorial <doc_arraymesh>`.

MeshDataTool
~~~~~~~~~~~~

MeshDataTool là một resource chuyển đổi dữ liệu Mesh thành các array của vertices, faces và edges, có thể được sửa đổi tại runtime.

Để biết thêm thông tin về MeshDataTool, vui lòng xem :ref:`MeshDataTool tutorial <doc_meshdatatool>`.

SurfaceTool
~~~~~~~~~~~

SurfaceTool cho phép tạo Mesh bằng một interface theo phong cách immediate mode của OpenGL 1.x.

Để biết thêm thông tin về SurfaceTool, vui lòng xem :ref:`SurfaceTool tutorial <doc_surfacetool>`.

ImmediateMesh
~~~~~~~~~~~~~

ImmediateMesh là một mesh sử dụng interface theo phong cách immediate mode (giống SurfaceTool) để vẽ các object. Điểm khác biệt giữa ImmediateMesh và SurfaceTool là ImmediateMesh được vẽ trực tiếp bằng code một cách động, trong khi SurfaceTool được dùng để tạo một Mesh mà bạn có thể tùy ý sử dụng.

ImmediateMesh hữu ích cho việc tạo prototype nhờ API đơn giản, nhưng chậm vì hình học được xây dựng lại mỗi khi bạn thực hiện thay đổi. Nó hữu ích nhất để thêm hình học đơn giản cho việc debug trực quan (ví dụ: bằng cách vẽ các đường để trực quan hóa raycast vật lý, v.v.).

Để biết thêm thông tin về ImmediateMesh, vui lòng xem :ref:`ImmediateMesh tutorial <doc_immediatemesh>`.

Nên sử dụng cái nào?
--------------------

Cách tiếp cận bạn sử dụng phụ thuộc vào mục tiêu bạn đang cố gắng thực hiện và loại quy trình mà bạn cảm thấy quen thuộc.

Cả SurfaceTool và ArrayMesh đều rất phù hợp để tạo hình học tĩnh (mesh) không thay đổi theo thời gian.

Sử dụng ArrayMesh nhanh hơn một chút so với SurfaceTool, nhưng API khó sử dụng hơn một chút. Ngoài ra, SurfaceTool có một số method cải thiện chất lượng sử dụng như ``generate_normals()`` và ``index()``.

ImmediateMesh bị giới hạn hơn cả ArrayMesh lẫn SurfaceTool. Tuy nhiên, nếu bạn cần hình học thay đổi ở mỗi frame, nó cung cấp một interface dễ sử dụng hơn nhiều và có thể nhanh hơn một chút so với việc tạo ArrayMesh ở mỗi frame.

MeshDataTool không nhanh, nhưng cho phép bạn truy cập vào đủ loại thuộc tính của mesh mà bạn không có được với các công cụ khác (edges, faces, v.v.). Nó cực kỳ hữu ích khi bạn cần loại dữ liệu đó để biến đổi mesh, nhưng không nên sử dụng nếu không cần đến thông tin bổ sung này. MeshDataTool phù hợp nhất khi bạn định sử dụng một algorithm yêu cầu quyền truy cập vào face array hoặc edge array.
