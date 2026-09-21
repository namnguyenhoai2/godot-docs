:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeBlend3.xml.

.. _class_AnimationNodeBlend3:

AnimationNodeBlend3
===================

**Kế thừa:** :ref:`AnimationNodeSync<class_AnimationNodeSync>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Trộn tuyến tính hai trong số ba animation bên trong một :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource để thêm vào :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Trộn tuyến tính hai animation trong số ba animation dựa trên giá trị amount.

Animation node này có ba đầu vào:

- Animation cơ sở để trộn cùng

- Một animation "-blend" để trộn cùng khi blend amount là giá trị âm

- Một animation "+blend" để trộn cùng khi blend amount là giá trị dương

Nhìn chung, giá trị blend nên nằm trong phạm vi ``[-1.0, 1.0]``. Các giá trị nằm ngoài phạm vi này có thể trộn các animation được khuếch đại; tuy nhiên, :ref:`AnimationNodeAdd3<class_AnimationNodeAdd3>` phù hợp hơn cho mục đích này.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
