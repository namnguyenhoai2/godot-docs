:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorScenePostImportPlugin.xml.

.. _class_EditorScenePostImportPlugin:

EditorScenePostImportPlugin
===========================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Plugin dùng để kiểm soát và sửa đổi quá trình import một scene.

.. rst-class:: classref-introduction-group

Mô tả
-----

Loại plugin này tồn tại để sửa đổi quá trình import các scene, cho phép thay đổi nội dung cũng như thêm các tùy chọn importer ở mọi giai đoạn của quá trình.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`_get_import_options<class_EditorScenePostImportPlugin_private_method__get_import_options>`\ (\ path\: :ref:`String<class_String>`\ ) |virtual|                                                                                                                                                                                                                                                                 |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`_get_internal_import_options<class_EditorScenePostImportPlugin_private_method__get_internal_import_options>`\ (\ category\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                                                                                                                                                 |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`_get_internal_option_update_view_required<class_EditorScenePostImportPlugin_private_method__get_internal_option_update_view_required>`\ (\ category\: :ref:`int<class_int>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                                                                         |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`_get_internal_option_visibility<class_EditorScenePostImportPlugin_private_method__get_internal_option_visibility>`\ (\ category\: :ref:`int<class_int>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                                                    |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`_get_option_visibility<class_EditorScenePostImportPlugin_private_method__get_option_visibility>`\ (\ path\: :ref:`String<class_String>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                                                                    |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`_internal_process<class_EditorScenePostImportPlugin_private_method__internal_process>`\ (\ category\: :ref:`int<class_int>`, base_node\: :ref:`Node<class_Node>`, node\: :ref:`Node<class_Node>`, resource\: :ref:`Resource<class_Resource>`\ ) |virtual|                                                                                                                                                      |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`_post_process<class_EditorScenePostImportPlugin_private_method__post_process>`\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                                                                                                |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`_pre_process<class_EditorScenePostImportPlugin_private_method__pre_process>`\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                                                                                                  |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`add_import_option<class_EditorScenePostImportPlugin_method_add_import_option>`\ (\ name\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                                                                                                                                                                |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`add_import_option_advanced<class_EditorScenePostImportPlugin_method_add_import_option_advanced>`\ (\ type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, default_value\: :ref:`Variant<class_Variant>`, hint\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>` = 0, hint_string\: :ref:`String<class_String>` = "", usage_flags\: :ref:`int<class_int>` = 6\ ) |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`get_option_value<class_EditorScenePostImportPlugin_method_get_option_value>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                                                                                                                         |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_EditorScenePostImportPlugin_InternalImportCategory:

.. rst-class:: classref-enumeration

enum **InternalImportCategory**: :ref:`🔗<enum_EditorScenePostImportPlugin_InternalImportCategory>`

.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_NODE:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_NODE** = ``0``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_MESH_3D_NODE:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_MESH_3D_NODE** = ``1``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_MESH:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_MESH** = ``2``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_MATERIAL:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_MATERIAL** = ``3``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_ANIMATION:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_ANIMATION** = ``4``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_ANIMATION_NODE:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_ANIMATION_NODE** = ``5``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_SKELETON_3D_NODE:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_SKELETON_3D_NODE** = ``6``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorScenePostImportPlugin_constant_INTERNAL_IMPORT_CATEGORY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`InternalImportCategory<enum_EditorScenePostImportPlugin_InternalImportCategory>` **INTERNAL_IMPORT_CATEGORY_MAX** = ``7``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_EditorScenePostImportPlugin_private_method__get_import_options:

.. rst-class:: classref-method

|void| **_get_import_options**\ (\ path\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__get_import_options>`

Ghi đè để thêm các tùy chọn import chung. Các tùy chọn này sẽ xuất hiện trong import dock chính của editor. Thêm các tùy chọn thông qua :ref:`add_import_option()<class_EditorScenePostImportPlugin_method_add_import_option>` và :ref:`add_import_option_advanced()<class_EditorScenePostImportPlugin_method_add_import_option_advanced>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__get_internal_import_options:

.. rst-class:: classref-method

|void| **_get_internal_import_options**\ (\ category\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__get_internal_import_options>`

Ghi đè để thêm các tùy chọn import nội bộ. Các tùy chọn này sẽ xuất hiện trong hộp thoại import scene 3D. Thêm các tùy chọn thông qua :ref:`add_import_option()<class_EditorScenePostImportPlugin_method_add_import_option>` và :ref:`add_import_option_advanced()<class_EditorScenePostImportPlugin_method_add_import_option_advanced>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__get_internal_option_update_view_required:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_internal_option_update_view_required**\ (\ category\: :ref:`int<class_int>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__get_internal_option_update_view_required>`

Nên trả về ``true`` nếu chế độ xem 3D của hộp thoại import cần cập nhật khi thay đổi tùy chọn đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__get_internal_option_visibility:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_internal_option_visibility**\ (\ category\: :ref:`int<class_int>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__get_internal_option_visibility>`

Nên trả về ``true`` để hiển thị tùy chọn đã cho, ``false`` để ẩn tùy chọn đã cho hoặc ``null`` để bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__get_option_visibility:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_option_visibility**\ (\ path\: :ref:`String<class_String>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__get_option_visibility>`

Nên trả về ``true`` để hiển thị tùy chọn đã cho, ``false`` để ẩn tùy chọn đã cho hoặc ``null`` để bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__internal_process:

.. rst-class:: classref-method

|void| **_internal_process**\ (\ category\: :ref:`int<class_int>`, base_node\: :ref:`Node<class_Node>`, node\: :ref:`Node<class_Node>`, resource\: :ref:`Resource<class_Resource>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__internal_process>`

Xử lý một node hoặc resource cụ thể cho một category đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__post_process:

.. rst-class:: classref-method

|void| **_post_process**\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__post_process>`

Hậu xử lý scene. Hàm này được gọi sau khi scene cuối cùng đã được cấu hình.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_private_method__pre_process:

.. rst-class:: classref-method

|void| **_pre_process**\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImportPlugin_private_method__pre_process>`

Tiền xử lý scene. Hàm này được gọi ngay sau khi scene format loader tải scene và chưa có thay đổi nào được thực hiện.

Pre-process có thể được dùng để điều chỉnh các tùy chọn import nội bộ trong các key ``"nodes"``, ``"meshes"``, ``"animations"`` hoặc ``"materials"`` bên trong ``get_option_value("_subresources")``.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_method_add_import_option:

.. rst-class:: classref-method

|void| **add_import_option**\ (\ name\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_EditorScenePostImportPlugin_method_add_import_option>`

Thêm một tùy chọn import cụ thể (chỉ tên và giá trị mặc định). Hàm này chỉ có thể được gọi từ :ref:`_get_import_options()<class_EditorScenePostImportPlugin_private_method__get_import_options>` và :ref:`_get_internal_import_options()<class_EditorScenePostImportPlugin_private_method__get_internal_import_options>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_method_add_import_option_advanced:

.. rst-class:: classref-method

|void| **add_import_option_advanced**\ (\ type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, default_value\: :ref:`Variant<class_Variant>`, hint\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>` = 0, hint_string\: :ref:`String<class_String>` = "", usage_flags\: :ref:`int<class_int>` = 6\ ) :ref:`🔗<class_EditorScenePostImportPlugin_method_add_import_option_advanced>`

Thêm một tùy chọn import cụ thể. Hàm này chỉ có thể được gọi từ :ref:`_get_import_options()<class_EditorScenePostImportPlugin_private_method__get_import_options>` và :ref:`_get_internal_import_options()<class_EditorScenePostImportPlugin_private_method__get_internal_import_options>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImportPlugin_method_get_option_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_option_value**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorScenePostImportPlugin_method_get_option_value>`

Truy vấn giá trị của một tùy chọn. Hàm này chỉ có thể được gọi từ các hàm truy vấn khả năng hiển thị hoặc xử lý.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
