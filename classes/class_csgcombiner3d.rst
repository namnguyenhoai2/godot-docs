:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGCombiner3D.xml.

.. _class_CSGCombiner3D:

CSGCombiner3D
=============

**Kế thừa:** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một CSG node cho phép bạn kết hợp các CSG modifier khác.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối với những sắp xếp hình dạng phức tạp, đôi khi cần thêm cấu trúc vào các CSG node của bạn. Node CSGCombiner3D cho phép bạn tạo cấu trúc này. Node này đóng gói kết quả của các phép toán CSG trên các node con của nó. Nhờ đó, bạn có thể thực hiện các phép toán trên một tập hợp hình dạng là các node con của một CSGCombiner3D node, thực hiện một tập hợp phép toán riêng biệt trên tập hợp hình dạng thứ hai là các node con của một CSGCombiner3D node thứ hai, rồi thực hiện một phép toán lấy hai kết quả cuối cùng đó làm đầu vào để tạo hình dạng cuối cùng.

\ **Lưu ý:** Các CSG node được thiết kế để sử dụng trong việc dựng prototype cho level. Việc tạo CSG node có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` bằng :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một CSG node bên trong một CSG node khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong gameplay.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tạo nguyên mẫu level bằng CSG <../tutorials/3d/csg_tools>`

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
