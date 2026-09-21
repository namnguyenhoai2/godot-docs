:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationPathQueryResult3D.xml.

.. _class_NavigationPathQueryResult3D:

NavigationPathQueryResult3D
===========================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Biểu diễn kết quả của một truy vấn tìm đường 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class này lưu trữ kết quả của một truy vấn đường dẫn navigation 3D từ :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng NavigationPathQueryObjects <../tutorials/navigation/navigation_using_navigationpathqueryobjects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`path<class_NavigationPathQueryResult3D_property_path>`                     | ``PackedVector3Array()`` |
   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`path_length<class_NavigationPathQueryResult3D_property_path_length>`       | ``0.0``                  |
   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>`     | :ref:`path_owner_ids<class_NavigationPathQueryResult3D_property_path_owner_ids>` | ``PackedInt64Array()``   |
   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]  | :ref:`path_rids<class_NavigationPathQueryResult3D_property_path_rids>`           | ``[]``                   |
   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`path_types<class_NavigationPathQueryResult3D_property_path_types>`         | ``PackedInt32Array()``   |
   +-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+--------------------------------------------------------------------+
   | |void| | :ref:`reset<class_NavigationPathQueryResult3D_method_reset>`\ (\ ) |
   +--------+--------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_NavigationPathQueryResult3D_PathSegmentType:

.. rst-class:: classref-enumeration

enum **PathSegmentType**: :ref:`🔗<enum_NavigationPathQueryResult3D_PathSegmentType>`

.. _class_NavigationPathQueryResult3D_constant_PATH_SEGMENT_TYPE_REGION:

.. rst-class:: classref-enumeration-constant

:ref:`PathSegmentType<enum_NavigationPathQueryResult3D_PathSegmentType>` **PATH_SEGMENT_TYPE_REGION** = ``0``

Segment này của path đi qua một region.

.. _class_NavigationPathQueryResult3D_constant_PATH_SEGMENT_TYPE_LINK:

.. rst-class:: classref-enumeration-constant

:ref:`PathSegmentType<enum_NavigationPathQueryResult3D_PathSegmentType>` **PATH_SEGMENT_TYPE_LINK** = ``1``

Segment này của path đi qua một link.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationPathQueryResult3D_property_path:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **path** = ``PackedVector3Array()`` :ref:`🔗<class_NavigationPathQueryResult3D_property_path>`

.. rst-class:: classref-property-setget

- |void| **set_path**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_path**\ (\ )

Mảng path thu được từ truy vấn navigation. Tất cả vị trí trong mảng path đều sử dụng tọa độ global. Nếu không tùy chỉnh các tham số truy vấn, đây chính là path được trả về bởi :ref:`NavigationServer3D.map_get_path()<class_NavigationServer3D_method_map_get_path>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryResult3D_property_path_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_length** = ``0.0`` :ref:`🔗<class_NavigationPathQueryResult3D_property_path_length>`

.. rst-class:: classref-property-setget

- |void| **set_path_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_length**\ (\ )

Trả về độ dài của path.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryResult3D_property_path_owner_ids:

.. rst-class:: classref-property

:ref:`PackedInt64Array<class_PackedInt64Array>` **path_owner_ids** = ``PackedInt64Array()`` :ref:`🔗<class_NavigationPathQueryResult3D_property_path_owner_ids>`

.. rst-class:: classref-property-setget

- |void| **set_path_owner_ids**\ (\ value\: :ref:`PackedInt64Array<class_PackedInt64Array>`\ ) - :ref:`PackedInt64Array<class_PackedInt64Array>` **get_path_owner_ids**\ (\ )

Các ``ObjectID``\ s của các :ref:`Object<class_Object>`\ s quản lý những region và link mà mỗi điểm của path đi qua.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedInt64Array<class_PackedInt64Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryResult3D_property_path_rids:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **path_rids** = ``[]`` :ref:`🔗<class_NavigationPathQueryResult3D_property_path_rids>`

.. rst-class:: classref-property-setget

- |void| **set_path_rids**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_path_rids**\ (\ )

Các :ref:`RID<class_RID>`\ s của những region và link mà mỗi điểm của path đi qua.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPathQueryResult3D_property_path_types:

.. rst-class:: classref-property

:ref:`PackedInt32Array<class_PackedInt32Array>` **path_types** = ``PackedInt32Array()`` :ref:`🔗<class_NavigationPathQueryResult3D_property_path_types>`

.. rst-class:: classref-property-setget

- |void| **set_path_types**\ (\ value\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) - :ref:`PackedInt32Array<class_PackedInt32Array>` **get_path_types**\ (\ )

Kiểu của navigation primitive (region hoặc link) mà mỗi điểm của path đi qua.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedInt32Array<class_PackedInt32Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationPathQueryResult3D_method_reset:

.. rst-class:: classref-method

|void| **reset**\ (\ ) :ref:`🔗<class_NavigationPathQueryResult3D_method_reset>`

Đặt lại object kết quả về trạng thái ban đầu. Điều này hữu ích khi tái sử dụng object cho nhiều truy vấn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
