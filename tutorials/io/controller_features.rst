.. _doc_controller_features:

Tính năng của controller
========================

Godot hỗ trợ các tính năng dành riêng cho controller, có thể nâng cao hơn nữa trải nghiệm gameplay. Trang này mô tả các tính năng đó, cách những game hiện có đã sử dụng chúng và cách bạn có thể bắt đầu sử dụng chúng trong Godot.

.. warning::

    Các tính năng của controller này hiện chỉ được hỗ trợ trên Windows, macOS, iOS và Linux.


.. warning::

    Trừ khi bạn quảng bá cụ thể game của mình là yêu cầu những controller nhất định, hãy nhớ rằng không có gì đảm bảo người chơi sẽ có controller với bất kỳ tính năng cụ thể nào.

    Vì vậy, chúng tôi khuyên bạn nên sử dụng các tính năng này để nâng cao trải nghiệm gameplay cho những người chơi có controller hỗ trợ chúng, mà không làm ảnh hưởng đến những người không có controller.

.. _doc_controller_features_led_color:

Màu LED
-------

Game có thể sử dụng đèn LED trên một số controller để bổ trợ tinh tế cho gameplay trên màn hình bằng cách cung cấp một số hình ảnh tương ứng trong tay người chơi. Dưới đây là một số ví dụ đáng chú ý:

- Trong *Hades*, màu của đèn khớp với vị thần mà bạn đang nhận boon. - Trong *Resident Evil 2*, màu của đèn cho biết lượng máu của bạn (xanh lá khi đầy, vàng khi ở mức trung bình, đỏ khi thấp). - Trong *Star Wars Jedi: Fallen Order*, màu của đèn khớp với màu lightsaber của bạn.

Sử dụng phương thức :ref:`Input.set_joy_light()<class_Input_method_set_joy_light>` để thiết lập màu cho các đèn LED của một controller cụ thể.

Để xác định một controller cụ thể có hỗ trợ thiết lập đèn LED hay không, hãy sử dụng phương thức :ref:`Input.has_joy_light()<class_Input_method_has_joy_light>`. Các controller PlayStation DualShock và DualSense được biết là có hỗ trợ đèn LED.

Phương thức ``_process()`` sau đây thiết lập màu LED theo nút hiện đang được nhấn và tắt đèn nếu không có nút nào được nhấn:

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


Ví dụ sau đây làm LED chuyển mượt qua các sắc độ màu trong một vòng lặp:

.. code-block::

    var hue = 0.0

    func _process(delta):
        var col = Color.from_hsv(hue, 1.0, 1.0)
        Input.set_joy_light(0, col)
        hue += delta * 0.1

Ví dụ sau đây khiến LED nhấp nháy màu đỏ ba lần khi nhấn nút phía nam (Cross/X trên các controller PlayStation):

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

Cảm biến chuyển động (gyroscope và accelerometer)
-------------------------------------------------

Với điều khiển chuyển động, game có thể theo dõi chuyển động và góc xoay vật lý của controller. Điều này có thể được dùng để cho phép người chơi xoay camera trong game bằng cách di chuyển controller hoặc lắc controller để thực hiện một hành động đặc biệt.

Một số thương hiệu controller đã tích hợp cảm biến gyroscope và accelerometer vào các controller hiện đại của họ, trong đó hai thương hiệu lớn nhất là PlayStation và Nintendo. Lưu ý rằng controller Xbox không có cảm biến chuyển động bên trong.

Để kiểm tra xem một controller đã kết nối có cảm biến chuyển động hay không, hãy sử dụng :ref:`Input.has_joy_motion_sensors()<class_Input_method_has_joy_motion_sensors>`.

Cảm biến chuyển động bị tắt theo mặc định để tránh làm cạn pin controller khi game không sử dụng các tính năng đó. Để bật chúng, hãy gọi :ref:`Input.set_joy_motion_sensors_enabled()<class_Input_method_set_joy_motion_sensors_enabled>`.

Lưu ý rằng các trục của những giá trị mà cảm biến chuyển động của controller báo cáo luôn tương đối với hướng tự nhiên của controller. Dưới đây là hình ảnh ánh xạ các trục để dễ hình dung hơn:

.. image:: img/controller_axes.webp

Các giá trị gyroscope của controller cho biết chuyển động xoay quanh các trục tương ứng:

- giá trị X của dữ liệu gyroscope cho biết chuyển động xoay quanh trục X (pitch). - giá trị Y của dữ liệu gyroscope cho biết chuyển động xoay quanh trục Y (yaw). - giá trị Z của dữ liệu gyroscope cho biết chuyển động xoay quanh trục Z (roll).

Accelerometer của controller sẽ cung cấp các giá trị theo những cách tương ứng sau:

- Chuyển động sang trái và phải được báo cáo lần lượt là **+X** và **-X**. - Chuyển động xuống và lên được báo cáo lần lượt là **+Y** và **-Y**. - Chuyển động ra xa và hướng về phía người dùng được báo cáo lần lượt là **+Z** và **-Z**.

Gyroscope
~~~~~~~~~

**Gyroscope** là một loại cảm biến phát hiện chuyển động xoay của controller. Dưới đây là một số ví dụ đáng chú ý về việc sử dụng gyroscope trong game:

- Trong *Helldivers 2*, *Horizon Forbidden West*, *Star Wars: Dark Forces Remaster* và *Fortnite*, việc nghiêng controller sẽ khiến camera xoay tương ứng ("gyro aiming"). `This video by *Daven On The Moon* <https://www.youtube.com/watch?v=Vlfg9yku2hY>`_ trình bày và thảo luận chi tiết hơn về gyro aiming. - Trong *Death Stranding*, BB có thể được xoa dịu bằng cách nhẹ nhàng xoay controller.

Ví dụ sau đây xoay một object bằng cảm biến gyroscope của controller. Bạn cũng có thể truy cập ví dụ này bằng cách xem
:ref:`Input.start_joy_motion_sensors_calibration()<class_Input_method_start_joy_motion_sensors_calibration>` documentation.

.. code-block::

    const GYRO_SENSITIVITY = 10.0

    func _ready():
        # Trong ví dụ này, chúng ta chỉ sử dụng joypad đầu tiên đã kết nối (id 0).
        if 0 not in Input.get_connected_joypads():
            return

        if not Input.has_joy_motion_sensors(0):
            return

        # Chúng ta phải bật các cảm biến chuyển động trước khi sử dụng chúng.
        Input.set_joy_motion_sensors_enabled(0, true)

        # (Hãy cho người dùng biết rằng họ cần đặt joypad trên một bề mặt phẳng và chờ xác nhận.)

        # Bắt đầu quá trình calibration.
        calibrate_motion()

    func _process(delta):
        # Chỉ di chuyển object nếu các cảm biến chuyển động của joypad đã được calibration.
        if Input.is_joy_motion_sensors_calibrated(0):
            move_object(delta)

    func calibrate_motion():
        Input.start_joy_motion_sensors_calibration(0)

        # Chờ một khoảng thời gian.
        await get_tree().create_timer(1.0).timeout

        Input.stop_joy_motion_sensors_calibration(0)
        # Joypad hiện đã được calibration.

    func move_object(delta):
        var node: Node3D = ... # Đặt object của bạn ở đây.

        var gyro := Input.get_joy_gyroscope(0)
        node.rotation.x -= -gyro.y * GYRO_SENSITIVITY * delta  # Sử dụng chuyển động xoay quanh trục Y (yaw) ở đây.
        node.rotation.y += -gyro.x * GYRO_SENSITIVITY * delta  # Sử dụng chuyển động xoay quanh trục X (pitch) ở đây.

Lưu ý rằng trước khi sử dụng dữ liệu của gyroscope, trước tiên chúng ta phải calibration nó bằng cách gọi :ref:`Input.start_joy_motion_sensors_calibration()<class_Input_method_start_joy_motion_sensors_calibration>` và :ref:`Input.stop_joy_motion_sensors_calibration()<class_Input_method_stop_joy_motion_sensors_calibration>`. Đó là vì các gyroscope hiện đại thường cần được calibration. Điều này giống như việc cân có thể cần được calibration để xác định "số 0" là gì. Cũng như cân, chỉ gyroscope được calibration chính xác mới cho kết quả đọc chính xác. Trong quá trình calibration, người dùng đặt controller xuống một bề mặt phẳng. Sau đó, controller xác định các giá trị mà gyroscope báo cáo khi nó thực sự hoàn toàn không di chuyển ("bias" của nó) và sử dụng thông tin này để làm cho dữ liệu chuyển động xoay chính xác hơn.

Xem `the article on GyroWiki <http://gyrowiki.jibbsmart.com/blog:good-gyro-controls-part-1:the-gyro-is-a-mouse>`__ để biết thông tin về cách sử dụng input từ gyroscope như chuột.

Sau khi gyroscope của controller đã được bật và calibration chính xác, bạn có thể đọc các giá trị mà nó báo cáo bằng cách sử dụng :ref:`Input.get_joy_gyroscope()<class_Input_method_get_joy_gyroscope>`.

Accelerometer
~~~~~~~~~~~~~

.. warning::

    Không sử dụng dữ liệu accelerometer để xác định vị trí của controller trong không gian 3D; accelerometer nói chung không đủ chính xác cho việc này.

**Accelerometer** là một loại cảm biến phát hiện gia tốc của controller tính bằng m/s². Ví dụ, nó có thể phát hiện người chơi nhanh chóng nâng controller lên, di chuyển controller sang một bên hoặc lắc controller.

Gia tốc mà accelerometer phát hiện mặc định bao gồm cả trọng lực. Để chỉ lấy *gia tốc do người dùng tạo ra*, hãy trừ trọng lực khỏi gia tốc được phát hiện:

.. code-block::

    Input.get_joy_accelerometer(device) - Input.get_joy_gravity(device)

Do cách accelerometer hoạt động về mặt vật lý, sau khi chuyển động theo một hướng dừng lại, chúng gần như ngay lập tức báo cáo chuyển động theo hướng ngược lại. Sau khi phát hiện chuyển động theo một hướng, bạn có thể muốn bỏ qua các kết quả đọc tiếp theo trong một khoảng thời gian ngắn để tránh phát hiện chuyển động ngược này.

Ví dụ sau đây in ra chuyển động của controller khi nó được di chuyển nhanh bằng accelerometer. Nếu độ nhạy không phù hợp với bạn, bạn có thể điều chỉnh hằng số ``THRESHOLD`` hoặc thay thế nó bằng một giá trị khác trong đoạn code bên dưới.

.. code-block::

    var detect_accelerometer = true

    # Thay đổi để game phát hiện chuyển động ở các ngưỡng khác nhau.
    # Với giá trị nhỏ hơn, các chuyển động nhỏ hơn sẽ được phát hiện, còn với giá trị
    # lớn hơn, chỉ những chuyển động lớn mới được phát hiện.
    const THRESHOLD = 10.0

    func _ready():
        # Trong ví dụ này, chúng ta chỉ sử dụng joypad đầu tiên đã kết nối (ID 0).
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

            # Sau khi phát hiện chuyển động theo một hướng, cảm biến accelerometer
            # sẽ nhanh chóng báo cáo chuyển động theo hướng ngược lại, dù controller chỉ di chuyển một lần.
            # Vì vậy, chúng ta cần bỏ qua các giá trị được báo cáo này trong một khoảng thời gian ngắn.
            detect_accelerometer = false
            await get_tree().create_timer(0.5, false).timeout
            detect_accelerometer = true
