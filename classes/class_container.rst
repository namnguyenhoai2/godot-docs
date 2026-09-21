:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Container.xml.

.. _class_Container:

Container
=========

**Kế thừa:** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AspectRatioContainer<class_AspectRatioContainer>`, :ref:`BoxContainer<class_BoxContainer>`, :ref:`CenterContainer<class_CenterContainer>`, :ref:`EditorProperty<class_EditorProperty>`, :ref:`FlowContainer<class_FlowContainer>`, :ref:`FoldableContainer<class_FoldableContainer>`, :ref:`GraphElement<class_GraphElement>`, :ref:`GridContainer<class_GridContainer>`, :ref:`MarginContainer<class_MarginContainer>`, :ref:`PanelContainer<class_PanelContainer>`, :ref:`ScrollContainer<class_ScrollContainer>`, :ref:`SplitContainer<class_SplitContainer>`, :ref:`SubViewportContainer<class_SubViewportContainer>`, :ref:`TabContainer<class_TabContainer>`

Lớp cơ sở cho tất cả container GUI.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho tất cả container GUI. Một **Container** sẽ tự động sắp xếp các control con theo một cách nhất định. Có thể kế thừa lớp này để tạo các loại container tùy chỉnh.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using Containers <../tutorials/ui/gui_containers>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +----------------------------------------------+----------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | :ref:`accessibility_region<class_Container_property_accessibility_region>` | ``false``                                                                          |
   +----------------------------------------------+----------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>` | mouse_filter                                                               | ``1`` (overrides :ref:`Control<class_Control_property_mouse_filter>`)              |
   +----------------------------------------------+----------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | propagate_maximum_size                                                     | ``true`` (overrides :ref:`Control<class_Control_property_propagate_maximum_size>`) |
   +----------------------------------------------+----------------------------------------------------------------------------+------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`_get_allowed_size_flags_horizontal<class_Container_private_method__get_allowed_size_flags_horizontal>`\ (\ ) |virtual| |const|              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`_get_allowed_size_flags_vertical<class_Container_private_method__get_allowed_size_flags_vertical>`\ (\ ) |virtual| |const|                  |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`fit_child_in_rect<class_Container_method_fit_child_in_rect>`\ (\ child\: :ref:`Control<class_Control>`, rect\: :ref:`Rect2<class_Rect2>`\ ) |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`queue_sort<class_Container_method_queue_sort>`\ (\ )                                                                                        |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_Container_signal_pre_sort_children:

.. rst-class:: classref-signal

**pre_sort_children**\ (\ ) :ref:`🔗<class_Container_signal_pre_sort_children>`

Được phát ra khi các node con sắp được sắp xếp.

.. rst-class:: classref-item-separator

----

.. _class_Container_signal_sort_children:

.. rst-class:: classref-signal

**sort_children**\ (\ ) :ref:`🔗<class_Container_signal_sort_children>`

Được phát ra khi cần sắp xếp các node con.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_Container_constant_NOTIFICATION_PRE_SORT_CHILDREN:

.. rst-class:: classref-constant

**NOTIFICATION_PRE_SORT_CHILDREN** = ``50`` :ref:`🔗<class_Container_constant_NOTIFICATION_PRE_SORT_CHILDREN>`

Thông báo ngay trước khi các node con sắp được sắp xếp, trong trường hợp cần xử lý trước một việc nào đó.

.. _class_Container_constant_NOTIFICATION_SORT_CHILDREN:

.. rst-class:: classref-constant

**NOTIFICATION_SORT_CHILDREN** = ``51`` :ref:`🔗<class_Container_constant_NOTIFICATION_SORT_CHILDREN>`

Thông báo khi sắp xếp các node con; thông báo này phải được tuân theo ngay lập tức.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Container_property_accessibility_region:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **accessibility_region** = ``false`` :ref:`🔗<class_Container_property_accessibility_region>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_region**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_accessibility_region**\ (\ )

Nếu ``true``, container này được đánh dấu là một vùng dành cho accessibility. Sử dụng :ref:`Control.accessibility_name<class_Control_property_accessibility_name>` để đặt tên mô tả cho vùng. Trình đọc màn hình có thể điều hướng giữa các vùng bằng cách sử dụng điều hướng landmark.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Container_private_method__get_allowed_size_flags_horizontal:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **_get_allowed_size_flags_horizontal**\ (\ ) |virtual| |const| :ref:`🔗<class_Container_private_method__get_allowed_size_flags_horizontal>`

Triển khai để trả về danh sách các :ref:`SizeFlags<enum_Control_SizeFlags>` ngang được phép cho các node con. Về mặt kỹ thuật, điều này không ngăn việc sử dụng bất kỳ cờ kích thước nào khác nếu triển khai của bạn yêu cầu. Điều này chỉ giới hạn các tùy chọn có sẵn cho người dùng trong dock Inspector.

\ **Lưu ý:** Không có cờ kích thước tương đương với việc có :ref:`Control.SIZE_SHRINK_BEGIN<class_Control_constant_SIZE_SHRINK_BEGIN>`. Do đó, giá trị này luôn được cho phép một cách ngầm định.

.. rst-class:: classref-item-separator

----

.. _class_Container_private_method__get_allowed_size_flags_vertical:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **_get_allowed_size_flags_vertical**\ (\ ) |virtual| |const| :ref:`🔗<class_Container_private_method__get_allowed_size_flags_vertical>`

Triển khai để trả về danh sách các :ref:`SizeFlags<enum_Control_SizeFlags>` dọc được phép cho các node con. Về mặt kỹ thuật, điều này không ngăn việc sử dụng bất kỳ cờ kích thước nào khác nếu triển khai của bạn yêu cầu. Điều này chỉ giới hạn các tùy chọn có sẵn cho người dùng trong dock Inspector.

\ **Lưu ý:** Không có cờ kích thước tương đương với việc có :ref:`Control.SIZE_SHRINK_BEGIN<class_Control_constant_SIZE_SHRINK_BEGIN>`. Do đó, giá trị này luôn được cho phép một cách ngầm định.

.. rst-class:: classref-item-separator

----

.. _class_Container_method_fit_child_in_rect:

.. rst-class:: classref-method

|void| **fit_child_in_rect**\ (\ child\: :ref:`Control<class_Control>`, rect\: :ref:`Rect2<class_Rect2>`\ ) :ref:`🔗<class_Container_method_fit_child_in_rect>`

Điều chỉnh một control con nằm trong rect đã cho. Đây chủ yếu là một helper để tạo các lớp container tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Container_method_queue_sort:

.. rst-class:: classref-method

|void| **queue_sort**\ (\ ) :ref:`🔗<class_Container_method_queue_sort>`

Đưa việc sắp xếp lại các node con chứa bên trong vào hàng đợi. Việc này vốn được tự động gọi, nhưng cũng có thể được gọi theo yêu cầu.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
