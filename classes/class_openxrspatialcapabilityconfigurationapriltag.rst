:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialCapabilityConfigurationAprilTag.xml.

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag:

OpenXRSpatialCapabilityConfigurationAprilTag
============================================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialCapabilityConfigurationBaseHeader<class_OpenXRSpatialCapabilityConfigurationBaseHeader>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Header cấu hình cho các marker thẻ April.

.. rst-class:: classref-introduction-group

Mô tả
-----

Header cấu hình cho các marker thẻ April. Truyền đối tượng này vào :ref:`OpenXRSpatialEntityExtension.create_spatial_context()<class_OpenXRSpatialEntityExtension_method_create_spatial_context>` để tạo một spatial context có thể phát hiện các thẻ April.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------+-------+
   | :ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` | :ref:`april_dict<class_OpenXRSpatialCapabilityConfigurationAprilTag_property_april_dict>` | ``4`` |
   +-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>` | :ref:`get_enabled_components<class_OpenXRSpatialCapabilityConfigurationAprilTag_method_get_enabled_components>`\ (\ ) |const| |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict:

.. rst-class:: classref-enumeration

enum **AprilTagDict**: :ref:`🔗<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>`

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_constant_APRIL_TAG_DICT_16H5:

.. rst-class:: classref-enumeration-constant

:ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **APRIL_TAG_DICT_16H5** = ``1``

4 x 4 bit, khoảng cách Hamming tối thiểu giữa hai mã bất kỳ = 5, 30 mã.

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_constant_APRIL_TAG_DICT_25H9:

.. rst-class:: classref-enumeration-constant

:ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **APRIL_TAG_DICT_25H9** = ``2``

5 x 5 bit, khoảng cách Hamming tối thiểu giữa hai mã bất kỳ = 9, 35 mã.

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_constant_APRIL_TAG_DICT_36H10:

.. rst-class:: classref-enumeration-constant

:ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **APRIL_TAG_DICT_36H10** = ``3``

6 x 6 bit, khoảng cách Hamming tối thiểu giữa hai mã bất kỳ = 10, 2320 mã.

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_constant_APRIL_TAG_DICT_36H11:

.. rst-class:: classref-enumeration-constant

:ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **APRIL_TAG_DICT_36H11** = ``4``

6 x 6 bit, khoảng cách Hamming tối thiểu giữa hai mã bất kỳ = 11, 587 mã.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_property_april_dict:

.. rst-class:: classref-property

:ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **april_dict** = ``4`` :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationAprilTag_property_april_dict>`

.. rst-class:: classref-property-setget

- |void| **set_april_dict**\ (\ value\: :ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>`\ ) - :ref:`AprilTagDict<enum_OpenXRSpatialCapabilityConfigurationAprilTag_AprilTagDict>` **get_april_dict**\ (\ )

Dictionary được sử dụng để giải mã các thẻ April.

\ **Lưu ý:** Phải thiết lập trước khi sử dụng cấu hình này để tạo một spatial context.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialCapabilityConfigurationAprilTag_method_get_enabled_components:

.. rst-class:: classref-method

:ref:`PackedInt64Array<class_PackedInt64Array>` **get_enabled_components**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationAprilTag_method_get_enabled_components>`

Trả về các component được bật bởi cấu hình này.

\ **Lưu ý:** Chỉ hợp lệ sau khi cấu hình này đã được sử dụng để tạo một spatial context.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
