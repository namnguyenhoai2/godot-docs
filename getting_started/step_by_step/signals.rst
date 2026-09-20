.. Mục đích: giúp người dùng có trải nghiệm đầu tiên về signal. Chúng ta nên viết thêm tài liệu trong phần scripting/. .. Lưu ý: các đoạn mã GDScript sử dụng lệnh return trên một dòng thay vì hai dòng vì chúng thực sự rất ngắn.

.. meta::
    :keywords: Signal

.. _doc_signals:

Sử dụng signal
==============

Trong bài học này, chúng ta sẽ tìm hiểu về signal. Đây là các thông báo mà node phát ra khi một điều cụ thể xảy ra với chúng, chẳng hạn như khi một nút được nhấn. Các node khác có thể kết nối với signal đó và gọi một hàm khi sự kiện xảy ra.

Signal là một cơ chế ủy quyền được tích hợp trong Godot, cho phép một đối tượng trong game phản ứng với thay đổi ở đối tượng khác mà không cần chúng tham chiếu lẫn nhau. Sử dụng signal giúp hạn chế `coupling <https://en.wikipedia.org/wiki/Coupling_(computer_programming)>`_ và giữ cho mã của bạn linh hoạt.

Ví dụ, bạn có thể có một thanh máu trên màn hình biểu thị lượng máu của người chơi. Khi người chơi chịu sát thương hoặc sử dụng bình hồi máu, bạn muốn thanh này phản ánh thay đổi đó. Để làm vậy, trong Godot, bạn sẽ sử dụng signal.

Giống như các phương thức (:ref:`class_callable`), signal là một kiểu hạng nhất kể từ Godot 4.0. Điều này có nghĩa là bạn có thể truyền chúng trực tiếp dưới dạng đối số của phương thức mà không cần truyền dưới dạng chuỗi, nhờ đó hỗ trợ tự động hoàn thành tốt hơn và giảm lỗi. Hãy xem tài liệu tham khảo lớp :ref:`class_signal` để biết danh sách những gì bạn có thể thực hiện trực tiếp với kiểu Signal.

.. seealso::

    Như đã đề cập trong phần giới thiệu, signal là phiên bản của mẫu observer trong Godot. Bạn có thể tìm hiểu thêm về mẫu này trong `Game Programming Patterns <https://gameprogrammingpatterns.com/observer.html>`__.

Bây giờ chúng ta sẽ sử dụng một signal để làm cho biểu tượng Godot từ bài học trước (:ref:`doc_scripting_player_input`) di chuyển và dừng lại khi nhấn một nút.

.. note:: For this project, we will be following the Godot naming conventions.

          - **GDScript**: Các lớp (node) sử dụng PascalCase, biến và hàm sử dụng snake_case, còn hằng số sử dụng ALL_CAPS (Xem
            :ref:`doc_gdscript_styleguide`).

          - **C#**: Lớp, biến export và phương thức sử dụng PascalCase, các trường private sử dụng _camelCase, còn biến cục bộ và tham số sử dụng camelCase (Xem :ref:`doc_c_sharp_styleguide`). Hãy cẩn thận nhập chính xác tên phương thức khi kết nối signal.

Thiết lập scene
---------------

Để thêm một nút vào game, chúng ta sẽ tạo một scene mới bao gồm cả :ref:`Button <class_button>` và scene ``sprite_2d.tscn`` mà chúng ta đã tạo trong bài học :ref:`doc_scripting_first_script`.

Tạo một scene mới bằng cách đi tới menu :menu:`Scene > New Scene`.

.. image:: img/signals_01_new_scene.webp

Trong dock Scene, hãy nhấp vào nút :button:`2D Scene`. Thao tác này sẽ thêm một :ref:`Node2D <class_Node2D>` làm node gốc.

.. image:: img/signals_02_2d_scene.webp

Trong dock FileSystem, hãy nhấp và kéo tệp ``sprite_2d.tscn`` mà bạn đã lưu trước đó vào Node2D để khởi tạo nó.

.. image:: img/signals_03_dragging_scene.webp

Chúng ta muốn thêm một node khác làm node cùng cấp với Sprite2D. Để làm vậy, hãy nhấp chuột phải vào Node2D và chọn :button:`Add Child Node`.

.. image:: img/signals_04_add_child_node.webp

Tìm node :ref:`Button <class_button>` và thêm nó.

.. image:: img/signals_05_add_button.webp

Theo mặc định, node này có kích thước nhỏ. Hãy nhấp và kéo nút điều khiển ở góc dưới bên phải của Button trong khung nhìn để thay đổi kích thước.

.. image:: img/signals_06_drag_button.png

Nếu bạn không thấy các nút điều khiển, hãy đảm bảo công cụ chọn đang được bật trên thanh công cụ.

.. image:: img/signals_07_select_tool.webp

Nhấp và kéo trực tiếp vào nút để di chuyển nó lại gần sprite hơn.

Bạn cũng có thể viết nhãn trên Button bằng cách chỉnh sửa thuộc tính :inspector:`Text` trong :ui:`Inspector`. Nhập ``Toggle motion``.

.. image:: img/signals_08_toggle_motion_text.webp

Cây scene và khung nhìn của bạn sẽ trông như sau.

.. image:: img/signals_09_scene_setup.webp

Lưu scene mới tạo của bạn dưới tên ``node_2d.tscn``, nếu bạn chưa làm vậy. Sau đó, bạn có thể chạy scene bằng :kbd:`F6` (:kbd:`Cmd + R` trên macOS). Hiện tại, nút sẽ hiển thị, nhưng sẽ không có gì xảy ra khi bạn nhấn nó.

Kết nối signal trong trình chỉnh sửa
------------------------------------

Ở đây, chúng ta muốn kết nối signal "pressed" của Button với Sprite2D và gọi một hàm mới để bật hoặc tắt chuyển động của nó. Chúng ta cần gắn một script vào node Sprite2D, việc này đã được thực hiện trong bài học trước.

Bạn có thể kết nối signal trong dock :ui:`Signals`. Chọn node Button và ở bên phải trình chỉnh sửa, nhấp vào tab có tên :ui:`Signals` bên cạnh
:ui:`Inspector`.

.. image:: img/signals_10_node_dock.webp

Dock này hiển thị danh sách các signal có sẵn trên node được chọn.

.. image:: img/signals_11_pressed_signals.webp

Nhấp đúp vào signal "pressed" để mở cửa sổ kết nối node.

.. image:: img/signals_12_node_connection.webp

Tại đó, bạn có thể kết nối signal với node Sprite2D. Node này cần một phương thức nhận, tức một hàm mà Godot sẽ gọi khi Button phát signal. Trình chỉnh sửa sẽ tạo sẵn một hàm cho bạn. Theo quy ước, chúng ta đặt tên các phương thức callback này là "_on_node_name_signal_name". Ở đây, tên sẽ là "_on_button_pressed".

.. note::

   Khi kết nối signal thông qua dock Signals của trình chỉnh sửa, bạn có thể sử dụng hai chế độ. Chế độ đơn giản chỉ cho phép bạn kết nối với các node đã được gắn script và tạo một hàm callback mới trên các node đó.

   .. image:: img/signals_advanced_connection_window.webp

   Chế độ xem nâng cao cho phép bạn kết nối với bất kỳ node nào và bất kỳ hàm tích hợp nào, thêm đối số vào callback và thiết lập các tùy chọn. Bạn có thể chuyển đổi chế độ ở góc dưới bên trái của cửa sổ bằng cách nhấp vào nút :button:`Advanced`.

.. note::

    Nếu bạn sử dụng trình chỉnh sửa bên ngoài (chẳng hạn như VS Code), tính năng tự động tạo mã này có thể không hoạt động. Trong trường hợp đó, bạn cần kết nối signal bằng mã như được giải thích trong phần tiếp theo.

Nhấp vào nút :button:`Connect` để hoàn tất kết nối signal và chuyển đến
:ui:`Script` workspace. You should see the new method with a connection icon in the
lề trái.

.. image:: img/signals_13_signals_connection_icon.webp

Nếu bạn nhấp vào biểu tượng, một cửa sổ sẽ bật lên và hiển thị thông tin về kết nối. Tính năng này chỉ khả dụng khi kết nối các node trong trình chỉnh sửa.

.. image:: img/signals_14_signals_connection_info.webp

Hãy thay thế dòng chứa từ khóa ``pass`` bằng mã để bật hoặc tắt chuyển động của node.

Sprite2D của chúng ta di chuyển nhờ mã trong hàm ``_process()``. Godot cung cấp một phương thức để bật hoặc tắt việc xử lý: :ref:`Node.set_process() <class_Node_method_set_process>`. Một phương thức khác của lớp Node, ``is_processing()``, trả về ``true`` nếu việc xử lý khi rảnh đang hoạt động. Chúng ta có thể sử dụng từ khóa ``not`` để đảo ngược giá trị.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_button_pressed(): set_process(not is_processing())

 .. code-tab:: csharp C#

    // We also specified this function name in PascalCase in the editor's connection window. private void OnButtonPressed() { SetProcess(!IsProcessing()); }

Hàm này sẽ bật hoặc tắt việc xử lý và do đó bật hoặc tắt chuyển động của biểu tượng khi nhấn nút.

Trước khi thử chạy game, chúng ta cần đơn giản hóa hàm ``_process()`` để node tự động di chuyển thay vì chờ người dùng nhập. Hãy thay thế hàm này bằng đoạn mã sau, mà chúng ta đã thấy từ hai bài học trước:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta): rotation += angular_speed * delta var velocity = Vector2.UP.rotated(rotation) * speed position += velocity * delta

 .. code-tab:: csharp C#

    public override void _Process(double delta) { Rotation += _angularSpeed * (float)delta; var velocity = Vector2.Up.Rotated(Rotation) * _speed; Position += velocity * (float)delta; }

Mã ``sprite_2d.gd`` hoàn chỉnh của bạn sẽ trông như sau.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400 var angular_speed = PI


    func _process(delta): rotation += angular_speed * delta var velocity = Vector2.UP.rotated(rotation) * speed position += velocity * delta


    func _on_button_pressed(): set_process(not is_processing())

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D { private float _speed = 400; private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta) { Rotation += _angularSpeed * (float)delta; var velocity = Vector2.Up.Rotated(Rotation) * _speed; Position += velocity * (float)delta; }

        // We also specified this function name in PascalCase in the editor's connection window. private void OnButtonPressed() { SetProcess(!IsProcessing()); } }

Chạy scene hiện tại bằng cách nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS), rồi nhấp vào nút để xem sprite bắt đầu và dừng lại.

Kết nối signal bằng mã
----------------------

Bạn có thể kết nối signal bằng mã thay vì sử dụng trình chỉnh sửa. Điều này cần thiết khi bạn tạo node hoặc khởi tạo scene bên trong một script.

Hãy sử dụng một node khác ở đây. Godot có node :ref:`Timer <class_Timer>`, rất hữu ích để triển khai thời gian hồi kỹ năng, nạp lại vũ khí và nhiều chức năng khác.

Quay lại workspace 2D. Bạn có thể nhấp vào dòng chữ "2D" ở đầu cửa sổ hoặc nhấn :kbd:`Ctrl + F1` (:kbd:`Ctrl + Cmd + 1` trên macOS).

Trong dock Scene, nhấp chuột phải vào node Sprite2D và thêm một node con mới. Tìm Timer và thêm node tương ứng. Scene của bạn lúc này sẽ trông như sau.

.. image:: img/signals_15_scene_tree.webp

Khi đã chọn node Timer, hãy đi tới :ui:`Inspector` và bật thuộc tính :inspector:`Autostart`.

.. image:: img/signals_18_timer_autostart.webp

Nhấp vào biểu tượng script bên cạnh Sprite2D để quay lại workspace scripting.

.. image:: img/signals_16_click_script.webp

Chúng ta cần thực hiện hai thao tác để kết nối các node bằng mã:

1. Lấy một tham chiếu đến Timer từ Sprite2D. 2. Gọi phương thức ``connect()`` trên signal "timeout" của Timer.

.. note:: To connect to a signal via code, you need to call the ``connect()``
          phương thức của signal mà bạn muốn lắng nghe. Trong trường hợp này, chúng ta muốn lắng nghe signal "timeout" của Timer.

Chúng ta muốn kết nối signal khi scene được khởi tạo, và có thể thực hiện điều đó bằng hàm tích hợp :ref:`Node._ready() <class_Node_private_method__ready>`, hàm này được engine tự động gọi khi một node đã được khởi tạo hoàn toàn.

Để lấy tham chiếu đến một node tương đối với node hiện tại, chúng ta sử dụng phương thức
:ref:`Node.get_node() <class_Node_method_get_node>`. We can store the reference
trong một biến.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready(): var timer = get_node("Timer")

 .. code-tab:: csharp C#

    public override void _Ready() { var timer = GetNode<Timer>("Timer"); }

Hàm ``get_node()`` xem các nút con của Sprite2D và lấy các nút theo tên của chúng. Ví dụ: nếu bạn đổi tên nút Timer thành "BlinkingTimer" trong trình chỉnh sửa, bạn sẽ phải thay đổi lời gọi thành ``get_node("BlinkingTimer")``.

.. add seealso vào một trang giải thích các tính năng của nút.

Bây giờ chúng ta có thể kết nối Timer với Sprite2D trong hàm ``_ready()``.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready(): var timer = get_node("Timer") timer.timeout.connect(_on_timer_timeout)

 .. code-tab:: csharp C#

    public override void _Ready() { var timer = GetNode<Timer>("Timer"); timer.Timeout += OnTimerTimeout; }

Dòng này có nghĩa như sau: chúng ta kết nối tín hiệu "timeout" của Timer với nút mà tập lệnh được gắn vào. Khi Timer phát ``timeout``, chúng ta muốn gọi hàm ``_on_timer_timeout()``, hàm mà chúng ta cần định nghĩa. Hãy thêm hàm này vào cuối tập lệnh và dùng nó để bật tắt khả năng hiển thị của sprite.

.. note:: By convention, we name these callback methods in GDScript as
          "_on_node_name_signal_name" trong GDScript và "OnNodeNameSignalName" trong C#. Ở đây, tên đó sẽ là "_on_timer_timeout" đối với GDScript và OnTimerTimeout() đối với C#.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_timer_timeout(): visible = not visible

 .. code-tab:: csharp C#

    private void OnTimerTimeout() { Visible = !Visible; }

Thuộc tính ``visible`` là một giá trị boolean điều khiển khả năng hiển thị của nút. Dòng ``visible = not visible`` bật tắt giá trị này. Nếu ``visible`` là ``true``, nó sẽ trở thành ``false``, và ngược lại.

Nếu chạy cảnh Node2D ngay bây giờ, bạn sẽ thấy sprite nhấp nháy bật tắt theo khoảng thời gian một giây.

Tập lệnh hoàn chỉnh
-------------------

Vậy là xong phần minh họa nhỏ về biểu tượng Godot chuyển động và nhấp nháy! Dưới đây là tệp ``sprite_2d.gd`` hoàn chỉnh để bạn tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400 var angular_speed = PI


    func _ready(): var timer = get_node("Timer") timer.timeout.connect(_on_timer_timeout)


    func _process(delta): rotation += angular_speed * delta var velocity = Vector2.UP.rotated(rotation) * speed position += velocity * delta


    func _on_button_pressed(): set_process(not is_processing())


    func _on_timer_timeout(): visible = not visible

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D { private float _speed = 400; private float _angularSpeed = Mathf.Pi;

        public override void _Ready() { var timer = GetNode<Timer>("Timer"); timer.Timeout += OnTimerTimeout; }

        public override void _Process(double delta) { Rotation += _angularSpeed * (float)delta; var velocity = Vector2.Up.Rotated(Rotation) * _speed; Position += velocity * (float)delta; }

        // We also specified this function name in PascalCase in the editor's connection window. private void OnButtonPressed() { SetProcess(!IsProcessing()); }

        private void OnTimerTimeout() { Visible = !Visible; } }

Tín hiệu tùy chỉnh
------------------

.. note:: This section is a reference on how to define and use your own signals,
          và không xây dựng dựa trên dự án được tạo trong các bài học trước.

Bạn có thể định nghĩa các tín hiệu tùy chỉnh trong một tập lệnh. Ví dụ, giả sử bạn muốn hiển thị màn hình kết thúc trò chơi khi lượng máu của người chơi giảm xuống 0. Để làm vậy, bạn có thể định nghĩa một tín hiệu có tên là "died" hoặc "health_depleted" khi lượng máu của họ đạt 0.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    signal health_depleted

    var health = 10

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyNode2D : Node2D { [Signal] public delegate void HealthDepletedEventHandler();

        private int _health = 10; }

.. note:: As signals represent events that just occurred, we generally use an
          động từ chỉ hành động ở thì quá khứ trong tên của chúng.

Các tín hiệu của bạn hoạt động giống như các tín hiệu dựng sẵn: chúng xuất hiện trong tab :ui:`Signals` và bạn có thể kết nối với chúng như với bất kỳ tín hiệu nào khác.

.. image:: img/signals_17_custom_signal.webp

Để phát một tín hiệu trong các tập lệnh, hãy gọi ``emit()`` trên tín hiệu đó.

.. tabs::
 .. code-tab:: gdscript GDScript

    func take_damage(amount): health -= amount if health <= 0: health_depleted.emit()

 .. code-tab:: csharp C#

    public void TakeDamage(int amount) { _health -= amount;

        if (_health <= 0) { EmitSignal(SignalName.HealthDepleted); } }

Một tín hiệu có thể tùy chọn khai báo một hoặc nhiều đối số. Chỉ định tên các đối số trong dấu ngoặc đơn:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    signal health_changed(old_value, new_value)

    var health = 10

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyNode : Node { [Signal] public delegate void HealthChangedEventHandler(int oldValue, int newValue);

        private int _health = 10; }

.. note::

    Các đối số của tín hiệu xuất hiện trong bảng điều khiển Signals của trình chỉnh sửa và Godot có thể dùng chúng để tạo các hàm callback cho bạn. Tuy nhiên, bạn vẫn có thể phát bất kỳ số lượng đối số nào khi phát tín hiệu. Vì vậy, bạn phải tự đảm bảo phát đúng các giá trị.

Để phát các giá trị cùng với tín hiệu, hãy thêm chúng làm các đối số bổ sung vào hàm ``emit()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func take_damage(amount): var old_health = health health -= amount health_changed.emit(old_health, health)

 .. code-tab:: csharp C#

    public void TakeDamage(int amount) { int oldHealth = _health; _health -= amount; EmitSignal(SignalName.HealthChanged, oldHealth, _health); }

Tóm tắt
-------

Mọi nút trong Godot đều phát tín hiệu khi một sự việc cụ thể xảy ra với chúng, chẳng hạn như khi một nút được nhấn. Các nút khác có thể kết nối với từng tín hiệu riêng lẻ và phản hồi những sự kiện được chọn.

Tín hiệu có rất nhiều cách sử dụng. Với chúng, bạn có thể phản hồi khi một nút đi vào hoặc rời khỏi thế giới trò chơi, khi xảy ra va chạm, khi một nhân vật đi vào hoặc rời khỏi một khu vực, khi một thành phần giao diện thay đổi kích thước và nhiều trường hợp khác.

Ví dụ, một :ref:`Area2D <class_Area2D>` đại diện cho một đồng xu sẽ phát tín hiệu ``body_entered`` mỗi khi phần thân vật lý của người chơi đi vào hình dạng va chạm của nó, nhờ đó bạn biết khi nào người chơi đã nhặt được đồng xu.

Trong phần tiếp theo, :ref:`doc_your_first_2d_game`, bạn sẽ tạo một trò chơi 2D hoàn chỉnh và áp dụng mọi điều đã học được cho đến nay vào thực tế.
