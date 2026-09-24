.. _doc_handling_quit_requests:

Xử lý yêu cầu thoát
===================

Thoát
-----

Hầu hết các nền tảng đều có tùy chọn yêu cầu ứng dụng thoát. Trên máy tính để bàn, thao tác này thường được thực hiện bằng biểu tượng "x" trên thanh tiêu đề của cửa sổ. Trên thiết bị di động, ứng dụng có thể thoát bất kỳ lúc nào khi bị tạm dừng và chuyển xuống nền.

Xử lý thông báo
---------------

Trên các nền tảng máy tính để bàn và web, :ref:`Node <class_Node>` sẽ nhận được một thông báo ``NOTIFICATION_WM_CLOSE_REQUEST`` đặc biệt khi trình quản lý cửa sổ yêu cầu thoát.

Việc xử lý thông báo được thực hiện như sau (trên bất kỳ node nào):

.. tabs::
 .. code-tab:: gdscript GDScript

    func _notification(what):
        if what == NOTIFICATION_WM_CLOSE_REQUEST:
            get_tree().quit() # hành vi mặc định

 .. code-tab:: csharp

    public override void _Notification(int what)
    {
        if (what == NotificationWMCloseRequest)
        {
            GetTree().Quit(); // hành vi mặc định
        }
    }

Điều quan trọng cần lưu ý là theo mặc định, các ứng dụng Godot có hành vi tích hợp là thoát khi trình quản lý cửa sổ yêu cầu thoát. Bạn có thể thay đổi điều này để người dùng tự xử lý toàn bộ quy trình thoát:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().set_auto_accept_quit(false)

 .. code-tab:: csharp

    GetTree().AutoAcceptQuit = false;

Trên thiết bị di động
---------------------

Trên các nền tảng di động không có tương đương trực tiếp với ``NOTIFICATION_WM_CLOSE_REQUEST``. Do đặc điểm của các hệ điều hành di động, nơi duy nhất bạn có thể chạy mã trước khi thoát là khi ứng dụng được tạm dừng và chuyển xuống nền. Trên cả Android và iOS, ứng dụng có thể bị người dùng hoặc hệ điều hành kết thúc bất kỳ lúc nào trong khi đang tạm dừng. Một cách chuẩn bị trước cho khả năng này là sử dụng ``NOTIFICATION_APPLICATION_PAUSED`` để thực hiện mọi hành động cần thiết khi ứng dụng đang được tạm dừng.

.. note:: Trên iOS, bạn chỉ có khoảng 5 giây để hoàn tất một tác vụ được bắt đầu bởi signal này. Nếu vượt quá khoảng thời gian đó, iOS sẽ kết thúc ứng dụng thay vì tạm dừng ứng dụng.

Trên Android, nhấn nút Back sẽ thoát ứng dụng nếu **Application > Config > Quit On Go Back** được chọn trong Project Settings (đây là thiết lập mặc định). Thao tác này sẽ kích hoạt ``NOTIFICATION_WM_GO_BACK_REQUEST``.


Gửi thông báo thoát của riêng bạn
---------------------------------

Bạn có thể buộc ứng dụng đóng bằng cách gọi
:ref:`SceneTree.quit <class_SceneTree_method_quit>`, nhưng thao tác này sẽ không gửi ``NOTIFICATION_WM_CLOSE_REQUEST`` đến các node trong scene tree. Việc thoát bằng cách gọi :ref:`SceneTree.quit <class_SceneTree_method_quit>` sẽ không cho phép các hành động tùy chỉnh hoàn tất (chẳng hạn như lưu, xác nhận thoát hoặc debug), ngay cả khi bạn cố trì hoãn dòng lệnh buộc thoát.

Thay vào đó, nếu muốn thông báo cho các node trong scene tree về việc chương trình sắp kết thúc, bạn nên tự gửi thông báo:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().root.propagate_notification(NOTIFICATION_WM_CLOSE_REQUEST)

 .. code-tab:: csharp

    GetTree().Root.PropagateNotification((int)NotificationWMCloseRequest);

Việc gửi thông báo này sẽ thông báo cho tất cả các node về việc chương trình kết thúc, nhưng sẽ không tự kết thúc chương trình *không giống như trong 3.X*. Để đạt được hành vi trước đây, cần gọi :ref:`SceneTree.quit <class_SceneTree_method_quit>` sau thông báo.
