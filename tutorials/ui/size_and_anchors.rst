
.. _doc_size_and_anchors:

Kích thước và anchor
====================

Nếu một game luôn được chạy trên cùng một thiết bị và ở cùng một độ phân giải, việc định vị các control sẽ chỉ đơn giản là đặt vị trí và kích thước cho từng control. Tuy nhiên, rất hiếm khi mọi việc lại như vậy.

Mặc dù một số cấu hình có thể phổ biến hơn những cấu hình khác, các thiết bị như điện thoại, máy tính bảng và máy chơi game cầm tay có thể khác nhau đáng kể. Vì vậy, chúng ta thường phải tính đến các tỷ lệ khung hình, độ phân giải và mức scaling của người dùng khác nhau.

Có một số cách để xử lý việc này, nhưng trước mắt, hãy chỉ hình dung rằng độ phân giải màn hình đã thay đổi và các control cần được định vị lại. Một số control sẽ cần bám theo cạnh dưới màn hình, một số khác theo cạnh trên, hoặc có thể theo lề phải hay lề trái.

.. image:: img/anchors.png

Việc này được thực hiện bằng cách chỉnh sửa *anchor offsets* của các control, hoạt động tương tự như margin. Để truy cập các thiết lập này, trước tiên bạn cần chọn preset anchor *Custom*.

Mỗi control có bốn anchor offset: left, right, bottom và top, tương ứng với các cạnh tương ứng của control. Theo mặc định, tất cả đều biểu thị khoảng cách tính bằng pixel so với góc trên bên trái của control cha hoặc (nếu không có control cha) viewport.

.. image:: img/offset.webp

Vì vậy, để làm control rộng hơn, bạn có thể tăng offset phải và/hoặc giảm offset trái. Cách này cho phép bạn thiết lập chính xác vị trí và hình dạng của control.

Các thuộc tính *anchor* điều chỉnh vị trí mà các offset được tính *tương đối với*. Mỗi offset có một anchor riêng, có thể được điều chỉnh từ đầu đến cuối của control cha. Vì vậy, các anchor dọc (top, bottom) được điều chỉnh từ ``0.0`` (đầu control cha) đến ``1.0`` (cuối control cha), trong đó ``0.5`` là tâm, và các offset của control sẽ được đặt tương đối với điểm đó. Tương tự, các anchor ngang (left, right) được điều chỉnh từ trái sang phải của control cha.

Lưu ý rằng khi muốn cạnh của một control nằm phía trên hoặc bên trái điểm anchor, bạn phải đổi giá trị offset thành số âm.

Ví dụ: khi các anchor ngang được đổi thành ``1.0``, các giá trị offset sẽ trở thành tương đối so với góc trên bên phải của control cha hoặc viewport.

.. image:: img/offset_end.webp

Điều chỉnh hai anchor ngang hoặc hai anchor dọc thành các giá trị khác nhau sẽ khiến kích thước của control thay đổi khi control cha thay đổi. Ở đây, control được thiết lập để neo góc dưới bên phải vào góc dưới bên phải của control cha, trong khi các offset của control ở góc trên bên trái vẫn được neo vào góc trên bên trái của control cha, nên khi thay đổi kích thước control cha, control sẽ luôn phủ kín nó, với một offset 20 pixel:

.. image:: img/offset_around.webp

Căn giữa một control
--------------------

Để căn giữa một control trong control cha, hãy đặt các anchor của nó thành ``0.5`` và đặt mỗi offset bằng một nửa kích thước tương ứng của nó. Ví dụ, đoạn code dưới đây cho biết cách căn giữa một TextureRect trong control cha:

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

Đặt mỗi anchor thành ``0.5`` sẽ di chuyển điểm tham chiếu của các offset đến tâm của control cha. Từ đó, chúng ta đặt các offset âm để control có được kích thước tự nhiên.

Anchor Presets
--------------

Thay vì điều chỉnh thủ công các giá trị offset và anchor, bạn có thể sử dụng menu Anchor trên thanh công cụ, phía trên viewport. Ngoài chức năng căn giữa, menu này còn cung cấp nhiều tùy chọn để căn chỉnh và thay đổi kích thước các control node.

.. image:: img/anchor_presets.webp
