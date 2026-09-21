:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PanoramaSkyMaterial.xml.

.. _class_PanoramaSkyMaterial:

PanoramaSkyMaterial
===================

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một material cung cấp texture đặc biệt cho một :ref:`Sky<class_Sky>`, thường là một panorama HDR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource được tham chiếu trong :ref:`Sky<class_Sky>` và được dùng để vẽ background. **PanoramaSkyMaterial** hoạt động tương tự như skybox trong các engine khác, ngoại trừ việc nó sử dụng sky map dạng equirectangular thay vì :ref:`Cubemap<class_Cubemap>`.

Bạn nên sử dụng panorama HDR để có phản chiếu chính xác, chất lượng cao. Godot hỗ trợ các định dạng ảnh Radiance HDR (``.hdr``) và OpenEXR (``.exr``) cho mục đích này.

Bạn có thể sử dụng `this tool <https://danilw.github.io/GLSL-howto/cubemap_to_panorama_js/cubemap_to_panorama.html>`__ để chuyển đổi cubemap thành sky map dạng equirectangular.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`         | :ref:`energy_multiplier<class_PanoramaSkyMaterial_property_energy_multiplier>` | ``1.0``  |
   +-----------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`           | :ref:`filter<class_PanoramaSkyMaterial_property_filter>`                       | ``true`` |
   +-----------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`panorama<class_PanoramaSkyMaterial_property_panorama>`                   |          |
   +-----------------------------------+--------------------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PanoramaSkyMaterial_property_energy_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **energy_multiplier** = ``1.0`` :ref:`🔗<class_PanoramaSkyMaterial_property_energy_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_energy_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_energy_multiplier**\ (\ )

Hệ số nhân độ sáng tổng thể của bầu trời. Giá trị cao hơn sẽ tạo ra bầu trời sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_PanoramaSkyMaterial_property_filter:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter** = ``true`` :ref:`🔗<class_PanoramaSkyMaterial_property_filter>`

.. rst-class:: classref-property-setget

- |void| **set_filtering_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_filtering_enabled**\ (\ )

Một giá trị boolean xác định texture background có được filtering hay không.

.. rst-class:: classref-item-separator

----

.. _class_PanoramaSkyMaterial_property_panorama:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **panorama** :ref:`🔗<class_PanoramaSkyMaterial_property_panorama>`

.. rst-class:: classref-property-setget

- |void| **set_panorama**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_panorama**\ (\ )

:ref:`Texture2D<class_Texture2D>` được áp dụng cho **PanoramaSkyMaterial**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
