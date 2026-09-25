.. _doc_groups:

Nhóm
====

Trong Godot, nhóm hoạt động giống như tag trong các phần mềm khác. Bạn có thể thêm một node vào bao nhiêu nhóm tùy ý. Sau đó, trong code, bạn có thể dùng SceneTree để:

- Lấy danh sách các node trong một nhóm.
- Gọi một phương thức trên tất cả node trong một nhóm.
- Gửi một thông báo đến tất cả node trong một nhóm.

Đây là một tính năng hữu ích để tổ chức các scene lớn và tách biệt code.


Quản lý nhóm
------------

Các nhóm được tạo bằng cách thêm một node vào tên nhóm mới, và tương tự, chúng được xóa bằng cách loại bỏ tất cả node khỏi một nhóm nhất định.

Có hai cách để thêm hoặc xóa node khỏi nhóm:

- Trong lúc thiết kế, bằng cách sử dụng Groups dock trong editor hoặc tab Groups trong Globals dock của project settings.
- Trong lúc thực thi, bằng cách gọi :ref:`Node.add_to_group() <class_Node_method_add_to_group>` hoặc :ref:`Node.remove_from_group() <class_Node_method_remove_from_group>`.

.. tip::

    Mặc dù không bắt buộc, bạn nên sử dụng quy ước đặt tên ``snake_case`` cho tên nhóm.

Sử dụng Groups dock
~~~~~~~~~~~~~~~~~~~

Bạn có thể tạo các nhóm mới bằng Groups dock.

.. image:: img/groups_dock.webp

Chọn một node trong Scene dock, sau đó nhấp vào nút thêm có ký hiệu +.

.. image:: img/groups_add_new_group_button.webp

Bây giờ bạn sẽ thấy modal Create New Group xuất hiện. Nhập tên nhóm vào trường.

Bạn có thể tùy chọn đánh dấu tùy chọn "Global", tùy chọn này sẽ làm cho nhóm hiển thị trên toàn project và có thể được sử dụng lại trong bất kỳ scene nào của project. Tùy chọn này cũng cho phép bạn thêm mô tả cho nhóm.

Khi hoàn tất, nhấn Ok để tạo nhóm.

.. image:: img/groups_add_new_group_modal.webp

Bạn sẽ thấy các nhóm mới xuất hiện trong Groups dock bên dưới Scene Groups nếu tùy chọn Global không được đánh dấu, hoặc bên dưới Global Groups nếu tùy chọn đó được đánh dấu.

Một Node được chọn từ Scene dock có thể được thêm vào các nhóm bằng cách đánh dấu checkbox ở bên trái các nhóm trong Groups dock. Node được chọn khi bạn tạo nhóm mới sẽ tự động được đánh dấu.

.. image:: img/groups_dock_with_created_groups.webp

Tất cả nhóm có trong project được đánh dấu là Global và được tạo từ bất kỳ scene nào sẽ hiển thị bên dưới Global Groups.

Mọi nhóm khác bắt nguồn từ các node trong scene hiện tại sẽ xuất hiện bên dưới Scene Groups.

.. warning:: Cả nhóm Global và nhóm Scene đều sử dụng cùng một logic nền tảng. Các nhóm có cùng tên được xem là một nhóm duy nhất. Tính năng này chỉ nhằm mục đích tổ chức.

.. image:: img/groups_node_tab_with_multiple_types_of_groups.webp

Bạn có thể quản lý Global Groups trong tab Groups của Globals dock, bên trong Project Settings. Tại đó, bạn có thể thêm các nhóm global mới hoặc thay đổi tên và mô tả của các nhóm hiện có.

.. image:: img/groups_global_groups_settings.webp

Sử dụng code
~~~~~~~~~~~~

Bạn cũng có thể quản lý nhóm từ các script. Đoạn code sau thêm node mà bạn gắn script vào nhóm ``guards`` ngay khi node đó đi vào scene tree.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        add_to_group("guards")

 .. code-tab:: csharp

    public override void _Ready()
    {
        base._Ready();

        AddToGroup("guards");
    }

Hãy tưởng tượng bạn đang tạo một game xâm nhập. Khi một kẻ địch phát hiện người chơi, bạn muốn tất cả lính canh và robot đều chuyển sang trạng thái cảnh giác.

Trong ví dụ giả định bên dưới, chúng ta sử dụng ``SceneTree.call_group()`` để cảnh báo tất cả kẻ địch rằng người chơi đã bị phát hiện.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_player_spotted():
        get_tree().call_group("guards", "enter_alert_mode")

 .. code-tab:: csharp

    public void _OnPlayerDiscovered()
    {
        GetTree().CallGroup("guards", "enter_alert_mode");
    }

Đoạn code trên gọi hàm ``enter_alert_mode`` trên mọi thành viên của nhóm ``guards``.

Để lấy toàn bộ danh sách các node trong nhóm ``guards`` dưới dạng một array, bạn có thể gọi
:ref:`SceneTree.get_nodes_in_group()
<class_SceneTree_method_get_nodes_in_group>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    var guards = get_tree().get_nodes_in_group("guards")

 .. code-tab:: csharp

    var guards = GetTree().GetNodesInGroup("guards");

Lớp :ref:`SceneTree <class_SceneTree>` cung cấp nhiều phương thức hữu ích hơn để tương tác với các scene, hệ thống phân cấp node và nhóm của chúng. Lớp này cho phép bạn dễ dàng chuyển đổi scene hoặc tải lại chúng, thoát game hoặc tạm dừng và tiếp tục game. Lớp này cũng cung cấp các signal hữu ích.
