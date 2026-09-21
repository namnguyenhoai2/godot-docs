:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Engine.xml.

.. _class_Engine:

Engine
======

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào các thuộc tính của engine.

.. rst-class:: classref-introduction-group

Mô tả
-----

Singleton **Engine** cho phép bạn truy vấn và sửa đổi các tham số run-time của project, chẳng hạn như số khung hình trên giây, time scale và các tham số khác. Singleton này cũng lưu trữ thông tin về bản build hiện tại của Godot, chẳng hạn như phiên bản hiện tại.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`     | :ref:`max_fps<class_Engine_property_max_fps>`                                         | ``0``    |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`     | :ref:`max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` | ``8``    |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`physics_jitter_fix<class_Engine_property_physics_jitter_fix>`                   | ``0.5``  |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`     | :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`       | ``60``   |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`print_error_messages<class_Engine_property_print_error_messages>`               | ``true`` |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`print_to_stdout<class_Engine_property_print_to_stdout>`                         | ``true`` |
   +---------------------------+---------------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`time_scale<class_Engine_property_time_scale>`                                   | ``1.0``  |
   +---------------------------+---------------------------------------------------------------------------------------+----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`ScriptBacktrace<class_ScriptBacktrace>`\] | :ref:`capture_script_backtraces<class_Engine_method_capture_script_backtraces>`\ (\ include_variables\: :ref:`bool<class_bool>` = false\ ) |const|          |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                | :ref:`get_architecture_name<class_Engine_method_get_architecture_name>`\ (\ ) |const|                                                                       |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                        | :ref:`get_author_info<class_Engine_method_get_author_info>`\ (\ ) |const|                                                                                   |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\]           | :ref:`get_copyright_info<class_Engine_method_get_copyright_info>`\ (\ ) |const|                                                                             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                        | :ref:`get_donor_info<class_Engine_method_get_donor_info>`\ (\ ) |const|                                                                                     |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`get_frames_drawn<class_Engine_method_get_frames_drawn>`\ (\ )                                                                                         |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                  | :ref:`get_frames_per_second<class_Engine_method_get_frames_per_second>`\ (\ ) |const|                                                                       |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                        | :ref:`get_license_info<class_Engine_method_get_license_info>`\ (\ ) |const|                                                                                 |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                | :ref:`get_license_text<class_Engine_method_get_license_text>`\ (\ ) |const|                                                                                 |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MainLoop<class_MainLoop>`                                            | :ref:`get_main_loop<class_Engine_method_get_main_loop>`\ (\ ) |const|                                                                                       |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`get_physics_frames<class_Engine_method_get_physics_frames>`\ (\ ) |const|                                                                             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                  | :ref:`get_physics_interpolation_fraction<class_Engine_method_get_physics_interpolation_fraction>`\ (\ ) |const|                                             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`get_process_frames<class_Engine_method_get_process_frames>`\ (\ ) |const|                                                                             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ScriptLanguage<class_ScriptLanguage>`                                | :ref:`get_script_language<class_Engine_method_get_script_language>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                            |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                      | :ref:`get_script_language_count<class_Engine_method_get_script_language_count>`\ (\ )                                                                       |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`                                                | :ref:`get_singleton<class_Engine_method_get_singleton>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                           |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                          | :ref:`get_singleton_list<class_Engine_method_get_singleton_list>`\ (\ ) |const|                                                                             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                        | :ref:`get_version_info<class_Engine_method_get_version_info>`\ (\ ) |const|                                                                                 |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                                | :ref:`get_write_movie_path<class_Engine_method_get_write_movie_path>`\ (\ ) |const|                                                                         |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`has_singleton<class_Engine_method_has_singleton>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                           |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`is_editor_hint<class_Engine_method_is_editor_hint>`\ (\ ) |const|                                                                                     |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`is_embedded_in_editor<class_Engine_method_is_embedded_in_editor>`\ (\ ) |const|                                                                       |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                    | :ref:`is_in_physics_frame<class_Engine_method_is_in_physics_frame>`\ (\ ) |const|                                                                           |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                      | :ref:`register_script_language<class_Engine_method_register_script_language>`\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`\ )                 |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                     | :ref:`register_singleton<class_Engine_method_register_singleton>`\ (\ name\: :ref:`StringName<class_StringName>`, instance\: :ref:`Object<class_Object>`\ ) |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                      | :ref:`unregister_script_language<class_Engine_method_unregister_script_language>`\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`\ )             |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                     | :ref:`unregister_singleton<class_Engine_method_unregister_singleton>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                     |
   +----------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Engine_property_max_fps:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_fps** = ``0`` :ref:`🔗<class_Engine_property_max_fps>`

.. rst-class:: classref-property-setget

- |void| **set_max_fps**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_fps**\ (\ )

Số khung hình tối đa có thể được render mỗi giây (FPS). Giá trị ``0`` có nghĩa là framerate không bị giới hạn.

Giới hạn FPS có thể hữu ích để giảm mức tiêu thụ điện của máy chủ, từ đó giảm nhiệt, tiếng ồn và cải thiện thời lượng pin.

Nếu :ref:`ProjectSettings.display/window/vsync/vsync_mode<class_ProjectSettings_property_display/window/vsync/vsync_mode>` là **Enabled** hoặc **Adaptive**, thiết lập này được ưu tiên và số FPS tối đa không thể vượt quá tần số quét của màn hình. Xem thêm :ref:`DisplayServer.screen_get_refresh_rate()<class_DisplayServer_method_screen_get_refresh_rate>`.

Nếu :ref:`ProjectSettings.display/window/vsync/vsync_mode<class_ProjectSettings_property_display/window/vsync/vsync_mode>` là **Enabled**, trên các màn hình đã bật variable refresh rate (G-Sync/FreeSync), việc sử dụng giới hạn FPS thấp hơn tần số quét của màn hình vài khung hình sẽ `reduce input lag while avoiding tearing <https://blurbusters.com/howto-low-lag-vsync-on/>`__. Ở tần số quét cao hơn, nên tăng khoảng cách giữa giới hạn FPS và tần số quét của màn hình để đảm bảo các khung hình bù cho sai số về thời gian. Công thức tối ưu cho giá trị giới hạn FPS trong trường hợp này là ``r - (r * r) / 3600.0``, trong đó ``r`` là tần số quét của màn hình.

\ **Lưu ý:** Số khung hình trên giây thực tế vẫn có thể thấp hơn giá trị này nếu CPU hoặc GPU không theo kịp logic và hoạt động render của project.

\ **Lưu ý:** Nếu :ref:`ProjectSettings.display/window/vsync/vsync_mode<class_ProjectSettings_property_display/window/vsync/vsync_mode>` là **Disabled**, việc giới hạn FPS ở một giá trị cao có thể đạt ổn định trên hệ thống có thể giảm input lag so với framerate không giới hạn. Vì cách này hoạt động bằng cách đảm bảo tải GPU thấp hơn 100%, việc giảm độ trễ này chỉ hiệu quả trong các trường hợp bị nghẽn do GPU, không phải các trường hợp bị nghẽn do CPU.

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_max_physics_steps_per_frame:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_physics_steps_per_frame** = ``8`` :ref:`🔗<class_Engine_property_max_physics_steps_per_frame>`

.. rst-class:: classref-property-setget

- |void| **set_max_physics_steps_per_frame**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_physics_steps_per_frame**\ (\ )

Số physics step tối đa có thể được mô phỏng trong mỗi frame đã render.

\ **Lưu ý:** Giá trị mặc định được tinh chỉnh để ngăn các mô phỏng physics tốn kém kích hoạt vô hạn các mô phỏng còn tốn kém hơn. Tuy nhiên, game sẽ có vẻ chậm lại nếu FPS render thấp hơn ``1 / max_physics_steps_per_frame`` của :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`. Điều này xảy ra ngay cả khi ``delta`` được sử dụng nhất quán trong các phép tính physics. Để tránh điều này, hãy tăng :ref:`max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` nếu bạn đã tăng :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` cao hơn đáng kể so với giá trị mặc định.

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_physics_jitter_fix:

.. rst-class:: classref-property

:ref:`float<class_float>` **physics_jitter_fix** = ``0.5`` :ref:`🔗<class_Engine_property_physics_jitter_fix>`

.. rst-class:: classref-property-setget

- |void| **set_physics_jitter_fix**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_physics_jitter_fix**\ (\ )

Mức độ các physics tick được đồng bộ với thời gian thực. Nếu ``0`` hoặc thấp hơn, các tick được đồng bộ hoàn toàn. Các giá trị cao hơn khiến đồng hồ trong game lệch nhiều hơn so với đồng hồ thực, nhưng làm mượt hiện tượng giật framerate.

\ **Lưu ý:** Giá trị mặc định ``0.5`` sẽ đủ tốt trong hầu hết trường hợp; các giá trị trên ``2`` có thể khiến game phản ứng với các frame bị rớt sau một khoảng trễ đáng kể và không được khuyến nghị.

\ **Lưu ý:** Khi sử dụng giải pháp physics interpolation tùy chỉnh hoặc trong game mạng, bạn nên tắt physics jitter fix bằng cách đặt thuộc tính này thành ``0``.

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_physics_ticks_per_second:

.. rst-class:: classref-property

:ref:`int<class_int>` **physics_ticks_per_second** = ``60`` :ref:`🔗<class_Engine_property_physics_ticks_per_second>`

.. rst-class:: classref-property-setget

- |void| **set_physics_ticks_per_second**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_physics_ticks_per_second**\ (\ )

Số lần lặp cố định mỗi giây. Giá trị này kiểm soát tần suất chạy mô phỏng physics và phương thức :ref:`Node._physics_process()<class_Node_private_method__physics_process>`.

Mức sử dụng CPU tăng xấp xỉ theo tần suất physics tick. Tuy nhiên, ở tần suất tick rất thấp (thường dưới 30), hoạt động physics có thể bị lỗi. Input cũng có thể kém phản hồi hơn ở tần suất tick thấp vì có thể tồn tại khoảng trễ giữa lúc input được ghi nhận và lúc phản hồi ở physics tick tiếp theo. Tần suất tick cao cho mô phỏng physics chính xác hơn, đặc biệt với các đối tượng di chuyển nhanh. Ví dụ, các game đua xe có thể được lợi khi tăng tần suất tick cao hơn giá trị mặc định 60.

Xem thêm :ref:`max_fps<class_Engine_property_max_fps>` và :ref:`ProjectSettings.physics/common/physics_ticks_per_second<class_ProjectSettings_property_physics/common/physics_ticks_per_second>`.

\ **Lưu ý:** Mỗi frame đã render chỉ có thể mô phỏng tối đa :ref:`max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` physics tick. Nếu cần mô phỏng nhiều physics tick hơn trong mỗi frame đã render để theo kịp hoạt động render, project sẽ có vẻ chậm lại (ngay cả khi ``delta`` được sử dụng nhất quán trong các phép tính physics). Vì vậy, bạn cũng nên tăng :ref:`max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` nếu tăng :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` cao hơn đáng kể so với giá trị mặc định.

\ **Lưu ý:** Hãy cân nhắc bật :doc:`physics interpolation <../tutorials/physics/interpolation/index>` nếu bạn thay đổi :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` thành một giá trị không phải bội số của ``60``. Sử dụng physics interpolation sẽ tránh hiện tượng giật khi tần số quét của màn hình và tần suất cập nhật physics không khớp chính xác.

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_print_error_messages:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **print_error_messages** = ``true`` :ref:`🔗<class_Engine_property_print_error_messages>`

.. rst-class:: classref-property-setget

- |void| **set_print_error_messages**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_printing_error_messages**\ (\ )

Nếu ``false``, sẽ dừng in các thông báo lỗi và cảnh báo ra console và nhật ký Output của editor. Có thể dùng thuộc tính này để ẩn các thông báo lỗi và cảnh báo trong khi chạy bộ unit test. Thuộc tính này tương đương với thiết lập project :ref:`ProjectSettings.application/run/disable_stderr<class_ProjectSettings_property_application/run/disable_stderr>`.

\ **Lưu ý:** Thuộc tính này không ảnh hưởng đến tab Errors của editor khi chạy project từ editor.

\ **Cảnh báo:** Nếu được đặt thành ``false`` ở bất kỳ đâu trong project, các thông báo lỗi quan trọng có thể bị ẩn ngay cả khi chúng được phát ra từ các script khác. Trong script ``@tool``, điều này cũng sẽ ảnh hưởng đến chính editor. *Không* báo cáo lỗi trước khi đảm bảo rằng các thông báo lỗi đã được bật (theo mặc định chúng được bật).

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_print_to_stdout:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **print_to_stdout** = ``true`` :ref:`🔗<class_Engine_property_print_to_stdout>`

.. rst-class:: classref-property-setget

- |void| **set_print_to_stdout**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_printing_to_stdout**\ (\ )

Nếu ``false``, sẽ dừng in các thông báo (ví dụ bằng cách sử dụng :ref:`@GlobalScope.print()<class_@GlobalScope_method_print>`) ra console, các tệp log và nhật ký Output của editor. Thuộc tính này tương đương với thiết lập project :ref:`ProjectSettings.application/run/disable_stdout<class_ProjectSettings_property_application/run/disable_stdout>`.

\ **Lưu ý:** Điều này không dừng việc in các lỗi hoặc cảnh báo do script tạo ra ra console hoặc các tệp log; để biết thêm chi tiết, xem :ref:`print_error_messages<class_Engine_property_print_error_messages>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_property_time_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_scale** = ``1.0`` :ref:`🔗<class_Engine_property_time_scale>`

.. rst-class:: classref-property-setget

- |void| **set_time_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_scale**\ (\ )

Hệ số tốc độ mà đồng hồ trong game cập nhật so với thời gian thực. Ví dụ, nếu đặt thành ``2.0``, game chạy nhanh gấp đôi; nếu đặt thành ``0.5``, game chạy chậm bằng một nửa.

Giá trị này ảnh hưởng đến :ref:`Timer<class_Timer>`, :ref:`SceneTreeTimer<class_SceneTreeTimer>` và tất cả mô phỏng khác sử dụng thời gian ``delta`` (chẳng hạn như :ref:`Node._process()<class_Node_private_method__process>` và :ref:`Node._physics_process()<class_Node_private_method__physics_process>`).

\ **Lưu ý:** Bạn nên giữ thuộc tính này lớn hơn ``0.0``, vì nếu không game có thể hoạt động ngoài dự kiến.

\ **Lưu ý:** Điều này không ảnh hưởng đến tốc độ phát audio. Sử dụng :ref:`AudioServer.playback_speed_scale<class_AudioServer_property_playback_speed_scale>` để điều chỉnh độc lập tốc độ phát audio so với :ref:`time_scale<class_Engine_property_time_scale>`.

\ **Lưu ý:** Điều này không tự động điều chỉnh :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`. Với các giá trị lớn hơn ``1.0``, mô phỏng physics có thể kém chính xác hơn, vì mỗi physics tick sẽ kéo dài trong một khoảng thời gian engine lớn hơn. Nếu bạn sửa đổi :ref:`time_scale<class_Engine_property_time_scale>` để tăng tốc mô phỏng lên một hệ số lớn, hãy cân nhắc đồng thời tăng :ref:`physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` để mô phỏng đáng tin cậy hơn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Engine_method_capture_script_backtraces:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`ScriptBacktrace<class_ScriptBacktrace>`\] **capture_script_backtraces**\ (\ include_variables\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Engine_method_capture_script_backtraces>`

Thu thập và trả về các backtrace từ tất cả ngôn ngữ script đã đăng ký.

Theo mặc định, :ref:`ScriptBacktrace<class_ScriptBacktrace>` được trả về chỉ chứa các stack frame trong các bản build editor và bản build debug. Để bật chúng cho cả các bản build release, bạn cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_call_stacks<class_ProjectSettings_property_debug/settings/gdscript/always_track_call_stacks>`.

Nếu ``include_variables`` là ``true``, backtrace cũng sẽ bao gồm tên và giá trị của mọi biến global (ví dụ: các singleton autoload) tại thời điểm capture, cũng như các biến local và biến thành viên của class trong mỗi stack frame. Tuy nhiên, điều này chỉ được áp dụng khi chạy game với debugger được đính kèm, chẳng hạn như khi chạy game từ editor. Để bật tính năng này cho cả các bản export, bạn cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_local_variables<class_ProjectSettings_property_debug/settings/gdscript/always_track_local_variables>`.

\ **Cảnh báo:** Khi ``include_variables`` là ``true``, mọi biến được capture có thể (ví dụ: với backtrace GDScript) chứa giá trị thực của chúng, bao gồm cả các tham chiếu đến object. Điều này có nghĩa là việc lưu trữ một :ref:`ScriptBacktrace<class_ScriptBacktrace>` như vậy sẽ ngăn các object đó được deallocate, vì vậy nhìn chung bạn không nên làm vậy.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_architecture_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_architecture_name**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_architecture_name>`

Trả về tên kiến trúc CPU mà binary Godot được build cho. Các giá trị có thể được trả về bao gồm ``"x86_64"``, ``"x86_32"``, ``"arm64"``, ``"arm32"``, ``"rv64"``, ``"ppc64"``, ``"loongarch64"``, ``"wasm64"``, và ``"wasm32"``.

Để phát hiện build hiện tại là 64-bit hay xác định loại kiến trúc, không sử dụng tên kiến trúc. Thay vào đó, hãy sử dụng :ref:`OS.has_feature()<class_OS_method_has_feature>` để kiểm tra feature tag ``"64"``, hoặc các tag như ``"x86"`` hay ``"arm"``. Xem tài liệu :doc:`Feature Tags <../tutorials/export/feature_tags>` để biết thêm chi tiết.

\ **Lưu ý:** Method này *không* trả về tên kiến trúc CPU của hệ thống (như :ref:`OS.get_processor_name()<class_OS_method_get_processor_name>`). Ví dụ, khi chạy binary Godot ``x86_32`` trên hệ thống ``x86_64``, giá trị được trả về vẫn là ``"x86_32"``.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_author_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_author_info**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_author_info>`

Trả về thông tin tác giả của engine dưới dạng :ref:`Dictionary<class_Dictionary>`, trong đó mỗi entry là một :ref:`Array<class_Array>` các chuỗi chứa tên của những người đóng góp nổi bật cho Godot Engine: ``lead_developers``, ``founders``, ``project_managers``, và ``developers``.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_copyright_info:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_copyright_info**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_copyright_info>`

Trả về một :ref:`Array<class_Array>` gồm các dictionary chứa thông tin bản quyền cho mọi component trong mã nguồn của Godot.

Mỗi :ref:`Dictionary<class_Dictionary>` chứa một identifier ``name`` và một array ``parts`` gồm các dictionary. Nó mô tả chi tiết component với các entry sau:

- ``files`` - :ref:`Array<class_Array>` các đường dẫn file từ mã nguồn bị component này ảnh hưởng;

- ``copyright`` - :ref:`Array<class_Array>` những người sở hữu component này;

- ``license`` - License được áp dụng cho component này (chẳng hạn như "`Expat <https://en.wikipedia.org/wiki/MIT_License#Ambiguity_and_variants>`__" hoặc "`CC-BY-4.0 <https://creativecommons.org/licenses/by/4.0/>`__").

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_donor_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_donor_info**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_donor_info>`

Trả về một :ref:`Dictionary<class_Dictionary>` gồm tên các donor được phân loại. Mỗi entry là một :ref:`Array<class_Array>` các chuỗi:

{``platinum_sponsors``, ``gold_sponsors``, ``silver_sponsors``, ``bronze_sponsors``, ``mini_sponsors``, ``gold_donors``, ``silver_donors``, ``bronze_donors``}

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_frames_drawn:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_frames_drawn**\ (\ ) :ref:`🔗<class_Engine_method_get_frames_drawn>`

Trả về tổng số frame đã được vẽ kể từ khi engine khởi động.

\ **Lưu ý:** Trên các nền tảng headless, hoặc khi rendering bị vô hiệu hóa bằng ``--disable-render-loop`` qua command line, method này luôn trả về ``0``. Xem thêm :ref:`get_process_frames()<class_Engine_method_get_process_frames>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_frames_per_second:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_frames_per_second**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_frames_per_second>`

Trả về số frame trung bình được render mỗi giây (FPS), còn gọi là framerate.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_license_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_license_info**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_license_info>`

Trả về một :ref:`Dictionary<class_Dictionary>` gồm các license được Godot sử dụng và các component bên thứ ba đi kèm. Mỗi entry là tên license (chẳng hạn như "`Expat <https://en.wikipedia.org/wiki/MIT_License#Ambiguity_and_variants>`__") cùng phần nội dung tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_license_text:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_license_text**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_license_text>`

Trả về toàn bộ nội dung license của Godot.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_main_loop:

.. rst-class:: classref-method

:ref:`MainLoop<class_MainLoop>` **get_main_loop**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_main_loop>`

Trả về instance của :ref:`MainLoop<class_MainLoop>`. Đây thường là :ref:`SceneTree<class_SceneTree>` chính và cũng chính là :ref:`Node.get_tree()<class_Node_method_get_tree>`.

\ **Lưu ý:** Type được instantiate làm main loop có thể được thay đổi bằng :ref:`ProjectSettings.application/run/main_loop_type<class_ProjectSettings_property_application/run/main_loop_type>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_physics_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_physics_frames**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_physics_frames>`

Trả về tổng số frame đã trôi qua kể từ khi engine khởi động. Con số này tăng lên sau mỗi **physics frame**. Xem thêm :ref:`get_process_frames()<class_Engine_method_get_process_frames>`.

Có thể sử dụng method này để chạy logic tốn nhiều tài nguyên ít thường xuyên hơn mà không phụ thuộc vào :ref:`Timer<class_Timer>`:


.. tabs::

 .. code-tab:: gdscript

    func _physics_process(_delta):
        if Engine.get_physics_frames() % 2 == 0:
            pass # Chạy logic tốn nhiều tài nguyên tại đây, chỉ một lần sau mỗi 2 physics frame.

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        base._PhysicsProcess(delta);

        if (Engine.GetPhysicsFrames() % 2 == 0)
        {
            // Chạy logic tốn nhiều tài nguyên tại đây, chỉ một lần sau mỗi 2 physics frame.
        }
    }



.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_physics_interpolation_fraction:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_physics_interpolation_fraction**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_physics_interpolation_fraction>`

Trả về phần thời gian đã trôi qua của physics tick hiện tại tại thời điểm render frame. Có thể sử dụng giá trị này để triển khai fixed timestep interpolation.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_process_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_process_frames**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_process_frames>`

Trả về tổng số frame đã trôi qua kể từ khi engine khởi động. Con số này tăng lên sau mỗi **process frame**, bất kể render loop có được bật hay không. Xem thêm :ref:`get_frames_drawn()<class_Engine_method_get_frames_drawn>` và :ref:`get_physics_frames()<class_Engine_method_get_physics_frames>`.

Có thể sử dụng method này để chạy logic tốn nhiều tài nguyên ít thường xuyên hơn mà không phụ thuộc vào :ref:`Timer<class_Timer>`:


.. tabs::

 .. code-tab:: gdscript

    func _process(_delta):
        if Engine.get_process_frames() % 5 == 0:
            pass # Chạy logic tốn nhiều tài nguyên tại đây, chỉ một lần sau mỗi 5 process (render) frame.

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        base._Process(delta);

        if (Engine.GetProcessFrames() % 5 == 0)
        {
            // Chạy logic tốn nhiều tài nguyên tại đây, chỉ một lần sau mỗi 5 process (render) frame.
        }
    }



.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_script_language:

.. rst-class:: classref-method

:ref:`ScriptLanguage<class_ScriptLanguage>` **get_script_language**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Engine_method_get_script_language>`

Trả về một instance của :ref:`ScriptLanguage<class_ScriptLanguage>` với ``index`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_script_language_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_script_language_count**\ (\ ) :ref:`🔗<class_Engine_method_get_script_language_count>`

Trả về số lượng ngôn ngữ script hiện có. Sử dụng cùng với :ref:`get_script_language()<class_Engine_method_get_script_language>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_singleton:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_singleton**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Engine_method_get_singleton>`

Trả về global singleton với ``name`` đã cho, hoặc ``null`` nếu không tồn tại. Thường được sử dụng cho plugin. Xem thêm :ref:`has_singleton()<class_Engine_method_has_singleton>` và :ref:`get_singleton_list()<class_Engine_method_get_singleton_list>`.

\ **Lưu ý:** Global singleton không giống các node được autoload, vốn có thể cấu hình trong project settings.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_singleton_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_singleton_list**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_singleton_list>`

Trả về danh sách tên của tất cả global singleton hiện có. Xem thêm :ref:`get_singleton()<class_Engine_method_get_singleton>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_version_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_version_info**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_version_info>`

Trả về thông tin version hiện tại của engine dưới dạng :ref:`Dictionary<class_Dictionary>`, chứa các entry sau:

- ``major`` - Số version Major dưới dạng int;

- ``minor`` - Số version Minor dưới dạng int;

- ``patch`` - Số version Patch dưới dạng int;

- ``hex`` - Version đầy đủ được mã hóa dưới dạng int hexadecimal với một byte (2 chữ số hex) cho mỗi số (xem ví dụ bên dưới);

- ``status`` - Status (chẳng hạn như "beta", "rc1", "rc2", "stable", v.v.) dưới dạng String;

- ``build`` - Tên build (ví dụ: "custom_build") dưới dạng String;

- ``hash`` - Git commit hash đầy đủ dưới dạng String;

- ``timestamp`` - Chứa timestamp UNIX của ngày Git commit tính bằng giây dưới dạng int, hoặc ``0`` nếu không khả dụng;

- ``string`` - ``major``, ``minor``, ``patch``, ``status``, và ``build`` trong một String duy nhất.

Giá trị ``hex`` được mã hóa như sau, từ trái sang phải: một byte cho major, một byte cho minor, một byte cho patch version. Ví dụ, "3.1.12" sẽ là ``0x03010C``.

\ **Lưu ý:** Giá trị ``hex`` bên trong vẫn là một :ref:`int<class_int>`, và khi in ra sẽ cho bạn biểu diễn dạng thập phân của nó, vốn không đặc biệt có ý nghĩa. Hãy sử dụng literal hexadecimal để nhanh chóng so sánh version từ code:


.. tabs::

 .. code-tab:: gdscript

    if Engine.get_version_info().hex >= 0x040100:
        pass # Thực hiện những việc dành riêng cho version 4.1 trở lên.
    else:
        pass # Thực hiện những việc dành riêng cho các version trước 4.1.

 .. code-tab:: csharp

    if ((int)Engine.GetVersionInfo()["hex"] >= 0x040100)
    {
        // Thực hiện những việc dành riêng cho version 4.1 trở lên.
    }
    else
    {
        // Thực hiện những việc dành riêng cho các version trước 4.1.
    }



.. rst-class:: classref-item-separator

----

.. _class_Engine_method_get_write_movie_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_write_movie_path**\ (\ ) |const| :ref:`🔗<class_Engine_method_get_write_movie_path>`

Trả về đường dẫn đến file output của :ref:`MovieWriter<class_MovieWriter>`, hoặc chuỗi rỗng nếu engine chưa được khởi động ở Movie Maker mode. Có thể thay đổi đường dẫn mặc định trong :ref:`ProjectSettings.editor/movie_writer/movie_file<class_ProjectSettings_property_editor/movie_writer/movie_file>`.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_has_singleton:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_singleton**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Engine_method_has_singleton>`

Trả về ``true`` nếu một singleton với ``name`` đã cho tồn tại trong global scope. Xem thêm :ref:`get_singleton()<class_Engine_method_get_singleton>`.


.. tabs::

 .. code-tab:: gdscript

    print(Engine.has_singleton("OS"))          # In ra true
    print(Engine.has_singleton("Engine"))      # In ra true
    print(Engine.has_singleton("AudioServer")) # In ra true
    print(Engine.has_singleton("Unknown"))     # In ra false

 .. code-tab:: csharp

    GD.Print(Engine.HasSingleton("OS"));          // In ra True
    GD.Print(Engine.HasSingleton("Engine"));      // In ra True
    GD.Print(Engine.HasSingleton("AudioServer")); // In ra True
    GD.Print(Engine.HasSingleton("Unknown"));     // In ra False



\ **Lưu ý:** Các global singleton không giống với các node được autoload, vốn có thể được cấu hình trong phần cài đặt dự án.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_is_editor_hint:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_editor_hint**\ (\ ) |const| :ref:`🔗<class_Engine_method_is_editor_hint>`

Trả về ``true`` nếu script hiện đang chạy bên trong editor, nếu không thì trả về ``false``. Điều này hữu ích cho các script ``@tool`` để vẽ có điều kiện các editor helper, hoặc ngăn việc vô tình chạy mã "game" có thể ảnh hưởng đến trạng thái scene khi đang ở trong editor:


.. tabs::

 .. code-tab:: gdscript

    if Engine.is_editor_hint():
        draw_gizmos()
    else:
        simulate_physics()

 .. code-tab:: csharp

    if (Engine.IsEditorHint())
        DrawGizmos();
    else
        SimulatePhysics();



Xem :doc:`Running code in the editor <../tutorials/plugins/running_code_in_the_editor>` trong tài liệu để biết thêm thông tin.

\ **Lưu ý:** Để phát hiện liệu script có đang chạy trên một *build* của editor hay không (chẳng hạn khi nhấn :kbd:`F5`), hãy dùng :ref:`OS.has_feature()<class_OS_method_has_feature>` với đối số ``"editor"`` thay thế. ``OS.has_feature("editor")`` sẽ cho kết quả ``true`` cả khi script đang chạy trong editor và khi chạy project từ editor, nhưng trả về ``false`` khi chạy từ một project đã export.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_is_embedded_in_editor:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_embedded_in_editor**\ (\ ) |const| :ref:`🔗<class_Engine_method_is_embedded_in_editor>`

Trả về ``true`` nếu engine đang chạy được embed trong editor. Điều này hữu ích để ngăn việc cố gắng cập nhật window mode hoặc window flags không được hỗ trợ khi chạy project được embed trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_is_in_physics_frame:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_in_physics_frame**\ (\ ) |const| :ref:`🔗<class_Engine_method_is_in_physics_frame>`

Trả về ``true`` nếu engine đang ở trong bước xử lý physics cố định của main loop.

::

    func _enter_tree():
        # Tùy thuộc vào thời điểm node được thêm vào tree,
        # sẽ in ra "true" hoặc "false".
        print(Engine.is_in_physics_frame())

    func _process(delta):
        print(Engine.is_in_physics_frame()) # In ra false

    func _physics_process(delta):
        print(Engine.is_in_physics_frame()) # In ra true

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_register_script_language:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **register_script_language**\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`\ ) :ref:`🔗<class_Engine_method_register_script_language>`

Đăng ký một instance :ref:`ScriptLanguage<class_ScriptLanguage>` để có thể dùng với ``ScriptServer``.

Trả về:

- :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu thành công;

- :ref:`@GlobalScope.ERR_UNAVAILABLE<class_@GlobalScope_constant_ERR_UNAVAILABLE>` nếu ``ScriptServer`` đã đạt giới hạn và không thể đăng ký thêm ngôn ngữ mới nào;

- :ref:`@GlobalScope.ERR_ALREADY_EXISTS<class_@GlobalScope_constant_ERR_ALREADY_EXISTS>` nếu ``ScriptServer`` đã chứa một ngôn ngữ có extension/name/type tương tự.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_register_singleton:

.. rst-class:: classref-method

|void| **register_singleton**\ (\ name\: :ref:`StringName<class_StringName>`, instance\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_Engine_method_register_singleton>`

Đăng ký :ref:`Object<class_Object>` ``instance`` đã cho dưới dạng singleton, có thể truy cập toàn cục bằng ``name``. Hữu ích cho các plugin.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_unregister_script_language:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **unregister_script_language**\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`\ ) :ref:`🔗<class_Engine_method_unregister_script_language>`

Hủy đăng ký instance :ref:`ScriptLanguage<class_ScriptLanguage>` khỏi ``ScriptServer``.

Trả về:

- :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu thành công;

- :ref:`@GlobalScope.ERR_DOES_NOT_EXIST<class_@GlobalScope_constant_ERR_DOES_NOT_EXIST>` nếu ngôn ngữ chưa được đăng ký trong ``ScriptServer``.

.. rst-class:: classref-item-separator

----

.. _class_Engine_method_unregister_singleton:

.. rst-class:: classref-method

|void| **unregister_singleton**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Engine_method_unregister_singleton>`

Xóa singleton được đăng ký dưới tên ``name``. Đối tượng singleton *không* được giải phóng. Chỉ hoạt động với các singleton do người dùng định nghĩa được đăng ký bằng :ref:`register_singleton()<class_Engine_method_register_singleton>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
