.. _doc_godot_interfaces:

Các interface của Godot
=======================

Thông thường, ta cần các script phụ thuộc vào những object khác để cung cấp các tính năng. Quy trình này gồm 2 phần:

1. Lấy reference đến object được cho là có các tính năng đó.

2. Truy cập dữ liệu hoặc logic từ object.

Phần còn lại của tutorial này trình bày các cách khác nhau để thực hiện tất cả những việc trên.

Lấy reference đến object
------------------------

Đối với tất cả :ref:`Object <class_Object>`\s, cách cơ bản nhất để tham chiếu đến chúng là lấy reference đến một object hiện có từ một instance đã được lấy trước đó.

.. tabs::
  .. code-tab:: gdscript GDScript

    var obj = node.object # Truy cập property.
    var obj = node.get_object() # Truy cập method.

  .. code-tab:: csharp

    GodotObject obj = node.Object; // Truy cập property.
    GodotObject obj = node.GetObject(); // Truy cập method.

Nguyên tắc tương tự cũng áp dụng cho các object :ref:`RefCounted <class_RefCounted>`. Mặc dù người dùng thường truy cập :ref:`Node <class_Node>` và
:ref:`Resource <class_Resource>` this way, alternative measures are available.

Thay vì truy cập property hoặc method, ta có thể lấy Resources bằng cách load.

.. tabs::
  .. code-tab:: gdscript GDScript

    # Nếu cần một "export const var" (vốn không tồn tại), hãy sử dụng một conditional
    # setter cho tool script để kiểm tra xem nó có đang được thực thi trong editor hay không.
    # Annotation `@tool` phải được đặt ở đầu script.
    @tool

    # Load resource trong khi scene được load.
    var preres = preload(path)
    # Load resource khi chương trình chạy đến statement.
    var res = load(path)

    # Note that users load scenes and scripts, by convention, with PascalCase
    # tên (chẳng hạn như typename), thường vào các constant.
    const MyScene = preload("my_scene.tscn") # Static load
    const MyScript = preload("my_script.gd")

    # Giá trị của type này thay đổi, tức là nó là một variable, nên sử dụng snake_case.
    @export var script_type: Script

    # Phải được cấu hình từ editor, mặc định là null.
    @export var const_script: Script:
        set(value):
            if Engine.is_editor_hint():
                const_script = value

    # Cảnh báo người dùng nếu giá trị chưa được thiết lập.
    func _get_configuration_warnings():
        if not const_script:
            return ["Must initialize property 'const_script'."]

        return []

  .. code-tab:: csharp

    // Thêm tool script cho ví dụ "const [Export]".
    [Tool]
    public MyType
    {
        // Các property initialization được load trong quá trình khởi tạo Script, tức là .new().
        // Trong C# không có thao tác "preload" nào được thực hiện trong quá trình load scene.

        // Khởi tạo với một giá trị. Có thể chỉnh sửa trong runtime.
        public Script MyScript = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Khởi tạo với cùng một giá trị. Không thể thay đổi giá trị.
        public readonly Script MyConstScript = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Tương tự 'readonly' vì setter không thể truy cập.
        // Tuy nhiên, giá trị có thể được thiết lập trong constructor, tức là MyType().
        public Script MyNoSetScript { get; } = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Nếu cần một "const [Export]" (vốn không tồn tại), hãy sử dụng một
        // conditional setter cho tool script để kiểm tra xem nó có đang được thực thi
        // trong editor hay không.
        private PackedScene _enemyScn;

        [Export]
        public PackedScene EnemyScn
        {
            get { return _enemyScn; }
            set
            {
                if (Engine.IsEditorHint())
                {
                    _enemyScn = value;
                }
            }
        };

        // Cảnh báo người dùng nếu giá trị chưa được thiết lập.
        public string[] _GetConfigurationWarnings()
        {
            if (EnemyScn == null)
            {
                return ["Must initialize property 'EnemyScn'."];
            }
            return [];
        }
    }

Lưu ý những điều sau:

1. Có nhiều cách để một ngôn ngữ có thể load các resource như vậy.

2. Khi thiết kế cách các object truy cập dữ liệu, đừng quên rằng ta cũng có thể truyền các resource đi dưới dạng reference.

3. Hãy nhớ rằng việc load một resource sẽ lấy instance resource được cache và duy trì bởi engine. Để lấy một object mới, ta phải
   :ref:`duplicate <class_Resource_method_duplicate>` an existing reference
   hoặc khởi tạo một object từ đầu bằng ``new()``.

Các Node cũng có một điểm truy cập thay thế: SceneTree.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node

    # Chậm.
    func dynamic_lookup_with_dynamic_nodepath():
        print(get_node("Child"))

    # Nhanh hơn. Chỉ dành cho GDScript.
    func dynamic_lookup_with_cached_nodepath():
        print($Child)

    # Nhanh nhất. Không bị ảnh hưởng nếu node được di chuyển về sau.
    # Note that `@onready` annotation is GDScript-only.
    # Các ngôn ngữ khác phải làm như sau...
    # var child
    # func _ready():
    # child = get_node("Child")
    @onready var child = $Child
    func lookup_and_cache_for_future_access():
        print(child)

    # Nhanh nhất. Không bị ảnh hưởng nếu node được di chuyển trong Scene tree dock.
    # Node phải được chọn trong inspector vì đây là một exported property.
    @export var child: Node
    func lookup_and_cache_for_future_access():
        print(child)

    # Ủy quyền việc gán reference cho một nguồn bên ngoài.
    # Nhược điểm: cần thực hiện kiểm tra validation.
    # Ưu điểm: node không yêu cầu gì từ cấu trúc bên ngoài.
    # 'prop' có thể đến từ bất kỳ đâu.
    var prop
    func call_me_after_prop_is_initialized_by_parent():
        # Validate prop theo một trong ba cách.

        # Thất bại mà không có thông báo.
        if not prop:
            return

        # Thất bại với một thông báo lỗi.
        if not prop:
            printerr("'prop' wasn't initialized")
            return

        # Thất bại và kết thúc.
        # NOTE: Scripts run from a release export template don't run `assert`s.
        assert(prop, "'prop' wasn't initialized")

    # Sử dụng autoload.
    # Nguy hiểm đối với các node thông thường, nhưng hữu ích cho các singleton node thực sự
    # tự quản lý dữ liệu của chúng và không can thiệp vào các object khác.
    func reference_a_global_autoloaded_variable():
        print(globals)
        print(globals.prop)
        print(globals.my_getter())

  .. code-tab:: csharp

    using Godot;
    using System;
    using System.Diagnostics;

    public class MyNode : Node
    {
        // Chậm
        public void DynamicLookupWithDynamicNodePath()
        {
            GD.Print(GetNode("Child"));
        }

        // Nhanh nhất. Tìm node và cache nó để truy cập trong tương lai.
        // Không bị ảnh hưởng nếu node được di chuyển về sau.
        private Node _child;
        public void _Ready()
        {
            _child = GetNode("Child");
        }
        public void LookupAndCacheForFutureAccess()
        {
            GD.Print(_child);
        }

        // Ủy quyền việc gán reference cho một nguồn bên ngoài.
        // Nhược điểm: cần thực hiện kiểm tra validation.
        // Ưu điểm: node không yêu cầu gì từ cấu trúc bên ngoài.
        // 'prop' có thể đến từ bất kỳ đâu.
        public object Prop { get; set; }
        public void CallMeAfterPropIsInitializedByParent()
        {
            // Validate prop theo một trong ba cách.

            // Thất bại mà không có thông báo.
            if (prop == null)
            {
                return;
            }

            // Thất bại với một thông báo lỗi.
            if (prop == null)
            {
                GD.PrintErr("'Prop' wasn't initialized");
                return;
            }

            // Thất bại với một exception.
            if (prop == null)
            {
                throw new InvalidOperationException("'Prop' wasn't initialized.");
            }

            // Thất bại và kết thúc.
            // Note: Scripts run from a release export template don't run `Debug.Assert`s.
            Debug.Assert(Prop, "'Prop' wasn't initialized");
        }

        // Sử dụng autoload.
        // Nguy hiểm đối với các node thông thường, nhưng hữu ích cho các singleton node thực sự
        // tự quản lý dữ liệu của chúng và không can thiệp vào các object khác.
        public void ReferenceAGlobalAutoloadedVariable()
        {
            MyNode globals = GetNode<MyNode>("/root/Globals");
            GD.Print(globals);
            GD.Print(globals.Prop);
            GD.Print(globals.MyGetter());
        }
    };

.. _doc_accessing_data_or_logic_from_object:

Truy cập dữ liệu hoặc logic từ một object
-----------------------------------------

Scripting API của Godot sử dụng duck typing. Điều này có nghĩa là khi một script thực thi một operation, Godot không xác thực rằng object đó hỗ trợ operation bằng **type**. Thay vào đó, nó kiểm tra xem object có **implements** method riêng lẻ đó hay không.

Ví dụ, class :ref:`CanvasItem <class_CanvasItem>` có property ``visible``. Tất cả property được expose cho scripting API thực chất là một cặp setter và getter được liên kết với một name. Nếu thử truy cập
:ref:`CanvasItem.visible <class_CanvasItem_property_visible>`, then Godot would do the
các bước kiểm tra sau, theo thứ tự:

- Nếu object có một script được gắn vào, nó sẽ cố gắng thiết lập property thông qua script. Điều này cho phép script override một property được định nghĩa trên base object bằng cách override setter method của property đó.

- Nếu script không có property này, nó thực hiện tra cứu HashMap trong ClassDB để tìm property "visible" trên class CanvasItem và tất cả các type mà class này kế thừa. Nếu tìm thấy, nó sẽ gọi bound setter hoặc getter. Để biết thêm thông tin về HashMap, hãy xem
  :ref:`data preferences <doc_data_preferences>` docs.

- Nếu không tìm thấy, nó sẽ kiểm tra rõ ràng xem người dùng có muốn truy cập các property "script" hoặc "meta" hay không.

- If not, it checks for a ``_set``/``_get`` implementation (depending on type of access) in the CanvasItem and its inherited types. These methods can execute logic that gives the impression that the Object has a property. This is also the case with the ``_get_property_list`` method.

  - Lưu ý rằng điều này xảy ra ngay cả với các symbol name không hợp lệ, chẳng hạn như name bắt đầu bằng chữ số hoặc chứa dấu gạch chéo.

Do đó, hệ thống duck typing này có thể tìm property trong script, class của object hoặc bất kỳ class nào mà object kế thừa, nhưng chỉ áp dụng cho những đối tượng kế thừa Object.

Godot cung cấp nhiều tùy chọn để thực hiện các runtime check đối với những thao tác truy cập này:

- Truy cập property bằng duck typing. Đây sẽ là các property check (như mô tả ở trên). Nếu operation không được object hỗ trợ, quá trình thực thi sẽ dừng.

  .. tabs::
    .. code-tab:: gdscript GDScript

      # Tất cả Object đều có các wrapper method get, set và call sử dụng duck typing.
      get_parent().set("visible", false)

      # Việc sử dụng symbol accessor thay vì string trong method call
      # sẽ ngầm gọi method `set`, method này lần lượt gọi
      # setter method được liên kết với property thông qua chuỗi
      # tra cứu property.
      get_parent().visible = false

      # Note that if one defines a _set and _get that describe a property's
      # tồn tại, nhưng property không được nhận diện trong bất kỳ method _get_property_list
      # nào, thì các method set() và get() vẫn hoạt động, nhưng việc truy cập symbol
      # sẽ báo rằng không thể tìm thấy property.

    .. code-tab:: csharp

      // Tất cả Object đều có các wrapper method Get, Set và Call sử dụng duck typing.
      GetParent().Set("visible", false);

      // C# là một ngôn ngữ static, vì vậy nó không có dynamic symbol access, ví dụ
      // `GetParent().Visible = false` sẽ không hoạt động.

- Kiểm tra method. Trong trường hợp
  :ref:`CanvasItem.visible <class_CanvasItem_property_visible>`, one can
  truy cập các method, ``set_visible`` và ``is_visible`` như mọi method khác.

  .. tabs::
    .. code-tab:: gdscript GDScript

      var child = get_child(0)

      # Dynamic lookup.
      child.call("set_visible", false)

      # Dynamic lookup dựa trên symbol.
      # GDScript thực hiện việc này bằng cách alias thành method 'call' ở phía sau.
      child.set_visible(false)

      # Dynamic lookup, trước tiên kiểm tra method có tồn tại hay không.
      if child.has_method("set_visible"):
          child.set_visible(false)

      # Kiểm tra cast, sau đó là dynamic lookup.
      # Hữu ích khi bạn thực hiện nhiều lệnh gọi "an toàn" và biết rằng class triển khai tất cả chúng. Không cần kiểm tra lặp lại.
      # Hữu ích khi bạn thực hiện nhiều lệnh gọi "an toàn" và biết rằng class triển khai tất cả chúng. Không cần kiểm tra lặp lại.
      # Có thể phức tạp nếu thực hiện kiểm tra cast cho một type do người dùng định nghĩa vì điều đó tạo thêm dependency.
      # Có thể phức tạp nếu thực hiện kiểm tra cast cho một type do người dùng định nghĩa vì điều đó tạo thêm dependency.
      if child is CanvasItem:
          child.set_visible(false)
          child.show_on_top = true

      # Nếu không muốn các kiểm tra này thất bại mà không thông báo cho người dùng,
      # ta có thể sử dụng assert thay thế. Những assert này sẽ kích hoạt runtime error
      # ngay lập tức nếu điều kiện không đúng.
      assert(child.has_method("set_visible"))
      assert(child.is_in_group("offer"))
      assert(child is CanvasItem)

      # Cũng có thể sử dụng label của object để biểu thị một interface, tức là giả định object đó
      # triển khai một số method nhất định.
      # Có hai loại, cả hai đều chỉ tồn tại đối với Node: Name và
      # Group.

      # Giả sử...
      # Một object "Quest" tồn tại và 1) nó có thể "complete" hoặc "fail", đồng thời
      # có text khả dụng trước và sau mỗi state...

      # 1. Sử dụng một name.
      var quest = $Quest
      print(quest.text)
      quest.complete() # hoặc quest.fail()
      print(quest.text) # nội dung text mới được ngầm định

      # 2. Sử dụng một group.
      for a_child in get_children():
          if a_child.is_in_group("quest"):
              print(quest.text)
              quest.complete() # hoặc quest.fail()
              print(quest.text) # nội dung text mới được ngầm định

      # Note that these interfaces are project-specific conventions the team
      # defines (điều này có nghĩa là documentation! Nhưng có lẽ cũng đáng làm?).
      # Bất kỳ script nào tuân theo "interface" được document của name hoặc
      # group đều có thể thay thế cho nó.

    .. code-tab:: csharp

      Node child = GetChild(0);

      // Dynamic lookup.
      child.Call("SetVisible", false);

      // Dynamic lookup, trước tiên kiểm tra method có tồn tại hay không.
      if (child.HasMethod("SetVisible"))
      {
          child.Call("SetVisible", false);
      }

      // Sử dụng một group như thể đó là một "interface", tức là giả định rằng nó triển khai
      // một số phương thức nhất định.
      // Cần có tài liệu tốt để dự án duy trì được độ tin cậy
      // (trừ khi bạn tạo các công cụ editor để thực thi điều này ngay trong editor).
      // Note, this is generally not as good as using an actual interface in
      // C#, nhưng bạn không thể thiết lập các interface của C# từ editor vì chúng là
      // các tính năng ở cấp độ ngôn ngữ.
      if (child.IsInGroup("Offer"))
      {
          child.Call("Accept");
          child.Call("Reject");
      }

      // Kiểm tra cast, sau đó tra cứu tĩnh.
      CanvasItem ci = GetParent() as CanvasItem;
      if (ci != null)
      {
          ci.SetVisible(false);

          // hữu ích khi bạn cần thực hiện nhiều lần gọi an toàn đến class
          ci.ShowOnTop = true;
      }

      // Nếu không muốn các kiểm tra này thất bại mà không thông báo cho người dùng,
      // bạn có thể sử dụng assert thay thế. Các assert này sẽ ngay lập tức kích hoạt lỗi runtime
      // nếu điều kiện không đúng.
      Debug.Assert(child.HasMethod("set_visible"));
      Debug.Assert(child.IsInGroup("offer"));
      Debug.Assert(CanvasItem.InstanceHas(child));

      // Bạn cũng có thể sử dụng object label để ngụ ý một interface, tức là giả định rằng nó
      // triển khai một số phương thức nhất định.
      // Có hai loại, cả hai chỉ tồn tại đối với Node: Name và
      // Group.

      // Giả sử...
      // Một object "Quest" tồn tại và 1) nó có thể "Complete" hoặc "Fail", và
      // nó sẽ có Text khả dụng trước và sau mỗi trạng thái...

      // 1. Sử dụng một name.
      Node quest = GetNode("Quest");
      GD.Print(quest.Get("Text"));
      quest.Call("Complete"); // hoặc "Fail".
      GD.Print(quest.Get("Text")); // Nội dung text mới được ngầm định.

      // 2. Sử dụng một group.
      foreach (Node AChild in GetChildren())
      {
          if (AChild.IsInGroup("quest"))
          {
            GD.Print(quest.Get("Text"));
            quest.Call("Complete"); // hoặc "Fail".
            GD.Print(quest.Get("Text")); // Nội dung text mới được ngầm định.
          }
      }

      // Note that these interfaces are project-specific conventions the team
      // mà nó định nghĩa (điều này có nghĩa là phải có tài liệu! Nhưng có lẽ vẫn đáng làm?).
      // Bất kỳ script nào tuân theo "interface" đã được mô tả trong tài liệu của
      // name hoặc group đều có thể thay thế nó. Cũng lưu ý rằng trong C#, các phương thức này
      // sẽ chậm hơn so với các truy cập tĩnh bằng interface truyền thống.

- Ủy quyền việc truy cập cho :ref:`Callable <class_Callable>`. Cách này có thể hữu ích trong những trường hợp cần mức độ tự do tối đa khỏi các dependency. Trong trường hợp này, ta dựa vào một context bên ngoài để thiết lập phương thức.

.. tabs::
  .. code-tab:: gdscript GDScript

    # child.gd
    extends Node
    var fn = null

    func my_method():
        if fn:
            fn.call()

    # parent.gd
    extends Node

    @onready var child = $Child

    func _ready():
        child.fn = print_me
        child.my_method()

    func print_me():
        print(name)

  .. code-tab:: csharp

    // Child.cs
    using Godot;

    public partial class Child : Node
    {
        public Callable? Callable { get; set; }

        public void MyMethod()
        {
            Callable?.Call();
        }
    }

    // Parent.cs
    using Godot;

    public partial class Parent : Node
    {
        private Child _child;

        public void _Ready()
        {
            _child = GetNode<Child>("Child");
            _child.Callable = Callable.From(PrintMe);
            _child.MyMethod();
        }

        public void PrintMe()
        {
            GD.Print(Name);
        }
    }

Các chiến lược này góp phần tạo nên thiết kế linh hoạt của Godot. Kết hợp chúng, người dùng có một loạt công cụ để đáp ứng các nhu cầu cụ thể của mình.
