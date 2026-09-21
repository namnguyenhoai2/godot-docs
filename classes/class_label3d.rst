:github_url: hide

.. meta::
	:keywords: text

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Label3D.xml.

.. _class_Label3D:

Label3D
=======

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node dùng để hiển thị văn bản thuần túy trong không gian 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node dùng để hiển thị văn bản thuần túy trong không gian 3D. Bằng cách điều chỉnh nhiều thuộc tính khác nhau của node này, bạn có thể cấu hình những yếu tố như giao diện của văn bản và việc văn bản có luôn hướng về camera hay không.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Văn bản 3D <../tutorials/3d/3d_text>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`alpha_antialiasing_edge<class_Label3D_property_alpha_antialiasing_edge>`                             | ``0.0``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`AlphaAntiAliasing<enum_BaseMaterial3D_AlphaAntiAliasing>`           | :ref:`alpha_antialiasing_mode<class_Label3D_property_alpha_antialiasing_mode>`                             | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>`                            | :ref:`alpha_cut<class_Label3D_property_alpha_cut>`                                                         | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`alpha_hash_scale<class_Label3D_property_alpha_hash_scale>`                                           | ``1.0``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`alpha_scissor_threshold<class_Label3D_property_alpha_scissor_threshold>`                             | ``0.5``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`                         | :ref:`autowrap_mode<class_Label3D_property_autowrap_mode>`                                                 | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\]         | :ref:`autowrap_trim_flags<class_Label3D_property_autowrap_trim_flags>`                                     | ``192``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`BillboardMode<enum_BaseMaterial3D_BillboardMode>`                   | :ref:`billboard<class_Label3D_property_billboard>`                                                         | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` | cast_shadow                                                                                                | ``0`` (overrides :ref:`GeometryInstance3D<class_GeometryInstance3D_property_cast_shadow>`) |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`double_sided<class_Label3D_property_double_sided>`                                                   | ``true``                                                                                   |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`fixed_size<class_Label3D_property_fixed_size>`                                                       | ``false``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Font<class_Font>`                                                   | :ref:`font<class_Label3D_property_font>`                                                                   |                                                                                            |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`font_size<class_Label3D_property_font_size>`                                                         | ``32``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`GIMode<enum_GeometryInstance3D_GIMode>`                             | gi_mode                                                                                                    | ``0`` (overrides :ref:`GeometryInstance3D<class_GeometryInstance3D_property_gi_mode>`)     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`         | :ref:`horizontal_alignment<class_Label3D_property_horizontal_alignment>`                                   | ``1``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\] | :ref:`justification_flags<class_Label3D_property_justification_flags>`                                     | ``163``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                               | :ref:`language<class_Label3D_property_language>`                                                           | ``""``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`line_spacing<class_Label3D_property_line_spacing>`                                                   | ``0.0``                                                                                    |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                                                 | :ref:`modulate<class_Label3D_property_modulate>`                                                           | ``Color(1, 1, 1, 1)``                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`no_depth_test<class_Label3D_property_no_depth_test>`                                                 | ``false``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                             | :ref:`offset<class_Label3D_property_offset>`                                                               | ``Vector2(0, 0)``                                                                          |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                                                 | :ref:`outline_modulate<class_Label3D_property_outline_modulate>`                                           | ``Color(0, 0, 0, 1)``                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`outline_render_priority<class_Label3D_property_outline_render_priority>`                             | ``-1``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`outline_size<class_Label3D_property_outline_size>`                                                   | ``12``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`pixel_size<class_Label3D_property_pixel_size>`                                                       | ``0.005``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`render_priority<class_Label3D_property_render_priority>`                                             | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`shaded<class_Label3D_property_shaded>`                                                               | ``false``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>`         | :ref:`structured_text_bidi_override<class_Label3D_property_structured_text_bidi_override>`                 | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                 | :ref:`structured_text_bidi_override_options<class_Label3D_property_structured_text_bidi_override_options>` | ``[]``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                               | :ref:`text<class_Label3D_property_text>`                                                                   | ``""``                                                                                     |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`Direction<enum_TextServer_Direction>`                               | :ref:`text_direction<class_Label3D_property_text_direction>`                                               | ``0``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`TextureFilter<enum_BaseMaterial3D_TextureFilter>`                   | :ref:`texture_filter<class_Label3D_property_texture_filter>`                                               | ``3``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`uppercase<class_Label3D_property_uppercase>`                                                         | ``false``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`             | :ref:`vertical_alignment<class_Label3D_property_vertical_alignment>`                                       | ``1``                                                                                      |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`width<class_Label3D_property_width>`                                                                 | ``500.0``                                                                                  |
   +---------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TriangleMesh<class_TriangleMesh>` | :ref:`generate_triangle_mesh<class_Label3D_method_generate_triangle_mesh>`\ (\ ) |const|                                                           |
   +-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                 | :ref:`get_draw_flag<class_Label3D_method_get_draw_flag>`\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const|                            |
   +-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                  | :ref:`set_draw_flag<class_Label3D_method_set_draw_flag>`\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Label3D_DrawFlags:

.. rst-class:: classref-enumeration

enum **DrawFlags**: :ref:`🔗<enum_Label3D_DrawFlags>`

.. _class_Label3D_constant_FLAG_SHADED:

.. rst-class:: classref-enumeration-constant

:ref:`DrawFlags<enum_Label3D_DrawFlags>` **FLAG_SHADED** = ``0``

Nếu được đặt, ánh sáng trong môi trường sẽ ảnh hưởng đến label.

.. _class_Label3D_constant_FLAG_DOUBLE_SIDED:

.. rst-class:: classref-enumeration-constant

:ref:`DrawFlags<enum_Label3D_DrawFlags>` **FLAG_DOUBLE_SIDED** = ``1``

Nếu được đặt, văn bản cũng có thể được nhìn thấy từ phía sau. Nếu không, văn bản sẽ vô hình khi nhìn từ phía sau.

.. _class_Label3D_constant_FLAG_DISABLE_DEPTH_TEST:

.. rst-class:: classref-enumeration-constant

:ref:`DrawFlags<enum_Label3D_DrawFlags>` **FLAG_DISABLE_DEPTH_TEST** = ``2``

Vô hiệu hóa depth test, khiến object này được vẽ lên trên tất cả các object khác. Tuy nhiên, các object được vẽ sau nó trong thứ tự vẽ có thể che phủ nó.

.. _class_Label3D_constant_FLAG_FIXED_SIZE:

.. rst-class:: classref-enumeration-constant

:ref:`DrawFlags<enum_Label3D_DrawFlags>` **FLAG_FIXED_SIZE** = ``3``

Label được scale theo độ sâu để luôn xuất hiện với cùng kích thước trên màn hình.

.. _class_Label3D_constant_FLAG_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`DrawFlags<enum_Label3D_DrawFlags>` **FLAG_MAX** = ``4``

Biểu thị kích thước của enum :ref:`DrawFlags<enum_Label3D_DrawFlags>`.

.. rst-class:: classref-item-separator

----

.. _enum_Label3D_AlphaCutMode:

.. rst-class:: classref-enumeration

enum **AlphaCutMode**: :ref:`🔗<enum_Label3D_AlphaCutMode>`

.. _class_Label3D_constant_ALPHA_CUT_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **ALPHA_CUT_DISABLED** = ``0``

Chế độ này thực hiện alpha blending tiêu chuẩn. Chế độ này có thể hiển thị các vùng bán trong suốt, nhưng có thể thấy các vấn đề sắp xếp độ trong suốt khi nhiều material trong suốt chồng lên nhau. :ref:`GeometryInstance3D.cast_shadow<class_GeometryInstance3D_property_cast_shadow>` không có tác dụng khi sử dụng chế độ trong suốt này; **Label3D** sẽ không bao giờ đổ bóng.

.. _class_Label3D_constant_ALPHA_CUT_DISCARD:

.. rst-class:: classref-enumeration-constant

:ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **ALPHA_CUT_DISCARD** = ``1``

Chế độ này chỉ cho phép các pixel hoàn toàn trong suốt hoặc hoàn toàn không trong suốt. Các cạnh gắt sẽ hiện rõ trừ khi đã bật một dạng antialiasing trong không gian màn hình (xem :ref:`ProjectSettings.rendering/anti_aliasing/quality/screen_space_aa<class_ProjectSettings_property_rendering/anti_aliasing/quality/screen_space_aa>`). Chế độ này còn được gọi là *alpha testing* hoặc *độ trong suốt 1 bit*.

\ **Lưu ý:** Chế độ này có thể gặp vấn đề với font và đường viền đã được anti-alias, hãy thử điều chỉnh :ref:`alpha_scissor_threshold<class_Label3D_property_alpha_scissor_threshold>` hoặc sử dụng font MSDF.

\ **Lưu ý:** Khi sử dụng văn bản có các glyph chồng lên nhau (ví dụ: chữ viết tay), chế độ này có thể gặp vấn đề sắp xếp độ trong suốt giữa văn bản chính và đường viền.

.. _class_Label3D_constant_ALPHA_CUT_OPAQUE_PREPASS:

.. rst-class:: classref-enumeration-constant

:ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **ALPHA_CUT_OPAQUE_PREPASS** = ``2``

Chế độ này vẽ các pixel hoàn toàn không trong suốt trong depth prepass. Chế độ này chậm hơn :ref:`ALPHA_CUT_DISABLED<class_Label3D_constant_ALPHA_CUT_DISABLED>` hoặc :ref:`ALPHA_CUT_DISCARD<class_Label3D_constant_ALPHA_CUT_DISCARD>`, nhưng cho phép hiển thị các vùng bán trong suốt và các cạnh mượt mà đồng thời sử dụng cách sắp xếp phù hợp.

\ **Lưu ý:** Khi sử dụng văn bản có các glyph chồng lên nhau (ví dụ: chữ viết tay), chế độ này có thể gặp vấn đề sắp xếp độ trong suốt giữa văn bản chính và đường viền.

.. _class_Label3D_constant_ALPHA_CUT_HASH:

.. rst-class:: classref-enumeration-constant

:ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **ALPHA_CUT_HASH** = ``3``

Chế độ này loại bỏ tất cả các giá trị dưới một ngưỡng được xác định nhất quán theo không gian; các giá trị còn lại sẽ vẫn không trong suốt.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Label3D_property_alpha_antialiasing_edge:

.. rst-class:: classref-property

:ref:`float<class_float>` **alpha_antialiasing_edge** = ``0.0`` :ref:`🔗<class_Label3D_property_alpha_antialiasing_edge>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_antialiasing_edge**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_alpha_antialiasing_edge**\ (\ )

Ngưỡng tại đó antialiasing sẽ được áp dụng cho alpha channel.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_alpha_antialiasing_mode:

.. rst-class:: classref-property

:ref:`AlphaAntiAliasing<enum_BaseMaterial3D_AlphaAntiAliasing>` **alpha_antialiasing_mode** = ``0`` :ref:`🔗<class_Label3D_property_alpha_antialiasing_mode>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_antialiasing**\ (\ value\: :ref:`AlphaAntiAliasing<enum_BaseMaterial3D_AlphaAntiAliasing>`\ ) - :ref:`AlphaAntiAliasing<enum_BaseMaterial3D_AlphaAntiAliasing>` **get_alpha_antialiasing**\ (\ )

Loại alpha antialiasing cần áp dụng.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_alpha_cut:

.. rst-class:: classref-property

:ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **alpha_cut** = ``0`` :ref:`🔗<class_Label3D_property_alpha_cut>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_cut_mode**\ (\ value\: :ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>`\ ) - :ref:`AlphaCutMode<enum_Label3D_AlphaCutMode>` **get_alpha_cut_mode**\ (\ )

Chế độ alpha cutting được sử dụng cho sprite.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_alpha_hash_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **alpha_hash_scale** = ``1.0`` :ref:`🔗<class_Label3D_property_alpha_hash_scale>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_hash_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_alpha_hash_scale**\ (\ )

Scale hashing cho Alpha Hash. Các giá trị được khuyến nghị nằm giữa ``0`` và ``2``.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_alpha_scissor_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **alpha_scissor_threshold** = ``0.5`` :ref:`🔗<class_Label3D_property_alpha_scissor_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_alpha_scissor_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_alpha_scissor_threshold**\ (\ )

Ngưỡng tại đó alpha scissor sẽ loại bỏ các giá trị.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_autowrap_mode:

.. rst-class:: classref-property

:ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **autowrap_mode** = ``0`` :ref:`🔗<class_Label3D_property_autowrap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_mode**\ (\ value\: :ref:`AutowrapMode<enum_TextServer_AutowrapMode>`\ ) - :ref:`AutowrapMode<enum_TextServer_AutowrapMode>` **get_autowrap_mode**\ (\ )

Nếu được đặt thành giá trị khác :ref:`TextServer.AUTOWRAP_OFF<class_TextServer_constant_AUTOWRAP_OFF>`, văn bản sẽ được ngắt dòng bên trong hình chữ nhật bao quanh node. Nếu thay đổi kích thước node, chiều cao của node sẽ tự động thay đổi để hiển thị toàn bộ văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_autowrap_trim_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **autowrap_trim_flags** = ``192`` :ref:`🔗<class_Label3D_property_autowrap_trim_flags>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap_trim_flags**\ (\ value\: |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\]\ ) - |bitfield|\[:ref:`LineBreakFlag<enum_TextServer_LineBreakFlag>`\] **get_autowrap_trim_flags**\ (\ )

Các cờ cắt khoảng trắng khi ngắt dòng tự động. Xem :ref:`TextServer.BREAK_TRIM_START_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_START_EDGE_SPACES>` và :ref:`TextServer.BREAK_TRIM_END_EDGE_SPACES<class_TextServer_constant_BREAK_TRIM_END_EDGE_SPACES>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_billboard:

.. rst-class:: classref-property

:ref:`BillboardMode<enum_BaseMaterial3D_BillboardMode>` **billboard** = ``0`` :ref:`🔗<class_Label3D_property_billboard>`

.. rst-class:: classref-property-setget

- |void| **set_billboard_mode**\ (\ value\: :ref:`BillboardMode<enum_BaseMaterial3D_BillboardMode>`\ ) - :ref:`BillboardMode<enum_BaseMaterial3D_BillboardMode>` **get_billboard_mode**\ (\ )

Chế độ billboard được sử dụng cho label.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_double_sided:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **double_sided** = ``true`` :ref:`🔗<class_Label3D_property_double_sided>`

.. rst-class:: classref-property-setget

- |void| **set_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const|

Nếu ``true``, văn bản cũng có thể được nhìn thấy từ phía sau; nếu ``false``, văn bản sẽ vô hình khi nhìn từ phía sau.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_fixed_size:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **fixed_size** = ``false`` :ref:`🔗<class_Label3D_property_fixed_size>`

.. rst-class:: classref-property-setget

- |void| **set_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const|

Nếu ``true``, label được render với cùng kích thước bất kể khoảng cách. Kích thước của label trên màn hình giống như khi camera cách gốc của label ``1.0`` đơn vị, bất kể khoảng cách thực tế từ camera. Trường nhìn của :ref:`Camera3D<class_Camera3D>` (hoặc :ref:`Camera3D.size<class_Camera3D_property_size>` khi ở chế độ orthogonal/frustum) vẫn ảnh hưởng đến kích thước mà label được vẽ.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_font:

.. rst-class:: classref-property

:ref:`Font<class_Font>` **font** :ref:`🔗<class_Label3D_property_font>`

.. rst-class:: classref-property-setget

- |void| **set_font**\ (\ value\: :ref:`Font<class_Font>`\ ) - :ref:`Font<class_Font>` **get_font**\ (\ )

Cấu hình font được sử dụng để hiển thị văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_font_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **font_size** = ``32`` :ref:`🔗<class_Label3D_property_font_size>`

.. rst-class:: classref-property-setget

- |void| **set_font_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_font_size**\ (\ )

Kích thước font của văn bản trong **Label3D**. Để font trông chi tiết hơn khi ở gần, hãy tăng :ref:`font_size<class_Label3D_property_font_size>` đồng thời giảm :ref:`pixel_size<class_Label3D_property_pixel_size>`.

Kích thước font lớn hơn cần nhiều thời gian hơn để render các ký tự mới, điều này có thể gây giật trong khi chơi.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_horizontal_alignment:

.. rst-class:: classref-property

:ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **horizontal_alignment** = ``1`` :ref:`🔗<class_Label3D_property_horizontal_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_horizontal_alignment**\ (\ value\: :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>`\ ) - :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` **get_horizontal_alignment**\ (\ )

Điều khiển căn chỉnh ngang của văn bản. Hỗ trợ left, center, right và fill (còn gọi là justify).

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_justification_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\] **justification_flags** = ``163`` :ref:`🔗<class_Label3D_property_justification_flags>`

.. rst-class:: classref-property-setget

- |void| **set_justification_flags**\ (\ value\: |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\]\ ) - |bitfield|\[:ref:`JustificationFlag<enum_TextServer_JustificationFlag>`\] **get_justification_flags**\ (\ )

Các quy tắc căn chỉnh để lấp đầy dòng.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_language:

.. rst-class:: classref-property

:ref:`String<class_String>` **language** = ``""`` :ref:`🔗<class_Label3D_property_language>`

.. rst-class:: classref-property-setget

- |void| **set_language**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_language**\ (\ )

Mã ngôn ngữ được sử dụng cho các thuật toán ngắt dòng và định hình văn bản. Nếu để trống, locale hiện tại sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_line_spacing:

.. rst-class:: classref-property

:ref:`float<class_float>` **line_spacing** = ``0.0`` :ref:`🔗<class_Label3D_property_line_spacing>`

.. rst-class:: classref-property-setget

- |void| **set_line_spacing**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_line_spacing**\ (\ )

Khoảng cách dọc bổ sung giữa các dòng (tính bằng pixel), khoảng cách này được cộng vào độ đi xuống của dòng. Giá trị này có thể là số âm.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_modulate:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **modulate** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Label3D_property_modulate>`

.. rst-class:: classref-property-setget

- |void| **set_modulate**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_modulate**\ (\ )

:ref:`Color<class_Color>` của **Label3D**.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_no_depth_test:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **no_depth_test** = ``false`` :ref:`🔗<class_Label3D_property_no_depth_test>`

.. rst-class:: classref-property-setget

- |void| **set_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const|

Nếu ``true``, kiểm tra độ sâu sẽ bị tắt và đối tượng sẽ được vẽ theo thứ tự render.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Label3D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Độ lệch khi vẽ văn bản (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_outline_modulate:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **outline_modulate** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_Label3D_property_outline_modulate>`

.. rst-class:: classref-property-setget

- |void| **set_outline_modulate**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_outline_modulate**\ (\ )

Màu sắc của viền văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_outline_render_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **outline_render_priority** = ``-1`` :ref:`🔗<class_Label3D_property_outline_render_priority>`

.. rst-class:: classref-property-setget

- |void| **set_outline_render_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_outline_render_priority**\ (\ )

Đặt độ ưu tiên render cho viền văn bản. Các đối tượng có độ ưu tiên cao hơn sẽ được sắp xếp ở phía trước các đối tượng có độ ưu tiên thấp hơn.

\ **Lưu ý:** Điều này chỉ áp dụng nếu :ref:`alpha_cut<class_Label3D_property_alpha_cut>` được đặt thành :ref:`ALPHA_CUT_DISABLED<class_Label3D_constant_ALPHA_CUT_DISABLED>` (giá trị mặc định).

\ **Lưu ý:** Điều này chỉ áp dụng cho việc sắp xếp các đối tượng trong suốt. Điều này không ảnh hưởng đến cách các đối tượng trong suốt được sắp xếp tương đối so với các đối tượng đục. Nguyên nhân là các đối tượng đục không được sắp xếp, trong khi các đối tượng trong suốt được sắp xếp từ sau ra trước (phụ thuộc vào độ ưu tiên).

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_outline_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **outline_size** = ``12`` :ref:`🔗<class_Label3D_property_outline_size>`

.. rst-class:: classref-property-setget

- |void| **set_outline_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_outline_size**\ (\ )

Kích thước viền văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_pixel_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **pixel_size** = ``0.005`` :ref:`🔗<class_Label3D_property_pixel_size>`

.. rst-class:: classref-property-setget

- |void| **set_pixel_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pixel_size**\ (\ )

Kích thước chiều rộng của một pixel trên label để scale label trong không gian 3D. Để font trông chi tiết hơn khi ở gần, hãy tăng :ref:`font_size<class_Label3D_property_font_size>` đồng thời giảm :ref:`pixel_size<class_Label3D_property_pixel_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_render_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **render_priority** = ``0`` :ref:`🔗<class_Label3D_property_render_priority>`

.. rst-class:: classref-property-setget

- |void| **set_render_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_render_priority**\ (\ )

Đặt độ ưu tiên render cho văn bản. Các đối tượng có độ ưu tiên cao hơn sẽ được sắp xếp ở phía trước các đối tượng có độ ưu tiên thấp hơn.

\ **Lưu ý:** Điều này chỉ áp dụng nếu :ref:`alpha_cut<class_Label3D_property_alpha_cut>` được đặt thành :ref:`ALPHA_CUT_DISABLED<class_Label3D_constant_ALPHA_CUT_DISABLED>` (giá trị mặc định).

\ **Lưu ý:** Điều này chỉ áp dụng cho việc sắp xếp các đối tượng trong suốt. Điều này không ảnh hưởng đến cách các đối tượng trong suốt được sắp xếp tương đối so với các đối tượng đục. Nguyên nhân là các đối tượng đục không được sắp xếp, trong khi các đối tượng trong suốt được sắp xếp từ sau ra trước (phụ thuộc vào độ ưu tiên).

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_shaded:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shaded** = ``false`` :ref:`🔗<class_Label3D_property_shaded>`

.. rst-class:: classref-property-setget

- |void| **set_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const|

Nếu ``true``, :ref:`Light3D<class_Light3D>` trong :ref:`Environment<class_Environment>` sẽ có hiệu ứng lên label.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_structured_text_bidi_override:

.. rst-class:: classref-property

:ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **structured_text_bidi_override** = ``0`` :ref:`🔗<class_Label3D_property_structured_text_bidi_override>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override**\ (\ value\: :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>`\ ) - :ref:`StructuredTextParser<enum_TextServer_StructuredTextParser>` **get_structured_text_bidi_override**\ (\ )

Đặt chế độ override cho thuật toán BiDi của văn bản có cấu trúc.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_structured_text_bidi_override_options:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **structured_text_bidi_override_options** = ``[]`` :ref:`🔗<class_Label3D_property_structured_text_bidi_override_options>`

.. rst-class:: classref-property-setget

- |void| **set_structured_text_bidi_override_options**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_structured_text_bidi_override_options**\ (\ )

Đặt các tùy chọn bổ sung cho chế độ override BiDi.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **text** = ``""`` :ref:`🔗<class_Label3D_property_text>`

.. rst-class:: classref-property-setget

- |void| **set_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_text**\ (\ )

Văn bản sẽ hiển thị trên màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_text_direction:

.. rst-class:: classref-property

:ref:`Direction<enum_TextServer_Direction>` **text_direction** = ``0`` :ref:`🔗<class_Label3D_property_text_direction>`

.. rst-class:: classref-property-setget

- |void| **set_text_direction**\ (\ value\: :ref:`Direction<enum_TextServer_Direction>`\ ) - :ref:`Direction<enum_TextServer_Direction>` **get_text_direction**\ (\ )

Hướng viết cơ bản của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_texture_filter:

.. rst-class:: classref-property

:ref:`TextureFilter<enum_BaseMaterial3D_TextureFilter>` **texture_filter** = ``3`` :ref:`🔗<class_Label3D_property_texture_filter>`

.. rst-class:: classref-property-setget

- |void| **set_texture_filter**\ (\ value\: :ref:`TextureFilter<enum_BaseMaterial3D_TextureFilter>`\ ) - :ref:`TextureFilter<enum_BaseMaterial3D_TextureFilter>` **get_texture_filter**\ (\ )

Các cờ filter cho texture.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_uppercase:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **uppercase** = ``false`` :ref:`🔗<class_Label3D_property_uppercase>`

.. rst-class:: classref-property-setget

- |void| **set_uppercase**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_uppercase**\ (\ )

Nếu ``true``, toàn bộ văn bản sẽ hiển thị ở dạng CHỮ IN HOA.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_vertical_alignment:

.. rst-class:: classref-property

:ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **vertical_alignment** = ``1`` :ref:`🔗<class_Label3D_property_vertical_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_vertical_alignment**\ (\ value\: :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>`\ ) - :ref:`VerticalAlignment<enum_@GlobalScope_VerticalAlignment>` **get_vertical_alignment**\ (\ )

Điều khiển căn chỉnh dọc của văn bản. Hỗ trợ căn trên, căn giữa và căn dưới.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_property_width:

.. rst-class:: classref-property

:ref:`float<class_float>` **width** = ``500.0`` :ref:`🔗<class_Label3D_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_width**\ (\ )

Chiều rộng văn bản (tính bằng pixel), được dùng cho autowrap và căn chỉnh độ đầy.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Label3D_method_generate_triangle_mesh:

.. rst-class:: classref-method

:ref:`TriangleMesh<class_TriangleMesh>` **generate_triangle_mesh**\ (\ ) |const| :ref:`🔗<class_Label3D_method_generate_triangle_mesh>`

Trả về một :ref:`TriangleMesh<class_TriangleMesh>` với các vertex của label tuân theo cấu hình hiện tại của nó (chẳng hạn như :ref:`pixel_size<class_Label3D_property_pixel_size>`).

.. rst-class:: classref-item-separator

----

.. _class_Label3D_method_get_draw_flag:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`\ ) |const| :ref:`🔗<class_Label3D_method_get_draw_flag>`

Trả về giá trị của cờ được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Label3D_method_set_draw_flag:

.. rst-class:: classref-method

|void| **set_draw_flag**\ (\ flag\: :ref:`DrawFlags<enum_Label3D_DrawFlags>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Label3D_method_set_draw_flag>`

Nếu ``true``, ``flag`` được chỉ định sẽ được bật.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
