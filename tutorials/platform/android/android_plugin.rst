.. _doc_android_plugin:

plugin Android của Godot
========================

Giới thiệu
----------

Plugin Android là các công cụ mạnh mẽ để mở rộng khả năng của Godot engine bằng cách tận dụng các chức năng do nền tảng và hệ sinh thái Android cung cấp.

Ví dụ, trong Godot 4, plugin Android được sử dụng để hỗ trợ nhiều nền tảng XR dựa trên Android mà không làm mã nguồn cốt lõi trở nên cồng kềnh bởi mã hoặc binary dành riêng cho từng nhà cung cấp.

Plugin Android
--------------

**Version 1 (v1)** của hệ thống plugin Android được giới thiệu trong Godot 3 và tương thích với Godot 4.0 và 4.1. Phiên bản này cho phép các developer mở rộng Godot engine bằng chức năng Java, Kotlin và native.

Bắt đầu từ Godot 4.2, các plugin Android được xây dựng trên kiến trúc v1 hiện đã deprecated. Thay vào đó, Godot 4.2 giới thiệu kiến trúc **Version 2 (v2)** mới cho plugin Android.

Kiến trúc v2
~~~~~~~~~~~~

.. note::

    Plugin Android của Godot tận dụng :ref:`Gradle build system <doc_android_gradle_build>`.


Dựa trên kiến trúc v1 trước đó, các plugin Android tiếp tục được xây dựng từ `Android archive library <https://developer.android.com/studio/projects/android-library#aar-contents>`_.

Về cốt lõi, plugin Android v2 của Godot là một Android library có dependency vào :ref:`Godot Android library <doc_android_library>` và một Android library manifest tùy chỉnh.

Kiến trúc này cho phép plugin Android mở rộng chức năng của engine bằng:

- API nền tảng Android - Android library - thư viện Kotlin và Java - thư viện native (thông qua JNI) - thư viện GDExtension

Mỗi plugin có một init class kế thừa từ class `GodotPlugin <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L80>`_, được cung cấp bởi :ref:`Godot Android library <doc_android_library>`.

Class ``GodotPlugin`` cung cấp các API để truy cập instance Godot đang chạy và hook vào vòng đời của instance đó. Class này được Godot engine load tại runtime.

Định dạng đóng gói v2
~~~~~~~~~~~~~~~~~~~~~

Plugin Android v1 yêu cầu một file cấu hình ``gdap`` tùy chỉnh, được Godot Editor sử dụng để phát hiện và load plugin. Tuy nhiên, cách tiếp cận này có một số nhược điểm, trong đó nhược điểm chính là thiếu tính linh hoạt và khác với `existing Godot EditorExportPlugin format, delivery and installation flow <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/installing_plugins.html>`_.

Vấn đề này đã được giải quyết đối với plugin Android v2 bằng cách deprecated cơ chế đóng gói và cấu hình ``gdap``, thay vào đó sử dụng định dạng đóng gói Godot ``EditorExportPlugin`` hiện có. API ``EditorExportPlugin`` cũng đã được mở rộng để hỗ trợ đúng cách cho plugin Android.


Xây dựng plugin Android v2
--------------------------

Một template project github **được cung cấp** tại https://github.com/m4gr3d/Godot-Android-Plugin-Template dưới dạng **quickstart để xây dựng plugin Android của Godot cho Godot 4.2+**. Bạn có thể làm theo `template README <https://github.com/m4gr3d/Godot-Android-Plugin-Template#readme>`_ để thiết lập project plugin Android Godot của riêng mình.

Để hiểu rõ hơn, dưới đây là phân tích các bước được sử dụng để tạo template project:

1. Tạo một Android library module bằng cách làm theo `these instructions <https://developer.android.com/studio/projects/android-library>`_.

2. Thêm Android library của Godot làm dependency bằng cách cập nhật ``gradle`` `build file <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/build.gradle.kts#L42>`_ của module:

    .. code:: text

        dependencies {
            implementation("org.godotengine:godot:4.2.0.stable")
        }

  Android library của Godot là `hosted on MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_ và được cập nhật trong mỗi release.

3. Tạo `GodotAndroidPlugin <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/a01286b4cb459133bf07b11dfabdfd3980268797/plugin/src/main/java/org/godotengine/plugin/android/template/GodotAndroidPlugin.kt#L10>`_, một init class cho plugin kế thừa `GodotPlugin <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L80>`_.

    - Nếu plugin cung cấp các method Kotlin hoặc Java để được gọi từ GDScript, chúng phải được gắn annotation `@UsedByGodot <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/UsedByGodot.java#L45>`_. Tên được gọi từ GDScript **phải khớp chính xác với tên method**. **Không** có coercing ``snake_case`` thành ``camelCase``. Ví dụ, từ GDScript:

        ::

            if Engine.has_singleton("MyPlugin"):
                var singleton = Engine.get_singleton("MyPlugin")
                print(singleton.myPluginFunction("World"))

    - Nếu plugin sử dụng `signals <https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html>`_, init class phải trả về tập hợp các signal được sử dụng bằng cách override `GodotPlugin::getPluginSignals() <https://github.com/godotengine/godot/blob/fa3428ff25bc577d2a3433090478a6d615567056/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L302>`_. Để emit signal, plugin có thể sử dụng `GodotPlugin::emitSignal(...) method <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L317>`_.

4. Cập nhật ``AndroidManifest.xml`` `file <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/src/main/AndroidManifest.xml>`_ của plugin với metadata sau:

    .. code-block:: xml

        <meta-data
            android:name="org.godotengine.plugin.v2.[PluginName]"
            android:value="[plugin.init.ClassFullName]" />


  Trong đó:

      - ``PluginName`` là tên của plugin - ``plugin.init.ClassFullName`` là tên component đầy đủ (package + class name) của init class của plugin (ví dụ: ``org.godotengine.plugin.android.template.GodotAndroidPlugin``).

5. Tạo `EditorExportPlugin configuration <https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_ để đóng gói plugin. Các bước được sử dụng để tạo cấu hình có thể xem trong phần `Đóng gói plugin Android v2`_.


Xây dựng plugin Android v2 với khả năng GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tương tự như hỗ trợ GDNative trong plugin Android v1, plugin Android v2 hỗ trợ khả năng tích hợp các chức năng GDExtension.

Một template project github được cung cấp tại https://github.com/m4gr3d/GDExtension-Android-Plugin-Template dưới dạng quickstart để xây dựng plugin Android GDExtension cho Godot 4.2+. Bạn có thể làm theo `template's README <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template#readme>`_ để thiết lập project plugin Android Godot của riêng mình.


Di chuyển plugin Android v1 sang v2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hãy sử dụng các bước sau nếu bạn có một plugin Android v1 muốn di chuyển sang v2:

1. Cập nhật file manifest của plugin:

    - Đổi prefix ``org.godotengine.plugin.v1`` thành ``org.godotengine.plugin.v2``

2. Cập nhật build dependency của Godot Android library:

    - Bạn có thể tiếp tục sử dụng binary ``godot-lib.<version>.<status>.aar`` từ `Godot's download page <https://godotengine.org/download>`_ nếu muốn. Hãy đảm bảo binary này được cập nhật lên phiên bản stable mới nhất. - Hoặc bạn có thể chuyển sang dependency do MavenCentral cung cấp:

::

    dependencies {
        implementation("org.godotengine:godot:4.2.0.stable")
    }

3. Sau khi cập nhật dependency của Godot Android library, hãy sync hoặc build plugin và xử lý mọi lỗi compile:

    - Instance ``Godot`` do ``GodotPlugin::getGodot()`` cung cấp không còn quyền truy cập vào một tham chiếu ``android.content.Context``. Thay vào đó, hãy sử dụng ``GodotPlugin::getActivity()``.

4. Xóa các file cấu hình ``gdap`` và làm theo hướng dẫn trong phần `Đóng gói plugin Android v2`_ để thiết lập cấu hình plugin.

Đóng gói plugin Android v2
--------------------------

Như đã đề cập, plugin Android v2 hiện được cung cấp cho Godot Editor dưới dạng plugin ``EditorExportPlugin``, vì vậy nó chia sẻ nhiều `same packaging steps <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#creating-a-plugin>`_.

1. Thêm các binary output của plugin vào trong thư mục plugin (ví dụ: trong ``addons/<plugin_name>/``)

2. Thêm `tool script <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#the-script-file>`_ cho chức năng export vào trong thư mục plugin (ví dụ: trong ``addons/<plugin_name>/``)

    - Script được tạo phải là script ``@tool``, nếu không nó sẽ không hoạt động đúng - Script export tool được sử dụng để cấu hình plugin Android và hook plugin vào quy trình export của Godot Editor. Script này sẽ có dạng tương tự như sau:

    ::

        @tool
        extends EditorPlugin

        # Một class member dùng để lưu editor export plugin trong suốt vòng đời của plugin.
        var export_plugin : AndroidExportPlugin

        func _enter_tree():
            # Phần khởi tạo plugin được thực hiện ở đây.
            export_plugin = AndroidExportPlugin.new()
            add_export_plugin(export_plugin)


        func _exit_tree():
            # Phần dọn dẹp plugin được thực hiện ở đây.
            remove_export_plugin(export_plugin)
            export_plugin = null


        class AndroidExportPlugin extends EditorExportPlugin:
            # Tên của plugin.
            var _plugin_name = "<plugin_name>"

            # Chỉ định platform nào được plugin hỗ trợ.
            func _supports_platform(platform):
                if platform is EditorExportPlatformAndroid:
                    return true
                return false

            # Trả về các path của binary AAR của plugin, tính tương đối so với thư mục 'addons'.
            func _get_android_libraries(platform, debug):
                if debug:
                    return PackedStringArray(["<paths_to_debug_android_plugin_aar_binaries>"])
                else:
                    return PackedStringArray(["<paths_to_release_android_plugin_aar_binaries>"])

            # Trả về tên của plugin.
            func _get_name():
                return _plugin_name


    - Sau đây là tập hợp các `EditorExportPlugin APIs <https://docs.godotengine.org/en/stable/classes/class_editorexportplugin.html>`_ phù hợp nhất để sử dụng trong tool script này:

        - | `_supports_platform <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-supports-platform>`_: | Trả về ``true`` nếu plugin hỗ trợ platform đã cho. Đối với plugin Android, giá trị này phải trả về ``true`` khi ``platform`` là `EditorExportPlatformAndroid <https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html>`_ - | `_get_android_libraries <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-libraries>`_: | Lấy các path cục bộ của binary Android library (file AAR) do plugin cung cấp - | `_get_android_dependencies <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies>`_: | Lấy tập hợp các Android maven dependency (ví dụ: `org.godot.example:my-plugin:0.0.0`) provided by the plugin - | `_get_android_dependencies_maven_repos <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies-maven-repos>`_: | Retrieve the urls of the maven repos for the android dependencies provided by ``_get_android_dependencies`` - | `_get_android_manifest_activity_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-activity-element-contents>`_: | Update the contents of the ``<activity>`` element in the generated Android manifest - | `_get_android_manifest_application_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-application-element-contents>`_: | Update the contents of the ``<application>`` element in the generated Android manifest - | `_get_android_manifest_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-element-contents>`_: | Cập nhật nội dung của phần tử ``<manifest>`` trong Android manifest được tạo

      Các method ``_get_android_manifest_*`` cho phép plugin tự động cung cấp các thay đổi cho manifest của app. Những thay đổi này được giữ lại khi Godot Editor được cập nhật, giải quyết một vấn đề tồn tại lâu năm với plugin Android v1.


3. Tạo một ``plugin.cfg``. Đây là file INI chứa metadata về plugin của bạn:

::

      [plugin]

      name="<plugin_name>"
      description="<plugin_description>"
      author="<plugin_author>"
      version="<plugin_version>"
      script="<relative_path_to_the_export_tool_script>"

Để tham khảo, dưới đây là `folder structure for the Godot Android plugin project template <https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_. Khi build, nội dung của thư mục ``export_scripts_template`` cũng như các binary plugin được tạo sẽ được sao chép vào thư mục ``addons/<plugin_name>``:

.. code-block:: none

    export_scripts_template/
    |
    +--export_plugin.gd         # export plugin tool script
    |
    +--plugin.cfg               # plugin INI file


Đóng gói plugin Android v2 với khả năng GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đối với GDExtension, chúng ta thực hiện các bước tương tự như với `Đóng gói plugin Android v2`_ và thêm `GDExtension config file <https://docs.godotengine.org/en/stable/tutorials/scripting/cpp/gdextension_cpp_example.html#using-the-gdextension-module>`_ vào cùng vị trí với ``plugin.cfg``.

Để tham khảo, dưới đây là `folder structure for the GDExtension Android plugin project template <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_. Khi build, nội dung của thư mục ``export_scripts_template`` cũng như các binary plugin được tạo sẽ được sao chép vào thư mục ``addons/<plugin_name>``:

.. code-block:: none

    export_scripts_template/
    |
    +--export_plugin.gd         # export plugin tool script
    |
    +--plugin.cfg               # plugin INI file
    |
    +--plugin.gdextension       # GDExtension config file


Dưới đây là cấu hình ``plugin.gdextension`` sẽ trông như thế nào:

::

    [configuration]

    entry_symbol = "plugin_library_init"
    compatibility_minimum = "4.2"
    android_aar_plugin = true

    [libraries]

    android.debug.arm64 = "res://addons/GDExtensionAndroidPluginTemplate/bin/debug/arm64-v8a/libGDExtensionAndroidPluginTemplate.so"
    android.release.arm64 = "res://addons/GDExtensionAndroidPluginTemplate/bin/release/arm64-v8a/libGDExtensionAndroidPluginTemplate.so"
    ...


Đáng chú ý là field ``android_aar_plugin``, chỉ định rằng module GDExtension này được cung cấp như một phần của plugin Android v2. Trong quá trình export, thông tin này sẽ cho Godot Editor biết rằng các native shared library GDExtension được export bởi các binary Android plugin AAR.

Đối với plugin Android GDExtension, init class của plugin phải override `GodotPlugin::getPluginGDExtensionLibrariesPaths() <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L277>`_ và trả về các path đến các file cấu hình thư viện GDExtension đi kèm (``*.gdextension``).

Các path phải tương đối so với thư mục ``assets`` của Android library. Khi runtime, plugin sẽ cung cấp các path này cho Godot engine, engine sẽ sử dụng chúng để load và initialize các thư viện GDExtension đi kèm.

Sử dụng plugin Android v2
-------------------------

.. note::

    - Yêu cầu Godot 4.2 trở lên

    - Plugin Android v2 yêu cầu sử dụng `Gradle build process <https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html#class-editorexportplatformandroid-property-gradle-build-use-gradle-build>`_.

    - Các template dự án github được cung cấp bao gồm các dự án Godot demo để kiểm thử nhanh.


1. Sao chép thư mục đầu ra của plugin (``addons/<plugin_name>``) vào thư mục của dự án Godot đích

2. Mở dự án trong Godot Editor; Editor sẽ tự động phát hiện plugin

3. Đi đến ``Project`` -> ``Project Settings...`` -> ``Plugins``, và đảm bảo plugin đã được bật

4. Cài đặt template build Android của Godot bằng cách nhấp vào ``Project`` -> ``Install Android Build Template...``

5. Đi đến ``Project`` -> ``Export...``

6. Trong cửa sổ ``Export``, tạo một ``Android export preset``

7. Trong ``Android export preset``, cuộn đến ``Gradle Build`` và đặt ``Use Gradle Build`` thành ``true``

8. Cập nhật các script của dự án khi cần để truy cập chức năng của plugin. Ví dụ:

::

    if Engine.has_singleton("MyPlugin"):
            var singleton = Engine.get_singleton("MyPlugin")
            print(singleton.myPluginFunction("World"))

9. Kết nối thiết bị Android với máy của bạn và chạy dự án trên thiết bị đó


Sử dụng plugin Android v2 làm thư viện Android
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vì cũng là các thư viện Android, plugin Android v2 của Godot có thể được loại bỏ khỏi gói ``EditorExportPlugin`` và cung cấp dưới dạng các binary ``AAR`` thô để sử dụng làm thư viện cùng với :ref:`Godot Android library <doc_android_library>` bởi các ứng dụng Android.

Nếu hướng đến trường hợp sử dụng này, hãy nhớ bổ sung hướng dẫn về cách đưa các binary ``AAR`` vào (ví dụ: các bổ sung tùy chỉnh cho manifest của ứng dụng Android).

Các triển khai tham chiếu
-------------------------

- `Godot Android Plugins Samples <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/plugins>`_ - `Godot Android Plugin Template <https://github.com/m4gr3d/Godot-Android-Plugin-Template>`_ - `GDExtension Android Plugin Template <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template>`_ - `Godot OpenXR Loaders <https://github.com/GodotVR/godot_openxr_loaders>`_


Mẹo và hướng dẫn
----------------

Đơn giản hóa việc truy cập các API Java / Kotlin được công khai
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để giúp việc truy cập các API Java / Kotlin được công khai trong Godot Editor dễ dàng hơn, bạn nên cung cấp một (hoặc nhiều) class wrapper gdscript để người dùng plugin tương tác với các API này.

Ví dụ:

::

    class_name PluginInterface extends Object

    ## Interface dùng để truy cập chức năng do plugin này cung cấp.

    var _plugin_name = "GDExtensionAndroidPluginTemplate"
    var _plugin_singleton

    func _init():
        if Engine.has_singleton(_plugin_name):
            _plugin_singleton = Engine.get_singleton(_plugin_name)
        else:
            printerr("Initialization error: unable to access the java logic")

    ## In thông báo 'Hello World' vào logcat.
    func helloWorld():
        if _plugin_singleton:
            _plugin_singleton.helloWorld()
        else:
            printerr("Initialization error")

Hỗ trợ sử dụng chức năng GDExtension trong Godot Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu dự định sử dụng chức năng GDExtension trong Godot Editor, bạn nên biên dịch các binary native của GDExtension không chỉ cho Android mà còn cho hệ điều hành mà các developer / người dùng dự định chạy Godot Editor trên đó. Nếu không làm vậy, developer / người dùng có thể không viết được code truy cập plugin từ bên trong Godot Editor.

Điều này có thể bao gồm việc tạo các plugin giả cho hệ điều hành máy chủ chỉ để API được công khai với editor. Bạn có thể sử dụng template github `godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__ để tham khảo cách thực hiện.

Các kiểu dữ liệu được hỗ trợ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tất cả kiểu dữ liệu đều được hỗ trợ. Các kiểu phổ biến được ánh xạ sang các kiểu tương đương của Godot (ví dụ: ``String[]`` được ánh xạ sang ``PackedStringArray()``), nhưng với các kiểu khác, bạn có thể sử dụng `JavaClassWrapper <https://docs.godotengine.org/en/stable/tutorials/platform/android/javaclasswrapper_and_androidruntimeplugin.html#javaclasswrapper-godot-singleton>`_ để truy cập chúng.

Godot bị crash khi tải
~~~~~~~~~~~~~~~~~~~~~~

Kiểm tra `adb logcat <https://developer.android.com/tools/logcat>`_ để tìm các vấn đề có thể xảy ra.
