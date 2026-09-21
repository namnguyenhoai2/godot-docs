:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CopyTransformModifier3D.xml.

.. _class_CopyTransformModifier3D:

CopyTransformModifier3D
=======================

**Kế thừa:** :ref:`BoneConstraint3D<class_BoneConstraint3D>` **<** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` áp dụng transform cho bone được sao chép từ bone tham chiếu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Áp dụng transform đã sao chép của bone được thiết lập bởi :ref:`BoneConstraint3D.set_reference_bone()<class_BoneConstraint3D_method_set_reference_bone>` cho bone được thiết lập bởi :ref:`BoneConstraint3D.set_apply_bone()<class_BoneConstraint3D_method_set_apply_bone>`, đồng thời xử lý transform bằng một số mask và tùy chọn.

Có 4 cách áp dụng transform, tùy thuộc vào tổ hợp của :ref:`set_relative()<class_CopyTransformModifier3D_method_set_relative>` và :ref:`set_additive()<class_CopyTransformModifier3D_method_set_additive>`.

\ **Relative + Additive:**\

- Trích xuất pose tham chiếu tương đối so với rest và cộng nó vào pose của bone áp dụng.

\ **Relative + Not Additive:**\

- Trích xuất pose tham chiếu tương đối so với rest và cộng nó vào rest của bone áp dụng.

\ **Not Relative + Additive:**\

- Trích xuất pose tham chiếu tuyệt đối và cộng nó vào pose của bone áp dụng.

\ **Not Relative + Not Additive:**\

- Trích xuất pose tham chiếu tuyệt đối và thay thế pose của bone áp dụng bằng pose đó.

\ **Lưu ý:** Tùy chọn Relative chỉ khả dụng khi :ref:`BoneConstraint3D.get_reference_type()<class_BoneConstraint3D_method_get_reference_type>` là :ref:`BoneConstraint3D.REFERENCE_TYPE_BONE<class_BoneConstraint3D_constant_REFERENCE_TYPE_BONE>`. Xem thêm :ref:`ReferenceType<enum_BoneConstraint3D_ReferenceType>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+----------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`setting_count<class_CopyTransformModifier3D_property_setting_count>` | ``0`` |
   +-----------------------+----------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]           | :ref:`get_axis_flags<class_CopyTransformModifier3D_method_get_axis_flags>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                      |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>`\] | :ref:`get_copy_flags<class_CopyTransformModifier3D_method_get_copy_flags>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                      |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]           | :ref:`get_invert_flags<class_CopyTransformModifier3D_method_get_invert_flags>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                  |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_additive<class_CopyTransformModifier3D_method_is_additive>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                            |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_x_enabled<class_CopyTransformModifier3D_method_is_axis_x_enabled>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_x_inverted<class_CopyTransformModifier3D_method_is_axis_x_inverted>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                              |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_y_enabled<class_CopyTransformModifier3D_method_is_axis_y_enabled>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_y_inverted<class_CopyTransformModifier3D_method_is_axis_y_inverted>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                              |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_z_enabled<class_CopyTransformModifier3D_method_is_axis_z_enabled>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_axis_z_inverted<class_CopyTransformModifier3D_method_is_axis_z_inverted>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                              |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_position_copying<class_CopyTransformModifier3D_method_is_position_copying>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                            |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_relative<class_CopyTransformModifier3D_method_is_relative>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                            |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_rotation_copying<class_CopyTransformModifier3D_method_is_rotation_copying>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                            |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`is_scale_copying<class_CopyTransformModifier3D_method_is_scale_copying>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                  |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_additive<class_CopyTransformModifier3D_method_set_additive>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                               |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_flags<class_CopyTransformModifier3D_method_set_axis_flags>`\ (\ index\: :ref:`int<class_int>`, axis_flags\: |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]\ )           |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_x_enabled<class_CopyTransformModifier3D_method_set_axis_x_enabled>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                   |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_x_inverted<class_CopyTransformModifier3D_method_set_axis_x_inverted>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                 |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_y_enabled<class_CopyTransformModifier3D_method_set_axis_y_enabled>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                   |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_y_inverted<class_CopyTransformModifier3D_method_set_axis_y_inverted>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                 |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_z_enabled<class_CopyTransformModifier3D_method_set_axis_z_enabled>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                   |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_axis_z_inverted<class_CopyTransformModifier3D_method_set_axis_z_inverted>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                 |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_copy_flags<class_CopyTransformModifier3D_method_set_copy_flags>`\ (\ index\: :ref:`int<class_int>`, copy_flags\: |bitfield|\[:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>`\]\ ) |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_copy_position<class_CopyTransformModifier3D_method_set_copy_position>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                     |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_copy_rotation<class_CopyTransformModifier3D_method_set_copy_rotation>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                     |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_copy_scale<class_CopyTransformModifier3D_method_set_copy_scale>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                           |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_invert_flags<class_CopyTransformModifier3D_method_set_invert_flags>`\ (\ index\: :ref:`int<class_int>`, axis_flags\: |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]\ )       |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                         | :ref:`set_relative<class_CopyTransformModifier3D_method_set_relative>`\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )                                                               |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CopyTransformModifier3D_TransformFlag:

.. rst-class:: classref-enumeration

flags **TransformFlag**: :ref:`🔗<enum_CopyTransformModifier3D_TransformFlag>`

.. _class_CopyTransformModifier3D_constant_TRANSFORM_FLAG_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>` **TRANSFORM_FLAG_POSITION** = ``1``

Nếu được thiết lập, cho phép sao chép vị trí.

.. _class_CopyTransformModifier3D_constant_TRANSFORM_FLAG_ROTATION:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>` **TRANSFORM_FLAG_ROTATION** = ``2``

Nếu được thiết lập, cho phép sao chép rotation.

.. _class_CopyTransformModifier3D_constant_TRANSFORM_FLAG_SCALE:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>` **TRANSFORM_FLAG_SCALE** = ``4``

Nếu được thiết lập, cho phép sao chép scale.

.. _class_CopyTransformModifier3D_constant_TRANSFORM_FLAG_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>` **TRANSFORM_FLAG_ALL** = ``7``

Nếu được thiết lập, cho phép sao chép vị trí/rotation/scale.

.. rst-class:: classref-item-separator

----

.. _enum_CopyTransformModifier3D_AxisFlag:

.. rst-class:: classref-enumeration

flags **AxisFlag**: :ref:`🔗<enum_CopyTransformModifier3D_AxisFlag>`

.. _class_CopyTransformModifier3D_constant_AXIS_FLAG_X:

.. rst-class:: classref-enumeration-constant

:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>` **AXIS_FLAG_X** = ``1``

Nếu được thiết lập, cho phép xử lý trục X.

.. _class_CopyTransformModifier3D_constant_AXIS_FLAG_Y:

.. rst-class:: classref-enumeration-constant

:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>` **AXIS_FLAG_Y** = ``2``

Nếu được thiết lập, cho phép xử lý trục Y.

.. _class_CopyTransformModifier3D_constant_AXIS_FLAG_Z:

.. rst-class:: classref-enumeration-constant

:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>` **AXIS_FLAG_Z** = ``4``

Nếu được thiết lập, cho phép xử lý trục Z.

.. _class_CopyTransformModifier3D_constant_AXIS_FLAG_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>` **AXIS_FLAG_ALL** = ``7``

Nếu được thiết lập, cho phép xử lý tất cả các trục.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CopyTransformModifier3D_property_setting_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **setting_count** = ``0`` :ref:`🔗<class_CopyTransformModifier3D_property_setting_count>`

.. rst-class:: classref-property-setget

- |void| **set_setting_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_setting_count**\ (\ )

Số lượng setting trong modifier.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CopyTransformModifier3D_method_get_axis_flags:

.. rst-class:: classref-method

|bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\] **get_axis_flags**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_get_axis_flags>`

Trả về các axis flags của setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_get_copy_flags:

.. rst-class:: classref-method

|bitfield|\[:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>`\] **get_copy_flags**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_get_copy_flags>`

Trả về các copy flags của setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_get_invert_flags:

.. rst-class:: classref-method

|bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\] **get_invert_flags**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_get_invert_flags>`

Trả về các invert flags của setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_additive:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_additive**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_additive>`

Trả về ``true`` nếu tùy chọn additive được bật trong setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_x_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_x_enabled**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_x_enabled>`

Trả về ``true`` nếu enable flags có flag dành cho trục X trong setting tại ``index``. Xem thêm :ref:`set_axis_flags()<class_CopyTransformModifier3D_method_set_axis_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_x_inverted:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_x_inverted**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_x_inverted>`

Trả về ``true`` nếu invert flags có flag dành cho trục X trong setting tại ``index``. Xem thêm :ref:`set_invert_flags()<class_CopyTransformModifier3D_method_set_invert_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_y_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_y_enabled**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_y_enabled>`

Trả về ``true`` nếu enable flags có flag dành cho trục Y trong setting tại ``index``. Xem thêm :ref:`set_axis_flags()<class_CopyTransformModifier3D_method_set_axis_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_y_inverted:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_y_inverted**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_y_inverted>`

Trả về ``true`` nếu invert flags có flag dành cho trục Y trong setting tại ``index``. Xem thêm :ref:`set_invert_flags()<class_CopyTransformModifier3D_method_set_invert_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_z_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_z_enabled**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_z_enabled>`

Trả về ``true`` nếu enable flags có flag dành cho trục Z trong setting tại ``index``. Xem thêm :ref:`set_axis_flags()<class_CopyTransformModifier3D_method_set_axis_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_axis_z_inverted:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_axis_z_inverted**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_axis_z_inverted>`

Trả về ``true`` nếu invert flags có flag dành cho trục Z trong setting tại ``index``. Xem thêm :ref:`set_invert_flags()<class_CopyTransformModifier3D_method_set_invert_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_position_copying:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_position_copying**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_position_copying>`

Trả về ``true`` nếu copy flags có flag dành cho vị trí trong setting tại ``index``. Xem thêm :ref:`set_copy_flags()<class_CopyTransformModifier3D_method_set_copy_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_relative:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_relative**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_relative>`

Trả về ``true`` nếu tùy chọn relative được bật trong setting tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_rotation_copying:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_rotation_copying**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_rotation_copying>`

Trả về ``true`` nếu copy flags có flag dành cho rotation trong setting tại ``index``. Xem thêm :ref:`set_copy_flags()<class_CopyTransformModifier3D_method_set_copy_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_is_scale_copying:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_scale_copying**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CopyTransformModifier3D_method_is_scale_copying>`

Trả về ``true`` nếu copy flags có flag dành cho scale trong setting tại ``index``. Xem thêm :ref:`set_copy_flags()<class_CopyTransformModifier3D_method_set_copy_flags>`.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_additive:

.. rst-class:: classref-method

|void| **set_additive**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_additive>`

Thiết lập tùy chọn additive trong setting tại ``index`` thành ``enabled``. Điều này chủ yếu ảnh hưởng đến quá trình áp dụng transform cho :ref:`BoneConstraint3D.set_apply_bone()<class_BoneConstraint3D_method_set_apply_bone>`.

Nếu đặt ``enabled`` thành ``true``, transform đã xử lý sẽ được cộng vào pose của bone áp dụng hiện tại.

Nếu đặt ``enabled`` thành ``false``, pose của bone áp dụng hiện tại sẽ được thay thế bằng transform đã xử lý. Tuy nhiên, nếu đặt :ref:`set_relative()<class_CopyTransformModifier3D_method_set_relative>` thành ``true``, transform sẽ tương đối so với rest.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_flags:

.. rst-class:: classref-method

|void| **set_axis_flags**\ (\ index\: :ref:`int<class_int>`, axis_flags\: |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_flags>`

Thiết lập các flag để sao chép các trục. Nếu flag hợp lệ, trục đó sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_x_enabled:

.. rst-class:: classref-method

|void| **set_axis_x_enabled**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_x_enabled>`

Nếu đặt ``enabled`` thành ``true``, trục X sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_x_inverted:

.. rst-class:: classref-method

|void| **set_axis_x_inverted**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_x_inverted>`

Nếu đặt ``enabled`` thành ``true``, trục X sẽ bị đảo ngược.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_y_enabled:

.. rst-class:: classref-method

|void| **set_axis_y_enabled**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_y_enabled>`

Nếu đặt ``enabled`` thành ``true``, trục Y sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_y_inverted:

.. rst-class:: classref-method

|void| **set_axis_y_inverted**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_y_inverted>`

Nếu đặt ``enabled`` thành ``true``, trục Y sẽ bị đảo ngược.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_z_enabled:

.. rst-class:: classref-method

|void| **set_axis_z_enabled**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_z_enabled>`

Nếu đặt ``enabled`` thành ``true``, trục Z sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_axis_z_inverted:

.. rst-class:: classref-method

|void| **set_axis_z_inverted**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_axis_z_inverted>`

Nếu đặt ``enabled`` thành ``true``, trục Z sẽ bị đảo ngược.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_copy_flags:

.. rst-class:: classref-method

|void| **set_copy_flags**\ (\ index\: :ref:`int<class_int>`, copy_flags\: |bitfield|\[:ref:`TransformFlag<enum_CopyTransformModifier3D_TransformFlag>`\]\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_copy_flags>`

Thiết lập các flag để xử lý các thao tác transform. Nếu flag hợp lệ, thao tác transform sẽ được xử lý.

\ **Lưu ý:** Nếu rotation chỉ hợp lệ cho một trục, nó sẽ giữ roll của trục hợp lệ. Nếu rotation hợp lệ cho hai trục, nó sẽ loại bỏ roll của trục không hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_copy_position:

.. rst-class:: classref-method

|void| **set_copy_position**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_copy_position>`

Nếu đặt ``enabled`` thành ``true``, vị trí sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_copy_rotation:

.. rst-class:: classref-method

|void| **set_copy_rotation**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_copy_rotation>`

Nếu đặt ``enabled`` thành ``true``, rotation sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_copy_scale:

.. rst-class:: classref-method

|void| **set_copy_scale**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_copy_scale>`

Nếu đặt ``enabled`` thành ``true``, scale sẽ được sao chép.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_invert_flags:

.. rst-class:: classref-method

|void| **set_invert_flags**\ (\ index\: :ref:`int<class_int>`, axis_flags\: |bitfield|\[:ref:`AxisFlag<enum_CopyTransformModifier3D_AxisFlag>`\]\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_invert_flags>`

Thiết lập các flag để đảo ngược các trục. Nếu flag hợp lệ, trục đó sẽ được sao chép.

\ **Lưu ý:** Scale bị đảo ngược nghĩa là một số nghịch đảo, không phải scale âm. Ví dụ, đảo ngược ``2.0`` có nghĩa là ``0.5``.

\ **Lưu ý:** Rotation bị đảo ngược sẽ lật các phần tử của quaternion. Ví dụ, đảo ngược hai trục sẽ lật roll của từng trục, còn đảo ngược ba trục sẽ lật hướng cuối cùng. Tuy nhiên, hãy lưu ý rằng chỉ lật một trục có thể gây ra rotation ngoài ý muốn ở các trục không bị lật, do đặc tính của quaternion.

.. rst-class:: classref-item-separator

----

.. _class_CopyTransformModifier3D_method_set_relative:

.. rst-class:: classref-method

|void| **set_relative**\ (\ index\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CopyTransformModifier3D_method_set_relative>`

Thiết lập tùy chọn relative trong setting tại ``index`` thành ``enabled``.

Nếu đặt ``enabled`` thành ``true``, phép biến đổi được trích xuất và áp dụng là tương đối so với phần còn lại.

Nếu đặt ``enabled`` thành ``false``, phép biến đổi được trích xuất là tuyệt đối.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
