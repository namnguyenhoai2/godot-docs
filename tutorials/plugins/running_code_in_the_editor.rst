.. _doc_running_code_in_the_editor:

Chạy mã trong editor
====================

``@tool`` là gì?
----------------

``@tool`` là một dòng mã mạnh mẽ mà khi được thêm vào đầu script, sẽ khiến script thực thi trong editor. Bạn cũng có thể quyết định phần nào của script thực thi trong editor, phần nào thực thi trong game và phần nào thực thi trong cả hai.

Bạn có thể dùng nó để thực hiện nhiều việc, nhưng nó chủ yếu hữu ích trong thiết kế level để hiển thị trực quan những thứ khó dự đoán. Dưới đây là một số trường hợp sử dụng:

- Nếu bạn có một khẩu pháo bắn ra những viên đạn chịu tác động của physics (trọng lực), bạn có thể vẽ quỹ đạo của viên đạn trong editor, giúp việc thiết kế level dễ dàng hơn nhiều. - Nếu bạn có các jumppad với độ cao nhảy khác nhau, bạn có thể vẽ độ cao nhảy tối đa mà người chơi sẽ đạt được nếu nhảy lên một jumppad, cũng giúp việc thiết kế level dễ dàng hơn. - Nếu người chơi của bạn không sử dụng sprite mà tự vẽ bằng code, bạn có thể cho code vẽ đó thực thi trong editor để xem người chơi của mình.

.. danger::

    Các script ``@tool`` chạy bên trong editor và cho phép bạn truy cập scene tree của scene hiện đang được chỉnh sửa. Đây là một tính năng mạnh mẽ nhưng cũng đi kèm một số lưu ý, vì editor không có cơ chế bảo vệ trước việc sử dụng sai mục đích các script ``@tool``. Hãy **cực kỳ** thận trọng khi thao tác với scene tree, đặc biệt là thông qua
    :ref:`Node.queue_free<class_Node_method_queue_free>`, as it can cause
    sẽ gây crash nếu bạn giải phóng một node trong khi editor đang chạy logic liên quan đến node đó.

Cách sử dụng ``@tool``
----------------------

Để biến một script thành tool, hãy thêm annotation ``@tool`` ở đầu code.

Để kiểm tra xem bạn hiện có đang ở trong editor hay không, hãy sử dụng: ``Engine.is_editor_hint()``.

Ví dụ, nếu bạn muốn chỉ thực thi một đoạn code trong editor, hãy sử dụng:

.. tabs::
 .. code-tab:: gdscript GDScript

    if Engine.is_editor_hint():
        # Code thực thi khi ở trong editor.

 .. code-tab:: csharp

    if (Engine.IsEditorHint())
    {
        // Code thực thi khi ở trong editor.
    }

Ngược lại, nếu bạn muốn chỉ thực thi code trong game, chỉ cần phủ định cùng câu lệnh đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    if not Engine.is_editor_hint():
        # Code thực thi khi ở trong game.

 .. code-tab:: csharp

    if (!Engine.IsEditorHint())
    {
        // Code thực thi khi ở trong game.
    }

Các đoạn code không có một trong 2 điều kiện trên sẽ chạy cả trong editor lẫn trong game.

Sau đây là hình dạng của một hàm ``_process()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        if Engine.is_editor_hint():
            # Code thực thi trong editor.

        if not Engine.is_editor_hint():
            # Code thực thi trong game.

        # Code thực thi cả trong editor và trong game.

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        if (Engine.IsEditorHint())
        {
            // Code thực thi trong editor.
        }

        if (!Engine.IsEditorHint())
        {
            // Code thực thi trong game.
        }

        // Code thực thi cả trong editor và trong game.
    }

.. _doc_running_code_in_the_editor_important_information:

Thông tin quan trọng
--------------------

Quy tắc chung là **bất kỳ GDScript nào khác mà tool script của bạn sử dụng cũng *phải* là tool**. Editor không thể tạo các instance từ những file GDScript không có ``@tool``, nghĩa là nếu không có nó, bạn không thể gọi các method hoặc tham chiếu đến member variable từ những file đó. Tuy nhiên, vì có thể sử dụng static method, constant và enum mà không cần tạo instance, bạn có thể gọi chúng hoặc tham chiếu đến chúng từ một script ``@tool`` sang các script không phải tool khác. Một ngoại lệ là :ref:`static variables <doc_gdscript_basics_static_variables>`. Nếu bạn cố đọc giá trị của một static variable trong một script không có ``@tool``, nó sẽ luôn trả về ``null`` nhưng sẽ không in ra cảnh báo hoặc lỗi khi làm vậy. Hạn chế này không áp dụng cho static method, vốn có thể được gọi bất kể script đích có đang ở tool mode hay không.

Việc kế thừa một script ``@tool`` không tự động biến script kế thừa thành một ``@tool``. Bỏ qua ``@tool`` trong script kế thừa sẽ vô hiệu hóa hành vi tool từ super class. Vì vậy, script kế thừa cũng nên chỉ định annotation ``@tool``.

Các thay đổi trong editor là vĩnh viễn và không thể undo/redo. Ví dụ, trong phần tiếp theo khi chúng ta xóa script, node sẽ vẫn giữ rotation của nó. Hãy cẩn thận để tránh tạo ra những thay đổi không mong muốn. Hãy cân nhắc thiết lập
:ref:`version control <doc_version_control_systems>` to avoid losing work in
trong trường hợp bạn mắc lỗi.

Debugging
---------

Mặc dù debugger và breakpoint không thể được sử dụng trực tiếp với tool script, bạn vẫn có thể khởi chạy một instance mới của editor và debug từ đó. Để làm vậy, đi đến **Debug > Customize Run Instances...** và chỉ định `--editor` trong **Main Run Args**.

Xem :ref:`doc_overview_of_debugging_tools` để biết thêm thông tin.

Ngoài ra, bạn có thể dùng các câu lệnh print để hiển thị nội dung của các variable thay thế.


Hãy thử ``@tool``
-----------------

Thêm một node ``Sprite2D`` vào scene và đặt texture thành biểu tượng Godot. Gắn và mở một script, rồi thay đổi nó thành:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends Sprite2D

    func _process(delta):
        rotation += PI * delta

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MySprite : Sprite2D
    {
        public override void _Process(double delta)
        {
            Rotation += Mathf.Pi * (float)delta;
        }
    }

Lưu script và quay lại editor. Bây giờ bạn sẽ thấy object của mình xoay. Nếu chạy game, nó cũng sẽ xoay.

.. warning::
    Bạn có thể cần khởi động lại editor. Đây là một bug đã biết, xuất hiện trong tất cả các phiên bản Godot 4: `GH-66381 <https://github.com/godotengine/godot/issues/66381>`_.

.. image:: img/rotating_in_editor.gif

.. note::

    Nếu bạn không thấy các thay đổi, hãy reload scene (đóng rồi mở lại).

Bây giờ hãy chọn thời điểm chạy từng đoạn code. Sửa hàm ``_process()`` để có dạng như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        if Engine.is_editor_hint():
            rotation += PI * delta
        else:
            rotation -= PI * delta

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        if (Engine.IsEditorHint())
        {
            Rotation += Mathf.Pi * (float)delta;
        }
        else
        {
            Rotation -= Mathf.Pi * (float)delta;
        }
    }

Lưu script. Bây giờ object sẽ xoay theo chiều kim đồng hồ trong editor, nhưng nếu chạy game, nó sẽ xoay ngược chiều kim đồng hồ.

Chỉnh sửa variable
------------------

Thêm và export một variable speed vào script. Để cập nhật speed và đồng thời reset góc rotation, hãy thêm một setter ``set(new_speed)`` được thực thi với input từ inspector. Sửa ``_process()`` để bao gồm rotation speed.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends Sprite2D


    @export var speed = 1:
        # Cập nhật speed và reset rotation.
        set(new_speed):
            speed = new_speed
            rotation = 0


    func _process(delta):
        rotation += PI * delta * speed

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MySprite : Sprite2D
    {
        private float _speed = 1;

        [Export]
        public float Speed
        {
            get => _speed;
            set
            {
                // Cập nhật speed và reset rotation.
                _speed = value;
                Rotation = 0;
            }
        }

        public override void _Process(double delta)
        {
            Rotation += Mathf.Pi * (float)delta * _speed;
        }
    }

.. note::

    Code từ các node khác không chạy trong editor. Quyền truy cập của bạn vào các node khác bị giới hạn. Bạn có thể truy cập tree và các node cùng các property mặc định của chúng, nhưng không thể truy cập user variable. Nếu muốn làm vậy, các node khác cũng phải chạy trong editor.

Nhận thông báo khi array hoặc dictionary thay đổi
-------------------------------------------------

Bạn có thể sử dụng Array hoặc Dictionary làm variable ``@export``. Trong script ``@tool``, bạn có thể phản ứng với mọi thay đổi đối với collection đó bằng cách sử dụng setter. Thông thường, tại runtime, setter như vậy chỉ được gọi khi bạn gán giá trị cho variable, nhưng khi bạn chỉnh sửa Array hoặc Dictionary trong inspector, setter cũng sẽ được gọi.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    class_name MyTool
    extends Node

    @export var my_array = []:
        set(new_array):
            my_array = new_array
            print("My array just changed!")

    @export var my_dictionary = {}:
        set(new_dictionary):
            my_dictionary = new_dictionary
            print("My dictionary just changed!")

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MyTool : Node
    {
        private Array _myArray = new();
        private Dictionary _myDictionary = new();

        [Export]
        public Array MyArray
        {
            get => _myArray;
            set
            {
                _myArray = value;
                GD.Print("My array just changed!");
            }
        }

        [Export]
        public Dictionary MyDictionary
        {
            get => _myDictionary;
            set
            {
                _myDictionary = value;
                GD.Print("My dictionary just changed!");
            }
        }
    }


Nhận thông báo khi resource thay đổi
------------------------------------

Đôi khi bạn muốn tool của mình sử dụng một resource. Tuy nhiên, khi bạn thay đổi một property của resource đó trong editor, method ``set()`` của tool sẽ không được gọi.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    class_name MyTool
    extends Node

    @export var resource: MyResource:
        set(new_resource):
            resource = new_resource
            _on_resource_set()

    # Method này chỉ được gọi khi bạn tạo, xóa hoặc dán một resource.
    # Bạn sẽ không nhận được update khi tinh chỉnh các property của nó.
    func _on_resource_set():
        print("My resource was set!")

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MyTool : Node
    {
        private MyResource _resource;

        [Export]
        public MyResource Resource
        {
            get => _resource;
            set
            {
                _resource = value;
                OnResourceSet();
            }
        }

        // Method này chỉ được gọi khi bạn tạo, xóa hoặc dán một resource.
        // Bạn sẽ không nhận được update khi tinh chỉnh các property của nó.
        private void OnResourceSet()
        {
            GD.Print("My resource was set!");
        }
    }

Để khắc phục vấn đề này, trước tiên bạn phải biến resource của mình thành một tool và yêu cầu nó phát signal ``changed`` mỗi khi một property được thiết lập:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Biến Resource của bạn thành một tool.
    @tool
    class_name MyResource
    extends Resource

    @export var property = 1:
        set(new_setting):
            property = new_setting
            # Phát signal khi property thay đổi.
            changed.emit()

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MyResource : Resource
    {
        private float _property = 1;

        [Export]
        public float Property
        {
            get => _property;
            set
            {
                _property = value;
                // Phát signal khi property thay đổi.
                EmitChanged();
            }
        }
    }

Sau đó, bạn cần kết nối signal khi một resource mới được thiết lập:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    class_name MyTool
    extends Node

    @export var resource: MyResource:
        set(new_resource):
            resource = new_resource
            # Kết nối signal changed ngay khi một resource mới được thêm vào.
            if resource != null:
                resource.changed.connect(_on_resource_changed)

    func _on_resource_changed():
        print("My resource just changed!")

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MyTool : Node
    {
        private MyResource _resource;

        [Export]
        public MyResource Resource
        {
            get => _resource;
            set
            {
                _resource = value;
                // Kết nối signal changed ngay khi một resource mới được thêm vào.
                if (_resource != null)
                {
                    _resource.Changed += OnResourceChanged;
                }
            }
        }

        private void OnResourceChanged()
        {
            GD.Print("My resource just changed!");
        }
    }

Cuối cùng, hãy nhớ ngắt kết nối signal, vì resource cũ đang được sử dụng và bị thay đổi ở nơi khác sẽ gây ra các update không cần thiết.

.. tabs::
 .. code-tab:: gdscript GDScript

    @export var resource: MyResource:
        set(new_resource):
            # Ngắt kết nối signal nếu resource trước đó không phải là null.
            if resource != null:
                resource.changed.disconnect(_on_resource_changed)
            resource = new_resource
            if resource != null:
                resource.changed.connect(_on_resource_changed)

 .. code-tab:: csharp

    [Export]
    public MyResource Resource
    {
        get => _resource;
        set
        {
            // Ngắt kết nối signal nếu resource trước đó không phải là null.
            if (_resource != null)
            {
                _resource.Changed -= OnResourceChanged;
            }
            _resource = value;
            if (_resource != null)
            {
                _resource.Changed += OnResourceChanged;
            }
        }
    }

Báo cáo cảnh báo cấu hình node
------------------------------

Godot sử dụng hệ thống *node configuration warning* để cảnh báo người dùng về các node được cấu hình không đúng. Khi một node chưa được cấu hình chính xác, biểu tượng cảnh báo màu vàng sẽ xuất hiện bên cạnh tên node trong Scene dock. Khi bạn di chuột qua hoặc nhấp vào biểu tượng, một thông báo cảnh báo sẽ bật lên. Bạn có thể sử dụng tính năng này trong các script để giúp bạn và nhóm của mình tránh mắc lỗi khi thiết lập scene.

Khi sử dụng node configuration warning, bất cứ khi nào một giá trị có thể ảnh hưởng đến hoặc loại bỏ cảnh báo thay đổi, bạn cần gọi
:ref:`update_configuration_warnings<class_Node_method_update_configuration_warnings>` .
Theo mặc định, cảnh báo chỉ được cập nhật khi đóng và mở lại scene.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Sử dụng setter để tự động cập nhật node configuration warning.
    @export var title = "":
        set(p_title):
            if p_title != title:
                title = p_title
                update_configuration_warnings()

    @export var description = "":
        set(p_description):
            if p_description != description:
                description = p_description
                update_configuration_warnings()


    func _get_configuration_warnings():
        var warnings = []

        if title == "":
            warnings.append("Please set `title` to a non-empty value.")

        if description.length() >= 100:
            warnings.append("`description` should be less than 100 characters long.")

        # Trả về một array rỗng nghĩa là "không có cảnh báo".
        return warnings

.. _doc_running_code_in_the_editor_editorscript:

Chạy các script một lần bằng EditorScript
-----------------------------------------

Đôi khi, bạn cần chạy code chỉ một lần để tự động hóa một tác vụ cụ thể mà editor không có sẵn. Một số ví dụ có thể là:

- Dùng làm playground cho việc scripting bằng GDScript hoặc C# mà không cần chạy project. Output của ``print()`` được hiển thị trong bảng Output của editor. - Scale tất cả light node trong scene hiện đang được chỉnh sửa, vì bạn nhận thấy level của mình trở nên quá tối hoặc quá sáng sau khi đặt đèn ở vị trí mong muốn. - Thay thế các node đã được copy-paste bằng các scene instance để sau này dễ chỉnh sửa hơn.

Tính năng này có sẵn trong Godot bằng cách kế thừa :ref:`class_EditorScript` trong một script. Cách này cho phép chạy từng script riêng lẻ trong editor mà không cần tạo editor plugin.

Để tạo một EditorScript, hãy nhấp chuột phải vào một thư mục hoặc khoảng trống trong dock FileSystem, sau đó chọn **New > Script...**. Trong hộp thoại tạo script, hãy nhấp vào biểu tượng cây để chọn đối tượng cần kế thừa (hoặc nhập trực tiếp ``EditorScript`` vào trường ở bên trái, nhưng lưu ý rằng trường này phân biệt chữ hoa chữ thường):

.. figure:: img/running_code_in_the_editor_creating_editor_script.webp
   :align: center
   :alt: Creating an editor script in the script editor creation dialog

   Creating an editor script in the script editor creation dialog

Thao tác này sẽ tự động chọn một script template phù hợp với EditorScript, trong đó đã chèn sẵn một phương thức ``_run()``:

.. tabs::
    .. code-tab:: gdscript GDScript

        @tool
        extends EditorScript

        # Được gọi khi script được thực thi (bằng cách sử dụng File -> Run in Script Editor).
        func _run():
            pass

    .. code-tab:: csharp

        using Godot;

        [Tool]
        public partial class MyEditorScript : EditorScript
        {
            // Được gọi khi script được thực thi (nhấp chuột phải vào Script -> Run trong dock FileSystem).
            public override void _Run()
            {
                // ...
            }
        }

Phương thức ``_run()`` này được thực thi khi bạn sử dụng bất kỳ phương pháp nào trong 4 phương pháp có thể dùng để chạy một EditorScript:

- Sử dụng :menu:`File > Run` ở đầu script editor khi EditorScript là tab hiện tại. - Nhấn phím tắt :kbd:`Ctrl + Shift + X` khi EditorScript là tab hiện tại. Phím tắt này chỉ có hiệu lực khi script editor đang được focus. - Nhấp chuột phải vào script trong dock FileSystem và chọn :menu:`Run`. - Thêm một ``class_name <name>`` ở đầu script, mở command palette bằng cách nhấn :kbd:`Ctrl + Shift + P`, rồi nhập tên class để chạy. Mục nhập sẽ được đặt tên theo tên class, với việc tự động viết hoa.

Các script kế thừa EditorScript **phải** là các script ``@tool`` thì mới hoạt động.

.. note::

    EditorScript chỉ có thể được chạy từ Godot script editor. Nếu bạn đang sử dụng external editor, hãy dùng một trong hai phương pháp cuối cùng để chạy script.

.. note::

    Không thể chạy C# EditorScript từ script editor vì trình này chỉ hỗ trợ GDScript. Vui lòng tham khảo các phương pháp thay thế ở trên để chạy C# EditorScript tùy chỉnh.

    Hãy nhớ rằng tool script C# chỉ xuất hiện trong command palette khi được đánh dấu bằng attribute :ref:`GlobalClass <doc_c_sharp_global_classes>`.

.. danger::

    EditorScript không có chức năng undo/redo, vì vậy **hãy nhớ lưu scene trước khi chạy** nếu script được thiết kế để sửa đổi dữ liệu.

Để truy cập các node trong scene hiện đang được chỉnh sửa, hãy sử dụng
:ref:`EditorInterface.get_edited_scene_root() <class_EditorInterface_method_get_edited_scene_root>`
phương thức trả về Node gốc của scene hiện đang được chỉnh sửa. Dưới đây là một ví dụ đệ quy lấy tất cả node trong scene hiện đang được chỉnh sửa và tăng gấp đôi phạm vi của tất cả node OmniLight3D:

.. tabs::
    .. code-tab:: gdscript GDScript

        @tool
        # Nhờ tên class, chúng ta có thể chạy script này bằng cách mở
        # command palette và tìm kiếm "Scale Omni Lights".
        class_name ScaleOmniLights
        extends EditorScript

        func _run():
            for node in EditorInterface.get_edited_scene_root().find_children("", "OmniLight3D"):
                # Không thao tác trên các node con của subscene được instance, vì các thay đổi sẽ bị mất
                # khi tải lại scene.
                # Xem phần "Instancing scenes" bên dưới để biết mô tả về `owner`.
                var is_instanced_subscene_child = node != get_scene() and node.owner != get_scene()
                if not is_instanced_subscene_child:
                    node.omni_range *= 2.0
                    EditorInterface.mark_scene_as_unsaved()

    .. code-tab:: csharp

        using Godot;

        [GlobalClass, Tool]
        // Nhờ attribute GlobalClass, chúng ta có thể chạy script này bằng cách mở
        // command palette và tìm kiếm "Scale Omni Lights".
        public partial class ScaleOmniLights : EditorScript
        {
            public override void _Run()
            {
                var sceneNode = EditorInterface.Singleton.GetEditedSceneRoot();

                foreach (OmniLight3D node in sceneNode.FindChildren("", "OmniLight3D"))
                {
                    // Không thao tác trên các node con của subscene được instance, vì các thay đổi sẽ bị mất
                    // khi tải lại scene.
                    // Xem phần "Instancing scenes" bên dưới để biết mô tả về `owner`.
                    var isInstancedSubsceneChild = node != sceneNode && node.Owner != sceneNode;
                    if (!isInstancedSubsceneChild)
                    {
                        node.OmniRange *= 2.0f;
                        EditorInterface.Singleton.MarkSceneAsUnsaved();
                    }
                }
            }
        }

Trong ví dụ trên, chúng ta cũng gọi
:ref:`EditorScript.mark_scene_as_unsaved() <class_EditorInterface_method_mark_scene_as_unsaved>`
sau bất kỳ sửa đổi nào ảnh hưởng đến trạng thái của scene. Điều này cho phép editor hiển thị scene là "chưa lưu" (tức là có dấu hoa thị bên cạnh tên). Nhờ đó, bạn cũng sẽ nhận được thông báo xác nhận khi cố đóng scene có các thay đổi chưa lưu.

.. tip::

    Bạn có thể thay đổi scene hiện đang được chỉnh sửa ở đầu editor ngay cả khi Script view đang mở. Điều này sẽ ảnh hưởng đến giá trị trả về của
    :ref:`EditorInterface.get_edited_scene_root <class_EditorInterface_method_get_edited_scene_root>`,
    vì vậy hãy đảm bảo bạn đã chọn scene mà mình định lặp qua trước khi chạy script.

Instancing scenes
-----------------

Bạn có thể instance các packed scene theo cách thông thường và thêm chúng vào scene hiện đang mở trong editor. Theo mặc định, các node hoặc scene được thêm bằng
:ref:`Node.add_child(node) <class_Node_method_add_child>` are **not** visible
trong dock Scene tree và **không** được lưu vào ổ đĩa. Nếu muốn node hoặc scene hiển thị trong dock Scene tree và được lưu vào ổ đĩa khi lưu scene, bạn cần đặt thuộc tính :ref:`owner <class_Node_property_owner>` của node con thành root của scene hiện đang được chỉnh sửa.

Nếu bạn đang sử dụng ``@tool``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        var node = Node3D.new()
        add_child(node) # Parent có thể là bất kỳ node nào trong scene

        # Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene tree
        # và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.owner = get_tree().edited_scene_root

 .. code-tab:: csharp

    public override void _Ready()
    {
        var node = new Node3D();
        AddChild(node); // Parent có thể là bất kỳ node nào trong scene

        // Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene tree
        // và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.Owner = GetTree().EditedSceneRoot;
    }

Nếu bạn đang sử dụng :ref:`EditorScript <class_EditorScript>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _run():
        # `parent` có thể là bất kỳ node nào trong scene.
        var parent = get_scene().get_node("Parent")
        var node = Node3D.new()
        parent.add_child(node)

        # Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene tree
        # và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.owner = get_scene()

 .. code-tab:: csharp

    public override void _Run()
    {
        // `parent` có thể là bất kỳ node nào trong scene.
        var parent = GetScene().GetNode("Parent");
        var node = new Node3D();
        parent.AddChild(node);

        // Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene tree
        // và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.Owner = GetScene();
    }

.. note::

    Các thay đổi do tool script và EditorScript thực hiện (chẳng hạn như thêm node hoặc sửa đổi thuộc tính) **không** tự động đánh dấu scene là chưa lưu. Để hiển thị dấu hoa thị ``(*)`` và ngăn mất dữ liệu ngoài ý muốn, hãy gọi
    :ref:`EditorInterface.mark_scene_as_unsaved() <class_EditorInterface_method_mark_scene_as_unsaved>`
    sau khi sửa đổi, hoặc sử dụng :ref:`EditorUndoRedoManager <class_EditorUndoRedoManager>` để hỗ trợ undo.

.. warning::

    Sử dụng ``@tool`` không đúng cách có thể tạo ra nhiều lỗi. Bạn nên viết code theo cách mình muốn trước, rồi chỉ thêm annotation ``@tool`` vào đầu script sau đó. Ngoài ra, hãy đảm bảo tách riêng code chạy trong editor khỏi code chạy trong game. Nhờ vậy, bạn có thể tìm bug dễ dàng hơn.
