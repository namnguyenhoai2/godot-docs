.. _doc_scene_unique_nodes:

Các nút duy nhất trong scene
============================

Giới thiệu
----------

Việc sử dụng ``get_node()`` để tham chiếu đến các nút từ một script đôi khi có thể dễ gặp lỗi. Nếu bạn di chuyển một button trong một UI scene từ panel này sang panel khác, node path của button sẽ thay đổi; và nếu một script sử dụng ``get_node()`` với node path được hard-code, script đó sẽ không thể tìm thấy button nữa.

Trong những tình huống như vậy, có thể chuyển node thành một scene unique node để không phải cập nhật script mỗi khi node path của node thay đổi.

Tạo và sử dụng
--------------

Có hai cách để tạo một scene unique node.

Trong dock Scene, nhấp chuột phải vào một node và chọn **Access as Unique Name** trong context menu.

.. image:: img/unique_name.webp

Sau khi chọn tùy chọn này, node sẽ có thêm ký hiệu phần trăm (**%**) bên cạnh tên trong scene tree:

.. image:: img/percent.webp

Bạn cũng có thể thực hiện việc này khi đổi tên node bằng cách thêm "%" vào đầu tên. Sau khi bạn xác nhận, ký hiệu phần trăm sẽ xuất hiện bên cạnh tên node.

Bây giờ bạn có thể sử dụng node trong script. Ví dụ: bạn có thể tham chiếu đến node bằng lời gọi method ``get_node()`` bằng cách nhập ký hiệu %, theo sau là tên của node:

.. tabs::

 .. code-tab:: gdscript GDScript

    get_node("%RedButton").text = "Hello"
    %RedButton.text = "Hello" # Cú pháp ngắn hơn

 .. code-tab:: csharp

    GetNode<Button>("%RedButton").Text = "Hello";

Giới hạn trong cùng scene
-------------------------

Một scene unique node chỉ có thể được lấy bởi một node nằm trong cùng scene. Để minh họa giới hạn này, hãy xem xét scene **Player** mẫu này, trong đó tạo instance của scene **Sword**:

.. image:: img/unique_name_scene_instance_example.webp

Sau đây là kết quả của các lời gọi ``get_node()`` bên trong script **Player**:

- ``get_node("%Eyes")`` trả về node **Eyes**. - ``get_node("%Hilt")`` trả về ``null``.

Sau đây là kết quả của các lời gọi ``get_node()`` bên trong script **Sword**:

- ``get_node("%Eyes")`` trả về ``null``. - ``get_node("%Hilt")`` trả về node **Hilt**.

Nếu một script có quyền truy cập vào một node trong scene khác, nó có thể gọi ``get_node()`` trên node đó để lấy các scene unique node từ scene của node đó. Điều này cũng hoạt động trong node path, giúp tránh phải gọi ``get_node()`` nhiều lần. Sau đây là hai cách lấy node **Hilt** từ script **Player** bằng scene unique node:

- ``get_node("Hand/Sword").get_node("%Hilt")`` trả về node **Hilt**. - ``get_node("Hand/Sword/%Hilt")`` cũng trả về node **Hilt**.

Tên duy nhất trong scene không chỉ hoạt động ở cuối node path. Chúng có thể được sử dụng ở giữa node path để điều hướng từ node này sang node khác. Ví dụ: node **Sword** được đánh dấu là scene unique node trong scene **Player**, vì vậy có thể thực hiện như sau:

- ``get_node("%Sword/%Hilt")`` trả về node **Hilt**.

Các lựa chọn thay thế
---------------------

Scene unique node là một công cụ hữu ích để điều hướng trong scene. Tuy nhiên, có một số tình huống mà các kỹ thuật khác có thể phù hợp hơn.

Một :ref:`Group <doc_groups>` cho phép định vị một node (hoặc một nhóm gồm nhiều node) từ bất kỳ node nào khác, bất kể hai node nằm trong scene nào.

Một :ref:`Singleton (Autoload) <doc_singletons_autoload>` là một node luôn được load và có thể được bất kỳ node nào truy cập trực tiếp, bất kể scene nào. Những node này hữu ích khi một số dữ liệu hoặc chức năng được chia sẻ trên toàn cục.

:ref:`Node.find_child() <class_Node_method_find_child>` finds a node by name
mà không cần biết full path của nó. Cách này có vẻ tương tự scene unique node, nhưng có thể tìm thấy các node trong những scene lồng nhau và không yêu cầu đánh dấu node theo bất kỳ cách nào trong scene editor. Tuy nhiên, cách này chậm. Godot cache các scene unique node nên việc lấy chúng nhanh, nhưng mỗi lần method được gọi, ``find_child()`` phải kiểm tra mọi node hậu duệ (mọi node con, node cháu, v.v.).
