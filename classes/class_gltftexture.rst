:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFTexture.xml.

.. _class_GLTFTexture:

GLTFTexture
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

GLTFTexture đại diện cho một texture trong tệp glTF.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tải và lưu tệp runtime <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------+--------+
   | :ref:`int<class_int>` | :ref:`sampler<class_GLTFTexture_property_sampler>`     | ``-1`` |
   +-----------------------+--------------------------------------------------------+--------+
   | :ref:`int<class_int>` | :ref:`src_image<class_GLTFTexture_property_src_image>` | ``-1`` |
   +-----------------------+--------------------------------------------------------+--------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFTexture_property_sampler:

.. rst-class:: classref-property

:ref:`int<class_int>` **sampler** = ``-1`` :ref:`🔗<class_GLTFTexture_property_sampler>`

.. rst-class:: classref-property-setget

- |void| **set_sampler**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sampler**\ (\ )

ID của texture sampler sẽ được sử dụng khi lấy mẫu hình ảnh. Nếu là -1, sampler mặc định sẽ được sử dụng (lọc tuyến tính và wrapping lặp lại theo cả hai trục).

.. rst-class:: classref-item-separator

----

.. _class_GLTFTexture_property_src_image:

.. rst-class:: classref-property

:ref:`int<class_int>` **src_image** = ``-1`` :ref:`🔗<class_GLTFTexture_property_src_image>`

.. rst-class:: classref-property-setget

- |void| **set_src_image**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_src_image**\ (\ )

Chỉ mục của hình ảnh được liên kết với texture này, xem :ref:`GLTFState.get_images()<class_GLTFState_method_get_images>`. Nếu là -1, texture này chưa được gán hình ảnh.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
