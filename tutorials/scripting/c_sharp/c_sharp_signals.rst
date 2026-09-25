.. _doc_c_sharp_signals:

Tín hiệu C#
===========

Để xem giải thích chi tiết về tín hiệu nói chung, hãy xem phần :ref:`doc_signals` trong hướng dẫn từng bước.

Tín hiệu được triển khai bằng các sự kiện C#, cách biểu diễn theo thông lệ
:ref:`mẫu observer <doc_key_concepts_signals>` trong C#. Đây là cách được khuyến nghị để sử dụng tín hiệu trong C# và là trọng tâm của trang này.

Trong một số trường hợp, cần sử dụng
:ref:`Connect()<class_object_method_connect>` và
:ref:`Disconnect()<class_object_method_disconnect>` API cũ. Xem :ref:`using_connect_and_disconnect` để biết thêm chi tiết.

Nếu gặp ``System.ObjectDisposedException`` khi xử lý một tín hiệu, có thể bạn đã bỏ sót việc ngắt kết nối tín hiệu. Xem
:ref:`disconnecting_automatically_when_the_receiver_is_freed` để biết thêm chi tiết.

Tín hiệu dưới dạng sự kiện C#
-----------------------------

Để tăng độ an toàn kiểu, tất cả tín hiệu Godot cũng có sẵn thông qua các sự kiện `events <https://learn.microsoft.com/en-us/dotnet/csharp/events-overview>`_. Bạn có thể xử lý các sự kiện này như mọi sự kiện khác, bằng các toán tử ``+=`` và ``-=``.

.. code-block:: csharp

    Timer myTimer = GetNode<Timer>("Timer");
    myTimer.Timeout += () => GD.Print("Timeout!");

Ngoài ra, bạn luôn có thể truy cập tên tín hiệu được liên kết với một kiểu node thông qua lớp ``SignalName`` lồng bên trong kiểu đó. Điều này hữu ích khi bạn muốn await một tín hiệu, chẳng hạn (xem :ref:`doc_c_sharp_differences_await`).

.. code-block:: csharp

    await ToSignal(GetTree(), SceneTree.SignalName.ProcessFrame);

Tín hiệu tùy chỉnh dưới dạng sự kiện C#
---------------------------------------

Để khai báo một sự kiện tùy chỉnh trong script C#, hãy sử dụng thuộc tính ``[Signal]`` trên một kiểu delegate public. Lưu ý rằng tên của delegate này phải kết thúc bằng ``EventHandler``.

.. code-block:: csharp

    [Signal]
    public delegate void MySignalEventHandler();

    [Signal]
    public delegate void MySignalWithArgumentEventHandler(string myString);

Sau khi hoàn tất, Godot sẽ tự động tạo các sự kiện thích hợp ở phía sau. Sau đó, bạn có thể sử dụng các sự kiện đó như với bất kỳ tín hiệu Godot nào khác. Lưu ý rằng tên sự kiện được tạo từ tên delegate của bạn sau khi bỏ phần ``EventHandler`` cuối cùng.

.. code-block:: csharp

    public override void _Ready()
    {
        MySignal += () => GD.Print("Hello!");
        MySignalWithArgument += SayHelloTo;
    }

    private void SayHelloTo(string name)
    {
        GD.Print($"Hello {name}!");
    }

.. warning::

    Nếu muốn kết nối với các tín hiệu này trong editor, bạn cần build lại dự án để chúng xuất hiện.

    Bạn có thể nhấp vào nút **Build** ở góc trên bên phải của editor để thực hiện việc đó.

Phát tín hiệu
-------------

Để phát tín hiệu, hãy sử dụng phương thức ``EmitSignal``. Lưu ý rằng, cũng như các tín hiệu do engine định nghĩa, tên tín hiệu tùy chỉnh của bạn được liệt kê trong lớp ``SignalName`` lồng bên trong.

.. code-block:: csharp

    public void MyMethodEmittingSignals()
    {
        EmitSignal(SignalName.MySignal);
        EmitSignal(SignalName.MySignalWithArgument, "World");
    }

Khác với các sự kiện C# khác, bạn không thể sử dụng ``Invoke`` để phát các sự kiện gắn với tín hiệu Godot.

Tín hiệu hỗ trợ đối số thuộc bất kỳ :ref:`kiểu tương thích với Variant <c_sharp_variant_compatible_types>` nào.

Do đó, mọi ``Node`` hoặc ``RefCounted`` đều tự động tương thích, nhưng các đối tượng dữ liệu tùy chỉnh phải kế thừa từ ``GodotObject`` hoặc một trong các lớp con của nó.

.. code-block:: csharp

    using Godot;

    public partial class DataObject : GodotObject
    {
        public string MyFirstString { get; set; }
        public string MySecondString { get; set; }
    }

Giá trị liên kết
----------------

Đôi khi bạn sẽ muốn liên kết các giá trị với một tín hiệu ngay khi thiết lập kết nối, thay vì (hoặc ngoài việc) liên kết khi tín hiệu được phát. Để làm vậy, bạn có thể sử dụng một hàm ẩn danh như trong ví dụ sau.

Ở đây, tín hiệu :ref:`Button.Pressed <class_BaseButton_signal_pressed>` không nhận đối số nào. Nhưng chúng ta muốn sử dụng cùng một ``ModifyValue`` cho cả nút "plus" và "minus". Vì vậy, chúng ta liên kết giá trị modifier tại thời điểm kết nối các tín hiệu.

.. code-block:: csharp

    public int Value { get; private set; } = 1;

    public override void _Ready()
    {
        Button plusButton = GetNode<Button>("PlusButton");
        plusButton.Pressed += () => ModifyValue(1);

        Button minusButton = GetNode<Button>("MinusButton");
        minusButton.Pressed += () => ModifyValue(-1);
    }

    private void ModifyValue(int modifier)
    {
        Value += modifier;
    }

Tạo tín hiệu trong runtime
--------------------------

Cuối cùng, bạn có thể tạo các tín hiệu tùy chỉnh trực tiếp trong khi game đang chạy. Hãy sử dụng phương thức ``AddUserSignal`` cho việc đó. Lưu ý rằng phương thức này phải được thực thi trước khi sử dụng các tín hiệu đó (dù là kết nối với chúng hay phát chúng). Ngoài ra, các tín hiệu được tạo theo cách này sẽ không hiển thị thông qua lớp ``SignalName`` lồng bên trong.

.. code-block:: csharp

    public override void _Ready()
    {
        AddUserSignal("MyCustomSignal");
        EmitSignal("MyCustomSignal");
    }

.. _using_connect_and_disconnect:

Sử dụng Connect và Disconnect
-----------------------------

Nhìn chung, không nên sử dụng
:ref:`Connect()<class_object_method_connect>` và
:ref:`Disconnect()<class_object_method_disconnect>`. Các API này không cung cấp độ an toàn kiểu cao bằng các sự kiện. Tuy nhiên, chúng cần thiết để
:ref:`kết nối với các tín hiệu được định nghĩa bằng GDScript <connecting_to_signals_cross_language>` và truyền :ref:`ConnectFlags <enum_Object_ConnectFlags>`.

Trong ví dụ sau, lần đầu nhấn nút sẽ in ``Greetings!``. ``OneShot`` ngắt kết nối tín hiệu, vì vậy nhấn nút lần nữa sẽ không làm gì.

.. code-block:: csharp

    public override void _Ready()
    {
        Button button = GetNode<Button>("GreetButton");
        button.Connect(Button.SignalName.Pressed, Callable.From(OnButtonPressed), (uint)GodotObject.ConnectFlags.OneShot);
    }

    public void OnButtonPressed()
    {
        GD.Print("Greetings!");
    }

.. _disconnecting_automatically_when_the_receiver_is_freed:

Tự động ngắt kết nối khi receiver được giải phóng
-------------------------------------------------

Thông thường, khi bất kỳ ``GodotObject`` nào được giải phóng (chẳng hạn như bất kỳ ``Node`` nào), Godot sẽ tự động ngắt mọi kết nối liên kết với đối tượng đó. Điều này áp dụng cho cả signal emitter và signal receiver.

Ví dụ, một node chứa đoạn code này sẽ in "Hello!" khi nút được nhấn, sau đó tự giải phóng. Việc giải phóng node sẽ ngắt kết nối tín hiệu, vì vậy nhấn nút lần nữa sẽ không làm gì:

.. code-block:: csharp

    public override void _Ready()
    {
        Button myButton = GetNode<Button>("../MyButton");
        myButton.Pressed += SayHello;
    }

    private void SayHello()
    {
        GD.Print("Hello!");
        Free();
    }

Khi một signal receiver được giải phóng trong lúc signal emitter vẫn còn tồn tại, trong một số trường hợp việc tự động ngắt kết nối sẽ không xảy ra:

- Tín hiệu được kết nối với một biểu thức lambda capture một biến.
- Tín hiệu là một tín hiệu tùy chỉnh.

Các phần sau giải thích chi tiết hơn về những trường hợp này và đưa ra gợi ý về cách ngắt kết nối thủ công.

.. note::

    Việc tự động ngắt kết nối hoàn toàn đáng tin cậy nếu signal emitter được giải phóng trước khi bất kỳ receiver nào của nó được giải phóng. Với phong cách dự án ưu tiên mẫu này, những giới hạn trên có thể không đáng lo ngại.

Không tự động ngắt kết nối: biểu thức lambda capture một biến
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn kết nối với một biểu thức lambda capture các biến, Godot không thể biết lambda đó được liên kết với instance đã tạo ra nó. Điều này khiến ví dụ sau có hành vi có thể không như mong đợi:

.. code-block:: csharp

    Timer myTimer = GetNode<Timer>("../Timer");
    int x = 0;
    myTimer.Timeout += () =>
    {
        x++; // Biểu thức lambda này capture x.
        GD.Print($"Tick {x} my name is {Name}");
        if (x == 3)
        {
            GD.Print("Time's up!");
            Free();
        }
    };

.. code-block:: text

    Tick 1, my name is ExampleNode
    Tick 2, my name is ExampleNode
    Tick 3, my name is ExampleNode
    Time's up!
    [...] System.ObjectDisposedException: Cannot access a disposed object.

Ở tick 4, biểu thức lambda cố gắng truy cập thuộc tính ``Name`` của node, nhưng node đã được giải phóng. Điều này gây ra exception.

Để ngắt kết nối, hãy giữ một tham chiếu đến delegate được tạo bởi biểu thức lambda và truyền tham chiếu đó vào ``-=``. Ví dụ, node này kết nối và ngắt kết nối bằng các phương thức vòng đời ``_EnterTree`` và ``_ExitTree``:

.. code-block:: csharp

    [Export]
    public Timer MyTimer { get; set; }

    private Action _tick;

    public override void _EnterTree()
    {
        int x = 0;
        _tick = () =>
        {
            x++;
            GD.Print($"Tick {x} my name is {Name}");
            if (x == 3)
            {
                GD.Print("Time's up!");
                Free();
            }
        };
        MyTimer.Timeout += _tick;
    }

    public override void _ExitTree()
    {
        MyTimer.Timeout -= _tick;
    }

Trong ví dụ này, ``Free`` khiến node rời khỏi tree, từ đó gọi ``_ExitTree``. ``_ExitTree`` ngắt kết nối tín hiệu, vì vậy ``_tick`` sẽ không bao giờ được gọi lại.

Các phương thức trong vòng đời cần sử dụng phụ thuộc vào chức năng của node. Một lựa chọn khác là kết nối với các signal trong ``_Ready`` và ngắt kết nối trong ``Dispose``.

.. note::

    Godot sử dụng `Delegate.Target <https://learn.microsoft.com/en-us/dotnet/api/system.delegate.target>`_ để xác định delegate được liên kết với instance nào. Khi một biểu thức lambda không capture biến, ``Target`` của delegate được tạo ra là instance đã tạo delegate đó. Khi một biến được capture, ``Target`` thay vào đó trỏ đến một kiểu được tạo ra để lưu biến đã capture. Đây là nguyên nhân làm mất liên kết. Nếu muốn kiểm tra xem một delegate có được tự động dọn dẹp hay không, hãy thử kiểm tra ``Target`` của nó.

    ``Callable.From`` không ảnh hưởng đến ``Delegate.Target``, vì vậy việc kết nối một lambda capture các biến bằng ``Connect`` cũng không hiệu quả hơn ``+=``.

Không tự động ngắt kết nối: custom signal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết nối với một custom signal bằng ``+=`` sẽ không tự động ngắt kết nối khi node nhận được giải phóng.

Để ngắt kết nối, hãy sử dụng ``-=`` vào thời điểm thích hợp. Ví dụ:

.. code-block:: csharp

    [Export]
    public MyClass Target { get; set; }

    public override void _EnterTree()
    {
        Target.MySignal += OnMySignal;
    }

    public override void _ExitTree()
    {
        Target.MySignal -= OnMySignal;
    }

Một giải pháp khác là sử dụng ``Connect``, thao tác này cũng tự động ngắt kết nối với custom signal:

.. code-block:: csharp

    [Export]
    public MyClass Target { get; set; }

    public override void _EnterTree()
    {
        Target.Connect(MyClass.SignalName.MySignal, Callable.From(OnMySignal));
    }

.. _`events`: https://learn.microsoft.com/en-us/dotnet/csharp/events-overview
.. _`Delegate.Target`: https://learn.microsoft.com/en-us/dotnet/api/system.delegate.target
