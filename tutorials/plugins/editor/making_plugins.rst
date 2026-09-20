.. _doc_making_plugins:

Tạo plugin
==========

Giới thiệu về plugin
--------------------

Plugin là một cách tuyệt vời để mở rộng editor bằng các công cụ hữu ích. Plugin có thể được tạo hoàn toàn bằng GDScript và các scene tiêu chuẩn, thậm chí không cần tải lại editor. Không giống như module, bạn không cần tạo mã C++ hay biên dịch lại engine. Mặc dù điều này khiến plugin kém mạnh mẽ hơn, bạn vẫn có thể làm được rất nhiều việc với chúng. Lưu ý rằng plugin tương tự như bất kỳ scene nào bạn có thể tạo, ngoại trừ việc nó được tạo bằng script để bổ sung chức năng cho editor.

Tutorial này sẽ hướng dẫn bạn tạo hai plugin để hiểu cách chúng hoạt động và có thể tự phát triển plugin của riêng mình. Plugin đầu tiên là một node tùy chỉnh mà bạn có thể thêm vào bất kỳ scene nào trong project, còn plugin kia là một dock tùy chỉnh được thêm vào editor.

.. _doc_making_plugins_template:

Tạo plugin
----------

Trước khi bắt đầu, hãy tạo một project mới, trống, ở bất kỳ vị trí nào bạn muốn. Project này sẽ làm nền tảng để phát triển và kiểm thử các plugin.

Điều đầu tiên bạn cần để editor nhận diện một plugin mới là tạo hai file: một ``plugin.cfg`` để cấu hình và một tool script chứa chức năng. Plugin có đường dẫn tiêu chuẩn như ``addons/plugin_name`` bên trong thư mục project. Godot cung cấp một hộp thoại để tạo các file đó và đặt chúng vào đúng vị trí.

Trên thanh công cụ chính, hãy nhấp vào danh sách thả xuống ``Project``. Sau đó nhấp vào ``Project Settings...``. Chuyển đến tab ``Plugins``, rồi nhấp vào nút :button:`Create New Plugin` ở góc trên bên phải.

Bạn sẽ thấy hộp thoại xuất hiện như sau:

.. image:: img/making_plugins-create_plugin_dialog.webp

Văn bản placeholder trong mỗi trường mô tả cách trường đó ảnh hưởng đến việc tạo file của plugin và các giá trị trong file cấu hình.

Để tiếp tục với ví dụ, hãy sử dụng các giá trị sau:

.. tabs::
 .. code-tab:: ini GDScript

    Plugin Name: My Custom Node
    Subfolder: my_custom_node
    Description: A custom node made to extend the Godot Engine.
    Author: Your Name Here
    Version: 1.0.0
    Language: GDScript
    Script Name: custom_node.gd

 .. code-tab:: ini C#

    Plugin Name: My Custom Node
    Subfolder: MyCustomNode
    Description: A custom node made to extend the Godot Engine.
    Author: Your Name Here
    Version: 1.0.0
    Language: C#
    Script Name: CustomNode.cs

.. warning::

    Trong C#, script EditorPlugin cần được biên dịch, việc này yêu cầu build project. Sau khi build project, bạn có thể bật plugin trong tab ``Plugins`` của ``Project Settings``.

Bạn sẽ có một cấu trúc thư mục như sau:

.. image:: img/making_plugins-my_custom_mode_folder.webp

``plugin.cfg`` là một file INI chứa metadata về plugin của bạn. Tên và mô tả giúp mọi người hiểu plugin làm gì. Tên của bạn giúp ghi nhận chính xác công sức của bạn. Số phiên bản giúp người khác biết họ có đang sử dụng phiên bản đã lỗi thời hay không; nếu bạn không chắc nên đặt số phiên bản như thế nào, hãy xem `Semantic Versioning <https://semver.org/>`_. File script chính sẽ hướng dẫn Godot về chức năng của plugin trong editor khi plugin được kích hoạt.

File script
~~~~~~~~~~~

Khi tạo plugin, hộp thoại sẽ tự động mở script EditorPlugin cho bạn. Script này có hai yêu cầu mà bạn không thể thay đổi: nó phải là một ``@tool`` script, nếu không sẽ không được load đúng cách trong editor, và nó phải kế thừa từ :ref:`class_EditorPlugin`.

.. warning::

    Ngoài script EditorPlugin, mọi GDScript khác mà plugin sử dụng cũng *phải* là tool. Bất kỳ GDScript nào được editor sử dụng mà không có ``@tool`` sẽ hoạt động như một file rỗng!

Việc xử lý khởi tạo và dọn dẹp tài nguyên rất quan trọng. Một cách thực hành tốt là sử dụng hàm ảo
:ref:`_enter_tree() <class_Node_private_method__enter_tree>` to initialize your plugin and
:ref:`_exit_tree() <class_Node_private_method__exit_tree>` to clean it up. Thankfully,
hộp thoại sẽ tạo các callback này cho bạn. Script của bạn sẽ trông tương tự như sau:

.. _doc_making_plugins_template_code:
.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin


    func _enter_tree():
        # Đặt phần khởi tạo plugin ở đây.
        pass


    func _exit_tree():
        # Đặt phần dọn dẹp plugin ở đây.
        pass

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class CustomNode : EditorPlugin
    {
        public override void _EnterTree()
        {
            // Đặt phần khởi tạo plugin ở đây.
        }

        public override void _ExitTree()
        {
            // Đặt phần dọn dẹp plugin ở đây.
        }
    }
    #endif

Đây là một template phù hợp để sử dụng khi tạo plugin mới.

Node tùy chỉnh
--------------

Đôi khi bạn muốn một hành vi nhất định xuất hiện trong nhiều node, chẳng hạn như một scene hoặc control tùy chỉnh có thể tái sử dụng. Instancing hữu ích trong nhiều trường hợp, nhưng đôi khi có thể trở nên cồng kềnh, đặc biệt khi bạn sử dụng nó trong nhiều project. Một giải pháp tốt là tạo plugin thêm một node có hành vi tùy chỉnh.

Trong tutorial này, chúng ta sẽ tạo một button in ra thông báo khi được nhấp. Để làm vậy, chúng ta sẽ cần một script kế thừa từ
:ref:`class_Button`. It could also extend
:ref:`class_BaseButton` if you prefer:

.. tabs::
    .. code-tab:: gdscript GDScript

        # Tùy chọn, thêm để thực thi trong editor.
        @tool

        # Icon là tùy chọn.
        # Ngoài ra, bạn có thể sử dụng UID của icon hoặc đường dẫn tuyệt đối.
        @icon("icon.svg")

        # Tự động đăng ký node trong hộp thoại Create New Node
        # và cung cấp node để các script khác sử dụng.
        class_name MyButton
        extends Button


        func _enter_tree():
            pressed.connect(clicked)


        func clicked():
            print("You clicked me!")

    .. code-tab:: csharp

        using Godot;

        // Tùy chọn, thêm để thực thi trong editor.
        [Tool]

        // Icon là tùy chọn.
        // Ngoài ra, bạn có thể sử dụng UID của icon hoặc đường dẫn tuyệt đối.
        [Icon("icon.svg")]

        // Tự động đăng ký node trong hộp thoại Create New Node
        // và cung cấp node để các script khác sử dụng.
        [GlobalClass]
        public partial class MyButton : Button
        {
            public override void _EnterTree()
            {
                Pressed += Clicked;
            }

            public void Clicked()
            {
                GD.Print("You clicked me!");
            }
        }

Vậy là xong button cơ bản. Bạn có thể lưu nó dưới dạng ``my_button.gd`` bên trong thư mục plugin. Bạn có thể có một icon 16×16 để hiển thị trong scene tree. Nếu không có, bạn có thể lấy icon mặc định từ engine và lưu vào thư mục `addons/my_custom_node` dưới tên `icon.svg`, hoặc sử dụng logo Godot mặc định (`@icon("res://icon.svg")`).

.. tip::

    Các hình ảnh SVG được sử dụng làm icon node tùy chỉnh nên có các tùy chọn **Editor > Scale With Editor Scale** và **Editor > Convert Colors With Editor Theme**
    :ref:`import options <doc_importing_images_editor_import_options>` enabled. This allows
    để tuân theo thiết lập tỷ lệ và theme của editor nếu các icon được thiết kế với cùng bảng màu như icon của chính Godot.

.. image:: img/making_plugins-custom_node_icon.png


Sau khi hoàn tất, plugin sẽ có sẵn trong danh sách plugin trong **Project Settings**, vì vậy hãy kích hoạt plugin như được giải thích trong `Kiểm tra kết quả`_.

Sau đó, hãy thử bằng cách thêm node mới của bạn:

.. image:: img/making_plugins-custom_node_create.webp

Khi thêm node, bạn có thể thấy node đã được gắn script mà bạn tạo. Đặt text cho button, lưu và chạy scene. Khi nhấp vào button, bạn sẽ thấy một đoạn text trong console:

.. image:: img/making_plugins-custom_node_console.webp

.. _doc_making_plugins_custom_dock:

Dock tùy chỉnh
--------------

Đôi khi bạn cần mở rộng editor và thêm các công cụ luôn sẵn dùng. Một cách dễ thực hiện là thêm dock mới bằng plugin. Dock chỉ là các scene dựa trên Control, vì vậy chúng được tạo theo cách tương tự như các scene GUI thông thường.

Việc tạo dock tùy chỉnh được thực hiện giống như tạo node tùy chỉnh. Tạo một file ``plugin.cfg`` mới trong thư mục ``addons/my_custom_dock``, sau đó thêm nội dung sau vào file:

.. tabs::
 .. code-tab:: gdscript GDScript

    [plugin]

    name="My Custom Dock"
    description="A custom dock made so I can learn how to make plugins."
    author="Your Name Here"
    version="1.0"
    script="custom_dock.gd"

 .. code-tab:: csharp

    [plugin]

    name="My Custom Dock"
    description="A custom dock made so I can learn how to make plugins."
    author="Your Name Here"
    version="1.0"
    script="CustomDock.cs"

Sau đó, tạo script ``custom_dock.gd`` trong cùng thư mục. Đoạn code sau sẽ giúp bạn bắt đầu.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorDock


    func _enter_tree():
        # Đặt phần khởi tạo dock ở đây.
        pass


    func _exit_tree():
        # Đặt phần dọn dẹp dock ở đây.
        pass

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class CustomNode : EditorDock
    {
        public override void _EnterTree()
        {
            // Đặt phần khởi tạo dock ở đây.
        }

        public override void _ExitTree()
        {
            // Đặt phần dọn dẹp dock ở đây.
        }
    }
    #endif

Vì chúng ta đang cố gắng thêm một dock tùy chỉnh mới, chúng ta cần tạo nội dung cho dock. Nội dung này không khác gì một scene Godot tiêu chuẩn: chỉ cần tạo scene mới trong editor rồi chỉnh sửa nó.

Đối với dock của editor, node gốc **phải** là một :ref:`Control <class_Control>` hoặc một trong các class con của nó. Trong tutorial này, bạn có thể tạo một button duy nhất. Đừng quên thêm text cho button.

.. image:: img/making_plugins-my_custom_dock_scene.webp

Lưu scene này dưới dạng ``my_dock.tscn``. Bây giờ, chúng ta cần lấy scene đã tạo rồi thêm scene đó làm dock trong editor. Để làm việc này, bạn có thể sử dụng hàm
:ref:`add_dock() <class_EditorPlugin_method_add_dock>` from the
:ref:`EditorPlugin <class_EditorPlugin>` class.

Bạn cần chọn vị trí dock và xác định control cần thêm (chính là scene bạn vừa tạo). Đừng quên **xóa dock** khi plugin bị vô hiệu hóa. Script có thể trông như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin


    # Một class member dùng để lưu dock trong suốt vòng đời của plugin.
    var dock


    func _enter_tree():
        # Đặt phần khởi tạo plugin ở đây.
        # Load scene dock và tạo instance của nó.
        var dock_scene = preload("res://addons/my_custom_dock/my_dock.tscn").instantiate()

        # Tạo dock và thêm scene đã load vào đó.
        dock = EditorDock.new()
        dock.add_child(dock_scene)

        dock.title = "My Dock"

        # Note that LEFT_UL means the left of the editor, upper-left dock.
        dock.default_slot = EditorDock.DOCK_SLOT_LEFT_UL

        # Cho phép dock nằm ở bên trái hoặc bên phải editor, cũng như cho phép dock nổi.
        dock.available_layouts = EditorDock.DOCK_LAYOUT_VERTICAL | EditorDock.DOCK_LAYOUT_FLOATING

        add_dock(dock)


    func _exit_tree():
        # Đặt phần dọn dẹp plugin ở đây.
        # Xóa dock.
        remove_dock(dock)
        # Xóa control khỏi bộ nhớ.
        dock.queue_free()

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class CustomDock : EditorPlugin
    {
        private EditorDock _dock;

        public override void _EnterTree()
        {
            var dockScene = GD.Load<PackedScene>("res://addons/MyCustomDock/MyDock.tscn").Instantiate<Control>();

            // Tạo dock và thêm scene đã load vào đó.
            _dock = new EditorDock();
            _dock.AddChild(dockScene);

            _dock.Title = "My Dock";

            // Note that LeftUl means the left of the editor, upper-left dock.
            _dock.DefaultSlot = DockSlot.LeftUl;

            // Cho phép dock nằm ở bên trái hoặc bên phải editor, cũng như cho phép dock nổi.
            _dock.AvailableLayouts = DockLayout.Horizontal | DockLayout.Floating;

            AddDock(_dock);
        }

        public override void _ExitTree()
        {
            // Đặt phần dọn dẹp plugin ở đây.
            // Xóa dock.
            RemoveDock(_dock);
            // Xóa control khỏi bộ nhớ.
            _dock.QueueFree();
        }
    }
    #endif

Lưu ý rằng mặc dù dock ban đầu sẽ xuất hiện ở vị trí đã chỉ định, người dùng có thể tự do thay đổi vị trí của dock và lưu bố cục kết quả.

Kiểm tra kết quả
~~~~~~~~~~~~~~~~

Bây giờ là lúc kiểm tra kết quả công việc của bạn. Mở **Project Settings** rồi nhấp vào tab **Plugins**. Plugin của bạn sẽ là plugin duy nhất trong danh sách.

.. image:: img/making_plugins-project_settings.webp

Bạn có thể thấy plugin chưa được bật. Nhấp vào checkbox **Enable** để kích hoạt plugin. Dock sẽ hiển thị ngay cả trước khi bạn đóng cửa sổ cài đặt. Bây giờ bạn sẽ có một dock tùy chỉnh:

.. image:: img/making_plugins-custom_dock.webp

.. _doc_making_plugins_autoload:

Đăng ký autoload/singleton trong plugin
---------------------------------------

Các plugin của editor có thể tự động đăng ký
:ref:`autoloads <doc_singletons_autoload>` when the plugin is enabled.
Điều này cũng bao gồm việc hủy đăng ký autoload khi plugin bị vô hiệu hóa.

Điều này giúp thiết lập plugin nhanh hơn cho người dùng, vì họ không còn phải tự thêm autoload vào project settings nếu plugin của editor yêu cầu sử dụng autoload.

Sử dụng code sau để đăng ký một singleton từ plugin của editor:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin

    # Thay giá trị này bằng tên autoload theo kiểu PascalCase, như quy định trong style guide của GDScript.
    const AUTOLOAD_NAME = "SomeAutoload"


    func _enable_plugin():
        # Autoload có thể là một scene hoặc file script.
        add_autoload_singleton(AUTOLOAD_NAME, "res://addons/my_addon/some_autoload.tscn")


    func _disable_plugin():
        remove_autoload_singleton(AUTOLOAD_NAME)

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class MyEditorPlugin : EditorPlugin
    {
        // Thay thế giá trị này bằng tên autoload dạng PascalCase.
        private const string AutoloadName = "SomeAutoload";

        public override void _EnablePlugin()
        {
            // Autoload có thể là một tệp scene hoặc script.
            AddAutoloadSingleton(AutoloadName, "res://addons/MyAddon/SomeAutoload.tscn");
        }

        public override void _DisablePlugin()
        {
            RemoveAutoloadSingleton(AutoloadName);
        }
    }
    #endif

Sử dụng sub-plugin
------------------

Thông thường, một plugin bổ sung nhiều thành phần, chẳng hạn như một node tùy chỉnh và một panel. Trong những trường hợp đó, việc có một plugin script riêng cho từng tính năng có thể sẽ dễ dàng hơn. Bạn có thể sử dụng sub-plugin cho mục đích này.

Trước tiên, hãy tạo tất cả plugin và sub-plugin như các plugin thông thường:

.. image:: img/sub_plugin_creation.webp

Sau đó, di chuyển các sub-plugin vào thư mục plugin chính:

.. image:: img/sub_plugin_moved.webp

Godot sẽ ẩn các sub-plugin khỏi danh sách plugin để người dùng không thể bật hoặc tắt chúng. Thay vào đó, main plugin script nên bật và tắt các sub-plugin như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin

    # Plugin chính nằm tại res://addons/my_plugin/
    const PLUGIN_NAME = "my_plugin"

    func _enable_plugin():
        EditorInterface.set_plugin_enabled(PLUGIN_NAME + "/node", true)
        EditorInterface.set_plugin_enabled(PLUGIN_NAME + "/panel", true)

    func _disable_plugin():
        EditorInterface.set_plugin_enabled(PLUGIN_NAME + "/node", false)
        EditorInterface.set_plugin_enabled(PLUGIN_NAME + "/panel", false)

Mở rộng hơn nữa
---------------

Giờ đây, khi đã học cách tạo các plugin cơ bản, bạn có thể mở rộng editor theo nhiều cách. Có thể bổ sung rất nhiều chức năng cho editor bằng GDScript; đây là một cách mạnh mẽ để tạo các editor chuyên biệt mà không cần đi sâu vào các module C++.

Bạn có thể tự tạo các plugin để hỗ trợ công việc của mình và chia sẻ chúng trên `Asset Library <https://godotengine.org/asset-library/>`_ để mọi người có thể hưởng lợi từ công sức của bạn.
