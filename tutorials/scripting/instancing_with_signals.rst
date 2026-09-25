.. meta::
    :keywords: Signal

.. _doc_instancing_with_signals:

Tạo instance bằng signal
========================

Signal cung cấp một cách để tách rời các đối tượng trong game, giúp bạn tránh phải áp dụng một cấu trúc node cố định. Một dấu hiệu cho thấy bạn có thể cần dùng signal là khi bạn thấy mình đang sử dụng ``get_parent()``. Việc tham chiếu trực tiếp đến node cha của một node có nghĩa là bạn không thể dễ dàng di chuyển node đó đến một vị trí khác trong scene tree. Điều này có thể đặc biệt gây khó khăn khi bạn tạo instance của các đối tượng trong runtime và muốn đặt chúng ở một vị trí tùy ý trong scene tree đang chạy.

Dưới đây, chúng ta sẽ xem xét một ví dụ về tình huống như vậy: bắn đạn.

Ví dụ bắn súng
--------------

Hãy xem xét một nhân vật người chơi có thể xoay và bắn về phía chuột. Mỗi khi nút chuột được nhấp, chúng ta tạo một instance của viên đạn tại vị trí của người chơi. Xem :ref:`doc_instancing` để biết chi tiết.

Chúng ta sẽ sử dụng một ``Area2D`` cho viên đạn; viên đạn di chuyển theo đường thẳng với vận tốc cho trước:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Area2D

    var velocity = Vector2.RIGHT

    func _physics_process(delta):
        position += velocity * delta

 .. code-tab:: csharp

    using Godot;

    public partial class Bullet : Area2D
    {
        public Vector2 Velocity { get; set; } = Vector2.Right;

        public override void _PhysicsProcess(double delta)
        {
            Position += Velocity * (float)delta;
        }
    }

Tuy nhiên, nếu các viên đạn được thêm làm node con của người chơi, chúng sẽ vẫn "gắn" với người chơi khi người chơi xoay:

.. image:: img/signals_shoot1.gif

Thay vào đó, các viên đạn cần độc lập với chuyển động của người chơi - sau khi được bắn, chúng phải tiếp tục di chuyển theo đường thẳng và người chơi không thể tác động đến chúng nữa. Thay vì được thêm vào scene tree làm node con của người chơi, sẽ hợp lý hơn nếu thêm viên đạn làm node con của scene game "main", có thể là node cha của người chơi hoặc thậm chí là một node ở cao hơn trong cây.

Bạn có thể thực hiện việc này bằng cách thêm trực tiếp viên đạn vào scene main:

.. tabs::
 .. code-tab:: gdscript GDScript

    var bullet_instance = Bullet.instantiate()
    get_parent().add_child(bullet_instance)

 .. code-tab:: csharp

    Node bulletInstance = Bullet.Instantiate();
    GetParent().AddChild(bulletInstance);

Tuy nhiên, điều này sẽ dẫn đến một vấn đề khác. Nếu bây giờ bạn thử kiểm thử riêng scene "Player", game sẽ bị crash khi bắn, vì không có node cha để truy cập. Điều này khiến việc kiểm thử độc lập code của người chơi khó khăn hơn nhiều, đồng thời có nghĩa là nếu bạn quyết định thay đổi cấu trúc node của scene main, node cha của người chơi có thể không còn là node phù hợp để nhận các viên đạn.

Giải pháp cho vấn đề này là sử dụng signal để "phát" các viên đạn từ người chơi. Sau đó, người chơi không cần phải "biết" điều gì xảy ra với các viên đạn - bất kỳ node nào được kết nối với signal đều có thể "nhận" các viên đạn và thực hiện hành động phù hợp để tạo chúng.

Dưới đây là code của người chơi sử dụng signal để phát viên đạn:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    signal shoot(bullet, direction, location)

    var Bullet = preload("res://bullet.tscn")

    func _input(event):
        if event is InputEventMouseButton:
            if event.button_index == MOUSE_BUTTON_LEFT and event.pressed:
                shoot.emit(Bullet, rotation, position)

    func _process(delta):
        look_at(get_global_mouse_position())

 .. code-tab:: csharp

    using Godot;

    public partial class Player : Sprite2D
    {
        [Signal]
        public delegate void ShootEventHandler(PackedScene bullet, float direction, Vector2 location);

        private PackedScene _bullet = GD.Load<PackedScene>("res://Bullet.tscn");

        public override void _Input(InputEvent @event)
        {
            if (@event is InputEventMouseButton mouseButton)
            {
                if (mouseButton.ButtonIndex == MouseButton.Left && mouseButton.Pressed)
                {
                    EmitSignal(SignalName.Shoot, _bullet, Rotation, Position);
                }
            }
        }

        public override void _Process(double delta)
        {
            LookAt(GetGlobalMousePosition());
        }
    }

Trong scene main, chúng ta kết nối signal của người chơi (signal này sẽ xuất hiện trong tab "Node" của Inspector)

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_player_shoot(Bullet, direction, location):
        var spawned_bullet = Bullet.instantiate()
        add_child(spawned_bullet)
        spawned_bullet.rotation = direction
        spawned_bullet.position = location
        spawned_bullet.velocity = spawned_bullet.velocity.rotated(direction)

 .. code-tab:: csharp

    private void OnPlayerShoot(PackedScene bullet, float direction, Vector2 location)
    {
        var spawnedBullet = bullet.Instantiate<Bullet>();
        AddChild(spawnedBullet);
        spawnedBullet.Rotation = direction;
        spawnedBullet.Position = location;
        spawnedBullet.Velocity = spawnedBullet.Velocity.Rotated(direction);
    }

Giờ đây, các viên đạn sẽ duy trì chuyển động riêng, độc lập với việc người chơi xoay:

.. image:: img/signals_shoot2.gif
