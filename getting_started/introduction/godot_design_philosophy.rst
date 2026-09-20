.. _doc_godot_design_philosophy:

Triết lý thiết kế của Godot
===========================

Giờ bạn đã làm quen được phần nào, hãy cùng tìm hiểu về thiết kế của Godot.

**Mỗi game engine đều khác nhau và phù hợp với những nhu cầu khác nhau.** Chúng không chỉ cung cấp nhiều tính năng đa dạng, mà thiết kế của mỗi engine cũng độc đáo. Điều này dẫn đến những quy trình làm việc khác nhau và những cách khác nhau để hình thành cấu trúc game của bạn. Tất cả đều bắt nguồn từ triết lý thiết kế tương ứng của chúng.

Trang này giúp bạn hiểu cách Godot hoạt động, bắt đầu từ một số nền tảng cốt lõi của nó. Đây không phải là danh sách các tính năng hiện có, cũng không phải bài so sánh các engine. Để biết một engine có phù hợp với dự án của bạn hay không, bạn cần tự mình dùng thử và hiểu thiết kế cũng như những hạn chế của nó.

Hãy xem `Godot được giải thích trong 7 phút <https://www.youtube.com/watch?v=yS9cuu5o5Ug>`_ nếu bạn muốn có cái nhìn tổng quan về các tính năng của engine.

Thiết kế hướng đối tượng và kết hợp
-----------------------------------

Godot áp dụng thiết kế hướng đối tượng làm cốt lõi thông qua hệ thống scene linh hoạt và hệ thống phân cấp Node. Godot cố gắng tránh các mẫu lập trình cứng nhắc để cung cấp một cách trực quan nhằm cấu trúc game của bạn.

Trước hết, Godot cho phép bạn **kết hợp hoặc tổng hợp** các scene. Điều này giống như các prefab lồng nhau: bạn có thể tạo một scene BlinkingLight và một scene BrokenLantern sử dụng BlinkingLight. Sau đó, tạo một thành phố đầy BrokenLantern. Thay đổi màu của BlinkingLight, lưu lại, và tất cả BrokenLantern trong thành phố sẽ được cập nhật ngay lập tức.

Ngoài ra, bạn có thể **kế thừa** từ bất kỳ scene nào.

Một scene Godot có thể là một Weapon, một Character, một Item, một Door, một Level, một phần của level… bất cứ thứ gì bạn muốn. Nó hoạt động giống như một class trong mã thuần túy, nhưng bạn có thể tự do thiết kế bằng editor, chỉ sử dụng mã, hoặc kết hợp cả hai.

Điều này khác với các prefab bạn thấy trong một số engine 3D, vì sau đó bạn có thể kế thừa và mở rộng các scene đó. Bạn có thể tạo một Magician mở rộng Character. Sửa đổi Character trong editor và Magician cũng sẽ được cập nhật. Điều này giúp bạn xây dựng dự án sao cho cấu trúc của nó phù hợp với thiết kế của game.

|image0|

Cũng cần lưu ý rằng Godot cung cấp nhiều loại đối tượng khác nhau gọi là node, mỗi loại có một mục đích cụ thể. Node là một phần của cây và luôn kế thừa từ các node cha của chúng cho đến class Node. Mặc dù engine có một số node như các hình dạng va chạm mà một physics body cha sẽ sử dụng, phần lớn node hoạt động độc lập với nhau.

Nói cách khác, node của Godot không hoạt động giống như component trong một số game engine khác.

|image1|

Sprite2D là một Node2D, một CanvasItem và một Node. Nó có tất cả thuộc tính và tính năng của ba class cha, chẳng hạn như phép biến đổi hoặc khả năng vẽ các hình dạng tùy chỉnh và kết xuất bằng shader tùy chỉnh.

Gói tích hợp toàn diện
----------------------

Godot cố gắng cung cấp các công cụ riêng để đáp ứng hầu hết nhu cầu phổ biến. Godot có workspace viết script chuyên dụng, trình chỉnh sửa animation, trình chỉnh sửa tilemap, trình chỉnh sửa shader, trình gỡ lỗi, trình phân tích hiệu năng, khả năng hot-reload cục bộ và trên các thiết bị từ xa, v.v.

|image2|

Mục tiêu là cung cấp một gói đầy đủ để tạo game cùng trải nghiệm người dùng liền mạch. Bạn vẫn có thể làm việc với các chương trình bên ngoài miễn là có plugin import cho chương trình đó trong Godot.

Đó cũng là một phần lý do Godot cung cấp ngôn ngữ lập trình riêng GDScript cùng với C#. GDScript được thiết kế cho nhu cầu của các nhà phát triển game và nhà thiết kế game, đồng thời được tích hợp chặt chẽ vào engine và editor.

GDScript cho phép bạn viết mã bằng cú pháp dựa trên thụt lề, đồng thời phát hiện kiểu dữ liệu và cung cấp chất lượng tự động hoàn thành của một ngôn ngữ tĩnh. Nó cũng được tối ưu cho mã gameplay với các kiểu dựng sẵn như Vector và Color.

Lưu ý rằng với GDExtension, bạn có thể viết mã hiệu năng cao bằng các ngôn ngữ biên dịch như C, C++, Rust, D, Haxe hoặc Swift mà không cần biên dịch lại engine.

Lưu ý rằng workspace 3D không có nhiều công cụ như workspace 2D. Bạn sẽ cần các chương trình bên ngoài hoặc add-on để chỉnh sửa địa hình, tạo animation cho các nhân vật phức tạp, v.v. Godot cung cấp một API hoàn chỉnh để mở rộng chức năng của editor bằng mã game. Xem `The Godot editor is a Godot game`_ bên dưới.

Mã nguồn mở
-----------

Godot cung cấp toàn bộ codebase mã nguồn mở theo **giấy phép MIT**. Điều này có nghĩa là bất kỳ ai cũng được tự do tải xuống, sử dụng, sửa đổi hoặc chia sẻ codebase, miễn là tệp giấy phép được giữ nguyên.

Tất cả công nghệ đi kèm Godot, bao gồm các thư viện bên thứ ba, phải tương thích về mặt pháp lý với giấy phép mã nguồn mở này. Vì vậy, phần lớn Godot được các cộng tác viên trong cộng đồng phát triển từ đầu.

Bất kỳ ai cũng có thể tích hợp các công cụ độc quyền cho nhu cầu của dự án — chỉ là chúng sẽ không đi kèm engine. Những công cụ này có thể bao gồm Google AdMob hoặc FMOD. Thay vào đó, bất kỳ công cụ nào trong số này cũng có thể được cung cấp dưới dạng plugin bên thứ ba.

Mặt khác, codebase mở có nghĩa là bạn có thể **học hỏi từ engine và mở rộng engine** theo ý muốn. Bạn cũng có thể dễ dàng gỡ lỗi game, vì Godot sẽ in lỗi kèm theo stack trace, ngay cả khi lỗi xuất phát từ chính engine.

.. note::

   Điều này **không ảnh hưởng đến công việc bạn thực hiện với Godot** theo bất kỳ cách nào: không có ràng buộc nào gắn với engine hoặc bất cứ thứ gì bạn tạo ra bằng nó.

Do cộng đồng định hướng
-----------------------

**Godot được cộng đồng tạo ra, dành cho cộng đồng và cho tất cả những người sáng tạo game.** Chính nhu cầu của người dùng và những cuộc thảo luận cởi mở thúc đẩy các bản cập nhật cốt lõi. Các tính năng mới từ những nhà phát triển cốt lõi thường tập trung trước tiên vào những gì mang lại lợi ích cho nhiều người dùng nhất.

Tuy vậy, dù chỉ có một số ít nhà phát triển cốt lõi làm việc toàn thời gian, dự án đã có hàng nghìn cộng tác viên tại thời điểm viết tài liệu này. Những lập trình viên nhiệt tình phát triển các tính năng mà chính họ có thể cần, vì vậy bạn sẽ thấy các cải tiến xuất hiện ở mọi ngóc ngách của engine cùng lúc trong mỗi bản phát hành lớn.

Editor Godot là một game Godot
------------------------------

Editor Godot chạy trên game engine. Nó sử dụng hệ thống UI riêng của engine, có thể hot-reload mã và scene khi bạn kiểm thử dự án, hoặc chạy mã game trong editor. Điều này có nghĩa là bạn có thể **sử dụng cùng một đoạn mã** và các scene cho game của mình, hoặc **xây dựng plugin và mở rộng editor.**

Điều này tạo nên một hệ thống UI đáng tin cậy và linh hoạt, vì chính nó vận hành editor. Với annotation ``@tool``, bạn có thể chạy bất kỳ mã game nào trong editor.

.. figure:: img/introduction_rpg_in_a_box.webp
   :align: center

   RPG in a Box is a voxel RPG editor made with Godot. It uses Godot's
   UI tools for its node-based programming system and for the rest of the
   interface.

Đặt annotation ``@tool`` ở đầu bất kỳ tệp GDScript nào và tệp đó sẽ chạy trong editor. Điều này cho phép bạn import và export plugin, tạo plugin như các editor level tùy chỉnh, hoặc tạo script bằng chính các node và API mà bạn sử dụng trong dự án.

.. note::

   Editor được viết hoàn toàn bằng C++ và được biên dịch tĩnh vào binary. Điều này có nghĩa là bạn không thể import nó như một project thông thường có tệp ``project.godot``.

Engine 2D và 3D tách biệt
-------------------------

Godot cung cấp các engine kết xuất 2D và 3D chuyên dụng. Do đó, **đơn vị cơ sở cho các scene 2D là pixel.** Mặc dù các engine tách biệt, bạn vẫn có thể kết xuất 2D trong 3D, 3D trong 2D, cũng như phủ các sprite và interface 2D lên thế giới 3D của mình.

.. |image0| image:: img/engine_design_01.png
.. |image1| image:: img/engine_design_02.png
.. |image2| image:: img/engine_design_03.png
