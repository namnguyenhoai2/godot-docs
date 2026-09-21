:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EngineProfiler.xml.

.. _class_EngineProfiler:

EngineProfiler
==============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp cơ sở để tạo các profiler tùy chỉnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Có thể sử dụng lớp này để triển khai các profiler tùy chỉnh có khả năng tương tác với engine và trình gỡ lỗi của editor.

Xem :ref:`EngineDebugger<class_EngineDebugger>` và :ref:`EditorDebuggerPlugin<class_EditorDebuggerPlugin>` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_add_frame<class_EngineProfiler_private_method__add_frame>`\ (\ data\: :ref:`Array<class_Array>`\ ) |virtual|                                                                                                                                 |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_tick<class_EngineProfiler_private_method__tick>`\ (\ frame_time\: :ref:`float<class_float>`, process_time\: :ref:`float<class_float>`, physics_time\: :ref:`float<class_float>`, physics_frame_time\: :ref:`float<class_float>`\ ) |virtual| |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_toggle<class_EngineProfiler_private_method__toggle>`\ (\ enable\: :ref:`bool<class_bool>`, options\: :ref:`Array<class_Array>`\ ) |virtual|                                                                                                  |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EngineProfiler_private_method__add_frame:

.. rst-class:: classref-method

|void| **_add_frame**\ (\ data\: :ref:`Array<class_Array>`\ ) |virtual| :ref:`🔗<class_EngineProfiler_private_method__add_frame>`

Được gọi khi dữ liệu được thêm vào profiler bằng :ref:`EngineDebugger.profiler_add_frame_data()<class_EngineDebugger_method_profiler_add_frame_data>`.

.. rst-class:: classref-item-separator

----

.. _class_EngineProfiler_private_method__tick:

.. rst-class:: classref-method

|void| **_tick**\ (\ frame_time\: :ref:`float<class_float>`, process_time\: :ref:`float<class_float>`, physics_time\: :ref:`float<class_float>`, physics_frame_time\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_EngineProfiler_private_method__tick>`

Được gọi một lần trong mỗi vòng lặp của engine khi profiler đang hoạt động, kèm theo thông tin về frame hiện tại. Tất cả giá trị thời gian đều tính bằng giây. Giá trị thấp hơn biểu thị thời gian xử lý nhanh hơn và do đó được xem là tốt hơn.

.. rst-class:: classref-item-separator

----

.. _class_EngineProfiler_private_method__toggle:

.. rst-class:: classref-method

|void| **_toggle**\ (\ enable\: :ref:`bool<class_bool>`, options\: :ref:`Array<class_Array>`\ ) |virtual| :ref:`🔗<class_EngineProfiler_private_method__toggle>`

Được gọi khi profiler được bật/tắt, cùng với một tập hợp ``options``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
