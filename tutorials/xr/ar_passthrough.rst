.. _doc_openxr_passthrough:

AR / Passthrough
================

Thực tế tăng cường được hỗ trợ thông qua nhiều phương thức khác nhau, tùy thuộc vào khả năng của phần cứng.

Các headset như Magic Leap và kính như TiltFive hiển thị kết quả được render trên `see-through displays <https://en.wikipedia.org/wiki/See-through_display>`__, cho phép người dùng nhìn thấy thế giới thực.

Các headset như Quest, HTC Elite và Lynx R1 triển khai tính năng này thông qua một kỹ thuật gọi là video passthrough, trong đó camera ghi lại thế giới thực và những hình ảnh này được dùng làm nền, bên trên đó kết quả render của chúng ta được hiển thị.

.. note::

    Passthrough được triển khai rất khác nhau giữa các nền tảng.

    Trong Godot 4.3, chúng tôi đã triển khai một phương pháp thống nhất được giải thích trên trang trợ giúp này, vì vậy bạn không cần lo lắng về những khác biệt đó; việc triển khai :ref:`XRInterface <class_xrinterface>` hiện chịu trách nhiệm áp dụng phương thức phụ thuộc vào nền tảng phù hợp [#]_.

    Đối với các headset như Meta Quest và HTC Elite, bạn sẽ cần sử dụng `OpenXR vendors plugin v3.0.0 <https://github.com/GodotVR/godot_openxr_vendors/releases>`__ hoặc phiên bản mới hơn để bật video passthrough.

    Để tương thích ngược, API cũ cho passthrough vẫn khả dụng, nhưng bạn nên làm theo hướng dẫn mới bên dưới.

Chế độ hòa trộn môi trường
--------------------------

Cách chúng ta cấu hình chức năng VR hoặc AR là thiết lập chế độ hòa trộn môi trường. Chế độ này xác định cách môi trường (thế giới thực) được hòa trộn với thế giới ảo.

.. list-table:: Blend modes
  :widths: 35 65
  :header-rows: 1

  * - Chế độ hòa trộn
    - Mô tả
  * - XR_ENV_BLEND_MODE_OPAQUE
    - Hình ảnh được render là không trong suốt, chúng ta không nhìn thấy thế giới thực. Chúng ta đang ở chế độ VR.
      Tùy chọn này sẽ tắt passthrough nếu sử dụng video-passthrough.
  * - XR_ENV_BLEND_MODE_ADDITIVE
    - Hình ảnh được render được cộng vào thế giới thực và sẽ trông bán trong suốt.
      Chế độ này thường được sử dụng với các thiết bị see-through không thể che khuất
      thế giới thực.
      Tùy chọn này sẽ bật passthrough nếu sử dụng video-passthrough.
  * - XR_ENV_BLEND_MODE_ALPHA_BLEND
    - Hình ảnh được render được alpha blend với thế giới thực.
      Trên các thiết bị see-through hỗ trợ tính năng này, alpha sẽ điều khiển độ trong mờ
      của hệ thống quang học.
      Trên các thiết bị video-passthrough, alpha blending được áp dụng với hình ảnh video.
      passthrough cũng sẽ được bật nếu phù hợp.

Bạn có thể thiết lập chế độ hòa trộn môi trường cho ứng dụng của mình thông qua thuộc tính ``environment_blend_mode`` của instance :ref:`XRInterface <class_xrinterface>`.

Bạn có thể truy vấn các chế độ hòa trộn được phần cứng hỗ trợ bằng thuộc tính ``get_supported_environment_blend_modes`` trên cùng instance đó.

Cấu hình nền
------------

Khi đặt chế độ hòa trộn thành ``XR_ENV_BLEND_MODE_ALPHA_BLEND``, bạn phải đặt thuộc tính ``transparent_bg`` trên :ref:`Viewport <class_viewport>` thành true. Khi sử dụng chế độ hòa trộn ``XR_ENV_BLEND_MODE_ADDITIVE``, bạn nên đặt màu nền thành màu đen.

Cả hai giải pháp đều khiến việc render nền không đóng góp vào ánh sáng. Vì vậy, bạn cũng nên điều chỉnh các thiết lập môi trường cho phù hợp và bảo đảm có đủ ánh sáng môi trường để chiếu sáng cảnh của mình.

.. note::

    Một số AR SDK cung cấp thông tin về ánh sáng môi trường, thậm chí còn cung cấp một bản đồ bức xạ đầy đủ để cho phép phản chiếu thế giới thực trên các vật thể ảo. Tuy nhiên, chức năng Godot XR cốt lõi hiện chưa hỗ trợ điều này; chức năng này có thể được cung cấp thông qua các plugin.

Cụ thể cho OpenXR
-----------------

Trong OpenXR, bạn có thể cấu hình chế độ hòa trộn mặc định mà mình muốn sử dụng. Godot sẽ chọn chế độ hòa trộn này khi khởi động nếu chế độ đó khả dụng. Nếu không khả dụng, Godot sẽ mặc định sử dụng chế độ hòa trộn đầu tiên được XR runtime hỗ trợ cung cấp.

.. image:: img/openxr_default_blend_mode.webp

Đối với các thiết bị passthrough, OpenXR yêu cầu cấu hình thêm một số thiết lập. Những thiết lập này phụ thuộc vào nền tảng và được cung cấp thông qua plugin của các nhà cung cấp OpenXR.

Ví dụ, đây là các thiết lập cần thiết trên Meta Quest:

.. image:: img/openxr_export_passthrough.webp

Thiết lập ``Passthrough`` xác định liệu passthrough có được hỗ trợ hoặc thậm chí có bắt buộc hay không.

``Boundary Mode`` cho phép bạn xác định liệu guardian có cần thiết hay không; để tắt hoàn toàn guardian, passthrough phải luôn được bật.

Kết hợp các phần
----------------

Kết hợp những nội dung trên, chúng ta có thể sử dụng đoạn code sau làm cơ sở:

.. code-block:: gdscript

    @onready var viewport : Viewport = get_viewport()
    @onready var environment : Environment = $WorldEnvironment.environment

    func switch_to_ar() -> bool:
        var xr_interface: XRInterface = XRServer.primary_interface
        if xr_interface:
            var modes = xr_interface.get_supported_environment_blend_modes()
            if XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND in modes:
                xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_ALPHA_BLEND
                viewport.transparent_bg = true
            elif XRInterface.XR_ENV_BLEND_MODE_ADDITIVE in modes:
                xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_ADDITIVE
                viewport.transparent_bg = false
        else:
            return false

        environment.background_mode = Environment.BG_COLOR
        environment.background_color = Color(0.0, 0.0, 0.0, 0.0)
        environment.ambient_light_source = Environment.AMBIENT_SOURCE_COLOR
        return true

    func switch_to_vr() -> bool:
        var xr_interface: XRInterface = XRServer.primary_interface
        if xr_interface:
            var modes = xr_interface.get_supported_environment_blend_modes()
            if XRInterface.XR_ENV_BLEND_MODE_OPAQUE in modes:
                xr_interface.environment_blend_mode = XRInterface.XR_ENV_BLEND_MODE_OPAQUE
            else:
                return false

        viewport.transparent_bg = false
        environment.background_mode = Environment.BG_SKY
        environment.ambient_light_source = Environment.AMBIENT_SOURCE_BG
        return true

Chuyển bóng đổ thành độ trong suốt
----------------------------------

Chuyển bóng đổ thành độ trong suốt là một render mode dành cho Godot spatial shader, được giới thiệu trong Godot 3 nhằm phục vụ AR. Đây là một render mode đặc biệt, trong đó bề mặt càng ở trong bóng tối thì càng trở nên không trong suốt. Khi một bề mặt được chiếu sáng hoàn toàn, bề mặt đó trở nên hoàn toàn trong suốt và do đó hiển thị thế giới thực.

Tuy nhiên, bề mặt này thực tế được render trong trạng thái opaque. Điều này dẫn đến hai hệ quả:

* Vì cả depth buffer và color buffer đều được ghi, chúng ta che khuất mọi hình học phía sau bề mặt ngay cả khi bề mặt hoàn toàn trong suốt. * Vì chúng ta làm cho bề mặt trở nên opaque khi ở trong bóng tối, các vật thể ảo có thể đổ bóng lên các vật thể trong thế giới thực [#]_.

.. figure:: img/xr_passthrough_example.webp
    :alt: Image showing shadow to opacity being used to show the user's desk.

    Image showing shadow to opacity being used to show the user's desk.

Điều này cho phép thực hiện các trường hợp sử dụng sau:

* Bạn có thể render một box mesh bao quanh một chiếc bàn trong thế giới thực; điều này bảo đảm chiếc bàn vẫn hiển thị ngay cả khi một vật thể ảo được đặt bên dưới nó. Vật thể ảo sẽ được che khuất chính xác. Việc đặt một vật thể ảo lên trên chiếc bàn trong thế giới thực sẽ khiến bóng đổ lên mặt bàn. * Bạn có thể sử dụng shader với render mode này khi render hand mesh bằng chức năng hand tracking, đồng thời bảo đảm bàn tay của bạn che khuất đúng cách các vật thể ảo.

Đoạn shader code sau là cơ sở phù hợp cho chức năng này:

.. code-block:: glsl

    shader_type spatial;
    render_mode blend_mix, depth_draw_opaque, cull_back, shadow_to_opacity;

    void fragment() {
        ALBEDO = vec3(0.0, 0.0, 0.0);
    }

.. [#] Có thể áp dụng các hạn chế tùy thuộc vào việc triển khai XR interface.
.. [#] Tính năng này vẫn đang được hoàn thiện.
