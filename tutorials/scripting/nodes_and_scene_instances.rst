.. _doc_nodes_and_scene_instances:

Node và instance của scene
==========================

Hướng dẫn này giải thích cách lấy node, tạo node, thêm node làm node con và instance scene từ code.

.. seealso::

    Hãy xem hướng dẫn :ref:`doc_instancing` để tìm hiểu về cách Godot xử lý việc tạo instance của scene.

Lấy node
--------

Bạn có thể lấy tham chiếu đến một node bằng cách gọi phương thức :ref:`Node.get_node() <class_Node_method_get_node>`. Để cách này hoạt động, node con phải có trong cây scene. Việc lấy node trong hàm ``_ready()`` của node cha sẽ đảm bảo điều đó.

Ví dụ, nếu bạn có một cây scene như sau và muốn lấy tham chiếu đến các node Sprite2D và Camera2D để truy cập chúng trong script.

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

Lưu ý rằng bạn lấy node bằng tên của chúng, không phải bằng kiểu của chúng. Ở trên, "Sprite2D" và "Camera2D" là tên của các node trong scene.

.. image:: img/nodes_and_scene_instances_sprite_node.webp

Nếu đổi tên node Sprite2D thành Skin trong Scene dock, bạn phải thay đổi dòng lấy node thành ``get_node("Skin")`` trong script.

.. image:: img/nodes_and_scene_instances_sprite_node_renamed.webp

Đường dẫn node
--------------

Khi lấy tham chiếu đến một node, bạn không bị giới hạn ở việc lấy node con trực tiếp. Hàm ``get_node()`` hỗ trợ đường dẫn, tương tự như khi làm việc với trình duyệt tệp. Thêm dấu gạch chéo để phân tách các node.

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

.. note:: Tương tự đường dẫn tệp, bạn có thể dùng ".." để lấy node cha. Tuy nhiên, cách tốt nhất là tránh làm vậy để không phá vỡ tính đóng gói. Bạn cũng có thể bắt đầu đường dẫn bằng dấu gạch chéo xuôi để biến nó thành đường dẫn tuyệt đối; trong trường hợp đó, node ở trên cùng sẽ là "/root", viewport gốc được định nghĩa sẵn của ứng dụng.

Cú pháp rút gọn
~~~~~~~~~~~~~~~

Bạn có thể dùng hai cách viết tắt để rút gọn code trong GDScript. Đầu tiên, đặt annotation ``@onready`` trước một biến thành viên sẽ khiến biến đó được khởi tạo ngay trước callback ``_ready()``.

.. code-block:: gdscript

    @onready var sprite2d = get_node("Sprite2D")

Ngoài ra còn có cách viết ngắn cho ``get_node()``: dấu đô la, "$". Bạn đặt nó trước tên hoặc đường dẫn của node muốn lấy.

.. code-block:: gdscript

    @onready var sprite2d = $Sprite2D
    @onready var animation_player = $ShieldBar/AnimationPlayer

Tạo node
--------

Để tạo node từ code, hãy gọi phương thức ``new()`` của nó như với mọi kiểu dữ liệu dựa trên class khác.

Bạn có thể lưu tham chiếu đến node vừa tạo vào một biến và gọi ``add_child()`` để thêm node đó làm node con của node mà bạn đã gắn script.

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

Để xóa một node và giải phóng nó khỏi bộ nhớ, bạn có thể gọi phương thức ``queue_free()`` của nó. Thao tác này đưa node vào hàng đợi xóa ở cuối frame hiện tại, sau khi node hoàn tất quá trình xử lý. Khi đó, engine sẽ xóa node khỏi scene và giải phóng đối tượng trong bộ nhớ.

.. tabs::
 .. code-tab:: gdscript GDScript

    sprite2d.queue_free()

 .. code-tab:: csharp

    _sprite2D.QueueFree();

Trước khi gọi ``sprite2d.queue_free()``, cây scene từ xa trông như sau.

.. image:: img/nodes_and_scene_instances_remote_tree_with_sprite.webp

Sau khi engine giải phóng node, cây scene từ xa không còn hiển thị sprite nữa.

.. image:: img/nodes_and_scene_instances_remote_tree_no_sprite.webp

Ngoài ra, bạn có thể gọi ``free()`` để hủy node ngay lập tức. Bạn nên cẩn thận khi làm vậy vì mọi tham chiếu đến node sẽ lập tức trở nên không hợp lệ. Chúng tôi khuyến nghị sử dụng ``queue_free()`` trừ khi bạn biết rõ mình đang làm gì.

Khi giải phóng một node, tất cả node con của nó cũng được giải phóng. Nhờ đó, để xóa toàn bộ một nhánh của cây scene, bạn chỉ cần giải phóng node cha ở trên cùng.

Tạo instance của scene
----------------------

Scene là các mẫu từ đó bạn có thể tạo bao nhiêu bản sao tùy thích. Thao tác này được gọi là tạo instance, và thực hiện từ code gồm hai bước:

1. Tải scene từ ổ đĩa cục bộ.
2. Tạo một instance của resource :ref:`PackedScene <class_PackedScene>` đã tải.

.. tabs::
 .. code-tab:: gdscript GDScript

    var scene = load("res://my_scene.tscn")

 .. code-tab:: csharp

    var scene = GD.Load<PackedScene>("res://MyScene.tscn");

Việc preload scene có thể cải thiện trải nghiệm của người dùng vì thao tác tải diễn ra khi compiler đọc script thay vì trong runtime. Tính năng này chỉ có trong GDScript.

.. tabs::
 .. code-tab:: gdscript GDScript

    var scene = preload("res://my_scene.tscn")

Lúc này, ``scene`` là một resource packed scene, không phải node. Để tạo node thực tế, bạn cần gọi :ref:`PackedScene.instantiate() <class_PackedScene_method_instantiate>`. Phương thức này trả về một cây node mà bạn có thể dùng làm node con của node hiện tại.

.. tabs::
 .. code-tab:: gdscript GDScript

    var instance = scene.instantiate()
    add_child(instance)

 .. code-tab:: csharp

    var instance = scene.Instantiate();
    AddChild(instance);

Ưu điểm của quy trình hai bước này là bạn có thể giữ một packed scene đã tải và tạo các instance mới ngay trong lúc chạy. Ví dụ, để nhanh chóng tạo instance của nhiều kẻ địch hoặc đạn.
