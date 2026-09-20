.. _doc_overridable_functions:

Các hàm có thể ghi đè
=====================

Lớp Node của Godot cung cấp các hàm virtual mà bạn có thể ghi đè để cập nhật node ở mỗi frame hoặc khi xảy ra các sự kiện cụ thể, chẳng hạn như khi chúng đi vào scene tree.

Tài liệu này trình bày những hàm bạn sẽ sử dụng thường xuyên nhất.

.. seealso:: Under the hood, these functions rely on Godot's low-level
             hệ thống notifications. Để tìm hiểu thêm về hệ thống này, hãy xem
             :ref:`doc_godot_notifications`.

Hai hàm cho phép bạn khởi tạo và lấy các node ngoài constructor của class: ``_enter_tree()`` và ``_ready()``.

Khi node đi vào Scene Tree, nó sẽ hoạt động và engine gọi phương thức ``_enter_tree()`` của node đó. Các node con của node này có thể chưa thuộc scene đang hoạt động. Vì bạn có thể xóa node khỏi scene tree rồi thêm lại, hàm này có thể được gọi nhiều lần trong suốt vòng đời của node.

Trong hầu hết trường hợp, thay vào đó bạn sẽ sử dụng ``_ready()``. Hàm này chỉ được gọi một lần trong vòng đời của node, sau ``_enter_tree()``. ``_ready()`` đảm bảo rằng tất cả node con đã đi vào scene tree trước, để bạn có thể gọi ``get_node()`` trên chúng một cách an toàn.

.. seealso:: To learn more about getting node references, read
             :ref:`doc_nodes_and_scene_instances`.

Một callback liên quan khác là ``_exit_tree()``, được engine gọi mỗi khi một node sắp rời khỏi scene tree. Điều này có thể xảy ra khi bạn gọi :ref:`Node.remove_child() <class_Node_method_remove_child>` hoặc khi bạn giải phóng một node.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được gọi mỗi khi node đi vào scene tree.
    func _enter_tree():
        pass

    # Được gọi khi cả node và các node con của nó đã đi vào scene tree.
    func _ready():
        pass

    # Được gọi khi node sắp rời khỏi scene tree, sau khi tất cả các node con của nó
    # đã nhận callback _exit_tree().
    func _exit_tree():
        pass

 .. code-tab:: csharp

    // Được gọi mỗi khi node đi vào scene tree.
    public override void _EnterTree()
    {
        base._EnterTree();
    }

    // Được gọi khi cả node và các node con của nó đã đi vào scene tree.
    public override void _Ready()
    {
        base._Ready();
    }

    // Được gọi khi node sắp rời khỏi scene tree, sau khi tất cả các node con của nó
    // đã rời khỏi scene tree.
    public override void _ExitTree()
    {
        base._ExitTree();
    }

Hai phương thức virtual ``_process()`` và ``_physics_process()`` cho phép bạn cập nhật node lần lượt ở mỗi frame và mỗi physics frame. Để biết thêm thông tin, hãy đọc tài liệu chuyên biệt:
:ref:`doc_idle_and_physics_processing`.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được gọi ở mỗi frame.
    func _process(delta):
        pass

    # Được gọi ở mỗi physics frame.
    func _physics_process(delta):
        pass

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        // Được gọi ở mỗi frame.
        base._Process(delta);
    }

    public override void _PhysicsProcess(double delta)
    {
        // Được gọi ở mỗi physics frame.
        base._PhysicsProcess(delta);
    }

Hai hàm callback tích hợp thiết yếu khác của node là
:ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>` and
:ref:`Node._input() <class_Node_private_method__input>`, which you use to both receive
và xử lý từng input event riêng lẻ. Phương thức ``_unhandled_input()`` nhận mọi lần nhấn phím, cú nhấp chuột, v.v. chưa được xử lý trong callback ``_input()`` hoặc trong một component giao diện người dùng. Bạn nên sử dụng phương thức này cho input gameplay nói chung. Callback ``_input()`` cho phép bạn chặn và xử lý các input event trước khi ``_unhandled_input()`` nhận chúng.

Để tìm hiểu thêm về input trong Godot, hãy xem :ref:`Input section <toc-learn-features-inputs>`.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Được gọi một lần cho mỗi event.
    func _unhandled_input(event):
        pass

    # Được gọi một lần cho mỗi event trước _unhandled_input(), cho phép bạn
    # tiêu thụ một số event.
    func _input(event):
        pass

 .. code-tab:: csharp

    // Được gọi một lần cho mỗi event.
    public override void _UnhandledInput(InputEvent @event)
    {
        base._UnhandledInput(@event);
    }

    // Được gọi một lần cho mỗi event trước _UnhandledInput(), cho phép bạn
    // tiêu thụ một số event.
    public override void _Input(InputEvent @event)
    {
        base._Input(@event);
    }

Có thêm một số hàm có thể ghi đè như
:ref:`Node._get_configuration_warnings()
<class_Node_private_method__get_configuration_warnings>`. Các loại node chuyên biệt cung cấp thêm những callback như :ref:`CanvasItem._draw() <class_CanvasItem_private_method__draw>` để vẽ bằng lập trình hoặc :ref:`Control._gui_input() <class_Control_private_method__gui_input>` để xử lý thao tác nhấp và input trên các phần tử UI.
