.. _doc_visibility_ranges:

Phạm vi hiển thị (HLOD)
=======================

Cùng với :ref:`doc_mesh_lod` và :ref:`doc_occlusion_culling`, phạm vi hiển thị là một công cụ khác giúp cải thiện hiệu suất trong các cảnh 3D lớn và phức tạp.

Trên trang này, bạn sẽ học:

- Phạm vi hiển thị có thể làm được gì và hữu ích trong những trường hợp nào.
- Cách thiết lập phạm vi hiển thị (LOD thủ công) trong Godot.
- Cách tinh chỉnh phạm vi hiển thị để đạt hiệu suất và chất lượng tốt nhất.

.. seealso::

    Nếu bạn chỉ cần mesh trở nên ít chi tiết hơn theo khoảng cách, nhưng không có mesh LOD được tạo thủ công, hãy cân nhắc sử dụng LOD mesh tự động
    :ref:`doc_mesh_lod` thay vào đó.

    Lưu ý rằng LOD mesh tự động và phạm vi hiển thị có thể được sử dụng cùng lúc, ngay cả trên cùng một mesh.

Cách thức hoạt động
-------------------

Phạm vi hiển thị có thể được sử dụng với bất kỳ node nào kế thừa từ GeometryInstance3D. Điều này có nghĩa là chúng không chỉ dùng được với MeshInstance3D và MultiMeshInstance3D cho :abbr:`HLOD (Mức độ chi tiết phân cấp)` do nghệ sĩ kiểm soát, mà còn với GPUParticles3D, CPUParticles3D, Label3D, Sprite3D, AnimatedSprite3D và CSGShape3D.

Vì phạm vi hiển thị được cấu hình theo từng node, bạn có thể sử dụng các loại node khác nhau như một phần của hệ thống :abbr:`LOD (Mức độ chi tiết)`. Ví dụ, bạn có thể hiển thị một MeshInstance3D đại diện cho một cái cây khi ở gần, rồi thay thế nó bằng một impostor Sprite3D ở xa để cải thiện hiệu suất.

Lợi ích của :abbr:`HLOD (Mức độ chi tiết phân cấp)` so với hệ thống
:abbr:`LOD (Mức độ chi tiết)` truyền thống nằm ở tính phân cấp của nó. Một mesh lớn duy nhất có thể thay thế nhiều mesh nhỏ hơn, nhờ đó giảm số draw call ở khoảng cách xa, đồng thời vẫn duy trì các cơ hội culling khi ở gần. Ví dụ, bạn có thể có một nhóm nhà sử dụng các node MeshInstance3D riêng lẻ (mỗi node cho một ngôi nhà) khi ở gần, nhưng chuyển thành một MeshInstance3D duy nhất đại diện cho một nhóm nhà ít chi tiết hơn (hoặc sử dụng một MultiMeshInstance3D).

Cuối cùng, phạm vi hiển thị cũng có thể được dùng để làm mờ hoàn toàn một số đối tượng khi camera ở quá gần hoặc quá xa. Tính năng này có thể phục vụ mục đích gameplay, đồng thời giúp giảm sự lộn xộn về mặt hình ảnh. Ví dụ, các node Label3D có thể được làm mờ bằng phạm vi hiển thị khi chúng ở quá xa để người chơi đọc được hoặc không còn liên quan đến người chơi.

Thiết lập phạm vi hiển thị
--------------------------

Đây là hướng dẫn bắt đầu nhanh để cấu hình một hệ thống LOD cơ bản. Sau khi làm theo hướng dẫn này, hệ thống LOD sẽ hiển thị một SphereMesh khi ở gần và một BoxMesh khi camera đủ xa. Một khoảng hysteresis nhỏ cũng được cấu hình thông qua các thuộc tính **Begin Margin** và **End Margin**. Điều này ngăn LOD chuyển đổi qua lại quá nhanh khi camera di chuyển ở "ranh giới" chuyển đổi LOD.

Bạn có thể tìm thấy các thuộc tính phạm vi hiển thị trong mục **Visibility Range** của inspector GeometryInstance3D sau khi chọn Node MeshInstance3D.

- Thêm một node Node3D để nhóm hai node MeshInstance3D lại với nhau.
- Thêm node MeshInstance3D đầu tiên làm node con của Node3D. Gán một SphereMesh mới cho thuộc tính Mesh của nó.
- Đặt **End** trong phạm vi hiển thị của MeshInstance3D đầu tiên thành ``10.0`` và **End Margin** thành ``1.0``.
- Thêm node MeshInstance3D thứ hai làm node con của Node3D. Gán một BoxMesh mới cho thuộc tính Mesh của nó.
- Đặt **Begin** trong phạm vi hiển thị của MeshInstance3D thứ hai thành ``10.0`` và **Begin Margin** thành ``1.0``.
- Di chuyển camera ra xa rồi tiến lại gần đối tượng. Hãy chú ý cách đối tượng chuyển từ hình cầu sang hình hộp khi camera di chuyển ra xa.

Các thuộc tính phạm vi hiển thị
-------------------------------

Trong inspector của bất kỳ node nào kế thừa từ GeometryInstance3D, bạn có thể điều chỉnh các thuộc tính sau trong mục **Visibility Range** của GeometryInstance3D:

- **Begin:** Instance sẽ bị ẩn khi camera gần *tâm của AABB của instance* (hộp giới hạn căn chỉnh theo trục) hơn giá trị này (tính theo đơn vị 3D).
- **Begin Margin:** Khoảng cách chuyển tiếp hysteresis hoặc alpha fade được sử dụng cho quá trình chuyển đổi khi ở gần (tính theo đơn vị 3D). Cách hoạt động của thuộc tính này phụ thuộc vào **Fade Mode**.
- **End:** Instance sẽ bị ẩn khi camera cách *tâm của AABB của instance* xa hơn giá trị này (tính theo đơn vị 3D).
- **End Margin:** Khoảng cách chuyển tiếp hysteresis hoặc alpha fade được sử dụng cho quá trình chuyển đổi khi ở xa (tính theo đơn vị 3D). Cách hoạt động của thuộc tính này phụ thuộc vào **Fade Mode**.
- **Fade Mode:** Kiểm soát cách thực hiện chuyển đổi giữa các cấp độ LOD. Xem chi tiết bên dưới.

.. _doc_visibility_ranges_fade_mode:

Chế độ fade
~~~~~~~~~~~

.. note::

    Chế độ fade được chọn chỉ tạo ra thay đổi rõ rệt nếu **Visibility Range > Begin Margin** hoặc **Visibility Range > End Margin** lớn hơn ``0.0``.

Trong mục **Visibility Range** của inspector, có 3 chế độ fade để lựa chọn:

- **Disabled:** Sử dụng hysteresis để chuyển đổi tức thời giữa các cấp độ LOD. Điều này ngăn những tình huống các cấp độ LOD chuyển đổi qua lại nhanh chóng khi người chơi di chuyển về phía trước rồi lùi lại tại điểm chuyển đổi LOD. Khoảng cách hysteresis được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này mang lại hiệu suất tốt nhất vì không buộc quá trình render trở nên trong suốt trong quá trình chuyển tiếp fade.
- **Self:** Sử dụng alpha blending để chuyển đổi mượt mà giữa các cấp độ LOD. Node sẽ tự fade-out khi đạt đến giới hạn phạm vi hiển thị của chính nó. Khoảng cách chuyển tiếp fade được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này buộc đối tượng được render trong suốt trong quá trình chuyển tiếp fade, do đó ảnh hưởng đến hiệu suất.
- **Dependencies:** Sử dụng alpha blending để chuyển đổi mượt mà giữa các cấp độ LOD. Node sẽ fade-in các dependency của nó khi đạt đến giới hạn phạm vi hiển thị của chính nó. Khoảng cách chuyển tiếp fade được xác định bởi **Visibility Range > Begin Margin** và **Visibility Range > End Margin**. Chế độ này buộc đối tượng được render trong suốt trong quá trình chuyển tiếp fade, do đó ảnh hưởng đến hiệu suất. Chế độ này dành cho các hệ thống LOD phân cấp sử dụng
  :ref:`Visibility parent <doc_visibility_ranges_visibility_parent>`. Nó hoạt động giống **Self** khi sử dụng các phạm vi khả năng hiển thị để thực hiện LOD không phân cấp.

.. _doc_visibility_ranges_visibility_parent:

Đối tượng cha về khả năng hiển thị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Thuộc tính **Visibility Parent** giúp thiết lập
:abbr:`HLOD (Hierarchical Level of Detail)`. Thuộc tính này cho phép tự động ẩn các node con nếu node cha của chúng đang hiển thị dựa trên các thuộc tính phạm vi khả năng hiển thị hiện tại của node cha.

.. note::

    Đối tượng đích của **Visibility Parent** *must* kế thừa từ
    :ref:`class_GeometryInstance3D`.

    Mặc dù có tên như vậy, thuộc tính **Visibility Parent** *can* trỏ đến một node không phải là node cha của node đó trong cây cảnh. Tuy nhiên, không thể trỏ **Visibility Parent** đến một node con, vì điều này tạo ra một chu kỳ phụ thuộc không được hỗ trợ. Bạn sẽ nhận được thông báo lỗi trong bảng Output nếu xảy ra chu kỳ phụ thuộc.

Với cây cảnh sau (trong đó tất cả các node đều kế thừa từ GeometryInstance3D):

::

    ┖╴BatchOfHouses
        ┠╴House1
        ┠╴House2
        ┠╴House3
        ┖╴House4

Trong ví dụ này, *BatchOfHouses* là một mesh lớn được thiết kế để đại diện cho tất cả các node con khi nhìn từ xa. *House1* đến *House4* là các MeshInstance3D nhỏ hơn, đại diện cho từng ngôi nhà. Để cấu hình HLOD trong ví dụ này, chúng ta chỉ cần cấu hình hai điều:

- Đặt **Visibility Range Begin** thành một số lớn hơn `0.0` để *BatchOfHouses* chỉ xuất hiện khi ở đủ xa camera. Ở khoảng cách gần hơn, chúng ta muốn hiển thị *House1* đến *House4* thay thế.
- Trên các node từ *House1* đến *House4*, gán thuộc tính **Visibility Parent** cho *BatchOfHouses*.

Điều này giúp thực hiện các điều chỉnh tiếp theo dễ dàng hơn, vì bạn không cần điều chỉnh **Visibility Range Begin** của *BatchOfHouses* và **Visibility Range End** của các node từ *House1* đến *House4*.

Chế độ mờ dần được thuộc tính **Visibility Parent** tự động xử lý, để các node con chỉ bị ẩn sau khi node cha đã mờ hoàn toàn. Cách này nhằm giảm thiểu hiện tượng xuất hiện đột ngột. Tùy thuộc vào thiết lập :abbr:`HLOD (Hierarchical Level of Detail)` của bạn, bạn có thể thử cả hai **Self** và **Dependencies** :ref:`fade modes <doc_visibility_ranges_fade_mode>`.

.. note::

    Các node bị ẩn thông qua thuộc tính **Visible** về cơ bản sẽ bị loại khỏi cây phụ thuộc khả năng hiển thị, vì vậy các instance phụ thuộc sẽ không tính đến node bị ẩn hoặc các node tổ tiên của nó.

    Trên thực tế, điều này có nghĩa là nếu node đích của **Visibility Parent** bị ẩn bằng cách đặt thuộc tính **Visible** thành ``false``, node đó sẽ không bị ẩn theo giá trị **Visibility Range Begin** được chỉ định trong đối tượng cha về khả năng hiển thị.

Mẹo cấu hình
------------

Sử dụng material đơn giản hơn ở khoảng cách xa để cải thiện hiệu suất
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một cách để tiếp tục cải thiện hiệu suất là sử dụng material đơn giản hơn cho các mesh LOD ở xa. Mặc dù việc sử dụng mesh LOD sẽ giảm số vertex cần render, tải shading trên mỗi pixel của material vẫn không đổi. Tuy nhiên, tải shading trên mỗi pixel thường là một điểm nghẽn trên GPU trong các cảnh 3D phức tạp. Một cách để giảm tải shading này trên GPU là sử dụng material đơn giản hơn khi chúng không tạo ra nhiều khác biệt về mặt hình ảnh.

Cần đo lường cẩn thận mức cải thiện hiệu suất đạt được, vì việc tăng số lượng material *unique* trong một cảnh tự nó đã gây tốn hiệu suất. Tuy vậy, sử dụng material đơn giản hơn cho các mesh LOD ở xa vẫn có thể mang lại hiệu suất tổng thể tốt hơn nhờ cần ít phép tính trên mỗi pixel hơn.

Ví dụ: trong các material được dùng cho mesh LOD ở xa, bạn có thể tắt các tính năng material tốn kém như:

- Normal Map (đặc biệt trên các nền tảng di động)
- Rim
- Clearcoat
- Anisotropy
- Height
- Subsurface Scattering
- Back Lighting
- Refraction
- Proximity Fade

Sử dụng dithering cho các chuyển tiếp LOD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiện tại Godot chỉ hỗ trợ làm mờ dựa trên alpha cho các phạm vi khả năng hiển thị. Tuy nhiên, bạn có thể sử dụng dithering thay thế bằng cách dùng một số material khác nhau cho các cấp độ LOD khác nhau.

Sử dụng dithering thay vì alpha blending cho các chuyển tiếp LOD có hai ưu điểm:

- Hiệu suất cao hơn, vì transparency bằng dithering render nhanh hơn so với alpha blending.
- Không có lỗi hình ảnh do
  :ref:`transparency sorting issues <doc_3d_rendering_limitations_transparency_sorting>` trong các chuyển tiếp LOD.

Nhược điểm của dithering là một mẫu "nhiễu" sẽ hiển thị trong quá trình chuyển tiếp mờ dần LOD. Hiện tượng này có thể ít замет hơn ở độ phân giải viewport cao hơn hoặc khi bật khử răng cưa theo thời gian.

Ngoài ra, vì distance fade trong BaseMaterial3D chỉ hỗ trợ làm mờ khi ở gần *or* làm mờ khi ở xa, thiết lập này phù hợp nhất khi chỉ sử dụng hai LOD trong thiết lập.

- Đảm bảo **Begin Margin** và **End Margin** đều được đặt thành ``0.0`` trên cả hai node MeshInstance3D, vì ở đây không cần hysteresis hoặc alpha fade.
- Trên cả hai node MeshInstance3D, *decrease* **Begin** theo khoảng cách chuyển tiếp mờ dần mong muốn và *increase* **End** theo cùng khoảng cách đó. Điều này cần thiết để chuyển tiếp dithering thực sự hiển thị.
- Trên MeshInstance3D được hiển thị ở khoảng cách gần, hãy chỉnh sửa material của nó trong inspector. Đặt chế độ **Distance Fade** thành **Object Dither**. Đặt **Min Distance** thành cùng giá trị với **End** của visibility range. Đặt **Max Distance** thành cùng giá trị *trừ* khoảng cách chuyển tiếp fade.
- Trên MeshInstance3D được hiển thị ở khoảng cách xa, hãy chỉnh sửa material của nó trong inspector. Đặt chế độ **Distance Fade** thành **Object Dither**. Đặt **Min Distance** thành cùng giá trị với **Begin** của visibility range. Đặt **Max Distance** thành cùng giá trị *cộng* khoảng cách chuyển tiếp fade.
