:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialContextPersistenceConfig.xml.

.. _class_OpenXRSpatialContextPersistenceConfig:

OpenXRSpatialContextPersistenceConfig
=====================================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tiêu đề cấu hình cho persistence không gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tiêu đề cấu hình cho persistence không gian. Truyền đối tượng này cho :ref:`OpenXRSpatialEntityExtension.create_spatial_context()<class_OpenXRSpatialEntityExtension_method_create_spatial_context>` làm tham số tiếp theo để tạo một spatial context với các capability persistence không gian.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`add_persistence_context<class_OpenXRSpatialContextPersistenceConfig_method_add_persistence_context>`\ (\ persistence_context\: :ref:`RID<class_RID>`\ )       |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`get_persistence_contexts<class_OpenXRSpatialContextPersistenceConfig_method_get_persistence_contexts>`\ (\ ) |const|                                          |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`remove_persistence_context<class_OpenXRSpatialContextPersistenceConfig_method_remove_persistence_context>`\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_OpenXRSpatialContextPersistenceConfig_method_add_persistence_context:

.. rst-class:: classref-method

|void| **add_persistence_context**\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialContextPersistenceConfig_method_add_persistence_context>`

Thêm một persistence context vào cấu hình này. Bạn phải thêm ít nhất một persistence context để tạo một cấu hình hợp lệ. Bạn có thể tạo một persistence context bằng cách gọi :ref:`OpenXRSpatialAnchorCapability.create_persistence_context()<class_OpenXRSpatialAnchorCapability_method_create_persistence_context>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialContextPersistenceConfig_method_get_persistence_contexts:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_persistence_contexts**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialContextPersistenceConfig_method_get_persistence_contexts>`

Lấy các persistence context (dưới dạng :ref:`RID<class_RID>`\ s) nhận được bởi :ref:`add_persistence_context()<class_OpenXRSpatialContextPersistenceConfig_method_add_persistence_context>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialContextPersistenceConfig_method_remove_persistence_context:

.. rst-class:: classref-method

|void| **remove_persistence_context**\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialContextPersistenceConfig_method_remove_persistence_context>`

Xóa một persistence context.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
