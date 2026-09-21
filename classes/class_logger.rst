:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Logger.xml.

.. _class_Logger:

Logger
======

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Logger tùy chỉnh để nhận các thông báo từ luồng lỗi/cảnh báo nội bộ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Logger tùy chỉnh để nhận các thông báo từ luồng lỗi/cảnh báo nội bộ. Logger được đăng ký thông qua :ref:`OS.add_logger()<class_OS_method_add_logger>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Logging <../tutorials/scripting/logging>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_log_error<class_Logger_private_method__log_error>`\ (\ function\: :ref:`String<class_String>`, file\: :ref:`String<class_String>`, line\: :ref:`int<class_int>`, code\: :ref:`String<class_String>`, rationale\: :ref:`String<class_String>`, editor_notify\: :ref:`bool<class_bool>`, error_type\: :ref:`int<class_int>`, script_backtraces\: :ref:`Array<class_Array>`\[:ref:`ScriptBacktrace<class_ScriptBacktrace>`\]\ ) |virtual| |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_log_message<class_Logger_private_method__log_message>`\ (\ message\: :ref:`String<class_String>`, error\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                                                                                                                                                                                                                         |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Logger_ErrorType:

.. rst-class:: classref-enumeration

enum **ErrorType**: :ref:`🔗<enum_Logger_ErrorType>`

.. _class_Logger_constant_ERROR_TYPE_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorType<enum_Logger_ErrorType>` **ERROR_TYPE_ERROR** = ``0``

Thông báo nhận được là một lỗi.

.. _class_Logger_constant_ERROR_TYPE_WARNING:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorType<enum_Logger_ErrorType>` **ERROR_TYPE_WARNING** = ``1``

Thông báo nhận được là một cảnh báo.

.. _class_Logger_constant_ERROR_TYPE_SCRIPT:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorType<enum_Logger_ErrorType>` **ERROR_TYPE_SCRIPT** = ``2``

Thông báo nhận được là một lỗi script.

.. _class_Logger_constant_ERROR_TYPE_SHADER:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorType<enum_Logger_ErrorType>` **ERROR_TYPE_SHADER** = ``3``

Thông báo nhận được là một lỗi shader.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_Logger_private_method__log_error:

.. rst-class:: classref-method

|void| **_log_error**\ (\ function\: :ref:`String<class_String>`, file\: :ref:`String<class_String>`, line\: :ref:`int<class_int>`, code\: :ref:`String<class_String>`, rationale\: :ref:`String<class_String>`, editor_notify\: :ref:`bool<class_bool>`, error_type\: :ref:`int<class_int>`, script_backtraces\: :ref:`Array<class_Array>`\[:ref:`ScriptBacktrace<class_ScriptBacktrace>`\]\ ) |virtual| :ref:`🔗<class_Logger_private_method__log_error>`

Được gọi khi một lỗi được ghi log. Lỗi cung cấp ``function``, ``file`` và ``line`` nơi lỗi bắt nguồn, cùng với ``code`` đã tạo ra lỗi hoặc một ``rationale``.

Loại lỗi do ``error_type`` cung cấp được mô tả trong enumeration :ref:`ErrorType<enum_Logger_ErrorType>`.

Ngoài ra, ``script_backtraces`` cung cấp các backtrace cho từng ngôn ngữ script. Theo mặc định, các backtrace này chỉ chứa các stack frame trong editor build và debug build. Để bật chúng cho cả release build, bạn cũng cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_call_stacks<class_ProjectSettings_property_debug/settings/gdscript/always_track_call_stacks>`.

\ **Cảnh báo:** Phương thức này sẽ được gọi từ các thread khác thread chính, có thể đồng thời, vì vậy bạn cần có một cơ chế thread-safety nào đó trong phần triển khai của mình, chẳng hạn như :ref:`Mutex<class_Mutex>`.

\ **Lưu ý:** ``script_backtraces`` sẽ không chứa bất kỳ biến nào được capture, do chi phí quá cao. Để lấy được chúng, bạn sẽ cần tự capture các backtrace từ bên trong các phương thức virtual của **Logger**, bằng cách sử dụng :ref:`Engine.capture_script_backtraces()<class_Engine_method_capture_script_backtraces>`.

\ **Lưu ý:** Không hỗ trợ ghi log các lỗi từ phương thức này bằng những hàm như :ref:`@GlobalScope.push_error()<class_@GlobalScope_method_push_error>` hoặc :ref:`@GlobalScope.push_warning()<class_@GlobalScope_method_push_warning>`, vì điều đó có thể gây ra đệ quy vô hạn. Các lỗi này sẽ chỉ xuất hiện trong đầu ra console.

.. rst-class:: classref-item-separator

----

.. _class_Logger_private_method__log_message:

.. rst-class:: classref-method

|void| **_log_message**\ (\ message\: :ref:`String<class_String>`, error\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_Logger_private_method__log_message>`

Được gọi khi một thông báo được ghi log. Nếu ``error`` là ``true``, thì thông báo này được gửi đến ``stderr``.

\ **Cảnh báo:** Phương thức này sẽ được gọi từ các thread khác thread chính, có thể đồng thời, vì vậy bạn cần có một cơ chế thread-safety nào đó trong phần triển khai của mình, chẳng hạn như :ref:`Mutex<class_Mutex>`.

\ **Lưu ý:** Không hỗ trợ ghi một thông báo khác từ phương thức này bằng những hàm như :ref:`@GlobalScope.print()<class_@GlobalScope_method_print>`, vì điều đó có thể gây ra đệ quy vô hạn. Các thông báo này sẽ chỉ xuất hiện trong đầu ra console.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
