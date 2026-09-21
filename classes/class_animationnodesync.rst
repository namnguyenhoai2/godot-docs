:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AnimationNodeSync.xml.

.. _class_AnimationNodeSync:

AnimationNodeSync
=================

**Kế thừa:** :ref:`AnimationNode<class_AnimationNode>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AnimationNodeAdd2<class_AnimationNodeAdd2>`, :ref:`AnimationNodeAdd3<class_AnimationNodeAdd3>`, :ref:`AnimationNodeBlend2<class_AnimationNodeBlend2>`, :ref:`AnimationNodeBlend3<class_AnimationNodeBlend3>`, :ref:`AnimationNodeOneShot<class_AnimationNodeOneShot>`, :ref:`AnimationNodeSub2<class_AnimationNodeSub2>`, :ref:`AnimationNodeTransition<class_AnimationNodeTransition>`

Base class for :ref:`AnimationNode<class_AnimationNode>`\ s with multiple input ports that must be synchronized.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node animation được dùng để kết hợp, trộn hoặc blend từ hai animation trở lên với nhau, đồng thời giữ chúng đồng bộ trong một :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using AnimationTree <../tutorials/animation/animation_tree>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`sync<class_AnimationNodeSync_property_sync>` | ``false`` |
   +-------------------------+----------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AnimationNodeSync_property_sync:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **sync** = ``false`` :ref:`🔗<class_AnimationNodeSync_property_sync>`

.. rst-class:: classref-property-setget

- |void| **set_use_sync**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_sync**\ (\ )

Nếu ``false``, frame của các animation đã blend sẽ dừng lại khi giá trị blend là ``0``.

Nếu ``true``, buộc các animation đã blend tiến thêm một frame.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
