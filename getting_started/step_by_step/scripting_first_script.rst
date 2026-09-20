.. Mục đích:

    - Giới thiệu thực hành *ngắn gọn* và dễ hiểu về GDScript. Trang này tập trung vào việc làm việc trong trình soạn thảo mã. - Chúng tôi giả định người đọc đã có nền tảng lập trình. Nếu chưa, hãy cân nhắc tham gia khóa học mà chúng tôi đề xuất trong :ref:`introduction to Godot page <doc_introduction_learning_programming>`.

    Kỹ thuật:

    - Tạo một sprite. - Tạo một script. - _init() và _process(). - Di chuyển một đối tượng trên màn hình.

.. _doc_scripting_first_script:

Tạo script đầu tiên
===================

Trong bài học này, bạn sẽ viết mã cho script đầu tiên để làm cho biểu tượng Godot xoay theo vòng tròn. Như chúng tôi đã đề cập trong :ref:`in the introduction <doc_introduction_learning_programming>`, chúng tôi giả định bạn đã có nền tảng lập trình.

Hướng dẫn này được viết cho GDScript và mã C# tương đương được đưa vào một tab khác của mỗi khối mã để tiện theo dõi.

.. image:: img/scripting_first_script_rotating_godot.gif

.. seealso:: To learn more about GDScript, its keywords, and its syntax, head to
             phần :ref:`doc_gdscript`. Để tìm hiểu thêm về C#, hãy chuyển đến phần :ref:`doc_c_sharp`.

Thiết lập dự án
---------------

Vui lòng :ref:`create a new project <doc_creating_and_importing_projects>` để bắt đầu với một dự án sạch. Dự án của bạn sẽ chứa một hình ảnh: biểu tượng Godot, hình ảnh mà chúng tôi thường dùng để tạo nguyên mẫu trong cộng đồng.

.. image:: img/scripting_first_script_icon.svg

Chúng ta cần tạo một nút Sprite2D để hiển thị hình ảnh này trong trò chơi. Trong dock :ui:`Scene`, hãy nhấp vào nút :button:`Other Node`.

.. image:: img/scripting_first_script_click_other_node.webp

Nhập "Sprite2D" vào thanh tìm kiếm để lọc các nút, sau đó nhấp đúp vào Sprite2D để tạo nút.

.. image:: img/scripting_first_script_add_sprite_node.webp

Tab :ui:`Scene` của bạn lúc này chỉ nên có một nút Sprite2D.

.. image:: img/scripting_first_script_scene_tree.webp

Một nút Sprite2D cần có texture để hiển thị. Trong :ui:`Inspector` ở bên phải, bạn có thể thấy thuộc tính :inspector:`Texture` có giá trị là ``<empty>``. Để hiển thị biểu tượng Godot, hãy nhấp và kéo tệp ``icon.svg`` từ dock FileSystem vào ô Texture.

.. image:: img/scripting_first_script_setting_texture.webp

.. note::

    Bạn có thể tự động tạo các nút Sprite2D bằng cách kéo và thả hình ảnh vào khung nhìn.

Sau đó, hãy nhấp và kéo biểu tượng trong khung nhìn để căn giữa biểu tượng trong khung nhìn trò chơi.

.. image:: img/scripting_first_script_centering_sprite.webp

Tạo script mới
--------------

Để tạo và gắn một script mới vào nút của chúng ta, hãy nhấp chuột phải vào Sprite2D trong dock Scene và chọn :button:`Attach Script`.

.. image:: img/scripting_first_script_attach_script.webp

Cửa sổ :ui:`Attach Node Script` xuất hiện. Cửa sổ này cho phép bạn chọn ngôn ngữ và đường dẫn tệp của script, cùng nhiều tùy chọn khác.

Đổi trường :ui:`Template` từ ``Node: Default`` thành ``Object: Empty`` để bắt đầu với một tệp trống. Giữ nguyên các tùy chọn khác ở giá trị mặc định, rồi nhấp vào nút :button:`Create` để tạo script.

.. image:: img/scripting_first_script_attach_node_script.webp

.. note::

    Tên script C# cần khớp với tên lớp của chúng. Trong trường hợp này, bạn nên đặt tên tệp là ``MySprite2D.cs``.

Không gian làm việc :ui:`Script` sẽ xuất hiện cùng với tệp ``sprite_2d.gd`` mới đang mở và dòng mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

 .. code-tab:: csharp C#

    using Godot; using System;

    public partial class MySprite2D : Sprite2D { }

Mỗi tệp GDScript ngầm định là một lớp. Từ khóa ``extends`` xác định lớp mà script này kế thừa hoặc mở rộng. Trong trường hợp này, đó là ``Sprite2D``, nghĩa là script của chúng ta sẽ có quyền truy cập vào tất cả thuộc tính và hàm của nút Sprite2D, bao gồm cả các lớp mà nó mở rộng, như ``Node2D``, ``CanvasItem`` và ``Node``.

.. note:: In GDScript, if you omit the line with the ``extends`` keyword, your
          lớp sẽ ngầm định mở rộng :ref:`RefCounted <class_RefCounted>`, lớp mà Godot sử dụng để quản lý bộ nhớ của ứng dụng.

Các thuộc tính kế thừa bao gồm những thuộc tính bạn có thể thấy trong dock :ui:`Inspector`, chẳng hạn như ``texture`` của nút.

.. note::

    Theo mặc định, :ui:`Inspector` hiển thị các thuộc tính của một nút ở dạng "Title Case", với các từ viết hoa được phân cách bằng dấu cách. Trong mã GDScript, các thuộc tính này ở dạng "snake_case", trong đó tất cả chữ cái đều viết thường và mỗi từ được phân cách bằng dấu gạch dưới.

    Bạn có thể di chuột lên tên của bất kỳ thuộc tính nào trong :ui:`Inspector` để xem mô tả và mã định danh của thuộc tính đó.

Hello, world!
-------------

Hiện tại script của chúng ta chưa làm gì cả. Hãy để nó in văn bản "Hello, world!" vào bảng điều khiển dưới cùng Output để bắt đầu.

Thêm đoạn mã sau vào script của bạn:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _init(): print("Hello, world!")

 .. code-tab:: csharp C#

    public MySprite2D() { GD.Print("Hello, world!"); }


Hãy phân tích đoạn mã này. Từ khóa ``func`` định nghĩa một hàm mới có tên ``_init``. Đây là tên đặc biệt dành cho hàm khởi tạo của lớp. Engine sẽ gọi ``_init()`` trên mọi đối tượng hoặc nút ngay sau khi tạo nó trong bộ nhớ, nếu bạn định nghĩa hàm này.

.. note:: GDScript is an indent-based language. The tab at the start of the line
          cho biết rằng ``print()`` là cần thiết để mã hoạt động. Nếu bạn bỏ qua nó hoặc không thụt lề một dòng đúng cách, trình soạn thảo sẽ đánh dấu dòng đó màu đỏ và hiển thị thông báo lỗi sau: "Indented block expected".

Lưu cảnh dưới tên ``sprite_2d.tscn`` nếu bạn chưa làm vậy, sau đó nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS) để chạy cảnh. Hãy nhìn vào bảng điều khiển dưới cùng :ui:`Output` được mở rộng. Bảng này sẽ hiển thị "Hello, world!".

.. image:: img/scripting_first_script_print_hello_world.webp

Xóa hàm ``_init()``, để bạn chỉ còn lại dòng ``extends Sprite2D``.

Xoay vòng
---------

Đã đến lúc làm cho nút di chuyển và xoay. Để thực hiện việc này, chúng ta sẽ thêm hai biến thành viên vào script: tốc độ di chuyển tính bằng pixel mỗi giây và tốc độ góc tính bằng radian mỗi giây. Thêm đoạn mã sau bên dưới dòng ``extends Sprite2D``.

.. tabs::
 .. code-tab:: gdscript GDScript

    var speed = 400 var angular_speed = PI

 .. code-tab:: csharp C#

    private int _speed = 400; private float _angularSpeed = Mathf.Pi;

Các biến thành viên nằm gần đầu script, sau mọi dòng "extends" nhưng trước các hàm. Mỗi thực thể nút được gắn script này sẽ có bản sao riêng của các thuộc tính ``speed`` và ``angular_speed``.

.. note:: Angles in Godot work in radians by default,
          nhưng bạn có sẵn các hàm và thuộc tính tích hợp nếu muốn tính góc theo độ.

Để di chuyển biểu tượng, chúng ta cần cập nhật vị trí và góc xoay của nó trong mỗi khung hình của vòng lặp trò chơi. Chúng ta có thể sử dụng hàm ảo ``_process()`` của lớp ``Node``. Nếu bạn định nghĩa hàm này trong bất kỳ lớp nào mở rộng lớp Node, chẳng hạn như Sprite2D, Godot sẽ gọi hàm này trong mỗi khung hình và truyền cho nó một đối số có tên ``delta``, là khoảng thời gian đã trôi qua kể từ khung hình trước.

.. note::

    Trò chơi hoạt động bằng cách kết xuất nhiều hình ảnh mỗi giây, mỗi hình ảnh được gọi là một khung hình, và thực hiện việc này trong một vòng lặp. Chúng ta đo tốc độ trò chơi tạo ra hình ảnh bằng Frames Per Second (FPS). Hầu hết trò chơi nhắm đến 60 FPS, mặc dù trên các thiết bị di động chậm hơn, bạn có thể gặp các mức như 30 FPS, hoặc từ 90 đến 240 FPS đối với trò chơi thực tế ảo.

    Engine và các nhà phát triển trò chơi cố gắng hết sức để cập nhật thế giới trò chơi và kết xuất hình ảnh theo một khoảng thời gian cố định, nhưng thời gian kết xuất mỗi khung hình luôn có những biến động nhỏ. Đó là lý do engine cung cấp cho chúng ta giá trị thời gian delta này, giúp chuyển động không phụ thuộc vào tốc độ khung hình.

Ở cuối script, hãy định nghĩa hàm:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta): rotation += angular_speed * delta

 .. code-tab:: csharp C#

    public override void _Process(double delta) { Rotation += _angularSpeed * (float)delta; }

Từ khóa ``func`` định nghĩa một hàm mới. Sau từ khóa đó, chúng ta phải viết tên hàm và các đối số mà hàm nhận trong dấu ngoặc đơn. Dấu hai chấm kết thúc phần định nghĩa, còn các khối được thụt lề theo sau là nội dung hoặc các chỉ dẫn của hàm.

.. note:: Notice how ``_process()``, like ``_init()``, starts with a leading
          dấu gạch dưới. Theo quy ước, các hàm ảo của Godot, tức là những hàm tích hợp mà bạn có thể ghi đè để giao tiếp với engine, bắt đầu bằng dấu gạch dưới.

Dòng bên trong hàm, ``rotation += angular_speed * delta``, tăng góc xoay của sprite trong mỗi khung hình. Ở đây, ``rotation`` là một thuộc tính được kế thừa từ lớp ``Node2D``, lớp mà ``Sprite2D`` mở rộng. Thuộc tính này điều khiển góc xoay của nút và sử dụng radian.

.. tip:: In the code editor, you can :kbd:`Ctrl + Click` (:kbd:`Cmd + Click` on
         macOS) trên bất kỳ thuộc tính hoặc hàm tích hợp nào như ``position``, ``rotation`` hoặc ``_process`` để mở tài liệu tương ứng trong một tab mới.

Chạy cảnh để xem biểu tượng Godot xoay tại chỗ.

.. image:: img/scripting_first_script_godot_turning_in_place.gif

.. note:: In C#, notice how the ``delta`` argument taken by ``_Process()`` is a
          ``double``. Vì vậy, chúng ta cần chuyển đổi nó thành ``float`` khi áp dụng vào góc xoay.

Di chuyển về phía trước
~~~~~~~~~~~~~~~~~~~~~~~

Bây giờ hãy làm cho nút di chuyển. Thêm hai dòng sau vào bên trong hàm ``_process()``, đảm bảo các dòng mới được thụt lề giống với dòng ``rotation += angular_speed * delta`` đứng trước chúng.

.. tabs::
 .. code-tab:: gdscript GDScript

    var velocity = Vector2.UP.rotated(rotation) * speed

    position += velocity * delta

 .. code-tab:: csharp C#

    var velocity = Vector2.Up.Rotated(Rotation) * _speed;

    Position += velocity * (float)delta;

Như chúng ta đã thấy, từ khóa ``var`` định nghĩa một biến mới. Nếu đặt từ khóa này ở đầu script, nó định nghĩa một thuộc tính của lớp. Bên trong một hàm, nó định nghĩa một biến cục bộ: biến này chỉ tồn tại trong phạm vi của hàm.

Chúng ta định nghĩa một biến cục bộ có tên ``velocity``, một vector 2D biểu diễn cả hướng và tốc độ. Để làm cho nút di chuyển về phía trước, chúng ta bắt đầu từ hằng số ``Vector2.UP`` của lớp Vector2, một vector hướng lên trên, rồi xoay nó bằng cách gọi phương thức ``rotated()`` của Vector2. Biểu thức ``Vector2.UP.rotated(rotation)`` này là một vector hướng về phía trước tương đối so với biểu tượng của chúng ta. Nhân với thuộc tính ``speed``, nó cho chúng ta một vận tốc có thể dùng để di chuyển nút về phía trước.

Chúng ta cộng ``velocity * delta`` vào ``position`` của nút để di chuyển nó. Bản thân vị trí có kiểu :ref:`Vector2 <class_Vector2>`, một kiểu tích hợp trong Godot biểu diễn một vector 2D.

Chạy cảnh để xem đầu biểu tượng Godot chạy theo vòng tròn.

.. image:: img/scripting_first_script_rotating_godot.gif

.. note:: Moving a node like that does not take into account colliding with
          tường hoặc sàn nhà. Trong :ref:`doc_your_first_2d_game`, bạn sẽ tìm hiểu một cách tiếp cận khác để di chuyển các đối tượng đồng thời phát hiện va chạm.

Hiện tại, node của chúng ta tự di chuyển. Trong phần tiếp theo,
:ref:`doc_scripting_player_input`, we'll use player input to control it.

Toàn bộ tập lệnh
----------------

Dưới đây là tệp ``sprite_2d.gd`` hoàn chỉnh để bạn tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400 var angular_speed = PI


    func _process(delta): rotation += angular_speed * delta

        var velocity = Vector2.UP.rotated(rotation) * speed

        position += velocity * delta

 .. code-tab:: csharp C#

    using Godot; using System;

    public partial class MySprite2D : Sprite2D { private int _speed = 400; private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta) { Rotation += _angularSpeed * (float)delta; var velocity = Vector2.Up.Rotated(Rotation) * _speed;

            Position += velocity * (float)delta; } }
