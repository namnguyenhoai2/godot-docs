.. _doc_pausing_games:

Tạm dừng game và process mode
=============================

Giới thiệu
----------

Trong hầu hết các game, đôi khi cần tạm dừng game để làm việc khác, chẳng hạn như nghỉ giải lao hoặc thay đổi tùy chọn. Việc triển khai cơ chế kiểm soát chi tiết xem thành phần nào có thể tạm dừng (và thành phần nào không thể) đòi hỏi rất nhiều công sức, vì vậy Godot cung cấp một framework đơn giản để tạm dừng.

Cách thức tạm dừng hoạt động
----------------------------

Để tạm dừng game, cần thiết lập trạng thái tạm dừng. Thực hiện việc này bằng cách gán ``true`` cho thuộc tính :ref:`SceneTree.paused <class_SceneTree_property_paused>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_tree().paused = true

 .. code-tab:: csharp

    GetTree().Paused = true;

Thao tác này sẽ dẫn đến hai điều. Thứ nhất, physics 2D và 3D sẽ dừng đối với tất cả các node. Thứ hai, hành vi của một số node sẽ dừng hoặc bắt đầu tùy thuộc vào process mode của chúng.

.. note:: The physics servers can be made active while the game is
          bằng cách sử dụng các phương thức ``set_active`` của chúng.

Process Modes
-------------

Mỗi node trong Godot có một "Process Mode" xác định thời điểm node đó xử lý. Bạn có thể tìm và thay đổi thuộc tính này trong phần thuộc tính :ref:`Node <class_Node>` của node ở inspector.

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

Sau đây là ý nghĩa của từng mode đối với một node:

-  **Inherit**: Xử lý tùy thuộc vào trạng thái của parent, grandparent, v.v. Node sẽ sử dụng parent đầu tiên có trạng thái khác Inherit. - **Pausable**: Chỉ xử lý node (và các node con ở mode Inherit) khi game không bị tạm dừng. - **WhenPaused**: Chỉ xử lý node (và các node con ở mode Inherit) *khi game đang bị tạm dừng*. - **Always**: Xử lý node (và các node con ở mode Inherit) bất kể thế nào. Dù game có bị tạm dừng hay không, node này vẫn sẽ xử lý. - **Disabled**: Node (và các node con ở mode Inherit) sẽ hoàn toàn không xử lý.

Theo mặc định, tất cả node đều có thuộc tính này ở trạng thái "Inherit". Nếu parent được đặt thành "Inherit", grandparent sẽ được kiểm tra, và tiếp tục như vậy. Nếu không tìm thấy trạng thái nào ở bất kỳ grandparent nào, trạng thái tạm dừng trong SceneTree sẽ được sử dụng. Điều này có nghĩa là theo mặc định, khi game bị tạm dừng, mọi node sẽ bị tạm dừng. Khi một node ngừng xử lý, một số điều sẽ xảy ra.

Các hàm ``_process``, ``_physics_process``, ``_input`` và ``_input_event`` sẽ không được gọi. Tuy nhiên, các signal vẫn hoạt động và khiến hàm được kết nối của chúng chạy, ngay cả khi script của hàm đó được gắn vào một node hiện không được xử lý.

Các node animation sẽ tạm dừng animation hiện tại, các node audio sẽ tạm dừng audio stream hiện tại và particles sẽ tạm dừng. Những thành phần này sẽ tự động tiếp tục khi game không còn bị tạm dừng.

Điều quan trọng cần lưu ý là ngay cả khi một node vẫn đang xử lý trong lúc game bị tạm dừng, physics **sẽ KHÔNG** hoạt động đối với node đó theo mặc định. Như đã nêu trước đó, nguyên nhân là do các physics server đã bị tắt. Có thể kích hoạt physics server trong khi game bị tạm dừng bằng cách sử dụng các phương thức ``set_active`` của chúng.

Ví dụ về menu tạm dừng
----------------------

Trước tiên, hãy tạo một button dùng để tạm dừng game.

Tạo một menu chứa close button, đặt **Process Mode** của root node của menu thành **When Paused**, sau đó ẩn menu. Vì process mode được đặt thành **When Paused** trên root node, tất cả node con và node cháu của nó sẽ kế thừa process mode đó. Nhờ vậy, tất cả node trong menu sẽ bắt đầu xử lý khi game bị tạm dừng.

Gắn một script vào root node của menu, kết nối pause button đã tạo trước đó với một method mới trong script, rồi bên trong method đó tạm dừng game và hiển thị pause menu.

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

Cuối cùng, kết nối close button của menu với một method mới trong script. Bên trong method đó, tiếp tục game và ẩn pause menu.

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
