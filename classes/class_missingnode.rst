:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MissingNode.xml.

.. _class_MissingNode:

MissingNode
===========

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một editor class nội bộ dùng để lưu dữ liệu của các node không được nhận dạng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một editor class nội bộ dùng để lưu dữ liệu của các node thuộc kiểu không xác định (rất có thể kiểu này được cung cấp bởi một extension hiện không còn được load). Không thể khởi tạo hoặc đặt nó vào scene theo cách thủ công.

\ **Cảnh báo:** Không nên quan tâm đến các node bị thiếu trừ khi bạn biết rõ mình đang làm gì. Các thuộc tính hiện có trên một node bị thiếu có thể được tự do sửa đổi trong code, bất kể kiểu mà chúng được dự định sử dụng.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`original_class<class_MissingNode_property_original_class>`             |
   +-----------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`original_scene<class_MissingNode_property_original_scene>`             |
   +-----------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`recording_properties<class_MissingNode_property_recording_properties>` |
   +-----------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`recording_signals<class_MissingNode_property_recording_signals>`       |
   +-----------------------------+------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MissingNode_property_original_class:

.. rst-class:: classref-property

:ref:`String<class_String>` **original_class** :ref:`🔗<class_MissingNode_property_original_class>`

.. rst-class:: classref-property-setget

- |void| **set_original_class**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_original_class**\ (\ )

Tên của class mà node này đáng lẽ phải thuộc về (xem :ref:`Object.get_class()<class_Object_method_get_class>`).

.. rst-class:: classref-item-separator

----

.. _class_MissingNode_property_original_scene:

.. rst-class:: classref-property

:ref:`String<class_String>` **original_scene** :ref:`🔗<class_MissingNode_property_original_scene>`

.. rst-class:: classref-property-setget

- |void| **set_original_scene**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_original_scene**\ (\ )

Trả về đường dẫn của scene mà node này ban đầu là một instance.

.. rst-class:: classref-item-separator

----

.. _class_MissingNode_property_recording_properties:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recording_properties** :ref:`🔗<class_MissingNode_property_recording_properties>`

.. rst-class:: classref-property-setget

- |void| **set_recording_properties**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_recording_properties**\ (\ )

Nếu ``true``, cho phép thiết lập các thuộc tính mới cùng với các thuộc tính hiện có. Nếu ``false``, chỉ có thể thiết lập giá trị của các thuộc tính hiện có và không thể thêm thuộc tính mới.

.. rst-class:: classref-item-separator

----

.. _class_MissingNode_property_recording_signals:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recording_signals** :ref:`🔗<class_MissingNode_property_recording_signals>`

.. rst-class:: classref-property-setget

- |void| **set_recording_signals**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_recording_signals**\ (\ )

Nếu ``true``, cho phép kết nối các signal mới cùng với các signal hiện có. Nếu ``false``, chỉ có thể kết nối các signal hiện có và không thể thêm signal mới.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
