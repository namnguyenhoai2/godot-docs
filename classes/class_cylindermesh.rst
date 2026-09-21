:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CylinderMesh.xml.

.. _class_CylinderMesh:

CylinderMesh
============

**Kế thừa:** :ref:`PrimitiveMesh<class_PrimitiveMesh>` **<** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp biểu diễn một :ref:`PrimitiveMesh<class_PrimitiveMesh>` hình trụ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp biểu diễn một :ref:`PrimitiveMesh<class_PrimitiveMesh>` hình trụ. Lớp này có thể được dùng để tạo hình nón bằng cách đặt thuộc tính :ref:`top_radius<class_CylinderMesh_property_top_radius>` hoặc :ref:`bottom_radius<class_CylinderMesh_property_bottom_radius>` thành ``0.0``.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`bottom_radius<class_CylinderMesh_property_bottom_radius>`     | ``0.5``  |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`cap_bottom<class_CylinderMesh_property_cap_bottom>`           | ``true`` |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`cap_top<class_CylinderMesh_property_cap_top>`                 | ``true`` |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`height<class_CylinderMesh_property_height>`                   | ``2.0``  |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`     | :ref:`radial_segments<class_CylinderMesh_property_radial_segments>` | ``64``   |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`     | :ref:`rings<class_CylinderMesh_property_rings>`                     | ``4``    |
   +---------------------------+---------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`top_radius<class_CylinderMesh_property_top_radius>`           | ``0.5``  |
   +---------------------------+---------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CylinderMesh_property_bottom_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **bottom_radius** = ``0.5`` :ref:`🔗<class_CylinderMesh_property_bottom_radius>`

.. rst-class:: classref-property-setget

- |void| **set_bottom_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bottom_radius**\ (\ )

Bán kính đáy của hình trụ. Nếu đặt thành ``0.0``, các mặt đáy sẽ không được tạo, tạo ra hình nón. Xem thêm :ref:`cap_bottom<class_CylinderMesh_property_cap_bottom>`.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_cap_bottom:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cap_bottom** = ``true`` :ref:`🔗<class_CylinderMesh_property_cap_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_cap_bottom**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_cap_bottom**\ (\ )

Nếu ``true``, tạo nắp ở đáy hình trụ. Có thể đặt thành ``false`` để tăng tốc quá trình tạo và render khi camera không bao giờ nhìn thấy nắp. Xem thêm :ref:`bottom_radius<class_CylinderMesh_property_bottom_radius>`.

\ **Lưu ý:** Nếu :ref:`bottom_radius<class_CylinderMesh_property_bottom_radius>` là ``0.0``, quá trình tạo nắp luôn bị bỏ qua ngay cả khi :ref:`cap_bottom<class_CylinderMesh_property_cap_bottom>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_cap_top:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cap_top** = ``true`` :ref:`🔗<class_CylinderMesh_property_cap_top>`

.. rst-class:: classref-property-setget

- |void| **set_cap_top**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_cap_top**\ (\ )

Nếu ``true``, tạo nắp ở đỉnh hình trụ. Có thể đặt thành ``false`` để tăng tốc quá trình tạo và render khi camera không bao giờ nhìn thấy nắp. Xem thêm :ref:`top_radius<class_CylinderMesh_property_top_radius>`.

\ **Lưu ý:** Nếu :ref:`top_radius<class_CylinderMesh_property_top_radius>` là ``0.0``, quá trình tạo nắp luôn bị bỏ qua ngay cả khi :ref:`cap_top<class_CylinderMesh_property_cap_top>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``2.0`` :ref:`🔗<class_CylinderMesh_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Chiều cao toàn phần của hình trụ.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_radial_segments:

.. rst-class:: classref-property

:ref:`int<class_int>` **radial_segments** = ``64`` :ref:`🔗<class_CylinderMesh_property_radial_segments>`

.. rst-class:: classref-property-setget

- |void| **set_radial_segments**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_radial_segments**\ (\ )

Số lượng phân đoạn theo bán kính trên hình trụ. Giá trị cao hơn tạo ra hình trụ/hình nón chi tiết hơn nhưng làm giảm hiệu năng.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_rings:

.. rst-class:: classref-property

:ref:`int<class_int>` **rings** = ``4`` :ref:`🔗<class_CylinderMesh_property_rings>`

.. rst-class:: classref-property-setget

- |void| **set_rings**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_rings**\ (\ )

Số lượng vòng cạnh dọc theo chiều cao của hình trụ. Việc thay đổi :ref:`rings<class_CylinderMesh_property_rings>` không tạo ra bất kỳ ảnh hưởng trực quan nào trừ khi dùng shader hoặc công cụ procedural mesh để thay đổi dữ liệu vertex. Giá trị cao hơn tạo ra nhiều subdivision hơn, có thể được dùng để tạo các hiệu ứng trông mượt mà hơn với shader hoặc công cụ procedural mesh (đổi lại là hiệu năng). Khi không thay đổi dữ liệu vertex bằng shader hoặc công cụ procedural mesh, nên giữ :ref:`rings<class_CylinderMesh_property_rings>` ở giá trị mặc định.

.. rst-class:: classref-item-separator

----

.. _class_CylinderMesh_property_top_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **top_radius** = ``0.5`` :ref:`🔗<class_CylinderMesh_property_top_radius>`

.. rst-class:: classref-property-setget

- |void| **set_top_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_top_radius**\ (\ )

Bán kính đỉnh của hình trụ. Nếu đặt thành ``0.0``, các mặt đỉnh sẽ không được tạo, tạo ra hình nón. Xem thêm :ref:`cap_top<class_CylinderMesh_property_cap_top>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
