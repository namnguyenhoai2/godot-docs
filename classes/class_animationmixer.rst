:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationMixer.xml.

.. _class_AnimationMixer:

AnimationMixer
==============

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AnimationPlayer<class_AnimationPlayer>`, :ref:`AnimationTree<class_AnimationTree>`

Lớp cơ sở cho :ref:`AnimationPlayer<class_AnimationPlayer>` và :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho :ref:`AnimationPlayer<class_AnimationPlayer>` và :ref:`AnimationTree<class_AnimationTree>` để quản lý các danh sách animation. Lớp này cũng có các thuộc tính và phương thức chung để phát và blending.

Sau khi khởi tạo dữ liệu thông tin phát trong lớp mở rộng, việc blending được xử lý bởi **AnimationMixer**.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Migrating Animations from Godot 4.0 to 4.3 <https://godotengine.org/article/migrating-animations-from-godot-4-0-to-4-3/>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                                                 | :ref:`active<class_AnimationMixer_property_active>`                                 | ``true``           |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`int<class_int>`                                                                   | :ref:`audio_max_polyphony<class_AnimationMixer_property_audio_max_polyphony>`       | ``32``             |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` | :ref:`callback_mode_discrete<class_AnimationMixer_property_callback_mode_discrete>` | ``1``              |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>`     | :ref:`callback_mode_method<class_AnimationMixer_property_callback_mode_method>`     | ``0``              |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>`   | :ref:`callback_mode_process<class_AnimationMixer_property_callback_mode_process>`   | ``1``              |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                                                 | :ref:`deterministic<class_AnimationMixer_property_deterministic>`                   | ``false``          |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                                                 | :ref:`reset_on_save<class_AnimationMixer_property_reset_on_save>`                   | ``true``           |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                                                 | :ref:`root_motion_local<class_AnimationMixer_property_root_motion_local>`           | ``false``          |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`NodePath<class_NodePath>`                                                         | :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>`           | ``NodePath("")``   |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+
   | :ref:`NodePath<class_NodePath>`                                                         | :ref:`root_node<class_AnimationMixer_property_root_node>`                           | ``NodePath("..")`` |
   +-----------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+--------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`_post_process_key_value<class_AnimationMixer_private_method__post_process_key_value>`\ (\ animation\: :ref:`Animation<class_Animation>`, track\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`, object_id\: :ref:`int<class_int>`, object_sub_idx\: :ref:`int<class_int>`\ ) |virtual| |const| |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`add_animation_library<class_AnimationMixer_method_add_animation_library>`\ (\ name\: :ref:`StringName<class_StringName>`, library\: :ref:`AnimationLibrary<class_AnimationLibrary>`\ )                                                                                                                        |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`advance<class_AnimationMixer_method_advance>`\ (\ delta\: :ref:`float<class_float>`\ )                                                                                                                                                                                                                        |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`capture<class_AnimationMixer_method_capture>`\ (\ name\: :ref:`StringName<class_StringName>`, duration\: :ref:`float<class_float>`, trans_type\: :ref:`TransitionType<enum_Tween_TransitionType>` = 0, ease_type\: :ref:`EaseType<enum_Tween_EaseType>` = 0\ )                                                |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`clear_caches<class_AnimationMixer_method_clear_caches>`\ (\ )                                                                                                                                                                                                                                                 |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                              | :ref:`find_animation<class_AnimationMixer_method_find_animation>`\ (\ animation\: :ref:`Animation<class_Animation>`\ ) |const|                                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                              | :ref:`find_animation_library<class_AnimationMixer_method_find_animation_library>`\ (\ animation\: :ref:`Animation<class_Animation>`\ ) |const|                                                                                                                                                                      |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Animation<class_Animation>`                                | :ref:`get_animation<class_AnimationMixer_method_get_animation>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                                           |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AnimationLibrary<class_AnimationLibrary>`                  | :ref:`get_animation_library<class_AnimationMixer_method_get_animation_library>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                           |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_animation_library_list<class_AnimationMixer_method_get_animation_library_list>`\ (\ ) |const|                                                                                                                                                                                                             |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`get_animation_list<class_AnimationMixer_method_get_animation_list>`\ (\ ) |const|                                                                                                                                                                                                                             |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                    | :ref:`get_root_motion_position<class_AnimationMixer_method_get_root_motion_position>`\ (\ ) |const|                                                                                                                                                                                                                 |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                    | :ref:`get_root_motion_position_accumulator<class_AnimationMixer_method_get_root_motion_position_accumulator>`\ (\ ) |const|                                                                                                                                                                                         |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`                              | :ref:`get_root_motion_rotation<class_AnimationMixer_method_get_root_motion_rotation>`\ (\ ) |const|                                                                                                                                                                                                                 |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`                              | :ref:`get_root_motion_rotation_accumulator<class_AnimationMixer_method_get_root_motion_rotation_accumulator>`\ (\ ) |const|                                                                                                                                                                                         |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                    | :ref:`get_root_motion_scale<class_AnimationMixer_method_get_root_motion_scale>`\ (\ ) |const|                                                                                                                                                                                                                       |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                    | :ref:`get_root_motion_scale_accumulator<class_AnimationMixer_method_get_root_motion_scale_accumulator>`\ (\ ) |const|                                                                                                                                                                                               |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_animation<class_AnimationMixer_method_has_animation>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                                           |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_animation_library<class_AnimationMixer_method_has_animation_library>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                                                           |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_animation_library<class_AnimationMixer_method_remove_animation_library>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                                             |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`rename_animation_library<class_AnimationMixer_method_rename_animation_library>`\ (\ name\: :ref:`StringName<class_StringName>`, newname\: :ref:`StringName<class_StringName>`\ )                                                                                                                              |
   +------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_AnimationMixer_signal_animation_finished:

.. rst-class:: classref-signal

**animation_finished**\ (\ anim_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationMixer_signal_animation_finished>`

Thông báo khi một animation phát xong.

\ **Lưu ý:** Signal này không được phát nếu animation đang lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_animation_libraries_updated:

.. rst-class:: classref-signal

**animation_libraries_updated**\ (\ ) :ref:`🔗<class_AnimationMixer_signal_animation_libraries_updated>`

Thông báo khi các thư viện animation đã thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_animation_list_changed:

.. rst-class:: classref-signal

**animation_list_changed**\ (\ ) :ref:`🔗<class_AnimationMixer_signal_animation_list_changed>`

Thông báo khi danh sách animation thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_animation_started:

.. rst-class:: classref-signal

**animation_started**\ (\ anim_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationMixer_signal_animation_started>`

Thông báo khi một animation bắt đầu phát.

\ **Lưu ý:** Signal này không được phát nếu animation đang lặp.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_caches_cleared:

.. rst-class:: classref-signal

**caches_cleared**\ (\ ) :ref:`🔗<class_AnimationMixer_signal_caches_cleared>`

Thông báo khi các cache đã được xóa, είτε tự động hoặc thủ công thông qua :ref:`clear_caches()<class_AnimationMixer_method_clear_caches>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_mixer_applied:

.. rst-class:: classref-signal

**mixer_applied**\ (\ ) :ref:`🔗<class_AnimationMixer_signal_mixer_applied>`

Thông báo khi kết quả blending liên quan đã được áp dụng cho các đối tượng đích.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_signal_mixer_updated:

.. rst-class:: classref-signal

**mixer_updated**\ (\ ) :ref:`🔗<class_AnimationMixer_signal_mixer_updated>`

Thông báo khi quy trình liên quan đến thuộc tính đã được cập nhật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AnimationMixer_AnimationCallbackModeProcess:

.. rst-class:: classref-enumeration

enum **AnimationCallbackModeProcess**: :ref:`🔗<enum_AnimationMixer_AnimationCallbackModeProcess>`

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>` **ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS** = ``0``

Xử lý animation trong các frame physics (xem :ref:`Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`). Điều này đặc biệt hữu ích khi tạo animation cho các physics body.

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_IDLE:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>` **ANIMATION_CALLBACK_MODE_PROCESS_IDLE** = ``1``

Xử lý animation trong các frame process (xem :ref:`Node.NOTIFICATION_INTERNAL_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`).

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_MANUAL:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>` **ANIMATION_CALLBACK_MODE_PROCESS_MANUAL** = ``2``

Không xử lý animation. Sử dụng :ref:`advance()<class_AnimationMixer_method_advance>` để tự xử lý animation.

.. rst-class:: classref-item-separator

----

.. _enum_AnimationMixer_AnimationCallbackModeMethod:

.. rst-class:: classref-enumeration

enum **AnimationCallbackModeMethod**: :ref:`🔗<enum_AnimationMixer_AnimationCallbackModeMethod>`

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_METHOD_DEFERRED:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>` **ANIMATION_CALLBACK_MODE_METHOD_DEFERRED** = ``0``

Gom các lệnh gọi method trong quá trình xử lý animation, sau đó thực hiện các lệnh gọi sau khi các event được xử lý. Điều này tránh các lỗi liên quan đến việc xóa node hoặc sửa đổi AnimationPlayer trong khi đang phát.

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>` **ANIMATION_CALLBACK_MODE_METHOD_IMMEDIATE** = ``1``

Thực hiện các lệnh gọi method ngay khi gặp chúng trong animation.

.. rst-class:: classref-item-separator

----

.. _enum_AnimationMixer_AnimationCallbackModeDiscrete:

.. rst-class:: classref-enumeration

enum **AnimationCallbackModeDiscrete**: :ref:`🔗<enum_AnimationMixer_AnimationCallbackModeDiscrete>`

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_DISCRETE_DOMINANT:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` **ANIMATION_CALLBACK_MODE_DISCRETE_DOMINANT** = ``0``

Giá trị track :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>` được ưu tiên khi blending các giá trị track :ref:`Animation.UPDATE_CONTINUOUS<class_Animation_constant_UPDATE_CONTINUOUS>` hoặc :ref:`Animation.UPDATE_CAPTURE<class_Animation_constant_UPDATE_CAPTURE>` và các giá trị track :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>`.

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` **ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE** = ``1``

Giá trị track :ref:`Animation.UPDATE_CONTINUOUS<class_Animation_constant_UPDATE_CONTINUOUS>` hoặc :ref:`Animation.UPDATE_CAPTURE<class_Animation_constant_UPDATE_CAPTURE>` được ưu tiên khi blending các giá trị track :ref:`Animation.UPDATE_CONTINUOUS<class_Animation_constant_UPDATE_CONTINUOUS>` hoặc :ref:`Animation.UPDATE_CAPTURE<class_Animation_constant_UPDATE_CAPTURE>` và các giá trị track :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>`. Đây là hành vi mặc định của :ref:`AnimationPlayer<class_AnimationPlayer>`.

.. _class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS:

.. rst-class:: classref-enumeration-constant

:ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` **ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS** = ``2``

Luôn xem giá trị track :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>` là :ref:`Animation.UPDATE_CONTINUOUS<class_Animation_constant_UPDATE_CONTINUOUS>` với :ref:`Animation.INTERPOLATION_NEAREST<class_Animation_constant_INTERPOLATION_NEAREST>`. Đây là hành vi mặc định của :ref:`AnimationTree<class_AnimationTree>`.

Nếu một value track có các giá trị key thuộc kiểu không thể nội suy, nó sẽ được chuyển đổi nội bộ để sử dụng :ref:`ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_DISCRETE_RECESSIVE>` với :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>`.

Danh sách kiểu không thể nội suy:

- :ref:`@GlobalScope.TYPE_NIL<class_@GlobalScope_constant_TYPE_NIL>`\

- :ref:`@GlobalScope.TYPE_NODE_PATH<class_@GlobalScope_constant_TYPE_NODE_PATH>`\

- :ref:`@GlobalScope.TYPE_RID<class_@GlobalScope_constant_TYPE_RID>`\

- :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>`\

- :ref:`@GlobalScope.TYPE_CALLABLE<class_@GlobalScope_constant_TYPE_CALLABLE>`\

- :ref:`@GlobalScope.TYPE_SIGNAL<class_@GlobalScope_constant_TYPE_SIGNAL>`\

- :ref:`@GlobalScope.TYPE_DICTIONARY<class_@GlobalScope_constant_TYPE_DICTIONARY>`\

- :ref:`@GlobalScope.TYPE_PACKED_BYTE_ARRAY<class_@GlobalScope_constant_TYPE_PACKED_BYTE_ARRAY>`\

\ :ref:`@GlobalScope.TYPE_BOOL<class_@GlobalScope_constant_TYPE_BOOL>` và :ref:`@GlobalScope.TYPE_INT<class_@GlobalScope_constant_TYPE_INT>` được xử lý như :ref:`@GlobalScope.TYPE_FLOAT<class_@GlobalScope_constant_TYPE_FLOAT>` trong quá trình blending và được làm tròn khi lấy kết quả.

Điều tương tự cũng áp dụng cho các array và vector chứa chúng, chẳng hạn như :ref:`@GlobalScope.TYPE_PACKED_INT32_ARRAY<class_@GlobalScope_constant_TYPE_PACKED_INT32_ARRAY>` hoặc :ref:`@GlobalScope.TYPE_VECTOR2I<class_@GlobalScope_constant_TYPE_VECTOR2I>`; chúng được xử lý như :ref:`@GlobalScope.TYPE_PACKED_FLOAT32_ARRAY<class_@GlobalScope_constant_TYPE_PACKED_FLOAT32_ARRAY>` hoặc :ref:`@GlobalScope.TYPE_VECTOR2<class_@GlobalScope_constant_TYPE_VECTOR2>`. Ngoài ra, đối với array, kích thước cũng được nội suy.

\ :ref:`@GlobalScope.TYPE_STRING<class_@GlobalScope_constant_TYPE_STRING>` và :ref:`@GlobalScope.TYPE_STRING_NAME<class_@GlobalScope_constant_TYPE_STRING_NAME>` được nội suy giữa các mã ký tự và độ dài, nhưng lưu ý rằng thuật toán nội suy giữa các key khác với thuật toán nội suy bằng blending.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationMixer_property_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **active** = ``true`` :ref:`🔗<class_AnimationMixer_property_active>`

.. rst-class:: classref-property-setget

- |void| **set_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_active**\ (\ )

Nếu ``true``, **AnimationMixer** sẽ được xử lý.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_audio_max_polyphony:

.. rst-class:: classref-property

:ref:`int<class_int>` **audio_max_polyphony** = ``32`` :ref:`🔗<class_AnimationMixer_property_audio_max_polyphony>`

.. rst-class:: classref-property-setget

- |void| **set_audio_max_polyphony**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_audio_max_polyphony**\ (\ )

Số lượng âm thanh đồng thời tối đa có thể phát cho mỗi AudioStreamPlayer được gán.

For example, if this value is ``32`` and the animation has two audio tracks, the two :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`\ s assigned can play simultaneously up to ``32`` voices each.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_callback_mode_discrete:

.. rst-class:: classref-property

:ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` **callback_mode_discrete** = ``1`` :ref:`🔗<class_AnimationMixer_property_callback_mode_discrete>`

.. rst-class:: classref-property-setget

- |void| **set_callback_mode_discrete**\ (\ value\: :ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>`\ ) - :ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>` **get_callback_mode_discrete**\ (\ )

Thông thường, các track có thể được đặt thành :ref:`Animation.UPDATE_DISCRETE<class_Animation_constant_UPDATE_DISCRETE>` để cập nhật không thường xuyên, thường là khi sử dụng nearest interpolation.

Tuy nhiên, khi blending với :ref:`Animation.UPDATE_CONTINUOUS<class_Animation_constant_UPDATE_CONTINUOUS>`, một số kết quả sẽ được xem xét. :ref:`callback_mode_discrete<class_AnimationMixer_property_callback_mode_discrete>` chỉ định điều đó một cách rõ ràng. Xem thêm :ref:`AnimationCallbackModeDiscrete<enum_AnimationMixer_AnimationCallbackModeDiscrete>`.

Để kết quả blending trông đẹp mắt, bạn nên đặt giá trị này thành :ref:`ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_DISCRETE_FORCE_CONTINUOUS>` để cập nhật ở mỗi frame trong quá trình blending. Các giá trị khác tồn tại để đảm bảo khả năng tương thích và phù hợp nếu không có blending, nhưng nếu không, chúng có thể tạo ra các artifact.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_callback_mode_method:

.. rst-class:: classref-property

:ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>` **callback_mode_method** = ``0`` :ref:`🔗<class_AnimationMixer_property_callback_mode_method>`

.. rst-class:: classref-property-setget

- |void| **set_callback_mode_method**\ (\ value\: :ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>`\ ) - :ref:`AnimationCallbackModeMethod<enum_AnimationMixer_AnimationCallbackModeMethod>` **get_callback_mode_method**\ (\ )

Chế độ gọi được sử dụng cho các track "Call Method".

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_callback_mode_process:

.. rst-class:: classref-property

:ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>` **callback_mode_process** = ``1`` :ref:`🔗<class_AnimationMixer_property_callback_mode_process>`

.. rst-class:: classref-property-setget

- |void| **set_callback_mode_process**\ (\ value\: :ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>`\ ) - :ref:`AnimationCallbackModeProcess<enum_AnimationMixer_AnimationCallbackModeProcess>` **get_callback_mode_process**\ (\ )

Thông báo process dùng để cập nhật animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_deterministic:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **deterministic** = ``false`` :ref:`🔗<class_AnimationMixer_property_deterministic>`

.. rst-class:: classref-property-setget

- |void| **set_deterministic**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_deterministic**\ (\ )

Nếu ``true``, blending sử dụng thuật toán deterministic. Tổng trọng số không được chuẩn hóa và kết quả được cộng dồn với một giá trị ban đầu (``0`` hoặc animation ``"RESET"`` nếu có).

Điều này có nghĩa là nếu tổng mức blending là ``0.0``, kết quả sẽ bằng animation ``"RESET"``.

Nếu số lượng track giữa các animation được blend khác nhau, animation bị thiếu track sẽ được xử lý như thể nó có giá trị ban đầu.

Nếu ``false``, blend không sử dụng thuật toán deterministic. Tổng trọng số được chuẩn hóa và luôn là ``1.0``. Nếu số lượng track giữa các animation được blend khác nhau, không có xử lý nào được thực hiện đối với animation bị thiếu track.

\ **Lưu ý:** Trong :ref:`AnimationTree<class_AnimationTree>`, blending với :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>`, :ref:`AnimationNodeAdd3<class_AnimationNodeAdd3>`, :ref:`AnimationNodeSub2<class_AnimationNodeSub2>` hoặc trọng số lớn hơn ``1.0`` có thể tạo ra kết quả không mong muốn.

Ví dụ, nếu :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>` blend hai node với mức ``1.0``, tổng trọng số là ``2.0`` nhưng sẽ được chuẩn hóa để tổng mức trở thành ``1.0``, và kết quả sẽ tương đương với :ref:`AnimationNodeBlend2<class_AnimationNodeBlend2>` ở mức ``0.5``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_reset_on_save:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **reset_on_save** = ``true`` :ref:`🔗<class_AnimationMixer_property_reset_on_save>`

.. rst-class:: classref-property-setget

- |void| **set_reset_on_save_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_reset_on_save_enabled**\ (\ )

Tính năng này được editor sử dụng. Nếu được đặt thành ``true``, scene sẽ được lưu với các hiệu ứng của reset animation (animation có key ``"RESET"``) được áp dụng như thể animation đã được seek đến thời điểm 0, trong khi editor giữ lại các giá trị mà scene có trước khi lưu.

Điều này giúp việc xem trước và chỉnh sửa animation trong editor thuận tiện hơn, vì các thay đổi đối với scene sẽ không được lưu chừng nào chúng còn được đặt trong reset animation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_root_motion_local:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **root_motion_local** = ``false`` :ref:`🔗<class_AnimationMixer_property_root_motion_local>`

.. rst-class:: classref-property-setget

- |void| **set_root_motion_local**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_root_motion_local**\ (\ )

Nếu ``true``, giá trị :ref:`get_root_motion_position()<class_AnimationMixer_method_get_root_motion_position>` được trích xuất dưới dạng giá trị translation cục bộ trước khi blending. Nói cách khác, nó được xử lý như thể translation được thực hiện sau rotation.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_root_motion_track:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **root_motion_track** = ``NodePath("")`` :ref:`🔗<class_AnimationMixer_property_root_motion_track>`

.. rst-class:: classref-property-setget

- |void| **set_root_motion_track**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_root_motion_track**\ (\ )

Đường dẫn đến Animation track được sử dụng cho root motion. Các đường dẫn phải là scene-tree path hợp lệ đến một node và phải được chỉ định bắt đầu từ node cha của node sẽ tái tạo animation. :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` sử dụng cùng định dạng với :ref:`Animation.track_set_path()<class_Animation_method_track_set_path>`, nhưng lưu ý rằng phải chỉ định một bone.

Nếu track có kiểu :ref:`Animation.TYPE_POSITION_3D<class_Animation_constant_TYPE_POSITION_3D>`, :ref:`Animation.TYPE_ROTATION_3D<class_Animation_constant_TYPE_ROTATION_3D>` hoặc :ref:`Animation.TYPE_SCALE_3D<class_Animation_constant_TYPE_SCALE_3D>`, phép biến đổi sẽ bị hủy về mặt trực quan và animation sẽ có vẻ như đứng yên. Xem thêm :ref:`get_root_motion_position()<class_AnimationMixer_method_get_root_motion_position>`, :ref:`get_root_motion_rotation()<class_AnimationMixer_method_get_root_motion_rotation>`, :ref:`get_root_motion_scale()<class_AnimationMixer_method_get_root_motion_scale>` và :ref:`RootMotionView<class_RootMotionView>`.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_property_root_node:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **root_node** = ``NodePath("..")`` :ref:`🔗<class_AnimationMixer_property_root_node>`

.. rst-class:: classref-property-setget

- |void| **set_root_node**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_root_node**\ (\ )

Node mà các node path sẽ di chuyển từ đó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_AnimationMixer_private_method__post_process_key_value:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_post_process_key_value**\ (\ animation\: :ref:`Animation<class_Animation>`, track\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`, object_id\: :ref:`int<class_int>`, object_sub_idx\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_AnimationMixer_private_method__post_process_key_value>`

Một virtual function dùng để xử lý sau khi lấy được key trong quá trình playback.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_add_animation_library:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **add_animation_library**\ (\ name\: :ref:`StringName<class_StringName>`, library\: :ref:`AnimationLibrary<class_AnimationLibrary>`\ ) :ref:`🔗<class_AnimationMixer_method_add_animation_library>`

Thêm ``library`` vào animation player, với key ``name``.

AnimationMixer mặc định có một library toàn cục với chuỗi rỗng làm key. Để thêm một animation vào library toàn cục:


.. tabs::

 .. code-tab:: gdscript

    var global_library = mixer.get_animation_library("")
    global_library.add_animation("animation_name", animation_resource)



.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_advance:

.. rst-class:: classref-method

|void| **advance**\ (\ delta\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AnimationMixer_method_advance>`

Tiến animation thủ công theo khoảng thời gian được chỉ định (tính bằng giây).

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_capture:

.. rst-class:: classref-method

|void| **capture**\ (\ name\: :ref:`StringName<class_StringName>`, duration\: :ref:`float<class_float>`, trans_type\: :ref:`TransitionType<enum_Tween_TransitionType>` = 0, ease_type\: :ref:`EaseType<enum_Tween_EaseType>` = 0\ ) :ref:`🔗<class_AnimationMixer_method_capture>`

Nếu animation track được chỉ định bởi ``name`` có tùy chọn :ref:`Animation.UPDATE_CAPTURE<class_Animation_constant_UPDATE_CAPTURE>`, các giá trị hiện tại của những object được chỉ ra bởi track path sẽ được lưu dưới dạng cache. Nếu đã có cache được capture, cache cũ sẽ bị loại bỏ.

Sau đó, nó sẽ nội suy với kết quả blending animation hiện tại trong quá trình playback trong khoảng thời gian được chỉ định bởi ``duration``, hoạt động giống như crossfade.

Bạn có thể chỉ định ``trans_type`` làm curve cho phép nội suy. Để đạt kết quả tốt hơn, có thể nên chỉ định :ref:`Tween.TRANS_LINEAR<class_Tween_constant_TRANS_LINEAR>` trong các trường hợp key đầu tiên của track bắt đầu bằng giá trị khác không hoặc khi giá trị key không thay đổi, và :ref:`Tween.TRANS_QUAD<class_Tween_constant_TRANS_QUAD>` trong các trường hợp giá trị key thay đổi tuyến tính.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_clear_caches:

.. rst-class:: classref-method

|void| **clear_caches**\ (\ ) :ref:`🔗<class_AnimationMixer_method_clear_caches>`

**AnimationMixer** lưu cache các node được animation điều khiển. Nó có thể không nhận thấy khi một node biến mất; :ref:`clear_caches()<class_AnimationMixer_method_clear_caches>` buộc nó cập nhật cache lại.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_find_animation:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **find_animation**\ (\ animation\: :ref:`Animation<class_Animation>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_find_animation>`

Trả về key của ``animation`` hoặc một :ref:`StringName<class_StringName>` rỗng nếu không tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_find_animation_library:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **find_animation_library**\ (\ animation\: :ref:`Animation<class_Animation>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_find_animation_library>`

Trả về key của :ref:`AnimationLibrary<class_AnimationLibrary>` chứa ``animation`` hoặc một :ref:`StringName<class_StringName>` rỗng nếu không tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_animation:

.. rst-class:: classref-method

:ref:`Animation<class_Animation>` **get_animation**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_animation>`

Trả về :ref:`Animation<class_Animation>` có key ``name``. Nếu animation không tồn tại, ``null`` được trả về và một lỗi được ghi vào log.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_animation_library:

.. rst-class:: classref-method

:ref:`AnimationLibrary<class_AnimationLibrary>` **get_animation_library**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_animation_library>`

Trả về :ref:`AnimationLibrary<class_AnimationLibrary>` đầu tiên có key ``name`` hoặc ``null`` nếu không tìm thấy.

Để lấy global animation library của **AnimationMixer**, hãy sử dụng ``get_animation_library("")``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_animation_library_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_animation_library_list**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_animation_library_list>`

Trả về danh sách các library key đã lưu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_animation_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_animation_list**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_animation_list>`

Trả về danh sách các animation key đã lưu.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_root_motion_position**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_position>`

Lấy motion delta của position với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Vector3<class_Vector3>` có thể được sử dụng ở nơi khác.

Nếu :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` không phải là path đến một track có kiểu :ref:`Animation.TYPE_POSITION_3D<class_Animation_constant_TYPE_POSITION_3D>`, trả về ``Vector3(0, 0, 0)``.

Xem thêm :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` và :ref:`RootMotionView<class_RootMotionView>`.

Ví dụ cơ bản nhất là áp dụng position cho :ref:`CharacterBody3D<class_CharacterBody3D>`:


.. tabs::

 .. code-tab:: gdscript

    var current_rotation

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            current_rotation = get_quaternion()
            state_machine.travel("Animate")
        var velocity = current_rotation * animation_tree.get_root_motion_position() / delta
        set_velocity(velocity)
        move_and_slide()



Bằng cách sử dụng kết hợp với :ref:`get_root_motion_rotation_accumulator()<class_AnimationMixer_method_get_root_motion_rotation_accumulator>`, bạn có thể áp dụng root motion position chính xác hơn để tính đến rotation của node.


.. tabs::

 .. code-tab:: gdscript

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        set_quaternion(get_quaternion() * animation_tree.get_root_motion_rotation())
        var velocity = (animation_tree.get_root_motion_rotation_accumulator().inverse() * get_quaternion()) * animation_tree.get_root_motion_position() / delta
        set_velocity(velocity)
        move_and_slide()



Nếu :ref:`root_motion_local<class_AnimationMixer_property_root_motion_local>` là ``true``, trả về giá trị translation đã được nhân trước với rotation nghịch đảo.

Trong trường hợp này, code có thể được viết như sau:


.. tabs::

 .. code-tab:: gdscript

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        set_quaternion(get_quaternion() * animation_tree.get_root_motion_rotation())
        var velocity = get_quaternion() * animation_tree.get_root_motion_position() / delta
        set_velocity(velocity)
        move_and_slide()



.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_position_accumulator:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_root_motion_position_accumulator**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_position_accumulator>`

Lấy giá trị blended của các position track với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Vector3<class_Vector3>` có thể được sử dụng ở nơi khác.

Điều này hữu ích trong các trường hợp bạn muốn tôn trọng các giá trị key ban đầu của animation.

Ví dụ, nếu một animation chỉ có một key ``Vector3(0, 0, 0)`` được phát ở frame trước đó, sau đó một animation chỉ có một key ``Vector3(1, 0, 1)`` được phát ở frame tiếp theo, độ chênh lệch có thể được tính như sau:


.. tabs::

 .. code-tab:: gdscript

    var prev_root_motion_position_accumulator

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        var current_root_motion_position_accumulator = animation_tree.get_root_motion_position_accumulator()
        var difference = current_root_motion_position_accumulator - prev_root_motion_position_accumulator
        prev_root_motion_position_accumulator = current_root_motion_position_accumulator
        transform.origin += difference



Tuy nhiên, nếu animation lặp lại, một thay đổi rời rạc ngoài ý muốn có thể xảy ra, vì vậy cách này chỉ hữu ích cho một số trường hợp sử dụng đơn giản.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_rotation:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **get_root_motion_rotation**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_rotation>`

Lấy motion delta của rotation với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Quaternion<class_Quaternion>` có thể được sử dụng ở nơi khác.

Nếu :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` không phải là path đến một track có kiểu :ref:`Animation.TYPE_ROTATION_3D<class_Animation_constant_TYPE_ROTATION_3D>`, trả về ``Quaternion(0, 0, 0, 1)``.

Xem thêm :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` và :ref:`RootMotionView<class_RootMotionView>`.

Ví dụ cơ bản nhất là áp dụng rotation cho :ref:`CharacterBody3D<class_CharacterBody3D>`:


.. tabs::

 .. code-tab:: gdscript

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        set_quaternion(get_quaternion() * animation_tree.get_root_motion_rotation())



.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_rotation_accumulator:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **get_root_motion_rotation_accumulator**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_rotation_accumulator>`

Lấy giá trị blended của các rotation track với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Quaternion<class_Quaternion>` có thể được sử dụng ở nơi khác.

Điều này cần thiết để áp dụng root motion position chính xác, có tính đến rotation. Xem thêm :ref:`get_root_motion_position()<class_AnimationMixer_method_get_root_motion_position>`.

Ngoài ra, cách này hữu ích trong các trường hợp bạn muốn tôn trọng các giá trị key ban đầu của animation.

Ví dụ, nếu một animation chỉ có một key ``Quaternion(0, 0, 0, 1)`` được phát ở frame trước đó, sau đó một animation chỉ có một key ``Quaternion(0, 0.707, 0, 0.707)`` được phát ở frame tiếp theo, độ chênh lệch có thể được tính như sau:


.. tabs::

 .. code-tab:: gdscript

    var prev_root_motion_rotation_accumulator

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        var current_root_motion_rotation_accumulator = animation_tree.get_root_motion_rotation_accumulator()
        var difference = prev_root_motion_rotation_accumulator.inverse() * current_root_motion_rotation_accumulator
        prev_root_motion_rotation_accumulator = current_root_motion_rotation_accumulator
        transform.basis *=  Basis(difference)



Tuy nhiên, nếu animation lặp lại, một thay đổi rời rạc ngoài ý muốn có thể xảy ra, vì vậy cách này chỉ hữu ích cho một số trường hợp sử dụng đơn giản.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_scale:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_root_motion_scale**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_scale>`

Lấy motion delta của scale với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Vector3<class_Vector3>` có thể được sử dụng ở nơi khác.

Nếu :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` không phải là path đến một track có kiểu :ref:`Animation.TYPE_SCALE_3D<class_Animation_constant_TYPE_SCALE_3D>`, trả về ``Vector3(0, 0, 0)``.

Xem thêm :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` và :ref:`RootMotionView<class_RootMotionView>`.

Ví dụ cơ bản nhất là áp dụng scale cho :ref:`CharacterBody3D<class_CharacterBody3D>`:


.. tabs::

 .. code-tab:: gdscript

    var current_scale = Vector3(1, 1, 1)
    var scale_accum = Vector3(1, 1, 1)

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            current_scale = get_scale()
            scale_accum = Vector3(1, 1, 1)
            state_machine.travel("Animate")
        scale_accum += animation_tree.get_root_motion_scale()
        set_scale(current_scale * scale_accum)



.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_get_root_motion_scale_accumulator:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_root_motion_scale_accumulator**\ (\ ) |const| :ref:`🔗<class_AnimationMixer_method_get_root_motion_scale_accumulator>`

Lấy giá trị blended của các scale track với :ref:`root_motion_track<class_AnimationMixer_property_root_motion_track>` dưới dạng :ref:`Vector3<class_Vector3>` có thể được sử dụng ở nơi khác.

Ví dụ, nếu một animation chỉ có một key ``Vector3(1, 1, 1)`` được phát ở frame trước đó, sau đó một animation chỉ có một key ``Vector3(2, 2, 2)`` được phát ở frame tiếp theo, độ chênh lệch có thể được tính như sau:


.. tabs::

 .. code-tab:: gdscript

    var prev_root_motion_scale_accumulator

    func _process(delta):
        if Input.is_action_just_pressed("animate"):
            state_machine.travel("Animate")
        var current_root_motion_scale_accumulator = animation_tree.get_root_motion_scale_accumulator()
        var difference = current_root_motion_scale_accumulator - prev_root_motion_scale_accumulator
        prev_root_motion_scale_accumulator = current_root_motion_scale_accumulator
        transform.basis = transform.basis.scaled(difference)



Tuy nhiên, nếu animation lặp lại, một thay đổi rời rạc ngoài ý muốn có thể xảy ra, vì vậy cách này chỉ hữu ích cho một số trường hợp sử dụng đơn giản.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_has_animation:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_animation**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_has_animation>`

Trả về ``true`` nếu **AnimationMixer** lưu một :ref:`Animation<class_Animation>` với key ``name``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_has_animation_library:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_animation_library**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AnimationMixer_method_has_animation_library>`

Trả về ``true`` nếu **AnimationMixer** lưu một :ref:`AnimationLibrary<class_AnimationLibrary>` với key ``name``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_remove_animation_library:

.. rst-class:: classref-method

|void| **remove_animation_library**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationMixer_method_remove_animation_library>`

Xóa :ref:`AnimationLibrary<class_AnimationLibrary>` được liên kết với key ``name``.

.. rst-class:: classref-item-separator

----

.. _class_AnimationMixer_method_rename_animation_library:

.. rst-class:: classref-method

|void| **rename_animation_library**\ (\ name\: :ref:`StringName<class_StringName>`, newname\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AnimationMixer_method_rename_animation_library>`

Di chuyển :ref:`AnimationLibrary<class_AnimationLibrary>` được liên kết với key ``name`` sang key ``newname``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
