:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/JacobianIK3D.xml.

.. _class_JacobianIK3D:

JacobianIK3D
============

**Kế thừa:** :ref:`IterateIK3D<class_IterateIK3D>` **<** :ref:`ChainIK3D<class_ChainIK3D>` **<** :ref:`IKModifier3D<class_IKModifier3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ giải động học ngược dựa trên phép chuyển vị Jacobian.

.. rst-class:: classref-introduction-group

Mô tả
-----

**JacobianIK3D** tính toán phép xoay cho tất cả các khớp cùng lúc, tạo ra chuyển động tự nhiên và mượt mà. Bộ giải đặc biệt phù hợp với các animation sinh học.

Độ xoắn kết quả quanh vector hướng tiến sẽ luôn được giữ lại từ pose trước đó.

\ **Lưu ý:** Bộ giải hội tụ chậm hơn các bộ giải IK khác, dẫn đến việc theo dõi mục tiêu nhẹ nhàng hơn và ít tức thời hơn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
