:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GradientTexture1D.xml.

.. _class_GradientTexture1D:

GradientTexture1D
=================

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture 1D sử dụng các màu thu được từ một :ref:`Gradient<class_Gradient>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Texture 1D lấy các màu từ một :ref:`Gradient<class_Gradient>` để điền dữ liệu texture. Texture được điền bằng cách lấy mẫu gradient cho từng pixel. Do đó, texture không nhất thiết thể hiện bản sao chính xác của gradient, vì có thể bỏ sót một số màu nếu không có đủ pixel. Xem thêm :ref:`GradientTexture2D<class_GradientTexture2D>`, :ref:`CurveTexture<class_CurveTexture>` và :ref:`CurveXYZTexture<class_CurveXYZTexture>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Gradient<class_Gradient>` | :ref:`gradient<class_GradientTexture1D_property_gradient>` |                                                                                        |
   +---------------------------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | resource_local_to_scene                                    | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +---------------------------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`use_hdr<class_GradientTexture1D_property_use_hdr>`   | ``false``                                                                              |
   +---------------------------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`width<class_GradientTexture1D_property_width>`       | ``256``                                                                                |
   +---------------------------------+------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GradientTexture1D_property_gradient:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **gradient** :ref:`🔗<class_GradientTexture1D_property_gradient>`

.. rst-class:: classref-property-setget

- |void| **set_gradient**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_gradient**\ (\ )

:ref:`Gradient<class_Gradient>` được sử dụng để điền texture.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture1D_property_use_hdr:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_hdr** = ``false`` :ref:`🔗<class_GradientTexture1D_property_use_hdr>`

.. rst-class:: classref-property-setget

- |void| **set_use_hdr**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_hdr**\ (\ )

Nếu ``true``, texture được tạo sẽ hỗ trợ dải tương phản động cao (:ref:`Image.FORMAT_RGBAF<class_Image_constant_FORMAT_RGBAF>` format). Điều này cho phép các hiệu ứng phát sáng hoạt động nếu :ref:`Environment.glow_enabled<class_Environment_property_glow_enabled>` là ``true``. Nếu ``false``, texture được tạo sẽ sử dụng dải tương phản động thấp; các màu quá sáng sẽ bị giới hạn (:ref:`Image.FORMAT_RGBA8<class_Image_constant_FORMAT_RGBA8>` format).

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture1D_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``256`` :ref:`🔗<class_GradientTexture1D_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_width**\ (\ )

Số lượng mẫu màu sẽ được lấy từ :ref:`Gradient<class_Gradient>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
