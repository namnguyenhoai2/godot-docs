.. _doc_immediatemesh:

Sử dụng ImmediateMesh
=====================

:ref:`ImmediateMesh <class_ImmediateMesh>` là một công cụ tiện lợi để tạo hình học động bằng API theo kiểu OpenGL 1.x. Nhờ đó, công cụ này vừa dễ tiếp cận vừa hiệu quả đối với các mesh cần được cập nhật trong mỗi frame.

Việc tạo hình học phức tạp (vài nghìn đỉnh) bằng công cụ này sẽ không hiệu quả, ngay cả khi chỉ thực hiện một lần. Thay vào đó, công cụ được thiết kế để tạo hình học đơn giản thay đổi trong mỗi frame.

Trước tiên, bạn cần tạo một :ref:`MeshInstance3D <class_meshinstance3d>` và thêm một :ref:`ImmediateMesh <class_ImmediateMesh>` vào đó trong Inspector.

Tiếp theo, thêm một script vào MeshInstance3D. Mã cho ImmediateMesh nên được đặt trong hàm ``_process()`` nếu bạn muốn cập nhật nó trong mỗi frame, hoặc trong hàm ``_ready()`` nếu bạn muốn tạo mesh một lần và không cập nhật nó. Nếu chỉ tạo một surface một lần, ImmediateMesh cũng hiệu quả như mọi loại mesh khác vì mesh được tạo sẽ được lưu vào cache và tái sử dụng.

Để bắt đầu tạo hình học, bạn phải gọi ``surface_begin()``. ``surface_begin()`` nhận một ``PrimitiveType`` làm đối số. ``PrimitiveType`` hướng dẫn GPU cách sắp xếp primitive dựa trên các đỉnh được cung cấp, cho dù đó là triangles, lines, points, v.v. Bạn có thể xem danh sách đầy đủ trên trang tham chiếu lớp :ref:`Mesh <class_mesh>`.

Sau khi gọi ``surface_begin()``, bạn có thể bắt đầu thêm các đỉnh. Bạn thêm từng đỉnh một. Trước tiên, bạn thêm các thuộc tính riêng của đỉnh như normals hoặc UVs bằng ``surface_set_****()`` (ví dụ: ``surface_set_normal()``). Sau đó, bạn gọi ``surface_add_vertex()`` để thêm một đỉnh cùng các thuộc tính đó. Ví dụ:

.. tabs::
  .. code-tab:: gdscript GDScript

    # Thêm một đỉnh với normal và uv.
    surface_set_normal(Vector3(0, 1, 0))
    surface_set_uv(Vector2(1, 1))
    surface_add_vertex(Vector3(0, 0, 1))

Chỉ các thuộc tính được thêm trước khi gọi ``surface_add_vertex()`` mới được đưa vào đỉnh đó. Nếu bạn thêm một thuộc tính hai lần trước khi gọi ``surface_add_vertex()``, chỉ lần gọi thứ hai được sử dụng.

Cuối cùng, sau khi đã thêm tất cả các đỉnh, hãy gọi ``surface_end()`` để báo hiệu rằng bạn đã hoàn tất việc tạo surface. Bạn có thể gọi ``surface_begin()`` và ``surface_end()`` nhiều lần để tạo nhiều surface cho mesh.

Đoạn mã dưới đây vẽ một triangle duy nhất trong hàm ``_ready()``.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    func _ready():
        # Bắt đầu vẽ.
        mesh.surface_begin(Mesh.PRIMITIVE_TRIANGLES)

        # Chuẩn bị các thuộc tính cho add_vertex.
        mesh.surface_set_normal(Vector3(0, 0, 1))
        mesh.surface_set_uv(Vector2(0, 0))
        # Gọi lần cuối cho mỗi đỉnh để thêm các thuộc tính ở trên.
        mesh.surface_add_vertex(Vector3(-1, -1, 0))

        mesh.surface_set_normal(Vector3(0, 0, 1))
        mesh.surface_set_uv(Vector2(0, 1))
        mesh.surface_add_vertex(Vector3(-1, 1, 0))

        mesh.surface_set_normal(Vector3(0, 0, 1))
        mesh.surface_set_uv(Vector2(1, 1))
        mesh.surface_add_vertex(Vector3(1, 1, 0))

        # Kết thúc việc vẽ.
        mesh.surface_end()

ImmediateMesh cũng có thể được sử dụng qua nhiều frame. Mỗi khi bạn gọi ``surface_begin()`` và ``surface_end()``, bạn đang thêm một surface mới vào ImmediateMesh. Nếu muốn tạo lại mesh từ đầu trong mỗi frame, hãy gọi ``clear_surfaces()`` trước khi gọi ``surface_begin()``.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends MeshInstance3D

    func _process(delta):

        # Dọn dẹp trước khi vẽ.
        mesh.clear_surfaces()

        # Bắt đầu vẽ.
        mesh.surface_begin(Mesh.PRIMITIVE_TRIANGLES)

        # Vẽ mesh.

        # Kết thúc việc vẽ.
        mesh.surface_end()

Đoạn mã trên sẽ tự động tạo và vẽ một surface duy nhất trong mỗi frame.
