.. _doc_scene_organization:

Tổ chức scene
=============

Bài viết này trình bày các chủ đề liên quan đến việc tổ chức nội dung scene hiệu quả. Bạn nên sử dụng những node nào? Nên đặt chúng ở đâu? Chúng nên tương tác với nhau như thế nào?

Cách xây dựng mối quan hệ hiệu quả
----------------------------------

Khi bắt đầu tự xây dựng scene, người dùng Godot thường gặp phải vấn đề sau:

Họ tạo scene đầu tiên và thêm đầy đủ nội dung vào đó, nhưng cuối cùng lại lưu các nhánh của scene thành những scene riêng biệt khi cảm giác dai dẳng rằng nên tách chúng ra ngày càng lớn dần. Tuy nhiên, sau đó họ nhận ra rằng các tham chiếu cứng mà trước đây có thể sử dụng không còn khả thi nữa. Việc sử dụng lại scene ở nhiều nơi gây ra vấn đề vì các node path không tìm thấy đối tượng đích, còn các kết nối signal được thiết lập trong editor thì bị hỏng.

Để khắc phục những vấn đề này, bạn phải instantiate các sub-scene mà không yêu cầu chúng biết chi tiết về môi trường xung quanh. Bạn cần có thể tin tưởng rằng sub-scene sẽ tự khởi tạo mà không phụ thuộc vào cách nó được sử dụng.

Một trong những điều quan trọng nhất cần cân nhắc trong `Lập trình hướng đối tượng (Object-Oriented Programming - OOP) <https://en.wikipedia.org/wiki/Object-oriented_programming>`_ là duy trì các class có phạm vi tập trung và mục đích đơn nhất, với `liên kết lỏng <https://en.wikipedia.org/wiki/Loose_coupling>`_ với những phần khác của codebase. Điều này giữ cho kích thước của các object nhỏ (giúp dễ bảo trì hơn) và cải thiện khả năng tái sử dụng của chúng.

Những phương pháp hay nhất của OOP này có *một số* ảnh hưởng đến các phương pháp hay nhất trong cấu trúc scene và cách sử dụng script.

**Nếu có thể, bạn nên thiết kế scene không có dependency.** Nói cách khác, bạn nên tạo các scene tự chứa mọi thứ chúng cần.

Nếu scene bắt buộc phải tương tác với một context bên ngoài, các developer giàu kinh nghiệm khuyến nghị sử dụng `Dependency Injection <https://en.wikipedia.org/wiki/Dependency_injection>`_. Kỹ thuật này yêu cầu một API cấp cao cung cấp các dependency cho API cấp thấp. Tại sao phải làm vậy? Vì các class phụ thuộc vào môi trường bên ngoài có thể vô tình kích hoạt lỗi và hành vi không mong muốn.

Để thực hiện việc này, bạn phải công khai dữ liệu rồi dựa vào context của parent để khởi tạo dữ liệu đó:

1. Kết nối với một signal. Cực kỳ an toàn, nhưng chỉ nên dùng để "phản hồi" hành vi, không dùng để bắt đầu hành vi. Theo quy ước, tên signal thường là các động từ ở thì quá khứ như "entered", "skill_activated" hoặc "item_collected".

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Đối tượng cha
       $Child.signal_name.connect(method_on_the_object)

       # Đối tượng con
       signal_name.emit() # Kích hoạt hành vi do đối tượng cha chỉ định.

     .. code-tab:: csharp

       // Đối tượng cha
       GetNode("Child").Connect("SignalName", Callable.From(ObjectWithMethod.MethodOnTheObject));

       // Đối tượng con
       EmitSignal("SignalName"); // Kích hoạt hành vi do đối tượng cha chỉ định.

     .. code-tab:: cpp C++

       // Đối tượng cha
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           // Lưu ý rằng get_node có thể trả về nullptr, khiến việc gọi phương thức connect làm engine bị crash nếu "Child" không tồn tại!
           // Vì vậy, trừ khi bạn chắc chắn 1000% rằng get_node sẽ không bao giờ trả về nullptr, bạn nên luôn kiểm tra nullptr.
           node->connect("signal_name", callable_mp(this, &ObjectWithMethod::method_on_the_object));
       }

       // Đối tượng con
       emit_signal("signal_name"); // Kích hoạt hành vi do đối tượng cha chỉ định.

2. Gọi một phương thức. Dùng để bắt đầu hành vi.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Đối tượng cha
       $Child.method_name = "do"

       # Đối tượng con, với giả định rằng nó có thuộc tính String 'method_name' và phương thức 'do'.
       call(method_name) # Gọi phương thức do đối tượng cha chỉ định (mà đối tượng con phải sở hữu).

     .. code-tab:: csharp

       // Đối tượng cha
       GetNode("Child").Set("MethodName", "Do");

       // Đối tượng con
       Call(MethodName); // Gọi phương thức do đối tượng cha chỉ định (mà đối tượng con phải sở hữu).

     .. code-tab:: cpp C++

       // Đối tượng cha
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("method_name", "do");
       }

       // Đối tượng con
       call(method_name); // Gọi phương thức do đối tượng cha chỉ định (mà đối tượng con phải sở hữu).

3. Khởi tạo một :ref:`Callable <class_Callable>` thuộc tính. An toàn hơn phương thức vì không cần quyền sở hữu phương thức. Dùng để bắt đầu hành vi.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Đối tượng cha
       $Child.func_property = object_with_method.method_on_the_object

       # Đối tượng con
       func_property.call() # Gọi phương thức do đối tượng cha chỉ định (có thể đến từ bất kỳ đâu).

     .. code-tab:: csharp

       // Đối tượng cha
       GetNode("Child").Set("FuncProperty", Callable.From(ObjectWithMethod.MethodOnTheObject));

       // Đối tượng con
       FuncProperty.Call(); // Gọi phương thức do đối tượng cha chỉ định (có thể đến từ bất kỳ đâu).

     .. code-tab:: cpp C++

       // Đối tượng cha
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("func_property", Callable(&ObjectWithMethod::method_on_the_object));
       }

       // Đối tượng con
       func_property.call(); // Gọi phương thức do đối tượng cha chỉ định (có thể đến từ bất kỳ đâu).

4. Khởi tạo tham chiếu đến một Node hoặc Object khác.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Đối tượng cha
       $Child.target = self

       # Đối tượng con
       print(target) # Sử dụng node do đối tượng cha chỉ định.

     .. code-tab:: csharp

       // Đối tượng cha
       GetNode("Child").Set("Target", this);

       // Đối tượng con
       GD.Print(Target); // Sử dụng node do node cha chỉ định.

     .. code-tab:: cpp C++

       // Đối tượng cha
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("target", this);
       }

       // Đối tượng con
       UtilityFunctions::print(target);

5. Khởi tạo một NodePath.

   .. tabs::
     .. code-tab:: gdscript GDScript

       # Đối tượng cha
       $Child.target_path = ".."

       # Đối tượng con
       get_node(target_path) # Sử dụng NodePath do node cha chỉ định.

     .. code-tab:: csharp

       // Đối tượng cha
       GetNode("Child").Set("TargetPath", NodePath(".."));

       // Đối tượng con
       GetNode(TargetPath); // Sử dụng NodePath do node cha chỉ định.

     .. code-tab:: cpp C++

       // Đối tượng cha
       Node *node = get_node<Node>("Child");
       if (node != nullptr) {
           node->set("target_path", NodePath(".."));
       }

       // Đối tượng con
       get_node<Node>(target_path); // Sử dụng NodePath do node cha chỉ định.

Các tùy chọn này ẩn các điểm truy cập khỏi node con. Nhờ đó, node con được **liên kết lỏng lẻo** với môi trường của nó. Bạn có thể tái sử dụng nó trong một ngữ cảnh khác mà không cần thay đổi gì thêm đối với API của nó.

.. note::

  Mặc dù các ví dụ trên minh họa mối quan hệ cha-con, những nguyên tắc tương tự cũng áp dụng cho mọi mối quan hệ giữa các đối tượng. Các node cùng cấp chỉ nên nhận biết hệ phân cấp của riêng chúng, trong khi một node tổ tiên làm trung gian cho việc giao tiếp và tham chiếu giữa chúng.

  .. tabs::
    .. code-tab:: gdscript GDScript

      # Đối tượng cha
      $Left.target = $Right.get_node("Receiver")

      # Trái
      var target: Node
      func execute():
          # Làm gì đó với 'target'.

      # Phải
      func _init():
          var receiver = Receiver.new()
          add_child(receiver)

    .. code-tab:: csharp

      // Đối tượng cha
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

      // Đối tượng cha
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

  Những nguyên tắc tương tự cũng áp dụng cho các đối tượng không phải Node nhưng duy trì các dependency với những đối tượng khác. Đối tượng nào sở hữu các đối tượng kia thì nên quản lý mối quan hệ giữa chúng.

.. warning::

  Tuy nhiên, bạn nên ưu tiên giữ dữ liệu nội bộ (bên trong một scene), vì việc đặt dependency vào một ngữ cảnh bên ngoài, dù được liên kết lỏng lẻo, vẫn có nghĩa là node sẽ kỳ vọng một điều gì đó trong môi trường của nó là đúng. Các triết lý thiết kế của dự án nên ngăn điều này xảy ra. Nếu không, những hạn chế cố hữu của code sẽ buộc các developer phải dùng tài liệu để theo dõi mối quan hệ giữa các đối tượng ở quy mô rất nhỏ; điều này còn được gọi là địa ngục phát triển. Việc viết code phụ thuộc vào tài liệu bên ngoài để sử dụng an toàn vốn dễ phát sinh lỗi.

  Để tránh việc tạo và duy trì tài liệu như vậy, bạn chuyển node phụ thuộc ("child" ở trên) thành một tool script triển khai ``_get_configuration_warnings()``. Việc trả về một PackedStringArray không rỗng từ đó sẽ khiến Scene dock tạo một biểu tượng cảnh báo, với chuỗi tương ứng làm chú giải cho node. Đây cũng là biểu tượng xuất hiện đối với các node như
  node :ref:`Area2D <class_Area2D>` khi không có node con
  các node :ref:`CollisionShape2D <class_CollisionShape2D>` được định nghĩa. Sau đó, editor sẽ tự ghi lại tài liệu cho scene thông qua code script. Không cần trùng lặp nội dung bằng tài liệu.

  Một `Graphical User Interface (GUI) <https://en.wikipedia.org/wiki/Graphical_user_interface>`_ như thế này có thể cung cấp cho người dùng dự án thông tin quan trọng về một Node rõ ràng hơn. Nó có dependency bên ngoài không? Các dependency đó đã được đáp ứng chưa? Những lập trình viên khác, đặc biệt là designer và writer, sẽ cần các hướng dẫn rõ ràng trong thông báo, cho biết họ cần làm gì để cấu hình nó.

Vậy tại sao toàn bộ cách chuyển đổi phức tạp này lại hiệu quả? Đó là vì scene hoạt động tốt nhất khi hoạt động độc lập. Nếu không thể hoạt động độc lập, thì làm việc ẩn danh với các thành phần khác (với ít hard dependency nhất có thể, tức là liên kết lỏng lẻo) là lựa chọn tốt thứ hai. Không thể tránh khỏi việc phải thay đổi một class, và nếu những thay đổi đó khiến nó tương tác với các scene khác theo những cách không lường trước, mọi thứ sẽ bắt đầu hỏng. Toàn bộ mục đích của việc tạo lớp gián tiếp này là tránh rơi vào tình huống thay đổi một class lại gây ảnh hưởng bất lợi đến các class khác phụ thuộc vào nó.

Scripts và scene, với tư cách là phần mở rộng của các class engine, nên tuân thủ *tất cả* các nguyên tắc OOP. Ví dụ gồm...

- `SOLID: <https://en.wikipedia.org/wiki/SOLID>`_

  - `Single responsibility <https://en.wikipedia.org/wiki/Single-responsibility_principle>`_
  - `Open for extension, closed for modification <https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle>`_
  - `Liskov substitution <https://en.wikipedia.org/wiki/Liskov_substitution_principle>`_
  - `Interface segregation <https://en.wikipedia.org/wiki/Interface_segregation_principle>`_
  - `Dependency inversion <https://en.wikipedia.org/wiki/Dependency_inversion_principle>`_

- `DRY: Don't Repeat Yourself <https://en.wikipedia.org/wiki/Don%27t_repeat_yourself>`_
- `KISS: Keep It Simple Stupid <https://en.wikipedia.org/wiki/KISS_principle>`_
- `YAGNI: You Aren't Gonna Need It <https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it>`_

Chọn cấu trúc cây node
----------------------

Bạn có thể bắt đầu phát triển một game nhưng bị choáng ngợp trước vô số khả năng hiện ra trước mắt. Bạn có thể biết mình muốn làm gì, muốn có những hệ thống nào, nhưng *đặt chúng ở đâu*? Cách bạn tạo game luôn tùy thuộc vào bạn. Bạn có thể xây dựng cây node theo vô số cách. Nếu chưa chắc chắn, hướng dẫn này có thể cung cấp cho bạn một cấu trúc mẫu phù hợp để bắt đầu.

Một game luôn nên có một "điểm vào"; một nơi mà bạn có thể xác định rõ ràng mọi thứ bắt đầu từ đâu để theo dõi logic khi nó tiếp tục ở nơi khác. Nó cũng đóng vai trò là góc nhìn tổng quan về mọi dữ liệu và logic khác trong chương trình. Đối với các ứng dụng truyền thống, đây thường là một hàm "main". Trong Godot, đó là một node Main.

- Node "Main" (main.gd)

Script ``main.gd`` sẽ đóng vai trò là bộ điều khiển chính của game.

Sau đó, bạn có một "World" trong game (2D hoặc 3D). Đây có thể là một nút con của Main. Ngoài ra, bạn sẽ cần một GUI chính cho game để quản lý các menu và widget khác nhau mà dự án yêu cầu.

- Node "Main" (main.gd)

  - Node2D/Node3D "World" (game_world.gd)
  - Control "GUI" (gui.gd)

Khi thay đổi level, bạn có thể thay thế các nút con của nút "World".
:ref:`Thay đổi scene theo cách thủ công <doc_change_scenes_manually>` cho phép bạn kiểm soát hoàn toàn cách chuyển tiếp giữa các world trong game.

Bước tiếp theo là cân nhắc những gameplay system nào mà dự án của bạn yêu cầu. Nếu bạn có một system...

1. theo dõi toàn bộ dữ liệu của chính nó
2. nên có thể được truy cập trên toàn cục
3. nên tồn tại độc lập

... thì bạn nên tạo một :ref:`node 'singleton' autoload <doc_singletons_autoload>`.

.. note::

  Đối với các game nhỏ hơn, một phương án đơn giản hơn nhưng ít quyền kiểm soát hơn là có một singleton "Game" chỉ gọi
  :ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` để thay thế nội dung của main scene. Cấu trúc này ít nhiều vẫn giữ "World" làm node chính của game.

  Mọi GUI cũng sẽ cần phải là một singleton, một phần tạm thời của "World", hoặc được thêm thủ công làm nút con trực tiếp của root. Nếu không, các node GUI cũng sẽ tự xóa trong quá trình chuyển scene.

Nếu bạn có các system sửa đổi dữ liệu của những system khác, bạn nên định nghĩa chúng bằng các script hoặc scene riêng, thay vì autoload. Để biết thêm thông tin, hãy xem
:ref:`Autoload so với node thông thường <doc_autoloads_versus_regular_nodes>`.

Mỗi subsystem trong game của bạn nên có một section riêng trong SceneTree. Bạn chỉ nên sử dụng quan hệ cha-con khi các node thực sự là thành phần của node cha. Nếu xóa node cha, việc xóa các node con có hợp lý không? Nếu không, node đó nên có vị trí riêng trong hệ phân cấp, với tư cách là một node ngang hàng hoặc một quan hệ khác.

.. note::

  Trong một số trường hợp, bạn cần các node được tách riêng này *cũng* tự định vị tương đối với nhau. Bạn có thể sử dụng các
  :ref:`RemoteTransform2D <class_RemoteTransform2D>` /
  :ref:`RemoteTransform3D <class_RemoteTransform3D>` node cho mục đích này. Chúng cho phép một node đích kế thừa có điều kiện các thành phần transform được chọn từ node Remote\*. Để gán ``target``
  :ref:`NodePath <class_NodePath>`, hãy sử dụng một trong các cách sau:

  1. Một bên thứ ba đáng tin cậy, có thể là một node cha, để trung gian xử lý việc gán.
  2. Một group, để lấy tham chiếu đến node mong muốn (giả sử sẽ chỉ có một target).

  Việc có nên làm điều này hay không mang tính chủ quan. Vấn đề nảy sinh khi bạn phải quản lý quá chi tiết thời điểm một node cần di chuyển trong SceneTree để tự bảo toàn. Ví dụ...

  - Thêm một node "player" vào một "room".
  - Cần thay đổi room, vì vậy bạn phải xóa room hiện tại.
  - Trước khi room có thể bị xóa, bạn phải bảo toàn và/hoặc di chuyển player.

    Nếu bộ nhớ không phải là vấn đề, bạn có thể...

    - Tạo room mới.
    - Di chuyển player vào room mới.
    - Xóa room cũ.

    Nếu bộ nhớ là vấn đề, thay vào đó bạn sẽ cần...

    - Di chuyển player đến một nơi khác trong tree.
    - Xóa room.
    - Instantiate và thêm room mới.
    - Thêm lại player vào room mới.

  Vấn đề ở đây là player là một "trường hợp đặc biệt", trong đó các developer phải *biết* rằng họ cần xử lý player theo cách này cho dự án. Cách duy nhất để chia sẻ thông tin này một cách đáng tin cậy trong nhóm là *ghi lại* thông tin đó. Việc giữ các chi tiết triển khai trong tài liệu rất nguy hiểm. Nó tạo thêm gánh nặng bảo trì, làm giảm tính dễ đọc của code và khiến nội dung tri thức của dự án phình to không cần thiết.

  Trong một game phức tạp hơn với các asset lớn hơn, giữ player ở một nơi khác hoàn toàn trong SceneTree có thể là lựa chọn tốt hơn. Điều này mang lại:

  1. Tính nhất quán cao hơn.
  2. Không có "trường hợp đặc biệt" nào cần được ghi lại và duy trì ở đâu đó.
  3. Không có cơ hội phát sinh lỗi vì những chi tiết này không được tính đến.

  Ngược lại, nếu bạn cần một node con không *kế thừa* transform của node cha, bạn có các lựa chọn sau:

  1. Giải pháp **declarative**: đặt một :ref:`Node <class_Node>` vào giữa chúng. Vì nó không có transform, chúng sẽ không truyền thông tin này cho các node con của nó.
  2. Giải pháp **imperative**: Sử dụng thuộc tính ``top_level`` cho
     :ref:`CanvasItem <class_CanvasItem_property_top_level>` hoặc
     :ref:`Node3D <class_Node3D_property_top_level>` node. Điều này sẽ khiến node bỏ qua transform được kế thừa.

.. note::

  Nếu xây dựng một game có mạng, hãy lưu ý những node và gameplay system nào liên quan đến tất cả người chơi, so với những node và system chỉ liên quan đến authoritative server. Ví dụ, người dùng không cần có bản sao logic "PlayerController" của mọi player - họ chỉ cần logic của chính mình. Giữ chúng trong một branch riêng với "world" có thể giúp đơn giản hóa việc quản lý các kết nối game và những thứ tương tự.

Điểm mấu chốt để tổ chức scene là xem xét SceneTree theo các mối quan hệ thay vì theo vị trí không gian. Các node có phụ thuộc vào sự tồn tại của node cha không? Nếu không, chúng có thể tự hoạt động tốt ở một nơi khác. Nếu có, việc chúng là node con của node cha đó là hợp lý (và có khả năng chúng cũng nên là một phần của scene của node cha nếu chưa phải như vậy).

Điều này có nghĩa là bản thân các node là component sao? Hoàn toàn không. Các node tree của Godot tạo thành một quan hệ aggregation, không phải composition. Tuy nhiên, dù bạn vẫn có sự linh hoạt để di chuyển các node, tốt nhất là mặc định không cần thực hiện những thao tác di chuyển đó.

.. _`Object-Oriented Programming (OOP)`: https://en.wikipedia.org/wiki/Object-oriented_programming
.. _`loose coupling`: https://en.wikipedia.org/wiki/Loose_coupling
.. _`Dependency Injection`: https://en.wikipedia.org/wiki/Dependency_injection
.. _`Graphical User Interface (GUI)`: https://en.wikipedia.org/wiki/Graphical_user_interface
.. _`SOLID:`: https://en.wikipedia.org/wiki/SOLID
.. _`Single responsibility`: https://en.wikipedia.org/wiki/Single-responsibility_principle
.. _`Open for extension, closed for modification`: https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
.. _`Liskov substitution`: https://en.wikipedia.org/wiki/Liskov_substitution_principle
.. _`Interface segregation`: https://en.wikipedia.org/wiki/Interface_segregation_principle
.. _`Dependency inversion`: https://en.wikipedia.org/wiki/Dependency_inversion_principle
.. _`DRY: Don't Repeat Yourself`: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
.. _`KISS: Keep It Simple Stupid`: https://en.wikipedia.org/wiki/KISS_principle
.. _`YAGNI: You Aren't Gonna Need It`: https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it
