:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFBufferView.xml.

.. _class_GLTFBufferView:

GLTFBufferView
==============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một buffer view của glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

GLTFBufferView là một cấu trúc dữ liệu đại diện cho một ``bufferView`` glTF được tìm thấy trong mảng ``"bufferViews"``. Một buffer là một khối dữ liệu nhị phân. Một buffer view là một phần của buffer có thể được dùng để xác định và trích xuất dữ liệu từ buffer.

Hầu hết các trường hợp sử dụng buffer tùy chỉnh chỉ cần dùng :ref:`buffer<class_GLTFBufferView_property_buffer>`, :ref:`byte_length<class_GLTFBufferView_property_byte_length>` và :ref:`byte_offset<class_GLTFBufferView_property_byte_offset>`. Các thuộc tính :ref:`byte_stride<class_GLTFBufferView_property_byte_stride>` và :ref:`indices<class_GLTFBufferView_property_indices>` dành cho những trường hợp sử dụng nâng cao hơn, chẳng hạn như dữ liệu mesh đan xen được mã hóa cho GPU.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `Buffers, BufferViews, and Accessors in Khronos glTF specification <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_005_BuffersBufferViewsAccessors.md>`__

- :doc:`Tải và lưu tệp runtime <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`   | :ref:`buffer<class_GLTFBufferView_property_buffer>`                       | ``-1``    |
   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`   | :ref:`byte_length<class_GLTFBufferView_property_byte_length>`             | ``0``     |
   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`   | :ref:`byte_offset<class_GLTFBufferView_property_byte_offset>`             | ``0``     |
   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`   | :ref:`byte_stride<class_GLTFBufferView_property_byte_stride>`             | ``-1``    |
   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`indices<class_GLTFBufferView_property_indices>`                     | ``false`` |
   +-------------------------+---------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`vertex_attributes<class_GLTFBufferView_property_vertex_attributes>` | ``false`` |
   +-------------------------+---------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFBufferView<class_GLTFBufferView>`   | :ref:`from_dictionary<class_GLTFBufferView_method_from_dictionary>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static|     |
   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`load_buffer_view_data<class_GLTFBufferView_method_load_buffer_view_data>`\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |const| |
   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`           | :ref:`to_dictionary<class_GLTFBufferView_method_to_dictionary>`\ (\ ) |const|                                                            |
   +-----------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFBufferView_property_buffer:

.. rst-class:: classref-property

:ref:`int<class_int>` **buffer** = ``-1`` :ref:`🔗<class_GLTFBufferView_property_buffer>`

.. rst-class:: classref-property-setget

- |void| **set_buffer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_buffer**\ (\ )

Chỉ mục của buffer mà buffer view này đang tham chiếu. Nếu là ``-1``, buffer view này không tham chiếu đến buffer nào.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_property_byte_length:

.. rst-class:: classref-property

:ref:`int<class_int>` **byte_length** = ``0`` :ref:`🔗<class_GLTFBufferView_property_byte_length>`

.. rst-class:: classref-property-setget

- |void| **set_byte_length**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_byte_length**\ (\ )

Độ dài, tính bằng byte, của buffer view này. Nếu là ``0``, buffer view này trống.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_property_byte_offset:

.. rst-class:: classref-property

:ref:`int<class_int>` **byte_offset** = ``0`` :ref:`🔗<class_GLTFBufferView_property_byte_offset>`

.. rst-class:: classref-property-setget

- |void| **set_byte_offset**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_byte_offset**\ (\ )

Độ lệch, tính bằng byte, từ đầu buffer đến đầu buffer view này.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_property_byte_stride:

.. rst-class:: classref-property

:ref:`int<class_int>` **byte_stride** = ``-1`` :ref:`🔗<class_GLTFBufferView_property_byte_stride>`

.. rst-class:: classref-property-setget

- |void| **set_byte_stride**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_byte_stride**\ (\ )

Stride, tính bằng byte, giữa các dữ liệu đan xen. Nếu là ``-1``, buffer view này không đan xen.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_property_indices:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **indices** = ``false`` :ref:`🔗<class_GLTFBufferView_property_indices>`

.. rst-class:: classref-property-setget

- |void| **set_indices**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_indices**\ (\ )

``true`` nếu kiểu buffer OpenGL GPU của GLTFBufferView là một ``ELEMENT_ARRAY_BUFFER`` được dùng cho các chỉ mục vertex (hằng số nguyên ``34963``). ``false`` nếu kiểu buffer là bất kỳ giá trị nào khác. Xem `Buffers, BufferViews, and Accessors <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_005_BuffersBufferViewsAccessors.md>`__ để biết các giá trị có thể có. Thuộc tính này được thiết lập khi import và được dùng khi export.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_property_vertex_attributes:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **vertex_attributes** = ``false`` :ref:`🔗<class_GLTFBufferView_property_vertex_attributes>`

.. rst-class:: classref-property-setget

- |void| **set_vertex_attributes**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_vertex_attributes**\ (\ )

``true`` nếu kiểu buffer OpenGL GPU của GLTFBufferView là một ``ARRAY_BUFFER`` được dùng cho các thuộc tính vertex (hằng số nguyên ``34962``). ``false`` nếu kiểu buffer là bất kỳ giá trị nào khác. Xem `Buffers, BufferViews, and Accessors <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_005_BuffersBufferViewsAccessors.md>`__ để biết các giá trị có thể có. Thuộc tính này được thiết lập khi import và được dùng khi export.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFBufferView_method_from_dictionary:

.. rst-class:: classref-method

:ref:`GLTFBufferView<class_GLTFBufferView>` **from_dictionary**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| :ref:`🔗<class_GLTFBufferView_method_from_dictionary>`

Tạo một thực thể GLTFBufferView mới bằng cách phân tích :ref:`Dictionary<class_Dictionary>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_method_load_buffer_view_data:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **load_buffer_view_data**\ (\ state\: :ref:`GLTFState<class_GLTFState>`\ ) |const| :ref:`🔗<class_GLTFBufferView_method_load_buffer_view_data>`

Tải dữ liệu buffer view từ buffer được tham chiếu bởi buffer view này trong :ref:`GLTFState<class_GLTFState>` đã cho. Phương thức này hiện chưa hỗ trợ dữ liệu đan xen có byte stride. Dữ liệu được trả về dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFBufferView_method_to_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **to_dictionary**\ (\ ) |const| :ref:`🔗<class_GLTFBufferView_method_to_dictionary>`

Tuần tự hóa thực thể GLTFBufferView này thành một :ref:`Dictionary<class_Dictionary>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
