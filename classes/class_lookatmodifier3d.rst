:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LookAtModifier3D.xml.

.. _class_LookAtModifier3D:

LookAtModifier3D
================

**Kế thừa:** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**LookAtModifier3D** xoay một bone để hướng về một target.

.. rst-class:: classref-introduction-group

Mô tả
-----

:ref:`SkeletonModifier3D<class_SkeletonModifier3D>` này xoay một bone để hướng về một target. Điều này hữu ích khi muốn di chuyển đầu của nhân vật để nhìn về phía player, xoay một turret để hướng về một target, hoặc trong bất kỳ trường hợp nào khác khi bạn muốn làm cho một bone xoay về phía một đối tượng nào đó một cách nhanh chóng và dễ dàng.

Khi áp dụng nhiều **LookAtModifier3D**\ s, **LookAtModifier3D** được gán cho bone cha phải được đặt phía trên **LookAtModifier3D** được gán cho bone con trong danh sách để kết quả của bone con được chính xác.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                               | :ref:`bone<class_LookAtModifier3D_property_bone>`                                                           | ``-1``               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`String<class_String>`                         | :ref:`bone_name<class_LookAtModifier3D_property_bone_name>`                                                 | ``""``               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`duration<class_LookAtModifier3D_property_duration>`                                                   | ``0.0``              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`EaseType<enum_Tween_EaseType>`                | :ref:`ease_type<class_LookAtModifier3D_property_ease_type>`                                                 | ``0``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>`   | :ref:`forward_axis<class_LookAtModifier3D_property_forward_axis>`                                           | ``4``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                               | :ref:`origin_bone<class_LookAtModifier3D_property_origin_bone>`                                             |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`String<class_String>`                         | :ref:`origin_bone_name<class_LookAtModifier3D_property_origin_bone_name>`                                   |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`NodePath<class_NodePath>`                     | :ref:`origin_external_node<class_LookAtModifier3D_property_origin_external_node>`                           |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` | :ref:`origin_from<class_LookAtModifier3D_property_origin_from>`                                             | ``0``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`origin_offset<class_LookAtModifier3D_property_origin_offset>`                                         | ``Vector3(0, 0, 0)`` |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`origin_safe_margin<class_LookAtModifier3D_property_origin_safe_margin>`                               | ``0.1``              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_damp_threshold<class_LookAtModifier3D_property_primary_damp_threshold>`                       |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_limit_angle<class_LookAtModifier3D_property_primary_limit_angle>`                             |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_negative_damp_threshold<class_LookAtModifier3D_property_primary_negative_damp_threshold>`     |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_negative_limit_angle<class_LookAtModifier3D_property_primary_negative_limit_angle>`           |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_positive_damp_threshold<class_LookAtModifier3D_property_primary_positive_damp_threshold>`     |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`primary_positive_limit_angle<class_LookAtModifier3D_property_primary_positive_limit_angle>`           |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Axis<enum_Vector3_Axis>`                      | :ref:`primary_rotation_axis<class_LookAtModifier3D_property_primary_rotation_axis>`                         | ``1``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                             | :ref:`relative<class_LookAtModifier3D_property_relative>`                                                   | ``false``            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_damp_threshold<class_LookAtModifier3D_property_secondary_damp_threshold>`                   |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_limit_angle<class_LookAtModifier3D_property_secondary_limit_angle>`                         |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_negative_damp_threshold<class_LookAtModifier3D_property_secondary_negative_damp_threshold>` |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_negative_limit_angle<class_LookAtModifier3D_property_secondary_negative_limit_angle>`       |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_positive_damp_threshold<class_LookAtModifier3D_property_secondary_positive_damp_threshold>` |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                           | :ref:`secondary_positive_limit_angle<class_LookAtModifier3D_property_secondary_positive_limit_angle>`       |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                             | :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>`                             |                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`NodePath<class_NodePath>`                     | :ref:`target_node<class_LookAtModifier3D_property_target_node>`                                             | ``NodePath("")``     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`TransitionType<enum_Tween_TransitionType>`    | :ref:`transition_type<class_LookAtModifier3D_property_transition_type>`                                     | ``0``                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                             | :ref:`use_angle_limitation<class_LookAtModifier3D_property_use_angle_limitation>`                           | ``false``            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                             | :ref:`use_secondary_rotation<class_LookAtModifier3D_property_use_secondary_rotation>`                       | ``true``             |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_interpolation_remaining<class_LookAtModifier3D_method_get_interpolation_remaining>`\ (\ ) |const| |
   +---------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`is_interpolating<class_LookAtModifier3D_method_is_interpolating>`\ (\ ) |const|                       |
   +---------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`is_target_within_limitation<class_LookAtModifier3D_method_is_target_within_limitation>`\ (\ ) |const| |
   +---------------------------+-------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_LookAtModifier3D_OriginFrom:

.. rst-class:: classref-enumeration

enum **OriginFrom**: :ref:`🔗<enum_LookAtModifier3D_OriginFrom>`

.. _class_LookAtModifier3D_constant_ORIGIN_FROM_SELF:

.. rst-class:: classref-enumeration-constant

:ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` **ORIGIN_FROM_SELF** = ``0``

Vị trí rest của bone được chỉ định trong :ref:`bone<class_LookAtModifier3D_property_bone>` được dùng làm gốc.

.. _class_LookAtModifier3D_constant_ORIGIN_FROM_SPECIFIC_BONE:

.. rst-class:: classref-enumeration-constant

:ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` **ORIGIN_FROM_SPECIFIC_BONE** = ``1``

Vị trí global pose của bone được chỉ định trong :ref:`origin_bone<class_LookAtModifier3D_property_origin_bone>` được dùng làm gốc.

\ **Lưu ý:** Bạn nên chỉ chọn bone cha, trừ khi đã quen với quy trình xử lý bone. Pose của bone được chỉ định tại thời điểm **LookAtModifier3D** được xử lý sẽ được dùng làm tham chiếu. Nói cách khác, nếu bạn chỉ định một bone con và **LookAtModifier3D** khiến bone con di chuyển, kết quả được render và hướng sẽ không khớp.

.. _class_LookAtModifier3D_constant_ORIGIN_FROM_EXTERNAL_NODE:

.. rst-class:: classref-enumeration-constant

:ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` **ORIGIN_FROM_EXTERNAL_NODE** = ``2``

Vị trí global của :ref:`Node3D<class_Node3D>` được chỉ định trong :ref:`origin_external_node<class_LookAtModifier3D_property_origin_external_node>` được dùng làm gốc.

\ **Lưu ý:** Tương tự :ref:`ORIGIN_FROM_SPECIFIC_BONE<class_LookAtModifier3D_constant_ORIGIN_FROM_SPECIFIC_BONE>`, khi chỉ định một :ref:`BoneAttachment3D<class_BoneAttachment3D>` có bone con được gán, kết quả được render và hướng sẽ không khớp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LookAtModifier3D_property_bone:

.. rst-class:: classref-property

:ref:`int<class_int>` **bone** = ``-1`` :ref:`🔗<class_LookAtModifier3D_property_bone>`

.. rst-class:: classref-property-setget

- |void| **set_bone**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bone**\ (\ )

Chỉ mục của :ref:`bone_name<class_LookAtModifier3D_property_bone_name>` trong :ref:`Skeleton3D<class_Skeleton3D>` cha.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_bone_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **bone_name** = ``""`` :ref:`🔗<class_LookAtModifier3D_property_bone_name>`

.. rst-class:: classref-property-setget

- |void| **set_bone_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_bone_name**\ (\ )

Tên bone của :ref:`Skeleton3D<class_Skeleton3D>` mà phép sửa đổi sẽ tác động lên.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_duration:

.. rst-class:: classref-property

:ref:`float<class_float>` **duration** = ``0.0`` :ref:`🔗<class_LookAtModifier3D_property_duration>`

.. rst-class:: classref-property-setget

- |void| **set_duration**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_duration**\ (\ )

Thời lượng của phép nội suy dựa trên thời gian. Phép nội suy được kích hoạt trong các trường hợp sau:

- Khi node target thay đổi

- Khi một trục bị lật do giới hạn góc

\ **Lưu ý:** Việc lật xảy ra khi target nằm ngoài giới hạn góc và trục xoay phụ được tính toán nội bộ của vector hướng về phía trước bị lật. Về mặt trực quan, điều này xảy ra khi target nằm ngoài giới hạn góc và cắt qua mặt phẳng của :ref:`forward_axis<class_LookAtModifier3D_property_forward_axis>` và :ref:`primary_rotation_axis<class_LookAtModifier3D_property_primary_rotation_axis>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_ease_type:

.. rst-class:: classref-property

:ref:`EaseType<enum_Tween_EaseType>` **ease_type** = ``0`` :ref:`🔗<class_LookAtModifier3D_property_ease_type>`

.. rst-class:: classref-property-setget

- |void| **set_ease_type**\ (\ value\: :ref:`EaseType<enum_Tween_EaseType>`\ ) - :ref:`EaseType<enum_Tween_EaseType>` **get_ease_type**\ (\ )

Kiểu ease của phép nội suy dựa trên thời gian. Xem thêm :ref:`EaseType<enum_Tween_EaseType>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_forward_axis:

.. rst-class:: classref-property

:ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>` **forward_axis** = ``4`` :ref:`🔗<class_LookAtModifier3D_property_forward_axis>`

.. rst-class:: classref-property-setget

- |void| **set_forward_axis**\ (\ value\: :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>`\ ) - :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>` **get_forward_axis**\ (\ )

Trục hướng về phía trước của bone. :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` này sửa đổi bone để trục này hướng về phía :ref:`target_node<class_LookAtModifier3D_property_target_node>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_bone:

.. rst-class:: classref-property

:ref:`int<class_int>` **origin_bone** :ref:`🔗<class_LookAtModifier3D_property_origin_bone>`

.. rst-class:: classref-property-setget

- |void| **set_origin_bone**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_origin_bone**\ (\ )

Chỉ mục của :ref:`origin_bone_name<class_LookAtModifier3D_property_origin_bone_name>` trong :ref:`Skeleton3D<class_Skeleton3D>` cha.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_bone_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **origin_bone_name** :ref:`🔗<class_LookAtModifier3D_property_origin_bone_name>`

.. rst-class:: classref-property-setget

- |void| **set_origin_bone_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_origin_bone_name**\ (\ )

Nếu :ref:`origin_from<class_LookAtModifier3D_property_origin_from>` là :ref:`ORIGIN_FROM_SPECIFIC_BONE<class_LookAtModifier3D_constant_ORIGIN_FROM_SPECIFIC_BONE>`, vị trí global pose của bone được chỉ định cho thuộc tính này sẽ được dùng làm gốc.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_external_node:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **origin_external_node** :ref:`🔗<class_LookAtModifier3D_property_origin_external_node>`

.. rst-class:: classref-property-setget

- |void| **set_origin_external_node**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_origin_external_node**\ (\ )

Nếu :ref:`origin_from<class_LookAtModifier3D_property_origin_from>` là :ref:`ORIGIN_FROM_EXTERNAL_NODE<class_LookAtModifier3D_constant_ORIGIN_FROM_EXTERNAL_NODE>`, vị trí global của :ref:`Node3D<class_Node3D>` được chỉ định cho thuộc tính này sẽ được dùng làm gốc.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_from:

.. rst-class:: classref-property

:ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` **origin_from** = ``0`` :ref:`🔗<class_LookAtModifier3D_property_origin_from>`

.. rst-class:: classref-property-setget

- |void| **set_origin_from**\ (\ value\: :ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>`\ ) - :ref:`OriginFrom<enum_LookAtModifier3D_OriginFrom>` **get_origin_from**\ (\ )

Giá trị này xác định gốc nào được lấy để sử dụng trong phép tính vector hướng về phía trước.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_offset:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **origin_offset** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_LookAtModifier3D_property_origin_offset>`

.. rst-class:: classref-property-setget

- |void| **set_origin_offset**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_origin_offset**\ (\ )

Độ lệch của gốc pose của bone. Việc khớp các gốc bằng độ lệch hữu ích trong những trường hợp nhiều bone phải luôn hướng về cùng một hướng, chẳng hạn như các mắt.

\ **Lưu ý:** Giá trị này biểu thị vị trí local của đối tượng được đặt trong :ref:`origin_from<class_LookAtModifier3D_property_origin_from>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_origin_safe_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **origin_safe_margin** = ``0.1`` :ref:`🔗<class_LookAtModifier3D_property_origin_safe_margin>`

.. rst-class:: classref-property-setget

- |void| **set_origin_safe_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_origin_safe_margin**\ (\ )

Nếu target đi qua quá gần gốc, gần hơn giá trị này, phép nội suy dựa trên thời gian sẽ được sử dụng ngay cả khi target nằm trong giới hạn góc, nhằm ngăn vận tốc góc trở nên quá cao.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_primary_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_primary_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`primary_limit_angle<class_LookAtModifier3D_property_primary_limit_angle>`. Thuộc tính này cung cấp phép nội suy phi tuyến (b-spline), khiến chuyển động có cảm giác bị cản trở nhiều hơn khi xoay đến gần giới hạn biên. Điều này hữu ích để mô phỏng các giới hạn chuyển động của con người.

Nếu ``1.0``, không thực hiện damping. Nếu ``0.0``, damping luôn được thực hiện.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_primary_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_primary_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_limit_angle**\ (\ )

Góc giới hạn của phép xoay chính khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``true``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_negative_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_negative_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_primary_negative_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_primary_negative_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_negative_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`primary_negative_limit_angle<class_LookAtModifier3D_property_primary_negative_limit_angle>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_negative_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_negative_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_primary_negative_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_primary_negative_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_negative_limit_angle**\ (\ )

Góc giới hạn ở phía âm của phép xoay chính khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``false``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_positive_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_positive_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_primary_positive_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_primary_positive_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_positive_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`primary_positive_limit_angle<class_LookAtModifier3D_property_primary_positive_limit_angle>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_positive_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **primary_positive_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_primary_positive_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_primary_positive_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_primary_positive_limit_angle**\ (\ )

Góc giới hạn ở phía dương của phép xoay chính khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``false``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_primary_rotation_axis:

.. rst-class:: classref-property

:ref:`Axis<enum_Vector3_Axis>` **primary_rotation_axis** = ``1`` :ref:`🔗<class_LookAtModifier3D_property_primary_rotation_axis>`

.. rst-class:: classref-property-setget

- |void| **set_primary_rotation_axis**\ (\ value\: :ref:`Axis<enum_Vector3_Axis>`\ ) - :ref:`Axis<enum_Vector3_Axis>` **get_primary_rotation_axis**\ (\ )

Trục của phép xoay đầu tiên. :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` này hoạt động bằng cách tổng hợp phép xoay theo các góc Euler để tránh xoay :ref:`forward_axis<class_LookAtModifier3D_property_forward_axis>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_relative:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **relative** = ``false`` :ref:`🔗<class_LookAtModifier3D_property_relative>`

.. rst-class:: classref-property-setget

- |void| **set_relative**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_relative**\ (\ )

Tùy chọn relative. Nếu ``true``, phép xoay được áp dụng tương đối với tư thế. Nếu ``false``, phép xoay được áp dụng tương đối với tư thế nghỉ. Điều này có nghĩa là thay thế tư thế hiện tại bằng kết quả của **LookAtModifier3D**.

\ **Lưu ý:** Tùy chọn này ảnh hưởng đến góc cơ sở của :ref:`use_angle_limitation<class_LookAtModifier3D_property_use_angle_limitation>`. Vì **LookAtModifier3D** phụ thuộc nhiều vào phép xoay Euler, trục xác định giới hạn và phép xoay thực tế có mối liên hệ chặt chẽ với nhau.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_secondary_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`secondary_limit_angle<class_LookAtModifier3D_property_secondary_limit_angle>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_secondary_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_limit_angle**\ (\ )

Góc giới hạn của phép xoay phụ khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``true``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_negative_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_negative_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_secondary_negative_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_negative_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_negative_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`secondary_negative_limit_angle<class_LookAtModifier3D_property_secondary_negative_limit_angle>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_negative_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_negative_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_secondary_negative_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_negative_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_negative_limit_angle**\ (\ )

Góc giới hạn ở phía âm của phép xoay phụ khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``false``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_positive_damp_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_positive_damp_threshold** :ref:`🔗<class_LookAtModifier3D_property_secondary_positive_damp_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_positive_damp_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_positive_damp_threshold**\ (\ )

Ngưỡng bắt đầu damping cho :ref:`secondary_positive_limit_angle<class_LookAtModifier3D_property_secondary_positive_limit_angle>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_secondary_positive_limit_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **secondary_positive_limit_angle** :ref:`🔗<class_LookAtModifier3D_property_secondary_positive_limit_angle>`

.. rst-class:: classref-property-setget

- |void| **set_secondary_positive_limit_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_secondary_positive_limit_angle**\ (\ )

Góc giới hạn ở phía dương của phép xoay phụ khi :ref:`symmetry_limitation<class_LookAtModifier3D_property_symmetry_limitation>` là ``false``, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_symmetry_limitation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **symmetry_limitation** :ref:`🔗<class_LookAtModifier3D_property_symmetry_limitation>`

.. rst-class:: classref-property-setget

- |void| **set_symmetry_limitation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_limitation_symmetry**\ (\ )

Nếu ``true``, các giới hạn được phân bố đối xứng từ xương.

Nếu ``false``, có thể chỉ định giới hạn riêng cho mỗi phía của tư thế nghỉ của xương.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_target_node:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **target_node** = ``NodePath("")`` :ref:`🔗<class_LookAtModifier3D_property_target_node>`

.. rst-class:: classref-property-setget

- |void| **set_target_node**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_target_node**\ (\ )

:ref:`NodePath<class_NodePath>` đến node làm mục tiêu cho phép biến đổi look at. Node này là đối tượng mà phép biến đổi sẽ xoay xương hướng tới.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_transition_type:

.. rst-class:: classref-property

:ref:`TransitionType<enum_Tween_TransitionType>` **transition_type** = ``0`` :ref:`🔗<class_LookAtModifier3D_property_transition_type>`

.. rst-class:: classref-property-setget

- |void| **set_transition_type**\ (\ value\: :ref:`TransitionType<enum_Tween_TransitionType>`\ ) - :ref:`TransitionType<enum_Tween_TransitionType>` **get_transition_type**\ (\ )

Loại chuyển tiếp của phép nội suy dựa trên thời gian. Xem thêm :ref:`TransitionType<enum_Tween_TransitionType>`.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_use_angle_limitation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_angle_limitation** = ``false`` :ref:`🔗<class_LookAtModifier3D_property_use_angle_limitation>`

.. rst-class:: classref-property-setget

- |void| **set_use_angle_limitation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_angle_limitation**\ (\ )

Nếu ``true``, giới hạn mức độ xoay. Ví dụ, tùy chọn này giúp ngăn cổ của nhân vật xoay 360 độ.

\ **Lưu ý:** Cũng như phép blending của :ref:`AnimationTree<class_AnimationTree>`, phép nội suy được cung cấp để ưu tiên :ref:`Skeleton3D.get_bone_rest()<class_Skeleton3D_method_get_bone_rest>` hoặc :ref:`Skeleton3D.get_bone_pose()<class_Skeleton3D_method_get_bone_pose>` tùy thuộc vào tùy chọn :ref:`relative<class_LookAtModifier3D_property_relative>`. Điều này có nghĩa là trong một số trường hợp, phép nội suy không chọn đường đi ngắn nhất.

\ **Lưu ý:** Một số giá trị của :ref:`transition_type<class_LookAtModifier3D_property_transition_type>` (chẳng hạn như :ref:`Tween.TRANS_BACK<class_Tween_constant_TRANS_BACK>`, :ref:`Tween.TRANS_ELASTIC<class_Tween_constant_TRANS_ELASTIC>` và :ref:`Tween.TRANS_SPRING<class_Tween_constant_TRANS_SPRING>`) có thể vượt quá các giới hạn. Nếu phép nội suy xảy ra trong khi vượt quá các giới hạn, kết quả có thể không tôn trọng tư thế nghỉ của xương.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_property_use_secondary_rotation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_secondary_rotation** = ``true`` :ref:`🔗<class_LookAtModifier3D_property_use_secondary_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_use_secondary_rotation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_secondary_rotation**\ (\ )

Nếu ``true``, cung cấp phép xoay theo hai trục.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_LookAtModifier3D_method_get_interpolation_remaining:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_interpolation_remaining**\ (\ ) |const| :ref:`🔗<class_LookAtModifier3D_method_get_interpolation_remaining>`

Trả về số giây còn lại của phép nội suy dựa trên thời gian.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_method_is_interpolating:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_interpolating**\ (\ ) |const| :ref:`🔗<class_LookAtModifier3D_method_is_interpolating>`

Trả về ``true`` nếu phép nội suy dựa trên thời gian đang chạy. Nếu ``true``, điều này tương đương với việc :ref:`get_interpolation_remaining()<class_LookAtModifier3D_method_get_interpolation_remaining>` trả về ``0.0``.

Điều này hữu ích để xác định liệu có thể xóa **LookAtModifier3D** một cách an toàn hay không.

.. rst-class:: classref-item-separator

----

.. _class_LookAtModifier3D_method_is_target_within_limitation:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_target_within_limitation**\ (\ ) |const| :ref:`🔗<class_LookAtModifier3D_method_is_target_within_limitation>`

Trả về việc mục tiêu có nằm trong các giới hạn góc hay không. Điều này hữu ích để bỏ đặt :ref:`target_node<class_LookAtModifier3D_property_target_node>` khi mục tiêu nằm ngoài các giới hạn góc.

\ **Lưu ý:** Giá trị được cập nhật sau :ref:`SkeletonModifier3D._process_modification()<class_SkeletonModifier3D_private_method__process_modification>`. Để truy xuất chính xác giá trị này, bạn nên sử dụng signal :ref:`SkeletonModifier3D.modification_processed<class_SkeletonModifier3D_signal_modification_processed>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
