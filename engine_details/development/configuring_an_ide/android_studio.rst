.. _doc_configuring_an_ide_android_studio:

Android Studio
==============

`Android Studio <https://developer.android.com/studio>`_ là một IDE miễn phí dành cho việc phát triển Android, do `Google <https://about.google/>`_ và `JetBrains <https://www.jetbrains.com/>`_ tạo ra. IDE này dựa trên `IntelliJ IDEA <https://www.jetbrains.com/idea/>`_ và có trình soạn thảo giàu tính năng, hỗ trợ Java và C/C++. Bạn có thể dùng IDE này để làm việc trên engine cốt lõi của Godot cũng như codebase của nền tảng Android.

Nhập dự án
----------

- Từ cửa sổ chào mừng của Android Studio, chọn **Open**.

.. figure:: img/android_studio_setup_project_1.png
   :figclass: figure-w480
   :align: center

   Android Studio's welcome window.

- Điều hướng đến ``<Godot root directory>/platform/android/java`` và chọn tệp ``settings.gradle``. - Android Studio sẽ nhập và lập chỉ mục dự án.

Bố cục dự án Android Studio
---------------------------

Dự án được tổ chức bằng `các module của Android Studio <https://developer.android.com/studio/projects#ApplicationModules>`_:

- Module **lib**:

   - Nằm trong ``<Godot root directory>/platform/android/java/lib``, đây là một **module thư viện** dùng để tổ chức mã Java và mã native của Godot, đồng thời cung cấp chúng dưới dạng một `thư viện Android <https://developer.android.com/studio/projects/android-library>`_ có thể tái sử dụng. - :ref:`Godot Android library <doc_android_library>` được tạo ra sẽ khả dụng cho các module / dự án Android khác thông qua `MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_, cùng với `tài liệu của nó <https://javadoc.io/doc/org.godotengine/godot/latest/index.html>`_.

- Module **editor**:

   - Nằm trong ``<Godot root directory>/platform/android/java/editor``, đây là một **module ứng dụng** chứa mã nguồn cho `các bản chuyển của Android và XR <https://godotengine.org/download/android/>`_ của Godot Editor. - Module này phụ thuộc vào module **lib**.

- Module **app**:

   - Nằm trong ``<Godot root directory>/platform/android/java/app``, đây là một **module ứng dụng** chứa mã nguồn cho các template build Android. - Module này phụ thuộc vào module **lib**.

Build và gỡ lỗi module editor
-----------------------------

- Để build module ``editor``:

   - Chọn `menu thả xuống Run/Debug Configurations <https://developer.android.com/studio/run/rundebugconfig#running>`_ rồi chọn ``editor``.

   .. figure:: img/android_studio_editor_configurations_drop_down.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Run 'editor'** từ menu trên cùng hoặc `nhấp vào biểu tượng Run <https://developer.android.com/studio/run/rundebugconfig#running>`_.

- Để gỡ lỗi module ``editor``:

   - Mở cửa sổ **Build Variants** bằng cách chọn **View > Tools Windows > Build Variants** từ menu trên cùng. - Trong cửa sổ **Build Variants**, hãy đảm bảo rằng trong cột **Active Build Variant**, mục ``:editor`` được đặt thành một trong các biến thể **Debug**.

   .. figure:: img/android_studio_editor_build_variant.webp
      :figclass: figure-w480
      :align: center

   - Mở cửa sổ **Run/Debug Configurations** bằng cách nhấp vào **Run > Edit Configurations...** trên menu trên cùng. - Trong cửa sổ **Run/Debug Configurations**, chọn mục ``editor``, rồi trong **Debugger**, đảm bảo **Debug Type** được đặt thành ``Dual (Java + Native)`` - Nhấp vào dấu ``+`` trong phần **Symbol Directories**, rồi thêm thư mục ``platform/android/java/lib/libs/tools/debug``.

   .. figure:: img/android_studio_editor_debug_type_setup.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Debug 'editor'** từ menu trên cùng hoặc `nhấp vào biểu tượng Debug <https://developer.android.com/studio/run/rundebugconfig#running>`_.

Build và gỡ lỗi module app
--------------------------

Module ``app`` yêu cầu có một dự án Godot trong thư mục ``assets`` (``<Godot root directory>/platform/android/java/app/src/main/assets``) để chạy. Việc này thường được Godot Editor xử lý trong quá trình export. Khi phát triển bằng Android Studio, bạn cần tự thêm một dự án Godot vào thư mục đó để mô phỏng quá trình export. Sau khi hoàn tất, bạn có thể làm theo hướng dẫn dưới đây để chạy/gỡ lỗi module ``app``:

- Để build module ``app``:

   - Chọn `menu thả xuống Run/Debug Configurations <https://developer.android.com/studio/run/rundebugconfig#running>`_ rồi chọn ``app``.

   .. figure:: img/android_studio_app_configurations_drop_down.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Run 'app'** từ menu trên cùng hoặc `nhấp vào biểu tượng Run <https://developer.android.com/studio/run/rundebugconfig#running>`_.

- Để gỡ lỗi module ``app``:

   - Mở cửa sổ **Build Variants** bằng cách chọn **View > Tools Windows > Build Variants** từ menu trên cùng. - Trong cửa sổ **Build Variants**, hãy đảm bảo rằng trong cột **Active Build Variant**, mục ``:app`` được đặt thành một trong các biến thể **Debug**.

   .. figure:: img/android_studio_app_build_variant.webp
      :figclass: figure-w480
      :align: center

   - Mở cửa sổ **Run/Debug Configurations** bằng cách nhấp vào **Run > Edit Configurations...** trên menu trên cùng. - Trong cửa sổ **Run/Debug Configurations**, chọn mục ``app``, rồi trong **Debugger**, đảm bảo **Debug Type** được đặt thành ``Dual (Java + Native)`` - Nhấp vào dấu ``+`` trong phần **Symbol Directories**, rồi thêm thư mục ``platform/android/java/lib/libs/debug``.

   .. figure:: img/android_studio_app_debug_type_setup.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Debug 'app'** từ menu trên cùng hoặc `nhấp vào biểu tượng Debug <https://developer.android.com/studio/run/rundebugconfig#running>`_.


Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong `kênh phát triển Android của Godot <https://chat.godotengine.org/channel/android>`__.
