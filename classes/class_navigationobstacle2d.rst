:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationObstacle2D.xml.

.. _class_NavigationObstacle2D:

NavigationObstacle2D
====================

**Thử nghiệm:** Lớp này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Chướng ngại vật 2D được dùng để tác động đến quá trình baking navigation mesh hoặc giới hạn vận tốc của các agent do avoidance điều khiển.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một chướng ngại vật cần có navigation map và outline :ref:`vertices<class_NavigationObstacle2D_property_vertices>` được định nghĩa để hoạt động chính xác. Các outline không được giao nhau hoặc chồng lấp.

Các chướng ngại vật có thể được đưa vào quá trình baking navigation mesh khi :ref:`affect_navigation_mesh<class_NavigationObstacle2D_property_affect_navigation_mesh>` được bật. Chúng không thêm hình học có thể đi được; thay vào đó, vai trò của chúng là loại bỏ hình học nguồn nằm bên trong hình dạng. Điều này có thể được dùng để ngăn navigation mesh xuất hiện ở những vị trí không mong muốn. Nếu :ref:`carve_navigation_mesh<class_NavigationObstacle2D_property_carve_navigation_mesh>` được bật, hình dạng đã baking sẽ không bị ảnh hưởng bởi các offset của quá trình baking navigation mesh, chẳng hạn bán kính của agent.

Với :ref:`avoidance_enabled<class_NavigationObstacle2D_property_avoidance_enabled>`, chướng ngại vật có thể giới hạn các avoidance velocity của những agent sử dụng avoidance. Nếu các đỉnh của chướng ngại vật được sắp theo thứ tự chiều kim đồng hồ, các agent avoidance sẽ bị đẩy vào trong chướng ngại vật; nếu không, chúng sẽ bị đẩy ra ngoài. Các chướng ngại vật sử dụng vertices và avoidance có thể warp đến vị trí mới, nhưng không nên được di chuyển ở mọi frame, vì mỗi thay đổi đều yêu cầu xây dựng lại avoidance map.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationObstacles <../tutorials/navigation/navigation_using_navigationobstacles>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`affect_navigation_mesh<class_NavigationObstacle2D_property_affect_navigation_mesh>` | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`avoidance_enabled<class_NavigationObstacle2D_property_avoidance_enabled>`           | ``true``                 |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                               | :ref:`avoidance_layers<class_NavigationObstacle2D_property_avoidance_layers>`             | ``1``                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`carve_navigation_mesh<class_NavigationObstacle2D_property_carve_navigation_mesh>`   | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`radius<class_NavigationObstacle2D_property_radius>`                                 | ``0.0``                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`velocity<class_NavigationObstacle2D_property_velocity>`                             | ``Vector2(0, 0)``        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`vertices<class_NavigationObstacle2D_property_vertices>`                             | ``PackedVector2Array()`` |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_avoidance_layer_value<class_NavigationObstacle2D_method_get_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_navigation_map<class_NavigationObstacle2D_method_get_navigation_map>`\ (\ ) |const|                                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_rid<class_NavigationObstacle2D_method_get_rid>`\ (\ ) |const|                                                                                                    |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_avoidance_layer_value<class_NavigationObstacle2D_method_set_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_navigation_map<class_NavigationObstacle2D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_NavigationObstacle2D_property_affect_navigation_mesh:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **affect_navigation_mesh** = ``false`` :ref:`🔗<class_NavigationObstacle2D_property_affect_navigation_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_affect_navigation_mesh**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_affect_navigation_mesh**\ (\ )

Nếu được bật và được phân tích trong một quá trình baking navigation mesh, chướng ngại vật sẽ loại bỏ hình học nguồn bên trong hình dạng được định nghĩa bởi :ref:`vertices<class_NavigationObstacle2D_property_vertices>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_avoidance_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **avoidance_enabled** = ``true`` :ref:`🔗<class_NavigationObstacle2D_property_avoidance_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_avoidance_enabled**\ (\ )

Nếu ``true``, chướng ngại vật sẽ tác động đến các agent sử dụng avoidance.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_avoidance_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_layers** = ``1`` :ref:`🔗<class_NavigationObstacle2D_property_avoidance_layers>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_layers**\ (\ )

Một bitfield xác định các avoidance layer cho chướng ngại vật này. Các agent có bit tương ứng trong avoidance mask sẽ tránh chướng ngại vật này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_carve_navigation_mesh:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **carve_navigation_mesh** = ``false`` :ref:`🔗<class_NavigationObstacle2D_property_carve_navigation_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_carve_navigation_mesh**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_carve_navigation_mesh**\ (\ )

Nếu được bật, các đỉnh của chướng ngại vật sẽ khoét vào navigation mesh đã baking, với hình dạng không bị ảnh hưởng bởi các offset bổ sung (chẳng hạn bán kính của agent).

Nó vẫn sẽ bị ảnh hưởng bởi các bước postprocessing tiếp theo của quá trình baking, chẳng hạn đơn giản hóa cạnh và polygon.

Yêu cầu :ref:`affect_navigation_mesh<class_NavigationObstacle2D_property_affect_navigation_mesh>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.0`` :ref:`🔗<class_NavigationObstacle2D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Thiết lập bán kính avoidance cho chướng ngại vật.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationObstacle2D_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_velocity**\ (\ )

Thiết lập vận tốc mong muốn cho chướng ngại vật để các agent khác có thể dự đoán chướng ngại vật tốt hơn nếu nó được di chuyển đều đặn bằng một vận tốc (mỗi frame) thay vì warp đến vị trí mới. Chỉ ảnh hưởng đến avoidance đối với các chướng ngại vật :ref:`radius<class_NavigationObstacle2D_property_radius>`. Không có tác dụng đối với các chướng ngại vật có vertices tĩnh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_property_vertices:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **vertices** = ``PackedVector2Array()`` :ref:`🔗<class_NavigationObstacle2D_property_vertices>`

.. rst-class:: classref-property-setget

- |void| **set_vertices**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_vertices**\ (\ )

Các đỉnh outline của chướng ngại vật. Nếu các đỉnh được sắp theo thứ tự chiều kim đồng hồ, các agent sẽ bị chướng ngại vật đẩy vào trong; nếu không, chúng sẽ bị đẩy ra ngoài. Các outline không được giao nhau hoặc chồng lấp. Nếu các vertices dùng cho chướng ngại vật được warp đến vị trí mới, các agent không thể dự đoán chuyển động này và có thể bị mắc kẹt bên trong chướng ngại vật.

**Lưu ý:** Mảng được trả về là một *bản sao* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị property ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_NavigationObstacle2D_method_get_avoidance_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationObstacle2D_method_get_avoidance_layer_value>`

Trả về việc layer được chỉ định của bitmask :ref:`avoidance_layers<class_NavigationObstacle2D_property_avoidance_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationObstacle2D_method_get_navigation_map>`

Trả về :ref:`RID<class_RID>` của navigation map cho node NavigationObstacle này. Hàm này luôn trả về map được thiết lập trên node NavigationObstacle, không phải map của obstacle trừu tượng trên NavigationServer. Nếu map của obstacle được thay đổi trực tiếp bằng NavigationServer API, node NavigationObstacle sẽ không nhận biết được thay đổi map. Sử dụng :ref:`set_navigation_map()<class_NavigationObstacle2D_method_set_navigation_map>` để thay đổi navigation map cho NavigationObstacle và đồng thời cập nhật obstacle trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationObstacle2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của chướng ngại vật này trên :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_method_set_avoidance_layer_value:

.. rst-class:: classref-method

|void| **set_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationObstacle2D_method_set_avoidance_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`avoidance_layers<class_NavigationObstacle2D_property_avoidance_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationObstacle2D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationObstacle2D_method_set_navigation_map>`

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
