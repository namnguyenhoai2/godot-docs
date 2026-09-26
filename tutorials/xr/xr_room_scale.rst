.. _doc_xr_room_scale:

Room scale trong XR
===================

Một trong những điểm cốt lõi của các dự án XR là khả năng tự do đi lại trong một không gian rộng. Không gian này thường bị giới hạn bởi căn phòng nơi người chơi đang ở, với các cảm biến tracking được đặt trong không gian đó. Tuy nhiên, với sự ra đời của inside-out tracking, các không gian chơi ngày càng lớn hơn đã trở nên khả thi.

Đối với nhà phát triển, điều này tạo ra một số thách thức thú vị. Trong tài liệu này, chúng ta sẽ xem xét một số thách thức bạn có thể gặp phải và phác thảo một vài giải pháp. Chúng ta sẽ thảo luận về các vấn đề và thách thức đối với game XR ở tư thế ngồi trong một tài liệu khác.

.. note::
  Các nhà phát triển thường ngồi sau bàn làm việc khi xây dựng nền tảng cho game của mình. Ở chế độ này, các vấn đề khi phát triển cho room scale sẽ không xuất hiện cho đến khi quá muộn. Lời khuyên ở đây là hãy bắt đầu testing trong tư thế đứng và đi lại càng sớm càng tốt. Khi đã hài lòng rằng nền tảng của mình đủ vững chắc, bạn có thể phát triển một cách thoải mái trong khi vẫn ngồi.

Trong các game góc nhìn thứ nhất truyền thống, người chơi được biểu diễn bằng một node :ref:`CharacterBody3D <class_characterbody3d>`. Node này được di chuyển bằng cách xử lý input từ controller, mouse hoặc keyboard theo cách truyền thống. Một camera được gắn vào node này tại vị trí gần với vị trí đầu của người chơi.

Áp dụng mô hình này cho thiết lập XR, chúng ta thêm một node :ref:`XROrigin3D <class_xrorigin3d>` làm con của character body, và thêm một :ref:`XRCamera3D <class_xrcamera3d>` làm con của origin node. Thoạt nhìn, cách này có vẻ hoạt động. Tuy nhiên, khi xem xét kỹ hơn, mô hình này không tính đến việc có hai dạng chuyển động trong XR. Một là chuyển động thông qua input từ controller, và hai là chuyển động vật lý của người chơi trong thế giới thực.

Do đó, origin node không biểu diễn vị trí của người chơi. Nó biểu diễn tâm, hay điểm bắt đầu, của tracking space nơi người chơi có thể di chuyển về mặt vật lý. Khi người chơi đi lại trong phòng, chuyển động này được biểu diễn thông qua việc tracking headset của người chơi. Trong game, điều này được chuyển thành việc cập nhật vị trí của camera node tương ứng. Xét trên mọi phương diện, chúng ta đang tracking một cái đầu không có thân. Nếu không có body tracking, chúng ta không biết vị trí hoặc hướng của cơ thể người chơi.

.. image:: img/XRRoomCenterWalk.gif

Vấn đề đầu tiên mà cách này gây ra khá rõ ràng. Khi người chơi di chuyển bằng input từ controller, chúng ta có thể sử dụng cùng cách tiếp cận như trong các game thông thường và di chuyển người chơi theo hướng về phía trước. Tuy nhiên, người chơi không ở vị trí mà chúng ta nghĩ, nên khi di chuyển về phía trước, chúng ta đang kiểm tra va chạm ở sai vị trí.

.. image:: img/XRRoomWalkOffCliff.gif

Vấn đề thứ hai thực sự thể hiện rõ khi người chơi đi xa hơn khỏi tâm của tracking space và sử dụng input từ controller để xoay. Nếu xoay character body, người chơi sẽ di chuyển quanh căn phòng theo quỹ đạo tròn.

.. image:: img/XRRoomRotateOrigin.gif

Nếu khắc phục các vấn đề trên, chúng ta sẽ phát hiện vấn đề thứ ba. Khi đường đi của người chơi bị chặn trong thế giới ảo, người chơi vẫn có thể di chuyển về phía trước về mặt vật lý.

.. image:: img/XRRoomWalkWall.gif

Chúng ta sẽ xem xét cách giải quyết hai vấn đề đầu tiên bằng hai giải pháp riêng biệt, sau đó thảo luận về cách xử lý vấn đề thứ ba.

Giải pháp lấy origin làm tâm
----------------------------

Để xem xét cách tiếp cận đầu tiên nhằm giải quyết vấn đề này, chúng ta sẽ thay đổi cấu trúc. Đây là cách tiếp cận hiện được triển khai trong XR Tools.

.. image:: img/xr_room_scale_origin_body.webp

Trong thiết lập này, chúng ta đánh dấu character body là top level để nó không di chuyển cùng origin.

Chúng ta cũng có một helper node cho biết khớp cổ nằm ở đâu so với camera. Chúng ta sử dụng node này để xác định tâm của body.

Việc xử lý chuyển động của character giờ đây được thực hiện qua ba bước.

.. note::
  `Bản demo chuyển động lấy origin làm tâm <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_origin_centric_movement>`__ chứa một ví dụ chi tiết hơn về kỹ thuật được mô tả bên dưới.

Bước 1
------

Trong bước đầu tiên, chúng ta sẽ xử lý chuyển động vật lý của người chơi. Chúng ta xác định vị trí hiện tại của người chơi và cố gắng di chuyển character body đến đó.

.. code-block:: gdscript

  func _process_on_physical_movement(delta):
    # Ghi nhớ vận tốc hiện tại để áp dụng sau
    var current_velocity = $CharacterBody3D.velocity

    # Ghi nhớ vị trí hiện tại của player body
    var org_player_body: Vector3 = $CharacterBody3D.global_transform.origin

    # Xác định vị trí mà player body nên ở đó
    var player_body_location: Vector3 = $XRCamera3D.transform * $XRCamera3D/Neck.transform.origin
    player_body_location.y = 0.0
    player_body_location = global_transform * player_body_location

    # Cố gắng di chuyển character
    $CharacterBody3D.velocity = (player_body_location - org_player_body) / delta
    $CharacterBody3D.move_and_slide()

    # Đặt lại về giá trị hiện tại
    $CharacterBody3D.velocity = current_velocity

    # Kiểm tra xem chúng ta có di chuyển hết quãng đường hay không, bỏ qua thay đổi độ cao
    var movement_left = player_body_location - $CharacterBody3D.global_transform.origin
    movement_left.y = 0.0
    if (movement_left).length() > 0.01:
      # Chúng ta sẽ nói thêm về việc cần làm ở đây sau
      return true
    else:
      return false

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)

Lưu ý rằng chúng ta trả về ``true`` từ hàm ``_process_on_physical_movement`` khi không thể di chuyển người chơi hết quãng đường.

Bước 2
------

Bước thứ hai là xử lý việc xoay người chơi do input của người dùng.

Vì input được sử dụng có thể khác nhau tùy theo nhu cầu, chúng ta chỉ cần gọi hàm ``_get_rotational_input``. Hàm này cần lấy input cần thiết và trả về tốc độ xoay tính bằng radian mỗi giây.

.. note::
  Trong ví dụ này, chúng ta sẽ giữ mọi thứ đơn giản và dễ hiểu. Chúng ta sẽ không xử lý các tính năng tạo sự thoải mái như snap turning và áp dụng vignette. Chúng tôi thực sự khuyến nghị triển khai các tính năng tạo sự thoải mái này.

.. code-block:: gdscript

  func _get_rotational_input() -> float:
    # Triển khai hàm này để trả về góc xoay tính bằng radian mỗi giây.
    return 0.0

  func _copy_player_rotation_to_character_body():
    # Chúng ta chỉ sao chép hướng về phía trước vào character body và bỏ qua độ nghiêng
    var camera_forward: Vector3 = -$XRCamera3D.global_transform.basis.z
    var body_forward: Vector3 = Vector3(camera_forward.x, 0.0, camera_forward.z)

    $CharacterBody3D.global_transform.basis = Basis.looking_at(body_forward, Vector3.UP)

  func _process_rotation_on_input(delta):
    var t1 := Transform3D()
    var t2 := Transform3D()
    var rot := Transform3D()

    # Chúng ta sẽ xoay origin quanh người chơi
    var player_position = $CharacterBody3D.global_transform.origin - global_transform.origin

    t1.origin = -player_position
    t2.origin = player_position
    rot = rot.rotated(Vector3(0.0, 1.0, 0.0), _get_rotational_input() * delta)
    global_transform = (global_transform * t2 * rot * t1).orthonormalized()

    # Bây giờ hãy đảm bảo player body cũng đang hướng đúng cách
    _copy_player_rotation_to_character_body()

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)
    if !is_colliding:
      _process_rotation_on_input(delta)

.. note::
  Chúng ta đã thêm lời gọi để xử lý việc xoay vào physics process, nhưng chỉ thực thi lời gọi này nếu có thể di chuyển người chơi hoàn toàn. Điều này có nghĩa là nếu người chơi di chuyển đến một nơi không nên đến, chúng ta sẽ không xử lý thêm chuyển động.

Bước 3
------

Bước thứ ba và cũng là bước cuối cùng là di chuyển người chơi về phía trước, phía sau hoặc sang ngang do input của người dùng.

Cũng như với việc xoay, input khác nhau tùy từng dự án, nên chúng ta chỉ cần gọi hàm ``_get_movement_input``. Hàm này cần lấy input cần thiết và trả về một vector hướng được scale theo vận tốc yêu cầu.

.. note::
  Cũng như với việc xoay, chúng ta giữ mọi thứ đơn giản. Ở đây cũng nên cân nhắc việc bổ sung các thiết lập tạo sự thoải mái.

.. code-block:: gdscript

  var gravity = ProjectSettings.get_setting("physics/3d/default_gravity")

  func _get_movement_input() -> Vector2:
    # Triển khai để trả về chuyển động theo hướng được yêu cầu, tính bằng mét mỗi giây.
    return Vector2()

  func _process_movement_on_input(delta):
    # Ghi nhớ vị trí hiện tại của player body
    var org_player_body: Vector3 = $CharacterBody3D.global_transform.origin

    # Bắt đầu bằng cách áp dụng trọng lực
    $CharacterBody3D.velocity.y -= gravity * delta

    # Bây giờ thêm chuyển động của chúng ta
    var input: Vector2 = _get_movement_input()
    var movement: Vector3 = ($CharacterBody3D.global_transform.basis * Vector3(input.x, 0, input.y))
    $CharacterBody3D.velocity.x = movement.x
    $CharacterBody3D.velocity.z = movement.z

    # Cố gắng di chuyển người chơi
    $CharacterBody3D.move_and_slide()

    # Và giờ áp dụng chuyển động thực tế cho origin của chúng ta
    global_transform.origin += $CharacterBody3D.global_transform.origin - org_player_body

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)
    if !is_colliding:
      _process_rotation_on_input(delta)
      _process_movement_on_input(delta)

Giải pháp lấy character body làm trung tâm
------------------------------------------

Trong thiết lập này, chúng ta sẽ giữ character body làm node gốc, nhờ đó việc kết hợp với các cơ chế game truyền thống sẽ dễ dàng hơn.

.. image:: img/xr_room_scale_character_body.webp

Ở đây, chúng ta có một character body tiêu chuẩn với collision shape, cùng node XR origin và camera là các node con như bình thường. Chúng ta cũng có node helper neck.

Việc xử lý chuyển động của nhân vật vẫn được thực hiện qua cùng ba bước, nhưng được triển khai hơi khác một chút.

.. note::
  `Bản demo chuyển động lấy nhân vật làm trung tâm <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_character_centric_movement>`__ chứa một ví dụ chi tiết hơn về kỹ thuật được mô tả bên dưới.

Bước 1
------

Trong cách tiếp cận này, bước 1 là nơi mọi điều kỳ diệu xảy ra. Cũng như cách tiếp cận trước, chúng ta sẽ áp dụng chuyển động vật lý cho character body, nhưng sẽ bù trừ chuyển động đó trên node origin.

Điều này đảm bảo vị trí của người chơi luôn đồng bộ với vị trí của character body.

.. code-block:: gdscript

  # Các biến helper giúp code dễ đọc hơn
  @onready var origin_node = $XROrigin3D
  @onready var camera_node = $XROrigin3D/XRCamera3D
  @onready var neck_position_node = $XROrigin3D/XRCamera3D/Neck

  func _process_on_physical_movement(delta) -> bool:
    # Ghi nhớ vận tốc hiện tại để áp dụng sau
    var current_velocity = velocity

    # Bắt đầu bằng cách xoay người chơi để hướng cùng phía với người chơi thực tế
    var camera_basis: Basis = origin_node.transform.basis * camera_node.transform.basis
    var forward: Vector2 = Vector2(camera_basis.z.x, camera_basis.z.z)
    var angle: float = forward.angle_to(Vector2(0.0, 1.0))

    # Xoay character body của chúng ta
    transform.basis = transform.basis.rotated(Vector3.UP, angle)

    # Đảo ngược phép xoay này trên node origin
    origin_node.transform = Transform3D().rotated(Vector3.UP, -angle) * origin_node.transform

    # Giờ áp dụng chuyển động, trước tiên di chuyển player body đến đúng vị trí
    var org_player_body: Vector3 = global_transform.origin
    var player_body_location: Vector3 = origin_node.transform * camera_node.transform * neck_position_node.transform.origin
    player_body_location.y = 0.0
    player_body_location = global_transform * player_body_location

    velocity = (player_body_location - org_player_body) / delta
    move_and_slide()

    # Giờ di chuyển XROrigin ngược lại
    var delta_movement = global_transform.origin - org_player_body
    origin_node.global_transform.origin -= delta_movement

    # Trả về giá trị của chúng ta
    velocity = current_velocity

    if (player_body_location - global_transform.origin).length() > 0.01:
      # Chúng ta sẽ nói thêm về việc cần làm ở đây sau
      return true
    else:
      return false

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)

Về cơ bản, đoạn code trên sẽ di chuyển character body đến vị trí của người chơi, sau đó di chuyển node origin ngược lại một lượng tương đương. Kết quả là người chơi luôn ở chính giữa phía trên character body.

Chúng ta bắt đầu bằng việc áp dụng phép xoay. Character body phải hướng về phía mà người chơi đang nhìn ở frame trước. Chúng ta tính hướng của camera trong không gian của character body. Giờ chúng ta có thể tính góc mà người chơi đã xoay đầu. Chúng ta xoay character body cùng một lượng để character body hướng cùng hướng với người chơi. Sau đó, chúng ta đảo ngược phép xoay trên node origin để camera lại được căn chỉnh với người chơi.

Đối với chuyển động, chúng ta cũng thực hiện gần như tương tự. Character body phải ở vị trí mà người chơi đã đứng trong frame trước. Chúng ta tính khoảng cách người chơi đã di chuyển khỏi vị trí này. Sau đó, chúng ta thử di chuyển character body đến vị trí đó.

Vì người chơi có thể va vào collision body và bị dừng lại, chúng ta chỉ di chuyển điểm origin ngược lại một khoảng bằng đúng quãng đường character body thực sự đã di chuyển. Do đó, người chơi có thể di chuyển ra khỏi vị trí này, nhưng điều đó sẽ được phản ánh trong vị trí của người chơi.

Cũng như giải pháp trước, chúng ta trả về true nếu trường hợp này xảy ra.

Bước 2
------

Trong bước này, chúng ta lại áp dụng phép xoay dựa trên input từ controller. Tuy nhiên, trong trường hợp này, code gần như giống hệt cách triển khai trong một game góc nhìn người thứ nhất thông thường.

Vì input được sử dụng có thể khác nhau tùy theo nhu cầu, chúng ta chỉ cần gọi hàm ``_get_rotational_input``. Hàm này cần lấy input cần thiết và trả về tốc độ xoay tính bằng radian mỗi giây.

.. code-block:: gdscript

  func _get_rotational_input() -> float:
    # Triển khai hàm này để trả về góc xoay tính bằng radian mỗi giây.
    return 0.0

  func _process_rotation_on_input(delta):
    rotation.y += _get_rotational_input() * delta

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)
    if !is_colliding:
      _process_rotation_on_input(delta)


Bước 3
------

Ở bước ba, chúng ta lại áp dụng chuyển động dựa trên input từ controller. Tuy nhiên, cũng như ở bước 2, giờ chúng ta có thể triển khai việc này như trong một game góc nhìn người thứ nhất thông thường.

Cũng như với việc xoay, input khác nhau tùy từng dự án, nên chúng ta chỉ cần gọi hàm ``_get_movement_input``. Hàm này cần lấy input cần thiết và trả về một vector hướng được scale theo vận tốc yêu cầu.

.. code-block:: gdscript

  func _get_movement_input() -> Vector2:
    # Triển khai để trả về chuyển động theo hướng được yêu cầu, tính bằng mét mỗi giây.
    return Vector2()

  func _process_movement_on_input(delta):
    var movement_input = _get_movement_input()
    var direction = global_transform.basis * Vector3(movement_input.x, 0, movement_input.y)
    if direction:
      velocity.x = direction.x
      velocity.z = direction.z
    else:
      velocity.x = move_toward(velocity.x, 0, delta)
      velocity.z = move_toward(velocity.z, 0, delta)

    move_and_slide()

  func _physics_process(delta):
    var is_colliding = _process_on_physical_movement(delta)
    if !is_colliding:
      _process_rotation_on_input(delta)
      _process_movement_on_input(delta)

Khi người chơi đi đến nơi họ không nên đến
------------------------------------------

Hãy hình dung tình huống người chơi đang ở bên ngoài một căn phòng bị khóa. Bạn không muốn người chơi đi vào căn phòng đó cho đến khi cửa được mở khóa. Bạn cũng không muốn người chơi nhìn thấy bên trong căn phòng.

Logic di chuyển người chơi qua input từ controller đã ngăn việc này khá hiệu quả. Người chơi gặp một static body, và code ngăn họ di chuyển vào căn phòng.

Tuy nhiên, với XR, không có gì ngăn người chơi thực sự bước về phía trước.

Với cả hai cách tiếp cận đã hoàn thiện ở trên, chúng ta sẽ ngăn character body di chuyển đến nơi người chơi không thể đi. Vì người chơi đã thực sự di chuyển đến vị trí này, camera giờ sẽ di chuyển vào trong phòng.

Giải pháp hợp lý là ngăn hoàn toàn chuyển động và điều chỉnh vị trí của điểm XR origin để người chơi vẫn ở bên ngoài căn phòng.

Vấn đề của cách tiếp cận này là chuyển động vật lý giờ không được tái hiện trong không gian ảo. Điều này sẽ khiến người chơi buồn nôn.

Thay vào đó, nhiều game XR sẽ đo khoảng cách giữa vị trí thực tế của người chơi và vị trí mà virtual body của người chơi bị bỏ lại phía sau. Khi khoảng cách này tăng lên, thường đến vài centimet, màn hình sẽ từ từ chuyển sang màu đen.

Các giải pháp ở trên cho phép chúng ta thêm logic này vào code ở cuối bước 1.

Một số cải tiến bổ sung cho code đã trình bày có thể là:

  - cho phép input từ controller miễn là khoảng cách này vẫn còn nhỏ,
  - vẫn áp dụng gravity cho người chơi ngay cả khi input từ controller bị tắt.

.. note::
  Các bản demo chuyển động trong demo repository của chúng ta có một ví dụ về việc làm đen màn hình khi người dùng đi vào những khu vực bị hạn chế.

Các đề xuất cải tiến khác
-------------------------

Nội dung trên cung cấp hai lựa chọn tốt làm điểm khởi đầu để triển khai các game XR với không gian phòng.

Dưới đây là một vài điểm đáng lưu ý khác mà bạn có thể sẽ muốn triển khai:

  * Độ cao của camera có thể được dùng để phát hiện người chơi đang đứng, ngồi xổm, nhảy hay nằm. Bạn có thể điều chỉnh kích thước và hướng của collision shape cho phù hợp. Sẽ càng tốt hơn nếu bạn thêm nhiều collision shape để đầu và thân có các shape riêng với kích thước chính xác hơn.
  * Khi một scene được tải lần đầu, người chơi có thể ở cách xa tâm của không gian tracking. Điều này có thể khiến người chơi xuất hiện trong một căn phòng khác với origin point của chúng ta. Lúc này, game sẽ cố gắng di chuyển player body từ vị trí bắt đầu đến nơi người chơi đang đứng nhưng sẽ thất bại. Bạn nên triển khai một hàm reset để di chuyển origin point, đưa người chơi vào đúng vị trí bắt đầu.

Cả hai cải tiến trên đều yêu cầu người chơi đã sẵn sàng và đứng thẳng. Tuy nhiên, không có gì đảm bảo điều đó vì người chơi có thể vẫn đang đeo headset.

Nhiều game, bao gồm XR Tools, giải quyết vấn đề này bằng cách thêm intro screen hoặc loading screen, trong đó người chơi phải nhấn một nút khi đã sẵn sàng. Môi trường khởi đầu này thường là một khu vực rộng, nơi vị trí của người chơi ít ảnh hưởng đến những gì họ nhìn thấy. Khi người chơi đã sẵn sàng và nhấn nút, đó là thời điểm bạn ghi lại vị trí và độ cao của camera.
