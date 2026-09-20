.. _doc_hdr_output:

Đầu ra HDR
==========

Đầu ra HDR là một tính năng cho phép hiển thị hình ảnh High Dynamic Range (HDR) trên các màn hình hỗ trợ HDR. **Đầu ra** HDR không nên bị nhầm lẫn với quá trình kết xuất HDR nội bộ được Godot sử dụng cho cả chế độ đầu ra Standard Dynamic Range (SDR) và đầu ra HDR.

Đầu ra HDR được hỗ trợ trên iOS, Linux (Wayland), macOS, visionOS và Windows. Tính năng này không được hỗ trợ trên Android, Linux (X11) hoặc web.

.. note::

    Cả Windows 10 và 11 đều hỗ trợ đầu ra HDR, nhưng chỉ Windows 11 cung cấp một ứng dụng có thể được sử dụng để cấu hình độ chói tối đa của màn hình được Godot editor sử dụng.

    Trên Linux, các phiên bản GNOME trước 50 có một lỗi khiến đầu ra HDR không hoạt động trên Wayland. Nếu bạn đang sử dụng phiên bản GNOME cũ hơn, bạn sẽ cần nâng cấp lên phiên bản 50 trở lên để sử dụng đầu ra HDR trên Wayland.

Bật đầu ra HDR trong project của bạn
------------------------------------

Bạn có thể bật đầu ra HDR trong bất kỳ project mới hoặc hiện có nào bằng các bước sau:

1. Đảm bảo *không có* tài nguyên :ref:`Environment<class_environment>` nào sử dụng các tính năng chỉ dành cho SDR:

- Tonemap Mode: Filmic hoặc ACES - Glow Blend Mode: Soft Light - Adjustments: Color Correction

2. Cấu hình project setting :ref:`Renderer<class_ProjectSettings_property_rendering/renderer/rendering_method>` thành ``mobile`` hoặc ``forward_plus``. 3. Cấu hình advanced project setting :ref:`Rendering Device Driver<class_ProjectSettings_property_rendering/rendering_device/driver>` thành ``metal`` cho iOS và ``d3d12`` cho Windows. 4. Cấu hình advanced project setting :ref:`Display Server Driver.linuxbsd<class_ProjectSettings_property_display/display_server/driver.linuxbsd>` thành ``wayland`` và bật editor setting :ref:`Prefer Wayland<class_EditorSettings_property_run/platforms/linuxbsd/prefer_wayland>`. 5. Bật project setting :ref:`HDR 2D<class_ProjectSettings_property_rendering/viewport/hdr_2d>` và bật :ref:`use_hdr_2d<class_Viewport_property_use_hdr_2d>` cho tất cả
   :ref:`SubViewports <class_SubViewport>` and :ref:`Windows <class_Window>` that should support
   đầu ra HDR. 6. Bật project setting :ref:`Request HDR Output <class_ProjectSettings_property_display/window/hdr/request_hdr_output>` và bật :ref:`hdr_output_requested<class_Window_property_hdr_output_requested>` cho tất cả :ref:`Windows <class_Window>` khác cần hỗ trợ đầu ra HDR. 7. *[Tùy chọn]* Cung cấp các cài đặt HDR trong game bằng cách sao chép ví dụ từ `HDR output demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ vào project của bạn.

.. note::

   Một số cài đặt này có thể đã được cấu hình chính xác cho đầu ra HDR trong project của bạn. Ví dụ: Windows Rendering Device Driver được đặt thành ``d3d12`` trong các project được tạo bằng Godot 4.6 trở lên, nhưng sẽ cần được thay đổi nếu project được tạo bằng phiên bản Godot cũ hơn.

Sử dụng đầu ra HDR trong Godot
------------------------------

Hãy thử `HDR output demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ làm bước đầu tiên để sử dụng đầu ra HDR trong Godot. Demo này chứa các ví dụ về những khái niệm được mô tả trên trang này và sẽ giúp bạn đảm bảo môi trường phát triển của mình được cấu hình chính xác cho đầu ra HDR.

Đầu ra HDR trong Godot editor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Godot editor sẽ sử dụng đầu ra HDR cho cửa sổ chính khi project setting :ref:`Request HDR Output <class_ProjectSettings_property_display/window/hdr/request_hdr_output>` đã được bật. Bạn có thể biết game của mình đang chạy ở chế độ đầu ra SDR hay HDR dựa trên dòng chữ ở bên phải game view toolbar: Game của bạn đang chạy ở chế độ HDR khi dòng chữ "HDR" xuất hiện bên cạnh kích thước cửa sổ.

.. image:: img/rendering_hdr_output_game_view.webp

Số trong dấu ngoặc đơn bên cạnh dòng chữ "HDR" là :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` hiện tại, được mô tả trong các phần sau. Bạn có thể chuyển đổi menu tùy chọn cửa sổ của game:
:ref:`Window.hdr_output_requested<class_Window_property_hdr_output_requested>` property in the game
menu tùy chọn cửa sổ:

.. image:: img/rendering_hdr_output_game_window_options.webp

Kiến thức cơ bản về đầu ra HDR
------------------------------

Godot sử dụng mô hình `Extended Dynamic Range (EDR) <https://developer.apple.com/videos/play/wwdc2021/10161/>`__ cho đầu ra HDR. Trong khi đầu ra SDR cho phép hiển thị các giá trị thành phần màu trong khoảng từ ``0.0`` đến ``1.0``, đầu ra HDR cho phép các giá trị lớn hơn ``1.0``. Giá trị tối đa có thể hiển thị được cung cấp bởi
:ref:`Window.get_output_max_linear_value()<class_Window_method_get_output_max_linear_value>` and
phương thức này hợp lệ khi sử dụng SDR hoặc HDR.

.. image:: img/rendering_hdr_output_fundamentals.webp

.. note::

   Các biểu đồ này được trình bày dưới dạng hình ảnh SDR không chứa bất kỳ màu HDR nào. Để bù đắp cho hạn chế này, các thanh grayscale dọc theo mỗi trục được áp dụng hiệu ứng glow nhằm biểu thị các giá trị nằm ngoài phạm vi SDR. "output max value" trong biểu đồ này biểu thị giá trị thành phần màu tuyến tính tối đa được trả về bởi
   :ref:`Window.get_output_max_linear_value()<class_Window_method_get_output_max_linear_value>`.

Thiết kế cho đầu ra HDR
-----------------------

Có hai phương pháp chính để tận dụng tối đa đầu ra HDR: sử dụng
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` and using
tonemapping.

Mặc dù cả hai phương pháp đều có thể được sử dụng trong cùng một project, tonemapping nên được sử dụng để tạo đầu ra HDR từ :ref:`Viewport<class_Viewport>` sử dụng ánh sáng vượt quá khả năng của màn hình SDR, ánh sáng gián tiếp, global illumination, vật liệu phát sáng, hiệu ứng post-processing hoặc bất kỳ kỹ thuật nào khác tận dụng các giá trị màu trong scene.

:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` chỉ nên được sử dụng để hiển thị màu trực tiếp lên màn hình mà không cần tonemapping và không ảnh hưởng đến ánh sáng, hiệu ứng post-processing hoặc màu xung quanh. Điều này khiến
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` well suited for
:ref:`CanvasItems<class_CanvasItem>` or unshaded materials in a scene that has no lighting or basic
ánh sáng vốn không vượt quá khả năng của màn hình SDR.

Thuộc tính :ref:`Viewport.own_world_3d<class_Viewport_property_own_world_3d>` có thể được sử dụng để phân tách những :ref:`Viewports<class_Viewport>` nào chịu ảnh hưởng của tonemapping và các
:ref:`class_WorldEnvironment` effects.

Sử dụng giá trị tuyến tính tối đa của đầu ra
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Trong một game truyền thống chỉ dành cho SDR, độ sáng tối đa khi hiển thị một màu bị giới hạn bởi thành phần red, green hoặc blue của màu đó đạt tối đa ``1.0``. Khi sử dụng màn hình HDR hiện đại, giới hạn này không còn áp dụng và các thành phần màu lớn hơn ``1.0`` có thể được hiển thị chính xác. Godot cung cấp giá trị thành phần màu tối đa mà màn hình có thể hiển thị thông qua :ref:`output max linear value<class_Window_method_get_output_max_linear_value>`. Giá trị này có thể được sử dụng trong cả SDR và HDR, giúp dễ dàng xây dựng game cho cả hai chế độ đầu ra mà không cần thay đổi hành vi dựa trên việc đầu ra HDR có được bật hay không.

:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` có thể thay đổi thường xuyên khi người chơi điều chỉnh độ sáng thiết bị, bật hoặc tắt đầu ra HDR trên thiết bị hoặc di chuyển cửa sổ game giữa các màn hình, vì vậy điều quan trọng là phải lấy giá trị này ở mỗi frame hoặc sử dụng signal :ref:`output max linear value changed<class_Window_signal_output_max_linear_value_changed>`. Giá trị này sẽ luôn bằng ``1.0`` ở chế độ SDR và cũng có thể bằng ``1.0`` khi đầu ra HDR được bật và người chơi đã điều chỉnh màn hình đến độ sáng tối đa.

Tốt nhất nên sử dụng :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` này với các "highlights" và hiệu ứng đặc biệt có thời lượng ngắn hoặc chỉ chiếm một phần nhỏ màn hình; nếu phần lớn màn hình được hiển thị ở độ sáng tối đa này trong thời gian dài hơn một khoảng ngắn, game sẽ trông sáng đến mức khó chịu, như thể game đang bỏ qua cài đặt độ sáng của thiết bị. Bạn cũng có thể nhận thấy một số hiệu ứng trông đẹp nhất khi được giới hạn ở giá trị tuyến tính tối đa lớn hơn ``1.0`` nhưng nhỏ hơn :ref:`output max linear value<class_Window_method_get_output_max_linear_value>`. Bạn có thể đọc thêm về việc đôi khi nên giới hạn giá trị HDR tối đa trong bài đăng `HDR and User Interfaces <https://android-developers.googleblog.com/2025/09/hdr-and-user-interfaces.html>`__ của Android Developers Blog.

Có thể dùng script để biến đổi một màu thành màu sáng nhất mà màn hình có thể hiển thị. Khi làm việc với :ref:`class_CanvasItem`, việc áp dụng màu đã chỉnh sửa thu được cho :ref:`modulate<class_canvasitem_property_modulate>` hoặc có thể sẽ thuận tiện
:ref:`self_modulate<class_canvasitem_property_self_modulate>` property with the base color of the
:ref:`class_CanvasItem` set to :ref:`white<class_color_constant_white>`. The following script
minh họa điều này:

.. tabs::
 .. code-tab:: gdscript GDScript

	extends CanvasItem

	# Set this to your desired color when the CanvasItem's base color is white. @export var sdr_self_modulate: Color = Color.WHITE

	# Set this to -1.0 to disable limiting the maximum color value. @export_range(0, 20, 0.1, "or_less", "or_greater") var max_linear_value_limit: float = -1.0


	func _enter_tree() -> void: var window: Window = get_window() window.output_max_linear_value_changed.connect(_on_output_max_linear_value_changed) _on_output_max_linear_value_changed(window.get_output_max_linear_value())


	func _exit_tree() -> void: get_window().output_max_linear_value_changed.disconnect(_on_output_max_linear_value_changed)


	func _on_output_max_linear_value_changed(output_max_linear_value: float) -> void: # Adjust the brightness of color to be the brightest possible, regardless # of SDR or HDR output, but no brighter than max_linear_value_limit. if max_linear_value_limit >= 0.0: output_max_linear_value = minf(output_max_linear_value, max_linear_value_limit) self_modulate = normalize_color(sdr_self_modulate, output_max_linear_value)


	func normalize_color(srgb_color, output_max_linear_value = 1.0): # Color must be linear-encoded to use math operations. var linear_color = srgb_color.srgb_to_linear() var max_rgb_value = maxf(linear_color.r, maxf(linear_color.g, linear_color.b)) var brightness_scale = output_max_linear_value / max_rgb_value linear_color *= brightness_scale # Undo changes to the alpha channel, which should not be modified. linear_color.a = srgb_color.a # Convert back to nonlinear sRGB encoding, which is required for Color in # Godot unless stated otherwise. return linear_color.linear_to_srgb()

`HDR output demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/hdr_output>`__ bao gồm các phiên bản nâng cao hơn của script này và các ví dụ về cách sử dụng phương pháp này trong project của bạn.

Sử dụng Tonemapping
^^^^^^^^^^^^^^^^^^^

Để tạo đầu ra HDR mà không sử dụng :ref:`output max linear value<class_Window_method_get_output_max_linear_value>`, các scene của bạn sẽ cần các giá trị màu vượt quá khả năng hiển thị của màn hình SDR, vì vậy điều quan trọng là phải sử dụng một tonemapper như
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` or
:ref:`AgX<class_Environment_constant_tone_mapper_agx>` to handle display of these bright scene
các giá trị trên cả màn hình SDR và HDR.

**Tonemapping và HDR**

Vai trò chính của tonemapper là giảm dải động của một scene tự nhiên có dải độ sáng rất cao xuống một dải động nhỏ hơn có thể hiển thị trên màn hình. Tonemapper trong Godot sử dụng :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` để xác định phạm vi đầu ra mà màn hình có khả năng hiển thị. Ví dụ, với
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` tonemapper in Godot, linear
các giá trị scene trong khoảng từ ``0.0`` đến :ref:`tonemap white<class_Environment_property_tonemap_white>` được ánh xạ vào phạm vi đầu ra từ ``0.0`` đến
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>`.

.. image:: img/rendering_hdr_output_sdr_tonemap.webp

Với cách tiếp cận này, bạn có thể điều chỉnh :ref:`tonemap white<class_Environment_property_tonemap_white>` để bảo đảm rằng mọi giá trị cảnh tuyến tính dưới :ref:`tonemap white<class_Environment_property_tonemap_white>` đều được hiển thị mà không bị cắt. Điều này bảo đảm các chi tiết không bị mất khi trình bày hình ảnh trên màn hình có dải động thấp hơn cảnh gốc.

.. image:: img/rendering_hdr_output_tonemap_white.jpg

Mặc dù hành vi này hoàn toàn ổn định trong SDR, khi :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` được cố định ở ``1.0``, hành vi này sẽ thay đổi trong HDR tùy theo khả năng của màn hình:

.. image:: img/rendering_hdr_output_hdr_tonemap.webp

Như được minh họa trong các biểu đồ ở trên,
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` tonemapper will behave the same
với vai trò là tonemapper :ref:`Linear<class_Environment_constant_tone_mapper_linear>` khi
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` is equal to or higher than
:ref:`tonemap white<class_Environment_property_tonemap_white>`. This allows for accurate color
tái hiện trên các màn hình HDR có khả năng tái hiện các giá trị cảnh sáng hơn ban đầu. Khi :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` tăng lên cao hơn :ref:`tonemap white<class_Environment_property_tonemap_white>`, giá trị trắng của tonemap sẽ được điều chỉnh để khớp với giá trị tuyến tính tối đa đầu ra này.

Tonemapper :ref:`AgX<class_Environment_constant_tone_mapper_agx>` hoạt động tương tự như
:ref:`Reinhard<class_Environment_constant_tone_mapper_reinhardt>` in this way, but its
:ref:`tonemap white<class_Environment_property_tonemap_agx_white>` is always multiplied by
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>`. The
:ref:`Linear<class_Environment_constant_tone_mapper_linear>` tonemapper applies no tonemapping at
tất cả; :ref:`tonemap white<class_Environment_property_tonemap_white>` của nó bằng
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` in all scenarios. The
:ref:`Filmic<class_Environment_constant_tone_mapper_filmic>` and
:ref:`ACES<class_Environment_constant_tone_mapper_aces>` tonemappers ignore
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` entirely and always produce an
hình ảnh trong phạm vi SDR.

Tại sao không kết hợp giá trị tuyến tính tối đa đầu ra với các kỹ thuật khác?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Tonemapping, indirect lighting, global illumination và các hiệu ứng post-processing đều phụ thuộc vào các giá trị màu cảnh ổn định để tạo ra kết quả nhất quán và có thể dự đoán trong cả chế độ SDR và HDR. Nếu developer sử dụng các loại kỹ thuật này với một cảnh có các giá trị màu thay đổi dựa trên :ref:`output max linear value<class_Window_method_get_output_max_linear_value>`, kết quả sẽ không còn tương tự trên các màn hình có khả năng khác nhau.

Ví dụ: cường độ của hiệu ứng phát sáng chịu ảnh hưởng trực tiếp từ độ sáng của cảnh. Nếu độ sáng của cảnh thay đổi dựa trên
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>`, then the glow
thì cường độ cũng sẽ thay đổi: một
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` will produce a
hiệu ứng phát sáng mạnh hơn, đây thường là hành vi không mong muốn.

Giá trị độ chói tuyệt đối
-------------------------

Khi sử dụng đầu ra HDR, :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` được tính dựa trên độ chói của màu trắng tham chiếu và độ chói tối đa của màn hình.

Độ chói của màu trắng tham chiếu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Độ chói của màu trắng tham chiếu, hay gọi ngắn gọn là độ chói tham chiếu, đại diện cho giá trị trắng SDR sáng nhất có thể. Khi người dùng thay đổi cài đặt độ sáng của thiết bị tạo ra tín hiệu video, chẳng hạn như máy tính để bàn, máy tính xách tay hoặc điện thoại thông minh, họ chỉ đơn giản là đang điều chỉnh độ chói tham chiếu. Trên điện thoại thông minh, thay đổi này có thể diễn ra tự động thông qua tính năng độ sáng màn hình tự động của điện thoại, đồng thời cũng xảy ra khi người dùng tự điều chỉnh độ sáng màn hình. Trên máy tính để bàn hoặc máy tính xách tay, có nhiều cách khác nhau để điều chỉnh độ chói tham chiếu tùy thuộc vào hệ điều hành.

Giá trị này thường nằm trong khoảng 100 đến 300 nit và luôn được biểu diễn bằng một
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` of exactly ``1.0``.
Giá trị này cũng có thể được gọi là "paper white" hoặc "SDR white level".

.. note::

	Khi sử dụng màn hình ngoài trên Windows, cài đặt màn hình HDR *SDR content brightness* sẽ trực tiếp kiểm soát giá trị độ chói tham chiếu và là cách chính để điều chỉnh độ sáng của desktop Windows và Godot. Khi sử dụng màn hình HDR tích hợp trên Windows, việc thay đổi *HDR content brightness* cũng trực tiếp kiểm soát độ chói tham chiếu, nhưng không ảnh hưởng đến độ sáng của desktop Windows hoặc Godot vì một cơ chế triển khai độ sáng riêng sẽ triệt tiêu mọi tác động của các thay đổi đối với độ chói tham chiếu.

Độ chói tối đa
^^^^^^^^^^^^^^

Độ chói tối đa là một thuộc tính của màn hình HDR. Giá trị này có thể nằm trong khoảng từ 250 đến 2.000 nit hoặc cao hơn. Màn hình ngoài thường báo cáo giá trị độ chói tối đa cao hơn khả năng vật lý của màn hình, dẫn đến việc màn hình áp dụng tonemapping có thể nhìn thấy. Một số hệ điều hành máy tính để bàn hoặc máy tính xách tay cung cấp cách hiệu chỉnh giá trị độ chói tối đa được sử dụng cho từng màn hình ngoài.

.. note::

	Khi sử dụng màn hình tích hợp trên Windows, độ chói tối đa được báo cáo sẽ thay đổi khi người dùng điều chỉnh độ sáng màn hình máy tính xách tay, trong khi độ chói tham chiếu được báo cáo vẫn không đổi. Hành vi này trái ngược với việc sử dụng màn hình ngoài trên Windows và điều chỉnh cài đặt màn hình HDR *SDR content brightness*, đồng thời cũng trái ngược với các nền tảng khác.

Giá trị tuyến tính tối đa đầu ra trong thực tế
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Khi ở chế độ HDR, :ref:`output max linear value<class_Window_method_get_output_max_linear_value>` sẽ tăng khi người dùng giảm độ chói tham chiếu, vì có thêm khoảng headroom HDR. Tương tự, khi người dùng tăng độ chói tham chiếu, họ sẽ có ít khoảng headroom HDR hơn và
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` will decrease. In some cases when using
chế độ HDR với độ chói tham chiếu cao nhất,
:ref:`output max linear value<class_Window_method_get_output_max_linear_value>` will equal ``1.0``, matching SDR behavior,
vì không còn khoảng headroom HDR.

Không phải mọi màn hình đều giống nhau
--------------------------------------

Các tiêu chuẩn SDR được thiết kế để phù hợp với khả năng của những màn hình hiện có được sử dụng phổ biến trên toàn thế giới. Các tiêu chuẩn HDR được xây dựng có chủ đích theo hướng ngược lại: chúng được thiết kế để tận dụng khả năng của một màn hình lý tưởng hiện chưa phổ biến rộng rãi.

Trong thực tế, điều này có nghĩa là các màn hình HDR thông thường có thể tự thực hiện tonemapping, gamut mapping hoặc dynamic tonemapping (DTM) nội bộ để hỗ trợ nội dung mở rộng đến gamut và dải độ chói rộng hơn khả năng mà phần cứng vật lý có thể đạt được. Một số màn hình không thể hiển thị các giá trị màu rất sáng chiếm hơn một phần nhỏ (1% đến 10%) của màn hình, và sẽ tạm thời làm tối toàn bộ hình ảnh hoặc một phần hình ảnh khi điều này xảy ra. Các tính năng này có thể tạo ra những màu sắc không đại diện cho các màn hình khác, vì vậy tốt nhất là tắt chúng, nếu có thể, khi phát triển game HDR. Bạn có thể tắt một phần hoặc toàn bộ các tính năng này bằng cách bật chế độ HGiG trên màn hình hoặc đặt chế độ của màn hình thành "clip" và/hoặc "stable". Một số màn hình HDR có thể hiển thị các màu tối hoặc bão hòa khác với các màn hình khác; sự khác biệt về hình thức này thường là kết quả của các công nghệ màn hình.
