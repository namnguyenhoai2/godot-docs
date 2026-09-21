:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/platform/linuxbsd/doc_classes/EditorExportPlatformLinuxBSD.xml.

.. _class_EditorExportPlatformLinuxBSD:

EditorExportPlatformLinuxBSD
============================

**Kế thừa:** :ref:`EditorExportPlatformPC<class_EditorExportPlatformPC>` **<** :ref:`EditorExportPlatform<class_EditorExportPlatform>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Trình export cho Linux/BSD.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Exporting for Linux <../tutorials/export/exporting_for_linux>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`binary_format/architecture<class_EditorExportPlatformLinuxBSD_property_binary_format/architecture>`             |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`binary_format/embed_pck<class_EditorExportPlatformLinuxBSD_property_binary_format/embed_pck>`                   |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`custom_template/debug<class_EditorExportPlatformLinuxBSD_property_custom_template/debug>`                       |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`custom_template/release<class_EditorExportPlatformLinuxBSD_property_custom_template/release>`                   |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`debug/export_console_wrapper<class_EditorExportPlatformLinuxBSD_property_debug/export_console_wrapper>`         |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`shader_baker/enabled<class_EditorExportPlatformLinuxBSD_property_shader_baker/enabled>`                         |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/cleanup_script<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/cleanup_script>` |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`ssh_remote_deploy/enabled<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/enabled>`               |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/extra_args_scp<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_scp>` |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/extra_args_ssh<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_ssh>` |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/host<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/host>`                     |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/port<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/port>`                     |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ssh_remote_deploy/run_script<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/run_script>`         |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`texture_format/etc2_astc<class_EditorExportPlatformLinuxBSD_property_texture_format/etc2_astc>`                 |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`texture_format/s3tc_bptc<class_EditorExportPlatformLinuxBSD_property_texture_format/s3tc_bptc>`                 |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorExportPlatformLinuxBSD_property_binary_format/architecture:

.. rst-class:: classref-property

:ref:`String<class_String>` **binary_format/architecture** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_binary_format/architecture>`

Kiến trúc của tệp thực thi ứng dụng.

Các kiến trúc được hỗ trợ: ``x86_32``, ``x86_64``, ``arm64``, ``arm32``, ``rv64``, ``ppc64`` và ``loongarch64``.

Các export template chính thức chỉ bao gồm các binary ``x86_32``, ``x86_64``, ``arm32`` và ``arm64``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_binary_format/embed_pck:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **binary_format/embed_pck** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_binary_format/embed_pck>`

Nếu ``true``, các tài nguyên của project sẽ được nhúng vào tệp thực thi.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_custom_template/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/debug** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_custom_template/debug>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_custom_template/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/release** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_custom_template/release>`

Đường dẫn đến export template tùy chỉnh. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_debug/export_console_wrapper:

.. rst-class:: classref-property

:ref:`int<class_int>` **debug/export_console_wrapper** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_debug/export_console_wrapper>`

Nếu ``true``, một console wrapper sẽ được export cùng với tệp thực thi chính, cho phép chạy project với console output được bật.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_shader_baker/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shader_baker/enabled** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_shader_baker/enabled>`

Nếu ``true``, các shader sẽ được biên dịch và nhúng vào ứng dụng. Tùy chọn này chỉ được hỗ trợ khi sử dụng Forward+ hoặc Mobile renderer.

\ **Lưu ý:** Khi export dưới dạng dedicated server, shader baker luôn bị tắt vì không thực hiện rendering.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/cleanup_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/cleanup_script** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/cleanup_script>`

Mã script sẽ được thực thi trên remote host khi ứng dụng kết thúc.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn đến thư mục tạm trên remote, được dùng để tải ứng dụng và các script lên đó.

- ``{archive_name}`` - Tên của ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của tệp thực thi ứng dụng.

- ``{cmd_args}`` - Mảng các command-line argument của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ssh_remote_deploy/enabled** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/enabled>`

Bật remote deploy bằng SSH/SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_scp:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_scp** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_scp>`

Mảng các command-line argument bổ sung được truyền cho SCP.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_ssh:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/extra_args_ssh** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/extra_args_ssh>`

Mảng các command-line argument bổ sung được truyền cho SSH.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/host:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/host** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/host>`

Tên người dùng SSH và địa chỉ của remote host, theo định dạng ``user@address``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/port:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/port** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/port>`

Số cổng SSH của remote host.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/run_script:

.. rst-class:: classref-property

:ref:`String<class_String>` **ssh_remote_deploy/run_script** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_ssh_remote_deploy/run_script>`

Mã script sẽ được thực thi trên remote host khi chạy ứng dụng.

Có thể sử dụng các biến sau trong script:

- ``{temp_dir}`` - Đường dẫn đến thư mục tạm trên remote, được dùng để tải ứng dụng và các script lên đó.

- ``{archive_name}`` - Tên của ZIP chứa ứng dụng đã tải lên.

- ``{exe_name}`` - Tên của tệp thực thi ứng dụng.

- ``{cmd_args}`` - Mảng các command-line argument của ứng dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_texture_format/etc2_astc:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **texture_format/etc2_astc** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_texture_format/etc2_astc>`

Nếu ``true``, texture của project sẽ được export ở định dạng ETC2/ASTC.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformLinuxBSD_property_texture_format/s3tc_bptc:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **texture_format/s3tc_bptc** :ref:`🔗<class_EditorExportPlatformLinuxBSD_property_texture_format/s3tc_bptc>`

Nếu ``true``, texture của project sẽ được export ở định dạng S3TC/BPTC.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
