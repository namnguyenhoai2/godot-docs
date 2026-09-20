.. _doc_exporting_for_macos:

Xuất cho macOS
==============

.. seealso::

    Trang này mô tả cách xuất một project Godot sang macOS. Nếu bạn muốn biên dịch binary của editor hoặc export template từ source thay vào đó, hãy đọc :ref:`doc_compiling_for_macos`.

Các ứng dụng macOS được xuất bằng export template chính thức sẽ được xuất dưới dạng một binary "Universal 2" duy nhất ``.app`` bundle, một thư mục có cấu trúc cụ thể dùng để lưu executable, library và tất cả tệp của project. Bundle này có thể được xuất nguyên trạng, đóng gói trong kho lưu trữ ZIP hoặc đóng gói trong disk image DMG (chỉ được hỗ trợ khi xuất từ macOS). `Universal binaries for macOS support both Intel x86_64 and ARM64 (Apple Silicon) architectures <https://developer.apple.com/documentation/apple-silicon/building-a-universal-macos-binary>`__.

.. warning::
    Do các giới hạn của hệ thống tệp, các bundle ``.app`` được xuất từ Windows không có flag ``executable`` và sẽ không chạy trên macOS. Các project được xuất dưới dạng ``.zip`` không bị ảnh hưởng bởi vấn đề này. Để chạy các bundle ``.app`` được xuất từ Windows trên macOS, hãy chuyển ``.app`` sang một thiết bị chạy macOS hoặc Linux và dùng lệnh terminal ``chmod +x {executable_name}`` để thêm quyền ``executable``. Executable chính nằm trong thư mục con ``Contents/MacOS/``, cũng như các executable trợ giúp tùy chọn trong thư mục con ``Contents/Helpers/``, phải có quyền ``executable`` để bundle ``.app`` hợp lệ.

Yêu cầu
-------

-  Tải xuống export template của Godot. Sử dụng menu Godot: ``Editor > Manage Export Templates``. - Một ``Bundle identifier`` hợp lệ và duy nhất phải được đặt trong phần ``Application`` của tùy chọn export.

.. note::

    Bundle ID hợp lệ chỉ có thể chứa các ký tự chữ và số, dấu gạch ngang và dấu chấm (``A-Z``, ``a-z``, ``0-9``, ``-`` và ``.``). Apple khuyến nghị sử dụng định dạng reverse-DNS (ví dụ: ``com.example.your-game``) của một domain mà bạn sở hữu, để đảm bảo bundle ID của bạn là duy nhất. Bundle ID không phân biệt chữ hoa chữ thường. Xem `CFBundleIdentifier <https://developer.apple.com/documentation/bundleresources/information-property-list/cfbundleidentifier>`__.

.. warning::

    Các project được xuất mà không có code signing và notarization sẽ bị Gatekeeper chặn nếu được tải xuống từ các nguồn không xác định; xem trang :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết thêm thông tin.

Code signing và notarization
----------------------------

Theo mặc định, macOS chỉ chạy các ứng dụng đã được ký và notarize. Nếu bạn sử dụng cấu hình signing khác, hãy xem :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết các cách xử lý.

Để notarize một app, bạn **phải** có một `Apple Developer ID Certificate <https://developer.apple.com/>`__ hợp lệ.

Nếu bạn có Apple Developer ID Certificate và xuất từ macOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cài đặt các công cụ dòng lệnh `Xcode <https://developer.apple.com/xcode/>`__ và mở Xcode ít nhất một lần hoặc chạy lệnh ``sudo xcodebuild -license accept`` để chấp nhận thỏa thuận cấp phép.

Để sign app đã xuất
^^^^^^^^^^^^^^^^^^^

- Chọn ``Xcode codesign`` trong tùy chọn ``Code Signing > Codesign``. - Đặt identity của Apple ID certificate hợp lệ (certificate "Common Name") trong phần ``Code Signing > Identity``.

Để notarize app đã xuất
^^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``Xcode notarytool`` trong tùy chọn ``Notarization > Notarization``. - Vô hiệu hóa entitlement ``Debugging``. - Đặt thông tin đăng nhập Apple ID / app-specific password hoặc `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ API UUID / Key hợp lệ trong phần ``Notarization``.

Bạn có thể dùng lệnh ``xcrun notarytool history`` để kiểm tra trạng thái notarization và dùng lệnh ``xcrun notarytool log {ID}`` để tải nhật ký notarization xuống.

Nếu gặp vấn đề với notarization, hãy xem `Resolving common notarization issues <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/resolving_common_notarization_issues>`__ để biết thêm thông tin.

Sau khi hoàn tất notarization, `staple the ticket <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/customizing_the_notarization_workflow>`__ vào project đã xuất.

Nếu bạn có Apple Developer ID Certificate và xuất từ Linux hoặc Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cài đặt `rcodesign <https://github.com/indygreg/apple-platform-rs/tree/main/apple-codesign>`__ và cấu hình đường dẫn đến ``rcodesign`` trong tùy chọn ``Editor Settings > Export > macOS > rcodesign``.

Để sign app đã xuất
^^^^^^^^^^^^^^^^^^^

- Chọn ``rcodesign`` trong tùy chọn ``Code Signing > Codesign``. - Đặt tệp certificate Apple ID PKCS #12 và password hợp lệ trong phần ``Code Signing``.

Để notarize app đã xuất
^^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``rcodesign`` trong tùy chọn ``Notarization > Notarization``. - Vô hiệu hóa entitlement ``Debugging``. - Đặt `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ API UUID / Key hợp lệ trong phần ``Notarization``.

Bạn có thể dùng lệnh ``rcodesign notary-log`` để kiểm tra trạng thái notarization.

Sau khi hoàn tất notarization, dùng lệnh ``rcodesign staple`` để staple ticket vào project đã xuất.

Nếu bạn không có Apple Developer ID Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Chọn ``Built-in (ad-hoc only)`` trong tùy chọn ``Code Signing > Codesign``. - Chọn ``Disabled`` trong tùy chọn ``Notarization > Notarization``.

Trong trường hợp này, Godot sẽ sử dụng chữ ký ad-hoc, giúp người dùng cuối dễ chạy app đã xuất hơn; xem trang :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết thêm thông tin.

Tùy chọn Signing
~~~~~~~~~~~~~~~~

+------------------------------+---------------------------------------------------------------------------------------------------+
| Option                       | Description                                                                                       |
+==============================+===================================================================================================+
| Codesign                     | Tool to use for code signing.                                                                     |
+------------------------------+---------------------------------------------------------------------------------------------------+
| Identity                     | The "Full Name" or "Common Name" of the signing identity, store in the macOS keychain. [1]_       |
+------------------------------+---------------------------------------------------------------------------------------------------+
| Certificate File             | The PKCS #12 certificate file. [2]_                                                               |
+------------------------------+---------------------------------------------------------------------------------------------------+
| Certificate Password         | Password for the certificate file. [2]_                                                           |
+------------------------------+---------------------------------------------------------------------------------------------------+
| Custom Options               | Array of command line arguments passed to the code signing tool.                                  |
+------------------------------+---------------------------------------------------------------------------------------------------+

.. [1] Tùy chọn này chỉ hiển thị khi signing bằng Xcode codesign.
.. [2] Các tùy chọn này chỉ hiển thị khi signing bằng rcodesign.

Tùy chọn Notarization
~~~~~~~~~~~~~~~~~~~~~

+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Option             | Description                                                                                                                                                                       |
+====================+===================================================================================================================================================================================+
| Notarization       | Tool to use for notarization.                                                                                                                                                     |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple ID Name      | Apple ID account name (email address). [3]_                                                                                                                                       |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple ID Password  | Apple ID app-specific password. See `Using app-specific passwords <https://support.apple.com/en-us/HT204397>`__ to enable two-factor authentication and create app password. [3]_ |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple Team ID      | Team ID ("Organization Unit"), if your Apple ID belongs to multiple teams (optional). [3]_                                                                                        |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| API UUID           | Apple `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ API issuer UUID.                                                                       |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| API Key            | Apple `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ API key.                                                                               |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

    Bạn nên đặt Apple ID Name/Password hoặc App Store Connect API UUID/Key.

.. [3] Các tùy chọn này chỉ hiển thị khi notarizing bằng Xcode notarytool.

Xem `Notarizing macOS Software Before Distribution <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution?language=objc>`__ để biết thêm thông tin.

Entitlement
-----------

Entitlement Hardened Runtime
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Entitlement Hardened Runtime quản lý các tùy chọn bảo mật và chính sách truy cập tài nguyên. Xem `Hardened Runtime <https://developer.apple.com/documentation/security/hardened_runtime?language=objc>`__ để biết thêm thông tin.

+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Entitlement                           | Description                                                                                                                                                                                      |
+=======================================+==================================================================================================================================================================================================+
| Allow JIT Code Execution [4]_         | Allows creating writable and executable memory for JIT code. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation.             |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Allow Unsigned Executable Memory [4]_ | Allows creating writable and executable memory without JIT restrictions. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation. |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Allow DYLD Environment Variables [4]_ | Allows app to use dynamic linker environment variables to inject code. If you are using add-ons with dynamic or self-modifying native code, enable them according to the add-on documentation.   |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Disable Library Validation            | Allows app to load arbitrary libraries and frameworks. Enable it if you are using GDExtension add-ons or ad-hoc signing, or want to support user-provided external add-ons.                      |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Audio Input                           | Enable if you need to use the microphone or other audio input sources, if it's enabled you should also provide usage message in the `privacy/microphone_usage_description` option.               |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Camera                                | Enable if you need to use the camera, if it's enabled you should also provide usage message in the `privacy/camera_usage_description` option.                                                    |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Location                              | Enable if you need to use location information from Location Services, if it's enabled you should also provide usage message in the `privacy/location_usage_description` option.                 |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Address Book                          | [5]_ Enable to allow access contacts in the user's address book, if it's enabled you should also provide usage message in the `privacy/address_book_usage_description` option.                   |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Calendars                             | [5]_ Enable to allow access to the user's calendar, if it's enabled you should also provide usage message in the `privacy/calendar_usage_description` option.                                    |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Photo Library                         | [5]_ Enable to allow access to the user's Photos library, if it's enabled you should also provide usage message in the `privacy/photos_library_usage_description` option.                        |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple Events                          | [5]_ Enable to allow app to send Apple events to other apps.                                                                                                                                     |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Debugging                             | [6]_ You can temporarily enable this entitlement to use native debugger (GDB, LLDB) with the exported app. This entitlement should be disabled for production export.                            |
+---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. [4] Các entitlement ``Allow JIT Code Execution``, ``Allow Unsigned Executable Memory`` và ``Allow DYLD Environment Variables`` luôn được bật cho các bản export Godot Mono và không hiển thị trong tùy chọn export.
.. [5] Các tính năng này không được Godot hỗ trợ sẵn; chỉ bật chúng nếu bạn sử dụng add-on yêu cầu chúng.
.. [6] Để notarize một app, bạn phải vô hiệu hóa entitlement ``Debugging``.

Entitlement App Sandbox
~~~~~~~~~~~~~~~~~~~~~~~

App Sandbox hạn chế quyền truy cập vào dữ liệu người dùng, mạng và thiết bị. Các app được sandbox không thể truy cập phần lớn hệ thống tệp, không thể sử dụng hộp thoại tệp tùy chỉnh và thực thi binary (bằng ``OS.execute`` và ``OS.create_process``) bên ngoài bundle ``.app``. Xem `App Sandbox <https://developer.apple.com/documentation/security/app_sandbox?language=objc>`__ để biết thêm thông tin.

.. note::

    Để phân phối một app thông qua App Store, bạn phải bật App Sandbox.

+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Entitlement                       | Description                                                                                                                          |
+===================================+======================================================================================================================================+
| Enabled                           | Enables App Sandbox.                                                                                                                 |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Network Server                    | Enable to allow app to listen for incoming network connections.                                                                      |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Network Client                    | Enable to allow app to establish outgoing network connections.                                                                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Device USB                        | Enable to allow app to interact with USB devices. This entitlement is required to use wired controllers.                             |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Device Bluetooth                  | Enable to allow app to interact with Bluetooth devices. This entitlement is required to use wireless controllers.                    |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Files Downloads [7]_              | Allows read or write access to the user's "Downloads" folder.                                                                        |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Files Pictures [7]_               | Allows read or write access to the user's "Pictures" folder.                                                                         |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Files Music [7]_                  | Allows read or write access to the user's "Music" folder.                                                                            |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Files Movies [7]_                 | Allows read or write access to the user's "Movies" folder.                                                                           |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Files User Selected [7]_          | Allows read or write access to arbitrary folder. To gain access, a folder must be selected from the native file dialog by the user.  |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
| Helper Executable                 | List of helper executables to embedded to the app bundle. Sandboxed app are limited to execute only these executable.                |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+

.. [7] Bạn có thể tùy chọn cung cấp thông báo sử dụng cho nhiều thư mục khác nhau trong các tùy chọn `privacy/*_folder_usage_description`.

.. note::

    Bạn có thể ghi đè entitlement mặc định bằng cách chọn tệp entitlement tùy chỉnh; trong trường hợp này, tất cả entitlement khác sẽ bị bỏ qua.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để đặt tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè những giá trị bạn đặt trong menu export.

.. list-table:: macOS export environment variables
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Options / Codesign / Certificate File
     - ``GODOT_MACOS_CODESIGN_CERTIFICATE_FILE``
   * - Options / Codesign / Certificate Password
     - ``GODOT_MACOS_CODESIGN_CERTIFICATE_PASSWORD``
   * - Options / Codesign / Provisioning Profile
     - ``GODOT_MACOS_CODESIGN_PROVISIONING_PROFILE``
   * - Options / Notarization / API UUID
     - ``GODOT_MACOS_NOTARIZATION_API_UUID``
   * - Options / Notarization / API Key
     - ``GODOT_MACOS_NOTARIZATION_API_KEY``
   * - Options / Notarization / API Key ID
     - ``GODOT_MACOS_NOTARIZATION_API_KEY_ID``
   * - Options / Notarization / Apple ID Name
     - ``GODOT_MACOS_NOTARIZATION_APPLE_ID_NAME``
   * - Options / Notarization / Apple ID Password
     - ``GODOT_MACOS_NOTARIZATION_APPLE_ID_PASSWORD``

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có sẵn trong
:ref:`class_EditorExportPlatformMacOS` class reference.
