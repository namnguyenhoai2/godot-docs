.. _doc_upgrading_to_godot_4:

Nâng cấp từ Godot 3 lên Godot 4
===============================

Tôi có nên nâng cấp lên Godot 4 không?
--------------------------------------

Trước khi bắt đầu quá trình nâng cấp, bạn nên cân nhắc những ưu điểm và nhược điểm mà việc nâng cấp sẽ mang lại cho dự án của mình.

Ưu điểm của việc nâng cấp
~~~~~~~~~~~~~~~~~~~~~~~~~

Cùng với `các tính năng mới có trong 4.0 <https://godotengine.org/article/godot-4-0-sets-sail>`__, việc nâng cấp mang lại những ưu điểm sau:

- Nhiều lỗi được sửa trong 4.0 nhưng không thể được khắc phục trong 3.x vì nhiều lý do khác nhau (chẳng hạn như sự khác biệt giữa các graphics API hoặc khả năng tương thích ngược).
- 4.x sẽ có :ref:`thời gian hỗ trợ dài hơn <doc_release_policy>`. Godot 3.x sẽ tiếp tục được hỗ trợ trong một thời gian sau khi 4.0 được phát hành, nhưng cuối cùng sẽ ngừng nhận hỗ trợ.

Xem :ref:`doc_docs_changelog` để biết danh sách các trang mô tả những tính năng mới trong Godot 4.0, và :ref:`doc_list_of_features` để xem danh sách tất cả tính năng trong Godot.

Nhược điểm của việc nâng cấp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn không *cần* bất kỳ tính năng nào có trong Godot 4.x, bạn có thể muốn tiếp tục dùng Godot 3.x vì những lý do sau:

- Yêu cầu phần cứng cơ bản của Godot 4 (chẳng hạn như mức sử dụng bộ nhớ) cao hơn một chút, cả đối với editor lẫn các project đã export. Điều này là cần thiết để triển khai một số tối ưu hóa cốt lõi.
- Vì Godot 4 có nhiều tính năng hơn Godot 3 nên kích thước binary của các project đã export trong Godot 4 lớn hơn. Mặc dù điều này có thể được giảm thiểu bằng cách
  :ref:`tối ưu hóa bản build để giảm kích thước <doc_optimizing_for_size>`, một bản build 4.0 với cùng một tập module được bật vẫn sẽ lớn hơn bản build 3.x có cùng các module. Đây có thể là vấn đề khi
  :ref:`export lên Web <doc_exporting_for_web>`, vì kích thước binary ảnh hưởng trực tiếp đến tốc độ engine khởi tạo (bất kể tốc độ tải xuống).
- Godot 4 không hỗ trợ và sẽ không hỗ trợ rendering GLES2. (GLES3 vẫn được hỗ trợ thông qua Compatibility renderer mới, nghĩa là các thiết bị không hỗ trợ Vulkan vẫn có thể chạy Godot 4.)

  - Nếu bạn nhắm đến phần cứng **rất** cũ, chẳng hạn như đồ họa tích hợp Intel Sandy Bridge (thế hệ thứ 2), việc này sẽ khiến project không thể chạy trên phần cứng đó sau khi nâng cấp. `Các triển khai OpenGL bằng phần mềm <https://github.com/pal1000/mesa-dist-win>`__ có thể được dùng để vượt qua giới hạn này, nhưng chúng quá chậm để chơi game.

Những điểm cần lưu ý khi nâng cấp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. UPDATE: Planned feature. There are several planned or missing features that
.. may be added back in the future. Check this section for accuracy and update
.. it if things have changed!

**Vì Godot 4 được viết lại hoàn toàn ở nhiều khía cạnh nên đáng tiếc là một số tính năng đã bị mất trong quá trình này.** Một số tính năng trong đó có thể được khôi phục trong các bản phát hành Godot tương lai:

- Bullet physics đã bị loại bỏ để chuyển sang GodotPhysics. Điều này chỉ ảnh hưởng đến các project 3D sử dụng physics engine mặc định (là Bullet) và không thay đổi thủ công sang GodotPhysics. Không có kế hoạch thêm lại Bullet physics vào core, nhưng có thể tạo add-on của bên thứ ba cho tính năng này nhờ GDExtension.
- Theo mặc định, rendering trong 2D không còn được thực hiện ở HDR, nghĩa là các giá trị modulate "overbright" không tạo ra hiệu ứng hiển thị nào. Kể từ Godot 4.2, bạn có thể bật project setting :ref:`HDR 2D <class_ProjectSettings_property_rendering/viewport/hdr_2d>` để thực hiện rendering 2D ở HDR. Xem thêm :ref:`doc_environment_and_post_processing_using_glow_in_2d`.
- Mặc dù rendering trong 3D vẫn diễn ra ở HDR khi sử dụng Forward+ hoặc Mobile renderer, Viewport không còn có thể trả về dữ liệu HDR. Dự kiến tính năng này sẽ được khôi phục vào một thời điểm nào đó trong tương lai.
- Mono đã được thay thế bằng .NET 6. Điều này có nghĩa là hiện tại không còn hỗ trợ export các project C# sang Android, iOS và HTML5. Việc export các project C# sang các nền tảng desktop vẫn được hỗ trợ, và kể từ 4.2 đã có hỗ trợ thử nghiệm cho việc export sang các nền tảng mobile. Hỗ trợ export các project C# sang nhiều nền tảng hơn sẽ được khôi phục trong các bản phát hành 4.x tương lai khi hỗ trợ từ upstream được cải thiện.

Bạn có thể tìm danh sách đầy đủ hơn về các hồi quy chức năng bằng cách tìm kiếm `các issue được gắn nhãn "regression" nhưng không có nhãn "bug" trên GitHub <https://github.com/godotengine/godot/issues?q=is%3Aissue+is%3Aopen+label%3Aregression+-label%3Abug>`__.

Chuẩn bị trước khi nâng cấp (tùy chọn)
--------------------------------------

Nếu muốn sẵn sàng nâng cấp lên Godot 4 trong tương lai, hãy cân nhắc sử dụng
:ref:`class_Tweener` và singleton :ref:`class_Time` trong project của bạn. Cả hai class này đều có trong Godot 3.5 trở lên.

Nhờ vậy, bạn sẽ không phụ thuộc vào Tween node và các hàm thời gian của OS đã bị deprecated, cả hai đều bị loại bỏ trong Godot 4.0.

Bạn cũng nên đổi tên các shader bên ngoài để phần mở rộng của chúng là ``.gdshader`` thay vì ``.shader``. Godot 3.x hỗ trợ cả hai phần mở rộng, nhưng chỉ ``.gdshader`` được hỗ trợ trong Godot 4.0.

Chạy công cụ nâng cấp project
-----------------------------

.. danger::

    **Hãy tạo một bản sao lưu đầy đủ cho project của bạn** trước khi nâng cấp! Công cụ nâng cấp project *không* thực hiện bất kỳ thao tác sao lưu nào đối với project đang được nâng cấp.

    Bạn có thể sao lưu project bằng cách sử dụng version control hoặc sao chép thư mục project sang một vị trí khác.

Sử dụng Project Manager
~~~~~~~~~~~~~~~~~~~~~~~

Để sử dụng công cụ nâng cấp project:

1. Mở Godot 4 Project Manager.
2. Import project Godot 3.x bằng nút **Import**, hoặc dùng nút **Scan** để tìm project trong một thư mục.
3. Nhấp đúp vào project đã import (hoặc chọn project rồi chọn **Edit**).
4. Bạn sẽ thấy một hộp thoại xuất hiện với hai tùy chọn: **Convert project.godot Only** và **Convert Full Project**. Sau khi đảm bảo project của bạn đã được sao lưu (xem cảnh báo ở trên), hãy chọn **Convert Full Project**. **Convert project.godot Only** chỉ dành cho các trường hợp sử dụng nâng cao *only*, phòng khi công cụ chuyển đổi gặp lỗi.
5. Chờ cho đến khi quá trình chuyển đổi project hoàn tất. Với các project lớn có nhiều scene, quá trình này có thể mất vài phút.
6. Khi giao diện Project Manager xuất hiện trở lại, hãy nhấp đúp vào project (hoặc chọn project rồi chọn **Edit**) để mở project trong editor.

Nếu gặp vấn đề chuyển đổi do một số file project quá lớn hoặc quá dài, bạn có thể dùng command line để nâng cấp project (xem bên dưới). Cách này cho phép bạn ghi đè các giới hạn kích thước của trình chuyển đổi.

Sử dụng command line
~~~~~~~~~~~~~~~~~~~~

Để sử dụng công cụ nâng cấp dự án từ :ref:`dòng lệnh <doc_command_line_tutorial>`, bạn nên xác thực quá trình chuyển đổi dự án bằng cách chạy tệp nhị phân của trình chỉnh sửa Godot với các đối số sau:

::

    # [<max_file_kb>] [<max_line_size>] are optional arguments.
    # Remove them if you aren't changing their values.
    path/to/godot.binary --path /path/to/project/folder --validate-conversion-3to4 [<max_file_kb>] [<max_line_size>]

Nếu danh sách các nâng cấp dự kiến trông ổn, hãy chạy lệnh sau trên tệp nhị phân của trình chỉnh sửa Godot để nâng cấp các tệp dự án:

::

    # [<max_file_kb>] [<max_line_size>] are optional arguments.
    # Remove them if you aren't changing their values.
    path/to/godot.binary --path /path/to/project/folder --convert-3to4 [<max_file_kb>] [<max_line_size>]

``[<max_file_kb>]`` và ``[<max_line_size>]`` là các đối số *tùy chọn* dùng để chỉ định kích thước tối đa của các tệp cần chuyển đổi (tính bằng kilobyte và số dòng). Giới hạn mặc định lần lượt là 4 MB và 100.000 dòng. Nếu một tệp đạt một trong hai giới hạn này, tệp đó sẽ không được trình chuyển đổi dự án nâng cấp. Điều này hữu ích để ngăn các tài nguyên lớn làm quá trình nâng cấp chậm đến mức gần như dừng lại.

Nếu vẫn muốn công cụ nâng cấp dự án chuyển đổi các tệp lớn, hãy tăng giới hạn kích thước khi chạy công cụ nâng cấp dự án. Ví dụ: chạy tệp nhị phân của trình chỉnh sửa Godot với các đối số đó sẽ tăng cả hai giới hạn lên 10 lần:

::

    path/to/godot.binary --path /path/to/project/folder --convert-3to4 40000 1000000

.. note::

    Chỉ các dự án Godot 3.0 trở lên mới có thể được nâng cấp bằng công cụ chuyển đổi dự án có trong trình chỉnh sửa Godot 4.

    Bạn nên đảm bảo dự án của mình đã được cập nhật lên bản phát hành ổn định 3.x mới nhất trước khi chạy công cụ nâng cấp dự án.

Sửa dự án sau khi chạy công cụ nâng cấp dự án
---------------------------------------------

Sau khi nâng cấp dự án, bạn có thể nhận thấy một số thành phần không hiển thị như mong đợi. Các script cũng có thể chứa nhiều lỗi khác nhau (có thể lên đến hàng trăm lỗi trong các dự án lớn). Nguyên nhân là công cụ nâng cấp dự án không thể xử lý mọi tình huống. Do đó, phần lớn quá trình nâng cấp vẫn phải thực hiện thủ công.

Các node và tài nguyên được tự động đổi tên
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Danh sách dưới đây đề cập đến các node chỉ được đổi tên để bảo đảm tính nhất quán hoặc rõ ràng trong Godot 4.0. Công cụ nâng cấp dự án sẽ tự động đổi tên chúng trong các script của bạn.

Một nhóm tên đáng chú ý là các node 3D, tất cả đều được thêm hậu tố ``3D`` để nhất quán với các node 2D tương ứng. Ví dụ: ``Area`` hiện đã trở thành ``Area3D``.

Để dễ tìm kiếm, bảng này liệt kê tất cả các node và tài nguyên đã được đổi tên và tự động chuyển đổi, không bao gồm những mục chỉ được thêm hậu tố ``3D`` vào tên cũ:

+-----------------------------------------+-------------------------------------------+
| Tên cũ (Godot 3.x)                      | Tên mới (Godot 4)                         |
+=========================================+===========================================+
| AnimatedSprite                          | AnimatedSprite2D                          |
+-----------------------------------------+-------------------------------------------+
| ARVRCamera                              | XRCamera3D                                |
+-----------------------------------------+-------------------------------------------+
| ARVRController                          | XRController3D                            |
+-----------------------------------------+-------------------------------------------+
| ARVRAnchor                              | XRAnchor3D                                |
+-----------------------------------------+-------------------------------------------+
| ARVRInterface                           | XRInterface                               |
+-----------------------------------------+-------------------------------------------+
| ARVROrigin                              | XROrigin3D                                |
+-----------------------------------------+-------------------------------------------+
| ARVRPositionalTracker                   | XRPositionalTracker                       |
+-----------------------------------------+-------------------------------------------+
| ARVRServer                              | XRServer                                  |
+-----------------------------------------+-------------------------------------------+
| BoxShape                                | BoxShape3D                                |
+-----------------------------------------+-------------------------------------------+
| CapsuleShape                            | CapsuleShape3D                            |
+-----------------------------------------+-------------------------------------------+
| CubeMesh                                | BoxMesh                                   |
+-----------------------------------------+-------------------------------------------+
| EditorSpatialGizmo                      | EditorNode3DGizmo                         |
+-----------------------------------------+-------------------------------------------+
| EditorSpatialGizmoPlugin                | EditorNode3DGizmoPlugin                   |
+-----------------------------------------+-------------------------------------------+
| GIProbe                                 | VoxelGI                                   |
+-----------------------------------------+-------------------------------------------+
| GIProbeData                             | VoxelGIData                               |
+-----------------------------------------+-------------------------------------------+
| GradientTexture                         | GradientTexture1D                         |
+-----------------------------------------+-------------------------------------------+
| KinematicBody                           | CharacterBody3D                           |
+-----------------------------------------+-------------------------------------------+
| KinematicBody2D                         | CharacterBody2D                           |
+-----------------------------------------+-------------------------------------------+
| Light2D                                 | PointLight2D                              |
+-----------------------------------------+-------------------------------------------+
| LineShape2D                             | WorldBoundaryShape2D                      |
+-----------------------------------------+-------------------------------------------+
| Listener                                | AudioListener3D                           |
+-----------------------------------------+-------------------------------------------+
| NavigationMeshInstance                  | NavigationRegion3D                        |
+-----------------------------------------+-------------------------------------------+
| NavigationPolygonInstance               | NavigationRegion2D                        |
+-----------------------------------------+-------------------------------------------+
| Navigation2DServer                      | NavigationServer2D                        |
+-----------------------------------------+-------------------------------------------+
| PanoramaSky                             | Sky                                       |
+-----------------------------------------+-------------------------------------------+
| Particles                               | GPUParticles3D                            |
+-----------------------------------------+-------------------------------------------+
| Particles2D                             | GPUParticles2D                            |
+-----------------------------------------+-------------------------------------------+
| ParticlesMaterial                       | ParticleProcessMaterial                   |
+-----------------------------------------+-------------------------------------------+
| Physics2DDirectBodyState                | PhysicsDirectBodyState2D                  |
+-----------------------------------------+-------------------------------------------+
| Physics2DDirectSpaceState               | PhysicsDirectSpaceState2D                 |
+-----------------------------------------+-------------------------------------------+
| Physics2DServer                         | PhysicsServer2D                           |
+-----------------------------------------+-------------------------------------------+
| Physics2DShapeQueryParameters           | PhysicsShapeQueryParameters2D             |
+-----------------------------------------+-------------------------------------------+
| Physics2DTestMotionResult               | PhysicsTestMotionResult2D                 |
+-----------------------------------------+-------------------------------------------+
| PlaneShape                              | WorldBoundaryShape3D                      |
+-----------------------------------------+-------------------------------------------+
| Position2D                              | Marker2D                                  |
+-----------------------------------------+-------------------------------------------+
| Position3D                              | Marker3D                                  |
+-----------------------------------------+-------------------------------------------+
| ProceduralSky                           | Sky                                       |
+-----------------------------------------+-------------------------------------------+
| RayShape                                | SeparationRayShape3D                      |
+-----------------------------------------+-------------------------------------------+
| RayShape2D                              | SeparationRayShape2D                      |
+-----------------------------------------+-------------------------------------------+
| ShortCut                                | Shortcut                                  |
+-----------------------------------------+-------------------------------------------+
| Spatial                                 | Node3D                                    |
+-----------------------------------------+-------------------------------------------+
| SpatialGizmo                            | Node3DGizmo                               |
+-----------------------------------------+-------------------------------------------+
| SpatialMaterial                         | StandardMaterial3D                        |
+-----------------------------------------+-------------------------------------------+
| Sprite                                  | Sprite2D                                  |
+-----------------------------------------+-------------------------------------------+
| StreamTexture                           | CompressedTexture2D                       |
+-----------------------------------------+-------------------------------------------+
| TextureProgress                         | TextureProgressBar                        |
+-----------------------------------------+-------------------------------------------+
| VideoPlayer                             | VideoStreamPlayer                         |
+-----------------------------------------+-------------------------------------------+
| ViewportContainer                       | SubViewportContainer                      |
+-----------------------------------------+-------------------------------------------+
| Viewport                                | SubViewport                               |
+-----------------------------------------+-------------------------------------------+
| VisibilityEnabler                       | VisibleOnScreenEnabler3D                  |
+-----------------------------------------+-------------------------------------------+
| VisibilityNotifier                      | VisibleOnScreenNotifier3D                 |
+-----------------------------------------+-------------------------------------------+
| VisibilityNotifier2D                    | VisibleOnScreenNotifier2D                 |
+-----------------------------------------+-------------------------------------------+
| VisibilityNotifier3D                    | VisibleOnScreenNotifier3D                 |
+-----------------------------------------+-------------------------------------------+
| VisualServer                            | RenderingServer                           |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarConstant          | VisualShaderNodeFloatConstant             |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarFunc              | VisualShaderNodeFloatFunc                 |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarOp                | VisualShaderNodeFloatOp                   |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarClamp             | VisualShaderNodeClamp                     |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorClamp             | VisualShaderNodeClamp                     |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarInterp            | VisualShaderNodeMix                       |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorInterp            | VisualShaderNodeMix                       |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorScalarMix         | VisualShaderNodeMix                       |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarSmoothStep        | VisualShaderNodeSmoothStep                |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorSmoothStep        | VisualShaderNodeSmoothStep                |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorScalarSmoothStep  | VisualShaderNodeSmoothStep                |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorScalarStep        | VisualShaderNodeStep                      |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarSwitch            | VisualShaderNodeSwitch                    |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarTransformMult     | VisualShaderNodeTransformOp               |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarDerivativeFunc    | VisualShaderNodeDerivativeFunc            |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVectorDerivativeFunc    | VisualShaderNodeDerivativeFunc            |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeBooleanUniform          | VisualShaderNodeBooleanParameter          |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeColorUniform            | VisualShaderNodeColorParameter            |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeScalarUniform           | VisualShaderNodeFloatParameter            |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeCubeMapUniform          | VisualShaderNodeCubeMapParameter          |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeTextureUniform          | VisualShaderNodeTexture2DParameter        |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeTextureUniformTriplanar | VisualShaderNodeTextureParameterTriplanar |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeTransformUniform        | VisualShaderNodeTransformParameter        |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeVec3Uniform             | VisualShaderNodeVec3Parameter             |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeUniform                 | VisualShaderNodeParameter                 |
+-----------------------------------------+-------------------------------------------+
| VisualShaderNodeUniformRef              | VisualShaderNodeParameterRef              |
+-----------------------------------------+-------------------------------------------+

.. _doc_upgrading_to_godot_4_manual_rename:

Đổi tên thủ công các phương thức, thuộc tính, signal và hằng số
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Do cách hoạt động của công cụ nâng cấp dự án, không phải tất cả
các lần đổi tên :abbr:`API (Application Programming Interface)` đều có thể được thực hiện tự động. Danh sách dưới đây bao gồm tất cả các lần đổi tên phải được thực hiện thủ công bằng script editor.

Nếu bạn không tìm thấy node hoặc resource trong danh sách dưới đây, hãy tham khảo bảng trên để tìm tên mới của chúng.

.. tip::

    Bạn có thể sử dụng hộp thoại **Replace in Files** để tăng tốc việc thay thế bằng cách nhấn
    :kbd:`Ctrl + Shift + R` khi script editor đang mở. Tuy nhiên, hãy cẩn thận vì hộp thoại Replace in Files không cung cấp cách nào để hoàn tác thao tác thay thế. Hãy sử dụng version control để thường xuyên commit công việc nâng cấp của bạn. Bạn cũng có thể sử dụng các công cụ dòng lệnh như `sd <https://github.com/chmln/sd>`__ nếu cần một công cụ linh hoạt hơn hộp thoại Replace in Files của editor.

    Nếu sử dụng C#, hãy nhớ tìm các cách sử dụng API lỗi thời với ký hiệu PascalCase trong dự án (và thực hiện việc thay thế cũng bằng ký hiệu PascalCase).

**Các phương thức**

- Các lớp File và Directory đã được thay thế bằng :ref:`class_FileAccess` và
  :ref:`class_DirAccess`, vốn có API hoàn toàn khác. Một số phương thức hiện là static, nghĩa là bạn có thể gọi trực tiếp chúng trên FileAccess hoặc DirAccess mà không cần tạo một instance của lớp đó.
- Các phương thức liên quan đến màn hình và cửa sổ từ singleton :ref:`class_OS` (chẳng hạn như ``OS.get_screen_size()``) đã được chuyển sang singleton :ref:`class_DisplayServer`. Cách đặt tên phương thức cũng được thay đổi để sử dụng dạng ``DisplayServer.<object>_<get/set>_property()``. Ví dụ, ``OS.get_screen_size()`` trở thành ``DisplayServer.screen_get_size()``.
- Các phương thức về thời gian và ngày tháng từ singleton :ref:`class_OS` đã được chuyển sang
  singleton :ref:`class_Time`. (Singleton Time cũng có sẵn trong Godot 3.5 trở lên.)
- Bạn có thể phải thay thế một số lệnh gọi ``instance()`` bằng ``instantiate()``. Bộ chuyển đổi *should* sẽ tự động xử lý việc này, nhưng điều này phụ thuộc vào mã tùy chỉnh và có thể không hoạt động trong 100% trường hợp.
- ``set_autowrap()`` của AcceptDialog hiện là ``set_autowrap_mode()``.
- ``process()`` của AnimationNode hiện được đổi tên thành ``_process()`` (lưu ý dấu gạch dưới ở đầu, biểu thị một virtual method).
- ``add_animation()`` của AnimationPlayer hiện được đổi tên thành ``add_animation_library()`` và hiện sử dụng một :ref:`class_AnimationLibrary`.
- ``set_process_mode()`` của AnimationTree hiện được đổi tên thành ``set_process_callback()``.
- ``empty()`` của Array hiện được đổi tên thành ``is_empty()``.
- ``invert()`` của Array hiện được đổi tên thành ``reverse()``.
- ``remove()`` của Array hiện được đổi tên thành ``remove_at()``.
- ``get_points()`` của AStar2D và AStar3D hiện được đổi tên thành ``get_points_id()``.
- ``set_event()`` của BaseButton hiện được đổi tên thành ``set_shortcut()``.
- ``get_h_offset()`` của Camera2D hiện được đổi tên thành ``get_drag_horizontal_offset()``.
- ``get_v_offset()`` của Camera2D hiện được đổi tên thành ``get_drag_vertical_offset()``.
- ``set_h_offset()`` của Camera2D hiện được đổi tên thành ``set_drag_horizontal_offset()``.
- ``set_v_offset()`` của Camera2D hiện được đổi tên thành ``set_drag_vertical_offset()``.
- ``raise()`` của CanvasItem hiện được đổi tên thành ``move_to_front()``.
- ``update()`` của CanvasItem hiện được đổi tên thành ``queue_redraw()``.
- ``get_stylebox()`` của Control hiện được đổi tên thành ``get_theme_stylebox()``.
- ``set_tooltip()`` của Control hiện được đổi tên thành ``set_tooltip_text()``.
- ``create_gizmo()`` của EditorNode3DGizmoPlugin hiện được đổi tên thành ``_create_gizmo()`` (lưu ý dấu gạch dưới ở đầu, biểu thị một virtual method).
- ``get_peer_port()`` của ENetMultiplayerPeer hiện được đổi tên thành ``get_peer()``.
- ``get_mode()`` của FileDialog hiện được đổi tên thành ``get_file_mode()``.
- ``set_mode()`` của FileDialog hiện được đổi tên thành ``set_file_mode()``.
- ``get_offset()`` của GraphNode hiện được đổi tên thành ``get_position_offset()``.
- ``map_to_world()`` của GridMap hiện được đổi tên thành ``map_to_local()``.
- ``world_to_map()`` của GridMap hiện được đổi tên thành ``local_to_map()``.
- ``get_rect()`` của Image hiện được đổi tên thành ``get_region()``.
- ``set_normal()`` của ImmediateGeometry hiện được đổi tên thành ``surface_set_normal()``.
- ``set_color()`` của ImmediateMesh hiện được đổi tên thành ``surface_set_color()``.
- ``set_uv()`` của ImmediateMesh hiện được đổi tên thành ``surface_set_uv()``.
- ``get_v_scroll()`` của ItemList hiện được đổi tên thành ``get_v_scroll_bar()``.
- ``get_network_connected_peers()`` của MultiPlayerAPI hiện được đổi tên thành ``get_peers()``.
- ``get_network_peer()`` của MultiPlayerAPI hiện được đổi tên thành ``get_peer()``.
- ``get_network_unique_id()`` của MultiPlayerAPI hiện được đổi tên thành ``get_unique_id()``.
- ``has_network_peer()`` của MultiPlayerAPI hiện được đổi tên thành ``has_multiplayer_peer()``.
- ``is_refusing_new_network_connections()`` của MultiplayerAPI hiện được đổi tên thành ``is_refusing_new_connections()``.
- ``is_listening()`` của PacketPeerUDP hiện được đổi tên thành ``is_bound()``.
- ``listen()`` của PacketPeerUDP hiện được đổi tên thành ``bind()``.
- ``set_flag()`` của ParticleProcessMaterial hiện được đổi tên thành ``set_particle_flag()``.
- ``get_motion()`` của PhysicsTestMotionResult2D hiện được đổi tên thành ``get_travel()``.
- ``get_render_info()`` của RenderingServer hiện được đổi tên thành ``get_rendering_info()``.
- ``get_dependencies()`` của ResourceFormatLoader hiện được đổi tên thành ``_get_dependencies()`` (lưu ý dấu gạch dưới ở đầu, biểu thị một virtual method).
- ``load()`` của ResourceFormatLoader hiện được đổi tên thành ``_load()``.
- ``change_scene()`` của SceneTree hiện được đổi tên thành ``change_scene_to_file()``.
- ``is_valid()`` của Shortcut hiện được đổi tên thành ``has_valid_event()``.
- ``map_to_world()`` của TileMap hiện được đổi tên thành ``map_to_local()``.
- ``world_to_map()`` của TileMap hiện được đổi tên thành ``local_to_map()``.
- ``xform()`` của Transform2D là ``mat * vec`` và ``xform_inv()`` là ``vec * mat``.
- ``get_name()`` của XRPositionalTracker hiện được đổi tên thành ``get_tracker_name()``.
- ``get_type()`` của XRPositionalTracker hiện được đổi tên thành ``get_tracker_type()``.
- ``_set_name()`` của XRPositionalTracker hiện được đổi tên thành ``get_tracker_name()``.


**Các thuộc tính**

.. note::

    Nếu một thuộc tính được liệt kê ở đây, các phương thức getter và setter liên kết với thuộc tính đó cũng phải được đổi tên thủ công nếu được sử dụng trong project. Ví dụ, ``set_offset()`` và ``get_offset()`` của PathFollow2D và PathFollow3D lần lượt phải được đổi tên thành ``set_progress()`` và ``get_progress()``.

- ``device`` của AudioServer hiện được đổi tên thành ``output_device``.
- ``group`` của BaseButton hiện được đổi tên thành ``button_group``.
- ``zfar`` của Camera3D hiện được đổi tên thành ``far``.
- ``znear`` của Camera3D hiện là ``near``
- ``margin`` của Control hiện là ``offset``.
- ``doubleclick`` của InputEventMouseButton hiện là ``double_click``.
- ``alt`` của InputEventWithModifiers hiện là ``alt_pressed``.
- ``command`` của InputEventWithModifiers hiện là ``command_pressed``.
- ``control`` của InputEventWithModifiers hiện là ``ctrl_pressed``.
- ``meta`` của InputEventWithModifiers hiện là ``meta_pressed``.
- ``shift`` của InputEventWithModifiers hiện là ``shift_pressed``.
- ``percent_visible`` của Label hiện là ``visible_ratio``.
- ``refuse_new_network_connections`` của MultiPlayerAPI hiện là ``refuse_new_connections``.
- ``filename`` của Node hiện là ``scene_file_path``.
- ``rotate`` của PathFollow2D hiện là ``rotates``.
- ``offset`` của PathFollow2D và PathFollow3D hiện là ``progress``.
- ``extents`` của RectangleShape2D hiện là ``size``
- ``percent_visible`` của TextureProgressBar hiện là ``show_percentage``.
- ``off`` của Theme hiện là ``unchecked``.
- ``ofs`` của Theme hiện là ``offset``.
- ``on`` của Theme hiện là ``checked``.
- ``window_title`` của Window hiện là ``title``.
- ``d`` của WorldMarginShape2D hiện là ``distance``.
- Thuộc tính ``extents`` trên các node CSG và VoxelGI sẽ phải được thay thế bằng ``size``, với giá trị được đặt giảm một nửa (vì chúng không còn là half-extents). Điều này cũng ảnh hưởng đến các phương thức setter/getter ``set_extents()`` và ``get_extents()`` của thuộc tính này.
- Thuộc tính ``Engine.editor_hint`` đã bị loại bỏ để dùng phương thức ``Engine.is_editor_hint()`` *method* thay thế. Lý do là thuộc tính này chỉ có thể đọc, trong khi các thuộc tính trong Godot không được dùng cho các giá trị chỉ đọc.


**Enums**

- ``FLAG_MAX`` của CPUParticles2D hiện là ``PARTICLE_FLAG_MAX``.

**Signals**

- ``instantiate`` của FileSystemDock hiện là ``instance``.
- ``hide`` của CanvasItem hiện là ``hidden``. Việc đổi tên này **không** áp dụng cho phương thức ``hide()``, mà chỉ áp dụng cho signal.
- ``tween_all_completed`` của Tween hiện là ``loop_finished``.
- ``changed`` của EditorSettings hiện là ``settings_changed``.

**Constants**

- Tên màu hiện được viết hoa và sử dụng dấu gạch dưới giữa các từ. Ví dụ: ``Color.palegreen`` hiện là ``Color.PALE_GREEN``.
- Các hằng số ``NOTIFICATION_`` của MainLoop đã được sao chép sang ``Node``, nghĩa là bạn có thể xóa tiền tố ``MainLoop.`` khi tham chiếu đến chúng.
- ``NOTIFICATION_WM_QUIT_REQUEST`` của MainLoop hiện là ``NOTIFICATION_WM_CLOSE_REQUEST``.

Kiểm tra cài đặt dự án
~~~~~~~~~~~~~~~~~~~~~~

Một số cài đặt dự án đã được đổi tên, và một số trong đó có enum được thay đổi theo cách không tương thích (chẳng hạn như chất lượng bộ lọc bóng đổ). Điều này có nghĩa là bạn có thể cần đặt lại giá trị của một số cài đặt dự án. Hãy đảm bảo bật nút chuyển **Advanced** trong hộp thoại cài đặt dự án để có thể xem tất cả cài đặt dự án.

Kiểm tra cài đặt Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các cài đặt chất lượng đồ họa đã được chuyển từ thuộc tính Environment sang cài đặt dự án. Việc này giúp điều chỉnh chất lượng trong runtime dễ dàng hơn mà không cần truy cập tài nguyên Environment hiện đang hoạt động rồi sửa đổi các thuộc tính của nó.

Do đó, bạn sẽ phải cấu hình các cài đặt chất lượng Environment trong cài đặt dự án, vì các cài đặt chất lượng Environment cũ không được tự động chuyển đổi sang cài đặt dự án.

Nếu bạn có menu cài đặt đồ họa đã thay đổi các thuộc tính environment trong Godot 3.x, bạn sẽ phải thay đổi code của menu này để gọi các phương thức :ref:`class_RenderingServer` tác động đến chất lượng của các hiệu ứng environment. Chỉ nút chuyển "base" của mỗi hiệu ứng environment và các điều khiển trực quan của hiệu ứng đó vẫn nằm trong tài nguyên Environment.

Cập nhật shader
~~~~~~~~~~~~~~~

Shader đã có một số thay đổi không được công cụ nâng cấp xử lý. Bạn sẽ cần thực hiện một số thay đổi thủ công, đặc biệt nếu shader của bạn sử dụng các phép biến đổi không gian tọa độ hoặc một hàm ``light()`` tùy chỉnh.

Phần mở rộng tệp ``.shader`` không còn được hỗ trợ, nghĩa là bạn phải đổi tên các tệp ``.shader`` thành ``.gdshader`` và cập nhật các tham chiếu tương ứng trong các tệp scene/resource bằng trình soạn thảo văn bản bên ngoài.

Một số thay đổi đáng chú ý bạn cần thực hiện trong shader là:

- Các chế độ lọc và lặp texture hiện được đặt trên từng uniform riêng lẻ, thay vì trên chính các tệp texture.
- ``hint_albedo`` hiện là ``source_color``.
- ``hint_color`` hiện là ``source_color``.
- :ref:`Built in matrix variables were renamed. <doc_spatial_shader>`
- Shader particle không còn sử dụng hàm xử lý ``vertex()``. Thay vào đó, chúng sử dụng ``start()`` và ``process()``.
- Trong các renderer Forward+ và Mobile, tọa độ thiết bị chuẩn hóa hiện có phạm vi Z là ``[0.0,1.0]`` thay vì ``[-1.0,1.0]``. Khi tái tạo NDC từ ``SCREEN_UV`` và độ sâu, hãy dùng ``vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);`` thay vì ``vec3 ndc = vec3(SCREEN_UV, depth) * 2.0 - 1.0;``. Renderer Compatibility không thay đổi, vẫn sử dụng phạm vi Z của NDC như trong 3.x.
- Mô hình chiếu sáng đã thay đổi. Nếu shader của bạn có hàm ``light()`` tùy chỉnh, bạn có thể cần thay đổi để đạt được kết quả hiển thị tương tự.
- Trong phiên bản 4.3 trở lên, kỹ thuật bộ đệm độ sâu Z đảo ngược hiện đã được triển khai, điều này có thể làm hỏng các shader nâng cao. Hãy xem `Giới thiệu về Z đảo ngược (CÒN GỌI LÀ Xin lỗi vì đã làm hỏng shader của bạn) <https://godotengine.org/article/introducing-reverse-z/>`__.

Xem :ref:`doc_shading_language` để biết thêm thông tin.

Danh sách này không đầy đủ. Nếu bạn đã thực hiện tất cả thay đổi được đề cập ở đây mà shader vẫn không hoạt động, hãy thử yêu cầu trợ giúp trong một trong các `kênh cộng đồng <https://godotengine.org/community/>`__.

Cập nhật script để tính đến các thay đổi không tương thích ngược
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một số thay đổi được thực hiện giữa Godot 3.x và 4 không phải là đổi tên, nhưng vẫn phá vỡ khả năng tương thích ngược do hành vi mặc định khác nhau.

Các ví dụ đáng chú ý nhất là:

- Các hàm vòng đời như ``_ready()`` và ``_process()`` không còn ngầm gọi các hàm của lớp cha có cùng tên. Thay vào đó, bạn phải sử dụng ``super()`` ở đầu hàm vòng đời trong lớp con để hàm của lớp cha được gọi trước.
- Cả :ref:`class_String` và :ref:`class_StringName` hiện đã được cung cấp cho GDScript. Điều này cho phép tối ưu hóa tốt hơn, vì StringName được thiết kế riêng để dùng cho các chuỗi "hằng" được tạo một lần và tái sử dụng nhiều lần. Các kiểu này không hoàn toàn tương đương nhau, có nghĩa là ``is_same("example", &"example")`` trả về ``false``. Mặc dù trong hầu hết trường hợp chúng có thể thay thế cho nhau (``"example" == &"example"`` trả về ``true``), đôi khi bạn có thể phải thay ``"example"`` bằng ``&"example"``.
- :ref:`Cú pháp setter và getter của GDScript <doc_gdscript_basics_setters_getters>` đã thay đổi, nhưng công cụ chuyển đổi chỉ chuyển đổi một phần cú pháp này. Trong hầu hết trường hợp, cần thực hiện thay đổi thủ công để setter và getter hoạt động trở lại.
- :ref:`Cú pháp kết nối signal của GDScript <doc_gdscript_signals>` đã thay đổi. Công cụ chuyển đổi sẽ sử dụng cú pháp dựa trên chuỗi, vẫn còn được hỗ trợ trong Godot 4, nhưng bạn nên chuyển sang cú pháp dựa trên :ref:`class_Signal` được mô tả ở trang liên kết. Nhờ đó, chuỗi không còn được sử dụng, tránh các vấn đề về lỗi tên signal mà chỉ có thể phát hiện trong runtime.
- Các script tích hợp là :ref:`tool script <doc_running_code_in_the_editor>` không được chuyển đổi từ từ khóa ``tool`` sang annotation ``@tool``.
- Node Tween đã bị loại bỏ để thay thế bằng Tweeners, vốn cũng có trong Godot 3.5 trở lên. Xem `pull request ban đầu <https://github.com/godotengine/godot/pull/41794>`__ để biết chi tiết.
- ``randomize()`` hiện được tự động gọi khi tải project, vì vậy để có tính ngẫu nhiên xác định được với instance RandomNumberGenerator toàn cục, bạn phải tự đặt seed trong hàm ``_ready()`` của script.
- ``call_group()``, ``set_group()`` và ``notify_group()`` hiện mặc định được thực thi ngay lập tức. Nếu gọi một hàm tốn nhiều chi phí, điều này có thể gây giật khi sử dụng trên một group chứa số lượng lớn node. Để sử dụng các lời gọi deferred như trước, hãy thay ``call_group(...)`` bằng ``call_group_flags(SceneTree.GROUP_CALL_DEFERRED, ...)`` (và thực hiện tương tự với ``set_group()`` và ``notify_group()``).
- Thay vì ``rotation_degrees``, thuộc tính ``rotation`` được hiển thị trong editor và tự động hiển thị dưới dạng độ trong dock Inspector. Điều này có thể làm hỏng animation, vì công cụ chuyển đổi không tự động xử lý việc chuyển đổi.
- :ref:`class_AABB`'s ``has_no_surface()`` đã được đảo ngược và đổi tên thành ``has_surface()``.
- :ref:`class_AABB` và :ref:`class_Rect2`'s ``has_no_area()`` đã được đảo ngược và đổi tên thành ``has_area()``.
- Thuộc tính ``fps`` của :ref:`class_AnimatedTexture` đã được thay thế bằng ``speed_scale``, hoạt động giống như thuộc tính ``playback_speed`` của AnimationPlayer.
- :ref:`class_AnimatedSprite2D` và :ref:`class_AnimatedSprite3D` hiện cho phép các giá trị ``speed_scale`` âm. Điều này có thể làm hỏng animation nếu bạn dựa vào việc ``speed_scale`` được ngầm giới hạn trong ``0.0``.
- Thuộc tính ``playing`` của :ref:`class_AnimatedSprite2D` và :ref:`class_AnimatedSprite3D` đã bị loại bỏ. Thay vào đó, hãy sử dụng phương thức ``play()``/``stop()`` HOẶC cấu hình animation ``autoplay`` thông qua panel SpriteFrames ở dưới cùng (nhưng không sử dụng cả hai cùng lúc).
- Tham số thứ hai (``end``) của :ref:`class_Array`'s ``slice()`` hiện là *exclusive*, thay vì inclusive. Ví dụ, điều này có nghĩa là ``[1, 2, 3].slice(0, 1)`` hiện trả về ``[1]`` thay vì ``[1, 2]``.
- Các signal của :ref:`class_BaseButton` hiện là ``button_up`` và ``button_down``. Thuộc tính ``pressed`` hiện là ``button_pressed``.
- Thuộc tính ``rotating`` của :ref:`class_Camera2D` đã được thay thế bằng ``ignore_rotation``, có hành vi đảo ngược.
- Thuộc tính ``zoom`` của Camera2D đã được đảo ngược: các giá trị cao hơn hiện phóng to hơn thay vì thu nhỏ hơn.
- Phương thức ``remove_and_skip()`` của :ref:`class_Node` đã bị loại bỏ. Nếu cần triển khai lại phương thức này trong script, bạn có thể dùng `triển khai C++ cũ <https://github.com/godotengine/godot/blob/7936b3cc4c657e4b273b376068f095e1e0e4d82a/scene/main/node.cpp#L1910-L1945>`__ làm tài liệu tham khảo.
- ``OS.get_system_time_secs()`` nên được chuyển đổi thành ``Time.get_time_dict_from_system()["second"]``.
- Phương thức ``save()`` của :ref:`class_ResourceSaver` hiện đã hoán đổi thứ tự các đối số (``resource: Resource, path: String``). Điều này cũng áp dụng cho
  phương thức ``_save()`` của :ref:`class_ResourceFormatSaver`.
- Một :ref:`class_StreamPeerTCP` phải được gọi ``poll()`` để cập nhật trạng thái, thay vì dựa vào việc ``get_status()`` tự động polling: `GH-59582 <https://github.com/godotengine/godot/pull/59582>`__
- Phương thức ``right()`` của :ref:`class_String` `đã thay đổi hành vi <https://github.com/godotengine/godot/pull/36180>`__: hiện trả về số ký tự tính từ bên phải của chuỗi, thay vì phần bên phải của chuỗi tính từ một vị trí cho trước. Nếu cần hành vi cũ, bạn có thể sử dụng ``substr()`` thay thế.
- ``is_connected_to_host()`` đã bị loại bỏ khỏi StreamPeerTCP và PacketPeerUDP theo `GH-59582 <https://github.com/godotengine/godot/pull/59582>`__. Có thể sử dụng ``get_status()`` thay thế trong StreamPeerTCP. Có thể sử dụng ``is_socket_connected()`` thay thế trong :ref:`class_PacketPeerUDP`.
- Trong ``_get_property_list()``, chuỗi gợi ý thuộc tính ``or_lesser`` hiện là ``or_less``.
- Trong ``_get_property_list()``, chuỗi gợi ý thuộc tính ``noslider`` hiện là ``no_slider``.
- VisualShaderNodeVec4Parameter hiện nhận :ref:`class_Vector4` làm tham số thay vì :ref:`class_Quaternion`.

**Các node/resource đã bị loại bỏ hoặc thay thế**

Danh sách này bao gồm tất cả các node đã được thay thế bằng một node khác yêu cầu cấu hình khác. Bạn phải thiết lập lại từ đầu, vì công cụ chuyển đổi dự án không hỗ trợ cập nhật các thiết lập hiện có:

+---------------------+-----------------------+----------------------------------------------------------------------------+
| Removed node        | Closest approximation | Comment                                                                    |
+=====================+=======================+============================================================================+
| AnimationTreePlayer | AnimationTree         | AnimationTreePlayer was deprecated since Godot 3.1.                        |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| BakedLightmap       | LightmapGI            | See :ref:`doc_using_lightmap_gi`.                                          |
+---------------------+-----------------------+                                                                            |
| BakedLightmapData   | LightmapGIData        |                                                                            |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| BitmapFont          | FontFile              | See :ref:`doc_gui_using_fonts`.                                            |
+---------------------+-----------------------+                                                                            |
| DynamicFont         | FontFile              |                                                                            |
+---------------------+-----------------------+                                                                            |
| DynamicFontData     | FontFile              |                                                                            |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| ClippedCamera       | Camera2D or Camera3D  | Camera's pyramid shape was moved to :ref:`class_Camera3D`.                 |
+---------------------+-----------------------+                                                                            |
| InterpolatedCamera  | Camera2D or Camera3D  |                                                                            |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| Navigation2D        | Node2D                | Replaced by :ref:`other 2D Navigation nodes <doc_navigation_overview_2d>`. |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| Navigation3D        | Node3D                | Replaced by :ref:`other 3D Navigation nodes <doc_navigation_overview_3d>`. |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| OpenSimplexNoise    | FastNoiseLite         | Has different parameters and more noise types such as cellular. No         |
|                     |                       | support for 4D noise as it's absent from the FastNoiseLite library.        |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| ToolButton          | Button                | ToolButton was Button with the **Flat** property enabled by default.       |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| YSort               | Node2D or Control     | CanvasItem has a new **Y Sort Enabled** property in 4.0.                   |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| ProximityGroup      | Node3D                | :ref:`class_VisibleOnScreenNotifier3D` can act as a replacement.           |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| Portal              | Node3D                | Portal and room occlusion culling was replaced by raster                   |
|                     |                       | :ref:`occlusion culling <doc_occlusion_culling>`                           |
|                     |                       | (OccluderInstance3D node), which requires a different setup process.       |
+---------------------+-----------------------+                                                                            |
| Room                | Node3D                |                                                                            |
+---------------------+-----------------------+                                                                            |
| RoomManager         | Node3D                |                                                                            |
+---------------------+-----------------------+                                                                            |
| RoomGroup           | Node3D                |                                                                            |
+---------------------+-----------------------+----------------------------------------------------------------------------+
| Occluder            | Node3D                | Geometry occlusion culling was replaced by raster                          |
|                     |                       | :ref:`occlusion culling <doc_occlusion_culling>`                           |
|                     |                       | (OccluderInstance3D node), which requires a different setup process.       |
+---------------------+-----------------------+                                                                            |
| OccluderShapeSphere | Resource              |                                                                            |
+---------------------+-----------------------+----------------------------------------------------------------------------+

Khi tải một dự án cũ, node sẽ tự động được thay thế bằng *phương án gần đúng nhất* (ngay cả khi không sử dụng công cụ nâng cấp dự án).

**Các thay đổi về threading**

Các API :ref:`threading <doc_using_multiple_threads>` đã thay đổi trong 4.0. Ví dụ: đoạn mã sau trong Godot 3.x phải được sửa đổi để hoạt động trong 4.0:

::

    # 3.x
    var start_success = new_thread.start(self, "__threaded_background_loader",
        [resource_path, thread_num]
    )

    # 4.0
    var start_success = new_thread.start(__threaded_background_loader.bind(resource_path, thread_num))

``Thread.is_active()`` không còn được sử dụng và nên được chuyển đổi thành ``Thread.is_alive()``.

.. seealso::

    Xem `changelog <https://github.com/godotengine/godot/blob/master/CHANGELOG.md>`__ để biết danh sách đầy đủ các thay đổi giữa Godot 3.x và 4.

Sự cố phá vỡ khả năng tương thích của resource ArrayMesh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn đã lưu một resource ArrayMesh vào tệp ``.res`` hoặc ``.tres``, định dạng được sử dụng trong 4.0 không tương thích với định dạng được sử dụng trong 3.x. Bạn sẽ cần thực hiện lại quy trình import tệp mesh nguồn và lưu lại dưới dạng resource ArrayMesh.

Danh sách các method, property, signal và constant được tự động đổi tên
-----------------------------------------------------------------------

Tệp mã nguồn `editor/project_upgrade/renames_map_3_to_4.cpp <https://github.com/godotengine/godot/blob/master/editor/project_upgrade/renames_map_3_to_4.cpp>`__ liệt kê tất cả các tên được tự động đổi bởi công cụ nâng cấp dự án. Các dòng được chú thích đề cập đến những lần đổi tên API mà :ref:`không thể thực hiện tự động <doc_upgrading_to_godot_4_manual_rename>`.

Chuyển các thiết lập editor
---------------------------

Godot 3.x và 4.0 sử dụng các tệp thiết lập editor khác nhau. Điều này có nghĩa là bạn có thể thay đổi các thiết lập của chúng độc lập với nhau.

Nếu muốn chuyển các thiết lập Godot 3.x sang Godot 4, hãy mở
:ref:`thư mục thiết lập editor <doc_data_paths_editor_data_paths>` và sao chép ``editor_settings-3.tres`` vào ``editor_settings-4.tres`` khi editor Godot 4 đã đóng.

.. note::

    Tên và danh mục của nhiều thiết lập đã thay đổi kể từ Godot 3.x. Các thiết lập editor có tên hoặc danh mục đã thay đổi sẽ không được chuyển sang Godot 4.0; bạn sẽ phải đặt lại các giá trị của chúng.


Cập nhật các thiết lập kiểm soát phiên bản
------------------------------------------

Godot 3.x và 4.x có các danh sách tệp và thư mục hoàn toàn khác nhau cần được bỏ qua bởi :ref:`hệ thống kiểm soát phiên bản <doc_version_control_systems>` của bạn.
