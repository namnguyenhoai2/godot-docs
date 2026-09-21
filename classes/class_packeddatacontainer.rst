:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedDataContainer.xml.

.. _class_PackedDataContainer:

PackedDataContainer
===================

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`@GlobalScope.var_to_bytes()<class_@GlobalScope_method_var_to_bytes>` hoặc :ref:`FileAccess.store_var()<class_FileAccess_method_store_var>`. Để bật tính năng nén dữ liệu, hãy sử dụng :ref:`PackedByteArray.compress()<class_PackedByteArray_method_compress>` hoặc :ref:`FileAccess.open_compressed()<class_FileAccess_method_open_compressed>`.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đóng gói và tuần tự hóa :ref:`Array<class_Array>` hoặc :ref:`Dictionary<class_Dictionary>` một cách hiệu quả.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PackedDataContainer** có thể được dùng để lưu trữ hiệu quả dữ liệu từ các container không định kiểu. Dữ liệu được đóng gói thành các byte thô và có thể được lưu vào tệp. Chỉ :ref:`Array<class_Array>` và :ref:`Dictionary<class_Dictionary>` mới có thể được lưu trữ theo cách này.

Bạn có thể lấy dữ liệu bằng cách lặp qua container; thao tác này sẽ hoạt động như thể đang lặp trực tiếp trên dữ liệu đã đóng gói. Nếu packed container là một :ref:`Dictionary<class_Dictionary>`, bạn có thể lấy dữ liệu theo tên khóa (chỉ :ref:`String<class_String>`/:ref:`StringName<class_StringName>`).

::

    var data = { "key": "value", "another_key": 123, "lock": Vector2() }
    var packed = PackedDataContainer.new()
    packed.pack(data)
    ResourceSaver.save(packed, "packed_data.res")

::

    var container = load("packed_data.res")
    for key in container:
        prints(key, container[key])

In ra:

.. code:: text

    key value
    lock (0, 0)
    another_key 123

Các container lồng nhau sẽ được đóng gói đệ quy. Khi lặp qua, chúng sẽ được trả về dưới dạng :ref:`PackedDataContainerRef<class_PackedDataContainerRef>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`pack<class_PackedDataContainer_method_pack>`\ (\ value\: :ref:`Variant<class_Variant>`\ ) |
   +---------------------------------------+-------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`size<class_PackedDataContainer_method_size>`\ (\ ) |const|                                |
   +---------------------------------------+-------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedDataContainer_method_pack:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **pack**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_PackedDataContainer_method_pack>`

Đóng gói container đã cho thành một biểu diễn nhị phân. ``value`` phải là :ref:`Array<class_Array>` hoặc :ref:`Dictionary<class_Dictionary>`; bất kỳ kiểu nào khác sẽ dẫn đến lỗi dữ liệu không hợp lệ.

\ **Lưu ý:** Các lần gọi tiếp theo đến phương thức này sẽ ghi đè dữ liệu hiện có.

.. rst-class:: classref-item-separator

----

.. _class_PackedDataContainer_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedDataContainer_method_size>`

Trả về kích thước của packed container (xem :ref:`Array.size()<class_Array_method_size>` và :ref:`Dictionary.size()<class_Dictionary_method_size>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
