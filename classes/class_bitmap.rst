:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BitMap.xml.

.. _class_BitMap:

BitMap
======

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Ma trận boolean.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng hai chiều gồm các giá trị boolean, có thể được dùng để lưu trữ hiệu quả một ma trận nhị phân (mỗi phần tử ma trận chỉ chiếm một bit) và truy vấn các giá trị bằng tọa độ Descartes tự nhiên.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Image<class_Image>`                                                        | :ref:`convert_to_image<class_BitMap_method_convert_to_image>`\ (\ ) |const|                                                                                       |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`create<class_BitMap_method_create>`\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ )                                                                           |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`create_from_image_alpha<class_BitMap_method_create_from_image_alpha>`\ (\ image\: :ref:`Image<class_Image>`, threshold\: :ref:`float<class_float>` = 0.1\ ) |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`get_bit<class_BitMap_method_get_bit>`\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`\ ) |const|                                                   |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`get_bitv<class_BitMap_method_get_bitv>`\ (\ position\: :ref:`Vector2i<class_Vector2i>`\ ) |const|                                                           |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>`                                                  | :ref:`get_size<class_BitMap_method_get_size>`\ (\ ) |const|                                                                                                       |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                            | :ref:`get_true_bit_count<class_BitMap_method_get_true_bit_count>`\ (\ ) |const|                                                                                   |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`grow_mask<class_BitMap_method_grow_mask>`\ (\ pixels\: :ref:`int<class_int>`, rect\: :ref:`Rect2i<class_Rect2i>`\ )                                         |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`opaque_to_polygons<class_BitMap_method_opaque_to_polygons>`\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, epsilon\: :ref:`float<class_float>` = 2.0\ ) |const|    |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`resize<class_BitMap_method_resize>`\ (\ new_size\: :ref:`Vector2i<class_Vector2i>`\ )                                                                       |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_bit<class_BitMap_method_set_bit>`\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`, bit\: :ref:`bool<class_bool>`\ )                            |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_bit_rect<class_BitMap_method_set_bit_rect>`\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, bit\: :ref:`bool<class_bool>`\ )                                    |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                           | :ref:`set_bitv<class_BitMap_method_set_bitv>`\ (\ position\: :ref:`Vector2i<class_Vector2i>`, bit\: :ref:`bool<class_bool>`\ )                                    |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_BitMap_method_convert_to_image:

.. rst-class:: classref-method

:ref:`Image<class_Image>` **convert_to_image**\ (\ ) |const| :ref:`🔗<class_BitMap_method_convert_to_image>`

Trả về một hình ảnh có cùng kích thước với bitmap và có :ref:`Format<enum_Image_Format>` thuộc kiểu :ref:`Image.FORMAT_L8<class_Image_constant_FORMAT_L8>`. Các bit ``true`` của bitmap được chuyển đổi thành các pixel màu trắng, còn các bit ``false`` thành màu đen.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_create:

.. rst-class:: classref-method

|void| **create**\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_BitMap_method_create>`

Tạo một bitmap có kích thước được chỉ định, được điền bằng ``false``.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_create_from_image_alpha:

.. rst-class:: classref-method

|void| **create_from_image_alpha**\ (\ image\: :ref:`Image<class_Image>`, threshold\: :ref:`float<class_float>` = 0.1\ ) :ref:`🔗<class_BitMap_method_create_from_image_alpha>`

Tạo một bitmap khớp với kích thước của hình ảnh đã cho; mỗi phần tử của bitmap được đặt thành ``false`` nếu giá trị alpha của hình ảnh tại vị trí đó nhỏ hơn hoặc bằng ``threshold``, và thành ``true`` trong trường hợp còn lại.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_get_bit:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_bit**\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_BitMap_method_get_bit>`

Trả về giá trị của bitmap tại vị trí được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_get_bitv:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_bitv**\ (\ position\: :ref:`Vector2i<class_Vector2i>`\ ) |const| :ref:`🔗<class_BitMap_method_get_bitv>`

Trả về giá trị của bitmap tại vị trí được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_get_size:

.. rst-class:: classref-method

:ref:`Vector2i<class_Vector2i>` **get_size**\ (\ ) |const| :ref:`🔗<class_BitMap_method_get_size>`

Trả về các kích thước của bitmap.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_get_true_bit_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_true_bit_count**\ (\ ) |const| :ref:`🔗<class_BitMap_method_get_true_bit_count>`

Trả về số phần tử của bitmap được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_grow_mask:

.. rst-class:: classref-method

|void| **grow_mask**\ (\ pixels\: :ref:`int<class_int>`, rect\: :ref:`Rect2i<class_Rect2i>`\ ) :ref:`🔗<class_BitMap_method_grow_mask>`

Áp dụng phép giãn nở hoặc co mòn hình thái học cho bitmap. Nếu ``pixels`` dương, phép giãn nở được áp dụng cho bitmap. Nếu ``pixels`` âm, phép co mòn được áp dụng cho bitmap. ``rect`` xác định vùng áp dụng phép toán hình thái học. Các pixel nằm bên ngoài ``rect`` không bị ảnh hưởng bởi :ref:`grow_mask()<class_BitMap_method_grow_mask>`.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_opaque_to_polygons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **opaque_to_polygons**\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, epsilon\: :ref:`float<class_float>` = 2.0\ ) |const| :ref:`🔗<class_BitMap_method_opaque_to_polygons>`

Tạo một :ref:`Array<class_Array>` gồm các đa giác bao phủ một phần hình chữ nhật của bitmap. Phương thức này sử dụng thuật toán marching squares, sau đó dùng phép rút gọn Ramer-Douglas-Peucker (RDP) để giảm số lượng đỉnh. Mỗi đa giác được mô tả dưới dạng :ref:`PackedVector2Array<class_PackedVector2Array>` gồm các đỉnh của nó.

Để lấy các đa giác bao phủ toàn bộ bitmap, hãy truyền:

::

    Rect2(Vector2(), get_size())

\ ``epsilon`` được truyền cho RDP để kiểm soát độ chính xác của việc các đa giác bao phủ bitmap: ``epsilon`` thấp hơn tương ứng với nhiều điểm hơn trong các đa giác.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_resize:

.. rst-class:: classref-method

|void| **resize**\ (\ new_size\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_BitMap_method_resize>`

Thay đổi kích thước hình ảnh thành ``new_size``.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_set_bit:

.. rst-class:: classref-method

|void| **set_bit**\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`, bit\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BitMap_method_set_bit>`

Đặt phần tử của bitmap tại vị trí được chỉ định thành giá trị được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_set_bit_rect:

.. rst-class:: classref-method

|void| **set_bit_rect**\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, bit\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BitMap_method_set_bit_rect>`

Đặt một phần hình chữ nhật của bitmap thành giá trị được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_BitMap_method_set_bitv:

.. rst-class:: classref-method

|void| **set_bitv**\ (\ position\: :ref:`Vector2i<class_Vector2i>`, bit\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BitMap_method_set_bitv>`

Đặt phần tử của bitmap tại vị trí được chỉ định thành giá trị được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
