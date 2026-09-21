:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/JavaClass.xml.

.. _class_JavaClass:

JavaClass
=========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một lớp từ Java Native Interface.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một lớp từ Java Native Interface. Được trả về từ :ref:`JavaClassWrapper.wrap()<class_JavaClassWrapper_method_wrap>`.

\ **Lưu ý:** Lớp này chỉ hoạt động trên Android. Trên mọi nền tảng khác, lớp này không thực hiện tác vụ nào.

\ **Lưu ý:** Không được nhầm lẫn lớp này với :ref:`JavaScriptObject<class_JavaScriptObject>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`get_java_class_name<class_JavaClass_method_get_java_class_name>`\ (\ ) |const|                                       |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_java_method_list<class_JavaClass_method_get_java_method_list>`\ (\ ) |const|                                     |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaClass<class_JavaClass>`                                | :ref:`get_java_parent_class<class_JavaClass_method_get_java_parent_class>`\ (\ ) |const|                                   |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_java_method<class_JavaClass_method_has_java_method>`\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_JavaClass_method_get_java_class_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_java_class_name**\ (\ ) |const| :ref:`🔗<class_JavaClass_method_get_java_class_name>`

Trả về tên lớp Java.

.. rst-class:: classref-item-separator

----

.. _class_JavaClass_method_get_java_method_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_java_method_list**\ (\ ) |const| :ref:`🔗<class_JavaClass_method_get_java_method_list>`

Trả về các phương thức Java của đối tượng và chữ ký của chúng dưới dạng :ref:`Array<class_Array>` chứa các dictionary, theo cùng định dạng như :ref:`Object.get_method_list()<class_Object_method_get_method_list>`.

.. rst-class:: classref-item-separator

----

.. _class_JavaClass_method_get_java_parent_class:

.. rst-class:: classref-method

:ref:`JavaClass<class_JavaClass>` **get_java_parent_class**\ (\ ) |const| :ref:`🔗<class_JavaClass_method_get_java_parent_class>`

Trả về một **JavaClass** đại diện cho lớp Java cha của lớp này.

.. rst-class:: classref-item-separator

----

.. _class_JavaClass_method_has_java_method:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_java_method**\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_JavaClass_method_has_java_method>`

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
