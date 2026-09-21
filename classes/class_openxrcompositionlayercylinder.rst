:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRCompositionLayerCylinder.xml.

.. _class_OpenXRCompositionLayerCylinder:

OpenXRCompositionLayerCylinder
==============================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một lớp composition OpenXR được render dưới dạng một lát cắt bên trong của hình trụ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một lớp composition OpenXR cho phép render một :ref:`SubViewport<class_SubViewport>` trên một lát cắt bên trong của hình trụ.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`aspect_ratio<class_OpenXRCompositionLayerCylinder_property_aspect_ratio>`           | ``1.0``       |
   +---------------------------+-------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`central_angle<class_OpenXRCompositionLayerCylinder_property_central_angle>`         | ``1.5707964`` |
   +---------------------------+-------------------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`     | :ref:`fallback_segments<class_OpenXRCompositionLayerCylinder_property_fallback_segments>` | ``10``        |
   +---------------------------+-------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`radius<class_OpenXRCompositionLayerCylinder_property_radius>`                       | ``1.0``       |
   +---------------------------+-------------------------------------------------------------------------------------------+---------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRCompositionLayerCylinder_property_aspect_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **aspect_ratio** = ``1.0`` :ref:`🔗<class_OpenXRCompositionLayerCylinder_property_aspect_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_aspect_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_aspect_ratio**\ (\ )

Tỷ lệ khung hình của lát cắt. Được dùng để thiết lập chiều cao tương ứng với chiều rộng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayerCylinder_property_central_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **central_angle** = ``1.5707964`` :ref:`🔗<class_OpenXRCompositionLayerCylinder_property_central_angle>`

.. rst-class:: classref-property-setget

- |void| **set_central_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_central_angle**\ (\ )

Góc ở tâm của hình trụ. Được dùng để thiết lập chiều rộng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayerCylinder_property_fallback_segments:

.. rst-class:: classref-property

:ref:`int<class_int>` **fallback_segments** = ``10`` :ref:`🔗<class_OpenXRCompositionLayerCylinder_property_fallback_segments>`

.. rst-class:: classref-property-setget

- |void| **set_fallback_segments**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fallback_segments**\ (\ )

Số lượng segment được sử dụng trong mesh dự phòng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayerCylinder_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``1.0`` :ref:`🔗<class_OpenXRCompositionLayerCylinder_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của hình trụ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
