.. _doc_c_sharp_signals:

C# signals
==========

Để xem phần giải thích chi tiết về signals nói chung, hãy xem phần :ref:`doc_signals` trong tutorial từng bước.

Signals được triển khai bằng các C# event, là cách tự nhiên để biểu diễn
:ref:`the observer pattern<doc_key_concepts_signals>` in C#. This is the
cách được khuyến nghị để sử dụng signals trong C# và là trọng tâm của trang này.

Trong một số trường hợp, cần sử dụng cách cũ hơn
:ref:`Connect()<class_object_method_connect>` and
:ref:`Disconnect()<class_object_method_disconnect>` APIs.
Xem :ref:`using_connect_and_disconnect` để biết thêm chi tiết.

Nếu bạn gặp phải một ``System.ObjectDisposedException`` khi xử lý signal, có thể bạn đã bỏ sót việc ngắt kết nối signal. Hãy xem
:ref:`disconnecting_automatically_when_the_receiver_is_freed` for more details.

Signals dưới dạng C# event
--------------------------

Để tăng độ an toàn kiểu, tất cả Godot signal cũng đều khả dụng thông qua `events <https://learn.microsoft.com/en-us/dotnet/csharp/events-overview>`_. Bạn có thể xử lý các event này như mọi event khác, bằng các toán tử ``+=`` và ``-=``.

.. code-block:: csharp

    Timer myTimer = GetNode<Timer>("Timer");
    myTimer.Timeout += () => GD.Print("Timeout!");

Ngoài ra, bạn luôn có thể truy cập tên signal gắn với một loại node thông qua class ``SignalName`` lồng nhau của nó. Điều này hữu ích khi, chẳng hạn, bạn muốn await một signal (xem :ref:`doc_c_sharp_differences_await`).

.. code-block:: csharp

    await ToSignal(GetTree(), SceneTree.SignalName.ProcessFrame);

Custom signal dưới dạng C# event
--------------------------------

Để khai báo một custom event trong C# script, hãy sử dụng attribute ``[Signal]`` trên một kiểu delegate public. Lưu ý rằng tên của delegate này cần kết thúc bằng ``EventHandler``.

.. code-block:: csharp

    [Signal]
    public delegate void MySignalEventHandler();

    [Signal]
    public delegate void MySignalWithArgumentEventHandler(string myString);

Sau khi hoàn tất, Godot sẽ tự động tạo các event tương ứng ở phía sau. Sau đó, bạn có thể sử dụng các event này như với bất kỳ Godot signal nào khác. Lưu ý rằng event được đặt tên bằng tên delegate của bạn, bỏ đi phần ``EventHandler`` cuối cùng.

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

    Nếu muốn kết nối với các signal này trong editor, bạn cần build lại project để chúng xuất hiện.

    Bạn có thể nhấp vào nút **Build** ở góc trên bên phải của editor để thực hiện việc đó.

Phát signal
-----------

Để phát signal, hãy sử dụng method ``EmitSignal``. Lưu ý rằng, cũng như các signal do engine định nghĩa, tên custom signal của bạn được liệt kê trong class ``SignalName`` lồng nhau.

.. code-block:: csharp

    public void MyMethodEmittingSignals()
    {
        EmitSignal(SignalName.MySignal);
        EmitSignal(SignalName.MySignalWithArgument, "World");
    }

Khác với các C# event khác, bạn không thể sử dụng ``Invoke`` để phát các event gắn với Godot signal.

Signal hỗ trợ các đối số thuộc mọi :ref:`Variant-compatible type <c_sharp_variant_compatible_types>`.

Do đó, mọi ``Node`` hoặc ``RefCounted`` sẽ tự động tương thích, nhưng các custom data object cần kế thừa từ ``GodotObject`` hoặc một trong các subclass của nó.

.. code-block:: csharp

    using Godot;

    public partial class DataObject : GodotObject
    {
        public string MyFirstString { get; set; }
        public string MySecondString { get; set; }
    }

Các giá trị được bind
---------------------

Đôi khi, bạn sẽ muốn bind các giá trị vào signal khi thiết lập kết nối, thay vì (hoặc בנוסף vào) khi signal được phát. Để làm vậy, bạn có thể sử dụng anonymous function như trong ví dụ sau.

Ở đây, signal :ref:`Button.Pressed <class_BaseButton_signal_pressed>` không nhận bất kỳ đối số nào. Nhưng chúng ta muốn sử dụng cùng một ``ModifyValue`` cho cả nút "plus" và "minus". Vì vậy, chúng ta bind giá trị modifier tại thời điểm kết nối các signal.

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

Tạo signal trong runtime
------------------------

Cuối cùng, bạn có thể tạo custom signal trực tiếp trong khi game đang chạy. Hãy sử dụng method ``AddUserSignal`` cho việc đó. Lưu ý rằng method này phải được thực thi trước khi sử dụng các signal đó (dù là kết nối với chúng hay phát chúng). Ngoài ra, các signal được tạo theo cách này sẽ không hiển thị thông qua class ``SignalName`` lồng nhau.

.. code-block:: csharp

    public override void _Ready()
    {
        AddUserSignal("MyCustomSignal");
        EmitSignal("MyCustomSignal");
    }

.. _using_connect_and_disconnect:

Sử dụng Connect và Disconnect
-----------------------------

Nói chung, không nên sử dụng
:ref:`Connect()<class_object_method_connect>` and
:ref:`Disconnect()<class_object_method_disconnect>`. These APIs don't provide as
nhiều type safety như event. Tuy nhiên, chúng cần thiết cho
:ref:`connecting to signals defined by GDScript <connecting_to_signals_cross_language>`
và truyền :ref:`ConnectFlags<enum_Object_ConnectFlags>`.

Trong ví dụ sau, lần đầu nhấn nút sẽ in ``Greetings!``. ``OneShot`` ngắt kết nối signal, vì vậy nhấn nút lần nữa sẽ không làm gì cả.

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

Thông thường, khi bất kỳ ``GodotObject`` nào được giải phóng (chẳng hạn như bất kỳ ``Node`` nào), Godot sẽ tự động ngắt tất cả kết nối gắn với object đó. Điều này áp dụng cho cả signal emitter và signal receiver.

Ví dụ, một node có đoạn code này sẽ in "Hello!" khi nhấn nút, sau đó tự giải phóng. Việc giải phóng node sẽ ngắt kết nối signal, vì vậy nhấn nút lần nữa sẽ không làm gì cả:

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

Khi một signal receiver được giải phóng trong lúc signal emitter vẫn còn tồn tại, việc ngắt kết nối tự động sẽ không xảy ra trong một số trường hợp:

- Signal được kết nối với một lambda expression capture một variable. - Signal là một custom signal.

Các phần sau giải thích chi tiết hơn về những trường hợp này và đưa ra các gợi ý về cách ngắt kết nối thủ công.

.. note::

    Việc ngắt kết nối tự động hoàn toàn đáng tin cậy nếu signal emitter được giải phóng trước khi bất kỳ receiver nào của nó được giải phóng. Với một project style ưu tiên pattern này, các giới hạn trên có thể không đáng lo ngại.

Không tự động ngắt kết nối: lambda expression capture một variable
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn kết nối với một lambda expression capture các variable, Godot không thể biết lambda đó gắn với instance đã tạo ra nó. Điều này khiến ví dụ sau có hành vi có thể không như mong đợi:

.. code-block:: csharp

    Timer myTimer = GetNode<Timer>("../Timer");
    int x = 0;
    myTimer.Timeout += () =>
    {
        x++; // Lambda expression này capture x.
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

Ở tick 4, lambda expression cố truy cập property ``Name`` của node, nhưng node đã được giải phóng. Điều này gây ra exception.

Để ngắt kết nối, hãy giữ một reference đến delegate được tạo bởi lambda expression và truyền reference đó vào ``-=``. Ví dụ, node này kết nối và ngắt kết nối bằng các lifecycle method ``_EnterTree`` và ``_ExitTree``:

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

Trong ví dụ này, ``Free`` khiến node rời khỏi tree, việc này gọi ``_ExitTree``. ``_ExitTree`` ngắt kết nối signal, vì vậy ``_tick`` sẽ không bao giờ được gọi lại.

Các lifecycle method cần sử dụng phụ thuộc vào việc node thực hiện gì. Một lựa chọn khác là kết nối với signal trong ``_Ready`` và ngắt kết nối trong ``Dispose``.

.. note::

    Godot sử dụng `Delegate.Target <https://learn.microsoft.com/en-us/dotnet/api/system.delegate.target>`_ để xác định delegate được gắn với instance nào. Khi lambda expression không capture variable, ``Target`` của delegate được tạo là instance đã tạo delegate đó. Khi một variable được capture, ``Target`` lại trỏ đến một type được tạo để lưu variable đã capture. Đây là nguyên nhân phá vỡ mối liên kết. Nếu muốn kiểm tra xem một delegate có được tự động dọn dẹp hay không, hãy thử kiểm tra ``Target`` của nó.

    ``Callable.From`` không ảnh hưởng đến ``Delegate.Target``, vì vậy việc kết nối một lambda capture các variable bằng ``Connect`` cũng không hiệu quả hơn ``+=``.

Không tự động ngắt kết nối: custom signal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết nối với custom signal bằng ``+=`` sẽ không tự động ngắt kết nối khi receiving node được giải phóng.

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

Một giải pháp khác là sử dụng ``Connect``, vốn sẽ tự động ngắt kết nối với custom signal:

.. code-block:: csharp

    [Export]
    public MyClass Target { get; set; }

    public override void _EnterTree()
    {
        Target.Connect(MyClass.SignalName.MySignal, Callable.From(OnMySignal));
    }
