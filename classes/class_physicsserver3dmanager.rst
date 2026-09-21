:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsServer3DManager.xml.

.. _class_PhysicsServer3DManager:

PhysicsServer3DManager
======================

**Kế thừa:** :ref:`Object<class_Object>`

Một singleton dùng để quản lý các triển khai :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PhysicsServer3DManager** là API dùng để đăng ký các triển khai :ref:`PhysicsServer3D<class_PhysicsServer3D>` và thiết lập triển khai mặc định.

\ **Lưu ý:** Không thể chuyển đổi physics server trong runtime. Class này chỉ được Godot sử dụng khi khởi động, ở cấp độ khởi tạo server, và có thể được các GDExtensions sử dụng.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`register_server<class_PhysicsServer3DManager_method_register_server>`\ (\ name\: :ref:`String<class_String>`, create_callback\: :ref:`Callable<class_Callable>`\ ) |
   +--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`set_default_server<class_PhysicsServer3DManager_method_set_default_server>`\ (\ name\: :ref:`String<class_String>`, priority\: :ref:`int<class_int>`\ )            |
   +--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicsServer3DManager_method_register_server:

.. rst-class:: classref-method

|void| **register_server**\ (\ name\: :ref:`String<class_String>`, create_callback\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_PhysicsServer3DManager_method_register_server>`

Đăng ký một triển khai :ref:`PhysicsServer3D<class_PhysicsServer3D>` bằng cách truyền vào một ``name`` và một :ref:`Callable<class_Callable>` trả về một đối tượng :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsServer3DManager_method_set_default_server:

.. rst-class:: classref-method

|void| **set_default_server**\ (\ name\: :ref:`String<class_String>`, priority\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PhysicsServer3DManager_method_set_default_server>`

Đặt triển khai :ref:`PhysicsServer3D<class_PhysicsServer3D>` mặc định thành triển khai được xác định bởi ``name``, nếu ``priority`` lớn hơn priority của triển khai mặc định hiện tại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
