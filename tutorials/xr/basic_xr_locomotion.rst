.. _doc_basic_xr_locomotion:

Di chuyển XR cơ bản
===================

Đối với việc di chuyển cơ bản, chúng ta sẽ tiếp tục sử dụng thư viện Godot XR Tools. Thư viện này bao gồm cả các tính năng di chuyển cơ bản lẫn các tính năng nâng cao hơn.

Thêm thân nhân vật của chúng ta
-------------------------------

Bước đầu tiên chúng ta cần thực hiện là thêm một helper node vào node :ref:`XROrigin3D <class_xrorigin3d>` của chúng ta. Vì XR hỗ trợ tracking theo không gian phòng, bạn không thể chỉ cần thêm thiết lập XR vào node :ref:`CharacterBody3D <class_characterbody3d>` và mong mọi thứ hoạt động bình thường. Bạn sẽ gặp vấn đề khi người dùng di chuyển trong không gian thực của họ và không còn đứng ở trung tâm phòng. Godot XR Tools nhúng logic cần thiết vào một helper node có tên ``PlayerBody``.

Chọn node :ref:`XROrigin3D <class_xrorigin3d>` của bạn và nhấp vào nút :button:`Instantiate Child Scene` để thêm một child scene. Chọn ``addons/godot-xr-tools/player/player_body.tscn`` và thêm node này.

Thêm sàn
--------

Node này điều khiển chuyển động trong game của nhân vật và sẽ ngay lập tức phản ứng với trọng lực. Vì vậy, để ngăn player của chúng ta rơi vô hạn, chúng ta sẽ nhanh chóng thêm một sàn vào scene.

Trước tiên, chúng ta thêm một node :ref:`StaticBody3D <class_staticbody3d>` vào root node và đổi tên node này thành ``Floor``. Chúng ta thêm một node :ref:`MeshInstance3D <class_meshinstance3d>` làm child node cho ``Floor`` của mình. Sau đó, tạo một :ref:`PlaneMesh <class_planemesh>` mới làm mesh của nó. Hiện tại, chúng ta đặt kích thước mesh là 100 x 100 mét. Tiếp theo, chúng ta thêm một node :ref:`CollisionShape3D <class_collisionshape3d>` làm child node cho ``Floor`` của mình. Sau đó, tạo một ``BoxShape`` làm shape của chúng ta. Chúng ta đặt kích thước của box shape này là 100 x 1 x 100 mét. Chúng ta cũng cần di chuyển collision shape xuống 0,5 mét để mặt trên của box nằm ngang với sàn.

Để dễ nhận thấy rằng chúng ta thực sự đang di chuyển trong thế giới của mình, một sàn màu trắng sẽ không đủ. Tạo một texture bằng `Wahooneys excellent free texture generator <https://wahooney.itch.io/texture-grid-generator>`_. Sau khi tạo texture, hãy thêm texture đó vào project của bạn. Sau đó, tạo một material mới cho node MeshInstance3D, thêm texture của bạn làm albedo và bật **Triplanar** bên dưới **UV1** trong các thuộc tính của material.

.. image:: img/godot_xr_tools_floor.webp

Di chuyển trực tiếp
-------------------

Chúng ta sẽ bắt đầu thêm một số tính năng di chuyển trực tiếp cơ bản vào thiết lập của mình. Tính năng này cho phép người dùng di chuyển trong thế giới ảo bằng input từ joystick.

.. note::
  Điều quan trọng cần lưu ý là việc di chuyển trong thế giới ảo trong khi player đứng yên ở thế giới thực có thể gây buồn nôn, đặc biệt đối với những người chơi mới làm quen với VR. Các thiết lập mặc định cho các hàm di chuyển của chúng ta khá thận trọng. Chúng tôi khuyên bạn nên giữ các thiết lập mặc định này, nhưng cung cấp các tính năng trong game để bật những thiết lập kém thoải mái hơn cho người dùng có kinh nghiệm, vốn đã quen với việc chơi game VR.

Chúng ta muốn bật tính năng này trên controller tay phải. Chúng ta thực hiện bằng cách thêm một subscene vào node :ref:`XRController3D <class_xrcontroller3d>` của tay phải. Chọn ``addons/godot-xr-tools/functions/movement_direct.tscn`` làm scene cần thêm.

Hàm này thêm chuyển động tiến và lùi cho player bằng cách sử dụng joystick trên controller tay phải. Hàm cũng có tùy chọn thêm strafe trái/phải, nhưng tùy chọn này bị tắt theo mặc định.

Thay vào đó, chúng ta sẽ thêm khả năng xoay cho player bằng joystick này. Chúng ta sẽ thêm một subscene khác vào controller node của mình và chọn ``addons/godot-xr-tools/functions/movement_turn.tscn`` cho mục này.

Theo mặc định, hệ thống xoay sử dụng phương pháp snap turn. Điều này có nghĩa là việc xoay diễn ra theo từng bước. Cách này có thể gây cảm giác giật, tuy nhiên đây là một phương pháp đã được thử nghiệm và chứng minh hiệu quả trong việc chống say chuyển động. Bạn có thể dễ dàng chuyển sang chế độ cung cấp khả năng xoay mượt bằng cách thay đổi thuộc tính ``mode`` trên turn node.

Nếu chạy game vào thời điểm này, bạn sẽ thấy mình có thể tự do di chuyển trong thế giới bằng joystick tay phải.

Dịch chuyển tức thời
--------------------

Một lựa chọn thay thế cho việc di chuyển trực tiếp mà một số người dùng cảm thấy dễ chịu hơn là khả năng dịch chuyển đến một vị trí khác trong thế giới game. Godot XR Tools hỗ trợ tính năng này thông qua chức năng teleport và chúng ta sẽ thêm nó vào controller tay trái.

Thêm một child scene mới vào node :ref:`XRController3D <class_xrcontroller3d>` tay trái bằng cách chọn scene ``addons/godot-xr-tools/functions/function_teleport.tscn``.

Sau khi thêm scene này, player sẽ có thể dịch chuyển trong thế giới bằng cách nhấn trigger trên controller tay trái, hướng đến nơi họ muốn đi rồi nhả trigger. Player cũng có thể điều chỉnh hướng bằng joystick của controller tay trái.

Nếu bạn đã làm theo đúng tất cả hướng dẫn, scene của bạn bây giờ sẽ trông tương tự như sau:

.. image:: img/godot_xr_tools_basic_movement.webp

Các tính năng di chuyển nâng cao hơn
------------------------------------

Godot XR Tools bổ sung nhiều tính năng di chuyển khác như lượn, triển khai grapple hook, jetpack, cơ chế leo trèo, v.v.

Hầu hết các tính năng này hoạt động tương tự như những tính năng di chuyển cơ bản mà chúng ta đã xử lý cho đến nay: chỉ cần thêm subscene liên quan từ plugin vào controller triển khai tính năng đó.

Chúng ta sẽ xem xét một số tính năng này chi tiết hơn ở phần sau của tutorial, nơi cần có thêm thiết lập (chẳng hạn như tính năng leo trèo), nhưng đối với các tính năng khác, vui lòng xem các trang trợ giúp riêng của Godot XR Tools để biết thêm chi tiết.
