.. _doc_scenes_versus_scripts:

Khi nào nên dùng scene thay vì script
=====================================

Chúng ta đã tìm hiểu sự khác biệt giữa scene và script. Script định nghĩa phần mở rộng của một engine class bằng mã mệnh lệnh, còn scene dùng mã khai báo.

Do đó, khả năng của mỗi hệ thống cũng khác nhau. Scene có thể định nghĩa cách một class mở rộng được khởi tạo, nhưng không định nghĩa hành vi thực sự của nó. Scene thường được dùng kết hợp với script: scene khai báo một cấu trúc gồm các node, còn script bổ sung hành vi bằng mã mệnh lệnh.

Kiểu vô danh
------------

Hoàn toàn *có thể* định nghĩa nội dung của một scene chỉ bằng script. Về bản chất, đây là điều Godot Editor thực hiện, chỉ khác là trong constructor C++ của các object của nó.

Tuy nhiên, việc chọn loại nào để sử dụng có thể là một vấn đề khó. Việc tạo các instance của script giống hệt việc tạo các class trong engine, trong khi xử lý scene yêu cầu thay đổi API:

.. tabs::
  .. code-tab:: gdscript GDScript

    const MyNode = preload("my_node.gd")
    const MyScene = preload("my_scene.tscn")
    var node = Node.new()
    var my_node = MyNode.new() # Lời gọi method giống nhau.
    var my_scene = MyScene.instantiate() # Lời gọi method khác nhau.
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

Ngoài ra, script sẽ hoạt động chậm hơn một chút so với scene do sự khác biệt về tốc độ giữa mã engine và mã script. Node càng lớn và phức tạp thì càng có nhiều lý do để xây dựng nó dưới dạng scene.

Kiểu có tên
-----------

Script có thể được đăng ký thành một kiểu mới ngay trong editor. Kiểu này sẽ xuất hiện dưới dạng một kiểu mới trong hộp thoại tạo node hoặc resource, cùng với một icon tùy chọn. Nhờ vậy, người dùng có thể sử dụng script thuận tiện hơn nhiều. Thay vì phải...

1. Biết kiểu cơ sở của script mà họ muốn sử dụng.

2. Tạo một instance của kiểu cơ sở đó.

3. Thêm script vào node.

Khi script đã được đăng ký, kiểu có script sẽ trở thành một tùy chọn tạo giống như các node và resource khác trong hệ thống. Hộp thoại tạo thậm chí còn có thanh tìm kiếm để tra cứu kiểu theo tên.

Có hai hệ thống để đăng ký kiểu:

- :ref:`Custom Types <doc_making_plugins>`

   - Chỉ dành cho editor. Tên kiểu không thể truy cập lúc runtime.

   - Không hỗ trợ các kiểu tùy chỉnh kế thừa.

   - Một công cụ khởi tạo. Tạo node cùng với script. Không làm gì thêm.

   - Editor không nhận biết kiểu của script hoặc mối quan hệ của nó với các kiểu engine hay script khác.

   - Cho phép người dùng xác định một icon.

   - Hoạt động với mọi ngôn ngữ scripting vì xử lý các Script resource ở dạng trừu tượng.

   - Thiết lập bằng :ref:`EditorPlugin.add_custom_type <class_EditorPlugin_method_add_custom_type>`.

- :ref:`Script Classes <doc_gdscript_basics_class_name>`

   - Có thể truy cập từ editor và runtime.

   - Hiển thị đầy đủ các mối quan hệ kế thừa.

   - Tạo node cùng với script, nhưng cũng có thể thay đổi kiểu hoặc mở rộng kiểu từ editor.

   - Editor nhận biết các mối quan hệ kế thừa giữa script, script class và các class C++ của engine.

   - Cho phép người dùng xác định một icon.

   - Nhà phát triển engine phải tự thêm hỗ trợ cho các ngôn ngữ (cả việc hiển thị tên và khả năng truy cập lúc runtime).

   - Editor quét các thư mục project và đăng ký mọi tên được công khai cho tất cả ngôn ngữ scripting. Mỗi ngôn ngữ scripting phải tự triển khai khả năng hiển thị thông tin này.

Cả hai phương pháp đều thêm tên vào hộp thoại tạo, nhưng đặc biệt là script class còn cho phép người dùng truy cập tên kiểu mà không cần tải script resource. Có thể tạo instance và truy cập constant hoặc static method từ bất kỳ đâu.

Với những tính năng như vậy, người ta có thể muốn kiểu của mình là một script không kèm scene vì sự tiện dụng mà nó mang lại cho người dùng. Những người phát triển plugin hoặc tạo các công cụ nội bộ cho designer sử dụng sẽ thấy cách này dễ dàng hơn.

Mặt hạn chế là bạn cũng phải sử dụng phần lớn phương pháp lập trình mệnh lệnh.

Hiệu năng của Script so với PackedScene
---------------------------------------

Một khía cạnh cuối cùng cần cân nhắc khi lựa chọn scene và script là tốc độ thực thi.

Khi kích thước object tăng, lượng mã cần thiết trong script để tạo và khởi tạo chúng cũng tăng lên đáng kể. Việc tạo các hệ thống phân cấp node minh họa rõ điều này. Logic của mỗi Node có thể dài đến vài trăm dòng mã.

Ví dụ mã dưới đây tạo một ``Node``, thay đổi tên của nó, gán một script cho nó, đặt parent tương lai của nó làm owner để nó được lưu vào đĩa cùng với parent, rồi cuối cùng thêm nó làm node con của node ``Main``:

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
            // SetScript() khiến đối tượng wrapper C# bị giải phóng, vì vậy hãy lấy một
            // wrapper mới cho node Child bằng instance ID của nó trước khi tiếp tục.
            Child = (Node)GodotObject.InstanceFromId(childID);
            AddChild(Child);
            Child.Owner = this;
        }
    }

Mã script như thế này chậm hơn nhiều so với mã C++ phía engine. Mỗi instruction tạo một lời gọi đến scripting API, dẫn đến nhiều "tra cứu" ở back-end để tìm logic cần thực thi.

Scene giúp tránh vấn đề hiệu năng này. :ref:`PackedScene <class_PackedScene>`, kiểu cơ sở mà scene kế thừa, định nghĩa các resource sử dụng dữ liệu đã được tuần tự hóa để tạo object. Engine có thể xử lý scene theo lô ở back-end và mang lại hiệu năng tốt hơn nhiều so với script.

Kết luận
--------

Tóm lại, cách tiếp cận tốt nhất là cân nhắc những điều sau:

- Nếu muốn tạo một công cụ cơ bản để tái sử dụng trong nhiều project khác nhau và có khả năng được mọi người ở mọi trình độ sử dụng (bao gồm cả những người không tự nhận mình là "programmer"), thì nhiều khả năng công cụ đó nên là một script, có thể là script với tên/icon tùy chỉnh.

- Nếu muốn tạo một khái niệm đặc thù cho game của mình, thì luôn nên dùng scene. Scene dễ theo dõi/chỉnh sửa hơn và an toàn hơn script.

- Nếu muốn đặt tên cho một scene, bạn vẫn có thể thực hiện việc này bằng cách khai báo một script class và gán một scene cho nó dưới dạng constant. Về bản chất, script sẽ trở thành một namespace:

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
