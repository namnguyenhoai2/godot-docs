.. _doc_singletons_autoload:

Singleton (Autoload)
====================

Giới thiệu
----------

Hệ thống scene của Godot tuy mạnh mẽ và linh hoạt nhưng có một hạn chế: không có phương thức nào để lưu trữ thông tin (ví dụ: điểm số hoặc vật phẩm của người chơi) cần dùng trong nhiều scene.

Có thể giải quyết vấn đề này bằng một số cách khắc phục, nhưng chúng cũng có những hạn chế riêng:

-  Bạn có thể sử dụng một scene "chính" để tải và dỡ các scene khác dưới dạng các scene con. Tuy nhiên, điều này có nghĩa là bạn không thể chạy riêng các scene đó và mong chúng hoạt động chính xác.
-  Thông tin có thể được lưu vào đĩa trong ``user://`` rồi được các scene cần thông tin đó tải lên, nhưng việc thường xuyên lưu và tải dữ liệu khá bất tiện và có thể chậm.

Mẫu `Singleton <https://en.wikipedia.org/wiki/Singleton_pattern>`_ là một công cụ hữu ích để giải quyết trường hợp phổ biến khi bạn cần lưu trữ thông tin bền vững giữa các scene. Trong trường hợp của chúng ta, có thể tái sử dụng cùng một scene hoặc class cho nhiều singleton, miễn là chúng có tên khác nhau.

Dựa trên khái niệm này, bạn có thể tạo các đối tượng:

- Luôn được tải, bất kể scene nào hiện đang chạy.
- Có thể lưu trữ các biến toàn cục như thông tin người chơi.
- Có thể xử lý việc chuyển scene và các quá trình chuyển tiếp giữa các scene.
- *Hoạt động* như một singleton, vì GDScript không hỗ trợ biến toàn cục theo thiết kế.

Việc autoload node và script có thể cung cấp cho chúng ta những đặc điểm này.

.. note::

    Godot sẽ không biến một Autoload thành singleton "thực sự" theo mẫu thiết kế singleton. Người dùng vẫn có thể tạo nhiều instance của nó nếu muốn.

.. tip::

    Nếu bạn tạo một autoload trong một editor plugin, hãy cân nhắc
    :ref:`tự động đăng ký nó trong Project Settings <doc_making_plugins_autoload>` khi plugin được bật.

Autoload
--------

Bạn có thể tạo một Autoload để tải một scene hoặc một script kế thừa từ
:ref:`class_Node`.

.. note::

    Khi autoload một script, một :ref:`class_Node` sẽ được tạo và script sẽ được gắn vào đó. Node này sẽ được thêm vào viewport gốc trước khi bất kỳ scene nào khác được tải.

.. image:: img/singleton.webp

Để autoload một scene hoặc script, bắt đầu từ menu và điều hướng đến **Project > Project Settings > Globals > Autoload**.

.. image:: img/autoload_tab.webp

Tại đây, bạn có thể thêm bất kỳ số lượng scene hoặc script nào. Mỗi mục trong danh sách yêu cầu một tên, được gán làm thuộc tính ``name`` của node. Có thể điều chỉnh thứ tự các mục khi chúng được thêm vào scene tree toàn cục bằng các phím mũi tên lên/xuống. Giống như các scene thông thường, engine sẽ đọc các node này theo thứ tự từ trên xuống dưới.

.. image:: img/autoload_example.webp

Nếu cột **Enable** được chọn (mặc định là vậy), singleton có thể được truy cập trực tiếp trong GDScript:

.. tabs::
 .. code-tab:: gdscript GDScript

   PlayerVariables.health -= 10

Cột **Enable** không có tác dụng trong mã C#. Tuy nhiên, nếu singleton là một C# script, có thể đạt được hiệu ứng tương tự bằng cách thêm một static property có tên ``Instance`` và gán giá trị cho nó trong ``_Ready()``:

.. tabs::
 .. code-tab:: csharp

    public partial class PlayerVariables : Node
    {
        public static PlayerVariables Instance { get; private set; }

        public int Health { get; set; }

        public override void _Ready()
        {
            Instance = this;
        }
    }

Điều này cho phép truy cập singleton từ mã C# mà không cần ``GetNode()`` và không cần typecast:

.. tabs::
 .. code-tab:: csharp

    PlayerVariables.Instance.Health -= 10;

Lưu ý rằng các đối tượng autoload (script và/hoặc scene) được truy cập giống như bất kỳ node nào khác trong scene tree. Thực tế, nếu xem scene tree đang chạy, bạn sẽ thấy các node đã được autoload xuất hiện:

.. image:: img/autoload_runtime.webp

.. warning::

    Tuyệt đối **không** được xóa các đối tượng autoload bằng ``free()`` hoặc ``queue_free()`` trong runtime, nếu không engine sẽ bị crash.

Scene switcher tùy chỉnh
------------------------

Tutorial này sẽ hướng dẫn xây dựng một scene switcher bằng autoload. Để chuyển scene cơ bản, bạn có thể sử dụng
phương thức :ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` (xem :ref:`doc_scene_tree` để biết chi tiết). Tuy nhiên, nếu cần hành vi phức tạp hơn khi thay đổi scene, phương thức này cung cấp nhiều chức năng hơn.

Để bắt đầu, hãy tải template từ đây: `singleton_autoload_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/singleton_autoload_starter.zip>`_ và mở nó trong Godot.

Một cửa sổ thông báo rằng project được mở lần cuối bằng phiên bản Godot cũ hơn có thể xuất hiện; điều đó không thành vấn đề. Nhấp vào *Ok* để mở project.

Project chứa hai scene: ``scene_1.tscn`` và ``scene_2.tscn``. Mỗi scene chứa một label hiển thị tên scene và một button đã kết nối signal ``pressed()`` của nó. Khi chạy project, project bắt đầu trong ``scene_1.tscn``. Tuy nhiên, nhấn button không thực hiện điều gì.

Tạo script
~~~~~~~~~~

Mở cửa sổ **Script** và tạo một script mới có tên ``global.gd``. Đảm bảo script kế thừa từ ``Node``:

.. image:: img/autoload_script.webp

Bước tiếp theo là thêm script này vào danh sách autoload. Từ menu, mở **Project > Project Settings > Globals > Autoload** và chọn script bằng cách nhấp vào nút browse hoặc nhập đường dẫn của nó: ``res://global.gd``. Nhấn **Add** để thêm script vào danh sách autoload và đặt tên là "Global", tên bắt buộc để các script có thể truy cập nó bằng tên "Global":

.. image:: img/autoload_tutorial1.webp

Bây giờ, bất cứ khi nào chạy một scene trong project, script này sẽ luôn được tải.

Quay lại script, script cần lấy scene hiện tại trong hàm `_ready()`. Cả scene hiện tại (scene có button) và ``global.gd`` đều là các node con của root, nhưng các node autoload luôn đứng trước. Điều này có nghĩa là node con cuối cùng của root luôn là scene đã được tải.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node

    var current_scene = null

    func _ready():
        var root = get_tree().root
        # Dùng index âm sẽ đếm từ cuối, vì vậy câu lệnh này lấy node con cuối cùng của `root`.
        current_scene = root.get_child(-1)

 .. code-tab:: csharp

    using Godot;

    public partial class Global : Node
    {
        public Node CurrentScene { get; set; }

        public override void _Ready()
        {
            Viewport root = GetTree().Root;
            // Dùng index âm sẽ đếm từ cuối, vì vậy câu lệnh này lấy node con cuối cùng của `root`.
            CurrentScene = root.GetChild(-1);
        }
    }

Bây giờ chúng ta cần một hàm để thay đổi scene. Hàm này cần giải phóng scene hiện tại và thay thế nó bằng scene được yêu cầu.

.. tabs::
 .. code-tab:: gdscript GDScript

    func goto_scene(path):
        # Hàm này thường được gọi từ một signal callback,
        # hoặc một hàm khác trong scene hiện tại.
        # Xóa scene hiện tại tại thời điểm này là
        # một ý tưởng tồi, vì scene đó có thể vẫn đang thực thi mã.
        # Điều này sẽ gây ra crash hoặc hành vi không mong muốn.

        # Giải pháp là trì hoãn việc tải đến một thời điểm muộn hơn, khi
        # chúng ta có thể chắc chắn rằng không có mã nào từ scene hiện tại đang chạy:

        _deferred_goto_scene.call_deferred(path)


    func _deferred_goto_scene(path):
        # Bây giờ có thể an toàn xóa scene hiện tại.
        current_scene.free()

        # Tải scene mới.
        var s = ResourceLoader.load(path)

        # Tạo instance của scene mới.
        current_scene = s.instantiate()

        # Thêm scene đó vào scene đang hoạt động, làm node con của root.
        get_tree().root.add_child(current_scene)

        # Tùy chọn, để tương thích với API SceneTree.change_scene_to_file().
        get_tree().current_scene = current_scene

 .. code-tab:: csharp

    public void GotoScene(string path)
    {
        // Hàm này thường được gọi từ một signal callback,
        // hoặc một hàm khác trong scene hiện tại.
        // Xóa scene hiện tại tại thời điểm này là
        // một ý tưởng tồi, vì scene đó có thể vẫn đang thực thi code.
        // Điều này sẽ gây ra crash hoặc hành vi không mong muốn.

        // Giải pháp là trì hoãn việc tải đến thời điểm sau, khi
        // ta có thể chắc chắn rằng không có code nào từ scene hiện tại đang chạy:

        CallDeferred(MethodName.DeferredGotoScene, path);
    }

    public void DeferredGotoScene(string path)
    {
        // Bây giờ có thể an toàn xóa scene hiện tại.
        CurrentScene.Free();

        // Tải scene mới.
        var nextScene = GD.Load<PackedScene>(path);

        // Tạo instance của scene mới.
        CurrentScene = nextScene.Instantiate();

        // Thêm scene đó vào scene đang hoạt động, làm node con của root.
        GetTree().Root.AddChild(CurrentScene);

        // Tùy chọn, để tương thích với API SceneTree.change_scene_to_file().
        GetTree().CurrentScene = CurrentScene;
    }

Với :ref:`Object.call_deferred() <class_Object_method_call_deferred>`, hàm thứ hai sẽ chỉ chạy sau khi toàn bộ code từ scene hiện tại đã hoàn tất. Do đó, scene hiện tại sẽ không bị xóa trong khi vẫn đang được sử dụng (tức là code của scene đó vẫn đang chạy).

Cuối cùng, chúng ta cần điền các hàm callback còn trống trong hai scene:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thêm vào 'scene_1.gd'.

    func _on_button_pressed():
        Global.goto_scene("res://scene_2.tscn")

 .. code-tab:: csharp

    // Thêm vào 'Scene1.cs'.

    private void OnButtonPressed()
    {
        var global = GetNode<Global>("/root/Global");
        global.GotoScene("res://Scene2.tscn");
    }

và

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thêm vào 'scene_2.gd'.

    func _on_button_pressed():
        Global.goto_scene("res://scene_1.tscn")

 .. code-tab:: csharp

    // Thêm vào 'Scene2.cs'.

    private void OnButtonPressed()
    {
        var global = GetNode<Global>("/root/Global");
        global.GotoScene("res://Scene1.tscn");
    }

Chạy project và kiểm tra rằng bạn có thể chuyển đổi giữa các scene bằng cách nhấn nút.

.. note::

    Khi các scene nhỏ, quá trình chuyển đổi diễn ra tức thì. Tuy nhiên, nếu scene của bạn phức tạp hơn, chúng có thể mất một khoảng thời gian đáng kể mới xuất hiện. Để tìm hiểu cách xử lý trường hợp này, hãy xem tutorial tiếp theo: :ref:`doc_background_loading`.

    Ngoài ra, nếu thời gian tải tương đối ngắn (khoảng dưới 3 giây), bạn có thể hiển thị "loading plaque" bằng cách hiển thị một dạng phần tử 2D nào đó ngay trước khi thay đổi scene. Sau đó, bạn có thể ẩn phần tử này ngay sau khi scene được thay đổi. Cách này có thể được dùng để cho người chơi biết rằng một scene đang được tải.

.. _`Singleton pattern`: https://en.wikipedia.org/wiki/Singleton_pattern
.. _`singleton_autoload_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/singleton_autoload_starter.zip
