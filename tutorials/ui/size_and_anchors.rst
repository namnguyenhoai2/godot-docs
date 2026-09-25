
.. _doc_size_and_anchors:

Kích thước và điểm neo
======================

Nếu một game luôn được chạy trên cùng một thiết bị và ở cùng một độ phân giải, việc định vị các control sẽ chỉ đơn giản là đặt vị trí và kích thước cho từng control. Tuy nhiên, trường hợp đó hiếm khi xảy ra.

Mặc dù một số cấu hình có thể phổ biến hơn các cấu hình khác, những thiết bị như điện thoại, máy tính bảng và máy chơi game cầm tay có thể rất khác nhau. Vì vậy, chúng ta thường phải tính đến các tỷ lệ khung hình, độ phân giải và mức scaling khác nhau của người dùng.

Có một số cách để xử lý việc này, nhưng trước mắt hãy hình dung rằng độ phân giải màn hình đã thay đổi và các control cần được định vị lại. Một số control cần bám theo cạnh dưới màn hình, số khác bám theo cạnh trên, hoặc có thể là lề phải hay lề trái.

.. image:: img/anchors.png

Việc này được thực hiện bằng cách chỉnh sửa *độ lệch điểm neo* của các control, hoạt động tương tự như margin. Để truy cập các thiết lập này, trước tiên bạn cần chọn preset điểm neo *Custom*.

Mỗi control có bốn độ lệch điểm neo: trái, phải, dưới và trên, tương ứng với các cạnh tương ứng của control. Theo mặc định, tất cả đều biểu thị khoảng cách tính bằng pixel so với góc trên bên trái của control cha hoặc (nếu không có control cha) viewport.

.. image:: img/offset.webp

Vì vậy, để làm control rộng hơn, bạn có thể tăng độ lệch phải và/hoặc giảm độ lệch trái. Cách này cho phép bạn đặt chính xác vị trí và hình dạng của control.

Các thuộc tính *điểm neo* điều chỉnh vị trí mà các độ lệch được tính tương đối *so với*. Mỗi độ lệch có một điểm neo riêng, có thể được điều chỉnh từ đầu đến cuối control cha. Vì vậy, các điểm neo theo chiều dọc (trên, dưới) được điều chỉnh từ ``0.0`` (đầu control cha) đến ``1.0`` (cuối control cha), trong đó ``0.5`` là tâm, và các độ lệch của control sẽ được đặt tương đối so với điểm đó. Tương tự, các điểm neo theo chiều ngang (trái, phải) được điều chỉnh từ trái sang phải của control cha.

Lưu ý rằng khi muốn cạnh của một control nằm phía trên hoặc bên trái điểm neo, bạn phải đặt giá trị độ lệch thành số âm.

Ví dụ: khi các điểm neo theo chiều ngang được đổi thành ``1.0``, các giá trị độ lệch sẽ được tính tương đối so với góc trên bên phải của control cha hoặc viewport.

.. image:: img/offset_end.webp

Việc đặt hai điểm neo theo chiều ngang hoặc hai điểm neo theo chiều dọc thành các giá trị khác nhau sẽ khiến kích thước của control thay đổi khi control cha thay đổi. Ở đây, control được đặt để neo góc dưới bên phải vào góc dưới bên phải của control cha, trong khi các độ lệch của góc trên bên trái của control vẫn được neo vào góc trên bên trái của control cha, vì vậy khi thay đổi kích thước control cha, control sẽ luôn phủ kín control cha và chừa ra một độ lệch 20 pixel:

.. image:: img/offset_around.webp

Căn giữa một control
--------------------

Để căn giữa một control trong control cha, đặt các điểm neo của nó thành ``0.5`` và đặt mỗi độ lệch bằng một nửa kích thước tương ứng. Ví dụ, đoạn mã dưới đây cho biết cách căn giữa một TextureRect trong control cha:

.. tabs::
 .. code-tab:: gdscript GDScript

    var rect = TextureRect.new()
    rect.texture = load("res://icon.svg")
    rect.anchor_left = 0.5
    rect.anchor_right = 0.5
    rect.anchor_top = 0.5
    rect.anchor_bottom = 0.5
    var texture_size = rect.texture.get_size()
    rect.offset_left = -texture_size.x / 2
    rect.offset_right = texture_size.x / 2
    rect.offset_top = -texture_size.y / 2
    rect.offset_bottom = texture_size.y / 2
    add_child(rect)

 .. code-tab:: csharp

    var rect = new TextureRect();

    rect.Texture = ResourceLoader.Load<Texture>("res://icon.svg");
    rect.AnchorLeft = 0.5f;
    rect.AnchorRight = 0.5f;
    rect.AnchorTop = 0.5f;
    rect.AnchorBottom = 0.5f;

    var textureSize = rect.Texture.GetSize();

    rect.OffsetLeft = -textureSize.X / 2;
    rect.OffsetRight = textureSize.X / 2;
    rect.OffsetTop = -textureSize.Y / 2;
    rect.OffsetBottom = textureSize.Y / 2;
    AddChild(rect);

Đặt mỗi điểm neo thành ``0.5`` sẽ di chuyển điểm tham chiếu của các độ lệch đến tâm của control cha. Từ đó, chúng ta đặt các độ lệch âm để control có được kích thước tự nhiên.

Preset điểm neo
---------------

Thay vì điều chỉnh thủ công các giá trị độ lệch và điểm neo, bạn có thể sử dụng menu Anchor trên thanh công cụ, phía trên viewport. Ngoài chức năng căn giữa, menu này còn cung cấp nhiều tùy chọn để căn chỉnh và thay đổi kích thước các control node.

.. image:: img/anchor_presets.webp
