:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFDocument.xml.

.. _class_GLTFDocument:

GLTFDocument
============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`FBXDocument<class_FBXDocument>`

Class dùng để import và export các tệp glTF vào và ra khỏi Godot.

.. rst-class:: classref-introduction-group

Mô tả
-----

GLTFDocument hỗ trợ đọc dữ liệu từ tệp glTF, buffer hoặc scene Godot. Sau đó, dữ liệu này có thể được ghi vào filesystem, buffer hoặc dùng để tạo scene Godot.

Tất cả dữ liệu trong một scene glTF được lưu trữ trong class :ref:`GLTFState<class_GLTFState>`. GLTFDocument xử lý các state object nhưng bản thân không chứa dữ liệu scene. GLTFDocument có các biến thành viên để lưu trữ các thiết lập cấu hình export, chẳng hạn như định dạng hình ảnh, nhưng nhìn chung là stateless. Có thể xử lý nhiều scene với cùng các thiết lập bằng cùng một object GLTFDocument và các object :ref:`GLTFState<class_GLTFState>` khác nhau.

GLTFDocument có thể được mở rộng với chức năng tùy ý bằng cách mở rộng class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` và đăng ký class đó với GLTFDocument thông qua :ref:`register_gltf_document_extension()<class_GLTFDocument_method_register_gltf_document_extension>`. Điều này cho phép import và export dữ liệu tùy chỉnh.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tải và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `glTF 'What the duck?' guide <https://www.khronos.org/files/gltf20-reference-guide.pdf>`__

- `Khronos glTF specification <https://registry.khronos.org/glTF/>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`String<class_String>`                             | :ref:`fallback_image_format<class_GLTFDocument_property_fallback_image_format>`   | ``"None"`` |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                               | :ref:`fallback_image_quality<class_GLTFDocument_property_fallback_image_quality>` | ``0.25``   |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`String<class_String>`                             | :ref:`image_format<class_GLTFDocument_property_image_format>`                     | ``"PNG"``  |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                               | :ref:`lossy_quality<class_GLTFDocument_property_lossy_quality>`                   | ``0.75``   |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>`     | :ref:`root_node_mode<class_GLTFDocument_property_root_node_mode>`                 | ``0``      |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>` | :ref:`texture_map_mode<class_GLTFDocument_property_texture_map_mode>`             | ``1``      |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+
   | :ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` | :ref:`visibility_mode<class_GLTFDocument_property_visibility_mode>`               | ``0``      |
   +---------------------------------------------------------+-----------------------------------------------------------------------------------+------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                         | :ref:`append_from_buffer<class_GLTFDocument_method_append_from_buffer>`\ (\ bytes\: :ref:`PackedByteArray<class_PackedByteArray>`, base_path\: :ref:`String<class_String>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0\ )                       |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                         | :ref:`append_from_file<class_GLTFDocument_method_append_from_file>`\ (\ path\: :ref:`String<class_String>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0, base_path\: :ref:`String<class_String>` = ""\ )                                         |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                         | :ref:`append_from_scene<class_GLTFDocument_method_append_from_scene>`\ (\ node\: :ref:`Node<class_Node>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0\ )                                                                                         |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` | :ref:`export_object_model_property<class_GLTFDocument_method_export_object_model_property>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, node_path\: :ref:`NodePath<class_NodePath>`, godot_node\: :ref:`Node<class_Node>`, gltf_node_index\: :ref:`int<class_int>`\ ) |static| |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`                 | :ref:`generate_buffer<class_GLTFDocument_method_generate_buffer>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ )                                                                                                                                                                |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                       | :ref:`generate_scene<class_GLTFDocument_method_generate_scene>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, bake_fps\: :ref:`float<class_float>` = 30, trimming\: :ref:`bool<class_bool>` = false, remove_immutable_tracks\: :ref:`bool<class_bool>` = true\ )                 |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`             | :ref:`get_supported_gltf_extensions<class_GLTFDocument_method_get_supported_gltf_extensions>`\ (\ ) |static|                                                                                                                                                                      |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` | :ref:`import_object_model_property<class_GLTFDocument_method_import_object_model_property>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, json_pointer\: :ref:`String<class_String>`\ ) |static|                                                                                 |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`register_gltf_document_extension<class_GLTFDocument_method_register_gltf_document_extension>`\ (\ extension\: :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, first_priority\: :ref:`bool<class_bool>` = false\ ) |static|                                       |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                        | :ref:`unregister_gltf_document_extension<class_GLTFDocument_method_unregister_gltf_document_extension>`\ (\ extension\: :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`\ ) |static|                                                                                     |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                         | :ref:`write_to_filesystem<class_GLTFDocument_method_write_to_filesystem>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, path\: :ref:`String<class_String>`\ )                                                                                                                    |
   +---------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_GLTFDocument_RootNodeMode:

.. rst-class:: classref-enumeration

enum **RootNodeMode**: :ref:`🔗<enum_GLTFDocument_RootNodeMode>`

.. _class_GLTFDocument_constant_ROOT_NODE_MODE_SINGLE_ROOT:

.. rst-class:: classref-enumeration-constant

:ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>` **ROOT_NODE_MODE_SINGLE_ROOT** = ``0``

Coi node gốc của scene Godot là node gốc của tệp glTF và đánh dấu node đó là node gốc duy nhất thông qua extension glTF ``GODOT_single_root``. Node này sẽ được phân tích giống như :ref:`ROOT_NODE_MODE_KEEP_ROOT<class_GLTFDocument_constant_ROOT_NODE_MODE_KEEP_ROOT>` nếu implementation không hỗ trợ ``GODOT_single_root``.

.. _class_GLTFDocument_constant_ROOT_NODE_MODE_KEEP_ROOT:

.. rst-class:: classref-enumeration-constant

:ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>` **ROOT_NODE_MODE_KEEP_ROOT** = ``1``

Coi node gốc của scene Godot là node gốc của tệp glTF, nhưng không đánh dấu node đó là thành phần đặc biệt nào. Một node gốc bổ sung sẽ được tạo khi import vào Godot. Cách này chỉ sử dụng các tính năng glTF vanilla. Tương đương với hành vi trong Godot 4.1 trở về trước.

.. _class_GLTFDocument_constant_ROOT_NODE_MODE_MULTI_ROOT:

.. rst-class:: classref-enumeration-constant

:ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>` **ROOT_NODE_MODE_MULTI_ROOT** = ``2``

Coi node gốc của scene Godot là tên của scene glTF và thêm tất cả node con của nó làm các node gốc của tệp glTF. Cách này chỉ sử dụng các tính năng glTF vanilla. Điều này tránh tạo node gốc bổ sung, nhưng chỉ bảo toàn tên của node gốc scene Godot, vì node đó sẽ không được lưu dưới dạng node.

.. rst-class:: classref-item-separator

----

.. _enum_GLTFDocument_TextureMapMode:

.. rst-class:: classref-enumeration

enum **TextureMapMode**: :ref:`🔗<enum_GLTFDocument_TextureMapMode>`

.. _class_GLTFDocument_constant_TEXTURE_MAP_MODE_DO_NOT_REMAP:

.. rst-class:: classref-enumeration-constant

:ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>` **TEXTURE_MAP_MODE_DO_NOT_REMAP** = ``0``

Import các texture map trong tệp glTF nguyên trạng, không cố gắng đưa chúng vào các texture slot cụ thể phù hợp với material tích hợp sẵn của Godot. Điều này có thể phù hợp khi sử dụng tệp glTF với custom shader, nhưng có thể không hiển thị chính xác với material tích hợp sẵn của Godot. Tương đương với hành vi trong Godot 4.6 trở về trước.

.. _class_GLTFDocument_constant_TEXTURE_MAP_MODE_REMAP_TO_STANDARD_MATERIAL:

.. rst-class:: classref-enumeration-constant

:ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>` **TEXTURE_MAP_MODE_REMAP_TO_STANDARD_MATERIAL** = ``1``

Import các texture map trong tệp glTF sau khi remap chúng vào các texture slot phù hợp nhất dựa trên class :ref:`StandardMaterial3D<class_StandardMaterial3D>` của Godot. Đây là hành vi mặc định.

.. rst-class:: classref-item-separator

----

.. _enum_GLTFDocument_VisibilityMode:

.. rst-class:: classref-enumeration

enum **VisibilityMode**: :ref:`🔗<enum_GLTFDocument_VisibilityMode>`

.. _class_GLTFDocument_constant_VISIBILITY_MODE_INCLUDE_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` **VISIBILITY_MODE_INCLUDE_REQUIRED** = ``0``

Nếu scene chứa bất kỳ node không hiển thị nào, hãy đưa chúng vào, đánh dấu chúng là không hiển thị bằng ``KHR_node_visibility`` và yêu cầu các importer tôn trọng trạng thái không hiển thị của chúng. Nhược điểm: Nếu importer không hỗ trợ ``KHR_node_visibility``, tệp không thể được import.

.. _class_GLTFDocument_constant_VISIBILITY_MODE_INCLUDE_OPTIONAL:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` **VISIBILITY_MODE_INCLUDE_OPTIONAL** = ``1``

Nếu scene chứa bất kỳ node không hiển thị nào, hãy đưa chúng vào, đánh dấu chúng là không hiển thị bằng ``KHR_node_visibility`` và không áp đặt yêu cầu nào lên các importer. Nhược điểm: Nếu importer không hỗ trợ ``KHR_node_visibility``, các object vô hình sẽ hiển thị.

.. _class_GLTFDocument_constant_VISIBILITY_MODE_EXCLUDE:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` **VISIBILITY_MODE_EXCLUDE** = ``2``

Nếu scene chứa bất kỳ node không hiển thị nào, không đưa chúng vào bản export. Đây là hành vi tương tự Godot 4.4 trở về trước. Nhược điểm: Các node vô hình sẽ không tồn tại trong tệp đã export.

.. rst-class:: classref-item-separator

----

.. _enum_GLTFDocument_ImportFlags:

.. rst-class:: classref-enumeration

flags **ImportFlags**: :ref:`🔗<enum_GLTFDocument_ImportFlags>`

.. _class_GLTFDocument_constant_IMPORT_FLAG_GENERATE_TANGENT_ARRAYS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_GLTFDocument_ImportFlags>` **IMPORT_FLAG_GENERATE_TANGENT_ARRAYS** = ``8``

Nếu ``true``, hãy tạo tangent cho vertex bằng `Mikktspace <http://www.mikktspace.com/>`__ nếu mesh đầu vào không có dữ liệu tangent. Khi có thể, nên để phần mềm 3D modeling tạo tangent khi export thay vì phụ thuộc vào tùy chọn này. Tangent là bắt buộc để hiển thị chính xác normal map và height map, cùng với mọi tính năng material/shader yêu cầu tangent.

Nếu bạn không cần các tính năng material yêu cầu tangent, việc tắt tùy chọn này có thể giảm kích thước tệp đầu ra và tăng tốc quá trình import nếu tệp 3D nguồn không chứa tangent.

.. _class_GLTFDocument_constant_IMPORT_FLAG_USE_NAMED_SKIN_BINDS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_GLTFDocument_ImportFlags>` **IMPORT_FLAG_USE_NAMED_SKIN_BINDS** = ``16``

Nếu được bật, hãy sử dụng :ref:`Skin<class_Skin>`\ s có tên cho animation. Node :ref:`MeshInstance3D<class_MeshInstance3D>` chứa 3 property liên quan ở đây: một :ref:`NodePath<class_NodePath>` skeleton trỏ đến node :ref:`Skeleton3D<class_Skeleton3D>` (thường là ``..``), một mesh và một skin:

- Node :ref:`Skeleton3D<class_Skeleton3D>` chứa danh sách bone cùng tên, pose và rest của chúng, một tên và bone cha.

- Mesh là toàn bộ dữ liệu vertex thô cần thiết để hiển thị một mesh. Về mesh, nó biết các vertex được weight-paint như thế nào và sử dụng một số đánh số nội bộ thường được import từ phần mềm 3D modeling.

- Skin chứa thông tin cần thiết để bind mesh này vào Skeleton3D. Với mỗi bone ID nội bộ do phần mềm 3D modeling chọn, nó chứa hai thành phần. Thứ nhất là một matrix được gọi là Bind Pose Matrix, Inverse Bind Matrix hoặc viết tắt là IBM. Thứ hai, :ref:`Skin<class_Skin>` chứa tên của từng bone (nếu flag này được bật) hoặc index của bone trong danh sách :ref:`Skeleton3D<class_Skeleton3D>` (nếu flag này bị tắt).

Kết hợp lại, thông tin này đủ để cho Godot biết cách sử dụng các bone pose trong node :ref:`Skeleton3D<class_Skeleton3D>` để render mesh từ từng :ref:`MeshInstance3D<class_MeshInstance3D>`. Lưu ý rằng mỗi :ref:`MeshInstance3D<class_MeshInstance3D>` có thể dùng chung các bind, như thường thấy trong các model được export từ Blender, hoặc mỗi :ref:`MeshInstance3D<class_MeshInstance3D>` có thể sử dụng một object :ref:`Skin<class_Skin>` riêng, như thường thấy trong các model được export từ những công cụ khác như Maya.

.. _class_GLTFDocument_constant_IMPORT_FLAG_DISCARD_MESHES_AND_MATERIALS:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_GLTFDocument_ImportFlags>` **IMPORT_FLAG_DISCARD_MESHES_AND_MATERIALS** = ``32``

Bỏ qua mesh và material khi import. Khi import một scene dưới dạng :ref:`AnimationLibrary<class_AnimationLibrary>`, flag này luôn được bật.

.. _class_GLTFDocument_constant_IMPORT_FLAG_FORCE_DISABLE_MESH_COMPRESSION:

.. rst-class:: classref-enumeration-constant

:ref:`ImportFlags<enum_GLTFDocument_ImportFlags>` **IMPORT_FLAG_FORCE_DISABLE_MESH_COMPRESSION** = ``64``

Nếu ``true``, sẽ không sử dụng mesh compression. Hãy cân nhắc bật tùy chọn này nếu bạn nhận thấy các artifact dạng khối trên normal hoặc UV của mesh, hoặc nếu bạn có các mesh lớn hơn vài nghìn mét theo mỗi chiều.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_GLTFDocument_property_fallback_image_format:

.. rst-class:: classref-property

:ref:`String<class_String>` **fallback_image_format** = ``"None"`` :ref:`🔗<class_GLTFDocument_property_fallback_image_format>`

.. rst-class:: classref-property-setget

- |void| **set_fallback_image_format**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_fallback_image_format**\ (\ )

Tên thân thiện với người dùng của định dạng hình ảnh fallback. Tùy chọn này được sử dụng khi export tệp glTF, bao gồm cả việc ghi vào tệp và ghi vào byte array.

Property này chỉ có thể là một trong các giá trị "None", "PNG" hoặc "JPEG" và chỉ được sử dụng khi :ref:`image_format<class_GLTFDocument_property_image_format>` không phải là một trong các giá trị "None", "PNG" hoặc "JPEG". Nếu muốn có nhiều định dạng hình ảnh extension, có thể thực hiện bằng class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` - property này chỉ bao quát trường hợp cung cấp hình ảnh fallback glTF cơ sở khi sử dụng định dạng hình ảnh tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_fallback_image_quality:

.. rst-class:: classref-property

:ref:`float<class_float>` **fallback_image_quality** = ``0.25`` :ref:`🔗<class_GLTFDocument_property_fallback_image_quality>`

.. rst-class:: classref-property-setget

- |void| **set_fallback_image_quality**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fallback_image_quality**\ (\ )

Chất lượng của hình ảnh fallback, nếu có. Với tệp PNG, tùy chọn này thu nhỏ hình ảnh theo cả hai chiều bằng hệ số này. Với tệp JPEG, đây là chất lượng lossy của hình ảnh. Nên sử dụng giá trị thấp, vì việc đưa nhiều hình ảnh chất lượng cao vào tệp glTF sẽ làm mất lợi ích về kích thước tệp khi sử dụng định dạng hình ảnh hiệu quả hơn.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_image_format:

.. rst-class:: classref-property

:ref:`String<class_String>` **image_format** = ``"PNG"`` :ref:`🔗<class_GLTFDocument_property_image_format>`

.. rst-class:: classref-property-setget

- |void| **set_image_format**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_image_format**\ (\ )

Tên thân thiện với người dùng của định dạng hình ảnh export. Tùy chọn này được sử dụng khi export tệp glTF, bao gồm cả việc ghi vào tệp và ghi vào byte array.

Theo mặc định, Godot cho phép các tùy chọn sau: "None", "PNG", "JPEG", "Lossless WebP" và "Lossy WebP". Có thể thêm hỗ trợ cho nhiều định dạng hình ảnh hơn trong các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`. Một class extension có thể cung cấp nhiều tùy chọn cho định dạng cụ thể cần sử dụng hoặc thậm chí một tùy chọn sử dụng đồng thời nhiều định dạng.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_lossy_quality:

.. rst-class:: classref-property

:ref:`float<class_float>` **lossy_quality** = ``0.75`` :ref:`🔗<class_GLTFDocument_property_lossy_quality>`

.. rst-class:: classref-property-setget

- |void| **set_lossy_quality**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lossy_quality**\ (\ )

Nếu :ref:`image_format<class_GLTFDocument_property_image_format>` là định dạng ảnh lossy, giá trị này xác định chất lượng lossy của ảnh. Trong khoảng từ ``0.0`` đến ``1.0``, trong đó ``0.0`` là chất lượng thấp nhất và ``1.0`` là chất lượng cao nhất. Chất lượng lossy ``1.0`` không giống với lossless.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_root_node_mode:

.. rst-class:: classref-property

:ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>` **root_node_mode** = ``0`` :ref:`🔗<class_GLTFDocument_property_root_node_mode>`

.. rst-class:: classref-property-setget

- |void| **set_root_node_mode**\ (\ value\: :ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>`\ ) - :ref:`RootNodeMode<enum_GLTFDocument_RootNodeMode>` **get_root_node_mode**\ (\ )

Cách xử lý node gốc trong quá trình export. Giá trị mặc định và được khuyến nghị là :ref:`ROOT_NODE_MODE_SINGLE_ROOT<class_GLTFDocument_constant_ROOT_NODE_MODE_SINGLE_ROOT>`.

\ **Lưu ý:** Bất kể tệp glTF được export như thế nào, khi import, kiểu và tên của node gốc có thể được ghi đè trong tab cài đặt import scene.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_texture_map_mode:

.. rst-class:: classref-property

:ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>` **texture_map_mode** = ``1`` :ref:`🔗<class_GLTFDocument_property_texture_map_mode>`

.. rst-class:: classref-property-setget

- |void| **set_texture_map_mode**\ (\ value\: :ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>`\ ) - :ref:`TextureMapMode<enum_GLTFDocument_TextureMapMode>` **get_texture_map_mode**\ (\ )

Cách xử lý texture map trong quá trình import. Giá trị mặc định và được khuyến nghị là :ref:`TEXTURE_MAP_MODE_REMAP_TO_STANDARD_MATERIAL<class_GLTFDocument_constant_TEXTURE_MAP_MODE_REMAP_TO_STANDARD_MATERIAL>`, tự động ánh xạ lại từ hệ thống texture map linh hoạt của glTF sang các texture map slot cụ thể hơn trong class :ref:`StandardMaterial3D<class_StandardMaterial3D>` của Godot. Ngoài ra, có thể sử dụng :ref:`TEXTURE_MAP_MODE_DO_NOT_REMAP<class_GLTFDocument_constant_TEXTURE_MAP_MODE_DO_NOT_REMAP>` để giữ lại các texture map ban đầu từ tệp glTF. Điều này có thể hữu ích khi sử dụng tệp glTF với custom shader, nhưng có thể không hiển thị chính xác với material tích hợp sẵn của Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_property_visibility_mode:

.. rst-class:: classref-property

:ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` **visibility_mode** = ``0`` :ref:`🔗<class_GLTFDocument_property_visibility_mode>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_mode**\ (\ value\: :ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>`\ ) - :ref:`VisibilityMode<enum_GLTFDocument_VisibilityMode>` **get_visibility_mode**\ (\ )

Cách xử lý khả năng hiển thị của node trong quá trình export. Cài đặt này không có tác dụng nếu tất cả node đều hiển thị. Giá trị mặc định và được khuyến nghị là :ref:`VISIBILITY_MODE_INCLUDE_REQUIRED<class_GLTFDocument_constant_VISIBILITY_MODE_INCLUDE_REQUIRED>`, sử dụng extension ``KHR_node_visibility``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_GLTFDocument_method_append_from_buffer:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **append_from_buffer**\ (\ bytes\: :ref:`PackedByteArray<class_PackedByteArray>`, base_path\: :ref:`String<class_String>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_GLTFDocument_method_append_from_buffer>`

Nhận một :ref:`PackedByteArray<class_PackedByteArray>` định nghĩa glTF và import dữ liệu vào object :ref:`GLTFState<class_GLTFState>` đã cho thông qua parameter ``state``.

\ **Lưu ý:** ``base_path`` cho :ref:`append_from_buffer()<class_GLTFDocument_method_append_from_buffer>` biết nơi tìm các dependency và có thể để trống.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_append_from_file:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **append_from_file**\ (\ path\: :ref:`String<class_String>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0, base_path\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_GLTFDocument_method_append_from_file>`

Nhận đường dẫn đến một tệp glTF và import dữ liệu tại đường dẫn tệp đó vào object :ref:`GLTFState<class_GLTFState>` đã cho thông qua parameter ``state``.

\ **Lưu ý:** ``base_path`` cho :ref:`append_from_file()<class_GLTFDocument_method_append_from_file>` biết nơi tìm các dependency và có thể để trống.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_append_from_scene:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **append_from_scene**\ (\ node\: :ref:`Node<class_Node>`, state\: :ref:`GLTFState<class_GLTFState>`, flags\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_GLTFDocument_method_append_from_scene>`

Nhận một node scene của Godot Engine, export node đó cùng các node con của nó vào object :ref:`GLTFState<class_GLTFState>` đã cho thông qua parameter ``state``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_export_object_model_property:

.. rst-class:: classref-method

:ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` **export_object_model_property**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, node_path\: :ref:`NodePath<class_NodePath>`, godot_node\: :ref:`Node<class_Node>`, gltf_node_index\: :ref:`int<class_int>`\ ) |static| :ref:`🔗<class_GLTFDocument_method_export_object_model_property>`

Xác định ánh xạ giữa ``node_path`` Godot đã cho và các con trỏ JSON Object Model glTF tương ứng trong tệp glTF được tạo. Chi tiết của ánh xạ này được trả về trong object :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>`. Có thể cung cấp thêm các ánh xạ thông qua callback method :ref:`GLTFDocumentExtension._import_object_model_property()<class_GLTFDocumentExtension_private_method__import_object_model_property>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_generate_buffer:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **generate_buffer**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) :ref:`🔗<class_GLTFDocument_method_generate_buffer>`

Nhận object :ref:`GLTFState<class_GLTFState>` thông qua parameter ``state`` và trả về một :ref:`PackedByteArray<class_PackedByteArray>` glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_generate_scene:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **generate_scene**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, bake_fps\: :ref:`float<class_float>` = 30, trimming\: :ref:`bool<class_bool>` = false, remove_immutable_tracks\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_GLTFDocument_method_generate_scene>`

Nhận object :ref:`GLTFState<class_GLTFState>` thông qua parameter ``state`` và trả về một node scene của Godot Engine.

Parameter ``bake_fps`` ghi đè bake_fps trong ``state``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_get_supported_gltf_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_supported_gltf_extensions**\ (\ ) |static| :ref:`🔗<class_GLTFDocument_method_get_supported_gltf_extensions>`

Trả về danh sách tất cả extension glTF được hỗ trợ, bao gồm các extension được engine hỗ trợ trực tiếp và các extension được hỗ trợ bởi user plugin đăng ký các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`.

\ **Lưu ý:** Nếu method này được chạy trước khi một GLTFDocumentExtension được đăng ký, các extension của nó sẽ không được đưa vào danh sách. Hãy chỉ chạy method này sau khi tất cả extension đã được đăng ký. Nếu chạy method này khi engine khởi động, hãy cân nhắc chờ một frame trước khi gọi method để đảm bảo tất cả extension đã được đăng ký.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_import_object_model_property:

.. rst-class:: classref-method

:ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` **import_object_model_property**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, json_pointer\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_GLTFDocument_method_import_object_model_property>`

Xác định ánh xạ giữa ``json_pointer`` Object Model glTF đã cho và các node path Godot tương ứng trong scene Godot được tạo. Chi tiết của ánh xạ này được trả về trong object :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>`. Có thể cung cấp thêm các ánh xạ thông qua callback method :ref:`GLTFDocumentExtension._export_object_model_property()<class_GLTFDocumentExtension_private_method__export_object_model_property>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_register_gltf_document_extension:

.. rst-class:: classref-method

|void| **register_gltf_document_extension**\ (\ extension\: :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, first_priority\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_GLTFDocument_method_register_gltf_document_extension>`

Đăng ký instance :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` đã cho với GLTFDocument. Nếu ``first_priority`` là ``true``, extension này sẽ được chạy đầu tiên. Nếu không, nó sẽ được chạy cuối cùng.

\ **Lưu ý:** Giống như bản thân GLTFDocument, tất cả class GLTFDocumentExtension phải stateless để hoạt động chính xác. Nếu cần lưu trữ dữ liệu, hãy sử dụng các method ``set_additional_data`` và ``get_additional_data`` trong :ref:`GLTFState<class_GLTFState>` hoặc :ref:`GLTFNode<class_GLTFNode>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_unregister_gltf_document_extension:

.. rst-class:: classref-method

|void| **unregister_gltf_document_extension**\ (\ extension\: :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`\ ) |static| :ref:`🔗<class_GLTFDocument_method_unregister_gltf_document_extension>`

Hủy đăng ký instance :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocument_method_write_to_filesystem:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **write_to_filesystem**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GLTFDocument_method_write_to_filesystem>`

Nhận object :ref:`GLTFState<class_GLTFState>` thông qua parameter ``state`` và ghi một tệp glTF vào filesystem.

\ **Lưu ý:** Phần mở rộng của tệp glTF xác định đó là tệp nhị phân .glb hay tệp văn bản .gltf.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
