:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ArrayOccluder3D.xml.

.. _class_ArrayOccluder3D:

ArrayOccluder3D
===============

**Kế thừa:** :ref:`Occluder3D<class_Occluder3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Hình đa giác 3D để sử dụng với occlusion culling trong :ref:`OccluderInstance3D<class_OccluderInstance3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**ArrayOccluder3D** lưu trữ một hình đa giác 3D bất kỳ có thể được engine sử dụng bởi hệ thống occlusion culling. Tương tự như :ref:`ArrayMesh<class_ArrayMesh>`, nhưng dành cho các occluder.

Xem tài liệu của :ref:`OccluderInstance3D<class_OccluderInstance3D>` để biết hướng dẫn thiết lập occlusion culling.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Occlusion culling <../tutorials/3d/occlusion_culling>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------+--------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`indices<class_ArrayOccluder3D_property_indices>`   | ``PackedInt32Array()``   |
   +-----------------------------------------------------+----------------------------------------------------------+--------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`vertices<class_ArrayOccluder3D_property_vertices>` | ``PackedVector3Array()`` |
   +-----------------------------------------------------+----------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`set_arrays<class_ArrayOccluder3D_method_set_arrays>`\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`, indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) |
   +--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ArrayOccluder3D_property_indices:

.. rst-class:: classref-property

:ref:`PackedInt32Array<class_PackedInt32Array>` **indices** = ``PackedInt32Array()`` :ref:`🔗<class_ArrayOccluder3D_property_indices>`

.. rst-class:: classref-property-setget

- |void| **set_indices**\ (\ value\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) - :ref:`PackedInt32Array<class_PackedInt32Array>` **get_indices**\ (\ )

Vị trí chỉ mục của occluder. Các chỉ mục xác định những điểm nào trong mảng :ref:`vertices<class_ArrayOccluder3D_property_vertices>` sẽ được vẽ và thứ tự vẽ.

\ **Lưu ý:** Occluder luôn được cập nhật sau khi đặt giá trị này. Nếu tạo occluder bằng quy trình, hãy cân nhắc sử dụng :ref:`set_arrays()<class_ArrayOccluder3D_method_set_arrays>` thay thế để tránh cập nhật occluder hai lần khi tạo.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính gốc. Xem :ref:`PackedInt32Array<class_PackedInt32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_ArrayOccluder3D_property_vertices:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **vertices** = ``PackedVector3Array()`` :ref:`🔗<class_ArrayOccluder3D_property_vertices>`

.. rst-class:: classref-property-setget

- |void| **set_vertices**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_vertices**\ (\ )

Vị trí các đỉnh của occluder trong hệ tọa độ 3D cục bộ.

\ **Lưu ý:** Occluder luôn được cập nhật sau khi đặt giá trị này. Nếu tạo occluder bằng quy trình, hãy cân nhắc sử dụng :ref:`set_arrays()<class_ArrayOccluder3D_method_set_arrays>` thay thế để tránh cập nhật occluder hai lần khi tạo.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính gốc. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ArrayOccluder3D_method_set_arrays:

.. rst-class:: classref-method

|void| **set_arrays**\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`, indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_ArrayOccluder3D_method_set_arrays>`

Thiết lập :ref:`indices<class_ArrayOccluder3D_property_indices>` và :ref:`vertices<class_ArrayOccluder3D_property_vertices>`, đồng thời chỉ cập nhật occluder cuối cùng một lần sau khi cả hai giá trị được thiết lập.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
