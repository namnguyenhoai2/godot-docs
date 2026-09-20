.. _doc_groups:

Groups
======

Groups trong Godot hoạt động giống như tags trong các phần mềm khác. Bạn có thể thêm một node vào bao nhiêu group tùy ý. Sau đó, trong code, bạn có thể dùng SceneTree để:

- Lấy danh sách các node trong một group. - Gọi một method trên tất cả node trong một group. - Gửi một notification đến tất cả node trong một group.

Đây là một tính năng hữu ích để tổ chức các scene lớn và tách rời code.


Quản lý groups
--------------

Groups được tạo bằng cách thêm một node vào tên group mới, và tương tự, chúng được xóa bằng cách xóa tất cả node khỏi một group nhất định.

Có hai cách để thêm/xóa node khỏi groups:

- Trong quá trình thiết kế, bằng cách sử dụng Groups dock trong editor hoặc tab Groups trong Globals dock của project settings. - Trong quá trình thực thi, bằng cách gọi :ref:`Node.add_to_group() <class_Node_method_add_to_group>` hoặc :ref:`Node.remove_from_group() <class_Node_method_remove_from_group>`.

.. tip::

    Mặc dù không bắt buộc nghiêm ngặt, bạn nên sử dụng quy ước đặt tên ``snake_case`` cho tên các group.

Sử dụng Groups dock
~~~~~~~~~~~~~~~~~~~

Bạn có thể tạo groups mới bằng Groups dock.

.. image:: img/groups_dock.webp

Chọn một node trong Scene dock, sau đó nhấp vào nút thêm có biểu tượng +.

.. image:: img/groups_add_new_group_button.webp

Bây giờ bạn sẽ thấy modal Create New Group xuất hiện. Nhập tên group vào trường này.

Bạn có thể tùy chọn đánh dấu "Global", để group hiển thị trên toàn project và có thể được sử dụng lại trong bất kỳ scene nào của project. Tùy chọn này cũng cho phép bạn thêm mô tả cho group.

Khi hoàn tất, nhấn Ok để tạo group.

.. image:: img/groups_add_new_group_modal.webp

Bạn sẽ thấy các group mới xuất hiện trong Groups dock, bên dưới Scene Groups nếu tùy chọn Global không được đánh dấu, hoặc bên dưới Global Groups nếu tùy chọn đó được đánh dấu.

Một Node được chọn trong Scene dock có thể được thêm vào các group bằng cách đánh dấu checkbox ở bên trái các group trong Groups dock. Node bạn đã chọn khi tạo group mới sẽ tự động được đánh dấu.

.. image:: img/groups_dock_with_created_groups.webp

Tất cả group trong project được đánh dấu là Global và được tạo từ bất kỳ scene nào sẽ hiển thị bên dưới Global Groups.

Mọi group khác được tạo từ các node trong scene hiện tại sẽ xuất hiện bên dưới Scene Groups.

.. warning:: The same underlying logic is used for both Global and Scene groups.
             Các group có cùng tên được xem là một group duy nhất. Tính năng này chỉ nhằm mục đích tổ chức.

.. image:: img/groups_node_tab_with_multiple_types_of_groups.webp

Bạn có thể quản lý Global Groups trong tab Groups của Globals dock, bên trong Project Settings. Tại đó, bạn có thể thêm các global group mới hoặc thay đổi tên và mô tả của các group hiện có.

.. image:: img/groups_global_groups_settings.webp

Sử dụng code
~~~~~~~~~~~~

Bạn cũng có thể quản lý groups từ các script. Đoạn code sau thêm node mà bạn gắn script vào group ``guards`` ngay khi node đó đi vào scene tree.

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

Hãy tưởng tượng bạn đang tạo một game xâm nhập. Khi một enemy phát hiện player, bạn muốn tất cả guard và robot chuyển sang trạng thái cảnh giác.

Trong ví dụ giả tưởng bên dưới, chúng ta sử dụng ``SceneTree.call_group()`` để cảnh báo tất cả enemy rằng player đã bị phát hiện.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_player_spotted():
        get_tree().call_group("guards", "enter_alert_mode")

 .. code-tab:: csharp

    public void _OnPlayerDiscovered()
    {
        GetTree().CallGroup("guards", "enter_alert_mode");
    }

Đoạn code trên gọi function ``enter_alert_mode`` trên mọi member của group ``guards``.

Để lấy toàn bộ danh sách các node trong group ``guards`` dưới dạng một array, bạn có thể gọi
:ref:`SceneTree.get_nodes_in_group()
<class_SceneTree_method_get_nodes_in_group>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    var guards = get_tree().get_nodes_in_group("guards")

 .. code-tab:: csharp

    var guards = GetTree().GetNodesInGroup("guards");

Class :ref:`SceneTree <class_SceneTree>` cung cấp nhiều method hữu ích khác để tương tác với các scene, hệ thống phân cấp node và groups. Class này cho phép bạn dễ dàng chuyển đổi scene hoặc tải lại chúng, thoát game hoặc tạm dừng và tiếp tục game. Class này cũng cung cấp các signal hữu ích.
