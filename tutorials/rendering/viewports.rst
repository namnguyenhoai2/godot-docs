.. _doc_viewports:

Sử dụng Viewport
================

Giới thiệu
----------

Hãy hình dung :ref:`Viewport <class_Viewport>` như một màn hình mà trên đó game được chiếu lên. Để nhìn thấy game, chúng ta cần có một bề mặt để vẽ game lên. Bề mặt đó là Root Viewport.

.. image:: img/subviewportnode.webp

:ref:`SubViewports <class_SubViewport>` are a kind of Viewport that can be added to the scene so that there
có nhiều bề mặt để vẽ lên. Khi vẽ vào một SubViewport, chúng ta gọi nó là render target. Chúng ta có thể truy cập nội dung của render target bằng cách truy cập :ref:`texture <class_Viewport_method_get_texture>` tương ứng. Bằng cách sử dụng một SubViewport làm render target, chúng ta có thể render nhiều scene đồng thời hoặc render vào một :ref:`ViewportTexture <class_ViewportTexture>` được áp dụng lên một đối tượng trong scene, chẳng hạn như một skybox động.

:ref:`SubViewports <class_SubViewport>` have a variety of use cases, including:

- Render các đối tượng 3D trong game 2D - Render các phần tử 2D trong game 3D - Render texture động - Tạo texture theo thủ tục trong runtime - Render nhiều camera trong cùng một scene

Điểm chung của tất cả các trường hợp sử dụng này là bạn có khả năng vẽ các đối tượng lên một texture như thể đó là một màn hình khác, sau đó có thể chọn cách xử lý texture kết quả.

Một loại Viewport khác trong Godot là :ref:`Windows <class_Window>`. Chúng cho phép chiếu nội dung lên một cửa sổ. Mặc dù Root Viewport là một Window, chúng kém linh hoạt hơn. Nếu muốn sử dụng texture của một Viewport, phần lớn thời gian bạn sẽ làm việc với :ref:`SubViewports <class_SubViewport>`.

Input
-----

:ref:`Viewports <class_Viewport>` are also responsible for delivering properly adjusted and
các sự kiện input đã scale đến những node con của chúng. Theo mặc định, :ref:`SubViewports <class_SubViewport>` không tự động nhận input, trừ khi chúng nhận input từ node trực tiếp
:ref:`SubViewportContainer <class_SubViewportContainer>` parent node. In this case, input can be
bị vô hiệu hóa bằng thuộc tính :ref:`Disable Input <class_Viewport_property_gui_disable_input>`.

.. image:: img/input.webp

Để biết thêm thông tin về cách Godot xử lý input, hãy đọc :ref:`Input Event Tutorial <doc_inputevent>`.

Listener
--------

Godot hỗ trợ âm thanh 3D (trong cả node 2D và 3D). Bạn có thể tìm hiểu thêm về nội dung này trong :ref:`Audio Streams Tutorial <doc_audio_streams>`. Để có thể nghe được loại âm thanh này, :ref:`Viewport <class_Viewport>` cần được bật làm listener (cho 2D hoặc 3D). Nếu bạn đang sử dụng :ref:`SubViewport <class_SubViewport>` để hiển thị :ref:`World3D <class_World3D>` hoặc
:ref:`World2D <class_World2D>`, don't forget to enable this!

Camera (2D & 3D)
----------------

Khi sử dụng :ref:`Camera3D <class_Camera3D>` hoặc
:ref:`Camera2D <class_Camera2D>`, it will always display on the
:ref:`Viewport <class_Viewport>` cha gần nhất (đi về phía root). Ví dụ, trong hệ phân cấp sau:

.. image:: img/cameras.webp

``CameraA`` sẽ hiển thị trên Root :ref:`Viewport <class_Viewport>` và sẽ vẽ ``MeshA``. ``CameraB`` sẽ được :ref:`SubViewport <class_SubViewport>` thu nhận cùng với ``MeshB``. Mặc dù ``MeshB`` nằm trong hệ phân cấp của scene, nó vẫn không được vẽ lên Root Viewport. Tương tự, ``MeshA`` sẽ không hiển thị từ SubViewport vì SubViewport chỉ thu nhận các node nằm bên dưới chúng trong hệ phân cấp.

Chỉ có thể có một camera hoạt động trên mỗi :ref:`Viewport <class_Viewport>`, vì vậy nếu có nhiều hơn một camera, hãy đảm bảo camera mong muốn có thuộc tính :ref:`current <class_Camera3D_property_current>` được đặt, hoặc đặt nó làm camera hiện tại bằng cách gọi:

.. tabs::
 .. code-tab:: gdscript GDScript

    camera.make_current()

 .. code-tab:: csharp

    camera.MakeCurrent();

Theo mặc định, camera sẽ render tất cả các đối tượng trong world của chúng. Trong 3D, camera có thể sử dụng
:ref:`cull_mask <class_Camera3D_property_cull_mask>` property combined with the
:ref:`VisualInstance3D's <class_VisualInstance3D>` :ref:`layer <class_VisualInstance3D_property_layers>`
thuộc tính để giới hạn những đối tượng được render.

Scale & stretching
------------------

:ref:`SubViewports <class_SubViewport>` have a :ref:`size<class_SubViewport_property_size>` property, which represents the size of the SubViewport
theo pixel. Đối với các SubViewport là node con của :ref:`SubViewportContainers <class_SubViewportContainer>`, những giá trị này sẽ bị ghi đè, nhưng đối với tất cả các SubViewport khác, chúng sẽ thiết lập độ phân giải.

Bạn cũng có thể scale nội dung 2D và làm cho độ phân giải của :ref:`SubViewport <class_SubViewport>` khác với độ phân giải được chỉ định trong size bằng cách gọi:

.. tabs::
 .. code-tab:: gdscript GDScript

    sub_viewport.set_size_2d_override(Vector2i(width, height)) # Kích thước tùy chỉnh cho 2D.
    sub_viewport.set_size_2d_override_stretch(true) # Bật stretch cho kích thước tùy chỉnh.

 .. code-tab:: csharp

    subViewport.Size2DOverride = new Vector2I(width, height); // Kích thước tùy chỉnh cho 2D.
    subViewport.Size2DOverrideStretch = true; // Bật stretch cho kích thước tùy chỉnh.

Để biết thông tin về scale và stretching với Root Viewport, hãy truy cập :ref:`Multiple Resolutions Tutorial <doc_multiple_resolutions>`

World
-----

Đối với 3D, một :ref:`Viewport <class_Viewport>` sẽ chứa một :ref:`World3D <class_World3D>`. Về cơ bản, đây là vũ trụ liên kết physics và rendering với nhau. Các node dựa trên Node3D sẽ đăng ký bằng World3D của Viewport gần nhất. Theo mặc định, Viewport mới tạo không chứa World3D mà sử dụng World3D giống Viewport cha. Root Viewport luôn chứa một World3D, đây là nơi các đối tượng được render theo mặc định.

Có thể thiết lập một :ref:`World3D <class_World3D>` trong một :ref:`Viewport <class_Viewport>` bằng thuộc tính :ref:`World 3D<class_Viewport_property_world_3d>`, thuộc tính này sẽ tách tất cả node con của :ref:`Viewport <class_Viewport>` và ngăn chúng tương tác với World3D của Viewport cha. Điều này đặc biệt hữu ích trong những trường hợp chẳng hạn như khi bạn muốn hiển thị một nhân vật 3D riêng biệt chồng lên game (như trong StarCraft).

Để hỗ trợ các trường hợp bạn muốn tạo :ref:`Viewports <class_Viewport>` chỉ hiển thị một đối tượng nhưng không muốn tạo :ref:`World3D <class_World3D>`, Viewport có tùy chọn sử dụng :ref:`Own World3D <class_Viewport_property_own_world_3d>`. Tùy chọn này hữu ích khi bạn muốn instance các nhân vật hoặc đối tượng 3D trong :ref:`World2D <class_World2D>`.

Đối với 2D, mỗi :ref:`Viewport <class_Viewport>` luôn chứa :ref:`World2D <class_World2D>` riêng. Trong hầu hết trường hợp, điều này là đủ, nhưng nếu cần chia sẻ chúng, bạn có thể thực hiện bằng cách thiết lập :ref:`world_2d<class_Viewport_property_world_2d>` trên Viewport thông qua code.

Để xem ví dụ về cách hoạt động của tính năng này, hãy xem lần lượt các demo project `3D in 2D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/3d_in_2d>`_ và `2D in 3D <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/2d_in_3d>`_.

Capture
-------

Bạn có thể truy vấn bản capture của nội dung :ref:`Viewport <class_Viewport>`. Đối với Root Viewport, về cơ bản đây là ảnh chụp màn hình. Việc này được thực hiện bằng đoạn code sau:

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

Nhưng nếu bạn sử dụng cách này trong ``_ready()`` hoặc từ frame đầu tiên của quá trình khởi tạo :ref:`Viewport's <class_Viewport>`, bạn sẽ nhận được một texture rỗng vì chưa có gì để lấy làm texture. Bạn có thể xử lý việc này bằng (ví dụ):

.. tabs::
 .. code-tab:: gdscript GDScript

   # Chờ đến khi frame hoàn tất trước khi lấy texture.
   await RenderingServer.frame_post_draw
   # Sau đó, bạn có thể lấy image.

 .. code-tab:: csharp

    // Chờ đến khi frame hoàn tất trước khi lấy texture.
    await ToSignal(RenderingServer.Singleton, RenderingServer.SignalName.FramePostDraw);
    // Sau đó, bạn có thể lấy image.

Viewport Container
------------------

Nếu :ref:`SubViewport <class_SubViewport>` là node con của :ref:`SubViewportContainer <class_SubViewportContainer>`, nó sẽ trở nên hoạt động và hiển thị mọi thứ bên trong. Bố cục sẽ như sau:

.. image:: img/container.webp

:ref:`SubViewport <class_SubViewport>` sẽ phủ hoàn toàn khu vực của :ref:`SubViewportContainer <class_SubViewportContainer>` cha nếu :ref:`Stretch<class_SubViewportContainer_property_stretch>` được đặt thành ``true`` trong SubViewportContainer.

.. note::

    Kích thước của :ref:`SubViewportContainer <class_SubViewportContainer>` không thể nhỏ hơn kích thước của :ref:`SubViewport <class_SubViewport>`.

Rendering
---------

Vì :ref:`Viewport <class_Viewport>` là lối vào một bề mặt rendering khác, nó cung cấp một số thuộc tính rendering có thể khác với project settings. Bạn có thể chọn sử dụng mức :ref:`MSAA <class_Viewport_property_msaa_2d>` khác cho từng Viewport. Hành vi mặc định là ``Disabled``.

Nếu biết rằng :ref:`Viewport <class_Viewport>` chỉ được sử dụng cho 2D, bạn có thể :ref:`Disable 3D<class_Viewport_property_disable_3d>`. Khi đó, Godot sẽ giới hạn cách Viewport được vẽ. Việc tắt 3D nhanh hơn một chút và sử dụng ít bộ nhớ hơn so với khi bật 3D. Bạn nên tắt 3D nếu viewport của bạn không render bất kỳ nội dung 3D nào.

.. note::

    Nếu cần render shadow 3D trong viewport, hãy đảm bảo đặt thuộc tính :ref:`positional_shadow_atlas_size<class_Viewport_property_positional_shadow_atlas_size>` của viewport thành giá trị cao hơn ``0``. Nếu không, shadow sẽ không được render. Theo mặc định, project setting tương đương được đặt thành ``4096`` trên nền tảng desktop và ``2048`` trên nền tảng mobile.

Godot cũng cung cấp cách tùy chỉnh cách mọi thứ được vẽ bên trong :ref:`Viewports <class_Viewport>` bằng :ref:`Debug Draw<class_Viewport_property_debug_draw>`. Debug Draw cho phép bạn chỉ định một mode xác định cách Viewport hiển thị những thứ được vẽ bên trong nó. Theo mặc định, Debug Draw là ``Disabled``. Một số tùy chọn khác là ``Unshaded``, ``Overdraw`` và ``Wireframe``. Để xem danh sách đầy đủ, hãy tham khảo :ref:`Viewport Documentation<class_Viewport_property_debug_draw>`.

-  **Debug Draw = Disabled** (mặc định): Scene được vẽ bình thường.

  .. image:: img/default_scene.webp

-  **Debug Draw = Unshaded**: Unshaded vẽ scene mà không sử dụng thông tin lighting, vì vậy tất cả đối tượng sẽ có màu phẳng theo màu albedo của chúng.

  .. image:: img/unshaded.webp

-  **Debug Draw = Overdraw**: Overdraw vẽ các mesh bán trong suốt với additive blend, để bạn có thể thấy các mesh chồng lấn lên nhau như thế nào.

  .. image:: img/overdraw.webp

-  **Debug Draw = Wireframe**: Wireframe vẽ scene chỉ bằng các cạnh của những triangle trong mesh.

  .. image:: img/wireframe.webp

.. note::

    Các mode Debug Draw hiện chưa được hỗ trợ khi sử dụng phương thức rendering Compatibility. Chúng sẽ hiển thị như các mode draw thông thường.

Render target
-------------

Khi render vào một :ref:`SubViewport <class_SubViewport>`, bất kỳ nội dung nào bên trong sẽ không hiển thị trong scene editor. Để hiển thị nội dung, bạn phải vẽ :ref:`ViewportTexture <class_ViewportTexture>` của SubViewport ở đâu đó. Bạn có thể yêu cầu việc này qua code bằng (ví dụ):

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lệnh này cung cấp cho chúng ta ViewportTexture.
    var tex = viewport.get_texture()
    sprite.texture = tex

 .. code-tab:: csharp

    // Lệnh này cung cấp cho chúng ta ViewportTexture.
    var tex = viewport.GetTexture();
    sprite.Texture = tex;

Hoặc bạn có thể gán nó trong editor bằng cách chọn "New ViewportTexture"

.. image:: img/texturemenu.webp

rồi chọn :ref:`Viewport <class_Viewport>` mà bạn muốn sử dụng.

.. image:: img/texturepath.webp

Mỗi frame, texture :ref:`Viewport's <class_Viewport>` sẽ được xóa bằng clear color mặc định (hoặc màu trong suốt nếu :ref:`Transparent BG<class_Viewport_property_transparent_bg>` được đặt thành ``true``). Bạn có thể thay đổi điều này bằng cách đặt :ref:`Clear Mode<class_SubViewport_property_render_target_clear_mode>` thành ``Never`` hoặc ``Next Frame``. Đúng như tên gọi, Never nghĩa là texture sẽ không bao giờ bị xóa, trong khi next frame sẽ xóa texture ở frame tiếp theo rồi tự đặt lại thành Never.

Theo mặc định, việc kết xuất lại :ref:`SubViewport <class_SubViewport>` sẽ xảy ra khi :ref:`ViewportTexture <class_ViewportTexture>` của nó đã được vẽ trong một frame. Nếu hiển thị, nó sẽ được kết xuất; nếu không thì sẽ không được kết xuất. Có thể thay đổi hành vi này bằng cách đặt :ref:`Update Mode<class_SubViewport_property_render_target_update_mode>` thành ``Never``, ``Once``, ``Always`` hoặc ``When Parent Visible``. Never và Always lần lượt sẽ không bao giờ hoặc luôn luôn kết xuất lại. Once sẽ kết xuất lại trong frame tiếp theo, sau đó chuyển thành Never. Có thể sử dụng tùy chọn này để cập nhật Viewport theo cách thủ công. Tính linh hoạt này cho phép người dùng kết xuất một hình ảnh một lần, sau đó sử dụng texture mà không phải chịu chi phí kết xuất trong mỗi frame.

.. note::

    Hãy nhớ xem các bản demo của Viewport. Chúng có trong thư mục viewport của kho lưu trữ bản demo hoặc tại https://github.com/godotengine/godot-demo-projects/tree/master/viewport.
