:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFSpecGloss.xml.

.. _class_GLTFSpecGloss:

GLTFSpecGloss
=============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

glTF extension đã lưu trữ cho các material specular/glossy.

.. rst-class:: classref-introduction-group

Mô tả
-----

KHR_materials_pbrSpecularGlossiness là một glTF extension đã lưu trữ. Điều này có nghĩa là extension này đã lỗi thời và không được khuyến nghị cho các tệp mới. Tuy nhiên, extension này vẫn được hỗ trợ khi load các tệp cũ.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Load và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `KHR_materials_pbrSpecularGlossiness glTF extension spec <https://github.com/KhronosGroup/glTF/blob/main/extensions/2.0/Archived/KHR_materials_pbrSpecularGlossiness>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>` | :ref:`diffuse_factor<class_GLTFSpecGloss_property_diffuse_factor>`   | ``Color(1, 1, 1, 1)`` |
   +---------------------------+----------------------------------------------------------------------+-----------------------+
   | :ref:`Image<class_Image>` | :ref:`diffuse_img<class_GLTFSpecGloss_property_diffuse_img>`         |                       |
   +---------------------------+----------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>` | :ref:`gloss_factor<class_GLTFSpecGloss_property_gloss_factor>`       | ``1.0``               |
   +---------------------------+----------------------------------------------------------------------+-----------------------+
   | :ref:`Image<class_Image>` | :ref:`spec_gloss_img<class_GLTFSpecGloss_property_spec_gloss_img>`   |                       |
   +---------------------------+----------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>` | :ref:`specular_factor<class_GLTFSpecGloss_property_specular_factor>` | ``Color(1, 1, 1, 1)`` |
   +---------------------------+----------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFSpecGloss_property_diffuse_factor:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **diffuse_factor** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_GLTFSpecGloss_property_diffuse_factor>`

.. rst-class:: classref-property-setget

- |void| **set_diffuse_factor**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_diffuse_factor**\ (\ )

Hệ số diffuse được phản xạ của material.

.. rst-class:: classref-item-separator

----

.. _class_GLTFSpecGloss_property_diffuse_img:

.. rst-class:: classref-property

:ref:`Image<class_Image>` **diffuse_img** :ref:`🔗<class_GLTFSpecGloss_property_diffuse_img>`

.. rst-class:: classref-property-setget

- |void| **set_diffuse_img**\ (\ value\: :ref:`Image<class_Image>`\ ) - :ref:`Image<class_Image>` **get_diffuse_img**\ (\ )

Texture diffuse.

.. rst-class:: classref-item-separator

----

.. _class_GLTFSpecGloss_property_gloss_factor:

.. rst-class:: classref-property

:ref:`float<class_float>` **gloss_factor** = ``1.0`` :ref:`🔗<class_GLTFSpecGloss_property_gloss_factor>`

.. rst-class:: classref-property-setget

- |void| **set_gloss_factor**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gloss_factor**\ (\ )

Độ bóng hoặc độ mịn của material.

.. rst-class:: classref-item-separator

----

.. _class_GLTFSpecGloss_property_spec_gloss_img:

.. rst-class:: classref-property

:ref:`Image<class_Image>` **spec_gloss_img** :ref:`🔗<class_GLTFSpecGloss_property_spec_gloss_img>`

.. rst-class:: classref-property-setget

- |void| **set_spec_gloss_img**\ (\ value\: :ref:`Image<class_Image>`\ ) - :ref:`Image<class_Image>` **get_spec_gloss_img**\ (\ )

Texture specular-glossiness.

.. rst-class:: classref-item-separator

----

.. _class_GLTFSpecGloss_property_specular_factor:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **specular_factor** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_GLTFSpecGloss_property_specular_factor>`

.. rst-class:: classref-property-setget

- |void| **set_specular_factor**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_specular_factor**\ (\ )

Màu RGB specular của material. Kênh alpha không được sử dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
