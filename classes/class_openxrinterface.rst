:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRInterface.xml.

.. _class_OpenXRInterface:

OpenXRInterface
===============

**Kế thừa:** :ref:`XRInterface<class_XRInterface>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Interface OpenXR của chúng ta.

.. rst-class:: classref-introduction-group

Mô tả
-----

Interface OpenXR cho phép Godot tương tác với các OpenXR runtime và giúp bạn tạo các trải nghiệm cũng như game XR.

Do các yêu cầu của OpenXR, interface này hoạt động hơi khác so với các interface XR dựa trên plugin khác. Interface này cần được khởi tạo khi Godot khởi động. Bạn cần bật OpenXR; các thiết lập cho việc này có thể tìm thấy trong project settings của game, bên dưới mục XR. Bạn cũng cần đánh dấu một viewport để sử dụng với XR, để Godot biết kết quả render nào cần được xuất ra headset.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Thiết lập XR <../tutorials/xr/setting_up_xr>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`display_refresh_rate<class_OpenXRInterface_property_display_refresh_rate>`                         | ``0.0``   |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`foveation_dynamic<class_OpenXRInterface_property_foveation_dynamic>`                               | ``false`` |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`     | :ref:`foveation_level<class_OpenXRInterface_property_foveation_level>`                                   | ``0``     |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`foveation_with_subsampled_images<class_OpenXRInterface_property_foveation_with_subsampled_images>` | ``false`` |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`render_target_size_multiplier<class_OpenXRInterface_property_render_target_size_multiplier>`       | ``1.0``   |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`vrs_min_radius<class_OpenXRInterface_property_vrs_min_radius>`                                     | ``20.0``  |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`vrs_strength<class_OpenXRInterface_property_vrs_strength>`                                         | ``1.0``   |
   +---------------------------+----------------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                | :ref:`get_action_sets<class_OpenXRInterface_method_get_action_sets>`\ (\ ) |const|                                                                                                                                            |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                | :ref:`get_available_display_refresh_rates<class_OpenXRInterface_method_get_available_display_refresh_rates>`\ (\ ) |const|                                                                                                    |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                            | :ref:`get_hand_joint_angular_velocity<class_OpenXRInterface_method_get_hand_joint_angular_velocity>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>`\] | :ref:`get_hand_joint_flags<class_OpenXRInterface_method_get_hand_joint_flags>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const|                       |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                            | :ref:`get_hand_joint_linear_velocity<class_OpenXRInterface_method_get_hand_joint_linear_velocity>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const|   |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                            | :ref:`get_hand_joint_position<class_OpenXRInterface_method_get_hand_joint_position>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const|                 |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                | :ref:`get_hand_joint_radius<class_OpenXRInterface_method_get_hand_joint_radius>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const|                     |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`                                      | :ref:`get_hand_joint_rotation<class_OpenXRInterface_method_get_hand_joint_rotation>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const|                 |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>`         | :ref:`get_hand_tracking_source<class_OpenXRInterface_method_get_hand_tracking_source>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`\ ) |const|                                                                           |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>`             | :ref:`get_motion_range<class_OpenXRInterface_method_get_motion_range>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`\ ) |const|                                                                                           |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SessionState<enum_OpenXRInterface_SessionState>`                   | :ref:`get_session_state<class_OpenXRInterface_method_get_session_state>`\ (\ )                                                                                                                                                |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_action_set_active<class_OpenXRInterface_method_is_action_set_active>`\ (\ name\: :ref:`String<class_String>`\ ) |const|                                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_eye_gaze_interaction_supported<class_OpenXRInterface_method_is_eye_gaze_interaction_supported>`\ (\ )                                                                                                                |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_foveation_supported<class_OpenXRInterface_method_is_foveation_supported>`\ (\ ) |const|                                                                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_hand_interaction_supported<class_OpenXRInterface_method_is_hand_interaction_supported>`\ (\ ) |const|                                                                                                                |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_hand_tracking_supported<class_OpenXRInterface_method_is_hand_tracking_supported>`\ (\ )                                                                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_user_presence_supported<class_OpenXRInterface_method_is_user_presence_supported>`\ (\ ) |const|                                                                                                                      |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                  | :ref:`is_user_present<class_OpenXRInterface_method_is_user_present>`\ (\ ) |const|                                                                                                                                            |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`set_action_set_active<class_OpenXRInterface_method_set_action_set_active>`\ (\ name\: :ref:`String<class_String>`, active\: :ref:`bool<class_bool>`\ )                                                                  |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`set_cpu_level<class_OpenXRInterface_method_set_cpu_level>`\ (\ level\: :ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>`\ )                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`set_gpu_level<class_OpenXRInterface_method_set_gpu_level>`\ (\ level\: :ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>`\ )                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`set_motion_range<class_OpenXRInterface_method_set_motion_range>`\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, motion_range\: :ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>`\ )                      |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_OpenXRInterface_signal_cpu_level_changed:

.. rst-class:: classref-signal

**cpu_level_changed**\ (\ sub_domain\: :ref:`int<class_int>`, from_level\: :ref:`int<class_int>`, to_level\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRInterface_signal_cpu_level_changed>`

Thông báo rằng mức hiệu năng CPU của thiết bị đã thay đổi trong subdomain được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_gpu_level_changed:

.. rst-class:: classref-signal

**gpu_level_changed**\ (\ sub_domain\: :ref:`int<class_int>`, from_level\: :ref:`int<class_int>`, to_level\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRInterface_signal_gpu_level_changed>`

Thông báo rằng mức hiệu năng GPU của thiết bị đã thay đổi trong subdomain được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_instance_exiting:

.. rst-class:: classref-signal

**instance_exiting**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_instance_exiting>`

Thông báo rằng OpenXR instance của chúng ta đang thoát.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_pose_recentered:

.. rst-class:: classref-signal

**pose_recentered**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_pose_recentered>`

Thông báo rằng người dùng đã yêu cầu căn giữa lại vị trí của người chơi.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_refresh_rate_changed:

.. rst-class:: classref-signal

**refresh_rate_changed**\ (\ refresh_rate\: :ref:`float<class_float>`\ ) :ref:`🔗<class_OpenXRInterface_signal_refresh_rate_changed>`

Thông báo rằng refresh rate của HMD đã thay đổi.

\ **Lưu ý:** Chỉ được phát ra nếu XR runtime hỗ trợ extension refresh rate.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_begun:

.. rst-class:: classref-signal

**session_begun**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_begun>`

Thông báo rằng OpenXR session của chúng ta đã được bắt đầu.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_focussed:

.. rst-class:: classref-signal

**session_focussed**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_focussed>`

Thông báo rằng OpenXR session của chúng ta hiện đã có focus, chẳng hạn output được gửi đến HMD và chúng ta đang nhận XR input.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_loss_pending:

.. rst-class:: classref-signal

**session_loss_pending**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_loss_pending>`

Thông báo rằng OpenXR session của chúng ta đang trong quá trình bị mất.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_stopping:

.. rst-class:: classref-signal

**session_stopping**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_stopping>`

Thông báo rằng OpenXR session của chúng ta đang dừng.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_synchronized:

.. rst-class:: classref-signal

**session_synchronized**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_synchronized>`

Thông báo rằng OpenXR session của chúng ta đã được đồng bộ hóa.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_session_visible:

.. rst-class:: classref-signal

**session_visible**\ (\ ) :ref:`🔗<class_OpenXRInterface_signal_session_visible>`

Thông báo rằng OpenXR session của chúng ta hiện đã hiển thị, chẳng hạn output được gửi đến HMD nhưng chúng ta không nhận XR input.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_signal_user_presence_changed:

.. rst-class:: classref-signal

**user_presence_changed**\ (\ is_user_present\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_OpenXRInterface_signal_user_presence_changed>`

Signal được phát ra khi giá trị hiện diện của người dùng thay đổi.

\ **Lưu ý:** Signal này sẽ không được phát ra trong quá trình khởi động và tắt ứng dụng. Developer nên giả định rằng người dùng hiện diện khi khởi động và không còn hiện diện khi tắt ứng dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_OpenXRInterface_SessionState:

.. rst-class:: classref-enumeration

enum **SessionState**: :ref:`🔗<enum_OpenXRInterface_SessionState>`

.. _class_OpenXRInterface_constant_SESSION_STATE_UNKNOWN:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_UNKNOWN** = ``0``

Trạng thái của session chưa xác định; chúng ta vẫn chưa thử thiết lập OpenXR.

.. _class_OpenXRInterface_constant_SESSION_STATE_IDLE:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_IDLE** = ``1``

Trạng thái ban đầu sau khi OpenXR session được tạo hoặc sau khi session bị hủy.

.. _class_OpenXRInterface_constant_SESSION_STATE_READY:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_READY** = ``2``

OpenXR đã sẵn sàng bắt đầu session của chúng ta. :ref:`session_begun<class_OpenXRInterface_signal_session_begun>` được phát ra khi chúng ta chuyển sang trạng thái này.

.. _class_OpenXRInterface_constant_SESSION_STATE_SYNCHRONIZED:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_SYNCHRONIZED** = ``3``

Ứng dụng đã đồng bộ vòng lặp frame với runtime nhưng chúng ta chưa render gì. :ref:`session_synchronized<class_OpenXRInterface_signal_session_synchronized>` được phát ra khi chúng ta chuyển sang trạng thái này.

.. _class_OpenXRInterface_constant_SESSION_STATE_VISIBLE:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_VISIBLE** = ``4``

Ứng dụng đã đồng bộ vòng lặp frame với runtime và đang render output cho người dùng, tuy nhiên chúng ta không nhận được input của người dùng. :ref:`session_visible<class_OpenXRInterface_signal_session_visible>` được phát ra khi chúng ta chuyển sang trạng thái này.

\ **Lưu ý:** Đây là trạng thái hiện tại ngay trước khi chuyển sang trạng thái focused, bất cứ khi nào người dùng mở menu hệ thống, chuyển sang ứng dụng khác hoặc tháo headset.

.. _class_OpenXRInterface_constant_SESSION_STATE_FOCUSED:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_FOCUSED** = ``5``

Ứng dụng đã đồng bộ vòng lặp frame với runtime, đang render output cho người dùng và đang nhận XR input. :ref:`session_focussed<class_OpenXRInterface_signal_session_focussed>` được phát ra khi chúng ta chuyển sang trạng thái này.

\ **Lưu ý:** Đây là trạng thái OpenXR sẽ ở vào khi người dùng có thể tương tác đầy đủ với game của bạn.

.. _class_OpenXRInterface_constant_SESSION_STATE_STOPPING:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_STOPPING** = ``6``

Session của chúng ta đang được dừng. :ref:`session_stopping<class_OpenXRInterface_signal_session_stopping>` được phát ra khi chúng ta chuyển sang trạng thái này.

.. _class_OpenXRInterface_constant_SESSION_STATE_LOSS_PENDING:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_LOSS_PENDING** = ``7``

Session sắp bị mất. :ref:`session_loss_pending<class_OpenXRInterface_signal_session_loss_pending>` được phát ra khi chúng ta chuyển sang trạng thái này.

.. _class_OpenXRInterface_constant_SESSION_STATE_EXITING:

.. rst-class:: classref-enumeration-constant

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **SESSION_STATE_EXITING** = ``8``

OpenXR instance sắp bị hủy và chúng ta đang thoát. :ref:`instance_exiting<class_OpenXRInterface_signal_instance_exiting>` được phát ra khi chúng ta chuyển sang trạng thái này.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_Hand:

.. rst-class:: classref-enumeration

enum **Hand**: :ref:`🔗<enum_OpenXRInterface_Hand>`

.. _class_OpenXRInterface_constant_HAND_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`Hand<enum_OpenXRInterface_Hand>` **HAND_LEFT** = ``0``

Bàn tay trái.

.. _class_OpenXRInterface_constant_HAND_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`Hand<enum_OpenXRInterface_Hand>` **HAND_RIGHT** = ``1``

Bàn tay phải.

.. _class_OpenXRInterface_constant_HAND_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Hand<enum_OpenXRInterface_Hand>` **HAND_MAX** = ``2``

Giá trị tối đa của enum hand.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_HandMotionRange:

.. rst-class:: classref-enumeration

enum **HandMotionRange**: :ref:`🔗<enum_OpenXRInterface_HandMotionRange>`

.. _class_OpenXRInterface_constant_HAND_MOTION_RANGE_UNOBSTRUCTED:

.. rst-class:: classref-enumeration-constant

:ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>` **HAND_MOTION_RANGE_UNOBSTRUCTED** = ``0``

Phạm vi đầy đủ của bàn tay; nếu người dùng nắm tay, chúng ta tạo thành nắm đấm hoàn chỉnh.

.. _class_OpenXRInterface_constant_HAND_MOTION_RANGE_CONFORM_TO_CONTROLLER:

.. rst-class:: classref-enumeration-constant

:ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>` **HAND_MOTION_RANGE_CONFORM_TO_CONTROLLER** = ``1``

Tuân theo controller; nếu người dùng nắm tay, dữ liệu được tracking sẽ tuân theo hình dạng của controller.

.. _class_OpenXRInterface_constant_HAND_MOTION_RANGE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>` **HAND_MOTION_RANGE_MAX** = ``2``

Giá trị tối đa của enum motion range.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_HandTrackedSource:

.. rst-class:: classref-enumeration

enum **HandTrackedSource**: :ref:`🔗<enum_OpenXRInterface_HandTrackedSource>`

.. _class_OpenXRInterface_constant_HAND_TRACKED_SOURCE_UNKNOWN:

.. rst-class:: classref-enumeration-constant

:ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>` **HAND_TRACKED_SOURCE_UNKNOWN** = ``0``

Nguồn dữ liệu hand tracking chưa xác định (extension có thể không được hỗ trợ).

.. _class_OpenXRInterface_constant_HAND_TRACKED_SOURCE_UNOBSTRUCTED:

.. rst-class:: classref-enumeration-constant

:ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>` **HAND_TRACKED_SOURCE_UNOBSTRUCTED** = ``1``

Nguồn hand tracking không bị cản trở; điều này có nghĩa là một phương pháp hand tracking chính xác được sử dụng, ví dụ như optical hand tracking, găng tay dữ liệu, v.v.

.. _class_OpenXRInterface_constant_HAND_TRACKED_SOURCE_CONTROLLER:

.. rst-class:: classref-enumeration-constant

:ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>` **HAND_TRACKED_SOURCE_CONTROLLER** = ``2``

Nguồn hand tracking là một controller; vị trí các bone được suy ra từ input của controller.

.. _class_OpenXRInterface_constant_HAND_TRACKED_SOURCE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>` **HAND_TRACKED_SOURCE_MAX** = ``3``

Biểu thị kích thước của enum :ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>`.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_HandJoints:

.. rst-class:: classref-enumeration

enum **HandJoints**: :ref:`🔗<enum_OpenXRInterface_HandJoints>`

.. _class_OpenXRInterface_constant_HAND_JOINT_PALM:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_PALM** = ``0``

Khớp lòng bàn tay.

.. _class_OpenXRInterface_constant_HAND_JOINT_WRIST:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_WRIST** = ``1``

Khớp cổ tay.

.. _class_OpenXRInterface_constant_HAND_JOINT_THUMB_METACARPAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_THUMB_METACARPAL** = ``2``

Khớp xương bàn của ngón cái.

.. _class_OpenXRInterface_constant_HAND_JOINT_THUMB_PROXIMAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_THUMB_PROXIMAL** = ``3``

Khớp đốt gần của ngón cái.

.. _class_OpenXRInterface_constant_HAND_JOINT_THUMB_DISTAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_THUMB_DISTAL** = ``4``

Khớp đốt xa của ngón cái.

.. _class_OpenXRInterface_constant_HAND_JOINT_THUMB_TIP:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_THUMB_TIP** = ``5``

Khớp đầu ngón cái.

.. _class_OpenXRInterface_constant_HAND_JOINT_INDEX_METACARPAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_INDEX_METACARPAL** = ``6``

Khớp xương bàn của ngón trỏ.

.. _class_OpenXRInterface_constant_HAND_JOINT_INDEX_PROXIMAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_INDEX_PROXIMAL** = ``7``

Khớp đốt gần của ngón trỏ.

.. _class_OpenXRInterface_constant_HAND_JOINT_INDEX_INTERMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_INDEX_INTERMEDIATE** = ``8``

Khớp đốt giữa của ngón trỏ.

.. _class_OpenXRInterface_constant_HAND_JOINT_INDEX_DISTAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_INDEX_DISTAL** = ``9``

Khớp đốt xa của ngón trỏ.

.. _class_OpenXRInterface_constant_HAND_JOINT_INDEX_TIP:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_INDEX_TIP** = ``10``

Khớp đầu ngón trỏ.

.. _class_OpenXRInterface_constant_HAND_JOINT_MIDDLE_METACARPAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MIDDLE_METACARPAL** = ``11``

Khớp xương bàn của ngón giữa.

.. _class_OpenXRInterface_constant_HAND_JOINT_MIDDLE_PROXIMAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MIDDLE_PROXIMAL** = ``12``

Khớp đốt gần của ngón giữa.

.. _class_OpenXRInterface_constant_HAND_JOINT_MIDDLE_INTERMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MIDDLE_INTERMEDIATE** = ``13``

Khớp giữa của đốt ngón tay giữa.

.. _class_OpenXRInterface_constant_HAND_JOINT_MIDDLE_DISTAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MIDDLE_DISTAL** = ``14``

Khớp xa của đốt ngón tay giữa.

.. _class_OpenXRInterface_constant_HAND_JOINT_MIDDLE_TIP:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MIDDLE_TIP** = ``15``

Khớp đầu ngón tay giữa.

.. _class_OpenXRInterface_constant_HAND_JOINT_RING_METACARPAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_RING_METACARPAL** = ``16``

Khớp xương bàn tay của ngón áp út.

.. _class_OpenXRInterface_constant_HAND_JOINT_RING_PROXIMAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_RING_PROXIMAL** = ``17``

Khớp gần của đốt ngón tay áp út.

.. _class_OpenXRInterface_constant_HAND_JOINT_RING_INTERMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_RING_INTERMEDIATE** = ``18``

Khớp giữa của đốt ngón tay áp út.

.. _class_OpenXRInterface_constant_HAND_JOINT_RING_DISTAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_RING_DISTAL** = ``19``

Khớp xa của đốt ngón tay áp út.

.. _class_OpenXRInterface_constant_HAND_JOINT_RING_TIP:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_RING_TIP** = ``20``

Khớp đầu ngón tay áp út.

.. _class_OpenXRInterface_constant_HAND_JOINT_LITTLE_METACARPAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_LITTLE_METACARPAL** = ``21``

Khớp xương bàn tay của ngón út.

.. _class_OpenXRInterface_constant_HAND_JOINT_LITTLE_PROXIMAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_LITTLE_PROXIMAL** = ``22``

Khớp gần của đốt ngón tay út.

.. _class_OpenXRInterface_constant_HAND_JOINT_LITTLE_INTERMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_LITTLE_INTERMEDIATE** = ``23``

Khớp giữa của đốt ngón tay út.

.. _class_OpenXRInterface_constant_HAND_JOINT_LITTLE_DISTAL:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_LITTLE_DISTAL** = ``24``

Khớp xa của đốt ngón tay út.

.. _class_OpenXRInterface_constant_HAND_JOINT_LITTLE_TIP:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_LITTLE_TIP** = ``25``

Khớp đầu ngón tay út.

.. _class_OpenXRInterface_constant_HAND_JOINT_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`HandJoints<enum_OpenXRInterface_HandJoints>` **HAND_JOINT_MAX** = ``26``

Biểu thị kích thước của enum :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_PerfSettingsLevel:

.. rst-class:: classref-enumeration

enum **PerfSettingsLevel**: :ref:`🔗<enum_OpenXRInterface_PerfSettingsLevel>`

.. _class_OpenXRInterface_constant_PERF_SETTINGS_LEVEL_POWER_SAVINGS:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>` **PERF_SETTINGS_LEVEL_POWER_SAVINGS** = ``0``

Ứng dụng đã chuyển sang một phần không phải XR (head-locked / màn hình tĩnh), trong đó cần ưu tiên tiết kiệm điện năng.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_LEVEL_SUSTAINED_LOW:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>` **PERF_SETTINGS_LEVEL_SUSTAINED_LOW** = ``1``

Ứng dụng đã chuyển sang một phần có độ phức tạp thấp và ổn định, trong đó việc giảm mức tiêu thụ điện quan trọng hơn so với việc thỉnh thoảng kết xuất khung hình trễ.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_LEVEL_SUSTAINED_HIGH:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>` **PERF_SETTINGS_LEVEL_SUSTAINED_HIGH** = ``2``

Ứng dụng đã chuyển sang một phần có độ phức tạp cao hoặc động, trong đó XR Runtime cố gắng duy trì việc compositing XR và kết xuất khung hình nhất quán trong phạm vi có thể duy trì về nhiệt.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_LEVEL_BOOST:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>` **PERF_SETTINGS_LEVEL_BOOST** = ``3``

Ứng dụng đã chuyển sang một phần có độ phức tạp rất cao, trong đó XR Runtime được phép tăng mức hoạt động vượt quá phạm vi có thể duy trì về nhiệt.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_PerfSettingsSubDomain:

.. rst-class:: classref-enumeration

enum **PerfSettingsSubDomain**: :ref:`🔗<enum_OpenXRInterface_PerfSettingsSubDomain>`

.. _class_OpenXRInterface_constant_PERF_SETTINGS_SUB_DOMAIN_COMPOSITING:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsSubDomain<enum_OpenXRInterface_PerfSettingsSubDomain>` **PERF_SETTINGS_SUB_DOMAIN_COMPOSITING** = ``0``

Hiệu năng compositing trong runtime đã đạt đến một cấp độ mới.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_SUB_DOMAIN_RENDERING:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsSubDomain<enum_OpenXRInterface_PerfSettingsSubDomain>` **PERF_SETTINGS_SUB_DOMAIN_RENDERING** = ``1``

Hiệu năng kết xuất của ứng dụng đã đạt đến một cấp độ mới.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_SUB_DOMAIN_THERMAL:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsSubDomain<enum_OpenXRInterface_PerfSettingsSubDomain>` **PERF_SETTINGS_SUB_DOMAIN_THERMAL** = ``2``

Nhiệt độ của thiết bị đã đạt đến một cấp độ mới.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_PerfSettingsNotificationLevel:

.. rst-class:: classref-enumeration

enum **PerfSettingsNotificationLevel**: :ref:`🔗<enum_OpenXRInterface_PerfSettingsNotificationLevel>`

.. _class_OpenXRInterface_constant_PERF_SETTINGS_NOTIF_LEVEL_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsNotificationLevel<enum_OpenXRInterface_PerfSettingsNotificationLevel>` **PERF_SETTINGS_NOTIF_LEVEL_NORMAL** = ``0``

Miền con đã đạt đến một cấp độ mà không cần thực hiện thêm hành động nào ngoài các hành động hiện đang được áp dụng.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_NOTIF_LEVEL_WARNING:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsNotificationLevel<enum_OpenXRInterface_PerfSettingsNotificationLevel>` **PERF_SETTINGS_NOTIF_LEVEL_WARNING** = ``1``

Miền con đã đạt đến cấp độ cảnh báo sớm, tại đó ứng dụng nên bắt đầu các hành động giảm thiểu chủ động.

.. _class_OpenXRInterface_constant_PERF_SETTINGS_NOTIF_LEVEL_IMPAIRED:

.. rst-class:: classref-enumeration-constant

:ref:`PerfSettingsNotificationLevel<enum_OpenXRInterface_PerfSettingsNotificationLevel>` **PERF_SETTINGS_NOTIF_LEVEL_IMPAIRED** = ``2``

Miền con đã đạt đến cấp độ nghiêm trọng, tại đó ứng dụng nên bắt đầu các hành động giảm thiểu mạnh mẽ.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRInterface_HandJointFlags:

.. rst-class:: classref-enumeration

flags **HandJointFlags**: :ref:`🔗<enum_OpenXRInterface_HandJointFlags>`

.. _class_OpenXRInterface_constant_HAND_JOINT_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_NONE** = ``0``

Không có flag nào được thiết lập.

.. _class_OpenXRInterface_constant_HAND_JOINT_ORIENTATION_VALID:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_ORIENTATION_VALID** = ``1``

Nếu được thiết lập, dữ liệu hướng là hợp lệ; nếu không, dữ liệu hướng không đáng tin cậy và không nên được sử dụng.

.. _class_OpenXRInterface_constant_HAND_JOINT_ORIENTATION_TRACKED:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_ORIENTATION_TRACKED** = ``2``

Nếu được thiết lập, dữ liệu hướng đến từ dữ liệu tracking; nếu không, dữ liệu hướng chứa dữ liệu dự đoán.

.. _class_OpenXRInterface_constant_HAND_JOINT_POSITION_VALID:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_POSITION_VALID** = ``4``

Nếu được thiết lập, dữ liệu vị trí là hợp lệ; nếu không, dữ liệu vị trí không đáng tin cậy và không nên được sử dụng.

.. _class_OpenXRInterface_constant_HAND_JOINT_POSITION_TRACKED:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_POSITION_TRACKED** = ``8``

Nếu được thiết lập, dữ liệu vị trí đến từ dữ liệu tracking; nếu không, dữ liệu vị trí chứa dữ liệu dự đoán.

.. _class_OpenXRInterface_constant_HAND_JOINT_LINEAR_VELOCITY_VALID:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_LINEAR_VELOCITY_VALID** = ``16``

Nếu được thiết lập, dữ liệu vận tốc tuyến tính của chúng ta là hợp lệ; nếu không, dữ liệu vận tốc tuyến tính không đáng tin cậy và không nên được sử dụng.

.. _class_OpenXRInterface_constant_HAND_JOINT_ANGULAR_VELOCITY_VALID:

.. rst-class:: classref-enumeration-constant

:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>` **HAND_JOINT_ANGULAR_VELOCITY_VALID** = ``32``

Nếu được thiết lập, dữ liệu vận tốc góc của chúng ta là hợp lệ; nếu không, dữ liệu vận tốc góc không đáng tin cậy và không nên được sử dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRInterface_property_display_refresh_rate:

.. rst-class:: classref-property

:ref:`float<class_float>` **display_refresh_rate** = ``0.0`` :ref:`🔗<class_OpenXRInterface_property_display_refresh_rate>`

.. rst-class:: classref-property-setget

- |void| **set_display_refresh_rate**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_display_refresh_rate**\ (\ )

Tần số làm mới màn hình của HMD hiện tại. Chỉ hoạt động nếu tính năng này được OpenXR runtime hỗ trợ và sau khi interface đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_foveation_dynamic:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **foveation_dynamic** = ``false`` :ref:`🔗<class_OpenXRInterface_property_foveation_dynamic>`

.. rst-class:: classref-property-setget

- |void| **set_foveation_dynamic**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_foveation_dynamic**\ (\ )

Nếu ``true``, bật điều chỉnh foveation động. Interface phải được khởi tạo trước khi có thể truy cập thuộc tính này. Nếu được bật, foveation sẽ tự động được điều chỉnh giữa mức thấp và :ref:`foveation_level<class_OpenXRInterface_property_foveation_level>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_foveation_level:

.. rst-class:: classref-property

:ref:`int<class_int>` **foveation_level** = ``0`` :ref:`🔗<class_OpenXRInterface_property_foveation_level>`

.. rst-class:: classref-property-setget

- |void| **set_foveation_level**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_foveation_level**\ (\ )

Mức foveation, từ ``0`` (tắt) đến ``3`` (cao). Interface phải được khởi tạo trước khi có thể truy cập thuộc tính này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_foveation_with_subsampled_images:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **foveation_with_subsampled_images** = ``false`` :ref:`🔗<class_OpenXRInterface_property_foveation_with_subsampled_images>`

.. rst-class:: classref-property-setget

- |void| **set_foveation_with_subsampled_images**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_foveation_with_subsampled_images**\ (\ )

Nếu ``true``, bật hình ảnh subsampled cùng với foveation, có thể cải thiện hiệu năng trên Vulkan.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_render_target_size_multiplier:

.. rst-class:: classref-property

:ref:`float<class_float>` **render_target_size_multiplier** = ``1.0`` :ref:`🔗<class_OpenXRInterface_property_render_target_size_multiplier>`

.. rst-class:: classref-property-setget

- |void| **set_render_target_size_multiplier**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_render_target_size_multiplier**\ (\ )

Hệ số nhân kích thước render của HMD hiện tại. Phải được thiết lập trước khi interface được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_vrs_min_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **vrs_min_radius** = ``20.0`` :ref:`🔗<class_OpenXRInterface_property_vrs_min_radius>`

.. rst-class:: classref-property-setget

- |void| **set_vrs_min_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_vrs_min_radius**\ (\ )

Bán kính tối thiểu quanh tiêu điểm, nơi chất lượng đầy đủ được đảm bảo nếu VRS được sử dụng theo tỷ lệ phần trăm kích thước màn hình.

\ **Lưu ý:** Chỉ dành cho Mobile và Forward+ renderer. Yêu cầu :ref:`Viewport.vrs_mode<class_Viewport_property_vrs_mode>` được thiết lập thành :ref:`Viewport.VRS_XR<class_Viewport_constant_VRS_XR>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_property_vrs_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **vrs_strength** = ``1.0`` :ref:`🔗<class_OpenXRInterface_property_vrs_strength>`

.. rst-class:: classref-property-setget

- |void| **set_vrs_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_vrs_strength**\ (\ )

Mức độ được sử dụng để tính toán density map của VRS. Giá trị này càng lớn thì VRS càng dễ nhận thấy. Điều này cải thiện hiệu năng nhưng phải đánh đổi bằng chất lượng.

\ **Lưu ý:** Chỉ dành cho Mobile và Forward+ renderer. Yêu cầu :ref:`Viewport.vrs_mode<class_Viewport_property_vrs_mode>` được thiết lập thành :ref:`Viewport.VRS_XR<class_Viewport_constant_VRS_XR>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRInterface_method_get_action_sets:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_action_sets**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_action_sets>`

Trả về danh sách các action set đã đăng ký với Godot (được tải từ action map tại runtime).

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_available_display_refresh_rates:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_available_display_refresh_rates**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_available_display_refresh_rates>`

Trả về danh sách các tần số làm mới màn hình được HMD hiện tại hỗ trợ. Chỉ được trả về nếu tính năng này được OpenXR runtime hỗ trợ và sau khi interface đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_angular_velocity:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_hand_joint_angular_velocity**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_angular_velocity>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_angular_velocity()<class_XRHandTracker_method_get_hand_joint_angular_velocity>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về vận tốc góc của một khớp (``joint``) của bàn tay (``hand``) do OpenXR cung cấp. Giá trị này tương đối so với :ref:`XROrigin3D<class_XROrigin3D>`!

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_flags:

.. rst-class:: classref-method

|bitfield|\[:ref:`HandJointFlags<enum_OpenXRInterface_HandJointFlags>`\] **get_hand_joint_flags**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_flags>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_flags()<class_XRHandTracker_method_get_hand_joint_flags>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về các cờ cho biết tính hợp lệ của dữ liệu tracking.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_linear_velocity:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_hand_joint_linear_velocity**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_linear_velocity>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_linear_velocity()<class_XRHandTracker_method_get_hand_joint_linear_velocity>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về vận tốc tuyến tính của một khớp (``joint``) của bàn tay (``hand``) do OpenXR cung cấp. Giá trị này tương đối so với :ref:`XROrigin3D<class_XROrigin3D>` và chưa áp dụng worldscale!

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_hand_joint_position**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_position>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_transform()<class_XRHandTracker_method_get_hand_joint_transform>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về vị trí của một khớp (``joint``) của bàn tay (``hand``) do OpenXR cung cấp. Giá trị này tương đối so với :ref:`XROrigin3D<class_XROrigin3D>` và chưa áp dụng worldscale!

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_radius:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_hand_joint_radius**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_radius>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_radius()<class_XRHandTracker_method_get_hand_joint_radius>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về bán kính của một khớp (``joint``) của bàn tay (``hand``) do OpenXR cung cấp. Giá trị này chưa áp dụng worldscale!

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_joint_rotation:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **get_hand_joint_rotation**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, joint\: :ref:`HandJoints<enum_OpenXRInterface_HandJoints>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_joint_rotation>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.get_hand_joint_transform()<class_XRHandTracker_method_get_hand_joint_transform>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật, trả về góc xoay của một khớp (``joint``) của bàn tay (``hand``) do OpenXR cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_hand_tracking_source:

.. rst-class:: classref-method

:ref:`HandTrackedSource<enum_OpenXRInterface_HandTrackedSource>` **get_hand_tracking_source**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_hand_tracking_source>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`XRHandTracker.hand_tracking_source<class_XRHandTracker_property_hand_tracking_source>` nhận được từ :ref:`XRServer.get_tracker()<class_XRServer_method_get_tracker>`.

Nếu handtracking được bật và nguồn hand tracking được hỗ trợ, lấy nguồn của dữ liệu hand tracking cho ``hand``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_motion_range:

.. rst-class:: classref-method

:ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>` **get_motion_range**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_get_motion_range>`

Nếu handtracking được bật và motion range được hỗ trợ, lấy motion range hiện được cấu hình cho ``hand``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_get_session_state:

.. rst-class:: classref-method

:ref:`SessionState<enum_OpenXRInterface_SessionState>` **get_session_state**\ (\ ) :ref:`🔗<class_OpenXRInterface_method_get_session_state>`

Trả về trạng thái hiện tại của OpenXR session.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_action_set_active:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_action_set_active**\ (\ name\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_OpenXRInterface_method_is_action_set_active>`

Trả về ``true`` nếu action set đã cho đang active.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_eye_gaze_interaction_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_eye_gaze_interaction_supported**\ (\ ) :ref:`🔗<class_OpenXRInterface_method_is_eye_gaze_interaction_supported>`

Trả về các capability của eye gaze interaction extension.

\ **Lưu ý:** Giá trị này chỉ hợp lệ sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_foveation_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_foveation_supported**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_is_foveation_supported>`

Trả về ``true`` nếu foveation extension của OpenXR được hỗ trợ. Interface phải được khởi tạo trước khi giá trị này hợp lệ.

\ **Lưu ý:** Khi sử dụng Vulkan rendering driver, :ref:`Viewport.vrs_mode<class_Viewport_property_vrs_mode>` phải được đặt thành :ref:`Viewport.VRS_XR<class_Viewport_constant_VRS_XR>` để hỗ trợ foveation.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_hand_interaction_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_hand_interaction_supported**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_is_hand_interaction_supported>`

Trả về ``true`` nếu hand interaction profile của OpenXR được hỗ trợ và bật.

\ **Lưu ý:** Giá trị này chỉ hợp lệ sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_hand_tracking_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_hand_tracking_supported**\ (\ ) :ref:`🔗<class_OpenXRInterface_method_is_hand_tracking_supported>`

Trả về ``true`` nếu hand tracking của OpenXR được hỗ trợ và bật.

\ **Lưu ý:** Giá trị này chỉ hợp lệ sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_user_presence_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_user_presence_supported**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_is_user_presence_supported>`

Trả về ``true`` nếu user presence extension của OpenXR được hỗ trợ và bật.

\ **Lưu ý:** Giá trị này chỉ hợp lệ sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_is_user_present:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_user_present**\ (\ ) |const| :ref:`🔗<class_OpenXRInterface_method_is_user_present>`

Trả về ``true`` nếu hệ thống phát hiện có người dùng trong trải nghiệm XR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_set_action_set_active:

.. rst-class:: classref-method

|void| **set_action_set_active**\ (\ name\: :ref:`String<class_String>`, active\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_OpenXRInterface_method_set_action_set_active>`

Đặt action set đã cho thành active hoặc inactive.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_set_cpu_level:

.. rst-class:: classref-method

|void| **set_cpu_level**\ (\ level\: :ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>`\ ) :ref:`🔗<class_OpenXRInterface_method_set_cpu_level>`

Đặt mức hiệu năng CPU của thiết bị OpenXR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_set_gpu_level:

.. rst-class:: classref-method

|void| **set_gpu_level**\ (\ level\: :ref:`PerfSettingsLevel<enum_OpenXRInterface_PerfSettingsLevel>`\ ) :ref:`🔗<class_OpenXRInterface_method_set_gpu_level>`

Đặt mức hiệu năng GPU của thiết bị OpenXR.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRInterface_method_set_motion_range:

.. rst-class:: classref-method

|void| **set_motion_range**\ (\ hand\: :ref:`Hand<enum_OpenXRInterface_Hand>`, motion_range\: :ref:`HandMotionRange<enum_OpenXRInterface_HandMotionRange>`\ ) :ref:`🔗<class_OpenXRInterface_method_set_motion_range>`

Nếu handtracking được bật và motion range được hỗ trợ, đặt motion range hiện được cấu hình cho ``hand`` thành ``motion_range``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
