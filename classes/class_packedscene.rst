:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedScene.xml.

.. _class_PackedScene:

PackedScene
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một abstraction của scene đã được serialize.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một interface đơn giản hóa cho tệp scene. Cung cấp quyền truy cập vào các thao tác và kiểm tra có thể thực hiện trên chính scene resource.

Có thể được dùng để lưu một node vào tệp. Khi lưu, node cũng như tất cả các node mà nó sở hữu sẽ được lưu (xem property :ref:`Node.owner<class_Node_property_owner>`).

\ **Lưu ý:** Node không cần phải sở hữu chính nó.

\ **Ví dụ:** Load một scene đã lưu:


.. tabs::

 .. code-tab:: gdscript

    # Dùng load() thay vì preload() nếu path chưa được biết tại thời điểm compile.
    var scene = preload("res://scene.tscn").instantiate()
    # Thêm node làm node con của node mà script được gắn vào.
    add_child(scene)

 .. code-tab:: csharp

    // C# không có preload, vì vậy bạn luôn phải dùng ResourceLoader.Load<PackedScene>().
    var scene = ResourceLoader.Load<PackedScene>("res://scene.tscn").Instantiate();
    // Thêm node làm node con của node mà script được gắn vào.
    AddChild(scene);



\ **Ví dụ:** Lưu một node với các owner khác nhau. Ví dụ sau tạo 3 object: :ref:`Node2D<class_Node2D>` (``node``), :ref:`RigidBody2D<class_RigidBody2D>` (``body``) và :ref:`CollisionObject2D<class_CollisionObject2D>` (``collision``). ``collision`` là node con của ``body``, vốn là node con của ``node``. Chỉ ``body`` được ``node`` sở hữu, do đó :ref:`pack()<class_PackedScene_method_pack>` sẽ chỉ lưu hai node đó, nhưng không lưu ``collision``.


.. tabs::

 .. code-tab:: gdscript

    # Tạo các object.
    var node = Node2D.new()
    var body = RigidBody2D.new()
    var collision = CollisionShape2D.new()

    # Tạo hierarchy của các object.
    body.add_child(collision)
    node.add_child(body)

    # Thay đổi owner của `body`, nhưng không thay đổi owner của `collision`.
    body.owner = node
    var scene = PackedScene.new()

    # Giờ chỉ `node` và `body` được pack.
    var result = scene.pack(node)
    if result == OK:
        var error = ResourceSaver.save(scene, "res://path/name.tscn")  # Hoặc "user://..."
        if error != OK:
            push_error("An error occurred while saving the scene to disk.")

 .. code-tab:: csharp

    // Tạo các object.
    var node = new Node2D();
    var body = new RigidBody2D();
    var collision = new CollisionShape2D();

    // Tạo hierarchy của các object.
    body.AddChild(collision);
    node.AddChild(body);

    // Thay đổi owner của `body`, nhưng không thay đổi owner của `collision`.
    body.Owner = node;
    var scene = new PackedScene();

    // Giờ chỉ `node` và `body` được pack.
    Error result = scene.Pack(node);
    if (result == Error.Ok)
    {
        Error error = ResourceSaver.Save(scene, "res://path/name.tscn"); // Hoặc "user://..."
        if (error != Error.Ok)
        {
            GD.PushError("An error occurred while saving the scene to disk.");
        }
    }



.. rst-class:: classref-introduction-group

Tutorials
---------

- `2D Role Playing Game (RPG) Demo <https://godotengine.org/asset-library/asset/2729>`__

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`can_instantiate<class_PackedScene_method_can_instantiate>`\ (\ ) |const|                                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SceneState<class_SceneState>`   | :ref:`get_state<class_PackedScene_method_get_state>`\ (\ ) |const|                                                                          |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`               | :ref:`instantiate<class_PackedScene_method_instantiate>`\ (\ edit_state\: :ref:`GenEditState<enum_PackedScene_GenEditState>` = 0\ ) |const| |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`pack<class_PackedScene_method_pack>`\ (\ path\: :ref:`Node<class_Node>`\ )                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_PackedScene_GenEditState:

.. rst-class:: classref-enumeration

enum **GenEditState**: :ref:`🔗<enum_PackedScene_GenEditState>`

.. _class_PackedScene_constant_GEN_EDIT_STATE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`GenEditState<enum_PackedScene_GenEditState>` **GEN_EDIT_STATE_DISABLED** = ``0``

Nếu được truyền vào :ref:`instantiate()<class_PackedScene_method_instantiate>`, sẽ chặn việc chỉnh sửa scene state.

.. _class_PackedScene_constant_GEN_EDIT_STATE_INSTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`GenEditState<enum_PackedScene_GenEditState>` **GEN_EDIT_STATE_INSTANCE** = ``1``

Nếu được truyền vào :ref:`instantiate()<class_PackedScene_method_instantiate>`, sẽ cung cấp local scene resource cho local scene.

\ **Lưu ý:** Chỉ khả dụng trong các bản build editor.

.. _class_PackedScene_constant_GEN_EDIT_STATE_MAIN:

.. rst-class:: classref-enumeration-constant

:ref:`GenEditState<enum_PackedScene_GenEditState>` **GEN_EDIT_STATE_MAIN** = ``2``

Nếu được truyền vào :ref:`instantiate()<class_PackedScene_method_instantiate>`, sẽ cung cấp local scene resource cho local scene. Chỉ main scene mới nên nhận main edit state.

\ **Lưu ý:** Chỉ khả dụng trong các bản build editor.

.. _class_PackedScene_constant_GEN_EDIT_STATE_MAIN_INHERITED:

.. rst-class:: classref-enumeration-constant

:ref:`GenEditState<enum_PackedScene_GenEditState>` **GEN_EDIT_STATE_MAIN_INHERITED** = ``3``

Tương tự như :ref:`GEN_EDIT_STATE_MAIN<class_PackedScene_constant_GEN_EDIT_STATE_MAIN>`, nhưng áp dụng khi scene đang được instantiate để làm base của một scene khác.

\ **Lưu ý:** Chỉ khả dụng trong các bản build editor.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_PackedScene_method_can_instantiate:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_instantiate**\ (\ ) |const| :ref:`🔗<class_PackedScene_method_can_instantiate>`

Trả về ``true`` nếu tệp scene có các node.

.. rst-class:: classref-item-separator

----

.. _class_PackedScene_method_get_state:

.. rst-class:: classref-method

:ref:`SceneState<class_SceneState>` **get_state**\ (\ ) |const| :ref:`🔗<class_PackedScene_method_get_state>`

Trả về :ref:`SceneState<class_SceneState>` đại diện cho nội dung của tệp scene.

.. rst-class:: classref-item-separator

----

.. _class_PackedScene_method_instantiate:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **instantiate**\ (\ edit_state\: :ref:`GenEditState<enum_PackedScene_GenEditState>` = 0\ ) |const| :ref:`🔗<class_PackedScene_method_instantiate>`

Instantiate hierarchy node của scene. Kích hoạt việc instantiate các child scene. Kích hoạt notification :ref:`Node.NOTIFICATION_SCENE_INSTANTIATED<class_Node_constant_NOTIFICATION_SCENE_INSTANTIATED>` trên root node.

.. rst-class:: classref-item-separator

----

.. _class_PackedScene_method_pack:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **pack**\ (\ path\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_PackedScene_method_pack>`

Pack node ``path`` và tất cả sub-node được sở hữu vào **PackedScene** này. Mọi dữ liệu hiện có sẽ bị xóa. Xem :ref:`Node.owner<class_Node_property_owner>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
