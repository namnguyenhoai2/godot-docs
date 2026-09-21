:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicalSkyMaterial.xml.

.. _class_PhysicalSkyMaterial:

PhysicalSkyMaterial
===================

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một material định nghĩa bầu trời cho resource :ref:`Sky<class_Sky>` bằng một tập hợp các thuộc tính vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PhysicalSkyMaterial** sử dụng mô hình ánh sáng ban ngày giải tích Preetham để vẽ bầu trời dựa trên các thuộc tính vật lý. Kết quả là bầu trời thực tế hơn đáng kể so với :ref:`ProceduralSkyMaterial<class_ProceduralSkyMaterial>`, nhưng hơi chậm hơn và kém linh hoạt hơn.

**PhysicalSkyMaterial** chỉ hỗ trợ một mặt trời. Màu sắc, năng lượng và hướng của mặt trời được lấy từ :ref:`DirectionalLight3D<class_DirectionalLight3D>` đầu tiên trong scene tree.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`energy_multiplier<class_PhysicalSkyMaterial_property_energy_multiplier>`       | ``1.0``                          |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`ground_color<class_PhysicalSkyMaterial_property_ground_color>`                 | ``Color(0.1, 0.07, 0.034, 1)``   |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`mie_coefficient<class_PhysicalSkyMaterial_property_mie_coefficient>`           | ``0.005``                        |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`mie_color<class_PhysicalSkyMaterial_property_mie_color>`                       | ``Color(0.69, 0.729, 0.812, 1)`` |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`mie_eccentricity<class_PhysicalSkyMaterial_property_mie_eccentricity>`         | ``0.8``                          |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`night_sky<class_PhysicalSkyMaterial_property_night_sky>`                       |                                  |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`rayleigh_coefficient<class_PhysicalSkyMaterial_property_rayleigh_coefficient>` | ``2.0``                          |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`rayleigh_color<class_PhysicalSkyMaterial_property_rayleigh_color>`             | ``Color(0.3, 0.405, 0.6, 1)``    |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`sun_disk_scale<class_PhysicalSkyMaterial_property_sun_disk_scale>`             | ``1.0``                          |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`float<class_float>`         | :ref:`turbidity<class_PhysicalSkyMaterial_property_turbidity>`                       | ``10.0``                         |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+
   | :ref:`bool<class_bool>`           | :ref:`use_debanding<class_PhysicalSkyMaterial_property_use_debanding>`               | ``true``                         |
   +-----------------------------------+--------------------------------------------------------------------------------------+----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicalSkyMaterial_property_energy_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **energy_multiplier** = ``1.0`` :ref:`🔗<class_PhysicalSkyMaterial_property_energy_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_energy_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_energy_multiplier**\ (\ )

Hệ số nhân độ sáng tổng thể của bầu trời. Giá trị cao hơn tạo ra bầu trời sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_ground_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **ground_color** = ``Color(0.1, 0.07, 0.034, 1)`` :ref:`🔗<class_PhysicalSkyMaterial_property_ground_color>`

.. rst-class:: classref-property-setget

- |void| **set_ground_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_ground_color**\ (\ )

Điều chỉnh :ref:`Color<class_Color>` ở nửa dưới của bầu trời để biểu thị mặt đất.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_mie_coefficient:

.. rst-class:: classref-property

:ref:`float<class_float>` **mie_coefficient** = ``0.005`` :ref:`🔗<class_PhysicalSkyMaterial_property_mie_coefficient>`

.. rst-class:: classref-property-setget

- |void| **set_mie_coefficient**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mie_coefficient**\ (\ )

Điều khiển cường độ của `Mie scattering <https://en.wikipedia.org/wiki/Mie_scattering>`__ đối với bầu trời. Tán xạ Mie xảy ra khi ánh sáng va chạm với các hạt lớn hơn (chẳng hạn như nước). Trên Trái Đất, tán xạ Mie tạo ra màu trắng đục quanh mặt trời và đường chân trời.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_mie_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **mie_color** = ``Color(0.69, 0.729, 0.812, 1)`` :ref:`🔗<class_PhysicalSkyMaterial_property_mie_color>`

.. rst-class:: classref-property-setget

- |void| **set_mie_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_mie_color**\ (\ )

Điều khiển :ref:`Color<class_Color>` của hiệu ứng `Mie scattering <https://en.wikipedia.org/wiki/Mie_scattering>`__. Dù không chính xác về mặt vật lý, tùy chọn này cho phép tạo ra các hành tinh trông như ngoài hành tinh.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_mie_eccentricity:

.. rst-class:: classref-property

:ref:`float<class_float>` **mie_eccentricity** = ``0.8`` :ref:`🔗<class_PhysicalSkyMaterial_property_mie_eccentricity>`

.. rst-class:: classref-property-setget

- |void| **set_mie_eccentricity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mie_eccentricity**\ (\ )

Điều khiển hướng của `Mie scattering <https://en.wikipedia.org/wiki/Mie_scattering>`__. Giá trị ``1`` có nghĩa là khi ánh sáng chạm vào một hạt, nó truyền thẳng qua. Giá trị ``-1`` có nghĩa là toàn bộ ánh sáng bị tán xạ ngược.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_night_sky:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **night_sky** :ref:`🔗<class_PhysicalSkyMaterial_property_night_sky>`

.. rst-class:: classref-property-setget

- |void| **set_night_sky**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_night_sky**\ (\ )

:ref:`Texture2D<class_Texture2D>` cho bầu trời ban đêm. Giá trị này được thêm vào bầu trời, vì vậy nếu đủ sáng, nó có thể nhìn thấy vào ban ngày.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_rayleigh_coefficient:

.. rst-class:: classref-property

:ref:`float<class_float>` **rayleigh_coefficient** = ``2.0`` :ref:`🔗<class_PhysicalSkyMaterial_property_rayleigh_coefficient>`

.. rst-class:: classref-property-setget

- |void| **set_rayleigh_coefficient**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rayleigh_coefficient**\ (\ )

Điều khiển cường độ của `Rayleigh scattering <https://en.wikipedia.org/wiki/Rayleigh_scattering>`__. Tán xạ Rayleigh xảy ra khi ánh sáng va chạm với các hạt nhỏ. Đây là nguyên nhân tạo ra màu xanh lam của bầu trời.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_rayleigh_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **rayleigh_color** = ``Color(0.3, 0.405, 0.6, 1)`` :ref:`🔗<class_PhysicalSkyMaterial_property_rayleigh_color>`

.. rst-class:: classref-property-setget

- |void| **set_rayleigh_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_rayleigh_color**\ (\ )

Điều khiển :ref:`Color<class_Color>` của `Rayleigh scattering <https://en.wikipedia.org/wiki/Rayleigh_scattering>`__. Dù không chính xác về mặt vật lý, tùy chọn này cho phép tạo ra các hành tinh trông như ngoài hành tinh. Ví dụ: đặt giá trị này thành một :ref:`Color<class_Color>` màu đỏ sẽ tạo ra bầu khí quyển giống sao Hỏa cùng với hoàng hôn màu xanh lam tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_sun_disk_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **sun_disk_scale** = ``1.0`` :ref:`🔗<class_PhysicalSkyMaterial_property_sun_disk_scale>`

.. rst-class:: classref-property-setget

- |void| **set_sun_disk_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sun_disk_scale**\ (\ )

Đặt kích thước đĩa mặt trời. Giá trị mặc định dựa trên kích thước cảm nhận được của Sol khi nhìn từ Trái Đất.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_turbidity:

.. rst-class:: classref-property

:ref:`float<class_float>` **turbidity** = ``10.0`` :ref:`🔗<class_PhysicalSkyMaterial_property_turbidity>`

.. rst-class:: classref-property-setget

- |void| **set_turbidity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_turbidity**\ (\ )

Đặt độ dày của khí quyển. Độ đục cao tạo ra khí quyển trông như có sương mù, trong khi độ đục thấp tạo ra khí quyển trong hơn.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalSkyMaterial_property_use_debanding:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_debanding** = ``true`` :ref:`🔗<class_PhysicalSkyMaterial_property_use_debanding>`

.. rst-class:: classref-property-setget

- |void| **set_use_debanding**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_debanding**\ (\ )

Nếu ``true``, bật debanding. Debanding thêm một lượng nhiễu nhỏ để giúp giảm hiện tượng banding xuất hiện do sự thay đổi màu sắc mượt mà trên bầu trời.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
