:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/mobile_vr/doc_classes/MobileVRInterface.xml.

.. _class_MobileVRInterface:

MobileVRInterface
=================

**Kế thừa:** :ref:`XRInterface<class_XRInterface>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Triển khai VR di động tổng quát.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một triển khai VR di động tổng quát, trong đó bạn cần cung cấp thông tin chi tiết về điện thoại và HMD được sử dụng. Triển khai này không phụ thuộc vào bất kỳ framework hiện có nào. Đây là interface cơ bản nhất mà chúng tôi có. Để đạt hiệu quả tốt nhất, bạn cần một điện thoại di động có con quay hồi chuyển và gia tốc kế.

Lưu ý rằng mặc dù không có tracking vị trí, camera sẽ giả định headset ở độ cao 1,85 mét. Bạn có thể thay đổi giá trị này bằng cách thiết lập :ref:`eye_height<class_MobileVRInterface_property_eye_height>`.

Bạn có thể khởi tạo interface này như sau:

::

    var interface = XRServer.find_interface("Native mobile")
    if interface and interface.initialize():
        get_viewport().use_xr = true

\ **Lưu ý:** Đối với Android, :ref:`ProjectSettings.input_devices/sensors/enable_accelerometer<class_ProjectSettings_property_input_devices/sensors/enable_accelerometer>`, :ref:`ProjectSettings.input_devices/sensors/enable_gravity<class_ProjectSettings_property_input_devices/sensors/enable_gravity>`, :ref:`ProjectSettings.input_devices/sensors/enable_gyroscope<class_ProjectSettings_property_input_devices/sensors/enable_gyroscope>` và :ref:`ProjectSettings.input_devices/sensors/enable_magnetometer<class_ProjectSettings_property_input_devices/sensors/enable_magnetometer>` phải được bật.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`display_to_lens<class_MobileVRInterface_property_display_to_lens>` | ``4.0``                                                                            |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`display_width<class_MobileVRInterface_property_display_width>`     | ``14.5``                                                                           |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`eye_height<class_MobileVRInterface_property_eye_height>`           | ``1.85``                                                                           |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`iod<class_MobileVRInterface_property_iod>`                         | ``6.0``                                                                            |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`k1<class_MobileVRInterface_property_k1>`                           | ``0.215``                                                                          |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`k2<class_MobileVRInterface_property_k2>`                           | ``0.215``                                                                          |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                          | :ref:`offset_rect<class_MobileVRInterface_property_offset_rect>`         | ``Rect2(0, 0, 1, 1)``                                                              |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`oversample<class_MobileVRInterface_property_oversample>`           | ``1.5``                                                                            |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`vrs_min_radius<class_MobileVRInterface_property_vrs_min_radius>`   | ``20.0``                                                                           |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`vrs_strength<class_MobileVRInterface_property_vrs_strength>`       | ``1.0``                                                                            |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`PlayAreaMode<enum_XRInterface_PlayAreaMode>` | xr_play_area_mode                                                        | ``1`` (overrides :ref:`XRInterface<class_XRInterface_property_xr_play_area_mode>`) |
   +----------------------------------------------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MobileVRInterface_property_display_to_lens:

.. rst-class:: classref-property

:ref:`float<class_float>` **display_to_lens** = ``4.0`` :ref:`🔗<class_MobileVRInterface_property_display_to_lens>`

.. rst-class:: classref-property-setget

- |void| **set_display_to_lens**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_display_to_lens**\ (\ )

Khoảng cách giữa màn hình và các thấu kính bên trong thiết bị, tính bằng centimet.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_display_width:

.. rst-class:: classref-property

:ref:`float<class_float>` **display_width** = ``14.5`` :ref:`🔗<class_MobileVRInterface_property_display_width>`

.. rst-class:: classref-property-setget

- |void| **set_display_width**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_display_width**\ (\ )

Chiều rộng của màn hình, tính bằng centimet.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_eye_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **eye_height** = ``1.85`` :ref:`🔗<class_MobileVRInterface_property_eye_height>`

.. rst-class:: classref-property-setget

- |void| **set_eye_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_eye_height**\ (\ )

Độ cao đặt camera so với mặt đất (tức là node :ref:`XROrigin3D<class_XROrigin3D>`).

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_iod:

.. rst-class:: classref-property

:ref:`float<class_float>` **iod** = ``6.0`` :ref:`🔗<class_MobileVRInterface_property_iod>`

.. rst-class:: classref-property-setget

- |void| **set_iod**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_iod**\ (\ )

Khoảng cách giữa hai mắt, còn được gọi là khoảng cách giữa hai đồng tử. Khoảng cách giữa đồng tử của mắt trái và mắt phải.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_k1:

.. rst-class:: classref-property

:ref:`float<class_float>` **k1** = ``0.215`` :ref:`🔗<class_MobileVRInterface_property_k1>`

.. rst-class:: classref-property-setget

- |void| **set_k1**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_k1**\ (\ )

Hệ số thấu kính k1 là một trong hai hằng số xác định độ mạnh của thấu kính được sử dụng và ảnh hưởng trực tiếp đến hiệu ứng biến dạng thấu kính.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_k2:

.. rst-class:: classref-property

:ref:`float<class_float>` **k2** = ``0.215`` :ref:`🔗<class_MobileVRInterface_property_k2>`

.. rst-class:: classref-property-setget

- |void| **set_k2**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_k2**\ (\ )

Hệ số thấu kính k2, xem k1.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_offset_rect:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **offset_rect** = ``Rect2(0, 0, 1, 1)`` :ref:`🔗<class_MobileVRInterface_property_offset_rect>`

.. rst-class:: classref-property-setget

- |void| **set_offset_rect**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_offset_rect**\ (\ )

Thiết lập hình chữ nhật offset tương đối so với vùng đang được render. Độ dài bằng 1 biểu thị toàn bộ vùng render trên trục đó.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_oversample:

.. rst-class:: classref-property

:ref:`float<class_float>` **oversample** = ``1.5`` :ref:`🔗<class_MobileVRInterface_property_oversample>`

.. rst-class:: classref-property-setget

- |void| **set_oversample**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_oversample**\ (\ )

Thiết lập oversample. Do biến dạng thấu kính, chúng ta phải render các buffer ở độ phân giải cao hơn mức màn hình có thể xử lý tự nhiên. Giá trị từ 1.5 đến 2.0 thường cho kết quả tốt, nhưng phải đánh đổi bằng hiệu năng.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_vrs_min_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **vrs_min_radius** = ``20.0`` :ref:`🔗<class_MobileVRInterface_property_vrs_min_radius>`

.. rst-class:: classref-property-setget

- |void| **set_vrs_min_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_vrs_min_radius**\ (\ )

Bán kính tối thiểu quanh tiêu điểm, tại đó chất lượng đầy đủ được đảm bảo khi sử dụng VRS, tính theo phần trăm kích thước màn hình.

\ **Lưu ý:** Chỉ dành cho các renderer Mobile và Forward+. Yêu cầu :ref:`Viewport.vrs_mode<class_Viewport_property_vrs_mode>` được đặt thành :ref:`Viewport.VRS_XR<class_Viewport_constant_VRS_XR>`.

.. rst-class:: classref-item-separator

----

.. _class_MobileVRInterface_property_vrs_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **vrs_strength** = ``1.0`` :ref:`🔗<class_MobileVRInterface_property_vrs_strength>`

.. rst-class:: classref-property-setget

- |void| **set_vrs_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_vrs_strength**\ (\ )

Mức strength được sử dụng để tính toán density map của VRS. Giá trị này càng lớn thì VRS càng dễ nhận thấy. Thiết lập này cải thiện hiệu năng nhưng làm giảm chất lượng.

\ **Lưu ý:** Chỉ dành cho các renderer Mobile và Forward+. Yêu cầu :ref:`Viewport.vrs_mode<class_Viewport_property_vrs_mode>` được đặt thành :ref:`Viewport.VRS_XR<class_Viewport_constant_VRS_XR>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
