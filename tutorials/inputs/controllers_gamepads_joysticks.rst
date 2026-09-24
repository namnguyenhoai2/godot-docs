.. _doc_controllers_gamepads_joysticks:

Bộ điều khiển, gamepad và cần điều khiển
========================================

Godot hỗ trợ sẵn hàng trăm mẫu bộ điều khiển. Bộ điều khiển được hỗ trợ trên Windows, macOS, Linux, Android, iOS và Web.

.. note::

    Kể từ Godot 4.5, engine dựa vào `SDL 3 <https://www.libsdl.org/index.php>`__ để hỗ trợ bộ điều khiển trên Windows, macOS và Linux. Điều này có nghĩa là danh sách các bộ điều khiển được hỗ trợ và cách chúng hoạt động sẽ gần như khớp với những gì có trong các game và engine khác sử dụng SDL 3. Lưu ý rằng SDL chỉ được dùng cho input, không dùng cho cửa sổ hoặc âm thanh.

    Trước Godot 4.5, engine sử dụng mã hỗ trợ bộ điều khiển riêng. Điều này có thể khiến một số bộ điều khiển hoạt động không chính xác. Mã tùy chỉnh này vẫn được dùng để hỗ trợ bộ điều khiển trên Android và Web, vì vậy có thể gây ra các vấn đề chỉ xuất hiện trên những nền tảng đó.

Lưu ý rằng các thiết bị chuyên dụng hơn như vô lăng, bàn đạp bánh lái và `HOTAS <https://en.wikipedia.org/wiki/HOTAS>`__ ít được kiểm thử hơn và có thể không phải lúc nào cũng hoạt động như mong đợi. Việc ghi đè force feedback cho những thiết bị đó cũng chưa được triển khai. Nếu bạn có một trong những thiết bị này, đừng ngần ngại `báo lỗi trên GitHub <https://github.com/godotengine/godot/blob/master/CONTRIBUTING.md#reporting-bugs>`__.

Trong hướng dẫn này, bạn sẽ học:

- **Cách viết logic input để hỗ trợ cả input từ bàn phím và bộ điều khiển.**
- **Bộ điều khiển có thể hoạt động khác với input từ bàn phím/chuột như thế nào.**
- **Cách khắc phục sự cố với bộ điều khiển trong Godot.**

Hỗ trợ input đa dạng
--------------------

Nhờ hệ thống input action của Godot, bạn có thể hỗ trợ cả input từ bàn phím và bộ điều khiển mà không cần viết các nhánh mã riêng biệt. Thay vì hardcode phím hoặc nút bộ điều khiển trong các script, bạn nên tạo *input actions* trong Project Settings; các action này sẽ tham chiếu đến những input phím và bộ điều khiển được chỉ định.

Input actions được giải thích chi tiết trên :ref:`doc_inputevent`.

.. note::

    Không giống input từ bàn phím, việc hỗ trợ cả input từ chuột và bộ điều khiển cho một action (chẳng hạn như quan sát xung quanh trong game góc nhìn thứ nhất) sẽ yêu cầu các nhánh mã khác nhau vì chúng phải được xử lý riêng biệt.

Tôi nên sử dụng phương thức singleton Input nào?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có 3 cách để nhận input theo cách có nhận biết analog:

- Khi bạn có hai trục (chẳng hạn như chuyển động bằng joystick hoặc WASD) và muốn cả hai trục hoạt động như một input duy nhất, hãy sử dụng ``Input.get_vector()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `velocity` sẽ là một Vector2 nằm giữa `Vector2(-1.0, -1.0)` và `Vector2(1.0, 1.0)`.
    # Cách này xử lý deadzone đúng đắn trong hầu hết trường hợp sử dụng.
    # Deadzone kết quả sẽ có dạng hình tròn, như thông thường nên có.
    var velocity = Input.get_vector("move_left", "move_right", "move_forward", "move_back")

    # Dòng bên dưới tương tự như `get_vector()`, ngoại trừ việc nó xử lý
    # deadzone theo cách kém tối ưu hơn. Deadzone kết quả sẽ có
    # dạng gần giống hình vuông trong khi lý tưởng nhất là có dạng hình tròn.
    var velocity = Vector2(
            Input.get_action_strength("move_right") - Input.get_action_strength("move_left"),
            Input.get_action_strength("move_back") - Input.get_action_strength("move_forward")
    ).limit_length(1.0)

 .. code-tab:: csharp

    // `velocity` sẽ là một Vector2 nằm giữa `Vector2(-1.0, -1.0)` và `Vector2(1.0, 1.0)`.
    // Cách này xử lý deadzone đúng đắn trong hầu hết trường hợp sử dụng.
    // Deadzone kết quả sẽ có dạng hình tròn, như thông thường nên có.
    Vector2 velocity = Input.GetVector("move_left", "move_right", "move_forward", "move_back");

    // Dòng bên dưới tương tự như `get_vector()`, ngoại trừ việc nó xử lý
    // deadzone theo cách kém tối ưu hơn. Deadzone kết quả sẽ có
    // dạng gần giống hình vuông trong khi lý tưởng nhất là có dạng hình tròn.
    Vector2 velocity = new Vector2(
            Input.GetActionStrength("move_right") - Input.GetActionStrength("move_left"),
            Input.GetActionStrength("move_back") - Input.GetActionStrength("move_forward")
    ).LimitLength(1.0);

- Khi bạn có một trục có thể di chuyển theo cả hai hướng (chẳng hạn như cần ga trên cần điều khiển bay), hoặc khi muốn xử lý riêng từng trục, hãy sử dụng ``Input.get_axis()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `walk` sẽ là một số dấu phẩy động nằm giữa `-1.0` và `1.0`.
    var walk = Input.get_axis("move_left", "move_right")

    # Dòng bên trên là dạng viết ngắn hơn của:
    var walk = Input.get_action_strength("move_right") - Input.get_action_strength("move_left")

 .. code-tab:: csharp

    // `walk` sẽ là một số dấu phẩy động nằm giữa `-1.0` và `1.0`.
    float walk = Input.GetAxis("move_left", "move_right");

    // Dòng bên trên là dạng viết ngắn hơn của:
    float walk = Input.GetActionStrength("move_right") - Input.GetActionStrength("move_left");

- Đối với các loại input analog khác, chẳng hạn như xử lý cò hoặc xử lý từng hướng một, hãy sử dụng ``Input.get_action_strength()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `strength` sẽ là một số dấu phẩy động nằm giữa `0.0` và `1.0`.
    var strength = Input.get_action_strength("accelerate")

 .. code-tab:: csharp

    // `strength` sẽ là một số dấu phẩy động nằm giữa `0.0` và `1.0`.
    float strength = Input.GetActionStrength("accelerate");

Đối với input digital/boolean không phải analog (chỉ có các giá trị "được nhấn" hoặc "không được nhấn"), chẳng hạn như nút bộ điều khiển, nút chuột hoặc phím bàn phím, hãy sử dụng ``Input.is_action_pressed()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `jumping` sẽ là một boolean có giá trị `true` hoặc `false`.
    var jumping = Input.is_action_pressed("jump")

 .. code-tab:: csharp

    // `jumping` sẽ là một boolean có giá trị `true` hoặc `false`.
    bool jumping = Input.IsActionPressed("jump");

.. note::

    Nếu bạn cần biết liệu input có *vừa mới* được nhấn trong frame trước hay không, hãy sử dụng ``Input.is_action_just_pressed()`` thay vì ``Input.is_action_pressed()``. Không giống ``Input.is_action_pressed()``, vốn trả về ``true`` trong suốt thời gian input được giữ, ``Input.is_action_just_pressed()`` chỉ trả về ``true`` trong một frame sau khi nút được nhấn.

Rung
----

Rung (còn gọi là *phản hồi xúc giác*) có thể được dùng để tăng cảm giác chân thực cho game. Ví dụ, trong game đua xe, bạn có thể truyền đạt bề mặt mà xe đang chạy qua bằng rung, hoặc tạo rung đột ngột khi xảy ra va chạm.

Sử dụng phương thức của singleton Input để
:ref:`start_joy_vibration<class_Input_method_start_joy_vibration>` bắt đầu rung gamepad. Sử dụng
:ref:`stop_joy_vibration<class_Input_method_stop_joy_vibration>` để dừng rung sớm (hữu ích nếu không chỉ định thời lượng khi bắt đầu).

Trên các thiết bị di động, bạn cũng có thể sử dụng
:ref:`vibrate_handheld<class_Input_method_vibrate_handheld>` để làm rung chính thiết bị (độc lập với gamepad). Trên Android, bạn cần bật quyền ``VIBRATE`` trong preset xuất Android trước khi xuất project.

.. note::

   Rung có thể gây khó chịu cho một số người chơi. Hãy đảm bảo cung cấp một thanh trượt trong game để tắt rung hoặc giảm cường độ rung.

Sự khác biệt giữa input từ bàn phím/chuột và controller
-------------------------------------------------------

Nếu đã quen xử lý input từ bàn phím và chuột, bạn có thể ngạc nhiên trước cách controller xử lý các tình huống cụ thể.

Vùng chết
~~~~~~~~~

Không giống bàn phím và chuột, controller cung cấp các trục với input *analog*. Ưu điểm của input analog là chúng mang lại thêm tính linh hoạt cho các action. Không giống input digital, vốn chỉ có thể cung cấp cường độ ``0.0`` và ``1.0``, input analog có thể cung cấp *bất kỳ* cường độ nào giữa ``0.0`` và ``1.0``. Nhược điểm là nếu không có hệ thống vùng chết, cường độ của một trục analog sẽ không bao giờ bằng ``0.0`` do cách controller được cấu tạo về mặt vật lý. Thay vào đó, nó sẽ duy trì ở một giá trị thấp chẳng hạn như ``0.062``. Hiện tượng này được gọi là *drifting* và có thể dễ nhận thấy hơn trên các controller cũ hoặc bị lỗi.

Hãy lấy một game đua xe làm ví dụ thực tế. Nhờ input analog, chúng ta có thể điều khiển xe rẽ chậm theo hướng này hoặc hướng kia. Tuy nhiên, nếu không có hệ thống vùng chết, xe sẽ từ từ tự rẽ ngay cả khi người chơi không chạm vào joystick. Điều này là do cường độ của trục định hướng sẽ không bằng ``0.0`` khi chúng ta mong đợi. Vì không muốn xe tự rẽ trong trường hợp này, chúng ta xác định giá trị "vùng chết" là ``0.2``, giá trị này sẽ bỏ qua mọi input có cường độ thấp hơn ``0.2``. Giá trị vùng chết lý tưởng đủ cao để bỏ qua input do joystick drifting gây ra, nhưng đủ thấp để không bỏ qua input thực tế từ người chơi.

Godot có hệ thống vùng chết tích hợp để xử lý vấn đề này. Giá trị mặc định là ``0.5``, nhưng bạn có thể điều chỉnh giá trị này cho từng action trong tab Input Map của Project Settings. Đối với ``Input.get_vector()``, vùng chết có thể được chỉ định dưới dạng tham số thứ 5 tùy chọn. Nếu không được chỉ định, nó sẽ tính giá trị vùng chết trung bình từ tất cả action trong vector.

Các event "Echo"
~~~~~~~~~~~~~~~~

Không giống input từ bàn phím, việc giữ một nút controller, chẳng hạn như hướng trên D-pad, **không** tạo ra các event input lặp lại theo những khoảng thời gian cố định (còn gọi là event "echo"). Điều này là do ngay từ đầu, hệ điều hành không bao giờ gửi event "echo" cho input từ controller.

Nếu muốn các nút controller gửi event echo, bạn sẽ phải tạo
:ref:`class_InputEvent` object bằng code và phân tích chúng bằng
:ref:`Input.parse_input_event() <class_Input_method_parse_input_event>` theo các khoảng thời gian đều đặn. Bạn có thể thực hiện việc này với sự trợ giúp của node :ref:`class_Timer`.

Tiêu điểm cửa sổ
~~~~~~~~~~~~~~~~

Không giống input từ bàn phím, theo mặc định input từ controller có thể được **tất cả** cửa sổ trên hệ điều hành nhận biết, bao gồm cả các cửa sổ không có tiêu điểm.

Mặc dù điều này hữu ích cho `chức năng chia màn hình của bên thứ ba <https://nucleus-coop.github.io/>`__, nó cũng có thể gây ra tác động không mong muốn. Người chơi có thể vô tình gửi input từ controller đến project đang chạy trong khi tương tác với một cửa sổ khác.

Nếu muốn bỏ qua các event input từ controller khi project không có tiêu điểm, hãy đặt :ref:`ProjectSettings.input_devices/joypads/ignore_joypad_on_unfocused_application <class_ProjectSettings_property_input_devices/joypads/ignore_joypad_on_unfocused_application>` thành ``true``. Ngoài ra, bạn cũng có thể đặt :ref:`Input.ignore_joypad_on_unfocused_application <class_Input_property_ignore_joypad_on_unfocused_application>` thành ``true``.

Ngăn tiết kiệm năng lượng
~~~~~~~~~~~~~~~~~~~~~~~~~

Không giống input từ bàn phím và chuột, input từ controller **không** ngăn chế độ ngủ và các biện pháp tiết kiệm năng lượng (chẳng hạn như tắt màn hình sau khi một khoảng thời gian nhất định đã trôi qua).

Để khắc phục điều này, Godot bật tính năng ngăn tiết kiệm năng lượng theo mặc định khi project đang chạy. Nếu nhận thấy hệ thống tắt màn hình khi chơi bằng gamepad, hãy kiểm tra giá trị của **Display > Window > Energy Saving > Keep Screen On** trong Project Settings.

Xử lý sự cố
-----------

.. seealso::

    Bạn có thể xem danh sách `các vấn đề đã biết về hỗ trợ controller <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Ainput+gamepad>`__ trên GitHub.

Controller của tôi không được Godot nhận diện.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trước tiên, hãy kiểm tra xem controller của bạn có được các ứng dụng khác nhận diện hay không. Bạn có thể sử dụng website `Gamepad Tester <https://hardwaretester.com/gamepad>`__ để xác nhận controller của mình được nhận diện.

Trên Windows, Godot chỉ hỗ trợ tối đa 4 controller cùng lúc. Điều này là do Godot sử dụng API XInput, vốn bị giới hạn ở việc hỗ trợ 4 controller cùng lúc. Các controller vượt quá giới hạn này sẽ bị Godot bỏ qua.

Controller của tôi có các nút hoặc trục được ánh xạ không chính xác.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trước tiên, nếu controller của bạn cung cấp một tiện ích cập nhật firmware, hãy đảm bảo chạy tiện ích đó để nhận các bản sửa lỗi mới nhất từ nhà sản xuất. Chẳng hạn, firmware của controller Xbox One và Xbox Series có thể được cập nhật bằng `Xbox Accessories app <https://www.microsoft.com/en-us/p/xbox-accessories/9nblggh30xj3>`__. (Ứng dụng này chỉ chạy trên Windows, vì vậy bạn phải sử dụng máy Windows hoặc máy ảo Windows có hỗ trợ USB để cập nhật firmware của controller.) Sau khi cập nhật firmware của controller, hãy hủy ghép đôi controller rồi ghép đôi lại với PC nếu bạn đang sử dụng controller ở chế độ không dây.

Nếu các nút được ánh xạ không chính xác, nguyên nhân có thể là mapping sai từ cơ sở dữ liệu SDL game controller được Godot sử dụng hoặc từ `cơ sở dữ liệu game controller của Godot <https://github.com/godotengine/godot/blob/master/core/input/godotcontrollerdb.txt>`__. Trong trường hợp này, bạn sẽ cần tạo mapping tùy chỉnh cho controller của mình.

.. Nintorch: Currently Godot's Input.add_joy_mapping() is broken, it will add a new mapping
   on top of an already existing mapping from SDL (if it exists), so I'm not sure it
   should be used as an example at the moment. See GH-118606 in Godot's main repository
   for more information.

   One option is to use the mapping wizard
   in the `official Joypads demo <https://godotengine.org/asset-library/asset/2785>`__.

Có nhiều cách để tạo mapping. Một lựa chọn là khởi động Steam ở chế độ Big Picture, cấu hình controller rồi tìm trong ``config/config.vdf`` trong thư mục cài đặt Steam mục ``SDL_GamepadBind``. Một lựa chọn khác là sử dụng `ứng dụng testcontroller của SDL <https://www.libsdl.org/tmp/testcontroller.zip>`__ (liên kết này chỉ cung cấp tệp thực thi Windows). Sau khi có mapping hoạt động cho controller, bạn có thể kiểm tra mapping bằng cách định nghĩa biến môi trường ``SDL_GAMECONTROLLERCONFIG`` trước khi chạy Godot:

.. tabs::
 .. code-tab:: bash Linux/macOS

    export SDL_GAMECONTROLLERCONFIG="your:mapping:here"
    ./path/to/godot.x86_64

 .. code-tab:: bat Windows (cmd)

    set SDL_GAMECONTROLLERCONFIG=your:mapping:here
    path\to\godot.exe

 .. code-tab:: powershell Windows (PowerShell)

    $env:SDL_GAMECONTROLLERCONFIG="your:mapping:here"
    path\to\godot.exe

.. Nintorch: See the comment above on why this is commented out.
   To test mappings on non-desktop platforms or to distribute your project with
   additional controller mappings, you can add them by calling
   :ref:`Input.add_joy_mapping() <class_Input_method_add_joy_mapping>`
   as early as possible in a script's ``_ready()`` function.

Khi đã hài lòng với mapping tùy chỉnh, bạn có thể đóng góp mapping đó cho phiên bản Godot tiếp theo bằng cách mở pull request trên `cơ sở dữ liệu game controller của Godot <https://github.com/godotengine/godot/blob/master/core/input/godotcontrollerdb.txt>`__, hoặc tạo issue trong `repository Godot <https://github.com/godotengine/godot/issues>`__.

Vì Godot sử dụng SDL 3 cho input từ controller, bạn cũng nên đóng góp mapping cho thư viện SDL bằng cách mở pull request trên `cơ sở dữ liệu gamepad chính thức của SDL <https://github.com/libsdl-org/SDL/blob/main/src/joystick/SDL_gamepad_db.h>`__, hoặc tạo issue trong `repository SDL <https://github.com/libsdl-org/SDL/issues>`__.

.. note::

    Lưu ý rằng trên thị trường có các controller "generic" (thường thuộc tính ``Input.get_joy_info(device)["raw_name"]`` của chúng chứa chuỗi ``"USB Gamepad"``), và các controller generic khác nhau có thể sử dụng cùng một chipset, nhưng chúng có thể có cách bố trí nút khác nhau. Vì vậy, việc tạo mapping cho một trong các controller đó rất có thể sẽ xung đột với những controller khác, bởi engine không có cách nào phân biệt các controller sử dụng cùng chipset.

Controller của tôi hoạt động trên một nền tảng nhất định nhưng không hoạt động trên nền tảng khác.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Linux
^^^^^

Nếu bạn đang sử dụng binary engine tự biên dịch, hãy đảm bảo binary đó được biên dịch với hỗ trợ udev. Tính năng này được bật theo mặc định, nhưng bạn có thể tắt hỗ trợ udev bằng cách chỉ định ``udev=no`` trên dòng lệnh SCons. Nếu bạn đang sử dụng binary engine do một bản phân phối Linux cung cấp, hãy kiểm tra lại xem binary đó có được biên dịch với hỗ trợ udev hay không.

Controller vẫn có thể hoạt động mà không cần hỗ trợ udev, nhưng độ tin cậy sẽ thấp hơn vì phải sử dụng polling thông thường để kiểm tra xem controller có được kết nối hoặc ngắt kết nối trong khi chơi hay không (hotplugging).

Android
^^^^^^^

Như đã mô tả ở đầu trang, hỗ trợ controller trên các nền tảng di động dựa vào một implementation tùy chỉnh thay vì sử dụng SDL cho input. Điều này có nghĩa là hỗ trợ controller có thể kém tin cậy hơn so với trên các nền tảng desktop.

Hỗ trợ input từ controller dựa trên SDL trên các nền tảng di động được dự kiến sẽ có trong một bản phát hành tương lai.

Web
^^^

Hỗ trợ controller trên Web thường kém tin cậy hơn so với các nền tảng "native". Chất lượng hỗ trợ controller có xu hướng khác biệt rất lớn giữa các trình duyệt. Do đó, bạn có thể phải hướng dẫn người chơi sử dụng một trình duyệt khác nếu họ không thể làm cho controller hoạt động.

Tương tự như trên các nền tảng di động, hỗ trợ input từ controller dựa trên SDL trên nền tảng web được dự kiến sẽ có trong một bản phát hành tương lai.
