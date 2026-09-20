.. _doc_configuring_an_ide_clion:

CLion
=====

`CLion <https://www.jetbrains.com/clion/>`_ là một IDE `JetBrains <https://www.jetbrains.com/>`_ dành cho C++, miễn phí cho mục đích phát triển cá nhân, phi thương mại.

Nhập dự án
----------

CLion có thể nhập `tệp cơ sở dữ liệu biên dịch <https://clang.llvm.org/docs/JSONCompilationDatabase.html>`_ của dự án, thường có tên là ``compile_commands.json``. Để tạo tệp cơ sở dữ liệu biên dịch, hãy mở terminal, chuyển đến thư mục gốc của Godot và chạy:

::

    scons compiledb=yes compile_commands.json

Tiếp theo, mở thư mục gốc của Godot bằng CLion và chờ dự án được lập chỉ mục hoàn toàn. Nếu tính năng tự động hoàn tất mã, thông tin tham số hoặc tái cấu trúc chưa được bật, bạn sẽ cần tải dự án bằng CMake. Để thực hiện việc này, hãy tìm tệp ``CMakeLists.txt`` trong thư mục ``platform\android\java\nativeSrcsConfigs``, nhấp chuột phải và chọn :button:`Load CMake Project`. Sau khi dự án được tải lại, một cấu hình build ``godot`` sẽ được thêm vào. Bạn có thể an toàn xóa cấu hình này vì tệp CMake sẽ không build dự án mà chỉ tồn tại để tải dự án trong các IDE của JetBrains.

   .. note:: Windows Users:

      Để ``compile_commands.json`` được tải chính xác trong CLion, trước tiên bạn phải cấu hình toolchain Visual Studio cho CLion.

      - Đi đến **Settings > Build, Execution, Deployment > Toolchains** - Nhấp vào nút **+** và chọn ``Visual Studio`` - CLion sẽ cố gắng phát hiện bản cài đặt Visual Studio của bạn. Nếu không thành công, hãy sử dụng biểu tượng tệp ở bên phải ``Toolset:`` để chọn thư mục chứa bản cài đặt Visual Studio của bạn.

      Bạn có thể thoát và tải lại CLion; khi đó CLion sẽ tải lại ``compile_commands.json``

.. figure:: img/clion_visual_studio_toolchain.webp
   :align: center

Biên dịch và gỡ lỗi dự án
-------------------------

CLion không hỗ trợ biên dịch và gỡ lỗi Godot thông qua SCons ngay từ đầu. Bạn có thể thực hiện việc này bằng cách tạo một đích build tùy chỉnh và cấu hình chạy trong CLion. Trước khi tạo đích build tùy chỉnh, bạn phải :ref:`compile Godot <toc-devel-compiling>` một lần trên dòng lệnh để tạo tệp thực thi Godot. Hãy mở terminal, chuyển đến thư mục gốc của Godot và thực thi:

::

    scons dev_build=yes

Để thêm một đích build tùy chỉnh gọi SCons để biên dịch:

- Mở CLion và đi đến **Settings > Build, Execution, Deployment > Custom Build Targets**

.. figure:: img/clion-preferences.png
   :align: center

- Nhấp vào **Add target** và đặt tên cho đích, ví dụ: ``Godot debug``.

.. figure:: img/clion-target.png
   :align: center

- Nhấp vào **...** bên cạnh hộp chọn **Build:**, sau đó nhấp vào nút **+** trong hộp thoại **External Tools** để thêm một công cụ bên ngoài mới.

.. figure:: img/clion-external-tools.png
   :align: center

- Đặt tên cho công cụ, ví dụ: ``Build Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành các tùy chọn biên dịch bạn muốn (xem :ref:`compiling Godot <toc-devel-compiling>`), và đặt **Working directory** thành ``$ProjectFileDirĐặt tên cho công cụ, ví dụ: ``Build Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành các tùy chọn biên dịch bạn muốn (xem :ref:`compiling Godot <toc-devel-compiling>`), và đặt **Working directory** thành `, tương ứng với thư mục gốc của Godot. Nhấp **OK** để tạo công cụ.

   .. note:: CLion does not expand shell commands like ``scons -j$(nproc)``. Use concrete values instead, e.g. ``scons -j8``.

.. figure:: img/clion-create-build-tool.webp
   :align: center

- Quay lại hộp thoại **External Tools**, nhấp lại vào **+** để thêm công cụ bên ngoài thứ hai nhằm dọn dẹp bản build Godot thông qua SCons. Đặt tên cho công cụ, ví dụ: ``Clean Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành ``-c`` (tùy chọn này sẽ dọn dẹp bản build), và đặt **Working directory** thành ``$ProjectFileDirQuay lại hộp thoại **External Tools**, nhấp lại vào **+** để thêm công cụ bên ngoài thứ hai nhằm dọn dẹp bản build Godot thông qua SCons. Đặt tên cho công cụ, ví dụ: ``Clean Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành ``-c`` (tùy chọn này sẽ dọn dẹp bản build), và đặt **Working directory** thành `. Nhấp **OK** để tạo công cụ.

.. figure:: img/clion-create-clean-tool.png
   :align: center

- Đóng hộp thoại **External Tools**. Trong hộp thoại **Custom Build Target** dành cho đích build tùy chỉnh ``Godot debug``, chọn công cụ **Build Godot debug** từ hộp chọn **Build**, và chọn công cụ **Clean Godot debug** từ hộp chọn **Clean**. Nhấp **OK** để tạo đích build tùy chỉnh.

.. figure:: img/clion-select-tools.png
   :align: center

- Trong cửa sổ IDE chính, nhấp vào **Add Configuration**.

.. figure:: img/clion-add-configuration.png
   :align: center

- Trong hộp thoại **Run/Debug Configuration**, nhấp vào **Add new...**, sau đó chọn **Custom Build Application** để tạo cấu hình chạy/gỡ lỗi tùy chỉnh mới.

.. figure:: img/clion-add-custom-build-application.png
   :align: center

- Đặt tên cho cấu hình chạy/gỡ lỗi, ví dụ: ``Godot debug``, chọn đích build tùy chỉnh ``Godot debug`` làm **Target**. Chọn tệp thực thi Godot trong thư mục ``bin/`` làm **Executable**, và đặt **Program arguments** thành ``--editor --path path-to-your-project/``, trong đó ``path-to-your-project/`` phải là đường dẫn trỏ đến một dự án Godot hiện có. Nếu bỏ qua đối số ``--path``, bạn sẽ chỉ có thể gỡ lỗi cửa sổ Godot Project Manager. Nhấp **OK** để tạo cấu hình chạy/gỡ lỗi.

.. figure:: img/clion-run-configuration.png
   :align: center

Giờ đây, bạn có thể build, chạy, gỡ lỗi, lập hồ sơ và kiểm tra Valgrind cho trình chỉnh sửa Godot thông qua cấu hình chạy.

.. figure:: img/clion-build-run.png
   :align: center

Khi chạy một cảnh, trình chỉnh sửa Godot sẽ tạo một tiến trình riêng. Bạn có thể gỡ lỗi tiến trình này trong CLion bằng cách đi đến **Run > Attach to process...**, nhập ``godot`` và chọn tiến trình Godot có **pid** (ID tiến trình) cao nhất; đây thường sẽ là dự án đang chạy.

Bỏ qua các tệp đối tượng và thư viện
------------------------------------

Sau khi build Godot trong CLion, bạn có thể thấy các tệp đối tượng và thư viện xuất hiện trong chế độ xem **Project**.

.. figure:: img/clion-object-library-files-in-project-view.webp
   :align: center

Bạn có thể cấu hình CLion để bỏ qua các tệp này:

- Mở CLion và đi đến **Settings > Editor > File Types > Ignored Files and Folders** - Nhấp vào nút **+** để thêm ``*.o`` và ``*.a`` vào danh sách. Trong Windows, bạn sẽ thêm ``*.obj`` và ``*.dll``.

.. figure:: img/clion-ignore-object-library-files.webp
   :align: center

Giờ đây, các tệp sẽ được bỏ qua trong chế độ xem Project.
