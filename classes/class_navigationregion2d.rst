:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationRegion2D.xml.

.. _class_NavigationRegion2D:

NavigationRegion2D
==================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một vùng 2D có thể đi qua mà :ref:`NavigationAgent2D<class_NavigationAgent2D>`\ s có thể sử dụng để tìm đường.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một vùng 2D có thể đi qua dựa trên :ref:`NavigationPolygon<class_NavigationPolygon>` mà :ref:`NavigationAgent2D<class_NavigationAgent2D>`\ s có thể sử dụng để tìm đường.

Hai vùng có thể được kết nối với nhau nếu chúng có chung một cạnh tương tự nhau. Bạn có thể thiết lập khoảng cách tối thiểu giữa hai đỉnh cần thiết để kết nối hai cạnh bằng cách sử dụng :ref:`NavigationServer2D.map_set_edge_connection_margin()<class_NavigationServer2D_method_map_set_edge_connection_margin>`.

\ **Lưu ý:** Việc chồng hai navigation polygon của các vùng lên nhau là chưa đủ để kết nối hai vùng. Chúng phải có chung một cạnh tương tự nhau.

Chi phí tìm đường khi đi vào một vùng từ vùng khác có thể được điều khiển bằng giá trị :ref:`enter_cost<class_NavigationRegion2D_property_enter_cost>`.

\ **Lưu ý:** Giá trị này không được cộng vào chi phí đường đi khi vị trí bắt đầu đã nằm bên trong vùng này.

Chi phí tìm đường khi di chuyển trong vùng này có thể được điều khiển bằng hệ số :ref:`travel_cost<class_NavigationRegion2D_property_travel_cost>`.

\ **Lưu ý:** Node này lưu bộ nhớ đệm các thay đổi đối với những thuộc tính của nó, vì vậy nếu bạn thay đổi region :ref:`RID<class_RID>` underlying trong :ref:`NavigationServer2D<class_NavigationServer2D>`, những thay đổi đó sẽ không được phản ánh trong các thuộc tính của node này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationRegions <../tutorials/navigation/navigation_using_navigationregions>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                           | :ref:`enabled<class_NavigationRegion2D_property_enabled>`                           | ``true`` |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`                         | :ref:`enter_cost<class_NavigationRegion2D_property_enter_cost>`                     | ``0.0``  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`                             | :ref:`navigation_layers<class_NavigationRegion2D_property_navigation_layers>`       | ``1``    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`NavigationPolygon<class_NavigationPolygon>` | :ref:`navigation_polygon<class_NavigationRegion2D_property_navigation_polygon>`     |          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`                         | :ref:`travel_cost<class_NavigationRegion2D_property_travel_cost>`                   | ``1.0``  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                           | :ref:`use_edge_connections<class_NavigationRegion2D_property_use_edge_connections>` | ``true`` |
   +---------------------------------------------------+-------------------------------------------------------------------------------------+----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`bake_navigation_polygon<class_NavigationRegion2D_method_bake_navigation_polygon>`\ (\ on_thread\: :ref:`bool<class_bool>` = true\ )                                  |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>` | :ref:`get_bounds<class_NavigationRegion2D_method_get_bounds>`\ (\ ) |const|                                                                                                |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_navigation_layer_value<class_NavigationRegion2D_method_get_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`     | :ref:`get_navigation_map<class_NavigationRegion2D_method_get_navigation_map>`\ (\ ) |const|                                                                                |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`     | :ref:`get_region_rid<class_NavigationRegion2D_method_get_region_rid>`\ (\ ) |const|                                                                                        |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`     | :ref:`get_rid<class_NavigationRegion2D_method_get_rid>`\ (\ ) |const|                                                                                                      |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`is_baking<class_NavigationRegion2D_method_is_baking>`\ (\ ) |const|                                                                                                  |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_navigation_layer_value<class_NavigationRegion2D_method_set_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_navigation_map<class_NavigationRegion2D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_NavigationRegion2D_signal_bake_finished:

.. rst-class:: classref-signal

**bake_finished**\ (\ ) :ref:`🔗<class_NavigationRegion2D_signal_bake_finished>`

Được phát ra khi thao tác bake navigation polygon hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_signal_navigation_polygon_changed:

.. rst-class:: classref-signal

**navigation_polygon_changed**\ (\ ) :ref:`🔗<class_NavigationRegion2D_signal_navigation_polygon_changed>`

Được phát ra khi navigation polygon đang được sử dụng bị thay thế hoặc các thay đổi đối với phần bên trong của navigation polygon hiện tại được commit.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationRegion2D_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``true`` :ref:`🔗<class_NavigationRegion2D_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Xác định **NavigationRegion2D** được bật hay tắt.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_property_enter_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **enter_cost** = ``0.0`` :ref:`🔗<class_NavigationRegion2D_property_enter_cost>`

.. rst-class:: classref-property-setget

- |void| **set_enter_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_enter_cost**\ (\ )

Khi quá trình tìm đường đi vào navigation mesh của vùng này từ navigation mesh của một vùng khác, giá trị :ref:`enter_cost<class_NavigationRegion2D_property_enter_cost>` được cộng vào khoảng cách đường đi để xác định đường đi ngắn nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationRegion2D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Một bitfield xác định tất cả các navigation layer mà vùng này thuộc về. Các navigation layer này có thể được kiểm tra khi yêu cầu một đường đi bằng :ref:`NavigationServer2D.map_get_path()<class_NavigationServer2D_method_map_get_path>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_property_navigation_polygon:

.. rst-class:: classref-property

:ref:`NavigationPolygon<class_NavigationPolygon>` **navigation_polygon** :ref:`🔗<class_NavigationRegion2D_property_navigation_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_polygon**\ (\ value\: :ref:`NavigationPolygon<class_NavigationPolygon>`\ ) - :ref:`NavigationPolygon<class_NavigationPolygon>` **get_navigation_polygon**\ (\ )

Resource :ref:`NavigationPolygon<class_NavigationPolygon>` cần sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_property_travel_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **travel_cost** = ``1.0`` :ref:`🔗<class_NavigationRegion2D_property_travel_cost>`

.. rst-class:: classref-property-setget

- |void| **set_travel_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_travel_cost**\ (\ )

Khi quá trình tìm đường di chuyển bên trong navigation mesh của vùng này, các khoảng cách đã đi được nhân với :ref:`travel_cost<class_NavigationRegion2D_property_travel_cost>` để xác định đường đi ngắn nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_property_use_edge_connections:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_edge_connections** = ``true`` :ref:`🔗<class_NavigationRegion2D_property_use_edge_connections>`

.. rst-class:: classref-property-setget

- |void| **set_use_edge_connections**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_edge_connections**\ (\ )

Nếu được bật, navigation region sẽ sử dụng các kết nối cạnh để kết nối với những navigation region khác nằm trong phạm vi margin kết nối cạnh của navigation map.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationRegion2D_method_bake_navigation_polygon:

.. rst-class:: classref-method

|void| **bake_navigation_polygon**\ (\ on_thread\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_NavigationRegion2D_method_bake_navigation_polygon>`

Bake :ref:`NavigationPolygon<class_NavigationPolygon>`. Nếu ``on_thread`` được đặt thành ``true`` (mặc định), quá trình bake sẽ được thực hiện trên một thread riêng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_get_bounds:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **get_bounds**\ (\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_get_bounds>`

Trả về hình chữ nhật căn theo trục của navigation mesh đã được biến đổi của vùng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_get_navigation_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_get_navigation_layer_value>`

Trả về liệu layer được chỉ định của bitmask :ref:`navigation_layers<class_NavigationRegion2D_property_navigation_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_get_navigation_map>`

Trả về navigation map hiện tại :ref:`RID<class_RID>` được vùng này sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_get_region_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_region_rid**\ (\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_get_region_rid>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`get_rid()<class_NavigationRegion2D_method_get_rid>`.

Trả về :ref:`RID<class_RID>` của vùng này trên :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của vùng này trên :ref:`NavigationServer2D<class_NavigationServer2D>`. Kết hợp với :ref:`NavigationServer2D.map_get_closest_point_owner()<class_NavigationServer2D_method_map_get_closest_point_owner>`, giá trị này có thể được sử dụng để xác định **NavigationRegion2D** gần một điểm nhất trên navigation map đã hợp nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_is_baking:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_baking**\ (\ ) |const| :ref:`🔗<class_NavigationRegion2D_method_is_baking>`

Trả về ``true`` khi :ref:`NavigationPolygon<class_NavigationPolygon>` đang được bake trên một background thread.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_set_navigation_layer_value:

.. rst-class:: classref-method

|void| **set_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationRegion2D_method_set_navigation_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationRegion2D_property_navigation_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationRegion2D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationRegion2D_method_set_navigation_map>`

Đặt :ref:`RID<class_RID>` của navigation map mà vùng này sẽ sử dụng. Theo mặc định, vùng sẽ tự động tham gia navigation map mặc định :ref:`World2D<class_World2D>`, vì vậy chỉ cần sử dụng hàm này để ghi đè map mặc định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
