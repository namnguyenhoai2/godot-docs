.. _doc_tscn_file_format:

Định dạng tệp TSCN
==================

Định dạng tệp TSCN (text scene) biểu diễn một cây scene đơn trong Godot. Không giống các tệp SCN nhị phân, tệp TSCN có ưu điểm là phần lớn có thể đọc được và dễ quản lý bằng các hệ thống kiểm soát phiên bản.

Định dạng tệp ESCN (exported scene) giống hệt định dạng tệp TSCN, nhưng được dùng để cho Godot biết rằng tệp đã được export từ một chương trình khác và người dùng không nên chỉnh sửa tệp từ bên trong Godot. Không giống các tệp SCN và TSCN, trong quá trình import, các tệp ESCN được biên dịch thành các tệp SCN nhị phân lưu trong thư mục ``.godot/imported/``. Điều này làm giảm kích thước dữ liệu và tăng tốc độ tải, vì các định dạng nhị phân tải nhanh hơn so với các định dạng dựa trên văn bản.

Để làm cho tệp gọn hơn, các thuộc tính có giá trị bằng giá trị mặc định sẽ không được lưu trong các tệp scene/resource. Bạn có thể tự ghi chúng, nhưng chúng sẽ bị loại bỏ khi lưu tệp.

Nếu cần mô tả đầy đủ, việc phân tích cú pháp được xử lý trong tệp `resource_format_text.cpp <https://github.com/godotengine/godot/blob/master/scene/resources/resource_format_text.cpp>`_ thuộc lớp ``ResourceFormatLoaderText``.

.. note::

    Định dạng tệp scene và resource đã thay đổi đáng kể trong Godot 4, với việc giới thiệu UID dựa trên chuỗi để thay thế các ID số nguyên tăng dần.

    Dữ liệu mesh, skeleton và animation cũng được lưu khác so với Godot 3. Bạn có thể đọc về một số thay đổi trong bài viết này: `Animation data rework for 4.0 <https://godotengine.org/article/animation-data-redesign-40/>`__

    Các scene và resource được lưu bằng Godot 4.x chứa ``format=3`` trong phần header, trong khi Godot 3.x sử dụng ``format=2``.

Cấu trúc tệp
------------

Có năm phần chính bên trong tệp TSCN:

0. Mô tả tệp
1. Resource bên ngoài
2. Resource nội bộ
3. Node
4. Kết nối

Mô tả tệp có dạng ``[gd_scene format=3 uid="uid://cecaux1sm7mo0"]`` và phải là mục đầu tiên trong tệp. Lưu ý rằng các scene được lưu trước Godot 4.6 cũng sẽ có thuộc tính ``load_steps=<int>`` trong mô tả tệp. Thuộc tính này hiện đã lỗi thời và nên được bỏ qua nếu có.

``uid`` là một mã định danh duy nhất dựa trên chuỗi, đại diện cho scene. Engine dùng mã này để theo dõi các tệp được di chuyển, kể cả khi editor đang đóng. Script cũng có thể tải các resource dựa trên UID bằng tiền tố đường dẫn ``uid://`` để tránh phụ thuộc vào đường dẫn hệ thống tệp. Nhờ đó, bạn có thể di chuyển một tệp trong project mà vẫn tải được tệp đó trong script mà không cần sửa script. Godot không dùng các tệp bên ngoài để theo dõi ID, nghĩa là không cần vị trí lưu trữ metadata tập trung trong project. Xem `this pull request <https://github.com/godotengine/godot/pull/50786>`__ để biết thông tin chi tiết.

Các phần này phải xuất hiện theo đúng thứ tự, nhưng có thể khó phân biệt chúng. Điểm khác biệt duy nhất giữa chúng là phần tử đầu tiên trong heading của tất cả các mục thuộc phần đó. Ví dụ, heading của tất cả resource bên ngoài phải bắt đầu bằng ``[ext_resource ...]``.

Tệp TSCN có thể chứa các comment một dòng bắt đầu bằng dấu chấm phẩy (``;``). Tuy nhiên, comment sẽ bị loại bỏ khi lưu tệp bằng Godot editor. Khoảng trắng trong tệp TSCN không có ý nghĩa (ngoại trừ bên trong chuỗi), nhưng khoảng trắng thừa sẽ bị loại bỏ khi lưu tệp.

Các mục bên trong tệp
~~~~~~~~~~~~~~~~~~~~~

Một heading có dạng ``[<resource_type> key1=value1 key2=value2 key3=value3 ...]``, trong đó resource_type là một trong các giá trị sau:

- ``ext_resource``
- ``sub_resource``
- ``node``
- ``connection``

Bên dưới mỗi heading là không hoặc nhiều cặp ``key = value``. Các giá trị có thể là những kiểu dữ liệu phức tạp như Array, Transform, Color, v.v. Ví dụ, một Node3D có dạng:

::

    [node name="Cube" type="Node3D" unique_id=224283918]
    transform = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 1, 2, 3)

Cây scene
---------

Cây scene được tạo thành từ… các node! Heading của mỗi node gồm tên, parent, một ID duy nhất (dùng để theo dõi node ngay cả khi node được di chuyển hoặc đổi tên), và trong hầu hết trường hợp là một kiểu. Ví dụ: ``[node name="PlayerCamera" type="Camera" parent="Player/Head" unique_id=1697057368]``

Lưu ý rằng ``unique_id`` chỉ xuất hiện trong các scene được lưu bằng Godot 4.6 trở lên. Vì vậy, không đảm bảo rằng mục này luôn có mặt.

Các keyword hợp lệ khác gồm:

 - ``instance``
 - ``instance_placeholder``
 - ``owner``
 - ``index`` (đặt thứ tự xuất hiện trong cây; nếu không có, các node kế thừa sẽ được ưu tiên hơn các node thông thường)
 - ``groups``
 - ``node_paths`` (liệt kê tên các thuộc tính được export dưới dạng Node, nhưng được tham chiếu dưới dạng NodePath trong tệp)

Node đầu tiên trong tệp, cũng là scene root, **không** được có mục ``parent="Path/To/Node"`` trong heading. Tất cả các tệp scene phải có chính xác *một* scene root. Nếu không, Godot sẽ không thể import tệp. Đường dẫn parent của các node khác phải là đường dẫn tuyệt đối, nhưng không được chứa tên scene root. Nếu node là node con trực tiếp của scene root, đường dẫn phải là ``"."``. Sau đây là một ví dụ về cây scene (nhưng không có nội dung node nào):

::

    [node name="Player" type="Node3D" unique_id=1155673912]                    ; The scene root
    [node name="Arm" type="Node3D" parent="." unique_id=1010797352]            ; Parented to the scene root
    [node name="Hand" type="Node3D" parent="Arm" unique_id=536436825]          ; Child of "Arm"
    [node name="Finger" type="Node3D" parent="Arm/Hand" unique_id=1732647084]  ; Child of "Hand"

.. tip::

    Để dễ nắm bắt cấu trúc tệp hơn, bạn có thể lưu một tệp chứa bất kỳ node hoặc resource nào, rồi tự kiểm tra tệp đó trong một editor bên ngoài. Bạn cũng có thể thực hiện các thay đổi từng bước trong Godot editor và mở tệp ``.tscn`` hoặc ``.tres`` bằng một trình soạn thảo văn bản bên ngoài, bật tính năng tự động tải lại để xem các thay đổi.

Sau đây là ví dụ về một scene chứa một quả bóng dựa trên RigidBody3D với collision, phần hiển thị (mesh + light) và một camera được đặt làm con của RigidBody3D:

::

    [gd_scene format=3 uid="uid://cecaux1sm7mo0"]

    [sub_resource type="SphereShape3D" id="SphereShape3D_tj6p1"]

    [sub_resource type="SphereMesh" id="SphereMesh_4w3ye"]

    [sub_resource type="StandardMaterial3D" id="StandardMaterial3D_k54se"]
    albedo_color = Color(1, 0.639216, 0.309804, 1)

    [node name="Ball" type="RigidBody3D" unique_id=1358867382]

    [node name="CollisionShape3D" type="CollisionShape3D" parent="." unique_id=1279975976]
    shape = SubResource("SphereShape3D_tj6p1")

    [node name="MeshInstance3D" type="MeshInstance3D" parent="." unique_id=558852834]
    mesh = SubResource("SphereMesh_4w3ye")
    surface_material_override/0 = SubResource("StandardMaterial3D_k54se")

    [node name="OmniLight3D" type="OmniLight3D" parent="." unique_id=1581292810 node_paths=PackedStringArray("follow_node")]
    light_color = Color(1, 0.698039, 0.321569, 1)
    omni_range = 10.0
    follow_node = NodePath("..")

    [node name="Camera3D" type="Camera3D" parent="." unique_id=795715540]
    transform = Transform3D(1, 0, 0, 0, 0.939693, 0.34202, 0, -0.34202, 0.939693, 0, 1, 3)

NodePath
~~~~~~~~

Một cấu trúc cây là chưa đủ để biểu diễn toàn bộ scene. Godot sử dụng cấu trúc ``NodePath(Path/To/Node)`` để tham chiếu đến một node khác hoặc một thuộc tính của node ở bất kỳ đâu trong cây scene. Các path có tính tương đối so với node hiện tại, trong đó ``NodePath(".")`` trỏ đến node hiện tại và ``NodePath("")`` trỏ đến không node nào cả.

Ví dụ, MeshInstance3D sử dụng ``NodePath()`` để trỏ đến skeleton của nó. Tương tự, các track Animation sử dụng ``NodePath()`` để trỏ đến các thuộc tính node cần animate.

NodePath cũng có thể trỏ đến một thuộc tính bằng hậu tố ``:property_name``, thậm chí trỏ đến một component cụ thể đối với các kiểu vector, transform và color. Resource Animation sử dụng tính năng này để trỏ đến các thuộc tính cụ thể cần animate. Ví dụ, ``NodePath("MeshInstance3D:scale.x")`` trỏ đến component ``x`` của thuộc tính Vector3 ``scale`` trong MeshInstance3D.

Ví dụ, thuộc tính ``skeleton`` trong node MeshInstance3D có tên ``mesh`` trỏ đến parent của nó, ``Armature01``:

::

    [node name="mesh" type="MeshInstance3D" parent="Armature01" unique_id=1638249225]
    skeleton = NodePath("..")

Skeleton3D
~~~~~~~~~~

Node :ref:`class_Skeleton3D` kế thừa node Node3D, nhưng cũng có thể có một danh sách bone được mô tả bằng các cặp key-value theo định dạng ``bones/<id>/<attribute> = value``. Các thuộc tính của bone gồm:

- ``position``: Vector3
- ``rotation``: Quaternion
- ``scale``: Vector3

Tất cả các thuộc tính này đều là tùy chọn. Ví dụ, một bone có thể chỉ định nghĩa ``position`` hoặc ``rotation`` mà không định nghĩa các thuộc tính còn lại.

Sau đây là ví dụ về một node skeleton có hai bone:

::

    [node name="Skeleton3D" type="Skeleton3D" parent="PlayerModel/Robot_Skeleton" index="0" unique_id=542985694]
    bones/1/position = Vector3(0.114471, 2.19771, -0.197845)
    bones/1/rotation = Quaternion(0.191422, -0.0471201, -0.00831942, 0.980341)
    bones/2/position = Vector3(-2.59096e-05, 0.236002, 0.000347473)
    bones/2/rotation = Quaternion(-0.0580488, 0.0310587, -0.0085914, 0.997794)
    bones/2/scale = Vector3(0.9276, 0.9276, 0.9276)

BoneAttachment3D
~~~~~~~~~~~~~~~~

Nút :ref:`class_BoneAttachment3D` là một nút trung gian dùng để mô tả một nút được gắn làm nút con của một xương duy nhất trong một nút Skeleton. BoneAttachment có thuộc tính ``bone_name = "name of bone"``, cũng như một thuộc tính cho chỉ số xương tương ứng.

Ví dụ về một nút :ref:`class_Marker3D` được gắn làm nút con của một xương trong Skeleton:

::

    [node name="GunBone" type="BoneAttachment3D" parent="PlayerModel/Robot_Skeleton/Skeleton3D" index="5" unique_id=63481392]
    transform = Transform3D(0.333531, 0.128981, -0.933896, 0.567174, 0.763886, 0.308015, 0.753209, -0.632331, 0.181604, -0.323915, 1.07098, 0.0497144)
    bone_name = "hand.R"
    bone_idx = 55

    [node name="ShootFrom" type="Marker3D" parent="PlayerModel/Robot_Skeleton/Skeleton3D/GunBone" unique_id=679926736]
    transform = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0.4, 0)

AnimationPlayer
~~~~~~~~~~~~~~~

Nút :ref:`class_AnimationPlayer` hoạt động với một hoặc nhiều thư viện animation được lưu trong các resource :ref:`class_AnimationLibrary`. Một thư viện animation là tập hợp các resource :ref:`class_Animation` riêng lẻ, cấu trúc của chúng được ghi lại :ref:`tại đây <doc_tscn_animation>`.

Phần tách animation và thư viện animation được thực hiện trong Godot 4, để các animation có thể được import riêng khỏi các mesh 3D, đây là quy trình phổ biến trong phần mềm animation 3D. Xem `pull request gốc <https://github.com/godotengine/godot/pull/59980>`__ để biết chi tiết.

Nếu tên thư viện trống, thư viện đó sẽ đóng vai trò là nguồn animation duy nhất cho AnimationPlayer này. Điều này cho phép sử dụng ``<animation_name>`` trực tiếp để phát animation từ script. Nếu đặt tên cho thư viện, bạn phải phát thư viện đó dưới dạng ``<library_name>/<animation_name>``. Điều này đảm bảo khả năng tương thích ngược và duy trì quy trình hiện có nếu bạn không muốn sử dụng nhiều thư viện animation.

Resources
---------

Resources là các thành phần cấu tạo nên các node. Ví dụ, một node MeshInstance3D sẽ có một resource ArrayMesh đi kèm. Resource ArrayMesh có thể là nội bộ hoặc bên ngoài tệp TSCN.

Các tham chiếu đến resource được xử lý bằng các ID dựa trên chuỗi duy nhất trong phần tiêu đề của resource. Điều này khác với thuộc tính ``uid``, thuộc tính mà mỗi external resource cũng có (nhưng subresource thì không).

External resource và internal resource lần lượt được tham chiếu bằng ``ExtResource("id")`` và ``SubResource("id")``. Vì có các phương thức khác nhau để tham chiếu internal resource và external resource, bạn có thể sử dụng cùng một ID cho cả một internal resource và một external resource.

Ví dụ, để tham chiếu đến resource ``[ext_resource type="Material" uid="uid://c4cp0al3ljsjv" path="res://material.tres" id="1_7bt6s"]``, bạn sẽ sử dụng ``ExtResource("1_7bt6s")``.

External resources
~~~~~~~~~~~~~~~~~~

External resource là các liên kết đến những resource không nằm trong chính tệp TSCN. Một external resource bao gồm một đường dẫn, một kiểu, một UID (dùng để ánh xạ vị trí của nó trong filesystem với một mã định danh duy nhất) và một ID (dùng để tham chiếu resource trong tệp scene).

Godot luôn tạo các đường dẫn tuyệt đối tương đối với thư mục resource và do đó được thêm tiền tố ``res://``, nhưng các đường dẫn tương đối với vị trí của tệp TSCN cũng hợp lệ.

Một số ví dụ về external resource là:

::

    [ext_resource type="Texture2D" uid="uid://ccbm14ebjmpy1" path="res://gradient.tres" id="2_eorut"]
    [ext_resource type="Material" uid="uid://c4cp0al3ljsjv" path="material.tres" id="1_7bt6s"]

Tương tự tệp TSCN, tệp TRES có thể chứa các chú thích một dòng bắt đầu bằng dấu chấm phẩy (``;``). Tuy nhiên, các chú thích sẽ bị loại bỏ khi lưu resource bằng Godot editor. Khoảng trắng trong tệp TRES không có ý nghĩa (ngoại trừ bên trong chuỗi), nhưng khoảng trắng thừa sẽ bị loại bỏ khi lưu tệp.

Internal resources
~~~~~~~~~~~~~~~~~~

Một tệp TSCN có thể chứa mesh, material và dữ liệu khác. Chúng nằm trong phần *internal resources* của tệp. Tiêu đề của một internal resource trông tương tự tiêu đề của external resource, ngoại trừ việc không có đường dẫn. Internal resource cũng có các cặp ``key=value`` bên dưới mỗi tiêu đề. Ví dụ, một capsule collision shape có dạng:

::

    [sub_resource type="CapsuleShape3D" id="CapsuleShape3D_fdxgg"]
    radius = 1.0
    height = 3.0

Một số internal resource chứa các liên kết đến những internal resource khác (chẳng hạn một mesh có một material). Trong trường hợp này, resource được tham chiếu phải xuất hiện *trước* tham chiếu đến nó. Điều này có nghĩa là thứ tự rất quan trọng trong phần internal resources của tệp.

ArrayMesh
~~~~~~~~~

Một ArrayMesh bao gồm nhiều surface nằm trong mảng ``_surfaces`` (lưu ý dấu gạch dưới ở đầu). Dữ liệu của mỗi surface được lưu trong một dictionary với các key sau:

- ``aabb``: Hộp giới hạn căn chỉnh theo trục được tính toán để xác định khả năng hiển thị.
- ``attribute_data``: Dữ liệu thuộc tính vertex, chẳng hạn như normal, tangent, màu vertex, UV1, UV2 và dữ liệu vertex tùy chỉnh.
- ``bone_aabbs``: Hộp giới hạn căn chỉnh theo trục của mỗi xương để xác định khả năng hiển thị.
- ``format``: Định dạng buffer của surface.
- ``index_count``: Số lượng index trong surface. Giá trị này phải khớp với kích thước của ``index_data``.
- ``index_data``: Dữ liệu index, xác định các vertex nào từ ``vertex_data`` sẽ được vẽ.
- ``lods``: Các biến thể level of detail, được lưu dưới dạng một mảng. Mỗi level LOD biểu diễn hai giá trị trong mảng. Giá trị đầu tiên là phần trăm không gian màn hình mà level LOD phù hợp nhất (độ dài cạnh); giá trị thứ hai là danh sách các index cần được vẽ cho level LOD tương ứng.
- ``material``: Material được sử dụng khi vẽ surface.
- ``name``: Tên của surface. Tên này có thể được sử dụng trong script và được import từ các DCC 3D.
- ``primitive``: Kiểu primitive của surface, tương ứng với enum Godot ``Mesh.PrimitiveType``. ``0`` = điểm, ``1`` = đường, ``2`` = dải đường, ``3`` = tam giác (phổ biến nhất), ``4`` = dải tam giác.
- ``skin_data``: Dữ liệu trọng số xương.
- ``vertex_count``: Số lượng vertex trong surface. Giá trị này phải khớp với kích thước của ``vertex_data``.
- ``vertex_data``: Dữ liệu vị trí vertex.

Đây là ví dụ về một ArrayMesh được lưu trong tệp ``.tres`` riêng. Một số trường được rút gọn bằng ``...`` để văn bản ngắn gọn hơn:

::

    [gd_resource type="ArrayMesh" format=3 uid="uid://dww8o7hsqrhx5"]

    [ext_resource type="Material" path="res://player/model/playerobot.tres" id="1_r3bjq"]

    [resource]
    resource_name = "player_Sphere_016"
    _surfaces = [{
    "aabb": AABB(-0.207928, 1.21409, -0.14545, 0.415856, 0.226569, 0.223374),
    "attribute_data": PackedByteArray(63, 121, ..., 117, 63),
    "bone_aabbs": [AABB(0, 0, 0, -1, -1, -1), ..., AABB(-0.207928, 1.21409, -0.14545, 0.134291, 0.226569, 0.223374)],
    "format": 7191,
    "index_count": 1224,
    "index_data": PackedByteArray(30, 0, ..., 150, 4),
    "lods": [0.0382013, PackedByteArray(33, 1, ..., 150, 4)],
    "material": ExtResource("1_r3bjq"),
    "name": "playerobot",
    "primitive": 3,
    "skin_data": PackedByteArray(15, 0, ..., 0, 0),
    "vertex_count": 1250,
    "vertex_data": PackedByteArray(196, 169, ..., 11, 38)
    }]
    blend_shape_mode = 0

.. _doc_tscn_animation:

Animation
~~~~~~~~~

Mỗi animation có các thuộc tính sau:

- ``length``: Độ dài của animation tính bằng giây. Lưu ý rằng keyframe có thể được đặt bên ngoài khoảng ``[0; length]``, nhưng có thể không có hiệu lực tùy thuộc vào chế độ nội suy được chọn.
- ``loop_mode``: ``0`` = không lặp, ``1`` = lặp vòng, ``2`` = lặp giới hạn.
- ``step``: Bước nhảy được sử dụng khi chỉnh sửa animation này trong editor. Giá trị này chỉ được sử dụng trong editor; nó không ảnh hưởng đến việc phát animation theo bất kỳ cách nào.

Mỗi track được mô tả bằng một danh sách các cặp key-value theo định dạng ``tracks/<id>/<attribute>``. Mỗi track bao gồm:

- ``type``: Kiểu của track. Kiểu này xác định những thuộc tính nào có thể được animation hóa bởi track và cách chúng được hiển thị cho người dùng trong editor. Các kiểu hợp lệ là ``value`` (track thuộc tính chung), ``position_3d``, ``rotation_3d``, ``scale_3d``, ``blend_shape`` (track animation 3D được tối ưu hóa), ``method`` (track gọi phương thức), ``bezier`` (track đường cong Bezier), ``audio`` (track phát âm thanh), ``animation`` (track phát các animation khác).
- ``imported``: ``true`` nếu track được tạo từ một scene 3D đã import, ``false`` nếu track được người dùng tạo thủ công trong Godot editor hoặc bằng script.
- ``enabled``: ``true`` nếu track đang hoạt động, ``false`` nếu track đã bị vô hiệu hóa trong editor.
- ``path``: Đường dẫn đến thuộc tính của node sẽ bị track tác động. Thuộc tính được viết sau đường dẫn node với dấu phân cách ``:``.
- ``interp``: Chế độ nội suy sẽ sử dụng. ``0`` = nearest, ``1`` = linear, ``2`` = cubic, ``3`` = linear angle, ``4`` = cubic angle.
- ``loop_wrap``: ``true`` nếu track được thiết kế để lặp vòng khi animation lặp lại, ``false`` nếu track giới hạn ở keyframe đầu tiên/cuối cùng.
- ``keys``: Các giá trị của animation track. Cấu trúc của thuộc tính này phụ thuộc vào ``type``.

Dưới đây là một scene chứa AnimationPlayer thu nhỏ một hình lập phương theo thời gian bằng generic property track. Quy trình AnimationLibrary không được sử dụng, vì vậy animation library có tên trống (nhưng animation vẫn được đặt tên ``scale_down``). Lưu ý rằng track ``RESET`` không được tạo trong AnimationPlayer này để phần minh họa ngắn gọn hơn:

::

    [gd_scene format=3 uid="uid://cdyt3nktp6y6"]

    [sub_resource type="Animation" id="Animation_r2qdp"]
    resource_name = "scale_down"
    length = 1.5
    loop_mode = 2
    step = 0.05
    tracks/0/type = "value"
    tracks/0/imported = false
    tracks/0/enabled = true
    tracks/0/path = NodePath("Box:scale")
    tracks/0/interp = 1
    tracks/0/loop_wrap = true
    tracks/0/keys = {
    "times": PackedFloat32Array(0, 1),
    "transitions": PackedFloat32Array(1, 1),
    "update": 0,
    "values": [Vector3(1, 1, 1), Vector3(0, 0, 0)]
    }

    [sub_resource type="AnimationLibrary" id="AnimationLibrary_4qx36"]
    _data = {
    "scale_down": SubResource("Animation_r2qdp")
    }

    [sub_resource type="BoxMesh" id="BoxMesh_u688r"]

    [node name="Node3D" type="Node3D" unique_id=2076735200]

    [node name="AnimationPlayer" type="AnimationPlayer" parent="." unique_id=2139773137]
    autoplay = "scale_down"
    libraries = {
    "": SubResource("AnimationLibrary_4qx36")
    }

    [node name="Box" type="MeshInstance3D" parent="." unique_id=711004519]
    mesh = SubResource("BoxMesh_u688r")

Đối với các track generic property ``value``, ``keys`` là một dictionary chứa 3 mảng với các vị trí trong ``times`` (PackedFloat32Array), các giá trị easing trong ``transitions`` (PackedFloat32Array) và các giá trị trong ``values`` (Array). Ngoài ra còn có thuộc tính ``update``, là một số nguyên với các giá trị ``0`` = continuous, ``1`` = discrete, ``2`` = capture.

Dưới đây là một Animation resource thứ hai sử dụng các track 3D Position và 3D Rotation. Các track này (cùng với track 3D Scale) thay thế các track Transform từ Godot 3. Chúng được tối ưu để phát nhanh và có thể tùy chọn nén.

Nhược điểm của các loại track được tối ưu này là chúng không thể sử dụng các giá trị easing tùy chỉnh. Thay vào đó, mọi keyframe đều sử dụng nội suy linear. Tuy vậy, bạn vẫn có thể chọn sử dụng nội suy nearest hoặc cubic cho tất cả keyframe trong một track cụ thể bằng cách thay đổi chế độ nội suy của track.

::

    [sub_resource type="Animation" id="Animation_r2qdp"]
    resource_name = "move_and_rotate"
    length = 1.5
    loop_mode = 2
    step = 0.05
    tracks/0/type = "position_3d"
    tracks/0/imported = false
    tracks/0/enabled = true
    tracks/0/path = NodePath("Box")
    tracks/0/interp = 1
    tracks/0/loop_wrap = true
    tracks/0/keys = PackedFloat32Array(0, 1, 0, 0, 0, 1.5, 1, 1.5, 1, 0)
    tracks/1/type = "rotation_3d"
    tracks/1/imported = false
    tracks/1/enabled = true
    tracks/1/path = NodePath("Box")
    tracks/1/interp = 1
    tracks/1/loop_wrap = true
    tracks/1/keys = PackedFloat32Array(0, 1, 0.211, -0.047, 0.211, 0.953, 1.5, 1, 0.005, 0.976, -0.216, 0.022)

Đối với các track 3D position, rotation và scale, ``keys`` là một PackedFloat32Array chứa tất cả giá trị theo một chuỗi.

Trong hướng dẫn trực quan bên dưới, ``T`` là thời gian của keyframe tính bằng giây kể từ khi animation bắt đầu, ``E`` là transition của keyframe (hiện luôn là ``1``). Đối với các track 3D position và scale, ``X``, ``Y``, ``Z`` là các tọa độ của Vector3. Đối với các track 3D rotation, ``X``, ``Y``, ``Z`` và ``W`` là các tọa độ của Quaternion.

::

    # For 3D position and scale, which use Vector3:
    tracks/<id>/keys = PackedFloat32Array(T, E,   X, Y, Z,      T, E,   X, Y, Z, ...)

    # For 3D rotation, which use Quaternion:
    tracks/<id>/keys = PackedFloat32Array(T, E,   X, Y, Z, W,      T, E,   X, Y, Z, W, ...)

.. _`resource_format_text.cpp`: https://github.com/godotengine/godot/blob/master/scene/resources/resource_format_text.cpp
