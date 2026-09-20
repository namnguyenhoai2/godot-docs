.. _doc_handling_quit_requests:

Xử lý yêu cầu thoát
===================

Thoát
-----

Hầu hết các nền tảng đều có tùy chọn yêu cầu ứng dụng thoát. Trên máy tính để bàn, thao tác này thường được thực hiện bằng biểu tượng "x" trên thanh tiêu đề của cửa sổ. Trên thiết bị di động, ứng dụng có thể thoát bất cứ lúc nào trong khi đang được tạm ngưng và chuyển xuống nền.

Xử lý notification
------------------

Trên các nền tảng máy tính để bàn và web, :ref:`Node <class_Node>` nhận một notification ``NOTIFICATION_WM_CLOSE_REQUEST`` đặc biệt khi trình quản lý cửa sổ yêu cầu thoát.

Notification được xử lý như sau (trên bất kỳ node nào):

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

Điều quan trọng cần lưu ý là theo mặc định, ứng dụng Godot có hành vi tích hợp là thoát khi trình quản lý cửa sổ yêu cầu thoát. Có thể thay đổi hành vi này để người dùng có thể tự thực hiện toàn bộ quy trình thoát:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().set_auto_accept_quit(false)

 .. code-tab:: csharp

    GetTree().AutoAcceptQuit = false;

Trên thiết bị di động
---------------------

Không có thành phần tương đương trực tiếp với ``NOTIFICATION_WM_CLOSE_REQUEST`` trên các nền tảng di động. Do đặc thù của các hệ điều hành di động, nơi duy nhất bạn có thể chạy code trước khi thoát là khi ứng dụng đang được tạm ngưng và chuyển xuống nền. Trên cả Android và iOS, ứng dụng có thể bị người dùng hoặc hệ điều hành buộc dừng bất cứ lúc nào trong khi đang bị tạm ngưng. Một cách chuẩn bị trước cho khả năng này là sử dụng ``NOTIFICATION_APPLICATION_PAUSED`` để thực hiện mọi thao tác cần thiết khi ứng dụng được tạm ngưng.

.. note:: On iOS, you only have approximately 5 seconds to finish a task started by this signal. If you go over this allotment, iOS will kill the app instead of pausing it.

Trên Android, nhấn nút Back sẽ thoát ứng dụng nếu **Application > Config > Quit On Go Back** được bật trong Project Settings (đây là thiết lập mặc định). Thao tác này sẽ kích hoạt ``NOTIFICATION_WM_GO_BACK_REQUEST``.


Gửi notification thoát của riêng bạn
------------------------------------

Mặc dù có thể buộc ứng dụng đóng bằng cách gọi
:ref:`SceneTree.quit <class_SceneTree_method_quit>`, doing so will not send
``NOTIFICATION_WM_CLOSE_REQUEST`` đến các node trong scene tree. Việc thoát bằng cách gọi :ref:`SceneTree.quit <class_SceneTree_method_quit>` sẽ không cho phép các thao tác tùy chỉnh hoàn tất (chẳng hạn như lưu, xác nhận thoát hoặc debugging), ngay cả khi bạn cố trì hoãn dòng lệnh buộc thoát.

Thay vào đó, nếu muốn thông báo cho các node trong scene tree về việc chương trình sắp kết thúc, bạn nên tự gửi notification:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().root.propagate_notification(NOTIFICATION_WM_CLOSE_REQUEST)

 .. code-tab:: csharp

    GetTree().Root.PropagateNotification((int)NotificationWMCloseRequest);

Việc gửi notification này sẽ thông báo cho tất cả các node về việc chương trình kết thúc, nhưng bản thân nó sẽ không kết thúc chương trình *khác với trong 3.X*. Để đạt được hành vi trước đây, cần gọi :ref:`SceneTree.quit <class_SceneTree_method_quit>` sau notification.
