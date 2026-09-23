.. _doc_godot_design_philosophy:

Triết lý thiết kế của Godot
===========================

Bây giờ bạn đã bắt đầu làm quen, hãy cùng tìm hiểu về thiết kế của Godot.

**Mỗi game engine đều khác nhau và phù hợp với những nhu cầu khác nhau.** Không chỉ cung cấp nhiều tính năng, thiết kế của mỗi engine cũng độc đáo. Điều này dẫn đến các quy trình làm việc khác nhau và những cách khác nhau để xây dựng cấu trúc game của bạn. Tất cả đều bắt nguồn từ triết lý thiết kế tương ứng của chúng.

Trang này giúp bạn hiểu cách Godot hoạt động, bắt đầu với một số nền tảng cốt lõi. Đây không phải là danh sách các tính năng hiện có, cũng không phải bài so sánh các engine. Để biết engine nào có phù hợp với dự án của bạn hay không, bạn cần tự mình dùng thử và hiểu thiết kế cũng như những giới hạn của nó.

Hãy xem `Godot explained in 7 minutes <https://www.youtube.com/watch?v=yS9cuu5o5Ug>`_ nếu bạn muốn có cái nhìn tổng quan về các tính năng của engine.

Thiết kế hướng đối tượng và composition
---------------------------------------

Godot lấy thiết kế hướng đối tượng làm nền tảng cốt lõi với hệ thống scene linh hoạt và hệ thống phân cấp Node. Godot cố gắng tránh các mẫu lập trình cứng nhắc để cung cấp một cách trực quan nhằm xây dựng cấu trúc game của bạn.

Trước hết, Godot cho phép bạn **compose hoặc aggregate** các scene. Nó giống như các prefab lồng nhau: bạn có thể tạo một scene BlinkingLight và một scene BrokenLantern sử dụng BlinkingLight. Sau đó, hãy tạo một thành phố chứa đầy các BrokenLantern. Thay đổi màu của BlinkingLight, lưu lại, và tất cả BrokenLantern trong thành phố sẽ được cập nhật ngay lập tức.

Ngoài ra, bạn có thể **inherit** từ bất kỳ scene nào.

Một scene Godot có thể là một Weapon, một Character, một Item, một Door, một Level, một phần của level… bất cứ thứ gì bạn muốn. Nó hoạt động như một class trong code thuần túy, ngoại trừ việc bạn được tự do thiết kế bằng editor, chỉ dùng code, hoặc kết hợp cả hai.

Điều này khác với các prefab bạn thấy trong một số 3D engine, vì sau đó bạn có thể kế thừa và mở rộng các scene đó. Bạn có thể tạo một Magician mở rộng Character. Hãy chỉnh sửa Character trong editor và Magician cũng sẽ được cập nhật. Điều này giúp bạn xây dựng dự án sao cho cấu trúc của chúng phù hợp với thiết kế game.

|image0|

Cũng cần lưu ý rằng Godot cung cấp nhiều loại đối tượng khác nhau được gọi là node, mỗi loại có một mục đích cụ thể. Node là một phần của cây và luôn kế thừa từ các node cha của chúng cho đến class Node. Mặc dù engine có một số node như các hình dạng collision mà một physics body cha sẽ sử dụng, phần lớn node hoạt động độc lập với nhau.

Nói cách khác, các node của Godot không hoạt động giống như component trong một số game engine khác.

|image1|

Sprite2D là một Node2D, một CanvasItem và một Node. Nó có tất cả thuộc tính và tính năng của ba class cha, chẳng hạn như transform hoặc khả năng vẽ các hình dạng tùy chỉnh và render bằng custom shader.

Gói tích hợp đầy đủ
-------------------

Godot cố gắng cung cấp các công cụ riêng để đáp ứng hầu hết nhu cầu phổ biến. Godot có workspace scripting chuyên dụng, animation editor, tilemap editor, shader editor, debugger, profiler, khả năng hot-reload cục bộ và trên các thiết bị từ xa, v.v.

|image2|

Mục tiêu là cung cấp một gói hoàn chỉnh để tạo game cùng trải nghiệm người dùng liền mạch. Bạn vẫn có thể làm việc với các chương trình bên ngoài, miễn là Godot có import plugin cho chương trình đó.

Đó cũng là một phần lý do Godot cung cấp ngôn ngữ lập trình riêng GDScript cùng với C#. GDScript được thiết kế cho nhu cầu của game developer và game designer, đồng thời được tích hợp chặt chẽ vào engine và editor.

GDScript cho phép bạn viết code bằng cú pháp dựa trên thụt lề, đồng thời nhận diện type và cung cấp chất lượng auto-completion của một ngôn ngữ tĩnh. GDScript cũng được tối ưu cho gameplay code với các type tích hợp như Vector và Color.

Lưu ý rằng với GDExtension, bạn có thể viết code hiệu năng cao bằng các ngôn ngữ biên dịch như C, C++, Rust, D, Haxe hoặc Swift mà không cần biên dịch lại engine.

Lưu ý rằng workspace 3D không có nhiều công cụ như workspace 2D. Bạn sẽ cần các chương trình bên ngoài hoặc add-on để chỉnh sửa địa hình, tạo animation cho các character phức tạp, v.v. Godot cung cấp một API hoàn chỉnh để mở rộng chức năng của editor bằng game code. Xem `The Godot editor is a Godot game <The Godot editor is a Godot game_>`_ bên dưới.

Mã nguồn mở
-----------

Godot cung cấp toàn bộ codebase mã nguồn mở theo **MIT license**. Điều này có nghĩa là bất kỳ ai cũng được tự do tải xuống, sử dụng, chỉnh sửa hoặc chia sẻ codebase, miễn là giữ nguyên file license của nó.

Tất cả công nghệ được cung cấp cùng Godot, bao gồm các thư viện bên thứ ba, phải tương thích hợp pháp với license mã nguồn mở này. Vì vậy, phần lớn Godot được các contributor trong cộng đồng phát triển từ đầu.

Bất kỳ ai cũng có thể tích hợp các công cụ độc quyền cho nhu cầu của dự án — chỉ là chúng sẽ không được cung cấp cùng engine. Có thể kể đến Google AdMob hoặc FMOD. Thay vào đó, bất kỳ công cụ nào trong số này đều có thể được cung cấp dưới dạng plugin bên thứ ba.

Mặt khác, codebase mở có nghĩa là bạn có thể **học hỏi từ và mở rộng engine** tùy thích. Bạn cũng có thể debug game dễ dàng, vì Godot sẽ in lỗi kèm stack trace, ngay cả khi lỗi xuất phát từ chính engine.

.. note::

   Điều này **không ảnh hưởng đến công việc bạn thực hiện với Godot** theo bất kỳ cách nào: engine và bất cứ thứ gì bạn tạo bằng nó đều không có ràng buộc nào.

Do cộng đồng phát triển
-----------------------

**Godot được cộng đồng tạo ra, vì cộng đồng và vì tất cả game creator trên thế giới.** Chính nhu cầu của người dùng và các cuộc thảo luận mở thúc đẩy những cập nhật cốt lõi. Các tính năng mới từ core developer thường tập trung trước tiên vào những gì mang lại lợi ích cho nhiều người dùng nhất.

Dù vậy, mặc dù chỉ có một nhóm nhỏ core developer làm việc toàn thời gian, tại thời điểm viết bài, dự án có hàng nghìn contributor. Những lập trình viên tâm huyết phát triển các tính năng mà chính họ có thể cần, vì vậy bạn sẽ thấy các cải tiến xuất hiện đồng thời ở mọi khía cạnh của engine trong mỗi bản phát hành lớn.

.. _`The Godot editor is a Godot game`:

Editor Godot là một game Godot
------------------------------

Editor Godot chạy trên game engine. Nó sử dụng hệ thống UI của chính engine, có thể hot-reload code và scene khi bạn kiểm thử dự án, hoặc chạy game code trong editor. Điều này có nghĩa là bạn có thể **sử dụng cùng một code** và scene cho game của mình, hoặc **xây dựng plugin và mở rộng editor.**

Điều này tạo ra một hệ thống UI đáng tin cậy và linh hoạt, vì chính nó cung cấp năng lượng cho editor. Với annotation ``@tool``, bạn có thể chạy bất kỳ game code nào trong editor.

.. figure:: img/introduction_rpg_in_a_box.webp
   :align: center

   RPG in a Box là một editor RPG voxel được tạo bằng Godot. Nó sử dụng các công cụ UI của Godot cho hệ thống lập trình dựa trên node và cho phần còn lại của giao diện.

Đặt annotation ``@tool`` ở đầu bất kỳ file GDScript nào và file đó sẽ chạy trong editor. Điều này cho phép bạn import và export plugin, tạo plugin như các level editor tùy chỉnh, hoặc tạo script với cùng các node và API mà bạn sử dụng trong dự án.

.. note::

   Trình chỉnh sửa được viết hoàn toàn bằng C++ và được biên dịch tĩnh vào binary. Điều này có nghĩa là bạn không thể import nó như một project thông thường có tệp ``project.godot``.

Các engine 2D và 3D riêng biệt
------------------------------

Godot cung cấp các engine rendering 2D và 3D chuyên dụng. Do đó, **đơn vị cơ bản cho các scene 2D là pixel.** Mặc dù các engine tách biệt, bạn vẫn có thể render 2D trong 3D, 3D trong 2D và phủ các sprite cùng interface 2D lên thế giới 3D của mình.

.. |image0| image:: img/engine_design_01.png
.. |image1| image:: img/engine_design_02.png
.. |image2| image:: img/engine_design_03.png

.. _`Godot explained in 7 minutes`: https://www.youtube.com/watch?v=yS9cuu5o5Ug
