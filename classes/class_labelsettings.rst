:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LabelSettings.xml.

.. _class_LabelSettings:

LabelSettings
=============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các thiết lập chung để tùy chỉnh văn bản trong một :ref:`Label<class_Label>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**LabelSettings** là một resource cung cấp các thiết lập chung để tùy chỉnh văn bản trong một :ref:`Label<class_Label>`. Resource này được ưu tiên hơn các thuộc tính được định nghĩa trong :ref:`Control.theme<class_Control_property_theme>`. Resource có thể được chia sẻ giữa nhiều label và thay đổi ngay trong khi chạy, vì vậy đây là cách thuận tiện và linh hoạt để thiết lập kiểu văn bản.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Font<class_Font>`       | :ref:`font<class_LabelSettings_property_font>`                                                               |                       |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`font_color<class_LabelSettings_property_font_color>`                                                   | ``Color(1, 1, 1, 1)`` |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`font_size<class_LabelSettings_property_font_size>`                                                     | ``16``                |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`     | :ref:`line_spacing<class_LabelSettings_property_line_spacing>`                                               | ``3.0``               |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`outline_color<class_LabelSettings_property_outline_color>`                                             | ``Color(1, 1, 1, 1)`` |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`outline_size<class_LabelSettings_property_outline_size>`                                               | ``0``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`     | :ref:`paragraph_spacing<class_LabelSettings_property_paragraph_spacing>`                                     | ``0.0``               |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`shadow_color<class_LabelSettings_property_shadow_color>`                                               | ``Color(0, 0, 0, 0)`` |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`shadow_offset<class_LabelSettings_property_shadow_offset>`                                             | ``Vector2(1, 1)``     |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`shadow_size<class_LabelSettings_property_shadow_size>`                                                 | ``1``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`stacked_outline_count<class_LabelSettings_property_stacked_outline_count>`                             | ``0``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`stacked_outline_{index}/color<class_LabelSettings_property_stacked_outline_{index}/color>`             | ``Color(0, 0, 0, 1)`` |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`stacked_outline_{index}/size<class_LabelSettings_property_stacked_outline_{index}/size>`               | ``0``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`stacked_shadow_count<class_LabelSettings_property_stacked_shadow_count>`                               | ``0``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`stacked_shadow_{index}/color<class_LabelSettings_property_stacked_shadow_{index}/color>`               | ``Color(0, 0, 0, 1)`` |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`stacked_shadow_{index}/offset<class_LabelSettings_property_stacked_shadow_{index}/offset>`             | ``Vector2(1, 1)``     |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`         | :ref:`stacked_shadow_{index}/outline_size<class_LabelSettings_property_stacked_shadow_{index}/outline_size>` | ``0``                 |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`add_stacked_outline<class_LabelSettings_method_add_stacked_outline>`\ (\ index\: :ref:`int<class_int>` = -1\ )                                                  |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`add_stacked_shadow<class_LabelSettings_method_add_stacked_shadow>`\ (\ index\: :ref:`int<class_int>` = -1\ )                                                    |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`     | :ref:`get_stacked_outline_color<class_LabelSettings_method_get_stacked_outline_color>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                   |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_stacked_outline_size<class_LabelSettings_method_get_stacked_outline_size>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                     |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`     | :ref:`get_stacked_shadow_color<class_LabelSettings_method_get_stacked_shadow_color>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                     |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_stacked_shadow_offset<class_LabelSettings_method_get_stacked_shadow_offset>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                   |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_stacked_shadow_outline_size<class_LabelSettings_method_get_stacked_shadow_outline_size>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                       |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`move_stacked_outline<class_LabelSettings_method_move_stacked_outline>`\ (\ from_index\: :ref:`int<class_int>`, to_position\: :ref:`int<class_int>`\ )           |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`move_stacked_shadow<class_LabelSettings_method_move_stacked_shadow>`\ (\ from_index\: :ref:`int<class_int>`, to_position\: :ref:`int<class_int>`\ )             |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`remove_stacked_outline<class_LabelSettings_method_remove_stacked_outline>`\ (\ index\: :ref:`int<class_int>`\ )                                                 |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`remove_stacked_shadow<class_LabelSettings_method_remove_stacked_shadow>`\ (\ index\: :ref:`int<class_int>`\ )                                                   |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_stacked_outline_color<class_LabelSettings_method_set_stacked_outline_color>`\ (\ index\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ )        |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_stacked_outline_size<class_LabelSettings_method_set_stacked_outline_size>`\ (\ index\: :ref:`int<class_int>`, size\: :ref:`int<class_int>`\ )               |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_stacked_shadow_color<class_LabelSettings_method_set_stacked_shadow_color>`\ (\ index\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ )          |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_stacked_shadow_offset<class_LabelSettings_method_set_stacked_shadow_offset>`\ (\ index\: :ref:`int<class_int>`, offset\: :ref:`Vector2<class_Vector2>`\ )   |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_stacked_shadow_outline_size<class_LabelSettings_method_set_stacked_shadow_outline_size>`\ (\ index\: :ref:`int<class_int>`, size\: :ref:`int<class_int>`\ ) |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LabelSettings_property_font:

.. rst-class:: classref-property

:ref:`Font<class_Font>` **font** :ref:`🔗<class_LabelSettings_property_font>`

.. rst-class:: classref-property-setget

- |void| **set_font**\ (\ value\: :ref:`Font<class_Font>`\ ) - :ref:`Font<class_Font>` **get_font**\ (\ )

:ref:`Font<class_Font>` được sử dụng cho văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_font_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **font_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_LabelSettings_property_font_color>`

.. rst-class:: classref-property-setget

- |void| **set_font_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_font_color**\ (\ )

Màu của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_font_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **font_size** = ``16`` :ref:`🔗<class_LabelSettings_property_font_size>`

.. rst-class:: classref-property-setget

- |void| **set_font_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_font_size**\ (\ )

Kích thước của văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_line_spacing:

.. rst-class:: classref-property

:ref:`float<class_float>` **line_spacing** = ``3.0`` :ref:`🔗<class_LabelSettings_property_line_spacing>`

.. rst-class:: classref-property-setget

- |void| **set_line_spacing**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_line_spacing**\ (\ )

Khoảng cách dọc bổ sung giữa các dòng (tính bằng pixel), khoảng cách này được cộng vào độ hạ dòng. Giá trị này có thể là số âm.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_outline_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **outline_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_LabelSettings_property_outline_color>`

.. rst-class:: classref-property-setget

- |void| **set_outline_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_outline_color**\ (\ )

Màu của đường viền.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_outline_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **outline_size** = ``0`` :ref:`🔗<class_LabelSettings_property_outline_size>`

.. rst-class:: classref-property-setget

- |void| **set_outline_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_outline_size**\ (\ )

Kích thước đường viền văn bản.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_paragraph_spacing:

.. rst-class:: classref-property

:ref:`float<class_float>` **paragraph_spacing** = ``0.0`` :ref:`🔗<class_LabelSettings_property_paragraph_spacing>`

.. rst-class:: classref-property-setget

- |void| **set_paragraph_spacing**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_paragraph_spacing**\ (\ )

Khoảng cách dọc giữa các đoạn văn. Được cộng thêm vào :ref:`line_spacing<class_LabelSettings_property_line_spacing>`.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_shadow_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **shadow_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_LabelSettings_property_shadow_color>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_shadow_color**\ (\ )

Màu của hiệu ứng bóng. Nếu alpha là ``0``, bóng sẽ không được vẽ.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_shadow_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **shadow_offset** = ``Vector2(1, 1)`` :ref:`🔗<class_LabelSettings_property_shadow_offset>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_shadow_offset**\ (\ )

Độ lệch của hiệu ứng bóng, tính bằng pixel.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_shadow_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **shadow_size** = ``1`` :ref:`🔗<class_LabelSettings_property_shadow_size>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_shadow_size**\ (\ )

Kích thước của hiệu ứng bóng.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_outline_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **stacked_outline_count** = ``0`` :ref:`🔗<class_LabelSettings_property_stacked_outline_count>`

.. rst-class:: classref-property-setget

- |void| **set_stacked_outline_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_stacked_outline_count**\ (\ )

Số lượng đường viền xếp chồng.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_outline_{index}/color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **stacked_outline_{index}/color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_LabelSettings_property_stacked_outline_{index}/color>`

Màu của đường viền tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. stacked_outline_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_outline_{index}/size:

.. rst-class:: classref-property

:ref:`int<class_int>` **stacked_outline_{index}/size** = ``0`` :ref:`🔗<class_LabelSettings_property_stacked_outline_{index}/size>`

Kích thước của đường viền tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. stacked_outline_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_shadow_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **stacked_shadow_count** = ``0`` :ref:`🔗<class_LabelSettings_property_stacked_shadow_count>`

.. rst-class:: classref-property-setget

- |void| **set_stacked_shadow_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_stacked_shadow_count**\ (\ )

Số lượng bóng xếp chồng.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_shadow_{index}/color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **stacked_shadow_{index}/color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_LabelSettings_property_stacked_shadow_{index}/color>`

Màu của bóng tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. stacked_shadow_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_shadow_{index}/offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **stacked_shadow_{index}/offset** = ``Vector2(1, 1)`` :ref:`🔗<class_LabelSettings_property_stacked_shadow_{index}/offset>`

Độ lệch của bóng tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. stacked_shadow_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_property_stacked_shadow_{index}/outline_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **stacked_shadow_{index}/outline_size** = ``0`` :ref:`🔗<class_LabelSettings_property_stacked_shadow_{index}/outline_size>`

Kích thước đường viền của bóng tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. stacked_shadow_count - 1``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_LabelSettings_method_add_stacked_outline:

.. rst-class:: classref-method

|void| **add_stacked_outline**\ (\ index\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_LabelSettings_method_add_stacked_outline>`

Thêm một đường viền xếp chồng mới vào label tại ``index`` đã cho. Nếu ``index`` là ``-1``, đường viền xếp chồng mới sẽ được thêm vào cuối danh sách.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_add_stacked_shadow:

.. rst-class:: classref-method

|void| **add_stacked_shadow**\ (\ index\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_LabelSettings_method_add_stacked_shadow>`

Thêm một bóng xếp chồng mới vào label tại ``index`` đã cho. Nếu ``index`` là ``-1``, bóng xếp chồng mới sẽ được thêm vào cuối danh sách.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_get_stacked_outline_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_stacked_outline_color**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LabelSettings_method_get_stacked_outline_color>`

Trả về màu của đường viền xếp chồng tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_get_stacked_outline_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_stacked_outline_size**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LabelSettings_method_get_stacked_outline_size>`

Trả về kích thước của đường viền xếp chồng tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_get_stacked_shadow_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_stacked_shadow_color**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LabelSettings_method_get_stacked_shadow_color>`

Trả về màu của bóng xếp chồng tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_get_stacked_shadow_offset:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_stacked_shadow_offset**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LabelSettings_method_get_stacked_shadow_offset>`

Trả về độ lệch của bóng xếp chồng tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_get_stacked_shadow_outline_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_stacked_shadow_outline_size**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LabelSettings_method_get_stacked_shadow_outline_size>`

Trả về kích thước đường viền của bóng xếp chồng tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_move_stacked_outline:

.. rst-class:: classref-method

|void| **move_stacked_outline**\ (\ from_index\: :ref:`int<class_int>`, to_position\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_move_stacked_outline>`

Di chuyển đường viền xếp chồng tại chỉ mục ``from_index`` đến vị trí ``to_position`` đã cho trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_move_stacked_shadow:

.. rst-class:: classref-method

|void| **move_stacked_shadow**\ (\ from_index\: :ref:`int<class_int>`, to_position\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_move_stacked_shadow>`

Di chuyển bóng xếp chồng tại chỉ mục ``from_index`` đến vị trí ``to_position`` đã cho trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_remove_stacked_outline:

.. rst-class:: classref-method

|void| **remove_stacked_outline**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_remove_stacked_outline>`

Xóa đường viền xếp chồng tại chỉ mục ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_remove_stacked_shadow:

.. rst-class:: classref-method

|void| **remove_stacked_shadow**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_remove_stacked_shadow>`

Xóa bóng xếp chồng tại chỉ mục ``index``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_set_stacked_outline_color:

.. rst-class:: classref-method

|void| **set_stacked_outline_color**\ (\ index\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_LabelSettings_method_set_stacked_outline_color>`

Đặt màu của đường viền xếp chồng được xác định bởi ``index`` đã cho thành ``color``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_set_stacked_outline_size:

.. rst-class:: classref-method

|void| **set_stacked_outline_size**\ (\ index\: :ref:`int<class_int>`, size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_set_stacked_outline_size>`

Đặt kích thước của đường viền xếp chồng được xác định bởi ``index`` đã cho thành ``size``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_set_stacked_shadow_color:

.. rst-class:: classref-method

|void| **set_stacked_shadow_color**\ (\ index\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_LabelSettings_method_set_stacked_shadow_color>`

Đặt màu của bóng xếp chồng được xác định bởi ``index`` đã cho thành ``color``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_set_stacked_shadow_offset:

.. rst-class:: classref-method

|void| **set_stacked_shadow_offset**\ (\ index\: :ref:`int<class_int>`, offset\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_LabelSettings_method_set_stacked_shadow_offset>`

Đặt độ lệch của stacked shadow được xác định bởi ``index`` đã cho thành ``offset``.

.. rst-class:: classref-item-separator

----

.. _class_LabelSettings_method_set_stacked_shadow_outline_size:

.. rst-class:: classref-method

|void| **set_stacked_shadow_outline_size**\ (\ index\: :ref:`int<class_int>`, size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LabelSettings_method_set_stacked_shadow_outline_size>`

Đặt kích thước outline của stacked shadow được xác định bởi ``index`` đã cho thành ``size``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
