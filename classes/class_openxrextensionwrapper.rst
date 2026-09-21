:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRExtensionWrapper.xml.

.. _class_OpenXRExtensionWrapper:

OpenXRExtensionWrapper
======================

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`OpenXRAndroidThreadSettingsExtension<class_OpenXRAndroidThreadSettingsExtension>`, :ref:`OpenXRExtensionWrapperExtension<class_OpenXRExtensionWrapperExtension>`, :ref:`OpenXRFrameSynthesisExtension<class_OpenXRFrameSynthesisExtension>`, :ref:`OpenXRFutureExtension<class_OpenXRFutureExtension>`, :ref:`OpenXRRenderModelExtension<class_OpenXRRenderModelExtension>`, :ref:`OpenXRSpatialAnchorCapability<class_OpenXRSpatialAnchorCapability>`, :ref:`OpenXRSpatialEntityExtension<class_OpenXRSpatialEntityExtension>`, :ref:`OpenXRSpatialMarkerTrackingCapability<class_OpenXRSpatialMarkerTrackingCapability>`, :ref:`OpenXRSpatialPlaneTrackingCapability<class_OpenXRSpatialPlaneTrackingCapability>`

Cho phép triển khai các extension OpenXR bằng GDExtension.

.. rst-class:: classref-introduction-group

Mô tả
-----

**OpenXRExtensionWrapper** cho phép triển khai các extension OpenXR bằng GDExtension. Extension này phải được đăng ký với :ref:`register_extension_wrapper()<class_OpenXRExtensionWrapper_method_register_extension_wrapper>`.

Khi :ref:`OpenXRInterface<class_OpenXRInterface>` được khởi tạo làm interface chính và bất kỳ :ref:`Viewport<class_Viewport>` nào có :ref:`Viewport.use_xr<class_Viewport_property_use_xr>` được đặt thành ``true``, OpenXR sẽ tham gia vào quy trình rendering của Godot. Nếu :ref:`ProjectSettings.rendering/driver/threads/thread_model<class_ProjectSettings_property_rendering/driver/threads/thread_model>` được đặt thành "Separate", renderer của Godot sẽ chạy trên thread riêng, và cần đặc biệt cẩn thận trong mọi **OpenXRExtensionWrapper**\ s để tránh crash hoặc hành vi bất ngờ. Một số phương thức ảo sẽ được gọi trên render thread, và mọi dữ liệu mà chúng truy cập không được ghi trực tiếp trên main thread. Điều này nhằm ngăn chặn hai vấn đề tiềm ẩn:

1. Các thay đổi dự định áp dụng cho frame tiếp theo nhưng lại có hiệu lực ở frame hiện tại. Khi sử dụng thread model "Separate", main thread sẽ ngay lập tức bắt đầu xử lý frame tiếp theo trong khi render thread có thể vẫn đang render frame hiện tại. Nếu main thread trực tiếp thay đổi bất kỳ thứ gì được render thread sử dụng, thay đổi đó có thể bị áp dụng sớm hơn một frame so với dự định.

2. Việc đọc và ghi cùng một dữ liệu cùng lúc từ các thread khác nhau có thể khiến render thread sử dụng dữ liệu ở trạng thái không hợp lệ.

Trong hầu hết trường hợp, giải pháp là sử dụng :ref:`RenderingServer.call_on_render_thread()<class_RenderingServer_method_call_on_render_thread>` để lên lịch cho :ref:`Callable<class_Callable>`\ s ghi vào mọi dữ liệu được sử dụng trên render thread. Khi sử dụng thread model "Separate", các :ref:`Callable<class_Callable>`\ s này sẽ chạy sau khi renderer hoàn tất frame hiện tại và trước khi bắt đầu render frame tiếp theo. Khi không sử dụng mode này, chúng sẽ chạy ngay lập tức, vì vậy nên luôn sử dụng :ref:`RenderingServer.call_on_render_thread()<class_RenderingServer_method_call_on_render_thread>` trong các trường hợp này để code của bạn hoạt động đúng bất kể thread model nào.

Mọi phương thức ảo chạy trên render thread sẽ được ghi chú bên dưới.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_composition_layer<class_OpenXRExtensionWrapper_private_method__get_composition_layer>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                                        |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_composition_layer_count<class_OpenXRExtensionWrapper_private_method__get_composition_layer_count>`\ (\ ) |virtual|                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_composition_layer_order<class_OpenXRExtensionWrapper_private_method__get_composition_layer_order>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                            |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`_get_requested_extensions<class_OpenXRExtensionWrapper_private_method__get_requested_extensions>`\ (\ xr_version\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_suggested_tracker_names<class_OpenXRExtensionWrapper_private_method__get_suggested_tracker_names>`\ (\ ) |virtual|                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_viewport_composition_layer_extension_properties<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties>`\ (\ ) |virtual|                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`_get_viewport_composition_layer_extension_property_defaults<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_property_defaults>`\ (\ ) |virtual|                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_before_instance_created<class_OpenXRExtensionWrapper_private_method__on_before_instance_created>`\ (\ ) |virtual|                                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_on_event_polled<class_OpenXRExtensionWrapper_private_method__on_event_polled>`\ (\ event\: ``const void*``\ ) |virtual|                                                                                                                                                          |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_instance_created<class_OpenXRExtensionWrapper_private_method__on_instance_created>`\ (\ instance\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_instance_destroyed<class_OpenXRExtensionWrapper_private_method__on_instance_destroyed>`\ (\ ) |virtual|                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_main_swapchains_created<class_OpenXRExtensionWrapper_private_method__on_main_swapchains_created>`\ (\ ) |virtual|                                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_post_draw_viewport<class_OpenXRExtensionWrapper_private_method__on_post_draw_viewport>`\ (\ viewport\: :ref:`RID<class_RID>`\ ) |virtual|                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_pre_draw_viewport<class_OpenXRExtensionWrapper_private_method__on_pre_draw_viewport>`\ (\ viewport\: :ref:`RID<class_RID>`\ ) |virtual|                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_pre_render<class_OpenXRExtensionWrapper_private_method__on_pre_render>`\ (\ ) |virtual|                                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_process<class_OpenXRExtensionWrapper_private_method__on_process>`\ (\ ) |virtual|                                                                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_register_metadata<class_OpenXRExtensionWrapper_private_method__on_register_metadata>`\ (\ interaction_profile_metadata\: :ref:`OpenXRInteractionProfileMetadata<class_OpenXRInteractionProfileMetadata>`\ ) |virtual|                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_session_created<class_OpenXRExtensionWrapper_private_method__on_session_created>`\ (\ session\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                                            |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_session_destroyed<class_OpenXRExtensionWrapper_private_method__on_session_destroyed>`\ (\ ) |virtual|                                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_exiting<class_OpenXRExtensionWrapper_private_method__on_state_exiting>`\ (\ ) |virtual|                                                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_focused<class_OpenXRExtensionWrapper_private_method__on_state_focused>`\ (\ ) |virtual|                                                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_idle<class_OpenXRExtensionWrapper_private_method__on_state_idle>`\ (\ ) |virtual|                                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_loss_pending<class_OpenXRExtensionWrapper_private_method__on_state_loss_pending>`\ (\ ) |virtual|                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_ready<class_OpenXRExtensionWrapper_private_method__on_state_ready>`\ (\ ) |virtual|                                                                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_stopping<class_OpenXRExtensionWrapper_private_method__on_state_stopping>`\ (\ ) |virtual|                                                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_synchronized<class_OpenXRExtensionWrapper_private_method__on_state_synchronized>`\ (\ ) |virtual|                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_state_visible<class_OpenXRExtensionWrapper_private_method__on_state_visible>`\ (\ ) |virtual|                                                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_sync_actions<class_OpenXRExtensionWrapper_private_method__on_sync_actions>`\ (\ ) |virtual|                                                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_on_viewport_composition_layer_destroyed<class_OpenXRExtensionWrapper_private_method__on_viewport_composition_layer_destroyed>`\ (\ layer\: ``const void*``\ ) |virtual|                                                                                                          |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_prepare_view_configuration<class_OpenXRExtensionWrapper_private_method__prepare_view_configuration>`\ (\ view_count\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_print_view_configuration_info<class_OpenXRExtensionWrapper_private_method__print_view_configuration_info>`\ (\ view\: :ref:`int<class_int>`\ ) |virtual| |const|                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_android_surface_swapchain_create_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_android_surface_swapchain_create_info_and_get_next_pointer>`\ (\ property_values\: :ref:`Dictionary<class_Dictionary>`, next_pointer\: ``void*``\ ) |virtual|    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_frame_end_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_frame_end_info_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_frame_wait_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_frame_wait_info_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_hand_joint_locations_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_hand_joint_locations_and_get_next_pointer>`\ (\ hand_index\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual|                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_instance_create_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_instance_create_info_and_get_next_pointer>`\ (\ xr_version\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual|                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_projection_layer_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_projection_layer_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_projection_views_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_projection_views_and_get_next_pointer>`\ (\ view_index\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual|                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_reference_space_create_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_reference_space_create_info_and_get_next_pointer>`\ (\ reference_space_type\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual|                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_session_create_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_session_create_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_swapchain_create_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_swapchain_create_info_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_system_properties_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_system_properties_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_view_configuration_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_view_configuration_and_get_next_pointer>`\ (\ view\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual|                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_view_locate_info_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_view_locate_info_and_get_next_pointer>`\ (\ next_pointer\: ``void*``\ ) |virtual|                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_set_viewport_composition_layer_and_get_next_pointer<class_OpenXRExtensionWrapper_private_method__set_viewport_composition_layer_and_get_next_pointer>`\ (\ layer\: ``const void*``, property_values\: :ref:`Dictionary<class_Dictionary>`, next_pointer\: ``void*``\ ) |virtual| |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRAPIExtension<class_OpenXRAPIExtension>`              | :ref:`get_openxr_api<class_OpenXRExtensionWrapper_method_get_openxr_api>`\ (\ )                                                                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`register_extension_wrapper<class_OpenXRExtensionWrapper_method_register_extension_wrapper>`\ (\ )                                                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRExtensionWrapper_private_method__get_composition_layer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_composition_layer**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_composition_layer>`

Trả về một con trỏ đến struct ``XrCompositionLayerBaseHeader`` để cung cấp composition layer đã cho.

Phương thức này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_composition_layer_provider()<class_OpenXRAPIExtension_method_register_composition_layer_provider>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà phương thức trả về sẽ được sử dụng ngay sau khi phương thức này được gọi, vì vậy dữ liệu đó phải còn hợp lệ cho đến lần tiếp theo :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>` chạy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_composition_layer_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_composition_layer_count**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_composition_layer_count>`

Trả về số lượng composition layer mà extension wrapper này cung cấp thông qua :ref:`_get_composition_layer()<class_OpenXRExtensionWrapper_private_method__get_composition_layer>`.

Phương thức này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_composition_layer_provider()<class_OpenXRAPIExtension_method_register_composition_layer_provider>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà phương thức trả về sẽ được sử dụng ngay sau khi phương thức này được gọi, vì vậy dữ liệu đó phải còn hợp lệ cho đến lần tiếp theo :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>` chạy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_composition_layer_order:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_composition_layer_order**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_composition_layer_order>`

Trả về một số nguyên được dùng để sắp xếp composition layer đã cho, được cung cấp thông qua :ref:`_get_composition_layer()<class_OpenXRExtensionWrapper_private_method__get_composition_layer>`. Các số nhỏ hơn sẽ đưa layer lên đầu danh sách, còn các số lớn hơn sẽ đưa layer về cuối danh sách. Projection layer mặc định có thứ tự là ``0``, vì vậy các layer do phương thức này cung cấp có lẽ nên nằm trên hoặc dưới (nhưng không chính xác bằng) ``0``.

Phương thức này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_composition_layer_provider()<class_OpenXRAPIExtension_method_register_composition_layer_provider>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà phương thức trả về sẽ được sử dụng ngay sau khi phương thức này được gọi, vì vậy dữ liệu đó phải còn hợp lệ cho đến lần tiếp theo :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>` chạy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_requested_extensions:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_get_requested_extensions**\ (\ xr_version\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_requested_extensions>`

Trả về một :ref:`Dictionary<class_Dictionary>` các extension OpenXR liên quan đến extension này. ``xr_version`` chỉ định phiên bản OpenXR mà chúng ta đang khởi tạo. Giá trị này sẽ bằng zero nếu editor yêu cầu danh sách này để đánh dấu các feature được hỗ trợ. :ref:`Dictionary<class_Dictionary>` phải chứa tên của extension, được ánh xạ tới một ``bool *`` được ép kiểu thành số nguyên:

- Nếu ``bool *`` là một ``nullptr``, extension này là bắt buộc.

- Nếu ``bool *`` trỏ đến một boolean, boolean đó sẽ được cập nhật thành ``true`` nếu extension được bật.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_suggested_tracker_names:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_suggested_tracker_names**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_suggested_tracker_names>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` các tên positional tracker được sử dụng trong extension wrapper.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_viewport_composition_layer_extension_properties**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties>`

Lấy một mảng các :ref:`Dictionary<class_Dictionary>`\ s đại diện cho các property, tương tự như :ref:`Object._get_property_list()<class_Object_private_method__get_property_list>`, sẽ được thêm vào các node :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_property_defaults:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_get_viewport_composition_layer_extension_property_defaults**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_property_defaults>`

Lấy một :ref:`Dictionary<class_Dictionary>` chứa các giá trị mặc định cho những property được trả về bởi :ref:`_get_viewport_composition_layer_extension_properties()<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_before_instance_created:

.. rst-class:: classref-method

|void| **_on_before_instance_created**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_before_instance_created>`

Được gọi trước khi OpenXR instance được tạo.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên main thread, tuy nhiên, nó sẽ được gọi *trước khi* OpenXR tham gia vào rendering, vì vậy có thể an toàn ghi vào dữ liệu sẽ được render thread sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_event_polled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_on_event_polled**\ (\ event\: ``const void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_event_polled>`

Được gọi khi có một event OpenXR cần xử lý. Khi triển khai, trả về ``true`` nếu event đã được xử lý, nếu không thì trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_instance_created:

.. rst-class:: classref-method

|void| **_on_instance_created**\ (\ instance\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_instance_created>`

Được gọi ngay sau khi OpenXR instance được tạo.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên main thread, tuy nhiên, nó sẽ được gọi *trước khi* OpenXR tham gia vào rendering, vì vậy có thể an toàn ghi vào dữ liệu sẽ được render thread sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_instance_destroyed:

.. rst-class:: classref-method

|void| **_on_instance_destroyed**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_instance_destroyed>`

Được gọi ngay trước khi OpenXR instance bị hủy.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên main thread, tuy nhiên, nó sẽ được gọi *sau khi* OpenXR hoàn tất việc tham gia vào rendering, vì vậy có thể an toàn ghi vào dữ liệu đã được render thread sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_main_swapchains_created:

.. rst-class:: classref-method

|void| **_on_main_swapchains_created**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_main_swapchains_created>`

Được gọi ngay sau khi các main swapchain được tạo (lại).

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_post_draw_viewport:

.. rst-class:: classref-method

|void| **_on_post_draw_viewport**\ (\ viewport\: :ref:`RID<class_RID>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_post_draw_viewport>`

Được gọi ngay sau khi viewport đã cho được render.

\ **Lưu ý:** Các draw command có thể mới chỉ được đưa vào queue tại thời điểm này, chưa được thực thi.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_pre_draw_viewport:

.. rst-class:: classref-method

|void| **_on_pre_draw_viewport**\ (\ viewport\: :ref:`RID<class_RID>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_pre_draw_viewport>`

Được gọi ngay trước khi viewport đã cho được render.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_pre_render:

.. rst-class:: classref-method

|void| **_on_pre_render**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_pre_render>`

Được gọi ngay trước khi các XR viewport bắt đầu bước rendering của chúng.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_process:

.. rst-class:: classref-method

|void| **_on_process**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_process>`

Được gọi như một phần của quá trình xử lý OpenXR. Việc này diễn ra ngay trước các bước xử lý tổng quát và vật lý của main loop. Trong bước này, dữ liệu controller được truy vấn và cung cấp cho game logic.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_register_metadata:

.. rst-class:: classref-method

|void| **_on_register_metadata**\ (\ interaction_profile_metadata\: :ref:`OpenXRInteractionProfileMetadata<class_OpenXRInteractionProfileMetadata>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_register_metadata>`

Cho phép các extension đăng ký metadata bổ sung cho controller. Hàm này được gọi ngay cả khi API OpenXR chưa được khởi tạo, vì metadata cần phải có sẵn cho editor.

Các extension cũng nên cung cấp metadata bất kể chúng có được hỗ trợ trên hệ thống host hay không. Dữ liệu controller được dùng để thiết lập action map cho những người dùng có thể truy cập phần cứng tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_session_created:

.. rst-class:: classref-method

|void| **_on_session_created**\ (\ session\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_session_created>`

Được gọi ngay sau khi session OpenXR được tạo.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên main thread, tuy nhiên, nó sẽ được gọi *trước khi* OpenXR bắt đầu tham gia vào quá trình rendering, vì vậy việc ghi vào dữ liệu sẽ được render thread sử dụng là an toàn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_session_destroyed:

.. rst-class:: classref-method

|void| **_on_session_destroyed**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_session_destroyed>`

Được gọi ngay trước khi session OpenXR bị hủy.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên main thread, tuy nhiên, nó sẽ được gọi *sau khi* OpenXR hoàn tất việc tham gia vào quá trình rendering, vì vậy việc ghi vào dữ liệu đã được render thread sử dụng là an toàn.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_exiting:

.. rst-class:: classref-method

|void| **_on_state_exiting**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_exiting>`

Được gọi khi trạng thái session OpenXR được chuyển thành exiting.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_focused:

.. rst-class:: classref-method

|void| **_on_state_focused**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_focused>`

Được gọi khi trạng thái session OpenXR được chuyển thành focused. Đây là trạng thái hoạt động khi game chạy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_idle:

.. rst-class:: classref-method

|void| **_on_state_idle**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_idle>`

Được gọi khi trạng thái session OpenXR được chuyển thành idle.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_loss_pending:

.. rst-class:: classref-method

|void| **_on_state_loss_pending**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_loss_pending>`

Được gọi khi trạng thái session OpenXR được chuyển thành loss pending.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_ready:

.. rst-class:: classref-method

|void| **_on_state_ready**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_ready>`

Được gọi khi trạng thái session OpenXR được chuyển thành ready. Điều này có nghĩa là OpenXR đã sẵn sàng thiết lập session.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_stopping:

.. rst-class:: classref-method

|void| **_on_state_stopping**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_stopping>`

Được gọi khi trạng thái session OpenXR được chuyển thành stopping.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_synchronized:

.. rst-class:: classref-method

|void| **_on_state_synchronized**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_synchronized>`

Được gọi khi trạng thái session OpenXR được chuyển thành synchronized. OpenXR cũng quay lại trạng thái này khi ứng dụng mất focus.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_state_visible:

.. rst-class:: classref-method

|void| **_on_state_visible**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_state_visible>`

Được gọi khi trạng thái session OpenXR được chuyển thành visible. Điều này có nghĩa là OpenXR hiện đã sẵn sàng nhận các frame.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_sync_actions:

.. rst-class:: classref-method

|void| **_on_sync_actions**\ (\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_sync_actions>`

Được gọi khi OpenXR đã thực hiện đồng bộ action.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__on_viewport_composition_layer_destroyed:

.. rst-class:: classref-method

|void| **_on_viewport_composition_layer_destroyed**\ (\ layer\: ``const void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__on_viewport_composition_layer_destroyed>`

Được gọi khi composition layer được tạo thông qua :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>` bị hủy.

\ ``layer`` là một con trỏ đến struct ``XrCompositionLayerBaseHeader``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__prepare_view_configuration:

.. rst-class:: classref-method

|void| **_prepare_view_configuration**\ (\ view_count\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__prepare_view_configuration>`

Được gọi trước :ref:`_set_view_configuration_and_get_next_pointer()<class_OpenXRExtensionWrapper_private_method__set_view_configuration_and_get_next_pointer>` để cho phép extension dành chỗ cho dữ liệu tương ứng với số lượng view đã cho.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__print_view_configuration_info:

.. rst-class:: classref-method

|void| **_print_view_configuration_info**\ (\ view\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__print_view_configuration_info>`

Được gọi để cho phép extension in thêm thông tin về view configuration của nó, nếu phù hợp. Hàm này chỉ được gọi khi đầu ra verbose được bật.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_android_surface_swapchain_create_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_android_surface_swapchain_create_info_and_get_next_pointer**\ (\ property_values\: :ref:`Dictionary<class_Dictionary>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_android_surface_swapchain_create_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào Android surface swapchain được tạo bởi :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>`.

\ ``property_values`` chứa các giá trị của những property được :ref:`_get_viewport_composition_layer_extension_properties()<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties>` trả về.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_frame_end_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_frame_end_info_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_frame_end_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào ``XrFrameEndInfo``.

Hàm này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_frame_info_extension()<class_OpenXRAPIExtension_method_register_frame_info_extension>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà hàm trả về sẽ được sử dụng ngay sau khi hàm này được gọi, vì vậy dữ liệu đó phải duy trì hiệu lực cho đến lần chạy tiếp theo của :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_frame_wait_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_frame_wait_info_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_frame_wait_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào ``XrFrameWaitInfo``.

Hàm này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_frame_info_extension()<class_OpenXRAPIExtension_method_register_frame_info_extension>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_hand_joint_locations_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_hand_joint_locations_and_get_next_pointer**\ (\ hand_index\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_hand_joint_locations_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi mỗi hand tracker được tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_instance_create_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_instance_create_info_and_get_next_pointer**\ (\ xr_version\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_instance_create_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi instance OpenXR được tạo. ``xr_version`` chỉ định phiên bản OpenXR mà chúng ta đang khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_projection_layer_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_projection_layer_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_projection_layer_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào ``XrCompositionLayerProjection``.

Hàm này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_projection_layer_extension()<class_OpenXRAPIExtension_method_register_projection_layer_extension>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_projection_views_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_projection_views_and_get_next_pointer**\ (\ view_index\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_projection_views_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào projection view của ``view_index`` đã cho.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà hàm trả về sẽ được sử dụng ngay sau khi hàm này được gọi, vì vậy dữ liệu đó phải duy trì hiệu lực cho đến lần chạy tiếp theo của :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_reference_space_create_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_reference_space_create_info_and_get_next_pointer**\ (\ reference_space_type\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_reference_space_create_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào ``XrReferenceSpaceCreateInfo``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_session_create_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_session_create_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_session_create_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi session OpenXR được tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_swapchain_create_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_swapchain_create_info_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_swapchain_create_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi tạo swapchain OpenXR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_system_properties_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_system_properties_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_system_properties_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi truy vấn các system capabilities của OpenXR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_view_configuration_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_view_configuration_and_get_next_pointer**\ (\ view\: :ref:`int<class_int>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_view_configuration_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung khi truy vấn view configuration của OpenXR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_view_locate_info_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_view_locate_info_and_get_next_pointer**\ (\ next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_view_locate_info_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào ``XrViewLocateInfo``.

Hàm này chỉ được gọi nếu extension trước đó đã tự đăng ký với :ref:`OpenXRAPIExtension.register_frame_info_extension()<class_OpenXRAPIExtension_method_register_frame_info_extension>`.

\ **Lưu ý:** Phương thức ảo này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà hàm trả về sẽ được sử dụng ngay sau khi hàm này được gọi, vì vậy dữ liệu đó phải duy trì hiệu lực cho đến lần chạy tiếp theo của :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_private_method__set_viewport_composition_layer_and_get_next_pointer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_set_viewport_composition_layer_and_get_next_pointer**\ (\ layer\: ``const void*``, property_values\: :ref:`Dictionary<class_Dictionary>`, next_pointer\: ``void*``\ ) |virtual| :ref:`🔗<class_OpenXRExtensionWrapper_private_method__set_viewport_composition_layer_and_get_next_pointer>`

Thêm các cấu trúc dữ liệu bổ sung vào các composition layer được tạo bởi :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>`.

\ ``property_values`` chứa các giá trị của những thuộc tính được :ref:`_get_viewport_composition_layer_extension_properties()<class_OpenXRExtensionWrapper_private_method__get_viewport_composition_layer_extension_properties>` trả về.

\ ``layer`` là một con trỏ tới một struct ``XrCompositionLayerBaseHeader``.

\ **Lưu ý:** Phương thức virtual này sẽ được gọi trên render thread. Ngoài ra, dữ liệu mà phương thức này trả về sẽ được sử dụng ngay sau khi phương thức được gọi, vì vậy dữ liệu cần vẫn hợp lệ cho đến lần tiếp theo :ref:`_on_pre_render()<class_OpenXRExtensionWrapper_private_method__on_pre_render>` chạy.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_method_get_openxr_api:

.. rst-class:: classref-method

:ref:`OpenXRAPIExtension<class_OpenXRAPIExtension>` **get_openxr_api**\ (\ ) :ref:`🔗<class_OpenXRExtensionWrapper_method_get_openxr_api>`

Trả về :ref:`OpenXRAPIExtension<class_OpenXRAPIExtension>` đã được tạo, có thể dùng để truy cập OpenXR API.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRExtensionWrapper_method_register_extension_wrapper:

.. rst-class:: classref-method

|void| **register_extension_wrapper**\ (\ ) :ref:`🔗<class_OpenXRExtensionWrapper_method_register_extension_wrapper>`

Đăng ký extension. Việc này nên được thực hiện ở cấp độ khởi tạo core module.

\ **Lưu ý:** Không thể gọi hàm này sau khi OpenXR đã được khởi tạo.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
