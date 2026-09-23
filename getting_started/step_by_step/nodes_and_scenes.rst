.. The goal of this page is to explain more than doc_key_concepts_overview about nodes and scenes,
   get the user to create their first concrete scene.

.. _doc_nodes_and_scenes:

Node và Scene
=============

Trong :ref:`doc_key_concepts_overview`, chúng ta đã thấy rằng một game Godot là một cây gồm các scene và mỗi scene là một cây gồm các node. Trong bài học này, chúng ta sẽ giải thích thêm một chút về chúng. Bạn cũng sẽ tạo scene đầu tiên của mình.

Node
----

**Node là các khối xây dựng cơ bản của game của bạn**. Chúng giống như các nguyên liệu trong một công thức nấu ăn. Có hàng chục loại node có thể hiển thị hình ảnh, phát âm thanh, biểu diễn camera và nhiều hơn nữa.

.. image:: img/nodes_and_scenes_nodes.webp

Tất cả node đều có các đặc điểm sau:

- Một tên.
- Các thuộc tính có thể chỉnh sửa.
- Chúng nhận callback để cập nhật mỗi frame.
- Bạn có thể mở rộng chúng bằng các thuộc tính và hàm mới.
- Bạn có thể thêm chúng vào một node khác dưới dạng node con.

Đặc điểm cuối cùng rất quan trọng. **Các node kết hợp lại tạo thành một cây**, đây là một tính năng mạnh mẽ để tổ chức project. Vì các node khác nhau có những chức năng khác nhau, việc kết hợp chúng sẽ tạo ra hành vi phức tạp hơn. Như chúng ta đã thấy trước đây, bạn có thể xây dựng một nhân vật có thể chơi được mà camera bám theo bằng cách sử dụng node :ref:`CharacterBody2D <class_CharacterBody2D>`, node :ref:`Sprite2D <class_Sprite2D>`, node :ref:`Camera2D <class_Camera2D>` và node :ref:`CollisionShape2D <class_CollisionShape2D>`.

.. image:: img/nodes_and_scenes_character_nodes.webp

Scene
-----

Khi bạn tổ chức các node thành một cây, như nhân vật của chúng ta, chúng ta gọi cấu trúc này là một scene. Sau khi được lưu, scene hoạt động như các loại node mới trong editor, nơi bạn có thể thêm chúng làm node con của một node hiện có. Trong trường hợp đó, instance của scene xuất hiện dưới dạng một node duy nhất với các thành phần bên trong được ẩn đi.

Scene cho phép bạn cấu trúc code của game theo bất kỳ cách nào bạn muốn. Bạn có thể **kết hợp các node** để tạo các loại node tùy chỉnh và phức tạp, chẳng hạn như một nhân vật game có thể chạy và nhảy, một thanh máu, một chiếc rương mà bạn có thể tương tác và nhiều hơn nữa.

.. image:: img/nodes_and_scenes_3d_scene_example.webp

Editor Godot về cơ bản là một **scene editor**. Nó có nhiều công cụ để chỉnh sửa scene 2D và 3D, cũng như giao diện người dùng. Một project Godot có thể chứa bao nhiêu scene tùy theo nhu cầu của bạn. Engine chỉ yêu cầu một scene làm **main scene** của ứng dụng. Đây là scene mà Godot sẽ tải đầu tiên khi bạn hoặc người chơi chạy game.

Ngoài việc hoạt động như các node, scene còn có các đặc điểm sau:

1. Chúng luôn có một node gốc, giống như "Player" trong ví dụ của chúng ta.
2. Bạn có thể lưu chúng vào ổ đĩa cục bộ và tải chúng sau.
3. Bạn có thể tạo bao nhiêu instance của một scene tùy thích. Bạn có thể có năm hoặc mười nhân vật trong game, được tạo từ scene Character của mình.

Tạo scene đầu tiên
------------------

Hãy tạo scene đầu tiên với một node duy nhất. Để làm vậy, bạn cần
:ref:`tạo một project mới <doc_creating_and_importing_projects>` trước. Sau khi mở project, bạn sẽ thấy một editor trống.

.. image:: img/nodes_and_scenes_01_empty_editor.webp

Trong một scene trống, :ui:`Scene` dock ở bên trái hiển thị một số tùy chọn để nhanh chóng thêm node gốc. :button:`2D Scene` thêm một node :ref:`Node2D <class_Node2D>`,
:button:`3D Scene` thêm một node :ref:`Node3D <class_Node3D>`, còn :button:`User Interface` thêm một node :ref:`Control <class_Control>`. Các preset này nhằm tạo thuận tiện; chúng không bắt buộc.
:button:`Other Node` cho phép bạn chọn bất kỳ node nào làm node gốc. Trong một scene trống, :button:`Other Node` tương đương với việc nhấn nút :button:`Add Child Node` ở phía trên bên trái của Scene dock; nút này thường thêm một node mới làm node con của node hiện đang được chọn.

Chúng ta sẽ thêm một node :ref:`Label <class_Label>` duy nhất vào scene. Chức năng của node này là vẽ văn bản lên màn hình.

Nhấn nút :button:`Add Child Node` hoặc :button:`Other Node` để tạo node gốc.

.. image:: img/nodes_and_scenes_02_scene_dock.webp

Hộp thoại :ui:`Create New Node` mở ra, hiển thị danh sách dài các node hiện có.

.. image:: img/nodes_and_scenes_03_create_node_window.webp

Chọn node Label. Bạn có thể nhập tên của node để lọc danh sách.

.. image:: img/nodes_and_scenes_04_create_label_window.webp

Nhấp vào node Label để chọn, rồi nhấp vào nút :button:`Create` ở cuối cửa sổ.

.. image:: img/nodes_and_scenes_05_editor_with_label.webp

Nhiều thay đổi xảy ra khi bạn thêm node đầu tiên của một scene. Scene chuyển sang workspace 2D vì Label là một loại node 2D. Label xuất hiện ở góc trên bên trái của viewport và được chọn. Node xuất hiện trong Scene dock ở bên trái, còn các thuộc tính của node xuất hiện trong Inspector dock ở bên phải.

Thay đổi thuộc tính của node
----------------------------

Bước tiếp theo là thay đổi thuộc tính :inspector:`Text` của Label. Hãy đổi nó thành "Hello World".

Đi đến Inspector dock ở bên phải viewport. Nhấp vào trường bên dưới thuộc tính :inspector:`Text` và nhập "Hello World".

.. image:: img/nodes_and_scenes_06_label_text.webp

Bạn sẽ thấy văn bản được vẽ trong viewport khi nhập.

.. seealso:: Bạn có thể chỉnh sửa bất kỳ thuộc tính nào được liệt kê trong Inspector, giống như chúng ta đã làm với Text. Để xem tài liệu tham khảo đầy đủ về Inspector dock, hãy xem
             :ref:`doc_editor_inspector_dock`.

Bạn có thể di chuyển node Label trong viewport bằng cách chọn công cụ di chuyển trên thanh công cụ.

.. image:: img/nodes_and_scenes_07_move_tool.webp

Khi Label được chọn, hãy nhấp và kéo ở bất kỳ đâu trong viewport để di chuyển nó đến giữa vùng nhìn được giới hạn bởi hình chữ nhật.

.. image:: img/nodes_and_scenes_08_hello_world_text.webp

Chạy scene
----------

Mọi thứ đã sẵn sàng để chạy scene! Nhấn nút :button:`Run Current Scene` ở phía trên bên phải màn hình hoặc nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS).

.. image:: img/nodes_and_scenes_09_play_scene_button.webp

Một cửa sổ bật lên yêu cầu bạn lưu scene, đây là điều bắt buộc để chạy scene. Nhấp vào
nút :button:`Save` trong trình duyệt tệp để lưu scene với tên ``label.tscn``.

.. image:: img/nodes_and_scenes_10_save_scene_as.webp

.. note:: Hộp thoại :ui:`Save Scene As`, giống như các hộp thoại tệp khác trong editor, chỉ cho phép bạn lưu tệp bên trong project. Đường dẫn ``res://`` ở đầu cửa sổ biểu thị thư mục gốc của project và là viết tắt của "resource path". Để biết thêm thông tin về đường dẫn tệp trong Godot, hãy xem :ref:`doc_filesystem`.

Ứng dụng sẽ mở trong một cửa sổ mới và hiển thị văn bản "Hello World".

.. image:: img/nodes_and_scenes_11_final_result.webp

Đóng cửa sổ hoặc nhấn :kbd:`F8` (:kbd:`Cmd + .` trên macOS) để thoát scene đang chạy.

.. seealso::

   Xem :ref:`doc_game_embedding` để biết thêm thông tin về cửa sổ Game xuất hiện khi chạy project.

Đặt main scene
--------------

Để chạy scene kiểm thử, chúng ta đã sử dụng nút :button:`Run Current Scene`. Một nút khác bên cạnh, :button:`Run Project`, cho phép bạn đặt và chạy **main scene** của project. Bạn cũng có thể nhấn :kbd:`F5` (:kbd:`Cmd + B` trên macOS) để thực hiện việc này.

.. image:: img/nodes_and_scenes_12_play_button.webp

.. note:: Chạy *main scene* của project khác với chạy *current scene*. Nếu gặp hành vi không mong muốn, hãy kiểm tra để đảm bảo bạn đang chạy đúng scene.

Một cửa sổ bật lên xuất hiện và yêu cầu bạn chọn scene chính.

.. image:: img/nodes_and_scenes_13_main_scene_popup.webp

Nhấp vào nút :button:`Select`, rồi trong hộp thoại tệp xuất hiện, nhấp đúp vào ``label.tscn``.

.. image:: img/nodes_and_scenes_14_select_main_scene.webp

Bản demo sẽ chạy lại. Từ giờ trở đi, mỗi khi chạy project, Godot sẽ sử dụng scene này làm điểm bắt đầu.

.. note:: Trình chỉnh sửa lưu đường dẫn của scene chính trong tệp project.godot trong thư mục của project. Mặc dù bạn có thể chỉnh sửa trực tiếp tệp văn bản này để thay đổi các thiết lập của project, bạn cũng có thể sử dụng cửa sổ :menu:`Project > Project Settings` để thực hiện việc đó. Để biết thêm thông tin, hãy xem :ref:`doc_project_settings`.

Trong phần tiếp theo, chúng ta sẽ thảo luận về một khái niệm quan trọng khác trong game và Godot: tạo các instance của một scene.
