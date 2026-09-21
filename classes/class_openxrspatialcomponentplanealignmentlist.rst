:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialComponentPlaneAlignmentList.xml.

.. _class_OpenXRSpatialComponentPlaneAlignmentList:

OpenXRSpatialComponentPlaneAlignmentList
========================================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đối tượng dùng để lưu trữ dữ liệu kết quả căn chỉnh mặt phẳng của các truy vấn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng dùng để lưu trữ dữ liệu kết quả căn chỉnh mặt phẳng của các truy vấn khi gọi :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` | :ref:`get_plane_alignment<class_OpenXRSpatialComponentPlaneAlignmentList_method_get_plane_alignment>`\ (\ index\: :ref:`int<class_int>`\ ) |const| |
   +-------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment:

.. rst-class:: classref-enumeration

enum **PlaneAlignment**: :ref:`🔗<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>`

.. _class_OpenXRSpatialComponentPlaneAlignmentList_constant_PLANE_ALIGNMENT_HORIZONTAL_UPWARD:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` **PLANE_ALIGNMENT_HORIZONTAL_UPWARD** = ``0``

Mặt phẳng hướng lên trên.

.. _class_OpenXRSpatialComponentPlaneAlignmentList_constant_PLANE_ALIGNMENT_HORIZONTAL_DOWNWARD:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` **PLANE_ALIGNMENT_HORIZONTAL_DOWNWARD** = ``1``

Mặt phẳng hướng xuống dưới.

.. _class_OpenXRSpatialComponentPlaneAlignmentList_constant_PLANE_ALIGNMENT_VERTICAL:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` **PLANE_ALIGNMENT_VERTICAL** = ``2``

Mặt phẳng được căn chỉnh theo chiều dọc.

.. _class_OpenXRSpatialComponentPlaneAlignmentList_constant_PLANE_ALIGNMENT_ARBITRARY:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` **PLANE_ALIGNMENT_ARBITRARY** = ``3``

Mặt phẳng có căn chỉnh tùy ý.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialComponentPlaneAlignmentList_method_get_plane_alignment:

.. rst-class:: classref-method

:ref:`PlaneAlignment<enum_OpenXRSpatialComponentPlaneAlignmentList_PlaneAlignment>` **get_plane_alignment**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialComponentPlaneAlignmentList_method_get_plane_alignment>`

Trả về căn chỉnh mặt phẳng cho entity cha tại ``index`` này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
