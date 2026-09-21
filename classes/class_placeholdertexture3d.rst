:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderTexture3D.xml.

.. _class_PlaceholderTexture3D:

PlaceholderTexture3D
====================

**Kế thừa:** :ref:`Texture3D<class_Texture3D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp placeholder cho texture 3 chiều.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng khi tải một project sử dụng subclass :ref:`Texture3D<class_Texture3D>` trong 2 trường hợp:

- Khi chạy project được export ở dedicated server mode, chỉ các kích thước của texture được giữ lại (vì chúng có thể được sử dụng cho gameplay hoặc để định vị các thành phần khác). Điều này giúp giảm đáng kể kích thước của PCK được export.

- Khi subclass này bị thiếu do sử dụng phiên bản hoặc bản build engine khác (ví dụ: đã tắt các module).

\ **Lưu ý:** Lớp này không предназнач để được sử dụng như một texture thực tế cho việc rendering. Không đảm bảo lớp này hoạt động như texture trong shader hoặc material (ví dụ khi tính toán UV).

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-------------------------------------------------------+-----------------------+
   | :ref:`Vector3i<class_Vector3i>` | :ref:`size<class_PlaceholderTexture3D_property_size>` | ``Vector3i(1, 1, 1)`` |
   +---------------------------------+-------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PlaceholderTexture3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3i<class_Vector3i>` **size** = ``Vector3i(1, 1, 1)`` :ref:`🔗<class_PlaceholderTexture3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3i<class_Vector3i>`\ ) - :ref:`Vector3i<class_Vector3i>` **get_size**\ (\ )

Kích thước của texture (tính bằng pixel).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
