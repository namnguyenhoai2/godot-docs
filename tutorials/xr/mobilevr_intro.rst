.. _doc_mobilevr_intro:

VR trên thiết bị di động
========================

Godot có một triển khai VR trên thiết bị di động, предназначено для использования с телефонами, đặt bên trong một giá đỡ VR. Triển khai này được thực hiện thông qua :ref:`MobileVRInterface <class_mobilevrinterface>`. Đây là một triển khai tối giản, xuất hình ảnh lập thể side-by-side. Triển khai này hỗ trợ tracking 3DOF cơ bản trên các điện thoại cung cấp dữ liệu từ con quay hồi chuyển và gia tốc kế.

.. warning::

    Triển khai này hiện không được tích cực bảo trì. Vì cho phép những người bảo trì và reviewer kiểm thử việc render lập thể mà không cần phần cứng XR đắt tiền, interface XR này chủ yếu được sử dụng cho mục đích chẩn đoán.


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

Interface VR trên thiết bị di động có nhiều thiết lập kiểm soát đầu ra được cung cấp cho màn hình. Hai thiết lập quan trọng nhất là các hằng số ``k1`` và ``k2``, ảnh hưởng đến mức độ barrel distortion được áp dụng để bù cho lens distortion của giá đỡ điện thoại VR đang sử dụng. Nhiều giá đỡ có mã QR mà bạn có thể quét để cung cấp thông tin này.

Cũng cần cung cấp đúng kích thước của thiết bị và màn hình điện thoại; các thông số này được lưu trữ theo đơn vị centimet.
