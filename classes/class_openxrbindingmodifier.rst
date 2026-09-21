:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRBindingModifier.xml.

.. _class_OpenXRBindingModifier:

OpenXRBindingModifier
=====================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`OpenXRActionBindingModifier<class_OpenXRActionBindingModifier>`, :ref:`OpenXRIPBindingModifier<class_OpenXRIPBindingModifier>`

Lớp cơ sở của binding modifier.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở của binding modifier. Các lớp con triển khai nhiều modifier khác nhau để thay đổi cách OpenXR runtime xử lý các input.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`_get_description<class_OpenXRBindingModifier_private_method__get_description>`\ (\ ) |virtual| |required| |const| |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`_get_ip_modification<class_OpenXRBindingModifier_private_method__get_ip_modification>`\ (\ ) |virtual| |required| |
   +-----------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRBindingModifier_private_method__get_description:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_description**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_OpenXRBindingModifier_private_method__get_description>`

Trả về phần mô tả của lớp này, được dùng làm thanh tiêu đề của trình chỉnh sửa binding modifier.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRBindingModifier_private_method__get_ip_modification:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **_get_ip_modification**\ (\ ) |virtual| |required| :ref:`🔗<class_OpenXRBindingModifier_private_method__get_ip_modification>`

Trả về dữ liệu được gửi đến OpenXR khi gửi các binding tương tác được đề xuất mà modifier này là một phần trong đó.

\ **Lưu ý:** Đây phải là dữ liệu tương thích với cấu trúc ``XrBindingModificationBaseHeaderKHR``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
