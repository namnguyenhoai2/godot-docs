:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/OccluderInstance3D.xml.

.. _class_OccluderInstance3D:

OccluderInstance3D
==================

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Cung cấp tính năng occlusion culling cho các node 3D, giúp cải thiện hiệu suất trong các khu vực khép kín.

.. rst-class:: classref-introduction-group

Mô tả
-----

Occlusion culling có thể cải thiện hiệu suất rendering trong các khu vực khép kín/bán mở bằng cách ẩn hình học bị các đối tượng khác che khuất.

Hệ thống occlusion culling chủ yếu là tĩnh. **OccluderInstance3D**\ s có thể được di chuyển hoặc ẩn tại run-time, nhưng việc này sẽ kích hoạt quá trình tính toán lại trong background và có thể mất vài frame. Bạn nên chỉ di chuyển **OccluderInstance3D**\ s không thường xuyên (ví dụ: cho mục đích procedural generation), thay vì thực hiện việc này ở mỗi frame.

Hệ thống occlusion culling hoạt động bằng cách rendering các occluder trên CPU song song bằng `Embree <https://www.embree.org/>`__, vẽ kết quả vào một buffer có độ phân giải thấp, sau đó dùng buffer này để cull từng node 3D. Trong 3D editor, bạn có thể xem trước buffer occlusion culling bằng cách chọn **Perspective > Display Advanced... > Occlusion Culling Buffer** ở góc trên bên trái của 3D viewport. Có thể điều chỉnh chất lượng của buffer occlusion culling trong Project Settings.

\ **Baking:** Chọn một node **OccluderInstance3D**, sau đó sử dụng nút **Bake Occluders** ở phía trên 3D editor. Chỉ các material opaque mới được tính đến; các material trong suốt (alpha-blended hoặc alpha-tested) sẽ bị bỏ qua khi tạo occluder.

\ **Lưu ý:** Occlusion culling chỉ hiệu quả nếu :ref:`ProjectSettings.rendering/occlusion_culling/use_occlusion_culling<class_ProjectSettings_property_rendering/occlusion_culling/use_occlusion_culling>` là ``true``. Việc bật occlusion culling sẽ tạo thêm chi phí cho CPU. Chỉ bật occlusion culling nếu bạn thực sự dự định sử dụng nó. Các scene lớn, mở, có ít hoặc không có đối tượng chắn tầm nhìn thường sẽ không được hưởng lợi nhiều từ occlusion culling. Các scene lớn, mở thường hưởng lợi nhiều hơn từ mesh LOD và visibility ranges (:ref:`GeometryInstance3D.visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>` và :ref:`GeometryInstance3D.visibility_range_end<class_GeometryInstance3D_property_visibility_range_end>`) so với occlusion culling.

\ **Lưu ý:** Do các giới hạn về bộ nhớ, occlusion culling không được hỗ trợ mặc định trong các Web export template. Có thể bật tính năng này bằng cách biên dịch các Web export template tùy chỉnh với ``module_raycast_enabled=yes``.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Occlusion culling <../tutorials/3d/occlusion_culling>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------+----------------+
   | :ref:`int<class_int>`               | :ref:`bake_mask<class_OccluderInstance3D_property_bake_mask>`                                       | ``4294967295`` |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>`           | :ref:`bake_simplification_distance<class_OccluderInstance3D_property_bake_simplification_distance>` | ``0.1``        |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------+----------------+
   | :ref:`Occluder3D<class_Occluder3D>` | :ref:`occluder<class_OccluderInstance3D_property_occluder>`                                         |                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------+----------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_bake_mask_value<class_OccluderInstance3D_method_get_bake_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_bake_mask_value<class_OccluderInstance3D_method_set_bake_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OccluderInstance3D_property_bake_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **bake_mask** = ``4294967295`` :ref:`🔗<class_OccluderInstance3D_property_bake_mask>`

.. rst-class:: classref-property-setget

- |void| **set_bake_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bake_mask**\ (\ )

Các visual layer cần được tính đến khi baking cho occluder. Chỉ các :ref:`MeshInstance3D<class_MeshInstance3D>`\ s có :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>` khớp với :ref:`bake_mask<class_OccluderInstance3D_property_bake_mask>` này mới được đưa vào occluder mesh được tạo. Theo mặc định, tất cả đối tượng có material *opaque* đều được tính đến khi baking occluder.

Để cải thiện hiệu suất và tránh artifact, bạn nên loại trừ các đối tượng động, đối tượng nhỏ và fixture khỏi quá trình baking bằng cách chuyển chúng sang một visual layer riêng và loại trừ layer này trong :ref:`bake_mask<class_OccluderInstance3D_property_bake_mask>`.

.. rst-class:: classref-item-separator

----

.. _class_OccluderInstance3D_property_bake_simplification_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **bake_simplification_distance** = ``0.1`` :ref:`🔗<class_OccluderInstance3D_property_bake_simplification_distance>`

.. rst-class:: classref-property-setget

- |void| **set_bake_simplification_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bake_simplification_distance**\ (\ )

Khoảng cách simplification được sử dụng để đơn giản hóa polygon của occluder được tạo (theo đơn vị 3D). Giá trị cao hơn tạo ra occluder mesh ít chi tiết hơn, giúp cải thiện hiệu suất nhưng làm giảm độ chính xác của việc culling.

Hình học của occluder được render trên CPU, vì vậy điều quan trọng là giữ cho hình học của nó đơn giản nhất có thể. Vì buffer được render ở độ phân giải thấp, các occluder mesh ít chi tiết hơn nhìn chung vẫn hoạt động tốt. Giá trị mặc định khá mạnh, vì vậy bạn có thể phải giảm giá trị này nếu gặp false negative (các đối tượng bị coi là đã bị che khuất dù camera vẫn nhìn thấy chúng). Giá trị ``0.01`` sẽ hoạt động theo hướng thận trọng và giữ cho hình học *về mặt cảm nhận* không bị ảnh hưởng trong buffer occlusion culling. Tùy theo scene, giá trị ``0.01`` vẫn có thể đơn giản hóa mesh đáng kể so với việc tắt hoàn toàn simplification.

Đặt giá trị này thành ``0.0`` sẽ tắt hoàn toàn simplification, nhưng các vertex ở đúng cùng một vị trí vẫn sẽ được hợp nhất. Mesh cũng sẽ được đánh lại index để giảm cả số lượng vertex lẫn index.

\ **Lưu ý:** Tính năng này sử dụng thư viện `meshoptimizer <https://meshoptimizer.org/>`__ ở bên dưới, tương tự như quá trình tạo LOD.

.. rst-class:: classref-item-separator

----

.. _class_OccluderInstance3D_property_occluder:

.. rst-class:: classref-property

:ref:`Occluder3D<class_Occluder3D>` **occluder** :ref:`🔗<class_OccluderInstance3D_property_occluder>`

.. rst-class:: classref-property-setget

- |void| **set_occluder**\ (\ value\: :ref:`Occluder3D<class_Occluder3D>`\ ) - :ref:`Occluder3D<class_Occluder3D>` **get_occluder**\ (\ )

Resource occluder cho **OccluderInstance3D** này. Bạn có thể tạo resource occluder bằng cách chọn một node **OccluderInstance3D**, sau đó sử dụng nút **Bake Occluders** ở phía trên editor.

Bạn cũng có thể tự vẽ một polygon occluder 2D bằng cách thêm một resource :ref:`PolygonOccluder3D<class_PolygonOccluder3D>` mới vào thuộc tính :ref:`occluder<class_OccluderInstance3D_property_occluder>` trong Inspector.

Ngoài ra, bạn có thể chọn một primitive occluder để sử dụng: :ref:`QuadOccluder3D<class_QuadOccluder3D>`, :ref:`BoxOccluder3D<class_BoxOccluder3D>` hoặc :ref:`SphereOccluder3D<class_SphereOccluder3D>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OccluderInstance3D_method_get_bake_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_bake_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_OccluderInstance3D_method_get_bake_mask_value>`

Trả về việc layer được chỉ định của :ref:`bake_mask<class_OccluderInstance3D_property_bake_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_OccluderInstance3D_method_set_bake_mask_value:

.. rst-class:: classref-method

|void| **set_bake_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_OccluderInstance3D_method_set_bake_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`bake_mask<class_OccluderInstance3D_property_bake_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
