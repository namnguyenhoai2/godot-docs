:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/BoxOccluder3D.xml.

.. _class_BoxOccluder3D:

BoxOccluder3D
=============

**Kế thừa:** :ref:`Occluder3D<class_Occluder3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Hình hộp dùng cho việc loại bỏ vật bị che khuất (occlusion culling) trong :ref:`OccluderInstance3D<class_OccluderInstance3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**BoxOccluder3D** lưu trữ một hình hộp có thể được engine sử dụng trong hệ thống loại bỏ vật bị che khuất (occlusion culling).

Xem tài liệu của :ref:`OccluderInstance3D<class_OccluderInstance3D>` để biết hướng dẫn thiết lập tính năng loại bỏ vật bị che khuất (occlusion culling).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Occlusion culling <../tutorials/3d/occlusion_culling>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_BoxOccluder3D_property_size>` | ``Vector3(1, 1, 1)`` |
   +-------------------------------+------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoxOccluder3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_BoxOccluder3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của hình hộp theo đơn vị 3D.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
