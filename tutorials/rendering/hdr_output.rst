.. _doc_hdr_output:

Đầu ra HDR
==========

Đầu ra HDR là một tính năng cho phép hiển thị hình ảnh High Dynamic Range (HDR) trên các màn hình hỗ trợ HDR. **Đầu ra HDR** không nên bị nhầm lẫn với quá trình render HDR nội bộ được Godot sử dụng cho cả chế độ đầu ra Standard Dynamic Range (SDR) và HDR.

Đầu ra HDR được hỗ trợ trên iOS, Linux (Wayland), macOS, visionOS và Windows. Tính năng này không được hỗ trợ trên Android, Linux (X11) hoặc web.

.. note::

    Cả Windows 10 và 11 đều hỗ trợ đầu ra HDR, nhưng chỉ Windows 11 cung cấp một ứng dụng có thể dùng để cấu hình độ sáng tối đa của màn hình được Godot editor sử dụng.

    Trên Linux, các phiên bản GNOME trước 50 có một lỗi khiến đầu ra HDR không hoạt động trên Wayland. Nếu bạn đang sử dụng phiên bản GNOME cũ hơn, bạn sẽ cần nâng cấp lên phiên bản 50 hoặc mới hơn để sử dụng đầu ra HDR trên Wayland.

Bật đầu ra HDR trong project của bạn
------------------------------------

Bạn có thể bật đầu ra HDR trong bất kỳ project mới hoặc hiện có nào bằng các bước sau:

1. Đảm bảo *không* :ref:`Environment<class_environment>` tài nguyên nào sử dụng các tính năng chỉ dành cho SDR:

- Tonemap Mode: Filmic hoặc ACES
- Glow Blend Mode: Soft Light
- Adjustments: Color Correction

2. Cấu hình thiết lập project :ref:`Renderer<class_ProjectSettings_property_rendering/renderer/rendering_method>` thành ``mobile`` hoặc ``forward_plus``.
3. Cấu hình thiết lập project nâng cao :ref:`Rendering Device Driver <class_ProjectSettings_property_rendering/rendering_device/driver>` thành ``metal`` cho iOS và ``d3d12`` cho Windows.
4. Cấu hình thiết lập project nâng cao :ref:`Display Server Driver.linuxbsd <class_ProjectSettings_property_display/display_server/driver.linuxbsd>` thành ``wayland`` và bật thiết lập editor :ref:`Prefer Wayland <class_EditorSettings_property_run/platforms/linuxbsd/prefer_wayland>`.
5. Bật thiết lập project :ref:`HDR 2D <class_ProjectSettings_property_rendering/viewport/hdr_2d>` và bật :ref:`use_hdr_2d<class_Viewport_property_use_hdr_2d>` cho tất cả
   :ref:`SubViewports <class_SubViewport>` và :ref:`Windows <class_Window>` cần hỗ trợ đầu ra HDR.
6. Bật thiết lập project :ref:`Request HDR Output <class_ProjectSettings_property_display/window/hdr/request_hdr_output>` và bật :ref:`hdr_output_requested<class_Window_property_hdr_output_requested>` cho tất cả :ref:`Windows <class_Window>` khác cần hỗ trợ đầu ra HDR.
7. *[Tùy chọn]* Cung cấp các thiết lập HDR trong game bằng cách sao chép ví dụ từ `HDR output demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ vào project của bạn.

.. note::

   Một số thiết lập này có thể đã được cấu hình chính xác cho đầu ra HDR trong project của bạn. Ví dụ: Windows Rendering Device Driver được đặt thành ``d3d12`` trong các project được tạo bằng Godot 4.6 trở lên, nhưng sẽ cần được thay đổi nếu project được tạo bằng phiên bản Godot cũ hơn.

Sử dụng đầu ra HDR trong Godot
------------------------------

Hãy thử `HDR output demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ như bước đầu tiên để sử dụng đầu ra HDR trong Godot. Demo này chứa các ví dụ về những khái niệm được mô tả trên trang này và sẽ giúp bạn đảm bảo rằng môi trường phát triển của mình được cấu hình chính xác cho đầu ra HDR.

Đầu ra HDR trong Godot editor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Godot editor sẽ sử dụng đầu ra HDR cho cửa sổ chính khi thiết lập project :ref:`Request HDR Output <class_ProjectSettings_property_display/window/hdr/request_hdr_output>` đã được bật. Bạn có thể biết game của mình đang chạy ở chế độ đầu ra SDR hay HDR dựa trên dòng chữ ở bên phải thanh công cụ game view: Game của bạn đang chạy ở chế độ HDR khi dòng chữ "HDR" xuất hiện bên cạnh kích thước cửa sổ.

.. image:: img/rendering_hdr_output_game_view.webp

Con số trong ngoặc đơn bên cạnh dòng chữ "HDR" là :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` hiện tại, được mô tả trong các phần sau. Bạn có thể bật hoặc tắt
:ref:`Window.hdr_output_requested<class_Window_property_hdr_output_requested>` trong menu tùy chọn cửa sổ game:

.. image:: img/rendering_hdr_output_game_window_options.webp

Kiến thức cơ bản về đầu ra HDR
------------------------------

Godot sử dụng mô hình `Extended Dynamic Range (EDR) <https://developer.apple.com/videos/play/wwdc2021/10161/>`__ cho đầu ra HDR. Trong khi đầu ra SDR cho phép hiển thị các giá trị thành phần màu từ ``0.0`` đến ``1.0``, đầu ra HDR cho phép hiển thị các giá trị lớn hơn ``1.0``. Giá trị tối đa có thể hiển thị được cung cấp bởi
:ref:`Window.get_output_max_linear_value()<class_Window_method_get_output_max_linear_value>` và phương thức này hợp lệ khi sử dụng SDR hoặc HDR.

.. image:: img/rendering_hdr_output_fundamentals.webp

.. note::

   Các biểu đồ này được trình bày dưới dạng hình ảnh SDR không chứa bất kỳ màu HDR nào. Để bù đắp cho hạn chế này, các thanh thang độ xám dọc theo mỗi trục được áp dụng hiệu ứng phát sáng nhằm biểu thị các giá trị nằm ngoài phạm vi SDR. "Giá trị tối đa của đầu ra" trong biểu đồ này biểu thị giá trị thành phần màu tuyến tính tối đa được trả về bởi
   :ref:`Window.get_output_max_linear_value()<class_Window_method_get_output_max_linear_value>`.

Thiết kế cho đầu ra HDR
-----------------------

Có hai phương pháp chính để tận dụng tối đa đầu ra HDR: sử dụng
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` và sử dụng tonemapping.

Mặc dù cả hai phương pháp có thể được sử dụng trong cùng một project, tonemapping nên được dùng để tạo đầu ra HDR từ một :ref:`Viewport<class_Viewport>` sử dụng ánh sáng vượt quá khả năng của màn hình SDR, ánh sáng gián tiếp, global illumination, vật liệu phát sáng, hiệu ứng hậu kỳ hoặc bất kỳ kỹ thuật nào khác tận dụng các giá trị màu trong cảnh.

:ref:`Giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` chỉ nên được sử dụng để hiển thị màu trực tiếp lên màn hình mà không sử dụng tonemapping và không ảnh hưởng đến ánh sáng, hiệu ứng hậu kỳ hoặc màu xung quanh. Điều này khiến
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` rất phù hợp cho
:ref:`CanvasItems<class_CanvasItem>` hoặc các vật liệu không đổ bóng trong một cảnh không có ánh sáng hoặc có ánh sáng cơ bản nhưng không vượt quá khả năng của màn hình SDR.

Thuộc tính :ref:`Viewport.own_world_3d<class_Viewport_property_own_world_3d>` có thể được sử dụng để phân tách các :ref:`Viewports<class_Viewport>` chịu ảnh hưởng của tonemapping và các
:ref:`class_WorldEnvironment` hiệu ứng khác.

Sử dụng giá trị tuyến tính tối đa của đầu ra
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Trong một game truyền thống chỉ sử dụng SDR, khả năng hiển thị màu sáng nhất bị giới hạn bởi việc một trong các thành phần đỏ, xanh lá hoặc xanh dương của màu đạt tối đa ``1.0``. Khi sử dụng màn hình HDR hiện đại, giới hạn này không còn áp dụng và các thành phần màu lớn hơn ``1.0`` có thể được hiển thị chính xác. Godot cung cấp giá trị thành phần màu tối đa mà màn hình có thể hiển thị thông qua :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`. Giá trị này có thể được sử dụng trong cả SDR và HDR, nhờ đó bạn có thể dễ dàng xây dựng game cho cả hai chế độ đầu ra mà không cần thay đổi hành vi dựa trên việc đầu ra HDR có được bật hay không.

:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` có thể thay đổi thường xuyên khi người chơi điều chỉnh độ sáng thiết bị, bật hoặc tắt đầu ra HDR trên thiết bị, hoặc di chuyển cửa sổ trò chơi giữa các màn hình, vì vậy điều quan trọng là phải lấy giá trị này ở mỗi frame hoặc sử dụng tín hiệu :ref:`giá trị tuyến tính tối đa của đầu ra đã thay đổi <class_Window_signal_output_max_linear_value_changed>`. Giá trị này luôn bằng ``1.0`` ở chế độ SDR và cũng có thể bằng ``1.0`` khi đầu ra HDR được bật và người chơi đã điều chỉnh màn hình đến độ sáng tối đa.

Tốt nhất nên sử dụng :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` này với các "điểm sáng" và hiệu ứng đặc biệt có thời lượng ngắn hoặc chỉ chiếm một phần nhỏ màn hình; nếu phần lớn màn hình được hiển thị ở độ sáng tối đa này trong thời gian dài hơn một khoảng ngắn, trò chơi sẽ trông sáng đến mức khó chịu, như thể trò chơi đang bỏ qua cài đặt độ sáng của thiết bị. Bạn cũng có thể thấy một số hiệu ứng trông đẹp nhất khi bị giới hạn ở một giá trị tuyến tính tối đa lớn hơn ``1.0``, nhưng nhỏ hơn :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`. Bạn có thể đọc thêm về việc đôi khi nên giới hạn giá trị HDR tối đa trong bài đăng `HDR và Giao diện người dùng <https://android-developers.googleblog.com/2025/09/hdr-and-user-interfaces.html>`__ trên Android Developers Blog.

Có thể dùng một script để biến đổi màu thành màu sáng nhất mà màn hình có thể hiển thị. Khi làm việc với :ref:`class_CanvasItem`, việc áp dụng màu đã chỉnh sửa thu được cho :ref:`modulate<class_canvasitem_property_modulate>` có thể thuận tiện, hoặc
:ref:`self_modulate<class_canvasitem_property_self_modulate>` thuộc tính với màu cơ sở của
:ref:`class_CanvasItem` được đặt thành :ref:`white<class_color_constant_white>`. Script sau đây minh họa cách thực hiện:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CanvasItem

    # Đặt giá trị này thành màu mong muốn khi màu cơ sở của CanvasItem là màu trắng.
    @export var sdr_self_modulate: Color = Color.WHITE

    # Đặt giá trị này thành -1.0 để tắt giới hạn giá trị màu tối đa.
    @export_range(0, 20, 0.1, "or_less", "or_greater") var max_linear_value_limit: float = -1.0


    func _enter_tree() -> void:
        var window: Window = get_window()
        window.output_max_linear_value_changed.connect(_on_output_max_linear_value_changed)
        _on_output_max_linear_value_changed(window.get_output_max_linear_value())


    func _exit_tree() -> void:
        get_window().output_max_linear_value_changed.disconnect(_on_output_max_linear_value_changed)


    func _on_output_max_linear_value_changed(output_max_linear_value: float) -> void:
        # Điều chỉnh độ sáng của màu để đạt mức sáng nhất có thể, bất kể
        # đầu ra SDR hay HDR, nhưng không sáng hơn max_linear_value_limit.
        if max_linear_value_limit >= 0.0:
            output_max_linear_value = minf(output_max_linear_value, max_linear_value_limit)
        self_modulate = normalize_color(sdr_self_modulate, output_max_linear_value)


    func normalize_color(srgb_color, output_max_linear_value = 1.0):
        # Màu phải được mã hóa tuyến tính để sử dụng các phép toán.
        var linear_color = srgb_color.srgb_to_linear()
        var max_rgb_value = maxf(linear_color.r, maxf(linear_color.g, linear_color.b))
        var brightness_scale = output_max_linear_value / max_rgb_value
        linear_color *= brightness_scale
        # Hoàn tác các thay đổi đối với kênh alpha, vốn không được sửa đổi.
        linear_color.a = srgb_color.a
        # Chuyển đổi lại sang mã hóa sRGB phi tuyến, vốn được yêu cầu đối với Color trong
        # Godot trừ khi có quy định khác.
        return linear_color.linear_to_srgb()

Dự án `demo đầu ra HDR <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ có các phiên bản nâng cao hơn của script này cùng các ví dụ về cách sử dụng phương pháp này trong dự án của bạn.

Sử dụng Tonemapping
^^^^^^^^^^^^^^^^^^^

Để tạo đầu ra HDR mà không sử dụng :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`, các scene của bạn sẽ cần những giá trị màu vượt quá khả năng hiển thị của màn hình SDR, vì vậy điều quan trọng là sử dụng một tonemapper như
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` hoặc
:ref:`AgX<class_Environment_constant_tone_mapper_agx>` để xử lý việc hiển thị các giá trị sáng này của scene trên cả màn hình SDR và HDR.

**Tonemapping và HDR**

Vai trò chính của tonemapper là giảm dải động của một scene tự nhiên có dải động độ sáng rất cao xuống một dải động nhỏ hơn có thể hiển thị trên màn hình. Tonemapper trong Godot sử dụng :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` để xác định dải đầu ra mà màn hình có khả năng hiển thị. Ví dụ, với tonemapper
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` trong Godot, các giá trị tuyến tính của scene trong phạm vi từ ``0.0`` đến :ref:`trắng của tonemap <class_Environment_property_tonemap_white>` được ánh xạ vào một dải đầu ra từ ``0.0`` đến
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`.

.. image:: img/rendering_hdr_output_sdr_tonemap.webp

Với phương pháp này, bạn có thể điều chỉnh :ref:`trắng của tonemap <class_Environment_property_tonemap_white>` để đảm bảo rằng mọi giá trị tuyến tính của scene nhỏ hơn :ref:`trắng của tonemap <class_Environment_property_tonemap_white>` sẽ được hiển thị mà không bị cắt ngưỡng. Điều này đảm bảo các chi tiết không bị mất khi hiển thị hình ảnh trên màn hình có dải động thấp hơn scene gốc.

.. image:: img/rendering_hdr_output_tonemap_white.jpg

Trong SDR, hành vi này hoàn toàn ổn định vì :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` được cố định ở ``1.0``, nhưng trong HDR, hành vi này thay đổi tùy theo khả năng của màn hình:

.. image:: img/rendering_hdr_output_hdr_tonemap.webp

Như được thể hiện trong các biểu đồ ở trên,
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` tonemapper sẽ hoạt động giống như :ref:`Linear<class_Environment_constant_tone_mapper_linear>` tonemapper khi
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` bằng hoặc cao hơn
:ref:`trắng của tonemap <class_Environment_property_tonemap_white>`. Điều này cho phép tái tạo màu chính xác trên các màn hình HDR có khả năng tái tạo những giá trị sáng hơn ban đầu của scene. Khi :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` tăng lên cao hơn :ref:`trắng của tonemap <class_Environment_property_tonemap_white>`, trắng của tonemap sẽ được điều chỉnh để khớp với giá trị tuyến tính tối đa của đầu ra này.

Tonemapper :ref:`AgX<class_Environment_constant_tone_mapper_agx>` hoạt động tương tự như
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` theo cách này, nhưng
:ref:`trắng của tonemap <class_Environment_property_tonemap_agx_white>` luôn được nhân với
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`. Tonemapper
:ref:`Linear<class_Environment_constant_tone_mapper_linear>` không áp dụng tonemapping; :ref:`trắng của tonemap <class_Environment_property_tonemap_white>` của nó bằng
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` trong mọi trường hợp. Các
:ref:`Filmic<class_Environment_constant_tone_mapper_filmic>` và
:ref:`ACES<class_Environment_constant_tone_mapper_aces>` tonemapper bỏ qua hoàn toàn
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` và luôn tạo ra hình ảnh trong phạm vi SDR.

Tại sao không kết hợp giá trị tuyến tính tối đa của đầu ra với các kỹ thuật khác?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Tonemapping, chiếu sáng gián tiếp, global illumination và các hiệu ứng hậu kỳ đều phụ thuộc vào các giá trị màu ổn định của scene để tạo ra kết quả nhất quán và có thể dự đoán trong cả chế độ SDR và HDR. Nếu nhà phát triển sử dụng những kỹ thuật này với một scene có các giá trị màu thay đổi dựa trên :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`, kết quả sẽ không còn tương tự trên các màn hình có khả năng khác nhau.

Ví dụ, cường độ của hiệu ứng glow chịu ảnh hưởng trực tiếp bởi độ sáng của scene. Nếu độ sáng của scene thay đổi dựa trên
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>`, cường độ glow cũng sẽ thay đổi: một
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` sẽ tạo ra hiệu ứng phát sáng mạnh hơn, đây thường là hành vi không mong muốn.

Độ chói tuyệt đối
-----------------

Khi sử dụng đầu ra HDR, :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` được tính dựa trên độ chói trắng tham chiếu và độ chói tối đa của màn hình.

Độ chói trắng tham chiếu
^^^^^^^^^^^^^^^^^^^^^^^^

Độ chói trắng tham chiếu, hay gọi ngắn gọn là độ chói tham chiếu, biểu thị giá trị trắng SDR sáng nhất có thể. Khi người dùng thay đổi cài đặt độ sáng của thiết bị tạo tín hiệu video, chẳng hạn như máy tính để bàn, máy tính xách tay hoặc điện thoại thông minh, họ chỉ đơn giản là đang điều chỉnh độ chói tham chiếu. Trên điện thoại thông minh, thay đổi này có thể diễn ra tự động thông qua tính năng tự động điều chỉnh độ sáng màn hình của điện thoại, đồng thời cũng xảy ra khi người dùng tự điều chỉnh độ sáng màn hình. Trên máy tính để bàn hoặc máy tính xách tay, có nhiều cách khác nhau để điều chỉnh độ chói tham chiếu này tùy theo hệ điều hành.

Giá trị này thường nằm trong khoảng từ 100 đến 300 nit và luôn được biểu thị bằng một
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` chính xác là ``1.0``. Giá trị này cũng có thể được gọi là "trắng giấy" hoặc "mức trắng SDR".

.. note::

	When using an external screen on Windows, the *SDR content brightness* HDR display setting
	directly controls the reference luminance value and is the primary way to adjust the brightness
	of the Windows desktop and Godot. When using a built-in HDR screen on Windows, changing *HDR
	content brightness* also directly controls the reference luminance, but has no effect on the
	brightness of the Windows desktop or Godot because a separate brightness implementation negates
	any effect of changes to the reference luminance.

Độ chói tối đa
^^^^^^^^^^^^^^

Độ chói tối đa là một thuộc tính của màn hình HDR. Giá trị này có thể nằm trong khoảng từ 250 đến 2.000 nit hoặc cao hơn. Các màn hình ngoài thường báo cáo giá trị độ chói tối đa cao hơn khả năng vật lý của màn hình, dẫn đến việc màn hình áp dụng tonemapping có thể nhìn thấy. Một số hệ điều hành máy tính để bàn hoặc máy tính xách tay cung cấp cách hiệu chỉnh giá trị độ chói tối đa được sử dụng cho từng màn hình ngoài.

.. note::

	When using a built-in screen on Windows, the reported maximum luminance will change as the user
	adjusts their laptop screen brightness while the reported reference luminance remains constant.
	This behavior is opposite from using an external display on Windows and adjusting the *SDR content
	brightness* HDR display setting and also opposite of other platforms.

Giá trị tuyến tính tối đa của đầu ra trong thực tế
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Khi ở chế độ HDR, :ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` sẽ tăng khi người dùng giảm độ chói tham chiếu, vì có thêm khoảng dự trữ HDR. Tương tự, khi người dùng tăng độ chói tham chiếu, họ sẽ có ít khoảng dự trữ HDR hơn và
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` sẽ giảm. Trong một số trường hợp, khi sử dụng chế độ HDR với độ chói tham chiếu cao nhất,
:ref:`giá trị tuyến tính tối đa của đầu ra <class_Window_method_get_output_max_linear_value>` sẽ bằng ``1.0``, tương ứng với hành vi SDR, vì không còn khoảng dự trữ HDR.

Không phải màn hình nào cũng giống nhau
---------------------------------------

Các tiêu chuẩn SDR được thiết kế để phù hợp với khả năng của những màn hình hiện có được sử dụng phổ biến trên toàn thế giới. Các tiêu chuẩn HDR được xây dựng theo hướng ngược lại một cách có chủ đích: chúng được thiết kế để tận dụng khả năng của một màn hình lý tưởng hiện chưa được cung cấp rộng rãi.

Trên thực tế, điều này có nghĩa là các màn hình HDR phổ biến có thể tự thực hiện tonemapping, gamut mapping hoặc dynamic tonemapping (DTM) nội bộ để hỗ trợ nội dung mở rộng đến gamut và dải độ chói rộng hơn khả năng mà phần cứng vật lý có thể đạt được. Một số màn hình không thể hiển thị các giá trị màu rất sáng chiếm hơn một phần nhỏ (từ 1% đến 10%) của màn hình và sẽ tạm thời làm tối toàn bộ hình ảnh hoặc một phần hình ảnh khi điều này xảy ra. Những tính năng này có thể tạo ra màu sắc không đại diện cho các màn hình khác, vì vậy tốt nhất là tắt chúng nếu có thể khi phát triển game HDR. Bạn có thể tắt một phần hoặc toàn bộ các tính năng này bằng cách bật chế độ HGiG trên màn hình hoặc đặt chế độ của màn hình thành "clip" và/hoặc "stable". Một số màn hình HDR có thể hiển thị màu tối hoặc màu bão hòa khác với các màn hình khác; sự khác biệt về hình thức này thường là kết quả của công nghệ màn hình.
