:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PopupPanel.xml.

.. _class_PopupPanel:

PopupPanel
==========

**Kế thừa:** :ref:`Popup<class_Popup>` **<** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một popup có nền panel.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một popup có nền panel có thể cấu hình. Mọi control con được thêm vào node này sẽ được kéo giãn để vừa với kích thước của panel (tương tự như cách :ref:`PanelContainer<class_PanelContainer>` hoạt động). Nếu bạn đang tạo cửa sổ, hãy xem :ref:`Window<class_Window>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------------------+------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`DefaultCanvasItemTextureFilter<enum_Viewport_DefaultCanvasItemTextureFilter>` | canvas_item_default_texture_filter | ``4`` (overrides :ref:`Viewport<class_Viewport_property_canvas_item_default_texture_filter>`) |
   +-------------------------------------------------------------------------------------+------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`DefaultCanvasItemTextureRepeat<enum_Viewport_DefaultCanvasItemTextureRepeat>` | canvas_item_default_texture_repeat | ``3`` (overrides :ref:`Viewport<class_Viewport_property_canvas_item_default_texture_repeat>`) |
   +-------------------------------------------------------------------------------------+------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                             | transparent                        | ``true`` (overrides :ref:`Window<class_Window_property_transparent>`)                         |
   +-------------------------------------------------------------------------------------+------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                             | transparent_bg                     | ``true`` (overrides :ref:`Viewport<class_Viewport_property_transparent_bg>`)                  |
   +-------------------------------------------------------------------------------------+------------------------------------+-----------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các thuộc tính Theme
--------------------

.. table::
   :widths: auto

   +---------------------------------+--------------------------------------------------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`panel<class_PopupPanel_theme_style_panel>` |
   +---------------------------------+--------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các thuộc tính Theme
--------------------------

.. _class_PopupPanel_theme_style_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **panel** :ref:`🔗<class_PopupPanel_theme_style_panel>`

:ref:`StyleBox<class_StyleBox>` cho panel nền.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
