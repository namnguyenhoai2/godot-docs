:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationMeshGenerator.xml.

.. _class_NavigationMeshGenerator:

NavigationMeshGenerator
=======================

**Đã lỗi thời:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Object<class_Object>`

Lớp trợ giúp để tạo và xóa navigation mesh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này chịu trách nhiệm tạo và xóa navigation mesh 3D được sử dụng làm tài nguyên :ref:`NavigationMesh<class_NavigationMesh>` bên trong :ref:`NavigationRegion3D<class_NavigationRegion3D>`. **NavigationMeshGenerator** có rất ít hoặc không có tác dụng cho 2D vì quy trình baking navigation mesh yêu cầu các loại node 3D và hình học nguồn 3D để phân tích.

Toàn bộ quy trình baking navigation mesh tốt nhất nên được thực hiện trong một thread riêng vì các bước voxelization, kiểm tra va chạm và tối ưu mesh liên quan đều rất chậm và tiêu tốn nhiều tài nguyên.

Quy trình baking navigation mesh diễn ra qua nhiều bước và kết quả phụ thuộc vào hình học nguồn 3D cũng như các thuộc tính của tài nguyên :ref:`NavigationMesh<class_NavigationMesh>`. Ở bước đầu tiên, bắt đầu từ một node gốc và tùy thuộc vào các thuộc tính :ref:`NavigationMesh<class_NavigationMesh>`, tất cả node hình học nguồn 3D hợp lệ sẽ được thu thập từ :ref:`SceneTree<class_SceneTree>`. Tiếp theo, tất cả node đã thu thập được phân tích để lấy dữ liệu hình học 3D liên quan và một mesh 3D tổng hợp được tạo ra. Do có nhiều loại đối tượng khác nhau có thể phân tích, từ các :ref:`MeshInstance3D<class_MeshInstance3D>`\ s thông thường đến các :ref:`CSGShape3D<class_CSGShape3D>`\ s hoặc nhiều loại :ref:`CollisionObject3D<class_CollisionObject3D>`\ s khác nhau, một số thao tác thu thập dữ liệu hình học có thể kích hoạt quá trình đồng bộ hóa :ref:`RenderingServer<class_RenderingServer>` và :ref:`PhysicsServer3D<class_PhysicsServer3D>`. Việc đồng bộ hóa Server có thể ảnh hưởng tiêu cực đến thời gian baking hoặc framerate vì thường liên quan đến việc khóa :ref:`Mutex<class_Mutex>` để đảm bảo an toàn cho thread. Nhiều đối tượng có thể phân tích và việc đồng bộ hóa liên tục với các Server chạy trong các thread khác có thể làm tăng đáng kể thời gian baking. Mặt khác, chỉ một vài đối tượng nhưng rất lớn và phức tạp sẽ cần thời gian để chuẩn bị cho các Server, điều này có thể khiến quá trình render frame tiếp theo bị đình trệ rõ rệt. Theo nguyên tắc chung, cần cân bằng tổng số đối tượng có thể phân tích với kích thước và độ phức tạp riêng của chúng để tránh vấn đề về framerate hoặc thời gian baking quá dài. Sau đó, mesh tổng hợp được chuyển đến Recast Navigation Object để kiểm tra hình học nguồn nhằm xác định địa hình có thể đi được, phù hợp với các thuộc tính của agent :ref:`NavigationMesh<class_NavigationMesh>`, bằng cách tạo một thế giới voxel xung quanh vùng giới hạn của các mesh.

Sau đó, navigation mesh hoàn thiện được trả về và lưu bên trong :ref:`NavigationMesh<class_NavigationMesh>` để sử dụng làm tài nguyên bên trong các node :ref:`NavigationRegion3D<class_NavigationRegion3D>`.

\ **Lưu ý:** Việc sử dụng mesh không chỉ để xác định các bề mặt có thể đi được mà còn để cản trở quá trình baking navigation không phải lúc nào cũng hiệu quả. Khi xử lý hình học nguồn dạng mesh, quy trình baking navigation không có khái niệm về việc một hình học nằm "bên trong" là gì, và đây là chủ ý. Tùy thuộc vào các tham số baking hiện tại, ngay khi mesh cản trở đủ lớn để chứa vừa một vùng navigation mesh bên trong, quy trình baking sẽ tạo ra các vùng navigation mesh nằm bên trong mesh hình học nguồn cản trở đó.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationMeshes <../tutorials/navigation/navigation_using_navigationmeshes>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`bake<class_NavigationMeshGenerator_method_bake>`\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, root_node\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                                  |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`bake_from_source_geometry_data<class_NavigationMeshGenerator_method_bake_from_source_geometry_data>`\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, source_geometry_data\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`, callback\: :ref:`Callable<class_Callable>` = Callable()\ )                              |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`clear<class_NavigationMeshGenerator_method_clear>`\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`\ )                                                                                                                                                                                                                                                     |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`parse_source_geometry_data<class_NavigationMeshGenerator_method_parse_source_geometry_data>`\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, source_geometry_data\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`, root_node\: :ref:`Node<class_Node>`, callback\: :ref:`Callable<class_Callable>` = Callable()\ ) |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationMeshGenerator_method_bake:

.. rst-class:: classref-method

|void| **bake**\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, root_node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_NavigationMeshGenerator_method_bake>`

**Đã lỗi thời:** Phương thức này đã lỗi thời do các thay đổi về threading trong core. Để nâng cấp mã hiện có, trước tiên hãy tạo một tài nguyên :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`. Sử dụng tài nguyên này với :ref:`parse_source_geometry_data()<class_NavigationMeshGenerator_method_parse_source_geometry_data>` để phân tích :ref:`SceneTree<class_SceneTree>` nhằm tìm các node sẽ đóng góp vào quá trình baking navigation mesh. Việc phân tích :ref:`SceneTree<class_SceneTree>` phải được thực hiện trên main thread. Sau khi hoàn tất phân tích, hãy sử dụng tài nguyên này với :ref:`bake_from_source_geometry_data()<class_NavigationMeshGenerator_method_bake_from_source_geometry_data>` để bake navigation mesh.

Bake ``navigation_mesh`` với hình học nguồn được thu thập bắt đầu từ ``root_node``.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshGenerator_method_bake_from_source_geometry_data:

.. rst-class:: classref-method

|void| **bake_from_source_geometry_data**\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, source_geometry_data\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`, callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_NavigationMeshGenerator_method_bake_from_source_geometry_data>`

Bake ``navigation_mesh`` được cung cấp với dữ liệu từ ``source_geometry_data`` được cung cấp. Sau khi quá trình hoàn tất, ``callback`` tùy chọn sẽ được gọi.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshGenerator_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`\ ) :ref:`🔗<class_NavigationMeshGenerator_method_clear>`

Xóa tất cả polygon và vertex khỏi tài nguyên ``navigation_mesh`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshGenerator_method_parse_source_geometry_data:

.. rst-class:: classref-method

|void| **parse_source_geometry_data**\ (\ navigation_mesh\: :ref:`NavigationMesh<class_NavigationMesh>`, source_geometry_data\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`, root_node\: :ref:`Node<class_Node>`, callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_NavigationMeshGenerator_method_parse_source_geometry_data>`

Phân tích :ref:`SceneTree<class_SceneTree>` để lấy hình học nguồn theo các thuộc tính của ``navigation_mesh``. Cập nhật tài nguyên ``source_geometry_data`` được cung cấp bằng dữ liệu thu được. Sau đó, tài nguyên này có thể được dùng để bake navigation mesh với :ref:`bake_from_source_geometry_data()<class_NavigationMeshGenerator_method_bake_from_source_geometry_data>`. Sau khi quá trình hoàn tất, ``callback`` tùy chọn sẽ được gọi.

\ **Lưu ý:** Hàm này cần chạy trên main thread hoặc bằng một deferred call vì SceneTree không an toàn cho thread.

\ **Hiệu năng:** Mặc dù thuận tiện, việc đọc các mảng dữ liệu từ tài nguyên :ref:`Mesh<class_Mesh>` có thể ảnh hưởng tiêu cực đến framerate. Dữ liệu cần được nhận từ GPU, khiến :ref:`RenderingServer<class_RenderingServer>` bị đình trệ trong quá trình này. Để đạt hiệu năng tốt hơn, hãy ưu tiên sử dụng, chẳng hạn, các collision shape hoặc tạo hoàn toàn các mảng dữ liệu trong code.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
