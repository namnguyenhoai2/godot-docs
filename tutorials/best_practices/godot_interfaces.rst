.. _doc_godot_interfaces:

Các interface của Godot
=======================

Thông thường, script cần dựa vào các object khác để có được một số tính năng. Quy trình này gồm 2 phần:

1. Lấy một reference đến object được cho là có các tính năng đó.

2. Truy cập dữ liệu hoặc logic từ object.

Phần còn lại của tutorial này trình bày các cách khác nhau để thực hiện tất cả những việc đó.

Lấy reference đến object
------------------------

Đối với tất cả :ref:`Object <class_Object>`\s, cách cơ bản nhất để reference chúng là lấy reference đến một object hiện có từ một instance đã lấy được khác.

.. tabs::
  .. code-tab:: gdscript GDScript

    var obj = node.object # Truy cập property.
    var obj = node.get_object() # Truy cập method.

  .. code-tab:: csharp

    GodotObject obj = node.Object; // Truy cập property.
    GodotObject obj = node.GetObject(); // Truy cập method.

Nguyên tắc tương tự cũng áp dụng cho các object :ref:`RefCounted <class_RefCounted>`. Mặc dù người dùng thường truy cập :ref:`Node <class_Node>` và
:ref:`Resource <class_Resource>` theo cách này, vẫn có những phương án thay thế.

Thay vì truy cập property hoặc method, ta có thể lấy Resources bằng cách truy cập load.

.. tabs::
  .. code-tab:: gdscript GDScript

    # Nếu cần một "export const var" (không tồn tại), hãy sử dụng setter có điều kiện
    # cho một tool script để kiểm tra xem nó có đang chạy trong editor hay không.
    # Annotation `@tool` phải được đặt ở đầu script.
    @tool

    # Load resource trong quá trình load scene.
    var preres = preload(path)
    # Load resource khi chương trình đi đến câu lệnh.
    var res = load(path)

    # Theo quy ước, người dùng load scene và script bằng tên PascalCase
    # (như typename), thường vào các hằng số.
    const MyScene = preload("my_scene.tscn") # Static load
    const MyScript = preload("my_script.gd")

    # Giá trị của type này thay đổi, tức là đây là một biến, nên sử dụng snake_case.
    @export var script_type: Script

    # Phải cấu hình trong editor, mặc định là null.
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
        // Các khởi tạo property được load trong quá trình tạo instance của Script, tức là .new().
        // C# không có cơ chế "preload" trong quá trình load scene.

        // Khởi tạo bằng một giá trị. Có thể chỉnh sửa trong runtime.
        public Script MyScript = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Khởi tạo bằng cùng một giá trị. Không thể thay đổi giá trị.
        public readonly Script MyConstScript = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Giống 'readonly' vì setter không thể truy cập.
        // Tuy nhiên, có thể thiết lập giá trị trong constructor, tức là MyType().
        public Script MyNoSetScript { get; } = GD.Load<Script>("res://Path/To/MyScript.cs");

        // Nếu cần một "const [Export]" (không tồn tại), hãy sử dụng
        // setter có điều kiện cho một tool script để kiểm tra xem nó có đang chạy
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

1. Có nhiều cách để một ngôn ngữ load các resource như vậy.

2. Khi thiết kế cách các object truy cập dữ liệu, đừng quên rằng ta cũng có thể truyền các resource dưới dạng reference.

3. Hãy nhớ rằng việc load một resource sẽ lấy instance resource đã được cache mà engine duy trì. Để có một object mới, ta phải
   :ref:`duplicate <class_Resource_method_duplicate>` một reference hiện có hoặc tạo instance mới hoàn toàn bằng ``new()``.

Node cũng có một điểm truy cập thay thế: SceneTree.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node

    # Chậm.
    func dynamic_lookup_with_dynamic_nodepath():
        print(get_node("Child"))

    # Nhanh hơn. Chỉ dành cho GDScript.
    func dynamic_lookup_with_cached_nodepath():
        print($Child)

    # Nhanh nhất. Không bị ảnh hưởng nếu node được di chuyển sau này.
    # Lưu ý rằng annotation `@onready` chỉ dành cho GDScript.
    # Các ngôn ngữ khác phải thực hiện...
    #     var child
    #     func _ready():
    #         child = get_node("Child")
    @onready var child = $Child
    func lookup_and_cache_for_future_access():
        print(child)

    # Nhanh nhất. Không bị ảnh hưởng nếu node được di chuyển trong dock Scene tree.
    # Node phải được chọn trong inspector vì đây là một exported property.
    @export var child: Node
    func lookup_and_cache_for_future_access():
        print(child)

    # Ủy quyền việc gán reference cho một nguồn bên ngoài.
    # Nhược điểm: cần thực hiện kiểm tra validation.
    # Ưu điểm: node không yêu cầu cấu trúc bên ngoài của nó.
    #      'prop' có thể đến từ bất kỳ đâu.
    var prop
    func call_me_after_prop_is_initialized_by_parent():
        # Xác thực prop theo một trong ba cách.

        # Thất bại mà không thông báo.
        if not prop:
            return

        # Thất bại với thông báo lỗi.
        if not prop:
            printerr("'prop' wasn't initialized")
            return

        # Thất bại và chấm dứt.
        # LƯU Ý: Các script chạy từ release export template không chạy `assert`s.
        assert(prop, "'prop' wasn't initialized")

    # Sử dụng autoload.
    # Nguy hiểm đối với các node thông thường, nhưng hữu ích cho các node singleton thực sự
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

        // Nhanh nhất. Tìm node và lưu vào cache để truy cập sau.
        // Không bị hỏng nếu node di chuyển về sau.
        private Node _child;
        public void _Ready()
        {
            _child = GetNode("Child");
        }
        public void LookupAndCacheForFutureAccess()
        {
            GD.Print(_child);
        }

        // Ủy quyền việc gán tham chiếu cho một nguồn bên ngoài.
        // Nhược điểm: cần thực hiện kiểm tra xác thực.
        // Ưu điểm: node không yêu cầu cấu trúc bên ngoài của nó.
        //      'prop' có thể đến từ bất kỳ đâu.
        public object Prop { get; set; }
        public void CallMeAfterPropIsInitializedByParent()
        {
            // Xác thực prop theo một trong ba cách.

            // Thất bại mà không thông báo.
            if (prop == null)
            {
                return;
            }

            // Thất bại với thông báo lỗi.
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

            // Thất bại và chấm dứt.
            // Lưu ý: Các script chạy từ release export template không chạy `Debug.Assert`s.
            Debug.Assert(Prop, "'Prop' wasn't initialized");
        }

        // Sử dụng autoload.
        // Nguy hiểm đối với các node thông thường, nhưng hữu ích cho các node singleton thực sự
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

API scripting của Godot sử dụng kiểu duck typing. Điều này có nghĩa là nếu một script thực thi một thao tác, Godot không xác thực rằng nó hỗ trợ thao tác đó bằng **type**. Thay vào đó, nó kiểm tra object có **implements** method riêng lẻ hay không.

Ví dụ, class :ref:`CanvasItem <class_CanvasItem>` có property ``visible``. Trên thực tế, tất cả property được expose cho API scripting đều là một cặp setter và getter được liên kết với một tên. Nếu thử truy cập
:ref:`CanvasItem.visible <class_CanvasItem_property_visible>`, Godot sẽ thực hiện các kiểm tra sau theo thứ tự:

- Nếu object có một script được gắn vào, nó sẽ cố gắng set property thông qua script. Điều này tạo cơ hội để các script ghi đè một property được định nghĩa trên object cơ sở bằng cách ghi đè setter method của property đó.

- Nếu script không có property này, nó sẽ thực hiện tra cứu HashMap trong ClassDB để tìm property "visible" trên class CanvasItem và tất cả các type mà nó kế thừa. Nếu tìm thấy, nó sẽ gọi bound setter hoặc getter. Để biết thêm thông tin về HashMap, hãy xem
  tài liệu về :ref:`data preferences <doc_data_preferences>`.

- Nếu không tìm thấy, nó sẽ kiểm tra rõ ràng xem người dùng có muốn truy cập các property "script" hoặc "meta" hay không.

- Nếu không, nó sẽ kiểm tra việc triển khai ``_set``/``_get`` (tùy thuộc vào kiểu truy cập) trong CanvasItem và các type mà nó kế thừa. Các method này có thể thực thi logic tạo ấn tượng rằng Object có một property. Điều này cũng đúng với method ``_get_property_list``.

  - Lưu ý rằng điều này xảy ra ngay cả với các tên symbol không hợp lệ, chẳng hạn như tên bắt đầu bằng chữ số hoặc chứa dấu gạch chéo.

Do đó, hệ thống duck typing này có thể định vị một property trong script, class của object hoặc bất kỳ class nào mà object kế thừa, nhưng chỉ đối với những thứ mở rộng Object.

Godot cung cấp nhiều tùy chọn để thực hiện các kiểm tra runtime trên những lượt truy cập này:

- Truy cập property theo kiểu duck typing. Đây sẽ là các kiểm tra property (như mô tả ở trên). Nếu object không hỗ trợ thao tác, quá trình thực thi sẽ dừng.

  .. tabs::
    .. code-tab:: gdscript GDScript

      # Tất cả Object đều có các method wrapper get, set và call theo kiểu duck typing.
      get_parent().set("visible", false)

      # Việc sử dụng symbol accessor thay vì một string trong lời gọi method
      # sẽ ngầm gọi method `set`, đến lượt nó sẽ gọi
      # setter method liên kết với property thông qua chuỗi tra cứu property
      # .
      get_parent().visible = false

      # Lưu ý rằng nếu định nghĩa _set và _get mô tả sự tồn tại của một property,
      # nhưng property đó không được nhận diện trong bất kỳ method _get_property_list nào
      # thì các method set() và get() sẽ hoạt động, nhưng việc truy cập symbol
      # sẽ báo rằng không thể tìm thấy property.

    .. code-tab:: csharp

      // Tất cả Object đều có các method wrapper Get, Set và Call theo kiểu duck typing.
      GetParent().Set("visible", false);

      // C# là một ngôn ngữ static, vì vậy nó không có quyền truy cập symbol động, ví dụ như
      // `GetParent().Visible = false` sẽ không hoạt động.

- Kiểm tra method. Trong trường hợp
  :ref:`CanvasItem.visible <class_CanvasItem_property_visible>`, có thể truy cập các method, ``set_visible`` và ``is_visible`` như với bất kỳ method nào khác.

  .. tabs::
    .. code-tab:: gdscript GDScript

      var child = get_child(0)

      # Tra cứu động.
      child.call("set_visible", false)

      # Tra cứu động dựa trên symbol.
      # GDScript bí danh hóa thành method 'call' ở phía sau.
      child.set_visible(false)

      # Tra cứu động, trước tiên kiểm tra method có tồn tại hay không.
      if child.has_method("set_visible"):
          child.set_visible(false)

      # Kiểm tra cast, sau đó tra cứu động.
      # Hữu ích khi thực hiện nhiều lời gọi "an toàn" và biết rằng class
      # triển khai tất cả chúng. Không cần kiểm tra lặp lại.
      # Phức tạp nếu thực hiện kiểm tra cast cho một kiểu do người dùng định nghĩa vì nó
      # buộc phải có thêm dependency.
      if child is CanvasItem:
          child.set_visible(false)
          child.show_on_top = true

      # Nếu không muốn các kiểm tra này thất bại mà không thông báo cho người dùng,
      # có thể dùng assert thay thế. Các lệnh này sẽ ngay lập tức kích hoạt lỗi runtime
      # nếu điều kiện không đúng.
      assert(child.has_method("set_visible"))
      assert(child.is_in_group("offer"))
      assert(child is CanvasItem)

      # Cũng có thể dùng nhãn object để ngầm thể hiện một interface, tức là giả định object đó
      # triển khai một số method nhất định.
      # Có hai loại, cả hai chỉ tồn tại với Nodes: Names và
      # Groups.

      # Giả sử...
      # Một object "Quest" tồn tại và 1) có thể "complete" hoặc "fail", đồng thời
      # có sẵn text trước và sau mỗi trạng thái...

      # 1. Dùng một name.
      var quest = $Quest
      print(quest.text)
      quest.complete() # hoặc quest.fail()
      print(quest.text) # nội dung text mới được ngầm hiểu

      # 2. Dùng một group.
      for a_child in get_children():
          if a_child.is_in_group("quest"):
              print(quest.text)
              quest.complete() # hoặc quest.fail()
              print(quest.text) # nội dung text mới được ngầm hiểu

      # Lưu ý rằng các interface này là những quy ước dành riêng cho project mà team
      # định nghĩa (điều đó có nghĩa là cần tài liệu! Nhưng có lẽ cũng đáng làm?).
      # Bất kỳ script nào tuân theo "interface" được tài liệu hóa của name hoặc
      # group đều có thể thay thế nó.

    .. code-tab:: csharp

      Node child = GetChild(0);

      // Tra cứu động.
      child.Call("SetVisible", false);

      // Tra cứu động, trước tiên kiểm tra method có tồn tại hay không.
      if (child.HasMethod("SetVisible"))
      {
          child.Call("SetVisible", false);
      }

      // Dùng một group như thể đó là một "interface", tức là giả định group đó triển khai
      // một số method nhất định.
      // Cần có tài liệu tốt cho project để duy trì độ tin cậy
      // (trừ khi tạo các editor tool để áp đặt điều này trong editor).
      // Lưu ý, cách này nhìn chung không tốt bằng việc sử dụng một interface thực sự trong
      // C#, nhưng không thể thiết lập interface C# từ editor vì chúng là
      // tính năng ở cấp ngôn ngữ.
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

          // hữu ích khi cần thực hiện nhiều lời gọi an toàn đến class
          ci.ShowOnTop = true;
      }

      // Nếu không muốn các kiểm tra này thất bại mà không thông báo cho người dùng,
      // có thể dùng assert thay thế. Các lệnh này sẽ ngay lập tức kích hoạt lỗi runtime
      // nếu điều kiện không đúng.
      Debug.Assert(child.HasMethod("set_visible"));
      Debug.Assert(child.IsInGroup("offer"));
      Debug.Assert(CanvasItem.InstanceHas(child));

      // Cũng có thể dùng nhãn object để ngầm thể hiện một interface, tức là giả định object đó
      // triển khai một số method nhất định.
      // Có hai loại, cả hai chỉ tồn tại với Nodes: Names và
      // Groups.

      // Giả sử...
      // Một object "Quest" tồn tại và 1) có thể "Complete" hoặc "Fail", đồng thời
      // rằng nó sẽ có Text khả dụng trước và sau mỗi trạng thái...

      // 1. Sử dụng một tên.
      Node quest = GetNode("Quest");
      GD.Print(quest.Get("Text"));
      quest.Call("Complete"); // hoặc "Fail".
      GD.Print(quest.Get("Text")); // Nội dung văn bản mới được ngầm hiểu.

      // 2. Sử dụng một group.
      foreach (Node AChild in GetChildren())
      {
          if (AChild.IsInGroup("quest"))
          {
            GD.Print(quest.Get("Text"));
            quest.Call("Complete"); // hoặc "Fail".
            GD.Print(quest.Get("Text")); // Nội dung văn bản mới được ngầm hiểu.
          }
      }

      // Lưu ý rằng các interface này là những quy ước riêng của project do nhóm
      // định nghĩa (điều đó có nghĩa là phải có tài liệu! Nhưng có lẽ cũng đáng làm?).
      // Bất kỳ script nào tuân theo "interface" được ghi lại trong tài liệu của
      // name hoặc group đều có thể thay thế nó. Cũng lưu ý rằng trong C#, các method này
      // sẽ chậm hơn các lần truy cập static bằng interface truyền thống.

- Ủy thác việc truy cập cho một :ref:`Callable <class_Callable>`. Cách này có thể hữu ích trong những trường hợp cần mức độ tự do tối đa khỏi các dependency. Trong trường hợp này, ta dựa vào một context bên ngoài để thiết lập method.

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

Những chiến lược này góp phần tạo nên thiết kế linh hoạt của Godot. Kết hợp với nhau, chúng cung cấp cho người dùng nhiều công cụ để đáp ứng nhu cầu cụ thể của mình.
