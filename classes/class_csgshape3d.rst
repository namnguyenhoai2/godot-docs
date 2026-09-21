:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGShape3D.xml.

.. _class_CSGShape3D:

CSGShape3D
==========

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CSGCombiner3D<class_CSGCombiner3D>`, :ref:`CSGPrimitive3D<class_CSGPrimitive3D>`

Lớp cơ sở CSG.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là lớp cơ sở CSG, cung cấp khả năng hỗ trợ các phép toán CSG cho nhiều node CSG trong Godot.

\ **Hiệu năng:** Các node CSG chỉ được dùng để prototype vì chúng có chi phí hiệu năng CPU đáng kể. Hãy cân nhắc baking kết quả phép toán CSG cuối cùng thành geometry tĩnh để thay thế các node CSG.

Có thể bake kết quả của từng node gốc CSG thành các node có tài nguyên tĩnh bằng menu editor xuất hiện khi chọn một node gốc CSG.

Các node gốc CSG riêng lẻ cũng có thể được bake thành tài nguyên tĩnh bằng script, thông qua việc gọi :ref:`bake_static_mesh()<class_CSGShape3D_method_bake_static_mesh>` cho visual mesh hoặc :ref:`bake_collision_shape()<class_CSGShape3D_method_bake_collision_shape>` cho physics collision.

Toàn bộ scene gồm các node CSG có thể được bake thành geometry tĩnh và export bằng trình xuất scene glTF của editor: **Scene > Export As... > glTF 2.0 Scene...**

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Prototyping levels with CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                     | :ref:`autosmooth<class_CSGShape3D_property_autosmooth>`                 | ``false`` |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                     | :ref:`calculate_tangents<class_CSGShape3D_property_calculate_tangents>` | ``true``  |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                       | :ref:`collision_layer<class_CSGShape3D_property_collision_layer>`       | ``1``     |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                       | :ref:`collision_mask<class_CSGShape3D_property_collision_mask>`         | ``1``     |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                   | :ref:`collision_priority<class_CSGShape3D_property_collision_priority>` | ``1.0``   |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`Operation<enum_CSGShape3D_Operation>` | :ref:`operation<class_CSGShape3D_property_operation>`                   | ``0``     |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                   | :ref:`smoothing_angle<class_CSGShape3D_property_smoothing_angle>`       | ``50.0``  |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                   | :ref:`snap<class_CSGShape3D_property_snap>`                             |           |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                     | :ref:`use_collision<class_CSGShape3D_property_use_collision>`           | ``false`` |
   +---------------------------------------------+-------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` | :ref:`bake_collision_shape<class_CSGShape3D_method_bake_collision_shape>`\ (\ )                                                                                  |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ArrayMesh<class_ArrayMesh>`                         | :ref:`bake_static_mesh<class_CSGShape3D_method_bake_static_mesh>`\ (\ )                                                                                          |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`get_collision_layer_value<class_CSGShape3D_method_get_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`get_collision_mask_value<class_CSGShape3D_method_get_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                            |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                 | :ref:`get_meshes<class_CSGShape3D_method_get_meshes>`\ (\ ) |const|                                                                                              |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`is_root_shape<class_CSGShape3D_method_is_root_shape>`\ (\ ) |const|                                                                                        |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`set_collision_layer_value<class_CSGShape3D_method_set_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`set_collision_mask_value<class_CSGShape3D_method_set_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )   |
   +-----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumeration
-----------

.. _enum_CSGShape3D_Operation:

.. rst-class:: classref-enumeration

enum **Operation**: :ref:`🔗<enum_CSGShape3D_Operation>`

.. _class_CSGShape3D_constant_OPERATION_UNION:

.. rst-class:: classref-enumeration-constant

:ref:`Operation<enum_CSGShape3D_Operation>` **OPERATION_UNION** = ``0``

Geometry của cả hai primitive được hợp nhất, geometry giao nhau bị loại bỏ.

.. _class_CSGShape3D_constant_OPERATION_INTERSECTION:

.. rst-class:: classref-enumeration-constant

:ref:`Operation<enum_CSGShape3D_Operation>` **OPERATION_INTERSECTION** = ``1``

Chỉ giữ lại geometry giao nhau, phần còn lại bị loại bỏ.

.. _class_CSGShape3D_constant_OPERATION_SUBTRACTION:

.. rst-class:: classref-enumeration-constant

:ref:`Operation<enum_CSGShape3D_Operation>` **OPERATION_SUBTRACTION** = ``2``

Shape thứ hai bị trừ khỏi shape thứ nhất, để lại một chỗ lõm có hình dạng của nó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGShape3D_property_autosmooth:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autosmooth** = ``false`` :ref:`🔗<class_CSGShape3D_property_autosmooth>`

.. rst-class:: classref-property-setget

- |void| **set_autosmooth**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_autosmooth**\ (\ )

Bật làm mượt tự động. Tùy chọn này ghi đè mọi thiết lập làm mượt trên node CSG và thay vào đó sử dụng :ref:`smoothing_angle<class_CSGShape3D_property_smoothing_angle>` để tính normal dựa trên góc giữa các mặt.

Các node con của node :ref:`CSGCombiner3D<class_CSGCombiner3D>` sẽ được xử lý như một mesh duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_calculate_tangents:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **calculate_tangents** = ``true`` :ref:`🔗<class_CSGShape3D_property_calculate_tangents>`

.. rst-class:: classref-property-setget

- |void| **set_calculate_tangents**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_calculating_tangents**\ (\ )

Tính tangent cho shape CSG, cho phép sử dụng normal map và height map. Tùy chọn này chỉ được áp dụng cho shape gốc, mọi node con sẽ bỏ qua thiết lập này. Đặt thành ``false`` có thể tăng nhẹ tốc độ tạo shape.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_collision_layer:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_layer** = ``1`` :ref:`🔗<class_CSGShape3D_property_collision_layer>`

.. rst-class:: classref-property-setget

- |void| **set_collision_layer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_layer**\ (\ )

Các physics layer mà area này thuộc về.

Các object có thể va chạm có thể tồn tại trong bất kỳ lớp nào trong số 32 layer khác nhau. Các layer này hoạt động như một hệ thống tagging và không mang tính trực quan. Một object có thể va chạm có thể sử dụng các layer này để chọn những object mà nó có thể va chạm, thông qua thuộc tính collision_mask.

Một contact được phát hiện nếu object A nằm trong bất kỳ layer nào mà object B quét, hoặc object B nằm trong bất kỳ layer nào mà object A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``1`` :ref:`🔗<class_CSGShape3D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà shape CSG này quét để phát hiện va chạm. Chỉ có hiệu lực khi :ref:`use_collision<class_CSGShape3D_property_use_collision>` là ``true``. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_collision_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_priority** = ``1.0`` :ref:`🔗<class_CSGShape3D_property_collision_priority>`

.. rst-class:: classref-property-setget

- |void| **set_collision_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_priority**\ (\ )

Độ ưu tiên được sử dụng để giải quyết va chạm khi xảy ra xuyên lấn. Chỉ có hiệu lực khi :ref:`use_collision<class_CSGShape3D_property_use_collision>` là ``true``. Độ ưu tiên càng cao thì mức độ xuyên vào object càng thấp. Ví dụ, tùy chọn này có thể được dùng để ngăn người chơi xuyên qua ranh giới của một level.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_operation:

.. rst-class:: classref-property

:ref:`Operation<enum_CSGShape3D_Operation>` **operation** = ``0`` :ref:`🔗<class_CSGShape3D_property_operation>`

.. rst-class:: classref-property-setget

- |void| **set_operation**\ (\ value\: :ref:`Operation<enum_CSGShape3D_Operation>`\ ) - :ref:`Operation<enum_CSGShape3D_Operation>` **get_operation**\ (\ )

Phép toán được thực hiện trên shape này. Tùy chọn này bị bỏ qua đối với node con CSG đầu tiên, vì phép toán được thực hiện giữa node này và node con trước đó của parent của node này.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_smoothing_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **smoothing_angle** = ``50.0`` :ref:`🔗<class_CSGShape3D_property_smoothing_angle>`

.. rst-class:: classref-property-setget

- |void| **set_smoothing_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_smoothing_angle**\ (\ )

Khi autosmooth được bật, các mặt có góc giữa chúng lớn hơn giá trị này sẽ được làm mượt, còn các mặt có góc nhỏ hơn sẽ vẫn sắc.

Lưu ý: Góc nhỏ hơn 0.1 sẽ khiến toàn bộ quá trình làm mượt bị vô hiệu hóa; có thể dùng tùy chọn này để tăng hiệu năng.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_snap:

.. rst-class:: classref-property

:ref:`float<class_float>` **snap** :ref:`🔗<class_CSGShape3D_property_snap>`

.. rst-class:: classref-property-setget

- |void| **set_snap**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_snap**\ (\ )

**Đã lỗi thời:** Thư viện CSG không còn sử dụng snapping.

Thuộc tính này không có tác dụng.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_property_use_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_collision** = ``false`` :ref:`🔗<class_CSGShape3D_property_use_collision>`

.. rst-class:: classref-property-setget

- |void| **set_use_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_collision**\ (\ )

Thêm một collision shape vào physics engine cho shape CSG của chúng ta. Shape này luôn hoạt động như một static body. Lưu ý rằng collision shape vẫn hoạt động ngay cả khi bản thân shape CSG bị ẩn. Xem thêm :ref:`collision_mask<class_CSGShape3D_property_collision_mask>` và :ref:`collision_priority<class_CSGShape3D_property_collision_priority>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CSGShape3D_method_bake_collision_shape:

.. rst-class:: classref-method

:ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` **bake_collision_shape**\ (\ ) :ref:`🔗<class_CSGShape3D_method_bake_collision_shape>`

Trả về một :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` đã bake từ kết quả phép toán CSG của node này. Trả về một shape rỗng nếu node không phải là node gốc CSG hoặc không có geometry hợp lệ.

\ **Hiệu năng:** Nếu phép toán CSG tạo ra geometry rất chi tiết với nhiều mặt, hiệu năng physics sẽ rất chậm. Nhìn chung, chỉ nên sử dụng các shape lõm cho geometry tĩnh của level, không nên dùng với các object động đang di chuyển.

\ **Lưu ý:** Dữ liệu mesh CSG được cập nhật trì hoãn, nghĩa là chúng được cập nhật sau một frame đã render. Để tránh nhận được shape rỗng hoặc dữ liệu mesh lỗi thời, hãy đảm bảo gọi ``await get_tree().process_frame`` trước khi sử dụng :ref:`bake_collision_shape()<class_CSGShape3D_method_bake_collision_shape>` trong :ref:`Node._ready()<class_Node_private_method__ready>` hoặc sau khi thay đổi các thuộc tính trên **CSGShape3D**.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_bake_static_mesh:

.. rst-class:: classref-method

:ref:`ArrayMesh<class_ArrayMesh>` **bake_static_mesh**\ (\ ) :ref:`🔗<class_CSGShape3D_method_bake_static_mesh>`

Trả về một :ref:`ArrayMesh<class_ArrayMesh>` tĩnh đã bake từ kết quả phép toán CSG của node này. Các material từ những node CSG liên quan được thêm vào dưới dạng các mesh surface bổ sung. Trả về một mesh rỗng nếu node không phải là node gốc CSG hoặc không có geometry hợp lệ.

\ **Lưu ý:** Dữ liệu mesh CSG được cập nhật trì hoãn, nghĩa là chúng được cập nhật sau một frame đã render. Để tránh nhận được mesh rỗng hoặc dữ liệu mesh lỗi thời, hãy đảm bảo gọi ``await get_tree().process_frame`` trước khi sử dụng :ref:`bake_static_mesh()<class_CSGShape3D_method_bake_static_mesh>` trong :ref:`Node._ready()<class_Node_private_method__ready>` hoặc sau khi thay đổi các thuộc tính trên **CSGShape3D**.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_get_collision_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CSGShape3D_method_get_collision_layer_value>`

Trả về việc layer được chỉ định của :ref:`collision_layer<class_CSGShape3D_property_collision_layer>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CSGShape3D_method_get_collision_mask_value>`

Trả về việc layer được chỉ định của :ref:`collision_mask<class_CSGShape3D_property_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_get_meshes:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_meshes**\ (\ ) |const| :ref:`🔗<class_CSGShape3D_method_get_meshes>`

Trả về một :ref:`Array<class_Array>` gồm hai phần tử: phần tử đầu tiên là :ref:`Transform3D<class_Transform3D>` của node này và phần tử thứ hai là :ref:`Mesh<class_Mesh>` gốc của node này. Chỉ hoạt động khi node này là shape gốc.

\ **Lưu ý:** Dữ liệu mesh CSG được cập nhật trì hoãn, nghĩa là chúng được cập nhật sau một frame đã render. Để tránh nhận được shape rỗng hoặc dữ liệu mesh lỗi thời, hãy đảm bảo gọi ``await get_tree().process_frame`` trước khi sử dụng :ref:`get_meshes()<class_CSGShape3D_method_get_meshes>` trong :ref:`Node._ready()<class_Node_private_method__ready>` hoặc sau khi thay đổi các thuộc tính trên **CSGShape3D**.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_is_root_shape:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_root_shape**\ (\ ) |const| :ref:`🔗<class_CSGShape3D_method_is_root_shape>`

Trả về ``true`` nếu đây là shape gốc và do đó là object được render.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_set_collision_layer_value:

.. rst-class:: classref-method

|void| **set_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CSGShape3D_method_set_collision_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_layer<class_CSGShape3D_property_collision_layer>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CSGShape3D_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CSGShape3D_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_mask<class_CSGShape3D_property_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
