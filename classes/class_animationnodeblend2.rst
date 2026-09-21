:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeBlend2.xml.

.. _class_AnimationNodeBlend2:

AnimationNodeBlend2
===================

**Kế thừa:** :ref:`AnimationNodeSync<class_AnimationNodeSync>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Trộn tuyến tính hai animation bên trong một :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource để thêm vào :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Trộn tuyến tính hai animation dựa trên giá trị amount.

Nhìn chung, giá trị blend nên nằm trong phạm vi ``[0.0, 1.0]``. Các giá trị nằm ngoài phạm vi này có thể trộn các animation được khuếch đại hoặc đảo ngược; tuy nhiên, :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>` phù hợp hơn cho mục đích này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
