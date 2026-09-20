.. _doc_standard_material_3d:

Standard Material 3D và ORM Material 3D
=======================================

Giới thiệu
----------

``StandardMaterial3D`` và ``ORMMaterial3D`` (Occlusion, Roughness, Metallic) là các material 3D mặc định nhằm cung cấp hầu hết các tính năng mà artist thường tìm kiếm ở một material mà không cần viết shader code. Tuy nhiên, chúng có thể được chuyển đổi thành shader code nếu cần thêm chức năng.

Tutorial này giải thích các tham số có trong cả hai material.

Có 4 cách để thêm các material này vào một object. Có thể thêm material vào thuộc tính *Material* của mesh. Có thể thêm material vào thuộc tính *Material* của node sử dụng mesh (chẳng hạn như node MeshInstance3D), thuộc tính *Material Override* của node sử dụng mesh và *Material Overlay*.

.. image:: img/add_material.webp

Nếu bạn thêm material vào chính mesh, mỗi khi mesh đó được sử dụng, nó sẽ có material đó. Nếu bạn thêm material vào node sử dụng mesh, material này chỉ được node đó sử dụng; nó cũng sẽ ghi đè thuộc tính material của mesh. Nếu material được thêm vào thuộc tính *Material Override* của node, nó chỉ được node đó sử dụng. Nó cũng sẽ ghi đè thuộc tính material thông thường của node và thuộc tính material của mesh.

Thuộc tính *Material Overlay* sẽ render một material **lên trên** material hiện tại đang được mesh sử dụng. Ví dụ, bạn có thể dùng thuộc tính này để tạo hiệu ứng lá chắn trong suốt trên một mesh.

Thiết lập BaseMaterial 3D
-------------------------

StandardMaterial3D có nhiều thiết lập quyết định diện mạo của một material. Tất cả các thiết lập này đều nằm trong danh mục BaseMaterial3D

.. image:: img/spatial_material1.webp

ORM material gần như hoàn toàn giống, với một điểm khác biệt. Thay vì có các thiết lập và texture riêng cho occlusion, roughness và metallic, nó sử dụng một texture ORM duy nhất. Các kênh màu khác nhau của texture đó được dùng cho từng tham số. Các chương trình như Substance Painter và Armor Paint sẽ cho phép bạn export theo định dạng này; với hai chương trình này, bạn có thể sử dụng export preset cho unreal engine, vốn cũng sử dụng texture ORM.

Độ trong suốt
-------------

Theo mặc định, material trong Godot là opaque. Điều này giúp render nhanh, nhưng có nghĩa là không thể nhìn xuyên qua material, ngay cả khi bạn sử dụng texture trong suốt trong thuộc tính **Albedo > Texture** (hoặc đặt **Albedo > Color** thành một màu trong suốt).

Để có thể nhìn xuyên qua một material, material đó cần được đặt thành *transparent*. Godot cung cấp một số transparency mode:

- **Disabled:** Material là opaque. Đây là mode render nhanh nhất và hỗ trợ tất cả các tính năng rendering.

- **Alpha:** Material là transparent. Các vùng bán trong suốt được vẽ bằng blending. Mode này render chậm, nhưng cho phép tạo độ trong suốt một phần (còn gọi là translucency). Material sử dụng alpha blending cũng không thể đổ bóng và không hiển thị trong screen-space reflection.

  - **Alpha** phù hợp với particle effect và VFX.

- **Alpha Scissor:** Material là transparent. Các vùng bán trong suốt có độ opacity thấp hơn **Alpha Scissor Threshold** sẽ không được vẽ (với độ opacity cao hơn ngưỡng này, chúng sẽ được vẽ như opaque). Mode này render nhanh hơn Alpha và không gặp các vấn đề về sắp xếp transparency. Nhược điểm là nó tạo ra độ trong suốt kiểu "all or nothing", không thể có các giá trị trung gian. Material sử dụng alpha scissor có thể đổ bóng.

  - **Alpha Scissor** lý tưởng cho foliage và fence, vì chúng có các cạnh rõ ràng và cần được sắp xếp chính xác để hiển thị đẹp.

- **Alpha Hash:** Material là transparent. Các vùng bán trong suốt được vẽ bằng dithering. Đây cũng là độ trong suốt kiểu "all or nothing", nhưng dithering giúp biểu thị các vùng bán opaque với độ chính xác giới hạn, tùy thuộc vào độ phân giải của viewport. Material sử dụng alpha hash có thể đổ bóng.

  - **Alpha Hash** phù hợp với tóc có vẻ ngoài chân thực, dù tóc được stylize có thể hoạt động tốt hơn với alpha scissor.

- **Depth Pre-Pass:** Đầu tiên, các pixel hoàn toàn opaque của object được render qua opaque pipeline, sau đó phần còn lại được render bằng alpha blending. Điều này cho phép việc sắp xếp transparency nhìn chung là *đúng* (mặc dù không hoàn toàn, vì các vùng bán trong suốt vẫn có thể được sắp xếp không chính xác). Material sử dụng depth prepass có thể đổ bóng.

.. note::

    Godot sẽ tự động buộc material trở thành transparent với alpha blending nếu thỏa mãn *bất kỳ* điều kiện nào sau đây:

    - Đặt transparency mode thành **Alpha** (như mô tả ở đây). - Đặt blend mode khác với **Mix** mặc định - Bật **Refraction**, **Proximity Fade** hoặc **Distance Fade**.

So sánh transparency bằng alpha blending (bên trái) và alpha scissor (bên phải):

.. image:: img/spatial_material12.png

.. warning::

    Transparency bằng alpha blending có một số
    :ref:`limitations <doc_3d_rendering_limitations_transparency_sorting>`:

    - Material dùng alpha blending render chậm hơn đáng kể, đặc biệt khi chúng chồng lên nhau. - Material dùng alpha blending có thể gặp vấn đề về sắp xếp khi các bề mặt transparent chồng lên nhau. Điều này có nghĩa là các bề mặt có thể được render không đúng thứ tự, khiến các bề mặt ở phía sau trông như ở phía trước những bề mặt thực sự gần camera hơn. - Material dùng alpha blending không đổ bóng, dù chúng có thể nhận bóng. - Material dùng alpha blending không xuất hiện trong bất kỳ reflection nào (ngoại trừ reflection probe). - Screen-space reflection và reflection SDFGI sắc nét không xuất hiện trên material dùng alpha blending. Khi SDFGI được bật, reflection thô được dùng làm phương án dự phòng bất kể roughness của material.

    Trước khi sử dụng transparency mode **Alpha**, luôn cân nhắc xem một transparency mode khác có phù hợp hơn với nhu cầu của bạn hay không.

.. _doc_standard_material_3d_alpha_antialiasing:

Alpha Antialiasing
~~~~~~~~~~~~~~~~~~

.. note::

    Thuộc tính này chỉ hiển thị khi transparency mode là **Alpha Scissor** hoặc **Alpha Hash**.

Mặc dù material alpha scissor và alpha hash render nhanh hơn material dùng alpha blending, chúng tạo ra các cạnh rõ giữa vùng opaque và transparent. Mặc dù có thể sử dụng :ref:`antialiasing techniques <doc_3d_antialiasing>` dựa trên post-processing như FXAA và TAA, điều này không phải lúc nào cũng được mong muốn vì các kỹ thuật này thường khiến kết quả cuối cùng trông mờ hơn hoặc xuất hiện các artifact ghosting.

Có 3 alpha antialiasing mode:

- **Disabled:** Không có alpha antialiasing. Các cạnh của material transparent sẽ bị aliasing trừ khi sử dụng giải pháp antialiasing dựa trên post-processing. - **Alpha Edge Blend:** Tạo ra chuyển tiếp mượt giữa các vùng opaque và transparent. Còn được gọi là "alpha to coverage". - **Alpha Edge Clip:** Tạo ra chuyển tiếp rõ nhưng vẫn được antialiasing giữa các vùng opaque và transparent. Còn được gọi là "alpha to coverage + alpha to one".

Khi alpha antialiasing mode được đặt thành **Alpha Edge Blend** hoặc **Alpha Edge Clip**, một thuộc tính **Alpha Antialiasing Edge** mới sẽ hiển thị bên dưới trong inspector. Thuộc tính này kiểm soát ngưỡng bên dưới đó các pixel sẽ được làm transparent. Mặc dù bạn đã xác định một alpha scissor threshold (chỉ khi sử dụng **Alpha Scissor**), ngưỡng bổ sung này được dùng để chuyển tiếp mượt giữa các pixel opaque và transparent. **Alpha Antialiasing Edge** *luôn luôn* phải được đặt thành giá trị nhỏ hơn nghiêm ngặt so với alpha scissor threshold. Giá trị mặc định ``0.3`` là hợp lý khi alpha scissor có threshold là ``0.5``, nhưng hãy nhớ điều chỉnh alpha antialiasing edge khi thay đổi alpha scissor threshold.

Nếu bạn thấy hiệu ứng antialiasing chưa đủ hiệu quả, hãy thử tăng **Alpha Antialiasing Edge**, đồng thời bảo đảm giá trị này thấp hơn **Alpha Scissor Threshold** (nếu material sử dụng alpha scissor). Ngược lại, nếu bạn nhận thấy diện mạo của texture thay đổi rõ rệt khi camera tiến gần material hơn, hãy thử giảm **Alpha Antialiasing Edge**.

.. important::

    Để có kết quả tốt nhất, MSAA 3D nên được đặt ít nhất là 2× trong Project Settings khi sử dụng alpha antialiasing. Điều này là do tính năng này dựa vào alpha to coverage, một tính năng do MSAA cung cấp.

    Nếu không có MSAA, một mẫu dithering cố định sẽ được áp dụng lên các cạnh của material, nhưng không quá hiệu quả trong việc làm mượt các cạnh (dù vẫn có thể hỗ trợ đôi chút).

Blend Mode
~~~~~~~~~~

Kiểm soát blend mode của material. Hãy lưu ý rằng bất kỳ mode nào khác *Mix* đều buộc object đi qua transparent pipeline.

* **Mix:** Blend mode mặc định, alpha kiểm soát mức độ hiển thị của object. * **Add:** Màu cuối cùng của object được cộng vào màu của màn hình, phù hợp với flare hoặc một số hiệu ứng giống lửa. * **Subtract:** Màu cuối cùng của object được trừ khỏi màu của màn hình. * **Multiply:** Màu cuối cùng của object được nhân với màu của màn hình. * **Premultiplied Alpha:** Màu của object được kỳ vọng là đã được nhân với alpha. Mode này hoạt động như **Add** khi alpha là ``0.0`` (hoàn toàn trong suốt) và như **Mix** khi alpha là ``1.0`` (opaque).

.. image:: img/spatial_material8.png

Cull Mode
~~~~~~~~~

Xác định mặt nào của object không được vẽ khi các backface được render:

* **Back:** Mặt sau của object bị cull khi không hiển thị (mặc định). * **Front:** Mặt trước của object bị cull khi không hiển thị. * **Disabled:** Dùng cho các object có hai mặt (không thực hiện culling).

.. note::

  Theo mặc định, Blender tắt tính năng loại bỏ mặt sau (backface culling) trên các material và sẽ export material sao cho khớp với cách chúng được render trong Blender. Điều này có nghĩa là các material trong Godot sẽ có chế độ cull được đặt thành **Disabled**. Điều này có thể làm giảm hiệu năng vì các mặt sau vẫn được render, ngay cả khi chúng đang bị các mặt khác loại bỏ. Để khắc phục, hãy bật **Backface Culling** trong tab Materials của Blender, sau đó export lại scene sang glTF.

Depth Draw Mode
~~~~~~~~~~~~~~~

Chỉ định thời điểm bắt buộc phải thực hiện việc render depth.

* **Opaque Only (default):** Depth chỉ được vẽ cho các object opaque. * **Always:** Depth được vẽ cho cả object opaque và transparent. * **Never:** Không thực hiện việc vẽ depth (đừng nhầm tùy chọn này với tùy chọn No Depth Test bên dưới). * **Depth Pre-Pass:** Đối với các object transparent, trước tiên sẽ thực hiện một opaque pass với các phần opaque, sau đó vẽ phần transparency bên trên. Hãy dùng tùy chọn này với cỏ hoặc tán cây transparent.

.. image:: img/material_depth_draw.png

No Depth Test
~~~~~~~~~~~~~

Để các object ở gần xuất hiện phía trên các object ở xa, depth testing được thực hiện. Việc tắt tùy chọn này khiến các object xuất hiện phía trên (hoặc phía dưới) mọi thứ khác.

Việc tắt tùy chọn này phù hợp nhất khi vẽ các indicator trong world space và hoạt động rất hiệu quả cùng với thuộc tính *Render Priority* của Material (xem cuối trang này).

.. image:: img/spatial_material3.png

Depth Test
~~~~~~~~~~

Bạn có thể dùng tùy chọn này để đảo ngược depth test tiêu chuẩn. Khi được đặt thành **Inverted**, object sẽ chỉ xuất hiện khi bị che khuất và sẽ bị ẩn trong các trường hợp khác.

Tùy chọn này không có tác dụng nếu **No Depth Test** được bật.

.. image:: img/material_depth_test.webp

Shading
-------

Shading mode
~~~~~~~~~~~~

Material hỗ trợ ba shading mode: **Per-Pixel**, **Per-Vertex** và **Unshaded**.

.. figure:: img/standard_material_shading_modes.webp
  :align: center
  :alt: Three spheres showing the Per-Pixel, Per-Vertex, and Unshaded modes.

Shading mode **Per-Pixel** tính toán lighting cho từng pixel và phù hợp với hầu hết trường hợp sử dụng. Tuy nhiên, trong một số trường hợp, bạn có thể muốn tăng hiệu năng bằng cách sử dụng một shading mode khác.

Shading mode **Per-Vertex**, thường được gọi là "vertex shading" hoặc "vertex lighting", thay vào đó tính toán lighting một lần cho mỗi vertex và nội suy kết quả giữa từng pixel.

Trên các thiết bị cấp thấp hoặc mobile, sử dụng per-vertex lighting có thể tăng đáng kể hiệu năng rendering. Khi render nhiều layer transparency, chẳng hạn khi sử dụng particle system, dùng per-vertex shading có thể cải thiện hiệu năng, đặc biệt khi camera ở gần các particle.

Bạn cũng có thể sử dụng per-vertex lighting để tạo ra phong cách retro.

.. figure:: img/standard_material_shading_modes_textured.webp
  :align: center
  :alt: Two cubes with a brick texture, one shaded and one unshaded.

  Texture from `AmbientCG <https://ambientcg.com/view?id=Bricks051>`__

Shading mode **Unshaded** hoàn toàn không tính toán lighting. Thay vào đó, màu **Albedo** được xuất trực tiếp. Light sẽ hoàn toàn không ảnh hưởng đến material, và các material unshaded thường sẽ trông sáng hơn đáng kể so với các material shaded.

Render unshaded hữu ích cho một số hiệu ứng hình ảnh cụ thể. Nếu cần hiệu năng tối đa, bạn cũng có thể dùng nó cho particle hoặc trên các thiết bị cấp thấp hay mobile.

Diffuse Mode
~~~~~~~~~~~~

Chỉ định algorithm được sử dụng cho việc khuếch tán ánh sáng khi ánh sáng chiếu vào object. Mặc định là **Burley**. Các mode khác cũng khả dụng:

* **Burley:** Mode mặc định, algorithm diffuse PBS Disney Principled nguyên bản. * **Lambert:** Không bị ảnh hưởng bởi roughness. * **Lambert Wrap:** Mở rộng Lambert để bao phủ hơn 90 độ khi roughness tăng. Hoạt động rất tốt với tóc và mô phỏng subsurface scattering giá rẻ. Implementation này bảo toàn năng lượng. * **Toon:** Tạo đường cắt cứng cho lighting, với độ làm mượt bị ảnh hưởng bởi roughness. Bạn nên tắt sky contribution trong các thiết lập ambient light của environment hoặc tắt ambient light trong StandardMaterial3D để đạt hiệu ứng tốt hơn.

.. image:: img/spatial_material6.webp

Specular Mode
~~~~~~~~~~~~~

Chỉ định cách specular blob được render. Specular blob thể hiện hình dạng của nguồn sáng phản chiếu trên object.

* **SchlickGGX:** Blob phổ biến nhất được các 3D engine PBR sử dụng hiện nay. * **Toon:** Tạo toon blob, thay đổi kích thước tùy theo roughness. * **Disabled:** Đôi khi blob gây vướng. Hãy loại bỏ nó!

.. image:: img/spatial_material7.webp

Disable Ambient Light
~~~~~~~~~~~~~~~~~~~~~

Khiến object không nhận bất kỳ loại ambient lighting nào vốn có thể chiếu sáng nó.

Disable Fog
~~~~~~~~~~~

Khiến object không bị ảnh hưởng bởi fog dựa trên depth hoặc volumetric fog. Điều này hữu ích cho particle hoặc các material được blend additive, vốn nếu không sẽ hiển thị hình dạng của mesh (ngay cả ở những nơi mà nó sẽ không nhìn thấy nếu không có fog).

Disable Specular Occlusion
~~~~~~~~~~~~~~~~~~~~~~~~~~

Khiến các reflection của object không bị giảm ở những nơi chúng thường bị che khuất.

Vertex Color
------------

Thiết lập này cho phép chọn hành động mặc định đối với vertex color đến từ ứng dụng 3D modeling của bạn. Theo mặc định, chúng bị bỏ qua.

Use as Albedo
~~~~~~~~~~~~~

Chọn tùy chọn này nghĩa là vertex color được sử dụng làm albedo color.

Is sRGB
~~~~~~~

Hầu hết phần mềm 3D modeling có khả năng sẽ export vertex color dưới dạng sRGB, vì vậy bật tùy chọn này sẽ giúp chúng hiển thị chính xác.

Albedo
------

*Albedo* là màu cơ sở của material, trên đó tất cả thiết lập khác hoạt động. Khi được đặt thành *Unshaded*, đây là màu duy nhất hiển thị. Trong các phiên bản Godot trước đây, channel này có tên là *Diffuse*. Việc đổi tên chủ yếu xảy ra vì trong PBR (Physically Based Rendering), màu này ảnh hưởng đến nhiều phép tính hơn chỉ riêng diffuse lighting path.

Albedo color và texture có thể được sử dụng cùng nhau vì chúng được nhân với nhau.

*Alpha channel* trong albedo color và texture cũng được sử dụng cho transparency của object. Nếu bạn dùng color hoặc texture có *alpha channel*, hãy đảm bảo bật transparency hoặc *alpha scissoring* để nó hoạt động.

Metallic
--------

Godot sử dụng metallic model thay vì các model cạnh tranh nhờ tính đơn giản của nó. Tham số này xác định mức độ phản chiếu của material. Càng phản chiếu nhiều thì diffuse/ambient light càng ảnh hưởng ít đến material và càng nhiều ánh sáng được phản chiếu. Model này được gọi là "energy-conserving".

Tham số *Specular* là mức độ tổng quát của reflectivity (không giống *Metallic*, tham số này không energy-conserving, vì vậy hãy giữ ở mức ``0.5`` và đừng thay đổi trừ khi bạn cần).

Độ reflectivity nội bộ tối thiểu là ``0.04``, vì vậy không thể tạo một material hoàn toàn không phản chiếu, cũng giống như trong đời thực.

.. image:: img/spatial_material13.png

Roughness
---------

*Roughness* ảnh hưởng đến cách reflection diễn ra. Giá trị ``0`` tạo ra một tấm gương hoàn hảo, trong khi giá trị ``1`` làm mờ hoàn toàn reflection (mô phỏng bề mặt vi mô tự nhiên). Hầu hết các loại material phổ biến có thể đạt được bằng sự kết hợp phù hợp giữa *Metallic* và *Roughness*.

.. image:: img/spatial_material14.png

Emission
--------

*Emission* chỉ định lượng ánh sáng được material phát ra (hãy nhớ rằng giá trị này không bao gồm ánh sáng chiếu lên geometry xung quanh trừ khi sử dụng :ref:`VoxelGI <doc_using_voxel_gi>` hoặc :ref:`SDFGI <doc_using_sdfgi>`). Giá trị này được cộng vào hình ảnh cuối cùng và không bị ảnh hưởng bởi lighting khác trong scene.

.. image:: img/spatial_material15.png

Normal map
----------

Normal mapping cho phép bạn đặt một texture đại diện cho chi tiết hình dạng nhỏ hơn. Nó không thay đổi geometry, chỉ thay đổi góc tới của ánh sáng. Trong Godot, chỉ các channel đỏ và xanh lá của normal map được sử dụng để có compression tốt hơn và compatibility rộng hơn.

.. image:: img/spatial_material16.png

.. note::

  Godot yêu cầu normal map sử dụng tọa độ X+, Y+ và Z+; kiểu này được gọi là OpenGL style. Nếu bạn đã import một material được tạo để dùng với engine khác, nó có thể là DirectX style; trong trường hợp đó, normal map cần được chuyển đổi để trục Y bị lật.

  Bạn có thể tìm thấy thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `tại đây <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

.. _doc_standard_material_3d_bent_normal_map:

Bent normal map
---------------

Bent normal map mô tả hướng trung bình của ambient lighting. Khác với normal map thông thường, nó được dùng để cải thiện cách material phản ứng với lighting thay vì thêm surface detail.

Điều này đạt được theo hai cách:

* Indirect diffuse lighting được điều chỉnh để khớp với global illumination hơn. * Nếu specular occlusion được bật, nó được tính toán bằng bent normal và ambient occlusion thay vì chỉ từ ambient light. Điều này bao gồm screen-space ambient occlusion (SSAO) và các nguồn ambient occlusion khác.

.. image:: img/spatial_material_bentnormals.webp

Godot chỉ sử dụng các channel đỏ và xanh lá của bent normal map để có compression tốt hơn và compatibility rộng hơn.

Khi tạo bent normal map, cần có ba điều để nó hoạt động chính xác trong Godot:

* Phải sử dụng **cosine distribution** của các tia khi baking. * Texture phải được tạo trong **tangent space**. * Bent normal map cần sử dụng tọa độ X+, Y+ và Z+; kiểu này được gọi là OpenGL style. Nếu bạn đã import một material được tạo để dùng với engine khác, nó có thể là DirectX style; trong trường hợp đó, bent normal map cần được chuyển đổi để trục Y bị lật. Bạn có thể thực hiện việc này bằng cách đặt channel xanh lá trong phần **Channel Remap** thành **Inverted Green** trong import dock.

.. note::

  Bent normal map khác với normal map thông thường. Hai loại này không thể thay thế cho nhau.

Rim
---

Một số loại vải có lớp lông siêu nhỏ khiến ánh sáng tán xạ xung quanh chúng. Godot mô phỏng điều này bằng tham số *Rim*. Không giống các cách triển khai chiếu sáng viền khác chỉ sử dụng kênh phát sáng, cách này thực sự tính đến ánh sáng (không có ánh sáng thì không có viền). Điều này khiến hiệu ứng trở nên chân thực hơn đáng kể.

.. image:: img/spatial_material17.png

Kích thước viền phụ thuộc vào độ nhám, và có một tham số đặc biệt để chỉ định cách tô màu cho viền. Nếu *Tint* là ``0``, màu của ánh sáng sẽ được sử dụng cho viền. Nếu *Tint* là ``1``, albedo của vật liệu sẽ được sử dụng. Nhìn chung, sử dụng các giá trị trung gian sẽ cho kết quả tốt nhất.

Lớp phủ trong
-------------


Tham số *Clearcoat* được dùng để thêm một lớp phủ trong suốt thứ cấp vào vật liệu. Cách này thường được sử dụng cho sơn xe và đồ chơi. Trên thực tế, đây là một vùng phản chiếu nhỏ được thêm lên trên vật liệu hiện có.

.. image:: img/clearcoat_comparison.png

Anisotropy
----------


Thao tác này thay đổi hình dạng của vùng phản chiếu và căn chỉnh nó theo tangent space. Anisotropy thường được sử dụng với tóc hoặc để làm cho các vật liệu như nhôm xước trở nên chân thực hơn. Hiệu ứng này đặc biệt hiệu quả khi kết hợp với flowmap.

.. image:: img/spatial_material18.png

Ambient Occlusion
-----------------

Bạn có thể chỉ định một ambient occlusion map đã được bake. Map này ảnh hưởng đến lượng ánh sáng môi trường chiếu tới từng bề mặt của vật thể (theo mặc định, nó không ảnh hưởng đến ánh sáng trực tiếp). Mặc dù có thể sử dụng Screen-Space Ambient Occlusion (SSAO) để tạo ambient occlusion, không gì có thể vượt qua chất lượng của một AO map được bake tốt. Bạn nên bake ambient occlusion bất cứ khi nào có thể.

.. image:: img/spatial_material19.png

Độ cao
------

Thiết lập height map cho vật liệu sẽ thực hiện quá trình tìm kiếm bằng ray marching để mô phỏng độ lõm phù hợp của các hốc theo hướng nhìn. Thao tác này chỉ tạo ảo giác về độ sâu và không thêm hình học thực — để biết hình dạng height map dùng cho va chạm vật lý (chẳng hạn như địa hình), hãy xem :ref:`class_HeightMapShape3D`. Cách này có thể không hoạt động với các vật thể phức tạp, nhưng tạo ra hiệu ứng độ sâu chân thực cho texture. Để có kết quả tốt nhất, nên sử dụng *Height* cùng với normal mapping.

.. image:: img/spatial_material20.png

Subsurface Scattering
---------------------

*Tính năng này chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.*

Hiệu ứng này mô phỏng ánh sáng xuyên qua bề mặt của vật thể, bị tán xạ rồi thoát ra ngoài. Nó hữu ích để tạo da, đá cẩm thạch, chất lỏng có màu và nhiều vật liệu khác một cách chân thực.

.. image:: img/spatial_material21.png

Back Lighting
-------------

Tùy chọn này kiểm soát lượng ánh sáng từ phía được chiếu sáng (có thể nhìn thấy đối với ánh sáng) truyền sang phía tối (đối diện với nguồn sáng). Cách này hoạt động tốt với các vật thể mỏng như lá cây, cỏ, tai người, v.v.

.. image:: img/spatial_material22.png

Refraction
----------

Khi refraction được bật, Godot sẽ cố gắng lấy thông tin từ phía sau vật thể đang được render. Điều này cho phép làm biến dạng độ trong suốt theo cách tương tự hiện tượng khúc xạ trong đời thực.

Hãy nhớ sử dụng texture albedo trong suốt (hoặc giảm kênh alpha của màu albedo) để làm cho refraction hiển thị, vì refraction phụ thuộc vào độ trong suốt để tạo ra hiệu ứng có thể nhìn thấy.

Refraction cũng tính đến độ nhám của vật liệu. Các giá trị độ nhám cao hơn sẽ khiến những vật thể phía sau refraction trông mờ hơn, mô phỏng hành vi trong đời thực. Nếu bạn không thể nhìn thấy phía sau vật thể khi refraction được bật và độ trong suốt của albedo đã giảm, hãy giảm giá trị **Roughness** của vật liệu.

Bạn có thể chỉ định một normal map trong thuộc tính **Refraction Texture** để cho phép làm biến dạng hướng khúc xạ theo từng pixel.

.. image:: img/spatial_material23.png

.. note::

    Refraction được triển khai dưới dạng hiệu ứng screen-space và buộc vật liệu phải trong suốt. Điều này khiến hiệu ứng tương đối nhanh, nhưng dẫn đến một số hạn chế:

    - Có thể xảy ra các vấn đề :ref:`Transparency sorting <doc_3d_rendering_limitations_transparency_sorting>`. - Vật liệu khúc xạ không thể khúc xạ lên chính nó hoặc lên các vật liệu trong suốt khác. Vật liệu khúc xạ nằm phía sau một vật liệu trong suốt khác sẽ không hiển thị. - Các vật thể ngoài màn hình không thể xuất hiện trong refraction. Điều này dễ nhận thấy nhất khi giá trị cường độ khúc xạ cao. - Các vật liệu đục nằm phía trước vật liệu khúc xạ sẽ có vẻ như có các cạnh "bị khúc xạ", dù lẽ ra chúng không nên như vậy.

Chi tiết
--------

Godot cho phép sử dụng albedo map và normal map thứ cấp để tạo detail texture, có thể được blend theo nhiều cách. Bằng cách kết hợp tính năng này với các chế độ UV thứ cấp hoặc triplanar, bạn có thể tạo ra nhiều texture thú vị.

.. image:: img/spatial_material24.png

Có một số cài đặt kiểm soát cách sử dụng chi tiết.

Mask: Detail mask là một hình ảnh đen trắng dùng để kiểm soát vị trí blending diễn ra trên texture. Màu trắng dành cho các detail texture, màu đen dành cho các texture của vật liệu thông thường, còn các sắc độ xám khác nhau dùng để blend một phần giữa texture của vật liệu và detail texture.

Blend Mode: Bốn chế độ này kiểm soát cách các texture được blend với nhau.

- Mix: Kết hợp các giá trị pixel của cả hai texture. Ở màu đen, chỉ hiển thị texture của vật liệu; ở màu trắng, chỉ hiển thị detail texture. Các giá trị màu xám tạo ra sự blend mượt mà giữa hai texture.

- Add: Cộng các giá trị pixel của một Texture với texture còn lại. Không giống chế độ mix, cả hai texture được trộn hoàn toàn ở các vùng màu trắng của mask và không được trộn ở các vùng màu xám. Texture gốc hầu như không thay đổi ở các vùng màu đen.

- Sub: Trừ các giá trị pixel của một texture cho texture còn lại. Texture thứ hai bị trừ hoàn toàn ở các vùng màu trắng của mask, chỉ bị trừ một ít ở các vùng màu đen; các vùng màu xám có mức độ trừ khác nhau dựa trên texture cụ thể.

- Mul: Nhân các giá trị số của kênh RGB cho từng pixel của texture trên cùng với các giá trị của pixel tương ứng trong texture bên dưới.

Albedo: Đây là nơi bạn đưa vào texture albedo muốn blend. Nếu ô này không có gì, theo mặc định nó sẽ được diễn giải là màu trắng.

Normal: Đây là nơi bạn đưa vào normal texture muốn blend. Nếu ô này không có gì, theo mặc định nó sẽ được diễn giải là một normal map phẳng. Bạn vẫn có thể sử dụng tùy chọn này ngay cả khi vật liệu chưa bật normal map.

UV1 và UV2
----------

Godot hỗ trợ hai kênh UV cho mỗi vật liệu. UV thứ cấp thường hữu ích cho ambient occlusion hoặc emission (ánh sáng đã bake). UV có thể được scale và offset, rất hữu ích khi sử dụng các texture lặp lại.

.. _doc_standard_material_3d_triplanar_mapping:

Triplanar Mapping
~~~~~~~~~~~~~~~~~

Triplanar mapping được hỗ trợ cho cả UV1 và UV2. Đây là một cách thay thế để lấy tọa độ texture, đôi khi được gọi là "Autotexture". Texture được sample theo các trục X, Y và Z rồi blend dựa trên normal. Triplanar mapping có thể được thực hiện trong world space hoặc object space.

Trong hình bên dưới, bạn có thể thấy tất cả primitive dùng chung một vật liệu với world triplanar, vì vậy texture gạch tiếp nối liền mạch giữa chúng.

.. image:: img/spatial_material25.png

World Triplanar
~~~~~~~~~~~~~~~

Khi sử dụng triplanar mapping, phép tính được thực hiện trong object local space. Tùy chọn này khiến phép tính sử dụng world space thay thế.

.. _doc_standard_material_3d_sampling:

Sampling
--------

Filter
~~~~~~

Phương thức filtering dành cho các texture được vật liệu sử dụng. Xem :ref:`this page<class_BaseMaterial3D_property_texture_filter>` để biết danh sách đầy đủ các tùy chọn và mô tả của chúng.

Repeat
~~~~~~

nếu các texture được vật liệu sử dụng có lặp lại và cách chúng lặp lại. Xem :ref:`this page<class_BaseMaterial3D_property_texture_repeat>` để biết danh sách đầy đủ các tùy chọn và mô tả của chúng.

Shadows
-------

Disable Receive Shadows
~~~~~~~~~~~~~~~~~~~~~~~

Khiến vật thể không nhận bất kỳ loại bóng nào lẽ ra sẽ đổ lên nó.

Shadow to Opacity
~~~~~~~~~~~~~~~~~

Lighting điều chỉnh alpha để các vùng có bóng trở nên đục còn các vùng không có bóng trở nên trong suốt. Hữu ích khi phủ bóng lên hình ảnh camera trong AR.

Billboard
---------

Billboard Mode
~~~~~~~~~~~~~~

Bật billboard mode để vẽ vật liệu. Tùy chọn này kiểm soát cách vật thể hướng về camera:

* **Disabled:** Billboard mode bị tắt. * **Enabled:** Billboard mode được bật. Trục -Z của vật thể sẽ luôn hướng về mặt phẳng nhìn của camera. * **Y-Billboard:** Trục X của vật thể sẽ luôn được căn chỉnh theo mặt phẳng nhìn của camera. * **Particle Billboard:** Phù hợp nhất cho các hệ thống particle vì cho phép chỉ định :ref:`flipbook animation <doc_process_material_properties_animation>`.

.. image:: img/spatial_material9.webp

Phần **Particles Anim** chỉ hiển thị khi billboard mode là **Particle Billboard**.

Billboard Keep Scale
~~~~~~~~~~~~~~~~~~~~

Cho phép scale mesh trong billboard mode.

.. _ref_standard_material_3d_grow:

Grow
----

Mở rộng các đỉnh của vật thể theo hướng mà normal của chúng chỉ tới:

.. image:: img/spatial_material10.png

Tùy chọn này thường được sử dụng để tạo outline với chi phí thấp. Thêm một material pass thứ hai, đặt màu đen và không được shade, đảo ngược culling (Cull Front), rồi thêm một mức grow:

.. image:: img/spatial_material11.png

.. note::

    Để Grow hoạt động như mong đợi, mesh phải có các mặt được kết nối với các đỉnh dùng chung, hay còn gọi là "smooth shading". Nếu mesh có các mặt bị ngắt kết nối với các đỉnh riêng biệt, hay còn gọi là "flat shading", mesh sẽ trông như có các khoảng hở khi sử dụng Grow.

Lưu ý rằng từ Godot 4.5 trở đi, outline dựa trên stencil buffer có sẵn thông qua **Outline** :ref:`stencil mode <doc_standard_material_3d_stencil>`. Tùy chọn này có thể được sử dụng thay cho Grow để tạo outline.

Transform
---------

Fixed Size
~~~~~~~~~~

Khiến vật thể được render ở cùng một kích thước bất kể khoảng cách. Tùy chọn này chủ yếu hữu ích cho các indicator (không kiểm tra độ sâu và có render priority cao) và một số loại billboard.

Use Point Size
~~~~~~~~~~~~~~

Tùy chọn này chỉ có hiệu lực khi hình học được kết xuất tạo thành từ các điểm (thông thường hình học được tạo thành từ các tam giác khi được nhập từ phần mềm dựng hình 3D). Nếu đúng như vậy, các điểm đó có thể được thay đổi kích thước (xem bên dưới).

Point Size
~~~~~~~~~~

Khi vẽ các điểm, hãy chỉ định kích thước điểm theo pixel.

Use Particle Trails
~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng trong các renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Nếu là true, tùy chọn này bật các phần của shader cần thiết để các vệt của GPUParticles3D hoạt động. Tùy chọn này cũng yêu cầu sử dụng mesh có skinning phù hợp, chẳng hạn như RibbonTrailMesh hoặc TubeTrailMesh. Việc bật tính năng này bên ngoài các material được sử dụng trong mesh của GPUParticles3D sẽ khiến material không được kết xuất đúng.

Use Z Clip Scale
~~~~~~~~~~~~~~~~

Thu nhỏ đối tượng đang được kết xuất về phía camera để tránh bị cắt vào các vật thể như tường. Tùy chọn này предназначены để sử dụng cho các đối tượng cố định tương đối với camera, chẳng hạn như cánh tay của người chơi, công cụ, v.v. Ánh sáng và bóng đổ sẽ tiếp tục hoạt động chính xác khi điều chỉnh thiết lập này, nhưng các hiệu ứng trong không gian màn hình như SSAO và SSR có thể bị lỗi với các giá trị scale thấp hơn. Vì vậy, hãy cố gắng giữ thiết lập này càng gần 1.0 càng tốt.

Use FOV Override
~~~~~~~~~~~~~~~~

Ghi đè góc trường nhìn (theo độ) của ``Camera3D``.

.. note::

  Tùy chọn này hoạt động như thể trường nhìn được thiết lập trên một ``Camera3D`` với ``Camera3D.keep_aspect`` được đặt thành ``Camera3D.KEEP_HEIGHT``. Ngoài ra, nó có thể hiển thị không chính xác trên camera không phối cảnh, nơi thiết lập trường nhìn bị bỏ qua.

Proximity and Distance Fade
---------------------------

Godot cho phép material mờ dần khi ở gần nhau, cũng như tùy theo khoảng cách đến người quan sát. Proximity fade hữu ích cho các hiệu ứng như soft particle hoặc một khối nước có sự hòa trộn mượt mà với bờ.

.. image:: img/spatial_material_proxfade.gif

Distance fade hữu ích cho các tia sáng hoặc chỉ báo chỉ xuất hiện sau một khoảng cách nhất định.

Lưu ý rằng việc bật proximity fade hoặc distance fade cùng với chế độ **Pixel Alpha** sẽ bật alpha blending. Alpha blending sử dụng GPU nhiều hơn và có thể gây ra các vấn đề về sắp xếp transparency. Alpha blending cũng vô hiệu hóa nhiều tính năng của material, chẳng hạn như khả năng đổ bóng.

.. note::

    Để ẩn một nhân vật khi họ đến quá gần camera, hãy cân nhắc sử dụng **Pixel Dither**, hoặc tốt hơn là **Object Dither** (thậm chí còn nhanh hơn **Pixel Dither**).

Chế độ **Pixel Alpha**: Độ trong suốt thực tế của một pixel trên đối tượng thay đổi theo khoảng cách đến camera. Đây là chế độ hiệu quả nhất, nhưng buộc material phải sử dụng transparency pipeline (do đó, chẳng hạn, sẽ không có bóng đổ).

.. image:: img/standart_material_distance_fade_pixel_alpha_mode.webp

Chế độ **Pixel Dither**: Cách hoạt động của chế độ này là xấp xỉ độ trong suốt bằng cách chỉ kết xuất một phần các pixel.

.. image:: img/standart_material_distance_fade_pixel_dither_mode.webp

Chế độ **Object Dither**: Tương tự chế độ trước, nhưng độ trong suốt được tính toán giống nhau trên toàn bộ bề mặt của đối tượng.

.. image:: img/standart_material_distance_fade_object_dither_mode.webp

.. _doc_standard_material_3d_stencil:

Stencil
-------

Kể từ Godot 4.5, Godot cho phép material sử dụng stencil buffer. Tính năng này thường được dùng để tạo outline và hiệu ứng X-ray, có thể hữu ích khi làm nổi bật các đối tượng, đặc biệt là những đối tượng nằm phía sau tường.

Các chế độ **Outline** và **X-Ray** gán một stencil material được cấu hình sẵn trong thuộc tính **Next Pass** của material. Có thể sử dụng chế độ **Custom** cho các hiệu ứng nâng cao.

.. image:: img/material_stencil.webp

Các material ghi vào stencil buffer luôn được vẽ trong transparent pass, vì vậy chúng chịu ảnh hưởng của các quy tắc thông thường
:ref:`transparency limitations <doc_3d_rendering_limitations_transparency_sorting>`.

.. note::

    Tương tự như :ref:`Grow property <ref_standard_material_3d_grow>`, để stencil outline hoạt động như mong đợi, mesh phải có các mặt được kết nối với các đỉnh dùng chung, hay còn gọi là "smooth shading". Nếu mesh có các mặt không được kết nối với các đỉnh riêng biệt, hay còn gọi là "flat shading", mesh sẽ xuất hiện các khoảng hở khi sử dụng stencil outline.

    Stencil outline được kết xuất tương tự thuộc tính Grow, nhưng sẽ không trông giống hệt trong mọi trường hợp, đặc biệt khi có giao nhau với các bề mặt opaque.

Material Settings
-----------------

Render priority
---------------

Có thể thay đổi thứ tự kết xuất của các đối tượng, mặc dù điều này chủ yếu hữu ích cho các đối tượng transparent (hoặc các đối tượng opaque thực hiện depth draw nhưng không thực hiện color draw, chẳng hạn như các vết nứt trên sàn).

Các đối tượng được sắp xếp theo hàng đợi opaque/transparent, sau đó theo :ref:`render_priority<class_Material_property_render_priority>`, với các đối tượng có priority cao hơn được vẽ sau. Các đối tượng transparent cũng được sắp xếp theo depth.

Depth testing sẽ ghi đè priority. Chỉ riêng priority không thể buộc các đối tượng opaque được vẽ đè lên nhau.

Next Pass
---------

Thiết lập :ref:`next_pass<class_Material_property_next_pass>` trên một material sẽ khiến một đối tượng được kết xuất lại bằng material tiếp theo đó.

Các material được sắp xếp theo hàng đợi opaque/transparent, sau đó theo :ref:`render_priority<class_Material_property_render_priority>`, với các material có priority cao hơn được vẽ sau.

.. image:: img/next_pass.webp

Depth sẽ được kiểm tra là bằng nhau giữa cả hai material, trừ khi sử dụng thiết lập grow hoặc các biến đổi vertex khác. Các transparent pass liên tiếp nên sử dụng :ref:`render_priority<class_Material_property_render_priority>` để đảm bảo thứ tự chính xác.
