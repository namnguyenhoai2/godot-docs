:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorSceneFormatImporter.xml.

.. _class_EditorSceneFormatImporter:

EditorSceneFormatImporter
=========================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`EditorSceneFormatImporterBlend<class_EditorSceneFormatImporterBlend>`, :ref:`EditorSceneFormatImporterFBX2GLTF<class_EditorSceneFormatImporterFBX2GLTF>`, :ref:`EditorSceneFormatImporterGLTF<class_EditorSceneFormatImporterGLTF>`, :ref:`EditorSceneFormatImporterUFBX<class_EditorSceneFormatImporterUFBX>`

Nhập các scene từ tệp 3D của bên thứ ba.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorSceneFormatImporter** cho phép định nghĩa một importer script cho định dạng 3D của bên thứ ba.

Để sử dụng **EditorSceneFormatImporter**, trước tiên hãy đăng ký nó bằng phương thức :ref:`EditorPlugin.add_scene_format_importer_plugin()<class_EditorPlugin_method_add_scene_format_importer_plugin>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`_get_extensions<class_EditorSceneFormatImporter_private_method__get_extensions>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                                                          |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`_get_import_options<class_EditorSceneFormatImporter_private_method__get_import_options>`\ (\ path\: :ref:`String<class_String>`\ ) |virtual|                                                                                                                                                                                                                                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                     | :ref:`_get_option_visibility<class_EditorSceneFormatImporter_private_method__get_option_visibility>`\ (\ path\: :ref:`String<class_String>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                                                                    |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`                       | :ref:`_import_scene<class_EditorSceneFormatImporter_private_method__import_scene>`\ (\ path\: :ref:`String<class_String>`, flags\: :ref:`int<class_int>`, options\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| |required|                                                                                                                                                                                    |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_import_option<class_EditorSceneFormatImporter_method_add_import_option>`\ (\ name\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                                                                                                                                                                |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_import_option_advanced<class_EditorSceneFormatImporter_method_add_import_option_advanced>`\ (\ type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, default_value\: :ref:`Variant<class_Variant>`, hint\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>` = 0, hint_string\: :ref:`String<class_String>` = "", usage_flags\: :ref:`int<class_int>` = 6\ ) |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_EditorSceneFormatImporter_ImportFlags:

.. rst-class:: classref-enumeration

flags **ImportFlags**: :ref:`🔗<enum_EditorSceneFormatImporter_ImportFlags>`

.. _class_EditorSceneFormatImporter_constant_IMPORT_SCENE:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_SCENE** = ``1``

Flag không được sử dụng (không có tác dụng khi được bật).

.. _class_EditorSceneFormatImporter_constant_IMPORT_ANIMATION:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_ANIMATION** = ``2``

Nhập các animation từ scene 3D. Khi nhập một scene dưới dạng :ref:`AnimationLibrary<class_AnimationLibrary>`, flag này luôn được bật.

.. _class_EditorSceneFormatImporter_constant_IMPORT_FAIL_ON_MISSING_DEPENDENCIES:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_FAIL_ON_MISSING_DEPENDENCIES** = ``4``

Flag không được sử dụng (không có tác dụng khi được bật).

.. _class_EditorSceneFormatImporter_constant_IMPORT_GENERATE_TANGENT_ARRAYS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_GENERATE_TANGENT_ARRAYS** = ``8``

Nếu ``true``, tạo tangent cho vertex bằng `Mikktspace <http://www.mikktspace.com/>`__ nếu các mesh đầu vào không có dữ liệu tangent. Khi có thể, bạn nên để phần mềm tạo mô hình 3D tạo tangent khi export thay vì dựa vào tùy chọn này. Tangent là bắt buộc để hiển thị chính xác normal map và height map, cùng với bất kỳ tính năng material/shader nào yêu cầu tangent.

Nếu bạn không cần các tính năng material yêu cầu tangent, việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình import nếu tệp 3D nguồn không chứa tangent.

.. _class_EditorSceneFormatImporter_constant_IMPORT_USE_NAMED_SKIN_BINDS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_USE_NAMED_SKIN_BINDS** = ``16``

Nếu được chọn, sử dụng :ref:`Skin<class_Skin>`\ s có tên cho animation. Node :ref:`MeshInstance3D<class_MeshInstance3D>` chứa 3 thuộc tính liên quan ở đây: một :ref:`NodePath<class_NodePath>` trỏ đến node :ref:`Skeleton3D<class_Skeleton3D>` (thường là ``..``), một mesh và một skin:

- Node :ref:`Skeleton3D<class_Skeleton3D>` chứa danh sách các bone cùng tên, pose và rest của chúng, một tên và bone cha.

- Mesh chứa toàn bộ dữ liệu vertex thô cần thiết để hiển thị một mesh. Xét riêng về mesh, nó biết các vertex được weight-paint như thế nào và sử dụng một số thứ tự nội bộ thường được import từ phần mềm tạo mô hình 3D.

- Skin chứa thông tin cần thiết để bind mesh này vào Skeleton3D. Với mỗi ID bone nội bộ do phần mềm tạo mô hình 3D chọn, nó chứa hai thành phần. Thứ nhất là một ma trận được gọi là Bind Pose Matrix, Inverse Bind Matrix hoặc viết tắt là IBM. Thứ hai, :ref:`Skin<class_Skin>` chứa tên của từng bone (nếu flag này được bật) hoặc index của bone trong danh sách :ref:`Skeleton3D<class_Skeleton3D>` (nếu flag này bị tắt).

Kết hợp lại, thông tin này đủ để cho Godot biết cách sử dụng các pose của bone trong node :ref:`Skeleton3D<class_Skeleton3D>` để render mesh từ từng :ref:`MeshInstance3D<class_MeshInstance3D>`. Lưu ý rằng mỗi :ref:`MeshInstance3D<class_MeshInstance3D>` có thể dùng chung các bind, như thường thấy trong các model được export từ Blender, hoặc mỗi :ref:`MeshInstance3D<class_MeshInstance3D>` có thể sử dụng một đối tượng :ref:`Skin<class_Skin>` riêng, như thường thấy trong các model được export từ các công cụ khác như Maya.

.. _class_EditorSceneFormatImporter_constant_IMPORT_DISCARD_MESHES_AND_MATERIALS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_DISCARD_MESHES_AND_MATERIALS** = ``32``

Bỏ qua mesh và material khi import. Khi nhập một scene dưới dạng :ref:`AnimationLibrary<class_AnimationLibrary>`, flag này luôn được bật.

.. _class_EditorSceneFormatImporter_constant_IMPORT_FORCE_DISABLE_MESH_COMPRESSION:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_EditorSceneFormatImporter_ImportFlags>` **IMPORT_FORCE_DISABLE_MESH_COMPRESSION** = ``64``

Nếu ``true``, tính năng nén mesh sẽ không được sử dụng. Hãy cân nhắc bật tùy chọn này nếu bạn nhận thấy hiện tượng lỗi dạng khối trong normal hoặc UV của mesh, hoặc nếu bạn có các mesh lớn hơn vài nghìn mét theo mỗi chiều.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_EditorSceneFormatImporter_private_method__get_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_extensions**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorSceneFormatImporter_private_method__get_extensions>`

Trả về các phần mở rộng tệp được scene importer này hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_EditorSceneFormatImporter_private_method__get_import_options:

.. rst-class:: classref-method

|void| **_get_import_options**\ (\ path\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorSceneFormatImporter_private_method__get_import_options>`

Ghi đè để thêm các tùy chọn import chung. Các tùy chọn này sẽ xuất hiện trong import dock chính của editor. Thêm tùy chọn bằng :ref:`add_import_option()<class_EditorSceneFormatImporter_method_add_import_option>` và :ref:`add_import_option_advanced()<class_EditorSceneFormatImporter_method_add_import_option_advanced>`.

\ **Lưu ý:** Tất cả các instance **EditorSceneFormatImporter** và :ref:`EditorScenePostImportPlugin<class_EditorScenePostImportPlugin>` sẽ thêm tùy chọn cho mọi tệp. Bạn nên kiểm tra phần mở rộng tệp khi ``path`` không rỗng.

Khi người dùng đang chỉnh sửa project settings, ``path`` sẽ rỗng. Bạn nên thêm tất cả tùy chọn khi ``path`` rỗng để cho phép người dùng tùy chỉnh Import Defaults.

.. rst-class:: classref-item-separator

----

.. _class_EditorSceneFormatImporter_private_method__get_option_visibility:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_option_visibility**\ (\ path\: :ref:`String<class_String>`, for_animation\: :ref:`bool<class_bool>`, option\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorSceneFormatImporter_private_method__get_option_visibility>`

Nên trả về ``true`` để hiển thị tùy chọn đã cho, ``false`` để ẩn tùy chọn đã cho hoặc ``null`` để bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_EditorSceneFormatImporter_private_method__import_scene:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **_import_scene**\ (\ path\: :ref:`String<class_String>`, flags\: :ref:`int<class_int>`, options\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| |required| :ref:`🔗<class_EditorSceneFormatImporter_private_method__import_scene>`

Thực hiện phần lớn logic import scene tại đây, chẳng hạn bằng cách sử dụng :ref:`GLTFDocument<class_GLTFDocument>` hoặc :ref:`FBXDocument<class_FBXDocument>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorSceneFormatImporter_method_add_import_option:

.. rst-class:: classref-method

|void| **add_import_option**\ (\ name\: :ref:`String<class_String>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_EditorSceneFormatImporter_method_add_import_option>`

Thêm một tùy chọn import cụ thể (chỉ gồm tên và giá trị mặc định). Hàm này chỉ có thể được gọi từ :ref:`_get_import_options()<class_EditorSceneFormatImporter_private_method__get_import_options>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorSceneFormatImporter_method_add_import_option_advanced:

.. rst-class:: classref-method

|void| **add_import_option_advanced**\ (\ type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, default_value\: :ref:`Variant<class_Variant>`, hint\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>` = 0, hint_string\: :ref:`String<class_String>` = "", usage_flags\: :ref:`int<class_int>` = 6\ ) :ref:`🔗<class_EditorSceneFormatImporter_method_add_import_option_advanced>`

Thêm một tùy chọn import cụ thể. Hàm này chỉ có thể được gọi từ :ref:`_get_import_options()<class_EditorSceneFormatImporter_private_method__get_import_options>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
