:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRAnchorTracker.xml.

.. _class_OpenXRAnchorTracker:

OpenXRAnchorTracker
===================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialEntityTracker<class_OpenXRSpatialEntityTracker>` **<** :ref:`XRPositionalTracker<class_XRPositionalTracker>` **<** :ref:`XRTracker<class_XRTracker>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Bộ theo dõi vị trí cho extension neo thực thể không gian của chúng ta.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bộ theo dõi vị trí cho extension neo thực thể không gian OpenXR của chúng ta; nó theo dõi một vị trí do người dùng xác định trong không gian thực và ánh xạ vị trí đó vào không gian ảo của chúng ta.

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------+------------------------------------------------------+--------+
   | :ref:`String<class_String>` | :ref:`uuid<class_OpenXRAnchorTracker_property_uuid>` | ``""`` |
   +-----------------------------+------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`has_uuid<class_OpenXRAnchorTracker_method_has_uuid>`\ (\ ) |const| |
   +-------------------------+--------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_OpenXRAnchorTracker_signal_uuid_changed:

.. rst-class:: classref-signal

**uuid_changed**\ (\ ) :ref:`🔗<class_OpenXRAnchorTracker_signal_uuid_changed>`

Được phát ra khi UUID của neo này thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRAnchorTracker_property_uuid:

.. rst-class:: classref-property

:ref:`String<class_String>` **uuid** = ``""`` :ref:`🔗<class_OpenXRAnchorTracker_property_uuid>`

.. rst-class:: classref-property-setget

- |void| **set_uuid**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_uuid**\ (\ )

UUID được cung cấp cho các neo persistent.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRAnchorTracker_method_has_uuid:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_uuid**\ (\ ) |const| :ref:`🔗<class_OpenXRAnchorTracker_method_has_uuid>`

Trả về ``true`` nếu đã thiết lập UUID khác không.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
