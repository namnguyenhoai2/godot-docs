.. _doc_scene_tree:

Sử dụng SceneTree
=================

Giới thiệu
----------

Trong các tutorial trước, mọi thứ đều xoay quanh khái niệm node. Scene là tập hợp các node. Chúng trở nên hoạt động khi được đưa vào *scene tree*.

MainLoop
--------

Cách Godot hoạt động bên trong như sau: Có
:ref:`OS <class_OS>` class,
đây là instance duy nhất chạy ngay từ đầu. Sau đó, tất cả driver, server, ngôn ngữ scripting, hệ thống scene, v.v. sẽ được tải.

Khi quá trình khởi tạo hoàn tất, :ref:`OS <class_OS>` cần được cung cấp một :ref:`MainLoop <class_MainLoop>` để chạy. Cho đến thời điểm này, tất cả những gì diễn ra đều là hoạt động nội bộ (bạn có thể xem tệp main/main.cpp trong source code nếu muốn tìm hiểu cách hoạt động bên trong).

Chương trình của người dùng, hay game, bắt đầu trong MainLoop. Class này có một số method dùng cho việc khởi tạo, idle (callback đồng bộ theo frame), fixed (callback đồng bộ theo physics) và input. Một lần nữa, đây là cấp thấp, và khi làm game trong Godot, việc tự viết MainLoop hiếm khi hợp lý.

SceneTree
---------

Một cách để giải thích cách Godot hoạt động là: đây là một game engine cấp cao chạy trên middleware cấp thấp.

Hệ thống scene là game engine, còn :ref:`OS <class_OS>` và các server là API cấp thấp.

Hệ thống scene cung cấp main loop riêng cho OS,
:ref:`SceneTree <class_SceneTree>`.
Thành phần này được tự động tạo instance và thiết lập khi chạy một scene, không cần thực hiện thêm bất kỳ công việc nào.

Điều quan trọng là phải biết class này tồn tại vì nó có một số công dụng quan trọng:

-  Nó chứa :ref:`Viewport <class_Viewport>` gốc, nơi một scene được thêm vào làm child khi lần đầu được mở để trở thành một phần của *Scene Tree* (sẽ nói thêm về điều này ở phần sau). - Nó chứa thông tin về các group và có khả năng gọi tất cả node trong một group hoặc lấy danh sách các node đó. - Nó chứa một số chức năng về trạng thái toàn cục, chẳng hạn như thiết lập pause mode hoặc thoát process.

Khi một node là một phần của Scene Tree,
:ref:`SceneTree <class_SceneTree>`
singleton có thể được lấy bằng cách gọi
:ref:`Node.get_tree() <class_Node_method_get_tree>`.

Root viewport
-------------

:ref:`Viewport <class_Viewport>` gốc luôn nằm ở trên cùng của scene. Từ một node, có thể lấy nó bằng hai cách khác nhau:

.. tabs::
 .. code-tab:: gdscript GDScript

        get_tree().root # Truy cập thông qua main loop của scene.
        get_node("/root") # Truy cập thông qua absolute path.

 .. code-tab:: csharp

        GetTree().Root // Truy cập thông qua main loop của scene.
        GetNode("/root"); // Truy cập thông qua absolute path.

Node này chứa viewport chính. Mọi thứ là child của một
:ref:`Viewport <class_Viewport>`
đều được vẽ bên trong nó theo mặc định, vì vậy việc node ở trên cùng luôn thuộc kiểu này là hợp lý; nếu không, sẽ không thấy gì.

Mặc dù có thể tạo các viewport khác trong scene (chẳng hạn để tạo hiệu ứng split-screen), đây là viewport duy nhất không bao giờ được người dùng tạo. Nó được tự động tạo bên trong SceneTree.

Scene tree
----------

Khi một node được kết nối, trực tiếp hoặc gián tiếp, với root viewport, nó trở thành một phần của *scene tree*.

Điều này có nghĩa là, như đã giải thích trong các tutorial trước, nó sẽ nhận các callback ``_enter_tree()`` và ``_ready()`` (cũng như ``_exit_tree()``).

.. image:: img/activescene.webp

Khi các node đi vào *Scene Tree*, chúng trở nên hoạt động. Chúng có quyền truy cập vào mọi thứ cần thiết để xử lý, nhận input, hiển thị hình ảnh 2D và 3D, nhận và gửi notification, phát âm thanh, v.v. Khi bị xóa khỏi *scene tree*, chúng sẽ mất các khả năng này.

Thứ tự trong tree
-----------------

Hầu hết các thao tác trên node trong Godot, chẳng hạn như vẽ 2D, xử lý hoặc nhận notification, đều được thực hiện theo *tree order*, tức từ trên xuống dưới như hiển thị trong editor (còn gọi là duyệt pre-order):

.. image:: img/toptobottom.webp

Ví dụ, node trên cùng trong một scene sẽ được gọi function ``_process()`` trước, sau đó node ngay bên dưới sẽ được gọi function ``_process()``, rồi đến node bên dưới nó, cứ tiếp tục như vậy.

Một ngoại lệ quan trọng là function ``_ready()``: mỗi node cha chỉ được gọi function ``_ready()`` sau khi tất cả node con của nó đã được gọi function ``_ready()``, ताकि node cha biết rằng các node con đã hoàn toàn sẵn sàng để được truy cập. Đây còn được gọi là duyệt post-order. Trong hình trên, ``NameLabel`` sẽ nhận notification trước (nhưng chỉ sau các node con của nó, nếu có!), tiếp theo là ``Name``, v.v., và ``Panel`` sẽ nhận notification cuối cùng.

Có thể ghi đè thứ tự thao tác bằng thuộc tính node ``process_priority``. Các node có số nhỏ hơn sẽ được gọi trước. Ví dụ, các node có độ ưu tiên "0, 1, 2, 3" sẽ được gọi theo thứ tự đó từ trái sang phải.

“Trở nên hoạt động” bằng cách đi vào *Scene Tree*
-------------------------------------------------

#. Một scene được tải từ ổ đĩa hoặc được tạo bằng scripting. #. Node gốc của scene đó (hãy nhớ rằng chỉ có một node gốc) được thêm vào làm child của Viewport "root" (từ SceneTree), hoặc vào bất kỳ node con nào của nó. #. Mọi node trong scene mới được thêm sẽ nhận notification "enter_tree" (callback ``_enter_tree()`` trong GDScript) theo thứ tự từ trên xuống dưới (duyệt pre-order). #. Mọi node sẽ nhận notification "ready" (callback ``_ready()`` trong GDScript) để thuận tiện, sau khi tất cả node con của nó đã nhận notification "ready" (duyệt post-order). #. Khi một scene (hoặc một phần của scene) bị xóa, các node đó sẽ nhận notification "exit scene" (callback ``_exit_tree()`` trong GDScript) theo thứ tự từ dưới lên trên (hoàn toàn ngược với thứ tự từ trên xuống dưới).

Thay đổi scene hiện tại
-----------------------

Sau khi một scene được tải, bạn có thể muốn chuyển sang một scene khác. Một cách để thực hiện việc này là sử dụng function
:ref:`SceneTree.change_scene_to_file() <class_SceneTree_method_change_scene_to_file>`
function:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _my_level_was_completed():
        get_tree().change_scene_to_file("res://levels/level2.tscn")

 .. code-tab:: csharp

    public void _MyLevelWasCompleted()
    {
        GetTree().ChangeSceneToFile("res://levels/level2.tscn");
    }

Thay vì sử dụng file path, bạn cũng có thể sử dụng các
:ref:`PackedScene <class_PackedScene>` resources using the equivalent
function có sẵn
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

Đây là những cách nhanh chóng và hữu ích để chuyển scene, nhưng có nhược điểm là game sẽ bị đứng cho đến khi scene mới được tải và chạy. Ở một thời điểm nào đó trong quá trình phát triển game, bạn có thể muốn tạo các màn hình loading phù hợp với progress bar, indicator động hoặc loading theo thread (background). Việc này phải được thực hiện thủ công bằng cách sử dụng :ref:`doc_singletons_autoload` và :ref:`doc_background_loading`.
