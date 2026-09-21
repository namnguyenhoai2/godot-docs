:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AimModifier3D.xml.

.. _class_AimModifier3D:

AimModifier3D
=============

**Kế thừa:** :ref:`BoneConstraint3D<class_BoneConstraint3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**AimModifier3D** xoay một bone để hướng về một bone tham chiếu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là phiên bản đơn giản của :ref:`LookAtModifier3D<class_LookAtModifier3D>`, chỉ cho phép bone hướng về bone tham chiếu mà không có các tùy chọn nâng cao như giới hạn góc hoặc nội suy dựa trên thời gian.

Tính năng này được đơn giản hóa, nhưng thay vào đó được triển khai bằng cơ chế theo dõi mượt mà không sử dụng euler, xem :ref:`set_use_euler()<class_AimModifier3D_method_set_use_euler>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`setting_count<class_AimModifier3D_property_setting_count>` | ``0`` |
   +-----------------------+------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>` | :ref:`get_forward_axis<class_AimModifier3D_method_get_forward_axis>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Axis<enum_Vector3_Axis>`                    | :ref:`get_primary_rotation_axis<class_AimModifier3D_method_get_primary_rotation_axis>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                 |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_relative<class_AimModifier3D_method_is_relative>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                             |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_using_euler<class_AimModifier3D_method_is_using_euler>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                       |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_using_secondary_rotation<class_AimModifier3D_method_is_using_secondary_rotation>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                             |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_forward_axis<class_AimModifier3D_method_set_forward_axis>`\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>`\ ) |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_primary_rotation_axis<class_AimModifier3D_method_set_primary_rotation_axis>`\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ )  |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_relative<class_AimModifier3D_method_set_relative>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_use_euler<class_AimModifier3D_method_set_use_euler>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                              |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_use_secondary_rotation<class_AimModifier3D_method_set_use_secondary_rotation>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )    |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AimModifier3D_property_setting_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **setting_count** = ``0`` :ref:`🔗<class_AimModifier3D_property_setting_count>`

.. rst-class:: classref-property-setget

- |void| **set_setting_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_setting_count**\ (\ )

Số lượng thiết lập trong modifier.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AimModifier3D_method_get_forward_axis:

.. rst-class:: classref-method

:ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>` **get_forward_axis**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AimModifier3D_method_get_forward_axis>`

Trả về trục hướng về phía trước của bone.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_get_primary_rotation_axis:

.. rst-class:: classref-method

:ref:`Axis<enum_Vector3_Axis>` **get_primary_rotation_axis**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AimModifier3D_method_get_primary_rotation_axis>`

Trả về trục của lần xoay đầu tiên. Trục này chỉ được bật khi :ref:`is_using_euler()<class_AimModifier3D_method_is_using_euler>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_is_relative:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_relative**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AimModifier3D_method_is_relative>`

Trả về ``true`` nếu tùy chọn tương đối được bật trong thiết lập tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_is_using_euler:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_using_euler**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AimModifier3D_method_is_using_euler>`

Trả về ``true`` nếu nó cung cấp phép xoay bằng euler.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_is_using_secondary_rotation:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_using_secondary_rotation**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AimModifier3D_method_is_using_secondary_rotation>`

Trả về ``true`` nếu nó cung cấp phép xoay bằng hai trục. Tùy chọn này chỉ được bật khi :ref:`is_using_euler()<class_AimModifier3D_method_is_using_euler>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_set_forward_axis:

.. rst-class:: classref-method

|void| **set_forward_axis**\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`BoneAxis<enum_SkeletonModifier3D_BoneAxis>`\ ) :ref:`🔗<class_AimModifier3D_method_set_forward_axis>`

Thiết lập trục hướng về phía trước của bone.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_set_primary_rotation_axis:

.. rst-class:: classref-method

|void| **set_primary_rotation_axis**\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ ) :ref:`🔗<class_AimModifier3D_method_set_primary_rotation_axis>`

Thiết lập trục của lần xoay đầu tiên. Trục này chỉ được bật khi :ref:`is_using_euler()<class_AimModifier3D_method_is_using_euler>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_set_relative:

.. rst-class:: classref-method

|void| **set_relative**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AimModifier3D_method_set_relative>`

Thiết lập tùy chọn tương đối trong thiết lập tại ``index`` thành ``enabled``.

Nếu đặt ``enabled`` thành ``true``, phép xoay được áp dụng tương đối với pose.

Nếu đặt ``enabled`` thành ``false``, phép xoay được áp dụng tương đối với trạng thái nghỉ. Điều này có nghĩa là thay thế pose hiện tại bằng kết quả của **AimModifier3D**.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_set_use_euler:

.. rst-class:: classref-method

|void| **set_use_euler**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AimModifier3D_method_set_use_euler>`

Nếu đặt ``enabled`` thành ``true``, nó cung cấp phép xoay bằng euler.

Nếu đặt ``enabled`` thành ``false``, nó cung cấp phép xoay bằng cung được tạo từ vector trục hướng về phía trước và vector hướng đến đối tượng tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_AimModifier3D_method_set_use_secondary_rotation:

.. rst-class:: classref-method

|void| **set_use_secondary_rotation**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AimModifier3D_method_set_use_secondary_rotation>`

Nếu đặt ``enabled`` thành ``true``, nó cung cấp phép xoay bằng hai trục. Tùy chọn này chỉ được bật khi :ref:`is_using_euler()<class_AimModifier3D_method_is_using_euler>` là ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
