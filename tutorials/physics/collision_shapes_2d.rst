.. _doc_collision_shapes_2d:

Các hình dạng va chạm (2D)
==========================

Hướng dẫn này giải thích:

- Các loại hình dạng va chạm có sẵn trong 2D ở Godot.
- Sử dụng một hình ảnh được chuyển đổi thành polygon làm hình dạng va chạm.
- Các yếu tố cần cân nhắc về hiệu suất liên quan đến va chạm 2D.

Godot cung cấp nhiều loại hình dạng va chạm, với những đánh đổi khác nhau giữa hiệu suất và độ chính xác.

Bạn có thể xác định hình dạng của một :ref:`class_PhysicsBody2D` bằng cách thêm một hoặc nhiều
:ref:`CollisionShape2Ds <class_CollisionShape2D>` hoặc
:ref:`CollisionPolygon2Ds <class_CollisionPolygon2D>` làm các node con *direct*. Các node con gián tiếp (tức là các node con của node con) sẽ bị bỏ qua và không được sử dụng làm hình dạng va chạm. Ngoài ra, lưu ý rằng bạn phải thêm một :ref:`class_Shape2D` *resource* vào các node hình dạng va chạm trong dock Inspector.

.. note::

    Khi thêm nhiều hình dạng va chạm vào một PhysicsBody2D, bạn không cần lo lắng về việc chúng chồng lấn lên nhau. Chúng sẽ không "va chạm" với nhau.

Hình dạng va chạm nguyên thủy
-----------------------------

Godot cung cấp các loại hình dạng va chạm nguyên thủy sau:

- :ref:`class_RectangleShape2D`
- :ref:`class_CircleShape2D`
- :ref:`class_CapsuleShape2D`
- :ref:`class_SegmentShape2D`
- :ref:`class_SeparationRayShape2D` (được thiết kế cho nhân vật)
- :ref:`class_WorldBoundaryShape2D` (mặt phẳng vô hạn)

Bạn có thể biểu diễn va chạm của hầu hết các vật thể nhỏ bằng một hoặc nhiều hình dạng nguyên thủy. Tuy nhiên, với các vật thể phức tạp hơn, chẳng hạn như một con tàu lớn hoặc toàn bộ level, bạn có thể cần dùng hình dạng lồi hoặc lõm. Nội dung này sẽ được giải thích thêm bên dưới.

Chúng tôi khuyến nghị ưu tiên sử dụng hình dạng nguyên thủy cho các vật thể động như RigidBodies và CharacterBodies vì hành vi của chúng đáng tin cậy nhất. Chúng cũng thường mang lại hiệu suất tốt hơn.

Hình dạng va chạm lồi
---------------------

.. warning::

    Hiện tại Godot không cung cấp cách tích hợp sẵn để tạo hình dạng va chạm lồi 2D. Phần này chủ yếu được đưa vào để tham khảo.

:ref:`Hình dạng va chạm lồi <class_ConvexPolygonShape2D>` là sự thỏa hiệp giữa hình dạng va chạm nguyên thủy và hình dạng va chạm lõm. Chúng có thể biểu diễn các hình dạng với bất kỳ mức độ phức tạp nào, nhưng có một điểm cần lưu ý. Như tên gọi cho thấy, một hình dạng riêng lẻ chỉ có thể biểu diễn một hình dạng *lồi*. Ví dụ, kim tự tháp là *lồi*, nhưng một chiếc hộp rỗng là *lõm*. Để xác định một vật thể lõm bằng một hình dạng va chạm duy nhất, bạn cần sử dụng hình dạng va chạm lõm.

Tùy thuộc vào độ phức tạp của vật thể, bạn có thể đạt được hiệu suất tốt hơn khi sử dụng nhiều hình dạng lồi thay vì một hình dạng va chạm lõm. Godot cho phép bạn sử dụng *phân rã lồi* để tạo ra các hình dạng lồi gần khớp với một vật thể rỗng. Lưu ý rằng lợi thế về hiệu suất này sẽ không còn áp dụng sau khi số lượng hình dạng lồi vượt quá một mức nhất định. Với các vật thể lớn và phức tạp như toàn bộ level, chúng tôi khuyến nghị sử dụng hình dạng lõm.

Hình dạng va chạm lõm hoặc trimesh
----------------------------------

:ref:`Hình dạng va chạm lõm <class_ConcavePolygonShape2D>`, còn được gọi là hình dạng va chạm trimesh, có thể mang bất kỳ hình dạng nào, từ vài hình tam giác đến hàng nghìn hình tam giác. Hình dạng lõm là lựa chọn chậm nhất nhưng cũng chính xác nhất trong Godot. **Bạn chỉ có thể sử dụng hình dạng lõm bên trong StaticBodies.** Chúng sẽ không hoạt động với CharacterBodies hoặc RigidBodies, trừ khi mode của RigidBody là Static.

.. note::

    Mặc dù hình dạng lõm cung cấp *va chạm* chính xác nhất, việc báo cáo tiếp xúc có thể kém chính xác hơn so với hình dạng nguyên thủy.

Khi không sử dụng TileMaps để thiết kế level, hình dạng lõm là cách tiếp cận tốt nhất cho va chạm của level.

Bạn có thể cấu hình *chế độ xây dựng* của node CollisionPolygon2D trong inspector. Nếu được đặt thành **Solids** (mặc định), va chạm sẽ bao gồm polygon và vùng bên trong nó. Nếu được đặt thành **Segments**, va chạm sẽ chỉ bao gồm các cạnh của polygon.

Bạn có thể tạo hình dạng va chạm lõm từ editor bằng cách chọn một Sprite2D và sử dụng menu **Sprite2D** ở phía trên viewport 2D. Danh sách thả xuống của menu Sprite2D hiển thị một tùy chọn có tên **Create CollisionPolygon2D Sibling**. Sau khi nhấp vào đó, một menu có 3 thiết lập sẽ được hiển thị:

- **Simplification:** Giá trị càng cao thì hình dạng càng ít chi tiết, giúp cải thiện hiệu suất nhưng làm giảm độ chính xác.
- **Shrink (Pixels):** Giá trị càng cao thì polygon va chạm được tạo càng thu nhỏ so với các cạnh của sprite.
- **Grow (Pixels):** Giá trị càng cao thì polygon va chạm được tạo càng mở rộng so với các cạnh của sprite. Lưu ý rằng việc đặt Grow và Shrink thành các giá trị bằng nhau có thể cho kết quả khác với việc để cả hai ở mức 0.

.. note::

    Nếu bạn có một hình ảnh chứa nhiều chi tiết nhỏ, bạn nên tạo một phiên bản đơn giản hóa và sử dụng phiên bản đó để tạo polygon va chạm. Điều này có thể mang lại hiệu suất và cảm giác chơi tốt hơn, vì người chơi sẽ không bị cản bởi các chi tiết nhỏ mang tính trang trí.

    Để sử dụng một hình ảnh riêng cho việc tạo polygon va chạm, hãy tạo một Sprite2D khác, tạo node con CollisionPolygon2D từ nó rồi xóa node Sprite2D. Bằng cách này, bạn có thể loại bỏ các chi tiết nhỏ khỏi va chạm được tạo.

Lưu ý về hiệu suất
------------------

Bạn không bị giới hạn ở một hình dạng va chạm duy nhất cho mỗi PhysicsBody. Tuy vậy, chúng tôi khuyến nghị giữ số lượng hình dạng ở mức thấp nhất có thể để cải thiện hiệu suất, đặc biệt với các vật thể động như RigidBodies và CharacterBodies. Ngoài ra, hãy tránh dịch chuyển, xoay hoặc thay đổi tỷ lệ của CollisionShapes để tận dụng các tối ưu hóa nội bộ của physics engine.

Khi sử dụng một hình dạng va chạm duy nhất không bị biến đổi trong một StaticBody, thuật toán *broad phase* của engine có thể loại bỏ các PhysicsBodies không hoạt động. Khi đó, *narrow phase* chỉ cần xét đến các hình dạng của những body đang hoạt động. Nếu một StaticBody có nhiều hình dạng va chạm, broad phase sẽ không hoạt động hiệu quả. Narrow phase, vốn chậm hơn, khi đó phải thực hiện kiểm tra va chạm với từng hình dạng.

Nếu gặp vấn đề về hiệu suất, bạn có thể phải đánh đổi về độ chính xác. Hầu hết các game hiện nay đều không có va chạm chính xác 100%. Chúng tìm ra những cách sáng tạo để che giấu hoặc làm cho điều đó không dễ nhận thấy trong quá trình chơi thông thường.
