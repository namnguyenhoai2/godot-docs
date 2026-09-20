.. _doc_custom_performance_monitors:

Trình giám sát hiệu năng tùy chỉnh
==================================

Giới thiệu
----------

Như đã giải thích trong tài liệu :ref:`doc_debugger_panel`, Godot cung cấp một panel bên dưới **Debugger > Monitors**, cho phép theo dõi nhiều giá trị khác nhau bằng các biểu đồ thể hiện sự thay đổi của chúng theo thời gian. Dữ liệu cho các biểu đồ này được lấy từ singleton :ref:`class_Performance` của engine.

Godot cho phép bạn khai báo các giá trị tùy chỉnh để hiển thị trong tab Monitors. Một số trường hợp sử dụng trình giám sát hiệu năng tùy chỉnh gồm:

- Hiển thị các chỉ số hiệu năng cụ thể cho dự án của bạn. Ví dụ, trong một game voxel, bạn có thể tạo một trình giám sát hiệu năng để theo dõi số chunk được tải mỗi giây. - Hiển thị các chỉ số trong game không liên quan trực tiếp đến hiệu năng nhưng vẫn hữu ích khi biểu diễn trên biểu đồ cho mục đích debug. Ví dụ, bạn có thể theo dõi số kẻ địch hiện diện trong game để đảm bảo cơ chế spawn hoạt động như mong muốn.

Tạo trình giám sát hiệu năng tùy chỉnh
--------------------------------------

Trong ví dụ này, chúng ta sẽ tạo một trình giám sát hiệu năng tùy chỉnh để theo dõi số kẻ địch hiện diện trong project đang chạy.

Scene chính có một node :ref:`class_Timer` với script sau được gắn vào:

::

    extends Timer


    func _ready():
        # Dấu phân cách slash được dùng để xác định category của monitor.
        # Nếu tên monitor không có slash, category "Custom" chung
        # sẽ được sử dụng thay thế.
        Performance.add_custom_monitor("game/enemies", get_enemy_count)
        timeout.connect(_on_timeout)
        # Spawn 20 kẻ địch mỗi giây.
        wait_time = 0.05
        start()


    func _on_timeout():
        var enemy = preload("res://enemy.tscn").instantiate()
        get_parent().add_child(enemy)


    # Hàm này được gọi mỗi khi performance monitor được truy vấn
    # (việc này xảy ra một lần mỗi giây trong editor, hoặc nhiều hơn nếu được gọi thủ công).
    # Hàm phải trả về một số lớn hơn hoặc bằng 0 (int hoặc float).
    func get_enemy_count():
        return get_tree().get_nodes_in_group("enemies").size()


Tham số thứ hai của
:ref:`Performance.add_custom_monitor<class_Performance_method_add_custom_monitor>`
là một :ref:`class_Callable`.

``enemy.tscn`` là một scene có node gốc Node2D và node con Timer. Node2D có script sau được gắn vào:

::

    extends Node2D


    func _ready():
        add_to_group("enemies")
        $Timer.timeout.connect(_on_timer_timeout)
        # Despawn kẻ địch 2,5 giây sau khi chúng spawn.
        $Timer.wait_time = 2.5
        $Timer.start()


    func _on_timer_timeout():
        queue_free()

Trong ví dụ này, vì chúng ta spawn 20 kẻ địch mỗi giây và mỗi kẻ địch despawn 2,5 giây sau khi spawn, chúng ta kỳ vọng số kẻ địch hiện diện trong scene sẽ ổn định ở mức 50. Chúng ta có thể xác nhận điều này bằng cách xem biểu đồ.

Để trực quan hóa biểu đồ được tạo từ performance monitor tùy chỉnh này, hãy chạy project, chuyển sang editor trong khi project đang chạy và mở **Debugger > Monitors** ở cuối cửa sổ editor. Cuộn xuống phần **Game** mới xuất hiện và chọn **Enemies**. Bạn sẽ thấy một biểu đồ xuất hiện như sau:

.. figure:: img/custom_performance_monitors_graph_example.webp
   :align: center
   :alt: Example editor graph from a custom performance monitor

   Example editor graph from a custom performance monitor

.. note::

    Code xử lý performance monitor không nhất thiết phải nằm trong cùng script với các node. Thay vào đó, bạn có thể chuyển phần đăng ký performance monitor và hàm getter sang một :ref:`autoload <doc_singletons_autoload>`.

Truy vấn performance monitor trong một project
----------------------------------------------

Nếu muốn hiển thị giá trị của performance monitor trong cửa sổ của project đang chạy (thay vì trong editor), hãy dùng ``Performance.get_custom_monitor("category/name")`` để lấy giá trị của monitor tùy chỉnh. Bạn có thể hiển thị giá trị bằng :ref:`class_Label`,
:ref:`class_RichTextLabel`, :ref:`doc_custom_drawing_in_2d`, :ref:`doc_3d_text`,
v.v.

Phương thức này cũng có thể được sử dụng trong các project đã export (ở chế độ debug và release), cho phép bạn tạo các hình ảnh trực quan bên ngoài editor.
