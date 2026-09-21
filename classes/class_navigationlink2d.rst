:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationLink2D.xml.

.. _class_NavigationLink2D:

NavigationLink2D
================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một liên kết giữa hai vị trí trên :ref:`NavigationRegion2D<class_NavigationRegion2D>`\ s mà các agent có thể được định tuyến qua.

.. rst-class:: classref-introduction-group

Mô tả
-----

A link between two positions on :ref:`NavigationRegion2D<class_NavigationRegion2D>`\ s that agents can be routed through. These positions can be on the same :ref:`NavigationRegion2D<class_NavigationRegion2D>` or on two different ones. Links are useful to express navigation methods other than traveling along the surface of the navigation polygon, such as ziplines, teleporters, or gaps that can be jumped across.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationLinks <../tutorials/navigation/navigation_using_navigationlinks>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`bidirectional<class_NavigationLink2D_property_bidirectional>`         | ``true``          |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`enabled<class_NavigationLink2D_property_enabled>`                     | ``true``          |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`end_position<class_NavigationLink2D_property_end_position>`           | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`enter_cost<class_NavigationLink2D_property_enter_cost>`               | ``0.0``           |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`navigation_layers<class_NavigationLink2D_property_navigation_layers>` | ``1``             |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`start_position<class_NavigationLink2D_property_start_position>`       | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`travel_cost<class_NavigationLink2D_property_travel_cost>`             | ``1.0``           |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_global_end_position<class_NavigationLink2D_method_get_global_end_position>`\ (\ ) |const|                                                                      |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_global_start_position<class_NavigationLink2D_method_get_global_start_position>`\ (\ ) |const|                                                                  |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`get_navigation_layer_value<class_NavigationLink2D_method_get_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`         | :ref:`get_navigation_map<class_NavigationLink2D_method_get_navigation_map>`\ (\ ) |const|                                                                                |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`         | :ref:`get_rid<class_NavigationLink2D_method_get_rid>`\ (\ ) |const|                                                                                                      |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_global_end_position<class_NavigationLink2D_method_set_global_end_position>`\ (\ position\: :ref:`Vector2<class_Vector2>`\ )                                    |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_global_start_position<class_NavigationLink2D_method_set_global_start_position>`\ (\ position\: :ref:`Vector2<class_Vector2>`\ )                                |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_navigation_layer_value<class_NavigationLink2D_method_set_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_navigation_map<class_NavigationLink2D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationLink2D_property_bidirectional:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **bidirectional** = ``true`` :ref:`🔗<class_NavigationLink2D_property_bidirectional>`

.. rst-class:: classref-property-setget

- |void| **set_bidirectional**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_bidirectional**\ (\ )

Liên kết này có thể được đi qua theo cả hai hướng hay chỉ từ :ref:`start_position<class_NavigationLink2D_property_start_position>` đến :ref:`end_position<class_NavigationLink2D_property_end_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``true`` :ref:`🔗<class_NavigationLink2D_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Liên kết này hiện có đang hoạt động hay không. Nếu ``false``, :ref:`NavigationServer2D.map_get_path()<class_NavigationServer2D_method_map_get_path>` sẽ bỏ qua liên kết này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_end_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **end_position** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationLink2D_property_end_position>`

.. rst-class:: classref-property-setget

- |void| **set_end_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_end_position**\ (\ )

Vị trí kết thúc của liên kết.

Vị trí này sẽ tìm polygon gần nhất trong navigation mesh để gắn vào.

Khoảng cách mà liên kết tìm kiếm được kiểm soát bởi :ref:`NavigationServer2D.map_set_link_connection_radius()<class_NavigationServer2D_method_map_set_link_connection_radius>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_enter_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **enter_cost** = ``0.0`` :ref:`🔗<class_NavigationLink2D_property_enter_cost>`

.. rst-class:: classref-property-setget

- |void| **set_enter_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_enter_cost**\ (\ )

Khi pathfinding đi vào liên kết này từ navigation mesh của một region khác, giá trị :ref:`enter_cost<class_NavigationLink2D_property_enter_cost>` được cộng vào khoảng cách của path để xác định path ngắn nhất.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationLink2D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Một bitfield xác định tất cả navigation layer mà liên kết thuộc về. Các navigation layer này sẽ được kiểm tra khi yêu cầu một path bằng :ref:`NavigationServer2D.map_get_path()<class_NavigationServer2D_method_map_get_path>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_start_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **start_position** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationLink2D_property_start_position>`

.. rst-class:: classref-property-setget

- |void| **set_start_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_start_position**\ (\ )

Vị trí bắt đầu của liên kết.

Vị trí này sẽ tìm polygon gần nhất trong navigation mesh để gắn vào.

Khoảng cách mà liên kết tìm kiếm được kiểm soát bởi :ref:`NavigationServer2D.map_set_link_connection_radius()<class_NavigationServer2D_method_map_set_link_connection_radius>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_property_travel_cost:

.. rst-class:: classref-property

:ref:`float<class_float>` **travel_cost** = ``1.0`` :ref:`🔗<class_NavigationLink2D_property_travel_cost>`

.. rst-class:: classref-property-setget

- |void| **set_travel_cost**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_travel_cost**\ (\ )

Khi pathfinding di chuyển dọc theo liên kết, khoảng cách đã đi được nhân với :ref:`travel_cost<class_NavigationLink2D_property_travel_cost>` để xác định path ngắn nhất.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationLink2D_method_get_global_end_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_global_end_position**\ (\ ) |const| :ref:`🔗<class_NavigationLink2D_method_get_global_end_position>`

Trả về :ref:`end_position<class_NavigationLink2D_property_end_position>` tương đối với liên kết dưới dạng một vị trí global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_get_global_start_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_global_start_position**\ (\ ) |const| :ref:`🔗<class_NavigationLink2D_method_get_global_start_position>`

Trả về :ref:`start_position<class_NavigationLink2D_property_start_position>` tương đối với liên kết dưới dạng một vị trí global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_get_navigation_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationLink2D_method_get_navigation_layer_value>`

Trả về việc layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationLink2D_property_navigation_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationLink2D_method_get_navigation_map>`

Trả về navigation map hiện tại :ref:`RID<class_RID>` được liên kết này sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationLink2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của liên kết này trên :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_set_global_end_position:

.. rst-class:: classref-method

|void| **set_global_end_position**\ (\ position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_NavigationLink2D_method_set_global_end_position>`

Đặt :ref:`end_position<class_NavigationLink2D_property_end_position>` tương đối với liên kết từ một ``position`` global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_set_global_start_position:

.. rst-class:: classref-method

|void| **set_global_start_position**\ (\ position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_NavigationLink2D_method_set_global_start_position>`

Đặt :ref:`start_position<class_NavigationLink2D_property_start_position>` tương đối với liên kết từ một ``position`` global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_set_navigation_layer_value:

.. rst-class:: classref-method

|void| **set_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationLink2D_method_set_navigation_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationLink2D_property_navigation_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationLink2D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationLink2D_method_set_navigation_map>`

Đặt :ref:`RID<class_RID>` của navigation map mà liên kết này nên sử dụng. Theo mặc định, liên kết sẽ tự động tham gia :ref:`World2D<class_World2D>` navigation map mặc định, vì vậy chỉ cần dùng phương thức này để ghi đè map mặc định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
