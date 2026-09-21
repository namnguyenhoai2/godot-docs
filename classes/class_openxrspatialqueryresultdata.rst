:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialQueryResultData.xml.

.. _class_OpenXRSpatialQueryResultData:

OpenXRSpatialQueryResultData
============================

**Experimental:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đối tượng dùng để lưu trữ dữ liệu kết quả truy vấn chính.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng dùng để lưu trữ dữ liệu kết quả truy vấn chính khi gọi :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>`. Đây luôn phải là component đầu tiên được yêu cầu.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                           | :ref:`get_capacity<class_OpenXRSpatialQueryResultData_method_get_capacity>`\ (\ ) |const|                                        |
   +---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                           | :ref:`get_entity_id<class_OpenXRSpatialQueryResultData_method_get_entity_id>`\ (\ index\: :ref:`int<class_int>`\ ) |const|       |
   +---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` | :ref:`get_entity_state<class_OpenXRSpatialQueryResultData_method_get_entity_state>`\ (\ index\: :ref:`int<class_int>`\ ) |const| |
   +---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialQueryResultData_method_get_capacity:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_capacity**\ (\ ) |const| :ref:`🔗<class_OpenXRSpatialQueryResultData_method_get_capacity>`

Trả về số lượng entity đã được truy xuất.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialQueryResultData_method_get_entity_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_entity_id**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialQueryResultData_method_get_entity_id>`

Trả về entity id (``XrSpatialEntityIdEXT``) của entity tại ``index`` này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRSpatialQueryResultData_method_get_entity_state:

.. rst-class:: classref-method

:ref:`EntityTrackingState<enum_OpenXRSpatialEntityTracker_EntityTrackingState>` **get_entity_state**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialQueryResultData_method_get_entity_state>`

Trả về trạng thái của entity tại ``index`` này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
