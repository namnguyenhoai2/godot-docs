:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialAnchorCapability.xml.

.. _class_OpenXRSpatialAnchorCapability:

OpenXRSpatialAnchorCapability
=============================

**Thử nghiệm:** Class này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRExtensionWrapper<class_OpenXRExtensionWrapper>` **<** :ref:`Object<class_Object>`

Triển khai để xử lý logic anchor của spatial entity.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một class nội bộ xử lý extension spatial entity anchor của OpenXR.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>`   | :ref:`create_default_persistence_context<class_OpenXRSpatialAnchorCapability_method_create_default_persistence_context>`\ (\ user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` | :ref:`create_new_anchor<class_OpenXRSpatialAnchorCapability_method_create_new_anchor>`\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, spatial_context\: :ref:`RID<class_RID>` = RID(), next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ )                                                                                                                                                                                                                                     |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>`   | :ref:`create_persistence_context<class_OpenXRSpatialAnchorCapability_method_create_persistence_context>`\ (\ scope\: :ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>`, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                                                                                                                                                                                                                        |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`do_entity_update<class_OpenXRSpatialAnchorCapability_method_do_entity_update>`\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next_snapshot_create\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, next_snapshot_query\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ )                                                                           |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`free_persistence_context<class_OpenXRSpatialAnchorCapability_method_free_persistence_context>`\ (\ persistence_context\: :ref:`RID<class_RID>`\ )                                                                                                                                                                                                                                                                                                                                                   |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_persistence_context_handle<class_OpenXRSpatialAnchorCapability_method_get_persistence_context_handle>`\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) |const|                                                                                                                                                                                                                                                                                                                               |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_persistence_scope_supported<class_OpenXRSpatialAnchorCapability_method_is_persistence_scope_supported>`\ (\ scope\: :ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>`\ )                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_spatial_anchor_supported<class_OpenXRSpatialAnchorCapability_method_is_spatial_anchor_supported>`\ (\ )                                                                                                                                                                                                                                                                                                                                                                                          |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_spatial_persistence_supported<class_OpenXRSpatialAnchorCapability_method_is_spatial_persistence_supported>`\ (\ )                                                                                                                                                                                                                                                                                                                                                                                |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>`   | :ref:`persist_anchor<class_OpenXRSpatialAnchorCapability_method_persist_anchor>`\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`, persistence_context\: :ref:`RID<class_RID>` = RID(), user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                                                                                                                                                                                                         |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`remove_anchor<class_OpenXRSpatialAnchorCapability_method_remove_anchor>`\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`\ )                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>`   | :ref:`start_entity_discovery<class_OpenXRSpatialAnchorCapability_method_start_entity_discovery>`\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next_snapshot_create\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, next_snapshot_query\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>`   | :ref:`unpersist_anchor<class_OpenXRSpatialAnchorCapability_method_unpersist_anchor>`\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`, persistence_context\: :ref:`RID<class_RID>` = RID(), user_callback\: :ref:`Callable<class_Callable>` = Callable()\ )                                                                                                                                                                                                                     |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRSpatialAnchorCapability_PersistenceScope:

.. rst-class:: classref-enumeration

enum **PersistenceScope**: :ref:`🔗<enum_OpenXRSpatialAnchorCapability_PersistenceScope>`

.. _class_OpenXRSpatialAnchorCapability_constant_PERSISTENCE_SCOPE_SYSTEM_MANAGED:

.. rst-class:: classref-enumeration-constant

:ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>` **PERSISTENCE_SCOPE_SYSTEM_MANAGED** = ``1``

Cung cấp cho ứng dụng quyền truy cập chỉ đọc (tức là ứng dụng không thể sửa đổi scope này) vào các spatial entity được hệ thống lưu trữ và quản lý. Ứng dụng có thể sử dụng UUID trong persistence component cho scope này để đối chiếu các entity giữa những spatial context và các lần khởi động lại thiết bị.

.. _class_OpenXRSpatialAnchorCapability_constant_PERSISTENCE_SCOPE_LOCAL_ANCHORS:

.. rst-class:: classref-enumeration-constant

:ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>` **PERSISTENCE_SCOPE_LOCAL_ANCHORS** = ``1000781000``

Các thao tác persistence và quyền truy cập dữ liệu chỉ giới hạn ở các spatial anchor trên cùng thiết bị, dành cho cùng người dùng và cùng ứng dụng (sử dụng các hàm :ref:`persist_anchor()<class_OpenXRSpatialAnchorCapability_method_persist_anchor>` và :ref:`unpersist_anchor()<class_OpenXRSpatialAnchorCapability_method_unpersist_anchor>`) 

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialAnchorCapability_method_create_default_persistence_context:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **create_default_persistence_context**\ (\ user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_create_default_persistence_context>`

Gọi :ref:`create_persistence_context()<class_OpenXRSpatialAnchorCapability_method_create_persistence_context>` với một cấu hình có khả năng hoạt động với XR runtime.

\ ``user_callback`` được gọi khi context được tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_create_new_anchor:

.. rst-class:: classref-method

:ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` **create_new_anchor**\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, spatial_context\: :ref:`RID<class_RID>` = RID(), next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_create_new_anchor>`

Tạo một anchor mới sẽ được XR runtime theo dõi. ``transform`` phải là một transform trong local space của node :ref:`XROrigin3D<class_XROrigin3D>`. Nếu ``spatial_context`` không được chỉ định, giá trị mặc định sẽ được sử dụng; điều này yêu cầu :ref:`ProjectSettings.xr/openxr/extensions/spatial_entity/enable_builtin_anchor_detection<class_ProjectSettings_property_xr/openxr/extensions/spatial_entity/enable_builtin_anchor_detection>` phải được thiết lập. Tracker được trả về sẽ theo dõi vị trí trong trường hợp reference space của chúng ta thay đổi.

\ ``next`` phải là một next object hợp lệ cho chuỗi ``XrSpatialAnchorCreateInfoEXT``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_create_persistence_context:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **create_persistence_context**\ (\ scope\: :ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>`, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_create_persistence_context>`

Tạo một persistence context mới để lưu trữ dữ liệu persistent.

\ **Lưu ý:** Đây là một phương thức bất đồng bộ và trả về một object :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` dùng để theo dõi trạng thái; việc loại bỏ object này sẽ không hủy quá trình tạo. Khi thành công, ``user_callback`` sẽ được gọi nếu được chỉ định. Giá trị kết quả của hàm này là :ref:`RID<class_RID>` của persistence context.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_do_entity_update:

.. rst-class:: classref-method

|void| **do_entity_update**\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next_snapshot_create\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, next_snapshot_query\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_do_entity_update>`

Gọi :ref:`OpenXRSpatialEntityExtension.update_spatial_entities()<class_OpenXRSpatialEntityExtension_method_update_spatial_entities>` và :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>` với các anchor entity được liên kết với ``spatial_context``.

\ ``component_data`` là các :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\ s cần được cập nhật cho anchor capability này.

Nếu ``next_snapshot_create`` khác null, hãy truyền giá trị này vào tham số ``next`` trong :ref:`OpenXRSpatialEntityExtension.update_spatial_entities()<class_OpenXRSpatialEntityExtension_method_update_spatial_entities>`.

Nếu ``next_snapshot_query`` khác null, hãy truyền giá trị này vào tham số ``next`` trong :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_free_persistence_context:

.. rst-class:: classref-method

|void| **free_persistence_context**\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_free_persistence_context>`

Giải phóng persistence context đã được tạo trước đó bằng :ref:`create_persistence_context()<class_OpenXRSpatialAnchorCapability_method_create_persistence_context>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_get_persistence_context_handle:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_persistence_context_handle**\ (\ persistence_context\: :ref:`RID<class_RID>`\ ) |const| :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_get_persistence_context_handle>`

Trả về handle nội bộ của persistence context này.

\ **Lưu ý:** Dành cho các triển khai GDExtension.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_is_persistence_scope_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_persistence_scope_supported**\ (\ scope\: :ref:`PersistenceScope<enum_OpenXRSpatialAnchorCapability_PersistenceScope>`\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_is_persistence_scope_supported>`

Trả về ``true`` nếu persistence scope này được spatial anchor capability hỗ trợ.

\ **Lưu ý:** Chỉ hợp lệ sau khi một OpenXR instance được tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_is_spatial_anchor_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_spatial_anchor_supported**\ (\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_is_spatial_anchor_supported>`

Trả về ``true`` nếu phần cứng hỗ trợ spatial anchor. Chỉ trả về giá trị hợp lệ sau khi OpenXR được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_is_spatial_persistence_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_spatial_persistence_supported**\ (\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_is_spatial_persistence_supported>`

Trả về ``true`` nếu phần cứng hỗ trợ persistent spatial anchor. Chỉ trả về giá trị hợp lệ sau khi OpenXR được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_persist_anchor:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **persist_anchor**\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`, persistence_context\: :ref:`RID<class_RID>` = RID(), user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_persist_anchor>`

Chuyển anchor này thành persistent anchor. Điều này có nghĩa là vị trí của nó sẽ được lưu trên thiết bị và anchor sẽ được khôi phục vào lần tiếp theo ứng dụng của bạn khởi động. Nếu ``persistence_context`` không được chỉ định, giá trị mặc định sẽ được sử dụng; điều này yêu cầu :ref:`ProjectSettings.xr/openxr/extensions/spatial_entity/enable_builtin_anchor_detection<class_ProjectSettings_property_xr/openxr/extensions/spatial_entity/enable_builtin_anchor_detection>` phải được thiết lập.

\ **Lưu ý:** Đây là một phương thức bất đồng bộ và trả về một object :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` dùng để theo dõi trạng thái; việc loại bỏ object này sẽ không hủy quá trình tạo. Khi thành công, ``user_callback`` sẽ được gọi nếu được chỉ định. Giá trị kết quả của hàm này là một boolean, sẽ được đặt thành ``true`` khi hoàn tất thành công.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_remove_anchor:

.. rst-class:: classref-method

|void| **remove_anchor**\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_remove_anchor>`

Xóa anchor đã được tạo trước đó bằng :ref:`create_new_anchor()<class_OpenXRSpatialAnchorCapability_method_create_new_anchor>`. Nếu anchor này là persistent, trước tiên bạn phải gọi :ref:`unpersist_anchor()<class_OpenXRSpatialAnchorCapability_method_unpersist_anchor>` và chờ callback của nó.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_start_entity_discovery:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **start_entity_discovery**\ (\ spatial_context\: :ref:`RID<class_RID>`, component_data\: :ref:`Array<class_Array>`\[:ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\], next_snapshot_create\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, next_snapshot_query\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` = null, user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_start_entity_discovery>`

Gọi :ref:`OpenXRSpatialEntityExtension.discover_spatial_entities()<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>` và :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>` với các anchor entity được liên kết với ``spatial_context``.

\ ``component_data`` là các :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>`\ s cần được phát hiện cho anchor capability này.

Nếu ``next_snapshot_create`` khác null, hãy truyền giá trị này vào tham số ``next`` trong :ref:`OpenXRSpatialEntityExtension.discover_spatial_entities()<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>`.

Nếu ``next_snapshot_query`` khác null, hãy truyền giá trị này vào tham số ``next`` trong :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>`.

\ ``user_callback``, khi khác null, được gọi với hai tham số, thường là hai lần. Tham số đầu tiên là :ref:`RID<class_RID>` của discovery snapshot, còn tham số thứ hai là một boolean, trong đó ``false`` cho biết discovery snapshot sắp được xử lý và ``true`` cho biết discovery snapshot đã được xử lý xong và ``component_data`` có dữ liệu hợp lệ. Lần gọi thứ hai sẽ được bỏ qua nếu xảy ra lỗi.

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` được trả về giống hệt giá trị trả về từ :ref:`OpenXRSpatialEntityExtension.discover_spatial_entities()<class_OpenXRSpatialEntityExtension_method_discover_spatial_entities>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialAnchorCapability_method_unpersist_anchor:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **unpersist_anchor**\ (\ anchor_tracker\: :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`, persistence_context\: :ref:`RID<class_RID>` = RID(), user_callback\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRSpatialAnchorCapability_method_unpersist_anchor>`

Xóa dữ liệu persistent khỏi anchor này. Runtime sẽ không tạo lại anchor khi ứng dụng của bạn khởi động lại. Nếu ``persistence_context`` không được chỉ định, giá trị mặc định sẽ được sử dụng; điều này yêu cầu :ref:`ProjectSettings.xr/openxr/extensions/spatial_entity/enabled<class_ProjectSettings_property_xr/openxr/extensions/spatial_entity/enabled>` phải được thiết lập.

\ **Lưu ý:** Đây là một phương thức bất đồng bộ và trả về một object :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` dùng để theo dõi trạng thái; việc loại bỏ object này sẽ không hủy quá trình tạo. Khi thành công, ``user_callback`` sẽ được gọi nếu được chỉ định. Giá trị kết quả của hàm này là một boolean, sẽ được đặt thành ``true`` khi hoàn tất thành công.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
