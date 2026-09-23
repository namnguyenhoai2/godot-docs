.. Intention: give the user a first taste of signals. We should write more
   documentation in the scripting/ section.
.. Note: GDScript snippets use one line return instead of two because they're
   really short.

.. meta::
    :keywords: Signal

.. _doc_signals:

Sử dụng signal
==============

Trong bài học này, chúng ta sẽ tìm hiểu về signal. Đây là các thông báo mà node phát ra khi một điều cụ thể xảy ra với chúng, chẳng hạn như khi một nút được nhấn. Các node khác có thể kết nối với signal đó và gọi một hàm khi sự kiện xảy ra.

Signal là một cơ chế ủy quyền được tích hợp trong Godot, cho phép một đối tượng game phản ứng với thay đổi ở đối tượng khác mà không cần tham chiếu đến nhau. Việc sử dụng signal giúp hạn chế `coupling <https://en.wikipedia.org/wiki/Coupling_(computer_programming)>`_ và giữ cho code của bạn linh hoạt.

Ví dụ, bạn có thể có một thanh sinh lực trên màn hình biểu thị máu của người chơi. Khi người chơi nhận sát thương hoặc sử dụng bình hồi máu, bạn muốn thanh này phản ánh thay đổi đó. Để thực hiện việc này trong Godot, bạn sẽ sử dụng signal.

Giống như method (:ref:`class_callable`), signal là một kiểu hạng nhất kể từ Godot 4.0. Điều này nghĩa là bạn có thể truyền chúng trực tiếp dưới dạng đối số của method mà không cần truyền dưới dạng chuỗi, nhờ đó có tính năng tự động hoàn thành tốt hơn và ít dễ xảy ra lỗi hơn. Xem tài liệu tham khảo lớp :ref:`class_signal` để biết danh sách những việc bạn có thể làm trực tiếp với kiểu Signal.

.. seealso::

    Như đã đề cập trong phần giới thiệu, signal là phiên bản của Godot về mẫu observer. Bạn có thể tìm hiểu thêm về mẫu này trong `Game Programming Patterns <https://gameprogrammingpatterns.com/observer.html>`__.

Bây giờ chúng ta sẽ sử dụng signal để làm cho biểu tượng Godot từ bài học trước (:ref:`doc_scripting_player_input`) di chuyển và dừng lại khi nhấn một nút.

.. note:: Trong dự án này, chúng ta sẽ tuân theo các quy ước đặt tên của Godot.

          - **GDScript**: Class (node) sử dụng PascalCase, biến và function sử dụng snake_case, còn hằng số sử dụng ALL_CAPS (Xem
            :ref:`doc_gdscript_styleguide`).

          - **C#**: Class, biến export và method sử dụng PascalCase, field private sử dụng _camelCase, biến cục bộ và tham số sử dụng camelCase (Xem :ref:`doc_c_sharp_styleguide`). Hãy cẩn thận nhập chính xác tên method khi kết nối signal.

Thiết lập scene
---------------

Để thêm một nút vào game, chúng ta sẽ tạo một scene mới, bao gồm cả :ref:`Button <class_button>` và scene ``sprite_2d.tscn`` mà chúng ta đã tạo trong bài học :ref:`doc_scripting_first_script`.

Tạo một scene mới bằng cách mở menu :menu:`Scene > New Scene`.

.. image:: img/signals_01_new_scene.webp

Trong dock Scene, nhấp vào nút :button:`2D Scene`. Thao tác này sẽ thêm một :ref:`Node2D <class_Node2D>` làm node gốc.

.. image:: img/signals_02_2d_scene.webp

Trong dock FileSystem, nhấp và kéo file ``sprite_2d.tscn`` mà bạn đã lưu trước đó vào Node2D để instantiate nó.

.. image:: img/signals_03_dragging_scene.webp

Chúng ta muốn thêm một node khác làm node cùng cấp với Sprite2D. Để thực hiện việc này, nhấp chuột phải vào Node2D và chọn :button:`Add Child Node`.

.. image:: img/signals_04_add_child_node.webp

Tìm node :ref:`Button <class_button>` và thêm node đó.

.. image:: img/signals_05_add_button.webp

Theo mặc định, node này có kích thước nhỏ. Nhấp và kéo nút điều khiển ở góc dưới bên phải của Button trong viewport để thay đổi kích thước.

.. image:: img/signals_06_drag_button.png

Nếu không thấy các nút điều khiển, hãy đảm bảo công cụ chọn đang hoạt động trên thanh công cụ.

.. image:: img/signals_07_select_tool.webp

Nhấp và kéo chính nút đó để di chuyển nó lại gần sprite hơn.

Bạn cũng có thể viết nhãn trên Button bằng cách chỉnh sửa thuộc tính :inspector:`Text` trong :ui:`Inspector`. Nhập ``Toggle motion``.

.. image:: img/signals_08_toggle_motion_text.webp

Cây scene và viewport của bạn sẽ trông như thế này.

.. image:: img/signals_09_scene_setup.webp

Lưu scene mới tạo dưới tên ``node_2d.tscn``, nếu bạn chưa làm vậy. Sau đó, bạn có thể chạy scene bằng :kbd:`F6` (:kbd:`Cmd + R` trên macOS). Hiện tại, nút sẽ hiển thị, nhưng sẽ không có gì xảy ra khi bạn nhấn nút.

Kết nối signal trong editor
---------------------------

Ở đây, chúng ta muốn kết nối signal "pressed" của Button với Sprite2D và gọi một function mới để bật hoặc tắt chuyển động của nó. Chúng ta cần gắn một script vào node Sprite2D, việc này đã được thực hiện trong bài học trước.

Bạn có thể kết nối signal trong dock :ui:`Signals`. Chọn node Button, sau đó ở phía bên phải của editor, nhấp vào tab có tên :ui:`Signals` bên cạnh
:ui:`Inspector`.

.. image:: img/signals_10_node_dock.webp

Dock này hiển thị danh sách các signal có sẵn trên node đã chọn.

.. image:: img/signals_11_pressed_signals.webp

Nhấp đúp vào signal "pressed" để mở cửa sổ kết nối node.

.. image:: img/signals_12_node_connection.webp

Tại đó, bạn có thể kết nối signal với node Sprite2D. Node này cần một method nhận, tức là một function mà Godot sẽ gọi khi Button phát signal. Editor sẽ tạo method đó cho bạn. Theo quy ước, chúng ta đặt tên cho các method callback này là "_on_node_name_signal_name". Trong trường hợp này, tên sẽ là "_on_button_pressed".

.. note::

   Khi kết nối signal thông qua dock Signals của editor, bạn có thể sử dụng hai chế độ. Chế độ đơn giản chỉ cho phép bạn kết nối với các node đã được gắn script và tạo một function callback mới trên các node đó.

   .. image:: img/signals_advanced_connection_window.webp

   Chế độ xem nâng cao cho phép bạn kết nối với bất kỳ node và function tích hợp nào, thêm đối số vào callback và thiết lập các tùy chọn. Bạn có thể chuyển đổi chế độ ở góc dưới bên trái của cửa sổ bằng cách nhấp vào nút :button:`Advanced`.

.. note::

    Nếu đang sử dụng editor bên ngoài (chẳng hạn như VS Code), tính năng tự động tạo code này có thể không hoạt động. Trong trường hợp đó, bạn cần kết nối signal thông qua code như được giải thích trong phần tiếp theo.

Nhấp vào nút :button:`Connect` để hoàn tất việc kết nối signal và chuyển đến
workspace :ui:`Script`. Bạn sẽ thấy method mới cùng biểu tượng kết nối ở lề trái.

.. image:: img/signals_13_signals_connection_icon.webp

Nếu nhấp vào biểu tượng đó, một cửa sổ sẽ bật lên và hiển thị thông tin về kết nối. Tính năng này chỉ khả dụng khi kết nối các node trong editor.

.. image:: img/signals_14_signals_connection_info.webp

Hãy thay dòng chứa keyword ``pass`` bằng code để bật hoặc tắt chuyển động của node.

Sprite2D của chúng ta di chuyển nhờ code trong function ``_process()``. Godot cung cấp một method để bật hoặc tắt việc xử lý: :ref:`Node.set_process() <class_Node_method_set_process>`. Một method khác của class Node, ``is_processing()``, trả về ``true`` nếu xử lý idle đang hoạt động. Chúng ta có thể sử dụng keyword ``not`` để đảo ngược giá trị này.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_button_pressed():
        set_process(not is_processing())

 .. code-tab:: csharp C#

    // Chúng ta cũng đã chỉ định tên function này theo PascalCase trong cửa sổ kết nối của editor.
    private void OnButtonPressed()
    {
        SetProcess(!IsProcessing());
    }

Function này sẽ bật hoặc tắt việc xử lý, từ đó bật hoặc tắt chuyển động của biểu tượng khi nhấn nút.

Trước khi thử game, chúng ta cần đơn giản hóa function ``_process()`` để node tự động di chuyển thay vì chờ input của người dùng. Hãy thay function này bằng code sau, mà chúng ta đã thấy từ hai bài học trước:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        rotation += angular_speed * delta
        var velocity = Vector2.UP.rotated(rotation) * speed
        position += velocity * delta

 .. code-tab:: csharp C#

    public override void _Process(double delta)
    {
        Rotation += _angularSpeed * (float)delta;
        var velocity = Vector2.Up.Rotated(Rotation) * _speed;
        Position += velocity * (float)delta;
    }

Code ``sprite_2d.gd`` hoàn chỉnh của bạn sẽ trông như sau.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400
    var angular_speed = PI


    func _process(delta):
        rotation += angular_speed * delta
        var velocity = Vector2.UP.rotated(rotation) * speed
        position += velocity * delta


    func _on_button_pressed():
        set_process(not is_processing())

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D
    {
        private float _speed = 400;
        private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta)
        {
            Rotation += _angularSpeed * (float)delta;
            var velocity = Vector2.Up.Rotated(Rotation) * _speed;
            Position += velocity * (float)delta;
        }

        // Chúng ta cũng đã chỉ định tên function này theo PascalCase trong cửa sổ kết nối của editor.
        private void OnButtonPressed()
        {
            SetProcess(!IsProcessing());
        }
    }

Chạy scene hiện tại bằng cách nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS), rồi nhấp vào nút để thấy sprite bắt đầu và dừng lại.

Kết nối signal thông qua code
-----------------------------

Bạn có thể kết nối các signal bằng code thay vì sử dụng editor. Điều này cần thiết khi bạn tạo node hoặc instantiate scene bên trong một script.

Hãy sử dụng một node khác ở đây. Godot có node :ref:`Timer <class_Timer>` hữu ích để triển khai thời gian cooldown của kỹ năng, nạp lại vũ khí và nhiều mục đích khác.

Quay lại workspace 2D. Bạn có thể nhấp vào dòng chữ "2D" ở đầu cửa sổ hoặc nhấn :kbd:`Ctrl + F1` (:kbd:`Ctrl + Cmd + 1` trên macOS).

Trong Scene dock, nhấp chuột phải vào node Sprite2D và thêm một node con mới. Tìm Timer rồi thêm node tương ứng. Scene của bạn lúc này sẽ trông như sau.

.. image:: img/signals_15_scene_tree.webp

Khi đã chọn node Timer, hãy đi đến :ui:`Inspector` và bật thuộc tính :inspector:`Autostart`.

.. image:: img/signals_18_timer_autostart.webp

Nhấp vào biểu tượng script bên cạnh Sprite2D để quay lại scripting workspace.

.. image:: img/signals_16_click_script.webp

Chúng ta cần thực hiện hai thao tác để kết nối các node bằng code:

1. Lấy tham chiếu đến Timer từ Sprite2D.
2. Gọi phương thức ``connect()`` trên signal "timeout" của Timer.

.. note:: Để kết nối với một signal bằng code, bạn cần gọi phương thức ``connect()`` của signal mà bạn muốn lắng nghe. Trong trường hợp này, chúng ta muốn lắng nghe signal "timeout" của Timer.

Chúng ta muốn kết nối signal khi scene được instantiate, và có thể thực hiện việc đó bằng hàm tích hợp :ref:`Node._ready() <class_Node_private_method__ready>`, được engine tự động gọi khi một node đã được instantiate hoàn tất.

Để lấy tham chiếu đến một node tương đối với node hiện tại, chúng ta sử dụng phương thức
:ref:`Node.get_node() <class_Node_method_get_node>`. Chúng ta có thể lưu tham chiếu đó vào một biến.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        var timer = get_node("Timer")

 .. code-tab:: csharp C#

    public override void _Ready()
    {
        var timer = GetNode<Timer>("Timer");
    }

Hàm ``get_node()`` tìm trong các node con của Sprite2D và lấy node theo tên của chúng. Ví dụ, nếu bạn đổi tên node Timer thành "BlinkingTimer" trong editor, bạn sẽ phải đổi lời gọi thành ``get_node("BlinkingTimer")``.

.. add seealso to a page that explains node features.

Bây giờ chúng ta có thể kết nối Timer với Sprite2D trong hàm ``_ready()``.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        var timer = get_node("Timer")
        timer.timeout.connect(_on_timer_timeout)

 .. code-tab:: csharp C#

    public override void _Ready()
    {
        var timer = GetNode<Timer>("Timer");
        timer.Timeout += OnTimerTimeout;
    }

Dòng này có thể hiểu như sau: chúng ta kết nối signal "timeout" của Timer với node mà script được gắn vào. Khi Timer phát ``timeout``, chúng ta muốn gọi hàm ``_on_timer_timeout()``, và cần định nghĩa hàm này. Hãy thêm hàm đó vào cuối script và dùng nó để bật tắt khả năng hiển thị của sprite.

.. note:: Theo quy ước, chúng ta đặt tên các phương thức callback trong GDScript là "_on_node_name_signal_name" và trong C# là "OnNodeNameSignalName". Ở đây, tên sẽ là "_on_timer_timeout" đối với GDScript và OnTimerTimeout() đối với C#.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_timer_timeout():
        visible = not visible

 .. code-tab:: csharp C#

    private void OnTimerTimeout()
    {
        Visible = !Visible;
    }

Thuộc tính ``visible`` là một boolean điều khiển khả năng hiển thị của node. Dòng ``visible = not visible`` bật tắt giá trị này. Nếu ``visible`` là ``true``, nó sẽ trở thành ``false``, và ngược lại.

Nếu bây giờ bạn chạy scene Node2D, bạn sẽ thấy sprite nhấp nháy bật tắt theo các khoảng thời gian một giây.

Script hoàn chỉnh
-----------------

Vậy là xong phần demo biểu tượng Godot vừa di chuyển vừa nhấp nháy của chúng ta! Dưới đây là file ``sprite_2d.gd`` hoàn chỉnh để bạn tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400
    var angular_speed = PI


    func _ready():
        var timer = get_node("Timer")
        timer.timeout.connect(_on_timer_timeout)


    func _process(delta):
        rotation += angular_speed * delta
        var velocity = Vector2.UP.rotated(rotation) * speed
        position += velocity * delta


    func _on_button_pressed():
        set_process(not is_processing())


    func _on_timer_timeout():
        visible = not visible

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D
    {
        private float _speed = 400;
        private float _angularSpeed = Mathf.Pi;

        public override void _Ready()
        {
            var timer = GetNode<Timer>("Timer");
            timer.Timeout += OnTimerTimeout;
        }

        public override void _Process(double delta)
        {
            Rotation += _angularSpeed * (float)delta;
            var velocity = Vector2.Up.Rotated(Rotation) * _speed;
            Position += velocity * (float)delta;
        }

        // Chúng ta cũng đã chỉ định tên hàm này theo PascalCase trong cửa sổ kết nối của editor.
        private void OnButtonPressed()
        {
            SetProcess(!IsProcessing());
        }

        private void OnTimerTimeout()
        {
            Visible = !Visible;
        }
    }

Signal tùy chỉnh
----------------

.. note:: Phần này là tài liệu tham khảo về cách định nghĩa và sử dụng signal của riêng bạn, không xây dựng dựa trên project được tạo trong các bài học trước.

Bạn có thể định nghĩa signal tùy chỉnh trong script. Ví dụ, giả sử bạn muốn hiển thị màn hình game over khi máu của người chơi giảm xuống 0. Để làm vậy, bạn có thể định nghĩa một signal có tên là "died" hoặc "health_depleted" khi máu của họ đạt 0.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    signal health_depleted

    var health = 10

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        [Signal]
        public delegate void HealthDepletedEventHandler();

        private int _health = 10;
    }

.. note:: Vì signal đại diện cho các sự kiện vừa xảy ra, chúng ta thường sử dụng một động từ chỉ hành động ở thì quá khứ trong tên của chúng.

Các signal của bạn hoạt động giống như signal tích hợp: chúng xuất hiện trong tab :ui:`Signals` và bạn có thể kết nối với chúng như với bất kỳ signal nào khác.

.. image:: img/signals_17_custom_signal.webp

Để phát một signal trong script, hãy gọi ``emit()`` trên signal đó.

.. tabs::
 .. code-tab:: gdscript GDScript

    func take_damage(amount):
        health -= amount
        if health <= 0:
            health_depleted.emit()

 .. code-tab:: csharp C#

    public void TakeDamage(int amount)
    {
        _health -= amount;

        if (_health <= 0)
        {
            EmitSignal(SignalName.HealthDepleted);
        }
    }

Một signal có thể tùy chọn khai báo một hoặc nhiều đối số. Hãy chỉ định tên các đối số trong dấu ngoặc đơn:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    signal health_changed(old_value, new_value)

    var health = 10

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyNode : Node
    {
        [Signal]
        public delegate void HealthChangedEventHandler(int oldValue, int newValue);

        private int _health = 10;
    }

.. note::

    Các đối số của signal xuất hiện trong Signals dock của editor và Godot có thể dùng chúng để tạo các hàm callback cho bạn. Tuy nhiên, bạn vẫn có thể phát bất kỳ số lượng đối số nào khi phát signal. Vì vậy, bạn phải tự đảm bảo phát đúng các giá trị.

Để phát các giá trị cùng với signal, hãy thêm chúng làm các đối số bổ sung vào hàm ``emit()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func take_damage(amount):
        var old_health = health
        health -= amount
        health_changed.emit(old_health, health)

 .. code-tab:: csharp C#

    public void TakeDamage(int amount)
    {
        int oldHealth = _health;
        _health -= amount;
        EmitSignal(SignalName.HealthChanged, oldHealth, _health);
    }

Tóm tắt
-------

Mọi node trong Godot đều phát signal khi có điều gì đó cụ thể xảy ra với chúng, chẳng hạn như khi một nút được nhấn. Các node khác có thể kết nối với từng signal riêng lẻ và phản ứng với những sự kiện được chọn.

Signal có rất nhiều cách sử dụng. Với chúng, bạn có thể phản ứng khi một node đi vào hoặc rời khỏi thế giới game, khi xảy ra va chạm, khi một nhân vật đi vào hoặc rời khỏi một khu vực, khi một phần tử giao diện thay đổi kích thước và nhiều trường hợp khác.

Ví dụ, một :ref:`Area2D <class_Area2D>` đại diện cho một đồng xu sẽ phát signal ``body_entered`` mỗi khi physics body của người chơi đi vào collision shape của nó, nhờ đó bạn biết khi nào người chơi đã nhặt được đồng xu.

Trong phần tiếp theo, :ref:`doc_your_first_2d_game`, bạn sẽ tạo một game 2D hoàn chỉnh và áp dụng mọi điều đã học được cho đến nay vào thực tế.

.. _`coupling`: https://en.wikipedia.org/wiki/Coupling_(computer_programming)
