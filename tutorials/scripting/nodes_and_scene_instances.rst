.. _doc_nodes_and_scene_instances:

Node và instance của scene
==========================

Hướng dẫn này giải thích cách lấy node, tạo node, thêm node làm node con và instantiate scene bằng code.

.. seealso::

    Xem tutorial :ref:`doc_instancing` để tìm hiểu về cách Godot xử lý việc instancing scene.

Lấy node
--------

Bạn có thể lấy một reference đến node bằng cách gọi method :ref:`Node.get_node() <class_Node_method_get_node>`. Để cách này hoạt động, node con phải có mặt trong scene tree. Việc lấy node trong hàm ``_ready()`` của node cha sẽ đảm bảo điều đó.

Ví dụ, nếu bạn có một scene tree như sau và muốn lấy reference đến các node Sprite2D và Camera2D để truy cập chúng trong script.

.. image:: img/nodes_and_scene_instances_player_scene_example.webp

Để làm vậy, bạn có thể sử dụng đoạn code sau.

.. tabs::
 .. code-tab:: gdscript GDScript

    var sprite2d
    var camera2d

    func _ready():
        sprite2d = get_node("Sprite2D")
        camera2d = get_node("Camera2D")

 .. code-tab:: csharp

    private Sprite2D _sprite2D;
    private Camera2D _camera2D;

    public override void _Ready()
    {
        base._Ready();

        _sprite2D = GetNode<Sprite2D>("Sprite2D");
        _camera2D = GetNode<Camera2D>("Camera2D");
    }

Lưu ý rằng bạn lấy node bằng tên của chúng, không phải bằng type. Ở trên, "Sprite2D" và "Camera2D" là tên của các node trong scene.

.. image:: img/nodes_and_scene_instances_sprite_node.webp

Nếu bạn đổi tên node Sprite2D thành Skin trong Scene dock, bạn phải đổi dòng lấy node thành ``get_node("Skin")`` trong script.

.. image:: img/nodes_and_scene_instances_sprite_node_renamed.webp

Đường dẫn node
--------------

Khi lấy reference đến một node, bạn không bị giới hạn ở việc lấy node con trực tiếp. Hàm ``get_node()`` hỗ trợ các path, tương tự như khi làm việc với file browser. Thêm dấu gạch chéo để phân tách các node.

Hãy xem scene ví dụ sau, trong đó script được gắn vào node UserInterface.

.. image:: img/nodes_and_scene_instances_ui_scene_example.webp

Để lấy node AnimationPlayer, bạn sẽ sử dụng đoạn code sau.

.. tabs::
 .. code-tab:: gdscript GDScript

    var animation_player

    func _ready():
        animation_player = get_node("ShieldBar/AnimationPlayer")

 .. code-tab:: csharp

    private AnimationPlayer _animationPlayer;

    public override void _Ready()
    {
        base._Ready();

        _animationPlayer = GetNode<AnimationPlayer>("ShieldBar/AnimationPlayer");
    }

.. note:: As with file paths, you can use ".." to get a parent node. The best
          tuy nhiên, bạn nên tránh làm vậy để không phá vỡ tính đóng gói (encapsulation). Bạn cũng có thể bắt đầu path bằng dấu gạch chéo xuôi để biến nó thành path tuyệt đối; trong trường hợp đó, node ở trên cùng của bạn sẽ là "/root", viewport gốc được định sẵn của ứng dụng.

Cú pháp viết tắt
~~~~~~~~~~~~~~~~

Bạn có thể sử dụng hai cách viết tắt để rút gọn code trong GDScript. Trước tiên, đặt annotation ``@onready`` trước một member variable sẽ khiến nó được khởi tạo ngay trước callback ``_ready()``.

.. code-block:: gdscript

    @onready var sprite2d = get_node("Sprite2D")

Ngoài ra còn có cách viết ngắn gọn cho ``get_node()``: dấu đô la, "$". Bạn đặt nó trước tên hoặc path của node muốn lấy.

.. code-block:: gdscript

    @onready var sprite2d = $Sprite2D
    @onready var animation_player = $ShieldBar/AnimationPlayer

Tạo node
--------

Để tạo một node bằng code, hãy gọi method ``new()`` của node đó, giống như với mọi datatype dựa trên class khác.

Bạn có thể lưu reference của node vừa tạo vào một biến và gọi ``add_child()`` để thêm nó làm node con của node mà bạn đã gắn script.

.. tabs::
 .. code-tab:: gdscript GDScript

    var sprite2d

    func _ready():
        sprite2d = Sprite2D.new() # Tạo một Sprite2D mới.
        add_child(sprite2d) # Thêm nó làm node con của node này.

 .. code-tab:: csharp

    private Sprite2D _sprite2D;

    public override void _Ready()
    {
        base._Ready();

        _sprite2D = new Sprite2D(); // Tạo một Sprite2D mới.
        AddChild(_sprite2D); // Thêm nó làm node con của node này.
    }

Để xóa một node và giải phóng nó khỏi bộ nhớ, bạn có thể gọi method ``queue_free()`` của node đó. Thao tác này đưa node vào hàng đợi để xóa vào cuối frame hiện tại, sau khi node đã xử lý xong. Khi đó, engine sẽ xóa node khỏi scene và giải phóng object trong bộ nhớ.

.. tabs::
 .. code-tab:: gdscript GDScript

    sprite2d.queue_free()

 .. code-tab:: csharp

    _sprite2D.QueueFree();

Trước khi gọi ``sprite2d.queue_free()``, remote scene tree trông như sau.

.. image:: img/nodes_and_scene_instances_remote_tree_with_sprite.webp

Sau khi engine giải phóng node, remote scene tree không còn hiển thị sprite nữa.

.. image:: img/nodes_and_scene_instances_remote_tree_no_sprite.webp

Ngoài ra, bạn có thể gọi ``free()`` để hủy node ngay lập tức. Bạn nên thận trọng khi làm vậy vì mọi reference đến node sẽ ngay lập tức trở nên không hợp lệ. Chúng tôi khuyến nghị sử dụng ``queue_free()`` trừ khi bạn biết mình đang làm gì.

Khi giải phóng một node, engine cũng giải phóng tất cả node con của nó. Nhờ vậy, để xóa toàn bộ một nhánh của scene tree, bạn chỉ cần giải phóng node cha ở trên cùng.

Instancing scene
----------------

Scene là các template mà từ đó bạn có thể tạo bao nhiêu bản sao tùy thích. Thao tác này được gọi là instancing, và thực hiện bằng code gồm hai bước:

1. 1. Tải scene từ ổ đĩa cục bộ. 2. Tạo một instance của resource :ref:`PackedScene <class_PackedScene>` đã tải.

.. tabs::
 .. code-tab:: gdscript GDScript

    var scene = load("res://my_scene.tscn")

 .. code-tab:: csharp

    var scene = GD.Load<PackedScene>("res://MyScene.tscn");

Preload scene có thể cải thiện trải nghiệm của người dùng vì thao tác load diễn ra khi compiler đọc script chứ không phải trong runtime. Tính năng này chỉ khả dụng với GDScript.

.. tabs::
 .. code-tab:: gdscript GDScript

    var scene = preload("res://my_scene.tscn")

Khi đó, ``scene`` là một packed scene resource, không phải một node. Để tạo node thực tế, bạn cần gọi :ref:`PackedScene.instantiate() <class_PackedScene_method_instantiate>`. Method này trả về một cây node mà bạn có thể sử dụng làm node con của node hiện tại.

.. tabs::
 .. code-tab:: gdscript GDScript

    var instance = scene.instantiate()
    add_child(instance)

 .. code-tab:: csharp

    var instance = scene.Instantiate();
    AddChild(instance);

Ưu điểm của quy trình hai bước này là bạn có thể giữ một packed scene đã load và tạo các instance mới ngay khi cần. Ví dụ, để nhanh chóng instance nhiều enemy hoặc bullet.
