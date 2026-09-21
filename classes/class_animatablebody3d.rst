:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimatableBody3D.xml.

.. _class_AnimatableBody3D:

AnimatableBody3D
================

**Kế thừa:** :ref:`StaticBody3D<class_StaticBody3D>` **<** :ref:`PhysicsBody3D<class_PhysicsBody3D>` **<** :ref:`CollisionObject3D<class_CollisionObject3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics body 3D không thể bị di chuyển bởi các lực bên ngoài. Khi được di chuyển thủ công, nó sẽ tác động đến các body khác trên đường đi của nó.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một physics body 2D có thể được tạo hiệu ứng chuyển động. Nó không thể bị di chuyển bởi các lực hoặc va chạm bên ngoài, nhưng có thể được di chuyển thủ công bằng các phương thức khác, chẳng hạn như bằng mã, :ref:`AnimationMixer<class_AnimationMixer>`\ s (với :ref:`AnimationMixer.callback_mode_process<class_AnimationMixer_property_callback_mode_process>` được đặt thành :ref:`AnimationMixer.ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS<class_AnimationMixer_constant_ANIMATION_CALLBACK_MODE_PROCESS_PHYSICS>`), và :ref:`RemoteTransform3D<class_RemoteTransform3D>`.

Khi **AnimatableBody3D** được di chuyển, vận tốc tuyến tính và vận tốc góc của nó được ước tính và dùng để tác động đến các physics body khác trên đường đi của nó. Điều này khiến nó hữu ích cho các platform, cửa và những đối tượng chuyển động khác.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Physics introduction <../tutorials/physics/physics_introduction>`

- :doc:`Troubleshooting physics issues <../tutorials/physics/troubleshooting_physics_issues>`

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+-------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>` | :ref:`sync_to_physics<class_AnimatableBody3D_property_sync_to_physics>` | ``true`` |
   +-------------------------+-------------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimatableBody3D_property_sync_to_physics:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **sync_to_physics** = ``true`` :ref:`🔗<class_AnimatableBody3D_property_sync_to_physics>`

.. rst-class:: classref-property-setget

- |void| **set_sync_to_physics**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_sync_to_physics_enabled**\ (\ )

Nếu ``true``, chuyển động của body sẽ được đồng bộ hóa với physics frame. Điều này hữu ích khi tạo chuyển động thông qua :ref:`AnimationPlayer<class_AnimationPlayer>`, chẳng hạn như trên các platform chuyển động. **Không** sử dụng cùng với :ref:`PhysicsBody3D.move_and_collide()<class_PhysicsBody3D_method_move_and_collide>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
