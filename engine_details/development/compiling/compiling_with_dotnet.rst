.. _doc_compiling_with_dotnet:

Biên dịch với .NET
==================

.. highlight:: shell

Yêu cầu
-------

- `.NET SDK 8.0+ <https://dotnet.microsoft.com/download>`_

  Bạn có thể sử dụng ``dotnet --info`` để kiểm tra các phiên bản .NET SDK đã được cài đặt.

Bật module .NET
---------------

.. note:: C# support for Godot has historically used the
          môi trường runtime `Mono <https://www.mono-project.com/>`_ thay vì `.NET Runtime <https://github.com/dotnet/runtime>`_ và bên trong, nhiều thứ vẫn được đặt tên là ``mono`` thay vì ``dotnet`` hoặc được gọi theo cách khác là ``mono``.

Theo mặc định, module .NET bị tắt khi build. Để bật module này, hãy thêm tùy chọn ``module_mono_enabled=yes`` vào dòng lệnh SCons, đồng thời làm theo các hướng dẫn để build các binary Godot mong muốn.

Tạo glue
--------

Một phần mã nguồn của các thư viện managed được tạo từ ClassDB. Các tệp mã nguồn này phải được tạo trước khi build các thư viện managed. Bạn có thể tạo chúng bằng bất kỳ binary editor Godot nào đã bật .NET bằng cách chạy binary đó với các tham số ``--headless --generate-mono-glue``, theo sau là đường dẫn đến một thư mục đầu ra. Đường dẫn này phải là ``modules/mono/glue`` trong thư mục Godot:

::

    <godot_binary> --headless --generate-mono-glue modules/mono/glue

Lệnh này yêu cầu Godot tạo các liên kết C# cho API Godot tại ``modules/mono/glue/GodotSharp/GodotSharp/Generated`` và các liên kết C# cho các công cụ editor tại ``modules/mono/glue/GodotSharp/GodotSharpEditor/Generated``. Sau khi các tệp này được tạo, bạn có thể build các thư viện managed của Godot cho tất cả các target mong muốn mà không cần lặp lại quy trình này.

``<godot_binary>`` là binary editor mà bạn đã biên dịch với module .NET được bật. Tên chính xác sẽ khác nhau tùy theo hệ thống và cấu hình của bạn, nhưng phải có dạng ``bin/godot.<platform>.editor.<arch>.mono``, ví dụ ``bin/godot.linuxbsd.editor.x86_64.mono`` hoặc ``bin/godot.windows.editor.x86_32.mono.exe``. Đặc biệt lưu ý hậu tố **.mono**! Nếu trước đây bạn đã biên dịch Godot mà không có hỗ trợ .NET, bạn có thể cũng có các binary có tên tương tự nhưng không có hậu tố này. Không thể sử dụng các binary đó để tạo glue .NET.

.. note:: The glue sources must be regenerated every time the ClassDB-registered
          các thay đổi API. Chẳng hạn, khi một phương thức mới được đăng ký vào scripting API hoặc một trong các tham số của phương thức đó thay đổi. Godot sẽ in lỗi khi khởi động nếu có sự không khớp API giữa ClassDB và mã nguồn glue.

Build các thư viện managed
--------------------------

Sau khi đã tạo glue .NET, bạn có thể build các thư viện managed bằng script ``build_assemblies.py``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir=./bin

Nếu mọi thứ diễn ra thuận lợi, thư mục ``GodotSharp``, chứa các thư viện managed, sẽ được tạo trong thư mục ``bin``.

.. note:: By default, all development builds share a version number, which can
          có thể gây ra một số vấn đề với việc lưu bộ nhớ đệm của các gói NuGet. Để giải quyết vấn đề này, hãy sử dụng ``GODOT_VERSION_STATUS`` để cung cấp cho mỗi bản build một phiên bản duy nhất hoặc xóa ``GodotNuGetFallbackFolder`` sau mỗi lần build để xóa bộ nhớ đệm gói.

Không giống các bản build Godot "cổ điển", khi build với module .NET được bật (và tùy thuộc vào nền tảng đích), một thư mục dữ liệu có thể được tạo cho cả editor và các project đã export. Thư mục này rất quan trọng để Godot hoạt động chính xác và phải được phân phối cùng với Godot. Xem thêm chi tiết về thư mục này trong
:ref:`Data directory<compiling_with_dotnet_data_directory>`.

Nền tảng build
~~~~~~~~~~~~~~

Cung cấp đối số ``--godot-platform=<platform>`` để kiểm soát thư viện được build dành riêng cho nền tảng nào. Bỏ qua đối số này để build cho hệ thống hiện tại.

Hiện tại, tùy chọn này chỉ kiểm soát việc đưa hỗ trợ cho Visual Studio dưới dạng editor bên ngoài vào; các thư viện này otherwise giống hệt nhau.

Các gói NuGet
~~~~~~~~~~~~~

Các assembly API, source generator và custom MSBuild project SDK được phân phối dưới dạng các gói NuGet. Người dùng hoàn toàn không cần quan tâm đến việc này, nhưng nó có thể khiến quá trình phát triển trở nên phức tạp.

Để sử dụng Godot với phiên bản phát triển của các gói đó, cần tạo một nguồn NuGet cục bộ để MSBuild có thể tìm thấy chúng.

Trước tiên, hãy chọn một vị trí cho nguồn NuGet cục bộ. Nếu không có lựa chọn ưu tiên, hãy tạo một thư mục trống tại một trong các vị trí được khuyến nghị sau:

- Trên Windows, ``C:\Users\<username>\MyLocalNugetSource`` - Trên Linux, \*BSD, v.v., ``~/MyLocalNugetSource``

Đường dẫn này sẽ được gọi là ``<my_local_source>`` ở phần sau.

Sau khi chọn một thư mục, hãy chạy lệnh .NET CLI này để cấu hình NuGet sử dụng nguồn cục bộ của bạn:

::

    dotnet nuget add source <my_local_source> --name MyLocalNugetSource

Khi chạy script ``build_assemblies.py``, hãy truyền ``<my_local_source>`` cho tùy chọn ``--push-nupkgs-local``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source>

Tùy chọn này đảm bảo các gói sẽ được thêm vào nguồn NuGet cục bộ đã chỉ định và các phiên bản xung đột của gói sẽ được xóa khỏi bộ nhớ đệm NuGet. Bạn nên luôn sử dụng tùy chọn này khi build các solution C# trong quá trình phát triển để tránh sai sót.

Build mà không phụ thuộc vào các tính năng đã bị loại bỏ (NO_DEPRECATED)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi build Godot mà không có các class và hàm đã bị loại bỏ, tức là sử dụng đối số ``deprecated=no`` cho scons, các thư viện managed cũng phải được build mà không phụ thuộc vào mã đã bị loại bỏ. Thực hiện việc này bằng cách truyền đối số ``--no-deprecated``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --no-deprecated

Hỗ trợ độ chính xác kép (REAL_T_IS_DOUBLE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi build Godot với hỗ trợ độ chính xác kép, tức là sử dụng đối số ``precision=double`` cho scons, các thư viện managed phải được điều chỉnh cho phù hợp bằng cách truyền đối số ``--precision=double``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --precision=double

Ví dụ
-----

Ví dụ (Windows)
~~~~~~~~~~~~~~~

::

    # Build editor binary
    scons platform=windows target=editor module_mono_enabled=yes
    # Build export templates
    scons platform=windows target=template_debug module_mono_enabled=yes
    scons platform=windows target=template_release module_mono_enabled=yes

    # Generate glue sources
    bin/godot.windows.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue
    # Build .NET assemblies
    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --godot-platform=windows


Ví dụ (Linux, \*BSD)
~~~~~~~~~~~~~~~~~~~~

::

    # Build editor binary
    scons platform=linuxbsd target=editor module_mono_enabled=yes
    # Build export templates
    scons platform=linuxbsd target=template_debug module_mono_enabled=yes
    scons platform=linuxbsd target=template_release module_mono_enabled=yes

    # Generate glue sources
    bin/godot.linuxbsd.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue
    # Generate binaries
    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --godot-platform=linuxbsd

.. _compiling_with_dotnet_data_directory:

Thư mục dữ liệu
---------------

Thư mục dữ liệu là một phần phụ thuộc của các binary Godot được build với module .NET được bật. Thư mục này chứa các tệp quan trọng để Godot hoạt động chính xác. Nó phải được phân phối cùng với tệp thực thi Godot.

Editor
~~~~~~

Tên của thư mục dữ liệu dành cho Godot editor sẽ luôn là ``GodotSharp``. Thư mục này chứa một thư mục con ``Api`` với các assembly API của Godot và một thư mục con ``Tools`` với các công cụ cần thiết cho editor, chẳng hạn như các assembly ``GodotTools`` và các phần phụ thuộc của chúng.

Trên macOS, nếu Godot editor được phân phối dưới dạng bundle, thư mục ``GodotSharp`` có thể được đặt trong thư mục ``<bundle_name>.app/Contents/Resources/`` bên trong bundle.

Các template export
~~~~~~~~~~~~~~~~~~~

Thư mục dữ liệu cho các project đã export được editor tạo trong quá trình export. Thư mục này có tên ``data_<APPNAME>_<ARCH>``, trong đó ``<APPNAME>`` là tên ứng dụng được chỉ định trong project setting ``application/config/name`` và ``<ARCH>`` là kiến trúc hiện tại của bản export.

Trong trường hợp export đa kiến trúc, nhiều thư mục dữ liệu như vậy sẽ được tạo.

Các tùy chọn dòng lệnh
----------------------

Sau đây là danh sách các tùy chọn dòng lệnh có sẵn khi build với module .NET:

- **module_mono_enabled**\ =yes | **no**

  - Build Godot với module .NET được bật.
