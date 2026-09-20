.. _doc_your_first_spatial_shader:

Shader 3D đầu tiên của bạn
==========================

Bạn đã quyết định bắt đầu viết Spatial shader tùy chỉnh của riêng mình. Có thể bạn đã thấy một thủ thuật thú vị trên mạng được thực hiện bằng shader, hoặc bạn nhận thấy rằng
:ref:`StandardMaterial3D <class_StandardMaterial3D>` isn't quite meeting your
cần thiết. Dù thế nào đi nữa, bạn đã quyết định tự viết shader và bây giờ cần tìm hiểu nên bắt đầu từ đâu.

Tutorial này sẽ giải thích cách viết Spatial shader và đề cập đến nhiều chủ đề hơn tutorial :ref:`CanvasItem <doc_your_first_canvasitem_shader>`.

Spatial shader có nhiều chức năng built-in hơn CanvasItem shader. Với spatial shader, Godot được kỳ vọng đã cung cấp sẵn chức năng cho các trường hợp sử dụng phổ biến và người dùng chỉ cần thiết lập các tham số phù hợp trong shader. Điều này đặc biệt đúng với quy trình PBR (physically based rendering).

Đây là tutorial gồm hai phần. Trong phần đầu tiên, chúng ta sẽ tạo terrain bằng cách dịch chuyển vertex từ heightmap trong hàm vertex. Trong :ref:`second part <doc_your_second_spatial_shader>`, chúng ta sẽ áp dụng các khái niệm từ tutorial này và thiết lập các material tùy chỉnh trong fragment shader bằng cách viết một ocean water shader.

.. note:: This tutorial assumes some basic shader knowledge such as types
          (``vec2``, ``float``, ``sampler2D``) và các hàm. Nếu bạn chưa quen với những khái niệm này, tốt nhất nên tìm hiểu nhập môn nhẹ nhàng từ `The Book of Shaders <https://thebookofshaders.com>`_ trước khi hoàn thành tutorial này.

Nơi gán material của tôi
------------------------

Trong 3D, các object được vẽ bằng :ref:`Meshes <class_Mesh>`. Mesh là một loại resource lưu trữ geometry (hình dạng của object) và material (màu sắc và cách object phản ứng với ánh sáng) trong các đơn vị gọi là "surface". Một Mesh có thể có nhiều surface hoặc chỉ một surface. Thông thường, bạn sẽ import mesh từ một chương trình khác (ví dụ: Blender). Tuy nhiên, Godot cũng có một số :ref:`PrimitiveMeshes <class_primitivemesh>` cho phép bạn thêm geometry cơ bản vào scene mà không cần import Mesh.

Có nhiều loại node mà bạn có thể dùng để vẽ một mesh. Loại chính là
:ref:`MeshInstance3D <class_MeshInstance3D>`, but you can also use :ref:`GPUParticles3D
<class_GPUParticles3D>`, :ref:`MultiMeshes <class_MultiMesh>` (với một
:ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>`), or others.

Thông thường, một material được liên kết với một surface cụ thể trong mesh, nhưng một số node, như MeshInstance3D, cho phép bạn override material cho một surface cụ thể hoặc cho tất cả surface.

Nếu bạn đặt material trên chính surface hoặc mesh, thì tất cả MeshInstance3D dùng chung mesh đó cũng sẽ dùng chung material đó. Tuy nhiên, nếu bạn muốn tái sử dụng cùng một mesh cho nhiều mesh instance nhưng có material khác nhau cho từng instance, bạn nên đặt material trên MeshInstance3D.

Trong tutorial này, chúng ta sẽ đặt material trên chính mesh thay vì tận dụng khả năng override material của MeshInstance3D.

Thiết lập
---------

Thêm một node :ref:`MeshInstance3D <class_MeshInstance3D>` mới vào scene.

Trong tab inspector, đặt thuộc tính **Mesh** của MeshInstance3D thành một
:ref:`PlaneMesh <class_planemesh>` resource, by clicking on ``<empty>`` and
mới bằng cách chọn **New PlaneMesh**. Sau đó mở rộng resource bằng cách nhấp vào hình ảnh plane xuất hiện.

Thao tác này thêm một plane vào scene.

Tiếp theo, trong viewport, nhấp vào nút **Perspective** ở góc trên bên trái. Trong menu xuất hiện, chọn **Display Wireframe**.

Thao tác này cho phép bạn nhìn thấy các triangle tạo nên plane.

.. image:: img/plane.webp

Bây giờ đặt **Subdivide Width** và **Subdivide Depth** của :ref:`PlaneMesh <class_planemesh>` thành ``32``.

.. image:: img/plane-sub-set.webp

Bạn có thể thấy hiện đã có nhiều triangle hơn trong
:ref:`MeshInstance3D<class_MeshInstance3D>`. This will give us more vertices to work with
và do đó cho phép chúng ta thêm nhiều chi tiết hơn.

.. image:: img/plane-sub.webp

:ref:`PrimitiveMeshes <class_primitivemesh>`, like PlaneMesh, only have one
surface, vì vậy thay vì một mảng material, ở đây chỉ có một material. Đặt **Material** thành một ShaderMaterial mới, sau đó mở rộng material bằng cách nhấp vào hình cầu xuất hiện.

.. note::
  Các material kế thừa từ resource :ref:`class_Material`, chẳng hạn như :ref:`class_StandardMaterial3D` và :ref:`class_ParticleProcessMaterial`, có thể được chuyển đổi thành :ref:`class_ShaderMaterial` và các thuộc tính hiện có của chúng sẽ được chuyển đổi thành một text shader đi kèm. Để thực hiện việc này, nhấp chuột phải vào material trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào đang chứa tham chiếu đến material trong inspector.

Bây giờ đặt **Shader** của material thành một Shader mới bằng cách nhấp vào ``<empty>`` rồi chọn **New Shader...**. Giữ nguyên các thiết lập mặc định, đặt tên cho shader và nhấp vào **Create**.

Nhấp vào shader trong inspector, lúc này shader editor sẽ xuất hiện. Bạn đã sẵn sàng bắt đầu viết Spatial shader đầu tiên của mình!

Phép màu shader
---------------

.. image:: img/shader-editor.webp

Shader mới đã được tạo sẵn với một biến ``shader_type``, hàm ``vertex()`` và hàm ``fragment()``. Điều đầu tiên Godot shader cần là khai báo loại shader. Trong trường hợp này, ``shader_type`` được đặt thành ``spatial`` vì đây là spatial shader.

.. code-block:: glsl

  shader_type spatial;

Hàm ``vertex()`` xác định vị trí các vertex của :ref:`MeshInstance3D<class_MeshInstance3D>` xuất hiện trong scene cuối cùng. Chúng ta sẽ dùng hàm này để thay đổi độ cao của từng vertex và làm cho plane phẳng của chúng ta trông giống một terrain nhỏ.

Khi hàm ``vertex()`` không có nội dung, Godot sẽ dùng vertex shader mặc định. Chúng ta có thể bắt đầu thay đổi bằng cách thêm một dòng duy nhất:

.. code-block:: glsl

  void vertex() {
    VERTEX.y += cos(VERTEX.x) * sin(VERTEX.z);
  }

Sau khi thêm dòng này, bạn sẽ nhận được hình ảnh giống như bên dưới.

.. image:: img/cos.webp

Được rồi, hãy phân tích điều này. Giá trị ``y`` của ``VERTEX`` đang được tăng lên. Và chúng ta truyền các component ``x`` và ``z`` của ``VERTEX`` làm đối số cho :ref:`cos() <shader_func_cos>` và :ref:`sin() <shader_func_sin>`; điều đó tạo ra diện mạo giống như sóng trên các trục ``x`` và ``z``.

Điều chúng ta muốn đạt được là diện mạo của những ngọn đồi nhỏ; dù sao thì. ``cos()`` và ``sin()`` vốn đã trông hơi giống những ngọn đồi. Chúng ta thực hiện điều này bằng cách scale các input của các hàm ``cos()`` và ``sin()``.

.. code-block:: glsl

  void vertex() {
    VERTEX.y += cos(VERTEX.x * 4.0) * sin(VERTEX.z * 4.0);
  }

.. image:: img/cos4.webp

Trông đã đẹp hơn, nhưng vẫn quá nhọn và lặp lại; hãy làm cho nó thú vị hơn một chút.

Heightmap từ noise
------------------

Noise là một công cụ rất phổ biến để giả lập diện mạo của terrain. Hãy hình dung nó tương tự hàm cosine, trong đó bạn có những ngọn đồi lặp lại, ngoại trừ việc với noise, mỗi ngọn đồi có một độ cao khác nhau.

Godot cung cấp resource :ref:`NoiseTexture2D <class_noisetexture2D>` để tạo noise texture có thể được truy cập từ shader.

Để truy cập texture trong shader, hãy thêm đoạn code sau gần đầu shader, bên ngoài hàm ``vertex()``.

.. code-block:: glsl

  uniform sampler2D noise;

Thao tác này cho phép bạn truyền một noise texture vào shader. Bây giờ hãy nhìn vào inspector bên dưới material. Bạn sẽ thấy một section có tên **Shader Parameters**. Nếu mở section đó, bạn sẽ thấy một tham số có tên "Noise".

Đặt tham số **Noise** này thành một :ref:`NoiseTexture2D <class_noisetexture2D>` mới. Sau đó, trong NoiseTexture2D, đặt thuộc tính **Noise** của nó thành một
:ref:`FastNoiseLite <class_fastnoiselite>`. The FastNoiseLite class is used by
mới để NoiseTexture2D tạo heightmap.

Sau khi thiết lập xong, kết quả sẽ trông như thế này.

.. image:: img/noise-set.webp

Bây giờ, truy cập noise texture bằng hàm ``texture()``:

.. code-block:: glsl

  void vertex() {
    float height = texture(noise, VERTEX.xz / 2.0 + 0.5).x;
    VERTEX.y += height;
  }

:ref:`texture() <shader_func_texture>` takes a texture as the first argument and
một ``vec2`` cho vị trí trên texture làm đối số thứ hai. Chúng ta sử dụng các channel ``x`` và ``z`` của ``VERTEX`` để xác định vị trí cần tra cứu trên texture.

Vì tọa độ của PlaneMesh nằm trong khoảng ``[-1.0, 1.0]`` (với kích thước ``2.0``), còn tọa độ texture nằm trong ``[0.0, 1.0]``, nên để ánh xạ lại tọa độ, chúng ta chia cho kích thước của PlaneMesh theo ``2.0`` và cộng thêm ``0.5`` .

``texture()`` trả về một ``vec4`` của các channel ``r, g, b, a`` tại vị trí đó. Vì noise texture là grayscale nên tất cả các giá trị đều giống nhau, do đó chúng ta có thể dùng bất kỳ channel nào làm độ cao. Trong trường hợp này, chúng ta sẽ dùng channel ``r`` hoặc ``x``.

.. note::

  ``xyzw`` giống với ``rgba`` trong GLSL, vì vậy thay vì ``texture().x`` ở trên, chúng ta có thể dùng ``texture().r``. Xem `OpenGL documentation <https://www.khronos.org/opengl/wiki/Data_Type_(GLSL)#Vectors>`_ để biết thêm chi tiết.

Với đoạn code này, bạn có thể thấy texture tạo ra những ngọn đồi trông ngẫu nhiên.

.. image:: img/noise.webp

Hiện tại các ngọn đồi quá nhọn, chúng ta muốn làm chúng mềm hơn một chút. Để làm điều đó, chúng ta sẽ dùng một uniform. Bạn đã sử dụng uniform ở trên để truyền noise texture; bây giờ hãy tìm hiểu cách chúng hoạt động.

Uniform
-------

:ref:`Uniform variables <doc_shading_language_uniforms>` allow you to pass data
từ game vào shader. Chúng rất hữu ích để điều khiển các hiệu ứng shader. Uniform có thể là gần như bất kỳ datatype nào được dùng trong shader. Để sử dụng uniform, bạn khai báo nó trong
:ref:`Shader<class_Shader>` using the keyword ``uniform``.

Hãy tạo một uniform thay đổi độ cao của terrain.

.. code-block:: glsl

  uniform float height_scale = 0.5;


Godot cho phép bạn khởi tạo một uniform bằng một giá trị; ở đây, ``height_scale`` được đặt thành ``0.5``. Bạn có thể đặt uniform từ GDScript bằng cách gọi hàm
:ref:`set_shader_parameter() <class_ShaderMaterial_method_set_shader_parameter>`
trên material tương ứng với shader. Giá trị được truyền từ GDScript sẽ được ưu tiên hơn giá trị dùng để khởi tạo trong shader.

.. code-block:: gdscript

  # được gọi từ MeshInstance3D
  mesh.material.set_shader_parameter("height_scale", 0.5)

.. note:: Changing uniforms in Spatial-based nodes is different from
          node dựa trên CanvasItem. Ở đây, chúng ta đặt material bên trong resource PlaneMesh. Với các mesh resource khác, trước tiên bạn có thể cần truy cập material bằng cách gọi ``surface_get_material()``. Còn trong MeshInstance3D, bạn sẽ truy cập material bằng ``get_surface_material()`` hoặc ``material_override``.

Hãy nhớ rằng chuỗi được truyền vào ``set_shader_parameter()`` phải khớp với tên của biến uniform trong shader. Bạn có thể sử dụng biến uniform ở bất kỳ đâu bên trong shader. Ở đây, chúng ta sẽ dùng nó để đặt giá trị độ cao thay vì nhân tùy ý với ``0.5``.

.. code-block:: glsl

  VERTEX.y += height * height_scale;

Bây giờ trông đẹp hơn nhiều.

.. image:: img/noise-low.webp

Bằng cách sử dụng uniforms, chúng ta thậm chí có thể thay đổi giá trị ở mỗi frame để tạo animation cho độ cao của địa hình. Khi kết hợp với :ref:`Tweens <class_Tween>`, cách này đặc biệt hữu ích cho các animation.

Tương tác với ánh sáng
----------------------

Trước tiên, hãy tắt wireframe. Để làm vậy, mở lại menu **Perspective** ở góc trên bên trái của viewport và chọn **Display Normal**. Ngoài ra, trong thanh công cụ cảnh 3D, hãy tắt preview sunlight.

.. image:: img/normal.webp

Hãy chú ý rằng màu của mesh trở nên đồng nhất. Đó là vì ánh sáng trên mesh cũng đồng nhất. Hãy thêm một light!

Trước tiên, chúng ta sẽ thêm một :ref:`OmniLight3D<class_OmniLight3D>` vào scene, rồi kéo nó lên để nó nằm phía trên địa hình.

.. image:: img/light.webp

Bạn có thể thấy light đang tác động lên địa hình, nhưng kết quả trông khá kỳ lạ. Vấn đề là light đang tác động lên địa hình như thể nó là một mặt phẳng. Đó là vì light shader sử dụng các normal từ :ref:`Mesh <class_mesh>` để tính toán ánh sáng.

Các normal được lưu trong Mesh, nhưng chúng ta đang thay đổi hình dạng của Mesh trong shader, nên các normal không còn chính xác nữa. Để khắc phục, chúng ta có thể tính toán lại các normal trong shader hoặc sử dụng một normal texture tương ứng với noise của mình. Godot giúp chúng ta thực hiện cả hai cách này một cách dễ dàng.

Bạn có thể tự tính toán normal mới trong hàm vertex, sau đó chỉ cần đặt ``NORMAL``. Khi đã đặt ``NORMAL``, Godot sẽ thực hiện mọi phép tính ánh sáng phức tạp thay cho chúng ta. Chúng ta sẽ tìm hiểu phương pháp này trong phần tiếp theo của tutorial; còn bây giờ, chúng ta sẽ đọc các normal từ một texture.

Thay vào đó, chúng ta sẽ tiếp tục dựa vào NoiseTexture để tính toán các normal cho mình. Chúng ta thực hiện việc này bằng cách truyền vào một noise texture thứ hai.

.. code-block:: glsl

  uniform sampler2D normalmap;

Đặt uniform texture thứ hai này thành một :ref:`NoiseTexture2D <class_noisetexture2D>` khác với một
:ref:`FastNoiseLite <class_fastnoiselite>`. But this time, check **As Normal Map**.

.. image:: img/normal-set.webp

Khi có các normal tương ứng với một vertex cụ thể, chúng ta đặt ``NORMAL``, nhưng nếu bạn có một normalmap lấy từ một texture, hãy đặt normal bằng ``NORMAL_MAP`` trong hàm ``fragment()``. Nhờ vậy, Godot sẽ tự động xử lý việc wrap texture quanh mesh.

Cuối cùng, để đảm bảo rằng chúng ta đang đọc từ cùng một vị trí trên noise texture và normalmap texture, chúng ta sẽ truyền vị trí ``VERTEX.xz`` từ hàm ``vertex()`` sang hàm ``fragment()``. Chúng ta thực hiện việc này bằng một :ref:`varying <doc_shading_language_varyings>`.

Bên trên ``vertex()``, hãy định nghĩa một ``varying vec2`` có tên là ``tex_position``. Và bên trong hàm ``vertex()``, hãy gán ``VERTEX.xz`` cho ``tex_position``.

.. code-block:: glsl

  varying vec2 tex_position;

  void vertex() {
    tex_position = VERTEX.xz / 2.0 + 0.5;
    float height = texture(noise, tex_position).x;
    VERTEX.y += height * height_scale;
  }

Và bây giờ chúng ta có thể truy cập ``tex_position`` từ hàm ``fragment()``.

.. code-block:: glsl

  void fragment() {
    NORMAL_MAP = texture(normalmap, tex_position).xyz;
  }

Khi các normal đã được thiết lập, light giờ đây phản ứng linh hoạt theo độ cao của mesh.

.. image:: img/normalmap.webp

Chúng ta thậm chí có thể kéo light đi xung quanh, và ánh sáng sẽ tự động cập nhật.

.. image:: img/normalmap2.webp

Toàn bộ code
------------

Đây là toàn bộ code của tutorial này. Bạn có thể thấy nó không dài lắm vì Godot đã xử lý phần lớn những công việc phức tạp thay cho bạn.

.. code-block:: glsl

  shader_type spatial;

  uniform float height_scale = 0.5;
  uniform sampler2D noise;
  uniform sampler2D normalmap;

  varying vec2 tex_position;

  void vertex() {
    tex_position = VERTEX.xz / 2.0 + 0.5;
    float height = texture(noise, tex_position).x;
    VERTEX.y += height * height_scale;
  }

  void fragment() {
    NORMAL_MAP = texture(normalmap, tex_position).xyz;
  }

Đó là tất cả nội dung của phần này. Hy vọng giờ đây bạn đã hiểu những điều cơ bản về vertex shader trong Godot. Trong phần tiếp theo của tutorial, chúng ta sẽ viết một hàm fragment để đi cùng với hàm vertex này, đồng thời tìm hiểu một kỹ thuật nâng cao hơn để biến địa hình này thành một đại dương với những con sóng chuyển động.
