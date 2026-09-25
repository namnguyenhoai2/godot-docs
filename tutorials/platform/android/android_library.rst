.. _doc_android_library:

Thư viện Godot Android
======================

Godot Engine dành cho các nền tảng Android được thiết kế để sử dụng như một `thư viện Android <https://developer.android.com/studio/projects/android-library>`_. Kiến trúc này hỗ trợ một số tính năng quan trọng trên các nền tảng Android:

- Khả năng tích hợp hệ thống build Gradle vào Godot Editor, cho phép tận dụng thêm nhiều thành phần từ hệ sinh thái Android như thư viện và công cụ

- Khả năng giúp engine có tính di động và có thể nhúng:

  - Then chốt trong việc hỗ trợ port Godot Editor sang các thiết bị Android và XR di động
  - Then chốt trong việc cho phép tích hợp và tái sử dụng các khả năng của Godot trong codebase hiện có

Dưới đây, chúng tôi mô tả một số trường hợp sử dụng và tình huống mà kiến trúc này hỗ trợ.

Sử dụng thư viện Godot Android
------------------------------

Thư viện Godot Android được đóng gói dưới dạng tệp lưu trữ AAR và được lưu trữ trên `MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_ cùng với `tài liệu của nó <https://javadoc.io/doc/org.godotengine/godot/latest/index.html>`_.

Thư viện này cung cấp quyền truy cập vào các API và khả năng của Godot trên nền tảng Android cho các trường hợp sử dụng không giới hạn sau đây.

Plugin Godot Android
--------------------

Plugin Android là các công cụ mạnh mẽ để mở rộng khả năng của Godot Engine bằng cách khai thác chức năng do các nền tảng và hệ sinh thái Android cung cấp.

Plugin Android là một thư viện Android phụ thuộc vào thư viện Godot Android. Plugin sử dụng thư viện này để tích hợp vào vòng đời của engine và truy cập các API Godot, nhờ đó có được các khả năng mạnh mẽ như hỗ trợ GDExtension, cho phép cập nhật / sửa đổi hành vi của engine khi cần.

Để biết thêm thông tin, hãy xem :ref:`plugin Godot Android <doc_android_plugin>`.

Nhúng Godot vào các dự án Android hiện có
-----------------------------------------

Godot Engine có thể được nhúng vào các ứng dụng hoặc thư viện Android hiện có, cho phép nhà phát triển tận dụng code và thư viện đã trưởng thành, được kiểm chứng kỹ lưỡng, phù hợp hơn với một tác vụ cụ thể.

Thành phần host chịu trách nhiệm điều khiển vòng đời của engine thông qua các API Android của Godot. Các API này cũng có thể được dùng để cung cấp giao tiếp hai chiều giữa host và thực thể Godot được nhúng, giúp kiểm soát tốt hơn trải nghiệm mong muốn.

Chúng tôi minh họa cách thực hiện việc này bằng một ứng dụng Android mẫu nhúng Godot Engine dưới dạng Android view và dùng nó để render các mô hình glTF 3D.

Ứng dụng mẫu `GLTF Viewer <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer>`_ sử dụng `thành phần Android RecyclerView <https://developer.android.com/develop/ui/views/layout/recyclerview>`_ để tạo danh sách các mục glTF, được nạp từ `gói Food Kit của Kenney <https://kenney.nl/assets/food-kit>`_. Khi một mục trong danh sách được chọn, logic của ứng dụng tương tác với Godot Engine được nhúng để render mục glTF đã chọn dưới dạng mô hình 3D.

.. image:: img/gltf_viewer_sample_app_screenshot.webp

Bạn có thể tìm mã nguồn của ứng dụng mẫu `trên GitHub <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer>`_. Hãy làm theo hướng dẫn trong `README của ứng dụng <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md>`_ để build và cài đặt ứng dụng.

Dưới đây, chúng tôi phân tích các bước được dùng để tạo ứng dụng GLTF Viewer.

.. warning::

  Hiện tại, mỗi process chỉ hỗ trợ một thực thể Godot Engine. Bạn có thể cấu hình process mà Android Activity chạy trong đó bằng `thuộc tính android:process <https://developer.android.com/guide/topics/manifest/activity-element#proc>`_.

.. warning::

  Các sự kiện cấu hình tự động thay đổi kích thước / hướng không được hỗ trợ và có thể gây crash. Bạn có thể vô hiệu hóa các sự kiện đó:

  - Khóa ở một hướng cụ thể bằng `thuộc tính android:screenOrientation <https://developer.android.com/guide/topics/manifest/activity-element#screen>`_.
  - Khai báo rằng Activity sẽ xử lý các sự kiện cấu hình này bằng `thuộc tính android:configChanges <https://developer.android.com/guide/topics/manifest/activity-element#config>`_.

1. Tạo ứng dụng Android
~~~~~~~~~~~~~~~~~~~~~~~

.. note::

  Ứng dụng Android mẫu được tạo bằng `Android Studio <https://developer.android.com/studio>`_ và sử dụng `Gradle <https://developer.android.com/build>`_ làm hệ thống build.

  Hệ sinh thái Android cung cấp nhiều công cụ, IDE và hệ thống build để tạo ứng dụng Android, vì vậy bạn cứ thoải mái dùng những gì quen thuộc và điều chỉnh các bước bên dưới cho phù hợp (các đóng góp cho tài liệu này cũng rất được hoan nghênh!).


- Thiết lập một dự án ứng dụng Android. Đây có thể là một dự án trống hoàn toàn mới hoặc một dự án hiện có
- Thêm `dependency maven cho thư viện Godot Android <https://central.sonatype.com/artifact/org.godotengine/godot>`_

  - Nếu sử dụng ``gradle``, hãy thêm nội dung sau vào phần ``dependency`` trong tệp build gradle của ứng dụng. Hãy đảm bảo cập nhật ``<version>`` lên phiên bản mới nhất của thư viện Godot Android:

  .. code-block:: kotlin

    implementation("org.godotengine:godot:<version>")

- Nếu sử dụng ``gradle``, hãy thêm cấu hình ``aaptOptions`` sau vào phần ``android > defaultConfig`` trong tệp build gradle của ứng dụng. Việc này cho phép ``gradle`` bao gồm các thư mục ẩn của Godot khi build binary của ứng dụng.

  - Nếu hệ thống build của bạn không hỗ trợ bao gồm các thư mục ẩn, bạn có thể cấu hình dự án Godot không sử dụng thư mục ẩn bằng cách bỏ chọn
    :ref:`Application > Config > Use Hidden Project Data Directory <class_ProjectSettings_property_application/config/use_hidden_project_data_directory>` trong Project Settings.

.. code-block:: groovy

  android {

    defaultConfig {
        // Mẫu bỏ qua mặc định cho thư mục 'assets' bao gồm các tệp ẩn và
        // các thư mục được dự án Godot sử dụng, vì vậy chúng tôi ghi đè mẫu này bằng nội dung sau.
        aaptOptions {
            ignoreAssetsPattern "!.svn:!.git:!.gitignore:!.ds_store:!*.scc:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
        }
      ...

- Tạo / cập nhật Activity của ứng dụng để host thực thể Godot Engine. Trong ứng dụng mẫu, đây là `MainActivity <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt>`_

  - Activity host phải triển khai `interface GodotHost <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java>`_
  - Ứng dụng mẫu sử dụng `Fragments <https://developer.android.com/guide/fragments>`_ để tổ chức UI, vì vậy ứng dụng dùng `GodotFragment <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotFragment.java>`_, một thành phần fragment do thư viện Godot Android cung cấp để tự động host và quản lý thực thể Godot Engine.

  .. code-block:: kotlin

    private var godotFragment: GodotFragment? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContentView(R.layout.activity_main)

        val currentGodotFragment = supportFragmentManager.findFragmentById(R.id.godot_fragment_container)
        if (currentGodotFragment is GodotFragment) {
            godotFragment = currentGodotFragment
        } else {
            godotFragment = GodotFragment()
            supportFragmentManager.beginTransaction()
                .replace(R.id.godot_fragment_container, godotFragment!!)
                .commitNowAllowingStateLoss()
        }

        ...

.. note::

  Thư viện Godot Android cũng cung cấp `GodotActivity <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotActivity.kt>`_, một thành phần Activity có thể được mở rộng để tự động host và quản lý thực thể Godot Engine.

  Ngoài ra, ứng dụng có thể trực tiếp tạo một thực thể `Godot <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/Godot.kt>`_, rồi tự host và quản lý thực thể đó.

- Bằng cách sử dụng `GodotHost#getHostPlugins(...) <https://github.com/m4gr3d/Godot-Android-Samples/blob/0e3440f357f8be5b4c63a4fe75766793199a99d0/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt#L55>`_, ứng dụng mẫu tạo một `thực thể GodotPlugin tại runtime <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/AppPlugin.kt>`_ để gửi các :ref:`signal <doc_signals>` đến logic ``gdscript``

  - Runtime ``GodotPlugin`` cũng có thể được logic ``gdscript`` sử dụng để truy cập các phương thức JVM. Để biết thêm thông tin, xem :ref:`plugin Android của Godot <doc_android_plugin>`.

- Thêm mọi logic bổ sung mà ứng dụng của bạn sẽ sử dụng

  - Đối với ứng dụng mẫu, việc này bao gồm thêm fragment `ItemsSelectionFragment <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/ItemsSelectionFragment.kt>`_ (và các lớp liên quan), một fragment dùng để xây dựng và hiển thị danh sách các mục glTF

- Mở tệp ``AndroidManifest.xml`` và cấu hình orientation nếu cần bằng thuộc tính `android:screenOrientation <https://developer.android.com/guide/topics/manifest/activity-element#screen>`_

  - Nếu cần, hãy tắt tính năng tự động thay đổi kích thước / thay đổi cấu hình orientation bằng thuộc tính `android:configChanges <https://developer.android.com/guide/topics/manifest/activity-element#config>`_

.. code-block:: xml

  <activity android:name=".MainActivity"
      android:screenOrientation="fullUser"
      android:configChanges="orientation|screenSize|smallestScreenSize|screenLayout"
      android:exported="true">

      ...
  </activity>


2. Tạo dự án Godot
~~~~~~~~~~~~~~~~~~

.. note::

  Trên Android, các tệp dự án của Godot được export vào thư mục ``assets`` của binary ``apk`` được tạo ra.

  Chúng ta tận dụng kiến trúc đó để liên kết ứng dụng Android và dự án Godot với nhau bằng cách tạo dự án Godot trong thư mục ``assets`` của ứng dụng Android.

  Lưu ý rằng bạn cũng có thể tạo dự án Godot trong một thư mục riêng và export nó dưới dạng `tệp PCK hoặc ZIP <https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html#pck-versus-zip-pack-file-formats>`_ vào thư mục ``assets`` của ứng dụng Android. Cách tiếp cận này yêu cầu truyền đối số ``--main-pack <pck_or_zip_filepath_relative_to_assets_dir>`` tới instance Godot Engine được host bằng `GodotHost#getCommandLine() <https://github.com/godotengine/godot/blob/6916349697a4339216469e9bf5899b983d78db07/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java#L45>`_.

  Ví dụ:

  .. code-block:: java

    @Override
    public List<String> getCommandLine(){
        List<String> results = new ArrayList<>();
        results.addAll(super.getCommandLine());
        results.add("--main-pack");
        results.add("res://foo.pck");
        return results;
    }

  Các hướng dẫn bên dưới và ứng dụng mẫu sử dụng cách tiếp cận đầu tiên là tạo dự án Godot trong thư mục ``assets`` của ứng dụng Android.


- Như đã đề cập trong **lưu ý** ở trên, hãy mở Godot Editor và tạo trực tiếp một dự án Godot (không có thư mục con) trong thư mục ``assets`` của dự án ứng dụng Android

  - Tham khảo `dự án Godot <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer/src/main/assets>`_ của ứng dụng mẫu

- Cấu hình dự án Godot theo ý muốn

  - Đảm bảo `orientation <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-display-window-handheld-orientation>`_ được đặt cho dự án Godot khớp với giá trị được đặt trong manifest của ứng dụng Android
  - Đối với Android, hãy đảm bảo `textures/vram_compression/import_etc2_astc <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-rendering-textures-vram-compression-import-etc2-astc>`_ được đặt thành `true`

- Cập nhật logic script của dự án Godot khi cần

  - Đối với ứng dụng mẫu, `logic script <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/assets/main.gd>`_ truy vấn instance runtime ``GodotPlugin`` và sử dụng nó để đăng ký các signal do logic ứng dụng phát ra
  - Logic ứng dụng phát một signal mỗi khi một mục được chọn trong danh sách. Signal này chứa đường dẫn tệp của mô hình glTF, được logic ``gdscript`` sử dụng để render mô hình.

  .. code-block:: gdscript

    extends Node3D

    # Tham chiếu đến mô hình gltf hiện đang được hiển thị.
    var current_gltf_node: Node3D = null

    func _ready():
      # Asset mặc định cần tải khi ứng dụng khởi động
      _load_gltf("res://gltfs/food_kit/turkey.glb")

      var appPlugin = Engine.get_singleton("AppPlugin")
      if appPlugin:
        print("App plugin is available")

        # Signal được phát từ logic ứng dụng để cập nhật mô hình gltf đang hiển thị
        appPlugin.connect("show_gltf", _load_gltf)
      else:
        print("App plugin is not available")


    # Tải mô hình gltf được chỉ định bởi đường dẫn đã cho
    func _load_gltf(gltf_path: String):
      if current_gltf_node != null:
        remove_child(current_gltf_node)

      current_gltf_node = load(gltf_path).instantiate()

      add_child(current_gltf_node)


3. Build và chạy ứng dụng
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi hoàn tất cấu hình dự án Godot, hãy build và chạy ứng dụng Android. Nếu được thiết lập đúng, Activity host sẽ khởi tạo Godot Engine nhúng khi khởi động. Godot Engine sẽ kiểm tra thư mục ``assets`` để tìm các tệp dự án cần tải (trừ khi được cấu hình để tìm ``main pack``) và sau đó chạy dự án.

Khi ứng dụng đang chạy trên thiết bị, bạn có thể kiểm tra `Android logcat <https://developer.android.com/studio/debug/logcat>`_ để điều tra mọi lỗi hoặc sự cố crash.

Để tham khảo, hãy xem `hướng dẫn build và cài đặt <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md>`_ cho ứng dụng mẫu GLTF Viewer.

.. _`Android library`: https://developer.android.com/studio/projects/android-library
.. _`MavenCentral`: https://central.sonatype.com/artifact/org.godotengine/godot
.. _`its documentation`: https://javadoc.io/doc/org.godotengine/godot/latest/index.html
.. _`GLTF Viewer`: https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer
.. _`Android RecyclerView component`: https://developer.android.com/develop/ui/views/layout/recyclerview
.. _`Kenney's Food Kit pack`: https://kenney.nl/assets/food-kit
.. _`on GitHub`: https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer
.. _`its README`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md
.. _`android:process attribute`: https://developer.android.com/guide/topics/manifest/activity-element#proc
.. _`android:screenOrientation attribute`: https://developer.android.com/guide/topics/manifest/activity-element#screen
.. _`android:configChanges attribute`: https://developer.android.com/guide/topics/manifest/activity-element#config
.. _`Android Studio`: https://developer.android.com/studio
.. _`Gradle`: https://developer.android.com/build
.. _`maven dependency for the Godot Android library`: https://central.sonatype.com/artifact/org.godotengine/godot
.. _`MainActivity`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt
.. _`GodotHost interface`: https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java
.. _`Fragments`: https://developer.android.com/guide/fragments
.. _`GodotFragment`: https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotFragment.java
.. _`GodotActivity`: https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotActivity.kt
.. _`Godot`: https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/Godot.kt
.. _`GodotHost#getHostPlugins(...)`: https://github.com/m4gr3d/Godot-Android-Samples/blob/0e3440f357f8be5b4c63a4fe75766793199a99d0/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt#L55
.. _`runtime GodotPlugin instance`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/AppPlugin.kt
.. _`ItemsSelectionFragment fragment`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/ItemsSelectionFragment.kt
.. _`PCK or ZIP file`: https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html#pck-versus-zip-pack-file-formats
.. _`GodotHost#getCommandLine()`: https://github.com/godotengine/godot/blob/6916349697a4339216469e9bf5899b983d78db07/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java#L45
.. _`Godot project`: https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer/src/main/assets
.. _`orientation`: https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-display-window-handheld-orientation
.. _`textures/vram_compression/import_etc2_astc`: https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-rendering-textures-vram-compression-import-etc2-astc
.. _`script logic`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/assets/main.gd
.. _`Android logcat`: https://developer.android.com/studio/debug/logcat
.. _`build and install instructions`: https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md
