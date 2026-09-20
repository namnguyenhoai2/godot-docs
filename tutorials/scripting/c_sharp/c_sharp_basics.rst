Kiến thức cơ bản về C#
======================

Giới thiệu
----------

Trang này cung cấp phần giới thiệu ngắn gọn về C#, bao gồm C# là gì và cách sử dụng trong Godot. Sau đó, bạn có thể muốn xem
:ref:`how to use specific features <doc_c_sharp_features>`, read about the
:ref:`differences between the C# and the GDScript API <doc_c_sharp_differences>`,
và xem lại :ref:`Scripting section <doc_scripting>` của hướng dẫn từng bước.

C# là một ngôn ngữ lập trình cấp cao do Microsoft phát triển. Trong Godot, ngôn ngữ này được triển khai bằng runtime .NET hiện đại.

.. attention::

    Các project được viết bằng C# sử dụng Godot 4 hiện chưa thể export sang nền tảng web. Để sử dụng C# trên nền tảng web, hãy cân nhắc dùng Godot 3. Hỗ trợ nền tảng Android và iOS có từ Godot 4.2, nhưng vẫn đang ở trạng thái thử nghiệm và :ref:`some limitations apply <doc_c_sharp_platforms>`.

.. note::

    Đây **không phải** là hướng dẫn đầy đủ về toàn bộ ngôn ngữ C#. Nếu bạn chưa quen với cú pháp hoặc các tính năng của ngôn ngữ này, hãy xem `Microsoft C# guide <https://docs.microsoft.com/en-us/dotnet/csharp/index>`_ hoặc tìm một phần giới thiệu phù hợp ở nơi khác.

.. _doc_c_sharp_setup:

Điều kiện tiên quyết
--------------------

Godot tích hợp các thành phần .NET cần thiết để chạy các game đã được compile. Tuy nhiên, Godot không tích hợp các công cụ cần thiết để build và compile game, chẳng hạn như MSBuild và trình biên dịch C#. Các công cụ này nằm trong .NET SDK và cần được cài đặt riêng.

Tóm lại, bạn phải cài đặt .NET SDK **và** phiên bản Godot hỗ trợ .NET.

Tải xuống và cài đặt phiên bản ổn định mới nhất của SDK từ `.NET download page <https://dotnet.microsoft.com/download>`__. Godot 4.5 yêu cầu .NET 8 trở lên, nhưng để export sang Android thì cần .NET 9 trở lên.

.. important::

    Hãy nhớ cài đặt phiên bản 64-bit của SDK nếu bạn đang sử dụng phiên bản Godot 64-bit.

Nếu bạn build Godot từ source, hãy đảm bảo làm theo các bước để bật hỗ trợ .NET trong bản build như được nêu trên trang :ref:`doc_compiling_with_dotnet`.

.. _doc_c_sharp_setup_external_editor:

Cấu hình external editor
------------------------

Hỗ trợ C# trong script editor tích hợp sẵn của Godot còn hạn chế. Hãy cân nhắc sử dụng một IDE hoặc editor bên ngoài, chẳng hạn như `Visual Studio Code <https://code.visualstudio.com/>`__ hoặc `Visual Studio <https://visualstudio.microsoft.com/>`__. Các công cụ này cung cấp tính năng autocompletion, debugging và những tính năng hữu ích khác cho C#. Để chọn external editor trong Godot, hãy nhấp vào **Editor → Editor Settings** rồi cuộn xuống **Dotnet**. Trong **Dotnet**, nhấp vào **Editor** và chọn external editor bạn muốn sử dụng. Hiện tại Godot hỗ trợ các external editor sau:

- Visual Studio 2022 - Visual Studio Code - MonoDevelop - Visual Studio for Mac - JetBrains Rider

Xem các phần sau để biết cách cấu hình external editor:

JetBrains Rider
~~~~~~~~~~~~~~~

Sau khi đọc phần "Prerequisites", bạn có thể tải xuống và cài đặt `JetBrains Rider <https://www.jetbrains.com/rider/download>`__.

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **JetBrains Rider**.

Trong Rider:

- Đặt **MSBuild version** thành **.NET Core**. - Nếu bạn đang sử dụng phiên bản Rider cũ hơn 2024.2, hãy cài đặt plugin **Godot support**. Tính năng này hiện đã được tích hợp sẵn trong Rider.

Visual Studio Code
~~~~~~~~~~~~~~~~~~

Sau khi đọc phần "Prerequisites", bạn có thể tải xuống và cài đặt `Visual Studio Code <https://code.visualstudio.com/download>`__ (còn gọi là VS Code).

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **Visual Studio Code**.

Trong Visual Studio Code:

- Cài đặt extension `C# <https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp>`__.

Để cấu hình một project cho việc debugging, bạn cần có file ``tasks.json`` và ``launch.json`` trong thư mục ``.vscode`` với cấu hình cần thiết.

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

Để launch configuration này hoạt động, bạn cần thiết lập một biến môi trường GODOT4 trỏ đến file thực thi Godot, hoặc thay thế tham số ``program`` bằng đường dẫn đến file thực thi Godot.

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

Giờ đây, khi khởi động debugger trong Visual Studio Code, project Godot của bạn sẽ chạy.

Visual Studio (chỉ dành cho Windows)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tải xuống và cài đặt phiên bản mới nhất của `Visual Studio <https://visualstudio.microsoft.com/downloads/>`__. Visual Studio sẽ bao gồm các SDK cần thiết nếu bạn chọn đúng workloads, vì vậy bạn không cần cài đặt thủ công những thành phần được liệt kê trong phần "Prerequisites".

Trong quá trình cài đặt Visual Studio, hãy chọn workload này:

- .NET desktop development

Trong menu **Editor → Editor Settings** của Godot:

- Đặt **Dotnet** -> **Editor** -> **External Editor** thành **Visual Studio**.

.. note:: If you see an error like "Unable to find package Godot.NET.Sdk",
          cấu hình NuGet của bạn có thể không chính xác và cần được sửa.

          Một cách đơn giản để sửa file cấu hình NuGet là tạo lại file đó. Trong cửa sổ file explorer, đi đến ``%AppData%\NuGet``. Đổi tên hoặc xóa file ``NuGet.Config``. Khi bạn build lại project Godot, file này sẽ tự động được tạo với các giá trị mặc định.

Để debug các script C# bằng Visual Studio, hãy mở file .sln được tạo sau khi mở script C# đầu tiên trong editor. Trong menu **Debug**, đi đến mục menu **Debug Properties** của project. Nhấp vào nút **Create a new profile** và chọn **Executable**. Trong trường **Executable**, hãy duyệt đến đường dẫn của phiên bản C# của Godot editor hoặc nhập ``%GODOT4%`` nếu bạn đã tạo một biến môi trường cho đường dẫn đến file thực thi Godot. Đường dẫn này phải trỏ đến file thực thi Godot chính, không phải phiên bản 'console'. Đối với **Working Directory**, hãy nhập một dấu chấm đơn, ``.``, biểu thị thư mục hiện tại. Đồng thời chọn checkbox **Enable native code debugging**. Bây giờ bạn có thể đóng cửa sổ này, nhấp vào mũi tên hướng xuống trên dropdown debug profile và chọn launch profile mới. Nhấn nút start màu xanh lá, game của bạn sẽ bắt đầu chạy ở debug mode.


Tạo script C#
-------------

Sau khi thiết lập C# cho Godot thành công, bạn sẽ thấy tùy chọn sau khi chọn **Attach Script** trong context menu của một node trong scene:

.. image:: img/attachcsharpscript.webp

Lưu ý rằng dù một số chi tiết có thay đổi, hầu hết các khái niệm vẫn hoạt động tương tự khi sử dụng C# để viết script. Nếu bạn mới làm quen với Godot, ở thời điểm này bạn có thể muốn làm theo các tutorial trên :ref:`doc_scripting`. Mặc dù một số trang tài liệu vẫn chưa có ví dụ C#, hầu hết các khái niệm đều có thể chuyển đổi từ GDScript.

Thiết lập project và workflow
-----------------------------

Khi bạn tạo script C# đầu tiên, Godot sẽ khởi tạo các file project C# cho project Godot của bạn. Việc này bao gồm tạo một C# solution (``.sln``) và một project file (``.csproj``), cùng với một số file và thư mục tiện ích (``.godot/mono``). Tất cả các thành phần này, ngoại trừ ``.godot/mono``, đều quan trọng và nên được commit vào hệ thống version control của bạn. Mọi thứ bên trong ``.godot`` đều có thể an toàn được thêm vào danh sách ignore của VCS. Khi troubleshooting, đôi khi việc xóa thư mục ``.godot/mono`` và để Godot tạo lại thư mục này có thể hữu ích.

Ví dụ
-----

Dưới đây là một script C# trống với một số comment để minh họa cách hoạt động.

.. code-block:: csharp

    using Godot;

    public partial class YourCustomClass : Node
    {
        // Các member variable ở đây, ví dụ:
        private int _a = 2;
        private string _b = "textvar";

        public override void _Ready()
        {
            // Được gọi mỗi khi node được thêm vào scene.
            // Phần khởi tạo ở đây.
            GD.Print("Hello from C# to Godot :)");
        }

        public override void _Process(double delta)
        {
            // Được gọi ở mỗi frame. Delta là khoảng thời gian kể từ frame trước đó.
            // Cập nhật logic game ở đây.
        }
    }

Như bạn có thể thấy, các function thường nằm trong global scope ở GDScript, chẳng hạn như function ``print`` của Godot, có sẵn trong static class ``GD``, thuộc namespace ``Godot``. Để xem danh sách đầy đủ các method trong class ``GD``, hãy xem các trang class reference dành cho
:ref:`@GDScript <class_@gdscript>` and :ref:`@GlobalScope <class_@globalscope>`.

.. note::

    Hãy nhớ rằng class bạn muốn attach vào node phải có cùng tên với file ``.cs``. Nếu không, bạn sẽ nhận được lỗi sau:

    *"Cannot find class XXX for script res://XXX.cs"*

.. _doc_c_sharp_general_differences:

Những khác biệt chung giữa C# và GDScript
-----------------------------------------

C# API sử dụng ``PascalCase`` thay vì ``snake_case`` trong GDScript/C++. Khi có thể, các field và getter/setter đã được chuyển đổi thành property. Nhìn chung, C# Godot API hướng tới việc mang tính idiomatic nhất có thể trong phạm vi hợp lý.

Để biết thêm thông tin, hãy xem trang :ref:`doc_c_sharp_differences`.

.. warning::

    Bạn cần (re)build các project assembly mỗi khi muốn thấy các biến được export hoặc signal mới trong editor. Có thể kích hoạt thủ công quá trình build này bằng cách nhấp vào nút **Build** ở góc trên bên phải của editor.

    .. image:: img/build_dotnet.webp

    Bạn cũng cần rebuild các project assembly để áp dụng những thay đổi trong các script "tool".

Các điểm cần lưu ý và vấn đề đã biết hiện tại
---------------------------------------------

Vì hỗ trợ C# trong Godot còn khá mới, vẫn có một số khó khăn ban đầu và những vấn đề cần được hoàn thiện. Dưới đây là danh sách các vấn đề quan trọng nhất mà bạn nên biết khi bắt đầu sử dụng C# trong Godot, nhưng nếu không chắc chắn, bạn cũng nên xem qua `issue tracker for .NET issues <https://github.com/godotengine/godot/labels/topic%3Adotnet>`_ chính thức.

- Writing editor plugins is possible, but it is currently quite convoluted. - State is currently not saved and restored when hot-reloading, with the exception of exported variables. - Attached C# scripts should refer to a class that has a class name that matches the file name. - There are some methods such as ``Get()``/``Set()``, ``Call()``/``CallDeferred()`` and signal connection method ``Connect()`` that rely on Godot's ``snake_case`` API naming conventions. So when using e.g. ``CallDeferred("AddChild")``, ``AddChild`` will not work because the API is expecting the original ``snake_case`` version ``add_child``. However, you can use any custom properties or methods without this limitation. Prefer using the exposed ``StringName`` in the ``PropertyName``, ``MethodName`` and ``SignalName`` to avoid extra ``StringName`` allocations and worrying about snake_case naming.


Kể từ Godot 4.0, việc export các project .NET được hỗ trợ trên các nền tảng desktop (Linux, Windows và macOS). Các nền tảng khác sẽ được hỗ trợ trong những bản phát hành 4.x tương lai.

Các lỗi thường gặp
------------------

Bạn có thể gặp lỗi sau khi cố gắng sửa đổi một số giá trị trong các object của Godot, chẳng hạn khi cố thay đổi tọa độ X của một ``Node2D``:

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

Điều này hoàn toàn bình thường. Các struct (trong ví dụ này là một ``Vector2``) trong C# được sao chép khi gán, nghĩa là khi bạn lấy một object như vậy từ một property hoặc indexer, bạn nhận được một bản sao của nó, không phải chính object đó. Việc sửa đổi bản sao nói trên mà không gán lại sau đó sẽ không mang lại kết quả gì.

Cách khắc phục rất đơn giản: lấy toàn bộ struct, sửa đổi giá trị bạn muốn thay đổi, rồi gán lại property.

.. code-block:: csharp

    var newPosition = Position;
    newPosition.X = 100.0f;
    Position = newPosition;

Kể từ C# 10, bạn cũng có thể sử dụng `with expressions <https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/with-expression>`_ trên các struct, cho phép thực hiện cùng việc đó trên một dòng duy nhất.

.. code-block:: csharp

    Position = Position with { X = 100.0f };

Bạn có thể đọc thêm về lỗi này tại `C# language reference <https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/cs1612>`_.

Hiệu năng của C# trong Godot
----------------------------

.. seealso::

    Để xem so sánh hiệu năng giữa các ngôn ngữ được Godot hỗ trợ, hãy xem :ref:`doc_faq_which_programming_language_is_fastest`.

Hầu hết các property của object Godot C# dựa trên ``GodotObject`` (chẳng hạn như mọi ``Node`` như ``Control`` hoặc ``Node3D`` như ``Camera3D``) đều yêu cầu các native call (interop), vì chúng giao tiếp với core C++ của Godot. Hãy cân nhắc gán giá trị của các property như vậy vào một biến cục bộ nếu bạn cần sửa đổi hoặc đọc chúng nhiều lần tại cùng một vị trí trong code:

.. code-block:: csharp

    using Godot;

    public partial class YourCustomClass : Node3D
    {
        private void ExpensiveReposition()
        {
            for (var i = 0; i < 10; i++)
            {
                // Position được đọc và thiết lập 10 lần, dẫn đến các lần interop với native.
                // Ngoài ra, object được reposition 10 lần trong không gian 3D, việc này
                // tốn thêm thời gian.
                Position += new Vector3(i, i);
            }
        }

        private void Reposition()
        {
            // Một biến được sử dụng để tránh interop với native đối với Position trong mỗi vòng lặp.
            var newPosition = Position;
            for (var i = 0; i < 10; i++)
            {
                newPosition += new Vector3(i, i);
            }
            // Chỉ thiết lập Position một lần giúp tránh interop với native và việc reposition trong không gian 3D.
            Position = newPosition;
        }
    }

Việc truyền các mảng raw (chẳng hạn như ``byte[]``) hoặc ``string`` đến API C# của Godot yêu cầu marshalling, vốn tương đối tốn kém.

Việc chuyển đổi ngầm định từ ``string`` sang ``NodePath`` hoặc ``StringName`` phát sinh cả chi phí interop với native và marshalling, vì ``string`` phải được marshal và truyền đến native constructor tương ứng.

Sử dụng package NuGet trong Godot
---------------------------------

Các package `NuGet <https://www.nuget.org/>`_ có thể được cài đặt và sử dụng với Godot, giống như trong mọi project C#. Nhiều IDE có thể thêm package trực tiếp. Bạn cũng có thể thêm chúng thủ công bằng cách thêm package reference vào file ``.csproj`` nằm trong thư mục gốc của project:

.. code-block:: xml
    :emphasize-lines: 2

        <ItemGroup>
            <PackageReference Include="Newtonsoft.Json" Version="11.0.2" />
        </ItemGroup>
        ...
    </Project>

Godot tự động tải xuống và thiết lập các package NuGet mới được thêm vào trong lần build project tiếp theo.

Profiling code C# của bạn
-------------------------

Có thể sử dụng các công cụ sau để profiling hiệu năng và bộ nhớ của managed code:

- JetBrains Rider với plugin dotTrace/dotMemory. - JetBrains dotTrace/dotMemory độc lập. - Visual Studio.

Có thể profiling đồng thời managed code và unmanaged code bằng cả các công cụ của JetBrains lẫn Visual Studio, nhưng chỉ giới hạn trên Windows.
