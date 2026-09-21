:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeBlendSpace1D.xml.

.. _class_AnimationNodeBlendSpace1D:

AnimationNodeBlendSpace1D
=========================

**Kế thừa:** :ref:`AnimationRootNode<class_AnimationRootNode>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A set of :ref:`AnimationRootNode<class_AnimationRootNode>`\ s placed on a virtual axis, crossfading between the two adjacent ones. Used by :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource được :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>` sử dụng.

\ **AnimationNodeBlendSpace1D** represents a virtual axis on which any type of :ref:`AnimationRootNode<class_AnimationRootNode>`\ s can be added using :ref:`add_blend_point()<class_AnimationNodeBlendSpace1D_method_add_blend_point>`. Outputs the linear blend of the two :ref:`AnimationRootNode<class_AnimationRootNode>`\ s adjacent to the current value.

Bạn có thể thiết lập phạm vi của trục bằng :ref:`min_space<class_AnimationNodeBlendSpace1D_property_min_space>` và :ref:`max_space<class_AnimationNodeBlendSpace1D_property_max_space>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` | :ref:`blend_mode<class_AnimationNodeBlendSpace1D_property_blend_mode>`       | ``0``       |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                  | :ref:`cyclic_length<class_AnimationNodeBlendSpace1D_property_cyclic_length>` | ``0.0``     |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                  | :ref:`max_space<class_AnimationNodeBlendSpace1D_property_max_space>`         | ``1.0``     |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                  | :ref:`min_space<class_AnimationNodeBlendSpace1D_property_min_space>`         | ``-1.0``    |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>`                                  | :ref:`snap<class_AnimationNodeBlendSpace1D_property_snap>`                   | ``0.1``     |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`bool<class_bool>`                                    | :ref:`sync<class_AnimationNodeBlendSpace1D_property_sync>`                   |             |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>`   | :ref:`sync_mode<class_AnimationNodeBlendSpace1D_property_sync_mode>`         | ``0``       |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+
   | :ref:`String<class_String>`                                | :ref:`value_label<class_AnimationNodeBlendSpace1D_property_value_label>`     | ``"value"`` |
   +------------------------------------------------------------+------------------------------------------------------------------------------+-------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_blend_point<class_AnimationNodeBlendSpace1D_method_add_blend_point>`\ (\ node\: :ref:`AnimationRootNode<class_AnimationRootNode>`, pos\: :ref:`float<class_float>`, at_index\: :ref:`int<class_int>` = -1, name\: :ref:`StringName<class_StringName>` = &""\ ) |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`find_blend_point_by_name<class_AnimationNodeBlendSpace1D_method_find_blend_point_by_name>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                               |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_blend_point_count<class_AnimationNodeBlendSpace1D_method_get_blend_point_count>`\ (\ ) |const|                                                                                                                                                                 |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`               | :ref:`get_blend_point_name<class_AnimationNodeBlendSpace1D_method_get_blend_point_name>`\ (\ point\: :ref:`int<class_int>`\ ) |const|                                                                                                                                    |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationRootNode<class_AnimationRootNode>` | :ref:`get_blend_point_node<class_AnimationNodeBlendSpace1D_method_get_blend_point_node>`\ (\ point\: :ref:`int<class_int>`\ ) |const|                                                                                                                                    |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                         | :ref:`get_blend_point_position<class_AnimationNodeBlendSpace1D_method_get_blend_point_position>`\ (\ point\: :ref:`int<class_int>`\ ) |const|                                                                                                                            |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`remove_blend_point<class_AnimationNodeBlendSpace1D_method_remove_blend_point>`\ (\ point\: :ref:`int<class_int>`\ )                                                                                                                                                |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`reorder_blend_point<class_AnimationNodeBlendSpace1D_method_reorder_blend_point>`\ (\ from_index\: :ref:`int<class_int>`, to_index\: :ref:`int<class_int>`\ )                                                                                                       |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_blend_point_name<class_AnimationNodeBlendSpace1D_method_set_blend_point_name>`\ (\ point\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ )                                                                                                |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_blend_point_node<class_AnimationNodeBlendSpace1D_method_set_blend_point_node>`\ (\ point\: :ref:`int<class_int>`, node\: :ref:`AnimationRootNode<class_AnimationRootNode>`\ )                                                                                  |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_blend_point_position<class_AnimationNodeBlendSpace1D_method_set_blend_point_position>`\ (\ point\: :ref:`int<class_int>`, pos\: :ref:`float<class_float>`\ )                                                                                                   |
   +---------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationNodeBlendSpace1D_BlendMode:

.. rst-class:: classref-enumeration

enum **BlendMode**: :ref:`🔗<enum_AnimationNodeBlendSpace1D_BlendMode>`

.. _class_AnimationNodeBlendSpace1D_constant_BLEND_MODE_INTERPOLATED:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` **BLEND_MODE_INTERPOLATED** = ``0``

Phép nội suy giữa các animation là tuyến tính.

.. _class_AnimationNodeBlendSpace1D_constant_BLEND_MODE_DISCRETE:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` **BLEND_MODE_DISCRETE** = ``1``

Blend space phát animation của animation node có vị trí blend gần nhất. Hữu ích cho các animation 2D theo từng khung hình.

.. _class_AnimationNodeBlendSpace1D_constant_BLEND_MODE_DISCRETE_CARRY:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` **BLEND_MODE_DISCRETE_CARRY** = ``2``

Tương tự :ref:`BLEND_MODE_DISCRETE<class_AnimationNodeBlendSpace1D_constant_BLEND_MODE_DISCRETE>`, nhưng bắt đầu animation mới tại vị trí phát của animation trước đó.

.. rst-class:: classref-item-separator

----

.. _enum_AnimationNodeBlendSpace1D_SyncMode:

.. rst-class:: classref-enumeration

enum **SyncMode**: :ref:`🔗<enum_AnimationNodeBlendSpace1D_SyncMode>`

.. _class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **SYNC_MODE_NONE** = ``0``

Các animation không hoạt động bị đóng băng và không tiến triển.

.. _class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_INDEPENDENT:

.. rst-class:: classref-enumeration-constant

:ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **SYNC_MODE_INDEPENDENT** = ``1``

Các animation không hoạt động tiến triển với weight bằng ``0``. Điều này tương đương với hành vi ``sync = true`` trước đây.

.. _class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_CYCLIC_MUTABLE:

.. rst-class:: classref-enumeration-constant

:ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **SYNC_MODE_CYCLIC_MUTABLE** = ``2``

Tất cả animation được scale theo thời gian để duy trì đồng bộ, với độ dài chu kỳ được tính động từ các blend weight đang hoạt động. Cơ chế này tự chuẩn hóa: một animation solo sẽ phát ở tốc độ bình thường.

\ **Lưu ý:** Nếu bạn áp dụng :ref:`AnimationNodeTimeSeek<class_AnimationNodeTimeSeek>` cho kết quả khi xử lý các animation có độ dài khác nhau, việc đồng bộ sẽ bị phá vỡ. Trong những trường hợp như vậy, bạn nên sử dụng :ref:`AnimationNodeAnimation.use_custom_timeline<class_AnimationNodeAnimation_property_use_custom_timeline>` để căn chỉnh độ dài animation.

.. _class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_CYCLIC_CONSTANT:

.. rst-class:: classref-enumeration-constant

:ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **SYNC_MODE_CYCLIC_CONSTANT** = ``3``

Tất cả animation được scale theo thời gian để hoàn thành một chu kỳ trong :ref:`cyclic_length<class_AnimationNodeBlendSpace1D_property_cyclic_length>` giây, giữ chúng đồng bộ bất kể độ dài riêng của từng animation.

\ **Lưu ý:** Nếu bạn áp dụng :ref:`AnimationNodeTimeSeek<class_AnimationNodeTimeSeek>` cho kết quả khi xử lý các animation có độ dài khác nhau, việc đồng bộ sẽ bị phá vỡ. Trong những trường hợp như vậy, bạn nên sử dụng :ref:`AnimationNodeAnimation.use_custom_timeline<class_AnimationNodeAnimation_property_use_custom_timeline>` để căn chỉnh độ dài animation.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeBlendSpace1D_property_blend_mode:

.. rst-class:: classref-property

:ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` **blend_mode** = ``0`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_blend_mode>`

.. rst-class:: classref-property-setget

- |void| **set_blend_mode**\ (\ value\: :ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>`\ ) - :ref:`BlendMode<enum_AnimationNodeBlendSpace1D_BlendMode>` **get_blend_mode**\ (\ )

Điều khiển phép nội suy giữa các animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_cyclic_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **cyclic_length** = ``0.0`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_cyclic_length>`

.. rst-class:: classref-property-setget

- |void| **set_cyclic_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cyclic_length**\ (\ )

Độ dài chu kỳ tính bằng giây được :ref:`SYNC_MODE_CYCLIC_CONSTANT<class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_CYCLIC_CONSTANT>` sử dụng. Tất cả animation được scale theo thời gian để hoàn thành một chu kỳ đầy đủ trong khoảng thời gian này. Phải lớn hơn ``0`` để tính năng đồng bộ theo chu kỳ có hiệu lực.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_max_space:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_space** = ``1.0`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_max_space>`

.. rst-class:: classref-property-setget

- |void| **set_max_space**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_space**\ (\ )

Giới hạn trên của trục blend space đối với vị trí các điểm. Xem :ref:`add_blend_point()<class_AnimationNodeBlendSpace1D_method_add_blend_point>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_min_space:

.. rst-class:: classref-property

:ref:`float<class_float>` **min_space** = ``-1.0`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_min_space>`

.. rst-class:: classref-property-setget

- |void| **set_min_space**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_min_space**\ (\ )

Giới hạn dưới của trục blend space đối với vị trí các điểm. Xem :ref:`add_blend_point()<class_AnimationNodeBlendSpace1D_method_add_blend_point>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_snap:

.. rst-class:: classref-property

:ref:`float<class_float>` **snap** = ``0.1`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_snap>`

.. rst-class:: classref-property-setget

- |void| **set_snap**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_snap**\ (\ )

Mức tăng vị trí cần snap tới khi di chuyển một điểm trên trục.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_sync:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **sync** :ref:`🔗<class_AnimationNodeBlendSpace1D_property_sync>`

.. rst-class:: classref-property-setget

- |void| **set_use_sync**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_sync**\ (\ )

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`sync_mode<class_AnimationNodeBlendSpace1D_property_sync_mode>`.

Nếu ``true``, chế độ đồng bộ được bật (tương đương với :ref:`SYNC_MODE_INDEPENDENT<class_AnimationNodeBlendSpace1D_constant_SYNC_MODE_INDEPENDENT>`). Thuộc tính này được giữ lại để tương thích ngược.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_sync_mode:

.. rst-class:: classref-property

:ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **sync_mode** = ``0`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_sync_mode>`

.. rst-class:: classref-property-setget

- |void| **set_sync_mode**\ (\ value\: :ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>`\ ) - :ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` **get_sync_mode**\ (\ )

Điều khiển cách đồng bộ các animation khi blend. Xem :ref:`SyncMode<enum_AnimationNodeBlendSpace1D_SyncMode>` để biết các tùy chọn khả dụng.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_property_value_label:

.. rst-class:: classref-property

:ref:`String<class_String>` **value_label** = ``"value"`` :ref:`🔗<class_AnimationNodeBlendSpace1D_property_value_label>`

.. rst-class:: classref-property-setget

- |void| **set_value_label**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_value_label**\ (\ )

Nhãn của trục ảo trong blend space.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNodeBlendSpace1D_method_add_blend_point:

.. rst-class:: classref-method

|void| **add_blend_point**\ (\ node\: :ref:`AnimationRootNode<class_AnimationRootNode>`, pos\: :ref:`float<class_float>`, at_index\: :ref:`int<class_int>` = -1, name\: :ref:`StringName<class_StringName>` = &""\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_add_blend_point>`

Thêm một điểm mới với ``name``, đại diện cho một ``node`` trên trục ảo tại vị trí được thiết lập bởi ``pos``. Bạn có thể chèn điểm này tại một chỉ mục cụ thể bằng đối số ``at_index``. Nếu sử dụng giá trị mặc định cho ``at_index``, điểm sẽ được chèn vào cuối mảng các blend point.

\ **Lưu ý:** Nếu không cung cấp tên, safe index sẽ được sử dụng làm tham chiếu. Trong tương lai, tên trống sẽ bị loại bỏ, vì vậy nên truyền tên một cách rõ ràng.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_find_blend_point_by_name:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_blend_point_by_name**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendSpace1D_method_find_blend_point_by_name>`

Trả về chỉ mục của blend point có ``name`` đã cho. Trả về ``-1`` nếu không tìm thấy blend point có tên đó.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_get_blend_point_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_blend_point_count**\ (\ ) |const| :ref:`🔗<class_AnimationNodeBlendSpace1D_method_get_blend_point_count>`

Trả về số lượng điểm trên trục blend.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_get_blend_point_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_blend_point_name**\ (\ point\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendSpace1D_method_get_blend_point_name>`

Trả về tên của blend point tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_get_blend_point_node:

.. rst-class:: classref-method

:ref:`AnimationRootNode<class_AnimationRootNode>` **get_blend_point_node**\ (\ point\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendSpace1D_method_get_blend_point_node>`

Trả về :ref:`AnimationNode<class_AnimationNode>` được điểm tại chỉ mục ``point`` tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_get_blend_point_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_blend_point_position**\ (\ point\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNodeBlendSpace1D_method_get_blend_point_position>`

Trả về vị trí của điểm tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_remove_blend_point:

.. rst-class:: classref-method

|void| **remove_blend_point**\ (\ point\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_remove_blend_point>`

Xóa điểm tại chỉ mục ``point`` khỏi trục blend.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_reorder_blend_point:

.. rst-class:: classref-method

|void| **reorder_blend_point**\ (\ from_index\: :ref:`int<class_int>`, to_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_reorder_blend_point>`

Hoán đổi các blend point tại chỉ mục ``from_index`` và ``to_index``, đổi vị trí và thuộc tính của chúng.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_set_blend_point_name:

.. rst-class:: classref-method

|void| **set_blend_point_name**\ (\ point\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_set_blend_point_name>`

Đặt tên cho blend point tại chỉ mục ``point``. Nếu tên xung đột với một điểm hiện có, một tên duy nhất sẽ được tự động tạo.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_set_blend_point_node:

.. rst-class:: classref-method

|void| **set_blend_point_node**\ (\ point\: :ref:`int<class_int>`, node\: :ref:`AnimationRootNode<class_AnimationRootNode>`\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_set_blend_point_node>`

Thay đổi :ref:`AnimationNode<class_AnimationNode>` được điểm tại chỉ mục ``point`` tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNodeBlendSpace1D_method_set_blend_point_position:

.. rst-class:: classref-method

|void| **set_blend_point_position**\ (\ point\: :ref:`int<class_int>`, pos\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AnimationNodeBlendSpace1D_method_set_blend_point_position>`

Cập nhật vị trí của điểm tại chỉ mục ``point`` trên trục blend.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
