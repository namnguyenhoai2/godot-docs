:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeSub2.xml.

.. _class_AnimationNodeSub2:

AnimationNodeSub2
=================

**Kế thừa:** :ref:`AnimationNodeSync<class_AnimationNodeSync>` **<** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Trộn hai animation theo phép trừ bên trong :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource để thêm vào :ref:`AnimationNodeBlendTree<class_AnimationNodeBlendTree>`. Trộn hai animation theo phép trừ dựa trên giá trị amount.

Animation node này thường được dùng để tính toán trước nhằm loại bỏ mọi pose dư thừa khỏi animation cho animation source "add" trong :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>` hoặc :ref:`AnimationNodeAdd3<class_AnimationNodeAdd3>`.

Nhìn chung, giá trị blend nên nằm trong khoảng ``[0.0, 1.0]``, nhưng có thể sử dụng các giá trị nằm ngoài khoảng này để tạo animation được khuếch đại hoặc đảo ngược.

\ **Lưu ý:** Phép tính này khác với việc sử dụng giá trị âm trong :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>`, vì các ma trận biến đổi không tuân theo luật giao hoán. **AnimationNodeSub2** nhân ma trận biến đổi của animation đảo ngược từ phía bên trái, trong khi :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>` âm nhân nó từ phía bên phải.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`AnimationTree <../tutorials/animation/animation_tree>`

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
