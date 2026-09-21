:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CharFXTransform.xml.

.. _class_CharFXTransform:

CharFXTransform
===============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Kiểm soát cách một ký tự riêng lẻ được hiển thị trong :ref:`RichTextEffect<class_RichTextEffect>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thiết lập nhiều thuộc tính khác nhau trên đối tượng này, bạn có thể kiểm soát cách từng ký tự được hiển thị trong :ref:`RichTextEffect<class_RichTextEffect>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`BBCode in RichTextLabel <../tutorials/ui/bbcode_in_richtextlabel>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`             | :ref:`color<class_CharFXTransform_property_color>`                   | ``Color(0, 0, 0, 1)``             |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`             | :ref:`elapsed_time<class_CharFXTransform_property_elapsed_time>`     | ``0.0``                           |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`Dictionary<class_Dictionary>`   | :ref:`env<class_CharFXTransform_property_env>`                       | ``{}``                            |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`RID<class_RID>`                 | :ref:`font<class_CharFXTransform_property_font>`                     | ``RID()``                         |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                 | :ref:`glyph_count<class_CharFXTransform_property_glyph_count>`       | ``0``                             |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                 | :ref:`glyph_flags<class_CharFXTransform_property_glyph_flags>`       | ``0``                             |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                 | :ref:`glyph_index<class_CharFXTransform_property_glyph_index>`       | ``0``                             |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`offset<class_CharFXTransform_property_offset>`                 | ``Vector2(0, 0)``                 |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`outline<class_CharFXTransform_property_outline>`               | ``false``                         |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2i<class_Vector2i>`       | :ref:`range<class_CharFXTransform_property_range>`                   | ``Vector2i(0, 0)``                |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                 | :ref:`relative_index<class_CharFXTransform_property_relative_index>` | ``0``                             |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`transform<class_CharFXTransform_property_transform>`           | ``Transform2D(1, 0, 0, 1, 0, 0)`` |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`visible<class_CharFXTransform_property_visible>`               | ``true``                          |
   +---------------------------------------+----------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CharFXTransform_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_CharFXTransform_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

Màu mà ký tự sẽ được vẽ bằng.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_elapsed_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **elapsed_time** = ``0.0`` :ref:`🔗<class_CharFXTransform_property_elapsed_time>`

.. rst-class:: classref-property-setget

- |void| **set_elapsed_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_elapsed_time**\ (\ )

Thời gian đã trôi qua kể từ khi :ref:`RichTextLabel<class_RichTextLabel>` được thêm vào scene tree (tính bằng giây). Thời gian dừng khi :ref:`RichTextLabel<class_RichTextLabel>` được tạm dừng (xem :ref:`Node.process_mode<class_Node_property_process_mode>`). Được đặt lại khi văn bản trong :ref:`RichTextLabel<class_RichTextLabel>` thay đổi.

\ **Lưu ý:** Thời gian vẫn trôi qua khi :ref:`RichTextLabel<class_RichTextLabel>` bị ẩn.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_env:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **env** = ``{}`` :ref:`🔗<class_CharFXTransform_property_env>`

.. rst-class:: classref-property-setget

- |void| **set_environment**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_environment**\ (\ )

Chứa các đối số được truyền vào thẻ BBCode mở. Theo mặc định, các đối số là chuỗi; nếu nội dung của chúng khớp với một kiểu như :ref:`bool<class_bool>`, :ref:`int<class_int>` hoặc :ref:`float<class_float>`, chúng sẽ được tự động chuyển đổi. Mã màu ở dạng ``#rrggbb`` hoặc ``#rgb`` sẽ được chuyển đổi thành một :ref:`Color<class_Color>` không trong suốt. Đối số chuỗi không được chứa khoảng trắng, ngay cả khi chúng được đặt trong dấu ngoặc kép. Nếu có dấu ngoặc kép, chúng cũng sẽ xuất hiện trong chuỗi cuối cùng.

Ví dụ: thẻ BBCode mở ``[example foo=hello bar=true baz=42 color=#ffffff]`` sẽ ánh xạ tới :ref:`Dictionary<class_Dictionary>` sau đây:

::

    {"foo": "hello", "bar": true, "baz": 42, "color": Color(1, 1, 1, 1)}

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_font:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **font** = ``RID()`` :ref:`🔗<class_CharFXTransform_property_font>`

.. rst-class:: classref-property-setget

- |void| **set_font**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_font**\ (\ )

:ref:`TextServer<class_TextServer>` RID of the font used to render glyph, this value can be used with ``TextServer.font_*`` methods to retrieve font information.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_glyph_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **glyph_count** = ``0`` :ref:`🔗<class_CharFXTransform_property_glyph_count>`

.. rst-class:: classref-property-setget

- |void| **set_glyph_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_glyph_count**\ (\ )

Số glyph trong grapheme cluster. Giá trị này được thiết lập trong glyph đầu tiên của một cluster.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_glyph_flags:

.. rst-class:: classref-property

:ref:`int<class_int>` **glyph_flags** = ``0`` :ref:`🔗<class_CharFXTransform_property_glyph_flags>`

.. rst-class:: classref-property-setget

- |void| **set_glyph_flags**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_glyph_flags**\ (\ )

Các cờ của glyph. Xem :ref:`GraphemeFlag<enum_TextServer_GraphemeFlag>` để biết thêm thông tin.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_glyph_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **glyph_index** = ``0`` :ref:`🔗<class_CharFXTransform_property_glyph_index>`

.. rst-class:: classref-property-setget

- |void| **set_glyph_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_glyph_index**\ (\ )

Chỉ mục glyph dành riêng cho :ref:`font<class_CharFXTransform_property_font>`. Nếu muốn thay thế glyph này, hãy sử dụng :ref:`TextServer.font_get_glyph_index()<class_TextServer_method_font_get_glyph_index>` với :ref:`font<class_CharFXTransform_property_font>` để lấy chỉ mục glyph mới cho một ký tự.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_CharFXTransform_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Độ lệch vị trí mà ký tự sẽ được vẽ với (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_outline:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **outline** = ``false`` :ref:`🔗<class_CharFXTransform_property_outline>`

.. rst-class:: classref-property-setget

- |void| **set_outline**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_outline**\ (\ )

Nếu ``true``, FX transform sẽ được gọi để vẽ đường viền.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_range:

.. rst-class:: classref-property

:ref:`Vector2i<class_Vector2i>` **range** = ``Vector2i(0, 0)`` :ref:`🔗<class_CharFXTransform_property_range>`

.. rst-class:: classref-property-setget

- |void| **set_range**\ (\ value\: :ref:`Vector2i<class_Vector2i>`\ ) - :ref:`Vector2i<class_Vector2i>` **get_range**\ (\ )

Phạm vi ký tự tuyệt đối trong chuỗi, tương ứng với glyph.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_relative_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **relative_index** = ``0`` :ref:`🔗<class_CharFXTransform_property_relative_index>`

.. rst-class:: classref-property-setget

- |void| **set_relative_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_relative_index**\ (\ )

Độ lệch ký tự của glyph, tương đối so với custom block hiện tại của :ref:`RichTextEffect<class_RichTextEffect>`.

\ **Lưu ý:** Chỉ đọc. Việc thiết lập thuộc tính này sẽ không ảnh hưởng đến quá trình vẽ.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **transform** = ``Transform2D(1, 0, 0, 1, 0, 0)`` :ref:`🔗<class_CharFXTransform_property_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_transform**\ (\ )

Transform hiện tại của glyph hiện tại. Có thể ghi đè giá trị này (ví dụ: điều khiển vị trí và góc xoay từ một curve). Bạn cũng có thể thay đổi giá trị hiện có để áp dụng các transform bổ sung lên những hiệu ứng khác.

.. rst-class:: classref-item-separator

----

.. _class_CharFXTransform_property_visible:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **visible** = ``true`` :ref:`🔗<class_CharFXTransform_property_visible>`

.. rst-class:: classref-property-setget

- |void| **set_visibility**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_visible**\ (\ )

Nếu ``true``, ký tự sẽ được vẽ. Nếu ``false``, ký tự sẽ bị ẩn. Các ký tự xung quanh những ký tự bị ẩn sẽ reflow để sử dụng khoảng trống của các ký tự bị ẩn. Nếu không mong muốn điều này, hãy đặt :ref:`color<class_CharFXTransform_property_color>` của chúng thành ``Color(1, 1, 1, 0)`` thay thế.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
