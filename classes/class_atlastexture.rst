:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AtlasTexture.xml.

.. _class_AtlasTexture:

AtlasTexture
============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture cắt ra một phần của Texture2D khác.

.. rst-class:: classref-introduction-group

Mô tả
-----

:ref:`Texture2D<class_Texture2D>` resource that draws only part of its :ref:`atlas<class_AtlasTexture_property_atlas>` texture, as defined by the :ref:`region<class_AtlasTexture_property_region>`. An additional :ref:`margin<class_AtlasTexture_property_margin>` can also be set, which is useful for small adjustments.

Nhiều resource **AtlasTexture** có thể được cắt từ cùng một :ref:`atlas<class_AtlasTexture_property_atlas>`. Đóng gói nhiều texture nhỏ hơn vào một texture lớn duy nhất giúp tối ưu chi phí bộ nhớ video và số lần render.

\ **Lưu ý:** Không thể sử dụng **AtlasTexture** trong một :ref:`AnimatedTexture<class_AnimatedTexture>`, và nó sẽ không được lát đúng cách trong các node như :ref:`TextureRect<class_TextureRect>` hoặc :ref:`Sprite2D<class_Sprite2D>`. Để lát một **AtlasTexture**, hãy thay đổi :ref:`region<class_AtlasTexture_property_region>` của nó.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`atlas<class_AtlasTexture_property_atlas>`             |                                                                                        |
   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`           | :ref:`filter_clip<class_AtlasTexture_property_filter_clip>` | ``false``                                                                              |
   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`         | :ref:`margin<class_AtlasTexture_property_margin>`           | ``Rect2(0, 0, 0, 0)``                                                                  |
   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`         | :ref:`region<class_AtlasTexture_property_region>`           | ``Rect2(0, 0, 0, 0)``                                                                  |
   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`           | resource_local_to_scene                                     | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-----------------------------------+-------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AtlasTexture_property_atlas:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **atlas** :ref:`🔗<class_AtlasTexture_property_atlas>`

.. rst-class:: classref-property-setget

- |void| **set_atlas**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_atlas**\ (\ )

Texture chứa atlas. Có thể là bất kỳ kiểu nào kế thừa từ :ref:`Texture2D<class_Texture2D>`, bao gồm cả **AtlasTexture** khác.

.. rst-class:: classref-item-separator

----

.. _class_AtlasTexture_property_filter_clip:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter_clip** = ``false`` :ref:`🔗<class_AtlasTexture_property_filter_clip>`

.. rst-class:: classref-property-setget

- |void| **set_filter_clip**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_filter_clip**\ (\ )

Nếu ``true``, vùng bên ngoài :ref:`region<class_AtlasTexture_property_region>` sẽ bị cắt để tránh hiện tượng lem của các pixel texture xung quanh.

.. rst-class:: classref-item-separator

----

.. _class_AtlasTexture_property_margin:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **margin** = ``Rect2(0, 0, 0, 0)`` :ref:`🔗<class_AtlasTexture_property_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_margin**\ (\ )

Lề xung quanh :ref:`region<class_AtlasTexture_property_region>`. Hữu ích cho những điều chỉnh nhỏ. Nếu :ref:`Rect2.size<class_Rect2_property_size>` của thuộc tính này ("w" và "h" trong trình chỉnh sửa) được đặt, texture được vẽ sẽ được thay đổi kích thước để vừa với lề.

.. rst-class:: classref-item-separator

----

.. _class_AtlasTexture_property_region:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **region** = ``Rect2(0, 0, 0, 0)`` :ref:`🔗<class_AtlasTexture_property_region>`

.. rst-class:: classref-property-setget

- |void| **set_region**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_region**\ (\ )

Vùng được dùng để vẽ :ref:`atlas<class_AtlasTexture_property_atlas>`. Nếu một trong hai chiều của kích thước vùng là ``0``, giá trị từ kích thước :ref:`atlas<class_AtlasTexture_property_atlas>` sẽ được sử dụng thay cho trục đó.

\ **Lưu ý:** Kích thước hình ảnh luôn là số nguyên, vì vậy kích thước vùng thực tế sẽ được làm tròn xuống.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
