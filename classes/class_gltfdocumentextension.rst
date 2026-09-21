:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFDocumentExtension.xml.

.. _class_GLTFDocumentExtension:

GLTFDocumentExtension
=====================

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GLTFDocumentExtensionConvertImporterMesh<class_GLTFDocumentExtensionConvertImporterMesh>`

Lớp mở rộng :ref:`GLTFDocument<class_GLTFDocument>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Mở rộng chức năng của lớp :ref:`GLTFDocument<class_GLTFDocument>` bằng cách cho phép bạn chạy mã tùy ý ở nhiều giai đoạn khác nhau trong quá trình import hoặc export glTF.

Để sử dụng, hãy tạo một lớp mới kế thừa GLTFDocumentExtension, override mọi phương thức bạn cần, tạo một instance của lớp, rồi đăng ký lớp đó bằng :ref:`GLTFDocument.register_gltf_document_extension()<class_GLTFDocument_method_register_gltf_document_extension>`.

\ **Lưu ý:** Tất cả các lớp GLTFDocumentExtension đều được nhân bản khi bắt đầu quá trình import hoặc export. Ngoại trừ các giá trị cấu hình, các lớp này phải stateless để hoạt động đúng cách. Nếu cần lưu trữ dữ liệu, hãy sử dụng các phương thức ``set_additional_data`` và ``get_additional_data`` trong :ref:`GLTFState<class_GLTFState>` hoặc :ref:`GLTFNode<class_GLTFNode>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tải và lưu tệp trong runtime <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_convert_scene_node<class_GLTFDocumentExtension_private_method__convert_scene_node>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, scene_node\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                 |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_export_get_property_list<class_GLTFDocumentExtension_private_method__export_get_property_list>`\ (\ root_node\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_export_node<class_GLTFDocumentExtension_private_method__export_node>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, json\: :ref:`Dictionary<class_Dictionary>`, node\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>`    | :ref:`_export_object_model_property<class_GLTFDocumentExtension_private_method__export_object_model_property>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, node_path\: :ref:`NodePath<class_NodePath>`, godot_node\: :ref:`Node<class_Node>`, gltf_node_index\: :ref:`int<class_int>`, target_object\: :ref:`Object<class_Object>`, target_depth\: :ref:`int<class_int>`\ ) |virtual| |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_export_post<class_GLTFDocumentExtension_private_method__export_post>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual|                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_export_post_convert<class_GLTFDocumentExtension_private_method__export_post_convert>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_export_preflight<class_GLTFDocumentExtension_private_method__export_preflight>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_export_preserialize<class_GLTFDocumentExtension_private_method__export_preserialize>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual|                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node3D<class_Node3D>`                                      | :ref:`_generate_scene_node<class_GLTFDocumentExtension_private_method__generate_scene_node>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, scene_parent\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                             |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_image_file_extension<class_GLTFDocumentExtension_private_method__get_image_file_extension>`\ (\ ) |virtual|                                                                                                                                                                                                                                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_saveable_image_formats<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>`\ (\ ) |virtual|                                                                                                                                                                                                                                                               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_supported_extensions<class_GLTFDocumentExtension_private_method__get_supported_extensions>`\ (\ ) |virtual|                                                                                                                                                                                                                                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import_node<class_GLTFDocumentExtension_private_method__import_node>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, json\: :ref:`Dictionary<class_Dictionary>`, node\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>`    | :ref:`_import_object_model_property<class_GLTFDocumentExtension_private_method__import_object_model_property>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, split_json_pointer\: :ref:`PackedStringArray<class_PackedStringArray>`, partial_paths\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) |virtual|                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import_post<class_GLTFDocumentExtension_private_method__import_post>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual|                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import_post_parse<class_GLTFDocumentExtension_private_method__import_post_parse>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual|                                                                                                                                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import_pre_generate<class_GLTFDocumentExtension_private_method__import_pre_generate>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual|                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import_preflight<class_GLTFDocumentExtension_private_method__import_preflight>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, extensions\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual|                                                                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_parse_image_data<class_GLTFDocumentExtension_private_method__parse_image_data>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image_data\: :ref:`PackedByteArray<class_PackedByteArray>`, mime_type\: :ref:`String<class_String>`, ret_image\: :ref:`Image<class_Image>`\ ) |virtual|                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_parse_node_extensions<class_GLTFDocumentExtension_private_method__parse_node_extensions>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, extensions\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual|                                                                                                                               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_parse_texture_json<class_GLTFDocumentExtension_private_method__parse_texture_json>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, texture_json\: :ref:`Dictionary<class_Dictionary>`, ret_gltf_texture\: :ref:`GLTFTexture<class_GLTFTexture>`\ ) |virtual|                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_save_image_at_path<class_GLTFDocumentExtension_private_method__save_image_at_path>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image\: :ref:`Image<class_Image>`, file_path\: :ref:`String<class_String>`, image_format\: :ref:`String<class_String>`, lossy_quality\: :ref:`float<class_float>`\ ) |virtual|                                                                 |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`                    | :ref:`_serialize_image_to_bytes<class_GLTFDocumentExtension_private_method__serialize_image_to_bytes>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image\: :ref:`Image<class_Image>`, image_dict\: :ref:`Dictionary<class_Dictionary>`, image_format\: :ref:`String<class_String>`, lossy_quality\: :ref:`float<class_float>`\ ) |virtual|                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_serialize_texture_json<class_GLTFDocumentExtension_private_method__serialize_texture_json>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`, texture_json\: :ref:`Dictionary<class_Dictionary>`, gltf_texture\: :ref:`GLTFTexture<class_GLTFTexture>`, image_format\: :ref:`String<class_String>`\ ) |virtual|                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFDocumentExtension_private_method__convert_scene_node:

.. rst-class:: classref-method

|void| **_convert_scene_node**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, scene_node\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__convert_scene_node>`

Là một phần của quá trình export. Phương thức này được chạy sau :ref:`_export_preflight()<class_GLTFDocumentExtension_private_method__export_preflight>` và trước :ref:`_export_post_convert()<class_GLTFDocumentExtension_private_method__export_post_convert>`.

Được chạy khi chuyển đổi dữ liệu từ một node của scene Godot. Phương thức này có thể được dùng để xử lý dữ liệu node của scene Godot thành định dạng có thể được sử dụng bởi :ref:`_export_node()<class_GLTFDocumentExtension_private_method__export_node>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_get_property_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_export_get_property_list**\ (\ root_node\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_get_property_list>`

Được chạy trước quá trình export. Phương thức này được chạy trước :ref:`_export_preflight()<class_GLTFDocumentExtension_private_method__export_preflight>` khi export một scene từ editor, hoặc có thể hoàn toàn không được chạy trong các tình huống khác.

Không giống các phương thức export còn lại, phương thức này không chạy khi gọi tuần tự các phương thức export của một :ref:`GLTFDocument<class_GLTFDocument>` cùng với mọi thành phần khác, mà chạy trước khi toàn bộ quá trình đó diễn ra, cho phép thực hiện cấu hình trước, có thể sớm hơn hàng phút hoặc hàng giờ so với :ref:`_export_preflight()<class_GLTFDocumentExtension_private_method__export_preflight>`. Điều này cho phép các extension quyết định những thuộc tính nào sẽ hiển thị trong hộp thoại cài đặt export của editor dựa trên nội dung của scene, đồng thời ẩn các cài đặt không liên quan đến scene đó. Tham số ``root_node`` có thể là ``null``, trong trường hợp đó tất cả thuộc tính sẽ được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_node:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_export_node**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, json\: :ref:`Dictionary<class_Dictionary>`, node\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_node>`

Là một phần của quá trình export. Phương thức này được chạy sau :ref:`_get_saveable_image_formats()<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>` và trước :ref:`_export_post()<class_GLTFDocumentExtension_private_method__export_post>`. Nếu **GLTFDocumentExtension** này được dùng để export hình ảnh, phương thức này chạy sau :ref:`_serialize_texture_json()<class_GLTFDocumentExtension_private_method__serialize_texture_json>`.

Phương thức này có thể được dùng để sửa đổi JSON cuối cùng của từng node. Dữ liệu trước tiên nên được lưu trong ``gltf_node`` trước khi serialize JSON, nhưng node Godot :ref:`Node<class_Node>` ban đầu cũng được cung cấp nếu có. ``node`` có thể là ``null`` nếu không có, chẳng hạn khi export dữ liệu glTF không được tạo từ một scene Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_object_model_property:

.. rst-class:: classref-method

:ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` **_export_object_model_property**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, node_path\: :ref:`NodePath<class_NodePath>`, godot_node\: :ref:`Node<class_Node>`, gltf_node_index\: :ref:`int<class_int>`, target_object\: :ref:`Object<class_Object>`, target_depth\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_object_model_property>`

Là một phần của quá trình export. Cho phép các lớp GLTFDocumentExtension cung cấp ánh xạ cho các thuộc tính của node trong scene tree Godot tới các JSON pointer trỏ đến các thuộc tính glTF, như được định nghĩa bởi glTF object model.

Trả về một instance :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` xác định cách thuộc tính cần được ánh xạ. Nếu extension của bạn không thể xử lý thuộc tính, hãy trả về ``null`` hoặc một instance không có JSON pointer nào (xem :ref:`GLTFObjectModelProperty.has_json_pointers()<class_GLTFObjectModelProperty_method_has_json_pointers>`). Bạn nên sử dụng :ref:`GLTFObjectModelProperty.set_types()<class_GLTFObjectModelProperty_method_set_types>` để thiết lập các type và thiết lập JSON pointer bằng thuộc tính :ref:`GLTFObjectModelProperty.json_pointers<class_GLTFObjectModelProperty_property_json_pointers>`.

Các tham số cung cấp ngữ cảnh cho thuộc tính, bao gồm NodePath, node Godot, chỉ mục node glTF và target object. ``target_object`` sẽ bằng ``godot_node`` nếu không tìm thấy sub-object, nếu không thì sẽ trỏ đến một sub-object. Ví dụ, nếu path là ``^"A/B/C/MeshInstance3D:mesh:surface_0/material:emission_intensity"``, nó sẽ lấy node, sau đó mesh, rồi material, vì vậy ``target_object`` sẽ là resource :ref:`Material<class_Material>`, và ``target_depth`` sẽ là 2 vì đã duyệt qua 2 cấp để đến target.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_post:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_export_post**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_post>`

Là một phần của quá trình export. Phương thức này được chạy sau cùng, sau tất cả các phần khác của quá trình export.

Phương thức này có thể được dùng để sửa đổi JSON cuối cùng của tệp glTF được tạo.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_post_convert:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_export_post_convert**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_post_convert>`

Là một phần của quá trình export. Phương thức này được chạy sau :ref:`_convert_scene_node()<class_GLTFDocumentExtension_private_method__convert_scene_node>` và trước :ref:`_export_preserialize()<class_GLTFDocumentExtension_private_method__export_preserialize>`.

Phương thức này có thể được dùng để sửa đổi các cấu trúc dữ liệu node đã chuyển đổi trước khi serialize cùng với mọi dữ liệu bổ sung từ scene tree.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_preflight:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_export_preflight**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_preflight>`

Là một phần của quá trình export. Phương thức này được chạy đầu tiên, trước tất cả các phần khác của quá trình export.

Giá trị trả về được dùng để xác định instance **GLTFDocumentExtension** này có được dùng để export một tệp glTF nhất định hay không. Nếu :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>`, quá trình export sẽ sử dụng instance **GLTFDocumentExtension** này. Nếu không override, :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__export_preserialize:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_export_preserialize**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__export_preserialize>`

Là một phần của quá trình export. Phương thức này được chạy sau :ref:`_export_post_convert()<class_GLTFDocumentExtension_private_method__export_post_convert>` và trước :ref:`_get_saveable_image_formats()<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>`.

Phương thức này có thể được dùng để thay đổi state trước khi thực hiện serialization. Phương thức chạy mỗi lần tạo buffer bằng :ref:`GLTFDocument.generate_buffer()<class_GLTFDocument_method_generate_buffer>` hoặc ghi vào file system bằng :ref:`GLTFDocument.write_to_filesystem()<class_GLTFDocument_method_write_to_filesystem>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__generate_scene_node:

.. rst-class:: classref-method

:ref:`Node3D<class_Node3D>` **_generate_scene_node**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, scene_parent\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__generate_scene_node>`

Là một phần của quá trình import. Phương thức này được chạy sau :ref:`_import_pre_generate()<class_GLTFDocumentExtension_private_method__import_pre_generate>` và trước :ref:`_import_node()<class_GLTFDocumentExtension_private_method__import_node>`.

Được chạy khi tạo một node scene Godot từ một GLTFNode. Node được trả về sẽ được thêm vào scene tree. Có thể tạo nhiều node trong bước này nếu chúng được thêm làm child của node được trả về.

\ **Lưu ý:** Tham số ``scene_parent`` có thể là ``null`` nếu đây là node root duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__get_image_file_extension:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_image_file_extension**\ (\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__get_image_file_extension>`

Trả về phần mở rộng tệp được dùng để lưu dữ liệu hình ảnh vào, chẳng hạn như ``".png"``. Nếu được định nghĩa, khi extension này được dùng để xử lý hình ảnh và hình ảnh được lưu vào một tệp riêng, các byte hình ảnh sẽ được sao chép vào một tệp có phần mở rộng này. Nếu được thiết lập, phải có một lớp :ref:`ResourceImporter<class_ResourceImporter>` có khả năng import tệp đó. Nếu không được định nghĩa hoặc để trống, Godot sẽ lưu hình ảnh vào tệp PNG.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__get_saveable_image_formats:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_saveable_image_formats**\ (\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>`

Là một phần của quá trình export. Phương thức này được chạy sau :ref:`_convert_scene_node()<class_GLTFDocumentExtension_private_method__convert_scene_node>` và trước :ref:`_export_node()<class_GLTFDocumentExtension_private_method__export_node>`.

Trả về một array gồm các định dạng hình ảnh có thể được lưu/export bởi extension này. Extension này chỉ được chọn làm image exporter nếu :ref:`GLTFDocument<class_GLTFDocument>` của :ref:`GLTFDocument.image_format<class_GLTFDocument_property_image_format>` nằm trong array này. Nếu **GLTFDocumentExtension** này được chọn làm image exporter, một trong các phương thức :ref:`_save_image_at_path()<class_GLTFDocumentExtension_private_method__save_image_at_path>` hoặc :ref:`_serialize_image_to_bytes()<class_GLTFDocumentExtension_private_method__serialize_image_to_bytes>` sẽ chạy tiếp theo; nếu không, :ref:`_export_node()<class_GLTFDocumentExtension_private_method__export_node>` sẽ chạy tiếp theo. Nếu tên định dạng chứa ``"Lossy"``, thanh trượt chất lượng lossy sẽ được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__get_supported_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_supported_extensions**\ (\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__get_supported_extensions>`

Là một phần của quá trình import. Phương thức này được chạy sau :ref:`_import_preflight()<class_GLTFDocumentExtension_private_method__import_preflight>` và trước :ref:`_parse_node_extensions()<class_GLTFDocumentExtension_private_method__parse_node_extensions>`.

Trả về một array gồm các extension glTF được lớp GLTFDocumentExtension này hỗ trợ. Thông tin này được dùng để xác thực xem có thể load một tệp glTF chứa các extension bắt buộc hay không.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_node:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import_node**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, json\: :ref:`Dictionary<class_Dictionary>`, node\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_node>`

Là một phần của quá trình import. Phương thức này được chạy sau :ref:`_generate_scene_node()<class_GLTFDocumentExtension_private_method__generate_scene_node>` và trước :ref:`_import_post()<class_GLTFDocumentExtension_private_method__import_post>`.

Phương thức này có thể được dùng để thực hiện sửa đổi đối với từng node scene Godot được tạo.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_object_model_property:

.. rst-class:: classref-method

:ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` **_import_object_model_property**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, split_json_pointer\: :ref:`PackedStringArray<class_PackedStringArray>`, partial_paths\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_object_model_property>`

Một phần của quy trình import. Cho phép các lớp GLTFDocumentExtension cung cấp ánh xạ từ các JSON pointer đến các thuộc tính glTF, như được định nghĩa bởi mô hình đối tượng glTF, sang các thuộc tính của các node trong scene tree của Godot.

Trả về một instance :ref:`GLTFObjectModelProperty<class_GLTFObjectModelProperty>` xác định cách thuộc tính cần được ánh xạ. Nếu extension của bạn không thể xử lý thuộc tính này, hãy trả về ``null`` hoặc một instance không có NodePath nào (xem :ref:`GLTFObjectModelProperty.has_node_paths()<class_GLTFObjectModelProperty_method_has_node_paths>`). Bạn nên sử dụng :ref:`GLTFObjectModelProperty.set_types()<class_GLTFObjectModelProperty_method_set_types>` để thiết lập các type, và hàm :ref:`GLTFObjectModelProperty.append_path_to_property()<class_GLTFObjectModelProperty_method_append_path_to_property>` hữu ích trong hầu hết các trường hợp đơn giản.

Trong nhiều trường hợp, ``partial_paths`` sẽ chứa phần đầu của một path, cho phép extension hoàn thiện path đó. Ví dụ, với ``/nodes/3/extensions/MY_ext/prop``, Godot sẽ truyền cho bạn một NodePath dẫn đến node 3, vì vậy lớp GLTFDocumentExtension chỉ cần phân giải phần ``MY_ext/prop`` cuối cùng của path. Trong ví dụ này, extension nên kiểm tra ``split.size() > 4 and split[0] == "nodes" and split[2] == "extensions" and split[3] == "MY_ext"`` ở đầu hàm để xác định JSON pointer này có áp dụng cho nó hay không, sau đó có thể sử dụng ``partial_paths`` và xử lý ``split[4]``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_post:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import_post**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, root\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_post>`

Một phần của quy trình import. Phương thức này được chạy sau cùng, sau tất cả các phần khác của quy trình import.

Có thể sử dụng phương thức này để sửa đổi Godot scene cuối cùng được tạo bởi quy trình import.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_post_parse:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import_post_parse**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_post_parse>`

Một phần của quy trình import. Phương thức này được chạy sau :ref:`_parse_node_extensions()<class_GLTFDocumentExtension_private_method__parse_node_extensions>` và trước :ref:`_import_pre_generate()<class_GLTFDocumentExtension_private_method__import_pre_generate>`.

Có thể sử dụng phương thức này để sửa đổi bất kỳ dữ liệu nào đã được import cho đến thời điểm hiện tại sau khi phân tích cú pháp từng node, nhưng trước khi tạo scene hoặc bất kỳ node nào của scene.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_pre_generate:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import_pre_generate**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_pre_generate>`

Một phần của quy trình import. Phương thức này được chạy sau :ref:`_import_post_parse()<class_GLTFDocumentExtension_private_method__import_post_parse>` và trước :ref:`_generate_scene_node()<class_GLTFDocumentExtension_private_method__generate_scene_node>`.

Có thể sử dụng phương thức này để sửa đổi hoặc đọc bất kỳ cấu trúc dữ liệu nào đã được xử lý, trước khi tạo các node rồi chạy bước import cuối cùng cho từng node.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__import_preflight:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import_preflight**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, extensions\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__import_preflight>`

Một phần của quy trình import. Phương thức này được chạy đầu tiên, trước tất cả các phần khác của quy trình import.

Giá trị trả về được dùng để xác định instance **GLTFDocumentExtension** này có nên được sử dụng để import một tệp glTF nhất định hay không. Nếu :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>`, quy trình import sẽ sử dụng instance **GLTFDocumentExtension** này. Nếu không được override, :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__parse_image_data:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_parse_image_data**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image_data\: :ref:`PackedByteArray<class_PackedByteArray>`, mime_type\: :ref:`String<class_String>`, ret_image\: :ref:`Image<class_Image>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__parse_image_data>`

Một phần của quy trình import. Phương thức này được chạy sau :ref:`_parse_node_extensions()<class_GLTFDocumentExtension_private_method__parse_node_extensions>` và trước :ref:`_parse_texture_json()<class_GLTFDocumentExtension_private_method__parse_texture_json>`.

Được chạy khi phân tích dữ liệu image từ một tệp glTF. Dữ liệu có thể bắt nguồn từ một tệp riêng, một URI hoặc một buffer, sau đó được truyền dưới dạng một byte array.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__parse_node_extensions:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_parse_node_extensions**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, extensions\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__parse_node_extensions>`

Một phần của quy trình import. Phương thức này được chạy sau :ref:`_get_supported_extensions()<class_GLTFDocumentExtension_private_method__get_supported_extensions>` và trước :ref:`_import_post_parse()<class_GLTFDocumentExtension_private_method__import_post_parse>`.

Được chạy khi phân tích các extension của một GLTFNode. Có thể sử dụng phương thức này để xử lý dữ liệu JSON của extension thành một định dạng có thể được :ref:`_generate_scene_node()<class_GLTFDocumentExtension_private_method__generate_scene_node>` sử dụng. Giá trị trả về phải là một member của enum :ref:`Error<enum_@GlobalScope_Error>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__parse_texture_json:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_parse_texture_json**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, texture_json\: :ref:`Dictionary<class_Dictionary>`, ret_gltf_texture\: :ref:`GLTFTexture<class_GLTFTexture>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__parse_texture_json>`

Một phần của quy trình import. Phương thức này được chạy sau :ref:`_parse_image_data()<class_GLTFDocumentExtension_private_method__parse_image_data>` và trước :ref:`_generate_scene_node()<class_GLTFDocumentExtension_private_method__generate_scene_node>`.

Được chạy khi phân tích JSON texture từ mảng textures của glTF. Có thể sử dụng phương thức này để thiết lập image source index sẽ được dùng làm texture.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__save_image_at_path:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_save_image_at_path**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image\: :ref:`Image<class_Image>`, file_path\: :ref:`String<class_String>`, image_format\: :ref:`String<class_String>`, lossy_quality\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__save_image_at_path>`

Một phần của quy trình export. Phương thức này được chạy sau :ref:`_get_saveable_image_formats()<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>` và trước :ref:`_serialize_texture_json()<class_GLTFDocumentExtension_private_method__serialize_texture_json>`.

Phương thức này được chạy khi lưu các image riêng khỏi tệp glTF. Khi image được nhúng, :ref:`_serialize_image_to_bytes()<class_GLTFDocumentExtension_private_method__serialize_image_to_bytes>` sẽ được chạy thay thế. Lưu ý rằng các phương thức này chỉ được chạy khi **GLTFDocumentExtension** này được chọn làm image exporter.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__serialize_image_to_bytes:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **_serialize_image_to_bytes**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, image\: :ref:`Image<class_Image>`, image_dict\: :ref:`Dictionary<class_Dictionary>`, image_format\: :ref:`String<class_String>`, lossy_quality\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__serialize_image_to_bytes>`

Một phần của quy trình export. Phương thức này được chạy sau :ref:`_get_saveable_image_formats()<class_GLTFDocumentExtension_private_method__get_saveable_image_formats>` và trước :ref:`_serialize_texture_json()<class_GLTFDocumentExtension_private_method__serialize_texture_json>`.

Phương thức này được chạy khi nhúng image vào tệp glTF. Khi image được lưu riêng, :ref:`_save_image_at_path()<class_GLTFDocumentExtension_private_method__save_image_at_path>` sẽ được chạy thay thế. Lưu ý rằng các phương thức này chỉ được chạy khi **GLTFDocumentExtension** này được chọn làm image exporter.

Phương thức này phải thiết lập MIME type của image trong ``image_dict`` bằng key ``"mimeType"``. Ví dụ, đối với image PNG, giá trị sẽ được thiết lập thành ``"image/png"``. Giá trị trả về phải là một :ref:`PackedByteArray<class_PackedByteArray>` chứa dữ liệu image.

.. rst-class:: classref-item-separator

----

.. _class_GLTFDocumentExtension_private_method__serialize_texture_json:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_serialize_texture_json**\ (\ state\: :ref:`GLTFState<class_GLTFState>`, texture_json\: :ref:`Dictionary<class_Dictionary>`, gltf_texture\: :ref:`GLTFTexture<class_GLTFTexture>`, image_format\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_GLTFDocumentExtension_private_method__serialize_texture_json>`

Một phần của quy trình export. Phương thức này được chạy sau :ref:`_save_image_at_path()<class_GLTFDocumentExtension_private_method__save_image_at_path>` hoặc :ref:`_serialize_image_to_bytes()<class_GLTFDocumentExtension_private_method__serialize_image_to_bytes>`, và trước :ref:`_export_node()<class_GLTFDocumentExtension_private_method__export_node>`. Lưu ý rằng phương thức này chỉ được chạy khi **GLTFDocumentExtension** này được chọn làm image exporter.

Có thể sử dụng phương thức này để thiết lập các extension cho JSON texture bằng cách chỉnh sửa ``texture_json``. Extension cũng phải được thêm dưới dạng extension được sử dụng bằng :ref:`GLTFState.add_used_extension()<class_GLTFState_method_add_used_extension>`; hãy nhớ đặt ``required`` thành ``true`` nếu bạn không cung cấp fallback.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
