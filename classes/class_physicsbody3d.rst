:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsBody3D.xml.

.. _class_PhysicsBody3D:

PhysicsBody3D
=============

**Kế thừa:** :ref:`CollisionObject3D<class_CollisionObject3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CharacterBody3D<class_CharacterBody3D>`, :ref:`PhysicalBone3D<class_PhysicalBone3D>`, :ref:`RigidBody3D<class_RigidBody3D>`, :ref:`StaticBody3D<class_StaticBody3D>`

Lớp cơ sở trừu tượng cho các đối tượng game 3D chịu ảnh hưởng của vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PhysicsBody3D** là lớp cơ sở trừu tượng cho các đối tượng game 3D chịu ảnh hưởng của vật lý. Tất cả các physics body 3D đều kế thừa từ lớp này.

\ **Cảnh báo:** Với scale không đồng nhất, node này có thể sẽ không hoạt động như mong đợi. Bạn nên giữ scale giống nhau trên tất cả các trục và thay vào đó điều chỉnh các collision shape của nó.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Giới thiệu về vật lý <../tutorials/physics/physics_introduction>`

- :doc:`Khắc phục sự cố vật lý <../tutorials/physics/troubleshooting_physics_issues>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_angular_x<class_PhysicsBody3D_property_axis_lock_angular_x>` | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_angular_y<class_PhysicsBody3D_property_axis_lock_angular_y>` | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_angular_z<class_PhysicsBody3D_property_axis_lock_angular_z>` | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_linear_x<class_PhysicsBody3D_property_axis_lock_linear_x>`   | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_linear_y<class_PhysicsBody3D_property_axis_lock_linear_y>`   | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`axis_lock_linear_z<class_PhysicsBody3D_property_axis_lock_linear_z>`   | ``false`` |
   +-------------------------+------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                 | :ref:`add_collision_exception_with<class_PhysicsBody3D_method_add_collision_exception_with>`\ (\ body\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                                                                   |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                | :ref:`get_axis_lock<class_PhysicsBody3D_method_get_axis_lock>`\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PhysicsBody3D<class_PhysicsBody3D>`\] | :ref:`get_collision_exceptions<class_PhysicsBody3D_method_get_collision_exceptions>`\ (\ )                                                                                                                                                                                                                                                                                           |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                          | :ref:`get_gravity<class_PhysicsBody3D_method_get_gravity>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                             |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`KinematicCollision3D<class_KinematicCollision3D>`                | :ref:`move_and_collide<class_PhysicsBody3D_method_move_and_collide>`\ (\ motion\: :ref:`Vector3<class_Vector3>`, test_only\: :ref:`bool<class_bool>` = false, safe_margin\: :ref:`float<class_float>` = 0.001, recovery_as_collision\: :ref:`bool<class_bool>` = false, max_collisions\: :ref:`int<class_int>` = 1\ )                                                                |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                 | :ref:`remove_collision_exception_with<class_PhysicsBody3D_method_remove_collision_exception_with>`\ (\ body\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                                                             |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                 | :ref:`set_axis_lock<class_PhysicsBody3D_method_set_axis_lock>`\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ )                                                                                                                                                                                                                          |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                | :ref:`test_move<class_PhysicsBody3D_method_test_move>`\ (\ from\: :ref:`Transform3D<class_Transform3D>`, motion\: :ref:`Vector3<class_Vector3>`, collision\: :ref:`KinematicCollision3D<class_KinematicCollision3D>` = null, safe_margin\: :ref:`float<class_float>` = 0.001, recovery_as_collision\: :ref:`bool<class_bool>` = false, max_collisions\: :ref:`int<class_int>` = 1\ ) |
   +------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsBody3D_property_axis_lock_angular_x:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_angular_x** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_angular_x>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động xoay của body trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_property_axis_lock_angular_y:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_angular_y** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_angular_y>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động xoay của body trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_property_axis_lock_angular_z:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_angular_z** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_angular_z>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động xoay của body trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_property_axis_lock_linear_x:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_linear_x** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_linear_x>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động tịnh tiến của body trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_property_axis_lock_linear_y:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_linear_y** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_linear_y>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động tịnh tiến của body trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_property_axis_lock_linear_z:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **axis_lock_linear_z** = ``false`` :ref:`🔗<class_PhysicsBody3D_property_axis_lock_linear_z>`

.. rst-class:: classref-property-setget

- |void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const|

Khóa chuyển động tịnh tiến của body trên trục Z.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicsBody3D_method_add_collision_exception_with:

.. rst-class:: classref-method

|void| **add_collision_exception_with**\ (\ body\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_PhysicsBody3D_method_add_collision_exception_with>`

Thêm một body vào danh sách các body mà body này không thể va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_get_axis_lock:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`\ ) |const| :ref:`🔗<class_PhysicsBody3D_method_get_axis_lock>`

Trả về ``true`` nếu ``axis`` tịnh tiến hoặc xoay được chỉ định đang bị khóa.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_get_collision_exceptions:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PhysicsBody3D<class_PhysicsBody3D>`\] **get_collision_exceptions**\ (\ ) :ref:`🔗<class_PhysicsBody3D_method_get_collision_exceptions>`

Trả về một mảng các node được thêm làm ngoại lệ va chạm cho body này.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_get_gravity:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_gravity**\ (\ ) |const| :ref:`🔗<class_PhysicsBody3D_method_get_gravity>`

Trả về vector trọng lực được tính toán từ tất cả các nguồn có thể ảnh hưởng đến body, bao gồm tất cả các gravity override từ các node :ref:`Area3D<class_Area3D>` và trọng lực toàn cục của thế giới.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_move_and_collide:

.. rst-class:: classref-method

:ref:`KinematicCollision3D<class_KinematicCollision3D>` **move_and_collide**\ (\ motion\: :ref:`Vector3<class_Vector3>`, test_only\: :ref:`bool<class_bool>` = false, safe_margin\: :ref:`float<class_float>` = 0.001, recovery_as_collision\: :ref:`bool<class_bool>` = false, max_collisions\: :ref:`int<class_int>` = 1\ ) :ref:`🔗<class_PhysicsBody3D_method_move_and_collide>`

Di chuyển body theo vector ``motion``. Để không phụ thuộc vào frame rate trong :ref:`Node._physics_process()<class_Node_private_method__physics_process>` hoặc :ref:`Node._process()<class_Node_private_method__process>`, cần tính ``motion`` bằng ``delta``.

Body sẽ dừng lại nếu va chạm. Trả về một :ref:`KinematicCollision3D<class_KinematicCollision3D>`, chứa thông tin về va chạm khi body dừng lại hoặc khi chạm vào một body khác trong quá trình di chuyển.

Nếu ``test_only`` là ``true``, body sẽ không di chuyển nhưng thông tin về va chạm có thể xảy ra sẽ được cung cấp.

\ ``safe_margin`` là khoảng cách bổ sung được dùng để phục hồi sau va chạm (xem :ref:`CharacterBody3D.safe_margin<class_CharacterBody3D_property_safe_margin>` để biết thêm chi tiết).

Nếu ``recovery_as_collision`` là ``true``, mọi quá trình tách xuyên từ giai đoạn phục hồi cũng được báo cáo như một va chạm; điều này được :ref:`CharacterBody3D<class_CharacterBody3D>` sử dụng, chẳng hạn, để cải thiện việc phát hiện sàn trong quá trình floor snapping.

\ ``max_collisions`` cho phép truy xuất nhiều hơn một kết quả va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_remove_collision_exception_with:

.. rst-class:: classref-method

|void| **remove_collision_exception_with**\ (\ body\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_PhysicsBody3D_method_remove_collision_exception_with>`

Xóa một body khỏi danh sách các body mà body này không thể va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_set_axis_lock:

.. rst-class:: classref-method

|void| **set_axis_lock**\ (\ axis\: :ref:`BodyAxis<enum_PhysicsServer3D_BodyAxis>`, lock\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_PhysicsBody3D_method_set_axis_lock>`

Khóa hoặc mở khóa ``axis`` tịnh tiến hoặc xoay được chỉ định, tùy thuộc vào giá trị của ``lock``.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody3D_method_test_move:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **test_move**\ (\ from\: :ref:`Transform3D<class_Transform3D>`, motion\: :ref:`Vector3<class_Vector3>`, collision\: :ref:`KinematicCollision3D<class_KinematicCollision3D>` = null, safe_margin\: :ref:`float<class_float>` = 0.001, recovery_as_collision\: :ref:`bool<class_bool>` = false, max_collisions\: :ref:`int<class_int>` = 1\ ) :ref:`🔗<class_PhysicsBody3D_method_test_move>`

Kiểm tra va chạm mà không di chuyển body. Để không phụ thuộc vào frame rate trong :ref:`Node._physics_process()<class_Node_private_method__physics_process>` hoặc :ref:`Node._process()<class_Node_private_method__process>`, cần tính ``motion`` bằng ``delta``.

Thiết lập ảo vị trí, scale và rotation của node theo :ref:`Transform3D<class_Transform3D>` đã cho, sau đó thử di chuyển body theo vector ``motion``. Trả về ``true`` nếu một va chạm sẽ khiến body không thể di chuyển hết toàn bộ đường đi.

\ ``collision`` là một object tùy chọn thuộc kiểu :ref:`KinematicCollision3D<class_KinematicCollision3D>`, chứa thông tin bổ sung về va chạm khi dừng lại hoặc khi chạm vào một body khác trong quá trình di chuyển.

\ ``safe_margin`` là khoảng cách bổ sung được dùng để phục hồi sau va chạm (xem :ref:`CharacterBody3D.safe_margin<class_CharacterBody3D_property_safe_margin>` để biết thêm chi tiết).

Nếu ``recovery_as_collision`` là ``true``, mọi quá trình tách xuyên từ giai đoạn phục hồi cũng được báo cáo như một va chạm; điều này hữu ích để kiểm tra xem body có *chạm* vào bất kỳ body nào khác hay không.

\ ``max_collisions`` cho phép truy xuất nhiều hơn một kết quả va chạm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
