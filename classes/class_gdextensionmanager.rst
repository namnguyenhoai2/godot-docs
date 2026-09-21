:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GDExtensionManager.xml.

.. _class_GDExtensionManager:

GDExtensionManager
==================

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào chức năng GDExtension.

.. rst-class:: classref-introduction-group

Mô tả
-----

GDExtensionManager tải, khởi tạo và theo dõi tất cả các thư viện :ref:`GDExtension<class_GDExtension>` hiện có trong project.

\ **Lưu ý:** Không cần quan tâm đến GDExtension trừ khi bạn biết mình đang làm gì.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Tổng quan về GDExtension <../engine_details/engine_api/gdextension/what_is_gdextension>`

- :doc:`Ví dụ GDExtension trong C++ <../tutorials/scripting/cpp/gdextension_cpp_example>`

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GDExtension<class_GDExtension>`                 | :ref:`get_extension<class_GDExtensionManager_method_get_extension>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                         |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`     | :ref:`get_loaded_extensions<class_GDExtensionManager_method_get_loaded_extensions>`\ (\ ) |const|                                                                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_extension_loaded<class_GDExtensionManager_method_is_extension_loaded>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` | :ref:`load_extension<class_GDExtensionManager_method_load_extension>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                       |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` | :ref:`load_extension_from_function<class_GDExtensionManager_method_load_extension_from_function>`\ (\ path\: :ref:`String<class_String>`, init_func\: ``const GDExtensionInitializationFunction*``\ ) |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` | :ref:`reload_extension<class_GDExtensionManager_method_reload_extension>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                   |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` | :ref:`unload_extension<class_GDExtensionManager_method_unload_extension>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                   |
   +-------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_GDExtensionManager_signal_extension_loaded:

.. rst-class:: classref-signal

**extension_loaded**\ (\ extension\: :ref:`GDExtension<class_GDExtension>`\ ) :ref:`🔗<class_GDExtensionManager_signal_extension_loaded>`

Được phát ra sau khi editor hoàn tất việc tải một extension mới.

\ **Lưu ý:** Signal này chỉ được phát ra trong các bản build editor.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_signal_extension_unloading:

.. rst-class:: classref-signal

**extension_unloading**\ (\ extension\: :ref:`GDExtension<class_GDExtension>`\ ) :ref:`🔗<class_GDExtensionManager_signal_extension_unloading>`

Được phát ra trước khi editor bắt đầu gỡ tải một extension.

\ **Lưu ý:** Signal này chỉ được phát ra trong các bản build editor.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_signal_extensions_reloaded:

.. rst-class:: classref-signal

**extensions_reloaded**\ (\ ) :ref:`🔗<class_GDExtensionManager_signal_extensions_reloaded>`

Được phát ra sau khi editor hoàn tất việc tải lại một hoặc nhiều extension.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_GDExtensionManager_LoadStatus:

.. rst-class:: classref-enumeration

enum **LoadStatus**: :ref:`🔗<enum_GDExtensionManager_LoadStatus>`

.. _class_GDExtensionManager_constant_LOAD_STATUS_OK:

.. rst-class:: classref-enumeration-constant

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **LOAD_STATUS_OK** = ``0``

Extension đã được tải thành công.

.. _class_GDExtensionManager_constant_LOAD_STATUS_FAILED:

.. rst-class:: classref-enumeration-constant

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **LOAD_STATUS_FAILED** = ``1``

Extension không tải được, có thể vì extension không tồn tại hoặc thiếu dependency.

.. _class_GDExtensionManager_constant_LOAD_STATUS_ALREADY_LOADED:

.. rst-class:: classref-enumeration-constant

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **LOAD_STATUS_ALREADY_LOADED** = ``2``

Extension đã được tải.

.. _class_GDExtensionManager_constant_LOAD_STATUS_NOT_LOADED:

.. rst-class:: classref-enumeration-constant

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **LOAD_STATUS_NOT_LOADED** = ``3``

Extension chưa được tải.

.. _class_GDExtensionManager_constant_LOAD_STATUS_NEEDS_RESTART:

.. rst-class:: classref-enumeration-constant

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **LOAD_STATUS_NEEDS_RESTART** = ``4``

Extension yêu cầu ứng dụng khởi động lại để được tải hoàn toàn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_GDExtensionManager_method_get_extension:

.. rst-class:: classref-method

:ref:`GDExtension<class_GDExtension>` **get_extension**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDExtensionManager_method_get_extension>`

Trả về :ref:`GDExtension<class_GDExtension>` tại ``path`` tệp đã cho, hoặc ``null`` nếu extension chưa được tải hoặc không tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_get_loaded_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_loaded_extensions**\ (\ ) |const| :ref:`🔗<class_GDExtensionManager_method_get_loaded_extensions>`

Trả về các đường dẫn tệp của tất cả extension hiện đang được tải.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_is_extension_loaded:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_extension_loaded**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_GDExtensionManager_method_is_extension_loaded>`

Trả về ``true`` nếu extension tại ``path`` tệp đã cho đã được tải thành công. Xem thêm :ref:`get_loaded_extensions()<class_GDExtensionManager_method_get_loaded_extensions>`.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_load_extension:

.. rst-class:: classref-method

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **load_extension**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDExtensionManager_method_load_extension>`

Tải một extension bằng đường dẫn tệp tuyệt đối. ``path`` cần trỏ đến một :ref:`GDExtension<class_GDExtension>` hợp lệ. Trả về :ref:`LOAD_STATUS_OK<class_GDExtensionManager_constant_LOAD_STATUS_OK>` nếu thành công.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_load_extension_from_function:

.. rst-class:: classref-method

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **load_extension_from_function**\ (\ path\: :ref:`String<class_String>`, init_func\: ``const GDExtensionInitializationFunction*``\ ) :ref:`🔗<class_GDExtensionManager_method_load_extension_from_function>`

Tải extension đã có trong address space thông qua path và initialization function được cung cấp. ``path`` cần là duy nhất và bắt đầu bằng ``"libgodot://"``. Trả về :ref:`LOAD_STATUS_OK<class_GDExtensionManager_constant_LOAD_STATUS_OK>` nếu thành công.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_reload_extension:

.. rst-class:: classref-method

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **reload_extension**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDExtensionManager_method_reload_extension>`

Tải lại extension tại path tệp đã cho. ``path`` cần trỏ đến một :ref:`GDExtension<class_GDExtension>` hợp lệ; nếu không, method này có thể trả về :ref:`LOAD_STATUS_NOT_LOADED<class_GDExtensionManager_constant_LOAD_STATUS_NOT_LOADED>` hoặc :ref:`LOAD_STATUS_FAILED<class_GDExtensionManager_constant_LOAD_STATUS_FAILED>`.

\ **Lưu ý:** Bạn chỉ có thể tải lại extension trong editor. Trong các bản build release, method này luôn thất bại và trả về :ref:`LOAD_STATUS_FAILED<class_GDExtensionManager_constant_LOAD_STATUS_FAILED>`.

.. rst-class:: classref-item-separator

----

.. _class_GDExtensionManager_method_unload_extension:

.. rst-class:: classref-method

:ref:`LoadStatus<enum_GDExtensionManager_LoadStatus>` **unload_extension**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDExtensionManager_method_unload_extension>`

Gỡ tải một extension theo đường dẫn tệp. ``path`` cần trỏ đến một :ref:`GDExtension<class_GDExtension>` đã được tải; nếu không, method này trả về :ref:`LOAD_STATUS_NOT_LOADED<class_GDExtensionManager_constant_LOAD_STATUS_NOT_LOADED>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
