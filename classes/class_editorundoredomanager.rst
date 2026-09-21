:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorUndoRedoManager.xml.

.. _class_EditorUndoRedoManager:

EditorUndoRedoManager
=====================

**Kế thừa:** :ref:`Object<class_Object>`

Quản lý lịch sử undo của các scene được mở trong editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorUndoRedoManager** là một trình quản lý các đối tượng :ref:`UndoRedo<class_UndoRedo>` liên kết với những scene đang được chỉnh sửa. Mỗi scene có lịch sử undo riêng và **EditorUndoRedoManager** đảm bảo mỗi action được thực hiện trong editor đều được liên kết với scene thích hợp. Đối với các action không liên quan đến scene (chỉnh sửa :ref:`ProjectSettings<class_ProjectSettings>`, tài nguyên bên ngoài, v.v.), một lịch sử toàn cục riêng sẽ được sử dụng.

Cách sử dụng hầu như giống với :ref:`UndoRedo<class_UndoRedo>`. Bạn tạo và commit các action, còn trình quản lý sẽ tự động quyết định ở phía backend action đó thuộc về scene nào. Scene được suy ra dựa trên operation đầu tiên trong một action, bằng cách sử dụng object từ operation đó. Các quy tắc như sau:

- Nếu object là một :ref:`Node<class_Node>`, hãy sử dụng scene hiện đang được chỉnh sửa;

- Nếu object là một tài nguyên tích hợp sẵn, hãy sử dụng scene từ path của tài nguyên đó;

- Nếu object là tài nguyên bên ngoài hoặc bất kỳ thứ gì khác, hãy sử dụng lịch sử toàn cục.

Việc suy đoán này đôi khi có thể cho kết quả sai, vì vậy bạn có thể cung cấp một object context tùy chỉnh khi tạo action.

\ **EditorUndoRedoManager** được thiết kế để sử dụng bởi các plugin của Godot editor. Bạn có thể lấy nó bằng :ref:`EditorPlugin.get_undo_redo()<class_EditorPlugin_method_get_undo_redo>`. Đối với các mục đích sử dụng không thuộc editor hoặc các plugin không cần tích hợp với lịch sử undo của editor, hãy sử dụng :ref:`UndoRedo<class_UndoRedo>` thay thế.

API của trình quản lý hầu như giống với :ref:`UndoRedo<class_UndoRedo>`, vì vậy bạn có thể tham khảo tài liệu của nó để xem thêm ví dụ. Điểm khác biệt chính là **EditorUndoRedoManager** sử dụng object + tên method cho các action, thay vì :ref:`Callable<class_Callable>`.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_do_method<class_EditorUndoRedoManager_method_add_do_method>`\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                                                        |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_do_property<class_EditorUndoRedoManager_method_add_do_property>`\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                                         |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_do_reference<class_EditorUndoRedoManager_method_add_do_reference>`\ (\ object\: :ref:`Object<class_Object>`\ )                                                                                                                                                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_undo_method<class_EditorUndoRedoManager_method_add_undo_method>`\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                                                    |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_undo_property<class_EditorUndoRedoManager_method_add_undo_property>`\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                                     |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_undo_reference<class_EditorUndoRedoManager_method_add_undo_reference>`\ (\ object\: :ref:`Object<class_Object>`\ )                                                                                                                                                                                                          |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`clear_history<class_EditorUndoRedoManager_method_clear_history>`\ (\ id\: :ref:`int<class_int>` = -99, increase_version\: :ref:`bool<class_bool>` = true\ )                                                                                                                                                                     |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`commit_action<class_EditorUndoRedoManager_method_commit_action>`\ (\ execute\: :ref:`bool<class_bool>` = true\ )                                                                                                                                                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`create_action<class_EditorUndoRedoManager_method_create_action>`\ (\ name\: :ref:`String<class_String>`, merge_mode\: :ref:`MergeMode<enum_UndoRedo_MergeMode>` = 0, custom_context\: :ref:`Object<class_Object>` = null, backward_undo_ops\: :ref:`bool<class_bool>` = false, mark_unsaved\: :ref:`bool<class_bool>` = true\ ) |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`force_fixed_history<class_EditorUndoRedoManager_method_force_fixed_history>`\ (\ )                                                                                                                                                                                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`UndoRedo<class_UndoRedo>` | :ref:`get_history_undo_redo<class_EditorUndoRedoManager_method_get_history_undo_redo>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                      |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`get_object_history_id<class_EditorUndoRedoManager_method_get_object_history_id>`\ (\ object\: :ref:`Object<class_Object>`\ ) |const|                                                                                                                                                                                            |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`is_committing_action<class_EditorUndoRedoManager_method_is_committing_action>`\ (\ ) |const|                                                                                                                                                                                                                                    |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_EditorUndoRedoManager_signal_history_changed:

.. rst-class:: classref-signal

**history_changed**\ (\ ) :ref:`🔗<class_EditorUndoRedoManager_signal_history_changed>`

Được phát ra khi danh sách action trong bất kỳ lịch sử nào thay đổi, dù là khi một action được commit hay khi một lịch sử bị xóa.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_signal_version_changed:

.. rst-class:: classref-signal

**version_changed**\ (\ ) :ref:`🔗<class_EditorUndoRedoManager_signal_version_changed>`

Được phát ra khi version của bất kỳ lịch sử nào thay đổi do lệnh undo hoặc redo.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_EditorUndoRedoManager_SpecialHistory:

.. rst-class:: classref-enumeration

enum **SpecialHistory**: :ref:`🔗<enum_EditorUndoRedoManager_SpecialHistory>`

.. _class_EditorUndoRedoManager_constant_GLOBAL_HISTORY:

.. rst-class:: classref-enumeration-constant

:ref:`SpecialHistory<enum_EditorUndoRedoManager_SpecialHistory>` **GLOBAL_HISTORY** = ``0``

Lịch sử toàn cục không liên kết với bất kỳ scene nào mà liên kết với các tài nguyên bên ngoài, v.v.

.. _class_EditorUndoRedoManager_constant_REMOTE_HISTORY:

.. rst-class:: classref-enumeration-constant

:ref:`SpecialHistory<enum_EditorUndoRedoManager_SpecialHistory>` **REMOTE_HISTORY** = ``-9``

Lịch sử liên kết với remote inspector. Được sử dụng khi live editing một project đang chạy.

.. _class_EditorUndoRedoManager_constant_INVALID_HISTORY:

.. rst-class:: classref-enumeration-constant

:ref:`SpecialHistory<enum_EditorUndoRedoManager_SpecialHistory>` **INVALID_HISTORY** = ``-99``

Lịch sử "null" không hợp lệ. Đây là một giá trị đặc biệt, không liên kết với bất kỳ object nào.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_EditorUndoRedoManager_method_add_do_method:

.. rst-class:: classref-method

|void| **add_do_method**\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_EditorUndoRedoManager_method_add_do_method>`

Đăng ký một method sẽ được gọi khi action được commit (tức là action "do").

Nếu đây là operation đầu tiên, ``object`` sẽ được sử dụng để suy ra lịch sử undo đích.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_add_do_property:

.. rst-class:: classref-method

|void| **add_do_property**\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_EditorUndoRedoManager_method_add_do_property>`

Đăng ký một thay đổi giá trị property cho "do".

Nếu đây là operation đầu tiên, ``object`` sẽ được sử dụng để suy ra lịch sử undo đích.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_add_do_reference:

.. rst-class:: classref-method

|void| **add_do_reference**\ (\ object\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_EditorUndoRedoManager_method_add_do_reference>`

Đăng ký một reference cho "do", reference này sẽ bị xóa nếu lịch sử "do" bị mất. Điều này chủ yếu hữu ích cho các node mới được tạo trong lệnh gọi "do". Không sử dụng cho các resource.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_add_undo_method:

.. rst-class:: classref-method

|void| **add_undo_method**\ (\ object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_EditorUndoRedoManager_method_add_undo_method>`

Đăng ký một method sẽ được gọi khi action được undo (tức là action "undo").

Nếu đây là operation đầu tiên, ``object`` sẽ được sử dụng để suy ra lịch sử undo đích.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_add_undo_property:

.. rst-class:: classref-method

|void| **add_undo_property**\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_EditorUndoRedoManager_method_add_undo_property>`

Đăng ký một thay đổi giá trị property cho "undo".

Nếu đây là operation đầu tiên, ``object`` sẽ được sử dụng để suy ra lịch sử undo đích.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_add_undo_reference:

.. rst-class:: classref-method

|void| **add_undo_reference**\ (\ object\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_EditorUndoRedoManager_method_add_undo_reference>`

Đăng ký một reference cho "undo", reference này sẽ bị xóa nếu lịch sử "undo" bị mất. Điều này chủ yếu hữu ích cho các node bị xóa bằng lệnh gọi "do" (không phải lệnh gọi "undo"!).

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_clear_history:

.. rst-class:: classref-method

|void| **clear_history**\ (\ id\: :ref:`int<class_int>` = -99, increase_version\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_EditorUndoRedoManager_method_clear_history>`

Xóa lịch sử undo được chỉ định. Bạn có thể xóa lịch sử của một scene cụ thể, lịch sử toàn cục hoặc tất cả lịch sử cùng lúc (ngoại trừ :ref:`REMOTE_HISTORY<class_EditorUndoRedoManager_constant_REMOTE_HISTORY>`) nếu ``id`` là :ref:`INVALID_HISTORY<class_EditorUndoRedoManager_constant_INVALID_HISTORY>`.

Nếu ``increase_version`` là ``true``, version của lịch sử undo sẽ được tăng lên, đánh dấu lịch sử là chưa được lưu. Hữu ích cho các operation sửa đổi scene nhưng không hỗ trợ undo.

::

    var scene_root = EditorInterface.get_edited_scene_root()
    var undo_redo = EditorInterface.get_editor_undo_redo()
    undo_redo.clear_history(undo_redo.get_object_history_id(scene_root))

\ **Lưu ý:** Nếu bạn muốn đánh dấu một scene đã chỉnh sửa là chưa được lưu mà không xóa lịch sử của nó, hãy sử dụng :ref:`EditorInterface.mark_scene_as_unsaved()<class_EditorInterface_method_mark_scene_as_unsaved>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_commit_action:

.. rst-class:: classref-method

|void| **commit_action**\ (\ execute\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_EditorUndoRedoManager_method_commit_action>`

Commit action. Nếu ``execute`` là ``true`` (mặc định), tất cả method/property "do" sẽ được gọi/thiết lập khi hàm này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_create_action:

.. rst-class:: classref-method

|void| **create_action**\ (\ name\: :ref:`String<class_String>`, merge_mode\: :ref:`MergeMode<enum_UndoRedo_MergeMode>` = 0, custom_context\: :ref:`Object<class_Object>` = null, backward_undo_ops\: :ref:`bool<class_bool>` = false, mark_unsaved\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_EditorUndoRedoManager_method_create_action>`

Tạo một action mới. Sau khi gọi hàm này, hãy thực hiện tất cả các lệnh gọi đến :ref:`add_do_method()<class_EditorUndoRedoManager_method_add_do_method>`, :ref:`add_undo_method()<class_EditorUndoRedoManager_method_add_undo_method>`, :ref:`add_do_property()<class_EditorUndoRedoManager_method_add_do_property>` và :ref:`add_undo_property()<class_EditorUndoRedoManager_method_add_undo_property>`, sau đó commit action bằng :ref:`commit_action()<class_EditorUndoRedoManager_method_commit_action>`.

Cách các action được merge được quy định bởi argument ``merge_mode``.

Nếu cung cấp object ``custom_context``, object đó sẽ được sử dụng để suy ra lịch sử đích (thay vì sử dụng operation đầu tiên).

Cách sắp xếp các operation undo trong action được quy định bởi ``backward_undo_ops``. Khi ``backward_undo_ops`` là ``false``, các tùy chọn undo được sắp xếp theo cùng thứ tự chúng được thêm vào. Điều đó có nghĩa là operation đầu tiên được thêm vào sẽ là operation đầu tiên được undo.

Nếu ``mark_unsaved`` là ``false``, action sẽ không đánh dấu lịch sử là chưa được lưu. Điều này hữu ích chẳng hạn với các action thay đổi lựa chọn hoặc một setting sẽ được tự động lưu. Nếu không, nên giữ giá trị này là ``true`` nếu action yêu cầu người dùng lưu hoặc có thể gây mất dữ liệu khi để ở trạng thái chưa được lưu.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_force_fixed_history:

.. rst-class:: classref-method

|void| **force_fixed_history**\ (\ ) :ref:`🔗<class_EditorUndoRedoManager_method_force_fixed_history>`

Buộc operation tiếp theo (ví dụ :ref:`add_do_method()<class_EditorUndoRedoManager_method_add_do_method>`) sử dụng lịch sử của action thay vì suy đoán từ object. Điều này đôi khi cần thiết khi không thể xác định chính xác một lịch sử, chẳng hạn với một resource lồng nhau chưa có path.

Chỉ nên sử dụng method này khi thực sự cần thiết, nếu không nó có thể gây ra trạng thái lịch sử không hợp lệ. Đối với hầu hết các trường hợp phức tạp, parameter ``custom_context`` của :ref:`create_action()<class_EditorUndoRedoManager_method_create_action>` là đủ.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_get_history_undo_redo:

.. rst-class:: classref-method

:ref:`UndoRedo<class_UndoRedo>` **get_history_undo_redo**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorUndoRedoManager_method_get_history_undo_redo>`

Trả về object :ref:`UndoRedo<class_UndoRedo>` được liên kết với history ``id`` đã cho.

\ Các ``id`` ở trên ``0`` được ánh xạ tới các tab scene đang mở (nhưng không khớp với thứ tự của chúng). ``id`` của ``0`` trở xuống có ý nghĩa đặc biệt (xem :ref:`SpecialHistory<enum_EditorUndoRedoManager_SpecialHistory>`).

Tốt nhất nên sử dụng cùng với :ref:`get_object_history_id()<class_EditorUndoRedoManager_method_get_object_history_id>`. Method này chỉ được cung cấp trong trường hợp bạn cần một số method nâng cao hơn của :ref:`UndoRedo<class_UndoRedo>` (nhưng hãy lưu ý rằng việc thao tác trực tiếp trên object :ref:`UndoRedo<class_UndoRedo>` có thể ảnh hưởng đến độ ổn định của editor).

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_get_object_history_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_object_history_id**\ (\ object\: :ref:`Object<class_Object>`\ ) |const| :ref:`🔗<class_EditorUndoRedoManager_method_get_object_history_id>`

Trả về history ID được suy ra từ ``object`` đã cho. ID này có thể được sử dụng với :ref:`get_history_undo_redo()<class_EditorUndoRedoManager_method_get_history_undo_redo>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorUndoRedoManager_method_is_committing_action:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_committing_action**\ (\ ) |const| :ref:`🔗<class_EditorUndoRedoManager_method_is_committing_action>`

Trả về ``true`` nếu **EditorUndoRedoManager** hiện đang commit action, tức là đang chạy method "do" hoặc thay đổi property của action đó (xem :ref:`commit_action()<class_EditorUndoRedoManager_method_commit_action>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
