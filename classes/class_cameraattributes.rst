:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CameraAttributes.xml.

.. _class_CameraAttributes:

CameraAttributes
================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CameraAttributesPhysical<class_CameraAttributesPhysical>`, :ref:`CameraAttributesPractical<class_CameraAttributesPractical>`

Lớp cha cho các thiết lập camera.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểm soát các thuộc tính dành riêng cho camera, chẳng hạn như độ sâu trường ảnh và ghi đè phơi sáng.

Khi được sử dụng trong :ref:`WorldEnvironment<class_WorldEnvironment>`, nó cung cấp các thiết lập mặc định cho phơi sáng, tự động phơi sáng và độ sâu trường ảnh, được sử dụng bởi tất cả camera không có **CameraAttributes** riêng, bao gồm cả camera của editor. Khi được sử dụng trong :ref:`Camera3D<class_Camera3D>`, nó sẽ ghi đè mọi **CameraAttributes** được thiết lập trong :ref:`WorldEnvironment<class_WorldEnvironment>`. Khi được sử dụng trong :ref:`VoxelGI<class_VoxelGI>` hoặc :ref:`LightmapGI<class_LightmapGI>`, chỉ các thiết lập phơi sáng được sử dụng.

Xem thêm :ref:`Environment<class_Environment>` để biết các thiết lập môi trường 3D chung.

Đây là một lớp thuần ảo được :ref:`CameraAttributesPhysical<class_CameraAttributesPhysical>` và :ref:`CameraAttributesPractical<class_CameraAttributesPractical>` kế thừa.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`auto_exposure_enabled<class_CameraAttributes_property_auto_exposure_enabled>` | ``false`` |
   +---------------------------+-------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_scale<class_CameraAttributes_property_auto_exposure_scale>`     | ``0.4``   |
   +---------------------------+-------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_speed<class_CameraAttributes_property_auto_exposure_speed>`     | ``0.5``   |
   +---------------------------+-------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`exposure_multiplier<class_CameraAttributes_property_exposure_multiplier>`     | ``1.0``   |
   +---------------------------+-------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`exposure_sensitivity<class_CameraAttributes_property_exposure_sensitivity>`   | ``100.0`` |
   +---------------------------+-------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraAttributes_property_auto_exposure_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **auto_exposure_enabled** = ``false`` :ref:`🔗<class_CameraAttributes_property_auto_exposure_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_auto_exposure_enabled**\ (\ )

Nếu ``true``, bật chế độ tự động phơi sáng tonemapping của trình kết xuất cảnh. Nếu ``true``, trình kết xuất sẽ tự động xác định thiết lập phơi sáng để thích ứng với độ chiếu sáng của cảnh và nguồn sáng được quan sát.

\ **Lưu ý:** Tự động phơi sáng chỉ được hỗ trợ trong phương thức kết xuất Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributes_property_auto_exposure_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_scale** = ``0.4`` :ref:`🔗<class_CameraAttributes_property_auto_exposure_scale>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_scale**\ (\ )

Tỷ lệ của hiệu ứng tự động phơi sáng. Ảnh hưởng đến cường độ của tự động phơi sáng.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributes_property_auto_exposure_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_speed** = ``0.5`` :ref:`🔗<class_CameraAttributes_property_auto_exposure_speed>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_speed**\ (\ )

Tốc độ của hiệu ứng tự động phơi sáng. Ảnh hưởng đến thời gian cần thiết để camera thực hiện tự động phơi sáng.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributes_property_exposure_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **exposure_multiplier** = ``1.0`` :ref:`🔗<class_CameraAttributes_property_exposure_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_exposure_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_exposure_multiplier**\ (\ )

Hệ số nhân cho mức phơi sáng. Giá trị cao hơn tạo ra hình ảnh sáng hơn.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributes_property_exposure_sensitivity:

.. rst-class:: classref-property

:ref:`float<class_float>` **exposure_sensitivity** = ``100.0`` :ref:`🔗<class_CameraAttributes_property_exposure_sensitivity>`

.. rst-class:: classref-property-setget

- |void| **set_exposure_sensitivity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_exposure_sensitivity**\ (\ )

Độ nhạy của cảm biến camera, được đo bằng ISO. Độ nhạy cao hơn tạo ra hình ảnh sáng hơn.

Nếu :ref:`auto_exposure_enabled<class_CameraAttributes_property_auto_exposure_enabled>` là ``true``, giá trị này có thể được dùng như một phương pháp bù phơi sáng; việc tăng gấp đôi giá trị sẽ tăng giá trị phơi sáng (đo bằng EV100) lên 1 stop.

\ **Lưu ý:** Chỉ khả dụng khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` được bật.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
