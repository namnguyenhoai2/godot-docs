:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFState.xml.

.. _class_GLTFState:

GLTFState
=========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`FBXState<class_FBXState>`

Đại diện cho toàn bộ dữ liệu của một tệp glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

Chứa tất cả node và resource của một tệp glTF. :ref:`GLTFDocument<class_GLTFDocument>` sử dụng dữ liệu này làm nơi lưu trữ, nhờ đó :ref:`GLTFDocument<class_GLTFDocument>` và tất cả các lớp :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` có thể giữ trạng thái.

GLTFState có thể được điền dữ liệu bằng cách :ref:`GLTFDocument<class_GLTFDocument>` đọc một tệp hoặc chuyển đổi một scene Godot. Sau đó, dữ liệu có thể được dùng để tạo scene Godot hoặc lưu vào một tệp glTF. Mã chuyển đổi đến/từ scene Godot có thể được các lớp :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` can thiệp tại những điểm bất kỳ. Điều này cho phép lưu dữ liệu tùy chỉnh vào tệp glTF hoặc chuyển đổi dữ liệu tùy chỉnh đến/từ các node Godot.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tải và lưu tệp khi runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `glTF asset header schema <https://github.com/KhronosGroup/glTF/blob/main/specification/2.0/schema/asset.schema.json>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`float<class_float>`                                                  | :ref:`bake_fps<class_GLTFState_property_bake_fps>`                                 | ``30.0``               |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`String<class_String>`                                                | :ref:`base_path<class_GLTFState_property_base_path>`                               | ``""``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedByteArray<class_PackedByteArray>`\] | :ref:`buffers<class_GLTFState_property_buffers>`                                   | ``[]``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`String<class_String>`                                                | :ref:`copyright<class_GLTFState_property_copyright>`                               | ``""``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`create_animations<class_GLTFState_property_create_animations>`               | ``true``               |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`String<class_String>`                                                | :ref:`filename<class_GLTFState_property_filename>`                                 | ``""``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`                              | :ref:`glb_data<class_GLTFState_property_glb_data>`                                 | ``PackedByteArray()``  |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>`         | :ref:`handle_binary_image_mode<class_GLTFState_property_handle_binary_image_mode>` | ``1``                  |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`import_as_skeleton_bones<class_GLTFState_property_import_as_skeleton_bones>` | ``false``              |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                        | :ref:`json<class_GLTFState_property_json>`                                         | ``{}``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`major_version<class_GLTFState_property_major_version>`                       | ``0``                  |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`minor_version<class_GLTFState_property_minor_version>`                       | ``0``                  |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`                            | :ref:`root_nodes<class_GLTFState_property_root_nodes>`                             | ``PackedInt32Array()`` |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`String<class_String>`                                                | :ref:`scene_name<class_GLTFState_property_scene_name>`                             | ``""``                 |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`use_named_skin_binds<class_GLTFState_property_use_named_skin_binds>`         | ``false``              |
   +----------------------------------------------------------------------------+------------------------------------------------------------------------------------+------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`add_used_extension<class_GLTFState_method_add_used_extension>`\ (\ extension_name\: :ref:`String<class_String>`, required\: :ref:`bool<class_bool>`\ )                                               |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`append_data_to_buffers<class_GLTFState_method_append_data_to_buffers>`\ (\ data\: :ref:`PackedByteArray<class_PackedByteArray>`, deduplication\: :ref:`bool<class_bool>`\ )                          |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`append_gltf_node<class_GLTFState_method_append_gltf_node>`\ (\ gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, godot_scene_node\: :ref:`Node<class_Node>`, parent_node_index\: :ref:`int<class_int>`\ ) |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFAccessor<class_GLTFAccessor>`\]             | :ref:`get_accessors<class_GLTFState_method_get_accessors>`\ (\ ) |const|                                                                                                                                   |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                                    | :ref:`get_additional_data<class_GLTFState_method_get_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                 |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationPlayer<class_AnimationPlayer>`                                    | :ref:`get_animation_player<class_GLTFState_method_get_animation_player>`\ (\ anim_player_index\: :ref:`int<class_int>`\ ) |const|                                                                          |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`get_animation_players_count<class_GLTFState_method_get_animation_players_count>`\ (\ anim_player_index\: :ref:`int<class_int>`\ ) |const|                                                            |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFAnimation<class_GLTFAnimation>`\]           | :ref:`get_animations<class_GLTFState_method_get_animations>`\ (\ ) |const|                                                                                                                                 |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFBufferView<class_GLTFBufferView>`\]         | :ref:`get_buffer_views<class_GLTFState_method_get_buffer_views>`\ (\ ) |const|                                                                                                                             |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFCamera<class_GLTFCamera>`\]                 | :ref:`get_cameras<class_GLTFState_method_get_cameras>`\ (\ ) |const|                                                                                                                                       |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`get_handle_binary_image<class_GLTFState_method_get_handle_binary_image>`\ (\ ) |const|                                                                                                               |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\]                   | :ref:`get_images<class_GLTFState_method_get_images>`\ (\ ) |const|                                                                                                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFLight<class_GLTFLight>`\]                   | :ref:`get_lights<class_GLTFState_method_get_lights>`\ (\ ) |const|                                                                                                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\]                     | :ref:`get_materials<class_GLTFState_method_get_materials>`\ (\ ) |const|                                                                                                                                   |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFMesh<class_GLTFMesh>`\]                     | :ref:`get_meshes<class_GLTFState_method_get_meshes>`\ (\ ) |const|                                                                                                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`get_node_index<class_GLTFState_method_get_node_index>`\ (\ scene_node\: :ref:`Node<class_Node>`\ ) |const|                                                                                           |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFNode<class_GLTFNode>`\]                     | :ref:`get_nodes<class_GLTFState_method_get_nodes>`\ (\ ) |const|                                                                                                                                           |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                                          | :ref:`get_scene_node<class_GLTFState_method_get_scene_node>`\ (\ gltf_node_index\: :ref:`int<class_int>`\ ) |const|                                                                                        |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFSkeleton<class_GLTFSkeleton>`\]             | :ref:`get_skeletons<class_GLTFState_method_get_skeletons>`\ (\ ) |const|                                                                                                                                   |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFSkin<class_GLTFSkin>`\]                     | :ref:`get_skins<class_GLTFState_method_get_skins>`\ (\ ) |const|                                                                                                                                           |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFTextureSampler<class_GLTFTextureSampler>`\] | :ref:`get_texture_samplers<class_GLTFState_method_get_texture_samplers>`\ (\ ) |const|                                                                                                                     |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`GLTFTexture<class_GLTFTexture>`\]               | :ref:`get_textures<class_GLTFState_method_get_textures>`\ (\ ) |const|                                                                                                                                     |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]                         | :ref:`get_unique_animation_names<class_GLTFState_method_get_unique_animation_names>`\ (\ ) |const|                                                                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]                         | :ref:`get_unique_names<class_GLTFState_method_get_unique_names>`\ (\ ) |const|                                                                                                                             |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_accessors<class_GLTFState_method_set_accessors>`\ (\ accessors\: :ref:`Array<class_Array>`\[:ref:`GLTFAccessor<class_GLTFAccessor>`\]\ )                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_additional_data<class_GLTFState_method_set_additional_data>`\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ )                        |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_animations<class_GLTFState_method_set_animations>`\ (\ animations\: :ref:`Array<class_Array>`\[:ref:`GLTFAnimation<class_GLTFAnimation>`\]\ )                                                    |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_buffer_views<class_GLTFState_method_set_buffer_views>`\ (\ buffer_views\: :ref:`Array<class_Array>`\[:ref:`GLTFBufferView<class_GLTFBufferView>`\]\ )                                            |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_cameras<class_GLTFState_method_set_cameras>`\ (\ cameras\: :ref:`Array<class_Array>`\[:ref:`GLTFCamera<class_GLTFCamera>`\]\ )                                                                   |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_handle_binary_image<class_GLTFState_method_set_handle_binary_image>`\ (\ method\: :ref:`int<class_int>`\ )                                                                                       |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_images<class_GLTFState_method_set_images>`\ (\ images\: :ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\]\ )                                                                        |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_lights<class_GLTFState_method_set_lights>`\ (\ lights\: :ref:`Array<class_Array>`\[:ref:`GLTFLight<class_GLTFLight>`\]\ )                                                                        |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_materials<class_GLTFState_method_set_materials>`\ (\ materials\: :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\]\ )                                                                 |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_meshes<class_GLTFState_method_set_meshes>`\ (\ meshes\: :ref:`Array<class_Array>`\[:ref:`GLTFMesh<class_GLTFMesh>`\]\ )                                                                          |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_nodes<class_GLTFState_method_set_nodes>`\ (\ nodes\: :ref:`Array<class_Array>`\[:ref:`GLTFNode<class_GLTFNode>`\]\ )                                                                             |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_skeletons<class_GLTFState_method_set_skeletons>`\ (\ skeletons\: :ref:`Array<class_Array>`\[:ref:`GLTFSkeleton<class_GLTFSkeleton>`\]\ )                                                         |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_skins<class_GLTFState_method_set_skins>`\ (\ skins\: :ref:`Array<class_Array>`\[:ref:`GLTFSkin<class_GLTFSkin>`\]\ )                                                                             |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_texture_samplers<class_GLTFState_method_set_texture_samplers>`\ (\ texture_samplers\: :ref:`Array<class_Array>`\[:ref:`GLTFTextureSampler<class_GLTFTextureSampler>`\]\ )                        |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_textures<class_GLTFState_method_set_textures>`\ (\ textures\: :ref:`Array<class_Array>`\[:ref:`GLTFTexture<class_GLTFTexture>`\]\ )                                                              |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_unique_animation_names<class_GLTFState_method_set_unique_animation_names>`\ (\ unique_animation_names\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ )                              |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_unique_names<class_GLTFState_method_set_unique_names>`\ (\ unique_names\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ )                                                            |
   +----------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GLTFState_HandleBinaryImageMode:

.. rst-class:: classref-enumeration

enum **HandleBinaryImageMode**: :ref:`🔗<enum_GLTFState_HandleBinaryImageMode>`

.. _class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_DISCARD_TEXTURES:

.. rst-class:: classref-enumeration-constant

:ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **HANDLE_BINARY_IMAGE_MODE_DISCARD_TEXTURES** = ``0``

Khi import một tệp glTF có chứa các ảnh nhị phân được nhúng, loại bỏ tất cả ảnh và thay thế chúng bằng các material không có texture. Các ảnh được lưu dưới dạng tệp riêng trong thư mục ``res://`` không bị ảnh hưởng; chúng sẽ được sử dụng theo cách Godot đã import.

.. _class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EXTRACT_TEXTURES:

.. rst-class:: classref-enumeration-constant

:ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **HANDLE_BINARY_IMAGE_MODE_EXTRACT_TEXTURES** = ``1``

Khi import một tệp glTF có chứa các ảnh nhị phân được nhúng, trích xuất chúng và lưu vào các tệp riêng. Điều này cho phép image importer của Godot import ảnh, sau đó người dùng có thể tùy chỉnh các tùy chọn import, bao gồm tùy chọn nén ảnh sang các định dạng texture VRAM.

Thao tác này sẽ lưu các byte của ảnh chính xác như nguyên bản, không nén lại. Đối với các định dạng ảnh được cung cấp bởi các extension glTF, tệp sẽ có tên kết thúc bằng phần mở rộng tệp do :ref:`GLTFDocumentExtension._get_image_file_extension()<class_GLTFDocumentExtension_private_method__get_image_file_extension>` của lớp extension cung cấp.

\ **Lưu ý:** Tùy chọn này chỉ dành cho editor. Khi runtime, tùy chọn này hoạt động giống :ref:`HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED<class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED>`.

.. _class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EMBED_AS_BASISU:

.. rst-class:: classref-enumeration-constant

:ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **HANDLE_BINARY_IMAGE_MODE_EMBED_AS_BASISU** = ``2``

Khi import một tệp glTF có chứa các ảnh nhị phân được nhúng, nhúng các texture được nén VRAM bằng Basis Universal vào scene được tạo. Các ảnh được lưu dưới dạng tệp riêng trong thư mục ``res://`` không bị ảnh hưởng; chúng sẽ được sử dụng theo cách Godot đã import.

.. _class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED:

.. rst-class:: classref-enumeration-constant

:ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED** = ``3``

Khi import một tệp glTF có chứa các ảnh nhị phân được nhúng, nhúng các texture được nén không mất dữ liệu vào scene được tạo. Các ảnh được lưu dưới dạng tệp riêng trong thư mục ``res://`` không bị ảnh hưởng; chúng sẽ được sử dụng theo cách Godot đã import.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_GLTFState_constant_HANDLE_BINARY_DISCARD_TEXTURES:

.. rst-class:: classref-constant

**HANDLE_BINARY_DISCARD_TEXTURES** = ``0`` :ref:`🔗<class_GLTFState_constant_HANDLE_BINARY_DISCARD_TEXTURES>`

**Đã lỗi thời:** Thay vào đó, hãy dùng :ref:`HANDLE_BINARY_IMAGE_MODE_DISCARD_TEXTURES<class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_DISCARD_TEXTURES>`.

Loại bỏ tất cả texture được nhúng và sử dụng các material không có texture.

.. _class_GLTFState_constant_HANDLE_BINARY_EXTRACT_TEXTURES:

.. rst-class:: classref-constant

**HANDLE_BINARY_EXTRACT_TEXTURES** = ``1`` :ref:`🔗<class_GLTFState_constant_HANDLE_BINARY_EXTRACT_TEXTURES>`

**Đã lỗi thời:** Thay vào đó, hãy dùng :ref:`HANDLE_BINARY_IMAGE_MODE_EXTRACT_TEXTURES<class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EXTRACT_TEXTURES>`.

Trích xuất các texture được nhúng để import lại và nén. Chỉ dành cho editor. Khi runtime, hoạt động như dạng không nén.

.. _class_GLTFState_constant_HANDLE_BINARY_EMBED_AS_BASISU:

.. rst-class:: classref-constant

**HANDLE_BINARY_EMBED_AS_BASISU** = ``2`` :ref:`🔗<class_GLTFState_constant_HANDLE_BINARY_EMBED_AS_BASISU>`

**Đã lỗi thời:** Thay vào đó, hãy dùng :ref:`HANDLE_BINARY_IMAGE_MODE_EMBED_AS_BASISU<class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EMBED_AS_BASISU>`.

Nhúng các texture được nén VRAM bằng Basis Universal vào scene được tạo.

.. _class_GLTFState_constant_HANDLE_BINARY_EMBED_AS_UNCOMPRESSED:

.. rst-class:: classref-constant

**HANDLE_BINARY_EMBED_AS_UNCOMPRESSED** = ``3`` :ref:`🔗<class_GLTFState_constant_HANDLE_BINARY_EMBED_AS_UNCOMPRESSED>`

**Đã lỗi thời:** Thay vào đó, hãy dùng :ref:`HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED<class_GLTFState_constant_HANDLE_BINARY_IMAGE_MODE_EMBED_AS_UNCOMPRESSED>`.

Nhúng các texture được nén không mất dữ liệu vào scene được tạo, tương ứng với hành vi cũ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFState_property_bake_fps:

.. rst-class:: classref-property

:ref:`float<class_float>` **bake_fps** = ``30.0`` :ref:`🔗<class_GLTFState_property_bake_fps>`

.. rst-class:: classref-property-setget

- |void| **set_bake_fps**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bake_fps**\ (\ )

FPS bake của animation khi import hoặc export.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_base_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **base_path** = ``""`` :ref:`🔗<class_GLTFState_property_base_path>`

.. rst-class:: classref-property-setget

- |void| **set_base_path**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_base_path**\ (\ )

Đường dẫn thư mục liên kết với dữ liệu glTF này. Đường dẫn này được dùng để tìm các tệp khác được tệp glTF tham chiếu, chẳng hạn như ảnh hoặc buffer nhị phân. Giá trị này được thiết lập trong quá trình import khi nối dữ liệu từ một tệp, và được thiết lập trong quá trình export khi ghi vào một tệp.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_buffers:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`PackedByteArray<class_PackedByteArray>`\] **buffers** = ``[]`` :ref:`🔗<class_GLTFState_property_buffers>`

.. rst-class:: classref-property-setget

- |void| **set_buffers**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`PackedByteArray<class_PackedByteArray>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`PackedByteArray<class_PackedByteArray>`\] **get_buffers**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_copyright:

.. rst-class:: classref-property

:ref:`String<class_String>` **copyright** = ``""`` :ref:`🔗<class_GLTFState_property_copyright>`

.. rst-class:: classref-property-setget

- |void| **set_copyright**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_copyright**\ (\ )

Chuỗi bản quyền trong asset header của tệp glTF. Giá trị này được thiết lập trong quá trình import nếu có và trong quá trình export nếu không rỗng. Xem tài liệu về asset header của glTF để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_create_animations:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **create_animations** = ``true`` :ref:`🔗<class_GLTFState_property_create_animations>`

.. rst-class:: classref-property-setget

- |void| **set_create_animations**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_create_animations**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_filename:

.. rst-class:: classref-property

:ref:`String<class_String>` **filename** = ``""`` :ref:`🔗<class_GLTFState_property_filename>`

.. rst-class:: classref-property-setget

- |void| **set_filename**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_filename**\ (\ )

Tên tệp liên kết với dữ liệu glTF này. Nếu kết thúc bằng ``.gltf``, đây là glTF dạng văn bản; nếu không, đây là GLB nhị phân. Giá trị này được thiết lập trong quá trình import khi nối dữ liệu từ một tệp, và được thiết lập trong quá trình export khi ghi vào một tệp. Nếu ghi vào một buffer, đây sẽ là chuỗi rỗng.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_glb_data:

.. rst-class:: classref-property

:ref:`PackedByteArray<class_PackedByteArray>` **glb_data** = ``PackedByteArray()`` :ref:`🔗<class_GLTFState_property_glb_data>`

.. rst-class:: classref-property-setget

- |void| **set_glb_data**\ (\ value\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) - :ref:`PackedByteArray<class_PackedByteArray>` **get_glb_data**\ (\ )

Buffer nhị phân được đính kèm với tệp .glb.

**Lưu ý:** Mảng được trả về là một bản *sao chép*, và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedByteArray<class_PackedByteArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_handle_binary_image_mode:

.. rst-class:: classref-property

:ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **handle_binary_image_mode** = ``1`` :ref:`🔗<class_GLTFState_property_handle_binary_image_mode>`

.. rst-class:: classref-property-setget

- |void| **set_handle_binary_image_mode**\ (\ value\: :ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>`\ ) - :ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` **get_handle_binary_image_mode**\ (\ )

Khi import một tệp glTF có các ảnh nhị phân thô chưa được import được nhúng bên trong các buffer blob nhị phân, trong data URI hoặc trong các tệp riêng chưa được Godot import, tùy chọn này kiểm soát cách xử lý các ảnh. Ảnh có thể bị loại bỏ, được lưu dưới dạng tệp riêng hoặc được nhúng vào scene theo cách nén mất dữ liệu hoặc không mất dữ liệu. Xem :ref:`HandleBinaryImageMode<enum_GLTFState_HandleBinaryImageMode>` để biết các tùy chọn.

Thuộc tính này không có tác dụng đối với các tệp ảnh trong thư mục ``res://`` được Godot import, vì chúng được image importer của Godot xử lý trực tiếp; sau đó scene Godot được tạo từ tệp glTF sẽ sử dụng các ảnh theo cách Godot đã import.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_import_as_skeleton_bones:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **import_as_skeleton_bones** = ``false`` :ref:`🔗<class_GLTFState_property_import_as_skeleton_bones>`

.. rst-class:: classref-property-setget

- |void| **set_import_as_skeleton_bones**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_import_as_skeleton_bones**\ (\ )

Nếu ``true``, buộc tất cả GLTFNode trong tài liệu trở thành các bone của một node Godot :ref:`Skeleton3D<class_Skeleton3D>` duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_json:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **json** = ``{}`` :ref:`🔗<class_GLTFState_property_json>`

.. rst-class:: classref-property-setget

- |void| **set_json**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_json**\ (\ )

Tài liệu JSON thô ban đầu tương ứng với GLTFState này.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_major_version:

.. rst-class:: classref-property

:ref:`int<class_int>` **major_version** = ``0`` :ref:`🔗<class_GLTFState_property_major_version>`

.. rst-class:: classref-property-setget

- |void| **set_major_version**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_major_version**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_minor_version:

.. rst-class:: classref-property

:ref:`int<class_int>` **minor_version** = ``0`` :ref:`🔗<class_GLTFState_property_minor_version>`

.. rst-class:: classref-property-setget

- |void| **set_minor_version**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_minor_version**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_root_nodes:

.. rst-class:: classref-property

:ref:`PackedInt32Array<class_PackedInt32Array>` **root_nodes** = ``PackedInt32Array()`` :ref:`🔗<class_GLTFState_property_root_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_root_nodes**\ (\ value\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) - :ref:`PackedInt32Array<class_PackedInt32Array>` **get_root_nodes**\ (\ )

Các node gốc của tệp glTF. Thông thường, một tệp glTF chỉ có một scene và do đó chỉ có một node gốc. Tuy nhiên, một tệp glTF có thể có nhiều scene và do đó có nhiều node gốc; các node này sẽ được tạo làm các node cùng cấp với nhau và làm node con của node gốc trong scene Godot được tạo.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedInt32Array<class_PackedInt32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_scene_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **scene_name** = ``""`` :ref:`🔗<class_GLTFState_property_scene_name>`

.. rst-class:: classref-property-setget

- |void| **set_scene_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_scene_name**\ (\ )

Tên của scene. Khi import, nếu không được chỉ định, giá trị này sẽ là tên tệp. Khi export, nếu được chỉ định, tên scene sẽ được lưu vào tệp glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_property_use_named_skin_binds:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_named_skin_binds** = ``false`` :ref:`🔗<class_GLTFState_property_use_named_skin_binds>`

.. rst-class:: classref-property-setget

- |void| **set_use_named_skin_binds**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_named_skin_binds**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_GLTFState_method_add_used_extension:

.. rst-class:: classref-method

|void| **add_used_extension**\ (\ extension_name\: :ref:`String<class_String>`, required\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GLTFState_method_add_used_extension>`

Thêm một extension vào danh sách các extension được tệp glTF này sử dụng trong quá trình serialization. Nếu ``required`` là ``true``, extension đó cũng sẽ được thêm vào danh sách các extension bắt buộc. Không chạy lệnh này trong :ref:`GLTFDocumentExtension._export_post()<class_GLTFDocumentExtension_private_method__export_post>`, vì giai đoạn đó đã quá muộn để thêm extension. Danh sách cuối cùng được sắp xếp theo thứ tự bảng chữ cái.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_append_data_to_buffers:

.. rst-class:: classref-method

:ref:`int<class_int>` **append_data_to_buffers**\ (\ data\: :ref:`PackedByteArray<class_PackedByteArray>`, deduplication\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GLTFState_method_append_data_to_buffers>`

Thêm mảng byte đã cho ``data`` vào các buffer và tạo một :ref:`GLTFBufferView<class_GLTFBufferView>` cho mảng đó. Chỉ mục của :ref:`GLTFBufferView<class_GLTFBufferView>` đích được trả về. Nếu ``deduplication`` là ``true``, trước tiên các buffer sẽ được tìm kiếm dữ liệu trùng lặp; nếu không, các byte mới luôn được thêm vào.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_append_gltf_node:

.. rst-class:: classref-method

:ref:`int<class_int>` **append_gltf_node**\ (\ gltf_node\: :ref:`GLTFNode<class_GLTFNode>`, godot_scene_node\: :ref:`Node<class_Node>`, parent_node_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GLTFState_method_append_gltf_node>`

Thêm :ref:`GLTFNode<class_GLTFNode>` đã cho vào state và trả về chỉ mục mới của nó. Có thể dùng phương thức này để export một node Godot thành nhiều node glTF hoặc chèn các node glTF mới trong thời gian import. Khi import, phải gọi phương thức này trước khi :ref:`GLTFDocumentExtension._generate_scene_node()<class_GLTFDocumentExtension_private_method__generate_scene_node>` hoàn tất cho node cha. Khi export, phải gọi phương thức này trước khi :ref:`GLTFDocumentExtension._export_node()<class_GLTFDocumentExtension_private_method__export_node>` chạy cho node cha.

Tham số ``godot_scene_node`` là node scene Godot tương ứng với node glTF này. Rất nên đặt tham số này thành một node hợp lệ, nhưng có thể là ``null`` nếu không có node scene Godot tương ứng. Một node scene Godot có thể được dùng cho nhiều node glTF, vì vậy nếu export nhiều node glTF cho một node scene Godot, hãy dùng cùng node scene Godot đó cho từng node.

Tham số ``parent_node_index`` là chỉ mục của :ref:`GLTFNode<class_GLTFNode>` cha trong state. Nếu là ``-1``, node sẽ là node gốc; nếu không, node mới sẽ được thêm vào danh sách node con của node cha. Chỉ mục này cũng sẽ được ghi vào thuộc tính :ref:`GLTFNode.parent<class_GLTFNode_property_parent>` của node mới.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_accessors:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFAccessor<class_GLTFAccessor>`\] **get_accessors**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_accessors>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_additional_data:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_GLTFState_method_get_additional_data>`

Lấy dữ liệu tùy ý bổ sung trong instance **GLTFState** này. Có thể dùng dữ liệu này để lưu state data theo từng tệp trong các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này rất quan trọng vì chúng là stateless.

Đối số phải là tên :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` (không nhất thiết phải khớp với tên extension trong tệp glTF), và giá trị trả về có thể là bất cứ thứ gì bạn đặt. Nếu chưa đặt gì, giá trị trả về là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_animation_player:

.. rst-class:: classref-method

:ref:`AnimationPlayer<class_AnimationPlayer>` **get_animation_player**\ (\ anim_player_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GLTFState_method_get_animation_player>`

Trả về node :ref:`AnimationPlayer<class_AnimationPlayer>` có chỉ mục đã cho. Các node này chỉ được sử dụng trong quá trình export khi chuyển đổi các node :ref:`AnimationPlayer<class_AnimationPlayer>` của Godot thành animation glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_animation_players_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_animation_players_count**\ (\ anim_player_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GLTFState_method_get_animation_players_count>`

Trả về số lượng node :ref:`AnimationPlayer<class_AnimationPlayer>` trong **GLTFState** này. Các node này chỉ được sử dụng trong quá trình export khi chuyển đổi các node :ref:`AnimationPlayer<class_AnimationPlayer>` của Godot thành animation glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_animations:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFAnimation<class_GLTFAnimation>`\] **get_animations**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_animations>`

Trả về một mảng chứa tất cả :ref:`GLTFAnimation<class_GLTFAnimation>`\ s trong tệp glTF. Khi import, chúng sẽ được tạo thành các animation trong node :ref:`AnimationPlayer<class_AnimationPlayer>`. Khi export, chúng sẽ được tạo từ các node :ref:`AnimationPlayer<class_AnimationPlayer>` của Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_buffer_views:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFBufferView<class_GLTFBufferView>`\] **get_buffer_views**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_buffer_views>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_cameras:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFCamera<class_GLTFCamera>`\] **get_cameras**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_cameras>`

Trả về một mảng chứa tất cả :ref:`GLTFCamera<class_GLTFCamera>`\ s trong tệp glTF. Đây là các camera mà chỉ mục :ref:`GLTFNode.camera<class_GLTFNode_property_camera>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_handle_binary_image:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_handle_binary_image**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_handle_binary_image>`

**Đã ngừng sử dụng:** Thay vào đó, hãy dùng :ref:`handle_binary_image_mode<class_GLTFState_property_handle_binary_image_mode>`.

Bí danh untyped đã ngừng sử dụng cho :ref:`handle_binary_image_mode<class_GLTFState_property_handle_binary_image_mode>`. Khi import một tệp glTF có các hình ảnh nhị phân thô chưa được import được nhúng bên trong các buffer binary blob, trong các data URI hoặc trong các tệp riêng không được Godot import, tùy chọn này kiểm soát cách xử lý các hình ảnh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_images:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\] **get_images**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_images>`

Lấy các hình ảnh của tệp glTF dưới dạng một mảng các :ref:`Texture2D<class_Texture2D>`\ s. Đây là các hình ảnh mà chỉ mục :ref:`GLTFTexture.src_image<class_GLTFTexture_property_src_image>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_lights:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFLight<class_GLTFLight>`\] **get_lights**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_lights>`

Trả về một mảng chứa tất cả :ref:`GLTFLight<class_GLTFLight>`\ s trong tệp glTF. Đây là các light mà chỉ mục :ref:`GLTFNode.light<class_GLTFNode_property_light>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_materials:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\] **get_materials**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_materials>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_meshes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFMesh<class_GLTFMesh>`\] **get_meshes**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_meshes>`

Trả về một mảng chứa tất cả :ref:`GLTFMesh<class_GLTFMesh>`\ es trong tệp glTF. Đây là các mesh mà chỉ mục :ref:`GLTFNode.mesh<class_GLTFNode_property_mesh>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_node_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_node_index**\ (\ scene_node\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_GLTFState_method_get_node_index>`

Trả về chỉ mục của :ref:`GLTFNode<class_GLTFNode>` tương ứng với node scene Godot này. Đây là phép đảo của :ref:`get_scene_node()<class_GLTFState_method_get_scene_node>`. Hữu ích trong quá trình export.

\ **Lưu ý:** Không phải mọi node scene Godot đều có :ref:`GLTFNode<class_GLTFNode>` tương ứng và không phải mọi :ref:`GLTFNode<class_GLTFNode>` đều có node scene được tạo. Nếu không có chỉ mục :ref:`GLTFNode<class_GLTFNode>` cho node scene này, ``-1`` sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_nodes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFNode<class_GLTFNode>`\] **get_nodes**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_nodes>`

Trả về một mảng chứa tất cả :ref:`GLTFNode<class_GLTFNode>`\ s trong tệp glTF. Đây là các node mà :ref:`GLTFNode.children<class_GLTFNode_property_children>` và :ref:`root_nodes<class_GLTFState_property_root_nodes>` tham chiếu đến. Mảng này bao gồm các node có thể không được tạo trong scene Godot hoặc các node có thể tạo ra nhiều node scene Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_scene_node:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_scene_node**\ (\ gltf_node_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GLTFState_method_get_scene_node>`

Trả về node scene Godot tương ứng với cùng chỉ mục như :ref:`GLTFNode<class_GLTFNode>` mà nó được tạo từ đó. Đây là phép đảo của :ref:`get_node_index()<class_GLTFState_method_get_node_index>`. Hữu ích trong quá trình import.

\ **Lưu ý:** Không phải mọi :ref:`GLTFNode<class_GLTFNode>` đều có node scene được tạo và không phải mọi node scene được tạo đều có :ref:`GLTFNode<class_GLTFNode>` tương ứng. Nếu không có scene node cho chỉ mục :ref:`GLTFNode<class_GLTFNode>` này, ``null`` sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_skeletons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFSkeleton<class_GLTFSkeleton>`\] **get_skeletons**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_skeletons>`

Trả về một mảng chứa tất cả :ref:`GLTFSkeleton<class_GLTFSkeleton>`\ s trong tệp glTF. Đây là các skeleton mà chỉ mục :ref:`GLTFNode.skeleton<class_GLTFNode_property_skeleton>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_skins:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFSkin<class_GLTFSkin>`\] **get_skins**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_skins>`

Trả về một mảng chứa tất cả :ref:`GLTFSkin<class_GLTFSkin>`\ s trong tệp glTF. Đây là các skin mà chỉ mục :ref:`GLTFNode.skin<class_GLTFNode_property_skin>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_texture_samplers:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFTextureSampler<class_GLTFTextureSampler>`\] **get_texture_samplers**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_texture_samplers>`

Lấy mảng các texture sampler được sử dụng bởi những texture có trong glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_textures:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`GLTFTexture<class_GLTFTexture>`\] **get_textures**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_textures>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_unique_animation_names:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`String<class_String>`\] **get_unique_animation_names**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_unique_animation_names>`

Trả về một mảng các tên animation duy nhất. Tên này chỉ được sử dụng trong quá trình import.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_get_unique_names:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`String<class_String>`\] **get_unique_names**\ (\ ) |const| :ref:`🔗<class_GLTFState_method_get_unique_names>`

Trả về một mảng các tên node duy nhất. Mảng này được sử dụng trong cả quá trình import và export.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_accessors:

.. rst-class:: classref-method

|void| **set_accessors**\ (\ accessors\: :ref:`Array<class_Array>`\[:ref:`GLTFAccessor<class_GLTFAccessor>`\]\ ) :ref:`🔗<class_GLTFState_method_set_accessors>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_additional_data:

.. rst-class:: classref-method

|void| **set_additional_data**\ (\ extension_name\: :ref:`StringName<class_StringName>`, additional_data\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GLTFState_method_set_additional_data>`

Thiết lập dữ liệu tùy ý bổ sung trong instance **GLTFState** này. Dữ liệu này có thể được dùng để lưu dữ liệu trạng thái theo từng file trong các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`, điều này rất quan trọng vì chúng không có trạng thái.

Đối số đầu tiên phải là tên :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` (không nhất thiết phải khớp với tên extension trong file glTF), còn đối số thứ hai có thể là bất cứ giá trị nào bạn muốn.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_animations:

.. rst-class:: classref-method

|void| **set_animations**\ (\ animations\: :ref:`Array<class_Array>`\[:ref:`GLTFAnimation<class_GLTFAnimation>`\]\ ) :ref:`🔗<class_GLTFState_method_set_animations>`

Thiết lập các :ref:`GLTFAnimation<class_GLTFAnimation>` trong state. Khi import, chúng sẽ được tạo thành các animation trong node :ref:`AnimationPlayer<class_AnimationPlayer>`. Khi export, chúng sẽ được tạo từ các node :ref:`AnimationPlayer<class_AnimationPlayer>` của Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_buffer_views:

.. rst-class:: classref-method

|void| **set_buffer_views**\ (\ buffer_views\: :ref:`Array<class_Array>`\[:ref:`GLTFBufferView<class_GLTFBufferView>`\]\ ) :ref:`🔗<class_GLTFState_method_set_buffer_views>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_cameras:

.. rst-class:: classref-method

|void| **set_cameras**\ (\ cameras\: :ref:`Array<class_Array>`\[:ref:`GLTFCamera<class_GLTFCamera>`\]\ ) :ref:`🔗<class_GLTFState_method_set_cameras>`

Thiết lập các :ref:`GLTFCamera<class_GLTFCamera>` trong state. Đây là các camera mà chỉ mục :ref:`GLTFNode.camera<class_GLTFNode_property_camera>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_handle_binary_image:

.. rst-class:: classref-method

|void| **set_handle_binary_image**\ (\ method\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GLTFState_method_set_handle_binary_image>`

**Đã ngừng sử dụng:** Thay vào đó, hãy sử dụng :ref:`handle_binary_image_mode<class_GLTFState_property_handle_binary_image_mode>`.

Bí danh không định kiểu đã ngừng sử dụng cho :ref:`handle_binary_image_mode<class_GLTFState_property_handle_binary_image_mode>`. Khi import file glTF có các ảnh nhị phân thô chưa được import được nhúng bên trong các buffer binary blob, trong data URI hoặc trong các file riêng biệt chưa được Godot import, tùy chọn này kiểm soát cách xử lý các ảnh.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_images:

.. rst-class:: classref-method

|void| **set_images**\ (\ images\: :ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\]\ ) :ref:`🔗<class_GLTFState_method_set_images>`

Thiết lập các image trong state, được lưu dưới dạng một mảng các :ref:`Texture2D<class_Texture2D>`. Có thể sử dụng trong quá trình export. Đây là các image mà chỉ mục :ref:`GLTFTexture.src_image<class_GLTFTexture_property_src_image>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_lights:

.. rst-class:: classref-method

|void| **set_lights**\ (\ lights\: :ref:`Array<class_Array>`\[:ref:`GLTFLight<class_GLTFLight>`\]\ ) :ref:`🔗<class_GLTFState_method_set_lights>`

Thiết lập các :ref:`GLTFLight<class_GLTFLight>` trong state. Đây là các light mà chỉ mục :ref:`GLTFNode.light<class_GLTFNode_property_light>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_materials:

.. rst-class:: classref-method

|void| **set_materials**\ (\ materials\: :ref:`Array<class_Array>`\[:ref:`Material<class_Material>`\]\ ) :ref:`🔗<class_GLTFState_method_set_materials>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_meshes:

.. rst-class:: classref-method

|void| **set_meshes**\ (\ meshes\: :ref:`Array<class_Array>`\[:ref:`GLTFMesh<class_GLTFMesh>`\]\ ) :ref:`🔗<class_GLTFState_method_set_meshes>`

Thiết lập các :ref:`GLTFMesh<class_GLTFMesh>` trong state. Đây là các mesh mà chỉ mục :ref:`GLTFNode.mesh<class_GLTFNode_property_mesh>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_nodes:

.. rst-class:: classref-method

|void| **set_nodes**\ (\ nodes\: :ref:`Array<class_Array>`\[:ref:`GLTFNode<class_GLTFNode>`\]\ ) :ref:`🔗<class_GLTFState_method_set_nodes>`

Thiết lập các :ref:`GLTFNode<class_GLTFNode>` trong state. Đây là các node mà :ref:`GLTFNode.children<class_GLTFNode_property_children>` và :ref:`root_nodes<class_GLTFState_property_root_nodes>` tham chiếu đến. Một số node được thiết lập ở đây có thể không được tạo trong scene Godot hoặc có thể tạo ra nhiều node scene Godot.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_skeletons:

.. rst-class:: classref-method

|void| **set_skeletons**\ (\ skeletons\: :ref:`Array<class_Array>`\[:ref:`GLTFSkeleton<class_GLTFSkeleton>`\]\ ) :ref:`🔗<class_GLTFState_method_set_skeletons>`

Thiết lập các :ref:`GLTFSkeleton<class_GLTFSkeleton>` trong state. Đây là các skeleton mà chỉ mục :ref:`GLTFNode.skeleton<class_GLTFNode_property_skeleton>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_skins:

.. rst-class:: classref-method

|void| **set_skins**\ (\ skins\: :ref:`Array<class_Array>`\[:ref:`GLTFSkin<class_GLTFSkin>`\]\ ) :ref:`🔗<class_GLTFState_method_set_skins>`

Thiết lập các :ref:`GLTFSkin<class_GLTFSkin>` trong state. Đây là các skin mà chỉ mục :ref:`GLTFNode.skin<class_GLTFNode_property_skin>` tham chiếu đến.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_texture_samplers:

.. rst-class:: classref-method

|void| **set_texture_samplers**\ (\ texture_samplers\: :ref:`Array<class_Array>`\[:ref:`GLTFTextureSampler<class_GLTFTextureSampler>`\]\ ) :ref:`🔗<class_GLTFState_method_set_texture_samplers>`

Thiết lập mảng các texture sampler được sử dụng bởi những texture có trong glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_textures:

.. rst-class:: classref-method

|void| **set_textures**\ (\ textures\: :ref:`Array<class_Array>`\[:ref:`GLTFTexture<class_GLTFTexture>`\]\ ) :ref:`🔗<class_GLTFState_method_set_textures>`

.. container:: contribute

	Hiện chưa có mô tả cho method này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_unique_animation_names:

.. rst-class:: classref-method

|void| **set_unique_animation_names**\ (\ unique_animation_names\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ ) :ref:`🔗<class_GLTFState_method_set_unique_animation_names>`

Thiết lập các tên animation duy nhất trong state. Tên này chỉ được sử dụng trong quá trình import.

.. rst-class:: classref-item-separator

----

.. _class_GLTFState_method_set_unique_names:

.. rst-class:: classref-method

|void| **set_unique_names**\ (\ unique_names\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ ) :ref:`🔗<class_GLTFState_method_set_unique_names>`

Thiết lập các tên node duy nhất trong state. Các tên này được sử dụng trong cả quá trình import và export.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
