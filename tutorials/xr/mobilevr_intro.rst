.. _doc_mobilevr_intro:

VR di động
==========

Godot có một triển khai VR di động dành cho việc sử dụng với điện thoại được đặt bên trong giá đỡ VR. Tính năng này được triển khai thông qua :ref:`MobileVRInterface <class_mobilevrinterface>`. Đây là một triển khai tối giản, xuất ra hình ảnh lập thể song song. Tính năng này hỗ trợ tracking 3DOF cơ bản trên các điện thoại cung cấp dữ liệu từ con quay hồi chuyển và gia tốc kế.

.. warning::

    Triển khai này hiện không được duy trì tích cực. Vì cho phép các maintainer và reviewer kiểm thử việc render lập thể mà không cần phần cứng XR đắt tiền, interface XR này chủ yếu được sử dụng cho mục đích chẩn đoán.


.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node3D

    var xr_interface: XRInterface

    func _ready() -> void:
        xr_interface = XRServer.find_interface("Native mobile")
        if xr_interface and xr_interface.initialize():
            print("Mobile VR initialized successfully")

            # Thay đổi viewport chính để xuất ra HMD.
            get_viewport().use_xr = true
        else:
            print("Mobile VR not initialized, please check if your headset is connected")

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private XRInterface _xrInterface;

        public override void _Ready()
        {
            _xrInterface = XRServer.FindInterface("Native mobile");
            if(_xrInterface != null && _xrInterface.Initialize())
            {
                GD.Print("Mobile VR initialized successfully");

                // Thay đổi viewport chính để xuất ra HMD.
                GetViewport().UseXR = true;
            }
            else
            {
                GD.Print("Mobile VR not initialized, please check if your headset is connected");
            }
        }
    }

Interface VR di động có nhiều thiết lập khác nhau để điều khiển đầu ra hiển thị trên màn hình. Hai thiết lập quan trọng nhất là các hằng số ``k1`` và ``k2``, ảnh hưởng đến mức độ biến dạng barrel được áp dụng để bù cho biến dạng của thấu kính trong giá đỡ điện thoại VR được sử dụng. Nhiều thiết bị có mã QR mà bạn có thể quét để cung cấp thông tin này.

Điều quan trọng không kém là cung cấp chính xác kích thước của thiết bị và màn hình điện thoại; các thông số này được lưu trữ theo đơn vị centimet.
