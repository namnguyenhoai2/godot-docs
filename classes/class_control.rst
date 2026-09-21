:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Control.xml.

.. _class_Control:

Control
=======

**Kế thừa:** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`BaseButton<class_BaseButton>`, :ref:`ColorRect<class_ColorRect>`, :ref:`Container<class_Container>`, :ref:`GraphEdit<class_GraphEdit>`, :ref:`ItemList<class_ItemList>`, :ref:`Label<class_Label>`, :ref:`LineEdit<class_LineEdit>`, :ref:`MenuBar<class_MenuBar>`, :ref:`NinePatchRect<class_NinePatchRect>`, :ref:`Panel<class_Panel>`, :ref:`Range<class_Range>`, :ref:`ReferenceRect<class_ReferenceRect>`, :ref:`RichTextLabel<class_RichTextLabel>`, :ref:`Separator<class_Separator>`, :ref:`TabBar<class_TabBar>`, :ref:`TextEdit<class_TextEdit>`, :ref:`TextureRect<class_TextureRect>`, :ref:`Tree<class_Tree>`, :ref:`VideoStreamPlayer<class_VideoStreamPlayer>`, :ref:`VirtualJoystick<class_VirtualJoystick>`

Lớp cơ sở cho tất cả các control GUI. Điều chỉnh vị trí và kích thước dựa trên control cha.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho tất cả các node liên quan đến UI. **Control** có một hình chữ nhật bao quanh xác định phạm vi của nó, một vị trí anchor tương đối với control cha hoặc viewport hiện tại, và các offset tương đối với anchor. Các offset tự động cập nhật khi node, bất kỳ node cha nào của nó hoặc kích thước màn hình thay đổi.

Để biết thêm thông tin về hệ thống UI, anchor, offset và container của Godot, hãy xem các tutorial liên quan trong sổ tay. Để xây dựng UI linh hoạt, bạn sẽ cần kết hợp các phần tử UI kế thừa từ **Control** và các node :ref:`Container<class_Container>`.

\ **Lưu ý:** Vì cả :ref:`Node2D<class_Node2D>` và **Control** đều kế thừa từ :ref:`CanvasItem<class_CanvasItem>`, chúng dùng chung một số khái niệm từ lớp này, chẳng hạn như các thuộc tính :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` và :ref:`CanvasItem.visible<class_CanvasItem_property_visible>`.

\ **Node giao diện người dùng và input**\

Godot truyền các input event thông qua viewport. Mỗi :ref:`Viewport<class_Viewport>` chịu trách nhiệm truyền các :ref:`InputEvent<class_InputEvent>`\ đến các node con của chúng. Vì :ref:`SceneTree.root<class_SceneTree_property_root>` là một :ref:`Window<class_Window>`, việc này đã tự động diễn ra đối với tất cả phần tử UI trong game của bạn.

Các input event được truyền qua :ref:`SceneTree<class_SceneTree>` từ node gốc đến tất cả node con bằng cách gọi :ref:`Node._input()<class_Node_private_method__input>`. Riêng với các phần tử UI, việc ghi đè virtual method :ref:`_gui_input()<class_Control_private_method__gui_input>` sẽ phù hợp hơn; method này lọc các input event không liên quan, chẳng hạn bằng cách kiểm tra thứ tự z, :ref:`mouse_filter<class_Control_property_mouse_filter>`, focus hoặc xem event có nằm bên trong hình chữ nhật bao quanh control hay không.

Gọi :ref:`accept_event()<class_Control_method_accept_event>` để không node nào khác nhận event. Sau khi bạn chấp nhận một input, nó được đánh dấu là đã xử lý nên :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>` sẽ không xử lý nó.

Chỉ một node **Control** có thể được focus. Chỉ node đang focus mới nhận event. Để nhận focus, hãy gọi :ref:`grab_focus()<class_Control_method_grab_focus>`. Các node **Control** mất focus khi một node khác giành được focus hoặc khi bạn ẩn node đang focus. Focus sẽ không được biểu thị trực quan nếu đạt được thông qua input chuột/cảm ứng, mà chỉ xuất hiện với input từ bàn phím/gamepad (nhằm hỗ trợ khả năng truy cập), hoặc thông qua :ref:`grab_focus()<class_Control_method_grab_focus>`.

Đặt :ref:`mouse_filter<class_Control_property_mouse_filter>` thành :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>` để yêu cầu một node **Control** bỏ qua các event chuột hoặc cảm ứng. Bạn sẽ cần thiết lập này nếu đặt một biểu tượng lên trên một button.

\ Các resource :ref:`Theme<class_Theme>` thay đổi giao diện của control. :ref:`theme<class_Control_property_theme>` của một node **Control** ảnh hưởng đến tất cả node con trực tiếp và gián tiếp của nó (miễn là chuỗi các control không bị gián đoạn). Để ghi đè một số theme item, hãy gọi một trong các method ``add_theme_*_override``, chẳng hạn như :ref:`add_theme_font_override()<class_Control_method_add_theme_font_override>`. Bạn cũng có thể ghi đè theme item trong Inspector.

\ **Lưu ý:** Theme item *không phải là* các thuộc tính :ref:`Object<class_Object>`. Điều này có nghĩa là bạn không thể truy cập giá trị của chúng bằng :ref:`Object.get()<class_Object_method_get>` và :ref:`Object.set()<class_Object_method_set>`. Thay vào đó, hãy sử dụng các method ``get_theme_*`` và ``add_theme_*_override`` do lớp này cung cấp.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Chỉ mục tài liệu GUI <../tutorials/ui/index>`

- :doc:`Vẽ tùy chỉnh trong 2D <../tutorials/2d/custom_drawing_in_2d>`

- :doc:`Bộ sưu tập node Control <../tutorials/ui/control_node_gallery>`

- :doc:`Nhiều độ phân giải <../tutorials/rendering/multiple_resolutions>`

- `All GUI Demos <https://github.com/godotengine/godot-demo-projects/tree/master/gui>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]                 | :ref:`accessibility_controls_nodes<class_Control_property_accessibility_controls_nodes>`         | ``[]``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]                 | :ref:`accessibility_described_by_nodes<class_Control_property_accessibility_described_by_nodes>` | ``[]``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                  | :ref:`accessibility_description<class_Control_property_accessibility_description>`               | ``""``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]                 | :ref:`accessibility_flow_to_nodes<class_Control_property_accessibility_flow_to_nodes>`           | ``[]``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]                 | :ref:`accessibility_labeled_by_nodes<class_Control_property_accessibility_labeled_by_nodes>`     | ``[]``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`AccessibilityLiveMode<enum_AccessibilityServer_AccessibilityLiveMode>` | :ref:`accessibility_live<class_Control_property_accessibility_live>`                             | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                  | :ref:`accessibility_name<class_Control_property_accessibility_name>`                             | ``""``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`anchor_bottom<class_Control_property_anchor_bottom>`                                       | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`anchor_left<class_Control_property_anchor_left>`                                           | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`anchor_right<class_Control_property_anchor_right>`                                         | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`anchor_top<class_Control_property_anchor_top>`                                             | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`auto_translate<class_Control_property_auto_translate>`                                     |                                                                               |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`clip_contents<class_Control_property_clip_contents>`                                       | ``false``                                                                     |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>`                           | ``Vector2(-1, -1)``                                                           |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>`                           | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>`           | :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>`                 | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`                                     | :ref:`focus_mode<class_Control_property_focus_mode>`                                             | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_neighbor_bottom<class_Control_property_focus_neighbor_bottom>`                       | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_neighbor_left<class_Control_property_focus_neighbor_left>`                           | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_neighbor_right<class_Control_property_focus_neighbor_right>`                         | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_neighbor_top<class_Control_property_focus_neighbor_top>`                             | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_next<class_Control_property_focus_next>`                                             | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                              | :ref:`focus_previous<class_Control_property_focus_previous>`                                     | ``NodePath("")``                                                              |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`global_position<class_Control_property_global_position>`                                   |                                                                               |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`GrowDirection<enum_Control_GrowDirection>`                             | :ref:`grow_horizontal<class_Control_property_grow_horizontal>`                                   | ``1``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`GrowDirection<enum_Control_GrowDirection>`                             | :ref:`grow_vertical<class_Control_property_grow_vertical>`                                       | ``1``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`LayoutDirection<enum_Control_LayoutDirection>`                         | :ref:`layout_direction<class_Control_property_layout_direction>`                                 | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`localize_numeral_system<class_Control_property_localize_numeral_system>`                   | ``true``                                                                      |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>`           | :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>`                 | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`CursorShape<enum_Control_CursorShape>`                                 | :ref:`mouse_default_cursor_shape<class_Control_property_mouse_default_cursor_shape>`             | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>`                                 | :ref:`mouse_filter<class_Control_property_mouse_filter>`                                         | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`mouse_force_pass_scroll_events<class_Control_property_mouse_force_pass_scroll_events>`     | ``true``                                                                      |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`offset_bottom<class_Control_property_offset_bottom>`                                       | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`offset_left<class_Control_property_offset_left>`                                           | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`offset_right<class_Control_property_offset_right>`                                         | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`offset_top<class_Control_property_offset_top>`                                             | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>`                 | ``false``                                                                     |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`offset_transform_pivot<class_Control_property_offset_transform_pivot>`                     | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`offset_transform_pivot_ratio<class_Control_property_offset_transform_pivot_ratio>`         | ``Vector2(0.5, 0.5)``                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`offset_transform_position<class_Control_property_offset_transform_position>`               | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`offset_transform_position_ratio<class_Control_property_offset_transform_position_ratio>`   | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`offset_transform_rotation<class_Control_property_offset_transform_rotation>`               | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`offset_transform_scale<class_Control_property_offset_transform_scale>`                     | ``Vector2(1, 1)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`offset_transform_visual_only<class_Control_property_offset_transform_visual_only>`         | ``true``                                                                      |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>`          | physics_interpolation_mode                                                                       | ``2`` (overrides :ref:`Node<class_Node_property_physics_interpolation_mode>`) |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`pivot_offset<class_Control_property_pivot_offset>`                                         | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`pivot_offset_ratio<class_Control_property_pivot_offset_ratio>`                             | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`position<class_Control_property_position>`                                                 | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`propagate_maximum_size<class_Control_property_propagate_maximum_size>`                     | ``false``                                                                     |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`rotation<class_Control_property_rotation>`                                                 | ``0.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`rotation_degrees<class_Control_property_rotation_degrees>`                                 |                                                                               |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`scale<class_Control_property_scale>`                                                       | ``Vector2(1, 1)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                                      | :ref:`shortcut_context<class_Control_property_shortcut_context>`                                 |                                                                               |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                | :ref:`size<class_Control_property_size>`                                                         | ``Vector2(0, 0)``                                                             |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\]                       | :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>`                       | ``1``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                    | :ref:`size_flags_stretch_ratio<class_Control_property_size_flags_stretch_ratio>`                 | ``1.0``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\]                       | :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`                           | ``1``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Theme<class_Theme>`                                                    | :ref:`theme<class_Control_property_theme>`                                                       |                                                                               |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                          | :ref:`theme_type_variation<class_Control_property_theme_type_variation>`                         | ``&""``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>`                        | :ref:`tooltip_auto_translate_mode<class_Control_property_tooltip_auto_translate_mode>`           | ``0``                                                                         |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                  | :ref:`tooltip_text<class_Control_property_tooltip_text>`                                         | ``""``                                                                        |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                          | :ref:`translation_context<class_Control_property_translation_context>`                           | ``&""``                                                                       |
   +------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Method
------

.. table::
   :widths: auto

   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                  | :ref:`_accessibility_get_contextual_info<class_Control_private_method__accessibility_get_contextual_info>`\ (\ ) |virtual| |const|                                                                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`_can_drop_data<class_Control_private_method__can_drop_data>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`, data\: :ref:`Variant<class_Variant>`\ ) |virtual| |const|                                                                                           |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`_drop_data<class_Control_private_method__drop_data>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`, data\: :ref:`Variant<class_Variant>`\ ) |virtual|                                                                                                           |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                  | :ref:`_get_accessibility_container_name<class_Control_private_method__get_accessibility_container_name>`\ (\ node\: :ref:`Node<class_Node>`\ ) |virtual| |const|                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`_get_cursor_shape<class_Control_private_method__get_cursor_shape>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                                                                                           |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                | :ref:`_get_drag_data<class_Control_private_method__get_drag_data>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual|                                                                                                                                         |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`_get_maximum_size<class_Control_private_method__get_maximum_size>`\ (\ ) |virtual| |const|                                                                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`_get_minimum_size<class_Control_private_method__get_minimum_size>`\ (\ ) |virtual| |const|                                                                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                  | :ref:`_get_tooltip<class_Control_private_method__get_tooltip>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                                                                                                     |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>`        | :ref:`_get_tooltip_auto_translate_mode_at<class_Control_private_method__get_tooltip_auto_translate_mode_at>`\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                                                       |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`_gui_input<class_Control_private_method__gui_input>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual|                                                                                                                                                 |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`_has_point<class_Control_private_method__has_point>`\ (\ point\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const|                                                                                                                                               |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`                                  | :ref:`_make_custom_tooltip<class_Control_private_method__make_custom_tooltip>`\ (\ for_text\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`_structured_text_parser<class_Control_private_method__structured_text_parser>`\ (\ args\: :ref:`Array<class_Array>`, text\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`accept_event<class_Control_method_accept_event>`\ (\ )                                                                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`accessibility_drag<class_Control_method_accessibility_drag>`\ (\ )                                                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`accessibility_drop<class_Control_method_accessibility_drop>`\ (\ )                                                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_color_override<class_Control_method_add_theme_color_override>`\ (\ name\: :ref:`StringName<class_StringName>`, color\: :ref:`Color<class_Color>`\ )                                                                                                     |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_constant_override<class_Control_method_add_theme_constant_override>`\ (\ name\: :ref:`StringName<class_StringName>`, constant\: :ref:`int<class_int>`\ )                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_font_override<class_Control_method_add_theme_font_override>`\ (\ name\: :ref:`StringName<class_StringName>`, font\: :ref:`Font<class_Font>`\ )                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_font_size_override<class_Control_method_add_theme_font_size_override>`\ (\ name\: :ref:`StringName<class_StringName>`, font_size\: :ref:`int<class_int>`\ )                                                                                             |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_icon_override<class_Control_method_add_theme_icon_override>`\ (\ name\: :ref:`StringName<class_StringName>`, texture\: :ref:`Texture2D<class_Texture2D>`\ )                                                                                             |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`add_theme_stylebox_override<class_Control_method_add_theme_stylebox_override>`\ (\ name\: :ref:`StringName<class_StringName>`, stylebox\: :ref:`StyleBox<class_StyleBox>`\ )                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`begin_bulk_theme_override<class_Control_method_begin_bulk_theme_override>`\ (\ )                                                                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`end_bulk_theme_override<class_Control_method_end_bulk_theme_override>`\ (\ )                                                                                                                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>`                                | :ref:`find_next_valid_focus<class_Control_method_find_next_valid_focus>`\ (\ ) |const|                                                                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>`                                | :ref:`find_prev_valid_focus<class_Control_method_find_prev_valid_focus>`\ (\ ) |const|                                                                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>`                                | :ref:`find_valid_focus_neighbor<class_Control_method_find_valid_focus_neighbor>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`force_drag<class_Control_method_force_drag>`\ (\ data\: :ref:`Variant<class_Variant>`, preview\: :ref:`Control<class_Control>`\ )                                                                                                                                 |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                    | :ref:`get_anchor<class_Control_method_get_anchor>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_begin<class_Control_method_get_begin>`\ (\ ) |const|                                                                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_bound_minimum_size<class_Control_method_get_bound_minimum_size>`\ (\ ) |const|                                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_combined_maximum_size<class_Control_method_get_combined_maximum_size>`\ (\ ) |const|                                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_combined_minimum_size<class_Control_method_get_combined_minimum_size>`\ (\ ) |const|                                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_combined_pivot_offset<class_Control_method_get_combined_pivot_offset>`\ (\ ) |const|                                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`CursorShape<enum_Control_CursorShape>`                 | :ref:`get_cursor_shape<class_Control_method_get_cursor_shape>`\ (\ at_position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const|                                                                                                                               |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_end<class_Control_method_get_end>`\ (\ ) |const|                                                                                                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`                     | :ref:`get_focus_mode_with_override<class_Control_method_get_focus_mode_with_override>`\ (\ ) |const|                                                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                              | :ref:`get_focus_neighbor<class_Control_method_get_focus_neighbor>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                                    | :ref:`get_global_rect<class_Control_method_get_global_rect>`\ (\ ) |const|                                                                                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_maximum_size<class_Control_method_get_maximum_size>`\ (\ ) |const|                                                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_minimum_size<class_Control_method_get_minimum_size>`\ (\ ) |const|                                                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>`                 | :ref:`get_mouse_filter_with_override<class_Control_method_get_mouse_filter_with_override>`\ (\ ) |const|                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                    | :ref:`get_offset<class_Control_method_get_offset>`\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_parent_area_size<class_Control_method_get_parent_area_size>`\ (\ ) |const|                                                                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>`                                | :ref:`get_parent_control<class_Control_method_get_parent_control>`\ (\ ) |const|                                                                                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                                    | :ref:`get_rect<class_Control_method_get_rect>`\ (\ ) |const|                                                                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`get_screen_position<class_Control_method_get_screen_position>`\ (\ ) |const|                                                                                                                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                                    | :ref:`get_theme_color<class_Control_method_get_theme_color>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_theme_constant<class_Control_method_get_theme_constant>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                    | :ref:`get_theme_default_base_scale<class_Control_method_get_theme_default_base_scale>`\ (\ ) |const|                                                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Font<class_Font>`                                      | :ref:`get_theme_default_font<class_Control_method_get_theme_default_font>`\ (\ ) |const|                                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_theme_default_font_size<class_Control_method_get_theme_default_font_size>`\ (\ ) |const|                                                                                                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Font<class_Font>`                                      | :ref:`get_theme_font<class_Control_method_get_theme_font>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_theme_font_size<class_Control_method_get_theme_font_size>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                            | :ref:`get_theme_icon<class_Control_method_get_theme_icon>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StyleBox<class_StyleBox>`                              | :ref:`get_theme_stylebox<class_Control_method_get_theme_stylebox>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                  | :ref:`get_tooltip<class_Control_method_get_tooltip>`\ (\ at_position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const|                                                                                                                                         |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`grab_click_focus<class_Control_method_grab_click_focus>`\ (\ )                                                                                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`grab_focus<class_Control_method_grab_focus>`\ (\ hide_focus\: :ref:`bool<class_bool>` = false\ )                                                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_focus<class_Control_method_has_focus>`\ (\ ignore_hidden_focus\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                                                                                   |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_color<class_Control_method_has_theme_color>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_color_override<class_Control_method_has_theme_color_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_constant<class_Control_method_has_theme_constant>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_constant_override<class_Control_method_has_theme_constant_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_font<class_Control_method_has_theme_font>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_font_override<class_Control_method_has_theme_font_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_font_size<class_Control_method_has_theme_font_size>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_font_size_override<class_Control_method_has_theme_font_size_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_icon<class_Control_method_has_theme_icon>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_icon_override<class_Control_method_has_theme_icon_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_stylebox<class_Control_method_has_theme_stylebox>`\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`has_theme_stylebox_override<class_Control_method_has_theme_stylebox_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`is_drag_successful<class_Control_method_is_drag_successful>`\ (\ ) |const|                                                                                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`is_layout_rtl<class_Control_method_is_layout_rtl>`\ (\ ) |const|                                                                                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`release_focus<class_Control_method_release_focus>`\ (\ )                                                                                                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_color_override<class_Control_method_remove_theme_color_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_constant_override<class_Control_method_remove_theme_constant_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_font_override<class_Control_method_remove_theme_font_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_font_size_override<class_Control_method_remove_theme_font_size_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_icon_override<class_Control_method_remove_theme_icon_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`remove_theme_stylebox_override<class_Control_method_remove_theme_stylebox_override>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`reset_size<class_Control_method_reset_size>`\ (\ )                                                                                                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_anchor<class_Control_method_set_anchor>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, anchor\: :ref:`float<class_float>`, keep_offset\: :ref:`bool<class_bool>` = false, push_opposite_anchor\: :ref:`bool<class_bool>` = true\ )                          |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_anchor_and_offset<class_Control_method_set_anchor_and_offset>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, anchor\: :ref:`float<class_float>`, offset\: :ref:`float<class_float>`, push_opposite_anchor\: :ref:`bool<class_bool>` = false\ )              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_anchors_and_offsets_preset<class_Control_method_set_anchors_and_offsets_preset>`\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, resize_mode\: :ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` = 0, margin\: :ref:`int<class_int>` = 0\ ) |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_anchors_preset<class_Control_method_set_anchors_preset>`\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, keep_offsets\: :ref:`bool<class_bool>` = false\ )                                                                                       |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_begin<class_Control_method_set_begin>`\ (\ position\: :ref:`Vector2<class_Vector2>`\ )                                                                                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_drag_forwarding<class_Control_method_set_drag_forwarding>`\ (\ drag_func\: :ref:`Callable<class_Callable>`, can_drop_func\: :ref:`Callable<class_Callable>`, drop_func\: :ref:`Callable<class_Callable>`\ )                                                   |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_drag_preview<class_Control_method_set_drag_preview>`\ (\ control\: :ref:`Control<class_Control>`\ )                                                                                                                                                           |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_end<class_Control_method_set_end>`\ (\ position\: :ref:`Vector2<class_Vector2>`\ )                                                                                                                                                                            |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_focus_neighbor<class_Control_method_set_focus_neighbor>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ )                                                                                                        |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_global_position<class_Control_method_set_global_position>`\ (\ position\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ )                                                                                                    |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_offset<class_Control_method_set_offset>`\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ )                                                                                                                                |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_offsets_preset<class_Control_method_set_offsets_preset>`\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, resize_mode\: :ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` = 0, margin\: :ref:`int<class_int>` = 0\ )                         |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_position<class_Control_method_set_position>`\ (\ position\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ )                                                                                                                  |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_size<class_Control_method_set_size>`\ (\ size\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ )                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`update_maximum_size<class_Control_method_update_maximum_size>`\ (\ )                                                                                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`update_minimum_size<class_Control_method_update_minimum_size>`\ (\ )                                                                                                                                                                                              |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`warp_mouse<class_Control_method_warp_mouse>`\ (\ position\: :ref:`Vector2<class_Vector2>`\ )                                                                                                                                                                      |
   +--------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_Control_signal_focus_entered:

.. rst-class:: classref-signal

**focus_entered**\ (\ ) :ref:`🔗<class_Control_signal_focus_entered>`

Được phát khi node nhận focus.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_focus_exited:

.. rst-class:: classref-signal

**focus_exited**\ (\ ) :ref:`🔗<class_Control_signal_focus_exited>`

Được phát khi node mất focus.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_gui_input:

.. rst-class:: classref-signal

**gui_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) :ref:`🔗<class_Control_signal_gui_input>`

Được phát khi node nhận một :ref:`InputEvent<class_InputEvent>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_maximum_size_changed:

.. rst-class:: classref-signal

**maximum_size_changed**\ (\ ) :ref:`🔗<class_Control_signal_maximum_size_changed>`

Được phát khi kích thước tối đa của node thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_minimum_size_changed:

.. rst-class:: classref-signal

**minimum_size_changed**\ (\ ) :ref:`🔗<class_Control_signal_minimum_size_changed>`

Được phát khi kích thước tối thiểu của node thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_mouse_entered:

.. rst-class:: classref-signal

**mouse_entered**\ (\ ) :ref:`🔗<class_Control_signal_mouse_entered>`

Được phát khi con trỏ chuột đi vào vùng hiển thị của control (hoặc bất kỳ control con nào), không bị che khuất phía sau các Control hoặc Window khác, miễn là :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép event đến được nó, bất kể nó hiện đang được focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến việc Control nào nhận signal.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_mouse_exited:

.. rst-class:: classref-signal

**mouse_exited**\ (\ ) :ref:`🔗<class_Control_signal_mouse_exited>`

Được phát khi con trỏ chuột rời khỏi vùng hiển thị của control (và tất cả control con), không bị che khuất phía sau các Control hoặc Window khác, miễn là :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép event đến được nó, bất kể nó hiện đang được focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến việc Control nào nhận signal.

\ **Lưu ý:** Nếu bạn muốn kiểm tra xem chuột có thực sự rời khỏi vùng này hay không, bỏ qua mọi node ở trên, bạn có thể dùng đoạn code như sau:

::

    func _on_mouse_exited():
        if not Rect2(Vector2(), size).has_point(get_local_mouse_position()):
            # Không di chuột trên vùng.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_resized:

.. rst-class:: classref-signal

**resized**\ (\ ) :ref:`🔗<class_Control_signal_resized>`

Được phát khi kích thước của control thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_size_flags_changed:

.. rst-class:: classref-signal

**size_flags_changed**\ (\ ) :ref:`🔗<class_Control_signal_size_flags_changed>`

Được phát khi một trong các size flag thay đổi. Xem :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_signal_theme_changed:

.. rst-class:: classref-signal

**theme_changed**\ (\ ) :ref:`🔗<class_Control_signal_theme_changed>`

Được phát khi notification :ref:`NOTIFICATION_THEME_CHANGED<class_Control_constant_NOTIFICATION_THEME_CHANGED>` được gửi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_Control_FocusMode:

.. rst-class:: classref-enumeration

enum **FocusMode**: :ref:`🔗<enum_Control_FocusMode>`

.. _class_Control_constant_FOCUS_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`FocusMode<enum_Control_FocusMode>` **FOCUS_NONE** = ``0``

Node không thể nhận focus. Dùng với :ref:`focus_mode<class_Control_property_focus_mode>`.

.. _class_Control_constant_FOCUS_CLICK:

.. rst-class:: classref-enumeration-constant

:ref:`FocusMode<enum_Control_FocusMode>` **FOCUS_CLICK** = ``1``

Node chỉ có thể nhận focus khi nhấp chuột. Dùng với :ref:`focus_mode<class_Control_property_focus_mode>`.

.. _class_Control_constant_FOCUS_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`FocusMode<enum_Control_FocusMode>` **FOCUS_ALL** = ``2``

Node có thể nhận focus khi nhấp chuột, sử dụng các phím mũi tên và Tab trên bàn phím, hoặc sử dụng các nút D-pad trên gamepad. Dùng với :ref:`focus_mode<class_Control_property_focus_mode>`.

.. _class_Control_constant_FOCUS_ACCESSIBILITY:

.. rst-class:: classref-enumeration-constant

:ref:`FocusMode<enum_Control_FocusMode>` **FOCUS_ACCESSIBILITY** = ``3``

Node chỉ có thể nhận focus khi screen reader đang hoạt động. Dùng với :ref:`focus_mode<class_Control_property_focus_mode>`.

.. rst-class:: classref-item-separator

----

.. _enum_Control_FocusBehaviorRecursive:

.. rst-class:: classref-enumeration

enum **FocusBehaviorRecursive**: :ref:`🔗<enum_Control_FocusBehaviorRecursive>`

.. _class_Control_constant_FOCUS_BEHAVIOR_INHERITED:

.. rst-class:: classref-enumeration-constant

:ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>` **FOCUS_BEHAVIOR_INHERITED** = ``0``

Kế thừa :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>` từ control cha. Nếu không có control cha, giá trị này giống với :ref:`FOCUS_BEHAVIOR_ENABLED<class_Control_constant_FOCUS_BEHAVIOR_ENABLED>`.

.. _class_Control_constant_FOCUS_BEHAVIOR_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>` **FOCUS_BEHAVIOR_DISABLED** = ``1``

Ngăn control nhận focus. :ref:`get_focus_mode_with_override()<class_Control_method_get_focus_mode_with_override>` sẽ trả về :ref:`FOCUS_NONE<class_Control_constant_FOCUS_NONE>`.

.. _class_Control_constant_FOCUS_BEHAVIOR_ENABLED:

.. rst-class:: classref-enumeration-constant

:ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>` **FOCUS_BEHAVIOR_ENABLED** = ``2``

Cho phép control được focus, tùy thuộc vào :ref:`focus_mode<class_Control_property_focus_mode>`. Có thể dùng tùy chọn này để bỏ qua :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>` của control cha. :ref:`get_focus_mode_with_override()<class_Control_method_get_focus_mode_with_override>` sẽ trả về :ref:`focus_mode<class_Control_property_focus_mode>`.

.. rst-class:: classref-item-separator

----

.. _enum_Control_MouseBehaviorRecursive:

.. rst-class:: classref-enumeration

enum **MouseBehaviorRecursive**: :ref:`🔗<enum_Control_MouseBehaviorRecursive>`

.. _class_Control_constant_MOUSE_BEHAVIOR_INHERITED:

.. rst-class:: classref-enumeration-constant

:ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>` **MOUSE_BEHAVIOR_INHERITED** = ``0``

Kế thừa :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>` từ control cha. Nếu không có control cha, giá trị này giống với :ref:`MOUSE_BEHAVIOR_ENABLED<class_Control_constant_MOUSE_BEHAVIOR_ENABLED>`.

.. _class_Control_constant_MOUSE_BEHAVIOR_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>` **MOUSE_BEHAVIOR_DISABLED** = ``1``

Ngăn control nhận input chuột. :ref:`get_mouse_filter_with_override()<class_Control_method_get_mouse_filter_with_override>` sẽ trả về :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>`.

.. _class_Control_constant_MOUSE_BEHAVIOR_ENABLED:

.. rst-class:: classref-enumeration-constant

:ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>` **MOUSE_BEHAVIOR_ENABLED** = ``2``

Cho phép control nhận input chuột, tùy thuộc vào :ref:`mouse_filter<class_Control_property_mouse_filter>`. Có thể dùng tùy chọn này để bỏ qua :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>` của control cha. :ref:`get_mouse_filter_with_override()<class_Control_method_get_mouse_filter_with_override>` sẽ trả về :ref:`mouse_filter<class_Control_property_mouse_filter>`.

.. rst-class:: classref-item-separator

----

.. _enum_Control_CursorShape:

.. rst-class:: classref-enumeration

enum **CursorShape**: :ref:`🔗<enum_Control_CursorShape>`

.. _class_Control_constant_CURSOR_ARROW:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_ARROW** = ``0``

Hiển thị con trỏ chuột mũi tên của hệ thống khi người dùng di chuột lên node. Dùng với :ref:`mouse_default_cursor_shape<class_Control_property_mouse_default_cursor_shape>`.

.. _class_Control_constant_CURSOR_IBEAM:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_IBEAM** = ``1``

Hiển thị con trỏ chuột dạng I-beam của hệ thống khi người dùng di chuột lên node. Con trỏ I-beam có hình dạng tương tự chữ "I". Nó cho người dùng biết họ có thể bôi chọn hoặc chèn văn bản.

.. _class_Control_constant_CURSOR_POINTING_HAND:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_POINTING_HAND** = ``2``

Hiển thị con trỏ chuột hình bàn tay chỉ của hệ thống khi người dùng di chuột lên node.

.. _class_Control_constant_CURSOR_CROSS:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_CROSS** = ``3``

Hiển thị con trỏ chuột hình chữ thập của hệ thống khi người dùng di chuột lên node.

.. _class_Control_constant_CURSOR_WAIT:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_WAIT** = ``4``

Hiển thị con trỏ chuột chờ của hệ thống khi người dùng di chuột qua node. Thường là hình đồng hồ cát.

.. _class_Control_constant_CURSOR_BUSY:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_BUSY** = ``5``

Hiển thị con trỏ chuột bận của hệ thống khi người dùng di chuột qua node. Thường là mũi tên có một đồng hồ cát nhỏ.

.. _class_Control_constant_CURSOR_DRAG:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_DRAG** = ``6``

Hiển thị con trỏ chuột kéo của hệ thống, thường là nắm tay khép lại hoặc biểu tượng chữ thập, khi người dùng di chuột qua node. Con trỏ này cho người dùng biết họ hiện đang kéo một mục, chẳng hạn như một node trong Scene dock.

.. _class_Control_constant_CURSOR_CAN_DROP:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_CAN_DROP** = ``7``

Hiển thị con trỏ chuột thả của hệ thống khi người dùng di chuột qua node. Con trỏ này có thể là bàn tay mở. Nó cho người dùng biết họ có thể thả mục đang cầm, chẳng hạn như một node trong Scene dock.

.. _class_Control_constant_CURSOR_FORBIDDEN:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_FORBIDDEN** = ``8``

Hiển thị con trỏ chuột cấm của hệ thống khi người dùng di chuột qua node. Thường là một vòng tròn có gạch chéo.

.. _class_Control_constant_CURSOR_VSIZE:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_VSIZE** = ``9``

Hiển thị con trỏ chuột thay đổi kích thước theo chiều dọc của hệ thống khi người dùng di chuột qua node. Đây là mũi tên dọc hai đầu. Nó cho người dùng biết họ có thể thay đổi kích thước cửa sổ hoặc panel theo chiều dọc.

.. _class_Control_constant_CURSOR_HSIZE:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_HSIZE** = ``10``

Hiển thị con trỏ chuột thay đổi kích thước theo chiều ngang của hệ thống khi người dùng di chuột qua node. Đây là mũi tên ngang hai đầu. Nó cho người dùng biết họ có thể thay đổi kích thước cửa sổ hoặc panel theo chiều ngang.

.. _class_Control_constant_CURSOR_BDIAGSIZE:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_BDIAGSIZE** = ``11``

Hiển thị con trỏ chuột thay đổi kích thước cửa sổ của hệ thống khi người dùng di chuột qua node. Con trỏ là một mũi tên hai đầu đi từ dưới trái lên trên phải. Nó cho người dùng biết họ có thể thay đổi kích thước cửa sổ hoặc panel theo cả chiều ngang và chiều dọc.

.. _class_Control_constant_CURSOR_FDIAGSIZE:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_FDIAGSIZE** = ``12``

Hiển thị con trỏ chuột thay đổi kích thước cửa sổ của hệ thống khi người dùng di chuột qua node. Con trỏ là một mũi tên hai đầu đi từ trên trái xuống dưới phải, ngược với :ref:`CURSOR_BDIAGSIZE<class_Control_constant_CURSOR_BDIAGSIZE>`. Nó cho người dùng biết họ có thể thay đổi kích thước cửa sổ hoặc panel theo cả chiều ngang và chiều dọc.

.. _class_Control_constant_CURSOR_MOVE:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_MOVE** = ``13``

Hiển thị con trỏ chuột di chuyển của hệ thống khi người dùng di chuột qua node. Con trỏ hiển thị 2 mũi tên hai đầu tạo thành góc 90 độ. Nó cho người dùng biết họ có thể tự do di chuyển một phần tử UI.

.. _class_Control_constant_CURSOR_VSPLIT:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_VSPLIT** = ``14``

Hiển thị con trỏ chuột chia dọc của hệ thống khi người dùng di chuột qua node. Trên Windows, nó giống :ref:`CURSOR_VSIZE<class_Control_constant_CURSOR_VSIZE>`.

.. _class_Control_constant_CURSOR_HSPLIT:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_HSPLIT** = ``15``

Hiển thị con trỏ chuột chia ngang của hệ thống khi người dùng di chuột qua node. Trên Windows, nó giống :ref:`CURSOR_HSIZE<class_Control_constant_CURSOR_HSIZE>`.

.. _class_Control_constant_CURSOR_HELP:

.. rst-class:: classref-enumeration-constant

:ref:`CursorShape<enum_Control_CursorShape>` **CURSOR_HELP** = ``16``

Hiển thị con trỏ chuột trợ giúp của hệ thống khi người dùng di chuột qua node, có dạng dấu hỏi.

.. rst-class:: classref-item-separator

----

.. _enum_Control_LayoutPreset:

.. rst-class:: classref-enumeration

enum **LayoutPreset**: :ref:`🔗<enum_Control_LayoutPreset>`

.. _class_Control_constant_PRESET_TOP_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_TOP_LEFT** = ``0``

Căn cả 4 anchor vào góc trên bên trái của giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_TOP_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_TOP_RIGHT** = ``1``

Căn cả 4 anchor vào góc trên bên phải của giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_BOTTOM_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_BOTTOM_LEFT** = ``2``

Căn cả 4 anchor vào góc dưới bên trái của giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_BOTTOM_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_BOTTOM_RIGHT** = ``3``

Căn cả 4 anchor vào góc dưới bên phải của giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_CENTER_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_CENTER_LEFT** = ``4``

Căn cả 4 anchor vào tâm của cạnh trái trong giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_CENTER_TOP:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_CENTER_TOP** = ``5``

Căn cả 4 anchor vào tâm của cạnh trên trong giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_CENTER_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_CENTER_RIGHT** = ``6``

Căn cả 4 anchor vào tâm của cạnh phải trong giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_CENTER_BOTTOM:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_CENTER_BOTTOM** = ``7``

Căn cả 4 anchor vào tâm của cạnh dưới trong giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_CENTER** = ``8``

Căn cả 4 anchor vào tâm của giới hạn của parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_LEFT_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_LEFT_WIDE** = ``9``

Căn cả 4 anchor vào cạnh trái của parent control. Offset trái trở thành tương đối với cạnh trái, còn offset trên tương đối với góc trên bên trái của parent của node. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_TOP_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_TOP_WIDE** = ``10``

Căn cả 4 anchor vào cạnh trên của parent control. Offset trái trở thành tương đối với góc trên bên trái, offset trên tương đối với cạnh trên và offset phải tương đối với góc trên bên phải của parent của node. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_RIGHT_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_RIGHT_WIDE** = ``11``

Căn cả 4 anchor vào cạnh phải của parent control. Offset phải trở thành tương đối với cạnh phải, còn offset trên tương đối với góc trên bên phải của parent của node. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_BOTTOM_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_BOTTOM_WIDE** = ``12``

Căn cả 4 anchor vào cạnh dưới của parent control. Offset trái trở thành tương đối với góc dưới bên trái, offset dưới tương đối với cạnh dưới và offset phải tương đối với góc dưới bên phải của parent của node. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_VCENTER_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_VCENTER_WIDE** = ``13``

Căn cả 4 anchor vào một đường dọc chia parent control thành hai nửa. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_HCENTER_WIDE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_HCENTER_WIDE** = ``14``

Căn cả 4 anchor vào một đường ngang chia parent control thành hai nửa. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_PRESET_FULL_RECT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPreset<enum_Control_LayoutPreset>` **PRESET_FULL_RECT** = ``15``

Căn cả 4 anchor vào các góc tương ứng của parent control. Đặt cả 4 offset thành 0 sau khi áp dụng preset này, khi đó **Control** sẽ vừa khít với parent control. Dùng với :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. rst-class:: classref-item-separator

----

.. _enum_Control_LayoutPresetMode:

.. rst-class:: classref-enumeration

enum **LayoutPresetMode**: :ref:`🔗<enum_Control_LayoutPresetMode>`

.. _class_Control_constant_PRESET_MODE_MINSIZE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` **PRESET_MODE_MINSIZE** = ``0``

Control sẽ được thay đổi kích thước thành kích thước tối thiểu.

.. _class_Control_constant_PRESET_MODE_KEEP_WIDTH:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` **PRESET_MODE_KEEP_WIDTH** = ``1``

Chiều rộng của control sẽ không thay đổi.

.. _class_Control_constant_PRESET_MODE_KEEP_HEIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` **PRESET_MODE_KEEP_HEIGHT** = ``2``

Chiều cao của control sẽ không thay đổi.

.. _class_Control_constant_PRESET_MODE_KEEP_SIZE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` **PRESET_MODE_KEEP_SIZE** = ``3``

Kích thước của control sẽ không thay đổi.

.. rst-class:: classref-item-separator

----

.. _enum_Control_SizeFlags:

.. rst-class:: classref-enumeration

flags **SizeFlags**: :ref:`🔗<enum_Control_SizeFlags>`

.. _class_Control_constant_SIZE_SHRINK_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_SHRINK_BEGIN** = ``0``

Cho parent :ref:`Container<class_Container>` biết cần căn node về phía bắt đầu, tức cạnh trên hoặc cạnh trái. Flag này loại trừ lẫn nhau với :ref:`SIZE_FILL<class_Control_constant_SIZE_FILL>` và các shrink size flag khác, nhưng có thể được dùng với :ref:`SIZE_EXPAND<class_Control_constant_SIZE_EXPAND>` trong một số container. Dùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

\ **Lưu ý:** Việc đặt flag này tương đương với không có size flag nào.

.. _class_Control_constant_SIZE_FILL:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_FILL** = ``1``

Cho parent :ref:`Container<class_Container>` biết cần mở rộng giới hạn của node này để lấp đầy toàn bộ không gian khả dụng mà không đẩy node nào khác. Flag này loại trừ lẫn nhau với các shrink size flag. Dùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

.. _class_Control_constant_SIZE_EXPAND:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_EXPAND** = ``2``

Cho parent :ref:`Container<class_Container>` biết cần để node này chiếm toàn bộ không gian khả dụng trên axis được đánh dấu. Nếu nhiều node liền kề được đặt thành expand, chúng sẽ chia sẻ không gian dựa trên stretch ratio. Xem :ref:`size_flags_stretch_ratio<class_Control_property_size_flags_stretch_ratio>`. Dùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

.. _class_Control_constant_SIZE_EXPAND_FILL:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_EXPAND_FILL** = ``3``

Đặt size flag của node thành cả fill và expand. Xem :ref:`SIZE_FILL<class_Control_constant_SIZE_FILL>` và :ref:`SIZE_EXPAND<class_Control_constant_SIZE_EXPAND>` để biết thêm thông tin.

.. _class_Control_constant_SIZE_SHRINK_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_SHRINK_CENTER** = ``4``

Cho parent :ref:`Container<class_Container>` biết cần căn node vào giữa không gian khả dụng. Flag này loại trừ lẫn nhau với :ref:`SIZE_FILL<class_Control_constant_SIZE_FILL>` và các shrink size flag khác, nhưng có thể được dùng với :ref:`SIZE_EXPAND<class_Control_constant_SIZE_EXPAND>` trong một số container. Dùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

.. _class_Control_constant_SIZE_SHRINK_END:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_SHRINK_END** = ``8``

Cho parent :ref:`Container<class_Container>` biết cần căn node về phía kết thúc, tức cạnh dưới hoặc cạnh phải. Flag này loại trừ lẫn nhau với :ref:`SIZE_FILL<class_Control_constant_SIZE_FILL>` và các shrink size flag khác, nhưng có thể được dùng với :ref:`SIZE_EXPAND<class_Control_constant_SIZE_EXPAND>` trong một số container. Dùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

.. _class_Control_constant_SIZE_MAXIMIZE:

.. rst-class:: classref-enumeration-constant

:ref:`SizeFlags<enum_Control_SizeFlags>` **SIZE_MAXIMIZE** = ``16``

Cho parent :ref:`Container<class_Container>` sử dụng :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` của node khi thực hiện các phép tính kích thước tối thiểu. Sử dụng cùng với :ref:`size_flags_horizontal<class_Control_property_size_flags_horizontal>` và :ref:`size_flags_vertical<class_Control_property_size_flags_vertical>`.

\ **Lưu ý:** Việc đặt flag này không nhất thiết có nghĩa là node sẽ được thay đổi kích thước thành kích thước tối đa, vì container cha có thể không có đủ không gian để thực hiện việc đó.

\ **Lưu ý:** Nếu node này là con của một Container bật thuộc tính :ref:`size_flags_stretch_ratio<class_Control_property_size_flags_stretch_ratio>` trên các node con để bố cục, các node được đặt flag này sẽ được ưu tiên khi kéo giãn. Nếu nhiều node được đặt flag này, các tỷ lệ kéo giãn tương đối của chúng vẫn được giữ nguyên.

.. rst-class:: classref-item-separator

----

.. _enum_Control_MouseFilter:

.. rst-class:: classref-enumeration

enum **MouseFilter**: :ref:`🔗<enum_Control_MouseFilter>`

.. _class_Control_constant_MOUSE_FILTER_STOP:

.. rst-class:: classref-enumeration-constant

:ref:`MouseFilter<enum_Control_MouseFilter>` **MOUSE_FILTER_STOP** = ``0``

Control sẽ nhận các sự kiện input chuyển động chuột và các sự kiện input nút chuột nếu được nhấp qua :ref:`_gui_input()<class_Control_private_method__gui_input>`. Control cũng sẽ nhận các signal :ref:`mouse_entered<class_Control_signal_mouse_entered>` và :ref:`mouse_exited<class_Control_signal_mouse_exited>`. Các sự kiện này tự động được đánh dấu là đã xử lý và sẽ không lan truyền tiếp đến các control khác. Điều này cũng khiến các signal trong những control khác bị chặn.

.. _class_Control_constant_MOUSE_FILTER_PASS:

.. rst-class:: classref-enumeration-constant

:ref:`MouseFilter<enum_Control_MouseFilter>` **MOUSE_FILTER_PASS** = ``1``

Control sẽ nhận các sự kiện input chuyển động chuột và các sự kiện input nút chuột nếu được nhấp qua :ref:`_gui_input()<class_Control_private_method__gui_input>`. Control cũng sẽ nhận các signal :ref:`mouse_entered<class_Control_signal_mouse_entered>` và :ref:`mouse_exited<class_Control_signal_mouse_exited>`.

Nếu control này không xử lý sự kiện, sự kiện sẽ lan truyền lên control cha của nó nếu có. Sự kiện được truyền ngược lên hệ phân cấp node cho đến khi gặp một node không phải :ref:`CanvasItem<class_CanvasItem>`, một control có :ref:`MOUSE_FILTER_STOP<class_Control_constant_MOUSE_FILTER_STOP>`, hoặc một :ref:`CanvasItem<class_CanvasItem>` bật :ref:`CanvasItem.top_level<class_CanvasItem_property_top_level>`. Điều này cho phép các signal được phát trong tất cả control mà sự kiện đi qua. Nếu không có control nào xử lý sự kiện, sự kiện sẽ được chuyển đến :ref:`Node._shortcut_input()<class_Node_private_method__shortcut_input>` để xử lý thêm.

.. _class_Control_constant_MOUSE_FILTER_IGNORE:

.. rst-class:: classref-enumeration-constant

:ref:`MouseFilter<enum_Control_MouseFilter>` **MOUSE_FILTER_IGNORE** = ``2``

Control sẽ không nhận bất kỳ sự kiện input chuyển động chuột nào cũng như sự kiện input nút chuột nào thông qua :ref:`_gui_input()<class_Control_private_method__gui_input>`. Control cũng sẽ không nhận các signal :ref:`mouse_entered<class_Control_signal_mouse_entered>` và :ref:`mouse_exited<class_Control_signal_mouse_exited>`. Điều này không ngăn các control khác nhận những sự kiện này hoặc phát các signal. Các sự kiện bị bỏ qua sẽ không tự động được xử lý. Nếu một node con có :ref:`MOUSE_FILTER_PASS<class_Control_constant_MOUSE_FILTER_PASS>` và một sự kiện được truyền đến control này, sự kiện sẽ tiếp tục lan truyền lên control cha của control.

\ **Lưu ý:** Nếu control đã nhận :ref:`mouse_entered<class_Control_signal_mouse_entered>` nhưng chưa nhận :ref:`mouse_exited<class_Control_signal_mouse_exited>`, việc thay đổi :ref:`mouse_filter<class_Control_property_mouse_filter>` thành :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>` sẽ khiến :ref:`mouse_exited<class_Control_signal_mouse_exited>` được phát.

.. rst-class:: classref-item-separator

----

.. _enum_Control_GrowDirection:

.. rst-class:: classref-enumeration

enum **GrowDirection**: :ref:`🔗<enum_Control_GrowDirection>`

.. _class_Control_constant_GROW_DIRECTION_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`GrowDirection<enum_Control_GrowDirection>` **GROW_DIRECTION_BEGIN** = ``0``

Control sẽ tăng/giảm kích thước về bên trái hoặc phía trên nếu kích thước của nó được thay đổi để lớn hơn/nhỏ hơn kích thước hiện tại trên trục tương ứng.

.. _class_Control_constant_GROW_DIRECTION_END:

.. rst-class:: classref-enumeration-constant

:ref:`GrowDirection<enum_Control_GrowDirection>` **GROW_DIRECTION_END** = ``1``

Control sẽ tăng/giảm kích thước về bên phải hoặc phía dưới nếu kích thước của nó được thay đổi để lớn hơn/nhỏ hơn kích thước hiện tại trên trục tương ứng.

.. _class_Control_constant_GROW_DIRECTION_BOTH:

.. rst-class:: classref-enumeration-constant

:ref:`GrowDirection<enum_Control_GrowDirection>` **GROW_DIRECTION_BOTH** = ``2``

Control sẽ tăng/giảm kích thước theo cả hai hướng như nhau nếu kích thước của nó được thay đổi để lớn hơn/nhỏ hơn kích thước hiện tại.

.. rst-class:: classref-item-separator

----

.. _enum_Control_Anchor:

.. rst-class:: classref-enumeration

enum **Anchor**: :ref:`🔗<enum_Control_Anchor>`

.. _class_Control_constant_ANCHOR_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`Anchor<enum_Control_Anchor>` **ANCHOR_BEGIN** = ``0``

Gắn một trong 4 cạnh anchor vào gốc của ``Rect`` của node, ở phía trên bên trái. Sử dụng cùng với một trong các biến thành viên ``anchor_*``, chẳng hạn như :ref:`anchor_left<class_Control_property_anchor_left>`. Để thay đổi cả 4 anchor cùng lúc, hãy sử dụng :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. _class_Control_constant_ANCHOR_END:

.. rst-class:: classref-enumeration-constant

:ref:`Anchor<enum_Control_Anchor>` **ANCHOR_END** = ``1``

Gắn một trong 4 cạnh anchor vào điểm cuối của ``Rect`` của node, ở phía dưới bên phải. Sử dụng cùng với một trong các biến thành viên ``anchor_*``, chẳng hạn như :ref:`anchor_left<class_Control_property_anchor_left>`. Để thay đổi cả 4 anchor cùng lúc, hãy sử dụng :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>`.

.. rst-class:: classref-item-separator

----

.. _enum_Control_LayoutDirection:

.. rst-class:: classref-enumeration

enum **LayoutDirection**: :ref:`🔗<enum_Control_LayoutDirection>`

.. _class_Control_constant_LAYOUT_DIRECTION_INHERITED:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_INHERITED** = ``0``

Hướng bố cục tự động, được xác định từ hướng bố cục của control cha.

.. _class_Control_constant_LAYOUT_DIRECTION_APPLICATION_LOCALE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_APPLICATION_LOCALE** = ``1``

Hướng bố cục tự động, được xác định từ locale hiện tại. Hướng bố cục từ phải sang trái được tự động sử dụng cho các ngôn ngữ yêu cầu hướng này, chẳng hạn như tiếng Ả Rập và tiếng Hebrew, nhưng chỉ khi một tệp bản dịch hợp lệ được tải cho ngôn ngữ tương ứng (trừ khi ngôn ngữ đó được cấu hình làm dự phòng trong :ref:`ProjectSettings.internationalization/locale/fallback<class_ProjectSettings_property_internationalization/locale/fallback>`). Với tất cả ngôn ngữ khác (hoặc nếu Godot không tìm thấy tệp bản dịch hợp lệ), hướng bố cục từ trái sang phải sẽ được sử dụng. Khi sử dụng :ref:`TextServerFallback<class_TextServerFallback>` (:ref:`ProjectSettings.internationalization/rendering/text_driver<class_ProjectSettings_property_internationalization/rendering/text_driver>`), hướng bố cục từ trái sang phải luôn được sử dụng bất kể ngôn ngữ nào. Cũng có thể buộc sử dụng hướng bố cục từ phải sang trái bằng :ref:`ProjectSettings.internationalization/rendering/force_right_to_left_layout_direction<class_ProjectSettings_property_internationalization/rendering/force_right_to_left_layout_direction>`.

.. _class_Control_constant_LAYOUT_DIRECTION_LTR:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_LTR** = ``2``

Hướng bố cục từ trái sang phải.

.. _class_Control_constant_LAYOUT_DIRECTION_RTL:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_RTL** = ``3``

Hướng bố cục từ phải sang trái.

.. _class_Control_constant_LAYOUT_DIRECTION_SYSTEM_LOCALE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_SYSTEM_LOCALE** = ``4``

Hướng bố cục tự động, được xác định từ locale hệ thống. Hướng bố cục từ phải sang trái được tự động sử dụng cho các ngôn ngữ yêu cầu hướng này, chẳng hạn như tiếng Ả Rập và tiếng Hebrew, nhưng chỉ khi một tệp bản dịch hợp lệ được tải cho ngôn ngữ tương ứng. Với tất cả ngôn ngữ khác (hoặc nếu Godot không tìm thấy tệp bản dịch hợp lệ), hướng bố cục từ trái sang phải sẽ được sử dụng. Khi sử dụng :ref:`TextServerFallback<class_TextServerFallback>` (:ref:`ProjectSettings.internationalization/rendering/text_driver<class_ProjectSettings_property_internationalization/rendering/text_driver>`), hướng bố cục từ trái sang phải luôn được sử dụng bất kể ngôn ngữ nào.

.. _class_Control_constant_LAYOUT_DIRECTION_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_MAX** = ``5``

Biểu thị kích thước của enum :ref:`LayoutDirection<enum_Control_LayoutDirection>`.

.. _class_Control_constant_LAYOUT_DIRECTION_LOCALE:

.. rst-class:: classref-enumeration-constant

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **LAYOUT_DIRECTION_LOCALE** = ``1``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`LAYOUT_DIRECTION_APPLICATION_LOCALE<class_Control_constant_LAYOUT_DIRECTION_APPLICATION_LOCALE>`.



.. rst-class:: classref-item-separator

----

.. _enum_Control_TextDirection:

.. rst-class:: classref-enumeration

enum **TextDirection**: :ref:`🔗<enum_Control_TextDirection>`

.. _class_Control_constant_TEXT_DIRECTION_INHERITED:

.. rst-class:: classref-enumeration-constant

:ref:`TextDirection<enum_Control_TextDirection>` **TEXT_DIRECTION_INHERITED** = ``3``

Hướng viết văn bản giống với hướng bố cục.

.. _class_Control_constant_TEXT_DIRECTION_AUTO:

.. rst-class:: classref-enumeration-constant

:ref:`TextDirection<enum_Control_TextDirection>` **TEXT_DIRECTION_AUTO** = ``0``

Hướng viết văn bản tự động, được xác định từ locale hiện tại và nội dung văn bản.

.. _class_Control_constant_TEXT_DIRECTION_LTR:

.. rst-class:: classref-enumeration-constant

:ref:`TextDirection<enum_Control_TextDirection>` **TEXT_DIRECTION_LTR** = ``1``

Hướng viết văn bản từ trái sang phải.

.. _class_Control_constant_TEXT_DIRECTION_RTL:

.. rst-class:: classref-enumeration-constant

:ref:`TextDirection<enum_Control_TextDirection>` **TEXT_DIRECTION_RTL** = ``2``

Hướng viết văn bản từ phải sang trái.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_Control_constant_NOTIFICATION_RESIZED:

.. rst-class:: classref-constant

**NOTIFICATION_RESIZED** = ``40`` :ref:`🔗<class_Control_constant_NOTIFICATION_RESIZED>`

Được gửi khi kích thước của node thay đổi. Sử dụng :ref:`size<class_Control_property_size>` để lấy kích thước mới.

.. _class_Control_constant_NOTIFICATION_MOUSE_ENTER:

.. rst-class:: classref-constant

**NOTIFICATION_MOUSE_ENTER** = ``41`` :ref:`🔗<class_Control_constant_NOTIFICATION_MOUSE_ENTER>`

Được gửi khi con trỏ chuột đi vào vùng hiển thị của control (hoặc bất kỳ control con nào), nơi không bị các Control hoặc Window khác che khuất, với điều kiện :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép sự kiện đến được control đó và không phụ thuộc vào việc nó hiện có focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến Control nào nhận notification.

Xem thêm :ref:`NOTIFICATION_MOUSE_ENTER_SELF<class_Control_constant_NOTIFICATION_MOUSE_ENTER_SELF>`.

.. _class_Control_constant_NOTIFICATION_MOUSE_EXIT:

.. rst-class:: classref-constant

**NOTIFICATION_MOUSE_EXIT** = ``42`` :ref:`🔗<class_Control_constant_NOTIFICATION_MOUSE_EXIT>`

Được gửi khi con trỏ chuột rời khỏi vùng hiển thị của control (và tất cả control con), nơi không bị các Control hoặc Window khác che khuất, với điều kiện :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép sự kiện đến được control đó và không phụ thuộc vào việc nó hiện có focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến Control nào nhận notification.

Xem thêm :ref:`NOTIFICATION_MOUSE_EXIT_SELF<class_Control_constant_NOTIFICATION_MOUSE_EXIT_SELF>`.

.. _class_Control_constant_NOTIFICATION_MOUSE_ENTER_SELF:

.. rst-class:: classref-constant

**NOTIFICATION_MOUSE_ENTER_SELF** = ``60`` :ref:`🔗<class_Control_constant_NOTIFICATION_MOUSE_ENTER_SELF>`

**Thử nghiệm:** Lý do gửi notification này có thể thay đổi trong tương lai.

Được gửi khi con trỏ chuột đi vào vùng hiển thị của control, nơi không bị các Control hoặc Window khác che khuất, với điều kiện :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép sự kiện đến được control đó và không phụ thuộc vào việc nó hiện có focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến Control nào nhận notification.

Xem thêm :ref:`NOTIFICATION_MOUSE_ENTER<class_Control_constant_NOTIFICATION_MOUSE_ENTER>`.

.. _class_Control_constant_NOTIFICATION_MOUSE_EXIT_SELF:

.. rst-class:: classref-constant

**NOTIFICATION_MOUSE_EXIT_SELF** = ``61`` :ref:`🔗<class_Control_constant_NOTIFICATION_MOUSE_EXIT_SELF>`

**Thử nghiệm:** Lý do gửi notification này có thể thay đổi trong tương lai.

Được gửi khi con trỏ chuột rời khỏi vùng hiển thị của control, nơi không bị các Control hoặc Window khác che khuất, với điều kiện :ref:`mouse_filter<class_Control_property_mouse_filter>` của nó cho phép sự kiện đến được control đó và không phụ thuộc vào việc nó hiện có focus hay không.

\ **Lưu ý:** :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` không ảnh hưởng đến Control nào nhận notification.

Xem thêm :ref:`NOTIFICATION_MOUSE_EXIT<class_Control_constant_NOTIFICATION_MOUSE_EXIT>`.

.. _class_Control_constant_NOTIFICATION_FOCUS_ENTER:

.. rst-class:: classref-constant

**NOTIFICATION_FOCUS_ENTER** = ``43`` :ref:`🔗<class_Control_constant_NOTIFICATION_FOCUS_ENTER>`

Được gửi khi node nhận focus.

.. _class_Control_constant_NOTIFICATION_FOCUS_EXIT:

.. rst-class:: classref-constant

**NOTIFICATION_FOCUS_EXIT** = ``44`` :ref:`🔗<class_Control_constant_NOTIFICATION_FOCUS_EXIT>`

Được gửi khi node mất focus.

Notification này được gửi theo thứ tự ngược lại.

.. _class_Control_constant_NOTIFICATION_THEME_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_THEME_CHANGED** = ``45`` :ref:`🔗<class_Control_constant_NOTIFICATION_THEME_CHANGED>`

Được gửi khi node cần làm mới các mục theme. Điều này xảy ra trong một trong các trường hợp sau:

- Thuộc tính :ref:`theme<class_Control_property_theme>` được thay đổi trên node này hoặc bất kỳ ancestor nào của nó.

- Thuộc tính :ref:`theme_type_variation<class_Control_property_theme_type_variation>` được thay đổi trên node này.

- Một trong các ghi đè thuộc tính theme của node được thay đổi.

- Node đi vào scene tree.

\ **Lưu ý:** Để tối ưu hóa, notification này sẽ không được gửi đối với các thay đổi xảy ra khi node này nằm ngoài scene tree. Thay vào đó, tất cả cập nhật mục theme có thể được áp dụng cùng lúc khi node đi vào scene tree.

\ **Lưu ý:** Notification này được nhận cùng với :ref:`Node.NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>`, vì vậy nếu bạn đang instantiate một scene, các node con vẫn chưa được khởi tạo. Bạn có thể sử dụng nó để thiết lập theming cho node này và các node con được tạo từ script; hoặc nếu muốn truy cập các node con được thêm trong editor, hãy đảm bảo node đã sẵn sàng bằng :ref:`Node.is_node_ready()<class_Node_method_is_node_ready>`.

::

    func _notification(what):
        if what == NOTIFICATION_THEME_CHANGED:
            if not is_node_ready():
                await ready # Đợi signal ready.
            $Label.add_theme_color_override("font_color", Color.YELLOW)

.. _class_Control_constant_NOTIFICATION_SCROLL_BEGIN:

.. rst-class:: classref-constant

**NOTIFICATION_SCROLL_BEGIN** = ``47`` :ref:`🔗<class_Control_constant_NOTIFICATION_SCROLL_BEGIN>`

Được gửi khi node này nằm trong một :ref:`ScrollContainer<class_ScrollContainer>` đã bắt đầu được cuộn khi kéo vùng có thể cuộn *bằng một touch event*. Notification này *không* được gửi khi cuộn bằng cách kéo thanh cuộn, cuộn bằng con lăn chuột hoặc cuộn bằng các event từ bàn phím/gamepad.

\ **Lưu ý:** Signal này chỉ được phát trên Android hoặc iOS, hoặc trên các nền tảng desktop/web khi :ref:`ProjectSettings.input_devices/pointing/emulate_touch_from_mouse<class_ProjectSettings_property_input_devices/pointing/emulate_touch_from_mouse>` được bật.

.. _class_Control_constant_NOTIFICATION_SCROLL_END:

.. rst-class:: classref-constant

**NOTIFICATION_SCROLL_END** = ``48`` :ref:`🔗<class_Control_constant_NOTIFICATION_SCROLL_END>`

Được gửi khi node này nằm trong một :ref:`ScrollContainer<class_ScrollContainer>` đã dừng được cuộn khi kéo vùng có thể cuộn *bằng một touch event*. Notification này *không* được gửi khi cuộn bằng cách kéo thanh cuộn, cuộn bằng con lăn chuột hoặc cuộn bằng các event từ bàn phím/gamepad.

\ **Lưu ý:** Signal này chỉ được phát trên Android hoặc iOS, hoặc trên các nền tảng desktop/web khi :ref:`ProjectSettings.input_devices/pointing/emulate_touch_from_mouse<class_ProjectSettings_property_input_devices/pointing/emulate_touch_from_mouse>` được bật.

.. _class_Control_constant_NOTIFICATION_LAYOUT_DIRECTION_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_LAYOUT_DIRECTION_CHANGED** = ``49`` :ref:`🔗<class_Control_constant_NOTIFICATION_LAYOUT_DIRECTION_CHANGED>`

Được gửi khi hướng layout của control thay đổi từ LTR sang RTL hoặc ngược lại. Notification này được truyền đến các node Control con do thay đổi đối với :ref:`layout_direction<class_Control_property_layout_direction>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Control_property_accessibility_controls_nodes:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **accessibility_controls_nodes** = ``[]`` :ref:`🔗<class_Control_property_accessibility_controls_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_controls_nodes**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **get_accessibility_controls_nodes**\ (\ )

Các path đến những node được node này điều khiển.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_described_by_nodes:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **accessibility_described_by_nodes** = ``[]`` :ref:`🔗<class_Control_property_accessibility_described_by_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_described_by_nodes**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **get_accessibility_described_by_nodes**\ (\ )

Các path đến những node mô tả node này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **accessibility_description** = ``""`` :ref:`🔗<class_Control_property_accessibility_description>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_description**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_accessibility_description**\ (\ )

Mô tả node ở dạng con người có thể đọc được, được báo cáo cho các ứng dụng hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_flow_to_nodes:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **accessibility_flow_to_nodes** = ``[]`` :ref:`🔗<class_Control_property_accessibility_flow_to_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_flow_to_nodes**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **get_accessibility_flow_to_nodes**\ (\ )

Các path đến những node mà node này chuyển luồng tới.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_labeled_by_nodes:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **accessibility_labeled_by_nodes** = ``[]`` :ref:`🔗<class_Control_property_accessibility_labeled_by_nodes>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_labeled_by_nodes**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`NodePath<class_NodePath>`\] **get_accessibility_labeled_by_nodes**\ (\ )

Các path đến những node gắn nhãn cho node này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_live:

.. rst-class:: classref-property

:ref:`AccessibilityLiveMode<enum_AccessibilityServer_AccessibilityLiveMode>` **accessibility_live** = ``0`` :ref:`🔗<class_Control_property_accessibility_live>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_live**\ (\ value\: :ref:`AccessibilityLiveMode<enum_AccessibilityServer_AccessibilityLiveMode>`\ ) - :ref:`AccessibilityLiveMode<enum_AccessibilityServer_AccessibilityLiveMode>` **get_accessibility_live**\ (\ )

Chế độ dùng để cập nhật live region. Live region là một :ref:`Node<class_Node>` được cập nhật do một event bên ngoài khi focus của người dùng có thể đang ở nơi khác.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_accessibility_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **accessibility_name** = ``""`` :ref:`🔗<class_Control_property_accessibility_name>`

.. rst-class:: classref-property-setget

- |void| **set_accessibility_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_accessibility_name**\ (\ )

Tên node ở dạng con người có thể đọc được, được báo cáo cho các ứng dụng hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_anchor_bottom:

.. rst-class:: classref-property

:ref:`float<class_float>` **anchor_bottom** = ``0.0`` :ref:`🔗<class_Control_property_anchor_bottom>`

.. rst-class:: classref-property-setget

- :ref:`float<class_float>` **get_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Neo cạnh dưới của node vào gốc, tâm hoặc cuối của control cha. Điều này thay đổi cách offset dưới được cập nhật khi node di chuyển hoặc thay đổi kích thước. Bạn có thể sử dụng một trong các hằng số :ref:`Anchor<enum_Control_Anchor>` để thuận tiện.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_anchor_left:

.. rst-class:: classref-property

:ref:`float<class_float>` **anchor_left** = ``0.0`` :ref:`🔗<class_Control_property_anchor_left>`

.. rst-class:: classref-property-setget

- :ref:`float<class_float>` **get_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Neo cạnh trái của node vào gốc, tâm hoặc cuối của control cha. Điều này thay đổi cách offset trái được cập nhật khi node di chuyển hoặc thay đổi kích thước. Bạn có thể sử dụng một trong các hằng số :ref:`Anchor<enum_Control_Anchor>` để thuận tiện.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_anchor_right:

.. rst-class:: classref-property

:ref:`float<class_float>` **anchor_right** = ``0.0`` :ref:`🔗<class_Control_property_anchor_right>`

.. rst-class:: classref-property-setget

- :ref:`float<class_float>` **get_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Neo cạnh phải của node vào gốc, tâm hoặc cuối của control cha. Điều này thay đổi cách offset phải được cập nhật khi node di chuyển hoặc thay đổi kích thước. Bạn có thể sử dụng một trong các hằng số :ref:`Anchor<enum_Control_Anchor>` để thuận tiện.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_anchor_top:

.. rst-class:: classref-property

:ref:`float<class_float>` **anchor_top** = ``0.0`` :ref:`🔗<class_Control_property_anchor_top>`

.. rst-class:: classref-property-setget

- :ref:`float<class_float>` **get_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Neo cạnh trên của node vào gốc, tâm hoặc cuối của control cha. Điều này thay đổi cách offset trên được cập nhật khi node di chuyển hoặc thay đổi kích thước. Bạn có thể sử dụng một trong các hằng số :ref:`Anchor<enum_Control_Anchor>` để thuận tiện.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_auto_translate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **auto_translate** :ref:`🔗<class_Control_property_auto_translate>`

.. rst-class:: classref-property-setget

- |void| **set_auto_translate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_auto_translating**\ (\ )

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`Node.auto_translate_mode<class_Node_property_auto_translate_mode>` và :ref:`Node.can_auto_translate()<class_Node_method_can_auto_translate>`.

Bật/tắt việc tự động thay đổi văn bản sang phiên bản đã dịch tùy theo locale hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_clip_contents:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **clip_contents** = ``false`` :ref:`🔗<class_Control_property_clip_contents>`

.. rst-class:: classref-property-setget

- |void| **set_clip_contents**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_clipping_contents**\ (\ )

Cho phép cắt phần hiển thị của các child dựa trên :ref:`CanvasItem<class_CanvasItem>` theo hình chữ nhật của control này. Nếu ``true``, các phần của child nằm ngoài hình chữ nhật của control này sẽ không được render và sẽ không nhận input.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_custom_maximum_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **custom_maximum_size** = ``Vector2(-1, -1)`` :ref:`🔗<class_Control_property_custom_maximum_size>`

.. rst-class:: classref-property-setget

- |void| **set_custom_maximum_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_custom_maximum_size**\ (\ )

Kích thước tối đa của hình chữ nhật bao quanh node. Nếu được đặt thành giá trị lớn hơn hoặc bằng ``(0, 0)``, hình chữ nhật bao quanh node sẽ không bao giờ vượt quá kích thước này. Giá trị nhỏ hơn ``(0, 0)`` có nghĩa là không có kích thước tối đa. Giá trị này được ưu tiên hơn :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` nếu hai giá trị xung đột.

\ **Lưu ý:** Kích thước tối đa hiệu dụng cuối cùng có thể phụ thuộc vào kích thước tối đa của parent (thông qua :ref:`propagate_maximum_size<class_Control_property_propagate_maximum_size>`), vì vậy bạn nên sử dụng :ref:`get_combined_maximum_size()<class_Control_method_get_combined_maximum_size>` thay vì :ref:`get_maximum_size()<class_Control_method_get_maximum_size>`. Tương tự, hãy sử dụng :ref:`get_bound_minimum_size()<class_Control_method_get_bound_minimum_size>` thay vì :ref:`get_combined_minimum_size()<class_Control_method_get_combined_minimum_size>` để tính đến kích thước tối đa.

\ **Lưu ý:** Không phải tất cả subtype **Control** đều xử lý điều này một cách ổn thỏa, và nội dung của chúng có thể mở rộng vượt ra ngoài hình chữ nhật bao quanh. Đặt :ref:`clip_contents<class_Control_property_clip_contents>` thành ``true`` để ngăn các control con render bên ngoài kích thước này, đặc biệt khi node này là một :ref:`Container<class_Container>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_custom_minimum_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **custom_minimum_size** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_custom_minimum_size>`

.. rst-class:: classref-property-setget

- |void| **set_custom_minimum_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_custom_minimum_size**\ (\ )

Kích thước tối thiểu của hình chữ nhật bao quanh node. Nếu đặt thành giá trị lớn hơn ``(0, 0)``, hình chữ nhật bao quanh node sẽ luôn có ít nhất kích thước này. Lưu ý rằng các node **Control** nhận kích thước tối thiểu nội bộ của chúng từ :ref:`get_minimum_size()<class_Control_method_get_minimum_size>`. Kích thước này phụ thuộc vào nội dung của control, chẳng hạn như văn bản, texture hoặc hộp kiểu. Kích thước tối thiểu thực tế là giá trị lớn nhất giữa thuộc tính này và kích thước tối thiểu nội bộ (xem :ref:`get_combined_minimum_size()<class_Control_method_get_combined_minimum_size>`).

\ **Lưu ý:** :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` được ưu tiên hơn thuộc tính này. Ví dụ: nếu đặt :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` thành ``(200, 200)`` và :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` thành ``(100, 100)``, kích thước kết quả sẽ là ``(100, 100)``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_behavior_recursive:

.. rst-class:: classref-property

:ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>` **focus_behavior_recursive** = ``0`` :ref:`🔗<class_Control_property_focus_behavior_recursive>`

.. rst-class:: classref-property-setget

- |void| **set_focus_behavior_recursive**\ (\ value\: :ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>`\ ) - :ref:`FocusBehaviorRecursive<enum_Control_FocusBehaviorRecursive>` **get_focus_behavior_recursive**\ (\ )

Xác định những control nào có thể được focus cùng với :ref:`focus_mode<class_Control_property_focus_mode>`. Xem :ref:`get_focus_mode_with_override()<class_Control_method_get_focus_mode_with_override>`. Vì hành vi mặc định là :ref:`FOCUS_BEHAVIOR_INHERITED<class_Control_constant_FOCUS_BEHAVIOR_INHERITED>`, bạn có thể dùng thuộc tính này để ngăn tất cả control con nhận focus.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_mode:

.. rst-class:: classref-property

:ref:`FocusMode<enum_Control_FocusMode>` **focus_mode** = ``0`` :ref:`🔗<class_Control_property_focus_mode>`

.. rst-class:: classref-property-setget

- |void| **set_focus_mode**\ (\ value\: :ref:`FocusMode<enum_Control_FocusMode>`\ ) - :ref:`FocusMode<enum_Control_FocusMode>` **get_focus_mode**\ (\ )

Xác định những control nào có thể được focus. Mỗi thời điểm chỉ một control có thể được focus, và control đang được focus sẽ nhận các sự kiện bàn phím, gamepad và chuột trong :ref:`_gui_input()<class_Control_private_method__gui_input>`. Dùng :ref:`get_focus_mode_with_override()<class_Control_method_get_focus_mode_with_override>` để xác định liệu một control có thể lấy focus hay không, vì :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>` cũng ảnh hưởng đến điều này. Xem thêm :ref:`grab_focus()<class_Control_method_grab_focus>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_neighbor_bottom:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_neighbor_bottom** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_neighbor_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn phím mũi tên xuống trên bàn phím hoặc hướng xuống trên gamepad. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_down<class_ProjectSettings_property_input/ui_down>`. Node phải là một **Control**. Nếu không đặt thuộc tính này, Godot sẽ focus **Control** gần nhất ở phía dưới control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_neighbor_left:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_neighbor_left** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_neighbor_left>`

.. rst-class:: classref-property-setget

- |void| **set_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn phím mũi tên trái trên bàn phím hoặc hướng sang trái trên gamepad. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_left<class_ProjectSettings_property_input/ui_left>`. Node phải là một **Control**. Nếu không đặt thuộc tính này, Godot sẽ focus **Control** gần nhất ở bên trái control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_neighbor_right:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_neighbor_right** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_neighbor_right>`

.. rst-class:: classref-property-setget

- |void| **set_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn phím mũi tên phải trên bàn phím hoặc hướng sang phải trên gamepad. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_right<class_ProjectSettings_property_input/ui_right>`. Node phải là một **Control**. Nếu không đặt thuộc tính này, Godot sẽ focus **Control** gần nhất ở bên phải control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_neighbor_top:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_neighbor_top** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_neighbor_top>`

.. rst-class:: classref-property-setget

- |void| **set_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn phím mũi tên lên trên bàn phím hoặc hướng lên trên gamepad. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_up<class_ProjectSettings_property_input/ui_up>`. Node phải là một **Control**. Nếu không đặt thuộc tính này, Godot sẽ focus **Control** gần nhất ở phía trên control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_next:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_next** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_next>`

.. rst-class:: classref-property-setget

- |void| **set_focus_next**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_next**\ (\ )

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn :kbd:`Tab` trên bàn phím. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_focus_next<class_ProjectSettings_property_input/ui_focus_next>`.

Nếu không đặt thuộc tính này, Godot sẽ chọn một node "phỏng đoán tốt nhất" dựa trên các node xung quanh trong scene tree.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_focus_previous:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **focus_previous** = ``NodePath("")`` :ref:`🔗<class_Control_property_focus_previous>`

.. rst-class:: classref-property-setget

- |void| **set_focus_previous**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_focus_previous**\ (\ )

Theo mặc định, cho Godot biết node nào cần được focus nếu người dùng nhấn :kbd:`Shift + Tab` trên bàn phím. Bạn có thể thay đổi phím bằng cách chỉnh sửa input action :ref:`ProjectSettings.input/ui_focus_prev<class_ProjectSettings_property_input/ui_focus_prev>`.

Nếu không đặt thuộc tính này, Godot sẽ chọn một node "phỏng đoán tốt nhất" dựa trên các node xung quanh trong scene tree.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_global_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **global_position** :ref:`🔗<class_Control_property_global_position>`

.. rst-class:: classref-property-setget

- :ref:`Vector2<class_Vector2>` **get_global_position**\ (\ )

Vị trí global của node, tương ứng với thế giới (thường là :ref:`CanvasLayer<class_CanvasLayer>`).

.. rst-class:: classref-item-separator

----

.. _class_Control_property_grow_horizontal:

.. rst-class:: classref-property

:ref:`GrowDirection<enum_Control_GrowDirection>` **grow_horizontal** = ``1`` :ref:`🔗<class_Control_property_grow_horizontal>`

.. rst-class:: classref-property-setget

- |void| **set_h_grow_direction**\ (\ value\: :ref:`GrowDirection<enum_Control_GrowDirection>`\ ) - :ref:`GrowDirection<enum_Control_GrowDirection>` **get_h_grow_direction**\ (\ )

Điều khiển hướng trên trục ngang mà control sẽ mở rộng hoặc thu hẹp nếu kích thước ngang của nó thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_grow_vertical:

.. rst-class:: classref-property

:ref:`GrowDirection<enum_Control_GrowDirection>` **grow_vertical** = ``1`` :ref:`🔗<class_Control_property_grow_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_v_grow_direction**\ (\ value\: :ref:`GrowDirection<enum_Control_GrowDirection>`\ ) - :ref:`GrowDirection<enum_Control_GrowDirection>` **get_v_grow_direction**\ (\ )

Điều khiển hướng trên trục dọc mà control sẽ mở rộng hoặc thu hẹp nếu kích thước dọc của nó thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_layout_direction:

.. rst-class:: classref-property

:ref:`LayoutDirection<enum_Control_LayoutDirection>` **layout_direction** = ``0`` :ref:`🔗<class_Control_property_layout_direction>`

.. rst-class:: classref-property-setget

- |void| **set_layout_direction**\ (\ value\: :ref:`LayoutDirection<enum_Control_LayoutDirection>`\ ) - :ref:`LayoutDirection<enum_Control_LayoutDirection>` **get_layout_direction**\ (\ )

Điều khiển hướng bố cục và hướng viết văn bản. Bố cục phải sang trái là cần thiết cho một số ngôn ngữ (ví dụ: tiếng Ả Rập và tiếng Hebrew). Xem thêm :ref:`is_layout_rtl()<class_Control_method_is_layout_rtl>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_localize_numeral_system:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **localize_numeral_system** = ``true`` :ref:`🔗<class_Control_property_localize_numeral_system>`

.. rst-class:: classref-property-setget

- |void| **set_localize_numeral_system**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_localizing_numeral_system**\ (\ )

Nếu ``true``, tự động chuyển đổi số dòng mã, chỉ mục danh sách, các giá trị :ref:`SpinBox<class_SpinBox>` và :ref:`ProgressBar<class_ProgressBar>` từ chữ số Ả Rập phương Tây (0..9) sang hệ chữ số được sử dụng trong locale hiện tại.

\ **Lưu ý:** Các số bên trong văn bản không được tự động chuyển đổi; có thể thực hiện thủ công bằng :ref:`TextServer.format_number()<class_TextServer_method_format_number>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_mouse_behavior_recursive:

.. rst-class:: classref-property

:ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>` **mouse_behavior_recursive** = ``0`` :ref:`🔗<class_Control_property_mouse_behavior_recursive>`

.. rst-class:: classref-property-setget

- |void| **set_mouse_behavior_recursive**\ (\ value\: :ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>`\ ) - :ref:`MouseBehaviorRecursive<enum_Control_MouseBehaviorRecursive>` **get_mouse_behavior_recursive**\ (\ )

Xác định những control nào có thể nhận input chuột cùng với :ref:`mouse_filter<class_Control_property_mouse_filter>`. Xem :ref:`get_mouse_filter_with_override()<class_Control_method_get_mouse_filter_with_override>`. Vì hành vi mặc định là :ref:`MOUSE_BEHAVIOR_INHERITED<class_Control_constant_MOUSE_BEHAVIOR_INHERITED>`, bạn có thể dùng thuộc tính này để ngăn tất cả control con nhận input chuột.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_mouse_default_cursor_shape:

.. rst-class:: classref-property

:ref:`CursorShape<enum_Control_CursorShape>` **mouse_default_cursor_shape** = ``0`` :ref:`🔗<class_Control_property_mouse_default_cursor_shape>`

.. rst-class:: classref-property-setget

- |void| **set_default_cursor_shape**\ (\ value\: :ref:`CursorShape<enum_Control_CursorShape>`\ ) - :ref:`CursorShape<enum_Control_CursorShape>` **get_default_cursor_shape**\ (\ )

Hình dạng con trỏ mặc định cho control này. Hữu ích cho các plugin Godot và những ứng dụng hoặc game sử dụng con trỏ chuột của hệ thống.

\ **Lưu ý:** Trên Linux, hình dạng có thể thay đổi tùy theo theme con trỏ của hệ thống.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_mouse_filter:

.. rst-class:: classref-property

:ref:`MouseFilter<enum_Control_MouseFilter>` **mouse_filter** = ``0`` :ref:`🔗<class_Control_property_mouse_filter>`

.. rst-class:: classref-property-setget

- |void| **set_mouse_filter**\ (\ value\: :ref:`MouseFilter<enum_Control_MouseFilter>`\ ) - :ref:`MouseFilter<enum_Control_MouseFilter>` **get_mouse_filter**\ (\ )

Xác định những control nào có thể nhận các sự kiện input nút chuột thông qua :ref:`_gui_input()<class_Control_private_method__gui_input>` và các signal :ref:`mouse_entered<class_Control_signal_mouse_entered>`, :ref:`mouse_exited<class_Control_signal_mouse_exited>`. Đồng thời xác định cách các sự kiện này được truyền tiếp. Xem các hằng số để biết chức năng của từng giá trị. Dùng :ref:`get_mouse_filter_with_override()<class_Control_method_get_mouse_filter_with_override>` để xác định liệu một control có thể nhận input chuột hay không, vì :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>` cũng ảnh hưởng đến điều này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_mouse_force_pass_scroll_events:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **mouse_force_pass_scroll_events** = ``true`` :ref:`🔗<class_Control_property_mouse_force_pass_scroll_events>`

.. rst-class:: classref-property-setget

- |void| **set_force_pass_scroll_events**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_force_pass_scroll_events**\ (\ )

Khi được bật, các sự kiện con lăn chuột được xử lý bởi :ref:`_gui_input()<class_Control_private_method__gui_input>` sẽ được chuyển đến control cha ngay cả khi :ref:`mouse_filter<class_Control_property_mouse_filter>` được đặt thành :ref:`MOUSE_FILTER_STOP<class_Control_constant_MOUSE_FILTER_STOP>`.

Bạn nên tắt tùy chọn này ở gốc của UI nếu không muốn các sự kiện cuộn được chuyển đến quá trình xử lý :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>`.

\ **Lưu ý:** Vì thuộc tính này mặc định là ``true``, các container có thể cuộn lồng nhau sẽ hoạt động ngay mà không cần cấu hình thêm.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_bottom:

.. rst-class:: classref-property

:ref:`float<class_float>` **offset_bottom** = ``0.0`` :ref:`🔗<class_Control_property_offset_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_offset**\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Khoảng cách giữa cạnh dưới của node và control cha của nó, dựa trên :ref:`anchor_bottom<class_Control_property_anchor_bottom>`.

Các offset thường được điều khiển bởi một hoặc nhiều node :ref:`Container<class_Container>` cha, vì vậy bạn không nên sửa đổi chúng thủ công nếu node của bạn là con trực tiếp của một :ref:`Container<class_Container>`. Các offset sẽ tự động cập nhật khi bạn di chuyển hoặc thay đổi kích thước node.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_left:

.. rst-class:: classref-property

:ref:`float<class_float>` **offset_left** = ``0.0`` :ref:`🔗<class_Control_property_offset_left>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_offset**\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Khoảng cách giữa cạnh trái của node và control cha của nó, dựa trên :ref:`anchor_left<class_Control_property_anchor_left>`.

Các offset thường được điều khiển bởi một hoặc nhiều node :ref:`Container<class_Container>` cha, vì vậy bạn không nên sửa đổi chúng thủ công nếu node của bạn là con trực tiếp của một :ref:`Container<class_Container>`. Các offset sẽ tự động cập nhật khi bạn di chuyển hoặc thay đổi kích thước node.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_right:

.. rst-class:: classref-property

:ref:`float<class_float>` **offset_right** = ``0.0`` :ref:`🔗<class_Control_property_offset_right>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_offset**\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Khoảng cách giữa cạnh phải của node và control cha của nó, dựa trên :ref:`anchor_right<class_Control_property_anchor_right>`.

Các offset thường được điều khiển bởi một hoặc nhiều node :ref:`Container<class_Container>` cha, vì vậy bạn không nên sửa đổi chúng thủ công nếu node của bạn là con trực tiếp của một :ref:`Container<class_Container>`. Các offset sẽ tự động cập nhật khi bạn di chuyển hoặc thay đổi kích thước node.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_top:

.. rst-class:: classref-property

:ref:`float<class_float>` **offset_top** = ``0.0`` :ref:`🔗<class_Control_property_offset_top>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_offset**\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Khoảng cách giữa cạnh trên của node và control cha của nó, dựa trên :ref:`anchor_top<class_Control_property_anchor_top>`.

Các offset thường được điều khiển bởi một hoặc nhiều node :ref:`Container<class_Container>` cha, vì vậy bạn không nên sửa đổi chúng thủ công nếu node của bạn là con trực tiếp của một :ref:`Container<class_Container>`. Các offset sẽ tự động cập nhật khi bạn di chuyển hoặc thay đổi kích thước node.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **offset_transform_enabled** = ``false`` :ref:`🔗<class_Control_property_offset_transform_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_offset_transform_enabled**\ (\ )

Nếu ``true``, áp dụng tất cả thuộc tính biến đổi offset. Nếu không, không có biến đổi offset nào được áp dụng và các thuộc tính này không có tác dụng.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_pivot:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset_transform_pivot** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_offset_transform_pivot>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_pivot**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset_transform_pivot**\ (\ )

Pivot được :ref:`offset_transform_rotation<class_Control_property_offset_transform_rotation>` và :ref:`offset_transform_scale<class_Control_property_offset_transform_scale>` sử dụng, tính theo đơn vị tuyệt đối.

Vị trí pivot cuối cùng là giá trị kết hợp của thuộc tính này và :ref:`offset_transform_pivot_ratio<class_Control_property_offset_transform_pivot_ratio>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_pivot_ratio:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset_transform_pivot_ratio** = ``Vector2(0.5, 0.5)`` :ref:`🔗<class_Control_property_offset_transform_pivot_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_pivot_ratio**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset_transform_pivot_ratio**\ (\ )

Giống :ref:`offset_transform_pivot<class_Control_property_offset_transform_pivot>` nhưng được biểu diễn theo các đơn vị tương đối với **Control** :ref:`size<class_Control_property_size>`, trong đó ``Vector2(0, 0)`` là góc trên bên trái của control này và ``Vector2(1, 1)`` là góc dưới bên phải của nó.

Vị trí pivot cuối cùng là giá trị kết hợp của thuộc tính này và :ref:`offset_transform_pivot<class_Control_property_offset_transform_pivot>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset_transform_position** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_offset_transform_position>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset_transform_position**\ (\ )

Offset vị trí theo các đơn vị tuyệt đối. Offset cuối cùng là giá trị kết hợp của thuộc tính này và :ref:`offset_transform_position_ratio<class_Control_property_offset_transform_position_ratio>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_position_ratio:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset_transform_position_ratio** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_offset_transform_position_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_position_ratio**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset_transform_position_ratio**\ (\ )

Giống :ref:`offset_transform_position<class_Control_property_offset_transform_position>` nhưng được biểu diễn theo các đơn vị tương đối với **Control** :ref:`size<class_Control_property_size>`, trong đó ``Vector2(0, 0)`` là góc trên bên trái của control này và ``Vector2(1, 1)`` là góc dưới bên phải của nó.

Offset cuối cùng là giá trị kết hợp của thuộc tính này và :ref:`offset_transform_position<class_Control_property_offset_transform_position>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **offset_transform_rotation** = ``0.0`` :ref:`🔗<class_Control_property_offset_transform_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_offset_transform_rotation**\ (\ )

Offset xoay. Pivot xoay được xác định bởi :ref:`offset_transform_pivot<class_Control_property_offset_transform_pivot>` và :ref:`offset_transform_pivot_ratio<class_Control_property_offset_transform_pivot_ratio>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset_transform_scale** = ``Vector2(1, 1)`` :ref:`🔗<class_Control_property_offset_transform_scale>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset_transform_scale**\ (\ )

Offset tỷ lệ. Pivot tỷ lệ được xác định bởi :ref:`offset_transform_pivot<class_Control_property_offset_transform_pivot>` và :ref:`offset_transform_pivot_ratio<class_Control_property_offset_transform_pivot_ratio>`.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_offset_transform_visual_only:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **offset_transform_visual_only** = ``true`` :ref:`🔗<class_Control_property_offset_transform_visual_only>`

.. rst-class:: classref-property-setget

- |void| **set_offset_transform_visual_only**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_offset_transform_visual_only**\ (\ )

Nếu ``true``, các biến đổi offset chỉ được áp dụng về mặt hiển thị và không ảnh hưởng đến input. Nói cách khác, Control này vẫn nhận các sự kiện input tại vị trí ban đầu trước khi áp dụng biến đổi offset.

Nếu ``false``, toàn bộ biến đổi của Control này sẽ bị ảnh hưởng và các sự kiện input sẽ được ghi nhận tại vị trí hiển thị của Control.

Không có tác dụng trừ khi :ref:`offset_transform_enabled<class_Control_property_offset_transform_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_pivot_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **pivot_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_pivot_offset>`

.. rst-class:: classref-property-setget

- |void| **set_pivot_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_pivot_offset**\ (\ )

Theo mặc định, pivot của node là góc trên bên trái của nó. Khi bạn thay đổi :ref:`rotation<class_Control_property_rotation>` hoặc :ref:`scale<class_Control_property_scale>` của node, node sẽ xoay hoặc thay đổi tỷ lệ quanh pivot này.

Offset thực tế là giá trị kết hợp của thuộc tính này và :ref:`pivot_offset_ratio<class_Control_property_pivot_offset_ratio>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_pivot_offset_ratio:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **pivot_offset_ratio** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_pivot_offset_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_pivot_offset_ratio**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_pivot_offset_ratio**\ (\ )

Giống :ref:`pivot_offset<class_Control_property_pivot_offset>`, nhưng được biểu diễn dưới dạng vector đồng nhất, trong đó ``Vector2(0, 0)`` là góc trên bên trái của control này và ``Vector2(1, 1)`` là góc dưới bên phải của nó. Đặt thuộc tính này thành ``Vector2(0.5, 0.5)`` để pivot quanh tâm của control này.

Offset thực tế là giá trị kết hợp của thuộc tính này và :ref:`pivot_offset<class_Control_property_pivot_offset>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_position>`

.. rst-class:: classref-property-setget

- :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Vị trí của node, tương đối với node chứa nó. Vị trí này tương ứng với góc trên bên trái của hình chữ nhật. Thuộc tính này không bị ảnh hưởng bởi :ref:`pivot_offset<class_Control_property_pivot_offset>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_propagate_maximum_size:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **propagate_maximum_size** = ``false`` :ref:`🔗<class_Control_property_propagate_maximum_size>`

.. rst-class:: classref-property-setget

- |void| **set_propagate_maximum_size**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_propagating_maximum_size**\ (\ )

Nếu ``true``, các node con của Control này sẽ sử dụng giá trị do :ref:`get_combined_maximum_size()<class_Control_method_get_combined_maximum_size>` trả về trong phép tính kích thước của chính chúng.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation** = ``0.0`` :ref:`🔗<class_Control_property_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation**\ (\ )

Góc xoay của node quanh pivot của nó, tính bằng radian. Xem :ref:`pivot_offset<class_Control_property_pivot_offset>` để thay đổi vị trí của pivot.

\ **Lưu ý:** Thuộc tính này được chỉnh sửa trong inspector theo đơn vị độ. Nếu muốn sử dụng độ trong script, hãy dùng :ref:`rotation_degrees<class_Control_property_rotation_degrees>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_rotation_degrees:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation_degrees** :ref:`🔗<class_Control_property_rotation_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_degrees**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation_degrees**\ (\ )

Thuộc tính trợ giúp để truy cập :ref:`rotation<class_Control_property_rotation>` theo đơn vị độ thay vì radian.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scale** = ``Vector2(1, 1)`` :ref:`🔗<class_Control_property_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scale**\ (\ )

Scale của node, tương đối so với :ref:`size<class_Control_property_size>` của nó. Thay đổi thuộc tính này để scale node quanh :ref:`pivot_offset<class_Control_property_pivot_offset>` của nó. Tooltip của Control cũng sẽ được scale theo giá trị này.

\ **Lưu ý:** Thuộc tính này chủ yếu nhằm phục vụ mục đích animation. Để hỗ trợ nhiều độ phân giải trong project, hãy sử dụng viewport stretch mode thích hợp như mô tả trong :doc:`documentation <../tutorials/rendering/multiple_resolutions>` thay vì scale từng Control riêng lẻ.

\ **Lưu ý:** :ref:`FontFile.oversampling<class_FontFile_property_oversampling>` *không* tính đến **Control** :ref:`scale<class_Control_property_scale>`. Điều này có nghĩa là khi scale lên/xuống, bitmap font và dynamic font được rasterize (không phải MSDF) sẽ bị mờ hoặc vỡ pixel. Để đảm bảo văn bản luôn sắc nét bất kể scale, bạn có thể bật MSDF font rendering bằng cách bật :ref:`ProjectSettings.gui/theme/default_font_multichannel_signed_distance_field<class_ProjectSettings_property_gui/theme/default_font_multichannel_signed_distance_field>` (chỉ áp dụng cho font mặc định của project), hoặc bật **Multichannel Signed Distance Field** trong các tùy chọn import của DynamicFont cho font tùy chỉnh. Với system font, có thể bật :ref:`SystemFont.multichannel_signed_distance_field<class_SystemFont_property_multichannel_signed_distance_field>` trong inspector.

\ **Lưu ý:** Nếu node Control là con của node :ref:`Container<class_Container>`, scale sẽ được đặt lại thành ``Vector2(1, 1)`` khi scene được khởi tạo. Để đặt scale của Control khi nó được khởi tạo, hãy chờ một frame bằng cách sử dụng ``await get_tree().process_frame``, sau đó đặt thuộc tính :ref:`scale<class_Control_property_scale>` của nó.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_shortcut_context:

.. rst-class:: classref-property

:ref:`Node<class_Node>` **shortcut_context** :ref:`🔗<class_Control_property_shortcut_context>`

.. rst-class:: classref-property-setget

- |void| **set_shortcut_context**\ (\ value\: :ref:`Node<class_Node>`\ ) - :ref:`Node<class_Node>` **get_shortcut_context**\ (\ )

:ref:`Node<class_Node>` phải là parent của **Control** đang được focus để shortcut được kích hoạt. Nếu ``null``, shortcut có thể được kích hoạt khi bất kỳ control nào được focus (global shortcut). Điều này cho phép chỉ chấp nhận shortcut khi người dùng đang focus một khu vực nhất định của GUI.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **size** = ``Vector2(0, 0)`` :ref:`🔗<class_Control_property_size>`

.. rst-class:: classref-property-setget

- :ref:`Vector2<class_Vector2>` **get_size**\ (\ )

Kích thước của hình chữ nhật bao quanh node, trong hệ tọa độ của node. Các node :ref:`Container<class_Container>` tự động cập nhật thuộc tính này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_size_flags_horizontal:

.. rst-class:: classref-property

|bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\] **size_flags_horizontal** = ``1`` :ref:`🔗<class_Control_property_size_flags_horizontal>`

.. rst-class:: classref-property-setget

- |void| **set_h_size_flags**\ (\ value\: |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\]\ ) - |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\] **get_h_size_flags**\ (\ )

Cho các node :ref:`Container<class_Container>` parent biết cách thay đổi kích thước và đặt node trên trục X. Sử dụng kết hợp các hằng số :ref:`SizeFlags<enum_Control_SizeFlags>` để thay đổi các flag. Xem các hằng số để biết chức năng của từng hằng số.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_size_flags_stretch_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **size_flags_stretch_ratio** = ``1.0`` :ref:`🔗<class_Control_property_size_flags_stretch_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_stretch_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_stretch_ratio**\ (\ )

Nếu node và ít nhất một node lân cận của nó sử dụng size flag :ref:`SIZE_EXPAND<class_Control_constant_SIZE_EXPAND>`, :ref:`Container<class_Container>` parent sẽ cho node chiếm nhiều hoặc ít không gian hơn tùy theo thuộc tính này. Nếu node này có stretch ratio là 2 và node lân cận có ratio là 1, node này sẽ chiếm hai phần ba không gian khả dụng.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_size_flags_vertical:

.. rst-class:: classref-property

|bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\] **size_flags_vertical** = ``1`` :ref:`🔗<class_Control_property_size_flags_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_v_size_flags**\ (\ value\: |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\]\ ) - |bitfield|\[:ref:`SizeFlags<enum_Control_SizeFlags>`\] **get_v_size_flags**\ (\ )

Cho các node :ref:`Container<class_Container>` parent biết cách thay đổi kích thước và đặt node trên trục Y. Sử dụng kết hợp các hằng số :ref:`SizeFlags<enum_Control_SizeFlags>` để thay đổi các flag. Xem các hằng số để biết chức năng của từng hằng số.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_theme:

.. rst-class:: classref-property

:ref:`Theme<class_Theme>` **theme** :ref:`🔗<class_Control_property_theme>`

.. rst-class:: classref-property-setget

- |void| **set_theme**\ (\ value\: :ref:`Theme<class_Theme>`\ ) - :ref:`Theme<class_Theme>` **get_theme**\ (\ )

Resource :ref:`Theme<class_Theme>` mà node này cùng tất cả các node con **Control** và :ref:`Window<class_Window>` sử dụng. Nếu một node con có resource :ref:`Theme<class_Theme>` riêng được thiết lập, các theme item sẽ được hợp nhất, trong đó các định nghĩa của node con có độ ưu tiên cao hơn.

\ **Lưu ý:** Các style :ref:`Window<class_Window>` sẽ không có hiệu lực trừ khi cửa sổ được embed.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_theme_type_variation:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **theme_type_variation** = ``&""`` :ref:`🔗<class_Control_property_theme_type_variation>`

.. rst-class:: classref-property-setget

- |void| **set_theme_type_variation**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_theme_type_variation**\ (\ )

Tên của một theme type variation được **Control** này sử dụng để tra cứu các theme item của chính nó. Khi để trống, tên class của node được sử dụng (ví dụ: ``Button`` cho control :ref:`Button<class_Button>`), cùng với tên class của tất cả class parent (theo thứ tự kế thừa).

Khi được thiết lập, thuộc tính này ưu tiên cao nhất cho type có tên được chỉ định. Type này có thể lần lượt mở rộng một type khác, tạo thành một dependency chain. Xem :ref:`Theme.set_type_variation()<class_Theme_method_set_type_variation>`. Nếu không tìm thấy theme item bằng type này hoặc các base type của nó, việc tra cứu sẽ chuyển sang tên class.

\ **Lưu ý:** Để tra cứu các item riêng của **Control**, hãy sử dụng nhiều phương thức ``get_theme_*`` mà không chỉ định ``theme_type``.

\ **Lưu ý:** Theme item được tìm kiếm theo thứ tự của tree, từ branch đến root, trong đó mỗi node **Control** được kiểm tra thuộc tính :ref:`theme<class_Control_property_theme>` của nó. Kết quả khớp sớm nhất với bất kỳ tên type/class nào sẽ được trả về. Theme cấp project và Theme mặc định được kiểm tra sau cùng.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_tooltip_auto_translate_mode:

.. rst-class:: classref-property

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **tooltip_auto_translate_mode** = ``0`` :ref:`🔗<class_Control_property_tooltip_auto_translate_mode>`

.. rst-class:: classref-property-setget

- |void| **set_tooltip_auto_translate_mode**\ (\ value\: :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>`\ ) - :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **get_tooltip_auto_translate_mode**\ (\ )

Xác định liệu văn bản tooltip có tự động chuyển thành phiên bản đã dịch tùy theo locale hiện tại hay không. Khi được đặt thành :ref:`Node.AUTO_TRANSLATE_MODE_INHERIT<class_Node_constant_AUTO_TRANSLATE_MODE_INHERIT>`, thuộc tính này sử dụng cùng auto translate mode với control này.

\ **Lưu ý:** Tooltip được tùy chỉnh bằng :ref:`_make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>` không tự động sử dụng auto translate mode này.

.. rst-class:: classref-item-separator

----

.. _class_Control_property_tooltip_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **tooltip_text** = ``""`` :ref:`🔗<class_Control_property_tooltip_text>`

.. rst-class:: classref-property-setget

- |void| **set_tooltip_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_tooltip_text**\ (\ )

Văn bản tooltip mặc định. Tooltip xuất hiện khi con trỏ chuột của người dùng đứng yên trên control này trong vài giây, với điều kiện thuộc tính :ref:`mouse_filter<class_Control_property_mouse_filter>` không phải là :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>`. Có thể thay đổi thời gian cần để tooltip xuất hiện bằng setting :ref:`ProjectSettings.gui/timers/tooltip_delay_sec<class_ProjectSettings_property_gui/timers/tooltip_delay_sec>`.

Chuỗi này là giá trị trả về mặc định của :ref:`get_tooltip()<class_Control_method_get_tooltip>`. Override :ref:`_get_tooltip()<class_Control_private_method__get_tooltip>` để tạo văn bản tooltip một cách động. Override :ref:`_make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>` để tùy chỉnh giao diện và hành vi của tooltip.

Popup tooltip sẽ sử dụng implementation mặc định hoặc implementation tùy chỉnh mà bạn có thể cung cấp bằng cách override :ref:`_make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>`. Tooltip mặc định bao gồm một :ref:`PopupPanel<class_PopupPanel>` và :ref:`Label<class_Label>`, với các theme property có thể được tùy chỉnh bằng các phương thức :ref:`Theme<class_Theme>` cùng với ``"TooltipPanel"`` và ``"TooltipLabel"`` tương ứng. Ví dụ:


.. tabs::

 .. code-tab:: gdscript

    var style_box = StyleBoxFlat.new()
    style_box.set_bg_color(Color(1, 1, 0))
    style_box.set_border_width_all(2)
    # Ở đây, chúng ta giả định rằng thuộc tính `theme` đã được gán một Theme tùy chỉnh từ trước.
    theme.set_stylebox("panel", "TooltipPanel", style_box)
    theme.set_color("font_color", "TooltipLabel", Color(0, 1, 1))

 .. code-tab:: csharp

    var styleBox = new StyleBoxFlat();
    styleBox.SetBgColor(new Color(1, 1, 0));
    styleBox.SetBorderWidthAll(2);
    // Ở đây, chúng ta giả định rằng thuộc tính `Theme` đã được gán một Theme tùy chỉnh từ trước.
    Theme.SetStyleBox("panel", "TooltipPanel", styleBox);
    Theme.SetColor("font_color", "TooltipLabel", new Color(0, 1, 1));



.. rst-class:: classref-item-separator

----

.. _class_Control_property_translation_context:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **translation_context** = ``&""`` :ref:`🔗<class_Control_property_translation_context>`

.. rst-class:: classref-property-setget

- |void| **set_translation_context**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_translation_context**\ (\ )

Translation context được sử dụng khi dịch văn bản hiển thị của control này, nếu control có văn bản đó. Context này cũng được sử dụng khi tạo translation template.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Control_private_method__accessibility_get_contextual_info:

.. rst-class:: classref-method

:ref:`String<class_String>` **_accessibility_get_contextual_info**\ (\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__accessibility_get_contextual_info>`

Trả về mô tả về các keyboard shortcut và trợ giúp theo ngữ cảnh khác cho control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__can_drop_data:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_drop_data**\ (\ at_position\: :ref:`Vector2<class_Vector2>`, data\: :ref:`Variant<class_Variant>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__can_drop_data>`

Godot gọi phương thức này để kiểm tra xem ``data`` từ :ref:`_get_drag_data()<class_Control_private_method__get_drag_data>` của một control có thể được thả tại ``at_position`` hay không. ``at_position`` là cục bộ đối với control này.

Phương thức này chỉ nên được sử dụng để kiểm tra data. Hãy xử lý data trong :ref:`_drop_data()<class_Control_private_method__drop_data>`.

\ **Lưu ý:** Nếu thao tác kéo được bắt đầu bằng phím tắt hoặc :ref:`accessibility_drag()<class_Control_method_accessibility_drag>`, ``at_position`` được đặt thành :ref:`Vector2.INF<class_Vector2_constant_INF>`, và vị trí mục/văn bản hiện được chọn sẽ được dùng làm vị trí thả.


.. tabs::

 .. code-tab:: gdscript

    func _can_drop_data(position, data):
        # Kiểm tra vị trí nếu điều đó phù hợp với bạn
        # Nếu không, chỉ cần kiểm tra dữ liệu
        return typeof(data) == TYPE_DICTIONARY and data.has("expected")

 .. code-tab:: csharp

    public override bool _CanDropData(Vector2 atPosition, Variant data)
    {
        // Kiểm tra vị trí nếu điều đó phù hợp với bạn
        // Nếu không, chỉ cần kiểm tra dữ liệu
        return data.VariantType == Variant.Type.Dictionary && data.AsGodotDictionary().ContainsKey("expected");
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__drop_data:

.. rst-class:: classref-method

|void| **_drop_data**\ (\ at_position\: :ref:`Vector2<class_Vector2>`, data\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_Control_private_method__drop_data>`

Godot gọi phương thức này để truyền ``data`` từ kết quả :ref:`_get_drag_data()<class_Control_private_method__get_drag_data>` của một control cho bạn. Trước tiên, Godot gọi :ref:`_can_drop_data()<class_Control_private_method__can_drop_data>` để kiểm tra xem ``data`` có được phép thả tại ``at_position`` hay không, trong đó ``at_position`` là cục bộ đối với control này.

\ **Lưu ý:** Nếu thao tác kéo được bắt đầu bằng phím tắt hoặc :ref:`accessibility_drag()<class_Control_method_accessibility_drag>`, ``at_position`` được đặt thành :ref:`Vector2.INF<class_Vector2_constant_INF>`, và vị trí mục/văn bản hiện được chọn sẽ được dùng làm vị trí thả.


.. tabs::

 .. code-tab:: gdscript

    func _can_drop_data(position, data):
        return typeof(data) == TYPE_DICTIONARY and data.has("color")

    func _drop_data(position, data):
        var color = data["color"]

 .. code-tab:: csharp

    public override bool _CanDropData(Vector2 atPosition, Variant data)
    {
        return data.VariantType == Variant.Type.Dictionary && data.AsGodotDictionary().ContainsKey("color");
    }

    public override void _DropData(Vector2 atPosition, Variant data)
    {
        Color color = data.AsGodotDictionary()["color"].AsColor();
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_accessibility_container_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_accessibility_container_name**\ (\ node\: :ref:`Node<class_Node>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_accessibility_container_name>`

Ghi đè phương thức này để trả về mô tả mà con người có thể đọc được về vị trí của node con ``node`` trong container tùy chỉnh, được thêm vào :ref:`accessibility_name<class_Control_property_accessibility_name>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_cursor_shape:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_cursor_shape**\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_cursor_shape>`

Phương thức virtual do người dùng triển khai. Trả về hình dạng con trỏ tại vị trí ``at_position`` trong tọa độ cục bộ của control, thường được sử dụng khi di con trỏ qua control này. Xem :ref:`get_cursor_shape()<class_Control_method_get_cursor_shape>`.

Nếu không được ghi đè, mặc định là :ref:`mouse_default_cursor_shape<class_Control_property_mouse_default_cursor_shape>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_drag_data:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_drag_data**\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| :ref:`🔗<class_Control_private_method__get_drag_data>`

Godot gọi phương thức này để lấy dữ liệu có thể được kéo và thả lên các control đang chờ dữ liệu thả. Trả về ``null`` nếu không có dữ liệu để kéo. Các control muốn nhận dữ liệu thả phải triển khai :ref:`_can_drop_data()<class_Control_private_method__can_drop_data>` và :ref:`_drop_data()<class_Control_private_method__drop_data>`. ``at_position`` là cục bộ đối với control này. Có thể buộc thao tác kéo bằng :ref:`force_drag()<class_Control_method_force_drag>`.

Có thể thiết lập bản xem trước đi theo chuột và đại diện cho dữ liệu bằng :ref:`set_drag_preview()<class_Control_method_set_drag_preview>`. Thời điểm thích hợp để thiết lập bản xem trước là trong phương thức này.

\ **Lưu ý:** Nếu thao tác kéo được bắt đầu bằng phím tắt hoặc :ref:`accessibility_drag()<class_Control_method_accessibility_drag>`, ``at_position`` được đặt thành :ref:`Vector2.INF<class_Vector2_constant_INF>`, và vị trí mục/văn bản hiện được chọn sẽ được dùng làm vị trí kéo.


.. tabs::

 .. code-tab:: gdscript

    func _get_drag_data(position):
        var mydata = make_data() # Đây là phương thức tùy chỉnh của bạn dùng để tạo dữ liệu kéo.
        set_drag_preview(make_preview(mydata)) # Đây là phương thức tùy chỉnh của bạn dùng để tạo bản xem trước của dữ liệu kéo.
        return mydata

 .. code-tab:: csharp

    public override Variant _GetDragData(Vector2 atPosition)
    {
        var myData = MakeData(); // Đây là phương thức tùy chỉnh của bạn dùng để tạo dữ liệu kéo.
        SetDragPreview(MakePreview(myData)); // Đây là phương thức tùy chỉnh của bạn dùng để tạo bản xem trước của dữ liệu kéo.
        return myData;
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_maximum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **_get_maximum_size**\ (\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_maximum_size>`

Phương thức virtual do người dùng triển khai. Trả về kích thước tối đa cho control này. Đây là lựa chọn thay thế cho :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` để điều khiển kích thước tối đa bằng code. Kích thước tối đa thực tế sẽ là giá trị lớn hơn của hai giá trị này (riêng biệt trên từng trục).

Nếu không được ghi đè, mặc định là :ref:`Vector2.ZERO<class_Vector2_constant_ZERO>`.

\ **Lưu ý:** Phương thức này sẽ không được gọi khi script được gắn vào một node **Control** đã ghi đè kích thước tối đa của nó (ví dụ: :ref:`ScrollContainer<class_ScrollContainer>`).

\ **Lưu ý:** Khuyến nghị sử dụng :ref:`get_bound_minimum_size()<class_Control_method_get_bound_minimum_size>` thay vì :ref:`get_combined_minimum_size()<class_Control_method_get_combined_minimum_size>` khi triển khai phương thức này, vì cách đầu tiên tôn trọng các giới hạn kích thước tối đa khi tính kích thước tối thiểu, còn cách sau thì không.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_minimum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **_get_minimum_size**\ (\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_minimum_size>`

Phương thức virtual do người dùng triển khai. Trả về kích thước tối thiểu cho control này. Đây là lựa chọn thay thế cho :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` để điều khiển kích thước tối thiểu bằng code. Kích thước tối thiểu thực tế sẽ là giá trị lớn hơn của hai giá trị này (riêng biệt trên từng trục).

Nếu không được ghi đè, mặc định là :ref:`Vector2.ZERO<class_Vector2_constant_ZERO>`.

\ **Lưu ý:** Phương thức này sẽ không được gọi khi script được gắn vào một node **Control** đã ghi đè kích thước tối thiểu của nó (ví dụ: :ref:`Label<class_Label>`, :ref:`Button<class_Button>`, :ref:`PanelContainer<class_PanelContainer>` v.v.). Phương thức này chỉ có thể được sử dụng với hầu hết các node GUI cơ bản, như **Control**, :ref:`Container<class_Container>`, :ref:`Panel<class_Panel>` v.v.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_tooltip:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_tooltip**\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_tooltip>`

Phương thức virtual do người dùng triển khai. Trả về văn bản tooltip tại vị trí ``at_position`` trong tọa độ cục bộ của control, thường xuất hiện khi con trỏ dừng trên control này. Xem :ref:`get_tooltip()<class_Control_method_get_tooltip>`.

\ **Lưu ý:** Nếu phương thức này trả về một :ref:`String<class_String>` rỗng và :ref:`_make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>` không được ghi đè, tooltip sẽ không được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__get_tooltip_auto_translate_mode_at:

.. rst-class:: classref-method

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **_get_tooltip_auto_translate_mode_at**\ (\ at_position\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__get_tooltip_auto_translate_mode_at>`

Trả về chế độ tự động dịch tại ``at_position`` đã cho. Nếu không được triển khai, thuộc tính :ref:`tooltip_auto_translate_mode<class_Control_property_tooltip_auto_translate_mode>` sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__gui_input:

.. rst-class:: classref-method

|void| **_gui_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual| :ref:`🔗<class_Control_private_method__gui_input>`

Phương thức virtual do người dùng triển khai. Ghi đè phương thức này để xử lý và chấp nhận các input trên các phần tử UI. Xem thêm :ref:`accept_event()<class_Control_method_accept_event>`.

\ **Ví dụ:** Nhấp vào control để in một thông báo:


.. tabs::

 .. code-tab:: gdscript

    func _gui_input(event):
        if event is InputEventMouseButton:
            if event.button_index == MOUSE_BUTTON_LEFT and event.pressed:
                print("I've been clicked D:")

 .. code-tab:: csharp

    public override void _GuiInput(InputEvent @event)
    {
        if (@event is InputEventMouseButton mb)
        {
            if (mb.ButtonIndex == MouseButton.Left && mb.Pressed)
            {
                GD.Print("I've been clicked D:");
            }
        }
    }



Nếu ``event`` kế thừa :ref:`InputEventMouse<class_InputEventMouse>`, phương thức này sẽ **không** được gọi khi:

- :ref:`mouse_filter<class_Control_property_mouse_filter>` của control được đặt thành :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>`;

- control bị một control khác ở phía trên che khuất và control đó không có :ref:`mouse_filter<class_Control_property_mouse_filter>` được đặt thành :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>`;

- node cha của control có :ref:`mouse_filter<class_Control_property_mouse_filter>` được đặt thành :ref:`MOUSE_FILTER_STOP<class_Control_constant_MOUSE_FILTER_STOP>` hoặc đã chấp nhận event;

- node cha của control đã bật :ref:`clip_contents<class_Control_property_clip_contents>` và vị trí của ``event`` nằm ngoài hình chữ nhật của node cha;

- vị trí của ``event`` nằm ngoài control (xem :ref:`_has_point()<class_Control_private_method__has_point>`).

\ **Lưu ý:** Vị trí của ``event`` là tương đối so với gốc của control này.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__has_point:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_has_point**\ (\ point\: :ref:`Vector2<class_Vector2>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__has_point>`

Phương thức virtual do người dùng triển khai. Trả về việc ``point`` đã cho có nằm bên trong control này hay không.

Nếu không được ghi đè, hành vi mặc định là kiểm tra xem point có nằm trong Rect của control hay không.

\ **Lưu ý:** Nếu bạn muốn kiểm tra xem một point có nằm bên trong control hay không, bạn có thể sử dụng ``Rect2(Vector2.ZERO, size).has_point(point)``.

.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__make_custom_tooltip:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **_make_custom_tooltip**\ (\ for_text\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__make_custom_tooltip>`

Phương thức virtual do người dùng triển khai. Trả về một node **Control** sẽ được dùng làm tooltip thay cho tooltip mặc định. ``for_text`` là giá trị trả về của :ref:`get_tooltip()<class_Control_method_get_tooltip>`.

Node được trả về phải có kiểu **Control** hoặc dẫn xuất từ Control. Node này có thể có các node con thuộc bất kỳ kiểu nào. Node sẽ được giải phóng khi tooltip biến mất, vì vậy hãy luôn cung cấp một instance mới (nếu bạn muốn sử dụng một node có sẵn trong scene tree, bạn có thể nhân bản node đó và truyền instance đã nhân bản). Khi trả về ``null`` hoặc một node không phải Control, tooltip mặc định sẽ được sử dụng thay thế.

Node được trả về sẽ được thêm làm node con của một :ref:`PopupPanel<class_PopupPanel>`, vì vậy bạn chỉ nên cung cấp nội dung của panel đó. :ref:`PopupPanel<class_PopupPanel>` có thể được áp dụng theme bằng :ref:`Theme.set_stylebox()<class_Theme_method_set_stylebox>` cho kiểu ``"TooltipPanel"`` (xem :ref:`tooltip_text<class_Control_property_tooltip_text>` để biết ví dụ).

\ **Lưu ý:** Tooltip được thu nhỏ về kích thước tối thiểu. Nếu muốn đảm bảo tooltip hiển thị đầy đủ, bạn có thể cần đặt :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` của nó thành một giá trị khác không.

\ **Lưu ý:** Node (và mọi node con liên quan) phải có :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` được đặt thành ``true`` khi được trả về, nếu không viewport khởi tạo node đó sẽ không thể tính toán đáng tin cậy kích thước tối thiểu của nó.

\ **Lưu ý:** Nếu được ghi đè, phương thức này vẫn được gọi ngay cả khi :ref:`get_tooltip()<class_Control_method_get_tooltip>` trả về một chuỗi rỗng. Khi điều này xảy ra với tooltip mặc định, tooltip sẽ không được hiển thị. Để sao chép hành vi này, hãy trả về ``null`` trong phương thức này khi ``for_text`` rỗng.

\ **Ví dụ:** Sử dụng một node được tạo làm tooltip:


.. tabs::

 .. code-tab:: gdscript

    func _make_custom_tooltip(for_text):
        var label = Label.new()
        label.text = for_text
        return label

 .. code-tab:: csharp

    public override Control _MakeCustomTooltip(string forText)
    {
        var label = new Label();
        label.Text = forText;
        return label;
    }



\ **Ví dụ:** Sử dụng một scene instance làm tooltip:


.. tabs::

 .. code-tab:: gdscript

    func _make_custom_tooltip(for_text):
        var tooltip = preload("res://some_tooltip_scene.tscn").instantiate()
        tooltip.get_node("Label").text = for_text
        return tooltip

 .. code-tab:: csharp

    public override Control _MakeCustomTooltip(string forText)
    {
        Node tooltip = ResourceLoader.Load<PackedScene>("res://some_tooltip_scene.tscn").Instantiate();
        tooltip.GetNode<Label>("Label").Text = forText;
        return tooltip;
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_private_method__structured_text_parser:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **_structured_text_parser**\ (\ args\: :ref:`Array<class_Array>`, text\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_Control_private_method__structured_text_parser>`

Hàm ghi đè algorithm BiDi do người dùng định nghĩa.

Trả về một :ref:`Array<class_Array>` gồm các phạm vi văn bản :ref:`Vector3i<class_Vector3i>` và hướng cơ sở của văn bản, theo thứ tự từ trái sang phải. Các phạm vi phải bao phủ toàn bộ ``text`` nguồn mà không chồng lấn. Algorithm BiDi sẽ được áp dụng riêng cho từng phạm vi.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_accept_event:

.. rst-class:: classref-method

|void| **accept_event**\ (\ ) :ref:`🔗<class_Control_method_accept_event>`

Đánh dấu một input event là đã được xử lý. Sau khi bạn chấp nhận một input event, nó sẽ ngừng lan truyền, kể cả đến các node đang lắng nghe :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>` hoặc :ref:`Node._unhandled_key_input()<class_Node_private_method__unhandled_key_input>`.

\ **Lưu ý:** Điều này không ảnh hưởng đến các method trong :ref:`Input<class_Input>`, mà chỉ ảnh hưởng đến cách các event được lan truyền.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_accessibility_drag:

.. rst-class:: classref-method

|void| **accessibility_drag**\ (\ ) :ref:`🔗<class_Control_method_accessibility_drag>`

Bắt đầu thao tác kéo-thả mà không sử dụng chuột.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_accessibility_drop:

.. rst-class:: classref-method

|void| **accessibility_drop**\ (\ ) :ref:`🔗<class_Control_method_accessibility_drop>`

Kết thúc thao tác kéo-thả mà không sử dụng chuột.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_color_override:

.. rst-class:: classref-method

|void| **add_theme_color_override**\ (\ name\: :ref:`StringName<class_StringName>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_Control_method_add_theme_color_override>`

Tạo một override cục bộ cho :ref:`Color<class_Color>` của theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_color_override()<class_Control_method_remove_theme_color_override>`.

Xem thêm :ref:`get_theme_color()<class_Control_method_get_theme_color>`.

\ **Ví dụ:** Ghi đè màu của :ref:`Label<class_Label>` và đặt lại sau đó:


.. tabs::

 .. code-tab:: gdscript

    # Với node Label con "MyLabel", ghi đè màu font của nó bằng một giá trị tùy chỉnh.
    $MyLabel.add_theme_color_override("font_color", Color(1, 0.5, 0))
    # Đặt lại màu font của label con.
    $MyLabel.remove_theme_color_override("font_color")
    # Ngoài ra, có thể ghi đè bằng giá trị mặc định từ kiểu Label.
    $MyLabel.add_theme_color_override("font_color", get_theme_color("font_color", "Label"))

 .. code-tab:: csharp

    // Với node Label con "MyLabel", ghi đè màu font của nó bằng một giá trị tùy chỉnh.
    GetNode<Label>("MyLabel").AddThemeColorOverride("font_color", new Color(1, 0.5f, 0));
    // Đặt lại màu font của label con.
    GetNode<Label>("MyLabel").RemoveThemeColorOverride("font_color");
    // Ngoài ra, có thể ghi đè bằng giá trị mặc định từ kiểu Label.
    GetNode<Label>("MyLabel").AddThemeColorOverride("font_color", GetThemeColor("font_color", "Label"));



.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_constant_override:

.. rst-class:: classref-method

|void| **add_theme_constant_override**\ (\ name\: :ref:`StringName<class_StringName>`, constant\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Control_method_add_theme_constant_override>`

Tạo một override cục bộ cho một hằng số theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_constant_override()<class_Control_method_remove_theme_constant_override>`.

Xem thêm :ref:`get_theme_constant()<class_Control_method_get_theme_constant>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_font_override:

.. rst-class:: classref-method

|void| **add_theme_font_override**\ (\ name\: :ref:`StringName<class_StringName>`, font\: :ref:`Font<class_Font>`\ ) :ref:`🔗<class_Control_method_add_theme_font_override>`

Tạo một override cục bộ cho :ref:`Font<class_Font>` của theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_font_override()<class_Control_method_remove_theme_font_override>`.

Xem thêm :ref:`get_theme_font()<class_Control_method_get_theme_font>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_font_size_override:

.. rst-class:: classref-method

|void| **add_theme_font_size_override**\ (\ name\: :ref:`StringName<class_StringName>`, font_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Control_method_add_theme_font_size_override>`

Tạo một override cục bộ cho kích thước font của theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_font_size_override()<class_Control_method_remove_theme_font_size_override>`.

Xem thêm :ref:`get_theme_font_size()<class_Control_method_get_theme_font_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_icon_override:

.. rst-class:: classref-method

|void| **add_theme_icon_override**\ (\ name\: :ref:`StringName<class_StringName>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) :ref:`🔗<class_Control_method_add_theme_icon_override>`

Tạo một override cục bộ cho icon của theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_icon_override()<class_Control_method_remove_theme_icon_override>`.

Xem thêm :ref:`get_theme_icon()<class_Control_method_get_theme_icon>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_add_theme_stylebox_override:

.. rst-class:: classref-method

|void| **add_theme_stylebox_override**\ (\ name\: :ref:`StringName<class_StringName>`, stylebox\: :ref:`StyleBox<class_StyleBox>`\ ) :ref:`🔗<class_Control_method_add_theme_stylebox_override>`

Tạo một override cục bộ cho :ref:`StyleBox<class_StyleBox>` của theme với ``name`` được chỉ định. Các override cục bộ luôn được ưu tiên khi lấy các theme item cho control. Có thể xóa một override bằng :ref:`remove_theme_stylebox_override()<class_Control_method_remove_theme_stylebox_override>`.

Xem thêm :ref:`get_theme_stylebox()<class_Control_method_get_theme_stylebox>`.

\ **Ví dụ:** Sửa đổi một property trong :ref:`StyleBox<class_StyleBox>` bằng cách nhân bản nó:


.. tabs::

 .. code-tab:: gdscript

    # Đoạn code dưới đây giả định node con "MyButton" đã được gán một StyleBoxFlat.
    # Các resource được chia sẻ giữa các instance, vì vậy chúng ta cần nhân bản nó
    # để tránh sửa đổi giao diện của tất cả button khác.
    var new_stylebox_normal = $MyButton.get_theme_stylebox("normal").duplicate()
    new_stylebox_normal.border_width_top = 3
    new_stylebox_normal.border_color = Color(0, 1, 0.5)
    $MyButton.add_theme_stylebox_override("normal", new_stylebox_normal)
    # Xóa stylebox override.
    $MyButton.remove_theme_stylebox_override("normal")

 .. code-tab:: csharp

    // Đoạn code dưới đây giả định node con "MyButton" đã được gán một StyleBoxFlat.
    // Các resource được chia sẻ giữa các instance, vì vậy chúng ta cần nhân bản nó
    // để tránh sửa đổi giao diện của tất cả button khác.
    StyleBoxFlat newStyleboxNormal = GetNode<Button>("MyButton").GetThemeStylebox("normal").Duplicate() as StyleBoxFlat;
    newStyleboxNormal.BorderWidthTop = 3;
    newStyleboxNormal.BorderColor = new Color(0, 1, 0.5f);
    GetNode<Button>("MyButton").AddThemeStyleboxOverride("normal", newStyleboxNormal);
    // Xóa stylebox override.
    GetNode<Button>("MyButton").RemoveThemeStyleboxOverride("normal");



.. rst-class:: classref-item-separator

----

.. _class_Control_method_begin_bulk_theme_override:

.. rst-class:: classref-method

|void| **begin_bulk_theme_override**\ (\ ) :ref:`🔗<class_Control_method_begin_bulk_theme_override>`

Ngăn các method ``*_theme_*_override`` phát ra :ref:`NOTIFICATION_THEME_CHANGED<class_Control_constant_NOTIFICATION_THEME_CHANGED>` cho đến khi :ref:`end_bulk_theme_override()<class_Control_method_end_bulk_theme_override>` được gọi.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_end_bulk_theme_override:

.. rst-class:: classref-method

|void| **end_bulk_theme_override**\ (\ ) :ref:`🔗<class_Control_method_end_bulk_theme_override>`

Kết thúc một lần cập nhật bulk theme override. Xem :ref:`begin_bulk_theme_override()<class_Control_method_begin_bulk_theme_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_find_next_valid_focus:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **find_next_valid_focus**\ (\ ) |const| :ref:`🔗<class_Control_method_find_next_valid_focus>`

Tìm **Control** tiếp theo (ở bên dưới trong cây) có thể nhận focus.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_find_prev_valid_focus:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **find_prev_valid_focus**\ (\ ) |const| :ref:`🔗<class_Control_method_find_prev_valid_focus>`

Tìm **Control** trước đó (ở bên trên trong cây) có thể nhận focus.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_find_valid_focus_neighbor:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **find_valid_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Control_method_find_valid_focus_neighbor>`

Tìm **Control** tiếp theo có thể nhận focus ở :ref:`Side<enum_@GlobalScope_Side>` được chỉ định.

\ **Lưu ý:** Điều này khác với :ref:`get_focus_neighbor()<class_Control_method_get_focus_neighbor>`, vốn trả về path của focus neighbor được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_force_drag:

.. rst-class:: classref-method

|void| **force_drag**\ (\ data\: :ref:`Variant<class_Variant>`, preview\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_Control_method_force_drag>`

Buộc thực hiện thao tác kéo và bỏ qua :ref:`_get_drag_data()<class_Control_private_method__get_drag_data>` và :ref:`set_drag_preview()<class_Control_method_set_drag_preview>` bằng cách truyền ``data`` và ``preview``. Thao tác kéo sẽ bắt đầu ngay cả khi chuột không ở trên hoặc không nhấn trên control này.

Các method :ref:`_can_drop_data()<class_Control_private_method__can_drop_data>` và :ref:`_drop_data()<class_Control_private_method__drop_data>` phải được triển khai trên các control muốn nhận dữ liệu thả.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_anchor:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Control_method_get_anchor>`

Trả về anchor cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Đây là một getter method cho :ref:`anchor_bottom<class_Control_property_anchor_bottom>`, :ref:`anchor_left<class_Control_property_anchor_left>`, :ref:`anchor_right<class_Control_property_anchor_right>` và :ref:`anchor_top<class_Control_property_anchor_top>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_begin:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_begin**\ (\ ) |const| :ref:`🔗<class_Control_method_get_begin>`

Trả về :ref:`offset_left<class_Control_property_offset_left>` và :ref:`offset_top<class_Control_property_offset_top>`. Xem thêm :ref:`position<class_Control_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_bound_minimum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_bound_minimum_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_bound_minimum_size>`

Trả về giá trị giới hạn của :ref:`get_combined_minimum_size()<class_Control_method_get_combined_minimum_size>` theo :ref:`get_combined_maximum_size()<class_Control_method_get_combined_maximum_size>`.

Giá trị này là kích thước tối thiểu thực sự của container, vì kích thước tối đa được ưu tiên hơn kích thước tối thiểu.

Ví dụ: nếu kích thước tối thiểu tổng hợp là (100, 100) và kích thước tối đa tổng hợp là (50, 150), thì kích thước tối thiểu giới hạn sẽ là (50, 100).

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_combined_maximum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_combined_maximum_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_combined_maximum_size>`

Trả về kích thước tối đa tổng hợp từ :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` và :ref:`get_maximum_size()<class_Control_method_get_maximum_size>`, cũng như :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` của node cha nếu node đó là một Control với :ref:`propagate_maximum_size<class_Control_property_propagate_maximum_size>` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_combined_minimum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_combined_minimum_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_combined_minimum_size>`

Trả về kích thước tối thiểu tổng hợp từ :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` và :ref:`get_minimum_size()<class_Control_method_get_minimum_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_combined_pivot_offset:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_combined_pivot_offset**\ (\ ) |const| :ref:`🔗<class_Control_method_get_combined_pivot_offset>`

Trả về giá trị tổng hợp của :ref:`pivot_offset<class_Control_property_pivot_offset>` và :ref:`pivot_offset_ratio<class_Control_property_pivot_offset_ratio>`, tính bằng pixel. Tỷ lệ này được nhân với kích thước của control.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_cursor_shape:

.. rst-class:: classref-method

:ref:`CursorShape<enum_Control_CursorShape>` **get_cursor_shape**\ (\ at_position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const| :ref:`🔗<class_Control_method_get_cursor_shape>`

Trả về hình dạng con trỏ chuột cho control này khi di chuột qua ``at_position`` trong tọa độ cục bộ. Với hầu hết control, giá trị này giống với :ref:`mouse_default_cursor_shape<class_Control_property_mouse_default_cursor_shape>`, nhưng một số control tích hợp triển khai logic phức tạp hơn.

Bạn có thể ghi đè :ref:`_get_cursor_shape()<class_Control_private_method__get_cursor_shape>` để triển khai hành vi tùy chỉnh cho method này.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_end:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_end**\ (\ ) |const| :ref:`🔗<class_Control_method_get_end>`

Trả về :ref:`offset_right<class_Control_property_offset_right>` và :ref:`offset_bottom<class_Control_property_offset_bottom>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_focus_mode_with_override:

.. rst-class:: classref-method

:ref:`FocusMode<enum_Control_FocusMode>` **get_focus_mode_with_override**\ (\ ) |const| :ref:`🔗<class_Control_method_get_focus_mode_with_override>`

Trả về :ref:`focus_mode<class_Control_property_focus_mode>`, nhưng có tính đến :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>`. Nếu :ref:`focus_behavior_recursive<class_Control_property_focus_behavior_recursive>` được đặt thành :ref:`FOCUS_BEHAVIOR_DISABLED<class_Control_constant_FOCUS_BEHAVIOR_DISABLED>`, hoặc được đặt thành :ref:`FOCUS_BEHAVIOR_INHERITED<class_Control_constant_FOCUS_BEHAVIOR_INHERITED>` và ancestor của nó được đặt thành :ref:`FOCUS_BEHAVIOR_DISABLED<class_Control_constant_FOCUS_BEHAVIOR_DISABLED>`, thì method này trả về :ref:`FOCUS_NONE<class_Control_constant_FOCUS_NONE>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_focus_neighbor:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Control_method_get_focus_neighbor>`

Trả về focus neighbor cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Đây là một getter method cho :ref:`focus_neighbor_bottom<class_Control_property_focus_neighbor_bottom>`, :ref:`focus_neighbor_left<class_Control_property_focus_neighbor_left>`, :ref:`focus_neighbor_right<class_Control_property_focus_neighbor_right>` và :ref:`focus_neighbor_top<class_Control_property_focus_neighbor_top>`.

\ **Lưu ý:** Để tìm **Control** tiếp theo trên :ref:`Side<enum_@GlobalScope_Side>` cụ thể, ngay cả khi một nút lân cận chưa được gán, hãy sử dụng :ref:`find_valid_focus_neighbor()<class_Control_method_find_valid_focus_neighbor>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_global_rect:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **get_global_rect**\ (\ ) |const| :ref:`🔗<class_Control_method_get_global_rect>`

Trả về vị trí và kích thước của control tương đối so với canvas chứa nó. Xem :ref:`global_position<class_Control_property_global_position>` và :ref:`size<class_Control_property_size>`.

\ **Lưu ý:** Nếu bản thân node hoặc bất kỳ :ref:`CanvasItem<class_CanvasItem>` cha nào giữa node và canvas có rotation hoặc skew khác mặc định, kích thước thu được có thể không có ý nghĩa.

\ **Lưu ý:** Đặt :ref:`Viewport.gui_snap_controls_to_pixels<class_Viewport_property_gui_snap_controls_to_pixels>` thành ``true`` có thể dẫn đến sai số làm tròn giữa control được hiển thị và :ref:`Rect2<class_Rect2>` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_maximum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_maximum_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_maximum_size>`

Trả về kích thước tối đa của control này. Xem :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_minimum_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_minimum_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_minimum_size>`

Trả về kích thước tối thiểu của control này. Xem :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_mouse_filter_with_override:

.. rst-class:: classref-method

:ref:`MouseFilter<enum_Control_MouseFilter>` **get_mouse_filter_with_override**\ (\ ) |const| :ref:`🔗<class_Control_method_get_mouse_filter_with_override>`

Trả về :ref:`mouse_filter<class_Control_property_mouse_filter>`, nhưng có tính đến :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>`. Nếu :ref:`mouse_behavior_recursive<class_Control_property_mouse_behavior_recursive>` được đặt thành :ref:`MOUSE_BEHAVIOR_DISABLED<class_Control_constant_MOUSE_BEHAVIOR_DISABLED>`, hoặc được đặt thành :ref:`MOUSE_BEHAVIOR_INHERITED<class_Control_constant_MOUSE_BEHAVIOR_INHERITED>` và ancestor của nó được đặt thành :ref:`MOUSE_BEHAVIOR_DISABLED<class_Control_constant_MOUSE_BEHAVIOR_DISABLED>`, thì hàm này trả về :ref:`MOUSE_FILTER_IGNORE<class_Control_constant_MOUSE_FILTER_IGNORE>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_offset:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_offset**\ (\ offset\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Control_method_get_offset>`

Trả về offset cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Đây là phương thức getter cho :ref:`offset_bottom<class_Control_property_offset_bottom>`, :ref:`offset_left<class_Control_property_offset_left>`, :ref:`offset_right<class_Control_property_offset_right>` và :ref:`offset_top<class_Control_property_offset_top>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_parent_area_size:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_parent_area_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_parent_area_size>`

Trả về chiều rộng/chiều cao mà control cha chiếm dụng.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_parent_control:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **get_parent_control**\ (\ ) |const| :ref:`🔗<class_Control_method_get_parent_control>`

Trả về node control cha.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_rect:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **get_rect**\ (\ ) |const| :ref:`🔗<class_Control_method_get_rect>`

Trả về vị trí và kích thước của control trong hệ tọa độ của node chứa nó. Xem :ref:`position<class_Control_property_position>`, :ref:`scale<class_Control_property_scale>` và :ref:`size<class_Control_property_size>`.

\ **Lưu ý:** Nếu :ref:`rotation<class_Control_property_rotation>` không phải rotation mặc định, kích thước thu được sẽ không có ý nghĩa.

\ **Lưu ý:** Đặt :ref:`Viewport.gui_snap_controls_to_pixels<class_Viewport_property_gui_snap_controls_to_pixels>` thành ``true`` có thể dẫn đến sai số làm tròn giữa control được hiển thị và :ref:`Rect2<class_Rect2>` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_screen_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_screen_position**\ (\ ) |const| :ref:`🔗<class_Control_method_get_screen_position>`

Trả về vị trí của **Control** này trong tọa độ màn hình toàn cục (tức là có tính đến vị trí cửa sổ). Chủ yếu hữu ích cho các editor plugin.

Tương đương với ``get_screen_transform().origin`` (xem :ref:`CanvasItem.get_screen_transform()<class_CanvasItem_method_get_screen_transform>`).

\ **Ví dụ:** Hiển thị một popup tại vị trí chuột:

::

    popup_menu.position = get_screen_position() + get_screen_transform().basis_xform(get_local_mouse_position())

    # Đoạn mã trên tương đương với:
    popup_menu.position = get_screen_transform() * get_local_mouse_position()

    popup_menu.reset_size()
    popup_menu.popup()

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_theme_color**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_color>`

Trả về một :ref:`Color<class_Color>` từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục màu với ``name`` và ``theme_type`` được chỉ định. Nếu bỏ qua ``theme_type``, tên class của control hiện tại sẽ được sử dụng làm type, hoặc :ref:`theme_type_variation<class_Control_property_theme_type_variation>` nếu nó được định nghĩa. Nếu type là tên class, các class cha của nó cũng được kiểm tra theo thứ tự kế thừa. Nếu type là một variation, các type cơ sở của nó được kiểm tra theo thứ tự phụ thuộc, sau đó tên class của control và các class cha của nó được kiểm tra.

Đối với control hiện tại, các override cục bộ của nó được xét trước (xem :ref:`add_theme_color_override()<class_Control_method_add_theme_color_override>`), sau đó là :ref:`theme<class_Control_property_theme>` được gán cho nó. Sau control hiện tại, từng control cha và :ref:`theme<class_Control_property_theme>` được gán cho chúng sẽ được xét; các control không được gán :ref:`theme<class_Control_property_theme>` sẽ bị bỏ qua. Nếu không tìm thấy :ref:`Theme<class_Theme>` khớp nào trong cây, :ref:`Theme<class_Theme>` tùy chỉnh của project (xem :ref:`ProjectSettings.gui/theme/custom<class_ProjectSettings_property_gui/theme/custom>`) và :ref:`Theme<class_Theme>` mặc định sẽ được sử dụng (xem :ref:`ThemeDB<class_ThemeDB>`).


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        # Lấy màu font được định nghĩa cho class của Control hiện tại, nếu tồn tại.
        modulate = get_theme_color("font_color")
        # Lấy màu font được định nghĩa cho class Button.
        modulate = get_theme_color("font_color", "Button")

 .. code-tab:: csharp

    public override void _Ready()
    {
        // Lấy màu font được định nghĩa cho class của Control hiện tại, nếu tồn tại.
        Modulate = GetThemeColor("font_color");
        // Lấy màu font được định nghĩa cho class Button.
        Modulate = GetThemeColor("font_color", "Button");
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_constant:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_theme_constant**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_constant>`

Trả về một constant từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục constant với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_default_base_scale:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_theme_default_base_scale**\ (\ ) |const| :ref:`🔗<class_Control_method_get_theme_default_base_scale>`

Trả về giá trị base scale mặc định từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có giá trị :ref:`Theme.default_base_scale<class_Theme_property_default_base_scale>` hợp lệ.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_default_font:

.. rst-class:: classref-method

:ref:`Font<class_Font>` **get_theme_default_font**\ (\ ) |const| :ref:`🔗<class_Control_method_get_theme_default_font>`

Trả về font mặc định từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có giá trị :ref:`Theme.default_font<class_Theme_property_default_font>` hợp lệ.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_default_font_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_theme_default_font_size**\ (\ ) |const| :ref:`🔗<class_Control_method_get_theme_default_font_size>`

Trả về giá trị font size mặc định từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có giá trị :ref:`Theme.default_font_size<class_Theme_property_default_font_size>` hợp lệ.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_font:

.. rst-class:: classref-method

:ref:`Font<class_Font>` **get_theme_font**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_font>`

Trả về một :ref:`Font<class_Font>` từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục font với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_font_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_theme_font_size**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_font_size>`

Trả về font size từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục font size với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_icon:

.. rst-class:: classref-method

:ref:`Texture2D<class_Texture2D>` **get_theme_icon**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_icon>`

Trả về một icon từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục icon với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_theme_stylebox:

.. rst-class:: classref-method

:ref:`StyleBox<class_StyleBox>` **get_theme_stylebox**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_get_theme_stylebox>`

Trả về một :ref:`StyleBox<class_StyleBox>` từ :ref:`Theme<class_Theme>` đầu tiên khớp trong cây nếu :ref:`Theme<class_Theme>` đó có một mục stylebox với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_get_tooltip:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_tooltip**\ (\ at_position\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const| :ref:`🔗<class_Control_method_get_tooltip>`

Trả về văn bản tooltip cho vị trí ``at_position`` trong tọa độ cục bộ của control, thường sẽ xuất hiện khi con trỏ dừng trên control này. Theo mặc định, hàm trả về :ref:`tooltip_text<class_Control_property_tooltip_text>`.

Bạn có thể override :ref:`_get_tooltip()<class_Control_private_method__get_tooltip>` để triển khai hành vi tùy chỉnh cho phương thức này.

\ **Lưu ý:** Nếu phương thức này trả về một :ref:`String<class_String>` rỗng và :ref:`_make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>` không được override, sẽ không có tooltip nào được hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_grab_click_focus:

.. rst-class:: classref-method

|void| **grab_click_focus**\ (\ ) :ref:`🔗<class_Control_method_grab_click_focus>`

Tạo một :ref:`InputEventMouseButton<class_InputEventMouseButton>` cố gắng click vào control. Nếu event được nhận, control sẽ nhận focus.


.. tabs::

 .. code-tab:: gdscript

    func _process(delta):
        grab_click_focus() # Khi click vào một node Control khác, thay vào đó node này sẽ được click.

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        GrabClickFocus(); // Khi click vào một node Control khác, thay vào đó node này sẽ được click.
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_method_grab_focus:

.. rst-class:: classref-method

|void| **grab_focus**\ (\ hide_focus\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_grab_focus>`

Lấy focus từ một control khác và trở thành control được focus (xem :ref:`focus_mode<class_Control_property_focus_mode>`).

Nếu ``hide_focus`` là ``true``, control sẽ không hiển thị trạng thái được focus về mặt trực quan. Không có tác dụng đối với :ref:`LineEdit<class_LineEdit>` và :ref:`TextEdit<class_TextEdit>` khi :ref:`ProjectSettings.gui/common/show_focus_state_on_pointer_event<class_ProjectSettings_property_gui/common/show_focus_state_on_pointer_event>` được đặt thành ``Text Input Controls``, hoặc đối với bất kỳ control nào khi nó được đặt thành ``Always``.

\ **Lưu ý:** Sử dụng phương thức này cùng với :ref:`Callable.call_deferred()<class_Callable_method_call_deferred>` sẽ đáng tin cậy hơn, đặc biệt khi được gọi bên trong :ref:`Node._ready()<class_Node_private_method__ready>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_focus:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_focus**\ (\ ignore_hidden_focus\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Control_method_has_focus>`

Trả về ``true`` nếu đây là control hiện đang được focus. Xem :ref:`focus_mode<class_Control_property_focus_mode>`.

Nếu ``ignore_hidden_focus`` là ``true``, các control bị ẩn focus sẽ luôn trả về ``false``. Focus bị ẩn tự động xảy ra khi các control nhận focus thông qua thao tác chuột hoặc thủ công bằng cách sử dụng :ref:`grab_focus()<class_Control_method_grab_focus>` với ``hide_focus`` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_color:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_color**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_color>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một color item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_color_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_color_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_color_override>`

Trả về ``true`` nếu có một override cục bộ cho theme :ref:`Color<class_Color>` với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_color_override()<class_Control_method_add_theme_color_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_constant:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_constant**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_constant>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một constant item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_constant_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_constant_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_constant_override>`

Trả về ``true`` nếu có một override cục bộ cho theme constant với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_constant_override()<class_Control_method_add_theme_constant_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_font:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_font**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_font>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một font item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_font_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_font_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_font_override>`

Trả về ``true`` nếu có một override cục bộ cho theme :ref:`Font<class_Font>` với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_font_override()<class_Control_method_add_theme_font_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_font_size:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_font_size**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_font_size>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một font size item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_font_size_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_font_size_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_font_size_override>`

Trả về ``true`` nếu có một override cục bộ cho theme font size với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_font_size_override()<class_Control_method_add_theme_font_size_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_icon:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_icon**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_icon>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một icon item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_icon_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_icon_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_icon_override>`

Trả về ``true`` nếu có một override cục bộ cho theme icon với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_icon_override()<class_Control_method_add_theme_icon_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_stylebox:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_stylebox**\ (\ name\: :ref:`StringName<class_StringName>`, theme_type\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Control_method_has_theme_stylebox>`

Trả về ``true`` nếu có một :ref:`Theme<class_Theme>` khớp trong tree có một stylebox item với ``name`` và ``theme_type`` được chỉ định.

Xem :ref:`get_theme_color()<class_Control_method_get_theme_color>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_has_theme_stylebox_override:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_theme_stylebox_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Control_method_has_theme_stylebox_override>`

Trả về ``true`` nếu có một override cục bộ cho theme :ref:`StyleBox<class_StyleBox>` với ``name`` được chỉ định trong node **Control** này.

Xem :ref:`add_theme_stylebox_override()<class_Control_method_add_theme_stylebox_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_is_drag_successful:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_drag_successful**\ (\ ) |const| :ref:`🔗<class_Control_method_is_drag_successful>`

Trả về ``true`` nếu thao tác kéo thành công. Đây là phương án thay thế cho :ref:`Viewport.gui_is_drag_successful()<class_Viewport_method_gui_is_drag_successful>`.

Nên sử dụng cùng với :ref:`Node.NOTIFICATION_DRAG_END<class_Node_constant_NOTIFICATION_DRAG_END>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_is_layout_rtl:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_layout_rtl**\ (\ ) |const| :ref:`🔗<class_Control_method_is_layout_rtl>`

Trả về ``true`` nếu layout là right-to-left. Xem thêm :ref:`layout_direction<class_Control_property_layout_direction>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_release_focus:

.. rst-class:: classref-method

|void| **release_focus**\ (\ ) :ref:`🔗<class_Control_method_release_focus>`

Bỏ focus. Không control nào khác có thể nhận input.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_color_override:

.. rst-class:: classref-method

|void| **remove_theme_color_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_color_override>`

Xóa override cục bộ cho theme :ref:`Color<class_Color>` với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_color_override()<class_Control_method_add_theme_color_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_constant_override:

.. rst-class:: classref-method

|void| **remove_theme_constant_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_constant_override>`

Xóa override cục bộ cho theme constant với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_constant_override()<class_Control_method_add_theme_constant_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_font_override:

.. rst-class:: classref-method

|void| **remove_theme_font_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_font_override>`

Xóa override cục bộ cho theme :ref:`Font<class_Font>` với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_font_override()<class_Control_method_add_theme_font_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_font_size_override:

.. rst-class:: classref-method

|void| **remove_theme_font_size_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_font_size_override>`

Xóa override cục bộ cho theme font size với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_font_size_override()<class_Control_method_add_theme_font_size_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_icon_override:

.. rst-class:: classref-method

|void| **remove_theme_icon_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_icon_override>`

Xóa override cục bộ cho theme icon với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_icon_override()<class_Control_method_add_theme_icon_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_remove_theme_stylebox_override:

.. rst-class:: classref-method

|void| **remove_theme_stylebox_override**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Control_method_remove_theme_stylebox_override>`

Xóa override cục bộ cho theme :ref:`StyleBox<class_StyleBox>` với ``name`` được chỉ định, trước đó được thêm bởi :ref:`add_theme_stylebox_override()<class_Control_method_add_theme_stylebox_override>` hoặc thông qua Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_reset_size:

.. rst-class:: classref-method

|void| **reset_size**\ (\ ) :ref:`🔗<class_Control_method_reset_size>`

Đặt lại kích thước thành :ref:`get_combined_minimum_size()<class_Control_method_get_combined_minimum_size>`. Tương đương với việc gọi ``set_size(Vector2())`` (hoặc bất kỳ kích thước nào nhỏ hơn mức tối thiểu).

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_anchor:

.. rst-class:: classref-method

|void| **set_anchor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, anchor\: :ref:`float<class_float>`, keep_offset\: :ref:`bool<class_bool>` = false, push_opposite_anchor\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_Control_method_set_anchor>`

Đặt anchor cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định thành ``anchor``. Đây là phương thức setter cho :ref:`anchor_bottom<class_Control_property_anchor_bottom>`, :ref:`anchor_left<class_Control_property_anchor_left>`, :ref:`anchor_right<class_Control_property_anchor_right>` và :ref:`anchor_top<class_Control_property_anchor_top>`.

Nếu ``keep_offset`` là ``true``, các offset sẽ không được cập nhật sau thao tác này.

Nếu ``push_opposite_anchor`` là ``true`` và anchor đối diện chồng lên anchor này, giá trị của anchor đối diện sẽ bị ghi đè. Ví dụ, khi đặt anchor trái thành 1 và anchor phải có giá trị 0.5, anchor phải cũng sẽ nhận giá trị 1. Nếu ``push_opposite_anchor`` là ``false``, anchor trái sẽ nhận giá trị 0.5.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_anchor_and_offset:

.. rst-class:: classref-method

|void| **set_anchor_and_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, anchor\: :ref:`float<class_float>`, offset\: :ref:`float<class_float>`, push_opposite_anchor\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_set_anchor_and_offset>`

Hoạt động giống như :ref:`set_anchor()<class_Control_method_set_anchor>`, nhưng thay vì đối số ``keep_offset`` và việc tự động cập nhật offset, cho phép bạn tự đặt offset (xem :ref:`set_offset()<class_Control_method_set_offset>`).

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_anchors_and_offsets_preset:

.. rst-class:: classref-method

|void| **set_anchors_and_offsets_preset**\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, resize_mode\: :ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` = 0, margin\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_Control_method_set_anchors_and_offsets_preset>`

Đặt cả anchor preset và offset preset. Xem :ref:`set_anchors_preset()<class_Control_method_set_anchors_preset>` và :ref:`set_offsets_preset()<class_Control_method_set_offsets_preset>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_anchors_preset:

.. rst-class:: classref-method

|void| **set_anchors_preset**\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, keep_offsets\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_set_anchors_preset>`

Đặt các anchor thành một ``preset`` từ enum :ref:`LayoutPreset<enum_Control_LayoutPreset>`. Đây là tương đương trong code với việc sử dụng menu Layout trong trình chỉnh sửa 2D.

Nếu ``keep_offsets`` là ``true``, vị trí của control cũng sẽ được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_begin:

.. rst-class:: classref-method

|void| **set_begin**\ (\ position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Control_method_set_begin>`

Đặt :ref:`offset_left<class_Control_property_offset_left>` và :ref:`offset_top<class_Control_property_offset_top>` cùng lúc. Tương đương với việc thay đổi :ref:`position<class_Control_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_drag_forwarding:

.. rst-class:: classref-method

|void| **set_drag_forwarding**\ (\ drag_func\: :ref:`Callable<class_Callable>`, can_drop_func\: :ref:`Callable<class_Callable>`, drop_func\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_Control_method_set_drag_forwarding>`

Đặt các callable được cung cấp để sử dụng thay cho các phương thức ảo drag-and-drop của control. Nếu một callable trống, phương thức ảo tương ứng sẽ được sử dụng như bình thường.

Các đối số của mỗi callable phải hoàn toàn giống với các phương thức ảo tương ứng, cụ thể là:

- ``drag_func`` tương ứng với :ref:`_get_drag_data()<class_Control_private_method__get_drag_data>` và yêu cầu một :ref:`Vector2<class_Vector2>`;

- ``can_drop_func`` tương ứng với :ref:`_can_drop_data()<class_Control_private_method__can_drop_data>` và yêu cầu cả :ref:`Vector2<class_Vector2>` lẫn :ref:`Variant<class_Variant>`;

- ``drop_func`` tương ứng với :ref:`_drop_data()<class_Control_private_method__drop_data>` và yêu cầu cả :ref:`Vector2<class_Vector2>` lẫn :ref:`Variant<class_Variant>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_drag_preview:

.. rst-class:: classref-method

|void| **set_drag_preview**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_Control_method_set_drag_preview>`

Hiển thị control được cung cấp tại vị trí con trỏ chuột. Thời điểm thích hợp để gọi phương thức này là trong :ref:`_get_drag_data()<class_Control_private_method__get_drag_data>`. Control không được nằm trong scene tree. Bạn không nên giải phóng control và không nên giữ tham chiếu đến control sau khi thao tác kéo kết thúc. Control sẽ tự động bị xóa sau khi thao tác kéo kết thúc.


.. tabs::

 .. code-tab:: gdscript

    @export var color = Color(1, 0, 0, 1)

    func _get_drag_data(position):
        # Sử dụng một control không nằm trong tree
        var cpb = ColorPickerButton.new()
        cpb.color = color
        cpb.size = Vector2(50, 50)
        set_drag_preview(cpb)
        return color

 .. code-tab:: csharp

    [Export]
    private Color _color = new Color(1, 0, 0, 1);

    public override Variant _GetDragData(Vector2 atPosition)
    {
        // Sử dụng một control không nằm trong tree
        var cpb = new ColorPickerButton();
        cpb.Color = _color;
        cpb.Size = new Vector2(50, 50);
        SetDragPreview(cpb);
        return _color;
    }



.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_end:

.. rst-class:: classref-method

|void| **set_end**\ (\ position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Control_method_set_end>`

Đặt :ref:`offset_right<class_Control_property_offset_right>` và :ref:`offset_bottom<class_Control_property_offset_bottom>` cùng lúc.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_focus_neighbor:

.. rst-class:: classref-method

|void| **set_focus_neighbor**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, neighbor\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_Control_method_set_focus_neighbor>`

Đặt focus neighbor cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định thành **Control** tại node path ``neighbor``. Một phương thức setter cho :ref:`focus_neighbor_bottom<class_Control_property_focus_neighbor_bottom>`, :ref:`focus_neighbor_left<class_Control_property_focus_neighbor_left>`, :ref:`focus_neighbor_right<class_Control_property_focus_neighbor_right>` và :ref:`focus_neighbor_top<class_Control_property_focus_neighbor_top>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_global_position:

.. rst-class:: classref-method

|void| **set_global_position**\ (\ position\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_set_global_position>`

Đặt :ref:`global_position<class_Control_property_global_position>` thành ``position`` được cung cấp.

Nếu ``keep_offsets`` là ``true``, các anchor của control sẽ được cập nhật thay vì các offset.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_offset:

.. rst-class:: classref-method

|void| **set_offset**\ (\ side\: :ref:`Side<enum_@GlobalScope_Side>`, offset\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Control_method_set_offset>`

Đặt offset cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định thành ``offset``. Một phương thức setter cho :ref:`offset_bottom<class_Control_property_offset_bottom>`, :ref:`offset_left<class_Control_property_offset_left>`, :ref:`offset_right<class_Control_property_offset_right>` và :ref:`offset_top<class_Control_property_offset_top>`.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_offsets_preset:

.. rst-class:: classref-method

|void| **set_offsets_preset**\ (\ preset\: :ref:`LayoutPreset<enum_Control_LayoutPreset>`, resize_mode\: :ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` = 0, margin\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_Control_method_set_offsets_preset>`

Đặt các offset thành một ``preset`` từ enum :ref:`LayoutPreset<enum_Control_LayoutPreset>`. Đây là tương đương trong code với việc sử dụng menu Layout trong trình chỉnh sửa 2D.

Sử dụng tham số ``resize_mode`` với các hằng số từ :ref:`LayoutPresetMode<enum_Control_LayoutPresetMode>` để xác định tốt hơn kích thước kết quả của **Control**. Kích thước cố định sẽ bị bỏ qua nếu được sử dụng với các preset làm thay đổi kích thước, chẳng hạn như :ref:`PRESET_LEFT_WIDE<class_Control_constant_PRESET_LEFT_WIDE>`.

Sử dụng tham số ``margin`` để xác định khoảng cách giữa **Control** và các cạnh.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_position:

.. rst-class:: classref-method

|void| **set_position**\ (\ position\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_set_position>`

Đặt :ref:`position<class_Control_property_position>` thành ``position`` được cung cấp.

Nếu ``keep_offsets`` là ``true``, các anchor của control sẽ được cập nhật thay vì các offset.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_set_size:

.. rst-class:: classref-method

|void| **set_size**\ (\ size\: :ref:`Vector2<class_Vector2>`, keep_offsets\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Control_method_set_size>`

Đặt kích thước (xem :ref:`size<class_Control_property_size>`).

Nếu ``keep_offsets`` là ``true``, các anchor của control sẽ được cập nhật thay vì các offset.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_update_maximum_size:

.. rst-class:: classref-method

|void| **update_maximum_size**\ (\ ) :ref:`🔗<class_Control_method_update_maximum_size>`

Vô hiệu hóa cache kích thước tối đa trong node này và các node con có :ref:`CanvasItem.top_level<class_CanvasItem_property_top_level>` được đặt thành ``false``. Dự kiến được sử dụng với :ref:`get_maximum_size()<class_Control_method_get_maximum_size>` khi giá trị trả về thay đổi. Việc đặt trực tiếp :ref:`custom_maximum_size<class_Control_property_custom_maximum_size>` sẽ tự động gọi phương thức này.

\ **Lưu ý:** Việc gọi phương thức này cũng gọi :ref:`update_minimum_size()<class_Control_method_update_minimum_size>` vì kích thước tối thiểu kết hợp có thể bị ảnh hưởng bởi thay đổi kích thước tối đa.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_update_minimum_size:

.. rst-class:: classref-method

|void| **update_minimum_size**\ (\ ) :ref:`🔗<class_Control_method_update_minimum_size>`

Vô hiệu hóa cache kích thước tối thiểu trong node này và các node cha cho đến cấp cao nhất. Dự kiến được sử dụng với :ref:`get_minimum_size()<class_Control_method_get_minimum_size>` khi giá trị trả về thay đổi. Việc đặt trực tiếp :ref:`custom_minimum_size<class_Control_property_custom_minimum_size>` sẽ tự động gọi phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Control_method_warp_mouse:

.. rst-class:: classref-method

|void| **warp_mouse**\ (\ position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Control_method_warp_mouse>`

Di chuyển con trỏ chuột đến ``position``, tương đối so với :ref:`position<class_Control_property_position>` của **Control** này.

\ **Lưu ý:** :ref:`warp_mouse()<class_Control_method_warp_mouse>` chỉ được hỗ trợ trên Windows, macOS và Linux. Nó không có tác dụng trên Android, iOS và Web.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
