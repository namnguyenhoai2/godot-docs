:github_url: hide

.. meta::
	:keywords: directory, path, folder

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DirAccess.xml.

.. _class_DirAccess:

DirAccess
=========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các phương thức để quản lý thư mục và nội dung của chúng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được dùng để quản lý thư mục và nội dung của chúng, kể cả bên ngoài thư mục dự án.

\ **DirAccess** không thể được khởi tạo trực tiếp. Thay vào đó, nó được tạo bằng một static method nhận vào đường dẫn mà nó sẽ mở.

Hầu hết các phương thức đều có một static alternative có thể được sử dụng mà không cần tạo **DirAccess**. Các static method chỉ hỗ trợ đường dẫn tuyệt đối (bao gồm ``res://`` và ``user://``).

::

    # Chuẩn
    var dir = DirAccess.open("user://levels")
    dir.make_dir("world1")
    # Static
    DirAccess.make_dir_absolute("user://levels/world1")

\ **Lưu ý:** Việc truy cập các thư mục của dự án ("res://") sau khi đã export có thể cho kết quả không như mong đợi, vì một số tệp được chuyển đổi sang các định dạng dành riêng cho engine và các tệp nguồn ban đầu của chúng có thể không có trong PCK package như dự kiến. Vì vậy, để truy cập các resource trong dự án đã export, bạn nên sử dụng :ref:`ResourceLoader<class_ResourceLoader>` thay vì :ref:`FileAccess<class_FileAccess>`.

Sau đây là ví dụ về cách duyệt qua các tệp trong một thư mục:


.. tabs::

 .. code-tab:: gdscript

    func dir_contents(path):
        var dir = DirAccess.open(path)
        if dir:
            dir.list_dir_begin()
            var file_name = dir.get_next()
            while file_name != "":
                if dir.current_is_dir():
                    print("Found directory: " + file_name)
                else:
                    print("Found file: " + file_name)
                file_name = dir.get_next()
        else:
            print("An error occurred when trying to access the path.")

 .. code-tab:: csharp

    public void DirContents(string path)
    {
        using var dir = DirAccess.Open(path);
        if (dir != null)
        {
            dir.ListDirBegin();
            string fileName = dir.GetNext();
            while (fileName != "")
            {
                if (dir.CurrentIsDir())
                {
                    GD.Print($"Found directory: {fileName}");
                }
                else
                {
                    GD.Print($"Found file: {fileName}");
                }
                fileName = dir.GetNext();
            }
        }
        else
        {
            GD.Print("An error occurred when trying to access the path.");
        }
    }



Hãy nhớ rằng tên tệp có thể thay đổi hoặc được remap sau khi export. Nếu muốn xem danh sách tệp resource thực tế như trong editor, hãy sử dụng :ref:`ResourceLoader.list_directory()<class_ResourceLoader_method_list_directory>` thay thế.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Hệ thống tệp <../tutorials/scripting/filesystem>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`include_hidden<class_DirAccess_property_include_hidden>`             |
   +-------------------------+----------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`include_navigational<class_DirAccess_property_include_navigational>` |
   +-------------------------+----------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`change_dir<class_DirAccess_method_change_dir>`\ (\ to_dir\: :ref:`String<class_String>`\ )                                                                                          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`copy<class_DirAccess_method_copy>`\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`, chmod_flags\: :ref:`int<class_int>` = -1\ )                            |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`copy_absolute<class_DirAccess_method_copy_absolute>`\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`, chmod_flags\: :ref:`int<class_int>` = -1\ ) |static| |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`create_link<class_DirAccess_method_create_link>`\ (\ source\: :ref:`String<class_String>`, target\: :ref:`String<class_String>`\ )                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`DirAccess<class_DirAccess>`                 | :ref:`create_temp<class_DirAccess_method_create_temp>`\ (\ prefix\: :ref:`String<class_String>` = "", keep\: :ref:`bool<class_bool>` = false\ ) |static|                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`current_is_dir<class_DirAccess_method_current_is_dir>`\ (\ ) |const|                                                                                                                |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`dir_exists<class_DirAccess_method_dir_exists>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                            |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`dir_exists_absolute<class_DirAccess_method_dir_exists_absolute>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`file_exists<class_DirAccess_method_file_exists>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                          |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_current_dir<class_DirAccess_method_get_current_dir>`\ (\ include_drive\: :ref:`bool<class_bool>` = true\ ) |const|                                                              |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_current_drive<class_DirAccess_method_get_current_drive>`\ (\ )                                                                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_directories<class_DirAccess_method_get_directories>`\ (\ )                                                                                                                      |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_directories_at<class_DirAccess_method_get_directories_at>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                   |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_drive_count<class_DirAccess_method_get_drive_count>`\ (\ ) |static|                                                                                                             |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_drive_label<class_DirAccess_method_get_drive_label>`\ (\ idx\: :ref:`int<class_int>`\ ) |static|                                                                                |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_drive_name<class_DirAccess_method_get_drive_name>`\ (\ idx\: :ref:`int<class_int>`\ ) |static|                                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_files<class_DirAccess_method_get_files>`\ (\ )                                                                                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_files_at<class_DirAccess_method_get_files_at>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                               |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_filesystem_type<class_DirAccess_method_get_filesystem_type>`\ (\ ) |const|                                                                                                      |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_next<class_DirAccess_method_get_next>`\ (\ )                                                                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`get_open_error<class_DirAccess_method_get_open_error>`\ (\ ) |static|                                                                                                               |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_space_left<class_DirAccess_method_get_space_left>`\ (\ )                                                                                                                        |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_bundle<class_DirAccess_method_is_bundle>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                                                                                      |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_case_sensitive<class_DirAccess_method_is_case_sensitive>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                                                                      |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_equivalent<class_DirAccess_method_is_equivalent>`\ (\ path_a\: :ref:`String<class_String>`, path_b\: :ref:`String<class_String>`\ ) |const|                                      |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_link<class_DirAccess_method_is_link>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`list_dir_begin<class_DirAccess_method_list_dir_begin>`\ (\ )                                                                                                                        |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`list_dir_end<class_DirAccess_method_list_dir_end>`\ (\ )                                                                                                                            |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`make_dir<class_DirAccess_method_make_dir>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`make_dir_absolute<class_DirAccess_method_make_dir_absolute>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                     |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`make_dir_recursive<class_DirAccess_method_make_dir_recursive>`\ (\ path\: :ref:`String<class_String>`\ )                                                                            |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`make_dir_recursive_absolute<class_DirAccess_method_make_dir_recursive_absolute>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`DirAccess<class_DirAccess>`                 | :ref:`open<class_DirAccess_method_open>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                                               |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`read_link<class_DirAccess_method_read_link>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                              |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`remove<class_DirAccess_method_remove>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                    |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`remove_absolute<class_DirAccess_method_remove_absolute>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                                                                         |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`rename<class_DirAccess_method_rename>`\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`\ )                                                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`rename_absolute<class_DirAccess_method_rename_absolute>`\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`\ ) |static|                                       |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_DirAccess_property_include_hidden:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **include_hidden** :ref:`🔗<class_DirAccess_property_include_hidden>`

.. rst-class:: classref-property-setget

- |void| **set_include_hidden**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_include_hidden**\ (\ )

Nếu ``true``, các tệp ẩn sẽ được đưa vào khi duyệt thư mục.

Ảnh hưởng đến :ref:`list_dir_begin()<class_DirAccess_method_list_dir_begin>`, :ref:`get_directories()<class_DirAccess_method_get_directories>` và :ref:`get_files()<class_DirAccess_method_get_files>`.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_property_include_navigational:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **include_navigational** :ref:`🔗<class_DirAccess_property_include_navigational>`

.. rst-class:: classref-property-setget

- |void| **set_include_navigational**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_include_navigational**\ (\ )

Nếu ``true``, ``.`` và ``..`` sẽ được đưa vào khi duyệt thư mục.

Ảnh hưởng đến :ref:`list_dir_begin()<class_DirAccess_method_list_dir_begin>` và :ref:`get_directories()<class_DirAccess_method_get_directories>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_DirAccess_method_change_dir:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **change_dir**\ (\ to_dir\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_change_dir>`

Thay đổi thư mục hiện đang mở thành thư mục được truyền làm đối số. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại (ví dụ: ``newdir`` hoặc ``../newdir``), hoặc đường dẫn tuyệt đối (ví dụ: ``/tmp/newdir`` hoặc ``res://somedir/newdir``).

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

\ **Lưu ý:** Thư mục mới phải nằm trong cùng một scope; ví dụ, nếu bạn đã mở một thư mục bên trong ``res://``, bạn không thể chuyển sang thư mục ``user://``. Nếu cần mở một thư mục trong scope truy cập khác, hãy sử dụng :ref:`open()<class_DirAccess_method_open>` để tạo một instance mới.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_copy:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **copy**\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`, chmod_flags\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_DirAccess_method_copy>`

Sao chép tệp ``from`` đến đích ``to``. Cả hai đối số phải là đường dẫn đến tệp, có thể là đường dẫn tương đối hoặc tuyệt đối. Nếu tệp đích tồn tại và không bị hạn chế quyền truy cập, tệp đó sẽ bị ghi đè.

Nếu ``chmod_flags`` khác ``-1``, quyền Unix của đường dẫn đích sẽ được đặt thành giá trị đã cung cấp, nếu hệ điều hành hiện tại hỗ trợ.

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_copy_absolute:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **copy_absolute**\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`, chmod_flags\: :ref:`int<class_int>` = -1\ ) |static| :ref:`🔗<class_DirAccess_method_copy_absolute>`

Phiên bản static của :ref:`copy()<class_DirAccess_method_copy>`. Chỉ hỗ trợ đường dẫn tuyệt đối.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_create_link:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_link**\ (\ source\: :ref:`String<class_String>`, target\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_create_link>`

Tạo symbolic link giữa các tệp hoặc thư mục.

\ **Lưu ý:** Trên Windows, phương thức này chỉ hoạt động nếu ứng dụng đang chạy với đặc quyền nâng cao hoặc Developer Mode được bật.

\ **Lưu ý:** Phương thức này được triển khai trên macOS, Linux và Windows.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_create_temp:

.. rst-class:: classref-method

:ref:`DirAccess<class_DirAccess>` **create_temp**\ (\ prefix\: :ref:`String<class_String>` = "", keep\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_DirAccess_method_create_temp>`

Tạo một thư mục tạm thời. Thư mục này sẽ được giải phóng khi **DirAccess** được trả về bị giải phóng.

Nếu ``prefix`` không rỗng, giá trị này sẽ được thêm vào đầu tên thư mục, ngăn cách bằng một ``-``.

Nếu ``keep`` là ``true``, thư mục sẽ không bị xóa khi **DirAccess** được trả về bị giải phóng.

Trả về ``null`` nếu không mở được thư mục. Bạn có thể sử dụng :ref:`get_open_error()<class_DirAccess_method_get_open_error>` để kiểm tra lỗi đã xảy ra.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_current_is_dir:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **current_is_dir**\ (\ ) |const| :ref:`🔗<class_DirAccess_method_current_is_dir>`

Trả về thông tin cho biết mục hiện tại được xử lý bằng lần gọi :ref:`get_next()<class_DirAccess_method_get_next>` gần nhất có phải là thư mục hay không (``.`` và ``..`` được xem là thư mục).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_dir_exists:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **dir_exists**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_dir_exists>`

Trả về thông tin cho biết thư mục đích có tồn tại hay không. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại hoặc đường dẫn tuyệt đối.

\ **Lưu ý:** Giá trị :ref:`bool<class_bool>` được trả về trong editor và sau khi export khi sử dụng trên một đường dẫn trong thư mục ``res://`` có thể khác nhau. Một số tệp được chuyển đổi sang các định dạng dành riêng cho engine khi export, có thể làm thay đổi cấu trúc thư mục.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_dir_exists_absolute:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **dir_exists_absolute**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_dir_exists_absolute>`

Phiên bản static của :ref:`dir_exists()<class_DirAccess_method_dir_exists>`. Chỉ hỗ trợ đường dẫn tuyệt đối.

\ **Lưu ý:** Giá trị :ref:`bool<class_bool>` được trả về trong editor và sau khi export khi sử dụng trên một đường dẫn trong thư mục ``res://`` có thể khác nhau. Một số tệp được chuyển đổi sang các định dạng dành riêng cho engine khi export, có thể làm thay đổi cấu trúc thư mục.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_file_exists:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **file_exists**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_file_exists>`

Trả về thông tin cho biết tệp đích có tồn tại hay không. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại hoặc đường dẫn tuyệt đối.

Để sử dụng phiên bản static tương đương, hãy dùng :ref:`FileAccess.file_exists()<class_FileAccess_method_file_exists>`.

\ **Lưu ý:** Nhiều loại resource được import (ví dụ: texture hoặc tệp âm thanh), và asset nguồn của chúng sẽ không được đưa vào game đã export vì chỉ phiên bản đã import được sử dụng. Xem :ref:`ResourceLoader.exists()<class_ResourceLoader_method_exists>` để biết cách tiếp cận thay thế có tính đến việc remap resource.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_current_dir:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_current_dir**\ (\ include_drive\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_DirAccess_method_get_current_dir>`

Trả về đường dẫn tuyệt đối đến thư mục hiện đang mở (ví dụ: ``res://folder`` hoặc ``C:\tmp\folder``).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_current_drive:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_current_drive**\ (\ ) :ref:`🔗<class_DirAccess_method_get_current_drive>`

Trả về chỉ mục drive của thư mục hiện đang mở. Xem :ref:`get_drive_name()<class_DirAccess_method_get_drive_name>` để chuyển chỉ mục được trả về thành tên drive.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_directories:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_directories**\ (\ ) :ref:`🔗<class_DirAccess_method_get_directories>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` chứa tên tệp trong nội dung thư mục, không bao gồm các tệp. Mảng được sắp xếp theo thứ tự alphabet.

Bị ảnh hưởng bởi :ref:`include_hidden<class_DirAccess_property_include_hidden>` và :ref:`include_navigational<class_DirAccess_property_include_navigational>`.

\ **Lưu ý:** Các thư mục được trả về trong editor và sau khi export trong thư mục ``res://`` có thể khác nhau, vì một số tệp được chuyển đổi sang các định dạng dành riêng cho engine khi export.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_directories_at:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_directories_at**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_get_directories_at>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` chứa tên tệp trong nội dung thư mục, không bao gồm các tệp, tại ``path`` đã cho. Mảng được sắp xếp theo thứ tự alphabet.

Sử dụng :ref:`get_directories()<class_DirAccess_method_get_directories>` nếu bạn muốn kiểm soát nhiều hơn những gì được đưa vào.

\ **Lưu ý:** Các thư mục được trả về trong editor và sau khi export trong thư mục ``res://`` có thể khác nhau, vì một số tệp được chuyển đổi sang các định dạng dành riêng cho engine khi export.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_drive_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_drive_count**\ (\ ) |static| :ref:`🔗<class_DirAccess_method_get_drive_count>`

Trên Windows, trả về số lượng drive (phân vùng) được mount trên filesystem hiện tại.

Trên macOS và Android, trả về số lượng volume được mount.

Trên Linux, trả về số lượng volume được mount và bookmark GTK 3.

Trên các nền tảng khác, phương thức trả về 0.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_drive_label:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_drive_label**\ (\ idx\: :ref:`int<class_int>`\ ) |static| :ref:`🔗<class_DirAccess_method_get_drive_label>`

Trên Windows, trả về nhãn của ổ đĩa (phân vùng) được truyền làm đối số.

Trên các nền tảng khác hoặc nếu ổ đĩa được yêu cầu không tồn tại, trả về một String rỗng.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_drive_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_drive_name**\ (\ idx\: :ref:`int<class_int>`\ ) |static| :ref:`🔗<class_DirAccess_method_get_drive_name>`

Trên Windows, trả về tên của ổ đĩa (phân vùng) được truyền làm đối số (ví dụ: ``C:``).

Trên macOS, trả về đường dẫn đến volume đã mount được truyền làm đối số.

Trên Linux, trả về đường dẫn đến volume đã mount hoặc bookmark GTK 3 được truyền làm đối số.

Trên Android (API level 30 trở lên), trả về đường dẫn đến volume đã mount được truyền làm đối số.

Trên các nền tảng khác hoặc nếu ổ đĩa được yêu cầu không tồn tại, trả về một String rỗng.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_files:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_files**\ (\ ) :ref:`🔗<class_DirAccess_method_get_files>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` chứa tên tệp trong nội dung của thư mục, không bao gồm các thư mục. Mảng được sắp xếp theo thứ tự alphabet.

Bị ảnh hưởng bởi :ref:`include_hidden<class_DirAccess_property_include_hidden>`.

\ **Lưu ý:** Khi được sử dụng trên đường dẫn ``res://`` trong một project đã export, chỉ những tệp thực sự được đưa vào PCK ở cấp thư mục đã cho mới được trả về. Trên thực tế, điều này có nghĩa là vì các resource đã import được lưu trữ trong thư mục ``.godot/`` cấp cao nhất, chỉ các đường dẫn đến tệp ``*.gd`` và ``*.import`` mới được trả về (cùng với một vài tệp như ``project.godot`` hoặc ``project.binary`` và icon của project). Trong một project đã export, danh sách các tệp được trả về cũng sẽ thay đổi tùy thuộc vào việc :ref:`ProjectSettings.editor/export/convert_text_resources_to_binary<class_ProjectSettings_property_editor/export/convert_text_resources_to_binary>` có phải là ``true`` hay không.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_files_at:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_files_at**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_get_files_at>`

Trả về một :ref:`PackedStringArray<class_PackedStringArray>` chứa tên tệp trong nội dung của thư mục, không bao gồm các thư mục, tại ``path`` đã cho. Mảng được sắp xếp theo thứ tự alphabet.

Sử dụng :ref:`get_files()<class_DirAccess_method_get_files>` nếu bạn muốn kiểm soát tốt hơn những gì được đưa vào.

\ **Lưu ý:** Khi được sử dụng trên đường dẫn ``res://`` trong một project đã export, chỉ những tệp được đưa vào PCK ở cấp thư mục đã cho mới được trả về. Trên thực tế, điều này có nghĩa là vì các resource đã import được lưu trữ trong thư mục ``.godot/`` cấp cao nhất, chỉ các đường dẫn đến tệp ``.gd`` và ``.import`` mới được trả về (cùng với một vài tệp khác, chẳng hạn như ``project.godot`` hoặc ``project.binary`` và icon của project). Trong một project đã export, danh sách các tệp được trả về cũng sẽ thay đổi tùy thuộc vào :ref:`ProjectSettings.editor/export/convert_text_resources_to_binary<class_ProjectSettings_property_editor/export/convert_text_resources_to_binary>`.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_filesystem_type:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_filesystem_type**\ (\ ) |const| :ref:`🔗<class_DirAccess_method_get_filesystem_type>`

Trả về tên loại file system của disk chứa thư mục hiện tại. Các giá trị được trả về là các chuỗi viết hoa như ``NTFS``, ``FAT32``, ``EXFAT``, ``APFS``, ``EXT4``, ``BTRFS`` và các giá trị khác.

\ **Lưu ý:** Method này được triển khai trên macOS, Linux, Windows và cho virtual file system của PCK.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_next:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_next**\ (\ ) :ref:`🔗<class_DirAccess_method_get_next>`

Trả về phần tử tiếp theo (tệp hoặc thư mục) trong thư mục hiện tại.

Tên của tệp hoặc thư mục được trả về (không phải đường dẫn đầy đủ của nó). Sau khi stream được xử lý hoàn toàn, method trả về một :ref:`String<class_String>` rỗng và tự động đóng stream (tức là trong trường hợp đó, :ref:`list_dir_end()<class_DirAccess_method_list_dir_end>` sẽ không bắt buộc).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_open_error:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **get_open_error**\ (\ ) |static| :ref:`🔗<class_DirAccess_method_get_open_error>`

Trả về kết quả của lệnh gọi :ref:`open()<class_DirAccess_method_open>` gần nhất trong thread hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_get_space_left:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_space_left**\ (\ ) :ref:`🔗<class_DirAccess_method_get_space_left>`

Trả về dung lượng còn trống trên disk của thư mục hiện tại, tính bằng byte. Trả về ``0`` nếu method dành riêng cho nền tảng để truy vấn dung lượng còn trống không thành công.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_is_bundle:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bundle**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_DirAccess_method_is_bundle>`

Trả về ``true`` nếu thư mục là một bundle của macOS.

\ **Lưu ý:** Method này được triển khai trên macOS.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_is_case_sensitive:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_case_sensitive**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_DirAccess_method_is_case_sensitive>`

Trả về ``true`` nếu file system hoặc thư mục sử dụng tên tệp phân biệt chữ hoa chữ thường.

\ **Lưu ý:** Method này được triển khai trên macOS, Linux (chỉ cho file system EXT4 và F2FS) và Windows. Trên các nền tảng khác, method luôn trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_is_equivalent:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_equivalent**\ (\ path_a\: :ref:`String<class_String>`, path_b\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_DirAccess_method_is_equivalent>`

Trả về ``true`` nếu các đường dẫn ``path_a`` và ``path_b`` trỏ đến cùng một đối tượng file system. Nếu không, trả về ``false``, ngay cả khi các tệp giống hệt nhau từng bit (ví dụ: các bản sao giống hệt nhau của tệp nhưng không phải là symbolic link).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_is_link:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_link**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_is_link>`

Trả về ``true`` nếu tệp hoặc thư mục là symbolic link, directory junction hoặc reparse point khác.

\ **Lưu ý:** Method này được triển khai trên macOS, Linux và Windows.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_list_dir_begin:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **list_dir_begin**\ (\ ) :ref:`🔗<class_DirAccess_method_list_dir_begin>`

Khởi tạo stream được sử dụng để liệt kê tất cả tệp và thư mục bằng function :ref:`get_next()<class_DirAccess_method_get_next>`, đồng thời đóng stream hiện đang mở nếu cần. Sau khi stream được xử lý, thông thường nên đóng nó bằng :ref:`list_dir_end()<class_DirAccess_method_list_dir_end>`.

Bị ảnh hưởng bởi :ref:`include_hidden<class_DirAccess_property_include_hidden>` và :ref:`include_navigational<class_DirAccess_property_include_navigational>`.

\ **Lưu ý:** Thứ tự các tệp và thư mục được method này trả về không xác định và có thể khác nhau giữa các hệ điều hành. Nếu bạn muốn có danh sách tất cả tệp hoặc thư mục được sắp xếp theo thứ tự alphabet, hãy sử dụng :ref:`get_files()<class_DirAccess_method_get_files>` hoặc :ref:`get_directories()<class_DirAccess_method_get_directories>`.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_list_dir_end:

.. rst-class:: classref-method

|void| **list_dir_end**\ (\ ) :ref:`🔗<class_DirAccess_method_list_dir_end>`

Đóng stream hiện tại được mở bằng :ref:`list_dir_begin()<class_DirAccess_method_list_dir_begin>` (việc stream đã được xử lý hoàn toàn bằng :ref:`get_next()<class_DirAccess_method_get_next>` hay chưa không quan trọng).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_make_dir:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **make_dir**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_make_dir>`

Tạo một thư mục. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại hoặc đường dẫn tuyệt đối. Thư mục đích phải được đặt trong một thư mục đã tồn tại (để tạo toàn bộ đường dẫn một cách đệ quy, hãy xem :ref:`make_dir_recursive()<class_DirAccess_method_make_dir_recursive>`).

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_make_dir_absolute:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **make_dir_absolute**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_make_dir_absolute>`

Phiên bản static của :ref:`make_dir()<class_DirAccess_method_make_dir>`. Chỉ hỗ trợ các đường dẫn tuyệt đối.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_make_dir_recursive:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **make_dir_recursive**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_make_dir_recursive>`

Tạo một thư mục đích cùng tất cả thư mục trung gian cần thiết trong đường dẫn của nó bằng cách gọi đệ quy :ref:`make_dir()<class_DirAccess_method_make_dir>`. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại hoặc đường dẫn tuyệt đối.

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_make_dir_recursive_absolute:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **make_dir_recursive_absolute**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_make_dir_recursive_absolute>`

Phiên bản static của :ref:`make_dir_recursive()<class_DirAccess_method_make_dir_recursive>`. Chỉ hỗ trợ các đường dẫn tuyệt đối.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_open:

.. rst-class:: classref-method

:ref:`DirAccess<class_DirAccess>` **open**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_open>`

Tạo một đối tượng **DirAccess** mới và mở một thư mục hiện có trong file system. Đối số ``path`` có thể nằm trong cây project (``res://folder``), thư mục người dùng (``user://folder``) hoặc một đường dẫn tuyệt đối trong file system của người dùng (ví dụ: ``/tmp/folder`` hoặc ``C:\tmp\folder``).

Trả về ``null`` nếu mở thư mục không thành công. Bạn có thể sử dụng :ref:`get_open_error()<class_DirAccess_method_get_open_error>` để kiểm tra lỗi đã xảy ra.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_read_link:

.. rst-class:: classref-method

:ref:`String<class_String>` **read_link**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_read_link>`

Trả về đích của symbolic link.

\ **Lưu ý:** Method này được triển khai trên macOS, Linux và Windows.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_remove:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **remove**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_remove>`

Xóa vĩnh viễn tệp đích hoặc một thư mục rỗng. Đối số có thể là đường dẫn tương đối so với thư mục hiện tại hoặc đường dẫn tuyệt đối. Nếu thư mục đích không rỗng, thao tác sẽ thất bại.

Nếu bạn không muốn xóa tệp/thư mục vĩnh viễn, hãy sử dụng :ref:`OS.move_to_trash()<class_OS_method_move_to_trash>` thay thế.

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_remove_absolute:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **remove_absolute**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_remove_absolute>`

Phiên bản static của :ref:`remove()<class_DirAccess_method_remove>`. Chỉ hỗ trợ các đường dẫn tuyệt đối.

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_rename:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **rename**\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DirAccess_method_rename>`

Đổi tên (di chuyển) tệp hoặc thư mục ``from`` đến đích ``to``. Cả hai đối số phải là đường dẫn đến tệp hoặc thư mục, có thể là đường dẫn tương đối hoặc tuyệt đối. Nếu tệp hoặc thư mục đích đã tồn tại và không được bảo vệ khỏi quyền truy cập, nó sẽ bị ghi đè.

Trả về một trong các hằng số mã :ref:`Error<enum_@GlobalScope_Error>` (:ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công).

.. rst-class:: classref-item-separator

----

.. _class_DirAccess_method_rename_absolute:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **rename_absolute**\ (\ from\: :ref:`String<class_String>`, to\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_DirAccess_method_rename_absolute>`

Phiên bản static của :ref:`rename()<class_DirAccess_method_rename>`. Chỉ hỗ trợ các đường dẫn tuyệt đối.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
