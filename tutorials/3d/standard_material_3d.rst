.. _doc_standard_material_3d:

Standard Material 3D và ORM Material 3D
=======================================

Giới thiệu
----------

``StandardMaterial3D`` và ``ORMMaterial3D`` (Occlusion, Roughness, Metallic) là các vật liệu 3D mặc định nhằm cung cấp hầu hết tính năng mà nghệ sĩ thường tìm kiếm ở một vật liệu mà không cần viết mã shader. Tuy nhiên, chúng có thể được chuyển đổi thành mã shader nếu cần thêm chức năng.

Tutorial này giải thích các tham số có trong cả hai vật liệu.

Có 4 cách để thêm các vật liệu này vào một đối tượng. Có thể thêm vật liệu vào thuộc tính *Material* của mesh. Vật liệu cũng có thể được thêm vào thuộc tính *Material* của node sử dụng mesh (chẳng hạn như node MeshInstance3D), thuộc tính *Material Override* của node sử dụng mesh và *Material Overlay*.

.. image:: img/add_material.webp

Nếu thêm vật liệu vào chính mesh, mỗi lần mesh đó được sử dụng, nó sẽ có vật liệu đó. Nếu thêm vật liệu vào node sử dụng mesh, vật liệu sẽ chỉ được node đó sử dụng; đồng thời, nó cũng ghi đè thuộc tính material của mesh. Nếu thêm vật liệu vào thuộc tính *Material Override* của node, vật liệu đó sẽ chỉ được node đó sử dụng. Nó cũng ghi đè thuộc tính material thông thường của node và thuộc tính material của mesh.

Thuộc tính *Material Overlay* sẽ render một vật liệu **over** vật liệu hiện tại mà mesh đang sử dụng. Ví dụ, có thể dùng thuộc tính này để tạo hiệu ứng lá chắn trong suốt trên mesh.

Cài đặt BaseMaterial 3D
-----------------------

StandardMaterial3D có nhiều cài đặt quyết định giao diện của vật liệu. Tất cả các cài đặt này nằm trong danh mục BaseMaterial3D.

.. image:: img/spatial_material1.webp

Vật liệu ORM gần như hoàn toàn giống nhau, chỉ có một điểm khác biệt. Thay vì có các cài đặt và texture riêng cho occlusion, roughness và metallic, vật liệu ORM sử dụng một texture ORM duy nhất. Các kênh màu khác nhau của texture đó được dùng cho từng tham số. Các chương trình như Substance Painter và Armor Paint cho phép bạn xuất theo định dạng này; với hai chương trình này, bạn có thể dùng preset xuất cho unreal engine, vốn cũng sử dụng texture ORM.

Độ trong suốt
-------------

Theo mặc định, vật liệu trong Godot là opaque. Cách này render nhanh, nhưng có nghĩa là không thể nhìn xuyên qua vật liệu, ngay cả khi bạn sử dụng texture trong suốt trong thuộc tính **Albedo > Texture** (hoặc đặt **Albedo > Color** thành một màu trong suốt).

Để có thể nhìn xuyên qua vật liệu, vật liệu đó cần được đặt thành *transparent*. Godot cung cấp một số chế độ trong suốt:

- **Disabled:** Vật liệu opaque. Đây là chế độ render nhanh nhất và hỗ trợ tất cả tính năng render.

- **Alpha:** Vật liệu trong suốt. Các vùng bán trong suốt được vẽ bằng blending. Chế độ này render chậm, nhưng cho phép tạo độ trong suốt một phần (còn gọi là translucency). Vật liệu sử dụng alpha blending cũng không thể đổ bóng và không hiển thị trong screen-space reflections.

  - **Alpha** phù hợp để tạo hiệu ứng particle và VFX.

- **Alpha Scissor:** Vật liệu trong suốt. Các vùng bán trong suốt có độ mờ thấp hơn **Alpha Scissor Threshold** sẽ không được vẽ (với độ mờ cao hơn ngưỡng này, chúng sẽ được vẽ như opaque). Chế độ này render nhanh hơn Alpha và không gặp vấn đề sắp xếp độ trong suốt. Nhược điểm là nó tạo ra độ trong suốt "có hoặc không", không cho phép các giá trị trung gian. Vật liệu sử dụng alpha scissor có thể đổ bóng.

  - **Alpha Scissor** lý tưởng cho tán lá và hàng rào, vì chúng có các cạnh rõ ràng và cần được sắp xếp chính xác để hiển thị đẹp.

- **Alpha Hash:** Vật liệu trong suốt. Các vùng bán trong suốt được vẽ bằng dithering. Đây cũng là độ trong suốt "có hoặc không", nhưng dithering giúp biểu diễn các vùng opaque một phần với độ chính xác giới hạn tùy thuộc vào độ phân giải viewport. Vật liệu sử dụng alpha hash có thể đổ bóng.

  - **Alpha Hash** phù hợp với tóc có vẻ ngoài chân thực, mặc dù tóc cách điệu có thể hoạt động tốt hơn với alpha scissor.

- **Depth Pre-Pass:** Trước tiên, chế độ này render các pixel hoàn toàn opaque của đối tượng thông qua opaque pipeline, sau đó render phần còn lại bằng alpha blending. Điều này giúp việc sắp xếp độ trong suốt *mostly* chính xác (dù không hoàn toàn, vì các vùng trong suốt một phần vẫn có thể bị sắp xếp không chính xác). Vật liệu sử dụng depth prepass có thể đổ bóng.

.. note::

    Godot sẽ tự động buộc vật liệu trở thành trong suốt với alpha blending nếu *bất kỳ* điều kiện nào sau đây được đáp ứng:

    - Đặt chế độ trong suốt thành **Alpha** (như mô tả ở đây).
    - Đặt blend mode khác với **Mix** mặc định.
    - Bật **Refraction**, **Proximity Fade** hoặc **Distance Fade**.

So sánh độ trong suốt bằng alpha blending (bên trái) và alpha scissor (bên phải):

.. image:: img/spatial_material12.png

.. warning::

    Độ trong suốt bằng alpha blending có một số
    :ref:`hạn chế <doc_3d_rendering_limitations_transparency_sorting>`:

    - Vật liệu alpha-blended render chậm hơn đáng kể, đặc biệt khi chúng chồng lấn lên nhau.
    - Vật liệu alpha-blended có thể gặp vấn đề sắp xếp khi các bề mặt trong suốt chồng lấn lên nhau. Điều này có nghĩa là các bề mặt có thể được render không đúng thứ tự, khiến các bề mặt ở phía sau trông như nằm phía trước những bề mặt thực sự gần camera hơn.
    - Vật liệu alpha-blended không đổ bóng, mặc dù chúng có thể nhận bóng.
    - Vật liệu alpha-blended không xuất hiện trong bất kỳ phản chiếu nào (ngoại trừ reflection probe).
    - Screen-space reflections và các phản chiếu SDFGI sắc nét không xuất hiện trên vật liệu alpha-blended. Khi SDFGI được bật, các phản chiếu thô được dùng làm phương án dự phòng, bất kể roughness của vật liệu.

    Trước khi sử dụng chế độ trong suốt **Alpha**, luôn cân nhắc xem chế độ trong suốt khác có phù hợp hơn với nhu cầu của bạn hay không.

.. _doc_standard_material_3d_alpha_antialiasing:

Khử răng cưa Alpha
~~~~~~~~~~~~~~~~~~

.. note::

    Thuộc tính này chỉ hiển thị khi chế độ trong suốt là **Alpha Scissor** hoặc **Alpha Hash**.

Mặc dù vật liệu alpha scissor và alpha hash render nhanh hơn vật liệu alpha-blended, chúng có các cạnh cứng giữa những vùng opaque và trong suốt. Có thể sử dụng các :ref:`kỹ thuật khử răng cưa <doc_3d_antialiasing>` dựa trên post-processing như FXAA và TAA, nhưng điều này không phải lúc nào cũng được mong muốn vì các kỹ thuật này có xu hướng khiến kết quả cuối cùng trông mờ hơn hoặc xuất hiện hiện tượng bóng ma.

Có 3 chế độ khử răng cưa alpha:

- **Disabled:** Không khử răng cưa alpha. Các cạnh của vật liệu trong suốt sẽ bị răng cưa trừ khi sử dụng giải pháp khử răng cưa dựa trên post-processing.
- **Alpha Edge Blend:** Tạo ra sự chuyển tiếp mượt mà giữa các vùng đục và trong suốt. Còn được gọi là "alpha to coverage".
- **Alpha Edge Clip:** Tạo ra sự chuyển tiếp sắc nét nhưng vẫn được khử răng cưa giữa các vùng đục và trong suốt. Còn được gọi là "alpha to coverage + alpha to one".

Khi chế độ khử răng cưa alpha được đặt thành **Alpha Edge Blend** hoặc **Alpha Edge Clip**, một thuộc tính **Alpha Antialiasing Edge** mới sẽ hiển thị bên dưới trong inspector. Thuộc tính này kiểm soát ngưỡng bên dưới mà các pixel sẽ được làm trong suốt. Mặc dù bạn đã xác định một ngưỡng alpha scissor (chỉ khi sử dụng **Alpha Scissor**), ngưỡng bổ sung này được dùng để chuyển tiếp mượt mà giữa các pixel đục và trong suốt. **Alpha Antialiasing Edge** *luôn* phải được đặt thành giá trị thấp hơn nghiêm ngặt so với ngưỡng alpha scissor. Giá trị mặc định ``0.3`` là một giá trị hợp lý khi alpha scissor có ngưỡng ``0.5``, nhưng hãy nhớ điều chỉnh cạnh khử răng cưa alpha này khi thay đổi ngưỡng alpha scissor.

Nếu hiệu ứng khử răng cưa chưa đủ rõ, hãy thử tăng **Alpha Antialiasing Edge** nhưng vẫn đảm bảo giá trị này thấp hơn **Alpha Scissor Threshold** (nếu material sử dụng alpha scissor). Ngược lại, nếu bạn nhận thấy hình thức của texture thay đổi rõ rệt khi camera tiến gần material, hãy thử giảm **Alpha Antialiasing Edge**.

.. important::

    Để đạt kết quả tốt nhất, MSAA 3D nên được đặt thành ít nhất 2× trong Project Settings khi sử dụng khử răng cưa alpha. Điều này là do tính năng này dựa vào alpha to coverage, một tính năng do MSAA cung cấp.

    Nếu không có MSAA, một mẫu dithering cố định sẽ được áp dụng lên các cạnh của material, nhưng cách này không thực sự hiệu quả trong việc làm mượt các cạnh (mặc dù vẫn có thể giúp ích đôi chút).

Chế độ hòa trộn
~~~~~~~~~~~~~~~

Kiểm soát chế độ hòa trộn của material. Lưu ý rằng mọi chế độ khác *Mix* đều buộc object đi qua transparent pipeline.

* **Mix:** Chế độ hòa trộn mặc định, alpha kiểm soát mức độ hiển thị của object.
* **Add:** Màu cuối cùng của object được cộng vào màu của màn hình, phù hợp với flare hoặc một số hiệu ứng giống lửa.
* **Subtract:** Màu cuối cùng của object bị trừ khỏi màu của màn hình.
* **Multiply:** Màu cuối cùng của object được nhân với màu của màn hình.
* **Premultiplied Alpha:** Màu của object được giả định là đã được nhân với alpha. Chế độ này hoạt động như **Add** khi alpha là ``0.0`` (hoàn toàn trong suốt), và như **Mix** khi alpha là ``1.0`` (đục).

.. image:: img/spatial_material8.png

Chế độ loại bỏ mặt
~~~~~~~~~~~~~~~~~~

Xác định mặt nào của object không được vẽ khi các mặt sau được kết xuất:

* **Back:** Mặt sau của object bị loại bỏ khi không hiển thị (mặc định).
* **Front:** Mặt trước của object bị loại bỏ khi không hiển thị.
* **Disabled:** Dùng cho các object có hai mặt (không thực hiện loại bỏ mặt).

.. note::

  Theo mặc định, Blender tắt tính năng loại bỏ mặt sau trên material và sẽ xuất material để khớp với cách chúng được kết xuất trong Blender. Điều này có nghĩa là material trong Godot sẽ có chế độ loại bỏ mặt được đặt thành **Disabled**. Điều này có thể làm giảm hiệu suất vì các mặt sau vẫn được kết xuất, ngay cả khi chúng bị các mặt khác loại bỏ. Để khắc phục, hãy bật **Backface Culling** trong thẻ Materials của Blender, sau đó xuất lại scene sang glTF.

Chế độ vẽ độ sâu
~~~~~~~~~~~~~~~~

Xác định thời điểm phải thực hiện kết xuất độ sâu.

* **Opaque Only (default):** Độ sâu chỉ được vẽ cho các object đục.
* **Always:** Độ sâu được vẽ cho cả object đục và trong suốt.
* **Never:** Không thực hiện vẽ độ sâu (đừng nhầm tùy chọn này với tùy chọn No Depth Test bên dưới).
* **Depth Pre-Pass:** Đối với các object trong suốt, trước tiên một lượt vẽ đục được thực hiện với các phần đục, sau đó phần trong suốt được vẽ lên trên. Hãy dùng tùy chọn này với cỏ hoặc tán lá cây trong suốt.

.. image:: img/material_depth_draw.png

Không kiểm tra độ sâu
~~~~~~~~~~~~~~~~~~~~~

Để các object ở gần hiển thị phía trên các object ở xa, việc kiểm tra độ sâu được thực hiện. Tắt tính năng này khiến các object hiển thị phía trên (hoặc bên dưới) mọi thứ khác.

Tắt tính năng này phù hợp nhất khi vẽ các chỉ báo trong world space, và hoạt động rất tốt với thuộc tính *Render Priority* của Material (xem phần cuối trang này).

.. image:: img/spatial_material3.png

Kiểm tra độ sâu
~~~~~~~~~~~~~~~

Có thể dùng tùy chọn này để đảo ngược kiểm tra độ sâu tiêu chuẩn. Khi được đặt thành **Inverted**, object sẽ chỉ hiển thị khi bị che khuất và sẽ bị ẩn trong các trường hợp khác.

Tùy chọn này không có tác dụng nếu **No Depth Test** được bật.

.. image:: img/material_depth_test.webp

Đổ bóng
-------

Chế độ đổ bóng
~~~~~~~~~~~~~~

Material hỗ trợ ba chế độ đổ bóng: **Per-Pixel**, **Per-Vertex** và **Unshaded**.

.. figure:: img/standard_material_shading_modes.webp
  :align: center
  :alt: Ba hình cầu minh họa các chế độ Per-Pixel, Per-Vertex và Unshaded.

Chế độ đổ bóng **Per-Pixel** tính toán ánh sáng cho từng pixel và phù hợp với hầu hết trường hợp sử dụng. Tuy nhiên, trong một số trường hợp, bạn có thể muốn tăng hiệu suất bằng cách sử dụng chế độ đổ bóng khác.

Chế độ đổ bóng **Per-Vertex**, thường được gọi là "vertex shading" hoặc "vertex lighting", thay vào đó tính toán ánh sáng một lần cho mỗi vertex và nội suy kết quả giữa các pixel.

Trên các thiết bị cấp thấp hoặc thiết bị di động, sử dụng ánh sáng per-vertex có thể tăng đáng kể hiệu suất kết xuất. Khi kết xuất nhiều lớp trong suốt, chẳng hạn như khi sử dụng particle system, sử dụng đổ bóng per-vertex có thể cải thiện hiệu suất, đặc biệt khi camera ở gần các particle.

Bạn cũng có thể sử dụng ánh sáng per-vertex để tạo ra vẻ ngoài retro.

.. figure:: img/standard_material_shading_modes_textured.webp
  :align: center
  :alt: Hai khối lập phương có texture gạch, một khối được đổ bóng và một khối không được đổ bóng.

  Texture từ `AmbientCG <https://ambientcg.com/view?id=Bricks051>`__

Chế độ đổ bóng **Unshaded** hoàn toàn không tính toán ánh sáng. Thay vào đó, màu **Albedo** được xuất trực tiếp. Ánh sáng hoàn toàn không ảnh hưởng đến material, và các material không đổ bóng thường có vẻ sáng hơn đáng kể so với các material được đổ bóng.

Kết xuất không đổ bóng hữu ích cho một số hiệu ứng hình ảnh cụ thể. Nếu cần hiệu suất tối đa, bạn cũng có thể sử dụng cách này cho các hạt hoặc trên thiết bị cấp thấp hay thiết bị di động.

Diffuse Mode
~~~~~~~~~~~~

Chỉ định thuật toán được sử dụng để tán xạ khuếch tán của ánh sáng khi chiếu vào đối tượng. Mặc định là **Burley**. Các chế độ khác cũng có sẵn:

* **Burley:** Chế độ mặc định, thuật toán khuếch tán PBS Disney Principled nguyên bản.
* **Lambert:** Không bị ảnh hưởng bởi độ nhám.
* **Lambert Wrap:** Mở rộng Lambert để bao phủ hơn 90 độ khi độ nhám tăng. Hoạt động rất tốt cho tóc và mô phỏng tán xạ dưới bề mặt giá rẻ. Cách triển khai này bảo toàn năng lượng.
* **Toon:** Tạo ngưỡng cắt cứng cho ánh sáng, với độ làm mượt bị ảnh hưởng bởi độ nhám. Bạn nên tắt đóng góp của bầu trời trong cài đặt ánh sáng môi trường của environment hoặc tắt ánh sáng môi trường trong StandardMaterial3D để đạt hiệu ứng tốt hơn.

.. image:: img/spatial_material6.webp

Specular Mode
~~~~~~~~~~~~~

Chỉ định cách vùng sáng phản chiếu sẽ được kết xuất. Vùng sáng phản chiếu biểu thị hình dạng của nguồn sáng được phản chiếu trên đối tượng.

* **SchlickGGX:** Vùng sáng phổ biến nhất được các engine 3D PBR sử dụng hiện nay.
* **Toon:** Tạo vùng sáng kiểu toon, thay đổi kích thước tùy theo độ nhám.
* **Disabled:** Đôi khi vùng sáng gây vướng. Biến đi!

.. image:: img/spatial_material7.webp

Disable Ambient Light
~~~~~~~~~~~~~~~~~~~~~

Khiến đối tượng không nhận bất kỳ loại ánh sáng môi trường nào vốn sẽ chiếu sáng đối tượng.

Disable Fog
~~~~~~~~~~~

Khiến đối tượng không bị ảnh hưởng bởi sương mù dựa trên độ sâu hoặc sương mù thể tích. Điều này hữu ích cho các hạt hoặc vật liệu được pha trộn cộng, vì nếu không chúng sẽ hiển thị hình dạng của mesh (ngay cả ở những nơi vốn sẽ không nhìn thấy nếu không có sương mù).

Disable Specular Occlusion
~~~~~~~~~~~~~~~~~~~~~~~~~~

Khiến các phản chiếu của đối tượng không bị giảm ở những nơi thường bị che khuất.

Vertex Color
------------

Cài đặt này cho phép chọn thao tác mặc định đối với màu đỉnh đến từ ứng dụng tạo mô hình 3D của bạn. Theo mặc định, chúng bị bỏ qua.

Use as Albedo
~~~~~~~~~~~~~

Chọn tùy chọn này có nghĩa là màu đỉnh được sử dụng làm màu albedo.

Is sRGB
~~~~~~~

Hầu hết phần mềm tạo mô hình 3D có thể sẽ xuất màu đỉnh dưới dạng sRGB, vì vậy bật tùy chọn này sẽ giúp chúng hiển thị chính xác.

Albedo
------

*Albedo* là màu cơ sở của vật liệu, trên đó tất cả cài đặt khác hoạt động. Khi được đặt thành *Unshaded*, đây là màu duy nhất hiển thị. Trong các phiên bản Godot trước đây, kênh này có tên là *Diffuse*. Việc đổi tên chủ yếu xảy ra vì trong PBR (Physically Based Rendering), màu này ảnh hưởng đến nhiều phép tính hơn chỉ riêng đường dẫn ánh sáng khuếch tán.

Có thể sử dụng đồng thời màu và texture albedo vì chúng được nhân với nhau.

*Alpha channel* trong màu và texture albedo cũng được sử dụng cho độ trong suốt của đối tượng. Nếu bạn sử dụng màu hoặc texture có *alpha channel*, hãy đảm bảo bật transparency hoặc *alpha scissoring* để tính năng hoạt động.

Metallic
--------

Godot sử dụng mô hình metallic thay vì các mô hình cạnh tranh nhờ tính đơn giản của nó. Tham số này xác định mức độ phản chiếu của vật liệu. Càng phản chiếu nhiều thì ánh sáng khuếch tán/môi trường càng ít ảnh hưởng đến vật liệu và càng nhiều ánh sáng được phản chiếu. Mô hình này được gọi là "energy-conserving".

Tham số *Specular* biểu thị mức độ phản xạ nói chung (khác với *Metallic*, tham số này không bảo toàn năng lượng, vì vậy hãy để ở ``0.5`` và đừng chạm vào trừ khi bạn cần).

Độ phản xạ nội tại tối thiểu là ``0.04``, vì vậy không thể tạo vật liệu hoàn toàn không phản chiếu, giống như trong đời thực.

.. image:: img/spatial_material13.png

Roughness
---------

*Roughness* ảnh hưởng đến cách phản chiếu diễn ra. Giá trị ``0`` tạo ra một chiếc gương hoàn hảo, trong khi giá trị ``1`` làm mờ hoàn toàn phản chiếu (mô phỏng bề mặt vi mô tự nhiên). Có thể tạo ra hầu hết các loại vật liệu phổ biến bằng sự kết hợp phù hợp giữa *Metallic* và *Roughness*.

.. image:: img/spatial_material14.png

Emission
--------

*Emission* chỉ định lượng ánh sáng được vật liệu phát ra (lưu ý rằng giá trị này không bao gồm ánh sáng chiếu lên hình học xung quanh, trừ khi sử dụng :ref:`VoxelGI <doc_using_voxel_gi>` hoặc :ref:`SDFGI <doc_using_sdfgi>`). Giá trị này được cộng vào hình ảnh cuối cùng và không bị ảnh hưởng bởi các nguồn sáng khác trong cảnh.

.. image:: img/spatial_material15.png

Normal map
----------

Normal mapping cho phép bạn đặt một texture biểu thị các chi tiết hình dạng tinh hơn. Tính năng này không thay đổi hình học, chỉ thay đổi góc tới của ánh sáng. Trong Godot, chỉ các kênh đỏ và xanh lục của normal map được sử dụng để cải thiện khả năng nén và tăng tính tương thích.

.. image:: img/spatial_material16.png

.. note::

  Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+; kiểu này được gọi là kiểu OpenGL. Nếu bạn đã nhập một vật liệu được tạo để sử dụng với engine khác, vật liệu đó có thể ở kiểu DirectX; trong trường hợp này, normal map cần được chuyển đổi để đảo trục Y.

  Bạn có thể tìm thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `tại đây <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

.. _doc_standard_material_3d_bent_normal_map:

Bent normal map
---------------

Bent normal map mô tả hướng trung bình của ánh sáng môi trường. Không giống normal map thông thường, loại bản đồ này được sử dụng để cải thiện cách vật liệu phản ứng với ánh sáng thay vì thêm chi tiết bề mặt.

Điều này đạt được theo hai cách:

* Ánh sáng khuếch tán gián tiếp được điều chỉnh để phù hợp hơn với global illumination.
* Nếu bật specular occlusion, tính năng này sẽ được tính bằng bent normal và ambient occlusion thay vì chỉ dựa trên ánh sáng môi trường. Điều này bao gồm screen-space ambient occlusion (SSAO) và các nguồn ambient occlusion khác.

.. image:: img/spatial_material_bentnormals.webp

Godot chỉ sử dụng các kênh đỏ và xanh lục của bent normal map để cải thiện khả năng nén và tăng tính tương thích.

Khi tạo bent normal map, cần có ba điều để nó hoạt động chính xác trong Godot:

* Khi baking, phải sử dụng **cosine distribution** của các tia.
* Texture phải được tạo trong **tangent space**.
* Bản đồ pháp tuyến cong cần sử dụng các tọa độ X+, Y+ và Z+; kiểu này được gọi là kiểu OpenGL. Nếu bạn đã nhập một material được tạo để sử dụng với engine khác, material đó có thể dùng kiểu DirectX; khi đó cần chuyển đổi bản đồ pháp tuyến cong để lật trục Y. Bạn có thể thực hiện việc này bằng cách đặt kênh green trong phần **Channel Remap** thành **Inverted Green** trong import dock.

.. note::

  Bản đồ pháp tuyến cong khác với bản đồ pháp tuyến thông thường. Hai loại này không thể thay thế cho nhau.

Viền
----

Một số loại vải có lớp lông siêu nhỏ khiến ánh sáng tán xạ xung quanh chúng. Godot mô phỏng hiệu ứng này bằng tham số *Rim*. Không giống các cách triển khai chiếu sáng viền khác, vốn chỉ sử dụng kênh emission, cách này thực sự tính đến ánh sáng (không có ánh sáng thì không có viền). Điều này khiến hiệu ứng trở nên chân thực hơn đáng kể.

.. image:: img/spatial_material17.png

Kích thước viền phụ thuộc vào độ roughness, và có một tham số đặc biệt để chỉ định cách tô màu cho viền. Nếu *Tint* là ``0``, màu của ánh sáng sẽ được dùng cho viền. Nếu *Tint* là ``1``, albedo của material sẽ được dùng. Nhìn chung, các giá trị trung gian cho kết quả tốt nhất.

Lớp phủ trong
-------------


Tham số *Clearcoat* được dùng để thêm một lớp phủ trong thứ cấp vào material. Hiệu ứng này thường được dùng cho sơn xe và đồ chơi. Trên thực tế, đó là một vùng phản chiếu nhỏ hơn được thêm lên trên material hiện có.

.. image:: img/clearcoat_comparison.png

Tính dị hướng
-------------


Tính năng này thay đổi hình dạng của vùng phản chiếu và căn chỉnh nó theo tangent space. Tính dị hướng thường được dùng cho tóc hoặc để làm cho các material như nhôm chải xước trở nên chân thực hơn. Tính năng này đặc biệt hiệu quả khi kết hợp với flowmap.

.. image:: img/spatial_material18.png

Che khuất môi trường
--------------------

Bạn có thể chỉ định một bản đồ che khuất môi trường đã được bake. Bản đồ này ảnh hưởng đến lượng ánh sáng môi trường chiếu tới từng bề mặt của vật thể (theo mặc định, nó không ảnh hưởng đến ánh sáng trực tiếp). Mặc dù có thể sử dụng Screen-Space Ambient Occlusion (SSAO) để tạo hiệu ứng che khuất môi trường, không gì có thể vượt qua chất lượng của một bản đồ AO được bake tốt. Bạn nên bake hiệu ứng che khuất môi trường bất cứ khi nào có thể.

.. image:: img/spatial_material19.png

Độ cao
------

Việc đặt bản đồ độ cao trên một material sẽ tạo ra quá trình tìm kiếm bằng ray marching để mô phỏng độ dịch chuyển chính xác của các hốc theo hướng nhìn. Điều này chỉ tạo ra ảo giác về độ sâu, không thêm hình học thực — để biết về hình dạng bản đồ độ cao dùng cho va chạm vật lý (chẳng hạn như địa hình), hãy xem :ref:`class_HeightMapShape3D`. Có thể tính năng này không hoạt động với các vật thể phức tạp, nhưng nó tạo ra hiệu ứng độ sâu chân thực cho texture. Để đạt kết quả tốt nhất, nên sử dụng *Height* cùng với normal mapping.

.. image:: img/spatial_material20.png

Tán xạ dưới bề mặt
------------------

*Tính năng này chỉ có trong renderer Forward+, không có trong renderer Mobile hoặc Compatibility.*

Hiệu ứng này mô phỏng ánh sáng xuyên qua bề mặt của vật thể, bị tán xạ rồi đi ra ngoài. Tính năng này hữu ích để tạo da, đá cẩm thạch, chất lỏng có màu và các vật liệu khác một cách chân thực.

.. image:: img/spatial_material21.png

Chiếu sáng phía sau
-------------------

Tính năng này điều khiển lượng ánh sáng từ phía được chiếu sáng (nhìn thấy đối với nguồn sáng) truyền sang phía tối (đối diện với nguồn sáng). Hiệu ứng này phù hợp với các vật thể mỏng như lá cây, cỏ, tai người, v.v.

.. image:: img/spatial_material22.png

Khúc xạ
-------

Khi bật khúc xạ, Godot cố gắng lấy thông tin từ phía sau vật thể đang được render. Điều này cho phép làm biến dạng độ trong suốt theo cách tương tự hiện tượng khúc xạ trong thực tế.

Hãy nhớ sử dụng texture albedo trong suốt (hoặc giảm kênh alpha của màu albedo) để nhìn thấy hiệu ứng khúc xạ, vì khúc xạ dựa vào độ trong suốt để tạo ra hiệu ứng có thể nhìn thấy.

Khúc xạ cũng tính đến độ roughness của material. Giá trị roughness cao hơn sẽ khiến các vật thể phía sau hiệu ứng khúc xạ trông mờ hơn, mô phỏng hành vi trong thực tế. Nếu bạn không thể nhìn thấy phía sau vật thể khi đã bật khúc xạ và giảm độ trong suốt của albedo, hãy giảm giá trị **Roughness** của material.

Bạn có thể tùy chọn chỉ định một bản đồ pháp tuyến trong thuộc tính **Refraction Texture** để cho phép làm biến dạng hướng khúc xạ theo từng pixel.

.. image:: img/spatial_material23.png

.. note::

    Khúc xạ được triển khai dưới dạng hiệu ứng screen-space và buộc material phải trong suốt. Điều này khiến hiệu ứng tương đối nhanh, nhưng cũng dẫn đến một số hạn chế:

    - Có thể xảy ra các vấn đề về :ref:`Transparency sorting <doc_3d_rendering_limitations_transparency_sorting>`.
    - Material khúc xạ không thể khúc xạ lên chính nó hoặc lên các material trong suốt khác. Một material khúc xạ nằm phía sau material trong suốt khác sẽ bị vô hình.
    - Các vật thể nằm ngoài màn hình không thể xuất hiện trong hiệu ứng khúc xạ. Điều này dễ nhận thấy nhất khi giá trị cường độ khúc xạ cao.
    - Các material opaque nằm phía trước material khúc xạ sẽ có vẻ như có các cạnh đã "khúc xạ", dù lẽ ra chúng không nên như vậy.

Chi tiết
--------

Godot cho phép sử dụng albedo và normal map thứ cấp để tạo texture chi tiết, có thể được blend theo nhiều cách. Bằng cách kết hợp với các chế độ UV thứ cấp hoặc triplanar, bạn có thể tạo ra nhiều texture thú vị.

.. image:: img/spatial_material24.png

Có một số thiết lập điều khiển cách sử dụng chi tiết.

Mask: Mặt nạ chi tiết là một hình ảnh đen trắng dùng để điều khiển vị trí blend trên texture. Màu trắng dành cho các texture chi tiết, màu đen dành cho các texture material thông thường, còn các sắc độ xám khác nhau dùng để blend một phần giữa texture material và texture chi tiết.

Blend Mode: Bốn chế độ này điều khiển cách các texture được blend với nhau.

- Mix: Kết hợp các giá trị pixel của cả hai texture. Ở màu đen, chỉ hiển thị texture material; ở màu trắng, chỉ hiển thị texture chi tiết. Các giá trị màu xám tạo ra sự blend mượt mà giữa hai texture.

- Add: Cộng các giá trị pixel của một Texture với texture còn lại. Không giống chế độ mix, cả hai texture được trộn hoàn toàn ở các vùng màu trắng của mask và không được trộn ở các vùng màu xám. Texture gốc hầu như không thay đổi ở các vùng màu đen.

- Sub: Trừ các giá trị pixel của một texture cho texture còn lại. Texture thứ hai bị trừ hoàn toàn ở các vùng màu trắng của mask, chỉ bị trừ một ít ở các vùng màu đen; các vùng màu xám có mức độ trừ khác nhau dựa trên texture cụ thể.

- Mul: Nhân các giá trị kênh RGB của từng pixel trong texture trên với các giá trị của pixel tương ứng trong texture dưới.

Albedo: Đây là nơi bạn đặt texture albedo muốn blend. Nếu không có gì trong ô này, texture sẽ được mặc định diễn giải là màu trắng.

Normal: Đây là nơi bạn đặt normal texture muốn blend. Nếu không có gì trong ô này, texture sẽ được mặc định diễn giải là một bản đồ pháp tuyến phẳng. Bạn vẫn có thể sử dụng tính năng này ngay cả khi material chưa bật normal map.

UV1 và UV2
----------

Godot hỗ trợ hai kênh UV cho mỗi material. UV thứ cấp thường hữu ích cho che khuất môi trường hoặc emission (ánh sáng đã bake). Bạn có thể scale và offset UV, rất hữu ích khi sử dụng các texture lặp lại.

.. _doc_standard_material_3d_triplanar_mapping:

Mapping triplanar
~~~~~~~~~~~~~~~~~

Triplanar mapping được hỗ trợ cho cả UV1 và UV2. Đây là một cách thay thế để lấy tọa độ texture, đôi khi được gọi là "Autotexture". Texture được lấy mẫu theo các trục X, Y và Z rồi hòa trộn theo normal. Triplanar mapping có thể được thực hiện trong world space hoặc object space.

Trong hình ảnh bên dưới, bạn có thể thấy tất cả primitive đều dùng chung một material với world triplanar, nên texture gạch tiếp nối mượt mà giữa chúng.

.. image:: img/spatial_material25.png

World Triplanar
~~~~~~~~~~~~~~~

Khi sử dụng triplanar mapping, phép tính được thực hiện trong object local space. Tùy chọn này khiến phép tính sử dụng world space thay thế.

.. _doc_standard_material_3d_sampling:

Sampling
--------

Filter
~~~~~~

Phương pháp filtering cho các texture được material sử dụng. Xem :ref:`trang này <class_BaseMaterial3D_property_texture_filter>` để biết danh sách đầy đủ các tùy chọn và mô tả của chúng.

Repeat
~~~~~~

liệu các texture được material sử dụng có lặp lại hay không và cách chúng lặp lại. Xem :ref:`trang này <class_BaseMaterial3D_property_texture_repeat>` để biết danh sách đầy đủ các tùy chọn và mô tả của chúng.

Shadows
-------

Disable Receive Shadows
~~~~~~~~~~~~~~~~~~~~~~~

Khiến object không nhận bất kỳ loại shadow nào vốn sẽ được đổ lên object đó.

Shadow to Opacity
~~~~~~~~~~~~~~~~~

Lighting điều chỉnh alpha để các vùng có shadow trở nên opaque và các vùng không có shadow trở nên transparent. Hữu ích khi phủ shadow lên hình ảnh camera trong AR.

Billboard
---------

Billboard Mode
~~~~~~~~~~~~~~

Bật billboard mode cho các material dùng để vẽ. Tùy chọn này kiểm soát cách object hướng về camera:

* **Disabled:** Billboard mode bị tắt.
* **Enabled:** Billboard mode được bật. Trục -Z của object sẽ luôn hướng về mặt phẳng nhìn của camera.
* **Y-Billboard:** Trục X của object sẽ luôn được căn chỉnh với mặt phẳng nhìn của camera.
* **Particle Billboard:** Phù hợp nhất cho particle system vì cho phép chỉ định :ref:`flipbook animation <doc_process_material_properties_animation>`.

.. image:: img/spatial_material9.webp

Phần **Particles Anim** chỉ hiển thị khi billboard mode là **Particle Billboard**.

Billboard Keep Scale
~~~~~~~~~~~~~~~~~~~~

Cho phép scale một mesh trong billboard mode.

.. _ref_standard_material_3d_grow:

Grow
----

Mở rộng các vertex của object theo hướng mà normal của chúng chỉ tới:

.. image:: img/spatial_material10.png

Cách này thường được dùng để tạo outline với chi phí thấp. Thêm một material pass thứ hai, đặt material đó thành màu đen và unshaded, đảo ngược culling (Cull Front), rồi thêm grow:

.. image:: img/spatial_material11.png

.. note::

    Để Grow hoạt động như mong đợi, mesh phải có các mặt được nối với nhau và dùng chung vertex, hay còn gọi là "smooth shading". Nếu mesh có các mặt không nối với nhau và các vertex riêng biệt, hay "flat shading", mesh sẽ xuất hiện các khoảng hở khi sử dụng Grow.

Lưu ý rằng từ Godot 4.5 trở đi, outline dựa trên stencil buffer có thể được tạo bằng **Outline** :ref:`stencil mode <doc_standard_material_3d_stencil>`. Có thể dùng cách này thay cho Grow để tạo outline.

Transform
---------

Fixed Size
~~~~~~~~~~

Tùy chọn này khiến object được render với cùng một kích thước bất kể khoảng cách. Tùy chọn này chủ yếu hữu ích cho các indicator (không depth test và có render priority cao) cùng một số loại billboard.

Use Point Size
~~~~~~~~~~~~~~

Tùy chọn này chỉ có hiệu lực khi geometry được render tạo thành từ các point (thông thường geometry được tạo từ triangle khi import từ phần mềm dựng hình 3D). Khi đó, các point này có thể được thay đổi kích thước (xem bên dưới).

Point Size
~~~~~~~~~~

Khi vẽ các point, chỉ định kích thước point theo pixel.

Use Particle Trails
~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng trong renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Nếu là true, bật các phần shader cần thiết để trail của GPUParticles3D hoạt động. Tùy chọn này cũng yêu cầu sử dụng mesh có skinning phù hợp, chẳng hạn như RibbonTrailMesh hoặc TubeTrailMesh. Việc bật tính năng này ngoài các material được dùng trong mesh GPUParticles3D sẽ khiến material không được render đúng.

Use Z Clip Scale
~~~~~~~~~~~~~~~~

Scale object đang được render về phía camera để tránh bị clipping vào những thứ như tường. Tùy chọn này dành cho các object cố định tương đối với camera, chẳng hạn như cánh tay của người chơi, công cụ, v.v. Lighting và shadow vẫn tiếp tục hoạt động chính xác khi điều chỉnh thiết lập này, nhưng các hiệu ứng trong screen space như SSAO và SSR có thể bị lỗi khi scale thấp hơn. Vì vậy, hãy cố gắng giữ thiết lập này gần 1.0 nhất có thể.

Use FOV Override
~~~~~~~~~~~~~~~~

Ghi đè góc field of view (theo độ) của ``Camera3D``.

.. note::

  Tùy chọn này hoạt động như thể field of view được thiết lập trên một ``Camera3D`` với ``Camera3D.keep_aspect`` được đặt thành ``Camera3D.KEEP_HEIGHT``. Ngoài ra, kết quả có thể không hiển thị chính xác trên camera không phối cảnh, nơi thiết lập field of view bị bỏ qua.

Proximity and Distance Fade
---------------------------

Godot cho phép material fade theo khoảng cách gần giữa các object cũng như theo khoảng cách đến người xem. Proximity fade hữu ích cho các hiệu ứng như soft particle hoặc một khối nước có sự hòa trộn mượt mà với bờ.

.. image:: img/spatial_material_proxfade.gif

Distance fade hữu ích cho các light shaft hoặc indicator chỉ xuất hiện sau một khoảng cách nhất định.

Hãy lưu ý rằng việc bật proximity fade hoặc distance fade với chế độ **Pixel Alpha** sẽ bật alpha blending. Alpha blending sử dụng nhiều GPU hơn và có thể gây ra vấn đề khi sắp xếp transparency. Alpha blending cũng vô hiệu hóa nhiều tính năng của material, chẳng hạn như khả năng đổ shadow.

.. note::

    Để ẩn một nhân vật khi nhân vật đó đến quá gần camera, hãy cân nhắc sử dụng **Pixel Dither** hoặc tốt hơn là **Object Dither** (thậm chí còn nhanh hơn **Pixel Dither**).

Chế độ **Pixel Alpha**: Độ trong suốt thực tế của một pixel trên object thay đổi theo khoảng cách đến camera. Đây là hiệu ứng hiệu quả nhất, nhưng buộc material phải chuyển sang transparency pipeline (dẫn đến việc không có shadow, chẳng hạn).

.. image:: img/standart_material_distance_fade_pixel_alpha_mode.webp

Chế độ **Pixel Dither**: Cách này gần đúng với transparency bằng cách chỉ render một phần các pixel.

.. image:: img/standart_material_distance_fade_pixel_dither_mode.webp

Chế độ **Object Dither**: Tương tự chế độ trước, nhưng độ trong suốt được tính toán giống nhau trên toàn bộ bề mặt của object.

.. image:: img/standart_material_distance_fade_object_dither_mode.webp

.. _doc_standard_material_3d_stencil:

Stencil
-------

Kể từ Godot 4.5, Godot cho phép material sử dụng stencil buffer. Tính năng này thường được dùng để tạo hiệu ứng viền và X-Ray, hữu ích khi muốn làm nổi bật các đối tượng, đặc biệt là những đối tượng ở phía sau tường.

Các chế độ **Outline** và **X-Ray** gán một stencil material được cấu hình sẵn vào thuộc tính **Next Pass** của material. Có thể sử dụng chế độ **Custom** cho các hiệu ứng nâng cao.

.. image:: img/material_stencil.webp

Các material ghi vào stencil buffer luôn được vẽ trong transparent pass, vì vậy chúng chịu ảnh hưởng của các
:ref:`hạn chế về độ trong suốt <doc_3d_rendering_limitations_transparency_sorting>` thông thường.

.. note::

    Tương tự :ref:`thuộc tính Grow <ref_standard_material_3d_grow>`, để stencil outline hoạt động như mong đợi, mesh phải có các mặt được kết nối với các đỉnh dùng chung, hay còn gọi là "smooth shading". Nếu mesh có các mặt không kết nối với các đỉnh riêng biệt, hay còn gọi là "flat shading", mesh sẽ xuất hiện các khoảng hở khi sử dụng stencil outline.

    Stencil outline được kết xuất tương tự thuộc tính Grow, nhưng sẽ không trông giống hệt trong mọi tình huống, đặc biệt khi có giao nhau với các bề mặt opaque.

Cài đặt vật liệu
----------------

Độ ưu tiên kết xuất
-------------------

Có thể thay đổi thứ tự kết xuất của các đối tượng, mặc dù điều này chủ yếu hữu ích cho các đối tượng transparent (hoặc các đối tượng opaque thực hiện depth draw nhưng không thực hiện color draw, chẳng hạn như các vết nứt trên sàn).

Các đối tượng được sắp xếp theo hàng đợi opaque/transparent, sau đó theo :ref:`render_priority<class_Material_property_render_priority>`, với các đối tượng có độ ưu tiên cao hơn được vẽ sau. Các đối tượng transparent cũng được sắp xếp theo độ sâu.

Depth testing sẽ ghi đè độ ưu tiên. Chỉ riêng độ ưu tiên không thể buộc các đối tượng opaque được vẽ chồng lên nhau.

Next Pass
---------

Việc thiết lập :ref:`next_pass<class_Material_property_next_pass>` trên một material sẽ khiến một đối tượng được kết xuất lại bằng next material đó.

Các material được sắp xếp theo hàng đợi opaque/transparent, sau đó theo :ref:`render_priority<class_Material_property_render_priority>`, với các material có độ ưu tiên cao hơn được vẽ sau.

.. image:: img/next_pass.webp

Depth sẽ cho kết quả bằng nhau giữa cả hai material, trừ khi sử dụng thiết lập grow hoặc các phép biến đổi vertex khác. Nhiều transparent pass nên sử dụng :ref:`render_priority<class_Material_property_render_priority>` để đảm bảo thứ tự chính xác.
