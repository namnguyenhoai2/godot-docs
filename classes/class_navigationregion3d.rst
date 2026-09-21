:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationRegion3D.xml.

.. _class_NavigationRegion3D:

NavigationRegion3D
==================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một vùng 3D có thể đi qua mà :ref:`NavigationAgent3D<class_NavigationAgent3D>`\ s có thể sử dụng để tìm đường.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một vùng 3D có thể đi qua dựa trên :ref:`NavigationMesh<class_NavigationMesh>` mà :ref:`NavigationAgent3D<class_NavigationAgent3D>`\ s có thể sử dụng để tìm đường.

Hai vùng có thể được kết nối với nhau nếu chúng có chung một cạnh tương tự. Bạn có thể thiết lập khoảng cách tối thiểu giữa hai đỉnh cần thiết để kết nối hai cạnh bằng cách sử dụng :ref:`NavigationServer3D.map_set_edge_connection_margin()<class_NavigationServer3D_method_map_set_edge_connection_margin>`.

\ **Lưu ý:** Việc chồng hai navigation mesh của các vùng lên nhau là chưa đủ để kết nối hai vùng. Chúng phải có chung một cạnh tương tự.

Chi phí đi vào vùng này từ một vùng khác có thể được điều khiển bằng giá trị :ref:`enter_cost<class_NavigationRegion3D_property_enter_cost>`.

\ **Lưu ý:** Giá trị này không được cộng vào chi phí đường đi khi vị trí bắt đầu đã nằm bên trong vùng này.

Chi phí di chuyển trong vùng này có thể được điều khiển bằng hệ số :ref:`travel_cost<class_NavigationRegion3D_property_travel_cost>`.

\ **Lưu ý:** Node này lưu vào bộ nhớ đệm các thay đổi đối với các thuộc tính của nó, vì vậy nếu bạn thay đổi region :ref:`RID<class_RID>` nền tảng trong :ref:`NavigationServer3D<class_NavigationServer3D>`, những thay đổi đó sẽ không được phản ánh trong các thuộc tính của node này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationRegions <../tutorials/navigation/navigation_using_navigationregions>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                     | :ref:`enabled<class_NavigationRegion3D_property_enabled>`                           | ``true`` |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`                   | :ref:`enter_cost<class_NavigationRegion3D_property_enter_cost>`                     | ``0.0``  |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`                       | :ref:`navigation_layers<class_NavigationRegion3D_property_navigation_layers>`       | ``1``    |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`NavigationMesh<class_NavigationMesh>` | :ref:`navigation_mesh<class_NavigationRegion3D_property_navigation_mesh>`           |          |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`                   | :ref:`travel_cost<class_NavigationRegion3D_property_travel_cost>`                   | ``1.0``  |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                     | :ref:`use_edge_connections<class_NavigationRegion3D_property_use_edge_connections>` | ``true`` |
   +---------------------------------------------+-------------------------------------------------------------------------------------+----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`bake_navigation_mesh<class_NavigationRegion3D_method_bake_navigation_mesh>`\ (\ on_thread\: :ref:`bool<class_bool>` = true\ )                                        |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`get_bounds<class_NavigationRegion3D_method_get_bounds>`\ (\ ) |const|                                                                                                |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_navigation_layer_value<class_NavigationRegion3D_method_get_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_navigation_map<class_NavigationRegion3D_method_get_navigation_map>`\ (\ ) |const|                                                                                |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_region_rid<class_NavigationRegion3D_method_get_region_rid>`\ (\ ) |const|                                                                                        |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`   | :ref:`get_rid<class_NavigationRegion3D_method_get_rid>`\ (\ ) |const|                                                                                                      |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_baking<class_NavigationRegion3D_method_is_baking>`\ (\ ) |const|                                                                                                  |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_navigation_layer_value<class_NavigationRegion3D_method_set_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_navigation_map<class_NavigationRegion3D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_NavigationRegion3D_signal_bake_finished:

.. rst-class:: classref-signal

**bake_finished**\ (\ ) :ref:`🔗<class_NavigationRegion3D_signal_bake_finished>`

Thông báo khi thao tác bake navigation mesh hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_signal_navigation_mesh_changed:

.. rst-class:: classref-signal

**navigation_mesh_changed**\ (\ ) :ref:`🔗<class_NavigationRegion3D_signal_navigation_mesh_changed>`

Thông báo khi :ref:`NavigationMesh<class_NavigationMesh>` đã thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationRegion3D_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``true`` :ref:`🔗<class_NavigationRegion3D_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Xác định **NavigationRegion3D** được bật hay tắt.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_property_enter_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **enter_cost** = ``0.0`` :ref:`🔗<class_NavigationRegion3D_property_enter_cost>`

.. rst-class:: classref-property-setget

- |void| **set_enter_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_enter_cost**\ (\ )

Khi thao tác tìm đường đi vào navigation mesh của vùng này từ navigation mesh của một vùng khác, giá trị :ref:`enter_cost<class_NavigationRegion3D_property_enter_cost>` được cộng vào khoảng cách đường đi để xác định đường đi ngắn nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationRegion3D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Một bitfield xác định tất cả navigation layer mà vùng này thuộc về. Các navigation layer này có thể được kiểm tra khi yêu cầu đường đi bằng :ref:`NavigationServer3D.map_get_path()<class_NavigationServer3D_method_map_get_path>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_property_navigation_mesh:

.. rst-class:: classref-property

:ref:`NavigationMesh<class_NavigationMesh>` **navigation_mesh** :ref:`🔗<class_NavigationRegion3D_property_navigation_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_mesh**\ (\ value\: :ref:`NavigationMesh<class_NavigationMesh>`\ ) - :ref:`NavigationMesh<class_NavigationMesh>` **get_navigation_mesh**\ (\ )

Resource :ref:`NavigationMesh<class_NavigationMesh>` cần sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_property_travel_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **travel_cost** = ``1.0`` :ref:`🔗<class_NavigationRegion3D_property_travel_cost>`

.. rst-class:: classref-property-setget

- |void| **set_travel_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_travel_cost**\ (\ )

Khi thao tác tìm đường di chuyển bên trong navigation mesh của vùng này, các khoảng cách đã đi qua được nhân với :ref:`travel_cost<class_NavigationRegion3D_property_travel_cost>` để xác định đường đi ngắn nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_property_use_edge_connections:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_edge_connections** = ``true`` :ref:`🔗<class_NavigationRegion3D_property_use_edge_connections>`

.. rst-class:: classref-property-setget

- |void| **set_use_edge_connections**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_edge_connections**\ (\ )

Nếu được bật, navigation region sẽ sử dụng các kết nối cạnh để kết nối với những navigation region khác nằm trong phạm vi margin kết nối cạnh của navigation map.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationRegion3D_method_bake_navigation_mesh:

.. rst-class:: classref-method

|void| **bake_navigation_mesh**\ (\ on_thread\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_NavigationRegion3D_method_bake_navigation_mesh>`

Bake :ref:`NavigationMesh<class_NavigationMesh>`. Nếu ``on_thread`` được đặt thành ``true`` (mặc định), quá trình bake sẽ được thực hiện trên một thread riêng. Bake trên thread riêng rất hữu ích vì baking navigation không phải là thao tác nhẹ. Khi hoàn tất, thao tác này sẽ tự động đặt :ref:`NavigationMesh<class_NavigationMesh>` mới. Lưu ý rằng baking trên thread riêng có thể rất chậm nếu hình học được phân tích từ các mesh, vì việc truy cập bất đồng bộ vào từng mesh đòi hỏi đồng bộ hóa tốn nhiều tài nguyên. Ngoài ra, lưu ý rằng baking trên thread riêng sẽ tự động bị vô hiệu hóa trên các hệ điều hành không thể sử dụng thread (chẳng hạn Web khi tắt thread).

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_get_bounds:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **get_bounds**\ (\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_get_bounds>`

Trả về bounding box căn chỉnh theo trục cho navigation mesh đã biến đổi của vùng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_get_navigation_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_get_navigation_layer_value>`

Trả về layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationRegion3D_property_navigation_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_get_navigation_map>`

Trả về navigation map hiện tại :ref:`RID<class_RID>` được region này sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_get_region_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_region_rid**\ (\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_get_region_rid>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`get_rid()<class_NavigationRegion3D_method_get_rid>`.

Trả về :ref:`RID<class_RID>` của region này trên :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của region này trên :ref:`NavigationServer3D<class_NavigationServer3D>`. Khi kết hợp với :ref:`NavigationServer3D.map_get_closest_point_owner()<class_NavigationServer3D_method_map_get_closest_point_owner>`, có thể sử dụng để xác định **NavigationRegion3D** gần một điểm nhất trên navigation map đã hợp nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_is_baking:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_baking**\ (\ ) |const| :ref:`🔗<class_NavigationRegion3D_method_is_baking>`

Trả về ``true`` khi :ref:`NavigationMesh<class_NavigationMesh>` đang được bake trên background thread.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_set_navigation_layer_value:

.. rst-class:: classref-method

|void| **set_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationRegion3D_method_set_navigation_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationRegion3D_property_navigation_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion3D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationRegion3D_method_set_navigation_map>`

Đặt :ref:`RID<class_RID>` của navigation map mà region này sẽ sử dụng. Theo mặc định, region sẽ tự động tham gia navigation map mặc định :ref:`World3D<class_World3D>`, vì vậy chỉ cần sử dụng hàm này để ghi đè map mặc định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
