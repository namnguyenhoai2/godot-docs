:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorSelection.xml.

.. _class_EditorSelection:

EditorSelection
===============

**Kế thừa:** :ref:`Object<class_Object>`

Quản lý lựa chọn SceneTree trong editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng này quản lý lựa chọn SceneTree trong editor.

\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Thay vào đó, hãy truy cập singleton bằng :ref:`EditorInterface.get_selection()<class_EditorInterface_method_get_selection>`.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | |void|                                               | :ref:`add_node<class_EditorSelection_method_add_node>`\ (\ node\: :ref:`Node<class_Node>`\ )                 |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | |void|                                               | :ref:`clear<class_EditorSelection_method_clear>`\ (\ )                                                       |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] | :ref:`get_selected_nodes<class_EditorSelection_method_get_selected_nodes>`\ (\ )                             |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] | :ref:`get_top_selected_nodes<class_EditorSelection_method_get_top_selected_nodes>`\ (\ )                     |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] | :ref:`get_transformable_selected_nodes<class_EditorSelection_method_get_transformable_selected_nodes>`\ (\ ) |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+
   | |void|                                               | :ref:`remove_node<class_EditorSelection_method_remove_node>`\ (\ node\: :ref:`Node<class_Node>`\ )           |
   +------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_EditorSelection_signal_selection_changed:

.. rst-class:: classref-signal

**selection_changed**\ (\ ) :ref:`🔗<class_EditorSelection_signal_selection_changed>`

Được phát khi lựa chọn thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_EditorSelection_method_add_node:

.. rst-class:: classref-method

|void| **add_node**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_EditorSelection_method_add_node>`

Thêm một node vào lựa chọn.

\ **Lưu ý:** Node mới được chọn sẽ không tự động được chỉnh sửa trong inspector. Nếu muốn chỉnh sửa một node, hãy sử dụng :ref:`EditorInterface.edit_node()<class_EditorInterface_method_edit_node>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorSelection_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_EditorSelection_method_clear>`

Xóa lựa chọn.

.. rst-class:: classref-item-separator

----

.. _class_EditorSelection_method_get_selected_nodes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] **get_selected_nodes**\ (\ ) :ref:`🔗<class_EditorSelection_method_get_selected_nodes>`

Trả về danh sách các node đã chọn.

.. rst-class:: classref-item-separator

----

.. _class_EditorSelection_method_get_top_selected_nodes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] **get_top_selected_nodes**\ (\ ) :ref:`🔗<class_EditorSelection_method_get_top_selected_nodes>`

Chỉ trả về danh sách các node cấp cao nhất đã chọn, không bao gồm bất kỳ node con nào. Điều này hữu ích khi thực hiện các thao tác transform (di chuyển, xoay, v.v.).

Ví dụ: nếu có một node A với node con B và node cùng cấp C, việc chọn cả ba sẽ khiến method này chỉ trả về A và C. Việc thay đổi transform toàn cục của A sẽ ảnh hưởng đến transform toàn cục của B, vì vậy không cần thay đổi B riêng biệt.

.. rst-class:: classref-item-separator

----

.. _class_EditorSelection_method_get_transformable_selected_nodes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] **get_transformable_selected_nodes**\ (\ ) :ref:`🔗<class_EditorSelection_method_get_transformable_selected_nodes>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`get_top_selected_nodes()<class_EditorSelection_method_get_top_selected_nodes>`.

Chỉ trả về danh sách các node cấp cao nhất đã chọn, không bao gồm bất kỳ node con nào. Điều này hữu ích khi thực hiện các thao tác transform (di chuyển, xoay, v.v.). Xem :ref:`get_top_selected_nodes()<class_EditorSelection_method_get_top_selected_nodes>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorSelection_method_remove_node:

.. rst-class:: classref-method

|void| **remove_node**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_EditorSelection_method_remove_node>`

Xóa một node khỏi lựa chọn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
