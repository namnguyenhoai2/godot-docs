.. _doc_controller_features:

Các tính năng của tay cầm
=========================

Godot hỗ trợ các tính năng dành riêng cho tay cầm, có thể giúp nâng cao hơn nữa trải nghiệm chơi game. Trang này mô tả các tính năng đó, cách những game hiện có đã sử dụng chúng và cách bạn có thể bắt đầu sử dụng chúng trong Godot.

.. warning::

    Các tính năng của tay cầm này hiện chỉ được hỗ trợ trên Windows, macOS, iOS và Linux.


.. warning::

    Trừ khi bạn quảng cáo cụ thể rằng game của mình yêu cầu những tay cầm nhất định, hãy nhớ rằng không có gì đảm bảo người chơi sẽ có tay cầm sở hữu bất kỳ tính năng cụ thể nào.

    Do đó, chúng tôi khuyên bạn nên sử dụng các tính năng này để nâng cao trải nghiệm chơi game cho những người chơi có tay cầm hỗ trợ chúng, mà không làm giảm trải nghiệm của những người không có tay cầm.

.. _doc_controller_features_led_color:

Màu đèn LED
-----------

Game có thể sử dụng đèn LED trên một số tay cầm để bổ trợ một cách tinh tế cho diễn biến trên màn hình bằng cách cung cấp một số hình ảnh tương ứng trong tay người chơi. Dưới đây là một số ví dụ đáng chú ý:

- Trong *Hades*, màu của đèn khớp với vị thần mà bạn nhận phước lành từ đó.
- Trong *Resident Evil 2*, màu của đèn cho biết lượng máu của bạn (xanh lá khi đầy, vàng khi ở mức trung bình, đỏ khi thấp).
- Trong *Star Wars Jedi: Fallen Order*, màu của đèn khớp với màu thanh kiếm ánh sáng của bạn.

Sử dụng phương thức :ref:`Input.set_joy_light()<class_Input_method_set_joy_light>` để đặt màu đèn LED của một tay cầm cụ thể.

Để xác định một tay cầm cụ thể có hỗ trợ cài đặt đèn LED hay không, hãy sử dụng phương thức :ref:`Input.has_joy_light()<class_Input_method_has_joy_light>`. Tay cầm PlayStation DualShock và DualSense được biết là có hỗ trợ đèn LED.

Phương thức ``_process()`` sau đây đặt màu đèn LED dựa trên nút hiện đang được nhấn và tắt đèn nếu không có nút nào được nhấn:

.. code-block::

    func _process(_delta):
        var color := Color.BLACK

        if Input.is_joy_button_pressed(0, JOY_BUTTON_A):
            color = Color.BLUE
        elif Input.is_joy_button_pressed(0, JOY_BUTTON_X):
            color = Color.MAGENTA
        elif Input.is_joy_button_pressed(0, JOY_BUTTON_B):
            color = Color.RED
        elif Input.is_joy_button_pressed(0, JOY_BUTTON_Y):
            color = Color.GREEN

        Input.set_joy_light(0, color)


Ví dụ sau đây làm đèn LED chuyển mượt qua các sắc độ màu trong một vòng lặp:

.. code-block::

    var hue = 0.0

    func _process(delta):
        var col = Color.from_hsv(hue, 1.0, 1.0)
        Input.set_joy_light(0, col)
        hue += delta * 0.1

Ví dụ sau đây khiến đèn LED nhấp nháy màu đỏ ba lần khi nhấn nút south (Cross/X trên tay cầm PlayStation):

.. code-block::

    var blink_tween: Tween = null

    func _process(_delta):
        var ready_to_blink = not blink_tween or not blink_tween.is_running()
        if Input.is_joy_button_pressed(0, JOY_BUTTON_A) and ready_to_blink:
            do_blink()

    func do_blink():
        if blink_tween:
            blink_tween.kill()

        blink_tween = create_tween()
        blink_tween.tween_callback(func(): Input.set_joy_light(0, Color.RED))
        blink_tween.tween_interval(0.2)
        blink_tween.tween_callback(func(): Input.set_joy_light(0, Color.BLACK))
        blink_tween.tween_interval(0.2)
        blink_tween.set_loops(3)

.. _doc_controller_features_motion_sensors:

Cảm biến chuyển động (con quay hồi chuyển và gia tốc kế)
--------------------------------------------------------

Với điều khiển chuyển động, game có thể theo dõi chuyển động và góc xoay vật lý của tay cầm. Tính năng này có thể cho phép người chơi xoay camera trong game bằng cách di chuyển tay cầm hoặc lắc tay cầm để thực hiện một hành động đặc biệt.

Một số thương hiệu tay cầm đã tích hợp cảm biến con quay hồi chuyển và gia tốc kế vào các tay cầm hiện đại của họ, trong đó hai thương hiệu lớn nhất là PlayStation và Nintendo. Lưu ý rằng tay cầm Xbox không có cảm biến chuyển động bên trong.

Để kiểm tra xem một tay cầm đã kết nối có cảm biến chuyển động hay không, hãy sử dụng :ref:`Input.has_joy_motion_sensors()<class_Input_method_has_joy_motion_sensors>`.

Cảm biến chuyển động được tắt theo mặc định để tránh làm hao pin tay cầm khi game không sử dụng các tính năng đó. Để bật chúng, hãy gọi :ref:`Input.set_joy_motion_sensors_enabled()<class_Input_method_set_joy_motion_sensors_enabled>`.

Lưu ý rằng các trục của những giá trị do cảm biến chuyển động của tay cầm báo cáo luôn tương ứng với hướng tự nhiên của tay cầm. Dưới đây là hình ảnh ánh xạ các trục để giúp bạn hiểu rõ hơn:

.. image:: img/controller_axes.webp

Các giá trị con quay hồi chuyển của tay cầm biểu thị chuyển động xoay quanh các trục tương ứng:

- giá trị X của dữ liệu con quay hồi chuyển biểu thị chuyển động xoay quanh trục X (pitch).
- giá trị Y của dữ liệu con quay hồi chuyển biểu thị chuyển động xoay quanh trục Y (yaw).
- giá trị Z của dữ liệu con quay hồi chuyển biểu thị chuyển động xoay quanh trục Z (roll).

Gia tốc kế của tay cầm sẽ cung cấp các giá trị theo những cách sau, tương ứng:

- Chuyển động sang trái và phải được báo cáo lần lượt là **+X** và **-X**.
- Chuyển động xuống và lên được báo cáo lần lượt là **+Y** và **-Y**.
- Chuyển động ra xa và hướng về phía người dùng được báo cáo lần lượt là **+Z** và **-Z**.

Con quay hồi chuyển
~~~~~~~~~~~~~~~~~~~

**Con quay hồi chuyển** là một loại cảm biến phát hiện chuyển động xoay của tay cầm. Dưới đây là một số ví dụ đáng chú ý về việc sử dụng con quay hồi chuyển trong game:

- Trong *Helldivers 2*, *Horizon Forbidden West*, *Star Wars: Dark Forces Remaster* và *Fortnite*, việc nghiêng tay cầm sẽ khiến camera xoay tương ứng ("gyro aiming"). `Video này của *Daven On The Moon* <https://www.youtube.com/watch?v=Vlfg9yku2hY>`_ trình bày và thảo luận chi tiết hơn về gyro aiming.
- Trong *Death Stranding*, BB có thể được xoa dịu bằng cách nhẹ nhàng xoay tay cầm.

Ví dụ sau đây xoay một đối tượng bằng cảm biến con quay hồi chuyển của tay cầm. Bạn cũng có thể truy cập ví dụ này bằng cách xem
:ref:`Input.start_joy_motion_sensors_calibration()<class_Input_method_start_joy_motion_sensors_calibration>` tài liệu.

.. code-block::

    const GYRO_SENSITIVITY = 10.0

    func _ready():
        # Trong ví dụ này, chúng ta chỉ sử dụng joypad đầu tiên được kết nối (id 0).
        if 0 not in Input.get_connected_joypads():
            return

        if not Input.has_joy_motion_sensors(0):
            return

        # Chúng ta phải bật các cảm biến chuyển động trước khi sử dụng chúng.
        Input.set_joy_motion_sensors_enabled(0, true)

        # (Hãy cho người dùng biết ở đây rằng họ cần đặt joypad trên một bề mặt phẳng và chờ xác nhận.)

        # Bắt đầu quá trình hiệu chỉnh.
        calibrate_motion()

    func _process(delta):
        # Chỉ di chuyển đối tượng khi các cảm biến chuyển động của joypad đã được hiệu chỉnh.
        if Input.is_joy_motion_sensors_calibrated(0):
            move_object(delta)

    func calibrate_motion():
        Input.start_joy_motion_sensors_calibration(0)

        # Chờ một lúc.
        await get_tree().create_timer(1.0).timeout

        Input.stop_joy_motion_sensors_calibration(0)
        # Joypad hiện đã được hiệu chỉnh.

    func move_object(delta):
        var node: Node3D = ... # Đặt đối tượng của bạn ở đây.

        var gyro := Input.get_joy_gyroscope(0)
        node.rotation.x -= -gyro.y * GYRO_SENSITIVITY * delta  # Sử dụng chuyển động xoay quanh trục Y (yaw) ở đây.
        node.rotation.y += -gyro.x * GYRO_SENSITIVITY * delta  # Sử dụng chuyển động xoay quanh trục X (pitch) ở đây.

Lưu ý rằng trước khi sử dụng dữ liệu của con quay hồi chuyển, trước tiên chúng ta phải hiệu chỉnh nó bằng cách gọi :ref:`Input.start_joy_motion_sensors_calibration()<class_Input_method_start_joy_motion_sensors_calibration>` và :ref:`Input.stop_joy_motion_sensors_calibration()<class_Input_method_stop_joy_motion_sensors_calibration>`. Đó là vì các con quay hồi chuyển hiện đại thường cần được hiệu chỉnh. Điều này cũng giống như việc một chiếc cân có thể cần được hiệu chỉnh để xác định giá trị "0". Cũng như một chiếc cân, chỉ con quay hồi chuyển được hiệu chỉnh chính xác mới cho kết quả đo chính xác. Trong quá trình hiệu chỉnh, người dùng đặt tay cầm xuống một bề mặt phẳng. Sau đó, tay cầm xác định những giá trị mà con quay hồi chuyển báo cáo khi nó thực sự hoàn toàn không chuyển động ("bias"), rồi dùng thông tin này để làm cho dữ liệu chuyển động xoay chính xác hơn.

Xem `bài viết về GyroWiki <http://gyrowiki.jibbsmart.com/blog:good-gyro-controls-part-1:the-gyro-is-a-mouse>`__ để biết cách sử dụng dữ liệu đầu vào từ con quay hồi chuyển như một con chuột.

Sau khi con quay hồi chuyển của controller được bật và hiệu chỉnh chính xác, bạn có thể đọc các giá trị mà nó báo cáo bằng cách sử dụng :ref:`Input.get_joy_gyroscope()<class_Input_method_get_joy_gyroscope>`.

Accelerometer
~~~~~~~~~~~~~

.. warning::

    Không sử dụng dữ liệu từ cảm biến gia tốc để xác định vị trí của controller trong không gian 3D; nhìn chung, các cảm biến gia tốc không đủ chính xác cho việc này.

**Cảm biến gia tốc** là một loại cảm biến phát hiện gia tốc của controller theo đơn vị m/s². Ví dụ, cảm biến có thể phát hiện khi người chơi nhanh chóng nâng controller lên, di chuyển controller sang một bên hoặc lắc controller.

Theo mặc định, gia tốc mà cảm biến gia tốc phát hiện bao gồm cả trọng lực. Để chỉ lấy *gia tốc* do người dùng tác động, hãy trừ trọng lực khỏi gia tốc được phát hiện:

.. code-block::

    Input.get_joy_accelerometer(device) - Input.get_joy_gravity(device)

Do nguyên lý hoạt động vật lý của cảm biến gia tốc, sau khi chuyển động theo một hướng dừng lại, cảm biến gần như ngay lập tức báo cáo chuyển động theo hướng ngược lại. Sau khi phát hiện chuyển động theo một hướng, bạn có thể muốn bỏ qua các kết quả đọc tiếp theo trong một khoảng thời gian ngắn để tránh phát hiện chuyển động ngược này.

Ví dụ sau in ra chuyển động của controller khi controller được di chuyển nhanh bằng cảm biến gia tốc. Nếu độ nhạy không phù hợp với bạn, bạn có thể điều chỉnh hằng số ``THRESHOLD`` hoặc thay thế nó bằng một giá trị khác trong đoạn mã bên dưới.

.. code-block::

    var detect_accelerometer = true

    # Thay đổi để game phát hiện chuyển động ở các ngưỡng khác nhau.
    # Với giá trị nhỏ hơn, các chuyển động nhỏ hơn sẽ được phát hiện, còn với
    # giá trị lớn hơn, chỉ các chuyển động lớn mới được phát hiện.
    const THRESHOLD = 10.0

    func _ready():
        # Trong ví dụ này, chúng ta chỉ sử dụng joypad đầu tiên được kết nối (ID 0).
        if 0 not in Input.get_connected_joypads():
            return

        if not Input.has_joy_motion_sensors(0):
            return

        # Chúng ta phải bật các cảm biến chuyển động trước khi sử dụng chúng.
        Input.set_joy_motion_sensors_enabled(0, true)

    func _process(delta):
        if Input.has_joy_motion_sensors(0):
            accelerometer_example()

    func accelerometer_example():
        if not detect_accelerometer:
            return

        var acceleration = Input.get_joy_accelerometer(0) - Input.get_joy_gravity(0)
        if acceleration.length() > THRESHOLD:
            if acceleration.x > THRESHOLD:
                print("Moved left")
            elif acceleration.x < -THRESHOLD:
                print("Moved right")
            if acceleration.y < -THRESHOLD:
                print("Moved up")
            elif acceleration.y > THRESHOLD:
                print("Moved down")
            if acceleration.z < -THRESHOLD:
                print("Moved closer to the player")
            elif acceleration.z > THRESHOLD:
                print("Moved away from the player")

            # Sau khi phát hiện chuyển động theo một hướng, cảm biến gia tốc
            # sẽ báo cáo ngắn gọn chuyển động theo hướng ngược lại, dù controller chỉ di chuyển một lần.
            # Vì vậy, chúng ta cần bỏ qua các giá trị được báo cáo này trong một khoảng thời gian ngắn.
            detect_accelerometer = false
            await get_tree().create_timer(0.5, false).timeout
            detect_accelerometer = true

.. _`This video by *Daven On The Moon*`: https://www.youtube.com/watch?v=Vlfg9yku2hY
