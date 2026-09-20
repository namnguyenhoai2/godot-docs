.. _doc_collision_shapes_2d:

Các hình dạng va chạm (2D)
==========================

Hướng dẫn này giải thích:

- Các loại hình dạng va chạm có sẵn trong 2D của Godot. - Sử dụng một hình ảnh được chuyển đổi thành polygon làm hình dạng va chạm. - Các cân nhắc về hiệu năng liên quan đến va chạm 2D.

Godot cung cấp nhiều loại hình dạng va chạm, với những đánh đổi khác nhau giữa hiệu năng và độ chính xác.

Bạn có thể xác định hình dạng của :ref:`class_PhysicsBody2D` bằng cách thêm một hoặc nhiều
:ref:`CollisionShape2Ds <class_CollisionShape2D>` or
:ref:`CollisionPolygon2Ds <class_CollisionPolygon2D>` as *direct* child nodes.
Các node con gián tiếp (tức là các node con của node con) sẽ bị bỏ qua và không được sử dụng làm hình dạng va chạm. Ngoài ra, lưu ý rằng bạn phải thêm một *resource* :ref:`class_Shape2D` vào các node hình dạng va chạm trong dock Inspector.

.. note::

    Khi thêm nhiều hình dạng va chạm vào một PhysicsBody2D, bạn không cần lo lắng về việc chúng chồng lấn lên nhau. Chúng sẽ không "va chạm" với nhau.

Các hình dạng va chạm nguyên thủy
---------------------------------

Godot cung cấp các loại hình dạng va chạm nguyên thủy sau:

- :ref:`class_RectangleShape2D` - :ref:`class_CircleShape2D` - :ref:`class_CapsuleShape2D` - :ref:`class_SegmentShape2D` - :ref:`class_SeparationRayShape2D` (được thiết kế cho nhân vật) - :ref:`class_WorldBoundaryShape2D` (mặt phẳng vô hạn)

Bạn có thể biểu diễn va chạm của hầu hết các vật thể nhỏ bằng một hoặc nhiều hình dạng nguyên thủy. Tuy nhiên, đối với các vật thể phức tạp hơn, chẳng hạn như một con tàu lớn hoặc toàn bộ một level, bạn có thể cần các hình dạng lồi hoặc lõm. Nội dung này sẽ được trình bày thêm bên dưới.

Chúng tôi khuyến nghị ưu tiên các hình dạng nguyên thủy cho những vật thể động như RigidBodies và CharacterBodies vì hành vi của chúng đáng tin cậy nhất. Chúng cũng thường mang lại hiệu năng tốt hơn.

Các hình dạng va chạm lồi
-------------------------

.. warning::

    Hiện tại, Godot không cung cấp cách tích hợp sẵn để tạo các hình dạng va chạm lồi 2D. Phần này chủ yếu nhằm mục đích tham khảo.

:ref:`Convex collision shapes <class_ConvexPolygonShape2D>` are a compromise
giữa các hình dạng va chạm nguyên thủy và các hình dạng va chạm lõm. Chúng có thể biểu diễn các hình dạng có độ phức tạp bất kỳ, nhưng có một điểm cần lưu ý. Như tên gọi cho thấy, mỗi hình dạng chỉ có thể biểu diễn một hình dạng *lồi*. Ví dụ, một kim tự tháp là *lồi*, nhưng một chiếc hộp rỗng là *lõm*. Để xác định một vật thể lõm bằng một hình dạng va chạm duy nhất, bạn cần sử dụng một hình dạng va chạm lõm.

Tùy thuộc vào độ phức tạp của vật thể, bạn có thể đạt được hiệu năng tốt hơn bằng cách sử dụng nhiều hình dạng lồi thay vì một hình dạng va chạm lõm. Godot cho phép bạn sử dụng *convex decomposition* để tạo ra các hình dạng lồi gần đúng với một vật thể rỗng. Lưu ý rằng lợi thế về hiệu năng này sẽ không còn áp dụng sau khi số lượng hình dạng lồi vượt quá một mức nhất định. Đối với các vật thể lớn và phức tạp như toàn bộ một level, chúng tôi khuyến nghị sử dụng các hình dạng lõm.

Các hình dạng va chạm lõm hoặc trimesh
--------------------------------------

:ref:`Concave collision shapes <class_ConcavePolygonShape2D>`, also called trimesh
các hình dạng va chạm, có thể có bất kỳ hình dạng nào, từ vài triangle đến hàng nghìn triangle. Hình dạng lõm là tùy chọn chậm nhất nhưng cũng chính xác nhất trong Godot. **Bạn chỉ có thể sử dụng các hình dạng lõm bên trong StaticBodies.** Chúng sẽ không hoạt động với CharacterBodies hoặc RigidBodies, trừ khi mode của RigidBody là Static.

.. note::

    Mặc dù các hình dạng lõm cung cấp *va chạm* chính xác nhất, việc báo cáo tiếp xúc có thể kém chính xác hơn so với các hình dạng nguyên thủy.

Khi không sử dụng TileMaps để thiết kế level, các hình dạng lõm là cách tiếp cận tốt nhất cho phần va chạm của level.

Bạn có thể cấu hình *build mode* của node CollisionPolygon2D trong inspector. Nếu được đặt thành **Solids** (mặc định), va chạm sẽ bao gồm polygon và phần diện tích bên trong nó. Nếu được đặt thành **Segments**, va chạm sẽ chỉ bao gồm các cạnh của polygon.

Bạn có thể tạo một hình dạng va chạm lõm từ editor bằng cách chọn một Sprite2D và sử dụng menu **Sprite2D** ở phía trên viewport 2D. Menu dropdown Sprite2D hiển thị một tùy chọn có tên **Create CollisionPolygon2D Sibling**. Sau khi nhấp vào đó, một menu với 3 thiết lập sẽ được hiển thị:

- **Simplification:** Giá trị càng cao thì hình dạng càng ít chi tiết, giúp cải thiện hiệu năng nhưng phải đánh đổi bằng độ chính xác. - **Shrink (Pixels):** Giá trị càng cao thì polygon va chạm được tạo sẽ càng thu nhỏ so với các cạnh của sprite. - **Grow (Pixels):** Giá trị càng cao thì polygon va chạm được tạo sẽ càng mở rộng so với các cạnh của sprite. Lưu ý rằng việc đặt Grow và Shrink thành các giá trị bằng nhau có thể cho kết quả khác với việc để cả hai ở mức 0.

.. note::

    Nếu bạn có một hình ảnh với nhiều chi tiết nhỏ, bạn nên tạo một phiên bản đơn giản hóa và sử dụng nó để tạo polygon va chạm. Điều này có thể mang lại hiệu năng và cảm giác chơi tốt hơn, vì người chơi sẽ không bị chặn bởi các chi tiết nhỏ mang tính trang trí.

    Để sử dụng một hình ảnh riêng cho việc tạo polygon va chạm, hãy tạo một Sprite2D khác, tạo một sibling polygon va chạm từ đó rồi xóa node Sprite2D. Bằng cách này, bạn có thể loại trừ các chi tiết nhỏ khỏi va chạm được tạo.

Các lưu ý về hiệu năng
----------------------

Bạn không bị giới hạn ở một hình dạng va chạm duy nhất cho mỗi PhysicsBody. Tuy vậy, chúng tôi khuyến nghị giữ số lượng hình dạng ở mức thấp nhất có thể để cải thiện hiệu năng, đặc biệt là đối với các vật thể động như RigidBodies và CharacterBodies. Ngoài ra, hãy tránh dịch chuyển, xoay hoặc scale các CollisionShapes để tận dụng các tối ưu hóa nội bộ của physics engine.

Khi sử dụng một hình dạng va chạm duy nhất không bị biến đổi trong một StaticBody, thuật toán *broad phase* của engine có thể loại bỏ các PhysicsBodies không hoạt động. Khi đó, *narrow phase* chỉ cần xét đến các hình dạng của những body đang hoạt động. Nếu một StaticBody có nhiều hình dạng va chạm, broad phase sẽ không hoạt động hiệu quả. Khi đó, narrow phase, vốn chậm hơn, phải thực hiện kiểm tra va chạm với từng hình dạng.

Nếu gặp vấn đề về hiệu năng, bạn có thể phải đánh đổi về độ chính xác. Hầu hết các game hiện nay không có va chạm chính xác 100%. Chúng tìm ra những cách sáng tạo để che giấu hoặc khiến điều đó khó nhận thấy trong quá trình chơi thông thường.
