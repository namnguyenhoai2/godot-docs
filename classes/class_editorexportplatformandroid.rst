:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/platform/android/doc_classes/EditorExportPlatformAndroid.xml.

.. _class_EditorExportPlatformAndroid:

EditorExportPlatformAndroid
===========================

**Kế thừa:** :ref:`EditorExportPlatform<class_EditorExportPlatform>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Exporter cho Android.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Xuất cho Android <../tutorials/export/exporting_for_android>`

- :doc:`Build Gradle cho Android <../tutorials/export/android_gradle_build>`

- :doc:`Chỉ mục tài liệu về plugin Android <../tutorials/platform/index>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`architectures/arm64-v8a<class_EditorExportPlatformAndroid_property_architectures/arm64-v8a>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`architectures/armeabi-v7a<class_EditorExportPlatformAndroid_property_architectures/armeabi-v7a>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`architectures/x86<class_EditorExportPlatformAndroid_property_architectures/x86>`                                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`architectures/x86_64<class_EditorExportPlatformAndroid_property_architectures/x86_64>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`command_line/extra_args<class_EditorExportPlatformAndroid_property_command_line/extra_args>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/debug<class_EditorExportPlatformAndroid_property_custom_template/debug>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/release<class_EditorExportPlatformAndroid_property_custom_template/release>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`gesture/swipe_to_dismiss<class_EditorExportPlatformAndroid_property_gesture/swipe_to_dismiss>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`gradle_build/android_source_template<class_EditorExportPlatformAndroid_property_gradle_build/android_source_template>`                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`gradle_build/compress_native_libraries<class_EditorExportPlatformAndroid_property_gradle_build/compress_native_libraries>`                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`gradle_build/custom_theme_attributes<class_EditorExportPlatformAndroid_property_gradle_build/custom_theme_attributes>`                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`gradle_build/export_format<class_EditorExportPlatformAndroid_property_gradle_build/export_format>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`gradle_build/gradle_build_directory<class_EditorExportPlatformAndroid_property_gradle_build/gradle_build_directory>`                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`gradle_build/min_sdk<class_EditorExportPlatformAndroid_property_gradle_build/min_sdk>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`gradle_build/target_sdk<class_EditorExportPlatformAndroid_property_gradle_build/target_sdk>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`graphics/opengl_debug<class_EditorExportPlatformAndroid_property_graphics/opengl_debug>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/debug<class_EditorExportPlatformAndroid_property_keystore/debug>`                                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/debug_password<class_EditorExportPlatformAndroid_property_keystore/debug_password>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/debug_user<class_EditorExportPlatformAndroid_property_keystore/debug_user>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/release<class_EditorExportPlatformAndroid_property_keystore/release>`                                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/release_password<class_EditorExportPlatformAndroid_property_keystore/release_password>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`keystore/release_user<class_EditorExportPlatformAndroid_property_keystore/release_user>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`launcher_icons/adaptive_background_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_background_432x432>`         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`launcher_icons/adaptive_foreground_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_foreground_432x432>`         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`launcher_icons/adaptive_monochrome_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_monochrome_432x432>`         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`launcher_icons/main_192x192<class_EditorExportPlatformAndroid_property_launcher_icons/main_192x192>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`package/app_category<class_EditorExportPlatformAndroid_property_package/app_category>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/exclude_from_recents<class_EditorExportPlatformAndroid_property_package/exclude_from_recents>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`package/name<class_EditorExportPlatformAndroid_property_package/name>`                                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/retain_data_on_uninstall<class_EditorExportPlatformAndroid_property_package/retain_data_on_uninstall>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/show_as_launcher_app<class_EditorExportPlatformAndroid_property_package/show_as_launcher_app>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/show_in_android_tv<class_EditorExportPlatformAndroid_property_package/show_in_android_tv>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/show_in_app_library<class_EditorExportPlatformAndroid_property_package/show_in_app_library>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`package/signed<class_EditorExportPlatformAndroid_property_package/signed>`                                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`package/unique_name<class_EditorExportPlatformAndroid_property_package/unique_name>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_checkin_properties<class_EditorExportPlatformAndroid_property_permissions/access_checkin_properties>`                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_coarse_location<class_EditorExportPlatformAndroid_property_permissions/access_coarse_location>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_fine_location<class_EditorExportPlatformAndroid_property_permissions/access_fine_location>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_location_extra_commands<class_EditorExportPlatformAndroid_property_permissions/access_location_extra_commands>`         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_media_location<class_EditorExportPlatformAndroid_property_permissions/access_media_location>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_mock_location<class_EditorExportPlatformAndroid_property_permissions/access_mock_location>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_network_state<class_EditorExportPlatformAndroid_property_permissions/access_network_state>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_surface_flinger<class_EditorExportPlatformAndroid_property_permissions/access_surface_flinger>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/access_wifi_state<class_EditorExportPlatformAndroid_property_permissions/access_wifi_state>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/account_manager<class_EditorExportPlatformAndroid_property_permissions/account_manager>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/add_voicemail<class_EditorExportPlatformAndroid_property_permissions/add_voicemail>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/authenticate_accounts<class_EditorExportPlatformAndroid_property_permissions/authenticate_accounts>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/battery_stats<class_EditorExportPlatformAndroid_property_permissions/battery_stats>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_accessibility_service<class_EditorExportPlatformAndroid_property_permissions/bind_accessibility_service>`                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_appwidget<class_EditorExportPlatformAndroid_property_permissions/bind_appwidget>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_device_admin<class_EditorExportPlatformAndroid_property_permissions/bind_device_admin>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_input_method<class_EditorExportPlatformAndroid_property_permissions/bind_input_method>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_nfc_service<class_EditorExportPlatformAndroid_property_permissions/bind_nfc_service>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_notification_listener_service<class_EditorExportPlatformAndroid_property_permissions/bind_notification_listener_service>` |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_print_service<class_EditorExportPlatformAndroid_property_permissions/bind_print_service>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_remoteviews<class_EditorExportPlatformAndroid_property_permissions/bind_remoteviews>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_text_service<class_EditorExportPlatformAndroid_property_permissions/bind_text_service>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_vpn_service<class_EditorExportPlatformAndroid_property_permissions/bind_vpn_service>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bind_wallpaper<class_EditorExportPlatformAndroid_property_permissions/bind_wallpaper>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bluetooth<class_EditorExportPlatformAndroid_property_permissions/bluetooth>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bluetooth_admin<class_EditorExportPlatformAndroid_property_permissions/bluetooth_admin>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/bluetooth_privileged<class_EditorExportPlatformAndroid_property_permissions/bluetooth_privileged>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/brick<class_EditorExportPlatformAndroid_property_permissions/brick>`                                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/broadcast_package_removed<class_EditorExportPlatformAndroid_property_permissions/broadcast_package_removed>`                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/broadcast_sms<class_EditorExportPlatformAndroid_property_permissions/broadcast_sms>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/broadcast_sticky<class_EditorExportPlatformAndroid_property_permissions/broadcast_sticky>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/broadcast_wap_push<class_EditorExportPlatformAndroid_property_permissions/broadcast_wap_push>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/call_phone<class_EditorExportPlatformAndroid_property_permissions/call_phone>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/call_privileged<class_EditorExportPlatformAndroid_property_permissions/call_privileged>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/camera<class_EditorExportPlatformAndroid_property_permissions/camera>`                                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/capture_audio_output<class_EditorExportPlatformAndroid_property_permissions/capture_audio_output>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/capture_secure_video_output<class_EditorExportPlatformAndroid_property_permissions/capture_secure_video_output>`               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/capture_video_output<class_EditorExportPlatformAndroid_property_permissions/capture_video_output>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/change_component_enabled_state<class_EditorExportPlatformAndroid_property_permissions/change_component_enabled_state>`         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/change_configuration<class_EditorExportPlatformAndroid_property_permissions/change_configuration>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/change_network_state<class_EditorExportPlatformAndroid_property_permissions/change_network_state>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/change_wifi_multicast_state<class_EditorExportPlatformAndroid_property_permissions/change_wifi_multicast_state>`               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/change_wifi_state<class_EditorExportPlatformAndroid_property_permissions/change_wifi_state>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/clear_app_cache<class_EditorExportPlatformAndroid_property_permissions/clear_app_cache>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/clear_app_user_data<class_EditorExportPlatformAndroid_property_permissions/clear_app_user_data>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/control_location_updates<class_EditorExportPlatformAndroid_property_permissions/control_location_updates>`                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`permissions/custom_permissions<class_EditorExportPlatformAndroid_property_permissions/custom_permissions>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/delete_cache_files<class_EditorExportPlatformAndroid_property_permissions/delete_cache_files>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/delete_packages<class_EditorExportPlatformAndroid_property_permissions/delete_packages>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/device_power<class_EditorExportPlatformAndroid_property_permissions/device_power>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/diagnostic<class_EditorExportPlatformAndroid_property_permissions/diagnostic>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/disable_keyguard<class_EditorExportPlatformAndroid_property_permissions/disable_keyguard>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/dump<class_EditorExportPlatformAndroid_property_permissions/dump>`                                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/expand_status_bar<class_EditorExportPlatformAndroid_property_permissions/expand_status_bar>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/factory_test<class_EditorExportPlatformAndroid_property_permissions/factory_test>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/flashlight<class_EditorExportPlatformAndroid_property_permissions/flashlight>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/force_back<class_EditorExportPlatformAndroid_property_permissions/force_back>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/get_accounts<class_EditorExportPlatformAndroid_property_permissions/get_accounts>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/get_package_size<class_EditorExportPlatformAndroid_property_permissions/get_package_size>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/get_tasks<class_EditorExportPlatformAndroid_property_permissions/get_tasks>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/get_top_activity_info<class_EditorExportPlatformAndroid_property_permissions/get_top_activity_info>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/global_search<class_EditorExportPlatformAndroid_property_permissions/global_search>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/hardware_test<class_EditorExportPlatformAndroid_property_permissions/hardware_test>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/inject_events<class_EditorExportPlatformAndroid_property_permissions/inject_events>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/install_location_provider<class_EditorExportPlatformAndroid_property_permissions/install_location_provider>`                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/install_packages<class_EditorExportPlatformAndroid_property_permissions/install_packages>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/install_shortcut<class_EditorExportPlatformAndroid_property_permissions/install_shortcut>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/internal_system_window<class_EditorExportPlatformAndroid_property_permissions/internal_system_window>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/internet<class_EditorExportPlatformAndroid_property_permissions/internet>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/kill_background_processes<class_EditorExportPlatformAndroid_property_permissions/kill_background_processes>`                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/location_hardware<class_EditorExportPlatformAndroid_property_permissions/location_hardware>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/manage_accounts<class_EditorExportPlatformAndroid_property_permissions/manage_accounts>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/manage_app_tokens<class_EditorExportPlatformAndroid_property_permissions/manage_app_tokens>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/manage_documents<class_EditorExportPlatformAndroid_property_permissions/manage_documents>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/manage_external_storage<class_EditorExportPlatformAndroid_property_permissions/manage_external_storage>`                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/manage_media<class_EditorExportPlatformAndroid_property_permissions/manage_media>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/master_clear<class_EditorExportPlatformAndroid_property_permissions/master_clear>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/media_content_control<class_EditorExportPlatformAndroid_property_permissions/media_content_control>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/modify_audio_settings<class_EditorExportPlatformAndroid_property_permissions/modify_audio_settings>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/modify_phone_state<class_EditorExportPlatformAndroid_property_permissions/modify_phone_state>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/mount_format_filesystems<class_EditorExportPlatformAndroid_property_permissions/mount_format_filesystems>`                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/mount_unmount_filesystems<class_EditorExportPlatformAndroid_property_permissions/mount_unmount_filesystems>`                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/nfc<class_EditorExportPlatformAndroid_property_permissions/nfc>`                                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/persistent_activity<class_EditorExportPlatformAndroid_property_permissions/persistent_activity>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/post_notifications<class_EditorExportPlatformAndroid_property_permissions/post_notifications>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/process_outgoing_calls<class_EditorExportPlatformAndroid_property_permissions/process_outgoing_calls>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_calendar<class_EditorExportPlatformAndroid_property_permissions/read_calendar>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_call_log<class_EditorExportPlatformAndroid_property_permissions/read_call_log>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_contacts<class_EditorExportPlatformAndroid_property_permissions/read_contacts>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_external_storage<class_EditorExportPlatformAndroid_property_permissions/read_external_storage>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_frame_buffer<class_EditorExportPlatformAndroid_property_permissions/read_frame_buffer>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_history_bookmarks<class_EditorExportPlatformAndroid_property_permissions/read_history_bookmarks>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_input_state<class_EditorExportPlatformAndroid_property_permissions/read_input_state>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_logs<class_EditorExportPlatformAndroid_property_permissions/read_logs>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_media_audio<class_EditorExportPlatformAndroid_property_permissions/read_media_audio>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_media_images<class_EditorExportPlatformAndroid_property_permissions/read_media_images>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_media_video<class_EditorExportPlatformAndroid_property_permissions/read_media_video>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_media_visual_user_selected<class_EditorExportPlatformAndroid_property_permissions/read_media_visual_user_selected>`       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_phone_state<class_EditorExportPlatformAndroid_property_permissions/read_phone_state>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_profile<class_EditorExportPlatformAndroid_property_permissions/read_profile>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_sms<class_EditorExportPlatformAndroid_property_permissions/read_sms>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_social_stream<class_EditorExportPlatformAndroid_property_permissions/read_social_stream>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_sync_settings<class_EditorExportPlatformAndroid_property_permissions/read_sync_settings>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_sync_stats<class_EditorExportPlatformAndroid_property_permissions/read_sync_stats>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/read_user_dictionary<class_EditorExportPlatformAndroid_property_permissions/read_user_dictionary>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/reboot<class_EditorExportPlatformAndroid_property_permissions/reboot>`                                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/receive_boot_completed<class_EditorExportPlatformAndroid_property_permissions/receive_boot_completed>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/receive_mms<class_EditorExportPlatformAndroid_property_permissions/receive_mms>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/receive_sms<class_EditorExportPlatformAndroid_property_permissions/receive_sms>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/receive_wap_push<class_EditorExportPlatformAndroid_property_permissions/receive_wap_push>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/record_audio<class_EditorExportPlatformAndroid_property_permissions/record_audio>`                                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/reorder_tasks<class_EditorExportPlatformAndroid_property_permissions/reorder_tasks>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/restart_packages<class_EditorExportPlatformAndroid_property_permissions/restart_packages>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/send_respond_via_message<class_EditorExportPlatformAndroid_property_permissions/send_respond_via_message>`                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/send_sms<class_EditorExportPlatformAndroid_property_permissions/send_sms>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_activity_watcher<class_EditorExportPlatformAndroid_property_permissions/set_activity_watcher>`                             |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_alarm<class_EditorExportPlatformAndroid_property_permissions/set_alarm>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_always_finish<class_EditorExportPlatformAndroid_property_permissions/set_always_finish>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_animation_scale<class_EditorExportPlatformAndroid_property_permissions/set_animation_scale>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_debug_app<class_EditorExportPlatformAndroid_property_permissions/set_debug_app>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_orientation<class_EditorExportPlatformAndroid_property_permissions/set_orientation>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_pointer_speed<class_EditorExportPlatformAndroid_property_permissions/set_pointer_speed>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_preferred_applications<class_EditorExportPlatformAndroid_property_permissions/set_preferred_applications>`                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_process_limit<class_EditorExportPlatformAndroid_property_permissions/set_process_limit>`                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_time<class_EditorExportPlatformAndroid_property_permissions/set_time>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_time_zone<class_EditorExportPlatformAndroid_property_permissions/set_time_zone>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_wallpaper<class_EditorExportPlatformAndroid_property_permissions/set_wallpaper>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/set_wallpaper_hints<class_EditorExportPlatformAndroid_property_permissions/set_wallpaper_hints>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/signal_persistent_processes<class_EditorExportPlatformAndroid_property_permissions/signal_persistent_processes>`               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/status_bar<class_EditorExportPlatformAndroid_property_permissions/status_bar>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/subscribed_feeds_read<class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_read>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/subscribed_feeds_write<class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_write>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/system_alert_window<class_EditorExportPlatformAndroid_property_permissions/system_alert_window>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/transmit_ir<class_EditorExportPlatformAndroid_property_permissions/transmit_ir>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/uninstall_shortcut<class_EditorExportPlatformAndroid_property_permissions/uninstall_shortcut>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/update_device_stats<class_EditorExportPlatformAndroid_property_permissions/update_device_stats>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/use_credentials<class_EditorExportPlatformAndroid_property_permissions/use_credentials>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/use_sip<class_EditorExportPlatformAndroid_property_permissions/use_sip>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/vibrate<class_EditorExportPlatformAndroid_property_permissions/vibrate>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/wake_lock<class_EditorExportPlatformAndroid_property_permissions/wake_lock>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_apn_settings<class_EditorExportPlatformAndroid_property_permissions/write_apn_settings>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_calendar<class_EditorExportPlatformAndroid_property_permissions/write_calendar>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_call_log<class_EditorExportPlatformAndroid_property_permissions/write_call_log>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_contacts<class_EditorExportPlatformAndroid_property_permissions/write_contacts>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_external_storage<class_EditorExportPlatformAndroid_property_permissions/write_external_storage>`                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_gservices<class_EditorExportPlatformAndroid_property_permissions/write_gservices>`                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_history_bookmarks<class_EditorExportPlatformAndroid_property_permissions/write_history_bookmarks>`                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_profile<class_EditorExportPlatformAndroid_property_permissions/write_profile>`                                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_secure_settings<class_EditorExportPlatformAndroid_property_permissions/write_secure_settings>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_settings<class_EditorExportPlatformAndroid_property_permissions/write_settings>`                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_sms<class_EditorExportPlatformAndroid_property_permissions/write_sms>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_social_stream<class_EditorExportPlatformAndroid_property_permissions/write_social_stream>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_sync_settings<class_EditorExportPlatformAndroid_property_permissions/write_sync_settings>`                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`permissions/write_user_dictionary<class_EditorExportPlatformAndroid_property_permissions/write_user_dictionary>`                           |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                         | :ref:`screen/background_color<class_EditorExportPlatformAndroid_property_screen/background_color>`                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/edge_to_edge<class_EditorExportPlatformAndroid_property_screen/edge_to_edge>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/immersive_mode<class_EditorExportPlatformAndroid_property_screen/immersive_mode>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/support_large<class_EditorExportPlatformAndroid_property_screen/support_large>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/support_normal<class_EditorExportPlatformAndroid_property_screen/support_normal>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/support_small<class_EditorExportPlatformAndroid_property_screen/support_small>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`screen/support_xlarge<class_EditorExportPlatformAndroid_property_screen/support_xlarge>`                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`shader_baker/enabled<class_EditorExportPlatformAndroid_property_shader_baker/enabled>`                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                         | :ref:`splash_screen/background_color<class_EditorExportPlatformAndroid_property_splash_screen/background_color>`                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`splash_screen/branding_image<class_EditorExportPlatformAndroid_property_splash_screen/branding_image>`                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`splash_screen/disable_godot_boot_splash<class_EditorExportPlatformAndroid_property_splash_screen/disable_godot_boot_splash>`               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`splash_screen/icon<class_EditorExportPlatformAndroid_property_splash_screen/icon>`                                                         |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`user_data_backup/allow<class_EditorExportPlatformAndroid_property_user_data_backup/allow>`                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`version/code<class_EditorExportPlatformAndroid_property_version/code>`                                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`version/name<class_EditorExportPlatformAndroid_property_version/name>`                                                                     |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`xr_features/xr_mode<class_EditorExportPlatformAndroid_property_xr_features/xr_mode>`                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorExportPlatformAndroid_property_architectures/arm64-v8a:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **architectures/arm64-v8a** :ref:`🔗<class_EditorExportPlatformAndroid_property_architectures/arm64-v8a>`

Nếu ``true``, các binary ``arm64`` được đưa vào project đã xuất.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_architectures/armeabi-v7a:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **architectures/armeabi-v7a** :ref:`🔗<class_EditorExportPlatformAndroid_property_architectures/armeabi-v7a>`

Nếu ``true``, các binary ``arm32`` được đưa vào project đã xuất.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_architectures/x86:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **architectures/x86** :ref:`🔗<class_EditorExportPlatformAndroid_property_architectures/x86>`

Nếu ``true``, các binary ``x86_32`` được đưa vào project đã xuất.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_architectures/x86_64:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **architectures/x86_64** :ref:`🔗<class_EditorExportPlatformAndroid_property_architectures/x86_64>`

Nếu ``true``, các binary ``x86_64`` được đưa vào project đã xuất.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_command_line/extra_args:

.. rst-class:: classref-property

:ref:`String<class_String>` **command_line/extra_args** :ref:`🔗<class_EditorExportPlatformAndroid_property_command_line/extra_args>`

Danh sách các đối số command line bổ sung, được phân tách bằng dấu cách, mà project đã xuất sẽ nhận khi khởi chạy.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_custom_template/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/debug** :ref:`🔗<class_EditorExportPlatformAndroid_property_custom_template/debug>`

Đường dẫn đến tệp APK được sử dụng làm export template tùy chỉnh cho các bản export debug. Nếu để trống, template mặc định sẽ được sử dụng.

\ **Lưu ý:** Tùy chọn này chỉ được sử dụng nếu :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` bị tắt.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_custom_template/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/release** :ref:`🔗<class_EditorExportPlatformAndroid_property_custom_template/release>`

Đường dẫn đến tệp APK được sử dụng làm export template tùy chỉnh cho các bản export release. Nếu để trống, template mặc định sẽ được sử dụng.

\ **Lưu ý:** Tùy chọn này chỉ được sử dụng nếu :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` bị tắt.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gesture/swipe_to_dismiss:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **gesture/swipe_to_dismiss** :ref:`🔗<class_EditorExportPlatformAndroid_property_gesture/swipe_to_dismiss>`

Nếu ``true``, `Swipe to dismiss <https://developer.android.com/design/ui/wear/guides/components/swipe-to-dismiss>`__ sẽ được bật.

Chức năng này dành cho smartwatch và thường bị bỏ qua trên các thiết bị Android tiêu chuẩn. Tuy nhiên, một số thiết bị có thể không bỏ qua chức năng này. Do đó, bạn nên tắt tính năng này cho các ứng dụng Android tiêu chuẩn để tránh hành vi không mong muốn.

\ **Lưu ý:** Tùy chọn này ``false`` theo mặc định. Để bật hành vi này, cần có :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/android_source_template:

.. rst-class:: classref-property

:ref:`String<class_String>` **gradle_build/android_source_template** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/android_source_template>`

Đường dẫn đến tệp ZIP chứa mã nguồn của export template được sử dụng trong Gradle build. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/compress_native_libraries:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **gradle_build/compress_native_libraries** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/compress_native_libraries>`

Nếu ``true``, các native library sẽ được nén khi thực hiện Gradle build.

\ **Lưu ý:** Mặc dù bật tính năng nén có thể giảm kích thước binary, điều này có thể khiến ứng dụng khởi động chậm hơn vì các native library phải được giải nén trước khi sử dụng thay vì được load trực tiếp.

Nếu bạn phân phối ứng dụng qua Play Store, nhìn chung nên để tùy chọn này ở trạng thái ``false``, xem `official documentation <https://developer.android.com/build/releases/past-releases/agp-3-6-0-release-notes#extractNativeLibs>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/custom_theme_attributes:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **gradle_build/custom_theme_attributes** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/custom_theme_attributes>`

Một dictionary gồm các theme attribute tùy chỉnh cần đưa vào project Android đã xuất. Mỗi mục xác định tên theme attribute và giá trị của nó, sau đó sẽ được thêm vào **GodotAppMainTheme**.

Ví dụ, key ``android:windowSwipeToDismiss`` với giá trị ``false`` sẽ được phân giải thành ``<item name="android:windowSwipeToDismiss">false</item>``.

\ **Lưu ý:** Để thêm attribute tùy chỉnh vào **GodotAppSplashTheme**, hãy thêm tiền tố ``[splash]`` vào tên attribute.

\ **Lưu ý:** Các attribute dành riêng được cấu hình qua những tùy chọn export hoặc project settings khác không thể bị ``custom_theme_attributes`` ghi đè và sẽ bị bỏ qua trong quá trình export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/export_format:

.. rst-class:: classref-property

:ref:`int<class_int>` **gradle_build/export_format** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/export_format>`

Định dạng export ứng dụng (\*.apk hoặc \*.aab).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/gradle_build_directory:

.. rst-class:: classref-property

:ref:`String<class_String>` **gradle_build/gradle_build_directory** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/gradle_build_directory>`

Đường dẫn đến thư mục Gradle build. Nếu để trống, ``res://android`` sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/min_sdk:

.. rst-class:: classref-property

:ref:`String<class_String>` **gradle_build/min_sdk** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/min_sdk>`

Android API level tối thiểu cần thiết để ứng dụng chạy (được sử dụng trong Gradle build). Xem `android:minSdkVersion <https://developer.android.com/guide/topics/manifest/uses-sdk-element#uses>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/target_sdk:

.. rst-class:: classref-property

:ref:`String<class_String>` **gradle_build/target_sdk** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/target_sdk>`

Android API level mà ứng dụng được thiết kế để chạy trên đó (được sử dụng trong Gradle build). Xem `android:targetSdkVersion <https://developer.android.com/guide/topics/manifest/uses-sdk-element#uses>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **gradle_build/use_gradle_build** :ref:`🔗<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>`

Nếu ``true``, Gradle build sẽ được sử dụng thay cho APK dựng sẵn.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_graphics/opengl_debug:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **graphics/opengl_debug** :ref:`🔗<class_EditorExportPlatformAndroid_property_graphics/opengl_debug>`

Nếu ``true``, debug context của OpenGL ES sẽ được tạo (bổ sung việc kiểm tra runtime, validation và logging).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/debug** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/debug>`

Đường dẫn đến tệp debug keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_DEBUG_PATH``.

Nếu để trống, sẽ fallback về ``EditorSettings.export/android/debug_keystore``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/debug_password:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/debug_password** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/debug_password>`

Mật khẩu của tệp debug keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_DEBUG_PASSWORD``.

Fallbacks to ``EditorSettings.export/android/debug_keystore_pass`` if both it and :ref:`keystore/debug<class_EditorExportPlatformAndroid_property_keystore/debug>` are empty.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/debug_user:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/debug_user** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/debug_user>`

Tên người dùng của tệp debug keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_DEBUG_USER``.

Fallbacks to ``EditorSettings.export/android/debug_keystore_user`` if both it and :ref:`keystore/debug<class_EditorExportPlatformAndroid_property_keystore/debug>` are empty.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/release** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/release>`

Đường dẫn đến tệp release keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_RELEASE_PATH``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/release_password:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/release_password** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/release_password>`

Mật khẩu của tệp release keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_RELEASE_PASSWORD``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_keystore/release_user:

.. rst-class:: classref-property

:ref:`String<class_String>` **keystore/release_user** :ref:`🔗<class_EditorExportPlatformAndroid_property_keystore/release_user>`

Tên người dùng của tệp release keystore.

Có thể ghi đè bằng environment variable ``GODOT_ANDROID_KEYSTORE_RELEASE_USER``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_background_432x432:

.. rst-class:: classref-property

:ref:`String<class_String>` **launcher_icons/adaptive_background_432x432** :ref:`🔗<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_background_432x432>`

Lớp nền của tệp adaptive icon của ứng dụng. Xem `Design adaptive icons <https://developer.android.com/develop/ui/views/launch/icon_design_adaptive#design-adaptive-icons>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_foreground_432x432:

.. rst-class:: classref-property

:ref:`String<class_String>` **launcher_icons/adaptive_foreground_432x432** :ref:`🔗<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_foreground_432x432>`

Lớp tiền cảnh của tệp adaptive icon của ứng dụng. Xem `Design adaptive icons <https://developer.android.com/develop/ui/views/launch/icon_design_adaptive#design-adaptive-icons>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_monochrome_432x432:

.. rst-class:: classref-property

:ref:`String<class_String>` **launcher_icons/adaptive_monochrome_432x432** :ref:`🔗<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_monochrome_432x432>`

Lớp đơn sắc của tệp adaptive icon của ứng dụng. Xem `Design adaptive icons <https://developer.android.com/develop/ui/views/launch/icon_design_adaptive#design-adaptive-icons>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_launcher_icons/main_192x192:

.. rst-class:: classref-property

:ref:`String<class_String>` **launcher_icons/main_192x192** :ref:`🔗<class_EditorExportPlatformAndroid_property_launcher_icons/main_192x192>`

Tệp icon của ứng dụng. Nếu để trống, sẽ fallback về :ref:`ProjectSettings.application/config/icon<class_ProjectSettings_property_application/config/icon>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/app_category:

.. rst-class:: classref-property

:ref:`int<class_int>` **package/app_category** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/app_category>`

Danh mục ứng dụng trên Google Play Store. Chỉ xác định tùy chọn này nếu ứng dụng của bạn thực sự phù hợp với một trong các danh mục. Xem `android:appCategory <https://developer.android.com/guide/topics/manifest/application-element#appCategory>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/exclude_from_recents:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/exclude_from_recents** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/exclude_from_recents>`

Nếu ``true``, task do main activity khởi tạo sẽ bị loại khỏi danh sách các ứng dụng được sử dụng gần đây. Xem `android:excludeFromRecents <https://developer.android.com/guide/topics/manifest/activity-element#exclude>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/name:

.. rst-class:: classref-property

:ref:`String<class_String>` **package/name** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/name>`

Tên của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/retain_data_on_uninstall:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/retain_data_on_uninstall** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/retain_data_on_uninstall>`

Nếu ``true``, khi người dùng gỡ cài đặt ứng dụng, một lời nhắc giữ lại dữ liệu của ứng dụng sẽ hiển thị. Xem `android:hasFragileUserData <https://developer.android.com/guide/topics/manifest/application-element#fragileuserdata>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/show_as_launcher_app:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/show_as_launcher_app** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/show_as_launcher_app>`

Nếu ``true``, người dùng sẽ có thể đặt ứng dụng này làm system launcher trong phần tùy chọn Android.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/show_in_android_tv:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/show_in_android_tv** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/show_in_android_tv>`

Nếu ``true``, ứng dụng này sẽ hiển thị trong launcher UI của Android TV.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/show_in_app_library:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/show_in_app_library** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/show_in_app_library>`

Nếu ``true``, ứng dụng này sẽ hiển thị trong thư viện ứng dụng của thiết bị.

\ **Lưu ý:** Theo mặc định, đây là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/signed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **package/signed** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/signed>`

Nếu ``true``, việc ký package được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_package/unique_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **package/unique_name** :ref:`🔗<class_EditorExportPlatformAndroid_property_package/unique_name>`

Mã nhận dạng ứng dụng duy nhất ở định dạng reverse-DNS. Định dạng reverse DNS tốt nhất nên khớp với một tên miền mà bạn kiểm soát, nhưng đây không phải là yêu cầu bắt buộc. Ví dụ: nếu bạn sở hữu ``example.com``, tên duy nhất của package tốt nhất nên có dạng ``com.example.mygame``. Mã nhận dạng này chỉ có thể chứa các ký tự chữ và số viết thường (``a-z`` và ``0-9``), dấu gạch dưới (``_``) và dấu chấm (``.``). Mỗi thành phần của định dạng reverse DNS phải bắt đầu bằng một chữ cái: chẳng hạn, ``com.example.8game`` không hợp lệ.

Nếu ``$genname`` xuất hiện trong giá trị, nó sẽ được thay thế bằng tên project được chuyển thành chữ thường. Nếu tên project có các ký tự không hợp lệ, chúng sẽ bị loại bỏ. Nếu tất cả ký tự trong tên project bị loại bỏ, ``$genname`` sẽ được thay thế bằng ``noname``.

\ **Lưu ý:** Việc thay đổi tên package sẽ khiến package được xem là một package mới, với các đường dẫn cài đặt và dữ liệu riêng. Package mới sẽ không thể được dùng để cập nhật các bản cài đặt hiện có.

\ **Lưu ý:** Khi phát hành lên Google Play, tên package phải là *duy nhất trên toàn cầu*. Điều này có nghĩa là không ứng dụng nào khác được phát hành trên Google Play được sử dụng cùng tên package với ứng dụng của bạn. Nếu không, bạn sẽ không thể phát hành ứng dụng của mình trên Google Play.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_checkin_properties:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_checkin_properties** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_checkin_properties>`

Cho phép truy cập đọc/ghi vào bảng "properties" trong cơ sở dữ liệu checkin. Xem `ACCESS_CHECKIN_PROPERTIES <https://developer.android.com/reference/android/Manifest.permission#ACCESS_CHECKIN_PROPERTIES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_coarse_location:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_coarse_location** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_coarse_location>`

Cho phép truy cập thông tin vị trí gần đúng. Xem `ACCESS_COARSE_LOCATION <https://developer.android.com/reference/android/Manifest.permission#ACCESS_COARSE_LOCATION>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_fine_location:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_fine_location** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_fine_location>`

Cho phép truy cập thông tin vị trí chính xác. Xem `ACCESS_FINE_LOCATION <https://developer.android.com/reference/android/Manifest.permission#ACCESS_FINE_LOCATION>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_location_extra_commands:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_location_extra_commands** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_location_extra_commands>`

Cho phép truy cập các lệnh bổ sung của location provider. Xem `ACCESS_LOCATION_EXTRA_COMMANDS <https://developer.android.com/reference/android/Manifest.permission#ACCESS_LOCATION_EXTRA_COMMANDS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_media_location:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_media_location** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_media_location>`

Cho phép ứng dụng truy cập mọi vị trí địa lý được lưu trong bộ sưu tập dùng chung của người dùng. Xem `ACCESS_MEDIA_LOCATION <https://developer.android.com/reference/android/Manifest.permission#ACCESS_MEDIA_LOCATION>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_mock_location:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_mock_location** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_mock_location>`

Cho phép ứng dụng tạo các location provider giả để kiểm thử.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_network_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_network_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_network_state>`

Cho phép truy cập thông tin về các mạng. Xem `ACCESS_NETWORK_STATE <https://developer.android.com/reference/android/Manifest.permission#ACCESS_NETWORK_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_surface_flinger:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_surface_flinger** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_surface_flinger>`

Cho phép ứng dụng sử dụng các tính năng cấp thấp của SurfaceFlinger.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/access_wifi_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/access_wifi_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/access_wifi_state>`

Cho phép truy cập thông tin về các mạng Wi-Fi. Xem `ACCESS_WIFI_STATE <https://developer.android.com/reference/android/Manifest.permission#ACCESS_WIFI_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/account_manager:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/account_manager** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/account_manager>`

Cho phép ứng dụng gọi vào AccountAuthenticators. Xem `ACCOUNT_MANAGER <https://developer.android.com/reference/android/Manifest.permission#ACCOUNT_MANAGER>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/add_voicemail:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/add_voicemail** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/add_voicemail>`

Cho phép ứng dụng thêm voicemail vào hệ thống. Xem `ADD_VOICEMAIL <https://developer.android.com/reference/android/Manifest.permission#ADD_VOICEMAIL>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/authenticate_accounts:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/authenticate_accounts** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/authenticate_accounts>`

Cho phép ứng dụng hoạt động như một AccountAuthenticator cho AccountManager.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/battery_stats:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/battery_stats** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/battery_stats>`

Cho phép ứng dụng thu thập thống kê pin. Xem `BATTERY_STATS <https://developer.android.com/reference/android/Manifest.permission#BATTERY_STATS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_accessibility_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_accessibility_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_accessibility_service>`

AccessibilityService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_ACCESSIBILITY_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_ACCESSIBILITY_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_appwidget:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_appwidget** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_appwidget>`

Cho phép ứng dụng thông báo cho AppWidget service biết ứng dụng nào có thể truy cập dữ liệu của AppWidget. Xem `BIND_APPWIDGET <https://developer.android.com/reference/android/Manifest.permission#BIND_APPWIDGET>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_device_admin:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_device_admin** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_device_admin>`

Device administration receiver phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể tương tác với nó. Xem `BIND_DEVICE_ADMIN <https://developer.android.com/reference/android/Manifest.permission#BIND_DEVICE_ADMIN>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_input_method:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_input_method** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_input_method>`

InputMethodService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_INPUT_METHOD <https://developer.android.com/reference/android/Manifest.permission#BIND_INPUT_METHOD>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_nfc_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_nfc_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_nfc_service>`

HostApduService hoặc OffHostApduService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_NFC_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_NFC_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_notification_listener_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_notification_listener_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_notification_listener_service>`

NotificationListenerService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_NOTIFICATION_LISTENER_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_NOTIFICATION_LISTENER_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_print_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_print_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_print_service>`

PrintService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_PRINT_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_PRINT_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_remoteviews:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_remoteviews** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_remoteviews>`

RemoteViewsService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_REMOTEVIEWS <https://developer.android.com/reference/android/Manifest.permission#BIND_REMOTEVIEWS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_text_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_text_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_text_service>`

TextService (ví dụ: SpellCheckerService) phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_TEXT_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_TEXT_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_vpn_service:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_vpn_service** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_vpn_service>`

VpnService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_VPN_SERVICE <https://developer.android.com/reference/android/Manifest.permission#BIND_VPN_SERVICE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bind_wallpaper:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bind_wallpaper** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bind_wallpaper>`

WallpaperService phải yêu cầu quyền này để đảm bảo chỉ hệ thống mới có thể bind vào đó. Xem `BIND_WALLPAPER <https://developer.android.com/reference/android/Manifest.permission#BIND_WALLPAPER>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bluetooth:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bluetooth** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bluetooth>`

Cho phép ứng dụng kết nối với các thiết bị bluetooth đã ghép đôi. Xem `BLUETOOTH <https://developer.android.com/reference/android/Manifest.permission#BLUETOOTH>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bluetooth_admin:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bluetooth_admin** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bluetooth_admin>`

Cho phép ứng dụng phát hiện và ghép đôi các thiết bị bluetooth. Xem `BLUETOOTH_ADMIN <https://developer.android.com/reference/android/Manifest.permission#BLUETOOTH_ADMIN>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/bluetooth_privileged:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/bluetooth_privileged** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/bluetooth_privileged>`

Cho phép ứng dụng ghép đôi các thiết bị bluetooth mà không cần sự tương tác của người dùng, đồng thời cho phép hoặc không cho phép truy cập danh bạ hay tin nhắn. Xem `BLUETOOTH_PRIVILEGED <https://developer.android.com/reference/android/Manifest.permission#BLUETOOTH_PRIVILEGED>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/brick:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/brick** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/brick>`

Bắt buộc phải có để có thể vô hiệu hóa thiết bị (cực kỳ nguy hiểm!).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/broadcast_package_removed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/broadcast_package_removed** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/broadcast_package_removed>`

Cho phép ứng dụng broadcast một thông báo cho biết một application package đã bị xóa. Xem `BROADCAST_PACKAGE_REMOVED <https://developer.android.com/reference/android/Manifest.permission#BROADCAST_PACKAGE_REMOVED>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/broadcast_sms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/broadcast_sms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/broadcast_sms>`

Cho phép ứng dụng broadcast thông báo nhận SMS. Xem `BROADCAST_SMS <https://developer.android.com/reference/android/Manifest.permission#BROADCAST_SMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/broadcast_sticky:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/broadcast_sticky** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/broadcast_sticky>`

Cho phép ứng dụng broadcast các sticky intent. Xem `BROADCAST_STICKY <https://developer.android.com/reference/android/Manifest.permission#BROADCAST_STICKY>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/broadcast_wap_push:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/broadcast_wap_push** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/broadcast_wap_push>`

Cho phép ứng dụng broadcast thông báo nhận WAP PUSH. Xem `BROADCAST_WAP_PUSH <https://developer.android.com/reference/android/Manifest.permission#BROADCAST_WAP_PUSH>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/call_phone:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/call_phone** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/call_phone>`

Cho phép ứng dụng bắt đầu cuộc gọi mà không cần đi qua giao diện người dùng Dialer. Xem `CALL_PHONE <https://developer.android.com/reference/android/Manifest.permission#CALL_PHONE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/call_privileged:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/call_privileged** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/call_privileged>`

Cho phép ứng dụng gọi đến bất kỳ số điện thoại nào, bao gồm cả số khẩn cấp, mà không cần đi qua giao diện người dùng Dialer. Xem `CALL_PRIVILEGED <https://developer.android.com/reference/android/Manifest.permission#CALL_PRIVILEGED>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/camera:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/camera** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/camera>`

Bắt buộc phải có để có thể truy cập thiết bị camera. Xem `CAMERA <https://developer.android.com/reference/android/Manifest.permission#CAMERA>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/capture_audio_output:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/capture_audio_output** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/capture_audio_output>`

Cho phép ứng dụng capture đầu ra âm thanh. Xem `CAPTURE_AUDIO_OUTPUT <https://developer.android.com/reference/android/Manifest.permission#CAPTURE_AUDIO_OUTPUT>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/capture_secure_video_output:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/capture_secure_video_output** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/capture_secure_video_output>`

Cho phép ứng dụng capture đầu ra video bảo mật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/capture_video_output:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/capture_video_output** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/capture_video_output>`

Cho phép ứng dụng capture đầu ra video.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/change_component_enabled_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/change_component_enabled_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/change_component_enabled_state>`

Cho phép ứng dụng thay đổi trạng thái bật hoặc tắt của một application component (ngoài component của chính ứng dụng đó). Xem `CHANGE_COMPONENT_ENABLED_STATE <https://developer.android.com/reference/android/Manifest.permission#CHANGE_COMPONENT_ENABLED_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/change_configuration:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/change_configuration** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/change_configuration>`

Cho phép ứng dụng sửa đổi configuration hiện tại, chẳng hạn như locale. Xem `CHANGE_CONFIGURATION <https://developer.android.com/reference/android/Manifest.permission#CHANGE_CONFIGURATION>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/change_network_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/change_network_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/change_network_state>`

Cho phép ứng dụng thay đổi trạng thái kết nối mạng. Xem `CHANGE_NETWORK_STATE <https://developer.android.com/reference/android/Manifest.permission#CHANGE_NETWORK_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/change_wifi_multicast_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/change_wifi_multicast_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/change_wifi_multicast_state>`

Cho phép ứng dụng chuyển sang chế độ Wi-Fi Multicast. Xem `CHANGE_WIFI_MULTICAST_STATE <https://developer.android.com/reference/android/Manifest.permission#CHANGE_WIFI_MULTICAST_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/change_wifi_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/change_wifi_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/change_wifi_state>`

Cho phép ứng dụng thay đổi trạng thái kết nối Wi-Fi. Xem `CHANGE_WIFI_STATE <https://developer.android.com/reference/android/Manifest.permission#CHANGE_WIFI_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/clear_app_cache:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/clear_app_cache** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/clear_app_cache>`

Cho phép ứng dụng xóa cache của tất cả ứng dụng đã cài đặt trên thiết bị. Xem `CLEAR_APP_CACHE <https://developer.android.com/reference/android/Manifest.permission#CLEAR_APP_CACHE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/clear_app_user_data:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/clear_app_user_data** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/clear_app_user_data>`

Cho phép ứng dụng xóa dữ liệu người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/control_location_updates:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/control_location_updates** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/control_location_updates>`

Cho phép bật/tắt thông báo cập nhật vị trí từ radio. Xem `CONTROL_LOCATION_UPDATES <https://developer.android.com/reference/android/Manifest.permission#CONTROL_LOCATION_UPDATES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/custom_permissions:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **permissions/custom_permissions** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/custom_permissions>`

Mảng các chuỗi permission tùy chỉnh.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị property ban đầu. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/delete_cache_files:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/delete_cache_files** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/delete_cache_files>`

**Đã lỗi thời:** Property này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/delete_packages:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/delete_packages** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/delete_packages>`

Cho phép ứng dụng xóa các package. Xem `DELETE_PACKAGES <https://developer.android.com/reference/android/Manifest.permission#DELETE_PACKAGES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/device_power:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/device_power** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/device_power>`

Cho phép truy cập cấp thấp vào việc quản lý nguồn.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/diagnostic:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/diagnostic** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/diagnostic>`

Cho phép ứng dụng đọc/ghi (RW) vào các tài nguyên chẩn đoán. Xem `DIAGNOSTIC <https://developer.android.com/reference/android/Manifest.permission#DIAGNOSTIC>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/disable_keyguard:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/disable_keyguard** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/disable_keyguard>`

Cho phép ứng dụng tắt keyguard nếu keyguard không được bảo mật. Xem `DISABLE_KEYGUARD <https://developer.android.com/reference/android/Manifest.permission#DISABLE_KEYGUARD>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/dump:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/dump** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/dump>`

Cho phép ứng dụng lấy thông tin state dump từ các system service. Xem `DUMP <https://developer.android.com/reference/android/Manifest.permission#DUMP>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/expand_status_bar:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/expand_status_bar** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/expand_status_bar>`

Cho phép ứng dụng mở rộng hoặc thu gọn status bar. Xem `EXPAND_STATUS_BAR <https://developer.android.com/reference/android/Manifest.permission#EXPAND_STATUS_BAR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/factory_test:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/factory_test** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/factory_test>`

Chạy dưới dạng ứng dụng kiểm thử của nhà sản xuất, với tư cách người dùng root. Xem `FACTORY_TEST <https://developer.android.com/reference/android/Manifest.permission#FACTORY_TEST>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/flashlight:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/flashlight** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/flashlight>`

Cho phép truy cập đèn pin.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/force_back:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/force_back** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/force_back>`

Cho phép ứng dụng buộc thực hiện thao tác BACK trên activity đang ở trên cùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/get_accounts:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/get_accounts** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/get_accounts>`

Cho phép truy cập danh sách tài khoản trong Accounts Service. Xem `GET_ACCOUNTS <https://developer.android.com/reference/android/Manifest.permission#GET_ACCOUNTS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/get_package_size:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/get_package_size** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/get_package_size>`

Cho phép ứng dụng tìm ra dung lượng mà bất kỳ package nào đang sử dụng. Xem `GET_PACKAGE_SIZE <https://developer.android.com/reference/android/Manifest.permission#GET_PACKAGE_SIZE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/get_tasks:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/get_tasks** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/get_tasks>`

**Đã lỗi thời:** Đã lỗi thời ở API level 21.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/get_top_activity_info:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/get_top_activity_info** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/get_top_activity_info>`

Cho phép ứng dụng lấy thông tin riêng tư về activity đang ở trên cùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/global_search:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/global_search** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/global_search>`

Được sử dụng trên content provider để cho phép hệ thống tìm kiếm toàn cục truy cập dữ liệu của chúng. Xem `GLOBAL_SEARCH <https://developer.android.com/reference/android/Manifest.permission#GLOBAL_SEARCH>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/hardware_test:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/hardware_test** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/hardware_test>`

Cho phép truy cập các thiết bị ngoại vi phần cứng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/inject_events:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/inject_events** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/inject_events>`

Cho phép ứng dụng inject các sự kiện người dùng (phím, cảm ứng, trackball) vào event stream và chuyển chúng đến BẤT KỲ cửa sổ nào.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/install_location_provider:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/install_location_provider** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/install_location_provider>`

Cho phép ứng dụng cài đặt location provider vào Location Manager. Xem `INSTALL_LOCATION_PROVIDER <https://developer.android.com/reference/android/Manifest.permission#INSTALL_LOCATION_PROVIDER>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/install_packages:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/install_packages** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/install_packages>`

Cho phép ứng dụng cài đặt các package. Xem `INSTALL_PACKAGES <https://developer.android.com/reference/android/Manifest.permission#INSTALL_PACKAGES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/install_shortcut:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/install_shortcut** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/install_shortcut>`

Cho phép ứng dụng cài đặt shortcut trong Launcher. Xem `INSTALL_SHORTCUT <https://developer.android.com/reference/android/Manifest.permission#INSTALL_SHORTCUT>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/internal_system_window:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/internal_system_window** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/internal_system_window>`

Cho phép ứng dụng mở các cửa sổ được sử dụng bởi các thành phần của giao diện người dùng hệ thống.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/internet:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/internet** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/internet>`

Cho phép ứng dụng mở network socket. Xem `INTERNET <https://developer.android.com/reference/android/Manifest.permission#INTERNET>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/kill_background_processes:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/kill_background_processes** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/kill_background_processes>`

Cho phép ứng dụng gọi ActivityManager.killBackgroundProcesses(String). Xem `KILL_BACKGROUND_PROCESSES <https://developer.android.com/reference/android/Manifest.permission#KILL_BACKGROUND_PROCESSES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/location_hardware:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/location_hardware** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/location_hardware>`

Cho phép ứng dụng sử dụng các tính năng vị trí trong phần cứng, chẳng hạn như geofencing api. Xem `LOCATION_HARDWARE <https://developer.android.com/reference/android/Manifest.permission#LOCATION_HARDWARE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/manage_accounts:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/manage_accounts** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/manage_accounts>`

Cho phép ứng dụng quản lý danh sách tài khoản trong AccountManager.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/manage_app_tokens:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/manage_app_tokens** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/manage_app_tokens>`

Cho phép ứng dụng quản lý (tạo, hủy, Z-order) các application token trong window manager.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/manage_documents:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/manage_documents** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/manage_documents>`

Cho phép ứng dụng quản lý quyền truy cập vào tài liệu, thường là một phần của document picker. Xem `MANAGE_DOCUMENTS <https://developer.android.com/reference/android/Manifest.permission#MANAGE_DOCUMENTS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/manage_external_storage:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/manage_external_storage** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/manage_external_storage>`

Cho phép ứng dụng có quyền truy cập rộng vào external storage trong scoped storage. Xem `MANAGE_EXTERNAL_STORAGE <https://developer.android.com/reference/android/Manifest.permission#MANAGE_EXTERNAL_STORAGE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/manage_media:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/manage_media** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/manage_media>`

Cho phép ứng dụng sửa đổi và xóa các tệp media trên thiết bị này hoặc bất kỳ thiết bị lưu trữ nào được kết nối mà không cần người dùng xác nhận. Ứng dụng trước tiên phải được cấp permission ``READ_EXTERNAL_STORAGE`` hoặc ``MANAGE_EXTERNAL_STORAGE`` thì permission này mới có hiệu lực. Xem `MANAGE_MEDIA <https://developer.android.com/reference/android/Manifest.permission#MANAGE_MEDIA>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/master_clear:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/master_clear** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/master_clear>`

Xem `MASTER_CLEAR <https://developer.android.com/reference/android/Manifest.permission#MASTER_CLEAR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/media_content_control:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/media_content_control** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/media_content_control>`

Cho phép ứng dụng biết nội dung nào đang phát và điều khiển việc phát nội dung đó. Xem `MEDIA_CONTENT_CONTROL <https://developer.android.com/reference/android/Manifest.permission#MEDIA_CONTENT_CONTROL>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/modify_audio_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/modify_audio_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/modify_audio_settings>`

Cho phép ứng dụng sửa đổi các cài đặt âm thanh toàn cục. Xem `MODIFY_AUDIO_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#MODIFY_AUDIO_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/modify_phone_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/modify_phone_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/modify_phone_state>`

Cho phép sửa đổi trạng thái telephony - bật nguồn, mmi, v.v. Không bao gồm việc thực hiện cuộc gọi. Xem `MODIFY_PHONE_STATE <https://developer.android.com/reference/android/Manifest.permission#MODIFY_PHONE_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/mount_format_filesystems:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/mount_format_filesystems** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/mount_format_filesystems>`

Cho phép định dạng các hệ thống tệp cho bộ nhớ di động. Xem `MOUNT_FORMAT_FILESYSTEMS <https://developer.android.com/reference/android/Manifest.permission#MOUNT_FORMAT_FILESYSTEMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/mount_unmount_filesystems:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/mount_unmount_filesystems** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/mount_unmount_filesystems>`

Cho phép mount và unmount các hệ thống tệp cho bộ nhớ di động. Xem `MOUNT_UNMOUNT_FILESYSTEMS <https://developer.android.com/reference/android/Manifest.permission#MOUNT_UNMOUNT_FILESYSTEMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/nfc:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/nfc** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/nfc>`

Cho phép ứng dụng thực hiện các thao tác I/O qua NFC. Xem `NFC <https://developer.android.com/reference/android/Manifest.permission#NFC>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/persistent_activity:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/persistent_activity** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/persistent_activity>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 15.

Cho phép ứng dụng duy trì các activity của mình.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/post_notifications:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/post_notifications** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/post_notifications>`

Cho phép ứng dụng đăng thông báo. Được thêm từ API level 33. Xem `Notification runtime permission <https://developer.android.com/develop/ui/views/notifications/notification-permission>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/process_outgoing_calls:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/process_outgoing_calls** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/process_outgoing_calls>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 29.

Cho phép ứng dụng xem số điện thoại đang được gọi trong một cuộc gọi đi, với tùy chọn chuyển hướng cuộc gọi đến một số khác hoặc hủy hoàn toàn cuộc gọi. Xem `PROCESS_OUTGOING_CALLS <https://developer.android.com/reference/android/Manifest.permission#PROCESS_OUTGOING_CALLS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_calendar:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_calendar** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_calendar>`

Cho phép ứng dụng đọc dữ liệu lịch của người dùng. Xem `READ_CALENDAR <https://developer.android.com/reference/android/Manifest.permission#READ_CALENDAR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_call_log:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_call_log** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_call_log>`

Cho phép ứng dụng đọc nhật ký cuộc gọi của người dùng. Xem `READ_CALL_LOG <https://developer.android.com/reference/android/Manifest.permission#READ_CALL_LOG>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_contacts:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_contacts** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_contacts>`

Cho phép ứng dụng đọc dữ liệu danh bạ của người dùng. Xem `READ_CONTACTS <https://developer.android.com/reference/android/Manifest.permission#READ_CONTACTS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_external_storage:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_external_storage** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_external_storage>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 33.

Cho phép ứng dụng đọc dữ liệu từ bộ nhớ ngoài. Xem `READ_EXTERNAL_STORAGE <https://developer.android.com/reference/android/Manifest.permission#READ_EXTERNAL_STORAGE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_frame_buffer:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_frame_buffer** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_frame_buffer>`

Cho phép ứng dụng chụp ảnh màn hình và nói chung là truy cập dữ liệu frame buffer.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_history_bookmarks:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_history_bookmarks** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_history_bookmarks>`

Cho phép ứng dụng đọc (nhưng không ghi) lịch sử duyệt web và dấu trang của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_input_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_input_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_input_state>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 16.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_logs:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_logs** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_logs>`

Cho phép ứng dụng đọc các tệp nhật ký hệ thống cấp thấp. Xem `READ_LOGS <https://developer.android.com/reference/android/Manifest.permission#READ_LOGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_media_audio:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_media_audio** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_media_audio>`

Cho phép ứng dụng đọc các tệp âm thanh từ bộ nhớ ngoài. Xem `READ_MEDIA_AUDIO <https://developer.android.com/reference/android/Manifest.permission#READ_MEDIA_AUDIO>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_media_images:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_media_images** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_media_images>`

Cho phép ứng dụng đọc các tệp hình ảnh từ bộ nhớ ngoài. Xem `READ_MEDIA_IMAGES <https://developer.android.com/reference/android/Manifest.permission#READ_MEDIA_IMAGES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_media_video:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_media_video** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_media_video>`

Cho phép ứng dụng đọc các tệp video từ bộ nhớ ngoài. Xem `READ_MEDIA_VIDEO <https://developer.android.com/reference/android/Manifest.permission#READ_MEDIA_VIDEO>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_media_visual_user_selected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_media_visual_user_selected** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_media_visual_user_selected>`

Cho phép ứng dụng đọc các tệp hình ảnh hoặc video từ bộ nhớ ngoài mà người dùng đã chọn thông qua photo picker trong lời nhắc cấp quyền. Xem `READ_MEDIA_VISUAL_USER_SELECTED <https://developer.android.com/reference/android/Manifest.permission#READ_MEDIA_VISUAL_USER_SELECTED>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_phone_state:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_phone_state** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_phone_state>`

Cho phép chỉ đọc trạng thái điện thoại. Xem `READ_PHONE_STATE <https://developer.android.com/reference/android/Manifest.permission#READ_PHONE_STATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_profile:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_profile** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_profile>`

Cho phép ứng dụng đọc dữ liệu hồ sơ cá nhân của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_sms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_sms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_sms>`

Cho phép ứng dụng đọc tin nhắn SMS. Xem `READ_SMS <https://developer.android.com/reference/android/Manifest.permission#READ_SMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_social_stream:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_social_stream** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_social_stream>`

Cho phép ứng dụng đọc luồng mạng xã hội của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_sync_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_sync_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_sync_settings>`

Cho phép ứng dụng đọc các cài đặt đồng bộ hóa. Xem `READ_SYNC_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#READ_SYNC_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_sync_stats:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_sync_stats** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_sync_stats>`

Cho phép ứng dụng đọc số liệu thống kê đồng bộ hóa. Xem `READ_SYNC_STATS <https://developer.android.com/reference/android/Manifest.permission#READ_SYNC_STATS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/read_user_dictionary:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/read_user_dictionary** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/read_user_dictionary>`

Cho phép ứng dụng đọc từ điển người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/reboot:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/reboot** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/reboot>`

Bắt buộc phải có để có thể khởi động lại thiết bị. Xem `REBOOT <https://developer.android.com/reference/android/Manifest.permission#REBOOT>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/receive_boot_completed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/receive_boot_completed** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/receive_boot_completed>`

Cho phép ứng dụng nhận Intent.ACTION_BOOT_COMPLETED được broadcast sau khi hệ thống hoàn tất quá trình khởi động. Xem `RECEIVE_BOOT_COMPLETED <https://developer.android.com/reference/android/Manifest.permission#RECEIVE_BOOT_COMPLETED>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/receive_mms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/receive_mms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/receive_mms>`

Cho phép ứng dụng giám sát tin nhắn MMS đến. Xem `RECEIVE_MMS <https://developer.android.com/reference/android/Manifest.permission#RECEIVE_MMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/receive_sms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/receive_sms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/receive_sms>`

Cho phép ứng dụng nhận tin nhắn SMS. Xem `RECEIVE_SMS <https://developer.android.com/reference/android/Manifest.permission#RECEIVE_SMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/receive_wap_push:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/receive_wap_push** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/receive_wap_push>`

Cho phép ứng dụng nhận tin nhắn WAP push. Xem `RECEIVE_WAP_PUSH <https://developer.android.com/reference/android/Manifest.permission#RECEIVE_WAP_PUSH>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/record_audio:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/record_audio** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/record_audio>`

Cho phép ứng dụng ghi âm thanh. Xem `RECORD_AUDIO <https://developer.android.com/reference/android/Manifest.permission#RECORD_AUDIO>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/reorder_tasks:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/reorder_tasks** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/reorder_tasks>`

Cho phép ứng dụng thay đổi thứ tự Z của các task. Xem `REORDER_TASKS <https://developer.android.com/reference/android/Manifest.permission#REORDER_TASKS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/restart_packages:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/restart_packages** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/restart_packages>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 15.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/send_respond_via_message:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/send_respond_via_message** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/send_respond_via_message>`

Cho phép một ứng dụng (Phone) gửi yêu cầu đến các ứng dụng khác để xử lý hành động respond-via-message trong các cuộc gọi đến. Xem `SEND_RESPOND_VIA_MESSAGE <https://developer.android.com/reference/android/Manifest.permission#SEND_RESPOND_VIA_MESSAGE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/send_sms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/send_sms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/send_sms>`

Cho phép ứng dụng gửi tin nhắn SMS. Xem `SEND_SMS <https://developer.android.com/reference/android/Manifest.permission#SEND_SMS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_activity_watcher:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_activity_watcher** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_activity_watcher>`

Cho phép ứng dụng theo dõi và kiểm soát cách các activity được khởi chạy trên toàn hệ thống.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_alarm:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_alarm** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_alarm>`

Cho phép ứng dụng broadcast một Intent để đặt báo thức cho người dùng. Xem `SET_ALARM <https://developer.android.com/reference/android/Manifest.permission#SET_ALARM>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_always_finish:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_always_finish** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_always_finish>`

Cho phép ứng dụng kiểm soát việc các activity có được kết thúc ngay lập tức khi chuyển xuống nền hay không. Xem `SET_ALWAYS_FINISH <https://developer.android.com/reference/android/Manifest.permission#SET_ALWAYS_FINISH>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_animation_scale:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_animation_scale** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_animation_scale>`

Cho phép sửa đổi hệ số tỷ lệ animation toàn cục. Xem `SET_ANIMATION_SCALE <https://developer.android.com/reference/android/Manifest.permission#SET_ANIMATION_SCALE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_debug_app:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_debug_app** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_debug_app>`

Cấu hình một ứng dụng để debug. Xem `SET_DEBUG_APP <https://developer.android.com/reference/android/Manifest.permission#SET_DEBUG_APP>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_orientation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_orientation** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_orientation>`

Cho phép truy cập cấp thấp để thiết lập hướng (thực tế là xoay) của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_pointer_speed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_pointer_speed** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_pointer_speed>`

Cho phép truy cập cấp thấp để thiết lập tốc độ con trỏ.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_preferred_applications:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_preferred_applications** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_preferred_applications>`

**Đã ngừng sử dụng:** Đã ngừng sử dụng từ API level 15.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_process_limit:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_process_limit** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_process_limit>`

Cho phép ứng dụng đặt số lượng tối đa các tiến trình ứng dụng (không cần thiết) có thể đang chạy. Xem `SET_PROCESS_LIMIT <https://developer.android.com/reference/android/Manifest.permission#SET_PROCESS_LIMIT>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_time:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_time** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_time>`

Cho phép ứng dụng đặt trực tiếp thời gian hệ thống. Xem `SET_TIME <https://developer.android.com/reference/android/Manifest.permission#SET_TIME>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_time_zone:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_time_zone** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_time_zone>`

Cho phép các ứng dụng trực tiếp đặt múi giờ hệ thống. Xem `SET_TIME_ZONE <https://developer.android.com/reference/android/Manifest.permission#SET_TIME_ZONE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_wallpaper:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_wallpaper** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_wallpaper>`

Cho phép các ứng dụng đặt hình nền. Xem `SET_WALLPAPER <https://developer.android.com/reference/android/Manifest.permission#SET_WALLPAPER>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/set_wallpaper_hints:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/set_wallpaper_hints** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/set_wallpaper_hints>`

Cho phép các ứng dụng đặt gợi ý hình nền. Xem `SET_WALLPAPER_HINTS <https://developer.android.com/reference/android/Manifest.permission#SET_WALLPAPER_HINTS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/signal_persistent_processes:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/signal_persistent_processes** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/signal_persistent_processes>`

Cho phép một ứng dụng yêu cầu gửi một signal đến tất cả các process liên tục. Xem `SIGNAL_PERSISTENT_PROCESSES <https://developer.android.com/reference/android/Manifest.permission#SIGNAL_PERSISTENT_PROCESSES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/status_bar:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/status_bar** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/status_bar>`

Cho phép một ứng dụng mở, đóng hoặc vô hiệu hóa status bar và các biểu tượng của thanh này. Xem `STATUS_BAR <https://developer.android.com/reference/android/Manifest.permission#STATUS_BAR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_read:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/subscribed_feeds_read** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_read>`

Cho phép một ứng dụng cho phép truy cập vào ContentProvider của các feed đã đăng ký.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_write:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/subscribed_feeds_write** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/subscribed_feeds_write>`

**Đã ngừng sử dụng:** Thuộc tính này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/system_alert_window:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/system_alert_window** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/system_alert_window>`

Cho phép một app tạo các cửa sổ bằng kiểu WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY, hiển thị bên trên tất cả các app khác. Xem `SYSTEM_ALERT_WINDOW <https://developer.android.com/reference/android/Manifest.permission#SYSTEM_ALERT_WINDOW>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/transmit_ir:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/transmit_ir** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/transmit_ir>`

Cho phép sử dụng bộ phát IR của thiết bị, nếu có. Xem `TRANSMIT_IR <https://developer.android.com/reference/android/Manifest.permission#TRANSMIT_IR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/uninstall_shortcut:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/uninstall_shortcut** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/uninstall_shortcut>`

**Đã ngừng sử dụng:** Thuộc tính này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/update_device_stats:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/update_device_stats** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/update_device_stats>`

Cho phép một ứng dụng cập nhật số liệu thống kê của thiết bị. Xem `UPDATE_DEVICE_STATS <https://developer.android.com/reference/android/Manifest.permission#UPDATE_DEVICE_STATS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/use_credentials:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/use_credentials** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/use_credentials>`

Cho phép một ứng dụng yêu cầu authtoken từ AccountManager.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/use_sip:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/use_sip** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/use_sip>`

Cho phép một ứng dụng sử dụng dịch vụ SIP. Xem `USE_SIP <https://developer.android.com/reference/android/Manifest.permission#USE_SIP>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/vibrate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/vibrate** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/vibrate>`

Cho phép truy cập bộ rung. Xem `VIBRATE <https://developer.android.com/reference/android/Manifest.permission#VIBRATE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/wake_lock:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/wake_lock** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/wake_lock>`

Cho phép sử dụng PowerManager WakeLocks để ngăn processor chuyển sang trạng thái ngủ hoặc màn hình bị giảm độ sáng. Xem `WAKE_LOCK <https://developer.android.com/reference/android/Manifest.permission#WAKE_LOCK>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_apn_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_apn_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_apn_settings>`

Cho phép các ứng dụng ghi cài đặt apn và đọc các trường nhạy cảm của cài đặt apn hiện có, chẳng hạn như tên người dùng và mật khẩu. Xem `WRITE_APN_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#WRITE_APN_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_calendar:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_calendar** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_calendar>`

Cho phép một ứng dụng ghi dữ liệu lịch của người dùng. Xem `WRITE_CALENDAR <https://developer.android.com/reference/android/Manifest.permission#WRITE_CALENDAR>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_call_log:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_call_log** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_call_log>`

Cho phép một ứng dụng ghi (nhưng không đọc) dữ liệu nhật ký cuộc gọi của người dùng. Xem `WRITE_CALL_LOG <https://developer.android.com/reference/android/Manifest.permission#WRITE_CALL_LOG>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_contacts:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_contacts** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_contacts>`

Cho phép một ứng dụng ghi dữ liệu danh bạ của người dùng. Xem `WRITE_CONTACTS <https://developer.android.com/reference/android/Manifest.permission#WRITE_CONTACTS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_external_storage:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_external_storage** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_external_storage>`

Cho phép một ứng dụng ghi vào bộ nhớ ngoài. Xem `WRITE_EXTERNAL_STORAGE <https://developer.android.com/reference/android/Manifest.permission#WRITE_EXTERNAL_STORAGE>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_gservices:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_gservices** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_gservices>`

Cho phép một ứng dụng sửa đổi Google service map. Xem `WRITE_GSERVICES <https://developer.android.com/reference/android/Manifest.permission#WRITE_GSERVICES>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_history_bookmarks:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_history_bookmarks** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_history_bookmarks>`

Cho phép một ứng dụng ghi (nhưng không đọc) lịch sử duyệt web và dấu trang của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_profile:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_profile** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_profile>`

Cho phép một ứng dụng ghi (nhưng không đọc) dữ liệu hồ sơ cá nhân của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_secure_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_secure_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_secure_settings>`

Cho phép một ứng dụng đọc hoặc ghi các cài đặt hệ thống bảo mật. Xem `WRITE_SECURE_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#WRITE_SECURE_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_settings>`

Cho phép một ứng dụng đọc hoặc ghi các cài đặt hệ thống. Xem `WRITE_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#WRITE_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_sms:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_sms** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_sms>`

Cho phép một ứng dụng ghi tin nhắn SMS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_social_stream:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_social_stream** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_social_stream>`

Cho phép một ứng dụng ghi (nhưng không đọc) dữ liệu social stream của người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_sync_settings:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_sync_settings** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_sync_settings>`

Cho phép các ứng dụng ghi cài đặt đồng bộ hóa. Xem `WRITE_SYNC_SETTINGS <https://developer.android.com/reference/android/Manifest.permission#WRITE_SYNC_SETTINGS>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_permissions/write_user_dictionary:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **permissions/write_user_dictionary** :ref:`🔗<class_EditorExportPlatformAndroid_property_permissions/write_user_dictionary>`

Cho phép một ứng dụng ghi vào từ điển người dùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/background_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **screen/background_color** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/background_color>`

Màu nền được sử dụng cho cửa sổ root. Theo mặc định, giá trị này là :ref:`Color.BLACK<class_Color_constant_BLACK>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/edge_to_edge:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/edge_to_edge** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/edge_to_edge>`

Nếu ``true``, tùy chọn này làm cho navigation bar và status bar trong suốt, đồng thời cho phép nội dung ứng dụng mở rộng từ mép này đến mép kia.

\ **Lưu ý:** Bạn nên đảm bảo không có nội dung ứng dụng nào bị các thành phần hệ thống che khuất bằng cách sử dụng các phương thức :ref:`DisplayServer.get_display_safe_area()<class_DisplayServer_method_get_display_safe_area>` và :ref:`DisplayServer.get_display_cutouts()<class_DisplayServer_method_get_display_cutouts>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/immersive_mode:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/immersive_mode** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/immersive_mode>`

Nếu ``true``, navigation bar và status bar sẽ bị ẩn. Đặt :ref:`DisplayServer.window_set_mode()<class_DisplayServer_method_window_set_mode>` để thay đổi tùy chọn này trong runtime.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/support_large:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/support_large** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/support_large>`

Cho biết ứng dụng có hỗ trợ các form-factor màn hình lớn hơn hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/support_normal:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/support_normal** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/support_normal>`

Cho biết ứng dụng có hỗ trợ các form-factor màn hình "normal" hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/support_small:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/support_small** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/support_small>`

Cho biết ứng dụng có hỗ trợ các form-factor màn hình nhỏ hơn hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_screen/support_xlarge:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **screen/support_xlarge** :ref:`🔗<class_EditorExportPlatformAndroid_property_screen/support_xlarge>`

Cho biết ứng dụng có hỗ trợ các form-factor màn hình cực lớn hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_shader_baker/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shader_baker/enabled** :ref:`🔗<class_EditorExportPlatformAndroid_property_shader_baker/enabled>`

Nếu ``true``, các shader sẽ được biên dịch và nhúng vào ứng dụng. Tùy chọn này chỉ được hỗ trợ khi sử dụng renderer Forward+ hoặc Mobile.

\ **Lưu ý:** Khi export dưới dạng dedicated server, shader baker luôn bị vô hiệu hóa vì không thực hiện rendering.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_splash_screen/background_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **splash_screen/background_color** :ref:`🔗<class_EditorExportPlatformAndroid_property_splash_screen/background_color>`

Màu nền được sử dụng cho cửa sổ splash screen của hệ thống.

Nếu không được đặt, giá trị này sẽ quay về :ref:`launcher_icons/adaptive_background_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_background_432x432>`.

\ **Lưu ý:** Tùy chọn này chỉ được áp dụng nếu :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_splash_screen/branding_image:

.. rst-class:: classref-property

:ref:`String<class_String>` **splash_screen/branding_image** :ref:`🔗<class_EditorExportPlatformAndroid_property_splash_screen/branding_image>`

Tệp hình ảnh branding của splash screen hệ thống. Nếu để trống, sẽ không sử dụng hình ảnh branding. Xem `splash-screen dimensions <https://developer.android.com/develop/ui/views/launch/splash-screen#dimensions>`__.

\ **Lưu ý:** Có thể dùng tùy chọn này để đặt một hình ảnh hiển thị ở cuối splash screen.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_splash_screen/disable_godot_boot_splash:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **splash_screen/disable_godot_boot_splash** :ref:`🔗<class_EditorExportPlatformAndroid_property_splash_screen/disable_godot_boot_splash>`

Nếu ``true``, splash screen khởi động của Godot sẽ không được hiển thị và splash screen khởi động của hệ thống sẽ vẫn hiển thị lâu hơn, cho đến khi mainloop bắt đầu.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_splash_screen/icon:

.. rst-class:: classref-property

:ref:`String<class_String>` **splash_screen/icon** :ref:`🔗<class_EditorExportPlatformAndroid_property_splash_screen/icon>`

Tệp biểu tượng splash screen của hệ thống. Nếu để trống, giá trị này sẽ quay về :ref:`launcher_icons/adaptive_foreground_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_foreground_432x432>`. Xem `splash-screen dimensions <https://developer.android.com/develop/ui/views/launch/splash-screen#dimensions>`__.

\ **Lưu ý:** Bạn có thể cung cấp một XML `AnimatedVectorDrawable (AVD) <https://developer.android.com/reference/android/graphics/drawable/AnimatedVectorDrawable>`__. Tuy nhiên, tệp XML sẽ chỉ được sử dụng nếu :ref:`gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật. Nếu không, giá trị này sẽ quay về :ref:`launcher_icons/adaptive_background_432x432<class_EditorExportPlatformAndroid_property_launcher_icons/adaptive_background_432x432>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_user_data_backup/allow:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **user_data_backup/allow** :ref:`🔗<class_EditorExportPlatformAndroid_property_user_data_backup/allow>`

Nếu ``true``, cho phép ứng dụng tham gia vào infrastructure sao lưu và khôi phục.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_version/code:

.. rst-class:: classref-property

:ref:`int<class_int>` **version/code** :ref:`🔗<class_EditorExportPlatformAndroid_property_version/code>`

Phiên bản ứng dụng mà máy có thể đọc. Giá trị này phải được tăng lên trong mỗi bản phát hành mới được đẩy lên Play Store.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_version/name:

.. rst-class:: classref-property

:ref:`String<class_String>` **version/name** :ref:`🔗<class_EditorExportPlatformAndroid_property_version/name>`

Phiên bản ứng dụng hiển thị cho người dùng. Nếu để trống, giá trị này sẽ mặc định là :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformAndroid_property_xr_features/xr_mode:

.. rst-class:: classref-property

:ref:`int<class_int>` **xr_features/xr_mode** :ref:`🔗<class_EditorExportPlatformAndroid_property_xr_features/xr_mode>`

Chế độ thực tế mở rộng (XR) dành cho ứng dụng này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
