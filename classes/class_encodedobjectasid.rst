:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EncodedObjectAsID.xml.

.. _class_EncodedObjectAsID:

EncodedObjectAsID
=================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lưu tham chiếu đến instance ID của :ref:`Object<class_Object>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp tiện ích lưu tham chiếu đến mã định danh nội bộ của một instance :ref:`Object<class_Object>`, được cung cấp bởi :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`. Sau đó, ID này có thể được sử dụng để truy xuất instance đối tượng bằng :ref:`@GlobalScope.instance_from_id()<class_@GlobalScope_method_instance_from_id>`.

Lớp này được editor inspector và script debugger sử dụng nội bộ, nhưng cũng có thể được dùng trong các plugin để truyền và hiển thị các đối tượng dưới dạng ID của chúng.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`object_id<class_EncodedObjectAsID_property_object_id>` | ``0`` |
   +-----------------------+--------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EncodedObjectAsID_property_object_id:

.. rst-class:: classref-property

:ref:`int<class_int>` **object_id** = ``0`` :ref:`🔗<class_EncodedObjectAsID_property_object_id>`

.. rst-class:: classref-property-setget

- |void| **set_object_id**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_object_id**\ (\ )

Mã định danh :ref:`Object<class_Object>` được lưu trong instance **EncodedObjectAsID** này. Instance đối tượng có thể được truy xuất bằng :ref:`@GlobalScope.instance_from_id()<class_@GlobalScope_method_instance_from_id>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
