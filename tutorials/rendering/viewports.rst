.. _doc_viewports:

Sử dụng Viewport
================

Giới thiệu
----------

Hãy hình dung một :ref:`Viewport <class_Viewport>` như một màn hình mà trò chơi được chiếu lên đó. Để nhìn thấy trò chơi, chúng ta cần có một bề mặt để vẽ trò chơi lên. Bề mặt đó là Root Viewport.

.. image:: img/subviewportnode.webp

:ref:`SubViewports <class_SubViewport>` là một loại Viewport có thể được thêm vào scene để có nhiều bề mặt vẽ. Khi vẽ lên một SubViewport, chúng ta gọi nó là render target. Chúng ta có thể truy cập nội dung của render target bằng cách truy cập :ref:`texture <class_Viewport_method_get_texture>` tương ứng. Bằng cách sử dụng SubViewport làm render target, chúng ta có thể render nhiều scene đồng thời hoặc render lên một :ref:`ViewportTexture <class_ViewportTexture>` được áp dụng cho một đối tượng trong scene, chẳng hạn như một skybox động.

:ref:`SubViewports <class_SubViewport>` có nhiều trường hợp sử dụng, bao gồm:

- Render các đối tượng 3D trong một game 2D
- Render các thành phần 2D trong một game 3D
- Render các texture động
- Tạo texture theo quy trình trong runtime
- Render nhiều camera trong cùng một scene

Điểm chung của tất cả các trường hợp sử dụng này là bạn có khả năng vẽ các đối tượng lên một texture như thể đó là một màn hình khác, sau đó có thể chọn cách xử lý texture thu được.

Một loại Viewport khác trong Godot là :ref:`Windows <class_Window>`. Chúng cho phép chiếu nội dung lên một cửa sổ. Root Viewport là một Window, còn chúng thì kém linh hoạt hơn. Nếu muốn sử dụng texture của một Viewport, phần lớn thời gian bạn sẽ làm việc với :ref:`SubViewports <class_SubViewport>`.

Input
-----

:ref:`Viewports <class_Viewport>` cũng chịu trách nhiệm chuyển các input event đã được điều chỉnh và scale phù hợp đến các node con của chúng. Theo mặc định, :ref:`SubViewports <class_SubViewport>` không tự động nhận input, trừ khi nhận input từ node cha trực tiếp của chúng
:ref:`SubViewportContainer <class_SubViewportContainer>`. Trong trường hợp này, có thể tắt input bằng thuộc tính :ref:`Disable Input <class_Viewport_property_gui_disable_input>`.

.. image:: img/input.webp

Để biết thêm thông tin về cách Godot xử lý input, hãy đọc :ref:`Input Event Tutorial <doc_inputevent>`.

Listener
--------

Godot hỗ trợ âm thanh 3D (trong cả node 2D và 3D). Bạn có thể tìm thêm thông tin về vấn đề này trong :ref:`Audio Streams Tutorial <doc_audio_streams>`. Để có thể nghe được loại âm thanh này, cần bật :ref:`Viewport <class_Viewport>` làm listener (cho 2D hoặc 3D). Nếu bạn đang sử dụng một :ref:`SubViewport <class_SubViewport>` để hiển thị :ref:`World3D <class_World3D>` hoặc
:ref:`World2D <class_World2D>`, đừng quên bật tùy chọn này!

Camera (2D & 3D)
----------------

Khi sử dụng một :ref:`Camera3D <class_Camera3D>` hoặc
:ref:`Camera2D <class_Camera2D>`, nó sẽ luôn hiển thị trên :ref:`Viewport <class_Viewport>` cha gần nhất (theo hướng về root). Ví dụ, trong hệ phân cấp sau:

.. image:: img/cameras.webp

``CameraA`` sẽ hiển thị trên Root :ref:`Viewport <class_Viewport>` và sẽ vẽ ``MeshA``. ``CameraB`` sẽ được :ref:`SubViewport <class_SubViewport>` cùng với ``MeshB``. Mặc dù ``MeshB`` nằm trong hệ phân cấp của scene, nó vẫn không được vẽ lên Root Viewport. Tương tự, ``MeshA`` sẽ không hiển thị từ SubViewport vì SubViewport chỉ bắt các node nằm bên dưới chúng trong hệ phân cấp.

Mỗi :ref:`Viewport <class_Viewport>` chỉ có thể có một camera đang hoạt động, vì vậy nếu có nhiều hơn một camera, hãy đảm bảo camera mong muốn có thuộc tính :ref:`current <class_Camera3D_property_current>` được thiết lập hoặc đặt nó làm camera hiện tại bằng cách gọi:

.. tabs::
 .. code-tab:: gdscript GDScript

    camera.make_current()

 .. code-tab:: csharp

    camera.MakeCurrent();

Theo mặc định, camera sẽ render tất cả đối tượng trong world của chúng. Trong 3D, camera có thể sử dụng thuộc tính
:ref:`cull_mask <class_Camera3D_property_cull_mask>` kết hợp với thuộc tính
:ref:`VisualInstance3D's <class_VisualInstance3D>` :ref:`layer <class_VisualInstance3D_property_layers>` để giới hạn các đối tượng được render.

Scale & stretching
------------------

:ref:`SubViewports <class_SubViewport>` có thuộc tính :ref:`size<class_SubViewport_property_size>`, biểu thị kích thước của SubViewport tính bằng pixel. Đối với các SubViewport là node con của :ref:`SubViewportContainers <class_SubViewportContainer>`, những giá trị này sẽ bị ghi đè, nhưng đối với tất cả các SubViewport khác, thuộc tính này sẽ thiết lập độ phân giải của chúng.

Bạn cũng có thể scale nội dung 2D và làm cho độ phân giải của :ref:`SubViewport <class_SubViewport>` khác với độ phân giải được chỉ định trong size bằng cách gọi:

.. tabs::
 .. code-tab:: gdscript GDScript

    sub_viewport.set_size_2d_override(Vector2i(width, height)) # Kích thước tùy chỉnh cho 2D.
    sub_viewport.set_size_2d_override_stretch(true) # Bật stretch cho kích thước tùy chỉnh.

 .. code-tab:: csharp

    subViewport.Size2DOverride = new Vector2I(width, height); // Kích thước tùy chỉnh cho 2D.
    subViewport.Size2DOverrideStretch = true; // Bật stretch cho kích thước tùy chỉnh.

Để biết thông tin về việc scale và stretch với Root Viewport, hãy truy cập :ref:`Multiple Resolutions Tutorial <doc_multiple_resolutions>`

World
-----

Đối với 3D, một :ref:`Viewport <class_Viewport>` sẽ chứa một :ref:`World3D <class_World3D>`. Về cơ bản, đây là vũ trụ liên kết physics và rendering với nhau. Các node dựa trên Node3D sẽ đăng ký bằng World3D của Viewport gần nhất. Theo mặc định, Viewport mới được tạo không chứa World3D mà sử dụng World3D của Viewport cha. Root Viewport luôn chứa một World3D, và theo mặc định các đối tượng được render vào World3D này.

Có thể thiết lập một :ref:`World3D <class_World3D>` trong một :ref:`Viewport <class_Viewport>` bằng thuộc tính :ref:`World 3D <class_Viewport_property_world_3d>`, thuộc tính này sẽ tách tất cả node con của :ref:`Viewport <class_Viewport>` này và ngăn chúng tương tác với World3D của Viewport cha. Điều này đặc biệt hữu ích trong những tình huống mà bạn muốn hiển thị, chẳng hạn, một nhân vật 3D riêng biệt chồng lên game (như trong StarCraft).

Để hỗ trợ các tình huống bạn muốn tạo :ref:`Viewports <class_Viewport>` chỉ hiển thị từng đối tượng riêng lẻ mà không muốn tạo một :ref:`World3D <class_World3D>`, Viewport có tùy chọn sử dụng :ref:`Own World3D <class_Viewport_property_own_world_3d>` của nó. Điều này hữu ích khi bạn muốn instance các nhân vật hoặc đối tượng 3D trong :ref:`World2D <class_World2D>`.

Đối với 2D, mỗi :ref:`Viewport <class_Viewport>` luôn chứa :ref:`World2D <class_World2D>` riêng của nó. Điều này đáp ứng hầu hết trường hợp, nhưng nếu muốn chia sẻ chúng, bạn có thể thực hiện bằng cách thiết lập :ref:`world_2d<class_Viewport_property_world_2d>` trên Viewport thông qua code.

Để xem ví dụ về cách thức hoạt động, hãy xem lần lượt các project demo `3D in 2D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/3d_in_2d>`_ và `2D in 3D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/2d_in_3d>`_.

Capture
-------

Bạn có thể truy vấn ảnh chụp nội dung của :ref:`Viewport <class_Viewport>`. Đối với Root Viewport, đây thực chất là ảnh chụp màn hình. Việc này được thực hiện bằng code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

   # Lấy Image đã capture bằng get_image().
   var img = get_viewport().get_texture().get_image()
   # Chuyển Image thành ImageTexture.
   var tex = ImageTexture.create_from_image(img)
   # Thiết lập texture cho sprite.
   sprite.texture = tex

 .. code-tab:: csharp

    // Lấy Image đã capture bằng get_image().
    var img = GetViewport().GetTexture().GetImage();
    // Chuyển Image thành ImageTexture.
    var tex = ImageTexture.CreateFromImage(img);
    // Thiết lập texture cho sprite.
    sprite.Texture = tex;

Nhưng nếu bạn sử dụng điều này trong ``_ready()`` hoặc từ khung hình đầu tiên của quá trình khởi tạo :ref:`Viewport <class_Viewport>`, bạn sẽ nhận được một texture trống vì không có gì để lấy làm texture. Bạn có thể xử lý việc này, chẳng hạn như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

   # Chờ cho đến khi khung hình hoàn tất trước khi lấy texture.
   await RenderingServer.frame_post_draw
   # Sau đó, bạn có thể lấy image.

 .. code-tab:: csharp

    // Chờ cho đến khi khung hình hoàn tất trước khi lấy texture.
    await ToSignal(RenderingServer.Singleton, RenderingServer.SignalName.FramePostDraw);
    // Sau đó, bạn có thể lấy image.

Viewport Container
------------------

Nếu :ref:`SubViewport <class_SubViewport>` là một nút con của :ref:`SubViewportContainer <class_SubViewportContainer>`, nó sẽ trở nên hoạt động và hiển thị mọi thứ bên trong. Bố cục sẽ như sau:

.. image:: img/container.webp

:ref:`SubViewport <class_SubViewport>` sẽ phủ hoàn toàn vùng của :ref:`SubViewportContainer <class_SubViewportContainer>` cha nếu :ref:`Stretch<class_SubViewportContainer_property_stretch>` được đặt thành ``true`` trong SubViewportContainer.

.. note::

    Kích thước của :ref:`SubViewportContainer <class_SubViewportContainer>` không thể nhỏ hơn kích thước của :ref:`SubViewport <class_SubViewport>`.

Kết xuất
--------

Vì :ref:`Viewport <class_Viewport>` là một lối vào một bề mặt kết xuất khác, nó cung cấp một số thuộc tính kết xuất có thể khác với các thiết lập của project. Bạn có thể chọn sử dụng một mức :ref:`MSAA <class_Viewport_property_msaa_2d>` khác cho mỗi Viewport. Hành vi mặc định là ``Disabled``.

Nếu biết rằng :ref:`Viewport <class_Viewport>` chỉ được sử dụng cho 2D, bạn có thể :ref:`Disable 3D <class_Viewport_property_disable_3d>`. Khi đó, Godot sẽ giới hạn cách Viewport được vẽ. Việc tắt 3D nhanh hơn một chút và sử dụng ít bộ nhớ hơn so với khi bật 3D. Bạn nên tắt 3D nếu viewport của mình không kết xuất bất kỳ nội dung 3D nào.

.. note::

    Nếu cần kết xuất bóng 3D trong viewport, hãy đảm bảo đặt thuộc tính :ref:`positional_shadow_atlas_size<class_Viewport_property_positional_shadow_atlas_size>` của viewport thành giá trị cao hơn ``0``. Nếu không, bóng sẽ không được kết xuất. Theo mặc định, thiết lập tương đương của project được đặt thành ``4096`` trên các nền tảng desktop và ``2048`` trên các nền tảng mobile.

Godot cũng cung cấp cách tùy chỉnh cách mọi thứ được vẽ bên trong :ref:`Viewports <class_Viewport>` bằng :ref:`Debug Draw <class_Viewport_property_debug_draw>`. Debug Draw cho phép bạn chỉ định một chế độ xác định cách Viewport hiển thị những nội dung được vẽ bên trong nó. Theo mặc định, Debug Draw là ``Disabled``. Một số tùy chọn khác là ``Unshaded``, ``Overdraw`` và ``Wireframe``. Để xem danh sách đầy đủ, hãy tham khảo :ref:`Viewport Documentation <class_Viewport_property_debug_draw>`.

-  **Debug Draw = Disabled** (mặc định): Cảnh được vẽ bình thường.

  .. image:: img/default_scene.webp

-  **Debug Draw = Unshaded**: Unshaded vẽ cảnh mà không sử dụng thông tin chiếu sáng, vì vậy tất cả đối tượng đều có màu phẳng theo màu albedo của chúng.

  .. image:: img/unshaded.webp

-  **Debug Draw = Overdraw**: Overdraw vẽ các mesh bán trong suốt với phép trộn cộng, nhờ đó bạn có thể thấy các mesh chồng lên nhau như thế nào.

  .. image:: img/overdraw.webp

-  **Debug Draw = Wireframe**: Wireframe vẽ cảnh chỉ bằng các cạnh của tam giác trong các mesh.

  .. image:: img/wireframe.webp

.. note::

    Các chế độ Debug Draw hiện **chưa** được hỗ trợ khi sử dụng phương thức kết xuất Compatibility. Chúng sẽ xuất hiện như các chế độ vẽ thông thường.

Mục tiêu kết xuất
-----------------

Khi kết xuất vào một :ref:`SubViewport <class_SubViewport>`, mọi thứ bên trong sẽ không hiển thị trong trình chỉnh sửa cảnh. Để hiển thị nội dung, bạn phải vẽ :ref:`ViewportTexture <class_ViewportTexture>` của SubViewport ở đâu đó. Có thể yêu cầu việc này bằng code, chẳng hạn như:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thao tác này cung cấp cho chúng ta ViewportTexture.
    var tex = viewport.get_texture()
    sprite.texture = tex

 .. code-tab:: csharp

    // Thao tác này cung cấp cho chúng ta ViewportTexture.
    var tex = viewport.GetTexture();
    sprite.Texture = tex;

Hoặc có thể gán nó trong trình chỉnh sửa bằng cách chọn "New ViewportTexture"

.. image:: img/texturemenu.webp

rồi chọn :ref:`Viewport <class_Viewport>` mà bạn muốn sử dụng.

.. image:: img/texturepath.webp

Mỗi khung hình, texture của :ref:`Viewport <class_Viewport>` sẽ được xóa bằng màu xóa mặc định (hoặc màu trong suốt nếu :ref:`Transparent BG <class_Viewport_property_transparent_bg>` được đặt thành ``true``). Bạn có thể thay đổi điều này bằng cách đặt :ref:`Clear Mode <class_SubViewport_property_render_target_clear_mode>` thành ``Never`` hoặc ``Next Frame``. Như tên gọi cho thấy, Never nghĩa là texture sẽ không bao giờ bị xóa, còn next frame sẽ xóa texture ở khung hình tiếp theo rồi tự đặt lại thành Never.

Theo mặc định, :ref:`SubViewport <class_SubViewport>` sẽ được kết xuất lại khi :ref:`ViewportTexture <class_ViewportTexture>` của nó đã được vẽ trong một khung hình. Nếu hiển thị, nó sẽ được kết xuất; nếu không, nó sẽ không được kết xuất. Có thể thay đổi hành vi này bằng cách đặt :ref:`Update Mode <class_SubViewport_property_render_target_update_mode>` thành ``Never``, ``Once``, ``Always`` hoặc ``When Parent Visible``. Never và Always lần lượt sẽ không bao giờ hoặc luôn luôn kết xuất lại. Once sẽ kết xuất lại ở khung hình tiếp theo rồi chuyển thành Never. Bạn có thể dùng cách này để cập nhật Viewport thủ công. Tính linh hoạt này cho phép người dùng kết xuất một image một lần rồi sử dụng texture mà không phải chịu chi phí kết xuất ở mỗi khung hình.

.. note::

    Hãy nhớ kiểm tra các bản demo Viewport. Chúng có trong thư mục viewport của kho lưu trữ demo hoặc tại https://github.com/godotengine/godot-demo-projects/tree/master/viewport.

.. _`3D in 2D`: https://github.com/godotengine/godot-demo-projects/tree/master/viewport/3d_in_2d
.. _`2D in 3D`: https://github.com/godotengine/godot-demo-projects/tree/master/viewport/2d_in_3d
