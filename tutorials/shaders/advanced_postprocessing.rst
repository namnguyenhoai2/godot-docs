.. _doc_advanced_postprocessing:

Hậu xử lý nâng cao
==================

Giới thiệu
----------

Tutorial này mô tả một phương pháp nâng cao để thực hiện hậu xử lý trong Godot. Cụ thể, tutorial sẽ giải thích cách viết một post-processing shader sử dụng depth buffer. Bạn nên làm quen với hậu xử lý nói chung, đặc biệt là các phương pháp được nêu trong :ref:`tutorial hậu xử lý tùy chỉnh <doc_custom_postprocessing>`.

Quad toàn màn hình
------------------

Một cách để tạo các hiệu ứng hậu xử lý tùy chỉnh là sử dụng viewport. Tuy nhiên, việc sử dụng Viewport có hai nhược điểm chính:

1. Không thể truy cập depth buffer
2. Hiệu ứng của post-processing shader không hiển thị trong editor

Để khắc phục hạn chế khi sử dụng depth buffer, hãy dùng :ref:`MeshInstance3D <class_MeshInstance3D>` với primitive :ref:`QuadMesh <class_QuadMesh>`. Cách này cho phép chúng ta sử dụng shader và truy cập depth texture của scene. Tiếp theo, hãy dùng vertex shader để quad luôn phủ kín màn hình, nhờ đó hiệu ứng hậu xử lý sẽ luôn được áp dụng, kể cả trong editor.

Trước tiên, hãy tạo một MeshInstance3D mới và đặt mesh của nó thành QuadMesh. Thao tác này tạo một quad nằm giữa vị trí ``(0, 0, 0)`` với chiều rộng và chiều cao là ``1``. Đặt chiều rộng và chiều cao thành ``2`` và bật **Flip Faces**. Hiện tại, quad chiếm một vị trí trong world space tại gốc tọa độ. Tuy nhiên, chúng ta muốn nó di chuyển cùng camera để luôn phủ kín toàn bộ màn hình. Để làm điều này, chúng ta sẽ bỏ qua các phép biến đổi tọa độ chuyển đổi vị trí vertex qua các coordinate space khác nhau và coi các vertex như thể chúng đã ở trong clip space.

Vertex shader yêu cầu các tọa độ đầu ra nằm trong clip space, với tọa độ chạy từ ``-1`` ở bên trái và phía dưới màn hình đến ``1`` ở phía trên và bên phải màn hình. Đây là lý do QuadMesh cần có chiều cao và chiều rộng là ``2``. Godot xử lý ngầm việc biến đổi từ model space sang view space rồi sang clip space, vì vậy chúng ta cần vô hiệu hóa tác động của các phép biến đổi do Godot thực hiện. Chúng ta làm điều này bằng cách đặt ``POSITION`` built-in thành vị trí mong muốn. ``POSITION`` bỏ qua các phép biến đổi built-in và đặt trực tiếp vị trí vertex trong clip space.

.. code-block:: glsl

  shader_type spatial;
  // Ngăn quad bị ảnh hưởng bởi ánh sáng và sương mù. Điều này cũng cải thiện hiệu năng.
  render_mode unshaded, fog_disabled;

  void vertex() {
    POSITION = vec4(VERTEX.xy, 1.0, 1.0);
  }

.. note:: Trong các phiên bản Godot trước 4.3, đoạn mã này được khuyến nghị sử dụng ``POSITION = vec4(VERTEX, 1.0);``, ngầm giả định rằng mặt phẳng gần của clip space nằm tại ``0.0``. Đoạn mã đó hiện không còn đúng và sẽ không hoạt động trong các phiên bản 4.3+ vì hiện nay chúng ta sử dụng depth buffer "reversed-z", trong đó mặt phẳng gần nằm tại ``1.0``.

Ngay cả với vertex shader này, quad vẫn tiếp tục biến mất. Nguyên nhân là frustum culling, được thực hiện trên CPU. Frustum culling sử dụng ma trận camera và AABB của các Mesh để xác định Mesh có hiển thị hay không *trước khi* truyền nó đến GPU. CPU không biết chúng ta đang làm gì với các vertex, nên giả định các tọa độ được chỉ định là vị trí trong world space, không phải vị trí trong clip space. Điều này khiến Godot loại bỏ quad khi chúng ta quay camera khỏi tâm scene. Để quad không bị loại bỏ, có một số lựa chọn:

1. Thêm QuadMesh làm node con của camera để camera luôn hướng vào nó
2. Đặt thuộc tính Geometry ``extra_cull_margin`` lớn nhất có thể trong QuadMesh

Lựa chọn thứ hai bảo đảm quad hiển thị trong editor, còn lựa chọn thứ nhất bảo đảm quad vẫn hiển thị ngay cả khi camera di chuyển ra ngoài cull margin. Bạn cũng có thể sử dụng cả hai lựa chọn.

Depth texture
-------------

Để đọc depth texture, trước tiên chúng ta cần tạo một texture uniform được đặt thành depth buffer bằng cách sử dụng ``hint_depth_texture``.

.. code-block:: glsl

  uniform sampler2D depth_texture : hint_depth_texture;

Sau khi được định nghĩa, có thể đọc depth texture bằng hàm ``texture()``.

.. code-block:: glsl

  float depth = texture(depth_texture, SCREEN_UV).x;

.. note:: Tương tự như khi truy cập screen texture, chỉ có thể truy cập depth texture khi đọc từ viewport hiện tại. Không thể truy cập depth texture từ một viewport khác mà bạn đã render vào.

Các giá trị do ``depth_texture`` trả về nằm trong khoảng từ ``1.0`` đến ``0.0`` (tương ứng với mặt phẳng gần và xa, theo thứ tự, do sử dụng depth buffer "reverse-z") và là các giá trị phi tuyến tính. Khi hiển thị trực tiếp depth từ ``depth_texture``, mọi thứ sẽ gần như đen hoàn toàn trừ khi ở rất gần, do tính phi tuyến đó. Để làm cho giá trị depth phù hợp với tọa độ world hoặc model, chúng ta cần tuyến tính hóa giá trị này. Khi áp dụng projection matrix vào vị trí vertex, giá trị z trở nên phi tuyến tính. Vì vậy, để tuyến tính hóa, chúng ta nhân nó với ma trận nghịch đảo của projection matrix, có thể truy cập trong Godot bằng biến ``INV_PROJECTION_MATRIX``.

Trước hết, hãy lấy tọa độ trong screen space và biến đổi chúng thành normalized device coordinates (NDC). Khi sử dụng Vulkan backend, NDC chạy từ ``-1.0`` đến ``1.0`` theo hướng ``x`` và ``y``, và từ ``0.0`` đến ``1.0`` theo hướng ``z``. Hãy dựng lại NDC bằng cách sử dụng ``SCREEN_UV`` cho các trục ``x`` và ``y``, còn giá trị depth cho ``z``.


.. code-block:: glsl

  void fragment() {
    float depth = texture(depth_texture, SCREEN_UV).x;
    vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
  }

.. note::

  Tutorial này giả định sử dụng Forward+ hoặc Mobile renderer, cả hai đều dùng Vulkan NDC với Z-range là ``[0.0, 1.0]``. Ngược lại, Compatibility renderer sử dụng OpenGL NDC với Z-range là ``[-1.0, 1.0]``. Đối với Compatibility renderer, hãy thay phép tính NDC bằng đoạn sau:

  .. code-block:: glsl

    vec3 ndc = vec3(SCREEN_UV, depth) * 2.0 - 1.0;

  Bạn cũng có thể sử dụng các built-in define ``CURRENT_RENDERER`` và ``RENDERER_COMPATIBILITY`` để shader hoạt động với mọi renderer:

  .. code-block:: glsl

    #if CURRENT_RENDERER == RENDERER_COMPATIBILITY
    vec3 ndc = vec3(SCREEN_UV, depth) * 2.0 - 1.0;
    #else
    vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
    #endif

Chuyển NDC sang view space bằng cách nhân NDC với ``INV_PROJECTION_MATRIX``. Hãy nhớ rằng view space cung cấp các vị trí tương đối so với camera, vì vậy giá trị ``z`` sẽ cho chúng ta biết khoảng cách đến điểm đó.

.. code-block:: glsl

  void fragment() {
    ...
    vec4 view = INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    view.xyz /= view.w;
    float linear_depth = -view.z;
  }

Vì camera hướng theo hướng ``z`` âm, vị trí sẽ có giá trị ``z`` âm. Để lấy được giá trị depth có thể sử dụng, chúng ta phải đổi dấu ``view.z``.

Có thể dựng vị trí trong world space từ depth buffer bằng đoạn mã sau, sử dụng ``INV_VIEW_MATRIX`` để biến đổi vị trí từ view space sang world space.

.. code-block:: glsl

  void fragment() {
    ...
    vec4 world = INV_VIEW_MATRIX * INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    vec3 world_position = world.xyz / world.w;
  }

Shader ví dụ
------------

Sau khi thêm một dòng để xuất ra ``ALBEDO``, chúng ta có một shader hoàn chỉnh trông như sau. Shader này cho phép bạn trực quan hóa depth tuyến tính hoặc tọa độ trong world space, tùy thuộc vào dòng nào được comment out.

.. code-block:: glsl

  shader_type spatial;
  // Ngăn quad bị ảnh hưởng bởi ánh sáng và sương mù. Điều này cũng cải thiện hiệu năng.
  render_mode unshaded, fog_disabled;

  uniform sampler2D depth_texture : hint_depth_texture;

  void vertex() {
    POSITION = vec4(VERTEX.xy, 1.0, 1.0);
  }

  void fragment() {
    float depth = texture(depth_texture, SCREEN_UV).x;
    vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
    vec4 view = INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    view.xyz /= view.w;
    float linear_depth = -view.z;

    vec4 world = INV_VIEW_MATRIX * INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    vec3 world_position = world.xyz / world.w;

    // Trực quan hóa depth tuyến tính
    ALBEDO.rgb = vec3(fract(linear_depth));

    // Trực quan hóa tọa độ world
    //ALBEDO.rgb = fract(world_position).xyz;
  }

Một tối ưu hóa
--------------

Bạn có thể đạt hiệu quả tốt hơn khi sử dụng một tam giác lớn duy nhất thay vì quad toàn màn hình. Lý do được giải thích `tại đây <https://michaldrobot.com/2014/04/01/gcn-execution-patterns-in-full-screen-passes>`_. Tuy nhiên, lợi ích này khá nhỏ và chỉ đáng kể khi chạy các fragment shader đặc biệt phức tạp.

Đặt Mesh trong MeshInstance3D thành một :ref:`ArrayMesh <class_ArrayMesh>`. ArrayMesh là một công cụ cho phép bạn dễ dàng tạo một Mesh từ các Array dành cho vertex, normal, color, v.v.

Bây giờ, gắn một script vào MeshInstance3D và sử dụng đoạn mã sau:

::

  extends MeshInstance3D

  func _ready():
    # Create a single triangle out of vertices:
    var verts = PackedVector3Array()
    verts.append(Vector3(-1.0, -1.0, 0.0))
    verts.append(Vector3(3.0, -1.0, 0.0))
    verts.append(Vector3(-1.0, 3.0, 0.0))

    # Create an array of arrays.
    # This could contain normals, colors, UVs, etc.
    var mesh_array = []
    mesh_array.resize(Mesh.ARRAY_MAX) #required size for ArrayMesh Array
    mesh_array[Mesh.ARRAY_VERTEX] = verts #position of vertex array in ArrayMesh Array

    # Create mesh from mesh_array:
    mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, mesh_array)

.. note:: Triangle được chỉ định trong tọa độ thiết bị chuẩn hóa. Hãy nhớ rằng NDC chạy từ ``-1.0`` đến ``1.0`` theo cả hai hướng ``x`` và ``y``. Điều này khiến màn hình rộng ``2`` đơn vị và cao ``2`` đơn vị. Để phủ toàn bộ màn hình bằng một triangle duy nhất, hãy sử dụng một triangle rộng ``4`` đơn vị và cao ``4`` đơn vị, tức là gấp đôi chiều cao và chiều rộng.

Gán cùng vertex shader như ở trên và mọi thứ sẽ trông hoàn toàn giống nhau.

Hạn chế duy nhất khi sử dụng ArrayMesh thay cho QuadMesh là ArrayMesh không hiển thị trong editor vì triangle chỉ được tạo khi scene chạy. Để khắc phục điều này, hãy tạo một Mesh dạng triangle duy nhất trong một chương trình modeling rồi sử dụng Mesh đó trong MeshInstance3D.

.. _`here`: https://michaldrobot.com/2014/04/01/gcn-execution-patterns-in-full-screen-passes
