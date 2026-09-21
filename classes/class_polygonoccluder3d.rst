:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PolygonOccluder3D.xml.

.. _class_PolygonOccluder3D:

PolygonOccluder3D
=================

**Kế thừa:** :ref:`Occluder3D<class_Occluder3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Hình đa giác 2D phẳng để sử dụng với occlusion culling trong :ref:`OccluderInstance3D<class_OccluderInstance3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PolygonOccluder3D** lưu trữ một hình đa giác có thể được engine sử dụng trong hệ thống occlusion culling. Khi một :ref:`OccluderInstance3D<class_OccluderInstance3D>` có **PolygonOccluder3D** được chọn trong editor, một trình chỉnh sửa sẽ xuất hiện ở phía trên viewport 3D, cho phép bạn thêm/xóa các điểm. Tất cả các điểm phải được đặt trên cùng một mặt phẳng 2D, điều đó có nghĩa là không thể tạo các hình dạng 3D tùy ý bằng một **PolygonOccluder3D** duy nhất. Để sử dụng các hình dạng 3D tùy ý làm occluder, hãy sử dụng :ref:`ArrayOccluder3D<class_ArrayOccluder3D>` hoặc tính năng baking của :ref:`OccluderInstance3D<class_OccluderInstance3D>` thay vào đó.

Xem tài liệu của :ref:`OccluderInstance3D<class_OccluderInstance3D>` để biết hướng dẫn thiết lập occlusion culling.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Occlusion culling <../tutorials/3d/occlusion_culling>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`polygon<class_PolygonOccluder3D_property_polygon>` | ``PackedVector2Array()`` |
   +-----------------------------------------------------+----------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PolygonOccluder3D_property_polygon:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **polygon** = ``PackedVector2Array()`` :ref:`🔗<class_PolygonOccluder3D_property_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_polygon**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_polygon**\ (\ )

Hình đa giác được sử dụng cho occlusion culling. Hình đa giác có thể lồi hoặc lõm, nhưng nên có ít điểm nhất có thể để tối đa hóa hiệu năng.

Hình đa giác *không được* có các đường thẳng giao nhau. Nếu không, quá trình tam giác hóa sẽ thất bại (và in ra một thông báo lỗi).

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
