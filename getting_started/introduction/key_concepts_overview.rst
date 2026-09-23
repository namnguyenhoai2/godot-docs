.. Intention: introduce only a handful of key concepts and avoid a big cognitive
   load. Readers will then be reminded of the concepts further in the getting
   started series, reinforcing their learning.

.. _doc_key_concepts_overview:

Tổng quan về các khái niệm cốt lõi của Godot
============================================

Mọi game engine đều xoay quanh những abstraction mà bạn sử dụng để xây dựng ứng dụng. Trong Godot, một game là một **cây** gồm các **node** được bạn nhóm lại thành các **scene**. Sau đó, bạn có thể kết nối các node này để chúng giao tiếp với nhau bằng **signal**.

Đây là bốn khái niệm bạn sẽ học ở đây. Chúng ta sẽ xem qua chúng để giúp bạn hình dung cách engine hoạt động. Trong chuỗi bài hướng dẫn bắt đầu, bạn sẽ được thực hành sử dụng chúng.

.. _doc_key_concepts_overview_scenes:

Scene
-----

Trong Godot, bạn chia game của mình thành các scene có thể tái sử dụng. Một scene có thể là một nhân vật, một vũ khí, một menu trong giao diện người dùng, một ngôi nhà riêng lẻ, toàn bộ một level hoặc bất cứ thứ gì bạn có thể nghĩ ra. Các scene của Godot rất linh hoạt; chúng đảm nhiệm vai trò của cả prefab và scene trong một số game engine khác.

.. image:: img/key_concepts_main_menu.webp

Bạn cũng có thể lồng các scene vào nhau. Ví dụ, bạn có thể đặt nhân vật của mình vào một level và kéo thả một scene làm scene con của nhân vật đó.

.. image:: img/key_concepts_scene_example.webp

Node
----

Một scene được tạo thành từ một hoặc nhiều **node**. Node là những khối xây dựng nhỏ nhất của game mà bạn sắp xếp thành các cây. Sau đây là một ví dụ về các node của một nhân vật.

.. image:: img/key_concepts_character_nodes.webp

Nó gồm một node ``CharacterBody2D`` có tên là "Player", một ``Camera2D``, một ``Sprite2D`` và một ``CollisionShape2D``.

.. note:: Tên các node kết thúc bằng "2D" vì đây là một scene 2D. Các đối tượng tương ứng trong 3D có tên kết thúc bằng "3D". Lưu ý rằng các Node "Spatial" hiện được gọi là "Node3D" начиная từ Godot 4.

Hãy chú ý rằng node và scene trông giống nhau trong editor. Khi bạn lưu một cây node thành một scene, nó sẽ hiển thị dưới dạng một node duy nhất, với cấu trúc bên trong bị ẩn trong editor.

Godot cung cấp một thư viện phong phú gồm các loại node cơ sở mà bạn có thể kết hợp và mở rộng để xây dựng những node mạnh mẽ hơn. Dù là 2D, 3D hay giao diện người dùng, bạn sẽ thực hiện hầu hết mọi việc bằng các node này.

.. image:: img/key_concepts_node_menu.webp

Cây scene
---------

Tất cả scene trong game của bạn tập hợp lại trong **cây scene**, đúng nghĩa là một cây gồm các scene. Và vì scene là những cây gồm các node, cây scene cũng là một cây gồm các node. Tuy nhiên, sẽ dễ hình dung game của bạn hơn theo các scene, vì chúng có thể đại diện cho nhân vật, vũ khí, cánh cửa hoặc giao diện người dùng.

.. image:: img/key_concepts_scene_tree.webp

.. _doc_key_concepts_signals:

Signal
------

Node phát signal khi một sự kiện nào đó xảy ra. Tính năng này cho phép bạn khiến các node giao tiếp với nhau mà không cần liên kết cứng chúng trong code. Điều này mang lại cho bạn nhiều sự linh hoạt trong cách cấu trúc các scene.

.. image:: img/key_concepts_signals.webp

.. note:: Signal là phiên bản của Godot về mẫu *observer*. Bạn có thể đọc thêm về mẫu này tại đây: https://gameprogrammingpatterns.com/observer.html

Ví dụ, button phát signal khi được nhấn. Bạn có thể kết nối một đoạn code với signal này; đoạn code sẽ chạy để phản hồi sự kiện đó, chẳng hạn như bắt đầu game hoặc mở menu.

Các signal tích hợp khác có thể cho bạn biết khi hai đối tượng va chạm, khi một nhân vật hoặc quái vật đi vào một khu vực nhất định và nhiều sự kiện khác. Bạn cũng có thể định nghĩa các signal mới phù hợp với game của mình.

Tóm tắt
-------

Node, scene, cây scene và signal là bốn khái niệm cốt lõi trong Godot mà bạn sẽ thường xuyên thao tác.

Node là những khối xây dựng nhỏ nhất của game. Bạn kết hợp chúng để tạo ra các scene, sau đó tiếp tục kết hợp và lồng chúng vào cây scene. Bạn có thể dùng signal để khiến các node phản ứng với những sự kiện trong các node khác hoặc trong các nhánh khác của cây scene.

Sau phần phân tích ngắn này, có lẽ bạn có rất nhiều câu hỏi. Hãy kiên nhẫn với chúng tôi, vì bạn sẽ nhận được nhiều câu trả lời trong suốt chuỗi bài hướng dẫn Bắt đầu.
