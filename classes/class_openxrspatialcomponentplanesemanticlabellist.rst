:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRSpatialComponentPlaneSemanticLabelList.xml.

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList:

OpenXRSpatialComponentPlaneSemanticLabelList
============================================

**Experimental:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRSpatialComponentData<class_OpenXRSpatialComponentData>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đối tượng dùng để lưu trữ dữ liệu kết quả nhãn ngữ nghĩa của các mặt phẳng được truy vấn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng dùng để lưu trữ dữ liệu kết quả nhãn ngữ nghĩa của các mặt phẳng được truy vấn khi gọi :ref:`OpenXRSpatialEntityExtension.query_snapshot()<class_OpenXRSpatialEntityExtension_method_query_snapshot>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` | :ref:`get_plane_semantic_label<class_OpenXRSpatialComponentPlaneSemanticLabelList_method_get_plane_semantic_label>`\ (\ index\: :ref:`int<class_int>`\ ) |const| |
   +-------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel:

.. rst-class:: classref-enumeration

enum **PlaneSemanticLabel**: :ref:`🔗<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>`

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_constant_PLANE_SEMANTIC_LABEL_UNCATEGORIZED:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **PLANE_SEMANTIC_LABEL_UNCATEGORIZED** = ``1``

Mặt phẳng chưa được phân loại.

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_constant_PLANE_SEMANTIC_LABEL_FLOOR:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **PLANE_SEMANTIC_LABEL_FLOOR** = ``2``

Mặt phẳng biểu thị sàn.

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_constant_PLANE_SEMANTIC_LABEL_WALL:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **PLANE_SEMANTIC_LABEL_WALL** = ``3``

Mặt phẳng biểu thị tường.

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_constant_PLANE_SEMANTIC_LABEL_CEILING:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **PLANE_SEMANTIC_LABEL_CEILING** = ``4``

Mặt phẳng biểu thị trần nhà.

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_constant_PLANE_SEMANTIC_LABEL_TABLE:

.. rst-class:: classref-enumeration-constant

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **PLANE_SEMANTIC_LABEL_TABLE** = ``5``

Mặt phẳng biểu thị bề mặt của một chiếc bàn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRSpatialComponentPlaneSemanticLabelList_method_get_plane_semantic_label:

.. rst-class:: classref-method

:ref:`PlaneSemanticLabel<enum_OpenXRSpatialComponentPlaneSemanticLabelList_PlaneSemanticLabel>` **get_plane_semantic_label**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OpenXRSpatialComponentPlaneSemanticLabelList_method_get_plane_semantic_label>`

Trả về nhãn ngữ nghĩa của mặt phẳng cho thực thể cha tại ``index`` này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
