.. _doc_configuring_an_ide_clion:

CLion
=====

`CLion <https://www.jetbrains.com/clion/>`_ là một IDE `JetBrains <https://www.jetbrains.com/>`_ dành cho C++, miễn phí cho việc phát triển cá nhân, phi thương mại.

Nhập project
------------

CLion có thể nhập `compilation database file <https://clang.llvm.org/docs/JSONCompilationDatabase.html>`_ của project, thường có tên là ``compile_commands.json``. Để tạo compilation database file, hãy mở terminal, chuyển đến thư mục gốc của Godot và chạy:

::

    scons compiledb=yes compile_commands.json

Sau đó, mở thư mục gốc của Godot bằng CLion và chờ project được lập chỉ mục hoàn toàn. Nếu tính năng hoàn tất mã, thông tin tham số hoặc refactoring chưa được bật, bạn cần tải project bằng CMake. Để thực hiện việc này, hãy tìm tệp ``CMakeLists.txt`` trong thư mục ``platform\android\java\nativeSrcsConfigs``, nhấp chuột phải và chọn :button:`Load CMake Project`. Sau khi project được tải lại, cấu hình build ``godot`` sẽ được thêm vào. Bạn có thể an toàn xóa cấu hình này vì tệp CMake sẽ không build project mà chỉ tồn tại để tải project trong các IDE của JetBrains.

   .. note:: Người dùng Windows:

      Để ``compile_commands.json`` tải đúng cách trong CLion, trước tiên bạn phải cấu hình toolchain Visual Studio cho CLion.

      - Đi đến **Settings > Build, Execution, Deployment > Toolchains**
      - Nhấp vào nút **+** và chọn ``Visual Studio``
      - CLion sẽ cố gắng phát hiện bản cài đặt Visual Studio của bạn. Nếu không thành công, hãy sử dụng biểu tượng tệp ở bên phải ``Toolset:`` để chọn thư mục chứa bản cài đặt Visual Studio của bạn.

      Bạn có thể thoát và tải lại CLion; khi đó ``compile_commands.json`` sẽ được tải lại

.. figure:: img/clion_visual_studio_toolchain.webp
   :align: center

Biên dịch và debug project
--------------------------

CLion không hỗ trợ biên dịch và debug Godot bằng SCons ngay khi cài đặt. Bạn có thể thực hiện việc này bằng cách tạo build target tùy chỉnh và run configuration trong CLion. Trước khi tạo build target tùy chỉnh, bạn phải :ref:`compile Godot <toc-devel-compiling>` một lần trên command line để tạo tệp thực thi Godot. Hãy mở terminal, chuyển đến thư mục gốc của Godot và thực thi:

::

    scons dev_build=yes

Để thêm build target tùy chỉnh gọi SCons để biên dịch:

- Mở CLion và đi đến **Settings > Build, Execution, Deployment > Custom Build Targets**

.. figure:: img/clion-preferences.png
   :align: center

- Nhấp vào **Add target** và đặt tên cho target, ví dụ ``Godot debug``.

.. figure:: img/clion-target.png
   :align: center

- Nhấp vào **...** bên cạnh hộp chọn **Build:**, sau đó nhấp vào nút **+** trong hộp thoại **External Tools** để thêm external tool mới.

.. figure:: img/clion-external-tools.png
   :align: center

- Đặt tên cho tool, ví dụ ``Build Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành các tùy chọn biên dịch bạn muốn (xem :ref:`compiling Godot <toc-devel-compiling>`), và đặt **Working directory** thành ``$ProjectFileDir$``, tương ứng với thư mục gốc của Godot. Nhấp **OK** để tạo tool.

   .. note:: CLion không mở rộng các shell command như ``scons -j$(nproc)``. Thay vào đó, hãy sử dụng các giá trị cụ thể, ví dụ ``scons -j8``.

.. figure:: img/clion-create-build-tool.webp
   :align: center

- Quay lại hộp thoại **External Tools**, nhấp lại vào **+** để thêm external tool thứ hai nhằm dọn dẹp build Godot bằng SCons. Đặt tên cho tool, ví dụ ``Clean Godot debug``, đặt **Program** thành ``scons``, đặt **Arguments** thành ``-c`` (thao tác này sẽ dọn dẹp build), và đặt **Working directory** thành ``$ProjectFileDir$``. Nhấp **OK** để tạo tool.

.. figure:: img/clion-create-clean-tool.png
   :align: center

- Đóng hộp thoại **External Tools**. Trong hộp thoại **Custom Build Target** dành cho build target ``Godot debug`` tùy chỉnh, chọn tool **Build Godot debug** từ hộp chọn **Build**, rồi chọn tool **Clean Godot debug** từ hộp chọn **Clean**. Nhấp **OK** để tạo build target tùy chỉnh.

.. figure:: img/clion-select-tools.png
   :align: center

- Trong cửa sổ IDE chính, nhấp vào **Add Configuration**.

.. figure:: img/clion-add-configuration.png
   :align: center

- Trong hộp thoại **Run/Debug Configuration**, nhấp vào **Add new...**, sau đó chọn **Custom Build Application** để tạo run/debug configuration tùy chỉnh mới.

.. figure:: img/clion-add-custom-build-application.png
   :align: center

- Đặt tên cho run/debug configuration, ví dụ ``Godot debug``, chọn build target tùy chỉnh ``Godot debug`` làm **Target**. Chọn tệp thực thi Godot trong thư mục ``bin/`` làm **Executable**, và đặt **Program arguments** thành ``--editor --path path-to-your-project/``, trong đó ``path-to-your-project/`` phải là đường dẫn trỏ đến một project Godot hiện có. Nếu bỏ qua đối số ``--path``, bạn sẽ chỉ có thể debug cửa sổ Godot Project Manager. Nhấp **OK** để tạo run/debug configuration.

.. figure:: img/clion-run-configuration.png
   :align: center

Giờ đây, bạn có thể build, chạy, debug, lập hồ sơ hiệu năng và kiểm tra bằng Valgrind trình chỉnh sửa Godot thông qua run configuration.

.. figure:: img/clion-build-run.png
   :align: center

Khi chạy một scene, trình chỉnh sửa Godot sẽ tạo một process riêng. Bạn có thể debug process này trong CLion bằng cách đi đến **Run > Attach to process...**, nhập ``godot``, rồi chọn process Godot có **pid** (process ID) cao nhất; thông thường đó sẽ là project đang chạy.

Bỏ qua các tệp object và library
--------------------------------

Sau khi build Godot trong CLion, bạn có thể thấy các tệp object và library xuất hiện trong chế độ xem **Project**.

.. figure:: img/clion-object-library-files-in-project-view.webp
   :align: center

Bạn có thể cấu hình CLion để bỏ qua các tệp đó:

- Mở CLion và đi đến **Settings > Editor > File Types > Ignored Files and Folders**
- Nhấp vào nút **+** để thêm ``*.o`` và ``*.a`` vào danh sách. Trong Windows, bạn sẽ thêm ``*.obj`` và ``*.dll``.

.. figure:: img/clion-ignore-object-library-files.webp
   :align: center

Giờ đây, các tệp sẽ được bỏ qua trong chế độ xem Project.

.. _`CLion`: https://www.jetbrains.com/clion/
.. _`JetBrains`: https://www.jetbrains.com/
.. _`compilation database file`: https://clang.llvm.org/docs/JSONCompilationDatabase.html
