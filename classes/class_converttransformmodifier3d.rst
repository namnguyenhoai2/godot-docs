:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ConvertTransformModifier3D.xml.

.. _class_ConvertTransformModifier3D:

ConvertTransformModifier3D
==========================

**Kế thừa:** :ref:`BoneConstraint3D<class_BoneConstraint3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` áp dụng transform cho bone được chuyển đổi từ bone tham chiếu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Áp dụng transform đã sao chép của bone do :ref:`BoneConstraint3D.set_reference_bone()<class_BoneConstraint3D_method_set_reference_bone>` thiết lập cho bone do :ref:`BoneConstraint3D.set_apply_bone()<class_BoneConstraint3D_method_set_apply_bone>` thiết lập trên trục cụ thể, đồng thời remap transform đó bằng một số tùy chọn.

Có 4 cách áp dụng transform, tùy thuộc vào sự kết hợp của :ref:`set_relative()<class_ConvertTransformModifier3D_method_set_relative>` và :ref:`set_additive()<class_ConvertTransformModifier3D_method_set_additive>`.

\ **Relative + Additive:**\

- Trích xuất pose tham chiếu tương đối với rest và cộng nó vào pose của bone áp dụng.

\ **Relative + Not Additive:**\

- Trích xuất pose tham chiếu tương đối với rest và cộng nó vào rest của bone áp dụng.

\ **Not Relative + Additive:**\

- Trích xuất pose tham chiếu một cách tuyệt đối và cộng nó vào pose của bone áp dụng.

\ **Not Relative + Not Additive:**\

- Trích xuất pose tham chiếu một cách tuyệt đối và thay thế pose của bone áp dụng bằng pose đó.

\ **Lưu ý:** Tùy chọn Relative chỉ khả dụng trong trường hợp :ref:`BoneConstraint3D.get_reference_type()<class_BoneConstraint3D_method_get_reference_type>` là :ref:`BoneConstraint3D.REFERENCE_TYPE_BONE<class_BoneConstraint3D_constant_REFERENCE_TYPE_BONE>`. Xem thêm :ref:`ReferenceType<enum_BoneConstraint3D_ReferenceType>`.

\ **Lưu ý:** Nếu có rotation lớn hơn ``180`` độ với các trục bị giới hạn, hiện tượng lật có thể xảy ra.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------+-------------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`setting_count<class_ConvertTransformModifier3D_property_setting_count>` | ``0`` |
   +-----------------------+-------------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Axis<enum_Vector3_Axis>`                                      | :ref:`get_apply_axis<class_ConvertTransformModifier3D_method_get_apply_axis>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                           |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`get_apply_range_max<class_ConvertTransformModifier3D_method_get_apply_range_max>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                 |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`get_apply_range_min<class_ConvertTransformModifier3D_method_get_apply_range_min>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                 |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` | :ref:`get_apply_transform_mode<class_ConvertTransformModifier3D_method_get_apply_transform_mode>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                       |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Axis<enum_Vector3_Axis>`                                      | :ref:`get_reference_axis<class_ConvertTransformModifier3D_method_get_reference_axis>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                   |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`get_reference_range_max<class_ConvertTransformModifier3D_method_get_reference_range_max>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                         |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`get_reference_range_min<class_ConvertTransformModifier3D_method_get_reference_range_min>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                         |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` | :ref:`get_reference_transform_mode<class_ConvertTransformModifier3D_method_get_reference_transform_mode>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                               |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`is_additive<class_ConvertTransformModifier3D_method_is_additive>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                 |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`is_relative<class_ConvertTransformModifier3D_method_is_relative>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                 |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_additive<class_ConvertTransformModifier3D_method_set_additive>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                                                    |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_apply_axis<class_ConvertTransformModifier3D_method_set_apply_axis>`\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ )                                                                            |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_apply_range_max<class_ConvertTransformModifier3D_method_set_apply_range_max>`\ (\ index\: :ref:`int<class_int>`, range_max\: :ref:`float<class_float>`\ )                                                                  |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_apply_range_min<class_ConvertTransformModifier3D_method_set_apply_range_min>`\ (\ index\: :ref:`int<class_int>`, range_min\: :ref:`float<class_float>`\ )                                                                  |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_apply_transform_mode<class_ConvertTransformModifier3D_method_set_apply_transform_mode>`\ (\ index\: :ref:`int<class_int>`, transform_mode\: :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>`\ )         |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_reference_axis<class_ConvertTransformModifier3D_method_set_reference_axis>`\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ )                                                                    |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_reference_range_max<class_ConvertTransformModifier3D_method_set_reference_range_max>`\ (\ index\: :ref:`int<class_int>`, range_max\: :ref:`float<class_float>`\ )                                                          |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_reference_range_min<class_ConvertTransformModifier3D_method_set_reference_range_min>`\ (\ index\: :ref:`int<class_int>`, range_min\: :ref:`float<class_float>`\ )                                                          |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_reference_transform_mode<class_ConvertTransformModifier3D_method_set_reference_transform_mode>`\ (\ index\: :ref:`int<class_int>`, transform_mode\: :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>`\ ) |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                              | :ref:`set_relative<class_ConvertTransformModifier3D_method_set_relative>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                                                    |
   +---------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_ConvertTransformModifier3D_TransformMode:

.. rst-class:: classref-enumeration

enum **TransformMode**: :ref:`🔗<enum_ConvertTransformModifier3D_TransformMode>`

.. _class_ConvertTransformModifier3D_constant_TRANSFORM_MODE_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` **TRANSFORM_MODE_POSITION** = ``0``

Chuyển đổi với position. Truyền phần chênh lệch.

.. _class_ConvertTransformModifier3D_constant_TRANSFORM_MODE_ROTATION:

.. rst-class:: classref-enumeration-constant

:ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` **TRANSFORM_MODE_ROTATION** = ``1``

Chuyển đổi với rotation. Góc là roll của trục được chỉ định.

.. _class_ConvertTransformModifier3D_constant_TRANSFORM_MODE_SCALE:

.. rst-class:: classref-enumeration-constant

:ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` **TRANSFORM_MODE_SCALE** = ``2``

Chuyển đổi với scale. Truyền tỷ lệ, không phải phần chênh lệch.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConvertTransformModifier3D_property_setting_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **setting_count** = ``0`` :ref:`🔗<class_ConvertTransformModifier3D_property_setting_count>`

.. rst-class:: classref-property-setget

- |void| **set_setting_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_setting_count**\ (\ )

Số lượng setting trong modifier.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConvertTransformModifier3D_method_get_apply_axis:

.. rst-class:: classref-method

:ref:`Axis<enum_Vector3_Axis>` **get_apply_axis**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_apply_axis>`

Trả về trục của transform đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_apply_range_max:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_apply_range_max**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_apply_range_max>`

Trả về giá trị tối đa của range đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_apply_range_min:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_apply_range_min**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_apply_range_min>`

Trả về giá trị tối thiểu của range đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_apply_transform_mode:

.. rst-class:: classref-method

:ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` **get_apply_transform_mode**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_apply_transform_mode>`

Trả về phép toán của transform đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_reference_axis:

.. rst-class:: classref-method

:ref:`Axis<enum_Vector3_Axis>` **get_reference_axis**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_reference_axis>`

Trả về trục của transform nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_reference_range_max:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_reference_range_max**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_reference_range_max>`

Trả về giá trị tối đa của range nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_reference_range_min:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_reference_range_min**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_reference_range_min>`

Trả về giá trị tối thiểu của range nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_get_reference_transform_mode:

.. rst-class:: classref-method

:ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>` **get_reference_transform_mode**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_get_reference_transform_mode>`

Trả về phép toán của transform nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_is_additive:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_additive**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_is_additive>`

Trả về ``true`` nếu tùy chọn additive được bật trong setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_is_relative:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_relative**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ConvertTransformModifier3D_method_is_relative>`

Trả về ``true`` nếu tùy chọn relative được bật trong setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_additive:

.. rst-class:: classref-method

|void| **set_additive**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_additive>`

Thiết lập tùy chọn additive trong setting tại ``index`` thành ``enabled``. Tùy chọn này chủ yếu ảnh hưởng đến quá trình áp dụng transform cho :ref:`BoneConstraint3D.set_apply_bone()<class_BoneConstraint3D_method_set_apply_bone>`.

Nếu đặt ``enabled`` thành ``true``, transform đã xử lý sẽ được cộng vào pose của bone áp dụng hiện tại.

Nếu đặt ``enabled`` thành ``false``, pose của bone áp dụng hiện tại sẽ được thay thế bằng transform đã xử lý. Tuy nhiên, nếu đặt :ref:`set_relative()<class_ConvertTransformModifier3D_method_set_relative>` thành ``true``, transform sẽ tương đối so với rest.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_apply_axis:

.. rst-class:: classref-method

|void| **set_apply_axis**\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_apply_axis>`

Thiết lập trục của transform đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_apply_range_max:

.. rst-class:: classref-method

|void| **set_apply_range_max**\ (\ index\: :ref:`int<class_int>`, range_max\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_apply_range_max>`

Thiết lập giá trị tối đa của range đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_apply_range_min:

.. rst-class:: classref-method

|void| **set_apply_range_min**\ (\ index\: :ref:`int<class_int>`, range_min\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_apply_range_min>`

Thiết lập giá trị tối thiểu của range đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_apply_transform_mode:

.. rst-class:: classref-method

|void| **set_apply_transform_mode**\ (\ index\: :ref:`int<class_int>`, transform_mode\: :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_apply_transform_mode>`

Thiết lập phép toán của transform đích remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_reference_axis:

.. rst-class:: classref-method

|void| **set_reference_axis**\ (\ index\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_reference_axis>`

Thiết lập trục của transform nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_reference_range_max:

.. rst-class:: classref-method

|void| **set_reference_range_max**\ (\ index\: :ref:`int<class_int>`, range_max\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_reference_range_max>`

Thiết lập giá trị tối đa của range nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_reference_range_min:

.. rst-class:: classref-method

|void| **set_reference_range_min**\ (\ index\: :ref:`int<class_int>`, range_min\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_reference_range_min>`

Thiết lập giá trị tối thiểu của range nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_reference_transform_mode:

.. rst-class:: classref-method

|void| **set_reference_transform_mode**\ (\ index\: :ref:`int<class_int>`, transform_mode\: :ref:`TransformMode<enum_ConvertTransformModifier3D_TransformMode>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_reference_transform_mode>`

Thiết lập phép toán của transform nguồn remapping.

.. rst-class:: classref-item-separator

----

.. _class_ConvertTransformModifier3D_method_set_relative:

.. rst-class:: classref-method

|void| **set_relative**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_ConvertTransformModifier3D_method_set_relative>`

Thiết lập tùy chọn relative trong setting tại ``index`` thành ``enabled``.

Nếu đặt ``enabled`` thành ``true``, transform được trích xuất và áp dụng sẽ tương đối so với rest.

Nếu đặt ``enabled`` thành ``false``, transform được trích xuất sẽ là tuyệt đối.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
