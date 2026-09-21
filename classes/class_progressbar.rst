:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ProgressBar.xml.

.. _class_ProgressBar:

ProgressBar
===========

**Kế thừa:** :ref:`Range<class_Range>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một control được dùng để biểu diễn trực quan một phần trăm.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một control được dùng để biểu diễn trực quan một phần trăm. Hiển thị phần trăm được tô ở giữa. Cũng có thể được dùng để hiển thị tiến trình không xác định. Để có thêm các chế độ tô, hãy dùng :ref:`TextureProgressBar<class_TextureProgressBar>` thay thế.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`editor_preview_indeterminate<class_ProgressBar_property_editor_preview_indeterminate>` |           |
   +-------------------------+----------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`   | :ref:`fill_mode<class_ProgressBar_property_fill_mode>`                                       | ``0``     |
   +-------------------------+----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`indeterminate<class_ProgressBar_property_indeterminate>`                               | ``false`` |
   +-------------------------+----------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`show_percentage<class_ProgressBar_property_show_percentage>`                           | ``true``  |
   +-------------------------+----------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_color<class_ProgressBar_theme_color_font_color>`                 | ``Color(0.95, 0.95, 0.95, 1)`` |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`font_outline_color<class_ProgressBar_theme_color_font_outline_color>` | ``Color(0, 0, 0, 1)``          |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`int<class_int>`           | :ref:`outline_size<class_ProgressBar_theme_constant_outline_size>`          | ``0``                          |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`Font<class_Font>`         | :ref:`font<class_ProgressBar_theme_font_font>`                              |                                |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`int<class_int>`           | :ref:`font_size<class_ProgressBar_theme_font_size_font_size>`               |                                |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`background<class_ProgressBar_theme_style_background>`                 |                                |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`fill<class_ProgressBar_theme_style_fill>`                             |                                |
   +---------------------------------+-----------------------------------------------------------------------------+--------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_ProgressBar_FillMode:

.. rst-class:: classref-enumeration

enum **FillMode**: :ref:`🔗<enum_ProgressBar_FillMode>`

.. _class_ProgressBar_constant_FILL_BEGIN_TO_END:

.. rst-class:: classref-enumeration-constant

:ref:`FillMode<enum_ProgressBar_FillMode>` **FILL_BEGIN_TO_END** = ``0``

Thanh tiến trình được tô theo chiều ngang từ đầu đến cuối, tùy theo hướng ngôn ngữ. Nếu :ref:`Control.is_layout_rtl()<class_Control_method_is_layout_rtl>` trả về ``false``, thanh sẽ được tô từ trái sang phải; nếu trả về ``true``, thanh sẽ được tô từ phải sang trái.

.. _class_ProgressBar_constant_FILL_END_TO_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`FillMode<enum_ProgressBar_FillMode>` **FILL_END_TO_BEGIN** = ``1``

Thanh tiến trình được tô theo chiều ngang từ cuối đến đầu, tùy theo hướng ngôn ngữ. Nếu :ref:`Control.is_layout_rtl()<class_Control_method_is_layout_rtl>` trả về ``false``, thanh sẽ được tô từ phải sang trái; nếu trả về ``true``, thanh sẽ được tô từ trái sang phải.

.. _class_ProgressBar_constant_FILL_TOP_TO_BOTTOM:

.. rst-class:: classref-enumeration-constant

:ref:`FillMode<enum_ProgressBar_FillMode>` **FILL_TOP_TO_BOTTOM** = ``2``

Tiến trình được tô từ trên xuống dưới.

.. _class_ProgressBar_constant_FILL_BOTTOM_TO_TOP:

.. rst-class:: classref-enumeration-constant

:ref:`FillMode<enum_ProgressBar_FillMode>` **FILL_BOTTOM_TO_TOP** = ``3``

Tiến trình được tô từ dưới lên trên.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ProgressBar_property_editor_preview_indeterminate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_preview_indeterminate** :ref:`🔗<class_ProgressBar_property_editor_preview_indeterminate>`

.. rst-class:: classref-property-setget

- |void| **set_editor_preview_indeterminate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editor_preview_indeterminate_enabled**\ (\ )

Nếu ``false``, animation :ref:`indeterminate<class_ProgressBar_property_indeterminate>` sẽ bị tạm dừng trong editor.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_property_fill_mode:

.. rst-class:: classref-property

:ref:`int<class_int>` **fill_mode** = ``0`` :ref:`🔗<class_ProgressBar_property_fill_mode>`

.. rst-class:: classref-property-setget

- |void| **set_fill_mode**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fill_mode**\ (\ )

Hướng tô. Xem :ref:`FillMode<enum_ProgressBar_FillMode>` để biết các giá trị có thể có.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_property_indeterminate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **indeterminate** = ``false`` :ref:`🔗<class_ProgressBar_property_indeterminate>`

.. rst-class:: classref-property-setget

- |void| **set_indeterminate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_indeterminate**\ (\ )

Khi được đặt thành ``true``, thanh tiến trình cho biết một việc gì đó đang diễn ra bằng một animation, nhưng không hiển thị phần trăm hoặc giá trị được tô.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_property_show_percentage:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **show_percentage** = ``true`` :ref:`🔗<class_ProgressBar_property_show_percentage>`

.. rst-class:: classref-property-setget

- |void| **set_show_percentage**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_percentage_shown**\ (\ )

Nếu ``true``, phần trăm được tô sẽ hiển thị trên thanh.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_ProgressBar_theme_color_font_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_color** = ``Color(0.95, 0.95, 0.95, 1)`` :ref:`🔗<class_ProgressBar_theme_color_font_color>`

Màu của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_color_font_outline_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **font_outline_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_ProgressBar_theme_color_font_outline_color>`

Màu sắc của đường viền văn bản của **ProgressBar**.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_constant_outline_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_ProgressBar_theme_constant_outline_size>`

Kích thước đường viền văn bản.

\ **Lưu ý:** Nếu sử dụng font có bật :ref:`FontFile.multichannel_signed_distance_field<class_FontFile_property_multichannel_signed_distance_field>`, :ref:`FontFile.msdf_pixel_range<class_FontFile_property_msdf_pixel_range>` của font đó phải được đặt ít nhất bằng *hai lần* giá trị của :ref:`outline_size<class_ProgressBar_theme_constant_outline_size>` để việc render đường viền hiển thị chính xác. Nếu không, đường viền có thể bị cắt sớm hơn dự kiến.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_font_font:

.. rst-class:: classref-themeproperty

:ref:`Font<class_Font>` **font** :ref:`🔗<class_ProgressBar_theme_font_font>`

Font được dùng để vẽ phần trăm được tô nếu :ref:`show_percentage<class_ProgressBar_property_show_percentage>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_font_size_font_size:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **font_size** :ref:`🔗<class_ProgressBar_theme_font_size_font_size>`

Cỡ font được dùng để vẽ phần trăm được tô nếu :ref:`show_percentage<class_ProgressBar_property_show_percentage>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_style_background:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **background** :ref:`🔗<class_ProgressBar_theme_style_background>`

Style của nền.

.. rst-class:: classref-item-separator

----

.. _class_ProgressBar_theme_style_fill:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **fill** :ref:`🔗<class_ProgressBar_theme_style_fill>`

Style của tiến trình (tức là phần tô đầy thanh).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
