:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CurveXYZTexture.xml.

.. _class_CurveXYZTexture:

CurveXYZTexture
===============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 1D trong đó các kênh màu đỏ, xanh lá và xanh dương tương ứng với các điểm trên 3 đường cong.

.. rst-class:: classref-introduction-group

Mô tả
-----

A 1D texture where the red, green, and blue color channels correspond to points on 3 unit :ref:`Curve<class_Curve>` resources. Compared to using separate :ref:`CurveTexture<class_CurveTexture>`\ s, this further simplifies the task of saving curves as image files.

Nếu bạn chỉ cần lưu một đường cong trong một texture duy nhất, hãy sử dụng :ref:`CurveTexture<class_CurveTexture>` thay thế. Xem thêm :ref:`GradientTexture1D<class_GradientTexture1D>` và :ref:`GradientTexture2D<class_GradientTexture2D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Curve<class_Curve>` | :ref:`curve_x<class_CurveXYZTexture_property_curve_x>` |                                                                                        |
   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Curve<class_Curve>` | :ref:`curve_y<class_CurveXYZTexture_property_curve_y>` |                                                                                        |
   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Curve<class_Curve>` | :ref:`curve_z<class_CurveXYZTexture_property_curve_z>` |                                                                                        |
   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | resource_local_to_scene                                | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`width<class_CurveXYZTexture_property_width>`     | ``256``                                                                                |
   +---------------------------+--------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CurveXYZTexture_property_curve_x:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **curve_x** :ref:`🔗<class_CurveXYZTexture_property_curve_x>`

.. rst-class:: classref-property-setget

- |void| **set_curve_x**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_curve_x**\ (\ )

:ref:`Curve<class_Curve>` được kết xuất lên kênh màu đỏ của texture. Nên là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CurveXYZTexture_property_curve_y:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **curve_y** :ref:`🔗<class_CurveXYZTexture_property_curve_y>`

.. rst-class:: classref-property-setget

- |void| **set_curve_y**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_curve_y**\ (\ )

:ref:`Curve<class_Curve>` được kết xuất lên kênh màu xanh lá của texture. Nên là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CurveXYZTexture_property_curve_z:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **curve_z** :ref:`🔗<class_CurveXYZTexture_property_curve_z>`

.. rst-class:: classref-property-setget

- |void| **set_curve_z**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_curve_z**\ (\ )

:ref:`Curve<class_Curve>` được kết xuất lên kênh màu xanh dương của texture. Nên là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CurveXYZTexture_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``256`` :ref:`🔗<class_CurveXYZTexture_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_width**\ (\ )

Chiều rộng của texture (tính bằng pixel). Giá trị cao hơn cho phép biểu diễn dữ liệu tần số cao tốt hơn (chẳng hạn như các thay đổi hướng đột ngột), nhưng làm tăng thời gian tạo và mức sử dụng bộ nhớ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
