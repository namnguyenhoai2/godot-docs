:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/interactive_music/doc_classes/AudioStreamInteractive.xml.

.. _class_AudioStreamInteractive:

AudioStreamInteractive
======================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Audio stream có thể phát nhạc tương tác, kết hợp các clip và một bảng chuyển tiếp.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một audio stream có thể phát nhạc tương tác, kết hợp các clip và một bảng chuyển tiếp. Trước tiên phải thêm các clip, sau đó cấu hình các quy tắc chuyển tiếp thông qua :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`. Ngoài ra, stream này cung cấp một thuộc tính parameter để điều khiển việc phát thông qua :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`, :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>` hoặc :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>`.

Cách sử dụng là thêm một số clip, sau đó cấu hình bảng chuyển tiếp. Từ đó, các clip được chọn để phát và nhạc sẽ chuyển mượt mà từ clip hiện tại sang clip mới bằng quy tắc chuyển tiếp tương ứng được định nghĩa trong bảng chuyển tiếp.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+-------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`clip_count<class_AudioStreamInteractive_property_clip_count>`     | ``0`` |
   +-----------------------+-------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`initial_clip<class_AudioStreamInteractive_property_initial_clip>` | ``0`` |
   +-----------------------+-------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`add_transition<class_AudioStreamInteractive_method_add_transition>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`, from_time\: :ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>`, to_time\: :ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>`, fade_mode\: :ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>`, fade_beats\: :ref:`float<class_float>`, use_filler_clip\: :ref:`bool<class_bool>` = false, filler_clip\: :ref:`int<class_int>` = -1, hold_previous\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`erase_transition<class_AudioStreamInteractive_method_erase_transition>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                                                                                                                                                              |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>`       | :ref:`get_clip_auto_advance<class_AudioStreamInteractive_method_get_clip_auto_advance>`\ (\ clip_index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`get_clip_auto_advance_next_clip<class_AudioStreamInteractive_method_get_clip_auto_advance_next_clip>`\ (\ clip_index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                        |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                       | :ref:`get_clip_name<class_AudioStreamInteractive_method_get_clip_name>`\ (\ clip_index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStream<class_AudioStream>`                                     | :ref:`get_clip_stream<class_AudioStreamInteractive_method_get_clip_stream>`\ (\ clip_index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                 | :ref:`get_transition_fade_beats<class_AudioStreamInteractive_method_get_transition_fade_beats>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                    |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>`                     | :ref:`get_transition_fade_mode<class_AudioStreamInteractive_method_get_transition_fade_mode>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                      |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                     | :ref:`get_transition_filler_clip<class_AudioStreamInteractive_method_get_transition_filler_clip>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                  |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` | :ref:`get_transition_from_time<class_AudioStreamInteractive_method_get_transition_from_time>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                      |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`                           | :ref:`get_transition_list<class_AudioStreamInteractive_method_get_transition_list>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>`     | :ref:`get_transition_to_time<class_AudioStreamInteractive_method_get_transition_to_time>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                          |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`has_transition<class_AudioStreamInteractive_method_has_transition>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                                                          |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`is_transition_holding_previous<class_AudioStreamInteractive_method_is_transition_holding_previous>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                          |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                   | :ref:`is_transition_using_filler_clip<class_AudioStreamInteractive_method_is_transition_using_filler_clip>`\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                                                                                                        |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`set_clip_auto_advance<class_AudioStreamInteractive_method_set_clip_auto_advance>`\ (\ clip_index\: :ref:`int<class_int>`, mode\: :ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>`\ )                                                                                                                                                                                                                                                                                                                                                                        |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`set_clip_auto_advance_next_clip<class_AudioStreamInteractive_method_set_clip_auto_advance_next_clip>`\ (\ clip_index\: :ref:`int<class_int>`, auto_advance_next_clip\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                                                                                                                |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`set_clip_name<class_AudioStreamInteractive_method_set_clip_name>`\ (\ clip_index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                                                                                                                                                                                                                                                                                        |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                    | :ref:`set_clip_stream<class_AudioStreamInteractive_method_set_clip_stream>`\ (\ clip_index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`\ )                                                                                                                                                                                                                                                                                                                                                                                                                |
   +---------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_AudioStreamInteractive_TransitionFromTime:

.. rst-class:: classref-enumeration

enum **TransitionFromTime**: :ref:`🔗<enum_AudioStreamInteractive_TransitionFromTime>`

.. _class_AudioStreamInteractive_constant_TRANSITION_FROM_TIME_IMMEDIATE:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` **TRANSITION_FROM_TIME_IMMEDIATE** = ``0``

Bắt đầu chuyển tiếp ngay khi có thể, không chờ đến một vị trí thời gian cụ thể.

.. _class_AudioStreamInteractive_constant_TRANSITION_FROM_TIME_NEXT_BEAT:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` **TRANSITION_FROM_TIME_NEXT_BEAT** = ``1``

Chuyển tiếp khi vị trí phát của clip đạt đến nhịp tiếp theo.

.. _class_AudioStreamInteractive_constant_TRANSITION_FROM_TIME_NEXT_BAR:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` **TRANSITION_FROM_TIME_NEXT_BAR** = ``2``

Chuyển tiếp khi vị trí phát của clip đạt đến ô nhịp tiếp theo.

.. _class_AudioStreamInteractive_constant_TRANSITION_FROM_TIME_END:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` **TRANSITION_FROM_TIME_END** = ``3``

Chuyển tiếp khi clip hiện tại phát xong.

.. rst-class:: classref-item-separator

----

.. _enum_AudioStreamInteractive_TransitionToTime:

.. rst-class:: classref-enumeration

enum **TransitionToTime**: :ref:`🔗<enum_AudioStreamInteractive_TransitionToTime>`

.. _class_AudioStreamInteractive_constant_TRANSITION_TO_TIME_SAME_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>` **TRANSITION_TO_TIME_SAME_POSITION** = ``0``

Chuyển tiếp đến cùng vị trí trong clip đích. Điều này hữu ích khi cả hai clip có cùng độ dài và nhạc cần chuyển fade giữa chúng.

.. _class_AudioStreamInteractive_constant_TRANSITION_TO_TIME_START:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>` **TRANSITION_TO_TIME_START** = ``1``

Chuyển tiếp đến phần đầu của clip đích.

.. _class_AudioStreamInteractive_constant_TRANSITION_TO_TIME_PREVIOUS_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>` **TRANSITION_TO_TIME_PREVIOUS_POSITION** = ``2``

Chuyển tiếp đến vị trí phát gần nhất trong clip đích, nếu trước đó đã có chuyển tiếp từ clip đó. Nếu không, phát từ đầu clip đích.

.. rst-class:: classref-item-separator

----

.. _enum_AudioStreamInteractive_FadeMode:

.. rst-class:: classref-enumeration

enum **FadeMode**: :ref:`🔗<enum_AudioStreamInteractive_FadeMode>`

.. _class_AudioStreamInteractive_constant_FADE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **FADE_DISABLED** = ``0``

Không sử dụng fade cho quá trình chuyển tiếp. Điều này hữu ích khi chuyển từ cuối clip sang đầu clip và mỗi clip có phần đầu/cuối tương ứng.

.. _class_AudioStreamInteractive_constant_FADE_IN:

.. rst-class:: classref-enumeration-constant

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **FADE_IN** = ``1``

Sử dụng fade-in ở clip tiếp theo, để clip hiện tại phát xong.

.. _class_AudioStreamInteractive_constant_FADE_OUT:

.. rst-class:: classref-enumeration-constant

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **FADE_OUT** = ``2``

Sử dụng fade-out ở clip hiện tại, clip tiếp theo sẽ tự bắt đầu.

.. _class_AudioStreamInteractive_constant_FADE_CROSS:

.. rst-class:: classref-enumeration-constant

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **FADE_CROSS** = ``3``

Sử dụng cross-fade giữa các clip.

.. _class_AudioStreamInteractive_constant_FADE_AUTOMATIC:

.. rst-class:: classref-enumeration-constant

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **FADE_AUTOMATIC** = ``4``

Sử dụng logic fade tự động tùy thuộc vào điểm bắt đầu/kết thúc của chuyển tiếp. Khuyến nghị sử dụng tùy chọn này theo mặc định.

.. rst-class:: classref-item-separator

----

.. _enum_AudioStreamInteractive_AutoAdvanceMode:

.. rst-class:: classref-enumeration

enum **AutoAdvanceMode**: :ref:`🔗<enum_AudioStreamInteractive_AutoAdvanceMode>`

.. _class_AudioStreamInteractive_constant_AUTO_ADVANCE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>` **AUTO_ADVANCE_DISABLED** = ``0``

Tắt auto-advance (mặc định).

.. _class_AudioStreamInteractive_constant_AUTO_ADVANCE_ENABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>` **AUTO_ADVANCE_ENABLED** = ``1``

Bật auto-advance, phải chỉ định một clip.

.. _class_AudioStreamInteractive_constant_AUTO_ADVANCE_RETURN_TO_HOLD:

.. rst-class:: classref-enumeration-constant

:ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>` **AUTO_ADVANCE_RETURN_TO_HOLD** = ``2``

Bật auto-advance, nhưng thay vì chỉ định một clip, quá trình phát sẽ quay lại trạng thái hold (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_AudioStreamInteractive_constant_CLIP_ANY:

.. rst-class:: classref-constant

**CLIP_ANY** = ``-1`` :ref:`🔗<class_AudioStreamInteractive_constant_CLIP_ANY>`

Hằng số này cho biết mọi clip đều hợp lệ cho một chuyển tiếp cụ thể, với vai trò là nguồn hoặc đích.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamInteractive_property_clip_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **clip_count** = ``0`` :ref:`🔗<class_AudioStreamInteractive_property_clip_count>`

.. rst-class:: classref-property-setget

- |void| **set_clip_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_clip_count**\ (\ )

Số lượng clip có trong interactive player này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_property_initial_clip:

.. rst-class:: classref-property

:ref:`int<class_int>` **initial_clip** = ``0`` :ref:`🔗<class_AudioStreamInteractive_property_initial_clip>`

.. rst-class:: classref-property-setget

- |void| **set_initial_clip**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_initial_clip**\ (\ )

Index của clip ban đầu, clip sẽ được phát đầu tiên khi stream này được phát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamInteractive_method_add_transition:

.. rst-class:: classref-method

|void| **add_transition**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`, from_time\: :ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>`, to_time\: :ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>`, fade_mode\: :ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>`, fade_beats\: :ref:`float<class_float>`, use_filler_clip\: :ref:`bool<class_bool>` = false, filler_clip\: :ref:`int<class_int>` = -1, hold_previous\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AudioStreamInteractive_method_add_transition>`

Thêm một chuyển tiếp giữa hai clip. Cung cấp index của clip nguồn và clip đích, hoặc sử dụng hằng số :ref:`CLIP_ANY<class_AudioStreamInteractive_constant_CLIP_ANY>` để cho biết chuyển tiếp xảy ra từ/bất kỳ clip nào đến clip này.

\* ``from_time`` cho biết thời điểm trong clip hiện tại mà chuyển tiếp sẽ bắt đầu sau khi được kích hoạt.

\* ``to_time`` cho biết thời điểm trong clip tiếp theo mà quá trình phát sẽ bắt đầu.

\* ``fade_mode`` cho biết fade giữa các clip sẽ diễn ra như thế nào. Nếu không chắc chắn, chỉ cần sử dụng :ref:`FADE_AUTOMATIC<class_AudioStreamInteractive_constant_FADE_AUTOMATIC>`, tùy chọn này sử dụng kiểu fade phổ biến nhất cho từng tình huống.

\* ``fade_beats`` cho biết fade sẽ kéo dài bao nhiêu nhịp. Cho phép sử dụng số thập phân.

\* ``use_filler_clip`` cho biết sẽ sử dụng một filler clip ở giữa clip nguồn và clip đích.

\* ``filler_clip`` index của filler clip.

\* Nếu sử dụng ``hold_previous``, clip này sẽ được ghi nhớ. Có thể dùng cùng với :ref:`AUTO_ADVANCE_RETURN_TO_HOLD<class_AudioStreamInteractive_constant_AUTO_ADVANCE_RETURN_TO_HOLD>` để quay lại clip này sau khi clip khác phát xong.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_erase_transition:

.. rst-class:: classref-method

|void| **erase_transition**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamInteractive_method_erase_transition>`

Xóa một chuyển tiếp bằng cách cung cấp index của clip ``from_clip`` và ``to_clip``. Có thể sử dụng :ref:`CLIP_ANY<class_AudioStreamInteractive_constant_CLIP_ANY>` cho một hoặc cả hai đối số.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_clip_auto_advance:

.. rst-class:: classref-method

:ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>` **get_clip_auto_advance**\ (\ clip_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_clip_auto_advance>`

Trả về việc một clip có bật auto-advance hay không. Xem :ref:`set_clip_auto_advance()<class_AudioStreamInteractive_method_set_clip_auto_advance>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_clip_auto_advance_next_clip:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_clip_auto_advance_next_clip**\ (\ clip_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_clip_auto_advance_next_clip>`

Trả về clip mà clip được tham chiếu bởi ``clip_index`` sẽ tự động chuyển đến.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_clip_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_clip_name**\ (\ clip_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_clip_name>`

Trả về tên của một clip.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_clip_stream:

.. rst-class:: classref-method

:ref:`AudioStream<class_AudioStream>` **get_clip_stream**\ (\ clip_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_clip_stream>`

Trả về :ref:`AudioStream<class_AudioStream>` liên kết với một clip.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_fade_beats:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_transition_fade_beats**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_fade_beats>`

Trả về thời gian (tính bằng nhịp) của một chuyển tiếp (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_fade_mode:

.. rst-class:: classref-method

:ref:`FadeMode<enum_AudioStreamInteractive_FadeMode>` **get_transition_fade_mode**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_fade_mode>`

Trả về mode của một chuyển tiếp (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_filler_clip:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_transition_filler_clip**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_filler_clip>`

Trả về filler clip của một chuyển tiếp (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_from_time:

.. rst-class:: classref-method

:ref:`TransitionFromTime<enum_AudioStreamInteractive_TransitionFromTime>` **get_transition_from_time**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_from_time>`

Trả về vị trí thời gian nguồn của một chuyển tiếp (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_list:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_transition_list**\ (\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_list>`

Trả về danh sách các chuyển tiếp (from, to xen kẽ).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_get_transition_to_time:

.. rst-class:: classref-method

:ref:`TransitionToTime<enum_AudioStreamInteractive_TransitionToTime>` **get_transition_to_time**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_get_transition_to_time>`

Trả về vị trí thời gian đích của một chuyển tiếp (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_has_transition:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_transition**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_has_transition>`

Trả về ``true`` nếu một chuyển tiếp đã cho tồn tại (được thêm thông qua :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_is_transition_holding_previous:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_transition_holding_previous**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_is_transition_holding_previous>`

Trả về việc một chuyển tiếp có sử dụng chức năng *hold previous* hay không (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_is_transition_using_filler_clip:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_transition_using_filler_clip**\ (\ from_clip\: :ref:`int<class_int>`, to_clip\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamInteractive_method_is_transition_using_filler_clip>`

Trả về việc một chuyển tiếp có sử dụng chức năng *filler clip* hay không (xem :ref:`add_transition()<class_AudioStreamInteractive_method_add_transition>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_set_clip_auto_advance:

.. rst-class:: classref-method

|void| **set_clip_auto_advance**\ (\ clip_index\: :ref:`int<class_int>`, mode\: :ref:`AutoAdvanceMode<enum_AudioStreamInteractive_AutoAdvanceMode>`\ ) :ref:`🔗<class_AudioStreamInteractive_method_set_clip_auto_advance>`

Thiết lập việc clip có tự động chuyển tiếp hay không bằng cách thay đổi mode auto-advance.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_set_clip_auto_advance_next_clip:

.. rst-class:: classref-method

|void| **set_clip_auto_advance_next_clip**\ (\ clip_index\: :ref:`int<class_int>`, auto_advance_next_clip\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamInteractive_method_set_clip_auto_advance_next_clip>`

Thiết lập index của clip tiếp theo mà clip này sẽ tự động chuyển đến khi phát xong. Nếu clip đang phát lặp lại, auto-advance sẽ bị bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_set_clip_name:

.. rst-class:: classref-method

|void| **set_clip_name**\ (\ clip_index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AudioStreamInteractive_method_set_clip_name>`

Thiết lập tên của clip hiện tại (để dễ nhận diện hơn).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamInteractive_method_set_clip_stream:

.. rst-class:: classref-method

|void| **set_clip_stream**\ (\ clip_index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioStreamInteractive_method_set_clip_stream>`

Thiết lập :ref:`AudioStream<class_AudioStream>` liên kết với clip hiện tại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
