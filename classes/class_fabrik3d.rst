:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FABRIK3D.xml.

.. _class_FABRIK3D:

FABRIK3D
========

**Kế thừa:** :ref:`IterateIK3D<class_IterateIK3D>` **<** :ref:`ChainIK3D<class_ChainIK3D>` **<** :ref:`IKModifier3D<class_IKModifier3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ giải động học ngược dựa trên vị trí, sử dụng phương pháp tiếp cận xuôi và ngược.

.. rst-class:: classref-introduction-group

Mô tả
-----

**FABRIK3D** là IK dựa trên vị trí, cho phép theo dõi mục tiêu một cách chính xác. Nó lý tưởng cho các chuỗi đơn giản không có giới hạn.

Độ xoắn quanh vector hướng tiến sẽ luôn được giữ nguyên từ pose trước đó.

\ **Lưu ý:** Khi mục tiêu ở gần root, nó có xu hướng tạo ra các dạng ziczac, dẫn đến chuyển động trực quan không tự nhiên.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Inverse Kinematics Returns to Godot 4.6 - IKModifier3D <https://godotengine.org/article/inverse-kinematics-returns-to-godot-4-6/#ikmodifier3d-and-7-child-classes>`__

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
