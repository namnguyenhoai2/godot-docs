.. _doc_running_code_in_the_editor:

Chạy mã trong editor
====================

``@tool`` là gì?
----------------

``@tool`` là một dòng mã mạnh mẽ; khi được thêm vào đầu script, nó khiến script được thực thi trong editor. Bạn cũng có thể quyết định phần nào của script được thực thi trong editor, phần nào trong game và phần nào trong cả hai.

Bạn có thể dùng nó để thực hiện nhiều việc, nhưng nó chủ yếu hữu ích trong thiết kế level để trực quan hóa những thứ khó tự dự đoán. Sau đây là một số trường hợp sử dụng:

- Nếu bạn có một khẩu pháo bắn ra các viên đạn chịu tác động của vật lý (trọng lực), bạn có thể vẽ quỹ đạo của viên đạn trong editor, giúp việc thiết kế level dễ dàng hơn nhiều.
- Nếu bạn có các jumppad với độ cao nhảy khác nhau, bạn có thể vẽ độ cao tối đa mà người chơi sẽ đạt được khi nhảy lên một jumppad, qua đó cũng giúp việc thiết kế level dễ dàng hơn.
- Nếu người chơi của bạn không sử dụng sprite mà tự vẽ bằng mã, bạn có thể cho mã vẽ đó thực thi trong editor để xem người chơi của mình.

.. danger::

    Các script ``@tool`` chạy bên trong editor và cho phép bạn truy cập scene tree của scene hiện đang được chỉnh sửa. Đây là một tính năng mạnh mẽ nhưng cũng có những hạn chế cần lưu ý, vì editor không có cơ chế bảo vệ khỏi việc sử dụng sai các script ``@tool``. Hãy **cực kỳ** thận trọng khi thao tác với scene tree, đặc biệt là thông qua
    :ref:`Node.queue_free<class_Node_method_queue_free>`, vì việc giải phóng một node trong khi editor đang chạy logic liên quan đến node đó có thể gây crash.

Cách sử dụng ``@tool``
----------------------

Để biến một script thành tool, hãy thêm annotation ``@tool`` ở đầu mã.

Để kiểm tra xem hiện tại bạn có đang ở trong editor hay không, hãy sử dụng: ``Engine.is_editor_hint()``.

Ví dụ, nếu bạn muốn chỉ thực thi một đoạn mã trong editor, hãy sử dụng:

.. tabs::
 .. code-tab:: gdscript GDScript

    if Engine.is_editor_hint():
        # Mã sẽ được thực thi khi ở trong editor.

 .. code-tab:: csharp

    if (Engine.IsEditorHint())
    {
        // Mã sẽ được thực thi khi ở trong editor.
    }

Ngược lại, nếu bạn muốn chỉ thực thi mã trong game, chỉ cần phủ định cùng biểu thức đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    if not Engine.is_editor_hint():
        # Mã sẽ được thực thi khi ở trong game.

 .. code-tab:: csharp

    if (!Engine.IsEditorHint())
    {
        // Mã sẽ được thực thi khi ở trong game.
    }

Các đoạn mã không có một trong 2 điều kiện trên sẽ chạy cả trong editor lẫn trong game.

Sau đây là cách một hàm ``_process()`` có thể trông như thế nào:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        if Engine.is_editor_hint():
            # Mã sẽ được thực thi trong editor.

        if not Engine.is_editor_hint():
            # Mã sẽ được thực thi trong game.

        # Mã sẽ được thực thi cả trong editor và trong game.

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        if (Engine.IsEditorHint())
        {
            // Mã sẽ được thực thi trong editor.
        }

        if (!Engine.IsEditorHint())
        {
            // Mã sẽ được thực thi trong game.
        }

        // Mã sẽ được thực thi cả trong editor và trong game.
    }

.. _doc_running_code_in_the_editor_important_information:

Thông tin quan trọng
--------------------

Quy tắc chung là **mọi GDScript khác mà tool script của bạn sử dụng cũng phải *là* một tool**. Editor không thể tạo các instance từ những tệp GDScript không có ``@tool``, nghĩa là nếu không có điều này, bạn không thể gọi các method hoặc tham chiếu đến các biến thành viên từ chúng. Tuy nhiên, vì có thể sử dụng các static method, hằng số và enum mà không cần tạo instance, nên bạn có thể gọi hoặc tham chiếu đến chúng từ một script ``@tool`` tới các script không phải tool khác. Một ngoại lệ là :ref:`các biến static <doc_gdscript_basics_static_variables>`. Nếu bạn cố đọc giá trị của một biến static trong một script không có ``@tool``, nó sẽ luôn trả về ``null`` nhưng sẽ không in cảnh báo hay lỗi khi thực hiện việc đó. Hạn chế này không áp dụng cho các static method, vốn có thể được gọi bất kể script đích có ở chế độ tool hay không.

Việc mở rộng một script ``@tool`` không tự động biến script mở rộng thành một ``@tool``. Bỏ qua ``@tool`` trong script mở rộng sẽ vô hiệu hóa hành vi tool từ super class. Vì vậy, script mở rộng cũng nên chỉ định annotation ``@tool``.

Các thay đổi trong editor là vĩnh viễn, không thể undo/redo. Ví dụ, trong phần tiếp theo, khi chúng ta xóa script, node sẽ vẫn giữ nguyên góc xoay. Hãy cẩn thận để tránh tạo ra các thay đổi không mong muốn. Hãy cân nhắc thiết lập
:ref:`hệ thống kiểm soát phiên bản <doc_version_control_systems>` để tránh mất công việc trong trường hợp bạn mắc lỗi.

Gỡ lỗi
------

Mặc dù không thể sử dụng trực tiếp debugger và breakpoint với các tool script, bạn vẫn có thể khởi chạy một instance editor mới và gỡ lỗi từ đó. Để thực hiện việc này, hãy đi tới **Debug > Customize Run Instances...** và chỉ định `--editor` trong **Main Run Args**.

Xem :ref:`doc_overview_of_debugging_tools` để biết thêm thông tin.

Ngoài ra, bạn có thể sử dụng các câu lệnh print để hiển thị nội dung của các biến thay thế.


Dùng thử ``@tool``
------------------

Thêm một node ``Sprite2D`` vào scene của bạn và đặt texture thành biểu tượng Godot. Gắn và mở một script, rồi thay đổi script thành như sau:

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

Lưu script và quay lại editor. Bây giờ bạn sẽ thấy đối tượng của mình xoay. Nếu chạy game, nó cũng sẽ xoay.

.. warning::
    Bạn có thể cần khởi động lại editor. Đây là một bug đã biết xuất hiện trong mọi phiên bản Godot 4: `GH-66381 <https://github.com/godotengine/godot/issues/66381>`_.

.. image:: img/rotating_in_editor.gif

.. note::

    Nếu không thấy các thay đổi, hãy tải lại scene (đóng scene rồi mở lại).

Bây giờ hãy chọn đoạn mã nào sẽ chạy và chạy khi nào. Sửa đổi hàm ``_process()`` để có dạng như sau:

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

Lưu script. Bây giờ đối tượng sẽ xoay theo chiều kim đồng hồ trong editor, nhưng nếu chạy game, nó sẽ xoay ngược chiều kim đồng hồ.

Chỉnh sửa biến
--------------

Thêm và export một biến speed vào script. Để cập nhật speed và đồng thời đặt lại góc xoay, hãy thêm một setter ``set(new_speed)`` được thực thi với đầu vào từ inspector. Sửa đổi ``_process()`` để bao gồm tốc độ xoay.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends Sprite2D


    @export var speed = 1:
        # Cập nhật speed và đặt lại góc xoay.
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
                // Cập nhật speed và đặt lại góc xoay.
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

    Mã từ các node khác không chạy trong editor. Quyền truy cập của bạn vào các node khác bị giới hạn. Bạn có thể truy cập tree và các node cùng các thuộc tính mặc định của chúng, nhưng không thể truy cập các biến do người dùng định nghĩa. Nếu muốn làm vậy, các node khác cũng phải chạy trong editor.

Nhận thông báo khi các mảng hoặc dictionary thay đổi
----------------------------------------------------

Bạn có thể sử dụng Array hoặc Dictionary làm biến ``@export``. Trong script ``@tool``, bạn có thể phản hồi mọi thay đổi đối với collection đó bằng setter. Thông thường, trong runtime, setter như vậy chỉ được gọi khi bạn gán giá trị cho biến, nhưng khi bạn chỉnh sửa Array hoặc Dictionary trong inspector, setter cũng sẽ được gọi.

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

Đôi khi bạn muốn tool của mình sử dụng một resource. Tuy nhiên, khi bạn thay đổi một property của resource đó trong editor, phương thức ``set()`` của tool sẽ không được gọi.

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    class_name MyTool
    extends Node

    @export var resource: MyResource:
        set(new_resource):
            resource = new_resource
            _on_resource_set()

    # Chỉ được gọi khi bạn tạo, xóa hoặc dán một resource.
    # Bạn sẽ không nhận được cập nhật khi điều chỉnh các property của resource đó.
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

        // Chỉ được gọi khi bạn tạo, xóa hoặc dán một resource.
        // Bạn sẽ không nhận được cập nhật khi điều chỉnh các property của resource đó.
        private void OnResourceSet()
        {
            GD.Print("My resource was set!");
        }
    }

Để khắc phục vấn đề này, trước tiên bạn phải biến resource của mình thành một tool và khiến nó phát signal ``changed`` mỗi khi một property được thiết lập:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Biến Resource của bạn thành một tool.
    @tool
    class_name MyResource
    extends Resource

    @export var property = 1:
        set(new_setting):
            property = new_setting
            # Phát một signal khi property được thay đổi.
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
                // Phát một signal khi property được thay đổi.
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

Cuối cùng, hãy nhớ ngắt kết nối signal, vì resource cũ đang được sử dụng và bị thay đổi ở nơi khác sẽ gây ra các cập nhật không cần thiết.

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

Godot sử dụng hệ thống *cảnh báo cấu hình node* để cảnh báo người dùng về các node được cấu hình không đúng. Khi một node chưa được cấu hình chính xác, biểu tượng cảnh báo màu vàng sẽ xuất hiện bên cạnh tên node trong Scene dock. Khi bạn di chuột qua hoặc nhấp vào biểu tượng, một thông báo cảnh báo sẽ bật lên. Bạn có thể sử dụng tính năng này trong script để giúp bạn và nhóm của mình tránh sai sót khi thiết lập scene.

Khi sử dụng cảnh báo cấu hình node, nếu bất kỳ giá trị nào có thể ảnh hưởng đến hoặc loại bỏ cảnh báo thay đổi, bạn cần gọi
:ref:`update_configuration_warnings<class_Node_method_update_configuration_warnings>` . Theo mặc định, cảnh báo chỉ được cập nhật khi đóng rồi mở lại scene.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Dùng setter để tự động cập nhật cảnh báo cấu hình.
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

        # Trả về một mảng rỗng nghĩa là "không có cảnh báo".
        return warnings

.. _doc_running_code_in_the_editor_editorscript:

Chạy các script một lần bằng EditorScript
-----------------------------------------

Đôi khi, bạn cần chạy code chỉ một lần để tự động hóa một tác vụ cụ thể không có sẵn trong editor. Một số ví dụ có thể là:

- Dùng làm playground cho việc scripting bằng GDScript hoặc C# mà không cần chạy project. Kết quả ``print()`` được hiển thị trong bảng Output của editor.
- Scale tất cả light node trong scene hiện đang được chỉnh sửa, khi bạn nhận thấy level trở nên quá tối hoặc quá sáng sau khi đặt các light ở vị trí mong muốn.
- Thay thế các node đã được copy-paste bằng các scene instance để sau này dễ sửa đổi hơn.

Tính năng này có sẵn trong Godot bằng cách kế thừa :ref:`class_EditorScript` trong một script. Cách này cho phép chạy từng script riêng lẻ trong editor mà không cần tạo editor plugin.

Để tạo một EditorScript, nhấp chuột phải vào một thư mục hoặc khoảng trống trong FileSystem dock, sau đó chọn **New > Script...**. Trong hộp thoại tạo script, nhấp vào biểu tượng cây để chọn object cần kế thừa (hoặc nhập trực tiếp ``EditorScript`` vào trường bên trái, nhưng lưu ý rằng trường này phân biệt chữ hoa chữ thường):

.. figure:: img/running_code_in_the_editor_creating_editor_script.webp
   :align: center
   :alt: Tạo editor script trong hộp thoại tạo script của script editor

   Tạo editor script trong hộp thoại tạo script của script editor

Thao tác này sẽ tự động chọn một script template phù hợp với EditorScript, trong đó đã chèn sẵn phương thức ``_run()``:

.. tabs::
    .. code-tab:: gdscript GDScript

        @tool
        extends EditorScript

        # Được gọi khi script được thực thi (bằng cách chọn File -> Run trong Script Editor).
        func _run():
            pass

    .. code-tab:: csharp

        using Godot;

        [Tool]
        public partial class MyEditorScript : EditorScript
        {
            // Được gọi khi script được thực thi (nhấp chuột phải vào Script -> Run trong FileSystem dock).
            public override void _Run()
            {
                // ...
            }
        }

Phương thức ``_run()`` này được thực thi khi bạn sử dụng bất kỳ cách nào trong 4 cách chạy EditorScript:

- Sử dụng :menu:`File > Run` ở đầu script editor khi EditorScript đang là tab hiện tại.
- Nhấn phím tắt :kbd:`Ctrl + Shift + X` khi EditorScript đang là tab hiện tại. Phím tắt này chỉ có hiệu lực khi script editor đang được focus.
- Nhấp chuột phải vào script trong FileSystem dock và chọn :menu:`Run`.
- Thêm ``class_name <name>`` ở đầu script, mở command palette bằng cách nhấn :kbd:`Ctrl + Shift + P`, rồi nhập tên class để chạy class đó. Mục nhập sẽ được đặt tên theo tên class, với việc tự động viết hoa.

Các script kế thừa EditorScript **phải** là các script ``@tool`` thì mới hoạt động.

.. note::

    EditorScript chỉ có thể được chạy từ Godot script editor. Nếu bạn đang sử dụng editor bên ngoài, hãy dùng một trong hai cách cuối để chạy script.

.. note::

    Không thể chạy C# EditorScripts từ trình chỉnh sửa script vì trình này chỉ hỗ trợ GDScript. Vui lòng tham khảo các phương pháp thay thế ở trên để chạy C# EditorScripts tùy chỉnh.

    Lưu ý rằng các tool script C# chỉ xuất hiện trong command palette khi được đánh dấu bằng thuộc tính :ref:`GlobalClass <doc_c_sharp_global_classes>`.

.. danger::

    EditorScripts không có chức năng undo/redo, vì vậy **hãy nhớ lưu scene trước khi chạy một script** nếu script đó được thiết kế để sửa đổi dữ liệu.

Để truy cập các node trong scene hiện đang được chỉnh sửa, hãy sử dụng
:ref:`EditorInterface.get_edited_scene_root() <class_EditorInterface_method_get_edited_scene_root>` method, phương thức này trả về Node gốc của scene hiện đang được chỉnh sửa. Dưới đây là một ví dụ đệ quy lấy tất cả node trong scene hiện đang được chỉnh sửa và tăng gấp đôi phạm vi của tất cả node OmniLight3D:

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
        // Nhờ thuộc tính GlobalClass, chúng ta có thể chạy script này bằng cách mở
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
:ref:`EditorScript.mark_scene_as_unsaved() <class_EditorInterface_method_mark_scene_as_unsaved>` sau mọi sửa đổi ảnh hưởng đến trạng thái của scene. Điều này cho phép editor hiển thị scene là "chưa lưu" (tức là có dấu hoa thị bên cạnh tên). Nhờ đó, bạn cũng nhận được thông báo xác nhận khi cố đóng scene có các thay đổi chưa lưu.

.. tip::

    Bạn có thể thay đổi scene hiện đang được chỉnh sửa ở đầu editor ngay cả khi chế độ xem Script đang mở. Điều này sẽ ảnh hưởng đến giá trị trả về của
    :ref:`EditorInterface.get_edited_scene_root <class_EditorInterface_method_get_edited_scene_root>`, vì vậy hãy đảm bảo đã chọn scene mà bạn định duyệt qua trước khi chạy script.

Instancing scenes
-----------------

Bạn có thể khởi tạo các scene đã đóng gói như bình thường và thêm chúng vào scene hiện đang mở trong editor. Theo mặc định, các node hoặc scene được thêm bằng
:ref:`Node.add_child(node) <class_Node_method_add_child>` sẽ **không** hiển thị trong dock Scene và **không** được lưu vào đĩa. Nếu muốn node hoặc scene hiển thị trong dock Scene và được lưu vào đĩa khi lưu scene, bạn cần đặt thuộc tính :ref:`owner <class_Node_property_owner>` của node con thành root của scene hiện đang được chỉnh sửa.

Nếu bạn đang sử dụng ``@tool``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        var node = Node3D.new()
        add_child(node) # Parent có thể là bất kỳ node nào trong scene

        # Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene
        # và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.owner = get_tree().edited_scene_root

 .. code-tab:: csharp

    public override void _Ready()
    {
        var node = new Node3D();
        AddChild(node); // Parent có thể là bất kỳ node nào trong scene

        // Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene
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

        # Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene
        # và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.owner = get_scene()

 .. code-tab:: csharp

    public override void _Run()
    {
        // `parent` có thể là bất kỳ node nào trong scene.
        var parent = GetScene().GetNode("Parent");
        var node = new Node3D();
        parent.AddChild(node);

        // Dòng bên dưới là bắt buộc để node hiển thị trong dock Scene
        // và lưu các thay đổi do tool script thực hiện vào file scene đã lưu.
        node.Owner = GetScene();
    }

.. note::

    Các thay đổi do tool script và EditorScript thực hiện (chẳng hạn như thêm node hoặc sửa đổi thuộc tính) **không** tự động đánh dấu scene là chưa lưu. Để hiển thị dấu hoa thị ``(*)`` và ngăn mất dữ liệu do thao tác nhầm, hãy gọi
    :ref:`EditorInterface.mark_scene_as_unsaved() <class_EditorInterface_method_mark_scene_as_unsaved>` sau khi sửa đổi hoặc sử dụng :ref:`EditorUndoRedoManager <class_EditorUndoRedoManager>` để hỗ trợ undo.

.. warning::

    Sử dụng ``@tool`` không đúng cách có thể gây ra nhiều lỗi. Bạn nên viết code theo ý muốn trước, rồi mới thêm annotation ``@tool`` vào đầu. Ngoài ra, hãy đảm bảo tách riêng code chạy trong editor khỏi code chạy trong game. Nhờ vậy, bạn có thể tìm lỗi dễ dàng hơn.

.. _`GH-66381`: https://github.com/godotengine/godot/issues/66381
