.. _doc_instancing:

Tạo các instance
================

.. note::

   Hướng dẫn này đề cập đến việc tạo instance của các scene trong trình chỉnh sửa. Để tìm hiểu cách tạo instance của scene từ code, hãy xem :ref:`doc_nodes_and_scene_instances`.

   Cách tiếp cận của Godot đối với việc *tạo instance* được mô tả bên dưới không nên bị nhầm lẫn với hardware instancing, vốn có thể được dùng để kết xuất nhanh một lượng lớn các đối tượng tương tự. Thay vào đó, hãy xem :ref:`doc_using_multimesh`.

Trong phần trước, chúng ta đã thấy scene là một tập hợp các node được tổ chức theo cấu trúc cây, với một node duy nhất làm gốc. Bạn có thể chia dự án thành bất kỳ số lượng scene nào. Tính năng này giúp bạn phân tách và tổ chức các thành phần khác nhau trong game.

Bạn có thể tạo bao nhiêu scene tùy thích và lưu chúng thành các tệp có phần mở rộng ``.tscn``, viết tắt của "text scene". Tệp ``label.tscn`` từ bài học trước là một ví dụ. Chúng ta gọi những tệp này là "Packed Scenes" vì chúng đóng gói thông tin về nội dung scene của bạn.

Đây là một ví dụ về một quả bóng. Nó bao gồm một node :ref:`RigidBody2D <class_RigidBody2D>` làm gốc có tên là Ball, cho phép quả bóng rơi và nảy trên các bức tường, một node :ref:`Sprite2D <class_Sprite2D>`, và một
:ref:`CollisionShape2D <class_CollisionShape2D>`.

.. image:: img/instancing_ball_scene.webp

Sau khi lưu một scene, nó hoạt động như một bản thiết kế: bạn có thể tái tạo scene đó trong các scene khác bao nhiêu lần tùy thích. Việc nhân bản một đối tượng từ một mẫu như vậy được gọi là **tạo instance**.

.. image:: img/instancing_ball_instances_example.webp

Như đã đề cập trong phần trước, các scene được tạo instance hoạt động giống như một node: trình chỉnh sửa mặc định ẩn nội dung của chúng. Khi bạn tạo instance của Ball, bạn chỉ thấy node Ball. Cũng hãy chú ý rằng mỗi bản sao đều có một tên duy nhất.

Mỗi instance của scene Ball bắt đầu với cùng cấu trúc và thuộc tính như ``ball.tscn``. Tuy nhiên, bạn có thể sửa đổi từng instance một cách độc lập, chẳng hạn như thay đổi cách chúng nảy, trọng lượng của chúng hoặc bất kỳ thuộc tính nào được source scene cung cấp.

Thực hành
---------

Hãy thực hành việc tạo instance để xem nó hoạt động như thế nào trong Godot. Bạn có thể tải xuống project mẫu về quả bóng mà chúng tôi đã chuẩn bị: `instancing_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/instancing_starter.zip>`_.

Giải nén archive trên máy tính của bạn. Để import nó, bạn cần Project Manager. Có thể truy cập Project Manager bằng cách mở Godot hoặc, nếu Godot đã được mở, hãy nhấp vào :menu:`Project > Quit to Project List` (:kbd:`Ctrl + Shift + Q`, :kbd:`Ctrl + Option + Cmd + Q` trên macOS)

Trong Project Manager, nhấp vào nút :button:`Import` để import project.

.. image:: img/instancing_import_button.webp

Trong cửa sổ bật lên, hãy điều hướng đến thư mục bạn đã giải nén. Nhấp đúp vào tệp ``project.godot`` để mở tệp.

.. image:: img/instancing_import_project_file.webp

Cuối cùng, nhấp vào nút :button:`Import`.

.. image:: img/instancing_import_and_edit_button.webp

Có thể xuất hiện một cửa sổ thông báo rằng project được mở lần cuối bằng phiên bản Godot cũ hơn. Điều đó không có vấn đề gì. Nhấp vào :button:`OK` để mở project.

Project chứa hai packed scene: ``main.tscn``, chứa các bức tường mà quả bóng va chạm vào, và ``ball.tscn``. Scene Main sẽ tự động mở. Nếu bạn thấy một scene 3D trống thay vì scene chính, hãy nhấp vào nút 2D ở đầu màn hình.

.. image:: img/instancing_2d_scene_select.webp

.. image:: img/instancing_main_scene.webp

Hãy thêm một quả bóng làm node con của node Main. Trong dock Scene, chọn node Main. Sau đó, nhấp vào biểu tượng liên kết ở đầu dock Scene. Nút này cho phép bạn thêm một instance của scene làm node con của node hiện đang được chọn.

.. image:: img/instancing_scene_link_button.webp

Nhấp đúp vào scene quả bóng để tạo instance.

.. image:: img/instancing_instance_child_window.webp

Quả bóng xuất hiện ở góc trên bên trái của viewport.

.. image:: img/instancing_ball_instanced.webp

Nhấp vào nó và kéo về phía giữa khung nhìn.

.. image:: img/instancing_ball_moved.webp

Chạy game bằng cách nhấn :kbd:`F5` (:kbd:`Cmd + B` trên macOS). Bạn sẽ thấy nó rơi xuống.

Bây giờ, chúng ta muốn tạo thêm các instance của node Ball. Khi quả bóng vẫn đang được chọn, nhấn :kbd:`Ctrl + D` (:kbd:`Cmd + D` trên macOS) để gọi lệnh nhân bản. Nhấp và kéo để di chuyển quả bóng mới đến một vị trí khác.

.. image:: img/instancing_ball_duplicated.webp

Bạn có thể lặp lại quy trình này cho đến khi có nhiều quả bóng trong scene.

.. image:: img/instancing_main_scene_with_balls.webp

Chạy lại game. Bây giờ bạn sẽ thấy từng quả bóng rơi độc lập với nhau. Đó là chức năng của các instance. Mỗi instance là một bản sao độc lập của một scene mẫu.

Chỉnh sửa scene và instance
---------------------------

Instance còn có nhiều khả năng hơn. Với tính năng này, bạn có thể:

1. Thay đổi thuộc tính của một quả bóng mà không ảnh hưởng đến các quả bóng khác bằng cách sử dụng
   :ui:`Inspector`.
2. Thay đổi các thuộc tính mặc định của mọi Ball bằng cách mở scene ``ball.tscn`` và thực hiện thay đổi đối với node Ball tại đó. Sau khi lưu, tất cả instance của Ball trong project sẽ cập nhật các giá trị của chúng.

.. note:: Việc thay đổi một thuộc tính trên một instance luôn ghi đè các giá trị từ packed scene tương ứng.

Hãy thử thực hiện việc này. Nhấp đúp vào ``ball.tscn`` trong FileSystem để mở nó.

.. image:: img/instancing_ball_scene_open.webp

Trong dock Scene ở bên trái, chọn node Ball. Sau đó, trong :ui:`Inspector` ở bên phải, nhấp vào thuộc tính :inspector:`PhysicsMaterial` để mở rộng nó.

.. image:: img/instancing_physics_material_expand.webp

Đặt thuộc tính Bounce thành ``0.5`` bằng cách nhấp vào trường số, nhập ``0.5`` rồi nhấn :kbd:`Enter`.

.. image:: img/instancing_property_bounce_updated.webp

Chạy game bằng cách nhấn :kbd:`F5` (:kbd:`Cmd + B` trên macOS) và chú ý rằng tất cả các quả bóng giờ nảy nhiều hơn đáng kể. Vì scene Ball là mẫu cho tất cả các instance, việc sửa đổi và lưu scene này sẽ khiến tất cả instance cập nhật tương ứng.

Bây giờ hãy điều chỉnh một instance riêng lẻ. Quay lại scene Main bằng cách nhấp vào tab tương ứng phía trên viewport.

.. image:: img/instancing_scene_tabs.webp

Chọn một trong các node Ball được tạo instance rồi, trong :ui:`Inspector`, đặt
giá trị :inspector:`Gravity Scale` thành ``10``.

.. image:: img/instancing_property_gravity_scale.webp

Một nút "revert" màu xám xuất hiện bên cạnh thuộc tính đã điều chỉnh.

.. image:: img/instancing_property_revert_icon.webp

Biểu tượng này cho biết bạn đang ghi đè một giá trị từ packed scene nguồn. Ngay cả khi bạn sửa đổi thuộc tính trong scene gốc, giá trị ghi đè vẫn được giữ nguyên trong instance. Nhấp vào biểu tượng revert sẽ khôi phục thuộc tính về giá trị trong scene đã lưu.

Chạy lại game và chú ý rằng quả bóng này giờ rơi nhanh hơn nhiều so với những quả bóng khác.

.. note::

    Bạn có thể nhận thấy mình không thể thay đổi các giá trị của :inspector:`PhysicsMaterial` của quả bóng. Đó là vì :inspector:`PhysicsMaterial` là một *resource*, và cần được tạo thành duy nhất trước khi bạn có thể chỉnh sửa nó trong một scene đang liên kết đến scene gốc. Để tạo một resource duy nhất cho một instance, hãy nhấp chuột phải vào thuộc tính :inspector:`Physics Material` trong :ui:`Inspector` rồi nhấp vào :button:`Make Unique` trong menu ngữ cảnh.

    Resource là một khối xây dựng thiết yếu khác của các game Godot mà chúng ta sẽ đề cập trong một bài học sau.

Instance của scene như một ngôn ngữ thiết kế
--------------------------------------------

Instance và scene trong Godot tạo nên một ngôn ngữ thiết kế tuyệt vời, giúp engine này khác biệt với những engine khác. Chúng tôi đã xây dựng Godot xoay quanh khái niệm này ngay từ đầu.

Chúng tôi khuyên bạn không nên áp dụng các mẫu kiến trúc code khi làm game với Godot, chẳng hạn như Model-View-Controller (MVC) hoặc sơ đồ Entity-Relationship. Thay vào đó, bạn có thể bắt đầu bằng cách hình dung những thành phần mà người chơi sẽ nhìn thấy trong game, rồi cấu trúc code xoay quanh chúng.

Ví dụ, bạn có thể phân rã một game bắn súng như sau:

.. image:: img/instancing_diagram_shooter.png

Bạn có thể lập một sơ đồ như thế này cho gần như mọi loại game. Mỗi hình chữ nhật biểu thị một entity mà người chơi có thể nhìn thấy trong game. Các mũi tên hướng về phía đối tượng khởi tạo của mỗi scene.

Sau khi có sơ đồ, chúng tôi khuyên bạn tạo một scene cho mỗi thành phần được liệt kê trong đó để phát triển game. Bạn sẽ sử dụng instancing, bằng code hoặc trực tiếp trong editor, để xây dựng tree gồm các scene.

Lập trình viên thường dành rất nhiều thời gian để thiết kế các kiến trúc trừu tượng và cố gắng đưa các component vào đó. Thiết kế dựa trên scene giúp quá trình phát triển nhanh hơn và đơn giản hơn, cho phép bạn tập trung vào chính logic của game. Vì hầu hết component của game đều ánh xạ trực tiếp đến một scene, việc sử dụng thiết kế dựa trên khởi tạo scene có nghĩa là bạn không cần nhiều code kiến trúc bổ sung.

Sau đây là ví dụ về sơ đồ scene cho một game thế giới mở với rất nhiều asset và các thành phần lồng nhau:

.. image:: img/instancing_diagram_open_world.png

Hãy tưởng tượng chúng ta bắt đầu bằng việc tạo căn phòng. Chúng ta có thể tạo một vài scene phòng khác nhau, mỗi scene có cách sắp xếp nội thất riêng. Sau đó, chúng ta có thể tạo một scene ngôi nhà sử dụng nhiều instance phòng cho phần nội thất. Chúng ta sẽ xây dựng một thành trì từ nhiều instance ngôi nhà và một địa hình lớn để đặt thành trì lên đó. Mỗi thành phần này đều là một scene khởi tạo một hoặc nhiều sub-scene.

Sau đó, chúng ta có thể tạo các scene đại diện cho lính canh và thêm chúng vào thành trì. Chúng sẽ được thêm gián tiếp vào toàn bộ thế giới game.

Với Godot, việc lặp lại quá trình phát triển game theo cách này rất dễ dàng, vì tất cả những gì bạn cần làm là tạo và khởi tạo thêm các scene. Chúng tôi thiết kế editor để lập trình viên, designer và artist đều có thể sử dụng dễ dàng. Một quy trình phát triển điển hình của đội ngũ có thể bao gồm artist 2D hoặc 3D, level designer, game designer và animator, tất cả cùng làm việc với Godot editor.

Tóm tắt
-------

Instancing, tức quá trình tạo một object từ một bản thiết kế, có nhiều cách sử dụng hữu ích. Với scene, nó mang lại cho bạn:

- Khả năng chia game thành các component có thể tái sử dụng.
- Một công cụ để cấu trúc và đóng gói các hệ thống phức tạp.
- Một ngôn ngữ giúp bạn suy nghĩ về cấu trúc dự án game theo cách tự nhiên.

.. _`instancing_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/instancing_starter.zip
