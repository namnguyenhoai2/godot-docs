:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CameraAttributesPractical.xml.

.. _class_CameraAttributesPractical:

CameraAttributesPractical
=========================

**Kế thừa:** :ref:`CameraAttributes<class_CameraAttributes>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Các thiết lập camera ở định dạng dễ sử dụng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Điều khiển các thuộc tính dành riêng cho camera như auto-exposure, depth of field và exposure override.

Khi được sử dụng trong một :ref:`WorldEnvironment<class_WorldEnvironment>`, nó cung cấp các thiết lập mặc định cho exposure, auto-exposure và depth of field, được tất cả camera không có :ref:`CameraAttributes<class_CameraAttributes>` riêng sử dụng, bao gồm cả camera của editor. Khi được sử dụng trong một :ref:`Camera3D<class_Camera3D>`, nó sẽ ghi đè mọi :ref:`CameraAttributes<class_CameraAttributes>` được thiết lập trong :ref:`WorldEnvironment<class_WorldEnvironment>`. Khi được sử dụng trong :ref:`VoxelGI<class_VoxelGI>` hoặc :ref:`LightmapGI<class_LightmapGI>`, chỉ các thiết lập exposure được sử dụng.

\ **Lưu ý:** Làm mờ depth of field chỉ được hỗ trợ trong các phương thức rendering Forward+ và Mobile, không được hỗ trợ trong Compatibility.

\ **Lưu ý:** Auto-exposure chỉ được hỗ trợ trong phương thức rendering Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_max_sensitivity<class_CameraAttributesPractical_property_auto_exposure_max_sensitivity>` | ``800.0`` |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`auto_exposure_min_sensitivity<class_CameraAttributesPractical_property_auto_exposure_min_sensitivity>` | ``0.0``   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dof_blur_amount<class_CameraAttributesPractical_property_dof_blur_amount>`                             | ``0.1``   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dof_blur_far_distance<class_CameraAttributesPractical_property_dof_blur_far_distance>`                 | ``10.0``  |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`dof_blur_far_enabled<class_CameraAttributesPractical_property_dof_blur_far_enabled>`                   | ``false`` |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dof_blur_far_transition<class_CameraAttributesPractical_property_dof_blur_far_transition>`             | ``5.0``   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dof_blur_near_distance<class_CameraAttributesPractical_property_dof_blur_near_distance>`               | ``2.0``   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`dof_blur_near_enabled<class_CameraAttributesPractical_property_dof_blur_near_enabled>`                 | ``false`` |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`dof_blur_near_transition<class_CameraAttributesPractical_property_dof_blur_near_transition>`           | ``1.0``   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraAttributesPractical_property_auto_exposure_max_sensitivity:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_max_sensitivity** = ``800.0`` :ref:`🔗<class_CameraAttributesPractical_property_auto_exposure_max_sensitivity>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_max_sensitivity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_max_sensitivity**\ (\ )

Độ nhạy tối đa (tính theo ISO) được sử dụng khi tính toán auto exposure. Khi tính độ sáng trung bình của cảnh, các giá trị màu sẽ được giới hạn không thấp hơn giá trị này. Điều này giới hạn auto-exposure, ngăn không cho phơi sáng thấp hơn một mức sáng nhất định, tạo ra một ngưỡng mà tại đó cảnh sẽ vẫn sáng.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_auto_exposure_min_sensitivity:

.. rst-class:: classref-property

:ref:`float<class_float>` **auto_exposure_min_sensitivity** = ``0.0`` :ref:`🔗<class_CameraAttributesPractical_property_auto_exposure_min_sensitivity>`

.. rst-class:: classref-property-setget

- |void| **set_auto_exposure_min_sensitivity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_auto_exposure_min_sensitivity**\ (\ )

Độ nhạy tối thiểu (tính theo ISO) được sử dụng khi tính toán auto exposure. Khi tính độ sáng trung bình của cảnh, các giá trị màu sẽ được giới hạn không thấp hơn giá trị này. Điều này giới hạn auto-exposure, ngăn không cho phơi sáng cao hơn một mức sáng nhất định, tạo ra một ngưỡng mà tại đó cảnh sẽ vẫn tối.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_amount:

.. rst-class:: classref-property

:ref:`float<class_float>` **dof_blur_amount** = ``0.1`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_amount>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_amount**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dof_blur_amount**\ (\ )

Thiết lập mức độ làm mờ tối đa. Khi sử dụng mức độ làm mờ dựa trên vật lý, giá trị này sẽ thay vào đó hoạt động như một hệ số nhân. Giá trị cao làm tăng mức độ mờ, nhưng có thể tốn nhiều chi phí tính toán hơn đáng kể. Tốt nhất nên giữ giá trị này ở mức thấp nhất có thể đối với một phong cách đồ họa nhất định.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_far_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **dof_blur_far_distance** = ``10.0`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_far_distance>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_far_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dof_blur_far_distance**\ (\ )

Các đối tượng cách :ref:`Camera3D<class_Camera3D>` xa hơn khoảng cách này sẽ bị làm mờ bởi hiệu ứng depth of field. Đơn vị đo là mét.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_far_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **dof_blur_far_enabled** = ``false`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_far_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_far_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_dof_blur_far_enabled**\ (\ )

Bật làm mờ depth of field cho các đối tượng cách :ref:`dof_blur_far_distance<class_CameraAttributesPractical_property_dof_blur_far_distance>` xa hơn. Cường độ làm mờ được điều khiển bởi :ref:`dof_blur_amount<class_CameraAttributesPractical_property_dof_blur_amount>` và được điều chỉnh bởi :ref:`dof_blur_far_transition<class_CameraAttributesPractical_property_dof_blur_far_transition>`.

\ **Lưu ý:** Làm mờ depth of field chỉ được hỗ trợ trong các phương thức rendering Forward+ và Mobile, không được hỗ trợ trong Compatibility.

\ **Lưu ý:** Làm mờ depth of field không được hỗ trợ trên các viewport có nền trong suốt (khi :ref:`Viewport.transparent_bg<class_Viewport_property_transparent_bg>` là ``true``).

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_far_transition:

.. rst-class:: classref-property

:ref:`float<class_float>` **dof_blur_far_transition** = ``5.0`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_far_transition>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_far_transition**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dof_blur_far_transition**\ (\ )

Khi là số dương, đây là khoảng cách mà trong đó (bắt đầu từ :ref:`dof_blur_far_distance<class_CameraAttributesPractical_property_dof_blur_far_distance>`) hiệu ứng làm mờ sẽ tăng dần từ 0 đến :ref:`dof_blur_amount<class_CameraAttributesPractical_property_dof_blur_amount>`. Khi là số âm, sử dụng tỷ lệ theo vật lý, trong đó hiệu ứng depth of field sẽ tăng dần từ 0 tại :ref:`dof_blur_far_distance<class_CameraAttributesPractical_property_dof_blur_far_distance>` và tăng theo cách chính xác về mặt vật lý khi các đối tượng ở xa :ref:`Camera3D<class_Camera3D>` hơn.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_near_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **dof_blur_near_distance** = ``2.0`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_near_distance>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_near_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dof_blur_near_distance**\ (\ )

Các đối tượng cách :ref:`Camera3D<class_Camera3D>` gần hơn khoảng cách này sẽ bị làm mờ bởi hiệu ứng depth of field. Đơn vị đo là mét.

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_near_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **dof_blur_near_enabled** = ``false`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_near_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_near_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_dof_blur_near_enabled**\ (\ )

Bật làm mờ depth of field cho các đối tượng cách :ref:`dof_blur_near_distance<class_CameraAttributesPractical_property_dof_blur_near_distance>` gần hơn. Cường độ làm mờ được điều khiển bởi :ref:`dof_blur_amount<class_CameraAttributesPractical_property_dof_blur_amount>` và được điều chỉnh bởi :ref:`dof_blur_near_transition<class_CameraAttributesPractical_property_dof_blur_near_transition>`.

\ **Lưu ý:** Làm mờ depth of field chỉ được hỗ trợ trong các phương thức rendering Forward+ và Mobile, không được hỗ trợ trong Compatibility.

\ **Lưu ý:** Làm mờ depth of field không được hỗ trợ trên các viewport có nền trong suốt (khi :ref:`Viewport.transparent_bg<class_Viewport_property_transparent_bg>` là ``true``).

.. rst-class:: classref-item-separator

----

.. _class_CameraAttributesPractical_property_dof_blur_near_transition:

.. rst-class:: classref-property

:ref:`float<class_float>` **dof_blur_near_transition** = ``1.0`` :ref:`🔗<class_CameraAttributesPractical_property_dof_blur_near_transition>`

.. rst-class:: classref-property-setget

- |void| **set_dof_blur_near_transition**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dof_blur_near_transition**\ (\ )

Khi là số dương, đây là khoảng cách mà trong đó hiệu ứng làm mờ sẽ tăng dần từ 0 đến :ref:`dof_blur_amount<class_CameraAttributesPractical_property_dof_blur_amount>`, kết thúc tại :ref:`dof_blur_near_distance<class_CameraAttributesPractical_property_dof_blur_near_distance>`. Khi là số âm, sử dụng tỷ lệ theo vật lý, trong đó hiệu ứng depth of field sẽ tăng dần từ 0 tại :ref:`dof_blur_near_distance<class_CameraAttributesPractical_property_dof_blur_near_distance>` và tăng theo cách chính xác về mặt vật lý khi các đối tượng tiến gần :ref:`Camera3D<class_Camera3D>` hơn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
