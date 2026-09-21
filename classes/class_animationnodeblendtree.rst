:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeBlendTree.xml.

.. _class_AnimationNodeBlendTree:

AnimationNodeBlendTree
======================

**Kế thừa:** :ref:`AnimationRootNode<class_AnimationRootNode>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A sub-tree of many type :ref:`AnimationNode<class_AnimationNode>`\ s used for complex animations. Used by :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Animation node này có thể chứa một cây con gồm bất kỳ loại animation node nào khác, chẳng hạn như :ref:`AnimationNodeTransition<class_AnimationNodeTransition>`, :ref:`AnimationNodeBlend2<class_AnimationNodeBlend2>`, :ref:`AnimationNodeBlend3<class_AnimationNodeBlend3>`, :ref:`AnimationNodeOneShot<class_AnimationNodeOneShot>`, v.v. Đây là một trong những root animation node được sử dụng phổ biến nhất.

Một node :ref:`AnimationNodeOutput<class_AnimationNodeOutput>` có tên ``output`` được tạo theo mặc định.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`graph_offset<class_AnimationNodeBlendTree_property_graph_offset>` | ``Vector2(0, 0)`` |
   +-------------------------------+-------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_node<class_AnimationNodeBlendTree_method_add_node>`\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`connect_node<class_AnimationNodeBlendTree_method_connect_node>`\ (\ input_node\: :ref:`StringName<class_StringName>`, input_index\: :ref:`int<class_int>`, output_node\: :ref:`StringName<class_StringName>`\ )       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`disconnect_node<class_AnimationNodeBlendTree_method_disconnect_node>`\ (\ input_node\: :ref:`StringName<class_StringName>`, input_index\: :ref:`int<class_int>`\ )                                                    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationNode<class_AnimationNode>`                        | :ref:`get_node<class_AnimationNodeBlendTree_method_get_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_node_list<class_AnimationNodeBlendTree_method_get_node_list>`\ (\ ) |const|                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                    | :ref:`get_node_position<class_AnimationNodeBlendTree_method_get_node_position>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_node<class_AnimationNodeBlendTree_method_has_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_node<class_AnimationNodeBlendTree_method_remove_node>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`rename_node<class_AnimationNodeBlendTree_method_rename_node>`\ (\ name\: :ref:`StringName<class_StringName>`, new_name\: :ref:`StringName<class_StringName>`\ )                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_node_position<class_AnimationNodeBlendTree_method_set_node_position>`\ (\ name\: :ref:`StringName<class_StringName>`, position\: :ref:`Vector2<class_Vector2>`\ )                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_AnimationNodeBlendTree_signal_node_changed:

.. rst-class:: classref-signal

**node_changed**\ (\ node_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_signal_node_changed>`

Được phát ra khi thông tin về input port thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_AnimationNodeBlendTree_constant_CONNECTION_OK:

.. rst-class:: classref-constant

**CONNECTION_OK** = ``0`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_OK>`

Kết nối thành công.

.. _class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_INPUT:

.. rst-class:: classref-constant

**CONNECTION_ERROR_NO_INPUT** = ``1`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_INPUT>`

Input node là ``null``.

.. _class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_INPUT_INDEX:

.. rst-class:: classref-constant

**CONNECTION_ERROR_NO_INPUT_INDEX** = ``2`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_INPUT_INDEX>`

Input port được chỉ định nằm ngoài phạm vi.

.. _class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_OUTPUT:

.. rst-class:: classref-constant

**CONNECTION_ERROR_NO_OUTPUT** = ``3`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_NO_OUTPUT>`

Output node là ``null``.

.. _class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_SAME_NODE:

.. rst-class:: classref-constant

**CONNECTION_ERROR_SAME_NODE** = ``4`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_SAME_NODE>`

Input node và output node giống nhau.

.. _class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_CONNECTION_EXISTS:

.. rst-class:: classref-constant

**CONNECTION_ERROR_CONNECTION_EXISTS** = ``5`` :ref:`🔗<class_AnimationNodeBlendTree_constant_CONNECTION_ERROR_CONNECTION_EXISTS>`

Kết nối được chỉ định đã tồn tại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeBlendTree_property_graph_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **graph_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_AnimationNodeBlendTree_property_graph_offset>`

.. rst-class:: classref-property-setget

- |void| **set_graph_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_graph_offset**\ (\ )

Offset toàn cục của tất cả sub animation node.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeBlendTree_method_add_node:

.. rst-class:: classref-method

|void| **add_node**\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_add_node>`

Thêm một :ref:`AnimationNode<class_AnimationNode>` tại ``position`` đã cho. ``name`` được dùng để xác định sub animation node đã tạo về sau.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_connect_node:

.. rst-class:: classref-method

|void| **connect_node**\ (\ input_node\: :ref:`StringName<class_StringName>`, input_index\: :ref:`int<class_int>`, output_node\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_connect_node>`

Kết nối output của một :ref:`AnimationNode<class_AnimationNode>` làm input cho một :ref:`AnimationNode<class_AnimationNode>` khác, tại input port được chỉ định bởi ``input_index``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_disconnect_node:

.. rst-class:: classref-method

|void| **disconnect_node**\ (\ input_node\: :ref:`StringName<class_StringName>`, input_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_disconnect_node>`

Ngắt kết nối animation node được kết nối với input đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_get_node:

.. rst-class:: classref-method

:ref:`AnimationNode<class_AnimationNode>` **get_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendTree_method_get_node>`

Trả về sub animation node có ``name`` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_get_node_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_node_list**\ (\ ) |const| :ref:`🔗<class_AnimationNodeBlendTree_method_get_node_list>`

Trả về danh sách chứa tên của tất cả sub animation node trong blend tree này.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_get_node_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_node_position**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendTree_method_get_node_position>`

Trả về vị trí của sub animation node có ``name`` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_has_node:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendTree_method_has_node>`

Trả về ``true`` nếu tồn tại sub animation node có ``name`` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_remove_node:

.. rst-class:: classref-method

|void| **remove_node**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_remove_node>`

Xóa một sub animation node.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_rename_node:

.. rst-class:: classref-method

|void| **rename_node**\ (\ name\: :ref:`StringName<class_StringName>`, new_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_rename_node>`

Thay đổi tên của một sub animation node.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendTree_method_set_node_position:

.. rst-class:: classref-method

|void| **set_node_position**\ (\ name\: :ref:`StringName<class_StringName>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_AnimationNodeBlendTree_method_set_node_position>`

Sửa đổi vị trí của một sub animation node.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
