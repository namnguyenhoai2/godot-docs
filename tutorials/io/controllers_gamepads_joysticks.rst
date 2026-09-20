.. _doc_controllers_gamepads_joysticks:

Tay cầm, gamepad và joystick
============================

Godot hỗ trợ hàng trăm mẫu tay cầm ngay khi cài đặt. Tay cầm được hỗ trợ trên Windows, macOS, Linux, Android, iOS và Web.

.. note::

    Kể từ Godot 4.5, engine dựa vào `SDL 3 <https://www.libsdl.org/index.php>`__ để hỗ trợ tay cầm trên Windows, macOS và Linux. Điều này có nghĩa là danh sách tay cầm được hỗ trợ và cách chúng hoạt động sẽ tương đồng với những gì có sẵn trong các game và engine khác sử dụng SDL 3. Lưu ý rằng SDL chỉ được dùng cho input, không dùng cho windowing hoặc âm thanh.

    Trước Godot 4.5, engine sử dụng mã hỗ trợ tay cầm riêng. Điều này có thể khiến một số tay cầm hoạt động không chính xác. Mã tùy chỉnh này vẫn được dùng để hỗ trợ tay cầm trên Android và Web, vì vậy có thể gây ra các vấn đề chỉ xuất hiện trên những nền tảng đó.

Lưu ý rằng các thiết bị chuyên dụng hơn như vô lăng, bàn đạp rudder và `HOTAS <https://en.wikipedia.org/wiki/HOTAS>`__ ít được kiểm thử hơn và có thể không phải lúc nào cũng hoạt động như mong đợi. Việc ghi đè force feedback cho những thiết bị này cũng chưa được triển khai. Nếu bạn có một trong những thiết bị đó, đừng ngần ngại `report bugs on GitHub <https://github.com/godotengine/godot/blob/master/CONTRIBUTING.md#reporting-bugs>`__.

Trong hướng dẫn này, bạn sẽ học:

- **Cách viết logic input để hỗ trợ cả input từ bàn phím và tay cầm.** - **Cách tay cầm có thể hoạt động khác với input từ bàn phím/chuột.** - **Cách khắc phục sự cố với tay cầm trong Godot.**

Hỗ trợ input phổ quát
---------------------

Nhờ hệ thống input action của Godot, bạn có thể hỗ trợ cả input từ bàn phím và tay cầm mà không cần viết các nhánh code riêng biệt. Thay vì hardcode phím hoặc nút tay cầm trong các script, bạn nên tạo *input action* trong Project Settings; các action này sẽ tham chiếu đến những input phím và tay cầm cụ thể.

Input action được giải thích chi tiết trên trang :ref:`doc_inputevent`.

.. note::

    Không giống input từ bàn phím, việc hỗ trợ cả input từ chuột và tay cầm cho một action (chẳng hạn như xoay camera trong game góc nhìn thứ nhất) sẽ yêu cầu các nhánh code khác nhau vì chúng phải được xử lý riêng biệt.

Tôi nên sử dụng phương thức nào của Input singleton?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có 3 cách để lấy input theo cách có xét đến analog:

- Khi bạn có hai trục (chẳng hạn như chuyển động bằng joystick hoặc WASD) và muốn cả hai trục hoạt động như một input duy nhất, hãy sử dụng ``Input.get_vector()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `velocity` sẽ là một Vector2 nằm giữa `Vector2(-1.0, -1.0)` và `Vector2(1.0, 1.0)`.
    # Cách này xử lý deadzone chính xác trong hầu hết trường hợp sử dụng.
    # Deadzone kết quả sẽ có hình tròn, như thông thường nên có.
    var velocity = Input.get_vector("move_left", "move_right", "move_forward", "move_back")

    # Dòng bên dưới tương tự `get_vector()`, ngoại trừ việc nó xử lý
    # deadzone theo cách kém tối ưu hơn. Deadzone kết quả sẽ có
    # hình gần vuông, trong khi lý tưởng nhất là có hình tròn.
    var velocity = Vector2(
            Input.get_action_strength("move_right") - Input.get_action_strength("move_left"),
            Input.get_action_strength("move_back") - Input.get_action_strength("move_forward")
    ).limit_length(1.0)

 .. code-tab:: csharp

    // `velocity` sẽ là một Vector2 nằm giữa `Vector2(-1.0, -1.0)` và `Vector2(1.0, 1.0)`.
    // Cách này xử lý deadzone chính xác trong hầu hết trường hợp sử dụng.
    // Deadzone kết quả sẽ có hình tròn, như thông thường nên có.
    Vector2 velocity = Input.GetVector("move_left", "move_right", "move_forward", "move_back");

    // Dòng bên dưới tương tự `get_vector()`, ngoại trừ việc nó xử lý
    // deadzone theo cách kém tối ưu hơn. Deadzone kết quả sẽ có
    // hình gần vuông, trong khi lý tưởng nhất là có hình tròn.
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

- Đối với các loại input analog khác, chẳng hạn như xử lý trigger hoặc xử lý từng hướng một, hãy sử dụng ``Input.get_action_strength()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `strength` sẽ là một số dấu phẩy động nằm giữa `0.0` và `1.0`.
    var strength = Input.get_action_strength("accelerate")

 .. code-tab:: csharp

    // `strength` sẽ là một số dấu phẩy động nằm giữa `0.0` và `1.0`.
    float strength = Input.GetActionStrength("accelerate");

Đối với input digital/boolean không phải analog (chỉ có giá trị "pressed" hoặc "not pressed"), chẳng hạn như nút tay cầm, nút chuột hoặc phím bàn phím, hãy sử dụng ``Input.is_action_pressed()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # `jumping` sẽ là một boolean có giá trị `true` hoặc `false`.
    var jumping = Input.is_action_pressed("jump")

 .. code-tab:: csharp

    // `jumping` sẽ là một boolean có giá trị `true` hoặc `false`.
    bool jumping = Input.IsActionPressed("jump");

.. note::

    Nếu cần biết một input có *vừa mới* được nhấn ở frame trước hay không, hãy sử dụng ``Input.is_action_just_pressed()`` thay vì ``Input.is_action_pressed()``. Không giống ``Input.is_action_pressed()``, vốn trả về ``true`` trong suốt thời gian input được giữ, ``Input.is_action_just_pressed()`` sẽ chỉ trả về ``true`` trong một frame sau khi nút được nhấn.

Rung
----

Rung (còn gọi là *haptic feedback*) có thể được dùng để tăng cảm giác chân thực của game. Chẳng hạn, trong game đua xe, bạn có thể truyền tải bề mặt mà xe đang chạy qua rung, hoặc tạo một lần rung đột ngột khi xảy ra va chạm.

Sử dụng
:ref:`start_joy_vibration<class_Input_method_start_joy_vibration>` method to
của Input singleton để bắt đầu rung một gamepad. Sử dụng
:ref:`stop_joy_vibration<class_Input_method_stop_joy_vibration>` to stop
rung sớm (hữu ích nếu không chỉ định thời lượng khi bắt đầu).

Trên các thiết bị di động, bạn cũng có thể sử dụng
:ref:`vibrate_handheld<class_Input_method_vibrate_handheld>` to vibrate the
chính thiết bị đó (độc lập với gamepad). Trên Android, cần bật quyền ``VIBRATE`` trong Android export preset trước khi export project.

.. note::

   Rung có thể gây khó chịu cho một số người chơi. Hãy đảm bảo cung cấp một thanh trượt trong game để tắt rung hoặc giảm cường độ rung.

Sự khác biệt giữa input từ bàn phím/chuột và tay cầm
----------------------------------------------------

Nếu bạn đã quen xử lý input từ bàn phím và chuột, bạn có thể bất ngờ trước cách tay cầm xử lý một số tình huống cụ thể.

Dead zone
~~~~~~~~~

Không giống bàn phím và chuột, tay cầm cung cấp các trục có input *analog*. Ưu điểm của input analog là chúng mang lại thêm tính linh hoạt cho các action. Không giống input digital chỉ có thể cung cấp cường độ ``0.0`` và ``1.0``, input analog có thể cung cấp *bất kỳ* cường độ nào giữa ``0.0`` và ``1.0``. Nhược điểm là nếu không có hệ thống deadzone, cường độ của một trục analog sẽ không bao giờ bằng ``0.0`` do cách tay cầm được chế tạo về mặt vật lý. Thay vào đó, nó sẽ dao động ở một giá trị thấp như ``0.062``. Hiện tượng này được gọi là *drifting* và có thể dễ nhận thấy hơn trên các tay cầm cũ hoặc bị lỗi.

Hãy lấy game đua xe làm ví dụ trong thực tế. Nhờ input analog, chúng ta có thể từ từ đánh lái xe theo hướng này hoặc hướng khác. Tuy nhiên, nếu không có hệ thống deadzone, xe sẽ từ từ tự đánh lái ngay cả khi người chơi không chạm vào joystick. Đó là vì cường độ của trục định hướng sẽ không bằng ``0.0`` khi chúng ta mong đợi. Vì không muốn xe tự đánh lái trong trường hợp này, chúng ta xác định giá trị "dead zone" là ``0.2``, giá trị này sẽ bỏ qua mọi input có cường độ thấp hơn ``0.2``. Giá trị dead zone lý tưởng đủ cao để bỏ qua input do joystick bị drifting, nhưng đủ thấp để không bỏ qua input thực sự từ người chơi.

Godot có hệ thống deadzone tích hợp để giải quyết vấn đề này. Giá trị mặc định là ``0.5``, nhưng bạn có thể điều chỉnh theo từng action trong tab Input Map của Project Settings. Đối với ``Input.get_vector()``, deadzone có thể được chỉ định dưới dạng tham số thứ 5 tùy chọn. Nếu không được chỉ định, nó sẽ tính giá trị deadzone trung bình từ tất cả action trong vector.

Sự kiện "Echo"
~~~~~~~~~~~~~~

Không giống input từ bàn phím, việc giữ một nút tay cầm, chẳng hạn như hướng trên D-pad, sẽ **không** tạo ra các sự kiện input lặp lại theo những khoảng thời gian cố định (còn gọi là sự kiện "echo"). Điều này là do hệ điều hành ngay từ đầu không bao giờ gửi sự kiện "echo" cho input từ tay cầm.

Nếu muốn các nút tay cầm gửi sự kiện echo, bạn sẽ phải tạo
:ref:`class_InputEvent` objects by code and parse them using
:ref:`Input.parse_input_event() <class_Input_method_parse_input_event>`
theo các khoảng thời gian đều đặn. Bạn có thể thực hiện việc này với sự trợ giúp của một node :ref:`class_Timer`.

Focus của cửa sổ
~~~~~~~~~~~~~~~~

Không giống input từ bàn phím, theo mặc định, input từ tay cầm có thể được nhìn thấy bởi **tất cả** cửa sổ trên hệ điều hành, bao gồm cả các cửa sổ không có focus.

Mặc dù điều này hữu ích cho `third-party split screen functionality <https://nucleus-coop.github.io/>`__, nó cũng có thể gây ra tác động không mong muốn. Người chơi có thể vô tình gửi input từ tay cầm đến project đang chạy trong khi tương tác với một cửa sổ khác.

Nếu muốn bỏ qua các sự kiện input từ tay cầm khi project không có focus, hãy đặt :ref:`ProjectSettings.input_devices/joypads/ignore_joypad_on_unfocused_application<class_ProjectSettings_property_input_devices/joypads/ignore_joypad_on_unfocused_application>` thành ``true``. Ngoài ra, bạn cũng có thể đặt :ref:`Input.ignore_joypad_on_unfocused_application <class_Input_property_ignore_joypad_on_unfocused_application>` thành ``true``.

Ngăn tiết kiệm năng lượng
~~~~~~~~~~~~~~~~~~~~~~~~~

Không giống input từ bàn phím và chuột, input từ tay cầm **không** ngăn chế độ sleep và các biện pháp tiết kiệm năng lượng (chẳng hạn như tắt màn hình sau khi một khoảng thời gian nhất định đã trôi qua).

Để khắc phục điều này, Godot mặc định bật tính năng ngăn tiết kiệm năng lượng khi project đang chạy. Nếu nhận thấy hệ thống tắt màn hình khi chơi bằng gamepad, hãy kiểm tra giá trị **Display > Window > Energy Saving > Keep Screen On** trong Project Settings.

Khắc phục sự cố
---------------

.. seealso::

    Bạn có thể xem danh sách `known issues with controller support <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Ainput+gamepad>`__ trên GitHub.

Godot không nhận diện tay cầm của tôi.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trước tiên, hãy kiểm tra xem tay cầm có được các ứng dụng khác nhận diện hay không. Bạn có thể sử dụng website `Gamepad Tester <https://hardwaretester.com/gamepad>`__ để xác nhận tay cầm của mình được nhận diện.

Trên Windows, Godot chỉ hỗ trợ tối đa 4 controller cùng lúc. Điều này là do Godot sử dụng API XInput, vốn bị giới hạn ở việc hỗ trợ 4 controller cùng lúc. Các controller bổ sung vượt quá giới hạn này sẽ bị Godot bỏ qua.

Controller của tôi có các nút hoặc trục được ánh xạ không chính xác.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trước tiên, nếu controller của bạn cung cấp một tiện ích cập nhật firmware nào đó, hãy đảm bảo chạy tiện ích này để nhận các bản sửa lỗi mới nhất từ nhà sản xuất. Chẳng hạn, firmware của các controller Xbox One và Xbox Series có thể được cập nhật bằng `Xbox Accessories app <https://www.microsoft.com/en-us/p/xbox-accessories/9nblggh30xj3>`__. (Ứng dụng này chỉ chạy trên Windows, vì vậy bạn phải sử dụng máy Windows hoặc máy ảo Windows có hỗ trợ USB để cập nhật firmware của controller.) Sau khi cập nhật firmware của controller, hãy hủy ghép nối controller rồi ghép nối lại với PC nếu bạn đang sử dụng controller ở chế độ không dây.

Nếu các nút được ánh xạ không chính xác, nguyên nhân có thể là do ánh xạ sai từ cơ sở dữ liệu SDL game controller được Godot sử dụng hoặc từ `Godot game controller database <https://github.com/godotengine/godot/blob/master/core/input/godotcontrollerdb.txt>`__. Trong trường hợp này, bạn sẽ cần tạo ánh xạ tùy chỉnh cho controller của mình.

.. Nintorch: Hiện tại, Input.add_joy_mapping() của Godot bị lỗi; hàm này sẽ thêm một ánh xạ mới chồng lên ánh xạ đã tồn tại từ SDL (nếu có), vì vậy hiện tại tôi không chắc có nên dùng nó làm ví dụ hay không. Xem GH-118606 trong repository chính của Godot để biết thêm thông tin.

   Một lựa chọn là sử dụng trình hướng dẫn ánh xạ trong `official Joypads demo <https://godotengine.org/asset-library/asset/2785>`__.

There are many ways to create mappings. One option is to start Steam in Big Picture mode, configure the controller and then look in ``config/config.vdf`` in the Steam installation directory for the ``SDL_GamepadBind`` entry. Another option is to use `SDL's testcontroller application <https://www.libsdl.org/tmp/testcontroller.zip>`__ (the link only provides a Windows executable). Once you have a working mapping for your controller, you can test it by defining the ``SDL_GAMECONTROLLERCONFIG`` environment variable before running Godot:

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

.. Nintorch: Xem nhận xét bên trên để biết lý do đoạn mã này bị comment out. Để kiểm tra ánh xạ trên các nền tảng không phải desktop hoặc phân phối project của bạn kèm theo các ánh xạ controller bổ sung, bạn có thể thêm chúng bằng cách gọi
   :ref:`Input.add_joy_mapping() <class_Input_method_add_joy_mapping>`
   sớm nhất có thể trong hàm ``_ready()`` của một script.

Sau khi hài lòng với ánh xạ tùy chỉnh, bạn có thể đóng góp ánh xạ này cho phiên bản Godot tiếp theo bằng cách mở một pull request trên `Godot game controller database <https://github.com/godotengine/godot/blob/master/core/input/godotcontrollerdb.txt>`__ hoặc tạo một issue trong `Godot repository <https://github.com/godotengine/godot/issues>`__.

Vì Godot sử dụng SDL 3 cho input của controller, bạn cũng nên đóng góp ánh xạ này cho thư viện SDL bằng cách mở một pull request trên `official SDL gamepad database <https://github.com/libsdl-org/SDL/blob/main/src/joystick/SDL_gamepad_db.h>`__ hoặc tạo một issue trong `SDL repository <https://github.com/libsdl-org/SDL/issues>`__.

.. note::

    Lưu ý rằng trên thị trường có các controller "generic" (thường thuộc tính ``Input.get_joy_info(device)["raw_name"]`` của chúng chứa chuỗi ``"USB Gamepad"``), và các controller generic khác nhau có thể sử dụng cùng một chipset nhưng có cách bố trí nút khác nhau. Vì vậy, việc tạo ánh xạ cho một trong các controller này rất có thể sẽ xung đột với các controller khác, bởi engine không có cách nào phân biệt các controller sử dụng cùng một chipset.

Controller của tôi hoạt động trên một nền tảng nhất định nhưng không hoạt động trên nền tảng khác.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Linux
^^^^^

Nếu bạn đang sử dụng binary engine tự biên dịch, hãy đảm bảo nó được biên dịch với hỗ trợ udev. Tính năng này được bật theo mặc định, nhưng bạn có thể tắt hỗ trợ udev bằng cách chỉ định ``udev=no`` trên dòng lệnh SCons. Nếu bạn đang sử dụng binary engine do một bản phân phối Linux cung cấp, hãy kiểm tra lại xem nó có được biên dịch với hỗ trợ udev hay không.

Controller vẫn có thể hoạt động mà không cần hỗ trợ udev, nhưng độ tin cậy sẽ thấp hơn vì phải sử dụng polling thường xuyên để kiểm tra xem controller có được kết nối hoặc ngắt kết nối trong khi chơi hay không (hotplugging).

Android
^^^^^^^

Như đã mô tả ở đầu trang, hỗ trợ controller trên các nền tảng di động dựa vào một triển khai tùy chỉnh thay vì sử dụng SDL cho input. Điều này có nghĩa là hỗ trợ controller có thể kém tin cậy hơn so với trên các nền tảng desktop.

Hỗ trợ input của controller dựa trên SDL trên các nền tảng di động được lên kế hoạch cho một bản phát hành trong tương lai.

Web
^^^

Hỗ trợ controller trên Web thường kém tin cậy hơn so với các nền tảng "native". Chất lượng hỗ trợ controller có xu hướng khác biệt rất lớn giữa các trình duyệt. Do đó, bạn có thể phải hướng dẫn người chơi sử dụng một trình duyệt khác nếu họ không thể khiến controller của mình hoạt động.

Tương tự như trên các nền tảng di động, hỗ trợ input của controller dựa trên SDL trên nền tảng Web được lên kế hoạch cho một bản phát hành trong tương lai.
