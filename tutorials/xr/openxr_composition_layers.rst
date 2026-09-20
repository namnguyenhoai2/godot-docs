.. _doc_openxr_composition_layers:

Các lớp composition của OpenXR
==============================

Giới thiệu
----------

Trong các game XR, nhìn chung bạn muốn tạo ra những tương tác của người dùng diễn ra trong không gian 3D và liên quan đến việc người dùng chạm vào các đối tượng như thể họ đang chạm vào chúng ngoài đời thực.

Tuy nhiên, đôi khi việc tạo một giao diện 2D truyền thống hơn là điều không thể tránh khỏi. Nhưng trong XR, bạn không thể chỉ thêm các thành phần 2D vào scene. Godot cần thông tin về chiều sâu để định vị đúng các phần tử này, sao cho chúng xuất hiện ở vị trí thoải mái đối với người dùng. Ngay cả khi có thông tin về chiều sâu, một số headset có màn hình nghiêng khiến pipeline 2D tiêu chuẩn không thể render chính xác các phần tử 2D.

Giải pháp là render UI vào một :ref:`SubViewport <class_subviewport>` rồi hiển thị kết quả bằng :ref:`ViewportTexture <class_viewporttexture>` trên một mesh 3D. :ref:`QuadMesh <class_quadmesh>` là một lựa chọn phù hợp cho việc này.

.. note::
    Xem project mẫu `GUI in 3D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/gui_in_3d>`_ để biết ví dụ về cách tiếp cận này.

Vấn đề khi hiển thị viewport theo cách này là kết quả đã render sẽ được XR runtime lấy mẫu để biến dạng theo thấu kính, và chất lượng suy giảm do đó có thể khiến văn bản UI khó đọc.

OpenXR cung cấp giải pháp cho vấn đề này thông qua các composition layer. Với composition layer, nội dung của viewport có thể được chiếu lên một bề mặt sau khi biến dạng theo thấu kính, mang lại kết quả cuối cùng có chất lượng cao hơn nhiều.

.. note::
    Vì không phải mọi XR runtime đều hỗ trợ tất cả các loại composition layer, Godot triển khai một giải pháp fallback, trong đó viewport được render như một phần của scene thông thường nhưng vẫn có những hạn chế về chất lượng đã nêu ở trên.

.. warning::
    Khi composition layer được hỗ trợ, chính XR runtime sẽ hiển thị subviewport. Điều này có nghĩa là UI chỉ hiển thị trong headset, Godot không thể truy cập vào UI và do đó UI sẽ không được hiển thị khi bạn xem spectator view trên desktop.

Hiện tại có 3 node cung cấp chức năng này:

- :ref:`OpenXRCompositionLayerCylinder <class_OpenXRCompositionLayerCylinder>` hiển thị nội dung của SubViewport ở mặt trong của một hình trụ (hoặc "lát cắt" của hình trụ). - :ref:`OpenXRCompositionLayerEquirect <class_OpenXRCompositionLayerEquirect>` hiển thị nội dung của SubViewport ở mặt trong của một hình cầu (hoặc "lát cắt" của hình cầu). - :ref:`OpenXRCompositionLayerQuad <class_OpenXRCompositionLayerQuad>` hiển thị nội dung của SubViewport trên một hình chữ nhật phẳng.

Thiết lập SubViewport
---------------------

Bước đầu tiên là thêm một SubViewport cho UI 2D của chúng ta; việc này không yêu cầu bước đặc biệt nào. Trong ví dụ của mình, chúng ta đánh dấu viewport là trong suốt.

Bây giờ bạn có thể tạo UI 2D bằng cách thêm các node con vào SubViewport như bình thường. Bạn nên lưu UI 2D trong một subscene; điều này giúp bạn dễ dàng thực hiện layout hơn.

.. image:: img/openxr_composition_layer_subviewport.webp

.. warning::
    Chế độ cập nhật "When Visible" sẽ không hoạt động vì Godot không thể xác định viewport có hiển thị với người dùng hay không. Khi gán viewport của chúng ta cho một composition layer, Godot sẽ tự động điều chỉnh chế độ này.

Thêm composition layer
----------------------

Bước thứ hai là thêm composition layer. Chúng ta có thể thêm node composition layer phù hợp làm node con của node :ref:`XROrigin3D <class_xrorigin3d>`. Điều này rất quan trọng vì XR runtime định vị mọi thứ theo mối quan hệ với origin của chúng ta.

Chúng ta muốn định vị composition layer sao cho nó ở độ cao ngang tầm mắt và cách người chơi khoảng 1 đến 1,5 mét.

Bây giờ chúng ta gán SubViewport cho thuộc tính ``Layer Viewport`` và bật Alpha Blend.

.. image:: img/openxr_composition_layer_quad.webp

.. note::
    Vì người chơi có thể đi ra xa điểm origin, bạn sẽ muốn định vị lại composition layer khi người chơi căn giữa lại góc nhìn. Sử dụng reference space ``Local Floor`` sẽ tự động áp dụng logic này.

Làm cho giao diện hoạt động
---------------------------

Cho đến giờ chúng ta mới chỉ hiển thị UI; để UI hoạt động, chúng ta cần thêm một số code. Trong ví dụ này, chúng ta sẽ giữ mọi thứ đơn giản và dùng một trong các controller làm pointer. Sau đó, chúng ta sẽ mô phỏng các thao tác chuột bằng pointer này.

Code này cũng yêu cầu thêm một node ``MeshInstance3D`` có tên ``Pointer`` làm node con của node ``OpenXRCompositionLayerQuad``. Chúng ta cấu hình một ``SphereMesh`` với bán kính ``0.01`` mét. Chúng ta sẽ dùng nó làm trợ giúp để trực quan hóa vị trí người dùng đang trỏ tới.

Hàm chính điều khiển chức năng này là hàm ``intersects_ray`` trên node composition layer của chúng ta. Hàm này nhận vị trí và hướng toàn cục của pointer, rồi trả về UV tại vị trí tia của chúng ta giao với viewport. Hàm trả về ``Vector2(-1.0, -1.0)`` nếu chúng ta không trỏ vào viewport.

Chúng ta bắt đầu bằng việc thiết lập một số biến; ở đây quan trọng là các biến export, dùng để xác định node controller mà chúng ta sử dụng để trỏ vào màn hình.

.. code:: gdscript

    extends OpenXRCompositionLayerQuad

    const NO_INTERSECTION = Vector2(-1.0, -1.0)

    @export var controller : XRController3D
    @export var button_action : String = "trigger_click"

    var was_pressed : bool = false
    var was_intersect : Vector2 = NO_INTERSECTION

    ...

Tiếp theo, chúng ta định nghĩa một hàm trợ giúp nhận giá trị được trả về từ ``intersects_ray`` và cung cấp vị trí toàn cục của điểm giao đó. Cách triển khai này chỉ hoạt động với node ``OpenXRCompositionLayerQuad`` của chúng ta.

.. code:: gdscript

    ...

    func _intersect_to_global_pos(intersect : Vector2) -> Vector3:
        if intersect != NO_INTERSECTION:
            var local_pos : Vector2 = (intersect - Vector2(0.5, 0.5)) * quad_size
            return global_transform * Vector3(local_pos.x, -local_pos.y, 0.0)
        else:
            return Vector3()

    ...

Chúng ta cũng định nghĩa một hàm trợ giúp nhận giá trị ``intersect`` và trả về vị trí của chúng ta trong hệ tọa độ cục bộ của viewport:

.. code:: gdscript

    ...

    func _intersect_to_viewport_pos(intersect : Vector2) -> Vector2i:
        if layer_viewport and intersect != NO_INTERSECTION:
            var pos : Vector2 = intersect * Vector2(layer_viewport.size)
            return Vector2i(pos)
        else:
            return Vector2i(-1, -1)

    ...

Logic chính diễn ra trong hàm ``_process``. Trước tiên, chúng ta ẩn pointer, sau đó kiểm tra xem mình có controller và viewport hợp lệ hay không, rồi gọi ``intersects_ray`` với vị trí và hướng của controller:

.. code:: gdscript

    ...

    # Được gọi ở mỗi frame. 'delta' là khoảng thời gian đã trôi qua kể từ frame trước đó.
    func _process(_delta):
        # Ẩn pointer; chúng ta sẽ hiển thị nó nếu đang tương tác với viewport.
        $Pointer.visible = false

        if controller and layer_viewport:
            var controller_t : Transform3D = controller.global_transform
            var intersect : Vector2 = intersects_ray(controller_t.origin, -controller_t.basis.z)

    ...

Tiếp theo, chúng ta kiểm tra xem có đang giao với viewport hay không. Nếu có, chúng ta kiểm tra xem button đã được nhấn chưa và đặt pointer tại điểm giao của chúng ta.

.. code:: gdscript

    ...

            if intersect != NO_INTERSECTION:
                var is_pressed : bool = controller.is_button_pressed(button_action)

                # Đặt pointer tại vị trí chúng ta đang trỏ tới
                var pos : Vector3 = _intersect_to_global_pos(intersect)
                $Pointer.visible = true
                $Pointer.global_position = pos

    ...

Nếu chúng ta đã giao với viewport trong lần gọi process trước đó và pointer đã di chuyển, chúng ta chuẩn bị một đối tượng :ref:`InputEventMouseMotion <class_InputEventMouseMotion>` để mô phỏng thao tác di chuyển chuột, rồi gửi đối tượng đó đến viewport để xử lý tiếp.

.. code:: gdscript

    ...

                if was_intersect != NO_INTERSECTION and intersect != was_intersect:
                    # Pointer đã di chuyển
                    var event : InputEventMouseMotion = InputEventMouseMotion.new()
                    var from : Vector2 = _intersect_to_viewport_pos(was_intersect)
                    var to : Vector2 = _intersect_to_viewport_pos(intersect)
                    if was_pressed:
                        event.button_mask = MOUSE_BUTTON_MASK_LEFT
                    event.relative = to - from
                    event.position = to
                    layer_viewport.push_input(event)

    ...

Nếu chúng ta vừa nhả button, chúng ta cũng chuẩn bị một đối tượng :ref:`InputEventMouseButton <class_InputEventMouseButton>` để mô phỏng thao tác nhả button và gửi đối tượng đó đến viewport để xử lý tiếp.

.. code:: gdscript

    ...

                if not is_pressed and was_pressed:
                    # Đã nhả button?
                    var event : InputEventMouseButton = InputEventMouseButton.new()
                    event.button_index = 1
                    event.pressed = false
                    event.position = _intersect_to_viewport_pos(intersect)
                    layer_viewport.push_input(event)

    ...

Hoặc nếu chúng ta vừa nhấn button, chúng ta chuẩn bị một đối tượng :ref:`InputEventMouseButton <class_InputEventMouseButton>` để mô phỏng thao tác nhấn button và gửi đối tượng đó đến viewport để xử lý tiếp.

.. code:: gdscript

    ...

                elif is_pressed and not was_pressed:
                    # Đã nhấn button?
                    var event : InputEventMouseButton = InputEventMouseButton.new()
                    event.button_index = 1
                    event.button_mask = MOUSE_BUTTON_MASK_LEFT
                    event.pressed = true
                    event.position = _intersect_to_viewport_pos(intersect)
                    layer_viewport.push_input(event)

    ...

Tiếp theo, chúng ta ghi nhớ trạng thái để dùng cho frame tiếp theo.

.. code:: gdscript

    ...

                was_pressed = is_pressed
                was_intersect = intersect

    ...

Cuối cùng, nếu không có giao với viewport, chúng ta xóa trạng thái.

.. code:: gdscript

    ...

            else:
                was_pressed = false
                was_intersect = NO_INTERSECTION


Khoét lỗ
--------

Vì composition layer được composited bên trên kết quả render, nó có thể được render phía trước những đối tượng thực sự nằm phía trước viewport.

Bằng cách bật hole punch, bạn yêu cầu Godot render một đối tượng trong suốt tại nơi viewport được hiển thị. Godot thực hiện việc này theo cách lấp đầy depth buffer và xóa kết quả render hiện tại. Mọi thứ phía sau viewport giờ sẽ bị xóa, trong khi mọi thứ phía trước viewport vẫn được render như bình thường.

Bạn cũng cần đặt ``Sort Order`` thành một giá trị âm; XR compositor lúc này sẽ vẽ viewport trước, rồi phủ kết quả render của chúng ta lên trên.

.. figure:: img/openxr_composition_layer_hole_punch.webp
   :align: center

   Use case showing how the user's hand is incorrectly obscured
   by a composition layer when hole punching is not used.
