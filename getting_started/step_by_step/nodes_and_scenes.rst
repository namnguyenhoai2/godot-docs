.. Mục tiêu của trang này là giải thích nhiều hơn về doc_key_concepts_overview về các node và scene, đồng thời hướng dẫn người dùng tạo scene cụ thể đầu tiên của mình.

.. _doc_nodes_and_scenes:

Các node và scene
=================

Trong :ref:`doc_key_concepts_overview`, chúng ta đã thấy rằng một trò chơi Godot là một cây các scene và mỗi scene là một cây các node. Trong bài học này, chúng ta sẽ giải thích thêm một chút về chúng. Bạn cũng sẽ tạo scene đầu tiên của mình.

Các node
--------

**Node là những khối xây dựng cơ bản của trò chơi**. Chúng giống như các nguyên liệu trong một công thức. Có hàng chục loại node có thể hiển thị hình ảnh, phát âm thanh, đại diện cho camera và nhiều chức năng khác.

.. image:: img/nodes_and_scenes_nodes.webp

Tất cả các node đều có những đặc điểm sau:

- Tên. - Các thuộc tính có thể chỉnh sửa. - Chúng nhận các callback để cập nhật trong mỗi khung hình. - Bạn có thể mở rộng chúng bằng các thuộc tính và hàm mới. - Bạn có thể thêm chúng vào một node khác dưới dạng node con.

Đặc điểm cuối cùng rất quan trọng. **Các node kết hợp với nhau tạo thành một cây**, đây là một tính năng mạnh mẽ để tổ chức dự án. Vì các node khác nhau có những chức năng khác nhau, việc kết hợp chúng sẽ tạo ra hành vi phức tạp hơn. Như chúng ta đã thấy trước đây, bạn có thể xây dựng một nhân vật có thể điều khiển và được camera bám theo bằng cách sử dụng một node :ref:`CharacterBody2D <class_CharacterBody2D>`, một node :ref:`Sprite2D <class_Sprite2D>`, một node :ref:`Camera2D <class_Camera2D>` và một node :ref:`CollisionShape2D <class_CollisionShape2D>`.

.. image:: img/nodes_and_scenes_character_nodes.webp

Các scene
---------

Khi bạn tổ chức các node trong một cây, giống như nhân vật của chúng ta, chúng ta gọi cấu trúc này là một scene. Sau khi được lưu, các scene hoạt động như những loại node mới trong trình chỉnh sửa, nơi bạn có thể thêm chúng làm node con của một node hiện có. Trong trường hợp đó, instance của scene xuất hiện dưới dạng một node duy nhất với phần bên trong bị ẩn.

Scene cho phép bạn cấu trúc mã của trò chơi theo bất kỳ cách nào bạn muốn. Bạn có thể **kết hợp các node** để tạo ra những loại node tùy chỉnh và phức tạp, chẳng hạn như một nhân vật trò chơi có thể chạy và nhảy, một thanh máu, một chiếc rương mà bạn có thể tương tác và nhiều thứ khác.

.. image:: img/nodes_and_scenes_3d_scene_example.webp

Về bản chất, trình chỉnh sửa Godot là một **trình chỉnh sửa scene**. Nó có rất nhiều công cụ để chỉnh sửa scene 2D và 3D, cũng như giao diện người dùng. Một dự án Godot có thể chứa bao nhiêu scene tùy theo nhu cầu của bạn. Engine chỉ yêu cầu một scene làm **scene chính** của ứng dụng. Đây là scene mà Godot sẽ tải đầu tiên khi bạn hoặc người chơi chạy trò chơi.

Ngoài việc hoạt động như các node, scene còn có những đặc điểm sau:

1. Chúng luôn có một node gốc, giống như "Player" trong ví dụ của chúng ta. 2. Bạn có thể lưu chúng vào ổ đĩa cục bộ và tải chúng sau. 3. Bạn có thể tạo bao nhiêu instance của một scene tùy thích. Bạn có thể có năm hoặc mười nhân vật trong trò chơi, được tạo từ scene Character của mình.

Tạo scene đầu tiên của bạn
--------------------------

Hãy tạo scene đầu tiên với một node duy nhất. Để làm vậy, bạn sẽ cần
:ref:`create a new project <doc_creating_and_importing_projects>` first. After
sau khi mở dự án, bạn sẽ thấy một trình chỉnh sửa trống.

.. image:: img/nodes_and_scenes_01_empty_editor.webp

Trong một scene trống, dock :ui:`Scene` ở bên trái hiển thị một số tùy chọn để nhanh chóng thêm node gốc. :button:`2D Scene` thêm một node :ref:`Node2D <class_Node2D>`,
:button:`3D Scene` adds a :ref:`Node3D <class_Node3D>` node,
và :button:`User Interface` thêm một node :ref:`Control <class_Control>`. Các thiết lập sẵn này chỉ nhằm mang lại sự tiện lợi; chúng không bắt buộc.
:button:`Other Node` lets you select any node to be the root node.
Trong một scene trống, :button:`Other Node` tương đương với việc nhấn nút :button:`Add Child Node` ở phía trên bên trái của dock Scene, nút này thường thêm một node mới làm node con của node hiện đang được chọn.

Chúng ta sẽ thêm một node :ref:`Label <class_Label>` duy nhất vào scene. Chức năng của node này là vẽ văn bản trên màn hình.

Nhấn nút :button:`Add Child Node` hoặc :button:`Other Node` để tạo node gốc.

.. image:: img/nodes_and_scenes_02_scene_dock.webp

Hộp thoại :ui:`Create New Node` mở ra, hiển thị danh sách dài các node có sẵn.

.. image:: img/nodes_and_scenes_03_create_node_window.webp

Chọn node Label. Bạn có thể nhập tên của node để lọc danh sách.

.. image:: img/nodes_and_scenes_04_create_label_window.webp

Nhấp vào node Label để chọn, rồi nhấp vào nút :button:`Create` ở cuối cửa sổ.

.. image:: img/nodes_and_scenes_05_editor_with_label.webp

Có rất nhiều thay đổi xảy ra khi bạn thêm node đầu tiên của một scene. Scene chuyển sang không gian làm việc 2D vì Label là một loại node 2D. Label xuất hiện ở góc trên bên trái của viewport và được chọn. Node xuất hiện trong dock Scene ở bên trái, còn các thuộc tính của node xuất hiện trong dock Inspector ở bên phải.

Thay đổi thuộc tính của một node
--------------------------------

Bước tiếp theo là thay đổi thuộc tính :inspector:`Text` của Label. Hãy đổi nó thành "Hello World".

Đi đến dock Inspector ở bên phải viewport. Nhấp vào trường bên dưới thuộc tính :inspector:`Text` và nhập "Hello World".

.. image:: img/nodes_and_scenes_06_label_text.webp

Bạn sẽ thấy văn bản được vẽ trong viewport khi nhập.

.. seealso:: You can edit any property listed in the Inspector as we did with
             Text. Để xem tài liệu tham khảo đầy đủ về dock Inspector, hãy xem
             :ref:`doc_editor_inspector_dock`.

Bạn có thể di chuyển node Label trong viewport bằng cách chọn công cụ di chuyển trên thanh công cụ.

.. image:: img/nodes_and_scenes_07_move_tool.webp

Khi Label được chọn, hãy nhấp và kéo ở bất kỳ vị trí nào trong viewport để di chuyển nó đến giữa vùng xem được giới hạn bởi hình chữ nhật.

.. image:: img/nodes_and_scenes_08_hello_world_text.webp

Chạy scene
----------

Mọi thứ đã sẵn sàng để chạy scene! Nhấn nút :button:`Run Current Scene` ở phía trên bên phải màn hình hoặc nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS).

.. image:: img/nodes_and_scenes_09_play_scene_button.webp

Một cửa sổ bật lên yêu cầu bạn lưu scene, vì đây là điều kiện bắt buộc để chạy scene. Nhấp vào
:button:`Save` button in the file browser to save it as ``label.tscn``.

.. image:: img/nodes_and_scenes_10_save_scene_as.webp

.. note:: The :ui:`Save Scene As` dialog, like other file dialogs in the editor, only
          cho phép bạn lưu các tệp bên trong dự án. Đường dẫn ``res://`` ở đầu cửa sổ đại diện cho thư mục gốc của dự án và là viết tắt của "resource path". Để biết thêm thông tin về đường dẫn tệp trong Godot, hãy xem :ref:`doc_filesystem`.

Ứng dụng sẽ mở trong một cửa sổ mới và hiển thị văn bản "Hello World".

.. image:: img/nodes_and_scenes_11_final_result.webp

Đóng cửa sổ hoặc nhấn :kbd:`F8` (:kbd:`Cmd + .` trên macOS) để thoát scene đang chạy.

.. seealso::

   Xem :ref:`doc_game_embedding` để biết thêm thông tin về cửa sổ Game xuất hiện khi chạy dự án.

Thiết lập scene chính
---------------------

Để chạy scene thử nghiệm, chúng ta đã sử dụng nút :button:`Run Current Scene`. Một nút khác bên cạnh, :button:`Run Project`, cho phép bạn thiết lập và chạy **scene chính** của dự án. Bạn cũng có thể nhấn :kbd:`F5` (:kbd:`Cmd + B` trên macOS) để thực hiện việc này.

.. image:: img/nodes_and_scenes_12_play_button.webp

.. note:: Running the project's *main scene* is distinct from running the
          *scene hiện tại*. Nếu gặp hành vi bất ngờ, hãy kiểm tra để đảm bảo bạn đang chạy đúng scene.

Một cửa sổ bật lên xuất hiện và yêu cầu bạn chọn scene chính.

.. image:: img/nodes_and_scenes_13_main_scene_popup.webp

Nhấp vào nút :button:`Select`, rồi trong hộp thoại tệp xuất hiện, nhấp đúp vào ``label.tscn``.

.. image:: img/nodes_and_scenes_14_select_main_scene.webp

Bản demo sẽ chạy lại. Từ giờ trở đi, mỗi khi bạn chạy dự án, Godot sẽ sử dụng scene này làm điểm bắt đầu.

.. note:: The editor saves the main scene's path in a project.godot file in your
          thư mục của dự án. Mặc dù bạn có thể chỉnh sửa trực tiếp tệp văn bản này để thay đổi các thiết lập của dự án, bạn cũng có thể sử dụng cửa sổ :menu:`Project > Project Settings` để thực hiện việc đó. Để biết thêm thông tin, hãy xem :ref:`doc_project_settings`.

Trong phần tiếp theo, chúng ta sẽ thảo luận về một khái niệm quan trọng khác trong trò chơi và Godot: tạo các instance của một scene.
