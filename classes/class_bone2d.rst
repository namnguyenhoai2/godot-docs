:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Bone2D.xml.

.. _class_Bone2D:

Bone2D
======

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một joint được sử dụng cùng với :ref:`Skeleton2D<class_Skeleton2D>` để điều khiển và animate các node khác.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hệ phân cấp các **Bone2D**\ s có thể được liên kết với một :ref:`Skeleton2D<class_Skeleton2D>` để điều khiển và animate các node :ref:`Node2D<class_Node2D>` khác.

Bạn có thể sử dụng các node **Bone2D** và :ref:`Skeleton2D<class_Skeleton2D>` để animate các mesh 2D được tạo bằng trình chỉnh sửa UV :ref:`Polygon2D<class_Polygon2D>`.

Mỗi bone có một transform :ref:`rest<class_Bone2D_property_rest>` mà bạn có thể đặt lại bằng :ref:`apply_rest()<class_Bone2D_method_apply_rest>`. Các rest pose này là tương đối so với bone cha.

Trong editor, bạn có thể đặt rest pose của toàn bộ skeleton bằng một tùy chọn trong menu; còn từ code, bạn cần lặp qua các bone để đặt rest pose riêng cho từng bone.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------+-----------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`rest<class_Bone2D_property_rest>` | ``Transform2D(0, 0, 0, 0, 0, 0)`` |
   +---------------------------------------+-----------------------------------------+-----------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`apply_rest<class_Bone2D_method_apply_rest>`\ (\ )                                                                                           |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`get_autocalculate_length_and_angle<class_Bone2D_method_get_autocalculate_length_and_angle>`\ (\ ) |const|                                   |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_bone_angle<class_Bone2D_method_get_bone_angle>`\ (\ ) |const|                                                                           |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_index_in_skeleton<class_Bone2D_method_get_index_in_skeleton>`\ (\ ) |const|                                                             |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_length<class_Bone2D_method_get_length>`\ (\ ) |const|                                                                                   |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`get_skeleton_rest<class_Bone2D_method_get_skeleton_rest>`\ (\ ) |const|                                                                     |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_autocalculate_length_and_angle<class_Bone2D_method_set_autocalculate_length_and_angle>`\ (\ auto_calculate\: :ref:`bool<class_bool>`\ ) |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_bone_angle<class_Bone2D_method_set_bone_angle>`\ (\ angle\: :ref:`float<class_float>`\ )                                                |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_length<class_Bone2D_method_set_length>`\ (\ length\: :ref:`float<class_float>`\ )                                                       |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Bone2D_property_rest:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **rest** = ``Transform2D(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_Bone2D_property_rest>`

.. rst-class:: classref-property-setget

- |void| **set_rest**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_rest**\ (\ )

Transform rest của bone. Bạn có thể đặt lại các transform của node về giá trị này bằng :ref:`apply_rest()<class_Bone2D_method_apply_rest>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Bone2D_method_apply_rest:

.. rst-class:: classref-method

|void| **apply_rest**\ (\ ) :ref:`🔗<class_Bone2D_method_apply_rest>`

Đặt lại bone về rest pose. Tương đương với việc đặt :ref:`Node2D.transform<class_Node2D_property_transform>` thành :ref:`rest<class_Bone2D_property_rest>`.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_get_autocalculate_length_and_angle:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_autocalculate_length_and_angle**\ (\ ) |const| :ref:`🔗<class_Bone2D_method_get_autocalculate_length_and_angle>`

Trả về liệu **Bone2D** này có tự động tính độ dài và góc của bone bằng node con **Bone2D** đầu tiên hay không, nếu có. Nếu không có node con **Bone2D** nào, nó không thể tự động tính các giá trị này và sẽ in ra cảnh báo.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_get_bone_angle:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bone_angle**\ (\ ) |const| :ref:`🔗<class_Bone2D_method_get_bone_angle>`

Trả về góc của bone trong **Bone2D**.

\ **Lưu ý:** Góc này khác với rotation của **Bone2D**. Góc của bone là rotation của bone được hiển thị bằng gizmo, không bị ảnh hưởng bởi :ref:`Node2D.transform<class_Node2D_property_transform>` của **Bone2D**.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_get_index_in_skeleton:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_index_in_skeleton**\ (\ ) |const| :ref:`🔗<class_Bone2D_method_get_index_in_skeleton>`

Trả về chỉ mục của node trong toàn bộ skeleton. Xem :ref:`Skeleton2D<class_Skeleton2D>`.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_get_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_length**\ (\ ) |const| :ref:`🔗<class_Bone2D_method_get_length>`

Trả về độ dài của bone trong node **Bone2D**.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_get_skeleton_rest:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **get_skeleton_rest**\ (\ ) |const| :ref:`🔗<class_Bone2D_method_get_skeleton_rest>`

Trả về :ref:`rest<class_Bone2D_property_rest>` :ref:`Transform2D<class_Transform2D>` của node nếu node không có node cha, hoặc rest pose của node tương đối so với node cha.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_set_autocalculate_length_and_angle:

.. rst-class:: classref-method

|void| **set_autocalculate_length_and_angle**\ (\ auto_calculate\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Bone2D_method_set_autocalculate_length_and_angle>`

Khi được đặt thành ``true``, node **Bone2D** sẽ cố gắng tự động tính góc và độ dài của bone bằng node con **Bone2D** đầu tiên, nếu có. Nếu không có node con nào, **Bone2D** không thể tự động tính các giá trị này và sẽ in ra cảnh báo.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_set_bone_angle:

.. rst-class:: classref-method

|void| **set_bone_angle**\ (\ angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Bone2D_method_set_bone_angle>`

Đặt góc của bone cho **Bone2D**. Thông thường, giá trị này được đặt thành rotation từ **Bone2D** đến một node con **Bone2D**.

\ **Lưu ý:** Góc này khác với rotation của **Bone2D**. Góc của bone là rotation của bone được hiển thị bằng gizmo, không bị ảnh hưởng bởi :ref:`Node2D.transform<class_Node2D_property_transform>` của **Bone2D**.

.. rst-class:: classref-item-separator

----

.. _class_Bone2D_method_set_length:

.. rst-class:: classref-method

|void| **set_length**\ (\ length\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Bone2D_method_set_length>`

Đặt độ dài của bone trong **Bone2D**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
