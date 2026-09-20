.. _doc_advanced_postprocessing:

Hậu kỳ nâng cao
===============

Giới thiệu
----------

Tutorial này mô tả một phương pháp nâng cao để thực hiện hậu kỳ trong Godot. Cụ thể, tutorial sẽ giải thích cách viết một post-processing shader sử dụng depth buffer. Bạn nên nắm được những kiến thức cơ bản về hậu kỳ nói chung và đặc biệt là các phương pháp được trình bày trong :ref:`custom post-processing tutorial <doc_custom_postprocessing>`.

Quad toàn màn hình
------------------

Một cách để tạo các hiệu ứng hậu kỳ tùy chỉnh là sử dụng viewport. Tuy nhiên, việc sử dụng Viewport có hai nhược điểm chính:

1. Không thể truy cập depth buffer 2. Hiệu ứng của post-processing shader không hiển thị trong editor

Để khắc phục hạn chế khi sử dụng depth buffer, hãy dùng một :ref:`MeshInstance3D <class_MeshInstance3D>` với primitive :ref:`QuadMesh <class_QuadMesh>`. Điều này cho phép chúng ta sử dụng shader và truy cập depth texture của scene. Tiếp theo, hãy dùng vertex shader để làm cho quad luôn bao phủ màn hình, nhờ đó hiệu ứng hậu kỳ sẽ luôn được áp dụng, kể cả trong editor.

Trước tiên, tạo một MeshInstance3D mới và đặt mesh của nó thành một QuadMesh. Thao tác này tạo một quad nằm giữa tại vị trí ``(0, 0, 0)`` với chiều rộng và chiều cao là ``1``. Đặt chiều rộng và chiều cao thành ``2`` rồi bật **Flip Faces**. Hiện tại, quad chiếm một vị trí trong world space tại gốc tọa độ. Tuy nhiên, chúng ta muốn nó di chuyển theo camera để luôn bao phủ toàn bộ màn hình. Để làm điều này, chúng ta sẽ bỏ qua các phép biến đổi tọa độ chuyển đổi vị trí vertex qua các không gian tọa độ khác nhau và xử lý các vertex như thể chúng đã ở trong clip space.

Vertex shader yêu cầu các tọa độ đầu ra nằm trong clip space, tức là các tọa độ chạy từ ``-1`` ở bên trái và dưới màn hình đến ``1`` ở bên trên và bên phải màn hình. Đây là lý do QuadMesh cần có chiều cao và chiều rộng là ``2``. Godot xử lý ngầm việc biến đổi từ model space sang view space rồi sang clip space, vì vậy chúng ta cần vô hiệu hóa ảnh hưởng của các phép biến đổi của Godot. Chúng ta thực hiện việc này bằng cách đặt built-in ``POSITION`` thành vị trí mong muốn. ``POSITION`` bỏ qua các phép biến đổi built-in và đặt trực tiếp vị trí vertex trong clip space.

.. code-block:: glsl

  shader_type spatial;
  // Ngăn quad bị ảnh hưởng bởi lighting và fog. Điều này cũng cải thiện hiệu năng.
  render_mode unshaded, fog_disabled;

  void vertex() {
    POSITION = vec4(VERTEX.xy, 1.0, 1.0);
  }

.. note:: In versions of Godot earlier than 4.3, this code recommended using ``POSITION = vec4(VERTEX, 1.0);``
          vốn ngầm giả định rằng mặt phẳng near của clip space nằm tại ``0.0``. Đoạn code đó hiện không còn đúng và sẽ không hoạt động trong các phiên bản 4.3+ vì hiện nay chúng ta sử dụng depth buffer "reversed-z", trong đó mặt phẳng near nằm tại ``1.0``.

Ngay cả với vertex shader này, quad vẫn tiếp tục biến mất. Nguyên nhân là frustum culling, được thực hiện trên CPU. Frustum culling sử dụng camera matrix và AABB của các Mesh để xác định Mesh có hiển thị hay không *trước khi* truyền nó đến GPU. CPU không biết chúng ta đang làm gì với các vertex, nên giả định rằng các tọa độ được chỉ định là world position, không phải clip space position. Điều này khiến Godot cull quad khi chúng ta quay khỏi tâm của scene. Để ngăn quad bị cull, có một số lựa chọn:

1. Thêm QuadMesh làm node con của camera để camera luôn hướng vào nó 2. Đặt thuộc tính Geometry ``extra_cull_margin`` ở mức lớn nhất có thể trong QuadMesh

Lựa chọn thứ hai đảm bảo quad hiển thị trong editor, trong khi lựa chọn thứ nhất đảm bảo quad vẫn hiển thị ngay cả khi camera di chuyển ra ngoài cull margin. Bạn cũng có thể sử dụng cả hai lựa chọn.

Depth texture
-------------

Để đọc depth texture, trước tiên chúng ta cần tạo một texture uniform được đặt thành depth buffer bằng cách sử dụng ``hint_depth_texture``.

.. code-block:: glsl

  uniform sampler2D depth_texture : hint_depth_texture;

Sau khi được định nghĩa, có thể đọc depth texture bằng hàm ``texture()``.

.. code-block:: glsl

  float depth = texture(depth_texture, SCREEN_UV).x;

.. note:: Similar to accessing the screen texture, accessing the depth texture is only
          có thể thực hiện khi đọc từ viewport hiện tại. Không thể truy cập depth texture từ một viewport khác mà bạn đã render vào đó.

Các giá trị được trả về bởi ``depth_texture`` nằm trong khoảng từ ``1.0`` đến ``0.0`` (tương ứng với mặt phẳng near và far vì sử dụng depth buffer "reverse-z") và là các giá trị phi tuyến tính. Khi hiển thị trực tiếp depth từ ``depth_texture``, mọi thứ sẽ gần như đen hoàn toàn trừ khi ở rất gần, do tính phi tuyến này. Để làm cho giá trị depth phù hợp với world hoặc model coordinates, chúng ta cần tuyến tính hóa giá trị đó. Khi áp dụng projection matrix lên vị trí vertex, giá trị z trở nên phi tuyến tính; do đó, để tuyến tính hóa nó, chúng ta nhân nó với nghịch đảo của projection matrix, vốn có thể truy cập trong Godot bằng biến ``INV_PROJECTION_MATRIX``.

Trước hết, lấy các tọa độ trong screen space và biến đổi chúng thành normalized device coordinates (NDC). Khi sử dụng Vulkan backend, NDC chạy từ ``-1.0`` đến ``1.0`` theo các hướng ``x`` và ``y``, và từ ``0.0`` đến ``1.0`` theo hướng ``z``. Hãy tái tạo NDC bằng cách sử dụng ``SCREEN_UV`` cho các trục ``x`` và ``y``, cùng giá trị depth cho ``z``.


.. code-block:: glsl

  void fragment() {
    float depth = texture(depth_texture, SCREEN_UV).x;
    vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
  }

.. note::

  Tutorial này giả định sử dụng Forward+ hoặc Mobile renderer, cả hai đều dùng Vulkan NDC với Z-range là ``[0.0, 1.0]``. Ngược lại, Compatibility renderer sử dụng OpenGL NDC với Z-range là ``[-1.0, 1.0]``. Đối với Compatibility renderer, hãy thay phép tính NDC bằng đoạn sau:

  .. code-block:: glsl

    vec3 ndc = vec3(SCREEN_UV, depth) * 2.0 - 1.0;

  Bạn cũng có thể sử dụng các built-in define ``CURRENT_RENDERER`` và ``RENDERER_COMPATIBILITY`` cho một shader hoạt động trên tất cả renderer:

  .. code-block:: glsl

    #if CURRENT_RENDERER == RENDERER_COMPATIBILITY
    vec3 ndc = vec3(SCREEN_UV, depth) * 2.0 - 1.0;
    #else
    vec3 ndc = vec3(SCREEN_UV * 2.0 - 1.0, depth);
    #endif

Chuyển NDC sang view space bằng cách nhân NDC với ``INV_PROJECTION_MATRIX``. Hãy nhớ rằng view space cung cấp các vị trí tương đối so với camera, vì vậy giá trị ``z`` sẽ cho chúng ta khoảng cách đến điểm đó.

.. code-block:: glsl

  void fragment() {
    ...
    vec4 view = INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    view.xyz /= view.w;
    float linear_depth = -view.z;
  }

Vì camera hướng theo hướng ``z`` âm, vị trí sẽ có giá trị ``z`` âm. Để có được giá trị depth có thể sử dụng, chúng ta phải đổi dấu ``view.z``.

Có thể dựng world position từ depth buffer bằng đoạn code sau, sử dụng ``INV_VIEW_MATRIX`` để biến đổi vị trí từ view space sang world space.

.. code-block:: glsl

  void fragment() {
    ...
    vec4 world = INV_VIEW_MATRIX * INV_PROJECTION_MATRIX * vec4(ndc, 1.0);
    vec3 world_position = world.xyz / world.w;
  }

Shader ví dụ
------------

Sau khi thêm một dòng để xuất ra ``ALBEDO``, chúng ta có một shader hoàn chỉnh trông như sau. Shader này cho phép bạn trực quan hóa linear depth hoặc tọa độ world space, tùy thuộc vào dòng nào được comment out.

.. code-block:: glsl

  shader_type spatial;
  // Ngăn quad bị ảnh hưởng bởi lighting và fog. Điều này cũng cải thiện hiệu năng.
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

    // Trực quan hóa linear depth
    ALBEDO.rgb = vec3(fract(linear_depth));

    // Trực quan hóa tọa độ world
    //ALBEDO.rgb = fract(world_position).xyz;
  }

Một tối ưu hóa
--------------

Bạn có thể đạt được lợi ích khi sử dụng một triangle lớn duy nhất thay vì một quad toàn màn hình. Lý do cho việc này được giải thích `here <https://michaldrobot.com/2014/04/01/gcn-execution-patterns-in-full-screen-passes>`_. Tuy nhiên, lợi ích khá nhỏ và chỉ đáng kể khi chạy các fragment shader đặc biệt phức tạp.

Đặt Mesh trong MeshInstance3D thành một :ref:`ArrayMesh <class_ArrayMesh>`. ArrayMesh là một công cụ cho phép bạn dễ dàng dựng một Mesh từ các Array chứa vertex, normal, color, v.v.

Bây giờ, gắn một script vào MeshInstance3D và sử dụng đoạn code sau:

::

  extends MeshInstance3D

  func _ready():
    # Tạo một triangle duy nhất từ các vertex:
    var verts = PackedVector3Array()
    verts.append(Vector3(-1.0, -1.0, 0.0))
    verts.append(Vector3(3.0, -1.0, 0.0))
    verts.append(Vector3(-1.0, 3.0, 0.0))

    # Tạo một array gồm các array.
    # Array này có thể chứa normal, color, UV, v.v.
    var mesh_array = []
    mesh_array.resize(Mesh.ARRAY_MAX) #kích thước cần thiết cho ArrayMesh Array
    mesh_array[Mesh.ARRAY_VERTEX] = verts #vị trí của vertex array trong ArrayMesh Array

    # Tạo mesh từ mesh_array:
    mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, mesh_array)

.. note:: The triangle is specified in normalized device coordinates.
          Hãy nhớ rằng NDC chạy từ ``-1.0`` đến ``1.0`` theo cả hai hướng ``x`` và ``y``. Điều này khiến màn hình rộng ``2`` đơn vị và cao ``2`` đơn vị. Để bao phủ toàn bộ màn hình bằng một triangle duy nhất, hãy sử dụng một triangle rộng ``4`` đơn vị và cao ``4`` đơn vị, tức là gấp đôi chiều cao và chiều rộng của nó.

Gán vertex shader giống như ở trên và mọi thứ sẽ trông hoàn toàn giống nhau.

Nhược điểm duy nhất của việc sử dụng ArrayMesh thay cho QuadMesh là ArrayMesh không hiển thị trong editor vì triangle chưa được dựng cho đến khi scene chạy. Để khắc phục điều này, hãy dựng một Mesh dạng triangle duy nhất trong một modeling program rồi sử dụng Mesh đó trong MeshInstance3D.
