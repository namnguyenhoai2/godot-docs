.. _doc_navigation_using_navigationmaps:

Sử dụng NavigationMaps
======================

.. image:: img/nav_maps.png

NavigationMap là một thế giới điều hướng trừu tượng trên NavigationServer, được xác định bằng :ref:`RID<class_RID>` của NavigationServer.

Một map có thể chứa và kết nối gần như vô hạn navigation region với navigation mesh để xây dựng các khu vực có thể di chuyển trong thế giới game cho việc tìm đường.

Một map có thể chứa các avoidance agent. Việc tránh va chạm sẽ được tính toán dựa trên các agent hiện diện trong map.

.. note::

    Các NavigationMap khác nhau hoàn toàn tách biệt với nhau, nhưng navigation region và avoidance agent có thể chuyển đổi giữa các map khác nhau. Việc chuyển đổi sẽ có hiệu lực khi NavigationServer đồng bộ hóa.

Các navigation map mặc định
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, Godot tạo một navigation map cho mỗi :ref:`World2D<class_World2D>` và :ref:`World3D<class_World3D>` của root viewport.

Có thể lấy RID của navigation map mặc định 2D bằng ``get_world_2d().get_navigation_map()`` từ bất kỳ :ref:`Node2D<class_Node2D>` nào kế thừa Node.

Có thể lấy RID của navigation map mặc định 3D bằng ``get_world_3d().get_navigation_map()`` từ bất kỳ :ref:`Node3D<class_Node3D>` nào kế thừa Node.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    func _ready() -> void:
        var default_navigation_map_rid: RID = get_world_2d().get_navigation_map()

 .. code-tab:: csharp 2D C#

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            Rid defaultNavigationMapRid = GetWorld2D().NavigationMap;
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    func _ready() -> void:
        var default_navigation_map_rid: RID = get_world_3d().get_navigation_map()

 .. code-tab:: csharp 3D C#

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            Rid defaultNavigationMapRid = GetWorld3D().NavigationMap;
        }
    }

Tạo navigation map mới
~~~~~~~~~~~~~~~~~~~~~~

NavigationServer có thể tạo và hỗ trợ số lượng navigation map cần thiết cho gameplay cụ thể. Các navigation map bổ sung được tạo và xử lý bằng cách sử dụng trực tiếp API của NavigationServer, chẳng hạn để hỗ trợ các loại locomotion khác nhau của avoidance agent hoặc actor.

Để xem các ví dụ sử dụng những navigation map khác nhau, hãy xem :ref:`doc_navigation_different_actor_types` và :ref:`doc_navigation_different_actor_locomotion`.

Mỗi navigation map sẽ đồng bộ độc lập các thay đổi đang chờ đối với navigation region và avoidance agent của map đó. Một navigation map chưa nhận thay đổi sẽ tiêu tốn rất ít hoặc không tiêu tốn thời gian xử lý. Navigation region và avoidance agent chỉ có thể thuộc về một navigation map duy nhất, nhưng có thể chuyển map bất kỳ lúc nào.

.. note::

    Việc chuyển navigation map sẽ chỉ có hiệu lực sau lần đồng bộ NavigationServer tiếp theo.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    func _ready() -> void:
        var new_navigation_map: RID = NavigationServer2D.map_create()
        NavigationServer2D.map_set_active(new_navigation_map, true)

 .. code-tab:: csharp 2D C#

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            Rid newNavigationMap = NavigationServer2D.MapCreate();
            NavigationServer2D.MapSetActive(newNavigationMap, true);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    func _ready() -> void:
        var new_navigation_map: RID = NavigationServer3D.map_create()
        NavigationServer3D.map_set_active(new_navigation_map, true)

 .. code-tab:: csharp 3D C#

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            Rid newNavigationMap = NavigationServer3D.MapCreate();
            NavigationServer3D.MapSetActive(newNavigationMap, true);
        }
    }

.. note::

    Không có sự khác biệt giữa các navigation map được tạo bằng API NavigationServer2D và API NavigationServer3D.
