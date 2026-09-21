:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFPhysicsBody.xml.

.. _class_GLTFPhysicsBody:

GLTFPhysicsBody
===============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một physics body glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một physics body làm lớp trung gian giữa dữ liệu glTF ``OMI_physics_body`` và các node của Godot, đồng thời được trừu tượng hóa theo cách cho phép thêm hỗ trợ cho các glTF physics extension khác nhau trong tương lai.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tải và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `OMI_physics_body glTF extension <https://github.com/omigroup/gltf-extensions/tree/main/extensions/2.0/OMI_physics_body>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`angular_velocity<class_GLTFPhysicsBody_property_angular_velocity>`       | ``Vector3(0, 0, 0)``                 |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`String<class_String>`         | :ref:`body_type<class_GLTFPhysicsBody_property_body_type>`                     | ``"rigid"``                          |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`center_of_mass<class_GLTFPhysicsBody_property_center_of_mass>`           | ``Vector3(0, 0, 0)``                 |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`inertia_diagonal<class_GLTFPhysicsBody_property_inertia_diagonal>`       | ``Vector3(0, 0, 0)``                 |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`inertia_orientation<class_GLTFPhysicsBody_property_inertia_orientation>` | ``Quaternion(0, 0, 0, 1)``           |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`inertia_tensor<class_GLTFPhysicsBody_property_inertia_tensor>`           | ``Basis(0, 0, 0, 0, 0, 0, 0, 0, 0)`` |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`linear_velocity<class_GLTFPhysicsBody_property_linear_velocity>`         | ``Vector3(0, 0, 0)``                 |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`           | :ref:`mass<class_GLTFPhysicsBody_property_mass>`                               | ``1.0``                              |
   +-------------------------------------+--------------------------------------------------------------------------------+--------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFPhysicsBody<class_GLTFPhysicsBody>`     | :ref:`from_dictionary<class_GLTFPhysicsBody_method_from_dictionary>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static|  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFPhysicsBody<class_GLTFPhysicsBody>`     | :ref:`from_node<class_GLTFPhysicsBody_method_from_node>`\ (\ body_node\: :ref:`CollisionObject3D<class_CollisionObject3D>`\ ) |static| |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`to_dictionary<class_GLTFPhysicsBody_method_to_dictionary>`\ (\ ) |const|                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`CollisionObject3D<class_CollisionObject3D>` | :ref:`to_node<class_GLTFPhysicsBody_method_to_node>`\ (\ ) |const|                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_GLTFPhysicsBody_property_angular_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **angular_velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_GLTFPhysicsBody_property_angular_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_angular_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_angular_velocity**\ (\ )

Vận tốc góc của physics body, tính bằng radian trên giây. Giá trị này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle".

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_body_type:

.. rst-class:: classref-property

:ref:`String<class_String>` **body_type** = ``"rigid"`` :ref:`🔗<class_GLTFPhysicsBody_property_body_type>`

.. rst-class:: classref-property-setget

- |void| **set_body_type**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_body_type**\ (\ )

Kiểu của body.

Khi import, thuộc tính này kiểm soát kiểu node :ref:`CollisionObject3D<class_CollisionObject3D>` mà Godot sẽ tạo. Các giá trị hợp lệ là ``"static"``, ``"animatable"``, ``"character"``, ``"rigid"``, ``"vehicle"`` và ``"trigger"``.

Khi export, thuộc tính này sẽ được rút gọn thành một trong các kiểu chuyển động ``"static"``, ``"kinematic"`` hoặc ``"dynamic"``, hoặc thuộc tính ``"trigger"``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_center_of_mass:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **center_of_mass** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_GLTFPhysicsBody_property_center_of_mass>`

.. rst-class:: classref-property-setget

- |void| **set_center_of_mass**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_center_of_mass**\ (\ )

Tâm khối của body, tính bằng mét. Giá trị này nằm trong không gian cục bộ, tương đối so với body. Theo mặc định, tâm khối nằm tại gốc của body.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_inertia_diagonal:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **inertia_diagonal** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_GLTFPhysicsBody_property_inertia_diagonal>`

.. rst-class:: classref-property-setget

- |void| **set_inertia_diagonal**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_inertia_diagonal**\ (\ )

Độ lớn quán tính của physics body, tính bằng kilogram mét bình phương (kg⋅m²). Giá trị này biểu diễn quán tính quanh các trục chính, tức đường chéo của ma trận tensor quán tính. Giá trị này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle".

Khi được chuyển đổi thành node :ref:`RigidBody3D<class_RigidBody3D>` của Godot, nếu giá trị này bằng 0 thì quán tính sẽ được tự động tính toán.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_inertia_orientation:

.. rst-class:: classref-property

:ref:`Quaternion<class_Quaternion>` **inertia_orientation** = ``Quaternion(0, 0, 0, 1)`` :ref:`🔗<class_GLTFPhysicsBody_property_inertia_orientation>`

.. rst-class:: classref-property-setget

- |void| **set_inertia_orientation**\ (\ value\: :ref:`Quaternion<class_Quaternion>`\ ) - :ref:`Quaternion<class_Quaternion>` **get_inertia_orientation**\ (\ )

Hướng quán tính của physics body. Thuộc tính này xác định phép xoay của các trục chính của quán tính so với các trục cục bộ của đối tượng. Thuộc tính này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle" và :ref:`inertia_diagonal<class_GLTFPhysicsBody_property_inertia_diagonal>` được đặt thành giá trị khác 0.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_inertia_tensor:

.. rst-class:: classref-property

:ref:`Basis<class_Basis>` **inertia_tensor** = ``Basis(0, 0, 0, 0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_GLTFPhysicsBody_property_inertia_tensor>`

.. rst-class:: classref-property-setget

- |void| **set_inertia_tensor**\ (\ value\: :ref:`Basis<class_Basis>`\ ) - :ref:`Basis<class_Basis>` **get_inertia_tensor**\ (\ )

**Đã lỗi thời:** Property này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Tensor quán tính của physics body, tính bằng kilogram mét bình phương (kg⋅m²). Giá trị này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle".

Khi được chuyển đổi thành node :ref:`RigidBody3D<class_RigidBody3D>` của Godot, nếu giá trị này bằng 0 thì quán tính sẽ được tự động tính toán.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_linear_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **linear_velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_GLTFPhysicsBody_property_linear_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_linear_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_linear_velocity**\ (\ )

Vận tốc tuyến tính của physics body, tính bằng mét trên giây. Giá trị này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle".

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_property_mass:

.. rst-class:: classref-property

:ref:`float<class_float>` **mass** = ``1.0`` :ref:`🔗<class_GLTFPhysicsBody_property_mass>`

.. rst-class:: classref-property-setget

- |void| **set_mass**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mass**\ (\ )

Khối lượng của physics body, tính bằng kilogram. Giá trị này chỉ được sử dụng khi kiểu body là "rigid" hoặc "vehicle".

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_GLTFPhysicsBody_method_from_dictionary:

.. rst-class:: classref-method

:ref:`GLTFPhysicsBody<class_GLTFPhysicsBody>` **from_dictionary**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| :ref:`🔗<class_GLTFPhysicsBody_method_from_dictionary>`

Tạo một instance GLTFPhysicsBody mới bằng cách phân tích :ref:`Dictionary<class_Dictionary>` đã cho theo định dạng glTF extension ``OMI_physics_body``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_method_from_node:

.. rst-class:: classref-method

:ref:`GLTFPhysicsBody<class_GLTFPhysicsBody>` **from_node**\ (\ body_node\: :ref:`CollisionObject3D<class_CollisionObject3D>`\ ) |static| :ref:`🔗<class_GLTFPhysicsBody_method_from_node>`

Tạo một instance GLTFPhysicsBody mới từ node :ref:`CollisionObject3D<class_CollisionObject3D>` của Godot đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_method_to_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **to_dictionary**\ (\ ) |const| :ref:`🔗<class_GLTFPhysicsBody_method_to_dictionary>`

Tuần tự hóa instance GLTFPhysicsBody này thành một :ref:`Dictionary<class_Dictionary>`. Dữ liệu sẽ ở định dạng mà glTF extension ``OMI_physics_body`` mong đợi.

.. rst-class:: classref-item-separator

----

.. _class_GLTFPhysicsBody_method_to_node:

.. rst-class:: classref-method

:ref:`CollisionObject3D<class_CollisionObject3D>` **to_node**\ (\ ) |const| :ref:`🔗<class_GLTFPhysicsBody_method_to_node>`

Chuyển đổi instance GLTFPhysicsBody này thành một node :ref:`CollisionObject3D<class_CollisionObject3D>` của Godot.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
