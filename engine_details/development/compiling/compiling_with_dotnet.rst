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

.. note:: Hỗ trợ C# cho Godot trước đây sử dụng runtime `Mono <https://www.mono-project.com/>`_ thay vì `.NET Runtime <https://github.com/dotnet/runtime>`_, và nhiều thứ bên trong vẫn được đặt tên là ``mono`` thay vì ``dotnet`` hoặc được gọi theo cách khác là ``mono``.

Theo mặc định, module .NET bị tắt khi biên dịch. Để bật module này, hãy thêm tùy chọn ``module_mono_enabled=yes`` vào dòng lệnh SCons, đồng thời làm theo hướng dẫn biên dịch các binary Godot mong muốn.

Tạo glue
--------

Một phần mã nguồn của các thư viện managed được tạo từ ClassDB. Các tệp mã nguồn này phải được tạo trước khi biên dịch các thư viện managed. Bạn có thể tạo chúng bằng bất kỳ binary trình chỉnh sửa Godot nào đã bật .NET bằng cách chạy binary đó với các tham số ``--headless --generate-mono-glue``, theo sau là đường dẫn đến thư mục đầu ra. Đường dẫn này phải nằm ``modules/mono/glue`` trong thư mục Godot:

::

    <godot_binary> --headless --generate-mono-glue modules/mono/glue

Lệnh này yêu cầu Godot tạo các binding C# cho API Godot tại ``modules/mono/glue/GodotSharp/GodotSharp/Generated`` và các binding C# cho công cụ chỉnh sửa tại ``modules/mono/glue/GodotSharp/GodotSharpEditor/Generated``. Sau khi tạo các tệp này, bạn có thể biên dịch các thư viện managed của Godot cho tất cả target mong muốn mà không cần lặp lại quy trình này.

``<godot_binary>`` là binary trình chỉnh sửa mà bạn đã biên dịch với module .NET được bật. Tên chính xác sẽ khác nhau tùy theo hệ thống và cấu hình của bạn, nhưng thường có dạng ``bin/godot.<platform>.editor.<arch>.mono``, chẳng hạn như ``bin/godot.linuxbsd.editor.x86_64.mono`` hoặc ``bin/godot.windows.editor.x86_32.mono.exe``. Đặc biệt chú ý đến hậu tố **.mono**! Nếu trước đây bạn đã biên dịch Godot mà không có hỗ trợ .NET, có thể bạn cũng có các binary có tên tương tự nhưng không có hậu tố này. Không thể sử dụng các binary đó để tạo glue .NET.

.. note:: Phải tạo lại mã nguồn glue mỗi khi API được đăng ký trong ClassDB thay đổi. Ví dụ, điều này xảy ra khi một phương thức mới được đăng ký vào scripting API hoặc một trong các tham số của phương thức đó thay đổi. Godot sẽ in lỗi khi khởi động nếu có sự không khớp API giữa ClassDB và mã nguồn glue.

Biên dịch các thư viện managed
------------------------------

Sau khi tạo glue .NET, bạn có thể biên dịch các thư viện managed bằng script ``build_assemblies.py``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir=./bin

Nếu mọi việc diễn ra suôn sẻ, thư mục ``GodotSharp``, chứa các thư viện managed, sẽ được tạo trong thư mục ``bin``.

.. note:: Theo mặc định, tất cả các bản build development dùng chung một số phiên bản, điều này có thể gây ra một số vấn đề khi caching các package NuGet. Để giải quyết vấn đề này, hãy sử dụng ``GODOT_VERSION_STATUS`` để cung cấp cho mỗi bản build một phiên bản duy nhất hoặc xóa ``GodotNuGetFallbackFolder`` sau mỗi lần build để xóa package cache.

Không giống các bản build Godot "cổ điển", khi biên dịch với module .NET được bật (và tùy thuộc vào platform đích), một thư mục dữ liệu có thể được tạo cho cả trình chỉnh sửa và các project đã export. Thư mục này rất quan trọng để hoạt động đúng và phải được phân phối cùng với Godot. Có thêm thông tin chi tiết về thư mục này trong
:ref:`Thư mục dữ liệu <compiling_with_dotnet_data_directory>`.

Platform biên dịch
~~~~~~~~~~~~~~~~~~

Cung cấp đối số ``--godot-platform=<platform>`` để kiểm soát các thư viện được biên dịch dành cho platform cụ thể nào. Bỏ qua đối số này để biên dịch cho hệ thống hiện tại.

Hiện tại, tùy chọn này chỉ kiểm soát việc bao gồm hỗ trợ cho Visual Studio dưới dạng trình chỉnh sửa bên ngoài; các thư viện ansonsten giống hệt nhau.

Các package NuGet
~~~~~~~~~~~~~~~~~

Các assembly API, source generator và custom MSBuild project SDK được phân phối dưới dạng package NuGet. Người dùng không cần biết chi tiết này, nhưng nó có thể khiến việc development trở nên phức tạp.

Để sử dụng Godot với phiên bản development của các package đó, phải tạo một NuGet source cục bộ để MSBuild có thể tìm thấy chúng.

Trước tiên, hãy chọn vị trí cho NuGet source cục bộ. Nếu không có tùy chọn cụ thể, hãy tạo một thư mục trống tại một trong các vị trí được khuyến nghị sau:

- Trên Windows, ``C:\Users\<username>\MyLocalNugetSource``
- Trên Linux, \*BSD, v.v., ``~/MyLocalNugetSource``

Đường dẫn này sẽ được gọi là ``<my_local_source>`` ở các phần sau.

Sau khi chọn một thư mục, hãy chạy lệnh .NET CLI này để cấu hình NuGet sử dụng source cục bộ của bạn:

::

    dotnet nuget add source <my_local_source> --name MyLocalNugetSource

Khi chạy script ``build_assemblies.py``, hãy truyền ``<my_local_source>`` cho tùy chọn ``--push-nupkgs-local``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source>

Tùy chọn này đảm bảo các package được thêm vào NuGet source cục bộ đã chỉ định và các phiên bản package xung đột được xóa khỏi NuGet cache. Bạn nên luôn sử dụng tùy chọn này khi biên dịch các solution C# trong quá trình development để tránh sai sót.

Biên dịch mà không phụ thuộc vào các tính năng deprecated (NO_DEPRECATED)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi biên dịch Godot mà không có các class và function deprecated, tức là sử dụng đối số ``deprecated=no`` cho scons, các thư viện managed cũng phải được biên dịch mà không phụ thuộc vào mã deprecated. Thực hiện việc này bằng cách truyền đối số ``--no-deprecated``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --no-deprecated

Hỗ trợ độ chính xác kép (REAL_T_IS_DOUBLE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi biên dịch Godot với hỗ trợ độ chính xác kép, tức là sử dụng đối số ``precision=double`` cho scons, các thư viện managed phải được điều chỉnh cho phù hợp bằng cách truyền đối số ``--precision=double``:

::

    ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --precision=double

Ví dụ
-----

Ví dụ (Windows)
~~~~~~~~~~~~~~~

::

    # Build editor binary scons platform=windows target=editor module_mono_enabled=yes # Build export templates scons platform=windows target=template_debug module_mono_enabled=yes scons platform=windows target=template_release module_mono_enabled=yes

    # Generate glue sources bin/godot.windows.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue # Build .NET assemblies ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --godot-platform=windows


Ví dụ (Linux, \*BSD)
~~~~~~~~~~~~~~~~~~~~

::

    # Xây dựng binary editor scons platform=linuxbsd target=editor module_mono_enabled=yes # Xây dựng export template scons platform=linuxbsd target=template_debug module_mono_enabled=yes scons platform=linuxbsd target=template_release module_mono_enabled=yes

    # Tạo các source glue bin/godot.linuxbsd.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue # Tạo các binary ./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local <my_local_source> --godot-platform=linuxbsd

.. _compiling_with_dotnet_data_directory:

Thư mục dữ liệu
---------------

Thư mục dữ liệu là một dependency của các binary Godot được build với module .NET được bật. Thư mục này chứa các tệp quan trọng để Godot hoạt động đúng cách. Thư mục này phải được phân phối cùng với executable Godot.

Editor
~~~~~~

Tên của thư mục dữ liệu dành cho Godot editor sẽ luôn là ``GodotSharp``. Thư mục này chứa một thư mục con ``Api`` với các assembly API của Godot và một thư mục con ``Tools`` với các công cụ cần thiết cho editor, chẳng hạn như các assembly ``GodotTools`` và các dependency của chúng.

Trên macOS, nếu Godot editor được phân phối dưới dạng bundle, thư mục ``GodotSharp`` có thể được đặt trong thư mục ``<bundle_name>.app/Contents/Resources/`` bên trong bundle.

Export template
~~~~~~~~~~~~~~~

Thư mục dữ liệu dành cho các project đã export được editor tạo trong quá trình export. Thư mục này có tên ``data_<APPNAME>_<ARCH>``, trong đó ``<APPNAME>`` là tên ứng dụng được chỉ định trong project setting ``application/config/name`` và ``<ARCH>`` là architecture hiện tại của bản export.

Trong trường hợp export nhiều architecture, nhiều thư mục dữ liệu như vậy sẽ được tạo.

Các tùy chọn dòng lệnh
----------------------

Sau đây là danh sách các tùy chọn dòng lệnh có sẵn khi build với module .NET:

- **module_mono_enabled**\ =yes | **no**

  - Build Godot với module .NET được bật.

.. _`.NET SDK 8.0+`: https://dotnet.microsoft.com/download
.. _`Mono`: https://www.mono-project.com/
.. _`.NET Runtime`: https://github.com/dotnet/runtime
