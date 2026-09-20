.. _doc_visibility_ranges:

Phạm vi hiển thị (HLOD)
=======================

Cùng với :ref:`doc_mesh_lod` và :ref:`doc_occlusion_culling`, phạm vi hiển thị là một công cụ khác để cải thiện hiệu năng trong các scene 3D lớn và phức tạp.

Trong trang này, bạn sẽ tìm hiểu:

- Những gì phạm vi hiển thị có thể thực hiện và những tình huống nào chúng hữu ích. - Cách thiết lập phạm vi hiển thị (LOD thủ công) trong Godot. - Cách tinh chỉnh phạm vi hiển thị để đạt hiệu năng và chất lượng tốt nhất.

.. seealso::

    Nếu bạn chỉ cần mesh trở nên ít chi tiết hơn theo khoảng cách, nhưng không có các mesh LOD được tạo thủ công, hãy cân nhắc dựa vào automatic
    :ref:`doc_mesh_lod` instead.

    Lưu ý rằng automatic mesh LOD và phạm vi hiển thị có thể được sử dụng cùng lúc, kể cả trên cùng một mesh.

Cách hoạt động
--------------

Phạm vi hiển thị có thể được sử dụng với bất kỳ node nào kế thừa từ GeometryInstance3D. Điều này có nghĩa là chúng không chỉ được dùng với MeshInstance3D và MultiMeshInstance3D cho :abbr:`HLOD (Hierarchical Level of Detail)` do artist kiểm soát, mà còn với GPUParticles3D, CPUParticles3D, Label3D, Sprite3D, AnimatedSprite3D và CSGShape3D.

Vì phạm vi hiển thị được cấu hình theo từng node, bạn có thể sử dụng các loại node khác nhau như một phần của hệ thống :abbr:`LOD (Level of Detail)`. Ví dụ: bạn có thể hiển thị một MeshInstance3D đại diện cho một cái cây khi ở gần, rồi thay thế nó bằng một impostor Sprite3D ở xa để cải thiện hiệu năng.

Lợi ích của :abbr:`HLOD (Hierarchical Level of Detail)` so với một
:abbr:`LOD (Level of Detail)` system is its hierarchical nature. A single larger
mesh có thể thay thế nhiều mesh nhỏ hơn, nhờ đó giảm số lượng draw call ở khoảng cách xa, nhưng vẫn giữ được các cơ hội culling khi ở gần. Ví dụ, bạn có thể có một nhóm ngôi nhà sử dụng các node MeshInstance3D riêng lẻ (mỗi node cho một ngôi nhà) khi ở gần, nhưng chuyển thành một MeshInstance3D duy nhất đại diện cho một nhóm ngôi nhà ít chi tiết hơn (hoặc sử dụng MultiMeshInstance3D).

Cuối cùng, phạm vi hiển thị cũng có thể được dùng để làm mờ hoàn toàn một số đối tượng khi camera ở quá gần hoặc quá xa. Điều này có thể được dùng cho mục đích gameplay, cũng như để giảm sự rối mắt về mặt hình ảnh. Ví dụ, các node Label3D có thể được làm mờ bằng phạm vi hiển thị khi chúng ở quá xa để người chơi có thể đọc hoặc không còn liên quan đến người chơi.

Thiết lập phạm vi hiển thị
--------------------------

Đây là hướng dẫn bắt đầu nhanh để cấu hình một hệ thống LOD cơ bản. Sau khi làm theo hướng dẫn này, hệ thống LOD sẽ hiển thị một SphereMesh khi ở gần và một BoxMesh khi camera đủ xa. Một khoảng hysteresis nhỏ cũng được cấu hình thông qua các thuộc tính **Begin Margin** và **End Margin**. Điều này ngăn LOD chuyển đổi qua lại quá nhanh khi camera di chuyển tại "rìa" của quá trình chuyển đổi LOD.

Bạn có thể tìm thấy các thuộc tính phạm vi hiển thị trong phần **Visibility Range** của inspector GeometryInstance3D sau khi chọn Node MeshInstance3D.

- Thêm một node Node3D để nhóm hai node MeshInstance3D lại với nhau. - Thêm node MeshInstance3D đầu tiên làm node con của Node3D. Gán một SphereMesh mới cho thuộc tính Mesh của node. - Đặt **End** trong phạm vi hiển thị của MeshInstance3D đầu tiên thành ``10.0`` và **End Margin** thành ``1.0``. - Thêm node MeshInstance3D thứ hai làm node con của Node3D. Gán một BoxMesh mới cho thuộc tính Mesh của node. - Đặt **Begin** trong phạm vi hiển thị của MeshInstance3D thứ hai thành ``10.0`` và **Begin Margin** thành ``1.0``. - Di chuyển camera ra xa rồi trở lại về phía đối tượng. Hãy chú ý cách đối tượng chuyển từ hình cầu sang hình hộp khi camera di chuyển ra xa.

Các thuộc tính phạm vi hiển thị
-------------------------------

Trong inspector của bất kỳ node nào kế thừa từ GeometryInstance3D, bạn có thể điều chỉnh các thuộc tính sau trong phần **Visibility Range** của GeometryInstance3D:

- **Begin:** Instance sẽ bị ẩn khi camera ở gần *tâm của AABB của instance* (axis-aligned bounding box) hơn giá trị này (tính theo đơn vị 3D). - **Begin Margin:** Khoảng cách chuyển tiếp hysteresis hoặc alpha fade được sử dụng cho quá trình chuyển đổi khi ở gần (tính theo đơn vị 3D). Cách hoạt động của thuộc tính này phụ thuộc vào **Fade Mode**. - **End:** Instance sẽ bị ẩn khi camera ở xa *tâm của AABB của instance* hơn giá trị này (tính theo đơn vị 3D). - **End Margin:** Khoảng cách chuyển tiếp hysteresis hoặc alpha fade được sử dụng cho quá trình chuyển đổi khi ở xa (tính theo đơn vị 3D). Cách hoạt động của thuộc tính này phụ thuộc vào **Fade Mode**. - **Fade Mode:** Kiểm soát cách thực hiện quá trình chuyển đổi giữa các cấp độ LOD. Xem chi tiết bên dưới.

.. _doc_visibility_ranges_fade_mode:

Chế độ fade
~~~~~~~~~~~

.. note::

    Chế độ fade đã chọn chỉ tạo ra khác biệt có thể nhìn thấy nếu **Visibility Range > Begin Margin** hoặc **Visibility Range > End Margin** lớn hơn ``0.0``.

Trong phần **Visibility Range** của inspector, có 3 chế độ fade để lựa chọn:

- **Disabled:** Sử dụng hysteresis để chuyển đổi tức thì giữa các cấp độ LOD. Điều này ngăn các tình huống cấp độ LOD bị chuyển đổi qua lại nhanh chóng khi người chơi di chuyển về phía trước rồi lùi lại tại điểm chuyển đổi LOD. Khoảng cách hysteresis được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này mang lại hiệu năng tốt nhất vì không buộc quá trình render trở nên trong suốt trong quá trình chuyển tiếp fade. - **Self:** Sử dụng alpha blending để chuyển tiếp mượt mà giữa các cấp độ LOD. Node sẽ tự fade-out khi đạt đến các giới hạn trong phạm vi hiển thị của chính nó. Khoảng cách chuyển tiếp fade được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này buộc đối tượng được render trong suốt trong quá trình chuyển tiếp fade, nên sẽ ảnh hưởng đến hiệu năng. - **Dependencies:** Sử dụng alpha blending để chuyển tiếp mượt mà giữa các cấp độ LOD. Node sẽ fade-in các dependency của nó khi đạt đến các giới hạn trong phạm vi hiển thị của chính nó. Khoảng cách chuyển tiếp fade được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này buộc đối tượng được render trong suốt trong quá trình chuyển tiếp fade, nên sẽ ảnh hưởng đến hiệu năng. Chế độ này dành cho các hệ thống LOD phân cấp sử dụng
  :ref:`Visibility parent <doc_visibility_ranges_visibility_parent>`. It acts
  giống như **Self** nếu phạm vi hiển thị được sử dụng để thực hiện LOD không phân cấp.

.. _doc_visibility_ranges_visibility_parent:

Visibility parent
~~~~~~~~~~~~~~~~~

Thuộc tính **Visibility Parent** giúp việc thiết lập trở nên dễ dàng hơn
:abbr:`HLOD (Hierarchical Level of Detail)`. It allows automatically hiding
các node con nếu node cha của chúng đang hiển thị dựa trên các thuộc tính phạm vi hiển thị hiện tại của nó.

.. note::

    Đối tượng đích của **Visibility Parent** *phải* kế thừa từ
    :ref:`class_GeometryInstance3D`.

    Mặc dù có tên như vậy, thuộc tính **Visibility Parent** *có thể* trỏ đến một node không phải là node cha của node đó trong scene tree. Tuy nhiên, không thể trỏ **Visibility Parent** đến một node con, vì điều này tạo ra một dependency cycle không được hỗ trợ. Bạn sẽ nhận được thông báo lỗi trong bảng Output nếu xảy ra dependency cycle.

Xét scene tree sau (trong đó tất cả các node đều kế thừa từ GeometryInstance3D):

::

    ┖╴BatchOfHouses
        ┠╴House1
        ┠╴House2
        ┠╴House3
        ┖╴House4

Trong ví dụ này, *BatchOfHouses* là một mesh lớn được thiết kế để đại diện cho tất cả các node con khi nhìn từ xa. *House1* đến *House4* là các MeshInstance3D nhỏ hơn đại diện cho từng ngôi nhà. Để cấu hình HLOD trong ví dụ này, chúng ta chỉ cần cấu hình hai điều:

- Đặt **Visibility Range Begin** thành một số lớn hơn `0.0` để *BatchOfHouses* chỉ xuất hiện khi đủ xa camera. Ở khoảng cách gần hơn, chúng ta muốn hiển thị *House1* đến *House4* thay thế. - Trên *House1* đến *House4*, gán thuộc tính **Visibility Parent** là *BatchOfHouses*.

Điều này giúp thực hiện các điều chỉnh tiếp theo dễ dàng hơn, vì bạn không cần điều chỉnh **Visibility Range Begin** của *BatchOfHouses* và **Visibility Range End** của *House1* đến *House4*.

Chế độ fade được thuộc tính **Visibility Parent** tự động xử lý, để các node con chỉ bị ẩn sau khi node cha đã fade-out hoàn toàn. Điều này nhằm giảm thiểu hiện tượng pop-in có thể nhìn thấy. Tùy thuộc vào thiết lập :abbr:`HLOD (Hierarchical Level of Detail)` của bạn, bạn có thể thử cả hai :ref:`fade modes <doc_visibility_ranges_fade_mode>` **Self** và **Dependencies**.

.. note::

    Các node bị ẩn thông qua thuộc tính **Visible** về cơ bản sẽ bị loại khỏi cây dependency hiển thị, vì vậy các instance phụ thuộc sẽ không tính đến node bị ẩn hoặc các ancestor của node đó.

    Trên thực tế, điều này có nghĩa là nếu đối tượng đích của node **Visibility Parent** bị ẩn bằng cách đặt thuộc tính **Visible** thành ``false``, node đó sẽ không bị ẩn theo giá trị **Visibility Range Begin** được chỉ định trong visibility parent.

Mẹo cấu hình
------------

Sử dụng material đơn giản hơn ở khoảng cách xa để cải thiện hiệu năng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một cách để cải thiện hiệu năng hơn nữa là sử dụng material đơn giản hơn cho các mesh LOD ở xa. Mặc dù sử dụng mesh LOD sẽ giảm số lượng vertex cần render, tải shading trên mỗi pixel của material vẫn giữ nguyên. Tuy nhiên, tải shading trên mỗi pixel thường là một điểm nghẽn trên GPU trong các scene 3D phức tạp. Một cách để giảm tải shading này trên GPU là sử dụng material đơn giản hơn khi việc đó không tạo ra nhiều khác biệt về mặt hình ảnh.

Cần đo lường cẩn thận mức tăng hiệu năng khi làm như vậy, vì việc tăng số lượng material *unique* trong một scene cũng có chi phí hiệu năng riêng. Tuy vậy, sử dụng material đơn giản hơn cho các mesh LOD ở xa vẫn có thể mang lại mức tăng hiệu năng tổng thể nhờ cần ít phép tính trên mỗi pixel hơn.

Ví dụ, trên các material được sử dụng bởi các mesh LOD ở xa, bạn có thể tắt các tính năng material tốn kém như:

- Normal Map (đặc biệt trên các nền tảng di động) - Rim - Clearcoat - Anisotropy - Height - Subsurface Scattering - Back Lighting - Refraction - Proximity Fade

Sử dụng dithering cho các chuyển tiếp LOD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiện tại, Godot chỉ hỗ trợ hiệu ứng mờ dần dựa trên alpha cho các phạm vi hiển thị. Tuy nhiên, bạn có thể sử dụng dithering thay thế bằng cách dùng một số material khác nhau cho các cấp LOD khác nhau.

Có hai ưu điểm khi sử dụng dithering thay cho alpha blending cho các chuyển tiếp LOD:

- Hiệu năng cao hơn, vì độ trong suốt bằng dithering được render nhanh hơn so với alpha blending. - Không có lỗi hiển thị do
  :ref:`transparency sorting issues <doc_3d_rendering_limitations_transparency_sorting>`
  trong quá trình chuyển tiếp LOD.

Nhược điểm của dithering là một mẫu "nhiễu" sẽ hiển thị trong quá trình chuyển tiếp mờ dần của LOD. Điều này có thể ít замет hơn ở các độ phân giải viewport cao hơn hoặc khi bật temporal antialiasing.

Ngoài ra, vì distance fade trong BaseMaterial3D chỉ hỗ trợ mờ dần khi ở gần *hoặc* khi ở xa, thiết lập này phù hợp nhất khi chỉ sử dụng hai LOD trong cùng một thiết lập.

- Đảm bảo **Begin Margin** và **End Margin** được đặt thành ``0.0`` trên cả hai node MeshInstance3D, vì ở đây không cần hysteresis hoặc alpha fade. - Trên cả hai node MeshInstance3D, *giảm* **Begin** theo khoảng cách chuyển tiếp mờ dần mong muốn và *tăng* **End** thêm cùng khoảng cách đó. Điều này cần thiết để chuyển tiếp dithering thực sự hiển thị. - Trên MeshInstance3D được hiển thị ở khoảng cách gần, hãy chỉnh sửa material của nó trong inspector. Đặt chế độ **Distance Fade** thành **Object Dither**. Đặt **Min Distance** thành cùng giá trị với **End** của phạm vi hiển thị. Đặt **Max Distance** thành cùng giá trị đó *trừ đi* khoảng cách chuyển tiếp mờ dần. - Trên MeshInstance3D được hiển thị ở khoảng cách xa, hãy chỉnh sửa material của nó trong inspector. Đặt chế độ **Distance Fade** thành **Object Dither**. Đặt **Min Distance** thành cùng giá trị với **Begin** của phạm vi hiển thị. Đặt **Max Distance** thành cùng giá trị đó *cộng thêm* khoảng cách chuyển tiếp mờ dần.
