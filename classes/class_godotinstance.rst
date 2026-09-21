:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GodotInstance.xml.

.. _class_GodotInstance:

GodotInstance
=============

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào một Godot instance được nhúng.

.. rst-class:: classref-introduction-group

Mô tả
-----

GodotInstance đại diện cho một Godot instance đang chạy, được điều khiển từ một codebase bên ngoài mà không cần main loop chạy liên tục. Nó được tạo bởi C API ``libgodot_create_godot_instance``. Mỗi process chỉ có thể tạo một instance.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------+
   | |void|                  | :ref:`focus_in<class_GodotInstance_method_focus_in>`\ (\ )     |
   +-------------------------+----------------------------------------------------------------+
   | |void|                  | :ref:`focus_out<class_GodotInstance_method_focus_out>`\ (\ )   |
   +-------------------------+----------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_started<class_GodotInstance_method_is_started>`\ (\ ) |
   +-------------------------+----------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`iteration<class_GodotInstance_method_iteration>`\ (\ )   |
   +-------------------------+----------------------------------------------------------------+
   | |void|                  | :ref:`pause<class_GodotInstance_method_pause>`\ (\ )           |
   +-------------------------+----------------------------------------------------------------+
   | |void|                  | :ref:`resume<class_GodotInstance_method_resume>`\ (\ )         |
   +-------------------------+----------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`start<class_GodotInstance_method_start>`\ (\ )           |
   +-------------------------+----------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GodotInstance_method_focus_in:

.. rst-class:: classref-method

|void| **focus_in**\ (\ ) :ref:`🔗<class_GodotInstance_method_focus_in>`

Thông báo cho instance rằng hiện tại nó đang được focus.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_focus_out:

.. rst-class:: classref-method

|void| **focus_out**\ (\ ) :ref:`🔗<class_GodotInstance_method_focus_out>`

Thông báo cho instance rằng hiện tại nó không được focus.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_is_started:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_started**\ (\ ) :ref:`🔗<class_GodotInstance_method_is_started>`

Trả về ``true`` nếu instance này đã được khởi động hoàn toàn.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_iteration:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **iteration**\ (\ ) :ref:`🔗<class_GodotInstance_method_iteration>`

Chạy một iteration duy nhất của main loop. Trả về ``true`` nếu engine đang cố gắng thoát.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_pause:

.. rst-class:: classref-method

|void| **pause**\ (\ ) :ref:`🔗<class_GodotInstance_method_pause>`

Thông báo cho instance rằng nó sắp được tạm dừng.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_resume:

.. rst-class:: classref-method

|void| **resume**\ (\ ) :ref:`🔗<class_GodotInstance_method_resume>`

Thông báo cho instance rằng nó đang được tiếp tục.

.. rst-class:: classref-item-separator

----

.. _class_GodotInstance_method_start:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **start**\ (\ ) :ref:`🔗<class_GodotInstance_method_start>`

Hoàn tất chuỗi khởi động của instance này. Trả về ``true`` nếu thành công.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
