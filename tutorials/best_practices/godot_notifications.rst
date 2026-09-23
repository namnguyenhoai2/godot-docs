.. _doc_godot_notifications:

Các notification của Godot
==========================

Mọi Object trong Godot đều triển khai một
:ref:`_notification <class_Object_private_method__notification>` method. Mục đích của nó là cho phép Object phản hồi nhiều callback ở cấp engine có thể liên quan đến nó. Ví dụ, nếu engine yêu cầu một
:ref:`CanvasItem <class_CanvasItem>` thực hiện "draw", nó sẽ gọi ``_notification(NOTIFICATION_DRAW)``.

Một số notification trong số này, chẳng hạn như draw, rất hữu ích khi override trong script. Đến mức Godot cung cấp nhiều notification trong số đó bằng các function chuyên dụng:

- ``_ready()``: ``NOTIFICATION_READY``

- ``_enter_tree()``: ``NOTIFICATION_ENTER_TREE``

- ``_exit_tree()``: ``NOTIFICATION_EXIT_TREE``

- ``_process(delta)``: ``NOTIFICATION_PROCESS``

- ``_physics_process(delta)``: ``NOTIFICATION_PHYSICS_PROCESS``

- ``_draw()``: ``NOTIFICATION_DRAW``

Điều người dùng có thể *không* nhận ra là notification tồn tại cho các type khác ngoài Node, chẳng hạn như:

- :ref:`Object::NOTIFICATION_POSTINITIALIZE <class_Object_constant_NOTIFICATION_POSTINITIALIZE>`: callback được kích hoạt trong quá trình khởi tạo object. Không thể truy cập từ script.

- :ref:`Object::NOTIFICATION_PREDELETE <class_Object_constant_NOTIFICATION_PREDELETE>`: callback được kích hoạt trước khi engine xóa một Object, tức là một "destructor".

Và nhiều callback *có* trong Node không có method chuyên dụng, nhưng vẫn khá hữu ích.

- :ref:`Node::NOTIFICATION_PARENTED <class_Node_constant_NOTIFICATION_PARENTED>`: callback được kích hoạt mỗi khi bạn thêm một node con vào node khác.

- :ref:`Node::NOTIFICATION_UNPARENTED <class_Node_constant_NOTIFICATION_UNPARENTED>`: callback được kích hoạt mỗi khi bạn xóa một node con khỏi node khác.

Method ``_notification()`` phổ quát cho phép truy cập tất cả notification tùy chỉnh này.

.. note::
  Các method trong tài liệu được đánh dấu là "virtual" cũng được thiết kế để script override.

  Một ví dụ kinh điển là
  :ref:`_init <class_Object_private_method__init>` method trong Object. Mặc dù nó không có equivalent ``NOTIFICATION_*``, engine vẫn gọi method này. Hầu hết ngôn ngữ (trừ C#) đều dựa vào nó như một constructor.

Vậy khi nào bạn nên sử dụng từng notification hoặc virtual function này?

_process so với _physics_process so với \*_input
------------------------------------------------

Sử dụng ``_process()`` khi bạn cần delta time phụ thuộc vào framerate giữa các frame. Nếu code cập nhật dữ liệu của object cần cập nhật thường xuyên nhất có thể, đây là nơi phù hợp. Các phép kiểm tra logic lặp lại và việc caching dữ liệu thường được thực hiện ở đây, nhưng điều đó phụ thuộc vào tần suất cần cập nhật các phép đánh giá. Nếu chúng không cần thực thi ở mọi frame, việc triển khai một vòng lặp Timer-timeout là một lựa chọn khác.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Cho phép thực hiện các thao tác lặp lại mà không kích hoạt logic của script
    # mỗi frame (hoặc thậm chí mỗi fixed frame).
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
        // mỗi frame (hoặc thậm chí mỗi fixed frame).
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
        // mỗi frame (hoặc thậm chí mỗi fixed frame).
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

Sử dụng ``_physics_process()`` khi bạn cần delta time độc lập với framerate giữa các frame. Nếu code cần được cập nhật nhất quán theo thời gian, bất kể thời gian trôi nhanh hay chậm, đây là nơi phù hợp. Các thao tác kinematic và transform lặp lại của object nên được thực hiện ở đây.

Mặc dù có thể thực hiện, để đạt hiệu năng tốt nhất, bạn nên tránh kiểm tra input trong các callback này. ``_process()`` và ``_physics_process()`` sẽ được kích hoạt ở mọi cơ hội (theo mặc định, chúng không "rest"). Ngược lại, các callback ``*_input()`` chỉ được kích hoạt trong những frame mà engine thực sự phát hiện input.

Bạn cũng có thể kiểm tra các input action trong những input callback. Nếu muốn sử dụng delta time, bạn có thể lấy nó từ các method delta time liên quan khi cần.

.. tabs::
  .. code-tab:: gdscript GDScript

    # Được gọi ở mọi frame, ngay cả khi engine không phát hiện input.
    func _process(delta):
        if Input.is_action_just_pressed("ui_select"):
            print(delta)

    # Được gọi trong mỗi input event.
    func _unhandled_input(event):
        match event.get_class():
            "InputEventKey":
                if Input.is_action_just_pressed("ui_accept"):
                    print(get_process_delta_time())

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {

        // Được gọi ở mọi frame, ngay cả khi engine không phát hiện input.
        public void _Process(double delta)
        {
            if (Input.IsActionJustPressed("ui_select"))
            {
                GD.Print(delta);
            }
        }

        // Được gọi trong mỗi input event. Điều này cũng đúng với _input().
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
        // Được gọi ở mọi frame, ngay cả khi engine không phát hiện input.
        virtual void _process(double p_delta) override {
            if (Input::get_singleton->is_action_just_pressed("ui_select")) {
                UtilityFunctions::print(p_delta);
            }
        }

        // Được gọi trong mỗi input event. Điều này cũng đúng với _input().
        virtual void _unhandled_input(const Ref<InputEvent> &p_event) override {
            Ref<InputEventKey> key_event = event;
            if (key_event.is_valid() && Input::get_singleton->is_action_just_pressed("ui_accept")) {
                UtilityFunctions::print(get_process_delta_time());
            }
        }
    };

_init so với initialization so với export
-----------------------------------------

Nếu script khởi tạo subtree node của riêng nó mà không có scene, code đó nên được thực thi trong ``_init()``. Các quá trình khởi tạo property khác hoặc không phụ thuộc vào SceneTree cũng nên chạy ở đây.

.. note::
  Equivalent trong C# của method ``_init()`` của GDScript là constructor.

``_init()`` được kích hoạt trước ``_enter_tree()`` hoặc ``_ready()``, nhưng sau khi script tạo và khởi tạo các property của nó. Khi instantiate một scene, các giá trị property sẽ được thiết lập theo trình tự sau:

1. **Gán giá trị ban đầu:** property được gán giá trị khởi tạo hoặc giá trị mặc định nếu không chỉ định giá trị nào. Nếu có setter, setter sẽ không được sử dụng.

2. ``_init()`` **gán giá trị:** giá trị của property được thay thế bằng mọi phép gán được thực hiện trong ``_init()``, qua đó kích hoạt setter.

3. **Gán giá trị export:** giá trị của property được export lại bị thay thế bằng mọi giá trị được thiết lập trong Inspector, qua đó kích hoạt setter.

.. tabs::
  .. code-tab:: gdscript GDScript

    # test được khởi tạo thành "one" mà không kích hoạt setter.
    @export var test: String = "one":
        set(value):
            test = value + "!"

    func _init():
        # Kích hoạt setter, đổi giá trị của test từ "one" thành "two!".
        test = "two"

    # Nếu bạn đặt test thành "three" trong Inspector, thao tác đó sẽ kích hoạt
    # setter, đổi giá trị của test từ "two!" thành "three!".

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
            // Kích hoạt setter, đổi giá trị của _test từ "one" thành "two!".
            Test = "two";
        }

        // Nếu bạn đặt Test thành "three" trong Inspector, thao tác này sẽ kích hoạt
        // setter, đổi giá trị của _test từ "two!" thành "three!".
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
            // Kích hoạt setter, đổi giá trị của _test từ "one" thành "two!".
            set_test("two");
        }

        // Nếu bạn đặt test thành "three" trong Inspector, thao tác này sẽ kích hoạt
        // setter, đổi giá trị của test từ "two!" thành "three!".
    };

Do đó, việc khởi tạo script thay vì scene có thể ảnh hưởng đến cả việc khởi tạo *và* số lần engine gọi setter.

_ready so với _enter_tree so với NOTIFICATION_PARENTED
------------------------------------------------------

Khi khởi tạo một scene được kết nối với scene được thực thi đầu tiên, Godot sẽ khởi tạo các node theo hướng đi xuống trong cây (thực hiện các lệnh gọi ``_init()``) và xây dựng cây từ root đi xuống. Điều này khiến các lệnh gọi ``_enter_tree()`` lan truyền xuống cây. Khi cây hoàn tất, các node lá gọi ``_ready``. Một node sẽ gọi method này sau khi tất cả node con đã hoàn tất việc gọi method tương ứng. Sau đó, quá trình này gây ra một làn sóng ngược đi lên về phía root của cây.

Khi khởi tạo một script hoặc một scene độc lập, các node không được thêm vào SceneTree ngay lúc tạo, nên không có callback ``_enter_tree()`` nào được kích hoạt. Thay vào đó, chỉ có lệnh gọi ``_init()`` xảy ra. Khi scene được thêm vào SceneTree, các lệnh gọi ``_enter_tree()`` và ``_ready()`` sẽ xảy ra.

Nếu bạn cần kích hoạt hành vi xảy ra khi các node trở thành node cha của node khác, bất kể việc đó diễn ra trong scene chính/đang hoạt động hay không, bạn có thể sử dụng notification :ref:`PARENTED <class_Node_constant_NOTIFICATION_PARENTED>`. Ví dụ: đoạn mã sau kết nối method của một node với custom signal trên node cha mà không gây lỗi. Hữu ích cho các node tập trung vào dữ liệu có khả năng được tạo tại runtime.

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
