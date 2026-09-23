.. _doc_exporting_for_macos:

Xuất cho macOS
==============

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang macOS. Nếu bạn muốn biên dịch editor hoặc các binary export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_macos`.

Các ứng dụng macOS được xuất bằng export template chính thức sẽ được xuất dưới dạng một bundle binary "Universal 2" duy nhất ``.app``, một thư mục có cấu trúc cụ thể dùng để lưu executable, libraries và toàn bộ tệp dự án. Bundle này có thể được xuất nguyên trạng, đóng gói trong một kho lưu trữ ZIP hoặc đóng gói trong ảnh đĩa DMG (chỉ được hỗ trợ khi xuất từ macOS). `Universal binary cho macOS hỗ trợ cả hai kiến trúc Intel x86_64 và ARM64 (Apple Silicon) <https://developer.apple.com/documentation/apple-silicon/building-a-universal-macos-binary>`__.

.. warning::
    Do các hạn chế của hệ thống tệp, các bundle ``.app`` được xuất từ Windows không có cờ ``executable`` và sẽ không chạy trên macOS. Các dự án được xuất dưới dạng ``.zip`` không bị ảnh hưởng bởi vấn đề này. Để chạy các bundle ``.app`` được xuất từ Windows trên macOS, hãy chuyển ``.app`` sang một thiết bị chạy macOS hoặc Linux và dùng lệnh terminal ``chmod +x {executable_name}`` để thêm quyền ``executable``. Executable chính nằm trong thư mục con ``Contents/MacOS/``, cũng như các executable trợ giúp tùy chọn trong thư mục con ``Contents/Helpers/``, phải có quyền ``executable`` để bundle ``.app`` hợp lệ.

Yêu cầu
-------

-  Tải các export template của Godot. Sử dụng menu Godot: ``Editor > Manage Export Templates``.
-  Phải đặt một ``Bundle identifier`` hợp lệ và duy nhất trong phần ``Application`` của các tùy chọn export.

.. note::

    Một bundle ID hợp lệ chỉ có thể chứa các ký tự chữ và số, dấu gạch nối và dấu chấm (``A-Z``, ``a-z``, ``0-9``, ``-`` và ``.``). Apple khuyến nghị sử dụng định dạng reverse-DNS (ví dụ: ``com.example.your-game``) của một domain do bạn sở hữu, để đảm bảo bundle ID của bạn là duy nhất. Bundle ID không phân biệt chữ hoa chữ thường. Xem `CFBundleIdentifier <https://developer.apple.com/documentation/bundleresources/information-property-list/cfbundleidentifier>`__.

.. warning::

    Các dự án được xuất mà không có code signing và notarization sẽ bị Gatekeeper chặn nếu được tải xuống từ các nguồn không xác định; xem trang :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết thêm thông tin.

Code signing và notarization
----------------------------

Theo mặc định, macOS chỉ chạy các ứng dụng đã được ký và notarized. Nếu bạn sử dụng cấu hình signing khác, hãy xem :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết các cách khắc phục.

Để notarize một ứng dụng, bạn **phải** có một `Apple Developer ID Certificate <https://developer.apple.com/>`__ hợp lệ.

Nếu bạn có Apple Developer ID Certificate và xuất từ macOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cài đặt công cụ dòng lệnh `Xcode <https://developer.apple.com/xcode/>`__ và mở Xcode ít nhất một lần hoặc chạy lệnh ``sudo xcodebuild -license accept`` để chấp nhận thỏa thuận cấp phép.

Để ký ứng dụng đã xuất
^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``Xcode codesign`` trong tùy chọn ``Code Signing > Codesign``.
- Đặt danh tính certificate Apple ID hợp lệ ("Common Name" của certificate) trong phần ``Code Signing > Identity``.

Để notarize ứng dụng đã xuất
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``Xcode notarytool`` trong tùy chọn ``Notarization > Notarization``.
- Tắt entitlement ``Debugging``.
- Đặt thông tin đăng nhập Apple ID / mật khẩu dành riêng cho ứng dụng hợp lệ hoặc UUID / Key API của `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ trong phần ``Notarization``.

Bạn có thể sử dụng lệnh ``xcrun notarytool history`` để kiểm tra trạng thái notarization và lệnh ``xcrun notarytool log {ID}`` để tải nhật ký notarization xuống.

Nếu gặp vấn đề về notarization, hãy xem `Resolving common notarization issues <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/resolving_common_notarization_issues>`__ để biết thêm thông tin.

Sau khi hoàn tất notarization, `gắn ticket <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/customizing_the_notarization_workflow>`__ vào dự án đã xuất.

Nếu bạn có Apple Developer ID Certificate và xuất từ Linux hoặc Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cài đặt `rcodesign <https://github.com/indygreg/apple-platform-rs/tree/main/apple-codesign>`__ và cấu hình đường dẫn đến ``rcodesign`` trong tùy chọn ``Editor Settings > Export > macOS > rcodesign``.

Để ký ứng dụng đã xuất
^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``rcodesign`` trong tùy chọn ``Code Signing > Codesign``.
- Đặt tệp certificate PKCS #12 và mật khẩu Apple ID hợp lệ trong phần ``Code Signing``.

Để notarize ứng dụng đã xuất
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Chọn ``rcodesign`` trong tùy chọn ``Notarization > Notarization``.
- Tắt entitlement ``Debugging``.
- Đặt UUID / Key API `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ hợp lệ trong phần ``Notarization``.

Bạn có thể sử dụng lệnh ``rcodesign notary-log`` để kiểm tra trạng thái notarization.

Sau khi hoàn tất notarization, sử dụng lệnh ``rcodesign staple`` để gắn ticket vào dự án đã xuất.

Nếu bạn không có Apple Developer ID Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Chọn ``Built-in (ad-hoc only)`` trong tùy chọn ``Code Signing > Codesign``.
- Chọn ``Disabled`` trong tùy chọn ``Notarization > Notarization``.

Trong trường hợp này, Godot sẽ sử dụng chữ ký ad-hoc, giúp người dùng cuối dễ chạy ứng dụng đã xuất hơn; xem trang :ref:`Running Godot apps on macOS <doc_running_on_macos>` để biết thêm thông tin.

Tùy chọn signing
~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+
| Tùy chọn             | Mô tả                                                                                   |
+======================+=========================================================================================+
| Codesign             | Công cụ được sử dụng cho code signing.                                                  |
+----------------------+-----------------------------------------------------------------------------------------+
| Identity             | "Full Name" hoặc "Common Name" của signing identity được lưu trong macOS keychain. [1]_ |
+----------------------+-----------------------------------------------------------------------------------------+
| Tệp certificate      | Tệp certificate PKCS #12. [2]_                                                          |
+----------------------+-----------------------------------------------------------------------------------------+
| Mật khẩu certificate | Mật khẩu cho tệp chứng chỉ. [2]_                                                        |
+----------------------+-----------------------------------------------------------------------------------------+
| Custom Options       | Mảng các đối số dòng lệnh được truyền cho công cụ ký mã.                                |
+----------------------+-----------------------------------------------------------------------------------------+

.. [1] Tùy chọn này chỉ hiển thị khi ký bằng Xcode codesign.
.. [2] Các tùy chọn này chỉ hiển thị khi ký bằng rcodesign.

Tùy chọn notarization
~~~~~~~~~~~~~~~~~~~~~

+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Option            | Description                                                                                                                                                                              |
+===================+==========================================================================================================================================================================================+
| Notarization      | Công cụ dùng cho notarization.                                                                                                                                                           |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple ID Name     | Tên tài khoản Apple ID (địa chỉ email). [3]_                                                                                                                                             |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple ID Password | Mật khẩu dành riêng cho ứng dụng của Apple ID. Xem `Using app-specific passwords <https://support.apple.com/en-us/HT204397>`__ để bật xác thực hai yếu tố và tạo mật khẩu ứng dụng. [3]_ |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple Team ID     | Team ID ("Organization Unit"), nếu Apple ID của bạn thuộc nhiều team (tùy chọn). [3]_                                                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| API UUID          | UUID của nhà phát hành API `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ của Apple.                                                               |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| API Key           | API key `App Store Connect <https://developer.apple.com/documentation/appstoreconnectapi>`__ của Apple.                                                                                  |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

    Bạn nên đặt Apple ID Name/Password hoặc App Store Connect API UUID/Key.

.. [3] Các tùy chọn này chỉ hiển thị khi thực hiện notarization bằng Xcode notarytool.

Xem `Notarizing macOS Software Before Distribution <https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution?language=objc>`__ để biết thêm thông tin.

Entitlements
------------

Hardened Runtime Entitlements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hardened Runtime entitlements quản lý các tùy chọn bảo mật và chính sách truy cập tài nguyên. Xem `Hardened Runtime <https://developer.apple.com/documentation/security/hardened_runtime?language=objc>`__ để biết thêm thông tin.

+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Entitlement                           | Description                                                                                                                                                                                           |
+=======================================+=======================================================================================================================================================================================================+
| Allow JIT Code Execution [4]_         | Cho phép tạo bộ nhớ có thể ghi và thực thi cho mã JIT. Nếu bạn sử dụng các add-on có mã native động hoặc tự sửa đổi, hãy bật chúng theo tài liệu của add-on.                                          |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Allow Unsigned Executable Memory [4]_ | Cho phép tạo bộ nhớ có thể ghi và thực thi mà không bị giới hạn JIT. Nếu bạn sử dụng các add-on có mã native động hoặc tự sửa đổi, hãy bật chúng theo tài liệu của add-on.                            |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Allow DYLD Environment Variables [4]_ | Cho phép ứng dụng sử dụng các biến môi trường của dynamic linker để chèn mã. Nếu bạn sử dụng các add-on có mã native động hoặc tự sửa đổi, hãy bật chúng theo tài liệu của add-on.                    |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Disable Library Validation            | Cho phép ứng dụng tải các thư viện và framework tùy ý. Hãy bật tùy chọn này nếu bạn sử dụng các add-on GDExtension hoặc ad-hoc signing, hoặc muốn hỗ trợ các add-on bên ngoài do người dùng cung cấp. |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Audio Input                           | Bật nếu bạn cần sử dụng microphone hoặc các nguồn đầu vào âm thanh khác; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/microphone_usage_description`.                 |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Camera                                | Bật nếu bạn cần sử dụng camera; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/camera_usage_description`.                                                              |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Location                              | Bật nếu bạn cần sử dụng thông tin vị trí từ Location Services; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/location_usage_description`.                             |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Address Book                          | [5]_ Bật để cho phép truy cập danh bạ trong address book của người dùng; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/address_book_usage_description`.               |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Calendars                             | [5]_ Bật để cho phép truy cập lịch của người dùng; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/calendar_usage_description`.                                         |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Photo Library                         | [5]_ Bật để cho phép truy cập thư viện Photos của người dùng; nếu được bật, bạn cũng nên cung cấp thông báo sử dụng trong tùy chọn `privacy/photos_library_usage_description`.                        |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Apple Events                          | [5]_ Bật để cho phép ứng dụng gửi Apple events đến các ứng dụng khác.                                                                                                                                 |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Debugging                             | [6]_ Bạn có thể tạm thời bật entitlement này để sử dụng native debugger (GDB, LLDB) với ứng dụng đã export. Entitlement này nên được tắt khi export cho môi trường production.                        |
+---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. [4] Các entitlement ``Allow JIT Code Execution``, ``Allow Unsigned Executable Memory`` và ``Allow DYLD Environment Variables`` luôn được bật cho các bản export Godot Mono và không hiển thị trong các tùy chọn export.
.. [5] Godot không hỗ trợ sẵn các tính năng này; chỉ bật chúng nếu bạn đang sử dụng các add-on yêu cầu chúng.
.. [6] Để notarize một ứng dụng, bạn phải tắt entitlement ``Debugging``.

App Sandbox Entitlement
~~~~~~~~~~~~~~~~~~~~~~~

App Sandbox hạn chế quyền truy cập vào dữ liệu người dùng, mạng và thiết bị. Các ứng dụng trong sandbox không thể truy cập hầu hết hệ thống tệp, không thể sử dụng hộp thoại tệp tùy chỉnh và thực thi binary (bằng ``OS.execute`` và ``OS.create_process``) bên ngoài bundle ``.app``. Xem `App Sandbox <https://developer.apple.com/documentation/security/app_sandbox?language=objc>`__ để biết thêm thông tin.

.. note::

    Để phân phối ứng dụng thông qua App Store, bạn phải bật App Sandbox.

+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Entitlement              | Description                                                                                                                   |
+==========================+===============================================================================================================================+
| Enabled                  | Bật App Sandbox.                                                                                                              |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Network Server           | Bật để cho phép ứng dụng lắng nghe các kết nối mạng đến.                                                                      |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Network Client           | Bật để cho phép ứng dụng thiết lập các kết nối mạng đi.                                                                       |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Device USB               | Bật để cho phép ứng dụng tương tác với các thiết bị USB. Entitlement này là bắt buộc để sử dụng tay cầm có dây.               |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Device Bluetooth         | Bật để cho phép ứng dụng tương tác với các thiết bị Bluetooth. Entitlement này là bắt buộc để sử dụng tay cầm không dây.      |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Files Downloads [7]_     | Cho phép quyền đọc hoặc ghi vào thư mục "Downloads" của người dùng.                                                           |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Files Pictures [7]_      | Cho phép quyền đọc hoặc ghi vào thư mục "Pictures" của người dùng.                                                            |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Files Music [7]_         | Cho phép quyền đọc hoặc ghi vào thư mục "Music" của người dùng.                                                               |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Files Movies [7]_        | Cho phép quyền đọc hoặc ghi vào thư mục "Movies" của người dùng.                                                              |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Files User Selected [7]_ | Cho phép quyền đọc hoặc ghi vào một thư mục bất kỳ. Để cấp quyền truy cập, người dùng phải chọn thư mục từ hộp thoại tệp gốc. |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| Helper Executable        | Danh sách các helper executable được nhúng vào app bundle. Ứng dụng trong sandbox chỉ được phép thực thi các executable này.  |
+--------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. [7] Bạn có thể tùy chọn cung cấp thông báo sử dụng cho nhiều thư mục khác nhau trong các tùy chọn `privacy/*_folder_usage_description`.

.. note::

    Bạn có thể ghi đè các entitlement mặc định bằng cách chọn tệp entitlement tùy chỉnh; trong trường hợp này, mọi entitlement khác sẽ bị bỏ qua.

Environment variables
---------------------

Bạn có thể sử dụng các environment variable sau để thiết lập tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè những giá trị bạn đã đặt trong menu export.

.. list-table:: Environment variable cho bản export macOS
   :header-rows: 1

   * - Export option
     - Environment variable
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

Export options
--------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có trong
:ref:`class_EditorExportPlatformMacOS` class reference.
