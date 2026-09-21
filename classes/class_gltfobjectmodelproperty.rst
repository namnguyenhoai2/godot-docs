:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFObjectModelProperty.xml.

.. _class_GLTFObjectModelProperty:

GLTFObjectModelProperty
=======================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mô tả cách truy cập một property được định nghĩa trong glTF object model.

.. rst-class:: classref-introduction-group

Mô tả
-----

GLTFObjectModelProperty định nghĩa ánh xạ giữa một property trong glTF object model và một NodePath trong cây scene của Godot. Có thể dùng nó để animate các property trong tệp glTF bằng extension ``KHR_animation_pointer``, hoặc truy cập chúng thông qua một script độc lập với engine, chẳng hạn như behavior graph được định nghĩa bởi extension ``KHR_interactivity``.

glTF property được xác định bởi các JSON pointer được lưu trong :ref:`json_pointers<class_GLTFObjectModelProperty_property_json_pointers>`, trong khi Godot property mà nó ánh xạ tới được định nghĩa bởi :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>`. Trong hầu hết trường hợp, :ref:`json_pointers<class_GLTFObjectModelProperty_property_json_pointers>` và :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>` mỗi biến sẽ chỉ có một item, nhưng trong một số trường hợp, một glTF JSON pointer có thể ánh xạ tới nhiều Godot property, hoặc một Godot property có thể được ánh xạ tới nhiều glTF JSON pointer, hoặc có thể là quan hệ nhiều-nhiều.

\ Các object :ref:`Expression<class_Expression>` có thể được dùng để định nghĩa việc chuyển đổi giữa các dữ liệu, chẳng hạn như khi glTF định nghĩa một góc theo radians còn Godot sử dụng degrees. Property :ref:`object_model_type<class_GLTFObjectModelProperty_property_object_model_type>` định nghĩa kiểu dữ liệu được lưu trong tệp glTF theo object model; xem :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` để biết các giá trị có thể có.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `GLTF Object Model <https://github.com/KhronosGroup/glTF/blob/main/specification/2.0/ObjectModel.adoc>`__

- `KHR_animation_pointer GLTF extension <https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_animation_pointer>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`Expression<class_Expression>`                                            | :ref:`gltf_to_godot_expression<class_GLTFObjectModelProperty_property_gltf_to_godot_expression>` |        |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`Expression<class_Expression>`                                            | :ref:`godot_to_gltf_expression<class_GLTFObjectModelProperty_property_godot_to_gltf_expression>` |        |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] | :ref:`json_pointers<class_GLTFObjectModelProperty_property_json_pointers>`                       | ``[]`` |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]                   | :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>`                             | ``[]`` |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>`   | :ref:`object_model_type<class_GLTFObjectModelProperty_property_object_model_type>`               | ``0``  |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+
   | :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`                            | :ref:`variant_type<class_GLTFObjectModelProperty_property_variant_type>`                         | ``0``  |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                      | :ref:`append_node_path<class_GLTFObjectModelProperty_method_append_node_path>`\ (\ node_path\: :ref:`NodePath<class_NodePath>`\ )                                                                                                         |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                      | :ref:`append_path_to_property<class_GLTFObjectModelProperty_method_append_path_to_property>`\ (\ node_path\: :ref:`NodePath<class_NodePath>`, prop_name\: :ref:`StringName<class_StringName>`\ )                                          |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` | :ref:`get_accessor_type<class_GLTFObjectModelProperty_method_get_accessor_type>`\ (\ ) |const|                                                                                                                                            |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`has_json_pointers<class_GLTFObjectModelProperty_method_has_json_pointers>`\ (\ ) |const|                                                                                                                                            |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`has_node_paths<class_GLTFObjectModelProperty_method_has_node_paths>`\ (\ ) |const|                                                                                                                                                  |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                      | :ref:`set_types<class_GLTFObjectModelProperty_method_set_types>`\ (\ variant_type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, obj_model_type\: :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>`\ ) |
   +-------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_GLTFObjectModelProperty_GLTFObjectModelType:

.. rst-class:: classref-enumeration

enum **GLTFObjectModelType**: :ref:`🔗<enum_GLTFObjectModelProperty_GLTFObjectModelType>`

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_UNKNOWN:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_UNKNOWN** = ``0``

Kiểu object model không xác định hoặc chưa được thiết lập. Nếu kiểu object model được đặt thành giá trị này, vẫn cần xác định kiểu thực tế.

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_BOOL:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_BOOL** = ``1``

Kiểu object model "bool". Được biểu diễn trong glTF JSON dưới dạng boolean và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "SCALAR". Khi được mã hóa trong một accessor, giá trị ``0`` là ``false``, còn mọi giá trị khác là ``true``.

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT** = ``2``

Kiểu object model "float". Được biểu diễn trong glTF JSON dưới dạng một số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "SCALAR".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT_ARRAY:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT_ARRAY** = ``3``

Kiểu object model "float\[\]". Được biểu diễn trong glTF JSON dưới dạng một mảng các số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "SCALAR".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT2:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT2** = ``4``

Kiểu object model "float2". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm hai số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "VEC2".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT3:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT3** = ``5``

Kiểu object model "float3". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm ba số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "VEC3".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT4:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT4** = ``6``

Kiểu object model "float4". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm bốn số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "VEC4".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT2X2:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT2X2** = ``7``

Kiểu object model "float2x2". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm bốn số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "MAT2".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT3X3:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT3X3** = ``8``

Kiểu object model "float3x3". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm chín số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "MAT3".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_FLOAT4X4:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_FLOAT4X4** = ``9``

Kiểu object model "float4x4". Được biểu diễn trong glTF JSON dưới dạng một mảng gồm mười sáu số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "MAT4".

.. _class_GLTFObjectModelProperty_constant_GLTF_OBJECT_MODEL_TYPE_INT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **GLTF_OBJECT_MODEL_TYPE_INT** = ``10``

Kiểu object model "int". Được biểu diễn trong glTF JSON dưới dạng một số và được mã hóa trong một :ref:`GLTFAccessor<class_GLTFAccessor>` dưới dạng "SCALAR". Phạm vi giá trị bị giới hạn ở các số nguyên có dấu. Đối với ``KHR_interactivity``, chỉ hỗ trợ số nguyên 32-bit.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_GLTFObjectModelProperty_property_gltf_to_godot_expression:

.. rst-class:: classref-property

:ref:`Expression<class_Expression>` **gltf_to_godot_expression** :ref:`🔗<class_GLTFObjectModelProperty_property_gltf_to_godot_expression>`

.. rst-class:: classref-property-setget

- |void| **set_gltf_to_godot_expression**\ (\ value\: :ref:`Expression<class_Expression>`\ ) - :ref:`Expression<class_Expression>` **get_gltf_to_godot_expression**\ (\ )

Nếu được thiết lập, :ref:`Expression<class_Expression>` này sẽ được dùng để chuyển đổi giá trị property từ glTF object model sang giá trị mà Godot property yêu cầu. Điều này hữu ích khi glTF object model sử dụng một hệ đơn vị khác, hoặc khi dữ liệu cần được biến đổi theo một cách nào đó. Nếu ``null``, giá trị sẽ được sao chép nguyên trạng.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_property_godot_to_gltf_expression:

.. rst-class:: classref-property

:ref:`Expression<class_Expression>` **godot_to_gltf_expression** :ref:`🔗<class_GLTFObjectModelProperty_property_godot_to_gltf_expression>`

.. rst-class:: classref-property-setget

- |void| **set_godot_to_gltf_expression**\ (\ value\: :ref:`Expression<class_Expression>`\ ) - :ref:`Expression<class_Expression>` **get_godot_to_gltf_expression**\ (\ )

Nếu được thiết lập, :ref:`Expression<class_Expression>` này sẽ được dùng để chuyển đổi giá trị property từ Godot property sang giá trị mà glTF object model yêu cầu. Điều này hữu ích khi glTF object model sử dụng một hệ đơn vị khác, hoặc khi dữ liệu cần được biến đổi theo một cách nào đó. Nếu ``null``, giá trị sẽ được sao chép nguyên trạng.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_property_json_pointers:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] **json_pointers** = ``[]`` :ref:`🔗<class_GLTFObjectModelProperty_property_json_pointers>`

.. rst-class:: classref-property-setget

- |void| **set_json_pointers**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] **get_json_pointers**\ (\ )

Các JSON pointer của glTF object model được dùng để xác định property trong glTF object model. Trong hầu hết trường hợp, mảng này sẽ chỉ có một item, nhưng một số trường hợp cụ thể có thể yêu cầu nhiều pointer. Bản thân các item là những mảng biểu diễn JSON pointer được tách thành các thành phần.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_property_node_paths:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **node_paths** = ``[]`` :ref:`🔗<class_GLTFObjectModelProperty_property_node_paths>`

.. rst-class:: classref-property-setget

- |void| **set_node_paths**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **get_node_paths**\ (\ )

Một mảng các :ref:`NodePath<class_NodePath>`\ s trỏ tới một property hoặc nhiều property trong cây scene của Godot. Khi import, giá trị này sẽ được thiết lập bởi :ref:`GLTFDocument<class_GLTFDocument>`, hoặc bởi một class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>`. Đối với các trường hợp đơn giản, hãy dùng :ref:`append_path_to_property()<class_GLTFObjectModelProperty_method_append_path_to_property>` để thêm các property vào mảng này.

Trong hầu hết trường hợp, :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>` sẽ chỉ có một item, nhưng trong một số trường hợp, một glTF JSON pointer có thể ánh xạ tới nhiều Godot property. Ví dụ, một :ref:`GLTFCamera<class_GLTFCamera>` hoặc :ref:`GLTFLight<class_GLTFLight>` được dùng trên nhiều glTF node sẽ được biểu diễn bởi nhiều Godot node.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_property_object_model_type:

.. rst-class:: classref-property

:ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **object_model_type** = ``0`` :ref:`🔗<class_GLTFObjectModelProperty_property_object_model_type>`

.. rst-class:: classref-property-setget

- |void| **set_object_model_type**\ (\ value\: :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>`\ ) - :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` **get_object_model_type**\ (\ )

Kiểu dữ liệu được lưu trong tệp glTF theo định nghĩa của object model. Đây là một siêu tập của các accessor type hiện có và xác định accessor type.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_property_variant_type:

.. rst-class:: classref-property

:ref:`Variant.Type<enum_@GlobalScope_Variant.Type>` **variant_type** = ``0`` :ref:`🔗<class_GLTFObjectModelProperty_property_variant_type>`

.. rst-class:: classref-property-setget

- |void| **set_variant_type**\ (\ value\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`\ ) - :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>` **get_variant_type**\ (\ )

Kiểu dữ liệu được lưu trong Godot property. Đây là kiểu của property mà :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>` trỏ tới.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_GLTFObjectModelProperty_method_append_node_path:

.. rst-class:: classref-method

|void| **append_node_path**\ (\ node_path\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_GLTFObjectModelProperty_method_append_node_path>`

Thêm một :ref:`NodePath<class_NodePath>` vào :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>`. Các class :ref:`GLTFDocumentExtension<class_GLTFDocumentExtension>` có thể dùng cách này để định nghĩa cách một glTF object model property ánh xạ tới một Godot property hoặc nhiều Godot property. Nên dùng :ref:`append_path_to_property()<class_GLTFObjectModelProperty_method_append_path_to_property>` cho các trường hợp đơn giản. Đồng thời nhớ gọi :ref:`set_types()<class_GLTFObjectModelProperty_method_set_types>` một lần (thứ tự không quan trọng).

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_method_append_path_to_property:

.. rst-class:: classref-method

|void| **append_path_to_property**\ (\ node_path\: :ref:`NodePath<class_NodePath>`, prop_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_GLTFObjectModelProperty_method_append_path_to_property>`

Wrapper cấp cao cho :ref:`append_node_path()<class_GLTFObjectModelProperty_method_append_node_path>`, xử lý các trường hợp phổ biến nhất. Method này tạo một :ref:`NodePath<class_NodePath>` mới bằng cách dùng ``node_path`` làm cơ sở, rồi thêm ``prop_name`` vào subpath. Đồng thời nhớ gọi :ref:`set_types()<class_GLTFObjectModelProperty_method_set_types>` một lần (thứ tự không quan trọng).

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_method_get_accessor_type:

.. rst-class:: classref-method

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **get_accessor_type**\ (\ ) |const| :ref:`🔗<class_GLTFObjectModelProperty_method_get_accessor_type>`

Accessor type của GLTF liên kết với :ref:`object_model_type<class_GLTFObjectModelProperty_property_object_model_type>` của property này. Xem :ref:`GLTFAccessor.accessor_type<class_GLTFAccessor_property_accessor_type>` để biết các giá trị có thể có, và xem :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>` để biết cách kiểu object model ánh xạ tới accessor type.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_method_has_json_pointers:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_json_pointers**\ (\ ) |const| :ref:`🔗<class_GLTFObjectModelProperty_method_has_json_pointers>`

Trả về ``true`` nếu :ref:`json_pointers<class_GLTFObjectModelProperty_property_json_pointers>` không rỗng. Giá trị này được dùng trong quá trình export để xác định liệu **GLTFObjectModelProperty** có thể xử lý việc chuyển đổi một Godot property thành một glTF object model property hay không.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_method_has_node_paths:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_node_paths**\ (\ ) |const| :ref:`🔗<class_GLTFObjectModelProperty_method_has_node_paths>`

Trả về ``true`` nếu :ref:`node_paths<class_GLTFObjectModelProperty_property_node_paths>` không rỗng. Phương thức này được sử dụng trong quá trình import để xác định liệu một **GLTFObjectModelProperty** có thể xử lý việc chuyển đổi một thuộc tính trong mô hình đối tượng glTF thành một thuộc tính của Godot hay không.

.. rst-class:: classref-item-separator

----

.. _class_GLTFObjectModelProperty_method_set_types:

.. rst-class:: classref-method

|void| **set_types**\ (\ variant_type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, obj_model_type\: :ref:`GLTFObjectModelType<enum_GLTFObjectModelProperty_GLTFObjectModelType>`\ ) :ref:`🔗<class_GLTFObjectModelProperty_method_set_types>`

Thiết lập các thuộc tính :ref:`variant_type<class_GLTFObjectModelProperty_property_variant_type>` và :ref:`object_model_type<class_GLTFObjectModelProperty_property_object_model_type>`. Đây là một phương thức tiện ích để thiết lập cả hai thuộc tính cùng lúc, vì gần như lúc nào chúng cũng được biết đến cùng thời điểm. Phương thức này nên được gọi một lần. Việc gọi lại phương thức với cùng các giá trị sẽ không có tác dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
