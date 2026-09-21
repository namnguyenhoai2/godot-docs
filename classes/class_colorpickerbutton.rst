:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ColorPickerButton.xml.

.. _class_ColorPickerButton:

ColorPickerButton
=================

**Kế thừa:** :ref:`Button<class_Button>` **<** :ref:`BaseButton<class_BaseButton>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một nút mở :ref:`ColorPicker<class_ColorPicker>` khi được nhấn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đóng gói một :ref:`ColorPicker<class_ColorPicker>`, cho phép truy cập bằng cách nhấn một nút. Nhấn nút sẽ bật/tắt khả năng hiển thị của :ref:`ColorPicker<class_ColorPicker>`.

Xem thêm :ref:`BaseButton<class_BaseButton>`, nơi chứa các thuộc tính và phương thức phổ biến liên quan đến node này.

\ **Lưu ý:** Theo mặc định, nút có thể không đủ rộng để hiển thị ô xem trước màu. Hãy đảm bảo đặt :ref:`Control.custom_minimum_size<class_Control_property_custom_minimum_size>` thành một giá trị đủ lớn để cung cấp đủ không gian cho nút.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `2D GD Paint Demo <https://godotengine.org/asset-library/asset/2768>`__

- `GUI Drag And Drop Demo <https://godotengine.org/asset-library/asset/2767>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>` | :ref:`color<class_ColorPickerButton_property_color>`                   | ``Color(0, 0, 0, 1)``                                                         |
   +---------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`edit_alpha<class_ColorPickerButton_property_edit_alpha>`         | ``true``                                                                      |
   +---------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`edit_intensity<class_ColorPickerButton_property_edit_intensity>` | ``true``                                                                      |
   +---------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | toggle_mode                                                            | ``true`` (overrides :ref:`BaseButton<class_BaseButton_property_toggle_mode>`) |
   +---------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+--------------------------------------------------------------------+
   | :ref:`ColorPicker<class_ColorPicker>` | :ref:`get_picker<class_ColorPickerButton_method_get_picker>`\ (\ ) |
   +---------------------------------------+--------------------------------------------------------------------+
   | :ref:`PopupPanel<class_PopupPanel>`   | :ref:`get_popup<class_ColorPickerButton_method_get_popup>`\ (\ )   |
   +---------------------------------------+--------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính giao diện
--------------------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`bg<class_ColorPickerButton_theme_icon_bg>` |
   +-----------------------------------+--------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_ColorPickerButton_signal_color_changed:

.. rst-class:: classref-signal

**color_changed**\ (\ color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_ColorPickerButton_signal_color_changed>`

Được phát ra khi màu thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_ColorPickerButton_signal_picker_created:

.. rst-class:: classref-signal

**picker_created**\ (\ ) :ref:`🔗<class_ColorPickerButton_signal_picker_created>`

Được phát ra khi :ref:`ColorPicker<class_ColorPicker>` được tạo (nút được nhấn lần đầu tiên).

.. rst-class:: classref-item-separator

----

.. _class_ColorPickerButton_signal_popup_closed:

.. rst-class:: classref-signal

**popup_closed**\ (\ ) :ref:`🔗<class_ColorPickerButton_signal_popup_closed>`

Được phát ra khi :ref:`ColorPicker<class_ColorPicker>` bị đóng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ColorPickerButton_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_ColorPickerButton_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_pick_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_pick_color**\ (\ )

Màu hiện đang được chọn.

.. rst-class:: classref-item-separator

----

.. _class_ColorPickerButton_property_edit_alpha:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **edit_alpha** = ``true`` :ref:`🔗<class_ColorPickerButton_property_edit_alpha>`

.. rst-class:: classref-property-setget

- |void| **set_edit_alpha**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editing_alpha**\ (\ )

Nếu ``true``, kênh alpha trong :ref:`ColorPicker<class_ColorPicker>` đang hiển thị sẽ được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_ColorPickerButton_property_edit_intensity:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **edit_intensity** = ``true`` :ref:`🔗<class_ColorPickerButton_property_edit_intensity>`

.. rst-class:: classref-property-setget

- |void| **set_edit_intensity**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editing_intensity**\ (\ )

Nếu ``true``, thanh trượt cường độ trong :ref:`ColorPicker<class_ColorPicker>` đang hiển thị sẽ được hiển thị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ColorPickerButton_method_get_picker:

.. rst-class:: classref-method

:ref:`ColorPicker<class_ColorPicker>` **get_picker**\ (\ ) :ref:`🔗<class_ColorPickerButton_method_get_picker>`

Trả về :ref:`ColorPicker<class_ColorPicker>` mà node này bật/tắt.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng nó có thể gây crash. Nếu bạn muốn ẩn nó hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_ColorPickerButton_method_get_popup:

.. rst-class:: classref-method

:ref:`PopupPanel<class_PopupPanel>` **get_popup**\ (\ ) :ref:`🔗<class_ColorPickerButton_method_get_popup>`

Trả về :ref:`PopupPanel<class_PopupPanel>` của control, cho phép bạn kết nối với các tín hiệu popup. Điều này cho phép bạn xử lý các sự kiện khi ColorPicker được hiển thị hoặc ẩn.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng nó có thể gây crash. Nếu bạn muốn ẩn nó hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`Window.visible<class_Window_property_visible>` của chúng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính giao diện
--------------------------

.. _class_ColorPickerButton_theme_icon_bg:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **bg** :ref:`🔗<class_ColorPickerButton_theme_icon_bg>`

Nền của hình chữ nhật xem trước màu trên nút.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
