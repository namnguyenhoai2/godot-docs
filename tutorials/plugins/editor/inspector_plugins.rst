.. _doc_inspector_plugins:

Plugin Inspector
================

Dock Inspector cho phép bạn tạo các widget tùy chỉnh để chỉnh sửa thuộc tính thông qua plugin. Điều này có thể hữu ích khi làm việc với các kiểu dữ liệu và resource tùy chỉnh, mặc dù bạn cũng có thể dùng tính năng này để thay đổi widget Inspector cho các kiểu dựng sẵn. Bạn có thể thiết kế các control tùy chỉnh cho từng thuộc tính cụ thể, toàn bộ đối tượng, và thậm chí các control riêng liên kết với những kiểu dữ liệu cụ thể.

Hướng dẫn này giải thích cách sử dụng :ref:`class_EditorInspectorPlugin` và
các lớp :ref:`class_EditorProperty` để tạo giao diện tùy chỉnh cho số nguyên, thay thế hành vi mặc định bằng một nút tạo các giá trị ngẫu nhiên từ 0 đến 99.

.. figure:: img/inspector_plugin_example.png
   :align: center

   Hành vi mặc định ở bên trái và kết quả cuối cùng ở bên phải.


Thiết lập plugin
----------------

Tạo một plugin trống mới để bắt đầu.

.. seealso:: Xem hướng dẫn :ref:`doc_making_plugins` để thiết lập plugin mới.

Giả sử bạn đã đặt tên cho thư mục plugin là ``my_inspector_plugin``. Nếu vậy, bạn sẽ có một thư mục ``addons/my_inspector_plugin`` mới chứa hai tệp: ``plugin.cfg`` và ``plugin.gd``.

Như trước đây, ``plugin.gd`` là một script kế thừa :ref:`class_EditorPlugin` và bạn cần thêm mã mới cho các phương thức ``_enter_tree`` và ``_exit_tree`` của nó. Để thiết lập plugin Inspector, bạn phải tải script, sau đó tạo và thêm instance bằng cách gọi ``add_inspector_plugin()``. Nếu plugin bị vô hiệu hóa, bạn nên xóa instance đã thêm bằng cách gọi ``remove_inspector_plugin()``.

.. note:: Ở đây, bạn đang tải một script chứ không phải một scene đã đóng gói. Vì vậy, bạn nên dùng ``new()`` thay cho ``instantiate()``.

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

Để tương tác với dock Inspector, script ``my_inspector_plugin.gd`` của bạn phải kế thừa lớp :ref:`class_EditorInspectorPlugin`. Lớp này cung cấp một số phương thức ảo ảnh hưởng đến cách Inspector xử lý các thuộc tính.

Để script thực sự có tác dụng, script phải triển khai phương thức ``_can_handle()``. Hàm này được gọi cho từng :ref:`class_Object` đang được chỉnh sửa và phải trả về ``true`` nếu plugin này nên xử lý đối tượng hoặc các thuộc tính của đối tượng.

.. note:: Điều này bao gồm mọi :ref:`class_Resource` được gắn vào đối tượng.

Bạn có thể triển khai thêm bốn phương thức để thêm control vào Inspector ở các vị trí cụ thể. Các phương thức ``_parse_begin()`` và ``_parse_end()`` lần lượt chỉ được gọi một lần ở đầu và cuối quá trình phân tích cú pháp cho mỗi đối tượng. Chúng có thể thêm control ở đầu hoặc cuối bố cục Inspector bằng cách gọi ``add_custom_control()``.

Khi editor phân tích đối tượng, nó gọi các phương thức ``_parse_category()`` và ``_parse_property()``. Tại đó, ngoài ``add_custom_control()``, bạn có thể gọi cả ``add_property_editor()`` và ``add_property_editor_for_multiple_properties()``. Dùng hai phương thức sau để thêm riêng các control dựa trên :ref:`class_EditorProperty`.

.. tabs::
 .. code-tab:: gdscript GDScript

    # my_inspector_plugin.gd
    @tool
    extends EditorInspectorPlugin

    var RandomIntEditor = preload("res://addons/my_inspector_plugin/random_int_editor.gd")


    func _can_handle(object):
        # Trong ví dụ này, chúng ta hỗ trợ mọi đối tượng.
        return true


    func _parse_property(object, type, name, hint_type, hint_string, usage_flags, wide):
        # Chúng ta xử lý các thuộc tính kiểu integer.
        if type == TYPE_INT:
            # Tạo một instance của trình chỉnh sửa thuộc tính tùy chỉnh và đăng ký
            # nó với một đường dẫn thuộc tính cụ thể.
            add_property_editor(name, RandomIntEditor.new())
            # Thông báo cho editor xóa trình chỉnh sửa thuộc tính mặc định đối với
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
            // Trong ví dụ này, chúng ta hỗ trợ mọi đối tượng.
            return true;
        }

        public override bool _ParseProperty(GodotObject @object, Variant.Type type,
            string name, PropertyHint hintType, string hintString,
            PropertyUsageFlags usageFlags, bool wide)
        {
            // Chúng ta xử lý các thuộc tính kiểu integer.
            if (type == Variant.Type.Int)
            {
                // Tạo một instance của trình chỉnh sửa thuộc tính tùy chỉnh và đăng ký
                // nó với một đường dẫn thuộc tính cụ thể.
                AddPropertyEditor(name, new RandomIntEditor());
                // Thông báo cho editor xóa trình chỉnh sửa thuộc tính mặc định đối với
                // kiểu thuộc tính này.
                return true;
            }

            return false;
        }
    }
    #endif

Thêm giao diện để chỉnh sửa thuộc tính
--------------------------------------

Lớp :ref:`class_EditorProperty` là một kiểu :ref:`class_Control` đặc biệt có thể tương tác với các đối tượng đang được chỉnh sửa trong dock Inspector. Nó không hiển thị gì nhưng có thể chứa bất kỳ node control nào khác, kể cả các scene phức tạp.

Script kế thừa có ba phần thiết yếu
:ref:`class_EditorProperty`:

1. Bạn phải định nghĩa phương thức ``_init()`` để thiết lập cấu trúc của các node control.

2. Bạn nên triển khai ``_update_property()`` để xử lý các thay đổi dữ liệu từ bên ngoài.

3. Tại một thời điểm nào đó, phải phát ra một signal để thông báo cho Inspector rằng control đã thay đổi thuộc tính bằng ``emit_changed``.

Bạn có thể hiển thị widget tùy chỉnh theo hai cách. Chỉ dùng phương thức ``add_child()`` mặc định để hiển thị widget ở bên phải tên thuộc tính, hoặc dùng ``add_child()`` theo sau là ``set_bottom_editor()`` để đặt widget bên dưới tên.

.. FIXME: The second tab has the C# lexer for highlighting disabled for now, as the provided code causes errors.

.. tabs::
 .. code-tab:: gdscript GDScript

    # random_int_editor.gd
    @tool
    extends EditorProperty


    # Control chính dùng để chỉnh sửa thuộc tính.
    var property_control = Button.new()
    # Giá trị nội bộ của thuộc tính.
    var current_value = 0
    # Cờ bảo vệ chống lại các thay đổi nội bộ khi thuộc tính được cập nhật.
    var updating = false


    func _init():
        # Thêm control làm node con trực tiếp của node EditorProperty.
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

        # Tạo một số nguyên ngẫu nhiên mới trong khoảng từ 0 đến 99.
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
        // Ngăn các thay đổi nội bộ khi thuộc tính được cập nhật.
        private bool _updating = false;

        public RandomIntEditor()
        {
            // Thêm control làm node con trực tiếp của node EditorProperty.
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

            // Tạo một số nguyên ngẫu nhiên mới trong khoảng từ 0 đến 99.
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

Dựa trên mã ví dụ ở trên, bạn sẽ có thể tạo một widget tùy chỉnh thay thế control :ref:`class_SpinBox` mặc định cho số nguyên bằng một
:ref:`class_Button` tạo ra các giá trị ngẫu nhiên.
