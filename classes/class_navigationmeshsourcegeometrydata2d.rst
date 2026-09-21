:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationMeshSourceGeometryData2D.xml.

.. _class_NavigationMeshSourceGeometryData2D:

NavigationMeshSourceGeometryData2D
==================================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Container chứa dữ liệu hình học nguồn đã được phân tích cú pháp, được sử dụng để bake navigation mesh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Container chứa dữ liệu hình học nguồn đã được phân tích cú pháp, được sử dụng để bake navigation mesh.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`add_obstruction_outline<class_NavigationMeshSourceGeometryData2D_method_add_obstruction_outline>`\ (\ shape_outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                             |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`add_projected_obstruction<class_NavigationMeshSourceGeometryData2D_method_add_projected_obstruction>`\ (\ vertices\: :ref:`PackedVector2Array<class_PackedVector2Array>`, carve\: :ref:`bool<class_bool>`\ )             |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`add_traversable_outline<class_NavigationMeshSourceGeometryData2D_method_add_traversable_outline>`\ (\ shape_outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                             |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`append_obstruction_outlines<class_NavigationMeshSourceGeometryData2D_method_append_obstruction_outlines>`\ (\ obstruction_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`append_traversable_outlines<class_NavigationMeshSourceGeometryData2D_method_append_traversable_outlines>`\ (\ traversable_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`clear<class_NavigationMeshSourceGeometryData2D_method_clear>`\ (\ )                                                                                                                                                      |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`clear_projected_obstructions<class_NavigationMeshSourceGeometryData2D_method_clear_projected_obstructions>`\ (\ )                                                                                                        |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                                                        | :ref:`get_bounds<class_NavigationMeshSourceGeometryData2D_method_get_bounds>`\ (\ )                                                                                                                                            |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`get_obstruction_outlines<class_NavigationMeshSourceGeometryData2D_method_get_obstruction_outlines>`\ (\ ) |const|                                                                                                        |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                        | :ref:`get_projected_obstructions<class_NavigationMeshSourceGeometryData2D_method_get_projected_obstructions>`\ (\ ) |const|                                                                                                    |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`get_traversable_outlines<class_NavigationMeshSourceGeometryData2D_method_get_traversable_outlines>`\ (\ ) |const|                                                                                                        |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`has_data<class_NavigationMeshSourceGeometryData2D_method_has_data>`\ (\ )                                                                                                                                                |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`merge<class_NavigationMeshSourceGeometryData2D_method_merge>`\ (\ other_geometry\: :ref:`NavigationMeshSourceGeometryData2D<class_NavigationMeshSourceGeometryData2D>`\ )                                                |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_obstruction_outlines<class_NavigationMeshSourceGeometryData2D_method_set_obstruction_outlines>`\ (\ obstruction_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ )       |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_projected_obstructions<class_NavigationMeshSourceGeometryData2D_method_set_projected_obstructions>`\ (\ projected_obstructions\: :ref:`Array<class_Array>`\ )                                                        |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_traversable_outlines<class_NavigationMeshSourceGeometryData2D_method_set_traversable_outlines>`\ (\ traversable_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ )       |
   +----------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_NavigationMeshSourceGeometryData2D_method_add_obstruction_outline:

.. rst-class:: classref-method

|void| **add_obstruction_outline**\ (\ shape_outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_add_obstruction_outline>`

Thêm các điểm trên đường bao của một shape dưới dạng khu vực bị cản trở.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_add_projected_obstruction:

.. rst-class:: classref-method

|void| **add_projected_obstruction**\ (\ vertices\: :ref:`PackedVector2Array<class_PackedVector2Array>`, carve\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_add_projected_obstruction>`

Thêm một shape cản trở được chiếu vào hình học nguồn. Nếu ``carve`` là ``true`` thì shape được khoét sẽ không chịu ảnh hưởng của các offset bổ sung (ví dụ: bán kính agent) trong quá trình bake navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_add_traversable_outline:

.. rst-class:: classref-method

|void| **add_traversable_outline**\ (\ shape_outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_add_traversable_outline>`

Thêm các điểm trên đường bao của một shape dưới dạng khu vực có thể đi qua.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_append_obstruction_outlines:

.. rst-class:: classref-method

|void| **append_obstruction_outlines**\ (\ obstruction_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_append_obstruction_outlines>`

Nối thêm một mảng ``obstruction_outlines`` vào cuối mảng đường bao bị cản trở hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_append_traversable_outlines:

.. rst-class:: classref-method

|void| **append_traversable_outlines**\ (\ traversable_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_append_traversable_outlines>`

Nối thêm một mảng ``traversable_outlines`` vào cuối mảng đường bao có thể đi qua hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_clear>`

Xóa dữ liệu nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_clear_projected_obstructions:

.. rst-class:: classref-method

|void| **clear_projected_obstructions**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_clear_projected_obstructions>`

Xóa tất cả các vật cản được chiếu.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_get_bounds:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **get_bounds**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_get_bounds>`

Trả về một bounding box căn chỉnh theo trục, bao phủ tất cả dữ liệu hình học được lưu trữ. Các giới hạn được tính khi gọi hàm này và kết quả được lưu trong cache cho đến khi có thay đổi hình học tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_get_obstruction_outlines:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **get_obstruction_outlines**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_get_obstruction_outlines>`

Trả về tất cả các mảng đường bao của khu vực bị cản trở.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_get_projected_obstructions:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_projected_obstructions**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_get_projected_obstructions>`

Trả về các vật cản được chiếu dưới dạng một :ref:`Array<class_Array>` gồm các dictionary. Mỗi :ref:`Dictionary<class_Dictionary>` chứa các mục sau:

- ``vertices`` - Một :ref:`PackedFloat32Array<class_PackedFloat32Array>` xác định các điểm trên đường bao của shape được chiếu.

- ``carve`` - Một :ref:`bool<class_bool>` xác định cách shape được chiếu ảnh hưởng đến việc bake navigation mesh. Nếu ``true`` thì shape được chiếu sẽ không chịu ảnh hưởng của các offset bổ sung, ví dụ: bán kính agent.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_get_traversable_outlines:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **get_traversable_outlines**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_get_traversable_outlines>`

Trả về tất cả các mảng đường bao của khu vực có thể đi qua.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_has_data:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_data**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_has_data>`

Trả về ``true`` khi tồn tại dữ liệu hình học nguồn đã được phân tích cú pháp.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_merge:

.. rst-class:: classref-method

|void| **merge**\ (\ other_geometry\: :ref:`NavigationMeshSourceGeometryData2D<class_NavigationMeshSourceGeometryData2D>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_merge>`

Thêm dữ liệu hình học của một **NavigationMeshSourceGeometryData2D** khác vào dữ liệu bake navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_set_obstruction_outlines:

.. rst-class:: classref-method

|void| **set_obstruction_outlines**\ (\ obstruction_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_set_obstruction_outlines>`

Thiết lập tất cả các mảng đường bao của khu vực bị cản trở.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_set_projected_obstructions:

.. rst-class:: classref-method

|void| **set_projected_obstructions**\ (\ projected_obstructions\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_set_projected_obstructions>`

Thiết lập các vật cản được chiếu bằng một Array gồm các Dictionary với các cặp key-value sau:


.. tabs::

 .. code-tab:: gdscript

    "vertices" : PackedFloat32Array
    "carve" : bool



.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData2D_method_set_traversable_outlines:

.. rst-class:: classref-method

|void| **set_traversable_outlines**\ (\ traversable_outlines\: :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\]\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData2D_method_set_traversable_outlines>`

Thiết lập tất cả các mảng đường bao của khu vực có thể đi qua.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
