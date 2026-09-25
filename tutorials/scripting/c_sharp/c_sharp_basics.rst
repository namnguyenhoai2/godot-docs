Kiến thức cơ bản về C#
======================

Giới thiệu
----------

Trang này cung cấp phần giới thiệu ngắn gọn về C#, bao gồm C# là gì và cách sử dụng C# trong Godot. Sau đó, bạn có thể muốn xem
:ref:`cách sử dụng các tính năng cụ thể <doc_c_sharp_features>`, đọc về
:ref:`sự khác biệt giữa API C# và GDScript <doc_c_sharp_differences>`, và xem lại :ref:`phần Scripting <doc_scripting>` của tutorial từng bước.

C# là một ngôn ngữ lập trình bậc cao do Microsoft phát triển. Trong Godot, ngôn ngữ này được triển khai bằng runtime .NET hiện đại.

.. attention::

    Các project viết bằng C# sử dụng Godot 4 hiện chưa thể được export lên nền tảng web. Để sử dụng C# trên nền tảng web, hãy cân nhắc dùng Godot 3. Nền tảng Android và iOS được hỗ trợ kể từ Godot 4.2, nhưng vẫn đang ở trạng thái thử nghiệm và :ref:`có một số hạn chế <doc_c_sharp_platforms>`.

.. note::

    Đây **không** phải là tutorial chuyên sâu về toàn bộ ngôn ngữ C#. Nếu bạn chưa quen với cú pháp hoặc các tính năng của ngôn ngữ này, hãy xem `hướng dẫn C# của Microsoft <https://docs.microsoft.com/en-us/dotnet/csharp/index>`_ hoặc tìm một tài liệu giới thiệu phù hợp ở nơi khác.

.. _doc_c_sharp_setup:

Điều kiện tiên quyết
--------------------

Godot tích hợp các thành phần .NET cần thiết để chạy các game đã được biên dịch. Tuy nhiên, Godot không tích hợp các công cụ cần thiết để build và compile game, chẳng hạn như MSBuild và trình biên dịch C#. Các công cụ này được cung cấp trong .NET SDK và cần được cài đặt riêng.

Tóm lại, bạn phải cài đặt .NET SDK **và** phiên bản Godot có hỗ trợ .NET.

Hãy tải xuống và cài đặt phiên bản ổn định mới nhất của SDK từ `trang tải xuống .NET <https://dotnet.microsoft.com/download>`__. Godot 4.5 yêu cầu .NET 8 trở lên, nhưng việc export sang Android yêu cầu .NET 9 trở lên.

.. important::

    Hãy đảm bảo cài đặt phiên bản SDK 64-bit nếu bạn đang sử dụng phiên bản Godot 64-bit.

Nếu bạn build Godot từ source, hãy đảm bảo làm theo các bước để bật hỗ trợ .NET trong bản build như được nêu trên :ref:`doc_compiling_with_dotnet` trang.

.. _doc_c_sharp_setup_external_editor:

Cấu hình external editor
------------------------

Hỗ trợ C# trong script editor tích hợp của Godot còn hạn chế. Hãy cân nhắc sử dụng IDE hoặc editor bên ngoài, chẳng hạn như  `Visual Studio Code <https://code.visualstudio.com/>`__ hoặc `Visual Studio <https://visualstudio.microsoft.com/>`__. Các công cụ này cung cấp tính năng tự động hoàn thành, debugging và các tính năng hữu ích khác cho C#. Để chọn một editor bên ngoài trong Godot, hãy nhấp vào **Editor → Editor Settings** rồi cuộn xuống **Dotnet**. Trong **Dotnet**, hãy nhấp vào **Editor** và chọn editor bên ngoài bạn muốn sử dụng. Hiện tại Godot hỗ trợ các editor bên ngoài sau:

- Visual Studio 2022
- Visual Studio Code
- MonoDevelop
- Visual Studio for Mac
- JetBrains Rider

Xem các phần sau để biết cách cấu hình editor bên ngoài:

JetBrains Rider
~~~~~~~~~~~~~~~

Sau khi đọc phần "Điều kiện tiên quyết", bạn có thể tải xuống và cài đặt `JetBrains Rider <https://www.jetbrains.com/rider/download>`__.

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **JetBrains Rider**.

Trong Rider:

- Đặt **MSBuild version** thành **.NET Core**.
- Nếu bạn đang sử dụng phiên bản Rider thấp hơn 2024.2, hãy cài đặt plugin **Godot support**. Tính năng này hiện đã được tích hợp sẵn trong Rider.

Visual Studio Code
~~~~~~~~~~~~~~~~~~

Sau khi đọc phần "Điều kiện tiên quyết", bạn có thể tải xuống và cài đặt `Visual Studio Code <https://code.visualstudio.com/download>`__ (còn gọi là VS Code).

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **Visual Studio Code**.

Trong Visual Studio Code:

- Cài đặt extension `C# <https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp>`__.

Để cấu hình project cho việc debugging, bạn cần có file ``tasks.json`` và ``launch.json`` trong thư mục ``.vscode`` với cấu hình cần thiết.

Sau đây là một ví dụ về ``launch.json``:

.. code-block:: json

    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Play",
                "type": "coreclr",
                "request": "launch",
                "preLaunchTask": "build",
                "program": "${env:GODOT4}",
                "args": [],
                "cwd": "${workspaceFolder}",
                "stopAtEntry": false,
            }
        ]
    }

Để cấu hình launch này hoạt động, bạn cần thiết lập biến môi trường GODOT4 trỏ đến file thực thi Godot hoặc thay ``program`` parameter bằng đường dẫn đến file thực thi Godot.

Sau đây là một ví dụ về ``tasks.json``:

.. code-block:: json

    {
        "version": "2.0.0",
        "tasks": [
            {
                "label": "build",
                "command": "dotnet",
                "type": "process",
                "args": [
                    "build"
                ],
                "problemMatcher": "$msCompile"
            }
        ]
    }

Bây giờ, khi khởi động debugger trong Visual Studio Code, project Godot của bạn sẽ chạy.

Visual Studio (chỉ dành cho Windows)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hãy tải xuống và cài đặt phiên bản mới nhất của `Visual Studio <https://visualstudio.microsoft.com/downloads/>`__. Visual Studio sẽ bao gồm các SDK cần thiết nếu bạn chọn đúng workloads, vì vậy bạn không cần tự cài đặt các thành phần được liệt kê trong phần "Điều kiện tiên quyết".

Trong quá trình cài đặt Visual Studio, hãy chọn workload này:

- Phát triển ứng dụng desktop .NET

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **Visual Studio**.

.. note:: Nếu bạn gặp lỗi như "Unable to find package Godot.NET.Sdk", cấu hình NuGet của bạn có thể không chính xác và cần được sửa.

          Một cách đơn giản để sửa file cấu hình NuGet là tạo lại file này. Trong cửa sổ file explorer, hãy truy cập ``%AppData%\NuGet``. Đổi tên hoặc xóa file ``NuGet.Config``. Khi bạn build lại project Godot, file này sẽ tự động được tạo với các giá trị mặc định.

Để debug các script C# bằng Visual Studio, hãy mở tệp .sln được tạo sau khi mở script C# đầu tiên trong trình soạn thảo. Trong menu **Debug**, hãy đi đến mục **Debug Properties** cho project của bạn. Nhấp vào nút **Create a new profile** và chọn **Executable**. Trong trường **Executable**, hãy duyệt đến đường dẫn của phiên bản C# của Godot editor hoặc nhập ``%GODOT4%`` nếu bạn đã tạo biến môi trường cho đường dẫn đến tệp thực thi Godot. Đường dẫn này phải trỏ đến tệp thực thi Godot chính, không phải phiên bản 'console'. Đối với **Working Directory**, hãy nhập một dấu chấm đơn, ``.``, biểu thị thư mục hiện tại. Đồng thời, hãy chọn hộp kiểm **Enable native code debugging**. Bây giờ bạn có thể đóng cửa sổ này, nhấp vào mũi tên hướng xuống trong danh sách thả xuống của debug profile và chọn launch profile mới của mình. Nhấn nút khởi động màu xanh lá cây, game của bạn sẽ bắt đầu chạy ở chế độ debug.


Tạo script C#
-------------

Sau khi thiết lập C# cho Godot thành công, bạn sẽ thấy tùy chọn sau khi chọn **Attach Script** trong menu ngữ cảnh của một node trong scene:

.. image:: img/attachcsharpscript.webp

Lưu ý rằng mặc dù một số chi tiết thay đổi, hầu hết các khái niệm vẫn hoạt động tương tự khi sử dụng C# để viết script. Nếu bạn mới làm quen với Godot, lúc này bạn có thể muốn làm theo các hướng dẫn trên :ref:`doc_scripting`. Mặc dù một số trang tài liệu vẫn chưa có ví dụ C#, hầu hết các khái niệm đều có thể chuyển đổi từ GDScript.

Thiết lập project và quy trình làm việc
---------------------------------------

Khi tạo script C# đầu tiên, Godot sẽ khởi tạo các tệp project C# cho project Godot của bạn. Việc này bao gồm tạo một solution C# (``.sln``) và một tệp project (``.csproj``), cùng với một số tệp và thư mục tiện ích (``.godot/mono``). Tất cả các tệp này, ngoại trừ ``.godot/mono``, đều quan trọng và nên được commit vào hệ thống quản lý phiên bản của bạn. Mọi thứ bên trong ``.godot`` đều có thể được thêm an toàn vào danh sách ignore của VCS. Khi khắc phục sự cố, đôi khi việc xóa thư mục ``.godot/mono`` và để Godot tạo lại thư mục này có thể hữu ích.

Ví dụ
-----

Đây là một script C# trống với một số chú thích để minh họa cách hoạt động.

.. code-block:: csharp

    using Godot;

    public partial class YourCustomClass : Node
    {
        // Các biến thành viên, ví dụ:
        private int _a = 2;
        private string _b = "textvar";

        public override void _Ready()
        {
            // Được gọi mỗi khi node được thêm vào scene.
            // Phần khởi tạo.
            GD.Print("Hello from C# to Godot :)");
        }

        public override void _Process(double delta)
        {
            // Được gọi ở mỗi frame. Delta là khoảng thời gian kể từ frame trước.
            // Cập nhật logic game tại đây.
        }
    }

Như bạn có thể thấy, các hàm thường nằm trong phạm vi global của GDScript, chẳng hạn hàm ``print``, đều có sẵn trong static class ``GD``, một phần của namespace ``Godot``. Để xem danh sách đầy đủ các phương thức trong class ``GD``, hãy xem các trang tham chiếu class dành cho
:ref:`@GDScript <class_@gdscript>` và :ref:`@GlobalScope <class_@globalscope>`.

.. note::

    Hãy nhớ rằng class bạn muốn gắn vào node phải có cùng tên với tệp ``.cs``. Nếu không, bạn sẽ nhận được lỗi sau:

    *"Cannot find class XXX for script res://XXX.cs"*

.. _doc_c_sharp_general_differences:

Những khác biệt chung giữa C# và GDScript
-----------------------------------------

API C# sử dụng ``PascalCase`` thay vì ``snake_case`` trong GDScript/C++. Khi có thể, các field và getter/setter đã được chuyển đổi thành property. Nhìn chung, Godot API cho C# hướng đến việc có cách sử dụng phù hợp với ngôn ngữ nhất có thể.

Để biết thêm thông tin, hãy xem trang :ref:`doc_c_sharp_differences`.

.. warning::

    Bạn cần build lại các assembly của project mỗi khi muốn thấy các biến đã export hoặc signal mới trong editor. Có thể kích hoạt thủ công quá trình build này bằng cách nhấp vào nút **Build** ở góc trên bên phải của editor.

    .. image:: img/build_dotnet.webp

    Bạn cũng cần build lại các assembly của project để áp dụng các thay đổi trong các script "tool".

Các vấn đề cần lưu ý và sự cố đã biết hiện tại
----------------------------------------------

Vì hỗ trợ C# trong Godot vẫn còn khá mới, vẫn có một số khó khăn ban đầu và những điểm cần được hoàn thiện. Dưới đây là danh sách các vấn đề quan trọng nhất bạn nên biết khi bắt đầu sử dụng C# trong Godot, nhưng nếu không chắc chắn, bạn cũng nên xem qua `issue tracker for .NET issues <https://github.com/godotengine/godot/labels/topic%3Adotnet>`_ chính thức.

- Có thể viết editor plugin, nhưng hiện tại quy trình này khá phức tạp.
- Hiện tại, state không được lưu và khôi phục khi hot-reload, ngoại trừ các biến đã export.
- Các script C# được gắn vào node phải tham chiếu đến một class có tên trùng với tên tệp.
- Có một số phương thức như ``Get()``/``Set()``, ``Call()``/``CallDeferred()`` và phương thức kết nối signal ``Connect()`` phụ thuộc vào quy ước đặt tên API ``snake_case`` của Godot. Vì vậy, khi sử dụng chẳng hạn ``CallDeferred("AddChild")``, ``AddChild`` sẽ không hoạt động vì API đang chờ phiên bản ``snake_case`` gốc là ``add_child``. Tuy nhiên, bạn có thể sử dụng mọi property hoặc phương thức tùy chỉnh mà không bị giới hạn này. Nên sử dụng ``StringName`` được cung cấp trong ``PropertyName``, ``MethodName`` và ``SignalName`` để tránh phải cấp phát ``StringName`` bổ sung và không phải lo lắng về việc đặt tên snake_case.


Kể từ Godot 4.0, việc export các project .NET được hỗ trợ trên các nền tảng desktop (Linux, Windows và macOS). Các nền tảng khác sẽ được hỗ trợ trong những bản phát hành 4.x sau này.

Các lỗi thường gặp
------------------

Bạn có thể gặp lỗi sau khi cố gắng sửa đổi một số giá trị trong các object Godot, chẳng hạn khi cố thay đổi tọa độ X của một ``Node2D``:

.. code-block:: csharp
    :emphasize-lines: 5

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            Position.X = 100.0f;
            // CS1612: Cannot modify the return value of 'Node2D.Position' because
            // it is not a variable.
        }
    }

Điều này hoàn toàn bình thường. Struct (trong ví dụ này là một ``Vector2``) trong C# được sao chép khi gán, nghĩa là khi bạn lấy một object như vậy từ property hoặc indexer, bạn nhận được một bản sao của nó chứ không phải chính object đó. Việc sửa đổi bản sao này mà không gán lại sau đó sẽ không mang lại hiệu quả gì.

Cách khắc phục rất đơn giản: lấy toàn bộ struct, sửa đổi giá trị bạn muốn thay đổi, rồi gán lại property.

.. code-block:: csharp

    var newPosition = Position;
    newPosition.X = 100.0f;
    Position = newPosition;

Kể từ C# 10, bạn cũng có thể sử dụng `with expressions <https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/with-expression>`_ trên các struct, cho phép thực hiện điều tương tự trong một dòng duy nhất.

.. code-block:: csharp

    Position = Position with { X = 100.0f };

Bạn có thể đọc thêm về lỗi này trong `C# language reference <https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/cs1612>`_.

Hiệu năng của C# trong Godot
----------------------------

.. seealso::

    Để xem so sánh hiệu năng giữa các ngôn ngữ được Godot hỗ trợ, hãy xem :ref:`doc_faq_which_programming_language_is_fastest`.

Hầu hết các thuộc tính của đối tượng Godot C# dựa trên ``GodotObject`` (ví dụ: bất kỳ ``Node`` nào như ``Control`` hoặc ``Node3D`` như ``Camera3D``) đều yêu cầu các lệnh gọi native (interop), vì chúng giao tiếp với lõi C++ của Godot. Hãy cân nhắc gán giá trị của các thuộc tính như vậy vào một biến cục bộ nếu bạn cần sửa đổi hoặc đọc chúng nhiều lần tại cùng một vị trí trong mã:

.. code-block:: csharp

    using Godot;

    public partial class YourCustomClass : Node3D
    {
        private void ExpensiveReposition()
        {
            for (var i = 0; i < 10; i++)
            {
                // Position được đọc và thiết lập 10 lần, dẫn đến việc interop native.
                // Ngoài ra, đối tượng được định vị lại 10 lần trong không gian 3D, việc này
                // tốn thêm thời gian.
                Position += new Vector3(i, i);
            }
        }

        private void Reposition()
        {
            // Một biến được sử dụng để tránh interop native cho Position trong mỗi vòng lặp.
            var newPosition = Position;
            for (var i = 0; i < 10; i++)
            {
                newPosition += new Vector3(i, i);
            }
            // Chỉ thiết lập Position một lần sẽ tránh interop native và việc định vị lại trong không gian 3D.
            Position = newPosition;
        }
    }

Việc truyền các mảng thô (chẳng hạn như ``byte[]``) hoặc ``string`` đến API C# của Godot yêu cầu marshalling, vốn tương đối tốn kém.

Việc chuyển đổi ngầm từ ``string`` sang ``NodePath`` hoặc ``StringName`` phát sinh cả chi phí interop native và marshalling, vì ``string`` phải được marshal và truyền đến constructor native tương ứng.

Sử dụng các gói NuGet trong Godot
---------------------------------

Có thể cài đặt và sử dụng các gói `NuGet <https://www.nuget.org/>`_ với Godot như với bất kỳ dự án C# nào. Nhiều IDE có thể trực tiếp thêm các gói. Bạn cũng có thể thêm chúng theo cách thủ công bằng cách thêm tham chiếu gói vào tệp ``.csproj`` nằm trong thư mục gốc của dự án:

.. code-block:: xml
    :emphasize-lines: 2

        <ItemGroup>
            <PackageReference Include="Newtonsoft.Json" Version="11.0.2" />
        </ItemGroup>
        ...
    </Project>

Godot sẽ tự động tải xuống và thiết lập các gói NuGet mới được thêm vào trong lần tiếp theo xây dựng dự án.

Profiling mã C# của bạn
-----------------------

Có thể sử dụng các công cụ sau để profiling hiệu năng và bộ nhớ của mã managed:

- JetBrains Rider với plugin dotTrace/dotMemory.
- JetBrains dotTrace/dotMemory độc lập.
- Visual Studio.

Có thể profiling đồng thời mã managed và unmanaged bằng cả các công cụ JetBrains lẫn Visual Studio, nhưng chỉ giới hạn trên Windows.

.. _`Microsoft C# guide`: https://docs.microsoft.com/en-us/dotnet/csharp/index
.. _`issue tracker for .NET issues`: https://github.com/godotengine/godot/labels/topic%3Adotnet
.. _`with expressions`: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/with-expression
.. _`C# language reference`: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/cs1612
.. _`NuGet`: https://www.nuget.org/
