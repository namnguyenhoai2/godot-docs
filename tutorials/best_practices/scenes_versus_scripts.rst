.. _doc_scenes_versus_scripts:

Khi nào nên dùng scene thay vì script
=====================================

Chúng ta đã tìm hiểu sự khác biệt giữa scene và script. Script định nghĩa một phần mở rộng của engine class bằng mã imperative, còn scene bằng mã declarative.

Do đó, khả năng của mỗi hệ thống cũng khác nhau. Scene có thể định nghĩa cách một extended class khởi tạo, nhưng không định nghĩa được hành vi thực sự của nó. Scene thường được dùng kết hợp với script: scene khai báo một composition gồm các node, còn script bổ sung hành vi bằng mã imperative.

Kiểu anonymous
--------------

Hoàn toàn có thể định nghĩa nội dung của scene chỉ bằng một script. Về bản chất, đây chính là những gì Godot Editor thực hiện, chỉ khác là trong C++ constructor của các object.

Tuy nhiên, việc chọn dùng loại nào có thể là một vấn đề nan giải. Việc tạo các instance của script giống hệt việc tạo các class trong engine, trong khi xử lý scene đòi hỏi thay đổi API:

.. tabs::
  .. code-tab:: gdscript GDScript

    const MyNode = preload("my_node.gd")
    const MyScene = preload("my_scene.tscn")
    var node = Node.new()
    var my_node = MyNode.new() # Cùng một lời gọi phương thức.
    var my_scene = MyScene.instantiate() # Lời gọi phương thức khác nhau.
    var my_inherited_scene = MyScene.instantiate(PackedScene.GEN_EDIT_STATE_MAIN) # Tạo scene kế thừa từ MyScene.

  .. code-tab:: csharp

    using Godot;

    public partial class Game : Node
    {
        public static CSharpScript MyNode { get; } =
            GD.Load<CSharpScript>("res://Path/To/MyNode.cs");
        public static PackedScene MyScene { get; } =
            GD.Load<PackedScene>("res://Path/To/MyScene.tscn");
        private Node _node;
        private Node _myNode;
        private Node _myScene;
        private Node _myInheritedScene;

        public Game()
        {
            _node = new Node();
            _myNode = MyNode.New().As<Node>();
            // Khác với việc gọi new() hoặc MyNode.New(). Được khởi tạo từ một PackedScene.
            _myScene = MyScene.Instantiate();
            // Tạo scene kế thừa từ MyScene.
            _myInheritedScene = MyScene.Instantiate(PackedScene.GenEditState.Main);
        }
    }

Ngoài ra, script sẽ chạy chậm hơn một chút so với scene do khác biệt về tốc độ giữa mã engine và mã script. Node càng lớn và phức tạp thì càng có nhiều lý do để xây dựng nó dưới dạng scene.

Kiểu có tên
-----------

Script có thể được đăng ký thành một kiểu mới ngay trong editor. Điều này hiển thị nó như một kiểu mới trong hộp thoại tạo node hoặc resource, cùng với một icon tùy chọn. Nhờ đó, người dùng có thể sử dụng script dễ dàng và thuận tiện hơn nhiều. Thay vì phải...

1. Biết kiểu cơ sở của script mà họ muốn sử dụng.

2. Tạo một instance của kiểu cơ sở đó.

3. Thêm script vào node.

Với một script đã đăng ký, kiểu được viết bằng script sẽ trở thành một tùy chọn tạo giống như các node và resource khác trong hệ thống. Hộp thoại tạo thậm chí còn có thanh tìm kiếm để tra cứu kiểu theo tên.

Có hai hệ thống để đăng ký kiểu:

- :ref:`Custom Types <doc_making_plugins>`

   - Chỉ dành cho editor. Tên kiểu không thể truy cập tại runtime.

   - Không hỗ trợ các custom type kế thừa.

   - Một công cụ khởi tạo. Tạo node cùng với script. Không làm gì thêm.

   - Editor không nhận biết kiểu của script hoặc mối quan hệ của nó với các kiểu engine hay script khác.

   - Cho phép người dùng định nghĩa icon.

   - Hoạt động với mọi ngôn ngữ scripting vì xử lý các Script resource ở mức trừu tượng.

   - Thiết lập bằng :ref:`EditorPlugin.add_custom_type <class_EditorPlugin_method_add_custom_type>`.

- :ref:`Script Classes <doc_gdscript_basics_class_name>`

   - Có thể truy cập từ editor và runtime.

   - Hiển thị đầy đủ các mối quan hệ kế thừa.

   - Tạo node cùng với script, nhưng cũng có thể thay đổi kiểu hoặc mở rộng kiểu từ editor.

   - Editor nhận biết các mối quan hệ kế thừa giữa script, script class và engine C++ class.

   - Cho phép người dùng định nghĩa icon.

   - Các nhà phát triển engine phải tự thêm hỗ trợ cho từng ngôn ngữ (cả việc hiển thị tên lẫn khả năng truy cập tại runtime).

   - Editor quét các thư mục project và đăng ký mọi tên được exposed cho tất cả ngôn ngữ scripting. Mỗi ngôn ngữ scripting phải tự triển khai phần hỗ trợ riêng để expose thông tin này.

Cả hai phương pháp đều thêm tên vào hộp thoại tạo, nhưng đặc biệt, script class còn cho phép người dùng truy cập tên kiểu mà không cần load script resource. Việc tạo instance và truy cập các hằng số hoặc static method có thể thực hiện từ bất kỳ đâu.

Với những tính năng như vậy, người ta có thể muốn kiểu của mình là một script không có scene vì sự dễ sử dụng mà nó mang lại cho người dùng. Những người phát triển plugin hoặc tạo các công cụ nội bộ để designer sử dụng sẽ thấy mọi việc dễ dàng hơn theo cách này.

Mặt hạn chế là điều này cũng đồng nghĩa với việc phải sử dụng phương pháp lập trình imperative ở mức độ lớn.

Hiệu năng của Script so với PackedScene
---------------------------------------

Một khía cạnh cuối cùng cần cân nhắc khi lựa chọn scene và script là tốc độ thực thi.

Khi kích thước của object tăng lên, kích thước script cần thiết để tạo và khởi tạo chúng cũng tăng lớn hơn nhiều. Việc tạo các node hierarchy minh họa rõ điều này. Logic của mỗi Node có thể dài đến vài trăm dòng mã.

Ví dụ mã dưới đây tạo một ``Node`` mới, đổi tên nó, gán một script cho nó, đặt parent trong tương lai của nó làm owner để nó được lưu vào đĩa cùng với owner, rồi cuối cùng thêm nó làm child của node ``Main``:

.. tabs::
  .. code-tab:: gdscript GDScript

    # main.gd
    extends Node

    func _init():
        var child = Node.new()
        child.name = "Child"
        child.script = preload("child.gd")
        add_child(child)
        child.owner = self

  .. code-tab:: csharp

    using Godot;

    public partial class Main : Node
    {
        public Node Child { get; set; }

        public Main()
        {
            Child = new Node();
            Child.Name = "Child";
            var childID = Child.GetInstanceId();
            Child.SetScript(GD.Load<Script>("res://Path/To/Child.cs"));
            // SetScript() khiến wrapper object C# bị dispose, vì vậy hãy lấy một
            // wrapper mới cho node Child bằng instance ID của nó trước khi tiếp tục.
            Child = (Node)GodotObject.InstanceFromId(childID);
            AddChild(Child);
            Child.Owner = this;
        }
    }

Mã script như thế này chậm hơn nhiều so với mã C++ phía engine. Mỗi instruction tạo một lời gọi đến scripting API, dẫn đến nhiều lần "lookup" ở back-end để tìm logic cần thực thi.

Scene giúp tránh vấn đề hiệu năng này. :ref:`PackedScene <class_PackedScene>`, kiểu cơ sở mà scene kế thừa, định nghĩa các resource sử dụng dữ liệu đã serialize để tạo object. Engine có thể xử lý scene theo batch ở back-end và mang lại hiệu năng tốt hơn nhiều so với script.

Kết luận
--------

Cuối cùng, cách tiếp cận tốt nhất là cân nhắc những điều sau:

- Nếu muốn tạo một công cụ cơ bản sẽ được tái sử dụng trong nhiều project khác nhau và có khả năng được mọi người ở mọi trình độ sử dụng (bao gồm cả những người không tự nhận mình là "lập trình viên"), thì rất có thể công cụ đó nên là một script, nhiều khả năng là script có tên/icon tùy chỉnh.

- Nếu muốn tạo một concept đặc thù cho game của mình, thì nó luôn nên là một scene. Scene dễ theo dõi/chỉnh sửa hơn và cung cấp nhiều tính bảo mật hơn script.

- Nếu muốn đặt tên cho một scene, vẫn có thể làm điều gì đó tương tự bằng cách khai báo một script class và cung cấp cho nó một scene dưới dạng hằng số. Khi đó, script thực chất trở thành một namespace:

  .. tabs::
    .. code-tab:: gdscript GDScript

      # game.gd
      class_name Game # extends RefCounted, vì vậy nó sẽ không xuất hiện trong hộp thoại tạo node.
      extends RefCounted

      const MyScene = preload("my_scene.tscn")

      # main.gd
      extends Node
      func _ready():
          add_child(Game.MyScene.instantiate())

    .. code-tab:: csharp

      // Game.cs
      public partial class Game : RefCounted
      {
          public static PackedScene MyScene { get; } =
              GD.Load<PackedScene>("res://Path/To/MyScene.tscn");
      }

      // Main.cs
      public partial class Main : Node
      {
          public override void _Ready()
          {
              AddChild(Game.MyScene.Instantiate());
          }
      }
