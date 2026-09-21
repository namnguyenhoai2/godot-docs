:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorExportPlugin.xml.

.. _class_EditorExportPlugin:

EditorExportPlugin
==================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một script được thực thi khi export project.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorExportPlugin**\ được tự động gọi mỗi khi người dùng export project. Chúng có thể được dùng để sửa đổi các scene và resource trong quá trình export project, dựa trên các :doc:`Feature Tags <../tutorials/export/feature_tags>` được thiết lập. Với mỗi plugin, :ref:`_export_begin()<class_EditorExportPlugin_private_method__export_begin>` được gọi ở đầu quá trình export, sau đó :ref:`_export_file()<class_EditorExportPlugin_private_method__export_file>` được gọi cho từng tệp được export.

Đăng ký một **EditorExportPlugin** bằng cách tạo một :ref:`EditorPlugin<class_EditorPlugin>` mới và gọi method :ref:`EditorPlugin.add_export_plugin()<class_EditorPlugin_method_add_export_plugin>` của nó.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Export Android plugins <../tutorials/platform/android/android_plugin>`

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_begin_customize_resources<class_EditorExportPlugin_private_method__begin_customize_resources>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| |const|                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_begin_customize_scenes<class_EditorExportPlugin_private_method__begin_customize_scenes>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| |const|                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>`                                  | :ref:`_customize_resource<class_EditorExportPlugin_private_method__customize_resource>`\ (\ resource\: :ref:`Resource<class_Resource>`, path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                 |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`_customize_scene<class_EditorExportPlugin_private_method__customize_scene>`\ (\ scene\: :ref:`Node<class_Node>`, path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_end_customize_resources<class_EditorExportPlugin_private_method__end_customize_resources>`\ (\ ) |virtual|                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_end_customize_scenes<class_EditorExportPlugin_private_method__end_customize_scenes>`\ (\ ) |virtual|                                                                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_end_generate_apple_embedded_project<class_EditorExportPlugin_private_method__end_generate_apple_embedded_project>`\ (\ path\: :ref:`String<class_String>`, will_build_archive\: :ref:`bool<class_bool>`\ ) |virtual|                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_export_begin<class_EditorExportPlugin_private_method__export_begin>`\ (\ features\: :ref:`PackedStringArray<class_PackedStringArray>`, is_debug\: :ref:`bool<class_bool>`, path\: :ref:`String<class_String>`, flags\: :ref:`int<class_int>`\ ) |virtual|                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_export_end<class_EditorExportPlugin_private_method__export_end>`\ (\ ) |virtual|                                                                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_export_file<class_EditorExportPlugin_private_method__export_file>`\ (\ path\: :ref:`String<class_String>`, type\: :ref:`String<class_String>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual|                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_android_dependencies<class_EditorExportPlugin_private_method__get_android_dependencies>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_android_dependencies_maven_repos<class_EditorExportPlugin_private_method__get_android_dependencies_maven_repos>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|                           |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_android_libraries<class_EditorExportPlugin_private_method__get_android_libraries>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_android_manifest_activity_element_contents<class_EditorExportPlugin_private_method__get_android_manifest_activity_element_contents>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|       |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_android_manifest_application_element_contents<class_EditorExportPlugin_private_method__get_android_manifest_application_element_contents>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_android_manifest_element_contents<class_EditorExportPlugin_private_method__get_android_manifest_element_contents>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_customization_configuration_hash<class_EditorExportPlugin_private_method__get_customization_configuration_hash>`\ (\ ) |virtual| |required| |const|                                                                                                                     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_export_features<class_EditorExportPlugin_private_method__get_export_features>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const|                                                             |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_get_export_option_visibility<class_EditorExportPlugin_private_method__get_export_option_visibility>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_export_option_warning<class_EditorExportPlugin_private_method__get_export_option_warning>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_export_options<class_EditorExportPlugin_private_method__get_export_options>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const|                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`_get_export_options_overrides<class_EditorExportPlugin_private_method__get_export_options_overrides>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const|                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_name<class_EditorExportPlugin_private_method__get_name>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                             |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_should_update_export_options<class_EditorExportPlugin_private_method__should_update_export_options>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const|                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_supports_platform<class_EditorExportPlugin_private_method__supports_platform>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const|                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`                    | :ref:`_update_android_prebuilt_manifest<class_EditorExportPlugin_private_method__update_android_prebuilt_manifest>`\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, manifest_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |virtual| |const|     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_bundle_file<class_EditorExportPlugin_method_add_apple_embedded_platform_bundle_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_cpp_code<class_EditorExportPlugin_method_add_apple_embedded_platform_cpp_code>`\ (\ code\: :ref:`String<class_String>`\ )                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_embedded_framework<class_EditorExportPlugin_method_add_apple_embedded_platform_embedded_framework>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_framework<class_EditorExportPlugin_method_add_apple_embedded_platform_framework>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_linker_flags<class_EditorExportPlugin_method_add_apple_embedded_platform_linker_flags>`\ (\ flags\: :ref:`String<class_String>`\ )                                                                                                               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_plist_content<class_EditorExportPlugin_method_add_apple_embedded_platform_plist_content>`\ (\ plist_content\: :ref:`String<class_String>`\ )                                                                                                     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_apple_embedded_platform_project_static_lib<class_EditorExportPlugin_method_add_apple_embedded_platform_project_static_lib>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_file<class_EditorExportPlugin_method_add_file>`\ (\ path\: :ref:`String<class_String>`, file\: :ref:`PackedByteArray<class_PackedByteArray>`, remap\: :ref:`bool<class_bool>`\ )                                                                                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_bundle_file<class_EditorExportPlugin_method_add_ios_bundle_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_cpp_code<class_EditorExportPlugin_method_add_ios_cpp_code>`\ (\ code\: :ref:`String<class_String>`\ )                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_embedded_framework<class_EditorExportPlugin_method_add_ios_embedded_framework>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_framework<class_EditorExportPlugin_method_add_ios_framework>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_linker_flags<class_EditorExportPlugin_method_add_ios_linker_flags>`\ (\ flags\: :ref:`String<class_String>`\ )                                                                                                                                                       |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_plist_content<class_EditorExportPlugin_method_add_ios_plist_content>`\ (\ plist_content\: :ref:`String<class_String>`\ )                                                                                                                                             |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_ios_project_static_lib<class_EditorExportPlugin_method_add_ios_project_static_lib>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_macos_plugin_file<class_EditorExportPlugin_method_add_macos_plugin_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_shared_object<class_EditorExportPlugin_method_add_shared_object>`\ (\ path\: :ref:`String<class_String>`, tags\: :ref:`PackedStringArray<class_PackedStringArray>`, target\: :ref:`String<class_String>`\ )                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorExportPlatform<class_EditorExportPlatform>`          | :ref:`get_export_platform<class_EditorExportPlugin_method_get_export_platform>`\ (\ ) |const|                                                                                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorExportPreset<class_EditorExportPreset>`              | :ref:`get_export_preset<class_EditorExportPlugin_method_get_export_preset>`\ (\ ) |const|                                                                                                                                                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_option<class_EditorExportPlugin_method_get_option>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`skip<class_EditorExportPlugin_method_skip>`\ (\ )                                                                                                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_EditorExportPlugin_private_method__begin_customize_resources:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_begin_customize_resources**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__begin_customize_resources>`

Trả về ``true`` nếu plugin này sẽ tùy chỉnh các resource dựa trên platform và các feature được sử dụng.

Khi được bật, :ref:`_get_customization_configuration_hash()<class_EditorExportPlugin_private_method__get_customization_configuration_hash>` và :ref:`_customize_resource()<class_EditorExportPlugin_private_method__customize_resource>` sẽ được gọi và phải được implement.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__begin_customize_scenes:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_begin_customize_scenes**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__begin_customize_scenes>`

Trả về ``true`` nếu plugin này sẽ tùy chỉnh các scene dựa trên platform và các feature được sử dụng.

Khi được bật, :ref:`_get_customization_configuration_hash()<class_EditorExportPlugin_private_method__get_customization_configuration_hash>` và :ref:`_customize_scene()<class_EditorExportPlugin_private_method__customize_scene>` sẽ được gọi và phải được implement.

\ **Lưu ý:** :ref:`_customize_scene()<class_EditorExportPlugin_private_method__customize_scene>` sẽ chỉ được gọi cho các scene đã được sửa đổi kể từ lần export trước.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__customize_resource:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **_customize_resource**\ (\ resource\: :ref:`Resource<class_Resource>`, path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorExportPlugin_private_method__customize_resource>`

Tùy chỉnh một resource. Nếu có thay đổi, hãy trả về chính resource đó hoặc một resource mới. Nếu không, hãy trả về ``null``. Khi trả về một resource mới, ``resource`` sẽ được thay thế bằng một bản sao của resource mới.

Đối số ``path`` chỉ được sử dụng khi tùy chỉnh một tệp thực tế; nếu không, điều này có nghĩa resource này là một phần của resource khác và nó sẽ rỗng.

Việc implement method này là bắt buộc nếu :ref:`_begin_customize_resources()<class_EditorExportPlugin_private_method__begin_customize_resources>` trả về ``true``.

\ **Lưu ý:** Khi tùy chỉnh bất kỳ kiểu nào sau đây và trả về một resource khác, resource đó không được bỏ qua bằng cách sử dụng :ref:`skip()<class_EditorExportPlugin_method_skip>` trong :ref:`_export_file()<class_EditorExportPlugin_private_method__export_file>`:

- :ref:`AtlasTexture<class_AtlasTexture>`\

- :ref:`CompressedCubemap<class_CompressedCubemap>`\

- :ref:`CompressedCubemapArray<class_CompressedCubemapArray>`\

- :ref:`CompressedTexture2D<class_CompressedTexture2D>`\

- :ref:`CompressedTexture2DArray<class_CompressedTexture2DArray>`\

- :ref:`CompressedTexture3D<class_CompressedTexture3D>`

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__customize_scene:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **_customize_scene**\ (\ scene\: :ref:`Node<class_Node>`, path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorExportPlugin_private_method__customize_scene>`

Tùy chỉnh một scene. Nếu có thay đổi, hãy trả về chính scene đó hoặc một scene mới. Nếu không, hãy trả về ``null``. Nếu trả về một scene mới, bạn có trách nhiệm giải phóng scene cũ.

Việc implement method này là bắt buộc nếu :ref:`_begin_customize_scenes()<class_EditorExportPlugin_private_method__begin_customize_scenes>` trả về ``true``.

\ **Lưu ý:** Để thay đổi một biến trong scene, hãy sử dụng annotation ``@export`` khi khai báo biến đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__end_customize_resources:

.. rst-class:: classref-method

|void| **_end_customize_resources**\ (\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__end_customize_resources>`

Method này được gọi khi quá trình tùy chỉnh resource kết thúc.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__end_customize_scenes:

.. rst-class:: classref-method

|void| **_end_customize_scenes**\ (\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__end_customize_scenes>`

Method này được gọi khi quá trình tùy chỉnh scene kết thúc.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__end_generate_apple_embedded_project:

.. rst-class:: classref-method

|void| **_end_generate_apple_embedded_project**\ (\ path\: :ref:`String<class_String>`, will_build_archive\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__end_generate_apple_embedded_project>`

Method này được gọi sau khi tạo project Xcode nhưng trước khi project được build.

\ **Lưu ý:** Chỉ được hỗ trợ trên iOS và visionOS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__export_begin:

.. rst-class:: classref-method

|void| **_export_begin**\ (\ features\: :ref:`PackedStringArray<class_PackedStringArray>`, is_debug\: :ref:`bool<class_bool>`, path\: :ref:`String<class_String>`, flags\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__export_begin>`

Virtual method để người dùng override. Method này được gọi khi quá trình export bắt đầu và cung cấp mọi thông tin về quá trình export. ``features`` là danh sách các feature cho quá trình export, ``is_debug`` là ``true`` đối với các bản build debug, ``path`` là đường dẫn đích của project được export. ``flags`` chỉ được sử dụng khi chạy một runnable profile, ví dụ khi sử dụng native run trên Android.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__export_end:

.. rst-class:: classref-method

|void| **_export_end**\ (\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__export_end>`

Virtual method để người dùng override. Được gọi khi quá trình export hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__export_file:

.. rst-class:: classref-method

|void| **_export_file**\ (\ path\: :ref:`String<class_String>`, type\: :ref:`String<class_String>`, features\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| :ref:`🔗<class_EditorExportPlugin_private_method__export_file>`

Virtual method để người dùng override. Được gọi cho từng tệp được export trước :ref:`_customize_resource()<class_EditorExportPlugin_private_method__customize_resource>` và :ref:`_customize_scene()<class_EditorExportPlugin_private_method__customize_scene>`. Các đối số có thể được dùng để xác định tệp. ``path`` là đường dẫn của tệp, ``type`` là :ref:`Resource<class_Resource>` được tệp biểu diễn (ví dụ: :ref:`PackedScene<class_PackedScene>`), và ``features`` là danh sách các feature cho quá trình export.

Gọi :ref:`skip()<class_EditorExportPlugin_method_skip>` bên trong callback này sẽ khiến tệp không được đưa vào bản export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_dependencies:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_android_dependencies**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_dependencies>`

Virtual method để người dùng override. Method này được gọi để lấy tập hợp các Android dependency do plugin này cung cấp. Mỗi Android dependency được trả về phải có định dạng của một Android remote binary dependency: ``org.godot.example:my-plugin:0.0.0``\

Để biết thêm thông tin, hãy xem `Android documentation on dependencies <https://developer.android.com/build/dependencies?agpversion=4.1#dependency-types>`__.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_dependencies_maven_repos:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_android_dependencies_maven_repos**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_dependencies_maven_repos>`

Virtual method để người dùng override. Method này được gọi để lấy các URL của Maven repository cho tập hợp Android dependency do plugin này cung cấp.

Để biết thêm thông tin, hãy xem `Gradle documentation on dependency management <https://docs.gradle.org/current/userguide/dependency_management.html#sec:maven_repo>`__.

\ **Lưu ý:** Google Maven repo và Maven Central repo đã được bao gồm theo mặc định.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_libraries:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_android_libraries**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_libraries>`

Virtual method để người dùng override. Method này được gọi để lấy các đường dẫn cục bộ của các tệp archive thư viện Android (AAR) do plugin này cung cấp.

\ **Lưu ý:** Các đường dẫn tương đối **phải** tương đối với thư mục ``res://addons/`` của Godot. Ví dụ, một tệp AAR nằm dưới ``res://addons/hello_world_plugin/HelloWorld.release.aar`` có thể được trả về dưới dạng đường dẫn tuyệt đối bằng ``res://addons/hello_world_plugin/HelloWorld.release.aar`` hoặc đường dẫn tương đối bằng ``hello_world_plugin/HelloWorld.release.aar``.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_manifest_activity_element_contents:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_android_manifest_activity_element_contents**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_manifest_activity_element_contents>`

Virtual method để người dùng override. Method này được sử dụng tại thời điểm export để cập nhật nội dung của element ``activity`` trong Android manifest được tạo.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_manifest_application_element_contents:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_android_manifest_application_element_contents**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_manifest_application_element_contents>`

Virtual method để người dùng override. Method này được sử dụng tại thời điểm export để cập nhật nội dung của element ``application`` trong Android manifest được tạo.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_android_manifest_element_contents:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_android_manifest_element_contents**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_android_manifest_element_contents>`

Virtual method để người dùng override. Method này được sử dụng tại thời điểm export để cập nhật nội dung của element ``manifest`` trong Android manifest được tạo.

\ **Lưu ý:** Chỉ được hỗ trợ trên Android và yêu cầu :ref:`EditorExportPlatformAndroid.gradle_build/use_gradle_build<class_EditorExportPlatformAndroid_property_gradle_build/use_gradle_build>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_customization_configuration_hash:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_customization_configuration_hash**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_customization_configuration_hash>`

Trả về một hash dựa trên cấu hình được truyền vào (cho cả scene và resource). Điều này giúp duy trì các cache riêng biệt cho các cấu hình export riêng biệt.

Bắt buộc phải triển khai phương thức này nếu :ref:`_begin_customize_resources()<class_EditorExportPlugin_private_method__begin_customize_resources>` trả về ``true``.

\ **Lưu ý:** :ref:`_customize_resource()<class_EditorExportPlugin_private_method__customize_resource>` và :ref:`_customize_scene()<class_EditorExportPlugin_private_method__customize_scene>` sẽ không được gọi khi script **EditorExportPlugin** được sửa đổi, trừ khi hash này cũng thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_export_features:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_export_features**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, debug\: :ref:`bool<class_bool>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_export_features>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` gồm các feature bổ sung mà preset này, đối với ``platform`` đã cho, nên có.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_export_option_visibility:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_get_export_option_visibility**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_export_option_visibility>`

Xác thực ``option`` và trả về khả năng hiển thị của ``platform`` được chỉ định. Cài đặt mặc định trả về ``true`` cho tất cả option.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_export_option_warning:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_export_option_warning**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_export_option_warning>`

Kiểm tra các yêu cầu đối với ``option`` đã cho và trả về một chuỗi cảnh báo không rỗng nếu các yêu cầu đó không được đáp ứng.

\ **Lưu ý:** Sử dụng :ref:`get_option()<class_EditorExportPlugin_method_get_option>` để kiểm tra giá trị của các export option.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_export_options:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_export_options**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_export_options>`

Trả về danh sách các export option có thể được cấu hình cho export plugin này.

Mỗi phần tử trong giá trị trả về là một :ref:`Dictionary<class_Dictionary>` với các key sau:

- ``option``: Một dictionary có cấu trúc được ghi lại trong :ref:`Object.get_property_list()<class_Object_method_get_property_list>`, nhưng tất cả key đều là tùy chọn.

- ``default_value``: Giá trị mặc định cho option này.

- ``update_visibility``: Một giá trị boolean tùy chọn. Nếu được đặt thành ``true``, preset sẽ phát :ref:`Object.property_list_changed<class_Object_signal_property_list_changed>` khi option được thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_export_options_overrides:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_get_export_options_overrides**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_export_options_overrides>`

Trả về một :ref:`Dictionary<class_Dictionary>` gồm các giá trị override cho export option, được sử dụng thay cho các giá trị do người dùng cung cấp. Các option bị override sẽ bị ẩn khỏi giao diện người dùng.

::

    class MyExportPlugin extends EditorExportPlugin:
        func _get_name() -> String:
            return "MyExportPlugin"

        func _supports_platform(platform) -> bool:
            if platform is EditorExportPlatformPC:
                # Chạy trên tất cả nền tảng desktop, bao gồm Windows, MacOS và Linux.
                return true
            return false

        func _get_export_options_overrides(platform) -> Dictionary:
            # Override "Embed PCK" để luôn được bật.
            return {
                "binary_format/embed_pck": true,
            }

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__get_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_name**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorExportPlugin_private_method__get_name>`

Trả về định danh tên của plugin này (để exporter nhận diện trong tương lai). Các plugin được sắp xếp theo tên trước khi export.

Bắt buộc phải triển khai phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__should_update_export_options:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_should_update_export_options**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__should_update_export_options>`

Trả về ``true`` nếu kết quả của :ref:`_get_export_options()<class_EditorExportPlugin_private_method__get_export_options>` đã thay đổi và các export option của preset tương ứng với ``platform`` nên được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__supports_platform:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_supports_platform**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__supports_platform>`

Trả về ``true`` nếu plugin hỗ trợ ``platform`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_private_method__update_android_prebuilt_manifest:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **_update_android_prebuilt_manifest**\ (\ platform\: :ref:`EditorExportPlatform<class_EditorExportPlatform>`, manifest_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |virtual| |const| :ref:`🔗<class_EditorExportPlugin_private_method__update_android_prebuilt_manifest>`

Cung cấp quyền truy cập vào Android prebuilt manifest và cho phép plugin sửa đổi manifest nếu cần.

Các triển khai của virtual method này nên lấy dữ liệu manifest nhị phân từ ``manifest_data``, sao chép và sửa đổi dữ liệu, sau đó trả về dữ liệu cùng các thay đổi.

Nếu không cần sửa đổi, cần trả về một :ref:`PackedByteArray<class_PackedByteArray>` rỗng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_bundle_file:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_bundle_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_bundle_file>`

Thêm một file bundle của Apple embedded platform từ ``path`` đã cho vào project đã export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_cpp_code:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_cpp_code**\ (\ code\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_cpp_code>`

Thêm mã C++ vào Apple embedded platform export. Mã cuối cùng được tạo từ mã do mỗi export plugin đang hoạt động nối thêm.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_embedded_framework:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_embedded_framework**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_embedded_framework>`

Thêm một dynamic library (\*.dylib, \*.framework) vào Linking Phase trong project Xcode của Apple embedded platform và nhúng nó vào binary kết quả.

\ **Lưu ý:** Đối với static library (\*.a), thao tác này hoạt động giống như :ref:`add_apple_embedded_platform_framework()<class_EditorExportPlugin_method_add_apple_embedded_platform_framework>`.

\ **Lưu ý:** Không nên sử dụng phương thức này cho System library vì chúng đã có sẵn trên thiết bị.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_framework:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_framework**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_framework>`

Thêm một static library (\*.a) hoặc dynamic library (\*.dylib, \*.framework) vào Linking Phase của project Xcode trên Apple embedded platform.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_linker_flags:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_linker_flags**\ (\ flags\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_linker_flags>`

Thêm các linker flag cho Apple embedded platform export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_plist_content:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_plist_content**\ (\ plist_content\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_plist_content>`

Thêm các field bổ sung vào file Info.plist của project trên Apple embedded platform.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_apple_embedded_platform_project_static_lib:

.. rst-class:: classref-method

|void| **add_apple_embedded_platform_project_static_lib**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_apple_embedded_platform_project_static_lib>`

Thêm một static library từ ``path`` đã cho vào project trên Apple embedded platform.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_file:

.. rst-class:: classref-method

|void| **add_file**\ (\ path\: :ref:`String<class_String>`, file\: :ref:`PackedByteArray<class_PackedByteArray>`, remap\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_file>`

Thêm một file tùy chỉnh để export. ``path`` là virtual path có thể được sử dụng để load file, còn ``file`` là dữ liệu nhị phân của file.

Khi được gọi bên trong :ref:`_export_file()<class_EditorExportPlugin_private_method__export_file>` và ``remap`` là ``true``, file hiện tại sẽ không được export mà thay vào đó được remap tới file tùy chỉnh này. ``remap`` bị bỏ qua khi được gọi ở những nơi khác.

\ ``file`` sẽ không được import, vì vậy hãy cân nhắc sử dụng :ref:`_customize_resource()<class_EditorExportPlugin_private_method__customize_resource>` để remap các resource đã import.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_bundle_file:

.. rst-class:: classref-method

|void| **add_ios_bundle_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_bundle_file>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_bundle_file()<class_EditorExportPlugin_method_add_apple_embedded_platform_bundle_file>`.

Thêm một file bundle iOS từ ``path`` đã cho vào project đã export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_cpp_code:

.. rst-class:: classref-method

|void| **add_ios_cpp_code**\ (\ code\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_cpp_code>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_cpp_code()<class_EditorExportPlugin_method_add_apple_embedded_platform_cpp_code>`.

Thêm mã C++ vào iOS export. Mã cuối cùng được tạo từ mã do mỗi export plugin đang hoạt động nối thêm.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_embedded_framework:

.. rst-class:: classref-method

|void| **add_ios_embedded_framework**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_embedded_framework>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_embedded_framework()<class_EditorExportPlugin_method_add_apple_embedded_platform_embedded_framework>`.

Thêm một dynamic library (\*.dylib, \*.framework) vào Linking Phase trong project Xcode của iOS và nhúng nó vào binary kết quả.

\ **Lưu ý:** Đối với static library (\*.a), thao tác này hoạt động giống như :ref:`add_apple_embedded_platform_framework()<class_EditorExportPlugin_method_add_apple_embedded_platform_framework>`.

\ **Lưu ý:** Không nên sử dụng phương thức này cho System library vì chúng đã có sẵn trên thiết bị.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_framework:

.. rst-class:: classref-method

|void| **add_ios_framework**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_framework>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_framework()<class_EditorExportPlugin_method_add_apple_embedded_platform_framework>`.

Thêm một static library (\*.a) hoặc dynamic library (\*.dylib, \*.framework) vào Linking Phase của project Xcode iOS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_linker_flags:

.. rst-class:: classref-method

|void| **add_ios_linker_flags**\ (\ flags\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_linker_flags>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_linker_flags()<class_EditorExportPlugin_method_add_apple_embedded_platform_linker_flags>`.

Thêm các linker flag cho iOS export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_plist_content:

.. rst-class:: classref-method

|void| **add_ios_plist_content**\ (\ plist_content\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_plist_content>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_plist_content()<class_EditorExportPlugin_method_add_apple_embedded_platform_plist_content>`.

Thêm các field bổ sung vào file Info.plist của project iOS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_ios_project_static_lib:

.. rst-class:: classref-method

|void| **add_ios_project_static_lib**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_ios_project_static_lib>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`add_apple_embedded_platform_project_static_lib()<class_EditorExportPlugin_method_add_apple_embedded_platform_project_static_lib>`.

Thêm một static library từ ``path`` đã cho vào project iOS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_macos_plugin_file:

.. rst-class:: classref-method

|void| **add_macos_plugin_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_macos_plugin_file>`

Thêm tệp hoặc thư mục khớp với ``path`` vào thư mục ``PlugIns`` của gói ứng dụng macOS.

\ **Lưu ý:** Điều này chỉ hữu ích cho các bản export macOS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_add_shared_object:

.. rst-class:: classref-method

|void| **add_shared_object**\ (\ path\: :ref:`String<class_String>`, tags\: :ref:`PackedStringArray<class_PackedStringArray>`, target\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPlugin_method_add_shared_object>`

Thêm một shared object hoặc một thư mục chỉ chứa các shared object với ``tags`` và đích đến ``path`` đã cho.

\ **Lưu ý:** Trong trường hợp export macOS, các shared object đó sẽ được thêm vào thư mục ``Frameworks`` của gói ứng dụng.

Trong trường hợp là một thư mục, code-sign sẽ báo lỗi nếu bạn đặt đối tượng không phải code vào thư mục.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_get_export_platform:

.. rst-class:: classref-method

:ref:`EditorExportPlatform<class_EditorExportPlatform>` **get_export_platform**\ (\ ) |const| :ref:`🔗<class_EditorExportPlugin_method_get_export_platform>`

Trả về export platform hiện đang được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_get_export_preset:

.. rst-class:: classref-method

:ref:`EditorExportPreset<class_EditorExportPreset>` **get_export_preset**\ (\ ) |const| :ref:`🔗<class_EditorExportPlugin_method_get_export_preset>`

Trả về export preset hiện đang được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_get_option:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_option**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorExportPlugin_method_get_option>`

Trả về giá trị hiện tại của tùy chọn export được cung cấp bởi :ref:`_get_export_options()<class_EditorExportPlugin_private_method__get_export_options>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlugin_method_skip:

.. rst-class:: classref-method

|void| **skip**\ (\ ) :ref:`🔗<class_EditorExportPlugin_method_skip>`

Được gọi bên trong :ref:`_export_file()<class_EditorExportPlugin_private_method__export_file>`. Bỏ qua tệp hiện tại, vì vậy tệp đó sẽ không được đưa vào bản export.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
