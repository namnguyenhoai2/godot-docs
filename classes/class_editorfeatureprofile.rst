:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorFeatureProfile.xml.

.. _class_EditorFeatureProfile:

EditorFeatureProfile
====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một editor feature profile có thể được dùng để vô hiệu hóa các tính năng cụ thể.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một editor feature profile có thể được dùng để vô hiệu hóa các tính năng cụ thể của Godot editor. Khi bị vô hiệu hóa, các tính năng sẽ không xuất hiện trong editor, giúp giao diện bớt rối hơn. Điều này hữu ích trong môi trường giáo dục để giảm sự nhầm lẫn hoặc khi làm việc theo nhóm. Ví dụ, artist và level designer có thể sử dụng một feature profile vô hiệu hóa script editor để tránh vô tình thay đổi các tệp mà họ không được phép chỉnh sửa.

Để quản lý editor feature profile bằng giao diện trực quan, hãy sử dụng **Editor > Manage Feature Profiles...** ở phía trên cửa sổ editor.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_feature_name<class_EditorFeatureProfile_method_get_feature_name>`\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`\ )                                                                                             |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_class_disabled<class_EditorFeatureProfile_method_is_class_disabled>`\ (\ class_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                              |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_class_editor_disabled<class_EditorFeatureProfile_method_is_class_editor_disabled>`\ (\ class_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_class_property_disabled<class_EditorFeatureProfile_method_is_class_property_disabled>`\ (\ class_name\: :ref:`StringName<class_StringName>`, property\: :ref:`StringName<class_StringName>`\ ) |const|                            |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_feature_disabled<class_EditorFeatureProfile_method_is_feature_disabled>`\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`\ ) |const|                                                                               |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load_from_file<class_EditorFeatureProfile_method_load_from_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                          |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`save_to_file<class_EditorFeatureProfile_method_save_to_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                                              |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_disable_class<class_EditorFeatureProfile_method_set_disable_class>`\ (\ class_name\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ )                                                                   |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_disable_class_editor<class_EditorFeatureProfile_method_set_disable_class_editor>`\ (\ class_name\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ )                                                     |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_disable_class_property<class_EditorFeatureProfile_method_set_disable_class_property>`\ (\ class_name\: :ref:`StringName<class_StringName>`, property\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ ) |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_disable_feature<class_EditorFeatureProfile_method_set_disable_feature>`\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`, disable\: :ref:`bool<class_bool>`\ )                                                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_EditorFeatureProfile_Feature:

.. rst-class:: classref-enumeration

enum **Feature**: :ref:`🔗<enum_EditorFeatureProfile_Feature>`

.. _class_EditorFeatureProfile_constant_FEATURE_3D:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_3D** = ``0``

3D editor. Nếu tính năng này bị vô hiệu hóa, 3D editor sẽ không hiển thị, nhưng các node 3D vẫn sẽ hiển thị trong hộp thoại Create New Node.

.. _class_EditorFeatureProfile_constant_FEATURE_SCRIPT:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_SCRIPT** = ``1``

Tab Script, chứa script editor và class reference browser. Nếu tính năng này bị vô hiệu hóa, tab Script sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_ASSET_LIB:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_ASSET_LIB** = ``2``

Tab Asset Store. Nếu tính năng này bị vô hiệu hóa, tab Asset Store sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_SCENE_TREE:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_SCENE_TREE** = ``3``

Chỉnh sửa scene tree. Nếu tính năng này bị vô hiệu hóa, dock Scene tree vẫn hiển thị nhưng sẽ ở chế độ chỉ đọc.

.. _class_EditorFeatureProfile_constant_FEATURE_NODE_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_NODE_DOCK** = ``4``

**Đã deprecated:** Được thay thế bởi các dock Signals và Groups.

Dock Node. Nếu tính năng này bị vô hiệu hóa, signals và groups sẽ không hiển thị hoặc không thể chỉnh sửa từ editor.

.. _class_EditorFeatureProfile_constant_FEATURE_FILESYSTEM_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_FILESYSTEM_DOCK** = ``5``

Dock FileSystem. Nếu tính năng này bị vô hiệu hóa, dock FileSystem sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_IMPORT_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_IMPORT_DOCK** = ``6``

Dock Import. Nếu tính năng này bị vô hiệu hóa, dock Import sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_HISTORY_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_HISTORY_DOCK** = ``7``

Dock History. Nếu tính năng này bị vô hiệu hóa, dock History sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_GAME:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_GAME** = ``8``

Tab Game, cho phép nhúng cửa sổ game và chọn các node bằng cách nhấp vào bên trong cửa sổ. Nếu tính năng này bị vô hiệu hóa, tab Game sẽ không hiển thị.

.. _class_EditorFeatureProfile_constant_FEATURE_SIGNALS_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_SIGNALS_DOCK** = ``9``

Dock Signals. Nếu tính năng này bị vô hiệu hóa, signals sẽ không hiển thị hoặc không thể chỉnh sửa từ editor.

.. _class_EditorFeatureProfile_constant_FEATURE_GROUPS_DOCK:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_GROUPS_DOCK** = ``10``

Dock Groups. Nếu tính năng này bị vô hiệu hóa, groups sẽ không hiển thị hoặc không thể chỉnh sửa từ editor.

.. _class_EditorFeatureProfile_constant_FEATURE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Feature<enum_EditorFeatureProfile_Feature>` **FEATURE_MAX** = ``11``

Biểu thị kích thước của enum :ref:`Feature<enum_EditorFeatureProfile_Feature>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_EditorFeatureProfile_method_get_feature_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_feature_name**\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_get_feature_name>`

Trả về tên dễ đọc của ``feature`` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_is_class_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_class_disabled**\ (\ class_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorFeatureProfile_method_is_class_disabled>`

Trả về ``true`` nếu class được chỉ định bởi ``class_name`` bị vô hiệu hóa. Khi bị vô hiệu hóa, class sẽ không xuất hiện trong hộp thoại Create New Node.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_is_class_editor_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_class_editor_disabled**\ (\ class_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorFeatureProfile_method_is_class_editor_disabled>`

Trả về ``true`` nếu việc chỉnh sửa class được chỉ định bởi ``class_name`` bị vô hiệu hóa. Khi bị vô hiệu hóa, class vẫn xuất hiện trong hộp thoại Create New Node, nhưng Inspector sẽ ở chế độ chỉ đọc khi chọn một node kế thừa class đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_is_class_property_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_class_property_disabled**\ (\ class_name\: :ref:`StringName<class_StringName>`, property\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorFeatureProfile_method_is_class_property_disabled>`

Trả về ``true`` nếu ``property`` bị vô hiệu hóa trong class được chỉ định bởi ``class_name``. Khi một property bị vô hiệu hóa, property đó sẽ không xuất hiện trong Inspector khi chọn một node kế thừa class được chỉ định bởi ``class_name``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_is_feature_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_feature_disabled**\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`\ ) |const| :ref:`🔗<class_EditorFeatureProfile_method_is_feature_disabled>`

Trả về ``true`` nếu ``feature`` bị vô hiệu hóa. Khi một feature bị vô hiệu hóa, feature đó sẽ biến mất hoàn toàn khỏi editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_load_from_file:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load_from_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_load_from_file>`

Tải editor feature profile từ một tệp. Tệp phải tuân theo định dạng JSON thu được bằng cách sử dụng nút **Export** của feature profile manager hoặc phương thức :ref:`save_to_file()<class_EditorFeatureProfile_method_save_to_file>`.

\ **Lưu ý:** Feature profile được tạo thông qua giao diện người dùng sẽ được tải từ thư mục ``feature_profiles``, dưới dạng một tệp có phần mở rộng ``.profile``. Có thể tìm thấy thư mục cấu hình editor bằng cách sử dụng :ref:`EditorPaths.get_config_dir()<class_EditorPaths_method_get_config_dir>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_save_to_file:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save_to_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_save_to_file>`

Lưu editor feature profile vào một tệp ở định dạng JSON. Sau đó, profile có thể được import bằng nút **Import** của feature profile manager hoặc phương thức :ref:`load_from_file()<class_EditorFeatureProfile_method_load_from_file>`.

\ **Lưu ý:** Feature profile được tạo thông qua giao diện người dùng sẽ được lưu trong thư mục ``feature_profiles``, dưới dạng một tệp có phần mở rộng ``.profile``. Có thể tìm thấy thư mục cấu hình editor bằng cách sử dụng :ref:`EditorPaths.get_config_dir()<class_EditorPaths_method_get_config_dir>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_set_disable_class:

.. rst-class:: classref-method

|void| **set_disable_class**\ (\ class_name\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_set_disable_class>`

Nếu ``disable`` là ``true``, class được chỉ định bởi ``class_name`` sẽ bị vô hiệu hóa. Khi bị vô hiệu hóa, class sẽ không xuất hiện trong hộp thoại Create New Node.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_set_disable_class_editor:

.. rst-class:: classref-method

|void| **set_disable_class_editor**\ (\ class_name\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_set_disable_class_editor>`

Nếu ``disable`` là ``true``, việc chỉnh sửa class được chỉ định bởi ``class_name`` sẽ bị vô hiệu hóa. Khi bị vô hiệu hóa, class vẫn xuất hiện trong hộp thoại Create New Node, nhưng Inspector sẽ ở chế độ chỉ đọc khi chọn một node kế thừa class đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_set_disable_class_property:

.. rst-class:: classref-method

|void| **set_disable_class_property**\ (\ class_name\: :ref:`StringName<class_StringName>`, property\: :ref:`StringName<class_StringName>`, disable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_set_disable_class_property>`

Nếu ``disable`` là ``true``, việc chỉnh sửa ``property`` trong class được chỉ định bởi ``class_name`` sẽ bị vô hiệu hóa. Khi một property bị vô hiệu hóa, property đó sẽ không xuất hiện trong Inspector khi chọn một node kế thừa class được chỉ định bởi ``class_name``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFeatureProfile_method_set_disable_feature:

.. rst-class:: classref-method

|void| **set_disable_feature**\ (\ feature\: :ref:`Feature<enum_EditorFeatureProfile_Feature>`, disable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorFeatureProfile_method_set_disable_feature>`

Nếu ``disable`` là ``true``, feature của editor được chỉ định bởi ``feature`` sẽ bị vô hiệu hóa. Khi một feature bị vô hiệu hóa, feature đó sẽ biến mất hoàn toàn khỏi editor.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
