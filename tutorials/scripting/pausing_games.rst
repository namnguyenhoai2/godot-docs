.. _doc_pausing_games:

Tạm dừng game và process mode
=============================

Giới thiệu
----------

Trong hầu hết các game, tại một thời điểm nào đó, bạn sẽ muốn ngắt game để làm việc khác, chẳng hạn như nghỉ giải lao hoặc thay đổi tùy chọn. Việc triển khai cơ chế kiểm soát chi tiết xem những gì có thể tạm dừng (và những gì không thể) đòi hỏi rất nhiều công sức, vì vậy Godot cung cấp một framework đơn giản để tạm dừng.

Cách hoạt động của việc tạm dừng
--------------------------------

Để tạm dừng game, cần thiết lập trạng thái tạm dừng. Thực hiện việc này bằng cách gán ``true`` cho thuộc tính :ref:`SceneTree.paused <class_SceneTree_property_paused>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().paused = true

 .. code-tab:: csharp

    GetTree().Paused = true;

Việc này sẽ gây ra hai điều. Thứ nhất, vật lý 2D và 3D sẽ dừng đối với tất cả các node. Thứ hai, hành vi của một số node sẽ dừng hoặc bắt đầu tùy thuộc vào process mode của chúng.

.. note:: Có thể giữ cho các physics server hoạt động trong khi game đang tạm dừng bằng cách sử dụng các phương thức ``set_active`` của chúng.

Process Modes
-------------

Mỗi node trong Godot có một "Process Mode" xác định thời điểm node đó được process. Bạn có thể tìm và thay đổi thuộc tính này trong các thuộc tính :ref:`Node <class_Node>` của node ở inspector.

.. image:: img/pausemode.webp

Bạn cũng có thể thay đổi thuộc tính này bằng code:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        process_mode = Node.PROCESS_MODE_PAUSABLE

 .. code-tab:: csharp

    public override void _Ready()
    {
        ProcessMode = Node.ProcessModeEnum.Pausable;
    }

Mỗi mode yêu cầu node thực hiện như sau:

-  **Inherit**: Process tùy thuộc vào trạng thái của parent, grandparent, v.v. Node parent đầu tiên có trạng thái khác Inherit sẽ được sử dụng.
-  **Pausable**: Chỉ process node (và các node con ở mode Inherit) khi game không bị tạm dừng.
-  **WhenPaused**: Process node (và các node con ở mode Inherit) *chỉ* khi game đang tạm dừng.
-  **Always**: Process node (và các node con ở mode Inherit) trong mọi trường hợp. Dù game có tạm dừng hay không, node này vẫn sẽ được process.
-  **Disabled**: Node (và các node con ở mode Inherit) sẽ hoàn toàn không được process.

Theo mặc định, tất cả các node đều có thuộc tính này ở trạng thái "Inherit". Nếu parent được đặt thành "Inherit", grandparent sẽ được kiểm tra, rồi tiếp tục như vậy. Nếu không tìm thấy trạng thái nào trong các node grandparent, trạng thái tạm dừng trong SceneTree sẽ được sử dụng. Điều này có nghĩa là theo mặc định, khi game bị tạm dừng, mọi node sẽ bị tạm dừng. Khi một node dừng việc process, một số điều sẽ xảy ra.

Các hàm ``_process``, ``_physics_process``, ``_input`` và ``_input_event`` sẽ không được gọi. Tuy nhiên, các signal vẫn hoạt động và khiến hàm được kết nối của chúng chạy, ngay cả khi script của hàm đó được gắn vào một node hiện không được process.

Các node animation sẽ tạm dừng animation hiện tại, các node audio sẽ tạm dừng audio stream hiện tại, và các particle sẽ tạm dừng. Những thành phần này sẽ tự động tiếp tục khi game không còn bị tạm dừng.

Điều quan trọng cần lưu ý là ngay cả khi một node vẫn đang được process trong lúc game tạm dừng, physics theo mặc định sẽ **KHÔNG** hoạt động đối với node đó. Như đã nêu trước đó, nguyên nhân là do các physics server đã bị tắt. Có thể giữ cho các physics server hoạt động trong khi game đang tạm dừng bằng cách sử dụng các phương thức ``set_active`` của chúng.

Ví dụ về pause menu
-------------------

Bắt đầu bằng cách tạo một button dùng để tạm dừng game.

Tạo một menu chứa close button, đặt **Process Mode** của root node của menu thành **When Paused**, sau đó ẩn menu. Vì process mode được đặt thành **When Paused** trên root node, tất cả node con và node cháu của nó sẽ kế thừa process mode đó. Nhờ vậy, tất cả node trong menu sẽ bắt đầu được process khi game tạm dừng.

Gắn một script vào root node của menu, kết nối pause button đã tạo trước đó với một method mới trong script, rồi trong method đó tạm dừng game và hiển thị pause menu.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_pause_button_pressed():
        get_tree().paused = true
        show()

 .. code-tab:: csharp

    private void OnPauseButtonPressed()
    {
        GetTree().Paused = true;
        Show();
    }

Cuối cùng, kết nối close button của menu với một method mới trong script. Trong method đó, tiếp tục game và ẩn pause menu.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_close_button_pressed():
        hide()
        get_tree().paused = false

 .. code-tab:: csharp

    private void OnCloseButtonPressed()
    {
        Hide();
        GetTree().Paused = false;
    }

Bây giờ bạn đã có một pause menu hoạt động.
