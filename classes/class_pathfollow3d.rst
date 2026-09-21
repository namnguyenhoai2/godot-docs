:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PathFollow3D.xml.

.. _class_PathFollow3D:

PathFollow3D
============

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ lấy mẫu điểm cho một :ref:`Path3D<class_Path3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này nhận :ref:`Path3D<class_Path3D>` của nó và trả về tọa độ của một điểm bên trong nó, dựa trên khoảng cách tính từ đỉnh đầu tiên.

Nó hữu ích khi muốn các node khác đi theo một đường dẫn mà không cần lập trình mẫu chuyển động. Để làm vậy, các node đó phải là node con của node này. Sau đó, các node hậu duệ sẽ di chuyển tương ứng khi thiết lập :ref:`progress<class_PathFollow3D_property_progress>` trong node này.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`cubic_interp<class_PathFollow3D_property_cubic_interp>`       | ``true``  |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                           | :ref:`h_offset<class_PathFollow3D_property_h_offset>`               | ``0.0``   |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`loop<class_PathFollow3D_property_loop>`                       | ``true``  |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                           | :ref:`progress<class_PathFollow3D_property_progress>`               | ``0.0``   |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                           | :ref:`progress_ratio<class_PathFollow3D_property_progress_ratio>`   | ``0.0``   |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`RotationMode<enum_PathFollow3D_RotationMode>` | :ref:`rotation_mode<class_PathFollow3D_property_rotation_mode>`     | ``3``     |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`tilt_enabled<class_PathFollow3D_property_tilt_enabled>`       | ``true``  |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`use_model_front<class_PathFollow3D_property_use_model_front>` | ``false`` |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                           | :ref:`v_offset<class_PathFollow3D_property_v_offset>`               | ``0.0``   |
   +-----------------------------------------------------+---------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>` | :ref:`correct_posture<class_PathFollow3D_method_correct_posture>`\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, rotation_mode\: :ref:`RotationMode<enum_PathFollow3D_RotationMode>`\ ) |static| |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_PathFollow3D_RotationMode:

.. rst-class:: classref-enumeration

enum **RotationMode**: :ref:`🔗<enum_PathFollow3D_RotationMode>`

.. _class_PathFollow3D_constant_ROTATION_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **ROTATION_NONE** = ``0``

Ngăn PathFollow3D xoay.

.. _class_PathFollow3D_constant_ROTATION_Y:

.. rst-class:: classref-enumeration-constant

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **ROTATION_Y** = ``1``

Cho phép PathFollow3D chỉ xoay quanh trục Y.

.. _class_PathFollow3D_constant_ROTATION_XY:

.. rst-class:: classref-enumeration-constant

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **ROTATION_XY** = ``2``

Cho phép PathFollow3D xoay quanh cả hai trục X và Y.

.. _class_PathFollow3D_constant_ROTATION_XYZ:

.. rst-class:: classref-enumeration-constant

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **ROTATION_XYZ** = ``3``

Cho phép PathFollow3D xoay quanh bất kỳ trục nào.

.. _class_PathFollow3D_constant_ROTATION_ORIENTED:

.. rst-class:: classref-enumeration-constant

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **ROTATION_ORIENTED** = ``4``

Uses the up vector information in a :ref:`Curve3D<class_Curve3D>` to enforce orientation. This rotation mode requires the :ref:`Path3D<class_Path3D>`'s :ref:`Curve3D.up_vector_enabled<class_Curve3D_property_up_vector_enabled>` property to be set to ``true``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PathFollow3D_property_cubic_interp:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cubic_interp** = ``true`` :ref:`🔗<class_PathFollow3D_property_cubic_interp>`

.. rst-class:: classref-property-setget

- |void| **set_cubic_interpolation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_cubic_interpolation**\ (\ )

Nếu ``true``, vị trí giữa hai điểm đã lưu trong bộ nhớ đệm sẽ được nội suy theo cubic, nếu không thì nội suy tuyến tính.

Các điểm dọc theo :ref:`Curve3D<class_Curve3D>` của :ref:`Path3D<class_Path3D>` được tính toán trước khi sử dụng để tăng tốc độ tính toán. Sau đó, điểm tại offset được yêu cầu sẽ được tính bằng cách nội suy giữa hai điểm liền kề trong bộ nhớ đệm. Điều này có thể gây vấn đề nếu đường cong có các đoạn rẽ gấp, vì các điểm trong bộ nhớ đệm có thể không bám đủ sát đường cong.

Có hai cách giải quyết vấn đề này: hoặc tăng số lượng điểm trong bộ nhớ đệm và mức tiêu thụ bộ nhớ, hoặc thực hiện nội suy cubic giữa hai điểm với cái giá là tốc độ tính toán chậm hơn (một chút).

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_h_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **h_offset** = ``0.0`` :ref:`🔗<class_PathFollow3D_property_h_offset>`

.. rst-class:: classref-property-setget

- |void| **set_h_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_h_offset**\ (\ )

Offset của node dọc theo đường cong.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **loop** = ``true`` :ref:`🔗<class_PathFollow3D_property_loop>`

.. rst-class:: classref-property-setget

- |void| **set_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_loop**\ (\ )

Nếu ``true``, mọi offset nằm ngoài độ dài của đường dẫn sẽ quay vòng thay vì dừng ở hai đầu. Hãy sử dụng tùy chọn này cho các đường dẫn tuần hoàn.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_progress:

.. rst-class:: classref-property

:ref:`float<class_float>` **progress** = ``0.0`` :ref:`🔗<class_PathFollow3D_property_progress>`

.. rst-class:: classref-property-setget

- |void| **set_progress**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_progress**\ (\ )

Khoảng cách tính từ đỉnh đầu tiên, được đo bằng đơn vị 3D dọc theo đường dẫn. Việc thay đổi giá trị này sẽ đặt vị trí của node này vào một điểm trên đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_progress_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **progress_ratio** = ``0.0`` :ref:`🔗<class_PathFollow3D_property_progress_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_progress_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_progress_ratio**\ (\ )

Khoảng cách tính từ đỉnh đầu tiên, trong đó 0.0 là đỉnh đầu tiên và 1.0 là đỉnh cuối cùng. Đây chỉ là một cách khác để biểu thị tiến trình trên đường dẫn, vì giá trị progress được cung cấp sẽ được nhân với độ dài của đường dẫn ở bên trong.

Chỉ có thể thiết lập hoặc lấy giá trị này nếu **PathFollow3D** là node con của một :ref:`Path3D<class_Path3D>` thuộc scene tree, đồng thời :ref:`Path3D<class_Path3D>` đó có :ref:`Curve3D<class_Curve3D>` với độ dài khác 0. Nếu không, việc cố thiết lập trường này sẽ in ra lỗi, còn việc lấy trường này sẽ trả về ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_rotation_mode:

.. rst-class:: classref-property

:ref:`RotationMode<enum_PathFollow3D_RotationMode>` **rotation_mode** = ``3`` :ref:`🔗<class_PathFollow3D_property_rotation_mode>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_mode**\ (\ value\: :ref:`RotationMode<enum_PathFollow3D_RotationMode>`\ ) - :ref:`RotationMode<enum_PathFollow3D_RotationMode>` **get_rotation_mode**\ (\ )

Cho phép hoặc ngăn xoay quanh một hay nhiều trục, tùy thuộc vào các hằng số :ref:`RotationMode<enum_PathFollow3D_RotationMode>` được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_tilt_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **tilt_enabled** = ``true`` :ref:`🔗<class_PathFollow3D_property_tilt_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_tilt_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_tilt_enabled**\ (\ )

Nếu ``true``, thuộc tính tilt của :ref:`Curve3D<class_Curve3D>` sẽ có hiệu lực.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_use_model_front:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_model_front** = ``false`` :ref:`🔗<class_PathFollow3D_property_use_model_front>`

.. rst-class:: classref-property-setget

- |void| **set_use_model_front**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_model_front**\ (\ )

Nếu ``true``, node sẽ di chuyển trên đường đi với trục +Z được định hướng làm hướng tiến. Xem thêm :ref:`Vector3.FORWARD<class_Vector3_constant_FORWARD>` và :ref:`Vector3.MODEL_FRONT<class_Vector3_constant_MODEL_FRONT>`.

.. rst-class:: classref-item-separator

----

.. _class_PathFollow3D_property_v_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **v_offset** = ``0.0`` :ref:`🔗<class_PathFollow3D_property_v_offset>`

.. rst-class:: classref-property-setget

- |void| **set_v_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_v_offset**\ (\ )

Offset của node vuông góc với đường cong.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PathFollow3D_method_correct_posture:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **correct_posture**\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, rotation_mode\: :ref:`RotationMode<enum_PathFollow3D_RotationMode>`\ ) |static| :ref:`🔗<class_PathFollow3D_method_correct_posture>`

Điều chỉnh ``transform``. ``rotation_mode`` ngầm chỉ định cách tính tư thế (hướng tiến, hướng lên và hướng ngang).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
