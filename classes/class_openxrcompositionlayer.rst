:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRCompositionLayer.xml.

.. _class_OpenXRCompositionLayer:

OpenXRCompositionLayer
======================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`OpenXRCompositionLayerCylinder<class_OpenXRCompositionLayerCylinder>`, :ref:`OpenXRCompositionLayerEquirect<class_OpenXRCompositionLayerEquirect>`, :ref:`OpenXRCompositionLayerQuad<class_OpenXRCompositionLayerQuad>`

Lớp cha của tất cả các node lớp composition OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các lớp composition cho phép hiển thị viewport 2D bên trong headset bởi XR compositor thông qua các phép chiếu đặc biệt giúp giữ nguyên chất lượng. Điều này cho phép kết xuất văn bản rõ nét trong khi vẫn giữ lớp ở độ phân giải gốc.

\ **Lưu ý:** Nếu OpenXR runtime không hỗ trợ loại lớp composition đã cho, một mesh dự phòng có thể được tạo bằng :ref:`ViewportTexture<class_ViewportTexture>` để mô phỏng lớp composition.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                                         | :ref:`alpha_blend<class_OpenXRCompositionLayer_property_alpha_blend>`                                         | ``false``                |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2i<class_Vector2i>`                                 | :ref:`android_surface_size<class_OpenXRCompositionLayer_property_android_surface_size>`                       | ``Vector2i(1024, 1024)`` |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                                         | :ref:`enable_hole_punch<class_OpenXRCompositionLayer_property_enable_hole_punch>`                             | ``false``                |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` | :ref:`eye_visibility<class_OpenXRCompositionLayer_property_eye_visibility>`                                   | ``0``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`SubViewport<class_SubViewport>`                           | :ref:`layer_viewport<class_OpenXRCompositionLayer_property_layer_viewport>`                                   |                          |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                                         | :ref:`protected_content<class_OpenXRCompositionLayer_property_protected_content>`                             | ``false``                |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                           | :ref:`sort_order<class_OpenXRCompositionLayer_property_sort_order>`                                           | ``1``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`             | :ref:`swapchain_state_alpha_swizzle<class_OpenXRCompositionLayer_property_swapchain_state_alpha_swizzle>`     | ``3``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`             | :ref:`swapchain_state_blue_swizzle<class_OpenXRCompositionLayer_property_swapchain_state_blue_swizzle>`       | ``2``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`                                       | :ref:`swapchain_state_border_color<class_OpenXRCompositionLayer_property_swapchain_state_border_color>`       | ``Color(0, 0, 0, 0)``    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`             | :ref:`swapchain_state_green_swizzle<class_OpenXRCompositionLayer_property_swapchain_state_green_swizzle>`     | ``1``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>`                   | :ref:`swapchain_state_horizontal_wrap<class_OpenXRCompositionLayer_property_swapchain_state_horizontal_wrap>` | ``0``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Filter<enum_OpenXRCompositionLayer_Filter>`               | :ref:`swapchain_state_mag_filter<class_OpenXRCompositionLayer_property_swapchain_state_mag_filter>`           | ``1``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                                       | :ref:`swapchain_state_max_anisotropy<class_OpenXRCompositionLayer_property_swapchain_state_max_anisotropy>`   | ``1.0``                  |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Filter<enum_OpenXRCompositionLayer_Filter>`               | :ref:`swapchain_state_min_filter<class_OpenXRCompositionLayer_property_swapchain_state_min_filter>`           | ``1``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>`       | :ref:`swapchain_state_mipmap_mode<class_OpenXRCompositionLayer_property_swapchain_state_mipmap_mode>`         | ``2``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`             | :ref:`swapchain_state_red_swizzle<class_OpenXRCompositionLayer_property_swapchain_state_red_swizzle>`         | ``0``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>`                   | :ref:`swapchain_state_vertical_wrap<class_OpenXRCompositionLayer_property_swapchain_state_vertical_wrap>`     | ``0``                    |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                                         | :ref:`use_android_surface<class_OpenXRCompositionLayer_property_use_android_surface>`                         | ``false``                |
   +-----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaObject<class_JavaObject>` | :ref:`get_android_surface<class_OpenXRCompositionLayer_method_get_android_surface>`\ (\ )                                                                                  |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`       | :ref:`intersects_ray<class_OpenXRCompositionLayer_method_intersects_ray>`\ (\ origin\: :ref:`Vector3<class_Vector3>`, direction\: :ref:`Vector3<class_Vector3>`\ ) |const| |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_natively_supported<class_OpenXRCompositionLayer_method_is_natively_supported>`\ (\ ) |const|                                                                      |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRCompositionLayer_Filter:

.. rst-class:: classref-enumeration

enum **Filter**: :ref:`🔗<enum_OpenXRCompositionLayer_Filter>`

.. _class_OpenXRCompositionLayer_constant_FILTER_NEAREST:

.. rst-class:: classref-enumeration-constant

:ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **FILTER_NEAREST** = ``0``

Thực hiện lọc láng giềng gần nhất khi lấy mẫu texture.

.. _class_OpenXRCompositionLayer_constant_FILTER_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **FILTER_LINEAR** = ``1``

Thực hiện lọc tuyến tính khi lấy mẫu texture.

.. _class_OpenXRCompositionLayer_constant_FILTER_CUBIC:

.. rst-class:: classref-enumeration-constant

:ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **FILTER_CUBIC** = ``2``

Thực hiện lọc cubic khi lấy mẫu texture.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRCompositionLayer_MipmapMode:

.. rst-class:: classref-enumeration

enum **MipmapMode**: :ref:`🔗<enum_OpenXRCompositionLayer_MipmapMode>`

.. _class_OpenXRCompositionLayer_constant_MIPMAP_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>` **MIPMAP_MODE_DISABLED** = ``0``

Tắt mipmapping.

\ **Lưu ý:** Chỉ có thể tắt mipmapping trong Compatibility renderer.

.. _class_OpenXRCompositionLayer_constant_MIPMAP_MODE_NEAREST:

.. rst-class:: classref-enumeration-constant

:ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>` **MIPMAP_MODE_NEAREST** = ``1``

Sử dụng mipmap có độ phân giải gần nhất.

.. _class_OpenXRCompositionLayer_constant_MIPMAP_MODE_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>` **MIPMAP_MODE_LINEAR** = ``2``

Sử dụng nội suy tuyến tính của hai mipmap có độ phân giải gần nhất.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRCompositionLayer_Wrap:

.. rst-class:: classref-enumeration

enum **Wrap**: :ref:`🔗<enum_OpenXRCompositionLayer_Wrap>`

.. _class_OpenXRCompositionLayer_constant_WRAP_CLAMP_TO_BORDER:

.. rst-class:: classref-enumeration-constant

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **WRAP_CLAMP_TO_BORDER** = ``0``

Giới hạn texture theo màu viền được chỉ định.

.. _class_OpenXRCompositionLayer_constant_WRAP_CLAMP_TO_EDGE:

.. rst-class:: classref-enumeration-constant

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **WRAP_CLAMP_TO_EDGE** = ``1``

Giới hạn texture theo màu ở cạnh của nó.

.. _class_OpenXRCompositionLayer_constant_WRAP_REPEAT:

.. rst-class:: classref-enumeration-constant

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **WRAP_REPEAT** = ``2``

Lặp texture vô hạn.

.. _class_OpenXRCompositionLayer_constant_WRAP_MIRRORED_REPEAT:

.. rst-class:: classref-enumeration-constant

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **WRAP_MIRRORED_REPEAT** = ``3``

Lặp texture vô hạn, phản chiếu texture ở mỗi lần lặp.

.. _class_OpenXRCompositionLayer_constant_WRAP_MIRROR_CLAMP_TO_EDGE:

.. rst-class:: classref-enumeration-constant

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **WRAP_MIRROR_CLAMP_TO_EDGE** = ``4``

Phản chiếu texture một lần rồi giới hạn texture theo màu ở cạnh của nó.

\ **Lưu ý:** Chế độ wrap này không khả dụng trong Compatibility renderer.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRCompositionLayer_Swizzle:

.. rst-class:: classref-enumeration

enum **Swizzle**: :ref:`🔗<enum_OpenXRCompositionLayer_Swizzle>`

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_RED:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_RED** = ``0``

Ánh xạ một kênh màu sang giá trị của kênh đỏ.

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_GREEN:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_GREEN** = ``1``

Ánh xạ một kênh màu sang giá trị của kênh xanh lá.

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_BLUE:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_BLUE** = ``2``

Ánh xạ một kênh màu sang giá trị của kênh xanh dương.

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_ALPHA:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_ALPHA** = ``3``

Ánh xạ một kênh màu sang giá trị của kênh alpha.

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_ZERO:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_ZERO** = ``4``

Ánh xạ một kênh màu sang giá trị không.

.. _class_OpenXRCompositionLayer_constant_SWIZZLE_ONE:

.. rst-class:: classref-enumeration-constant

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **SWIZZLE_ONE** = ``5``

Ánh xạ một kênh màu sang giá trị một.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRCompositionLayer_EyeVisibility:

.. rst-class:: classref-enumeration

enum **EyeVisibility**: :ref:`🔗<enum_OpenXRCompositionLayer_EyeVisibility>`

.. _class_OpenXRCompositionLayer_constant_EYE_VISIBILITY_BOTH:

.. rst-class:: classref-enumeration-constant

:ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` **EYE_VISIBILITY_BOTH** = ``0``

Lớp hiển thị với cả mắt trái và mắt phải.

.. _class_OpenXRCompositionLayer_constant_EYE_VISIBILITY_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` **EYE_VISIBILITY_LEFT** = ``1``

Lớp chỉ hiển thị với mắt trái.

.. _class_OpenXRCompositionLayer_constant_EYE_VISIBILITY_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` **EYE_VISIBILITY_RIGHT** = ``2``

Lớp chỉ hiển thị với mắt phải.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRCompositionLayer_property_alpha_blend:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **alpha_blend** = ``false`` :ref:`🔗<class_OpenXRCompositionLayer_property_alpha_blend>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_blend**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_alpha_blend**\ (\ )

Bật blending cho lớp bằng kênh alpha của nó.

Có thể kết hợp với :ref:`Viewport.transparent_bg<class_Viewport_property_transparent_bg>` để tạo nền trong suốt cho lớp.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_android_surface_size:

.. rst-class:: classref-property

:ref:`Vector2i<class_Vector2i>` **android_surface_size** = ``Vector2i(1024, 1024)`` :ref:`🔗<class_OpenXRCompositionLayer_property_android_surface_size>`

.. rst-class:: classref-property-setget

- |void| **set_android_surface_size**\ (\ value\: :ref:`Vector2i<class_Vector2i>`\ ) - :ref:`Vector2i<class_Vector2i>` **get_android_surface_size**\ (\ )

Kích thước Android surface cần tạo nếu :ref:`use_android_surface<class_OpenXRCompositionLayer_property_use_android_surface>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_enable_hole_punch:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enable_hole_punch** = ``false`` :ref:`🔗<class_OpenXRCompositionLayer_property_enable_hole_punch>`

.. rst-class:: classref-property-setget

- |void| **set_enable_hole_punch**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_enable_hole_punch**\ (\ )

Bật một kỹ thuật gọi là "hole punching", cho phép đặt lớp composition phía sau lớp projection chính (tức là đặt :ref:`sort_order<class_OpenXRCompositionLayer_property_sort_order>` thành giá trị âm) đồng thời "đục một lỗ" xuyên qua mọi thứ được Godot kết xuất để lớp này vẫn hiển thị.

Có thể dùng kỹ thuật này để tạo ảo giác rằng lớp composition tồn tại trong cùng không gian 3D với mọi thứ được Godot kết xuất, cho phép các đối tượng xuất hiện như đi ra phía sau hoặc phía trước lớp composition.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_eye_visibility:

.. rst-class:: classref-property

:ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` **eye_visibility** = ``0`` :ref:`🔗<class_OpenXRCompositionLayer_property_eye_visibility>`

.. rst-class:: classref-property-setget

- |void| **set_eye_visibility**\ (\ value\: :ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>`\ ) - :ref:`EyeVisibility<enum_OpenXRCompositionLayer_EyeVisibility>` **get_eye_visibility**\ (\ )

(Các) mắt mà lớp composition hiển thị với.

\ **Lưu ý:** Không phải tất cả các loại lớp composition hoặc runtime đều hỗ trợ giới hạn khả năng hiển thị cho một mắt duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_layer_viewport:

.. rst-class:: classref-property

:ref:`SubViewport<class_SubViewport>` **layer_viewport** :ref:`🔗<class_OpenXRCompositionLayer_property_layer_viewport>`

.. rst-class:: classref-property-setget

- |void| **set_layer_viewport**\ (\ value\: :ref:`SubViewport<class_SubViewport>`\ ) - :ref:`SubViewport<class_SubViewport>` **get_layer_viewport**\ (\ )

:ref:`SubViewport<class_SubViewport>` cần kết xuất trên lớp composition.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_protected_content:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **protected_content** = ``false`` :ref:`🔗<class_OpenXRCompositionLayer_property_protected_content>`

.. rst-class:: classref-property-setget

- |void| **set_protected_content**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_protected_content**\ (\ )

Nếu được bật, OpenXR swapchain sẽ được tạo với cờ ``XR_SWAPCHAIN_CREATE_PROTECTED_CONTENT_BIT``, bảo vệ nội dung khỏi việc truy cập bằng CPU.

Khi được sử dụng với Android Surface, tùy chọn này có thể cho phép trình bày nội dung DRM và chỉ có hiệu lực khi Surface được tạo lần đầu; các thay đổi sau đó đối với thuộc tính này sẽ không có hiệu lực.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_sort_order:

.. rst-class:: classref-property

:ref:`int<class_int>` **sort_order** = ``1`` :ref:`🔗<class_OpenXRCompositionLayer_property_sort_order>`

.. rst-class:: classref-property-setget

- |void| **set_sort_order**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sort_order**\ (\ )

Thứ tự sắp xếp của lớp composition này. Các số lớn hơn sẽ được hiển thị phía trước các số nhỏ hơn.

\ **Lưu ý:** Thuộc tính này không có hiệu lực nếu đang sử dụng mesh dự phòng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_alpha_swizzle:

.. rst-class:: classref-property

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **swapchain_state_alpha_swizzle** = ``3`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_alpha_swizzle>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_swizzle**\ (\ value\: :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`\ ) - :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **get_alpha_swizzle**\ (\ )

Giá trị swizzle cho kênh alpha của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_blue_swizzle:

.. rst-class:: classref-property

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **swapchain_state_blue_swizzle** = ``2`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_blue_swizzle>`

.. rst-class:: classref-property-setget

- |void| **set_blue_swizzle**\ (\ value\: :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`\ ) - :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **get_blue_swizzle**\ (\ )

Giá trị swizzle cho kênh xanh dương của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_border_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **swapchain_state_border_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_border_color>`

.. rst-class:: classref-property-setget

- |void| **set_border_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_border_color**\ (\ )

Màu viền của trạng thái swapchain được sử dụng khi chế độ wrap giới hạn theo viền.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_green_swizzle:

.. rst-class:: classref-property

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **swapchain_state_green_swizzle** = ``1`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_green_swizzle>`

.. rst-class:: classref-property-setget

- |void| **set_green_swizzle**\ (\ value\: :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`\ ) - :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **get_green_swizzle**\ (\ )

Giá trị swizzle cho kênh xanh lá của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_horizontal_wrap:

.. rst-class:: classref-property

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **swapchain_state_horizontal_wrap** = ``0`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_horizontal_wrap>`

.. rst-class:: classref-property-setget

- |void| **set_horizontal_wrap**\ (\ value\: :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>`\ ) - :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **get_horizontal_wrap**\ (\ )

Chế độ wrap theo chiều ngang của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_mag_filter:

.. rst-class:: classref-property

:ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **swapchain_state_mag_filter** = ``1`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_mag_filter>`

.. rst-class:: classref-property-setget

- |void| **set_mag_filter**\ (\ value\: :ref:`Filter<enum_OpenXRCompositionLayer_Filter>`\ ) - :ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **get_mag_filter**\ (\ )

Bộ lọc phóng đại của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_max_anisotropy:

.. rst-class:: classref-property

:ref:`float<class_float>` **swapchain_state_max_anisotropy** = ``1.0`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_max_anisotropy>`

.. rst-class:: classref-property-setget

- |void| **set_max_anisotropy**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_anisotropy**\ (\ )

Độ bất đẳng hướng tối đa của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_min_filter:

.. rst-class:: classref-property

:ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **swapchain_state_min_filter** = ``1`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_min_filter>`

.. rst-class:: classref-property-setget

- |void| **set_min_filter**\ (\ value\: :ref:`Filter<enum_OpenXRCompositionLayer_Filter>`\ ) - :ref:`Filter<enum_OpenXRCompositionLayer_Filter>` **get_min_filter**\ (\ )

Bộ lọc thu nhỏ của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_mipmap_mode:

.. rst-class:: classref-property

:ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>` **swapchain_state_mipmap_mode** = ``2`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_mipmap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mipmap_mode**\ (\ value\: :ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>`\ ) - :ref:`MipmapMode<enum_OpenXRCompositionLayer_MipmapMode>` **get_mipmap_mode**\ (\ )

Chế độ mipmap của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_red_swizzle:

.. rst-class:: classref-property

:ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **swapchain_state_red_swizzle** = ``0`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_red_swizzle>`

.. rst-class:: classref-property-setget

- |void| **set_red_swizzle**\ (\ value\: :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>`\ ) - :ref:`Swizzle<enum_OpenXRCompositionLayer_Swizzle>` **get_red_swizzle**\ (\ )

Giá trị swizzle cho kênh đỏ của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_swapchain_state_vertical_wrap:

.. rst-class:: classref-property

:ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **swapchain_state_vertical_wrap** = ``0`` :ref:`🔗<class_OpenXRCompositionLayer_property_swapchain_state_vertical_wrap>`

.. rst-class:: classref-property-setget

- |void| **set_vertical_wrap**\ (\ value\: :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>`\ ) - :ref:`Wrap<enum_OpenXRCompositionLayer_Wrap>` **get_vertical_wrap**\ (\ )

Chế độ wrap theo chiều dọc của trạng thái swapchain.

\ **Lưu ý:** Thuộc tính này chỉ có hiệu lực trên các thiết bị hỗ trợ các extension OpenGLES/Vulkan OpenXR XR_FB_swapchain_update_state.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_property_use_android_surface:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_android_surface** = ``false`` :ref:`🔗<class_OpenXRCompositionLayer_property_use_android_surface>`

.. rst-class:: classref-property-setget

- |void| **set_use_android_surface**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_android_surface**\ (\ )

Nếu được bật, một Android surface sẽ được tạo (với các kích thước từ :ref:`android_surface_size<class_OpenXRCompositionLayer_property_android_surface_size>`) để cung cấp nội dung 2D cho composition layer, thay vì sử dụng :ref:`layer_viewport<class_OpenXRCompositionLayer_property_layer_viewport>`.

Xem :ref:`get_android_surface()<class_OpenXRCompositionLayer_method_get_android_surface>` để biết thông tin về cách lấy surface để ứng dụng của bạn có thể vẽ lên đó.

\ **Lưu ý:** Tính năng này chỉ hoạt động trong các bản build Android.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRCompositionLayer_method_get_android_surface:

.. rst-class:: classref-method

:ref:`JavaObject<class_JavaObject>` **get_android_surface**\ (\ ) :ref:`🔗<class_OpenXRCompositionLayer_method_get_android_surface>`

Trả về một :ref:`JavaObject<class_JavaObject>` đại diện cho một ``android.view.Surface`` nếu :ref:`use_android_surface<class_OpenXRCompositionLayer_property_use_android_surface>` được bật và OpenXR đã tạo surface. Nếu không, phương thức này sẽ trả về ``null``.

\ **Lưu ý:** Surface chỉ có thể được tạo trong một OpenXR session đang hoạt động. Vì vậy, nếu :ref:`use_android_surface<class_OpenXRCompositionLayer_property_use_android_surface>` được bật bên ngoài một OpenXR session, surface sẽ chưa được tạo cho đến khi một session mới khởi động hoàn toàn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_method_intersects_ray:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **intersects_ray**\ (\ origin\: :ref:`Vector3<class_Vector3>`, direction\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_OpenXRCompositionLayer_method_intersects_ray>`

Trả về các tọa độ UV tại vị trí ray đã cho giao với composition layer. ``origin`` và ``direction`` phải ở global space.

Trả về ``Vector2(-1.0, -1.0)`` nếu ray không giao.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRCompositionLayer_method_is_natively_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_natively_supported**\ (\ ) |const| :ref:`🔗<class_OpenXRCompositionLayer_method_is_natively_supported>`

Trả về ``true`` nếu OpenXR runtime hỗ trợ composition layer type này một cách native.

\ **Lưu ý:** Kết quả trả về chỉ chính xác sau khi OpenXR session đã bắt đầu.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
