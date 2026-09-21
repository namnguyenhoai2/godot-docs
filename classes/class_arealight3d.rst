:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AreaLight3D.xml.

.. _class_AreaLight3D:

AreaLight3D
===========

**Kế thừa:** :ref:`Light3D<class_Light3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đèn vùng, chẳng hạn như ống đèn neon hoặc màn hình.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đèn vùng là một loại node :ref:`Light3D<class_Light3D>` phát ra ánh sáng trên một vùng hai chiều có hình chữ nhật. Ánh sáng bị suy giảm theo khoảng cách. Có thể cấu hình mức suy giảm này bằng cách thay đổi energy, :ref:`area_attenuation<class_AreaLight3D_property_area_attenuation>` và :ref:`area_range<class_AreaLight3D_property_area_range>`.

Ánh sáng được phát ra theo hướng -Z của global basis của node. Đối với đèn không xoay, điều này có nghĩa là ánh sáng được phát ra về phía trước, chiếu sáng mặt trước của mô hình 3D (xem :ref:`Vector3.FORWARD<class_Vector3_constant_FORWARD>` và :ref:`Vector3.MODEL_FRONT<class_Vector3_constant_MODEL_FRONT>`).

Đèn vùng có thể tạo bóng mềm bằng PCSS; bạn có thể điều khiển điều này bằng cách điều chỉnh tham số size. Shadow map được vẽ từ tâm của đèn.

\ **Lưu ý:** Đèn vùng có hỗ trợ hạn chế trong các renderer Mobile và Compatibility. Trong renderer Mobile, kích thước của penumbra không thay đổi như mong đợi khi sử dụng PCSS. Trong Compatibility, đèn vùng không thể tạo bóng.

\ **Cảnh báo:** Bóng do đèn vùng tạo ra có thể trông không chính xác nếu đối tượng tạo bóng không có đủ subdivisions và ở quá gần đèn vùng. Đây là hạn chế tương tự như chế độ bóng Dual Paraboloid trên một :ref:`OmniLight3D<class_OmniLight3D>`.

\ **Hiệu năng:** Đèn vùng yêu cầu GPU xử lý nhiều hơn so với đèn omni và đèn spot. Trong Forward+, sẽ phát sinh thêm chi phí GPU trên *tất cả* các đối tượng được render ngay khi có một đèn vùng trong frustum nhìn thấy (do bản chất của clustered lighting). Hãy cân nhắc chỉ sử dụng chúng cho các cảnh điện ảnh hoặc khi nhắm đến các thiết bị cao cấp.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D lights and shadows <../tutorials/3d/lights_and_shadows.html#area-light>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`         | :ref:`area_attenuation<class_AreaLight3D_property_area_attenuation>`           | ``1.0``                                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`           | :ref:`area_normalize_energy<class_AreaLight3D_property_area_normalize_energy>` | ``true``                                                                      |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`         | :ref:`area_range<class_AreaLight3D_property_area_range>`                       | ``5.0``                                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`     | :ref:`area_size<class_AreaLight3D_property_area_size>`                         | ``Vector2(1, 1)``                                                             |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`area_texture<class_AreaLight3D_property_area_texture>`                   |                                                                               |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`         | light_size                                                                     | ``0.5`` (overrides :ref:`Light3D<class_Light3D_property_light_size>`)         |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`         | shadow_normal_bias                                                             | ``1.0`` (overrides :ref:`Light3D<class_Light3D_property_shadow_normal_bias>`) |
   +-----------------------------------+--------------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AreaLight3D_property_area_attenuation:

.. rst-class:: classref-property

:ref:`float<class_float>` **area_attenuation** = ``1.0`` :ref:`🔗<class_AreaLight3D_property_area_attenuation>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Điều khiển hàm suy giảm theo khoảng cách của đèn vùng này.

Giá trị ``0.0`` sẽ duy trì độ sáng không đổi trong phần lớn phạm vi, nhưng làm ánh sáng suy giảm mượt mà ở rìa phạm vi. Sử dụng giá trị ``2.0`` cho ánh sáng chính xác về mặt vật lý, vì giá trị này tạo ra mức suy giảm theo bình phương nghịch đảo phù hợp.

\ **Lưu ý:** Đặt attenuation thành ``2.0`` hoặc cao hơn có thể khiến các đối tượng ở xa nhận được rất ít ánh sáng, ngay cả khi chúng nằm trong phạm vi. Ví dụ, với phạm vi ``4096``, một đối tượng ở cách ``100`` đơn vị sẽ bị suy giảm theo hệ số ``0.0001``. Với độ sáng mặc định là ``1``, ánh sáng sẽ không thể nhìn thấy ở khoảng cách đó.

\ **Lưu ý:** Việc sử dụng các giá trị âm hoặc các giá trị lớn hơn ``10.0`` có thể dẫn đến kết quả không mong đợi.

.. rst-class:: classref-item-separator

----

.. _class_AreaLight3D_property_area_normalize_energy:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **area_normalize_energy** = ``true`` :ref:`🔗<class_AreaLight3D_property_area_normalize_energy>`

.. rst-class:: classref-property-setget

- |void| **set_area_normalize_energy**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_area_normalizing_energy**\ (\ )

Xác định liệu energy có được chuẩn hóa (chia) theo diện tích bề mặt của đèn hay không. Nếu đặt thành ``true``, việc thay đổi kích thước sẽ không ảnh hưởng đến tổng năng lượng phát ra và không làm thay đổi đáng kể độ sáng của cảnh.

.. rst-class:: classref-item-separator

----

.. _class_AreaLight3D_property_area_range:

.. rst-class:: classref-property

:ref:`float<class_float>` **area_range** = ``5.0`` :ref:`🔗<class_AreaLight3D_property_area_range>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Phạm vi của vùng tính bằng mét. Giá trị này xác định khoảng cách tối đa từ bất kỳ điểm nào trên vùng mà tại đó vùng vẫn có thể phát ra ánh sáng.

.. rst-class:: classref-item-separator

----

.. _class_AreaLight3D_property_area_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **area_size** = ``Vector2(1, 1)`` :ref:`🔗<class_AreaLight3D_property_area_size>`

.. rst-class:: classref-property-setget

- |void| **set_area_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_area_size**\ (\ )

Kích thước (chiều rộng và chiều cao) của vùng tính bằng mét.

.. rst-class:: classref-item-separator

----

.. _class_AreaLight3D_property_area_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **area_texture** :ref:`🔗<class_AreaLight3D_property_area_texture>`

.. rst-class:: classref-property-setget

- |void| **set_area_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_area_texture**\ (\ )

Một texture tùy chọn được sử dụng làm nguồn sáng. Việc thay đổi texture trong runtime có thể ảnh hưởng đến hiệu năng, vì texture cần được vẽ vào area light atlas với các mipmap đã lọc.

Nếu không được gán texture, đèn vùng sẽ phát ra ánh sáng đồng đều trên toàn bộ bề mặt.

\ **Lưu ý:** Texture của đèn vùng chỉ được hỗ trợ trong các phương thức render Forward+ và Mobile, không được hỗ trợ trong Compatibility. Để giảm ảnh hưởng đến hiệu năng khi chuyển đổi texture trong runtime, hãy đảm bảo mỗi chiều của texture vùng là bội số của 128 pixel hoặc là lũy thừa của hai. Điều này loại bỏ nhu cầu thực hiện một scaling pass, vốn làm chậm việc thay đổi texture. Texture không nhất thiết phải có dạng vuông để đạt hiệu quả tối ưu. Ví dụ về các kích thước texture tối ưu gồm 32x64, 128x128 và 256x384.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
