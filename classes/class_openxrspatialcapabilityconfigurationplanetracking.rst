:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialCapabilityConfigurationPlaneTracking.xml.

.. _class_OpenXRSpatialCapabilityConfigurationPlaneTracking:

OpenXRSpatialCapabilityConfigurationPlaneTracking
=================================================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialCapabilityConfigurationBaseHeader<class_OpenXRSpatialCapabilityConfigurationBaseHeader>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Header cấu hình cho việc tracking mặt phẳng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Header cấu hình cho việc tracking mặt phẳng. Truyền đối tượng này vào :ref:`OpenXRSpatialEntityExtension.create_spatial_context()<class_OpenXRSpatialEntityExtension_method_create_spatial_context>` để tạo một spatial context có các khả năng tracking mặt phẳng.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>` | :ref:`get_enabled_components<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_get_enabled_components>`\ (\ ) |const| |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`supports_labels<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_labels>`\ (\ )                       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`supports_mesh_2d<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_mesh_2d>`\ (\ )                     |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`supports_polygons<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_polygons>`\ (\ )                   |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_get_enabled_components:

.. rst-class:: classref-method

:ref:`PackedInt64Array<class_PackedInt64Array>` **get_enabled_components**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_get_enabled_components>`

Trả về các component được bật bởi cấu hình này.

\ **Lưu ý:** Chỉ hợp lệ sau khi cấu hình này được sử dụng để tạo một spatial context.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_labels:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **supports_labels**\ (\ ) :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_labels>`

Trả về ``true`` nếu chúng tôi hỗ trợ component nhãn semantic của mặt phẳng (chỉ hợp lệ sau khi OpenXR session đã bắt đầu). Bạn có thể truy vấn các nhãn này bằng data object :ref:`OpenXRSpatialComponentPlaneSemanticLabelList<class_OpenXRSpatialComponentPlaneSemanticLabelList>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_mesh_2d:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **supports_mesh_2d**\ (\ ) :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_mesh_2d>`

Trả về ``true`` nếu chúng tôi hỗ trợ component mesh 2D (chỉ hợp lệ sau khi OpenXR session đã bắt đầu). Bạn có thể truy vấn các mesh này bằng data object :ref:`OpenXRSpatialComponentMesh2DList<class_OpenXRSpatialComponentMesh2DList>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_polygons:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **supports_polygons**\ (\ ) :ref:`🔗<class_OpenXRSpatialCapabilityConfigurationPlaneTracking_method_supports_polygons>`

Trả về ``true`` nếu chúng tôi hỗ trợ component polygon 2D (chỉ hợp lệ sau khi OpenXR session đã bắt đầu). Bạn có thể truy vấn các polygon này bằng data object :ref:`OpenXRSpatialComponentPolygon2DList<class_OpenXRSpatialComponentPolygon2DList>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
