:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/multiplayer/doc_classes/MultiplayerSpawner.xml.

.. _class_MultiplayerSpawner:

MultiplayerSpawner
==================

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Tự động replicate các node có thể spawn từ authority đến các peer multiplayer khác.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các scene có thể spawn được cấu hình trong editor hoặc thông qua code (xem :ref:`add_spawnable_scene()<class_MultiplayerSpawner_method_add_spawnable_scene>`).

Cũng hỗ trợ spawn node tùy chỉnh thông qua :ref:`spawn()<class_MultiplayerSpawner_method_spawn>`, bằng cách gọi :ref:`spawn_function<class_MultiplayerSpawner_property_spawn_function>` trên tất cả peer.

Về bên trong, **MultiplayerSpawner** sử dụng :ref:`MultiplayerAPI.object_configuration_add()<class_MultiplayerAPI_method_object_configuration_add>` để thông báo việc spawn, truyền node đã spawn làm ``object`` và chính nó làm ``configuration``, còn :ref:`MultiplayerAPI.object_configuration_remove()<class_MultiplayerAPI_method_object_configuration_remove>` để thông báo việc despawn theo cách tương tự.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-------------------------------------------------------------------------+------------------+
   | :ref:`Callable<class_Callable>` | :ref:`spawn_function<class_MultiplayerSpawner_property_spawn_function>` |                  |
   +---------------------------------+-------------------------------------------------------------------------+------------------+
   | :ref:`int<class_int>`           | :ref:`spawn_limit<class_MultiplayerSpawner_property_spawn_limit>`       | ``0``            |
   +---------------------------------+-------------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`spawn_path<class_MultiplayerSpawner_property_spawn_path>`         | ``NodePath("")`` |
   +---------------------------------+-------------------------------------------------------------------------+------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | |void|                      | :ref:`add_spawnable_scene<class_MultiplayerSpawner_method_add_spawnable_scene>`\ (\ path\: :ref:`String<class_String>`\ )    |
   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | |void|                      | :ref:`clear_spawnable_scenes<class_MultiplayerSpawner_method_clear_spawnable_scenes>`\ (\ )                                  |
   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_spawnable_scene<class_MultiplayerSpawner_method_get_spawnable_scene>`\ (\ index\: :ref:`int<class_int>`\ ) |const| |
   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`get_spawnable_scene_count<class_MultiplayerSpawner_method_get_spawnable_scene_count>`\ (\ ) |const|                    |
   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`     | :ref:`spawn<class_MultiplayerSpawner_method_spawn>`\ (\ data\: :ref:`Variant<class_Variant>` = null\ )                       |
   +-----------------------------+------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_MultiplayerSpawner_signal_despawned:

.. rst-class:: classref-signal

**despawned**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_MultiplayerSpawner_signal_despawned>`

Được phát khi một scene có thể spawn hoặc một custom spawn bị authority multiplayer despawn. Chỉ được gọi trên các peer từ xa.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_signal_spawned:

.. rst-class:: classref-signal

**spawned**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_MultiplayerSpawner_signal_spawned>`

Được phát khi một scene có thể spawn hoặc một custom spawn được authority multiplayer spawn. Chỉ được gọi trên các peer từ xa.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiplayerSpawner_property_spawn_function:

.. rst-class:: classref-property

:ref:`Callable<class_Callable>` **spawn_function** :ref:`🔗<class_MultiplayerSpawner_property_spawn_function>`

.. rst-class:: classref-property-setget

- |void| **set_spawn_function**\ (\ value\: :ref:`Callable<class_Callable>`\ ) - :ref:`Callable<class_Callable>` **get_spawn_function**\ (\ )

Phương thức được gọi trên tất cả peer khi authority yêu cầu một :ref:`spawn()<class_MultiplayerSpawner_method_spawn>` tùy chỉnh. Phương thức sẽ nhận tham số ``data`` và phải trả về một :ref:`Node<class_Node>` không nằm trong scene tree.

\ **Lưu ý:** Node được trả về **không được** thêm vào scene bằng :ref:`Node.add_child()<class_Node_method_add_child>`. Việc này được thực hiện tự động.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_property_spawn_limit:

.. rst-class:: classref-property

:ref:`int<class_int>` **spawn_limit** = ``0`` :ref:`🔗<class_MultiplayerSpawner_property_spawn_limit>`

.. rst-class:: classref-property-setget

- |void| **set_spawn_limit**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spawn_limit**\ (\ )

Số node tối đa được phép spawn bởi spawner này. Bao gồm cả các scene có thể spawn và các custom spawn.

Khi được đặt thành ``0`` (mặc định), sẽ không có giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_property_spawn_path:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **spawn_path** = ``NodePath("")`` :ref:`🔗<class_MultiplayerSpawner_property_spawn_path>`

.. rst-class:: classref-property-setget

- |void| **set_spawn_path**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_spawn_path**\ (\ )

Đường dẫn đến root của các spawn. Các scene có thể spawn được thêm làm child trực tiếp sẽ được replicate đến các peer khác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerSpawner_method_add_spawnable_scene:

.. rst-class:: classref-method

|void| **add_spawnable_scene**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_MultiplayerSpawner_method_add_spawnable_scene>`

Thêm một đường dẫn scene vào các scene có thể spawn, khiến scene đó tự động được replicate từ authority multiplayer đến các peer khác khi được thêm làm child của node được :ref:`spawn_path<class_MultiplayerSpawner_property_spawn_path>` trỏ đến.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_method_clear_spawnable_scenes:

.. rst-class:: classref-method

|void| **clear_spawnable_scenes**\ (\ ) :ref:`🔗<class_MultiplayerSpawner_method_clear_spawnable_scenes>`

Xóa tất cả scene có thể spawn. Không despawn các instance hiện có trên các peer từ xa.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_method_get_spawnable_scene:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_spawnable_scene**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiplayerSpawner_method_get_spawnable_scene>`

Trả về đường dẫn scene có thể spawn theo index.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_method_get_spawnable_scene_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_spawnable_scene_count**\ (\ ) |const| :ref:`🔗<class_MultiplayerSpawner_method_get_spawnable_scene_count>`

Trả về số lượng đường dẫn scene có thể spawn.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSpawner_method_spawn:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **spawn**\ (\ data\: :ref:`Variant<class_Variant>` = null\ ) :ref:`🔗<class_MultiplayerSpawner_method_spawn>`

Yêu cầu một custom spawn, với ``data`` được truyền vào :ref:`spawn_function<class_MultiplayerSpawner_property_spawn_function>` trên tất cả peer. Trả về instance node được spawn cục bộ, đã nằm trong scene tree và được thêm làm child của node được :ref:`spawn_path<class_MultiplayerSpawner_property_spawn_path>` trỏ đến.

\ **Lưu ý:** Các scene có thể spawn được spawn tự động. :ref:`spawn()<class_MultiplayerSpawner_method_spawn>` chỉ cần thiết cho các custom spawn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
