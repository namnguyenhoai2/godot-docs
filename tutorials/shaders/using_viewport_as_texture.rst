.. _doc_viewport_as_texture:

Sử dụng SubViewport làm texture
===============================

Giới thiệu
----------

Tutorial này sẽ giới thiệu cách sử dụng :ref:`SubViewport <class_SubViewport>` làm texture có thể áp dụng cho các đối tượng 3D. Để thực hiện điều đó, tutorial sẽ hướng dẫn bạn quy trình tạo một hành tinh procedural như bên dưới:

.. image:: img/planet_example.png

.. note:: Tutorial này không hướng dẫn cách lập trình atmosphere động như của hành tinh này.

Tutorial này giả định bạn đã quen với cách thiết lập một scene cơ bản, bao gồm: một :ref:`Camera3D <class_Camera3D>`, một :ref:`light source <class_OmniLight3D>`, một
:ref:`MeshInstance3D <class_MeshInstance3D>` có :ref:`Primitive Mesh <class_PrimitiveMesh>`, và áp dụng một :ref:`StandardMaterial3D <class_StandardMaterial3D>` cho mesh. Trọng tâm sẽ là sử dụng :ref:`SubViewport <class_SubViewport>` để tạo động các texture có thể áp dụng cho mesh.

Trong tutorial này, chúng ta sẽ tìm hiểu các chủ đề sau:

- Cách sử dụng :ref:`SubViewport <class_SubViewport>` làm render texture
- Ánh xạ texture lên hình cầu bằng phép ánh xạ equirectangular
- Các kỹ thuật fragment shader cho hành tinh procedural
- Thiết lập bản đồ Roughness từ :ref:`Viewport Texture <class_ViewportTexture>`

Thiết lập scene
---------------

Tạo một scene mới và thêm chính xác các node sau như minh họa bên dưới.

.. image:: img/viewport_texture_node_tree.webp

Mở MeshInstance3D và đặt mesh thành SphereMesh

Thiết lập SubViewport
---------------------

Nhấp vào node :ref:`SubViewport <class_SubViewport>` và đặt kích thước thành ``(1024, 512)``.
:ref:`SubViewport <class_SubViewport>` thực tế có thể có kích thước bất kỳ, miễn là chiều rộng gấp đôi chiều cao. Chiều rộng cần gấp đôi chiều cao để hình ảnh được ánh xạ chính xác lên hình cầu, vì chúng ta sẽ sử dụng phép chiếu equirectangular, nhưng sẽ nói thêm về điều đó sau.

Tiếp theo, tắt 3D. Chúng ta sẽ sử dụng một :ref:`ColorRect <class_ColorRect>` để render bề mặt, vì vậy cũng không cần 3D.

.. image:: img/planet_new_viewport.webp

Chọn :ref:`ColorRect <class_ColorRect>` và trong inspector, đặt anchors preset thành ``Full Rect``. Điều này sẽ đảm bảo :ref:`ColorRect <class_ColorRect>` chiếm toàn bộ :ref:`SubViewport <class_SubViewport>`.

.. image:: img/planet_new_colorrect.webp

Tiếp theo, chúng ta thêm một :ref:`Shader Material <class_ShaderMaterial>` vào :ref:`ColorRect <class_ColorRect>` (ColorRect > CanvasItem > Material > Material > ``New ShaderMaterial``).

.. note:: Bạn nên có kiến thức cơ bản về shading để thực hiện tutorial này. Tuy nhiên, ngay cả khi bạn mới làm quen với shader, toàn bộ code sẽ được cung cấp, nên bạn sẽ không gặp vấn đề gì khi làm theo.

Nhấp vào nút menu thả xuống của shader material và nhấp / Edit. Từ đây, đi đến Shader > ``New Shader``. đặt tên cho nó và nhấp vào "Create". nhấp vào shader trong inspector để mở shader editor. Xóa code mặc định và thêm đoạn sau:

.. code-block:: glsl

    shader_type canvas_item;

    void fragment() {
        COLOR = vec4(UV.x, UV.y, 0.5, 1.0);
    }

Lưu shader code, bạn sẽ thấy trong inspector rằng đoạn code trên render một gradient như bên dưới.

.. image:: img/planet_gradient.png

Giờ chúng ta đã có những thành phần cơ bản của một :ref:`SubViewport <class_SubViewport>` để render và có một hình ảnh riêng có thể áp dụng cho hình cầu.

Áp dụng texture
---------------

Bây giờ mở :ref:`MeshInstance3D <class_MeshInstance3D>` và thêm một :ref:`StandardMaterial3D <class_StandardMaterial3D>` vào đó. Không cần :ref:`Shader Material <class_ShaderMaterial>` đặc biệt nào (mặc dù đó sẽ là ý tưởng hay cho các hiệu ứng nâng cao hơn, chẳng hạn như atmosphere trong ví dụ trên).

MeshInstance3D > GeometryInstance > Geometry > Material Override > ``New StandardMaterial3D``

Sau đó nhấp vào menu thả xuống của StandardMaterial3D và nhấp vào "Edit"

Đi đến phần "Resource" và đánh dấu vào ô ``Local to scene``. Sau đó, đi đến phần "Albedo" và nhấp bên cạnh thuộc tính "Texture" để thêm Albedo Texture. Tại đây, chúng ta sẽ áp dụng texture đã tạo. Chọn "New ViewportTexture"

.. image:: img/planet_new_viewport_texture.webp

Nhấp vào ViewportTexture vừa tạo trong inspector, sau đó nhấp vào "Assign". Tiếp theo, từ menu bật lên, chọn Viewport mà chúng ta đã render trước đó.

.. image:: img/planet_pick_viewport_texture.webp

Hình cầu của bạn giờ sẽ được tô màu bằng các màu đã render vào Viewport.

.. image:: img/planet_seam.webp

Bạn có thấy đường nối xấu xí hình thành tại nơi texture quấn quanh không? Điều này xảy ra vì chúng ta chọn màu dựa trên tọa độ UV, mà tọa độ UV không quấn quanh texture. Đây là một vấn đề kinh điển trong phép chiếu bản đồ 2D. Các nhà phát triển game thường có một bản đồ 2 chiều muốn chiếu lên hình cầu, nhưng khi quấn quanh, bản đồ sẽ có các đường nối lớn. Có một cách giải quyết tao nhã cho vấn đề này, và chúng ta sẽ minh họa trong phần tiếp theo.

Tạo texture cho hành tinh
-------------------------

Vậy là giờ đây, khi render vào :ref:`SubViewport <class_SubViewport>`, nó sẽ xuất hiện kỳ diệu trên hình cầu. Nhưng các tọa độ texture đã tạo ra một đường nối xấu xí. Vậy làm thế nào để có được một dải tọa độ quấn quanh hình cầu theo cách đẹp mắt? Một giải pháp là sử dụng một hàm lặp lại trên miền của texture. ``sin`` và ``cos`` là hai hàm như vậy. Hãy áp dụng chúng vào texture và xem điều gì xảy ra. Thay thế đoạn code màu hiện có trong shader bằng đoạn sau:

.. code-block:: glsl

    COLOR.xyz = vec3(sin(UV.x * 3.14159 * 4.0) * cos(UV.y * 3.14159 * 4.0) * 0.5 + 0.5);

.. image:: img/planet_sincos.webp

Không tệ. Nếu quan sát xung quanh, bạn sẽ thấy đường nối đã biến mất, nhưng thay vào đó, các cực bị co kéo. Hiện tượng co kéo này là do cách Godot ánh xạ texture lên hình cầu trong
:ref:`StandardMaterial3D <class_StandardMaterial3D>`. Godot sử dụng một kỹ thuật chiếu gọi là phép chiếu equirectangular, chuyển bản đồ hình cầu lên một mặt phẳng 2D.

.. note:: Nếu bạn muốn biết thêm một chút thông tin về kỹ thuật này, chúng ta sẽ chuyển đổi từ tọa độ cầu sang tọa độ Cartesian. Tọa độ cầu ánh xạ kinh độ và vĩ độ của hình cầu, trong khi tọa độ Cartesian, xét về mọi mặt, là một vector từ tâm hình cầu đến điểm đó.

Với mỗi pixel, chúng ta sẽ tính vị trí 3D của nó trên hình cầu. Từ đó, chúng ta sẽ sử dụng noise 3D để xác định giá trị màu. Bằng cách tính noise trong không gian 3D, chúng ta giải quyết được vấn đề co kéo ở các cực. Để hiểu lý do, hãy hình dung noise được tính trên bề mặt hình cầu thay vì trên mặt phẳng 2D. Khi tính trên bề mặt hình cầu, bạn không bao giờ chạm đến một cạnh, do đó không bao giờ tạo ra đường nối hoặc điểm co kéo ở cực. Đoạn code sau chuyển đổi ``UVs`` thành tọa độ Cartesian.

.. code-block:: glsl

    float theta = UV.y * 3.14159;
    float phi = UV.x * 3.14159 * 2.0;
    vec3 unit = vec3(0.0, 0.0, 0.0);

    unit.x = sin(phi) * sin(theta);
    unit.y = cos(theta) * -1.0;
    unit.z = cos(phi) * sin(theta);
    unit = normalize(unit);

Và nếu sử dụng ``unit`` làm giá trị ``COLOR`` đầu ra, chúng ta sẽ có:

.. image:: img/planet_normals.webp

Giờ chúng ta có thể tính vị trí 3D của bề mặt hình cầu, nên có thể sử dụng noise 3D để tạo hành tinh. Chúng ta sẽ sử dụng trực tiếp hàm noise này từ `Shadertoy <https://www.shadertoy.com/view/Xsl3Dl>`_:

.. code-block:: glsl

    vec3 hash(vec3 p) {
        p = vec3(dot(p, vec3(127.1, 311.7, 74.7)),
                 dot(p, vec3(269.5, 183.3, 246.1)),
                 dot(p, vec3(113.5, 271.9, 124.6)));

        return -1.0 + 2.0 * fract(sin(p) * 43758.5453123);
    }

    float noise(vec3 p) {
      vec3 i = floor(p);
      vec3 f = fract(p);
      vec3 u = f * f * (3.0 - 2.0 * f);

      return mix(mix(mix(dot(hash(i + vec3(0.0, 0.0, 0.0)), f - vec3(0.0, 0.0, 0.0)),
                         dot(hash(i + vec3(1.0, 0.0, 0.0)), f - vec3(1.0, 0.0, 0.0)), u.x),
                     mix(dot(hash(i + vec3(0.0, 1.0, 0.0)), f - vec3(0.0, 1.0, 0.0)),
                         dot(hash(i + vec3(1.0, 1.0, 0.0)), f - vec3(1.0, 1.0, 0.0)), u.x), u.y),
                 mix(mix(dot(hash(i + vec3(0.0, 0.0, 1.0)), f - vec3(0.0, 0.0, 1.0)),
                         dot(hash(i + vec3(1.0, 0.0, 1.0)), f - vec3(1.0, 0.0, 1.0)), u.x),
                     mix(dot(hash(i + vec3(0.0, 1.0, 1.0)), f - vec3(0.0, 1.0, 1.0)),
                         dot(hash(i + vec3(1.0, 1.0, 1.0)), f - vec3(1.0, 1.0, 1.0)), u.x), u.y), u.z );
    }

.. note:: Mọi công lao đều thuộc về tác giả, Inigo Quilez. Hàm này được phát hành theo giấy phép ``MIT``.

Để sử dụng ``noise``, hãy thêm đoạn sau vào hàm ``fragment``:

.. code-block:: glsl

    float n = noise(unit * 5.0);
    COLOR.xyz = vec3(n * 0.5 + 0.5);

.. image:: img/planet_noise.webp

.. note:: Để làm nổi bật texture, chúng ta đặt material thành unshaded.

Bây giờ bạn có thể thấy rằng nhiễu thực sự bao quanh quả cầu một cách liền mạch. Mặc dù nó trông chẳng giống hành tinh mà bạn đã được hứa hẹn chút nào. Vì vậy, hãy chuyển sang thứ gì đó nhiều màu sắc hơn.

Tô màu cho hành tinh
--------------------

Bây giờ hãy tạo màu cho hành tinh. Có nhiều cách để làm việc này, nhưng hiện tại, chúng ta sẽ dùng một gradient giữa nước và đất liền.

Để tạo gradient trong GLSL, chúng ta sử dụng hàm ``mix``. ``mix`` nhận hai giá trị để nội suy giữa chúng và một đối số thứ ba để chọn mức độ nội suy; về bản chất, nó *mixes* hai giá trị với nhau. Trong các API khác, hàm này thường được gọi là ``lerp``. Tuy nhiên, ``lerp`` thường được dành riêng cho việc trộn hai số thực; ``mix`` có thể nhận bất kỳ giá trị nào, dù đó là số thực hay kiểu vector.

.. code-block:: glsl

    COLOR.xyz = mix(vec3(0.05, 0.3, 0.5), vec3(0.9, 0.4, 0.1), n * 0.5 + 0.5);

Màu đầu tiên là màu xanh dương cho đại dương. Màu thứ hai là một màu hơi đỏ (vì mọi hành tinh ngoài hành tinh đều cần địa hình màu đỏ). Cuối cùng, chúng được trộn với nhau bằng ``n * 0.5 + 0.5``. ``n`` biến đổi mượt mà giữa ``-1`` và ``1``. Vì vậy, chúng ta ánh xạ nó vào miền ``0-1`` mà ``mix`` yêu cầu. Bây giờ bạn có thể thấy màu sắc thay đổi giữa xanh dương và đỏ.

.. image:: img/planet_noise_color.webp

Cách đó hơi mờ hơn mức chúng ta muốn. Các hành tinh thường có ranh giới tương đối rõ ràng giữa đất liền và biển. Để làm vậy, chúng ta sẽ đổi hạng tử cuối thành ``smoothstep(-0.1, 0.0, n)``. Và do đó, toàn bộ dòng lệnh trở thành:

.. code-block:: glsl

    COLOR.xyz = mix(vec3(0.05, 0.3, 0.5), vec3(0.9, 0.4, 0.1), smoothstep(-0.1, 0.0, n));

``smoothstep`` trả về ``0`` nếu đối số thứ ba nhỏ hơn đối số thứ nhất, trả về ``1`` nếu đối số thứ ba lớn hơn đối số thứ hai, và trộn mượt mà giữa ``0`` và ``1`` nếu số thứ ba nằm giữa số thứ nhất và số thứ hai. Vì vậy, trong dòng này, ``smoothstep`` trả về ``0`` bất cứ khi nào ``n`` nhỏ hơn ``-0.1``, và trả về ``1`` bất cứ khi nào ``n`` lớn hơn ``0``.

.. image:: img/planet_noise_smooth.webp

Thêm một điều nữa để hành tinh trông giống hành tinh hơn một chút. Đất liền không nên có dạng quá nhão; hãy làm cho các cạnh gồ ghề hơn một chút. Một thủ thuật thường được dùng trong shader để tạo địa hình trông gồ ghề bằng nhiễu là xếp chồng các mức nhiễu lên nhau ở nhiều tần số khác nhau. Chúng ta dùng một lớp để tạo cấu trúc tổng thể nhão của các lục địa. Sau đó, một lớp khác phá vỡ các cạnh đôi chút, rồi thêm một lớp nữa, và cứ tiếp tục như vậy. Chúng ta sẽ tính ``n`` bằng bốn dòng mã shader thay vì chỉ một dòng. ``n`` trở thành:

.. code-block:: glsl

    float n = noise(unit * 5.0) * 0.5;
    n += noise(unit * 10.0) * 0.25;
    n += noise(unit * 20.0) * 0.125;
    n += noise(unit * 40.0) * 0.0625;

Và bây giờ hành tinh trông như sau:

.. image:: img/planet_noise_fbm.webp

Tạo đại dương
-------------

Một điều cuối cùng để hình ảnh này trông giống một hành tinh hơn. Đại dương và đất liền phản xạ ánh sáng khác nhau. Vì vậy, chúng ta muốn đại dương sáng bóng hơn đất liền một chút. Có thể thực hiện điều này bằng cách truyền một giá trị thứ tư vào kênh ``alpha`` của ``COLOR`` đầu ra và sử dụng nó làm bản đồ Roughness.

.. code-block:: glsl

    COLOR.a = 0.3 + 0.7 * smoothstep(-0.1, 0.0, n);

Dòng này trả về ``0.3`` cho nước và ``1.0`` cho đất liền. Điều đó có nghĩa là đất liền sẽ khá gồ ghề, trong khi nước sẽ khá trơn.

Sau đó, trong material, bên dưới phần "Metallic", hãy đảm bảo ``Metallic`` được đặt thành ``0`` và ``Specular`` được đặt thành ``1``. Lý do là nước phản xạ ánh sáng rất tốt nhưng không mang tính kim loại. Các giá trị này không chính xác về mặt vật lý, nhưng đủ tốt cho bản demo này.

Tiếp theo, bên dưới phần "Roughness", hãy đặt texture roughness thành một
:ref:`Viewport Texture <class_ViewportTexture>` trỏ đến texture hành tinh :ref:`SubViewport <class_SubViewport>` của chúng ta. Cuối cùng, đặt ``Texture Channel`` thành ``Alpha``. Điều này hướng dẫn renderer sử dụng kênh ``alpha`` của ``COLOR`` đầu ra làm giá trị ``Roughness``.

.. image:: img/planet_ocean.webp

Bạn sẽ nhận thấy rằng hầu như không có gì thay đổi, ngoại trừ việc hành tinh không còn phản chiếu bầu trời nữa. Điều này xảy ra vì theo mặc định, khi một vật thể được render với giá trị alpha, nó được vẽ dưới dạng một vật thể trong suốt phủ lên nền. Và vì nền mặc định của :ref:`SubViewport <class_SubViewport>` là đục, kênh ``alpha`` của
:ref:`Viewport Texture <class_ViewportTexture>` là ``1``, khiến texture hành tinh được vẽ với màu nhạt hơn một chút và giá trị ``Roughness`` bằng ``1`` ở mọi nơi. Để khắc phục, chúng ta mở :ref:`SubViewport <class_SubViewport>` và bật thuộc tính "Transparent Bg". Vì hiện tại chúng ta đang render một vật thể trong suốt nằm trên một vật thể trong suốt khác, chúng ta muốn bật ``blend_premul_alpha``:

.. code-block:: glsl

    render_mode blend_premul_alpha;

Thao tác này nhân trước các màu với giá trị ``alpha``, sau đó trộn chúng với nhau một cách chính xác. Thông thường, khi trộn một màu trong suốt lên trên một màu trong suốt khác, ngay cả khi nền có ``alpha`` bằng ``0`` (như trong trường hợp này), bạn vẫn gặp phải các vấn đề loang màu kỳ lạ. Đặt ``blend_premul_alpha`` sẽ khắc phục điều đó.

Bây giờ, hành tinh sẽ trông như đang phản xạ ánh sáng trên đại dương nhưng không phản xạ trên đất liền. Di chuyển quanh :ref:`OmniLight3D <class_OmniLight3D>` trong scene để thấy hiệu ứng phản xạ trên đại dương.

.. image:: img/planet_ocean_reflect.webp

Vậy là xong. Một hành tinh được tạo theo quy trình bằng cách sử dụng :ref:`SubViewport <class_SubViewport>`.

.. _`Shadertoy`: https://www.shadertoy.com/view/Xsl3Dl
