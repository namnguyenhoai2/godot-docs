:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LinkButton.xml.

.. _class_LinkButton:

LinkButton
==========

**Kế thừa:** :ref:`BaseButton<class_BaseButton>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một nút đại diện cho một liên kết.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một nút đại diện cho một liên kết. Loại nút này chủ yếu được dùng cho các tương tác gây ra thay đổi ngữ cảnh (chẳng hạn như liên kết đến một trang web).

Xem thêm :ref:`BaseButton<class_BaseButton>`, chứa các thuộc tính và phương thức phổ biến liên quan đến node này.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`ellipsis_char<class_LinkButton_property_ellipsis_char>`                                                 | ``"…"``                                                                             |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`                          | focus_mode                                                                                                    | ``3`` (overrides :ref:`Control<class_Control_property_focus_mode>`)                 |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`language<class_LinkButton_property_language>`                                                           | ``""``                                                                              |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`CursorShape<enum_Control_CursorShape>`                      | mouse_default_cursor_shape                                                                                    | ``2`` (overrides :ref:`Control<class_Control_property_mouse_default_cursor_shape>`) |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` | :ref:`structured_text_bidi_override<class_LinkButton_property_structured_text_bidi_override>`                 | ``0``                                                                               |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                         | :ref:`structured_text_bidi_override_options<class_LinkButton_property_structured_text_bidi_override_options>` | ``[]``                                                                              |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`text<class_LinkButton_property_text>`                                                                   | ``""``                                                                              |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`TextDirection<enum_Control_TextDirection>`                  | :ref:`text_direction<class_LinkButton_property_text_direction>`                                               | ``0``                                                                               |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`           | :ref:`text_overrun_behavior<class_LinkButton_property_text_overrun_behavior>`                                 | ``0``                                                                               |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`UnderlineMode<enum_LinkButton_UnderlineMode>`               | :ref:`underline<class_LinkButton_property_underline>`                                                         | ``0``                                                                               |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`uri<class_LinkButton_property_uri>`                                                                     | ``""``                                                                              |
   +-------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_color<class_LinkButton_theme_color_font_color>`                             | ``Color(0.875, 0.875, 0.875, 1)`` |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_disabled_color<class_LinkButton_theme_color_font_disabled_color>`           | ``Color(0, 0, 0, 1)``             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_focus_color<class_LinkButton_theme_color_font_focus_color>`                 | ``Color(0.95, 0.95, 0.95, 1)``    |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_hover_color<class_LinkButton_theme_color_font_hover_color>`                 | ``Color(0.95, 0.95, 0.95, 1)``    |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_hover_pressed_color<class_LinkButton_theme_color_font_hover_pressed_color>` | ``Color(0, 0, 0, 1)``             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_outline_color<class_LinkButton_theme_color_font_outline_color>`             | ``Color(0, 0, 0, 1)``             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_pressed_color<class_LinkButton_theme_color_font_pressed_color>`             | ``Color(1, 1, 1, 1)``             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`           | :ref:`outline_size<class_LinkButton_theme_constant_outline_size>`                      | ``0``                             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`           | :ref:`underline_spacing<class_LinkButton_theme_constant_underline_spacing>`            | ``2``                             |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Font<class_Font>`         | :ref:`font<class_LinkButton_theme_font_font>`                                          |                                   |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`           | :ref:`font_size<class_LinkButton_theme_font_size_font_size>`                           |                                   |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`focus<class_LinkButton_theme_style_focus>`                                       |                                   |
   +---------------------------------+----------------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_LinkButton_UnderlineMode:

.. rst-class:: classref-enumeration

enum **UnderlineMode**: :ref:`🔗<enum_LinkButton_UnderlineMode>`

.. _class_LinkButton_constant_UNDERLINE_MODE_ALWAYS:

.. rst-class:: classref-enumeration-constant

:ref:`UnderlineMode<enum_LinkButton_UnderlineMode>` **UNDERLINE_MODE_ALWAYS** = ``0``

LinkButton sẽ luôn hiển thị dấu gạch chân ở phía dưới văn bản.

.. _class_LinkButton_constant_UNDERLINE_MODE_ON_HOVER:

.. rst-class:: classref-enumeration-constant

:ref:`UnderlineMode<enum_LinkButton_UnderlineMode>` **UNDERLINE_MODE_ON_HOVER** = ``1``

LinkButton sẽ hiển thị dấu gạch chân ở phía dưới văn bản khi con trỏ chuột nằm trên nó.

.. _class_LinkButton_constant_UNDERLINE_MODE_NEVER:

.. rst-class:: classref-enumeration-constant

:ref:`UnderlineMode<enum_LinkButton_UnderlineMode>` **UNDERLINE_MODE_NEVER** = ``2``

LinkButton sẽ không bao giờ hiển thị dấu gạch chân ở phía dưới văn bản.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LinkButton_property_ellipsis_char:

.. rst-class:: classref-property

:ref:`String<class_String>` **ellipsis_char** = ``"…"`` :ref:`🔗<class_LinkButton_property_ellipsis_char>`

.. rst-class:: classref-property-setget

- |void| **set_ellipsis_char**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_ellipsis_char**\ (\ )

Ký tự dấu ba chấm được dùng để cắt bớt văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_language:

.. rst-class:: classref-property

:ref:`String<class_String>` **language** = ``""`` :ref:`🔗<class_LinkButton_property_language>`

.. rst-class:: classref-property-setget

- |void| **set_language**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_language**\ (\ )

Mã ngôn ngữ được dùng cho các thuật toán ngắt dòng và định hình văn bản. Nếu để trống, locale hiện tại sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_structured_text_bidi_override:

.. rst-class:: classref-property

:ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **structured_text_bidi_override** = ``0`` :ref:`🔗<class_LinkButton_property_structured_text_bidi_override>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override**\ (\ value\: :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>`\ ) - :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **get_structured_text_bidi_override**\ (\ )

Thiết lập ghi đè thuật toán BiDi cho văn bản có cấu trúc.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_structured_text_bidi_override_options:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **structured_text_bidi_override_options** = ``[]`` :ref:`🔗<class_LinkButton_property_structured_text_bidi_override_options>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override_options**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_structured_text_bidi_override_options**\ (\ )

Thiết lập các tùy chọn bổ sung cho ghi đè BiDi.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **text** = ``""`` :ref:`🔗<class_LinkButton_property_text>`

.. rst-class:: classref-property-setget

- |void| **set_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_text**\ (\ )

Văn bản của nút sẽ được hiển thị bên trong vùng của nút.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_text_direction:

.. rst-class:: classref-property

:ref:`TextDirection<enum_Control_TextDirection>` **text_direction** = ``0`` :ref:`🔗<class_LinkButton_property_text_direction>`

.. rst-class:: classref-property-setget

- |void| **set_text_direction**\ (\ value\: :ref:`TextDirection<enum_Control_TextDirection>`\ ) - :ref:`TextDirection<enum_Control_TextDirection>` **get_text_direction**\ (\ )

Hướng viết cơ bản của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_text_overrun_behavior:

.. rst-class:: classref-property

:ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **text_overrun_behavior** = ``0`` :ref:`🔗<class_LinkButton_property_text_overrun_behavior>`

.. rst-class:: classref-property-setget

- |void| **set_text_overrun_behavior**\ (\ value\: :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`\ ) - :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **get_text_overrun_behavior**\ (\ )

Thiết lập hành vi cắt bớt khi văn bản vượt quá hình chữ nhật bao quanh node.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_underline:

.. rst-class:: classref-property

:ref:`UnderlineMode<enum_LinkButton_UnderlineMode>` **underline** = ``0`` :ref:`🔗<class_LinkButton_property_underline>`

.. rst-class:: classref-property-setget

- |void| **set_underline_mode**\ (\ value\: :ref:`UnderlineMode<enum_LinkButton_UnderlineMode>`\ ) - :ref:`UnderlineMode<enum_LinkButton_UnderlineMode>` **get_underline_mode**\ (\ )

Chế độ gạch chân được sử dụng cho văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_property_uri:

.. rst-class:: classref-property

:ref:`String<class_String>` **uri** = ``""`` :ref:`🔗<class_LinkButton_property_uri>`

.. rst-class:: classref-property-setget

- |void| **set_uri**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_uri**\ (\ )

`URI <https://en.wikipedia.org/wiki/Uniform_Resource_Identifier>`__ của **LinkButton** này. Nếu được đặt thành một URI hợp lệ, việc nhấn nút sẽ mở URI bằng chương trình mặc định của hệ điều hành cho giao thức đó (thông qua :ref:`OS.shell_open()<class_OS_method_shell_open>`). Các URL HTTP và HTTPS sẽ mở trình duyệt web mặc định.


.. tabs::

 .. code-tab:: gdscript

    uri = "https://godotengine.org"  # Mở URL trong trình duyệt web mặc định.
    uri = "C:\SomeFolder"  # Mở trình quản lý tệp tại đường dẫn đã cho.
    uri = "C:\SomeImage.png"  # Mở hình ảnh đã cho trong ứng dụng xem ảnh mặc định.

 .. code-tab:: csharp

    Uri = "https://godotengine.org"; // Mở URL trong trình duyệt web mặc định.
    Uri = "C:\SomeFolder"; // Mở trình quản lý tệp tại đường dẫn đã cho.
    Uri = "C:\SomeImage.png"; // Mở hình ảnh đã cho trong ứng dụng xem ảnh mặc định.



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_LinkButton_theme_color_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_color** = ``Color(0.875, 0.875, 0.875, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_color>`

:ref:`Color<class_Color>` văn bản mặc định của **LinkButton**.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_disabled_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_disabled_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_disabled_color>`

:ref:`Color<class_Color>` văn bản được dùng khi **LinkButton** bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_focus_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_focus_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_focus_color>`

:ref:`Color<class_Color>` văn bản được dùng khi **LinkButton** được focus. Chỉ thay thế màu văn bản thông thường của nút. Các trạng thái bị vô hiệu hóa, hover và nhấn được ưu tiên hơn màu này.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_hover_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_hover_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_hover_color>`

:ref:`Color<class_Color>` văn bản được dùng khi con trỏ đang hover trên **LinkButton**.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_hover_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_hover_pressed_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_hover_pressed_color>`

:ref:`Color<class_Color>` văn bản được dùng khi con trỏ đang hover trên và nút đang được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_outline_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_outline_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_outline_color>`

Màu phủ của viền văn bản của **LinkButton**.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_color_font_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_pressed_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_LinkButton_theme_color_font_pressed_color>`

:ref:`Color<class_Color>` văn bản được dùng khi **LinkButton** đang được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_constant_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_LinkButton_theme_constant_outline_size>`

Kích thước viền văn bản.

\ **Lưu ý:** Nếu sử dụng một font đã bật :ref:`FontFile.multichannel_signed_distance_field<class_FontFile_property_multichannel_signed_distance_field>`, :ref:`FontFile.msdf_pixel_range<class_FontFile_property_msdf_pixel_range>` của font đó phải được đặt ít nhất bằng *hai lần* giá trị của :ref:`outline_size<class_LinkButton_theme_constant_outline_size>` để việc hiển thị viền trông chính xác. Nếu không, viền có thể bị cắt sớm hơn dự kiến.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_constant_underline_spacing:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **underline_spacing** = ``2`` :ref:`🔗<class_LinkButton_theme_constant_underline_spacing>`

Khoảng cách theo chiều dọc giữa đường cơ sở của văn bản và dấu gạch chân.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_font_font:

.. rst-class:: classref-themeproperty

:ref:`Font<class_Font>` **font** :ref:`🔗<class_LinkButton_theme_font_font>`

:ref:`Font<class_Font>` của văn bản của **LinkButton**.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_font_size_font_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **font_size** :ref:`🔗<class_LinkButton_theme_font_size_font_size>`

Cỡ font của văn bản của **LinkButton**.

.. rst-class:: classref-item-separator

----

.. _class_LinkButton_theme_style_focus:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **focus** :ref:`🔗<class_LinkButton_theme_style_focus>`

:ref:`StyleBox<class_StyleBox>` được dùng khi **LinkButton** được focus. :ref:`focus<class_LinkButton_theme_style_focus>` :ref:`StyleBox<class_StyleBox>` được hiển thị *đè lên* :ref:`StyleBox<class_StyleBox>` cơ sở, vì vậy nên sử dụng :ref:`StyleBox<class_StyleBox>` bán trong suốt để đảm bảo :ref:`StyleBox<class_StyleBox>` cơ sở vẫn hiển thị. Một :ref:`StyleBox<class_StyleBox>` đại diện cho viền hoặc dấu gạch chân hoạt động tốt cho mục đích này. Để tắt hiệu ứng trực quan khi focus, hãy gán một tài nguyên :ref:`StyleBoxEmpty<class_StyleBoxEmpty>`. Lưu ý rằng việc tắt hiệu ứng trực quan khi focus sẽ làm giảm khả năng sử dụng của thao tác điều hướng bằng bàn phím/tay cầm, vì vậy không được khuyến nghị vì lý do khả năng tiếp cận.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
