:article_outdated: True

.. _doc_3d_gizmo_plugins:

plugin gizmo 3D
===============

Giới thiệu
----------

Plugin gizmo 3D được editor và các plugin tùy chỉnh sử dụng để định nghĩa các gizmo gắn vào bất kỳ loại node Node3D nào.

Tutorial này trình bày hai cách tiếp cận chính để định nghĩa gizmo tùy chỉnh của riêng bạn. Tùy chọn đầu tiên phù hợp với các gizmo đơn giản và tạo ra ít sự rườm rà hơn trong cấu trúc plugin của bạn, còn tùy chọn thứ hai cho phép bạn lưu trữ một số dữ liệu riêng cho từng gizmo.

.. note:: This tutorial assumes you already know how to make generic plugins. If
          nếu không chắc chắn, hãy tham khảo trang :ref:`doc_making_plugins`.

EditorNode3DGizmoPlugin
-----------------------

Bất kể chọn cách tiếp cận nào, chúng ta sẽ cần tạo một
:ref:`EditorNode3DGizmoPlugin <class_EditorNode3DGizmoPlugin>`. This will allow
cho phép chúng ta đặt tên cho loại gizmo mới và định nghĩa các hành vi khác, chẳng hạn như gizmo có thể bị ẩn hay không.

Thiết lập cơ bản sẽ như sau:

::

    # my_custom_gizmo_plugin.gd
    extends EditorNode3DGizmoPlugin


    func _get_gizmo_name():
        return "CustomNode"


::

    # MyCustomEditorPlugin.gd
    @tool
    extends EditorPlugin


    const MyCustomGizmoPlugin = preload("res://addons/my-addon/my_custom_gizmo_plugin.gd")

    var gizmo_plugin = MyCustomGizmoPlugin.new()


    func _enter_tree():
        add_node_3d_gizmo_plugin(gizmo_plugin)


    func _exit_tree():
        remove_node_3d_gizmo_plugin(gizmo_plugin)


Đối với các gizmo đơn giản, chỉ cần kế thừa :ref:`EditorNode3DGizmoPlugin <class_EditorNode3DGizmoPlugin>`. Nếu muốn lưu trữ một số dữ liệu riêng cho từng gizmo, bạn nên chọn cách tiếp cận thứ hai.


Cách tiếp cận đơn giản
----------------------

Bước đầu tiên là trong plugin gizmo tùy chỉnh, ghi đè phương thức :ref:`_has_gizmo()<class_EditorNode3DGizmoPlugin_private_method__has_gizmo>` để phương thức này trả về ``true`` khi tham số node có kiểu mục tiêu của chúng ta.

::

    # ...


    func _has_gizmo(node):
        return node is MyCustomNode3D


    # ...

Sau đó, chúng ta có thể ghi đè các phương thức như :ref:`_redraw()<class_EditorNode3DGizmoPlugin_private_method__redraw>` hoặc tất cả các phương thức liên quan đến handle.

::

    # ...


    func _init():
        create_material("main", Color(1, 0, 0))
        create_handle_material("handles")


    func _redraw(gizmo):
        gizmo.clear()

        var node3d = gizmo.get_node_3d()

        var lines = PackedVector3Array()

        lines.push_back(Vector3(0, 1, 0))
        lines.push_back(Vector3(0, node3d.my_custom_value, 0))

        var handles = PackedVector3Array()

        handles.push_back(Vector3(0, 1, 0))
        handles.push_back(Vector3(0, node3d.my_custom_value, 0))

        gizmo.add_lines(lines, get_material("main", gizmo), false)
        gizmo.add_handles(handles, get_material("handles", gizmo), [])


    # ...

Lưu ý rằng chúng ta đã tạo một material trong phương thức `_init` method, and retrieved it in the `_redraw` bằng cách sử dụng :ref:`get_material()<class_EditorNode3DGizmoPlugin_method_get_material>`. Phương thức này lấy một trong các biến thể của material tùy thuộc vào trạng thái của gizmo (được chọn và/hoặc có thể chỉnh sửa).

Vậy plugin hoàn chỉnh sẽ trông gần như sau:

::

    extends EditorNode3DGizmoPlugin


    const MyCustomNode3D = preload("res://addons/my-addon/my_custom_node_3d.gd")


    func _init():
        create_material("main", Color(1,0,0))
        create_handle_material("handles")


    func _has_gizmo(node):
        return node is MyCustomNode3D


    func _redraw(gizmo):
        gizmo.clear()

        var node3d = gizmo.get_node_3d()

        var lines = PackedVector3Array()

        lines.push_back(Vector3(0, 1, 0))
        lines.push_back(Vector3(0, node3d.my_custom_value, 0))

        var handles = PackedVector3Array()

        handles.push_back(Vector3(0, 1, 0))
        handles.push_back(Vector3(0, node3d.my_custom_value, 0))

        gizmo.add_lines(lines, get_material("main", gizmo), false)
        gizmo.add_handles(handles, get_material("handles", gizmo), [])


    # Bạn nên triển khai các callback còn lại liên quan đến handle
    # (_get_handle_name(), _get_handle_value(), _commit_handle(), ...).

Lưu ý rằng chúng ta vừa thêm một số handle trong phương thức `_redraw`, nhưng vẫn cần triển khai các callback còn lại liên quan đến handle trong :ref:`EditorNode3DGizmoPlugin <class_EditorNode3DGizmoPlugin>` để các handle hoạt động đúng cách.

Cách tiếp cận thay thế
----------------------

Trong một số trường hợp, chúng ta muốn cung cấp cách triển khai riêng cho :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, có thể vì muốn lưu trữ một số trạng thái trong từng gizmo hoặc vì đang chuyển một plugin gizmo cũ sang và không muốn thực hiện lại toàn bộ quá trình viết lại.

Trong những trường hợp này, tất cả những gì cần làm là trong plugin gizmo mới, ghi đè
:ref:`_create_gizmo()<class_EditorNode3DGizmoPlugin_private_method__create_gizmo>`, so it returns our custom gizmo implementation
cho các node Node3D mà chúng ta muốn nhắm tới.

::

    # my_custom_gizmo_plugin.gd
    extends EditorNode3DGizmoPlugin


    const MyCustomNode3D = preload("res://addons/my-addon/my_custom_node_3d.gd")
    const MyCustomGizmo = preload("res://addons/my-addon/my_custom_gizmo.gd")


    func _init():
        create_material("main", Color(1, 0, 0))
        create_handle_material("handles")


    func _create_gizmo(node):
        if node is MyCustomNode3D:
            return MyCustomGizmo.new()
        else:
            return null

Bằng cách này, toàn bộ logic và các phương thức vẽ gizmo có thể được triển khai trong một class mới mở rộng
:ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, like so:

::

    # my_custom_gizmo.gd
    extends EditorNode3DGizmo


    # Bạn có thể lưu trữ dữ liệu ngay trong gizmo (hữu ích hơn khi làm việc với các handle).
    var gizmo_size = 3.0


    func _redraw():
        clear()

        var node3d = get_node_3d()

        var lines = PackedVector3Array()

        lines.push_back(Vector3(0, 1, 0))
        lines.push_back(Vector3(gizmo_size, node3d.my_custom_value, 0))

        var handles = PackedVector3Array()

        handles.push_back(Vector3(0, 1, 0))
        handles.push_back(Vector3(gizmo_size, node3d.my_custom_value, 0))

        var material = get_plugin().get_material("main", self)
        add_lines(lines, material, false)

        var handles_material = get_plugin().get_material("handles", self)
        add_handles(handles, handles_material, [])


    # Bạn nên triển khai các callback còn lại liên quan đến handle
    # (_get_handle_name(), _get_handle_value(), _commit_handle(), ...).

Lưu ý rằng chúng ta vừa thêm một số handle trong phương thức `_redraw`, nhưng vẫn cần triển khai các callback còn lại liên quan đến handle trong :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` để các handle hoạt động đúng cách.
