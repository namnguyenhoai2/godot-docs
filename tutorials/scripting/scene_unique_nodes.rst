.. _doc_scene_unique_nodes:

Các Node duy nhất của Scene
===========================

Giới thiệu
----------

Việc sử dụng ``get_node()`` để tham chiếu đến các node từ một script đôi khi có thể dễ xảy ra lỗi. Nếu bạn di chuyển một button trong một UI scene từ panel này sang panel khác, node path của button sẽ thay đổi, và nếu một script sử dụng ``get_node()`` với node path được hard-code, script sẽ không thể tìm thấy button nữa.

Trong những tình huống như vậy, node có thể được chuyển thành scene unique node để không phải cập nhật script mỗi khi node path thay đổi.

Tạo và sử dụng
--------------

Có hai cách để tạo scene unique node.

Trong dock Scene tree, nhấp chuột phải vào một node và chọn **Access as Unique Name** trong context menu.

.. image:: img/unique_name.webp

Sau khi chọn tùy chọn này, node sẽ có biểu tượng phần trăm (**%**) bên cạnh tên của nó trong scene tree:

.. image:: img/percent.webp

Bạn cũng có thể thực hiện việc này khi đổi tên node bằng cách thêm "%" vào đầu tên. Sau khi xác nhận, biểu tượng phần trăm sẽ xuất hiện bên cạnh tên của node.

Bây giờ bạn có thể sử dụng node trong script. Ví dụ, bạn có thể tham chiếu đến node bằng một lời gọi method ``get_node()`` bằng cách nhập biểu tượng %, sau đó là tên của node:

.. tabs::

 .. code-tab:: gdscript GDScript

    get_node("%RedButton").text = "Hello"
    %RedButton.text = "Hello" # Cú pháp ngắn hơn

 .. code-tab:: csharp

    GetNode<Button>("%RedButton").Text = "Hello";

Giới hạn trong cùng Scene
-------------------------

Một scene unique node chỉ có thể được lấy bởi một node bên trong cùng scene. Để minh họa giới hạn này, hãy xem xét scene **Player** mẫu tạo một instance của scene **Sword**:

.. image:: img/unique_name_scene_instance_example.webp

Sau đây là kết quả của các lời gọi ``get_node()`` bên trong script **Player**:

- ``get_node("%Eyes")`` trả về node **Eyes**.
- ``get_node("%Hilt")`` trả về ``null``.

Sau đây là kết quả của các lời gọi ``get_node()`` bên trong script **Sword**:

- ``get_node("%Eyes")`` trả về ``null``.
- ``get_node("%Hilt")`` trả về node **Hilt**.

Nếu một script có quyền truy cập vào một node trong scene khác, nó có thể gọi ``get_node()`` trên node đó để lấy các scene unique node từ scene của node đó. Điều này cũng hoạt động trong một node path, giúp tránh nhiều lời gọi ``get_node()``. Sau đây là hai cách để lấy node **Hilt** từ script **Player** bằng scene unique node:

- ``get_node("Hand/Sword").get_node("%Hilt")`` trả về node **Hilt**.
- ``get_node("Hand/Sword/%Hilt")`` cũng trả về node **Hilt**.

Tên duy nhất của Scene không chỉ hoạt động ở cuối node path. Chúng có thể được sử dụng ở giữa để điều hướng từ node này sang node khác. Ví dụ, node **Sword** được đánh dấu là scene unique node trong scene **Player**, vì vậy điều này là khả thi:

- ``get_node("%Sword/%Hilt")`` trả về node **Hilt**.

Các lựa chọn thay thế
---------------------

Scene unique node là một công cụ hữu ích để điều hướng trong một scene. Tuy nhiên, có một số tình huống mà các kỹ thuật khác có thể phù hợp hơn.

:ref:`Group <doc_groups>` cho phép định vị một node (hoặc một nhóm gồm nhiều node) từ bất kỳ node nào khác, bất kể hai node nằm trong scene nào.

:ref:`Singleton (Autoload) <doc_singletons_autoload>` là một node luôn được load và có thể được bất kỳ node nào truy cập trực tiếp, bất kể scene. Chúng hữu ích khi một số dữ liệu hoặc chức năng được chia sẻ trên toàn cục.

:ref:`Node.find_child() <class_Node_method_find_child>` tìm một node theo tên mà không cần biết path đầy đủ của node. Điều này có vẻ tương tự như scene unique node, nhưng method này có thể tìm các node trong những scene lồng nhau và không yêu cầu đánh dấu node theo bất kỳ cách nào trong scene editor. Tuy nhiên, method này chậm. Godot cache các scene unique node và việc lấy chúng rất nhanh, nhưng mỗi khi method được gọi, ``find_child()`` phải kiểm tra mọi node con (mọi child, grandchild, v.v.).
