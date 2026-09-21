:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationObstacle3D.xml.

.. _class_NavigationObstacle3D:

NavigationObstacle3D
====================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Obstacle 3D được dùng để ảnh hưởng đến việc baking navigation mesh hoặc giới hạn velocity của các agent được điều khiển bởi avoidance.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một obstacle cần có navigation map và outline :ref:`vertices<class_NavigationObstacle3D_property_vertices>` được định nghĩa để hoạt động chính xác. Các outline không được giao nhau hoặc chồng lấp, đồng thời bị giới hạn trong một phép chiếu lên mặt phẳng. Điều này có nghĩa là trục y của các vertex bị bỏ qua; thay vào đó, vị trí global trên trục y của obstacle được dùng để đặt obstacle. Shape được chiếu sẽ được kéo dài theo chiều cao của obstacle dọc theo trục y.

Obstacles có thể được đưa vào quá trình baking navigation mesh khi :ref:`affect_navigation_mesh<class_NavigationObstacle3D_property_affect_navigation_mesh>` được bật. Chúng không thêm geometry có thể đi được; thay vào đó, vai trò của chúng là loại bỏ geometry nguồn nằm bên trong shape. Điều này có thể được dùng để ngăn navigation mesh xuất hiện ở những vị trí không mong muốn, ví dụ như bên trong geometry "solid" hoặc bên trên geometry đó. Nếu :ref:`carve_navigation_mesh<class_NavigationObstacle3D_property_carve_navigation_mesh>` được bật, shape đã bake sẽ không bị ảnh hưởng bởi các offset của quá trình baking navigation mesh, ví dụ như agent radius.

Với :ref:`avoidance_enabled<class_NavigationObstacle3D_property_avoidance_enabled>`, obstacle có thể giới hạn velocity avoidance của các agent sử dụng avoidance. Nếu các vertex của obstacle được sắp theo thứ tự chiều kim đồng hồ, các agent avoidance sẽ bị obstacle đẩy vào trong; nếu không, các agent avoidance sẽ bị đẩy ra ngoài. Obstacles sử dụng vertex và avoidance có thể warp đến vị trí mới, nhưng không nên được di chuyển trong từng frame vì mỗi thay đổi đều yêu cầu xây dựng lại avoidance map.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Sử dụng NavigationObstacles <../tutorials/navigation/navigation_using_navigationobstacles>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`affect_navigation_mesh<class_NavigationObstacle3D_property_affect_navigation_mesh>` | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`avoidance_enabled<class_NavigationObstacle3D_property_avoidance_enabled>`           | ``true``                 |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                               | :ref:`avoidance_layers<class_NavigationObstacle3D_property_avoidance_layers>`             | ``1``                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`carve_navigation_mesh<class_NavigationObstacle3D_property_carve_navigation_mesh>`   | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`height<class_NavigationObstacle3D_property_height>`                                 | ``1.0``                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`radius<class_NavigationObstacle3D_property_radius>`                                 | ``0.0``                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`use_3d_avoidance<class_NavigationObstacle3D_property_use_3d_avoidance>`             | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`velocity<class_NavigationObstacle3D_property_velocity>`                             | ``Vector3(0, 0, 0)``     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`vertices<class_NavigationObstacle3D_property_vertices>`                             | ``PackedVector3Array()`` |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_avoidance_layer_value<class_NavigationObstacle3D_method_get_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_navigation_map<class_NavigationObstacle3D_method_get_navigation_map>`\ (\ ) |const|                                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_rid<class_NavigationObstacle3D_method_get_rid>`\ (\ ) |const|                                                                                                    |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_avoidance_layer_value<class_NavigationObstacle3D_method_set_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_navigation_map<class_NavigationObstacle3D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả property
--------------

.. _class_NavigationObstacle3D_property_affect_navigation_mesh:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **affect_navigation_mesh** = ``false`` :ref:`🔗<class_NavigationObstacle3D_property_affect_navigation_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_affect_navigation_mesh**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_affect_navigation_mesh**\ (\ )

Nếu được bật và được phân tích trong quá trình baking navigation mesh, obstacle sẽ loại bỏ geometry nguồn bên trong shape được định nghĩa bởi :ref:`vertices<class_NavigationObstacle3D_property_vertices>` và :ref:`height<class_NavigationObstacle3D_property_height>` của nó.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_avoidance_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **avoidance_enabled** = ``true`` :ref:`🔗<class_NavigationObstacle3D_property_avoidance_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_avoidance_enabled**\ (\ )

Nếu ``true``, obstacle sẽ ảnh hưởng đến các agent sử dụng avoidance.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_avoidance_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_layers** = ``1`` :ref:`🔗<class_NavigationObstacle3D_property_avoidance_layers>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_layers**\ (\ )

Một bitfield xác định các avoidance layer cho obstacle này. Các agent có bit tương ứng trong avoidance mask của chúng sẽ tránh obstacle này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_carve_navigation_mesh:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **carve_navigation_mesh** = ``false`` :ref:`🔗<class_NavigationObstacle3D_property_carve_navigation_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_carve_navigation_mesh**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_carve_navigation_mesh**\ (\ )

Nếu được bật, các vertex của obstacle sẽ carve vào navigation mesh đã bake với shape không bị ảnh hưởng bởi các offset bổ sung, ví dụ như agent radius.

Nó vẫn sẽ bị ảnh hưởng bởi các bước postprocessing tiếp theo của quá trình baking, chẳng hạn như đơn giản hóa edge và polygon.

Yêu cầu :ref:`affect_navigation_mesh<class_NavigationObstacle3D_property_affect_navigation_mesh>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``1.0`` :ref:`🔗<class_NavigationObstacle3D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Thiết lập chiều cao của obstacle được sử dụng trong avoidance 2D. Các agent sử dụng avoidance 2D sẽ bỏ qua những obstacle nằm bên dưới hoặc bên trên chúng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.0`` :ref:`🔗<class_NavigationObstacle3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Thiết lập bán kính avoidance cho obstacle.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_use_3d_avoidance:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_3d_avoidance** = ``false`` :ref:`🔗<class_NavigationObstacle3D_property_use_3d_avoidance>`

.. rst-class:: classref-property-setget

- |void| **set_use_3d_avoidance**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_3d_avoidance**\ (\ )

Nếu ``true``, obstacle sẽ ảnh hưởng đến avoidance 3D của các agent có obstacle :ref:`radius<class_NavigationObstacle3D_property_radius>`.

Nếu ``false``, obstacle sẽ ảnh hưởng đến avoidance 2D của các agent có cả obstacle :ref:`vertices<class_NavigationObstacle3D_property_vertices>` lẫn obstacle :ref:`radius<class_NavigationObstacle3D_property_radius>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationObstacle3D_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_velocity**\ (\ )

Thiết lập velocity mong muốn cho obstacle để các agent khác có thể dự đoán obstacle tốt hơn nếu obstacle được di chuyển thường xuyên bằng một velocity (mỗi frame) thay vì warp đến vị trí mới. Chỉ ảnh hưởng đến avoidance đối với các obstacle :ref:`radius<class_NavigationObstacle3D_property_radius>`. Không có tác dụng với các obstacle có vertex tĩnh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_property_vertices:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **vertices** = ``PackedVector3Array()`` :ref:`🔗<class_NavigationObstacle3D_property_vertices>`

.. rst-class:: classref-property-setget

- |void| **set_vertices**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_vertices**\ (\ )

Các vertex outline của obstacle. Nếu các vertex được sắp theo thứ tự chiều kim đồng hồ, các agent sẽ bị obstacle đẩy vào trong; nếu không, chúng sẽ bị đẩy ra ngoài. Các outline không được giao nhau hoặc chồng lấp. Nếu obstacle sử dụng các vertex được warp đến vị trí mới, các agent không thể dự đoán chuyển động này và có thể bị mắc kẹt bên trong obstacle.

**Lưu ý:** Array được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị property gốc. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_NavigationObstacle3D_method_get_avoidance_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationObstacle3D_method_get_avoidance_layer_value>`

Trả về việc layer được chỉ định của bitmask :ref:`avoidance_layers<class_NavigationObstacle3D_property_avoidance_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationObstacle3D_method_get_navigation_map>`

Trả về :ref:`RID<class_RID>` của navigation map cho node NavigationObstacle này. Function này luôn trả về map được thiết lập trên node NavigationObstacle, không phải map của obstacle trừu tượng trên NavigationServer. Nếu map của obstacle được thay đổi trực tiếp bằng API của NavigationServer, node NavigationObstacle sẽ không biết về thay đổi map đó. Hãy sử dụng :ref:`set_navigation_map()<class_NavigationObstacle3D_method_set_navigation_map>` để thay đổi navigation map cho NavigationObstacle và đồng thời cập nhật obstacle trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationObstacle3D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của obstacle này trên :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_method_set_avoidance_layer_value:

.. rst-class:: classref-method

|void| **set_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationObstacle3D_method_set_avoidance_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`avoidance_layers<class_NavigationObstacle3D_property_avoidance_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle3D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationObstacle3D_method_set_navigation_map>`

Thiết lập :ref:`RID<class_RID>` của navigation map mà node NavigationObstacle này sẽ sử dụng, đồng thời cập nhật ``obstacle`` trên NavigationServer.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
