:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MissingResource.xml.

.. _class_MissingResource:

MissingResource
===============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một editor class nội bộ dùng để lưu dữ liệu của các resource không được nhận dạng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một editor class nội bộ dùng để lưu dữ liệu của các resource thuộc kiểu không xác định (rất có thể kiểu này được cung cấp bởi một extension hiện không còn được load). Không thể khởi tạo hoặc đặt nó vào scene theo cách thủ công.

\ **Cảnh báo:** Hãy bỏ qua các resource bị thiếu trừ khi bạn biết mình đang làm gì. Các property hiện có trên một resource bị thiếu có thể được tự do sửa đổi trong code, bất kể kiểu mà chúng được dự định sử dụng.

.. rst-class:: classref-reftable-group

Các property
------------

.. table::
   :widths: auto

   +-----------------------------+----------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`original_class<class_MissingResource_property_original_class>`             |
   +-----------------------------+----------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`recording_properties<class_MissingResource_property_recording_properties>` |
   +-----------------------------+----------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả property
--------------

.. _class_MissingResource_property_original_class:

.. rst-class:: classref-property

:ref:`String<class_String>` **original_class** :ref:`🔗<class_MissingResource_property_original_class>`

.. rst-class:: classref-property-setget

- |void| **set_original_class**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_original_class**\ (\ )

Tên của class mà resource này lẽ ra phải thuộc về (xem :ref:`Object.get_class()<class_Object_method_get_class>`).

.. rst-class:: classref-item-separator

----

.. _class_MissingResource_property_recording_properties:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recording_properties** :ref:`🔗<class_MissingResource_property_recording_properties>`

.. rst-class:: classref-property-setget

- |void| **set_recording_properties**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_recording_properties**\ (\ )

Nếu được đặt thành ``true``, cho phép thêm các property mới bên trên những property hiện có bằng :ref:`Object.set()<class_Object_method_set>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
