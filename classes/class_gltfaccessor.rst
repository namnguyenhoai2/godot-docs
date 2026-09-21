:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFAccessor.xml.

.. _class_GLTFAccessor:

GLTFAccessor
============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Biểu diễn một accessor glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

GLTFAccessor là một cấu trúc dữ liệu biểu diễn một ``accessor`` glTF được tìm thấy trong mảng ``"accessors"``. Buffer là một khối dữ liệu nhị phân. Buffer view là một lát cắt của buffer. Accessor là cách diễn giải có kiểu của dữ liệu trong buffer view.

Hầu hết dữ liệu tùy chỉnh được lưu trữ trong glTF không cần accessor mà chỉ cần buffer view (xem :ref:`GLTFBufferView<class_GLTFBufferView>`). Accessor dành cho các trường hợp sử dụng nâng cao hơn, chẳng hạn như dữ liệu mesh đan xen được mã hóa cho GPU.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `Buffers, BufferViews, and Accessors in Khronos glTF specification <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_005_BuffersBufferViewsAccessors.md>`__

- :doc:`Tải và lưu tệp runtime <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>`   | :ref:`accessor_type<class_GLTFAccessor_property_accessor_type>`                                 | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`buffer_view<class_GLTFAccessor_property_buffer_view>`                                     | ``-1``                   |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`byte_offset<class_GLTFAccessor_property_byte_offset>`                                     | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` | :ref:`component_type<class_GLTFAccessor_property_component_type>`                               | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`count<class_GLTFAccessor_property_count>`                                                 | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedFloat64Array<class_PackedFloat64Array>`           | :ref:`max<class_GLTFAccessor_property_max>`                                                     | ``PackedFloat64Array()`` |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedFloat64Array<class_PackedFloat64Array>`           | :ref:`min<class_GLTFAccessor_property_min>`                                                     | ``PackedFloat64Array()`` |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                                       | :ref:`normalized<class_GLTFAccessor_property_normalized>`                                       | ``false``                |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`sparse_count<class_GLTFAccessor_property_sparse_count>`                                   | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`sparse_indices_buffer_view<class_GLTFAccessor_property_sparse_indices_buffer_view>`       | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`sparse_indices_byte_offset<class_GLTFAccessor_property_sparse_indices_byte_offset>`       | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` | :ref:`sparse_indices_component_type<class_GLTFAccessor_property_sparse_indices_component_type>` | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`sparse_values_buffer_view<class_GLTFAccessor_property_sparse_values_buffer_view>`         | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`sparse_values_byte_offset<class_GLTFAccessor_property_sparse_values_byte_offset>`         | ``0``                    |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                                         | :ref:`type<class_GLTFAccessor_property_type>`                                                   |                          |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFAccessor<class_GLTFAccessor>` | :ref:`from_dictionary<class_GLTFAccessor_method_from_dictionary>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| |
   +-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`     | :ref:`to_dictionary<class_GLTFAccessor_method_to_dictionary>`\ (\ ) |const|                                                        |
   +-----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_GLTFAccessor_GLTFAccessorType:

.. rst-class:: classref-enumeration

enum **GLTFAccessorType**: :ref:`🔗<enum_GLTFAccessor_GLTFAccessorType>`

.. _class_GLTFAccessor_constant_TYPE_SCALAR:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_SCALAR** = ``0``

Kiểu accessor "SCALAR". Đối với mô hình đối tượng glTF, kiểu này có thể được dùng để ánh xạ tới một giá trị float, int hoặc bool đơn, hoặc một mảng float.

.. _class_GLTFAccessor_constant_TYPE_VEC2:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_VEC2** = ``1``

Kiểu accessor "VEC2". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float2", được biểu diễn trong JSON glTF dưới dạng một mảng gồm hai số thực.

.. _class_GLTFAccessor_constant_TYPE_VEC3:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_VEC3** = ``2``

Kiểu accessor "VEC3". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float3", được biểu diễn trong JSON glTF dưới dạng một mảng gồm ba số thực.

.. _class_GLTFAccessor_constant_TYPE_VEC4:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_VEC4** = ``3``

Kiểu accessor "VEC4". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float4", được biểu diễn trong JSON glTF dưới dạng một mảng gồm bốn số thực.

.. _class_GLTFAccessor_constant_TYPE_MAT2:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_MAT2** = ``4``

Kiểu accessor "MAT2". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float2x2", được biểu diễn trong JSON glTF dưới dạng một mảng gồm bốn số thực.

.. _class_GLTFAccessor_constant_TYPE_MAT3:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_MAT3** = ``5``

Kiểu accessor "MAT3". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float3x3", được biểu diễn trong JSON glTF dưới dạng một mảng gồm chín số thực.

.. _class_GLTFAccessor_constant_TYPE_MAT4:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **TYPE_MAT4** = ``6``

Kiểu accessor "MAT4". Đối với mô hình đối tượng glTF, kiểu này ánh xạ tới "float4x4", được biểu diễn trong JSON glTF dưới dạng một mảng gồm mười sáu số thực.

.. rst-class:: classref-item-separator

----

.. _enum_GLTFAccessor_GLTFComponentType:

.. rst-class:: classref-enumeration

enum **GLTFComponentType**: :ref:`🔗<enum_GLTFAccessor_GLTFComponentType>`

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_NONE** = ``0``

Kiểu component "NONE". Đây không phải là một kiểu component hợp lệ và được dùng để cho biết kiểu component chưa được thiết lập.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_SIGNED_BYTE:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_SIGNED_BYTE** = ``5120``

Kiểu component "BYTE". Giá trị là ``0x1400``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên có dấu 1 byte hoặc 8 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_UNSIGNED_BYTE:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_UNSIGNED_BYTE** = ``5121``

Kiểu component "UNSIGNED_BYTE". Giá trị là ``0x1401``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên không dấu 1 byte hoặc 8 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_SIGNED_SHORT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_SIGNED_SHORT** = ``5122``

Kiểu component "SHORT". Giá trị là ``0x1402``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên có dấu 2 byte hoặc 16 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_UNSIGNED_SHORT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_UNSIGNED_SHORT** = ``5123``

Kiểu component "UNSIGNED_SHORT". Giá trị là ``0x1403``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên không dấu 2 byte hoặc 16 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_SIGNED_INT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_SIGNED_INT** = ``5124``

Kiểu component "INT". Giá trị là ``0x1404``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên có dấu 4 byte hoặc 32 bit. Đây KHÔNG phải là một phần cốt lõi của đặc tả glTF và có thể không được tất cả glTF importer hỗ trợ. Có thể được một số extension sử dụng, bao gồm ``KHR_interactivity``.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_UNSIGNED_INT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_UNSIGNED_INT** = ``5125``

Kiểu component "UNSIGNED_INT". Giá trị là ``0x1405``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên không dấu 4 byte hoặc 32 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_SINGLE_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_SINGLE_FLOAT** = ``5126``

Kiểu component "FLOAT". Giá trị là ``0x1406``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số dấu phẩy động 4 byte hoặc 32 bit. Đây là một phần cốt lõi của đặc tả glTF.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_DOUBLE_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_DOUBLE_FLOAT** = ``5130``

Kiểu component "DOUBLE". Giá trị là ``0x140A``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số dấu phẩy động 8 byte hoặc 64 bit. Đây KHÔNG phải là một phần cốt lõi của đặc tả glTF và có thể không được tất cả glTF importer hỗ trợ. Có thể được một số extension sử dụng, bao gồm ``KHR_interactivity``.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_HALF_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_HALF_FLOAT** = ``5131``

Kiểu component "HALF_FLOAT". Giá trị là ``0x140B``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số dấu phẩy động 2 byte hoặc 16 bit. Đây KHÔNG phải là một phần cốt lõi của đặc tả glTF và có thể không được tất cả glTF importer hỗ trợ. Có thể được một số extension sử dụng, bao gồm ``KHR_interactivity``.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_SIGNED_LONG:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_SIGNED_LONG** = ``5134``

Kiểu component "LONG". Giá trị là ``0x140E``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên có dấu 8 byte hoặc 64 bit. Đây KHÔNG phải là một phần cốt lõi của đặc tả glTF và có thể không được tất cả glTF importer hỗ trợ. Có thể được một số extension sử dụng, bao gồm ``KHR_interactivity``.

.. _class_GLTFAccessor_constant_COMPONENT_TYPE_UNSIGNED_LONG:

.. rst-class:: classref-enumeration-constant

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **COMPONENT_TYPE_UNSIGNED_LONG** = ``5135``

Kiểu component "UNSIGNED_LONG". Giá trị là ``0x140F``, bắt nguồn từ OpenGL. Điều này cho biết dữ liệu được lưu trữ dưới dạng số nguyên không dấu 8 byte hoặc 64 bit. Đây KHÔNG phải là một phần cốt lõi của đặc tả glTF và có thể không được tất cả glTF importer hỗ trợ. Có thể được một số extension sử dụng, bao gồm ``KHR_interactivity``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFAccessor_property_accessor_type:

.. rst-class:: classref-property

:ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **accessor_type** = ``0`` :ref:`🔗<class_GLTFAccessor_property_accessor_type>`

.. rst-class:: classref-property-setget

- |void| **set_accessor_type**\ (\ value\: :ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>`\ ) - :ref:`GLTFAccessorType<enum_GLTFAccessor_GLTFAccessorType>` **get_accessor_type**\ (\ )

Kiểu accessor glTF, dưới dạng enum.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_buffer_view:

.. rst-class:: classref-property

:ref:`int<class_int>` **buffer_view** = ``-1`` :ref:`🔗<class_GLTFAccessor_property_buffer_view>`

.. rst-class:: classref-property-setget

- |void| **set_buffer_view**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_buffer_view**\ (\ )

Chỉ mục của buffer view mà accessor này tham chiếu. Nếu là ``-1``, accessor này không tham chiếu đến buffer view nào.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_byte_offset:

.. rst-class:: classref-property

:ref:`int<class_int>` **byte_offset** = ``0`` :ref:`🔗<class_GLTFAccessor_property_byte_offset>`

.. rst-class:: classref-property-setget

- |void| **set_byte_offset**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_byte_offset**\ (\ )

Offset tính bằng byte, tương đối so với phần đầu của buffer view.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_component_type:

.. rst-class:: classref-property

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **component_type** = ``0`` :ref:`🔗<class_GLTFAccessor_property_component_type>`

.. rst-class:: classref-property-setget

- |void| **set_component_type**\ (\ value\: :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>`\ ) - :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **get_component_type**\ (\ )

Kiểu component glTF, dưới dạng enum. Xem :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` để biết các giá trị khả dụng. Trong đặc tả glTF cốt lõi, không được sử dụng giá trị 5125 hoặc "UNSIGNED_INT" cho bất kỳ accessor nào không được mesh.primitive.indices tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **count** = ``0`` :ref:`🔗<class_GLTFAccessor_property_count>`

.. rst-class:: classref-property-setget

- |void| **set_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_count**\ (\ )

Số phần tử được accessor này tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_max:

.. rst-class:: classref-property

:ref:`PackedFloat64Array<class_PackedFloat64Array>` **max** = ``PackedFloat64Array()`` :ref:`🔗<class_GLTFAccessor_property_max>`

.. rst-class:: classref-property-setget

- |void| **set_max**\ (\ value\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`\ ) - :ref:`PackedFloat64Array<class_PackedFloat64Array>` **get_max**\ (\ )

Giá trị lớn nhất của mỗi component trong accessor này.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat64Array<class_PackedFloat64Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_min:

.. rst-class:: classref-property

:ref:`PackedFloat64Array<class_PackedFloat64Array>` **min** = ``PackedFloat64Array()`` :ref:`🔗<class_GLTFAccessor_property_min>`

.. rst-class:: classref-property-setget

- |void| **set_min**\ (\ value\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`\ ) - :ref:`PackedFloat64Array<class_PackedFloat64Array>` **get_min**\ (\ )

Giá trị nhỏ nhất của mỗi component trong accessor này.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat64Array<class_PackedFloat64Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_normalized:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **normalized** = ``false`` :ref:`🔗<class_GLTFAccessor_property_normalized>`

.. rst-class:: classref-property-setget

- |void| **set_normalized**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_normalized**\ (\ )

Chỉ định liệu các giá trị dữ liệu integer có được normalized trước khi sử dụng hay không.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **sparse_count** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_count>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sparse_count**\ (\ )

Số lượng các giá trị accessor sai lệch được lưu trữ trong sparse array.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_indices_buffer_view:

.. rst-class:: classref-property

:ref:`int<class_int>` **sparse_indices_buffer_view** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_indices_buffer_view>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_indices_buffer_view**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sparse_indices_buffer_view**\ (\ )

Chỉ mục của buffer view chứa các sparse indices. Buffer view được tham chiếu MUST NOT có các thuộc tính target hoặc byteStride được định nghĩa. Buffer view và byteOffset tùy chọn MUST được căn chỉnh theo độ dài byte của componentType.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_indices_byte_offset:

.. rst-class:: classref-property

:ref:`int<class_int>` **sparse_indices_byte_offset** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_indices_byte_offset>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_indices_byte_offset**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sparse_indices_byte_offset**\ (\ )

Offset tính bằng byte so với đầu buffer view.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_indices_component_type:

.. rst-class:: classref-property

:ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **sparse_indices_component_type** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_indices_component_type>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_indices_component_type**\ (\ value\: :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>`\ ) - :ref:`GLTFComponentType<enum_GLTFAccessor_GLTFComponentType>` **get_sparse_indices_component_type**\ (\ )

Kiểu dữ liệu component của các indices dưới dạng enum. Các giá trị có thể có là 5121 cho "UNSIGNED_BYTE", 5123 cho "UNSIGNED_SHORT" và 5125 cho "UNSIGNED_INT".

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_values_buffer_view:

.. rst-class:: classref-property

:ref:`int<class_int>` **sparse_values_buffer_view** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_values_buffer_view>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_values_buffer_view**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sparse_values_buffer_view**\ (\ )

Chỉ mục của bufferView chứa các sparse values. Buffer view được tham chiếu MUST NOT có các thuộc tính target hoặc byteStride được định nghĩa.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_sparse_values_byte_offset:

.. rst-class:: classref-property

:ref:`int<class_int>` **sparse_values_byte_offset** = ``0`` :ref:`🔗<class_GLTFAccessor_property_sparse_values_byte_offset>`

.. rst-class:: classref-property-setget

- |void| **set_sparse_values_byte_offset**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sparse_values_byte_offset**\ (\ )

Offset tính bằng byte so với đầu bufferView.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_property_type:

.. rst-class:: classref-property

:ref:`int<class_int>` **type** :ref:`🔗<class_GLTFAccessor_property_type>`

.. rst-class:: classref-property-setget

- |void| **set_type**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_type**\ (\ )

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`accessor_type<class_GLTFAccessor_property_accessor_type>`.

Kiểu accessor của glTF, dưới dạng :ref:`int<class_int>`. Các giá trị có thể có là ``0`` cho "SCALAR", ``1`` cho "VEC2", ``2`` cho "VEC3", ``3`` cho "VEC4", ``4`` cho "MAT2", ``5`` cho "MAT3" và ``6`` cho "MAT4".

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFAccessor_method_from_dictionary:

.. rst-class:: classref-method

:ref:`GLTFAccessor<class_GLTFAccessor>` **from_dictionary**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| :ref:`🔗<class_GLTFAccessor_method_from_dictionary>`

Tạo một instance GLTFAccessor mới bằng cách phân tích :ref:`Dictionary<class_Dictionary>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFAccessor_method_to_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **to_dictionary**\ (\ ) |const| :ref:`🔗<class_GLTFAccessor_method_to_dictionary>`

Serialize instance GLTFAccessor này thành một :ref:`Dictionary<class_Dictionary>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
