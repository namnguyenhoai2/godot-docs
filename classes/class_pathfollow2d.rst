:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PathFollow2D.xml.

.. _class_PathFollow2D:

PathFollow2D
============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ lấy mẫu điểm cho một :ref:`Path2D<class_Path2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này nhận :ref:`Path2D<class_Path2D>` của nó, rồi trả về tọa độ của một điểm bên trong đó, dựa trên khoảng cách tính từ vertex đầu tiên.

Nó hữu ích khi muốn các node khác đi theo một path mà không cần lập trình mẫu chuyển động. Để làm vậy, các node đó phải là node con của node này. Sau đó, các node hậu duệ sẽ di chuyển tương ứng khi thiết lập :ref:`progress<class_PathFollow2D_property_progress>` trong node này.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`cubic_interp<class_PathFollow2D_property_cubic_interp>`     | ``true`` |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`h_offset<class_PathFollow2D_property_h_offset>`             | ``0.0``  |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`loop<class_PathFollow2D_property_loop>`                     | ``true`` |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`progress<class_PathFollow2D_property_progress>`             | ``0.0``  |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`progress_ratio<class_PathFollow2D_property_progress_ratio>` | ``0.0``  |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`   | :ref:`rotates<class_PathFollow2D_property_rotates>`               | ``true`` |
   +---------------------------+-------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`v_offset<class_PathFollow2D_property_v_offset>`             | ``0.0``  |
   +---------------------------+-------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PathFollow2D_property_cubic_interp:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cubic_interp** = ``true`` :ref:`🔗<class_PathFollow2D_property_cubic_interp>`

.. rst-class:: classref-property-setget

- |void| **set_cubic_interpolation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_cubic_interpolation**\ (\ )

Nếu ``true``, vị trí giữa hai điểm được lưu vào bộ nhớ đệm sẽ được nội suy theo cubic; nếu không thì nội suy theo linear.

Các điểm dọc theo :ref:`Curve2D<class_Curve2D>` của :ref:`Path2D<class_Path2D>` được tính trước khi sử dụng để tính toán nhanh hơn. Sau đó, điểm tại offset được yêu cầu sẽ được tính bằng cách nội suy giữa hai điểm liền kề được lưu vào bộ nhớ đệm. Điều này có thể gây ra vấn đề nếu curve có những đoạn rẽ gấp, vì các điểm được lưu vào bộ nhớ đệm có thể không bám sát curve đủ.

Có hai cách giải quyết vấn đề này: tăng số lượng điểm được lưu vào bộ nhớ đệm và tăng mức sử dụng bộ nhớ, hoặc nội suy cubic giữa hai điểm với cái giá là việc tính toán chậm hơn (một chút).

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_h_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **h_offset** = ``0.0`` :ref:`🔗<class_PathFollow2D_property_h_offset>`

.. rst-class:: classref-property-setget

- |void| **set_h_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_h_offset**\ (\ )

Offset của node dọc theo curve.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **loop** = ``true`` :ref:`🔗<class_PathFollow2D_property_loop>`

.. rst-class:: classref-property-setget

- |void| **set_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_loop**\ (\ )

Nếu ``true``, mọi offset nằm ngoài độ dài của path sẽ được lặp vòng thay vì dừng lại ở các đầu mút. Hãy dùng thuộc tính này cho các path tuần hoàn.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_progress:

.. rst-class:: classref-property

:ref:`float<class_float>` **progress** = ``0.0`` :ref:`🔗<class_PathFollow2D_property_progress>`

.. rst-class:: classref-property-setget

- |void| **set_progress**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_progress**\ (\ )

Khoảng cách dọc theo path, tính bằng pixel. Việc thay đổi giá trị này sẽ đặt vị trí của node này vào một điểm bên trong path.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_progress_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **progress_ratio** = ``0.0`` :ref:`🔗<class_PathFollow2D_property_progress_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_progress_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_progress_ratio**\ (\ )

Khoảng cách dọc theo path dưới dạng một số trong phạm vi từ 0.0 (đối với vertex đầu tiên) đến 1.0 (đối với vertex cuối cùng). Đây chỉ là một cách khác để biểu diễn progress bên trong path, vì offset được cung cấp sẽ được nhân với độ dài của path ở bên trong.

Chỉ có thể set hoặc get giá trị này nếu **PathFollow2D** là node con của một :ref:`Path2D<class_Path2D>` thuộc scene tree, và :ref:`Path2D<class_Path2D>` này có một :ref:`Curve2D<class_Curve2D>` với độ dài khác không. Nếu không, việc cố set trường này sẽ in ra lỗi, còn việc get trường này sẽ trả về ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_rotates:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **rotates** = ``true`` :ref:`🔗<class_PathFollow2D_property_rotates>`

.. rst-class:: classref-property-setget

- |void| **set_rotates**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_rotating**\ (\ )

Nếu ``true``, node này sẽ xoay để đi theo path, với hướng +X hướng về phía trước trên path.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow2D_property_v_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **v_offset** = ``0.0`` :ref:`🔗<class_PathFollow2D_property_v_offset>`

.. rst-class:: classref-property-setget

- |void| **set_v_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_v_offset**\ (\ )

Offset của node vuông góc với curve.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
