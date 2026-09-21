:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderMesh.xml.

.. _class_PlaceholderMesh:

PlaceholderMesh
===============

**Kế thừa:** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp placeholder cho một mesh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng khi tải một project sử dụng một subclass của :ref:`Mesh<class_Mesh>` trong 2 trường hợp:

- Khi chạy project được export ở chế độ dedicated server, chỉ các kích thước của texture được giữ lại (vì chúng có thể được sử dụng cho mục đích gameplay hoặc để định vị các phần tử khác). Điều này giúp giảm đáng kể kích thước của PCK được export.

- Khi subclass này bị thiếu do sử dụng một phiên bản hoặc bản build engine khác (ví dụ: các module bị vô hiệu hóa).

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`aabb<class_PlaceholderMesh_property_aabb>` | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +-------------------------+--------------------------------------------------+----------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PlaceholderMesh_property_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_PlaceholderMesh_property_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_aabb**\ (\ )

:ref:`AABB<class_AABB>` nhỏ nhất bao quanh mesh này trong local space.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
