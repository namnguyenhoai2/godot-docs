.. _doc_android_plugin:

Plugin Android của Godot
========================

Giới thiệu
----------

Plugin Android là các công cụ mạnh mẽ giúp mở rộng khả năng của engine Godot bằng cách tận dụng chức năng do các nền tảng và hệ sinh thái Android cung cấp.

Ví dụ, trong Godot 4, plugin Android được dùng để hỗ trợ nhiều nền tảng XR dựa trên Android mà không làm mã nguồn lõi trở nên cồng kềnh với mã hoặc tệp nhị phân đặc thù của từng nhà cung cấp.

Plugin Android
--------------

**Phiên bản 1 (v1)** của hệ thống plugin Android được giới thiệu trong Godot 3 và tương thích với Godot 4.0 và 4.1. Phiên bản này cho phép các nhà phát triển bổ sung chức năng Java, Kotlin và native vào engine Godot.

Bắt đầu từ Godot 4.2, các plugin Android được xây dựng trên kiến trúc v1 hiện đã không còn được khuyến nghị. Thay vào đó, Godot 4.2 giới thiệu kiến trúc **Phiên bản 2 (v2)** mới cho plugin Android.

Kiến trúc v2
~~~~~~~~~~~~

.. note::

    Plugin Android của Godot tận dụng :ref:`hệ thống build Gradle <doc_android_gradle_build>`.


Dựa trên kiến trúc v1 trước đây, plugin Android tiếp tục được xây dựng từ `thư viện lưu trữ Android <https://developer.android.com/studio/projects/android-library#aar-contents>`_.

Về cốt lõi, plugin Android v2 của Godot là một thư viện Android có phụ thuộc vào :ref:`thư viện Android của Godot <doc_android_library>` và một tệp manifest thư viện Android tùy chỉnh.

Kiến trúc này cho phép plugin Android mở rộng chức năng của engine bằng:

- API nền tảng Android
- Thư viện Android
- Thư viện Kotlin và Java
- Thư viện native (thông qua JNI)
- Thư viện GDExtension

Mỗi plugin có một lớp init kế thừa từ lớp `GodotPlugin <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L80>`_, được cung cấp bởi :ref:`thư viện Android của Godot <doc_android_library>`.

``GodotPlugin`` lớp này cung cấp các API để truy cập instance Godot đang chạy và hook vào vòng đời của nó. Engine Godot tải lớp này trong runtime.

Định dạng đóng gói v2
~~~~~~~~~~~~~~~~~~~~~

Plugin Android v1 yêu cầu một tệp cấu hình ``gdap`` tùy chỉnh, được Godot Editor dùng để phát hiện và tải plugin. Tuy nhiên, cách tiếp cận này có một số hạn chế, trong đó quan trọng nhất là thiếu tính linh hoạt và khác với `định dạng, quy trình cung cấp và cài đặt hiện có của Godot EditorExportPlugin <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/installing_plugins.html>`_.

Vấn đề này đã được giải quyết đối với các plugin Android v2 bằng cách loại bỏ dần cơ chế đóng gói và cấu hình ``gdap``, thay thế bằng định dạng đóng gói plugin Godot ``EditorExportPlugin`` hiện có. API ``EditorExportPlugin`` cũng đã được mở rộng để hỗ trợ đầy đủ các plugin Android.


Xây dựng plugin Android v2
--------------------------

Một mẫu dự án github **được cung cấp** tại https://github.com/m4gr3d/Godot-Android-Plugin-Template dưới dạng **quickstart để xây dựng plugin Android của Godot cho Godot 4.2+**. Bạn có thể làm theo `README của mẫu plugin Android <https://github.com/m4gr3d/Godot-Android-Plugin-Template#readme>`_ để thiết lập dự án plugin Android của Godot riêng.

Để hiểu rõ hơn, dưới đây là phần phân tích các bước được dùng để tạo mẫu dự án:

1. Tạo một module thư viện Android bằng cách làm theo `các hướng dẫn này <https://developer.android.com/studio/projects/android-library>`_.

2. Thêm thư viện Android của Godot làm dependency bằng cách cập nhật ``gradle`` `tệp build <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/build.gradle.kts#L42>`_ của module:

    .. code:: text

        dependencies {
            implementation("org.godotengine:godot:4.2.0.stable")
        }

  Thư viện Android của Godot được `lưu trữ trên MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_ và được cập nhật theo mỗi bản phát hành.

3. Tạo `GodotAndroidPlugin <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/a01286b4cb459133bf07b11dfabdfd3980268797/plugin/src/main/java/org/godotengine/plugin/android/template/GodotAndroidPlugin.kt#L10>`_, một lớp init cho plugin kế thừa `GodotPlugin <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L80>`_.

    - Nếu plugin cung cấp các phương thức Kotlin hoặc Java để gọi từ GDScript, chúng phải được chú thích bằng `@UsedByGodot <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/UsedByGodot.java#L45>`_. Tên được gọi từ GDScript **phải khớp chính xác với tên phương thức**. Không có **sự** chuyển đổi kiểu ``snake_case`` sang ``camelCase``. Ví dụ, từ GDScript:

        ::

            if Engine.has_singleton("MyPlugin"):
                var singleton = Engine.get_singleton("MyPlugin")
                print(singleton.myPluginFunction("World"))

    - Nếu plugin sử dụng `signal <https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html>`_, lớp init phải trả về tập hợp các signal được sử dụng bằng cách ghi đè `GodotPlugin::getPluginSignals() <https://github.com/godotengine/godot/blob/fa3428ff25bc577d2a3433090478a6d615567056/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L302>`_. Để phát signal, plugin có thể sử dụng `phương thức GodotPlugin::emitSignal(...) <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L317>`_.

4. Cập nhật ``AndroidManifest.xml`` `tệp <https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/src/main/AndroidManifest.xml>`_ của plugin với siêu dữ liệu sau:

    .. code-block:: xml

        <meta-data
            android:name="org.godotengine.plugin.v2.[PluginName]"
            android:value="[plugin.init.ClassFullName]" />


  Trong đó:

      - ``PluginName`` là tên của plugin
      - ``plugin.init.ClassFullName`` là tên component đầy đủ (tên package + tên class) của lớp init plugin (ví dụ: ``org.godotengine.plugin.android.template.GodotAndroidPlugin``).

5. Tạo `cấu hình EditorExportPlugin <https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_ để đóng gói plugin. Các bước tạo cấu hình có thể xem trong phần `Đóng gói plugin Android v2 <Packaging a v2 Android plugin_>`_.


Xây dựng plugin Android v2 với khả năng GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tương tự như hỗ trợ GDNative trong plugin Android v1, plugin Android v2 hỗ trợ tích hợp các khả năng GDExtension.

Một mẫu dự án github được cung cấp tại https://github.com/m4gr3d/GDExtension-Android-Plugin-Template dưới dạng quickstart để xây dựng plugin Android GDExtension cho Godot 4.2+. Bạn có thể làm theo `README của mẫu GDExtension <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template#readme>`_ để thiết lập dự án plugin Android của Godot riêng.


Di chuyển plugin Android v1 sang v2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hãy thực hiện các bước sau nếu bạn có plugin Android v1 muốn di chuyển sang v2:

1. Cập nhật tệp manifest của plugin:

    - Đổi tiền tố ``org.godotengine.plugin.v1`` thành ``org.godotengine.plugin.v2``

2. Cập nhật dependency build của thư viện Android Godot:

    - Bạn có thể tiếp tục sử dụng ``godot-lib.<version>.<status>.aar`` tệp nhị phân từ `trang tải xuống của Godot <https://godotengine.org/download>`_ nếu muốn. Hãy đảm bảo tệp được cập nhật lên phiên bản ổn định mới nhất.
    - Hoặc bạn có thể chuyển sang dependency do MavenCentral cung cấp:

::

    dependencies {
        implementation("org.godotengine:godot:4.2.0.stable")
    }

3. Sau khi cập nhật dependency của thư viện Android Godot, hãy đồng bộ hoặc build plugin và khắc phục mọi lỗi biên dịch:

    - Instance ``Godot`` do ``GodotPlugin::getGodot()`` cung cấp hiện không còn quyền truy cập vào tham chiếu ``android.content.Context`` nữa. Thay vào đó, hãy sử dụng ``GodotPlugin::getActivity()``.

4. Xóa các tệp cấu hình ``gdap`` và làm theo hướng dẫn trong phần `Đóng gói plugin Android v2 <Packaging a v2 Android plugin_>`_ để thiết lập cấu hình plugin.

.. _`Packaging a v2 Android plugin`:

Đóng gói plugin Android v2
--------------------------

Như đã đề cập, plugin Android v2 hiện được cung cấp cho Godot Editor dưới dạng ``EditorExportPlugin`` plugin, vì vậy nó dùng chung nhiều `bước đóng gói <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#creating-a-plugin>`_.

1. Thêm các binary đầu ra của plugin vào trong thư mục plugin (ví dụ: trong ``addons/<plugin_name>/``)

2. Thêm `script công cụ <https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#the-script-file>`_ cho chức năng export vào trong thư mục plugin (ví dụ: trong ``addons/<plugin_name>/``)

    - Script được tạo phải là script ``@tool``, nếu không script sẽ không hoạt động đúng cách
    - Script công cụ export được dùng để cấu hình plugin Android và tích hợp plugin vào quy trình export của Godot Editor. Script này sẽ có dạng tương tự như sau:

    ::

        @tool
        extends EditorPlugin

        # Biến thành viên dùng để lưu editor export plugin trong suốt vòng đời của plugin.
        var export_plugin : AndroidExportPlugin

        func _enter_tree():
            # Phần khởi tạo plugin được đặt tại đây.
            export_plugin = AndroidExportPlugin.new()
            add_export_plugin(export_plugin)


        func _exit_tree():
            # Phần dọn dẹp plugin được đặt tại đây.
            remove_export_plugin(export_plugin)
            export_plugin = null


        class AndroidExportPlugin extends EditorExportPlugin:
            # Tên của plugin.
            var _plugin_name = "<plugin_name>"

            # Chỉ định nền tảng được plugin hỗ trợ.
            func _supports_platform(platform):
                if platform is EditorExportPlatformAndroid:
                    return true
                return false

            # Trả về các đường dẫn đến binary AAR của plugin, tương đối với thư mục 'addons'.
            func _get_android_libraries(platform, debug):
                if debug:
                    return PackedStringArray(["<paths_to_debug_android_plugin_aar_binaries>"])
                else:
                    return PackedStringArray(["<paths_to_release_android_plugin_aar_binaries>"])

            # Trả về tên của plugin.
            func _get_name():
                return _plugin_name


    - Sau đây là các API `EditorExportPlugin <https://docs.godotengine.org/en/stable/classes/class_editorexportplugin.html>`_ phù hợp nhất để sử dụng trong script công cụ này:

        - | `_supports_platform <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-supports-platform>`_:
          | Trả về ``true`` nếu plugin hỗ trợ nền tảng được chỉ định. Đối với các plugin Android, giá trị này phải là ``true`` khi ``platform`` là `EditorExportPlatformAndroid <https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html>`_
        - | `_get_android_libraries <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-libraries>`_:
          | Lấy các đường dẫn cục bộ của binary thư viện Android (tệp AAR) do plugin cung cấp
        - | `_get_android_dependencies <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies>`_:
          | Lấy tập hợp các dependency maven của Android (ví dụ: `org.godot.example:my-plugin:0.0.0`) do plugin cung cấp
        - | `_get_android_dependencies_maven_repos <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies-maven-repos>`_:
          | Lấy các URL của các repo maven dành cho các dependency Android do ``_get_android_dependencies`` cung cấp
        - | `_get_android_manifest_activity_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-activity-element-contents>`_:
          | Cập nhật nội dung của phần tử ``<activity>`` trong Android manifest được tạo
        - | `_get_android_manifest_application_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-application-element-contents>`_:
          | Cập nhật nội dung của phần tử ``<application>`` trong Android manifest được tạo
        - | `_get_android_manifest_element_contents <https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-element-contents>`_:
          | Cập nhật nội dung của phần tử ``<manifest>`` trong Android manifest được tạo

      Các phương thức ``_get_android_manifest_*`` cho phép plugin tự động cung cấp các thay đổi cho manifest của ứng dụng. Những thay đổi này được giữ lại khi Godot Editor được cập nhật, giải quyết một vấn đề tồn tại lâu nay với các plugin Android v1.


3. Tạo một ``plugin.cfg``. Đây là tệp INI chứa metadata về plugin của bạn:

::

      [plugin]

      name="<plugin_name>"
      description="<plugin_description>"
      author="<plugin_author>"
      version="<plugin_version>"
      script="<relative_path_to_the_export_tool_script>"

Để tham khảo, sau đây là `cấu trúc thư mục cho template dự án plugin Android của Godot <https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_. Khi build, nội dung của thư mục ``export_scripts_template`` cùng với các binary plugin được tạo sẽ được sao chép vào thư mục ``addons/<plugin_name>``:

.. code-block:: none

    export_scripts_template/
    |
    +--export_plugin.gd         # export plugin tool script
    |
    +--plugin.cfg               # plugin INI file


Đóng gói plugin Android v2 với các khả năng GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đối với GDExtension, chúng ta thực hiện các bước tương tự như khi `Đóng gói plugin Android v2 <Packaging a v2 Android plugin_>`_ và thêm `tệp cấu hình GDExtension <https://docs.godotengine.org/en/stable/tutorials/scripting/cpp/gdextension_cpp_example.html#using-the-gdextension-module>`_ vào cùng vị trí với ``plugin.cfg``.

Để tham khảo, sau đây là `cấu trúc thư mục cho template dự án plugin Android GDExtension <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template/tree/main/plugin/export_scripts_template>`_. Khi build, nội dung của thư mục ``export_scripts_template`` cùng với các binary plugin được tạo sẽ được sao chép vào thư mục ``addons/<plugin_name>``:

.. code-block:: none

    export_scripts_template/
    |
    +--export_plugin.gd         # export plugin tool script
    |
    +--plugin.cfg               # plugin INI file
    |
    +--plugin.gdextension       # GDExtension config file


Sau đây là dạng mà tệp cấu hình ``plugin.gdextension`` nên có:

::

    [configuration]

    entry_symbol = "plugin_library_init"
    compatibility_minimum = "4.2"
    android_aar_plugin = true

    [libraries]

    android.debug.arm64 = "res://addons/GDExtensionAndroidPluginTemplate/bin/debug/arm64-v8a/libGDExtensionAndroidPluginTemplate.so"
    android.release.arm64 = "res://addons/GDExtensionAndroidPluginTemplate/bin/release/arm64-v8a/libGDExtensionAndroidPluginTemplate.so"
    ...


Đáng chú ý là trường ``android_aar_plugin``, trường này chỉ định rằng module GDExtension này được cung cấp như một phần của plugin Android v2. Trong quá trình export, thông tin này sẽ cho Godot Editor biết rằng các shared library native của GDExtension được export bởi các binary AAR của plugin Android.

Đối với các plugin Android GDExtension, lớp init của plugin phải override `GodotPlugin::getPluginGDExtensionLibrariesPaths() <https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L277>`_ và trả về các đường dẫn đến các tệp cấu hình thư viện GDExtension đi kèm (``*.gdextension``).

Các đường dẫn phải tương đối so với thư mục ``assets`` của thư viện Android. Khi runtime, plugin sẽ cung cấp các đường dẫn này cho Godot engine, engine sẽ dùng chúng để tải và khởi tạo các thư viện GDExtension đi kèm.

Sử dụng plugin Android v2
-------------------------

.. note::

    - Yêu cầu Godot 4.2 trở lên

    - Plugin Android v2 yêu cầu sử dụng `quy trình build Gradle <https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html#class-editorexportplatformandroid-property-gradle-build-use-gradle-build>`_.

    - Các template dự án github được cung cấp bao gồm các dự án Godot demo để kiểm thử nhanh.


1. Sao chép thư mục đầu ra của plugin (``addons/<plugin_name>``) vào thư mục của dự án Godot đích

2. Mở dự án trong Godot Editor; Editor sẽ tự phát hiện plugin

3. Đi đến ``Project`` -> ``Project Settings...`` -> ``Plugins`` và đảm bảo plugin đã được bật

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

Vì cũng là các thư viện Android, plugin Android v2 của Godot có thể được loại bỏ phần đóng gói ``EditorExportPlugin`` và cung cấp dưới dạng các binary ``AAR`` thô để các ứng dụng Android sử dụng làm thư viện cùng với :ref:`thư viện Android của Godot <doc_android_library>`.

Nếu nhắm đến trường hợp sử dụng này, hãy đảm bảo bổ sung hướng dẫn về cách đưa các tệp nhị phân ``AAR`` vào (ví dụ: thêm tùy chỉnh vào manifest của ứng dụng Android).

Các triển khai tham khảo
------------------------

- `Mẫu Godot Android Plugins <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/plugins>`_
- `Mẫu Godot Android Plugin <https://github.com/m4gr3d/Godot-Android-Plugin-Template>`_
- `Mẫu GDExtension Android Plugin <https://github.com/m4gr3d/GDExtension-Android-Plugin-Template>`_
- `Godot OpenXR Loaders <https://github.com/GodotVR/godot_openxr_loaders>`_


Mẹo và hướng dẫn
----------------

Đơn giản hóa việc truy cập các API Java / Kotlin được cung cấp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để việc truy cập các API Java / Kotlin được cung cấp trong Godot Editor dễ dàng hơn, bạn nên cung cấp một hoặc nhiều lớp wrapper gdscript để người dùng plugin tương tác với chúng.

Ví dụ:

::

    class_name PluginInterface extends Object

    ## Interface used to access the functionality provided by this plugin.

    var _plugin_name = "GDExtensionAndroidPluginTemplate"
    var _plugin_singleton

    func _init():
        if Engine.has_singleton(_plugin_name):
            _plugin_singleton = Engine.get_singleton(_plugin_name)
        else:
            printerr("Initialization error: unable to access the java logic")

    ## Print a 'Hello World' message to the logcat.
    func helloWorld():
        if _plugin_singleton:
            _plugin_singleton.helloWorld()
        else:
            printerr("Initialization error")

Hỗ trợ sử dụng chức năng GDExtension trong Godot Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu dự định sử dụng chức năng GDExtension trong Godot Editor, bạn nên biên dịch các tệp nhị phân native của GDExtension không chỉ cho Android mà còn cho hệ điều hành mà các nhà phát triển / người dùng dự định chạy Godot Editor trên đó. Nếu không làm vậy, các nhà phát triển / người dùng có thể không viết được mã truy cập plugin từ bên trong Godot Editor.

Điều này có thể bao gồm việc tạo các plugin giả cho hệ điều hành máy chủ chỉ để API được cung cấp cho editor. Bạn có thể tham khảo template github `godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__ để biết cách thực hiện.

Các kiểu dữ liệu được hỗ trợ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tất cả các kiểu dữ liệu đều được hỗ trợ. Các kiểu phổ biến được ánh xạ sang các kiểu tương đương trong Godot (ví dụ: ``String[]`` được ánh xạ sang ``PackedStringArray()``), nhưng với các kiểu khác, bạn có thể sử dụng `JavaClassWrapper <https://docs.godotengine.org/en/stable/tutorials/platform/android/javaclasswrapper_and_androidruntimeplugin.html#javaclasswrapper-godot-singleton>`_ để truy cập chúng.

Godot gặp sự cố khi tải
~~~~~~~~~~~~~~~~~~~~~~~

Kiểm tra `adb logcat <https://developer.android.com/tools/logcat>`_ để tìm các vấn đề có thể xảy ra.

.. _`Android archive library`: https://developer.android.com/studio/projects/android-library#aar-contents
.. _`GodotPlugin`: https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L80
.. _`existing Godot EditorExportPlugin format, delivery and installation flow`: https://docs.godotengine.org/en/stable/tutorials/plugins/editor/installing_plugins.html
.. _`template README`: https://github.com/m4gr3d/Godot-Android-Plugin-Template#readme
.. _`these instructions`: https://developer.android.com/studio/projects/android-library
.. _`build file`: https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/build.gradle.kts#L42
.. _`hosted on MavenCentral`: https://central.sonatype.com/artifact/org.godotengine/godot
.. _`GodotAndroidPlugin`: https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/a01286b4cb459133bf07b11dfabdfd3980268797/plugin/src/main/java/org/godotengine/plugin/android/template/GodotAndroidPlugin.kt#L10
.. _`@UsedByGodot`: https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/UsedByGodot.java#L45
.. _`signals`: https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html
.. _`GodotPlugin::getPluginSignals()`: https://github.com/godotengine/godot/blob/fa3428ff25bc577d2a3433090478a6d615567056/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L302
.. _`GodotPlugin::emitSignal(...) method`: https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L317
.. _`file`: https://github.com/m4gr3d/Godot-Android-Plugin-Template/blob/main/plugin/src/main/AndroidManifest.xml
.. _`EditorExportPlugin configuration`: https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template
.. _`template's README`: https://github.com/m4gr3d/GDExtension-Android-Plugin-Template#readme
.. _`Godot's download page`: https://godotengine.org/download
.. _`same packaging steps`: https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#creating-a-plugin
.. _`tool script`: https://docs.godotengine.org/en/stable/tutorials/plugins/editor/making_plugins.html#the-script-file
.. _`EditorExportPlugin APIs`: https://docs.godotengine.org/en/stable/classes/class_editorexportplugin.html
.. _`_supports_platform`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-supports-platform
.. _`EditorExportPlatformAndroid`: https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html
.. _`_get_android_libraries`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-libraries
.. _`_get_android_dependencies`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies
.. _`_get_android_dependencies_maven_repos`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-dependencies-maven-repos
.. _`_get_android_manifest_activity_element_contents`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-activity-element-contents
.. _`_get_android_manifest_application_element_contents`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-application-element-contents
.. _`_get_android_manifest_element_contents`: https://docs.godotengine.org/en/latest/classes/class_editorexportplugin.html#class-editorexportplugin-method-get-android-manifest-element-contents
.. _`folder structure for the Godot Android plugin project template`: https://github.com/m4gr3d/Godot-Android-Plugin-Template/tree/main/plugin/export_scripts_template
.. _`GDExtension config file`: https://docs.godotengine.org/en/stable/tutorials/scripting/cpp/gdextension_cpp_example.html#using-the-gdextension-module
.. _`folder structure for the GDExtension Android plugin project template`: https://github.com/m4gr3d/GDExtension-Android-Plugin-Template/tree/main/plugin/export_scripts_template
.. _`GodotPlugin::getPluginGDExtensionLibrariesPaths()`: https://github.com/godotengine/godot/blob/0a7f75ec7b465604b6496c8f5f1d638aed250d6d/platform/android/java/lib/src/org/godotengine/godot/plugin/GodotPlugin.java#L277
.. _`Gradle build process`: https://docs.godotengine.org/en/stable/classes/class_editorexportplatformandroid.html#class-editorexportplatformandroid-property-gradle-build-use-gradle-build
.. _`Godot Android Plugins Samples`: https://github.com/m4gr3d/Godot-Android-Samples/tree/master/plugins
.. _`Godot Android Plugin Template`: https://github.com/m4gr3d/Godot-Android-Plugin-Template
.. _`GDExtension Android Plugin Template`: https://github.com/m4gr3d/GDExtension-Android-Plugin-Template
.. _`Godot OpenXR Loaders`: https://github.com/GodotVR/godot_openxr_loaders
.. _`JavaClassWrapper`: https://docs.godotengine.org/en/stable/tutorials/platform/android/javaclasswrapper_and_androidruntimeplugin.html#javaclasswrapper-godot-singleton
.. _`adb logcat`: https://developer.android.com/tools/logcat
