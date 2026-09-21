:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRFrameSynthesisExtension.xml.

.. _class_OpenXRFrameSynthesisExtension:

OpenXRFrameSynthesisExtension
=============================

**Kế thừa:** :ref:`OpenXRExtensionWrapper<class_OpenXRExtensionWrapper>` **<** :ref:`Object<class_Object>`

Extension tổng hợp khung hình OpenXR cho phép thực hiện reprojection nâng cao ở tốc độ khung hình thấp (hơn).

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này triển khai `OpenXR Frame synthesis extension <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_frame_synthesis>`__. Khi được bật trong cài đặt dự án và được XR runtime đang sử dụng hỗ trợ, việc tổng hợp khung hình sẽ sử dụng các kỹ thuật reprojection nâng cao để chèn thêm các khung hình, giúp trải nghiệm XR của bạn đạt tốc độ khung hình đầy đủ của thiết bị.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`enabled<class_OpenXRFrameSynthesisExtension_property_enabled>`                           | ``false`` |
   +-------------------------+------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`relax_frame_interval<class_OpenXRFrameSynthesisExtension_property_relax_frame_interval>` | ``false`` |
   +-------------------------+------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_available<class_OpenXRFrameSynthesisExtension_method_is_available>`\ (\ ) |const| |
   +-------------------------+--------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`skip_next_frame<class_OpenXRFrameSynthesisExtension_method_skip_next_frame>`\ (\ )   |
   +-------------------------+--------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRFrameSynthesisExtension_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``false`` :ref:`🔗<class_OpenXRFrameSynthesisExtension_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Bật tính năng tổng hợp khung hình. Khi ``true`` dữ liệu vector chuyển động và độ sâu được cung cấp cho XR runtime.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRFrameSynthesisExtension_property_relax_frame_interval:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **relax_frame_interval** = ``false`` :ref:`🔗<class_OpenXRFrameSynthesisExtension_property_relax_frame_interval>`

.. rst-class:: classref-property-setget

- |void| **set_relax_frame_interval**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_relax_frame_interval**\ (\ )

Nếu ``true``, điều này cho XR runtime biết rằng chúng ta sẽ cung cấp các khung hình ở tốc độ thấp hơn rất nhiều. Bật tùy chọn này khi bạn dự kiến ứng dụng sẽ chạy ở tốc độ khung hình thấp và muốn chèn nhiều khung hình được reprojection.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRFrameSynthesisExtension_method_is_available:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_available**\ (\ ) |const| :ref:`🔗<class_OpenXRFrameSynthesisExtension_method_is_available>`

Trả về ``true`` nếu tính năng tổng hợp khung hình được bật trong cài đặt dự án và XR runtime hiện tại hỗ trợ tính năng tổng hợp khung hình. Giá trị được trả về chỉ hợp lệ sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRFrameSynthesisExtension_method_skip_next_frame:

.. rst-class:: classref-method

|void| **skip_next_frame**\ (\ ) :ref:`🔗<class_OpenXRFrameSynthesisExtension_method_skip_next_frame>`

Xếp hàng để bỏ qua khung hình tiếp theo khi cung cấp dữ liệu vector chuyển động và độ sâu. Gọi phương thức này sau khi dịch chuyển player hoặc thực hiện hành động tương tự khiến player di chuyển, nhằm ngăn kết quả reprojection không chính xác do chuyển động này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
