:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/IterateIK3D.xml.

.. _class_IterateIK3D:

IterateIK3D
===========

**Kế thừa:** :ref:`ChainIK3D<class_ChainIK3D>` **<** :ref:`IKModifier3D<class_IKModifier3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CCDIK3D<class_CCDIK3D>`, :ref:`FABRIK3D<class_FABRIK3D>`, :ref:`JacobianIK3D<class_JacobianIK3D>`

Một :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` để tiến đến mục tiêu bằng cách lặp lại các phép xoay nhỏ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở của :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` để tiến đến mục tiêu bằng cách lặp lại các phép xoay nhỏ.

Mỗi chuỗi bone (thiết lập) có một effector, được xử lý theo thứ tự trong danh sách thiết lập. Bạn có thể đặt một số giới hạn cho từng joint.

\ **Lưu ý:** Tất cả các phương thức trong lớp này đều nhận tham số ``index``. Tham số này chỉ định mục trong danh sách thiết lập cần trả về nếu IK có nhiều mục (ví dụ: ``settings/<index>/target_node``).

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------+-----------------+
   | :ref:`float<class_float>` | :ref:`angular_delta_limit<class_IterateIK3D_property_angular_delta_limit>` | ``0.034906585`` |
   +---------------------------+----------------------------------------------------------------------------+-----------------+
   | :ref:`bool<class_bool>`   | :ref:`deterministic<class_IterateIK3D_property_deterministic>`             | ``false``       |
   +---------------------------+----------------------------------------------------------------------------+-----------------+
   | :ref:`int<class_int>`     | :ref:`max_iterations<class_IterateIK3D_property_max_iterations>`           | ``4``           |
   +---------------------------+----------------------------------------------------------------------------+-----------------+
   | :ref:`float<class_float>` | :ref:`min_distance<class_IterateIK3D_property_min_distance>`               | ``0.001``       |
   +---------------------------+----------------------------------------------------------------------------+-----------------+
   | :ref:`int<class_int>`     | :ref:`setting_count<class_IterateIK3D_property_setting_count>`             | ``0``           |
   +---------------------------+----------------------------------------------------------------------------+-----------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JointLimitation3D<class_JointLimitation3D>`                     | :ref:`get_joint_limitation<class_IterateIK3D_method_get_joint_limitation>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SecondaryDirection<enum_SkeletonModifier3D_SecondaryDirection>` | :ref:`get_joint_limitation_right_axis<class_IterateIK3D_method_get_joint_limitation_right_axis>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                         | :ref:`get_joint_limitation_right_axis_vector<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                              |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`                                   | :ref:`get_joint_limitation_rotation_offset<class_IterateIK3D_method_get_joint_limitation_rotation_offset>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RotationAxis<enum_SkeletonModifier3D_RotationAxis>`             | :ref:`get_joint_rotation_axis<class_IterateIK3D_method_get_joint_rotation_axis>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                                                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                         | :ref:`get_joint_rotation_axis_vector<class_IterateIK3D_method_get_joint_rotation_axis_vector>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const|                                                                              |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                       | :ref:`get_target_node<class_IterateIK3D_method_get_target_node>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_limitation<class_IterateIK3D_method_set_joint_limitation>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, limitation\: :ref:`JointLimitation3D<class_JointLimitation3D>`\ )                                          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_limitation_right_axis<class_IterateIK3D_method_set_joint_limitation_right_axis>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, direction\: :ref:`SecondaryDirection<enum_SkeletonModifier3D_SecondaryDirection>`\ ) |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_limitation_right_axis_vector<class_IterateIK3D_method_set_joint_limitation_right_axis_vector>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, vector\: :ref:`Vector3<class_Vector3>`\ )                              |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_limitation_rotation_offset<class_IterateIK3D_method_set_joint_limitation_rotation_offset>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, offset\: :ref:`Quaternion<class_Quaternion>`\ )                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_rotation_axis<class_IterateIK3D_method_set_joint_rotation_axis>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, axis\: :ref:`RotationAxis<enum_SkeletonModifier3D_RotationAxis>`\ )                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_joint_rotation_axis_vector<class_IterateIK3D_method_set_joint_rotation_axis_vector>`\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, axis_vector\: :ref:`Vector3<class_Vector3>`\ )                                         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_target_node<class_IterateIK3D_method_set_target_node>`\ (\ index\: :ref:`int<class_int>`, target_node\: :ref:`NodePath<class_NodePath>`\ )                                                                                                    |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_IterateIK3D_property_angular_delta_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_delta_limit** = ``0.034906585`` :ref:`🔗<class_IterateIK3D_property_angular_delta_limit>`

.. rst-class:: classref-property-setget

- |void| **set_angular_delta_limit**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_delta_limit**\ (\ )

Giới hạn lượng xoay tối đa mà mỗi bone có thể thực hiện trong một lần lặp.

\ **Lưu ý:** Giới hạn này được áp dụng trong mỗi lần lặp. Ví dụ, nếu :ref:`max_iterations<class_IterateIK3D_property_max_iterations>` là ``4`` và :ref:`angular_delta_limit<class_IterateIK3D_property_angular_delta_limit>` là ``5`` độ, thì phép xoay tối đa có thể thực hiện trong một frame là ``20`` độ.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_property_deterministic:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **deterministic** = ``false`` :ref:`🔗<class_IterateIK3D_property_deterministic>`

.. rst-class:: classref-property-setget

- |void| **set_deterministic**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_deterministic**\ (\ )

Nếu ``false``, kết quả được tính từ kết quả **IterateIK3D** của frame trước làm trạng thái ban đầu.

Nếu ``true``, kết quả **IterateIK3D** của frame trước sẽ bị loại bỏ. Khi đó, kết quả mới được tính từ tư thế bone, không bao gồm **IterateIK3D**, làm trạng thái ban đầu. Điều này có nghĩa là kết quả sẽ luôn giống nhau miễn là vị trí mục tiêu và tư thế bone trước đó giống nhau. Tuy nhiên, nếu :ref:`angular_delta_limit<class_IterateIK3D_property_angular_delta_limit>` và :ref:`max_iterations<class_IterateIK3D_property_max_iterations>` được đặt quá nhỏ, bone cuối của chuỗi sẽ không bao giờ đạt đến mục tiêu.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_property_max_iterations:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_iterations** = ``4`` :ref:`🔗<class_IterateIK3D_property_max_iterations>`

.. rst-class:: classref-property-setget

- |void| **set_max_iterations**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_iterations**\ (\ )

Số vòng lặp được bộ giải IK sử dụng để tạo ra kết quả chính xác hơn.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_property_min_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **min_distance** = ``0.001`` :ref:`🔗<class_IterateIK3D_property_min_distance>`

.. rst-class:: classref-property-setget

- |void| **set_min_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_min_distance**\ (\ )

Khoảng cách tối thiểu giữa bone cuối và mục tiêu. Nếu khoảng cách nhỏ hơn giá trị này, bộ giải IK sẽ dừng mọi lần lặp tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_property_setting_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **setting_count** = ``0`` :ref:`🔗<class_IterateIK3D_property_setting_count>`

.. rst-class:: classref-property-setget

- |void| **set_setting_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_setting_count**\ (\ )

Số lượng thiết lập.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_IterateIK3D_method_get_joint_limitation:

.. rst-class:: classref-method

:ref:`JointLimitation3D<class_JointLimitation3D>` **get_joint_limitation**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_limitation>`

Trả về giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_joint_limitation_right_axis:

.. rst-class:: classref-method

:ref:`SecondaryDirection<enum_SkeletonModifier3D_SecondaryDirection>` **get_joint_limitation_right_axis**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_limitation_right_axis>`

Trả về trục phải của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_joint_limitation_right_axis_vector:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_joint_limitation_right_axis_vector**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>`

Trả về vector trục phải của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

Nếu :ref:`get_joint_limitation_right_axis()<class_IterateIK3D_method_get_joint_limitation_right_axis>` là :ref:`SkeletonModifier3D.SECONDARY_DIRECTION_NONE<class_SkeletonModifier3D_constant_SECONDARY_DIRECTION_NONE>`, phương thức này trả về ``Vector3(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_joint_limitation_rotation_offset:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **get_joint_limitation_rotation_offset**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_limitation_rotation_offset>`

Trả về offset xoay của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

Phép xoay được thực hiện trong không gian cục bộ, được tạo bởi hướng của bone (thông thường là từ parent đến child) làm trục +Y và :ref:`get_joint_limitation_right_axis_vector()<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>` làm trục +X.

Nếu các trục +X và +Y không trực giao, trục +X sẽ được ngầm điều chỉnh để trở nên trực giao.

Ngoài ra, nếu độ dài của :ref:`get_joint_limitation_right_axis_vector()<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>` bằng không, không gian được tạo bằng cách xoay tư thế tham chiếu theo cung ngắn nhất, sao cho trục +Y của tư thế tham chiếu khớp với hướng của bone.

Ở đây, tư thế tham chiếu là tư thế bone ngay trước khi xử lý IK.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_joint_rotation_axis:

.. rst-class:: classref-method

:ref:`RotationAxis<enum_SkeletonModifier3D_RotationAxis>` **get_joint_rotation_axis**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_rotation_axis>`

Trả về trục xoay tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_joint_rotation_axis_vector:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_joint_rotation_axis_vector**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_joint_rotation_axis_vector>`

Trả về vector trục xoay cho joint được chỉ định trong chuỗi bone. Vector này biểu thị trục mà joint có thể xoay quanh. Trục này được xác định dựa trên trục xoay được đặt cho joint.

Nếu :ref:`get_joint_rotation_axis()<class_IterateIK3D_method_get_joint_rotation_axis>` là :ref:`SkeletonModifier3D.ROTATION_AXIS_ALL<class_SkeletonModifier3D_constant_ROTATION_AXIS_ALL>`, phương thức này trả về ``Vector3(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_get_target_node:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_target_node**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IterateIK3D_method_get_target_node>`

Trả về node mục tiêu mà bone cuối đang cố gắng đạt đến.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_limitation:

.. rst-class:: classref-method

|void| **set_joint_limitation**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, limitation\: :ref:`JointLimitation3D<class_JointLimitation3D>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_limitation>`

Đặt giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_limitation_right_axis:

.. rst-class:: classref-method

|void| **set_joint_limitation_right_axis**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, direction\: :ref:`SecondaryDirection<enum_SkeletonModifier3D_SecondaryDirection>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_limitation_right_axis>`

Đặt trục phải của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_limitation_right_axis_vector:

.. rst-class:: classref-method

|void| **set_joint_limitation_right_axis_vector**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, vector\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_limitation_right_axis_vector>`

Đặt vector trục phải tùy chọn của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_limitation_rotation_offset:

.. rst-class:: classref-method

|void| **set_joint_limitation_rotation_offset**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, offset\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_limitation_rotation_offset>`

Đặt offset xoay của giới hạn joint tại ``joint`` trong danh sách joint của chuỗi bone.

Phép xoay được thực hiện trong không gian cục bộ, được tạo bởi hướng của bone (thông thường là từ parent đến child) làm trục +Y và :ref:`get_joint_limitation_right_axis_vector()<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>` làm trục +X.

Nếu các trục +X và +Y không trực giao, trục +X sẽ được ngầm điều chỉnh để trở nên trực giao.

Ngoài ra, nếu độ dài của :ref:`get_joint_limitation_right_axis_vector()<class_IterateIK3D_method_get_joint_limitation_right_axis_vector>` bằng không, không gian được tạo bằng cách xoay tư thế tham chiếu theo cung ngắn nhất, sao cho trục +Y của tư thế tham chiếu khớp với hướng của bone.

Ở đây, tư thế tham chiếu là tư thế bone ngay trước khi xử lý IK.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_rotation_axis:

.. rst-class:: classref-method

|void| **set_joint_rotation_axis**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, axis\: :ref:`RotationAxis<enum_SkeletonModifier3D_RotationAxis>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_rotation_axis>`

Đặt trục xoay tại ``joint`` trong danh sách joint của chuỗi bone.

Các trục dựa trên không gian của tư thế tham chiếu; nếu ``axis`` là :ref:`SkeletonModifier3D.ROTATION_AXIS_CUSTOM<class_SkeletonModifier3D_constant_ROTATION_AXIS_CUSTOM>`, bạn có thể chỉ định bất kỳ trục nào.

Ở đây, tư thế tham chiếu là tư thế bone ngay trước khi xử lý IK.

\ **Lưu ý:** Trục xoay và vector hướng không nên đồng tuyến để tránh xoay ngoài ý muốn, vì :ref:`ChainIK3D<class_ChainIK3D>` không tính đến các lực xoắn.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_joint_rotation_axis_vector:

.. rst-class:: classref-method

|void| **set_joint_rotation_axis_vector**\ (\ index\: :ref:`int<class_int>`, joint\: :ref:`int<class_int>`, axis_vector\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_IterateIK3D_method_set_joint_rotation_axis_vector>`

Đặt vector trục xoay cho joint được chỉ định trong chuỗi bone.

Vector này được chuẩn hóa bởi một quy trình nội bộ và biểu thị trục mà chuỗi bone có thể xoay quanh.

Nếu độ dài vector là ``0``, nó được xem là đồng nghĩa với :ref:`SkeletonModifier3D.ROTATION_AXIS_ALL<class_SkeletonModifier3D_constant_ROTATION_AXIS_ALL>`.

.. rst-class:: classref-item-separator

----

.. _class_IterateIK3D_method_set_target_node:

.. rst-class:: classref-method

|void| **set_target_node**\ (\ index\: :ref:`int<class_int>`, target_node\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_IterateIK3D_method_set_target_node>`

Đặt node mục tiêu mà bone cuối đang cố gắng đạt đến.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
