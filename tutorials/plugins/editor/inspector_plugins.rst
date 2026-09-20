.. _doc_inspector_plugins:

Plugin Inspector
================

Dock Inspector cho phép bạn tạo các widget tùy chỉnh để chỉnh sửa thuộc tính thông qua plugin. Điều này có thể hữu ích khi làm việc với các datatype và resource tùy chỉnh, mặc dù bạn cũng có thể dùng tính năng này để thay đổi các widget Inspector cho những kiểu dựng sẵn. Bạn có thể thiết kế các control tùy chỉnh cho từng thuộc tính cụ thể, toàn bộ object, và thậm chí các control riêng biệt gắn với những datatype cụ thể.

Hướng dẫn này giải thích cách sử dụng :ref:`class_EditorInspectorPlugin` và
:ref:`class_EditorProperty` classes to create a custom interface for integers,
thay thế hành vi mặc định bằng một button tạo các giá trị ngẫu nhiên từ 0 đến 99.

.. figure:: img/inspector_plugin_example.png
   :align: center

   The default behavior on the left and the end result on the right.


Thiết lập plugin của bạn
------------------------

Tạo một plugin trống mới để bắt đầu.

.. seealso:: See :ref:`doc_making_plugins` guide to set up your new plugin.

Giả sử bạn đã đặt tên cho thư mục plugin là ``my_inspector_plugin``. Khi đó, bạn sẽ có một thư mục ``addons/my_inspector_plugin`` mới chứa hai file: ``plugin.cfg`` và ``plugin.gd``.

Như trước đây, ``plugin.gd`` là một script kế thừa :ref:`class_EditorPlugin` và bạn cần thêm code mới cho các method ``_enter_tree`` và ``_exit_tree`` của nó. Để thiết lập inspector plugin, bạn phải load script, sau đó tạo và thêm instance bằng cách gọi ``add_inspector_plugin()``. Nếu plugin bị vô hiệu hóa, bạn nên xóa instance đã thêm bằng cách gọi ``remove_inspector_plugin()``.

.. note:: Here, you are loading a script and not a packed scene. Therefore you
          nên sử dụng ``new()`` thay vì ``instantiate()``.

.. tabs::
  .. code-tab:: gdscript GDScript

    # plugin.gd
    @tool
    extends EditorPlugin

    var plugin


    func _enter_tree():
        plugin = preload("res://addons/my_inspector_plugin/my_inspector_plugin.gd").new()
        add_inspector_plugin(plugin)


    func _exit_tree():
        remove_inspector_plugin(plugin)

  .. code-tab:: csharp

    // Plugin.cs
    #if TOOLS
    using Godot;

    [Tool]
    public partial class Plugin : EditorPlugin
    {
        private MyInspectorPlugin _plugin;

        public override void _EnterTree()
        {
            _plugin = new MyInspectorPlugin();
            AddInspectorPlugin(_plugin);
        }

        public override void _ExitTree()
        {
            RemoveInspectorPlugin(_plugin);
        }
    }
    #endif


Tương tác với Inspector
-----------------------

Để tương tác với dock Inspector, script ``my_inspector_plugin.gd`` của bạn phải kế thừa class :ref:`class_EditorInspectorPlugin`. Class này cung cấp một số virtual method ảnh hưởng đến cách Inspector xử lý các thuộc tính.

Để có bất kỳ tác dụng nào, script phải triển khai method ``_can_handle()``. Hàm này được gọi cho từng :ref:`class_Object` được chỉnh sửa và phải trả về ``true`` nếu plugin này nên xử lý object hoặc các thuộc tính của nó.

.. note:: This includes any :ref:`class_Resource` attached to the object.

Bạn có thể triển khai thêm bốn method khác để thêm các control vào Inspector tại những vị trí cụ thể. Các method ``_parse_begin()`` và ``_parse_end()`` lần lượt chỉ được gọi một lần ở đầu và cuối quá trình phân tích cú pháp cho mỗi object. Chúng có thể thêm control ở đầu hoặc cuối bố cục Inspector bằng cách gọi ``add_custom_control()``.

Khi editor phân tích object, nó gọi các method ``_parse_category()`` và ``_parse_property()``. Tại đó, ngoài ``add_custom_control()``, bạn có thể gọi cả ``add_property_editor()`` và ``add_property_editor_for_multiple_properties()``. Sử dụng hai method sau để thêm riêng các control dựa trên :ref:`class_EditorProperty`.

.. tabs::
 .. code-tab:: gdscript GDScript

    # my_inspector_plugin.gd
    @tool
    extends EditorInspectorPlugin

    var RandomIntEditor = preload("res://addons/my_inspector_plugin/random_int_editor.gd")


    func _can_handle(object):
        # Trong ví dụ này, chúng ta hỗ trợ mọi object.
        return true


    func _parse_property(object, type, name, hint_type, hint_string, usage_flags, wide):
        # Chúng ta xử lý các thuộc tính có kiểu integer.
        if type == TYPE_INT:
            # Tạo một instance của property editor tùy chỉnh và đăng ký
            # nó cho một property path cụ thể.
            add_property_editor(name, RandomIntEditor.new())
            # Thông báo cho editor xóa property editor mặc định đối với
            # kiểu thuộc tính này.
            return true
        else:
            return false

 .. code-tab:: csharp

    // MyInspectorPlugin.cs
    #if TOOLS
    using Godot;

    [Tool]
    public partial class MyInspectorPlugin : EditorInspectorPlugin
    {
        public override bool _CanHandle(GodotObject @object)
        {
            // Trong ví dụ này, chúng ta hỗ trợ mọi object.
            return true;
        }

        public override bool _ParseProperty(GodotObject @object, Variant.Type type,
            string name, PropertyHint hintType, string hintString,
            PropertyUsageFlags usageFlags, bool wide)
        {
            // Chúng ta xử lý các thuộc tính có kiểu integer.
            if (type == Variant.Type.Int)
            {
                // Tạo một instance của property editor tùy chỉnh và đăng ký
                // nó cho một property path cụ thể.
                AddPropertyEditor(name, new RandomIntEditor());
                // Thông báo cho editor xóa property editor mặc định đối với
                // kiểu thuộc tính này.
                return true;
            }

            return false;
        }
    }
    #endif

Thêm một interface để chỉnh sửa thuộc tính
------------------------------------------

Class :ref:`class_EditorProperty` là một kiểu :ref:`class_Control` đặc biệt có thể tương tác với các object đang được chỉnh sửa trong dock Inspector. Nó không hiển thị bất cứ thứ gì nhưng có thể chứa bất kỳ control node nào khác, bao gồm cả các scene phức tạp.

Script kế thừa này có ba phần thiết yếu
:ref:`class_EditorProperty`:

1. Bạn phải định nghĩa method ``_init()`` để thiết lập cấu trúc của các control node.

2. Bạn nên triển khai ``_update_property()`` để xử lý các thay đổi đối với dữ liệu từ bên ngoài.

3. Tại một thời điểm nào đó, phải phát một signal để thông báo cho Inspector rằng control đã thay đổi thuộc tính bằng cách sử dụng ``emit_changed``.

Bạn có thể hiển thị widget tùy chỉnh theo hai cách. Chỉ cần sử dụng method ``add_child()`` mặc định để hiển thị nó ở bên phải tên thuộc tính, hoặc sử dụng ``add_child()`` rồi đến ``set_bottom_editor()`` để đặt nó bên dưới tên.

.. FIXME: Hiện tại tab thứ hai đã tắt lexer C# để tô sáng, vì code được cung cấp gây ra lỗi.

.. tabs::
 .. code-tab:: gdscript GDScript

    # random_int_editor.gd
    @tool
    extends EditorProperty


    # Control chính để chỉnh sửa thuộc tính.
    var property_control = Button.new()
    # Giá trị nội bộ của thuộc tính.
    var current_value = 0
    # Một cơ chế bảo vệ chống lại các thay đổi nội bộ khi thuộc tính được cập nhật.
    var updating = false


    func _init():
        # Thêm control dưới dạng direct child của node EditorProperty.
        add_child(property_control)
        # Đảm bảo control có thể giữ focus.
        add_focusable(property_control)
        # Thiết lập trạng thái ban đầu và kết nối với signal để theo dõi các thay đổi.
        refresh_control_text()
        property_control.pressed.connect(_on_button_pressed)


    func _on_button_pressed():
        # Bỏ qua signal nếu thuộc tính hiện đang được cập nhật.
        if (updating):
            return

        # Tạo một số nguyên ngẫu nhiên mới từ 0 đến 99.
        current_value = randi() % 100
        refresh_control_text()
        emit_changed(get_edited_property(), current_value)


    func _update_property():
        # Đọc giá trị hiện tại từ thuộc tính.
        var new_value = get_edited_object()[get_edited_property()]
        if (new_value == current_value):
            return

        # Cập nhật control bằng giá trị mới.
        updating = true
        current_value = new_value
        refresh_control_text()
        updating = false

    func refresh_control_text():
        property_control.text = "Value: " + str(current_value)

 .. code-tab:: csharp

    // RandomIntEditor.cs
    #if TOOLS
    using Godot;

    [Tool]
    public partial class RandomIntEditor : EditorProperty
    {
        // Control chính để chỉnh sửa thuộc tính.
        private Button _propertyControl = new Button();
        // Giá trị nội bộ của thuộc tính.
        private int _currentValue = 0;
        // Một cơ chế bảo vệ chống lại các thay đổi nội bộ khi thuộc tính được cập nhật.
        private bool _updating = false;

        public RandomIntEditor()
        {
            // Thêm control dưới dạng direct child của node EditorProperty.
            AddChild(_propertyControl);
            // Đảm bảo control có thể giữ focus.
            AddFocusable(_propertyControl);
            // Thiết lập trạng thái ban đầu và kết nối với signal để theo dõi các thay đổi.
            RefreshControlText();
            _propertyControl.Pressed += OnButtonPressed;
        }

        private void OnButtonPressed()
        {
            // Bỏ qua signal nếu thuộc tính hiện đang được cập nhật.
            if (_updating)
            {
                return;
            }

            // Tạo một số nguyên ngẫu nhiên mới từ 0 đến 99.
            _currentValue = (int)GD.Randi() % 100;
            RefreshControlText();
            EmitChanged(GetEditedProperty(), _currentValue);
        }

        public override void _UpdateProperty()
        {
            // Đọc giá trị hiện tại từ thuộc tính.
            var newValue = (int)GetEditedObject().Get(GetEditedProperty());
            if (newValue == _currentValue)
            {
                return;
            }

            // Cập nhật control bằng giá trị mới.
            _updating = true;
            _currentValue = newValue;
            RefreshControlText();
            _updating = false;
        }

        private void RefreshControlText()
        {
            _propertyControl.Text = $"Value: {_currentValue}";
        }
    }
    #endif

Sử dụng code ví dụ ở trên, bạn sẽ có thể tạo một widget tùy chỉnh thay thế control :ref:`class_SpinBox` mặc định cho các số nguyên bằng một
:ref:`class_Button` that generates random values.
