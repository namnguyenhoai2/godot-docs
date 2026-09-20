.. _doc_tscn_file_format:

Định dạng tệp TSCN
==================

Định dạng tệp TSCN (cảnh dạng văn bản) biểu diễn một cây cảnh duy nhất bên trong Godot. Không giống các tệp SCN nhị phân, tệp TSCN có ưu điểm là phần lớn đều dễ đọc đối với con người và dễ được các hệ thống kiểm soát phiên bản quản lý.

Định dạng tệp ESCN (cảnh đã xuất) giống hệt định dạng tệp TSCN, nhưng được dùng để cho Godot biết rằng tệp đã được xuất từ một chương trình khác và người dùng không nên chỉnh sửa tệp từ bên trong Godot. Không giống các tệp SCN và TSCN, trong quá trình nhập, các tệp ESCN được biên dịch thành các tệp SCN nhị phân được lưu bên trong thư mục ``.godot/imported/``. Điều này làm giảm kích thước dữ liệu và tăng tốc độ tải, vì các định dạng nhị phân tải nhanh hơn so với các định dạng dựa trên văn bản.

Để làm cho các tệp nhỏ gọn hơn, những thuộc tính có giá trị bằng giá trị mặc định sẽ không được lưu trong các tệp cảnh/tài nguyên. Bạn có thể ghi chúng thủ công, nhưng chúng sẽ bị loại bỏ khi lưu tệp.

Đối với những ai cần mô tả đầy đủ, việc phân tích cú pháp được xử lý trong tệp `resource_format_text.cpp <https://github.com/godotengine/godot/blob/master/scene/resources/resource_format_text.cpp>`_ thuộc lớp ``ResourceFormatLoaderText``.

.. note::

    Định dạng tệp cảnh và tài nguyên đã thay đổi đáng kể trong Godot 4, với việc giới thiệu UID dựa trên chuỗi để thay thế các ID số nguyên tăng dần.

    Dữ liệu lưới, bộ xương và hoạt ảnh cũng được lưu khác so với Godot 3. Bạn có thể đọc về một số thay đổi trong bài viết này: `Animation data rework for 4.0 <https://godotengine.org/article/animation-data-redesign-40/>`__

    Các cảnh và tài nguyên được lưu bằng Godot 4.x chứa ``format=3`` trong phần tiêu đề, trong khi Godot 3.x sử dụng ``format=2``.

Cấu trúc tệp
------------

Có năm phần chính bên trong tệp TSCN:

0. Mô tả tệp 1. Tài nguyên bên ngoài 2. Tài nguyên bên trong 3. Nút 4. Kết nối

Mô tả tệp có dạng ``[gd_scene format=3 uid="uid://cecaux1sm7mo0"]`` và phải là mục đầu tiên trong tệp. Lưu ý rằng các cảnh được lưu trước Godot 4.6 cũng sẽ có thuộc tính ``load_steps=<int>`` trong mô tả tệp. Thuộc tính này hiện đã không còn được dùng và nên được bỏ qua nếu xuất hiện.

``uid`` là một mã định danh duy nhất dựa trên chuỗi, đại diện cho cảnh. Công cụ này được engine sử dụng để theo dõi các tệp bị di chuyển, ngay cả khi trình biên tập đang đóng. Các tập lệnh cũng có thể tải tài nguyên dựa trên UID bằng tiền tố đường dẫn ``uid://`` để tránh phụ thuộc vào đường dẫn hệ thống tệp. Nhờ đó, bạn có thể di chuyển một tệp trong dự án mà vẫn tải được tệp đó trong các tập lệnh mà không cần sửa đổi tập lệnh. Godot không sử dụng các tệp bên ngoài để theo dõi ID, nghĩa là không cần một vị trí lưu trữ siêu dữ liệu tập trung trong dự án. Xem `pull request này <https://github.com/godotengine/godot/pull/50786>`__ để biết thông tin chi tiết.

Các phần này nên xuất hiện theo đúng thứ tự, nhưng có thể khó phân biệt chúng. Điểm khác biệt duy nhất giữa chúng là phần tử đầu tiên trong tiêu đề của tất cả các mục thuộc phần đó. Ví dụ: tiêu đề của tất cả tài nguyên bên ngoài phải bắt đầu bằng ``[ext_resource ...]``.

Tệp TSCN có thể chứa các chú thích một dòng bắt đầu bằng dấu chấm phẩy (``;``). Tuy nhiên, các chú thích sẽ bị loại bỏ khi lưu tệp bằng trình biên tập Godot. Khoảng trắng trong tệp TSCN không có ý nghĩa (ngoại trừ bên trong chuỗi), nhưng khoảng trắng thừa sẽ bị loại bỏ khi lưu tệp.

Các mục bên trong tệp
~~~~~~~~~~~~~~~~~~~~~

Một tiêu đề có dạng ``[<resource_type> key1=value1 key2=value2 key3=value3 ...]``, trong đó resource_type là một trong các giá trị sau:

- ``ext_resource`` - ``sub_resource`` - ``node`` - ``connection``

Bên dưới mỗi tiêu đề là không hoặc nhiều cặp ``key = value``. Các giá trị có thể là những kiểu dữ liệu phức tạp như Array, Transform, Color, v.v. Ví dụ, một Node3D có dạng:

::

    [node name="Cube" type="Node3D" unique_id=224283918]
    transform = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 1, 2, 3)

Cây cảnh
--------

Cây cảnh được tạo thành từ… các nút! Tiêu đề của mỗi nút gồm tên, nút cha, một ID duy nhất (dùng để theo dõi các nút ngay cả khi chúng được di chuyển hoặc đổi tên) và phần lớn trường hợp là một kiểu. Ví dụ: ``[node name="PlayerCamera" type="Camera" parent="Player/Head" unique_id=1697057368]``

Lưu ý rằng ``unique_id`` chỉ xuất hiện trong các cảnh được lưu bằng Godot 4.6 trở lên. Vì vậy, không đảm bảo thuộc tính này sẽ luôn có mặt.

Các từ khóa hợp lệ khác bao gồm:

 - ``instance`` - ``instance_placeholder`` - ``owner`` - ``index`` (thiết lập thứ tự xuất hiện trong cây; nếu không có, các nút kế thừa sẽ được ưu tiên hơn các nút thông thường) - ``groups`` - ``node_paths`` (liệt kê tên các thuộc tính được xuất dưới dạng kiểu Node nhưng được tham chiếu dưới dạng NodePath trong tệp)

Nút đầu tiên trong tệp, cũng là gốc của cảnh, **không được** có mục ``parent="Path/To/Node"`` trong tiêu đề. Tất cả các tệp cảnh phải có chính xác *một* gốc cảnh. Nếu không, Godot sẽ không thể nhập tệp. Đường dẫn đến nút cha của các nút khác nên là đường dẫn tuyệt đối, nhưng không được chứa tên của gốc cảnh. Nếu nút là con trực tiếp của gốc cảnh, đường dẫn phải là ``"."``. Sau đây là một ví dụ về cây cảnh (nhưng không có nội dung nút nào):

::

    [node name="Player" type="Node3D" unique_id=1155673912]                    ; The scene root
    [node name="Arm" type="Node3D" parent="." unique_id=1010797352]            ; Parented to the scene root
    [node name="Hand" type="Node3D" parent="Arm" unique_id=536436825]          ; Child of "Arm"
    [node name="Finger" type="Node3D" parent="Arm/Hand" unique_id=1732647084]  ; Child of "Hand"

.. tip::

    Để dễ nắm bắt cấu trúc tệp hơn, bạn có thể lưu một tệp có chứa bất kỳ nút hoặc tài nguyên nào, sau đó tự kiểm tra tệp bằng một trình biên tập bên ngoài. Bạn cũng có thể thực hiện các thay đổi tăng dần trong trình biên tập Godot và mở một trình biên tập văn bản bên ngoài trên tệp ``.tscn`` hoặc ``.tres`` với tính năng tự động tải lại được bật để xem các thay đổi.

Sau đây là một ví dụ về cảnh chứa một quả bóng dựa trên RigidBody3D với va chạm, phần hiển thị (lưới + ánh sáng) và một camera được gắn làm con của RigidBody3D:

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

Một cấu trúc cây là chưa đủ để biểu diễn toàn bộ cảnh. Godot sử dụng cấu trúc ``NodePath(Path/To/Node)`` để tham chiếu đến một nút hoặc thuộc tính của nút khác ở bất kỳ đâu trong cây cảnh. Các đường dẫn có liên quan đến nút hiện tại, với ``NodePath(".")`` trỏ đến nút hiện tại và ``NodePath("")`` trỏ đến không có nút nào.

Ví dụ, MeshInstance3D sử dụng ``NodePath()`` để trỏ đến bộ xương của nó. Tương tự, các track Animation sử dụng ``NodePath()`` để trỏ đến những thuộc tính của nút cần tạo hoạt ảnh.

NodePath cũng có thể trỏ đến một thuộc tính bằng hậu tố ``:property_name``, thậm chí trỏ đến một thành phần cụ thể đối với các kiểu vector, transform và color. Tài nguyên Animation sử dụng tính năng này để trỏ đến các thuộc tính cụ thể cần tạo hoạt ảnh. Ví dụ, ``NodePath("MeshInstance3D:scale.x")`` trỏ đến thành phần ``x`` của thuộc tính Vector3 ``scale`` trong MeshInstance3D.

Ví dụ, thuộc tính ``skeleton`` trong nút MeshInstance3D có tên ``mesh`` trỏ đến nút cha của nó, ``Armature01``:

::

    [node name="mesh" type="MeshInstance3D" parent="Armature01" unique_id=1638249225]
    skeleton = NodePath("..")

Skeleton3D
~~~~~~~~~~

Nút :ref:`class_Skeleton3D` kế thừa nút Node3D, nhưng cũng có thể chứa một danh sách xương được mô tả bằng các cặp khóa-giá trị theo định dạng ``bones/<id>/<attribute> = value``. Các thuộc tính của xương gồm:

- ``position``: Vector3 - ``rotation``: Quaternion - ``scale``: Vector3

Tất cả các thuộc tính này đều là tùy chọn. Ví dụ, một xương có thể chỉ định ``position`` hoặc ``rotation`` mà không cần chỉ định các thuộc tính còn lại.

Sau đây là một ví dụ về một nút skeleton có hai xương:

::

    [node name="Skeleton3D" type="Skeleton3D" parent="PlayerModel/Robot_Skeleton" index="0" unique_id=542985694]
    bones/1/position = Vector3(0.114471, 2.19771, -0.197845)
    bones/1/rotation = Quaternion(0.191422, -0.0471201, -0.00831942, 0.980341)
    bones/2/position = Vector3(-2.59096e-05, 0.236002, 0.000347473)
    bones/2/rotation = Quaternion(-0.0580488, 0.0310587, -0.0085914, 0.997794)
    bones/2/scale = Vector3(0.9276, 0.9276, 0.9276)

BoneAttachment3D
~~~~~~~~~~~~~~~~

Nút :ref:`class_BoneAttachment3D` là một nút trung gian dùng để mô tả một nút được gắn làm con của một xương duy nhất trong một nút Skeleton. BoneAttachment có thuộc tính ``bone_name = "name of bone"``, cũng như một thuộc tính chỉ số xương tương ứng.

Ví dụ về một nút :ref:`class_Marker3D` được gắn làm con của một xương trong Skeleton:

::

    [node name="GunBone" type="BoneAttachment3D" parent="PlayerModel/Robot_Skeleton/Skeleton3D" index="5" unique_id=63481392]
    transform = Transform3D(0.333531, 0.128981, -0.933896, 0.567174, 0.763886, 0.308015, 0.753209, -0.632331, 0.181604, -0.323915, 1.07098, 0.0497144)
    bone_name = "hand.R"
    bone_idx = 55

    [node name="ShootFrom" type="Marker3D" parent="PlayerModel/Robot_Skeleton/Skeleton3D/GunBone" unique_id=679926736]
    transform = Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0.4, 0)

AnimationPlayer
~~~~~~~~~~~~~~~

Nút :ref:`class_AnimationPlayer` hoạt động với một hoặc nhiều thư viện animation được lưu trong các tài nguyên :ref:`class_AnimationLibrary`. Một thư viện animation là tập hợp các tài nguyên :ref:`class_Animation` riêng lẻ, với cấu trúc được dokument tại :ref:`here <doc_tscn_animation>`.

Việc tách riêng các animation và thư viện animation được thực hiện trong Godot 4, để có thể nhập animation riêng biệt với các lưới 3D, một quy trình phổ biến trong phần mềm animation 3D. Xem `pull request ban đầu <https://github.com/godotengine/godot/pull/59980>`__ để biết chi tiết.

Nếu tên thư viện trống, thư viện đó sẽ hoạt động như nguồn animation duy nhất cho AnimationPlayer này. Nhờ đó, bạn có thể sử dụng ``<animation_name>`` trực tiếp để phát animation từ script. Nếu đặt tên cho thư viện, bạn phải phát nó dưới dạng ``<library_name>/<animation_name>``. Điều này đảm bảo khả năng tương thích ngược và duy trì quy trình hiện có nếu bạn không muốn sử dụng nhiều thư viện animation.

Tài nguyên
----------

Tài nguyên là các thành phần tạo nên các nút. Ví dụ, một nút MeshInstance3D sẽ có một tài nguyên ArrayMesh đi kèm. Tài nguyên ArrayMesh có thể nằm bên trong hoặc bên ngoài tệp TSCN.

Các tham chiếu đến tài nguyên được xử lý bằng các ID duy nhất dựa trên chuỗi trong tiêu đề của tài nguyên. Điều này khác với thuộc tính ``uid``, thuộc tính mà mỗi tài nguyên bên ngoài cũng có (nhưng các tài nguyên phụ thì không).

Các tài nguyên bên ngoài và tài nguyên bên trong lần lượt được tham chiếu bằng ``ExtResource("id")`` và ``SubResource("id")``. Vì có các phương thức khác nhau để tham chiếu đến tài nguyên bên trong và bên ngoài, bạn có thể sử dụng cùng một ID cho cả một tài nguyên bên trong lẫn một tài nguyên bên ngoài.

Ví dụ, để tham chiếu đến tài nguyên ``[ext_resource type="Material" uid="uid://c4cp0al3ljsjv" path="res://material.tres" id="1_7bt6s"]``, bạn sẽ sử dụng ``ExtResource("1_7bt6s")``.

Tài nguyên bên ngoài
~~~~~~~~~~~~~~~~~~~~

Tài nguyên bên ngoài là các liên kết đến những tài nguyên không nằm trong chính tệp TSCN. Một tài nguyên bên ngoài gồm có một đường dẫn, một kiểu, một UID (dùng để ánh xạ vị trí của tài nguyên trong hệ thống tệp với một mã định danh duy nhất) và một ID (dùng để tham chiếu đến tài nguyên trong tệp cảnh).

Godot luôn tạo các đường dẫn tuyệt đối tương đối với thư mục tài nguyên và do đó được thêm tiền tố ``res://``, nhưng các đường dẫn tương đối với vị trí của tệp TSCN cũng hợp lệ.

Một số tài nguyên bên ngoài mẫu gồm:

::

    [ext_resource type="Texture2D" uid="uid://ccbm14ebjmpy1" path="res://gradient.tres" id="2_eorut"]
    [ext_resource type="Material" uid="uid://c4cp0al3ljsjv" path="material.tres" id="1_7bt6s"]

Giống như các tệp TSCN, tệp TRES có thể chứa các chú thích một dòng bắt đầu bằng dấu chấm phẩy (``;``). Tuy nhiên, các chú thích sẽ bị loại bỏ khi lưu tài nguyên bằng trình chỉnh sửa Godot. Khoảng trắng trong tệp TRES không có ý nghĩa (ngoại trừ trong chuỗi), nhưng khoảng trắng thừa sẽ bị loại bỏ khi lưu tệp.

Tài nguyên nội bộ
~~~~~~~~~~~~~~~~~

Một tệp TSCN có thể chứa lưới, vật liệu và dữ liệu khác. Các dữ liệu này nằm trong phần *tài nguyên nội bộ* của tệp. Tiêu đề của một tài nguyên nội bộ trông tương tự tiêu đề của tài nguyên bên ngoài, ngoại trừ việc không có đường dẫn. Tài nguyên nội bộ cũng có các cặp ``key=value`` bên dưới mỗi tiêu đề. Ví dụ, một hình dạng va chạm viên nang có dạng:

::

    [sub_resource type="CapsuleShape3D" id="CapsuleShape3D_fdxgg"]
    radius = 1.0
    height = 3.0

Một số tài nguyên nội bộ chứa liên kết đến các tài nguyên nội bộ khác (chẳng hạn như một lưới có vật liệu). Trong trường hợp này, tài nguyên tham chiếu phải xuất hiện *trước* phần tham chiếu đến nó. Điều này có nghĩa là thứ tự trong phần tài nguyên nội bộ của tệp rất quan trọng.

ArrayMesh
~~~~~~~~~

Một ArrayMesh bao gồm nhiều bề mặt nằm trong mảng ``_surfaces`` (hãy chú ý dấu gạch dưới ở đầu). Dữ liệu của mỗi bề mặt được lưu trong một từ điển với các khóa sau:

- ``aabb``: Hộp giới hạn thẳng hàng với trục được tính toán để phục vụ khả năng hiển thị. - ``attribute_data``: Dữ liệu thuộc tính đỉnh, chẳng hạn như pháp tuyến, tiếp tuyến, màu đỉnh, UV1, UV2 và dữ liệu đỉnh tùy chỉnh. - ``bone_aabbs``: Hộp giới hạn thẳng hàng với trục của mỗi xương để phục vụ khả năng hiển thị. - ``format``: Định dạng bộ đệm của bề mặt. - ``index_count``: Số lượng chỉ mục trong bề mặt. Giá trị này phải khớp với kích thước của ``index_data``. - ``index_data``: Dữ liệu chỉ mục, xác định các đỉnh từ ``vertex_data`` sẽ được vẽ. - ``lods``: Các biến thể mức độ chi tiết, được lưu dưới dạng một mảng. Mỗi cấp độ LOD biểu diễn hai giá trị trong mảng. Giá trị đầu tiên là tỷ lệ phần trăm không gian màn hình mà cấp độ LOD phù hợp nhất (độ dài cạnh); giá trị thứ hai là danh sách các chỉ mục cần được vẽ cho cấp độ LOD tương ứng. - ``material``: Vật liệu được sử dụng khi vẽ bề mặt. - ``name``: Tên của bề mặt. Tên này có thể được sử dụng trong các tập lệnh và được nhập từ các DCC 3D. - ``primitive``: Kiểu nguyên thủy của bề mặt, tương ứng với enum Godot ``Mesh.PrimitiveType``. ``0`` = điểm, ``1`` = đường, ``2`` = dải đường, ``3`` = hình tam giác (phổ biến nhất), ``4`` = dải hình tam giác. - ``skin_data``: Dữ liệu trọng số xương. - ``vertex_count``: Số lượng đỉnh trong bề mặt. Giá trị này phải khớp với kích thước của ``vertex_data``. - ``vertex_data``: Dữ liệu vị trí đỉnh.

Sau đây là một ví dụ về ArrayMesh được lưu vào tệp ``.tres`` riêng. Một số trường đã được rút gọn bằng ``...`` để ngắn gọn:

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

Hoạt ảnh
~~~~~~~~

Mỗi hoạt ảnh có các thuộc tính sau:

- ``length``: Độ dài của hoạt ảnh tính bằng giây. Lưu ý rằng các khung hình chính có thể được đặt bên ngoài khoảng ``[0; length]``, nhưng chúng có thể không có tác dụng tùy thuộc vào chế độ nội suy được chọn. - ``loop_mode``: ``0`` = không lặp, ``1`` = lặp vòng, ``2`` = lặp giới hạn. - ``step``: Kích thước bước được sử dụng khi chỉnh sửa hoạt ảnh này trong trình chỉnh sửa. Giá trị này chỉ được sử dụng trong trình chỉnh sửa; nó không ảnh hưởng đến việc phát lại hoạt ảnh theo bất kỳ cách nào.

Mỗi track được mô tả bằng một danh sách các cặp khóa-giá trị theo định dạng ``tracks/<id>/<attribute>``. Mỗi track bao gồm:

- ``type``: Kiểu của track. Kiểu này xác định loại thuộc tính nào có thể được tạo hoạt ảnh bằng track và cách chúng được hiển thị cho người dùng trong trình chỉnh sửa. Các kiểu hợp lệ là ``value`` (track thuộc tính chung), ``position_3d``, ``rotation_3d``, ``scale_3d``, ``blend_shape`` (các track hoạt ảnh 3D được tối ưu hóa), ``method`` (các track gọi phương thức), ``bezier`` (các track đường cong Bezier), ``audio`` (các track phát âm thanh), ``animation`` (các track phát các hoạt ảnh khác). - ``imported``: ``true`` nếu track được tạo từ một cảnh 3D đã nhập, ``false`` nếu track được người dùng tạo thủ công trong trình chỉnh sửa Godot hoặc bằng một tập lệnh. - ``enabled``: ``true`` nếu track đang hoạt động, ``false`` nếu track đã bị vô hiệu hóa trong trình chỉnh sửa. - ``path``: Đường dẫn đến thuộc tính nút sẽ bị track tác động. Thuộc tính được viết sau đường dẫn nút, ngăn cách bằng ``:``. - ``interp``: Chế độ nội suy được sử dụng. ``0`` = gần nhất, ``1`` = tuyến tính, ``2`` = cubic, ``3`` = góc tuyến tính, ``4`` = góc cubic. - ``loop_wrap``: ``true`` nếu track được thiết kế để lặp vòng khi hoạt ảnh lặp, ``false`` nếu track giới hạn ở khung hình chính đầu tiên/cuối cùng. - ``keys``: Các giá trị của track hoạt ảnh. Cấu trúc của thuộc tính này phụ thuộc vào ``type``.

Đây là một cảnh chứa một AnimationPlayer thu nhỏ một khối lập phương theo thời gian bằng một track thuộc tính chung. Quy trình AnimationLibrary không được sử dụng, vì vậy thư viện hoạt ảnh có tên rỗng (nhưng hoạt ảnh vẫn được đặt một tên ``scale_down``). Lưu ý rằng track ``RESET`` không được tạo trong AnimationPlayer này để nội dung ngắn gọn hơn:

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

Đối với các track ``value`` thuộc tính chung, ``keys`` là một từ điển chứa 3 mảng với các vị trí trong ``times`` (PackedFloat32Array), các giá trị easing trong ``transitions`` (PackedFloat32Array) và các giá trị trong ``values`` (Array). Ngoài ra còn có thuộc tính ``update``, là một số nguyên với các giá trị ``0`` = liên tục, ``1`` = rời rạc, ``2`` = thu nhận.

Đây là một tài nguyên Animation thứ hai sử dụng các track 3D Position và 3D Rotation. Các track này (ngoài track 3D Scale) thay thế các track Transform từ Godot 3. Chúng được tối ưu hóa để phát lại nhanh và có thể tùy chọn được nén.

Nhược điểm của các kiểu track được tối ưu hóa này là chúng không thể sử dụng các giá trị easing tùy chỉnh. Thay vào đó, tất cả các khung hình chính đều sử dụng nội suy tuyến tính. Tuy vậy, bạn vẫn có thể chọn sử dụng nội suy gần nhất hoặc cubic cho tất cả các khung hình chính trong một track nhất định bằng cách thay đổi chế độ nội suy của track.

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

Đối với các track vị trí, xoay và tỷ lệ 3D, ``keys`` là một PackedFloat32Array chứa tất cả các giá trị được lưu theo một chuỗi.

Trong hướng dẫn trực quan bên dưới, ``T`` là thời điểm của khung hình chính tính bằng giây kể từ khi hoạt ảnh bắt đầu, ``E`` là chuyển tiếp của khung hình chính (hiện luôn là ``1``). Đối với các track vị trí và tỷ lệ 3D, ``X``, ``Y``, ``Z`` là các tọa độ của Vector3. Đối với các track xoay 3D, ``X``, ``Y``, ``Z`` và ``W`` là các tọa độ của Quaternion.

::

    # For 3D position and scale, which use Vector3:
    tracks/<id>/keys = PackedFloat32Array(T, E,   X, Y, Z,      T, E,   X, Y, Z, ...)

    # For 3D rotation, which use Quaternion:
    tracks/<id>/keys = PackedFloat32Array(T, E,   X, Y, Z, W,      T, E,   X, Y, Z, W, ...)
