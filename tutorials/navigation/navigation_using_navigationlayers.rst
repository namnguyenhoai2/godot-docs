.. _doc_navigation_advanced_using_navigationlayers:

Sử dụng NavigationLayers
========================

NavigationLayers là một tính năng tùy chọn, cho phép kiểm soát chi tiết hơn những navigation mesh nào được xét trong một truy vấn đường đi. Chúng hoạt động tương tự như cách các physics layer kiểm soát va chạm giữa các đối tượng va chạm, hoặc cách các visual layer kiểm soát nội dung được render lên Viewport.

NavigationLayers có thể được đặt tên trong **ProjectSettings**, tương tự như physics layer hoặc visual layer.

.. image:: img/navigationlayers_naming.png

Nếu một region không có bất kỳ navigation layer nào tương thích với tham số ``navigation_layers`` của truy vấn đường đi, navigation mesh của region này sẽ bị bỏ qua trong quá trình tìm đường. Xem :ref:`doc_navigation_using_navigationpaths` để biết thêm thông tin về cách truy vấn NavigationServer để lấy đường đi.

NavigationLayers là một giá trị ``int`` duy nhất được sử dụng như một **bitmask**. Nhiều node liên quan đến navigation có các hàm ``set_navigation_layer_value()`` và ``get_navigation_layer_value()`` để đặt và lấy trực tiếp số layer mà không cần thực hiện các phép toán bitwise phức tạp hơn.

Trong các script, có thể sử dụng các hàm trợ giúp sau để làm việc với bitmask ``navigation_layers``.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    func change_layers():
        var region: NavigationRegion2D = get_node("NavigationRegion2D")
        # bật layer thứ 4 cho region này
        region.navigation_layers = enable_bitmask_inx(region.navigation_layers, 4)
        # tắt layer thứ 1 cho region này
        region.navigation_layers = disable_bitmask_inx(region.navigation_layers, 1)

        var agent: NavigationAgent2D = get_node("NavigationAgent2D")
        # khiến các truy vấn đường đi sau này của agent này bỏ qua các region có layer thứ 4
        agent.navigation_layers = disable_bitmask_inx(agent.navigation_layers, 4)

        var path_query_navigation_layers: int = 0
        path_query_navigation_layers = enable_bitmask_inx(path_query_navigation_layers, 2)
        # lấy một đường đi chỉ xét các region thuộc layer thứ 2
        var path: PackedVector2Array = NavigationServer2D.map_get_path(
            map,
            start_position,
            target_position,
            true,
            path_query_navigation_layers
            )

    static func is_bitmask_inx_enabled(_bitmask: int, _index: int) -> bool:
        return _bitmask & (1 << _index) != 0

    static func enable_bitmask_inx(_bitmask: int, _index: int) -> int:
        return _bitmask | (1 << _index)

    static func disable_bitmask_inx(_bitmask: int, _index: int) -> int:
        return _bitmask & ~(1 << _index)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private Rid _map;
        private Vector2 _startPosition;
        private Vector2 _targetPosition;

        private void ChangeLayers()
        {
            NavigationRegion2D region = GetNode<NavigationRegion2D>("NavigationRegion2D");
            // Bật layer thứ 4 cho region này.
            region.NavigationLayers = EnableBitmaskInx(region.NavigationLayers, 4);
            // Tắt layer thứ 1 cho region này.
            region.NavigationLayers = DisableBitmaskInx(region.NavigationLayers, 1);

            NavigationAgent2D agent = GetNode<NavigationAgent2D>("NavigationAgent2D");
            // Khiến các truy vấn đường đi sau này của agent này bỏ qua các region có layer thứ 4.
            agent.NavigationLayers = DisableBitmaskInx(agent.NavigationLayers, 4);

            uint pathQueryNavigationLayers = 0;
            pathQueryNavigationLayers = EnableBitmaskInx(pathQueryNavigationLayers, 2);
            // Lấy một đường đi chỉ xét các region thuộc layer thứ 2.
            Vector2[] path = NavigationServer2D.MapGetPath(
                _map,
                _startPosition,
                _targetPosition,
                true,
                pathQueryNavigationLayers
            );
        }

        private static bool IsBitmaskInxEnabled(uint bitmask, int index)
        {
            return (bitmask & (1 << index)) != 0;
        }

        private static uint EnableBitmaskInx(uint bitmask, int index)
        {
            return bitmask | (1u << index);
        }

        private static uint DisableBitmaskInx(uint bitmask, int index)
        {
            return bitmask & ~(1u << index);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    func change_layers():
        var region: NavigationRegion3D = get_node("NavigationRegion3D")
        # bật layer thứ 4 cho region này
        region.navigation_layers = enable_bitmask_inx(region.navigation_layers, 4)
        # tắt layer thứ 1 cho region này
        region.navigation_layers = disable_bitmask_inx(region.navigation_layers, 1)

        var agent: NavigationAgent3D = get_node("NavigationAgent3D")
        # khiến các truy vấn đường đi sau này của agent này bỏ qua các region có layer thứ 4
        agent.navigation_layers = disable_bitmask_inx(agent.navigation_layers, 4)

        var path_query_navigation_layers: int = 0
        path_query_navigation_layers = enable_bitmask_inx(path_query_navigation_layers, 2)
        # lấy một đường đi chỉ xét các region thuộc layer thứ 2
        var path: PackedVector3Array = NavigationServer3D.map_get_path(
            map,
            start_position,
            target_position,
            true,
            path_query_navigation_layers
            )

    static func is_bitmask_inx_enabled(_bitmask: int, _index: int) -> bool:
        return _bitmask & (1 << _index) != 0

    static func enable_bitmask_inx(_bitmask: int, _index: int) -> int:
        return _bitmask | (1 << _index)

    static func disable_bitmask_inx(_bitmask: int, _index: int) -> int:
        return _bitmask & ~(1 << _index)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private Rid _map;
        private Vector3 _startPosition;
        private Vector3 _targetPosition;

        private void ChangeLayers()
        {
            NavigationRegion3D region = GetNode<NavigationRegion3D>("NavigationRegion3D");
            // Bật layer thứ 4 cho region này.
            region.NavigationLayers = EnableBitmaskInx(region.NavigationLayers, 4);
            // Tắt layer thứ 1 cho region này.
            region.NavigationLayers = DisableBitmaskInx(region.NavigationLayers, 1);

            NavigationAgent3D agent = GetNode<NavigationAgent3D>("NavigationAgent2D");
            // Khiến các truy vấn đường đi sau này của agent này bỏ qua các region có layer thứ 4.
            agent.NavigationLayers = DisableBitmaskInx(agent.NavigationLayers, 4);

            uint pathQueryNavigationLayers = 0;
            pathQueryNavigationLayers = EnableBitmaskInx(pathQueryNavigationLayers, 2);
            // Lấy một đường đi chỉ xét các region thuộc layer thứ 2.
            Vector3[] path = NavigationServer3D.MapGetPath(
                _map,
                _startPosition,
                _targetPosition,
                true,
                pathQueryNavigationLayers
            );
        }

        private static bool IsBitmaskInxEnabled(uint bitmask, int index)
        {
            return (bitmask & (1 << index)) != 0;
        }

        private static uint EnableBitmaskInx(uint bitmask, int index)
        {
            return bitmask | (1u << index);
        }

        private static uint DisableBitmaskInx(uint bitmask, int index)
        {
            return bitmask & ~(1u << index);
        }
    }

Thay đổi navigation layer cho các truy vấn đường đi là một giải pháp thân thiện với hiệu năng thay cho việc bật / tắt toàn bộ navigation region. So với việc thay đổi region, một truy vấn đường đi với các navigation layer khác nhau không kích hoạt các cập nhật quy mô lớn trên NavigationServer.

Việc thay đổi navigation layer của các node NavigationAgent sẽ có hiệu lực ngay lập tức trong truy vấn đường đi tiếp theo. Việc thay đổi navigation layer của các region sẽ có hiệu lực sau lần đồng bộ NavigationServer tiếp theo.
