:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GDExtension.xml.

.. _class_GDExtension:

GDExtension
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một thư viện native cho GDExtension.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu resource **GDExtension** đại diện cho một `shared library <https://en.wikipedia.org/wiki/Shared_library>`__ có thể mở rộng chức năng của engine. Singleton :ref:`GDExtensionManager<class_GDExtensionManager>` chịu trách nhiệm tải, tải lại và gỡ tải các resource **GDExtension**.

\ **Lưu ý:** Bản thân GDExtension không phải là ngôn ngữ scripting và không liên quan đến các resource :ref:`GDScript<class_GDScript>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tổng quan về GDExtension <../engine_details/engine_api/gdextension/what_is_gdextension>`

- :doc:`Ví dụ GDExtension bằng C++ <../tutorials/scripting/cpp/gdextension_cpp_example>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` | :ref:`get_minimum_library_initialization_level<class_GDExtension_method_get_minimum_library_initialization_level>`\ (\ ) |const| |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_library_open<class_GDExtension_method_is_library_open>`\ (\ ) |const|                                                   |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GDExtension_InitializationLevel:

.. rst-class:: classref-enumeration

enum **InitializationLevel**: :ref:`🔗<enum_GDExtension_InitializationLevel>`

.. _class_GDExtension_constant_INITIALIZATION_LEVEL_CORE:

.. rst-class:: classref-enumeration-constant

:ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` **INITIALIZATION_LEVEL_CORE** = ``0``

Thư viện được khởi tạo cùng lúc với các tính năng cốt lõi của engine.

.. _class_GDExtension_constant_INITIALIZATION_LEVEL_SERVERS:

.. rst-class:: classref-enumeration-constant

:ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` **INITIALIZATION_LEVEL_SERVERS** = ``1``

Thư viện được khởi tạo cùng lúc với các server của engine (chẳng hạn như :ref:`RenderingServer<class_RenderingServer>` hoặc :ref:`PhysicsServer3D<class_PhysicsServer3D>`).

.. _class_GDExtension_constant_INITIALIZATION_LEVEL_SCENE:

.. rst-class:: classref-enumeration-constant

:ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` **INITIALIZATION_LEVEL_SCENE** = ``2``

Thư viện được khởi tạo cùng lúc với các class liên quan đến scene của engine.

.. _class_GDExtension_constant_INITIALIZATION_LEVEL_EDITOR:

.. rst-class:: classref-enumeration-constant

:ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` **INITIALIZATION_LEVEL_EDITOR** = ``3``

Thư viện được khởi tạo cùng lúc với các class editor của engine. Chỉ xảy ra khi tải GDExtension trong editor.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GDExtension_method_get_minimum_library_initialization_level:

.. rst-class:: classref-method

:ref:`InitializationLevel<enum_GDExtension_InitializationLevel>` **get_minimum_library_initialization_level**\ (\ ) |const| :ref:`🔗<class_GDExtension_method_get_minimum_library_initialization_level>`

Trả về level thấp nhất cần thiết để extension này được khởi tạo đúng cách (xem enum :ref:`InitializationLevel<enum_GDExtension_InitializationLevel>`).

.. rst-class:: classref-item-separator

----

.. _class_GDExtension_method_is_library_open:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_library_open**\ (\ ) |const| :ref:`🔗<class_GDExtension_method_is_library_open>`

Trả về ``true`` nếu thư viện của extension này đã được mở.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
