:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Generic6DOFJoint3D.xml.

.. _class_Generic6DOFJoint3D:

Generic6DOFJoint3D
==================

**Kế thừa:** :ref:`Joint3D<class_Joint3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics joint cho phép chuyển động và xoay phức tạp giữa hai physics body 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Joint **Generic6DOFJoint3D** (6 Degrees Of Freedom) cho phép triển khai các loại joint tùy chỉnh bằng cách khóa chuyển động xoay và tịnh tiến của một số trục.

3 DOF đầu tiên biểu thị chuyển động tuyến tính của các physics body, còn 3 DOF cuối biểu thị chuyển động góc của các physics body. Mỗi trục có thể bị khóa hoặc bị giới hạn.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/damping<class_Generic6DOFJoint3D_property_angular_limit_x/damping>`                       | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_limit_x/enabled<class_Generic6DOFJoint3D_property_angular_limit_x/enabled>`                       | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/erp<class_Generic6DOFJoint3D_property_angular_limit_x/erp>`                               | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/force_limit<class_Generic6DOFJoint3D_property_angular_limit_x/force_limit>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/lower_angle<class_Generic6DOFJoint3D_property_angular_limit_x/lower_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/restitution<class_Generic6DOFJoint3D_property_angular_limit_x/restitution>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/softness<class_Generic6DOFJoint3D_property_angular_limit_x/softness>`                     | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_x/upper_angle<class_Generic6DOFJoint3D_property_angular_limit_x/upper_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/damping<class_Generic6DOFJoint3D_property_angular_limit_y/damping>`                       | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_limit_y/enabled<class_Generic6DOFJoint3D_property_angular_limit_y/enabled>`                       | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/erp<class_Generic6DOFJoint3D_property_angular_limit_y/erp>`                               | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/force_limit<class_Generic6DOFJoint3D_property_angular_limit_y/force_limit>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/lower_angle<class_Generic6DOFJoint3D_property_angular_limit_y/lower_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/restitution<class_Generic6DOFJoint3D_property_angular_limit_y/restitution>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/softness<class_Generic6DOFJoint3D_property_angular_limit_y/softness>`                     | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_y/upper_angle<class_Generic6DOFJoint3D_property_angular_limit_y/upper_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/damping<class_Generic6DOFJoint3D_property_angular_limit_z/damping>`                       | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_limit_z/enabled<class_Generic6DOFJoint3D_property_angular_limit_z/enabled>`                       | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/erp<class_Generic6DOFJoint3D_property_angular_limit_z/erp>`                               | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/force_limit<class_Generic6DOFJoint3D_property_angular_limit_z/force_limit>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/lower_angle<class_Generic6DOFJoint3D_property_angular_limit_z/lower_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/restitution<class_Generic6DOFJoint3D_property_angular_limit_z/restitution>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/softness<class_Generic6DOFJoint3D_property_angular_limit_z/softness>`                     | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_z/upper_angle<class_Generic6DOFJoint3D_property_angular_limit_z/upper_angle>`               | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_motor_x/enabled<class_Generic6DOFJoint3D_property_angular_motor_x/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_x/force_limit<class_Generic6DOFJoint3D_property_angular_motor_x/force_limit>`               | ``300.0`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_x/target_velocity<class_Generic6DOFJoint3D_property_angular_motor_x/target_velocity>`       | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_motor_y/enabled<class_Generic6DOFJoint3D_property_angular_motor_y/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_y/force_limit<class_Generic6DOFJoint3D_property_angular_motor_y/force_limit>`               | ``300.0`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_y/target_velocity<class_Generic6DOFJoint3D_property_angular_motor_y/target_velocity>`       | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_motor_z/enabled<class_Generic6DOFJoint3D_property_angular_motor_z/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_z/force_limit<class_Generic6DOFJoint3D_property_angular_motor_z/force_limit>`               | ``300.0`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_motor_z/target_velocity<class_Generic6DOFJoint3D_property_angular_motor_z/target_velocity>`       | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_x/damping<class_Generic6DOFJoint3D_property_angular_spring_x/damping>`                     | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_spring_x/enabled<class_Generic6DOFJoint3D_property_angular_spring_x/enabled>`                     | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_x/equilibrium_point<class_Generic6DOFJoint3D_property_angular_spring_x/equilibrium_point>` | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_x/stiffness<class_Generic6DOFJoint3D_property_angular_spring_x/stiffness>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_y/damping<class_Generic6DOFJoint3D_property_angular_spring_y/damping>`                     | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_spring_y/enabled<class_Generic6DOFJoint3D_property_angular_spring_y/enabled>`                     | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_y/equilibrium_point<class_Generic6DOFJoint3D_property_angular_spring_y/equilibrium_point>` | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_y/stiffness<class_Generic6DOFJoint3D_property_angular_spring_y/stiffness>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_z/damping<class_Generic6DOFJoint3D_property_angular_spring_z/damping>`                     | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_spring_z/enabled<class_Generic6DOFJoint3D_property_angular_spring_z/enabled>`                     | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_z/equilibrium_point<class_Generic6DOFJoint3D_property_angular_spring_z/equilibrium_point>` | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_spring_z/stiffness<class_Generic6DOFJoint3D_property_angular_spring_z/stiffness>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_x/damping<class_Generic6DOFJoint3D_property_linear_limit_x/damping>`                         | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_limit_x/enabled<class_Generic6DOFJoint3D_property_linear_limit_x/enabled>`                         | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_x/lower_distance<class_Generic6DOFJoint3D_property_linear_limit_x/lower_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_x/restitution<class_Generic6DOFJoint3D_property_linear_limit_x/restitution>`                 | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_x/softness<class_Generic6DOFJoint3D_property_linear_limit_x/softness>`                       | ``0.7``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_x/upper_distance<class_Generic6DOFJoint3D_property_linear_limit_x/upper_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_y/damping<class_Generic6DOFJoint3D_property_linear_limit_y/damping>`                         | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_limit_y/enabled<class_Generic6DOFJoint3D_property_linear_limit_y/enabled>`                         | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_y/lower_distance<class_Generic6DOFJoint3D_property_linear_limit_y/lower_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_y/restitution<class_Generic6DOFJoint3D_property_linear_limit_y/restitution>`                 | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_y/softness<class_Generic6DOFJoint3D_property_linear_limit_y/softness>`                       | ``0.7``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_y/upper_distance<class_Generic6DOFJoint3D_property_linear_limit_y/upper_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_z/damping<class_Generic6DOFJoint3D_property_linear_limit_z/damping>`                         | ``1.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_limit_z/enabled<class_Generic6DOFJoint3D_property_linear_limit_z/enabled>`                         | ``true``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_z/lower_distance<class_Generic6DOFJoint3D_property_linear_limit_z/lower_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_z/restitution<class_Generic6DOFJoint3D_property_linear_limit_z/restitution>`                 | ``0.5``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_z/softness<class_Generic6DOFJoint3D_property_linear_limit_z/softness>`                       | ``0.7``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_limit_z/upper_distance<class_Generic6DOFJoint3D_property_linear_limit_z/upper_distance>`           | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_motor_x/enabled<class_Generic6DOFJoint3D_property_linear_motor_x/enabled>`                         | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_x/force_limit<class_Generic6DOFJoint3D_property_linear_motor_x/force_limit>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_x/target_velocity<class_Generic6DOFJoint3D_property_linear_motor_x/target_velocity>`         | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_motor_y/enabled<class_Generic6DOFJoint3D_property_linear_motor_y/enabled>`                         | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_y/force_limit<class_Generic6DOFJoint3D_property_linear_motor_y/force_limit>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_y/target_velocity<class_Generic6DOFJoint3D_property_linear_motor_y/target_velocity>`         | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_motor_z/enabled<class_Generic6DOFJoint3D_property_linear_motor_z/enabled>`                         | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_z/force_limit<class_Generic6DOFJoint3D_property_linear_motor_z/force_limit>`                 | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_motor_z/target_velocity<class_Generic6DOFJoint3D_property_linear_motor_z/target_velocity>`         | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_x/damping<class_Generic6DOFJoint3D_property_linear_spring_x/damping>`                       | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_spring_x/enabled<class_Generic6DOFJoint3D_property_linear_spring_x/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_x/equilibrium_point<class_Generic6DOFJoint3D_property_linear_spring_x/equilibrium_point>`   | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_x/stiffness<class_Generic6DOFJoint3D_property_linear_spring_x/stiffness>`                   | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_y/damping<class_Generic6DOFJoint3D_property_linear_spring_y/damping>`                       | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_spring_y/enabled<class_Generic6DOFJoint3D_property_linear_spring_y/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_y/equilibrium_point<class_Generic6DOFJoint3D_property_linear_spring_y/equilibrium_point>`   | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_y/stiffness<class_Generic6DOFJoint3D_property_linear_spring_y/stiffness>`                   | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_z/damping<class_Generic6DOFJoint3D_property_linear_spring_z/damping>`                       | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`linear_spring_z/enabled<class_Generic6DOFJoint3D_property_linear_spring_z/enabled>`                       | ``false`` |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_z/equilibrium_point<class_Generic6DOFJoint3D_property_linear_spring_z/equilibrium_point>`   | ``0.0``   |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`linear_spring_z/stiffness<class_Generic6DOFJoint3D_property_linear_spring_z/stiffness>`                   | ``0.01``  |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_flag_x<class_Generic6DOFJoint3D_method_get_flag_x>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|                                 |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_flag_y<class_Generic6DOFJoint3D_method_get_flag_y>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|                                 |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_flag_z<class_Generic6DOFJoint3D_method_get_flag_z>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|                                 |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param_x<class_Generic6DOFJoint3D_method_get_param_x>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|                            |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param_y<class_Generic6DOFJoint3D_method_get_param_y>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|                            |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param_z<class_Generic6DOFJoint3D_method_get_param_z>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|                            |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_flag_x<class_Generic6DOFJoint3D_method_set_flag_x>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ )        |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_flag_y<class_Generic6DOFJoint3D_method_set_flag_y>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ )        |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_flag_z<class_Generic6DOFJoint3D_method_set_flag_z>`\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ )        |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_x<class_Generic6DOFJoint3D_method_set_param_x>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_y<class_Generic6DOFJoint3D_method_set_param_y>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_z<class_Generic6DOFJoint3D_method_set_param_z>`\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các phép liệt kê
----------------

.. _enum_Generic6DOFJoint3D_Param:

.. rst-class:: classref-enumeration

enum **Param**: :ref:`🔗<enum_Generic6DOFJoint3D_Param>`

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_LOWER_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_LOWER_LIMIT** = ``0``

Độ chênh lệch tối thiểu giữa các trục của các pivot point.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_UPPER_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_UPPER_LIMIT** = ``1``

Độ chênh lệch tối đa giữa các trục của các pivot point.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_LIMIT_SOFTNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_LIMIT_SOFTNESS** = ``2``

Hệ số được áp dụng cho chuyển động dọc theo các trục. Giá trị càng nhỏ, chuyển động càng chậm.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_RESTITUTION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_RESTITUTION** = ``3``

Mức restitution của chuyển động dọc theo các trục. Giá trị càng nhỏ, càng mất nhiều động lượng.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_DAMPING** = ``4``

Mức damping xảy ra trong chuyển động tuyến tính dọc theo các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_MOTOR_TARGET_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_MOTOR_TARGET_VELOCITY** = ``5``

Vận tốc mà linear motor sẽ cố đạt tới.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_MOTOR_FORCE_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_MOTOR_FORCE_LIMIT** = ``6``

Lực tối đa mà linear motor sẽ áp dụng khi cố đạt tới vận tốc mục tiêu.

.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_SPRING_STIFFNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_SPRING_STIFFNESS** = ``7``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_SPRING_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_SPRING_DAMPING** = ``8``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_LINEAR_SPRING_EQUILIBRIUM_POINT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_LINEAR_SPRING_EQUILIBRIUM_POINT** = ``9``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_LOWER_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_LOWER_LIMIT** = ``10``

Góc xoay tối thiểu theo hướng âm để bắt đầu chuyển động tự do và xoay quanh các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_UPPER_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_UPPER_LIMIT** = ``11``

Góc xoay tối thiểu theo hướng dương để bắt đầu chuyển động tự do và xoay quanh các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_LIMIT_SOFTNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_LIMIT_SOFTNESS** = ``12``

Tốc độ của mọi chuyển động xoay dọc theo các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_DAMPING** = ``13``

Mức damping xoay dọc theo các trục. Giá trị càng nhỏ, damping xảy ra càng nhiều.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_RESTITUTION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_RESTITUTION** = ``14``

Mức restitution xoay dọc theo các trục. Giá trị càng nhỏ, restitution xảy ra càng nhiều.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_FORCE_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_FORCE_LIMIT** = ``15``

Lực tối đa có thể xảy ra khi xoay quanh các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_ERP:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_ERP** = ``16``

Khi xoay dọc theo các trục, hệ số dung sai sai số này xác định mức độ làm chậm quá trình hiệu chỉnh. Giá trị càng nhỏ, tốc độ càng chậm.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_MOTOR_TARGET_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_MOTOR_TARGET_VELOCITY** = ``17``

Tốc độ mục tiêu cho motor tại các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_MOTOR_FORCE_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_MOTOR_FORCE_LIMIT** = ``18``

Gia tốc tối đa cho motor tại các trục.

.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_SPRING_STIFFNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_SPRING_STIFFNESS** = ``19``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_SPRING_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_SPRING_DAMPING** = ``20``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_ANGULAR_SPRING_EQUILIBRIUM_POINT:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_ANGULAR_SPRING_EQUILIBRIUM_POINT** = ``21``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_PARAM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Generic6DOFJoint3D_Param>` **PARAM_MAX** = ``22``

Biểu thị kích thước của enum :ref:`Param<enum_Generic6DOFJoint3D_Param>`.

.. rst-class:: classref-item-separator

----

.. _enum_Generic6DOFJoint3D_Flag:

.. rst-class:: classref-enumeration

enum **Flag**: :ref:`🔗<enum_Generic6DOFJoint3D_Flag>`

.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_LINEAR_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_LINEAR_LIMIT** = ``0``

Nếu được bật, chuyển động tuyến tính có thể xảy ra trong các giới hạn đã cho.

.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_ANGULAR_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_ANGULAR_LIMIT** = ``1``

Nếu được bật, chuyển động xoay có thể xảy ra trong các giới hạn đã cho.

.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_LINEAR_SPRING:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_LINEAR_SPRING** = ``3``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_ANGULAR_SPRING:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_ANGULAR_SPRING** = ``2``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_MOTOR:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_MOTOR** = ``4``

Nếu được bật, sẽ có một rotational motor dọc theo các trục này.

.. _class_Generic6DOFJoint3D_constant_FLAG_ENABLE_LINEAR_MOTOR:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_ENABLE_LINEAR_MOTOR** = ``5``

Nếu được bật, sẽ có một linear motor dọc theo các trục này.

.. _class_Generic6DOFJoint3D_constant_FLAG_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_Generic6DOFJoint3D_Flag>` **FLAG_MAX** = ``6``

Biểu thị kích thước của enum :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Generic6DOFJoint3D_property_angular_limit_x/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức damping xoay dọc theo trục X.

Giá trị càng nhỏ, xung lực từ một phía càng mất nhiều thời gian để truyền sang phía bên kia.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_limit_x/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động xoay dọc theo trục X bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/erp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/erp** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/erp>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Khi xoay dọc theo trục X, hệ số dung sai sai số này xác định mức độ làm chậm quá trình hiệu chỉnh. Giá trị càng nhỏ, tốc độ càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa có thể xảy ra khi xoay quanh trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/lower_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/lower_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/lower_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng âm để bắt đầu chuyển động tự do và xoay quanh trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/restitution** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức restitution xoay dọc theo trục X. Giá trị càng nhỏ, restitution xảy ra càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/softness** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ của mọi chuyển động xoay dọc theo trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_x/upper_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_x/upper_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_x/upper_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng dương để bắt đầu chuyển động tự do và xoay quanh trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức damping xoay trên trục Y. Giá trị càng thấp thì damping càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_limit_y/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động xoay trên trục Y sẽ bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/erp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/erp** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/erp>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Khi xoay trên trục Y, hệ số dung sai lỗi này xác định mức độ làm chậm hiệu chỉnh. Giá trị càng thấp thì tốc độ càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa có thể phát sinh khi xoay quanh trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/lower_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/lower_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/lower_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng âm để thoát khỏi giới hạn và xoay quanh trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/restitution** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức restitution xoay trên trục Y. Giá trị càng thấp thì restitution càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/softness** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ của mọi chuyển động xoay trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_y/upper_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_y/upper_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_y/upper_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng dương để thoát khỏi giới hạn và xoay quanh trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức damping xoay trên trục Z. Giá trị càng thấp thì damping càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_limit_z/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động xoay trên trục Z sẽ bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/erp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/erp** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/erp>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Khi xoay trên trục Z, hệ số dung sai lỗi này xác định mức độ làm chậm hiệu chỉnh. Giá trị càng thấp thì tốc độ càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa có thể phát sinh khi xoay quanh trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/lower_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/lower_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/lower_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng âm để thoát khỏi giới hạn và xoay quanh trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/restitution** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức restitution xoay trên trục Z. Giá trị càng thấp thì restitution càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/softness** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ của mọi chuyển động xoay trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_limit_z/upper_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_z/upper_angle** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_limit_z/upper_angle>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Góc xoay tối thiểu theo hướng dương để thoát khỏi giới hạn và xoay quanh trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_motor_x/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, motor xoay trên trục X được bật.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_x/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_x/force_limit** = ``300.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_x/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Gia tốc tối đa của motor trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_x/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_x/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_x/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mục tiêu của motor trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_motor_y/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, motor xoay trên trục Y được bật.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_y/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_y/force_limit** = ``300.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_y/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Gia tốc tối đa của motor trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_y/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_y/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_y/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mục tiêu của motor trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_motor_z/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, motor xoay trên trục Z được bật.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_z/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_z/force_limit** = ``300.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_z/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Gia tốc tối đa của motor trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_motor_z/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_motor_z/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_motor_z/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mục tiêu của motor trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_x/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_x/damping** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_x/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_spring_x/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_x/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_x/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_x/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_x/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_x/stiffness** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_x/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_y/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_y/damping** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_y/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_spring_y/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_y/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_y/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_y/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_y/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_y/stiffness** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_y/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_z/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_z/damping** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_z/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_spring_z/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_z/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_z/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_z/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_angular_spring_z/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_spring_z/stiffness** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_angular_spring_z/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_x/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức giảm chấn tác động lên chuyển động theo trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_limit_x/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động tuyến tính dọc theo trục X bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/lower_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_x/lower_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/lower_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Chênh lệch tối thiểu giữa các điểm pivot trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_x/restitution** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức độ đàn hồi trong chuyển động theo trục X. Giá trị càng thấp thì càng mất nhiều động lượng.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_x/softness** = ``0.7`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Hệ số được áp dụng cho chuyển động dọc theo trục X. Giá trị càng thấp thì chuyển động càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_x/upper_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_x/upper_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_x/upper_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Chênh lệch tối đa giữa các điểm pivot trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_y/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức giảm chấn tác động lên chuyển động theo trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_limit_y/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động tuyến tính dọc theo trục Y bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/lower_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_y/lower_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/lower_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Chênh lệch tối thiểu giữa các điểm pivot trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_y/restitution** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức độ đàn hồi trong chuyển động theo trục Y. Giá trị càng thấp thì càng mất nhiều động lượng.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_y/softness** = ``0.7`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Hệ số được áp dụng cho chuyển động dọc theo trục Y. Giá trị càng thấp thì chuyển động càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_y/upper_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_y/upper_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_y/upper_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Độ chênh lệch tối đa giữa các điểm xoay trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_z/damping** = ``1.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức damping xảy ra trong chuyển động theo trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_limit_z/enabled** = ``true`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, chuyển động tuyến tính dọc theo trục Z bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/lower_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_z/lower_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/lower_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Độ chênh lệch tối thiểu giữa các điểm xoay trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/restitution:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_z/restitution** = ``0.5`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/restitution>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Mức restitution trong chuyển động theo trục Z. Giá trị càng thấp thì động lượng bị mất càng nhiều.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_z/softness** = ``0.7`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Hệ số được áp dụng cho chuyển động dọc theo trục Z. Giá trị càng thấp thì chuyển động càng chậm.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_limit_z/upper_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_limit_z/upper_distance** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_limit_z/upper_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Độ chênh lệch tối đa giữa các điểm xoay trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_motor_x/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, một linear motor được kích hoạt trên trục X. Nó sẽ cố gắng đạt vận tốc mục tiêu trong khi vẫn nằm trong các giới hạn lực.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_x/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_x/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_x/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa mà linear motor có thể tác dụng lên trục X khi cố gắng đạt vận tốc mục tiêu.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_x/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_x/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_x/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mà linear motor sẽ cố gắng đạt được trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_motor_y/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, một linear motor được kích hoạt trên trục Y. Nó sẽ cố gắng đạt vận tốc mục tiêu trong khi vẫn nằm trong các giới hạn lực.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_y/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_y/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_y/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa mà linear motor có thể tác dụng lên trục Y khi cố gắng đạt vận tốc mục tiêu.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_y/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_y/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_y/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mà linear motor sẽ cố gắng đạt được trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_motor_z/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

Nếu ``true``, một linear motor được kích hoạt trên trục Z. Nó sẽ cố gắng đạt vận tốc mục tiêu trong khi vẫn nằm trong các giới hạn lực.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_z/force_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_z/force_limit** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_z/force_limit>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Lực tối đa mà linear motor có thể tác dụng lên trục Z khi cố gắng đạt vận tốc mục tiêu.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_motor_z/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_motor_z/target_velocity** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_motor_z/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

Tốc độ mà linear motor sẽ cố gắng đạt được trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_x/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_x/damping** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_x/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_x/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_spring_x/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_x/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_x/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_x/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_x/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_x/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_x/stiffness** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_x/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_y/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_y/damping** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_y/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_y/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_spring_y/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_y/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_y/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_y/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_y/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_y/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_y/stiffness** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_y/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_z/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_z/damping** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_z/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_z/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **linear_spring_z/enabled** = ``false`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_z/enabled>`

.. rst-class:: classref-property-setget

- |void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_z/equilibrium_point:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_z/equilibrium_point** = ``0.0`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_z/equilibrium_point>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_property_linear_spring_z/stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_spring_z/stiffness** = ``0.01`` :ref:`🔗<class_Generic6DOFJoint3D_property_linear_spring_z/stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Generic6DOFJoint3D_method_get_flag_x:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_flag_x>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_get_flag_y:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_flag_y>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_get_flag_z:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_flag_z>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_get_param_x:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_param_x>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_get_param_y:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_param_y>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_get_param_z:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`\ ) |const| :ref:`🔗<class_Generic6DOFJoint3D_method_get_param_z>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_flag_x:

.. rst-class:: classref-method

|void| **set_flag_x**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_flag_x>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_flag_y:

.. rst-class:: classref-method

|void| **set_flag_y**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_flag_y>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_flag_z:

.. rst-class:: classref-method

|void| **set_flag_z**\ (\ flag\: :ref:`Flag<enum_Generic6DOFJoint3D_Flag>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_flag_z>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_param_x:

.. rst-class:: classref-method

|void| **set_param_x**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_param_x>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_param_y:

.. rst-class:: classref-method

|void| **set_param_y**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_param_y>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_Generic6DOFJoint3D_method_set_param_z:

.. rst-class:: classref-method

|void| **set_param_z**\ (\ param\: :ref:`Param<enum_Generic6DOFJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Generic6DOFJoint3D_method_set_param_z>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
