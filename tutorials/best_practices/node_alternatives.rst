.. _doc_node_alternatives:

Khi nào và làm thế nào để tránh sử dụng node cho mọi thứ
========================================================

Node rất dễ tạo, nhưng ngay cả chúng cũng có giới hạn. Một project có thể có hàng chục nghìn node cùng thực hiện các tác vụ. Tuy nhiên, hành vi của chúng càng phức tạp thì mỗi node càng gây nhiều áp lực lên performance của project.

Godot cung cấp các object nhẹ hơn để tạo các API mà node sử dụng. Hãy luôn cân nhắc chúng như những lựa chọn khi thiết kế cách xây dựng các tính năng cho project của bạn.

1. :ref:`Object <class_Object>`: Object nhẹ nhất, Object nguyên bản yêu cầu quản lý bộ nhớ thủ công. Dù vậy, việc tự tạo các cấu trúc dữ liệu tùy chỉnh của riêng mình, kể cả các cấu trúc node, cũng không quá khó; và chúng còn nhẹ hơn class :ref:`Node <class_Node>`.

   - **Ví dụ:** Xem node :ref:`Tree <class_Tree>`. Nó hỗ trợ mức độ tùy biến cao cho một bảng nội dung có số hàng và cột tùy ý. Tuy nhiên, dữ liệu được dùng để tạo phần trực quan hóa của nó thực chất là một cây gồm các Object :ref:`TreeItem <class_TreeItem>`.

   - **Ưu điểm:** Đơn giản hóa API thành các object có phạm vi nhỏ hơn giúp cải thiện khả năng tiếp cận và rút ngắn thời gian lặp. Thay vì làm việc với toàn bộ thư viện Node, ta tạo một tập hợp Object rút gọn để node có thể tạo và quản lý các sub-node phù hợp.

   .. note::

       Cần cẩn thận khi xử lý chúng. Ta có thể lưu một Object vào một biến, nhưng các tham chiếu này có thể trở nên không hợp lệ mà không có cảnh báo. Ví dụ, nếu đối tượng tạo ra nó đột nhiên quyết định xóa nó, trạng thái lỗi sẽ được kích hoạt vào lần tiếp theo ta truy cập nó.

2. :ref:`RefCounted <class_RefCounted>`: Chỉ phức tạp hơn Object một chút. Chúng theo dõi các tham chiếu đến chính mình và chỉ xóa vùng nhớ đã cấp phát khi không còn tham chiếu nào khác đến chúng. Chúng hữu ích trong phần lớn trường hợp cần dữ liệu trong một class tùy chỉnh.

   - **Ví dụ:** Xem object :ref:`FileAccess <class_FileAccess>`. Nó hoạt động giống hệt một Object thông thường, ngoại trừ việc ta không cần tự xóa nó.

   - **Ưu điểm:** giống như Object.

3. :ref:`Resource <class_Resource>`: Chỉ phức tạp hơn RefCounted một chút. Chúng có khả năng tích hợp để serialize/deserialize (tức là lưu và tải) các thuộc tính object của mình vào/từ các file resource của Godot.

   - **Ví dụ:** Scripts, PackedScene (dùng cho các file scene), và các loại khác như từng class :ref:`AudioEffect <class_AudioEffect>`. Tất cả các loại này đều có thể được lưu và tải, vì vậy chúng kế thừa từ Resource.

   - **Ưu điểm:** Có rất nhiều
     :ref:`already been said <doc_resources>`
     về các ưu điểm của :ref:`Resource <class_Resource>` so với các phương pháp lưu trữ dữ liệu truyền thống. Tuy nhiên, trong bối cảnh sử dụng Resource thay cho Node, ưu điểm chính của chúng là khả năng tương thích với Inspector. Dù nhẹ gần như Object/RefCounted, chúng vẫn có thể hiển thị và export các thuộc tính trong Inspector. Điều này cho phép chúng đảm nhiệm vai trò tương tự như sub-Node về mặt khả năng sử dụng, đồng thời cải thiện performance nếu dự định có nhiều Resource/Node như vậy trong các scene của mình.
