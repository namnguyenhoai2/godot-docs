:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialEntityTracker.xml.

.. _class_OpenXRSpatialEntityTracker:

OpenXRSpatialEntityTracker
==========================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`XRPositionalTracker<class_XRPositionalTracker>` **<** :ref:`XRTracker<class_XRTracker>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>`, :ref:`OpenXRMarkerTracker<class_OpenXRMarkerTracker>`, :ref:`OpenXRPlaneTracker<class_OpenXRPlaneTracker>`

Class cơ sở cho các positional tracker được quản lý bởi các spatial extension của OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là các tracker được tạo và quản lý bởi các spatial extension của OpenXR, cung cấp quyền truy cập vào dữ liệu cụ thể liên quan đến các spatial entity của OpenXR. Chúng sẽ luôn có kiểu ``TRACKER_ANCHOR``.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                                           | :ref:`entity<class_OpenXRSpatialEntityTracker_property_entity>`                                 | ``RID()``                                                         |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
   | :ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` | :ref:`spatial_tracking_state<class_OpenXRSpatialEntityTracker_property_spatial_tracking_state>` | ``2``                                                             |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
   | :ref:`TrackerType<enum_XRServer_TrackerType>`                                   | type                                                                                            | ``8`` (overrides :ref:`XRTracker<class_XRTracker_property_type>`) |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`add_next<class_OpenXRSpatialEntityTracker_method_add_next>`\ (\ next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>`\ )       |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` | :ref:`get_next<class_OpenXRSpatialEntityTracker_method_get_next>`\ (\ ) |const|                                                             |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                 | :ref:`get_spatial_context<class_OpenXRSpatialEntityTracker_method_get_spatial_context>`\ (\ ) |const|                                       |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`remove_next<class_OpenXRSpatialEntityTracker_method_remove_next>`\ (\ next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>`\ ) |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_spatial_context<class_OpenXRSpatialEntityTracker_method_set_spatial_context>`\ (\ spatial_context\: :ref:`RID<class_RID>`\ )      |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_OpenXRSpatialEntityTracker_signal_next_changed:

.. rst-class:: classref-signal

**next_changed**\ (\ ) :ref:`🔗<class_OpenXRSpatialEntityTracker_signal_next_changed>`

Được phát ra khi next-chain thay đổi, từ :ref:`add_next()<class_OpenXRSpatialEntityTracker_method_add_next>` hoặc :ref:`remove_next()<class_OpenXRSpatialEntityTracker_method_remove_next>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_signal_spatial_tracking_state_changed:

.. rst-class:: classref-signal

**spatial_tracking_state_changed**\ (\ spatial_tracking_state\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRSpatialEntityTracker_signal_spatial_tracking_state_changed>`

.. container:: contribute

	Hiện chưa có mô tả cho signal này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRSpatialEntityTracker_EntityTrackingState:

.. rst-class:: classref-enumeration

enum **EntityTrackingState**: :ref:`🔗<enum_OpenXRSpatialEntityTracker_EntityTrackingState>`

.. _class_OpenXRSpatialEntityTracker_constant_ENTITY_TRACKING_STATE_STOPPED:

.. rst-class:: classref-enumeration-constant

:ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **ENTITY_TRACKING_STATE_STOPPED** = ``1``

Anchor này đã dừng được tracking.

.. _class_OpenXRSpatialEntityTracker_constant_ENTITY_TRACKING_STATE_PAUSED:

.. rst-class:: classref-enumeration-constant

:ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **ENTITY_TRACKING_STATE_PAUSED** = ``2``

Tracking hiện đang bị tạm dừng.

.. _class_OpenXRSpatialEntityTracker_constant_ENTITY_TRACKING_STATE_TRACKING:

.. rst-class:: classref-enumeration-constant

:ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **ENTITY_TRACKING_STATE_TRACKING** = ``3``

Anchor này hiện đang được tracking.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRSpatialEntityTracker_property_entity:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **entity** = ``RID()`` :ref:`🔗<class_OpenXRSpatialEntityTracker_property_entity>`

.. rst-class:: classref-property-setget

- |void| **set_entity**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_entity**\ (\ )

Spatial entity được liên kết với tracker này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_property_spatial_tracking_state:

.. rst-class:: classref-property

:ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **spatial_tracking_state** = ``2`` :ref:`🔗<class_OpenXRSpatialEntityTracker_property_spatial_tracking_state>`

.. rst-class:: classref-property-setget

- |void| **set_spatial_tracking_state**\ (\ value\: :ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>`\ ) - :ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **get_spatial_tracking_state**\ (\ )

Trạng thái spatial tracking của tracker này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialEntityTracker_method_add_next:

.. rst-class:: classref-method

|void| **add_next**\ (\ next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>`\ ) :ref:`🔗<class_OpenXRSpatialEntityTracker_method_add_next>`

Thêm một :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` mới vào next-chain.

\ :ref:`get_next()<class_OpenXRSpatialEntityTracker_method_get_next>` sẽ trả về ``next`` này cho đến khi :ref:`add_next()<class_OpenXRSpatialEntityTracker_method_add_next>` được gọi lại hoặc nó bị xóa trong :ref:`remove_next()<class_OpenXRSpatialEntityTracker_method_remove_next>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_method_get_next:

.. rst-class:: classref-method

:ref:`OpenXRStructureBase<class_OpenXRStructureBase>` **get_next**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityTracker_method_get_next>`

Lấy :ref:`OpenXRStructureBase<class_OpenXRStructureBase>` đầu trong next-chain.

Xem thêm :ref:`add_next()<class_OpenXRSpatialEntityTracker_method_add_next>` và :ref:`remove_next()<class_OpenXRSpatialEntityTracker_method_remove_next>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_method_get_spatial_context:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_spatial_context**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialEntityTracker_method_get_spatial_context>`

Lấy spatial context được dùng để tạo **OpenXRSpatialEntityTracker** này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_method_remove_next:

.. rst-class:: classref-method

|void| **remove_next**\ (\ next\: :ref:`OpenXRStructureBase<class_OpenXRStructureBase>`\ ) :ref:`🔗<class_OpenXRSpatialEntityTracker_method_remove_next>`

Xóa một đối tượng ``next`` đã được thêm trước đó trong :ref:`add_next()<class_OpenXRSpatialEntityTracker_method_add_next>` khỏi next-chain.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialEntityTracker_method_set_spatial_context:

.. rst-class:: classref-method

|void| **set_spatial_context**\ (\ spatial_context\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_OpenXRSpatialEntityTracker_method_set_spatial_context>`

Đặt spatial context được dùng để tạo tracker này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
