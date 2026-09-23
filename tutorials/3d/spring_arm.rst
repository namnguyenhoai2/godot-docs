.. _doc_spring_arm:

Camera góc nhìn người thứ ba với spring arm
===========================================

Giới thiệu
----------

Các game 3D thường có camera góc nhìn người thứ ba theo sau và xoay quanh một đối tượng như nhân vật người chơi hoặc phương tiện.

Trong Godot, bạn có thể thực hiện việc này bằng cách đặt một :ref:`Camera3D <class_Camera3D>` làm node con của một node. Tuy nhiên, nếu thử làm vậy mà không thực hiện thêm bước nào, bạn sẽ nhận thấy camera xuyên qua hình học và che khuất scene.

Đây là lúc node :ref:`SpringArm3D <class_SpringArm3D>` phát huy tác dụng.

Spring arm là gì?
-----------------

Spring arm có hai thành phần chính ảnh hưởng đến hành vi của nó.

"length" của spring arm là khoảng cách từ vị trí global của nó mà nó sẽ kiểm tra va chạm:

.. image:: img/spring_arm_position_length.webp

"shape" của spring arm là hình dạng mà nó dùng để kiểm tra va chạm. Spring arm sẽ "quét" hình dạng này từ điểm gốc ra phía ngoài theo chiều dài của nó.

.. image:: img/spring_arm_shape.webp

Spring arm cố gắng giữ tất cả node con của nó ở cuối chiều dài. Khi shape va chạm với một vật thể, các node con thay vào đó sẽ được đặt tại hoặc gần điểm va chạm đó:

.. image:: img/spring_arm_children.webp

Spring arm với camera
---------------------

Khi camera được đặt làm node con của spring arm, một hình chóp đại diện cho camera sẽ được dùng làm shape.

Hình chóp này đại diện cho **mặt phẳng gần** của camera:

.. image:: img/spring_arm_camera_shape.webp

.. note:: Nếu spring arm được gán một shape cụ thể, shape đó sẽ **luôn luôn** được sử dụng.

    Shape của camera chỉ được sử dụng nếu camera là **node con trực tiếp** của spring arm.

    Nếu không cung cấp shape và camera không phải là node con trực tiếp, spring arm sẽ chuyển sang dùng ray cast, vốn không chính xác cho các va chạm với camera và không được khuyến nghị.

Trong mỗi frame của quy trình vật lý, spring arm sẽ thực hiện một motion cast để kiểm tra xem có vật thể nào bị va chạm hay không:

.. image:: img/spring_arm_camera_motion_cast.webp

Khi shape va chạm với một vật thể, camera sẽ được đặt tại hoặc gần điểm va chạm đó:

.. image:: img/spring_arm_camera_collision.webp

Thiết lập spring arm và camera
------------------------------

Hãy thêm thiết lập camera với spring arm vào bản demo platformer.

.. note:: Bạn có thể tải bản demo Platformer 3D trên `GitHub <https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer>`_ hoặc dùng `Asset Library <https://godotengine.org/asset-library/asset/2748>`_.

Nhìn chung, đối với thiết lập camera góc nhìn người thứ ba, bạn sẽ có ba node là node con của node mà camera đang theo dõi:

- `Node3D` ("điểm xoay" của camera)

    - `SpringArm3D`

        - `Camera3D`

Mở scene ``player/player.tscn``. Thiết lập chúng làm node con của player và đặt tên riêng cho chúng để chúng ta có thể tìm thấy chúng trong script. **Hãy nhớ xóa node camera hiện có!**

.. image:: img/spring_arm_editor_setup.webp

Hãy di chuyển điểm xoay lên ``2`` trên trục Y để nó không nằm trên mặt đất:

.. image:: img/spring_arm_pivot_setup.webp


Đặt chiều dài của spring arm là ``3`` để nó được đặt phía sau nhân vật:

.. image:: img/spring_arm_length_setup.webp

.. note:: Để **Shape** của spring arm ở trạng thái ``<empty>``. Nhờ vậy, nó sẽ sử dụng hình chóp của camera.

    Nếu muốn, bạn cũng có thể thử các shape khác - sphere là lựa chọn phổ biến vì nó trượt mượt dọc theo các cạnh.

Cập nhật phần đầu của ``player/player.gd`` để lấy camera và các điểm xoay theo tên riêng của chúng:

.. code-block:: gdscript
    :caption: player/player.gd

    # Vô hiệu hóa dòng camera hiện có này bằng cách thêm dấu chú thích.
    # @onready var _camera := $Target/Camera3D as Camera3D

    @onready var _camera := %Camera3D as Camera3D
    @onready var _camera_pivot := %CameraPivot as Node3D

Thêm một hàm ``_unhandled_input`` để kiểm tra chuyển động của camera, sau đó xoay điểm xoay tương ứng:

.. code-block:: gdscript
    :caption: player/player.gd

    @export_range(0.0, 1.0) var mouse_sensitivity = 0.01
    @export var tilt_limit = deg_to_rad(75)


    func _unhandled_input(event: InputEvent) -> void:
        # Triển khai Mouselook bằng `screen_relative` để có độ nhạy độc lập với độ phân giải.
        if event is InputEventMouseMotion:
            _camera_pivot.rotation.x -= event.screen_relative.y * mouse_sensitivity
            # Ngăn camera xoay quá xa lên trên hoặc xuống dưới.
            _camera_pivot.rotation.x = clampf(_camera_pivot.rotation.x, -tilt_limit, tilt_limit)
            _camera_pivot.rotation.y += -event.screen_relative.x * mouse_sensitivity

Bằng cách xoay điểm xoay, spring arm cũng sẽ được xoay và vị trí của camera sẽ thay đổi. Chạy game và nhận thấy rằng chuyển động của chuột giờ đây xoay camera quanh nhân vật. Nếu camera di chuyển vào tường, nó sẽ va chạm với tường.

.. video:: video/spring_arm_camera.webm
   :alt: Camera attached to a spring arm colliding with walls
   :autoplay:
   :loop:
   :muted:
   :align: default

.. _`GitHub`: https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer
.. _`Asset Library`: https://godotengine.org/asset-library/asset/2748
