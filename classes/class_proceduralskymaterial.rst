:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ProceduralSkyMaterial.xml.

.. _class_ProceduralSkyMaterial:

ProceduralSkyMaterial
=====================

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một material định nghĩa bầu trời đơn giản cho resource :ref:`Sky<class_Sky>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**ProceduralSkyMaterial** cung cấp cách nhanh chóng tạo background hiệu quả bằng cách định nghĩa các tham số procedural cho mặt trời, bầu trời và mặt đất. Bầu trời và mặt đất được định nghĩa bằng một màu chính, một màu tại đường chân trời và một đường cong easing để nội suy giữa chúng. Mặt trời được mô tả bằng vị trí trên bầu trời, màu sắc và góc tối đa tính từ mặt trời, tại đó đường cong easing kết thúc. Do đó, góc tối đa xác định kích thước của mặt trời trên bầu trời.

\ **ProceduralSkyMaterial** hỗ trợ tối đa 4 mặt trời, sử dụng màu sắc, energy, hướng và khoảng cách góc của bốn node :ref:`DirectionalLight3D<class_DirectionalLight3D>` đầu tiên trong scene. Điều này có nghĩa là các mặt trời được định nghĩa riêng lẻ bởi các thuộc tính của các :ref:`DirectionalLight3D<class_DirectionalLight3D>`\ s tương ứng và trên toàn cục bởi :ref:`sun_angle_max<class_ProceduralSkyMaterial_property_sun_angle_max>` và :ref:`sun_curve<class_ProceduralSkyMaterial_property_sun_curve>`.

\ **ProceduralSkyMaterial** sử dụng một shader nhẹ để vẽ bầu trời và do đó phù hợp với các cập nhật theo thời gian thực. Đây là lựa chọn tuyệt vời cho bầu trời đơn giản, ít tốn tài nguyên tính toán nhưng không chân thực. Nếu cần một lựa chọn procedural chân thực hơn, hãy sử dụng :ref:`PhysicalSkyMaterial<class_PhysicalSkyMaterial>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`energy_multiplier<class_ProceduralSkyMaterial_property_energy_multiplier>`               | ``1.0``                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`ground_bottom_color<class_ProceduralSkyMaterial_property_ground_bottom_color>`           | ``Color(0.2, 0.169, 0.133, 1)``      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`ground_curve<class_ProceduralSkyMaterial_property_ground_curve>`                         | ``0.02``                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`ground_energy_multiplier<class_ProceduralSkyMaterial_property_ground_energy_multiplier>` | ``1.0``                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`ground_horizon_color<class_ProceduralSkyMaterial_property_ground_horizon_color>`         | ``Color(0.6463, 0.6558, 0.6708, 1)`` |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`sky_cover<class_ProceduralSkyMaterial_property_sky_cover>`                               |                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`sky_cover_modulate<class_ProceduralSkyMaterial_property_sky_cover_modulate>`             | ``Color(1, 1, 1, 1)``                |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`sky_curve<class_ProceduralSkyMaterial_property_sky_curve>`                               | ``0.15``                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`sky_energy_multiplier<class_ProceduralSkyMaterial_property_sky_energy_multiplier>`       | ``1.0``                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`sky_horizon_color<class_ProceduralSkyMaterial_property_sky_horizon_color>`               | ``Color(0.6463, 0.6558, 0.6708, 1)`` |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`sky_top_color<class_ProceduralSkyMaterial_property_sky_top_color>`                       | ``Color(0.385, 0.454, 0.55, 1)``     |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`sun_angle_max<class_ProceduralSkyMaterial_property_sun_angle_max>`                       | ``30.0``                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`float<class_float>`         | :ref:`sun_curve<class_ProceduralSkyMaterial_property_sun_curve>`                               | ``0.15``                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+
   | :ref:`bool<class_bool>`           | :ref:`use_debanding<class_ProceduralSkyMaterial_property_use_debanding>`                       | ``true``                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------+--------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ProceduralSkyMaterial_property_energy_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **energy_multiplier** = ``1.0`` :ref:`🔗<class_ProceduralSkyMaterial_property_energy_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_energy_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_energy_multiplier**\ (\ )

Hệ số nhân độ sáng tổng thể của bầu trời. Giá trị cao hơn sẽ tạo ra bầu trời sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_ground_bottom_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **ground_bottom_color** = ``Color(0.2, 0.169, 0.133, 1)`` :ref:`🔗<class_ProceduralSkyMaterial_property_ground_bottom_color>`

.. rst-class:: classref-property-setget

- |void| **set_ground_bottom_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_ground_bottom_color**\ (\ )

Màu của mặt đất ở phía dưới. Hòa trộn với :ref:`ground_horizon_color<class_ProceduralSkyMaterial_property_ground_horizon_color>`.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_ground_curve:

.. rst-class:: classref-property

:ref:`float<class_float>` **ground_curve** = ``0.02`` :ref:`🔗<class_ProceduralSkyMaterial_property_ground_curve>`

.. rst-class:: classref-property-setget

- |void| **set_ground_curve**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ground_curve**\ (\ )

:ref:`ground_horizon_color<class_ProceduralSkyMaterial_property_ground_horizon_color>` chuyển dần vào :ref:`ground_bottom_color<class_ProceduralSkyMaterial_property_ground_bottom_color>` nhanh đến mức nào.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_ground_energy_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **ground_energy_multiplier** = ``1.0`` :ref:`🔗<class_ProceduralSkyMaterial_property_ground_energy_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_ground_energy_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ground_energy_multiplier**\ (\ )

Hệ số nhân cho màu mặt đất. Giá trị cao hơn sẽ làm mặt đất sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_ground_horizon_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **ground_horizon_color** = ``Color(0.6463, 0.6558, 0.6708, 1)`` :ref:`🔗<class_ProceduralSkyMaterial_property_ground_horizon_color>`

.. rst-class:: classref-property-setget

- |void| **set_ground_horizon_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_ground_horizon_color**\ (\ )

Màu của mặt đất tại đường chân trời. Hòa trộn với :ref:`ground_bottom_color<class_ProceduralSkyMaterial_property_ground_bottom_color>`.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_cover:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **sky_cover** :ref:`🔗<class_ProceduralSkyMaterial_property_sky_cover>`

.. rst-class:: classref-property-setget

- |void| **set_sky_cover**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_sky_cover**\ (\ )

Texture sky cover được sử dụng. Texture này phải sử dụng phép chiếu equirectangular (tương tự :ref:`PanoramaSkyMaterial<class_PanoramaSkyMaterial>`). Màu của texture sẽ được *cộng* vào màu bầu trời hiện có và được nhân với :ref:`sky_energy_multiplier<class_ProceduralSkyMaterial_property_sky_energy_multiplier>` và :ref:`sky_cover_modulate<class_ProceduralSkyMaterial_property_sky_cover_modulate>`. Texture này chủ yếu phù hợp để hiển thị các ngôi sao vào ban đêm, nhưng cũng có thể được dùng để hiển thị mây vào ban ngày hoặc ban đêm (với hình ảnh không chính xác về mặt vật lý).

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_cover_modulate:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **sky_cover_modulate** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_ProceduralSkyMaterial_property_sky_cover_modulate>`

.. rst-class:: classref-property-setget

- |void| **set_sky_cover_modulate**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_sky_cover_modulate**\ (\ )

Màu phủ áp dụng cho texture :ref:`sky_cover<class_ProceduralSkyMaterial_property_sky_cover>`. Có thể dùng để thay đổi màu hoặc độ mờ của sky cover độc lập với energy của bầu trời, rất hữu ích cho các chuyển tiếp ngày/đêm hoặc thời tiết. Chỉ có hiệu lực nếu một texture được định nghĩa trong :ref:`sky_cover<class_ProceduralSkyMaterial_property_sky_cover>`.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_curve:

.. rst-class:: classref-property

:ref:`float<class_float>` **sky_curve** = ``0.15`` :ref:`🔗<class_ProceduralSkyMaterial_property_sky_curve>`

.. rst-class:: classref-property-setget

- |void| **set_sky_curve**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sky_curve**\ (\ )

:ref:`sky_horizon_color<class_ProceduralSkyMaterial_property_sky_horizon_color>` chuyển dần vào :ref:`sky_top_color<class_ProceduralSkyMaterial_property_sky_top_color>` nhanh đến mức nào.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_energy_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **sky_energy_multiplier** = ``1.0`` :ref:`🔗<class_ProceduralSkyMaterial_property_sky_energy_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_sky_energy_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sky_energy_multiplier**\ (\ )

Hệ số nhân cho màu bầu trời. Giá trị cao hơn sẽ làm bầu trời sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_horizon_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **sky_horizon_color** = ``Color(0.6463, 0.6558, 0.6708, 1)`` :ref:`🔗<class_ProceduralSkyMaterial_property_sky_horizon_color>`

.. rst-class:: classref-property-setget

- |void| **set_sky_horizon_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_sky_horizon_color**\ (\ )

Màu của bầu trời tại đường chân trời. Hòa trộn với :ref:`sky_top_color<class_ProceduralSkyMaterial_property_sky_top_color>`.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sky_top_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **sky_top_color** = ``Color(0.385, 0.454, 0.55, 1)`` :ref:`🔗<class_ProceduralSkyMaterial_property_sky_top_color>`

.. rst-class:: classref-property-setget

- |void| **set_sky_top_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_sky_top_color**\ (\ )

Màu của bầu trời ở phía trên. Hòa trộn với :ref:`sky_horizon_color<class_ProceduralSkyMaterial_property_sky_horizon_color>`.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sun_angle_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **sun_angle_max** = ``30.0`` :ref:`🔗<class_ProceduralSkyMaterial_property_sun_angle_max>`

.. rst-class:: classref-property-setget

- |void| **set_sun_angle_max**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sun_angle_max**\ (\ )

Khoảng cách tính từ tâm mặt trời mà tại đó mặt trời mờ đi hoàn toàn.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_sun_curve:

.. rst-class:: classref-property

:ref:`float<class_float>` **sun_curve** = ``0.15`` :ref:`🔗<class_ProceduralSkyMaterial_property_sun_curve>`

.. rst-class:: classref-property-setget

- |void| **set_sun_curve**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sun_curve**\ (\ )

Mặt trời mờ đi giữa mép đĩa mặt trời và :ref:`sun_angle_max<class_ProceduralSkyMaterial_property_sun_angle_max>` nhanh đến mức nào.

.. rst-class:: classref-item-separator

----

.. _class_ProceduralSkyMaterial_property_use_debanding:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_debanding** = ``true`` :ref:`🔗<class_ProceduralSkyMaterial_property_use_debanding>`

.. rst-class:: classref-property-setget

- |void| **set_use_debanding**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_debanding**\ (\ )

Nếu ``true``, bật debanding. Debanding thêm một lượng noise nhỏ giúp giảm hiện tượng banding xuất hiện do các thay đổi màu mượt mà trên bầu trời.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
