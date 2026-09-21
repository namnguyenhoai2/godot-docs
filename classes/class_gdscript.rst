:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gdscript/doc_classes/GDScript.xml.

.. _class_GDScript:

GDScript
========

**Kế thừa:** :ref:`Script<class_Script>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một script được triển khai bằng ngôn ngữ lập trình GDScript.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một script được triển khai bằng ngôn ngữ lập trình GDScript, được lưu với phần mở rộng ``.gd``. Script này mở rộng chức năng của tất cả các object khởi tạo nó.

Việc gọi :ref:`new()<class_GDScript_method_new>` sẽ tạo một instance mới của script. :ref:`Object.set_script()<class_Object_method_set_script>` mở rộng một object hiện có nếu class của object đó khớp với một trong các base class của script.

Nếu bạn đang tìm các hàm tích hợp sẵn của GDScript, hãy xem :ref:`@GDScript<class_@GDScript>` thay vào đó.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Mục lục tài liệu GDScript <../tutorials/scripting/gdscript/index>`

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`new<class_GDScript_method_new>`\ (\ ...\ ) |vararg| |
   +-------------------------------+-----------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GDScript_method_new:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **new**\ (\ ...\ ) |vararg| :ref:`🔗<class_GDScript_method_new>`

Trả về một instance mới của script.

::

    var MyClass = load("myclass.gd")
    var instance = MyClass.new()
    print(instance.get_script() == MyClass) # In ra true

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
