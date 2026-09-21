:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/HeightMapShape3D.xml.

.. _class_HeightMapShape3D:

HeightMapShape3D
================

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một shape heightmap 3D được dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một shape heightmap 3D, được thiết kế để sử dụng trong vật lý nhằm cung cấp shape cho một :ref:`CollisionShape3D<class_CollisionShape3D>`. Kiểu này thường được dùng nhất cho địa hình với các đỉnh được bố trí trên một lưới có chiều rộng cố định.

Heightmap được biểu diễn dưới dạng lưới 2D gồm các giá trị độ cao, biểu thị vị trí của các điểm lưới trên trục Y. Các điểm lưới cách nhau 1 đơn vị trên các trục X và Z, và lưới được căn giữa tại gốc của node :ref:`CollisionShape3D<class_CollisionShape3D>`. Bên trong, mỗi ô lưới được chia thành hai tam giác.

Do đặc tính của heightmap, nó không thể được dùng để mô hình hóa phần nhô ra hoặc hang động, vốn yêu cầu nhiều đỉnh ở cùng một vị trí theo phương dọc. Có thể tạo lỗ xuyên qua va chạm bằng cách gán :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` cho độ cao của các đỉnh mong muốn (tính năng này được hỗ trợ trong cả GodotPhysics3D và Jolt Physics). Sau đó, bạn có thể chèn các mesh có collision riêng để tạo phần nhô ra, hang động, v.v.

\ **Hiệu năng:** **HeightMapShape3D** kiểm tra va chạm nhanh hơn :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>`, nhưng chậm hơn đáng kể so với các primitive shape như :ref:`BoxShape3D<class_BoxShape3D>`.

Cũng có thể xây dựng shape va chạm heightmap bằng cách sử dụng một tham chiếu :ref:`Image<class_Image>`:


.. tabs::

 .. code-tab:: gdscript

    var heightmap_texture = ResourceLoader.load("res://heightmap_image.exr")
    var heightmap_image = heightmap_texture.get_image()
    heightmap_image.convert(Image.FORMAT_RF)

    var height_min = 0.0
    var height_max = 10.0

    update_map_data_from_image(heightmap_image, height_min, height_max)



\ **Lưu ý:** Nếu cần sử dụng khoảng cách khác 1 đơn vị, bạn có thể điều chỉnh :ref:`Node3D.scale<class_Node3D_property_scale>` của shape. Tuy nhiên, hãy nhớ rằng GodotPhysics3D không hỗ trợ scaling không đồng nhất: bạn sẽ cần scale trục Y bằng cùng một lượng như các trục X và Z, điều đó có nghĩa là các giá trị trong :ref:`map_data<class_HeightMapShape3D_property_map_data>` sẽ cần được scale trước bằng nghịch đảo của scale đó. Cũng lưu ý rằng GodotPhysics3D hoàn toàn không hỗ trợ scaling cho các dynamic body (tức là các node :ref:`RigidBody3D<class_RigidBody3D>` không bị đóng băng); để sử dụng **HeightMapShape3D** đã scale với các body này, bạn sẽ cần dùng Jolt Physics.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------+------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`map_data<class_HeightMapShape3D_property_map_data>`   | ``PackedFloat32Array(0, 0, 0, 0)`` |
   +-----------------------------------------------------+-------------------------------------------------------------+------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`map_depth<class_HeightMapShape3D_property_map_depth>` | ``2``                              |
   +-----------------------------------------------------+-------------------------------------------------------------+------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`map_width<class_HeightMapShape3D_property_map_width>` | ``2``                              |
   +-----------------------------------------------------+-------------------------------------------------------------+------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_max_height<class_HeightMapShape3D_method_get_max_height>`\ (\ ) |const|                                                                                                                                    |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_min_height<class_HeightMapShape3D_method_get_min_height>`\ (\ ) |const|                                                                                                                                    |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`update_map_data_from_image<class_HeightMapShape3D_method_update_map_data_from_image>`\ (\ image\: :ref:`Image<class_Image>`, height_min\: :ref:`float<class_float>`, height_max\: :ref:`float<class_float>`\ ) |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_HeightMapShape3D_property_map_data:

.. rst-class:: classref-property

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **map_data** = ``PackedFloat32Array(0, 0, 0, 0)`` :ref:`🔗<class_HeightMapShape3D_property_map_data>`

.. rst-class:: classref-property-setget

- |void| **set_map_data**\ (\ value\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) - :ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_map_data**\ (\ )

Dữ liệu heightmap. Kích thước của mảng phải bằng :ref:`map_width<class_HeightMapShape3D_property_map_width>` nhân với :ref:`map_depth<class_HeightMapShape3D_property_map_depth>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat32Array<class_PackedFloat32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_HeightMapShape3D_property_map_depth:

.. rst-class:: classref-property

:ref:`int<class_int>` **map_depth** = ``2`` :ref:`🔗<class_HeightMapShape3D_property_map_depth>`

.. rst-class:: classref-property-setget

- |void| **set_map_depth**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_map_depth**\ (\ )

Số lượng đỉnh theo chiều sâu của heightmap. Việc thay đổi giá trị này sẽ thay đổi kích thước của :ref:`map_data<class_HeightMapShape3D_property_map_data>`.

.. rst-class:: classref-item-separator

----

.. _class_HeightMapShape3D_property_map_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **map_width** = ``2`` :ref:`🔗<class_HeightMapShape3D_property_map_width>`

.. rst-class:: classref-property-setget

- |void| **set_map_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_map_width**\ (\ )

Số lượng đỉnh theo chiều rộng của heightmap. Việc thay đổi giá trị này sẽ thay đổi kích thước của :ref:`map_data<class_HeightMapShape3D_property_map_data>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_HeightMapShape3D_method_get_max_height:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_max_height**\ (\ ) |const| :ref:`🔗<class_HeightMapShape3D_method_get_max_height>`

Trả về giá trị độ cao lớn nhất được tìm thấy trong :ref:`map_data<class_HeightMapShape3D_property_map_data>`. Chỉ tính toán lại khi :ref:`map_data<class_HeightMapShape3D_property_map_data>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_HeightMapShape3D_method_get_min_height:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_min_height**\ (\ ) |const| :ref:`🔗<class_HeightMapShape3D_method_get_min_height>`

Trả về giá trị độ cao nhỏ nhất được tìm thấy trong :ref:`map_data<class_HeightMapShape3D_property_map_data>`. Chỉ tính toán lại khi :ref:`map_data<class_HeightMapShape3D_property_map_data>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_HeightMapShape3D_method_update_map_data_from_image:

.. rst-class:: classref-method

|void| **update_map_data_from_image**\ (\ image\: :ref:`Image<class_Image>`, height_min\: :ref:`float<class_float>`, height_max\: :ref:`float<class_float>`\ ) :ref:`🔗<class_HeightMapShape3D_method_update_map_data_from_image>`

Cập nhật :ref:`map_data<class_HeightMapShape3D_property_map_data>` bằng dữ liệu đọc từ một tham chiếu :ref:`Image<class_Image>`. Tự động thay đổi kích thước heightmap :ref:`map_width<class_HeightMapShape3D_property_map_width>` và :ref:`map_depth<class_HeightMapShape3D_property_map_depth>` để vừa với toàn bộ chiều rộng và chiều cao của image.

Image phải ở định dạng :ref:`Image.FORMAT_RF<class_Image_constant_FORMAT_RF>` (32 bit), :ref:`Image.FORMAT_RH<class_Image_constant_FORMAT_RH>` (16 bit) hoặc :ref:`Image.FORMAT_R8<class_Image_constant_FORMAT_R8>` (8 bit).

Mỗi pixel của image được đọc dưới dạng float trong khoảng từ ``0.0`` (pixel đen) đến ``1.0`` (pixel trắng). Giá trị khoảng này được ánh xạ lại thành ``height_min`` và ``height_max`` để tạo ra giá trị độ cao cuối cùng.

\ **Lưu ý:** Khuyến nghị sử dụng heightmap có dữ liệu 16 bit hoặc 32 bit, được lưu ở định dạng EXR hoặc HDR. Việc sử dụng dữ liệu độ cao 8 bit, hoặc định dạng như PNG mà Godot import dưới dạng 8 bit, sẽ tạo ra địa hình dạng bậc thang.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
