:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/platform/windows/doc_classes/EditorExportPlatformWindows.xml.

.. _class_EditorExportPlatformWindows:

EditorExportPlatformWindows
===========================

**Kế thừa:** :ref:`EditorExportPlatformPC<class_EditorExportPlatformPC>` **<** :ref:`EditorExportPlatform<class_EditorExportPlatform>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Exporter cho Windows.

.. rst-class:: classref-introduction-group

Mô tả
-----

Windows exporter tùy chỉnh cách một bản build Windows được xử lý. Trong cửa sổ "Export" của editor, đối tượng này được tạo khi thêm một preset "Windows" mới.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Exporting for Windows <../tutorials/export/exporting_for_windows>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/company_name<class_EditorExportPlatformWindows_property_application/company_name>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/console_wrapper_icon<class_EditorExportPlatformWindows_property_application/console_wrapper_icon>`               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/copyright<class_EditorExportPlatformWindows_property_application/copyright>`                                     |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`application/d3d12_agility_sdk_multiarch<class_EditorExportPlatformWindows_property_application/d3d12_agility_sdk_multiarch>` |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`application/export_angle<class_EditorExportPlatformWindows_property_application/export_angle>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`application/export_d3d12<class_EditorExportPlatformWindows_property_application/export_d3d12>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/file_description<class_EditorExportPlatformWindows_property_application/file_description>`                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/file_version<class_EditorExportPlatformWindows_property_application/file_version>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/icon<class_EditorExportPlatformWindows_property_application/icon>`                                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`application/icon_interpolation<class_EditorExportPlatformWindows_property_application/icon_interpolation>`                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`application/modify_resources<class_EditorExportPlatformWindows_property_application/modify_resources>`                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/product_name<class_EditorExportPlatformWindows_property_application/product_name>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/product_version<class_EditorExportPlatformWindows_property_application/product_version>`                         |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`application/trademarks<class_EditorExportPlatformWindows_property_application/trademarks>`                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`binary_format/architecture<class_EditorExportPlatformWindows_property_binary_format/architecture>`                           |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`binary_format/embed_pck<class_EditorExportPlatformWindows_property_binary_format/embed_pck>`                                 |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`codesign/custom_options<class_EditorExportPlatformWindows_property_codesign/custom_options>`                                 |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/description<class_EditorExportPlatformWindows_property_codesign/description>`                                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/digest_algorithm<class_EditorExportPlatformWindows_property_codesign/digest_algorithm>`                             |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/enable<class_EditorExportPlatformWindows_property_codesign/enable>`                                                 |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/identity<class_EditorExportPlatformWindows_property_codesign/identity>`                                             |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`codesign/identity_type<class_EditorExportPlatformWindows_property_codesign/identity_type>`                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/password<class_EditorExportPlatformWindows_property_codesign/password>`                                             |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`codesign/timestamp<class_EditorExportPlatformWindows_property_codesign/timestamp>`                                           |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`codesign/timestamp_server_url<class_EditorExportPlatformWindows_property_codesign/timestamp_server_url>`                     |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/debug<class_EditorExportPlatformWindows_property_custom_template/debug>`                                     |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`custom_template/release<class_EditorExportPlatformWindows_property_custom_template/release>`                                 |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`debug/export_console_wrapper<class_EditorExportPlatformWindows_property_debug/export_console_wrapper>`                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`shader_baker/enabled<class_EditorExportPlatformWindows_property_shader_baker/enabled>`                                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/cleanup_script<class_EditorExportPlatformWindows_property_ssh_remote_deploy/cleanup_script>`               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`ssh_remote_deploy/enabled<class_EditorExportPlatformWindows_property_ssh_remote_deploy/enabled>`                             |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/extra_args_scp<class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_scp>`               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/extra_args_ssh<class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_ssh>`               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/host<class_EditorExportPlatformWindows_property_ssh_remote_deploy/host>`                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/port<class_EditorExportPlatformWindows_property_ssh_remote_deploy/port>`                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`ssh_remote_deploy/run_script<class_EditorExportPlatformWindows_property_ssh_remote_deploy/run_script>`                       |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`texture_format/etc2_astc<class_EditorExportPlatformWindows_property_texture_format/etc2_astc>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`texture_format/s3tc_bptc<class_EditorExportPlatformWindows_property_texture_format/s3tc_bptc>`                               |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorExportPlatformWindows_property_application/company_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/company_name** :ref:`🔗<class_EditorExportPlatformWindows_property_application/company_name>`

Công ty sản xuất ứng dụng. Bắt buộc. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/console_wrapper_icon:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/console_wrapper_icon** :ref:`🔗<class_EditorExportPlatformWindows_property_application/console_wrapper_icon>`

Tệp biểu tượng của console wrapper. Nếu để trống, sẽ fallback về :ref:`application/icon<class_EditorExportPlatformWindows_property_application/icon>`, sau đó đến :ref:`ProjectSettings.application/config/windows_native_icon<class_ProjectSettings_property_application/config/windows_native_icon>`, và cuối cùng là :ref:`ProjectSettings.application/config/icon<class_ProjectSettings_property_application/config/icon>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/copyright:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/copyright** :ref:`🔗<class_EditorExportPlatformWindows_property_application/copyright>`

Thông báo bản quyền của bundle hiển thị cho người dùng. Không bắt buộc. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/d3d12_agility_sdk_multiarch:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **application/d3d12_agility_sdk_multiarch** :ref:`🔗<class_EditorExportPlatformWindows_property_application/d3d12_agility_sdk_multiarch>`

Nếu ``true`` và :ref:`application/export_d3d12<class_EditorExportPlatformWindows_property_application/export_d3d12>` được đặt, các DLL của Agility SDK sẽ được lưu trong các thư mục con dành riêng cho từng kiến trúc.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/export_angle:

.. rst-class:: classref-property

:ref:`int<class_int>` **application/export_angle** :ref:`🔗<class_EditorExportPlatformWindows_property_application/export_angle>`

Nếu được đặt thành ``1``, các thư viện ANGLE sẽ được export cùng ứng dụng được export. Nếu được đặt thành ``0``, các thư viện ANGLE chỉ được export khi :ref:`ProjectSettings.rendering/gl_compatibility/driver<class_ProjectSettings_property_rendering/gl_compatibility/driver>` được đặt thành ``"opengl3_angle"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/export_d3d12:

.. rst-class:: classref-property

:ref:`int<class_int>` **application/export_d3d12** :ref:`🔗<class_EditorExportPlatformWindows_property_application/export_d3d12>`

Nếu được đặt thành ``1``, các thư viện runtime Direct3D 12 (Agility SDK, PIX) sẽ được export cùng ứng dụng được export. Nếu được đặt thành ``0``, các thư viện Direct3D 12 chỉ được export khi :ref:`ProjectSettings.rendering/rendering_device/driver<class_ProjectSettings_property_rendering/rendering_device/driver>` được đặt thành ``"d3d12"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/file_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/file_description** :ref:`🔗<class_EditorExportPlatformWindows_property_application/file_description>`

Mô tả tệp hiển thị cho người dùng. Bắt buộc. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/file_version:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/file_version** :ref:`🔗<class_EditorExportPlatformWindows_property_application/file_version>`

Số phiên bản của tệp. Nếu để trống, fallback về :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>`. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/icon:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/icon** :ref:`🔗<class_EditorExportPlatformWindows_property_application/icon>`

Tệp biểu tượng ứng dụng. Nếu để trống, sẽ fallback về :ref:`ProjectSettings.application/config/windows_native_icon<class_ProjectSettings_property_application/config/windows_native_icon>`, sau đó đến :ref:`ProjectSettings.application/config/icon<class_ProjectSettings_property_application/config/icon>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/icon_interpolation:

.. rst-class:: classref-property

:ref:`int<class_int>` **application/icon_interpolation** :ref:`🔗<class_EditorExportPlatformWindows_property_application/icon_interpolation>`

Phương pháp interpolation được sử dụng để thay đổi kích thước biểu tượng ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/modify_resources:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **application/modify_resources** :ref:`🔗<class_EditorExportPlatformWindows_property_application/modify_resources>`

Nếu được bật, biểu tượng và metadata của executable được export sẽ được đặt theo các giá trị ``application/*`` khác.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/product_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/product_name** :ref:`🔗<class_EditorExportPlatformWindows_property_application/product_name>`

Tên ứng dụng. Bắt buộc. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/product_version:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/product_version** :ref:`🔗<class_EditorExportPlatformWindows_property_application/product_version>`

Phiên bản ứng dụng hiển thị cho người dùng. Nếu để trống, fallback về :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>`. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_application/trademarks:

.. rst-class:: classref-property

:ref:`String<class_String>` **application/trademarks** :ref:`🔗<class_EditorExportPlatformWindows_property_application/trademarks>`

Các nhãn hiệu và nhãn hiệu đã đăng ký áp dụng cho tệp. Không bắt buộc. Xem `StringFileInfo <https://learn.microsoft.com/en-us/windows/win32/menurc/stringfileinfo-block>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_binary_format/architecture:

.. rst-class:: classref-property

:ref:`String<class_String>` **binary_format/architecture** :ref:`🔗<class_EditorExportPlatformWindows_property_binary_format/architecture>`

Kiến trúc executable của ứng dụng.

Các kiến trúc được hỗ trợ: ``x86_32``, ``x86_64`` và ``arm64``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_binary_format/embed_pck:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **binary_format/embed_pck** :ref:`🔗<class_EditorExportPlatformWindows_property_binary_format/embed_pck>`

Nếu ``true``, các tài nguyên của project được nhúng vào executable.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/custom_options:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **codesign/custom_options** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/custom_options>`

Mảng các đối số command line bổ sung được truyền cho công cụ code signing. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

**Lưu ý:** Mảng trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/description:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/description** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/description>`

Mô tả nội dung đã ký. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/digest_algorithm:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/digest_algorithm** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/digest_algorithm>`

Thuật toán digest được sử dụng để tạo chữ ký. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/enable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/enable** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/enable>`

Nếu ``true``, việc ký executable được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/identity:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/identity** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/identity>`

Tệp certificate PKCS #12 được sử dụng để ký executable hoặc hash SHA-1 của certificate (nếu :ref:`codesign/identity_type<class_EditorExportPlatformWindows_property_codesign/identity_type>` được đặt thành "Use certificate store"). Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

Có thể được ghi đè bằng biến môi trường ``GODOT_WINDOWS_CODESIGN_IDENTITY``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/identity_type:

.. rst-class:: classref-property

:ref:`int<class_int>` **codesign/identity_type** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/identity_type>`

Loại identity được sử dụng. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

Có thể được ghi đè bằng biến môi trường ``GODOT_WINDOWS_CODESIGN_IDENTITY_TYPE``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/password:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/password** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/password>`

Mật khẩu của tệp certificate được sử dụng để ký executable. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

Có thể được ghi đè bằng biến môi trường ``GODOT_WINDOWS_CODESIGN_PASSWORD``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/timestamp:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **codesign/timestamp** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/timestamp>`

Nếu ``true``, dấu thời gian được thêm vào chữ ký. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_codesign/timestamp_server_url:

.. rst-class:: classref-property

:ref:`String<class_String>` **codesign/timestamp_server_url** :ref:`🔗<class_EditorExportPlatformWindows_property_codesign/timestamp_server_url>`

URL của máy chủ dấu thời gian. Nếu để trống, máy chủ mặc định sẽ được sử dụng. Xem `Sign Tool <https://learn.microsoft.com/en-us/dotnet/framework/tools/signtool-exe>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_custom_template/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/debug** :ref:`🔗<class_EditorExportPlatformWindows_property_custom_template/debug>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_custom_template/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/release** :ref:`🔗<class_EditorExportPlatformWindows_property_custom_template/release>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_debug/export_console_wrapper:

.. rst-class:: classref-property

:ref:`int<class_int>` **debug/export_console_wrapper** :ref:`🔗<class_EditorExportPlatformWindows_property_debug/export_console_wrapper>`

Nếu ``true``, một console wrapper executable sẽ được export cùng executable chính, cho phép chạy project với console output được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_shader_baker/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shader_baker/enabled** :ref:`🔗<class_EditorExportPlatformWindows_property_shader_baker/enabled>`

Nếu ``true``, các shader sẽ được compile và nhúng vào ứng dụng. Tùy chọn này chỉ được hỗ trợ khi sử dụng các renderer Forward+ và Mobile.

\ **Lưu ý:** Khi export dưới dạng dedicated server, shader baker luôn bị tắt vì không thực hiện rendering.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/cleanup_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/cleanup_script** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/cleanup_script>`

Mã script được thực thi trên remote host khi ứng dụng hoàn tất.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn của thư mục tạm trên remote, được sử dụng để tải ứng dụng và các script lên.

- ``{archive_name}`` - Tên của ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của executable ứng dụng.

- ``{cmd_args}`` - Mảng các đối số command line của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ssh_remote_deploy/enabled** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/enabled>`

Bật remote deploy bằng SSH/SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_scp:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_scp** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_scp>`

Mảng các đối số command line bổ sung được truyền cho SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_ssh:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_ssh** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/extra_args_ssh>`

Mảng các đối số command line bổ sung được truyền cho SSH.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/host:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/host** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/host>`

Tên người dùng SSH và địa chỉ của remote host, theo định dạng ``user@address``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/port:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/port** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/port>`

Số cổng SSH của remote host.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_ssh_remote_deploy/run_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/run_script** :ref:`🔗<class_EditorExportPlatformWindows_property_ssh_remote_deploy/run_script>`

Mã script được thực thi trên remote host khi chạy ứng dụng.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn của thư mục tạm trên remote, được sử dụng để tải ứng dụng và các script lên.

- ``{archive_name}`` - Tên của ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của executable ứng dụng.

- ``{cmd_args}`` - Mảng các đối số dòng lệnh của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_texture_format/etc2_astc:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **texture_format/etc2_astc** :ref:`🔗<class_EditorExportPlatformWindows_property_texture_format/etc2_astc>`

Nếu ``true``, texture của dự án sẽ được xuất ở định dạng ETC2/ASTC.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWindows_property_texture_format/s3tc_bptc:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **texture_format/s3tc_bptc** :ref:`🔗<class_EditorExportPlatformWindows_property_texture_format/s3tc_bptc>`

Nếu ``true``, texture của dự án sẽ được xuất ở định dạng S3TC/BPTC.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
