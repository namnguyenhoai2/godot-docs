:github_url: hide

.. meta::
	:keywords: expandable, collapsible, collapse, accordion, details

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FoldableContainer.xml.

.. _class_FoldableContainer:

FoldableContainer
=================

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một container có thể mở rộng/thu gọn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một container có thể mở rộng/thu gọn, với tiêu đề có thể chứa các control, chẳng hạn như nút. Đây còn được gọi là accordion.

Tiêu đề có thể được đặt ở phía trên hoặc phía dưới container. Có thể mở rộng hoặc thu gọn container bằng cách nhấp vào tiêu đề hoặc nhấn ``ui_accept`` khi tiêu đề được focus. Các node control con sẽ bị ẩn khi container được thu gọn. Bỏ qua các node không phải control.

Có thể nhóm một FoldableContainer với các FoldableContainer khác để chỉ một trong số chúng được mở tại một thời điểm; xem :ref:`foldable_group<class_FoldableContainer_property_foldable_group>` và :ref:`FoldableGroup<class_FoldableGroup>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`                          | focus_mode                                                                                       | ``2`` (overrides :ref:`Control<class_Control_property_focus_mode>`)   |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`FoldableGroup<class_FoldableGroup>`                         | :ref:`foldable_group<class_FoldableContainer_property_foldable_group>`                           |                                                                       |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`folded<class_FoldableContainer_property_folded>`                                           | ``false``                                                             |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`language<class_FoldableContainer_property_language>`                                       | ``""``                                                                |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>`                      | mouse_filter                                                                                     | ``0`` (overrides :ref:`Control<class_Control_property_mouse_filter>`) |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`title<class_FoldableContainer_property_title>`                                             | ``""``                                                                |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` | :ref:`title_alignment<class_FoldableContainer_property_title_alignment>`                         | ``0``                                                                 |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`TitlePosition<enum_FoldableContainer_TitlePosition>`        | :ref:`title_position<class_FoldableContainer_property_title_position>`                           | ``0``                                                                 |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`TextDirection<enum_Control_TextDirection>`                  | :ref:`title_text_direction<class_FoldableContainer_property_title_text_direction>`               | ``0``                                                                 |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`           | :ref:`title_text_overrun_behavior<class_FoldableContainer_property_title_text_overrun_behavior>` | ``0``                                                                 |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_title_bar_control<class_FoldableContainer_method_add_title_bar_control>`\ (\ control\: :ref:`Control<class_Control>`\ )       |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`expand<class_FoldableContainer_method_expand>`\ (\ )                                                                              |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`fold<class_FoldableContainer_method_fold>`\ (\ )                                                                                  |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`remove_title_bar_control<class_FoldableContainer_method_remove_title_bar_control>`\ (\ control\: :ref:`Control<class_Control>`\ ) |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`collapsed_font_color<class_FoldableContainer_theme_color_collapsed_font_color>`               | ``Color(1, 1, 1, 1)``             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_color<class_FoldableContainer_theme_color_font_color>`                                   | ``Color(0.875, 0.875, 0.875, 1)`` |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`font_outline_color<class_FoldableContainer_theme_color_font_outline_color>`                   | ``Color(1, 1, 1, 1)``             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`         | :ref:`hover_font_color<class_FoldableContainer_theme_color_hover_font_color>`                       | ``Color(0.95, 0.95, 0.95, 1)``    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`             | :ref:`h_separation<class_FoldableContainer_theme_constant_h_separation>`                            | ``2``                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`             | :ref:`outline_size<class_FoldableContainer_theme_constant_outline_size>`                            | ``0``                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Font<class_Font>`           | :ref:`font<class_FoldableContainer_theme_font_font>`                                                |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`             | :ref:`font_size<class_FoldableContainer_theme_font_size_font_size>`                                 |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`expanded_arrow<class_FoldableContainer_theme_icon_expanded_arrow>`                            |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`expanded_arrow_mirrored<class_FoldableContainer_theme_icon_expanded_arrow_mirrored>`          |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`folded_arrow<class_FoldableContainer_theme_icon_folded_arrow>`                                |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`folded_arrow_mirrored<class_FoldableContainer_theme_icon_folded_arrow_mirrored>`              |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`focus<class_FoldableContainer_theme_style_focus>`                                             |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`panel<class_FoldableContainer_theme_style_panel>`                                             |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`title_collapsed_hover_panel<class_FoldableContainer_theme_style_title_collapsed_hover_panel>` |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`title_collapsed_panel<class_FoldableContainer_theme_style_title_collapsed_panel>`             |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`title_hover_panel<class_FoldableContainer_theme_style_title_hover_panel>`                     |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>`   | :ref:`title_panel<class_FoldableContainer_theme_style_title_panel>`                                 |                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_FoldableContainer_signal_folding_changed:

.. rst-class:: classref-signal

**folding_changed**\ (\ is_folded\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_FoldableContainer_signal_folding_changed>`

Được phát ra khi container được thu gọn/mở rộng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_FoldableContainer_TitlePosition:

.. rst-class:: classref-enumeration

enum **TitlePosition**: :ref:`🔗<enum_FoldableContainer_TitlePosition>`

.. _class_FoldableContainer_constant_POSITION_TOP:

.. rst-class:: classref-enumeration-constant

:ref:`TitlePosition<enum_FoldableContainer_TitlePosition>` **POSITION_TOP** = ``0``

Đặt tiêu đề ở phía trên container.

.. _class_FoldableContainer_constant_POSITION_BOTTOM:

.. rst-class:: classref-enumeration-constant

:ref:`TitlePosition<enum_FoldableContainer_TitlePosition>` **POSITION_BOTTOM** = ``1``

Đặt tiêu đề ở phía dưới container. Đồng thời lật dọc tất cả StyleBox.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FoldableContainer_property_foldable_group:

.. rst-class:: classref-property

:ref:`FoldableGroup<class_FoldableGroup>` **foldable_group** :ref:`🔗<class_FoldableContainer_property_foldable_group>`

.. rst-class:: classref-property-setget

- |void| **set_foldable_group**\ (\ value\: :ref:`FoldableGroup<class_FoldableGroup>`\ ) - :ref:`FoldableGroup<class_FoldableGroup>` **get_foldable_group**\ (\ )

:ref:`FoldableGroup<class_FoldableGroup>` được liên kết với container. Khi nhiều node **FoldableContainer** dùng chung một group, chỉ một node trong số đó được phép mở.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_folded:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **folded** = ``false`` :ref:`🔗<class_FoldableContainer_property_folded>`

.. rst-class:: classref-property-setget

- |void| **set_folded**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_folded**\ (\ )

Nếu ``true``, container sẽ được thu gọn và ẩn tất cả các node con.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_language:

.. rst-class:: classref-property

:ref:`String<class_String>` **language** = ``""`` :ref:`🔗<class_FoldableContainer_property_language>`

.. rst-class:: classref-property-setget

- |void| **set_language**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_language**\ (\ )

Mã ngôn ngữ được dùng cho các thuật toán định hình văn bản. Nếu để trống, locale hiện tại sẽ được dùng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_title:

.. rst-class:: classref-property

:ref:`String<class_String>` **title** = ``""`` :ref:`🔗<class_FoldableContainer_property_title>`

.. rst-class:: classref-property-setget

- |void| **set_title**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_title**\ (\ )

Văn bản tiêu đề của container.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_title_alignment:

.. rst-class:: classref-property

:ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **title_alignment** = ``0`` :ref:`🔗<class_FoldableContainer_property_title_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_title_alignment**\ (\ value\: :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`\ ) - :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **get_title_alignment**\ (\ )

Căn chỉnh văn bản theo chiều ngang của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_title_position:

.. rst-class:: classref-property

:ref:`TitlePosition<enum_FoldableContainer_TitlePosition>` **title_position** = ``0`` :ref:`🔗<class_FoldableContainer_property_title_position>`

.. rst-class:: classref-property-setget

- |void| **set_title_position**\ (\ value\: :ref:`TitlePosition<enum_FoldableContainer_TitlePosition>`\ ) - :ref:`TitlePosition<enum_FoldableContainer_TitlePosition>` **get_title_position**\ (\ )

Vị trí của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_title_text_direction:

.. rst-class:: classref-property

:ref:`TextDirection<enum_Control_TextDirection>` **title_text_direction** = ``0`` :ref:`🔗<class_FoldableContainer_property_title_text_direction>`

.. rst-class:: classref-property-setget

- |void| **set_title_text_direction**\ (\ value\: :ref:`TextDirection<enum_Control_TextDirection>`\ ) - :ref:`TextDirection<enum_Control_TextDirection>` **get_title_text_direction**\ (\ )

Hướng viết văn bản của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_property_title_text_overrun_behavior:

.. rst-class:: classref-property

:ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **title_text_overrun_behavior** = ``0`` :ref:`🔗<class_FoldableContainer_property_title_text_overrun_behavior>`

.. rst-class:: classref-property-setget

- |void| **set_title_text_overrun_behavior**\ (\ value\: :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`\ ) - :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **get_title_text_overrun_behavior**\ (\ )

Xác định hành vi của tiêu đề khi văn bản dài hơn không gian khả dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_FoldableContainer_method_add_title_bar_control:

.. rst-class:: classref-method

|void| **add_title_bar_control**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_FoldableContainer_method_add_title_bar_control>`

Thêm một :ref:`Control<class_Control>` được đặt bên cạnh tiêu đề của container, che khuất vùng có thể nhấp. Mục đích sử dụng chính là thêm các node :ref:`Button<class_Button>`, nhưng có thể là bất kỳ :ref:`Control<class_Control>` nào.

Control sẽ được thêm làm node con của container này và được xóa khỏi parent trước đó nếu cần. Các control sẽ được đặt căn phải, trong đó control được thêm đầu tiên nằm ngoài cùng bên trái.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_method_expand:

.. rst-class:: classref-method

|void| **expand**\ (\ ) :ref:`🔗<class_FoldableContainer_method_expand>`

Mở rộng container và phát ra :ref:`folding_changed<class_FoldableContainer_signal_folding_changed>`.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_method_fold:

.. rst-class:: classref-method

|void| **fold**\ (\ ) :ref:`🔗<class_FoldableContainer_method_fold>`

Thu gọn container và phát ra :ref:`folding_changed<class_FoldableContainer_signal_folding_changed>`.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_method_remove_title_bar_control:

.. rst-class:: classref-method

|void| **remove_title_bar_control**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_FoldableContainer_method_remove_title_bar_control>`

Xóa một :ref:`Control<class_Control>` đã được thêm bằng :ref:`add_title_bar_control()<class_FoldableContainer_method_add_title_bar_control>`. Node này không được tự động giải phóng; bạn cần sử dụng :ref:`Node.queue_free()<class_Node_method_queue_free>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_FoldableContainer_theme_color_collapsed_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **collapsed_font_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_FoldableContainer_theme_color_collapsed_font_color>`

Màu font của tiêu đề khi được thu gọn.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_color_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_color** = ``Color(0.875, 0.875, 0.875, 1)`` :ref:`🔗<class_FoldableContainer_theme_color_font_color>`

Màu font của tiêu đề khi được mở rộng.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_color_font_outline_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_outline_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_FoldableContainer_theme_color_font_outline_color>`

Màu viền font của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_color_hover_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **hover_font_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_FoldableContainer_theme_color_hover_font_color>`

Màu hover của font tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_constant_h_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **h_separation** = ``2`` :ref:`🔗<class_FoldableContainer_theme_constant_h_separation>`

Khoảng cách theo chiều ngang giữa icon và văn bản của tiêu đề, cũng như giữa các control trên thanh tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_constant_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_FoldableContainer_theme_constant_outline_size>`

Kích thước viền font của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_font_font:

.. rst-class:: classref-themeproperty

:ref:`Font<class_Font>` **font** :ref:`🔗<class_FoldableContainer_theme_font_font>`

Font của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_font_size_font_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **font_size** :ref:`🔗<class_FoldableContainer_theme_font_size_font_size>`

Kích thước font của tiêu đề.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_icon_expanded_arrow:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **expanded_arrow** :ref:`🔗<class_FoldableContainer_theme_icon_expanded_arrow>`

Icon của tiêu đề được dùng khi mở rộng.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_icon_expanded_arrow_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **expanded_arrow_mirrored** :ref:`🔗<class_FoldableContainer_theme_icon_expanded_arrow_mirrored>`

Icon của tiêu đề được dùng khi mở rộng (đối với tiêu đề ở phía dưới).

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_icon_folded_arrow:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **folded_arrow** :ref:`🔗<class_FoldableContainer_theme_icon_folded_arrow>`

Icon của tiêu đề được dùng khi thu gọn (đối với bố cục từ trái sang phải).

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_icon_folded_arrow_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **folded_arrow_mirrored** :ref:`🔗<class_FoldableContainer_theme_icon_folded_arrow_mirrored>`

Icon của tiêu đề được dùng khi thu gọn (đối với bố cục từ phải sang trái).

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_focus:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **focus** :ref:`🔗<class_FoldableContainer_theme_style_focus>`

Nền được dùng khi **FoldableContainer** có focus GUI. :ref:`focus<class_FoldableContainer_theme_style_focus>` :ref:`StyleBox<class_StyleBox>` được hiển thị *bên trên* :ref:`StyleBox<class_StyleBox>` cơ sở, vì vậy nên sử dụng :ref:`StyleBox<class_StyleBox>` bán trong suốt để đảm bảo :ref:`StyleBox<class_StyleBox>` cơ sở vẫn hiển thị. Một :ref:`StyleBox<class_StyleBox>` biểu thị viền hoặc gạch chân phù hợp với mục đích này. Để tắt hiệu ứng hình ảnh focus, hãy gán tài nguyên :ref:`StyleBoxEmpty<class_StyleBoxEmpty>`. Lưu ý rằng việc tắt hiệu ứng hình ảnh focus sẽ làm giảm khả năng sử dụng của thao tác điều hướng bằng bàn phím/controller, vì vậy không nên làm vậy vì lý do khả năng tiếp cận.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **panel** :ref:`🔗<class_FoldableContainer_theme_style_panel>`

Nền mặc định cho **FoldableContainer**.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_title_collapsed_hover_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **title_collapsed_hover_panel** :ref:`🔗<class_FoldableContainer_theme_style_title_collapsed_hover_panel>`

Nền được dùng khi con trỏ chuột đi vào vùng tiêu đề lúc container được thu gọn.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_title_collapsed_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **title_collapsed_panel** :ref:`🔗<class_FoldableContainer_theme_style_title_collapsed_panel>`

Nền mặc định cho tiêu đề của **FoldableContainer** khi được thu gọn.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_title_hover_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **title_hover_panel** :ref:`🔗<class_FoldableContainer_theme_style_title_hover_panel>`

Nền được dùng khi con trỏ chuột đi vào vùng tiêu đề lúc container được mở rộng.

.. rst-class:: classref-item-separator

----

.. _class_FoldableContainer_theme_style_title_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **title_panel** :ref:`🔗<class_FoldableContainer_theme_style_title_panel>`

Nền mặc định cho tiêu đề của **FoldableContainer** khi được mở rộng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
