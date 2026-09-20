.. _doc_cross_language_scripting:

Lập trình script đa ngôn ngữ
============================

Godot cho phép bạn kết hợp và sử dụng các ngôn ngữ scripting tùy theo nhu cầu. Điều này có nghĩa là một project có thể định nghĩa các node bằng cả C# và GDScript. Trang này sẽ trình bày các tương tác có thể có giữa hai node được viết bằng các ngôn ngữ khác nhau.

Hai script sau đây sẽ được dùng làm tham chiếu trong suốt trang này.

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

Nếu bạn không sử dụng các node từ scene tree, có lẽ bạn sẽ muốn khởi tạo node trực tiếp từ code.

Khởi tạo node C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sử dụng C# từ GDScript không cần nhiều thao tác. Sau khi được load (xem :ref:`doc_gdscript_classes_as_resources`), script có thể được khởi tạo bằng :ref:`new() <class_CSharpScript_method_new>`.

.. code-block:: gdscript

    var MyCSharpScript = load("res://Path/To/MyCSharpNode.cs")
    var my_csharp_node = MyCSharpScript.new()

.. warning::

    Khi tạo script ``.cs``, bạn luôn cần ghi nhớ rằng class Godot sẽ sử dụng là class có tên giống với chính file ``.cs``. Nếu class đó không tồn tại trong file, bạn sẽ thấy lỗi sau: ``Invalid call. Nonexistent function `new` in base``.

    Ví dụ, MyCoolNode.cs phải chứa một class có tên MyCoolNode.

    Class C# cần kế thừa một class Godot, chẳng hạn như ``GodotObject``. Nếu không, lỗi tương tự sẽ xảy ra.

    Bạn cũng cần kiểm tra để đảm bảo file ``.cs`` được tham chiếu trong file ``.csproj`` của project. Nếu không, lỗi tương tự sẽ xảy ra.

Khởi tạo node GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Từ phía C#, mọi thứ cũng hoạt động theo cách tương tự. Sau khi được load, GDScript có thể được khởi tạo bằng :ref:`GDScript.New() <class_GDScript_method_new>`.

.. code-block:: csharp

    var myGDScript = GD.Load<GDScript>("res://path/to/my_gd_script.gd");
    var myGDScriptNode = (GodotObject)myGDScript.New(); // Đây là một GodotObject.

Ở đây chúng ta đang sử dụng một :ref:`class_Object`, nhưng bạn có thể sử dụng chuyển đổi kiểu như được giải thích trong :ref:`doc_c_sharp_features_type_conversion_and_casting`.

Truy cập các field
------------------

Truy cập field C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc truy cập field C# từ GDScript rất đơn giản, bạn không cần phải lo lắng gì.

.. code-block:: gdscript

    # Kết quả: "my c# value".
    print(my_csharp_node.MyProperty)
    my_csharp_node.MyProperty = "MY C# VALUE"
    # Kết quả: "MY C# VALUE".
    print(my_csharp_node.MyProperty)

Truy cập field GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vì C# là ngôn ngữ kiểu tĩnh, việc truy cập GDScript từ C# phức tạp hơn một chút. Bạn sẽ phải sử dụng :ref:`GodotObject.Get() <class_Object_method_get>` và :ref:`GodotObject.Set() <class_Object_method_set>`. Đối số đầu tiên là tên của field bạn muốn truy cập.

.. code-block:: csharp

    // Kết quả: "my gdscript value".
    GD.Print(myGDScriptNode.Get("my_property"));
    myGDScriptNode.Set("my_property", "MY GDSCRIPT VALUE");
    // Kết quả: "MY GDSCRIPT VALUE".
    GD.Print(myGDScriptNode.Get("my_property"));

Hãy nhớ rằng khi thiết lập giá trị của một field, bạn chỉ nên sử dụng các kiểu mà phía GDScript biết. Về cơ bản, bạn muốn làm việc với các kiểu dựng sẵn như được mô tả trong
:ref:`doc_gdscript_builtin_types` or classes extending :ref:`class_Object`.

Gọi method
----------

Gọi method C# từ GDScript
~~~~~~~~~~~~~~~~~~~~~~~~~

Again, calling C# methods from GDScript should be straightforward. The marshalling process will do its best to cast the arguments to match function signatures. If that's impossible, you'll see the following error: ``Invalid call. Nonexistent function `FunctionName```.

.. code-block:: gdscript

    # Kết quả: "my_gd_script_node" (hoặc tên của node nơi đoạn code này được đặt).
    my_csharp_node.PrintNodeName(self)
    # Dòng này sẽ thất bại.
    # my_csharp_node.PrintNodeName()

    # Xuất "Hello there!" hai lần, mỗi lần trên một dòng.
    my_csharp_node.PrintNTimes("Hello there!", 2)

    # Kết quả: "a", "b", "c" (mỗi giá trị trên một dòng).
    my_csharp_node.PrintArray(["a", "b", "c"])
    # Kết quả: "1", "2", "3" (mỗi giá trị trên một dòng).
    my_csharp_node.PrintArray([1, 2, 3])

Gọi method GDScript từ C#
~~~~~~~~~~~~~~~~~~~~~~~~~

Để gọi method GDScript từ C#, bạn sẽ cần sử dụng
:ref:`GodotObject.Call() <class_Object_method_call>`. The first argument is the
tên của method bạn muốn gọi. Các đối số sau đây sẽ được truyền vào method đó.

.. code-block:: csharp

    // Kết quả: "MyCSharpNode" (hoặc tên của node nơi đoạn code này được đặt).
    myGDScriptNode.Call("print_node_name", this);
    // Dòng này sẽ âm thầm thất bại và không báo lỗi.
    // myGDScriptNode.Call("print_node_name");

    // Xuất "Hello there!" hai lần, mỗi lần trên một dòng.
    myGDScriptNode.Call("print_n_times", "Hello there!", 2);

    string[] arr = ["a", "b", "c"];
    // Kết quả: "a", "b", "c" (mỗi giá trị trên một dòng).
    myGDScriptNode.Call("print_array", arr);
    // Kết quả: "1", "2", "3" (mỗi giá trị trên một dòng).
    myGDScriptNode.Call("print_array", new int[] { 1, 2, 3 });
    // Note how the type of each array entry does not matter
    // miễn là marshaller có thể xử lý được.

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

Việc kết nối với một signal GDScript từ C# chỉ hoạt động với method ``Connect`` vì không tồn tại kiểu tĩnh C# cho các signal được định nghĩa bởi GDScript:

.. code-block:: csharp

    myGDScriptNode.Connect("my_signal", Callable.From(MySignalHandler));

    myGDScriptNode.Connect("my_signal_with_params", Callable.From<string, int>(MySignalWithParamsHandler));

Kế thừa
-------

Một file GDScript không thể kế thừa từ một script C#. Tương tự, một script C# không thể kế thừa từ một file GDScript. Do việc triển khai điều này quá phức tạp, hạn chế này khó có khả năng được gỡ bỏ trong tương lai. Xem `this GitHub issue <https://github.com/godotengine/godot/issues/38352>`__ để biết thêm thông tin.
