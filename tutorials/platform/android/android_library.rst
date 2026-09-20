.. _doc_android_library:

Thư viện Android của Godot
==========================

Godot Engine dành cho các nền tảng Android được thiết kế để sử dụng như một `Android library <https://developer.android.com/studio/projects/android-library>`_. Kiến trúc này cung cấp một số tính năng quan trọng trên các nền tảng Android:

- Khả năng tích hợp hệ thống build Gradle trong Godot Editor, cho phép tận dụng thêm nhiều thành phần từ hệ sinh thái Android như các thư viện và công cụ

- Khả năng làm cho engine portable và có thể nhúng được:

  - Đóng vai trò then chốt trong việc chuyển Godot Editor sang Android và các thiết bị mobile XR - Đóng vai trò then chốt trong việc cho phép tích hợp và tái sử dụng các khả năng của Godot trong codebase hiện có

Dưới đây, chúng tôi mô tả một số trường hợp sử dụng và kịch bản mà kiến trúc này hỗ trợ.

Sử dụng thư viện Android của Godot
----------------------------------

Thư viện Android của Godot được đóng gói dưới dạng tệp lưu trữ AAR và được lưu trữ trên `MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_ cùng với `its documentation <https://javadoc.io/doc/org.godotengine/godot/latest/index.html>`_.

Thư viện này cung cấp quyền truy cập vào các API và khả năng của Godot trên các nền tảng Android cho các trường hợp sử dụng sau đây, nhưng danh sách không đầy đủ.

Godot Android plugins
---------------------

Android plugins là các công cụ mạnh mẽ để mở rộng khả năng của Godot Engine bằng cách tận dụng chức năng do các nền tảng và hệ sinh thái Android cung cấp.

Android plugin là một thư viện Android có dependency vào thư viện Android của Godot. Plugin sử dụng thư viện này để tích hợp vào lifecycle của engine và truy cập các API của Godot, nhờ đó có được các khả năng mạnh mẽ như hỗ trợ GDExtension, cho phép cập nhật / mod hành vi của engine khi cần.

Để biết thêm thông tin, hãy xem :ref:`Godot Android plugins <doc_android_plugin>`.

Nhúng Godot vào các dự án Android hiện có
-----------------------------------------

Godot Engine có thể được nhúng trong các ứng dụng hoặc thư viện Android hiện có, cho phép developer tận dụng code và thư viện成熟, đã được kiểm thử thực tế, phù hợp hơn với một tác vụ cụ thể.

Thành phần hosting chịu trách nhiệm điều khiển lifecycle của engine thông qua các API Android của Godot. Các API này cũng có thể được sử dụng để cung cấp giao tiếp hai chiều giữa host và instance Godot được nhúng, cho phép kiểm soát tốt hơn experience mong muốn.

Chúng tôi minh họa cách thực hiện việc này bằng một Android app mẫu nhúng Godot Engine dưới dạng một Android view và sử dụng engine để render các model glTF 3D.

Ứng dụng mẫu `GLTF Viewer <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer>`_ sử dụng một `Android RecyclerView component <https://developer.android.com/develop/ui/views/layout/recyclerview>`_ để tạo danh sách các mục glTF, được nạp từ `Kenney's Food Kit pack <https://kenney.nl/assets/food-kit>`_. Khi chọn một mục trong danh sách, logic của ứng dụng tương tác với Godot Engine được nhúng để render mục glTF đã chọn dưới dạng model 3D.

.. image:: img/gltf_viewer_sample_app_screenshot.webp

Bạn có thể tìm thấy mã nguồn của ứng dụng mẫu `on GitHub <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer>`_. Làm theo hướng dẫn trên `its README <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md>`_ để build và cài đặt ứng dụng.

Dưới đây, chúng tôi phân tích từng bước được sử dụng để tạo ứng dụng GLTF Viewer.

.. warning::

  Hiện tại, mỗi process chỉ hỗ trợ một instance Godot Engine duy nhất. Bạn có thể cấu hình process mà Android Activity chạy trên đó bằng `android:process attribute <https://developer.android.com/guide/topics/manifest/activity-element#proc>`_.

.. warning::

  Các sự kiện tự động thay đổi kích thước / cấu hình orientation không được hỗ trợ và có thể gây crash. Bạn có thể vô hiệu hóa các sự kiện đó bằng cách:

  - Khóa ở một orientation cụ thể bằng `android:screenOrientation attribute <https://developer.android.com/guide/topics/manifest/activity-element#screen>`_. - Khai báo rằng Activity sẽ xử lý các sự kiện cấu hình này bằng `android:configChanges attribute <https://developer.android.com/guide/topics/manifest/activity-element#config>`_.

1. Tạo Android app
~~~~~~~~~~~~~~~~~~

.. note::

  Ứng dụng Android mẫu được tạo bằng `Android Studio <https://developer.android.com/studio>`_ và sử dụng `Gradle <https://developer.android.com/build>`_ làm hệ thống build.

  Hệ sinh thái Android cung cấp nhiều công cụ, IDE và hệ thống build để tạo Android app, vì vậy bạn có thể tự do sử dụng những công cụ quen thuộc với mình và cập nhật các bước bên dưới cho phù hợp (chúng tôi cũng hoan nghênh các đóng góp cho tài liệu này!).


- Thiết lập một project ứng dụng Android. Đây có thể là một project trống hoàn toàn mới hoặc một project hiện có - Thêm `maven dependency for the Godot Android library <https://central.sonatype.com/artifact/org.godotengine/godot>`_

  - Nếu sử dụng ``gradle``, hãy thêm nội dung sau vào phần ``dependency`` trong tệp gradle build của app. Đảm bảo cập nhật ``<version>`` lên phiên bản mới nhất của thư viện Android của Godot:

  .. code-block:: kotlin

    implementation("org.godotengine:godot:<version>")

- Nếu sử dụng ``gradle``, hãy thêm cấu hình ``aaptOptions`` sau vào phần ``android > defaultConfig`` trong tệp gradle build của app. Việc này cho phép ``gradle`` đưa các thư mục ẩn của Godot vào khi build binary của app.

  - Nếu hệ thống build của bạn không hỗ trợ đưa các thư mục ẩn vào, bạn có thể cấu hình project Godot để không sử dụng các thư mục ẩn bằng cách bỏ chọn
    :ref:`Application > Config > Use Hidden Project Data Directory<class_ProjectSettings_property_application/config/use_hidden_project_data_directory>`
    trong Project Settings.

.. code-block:: groovy

  android {

    defaultConfig {
        // Mẫu ignore mặc định cho thư mục 'assets' bao gồm các tệp ẩn và
        // thư mục được các project Godot sử dụng, vì vậy chúng ta ghi đè mẫu này bằng nội dung sau.
        aaptOptions {
            ignoreAssetsPattern "!.svn:!.git:!.gitignore:!.ds_store:!*.scc:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
        }
      ...

- Tạo / cập nhật Activity của ứng dụng, nơi sẽ hosting instance Godot Engine. Đối với ứng dụng mẫu, đó là `MainActivity <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt>`_

  - Host Activity phải triển khai `GodotHost interface <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java>`_ - Ứng dụng mẫu sử dụng `Fragments <https://developer.android.com/guide/fragments>`_ để tổ chức UI, vì vậy ứng dụng sử dụng `GodotFragment <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotFragment.java>`_, một fragment component do thư viện Android của Godot cung cấp để tự động hosting và quản lý instance Godot Engine.

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

  Thư viện Android của Godot cũng cung cấp `GodotActivity <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/GodotActivity.kt>`_, một Activity component có thể được mở rộng để tự động hosting và quản lý instance Godot Engine.

  Ngoài ra, ứng dụng có thể trực tiếp tạo một instance `Godot <https://github.com/godotengine/godot/blob/master/platform/android/java/lib/src/org/godotengine/godot/Godot.kt>`_, rồi tự hosting và quản lý instance đó.

- Sử dụng `GodotHost#getHostPlugins(...) <https://github.com/m4gr3d/Godot-Android-Samples/blob/0e3440f357f8be5b4c63a4fe75766793199a99d0/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/MainActivity.kt#L55>`_, ứng dụng mẫu tạo một `runtime GodotPlugin instance <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/AppPlugin.kt>`_ được dùng để gửi :ref:`signals <doc_signals>` đến logic ``gdscript``

  - ``GodotPlugin`` runtime cũng có thể được logic ``gdscript`` sử dụng để truy cập các phương thức JVM. Để biết thêm thông tin, hãy xem :ref:`Godot Android plugins <doc_android_plugin>`.

- Thêm mọi logic bổ sung mà ứng dụng của bạn sẽ sử dụng

  - Đối với ứng dụng mẫu, việc này bao gồm thêm `ItemsSelectionFragment fragment <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/java/fhuyakou/godot/app/android/gltfviewer/ItemsSelectionFragment.kt>`_ (và các class liên quan), một fragment được sử dụng để build và hiển thị danh sách các mục glTF

- Mở tệp ``AndroidManifest.xml`` và cấu hình orientation nếu cần bằng `android:screenOrientation attribute <https://developer.android.com/guide/topics/manifest/activity-element#screen>`_

  - Nếu cần, vô hiệu hóa các thay đổi cấu hình tự động thay đổi kích thước / orientation bằng `android:configChanges attribute <https://developer.android.com/guide/topics/manifest/activity-element#config>`_

.. code-block:: xml

  <activity android:name=".MainActivity"
      android:screenOrientation="fullUser"
      android:configChanges="orientation|screenSize|smallestScreenSize|screenLayout"
      android:exported="true">

      ...
  </activity>


2. Tạo project Godot
~~~~~~~~~~~~~~~~~~~~

.. note::

  Trên Android, các tệp project của Godot được export vào thư mục ``assets`` của binary ``apk`` được tạo.

  Chúng ta tận dụng kiến trúc đó để liên kết Android app và project Godot bằng cách tạo project Godot trong thư mục ``assets`` của Android app.

  Lưu ý rằng bạn cũng có thể tạo project Godot trong một thư mục riêng và export project đó dưới dạng `PCK or ZIP file <https://docs.godotengine.org/en/stable/tutorials/export/exporting_projects.html#pck-versus-zip-pack-file-formats>`_ vào thư mục ``assets`` của Android app. Cách tiếp cận này yêu cầu truyền đối số ``--main-pack <pck_or_zip_filepath_relative_to_assets_dir>`` cho instance Godot Engine được hosting bằng `GodotHost#getCommandLine() <https://github.com/godotengine/godot/blob/6916349697a4339216469e9bf5899b983d78db07/platform/android/java/lib/src/org/godotengine/godot/GodotHost.java#L45>`_.

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

  Các hướng dẫn bên dưới và ứng dụng mẫu sử dụng cách tiếp cận đầu tiên: tạo project Godot trong thư mục ``assets`` của Android app.


- Như đã đề cập trong **lưu ý** ở trên, mở Godot Editor và tạo trực tiếp một project Godot (không có subfolder) trong thư mục ``assets`` của project ứng dụng Android

  - Xem `Godot project <https://github.com/m4gr3d/Godot-Android-Samples/tree/master/apps/gltf_viewer/src/main/assets>`_ của ứng dụng mẫu để tham khảo

- Cấu hình project Godot theo nhu cầu

  - Đảm bảo `orientation <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-display-window-handheld-orientation>`_ được đặt cho project Godot khớp với giá trị được đặt trong manifest của Android app - Đối với Android, đảm bảo `textures/vram_compression/import_etc2_astc <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-rendering-textures-vram-compression-import-etc2-astc>`_ được đặt thành `true`

- Cập nhật logic script của project Godot khi cần

  - Đối với ứng dụng mẫu, `script logic <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/src/main/assets/main.gd>`_ truy vấn instance runtime ``GodotPlugin`` và sử dụng instance này để đăng ký các signal do logic của app phát ra - Logic của app phát signal mỗi khi một mục được chọn trong danh sách. Signal chứa filepath của model glTF, được logic ``gdscript`` sử dụng để render model.

  .. code-block:: gdscript

    extends Node3D

    # Tham chiếu đến model gltf hiện đang được hiển thị.
    var current_gltf_node: Node3D = null

    func _ready():
      # Asset mặc định được load khi app khởi động
      _load_gltf("res://gltfs/food_kit/turkey.glb")

      var appPlugin = Engine.get_singleton("AppPlugin")
      if appPlugin:
        print("App plugin is available")

        # Signal được phát từ logic của app để cập nhật model gltf đang hiển thị
        appPlugin.connect("show_gltf", _load_gltf)
      else:
        print("App plugin is not available")


    # Load model gltf được chỉ định bởi path đã cho
    func _load_gltf(gltf_path: String):
      if current_gltf_node != null:
        remove_child(current_gltf_node)

      current_gltf_node = load(gltf_path).instantiate()

      add_child(current_gltf_node)


3. Build và chạy app
~~~~~~~~~~~~~~~~~~~~

Sau khi hoàn tất cấu hình project Godot, hãy build và chạy Android app. Nếu được thiết lập đúng, host Activity sẽ khởi tạo Godot Engine được nhúng khi khởi động. Godot Engine sẽ kiểm tra thư mục ``assets`` để tìm các tệp project cần load (trừ khi được cấu hình để tìm một ``main pack``), sau đó tiếp tục chạy project.

Trong khi app đang chạy trên thiết bị, bạn có thể kiểm tra `Android logcat <https://developer.android.com/studio/debug/logcat>`_ để điều tra mọi lỗi hoặc crash.

Để tham khảo, hãy kiểm tra `build and install instructions <https://github.com/m4gr3d/Godot-Android-Samples/blob/master/apps/gltf_viewer/README.md>`_ của ứng dụng mẫu GLTF Viewer.
