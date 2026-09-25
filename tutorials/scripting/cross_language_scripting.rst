.. _doc_cross_language_scripting:

Lập trình bằng nhiều ngôn ngữ
=============================

Godot cho phép bạn kết hợp các ngôn ngữ lập trình để phù hợp với nhu cầu của mình. Điều này có nghĩa là một dự án có thể định nghĩa các node bằng cả C# và GDScript. Trang này sẽ trình bày những tương tác có thể xảy ra giữa hai node được viết bằng các ngôn ngữ khác nhau.

Hai script sau sẽ được dùng làm tài liệu tham khảo trong suốt trang này.

.. tabs::

 .. code-tab:: gdscript GDScript

    extends Node

    var my_property: String = "my gdscript value":
        get:
            return my_property
        set(value):
            my_property = value

    signal my_signal
    signal my_signal_with_params(msg: String, n: int)

    func print_node_name(node: Node) -> void:
        print(node.get_name())

    func print_array(arr: Array) -> void:
        for element in arr:
            print(element)

    func print_n_times(msg: String, n: int) -> void:
        for i in range(n):
            print(msg)

    func my_signal_handler():
        print("The signal handler was called!")

    func my_signal_with_params_handler(msg: String, n: int):
        print_n_times(msg, n)

 .. code-tab:: csharp

    using Godot;

    public partial class MyCSharpNode : Node
    {
        public string MyProperty { get; set; } = "my c# value";

        [Signal] public delegate void MySignalEventHandler();
        [Signal] public delegate void MySignalWithParamsEventHandler(string msg, int n);

        public void PrintNodeName(Node node)
        {
            GD.Print(node.Name);
        }

        public void PrintArray(string[] arr)
        {
            foreach (string element in arr)
            {
                GD.Print(element);
            }
        }

        public void PrintNTimes(string msg, int n)
        {
            for (int i = 0; i < n; ++i)
            {
                GD.Print(msg);
            }
        }

        public void MySignalHandler()
        {
            GD.Print("The signal handler was called!");
        }

        public void MySignalWithParamsHandler(string msg, int n)
        {
            PrintNTimes(msg, n);
        }
    }

Khởi tạo node
-------------

Nếu không sử dụng các node trong scene tree, có thể bạn sẽ muốn khởi tạo node trực tiếp từ code.

Khởi tạo node C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sử dụng C# từ GDScript không cần nhiều thao tác. Sau khi được tải (xem :ref:`doc_gdscript_classes_as_resources`), script có thể được khởi tạo bằng :ref:`new() <class_CSharpScript_method_new>`.

.. code-block:: gdscript

    var MyCSharpScript = load("res://Path/To/MyCSharpNode.cs")
    var my_csharp_node = MyCSharpScript.new()

.. warning::

    Khi tạo script ``.cs``, bạn luôn cần nhớ rằng class Godot sẽ sử dụng là class có tên giống với chính file ``.cs``. Nếu class đó không tồn tại trong file, bạn sẽ thấy lỗi sau: ``Invalid call. Nonexistent function `new` in base``.

    Ví dụ, MyCoolNode.cs phải chứa một class có tên MyCoolNode.

    Class C# cần kế thừa một class Godot, chẳng hạn như ``GodotObject``. Nếu không, lỗi tương tự sẽ xảy ra.

    Bạn cũng cần kiểm tra xem file ``.cs`` đã được tham chiếu trong file ``.csproj`` của dự án hay chưa. Nếu không, lỗi tương tự sẽ xảy ra.

Khởi tạo node GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ở phía C#, mọi thứ cũng hoạt động theo cách tương tự. Sau khi được tải, GDScript có thể được khởi tạo bằng :ref:`GDScript.New() <class_GDScript_method_new>`.

.. code-block:: csharp

    var myGDScript = GD.Load<GDScript>("res://path/to/my_gd_script.gd");
    var myGDScriptNode = (GodotObject)myGDScript.New(); // Đây là một GodotObject.

Ở đây chúng ta sử dụng một :ref:`class_Object`, nhưng bạn có thể dùng chuyển đổi kiểu như được giải thích trong :ref:`doc_c_sharp_features_type_conversion_and_casting`.

Truy cập các trường
-------------------

Truy cập các trường C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Truy cập các trường C# từ GDScript rất đơn giản, bạn không cần phải lo lắng gì.

.. code-block:: gdscript

    # Đầu ra: "my c# value".
    print(my_csharp_node.MyProperty)
    my_csharp_node.MyProperty = "MY C# VALUE"
    # Đầu ra: "MY C# VALUE".
    print(my_csharp_node.MyProperty)

Truy cập các trường GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vì C# là ngôn ngữ định kiểu tĩnh, việc truy cập GDScript từ C# phức tạp hơn một chút. Bạn sẽ phải sử dụng :ref:`GodotObject.Get() <class_Object_method_get>` và :ref:`GodotObject.Set() <class_Object_method_set>`. Đối số đầu tiên là tên của trường bạn muốn truy cập.

.. code-block:: csharp

    // Đầu ra: "my gdscript value".
    GD.Print(myGDScriptNode.Get("my_property"));
    myGDScriptNode.Set("my_property", "MY GDSCRIPT VALUE");
    // Đầu ra: "MY GDSCRIPT VALUE".
    GD.Print(myGDScriptNode.Get("my_property"));

Hãy nhớ rằng khi thiết lập giá trị của một trường, bạn chỉ nên sử dụng các kiểu mà phía GDScript biết. Về cơ bản, bạn nên làm việc với các kiểu dựng sẵn như được mô tả trong
:ref:`doc_gdscript_builtin_types` hoặc các class mở rộng :ref:`class_Object`.

Gọi các method
--------------

Gọi các method C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một lần nữa, việc gọi các method C# từ GDScript khá đơn giản. Quá trình marshalling sẽ cố gắng hết sức để ép kiểu các đối số cho phù hợp với chữ ký của hàm. Nếu không thể thực hiện, bạn sẽ thấy lỗi sau: ``Invalid call. Nonexistent function `FunctionName``.

.. code-block:: gdscript

    # Đầu ra: "my_gd_script_node" (hoặc tên của node nơi đoạn code này được đặt).
    my_csharp_node.PrintNodeName(self)
    # Dòng này sẽ thất bại.
    # my_csharp_node.PrintNodeName()

    # Xuất "Hello there!" hai lần, mỗi dòng một lần.
    my_csharp_node.PrintNTimes("Hello there!", 2)

    # Đầu ra: "a", "b", "c" (mỗi dòng một giá trị).
    my_csharp_node.PrintArray(["a", "b", "c"])
    # Đầu ra: "1", "2", "3" (mỗi dòng một giá trị).
    my_csharp_node.PrintArray([1, 2, 3])

Gọi các method GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để gọi các method GDScript từ C#, bạn sẽ cần sử dụng
:ref:`GodotObject.Call() <class_Object_method_call>`. Đối số đầu tiên là tên của method bạn muốn gọi. Các đối số tiếp theo sẽ được truyền cho method đó.

.. code-block:: csharp

    // Đầu ra: "MyCSharpNode" (hoặc tên của node nơi đoạn code này được đặt).
    myGDScriptNode.Call("print_node_name", this);
    // Dòng này sẽ âm thầm thất bại và không báo lỗi.
    // myGDScriptNode.Call("print_node_name");

    // Xuất "Hello there!" hai lần, mỗi dòng một lần.
    myGDScriptNode.Call("print_n_times", "Hello there!", 2);

    string[] arr = ["a", "b", "c"];
    // Đầu ra: "a", "b", "c" (mỗi dòng một giá trị).
    myGDScriptNode.Call("print_array", arr);
    // Đầu ra: "1", "2", "3" (mỗi dòng một giá trị).
    myGDScriptNode.Call("print_array", new int[] { 1, 2, 3 });
    // Lưu ý rằng kiểu của từng phần tử trong mảng không quan trọng
    // miễn là marshaller có thể xử lý kiểu đó.

.. _connecting_to_signals_cross_language:

Kết nối với signal
------------------

Kết nối với signal C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết nối với một signal C# từ GDScript cũng giống như kết nối với một signal được định nghĩa trong GDScript:

.. code-block:: gdscript

    my_csharp_node.MySignal.connect(my_signal_handler)

    my_csharp_node.MySignalWithParams.connect(my_signal_with_params_handler)

Kết nối với signal GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết nối với một signal GDScript từ C# chỉ hoạt động với method ``Connect``, vì không tồn tại các kiểu tĩnh C# cho những signal được định nghĩa bởi GDScript:

.. code-block:: csharp

    myGDScriptNode.Connect("my_signal", Callable.From(MySignalHandler));

    myGDScriptNode.Connect("my_signal_with_params", Callable.From<string, int>(MySignalWithParamsHandler));

Kế thừa
-------

Một file GDScript không thể kế thừa từ một script C#. Tương tự, một script C# không thể kế thừa từ một file GDScript. Do việc triển khai điều này rất phức tạp, giới hạn này khó có khả năng được gỡ bỏ trong tương lai. Xem `this GitHub issue <https://github.com/godotengine/godot/issues/38352>`__ để biết thêm thông tin.
