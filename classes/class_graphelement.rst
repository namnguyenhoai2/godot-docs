:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GraphElement.xml.

.. _class_GraphElement:

GraphElement
============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GraphFrame<class_GraphFrame>`, :ref:`GraphNode<class_GraphNode>`

Một container biểu diễn một phần tử cơ bản có thể được đặt bên trong một control :ref:`GraphEdit<class_GraphEdit>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**GraphElement** cho phép tạo các phần tử tùy chỉnh cho graph :ref:`GraphEdit<class_GraphEdit>`. Theo mặc định, các phần tử này có thể được chọn, thay đổi kích thước và định vị lại, nhưng không thể kết nối. Để xem một phần tử graph cho phép kết nối, hãy xem :ref:`GraphNode<class_GraphNode>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`draggable<class_GraphElement_property_draggable>`             | ``true``          |
   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`position_offset<class_GraphElement_property_position_offset>` | ``Vector2(0, 0)`` |
   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`resizable<class_GraphElement_property_resizable>`             | ``false``         |
   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`scaling_menus<class_GraphElement_property_scaling_menus>`     | ``false``         |
   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`selectable<class_GraphElement_property_selectable>`           | ``true``          |
   +-------------------------------+---------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`selected<class_GraphElement_property_selected>`               | ``false``         |
   +-------------------------------+---------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------------------+-------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`resizer<class_GraphElement_theme_icon_resizer>` |
   +-----------------------------------+-------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_GraphElement_signal_delete_request:

.. rst-class:: classref-signal

**delete_request**\ (\ ) :ref:`🔗<class_GraphElement_signal_delete_request>`

Được phát ra khi có yêu cầu xóa GraphElement.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_dragged:

.. rst-class:: classref-signal

**dragged**\ (\ from\: :ref:`Vector2<class_Vector2>`, to\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_GraphElement_signal_dragged>`

Được phát ra khi GraphElement được kéo.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_node_deselected:

.. rst-class:: classref-signal

**node_deselected**\ (\ ) :ref:`🔗<class_GraphElement_signal_node_deselected>`

Được phát ra khi GraphElement bị bỏ chọn.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_node_selected:

.. rst-class:: classref-signal

**node_selected**\ (\ ) :ref:`🔗<class_GraphElement_signal_node_selected>`

Được phát ra khi GraphElement được chọn.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_position_offset_changed:

.. rst-class:: classref-signal

**position_offset_changed**\ (\ ) :ref:`🔗<class_GraphElement_signal_position_offset_changed>`

Được phát ra khi GraphElement được di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_raise_request:

.. rst-class:: classref-signal

**raise_request**\ (\ ) :ref:`🔗<class_GraphElement_signal_raise_request>`

Được phát ra khi có yêu cầu hiển thị GraphElement phía trên các phần tử khác. Điều này xảy ra khi GraphElement được focus (nhấp vào).

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_resize_end:

.. rst-class:: classref-signal

**resize_end**\ (\ new_size\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_GraphElement_signal_resize_end>`

Được phát ra khi thả nút chuột sau khi kéo handle thay đổi kích thước (xem :ref:`resizable<class_GraphElement_property_resizable>`).

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_signal_resize_request:

.. rst-class:: classref-signal

**resize_request**\ (\ new_size\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_GraphElement_signal_resize_request>`

Được phát ra khi có yêu cầu thay đổi kích thước GraphElement. Điều này xảy ra khi kéo handle thay đổi kích thước (xem :ref:`resizable<class_GraphElement_property_resizable>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GraphElement_property_draggable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **draggable** = ``true`` :ref:`🔗<class_GraphElement_property_draggable>`

.. rst-class:: classref-property-setget

- |void| **set_draggable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_draggable**\ (\ )

Nếu ``true``, người dùng có thể kéo GraphElement.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_property_position_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_GraphElement_property_position_offset>`

.. rst-class:: classref-property-setget

- |void| **set_position_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position_offset**\ (\ )

Độ lệch của GraphElement so với độ lệch cuộn của :ref:`GraphEdit<class_GraphEdit>`.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_property_resizable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **resizable** = ``false`` :ref:`🔗<class_GraphElement_property_resizable>`

.. rst-class:: classref-property-setget

- |void| **set_resizable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_resizable**\ (\ )

Nếu ``true``, người dùng có thể thay đổi kích thước GraphElement.

\ **Lưu ý:** Việc kéo handle sẽ chỉ phát ra các signal :ref:`resize_request<class_GraphElement_signal_resize_request>` và :ref:`resize_end<class_GraphElement_signal_resize_end>`, GraphElement cần được thay đổi kích thước thủ công.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_property_scaling_menus:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **scaling_menus** = ``false`` :ref:`🔗<class_GraphElement_property_scaling_menus>`

.. rst-class:: classref-property-setget

- |void| **set_scaling_menus**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_scaling_menus**\ (\ )

Nếu ``true``, các :ref:`PopupMenu<class_PopupMenu>`\ s là hậu duệ của GraphElement sẽ được scale theo zoom :ref:`GraphEdit<class_GraphEdit>`.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_property_selectable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **selectable** = ``true`` :ref:`🔗<class_GraphElement_property_selectable>`

.. rst-class:: classref-property-setget

- |void| **set_selectable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_selectable**\ (\ )

Nếu ``true``, người dùng có thể chọn GraphElement.

.. rst-class:: classref-item-separator

----

.. _class_GraphElement_property_selected:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **selected** = ``false`` :ref:`🔗<class_GraphElement_property_selected>`

.. rst-class:: classref-property-setget

- |void| **set_selected**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_selected**\ (\ )

Nếu ``true``, GraphElement được chọn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_GraphElement_theme_icon_resizer:

.. rst-class:: classref-themeproperty

:ref:`Texture2D<class_Texture2D>` **resizer** :ref:`🔗<class_GraphElement_theme_icon_resizer>`

Biểu tượng được sử dụng cho resizer, hiển thị khi :ref:`resizable<class_GraphElement_property_resizable>` được bật.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
