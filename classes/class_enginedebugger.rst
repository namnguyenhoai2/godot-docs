:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EngineDebugger.xml.

.. _class_EngineDebugger:

EngineDebugger
==============

**Kế thừa:** :ref:`Object<class_Object>`

Hiển thị trình gỡ lỗi nội bộ.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EngineDebugger** xử lý việc giao tiếp giữa editor và game đang chạy. Nó hoạt động trong game đang chạy. Có thể gửi/nhận các message thông qua nó. Nó cũng quản lý các profiler.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`clear_breakpoints<class_EngineDebugger_method_clear_breakpoints>`\ (\ )                                                                                                                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`debug<class_EngineDebugger_method_debug>`\ (\ can_continue\: :ref:`bool<class_bool>` = true, is_error_breakpoint\: :ref:`bool<class_bool>` = false\ )                                                                       |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`get_depth<class_EngineDebugger_method_get_depth>`\ (\ ) |const|                                                                                                                                                             |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`get_lines_left<class_EngineDebugger_method_get_lines_left>`\ (\ ) |const|                                                                                                                                                   |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`has_capture<class_EngineDebugger_method_has_capture>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`has_profiler<class_EngineDebugger_method_has_profiler>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                   |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`insert_breakpoint<class_EngineDebugger_method_insert_breakpoint>`\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ )                                                                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_active<class_EngineDebugger_method_is_active>`\ (\ )                                                                                                                                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_breakpoint<class_EngineDebugger_method_is_breakpoint>`\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ ) |const|                                                                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_profiling<class_EngineDebugger_method_is_profiling>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                   |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_skipping_breakpoints<class_EngineDebugger_method_is_skipping_breakpoints>`\ (\ ) |const|                                                                                                                                 |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`line_poll<class_EngineDebugger_method_line_poll>`\ (\ )                                                                                                                                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`profiler_add_frame_data<class_EngineDebugger_method_profiler_add_frame_data>`\ (\ name\: :ref:`StringName<class_StringName>`, data\: :ref:`Array<class_Array>`\ )                                                           |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`profiler_enable<class_EngineDebugger_method_profiler_enable>`\ (\ name\: :ref:`StringName<class_StringName>`, enable\: :ref:`bool<class_bool>`, arguments\: :ref:`Array<class_Array>` = []\ )                               |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`register_message_capture<class_EngineDebugger_method_register_message_capture>`\ (\ name\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ )                                               |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`register_profiler<class_EngineDebugger_method_register_profiler>`\ (\ name\: :ref:`StringName<class_StringName>`, profiler\: :ref:`EngineProfiler<class_EngineProfiler>`\ )                                                 |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`remove_breakpoint<class_EngineDebugger_method_remove_breakpoint>`\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ )                                                                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`script_debug<class_EngineDebugger_method_script_debug>`\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`, can_continue\: :ref:`bool<class_bool>` = true, is_error_breakpoint\: :ref:`bool<class_bool>` = false\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`send_message<class_EngineDebugger_method_send_message>`\ (\ message\: :ref:`String<class_String>`, data\: :ref:`Array<class_Array>`\ )                                                                                      |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_depth<class_EngineDebugger_method_set_depth>`\ (\ depth\: :ref:`int<class_int>`\ )                                                                                                                                      |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_lines_left<class_EngineDebugger_method_set_lines_left>`\ (\ lines\: :ref:`int<class_int>`\ )                                                                                                                            |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`unregister_message_capture<class_EngineDebugger_method_unregister_message_capture>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                       |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`unregister_profiler<class_EngineDebugger_method_unregister_profiler>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                     |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EngineDebugger_method_clear_breakpoints:

.. rst-class:: classref-method

|void| **clear_breakpoints**\ (\ ) :ref:`🔗<class_EngineDebugger_method_clear_breakpoints>`

Xóa tất cả breakpoint.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_debug:

.. rst-class:: classref-method

|void| **debug**\ (\ can_continue\: :ref:`bool<class_bool>` = true, is_error_breakpoint\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_EngineDebugger_method_debug>`

Bắt đầu tạm dừng để gỡ lỗi trong quá trình thực thi script, tùy chọn chỉ định liệu chương trình có thể tiếp tục dựa trên ``can_continue`` hay không và liệu việc tạm dừng có phải do breakpoint gây ra hay không.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_get_depth:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_depth**\ (\ ) |const| :ref:`🔗<class_EngineDebugger_method_get_depth>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Trả về độ sâu gỡ lỗi hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_get_lines_left:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_lines_left**\ (\ ) |const| :ref:`🔗<class_EngineDebugger_method_get_lines_left>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Trả về số dòng còn lại.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_has_capture:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_capture**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_has_capture>`

Trả về ``true`` nếu có capture với tên đã cho, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_has_profiler:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_profiler**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_has_profiler>`

Trả về ``true`` nếu có profiler với tên đã cho, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_insert_breakpoint:

.. rst-class:: classref-method

|void| **insert_breakpoint**\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_insert_breakpoint>`

Chèn một breakpoint mới với ``source`` và ``line`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_is_active:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_active**\ (\ ) :ref:`🔗<class_EngineDebugger_method_is_active>`

Trả về ``true`` nếu trình gỡ lỗi đang hoạt động, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_is_breakpoint:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_breakpoint**\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EngineDebugger_method_is_breakpoint>`

Trả về ``true`` nếu ``source`` và ``line`` đã cho biểu thị một breakpoint hiện có.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_is_profiling:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_profiling**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_is_profiling>`

Trả về ``true`` nếu profiler có tên đã cho đang tồn tại và hoạt động, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_is_skipping_breakpoints:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_skipping_breakpoints**\ (\ ) |const| :ref:`🔗<class_EngineDebugger_method_is_skipping_breakpoints>`

Trả về ``true`` nếu trình gỡ lỗi đang bỏ qua các breakpoint, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_line_poll:

.. rst-class:: classref-method

|void| **line_poll**\ (\ ) :ref:`🔗<class_EngineDebugger_method_line_poll>`

Buộc thực hiện một vòng lặp xử lý các sự kiện của trình gỡ lỗi. Mục đích của phương thức này chỉ là xử lý các sự kiện định kỳ khi script có thể trở nên quá bận, để các lỗi như vòng lặp vô hạn có thể được phát hiện.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_profiler_add_frame_data:

.. rst-class:: classref-method

|void| **profiler_add_frame_data**\ (\ name\: :ref:`StringName<class_StringName>`, data\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_EngineDebugger_method_profiler_add_frame_data>`

Gọi callable ``add`` của profiler với ``name`` và ``data`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_profiler_enable:

.. rst-class:: classref-method

|void| **profiler_enable**\ (\ name\: :ref:`StringName<class_StringName>`, enable\: :ref:`bool<class_bool>`, arguments\: :ref:`Array<class_Array>` = []\ ) :ref:`🔗<class_EngineDebugger_method_profiler_enable>`

Gọi callable ``toggle`` của profiler với ``name`` và ``arguments`` đã cho. Bật/tắt cùng profiler đó tùy theo đối số ``enable``.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_register_message_capture:

.. rst-class:: classref-method

|void| **register_message_capture**\ (\ name\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_EngineDebugger_method_register_message_capture>`

Đăng ký một message capture với ``name`` đã cho. Nếu ``name`` là "my_message" thì các message bắt đầu bằng "my_message:" sẽ được gọi với callable đã cho.

Callable phải chấp nhận một chuỗi message và một mảng data làm đối số. Callable nên trả về ``true`` nếu message được nhận diện.

\ **Lưu ý:** Callable sẽ nhận message đã bỏ phần tiền tố, không giống như :ref:`EditorDebuggerPlugin._capture()<class_EditorDebuggerPlugin_private_method__capture>`. Xem mô tả :ref:`EditorDebuggerPlugin<class_EditorDebuggerPlugin>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_register_profiler:

.. rst-class:: classref-method

|void| **register_profiler**\ (\ name\: :ref:`StringName<class_StringName>`, profiler\: :ref:`EngineProfiler<class_EngineProfiler>`\ ) :ref:`🔗<class_EngineDebugger_method_register_profiler>`

Đăng ký một profiler với ``name`` đã cho. Xem :ref:`EngineProfiler<class_EngineProfiler>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_remove_breakpoint:

.. rst-class:: classref-method

|void| **remove_breakpoint**\ (\ line\: :ref:`int<class_int>`, source\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_remove_breakpoint>`

Xóa breakpoint với ``source`` và ``line`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_script_debug:

.. rst-class:: classref-method

|void| **script_debug**\ (\ language\: :ref:`ScriptLanguage<class_ScriptLanguage>`, can_continue\: :ref:`bool<class_bool>` = true, is_error_breakpoint\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_EngineDebugger_method_script_debug>`

Bắt đầu tạm dừng để gỡ lỗi trong quá trình thực thi script, tùy chọn chỉ định liệu chương trình có thể tiếp tục dựa trên ``can_continue`` hay không và liệu việc tạm dừng có phải do breakpoint gây ra hay không.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_send_message:

.. rst-class:: classref-method

|void| **send_message**\ (\ message\: :ref:`String<class_String>`, data\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_EngineDebugger_method_send_message>`

Gửi một message với ``message`` và mảng ``data`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_set_depth:

.. rst-class:: classref-method

|void| **set_depth**\ (\ depth\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EngineDebugger_method_set_depth>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Đặt độ sâu gỡ lỗi hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_set_lines_left:

.. rst-class:: classref-method

|void| **set_lines_left**\ (\ lines\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EngineDebugger_method_set_lines_left>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Đặt số dòng gỡ lỗi còn lại hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_unregister_message_capture:

.. rst-class:: classref-method

|void| **unregister_message_capture**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_unregister_message_capture>`

Hủy đăng ký message capture với ``name`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EngineDebugger_method_unregister_profiler:

.. rst-class:: classref-method

|void| **unregister_profiler**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EngineDebugger_method_unregister_profiler>`

Hủy đăng ký profiler với ``name`` đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
