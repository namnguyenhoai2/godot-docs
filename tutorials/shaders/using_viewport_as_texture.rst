.. _doc_viewport_as_texture:

Sử dụng SubViewport làm texture
===============================

Giới thiệu
----------

Tutorial này sẽ hướng dẫn bạn sử dụng :ref:`SubViewport <class_SubViewport>` làm texture có thể áp dụng cho các đối tượng 3D. Để thực hiện điều đó, tutorial sẽ hướng dẫn bạn từng bước tạo một hành tinh procedural như bên dưới:

.. image:: img/planet_example.png

.. note:: This tutorial does not cover how to code a dynamic atmosphere like the one this planet has.

Tutorial này giả định bạn đã quen với cách thiết lập một scene cơ bản, bao gồm: một :ref:`Camera3D <class_Camera3D>`, một :ref:`light source <class_OmniLight3D>`, một
:ref:`MeshInstance3D <class_MeshInstance3D>` with a :ref:`Primitive Mesh <class_PrimitiveMesh>`,
và áp dụng một :ref:`StandardMaterial3D <class_StandardMaterial3D>` cho mesh. Trọng tâm sẽ là sử dụng :ref:`SubViewport <class_SubViewport>` để dynamically tạo các texture có thể áp dụng cho mesh.

Trong tutorial này, chúng ta sẽ tìm hiểu các chủ đề sau:

- Cách sử dụng :ref:`SubViewport <class_SubViewport>` làm render texture - Ánh xạ texture lên một hình cầu bằng phép ánh xạ equirectangular - Các kỹ thuật fragment shader cho hành tinh procedural - Thiết lập bản đồ Roughness từ một :ref:`Viewport Texture <class_ViewportTexture>`

Thiết lập scene
---------------

Tạo một scene mới và thêm các node sau đây chính xác như minh họa bên dưới.

.. image:: img/viewport_texture_node_tree.webp

Mở MeshInstance3D và đặt mesh thành SphereMesh

Thiết lập SubViewport
---------------------

Nhấp vào node :ref:`SubViewport <class_SubViewport>` và đặt kích thước của nó thành ``(1024, 512)``. Giá trị
:ref:`SubViewport <class_SubViewport>` can actually be any size so long as the width is double the
chiều cao. Chiều rộng cần gấp đôi chiều cao để hình ảnh được ánh xạ chính xác lên hình cầu, vì chúng ta sẽ sử dụng phép chiếu equirectangular, nhưng sẽ nói thêm về điều đó sau.

Tiếp theo, tắt 3D. Chúng ta sẽ sử dụng một :ref:`ColorRect <class_ColorRect>` để render bề mặt, vì vậy cũng không cần 3D.

.. image:: img/planet_new_viewport.webp

Chọn :ref:`ColorRect <class_ColorRect>` và trong inspector, đặt anchors preset thành ``Full Rect``. Điều này sẽ đảm bảo rằng :ref:`ColorRect <class_ColorRect>` chiếm toàn bộ :ref:`SubViewport <class_SubViewport>`.

.. image:: img/planet_new_colorrect.webp

Tiếp theo, chúng ta thêm một :ref:`Shader Material <class_ShaderMaterial>` vào :ref:`ColorRect <class_ColorRect>` (ColorRect > CanvasItem > Material > Material > ``New ShaderMaterial``).

.. note:: Basic familiarity with shading is recommended for this tutorial. However, even if you are new
          đối với shader, toàn bộ code sẽ được cung cấp, vì vậy bạn sẽ không gặp vấn đề gì khi làm theo.

Nhấp vào nút menu dropdown của shader material rồi nhấp vào / Edit. Từ đây, đi tới Shader > ``New Shader``, đặt tên cho nó rồi nhấp vào "Create". Nhấp vào shader trong inspector để mở shader editor. Xóa code mặc định và thêm đoạn sau:

.. code-block:: glsl

    shader_type canvas_item;

    void fragment() {
        COLOR = vec4(UV.x, UV.y, 0.5, 1.0);
    }

lưu shader code, bạn sẽ thấy trong inspector rằng đoạn code trên render một gradient như bên dưới.

.. image:: img/planet_gradient.png

Bây giờ chúng ta đã có những nền tảng cơ bản của một :ref:`SubViewport <class_SubViewport>` để render và có một hình ảnh độc nhất có thể áp dụng cho hình cầu.

Áp dụng texture
---------------

Bây giờ hãy mở :ref:`MeshInstance3D <class_MeshInstance3D>` và thêm một :ref:`StandardMaterial3D <class_StandardMaterial3D>` vào đó. Không cần một :ref:`Shader Material <class_ShaderMaterial>` đặc biệt (mặc dù đó sẽ là một ý tưởng hay cho các hiệu ứng nâng cao hơn, chẳng hạn như bầu khí quyển trong ví dụ trên).

MeshInstance3D > GeometryInstance > Geometry > Material Override > ``New StandardMaterial3D``

Sau đó nhấp vào dropdown của StandardMaterial3D và nhấp vào "Edit"

Đi tới phần "Resource" và chọn hộp ``Local to scene``. Sau đó, đi tới phần "Albedo" và nhấp bên cạnh thuộc tính "Texture" để thêm Albedo Texture. Tại đây, chúng ta sẽ áp dụng texture đã tạo. Chọn "New ViewportTexture"

.. image:: img/planet_new_viewport_texture.webp

Nhấp vào ViewportTexture vừa tạo trong inspector, sau đó nhấp vào "Assign". Tiếp theo, từ menu bật lên, chọn Viewport mà trước đó chúng ta đã render tới.

.. image:: img/planet_pick_viewport_texture.webp

Bây giờ hình cầu của bạn sẽ được tô màu bằng các màu mà chúng ta đã render tới Viewport.

.. image:: img/planet_seam.webp

Hãy chú ý đến đường nối xấu xí hình thành ở nơi texture wrap quanh? Điều này xảy ra vì chúng ta chọn màu dựa trên tọa độ UV, mà tọa độ UV không wrap quanh texture. Đây là một vấn đề kinh điển trong phép chiếu bản đồ 2D. Các nhà phát triển game thường có một bản đồ 2 chiều mà họ muốn chiếu lên một hình cầu, nhưng khi wrap quanh, nó sẽ có các đường nối lớn. Có một cách khắc phục tinh tế cho vấn đề này mà chúng ta sẽ minh họa trong phần tiếp theo.

Tạo texture cho hành tinh
-------------------------

Vậy là bây giờ, khi render tới :ref:`SubViewport <class_SubViewport>`, nó sẽ xuất hiện một cách kỳ diệu trên hình cầu. Nhưng các tọa độ texture của chúng ta tạo ra một đường nối xấu xí. Vậy làm thế nào để có được một dải tọa độ wrap quanh hình cầu theo cách đẹp mắt? Một giải pháp là sử dụng một function lặp lại trên domain của texture. ``sin`` và ``cos`` là hai function như vậy. Hãy áp dụng chúng cho texture và xem điều gì xảy ra. Thay thế color code hiện có trong shader bằng đoạn sau:

.. code-block:: glsl

    COLOR.xyz = vec3(sin(UV.x * 3.14159 * 4.0) * cos(UV.y * 3.14159 * 4.0) * 0.5 + 0.5);

.. image:: img/planet_sincos.webp

Không tệ lắm. Nếu quan sát xung quanh, bạn có thể thấy đường nối đã biến mất, nhưng thay vào đó, chúng ta có hiện tượng bóp ở các cực. Hiện tượng này là do cách Godot ánh xạ texture lên hình cầu trong phép
:ref:`StandardMaterial3D <class_StandardMaterial3D>`. It uses a projection technique called equirectangular
chiếu, chuyển một bản đồ hình cầu lên một mặt phẳng 2D.

.. note:: If you are interested in a little extra information on the technique, we will be converting from
          tọa độ hình cầu thành tọa độ Cartesian. Tọa độ hình cầu ánh xạ kinh độ và vĩ độ của hình cầu, trong khi tọa độ Cartesian, xét trên mọi phương diện, là một vector từ tâm hình cầu đến điểm đó.

Đối với mỗi pixel, chúng ta sẽ tính vị trí 3D của nó trên hình cầu. Từ đó, chúng ta sẽ sử dụng noise 3D để xác định giá trị màu. Bằng cách tính noise trong không gian 3D, chúng ta giải quyết được vấn đề bóp ở các cực. Để hiểu tại sao, hãy hình dung noise được tính trên bề mặt hình cầu thay vì trên mặt phẳng 2D. Khi tính trên bề mặt hình cầu, bạn không bao giờ chạm vào một cạnh, do đó không bao giờ tạo ra đường nối hoặc điểm bóp ở cực. Đoạn code sau chuyển đổi ``UVs`` thành tọa độ Cartesian.

.. code-block:: glsl

    float theta = UV.y * 3.14159;
    float phi = UV.x * 3.14159 * 2.0;
    vec3 unit = vec3(0.0, 0.0, 0.0);

    unit.x = sin(phi) * sin(theta);
    unit.y = cos(theta) * -1.0;
    unit.z = cos(phi) * sin(theta);
    unit = normalize(unit);

Và nếu chúng ta sử dụng ``unit`` làm giá trị ``COLOR`` đầu ra, chúng ta sẽ nhận được:

.. image:: img/planet_normals.webp

Bây giờ chúng ta có thể tính vị trí 3D của bề mặt hình cầu, chúng ta có thể sử dụng noise 3D để tạo hành tinh. Chúng ta sẽ sử dụng trực tiếp function noise này từ một `Shadertoy <https://www.shadertoy.com/view/Xsl3Dl>`_:

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

.. note:: All credit goes to the author, Inigo Quilez. It is published under the ``MIT`` licence.

Bây giờ, để sử dụng ``noise``, hãy thêm đoạn sau vào function ``fragment``:

.. code-block:: glsl

    float n = noise(unit * 5.0);
    COLOR.xyz = vec3(n * 0.5 + 0.5);

.. image:: img/planet_noise.webp

.. note:: In order to highlight the texture, we set the material to unshaded.

Bây giờ bạn có thể thấy noise thực sự wrap liền mạch quanh hình cầu. Tuy nhiên, nó hoàn toàn không giống hành tinh mà bạn đã được hứa hẹn. Vì vậy, hãy chuyển sang một thứ nhiều màu sắc hơn.

Tô màu cho hành tinh
--------------------

Bây giờ hãy tạo màu cho hành tinh. Có nhiều cách để thực hiện việc này, nhưng hiện tại, chúng ta sẽ dùng một gradient giữa nước và đất.

Để tạo gradient trong GLSL, chúng ta sử dụng function ``mix``. ``mix`` nhận hai giá trị để nội suy giữa chúng và một đối số thứ ba để chọn mức độ nội suy giữa hai giá trị; về bản chất, nó *trộn* hai giá trị với nhau. Trong các API khác, function này thường được gọi là ``lerp``. Tuy nhiên, ``lerp`` thường được dành cho việc trộn hai giá trị float với nhau; ``mix`` có thể nhận mọi giá trị, dù đó là float hay kiểu vector.

.. code-block:: glsl

    COLOR.xyz = mix(vec3(0.05, 0.3, 0.5), vec3(0.9, 0.4, 0.1), n * 0.5 + 0.5);

Màu đầu tiên là màu xanh dương của đại dương. Màu thứ hai là một màu hơi đỏ (vì mọi hành tinh ngoài hành tinh đều cần địa hình màu đỏ). Cuối cùng, chúng được trộn với nhau bằng ``n * 0.5 + 0.5``. ``n`` thay đổi mượt mà trong khoảng từ ``-1`` đến ``1``. Vì vậy, chúng ta ánh xạ nó vào khoảng ``0-1`` mà ``mix`` yêu cầu. Bây giờ bạn có thể thấy màu sắc thay đổi giữa xanh dương và đỏ.

.. image:: img/planet_noise_color.webp

Điều đó hơi mờ hơn mức chúng ta muốn. Các hành tinh thường có ranh giới tương đối rõ ràng giữa đất liền và biển. Để thực hiện điều đó, chúng ta sẽ thay đổi hạng tử cuối thành ``smoothstep(-0.1, 0.0, n)``. Và do đó, toàn bộ dòng sẽ trở thành:

.. code-block:: glsl

    COLOR.xyz = mix(vec3(0.05, 0.3, 0.5), vec3(0.9, 0.4, 0.1), smoothstep(-0.1, 0.0, n));

``smoothstep`` trả về ``0`` nếu đối số thứ ba nhỏ hơn đối số thứ nhất, và ``1`` nếu đối số thứ ba lớn hơn đối số thứ hai; nó trộn mượt mà giữa ``0`` và ``1`` nếu số thứ ba nằm giữa số thứ nhất và số thứ hai. Vì vậy, trong dòng này, ``smoothstep`` trả về ``0`` bất cứ khi nào ``n`` nhỏ hơn ``-0.1``, và trả về ``1`` bất cứ khi nào ``n`` lớn hơn ``0``.

.. image:: img/planet_noise_smooth.webp

Thêm một điều nữa để khiến nó giống hành tinh hơn một chút. Đất liền không nên có dạng quá nhão; hãy làm cho các cạnh gồ ghề hơn một chút. Một mẹo thường được sử dụng trong shader để tạo địa hình trông gồ ghề bằng noise là xếp chồng các lớp noise ở nhiều tần số khác nhau. Chúng ta dùng một lớp để tạo cấu trúc tổng thể nhão của các lục địa. Sau đó, một lớp khác phá vỡ các cạnh đôi chút, rồi một lớp khác nữa, v.v. Việc chúng ta sẽ làm là tính ``n`` bằng bốn dòng shader code thay vì chỉ một dòng. ``n`` trở thành:

.. code-block:: glsl

    float n = noise(unit * 5.0) * 0.5;
    n += noise(unit * 10.0) * 0.25;
    n += noise(unit * 20.0) * 0.125;
    n += noise(unit * 40.0) * 0.0625;

Và bây giờ hành tinh trông như sau:

.. image:: img/planet_noise_fbm.webp

Tạo đại dương
-------------

Một điều cuối cùng để khiến nó trông giống một hành tinh hơn. Đại dương và đất liền phản chiếu ánh sáng khác nhau. Vì vậy, chúng ta muốn đại dương sáng bóng hơn đất liền một chút. Chúng ta có thể thực hiện điều này bằng cách truyền giá trị thứ tư vào channel ``alpha`` của ``COLOR`` đầu ra và sử dụng nó làm bản đồ Roughness.

.. code-block:: glsl

    COLOR.a = 0.3 + 0.7 * smoothstep(-0.1, 0.0, n);

Dòng này trả về ``0.3`` cho nước và ``1.0`` cho đất liền. Điều này có nghĩa là đất liền sẽ khá thô, trong khi nước sẽ khá mịn.

Sau đó, trong material, dưới phần "Metallic", hãy đảm bảo ``Metallic`` được đặt thành ``0`` và ``Specular`` được đặt thành ``1``. Lý do là nước phản chiếu ánh sáng rất tốt nhưng không mang tính metallic. Các giá trị này không chính xác về mặt vật lý, nhưng đủ tốt cho bản demo này.

Tiếp theo, dưới phần "Roughness", đặt roughness texture thành một
:ref:`Viewport Texture <class_ViewportTexture>` pointing to our planet texture :ref:`SubViewport <class_SubViewport>`.
Cuối cùng, đặt ``Texture Channel`` thành ``Alpha``. Điều này hướng dẫn renderer sử dụng channel ``alpha`` của ``COLOR`` đầu ra làm giá trị ``Roughness``.

.. image:: img/planet_ocean.webp

Bạn sẽ nhận thấy rằng hầu như không có gì thay đổi, ngoại trừ việc hành tinh không còn phản chiếu bầu trời nữa. Điều này xảy ra vì theo mặc định, khi một đối tượng được render với giá trị alpha, nó sẽ được vẽ dưới dạng một đối tượng trong suốt phủ lên nền. Và vì nền mặc định của :ref:`SubViewport <class_SubViewport>` là opaque, kênh ``alpha`` của
:ref:`Viewport Texture <class_ViewportTexture>` is ``1``, resulting in the planet texture being
được vẽ với màu nhạt hơn một chút và giá trị ``Roughness`` là ``1`` ở mọi nơi. Để khắc phục điều này, chúng ta vào :ref:`SubViewport <class_SubViewport>` và bật thuộc tính "Transparent Bg". Vì hiện tại chúng ta đang render một đối tượng trong suốt chồng lên một đối tượng trong suốt khác, chúng ta muốn bật ``blend_premul_alpha``:

.. code-block:: glsl

    render_mode blend_premul_alpha;

Thao tác này sẽ pre-multiply màu theo giá trị ``alpha`` rồi blend chúng lại với nhau một cách chính xác. Thông thường, khi blend một màu trong suốt lên trên một màu trong suốt khác, ngay cả khi nền có ``alpha`` bằng ``0`` (như trong trường hợp này), bạn sẽ gặp các vấn đề màu bị loang kỳ lạ. Việc đặt ``blend_premul_alpha`` sẽ khắc phục điều đó.

Bây giờ, hành tinh sẽ trông như đang phản chiếu ánh sáng trên đại dương nhưng không phản chiếu trên đất liền. Di chuyển quanh :ref:`OmniLight3D <class_OmniLight3D>` trong scene để bạn có thể thấy hiệu ứng phản chiếu trên đại dương.

.. image:: img/planet_ocean_reflect.webp

Vậy là xong. Một hành tinh được tạo theo quy trình (procedural) bằng :ref:`SubViewport <class_SubViewport>`.
