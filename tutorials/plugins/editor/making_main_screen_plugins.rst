.. _doc_making_main_screen_plugins:

Tạo plugin cho màn hình chính
=============================

Nội dung của tutorial này
-------------------------

Plugin cho màn hình chính cho phép bạn tạo các UI mới ở khu vực trung tâm của editor, xuất hiện bên cạnh các nút "2D", "3D", "Script", "Game" và "AssetLib". Những plugin editor như vậy được gọi là "plugin cho màn hình chính".

Tutorial này hướng dẫn bạn từng bước tạo một plugin cơ bản cho màn hình chính. Để đơn giản, plugin cho màn hình chính của chúng ta sẽ chỉ chứa một nút in văn bản ra console.

Khởi tạo plugin
---------------

Trước tiên, hãy tạo một plugin mới từ menu Plugins. Trong tutorial này, chúng ta sẽ đặt plugin vào một thư mục có tên ``main_screen``, nhưng bạn có thể sử dụng bất kỳ tên nào mình muốn.

Script của plugin sẽ có sẵn các phương thức ``_enter_tree()`` và ``_exit_tree()``, nhưng đối với plugin cho màn hình chính, chúng ta cần thêm một vài phương thức khác. Hãy thêm bốn phương thức sao cho script trông như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin


    func _enter_tree():
        pass


    func _exit_tree():
        pass


    func _has_main_screen():
        return true


    func _make_visible(visible):
        pass


    func _get_plugin_name():
        return "Main Screen Plugin"


    func _get_plugin_icon():
        return EditorInterface.get_editor_theme().get_icon("Node", "EditorIcons")

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class MainScreenPlugin : EditorPlugin
    {
        public override void _EnterTree()
        {

        }

        public override void _ExitTree()
        {

        }

        public override bool _HasMainScreen()
        {
            return true;
        }

        public override void _MakeVisible(bool visible)
        {

        }

        public override string _GetPluginName()
        {
            return "Main Screen Plugin";
        }

        public override Texture2D _GetPluginIcon()
        {
            return EditorInterface.Singleton.GetEditorTheme().GetIcon("Node", "EditorIcons");
        }
    }
    #endif

Phần quan trọng trong script này là hàm ``_has_main_screen()``, được override để trả về ``true``. Editor sẽ tự động gọi hàm này khi kích hoạt plugin, để biết rằng plugin này thêm một khung nhìn trung tâm mới vào editor. Hiện tại, chúng ta sẽ giữ nguyên script này và sẽ quay lại với nó sau.

Scene màn hình chính
--------------------

Tạo một scene mới với node gốc kế thừa từ ``Control`` (đối với plugin mẫu này, chúng ta sẽ tạo node gốc là một ``CenterContainer``). Chọn node gốc này, sau đó trong viewport, nhấp vào menu ``Layout`` và chọn ``Full Rect``. Bạn cũng cần bật cờ kích thước dọc ``Expand`` trong inspector. Panel hiện sử dụng toàn bộ không gian có sẵn trong viewport chính.

Tiếp theo, hãy thêm một button vào plugin màn hình chính mẫu của chúng ta. Thêm một node ``Button``, rồi đặt text thành "Print Hello" hoặc tương tự. Thêm script vào button như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends Button


    func _on_print_hello_pressed():
        print("Hello from the main screen plugin!")

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class PrintHello : Button
    {
        private void OnPrintHelloPressed()
        {
            GD.Print("Hello from the main screen plugin!");
        }
    }


Sau đó, hãy kết nối signal "pressed" với chính nó. Nếu cần trợ giúp về signal, hãy xem bài viết :ref:`doc_signals`.

Chúng ta đã hoàn tất panel màn hình chính. Lưu scene với tên ``main_panel.tscn``.

Cập nhật script của plugin
--------------------------

Chúng ta cần cập nhật script ``main_screen_plugin.gd`` để plugin tạo instance từ scene panel chính và đặt nó vào đúng vị trí. Đây là toàn bộ script của plugin:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends EditorPlugin


    const MainPanel = preload("res://addons/main_screen/main_panel.tscn")

    var main_panel_instance


    func _enter_tree():
        main_panel_instance = MainPanel.instantiate()
        # Thêm panel chính vào viewport chính của editor.
        EditorInterface.get_editor_main_screen().add_child(main_panel_instance)
        # Ẩn panel chính. Đây là việc bắt buộc.
        _make_visible(false)


    func _exit_tree():
        if main_panel_instance:
            main_panel_instance.queue_free()


    func _has_main_screen():
        return true


    func _make_visible(visible):
        if main_panel_instance:
            main_panel_instance.visible = visible


    func _get_plugin_name():
        return "Main Screen Plugin"


    func _get_plugin_icon():
        # Phải trả về một đối tượng Texture nào đó cho icon.
        return EditorInterface.get_editor_theme().get_icon("Node", "EditorIcons")

 .. code-tab:: csharp

    #if TOOLS
    using Godot;

    [Tool]
    public partial class MainScreenPlugin : EditorPlugin
    {
        PackedScene MainPanel = ResourceLoader.Load<PackedScene>("res://addons/main_screen/main_panel.tscn");
        Control MainPanelInstance;

        public override void _EnterTree()
        {
            MainPanelInstance = (Control)MainPanel.Instantiate();
            // Thêm panel chính vào viewport chính của editor.
            EditorInterface.Singleton.GetEditorMainScreen().AddChild(MainPanelInstance);
            // Ẩn panel chính. Đây là việc bắt buộc.
            _MakeVisible(false);
        }

        public override void _ExitTree()
        {
            if (MainPanelInstance != null)
            {
                MainPanelInstance.QueueFree();
            }
        }

        public override bool _HasMainScreen()
        {
            return true;
        }

        public override void _MakeVisible(bool visible)
        {
            if (MainPanelInstance != null)
            {
                MainPanelInstance.Visible = visible;
            }
        }

        public override string _GetPluginName()
        {
            return "Main Screen Plugin";
        }

        public override Texture2D _GetPluginIcon()
        {
            // Phải trả về một đối tượng Texture nào đó cho icon.
            return EditorInterface.Singleton.GetEditorTheme().GetIcon("Node", "EditorIcons");
        }
    }
    #endif

Có một vài dòng cụ thể đã được thêm vào. ``MainPanel`` là một hằng số chứa tham chiếu đến scene, và chúng ta tạo instance của scene đó vào `main_panel_instance`.

Hàm ``_enter_tree()`` được gọi trước ``_ready()``. Đây là nơi chúng ta tạo instance từ scene panel chính và thêm chúng làm các node con vào những phần cụ thể của editor. Chúng ta sử dụng ``EditorInterface.get_editor_main_screen()`` để lấy màn hình chính của editor và thêm instance panel chính làm node con của nó. Chúng ta gọi hàm ``_make_visible(false)`` để ẩn panel chính, nhằm tránh việc panel chiếm không gian khi plugin được kích hoạt lần đầu.

Hàm ``_exit_tree()`` được gọi khi plugin bị vô hiệu hóa. Nếu màn hình chính vẫn tồn tại, chúng ta gọi ``queue_free()`` để giải phóng instance và xóa nó khỏi bộ nhớ.

Hàm ``_make_visible()`` được override để ẩn hoặc hiện panel chính khi cần. Editor sẽ tự động gọi hàm này khi người dùng nhấp vào các nút viewport chính ở phía trên editor.

Các hàm ``_get_plugin_name()`` và ``_get_plugin_icon()`` điều khiển tên và icon được hiển thị cho nút viewport chính của plugin.

Một hàm khác mà bạn có thể thêm là hàm ``_handles()``, cho phép bạn xử lý một loại node và tự động chuyển trọng tâm sang màn hình chính khi loại node đó được chọn. Cách này tương tự như khi nhấp vào một node 3D, editor sẽ tự động chuyển sang viewport 3D.

Icon màn hình chính
-------------------

Bạn có thể sử dụng một trong các icon tích hợp sẵn của editor hoặc cung cấp icon riêng cho plugin màn hình chính. Trong cả hai trường hợp, bạn thực hiện việc này bằng cách override phương thức ``_get_plugin_icon()`` trong script của plugin.

Để sử dụng icon tích hợp sẵn, hãy sao chép tên icon từ website `Godot editor icons <https://godotengine.github.io/editor-icons/>`__. Sử dụng tên đã sao chép từ website làm tham số *đầu tiên* của ``EditorInterface.get_editor_theme().get_icon()`` (tham số thứ hai vẫn phải là ``"EditorIcons"``).

Bạn có thể sử dụng icon tùy chỉnh bằng cách trả về một giá trị như ``preload("res://addons/main_screen/icon.svg")``. Khi thiết kế icon riêng, bạn nên tuân theo các hướng dẫn tương tự như đối với icon của node (khuyến nghị định dạng SVG, kích thước 16×16). Xem :ref:`doc_editor_icons` để biết thông tin về cách tạo icon cho plugin của bạn.

Thử plugin
----------

Kích hoạt plugin trong Project Settings. Bạn sẽ thấy một nút mới bên cạnh 2D, 3D, Script ở phía trên viewport chính. Nhấp vào nút này sẽ đưa bạn đến plugin màn hình chính mới, và button ở giữa sẽ in văn bản.

Nếu muốn thử phiên bản hoàn chỉnh của plugin này, hãy xem các bản demo plugin tại đây: https://github.com/godotengine/godot-demo-projects/tree/master/plugins

Nếu muốn xem một ví dụ đầy đủ hơn về khả năng của plugin màn hình chính, hãy xem các dự án demo 2.5D tại đây: https://github.com/godotengine/godot-demo-projects/tree/master/misc/2.5d
