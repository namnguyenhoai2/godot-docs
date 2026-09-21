:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/platform/macos/doc_classes/EditorExportPlatformMacOS.xml.

.. _class_EditorExportPlatformMacOS:

EditorExportPlatformMacOS
=========================

**Kế thừa:** :ref:`EditorExportPlatform<class_EditorExportPlatform>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Exporter cho macOS.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Xuất cho macOS <../tutorials/export/exporting_for_macos>`

- :doc:`Chạy ứng dụng Godot trên macOS <../tutorials//export/running_on_macos>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/additional_plist_content<class_EditorExportPlatformMacOS_property_application/additional_plist_content>`                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/app_category<class_EditorExportPlatformMacOS_property_application/app_category>`                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/bundle_identifier<class_EditorExportPlatformMacOS_property_application/bundle_identifier>`                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/copyright<class_EditorExportPlatformMacOS_property_application/copyright>`                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`application/copyright_localized<class_EditorExportPlatformMacOS_property_application/copyright_localized>`                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`application/export_angle<class_EditorExportPlatformMacOS_property_application/export_angle>`                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/icon<class_EditorExportPlatformMacOS_property_application/icon>`                                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`application/icon_interpolation<class_EditorExportPlatformMacOS_property_application/icon_interpolation>`                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/liquid_glass_icon<class_EditorExportPlatformMacOS_property_application/liquid_glass_icon>`                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/min_macos_version_arm64<class_EditorExportPlatformMacOS_property_application/min_macos_version_arm64>`                                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/min_macos_version_x86_64<class_EditorExportPlatformMacOS_property_application/min_macos_version_x86_64>`                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/short_version<class_EditorExportPlatformMacOS_property_application/short_version>`                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/signature<class_EditorExportPlatformMacOS_property_application/signature>`                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/version<class_EditorExportPlatformMacOS_property_application/version>`                                                                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`binary_format/architecture<class_EditorExportPlatformMacOS_property_binary_format/architecture>`                                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/apple_team_id<class_EditorExportPlatformMacOS_property_codesign/apple_team_id>`                                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/certificate_file<class_EditorExportPlatformMacOS_property_codesign/certificate_file>`                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/certificate_password<class_EditorExportPlatformMacOS_property_codesign/certificate_password>`                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/codesign<class_EditorExportPlatformMacOS_property_codesign/codesign>`                                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`codesign/custom_options<class_EditorExportPlatformMacOS_property_codesign/custom_options>`                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/entitlements/additional<class_EditorExportPlatformMacOS_property_codesign/entitlements/additional>`                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/address_book<class_EditorExportPlatformMacOS_property_codesign/entitlements/address_book>`                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/allow_dyld_environment_variables<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_dyld_environment_variables>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/allow_jit_code_execution<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_jit_code_execution>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/allow_unsigned_executable_memory<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_unsigned_executable_memory>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/app_sandbox/device_bluetooth<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_bluetooth>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/app_sandbox/device_usb<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_usb>`                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/app_sandbox/enabled<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/enabled>`                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/entitlements/app_sandbox/files_downloads<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_downloads>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/entitlements/app_sandbox/files_movies<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_movies>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/entitlements/app_sandbox/files_music<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_music>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/entitlements/app_sandbox/files_pictures<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_pictures>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/entitlements/app_sandbox/files_user_selected<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_user_selected>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                         | :ref:`codesign/entitlements/app_sandbox/helper_executables<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/helper_executables>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/app_sandbox/network_client<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_client>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/app_sandbox/network_server<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_server>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/apple_events<class_EditorExportPlatformMacOS_property_codesign/entitlements/apple_events>`                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/audio_input<class_EditorExportPlatformMacOS_property_codesign/entitlements/audio_input>`                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/calendars<class_EditorExportPlatformMacOS_property_codesign/entitlements/calendars>`                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/camera<class_EditorExportPlatformMacOS_property_codesign/entitlements/camera>`                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/entitlements/custom_file<class_EditorExportPlatformMacOS_property_codesign/entitlements/custom_file>`                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/debugging<class_EditorExportPlatformMacOS_property_codesign/entitlements/debugging>`                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/disable_library_validation<class_EditorExportPlatformMacOS_property_codesign/entitlements/disable_library_validation>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/location<class_EditorExportPlatformMacOS_property_codesign/entitlements/location>`                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/entitlements/photos_library<class_EditorExportPlatformMacOS_property_codesign/entitlements/photos_library>`                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/identity<class_EditorExportPlatformMacOS_property_codesign/identity>`                                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/installer_identity<class_EditorExportPlatformMacOS_property_codesign/installer_identity>`                                                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/provisioning_profile<class_EditorExportPlatformMacOS_property_codesign/provisioning_profile>`                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/debug<class_EditorExportPlatformMacOS_property_custom_template/debug>`                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/release<class_EditorExportPlatformMacOS_property_custom_template/release>`                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`debug/export_console_wrapper<class_EditorExportPlatformMacOS_property_debug/export_console_wrapper>`                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`display/high_res<class_EditorExportPlatformMacOS_property_display/high_res>`                                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`export/distribution_type<class_EditorExportPlatformMacOS_property_export/distribution_type>`                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`notarization/api_key<class_EditorExportPlatformMacOS_property_notarization/api_key>`                                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`notarization/api_key_id<class_EditorExportPlatformMacOS_property_notarization/api_key_id>`                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`notarization/api_uuid<class_EditorExportPlatformMacOS_property_notarization/api_uuid>`                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`notarization/apple_id_name<class_EditorExportPlatformMacOS_property_notarization/apple_id_name>`                                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`notarization/apple_id_password<class_EditorExportPlatformMacOS_property_notarization/apple_id_password>`                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`notarization/notarization<class_EditorExportPlatformMacOS_property_notarization/notarization>`                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/address_book_usage_description<class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description>`                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/address_book_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description_localized>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/calendar_usage_description<class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description>`                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/calendar_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description_localized>`                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/camera_usage_description<class_EditorExportPlatformMacOS_property_privacy/camera_usage_description>`                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/camera_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/camera_usage_description_localized>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/advertising_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/advertising_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/advertising_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/advertising_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/audio_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collected>`                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/audio_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collection_purposes>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/audio_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/linked_to_user>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/audio_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/used_for_tracking>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/browsing_history/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/browsing_history/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/browsing_history/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/browsing_history/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/coarse_location/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collected>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/coarse_location/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collection_purposes>`                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/coarse_location/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/linked_to_user>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/coarse_location/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/used_for_tracking>`                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/contacts/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collected>`                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/contacts/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collection_purposes>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/contacts/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/linked_to_user>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/contacts/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/used_for_tracking>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/crash_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collected>`                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/crash_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collection_purposes>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/crash_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/linked_to_user>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/crash_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/used_for_tracking>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/credit_info/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collected>`                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/credit_info/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collection_purposes>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/credit_info/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/linked_to_user>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/credit_info/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/used_for_tracking>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/customer_support/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/customer_support/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/customer_support/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/customer_support/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/device_id/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collected>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/device_id/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collection_purposes>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/device_id/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/linked_to_user>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/device_id/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/used_for_tracking>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/email_address/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collected>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/email_address/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collection_purposes>`                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/email_address/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/linked_to_user>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/email_address/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/used_for_tracking>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/emails_or_text_messages/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collected>`                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/emails_or_text_messages/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collection_purposes>` |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/emails_or_text_messages/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/linked_to_user>`           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/emails_or_text_messages/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/used_for_tracking>`     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/environment_scanning/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collected>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/environment_scanning/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collection_purposes>`       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/environment_scanning/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/linked_to_user>`                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/environment_scanning/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/used_for_tracking>`           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/fitness/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collected>`                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/fitness/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collection_purposes>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/fitness/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/linked_to_user>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/fitness/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/used_for_tracking>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/gameplay_content/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/gameplay_content/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/gameplay_content/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/gameplay_content/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/hands/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collected>`                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/hands/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collection_purposes>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/hands/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/linked_to_user>`                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/hands/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/used_for_tracking>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/head/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collected>`                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/head/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collection_purposes>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/head/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/linked_to_user>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/head/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/used_for_tracking>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/health/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collected>`                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/health/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collection_purposes>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/health/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/linked_to_user>`                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/health/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/used_for_tracking>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/name/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collected>`                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/name/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collection_purposes>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/name/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/linked_to_user>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/name/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/used_for_tracking>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_contact_info/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collected>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_contact_info/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collection_purposes>`           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_contact_info/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/linked_to_user>`                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_contact_info/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/used_for_tracking>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_data_types/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_data_types/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_data_types/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_data_types/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_diagnostic_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collected>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_diagnostic_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collection_purposes>`     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_diagnostic_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/linked_to_user>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_diagnostic_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/used_for_tracking>`         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_financial_info/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collected>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_financial_info/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collection_purposes>`       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_financial_info/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/linked_to_user>`                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_financial_info/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/used_for_tracking>`           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_usage_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_usage_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_usage_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_usage_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_user_content/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collected>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/other_user_content/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collection_purposes>`           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_user_content/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/linked_to_user>`                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/other_user_content/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/used_for_tracking>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/payment_info/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collected>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/payment_info/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collection_purposes>`                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/payment_info/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/linked_to_user>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/payment_info/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/used_for_tracking>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/performance_data/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/performance_data/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/performance_data/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/performance_data/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/phone_number/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collected>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/phone_number/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collection_purposes>`                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/phone_number/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/linked_to_user>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/phone_number/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/used_for_tracking>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/photos_or_videos/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/photos_or_videos/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/photos_or_videos/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/photos_or_videos/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/physical_address/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/physical_address/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/physical_address/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/physical_address/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/precise_location/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/precise_location/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/precise_location/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/precise_location/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/product_interaction/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collected>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/product_interaction/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collection_purposes>`         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/product_interaction/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/linked_to_user>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/product_interaction/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/used_for_tracking>`             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/purchase_history/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collected>`                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/purchase_history/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collection_purposes>`               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/purchase_history/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/linked_to_user>`                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/purchase_history/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/used_for_tracking>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/search_history/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collected>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/search_history/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collection_purposes>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/search_history/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/linked_to_user>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/search_history/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/used_for_tracking>`                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/sensitive_info/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collected>`                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/sensitive_info/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collection_purposes>`                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/sensitive_info/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/linked_to_user>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/sensitive_info/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/used_for_tracking>`                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/user_id/collected<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collected>`                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`privacy/collected_data/user_id/collection_purposes<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collection_purposes>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/user_id/linked_to_user<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/linked_to_user>`                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/collected_data/user_id/used_for_tracking<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/used_for_tracking>`                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/desktop_folder_usage_description<class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description>`                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/desktop_folder_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description_localized>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/documents_folder_usage_description<class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/documents_folder_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description_localized>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/downloads_folder_usage_description<class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description>`                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/downloads_folder_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description_localized>`                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/location_usage_description<class_EditorExportPlatformMacOS_property_privacy/location_usage_description>`                                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/location_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/location_usage_description_localized>`                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/microphone_usage_description<class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description>`                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/microphone_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description_localized>`                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/network_volumes_usage_description<class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description>`                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/network_volumes_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description_localized>`                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/photos_library_usage_description<class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description>`                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/photos_library_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description_localized>`                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`privacy/removable_volumes_usage_description<class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description>`                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`privacy/removable_volumes_usage_description_localized<class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description_localized>`                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`privacy/tracking_domains<class_EditorExportPlatformMacOS_property_privacy/tracking_domains>`                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`privacy/tracking_enabled<class_EditorExportPlatformMacOS_property_privacy/tracking_enabled>`                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`shader_baker/enabled<class_EditorExportPlatformMacOS_property_shader_baker/enabled>`                                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/cleanup_script<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/cleanup_script>`                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`ssh_remote_deploy/enabled<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/enabled>`                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/extra_args_scp<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_scp>`                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/extra_args_ssh<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_ssh>`                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/host<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/host>`                                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/port<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/port>`                                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/run_script<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/run_script>`                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/platform_build<class_EditorExportPlatformMacOS_property_xcode/platform_build>`                                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/sdk_build<class_EditorExportPlatformMacOS_property_xcode/sdk_build>`                                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/sdk_name<class_EditorExportPlatformMacOS_property_xcode/sdk_name>`                                                                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/sdk_version<class_EditorExportPlatformMacOS_property_xcode/sdk_version>`                                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/xcode_build<class_EditorExportPlatformMacOS_property_xcode/xcode_build>`                                                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`xcode/xcode_version<class_EditorExportPlatformMacOS_property_xcode/xcode_version>`                                                                                               |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorExportPlatformMacOS_property_application/additional_plist_content:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/additional_plist_content** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/additional_plist_content>`

Dữ liệu bổ sung được thêm vào section ``<dict>`` gốc của tệp `Info.plist <https://developer.apple.com/documentation/bundleresources/information_property_list>`__. Giá trị phải là một section XML gồm các cặp phần tử khóa-giá trị, ví dụ:

.. code:: text

    <key>key_name</key>
    <string>value</string>

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/app_category:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/app_category** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/app_category>`

Danh mục ứng dụng trên App Store.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/bundle_identifier:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/bundle_identifier** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/bundle_identifier>`

Mã định danh ứng dụng duy nhất theo định dạng reverse-DNS, chỉ được chứa các ký tự chữ và số (``A-Z``, ``a-z`` và ``0-9``), dấu gạch nối (``-``) và dấu chấm (``.``).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/copyright:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/copyright** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/copyright>`

Thông báo bản quyền của bundle hiển thị cho người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/copyright_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **application/copyright_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/copyright_localized>`

Thông báo bản quyền của bundle hiển thị cho người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/export_angle:

.. rst-class:: classref-property

:ref:`int<class_int>` **application/export_angle** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/export_angle>`

Nếu đặt thành ``1``, các thư viện ANGLE sẽ được xuất cùng ứng dụng đã xuất. Nếu đặt thành ``0``, các thư viện ANGLE chỉ được xuất khi :ref:`ProjectSettings.rendering/gl_compatibility/driver<class_ProjectSettings_property_rendering/gl_compatibility/driver>` được đặt thành ``"opengl3_angle"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/icon:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/icon** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/icon>`

Tệp biểu tượng ứng dụng. Nếu để trống, thuộc tính sẽ fallback về :ref:`ProjectSettings.application/config/macos_native_icon<class_ProjectSettings_property_application/config/macos_native_icon>`, sau đó đến :ref:`ProjectSettings.application/config/icon<class_ProjectSettings_property_application/config/icon>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/icon_interpolation:

.. rst-class:: classref-property

:ref:`int<class_int>` **application/icon_interpolation** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/icon_interpolation>`

Phương pháp interpolation được sử dụng để thay đổi kích thước biểu tượng ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/liquid_glass_icon:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/liquid_glass_icon** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/liquid_glass_icon>`

Tệp nguồn biểu tượng Liquid Glass của macOS 26. Sử dụng `Icon Composer <https://developer.apple.com/icon-composer/>`__ để tạo biểu tượng Liquid Glass.

\ **Lưu ý:** Chỉ được hỗ trợ khi xuất từ macOS, yêu cầu Xcode 26+.

\ **Lưu ý:** Biểu tượng Liquid Glass chỉ được hỗ trợ trên macOS 26; sử dụng :ref:`application/icon<class_EditorExportPlatformMacOS_property_application/icon>` để đặt biểu tượng cho các phiên bản macOS cũ hơn.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/min_macos_version_arm64:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/min_macos_version_arm64** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/min_macos_version_arm64>`

Phiên bản macOS tối thiểu cần thiết để ứng dụng này chạy trên máy Mac Apple Silicon, theo định dạng ``major.minor.patch`` hoặc ``major.minor``, chỉ được chứa các ký tự số (``0-9``) và dấu chấm (``.``).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/min_macos_version_x86_64:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/min_macos_version_x86_64** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/min_macos_version_x86_64>`

Phiên bản macOS tối thiểu cần thiết để ứng dụng này chạy trên máy Mac Intel, theo định dạng ``major.minor.patch`` hoặc ``major.minor``, chỉ được chứa các ký tự số (``0-9``) và dấu chấm (``.``).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/short_version:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/short_version** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/short_version>`

Phiên bản ứng dụng hiển thị cho người dùng. Chỉ được chứa các ký tự số (``0-9``) và dấu chấm (``.``). Nếu để trống, sẽ fallback về :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>`.

\ **Lưu ý:** Giá trị này được sử dụng cho giá trị *Identity > Version* trong Xcode project được tạo.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/signature:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/signature** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/signature>`

Mã creator gồm bốn ký tự, dành riêng cho bundle. Không bắt buộc.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_application/version:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/version** :ref:`🔗<class_EditorExportPlatformMacOS_property_application/version>`

Phiên bản ứng dụng dành cho máy đọc theo định dạng ``major.minor.patch``. Chỉ được chứa các ký tự số (``0-9``) và dấu chấm (``.``). Giá trị này phải được tăng sau mỗi bản phát hành mới được đưa lên App Store. Nếu để trống, sẽ fallback về :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>`.

\ **Lưu ý:** Giá trị này được sử dụng cho giá trị *Identity > Build* trong Xcode project được tạo.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_binary_format/architecture:

.. rst-class:: classref-property

:ref:`String<class_String>` **binary_format/architecture** :ref:`🔗<class_EditorExportPlatformMacOS_property_binary_format/architecture>`

Kiến trúc executable của ứng dụng.

Các kiến trúc được hỗ trợ: ``x86_64``, ``arm64`` và ``universal`` (``x86_64 + arm64``).

Các export template chính thức chỉ bao gồm binary ``universal``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/apple_team_id:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/apple_team_id** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/apple_team_id>`

Apple Team ID, một chuỗi duy nhất gồm 10 ký tự. Để tìm Team ID, hãy kiểm tra section "Membership details" trong dashboard tài khoản Apple developer hoặc "Organizational Unit" của chứng chỉ code signing. Xem `Locate your Team ID <https://developer.apple.com/help/account/manage-your-team/locate-your-team-id>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/certificate_file:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/certificate_file** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/certificate_file>`

Tệp chứng chỉ PKCS #12 được sử dụng để ký bundle ``.app``.

Có thể ghi đè bằng environment variable ``GODOT_MACOS_CODESIGN_CERTIFICATE_FILE``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/certificate_password:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/certificate_password** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/certificate_password>`

Mật khẩu của tệp chứng chỉ được sử dụng để ký bundle ``.app``.

Có thể ghi đè bằng environment variable ``GODOT_MACOS_CODESIGN_CERTIFICATE_PASSWORD``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/codesign:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/codesign** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/codesign>`

Công cụ được sử dụng cho code signing.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/custom_options:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **codesign/custom_options** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/custom_options>`

Mảng các đối số command line bổ sung được truyền cho công cụ code signing.

**Lưu ý:** Mảng được trả về là bản *sao chép* và mọi thay đổi trên đó sẽ không cập nhật giá trị thuộc tính gốc. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/additional:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/entitlements/additional** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/additional>`

Dữ liệu bổ sung được thêm vào section ``<dict>`` gốc của tệp `.entitlements <https://developer.apple.com/documentation/bundleresources/entitlements>`__. Giá trị phải là một section XML gồm các cặp phần tử khóa-giá trị, ví dụ:

.. code:: text

    <key>key_name</key>
    <string>value</string>

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/address_book:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/address_book** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/address_book>`

Bật để cho phép truy cập danh bạ trong address book của người dùng; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/address_book_usage_description<class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description>`. Xem `com.apple.security.personal-information.addressbook <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_personal-information_addressbook>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_dyld_environment_variables:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/allow_dyld_environment_variables** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_dyld_environment_variables>`

Cho phép ứng dụng sử dụng các environment variable của dynamic linker để inject code. Nếu bạn sử dụng add-on có native code động hoặc tự sửa đổi, hãy bật tùy chọn này theo tài liệu của add-on. Xem `com.apple.security.cs.allow-dyld-environment-variables <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_cs_allow-dyld-environment-variables>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_jit_code_execution:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/allow_jit_code_execution** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_jit_code_execution>`

Cho phép tạo vùng nhớ có thể ghi và thực thi cho JIT code. Nếu bạn sử dụng add-on có native code động hoặc tự sửa đổi, hãy bật tùy chọn này theo tài liệu của add-on. Xem `com.apple.security.cs.allow-jit <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_cs_allow-jit>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_unsigned_executable_memory:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/allow_unsigned_executable_memory** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/allow_unsigned_executable_memory>`

Cho phép tạo vùng nhớ có thể ghi và thực thi mà không bị giới hạn JIT. Nếu bạn sử dụng add-on có native code động hoặc tự sửa đổi, hãy bật tùy chọn này theo tài liệu của add-on. Xem `com.apple.security.cs.allow-unsigned-executable-memory <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_cs_allow-unsigned-executable-memory>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_bluetooth:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/app_sandbox/device_bluetooth** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_bluetooth>`

Bật để cho phép ứng dụng tương tác với thiết bị Bluetooth. Entitlement này là bắt buộc để sử dụng controller không dây. Xem `com.apple.security.device.bluetooth <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_device_bluetooth>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_usb:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/app_sandbox/device_usb** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/device_usb>`

Bật để cho phép ứng dụng tương tác với thiết bị USB. Entitlement này là bắt buộc để sử dụng controller có dây. Xem `com.apple.security.device.usb <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_device_usb>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/app_sandbox/enabled** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/enabled>`

Bật App Sandbox. App Sandbox hạn chế quyền truy cập vào dữ liệu người dùng, mạng và thiết bị. Ứng dụng trong sandbox không thể truy cập hầu hết hệ thống tệp, không thể sử dụng hộp thoại tệp tùy chỉnh và thực thi binary bên ngoài bundle .app. Xem `App Sandbox <https://developer.apple.com/documentation/security/app_sandbox>`__.

\ **Lưu ý:** Để phân phối ứng dụng thông qua App Store, bạn phải bật App Sandbox.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_downloads:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/entitlements/app_sandbox/files_downloads** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_downloads>`

Cho phép quyền đọc hoặc ghi vào thư mục "Downloads" của người dùng. Xem `com.apple.security.files.downloads.read-write <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_downloads_read-write>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_movies:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/entitlements/app_sandbox/files_movies** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_movies>`

Cho phép quyền đọc hoặc ghi vào thư mục "Movies" của người dùng. Xem `com.apple.security.files.movies.read-write <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_assets_movies_read-write>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_music:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/entitlements/app_sandbox/files_music** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_music>`

Cho phép đọc hoặc ghi vào thư mục "Music" của người dùng. Xem `com.apple.security.files.music.read-write <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_assets_music_read-write>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_pictures:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/entitlements/app_sandbox/files_pictures** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_pictures>`

Cho phép đọc hoặc ghi vào thư mục "Pictures" của người dùng. Xem `com.apple.security.files.pictures.read-write <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_assets_pictures_read-write>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_user_selected:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/entitlements/app_sandbox/files_user_selected** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/files_user_selected>`

Cho phép đọc hoặc ghi vào các vị trí mà người dùng đã chọn bằng hộp thoại tệp gốc. Xem `com.apple.security.files.user-selected.read-write <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_files_user-selected_read-write>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/helper_executables:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **codesign/entitlements/app_sandbox/helper_executables** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/helper_executables>`

Danh sách các helper executable được nhúng vào app bundle. App sandboxed chỉ được phép thực thi các executable này. Xem `Embedding a command-line tool in a sandboxed app <https://developer.apple.com/documentation/xcode/embedding-a-helper-tool-in-a-sandboxed-app>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_client:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/app_sandbox/network_client** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_client>`

Bật để cho phép app thiết lập các kết nối mạng đi. Xem `com.apple.security.network.client <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_network_client>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_server:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/app_sandbox/network_server** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/app_sandbox/network_server>`

Bật để cho phép app lắng nghe các kết nối mạng đến. Xem `com.apple.security.network.server <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_network_server>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/apple_events:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/apple_events** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/apple_events>`

Bật để cho phép app gửi Apple events đến các app khác. Xem `com.apple.security.automation.apple-events <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_automation_apple-events>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/audio_input:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/audio_input** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/audio_input>`

Bật nếu bạn cần sử dụng microphone hoặc các nguồn audio input khác; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/microphone_usage_description<class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description>`. Xem `com.apple.security.device.audio-input <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_device_audio-input>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/calendars:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/calendars** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/calendars>`

Bật để cho phép truy cập calendar của người dùng; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/calendar_usage_description<class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description>`. Xem `com.apple.security.personal-information.calendars <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_personal-information_calendars>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/camera:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/camera** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/camera>`

Bật nếu bạn cần sử dụng camera; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/camera_usage_description<class_EditorExportPlatformMacOS_property_privacy/camera_usage_description>`. Xem `com.apple.security.device.camera <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_device_camera>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/custom_file:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/entitlements/custom_file** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/custom_file>`

Tệp entitlements tùy chỉnh ``.plist``; nếu được chỉ định, các entitlements còn lại trong export config sẽ bị bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/debugging:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/debugging** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/debugging>`

Bạn có thể tạm thời bật entitlement này để sử dụng native debugger (GDB, LLDB) với app đã export. Entitlement này nên được tắt khi export cho production. Xem `Embedding a command-line tool in a sandboxed app <https://developer.apple.com/documentation/xcode/embedding-a-helper-tool-in-a-sandboxed-app>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/disable_library_validation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/disable_library_validation** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/disable_library_validation>`

Cho phép app tải các library và framework tùy ý (không được ký bằng cùng Team ID với executable chính hoặc bởi Apple). Bật nếu bạn sử dụng các add-on GDExtension hoặc ad-hoc signing, hoặc muốn hỗ trợ các add-on bên ngoài do người dùng cung cấp. Xem `com.apple.security.cs.disable-library-validation <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_cs_disable-library-validation>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/location:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/location** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/location>`

Bật nếu bạn cần sử dụng thông tin vị trí từ Location Services; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/location_usage_description<class_EditorExportPlatformMacOS_property_privacy/location_usage_description>`. Xem `com.apple.security.personal-information.location <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_personal-information_location>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/entitlements/photos_library:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/entitlements/photos_library** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/entitlements/photos_library>`

Bật để cho phép truy cập thư viện Photos của người dùng; nếu bật, bạn cũng nên cung cấp thông báo mục đích sử dụng trong tùy chọn :ref:`privacy/photos_library_usage_description<class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description>`. Xem `com.apple.security.personal-information.photos-library <https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_personal-information_photos-library>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/identity:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/identity** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/identity>`

"Full Name", "Common Name" hoặc mã băm SHA-1 của signing identity được sử dụng để ký bundle ``.app``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/installer_identity:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/installer_identity** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/installer_identity>`

"Full Name", "Common Name" hoặc mã băm SHA-1 của signing identity được sử dụng để ký installer package ``.pkg`` cho việc phân phối trên App Store; sử dụng identity ``3rd Party Mac Developer Installer: Name.``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_codesign/provisioning_profile:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/provisioning_profile** :ref:`🔗<class_EditorExportPlatformMacOS_property_codesign/provisioning_profile>`

Tệp provisioning profile được tải xuống từ dashboard tài khoản Apple developer. Xem `Edit, download, or delete provisioning profiles <https://developer.apple.com/help/account/manage-profiles/edit-download-or-delete-profiles>`__.

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_CODESIGN_PROVISIONING_PROFILE``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_custom_template/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/debug** :ref:`🔗<class_EditorExportPlatformMacOS_property_custom_template/debug>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_custom_template/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/release** :ref:`🔗<class_EditorExportPlatformMacOS_property_custom_template/release>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_debug/export_console_wrapper:

.. rst-class:: classref-property

:ref:`int<class_int>` **debug/export_console_wrapper** :ref:`🔗<class_EditorExportPlatformMacOS_property_debug/export_console_wrapper>`

Nếu được bật, một wrapper có thể dùng để chạy application với console output sẽ được tạo cùng với application đã export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_display/high_res:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **display/high_res** :ref:`🔗<class_EditorExportPlatformMacOS_property_display/high_res>`

Nếu là ``true``, application được render ở native display resolution; nếu không, application luôn được render ở độ phân giải loDPI và được OS upscale khi cần.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_export/distribution_type:

.. rst-class:: classref-property

:ref:`int<class_int>` **export/distribution_type** :ref:`🔗<class_EditorExportPlatformMacOS_property_export/distribution_type>`

Đích phân phối application.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/api_key:

.. rst-class:: classref-property

:ref:`String<class_String>` **notarization/api_key** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/api_key>`

Tệp issuer key của Apple App Store Connect API.

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_NOTARIZATION_API_KEY``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/api_key_id:

.. rst-class:: classref-property

:ref:`String<class_String>` **notarization/api_key_id** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/api_key_id>`

Key ID của issuer Apple App Store Connect API.

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_NOTARIZATION_API_KEY_ID``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/api_uuid:

.. rst-class:: classref-property

:ref:`String<class_String>` **notarization/api_uuid** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/api_uuid>`

UUID của issuer Apple App Store Connect API.

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_NOTARIZATION_API_UUID``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/apple_id_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **notarization/apple_id_name** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/apple_id_name>`

Tên tài khoản Apple ID (địa chỉ email).

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_NOTARIZATION_APPLE_ID_NAME``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/apple_id_password:

.. rst-class:: classref-property

:ref:`String<class_String>` **notarization/apple_id_password** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/apple_id_password>`

Mật khẩu dành riêng cho app của Apple ID.

Có thể được ghi đè bằng biến môi trường ``GODOT_MACOS_NOTARIZATION_APPLE_ID_PASSWORD``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_notarization/notarization:

.. rst-class:: classref-property

:ref:`int<class_int>` **notarization/notarization** :ref:`🔗<class_EditorExportPlatformMacOS_property_notarization/notarization>`

Công cụ dùng cho notarization.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/address_book_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào danh bạ của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/address_book_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/address_book_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào danh bạ của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/calendar_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào dữ liệu calendar của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/calendar_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/calendar_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào dữ liệu calendar của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/camera_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/camera_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/camera_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào camera của thiết bị (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/camera_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/camera_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/camera_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào camera của thiết bị (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/advertising_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collected>`

Cho biết app của bạn có thu thập dữ liệu quảng cáo hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/advertising_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/collection_purposes>`

Các lý do app của bạn thu thập dữ liệu quảng cáo. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/advertising_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/linked_to_user>`

Cho biết app của bạn có liên kết dữ liệu quảng cáo với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/advertising_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/advertising_data/used_for_tracking>`

Cho biết app của bạn có sử dụng dữ liệu quảng cáo để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/audio_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collected>`

Cho biết app của bạn có thu thập dữ liệu audio hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/audio_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/collection_purposes>`

Các lý do ứng dụng của bạn thu thập dữ liệu âm thanh. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/audio_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu âm thanh với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/audio_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/audio_data/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu âm thanh để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/browsing_history/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collected>`

Cho biết ứng dụng của bạn có thu thập lịch sử duyệt web hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/browsing_history/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/collection_purposes>`

Các lý do ứng dụng của bạn thu thập lịch sử duyệt web. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/browsing_history/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết lịch sử duyệt web với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/browsing_history/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/browsing_history/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng lịch sử duyệt web để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/coarse_location/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu vị trí gần đúng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/coarse_location/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/collection_purposes>`

Các lý do ứng dụng của bạn thu thập dữ liệu vị trí gần đúng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/coarse_location/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu vị trí gần đúng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/coarse_location/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/coarse_location/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu vị trí gần đúng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/contacts/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collected>`

Cho biết ứng dụng của bạn có thu thập danh bạ hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/contacts/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/collection_purposes>`

Các lý do ứng dụng của bạn thu thập danh bạ. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/contacts/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết danh bạ với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/contacts/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/contacts/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng danh bạ để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/crash_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu sự cố hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/crash_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/collection_purposes>`

Các lý do ứng dụng của bạn thu thập dữ liệu sự cố. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/crash_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu sự cố với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/crash_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/crash_data/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu sự cố để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/credit_info/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collected>`

Cho biết ứng dụng của bạn có thu thập thông tin tín dụng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/credit_info/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/collection_purposes>`

Các lý do ứng dụng của bạn thu thập thông tin tín dụng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/credit_info/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết thông tin tín dụng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/credit_info/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/credit_info/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng thông tin tín dụng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/customer_support/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu hỗ trợ khách hàng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/customer_support/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/collection_purposes>`

Các lý do ứng dụng của bạn thu thập dữ liệu hỗ trợ khách hàng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/customer_support/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu hỗ trợ khách hàng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/customer_support/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/customer_support/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu hỗ trợ khách hàng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/device_id/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collected>`

Cho biết ứng dụng của bạn có thu thập device ID hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/device_id/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/collection_purposes>`

Các lý do ứng dụng của bạn thu thập device ID. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/device_id/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết device ID với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/device_id/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/device_id/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng device ID để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/email_address/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collected>`

Cho biết ứng dụng của bạn có thu thập địa chỉ email hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/email_address/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/collection_purposes>`

Các lý do ứng dụng của bạn thu thập địa chỉ email. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/email_address/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết địa chỉ email với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/email_address/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/email_address/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng địa chỉ email để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/emails_or_text_messages/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collected>`

Cho biết ứng dụng của bạn có thu thập email hoặc tin nhắn văn bản hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/emails_or_text_messages/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/collection_purposes>`

Các lý do ứng dụng của bạn thu thập email hoặc tin nhắn văn bản. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/emails_or_text_messages/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết email hoặc tin nhắn văn bản với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/emails_or_text_messages/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/emails_or_text_messages/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng email hoặc tin nhắn văn bản để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/environment_scanning/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu quét môi trường hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/environment_scanning/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/collection_purposes>`

Các lý do ứng dụng của bạn thu thập dữ liệu quét môi trường. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/environment_scanning/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu quét môi trường với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/environment_scanning/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/environment_scanning/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu quét môi trường để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/fitness/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu thể chất và tập luyện hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/fitness/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/collection_purposes>`

Lý do ứng dụng của bạn thu thập dữ liệu thể chất và tập luyện. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/fitness/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu thể chất và tập luyện với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/fitness/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/fitness/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu thể chất và tập luyện để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/gameplay_content/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collected>`

Cho biết ứng dụng của bạn có thu thập nội dung gameplay hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/gameplay_content/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/collection_purposes>`

Lý do ứng dụng của bạn thu thập nội dung gameplay. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/gameplay_content/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết nội dung gameplay với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/gameplay_content/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/gameplay_content/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng nội dung gameplay để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/hands/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collected>`

Cho biết ứng dụng của bạn có thu thập cấu trúc bàn tay và chuyển động bàn tay của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/hands/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/collection_purposes>`

Lý do ứng dụng của bạn thu thập cấu trúc bàn tay và chuyển động bàn tay của người dùng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/hands/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết cấu trúc bàn tay và chuyển động bàn tay của người dùng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/hands/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/hands/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng cấu trúc bàn tay và chuyển động bàn tay của người dùng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/head/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collected>`

Cho biết ứng dụng của bạn có thu thập chuyển động đầu của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/head/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/collection_purposes>`

Lý do ứng dụng của bạn thu thập chuyển động đầu của người dùng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/head/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/head/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết chuyển động đầu của người dùng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/head/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/head/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/head/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng chuyển động đầu của người dùng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/health/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collected>`

Cho biết ứng dụng của bạn có thu thập dữ liệu sức khỏe và y tế hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/health/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/collection_purposes>`

Lý do ứng dụng của bạn thu thập dữ liệu sức khỏe và y tế. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/health/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/health/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết dữ liệu sức khỏe và y tế với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/health/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/health/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/health/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu sức khỏe và y tế để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/name/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collected>`

Cho biết ứng dụng của bạn có thu thập tên của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/name/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/collection_purposes>`

Lý do ứng dụng của bạn thu thập tên của người dùng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/name/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/name/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết tên của người dùng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/name/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/name/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/name/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng tên của người dùng để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_contact_info/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ thông tin liên hệ nào khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_contact_info/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ thông tin liên hệ nào khác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_contact_info/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết bất kỳ thông tin liên hệ nào khác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_contact_info/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_contact_info/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng bất kỳ thông tin liên hệ nào khác để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_data_types/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ dữ liệu nào khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_data_types/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ dữ liệu nào khác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_data_types/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết bất kỳ dữ liệu nào khác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_data_types/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_data_types/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng bất kỳ dữ liệu nào khác để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_diagnostic_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ dữ liệu chẩn đoán nào khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_diagnostic_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ dữ liệu chẩn đoán nào khác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_diagnostic_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết bất kỳ dữ liệu chẩn đoán nào khác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_diagnostic_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_diagnostic_data/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng bất kỳ dữ liệu chẩn đoán nào khác để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_financial_info/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ thông tin tài chính nào khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_financial_info/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ thông tin tài chính nào khác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_financial_info/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết bất kỳ thông tin tài chính nào khác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_financial_info/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_financial_info/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng bất kỳ thông tin tài chính nào khác để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_usage_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ dữ liệu sử dụng nào khác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_usage_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ dữ liệu sử dụng nào khác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_usage_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết bất kỳ dữ liệu sử dụng nào khác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_usage_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_usage_data/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng bất kỳ dữ liệu sử dụng nào khác để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_user_content/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collected>`

Cho biết ứng dụng của bạn có thu thập bất kỳ nội dung nào khác do người dùng tạo hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/other_user_content/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/collection_purposes>`

Lý do ứng dụng của bạn thu thập bất kỳ nội dung nào khác do người dùng tạo. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_user_content/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết bất kỳ nội dung nào khác do người dùng tạo với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/other_user_content/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/other_user_content/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng bất kỳ nội dung nào khác do người dùng tạo để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/payment_info/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collected>`

Cho biết liệu ứng dụng của bạn có thu thập thông tin thanh toán hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/payment_info/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/collection_purposes>`

Lý do ứng dụng của bạn thu thập thông tin thanh toán. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/payment_info/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết thông tin thanh toán với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/payment_info/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/payment_info/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng thông tin thanh toán để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/performance_data/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collected>`

Cho biết liệu ứng dụng của bạn có thu thập dữ liệu hiệu suất hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/performance_data/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/collection_purposes>`

Lý do ứng dụng của bạn thu thập dữ liệu hiệu suất. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/performance_data/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết dữ liệu hiệu suất với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/performance_data/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/performance_data/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng dữ liệu hiệu suất để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/phone_number/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collected>`

Cho biết liệu ứng dụng của bạn có thu thập số điện thoại hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/phone_number/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/collection_purposes>`

Lý do ứng dụng của bạn thu thập số điện thoại. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/phone_number/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết số điện thoại với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/phone_number/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/phone_number/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng số điện thoại để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/photos_or_videos/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collected>`

Cho biết liệu ứng dụng của bạn có thu thập ảnh hoặc video hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/photos_or_videos/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/collection_purposes>`

Lý do ứng dụng của bạn thu thập ảnh hoặc video. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/photos_or_videos/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết ảnh hoặc video với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/photos_or_videos/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/photos_or_videos/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng ảnh hoặc video để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/physical_address/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collected>`

Cho biết liệu ứng dụng của bạn có thu thập địa chỉ thực hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/physical_address/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/collection_purposes>`

Lý do ứng dụng của bạn thu thập địa chỉ thực. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/physical_address/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết địa chỉ thực với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/physical_address/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/physical_address/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng địa chỉ thực để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/precise_location/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collected>`

Cho biết liệu ứng dụng của bạn có thu thập dữ liệu vị trí chính xác hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/precise_location/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/collection_purposes>`

Lý do ứng dụng của bạn thu thập dữ liệu vị trí chính xác. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/precise_location/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết dữ liệu vị trí chính xác với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/precise_location/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/precise_location/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng dữ liệu vị trí chính xác để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/product_interaction/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collected>`

Cho biết liệu ứng dụng của bạn có thu thập dữ liệu tương tác với sản phẩm hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/product_interaction/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/collection_purposes>`

Lý do ứng dụng của bạn thu thập dữ liệu tương tác với sản phẩm. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/product_interaction/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết dữ liệu tương tác với sản phẩm với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/product_interaction/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/product_interaction/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng dữ liệu tương tác với sản phẩm để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/purchase_history/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collected>`

Cho biết liệu ứng dụng của bạn có thu thập lịch sử mua hàng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/purchase_history/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/collection_purposes>`

Lý do ứng dụng của bạn thu thập lịch sử mua hàng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/purchase_history/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết lịch sử mua hàng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/purchase_history/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/purchase_history/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng lịch sử mua hàng để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/search_history/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collected>`

Cho biết liệu ứng dụng của bạn có thu thập lịch sử tìm kiếm hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/search_history/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/collection_purposes>`

Lý do ứng dụng của bạn thu thập lịch sử tìm kiếm. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/search_history/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết lịch sử tìm kiếm với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/search_history/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/search_history/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng lịch sử tìm kiếm để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/sensitive_info/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collected>`

Cho biết liệu ứng dụng của bạn có thu thập thông tin nhạy cảm của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/sensitive_info/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/collection_purposes>`

Lý do ứng dụng của bạn thu thập thông tin nhạy cảm của người dùng. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/sensitive_info/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/linked_to_user>`

Cho biết liệu ứng dụng của bạn có liên kết thông tin nhạy cảm của người dùng với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/sensitive_info/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/sensitive_info/used_for_tracking>`

Cho biết liệu ứng dụng của bạn có sử dụng thông tin nhạy cảm của người dùng để theo dõi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/user_id/collected** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collected>`

Cho biết liệu ứng dụng của bạn có thu thập user ID hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collection_purposes:

.. rst-class:: classref-property

:ref:`int<class_int>` **privacy/collected_data/user_id/collection_purposes** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/collection_purposes>`

Các lý do ứng dụng của bạn thu thập user ID. Xem `Describing data use in privacy manifests <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/linked_to_user:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/user_id/linked_to_user** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/linked_to_user>`

Cho biết ứng dụng của bạn có liên kết user ID với danh tính của người dùng hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/used_for_tracking:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/collected_data/user_id/used_for_tracking** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/collected_data/user_id/used_for_tracking>`

Cho biết ứng dụng của bạn có sử dụng user ID để tracking hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/desktop_folder_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Desktop" của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/desktop_folder_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/desktop_folder_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Desktop" của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/documents_folder_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Documents" của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/documents_folder_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/documents_folder_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Documents" của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/downloads_folder_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Downloads" của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/downloads_folder_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/downloads_folder_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư mục "Downloads" của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/location_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/location_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/location_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thông tin vị trí của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/location_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/location_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/location_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thông tin vị trí của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/microphone_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào microphone của thiết bị (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/microphone_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/microphone_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào microphone của thiết bị (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/network_volumes_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào các ổ đĩa mạng của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/network_volumes_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/network_volumes_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào các ổ đĩa mạng của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/photos_library_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư viện ảnh của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/photos_library_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/photos_library_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào thư viện ảnh của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **privacy/removable_volumes_usage_description** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào các ổ đĩa di động của người dùng (bằng tiếng Anh).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description_localized:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **privacy/removable_volumes_usage_description_localized** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/removable_volumes_usage_description_localized>`

Thông báo hiển thị khi yêu cầu quyền truy cập vào các ổ đĩa di động của người dùng (đã bản địa hóa).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/tracking_domains:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **privacy/tracking_domains** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/tracking_domains>`

Danh sách các miền internet mà ứng dụng của bạn kết nối đến và thực hiện tracking. Xem `Privacy manifest files <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files>`__.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_privacy/tracking_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **privacy/tracking_enabled** :ref:`🔗<class_EditorExportPlatformMacOS_property_privacy/tracking_enabled>`

Cho biết ứng dụng của bạn có sử dụng dữ liệu để tracking hay không. Xem `Privacy manifest files <https://developer.apple.com/documentation/bundleresources/privacy_manifest_files>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_shader_baker/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shader_baker/enabled** :ref:`🔗<class_EditorExportPlatformMacOS_property_shader_baker/enabled>`

Nếu ``true``, các shader sẽ được biên dịch và nhúng vào ứng dụng. Tùy chọn này chỉ được hỗ trợ khi sử dụng renderer Forward+ hoặc Mobile.

\ **Lưu ý:** Khi xuất dưới dạng dedicated server, shader baker luôn bị tắt vì không thực hiện rendering.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/cleanup_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/cleanup_script** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/cleanup_script>`

Mã script sẽ thực thi trên host từ xa khi ứng dụng hoàn tất.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn đến thư mục tạm trên máy từ xa, được dùng để tải ứng dụng và các script lên.

- ``{archive_name}`` - Tên của tệp ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của tệp thực thi ứng dụng.

- ``{cmd_args}`` - Mảng các đối số dòng lệnh của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ssh_remote_deploy/enabled** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/enabled>`

Bật remote deploy bằng SSH/SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_scp:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_scp** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_scp>`

Mảng các đối số dòng lệnh bổ sung được truyền cho SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_ssh:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_ssh** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/extra_args_ssh>`

Mảng các đối số dòng lệnh bổ sung được truyền cho SSH.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/host:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/host** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/host>`

Tên người dùng và địa chỉ SSH của host từ xa, theo định dạng ``user@address``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/port:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/port** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/port>`

Số cổng SSH của host từ xa.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_ssh_remote_deploy/run_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/run_script** :ref:`🔗<class_EditorExportPlatformMacOS_property_ssh_remote_deploy/run_script>`

Mã script sẽ thực thi trên host từ xa khi chạy ứng dụng.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn đến thư mục tạm trên máy từ xa, được dùng để tải ứng dụng và các script lên.

- ``{archive_name}`` - Tên của tệp ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của tệp thực thi ứng dụng.

- ``{cmd_args}`` - Mảng các đối số dòng lệnh của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/platform_build:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/platform_build** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/platform_build>`

Số bản build macOS được sử dụng để build tệp thực thi ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/sdk_build:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/sdk_build** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/sdk_build>`

Số bản build macOS SDK được sử dụng để build tệp thực thi ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/sdk_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/sdk_name** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/sdk_name>`

Tên macOS SDK được sử dụng để build tệp thực thi ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/sdk_version:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/sdk_version** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/sdk_version>`

Phiên bản macOS SDK được sử dụng để build tệp thực thi ứng dụng theo định dạng ``major.minor``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/xcode_build:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/xcode_build** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/xcode_build>`

Số bản build Xcode được sử dụng để build tệp thực thi ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformMacOS_property_xcode/xcode_version:

.. rst-class:: classref-property

:ref:`String<class_String>` **xcode/xcode_version** :ref:`🔗<class_EditorExportPlatformMacOS_property_xcode/xcode_version>`

Phiên bản Xcode được sử dụng để build tệp thực thi ứng dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
