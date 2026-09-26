.. _doc_basic_xr_locomotion:

Di chuyển cơ bản trong XR
=========================

Đối với tính năng di chuyển cơ bản, chúng ta sẽ tiếp tục sử dụng thư viện Godot XR Tools. Thư viện này chứa cả các tính năng di chuyển cơ bản lẫn các tính năng nâng cao hơn.

Thêm thân nhân vật
------------------

Bước đầu tiên chúng ta cần thực hiện là thêm một node trợ giúp vào node :ref:`XROrigin3D <class_xrorigin3d>`. Vì XR hỗ trợ tracking theo không gian phòng, bạn không thể chỉ cần thêm thiết lập XR vào node :ref:`CharacterBody3D <class_characterbody3d>` và mong mọi thứ hoạt động. Bạn sẽ gặp vấn đề khi người dùng di chuyển trong không gian vật lý của họ và không còn đứng ở giữa phòng. Godot XR Tools tích hợp logic cần thiết vào một node trợ giúp có tên ``PlayerBody``.

Chọn node :ref:`XROrigin3D <class_xrorigin3d>` của bạn và nhấp vào nút :button:`Instantiate Child Scene` để thêm một scene con. Chọn ``addons/godot-xr-tools/player/player_body.tscn`` và thêm node này.

Thêm sàn
--------

Node này điều khiển chuyển động trong game của nhân vật và sẽ ngay lập tức phản ứng với trọng lực. Vì vậy, để ngăn nhân vật của chúng ta rơi xuống vô hạn, chúng ta sẽ nhanh chóng thêm một sàn vào scene.

Trước tiên, chúng ta thêm một node :ref:`StaticBody3D <class_staticbody3d>` vào node gốc và đổi tên node này thành ``Floor``. Chúng ta thêm một node :ref:`MeshInstance3D <class_meshinstance3d>` làm node con cho ``Floor``. Sau đó, tạo một :ref:`PlaneMesh <class_planemesh>` mới làm mesh của nó. Hiện tại, chúng ta đặt kích thước của mesh là 100 x 100 mét. Tiếp theo, chúng ta thêm một node :ref:`CollisionShape3D <class_collisionshape3d>` làm node con cho ``Floor``. Sau đó, tạo một ``BoxShape`` làm shape của nó. Chúng ta đặt kích thước của box shape này là 100 x 1 x 100 mét. Chúng ta cũng cần di chuyển collision shape xuống 0.5 mét để mặt trên của box ngang bằng với sàn.

Để dễ nhận thấy rằng chúng ta thực sự đang di chuyển trong thế giới của mình, một sàn màu trắng sẽ không phù hợp. Hãy tạo một texture bằng `trình tạo texture miễn phí tuyệt vời của Wahooney <https://wahooney.itch.io/texture-grid-generator>`_. Sau khi tạo texture, hãy thêm texture đó vào project của bạn. Sau đó, tạo một material mới cho node MeshInstance3D, thêm texture của bạn làm albedo và bật **Triplanar** trong **UV1** ở các thuộc tính material.

.. image:: img/godot_xr_tools_floor.webp

Di chuyển trực tiếp
-------------------

Chúng ta sẽ bắt đầu thêm tính năng di chuyển trực tiếp cơ bản vào thiết lập của mình. Tính năng này cho phép người dùng di chuyển trong thế giới ảo bằng đầu vào từ joystick.

.. note::
  Điều quan trọng cần lưu ý là việc di chuyển trong thế giới ảo khi người chơi đứng yên trong thế giới thực có thể gây buồn nôn, đặc biệt với những người chơi mới làm quen với VR. Các thiết lập mặc định cho những hàm di chuyển của chúng ta khá thận trọng. Chúng tôi khuyên bạn nên giữ các giá trị mặc định này, nhưng cung cấp các tính năng trong game để bật những thiết lập kém thoải mái hơn cho những người dùng có kinh nghiệm, vốn đã quen chơi game VR.

Chúng ta muốn bật tính năng này trên controller tay phải. Ta thực hiện việc này bằng cách thêm một subscene vào node :ref:`XRController3D <class_xrcontroller3d>` của tay phải. Chọn ``addons/godot-xr-tools/functions/movement_direct.tscn`` làm scene cần thêm.

Hàm này thêm chuyển động tiến và lùi cho người chơi bằng cách sử dụng joystick trên controller tay phải. Hàm cũng có tùy chọn thêm strafe trái/phải, nhưng theo mặc định tùy chọn này bị tắt.

Thay vào đó, chúng ta sẽ thêm khả năng xoay cho người chơi bằng joystick này. Chúng ta sẽ thêm một subscene khác vào node controller và chọn ``addons/godot-xr-tools/functions/movement_turn.tscn`` cho mục đích này.

Theo mặc định, hệ thống xoay sử dụng cách xoay snap. Điều này có nghĩa là việc xoay diễn ra theo từng bước. Cách này có thể gây cảm giác giật, tuy nhiên đây là một phương pháp đã được thử nghiệm và chứng minh hiệu quả trong việc chống say chuyển động. Bạn có thể dễ dàng chuyển sang chế độ xoay mượt bằng cách thay đổi thuộc tính ``mode`` trên node xoay.

Nếu chạy game vào thời điểm này, bạn sẽ thấy mình có thể tự do di chuyển trong thế giới bằng joystick tay phải.

Dịch chuyển tức thời
--------------------

Một lựa chọn thay thế cho việc di chuyển trực tiếp mà một số người dùng cảm thấy dễ chịu hơn là khả năng dịch chuyển tức thời đến một vị trí khác trong thế giới game. Godot XR Tools hỗ trợ tính năng này thông qua hàm teleport, và chúng ta sẽ thêm tính năng này vào controller tay trái.

Thêm một scene con mới vào node :ref:`XRController3D <class_xrcontroller3d>` của tay trái bằng cách chọn scene ``addons/godot-xr-tools/functions/function_teleport.tscn``.

Sau khi thêm scene này, người chơi sẽ có thể dịch chuyển tức thời trong thế giới bằng cách nhấn trigger trên controller tay trái, hướng đến nơi họ muốn đi rồi thả trigger. Người chơi cũng có thể điều chỉnh hướng bằng joystick của controller tay trái.

Nếu bạn đã làm đúng tất cả hướng dẫn, scene của bạn lúc này sẽ trông tương tự như sau:

.. image:: img/godot_xr_tools_basic_movement.webp

Các tính năng di chuyển nâng cao hơn
------------------------------------

Godot XR Tools bổ sung nhiều tính năng di chuyển khác như lượn, triển khai móc vật, jetpack, cơ chế leo trèo, v.v.

Hầu hết các tính năng này hoạt động tương tự những tính năng di chuyển cơ bản mà chúng ta đã xử lý, chỉ cần thêm subscene liên quan từ plugin vào controller triển khai tính năng đó.

Sau này trong tutorial này, chúng ta sẽ xem xét chi tiết hơn một số tính năng, trong đó có những tính năng yêu cầu thiết lập bổ sung như leo trèo; với các tính năng khác, vui lòng xem các trang trợ giúp riêng của Godot XR Tools để biết chi tiết.

.. _`Wahooneys excellent free texture generator`: https://wahooney.itch.io/texture-grid-generator
