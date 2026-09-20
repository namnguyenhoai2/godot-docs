.. _doc_scene_organization:

Tổ chức scene
=============

Bài viết này trình bày các chủ đề liên quan đến việc tổ chức nội dung scene một cách hiệu quả. Bạn nên sử dụng những node nào? Nên đặt chúng ở đâu? Chúng nên tương tác với nhau như thế nào?

Cách xây dựng các mối quan hệ hiệu quả
--------------------------------------

Khi người dùng Godot bắt đầu tự xây dựng các scene của mình, họ thường gặp phải vấn đề sau:

Họ tạo scene đầu tiên và thêm nội dung vào đó, nhưng cuối cùng lại lưu các nhánh của scene thành những scene riêng biệt khi cảm giác dai dẳng rằng nên tách chúng ra ngày càng tăng lên. Tuy nhiên, sau đó họ nhận thấy các tham chiếu cứng mà trước đây có thể dựa vào không còn khả thi nữa. Việc tái sử dụng scene ở nhiều nơi gây ra vấn đề vì các node path không tìm thấy đối tượng đích, còn các kết nối signal được thiết lập trong editor thì bị hỏng.

Để khắc phục những vấn đề này, bạn phải instantiate các sub-scene mà không yêu cầu chúng biết chi tiết về môi trường. Bạn cần có thể tin rằng sub-scene sẽ tự tạo mà không quá phụ thuộc vào cách nó được sử dụng.

Một trong những điều quan trọng nhất cần cân nhắc trong `Object-Oriented Programming (OOP) <https://en.wikipedia.org/wiki/Object-oriented_programming>`_ là duy trì các class có phạm vi tập trung và mục đích đơn nhất, với `loose coupling <https://en.wikipedia.org/wiki/Loose_coupling>`_ tới những phần khác của codebase. Điều này giúp giữ kích thước của các object ở mức nhỏ (để dễ bảo trì) và cải thiện khả năng tái sử dụng của chúng.

Những best practice về OOP này có *nhiều* hệ quả đối với best practice trong cấu trúc scene và cách sử dụng script.

**Nếu có thể, bạn nên thiết kế scene không có dependency.** Nghĩa là, bạn nên tạo các scene tự chứa mọi thứ chúng cần bên trong.

Nếu một scene phải tương tác với context bên ngoài, các developer giàu kinh nghiệm khuyến nghị sử dụng `Dependency Injection <https://en.wikipedia.org/wiki/Dependency_injection>`_. Kỹ thuật này consiste ở việc một API cấp cao cung cấp các dependency cho API cấp thấp. Tại sao lại làm vậy? Vì các class phụ thuộc vào môi trường bên ngoài có thể vô tình gây ra bug và hành vi không mong muốn.

Để làm điều này, bạn phải expose dữ liệu rồi dựa vào một context cha để khởi tạo nó:

1. Kết nối với một signal. Cực kỳ an toàn, nhưng chỉ nên dùng để "phản hồi" hành vi, không phải để khởi động hành vi đó. Theo quy ước, tên signal thường là các động từ ở thì quá khứ như "entered", "skill_activated" hoặc "item_collected".

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Parent
       $Child.signal_name.connect(method_on_the_object)

       # Child
       signal_name.emit() # Kích hoạt hành vi do parent chỉ định.

     .. code-tab:: csharp

       // Parent
       GetNode("Child").Connect("SignalName", Callable.From(ObjectWithMethod.MethodOnTheObject));

       // Child
       EmitSignal("SignalName"); // Kích hoạt hành vi do parent chỉ định.

     .. code-tab:: cpp C++

       // Parent
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           // Note that get_node may return a nullptr, which would make calling the connect method crash the engine if "Child" does not exist!
           // Vì vậy, trừ khi bạn chắc chắn 1000% rằng get_node sẽ không bao giờ trả về nullptr, bạn nên luôn kiểm tra nullptr.
           node->connect("signal_name", callable_mp(this, &ObjectWithMethod::method_on_the_object));
       }

       // Child
       emit_signal("signal_name"); // Kích hoạt hành vi do parent chỉ định.

2. Gọi một method. Dùng để khởi động hành vi.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Parent
       $Child.method_name = "do"

       # Child, với điều kiện nó có property String 'method_name' và method 'do'.
       call(method_name) # Gọi method do parent chỉ định (method này phải thuộc sở hữu của child).

     .. code-tab:: csharp

       // Parent
       GetNode("Child").Set("MethodName", "Do");

       // Child
       Call(MethodName); // Gọi method do parent chỉ định (method này phải thuộc sở hữu của child).

     .. code-tab:: cpp C++

       // Parent
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("method_name", "do");
       }

       // Child
       call(method_name); // Gọi method do parent chỉ định (method này phải thuộc sở hữu của child).

3. Khởi tạo một property :ref:`Callable <class_Callable>`. An toàn hơn method vì không cần method đó thuộc quyền sở hữu của đối tượng. Dùng để khởi động hành vi.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Parent
       $Child.func_property = object_with_method.method_on_the_object

       # Child
       func_property.call() # Gọi method do parent chỉ định (method này có thể đến từ bất kỳ đâu).

     .. code-tab:: csharp

       // Parent
       GetNode("Child").Set("FuncProperty", Callable.From(ObjectWithMethod.MethodOnTheObject));

       // Child
       FuncProperty.Call(); // Gọi method do parent chỉ định (method này có thể đến từ bất kỳ đâu).

     .. code-tab:: cpp C++

       // Parent
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("func_property", Callable(&ObjectWithMethod::method_on_the_object));
       }

       // Child
       func_property.call(); // Gọi method do parent chỉ định (method này có thể đến từ bất kỳ đâu).

4. Khởi tạo một tham chiếu đến Node hoặc Object khác.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Parent
       $Child.target = self

       # Child
       print(target) # Sử dụng node do parent chỉ định.

     .. code-tab:: csharp

       // Parent
       GetNode("Child").Set("Target", this);

       // Child
       GD.Print(Target); // Sử dụng node do parent chỉ định.

     .. code-tab:: cpp C++

       // Parent
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("target", this);
       }

       // Child
       UtilityFunctions::print(target);

5. Khởi tạo một NodePath.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Parent
       $Child.target_path = ".."

       # Child
       get_node(target_path) # Sử dụng NodePath do parent chỉ định.

     .. code-tab:: csharp

       // Parent
       GetNode("Child").Set("TargetPath", NodePath(".."));

       // Child
       GetNode(TargetPath); // Sử dụng NodePath do parent chỉ định.

     .. code-tab:: cpp C++

       // Parent
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("target_path", NodePath(".."));
       }

       // Child
       get_node<Node>(target_path); // Sử dụng NodePath do parent chỉ định.

Các tùy chọn này ẩn các điểm truy cập khỏi child node. Nhờ đó, child được **liên kết lỏng lẻo** với môi trường của nó. Bạn có thể tái sử dụng nó trong một context khác mà không cần thay đổi gì thêm đối với API của nó.

.. note::

  Mặc dù các ví dụ trên minh họa mối quan hệ parent-child, những nguyên tắc tương tự cũng áp dụng cho mọi mối quan hệ giữa các object. Các node là sibling chỉ nên biết về hierarchy của chính chúng, còn một ancestor sẽ điều phối việc giao tiếp và các tham chiếu giữa chúng.

  .. tabs::
    .. code-tab:: gdscript GDScript

      # Parent
      $Left.target = $Right.get_node("Receiver")

      # Left
      var target: Node
      func execute():
          # Làm gì đó với 'target'.

      # Right
      func _init():
          var receiver = Receiver.new()
          add_child(receiver)

    .. code-tab:: csharp

      // Parent
      GetNode<Left>("Left").Target = GetNode("Right/Receiver");

      public partial class Left : Node
      {
          public Node Target = null;

          public void Execute()
          {
              // Làm gì đó với 'Target'.
          }
      }

      public partial class Right : Node
      {
          public Node Receiver = null;

          public Right()
          {
              Receiver = ResourceLoader.Load<Script>("Receiver.cs").New();
              AddChild(Receiver);
          }
      }

    .. code-tab:: cpp C++

      // Parent
      get_node<Left>("Left")->target = get_node<Node>("Right/Receiver");

      class Left : public Node {
          GDCLASS(Left, Node)

          protected:
              static void _bind_methods() {}

          public:
              Node *target = nullptr;

              Left() {}

              void execute() {
                  // Làm gì đó với 'target'.
              }
      };

      class Right : public Node {
          GDCLASS(Right, Node)

          protected:
              static void _bind_methods() {}

          public:
              Node *receiver = nullptr;

              Right() {
                  receiver = memnew(Node);
                  add_child(receiver);
              }
      };

  Những nguyên tắc tương tự cũng áp dụng cho các object không phải Node nhưng duy trì dependency với những object khác. Object nào sở hữu các object khác thì nên quản lý mối quan hệ giữa chúng.

.. warning::

  Tuy vậy, bạn nên ưu tiên giữ dữ liệu nội bộ (bên trong một scene), vì việc đặt dependency lên một context bên ngoài, ngay cả khi được liên kết lỏng lẻo, vẫn có nghĩa là node sẽ kỳ vọng một điều gì đó trong môi trường của nó là đúng. Các nguyên tắc thiết kế của project nên ngăn điều này xảy ra. Nếu không, những nhược điểm vốn có của code sẽ buộc developer phải dùng documentation để theo dõi các mối quan hệ giữa object ở quy mô vi mô; đây còn được gọi là địa ngục phát triển. Việc viết code phụ thuộc vào documentation bên ngoài để sử dụng an toàn vốn đã dễ phát sinh lỗi.

  Để tránh phải tạo và duy trì loại documentation như vậy, bạn chuyển dependent node ("child" ở trên) thành một tool script triển khai ``_get_configuration_warnings()``. Việc trả về một PackedStringArray không rỗng từ đó sẽ khiến Scene dock tạo một icon cảnh báo, với các string làm tooltip bên node. Đây cũng là icon xuất hiện đối với những node như
  :ref:`Area2D <class_Area2D>` node when it has no child
  :ref:`CollisionShape2D <class_CollisionShape2D>` nodes defined. The editor
  sau đó tự document scene thông qua code trong script. Không cần lặp lại nội dung trong documentation.

  Một `Graphical User Interface (GUI) <https://en.wikipedia.org/wiki/Graphical_user_interface>`_ như thế này có thể cung cấp cho người dùng project thông tin quan trọng về một Node rõ ràng hơn. Nó có dependency bên ngoài không? Những dependency đó đã được đáp ứng chưa? Các programmer khác, đặc biệt là designer và writer, sẽ cần hướng dẫn rõ ràng trong các message cho biết họ phải làm gì để cấu hình nó.

Vậy tại sao toàn bộ màn chuyển đổi phức tạp này lại hiệu quả? Bởi vì scene hoạt động tốt nhất khi hoạt động độc lập. Nếu không thể hoạt động độc lập, thì làm việc ẩn danh với những đối tượng khác (với dependency cứng tối thiểu, tức là liên kết lỏng lẻo) là lựa chọn tốt nhất tiếp theo. Không thể tránh khỏi việc đôi khi cần thay đổi một class, và nếu những thay đổi đó khiến nó tương tác với các scene khác theo những cách không lường trước, mọi thứ sẽ bắt đầu hỏng. Mục đích của toàn bộ cơ chế gián tiếp này là tránh rơi vào tình huống thay đổi một class lại gây ảnh hưởng bất lợi đến các class khác phụ thuộc vào nó.

Scripts và scene, với tư cách là phần mở rộng của các class trong engine, nên tuân thủ *tất cả* nguyên tắc OOP. Ví dụ bao gồm...

- `SOLID: <https://en.wikipedia.org/wiki/SOLID>`_

  - `Single responsibility <https://en.wikipedia.org/wiki/Single-responsibility_principle>`_ - `Open for extension, closed for modification <https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle>`_ - `Liskov substitution <https://en.wikipedia.org/wiki/Liskov_substitution_principle>`_ - `Interface segregation <https://en.wikipedia.org/wiki/Interface_segregation_principle>`_ - `Dependency inversion <https://en.wikipedia.org/wiki/Dependency_inversion_principle>`_

- `DRY: Don't Repeat Yourself <https://en.wikipedia.org/wiki/Don%27t_repeat_yourself>`_ - `KISS: Keep It Simple Stupid <https://en.wikipedia.org/wiki/KISS_principle>`_ - `YAGNI: You Aren't Gonna Need It <https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it>`_

Chọn cấu trúc cây node
----------------------

Bạn có thể bắt đầu làm một game nhưng bị choáng ngợp trước vô số khả năng hiện ra trước mắt. Bạn có thể biết mình muốn làm gì, muốn có những system nào, nhưng *đặt* chúng ở đâu? Cách bạn xây dựng game luôn là lựa chọn của bạn. Bạn có thể cấu trúc cây node theo vô số cách. Nếu không chắc chắn, hướng dẫn này có thể cung cấp cho bạn một cấu trúc mẫu phù hợp để bắt đầu.

Một game luôn phải có một "entry point"; một nơi mà bạn có thể xác định rõ ràng mọi thứ bắt đầu từ đâu để theo dõi logic khi nó tiếp tục ở những nơi khác. Nó cũng đóng vai trò là góc nhìn toàn cảnh về mọi dữ liệu và logic khác trong program. Với các ứng dụng truyền thống, đây thường là một function "main". Trong Godot, đó là một node Main.

- Node "Main" (main.gd)

Script ``main.gd`` sẽ đóng vai trò là controller chính của game.

Sau đó, bạn có một "World" trong game (dạng 2D hoặc 3D). Đây có thể là child của Main. Ngoài ra, bạn sẽ cần một GUI chính cho game để quản lý các menu và widget khác nhau mà project cần.

- Node "Main" (main.gd)

  - Node2D/Node3D "World" (game_world.gd) - Control "GUI" (gui.gd)

Khi thay đổi level, bạn có thể thay thế các child của node "World".
:ref:`Changing scenes manually <doc_change_scenes_manually>` gives you full
quyền kiểm soát cách world trong game chuyển tiếp.

Bước tiếp theo là cân nhắc những gameplay system nào mà project của bạn yêu cầu. Nếu bạn có một system...

1. lưu trữ toàn bộ dữ liệu nội bộ 2. nên có thể truy cập toàn cục 3. nên tồn tại độc lập

... thì bạn nên tạo một :ref:`autoload 'singleton' node <doc_singletons_autoload>`.

.. note::

  Với các game nhỏ hơn, một lựa chọn đơn giản hơn nhưng ít quyền kiểm soát hơn là có một singleton "Game" chỉ đơn giản gọi
  :ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` method
  để thay thế nội dung của main scene. Cấu trúc này ít nhiều vẫn giữ "World" là node chính của game.

  Mọi GUI cũng cần phải là singleton, một phần tạm thời của "World", hoặc được thêm thủ công dưới dạng node con trực tiếp của root. Nếu không, các node GUI cũng sẽ tự xóa trong quá trình chuyển cảnh.

Nếu bạn có các system sửa đổi dữ liệu của các system khác, bạn nên định nghĩa chúng dưới dạng các script hoặc scene riêng, thay vì autoload. Để biết thêm thông tin, hãy xem
:ref:`Autoloads versus regular nodes <doc_autoloads_versus_regular_nodes>`.

Mỗi subsystem trong game của bạn nên có một section riêng trong SceneTree. Bạn chỉ nên sử dụng quan hệ parent-child trong những trường hợp các node thực sự là thành phần của parent. Việc xóa parent có hợp lý khi đồng nghĩa với việc các node con cũng phải bị xóa không? Nếu không, nó nên có vị trí riêng trong hierarchy với tư cách sibling hoặc một quan hệ khác.

.. note::

  Trong một số trường hợp, bạn cần các node được tách riêng này *cũng* tự định vị tương đối với nhau. Bạn có thể sử dụng
  :ref:`RemoteTransform2D <class_RemoteTransform2D>` /
  :ref:`RemoteTransform3D <class_RemoteTransform3D>` nodes for this purpose.
  Chúng cho phép một node đích có điều kiện kế thừa các thành phần transform đã chọn từ node Remote\*. Để gán ``target``
  :ref:`NodePath <class_NodePath>`, use one of the following:

  1. Một bên thứ ba đáng tin cậy, có khả năng là một parent node, để trung gian xử lý việc gán. 2. Một group, để lấy reference đến node mong muốn (giả sử sẽ luôn chỉ có một target).

  Khi nào nên làm điều này là tùy trường hợp. Vấn đề nảy sinh khi bạn phải quản lý vi mô thời điểm một node cần di chuyển trong SceneTree để tự bảo toàn. Ví dụ...

  - Thêm một node "player" vào một "room". - Cần thay đổi room, vì vậy bạn phải xóa room hiện tại. - Trước khi room có thể bị xóa, bạn phải bảo toàn và/hoặc di chuyển player.

    Nếu bộ nhớ không phải là vấn đề, bạn có thể...

    - Tạo room mới. - Di chuyển player vào room mới. - Xóa room cũ.

    Nếu bộ nhớ là một vấn đề, thay vào đó bạn sẽ cần...

    - Di chuyển player đến một nơi khác trong tree. - Xóa room. - Instantiate và thêm room mới. - Thêm lại player vào room mới.

  Vấn đề là player ở đây là một "special case", trong đó các developer phải *biết* rằng họ cần xử lý player theo cách này cho project. Cách duy nhất để chia sẻ thông tin này một cách đáng tin cậy trong team là *document* nó. Việc giữ các chi tiết triển khai trong documentation rất nguy hiểm. Nó tạo thêm gánh nặng bảo trì, làm giảm khả năng đọc code và không cần thiết làm phình to nội dung tri thức của project.

  Trong một game phức tạp hơn với các asset lớn hơn, việc giữ player hoàn toàn ở một nơi khác trong SceneTree có thể là lựa chọn tốt hơn. Điều này mang lại:

  1. Tính nhất quán cao hơn. 2. Không có "special case" nào cần được document và duy trì ở đâu đó. 3. Không có cơ hội phát sinh lỗi vì những chi tiết này không được tính đến.

  Ngược lại, nếu bạn từng cần một node con *không* kế thừa transform của parent, bạn có các tùy chọn sau:

  1. Giải pháp **declarative**: đặt một :ref:`Node <class_Node>` vào giữa chúng. Vì nó không có transform, chúng sẽ không truyền thông tin này cho các node con của nó. 2. Giải pháp **imperative**: Sử dụng property ``top_level`` cho
     :ref:`CanvasItem <class_CanvasItem_property_top_level>` or
     :ref:`Node3D <class_Node3D_property_top_level>` node. This will make
     node bỏ qua transform được kế thừa của nó.

.. note::

  Nếu xây dựng một game networked, hãy lưu ý node và gameplay system nào liên quan đến tất cả người chơi, so với những node và system chỉ liên quan đến authoritative server. Ví dụ, không phải người dùng nào cũng cần có bản sao logic "PlayerController" của mọi player - họ chỉ cần logic của chính mình. Giữ chúng trong một branch riêng với "world" có thể giúp đơn giản hóa việc quản lý các kết nối game và những thứ tương tự.

Chìa khóa để tổ chức scene là xem xét SceneTree theo các quan hệ thay vì theo không gian. Các node có phụ thuộc vào sự tồn tại của parent không? Nếu không, chúng có thể tự hoạt động tốt ở một nơi khác. Nếu có, thì hợp lý khi chúng là node con của parent đó (và có khả năng là một phần của scene của parent đó nếu chúng chưa phải như vậy).

Điều này có nghĩa là bản thân các node là component sao? Hoàn toàn không. Các node tree của Godot tạo thành một quan hệ aggregation, không phải composition. Tuy nhiên, dù bạn vẫn có sự linh hoạt để di chuyển các node, tốt nhất là mặc định không cần thực hiện những lần di chuyển như vậy.
