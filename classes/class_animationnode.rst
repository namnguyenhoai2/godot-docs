:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNode.xml.

.. _class_AnimationNode:

AnimationNode
=============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AnimationNodeExtension<class_AnimationNodeExtension>`, :ref:`AnimationNodeOutput<class_AnimationNodeOutput>`, :ref:`AnimationNodeSync<class_AnimationNodeSync>`, :ref:`AnimationNodeTimeScale<class_AnimationNodeTimeScale>`, :ref:`AnimationNodeTimeSeek<class_AnimationNodeTimeSeek>`, :ref:`AnimationRootNode<class_AnimationRootNode>`

Lớp cơ sở cho các node :ref:`AnimationTree<class_AnimationTree>`. Không liên quan đến các node của scene.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource cơ sở cho các node :ref:`AnimationTree<class_AnimationTree>`. Nhìn chung, nó không được sử dụng trực tiếp, nhưng bạn có thể tạo các node tùy chỉnh với công thức blending tùy chỉnh.

Kế thừa lớp này khi tạo các animation node chủ yếu để sử dụng trong :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`, nếu không thì nên sử dụng :ref:`AnimationRootNode<class_AnimationRootNode>` thay thế.

Bạn có thể truy cập thông tin thời gian dưới dạng tham số chỉ-đọc, được xử lý và lưu trữ trong frame trước đó cho tất cả các node ngoại trừ :ref:`AnimationNodeOutput<class_AnimationNodeOutput>`.

\ **Lưu ý:** Nếu có nhiều input trong **AnimationNode**, thông tin thời gian nào được ưu tiên sẽ phụ thuộc vào loại **AnimationNode**.

::

    var current_length = $AnimationTree["parameters/AnimationNodeName/current_length"]
    var current_position = $AnimationTree["parameters/AnimationNodeName/current_position"]
    var current_delta = $AnimationTree["parameters/AnimationNodeName/current_delta"]

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`filter_enabled<class_AnimationNode_property_filter_enabled>` |
   +-------------------------+--------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`               | :ref:`_get_caption<class_AnimationNode_private_method__get_caption>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                                                                            |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationNode<class_AnimationNode>` | :ref:`_get_child_by_name<class_AnimationNode_private_method__get_child_by_name>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                    |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`       | :ref:`_get_child_nodes<class_AnimationNode_private_method__get_child_nodes>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                                                                    |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`             | :ref:`_get_parameter_default_value<class_AnimationNode_private_method__get_parameter_default_value>`\ (\ parameter\: :ref:`StringName<class_StringName>`\ ) |virtual| |const|                                                                                                                                                                                                                                                                                           |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                 | :ref:`_get_parameter_list<class_AnimationNode_private_method__get_parameter_list>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`_has_filter<class_AnimationNode_private_method__has_filter>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`_is_parameter_read_only<class_AnimationNode_private_method__is_parameter_read_only>`\ (\ parameter\: :ref:`StringName<class_StringName>`\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                     |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                 | :ref:`_process<class_AnimationNode_private_method__process>`\ (\ time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, test_only\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                                                                                                                                                                      |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`add_input<class_AnimationNode_method_add_input>`\ (\ name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                                                                                                                                                        |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`blend_animation<class_AnimationNode_method_blend_animation>`\ (\ animation\: :ref:`StringName<class_StringName>`, time\: :ref:`float<class_float>`, delta\: :ref:`float<class_float>`, seeked\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, looped_flag\: :ref:`LoopedFlag<enum_Animation_LoopedFlag>` = 0\ )                                                                                      |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                 | :ref:`blend_input<class_AnimationNode_method_blend_input>`\ (\ input_index\: :ref:`int<class_int>`, time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, filter\: :ref:`FilterAction<enum_AnimationNode_FilterAction>` = 0, sync\: :ref:`bool<class_bool>` = true, test_only\: :ref:`bool<class_bool>` = false\ )                                                        |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                 | :ref:`blend_node<class_AnimationNode_method_blend_node>`\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, filter\: :ref:`FilterAction<enum_AnimationNode_FilterAction>` = 0, sync\: :ref:`bool<class_bool>` = true, test_only\: :ref:`bool<class_bool>` = false\ ) |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`find_input<class_AnimationNode_method_find_input>`\ (\ name\: :ref:`String<class_String>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`get_input_count<class_AnimationNode_method_get_input_count>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                        |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`               | :ref:`get_input_name<class_AnimationNode_method_get_input_name>`\ (\ input\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                           |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`             | :ref:`get_parameter<class_AnimationNode_method_get_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`get_processing_animation_tree_instance_id<class_AnimationNode_method_get_processing_animation_tree_instance_id>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                    |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`is_path_filtered<class_AnimationNode_method_is_path_filtered>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`is_process_testing<class_AnimationNode_method_is_process_testing>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                  |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`remove_input<class_AnimationNode_method_remove_input>`\ (\ index\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                                                                                                       |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`set_filter_path<class_AnimationNode_method_set_filter_path>`\ (\ path\: :ref:`NodePath<class_NodePath>`, enable\: :ref:`bool<class_bool>`\ )                                                                                                                                                                                                                                                                                                                      |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`set_input_name<class_AnimationNode_method_set_input_name>`\ (\ input\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                                                                                                               |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`set_parameter<class_AnimationNode_method_set_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                                                                                                                                                                                                                                 |
   +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AnimationNode_signal_animation_node_removed:

.. rst-class:: classref-signal

**animation_node_removed**\ (\ object_id\: :ref:`int<class_int>`, node_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AnimationNode_signal_animation_node_removed>`

Được phát ra bởi các node kế thừa từ lớp này và có một cây nội bộ khi một trong các animation node của chúng bị xóa. Các animation node phát ra signal này là :ref:`AnimationNodeBlendSpace1D<class_AnimationNodeBlendSpace1D>`, :ref:`AnimationNodeBlendSpace2D<class_AnimationNodeBlendSpace2D>`, :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` và :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_signal_animation_node_renamed:

.. rst-class:: classref-signal

**animation_node_renamed**\ (\ object_id\: :ref:`int<class_int>`, old_name\: :ref:`String<class_String>`, new_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AnimationNode_signal_animation_node_renamed>`

Được phát ra bởi các node kế thừa từ lớp này và có một cây nội bộ khi tên của một trong các animation node của chúng thay đổi. Các animation node phát ra signal này là :ref:`AnimationNodeBlendSpace1D<class_AnimationNodeBlendSpace1D>`, :ref:`AnimationNodeBlendSpace2D<class_AnimationNodeBlendSpace2D>`, :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>` và :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_signal_node_updated:

.. rst-class:: classref-signal

**node_updated**\ (\ object_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNode_signal_node_updated>`

**Thử nghiệm:** Signal này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Được phát ra bởi :ref:`AnimationNodeAnimation<class_AnimationNodeAnimation>` khi resource :ref:`AnimationNodeAnimation.animation<class_AnimationNodeAnimation_property_animation>` của nó thay đổi, hoặc bởi :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>` khi các kết nối của nó thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_signal_tree_changed:

.. rst-class:: classref-signal

**tree_changed**\ (\ ) :ref:`🔗<class_AnimationNode_signal_tree_changed>`

Được phát ra bởi các node kế thừa từ lớp này và có một cây nội bộ khi một trong các animation node của chúng thay đổi. Các animation node phát ra signal này là :ref:`AnimationNodeBlendSpace1D<class_AnimationNodeBlendSpace1D>`, :ref:`AnimationNodeBlendSpace2D<class_AnimationNodeBlendSpace2D>`, :ref:`AnimationNodeStateMachine<class_AnimationNodeStateMachine>`, :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>` và :ref:`AnimationNodeTransition<class_AnimationNodeTransition>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationNode_FilterAction:

.. rst-class:: classref-enumeration

enum **FilterAction**: :ref:`🔗<enum_AnimationNode_FilterAction>`

.. _class_AnimationNode_constant_FILTER_IGNORE:

.. rst-class:: classref-enumeration-constant

:ref:`FilterAction<enum_AnimationNode_FilterAction>` **FILTER_IGNORE** = ``0``

Không sử dụng filtering.

.. _class_AnimationNode_constant_FILTER_PASS:

.. rst-class:: classref-enumeration-constant

:ref:`FilterAction<enum_AnimationNode_FilterAction>` **FILTER_PASS** = ``1``

Các path khớp với filter sẽ được phép đi qua.

.. _class_AnimationNode_constant_FILTER_STOP:

.. rst-class:: classref-enumeration-constant

:ref:`FilterAction<enum_AnimationNode_FilterAction>` **FILTER_STOP** = ``2``

Các path khớp với filter sẽ bị loại bỏ.

.. _class_AnimationNode_constant_FILTER_BLEND:

.. rst-class:: classref-enumeration-constant

:ref:`FilterAction<enum_AnimationNode_FilterAction>` **FILTER_BLEND** = ``3``

Các path khớp với filter sẽ được blend (bằng giá trị blend).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNode_property_filter_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter_enabled** :ref:`🔗<class_AnimationNode_property_filter_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_filter_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_filter_enabled**\ (\ )

Nếu ``true``, filtering được bật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AnimationNode_private_method__get_caption:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_caption**\ (\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__get_caption>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để ghi đè caption dạng văn bản cho animation node này.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__get_child_by_name:

.. rst-class:: classref-method

:ref:`AnimationNode<class_AnimationNode>` **_get_child_by_name**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__get_child_by_name>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về animation node con theo ``name`` của nó.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__get_child_nodes:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_get_child_nodes**\ (\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__get_child_nodes>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về tất cả animation node con theo thứ tự dưới dạng dictionary ``name: node``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__get_parameter_default_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_parameter_default_value**\ (\ parameter\: :ref:`StringName<class_StringName>`\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__get_parameter_default_value>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về giá trị mặc định của một ``parameter``. Parameters là bộ nhớ cục bộ tùy chỉnh được sử dụng cho các animation node của bạn, vì một resource có thể được tái sử dụng trong nhiều cây.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__get_parameter_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **_get_parameter_list**\ (\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__get_parameter_list>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về danh sách các thuộc tính trên animation node này. Parameters là bộ nhớ cục bộ tùy chỉnh được sử dụng cho các animation node của bạn, vì một resource có thể được tái sử dụng trong nhiều cây. Định dạng tương tự như :ref:`Object.get_property_list()<class_Object_method_get_property_list>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__has_filter:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_has_filter**\ (\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__has_filter>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về liệu blend tree editor có nên hiển thị phần chỉnh sửa filter trên animation node này hay không.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__is_parameter_read_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_parameter_read_only**\ (\ parameter\: :ref:`StringName<class_StringName>`\ ) |virtual| |const| :ref:`🔗<class_AnimationNode_private_method__is_parameter_read_only>`

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để trả về liệu ``parameter`` có ở chế độ chỉ-đọc hay không. Parameters là bộ nhớ cục bộ tùy chỉnh được sử dụng cho các animation node của bạn, vì một resource có thể được tái sử dụng trong nhiều cây.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_private_method__process:

.. rst-class:: classref-method

:ref:`float<class_float>` **_process**\ (\ time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, test_only\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_AnimationNode_private_method__process>`

**Đã lỗi thời:** Hiện tại, phương thức này hầu như vô dụng vì thiếu nhiều API để mở rộng AnimationNode bằng GDScript. Dự kiến trong tương lai sẽ cung cấp một API linh hoạt hơn sử dụng các structure.

Khi kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, hãy triển khai virtual method này để chạy một số code khi animation node này được xử lý. Tham số ``time`` là delta tương đối, trừ khi ``seek`` là ``true``, khi đó nó là tuyệt đối.

Tại đây, hãy gọi các hàm :ref:`blend_input()<class_AnimationNode_method_blend_input>`, :ref:`blend_node()<class_AnimationNode_method_blend_node>` hoặc :ref:`blend_animation()<class_AnimationNode_method_blend_animation>`. Bạn cũng có thể sử dụng :ref:`get_parameter()<class_AnimationNode_method_get_parameter>` và :ref:`set_parameter()<class_AnimationNode_method_set_parameter>` để sửa đổi bộ nhớ cục bộ.

Hàm này sẽ trả về delta.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_add_input:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **add_input**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AnimationNode_method_add_input>`

Thêm một input vào animation node. Điều này chỉ hữu ích cho các animation node được tạo để sử dụng trong :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Nếu thao tác thêm thất bại, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_blend_animation:

.. rst-class:: classref-method

|void| **blend_animation**\ (\ animation\: :ref:`StringName<class_StringName>`, time\: :ref:`float<class_float>`, delta\: :ref:`float<class_float>`, seeked\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, looped_flag\: :ref:`LoopedFlag<enum_Animation_LoopedFlag>` = 0\ ) :ref:`🔗<class_AnimationNode_method_blend_animation>`

Blend một animation với lượng ``blend`` (tên phải hợp lệ trong :ref:`AnimationPlayer<class_AnimationPlayer>` được liên kết). Có thể truyền một ``time`` và ``delta``, cũng như thông tin liệu ``seeked`` đã xảy ra hay chưa.

Một ``looped_flag`` được sử dụng bởi quá trình xử lý nội bộ ngay sau vòng lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_blend_input:

.. rst-class:: classref-method

:ref:`float<class_float>` **blend_input**\ (\ input_index\: :ref:`int<class_int>`, time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, filter\: :ref:`FilterAction<enum_AnimationNode_FilterAction>` = 0, sync\: :ref:`bool<class_bool>` = true, test_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AnimationNode_method_blend_input>`

Blend một input. Điều này chỉ hữu ích cho các animation node được tạo cho :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Tham số ``time`` là delta tương đối, trừ khi ``seek`` là ``true``, khi đó nó là tuyệt đối. Có thể tùy chọn truyền vào một filter mode.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_blend_node:

.. rst-class:: classref-method

:ref:`float<class_float>` **blend_node**\ (\ name\: :ref:`StringName<class_StringName>`, node\: :ref:`AnimationNode<class_AnimationNode>`, time\: :ref:`float<class_float>`, seek\: :ref:`bool<class_bool>`, is_external_seeking\: :ref:`bool<class_bool>`, blend\: :ref:`float<class_float>`, filter\: :ref:`FilterAction<enum_AnimationNode_FilterAction>` = 0, sync\: :ref:`bool<class_bool>` = true, test_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AnimationNode_method_blend_node>`

Blend một animation node khác (trong trường hợp animation node này chứa các animation node con). Hàm này chỉ hữu ích nếu bạn kế thừa từ :ref:`AnimationRootNode<class_AnimationRootNode>`, nếu không các editor sẽ không hiển thị animation node của bạn để thêm vào.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_find_input:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_input**\ (\ name\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_AnimationNode_method_find_input>`

Trả về index của input tương ứng với ``name``. Nếu không tìm thấy, trả về ``-1``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_get_input_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_input_count**\ (\ ) |const| :ref:`🔗<class_AnimationNode_method_get_input_count>`

Số lượng input trong animation node này, chỉ hữu ích cho các animation node đi vào :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_get_input_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_input_name**\ (\ input\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AnimationNode_method_get_input_name>`

Lấy tên của một input theo index.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_get_parameter:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_parameter**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationNode_method_get_parameter>`

Lấy giá trị của một parameter. Parameters là bộ nhớ cục bộ tùy chỉnh được sử dụng cho các animation node của bạn, vì một resource có thể được tái sử dụng trong nhiều cây.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_get_processing_animation_tree_instance_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_processing_animation_tree_instance_id**\ (\ ) |const| :ref:`🔗<class_AnimationNode_method_get_processing_animation_tree_instance_id>`

Trả về object id của :ref:`AnimationTree<class_AnimationTree>` sở hữu node này.

\ **Lưu ý:** Chỉ nên gọi phương thức này từ bên trong phương thức :ref:`AnimationNodeExtension._process_animation_node()<class_AnimationNodeExtension_private_method__process_animation_node>`, nếu không sẽ trả về một id không hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_is_path_filtered:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_path_filtered**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_AnimationNode_method_is_path_filtered>`

Trả về ``true`` nếu path đã cho bị filter.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_is_process_testing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_process_testing**\ (\ ) |const| :ref:`🔗<class_AnimationNode_method_is_process_testing>`

Trả về ``true`` nếu animation node này đang được xử lý ở chế độ chỉ dành cho kiểm thử.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_remove_input:

.. rst-class:: classref-method

|void| **remove_input**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AnimationNode_method_remove_input>`

Xóa một input, chỉ gọi hàm này khi đang inactive.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_set_filter_path:

.. rst-class:: classref-method

|void| **set_filter_path**\ (\ path\: :ref:`NodePath<class_NodePath>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AnimationNode_method_set_filter_path>`

Thêm hoặc xóa một path khỏi filter.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_set_input_name:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **set_input_name**\ (\ input\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AnimationNode_method_set_input_name>`

Đặt tên cho input tại index ``input`` đã cho. Nếu thao tác cài đặt thất bại, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationNode_method_set_parameter:

.. rst-class:: classref-method

|void| **set_parameter**\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_AnimationNode_method_set_parameter>`

Đặt một parameter tùy chỉnh. Các parameter này được sử dụng làm bộ nhớ cục bộ, vì resource có thể được tái sử dụng trên toàn cây hoặc giữa các scene.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
