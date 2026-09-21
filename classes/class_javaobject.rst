:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/JavaObject.xml.

.. _class_JavaObject:

JavaObject
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một đối tượng từ Java Native Interface.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một đối tượng từ Java Native Interface. Đối tượng này có thể được trả về từ các phương thức Java được gọi trên :ref:`JavaClass<class_JavaClass>` hoặc các **JavaObject**\ s khác. Xem :ref:`JavaClassWrapper<class_JavaClassWrapper>` để biết ví dụ.

\ **Lưu ý:** Lớp này chỉ hoạt động trên Android. Trên mọi nền tảng khác, lớp này không thực hiện thao tác nào.

\ **Lưu ý:** Không được nhầm lẫn lớp này với :ref:`JavaScriptObject<class_JavaScriptObject>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaClass<class_JavaClass>` | :ref:`get_java_class<class_JavaObject_method_get_java_class>`\ (\ ) |const|                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`           | :ref:`has_java_method<class_JavaObject_method_has_java_method>`\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_JavaObject_method_get_java_class:

.. rst-class:: classref-method

:ref:`JavaClass<class_JavaClass>` **get_java_class**\ (\ ) |const| :ref:`🔗<class_JavaObject_method_get_java_class>`

Trả về :ref:`JavaClass<class_JavaClass>` mà đối tượng này là một instance của nó.

.. rst-class:: classref-item-separator

----

.. _class_JavaObject_method_has_java_method:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_java_method**\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_JavaObject_method_has_java_method>`

Trả về ``true`` nếu tên ``method`` đã cho tồn tại trong các phương thức Java của đối tượng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
