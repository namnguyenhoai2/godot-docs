:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFLight.xml.

.. _class_GLTFLight:

GLTFLight
=========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một glTF light.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một light như được định nghĩa bởi extension glTF ``KHR_lights_punctual``.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Nạp và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `KHR_lights_punctual glTF extension spec <https://github.com/KhronosGroup/glTF/blob/main/extensions/2.0/Khronos/KHR_lights_punctual>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`   | :ref:`color<class_GLTFLight_property_color>`                       | ``Color(1, 1, 1, 1)`` |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`   | :ref:`inner_cone_angle<class_GLTFLight_property_inner_cone_angle>` | ``0.0``               |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`   | :ref:`intensity<class_GLTFLight_property_intensity>`               | ``1.0``               |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`String<class_String>` | :ref:`light_type<class_GLTFLight_property_light_type>`             | ``""``                |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`   | :ref:`outer_cone_angle<class_GLTFLight_property_outer_cone_angle>` | ``0.7853982``         |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`   | :ref:`range<class_GLTFLight_property_range>`                       | ``inf``               |
   +-----------------------------+--------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFLight<class_GLTFLight>`   | :ref:`from_dictionary<class_GLTFLight_method_from_dictionary>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static|                                                     |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFLight<class_GLTFLight>`   | :ref:`from_node<class_GLTFLight_method_from_node>`\ (\ light_node\: :ref:`Light3D<class_Light3D>`\ ) |static|                                                                       |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get_additional_data<class_GLTFLight_method_get_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`\ )                                                  |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_additional_data<class_GLTFLight_method_set_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`to_dictionary<class_GLTFLight_method_to_dictionary>`\ (\ ) |const|                                                                                                            |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Light3D<class_Light3D>`       | :ref:`to_node<class_GLTFLight_method_to_node>`\ (\ ) |const|                                                                                                                        |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_GLTFLight_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_GLTFLight_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

:ref:`Color<class_Color>` của light trong không gian tuyến tính. Mặc định là màu trắng. Màu đen khiến light không có hiệu ứng.

Giá trị này là tuyến tính để khớp với glTF, nhưng sẽ được chuyển đổi thành sRGB phi tuyến khi tạo node Godot :ref:`Light3D<class_Light3D>` lúc import, hoặc được chuyển đổi thành tuyến tính khi export :ref:`Light3D<class_Light3D>` của Godot sang glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_property_inner_cone_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **inner_cone_angle** = ``0.0`` :ref:`🔗<class_GLTFLight_property_inner_cone_angle>`

.. rst-class:: classref-property-setget

- |void| **set_inner_cone_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_inner_cone_angle**\ (\ )

Góc bên trong của hình nón trong một spotlight. Phải nhỏ hơn hoặc bằng góc hình nón bên ngoài.

Trong góc này, light có độ sáng tối đa. Giữa góc hình nón bên trong và bên ngoài, có sự chuyển tiếp từ độ sáng tối đa đến độ sáng bằng không. Khi tạo một :ref:`SpotLight3D<class_SpotLight3D>` của Godot, tỷ lệ giữa góc hình nón bên trong và bên ngoài được dùng để tính độ suy giảm của light.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_property_intensity:

.. rst-class:: classref-property

:ref:`float<class_float>` **intensity** = ``1.0`` :ref:`🔗<class_GLTFLight_property_intensity>`

.. rst-class:: classref-property-setget

- |void| **set_intensity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_intensity**\ (\ )

Cường độ của light. Giá trị này được biểu thị bằng candela (lumen trên steradian) đối với point light và spot light, và lux (lumen trên m²) đối với directional light. Khi tạo một light của Godot, giá trị này được chuyển đổi thành một hệ số không có đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_property_light_type:

.. rst-class:: classref-property

:ref:`String<class_String>` **light_type** = ``""`` :ref:`🔗<class_GLTFLight_property_light_type>`

.. rst-class:: classref-property-setget

- |void| **set_light_type**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_light_type**\ (\ )

Loại light. Các giá trị được Godot chấp nhận là "point", "spot" và "directional", lần lượt tương ứng với :ref:`OmniLight3D<class_OmniLight3D>`, :ref:`SpotLight3D<class_SpotLight3D>` và :ref:`DirectionalLight3D<class_DirectionalLight3D>` của Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_property_outer_cone_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **outer_cone_angle** = ``0.7853982`` :ref:`🔗<class_GLTFLight_property_outer_cone_angle>`

.. rst-class:: classref-property-setget

- |void| **set_outer_cone_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_outer_cone_angle**\ (\ )

Góc bên ngoài của hình nón trong một spotlight. Phải lớn hơn hoặc bằng góc bên trong.

Tại góc này, light giảm xuống độ sáng bằng không. Giữa góc hình nón bên trong và bên ngoài, có sự chuyển tiếp từ độ sáng tối đa đến độ sáng bằng không. Nếu góc này là nửa vòng tròn, spotlight sẽ phát sáng theo mọi hướng. Khi tạo một :ref:`SpotLight3D<class_SpotLight3D>` của Godot, góc hình nón bên ngoài được dùng làm góc của spotlight.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_property_range:

.. rst-class:: classref-property

:ref:`float<class_float>` **range** = ``inf`` :ref:`🔗<class_GLTFLight_property_range>`

.. rst-class:: classref-property-setget

- |void| **set_range**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_range**\ (\ )

Phạm vi của light, vượt quá phạm vi này thì light không có hiệu ứng. Các glTF light không được định nghĩa range sẽ hoạt động như light vật lý (có phạm vi vô hạn). Khi tạo một light của Godot, range được giới hạn ở ``4096.0``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_GLTFLight_method_from_dictionary:

.. rst-class:: classref-method

:ref:`GLTFLight<class_GLTFLight>` **from_dictionary**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| :ref:`🔗<class_GLTFLight_method_from_dictionary>`

Tạo một instance GLTFLight mới bằng cách phân tích :ref:`Dictionary<class_Dictionary>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_method_from_node:

.. rst-class:: classref-method

:ref:`GLTFLight<class_GLTFLight>` **from_node**\ (\ light_node\: :ref:`Light3D<class_Light3D>`\ ) |static| :ref:`🔗<class_GLTFLight_method_from_node>`

Tạo một instance GLTFLight mới từ node :ref:`Light3D<class_Light3D>` của Godot đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_method_get_additional_data:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_GLTFLight_method_get_additional_data>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_method_set_additional_data:

.. rst-class:: classref-method

|void| **set_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GLTFLight_method_set_additional_data>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_method_to_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **to_dictionary**\ (\ ) |const| :ref:`🔗<class_GLTFLight_method_to_dictionary>`

Serialize instance GLTFLight này thành một :ref:`Dictionary<class_Dictionary>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFLight_method_to_node:

.. rst-class:: classref-method

:ref:`Light3D<class_Light3D>` **to_node**\ (\ ) |const| :ref:`🔗<class_GLTFLight_method_to_node>`

Chuyển đổi instance GLTFLight này thành một node :ref:`Light3D<class_Light3D>` của Godot.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
