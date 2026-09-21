:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Marshalls.xml.

.. _class_Marshalls:

Marshalls
=========

**Kế thừa:** :ref:`Object<class_Object>`

Các tiện ích chuyển đổi dữ liệu (marshaling) và mã hóa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp các hàm tiện ích để chuyển đổi và mã hóa dữ liệu.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`base64_to_raw<class_Marshalls_method_base64_to_raw>`\ (\ base64_str\: :ref:`String<class_String>`\ )                                                          |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`base64_to_utf8<class_Marshalls_method_base64_to_utf8>`\ (\ base64_str\: :ref:`String<class_String>`\ )                                                        |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                 | :ref:`base64_to_variant<class_Marshalls_method_base64_to_variant>`\ (\ base64_str\: :ref:`String<class_String>`, allow_objects\: :ref:`bool<class_bool>` = false\ ) |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`raw_to_base64<class_Marshalls_method_raw_to_base64>`\ (\ array\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                             |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`utf8_to_base64<class_Marshalls_method_utf8_to_base64>`\ (\ utf8_str\: :ref:`String<class_String>`\ )                                                          |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`variant_to_base64<class_Marshalls_method_variant_to_base64>`\ (\ variant\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ )   |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Marshalls_method_base64_to_raw:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **base64_to_raw**\ (\ base64_str\: :ref:`String<class_String>`\ ) :ref:`🔗<class_Marshalls_method_base64_to_raw>`

Trả về một :ref:`PackedByteArray<class_PackedByteArray>` đã được giải mã tương ứng với chuỗi được mã hóa Base64 ``base64_str``.

.. rst-class:: classref-item-separator

----

.. _class_Marshalls_method_base64_to_utf8:

.. rst-class:: classref-method

:ref:`String<class_String>` **base64_to_utf8**\ (\ base64_str\: :ref:`String<class_String>`\ ) :ref:`🔗<class_Marshalls_method_base64_to_utf8>`

Trả về một chuỗi đã được giải mã tương ứng với chuỗi được mã hóa Base64 ``base64_str``.

.. rst-class:: classref-item-separator

----

.. _class_Marshalls_method_base64_to_variant:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **base64_to_variant**\ (\ base64_str\: :ref:`String<class_String>`, allow_objects\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Marshalls_method_base64_to_variant>`

Trả về một :ref:`Variant<class_Variant>` đã được giải mã tương ứng với chuỗi được mã hóa Base64 ``base64_str``. Nếu ``allow_objects`` là ``true``, thì cho phép giải mã các object.

Bên trong, phương thức này sử dụng cùng cơ chế giải mã như phương thức :ref:`@GlobalScope.bytes_to_var()<class_@GlobalScope_method_bytes_to_var>`.

\ **Cảnh báo:** Các object được deserialize có thể chứa mã được thực thi. Không sử dụng tùy chọn này nếu object được serialize đến từ các nguồn không đáng tin cậy để tránh các mối đe dọa bảo mật tiềm ẩn như thực thi mã từ xa.

.. rst-class:: classref-item-separator

----

.. _class_Marshalls_method_raw_to_base64:

.. rst-class:: classref-method

:ref:`String<class_String>` **raw_to_base64**\ (\ array\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_Marshalls_method_raw_to_base64>`

Trả về một chuỗi được mã hóa Base64 của :ref:`PackedByteArray<class_PackedByteArray>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Marshalls_method_utf8_to_base64:

.. rst-class:: classref-method

:ref:`String<class_String>` **utf8_to_base64**\ (\ utf8_str\: :ref:`String<class_String>`\ ) :ref:`🔗<class_Marshalls_method_utf8_to_base64>`

Trả về một chuỗi được mã hóa Base64 của chuỗi UTF-8 ``utf8_str``.

.. rst-class:: classref-item-separator

----

.. _class_Marshalls_method_variant_to_base64:

.. rst-class:: classref-method

:ref:`String<class_String>` **variant_to_base64**\ (\ variant\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Marshalls_method_variant_to_base64>`

Returns a Base64-encoded string of the :ref:`Variant<class_Variant>` ``variant``. If ``full_objects`` is ``true``, encoding objects is allowed (and can potentially include code).

Bên trong, phương thức này sử dụng cùng cơ chế mã hóa như phương thức :ref:`@GlobalScope.var_to_bytes()<class_@GlobalScope_method_var_to_bytes>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
