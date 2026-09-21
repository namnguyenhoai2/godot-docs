:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Polygon2D.xml.

.. _class_Polygon2D:

Polygon2D
=========

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một polygon 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Polygon2D được định nghĩa bằng một tập hợp các điểm. Mỗi điểm được nối với điểm tiếp theo, trong đó điểm cuối được nối với điểm đầu, tạo thành một polygon khép kín. Polygon2D có thể được tô màu (màu đơn hoặc gradient) hoặc tô bằng một texture đã cho.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`antialiased<class_Polygon2D_property_antialiased>`                     | ``false``                |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`                           | :ref:`color<class_Polygon2D_property_color>`                                 | ``Color(1, 1, 1, 1)``    |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                               | :ref:`internal_vertex_count<class_Polygon2D_property_internal_vertex_count>` | ``0``                    |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`invert_border<class_Polygon2D_property_invert_border>`                 | ``100.0``                |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`invert_enabled<class_Polygon2D_property_invert_enabled>`               | ``false``                |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`offset<class_Polygon2D_property_offset>`                               | ``Vector2(0, 0)``        |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`polygon<class_Polygon2D_property_polygon>`                             | ``PackedVector2Array()`` |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Array<class_Array>`                           | :ref:`polygons<class_Polygon2D_property_polygons>`                           | ``[]``                   |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`NodePath<class_NodePath>`                     | :ref:`skeleton<class_Polygon2D_property_skeleton>`                           | ``NodePath("")``         |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>`                   | :ref:`texture<class_Polygon2D_property_texture>`                             |                          |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`texture_offset<class_Polygon2D_property_texture_offset>`               | ``Vector2(0, 0)``        |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`texture_rotation<class_Polygon2D_property_texture_rotation>`           | ``0.0``                  |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`texture_scale<class_Polygon2D_property_texture_scale>`                 | ``Vector2(1, 1)``        |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`uv<class_Polygon2D_property_uv>`                                       | ``PackedVector2Array()`` |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>`     | :ref:`vertex_colors<class_Polygon2D_property_vertex_colors>`                 | ``PackedColorArray()``   |
   +-----------------------------------------------------+------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_bone<class_Polygon2D_method_add_bone>`\ (\ path\: :ref:`NodePath<class_NodePath>`, weights\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )        |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_bones<class_Polygon2D_method_clear_bones>`\ (\ )                                                                                                         |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`erase_bone<class_Polygon2D_method_erase_bone>`\ (\ index\: :ref:`int<class_int>`\ )                                                                            |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_bone_count<class_Polygon2D_method_get_bone_count>`\ (\ ) |const|                                                                                           |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                     | :ref:`get_bone_path<class_Polygon2D_method_get_bone_path>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                              |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`get_bone_weights<class_Polygon2D_method_get_bone_weights>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_bone_path<class_Polygon2D_method_set_bone_path>`\ (\ index\: :ref:`int<class_int>`, path\: :ref:`NodePath<class_NodePath>`\ )                              |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_bone_weights<class_Polygon2D_method_set_bone_weights>`\ (\ index\: :ref:`int<class_int>`, weights\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |
   +-----------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Polygon2D_property_antialiased:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **antialiased** = ``false`` :ref:`🔗<class_Polygon2D_property_antialiased>`

.. rst-class:: classref-property-setget

- |void| **set_antialiased**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_antialiased**\ (\ )

Nếu ``true``, các cạnh của polygon sẽ được khử răng cưa.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Polygon2D_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

Màu tô của polygon. Nếu :ref:`texture<class_Polygon2D_property_texture>` được thiết lập, nó sẽ được nhân với màu này. Đây cũng sẽ là màu mặc định cho các đỉnh chưa được thiết lập trong :ref:`vertex_colors<class_Polygon2D_property_vertex_colors>`.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_internal_vertex_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **internal_vertex_count** = ``0`` :ref:`🔗<class_Polygon2D_property_internal_vertex_count>`

.. rst-class:: classref-property-setget

- |void| **set_internal_vertex_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_internal_vertex_count**\ (\ )

Số lượng đỉnh bên trong, được dùng cho ánh xạ UV.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_invert_border:

.. rst-class:: classref-property

:ref:`float<class_float>` **invert_border** = ``100.0`` :ref:`🔗<class_Polygon2D_property_invert_border>`

.. rst-class:: classref-property-setget

- |void| **set_invert_border**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_invert_border**\ (\ )

Phần đệm được thêm vào bounding box khi :ref:`invert_enabled<class_Polygon2D_property_invert_enabled>` được đặt thành ``true``. Đặt giá trị này quá nhỏ có thể dẫn đến lỗi "Bad Polygon".

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_invert_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **invert_enabled** = ``false`` :ref:`🔗<class_Polygon2D_property_invert_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_invert_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_invert_enabled**\ (\ )

Nếu ``true``, polygon sẽ được đảo ngược, bao gồm vùng bên ngoài các điểm đã định nghĩa và mở rộng đến :ref:`invert_border<class_Polygon2D_property_invert_border>`.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Polygon2D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Độ lệch được áp dụng cho mỗi đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_polygon:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **polygon** = ``PackedVector2Array()`` :ref:`🔗<class_Polygon2D_property_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_polygon**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_polygon**\ (\ )

Danh sách các đỉnh của polygon. Điểm cuối sẽ được nối với điểm đầu.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_polygons:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **polygons** = ``[]`` :ref:`🔗<class_Polygon2D_property_polygons>`

.. rst-class:: classref-property-setget

- |void| **set_polygons**\ (\ value\: :ref:`Array<class_Array>`\ ) - :ref:`Array<class_Array>` **get_polygons**\ (\ )

Danh sách các polygon, dùng trong trường hợp biểu diễn nhiều hơn một polygon. Mỗi polygon riêng lẻ được lưu trữ dưới dạng :ref:`PackedInt32Array<class_PackedInt32Array>`, trong đó mỗi :ref:`int<class_int>` là một chỉ mục đến một điểm trong :ref:`polygon<class_Polygon2D_property_polygon>`. Nếu rỗng, thuộc tính này sẽ bị bỏ qua và polygon đơn kết quả sẽ được tạo từ tất cả các điểm trong :ref:`polygon<class_Polygon2D_property_polygon>`, theo thứ tự chúng được lưu trữ.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_skeleton:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **skeleton** = ``NodePath("")`` :ref:`🔗<class_Polygon2D_property_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_skeleton**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_skeleton**\ (\ )

Đường dẫn đến một node :ref:`Skeleton2D<class_Skeleton2D>` được dùng cho các biến dạng dựa trên skeleton của polygon này. Nếu trống hoặc không hợp lệ, biến dạng xương sẽ không được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_Polygon2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

Texture tô của polygon. Dùng :ref:`uv<class_Polygon2D_property_uv>` để thiết lập tọa độ texture.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_texture_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **texture_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Polygon2D_property_texture_offset>`

.. rst-class:: classref-property-setget

- |void| **set_texture_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_texture_offset**\ (\ )

Độ lệch áp dụng cho :ref:`texture<class_Polygon2D_property_texture>` của polygon. Nếu được đặt thành ``Vector2(0, 0)``, gốc của texture (góc trên bên trái) sẽ được đặt tại vị trí của polygon.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_texture_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **texture_rotation** = ``0.0`` :ref:`🔗<class_Polygon2D_property_texture_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_texture_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_texture_rotation**\ (\ )

Độ xoay của texture, tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_texture_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **texture_scale** = ``Vector2(1, 1)`` :ref:`🔗<class_Polygon2D_property_texture_scale>`

.. rst-class:: classref-property-setget

- |void| **set_texture_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_texture_scale**\ (\ )

Hệ số nhân các tọa độ :ref:`uv<class_Polygon2D_property_uv>` khi sử dụng :ref:`texture<class_Polygon2D_property_texture>`. Giá trị lớn hơn làm texture nhỏ hơn và ngược lại.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_uv:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **uv** = ``PackedVector2Array()`` :ref:`🔗<class_Polygon2D_property_uv>`

.. rst-class:: classref-property-setget

- |void| **set_uv**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_uv**\ (\ )

Tọa độ texture cho mỗi đỉnh của polygon. Mỗi đỉnh polygon nên có một giá trị UV. Nếu số lượng ít hơn, các đỉnh chưa được định nghĩa sẽ sử dụng ``Vector2(0, 0)``.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_property_vertex_colors:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **vertex_colors** = ``PackedColorArray()`` :ref:`🔗<class_Polygon2D_property_vertex_colors>`

.. rst-class:: classref-property-setget

- |void| **set_vertex_colors**\ (\ value\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) - :ref:`PackedColorArray<class_PackedColorArray>` **get_vertex_colors**\ (\ )

Màu cho mỗi đỉnh. Màu được nội suy giữa các đỉnh, tạo ra các gradient mượt mà. Mỗi đỉnh polygon nên có một màu. Nếu số lượng ít hơn, các đỉnh chưa được định nghĩa sẽ sử dụng :ref:`color<class_Polygon2D_property_color>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Polygon2D_method_add_bone:

.. rst-class:: classref-method

|void| **add_bone**\ (\ path\: :ref:`NodePath<class_NodePath>`, weights\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_Polygon2D_method_add_bone>`

Thêm một bone với ``path`` và ``weights`` đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_clear_bones:

.. rst-class:: classref-method

|void| **clear_bones**\ (\ ) :ref:`🔗<class_Polygon2D_method_clear_bones>`

Xóa tất cả bone khỏi **Polygon2D** này.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_erase_bone:

.. rst-class:: classref-method

|void| **erase_bone**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Polygon2D_method_erase_bone>`

Xóa bone đã chỉ định khỏi **Polygon2D** này.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_get_bone_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bone_count**\ (\ ) |const| :ref:`🔗<class_Polygon2D_method_get_bone_count>`

Trả về số lượng bone trong **Polygon2D** này.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_get_bone_path:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_bone_path**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Polygon2D_method_get_bone_path>`

Trả về đường dẫn đến node liên kết với bone đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_get_bone_weights:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_bone_weights**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Polygon2D_method_get_bone_weights>`

Trả về các giá trị weight của bone đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_set_bone_path:

.. rst-class:: classref-method

|void| **set_bone_path**\ (\ index\: :ref:`int<class_int>`, path\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_Polygon2D_method_set_bone_path>`

Thiết lập đường dẫn đến node liên kết với bone đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Polygon2D_method_set_bone_weights:

.. rst-class:: classref-method

|void| **set_bone_weights**\ (\ index\: :ref:`int<class_int>`, weights\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_Polygon2D_method_set_bone_weights>`

Thiết lập các giá trị weight cho bone đã chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
