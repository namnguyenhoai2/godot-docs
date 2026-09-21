:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CameraAttributesPhysical.xml.

.. _class_CameraAttributesPhysical:

CameraAttributesPhysical
========================

**Kế thừa:** :ref:`CameraAttributes<class_CameraAttributes>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Các thiết lập camera dựa trên cơ sở vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CameraAttributesPhysical** được dùng để thiết lập các tùy chọn rendering dựa trên các thiết lập của camera dựa trên cơ sở vật lý. Nó chịu trách nhiệm về exposure, auto-exposure và depth of field.

When used in a :ref:`WorldEnvironment<class_WorldEnvironment>` it provides default settings for exposure, auto-exposure, and depth of field that will be used by all cameras without their own :ref:`CameraAttributes<class_CameraAttributes>`, including the editor camera. When used in a :ref:`Camera3D<class_Camera3D>` it will override any :ref:`CameraAttributes<class_CameraAttributes>` set in the :ref:`WorldEnvironment<class_WorldEnvironment>` and will override the :ref:`Camera3D<class_Camera3D>`\ s :ref:`Camera3D.far<class_Camera3D_property_far>`, :ref:`Camera3D.near<class_Camera3D_property_near>`, :ref:`Camera3D.fov<class_Camera3D_property_fov>`, and :ref:`Camera3D.keep_aspect<class_Camera3D_property_keep_aspect>` properties. When used in :ref:`VoxelGI<class_VoxelGI>` or :ref:`LightmapGI<class_LightmapGI>`, only the exposure settings will be used.

Các thiết lập mặc định предназнач dùng cho môi trường ngoài trời; bạn có thể tìm thấy các mẹo về thiết lập để sử dụng trong môi trường trong nhà trong tài liệu của từng thiết lập.

\ **Lưu ý:** Làm mờ depth of field chỉ được hỗ trợ trong các phương thức rendering Forward+ và Mobile, không được hỗ trợ trong Compatibility.

\ **Lưu ý:** Auto-exposure chỉ được hỗ trợ trong phương thức rendering Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Physical light and camera units <../tutorials/3d/physical_light_and_camera_units>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_max_exposure_value<class_CameraAttributesPhysical_property_auto_exposure_max_exposure_value>` | ``10.0``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_min_exposure_value<class_CameraAttributesPhysical_property_auto_exposure_min_exposure_value>` | ``-8.0``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`exposure_aperture<class_CameraAttributesPhysical_property_exposure_aperture>`                               | ``16.0``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`exposure_shutter_speed<class_CameraAttributesPhysical_property_exposure_shutter_speed>`                     | ``100.0``  |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`frustum_far<class_CameraAttributesPhysical_property_frustum_far>`                                           | ``4000.0`` |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`frustum_focal_length<class_CameraAttributesPhysical_property_frustum_focal_length>`                         | ``35.0``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`frustum_focus_distance<class_CameraAttributesPhysical_property_frustum_focus_distance>`                     | ``10.0``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>` | :ref:`frustum_near<class_CameraAttributesPhysical_property_frustum_near>`                                         | ``0.05``   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------+------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_fov<class_CameraAttributesPhysical_method_get_fov>`\ (\ ) |const| |
   +---------------------------+-----------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraAttributesPhysical_property_auto_exposure_max_exposure_value:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_max_exposure_value** = ``10.0`` :ref:`🔗<class_CameraAttributesPhysical_property_auto_exposure_max_exposure_value>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_max_exposure_value**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_max_exposure_value**\ (\ )

Độ chói tối đa (tính theo EV100) được sử dụng khi tính toán auto exposure. Khi tính toán độ chói trung bình của cảnh, các giá trị màu sẽ được giới hạn không thấp hơn giá trị này. Điều này giới hạn auto-exposure không phơi sáng dưới một độ sáng nhất định, tạo ra một điểm cắt tại đó cảnh sẽ vẫn sáng.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_auto_exposure_min_exposure_value:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_min_exposure_value** = ``-8.0`` :ref:`🔗<class_CameraAttributesPhysical_property_auto_exposure_min_exposure_value>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_min_exposure_value**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_min_exposure_value**\ (\ )

Độ chói tối thiểu (tính theo EV100) được sử dụng khi tính toán auto exposure. Khi tính toán độ chói trung bình của cảnh, các giá trị màu sẽ được giới hạn không thấp hơn giá trị này. Điều này giới hạn auto-exposure không phơi sáng trên một độ sáng nhất định, tạo ra một điểm cắt tại đó cảnh sẽ vẫn tối.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_exposure_aperture:

.. rst-class:: classref-property

:ref:`float<class_float>` **exposure_aperture** = ``16.0`` :ref:`🔗<class_CameraAttributesPhysical_property_exposure_aperture>`

.. rst-class:: classref-property-setget

- |void| **set_aperture**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_aperture**\ (\ )

Kích thước khẩu độ của camera, được đo bằng f-stop. F-stop là một tỷ lệ không có đơn vị giữa tiêu cự của camera và đường kính khẩu độ. Thiết lập khẩu độ cao sẽ tạo ra khẩu độ nhỏ hơn, dẫn đến hình ảnh tối hơn và tiêu điểm sắc nét hơn. Khẩu độ thấp tạo ra khẩu độ rộng, cho phép nhiều ánh sáng hơn và tạo ra hình ảnh sáng hơn nhưng kém tập trung hơn. Giá trị mặc định phù hợp với môi trường ngoài trời vào ban ngày (tức là để sử dụng với một :ref:`DirectionalLight3D<class_DirectionalLight3D>` mặc định); đối với ánh sáng trong nhà, giá trị từ 2 đến 4 sẽ phù hợp hơn.

Chỉ khả dụng khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_exposure_shutter_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **exposure_shutter_speed** = ``100.0`` :ref:`🔗<class_CameraAttributesPhysical_property_exposure_shutter_speed>`

.. rst-class:: classref-property-setget

- |void| **set_shutter_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_shutter_speed**\ (\ )

Thời gian màn trập mở và đóng, được đánh giá theo đơn vị ``1 / shutter_speed`` giây. Giá trị cao hơn sẽ cho phép ít ánh sáng hơn (dẫn đến hình ảnh tối hơn), trong khi giá trị thấp hơn sẽ cho phép nhiều ánh sáng hơn (dẫn đến hình ảnh sáng hơn).

Chỉ khả dụng khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_frustum_far:

.. rst-class:: classref-property

:ref:`float<class_float>` **frustum_far** = ``4000.0`` :ref:`🔗<class_CameraAttributesPhysical_property_frustum_far>`

.. rst-class:: classref-property-setget

- |void| **set_far**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_far**\ (\ )

Giá trị ghi đè cho :ref:`Camera3D.far<class_Camera3D_property_far>`. Được sử dụng nội bộ khi tính toán depth of field. Khi được gắn vào một :ref:`Camera3D<class_Camera3D>` dưới dạng :ref:`Camera3D.attributes<class_Camera3D_property_attributes>` của nó, thuộc tính này sẽ ghi đè thuộc tính :ref:`Camera3D.far<class_Camera3D_property_far>`.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_frustum_focal_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **frustum_focal_length** = ``35.0`` :ref:`🔗<class_CameraAttributesPhysical_property_frustum_focal_length>`

.. rst-class:: classref-property-setget

- |void| **set_focal_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_focal_length**\ (\ )

Khoảng cách giữa ống kính camera và khẩu độ camera, được đo bằng milimét. Kiểm soát field of view và depth of field. Tiêu cự lớn hơn sẽ tạo ra field of view nhỏ hơn và depth of field hẹp hơn, nghĩa là sẽ có ít đối tượng được lấy nét hơn. Tiêu cự nhỏ hơn sẽ tạo ra field of view rộng hơn và depth of field lớn hơn, nghĩa là sẽ có nhiều đối tượng được lấy nét hơn. Khi được gắn vào một :ref:`Camera3D<class_Camera3D>` dưới dạng :ref:`Camera3D.attributes<class_Camera3D_property_attributes>` của nó, thuộc tính này sẽ ghi đè thuộc tính :ref:`Camera3D.fov<class_Camera3D_property_fov>` và thuộc tính :ref:`Camera3D.keep_aspect<class_Camera3D_property_keep_aspect>`.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_frustum_focus_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **frustum_focus_distance** = ``10.0`` :ref:`🔗<class_CameraAttributesPhysical_property_frustum_focus_distance>`

.. rst-class:: classref-property-setget

- |void| **set_focus_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_focus_distance**\ (\ )

Khoảng cách từ camera đến đối tượng sẽ được lấy nét, được đo bằng mét. Về mặt nội bộ, giá trị này sẽ được giới hạn để lớn hơn :ref:`frustum_focal_length<class_CameraAttributesPhysical_property_frustum_focal_length>` ít nhất 1 milimét.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPhysical_property_frustum_near:

.. rst-class:: classref-property

:ref:`float<class_float>` **frustum_near** = ``0.05`` :ref:`🔗<class_CameraAttributesPhysical_property_frustum_near>`

.. rst-class:: classref-property-setget

- |void| **set_near**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_near**\ (\ )

Giá trị ghi đè cho :ref:`Camera3D.near<class_Camera3D_property_near>`. Được sử dụng nội bộ khi tính toán depth of field. Khi được gắn vào một :ref:`Camera3D<class_Camera3D>` dưới dạng :ref:`Camera3D.attributes<class_Camera3D_property_attributes>` của nó, thuộc tính này sẽ ghi đè thuộc tính :ref:`Camera3D.near<class_Camera3D_property_near>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CameraAttributesPhysical_method_get_fov:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_fov**\ (\ ) |const| :ref:`🔗<class_CameraAttributesPhysical_method_get_fov>`

Trả về field of view theo chiều dọc tương ứng với :ref:`frustum_focal_length<class_CameraAttributesPhysical_property_frustum_focal_length>`. Giá trị này được tính toán nội bộ mỗi khi :ref:`frustum_focal_length<class_CameraAttributesPhysical_property_frustum_focal_length>` được thay đổi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
