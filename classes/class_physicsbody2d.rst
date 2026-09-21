:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsBody2D.xml.

.. _class_PhysicsBody2D:

PhysicsBody2D
=============

**Kế thừa:** :ref:`CollisionObject2D<class_CollisionObject2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CharacterBody2D<class_CharacterBody2D>`, :ref:`RigidBody2D<class_RigidBody2D>`, :ref:`StaticBody2D<class_StaticBody2D>`

Lớp cơ sở trừu tượng cho các đối tượng game 2D chịu tác động của physics.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PhysicsBody2D** là lớp cơ sở trừu tượng cho các đối tượng game 2D chịu tác động của physics. Tất cả physics body 2D đều kế thừa từ lớp này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Giới thiệu về physics <../tutorials/physics/physics_introduction>`

- :doc:`Khắc phục sự cố physics <../tutorials/physics/troubleshooting_physics_issues>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+----------------+-------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | input_pickable | ``false`` (overrides :ref:`CollisionObject2D<class_CollisionObject2D_property_input_pickable>`) |
   +-------------------------+----------------+-------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                 | :ref:`add_collision_exception_with<class_PhysicsBody2D_method_add_collision_exception_with>`\ (\ body\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                      |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PhysicsBody2D<class_PhysicsBody2D>`\] | :ref:`get_collision_exceptions<class_PhysicsBody2D_method_get_collision_exceptions>`\ (\ )                                                                                                                                                                                                                                              |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                          | :ref:`get_gravity<class_PhysicsBody2D_method_get_gravity>`\ (\ ) |const|                                                                                                                                                                                                                                                                |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`KinematicCollision2D<class_KinematicCollision2D>`                | :ref:`move_and_collide<class_PhysicsBody2D_method_move_and_collide>`\ (\ motion\: :ref:`Vector2<class_Vector2>`, test_only\: :ref:`bool<class_bool>` = false, safe_margin\: :ref:`float<class_float>` = 0.08, recovery_as_collision\: :ref:`bool<class_bool>` = false\ )                                                                |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                 | :ref:`remove_collision_exception_with<class_PhysicsBody2D_method_remove_collision_exception_with>`\ (\ body\: :ref:`Node<class_Node>`\ )                                                                                                                                                                                                |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                | :ref:`test_move<class_PhysicsBody2D_method_test_move>`\ (\ from\: :ref:`Transform2D<class_Transform2D>`, motion\: :ref:`Vector2<class_Vector2>`, collision\: :ref:`KinematicCollision2D<class_KinematicCollision2D>` = null, safe_margin\: :ref:`float<class_float>` = 0.08, recovery_as_collision\: :ref:`bool<class_bool>` = false\ ) |
   +------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicsBody2D_method_add_collision_exception_with:

.. rst-class:: classref-method

|void| **add_collision_exception_with**\ (\ body\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_PhysicsBody2D_method_add_collision_exception_with>`

Thêm một body vào danh sách các body mà body này không thể va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody2D_method_get_collision_exceptions:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PhysicsBody2D<class_PhysicsBody2D>`\] **get_collision_exceptions**\ (\ ) :ref:`🔗<class_PhysicsBody2D_method_get_collision_exceptions>`

Trả về một mảng các node đã được thêm làm ngoại lệ va chạm cho body này.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody2D_method_get_gravity:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_gravity**\ (\ ) |const| :ref:`🔗<class_PhysicsBody2D_method_get_gravity>`

Trả về vector trọng lực được tính toán từ tất cả các nguồn có thể tác động đến body, bao gồm mọi gravity override từ các node :ref:`Area2D<class_Area2D>` và trọng lực toàn cục của world.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody2D_method_move_and_collide:

.. rst-class:: classref-method

:ref:`KinematicCollision2D<class_KinematicCollision2D>` **move_and_collide**\ (\ motion\: :ref:`Vector2<class_Vector2>`, test_only\: :ref:`bool<class_bool>` = false, safe_margin\: :ref:`float<class_float>` = 0.08, recovery_as_collision\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PhysicsBody2D_method_move_and_collide>`

Di chuyển body dọc theo vector ``motion``. Để độc lập với frame rate trong :ref:`Node._physics_process()<class_Node_private_method__physics_process>` hoặc :ref:`Node._process()<class_Node_private_method__process>`, ``motion`` nên được tính bằng ``delta``.

Trả về một :ref:`KinematicCollision2D<class_KinematicCollision2D>`, chứa thông tin về va chạm khi dừng lại hoặc khi chạm vào một body khác trong quá trình di chuyển.

Nếu ``test_only`` là ``true``, body không di chuyển nhưng thông tin về va chạm có thể xảy ra vẫn được cung cấp.

\ ``safe_margin`` là khoảng đệm bổ sung được sử dụng cho việc phục hồi sau va chạm (xem :ref:`CharacterBody2D.safe_margin<class_CharacterBody2D_property_safe_margin>` để biết thêm chi tiết).

Nếu ``recovery_as_collision`` là ``true``, mọi quá trình depenetration trong giai đoạn phục hồi cũng được báo cáo là một va chạm; điều này được :ref:`CharacterBody2D<class_CharacterBody2D>` sử dụng, chẳng hạn, để cải thiện việc phát hiện sàn trong quá trình floor snapping.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody2D_method_remove_collision_exception_with:

.. rst-class:: classref-method

|void| **remove_collision_exception_with**\ (\ body\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_PhysicsBody2D_method_remove_collision_exception_with>`

Xóa một body khỏi danh sách các body mà body này không thể va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsBody2D_method_test_move:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **test_move**\ (\ from\: :ref:`Transform2D<class_Transform2D>`, motion\: :ref:`Vector2<class_Vector2>`, collision\: :ref:`KinematicCollision2D<class_KinematicCollision2D>` = null, safe_margin\: :ref:`float<class_float>` = 0.08, recovery_as_collision\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PhysicsBody2D_method_test_move>`

Kiểm tra va chạm mà không di chuyển body. Để độc lập với frame rate trong :ref:`Node._physics_process()<class_Node_private_method__physics_process>` hoặc :ref:`Node._process()<class_Node_private_method__process>`, ``motion`` nên được tính bằng ``delta``.

Đặt ảo vị trí, scale và rotation của node thành các giá trị của :ref:`Transform2D<class_Transform2D>` đã cho, sau đó cố gắng di chuyển body dọc theo vector ``motion``. Trả về ``true`` nếu một va chạm có thể khiến body không di chuyển được hết quãng đường.

\ ``collision`` là một object tùy chọn thuộc kiểu :ref:`KinematicCollision2D<class_KinematicCollision2D>`, chứa thêm thông tin về va chạm khi dừng lại hoặc khi chạm vào một body khác trong quá trình di chuyển.

\ ``safe_margin`` là khoảng đệm bổ sung được sử dụng cho việc phục hồi sau va chạm (xem :ref:`CharacterBody2D.safe_margin<class_CharacterBody2D_property_safe_margin>` để biết thêm chi tiết).

Nếu ``recovery_as_collision`` là ``true``, mọi quá trình depenetration trong giai đoạn phục hồi cũng được báo cáo là một va chạm; điều này hữu ích để kiểm tra xem body có *chạm* vào body nào khác hay không.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
