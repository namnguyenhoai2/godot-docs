.. _doc_2d_lights_and_shadows:

Ánh sáng và bóng 2D
===================

Giới thiệu
----------

Theo mặc định, các scene 2D trong Godot không được chiếu sáng, không hiển thị ánh sáng và bóng. Mặc dù cách này giúp kết xuất nhanh, các scene không được chiếu sáng có thể trông đơn điệu. Godot cung cấp khả năng sử dụng ánh sáng và bóng 2D theo thời gian thực, có thể cải thiện đáng kể cảm nhận về chiều sâu trong project của bạn.

.. figure:: img/2d_lights_and_shadows_disabled.webp
   :align: center
   :alt: Không có ánh sáng hoặc bóng 2D, scene không được chiếu sáng

   Không có ánh sáng hoặc bóng 2D, scene không được chiếu sáng

.. figure:: img/2d_lights_and_shadows_enabled_no_shadows.webp
   :align: center
   :alt: Đã bật ánh sáng 2D (không có bóng)

   Đã bật ánh sáng 2D (không có bóng)

.. figure:: img/2d_lights_and_shadows_enabled.webp
   :align: center
   :alt: Đã bật ánh sáng và bóng 2D

   Đã bật ánh sáng và bóng 2D

Node
----

Có một số node tham gia vào một thiết lập chiếu sáng 2D hoàn chỉnh:

- :ref:`CanvasModulate <class_CanvasModulate>` (để làm tối phần còn lại của scene)
- :ref:`PointLight2D <class_PointLight2D>` (dành cho ánh sáng đa hướng hoặc ánh sáng điểm)
- :ref:`DirectionalLight2D <class_DirectionalLight2D>` (dành cho ánh sáng mặt trời hoặc ánh sáng mặt trăng)
- :ref:`LightOccluder2D <class_LightOccluder2D>` (dành cho các đối tượng đổ bóng của ánh sáng)
- Các node 2D khác nhận ánh sáng, chẳng hạn như Sprite2D hoặc TileMapLayer.

:ref:`CanvasModulate <class_CanvasModulate>` được dùng để làm tối scene bằng cách chỉ định một màu đóng vai trò là màu "môi trường" cơ sở. Đây là màu chiếu sáng cuối cùng ở những khu vực *not* được bất kỳ ánh sáng 2D nào chiếu tới. Nếu không có node CanvasModulate, scene cuối cùng sẽ trông quá sáng vì ánh sáng 2D chỉ làm sáng vẻ ngoài vốn không được chiếu sáng (trông như đã được chiếu sáng hoàn toàn).

:ref:`Sprite2Ds <class_Sprite2D>` được dùng để hiển thị texture cho các vùng sáng, nền và các đối tượng đổ bóng.

:ref:`PointLight2Ds <class_PointLight2D>` được dùng để chiếu sáng scene. Cách hoạt động thông thường của ánh sáng là phủ một texture đã chọn lên phần còn lại của scene để mô phỏng ánh sáng.

:ref:`LightOccluder2Ds <class_LightOccluder2D>` được dùng để cho shader biết những phần nào của scene tạo bóng. Các vật cản này có thể được đặt dưới dạng node độc lập hoặc là một phần của node TileMapLayer.

Bóng chỉ xuất hiện trên các khu vực được :ref:`PointLight2D <class_PointLight2D>` phủ và hướng của chúng dựa trên tâm của
:ref:`Light <class_PointLight2D>`.

.. note::

    Màu nền **not** nhận bất kỳ ánh sáng nào. Nếu muốn ánh sáng chiếu lên nền, bạn cần thêm một thành phần trực quan đại diện cho nền, chẳng hạn như Sprite2D.

    Các thuộc tính **Region** của Sprite2D có thể hữu ích để nhanh chóng tạo texture nền lặp lại, nhưng hãy nhớ đặt **Texture > Repeat** thành **Enabled** trong các thuộc tính của Sprite2D.

Ánh sáng điểm
-------------

Ánh sáng điểm (còn gọi là ánh sáng theo vị trí) là thành phần phổ biến nhất trong chiếu sáng 2D. Ánh sáng điểm có thể được dùng để biểu diễn ánh sáng từ đuốc, lửa, đạn, v.v.

PointLight2D cung cấp các thuộc tính sau để điều chỉnh trong inspector:

- **Texture:** Texture được dùng làm nguồn sáng. Kích thước của texture xác định kích thước của ánh sáng. Texture có thể có kênh alpha, hữu ích khi sử dụng chế độ hòa trộn **Mix** của Light2D, nhưng không bắt buộc nếu sử dụng chế độ hòa trộn **Add** (mặc định) hoặc **Subtract**.
- **Offset:** Độ lệch của texture ánh sáng. Không giống như khi di chuyển node ánh sáng, thay đổi độ lệch *not* khiến bóng di chuyển.
- **Texture Scale:** Hệ số nhân cho kích thước của ánh sáng. Giá trị cao hơn sẽ làm ánh sáng mở rộng ra xa hơn. Ánh sáng lớn hơn có chi phí hiệu năng cao hơn vì ảnh hưởng đến nhiều pixel hơn trên màn hình, do đó hãy cân nhắc điều này trước khi tăng kích thước ánh sáng.
- **Height:** Chiều cao ảo của ánh sáng liên quan đến normal mapping. Theo mặc định, ánh sáng ở rất gần các bề mặt nhận ánh sáng. Điều này khiến ánh sáng hầu như không nhìn thấy được nếu sử dụng normal mapping, vì vậy hãy cân nhắc tăng giá trị này. Việc điều chỉnh chiều cao của ánh sáng chỉ tạo ra khác biệt nhìn thấy được trên các bề mặt sử dụng normal mapping.

Nếu bạn không có texture tạo sẵn để dùng cho ánh sáng, bạn có thể sử dụng texture ánh sáng điểm "trung tính" này (nhấp chuột phải > **Save Image As…**):

.. figure:: img/2d_lights_and_shadows_neutral_point_light.webp
   :align: center
   :alt: Texture ánh sáng điểm trung tính

   Texture ánh sáng điểm trung tính

Nếu cần độ suy giảm khác, bạn có thể tạo texture theo cách thủ tục bằng cách gán **New GradientTexture2D** cho thuộc tính **Texture** của ánh sáng. Sau khi tạo resource, mở rộng phần **Fill** và đặt chế độ tô thành **Radial**. Sau đó, bạn sẽ phải điều chỉnh chính gradient để bắt đầu từ trắng đục đến trắng trong suốt, đồng thời di chuyển vị trí bắt đầu về chính giữa.

Ánh sáng định hướng
-------------------

Chiếu sáng định hướng được dùng để biểu diễn ánh sáng mặt trời hoặc mặt trăng. Các tia sáng được chiếu song song với nhau, như thể mặt trời hoặc mặt trăng ở cách vô hạn so với bề mặt nhận ánh sáng.

DirectionalLight2D cung cấp các thuộc tính sau:

- **Height:** Chiều cao ảo của ánh sáng liên quan đến normal mapping (``0.0`` = song song với bề mặt, ``1.0`` = vuông góc với bề mặt). Theo mặc định, ánh sáng hoàn toàn song song với các bề mặt nhận ánh sáng. Điều này khiến ánh sáng hầu như không nhìn thấy được nếu sử dụng normal mapping, vì vậy hãy cân nhắc tăng giá trị này. Việc điều chỉnh chiều cao của ánh sáng chỉ tạo ra khác biệt trực quan trên các bề mặt sử dụng normal mapping. **Height** không ảnh hưởng đến hình dạng của bóng.
- **Max Distance:** Khoảng cách tối đa tính từ tâm camera mà các đối tượng có thể ở trước khi bóng của chúng bị loại bỏ (tính bằng pixel). Giảm giá trị này có thể ngăn các đối tượng nằm ngoài camera tạo bóng (đồng thời cải thiện hiệu năng). Zoom của Camera2D không được **Max Distance** tính đến, nghĩa là ở các giá trị zoom cao hơn, bóng sẽ có vẻ mờ đi sớm hơn khi phóng to vào một điểm nhất định.

.. note::

    Bóng định hướng sẽ luôn có vẻ dài vô hạn, bất kể giá trị của thuộc tính **Height**. Đây là hạn chế của phương pháp kết xuất bóng được sử dụng cho ánh sáng 2D trong Godot.

    Để có bóng định hướng không dài vô hạn, bạn nên tắt bóng trong DirectionalLight2D và sử dụng shader tùy chỉnh đọc từ signed distance field 2D. Distance field này được tự động tạo từ các node LightOccluder2D có trong scene.

Các thuộc tính ánh sáng chung
-----------------------------

Cả PointLight2D và DirectionalLight2D đều cung cấp các thuộc tính chung, là một phần của lớp cơ sở Light2D:

- **Enabled:** Cho phép bật/tắt khả năng hiển thị của ánh sáng. Không giống như việc ẩn node ánh sáng, tắt thuộc tính này sẽ không ẩn các node con của ánh sáng.
- **Editor Only:** Nếu bật, đèn chỉ hiển thị trong editor. Tùy chọn này sẽ tự động bị tắt trong project đang chạy.
- **Color:** Màu của đèn.
- **Energy:** Hệ số cường độ của đèn. Giá trị càng cao thì đèn càng sáng.
- **Blend Mode:** Công thức blending được sử dụng để tính toán ánh sáng. Mặc định, **Add** phù hợp với hầu hết trường hợp sử dụng. Có thể dùng **Subtract** cho các đèn âm, tuy không chính xác về mặt vật lý nhưng có thể dùng cho các hiệu ứng đặc biệt. Chế độ blend **Mix** trộn giá trị của các pixel tương ứng với texture của đèn và giá trị của các pixel bên dưới bằng phép nội suy tuyến tính.
- **Range > Z Min:** Chỉ số Z thấp nhất chịu ảnh hưởng của đèn.
- **Range > Z Max:** Chỉ số Z cao nhất chịu ảnh hưởng của đèn.
- **Range > Layer Min:** Layer hiển thị thấp nhất chịu ảnh hưởng của đèn.
- **Range > Layer Max:** Layer hiển thị cao nhất chịu ảnh hưởng của đèn.
- **Range > Item Cull Mask:** Kiểm soát các node nhận ánh sáng từ node này, dựa trên các layer hiển thị đang bật của những node khác **Occluder Light Mask**. Có thể dùng tùy chọn này để ngăn một số đối tượng nhận ánh sáng.

.. _doc_2d_lights_and_shadows_setting_up_shadows:

Thiết lập bóng đổ
-----------------

Sau khi bật thuộc tính **Shadow > Enabled** trên node PointLight2D hoặc DirectionalLight2D, ban đầu bạn sẽ không thấy khác biệt về hình ảnh. Đó là vì chưa có node nào trong scene của bạn là *occluder*, vốn được dùng làm cơ sở để tạo bóng đổ.

Để bóng đổ xuất hiện trong scene, cần thêm các node LightOccluder2D vào scene. Các node này cũng phải có các polygon occluder được thiết kế khớp với đường viền của sprite.

Ngoài resource polygon (phải được thiết lập thì mới tạo ra hiệu ứng hình ảnh), các node LightOccluder2D có 2 thuộc tính:

- **SDF Collision:** Nếu bật, occluder sẽ là một phần của *signed distance field* được tạo theo thời gian thực và có thể được sử dụng trong các shader tùy chỉnh. Khi không sử dụng shader tùy chỉnh đọc SDF này, việc bật tùy chọn này không tạo ra khác biệt về hình ảnh và không tốn thêm hiệu năng, nên tùy chọn này được bật theo mặc định để thuận tiện.
- **Occluder Light Mask:** Tùy chọn này kết hợp với thuộc tính **Shadow > Item Cull Mask** của PointLight2D và DirectionalLight2D để kiểm soát đối tượng nào tạo bóng cho từng đèn. Có thể dùng tùy chọn này để ngăn các đối tượng cụ thể tạo bóng.

Có hai cách để tạo light occluder:

Tự động tạo light occluder
~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể tự động tạo occluder từ các node Sprite2D bằng cách chọn node, nhấp vào **Sprite2D** menu ở đầu 2D editor, rồi chọn **Create LightOccluder2D Sibling**.

Trong hộp thoại xuất hiện, một đường viền sẽ bao quanh các cạnh của sprite. Nếu đường viền khớp sát với các cạnh của sprite, bạn có thể nhấp vào **OK**. Nếu đường viền nằm quá xa các cạnh của sprite (hoặc "ăn" vào các cạnh của sprite), hãy điều chỉnh **Grow (pixels)** và **Shrink (pixels)**, rồi nhấp vào **Update Preview**. Lặp lại thao tác này cho đến khi đạt được kết quả vừa ý.

Vẽ light occluder thủ công
~~~~~~~~~~~~~~~~~~~~~~~~~~

Tạo một node LightOccluder2D, sau đó chọn node và nhấp vào nút "+" ở đầu 2D editor. Khi được hỏi có tạo resource polygon hay không, chọn **Yes**. Sau đó, bạn có thể bắt đầu vẽ polygon occluder bằng cách nhấp để tạo các điểm mới. Bạn có thể xóa các điểm hiện có bằng cách nhấp chuột phải vào chúng, cũng như tạo các điểm mới từ đường hiện có bằng cách nhấp vào đường rồi kéo.

Có thể điều chỉnh các thuộc tính sau trên những đèn 2D đã bật bóng đổ:

- **Color:** Màu của các vùng bị đổ bóng. Theo mặc định, các vùng bị đổ bóng có màu đen hoàn toàn, nhưng có thể thay đổi màu này cho mục đích nghệ thuật. Kênh alpha của màu kiểm soát mức độ bóng đổ được nhuộm theo màu đã chỉ định.
- **Filter:** Chế độ filter dùng cho bóng đổ. Mặc định **None** là chế độ render nhanh nhất và rất phù hợp với các game có phong cách pixel art (do hình ảnh "blocky"). Nếu muốn bóng đổ mềm, hãy dùng **PCF5**. **PCF13** còn mềm hơn, nhưng yêu cầu nhiều tài nguyên render nhất. Chỉ nên dùng PCF13 cho một vài đèn cùng lúc do chi phí render cao.
- **Filter Smooth:** Kiểm soát mức độ làm mềm bóng đổ khi **Filter** được đặt thành **PCF5** hoặc **PCF13**. Giá trị càng cao thì bóng đổ càng mềm, nhưng có thể khiến các hiện tượng banding xuất hiện (đặc biệt với PCF5).
- **Item Cull Mask:** Kiểm soát các node LightOccluder2D tạo bóng, dựa trên thuộc tính **Occluder Light Mask** tương ứng của chúng.

.. note::

    **Lighting and shadow resolution in pixel-art games**

    Engine tính toán ánh sáng và bóng đổ 2D ở **độ phân giải pixel của Viewport**, không phải ở độ phân giải texel của texture nguồn. Hình thức của ánh sáng và bóng đổ phụ thuộc vào độ phân giải cửa sổ hoặc Viewport, không phụ thuộc vào độ phân giải của từng texture sprite.

    Nếu bạn tạo một game pixel art và muốn ánh sáng cùng bóng đổ có dạng pixel hoặc blocky, phù hợp với phong cách nghệ thuật, bộ lọc texture **Nearest** sẽ **không** tạo ra hiệu ứng này. Bộ lọc Nearest chỉ ảnh hưởng đến cách engine lấy mẫu texture — nó không thay đổi cách engine render ánh sáng và bóng đổ.

    Để tạo ánh sáng và bóng đổ dạng pixel, hãy dùng shader tùy chỉnh để sửa đổi ``LIGHT_VERTEX`` và ``SHADOW_VERTEX`` nhằm cố định việc lấy mẫu ánh sáng theo một pixel grid. Shader sau đây cố định ánh sáng theo một grid bằng hàm ``floor()``:

    .. code-block:: glsl

        shader_type canvas_item;

        uniform float pixel_size = 4.0;

        void fragment() {
            // Cố định ánh sáng và bóng đổ theo pixel grid.
            LIGHT_VERTEX.xy = floor(LIGHT_VERTEX.xy / pixel_size) * pixel_size;
            SHADOW_VERTEX = floor(SHADOW_VERTEX / pixel_size) * pixel_size;

            // Render thông thường.
            COLOR = texture(TEXTURE, UV);
        }

    Cách này hoạt động bằng việc chia vị trí cho ``pixel_size`` để chuyển sang grid space, dùng ``floor()`` để làm tròn xuống điểm grid gần nhất, sau đó nhân ngược lại để chuyển về screen space. Kết quả buộc engine lấy mẫu ánh sáng từ các vị trí grid rời rạc, tạo ra hiệu ứng dạng pixel.

    Để biết thêm thông tin về canvas item shader, hãy xem :ref:`CanvasItem shaders <doc_canvas_item_shader>`.

.. figure:: img/2d_lights_and_shadows_hard_shadow.webp
   :align: center
   :alt: Bóng đổ cứng

   Bóng đổ cứng

.. figure:: img/2d_lights_and_shadows_soft_shadow.webp
   :align: center
   :alt: Bóng đổ mềm (PCF13, Filter Smooth 1.5)

   Bóng đổ mềm (PCF13, Filter Smooth 1.5)

.. figure:: img/2d_lights_and_shadows_soft_shadow_streaks.webp
   :align: center
   :alt: Bóng đổ mềm với hiện tượng kéo vệt do Filter Smooth quá cao (PCF5, Filter Smooth 4)

   Bóng đổ mềm với hiện tượng kéo vệt do Filter Smooth quá cao (PCF5, Filter Smooth 4)

Normal và specular map
----------------------

Normal map và specular map có thể tăng cường đáng kể cảm nhận về chiều sâu của hệ thống chiếu sáng 2D. Tương tự cách chúng hoạt động trong kết xuất 3D, normal map có thể giúp ánh sáng trông bớt phẳng hơn bằng cách thay đổi cường độ tùy theo hướng của bề mặt nhận ánh sáng (trên cơ sở từng pixel). Specular map tiếp tục cải thiện hình ảnh bằng cách khiến một phần ánh sáng phản xạ trở lại người xem.

Cả PointLight2D và DirectionalLight2D đều hỗ trợ normal mapping và specular mapping. Normal map và specular map có thể được gán cho bất kỳ phần tử 2D nào, bao gồm các node kế thừa từ Node2D hoặc Control.

Normal map biểu thị hướng mà mỗi pixel đang "hướng" tới. Sau đó, engine sử dụng thông tin này để áp dụng ánh sáng chính xác lên các bề mặt 2D theo cách hợp lý về mặt vật lý. Normal map thường được tạo từ height map vẽ thủ công, nhưng cũng có thể được tự động tạo từ các texture khác.

Specular map xác định mức độ mỗi pixel phản xạ ánh sáng (và phản xạ với màu nào, nếu specular map chứa màu). Các giá trị sáng hơn sẽ tạo ra phản xạ sáng hơn tại vị trí tương ứng trên texture. Specular map thường được tạo bằng cách chỉnh sửa thủ công, sử dụng diffuse texture làm nền.

.. tip::

    Nếu không có normal map hoặc specular map cho các sprite, bạn có thể tạo chúng bằng công cụ mã nguồn mở và miễn phí `Laigter <https://azagaya.itch.io/laigter>`__.

Để thiết lập normal map và/hoặc specular map trên một node 2D, hãy tạo một resource CanvasTexture mới cho thuộc tính dùng để vẽ texture của node. Ví dụ, trên một Sprite2D:

.. figure:: img/2d_lights_and_shadows_create_canvastexture.webp
   :align: center
   :alt: Tạo resource CanvasTexture cho một node Sprite2D

   Tạo resource CanvasTexture cho một node Sprite2D

Mở rộng resource vừa tạo. Bạn sẽ thấy một số thuộc tính cần điều chỉnh:

- **Diffuse > Texture:** Texture màu cơ sở. Trong thuộc tính này, hãy tải texture bạn đang dùng cho chính sprite đó.
- **Normal Map > Texture:** Texture normal map. Trong thuộc tính này, hãy tải một texture normal map được tạo từ height map (xem mẹo ở trên).
- **Specular > Texture:** Texture specular map, dùng để điều khiển cường độ specular của từng pixel trên diffuse texture. Specular map thường ở dạng grayscale, nhưng cũng có thể chứa màu để nhân màu của các phản xạ tương ứng. Trong thuộc tính này, hãy tải một texture specular map mà bạn đã tạo (xem mẹo ở trên).
- **Specular > Color:** Bộ nhân màu cho các phản xạ specular.
- **Specular > Shininess:** Số mũ specular dùng cho các phản xạ. Giá trị thấp hơn sẽ tăng độ sáng của phản xạ và khiến chúng khuếch tán hơn, trong khi giá trị cao hơn sẽ khiến phản xạ tập trung hơn. Giá trị cao phù hợp hơn với các bề mặt trông như bị ướt.
- **Texture > Filter:** Có thể được đặt để ghi đè chế độ lọc texture, bất kể thuộc tính của node được đặt như thế nào (hoặc cài đặt project **Rendering > Textures > Canvas Textures > Default Texture Filter**).
- **Texture > Repeat:** Có thể được đặt để ghi đè chế độ lọc texture, bất kể thuộc tính của node được đặt như thế nào (hoặc cài đặt project **Rendering > Textures > Canvas Textures > Default Texture Repeat**).

Sau khi bật normal mapping, bạn có thể nhận thấy đèn của mình có vẻ yếu hơn. Để khắc phục, hãy tăng thuộc tính **Height** trên các node PointLight2D và DirectionalLight2D. Bạn cũng có thể tăng nhẹ thuộc tính **Energy** của đèn để cường độ chiếu sáng gần với mức trước khi bật normal mapping hơn.

Sử dụng sprite additive làm giải pháp thay thế nhanh hơn cho đèn 2D
-------------------------------------------------------------------

Nếu gặp vấn đề về hiệu năng khi sử dụng đèn 2D, bạn có thể cân nhắc thay thế một số đèn bằng các node Sprite2D sử dụng additive blending. Cách này đặc biệt phù hợp với các hiệu ứng động có thời gian tồn tại ngắn, chẳng hạn như đạn hoặc vụ nổ.

Sprite additive được kết xuất nhanh hơn nhiều vì không cần đi qua một rendering pipeline riêng. Ngoài ra, có thể sử dụng cách tiếp cận này với AnimatedSprite2D (hoặc Sprite2D + AnimationPlayer), cho phép tạo các "đèn" 2D có animation.

Tuy nhiên, sprite additive có một số nhược điểm so với đèn 2D:

- Công thức blending không chính xác bằng hệ thống chiếu sáng 2D "thực tế". Điều này thường không thành vấn đề ở những khu vực đủ sáng, nhưng khiến sprite additive không thể chiếu sáng chính xác các khu vực hoàn toàn tối.
- Sprite additive không thể đổ bóng vì chúng không phải là đèn.
- Sprite additive bỏ qua normal map và specular map được sử dụng trên các sprite khác.

Để hiển thị một sprite với additive blending, hãy tạo một node Sprite2D và gán texture cho nó. Trong inspector, cuộn xuống phần **CanvasItem > Material**, mở rộng phần này rồi nhấp vào danh sách thả xuống bên cạnh thuộc tính **Material**. Chọn **New CanvasItemMaterial**, nhấp vào material vừa tạo để chỉnh sửa, sau đó đặt **Blend Mode** thành **Add**.
