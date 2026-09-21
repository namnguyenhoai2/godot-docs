:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Button.xml.

.. _class_Button:

Nút
===

**Kế thừa:** :ref:`BaseButton<class_BaseButton>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CheckBox<class_CheckBox>`, :ref:`CheckButton<class_CheckButton>`, :ref:`ColorPickerButton<class_ColorPickerButton>`, :ref:`MenuButton<class_MenuButton>`, :ref:`OptionButton<class_OptionButton>`

Một nút theo theme có thể chứa văn bản và biểu tượng.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Button** là nút theo theme tiêu chuẩn. Nó có thể chứa văn bản và biểu tượng, đồng thời sẽ hiển thị chúng theo :ref:`Theme<class_Theme>` hiện tại.

\ **Ví dụ:** Tạo một nút và kết nối một phương thức sẽ được gọi khi nút được nhấn:


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        var button = Button.new()
        button.text = "Click me"
        button.pressed.connect(_button_pressed)
        add_child(button)

    func _button_pressed():
        print("Hello world!")

 .. code-tab:: csharp

    public override void _Ready()
    {
        var button = new Button();
        button.Text = "Click me";
        button.Pressed += ButtonPressed;
        AddChild(button);
    }

    private void ButtonPressed()
    {
        GD.Print("Hello world!");
    }



Xem thêm :ref:`BaseButton<class_BaseButton>`, chứa các thuộc tính và phương thức phổ biến liên quan đến node này.

\ **Lưu ý:** Các nút hỗ trợ multitouch thông qua thao tác chạm, cho phép nhấn nhiều nút cùng lúc. Nếu không, thao tác chuột sẽ được sử dụng, giới hạn tương tác ở một lần nhấn nút tại một thời điểm.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `Operating System Testing Demo <https://godotengine.org/asset-library/asset/2789>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` | :ref:`alignment<class_Button_property_alignment>`                             | ``1``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`                 | :ref:`autowrap_mode<class_Button_property_autowrap_mode>`                     | ``0``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] | :ref:`autowrap_trim_flags<class_Button_property_autowrap_trim_flags>`         | ``128``   |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                           | :ref:`clip_text<class_Button_property_clip_text>`                             | ``false`` |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                           | :ref:`expand_icon<class_Button_property_expand_icon>`                         | ``false`` |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                           | :ref:`flat<class_Button_property_flat>`                                       | ``false`` |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`Texture2D<class_Texture2D>`                                 | :ref:`icon<class_Button_property_icon>`                                       |           |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` | :ref:`icon_alignment<class_Button_property_icon_alignment>`                   | ``0``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`                                       | :ref:`language<class_Button_property_language>`                               | ``""``    |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`                                       | :ref:`text<class_Button_property_text>`                                       | ``""``    |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`TextDirection<enum_Control_TextDirection>`                  | :ref:`text_direction<class_Button_property_text_direction>`                   | ``0``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`           | :ref:`text_overrun_behavior<class_Button_property_text_overrun_behavior>`     | ``0``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`     | :ref:`vertical_icon_alignment<class_Button_property_vertical_icon_alignment>` | ``1``     |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Thuộc tính theme
----------------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_color<class_Button_theme_color_font_color>`                                  | ``Color(0.875, 0.875, 0.875, 1)``   |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_disabled_color<class_Button_theme_color_font_disabled_color>`                | ``Color(0.875, 0.875, 0.875, 0.5)`` |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_focus_color<class_Button_theme_color_font_focus_color>`                      | ``Color(0.95, 0.95, 0.95, 1)``      |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_hover_color<class_Button_theme_color_font_hover_color>`                      | ``Color(0.95, 0.95, 0.95, 1)``      |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_hover_pressed_color<class_Button_theme_color_font_hover_pressed_color>`      | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_outline_color<class_Button_theme_color_font_outline_color>`                  | ``Color(0, 0, 0, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_pressed_color<class_Button_theme_color_font_pressed_color>`                  | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_disabled_color<class_Button_theme_color_icon_disabled_color>`                | ``Color(1, 1, 1, 0.4)``             |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_focus_color<class_Button_theme_color_icon_focus_color>`                      | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_hover_color<class_Button_theme_color_icon_hover_color>`                      | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_hover_pressed_color<class_Button_theme_color_icon_hover_pressed_color>`      | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_normal_color<class_Button_theme_color_icon_normal_color>`                    | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`icon_pressed_color<class_Button_theme_color_icon_pressed_color>`                  | ``Color(1, 1, 1, 1)``               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`align_to_largest_stylebox<class_Button_theme_constant_align_to_largest_stylebox>` | ``0``                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`h_separation<class_Button_theme_constant_h_separation>`                           | ``4``                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`icon_max_width<class_Button_theme_constant_icon_max_width>`                       | ``0``                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`line_spacing<class_Button_theme_constant_line_spacing>`                           | ``0``                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`outline_size<class_Button_theme_constant_outline_size>`                           | ``0``                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Font<class_Font>`           | :ref:`font<class_Button_theme_font_font>`                                               |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`             | :ref:`font_size<class_Button_theme_font_size_font_size>`                                |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`icon<class_Button_theme_icon_icon>`                                               |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`disabled<class_Button_theme_style_disabled>`                                      |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`disabled_mirrored<class_Button_theme_style_disabled_mirrored>`                    |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`focus<class_Button_theme_style_focus>`                                            |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`hover<class_Button_theme_style_hover>`                                            |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`hover_mirrored<class_Button_theme_style_hover_mirrored>`                          |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`hover_pressed<class_Button_theme_style_hover_pressed>`                            |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`hover_pressed_mirrored<class_Button_theme_style_hover_pressed_mirrored>`          |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`normal<class_Button_theme_style_normal>`                                          |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`normal_mirrored<class_Button_theme_style_normal_mirrored>`                        |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`pressed<class_Button_theme_style_pressed>`                                        |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`pressed_mirrored<class_Button_theme_style_pressed_mirrored>`                      |                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------+-------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Button_property_alignment:

.. rst-class:: classref-property

:ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **alignment** = ``1`` :ref:`🔗<class_Button_property_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_text_alignment**\ (\ value\: :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`\ ) - :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **get_text_alignment**\ (\ )

Chính sách căn chỉnh văn bản của nút.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_autowrap_mode:

.. rst-class:: classref-property

:ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **autowrap_mode** = ``0`` :ref:`🔗<class_Button_property_autowrap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_mode**\ (\ value\: :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`\ ) - :ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **get_autowrap_mode**\ (\ )

Nếu được đặt thành giá trị khác :ref:`TextServer.AUTOWRAP_OFF<class_TextServer_constant_AUTOWRAP_OFF>`, văn bản sẽ được ngắt dòng bên trong hình chữ nhật giới hạn của node.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_autowrap_trim_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **autowrap_trim_flags** = ``128`` :ref:`🔗<class_Button_property_autowrap_trim_flags>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_trim_flags**\ (\ value\: |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\]\ ) - |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **get_autowrap_trim_flags**\ (\ )

Các cờ cắt khoảng trắng khi ngắt dòng tự động. Xem :ref:`TextServer.BREAK_TRIM_START_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_START_EDGE_SPACES>` và :ref:`TextServer.BREAK_TRIM_END_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_END_EDGE_SPACES>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_clip_text:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **clip_text** = ``false`` :ref:`🔗<class_Button_property_clip_text>`

.. rst-class:: classref-property-setget

- |void| **set_clip_text**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_clip_text**\ (\ )

Nếu ``true``, văn bản quá lớn không thể vừa với nút sẽ bị cắt theo chiều ngang. Nếu ``false``, nút sẽ luôn đủ rộng để chứa văn bản. Văn bản không bị cắt theo chiều dọc và chiều cao của nút không bị ảnh hưởng bởi thuộc tính này.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_expand_icon:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **expand_icon** = ``false`` :ref:`🔗<class_Button_property_expand_icon>`

.. rst-class:: classref-property-setget

- |void| **set_expand_icon**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_expand_icon**\ (\ )

Khi được bật, biểu tượng của nút sẽ phóng to/thu nhỏ để vừa với kích thước nút nhưng vẫn giữ nguyên tỷ lệ. Xem thêm :ref:`icon_max_width<class_Button_theme_constant_icon_max_width>`.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_flat:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **flat** = ``false`` :ref:`🔗<class_Button_property_flat>`

.. rst-class:: classref-property-setget

- |void| **set_flat**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_flat**\ (\ )

Các nút phẳng không hiển thị phần trang trí.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_icon:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **icon** :ref:`🔗<class_Button_property_icon>`

.. rst-class:: classref-property-setget

- |void| **set_button_icon**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_button_icon**\ (\ )

Biểu tượng của nút; nếu có văn bản, biểu tượng sẽ được đặt trước văn bản.

Để chỉnh sửa lề và khoảng cách của biểu tượng, hãy sử dụng thuộc tính theme :ref:`h_separation<class_Button_theme_constant_h_separation>` và các thuộc tính ``content_margin_*`` của :ref:`StyleBox<class_StyleBox>` được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_icon_alignment:

.. rst-class:: classref-property

:ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **icon_alignment** = ``0`` :ref:`🔗<class_Button_property_icon_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_icon_alignment**\ (\ value\: :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`\ ) - :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **get_icon_alignment**\ (\ )

Xác định biểu tượng sẽ được căn theo chiều ngang về bên trái, bên phải hay ở giữa nút. Sử dụng cùng các hằng số :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` như căn chỉnh văn bản. Nếu được căn giữa theo cả chiều ngang và chiều dọc, văn bản sẽ được vẽ bên trên biểu tượng.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_language:

.. rst-class:: classref-property

:ref:`String<class_String>` **language** = ``""`` :ref:`🔗<class_Button_property_language>`

.. rst-class:: classref-property-setget

- |void| **set_language**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_language**\ (\ )

Mã ngôn ngữ được sử dụng cho các thuật toán ngắt dòng và định hình văn bản. Nếu để trống, locale hiện tại sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **text** = ``""`` :ref:`🔗<class_Button_property_text>`

.. rst-class:: classref-property-setget

- |void| **set_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_text**\ (\ )

Văn bản của nút sẽ được hiển thị bên trong vùng của nút.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_text_direction:

.. rst-class:: classref-property

:ref:`TextDirection<enum_Control_TextDirection>` **text_direction** = ``0`` :ref:`🔗<class_Button_property_text_direction>`

.. rst-class:: classref-property-setget

- |void| **set_text_direction**\ (\ value\: :ref:`TextDirection<enum_Control_TextDirection>`\ ) - :ref:`TextDirection<enum_Control_TextDirection>` **get_text_direction**\ (\ )

Hướng viết cơ bản của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_text_overrun_behavior:

.. rst-class:: classref-property

:ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **text_overrun_behavior** = ``0`` :ref:`🔗<class_Button_property_text_overrun_behavior>`

.. rst-class:: classref-property-setget

- |void| **set_text_overrun_behavior**\ (\ value\: :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`\ ) - :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **get_text_overrun_behavior**\ (\ )

Thiết lập cách cắt khi văn bản vượt quá hình chữ nhật giới hạn của node.

.. rst-class:: classref-item-separator

----

.. _class_Button_property_vertical_icon_alignment:

.. rst-class:: classref-property

:ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **vertical_icon_alignment** = ``1`` :ref:`🔗<class_Button_property_vertical_icon_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_vertical_icon_alignment**\ (\ value\: :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`\ ) - :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **get_vertical_icon_alignment**\ (\ )

Xác định biểu tượng sẽ được căn theo chiều dọc lên trên, xuống dưới hay ở giữa nút. Sử dụng cùng các hằng số :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` như căn chỉnh văn bản. Nếu được căn giữa theo cả chiều ngang và chiều dọc, văn bản sẽ được vẽ bên trên biểu tượng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính theme
----------------------

.. _class_Button_theme_color_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_color** = ``Color(0.875, 0.875, 0.875, 1)`` :ref:`🔗<class_Button_theme_color_font_color>`

:ref:`Color<class_Color>` văn bản mặc định của **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_disabled_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_disabled_color** = ``Color(0.875, 0.875, 0.875, 0.5)`` :ref:`🔗<class_Button_theme_color_font_disabled_color>`

:ref:`Color<class_Color>` văn bản được sử dụng khi **Button** bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_focus_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_focus_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_Button_theme_color_font_focus_color>`

:ref:`Color<class_Color>` văn bản được sử dụng khi **Button** được focus. Chỉ thay thế màu văn bản thông thường của nút. Các trạng thái bị vô hiệu hóa, di chuột và được nhấn sẽ được ưu tiên hơn màu này.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_hover_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_hover_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_Button_theme_color_font_hover_color>`

:ref:`Color<class_Color>` văn bản được sử dụng khi di chuột lên **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_hover_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_hover_pressed_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_font_hover_pressed_color>`

:ref:`Color<class_Color>` văn bản được sử dụng khi di chuột lên **Button** và nhấn nút.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_outline_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_outline_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_Button_theme_color_font_outline_color>`

Màu sắc đường viền văn bản của **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_font_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_pressed_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_font_pressed_color>`

:ref:`Color<class_Color>` văn bản được sử dụng khi **Button** đang được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_disabled_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_disabled_color** = ``Color(1, 1, 1, 0.4)`` :ref:`🔗<class_Button_theme_color_icon_disabled_color>`

:ref:`Color<class_Color>` điều biến biểu tượng được sử dụng khi **Button** bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_focus_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_focus_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_icon_focus_color>`

:ref:`Color<class_Color>` điều biến biểu tượng được sử dụng khi **Button** được focus. Chỉ thay thế màu điều biến thông thường của nút. Các trạng thái bị vô hiệu hóa, di chuột và được nhấn sẽ được ưu tiên hơn màu này.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_hover_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_hover_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_icon_hover_color>`

:ref:`Color<class_Color>` điều biến biểu tượng được sử dụng khi di chuột lên **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_hover_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_hover_pressed_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_icon_hover_pressed_color>`

:ref:`Color<class_Color>` điều biến biểu tượng được sử dụng khi di chuột lên **Button** và nhấn nút.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_normal_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_normal_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_icon_normal_color>`

:ref:`Color<class_Color>` điều biến biểu tượng mặc định của **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_color_icon_pressed_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **icon_pressed_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Button_theme_color_icon_pressed_color>`

:ref:`Color<class_Color>` điều biến biểu tượng được sử dụng khi **Button** đang được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_constant_align_to_largest_stylebox:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **align_to_largest_stylebox** = ``0`` :ref:`🔗<class_Button_theme_constant_align_to_largest_stylebox>`

Hằng số này hoạt động như một boolean. Nếu ``true``, kích thước tối thiểu của nút và việc căn chỉnh văn bản/biểu tượng luôn dựa trên các lề stylebox lớn nhất; nếu không, chúng dựa trên các lề stylebox của trạng thái nút hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_constant_h_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **h_separation** = ``4`` :ref:`🔗<class_Button_theme_constant_h_separation>`

Khoảng cách theo chiều ngang giữa biểu tượng và văn bản của **Button**. Các giá trị âm sẽ được coi là ``0`` khi được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_constant_icon_max_width:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **icon_max_width** = ``0`` :ref:`🔗<class_Button_theme_constant_icon_max_width>`

Chiều rộng tối đa cho phép của biểu tượng **Button**. Giới hạn này được áp dụng trên kích thước mặc định của biểu tượng hoặc kích thước mở rộng của nó nếu :ref:`expand_icon<class_Button_property_expand_icon>` là ``true``. Chiều cao được điều chỉnh theo tỷ lệ của biểu tượng. Nếu nút có các biểu tượng bổ sung (ví dụ: :ref:`CheckBox<class_CheckBox>`), chúng cũng sẽ bị giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_constant_line_spacing:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **line_spacing** = ``0`` :ref:`🔗<class_Button_theme_constant_line_spacing>`

Khoảng cách dọc bổ sung giữa các dòng (tính bằng pixel); khoảng cách được cộng vào độ hạ dòng. Giá trị này có thể là số âm.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_constant_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_Button_theme_constant_outline_size>`

Kích thước đường viền văn bản.

\ **Lưu ý:** Nếu sử dụng font có bật :ref:`FontFile.multichannel_signed_distance_field<class_FontFile_property_multichannel_signed_distance_field>`, :ref:`FontFile.msdf_pixel_range<class_FontFile_property_msdf_pixel_range>` của font đó phải được đặt ít nhất bằng *hai lần* giá trị của :ref:`outline_size<class_Button_theme_constant_outline_size>` để việc hiển thị đường viền trông chính xác. Nếu không, đường viền có thể bị cắt sớm hơn dự kiến.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_font_font:

.. rst-class:: classref-themeproperty

:ref:`Font<class_Font>` **font** :ref:`🔗<class_Button_theme_font_font>`

:ref:`Font<class_Font>` of the **Button**'s text.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_font_size_font_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **font_size** :ref:`🔗<class_Button_theme_font_size_font_size>`

Cỡ font của văn bản **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_icon_icon:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **icon** :ref:`🔗<class_Button_theme_icon_icon>`

Biểu tượng mặc định cho **Button**. Chỉ xuất hiện nếu :ref:`icon<class_Button_property_icon>` chưa được gán.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_disabled:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **disabled** :ref:`🔗<class_Button_theme_style_disabled>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is disabled.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_disabled_mirrored:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **disabled_mirrored** :ref:`🔗<class_Button_theme_style_disabled_mirrored>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is disabled (for right-to-left layouts).

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_focus:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **focus** :ref:`🔗<class_Button_theme_style_focus>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is focused. The :ref:`focus<class_Button_theme_style_focus>` :ref:`StyleBox<class_StyleBox>` is displayed *over* the base :ref:`StyleBox<class_StyleBox>`, so a partially transparent :ref:`StyleBox<class_StyleBox>` should be used to ensure the base :ref:`StyleBox<class_StyleBox>` remains visible. A :ref:`StyleBox<class_StyleBox>` that represents an outline or an underline works well for this purpose. To disable the focus visual effect, assign a :ref:`StyleBoxEmpty<class_StyleBoxEmpty>` resource. Note that disabling the focus visual effect will harm keyboard/controller navigation usability, so this is not recommended for accessibility reasons.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_hover:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **hover** :ref:`🔗<class_Button_theme_style_hover>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being hovered.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_hover_mirrored:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **hover_mirrored** :ref:`🔗<class_Button_theme_style_hover_mirrored>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being hovered (for right-to-left layouts).

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_hover_pressed:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **hover_pressed** :ref:`🔗<class_Button_theme_style_hover_pressed>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being pressed and hovered at the same time.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_hover_pressed_mirrored:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **hover_pressed_mirrored** :ref:`🔗<class_Button_theme_style_hover_pressed_mirrored>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being pressed and hovered at the same time (for right-to-left layouts).

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_normal:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **normal** :ref:`🔗<class_Button_theme_style_normal>`

:ref:`StyleBox<class_StyleBox>` mặc định cho **Button**.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_normal_mirrored:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **normal_mirrored** :ref:`🔗<class_Button_theme_style_normal_mirrored>`

:ref:`StyleBox<class_StyleBox>` mặc định cho **Button** (dành cho bố cục từ phải sang trái).

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_pressed:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **pressed** :ref:`🔗<class_Button_theme_style_pressed>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being pressed.

.. rst-class:: classref-item-separator

----

.. _class_Button_theme_style_pressed_mirrored:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **pressed_mirrored** :ref:`🔗<class_Button_theme_style_pressed_mirrored>`

:ref:`StyleBox<class_StyleBox>` used when the **Button** is being pressed (for right-to-left layouts).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
