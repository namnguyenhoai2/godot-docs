..
    Mục đích:

    - Cung cấp phần giới thiệu thực hành *ngắn gọn* và dễ hiểu về GDScript. Trang này nên tập trung vào việc làm việc trong trình soạn thảo mã.
    - Chúng tôi giả định người đọc đã có nền tảng lập trình. Nếu chưa, bạn nên tham gia khóa học được đề xuất trong :ref:`trang giới thiệu về Godot <doc_introduction_learning_programming>`.

    Kỹ thuật:

    - Tạo một sprite.
    - Tạo một script.
    - _init() và _process().
    - Di chuyển một đối tượng trên màn hình.

.. _doc_scripting_first_script:

Tạo script đầu tiên
===================

Trong bài học này, bạn sẽ viết code cho script đầu tiên để làm cho biểu tượng Godot xoay theo vòng tròn. Như đã đề cập :ref:`trong phần giới thiệu <doc_introduction_learning_programming>`, chúng tôi giả định bạn đã có nền tảng lập trình.

Hướng dẫn này được viết cho GDScript, còn code C# tương đương được đưa vào tab khác của mỗi codeblock để tiện tham khảo.

.. image:: img/scripting_first_script_rotating_godot.gif

.. seealso:: Để tìm hiểu thêm về GDScript, các từ khóa và cú pháp của nó, hãy truy cập phần :ref:`doc_gdscript`. Để tìm hiểu thêm về C#, hãy truy cập phần :ref:`doc_c_sharp`.

Thiết lập dự án
---------------

Vui lòng :ref:`tạo một dự án mới <doc_creating_and_importing_projects>` để bắt đầu với một dự án trống. Dự án của bạn nên chứa một hình ảnh: biểu tượng Godot, hình ảnh mà cộng đồng thường sử dụng để tạo prototype.

.. image:: img/scripting_first_script_icon.svg

Chúng ta cần tạo một node Sprite2D để hiển thị hình ảnh đó trong game. Trong dock :ui:`Scene`, hãy nhấp vào nút :button:`Other Node`.

.. image:: img/scripting_first_script_click_other_node.webp

Nhập "Sprite2D" vào thanh tìm kiếm để lọc các node, sau đó nhấp đúp vào Sprite2D để tạo node.

.. image:: img/scripting_first_script_add_sprite_node.webp

Tab :ui:`Scene` của bạn lúc này chỉ nên có một node Sprite2D.

.. image:: img/scripting_first_script_scene_tree.webp

Node Sprite2D cần một texture để hiển thị. Trong :ui:`Inspector` ở bên phải, bạn có thể thấy thuộc tính :inspector:`Texture` có giá trị là ``<empty>``. Để hiển thị biểu tượng Godot, hãy nhấp và kéo tệp ``icon.svg`` từ dock FileSystem vào ô Texture.

.. image:: img/scripting_first_script_setting_texture.webp

.. note::

    Bạn có thể tự động tạo các node Sprite2D bằng cách kéo và thả hình ảnh vào viewport.

Sau đó, nhấp và kéo biểu tượng trong viewport để căn giữa biểu tượng trong khung nhìn game.

.. image:: img/scripting_first_script_centering_sprite.webp

Tạo script mới
--------------

Để tạo và gắn một script mới vào node, hãy nhấp chuột phải vào Sprite2D trong dock Scene rồi chọn :button:`Attach Script`.

.. image:: img/scripting_first_script_attach_script.webp

Cửa sổ :ui:`Attach Node Script` xuất hiện. Cửa sổ này cho phép bạn chọn ngôn ngữ và đường dẫn tệp của script, cùng với các tùy chọn khác.

Đổi trường :ui:`Template` từ ``Node: Default`` thành ``Object: Empty`` để bắt đầu với một tệp trống. Giữ nguyên các tùy chọn khác ở giá trị mặc định rồi nhấp vào nút :button:`Create` để tạo script.

.. image:: img/scripting_first_script_attach_node_script.webp

.. note::

    Tên script C# cần khớp với tên class. Trong trường hợp này, bạn nên đặt tên tệp là ``MySprite2D.cs``.

Workspace :ui:`Script` sẽ xuất hiện, với tệp ``sprite_2d.gd`` mới được mở và dòng code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

 .. code-tab:: csharp C#

    using Godot;
    using System;

    public partial class MySprite2D : Sprite2D
    {
    }

Mọi tệp GDScript về bản chất đều là một class. Từ khóa ``extends`` xác định class mà script này kế thừa hoặc mở rộng. Trong trường hợp này, đó là ``Sprite2D``, nghĩa là script của chúng ta sẽ có quyền truy cập vào tất cả thuộc tính và hàm của node Sprite2D, bao gồm cả các class mà nó mở rộng, như ``Node2D``, ``CanvasItem`` và ``Node``.

.. note:: Trong GDScript, nếu bỏ qua dòng có từ khóa ``extends``, class của bạn sẽ ngầm mở rộng :ref:`RefCounted <class_RefCounted>`, class mà Godot sử dụng để quản lý bộ nhớ của ứng dụng.

Các thuộc tính kế thừa bao gồm những thuộc tính bạn có thể thấy trong dock :ui:`Inspector`, chẳng hạn như ``texture`` của node.

.. note::

    Theo mặc định, :ui:`Inspector` hiển thị các thuộc tính của node ở dạng "Title Case", với các từ viết hoa được ngăn cách bằng dấu cách. Trong code GDScript, các thuộc tính này có dạng "snake_case", tức là viết thường và mỗi từ được ngăn cách bằng dấu gạch dưới.

    Bạn có thể di chuột lên tên của bất kỳ thuộc tính nào trong :ui:`Inspector` để xem mô tả và identifier của thuộc tính đó trong code.

Hello, world!
-------------

Hiện tại script của chúng ta chưa làm gì cả. Hãy bắt đầu bằng cách cho script in dòng chữ "Hello, world!" vào panel Output ở phía dưới.

Thêm đoạn code sau vào script:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _init():
        print("Hello, world!")

 .. code-tab:: csharp C#

    public MySprite2D()
    {
        GD.Print("Hello, world!");
    }


Hãy phân tích đoạn code. Từ khóa ``func`` định nghĩa một hàm mới có tên ``_init``. Đây là tên đặc biệt dành cho constructor của class. Engine sẽ gọi ``_init()`` trên mọi object hoặc node khi tạo object hoặc node đó trong bộ nhớ, nếu bạn định nghĩa hàm này.

.. note:: GDScript là ngôn ngữ dựa trên thụt lề. Tab ở đầu dòng chứa ``print()`` là cần thiết để code hoạt động. Nếu bỏ qua tab này hoặc thụt lề một dòng không đúng, trình soạn thảo sẽ tô sáng dòng đó màu đỏ và hiển thị thông báo lỗi sau: "Indented block expected".

Lưu scene dưới tên ``sprite_2d.tscn`` nếu bạn chưa làm vậy, sau đó nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS) để chạy. Hãy nhìn vào panel :ui:`Output` ở phía dưới đang mở rộng. Panel này sẽ hiển thị "Hello, world!".

.. image:: img/scripting_first_script_print_hello_world.webp

Xóa hàm ``_init()``, để bạn chỉ còn lại dòng ``extends Sprite2D``.

Xoay vòng
---------

Đã đến lúc làm cho node di chuyển và xoay. Để thực hiện việc đó, chúng ta sẽ thêm hai biến thành viên vào script: tốc độ di chuyển tính bằng pixel mỗi giây và tốc độ góc tính bằng radian mỗi giây. Thêm đoạn sau sau dòng ``extends Sprite2D``.

.. tabs::
 .. code-tab:: gdscript GDScript

    var speed = 400
    var angular_speed = PI

 .. code-tab:: csharp C#

    private int _speed = 400;
    private float _angularSpeed = Mathf.Pi;

Các biến thành viên nằm gần đầu script, sau mọi dòng "extends" nhưng trước các hàm. Mỗi instance của node được gắn script này sẽ có bản sao riêng của các thuộc tính ``speed`` và ``angular_speed``.

.. note:: Theo mặc định, các góc trong Godot được tính bằng radian, nhưng bạn có thể sử dụng các hàm và thuộc tính tích hợp sẵn nếu muốn tính góc bằng độ.

Để di chuyển biểu tượng, chúng ta cần cập nhật vị trí và góc xoay của nó trong mỗi frame của game loop. Chúng ta có thể sử dụng hàm ảo ``_process()`` của class ``Node``. Nếu bạn định nghĩa hàm này trong bất kỳ class nào mở rộng class Node, chẳng hạn như Sprite2D, Godot sẽ gọi hàm đó trong mỗi frame và truyền cho hàm một đối số có tên ``delta``, là khoảng thời gian đã trôi qua kể từ frame trước.

.. note::

    Game hoạt động bằng cách kết xuất nhiều hình ảnh mỗi giây, mỗi hình ảnh được gọi là một frame, và thực hiện việc đó trong một vòng lặp. Chúng ta đo tốc độ game tạo ra hình ảnh bằng Frames Per Second (FPS). Hầu hết game hướng tới 60 FPS, mặc dù trên các thiết bị di động chậm hơn, bạn có thể gặp các mức như 30 FPS; còn game thực tế ảo có thể đạt từ 90 đến 240 FPS.

    Engine và các nhà phát triển game cố gắng hết sức để cập nhật thế giới game và kết xuất hình ảnh trong một khoảng thời gian không đổi, nhưng thời gian kết xuất mỗi frame luôn có những dao động nhỏ. Vì vậy, engine cung cấp cho chúng ta giá trị delta time này, giúp chuyển động không phụ thuộc vào framerate.

Ở cuối script, hãy định nghĩa hàm:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        rotation += angular_speed * delta

 .. code-tab:: csharp C#

    public override void _Process(double delta)
    {
        Rotation += _angularSpeed * (float)delta;
    }

Từ khóa ``func`` định nghĩa một hàm mới. Sau từ khóa đó, chúng ta phải viết tên hàm và các đối số mà hàm nhận trong dấu ngoặc đơn. Dấu hai chấm kết thúc phần định nghĩa, còn các block được thụt lề theo sau là nội dung hoặc các chỉ dẫn của hàm.

.. note:: Hãy chú ý rằng ``_process()``, giống như ``_init()``, bắt đầu bằng một dấu gạch dưới. Theo quy ước, các hàm virtual của Godot, tức là những hàm dựng sẵn mà bạn có thể override để giao tiếp với engine, bắt đầu bằng dấu gạch dưới.

Dòng bên trong hàm, ``rotation += angular_speed * delta``, tăng rotation của sprite sau mỗi frame. Ở đây, ``rotation`` là một thuộc tính được kế thừa từ class ``Node2D``, mà ``Sprite2D`` mở rộng. Thuộc tính này điều khiển rotation của node và sử dụng radian.

.. tip:: Trong code editor, bạn có thể :kbd:`Ctrl + Click` (:kbd:`Cmd + Click` trên macOS) trên bất kỳ thuộc tính hoặc hàm dựng sẵn nào như ``position``, ``rotation`` hoặc ``_process`` để mở tài liệu tương ứng trong một tab mới.

Chạy scene để xem biểu tượng Godot xoay tại chỗ.

.. image:: img/scripting_first_script_godot_turning_in_place.gif

.. note:: Trong C#, hãy chú ý rằng đối số ``delta`` được ``_Process()`` nhận vào là một ``double``. Vì vậy, chúng ta cần chuyển đổi nó thành ``float`` khi áp dụng nó cho rotation.

Di chuyển về phía trước
~~~~~~~~~~~~~~~~~~~~~~~

Bây giờ hãy làm cho node di chuyển. Thêm hai dòng sau vào bên trong hàm ``_process()``, đảm bảo các dòng mới được thụt lề giống như dòng ``rotation += angular_speed * delta`` ở phía trên.

.. tabs::
 .. code-tab:: gdscript GDScript

    var velocity = Vector2.UP.rotated(rotation) * speed

    position += velocity * delta

 .. code-tab:: csharp C#

    var velocity = Vector2.Up.Rotated(Rotation) * _speed;

    Position += velocity * (float)delta;

Như chúng ta đã thấy, từ khóa ``var`` định nghĩa một biến mới. Nếu đặt từ khóa này ở đầu script, nó sẽ định nghĩa một thuộc tính của class. Bên trong một hàm, nó định nghĩa một biến cục bộ: biến này chỉ tồn tại trong phạm vi của hàm.

Chúng ta định nghĩa một biến cục bộ có tên ``velocity``, là một vector 2D biểu diễn cả hướng và tốc độ. Để làm cho node di chuyển về phía trước, chúng ta bắt đầu từ hằng số ``Vector2.UP`` của class Vector2, một vector hướng lên trên, rồi xoay nó bằng cách gọi phương thức ``rotated()`` của Vector2. Biểu thức này, ``Vector2.UP.rotated(rotation)``, là một vector hướng về phía trước tương đối so với biểu tượng của chúng ta. Khi nhân với thuộc tính ``speed``, nó cho chúng ta một vận tốc có thể dùng để di chuyển node về phía trước.

Chúng ta thêm ``velocity * delta`` vào ``position`` của node để di chuyển node. Bản thân position có kiểu :ref:`Vector2 <class_Vector2>`, một kiểu dựng sẵn trong Godot dùng để biểu diễn vector 2D.

Chạy scene để xem đầu Godot chạy thành vòng tròn.

.. image:: img/scripting_first_script_rotating_godot.gif

.. note:: Cách di chuyển node như vậy không tính đến việc va chạm với tường hoặc sàn. Trong :ref:`doc_your_first_2d_game`, bạn sẽ học một cách tiếp cận khác để di chuyển các đối tượng đồng thời phát hiện va chạm.

Hiện tại node của chúng ta tự di chuyển. Trong phần tiếp theo,
:ref:`doc_scripting_player_input`, chúng ta sẽ dùng input của người chơi để điều khiển node.

Script hoàn chỉnh
-----------------

Dưới đây là file ``sprite_2d.gd`` hoàn chỉnh để tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400
    var angular_speed = PI


    func _process(delta):
        rotation += angular_speed * delta

        var velocity = Vector2.UP.rotated(rotation) * speed

        position += velocity * delta

 .. code-tab:: csharp C#

    using Godot;
    using System;

    public partial class MySprite2D : Sprite2D
    {
        private int _speed = 400;
        private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta)
        {
            Rotation += _angularSpeed * (float)delta;
            var velocity = Vector2.Up.Rotated(Rotation) * _speed;

            Position += velocity * (float)delta;
        }
    }
