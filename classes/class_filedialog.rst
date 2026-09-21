:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FileDialog.xml.

.. _class_FileDialog:

FileDialog
==========

**Kế thừa:** :ref:`ConfirmationDialog<class_ConfirmationDialog>` **<** :ref:`AcceptDialog<class_AcceptDialog>` **<** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`EditorFileDialog<class_EditorFileDialog>`

Một dialog để chọn tệp hoặc thư mục trong hệ thống tệp.

.. rst-class:: classref-introduction-group

Mô tả
-----

**FileDialog** là một dialog được định sẵn, dùng để chọn tệp và thư mục trong hệ thống tệp. Dialog này hỗ trợ các filter mask. **FileDialog** tự động đặt tiêu đề cửa sổ theo :ref:`file_mode<class_FileDialog_property_file_mode>`. Nếu muốn sử dụng tiêu đề tùy chỉnh, hãy tắt tính năng này bằng cách đặt :ref:`mode_overrides_title<class_FileDialog_property_mode_overrides_title>` thành ``false``.

\ **Lưu ý:** **FileDialog** mặc định bị ẩn. Để hiển thị nó, hãy gọi một trong các phương thức ``popup_*`` từ :ref:`Window<class_Window>` trên node, chẳng hạn như :ref:`Window.popup_centered_clamped()<class_Window_method_popup_centered_clamped>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`Access<enum_FileDialog_Access>`             | :ref:`access<class_FileDialog_property_access>`                                           | ``0``                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`current_dir<class_FileDialog_property_current_dir>`                                 |                                                                                          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`current_file<class_FileDialog_property_current_file>`                               |                                                                                          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`current_path<class_FileDialog_property_current_path>`                               |                                                                                          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`deleting_enabled<class_FileDialog_property_deleting_enabled>`                       | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | dialog_hide_on_ok                                                                         | ``false`` (overrides :ref:`AcceptDialog<class_AcceptDialog_property_dialog_hide_on_ok>`) |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`DisplayMode<enum_FileDialog_DisplayMode>`   | :ref:`display_mode<class_FileDialog_property_display_mode>`                               | ``0``                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`favorites_enabled<class_FileDialog_property_favorites_enabled>`                     | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`file_filter_toggle_enabled<class_FileDialog_property_file_filter_toggle_enabled>`   | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`FileMode<enum_FileDialog_FileMode>`         | :ref:`file_mode<class_FileDialog_property_file_mode>`                                     | ``4``                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`file_sort_options_enabled<class_FileDialog_property_file_sort_options_enabled>`     | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`filename_filter<class_FileDialog_property_filename_filter>`                         | ``""``                                                                                   |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`filters<class_FileDialog_property_filters>`                                         | ``PackedStringArray()``                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`folder_creation_enabled<class_FileDialog_property_folder_creation_enabled>`         | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`hidden_files_toggle_enabled<class_FileDialog_property_hidden_files_toggle_enabled>` | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`layout_toggle_enabled<class_FileDialog_property_layout_toggle_enabled>`             | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`mode_overrides_title<class_FileDialog_property_mode_overrides_title>`               | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`option_count<class_FileDialog_property_option_count>`                               | ``0``                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`option_{index}/default<class_FileDialog_property_option_{index}/default>`           | ``0``                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`option_{index}/name<class_FileDialog_property_option_{index}/name>`                 | ``""``                                                                                   |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`option_{index}/values<class_FileDialog_property_option_{index}/values>`             | ``PackedStringArray()``                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`overwrite_warning_enabled<class_FileDialog_property_overwrite_warning_enabled>`     | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`recent_list_enabled<class_FileDialog_property_recent_list_enabled>`                 | ``true``                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`root_subfolder<class_FileDialog_property_root_subfolder>`                           | ``""``                                                                                   |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`show_hidden_files<class_FileDialog_property_show_hidden_files>`                     | ``false``                                                                                |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>`                   | size                                                                                      | ``Vector2i(640, 360)`` (overrides :ref:`Window<class_Window_property_size>`)             |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | title                                                                                     | ``"Save a File"`` (overrides :ref:`Window<class_Window_property_title>`)                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`use_native_dialog<class_FileDialog_property_use_native_dialog>`                     | ``false``                                                                                |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_filter<class_FileDialog_method_add_filter>`\ (\ filter\: :ref:`String<class_String>`, description\: :ref:`String<class_String>` = "", mime_type\: :ref:`String<class_String>` = ""\ )          |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_option<class_FileDialog_method_add_option>`\ (\ name\: :ref:`String<class_String>`, values\: :ref:`PackedStringArray<class_PackedStringArray>`, default_value_index\: :ref:`int<class_int>`\ ) |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`clear_filename_filter<class_FileDialog_method_clear_filename_filter>`\ (\ )                                                                                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`clear_filters<class_FileDialog_method_clear_filters>`\ (\ )                                                                                                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`deselect_all<class_FileDialog_method_deselect_all>`\ (\ )                                                                                                                                          |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_favorite_list<class_FileDialog_method_get_favorite_list>`\ (\ ) |static|                                                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`LineEdit<class_LineEdit>`                   | :ref:`get_line_edit<class_FileDialog_method_get_line_edit>`\ (\ )                                                                                                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_option_default<class_FileDialog_method_get_option_default>`\ (\ option\: :ref:`int<class_int>`\ ) |const|                                                                                      |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_option_name<class_FileDialog_method_get_option_name>`\ (\ option\: :ref:`int<class_int>`\ ) |const|                                                                                            |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_option_values<class_FileDialog_method_get_option_values>`\ (\ option\: :ref:`int<class_int>`\ ) |const|                                                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_recent_list<class_FileDialog_method_get_recent_list>`\ (\ ) |static|                                                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`get_selected_options<class_FileDialog_method_get_selected_options>`\ (\ ) |const|                                                                                                                  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`VBoxContainer<class_VBoxContainer>`         | :ref:`get_vbox<class_FileDialog_method_get_vbox>`\ (\ )                                                                                                                                                  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`invalidate<class_FileDialog_method_invalidate>`\ (\ )                                                                                                                                              |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_customization_flag_enabled<class_FileDialog_method_is_customization_flag_enabled>`\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|                                    |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`popup_file_dialog<class_FileDialog_method_popup_file_dialog>`\ (\ )                                                                                                                                |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_customization_flag_enabled<class_FileDialog_method_set_customization_flag_enabled>`\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ )       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_favorite_list<class_FileDialog_method_set_favorite_list>`\ (\ favorites\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |static|                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_get_icon_callback<class_FileDialog_method_set_get_icon_callback>`\ (\ callback\: :ref:`Callable<class_Callable>`\ ) |static|                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_get_thumbnail_callback<class_FileDialog_method_set_get_thumbnail_callback>`\ (\ callback\: :ref:`Callable<class_Callable>`\ ) |static|                                                         |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_option_default<class_FileDialog_method_set_option_default>`\ (\ option\: :ref:`int<class_int>`, default_value_index\: :ref:`int<class_int>`\ )                                                 |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_option_name<class_FileDialog_method_set_option_name>`\ (\ option\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ )                                                                |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_option_values<class_FileDialog_method_set_option_values>`\ (\ option\: :ref:`int<class_int>`, values\: :ref:`PackedStringArray<class_PackedStringArray>`\ )                                    |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_recent_list<class_FileDialog_method_set_recent_list>`\ (\ recents\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |static|                                                              |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`         | :ref:`file_disabled_color<class_FileDialog_theme_color_file_disabled_color>`            | ``Color(1, 1, 1, 0.25)`` |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`         | :ref:`file_icon_color<class_FileDialog_theme_color_file_icon_color>`                    | ``Color(1, 1, 1, 1)``    |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`         | :ref:`folder_icon_color<class_FileDialog_theme_color_folder_icon_color>`                | ``Color(1, 1, 1, 1)``    |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`             | :ref:`thumbnail_size<class_FileDialog_theme_constant_thumbnail_size>`                   | ``64``                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`back_folder<class_FileDialog_theme_icon_back_folder>`                             |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`create_folder<class_FileDialog_theme_icon_create_folder>`                         |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`favorite<class_FileDialog_theme_icon_favorite>`                                   |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`favorite_down<class_FileDialog_theme_icon_favorite_down>`                         |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`favorite_up<class_FileDialog_theme_icon_favorite_up>`                             |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`file<class_FileDialog_theme_icon_file>`                                           |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`file_thumbnail<class_FileDialog_theme_icon_file_thumbnail>`                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`folder<class_FileDialog_theme_icon_folder>`                                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`folder_thumbnail<class_FileDialog_theme_icon_folder_thumbnail>`                   |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`forward_folder<class_FileDialog_theme_icon_forward_folder>`                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`list_mode<class_FileDialog_theme_icon_list_mode>`                                 |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_copy_path<class_FileDialog_theme_icon_menu_copy_path>`                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_delete<class_FileDialog_theme_icon_menu_delete>`                             |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_new_folder<class_FileDialog_theme_icon_menu_new_folder>`                     |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_open_bundle<class_FileDialog_theme_icon_menu_open_bundle>`                   |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_refresh<class_FileDialog_theme_icon_menu_refresh>`                           |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`menu_show_in_file_manager<class_FileDialog_theme_icon_menu_show_in_file_manager>` |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`parent_folder<class_FileDialog_theme_icon_parent_folder>`                         |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`reload<class_FileDialog_theme_icon_reload>`                                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`sort<class_FileDialog_theme_icon_sort>`                                           |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`thumbnail_mode<class_FileDialog_theme_icon_thumbnail_mode>`                       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`toggle_filename_filter<class_FileDialog_theme_icon_toggle_filename_filter>`       |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`toggle_hidden<class_FileDialog_theme_icon_toggle_hidden>`                         |                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_FileDialog_signal_dir_selected:

.. rst-class:: classref-signal

**dir_selected**\ (\ dir\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileDialog_signal_dir_selected>`

Được phát khi người dùng chọn một thư mục.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_signal_file_selected:

.. rst-class:: classref-signal

**file_selected**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileDialog_signal_file_selected>`

Được phát khi người dùng chọn một tệp bằng cách nhấp đúp vào tệp đó hoặc nhấn nút **OK**.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_signal_filename_filter_changed:

.. rst-class:: classref-signal

**filename_filter_changed**\ (\ filter\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileDialog_signal_filename_filter_changed>`

Được phát khi filter cho tên tệp thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_signal_files_selected:

.. rst-class:: classref-signal

**files_selected**\ (\ paths\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_FileDialog_signal_files_selected>`

Được phát khi người dùng chọn nhiều tệp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_FileDialog_FileMode:

.. rst-class:: classref-enumeration

enum **FileMode**: :ref:`🔗<enum_FileDialog_FileMode>`

.. _class_FileDialog_constant_FILE_MODE_OPEN_FILE:

.. rst-class:: classref-enumeration-constant

:ref:`FileMode<enum_FileDialog_FileMode>` **FILE_MODE_OPEN_FILE** = ``0``

Dialog cho phép chọn một và chỉ một tệp.

.. _class_FileDialog_constant_FILE_MODE_OPEN_FILES:

.. rst-class:: classref-enumeration-constant

:ref:`FileMode<enum_FileDialog_FileMode>` **FILE_MODE_OPEN_FILES** = ``1``

Dialog cho phép chọn nhiều tệp.

.. _class_FileDialog_constant_FILE_MODE_OPEN_DIR:

.. rst-class:: classref-enumeration-constant

:ref:`FileMode<enum_FileDialog_FileMode>` **FILE_MODE_OPEN_DIR** = ``2``

Dialog chỉ cho phép chọn một thư mục, không cho phép chọn bất kỳ tệp nào.

.. _class_FileDialog_constant_FILE_MODE_OPEN_ANY:

.. rst-class:: classref-enumeration-constant

:ref:`FileMode<enum_FileDialog_FileMode>` **FILE_MODE_OPEN_ANY** = ``3``

Dialog cho phép chọn một tệp hoặc thư mục.

.. _class_FileDialog_constant_FILE_MODE_SAVE_FILE:

.. rst-class:: classref-enumeration-constant

:ref:`FileMode<enum_FileDialog_FileMode>` **FILE_MODE_SAVE_FILE** = ``4``

Dialog sẽ cảnh báo khi tệp đã tồn tại.

.. rst-class:: classref-item-separator

----

.. _enum_FileDialog_Access:

.. rst-class:: classref-enumeration

enum **Access**: :ref:`🔗<enum_FileDialog_Access>`

.. _class_FileDialog_constant_ACCESS_RESOURCES:

.. rst-class:: classref-enumeration-constant

:ref:`Access<enum_FileDialog_Access>` **ACCESS_RESOURCES** = ``0``

Dialog chỉ cho phép truy cập các tệp trong đường dẫn :ref:`Resource<class_Resource>` (``res://``).

.. _class_FileDialog_constant_ACCESS_USERDATA:

.. rst-class:: classref-enumeration-constant

:ref:`Access<enum_FileDialog_Access>` **ACCESS_USERDATA** = ``1``

Dialog chỉ cho phép truy cập các tệp trong đường dẫn dữ liệu người dùng (``user://``).

.. _class_FileDialog_constant_ACCESS_FILESYSTEM:

.. rst-class:: classref-enumeration-constant

:ref:`Access<enum_FileDialog_Access>` **ACCESS_FILESYSTEM** = ``2``

Dialog cho phép truy cập các tệp trên toàn bộ hệ thống tệp.

.. rst-class:: classref-item-separator

----

.. _enum_FileDialog_DisplayMode:

.. rst-class:: classref-enumeration

enum **DisplayMode**: :ref:`🔗<enum_FileDialog_DisplayMode>`

.. _class_FileDialog_constant_DISPLAY_THUMBNAILS:

.. rst-class:: classref-enumeration-constant

:ref:`DisplayMode<enum_FileDialog_DisplayMode>` **DISPLAY_THUMBNAILS** = ``0``

Dialog hiển thị các tệp dưới dạng lưới hình thu nhỏ. Sử dụng :ref:`thumbnail_size<class_FileDialog_theme_constant_thumbnail_size>` để điều chỉnh kích thước của chúng.

.. _class_FileDialog_constant_DISPLAY_LIST:

.. rst-class:: classref-enumeration-constant

:ref:`DisplayMode<enum_FileDialog_DisplayMode>` **DISPLAY_LIST** = ``1``

Dialog hiển thị các tệp dưới dạng danh sách tên tệp.

.. rst-class:: classref-item-separator

----

.. _enum_FileDialog_Customization:

.. rst-class:: classref-enumeration

enum **Customization**: :ref:`🔗<enum_FileDialog_Customization>`

.. _class_FileDialog_constant_CUSTOMIZATION_HIDDEN_FILES:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_HIDDEN_FILES** = ``0``

Bật/tắt khả năng hiển thị của nút yêu thích và danh sách yêu thích ở bên trái dialog.

Tương đương với :ref:`hidden_files_toggle_enabled<class_FileDialog_property_hidden_files_toggle_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_CREATE_FOLDER:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_CREATE_FOLDER** = ``1``

Nếu được bật, hiển thị nút tạo thư mục mới (khi sử dụng :ref:`FILE_MODE_OPEN_DIR<class_FileDialog_constant_FILE_MODE_OPEN_DIR>`, :ref:`FILE_MODE_OPEN_ANY<class_FileDialog_constant_FILE_MODE_OPEN_ANY>` hoặc :ref:`FILE_MODE_SAVE_FILE<class_FileDialog_constant_FILE_MODE_SAVE_FILE>`).

Tương đương với :ref:`folder_creation_enabled<class_FileDialog_property_folder_creation_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_FILE_FILTER:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_FILE_FILTER** = ``2``

Nếu được bật, hiển thị nút bật/tắt file filter.

Tương đương với :ref:`file_filter_toggle_enabled<class_FileDialog_property_file_filter_toggle_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_FILE_SORT:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_FILE_SORT** = ``3``

Nếu được bật, hiển thị nút tùy chọn sắp xếp tệp.

Tương đương với :ref:`file_sort_options_enabled<class_FileDialog_property_file_sort_options_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_FAVORITES:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_FAVORITES** = ``4``

Nếu được bật, hiển thị nút bật/tắt yêu thích và danh sách yêu thích ở bên trái dialog.

Tương đương với :ref:`favorites_enabled<class_FileDialog_property_favorites_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_RECENT:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_RECENT** = ``5``

Nếu được bật, hiển thị danh sách các thư mục gần đây ở bên trái dialog.

Tương đương với :ref:`recent_list_enabled<class_FileDialog_property_recent_list_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_LAYOUT:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_LAYOUT** = ``6``

Nếu được bật, hiển thị các nút chuyển đổi bố cục (danh sách/hình thu nhỏ).

Tương đương với :ref:`layout_toggle_enabled<class_FileDialog_property_layout_toggle_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_OVERWRITE_WARNING:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_OVERWRITE_WARNING** = ``7``

Nếu được bật, **FileDialog** sẽ cảnh báo người dùng trước khi ghi đè các tệp trong chế độ lưu.

Tương đương với :ref:`overwrite_warning_enabled<class_FileDialog_property_overwrite_warning_enabled>`.

.. _class_FileDialog_constant_CUSTOMIZATION_DELETE:

.. rst-class:: classref-enumeration-constant

:ref:`Customization<enum_FileDialog_Customization>` **CUSTOMIZATION_DELETE** = ``8``

Nếu được bật, menu ngữ cảnh sẽ hiển thị tùy chọn "Delete", cho phép di chuyển các tệp và thư mục vào thùng rác.

Tương đương với :ref:`deleting_enabled<class_FileDialog_property_deleting_enabled>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FileDialog_property_access:

.. rst-class:: classref-property

:ref:`Access<enum_FileDialog_Access>` **access** = ``0`` :ref:`🔗<class_FileDialog_property_access>`

.. rst-class:: classref-property-setget

- |void| **set_access**\ (\ value\: :ref:`Access<enum_FileDialog_Access>`\ ) - :ref:`Access<enum_FileDialog_Access>` **get_access**\ (\ )

Phạm vi truy cập hệ thống tệp.

\ **Cảnh báo:** Trong các bản build Web, FileDialog không thể truy cập hệ thống tệp của máy chủ. Trong môi trường Linux và macOS sandbox, :ref:`use_native_dialog<class_FileDialog_property_use_native_dialog>` được tự động sử dụng để cho phép truy cập giới hạn vào hệ thống tệp của máy chủ.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_current_dir:

.. rst-class:: classref-property

:ref:`String<class_String>` **current_dir** :ref:`🔗<class_FileDialog_property_current_dir>`

.. rst-class:: classref-property-setget

- |void| **set_current_dir**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_current_dir**\ (\ )

Thư mục làm việc hiện tại của file dialog.

\ **Lưu ý:** Đối với các native file dialog, thuộc tính này chỉ được xem như một gợi ý và có thể không được các implementation cụ thể của OS tôn trọng.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_current_file:

.. rst-class:: classref-property

:ref:`String<class_String>` **current_file** :ref:`🔗<class_FileDialog_property_current_file>`

.. rst-class:: classref-property-setget

- |void| **set_current_file**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_current_file**\ (\ )

Tệp hiện được chọn trong file dialog.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_current_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **current_path** :ref:`🔗<class_FileDialog_property_current_path>`

.. rst-class:: classref-property-setget

- |void| **set_current_path**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_current_path**\ (\ )

Đường dẫn đến tệp hiện được chọn trong file dialog.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_deleting_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **deleting_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_deleting_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, menu ngữ cảnh sẽ hiển thị tùy chọn "Delete", cho phép di chuyển các tệp và thư mục vào thùng rác.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_display_mode:

.. rst-class:: classref-property

:ref:`DisplayMode<enum_FileDialog_DisplayMode>` **display_mode** = ``0`` :ref:`🔗<class_FileDialog_property_display_mode>`

.. rst-class:: classref-property-setget

- |void| **set_display_mode**\ (\ value\: :ref:`DisplayMode<enum_FileDialog_DisplayMode>`\ ) - :ref:`DisplayMode<enum_FileDialog_DisplayMode>` **get_display_mode**\ (\ )

Chế độ hiển thị danh sách tệp của dialog.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_favorites_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **favorites_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_favorites_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị nút bật/tắt yêu thích và danh sách yêu thích ở bên trái dialog.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_file_filter_toggle_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **file_filter_toggle_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_file_filter_toggle_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị nút bật/tắt file filter.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_file_mode:

.. rst-class:: classref-property

:ref:`FileMode<enum_FileDialog_FileMode>` **file_mode** = ``4`` :ref:`🔗<class_FileDialog_property_file_mode>`

.. rst-class:: classref-property-setget

- |void| **set_file_mode**\ (\ value\: :ref:`FileMode<enum_FileDialog_FileMode>`\ ) - :ref:`FileMode<enum_FileDialog_FileMode>` **get_file_mode**\ (\ )

Chế độ mở hoặc lưu của dialog, ảnh hưởng đến hành vi chọn.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_file_sort_options_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **file_sort_options_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_file_sort_options_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị nút tùy chọn sắp xếp tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_filename_filter:

.. rst-class:: classref-property

:ref:`String<class_String>` **filename_filter** = ``""`` :ref:`🔗<class_FileDialog_property_filename_filter>`

.. rst-class:: classref-property-setget

- |void| **set_filename_filter**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_filename_filter**\ (\ )

Bộ lọc cho tên tệp (không phân biệt chữ hoa chữ thường). Khi được đặt thành một chuỗi không rỗng, chỉ những tệp chứa chuỗi con đó mới được hiển thị. :ref:`filename_filter<class_FileDialog_property_filename_filter>` có thể được người dùng chỉnh sửa bằng nút bộ lọc ở đầu hộp thoại tệp.

Xem thêm :ref:`filters<class_FileDialog_property_filters>`, được dùng để hạn chế các loại tệp có thể chọn, thay vì :ref:`filename_filter<class_FileDialog_property_filename_filter>`, vốn được thiết lập bởi người dùng.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_filters:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **filters** = ``PackedStringArray()`` :ref:`🔗<class_FileDialog_property_filters>`

.. rst-class:: classref-property-setget

- |void| **set_filters**\ (\ value\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) - :ref:`PackedStringArray<class_PackedStringArray>` **get_filters**\ (\ )

Các bộ lọc loại tệp khả dụng. Mỗi chuỗi bộ lọc trong mảng phải được định dạng như sau: ``*.png,*.jpg,*.jpeg;Image Files;image/png,image/jpeg``. Phần văn bản mô tả bộ lọc là tùy chọn và có thể bỏ qua. Luôn phải thiết lập cả phần mở rộng tệp và MIME type.

\ **Lưu ý:** Hộp thoại tệp nhúng và hộp thoại tệp Windows chỉ hỗ trợ phần mở rộng tệp, trong khi hộp thoại tệp Android, Linux và macOS cũng hỗ trợ MIME type.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính gốc. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_folder_creation_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **folder_creation_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_folder_creation_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị nút tạo thư mục mới (khi sử dụng :ref:`FILE_MODE_OPEN_DIR<class_FileDialog_constant_FILE_MODE_OPEN_DIR>`, :ref:`FILE_MODE_OPEN_ANY<class_FileDialog_constant_FILE_MODE_OPEN_ANY>` hoặc :ref:`FILE_MODE_SAVE_FILE<class_FileDialog_constant_FILE_MODE_SAVE_FILE>`) và menu ngữ cảnh sẽ có tùy chọn "New Folder...".

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_hidden_files_toggle_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **hidden_files_toggle_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_hidden_files_toggle_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị nút bật/tắt tệp ẩn.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_layout_toggle_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **layout_toggle_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_layout_toggle_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị các nút chuyển bố cục (danh sách/hình thu nhỏ).

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_mode_overrides_title:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **mode_overrides_title** = ``true`` :ref:`🔗<class_FileDialog_property_mode_overrides_title>`

.. rst-class:: classref-property-setget

- |void| **set_mode_overrides_title**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_mode_overriding_title**\ (\ )

Nếu ``true``, việc thay đổi thuộc tính :ref:`file_mode<class_FileDialog_property_file_mode>` sẽ đặt tiêu đề cửa sổ tương ứng (ví dụ: đặt :ref:`file_mode<class_FileDialog_property_file_mode>` thành :ref:`FILE_MODE_OPEN_FILE<class_FileDialog_constant_FILE_MODE_OPEN_FILE>` sẽ đổi tiêu đề cửa sổ thành "Open a File").

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_option_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **option_count** = ``0`` :ref:`🔗<class_FileDialog_property_option_count>`

.. rst-class:: classref-property-setget

- |void| **set_option_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_option_count**\ (\ )

Số lượng :ref:`OptionButton<class_OptionButton>`\ s và :ref:`CheckBox<class_CheckBox>`\ es bổ sung trong hộp thoại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_option_{index}/default:

.. rst-class:: classref-property

:ref:`int<class_int>` **option_{index}/default** = ``0`` :ref:`🔗<class_FileDialog_property_option_{index}/default>`

Giá trị mặc định cho tùy chọn tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. option_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_option_{index}/name:

.. rst-class:: classref-property

:ref:`String<class_String>` **option_{index}/name** = ``""`` :ref:`🔗<class_FileDialog_property_option_{index}/name>`

Tên của tùy chọn tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. option_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_option_{index}/values:

.. rst-class:: classref-property

:ref:`PackedStringArray<class_PackedStringArray>` **option_{index}/values** = ``PackedStringArray()`` :ref:`🔗<class_FileDialog_property_option_{index}/values>`

Danh sách các giá trị cho tùy chọn tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. option_count - 1``.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính gốc. Xem :ref:`PackedStringArray<class_PackedStringArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_overwrite_warning_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **overwrite_warning_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_overwrite_warning_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, **FileDialog** sẽ cảnh báo người dùng trước khi ghi đè tệp trong chế độ lưu.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_recent_list_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recent_list_enabled** = ``true`` :ref:`🔗<class_FileDialog_property_recent_list_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const|

Nếu ``true``, hiển thị danh sách thư mục gần đây ở bên trái hộp thoại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_root_subfolder:

.. rst-class:: classref-property

:ref:`String<class_String>` **root_subfolder** = ``""`` :ref:`🔗<class_FileDialog_property_root_subfolder>`

.. rst-class:: classref-property-setget

- |void| **set_root_subfolder**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_root_subfolder**\ (\ )

Nếu không rỗng, thư mục con đã cho sẽ là "root" của **FileDialog** này, tức là người dùng sẽ không thể chuyển đến thư mục cha của nó.

\ **Lưu ý:** Thuộc tính này bị bỏ qua bởi các hộp thoại tệp native.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_show_hidden_files:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **show_hidden_files** = ``false`` :ref:`🔗<class_FileDialog_property_show_hidden_files>`

.. rst-class:: classref-property-setget

- |void| **set_show_hidden_files**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_showing_hidden_files**\ (\ )

Nếu ``true``, hộp thoại sẽ hiển thị các tệp ẩn.

\ **Lưu ý:** Thuộc tính này bị bỏ qua bởi các hộp thoại tệp native trên Android và Linux.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_property_use_native_dialog:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_native_dialog** = ``false`` :ref:`🔗<class_FileDialog_property_use_native_dialog>`

.. rst-class:: classref-property-setget

- |void| **set_use_native_dialog**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_native_dialog**\ (\ )

Nếu ``true`` và được :ref:`DisplayServer<class_DisplayServer>` hiện tại hỗ trợ, hộp thoại native của hệ điều hành sẽ được sử dụng thay cho hộp thoại tùy chỉnh.

\ **Lưu ý:** Trên Android, tính năng này chỉ được hỗ trợ khi sử dụng :ref:`ACCESS_FILESYSTEM<class_FileDialog_constant_ACCESS_FILESYSTEM>`. Với chế độ truy cập :ref:`ACCESS_RESOURCES<class_FileDialog_constant_ACCESS_RESOURCES>` và :ref:`ACCESS_USERDATA<class_FileDialog_constant_ACCESS_USERDATA>`, hệ thống sẽ chuyển về FileDialog tùy chỉnh.

\ **Lưu ý:** Trên Linux và macOS, các ứng dụng chạy trong sandbox luôn sử dụng hộp thoại native để truy cập hệ thống tệp của máy chủ.

\ **Lưu ý:** Trên macOS, các ứng dụng chạy trong sandbox sẽ lưu security-scoped bookmark để duy trì quyền truy cập vào các thư mục đã mở qua nhiều phiên. Sử dụng :ref:`OS.get_granted_permissions()<class_OS_method_get_granted_permissions>` để lấy danh sách bookmark đã lưu.

\ **Lưu ý:** Các hộp thoại native được tách biệt khỏi tiến trình cơ sở; không thể sửa đổi các thuộc tính của hộp thoại tệp sau khi hộp thoại được hiển thị.

\ **Lưu ý:** Thuộc tính này bị bỏ qua trong :ref:`EditorFileDialog<class_EditorFileDialog>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_FileDialog_method_add_filter:

.. rst-class:: classref-method

|void| **add_filter**\ (\ filter\: :ref:`String<class_String>`, description\: :ref:`String<class_String>` = "", mime_type\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_FileDialog_method_add_filter>`

Thêm một tùy chọn ``filter`` phần mở rộng tệp được phân tách bằng dấu phẩy và ``mime_type`` MIME type được phân tách bằng dấu phẩy vào **FileDialog**, cùng với ``description`` tùy chọn, dùng để giới hạn các tệp có thể chọn.

Một ``filter`` phải có dạng ``"filename.extension"``, trong đó tên tệp và phần mở rộng có thể là ``*`` để khớp với mọi chuỗi. Không cho phép các bộ lọc bắt đầu bằng ``.`` (tức là tên tệp rỗng).

Ví dụ: ``filter`` có giá trị ``"*.png, *.jpg"``, ``mime_type`` có giá trị ``image/png, image/jpeg`` và ``description`` có giá trị ``"Images"`` sẽ cho ra văn bản bộ lọc "Images (\*.png, \*.jpg)".

\ **Lưu ý:** Hộp thoại tệp nhúng và hộp thoại tệp Windows chỉ hỗ trợ phần mở rộng tệp, trong khi hộp thoại tệp Android, Linux và macOS cũng hỗ trợ MIME type.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_add_option:

.. rst-class:: classref-method

|void| **add_option**\ (\ name\: :ref:`String<class_String>`, values\: :ref:`PackedStringArray<class_PackedStringArray>`, default_value_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_FileDialog_method_add_option>`

Thêm một :ref:`OptionButton<class_OptionButton>` bổ sung vào hộp thoại tệp. Nếu ``values`` rỗng, một :ref:`CheckBox<class_CheckBox>` sẽ được thêm vào thay thế.

\ ``default_value_index`` phải là chỉ mục của giá trị trong ``values``. Nếu ``values`` rỗng, giá trị đó phải là ``1`` (đã chọn) hoặc ``0`` (bỏ chọn).

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_clear_filename_filter:

.. rst-class:: classref-method

|void| **clear_filename_filter**\ (\ ) :ref:`🔗<class_FileDialog_method_clear_filename_filter>`

Xóa bộ lọc tên tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_clear_filters:

.. rst-class:: classref-method

|void| **clear_filters**\ (\ ) :ref:`🔗<class_FileDialog_method_clear_filters>`

Xóa tất cả các bộ lọc đã thêm trong hộp thoại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_deselect_all:

.. rst-class:: classref-method

|void| **deselect_all**\ (\ ) :ref:`🔗<class_FileDialog_method_deselect_all>`

Bỏ chọn tất cả các mục hiện đang được chọn trong hộp thoại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_favorite_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_favorite_list**\ (\ ) |static| :ref:`🔗<class_FileDialog_method_get_favorite_list>`

Trả về danh sách các thư mục yêu thích, được dùng chung bởi tất cả các node **FileDialog**. Hữu ích để lưu danh sách thư mục yêu thích giữa các phiên làm việc của project. Phương thức này chỉ có thể được gọi từ main thread.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_line_edit:

.. rst-class:: classref-method

:ref:`LineEdit<class_LineEdit>` **get_line_edit**\ (\ ) :ref:`🔗<class_FileDialog_method_get_line_edit>`

Trả về LineEdit của tệp đã chọn.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_option_default:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_option_default**\ (\ option\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_FileDialog_method_get_option_default>`

Trả về chỉ mục giá trị mặc định của :ref:`OptionButton<class_OptionButton>` hoặc :ref:`CheckBox<class_CheckBox>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_option_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_option_name**\ (\ option\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_FileDialog_method_get_option_name>`

Trả về tên của :ref:`OptionButton<class_OptionButton>` hoặc :ref:`CheckBox<class_CheckBox>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_option_values:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_option_values**\ (\ option\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_FileDialog_method_get_option_values>`

Trả về một mảng các giá trị của :ref:`OptionButton<class_OptionButton>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_recent_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_recent_list**\ (\ ) |static| :ref:`🔗<class_FileDialog_method_get_recent_list>`

Trả về danh sách các thư mục gần đây, được dùng chung bởi tất cả các node **FileDialog**. Hữu ích để lưu danh sách các thư mục gần đây giữa các phiên làm việc của project. Phương thức này chỉ có thể được gọi từ main thread.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_selected_options:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_selected_options**\ (\ ) |const| :ref:`🔗<class_FileDialog_method_get_selected_options>`

Trả về một :ref:`Dictionary<class_Dictionary>` chứa các giá trị đã chọn của các :ref:`OptionButton<class_OptionButton>`\ s và/hoặc :ref:`CheckBox<class_CheckBox>`\ es bổ sung. Các khóa :ref:`Dictionary<class_Dictionary>` là tên và các giá trị là chỉ mục của những giá trị đã chọn.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_get_vbox:

.. rst-class:: classref-method

:ref:`VBoxContainer<class_VBoxContainer>` **get_vbox**\ (\ ) :ref:`🔗<class_FileDialog_method_get_vbox>`

Trả về container hộp dọc của hộp thoại; có thể thêm các control tùy chỉnh vào đó.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

\ **Lưu ý:** Các thay đổi đối với node này sẽ bị bỏ qua bởi native file dialogs; thay vào đó, hãy sử dụng :ref:`add_option()<class_FileDialog_method_add_option>` để thêm các phần tử tùy chỉnh vào hộp thoại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_invalidate:

.. rst-class:: classref-method

|void| **invalidate**\ (\ ) :ref:`🔗<class_FileDialog_method_invalidate>`

Làm mất hiệu lực và cập nhật danh sách nội dung của hộp thoại này.

\ **Lưu ý:** Phương thức này không có tác dụng với native file dialogs.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_is_customization_flag_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`\ ) |const| :ref:`🔗<class_FileDialog_method_is_customization_flag_enabled>`

Trả về ``true`` nếu ``flag`` được cung cấp đang bật.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_popup_file_dialog:

.. rst-class:: classref-method

|void| **popup_file_dialog**\ (\ ) :ref:`🔗<class_FileDialog_method_popup_file_dialog>`

Hiển thị **FileDialog** bằng kích thước và vị trí mặc định dành cho các hộp thoại tệp, đồng thời chọn tên tệp nếu có tệp hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_customization_flag_enabled:

.. rst-class:: classref-method

|void| **set_customization_flag_enabled**\ (\ flag\: :ref:`Customization<enum_FileDialog_Customization>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_FileDialog_method_set_customization_flag_enabled>`

Thiết lập ``flag`` tùy chỉnh được chỉ định, cho phép tùy chỉnh các tính năng có trong **FileDialog** này.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_favorite_list:

.. rst-class:: classref-method

|void| **set_favorite_list**\ (\ favorites\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |static| :ref:`🔗<class_FileDialog_method_set_favorite_list>`

Thiết lập danh sách các thư mục yêu thích, được dùng chung bởi tất cả các node **FileDialog**. Hữu ích để khôi phục danh sách thư mục yêu thích đã lưu bằng :ref:`get_favorite_list()<class_FileDialog_method_get_favorite_list>`. Phương thức này chỉ có thể được gọi từ main thread.

\ **Lưu ý:** **FileDialog** sẽ cập nhật :ref:`ItemList<class_ItemList>` nội bộ của nó về các thư mục yêu thích khi khả năng hiển thị thay đổi. Hãy nhớ gọi phương thức này sớm hơn nếu muốn các thay đổi của bạn có hiệu lực.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_get_icon_callback:

.. rst-class:: classref-method

|void| **set_get_icon_callback**\ (\ callback\: :ref:`Callable<class_Callable>`\ ) |static| :ref:`🔗<class_FileDialog_method_set_get_icon_callback>`

Thiết lập callback được các node **FileDialog** sử dụng để lấy biểu tượng tệp khi sử dụng chế độ :ref:`DISPLAY_LIST<class_FileDialog_constant_DISPLAY_LIST>`. Callback phải nhận một đối số :ref:`String<class_String>` duy nhất (đường dẫn tệp) và trả về một :ref:`Texture2D<class_Texture2D>`. Nếu trả về texture không hợp lệ, biểu tượng :ref:`file<class_FileDialog_theme_icon_file>` sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_get_thumbnail_callback:

.. rst-class:: classref-method

|void| **set_get_thumbnail_callback**\ (\ callback\: :ref:`Callable<class_Callable>`\ ) |static| :ref:`🔗<class_FileDialog_method_set_get_thumbnail_callback>`

Thiết lập callback được các node **FileDialog** sử dụng để lấy biểu tượng tệp khi sử dụng chế độ :ref:`DISPLAY_THUMBNAILS<class_FileDialog_constant_DISPLAY_THUMBNAILS>`. Callback phải nhận một đối số :ref:`String<class_String>` duy nhất (đường dẫn tệp) và trả về một :ref:`Texture2D<class_Texture2D>`. Nếu trả về texture không hợp lệ, biểu tượng :ref:`file_thumbnail<class_FileDialog_theme_icon_file_thumbnail>` sẽ được sử dụng thay thế.

Thumbnail thường phức tạp hơn và có thể mất một lúc để tải. Để tránh làm ứng dụng bị đình trệ, bạn có thể sử dụng :ref:`ImageTexture<class_ImageTexture>` để tạo thumbnail bất đồng bộ.

::

    func _ready():
        FileDialog.set_get_thumbnail_callback(thumbnail_method)

    func thumbnail_method(path):
        var image_texture = ImageTexture.new()
        make_thumbnail_async(path, image_texture)
        return image_texture

    func make_thumbnail_async(path, image_texture):
        var thumbnail_texture = await generate_thumbnail(path) # Một phương thức nào đó tạo thumbnail.
        image_texture.set_image(thumbnail_texture.get_image())

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_option_default:

.. rst-class:: classref-method

|void| **set_option_default**\ (\ option\: :ref:`int<class_int>`, default_value_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_FileDialog_method_set_option_default>`

Thiết lập chỉ mục giá trị mặc định của :ref:`OptionButton<class_OptionButton>` hoặc :ref:`CheckBox<class_CheckBox>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_option_name:

.. rst-class:: classref-method

|void| **set_option_name**\ (\ option\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileDialog_method_set_option_name>`

Thiết lập tên của :ref:`OptionButton<class_OptionButton>` hoặc :ref:`CheckBox<class_CheckBox>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_option_values:

.. rst-class:: classref-method

|void| **set_option_values**\ (\ option\: :ref:`int<class_int>`, values\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_FileDialog_method_set_option_values>`

Thiết lập các giá trị tùy chọn của :ref:`OptionButton<class_OptionButton>` có chỉ mục ``option``.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_method_set_recent_list:

.. rst-class:: classref-method

|void| **set_recent_list**\ (\ recents\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |static| :ref:`🔗<class_FileDialog_method_set_recent_list>`

Thiết lập danh sách các thư mục gần đây, được dùng chung bởi tất cả các node **FileDialog**. Hữu ích để khôi phục danh sách các thư mục gần đây đã lưu bằng :ref:`set_recent_list()<class_FileDialog_method_set_recent_list>`. Phương thức này chỉ có thể được gọi từ main thread.

\ **Lưu ý:** **FileDialog** sẽ cập nhật :ref:`ItemList<class_ItemList>` nội bộ của nó về các thư mục gần đây khi khả năng hiển thị thay đổi. Hãy nhớ gọi phương thức này sớm hơn nếu muốn các thay đổi của bạn có hiệu lực.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các thuộc tính của Theme
------------------------------

.. _class_FileDialog_theme_color_file_disabled_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **file_disabled_color** = ``Color(1, 1, 1, 0.25)`` :ref:`🔗<class_FileDialog_theme_color_file_disabled_color>`

Màu sắc áp dụng cho các tệp bị vô hiệu hóa (khi **FileDialog** được sử dụng ở chế độ mở thư mục).

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_color_file_icon_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **file_icon_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_FileDialog_theme_color_file_icon_color>`

Điều chỉnh màu được áp dụng cho biểu tượng tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_color_folder_icon_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **folder_icon_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_FileDialog_theme_color_folder_icon_color>`

Điều chỉnh màu được áp dụng cho biểu tượng thư mục.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_constant_thumbnail_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **thumbnail_size** = ``64`` :ref:`🔗<class_FileDialog_theme_constant_thumbnail_size>`

Kích thước của các biểu tượng thumbnail khi :ref:`DISPLAY_THUMBNAILS<class_FileDialog_constant_DISPLAY_THUMBNAILS>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_back_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **back_folder** :ref:`🔗<class_FileDialog_theme_icon_back_folder>`

Biểu tượng tùy chỉnh cho mũi tên quay lại.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_create_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **create_folder** :ref:`🔗<class_FileDialog_theme_icon_create_folder>`

Biểu tượng tùy chỉnh cho nút tạo thư mục.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_favorite:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **favorite** :ref:`🔗<class_FileDialog_theme_icon_favorite>`

Biểu tượng tùy chỉnh cho nút thư mục yêu thích.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_favorite_down:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **favorite_down** :ref:`🔗<class_FileDialog_theme_icon_favorite_down>`

Biểu tượng tùy chỉnh cho nút di chuyển mục yêu thích xuống dưới.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_favorite_up:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **favorite_up** :ref:`🔗<class_FileDialog_theme_icon_favorite_up>`

Biểu tượng tùy chỉnh cho nút di chuyển mục yêu thích lên trên.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_file:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **file** :ref:`🔗<class_FileDialog_theme_icon_file>`

Biểu tượng tùy chỉnh cho các tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_file_thumbnail:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **file_thumbnail** :ref:`🔗<class_FileDialog_theme_icon_file_thumbnail>`

Biểu tượng cho các tệp khi ở chế độ thumbnail.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **folder** :ref:`🔗<class_FileDialog_theme_icon_folder>`

Biểu tượng tùy chỉnh cho các thư mục.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_folder_thumbnail:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **folder_thumbnail** :ref:`🔗<class_FileDialog_theme_icon_folder_thumbnail>`

Biểu tượng cho các thư mục khi ở chế độ thumbnail.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_forward_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **forward_folder** :ref:`🔗<class_FileDialog_theme_icon_forward_folder>`

Biểu tượng tùy chỉnh cho mũi tên tiến tới.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_list_mode:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **list_mode** :ref:`🔗<class_FileDialog_theme_icon_list_mode>`

Biểu tượng cho nút bật chế độ danh sách.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_copy_path:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_copy_path** :ref:`🔗<class_FileDialog_theme_icon_menu_copy_path>`

Biểu tượng cho tùy chọn menu ngữ cảnh "Copy Path".

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_delete:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_delete** :ref:`🔗<class_FileDialog_theme_icon_menu_delete>`

Biểu tượng cho tùy chọn menu ngữ cảnh "Delete".

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_new_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_new_folder** :ref:`🔗<class_FileDialog_theme_icon_menu_new_folder>`

Biểu tượng cho tùy chọn menu ngữ cảnh "New Folder...". Thông thường, biểu tượng này nên giống với :ref:`create_folder<class_FileDialog_theme_icon_create_folder>`; để trống nếu bạn muốn menu ngữ cảnh không hiển thị biểu tượng.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_open_bundle:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_open_bundle** :ref:`🔗<class_FileDialog_theme_icon_menu_open_bundle>`

Biểu tượng cho tùy chọn menu ngữ cảnh "Show Package Contents". Tùy chọn này chỉ xuất hiện với các bundle của macOS.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_refresh:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_refresh** :ref:`🔗<class_FileDialog_theme_icon_menu_refresh>`

Biểu tượng cho tùy chọn menu ngữ cảnh "Refresh". Thông thường, biểu tượng này nên giống với :ref:`reload<class_FileDialog_theme_icon_reload>`; để trống nếu bạn muốn menu ngữ cảnh không hiển thị biểu tượng.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_menu_show_in_file_manager:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **menu_show_in_file_manager** :ref:`🔗<class_FileDialog_theme_icon_menu_show_in_file_manager>`

Biểu tượng cho tùy chọn menu ngữ cảnh "Show in File Manager".

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_parent_folder:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **parent_folder** :ref:`🔗<class_FileDialog_theme_icon_parent_folder>`

Biểu tượng tùy chỉnh cho mũi tên thư mục cha.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_reload:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **reload** :ref:`🔗<class_FileDialog_theme_icon_reload>`

Biểu tượng tùy chỉnh cho nút reload.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_sort:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **sort** :ref:`🔗<class_FileDialog_theme_icon_sort>`

Biểu tượng tùy chỉnh cho menu tùy chọn sắp xếp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_thumbnail_mode:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **thumbnail_mode** :ref:`🔗<class_FileDialog_theme_icon_thumbnail_mode>`

Biểu tượng cho nút bật chế độ thumbnail.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_toggle_filename_filter:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **toggle_filename_filter** :ref:`🔗<class_FileDialog_theme_icon_toggle_filename_filter>`

Biểu tượng tùy chỉnh cho nút bật/tắt bộ lọc tên tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileDialog_theme_icon_toggle_hidden:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **toggle_hidden** :ref:`🔗<class_FileDialog_theme_icon_toggle_hidden>`

Biểu tượng tùy chỉnh cho nút bật/tắt chế độ ẩn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
