.. _doc_background_loading:

Tải trong nền
=============

Thông thường, game cần tải tài nguyên một cách bất đồng bộ (asynchronously). Khi chuyển scene chính của game (ví dụ: đi đến một level mới), bạn có thể muốn hiển thị màn hình tải cùng một chỉ báo cho biết tiến trình đang diễn ra, hoặc bạn có thể muốn tải thêm tài nguyên trong khi chơi.

Phương thức tải tiêu chuẩn (:ref:`ResourceLoader.load <class_ResourceLoader_method_load>` hoặc phương thức đơn giản hơn của GDScript
:ref:`load <class_@GDScript_method_load>`) blocks your
thread, khiến game của bạn có vẻ không phản hồi trong khi tài nguyên đang được tải.

Một cách để tránh vấn đề này là sử dụng ``ResourceLoader`` để tải tài nguyên bất đồng bộ trong các background thread.

Sử dụng ResourceLoader
----------------------

Thông thường, bạn xếp hàng các yêu cầu tải tài nguyên cho một đường dẫn bằng cách sử dụng
:ref:`ResourceLoader.load_threaded_request <class_ResourceLoader_method_load_threaded_request>`,
sau đó tài nguyên sẽ được tải trong các thread ở background.

Bạn có thể kiểm tra trạng thái bằng
:ref:`ResourceLoader.load_threaded_get_status <class_ResourceLoader_method_load_threaded_get_status>`.
Có thể lấy tiến trình bằng cách truyền một biến mảng qua progress; biến này sẽ trả về một mảng có một phần tử chứa phần trăm.

Cuối cùng, bạn lấy các tài nguyên đã tải bằng cách gọi
:ref:`ResourceLoader.load_threaded_get <class_ResourceLoader_method_load_threaded_get>`.

Sau khi gọi ``load_threaded_get()``, tài nguyên либо đã tải xong trong background và sẽ được trả về ngay lập tức, либо quá trình tải sẽ bị block tại thời điểm này giống như ``load()``. Nếu muốn đảm bảo thao tác này không bị block, bạn cần đảm bảo có đủ thời gian giữa lúc yêu cầu tải và lúc lấy tài nguyên, hoặc cần tự kiểm tra trạng thái.

Ví dụ
-----

Ví dụ này minh họa cách tải một scene trong background. Chúng ta sẽ cho một button spawn một enemy khi được nhấn. Enemy sẽ là ``Enemy.tscn``, được chúng ta tải bằng ``_ready`` và instantiate khi button được nhấn. Đường dẫn sẽ là ``"Enemy.tscn"``, nằm tại ``res://Enemy.tscn``.

Trước tiên, chúng ta sẽ bắt đầu một yêu cầu tải tài nguyên và kết nối button:

.. tabs::
 .. code-tab:: gdscript

    const ENEMY_SCENE_PATH : String = "Enemy.tscn"

    func _ready():
        ResourceLoader.load_threaded_request(ENEMY_SCENE_PATH)
        self.pressed.connect(_on_button_pressed)

 .. code-tab:: csharp

    using Godot;

    public partial class MyButton : Button
    {
        private const string EnemyScenePath = "Enemy.tscn";

        public override void _Ready()
        {
            ResourceLoader.LoadThreadedRequest(EnemyScenePath);
            Pressed += OnButtonPressed;
        }
    }

Bây giờ ``_on_button_pressed`` sẽ được gọi khi button được nhấn. Phương thức này sẽ được dùng để spawn một enemy.

.. tabs::
 .. code-tab:: gdscript

    func _on_button_pressed(): # Button đã được nhấn.
        # Lấy tài nguyên vì bây giờ chúng ta cần đến nó.
        var enemy_scene = ResourceLoader.load_threaded_get(ENEMY_SCENE_PATH)
        # Instantiate scene enemy và thêm nó vào scene hiện tại.
        var enemy = enemy_scene.instantiate()
        add_child(enemy)

 .. code-tab:: csharp

    private void OnButtonPressed() // Button đã được nhấn.
    {
        // Lấy tài nguyên vì bây giờ chúng ta cần đến nó.
        var enemyScene = (PackedScene)ResourceLoader.LoadThreadedGet(EnemyScenePath);
        // Instantiate scene enemy và thêm nó vào scene hiện tại.
        var enemy = enemyScene.Instantiate();
        AddChild(enemy);
    }
