:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CCDIK3D.xml.

.. _class_CCDIK3D:

CCDIK3D
=======

**Kế thừa:** :ref:`IterateIK3D<class_IterateIK3D>` **<** :ref:`ChainIK3D<class_ChainIK3D>` **<** :ref:`IKModifier3D<class_IKModifier3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ giải inverse kinematics dựa trên phép xoay, sử dụng cyclic coordinate descent.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CCDIK3D** là IK dựa trên phép xoay, cho phép theo dõi nhanh và hiệu quả ngay cả khi các khớp xoay ở góc lớn. Nó đặc biệt phù hợp với các chuỗi có giới hạn, mang lại khả năng theo dõi mục tiêu mượt mà và ổn định hơn so với :ref:`FABRIK3D<class_FABRIK3D>`.

Độ xoắn kết quả quanh vector hướng về phía trước sẽ luôn được giữ lại từ pose trước đó.

\ **Lưu ý:** Khi mục tiêu ở gần root, điều này có thể gây ra chuyển động không tự nhiên, bao gồm hiện tượng lật khớp và dao động.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
