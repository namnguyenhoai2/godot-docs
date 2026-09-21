:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialEntityExtension.xml.

.. _class_OpenXRSpatialEntityExtension:

OpenXRSpatialEntityExtension
============================

**Thử nghiệm:** Lớp này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRExtensionWrapper<class_OpenXRExtensionWrapper>` **<** :ref:`Object<class_Object>`

Tiện ích mở rộng OpenXR xử lý các thực thể không gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tiện ích mở rộng OpenXR xử lý các thực thể không gian và, khi được bật, cho phép truy vấn các thực thể không gian đó. Tiện ích mở rộng này cũng sẽ tự động quản lý các đối tượng :ref:`XRTracker<class_XRTracker>` cho những thực thể tĩnh.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`add_spatial_entity<class_OpenXRSpatialEntityExtension_method_add_spatial_entity>`\ (\ spatial_context\: :ref:`RID<class_RID>`, entity_id\: :ref:`int<class_int>`, entity\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                          |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` | :ref:`create_spatial_context<class_OpenXRSpatialEntityExtension_method_create_spatial_context>`\ (\ capability_configurations\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialCapabilityConfigurationBaseHeader<class_OpenXRSpatialCapabilityConfigurationBaseHeader>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                     |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` | :ref:`discover_spatial_entities<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>`\ (\ spatial_context\: :ref:`RID<class_RID>`, component_types\: :ref:`PackedInt64Array<class_PackedInt64Array>`, next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                                                                         |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` | :ref:`discover_spatial_entities_with_component_data<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities_with_component_data>`\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`find_spatial_entity<class_OpenXRSpatialEntityExtension_method_find_spatial_entity>`\ (\ entity_id\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                                                 |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`free_spatial_context<class_OpenXRSpatialEntityExtension_method_free_spatial_context>`\ (\ spatial_context\: :ref:`RID<class_RID>`\ )                                                                                                                                                                                                                                                                                                         |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`free_spatial_entity<class_OpenXRSpatialEntityExtension_method_free_spatial_entity>`\ (\ entity\: :ref:`RID<class_RID>`\ )                                                                                                                                                                                                                                                                                                                    |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`free_spatial_snapshot<class_OpenXRSpatialEntityExtension_method_free_spatial_snapshot>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ )                                                                                                                                                                                                                                                                                                      |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`get_float_buffer<class_OpenXRSpatialEntityExtension_method_get_float_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                     |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_spatial_context_handle<class_OpenXRSpatialEntityExtension_method_get_spatial_context_handle>`\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                     |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`get_spatial_context_ready<class_OpenXRSpatialEntityExtension_method_get_spatial_context_ready>`\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                       |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`get_spatial_entity_context<class_OpenXRSpatialEntityExtension_method_get_spatial_entity_context>`\ (\ entity\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                              |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_spatial_entity_id<class_OpenXRSpatialEntityExtension_method_get_spatial_entity_id>`\ (\ entity\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`get_spatial_snapshot_context<class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_context>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_spatial_snapshot_handle<class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_handle>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                  |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                         | :ref:`get_string<class_OpenXRSpatialEntityExtension_method_get_string>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                 |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`       | :ref:`get_uint8_buffer<class_OpenXRSpatialEntityExtension_method_get_uint8_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                     |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_uint16_buffer<class_OpenXRSpatialEntityExtension_method_get_uint16_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                   |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_uint32_buffer<class_OpenXRSpatialEntityExtension_method_get_uint32_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                   |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`get_vector2_buffer<class_OpenXRSpatialEntityExtension_method_get_vector2_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                 |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_vector3_buffer<class_OpenXRSpatialEntityExtension_method_get_vector3_buffer>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                 |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`make_spatial_entity<class_OpenXRSpatialEntityExtension_method_make_spatial_entity>`\ (\ spatial_context\: :ref:`RID<class_RID>`, entity_id\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`query_snapshot<class_OpenXRSpatialEntityExtension_method_query_snapshot>`\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ )                                                                                                                            |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`supports_capability<class_OpenXRSpatialEntityExtension_method_supports_capability>`\ (\ capability\: :ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>`\ )                                                                                                                                                                                                                                                                      |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`supports_component_type<class_OpenXRSpatialEntityExtension_method_supports_component_type>`\ (\ capability\: :ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>`, component_type\: :ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>`\ )                                                                                                                                                                      |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                               | :ref:`update_spatial_entities<class_OpenXRSpatialEntityExtension_method_update_spatial_entities>`\ (\ spatial_context\: :ref:`RID<class_RID>`, entities\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\], component_types\: :ref:`PackedInt64Array<class_PackedInt64Array>`, next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ )                                                                                            |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_OpenXRSpatialEntityExtension_signal_spatial_discovery_recommended:

.. rst-class:: classref-signal

**spatial_discovery_recommended**\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_signal_spatial_discovery_recommended>`

Được phát ra khi OpenXR khuyến nghị chạy một truy vấn khám phá vì các thực thể do spatial context này quản lý đã (có khả năng) thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRSpatialEntityExtension_Capability:

.. rst-class:: classref-enumeration

enum **Capability**: :ref:`🔗<enum_OpenXRSpatialEntityExtension_Capability>`

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_PLANE_TRACKING:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_PLANE_TRACKING** = ``1000741000``

Khả năng tracking mặt phẳng.

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_MARKER_TRACKING_QR_CODE:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_MARKER_TRACKING_QR_CODE** = ``1000743000``

Khả năng tracking marker dựa trên mã QR.

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_MARKER_TRACKING_MICRO_QR_CODE:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_MARKER_TRACKING_MICRO_QR_CODE** = ``1000743001``

Khả năng tracking marker dựa trên mã Micro QR.

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_MARKER_TRACKING_ARUCO_MARKER:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_MARKER_TRACKING_ARUCO_MARKER** = ``1000743002``

Khả năng tracking marker dựa trên marker Aruco.

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_MARKER_TRACKING_APRIL_TAG:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_MARKER_TRACKING_APRIL_TAG** = ``1000743003``

Khả năng tracking marker dựa trên April tag.

.. _class_OpenXRSpatialEntityExtension_constant_CAPABILITY_ANCHOR:

.. rst-class:: classref-enumeration-constant

:ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>` **CAPABILITY_ANCHOR** = ``1000762000``

Khả năng anchor.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRSpatialEntityExtension_ComponentType:

.. rst-class:: classref-enumeration

enum **ComponentType**: :ref:`🔗<enum_OpenXRSpatialEntityExtension_ComponentType>`

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_BOUNDED_2D:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_BOUNDED_2D** = ``1``

Component cung cấp giới hạn 2D cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentBounded2DListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialBounded2DDataEXT``.

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_BOUNDED_3D:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_BOUNDED_3D** = ``2``

Component cung cấp giới hạn 3D cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentBounded3DListEXT``; cấu trúc dữ liệu tương ứng là ``XrBoxf``.

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_PARENT:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_PARENT** = ``3``

Component cung cấp XrSpatialEntityIdEXT của thực thể cha cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentParentListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialEntityIdEXT``.

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_MESH_3D:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_MESH_3D** = ``4``

Component cung cấp mesh 3D cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentMesh3DListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialMeshDataEXT``.

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_PLANE_ALIGNMENT:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_PLANE_ALIGNMENT** = ``1000741000``

Component cung cấp enum căn chỉnh mặt phẳng cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentPlaneAlignmentListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialPlaneAlignmentEXT`` (Được thêm bởi extension ``XR_EXT_spatial_plane_tracking``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_MESH_2D:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_MESH_2D** = ``1000741001``

Component cung cấp mesh 2D cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentMesh2DListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialMeshDataEXT`` (Được thêm bởi extension ``XR_EXT_spatial_plane_tracking``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_POLYGON_2D:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_POLYGON_2D** = ``1000741002``

Component cung cấp polygon biên 2D cho một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentPolygon2DListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialPolygon2DDataEXT`` (Được thêm bởi extension ``XR_EXT_spatial_plane_tracking``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_PLANE_SEMANTIC_LABEL:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_PLANE_SEMANTIC_LABEL** = ``1000741003``

Component cung cấp nhãn ngữ nghĩa cho một mặt phẳng. Cấu trúc danh sách tương ứng là ``XrSpatialComponentPlaneSemanticLabelListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialPlaneSemanticLabelEXT`` (Được thêm bởi extension ``XR_EXT_spatial_plane_tracking``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_MARKER:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_MARKER** = ``1000743000``

Component mô tả loại, ID và vị trí của marker. Cấu trúc danh sách tương ứng là ``XrSpatialComponentMarkerListEXT``; cấu trúc dữ liệu tương ứng là ``XrSpatialMarkerDataEXT`` (Được thêm bởi extension ``XR_EXT_spatial_marker_tracking``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_ANCHOR:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_ANCHOR** = ``1000762000``

Component cung cấp vị trí cho một anchor. Cấu trúc danh sách tương ứng là ``XrSpatialComponentAnchorListEXT``; cấu trúc dữ liệu tương ứng là ``XrPosef`` (Được thêm bởi extension ``XR_EXT_spatial_anchor``).

.. _class_OpenXRSpatialEntityExtension_constant_COMPONENT_TYPE_PERSISTENCE:

.. rst-class:: classref-enumeration-constant

:ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>` **COMPONENT_TYPE_PERSISTENCE** = ``1000763000``

Component cung cấp UUID đã lưu của một thực thể không gian. Cấu trúc danh sách tương ứng là ``XrSpatialComponentPersistenceListEXT; the corresponding data structure is [code]XrSpatialPersistenceDataEXT`` (Được thêm bởi extension ``XR_EXT_spatial_persistence``).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_OpenXRSpatialEntityExtension_method_add_spatial_entity:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **add_spatial_entity**\ (\ spatial_context\: :ref:`RID<class_RID>`, entity_id\: :ref:`int<class_int>`, entity\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_add_spatial_entity>`

Đăng ký một thực thể được tạo trực tiếp trên OpenXR runtime.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_create_spatial_context:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **create_spatial_context**\ (\ capability_configurations\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialCapabilityConfigurationBaseHeader<class_OpenXRSpatialCapabilityConfigurationBaseHeader>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_create_spatial_context>`

Tạo một spatial context mới để xử lý các thực thể theo những cấu hình capability được cung cấp. ``capability_configurations`` là một mảng :ref:`OpenXRSpatialCapabilityConfigurationBaseHeader<class_OpenXRSpatialCapabilityConfigurationBaseHeader>` chứa dữ liệu cấu hình capability cần thiết.

\ ``next`` là một tham số tùy chọn có thể chứa thông tin bổ sung để tạo spatial context của chúng ta.

\ **Lưu ý:** Đây là một phương thức bất đồng bộ và trả về một đối tượng :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` dùng để theo dõi trạng thái; việc loại bỏ đối tượng này sẽ không hủy quá trình tạo. Khi thành công, ``user_callback`` sẽ được gọi nếu được chỉ định. Dữ liệu kết quả của hàm này là :ref:`RID<class_RID>` của spatial context.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_discover_spatial_entities:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **discover_spatial_entities**\ (\ spatial_context\: :ref:`RID<class_RID>`, component_types\: :ref:`PackedInt64Array<class_PackedInt64Array>`, next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>`

Bắt đầu một truy vấn khám phá mới; truy vấn này sẽ thu thập tất cả các đối tượng được ``spatial_context`` tracking có ít nhất một trong các loại component được chỉ định trong ``component_types``.

\ ``next`` là một tham số tùy chọn có thể chứa thông tin bổ sung để thực thi truy vấn khám phá.

\ **Lưu ý:** Đây là một phương thức bất đồng bộ và trả về một đối tượng :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` dùng để theo dõi trạng thái; việc loại bỏ đối tượng này sẽ không hủy quá trình khám phá. Khi thành công, ``user_callback`` sẽ được gọi nếu được chỉ định. Dữ liệu kết quả của hàm này là :ref:`RID<class_RID>` cho snapshot của chúng ta.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_discover_spatial_entities_with_component_data:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **discover_spatial_entities_with_component_data**\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities_with_component_data>`

Phương thức tiện ích khi caller chỉ có một :ref:`Array<class_Array>` của :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>` và cần khám phá các thực thể không gian.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_find_spatial_entity:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **find_spatial_entity**\ (\ entity_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_find_spatial_entity>`

Trả về :ref:`RID<class_RID>` của thực thể không gian có ID được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_free_spatial_context:

.. rst-class:: classref-method

|void| **free_spatial_context**\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_free_spatial_context>`

Giải phóng một spatial context đã được tạo khi gọi :ref:`create_spatial_context()<class_OpenXRSpatialEntityExtension_method_create_spatial_context>`. Nếu quá trình tạo spatial context vẫn đang diễn ra, quá trình bất đồng bộ sẽ bị hủy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_free_spatial_entity:

.. rst-class:: classref-method

|void| **free_spatial_entity**\ (\ entity\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_free_spatial_entity>`

Giải phóng một thực thể đã được tạo khi gọi :ref:`add_spatial_entity()<class_OpenXRSpatialEntityExtension_method_add_spatial_entity>` hoặc :ref:`make_spatial_entity()<class_OpenXRSpatialEntityExtension_method_make_spatial_entity>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_free_spatial_snapshot:

.. rst-class:: classref-method

|void| **free_spatial_snapshot**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_free_spatial_snapshot>`

Giải phóng một spatial snapshot đã được tạo khi gọi :ref:`discover_spatial_entities()<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>`. Nếu quá trình tạo spatial snapshot vẫn đang diễn ra, quá trình bất đồng bộ sẽ bị hủy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_float_buffer:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_float_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_float_buffer>`

Trả về một buffer chứa các giá trị float từ một buffer được truy xuất khi chụp snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_context_handle:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_spatial_context_handle**\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_context_handle>`

Trả về handle spatial context của OpenXR cho snapshot này.

\ **Lưu ý:** Phương thức này dành cho việc sử dụng từ các GDExtensions triển khai các trình xử lý capability của thực thể không gian.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_context_ready:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_spatial_context_ready**\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_context_ready>`

Trả về ``true`` nếu ngữ cảnh không gian đã hoàn tất việc tạo và sẵn sàng được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_entity_context:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_spatial_entity_context**\ (\ entity\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_entity_context>`

Trả về ngữ cảnh không gian của thực thể này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_entity_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_spatial_entity_id**\ (\ entity\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_entity_id>`

Trả về ``XrSpatialEntityIdEXT`` nội bộ được liên kết với thực thể.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_context:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_spatial_snapshot_context**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_context>`

Trả về ngữ cảnh không gian liên quan đến snapshot không gian này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_handle:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_spatial_snapshot_handle**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_spatial_snapshot_handle>`

Trả về handle snapshot không gian OpenXR cho snapshot này.

\ **Lưu ý:** Phương thức này được thiết kế để sử dụng từ các GDExtensions triển khai các trình xử lý capability của thực thể không gian.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_string**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_string>`

Trả về một chuỗi từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_uint8_buffer:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **get_uint8_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_uint8_buffer>`

Trả về một buffer chứa các số nguyên 8 bit từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_uint16_buffer:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_uint16_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_uint16_buffer>`

Trả về một buffer chứa các số nguyên 16 bit từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_uint32_buffer:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_uint32_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_uint32_buffer>`

Trả về một buffer chứa các số nguyên 32 bit từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_vector2_buffer:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_vector2_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_vector2_buffer>`

Trả về một buffer chứa các mục :ref:`Vector2<class_Vector2>` từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_get_vector3_buffer:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_vector3_buffer**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, buffer_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityExtension_method_get_vector3_buffer>`

Trả về một buffer chứa các mục :ref:`Vector3<class_Vector3>` từ buffer được truy xuất khi tạo snapshot.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_make_spatial_entity:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **make_spatial_entity**\ (\ spatial_context\: :ref:`RID<class_RID>`, entity_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_make_spatial_entity>`

Tạo một thực thể mới cho ``entity_id`` này. ``spatial_context`` phải khớp với ngữ cảnh đã phát hiện thực thể.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_query_snapshot:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **query_snapshot**\ (\ spatial_snapshot\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_query_snapshot>`

Truy vấn dữ liệu snapshot. Thao tác này sẽ tìm tất cả thực thể trong snapshot chứa mọi component được yêu cầu trong ``component_data``. Sau đó, các đối tượng nằm trong ``component_data`` sẽ được điền dữ liệu đã truy vấn. ``component_data`` luôn phải có một đối tượng thuộc :ref:`OpenXRSpatialQueryResultData<class_OpenXRSpatialQueryResultData>` làm mục đầu tiên.

\ ``next`` là một tham số tùy chọn có thể chứa thông tin bổ sung được truyền vào khi thiết lập các điều kiện truy vấn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_supports_capability:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **supports_capability**\ (\ capability\: :ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_supports_capability>`

Trả về ``true`` nếu ``capability`` của thực thể không gian này được phần cứng đang sử dụng hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_supports_component_type:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **supports_component_type**\ (\ capability\: :ref:`Capability<enum_OpenXRSpatialEntityExtension_Capability>`, component_type\: :ref:`ComponentType<enum_OpenXRSpatialEntityExtension_ComponentType>`\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_supports_component_type>`

Trả về ``true`` nếu ``capability`` này hỗ trợ ``component_type``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityExtension_method_update_spatial_entities:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **update_spatial_entities**\ (\ spatial_context\: :ref:`RID<class_RID>`, entities\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\], component_types\: :ref:`PackedInt64Array<class_PackedInt64Array>`, next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ ) :ref:`🔗<class_OpenXRSpatialEntityExtension_method_update_spatial_entities>`

Thực hiện snapshot cho một số lượng thực thể giới hạn. Đây KHÔNG phải là phương thức bất đồng bộ và sẽ trả về snapshot ngay lập tức.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
