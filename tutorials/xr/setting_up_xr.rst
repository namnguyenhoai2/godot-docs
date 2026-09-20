.. _doc_setting_up_xr:

Thiết lập XR
============

Giới thiệu về hệ thống XR trong Godot
-------------------------------------

Godot cung cấp một hệ thống XR dạng mô-đun, giúp trừu tượng hóa nhiều đặc thù của các nền tảng XR khác nhau khỏi người dùng. Ở trung tâm là :ref:`XRServer <class_xrserver>`, đóng vai trò như một giao diện trung tâm của hệ thống XR, cho phép người dùng khám phá các giao diện và tương tác với các thành phần của hệ thống XR.

Mỗi nền tảng XR được hỗ trợ đều được triển khai dưới dạng một :ref:`XRInterface <class_xrinterface>`. Bạn có thể tìm thấy danh sách các nền tảng được hỗ trợ trên trang danh sách tính năng :ref:`here <doc_xr_support>`. Các giao diện được hỗ trợ sẽ đăng ký với :ref:`XRServer <class_xrserver>` và có thể được truy vấn bằng phương thức ``find_interface`` trên :ref:`XRServer <class_xrserver>`. Khi tìm thấy giao diện mong muốn, bạn có thể khởi tạo giao diện đó bằng cách gọi ``initialize``.

.. warning::
    Một giao diện đã đăng ký chỉ có nghĩa là giao diện đó khả dụng; nếu giao diện không được hệ thống host hỗ trợ, quá trình khởi tạo có thể thất bại và trả về ``false``. Điều này có thể xảy ra vì nhiều lý do, và đáng tiếc là lý do sẽ khác nhau tùy nền tảng. Có thể người dùng chưa cài đặt phần mềm cần thiết hoặc đơn giản là chưa kết nối headset. Vì vậy, với tư cách nhà phát triển, bạn phải xử lý đúng khi một giao diện không thể khởi tạo.

Do các yêu cầu đặc biệt về việc xuất hình ảnh trong XR, đặc biệt là đối với các thiết bị đeo trên đầu cung cấp hình ảnh khác nhau cho mỗi mắt, :ref:`XRServer <class_xrserver>` trong Godot sẽ ghi đè nhiều tính năng khác nhau trong hệ thống rendering. Đối với các thiết bị độc lập, điều này có nghĩa là đầu ra cuối cùng được xử lý bởi :ref:`XRInterface <class_xrinterface>` và hệ thống xuất hình ảnh thông thường của Godot bị vô hiệu hóa. Đối với các thiết bị XR dành cho desktop hoạt động như màn hình thứ hai, bạn có thể dành riêng một :ref:`Viewport <class_viewport>` để xử lý đầu ra XR, đồng thời giữ cửa sổ Godot chính để hiển thị nội dung thay thế.

.. note::
    Lưu ý rằng chỉ một giao diện có thể chịu trách nhiệm xử lý đầu ra đến thiết bị XR. Giao diện này được gọi là giao diện chính và theo mặc định sẽ là giao diện đầu tiên được khởi tạo. Vì vậy, hiện tại Godot chỉ hỗ trợ các triển khai với một headset duy nhất. Việc có thêm một giao diện phụ là khả thi nhưng ngày càng ít phổ biến, chẳng hạn để bổ sung tracking cho một thiết bị vốn chỉ hỗ trợ 3DOF.

Có ba loại node đặc thù của XR mà bạn sẽ thấy trong gần như mọi ứng dụng XR:

- :ref:`XROrigin3D <class_xrorigin3d>` về cơ bản đại diện cho tâm của không gian chơi. Đây là một cách diễn đạt đơn giản hóa quá mức, nhưng chúng ta sẽ tìm hiểu chi tiết hơn sau. Mọi đối tượng được nền tảng XR tracking trong không gian thực đều được định vị dựa trên điểm này. - :ref:`XRCamera3D <class_xrcamera3d>` đại diện cho camera (stereo) được sử dụng khi rendering đầu ra cho thiết bị XR. Vị trí của node này do hệ thống XR điều khiển và được tự động cập nhật bằng thông tin tracking do nền tảng XR cung cấp. - :ref:`XRController3D <class_xrcontroller3d>` đại diện cho một controller được người chơi sử dụng; thông thường sẽ có hai controller, mỗi tay cầm một chiếc. Các node này cho phép truy cập nhiều trạng thái khác nhau trên các controller và phát tín hiệu khi người chơi nhấn các nút trên đó. Vị trí của node này do hệ thống XR điều khiển và được tự động cập nhật bằng thông tin tracking do nền tảng XR cung cấp.

Có những node liên quan đến XR khác và còn nhiều điều cần nói về ba node này, nhưng chúng ta sẽ tìm hiểu thêm ở phần sau.

Nên sử dụng Renderer nào
------------------------

Godot có 3 tùy chọn renderer cho project: Compatibility, Mobile và Forward+. Khuyến nghị hiện tại là sử dụng renderer Mobile cho mọi project VR trên desktop hoặc mọi project chạy trên headset độc lập như Meta Quest 3. Các project XR vẫn sẽ chạy với renderer Forward+, nhưng hiện tại renderer này chưa được tối ưu tốt cho XR so với hai renderer còn lại.

OpenXR
------

OpenXR là API tiêu chuẩn của ngành, cho phép các nền tảng XR khác nhau tương tác với các ứng dụng XR. Tiêu chuẩn này là một open standard do Khronos Group duy trì và vì vậy rất phù hợp với định hướng của Godot. Do đó, chúng ta sẽ sử dụng nó làm ví dụ trong phần giới thiệu này. Hãy xem các chương tương ứng để biết sự khác biệt trong những API khác.

Triển khai Vulkan của OpenXR được tích hợp chặt chẽ với Vulkan và tiếp quản một phần hệ thống Vulkan. Điều này đòi hỏi phải tích hợp chặt chẽ một số tính năng đồ họa cốt lõi trong renderer Vulkan, những tính năng cần được thiết lập trước hệ thống XR. Đây là một trong những yếu tố chính dẫn đến quyết định đưa OpenXR vào làm giao diện cốt lõi.

Điều này cũng có nghĩa là OpenXR cần được bật khi Godot khởi động để thiết lập mọi thứ chính xác. Hãy kiểm tra thiết lập :ref:`Enabled<class_ProjectSettings_property_xr/openxr/enabled>` trong project settings tại **XR > OpenXR**.

.. image:: img/openxr_enabled.webp

Bạn cũng có thể tìm thấy một số thiết lập khác liên quan đến OpenXR tại đây. Không thể thay đổi các thiết lập này trong khi ứng dụng đang chạy. Các thiết lập mặc định sẽ giúp chúng ta bắt đầu, nhưng để biết thêm thông tin về các thiết lập ở đây, hãy xem :ref:`doc_openxr_settings`.

Bạn cũng cần vào **XR > Shaders** trong project settings và đánh dấu
:ref:`Enabled<class_ProjectSettings_property_xr/shaders/enabled>`
ô để bật chúng. Sau khi hoàn tất, hãy nhấp vào nút **Save & Restart**.

.. image:: img/xr_shaders.webp

.. warning::
    Nhiều hiệu ứng post-process vẫn chưa được cập nhật để hỗ trợ rendering lập thể. Việc sử dụng các hiệu ứng này sẽ gây ra tác động không mong muốn.


Thiết lập scene XR
------------------

Mọi ứng dụng XR cần ít nhất một node :ref:`XROrigin3D <class_xrorigin3d>` và một node :ref:`XRCamera3D <class_xrcamera3d>`. Hầu hết ứng dụng sẽ có hai :ref:`XRController3D <class_xrcontroller3d>`, một cho tay trái và một cho tay phải. Hãy nhớ rằng các node camera và controller phải là con của node origin. Thêm các node này vào một scene mới và đổi tên các node controller thành ``LeftHand`` và ``RightHand``; scene của bạn sẽ trông tương tự như sau:

.. image:: img/xr_basic_scene.webp

Các biểu tượng cảnh báo là điều bình thường và sẽ biến mất sau khi bạn cấu hình các controller. Chọn tay trái và thiết lập như sau:

.. image:: img/xr_left_hand.webp

Và tay phải:

.. image:: img/xr_right_hand.webp

Hiện tại, tất cả các node này đều nằm trên sàn; chúng sẽ được định vị chính xác khi runtime chạy. Để hỗ trợ quá trình phát triển, bạn có thể di chuyển camera lên trên để ``y`` của nó được đặt thành ``1.7``, đồng thời di chuyển các node controller đến ``-0.5, 1.0, -0.5`` và ``0.5, 1.0, -0.5`` lần lượt cho tay trái và tay phải.

Tiếp theo, chúng ta cần thêm một script vào node gốc. Thêm đoạn code sau vào script này:

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node3D

    var xr_interface: XRInterface

    func _ready():
        xr_interface = XRServer.find_interface("OpenXR")
        if xr_interface and xr_interface.is_initialized():
            print("OpenXR initialized successfully")

            # Thay đổi viewport chính để xuất hình ảnh đến HMD.
            get_viewport().use_xr = true
        else:
            print("OpenXR not initialized, please check if your headset is connected")

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private XRInterface _xrInterface;

        public override void _Ready()
        {
            _xrInterface = XRServer.FindInterface("OpenXR");
            if(_xrInterface != null && _xrInterface.IsInitialized())
            {
                GD.Print("OpenXR initialized successfully");

                // Thay đổi viewport chính để xuất hình ảnh đến HMD.
                GetViewport().UseXR = true;
            }
            else
            {
                GD.Print("OpenXR not initialized, please check if your headset is connected");
            }
        }
    }


.. note::

    Không có giới hạn nào về nơi thực thi đoạn code này. Thông thường, bạn sẽ thêm script này vào node :ref:`XROrigin3D <class_xrorigin3d>` hoặc dưới dạng một node con :ref:`Node3D <class_node3d>` của node gốc.

    Giao diện OpenXR đặc biệt ở chỗ chúng ta phải khởi động nó trước khi project được tải, vì vậy ``is_initialized`` được kiểm tra tại đây. Hầu hết giao diện đều yêu cầu gọi hàm ``initialize`` của chúng thay thế.

    Nếu muốn hỗ trợ nhiều giao diện XR, chẳng hạn phát hành một game vừa nhắm đến phần cứng OpenXR vừa triển khai qua WebXR, bạn có thể kiểm tra lần lượt từng giao diện cho đến khi tìm thấy một giao diện hoạt động.


.. warning::

    Vì OpenXR xuất kết quả rendering đến HMD, vốn thường chạy ở framerate cao hơn màn hình, các thiết lập V-Sync của Godot sẽ bị bỏ qua và V-sync luôn bị tắt.

    Thay vào đó, OpenXR tự thực hiện việc định thời khung hình để đảm bảo framerate nhất quán.

    Cũng lưu ý rằng theo mặc định, physics engine cũng chạy ở 60Hz và điều này có thể khiến physics bị giật. Bạn nên đặt ``Engine.physics_ticks_per_second`` thành một giá trị cao hơn.


Nếu chạy project vào lúc này, mọi thứ sẽ hoạt động nhưng bạn sẽ ở trong một thế giới tối. Vì vậy, để hoàn thiện phần khởi đầu, hãy thêm một node :ref:`DirectionalLight3D <class_directionallight3d>` và một node :ref:`WorldEnvironment <class_worldenvironment>` vào scene. Bạn cũng có thể thêm một mesh instance làm node con cho mỗi node controller để tạm thời hiển thị chúng. Hãy đảm bảo bạn cấu hình một sky trong world environment.

Bây giờ hãy chạy project; bạn sẽ lơ lửng đâu đó trong không gian và có thể nhìn xung quanh.

.. note::

    Mặc dù chắc chắn có thể sử dụng cách chuyển level truyền thống với các ứng dụng XR, trong đó thiết lập scene này được lặp lại ở mỗi level, hầu hết mọi người thấy việc thiết lập một lần rồi tải các level dưới dạng subscene dễ hơn. Nếu bạn chuyển scene và sao chép thiết lập XR trong mỗi scene, hãy đảm bảo không chạy ``initialize`` nhiều lần. Hiệu ứng có thể không dự đoán được tùy thuộc vào giao diện XR được sử dụng.

    Trong phần còn lại của loạt tutorial cơ bản này, chúng ta sẽ tạo một game sử dụng một scene duy nhất.
