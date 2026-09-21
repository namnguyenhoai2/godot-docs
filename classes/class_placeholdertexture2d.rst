:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderTexture2D.xml.

.. _class_PlaceholderTexture2D:

PlaceholderTexture2D
====================

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp placeholder cho texture 2 chiều.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng khi tải một project sử dụng lớp con :ref:`Texture2D<class_Texture2D>` trong 2 trường hợp:

- Khi chạy project được export ở chế độ dedicated server, chỉ kích thước của texture được giữ lại (vì chúng có thể được sử dụng cho gameplay hoặc để định vị các phần tử khác). Điều này cho phép giảm đáng kể kích thước của PCK đã export.

- Khi lớp con này bị thiếu do sử dụng một phiên bản hoặc bản build khác của engine (ví dụ: các module bị vô hiệu hóa).

\ **Lưu ý:** Lớp này không được thiết kế để sử dụng như một texture thực tế cho việc render. Không đảm bảo lớp này hoạt động như texture trong shader hoặc material (ví dụ: khi tính UV).

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | resource_local_to_scene                               | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`size<class_PlaceholderTexture2D_property_size>` | ``Vector2(1, 1)``                                                                      |
   +-------------------------------+-------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PlaceholderTexture2D_property_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **size** = ``Vector2(1, 1)`` :ref:`🔗<class_PlaceholderTexture2D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_size**\ (\ )

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
