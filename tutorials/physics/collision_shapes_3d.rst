.. _doc_collision_shapes_3d:

Hình dạng va chạm (3D)
======================

Hướng dẫn này giải thích:

- Các loại hình dạng va chạm có sẵn trong 3D ở Godot.
- Sử dụng mesh lồi hoặc lõm làm hình dạng va chạm.
- Các lưu ý về hiệu năng liên quan đến va chạm 3D.

Godot cung cấp nhiều loại hình dạng va chạm, với những đánh đổi khác nhau về hiệu năng và độ chính xác.

Bạn có thể xác định hình dạng của một :ref:`class_PhysicsBody3D` bằng cách thêm một hoặc nhiều
:ref:`CollisionShape3Ds <class_CollisionShape3D>` làm các node con *direct*. Các node con gián tiếp (tức là các node con của node con) sẽ bị bỏ qua và không được sử dụng làm hình dạng va chạm. Ngoài ra, hãy lưu ý rằng bạn phải thêm :ref:`class_Shape3D` *resource* vào các node hình dạng va chạm trong Inspector dock.

.. note::

    Khi thêm nhiều hình dạng va chạm vào một PhysicsBody, bạn không cần lo lắng về việc chúng chồng lên nhau. Chúng sẽ không "va chạm" với nhau.

Hình dạng va chạm nguyên thủy
-----------------------------

Godot cung cấp các loại hình dạng va chạm nguyên thủy sau:

- :ref:`class_BoxShape3D`
- :ref:`class_SphereShape3D`
- :ref:`class_CapsuleShape3D`
- :ref:`class_CylinderShape3D`

Bạn có thể biểu diễn va chạm của hầu hết các vật thể nhỏ bằng một hoặc nhiều hình dạng nguyên thủy. Tuy nhiên, đối với các vật thể phức tạp hơn, chẳng hạn như một con tàu lớn hoặc toàn bộ một level, bạn có thể cần các hình dạng lồi hoặc lõm. Nội dung này sẽ được trình bày thêm bên dưới.

Chúng tôi khuyến nghị ưu tiên các hình dạng nguyên thủy cho những object động như RigidBodies và CharacterBodies, vì hành vi của chúng đáng tin cậy nhất. Chúng cũng thường mang lại hiệu năng tốt hơn.

Hình dạng va chạm lồi
---------------------

:ref:`Hình dạng va chạm lồi <class_ConvexPolygonShape3D>` là sự thỏa hiệp giữa hình dạng va chạm nguyên thủy và hình dạng va chạm lõm. Chúng có thể biểu diễn các hình dạng với mọi độ phức tạp, nhưng có một điểm cần lưu ý quan trọng. Như tên gọi cho thấy, mỗi hình dạng riêng lẻ chỉ có thể biểu diễn một hình dạng *lồi*. Ví dụ, kim tự tháp là *lồi*, nhưng một chiếc hộp rỗng là *lõm*. Để xác định một vật thể lõm bằng một hình dạng va chạm duy nhất, bạn cần sử dụng hình dạng va chạm lõm.

Tùy thuộc vào độ phức tạp của vật thể, bạn có thể đạt hiệu năng tốt hơn bằng cách sử dụng nhiều hình dạng lồi thay vì một hình dạng va chạm lõm. Godot cho phép bạn sử dụng *phân rã lồi* để tạo các hình dạng lồi gần đúng với một vật thể rỗng. Lưu ý rằng lợi thế về hiệu năng này sẽ không còn áp dụng sau một số lượng hình dạng lồi nhất định. Đối với các vật thể lớn và phức tạp như toàn bộ một level, chúng tôi khuyến nghị sử dụng các hình dạng lõm.

Bạn có thể tạo một hoặc nhiều hình dạng va chạm lồi từ editor bằng cách chọn một MeshInstance3D và sử dụng menu **Mesh** ở đầu viewport 3D. Editor cung cấp hai chế độ tạo:

- **Create Single Convex Collision Sibling** sử dụng thuật toán Quickhull. Tùy chọn này tạo một node CollisionShape với hình dạng va chạm lồi được tạo tự động. Vì chỉ tạo một hình dạng, tùy chọn này mang lại hiệu năng tốt và phù hợp với các vật thể nhỏ.

- **Create Multiple Convex Collision Siblings** sử dụng thuật toán V-HACD. Tùy chọn này tạo nhiều node CollisionShape, mỗi node có một hình dạng lồi. Vì tạo nhiều hình dạng, tùy chọn này chính xác hơn đối với các vật thể lõm nhưng phải đánh đổi bằng hiệu năng. Đối với các vật thể có độ phức tạp trung bình, tùy chọn này có thể sẽ nhanh hơn so với việc sử dụng một hình dạng va chạm lõm duy nhất.

Hình dạng va chạm lõm hoặc trimesh
----------------------------------

:ref:`Hình dạng va chạm lõm <class_ConcavePolygonShape3D>`, còn được gọi là hình dạng va chạm trimesh, có thể có bất kỳ hình dạng nào, từ vài tam giác đến hàng nghìn tam giác. Hình dạng lõm là tùy chọn chậm nhất nhưng cũng chính xác nhất trong Godot. **Bạn chỉ có thể sử dụng hình dạng lõm bên trong StaticBodies.** Chúng sẽ không hoạt động với CharacterBodies hoặc RigidBodies trừ khi mode của RigidBody là Static.

.. note::

    Mặc dù hình dạng lõm cung cấp *va chạm* chính xác nhất, việc báo cáo tiếp xúc có thể kém chính xác hơn so với hình dạng nguyên thủy.

Khi không sử dụng GridMaps để thiết kế level, hình dạng lõm là cách tiếp cận tốt nhất cho va chạm của level. Tuy vậy, nếu level của bạn có các chi tiết nhỏ, bạn có thể muốn loại chúng khỏi va chạm để cải thiện hiệu năng và cảm giác khi chơi. Để làm vậy, bạn có thể xây dựng một mesh va chạm được đơn giản hóa trong một trình tạo mô hình 3D và để Godot tự động tạo hình dạng va chạm cho mesh đó. Nội dung này sẽ được trình bày thêm bên dưới.

Lưu ý rằng không giống như hình dạng nguyên thủy và hình dạng lồi, hình dạng va chạm lõm không có "thể tích" thực tế. Bạn có thể đặt các object cả *bên ngoài* hình dạng lẫn *bên trong* hình dạng.

Bạn có thể tạo hình dạng va chạm lõm từ editor bằng cách chọn một MeshInstance3D và sử dụng menu **Mesh** ở đầu viewport 3D. Editor cung cấp hai tùy chọn:

- **Create Trimesh Static Body** là một tùy chọn tiện lợi. Tùy chọn này tạo một StaticBody chứa hình dạng lõm khớp với hình học của mesh.

- **Create Trimesh Collision Sibling** tạo một node CollisionShape với hình dạng lõm khớp với hình học của mesh.

.. seealso::

    Xem :ref:`doc_importing_3d_scenes` để biết thông tin về cách export model cho Godot và tự động tạo hình dạng va chạm khi import.

Các lưu ý về hiệu năng
----------------------

Bạn không bị giới hạn ở một hình dạng va chạm duy nhất cho mỗi PhysicsBody. Tuy nhiên, chúng tôi khuyến nghị giữ số lượng hình dạng ở mức thấp nhất có thể để cải thiện hiệu năng, đặc biệt đối với các object động như RigidBodies và CharacterBodies. Ngoài ra, hãy tránh dịch chuyển, xoay hoặc thay đổi tỷ lệ của CollisionShapes để tận dụng các tối ưu hóa nội bộ của physics engine.

Khi sử dụng một hình dạng va chạm duy nhất không bị biến đổi trong một StaticBody, thuật toán *broad phase* của engine có thể loại bỏ các PhysicsBodies không hoạt động. Khi đó, *narrow phase* chỉ cần xem xét các hình dạng của những body đang hoạt động. Nếu một StaticBody có nhiều hình dạng va chạm, broad phase sẽ không hoạt động hiệu quả. Khi đó, narrow phase, vốn chậm hơn, phải thực hiện kiểm tra va chạm với từng hình dạng.

Nếu gặp vấn đề về hiệu năng, bạn có thể phải đánh đổi về độ chính xác. Hầu hết các game hiện có đều không có va chạm chính xác 100%. Chúng tìm ra những cách sáng tạo để che giấu điều đó hoặc khiến nó không thể nhận thấy trong quá trình chơi bình thường.
