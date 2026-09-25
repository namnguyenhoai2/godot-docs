.. _doc_scene_tree:

Sử dụng SceneTree
=================

Giới thiệu
----------

Trong các hướng dẫn trước, mọi thứ đều xoay quanh khái niệm node. Scene là tập hợp các node. Chúng trở nên hoạt động khi đi vào *scene tree*.

MainLoop
--------

Cách Godot hoạt động bên trong như sau: Có
:ref:`OS <class_OS>` class, đây là instance duy nhất chạy lúc khởi động. Sau đó, tất cả driver, server, ngôn ngữ scripting, hệ thống scene, v.v. được tải.

Khi quá trình khởi tạo hoàn tất, :ref:`OS <class_OS>` cần được cung cấp một :ref:`MainLoop <class_MainLoop>` để chạy. Cho đến thời điểm này, tất cả đều là hoạt động nội bộ (bạn có thể xem tệp main/main.cpp trong mã nguồn nếu muốn tìm hiểu cách thức hoạt động bên trong).

Chương trình người dùng, hay game, bắt đầu trong MainLoop. Class này có một số phương thức để khởi tạo, idle (callback đồng bộ theo frame), fixed (callback đồng bộ theo physics) và input. Một lần nữa, đây là cấp thấp và khi làm game trong Godot, việc tự viết MainLoop hiếm khi có ý nghĩa.

SceneTree
---------

Một cách để giải thích cách Godot hoạt động là đây là một game engine cấp cao chạy trên middleware cấp thấp.

Hệ thống scene là game engine, còn :ref:`OS <class_OS>` và các server là API cấp thấp.

Hệ thống scene cung cấp main loop riêng cho OS,
:ref:`SceneTree <class_SceneTree>`. Thành phần này được tạo instance và thiết lập tự động khi chạy một scene, không cần thực hiện thêm công việc nào.

Điều quan trọng là phải biết class này tồn tại vì nó có một số công dụng quan trọng:

-  Nó chứa :ref:`Viewport <class_Viewport>` root, nơi một scene được thêm làm child khi lần đầu được mở để trở thành một phần của *Scene Tree* (sẽ nói thêm ở phần tiếp theo).
-  Nó chứa thông tin về các group và có khả năng gọi tất cả node trong một group hoặc lấy danh sách các node đó.
-  Nó chứa một số chức năng về trạng thái toàn cục, chẳng hạn như thiết lập pause mode hoặc thoát process.

Khi một node là một phần của Scene Tree,
:ref:`SceneTree <class_SceneTree>` singleton có thể được lấy bằng cách gọi
:ref:`Node.get_tree() <class_Node_method_get_tree>`.

Root viewport
-------------

:ref:`Viewport <class_Viewport>` root luôn nằm ở trên cùng của scene. Từ một node, có thể lấy nó theo hai cách khác nhau:

.. tabs::
 .. code-tab:: gdscript GDScript

        get_tree().root # Truy cập thông qua scene main loop.
        get_node("/root") # Truy cập thông qua đường dẫn tuyệt đối.

 .. code-tab:: csharp

        GetTree().Root // Truy cập thông qua scene main loop.
        GetNode("/root"); // Truy cập thông qua đường dẫn tuyệt đối.

Node này chứa viewport chính. Mọi thành phần là child của một
:ref:`Viewport <class_Viewport>` mặc định đều được vẽ bên trong nó, vì vậy việc tất cả node ở trên cùng luôn là một node thuộc kiểu này là hợp lý; nếu không thì sẽ không nhìn thấy gì.

Mặc dù có thể tạo các viewport khác trong scene (để tạo hiệu ứng split-screen và các hiệu ứng tương tự), đây là viewport duy nhất không bao giờ được người dùng tạo. Nó được tạo tự động bên trong SceneTree.

Cây scene
---------

Khi một node được kết nối, trực tiếp hoặc gián tiếp, với root viewport, nó trở thành một phần của *scene tree*.

Điều này có nghĩa là, như đã giải thích trong các hướng dẫn trước, nó sẽ nhận các callback ``_enter_tree()`` và ``_ready()`` (cũng như ``_exit_tree()``).

.. image:: img/activescene.webp

Khi các node đi vào *Scene Tree*, chúng trở nên hoạt động. Chúng có quyền truy cập vào mọi thứ cần thiết để xử lý, nhận input, hiển thị hình ảnh 2D và 3D, nhận và gửi notification, phát âm thanh, v.v. Khi bị xóa khỏi *scene tree*, chúng sẽ mất các khả năng này.

Thứ tự trong cây
----------------

Hầu hết thao tác trên node trong Godot, chẳng hạn như vẽ 2D, xử lý hoặc nhận notification, đều được thực hiện theo *tree order*, tức từ trên xuống dưới như hiển thị trong editor (còn gọi là duyệt tiền thứ tự):

.. image:: img/toptobottom.webp

Ví dụ, node trên cùng trong một scene sẽ được gọi hàm ``_process()`` trước, sau đó node bên dưới sẽ được gọi hàm ``_process()``, rồi đến node bên dưới node đó, cứ tiếp tục như vậy.

Một ngoại lệ quan trọng là hàm ``_ready()``: mỗi node cha chỉ được gọi hàm ``_ready()`` sau khi tất cả node con của nó đã được gọi hàm ``_ready()``, để node cha biết rằng các node con đã hoàn toàn sẵn sàng để được truy cập. Đây còn được gọi là duyệt hậu thứ tự. Trong hình trên, ``NameLabel`` sẽ nhận notification đầu tiên (nhưng chỉ sau các node con của nó, nếu có!), tiếp theo là ``Name``, v.v., và ``Panel`` sẽ nhận notification cuối cùng.

Thứ tự thao tác cũng có thể được ghi đè bằng thuộc tính node ``process_priority``. Các node có số nhỏ hơn sẽ được gọi trước. Ví dụ, các node có độ ưu tiên "0, 1, 2, 3" sẽ được gọi theo thứ tự đó từ trái sang phải.

"Trở nên hoạt động" khi đi vào *Scene Tree*
-------------------------------------------

#. Một scene được tải từ đĩa hoặc được tạo bằng scripting.
#. Node root của scene đó (hãy nhớ rằng chỉ có một node root) được thêm làm child của Viewport "root" (từ SceneTree) hoặc của bất kỳ node hậu duệ nào của nó.
#. Mọi node của scene mới được thêm sẽ nhận notification "enter_tree" ( ``_enter_tree()`` callback trong GDScript) theo thứ tự từ trên xuống dưới (duyệt tiền thứ tự).
#. Mọi node sẽ nhận notification "ready" ( ``_ready()`` callback trong GDScript) để thuận tiện, sau khi tất cả node con của nó đã nhận notification "ready" (duyệt hậu thứ tự).
#. Khi một scene (hoặc một phần của scene) bị xóa, các node đó sẽ nhận notification "exit scene" ( ``_exit_tree()`` callback trong GDScript) theo thứ tự từ dưới lên trên (hoàn toàn ngược với thứ tự từ trên xuống dưới).

Thay đổi scene hiện tại
-----------------------

Sau khi một scene được tải, bạn có thể muốn thay scene này bằng một scene khác. Một cách để thực hiện việc này là sử dụng
:ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>` function:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _my_level_was_completed():
        get_tree().change_scene_to_file("res://levels/level2.tscn")

 .. code-tab:: csharp

    public void _MyLevelWasCompleted()
    {
        GetTree().ChangeSceneToFile("res://levels/level2.tscn");
    }

Thay vì sử dụng đường dẫn tệp, bạn cũng có thể sử dụng các resource
:ref:`PackedScene <class_PackedScene>` được tạo sẵn bằng function tương đương
:ref:`SceneTree.change_scene_to_packed(PackedScene scene) <class_SceneTree_method_change_scene_to_packed>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    var next_scene = preload("res://levels/level2.tscn")

    func _my_level_was_completed():
        get_tree().change_scene_to_packed(next_scene)

 .. code-tab:: csharp

    public void _MyLevelWasCompleted()
    {
        var nextScene = (PackedScene)ResourceLoader.Load("res://levels/level2.tscn");
        GetTree().ChangeSceneToPacked(nextScene);
    }

Đây là những cách nhanh chóng và hữu ích để chuyển cảnh, nhưng có nhược điểm là trò chơi sẽ bị dừng cho đến khi cảnh mới được tải và chạy. Ở một thời điểm nào đó trong quá trình phát triển trò chơi, bạn có thể muốn tạo các màn hình tải phù hợp với thanh tiến trình, chỉ báo hoạt ảnh hoặc tính năng tải theo luồng (chạy nền). Việc này phải được thực hiện thủ công bằng :ref:`doc_singletons_autoload` và :ref:`doc_background_loading`.
