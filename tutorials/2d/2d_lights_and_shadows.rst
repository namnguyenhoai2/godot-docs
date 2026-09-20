.. _doc_2d_lights_and_shadows:

Ánh sáng và bóng 2D
===================

Giới thiệu
----------

Theo mặc định, các cảnh 2D trong Godot không được chiếu sáng, không hiển thị ánh sáng và bóng. Mặc dù điều này giúp kết xuất nhanh, các cảnh không được chiếu sáng có thể trông đơn điệu. Godot cung cấp khả năng sử dụng ánh sáng và bóng 2D theo thời gian thực, giúp tăng đáng kể cảm giác chiều sâu cho dự án của bạn.

.. figure:: img/2d_lights_and_shadows_disabled.webp
   :align: center
   :alt: No 2D lights or shadows, scene is unshaded

   No 2D lights or shadows, scene is unshaded

.. figure:: img/2d_lights_and_shadows_enabled_no_shadows.webp
   :align: center
   :alt: 2D lights enabled (without shadows)

   2D lights enabled (without shadows)

.. figure:: img/2d_lights_and_shadows_enabled.webp
   :align: center
   :alt: 2D lights and shadows enabled

   2D lights and shadows enabled

Node
----

Có một số node liên quan đến việc thiết lập đầy đủ hệ thống chiếu sáng 2D:

- :ref:`CanvasModulate <class_CanvasModulate>` (để làm tối phần còn lại của cảnh) - :ref:`PointLight2D <class_PointLight2D>` (dành cho ánh sáng đa hướng hoặc ánh sáng điểm) - :ref:`DirectionalLight2D <class_DirectionalLight2D>` (dành cho ánh sáng mặt trời hoặc ánh trăng) - :ref:`LightOccluder2D <class_LightOccluder2D>` (dành cho các đối tượng chắn bóng) - Các node 2D khác nhận ánh sáng, chẳng hạn như Sprite2D hoặc TileMapLayer.

:ref:`CanvasModulate <class_CanvasModulate>` is used to darken the scene by
chỉ định một màu sẽ đóng vai trò là màu "môi trường" cơ sở. Đây là màu ánh sáng cuối cùng trong những khu vực *không* được bất kỳ ánh sáng 2D nào chiếu tới. Nếu không có node CanvasModulate, cảnh cuối cùng sẽ trông quá sáng vì ánh sáng 2D chỉ làm sáng thêm diện mạo không được chiếu sáng hiện có (vốn trông như đã được chiếu sáng hoàn toàn).

:ref:`Sprite2Ds <class_Sprite2D>` are used to display the textures for the light
các đốm, nền và các đối tượng chắn bóng.

:ref:`PointLight2Ds <class_PointLight2D>` are used to light the scene. The way a
ánh sáng thường hoạt động bằng cách phủ một texture đã chọn lên phần còn lại của cảnh để mô phỏng ánh sáng.

:ref:`LightOccluder2Ds <class_LightOccluder2D>` are used to tell the shader
những phần nào của cảnh tạo bóng. Các đối tượng chắn này có thể được đặt dưới dạng node độc lập hoặc có thể là một phần của node TileMapLayer.

Bóng chỉ xuất hiện trên các khu vực được :ref:`PointLight2D <class_PointLight2D>` bao phủ và hướng của chúng dựa trên tâm của
:ref:`Light <class_PointLight2D>`.

.. note::

    Màu nền **không** nhận bất kỳ ánh sáng nào. Nếu muốn ánh sáng chiếu lên nền, bạn cần thêm một thành phần trực quan cho nền, chẳng hạn như Sprite2D.

    Các thuộc tính **Region** của Sprite2D có thể hữu ích để nhanh chóng tạo texture nền lặp lại, nhưng hãy nhớ đặt **Texture > Repeat** thành **Enabled** trong các thuộc tính của Sprite2D.

Ánh sáng điểm
-------------

Ánh sáng điểm (còn gọi là ánh sáng vị trí) là thành phần phổ biến nhất trong hệ thống chiếu sáng 2D. Ánh sáng điểm có thể được dùng để mô phỏng ánh sáng từ đuốc, lửa, đạn, v.v.

PointLight2D cung cấp các thuộc tính sau để điều chỉnh trong trình kiểm tra:

- **Texture:** Texture được dùng làm nguồn sáng. Kích thước của texture quyết định kích thước của ánh sáng. Texture có thể có kênh alpha, hữu ích khi sử dụng chế độ hòa trộn **Mix** của Light2D, nhưng không bắt buộc nếu sử dụng chế độ hòa trộn **Add** (mặc định) hoặc **Subtract**. - **Offset:** Độ lệch của texture ánh sáng. Không giống như khi di chuyển node ánh sáng, thay đổi độ lệch *không* làm bóng di chuyển. - **Texture Scale:** Hệ số nhân cho kích thước của ánh sáng. Giá trị cao hơn sẽ làm ánh sáng lan rộng hơn. Ánh sáng lớn hơn có chi phí hiệu năng cao hơn vì ảnh hưởng đến nhiều pixel hơn trên màn hình, vì vậy hãy cân nhắc điều này trước khi tăng kích thước ánh sáng. - **Height:** Độ cao ảo của ánh sáng đối với ánh xạ pháp tuyến. Theo mặc định, ánh sáng ở rất gần các bề mặt nhận ánh sáng. Điều này khiến hiệu ứng chiếu sáng hầu như không nhìn thấy nếu sử dụng ánh xạ pháp tuyến, vì vậy hãy cân nhắc tăng giá trị này. Việc điều chỉnh độ cao của ánh sáng chỉ tạo ra khác biệt nhìn thấy được trên các bề mặt sử dụng ánh xạ pháp tuyến.

Nếu không có texture dựng sẵn để dùng cho ánh sáng, bạn có thể sử dụng texture ánh sáng điểm "trung tính" này (nhấp chuột phải > **Save Image As…**):

.. figure:: img/2d_lights_and_shadows_neutral_point_light.webp
   :align: center
   :alt: Neutral point light texture

   Neutral point light texture

Nếu cần độ suy giảm khác, bạn có thể tạo texture theo thủ tục bằng cách gán **New GradientTexture2D** cho thuộc tính **Texture** của ánh sáng. Sau khi tạo tài nguyên, mở rộng phần **Fill** và đặt chế độ tô thành **Radial**. Sau đó, bạn sẽ phải điều chỉnh chính gradient để bắt đầu từ màu trắng đục sang màu trắng trong suốt, đồng thời di chuyển vị trí bắt đầu vào chính giữa.

Ánh sáng định hướng
-------------------

Chiếu sáng định hướng được dùng để mô phỏng ánh sáng mặt trời hoặc ánh trăng. Các tia sáng được phát ra song song với nhau, như thể mặt trời hoặc mặt trăng ở cách vô hạn so với bề mặt nhận ánh sáng.

DirectionalLight2D cung cấp các thuộc tính sau:

- **Height:** Độ cao ảo của ánh sáng đối với ánh xạ pháp tuyến (``0.0`` = song song với các bề mặt, ``1.0`` = vuông góc với các bề mặt). Theo mặc định, ánh sáng hoàn toàn song song với các bề mặt nhận ánh sáng. Điều này khiến hiệu ứng chiếu sáng hầu như không nhìn thấy nếu sử dụng ánh xạ pháp tuyến, vì vậy hãy cân nhắc tăng giá trị này. Việc điều chỉnh độ cao của ánh sáng chỉ tạo ra khác biệt về hình ảnh trên các bề mặt sử dụng ánh xạ pháp tuyến. **Height** không ảnh hưởng đến hình dạng của bóng. - **Max Distance:** Khoảng cách tối đa tính từ tâm camera mà các đối tượng có thể ở trước khi bóng của chúng bị loại bỏ (tính bằng pixel). Giảm giá trị này có thể ngăn các đối tượng nằm ngoài camera tạo bóng (đồng thời cải thiện hiệu năng). Độ thu phóng của Camera2D không được **Max Distance** tính đến, điều đó có nghĩa là ở các giá trị thu phóng cao hơn, bóng sẽ có vẻ mờ dần sớm hơn khi phóng to vào một điểm cụ thể.

.. note::

    Bóng định hướng sẽ luôn có vẻ dài vô hạn, bất kể giá trị của thuộc tính **Height**. Đây là một hạn chế của phương pháp kết xuất bóng được sử dụng cho ánh sáng 2D trong Godot.

    Để có bóng định hướng không dài vô hạn, bạn nên tắt bóng trong DirectionalLight2D và sử dụng shader tùy chỉnh đọc từ trường khoảng cách có dấu 2D. Trường khoảng cách này được tự động tạo từ các node LightOccluder2D có trong cảnh.

Các thuộc tính ánh sáng chung
-----------------------------

Cả PointLight2D và DirectionalLight2D đều cung cấp các thuộc tính chung, là một phần của lớp cơ sở Light2D:

- **Enabled:** Cho phép bật/tắt khả năng hiển thị của ánh sáng. Không giống như ẩn node ánh sáng, việc tắt thuộc tính này sẽ không ẩn các node con của ánh sáng. - **Editor Only:** Nếu được bật, ánh sáng chỉ hiển thị trong trình chỉnh sửa. Nó sẽ tự động bị tắt trong dự án đang chạy. - **Color:** Màu của ánh sáng. - **Energy:** Hệ số cường độ của ánh sáng. Giá trị cao hơn tạo ra ánh sáng sáng hơn. - **Blend Mode:** Công thức hòa trộn được sử dụng để tính toán ánh sáng. **Add** mặc định phù hợp với hầu hết trường hợp sử dụng. **Subtract** có thể được dùng cho ánh sáng âm, tuy không chính xác về mặt vật lý nhưng có thể dùng cho các hiệu ứng đặc biệt. Chế độ hòa trộn **Mix** trộn giá trị của các pixel tương ứng với texture ánh sáng với giá trị của các pixel bên dưới bằng phép nội suy tuyến tính. - **Range > Z Min:** Chỉ số Z thấp nhất chịu ảnh hưởng của ánh sáng. - **Range > Z Max:** Chỉ số Z cao nhất chịu ảnh hưởng của ánh sáng. - **Range > Layer Min:** Lớp hình ảnh thấp nhất chịu ảnh hưởng của ánh sáng. - **Range > Layer Max:** Lớp hình ảnh cao nhất chịu ảnh hưởng của ánh sáng. - **Range > Item Cull Mask:** Kiểm soát các node nhận ánh sáng từ node này, tùy thuộc vào **Occluder Light Mask** của các lớp hình ảnh được bật trên các node khác. Có thể dùng thuộc tính này để ngăn một số đối tượng nhận ánh sáng.

.. _doc_2d_lights_and_shadows_setting_up_shadows:

Thiết lập bóng
--------------

Sau khi bật thuộc tính **Shadow > Enabled** trên node PointLight2D hoặc DirectionalLight2D, ban đầu bạn sẽ không thấy bất kỳ khác biệt trực quan nào. Đó là vì chưa có node nào trong cảnh của bạn có *đối tượng chắn*, vốn được dùng làm cơ sở để tạo bóng.

Để bóng xuất hiện trong cảnh, phải thêm các node LightOccluder2D vào cảnh. Các node này cũng phải có các đa giác chắn được thiết kế khớp với đường viền của sprite.

Ngoài tài nguyên đa giác (phải được thiết lập thì mới tạo ra hiệu ứng hình ảnh), các node LightOccluder2D có 2 thuộc tính:

- **SDF Collision:** Nếu được bật, đối tượng chắn sẽ là một phần của *trường khoảng cách có dấu* được tạo theo thời gian thực và có thể được dùng trong các shader tùy chỉnh. Khi không sử dụng shader tùy chỉnh đọc từ SDF này, việc bật tùy chọn này không tạo ra khác biệt về hình ảnh và không tốn thêm hiệu năng, vì vậy nó được bật mặc định để thuận tiện. - **Occluder Light Mask:** Thuộc tính này được dùng kết hợp với **Shadow > Item Cull Mask** của PointLight2D và DirectionalLight2D để kiểm soát những đối tượng tạo bóng cho từng ánh sáng. Có thể dùng thuộc tính này để ngăn các đối tượng cụ thể tạo bóng.

Có hai cách để tạo các đối tượng chắn ánh sáng:

Tự động tạo đối tượng chắn ánh sáng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể tự động tạo đối tượng chắn từ các node Sprite2D bằng cách chọn node, nhấp vào menu **Sprite2D** ở đầu trình chỉnh sửa 2D, sau đó chọn **Create LightOccluder2D Sibling**.

Trong hộp thoại xuất hiện, một đường viền sẽ bao quanh các cạnh của sprite. Nếu đường viền khớp sát với các cạnh của sprite, bạn có thể nhấp vào **OK**. Nếu đường viền nằm quá xa các cạnh của sprite (hoặc đang "ăn" vào các cạnh của sprite), hãy điều chỉnh **Grow (pixels)** và **Shrink (pixels)**, sau đó nhấp vào **Update Preview**. Lặp lại thao tác này cho đến khi đạt được kết quả ưng ý.

Tự vẽ đối tượng chắn ánh sáng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tạo một node LightOccluder2D, sau đó chọn node và nhấp vào nút "+" ở đầu trình chỉnh sửa 2D. Khi được hỏi có tạo tài nguyên đa giác hay không, hãy trả lời **Yes**. Sau đó, bạn có thể bắt đầu vẽ một đa giác chắn bằng cách nhấp để tạo các điểm mới. Bạn có thể xóa các điểm hiện có bằng cách nhấp chuột phải vào chúng, đồng thời có thể tạo các điểm mới từ đường hiện có bằng cách nhấp vào đường rồi kéo.

Có thể điều chỉnh các thuộc tính sau trên những ánh sáng 2D đã bật bóng:

- **Color:** Màu của các vùng được đổ bóng. Theo mặc định, các vùng được đổ bóng hoàn toàn có màu đen, nhưng bạn có thể thay đổi màu này cho mục đích nghệ thuật. Kênh alpha của màu kiểm soát mức độ bóng đổ được nhuộm bởi màu đã chỉ định. - **Filter:** Chế độ lọc được sử dụng cho bóng đổ. **None** mặc định có tốc độ kết xuất nhanh nhất và rất phù hợp với các trò chơi có phong cách pixel art (do hình ảnh "blocky" của nó). Nếu muốn bóng mềm, hãy sử dụng **PCF5**. **PCF13** còn mềm hơn, nhưng yêu cầu nhiều tài nguyên kết xuất nhất. Chỉ nên sử dụng PCF13 cho một vài nguồn sáng cùng lúc do chi phí kết xuất cao. - **Filter Smooth:** Kiểm soát mức độ làm mềm được áp dụng cho bóng đổ khi **Filter** được đặt thành **PCF5** hoặc **PCF13**. Giá trị cao hơn tạo ra bóng mềm hơn, nhưng có thể khiến các hiện tượng dải màu hiển thị (đặc biệt là với PCF5). - **Item Cull Mask:** Kiểm soát những node LightOccluder2D nào tạo bóng đổ, tùy thuộc vào các thuộc tính **Occluder Light Mask** tương ứng của chúng.

.. note::

    **Độ phân giải ánh sáng và bóng đổ trong các trò chơi pixel-art**

    Engine tính toán ánh sáng và bóng đổ 2D ở **độ phân giải pixel của Viewport**, không phải ở độ phân giải texel của texture nguồn. Hình thức của ánh sáng và bóng đổ phụ thuộc vào độ phân giải cửa sổ hoặc Viewport, không phụ thuộc vào độ phân giải của từng texture sprite.

    Nếu bạn tạo một trò chơi pixel-art và muốn ánh sáng, bóng đổ có dạng pixel hoặc blocky phù hợp với phong cách nghệ thuật, tính năng lọc texture **Nearest** sẽ **không** tạo ra hiệu ứng này. Lọc Nearest chỉ ảnh hưởng đến cách engine lấy mẫu texture — nó không thay đổi cách engine kết xuất ánh sáng và bóng đổ.

    Để tạo ánh sáng và bóng đổ dạng pixel, hãy sử dụng shader tùy chỉnh để sửa đổi ``LIGHT_VERTEX`` và ``SHADOW_VERTEX`` nhằm cố định việc lấy mẫu ánh sáng vào một lưới pixel. Shader sau đây cố định ánh sáng vào một lưới bằng hàm ``floor()``:

    .. code-block:: glsl

        shader_type canvas_item;

        uniform float pixel_size = 4.0;

        void fragment() {
            // Snap lighting and shadows to pixel grid.
            LIGHT_VERTEX.xy = floor(LIGHT_VERTEX.xy / pixel_size) * pixel_size;
            SHADOW_VERTEX = floor(SHADOW_VERTEX / pixel_size) * pixel_size;

            // Normal rendering.
            COLOR = texture(TEXTURE, UV);
        }

    Cách này hoạt động bằng cách chia vị trí cho ``pixel_size`` để chuyển đổi sang không gian lưới, sử dụng ``floor()`` để làm tròn xuống đến điểm lưới gần nhất, sau đó nhân ngược lại để chuyển đổi về không gian màn hình. Kết quả buộc engine lấy mẫu ánh sáng từ các vị trí lưới rời rạc, tạo ra hiệu ứng dạng pixel.

    Để biết thêm thông tin về shader canvas item, hãy xem :ref:`CanvasItem shaders <doc_canvas_item_shader>`.

.. figure:: img/2d_lights_and_shadows_hard_shadow.webp
   :align: center
   :alt: Hard shadows

   Hard shadows

.. figure:: img/2d_lights_and_shadows_soft_shadow.webp
   :align: center
   :alt: Soft shadows (PCF13, Filter Smooth 1.5)

   Soft shadows (PCF13, Filter Smooth 1.5)

.. figure:: img/2d_lights_and_shadows_soft_shadow_streaks.webp
   :align: center
   :alt: Soft shadows with streaking artifacts due to Filter Smooth being too high (PCF5, Filter Smooth 4)

   Soft shadows with streaking artifacts due to Filter Smooth being too high (PCF5, Filter Smooth 4)

Bản đồ pháp tuyến và bản đồ phản chiếu
--------------------------------------

Bản đồ pháp tuyến và bản đồ phản chiếu có thể cải thiện đáng kể cảm giác chiều sâu của ánh sáng 2D. Tương tự cách chúng hoạt động trong kết xuất 3D, bản đồ pháp tuyến có thể giúp ánh sáng trông bớt phẳng hơn bằng cách thay đổi cường độ tùy theo hướng của bề mặt nhận ánh sáng (trên từng pixel). Bản đồ phản chiếu còn giúp cải thiện hình ảnh bằng cách khiến một phần ánh sáng phản chiếu trở lại người xem.

Cả PointLight2D và DirectionalLight2D đều hỗ trợ ánh xạ pháp tuyến và ánh xạ phản chiếu. Có thể gán bản đồ pháp tuyến và bản đồ phản chiếu cho mọi phần tử 2D, bao gồm các node kế thừa từ Node2D hoặc Control.

Bản đồ pháp tuyến biểu thị hướng mà mỗi pixel đang "hướng" tới. Engine sử dụng thông tin này để áp dụng ánh sáng chính xác cho các bề mặt 2D theo cách hợp lý về mặt vật lý. Bản đồ pháp tuyến thường được tạo từ các bản đồ độ cao vẽ thủ công, nhưng cũng có thể được tự động tạo từ các texture khác.

Bản đồ phản chiếu xác định mức độ mỗi pixel phản chiếu ánh sáng (và phản chiếu theo màu nào, nếu bản đồ phản chiếu có chứa màu). Các giá trị sáng hơn sẽ tạo ra phản xạ sáng hơn tại vị trí tương ứng trên texture. Bản đồ phản chiếu thường được tạo bằng cách chỉnh sửa thủ công, sử dụng texture khuếch tán làm cơ sở.

.. tip::

    Nếu không có bản đồ pháp tuyến hoặc bản đồ phản chiếu cho sprite, bạn có thể tạo chúng bằng công cụ mã nguồn mở và miễn phí `Laigter <https://azagaya.itch.io/laigter>`__.

Để thiết lập bản đồ pháp tuyến và/hoặc bản đồ phản chiếu trên một node 2D, hãy tạo một tài nguyên CanvasTexture mới cho thuộc tính vẽ texture của node. Ví dụ, trên một Sprite2D:

.. figure:: img/2d_lights_and_shadows_create_canvastexture.webp
   :align: center
   :alt: Creating a CanvasTexture resource for a Sprite2D node

   Creating a CanvasTexture resource for a Sprite2D node

Mở rộng tài nguyên vừa tạo. Bạn sẽ tìm thấy một số thuộc tính cần điều chỉnh:

- **Diffuse > Texture:** Texture màu cơ sở. Trong thuộc tính này, hãy tải texture mà bạn đang sử dụng cho chính sprite. - **Normal Map > Texture:** Texture bản đồ pháp tuyến. Trong thuộc tính này, hãy tải texture bản đồ pháp tuyến mà bạn đã tạo từ một bản đồ độ cao (xem mẹo ở trên). - **Specular > Texture:** Texture bản đồ phản chiếu, kiểm soát cường độ phản chiếu của từng pixel trên texture khuếch tán. Bản đồ phản chiếu thường là ảnh grayscale, nhưng cũng có thể chứa màu để nhân màu của các phản xạ tương ứng. Trong thuộc tính này, hãy tải texture bản đồ phản chiếu mà bạn đã tạo (xem mẹo ở trên). - **Specular > Color:** Bộ nhân màu cho các phản xạ. - **Specular > Shininess:** Số mũ phản chiếu được sử dụng cho các phản xạ. Các giá trị thấp hơn sẽ tăng độ sáng của phản xạ và khiến chúng khuếch tán hơn, trong khi các giá trị cao hơn sẽ khiến phản xạ tập trung hơn. Các giá trị cao phù hợp hơn với những bề mặt có vẻ ướt. - **Texture > Filter:** Có thể được đặt để ghi đè chế độ lọc texture, bất kể thuộc tính của node được đặt như thế nào (hoặc thiết lập dự án **Rendering > Textures > Canvas Textures > Default Texture Filter**). - **Texture > Repeat:** Có thể được đặt để ghi đè chế độ lặp texture, bất kể thuộc tính của node được đặt như thế nào (hoặc thiết lập dự án **Rendering > Textures > Canvas Textures > Default Texture Repeat**).

Sau khi bật ánh xạ pháp tuyến, bạn có thể nhận thấy ánh sáng trông yếu hơn. Để khắc phục, hãy tăng thuộc tính **Height** trên các node PointLight2D và DirectionalLight2D. Bạn cũng có thể muốn tăng nhẹ thuộc tính **Energy** của ánh sáng để gần với cường độ ánh sáng trước khi bật ánh xạ pháp tuyến hơn.

Sử dụng sprite cộng màu như một giải pháp thay thế nhanh hơn cho đèn 2D
-----------------------------------------------------------------------

Nếu gặp vấn đề về hiệu năng khi sử dụng đèn 2D, bạn có thể thay thế một số đèn bằng các node Sprite2D sử dụng chế độ hòa trộn cộng màu. Cách này đặc biệt phù hợp với các hiệu ứng động có thời lượng ngắn, chẳng hạn như đạn hoặc vụ nổ.

Sprite cộng màu kết xuất nhanh hơn nhiều vì không cần đi qua một pipeline kết xuất riêng. Ngoài ra, có thể sử dụng cách tiếp cận này với AnimatedSprite2D (hoặc Sprite2D + AnimationPlayer), cho phép tạo ra các "đèn" 2D động.

Tuy nhiên, sprite cộng màu có một số nhược điểm so với đèn 2D:

- Công thức hòa trộn không chính xác bằng ánh sáng 2D "thực tế". Điều này thường không gây vấn đề ở những khu vực được chiếu sáng đầy đủ, nhưng khiến sprite cộng màu không thể chiếu sáng chính xác các khu vực hoàn toàn tối. - Sprite cộng màu không thể tạo bóng đổ vì chúng không phải là đèn. - Sprite cộng màu bỏ qua các bản đồ pháp tuyến và bản đồ phản chiếu được sử dụng trên các sprite khác.

Để hiển thị một sprite với chế độ hòa trộn cộng màu, hãy tạo một node Sprite2D và gán texture cho node đó. Trong inspector, cuộn xuống phần **CanvasItem > Material**, mở rộng phần này rồi nhấp vào danh sách thả xuống bên cạnh thuộc tính **Material**. Chọn **New CanvasItemMaterial**, nhấp vào material vừa tạo để chỉnh sửa, sau đó đặt **Blend Mode** thành **Add**.
