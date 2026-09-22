.. _doc_configuring_an_ide_android_studio:

Android Studio
==============

`Android Studio <https://developer.android.com/studio>`_ là một IDE miễn phí dành cho việc phát triển Android, do `Google <https://about.google/>`_ và `JetBrains <https://www.jetbrains.com/>`_ phát triển. IDE này dựa trên `IntelliJ IDEA <https://www.jetbrains.com/idea/>`_ và có trình chỉnh sửa giàu tính năng, hỗ trợ Java và C++. IDE này có thể được dùng để làm việc trên core engine của Godot cũng như codebase của nền tảng Android.

Nhập project
------------

- Từ cửa sổ chào mừng của Android Studio, chọn **Open**.

.. figure:: img/android_studio_setup_project_1.png
   :figclass: figure-w480
   :align: center

   Cửa sổ chào mừng của Android Studio.

- Đi đến ``<Godot root directory>/platform/android/java`` và chọn file ``settings.gradle``.
- Android Studio sẽ nhập và lập chỉ mục project.

Bố cục project Android Studio
-----------------------------

Project được tổ chức bằng `modules của Android Studio <https://developer.android.com/studio/projects#ApplicationModules>`_:

- Module **lib**:

   - Nằm trong ``<Godot root directory>/platform/android/java/lib``, đây là một **library module** tổ chức code Java và native của Godot, đồng thời cung cấp chúng dưới dạng một `Android library <https://developer.android.com/studio/projects/android-library>`_ có thể tái sử dụng.
   - :ref:`Godot Android library <doc_android_library>` được tạo ra và cung cấp cho các Android module / project khác thông qua `MavenCentral <https://central.sonatype.com/artifact/org.godotengine/godot>`_, cùng với `tài liệu của library <https://javadoc.io/doc/org.godotengine/godot/latest/index.html>`_.

- Module **editor**:

   - Nằm trong ``<Godot root directory>/platform/android/java/editor``, đây là một **application module** chứa source code cho `Android và XR port <https://godotengine.org/download/android/>`_ của Godot Editor.
   - Module này phụ thuộc vào module **lib**.

- Module **app**:

   - Nằm trong ``<Godot root directory>/platform/android/java/app``, đây là một **application module** chứa source code cho các build template của Android.
   - Module này phụ thuộc vào module **lib**.

Build và debug module editor
----------------------------

- Để build module ``editor``:

   - Chọn `Run/Debug Configurations drop down <https://developer.android.com/studio/run/rundebugconfig#running>`_ rồi chọn ``editor``.

   .. figure:: img/android_studio_editor_configurations_drop_down.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Run 'editor'** từ menu trên cùng hoặc `nhấp vào biểu tượng Run <https://developer.android.com/studio/run/rundebugconfig#running>`_.

- Để debug module ``editor``:

   - Mở cửa sổ **Build Variants** bằng cách chọn **View > Tools Windows > Build Variants** từ menu trên cùng.
   - Trong cửa sổ **Build Variants**, đảm bảo rằng trong cột **Active Build Variant**, mục ``:editor`` được đặt thành một trong các variant **Debug**.

   .. figure:: img/android_studio_editor_build_variant.webp
      :figclass: figure-w480
      :align: center

   - Mở cửa sổ **Run/Debug Configurations** bằng cách nhấp vào **Run > Edit Configurations...** trên menu trên cùng.
   - Trong cửa sổ **Run/Debug Configurations**, chọn mục ``editor``, sau đó trong **Debugger**, đảm bảo **Debug Type** được đặt thành ``Dual (Java + Native)``
   - Nhấp vào dấu ``+`` bên dưới phần **Symbol Directories**, rồi thêm thư mục ``platform/android/java/lib/libs/tools/debug``.

   .. figure:: img/android_studio_editor_debug_type_setup.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Debug 'editor'** từ menu trên cùng hoặc `nhấp vào biểu tượng Debug <https://developer.android.com/studio/run/rundebugconfig#running>`_.

Build và debug module app
-------------------------

Module ``app`` yêu cầu có một Godot project trong thư mục ``assets`` (``<Godot root directory>/platform/android/java/app/src/main/assets``) để chạy. Godot Editor thường xử lý việc này trong quá trình export. Khi phát triển bằng Android Studio, bạn cần tự thêm một Godot project vào thư mục đó để mô phỏng quy trình export. Sau khi hoàn tất, bạn có thể làm theo hướng dẫn dưới đây để chạy/debug module ``app``:

- Để build module ``app``:

   - Chọn `Run/Debug Configurations drop down <https://developer.android.com/studio/run/rundebugconfig#running>`_ rồi chọn ``app``.

   .. figure:: img/android_studio_app_configurations_drop_down.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Run 'app'** từ menu trên cùng hoặc `nhấp vào biểu tượng Run <https://developer.android.com/studio/run/rundebugconfig#running>`_.

- Để debug module ``app``:

   - Mở cửa sổ **Build Variants** bằng cách chọn **View > Tools Windows > Build Variants** từ menu trên cùng.
   - Trong cửa sổ **Build Variants**, đảm bảo rằng trong cột **Active Build Variant**, mục ``:app`` được đặt thành một trong các variant **Debug**.

   .. figure:: img/android_studio_app_build_variant.webp
      :figclass: figure-w480
      :align: center

   - Mở cửa sổ **Run/Debug Configurations** bằng cách nhấp vào **Run > Edit Configurations...** trên menu trên cùng.
   - Trong cửa sổ **Run/Debug Configurations**, chọn mục ``app``, sau đó trong **Debugger**, đảm bảo **Debug Type** được đặt thành ``Dual (Java + Native)``
   - Nhấp vào dấu ``+`` bên dưới phần **Symbol Directories**, rồi thêm thư mục ``platform/android/java/lib/libs/debug``.

   .. figure:: img/android_studio_app_debug_type_setup.webp
      :figclass: figure-w480
      :align: center

   - Chọn **Run > Debug 'app'** từ menu trên cùng hoặc `nhấp vào biểu tượng Debug <https://developer.android.com/studio/run/rundebugconfig#running>`_.


Nếu gặp vấn đề, hãy yêu cầu trợ giúp trong `kênh phát triển Android của Godot <https://chat.godotengine.org/channel/android>`__.

.. _`Android Studio`: https://developer.android.com/studio
.. _`Google`: https://about.google/
.. _`JetBrains`: https://www.jetbrains.com/
.. _`IntelliJ IDEA`: https://www.jetbrains.com/idea/
.. _`Android Studio's modules`: https://developer.android.com/studio/projects#ApplicationModules
.. _`Android library`: https://developer.android.com/studio/projects/android-library
.. _`MavenCentral`: https://central.sonatype.com/artifact/org.godotengine/godot
.. _`its documentation`: https://javadoc.io/doc/org.godotengine/godot/latest/index.html
.. _`Android and XR ports`: https://godotengine.org/download/android/
.. _`Run/Debug Configurations drop down`: https://developer.android.com/studio/run/rundebugconfig#running
.. _`click the Run icon`: https://developer.android.com/studio/run/rundebugconfig#running
.. _`click the Debug icon`: https://developer.android.com/studio/run/rundebugconfig#running
