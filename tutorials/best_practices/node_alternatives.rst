.. _doc_node_alternatives:

Khi nào và làm thế nào để tránh sử dụng node cho mọi thứ
========================================================

Node rất dễ tạo, nhưng ngay cả chúng cũng có những giới hạn. Một dự án có thể có hàng chục nghìn node cùng thực hiện các tác vụ. Tuy nhiên, hành vi của chúng càng phức tạp thì mỗi node càng tạo ra nhiều áp lực hơn lên hiệu năng của dự án.

Godot cung cấp các object nhẹ hơn để tạo các API mà node sử dụng. Hãy nhớ cân nhắc chúng như những lựa chọn khi thiết kế cách xây dựng các tính năng cho dự án của bạn.

1. :ref:`Object <class_Object>`: Object nguyên bản, nhẹ nhất, yêu cầu quản lý bộ nhớ thủ công. Tuy vậy, việc tạo các cấu trúc dữ liệu tùy chỉnh của riêng mình, thậm chí là các cấu trúc node, cũng không quá khó; chúng còn nhẹ hơn class :ref:`Node <class_Node>`.

   - **Ví dụ:** Xem node :ref:`Tree <class_Tree>`. Node này hỗ trợ mức độ tùy chỉnh cao cho một bảng mục lục với số hàng và cột tùy ý. Tuy nhiên, dữ liệu được sử dụng để tạo phần hiển thị thực ra là một cây gồm các Object :ref:`TreeItem <class_TreeItem>`.

   - **Ưu điểm:** Việc đơn giản hóa API thành các object có phạm vi nhỏ hơn giúp cải thiện khả năng tiếp cận và rút ngắn thời gian lặp. Thay vì làm việc với toàn bộ thư viện Node, ta tạo một tập hợp Object rút gọn để node có thể tạo và quản lý các sub-node phù hợp.

   .. note::

       Bạn nên cẩn thận khi xử lý chúng. Bạn có thể lưu một Object vào một biến, nhưng các tham chiếu này có thể trở nên không hợp lệ mà không có cảnh báo. Ví dụ, nếu tác giả của object đó quyết định xóa nó đột ngột, một trạng thái lỗi sẽ được kích hoạt vào lần tiếp theo bạn truy cập nó.

2. :ref:`RefCounted <class_RefCounted>`: Chỉ phức tạp hơn Object một chút. Chúng theo dõi các tham chiếu đến chính mình và chỉ xóa vùng nhớ đã được cấp phát khi không còn tham chiếu nào khác đến chúng. Chúng hữu ích trong phần lớn trường hợp cần dữ liệu trong một class tùy chỉnh.

   - **Ví dụ:** Xem object :ref:`FileAccess <class_FileAccess>`. Nó hoạt động giống hệt một Object thông thường, ngoại trừ việc bạn không cần tự xóa nó.

   - **Ưu điểm:** giống như Object.

3. :ref:`Resource <class_Resource>`: Chỉ phức tạp hơn RefCounted một chút. Chúng có khả năng tích hợp để serialize/deserialize (tức là lưu và tải) các thuộc tính object của mình vào/từ các tệp resource của Godot.

   - **Ví dụ:** Script, PackedScene (dùng cho các tệp scene) và các kiểu khác như từng class :ref:`AudioEffect <class_AudioEffect>`. Mỗi kiểu này đều có thể được lưu và tải, vì vậy chúng kế thừa từ Resource.

   - **Ưu điểm:** Đã có nhiều điều
     :ref:`được nói <doc_resources>` về các ưu điểm của :ref:`Resource <class_Resource>` so với các phương pháp lưu trữ dữ liệu truyền thống. Tuy nhiên, trong bối cảnh sử dụng Resource thay cho Node, ưu điểm chính của chúng là khả năng tương thích với Inspector. Dù gần như nhẹ như Object/RefCounted, chúng vẫn có thể hiển thị và export các thuộc tính trong Inspector. Điều này cho phép chúng đảm nhiệm vai trò tương tự sub-Node về mặt khả năng sử dụng, đồng thời cải thiện hiệu năng nếu bạn dự định có nhiều Resource/Node như vậy trong các scene.
