:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedDataContainerRef.xml.

.. _class_PackedDataContainerRef:

PackedDataContainerRef
======================

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`@GlobalScope.var_to_bytes()<class_@GlobalScope_method_var_to_bytes>` hoặc :ref:`FileAccess.store_var()<class_FileAccess_method_store_var>`. Để bật tính năng nén dữ liệu, hãy sử dụng :ref:`PackedByteArray.compress()<class_PackedByteArray_method_compress>` hoặc :ref:`FileAccess.open_compressed()<class_FileAccess_method_open_compressed>`.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một lớp nội bộ được :ref:`PackedDataContainer<class_PackedDataContainer>` sử dụng để đóng gói các mảng và dictionary lồng nhau.

.. rst-class:: classref-introduction-group

Mô tả
-----

Khi đóng gói các container lồng nhau bằng :ref:`PackedDataContainer<class_PackedDataContainer>`, chúng sẽ được đóng gói đệ quy vào **PackedDataContainerRef** (chỉ áp dụng cho :ref:`Array<class_Array>` và :ref:`Dictionary<class_Dictionary>`). Có thể truy xuất dữ liệu của chúng theo cùng cách như từ :ref:`PackedDataContainer<class_PackedDataContainer>`.

::

    var packed = PackedDataContainer.new()
    packed.pack([1, 2, 3, ["nested1", "nested2"], 4, 5, 6])

    for element in packed:
        if element is PackedDataContainerRef:
            for subelement in element:
                print("::", subelement)
        else:
            print(element)

In ra:

.. code:: text

    1
    2
    3
    ::nested1
    ::nested2
    4
    5
    6

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------+---------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`size<class_PackedDataContainerRef_method_size>`\ (\ ) |const| |
   +-----------------------+---------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedDataContainerRef_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedDataContainerRef_method_size>`

Trả về kích thước của container đã đóng gói (xem :ref:`Array.size()<class_Array_method_size>` và :ref:`Dictionary.size()<class_Dictionary_method_size>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
