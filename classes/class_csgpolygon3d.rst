:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGPolygon3D.xml.

.. _class_CSGPolygon3D:

CSGPolygon3D
============

**Kế thừa:** :ref:`CSGPrimitive3D<class_CSGPrimitive3D>` **<** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đùn một hình đa giác 2D để tạo mesh 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng các điểm 2D được đùn để nhanh chóng và dễ dàng tạo ra nhiều loại mesh 3D. Xem thêm :ref:`CSGMesh3D<class_CSGMesh3D>` để sử dụng mesh 3D làm các node CSG.

\ **Lưu ý:** Các node CSG được thiết kế để dùng cho việc tạo nguyên mẫu level. Việc tạo node CSG có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` với một :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một node CSG bên trong một node CSG khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong gameplay.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Prototyping levels with CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`float<class_float>`                                   | :ref:`depth<class_CSGPolygon3D_property_depth>`                                   | ``1.0``                                        |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`Material<class_Material>`                             | :ref:`material<class_CSGPolygon3D_property_material>`                             |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`Mode<enum_CSGPolygon3D_Mode>`                         | :ref:`mode<class_CSGPolygon3D_property_mode>`                                     | ``0``                                          |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`path_continuous_u<class_CSGPolygon3D_property_path_continuous_u>`           |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`float<class_float>`                                   | :ref:`path_interval<class_CSGPolygon3D_property_path_interval>`                   |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>` | :ref:`path_interval_type<class_CSGPolygon3D_property_path_interval_type>`         |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`path_joined<class_CSGPolygon3D_property_path_joined>`                       |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`path_local<class_CSGPolygon3D_property_path_local>`                         |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                             | :ref:`path_node<class_CSGPolygon3D_property_path_node>`                           |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`PathRotation<enum_CSGPolygon3D_PathRotation>`         | :ref:`path_rotation<class_CSGPolygon3D_property_path_rotation>`                   |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`path_rotation_accurate<class_CSGPolygon3D_property_path_rotation_accurate>` |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`float<class_float>`                                   | :ref:`path_simplify_angle<class_CSGPolygon3D_property_path_simplify_angle>`       |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`float<class_float>`                                   | :ref:`path_u_distance<class_CSGPolygon3D_property_path_u_distance>`               |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`         | :ref:`polygon<class_CSGPolygon3D_property_polygon>`                               | ``PackedVector2Array(0, 0, 0, 1, 1, 1, 1, 0)`` |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`smooth_faces<class_CSGPolygon3D_property_smooth_faces>`                     | ``false``                                      |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`float<class_float>`                                   | :ref:`spin_degrees<class_CSGPolygon3D_property_spin_degrees>`                     |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+
   | :ref:`int<class_int>`                                       | :ref:`spin_sides<class_CSGPolygon3D_property_spin_sides>`                         |                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------------------+------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CSGPolygon3D_Mode:

.. rst-class:: classref-enumeration

enum **Mode**: :ref:`🔗<enum_CSGPolygon3D_Mode>`

.. _class_CSGPolygon3D_constant_MODE_DEPTH:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_CSGPolygon3D_Mode>` **MODE_DEPTH** = ``0``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` được đùn dọc theo trục Z âm.

.. _class_CSGPolygon3D_constant_MODE_SPIN:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_CSGPolygon3D_Mode>` **MODE_SPIN** = ``1``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` được đùn bằng cách xoay quanh trục Y.

.. _class_CSGPolygon3D_constant_MODE_PATH:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_CSGPolygon3D_Mode>` **MODE_PATH** = ``2``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` được đùn dọc theo :ref:`Path3D<class_Path3D>` được chỉ định trong :ref:`path_node<class_CSGPolygon3D_property_path_node>`.

.. rst-class:: classref-item-separator

----

.. _enum_CSGPolygon3D_PathRotation:

.. rst-class:: classref-enumeration

enum **PathRotation**: :ref:`🔗<enum_CSGPolygon3D_PathRotation>`

.. _class_CSGPolygon3D_constant_PATH_ROTATION_POLYGON:

.. rst-class:: classref-enumeration-constant

:ref:`PathRotation<enum_CSGPolygon3D_PathRotation>` **PATH_ROTATION_POLYGON** = ``0``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` không được xoay.

\ **Lưu ý:** Tọa độ Z của path phải liên tục giảm để đảm bảo tạo được các hình hợp lệ.

.. _class_CSGPolygon3D_constant_PATH_ROTATION_PATH:

.. rst-class:: classref-enumeration-constant

:ref:`PathRotation<enum_CSGPolygon3D_PathRotation>` **PATH_ROTATION_PATH** = ``1``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` được xoay dọc theo path, nhưng không được xoay quanh trục của path.

\ **Lưu ý:** Tọa độ Z của path phải liên tục giảm để đảm bảo tạo được các hình hợp lệ.

.. _class_CSGPolygon3D_constant_PATH_ROTATION_PATH_FOLLOW:

.. rst-class:: classref-enumeration-constant

:ref:`PathRotation<enum_CSGPolygon3D_PathRotation>` **PATH_ROTATION_PATH_FOLLOW** = ``2``

Hình :ref:`polygon<class_CSGPolygon3D_property_polygon>` đi theo path và các phép xoay của nó quanh trục path.

.. rst-class:: classref-item-separator

----

.. _enum_CSGPolygon3D_PathIntervalType:

.. rst-class:: classref-enumeration

enum **PathIntervalType**: :ref:`🔗<enum_CSGPolygon3D_PathIntervalType>`

.. _class_CSGPolygon3D_constant_PATH_INTERVAL_DISTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>` **PATH_INTERVAL_DISTANCE** = ``0``

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` được đặt thành :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, :ref:`path_interval<class_CSGPolygon3D_property_path_interval>` sẽ xác định khoảng cách, tính bằng mét, mà mỗi khoảng của path sẽ được đùn.

.. _class_CSGPolygon3D_constant_PATH_INTERVAL_SUBDIVIDE:

.. rst-class:: classref-enumeration-constant

:ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>` **PATH_INTERVAL_SUBDIVIDE** = ``1``

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` được đặt thành :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, :ref:`path_interval<class_CSGPolygon3D_property_path_interval>` sẽ chia nhỏ các polygon dọc theo path.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGPolygon3D_property_depth:

.. rst-class:: classref-property

:ref:`float<class_float>` **depth** = ``1.0`` :ref:`🔗<class_CSGPolygon3D_property_depth>`

.. rst-class:: classref-property-setget

- |void| **set_depth**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_depth**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_DEPTH<class_CSGPolygon3D_constant_MODE_DEPTH>`, độ sâu của phần đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_CSGPolygon3D_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

Material được sử dụng cho mesh kết quả. UV sẽ ánh xạ nửa trên của material vào hình được đùn (U dọc theo chiều dài của các phần đùn và V quanh đường viền của :ref:`polygon<class_CSGPolygon3D_property_polygon>`), một phần tư dưới bên trái vào mặt đầu phía trước và một phần tư dưới bên phải vào mặt đầu phía sau.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_mode:

.. rst-class:: classref-property

:ref:`Mode<enum_CSGPolygon3D_Mode>` **mode** = ``0`` :ref:`🔗<class_CSGPolygon3D_property_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mode**\ (\ value\: :ref:`Mode<enum_CSGPolygon3D_Mode>`\ ) - :ref:`Mode<enum_CSGPolygon3D_Mode>` **get_mode**\ (\ )

:ref:`mode<class_CSGPolygon3D_property_mode>` được sử dụng để đùn :ref:`polygon<class_CSGPolygon3D_property_polygon>`.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_continuous_u:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **path_continuous_u** :ref:`🔗<class_CSGPolygon3D_property_path_continuous_u>`

.. rst-class:: classref-property-setget

- |void| **set_path_continuous_u**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_path_continuous_u**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, theo mặc định, nửa trên của :ref:`material<class_CSGPolygon3D_property_material>` được kéo giãn dọc theo toàn bộ chiều dài của hình được đùn. Nếu ``false`` thì nửa trên của material được lặp lại ở mỗi bước đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_interval:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_interval** :ref:`🔗<class_CSGPolygon3D_property_path_interval>`

.. rst-class:: classref-property-setget

- |void| **set_path_interval**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_interval**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, khoảng path hoặc tỷ lệ giữa các điểm path và các phần đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_interval_type:

.. rst-class:: classref-property

:ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>` **path_interval_type** :ref:`🔗<class_CSGPolygon3D_property_path_interval_type>`

.. rst-class:: classref-property-setget

- |void| **set_path_interval_type**\ (\ value\: :ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>`\ ) - :ref:`PathIntervalType<enum_CSGPolygon3D_PathIntervalType>` **get_path_interval_type**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, thuộc tính này sẽ xác định khoảng được tính theo khoảng cách (:ref:`PATH_INTERVAL_DISTANCE<class_CSGPolygon3D_constant_PATH_INTERVAL_DISTANCE>`) hay theo phân số chia nhỏ (:ref:`PATH_INTERVAL_SUBDIVIDE<class_CSGPolygon3D_constant_PATH_INTERVAL_SUBDIVIDE>`).

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_joined:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **path_joined** :ref:`🔗<class_CSGPolygon3D_property_path_joined>`

.. rst-class:: classref-property-setget

- |void| **set_path_joined**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_path_joined**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, nếu ``true`` thì các đầu của path được nối lại bằng cách thêm một phần đùn giữa điểm cuối và điểm đầu của path.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_local:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **path_local** :ref:`🔗<class_CSGPolygon3D_property_path_local>`

.. rst-class:: classref-property-setget

- |void| **set_path_local**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_path_local**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, nếu ``true`` thì :ref:`Transform3D<class_Transform3D>` của **CSGPolygon3D** được dùng làm điểm bắt đầu cho các phần đùn, thay vì :ref:`Transform3D<class_Transform3D>` của :ref:`path_node<class_CSGPolygon3D_property_path_node>`.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_node:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **path_node** :ref:`🔗<class_CSGPolygon3D_property_path_node>`

.. rst-class:: classref-property-setget

- |void| **set_path_node**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_path_node**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, vị trí của đối tượng :ref:`Path3D<class_Path3D>` được dùng để đùn :ref:`polygon<class_CSGPolygon3D_property_polygon>`.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_rotation:

.. rst-class:: classref-property

:ref:`PathRotation<enum_CSGPolygon3D_PathRotation>` **path_rotation** :ref:`🔗<class_CSGPolygon3D_property_path_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_path_rotation**\ (\ value\: :ref:`PathRotation<enum_CSGPolygon3D_PathRotation>`\ ) - :ref:`PathRotation<enum_CSGPolygon3D_PathRotation>` **get_path_rotation**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, phương thức xoay path được dùng để xoay :ref:`polygon<class_CSGPolygon3D_property_polygon>` khi nó được đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_rotation_accurate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **path_rotation_accurate** :ref:`🔗<class_CSGPolygon3D_property_path_rotation_accurate>`

.. rst-class:: classref-property-setget

- |void| **set_path_rotation_accurate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_path_rotation_accurate**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, nếu ``true`` thì polygon sẽ được xoay theo tiếp tuyến chính xác của path tại các điểm được lấy mẫu. Nếu ``false`` thì một phép xấp xỉ được sử dụng; độ chính xác của phép xấp xỉ giảm khi số lần chia nhỏ giảm.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_simplify_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_simplify_angle** :ref:`🔗<class_CSGPolygon3D_property_path_simplify_angle>`

.. rst-class:: classref-property-setget

- |void| **set_path_simplify_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_simplify_angle**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, các phần đùn nhỏ hơn góc này sẽ được gộp lại để giảm số lượng polygon.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_path_u_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_u_distance** :ref:`🔗<class_CSGPolygon3D_property_path_u_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_u_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_u_distance**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_PATH<class_CSGPolygon3D_constant_MODE_PATH>`, đây là khoảng cách dọc theo path, tính bằng mét, mà các tọa độ texture sẽ lặp lại. Khi được đặt thành 0, các tọa độ texture sẽ khớp chính xác với hình học và không lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_polygon:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **polygon** = ``PackedVector2Array(0, 0, 0, 1, 1, 1, 1, 0)`` :ref:`🔗<class_CSGPolygon3D_property_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_polygon**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_polygon**\ (\ )

Mảng điểm xác định polygon 2D được đùn. Đây có thể là polygon lồi hoặc lõm với 3 điểm trở lên. Polygon không được có bất kỳ cạnh nào giao nhau. Nếu không, quá trình triangulation sẽ thất bại và không có mesh nào được tạo.

\ **Lưu ý:** Nếu chỉ có 1 hoặc 2 điểm được xác định trong :ref:`polygon<class_CSGPolygon3D_property_polygon>`, sẽ không có mesh nào được tạo.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_smooth_faces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **smooth_faces** = ``false`` :ref:`🔗<class_CSGPolygon3D_property_smooth_faces>`

.. rst-class:: classref-property-setget

- |void| **set_smooth_faces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_smooth_faces**\ (\ )

Nếu ``true``, áp dụng smooth shading cho các phần đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_spin_degrees:

.. rst-class:: classref-property

:ref:`float<class_float>` **spin_degrees** :ref:`🔗<class_CSGPolygon3D_property_spin_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_spin_degrees**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_spin_degrees**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_SPIN<class_CSGPolygon3D_constant_MODE_SPIN>`, tổng số độ mà :ref:`polygon<class_CSGPolygon3D_property_polygon>` được xoay khi đùn.

.. rst-class:: classref-item-separator

----

.. _class_CSGPolygon3D_property_spin_sides:

.. rst-class:: classref-property

:ref:`int<class_int>` **spin_sides** :ref:`🔗<class_CSGPolygon3D_property_spin_sides>`

.. rst-class:: classref-property-setget

- |void| **set_spin_sides**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spin_sides**\ (\ )

Khi :ref:`mode<class_CSGPolygon3D_property_mode>` là :ref:`MODE_SPIN<class_CSGPolygon3D_constant_MODE_SPIN>`, số lượng phần đùn được thực hiện.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
