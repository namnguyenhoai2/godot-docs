:github_url: hide

.. meta::
	:keywords: switch, toggle

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CheckButton.xml.

.. _class_CheckButton:

CheckButton
===========

**Kế thừa:** :ref:`Button<class_Button>` **<** :ref:`BaseButton<class_BaseButton>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một nút biểu thị một lựa chọn nhị phân.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CheckButton** là một nút chuyển đổi được hiển thị dưới dạng ô kiểm. Chức năng của nó tương tự :ref:`CheckBox<class_CheckBox>`, nhưng có giao diện khác. Để tuân theo các mẫu UX đã được thiết lập, bạn nên sử dụng **CheckButton** khi việc bật/tắt nó có **tác động ngay lập tức** đến một thành phần nào đó. Ví dụ: có thể sử dụng nó khi việc nhấn nút sẽ hiển thị hoặc ẩn các cài đặt nâng cao mà không yêu cầu người dùng xác nhận hành động này.

Xem thêm :ref:`BaseButton<class_BaseButton>`, trong đó chứa các thuộc tính và phương thức phổ biến liên quan đến node này.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+-------------+-------------------------------------------------------------------------------+
   | :ref:`HorizontalAlignment<enum_@GlobalScope_HorizontalAlignment>` | alignment   | ``0`` (overrides :ref:`Button<class_Button_property_alignment>`)              |
   +-------------------------------------------------------------------+-------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | toggle_mode | ``true`` (overrides :ref:`BaseButton<class_BaseButton_property_toggle_mode>`) |
   +-------------------------------------------------------------------+-------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`         | :ref:`button_checked_color<class_CheckButton_theme_color_button_checked_color>`              | ``Color(1, 1, 1, 1)`` |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`         | :ref:`button_unchecked_color<class_CheckButton_theme_color_button_unchecked_color>`          | ``Color(1, 1, 1, 1)`` |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`             | :ref:`check_v_offset<class_CheckButton_theme_constant_check_v_offset>`                       | ``0``                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`checked<class_CheckButton_theme_icon_checked>`                                         |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`checked_disabled<class_CheckButton_theme_icon_checked_disabled>`                       |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`checked_disabled_mirrored<class_CheckButton_theme_icon_checked_disabled_mirrored>`     |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`checked_mirrored<class_CheckButton_theme_icon_checked_mirrored>`                       |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`unchecked<class_CheckButton_theme_icon_unchecked>`                                     |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`unchecked_disabled<class_CheckButton_theme_icon_unchecked_disabled>`                   |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`unchecked_disabled_mirrored<class_CheckButton_theme_icon_unchecked_disabled_mirrored>` |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`unchecked_mirrored<class_CheckButton_theme_icon_unchecked_mirrored>`                   |                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_CheckButton_theme_color_button_checked_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **button_checked_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_CheckButton_theme_color_button_checked_color>`

Màu của biểu tượng đã chọn khi ô kiểm được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_color_button_unchecked_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **button_unchecked_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_CheckButton_theme_color_button_unchecked_color>`

Màu của biểu tượng chưa chọn khi ô kiểm không được nhấn.

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_constant_check_v_offset:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **check_v_offset** = ``0`` :ref:`🔗<class_CheckButton_theme_constant_check_v_offset>`

Độ lệch dọc được sử dụng khi kết xuất các biểu tượng chuyển đổi (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_checked:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **checked** :ref:`🔗<class_CheckButton_theme_icon_checked>`

Biểu tượng hiển thị khi **CheckButton** được chọn (đối với bố cục từ trái sang phải).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_checked_disabled:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **checked_disabled** :ref:`🔗<class_CheckButton_theme_icon_checked_disabled>`

Biểu tượng hiển thị khi **CheckButton** được chọn và bị vô hiệu hóa (đối với bố cục từ trái sang phải).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_checked_disabled_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **checked_disabled_mirrored** :ref:`🔗<class_CheckButton_theme_icon_checked_disabled_mirrored>`

Biểu tượng hiển thị khi **CheckButton** được chọn và bị vô hiệu hóa (đối với bố cục từ phải sang trái).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_checked_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **checked_mirrored** :ref:`🔗<class_CheckButton_theme_icon_checked_mirrored>`

Biểu tượng hiển thị khi **CheckButton** được chọn (đối với bố cục từ phải sang trái).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_unchecked:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **unchecked** :ref:`🔗<class_CheckButton_theme_icon_unchecked>`

Biểu tượng hiển thị khi **CheckButton** không được chọn (đối với bố cục từ trái sang phải).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_unchecked_disabled:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **unchecked_disabled** :ref:`🔗<class_CheckButton_theme_icon_unchecked_disabled>`

Biểu tượng hiển thị khi **CheckButton** không được chọn và bị vô hiệu hóa (đối với bố cục từ trái sang phải).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_unchecked_disabled_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **unchecked_disabled_mirrored** :ref:`🔗<class_CheckButton_theme_icon_unchecked_disabled_mirrored>`

Biểu tượng hiển thị khi **CheckButton** không được chọn và bị vô hiệu hóa (đối với bố cục từ phải sang trái).

.. rst-class:: classref-item-separator

----

.. _class_CheckButton_theme_icon_unchecked_mirrored:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **unchecked_mirrored** :ref:`🔗<class_CheckButton_theme_icon_unchecked_mirrored>`

Biểu tượng hiển thị khi **CheckButton** không được chọn (đối với bố cục từ phải sang trái).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
