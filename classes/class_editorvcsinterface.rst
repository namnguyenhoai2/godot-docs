:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorVCSInterface.xml.

.. _class_EditorVCSInterface:

EditorVCSInterface
==================

**Kế thừa:** :ref:`Object<class_Object>`

Giao diện Hệ thống Kiểm soát Phiên bản (VCS), dùng để đọc và ghi vào VCS cục bộ đang được sử dụng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Định nghĩa API mà editor sử dụng để trích xuất thông tin từ VCS bên dưới. Phần triển khai API này được bao gồm trong các plugin VCS, là các plugin GDExtension kế thừa **EditorVCSInterface** và được gắn vào (khi có yêu cầu) instance singleton của **EditorVCSInterface**. Thay vì tự thực hiện tác vụ, tất cả các hàm virtual được liệt kê bên dưới đều gọi các hàm được override bên trong các plugin VCS để cung cấp trải nghiệm plug-n-play. Một plugin VCS tùy chỉnh được cho là sẽ kế thừa từ **EditorVCSInterface** và override từng hàm virtual này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Hệ thống kiểm soát phiên bản <../tutorials/best_practices/version_control_systems>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_allow_amends<class_EditorVCSInterface_private_method__allow_amends>`\ (\ ) |virtual|                                                                                                                                                                                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_checkout_branch<class_EditorVCSInterface_private_method__checkout_branch>`\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                           |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_commit<class_EditorVCSInterface_private_method__commit>`\ (\ msg\: :ref:`String<class_String>`, amend\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                                                                                                                               |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_create_branch<class_EditorVCSInterface_private_method__create_branch>`\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                               |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_create_remote<class_EditorVCSInterface_private_method__create_remote>`\ (\ remote_name\: :ref:`String<class_String>`, remote_url\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                     |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_discard_file<class_EditorVCSInterface_private_method__discard_file>`\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                   |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_fetch<class_EditorVCSInterface_private_method__fetch>`\ (\ remote\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                                    |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]         | :ref:`_get_branch_list<class_EditorVCSInterface_private_method__get_branch_list>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_current_branch_name<class_EditorVCSInterface_private_method__get_current_branch_name>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_diff<class_EditorVCSInterface_private_method__get_diff>`\ (\ identifier\: :ref:`String<class_String>`, area\: :ref:`int<class_int>`\ ) |virtual| |required|                                                                                                                                                                            |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_line_diff<class_EditorVCSInterface_private_method__get_line_diff>`\ (\ file_path\: :ref:`String<class_String>`, text\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                             |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_modified_files_data<class_EditorVCSInterface_private_method__get_modified_files_data>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_previous_commits<class_EditorVCSInterface_private_method__get_previous_commits>`\ (\ max_commits\: :ref:`int<class_int>`\ ) |virtual| |required|                                                                                                                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]         | :ref:`_get_remotes<class_EditorVCSInterface_private_method__get_remotes>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                                              |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_vcs_name<class_EditorVCSInterface_private_method__get_vcs_name>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                                            |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_initialize<class_EditorVCSInterface_private_method__initialize>`\ (\ project_path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                    |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_pull<class_EditorVCSInterface_private_method__pull>`\ (\ remote\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_push<class_EditorVCSInterface_private_method__push>`\ (\ remote\: :ref:`String<class_String>`, force\: :ref:`bool<class_bool>`\ ) |virtual| |required|                                                                                                                                                                                     |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_remove_branch<class_EditorVCSInterface_private_method__remove_branch>`\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                               |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_remove_remote<class_EditorVCSInterface_private_method__remove_remote>`\ (\ remote_name\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                               |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_set_credentials<class_EditorVCSInterface_private_method__set_credentials>`\ (\ username\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`, ssh_public_key_path\: :ref:`String<class_String>`, ssh_private_key_path\: :ref:`String<class_String>`, ssh_passphrase\: :ref:`String<class_String>`\ ) |virtual| |required| |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_shut_down<class_EditorVCSInterface_private_method__shut_down>`\ (\ ) |virtual| |required|                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_stage_file<class_EditorVCSInterface_private_method__stage_file>`\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_unstage_file<class_EditorVCSInterface_private_method__unstage_file>`\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required|                                                                                                                                                                                                   |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`add_diff_hunks_into_diff_file<class_EditorVCSInterface_method_add_diff_hunks_into_diff_file>`\ (\ diff_file\: :ref:`Dictionary<class_Dictionary>`, diff_hunks\: :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\]\ )                                                                                                         |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`add_line_diffs_into_diff_hunk<class_EditorVCSInterface_method_add_line_diffs_into_diff_hunk>`\ (\ diff_hunk\: :ref:`Dictionary<class_Dictionary>`, line_diffs\: :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\]\ )                                                                                                         |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`create_commit<class_EditorVCSInterface_method_create_commit>`\ (\ msg\: :ref:`String<class_String>`, author\: :ref:`String<class_String>`, id\: :ref:`String<class_String>`, unix_timestamp\: :ref:`int<class_int>`, offset_minutes\: :ref:`int<class_int>`\ )                                                                              |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`create_diff_file<class_EditorVCSInterface_method_create_diff_file>`\ (\ new_file\: :ref:`String<class_String>`, old_file\: :ref:`String<class_String>`\ )                                                                                                                                                                                   |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`create_diff_hunk<class_EditorVCSInterface_method_create_diff_hunk>`\ (\ old_start\: :ref:`int<class_int>`, new_start\: :ref:`int<class_int>`, old_lines\: :ref:`int<class_int>`, new_lines\: :ref:`int<class_int>`\ )                                                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`create_diff_line<class_EditorVCSInterface_method_create_diff_line>`\ (\ new_line_no\: :ref:`int<class_int>`, old_line_no\: :ref:`int<class_int>`, content\: :ref:`String<class_String>`, status\: :ref:`String<class_String>`\ )                                                                                                            |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`create_status_file<class_EditorVCSInterface_method_create_status_file>`\ (\ file_path\: :ref:`String<class_String>`, change_type\: :ref:`ChangeType<enum_EditorVCSInterface_ChangeType>`, area\: :ref:`TreeArea<enum_EditorVCSInterface_TreeArea>`\ )                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`popup_error<class_EditorVCSInterface_method_popup_error>`\ (\ msg\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                          |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_EditorVCSInterface_ChangeType:

.. rst-class:: classref-enumeration

enum **ChangeType**: :ref:`🔗<enum_EditorVCSInterface_ChangeType>`

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_NEW:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_NEW** = ``0``

Một tệp mới đã được thêm.

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_MODIFIED:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_MODIFIED** = ``1``

Một tệp đã được thêm trước đó đã bị sửa đổi.

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_RENAMED:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_RENAMED** = ``2``

Một tệp đã được thêm trước đó đã được đổi tên.

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_DELETED:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_DELETED** = ``3``

Một tệp đã được thêm trước đó đã bị xóa.

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_TYPECHANGE:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_TYPECHANGE** = ``4``

Kiểu của một tệp đã được thêm trước đó đã bị thay đổi.

.. _class_EditorVCSInterface_constant_CHANGE_TYPE_UNMERGED:

.. rst-class:: classref-enumeration-constant

:ref:`ChangeType<enum_EditorVCSInterface_ChangeType>` **CHANGE_TYPE_UNMERGED** = ``5``

Một tệp vẫn chưa được merge.

.. rst-class:: classref-item-separator

----

.. _enum_EditorVCSInterface_TreeArea:

.. rst-class:: classref-enumeration

enum **TreeArea**: :ref:`🔗<enum_EditorVCSInterface_TreeArea>`

.. _class_EditorVCSInterface_constant_TREE_AREA_COMMIT:

.. rst-class:: classref-enumeration-constant

:ref:`TreeArea<enum_EditorVCSInterface_TreeArea>` **TREE_AREA_COMMIT** = ``0``

Gặp một commit trong vùng commit.

.. _class_EditorVCSInterface_constant_TREE_AREA_STAGED:

.. rst-class:: classref-enumeration-constant

:ref:`TreeArea<enum_EditorVCSInterface_TreeArea>` **TREE_AREA_STAGED** = ``1``

Gặp một tệp trong vùng staged.

.. _class_EditorVCSInterface_constant_TREE_AREA_UNSTAGED:

.. rst-class:: classref-enumeration-constant

:ref:`TreeArea<enum_EditorVCSInterface_TreeArea>` **TREE_AREA_UNSTAGED** = ``2``

Gặp một tệp trong vùng unstaged.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorVCSInterface_private_method__allow_amends:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_allow_amends**\ (\ ) |virtual| :ref:`🔗<class_EditorVCSInterface_private_method__allow_amends>`

Trả về liệu plugin có cho phép amend commit hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__checkout_branch:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_checkout_branch**\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__checkout_branch>`

Checkout một ``branch_name`` trong VCS.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__commit:

.. rst-class:: classref-method

|void| **_commit**\ (\ msg\: :ref:`String<class_String>`, amend\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorVCSInterface_private_method__commit>`

Commit các thay đổi hiện đang staged và áp dụng ``msg`` commit cho commit kết quả. Nếu ``amend`` là ``true``, commit sẽ sửa đổi commit gần đây nhất thay vào đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__create_branch:

.. rst-class:: classref-method

|void| **_create_branch**\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__create_branch>`

Tạo một branch mới có tên ``branch_name`` trong VCS.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__create_remote:

.. rst-class:: classref-method

|void| **_create_remote**\ (\ remote_name\: :ref:`String<class_String>`, remote_url\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__create_remote>`

Tạo một đích remote mới có tên ``remote_name`` và trỏ nó đến ``remote_url``. Đây có thể là remote HTTPS hoặc remote SSH.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__discard_file:

.. rst-class:: classref-method

|void| **_discard_file**\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__discard_file>`

Loại bỏ các thay đổi đã thực hiện trong tệp nằm tại ``file_path``.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__fetch:

.. rst-class:: classref-method

|void| **_fetch**\ (\ remote\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__fetch>`

Fetch các thay đổi mới từ ``remote``, nhưng không ghi các thay đổi vào thư mục làm việc hiện tại. Tương đương với ``git fetch``.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_branch_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`String<class_String>`\] **_get_branch_list**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_branch_list>`

Lấy một instance :ref:`Array<class_Array>` gồm :ref:`String<class_String>`\ s chứa các tên branch hiện có trong VCS.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_current_branch_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_current_branch_name**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_current_branch_name>`

Lấy tên branch hiện tại được định nghĩa trong VCS.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_diff:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_diff**\ (\ identifier\: :ref:`String<class_String>`, area\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_diff>`

Trả về một mảng gồm các mục :ref:`Dictionary<class_Dictionary>` (xem :ref:`create_diff_file()<class_EditorVCSInterface_method_create_diff_file>`, :ref:`create_diff_hunk()<class_EditorVCSInterface_method_create_diff_hunk>`, :ref:`create_diff_line()<class_EditorVCSInterface_method_create_diff_line>`, :ref:`add_line_diffs_into_diff_hunk()<class_EditorVCSInterface_method_add_line_diffs_into_diff_hunk>` và :ref:`add_diff_hunks_into_diff_file()<class_EditorVCSInterface_method_add_diff_hunks_into_diff_file>`), mỗi mục chứa thông tin về một diff. Nếu ``identifier`` là đường dẫn tệp, trả về diff của tệp; nếu đó là mã định danh commit, trả về diff của commit.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_line_diff:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_line_diff**\ (\ file_path\: :ref:`String<class_String>`, text\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_line_diff>`

Trả về một :ref:`Array<class_Array>` gồm các mục :ref:`Dictionary<class_Dictionary>` (xem :ref:`create_diff_hunk()<class_EditorVCSInterface_method_create_diff_hunk>`), mỗi mục chứa diff theo dòng giữa một tệp tại ``file_path`` và ``text`` được truyền vào.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_modified_files_data:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_modified_files_data**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_modified_files_data>`

Trả về một :ref:`Array<class_Array>` gồm các mục :ref:`Dictionary<class_Dictionary>` (xem :ref:`create_status_file()<class_EditorVCSInterface_method_create_status_file>`), mỗi mục chứa dữ liệu trạng thái của mọi tệp đã sửa đổi trong thư mục dự án.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_previous_commits:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_previous_commits**\ (\ max_commits\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_previous_commits>`

Trả về một :ref:`Array<class_Array>` gồm các mục :ref:`Dictionary<class_Dictionary>` (xem :ref:`create_commit()<class_EditorVCSInterface_method_create_commit>`), mỗi mục chứa dữ liệu của một commit trước đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_remotes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`String<class_String>`\] **_get_remotes**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_remotes>`

Trả về một :ref:`Array<class_Array>` gồm các :ref:`String<class_String>`\ s, mỗi mục chứa tên của một remote được cấu hình trong VCS.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__get_vcs_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_vcs_name**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__get_vcs_name>`

Trả về tên của nhà cung cấp VCS bên dưới.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__initialize:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_initialize**\ (\ project_path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__initialize>`

Khởi tạo plugin VCS khi được gọi từ editor. Trả về liệu plugin có được khởi tạo thành công hay không. Một dự án VCS được khởi tạo tại ``project_path``.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__pull:

.. rst-class:: classref-method

|void| **_pull**\ (\ remote\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__pull>`

Pull các thay đổi từ remote. Việc này có thể dẫn đến xung đột merge.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__push:

.. rst-class:: classref-method

|void| **_push**\ (\ remote\: :ref:`String<class_String>`, force\: :ref:`bool<class_bool>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__push>`

Push các thay đổi lên ``remote``. Nếu ``force`` là ``true``, force push sẽ ghi đè lịch sử thay đổi đã có trên remote.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__remove_branch:

.. rst-class:: classref-method

|void| **_remove_branch**\ (\ branch_name\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__remove_branch>`

Xóa một branch khỏi VCS cục bộ.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__remove_remote:

.. rst-class:: classref-method

|void| **_remove_remote**\ (\ remote_name\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__remove_remote>`

Xóa một remote khỏi VCS cục bộ.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__set_credentials:

.. rst-class:: classref-method

|void| **_set_credentials**\ (\ username\: :ref:`String<class_String>`, password\: :ref:`String<class_String>`, ssh_public_key_path\: :ref:`String<class_String>`, ssh_private_key_path\: :ref:`String<class_String>`, ssh_passphrase\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__set_credentials>`

Đặt thông tin xác thực người dùng trong VCS bên dưới. ``username`` và ``password`` chỉ được sử dụng trong quá trình xác thực HTTPS, trừ khi chúng chưa được nêu trong remote URL. ``ssh_public_key_path``, ``ssh_private_key_path`` và ``ssh_passphrase`` chỉ được sử dụng trong quá trình xác thực SSH.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__shut_down:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_shut_down**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__shut_down>`

Tắt instance plugin VCS. Được gọi khi người dùng đóng editor hoặc tắt plugin VCS thông qua UI của editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__stage_file:

.. rst-class:: classref-method

|void| **_stage_file**\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__stage_file>`

Đưa tệp nằm tại ``file_path`` vào vùng staged.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_private_method__unstage_file:

.. rst-class:: classref-method

|void| **_unstage_file**\ (\ file_path\: :ref:`String<class_String>`\ ) |virtual| |required| :ref:`🔗<class_EditorVCSInterface_private_method__unstage_file>`

Đưa tệp nằm tại ``file_path`` ra khỏi vùng staged và chuyển vào vùng unstaged.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_add_diff_hunks_into_diff_file:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **add_diff_hunks_into_diff_file**\ (\ diff_file\: :ref:`Dictionary<class_Dictionary>`, diff_hunks\: :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\]\ ) :ref:`🔗<class_EditorVCSInterface_method_add_diff_hunks_into_diff_file>`

Hàm trợ giúp để thêm một mảng ``diff_hunks`` vào một ``diff_file``.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_add_line_diffs_into_diff_hunk:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **add_line_diffs_into_diff_hunk**\ (\ diff_hunk\: :ref:`Dictionary<class_Dictionary>`, line_diffs\: :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\]\ ) :ref:`🔗<class_EditorVCSInterface_method_add_line_diffs_into_diff_hunk>`

Hàm trợ giúp để thêm một mảng ``line_diffs`` vào một ``diff_hunk``.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_create_commit:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **create_commit**\ (\ msg\: :ref:`String<class_String>`, author\: :ref:`String<class_String>`, id\: :ref:`String<class_String>`, unix_timestamp\: :ref:`int<class_int>`, offset_minutes\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorVCSInterface_method_create_commit>`

Hàm trợ giúp để tạo một mục commit :ref:`Dictionary<class_Dictionary>`. ``msg`` là thông điệp của commit. ``author`` là một chuỗi duy nhất, dễ đọc chứa tất cả thông tin chi tiết của tác giả, chẳng hạn như email và tên được cấu hình trong VCS. ``id`` là mã định danh của commit, ở bất kỳ định dạng nào mà VCS của bạn có thể cung cấp cho mã định danh của các commit. ``unix_timestamp`` là Unix timestamp UTC về thời điểm commit được tạo. ``offset_minutes`` là độ lệch múi giờ tính bằng phút, được ghi nhận từ múi giờ hệ thống nơi commit được tạo.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_create_diff_file:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **create_diff_file**\ (\ new_file\: :ref:`String<class_String>`, old_file\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorVCSInterface_method_create_diff_file>`

Hàm trợ giúp để tạo một :ref:`Dictionary<class_Dictionary>` dùng để lưu trữ các đường dẫn tệp diff cũ và mới.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_create_diff_hunk:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **create_diff_hunk**\ (\ old_start\: :ref:`int<class_int>`, new_start\: :ref:`int<class_int>`, old_lines\: :ref:`int<class_int>`, new_lines\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorVCSInterface_method_create_diff_hunk>`

Hàm trợ giúp để tạo một :ref:`Dictionary<class_Dictionary>` dùng để lưu trữ dữ liệu diff hunk. ``old_start`` là số dòng bắt đầu trong tệp cũ. ``new_start`` là số dòng bắt đầu trong tệp mới. ``old_lines`` là số dòng trong tệp cũ. ``new_lines`` là số dòng trong tệp mới.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_create_diff_line:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **create_diff_line**\ (\ new_line_no\: :ref:`int<class_int>`, old_line_no\: :ref:`int<class_int>`, content\: :ref:`String<class_String>`, status\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorVCSInterface_method_create_diff_line>`

Hàm trợ giúp để tạo một :ref:`Dictionary<class_Dictionary>` dùng để lưu trữ một line diff. ``new_line_no`` là số dòng trong tệp mới (có thể là ``-1`` nếu dòng bị xóa). ``old_line_no`` là số dòng trong tệp cũ (có thể là ``-1`` nếu dòng được thêm vào). ``content`` là văn bản diff. ``status`` là một chuỗi ký tự đơn lưu trữ nguồn gốc của dòng.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_create_status_file:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **create_status_file**\ (\ file_path\: :ref:`String<class_String>`, change_type\: :ref:`ChangeType<enum_EditorVCSInterface_ChangeType>`, area\: :ref:`TreeArea<enum_EditorVCSInterface_TreeArea>`\ ) :ref:`🔗<class_EditorVCSInterface_method_create_status_file>`

Hàm trợ giúp để tạo một :ref:`Dictionary<class_Dictionary>` được editor sử dụng để đọc trạng thái của một tệp.

.. rst-class:: classref-item-separator

----

.. _class_EditorVCSInterface_method_popup_error:

.. rst-class:: classref-method

|void| **popup_error**\ (\ msg\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorVCSInterface_method_popup_error>`

Hiển thị một thông báo lỗi bật lên trong editor, cho biết thông báo đến từ VCS nền tảng. Sử dụng hàm này để hiển thị các thông báo lỗi cụ thể của VCS.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
