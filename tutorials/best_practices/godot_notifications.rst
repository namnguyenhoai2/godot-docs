.. _doc_godot_notifications:

Thông báo của Godot
===================

Mỗi Object trong Godot đều triển khai một
:ref:`_notification <class_Object_private_method__notification>` method. Its purpose is to
cho phép Object phản hồi nhiều callback ở cấp engine có thể liên quan đến nó. Ví dụ, nếu engine thông báo cho một
:ref:`CanvasItem <class_CanvasItem>` to "draw", it will call
``_notification(NOTIFICATION_DRAW)``.

Một số thông báo này, chẳng hạn như draw, rất hữu ích khi override trong script. Đến mức Godot cung cấp nhiều thông báo trong số đó dưới dạng các hàm chuyên biệt:

- ``_ready()``: ``NOTIFICATION_READY``

- ``_enter_tree()``: ``NOTIFICATION_ENTER_TREE``

- ``_exit_tree()``: ``NOTIFICATION_EXIT_TREE``

- ``_process(delta)``: ``NOTIFICATION_PROCESS``

- ``_physics_process(delta)``: ``NOTIFICATION_PHYSICS_PROCESS``

- ``_draw()``: ``NOTIFICATION_DRAW``

Điều mà người dùng có thể *không* nhận ra là thông báo cũng tồn tại cho các type khác ngoài Node, chẳng hạn như:

- :ref:`Object::NOTIFICATION_POSTINITIALIZE <class_Object_constant_NOTIFICATION_POSTINITIALIZE>`: callback được kích hoạt trong quá trình khởi tạo object. Không thể truy cập từ script.

- :ref:`Object::NOTIFICATION_PREDELETE <class_Object_constant_NOTIFICATION_PREDELETE>`: callback được kích hoạt trước khi engine xóa một Object, tức là một "destructor".

Và nhiều callback *có* tồn tại trong Node không có method chuyên biệt, nhưng vẫn khá hữu ích.

- :ref:`Node::NOTIFICATION_PARENTED <class_Node_constant_NOTIFICATION_PARENTED>`: callback được kích hoạt mỗi khi bạn thêm một node con vào node khác.

- :ref:`Node::NOTIFICATION_UNPARENTED <class_Node_constant_NOTIFICATION_UNPARENTED>`: callback được kích hoạt mỗi khi bạn xóa một node con khỏi node khác.

Method ``_notification()`` dùng chung cung cấp quyền truy cập vào tất cả các thông báo tùy chỉnh này.

.. note::
  Các method trong tài liệu được gắn nhãn là "virtual" cũng được thiết kế để script override.

  Một ví dụ kinh điển là
  :ref:`_init <class_Object_private_method__init>` method in Object. While it has no
  tương đương với ``NOTIFICATION_*``, engine vẫn gọi method này. Hầu hết các ngôn ngữ (ngoại trừ C#) đều dựa vào nó như một constructor.

Vậy khi nào bạn nên sử dụng từng thông báo hoặc hàm virtual này?

_process so với _physics_process so với \*_input
------------------------------------------------

Sử dụng ``_process()`` khi bạn cần delta time phụ thuộc vào framerate giữa các frame. Nếu code cập nhật dữ liệu của object cần được cập nhật thường xuyên nhất có thể, đây là nơi phù hợp. Các lần kiểm tra logic lặp lại và việc caching dữ liệu thường được thực hiện tại đây, nhưng điều đó phụ thuộc vào tần suất cần cập nhật các phép đánh giá. Nếu chúng không cần thực thi ở mỗi frame, thì triển khai một vòng lặp Timer-timeout là một lựa chọn khác.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Cho phép thực hiện các thao tác lặp lại mà không kích hoạt logic của script
    # ở mỗi frame (hoặc thậm chí ở mỗi fixed frame).
    func _ready():
        var timer = Timer.new()
        timer.autostart = true
        timer.wait_time = 0.5
        add_child(timer)
        timer.timeout.connect(func():
            print("This block runs every 0.5 seconds")
        )

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {
        // Cho phép thực hiện các thao tác lặp lại mà không kích hoạt logic của script
        // ở mỗi frame (hoặc thậm chí ở mỗi fixed frame).
        public override void _Ready()
        {
            var timer = new Timer();
            timer.Autostart = true;
            timer.WaitTime = 0.5;
            AddChild(timer);
            timer.Timeout += () => GD.Print("This block runs every 0.5 seconds");
        }
    }

 .. code-tab:: cpp C++

    using namespace godot;

    class MyNode : public Node {
        GDCLASS(MyNode, Node)

    public:
        // Cho phép thực hiện các thao tác lặp lại mà không kích hoạt logic của script
        // ở mỗi frame (hoặc thậm chí ở mỗi fixed frame).
        virtual void _ready() override {
            Timer *timer = memnew(Timer);
            timer->set_autostart(true);
            timer->set_wait_time(0.5);
            add_child(timer);
            timer->connect("timeout", callable_mp(this, &MyNode::run));
        }

        void run() {
            UtilityFunctions::print("This block runs every 0.5 seconds.");
        }
    };

Sử dụng ``_physics_process()`` khi bạn cần delta time độc lập với framerate giữa các frame. Nếu code cần được cập nhật nhất quán theo thời gian, bất kể thời gian trôi nhanh hay chậm, đây là nơi phù hợp. Các thao tác kinematic và biến đổi transform của object lặp lại nên được thực hiện tại đây.

Mặc dù có thể làm vậy, để đạt hiệu năng tốt nhất, bạn nên tránh thực hiện việc kiểm tra input trong các callback này. ``_process()`` và ``_physics_process()`` sẽ được kích hoạt ở mọi cơ hội (theo mặc định, chúng không "nghỉ"). Ngược lại, các callback ``*_input()`` sẽ chỉ được kích hoạt ở những frame mà engine thực sự phát hiện input.

Bạn vẫn có thể kiểm tra các input action trong các input callback theo cách tương tự. Nếu muốn sử dụng delta time, bạn có thể lấy nó từ các method delta time liên quan khi cần.

.. tabs::
  .. code-tab:: gdscript GDScript

    # Được gọi ở mỗi frame, ngay cả khi engine không phát hiện input.
    func _process(delta):
        if Input.is_action_just_pressed("ui_select"):
            print(delta)

    # Được gọi trong mỗi sự kiện input.
    func _unhandled_input(event):
        match event.get_class():
            "InputEventKey":
                if Input.is_action_just_pressed("ui_accept"):
                    print(get_process_delta_time())

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {

        // Được gọi ở mỗi frame, ngay cả khi engine không phát hiện input.
        public void _Process(double delta)
        {
            if (Input.IsActionJustPressed("ui_select"))
            {
                GD.Print(delta);
            }
        }

        // Được gọi trong mỗi sự kiện input. Điều này cũng đúng với _input().
        public void _UnhandledInput(InputEvent @event)
        {
            switch (@event)
            {
                case InputEventKey:
                    if (Input.IsActionJustPressed("ui_accept"))
                    {
                        GD.Print(GetProcessDeltaTime());
                    }
                    break;
            }
        }

    }

  .. code-tab:: cpp C++

    using namespace godot;

    class MyNode : public Node {
        GDCLASS(MyNode, Node)

    public:
        // Được gọi ở mỗi frame, ngay cả khi engine không phát hiện input.
        virtual void _process(double p_delta) override {
            if (Input::get_singleton->is_action_just_pressed("ui_select")) {
                UtilityFunctions::print(p_delta);
            }
        }

        // Được gọi trong mỗi sự kiện input. Điều này cũng đúng với _input().
        virtual void _unhandled_input(const Ref<InputEvent> &p_event) override {
            Ref<InputEventKey> key_event = event;
            if (key_event.is_valid() && Input::get_singleton->is_action_just_pressed("ui_accept")) {
                UtilityFunctions::print(get_process_delta_time());
            }
        }
    };

_init so với initialization so với export
-----------------------------------------

Nếu script khởi tạo subtree node của riêng nó mà không có scene, code đó nên được thực thi trong ``_init()``. Các quá trình khởi tạo property khác hoặc không phụ thuộc vào SceneTree cũng nên chạy tại đây.

.. note::
  Tương đương trong C# với method ``_init()`` của GDScript là constructor.

``_init()`` được kích hoạt trước ``_enter_tree()`` hoặc ``_ready()``, nhưng sau khi script tạo và khởi tạo các property của nó. Khi instantiate một scene, các giá trị property sẽ được thiết lập theo trình tự sau:

1. **Gán giá trị ban đầu:** property được gán giá trị khởi tạo hoặc giá trị mặc định nếu không chỉ định giá trị khởi tạo. Nếu có setter, setter sẽ không được sử dụng.

2. **Gán ``_init()``:** giá trị của property được thay thế bằng mọi phép gán được thực hiện trong ``_init()``, kích hoạt setter.

3. **Gán giá trị export:** giá trị của property được export một lần nữa bị thay thế bằng bất kỳ giá trị nào được đặt trong Inspector, kích hoạt setter.

.. tabs::
  .. code-tab:: gdscript GDScript

    # test được khởi tạo thành "one" mà không kích hoạt setter.
    @export var test: String = "one":
        set(value):
            test = value + "!"

    func _init():
        # Kích hoạt setter, thay đổi giá trị của test từ "one" thành "two!".
        test = "two"

    # Nếu bạn đặt test thành "three" trong Inspector, thao tác đó sẽ kích hoạt
    # setter, thay đổi giá trị của test từ "two!" thành "three!".

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {
        private string _test = "one";

        [Export]
        public string Test
        {
            get { return _test; }
            set { _test = $"{value}!"; }
        }

        public MyNode()
        {
            // Kích hoạt setter, thay đổi giá trị của _test từ "one" thành "two!".
            Test = "two";
        }

        // Nếu bạn đặt Test thành "three" trong Inspector, thao tác đó sẽ kích hoạt
        // setter, thay đổi giá trị của _test từ "two!" thành "three!".
    }

  .. code-tab:: cpp C++

    using namespace godot;

    class MyNode : public Node {
        GDCLASS(MyNode, Node)

        String test = "one";

    protected:
        static void _bind_methods() {
            ClassDB::bind_method(D_METHOD("get_test"), &MyNode::get_test);
            ClassDB::bind_method(D_METHOD("set_test", "test"), &MyNode::set_test);
            ADD_PROPERTY(PropertyInfo(Variant::STRING, "test"), "set_test", "get_test");
        }

    public:
        String get_test() { return test; }
        void set_test(String p_test) { test = p_test + "!"; }

        MyNode() {
            // Kích hoạt setter, thay đổi giá trị của _test từ "one" thành "two!".
            set_test("two");
        }

        // Nếu bạn đặt test thành "three" trong Inspector, thao tác đó sẽ kích hoạt
        // setter, thay đổi giá trị của test từ "two!" thành "three!".
    };

Do đó, việc instantiate một script thay vì một scene có thể ảnh hưởng đến cả quá trình khởi tạo *và* số lần engine gọi setter.

_ready so với _enter_tree so với NOTIFICATION_PARENTED
------------------------------------------------------

Khi instantiate một scene được kết nối với scene đầu tiên được thực thi, Godot sẽ instantiate các node theo chiều đi xuống trong tree (thực hiện các lời gọi ``_init()``) và xây dựng tree theo hướng đi xuống từ root. Điều này khiến các lời gọi ``_enter_tree()`` lan truyền xuống tree. Khi tree hoàn tất, các node lá gọi ``_ready``. Một node sẽ gọi method này sau khi tất cả node con đã hoàn tất việc gọi method của chúng. Việc này sau đó tạo ra một làn sóng ngược đi lên về phía root của tree.

Khi instantiate một script hoặc một scene độc lập, các node không được thêm vào SceneTree lúc tạo, vì vậy không có callback ``_enter_tree()`` nào được kích hoạt. Thay vào đó, chỉ có lời gọi ``_init()`` diễn ra. Khi scene được thêm vào SceneTree, các lời gọi ``_enter_tree()`` và ``_ready()`` sẽ diễn ra.

Nếu cần kích hoạt hành vi xảy ra khi các node trở thành node cha của node khác, bất kể việc đó xảy ra như một phần của scene chính/đang hoạt động hay không, bạn có thể sử dụng thông báo :ref:`PARENTED <class_Node_constant_NOTIFICATION_PARENTED>`. Ví dụ, sau đây là một đoạn mã kết nối method của một node với một signal tùy chỉnh trên node cha mà không gây lỗi. Hữu ích cho các node tập trung vào dữ liệu có thể được tạo trong runtime.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node

    var parent_cache

    func connection_check():
        return parent_cache.has_user_signal("interacted_with")

    func _notification(what):
        match what:
            NOTIFICATION_PARENTED:
                parent_cache = get_parent()
                if connection_check():
                    parent_cache.interacted_with.connect(_on_parent_interacted_with)
            NOTIFICATION_UNPARENTED:
                if connection_check():
                    parent_cache.interacted_with.disconnect(_on_parent_interacted_with)

    func _on_parent_interacted_with():
        print("I'm reacting to my parent's interaction!")

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {
        private Node _parentCache;

        public bool ConnectionCheck()
        {
            return _parentCache.HasUserSignal("InteractedWith");
        }

        public override void _Notification(int what)
        {
            switch ((long)what)
            {
                case NotificationParented:
                    _parentCache = GetParent();
                    if (ConnectionCheck())
                    {
                        _parentCache.Connect("InteractedWith", Callable.From(OnParentInteractedWith));
                    }
                    break;
                case NotificationUnparented:
                    if (ConnectionCheck())
                    {
                        _parentCache.Disconnect("InteractedWith", Callable.From(OnParentInteractedWith));
                    }
                    break;
            }
        }

        private void OnParentInteractedWith()
        {
            GD.Print("I'm reacting to my parent's interaction!");
        }
    }

  .. code-tab:: cpp C++

    using namespace godot;

    class MyNode : public Node {
        GDCLASS(MyNode, Node)

        Node *parent_cache = nullptr;

        void on_parent_interacted_with() {
            UtilityFunctions::print("I'm reacting to my parent's interaction!");
        }

    public:
        void connection_check() {
            return parent_cache->has_user_signal("interacted_with");
        }

        void _notification(int p_what) {
            switch (p_what) {
                case NOTIFICATION_PARENTED:
                    parent_cache = get_parent();
                    if (connection_check()) {
                        parent_cache->connect("interacted_with", callable_mp(this, &MyNode::on_parent_interacted_with));
                    }
                    break;
                case NOTIFICATION_UNPARENTED:
                    if (connection_check()) {
                        parent_cache->disconnect("interacted_with", callable_mp(this, &MyNode::on_parent_interacted_with));
                    }
                    break;
            }
        }
    };
