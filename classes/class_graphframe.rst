:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GraphFrame.xml.

.. _class_GraphFrame:

GraphFrame
==========

**Kế thừa:** :ref:`GraphElement<class_GraphElement>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

GraphFrame là một :ref:`GraphElement<class_GraphElement>` đặc biệt có thể được dùng để tổ chức các :ref:`GraphElement<class_GraphElement>`\ s khác bên trong một :ref:`GraphEdit<class_GraphEdit>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

GraphFrame là một :ref:`GraphElement<class_GraphElement>` đặc biệt mà các :ref:`GraphElement<class_GraphElement>`\ s khác có thể được gắn vào. Nó có thể được cấu hình để tự động thay đổi kích thước nhằm bao quanh tất cả :ref:`GraphElement<class_GraphElement>`\ s được gắn vào. Nếu frame được di chuyển, tất cả :ref:`GraphElement<class_GraphElement>`\ s được gắn vào bên trong nó cũng sẽ được di chuyển theo.

GraphFrame luôn được giữ phía sau lớp kết nối và các :ref:`GraphElement<class_GraphElement>`\ s khác bên trong một :ref:`GraphEdit<class_GraphEdit>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | :ref:`autoshrink_enabled<class_GraphFrame_property_autoshrink_enabled>` | ``true``                                                              |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                        | :ref:`autoshrink_margin<class_GraphFrame_property_autoshrink_margin>`   | ``40``                                                                |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                        | :ref:`drag_margin<class_GraphFrame_property_drag_margin>`               | ``16``                                                                |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>` | mouse_filter                                                            | ``0`` (overrides :ref:`Control<class_Control_property_mouse_filter>`) |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                    | :ref:`tint_color<class_GraphFrame_property_tint_color>`                 | ``Color(0.3, 0.3, 0.3, 0.75)``                                        |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | :ref:`tint_color_enabled<class_GraphFrame_property_tint_color_enabled>` | ``false``                                                             |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`String<class_String>`                  | :ref:`title<class_GraphFrame_property_title>`                           | ``""``                                                                |
   +----------------------------------------------+-------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`HBoxContainer<class_HBoxContainer>` | :ref:`get_titlebar_hbox<class_GraphFrame_method_get_titlebar_hbox>`\ (\ ) |
   +-------------------------------------------+---------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các thuộc tính giao diện
------------------------

.. table::
   :widths: auto

   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Color<class_Color>`       | :ref:`resizer_color<class_GraphFrame_theme_color_resizer_color>`         | ``Color(0.875, 0.875, 0.875, 1)`` |
   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`panel<class_GraphFrame_theme_style_panel>`                         |                                   |
   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`panel_selected<class_GraphFrame_theme_style_panel_selected>`       |                                   |
   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`titlebar<class_GraphFrame_theme_style_titlebar>`                   |                                   |
   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`titlebar_selected<class_GraphFrame_theme_style_titlebar_selected>` |                                   |
   +---------------------------------+--------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_GraphFrame_signal_autoshrink_changed:

.. rst-class:: classref-signal

**autoshrink_changed**\ (\ ) :ref:`🔗<class_GraphFrame_signal_autoshrink_changed>`

Được phát ra khi :ref:`autoshrink_enabled<class_GraphFrame_property_autoshrink_enabled>` hoặc :ref:`autoshrink_margin<class_GraphFrame_property_autoshrink_margin>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GraphFrame_property_autoshrink_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autoshrink_enabled** = ``true`` :ref:`🔗<class_GraphFrame_property_autoshrink_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_autoshrink_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_autoshrink_enabled**\ (\ )

Nếu ``true``, rect của frame sẽ được tự động điều chỉnh để bao quanh tất cả :ref:`GraphElement<class_GraphElement>`\ s được gắn vào.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_property_autoshrink_margin:

.. rst-class:: classref-property

:ref:`int<class_int>` **autoshrink_margin** = ``40`` :ref:`🔗<class_GraphFrame_property_autoshrink_margin>`

.. rst-class:: classref-property-setget

- |void| **set_autoshrink_margin**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_autoshrink_margin**\ (\ )

Lề xung quanh các node được gắn vào, được dùng để tính kích thước của frame khi :ref:`autoshrink_enabled<class_GraphFrame_property_autoshrink_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_property_drag_margin:

.. rst-class:: classref-property

:ref:`int<class_int>` **drag_margin** = ``16`` :ref:`🔗<class_GraphFrame_property_drag_margin>`

.. rst-class:: classref-property-setget

- |void| **set_drag_margin**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_drag_margin**\ (\ )

Lề bên trong frame có thể được dùng để kéo frame.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_property_tint_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **tint_color** = ``Color(0.3, 0.3, 0.3, 0.75)`` :ref:`🔗<class_GraphFrame_property_tint_color>`

.. rst-class:: classref-property-setget

- |void| **set_tint_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_tint_color**\ (\ )

Màu của frame khi :ref:`tint_color_enabled<class_GraphFrame_property_tint_color_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_property_tint_color_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **tint_color_enabled** = ``false`` :ref:`🔗<class_GraphFrame_property_tint_color_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_tint_color_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_tint_color_enabled**\ (\ )

Nếu ``true``, màu tint sẽ được dùng để tạo tint cho frame.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_property_title:

.. rst-class:: classref-property

:ref:`String<class_String>` **title** = ``""`` :ref:`🔗<class_GraphFrame_property_title>`

.. rst-class:: classref-property-setget

- |void| **set_title**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_title**\ (\ )

Tiêu đề của frame.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GraphFrame_method_get_titlebar_hbox:

.. rst-class:: classref-method

:ref:`HBoxContainer<class_HBoxContainer>` **get_titlebar_hbox**\ (\ ) :ref:`🔗<class_GraphFrame_method_get_titlebar_hbox>`

Trả về :ref:`HBoxContainer<class_HBoxContainer>` được dùng cho thanh tiêu đề, theo mặc định chỉ chứa một :ref:`Label<class_Label>` để hiển thị tiêu đề.

Có thể dùng phương thức này để thêm các control tùy chỉnh vào thanh tiêu đề, chẳng hạn như các nút tùy chọn hoặc đóng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính giao diện
--------------------------

.. _class_GraphFrame_theme_color_resizer_color:

.. rst-class:: classref-themeproperty

:ref:`Color<class_Color>` **resizer_color** = ``Color(0.875, 0.875, 0.875, 1)`` :ref:`🔗<class_GraphFrame_theme_color_resizer_color>`

Điều chế màu được áp dụng cho biểu tượng thay đổi kích thước.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_theme_style_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **panel** :ref:`🔗<class_GraphFrame_theme_style_panel>`

:ref:`StyleBox<class_StyleBox>` mặc định được dùng làm nền của **GraphFrame**.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_theme_style_panel_selected:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **panel_selected** :ref:`🔗<class_GraphFrame_theme_style_panel_selected>`

:ref:`StyleBox<class_StyleBox>` được dùng làm nền của **GraphFrame** khi nó được chọn.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_theme_style_titlebar:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **titlebar** :ref:`🔗<class_GraphFrame_theme_style_titlebar>`

:ref:`StyleBox<class_StyleBox>` được dùng cho thanh tiêu đề của **GraphFrame**.

.. rst-class:: classref-item-separator

----

.. _class_GraphFrame_theme_style_titlebar_selected:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **titlebar_selected** :ref:`🔗<class_GraphFrame_theme_style_titlebar_selected>`

:ref:`StyleBox<class_StyleBox>` được dùng cho thanh tiêu đề của **GraphFrame** khi nó được chọn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
