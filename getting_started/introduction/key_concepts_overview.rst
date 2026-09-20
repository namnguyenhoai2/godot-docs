.. Mục đích: chỉ giới thiệu một số khái niệm then chốt và tránh tạo gánh nặng nhận thức quá lớn. Sau đó, người đọc sẽ được nhắc lại các khái niệm này trong những phần tiếp theo của loạt bài bắt đầu, qua đó củng cố việc học.

.. _doc_key_concepts_overview:

Tổng quan về các khái niệm then chốt của Godot
==============================================

Mọi game engine đều xoay quanh các phép trừu tượng mà bạn sử dụng để xây dựng ứng dụng. Trong Godot, một trò chơi là một **cây** gồm các **node** được bạn nhóm lại thành **scene**. Sau đó, bạn có thể kết nối các node này để chúng giao tiếp với nhau bằng **signal**.

Đây là bốn khái niệm bạn sẽ học trong phần này. Chúng ta sẽ xem xét ngắn gọn từng khái niệm để bạn hình dung cách engine hoạt động. Trong loạt bài bắt đầu, bạn sẽ được sử dụng chúng vào thực tế.

.. _doc_key_concepts_overview_scenes:

Scene
-----

Trong Godot, bạn chia trò chơi của mình thành các scene có thể tái sử dụng. Một scene có thể là một nhân vật, một vũ khí, một menu trong giao diện người dùng, một ngôi nhà riêng lẻ, toàn bộ một màn chơi hoặc bất kỳ thứ gì bạn có thể nghĩ đến. Các scene của Godot rất linh hoạt; chúng đảm nhiệm vai trò của cả prefab và scene trong một số game engine khác.

.. image:: img/key_concepts_main_menu.webp

Bạn cũng có thể lồng các scene vào nhau. Ví dụ, bạn có thể đặt nhân vật của mình vào một màn chơi và kéo thả một scene làm phần tử con của nhân vật đó.

.. image:: img/key_concepts_scene_example.webp

Node
----

Một scene được cấu thành từ một hoặc nhiều **node**. Node là những khối xây dựng nhỏ nhất của trò chơi, được bạn sắp xếp thành các cây. Sau đây là ví dụ về các node của một nhân vật.

.. image:: img/key_concepts_character_nodes.webp

Nó gồm một node ``CharacterBody2D`` có tên là "Player", một ``Camera2D``, một ``Sprite2D`` và một ``CollisionShape2D``.

.. note:: The node names end with "2D" because this is a 2D scene. Their 3D
          các phiên bản tương ứng có tên kết thúc bằng "3D". Lưu ý rằng các Node "Spatial" hiện được gọi là "Node3D" kể từ Godot 4.

Hãy chú ý rằng node và scene trông giống nhau trong trình chỉnh sửa. Khi bạn lưu một cây node thành một scene, nó sẽ hiển thị dưới dạng một node duy nhất, với cấu trúc bên trong được ẩn trong trình chỉnh sửa.

Godot cung cấp một thư viện phong phú gồm các loại node cơ sở mà bạn có thể kết hợp và mở rộng để xây dựng những node mạnh mẽ hơn. Dù là 2D, 3D hay giao diện người dùng, bạn sẽ thực hiện hầu hết mọi việc bằng các node này.

.. image:: img/key_concepts_node_menu.webp

Cây scene
---------

Tất cả scene trong trò chơi của bạn kết hợp lại trong **cây scene**, theo đúng nghĩa đen là một cây gồm các scene. Và vì scene là những cây node, cây scene cũng là một cây node. Tuy nhiên, sẽ dễ hình dung trò chơi của bạn hơn khi xét theo các scene, vì chúng có thể đại diện cho nhân vật, vũ khí, cánh cửa hoặc giao diện người dùng.

.. image:: img/key_concepts_scene_tree.webp

.. _doc_key_concepts_signals:

Signal
------

Node phát signal khi một sự kiện nào đó xảy ra. Tính năng này cho phép bạn khiến các node giao tiếp với nhau mà không cần kết nối cứng chúng trong code. Nhờ đó, bạn có rất nhiều sự linh hoạt trong cách cấu trúc các scene.

.. image:: img/key_concepts_signals.webp

.. note:: Signals are Godot's version of the *observer* pattern. You can read
          thêm về vấn đề này tại đây: https://gameprogrammingpatterns.com/observer.html

Ví dụ, các nút phát một signal khi được nhấn. Bạn có thể kết nối một đoạn code với signal này; đoạn code sẽ chạy để phản hồi sự kiện đó, chẳng hạn như bắt đầu trò chơi hoặc mở một menu.

Các signal tích hợp khác có thể cho bạn biết khi hai đối tượng va chạm, khi một nhân vật hoặc quái vật đi vào một khu vực nhất định và nhiều thông tin khác. Bạn cũng có thể định nghĩa các signal mới phù hợp với trò chơi của mình.

Tóm tắt
-------

Node, scene, cây scene và signal là bốn khái niệm cốt lõi trong Godot mà bạn sẽ thường xuyên thao tác.

Node là những khối xây dựng nhỏ nhất của trò chơi. Bạn kết hợp chúng để tạo ra các scene, sau đó kết hợp và lồng chúng vào cây scene. Tiếp theo, bạn có thể dùng signal để khiến các node phản ứng với các sự kiện trong những node khác hoặc các nhánh khác nhau của cây scene.

Sau phần phân tích ngắn này, có lẽ bạn đang có rất nhiều câu hỏi. Hãy kiên nhẫn với chúng tôi, vì bạn sẽ nhận được nhiều câu trả lời trong suốt loạt bài Getting Started.
