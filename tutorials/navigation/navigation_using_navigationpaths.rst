.. _doc_navigation_using_navigationpaths:

Sử dụng NavigationPaths
=======================

Lấy một NavigationPath
----------------------

Các navigation path có thể được truy vấn trực tiếp từ NavigationServer và không yêu cầu thêm node hoặc object nào, miễn là navigation map có navigation mesh để sử dụng.

Để lấy một path 2D, hãy sử dụng ``NavigationServer2D.map_get_path(map, from, to, optimize, navigation_layers)``.

Để lấy một path 3D, hãy sử dụng ``NavigationServer3D.map_get_path(map, from, to, optimize, navigation_layers)``.

Để thực hiện các truy vấn navigation path có khả năng tùy biến cao hơn và yêu cầu thiết lập bổ sung, hãy xem :ref:`doc_navigation_using_navigationpathqueryobjects`.

Một trong các tham số bắt buộc của truy vấn là RID của navigation map. Mỗi game world đều có một navigation map mặc định được tự động tạo. Có thể lấy các navigation map mặc định bằng ``get_world_2d().get_navigation_map()`` từ bất kỳ node kế thừa Node2D nào hoặc bằng ``get_world_3d().get_navigation_map()`` từ bất kỳ node kế thừa Node3D nào. Tham số thứ hai và thứ ba là vị trí bắt đầu và vị trí đích dưới dạng Vector2 đối với 2D hoặc Vector3 đối với 3D.

Nếu tham số ``optimized`` là ``true``, các vị trí trên path sẽ được rút ngắn dọc theo các góc polygon bằng một lượt chạy thêm của funnel algorithm. Cách này hoạt động tốt khi di chuyển tự do trên các navigation mesh có các polygon không đồng đều về kích thước, vì path sẽ bám quanh các góc dọc theo corridor của polygon được tìm thấy bởi thuật toán A*. Với các cell nhỏ, thuật toán A* tạo ra một corridor funnel rất hẹp, có thể tạo ra các path góc xấu khi sử dụng với grid.

Nếu tham số ``optimized`` là ``false``, các vị trí trên path sẽ được đặt tại tâm của mỗi cạnh polygon. Cách này hoạt động tốt khi di chuyển thuần grid trên các navigation mesh có các polygon có kích thước bằng nhau, vì path sẽ đi qua tâm của các cell trong grid. Khi ở ngoài grid, do các polygon thường bao phủ những khu vực mở rộng lớn bằng một cạnh dài duy nhất, cách này có thể tạo ra các path với những đường vòng dài không cần thiết.


.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    # Truy vấn cơ bản cho một navigation path bằng navigation map mặc định.

    func get_navigation_path(p_start_position: Vector2, p_target_position: Vector2) -> PackedVector2Array:
        if not is_inside_tree():
            return PackedVector2Array()

        var default_map_rid: RID = get_world_2d().get_navigation_map()
        var path: PackedVector2Array = NavigationServer2D.map_get_path(
            default_map_rid,
            p_start_position,
            p_target_position,
            true
        )
        return path

 .. code-tab:: csharp 2D C#

    using Godot;
    using System;

    public partial class MyNode2D : Node2D
    {
        // Truy vấn cơ bản cho một navigation path bằng navigation map mặc định.

        private Vector2[] GetNavigationPath(Vector2 startPosition, Vector2 targetPosition)
        {
            if (!IsInsideTree())
            {
                return Array.Empty<Vector2>();
            }

            Rid defaultMapRid = GetWorld2D().NavigationMap;
            Vector2[] path = NavigationServer2D.MapGetPath(
                defaultMapRid,
                startPosition,
                targetPosition,
                true
            );
            return path;
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    # Truy vấn cơ bản cho một navigation path bằng navigation map mặc định.

    func get_navigation_path(p_start_position: Vector3, p_target_position: Vector3) -> PackedVector3Array:
        if not is_inside_tree():
            return PackedVector3Array()

        var default_map_rid: RID = get_world_3d().get_navigation_map()
        var path: PackedVector3Array = NavigationServer3D.map_get_path(
            default_map_rid,
            p_start_position,
            p_target_position,
            true
        )
        return path

 .. code-tab:: csharp 3D C#

    using Godot;
    using System;

    public partial class MyNode3D : Node3D
    {
        // Truy vấn cơ bản cho một navigation path bằng navigation map mặc định.

        private Vector3[] GetNavigationPath(Vector3 startPosition, Vector3 targetPosition)
        {
            if (!IsInsideTree())
            {
                return Array.Empty<Vector3>();
            }

            Rid defaultMapRid = GetWorld3D().NavigationMap;
            Vector3[] path = NavigationServer3D.MapGetPath(
                defaultMapRid,
                startPosition,
                targetPosition,
                true
            );
            return path;
        }
    }

Một ``path`` được NavigationServer trả về sẽ là một ``PackedVector2Array`` đối với 2D hoặc một ``PackedVector3Array`` đối với 3D. Đây chỉ là các ``Array`` của các vector vị trí được tối ưu hóa bộ nhớ. Tất cả các vector vị trí bên trong array đều được đảm bảo nằm trong một NavigationPolygon hoặc NavigationMesh. Nếu không rỗng, array path sẽ có vị trí trên navigation mesh gần vị trí bắt đầu nhất tại vị trí chỉ mục đầu tiên ``path[0]``. Vị trí trên navigation mesh khả dụng gần vị trí đích nhất là vị trí chỉ mục cuối cùng ``path[path.size()-1]``. Tất cả các chỉ mục ở giữa là những điểm trên path mà actor nên đi theo để đến đích mà không rời khỏi navigation mesh.

.. note::

    Nếu vị trí đích nằm trên một navigation mesh khác chưa được hợp nhất hoặc kết nối, navigation path sẽ dẫn đến vị trí khả dụng gần nhất trên navigation mesh tại vị trí bắt đầu.

Script sau di chuyển một node kế thừa Node3D dọc theo một navigation path bằng navigation map mặc định, bằng cách thiết lập vị trí đích với ``set_movement_target()``.

.. tabs::
 .. code-tab:: gdscript GDScript

    @onready var default_3d_map_rid: RID = get_world_3d().get_navigation_map()

    var movement_speed: float = 4.0
    var movement_delta: float
    var path_point_margin: float = 0.5

    var current_path_index: int = 0
    var current_path_point: Vector3
    var current_path: PackedVector3Array

    func set_movement_target(target_position: Vector3):

        var start_position: Vector3 = global_transform.origin

        current_path = NavigationServer3D.map_get_path(
            default_3d_map_rid,
            start_position,
            target_position,
            true
        )

        if not current_path.is_empty():
            current_path_index = 0
            current_path_point = current_path[0]

    func _physics_process(delta):

        if current_path.is_empty():
            return

        movement_delta = movement_speed * delta

        if global_transform.origin.distance_to(current_path_point) <= path_point_margin:
            current_path_index += 1
            if current_path_index >= current_path.size():
                current_path = []
                current_path_index = 0
                current_path_point = global_transform.origin
                return

        current_path_point = current_path[current_path_index]

        var new_velocity: Vector3 = global_transform.origin.direction_to(current_path_point) * movement_delta

        global_transform.origin = global_transform.origin.move_toward(global_transform.origin + new_velocity, movement_delta)

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private Rid _default3DMapRid;

        private float _movementSpeed = 4.0f;
        private float _movementDelta;
        private float _pathPointMargin = 0.5f;

        private int _currentPathIndex = 0;
        private Vector3 _currentPathPoint;
        private Vector3[] _currentPath;

        public override void _Ready()
        {
            _default3DMapRid = GetWorld3D().NavigationMap;
        }

        private void SetMovementTarget(Vector3 targetPosition)
        {
            Vector3 startPosition = GlobalTransform.Origin;

            _currentPath = NavigationServer3D.MapGetPath(_default3DMapRid, startPosition, targetPosition, true);

            if (!_currentPath.IsEmpty())
            {
                _currentPathIndex = 0;
                _currentPathPoint = _currentPath[0];
            }
        }

        public override void _PhysicsProcess(double delta)
        {
            if (_currentPath.IsEmpty())
            {
                return;
            }

            _movementDelta = _movementSpeed * (float)delta;

            if (GlobalTransform.Origin.DistanceTo(_currentPathPoint) <= _pathPointMargin)
            {
                _currentPathIndex += 1;
                if (_currentPathIndex >= _currentPath.Length)
                {
                    _currentPath = Array.Empty<Vector3>();
                    _currentPathIndex = 0;
                    _currentPathPoint = GlobalTransform.Origin;
                    return;
                }
            }

            _currentPathPoint = _currentPath[_currentPathIndex];

            Vector3 newVelocity = GlobalTransform.Origin.DirectionTo(_currentPathPoint) * _movementDelta;
            var globalTransform = GlobalTransform;
            globalTransform.Origin = globalTransform.Origin.MoveToward(globalTransform.Origin + newVelocity, _movementDelta);
            GlobalTransform = globalTransform;
        }
    }
