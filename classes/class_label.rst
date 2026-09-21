:github_url: hide

.. meta::
	:keywords: text

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Label.xml.

.. _class_Label:

Label
=====

**Kế thừa:** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một control dùng để hiển thị văn bản thuần túy.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một control dùng để hiển thị văn bản thuần túy. Nó cho phép bạn điều khiển căn chỉnh theo chiều ngang và chiều dọc, đồng thời có thể ngắt dòng văn bản bên trong hình chữ nhật giới hạn của node. Nó không hỗ trợ định dạng văn bản in đậm, in nghiêng hoặc định dạng văn bản đa dạng khác. Để làm điều đó, hãy sử dụng :ref:`RichTextLabel<class_RichTextLabel>` thay thế.

\ **Lưu ý:** Một node Label duy nhất không được thiết kế để hiển thị lượng văn bản khổng lồ. Để hiển thị lượng văn bản lớn trong một node duy nhất, hãy cân nhắc sử dụng :ref:`RichTextLabel<class_RichTextLabel>` thay thế vì nó hỗ trợ các tính năng như thanh cuộn tích hợp và threading. :ref:`RichTextLabel<class_RichTextLabel>` nhìn chung hoạt động tốt hơn khi hiển thị lượng văn bản lớn (vài trang trở lên).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`                           | :ref:`autowrap_mode<class_Label_property_autowrap_mode>`                                                 | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\]           | :ref:`autowrap_trim_flags<class_Label_property_autowrap_trim_flags>`                                     | ``192``                                                                      |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                     | :ref:`clip_text<class_Label_property_clip_text>`                                                         | ``false``                                                                    |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                 | :ref:`ellipsis_char<class_Label_property_ellipsis_char>`                                                 | ``"…"``                                                                      |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`           | :ref:`horizontal_alignment<class_Label_property_horizontal_alignment>`                                   | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\]   | :ref:`justification_flags<class_Label_property_justification_flags>`                                     | ``163``                                                                      |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`LabelSettings<class_LabelSettings>`                                   | :ref:`label_settings<class_Label_property_label_settings>`                                               |                                                                              |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                 | :ref:`language<class_Label_property_language>`                                                           | ``""``                                                                       |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                       | :ref:`lines_skipped<class_Label_property_lines_skipped>`                                                 | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                       | :ref:`max_lines_visible<class_Label_property_max_lines_visible>`                                         | ``-1``                                                                       |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>`                                | mouse_filter                                                                                             | ``2`` (overrides :ref:`Control<class_Control_property_mouse_filter>`)        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                 | :ref:`paragraph_separator<class_Label_property_paragraph_separator>`                                     | ``"\\n"``                                                                    |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\]                      | size_flags_vertical                                                                                      | ``4`` (overrides :ref:`Control<class_Control_property_size_flags_vertical>`) |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>`           | :ref:`structured_text_bidi_override<class_Label_property_structured_text_bidi_override>`                 | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                   | :ref:`structured_text_bidi_override_options<class_Label_property_structured_text_bidi_override_options>` | ``[]``                                                                       |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`                         | :ref:`tab_stops<class_Label_property_tab_stops>`                                                         | ``PackedFloat32Array()``                                                     |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                 | :ref:`text<class_Label_property_text>`                                                                   | ``""``                                                                       |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`TextDirection<enum_Control_TextDirection>`                            | :ref:`text_direction<class_Label_property_text_direction>`                                               | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`                     | :ref:`text_overrun_behavior<class_Label_property_text_overrun_behavior>`                                 | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                     | :ref:`uppercase<class_Label_property_uppercase>`                                                         | ``false``                                                                    |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`               | :ref:`vertical_alignment<class_Label_property_vertical_alignment>`                                       | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                       | :ref:`visible_characters<class_Label_property_visible_characters>`                                       | ``-1``                                                                       |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`VisibleCharactersBehavior<enum_TextServer_VisibleCharactersBehavior>` | :ref:`visible_characters_behavior<class_Label_property_visible_characters_behavior>`                     | ``0``                                                                        |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                   | :ref:`visible_ratio<class_Label_property_visible_ratio>`                                                 | ``1.0``                                                                      |
   +-----------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>` | :ref:`get_character_bounds<class_Label_method_get_character_bounds>`\ (\ pos\: :ref:`int<class_int>`\ ) |const| |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_line_count<class_Label_method_get_line_count>`\ (\ ) |const|                                          |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_line_height<class_Label_method_get_line_height>`\ (\ line\: :ref:`int<class_int>` = -1\ ) |const|     |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_total_character_count<class_Label_method_get_total_character_count>`\ (\ ) |const|                    |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_visible_line_count<class_Label_method_get_visible_line_count>`\ (\ ) |const|                          |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các thuộc tính theme
--------------------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_color<class_Label_theme_color_font_color>`                      | ``Color(1, 1, 1, 1)`` |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_outline_color<class_Label_theme_color_font_outline_color>`      | ``Color(0, 0, 0, 1)`` |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_shadow_color<class_Label_theme_color_font_shadow_color>`        | ``Color(0, 0, 0, 0)`` |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`line_spacing<class_Label_theme_constant_line_spacing>`               | ``3``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`outline_size<class_Label_theme_constant_outline_size>`               | ``0``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`paragraph_spacing<class_Label_theme_constant_paragraph_spacing>`     | ``0``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`shadow_offset_x<class_Label_theme_constant_shadow_offset_x>`         | ``1``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`shadow_offset_y<class_Label_theme_constant_shadow_offset_y>`         | ``1``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`shadow_outline_size<class_Label_theme_constant_shadow_outline_size>` | ``1``                 |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Font<class_Font>`         | :ref:`font<class_Label_theme_font_font>`                                   |                       |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`           | :ref:`font_size<class_Label_theme_font_size_font_size>`                    |                       |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`focus<class_Label_theme_style_focus>`                                |                       |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`normal<class_Label_theme_style_normal>`                              |                       |
   +---------------------------------+----------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Label_property_autowrap_mode:

.. rst-class:: classref-property

:ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **autowrap_mode** = ``0`` :ref:`🔗<class_Label_property_autowrap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_mode**\ (\ value\: :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`\ ) - :ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **get_autowrap_mode**\ (\ )

Nếu được đặt thành giá trị khác :ref:`TextServer.AUTOWRAP_OFF<class_TextServer_constant_AUTOWRAP_OFF>`, văn bản sẽ được ngắt dòng bên trong hình chữ nhật giới hạn của node. Nếu bạn thay đổi kích thước node, chiều cao của node sẽ tự động thay đổi để hiển thị toàn bộ văn bản.

\ **Lưu ý:** Các Label bật tính năng tự động ngắt dòng phải được cấu hình chiều rộng tối đa tùy chỉnh để hoạt động chính xác, thông qua :ref:`Control.custom_maximum_size<class_Control_property_custom_maximum_size>` của chính Label hoặc do kích thước tối đa được truyền từ một Control cha có bật :ref:`Control.propagate_maximum_size<class_Control_property_propagate_maximum_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_autowrap_trim_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **autowrap_trim_flags** = ``192`` :ref:`🔗<class_Label_property_autowrap_trim_flags>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_trim_flags**\ (\ value\: |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\]\ ) - |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **get_autowrap_trim_flags**\ (\ )

Các cờ cắt khoảng trắng khi tự động ngắt dòng. Xem :ref:`TextServer.BREAK_TRIM_START_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_START_EDGE_SPACES>` và :ref:`TextServer.BREAK_TRIM_END_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_END_EDGE_SPACES>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_clip_text:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **clip_text** = ``false`` :ref:`🔗<class_Label_property_clip_text>`

.. rst-class:: classref-property-setget

- |void| **set_clip_text**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_clipping_text**\ (\ )

Nếu ``true``, Label chỉ hiển thị phần văn bản vừa với hình chữ nhật giới hạn của nó và sẽ cắt văn bản theo chiều ngang.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_ellipsis_char:

.. rst-class:: classref-property

:ref:`String<class_String>` **ellipsis_char** = ``"…"`` :ref:`🔗<class_Label_property_ellipsis_char>`

.. rst-class:: classref-property-setget

- |void| **set_ellipsis_char**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_ellipsis_char**\ (\ )

Ký tự dấu ba chấm được sử dụng để cắt văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_horizontal_alignment:

.. rst-class:: classref-property

:ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **horizontal_alignment** = ``0`` :ref:`🔗<class_Label_property_horizontal_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_horizontal_alignment**\ (\ value\: :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`\ ) - :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **get_horizontal_alignment**\ (\ )

Điều khiển căn chỉnh văn bản theo chiều ngang. Hỗ trợ trái, giữa, phải và lấp đầy (còn gọi là justify).

.. rst-class:: classref-item-separator

----

.. _class_Label_property_justification_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\] **justification_flags** = ``163`` :ref:`🔗<class_Label_property_justification_flags>`

.. rst-class:: classref-property-setget

- |void| **set_justification_flags**\ (\ value\: |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\]\ ) - |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\] **get_justification_flags**\ (\ )

Các quy tắc căn chỉnh để lấp đầy dòng.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_label_settings:

.. rst-class:: classref-property

:ref:`LabelSettings<class_LabelSettings>` **label_settings** :ref:`🔗<class_Label_property_label_settings>`

.. rst-class:: classref-property-setget

- |void| **set_label_settings**\ (\ value\: :ref:`LabelSettings<class_LabelSettings>`\ ) - :ref:`LabelSettings<class_LabelSettings>` **get_label_settings**\ (\ )

Một resource :ref:`LabelSettings<class_LabelSettings>` có thể được chia sẻ giữa nhiều node **Label**. Được ưu tiên hơn các thuộc tính theme.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_language:

.. rst-class:: classref-property

:ref:`String<class_String>` **language** = ``""`` :ref:`🔗<class_Label_property_language>`

.. rst-class:: classref-property-setget

- |void| **set_language**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_language**\ (\ )

Mã ngôn ngữ được sử dụng cho các thuật toán ngắt dòng và định hình văn bản. Nếu để trống, locale hiện tại sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_lines_skipped:

.. rst-class:: classref-property

:ref:`int<class_int>` **lines_skipped** = ``0`` :ref:`🔗<class_Label_property_lines_skipped>`

.. rst-class:: classref-property-setget

- |void| **set_lines_skipped**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_lines_skipped**\ (\ )

Số dòng bị bỏ qua và không hiển thị từ đầu giá trị :ref:`text<class_Label_property_text>`.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_max_lines_visible:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_lines_visible** = ``-1`` :ref:`🔗<class_Label_property_max_lines_visible>`

.. rst-class:: classref-property-setget

- |void| **set_max_lines_visible**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_lines_visible**\ (\ )

Giới hạn số dòng văn bản mà node hiển thị trên màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_paragraph_separator:

.. rst-class:: classref-property

:ref:`String<class_String>` **paragraph_separator** = ``"\\n"`` :ref:`🔗<class_Label_property_paragraph_separator>`

.. rst-class:: classref-property-setget

- |void| **set_paragraph_separator**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_paragraph_separator**\ (\ )

Chuỗi được sử dụng làm dấu phân cách đoạn văn. Mỗi đoạn văn được xử lý độc lập, trong ngữ cảnh BiDi riêng.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_structured_text_bidi_override:

.. rst-class:: classref-property

:ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **structured_text_bidi_override** = ``0`` :ref:`🔗<class_Label_property_structured_text_bidi_override>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override**\ (\ value\: :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>`\ ) - :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **get_structured_text_bidi_override**\ (\ )

Đặt ghi đè thuật toán BiDi cho văn bản có cấu trúc.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_structured_text_bidi_override_options:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **structured_text_bidi_override_options** = ``[]`` :ref:`🔗<class_Label_property_structured_text_bidi_override_options>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override_options**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_structured_text_bidi_override_options**\ (\ )

Đặt các tùy chọn bổ sung cho ghi đè BiDi.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_tab_stops:

.. rst-class:: classref-property

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **tab_stops** = ``PackedFloat32Array()`` :ref:`🔗<class_Label_property_tab_stops>`

.. rst-class:: classref-property-setget

- |void| **set_tab_stops**\ (\ value\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) - :ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_tab_stops**\ (\ )

Căn chỉnh văn bản theo các điểm dừng tab đã cho.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat32Array<class_PackedFloat32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **text** = ``""`` :ref:`🔗<class_Label_property_text>`

.. rst-class:: classref-property-setget

- |void| **set_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_text**\ (\ )

Văn bản cần hiển thị trên màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_text_direction:

.. rst-class:: classref-property

:ref:`TextDirection<enum_Control_TextDirection>` **text_direction** = ``0`` :ref:`🔗<class_Label_property_text_direction>`

.. rst-class:: classref-property-setget

- |void| **set_text_direction**\ (\ value\: :ref:`TextDirection<enum_Control_TextDirection>`\ ) - :ref:`TextDirection<enum_Control_TextDirection>` **get_text_direction**\ (\ )

Hướng viết cơ bản của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_text_overrun_behavior:

.. rst-class:: classref-property

:ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **text_overrun_behavior** = ``0`` :ref:`🔗<class_Label_property_text_overrun_behavior>`

.. rst-class:: classref-property-setget

- |void| **set_text_overrun_behavior**\ (\ value\: :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>`\ ) - :ref:`OverrunBehavior<enum_TextServer_OverrunBehavior>` **get_text_overrun_behavior**\ (\ )

Hành vi cắt khi văn bản vượt quá hình chữ nhật giới hạn của node.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_uppercase:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **uppercase** = ``false`` :ref:`🔗<class_Label_property_uppercase>`

.. rst-class:: classref-property-setget

- |void| **set_uppercase**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_uppercase**\ (\ )

Nếu ``true``, toàn bộ văn bản sẽ được hiển thị bằng CHỮ IN HOA.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_vertical_alignment:

.. rst-class:: classref-property

:ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **vertical_alignment** = ``0`` :ref:`🔗<class_Label_property_vertical_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_vertical_alignment**\ (\ value\: :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`\ ) - :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **get_vertical_alignment**\ (\ )

Điều khiển căn chỉnh văn bản theo chiều dọc. Hỗ trợ trên, giữa, dưới và lấp đầy.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_visible_characters:

.. rst-class:: classref-property

:ref:`int<class_int>` **visible_characters** = ``-1`` :ref:`🔗<class_Label_property_visible_characters>`

.. rst-class:: classref-property-setget

- |void| **set_visible_characters**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_visible_characters**\ (\ )

Số ký tự cần hiển thị. Nếu được đặt thành ``-1``, tất cả ký tự sẽ được hiển thị. Điều này có thể hữu ích khi tạo hiệu ứng động cho văn bản xuất hiện trong hộp thoại.

\ **Lưu ý:** Việc đặt thuộc tính này sẽ cập nhật :ref:`visible_ratio<class_Label_property_visible_ratio>` tương ứng.

\ **Lưu ý:** Ký tự được đếm dưới dạng codepoint Unicode. Một grapheme hiển thị có thể chứa nhiều codepoint (ví dụ: một số emoji sử dụng ba codepoint). Một codepoint có thể chứa hai ký tự UTF-16, vốn được sử dụng trong chuỗi C#.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_visible_characters_behavior:

.. rst-class:: classref-property

:ref:`VisibleCharactersBehavior<enum_TextServer_VisibleCharactersBehavior>` **visible_characters_behavior** = ``0`` :ref:`🔗<class_Label_property_visible_characters_behavior>`

.. rst-class:: classref-property-setget

- |void| **set_visible_characters_behavior**\ (\ value\: :ref:`VisibleCharactersBehavior<enum_TextServer_VisibleCharactersBehavior>`\ ) - :ref:`VisibleCharactersBehavior<enum_TextServer_VisibleCharactersBehavior>` **get_visible_characters_behavior**\ (\ )

Hành vi cắt khi :ref:`visible_characters<class_Label_property_visible_characters>` hoặc :ref:`visible_ratio<class_Label_property_visible_ratio>` được đặt.

.. rst-class:: classref-item-separator

----

.. _class_Label_property_visible_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **visible_ratio** = ``1.0`` :ref:`🔗<class_Label_property_visible_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_visible_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_visible_ratio**\ (\ )

Tỷ lệ ký tự cần hiển thị so với tổng số ký tự (xem :ref:`get_total_character_count()<class_Label_method_get_total_character_count>`). Nếu đặt thành ``1.0``, tất cả ký tự sẽ được hiển thị. Nếu đặt thành ``0.5``, chỉ một nửa số ký tự sẽ được hiển thị. Điều này có thể hữu ích khi tạo hiệu ứng động cho văn bản xuất hiện trong hộp thoại.

\ **Lưu ý:** Việc thiết lập thuộc tính này sẽ cập nhật :ref:`visible_characters<class_Label_property_visible_characters>` tương ứng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Label_method_get_character_bounds:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **get_character_bounds**\ (\ pos\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Label_method_get_character_bounds>`

Trả về hình chữ nhật bao quanh ký tự tại vị trí ``pos`` trong hệ tọa độ cục bộ của nhãn. Nếu ký tự là ký tự không hiển thị hoặc ``pos`` nằm ngoài phạm vi hợp lệ, một :ref:`Rect2<class_Rect2>` rỗng sẽ được trả về. Nếu ký tự là một phần của grapheme tổng hợp, hình chữ nhật bao quanh toàn bộ grapheme sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Label_method_get_line_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_line_count**\ (\ ) |const| :ref:`🔗<class_Label_method_get_line_count>`

Trả về số dòng văn bản mà Label có.

.. rst-class:: classref-item-separator

----

.. _class_Label_method_get_line_height:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_line_height**\ (\ line\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_Label_method_get_line_height>`

Trả về chiều cao của dòng ``line``.

Nếu ``line`` được đặt thành ``-1``, trả về chiều cao dòng lớn nhất.

Nếu không có dòng nào, trả về kích thước font theo pixel.

.. rst-class:: classref-item-separator

----

.. _class_Label_method_get_total_character_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_total_character_count**\ (\ ) |const| :ref:`🔗<class_Label_method_get_total_character_count>`

Trả về tổng số ký tự có thể in trong văn bản (không bao gồm dấu cách và ký tự xuống dòng).

.. rst-class:: classref-item-separator

----

.. _class_Label_method_get_visible_line_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_visible_line_count**\ (\ ) |const| :ref:`🔗<class_Label_method_get_visible_line_count>`

Trả về số dòng được hiển thị. Hữu ích khi chiều cao của **Label** hiện không thể hiển thị tất cả các dòng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_Label_theme_color_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Label_theme_color_font_color>`

:ref:`Color<class_Color>` văn bản mặc định của **Label**.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_color_font_outline_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_outline_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_Label_theme_color_font_outline_color>`

Màu đường viền của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_color_font_shadow_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_shadow_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_Label_theme_color_font_shadow_color>`

:ref:`Color<class_Color>` của hiệu ứng bóng văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_line_spacing:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **line_spacing** = ``3`` :ref:`🔗<class_Label_theme_constant_line_spacing>`

Khoảng cách dọc bổ sung giữa các dòng (tính bằng pixel); khoảng cách này được cộng vào phần đi xuống của dòng. Giá trị này có thể là số âm.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_Label_theme_constant_outline_size>`

Kích thước đường viền văn bản.

\ **Lưu ý:** Nếu sử dụng font có bật :ref:`FontFile.multichannel_signed_distance_field<class_FontFile_property_multichannel_signed_distance_field>`, :ref:`FontFile.msdf_pixel_range<class_FontFile_property_msdf_pixel_range>` của font đó phải được đặt ít nhất bằng *hai lần* giá trị của :ref:`outline_size<class_Label_theme_constant_outline_size>` để việc hiển thị đường viền chính xác. Nếu không, đường viền có thể bị cắt sớm hơn dự kiến.

\ **Lưu ý:** Không khuyến nghị sử dụng giá trị lớn hơn một nửa kích thước font, vì trong trường hợp này đường viền font có thể không được khép kín hoàn toàn.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_paragraph_spacing:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **paragraph_spacing** = ``0`` :ref:`🔗<class_Label_theme_constant_paragraph_spacing>`

Khoảng cách dọc giữa các đoạn văn. Được cộng thêm vào :ref:`line_spacing<class_Label_theme_constant_line_spacing>`.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_shadow_offset_x:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **shadow_offset_x** = ``1`` :ref:`🔗<class_Label_theme_constant_shadow_offset_x>`

Độ lệch ngang của bóng văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_shadow_offset_y:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **shadow_offset_y** = ``1`` :ref:`🔗<class_Label_theme_constant_shadow_offset_y>`

Độ lệch dọc của bóng văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_constant_shadow_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **shadow_outline_size** = ``1`` :ref:`🔗<class_Label_theme_constant_shadow_outline_size>`

Kích thước đường viền bóng.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_font_font:

.. rst-class:: classref-themeproperty

:ref:`Font<class_Font>` **font** :ref:`🔗<class_Label_theme_font_font>`

:ref:`Font<class_Font>` được sử dụng cho văn bản của **Label**.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_font_size_font_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **font_size** :ref:`🔗<class_Label_theme_font_size_font_size>`

Kích thước font của văn bản **Label**.

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_style_focus:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **focus** :ref:`🔗<class_Label_theme_style_focus>`

:ref:`StyleBox<class_StyleBox>` được sử dụng khi **Label** được focus (khi được dùng với các ứng dụng hỗ trợ).

.. rst-class:: classref-item-separator

----

.. _class_Label_theme_style_normal:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **normal** :ref:`🔗<class_Label_theme_style_normal>`

:ref:`StyleBox<class_StyleBox>` nền cho **Label**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
