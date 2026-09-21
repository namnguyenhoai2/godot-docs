:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AABB.xml.

.. _class_AABB:

AABB
====

Một bounding box căn chỉnh theo trục trong không gian 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu dựng sẵn **AABB** :ref:`Variant<class_Variant>` đại diện cho một bounding box căn chỉnh theo trục trong không gian 3D. Nó được xác định bởi :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>`, vốn là :ref:`Vector3<class_Vector3>`. Kiểu này thường được dùng để kiểm tra chồng lấn nhanh (xem :ref:`intersects()<class_AABB_method_intersects>`). Mặc dù bản thân **AABB** được căn chỉnh theo trục, nó có thể kết hợp với :ref:`Transform3D<class_Transform3D>` để biểu diễn một bounding box bị xoay hoặc xiên.

Nó sử dụng tọa độ dấu phẩy động. Kiểu tương ứng trong 2D của **AABB** là :ref:`Rect2<class_Rect2>`. Không có phiên bản **AABB** nào sử dụng tọa độ số nguyên.

\ **Lưu ý:** Các giá trị âm của :ref:`size<class_AABB_property_size>` không được hỗ trợ. Khi kích thước âm, hầu hết các phương thức của **AABB** không hoạt động chính xác. Hãy dùng :ref:`abs()<class_AABB_method_abs>` để lấy một **AABB** tương đương có kích thước không âm.

\ **Lưu ý:** Trong ngữ cảnh boolean, một **AABB** được đánh giá là ``false`` nếu cả :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>` đều bằng không (bằng :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`). Nếu không, nó luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Math documentation index <../tutorials/math/index>`

- :doc:`Vector math <../tutorials/math/vector_math>`

- :doc:`Advanced vector math <../tutorials/math/vectors_advanced>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`end<class_AABB_property_end>`           | ``Vector3(0, 0, 0)`` |
   +-------------------------------+-----------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`position<class_AABB_property_position>` | ``Vector3(0, 0, 0)`` |
   +-------------------------------+-----------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_AABB_property_size>`         | ``Vector3(0, 0, 0)`` |
   +-------------------------------+-----------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Hàm khởi tạo
------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`AABB<class_AABB_constructor_AABB>`\ (\ )                                                                                 |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`AABB<class_AABB_constructor_AABB>`\ (\ from\: :ref:`AABB<class_AABB>`\ )                                                 |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`AABB<class_AABB_constructor_AABB>`\ (\ position\: :ref:`Vector3<class_Vector3>`, size\: :ref:`Vector3<class_Vector3>`\ ) |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`       | :ref:`abs<class_AABB_method_abs>`\ (\ ) |const|                                                                                                         |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`encloses<class_AABB_method_encloses>`\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const|                                                               |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`       | :ref:`expand<class_AABB_method_expand>`\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                         |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_center<class_AABB_method_get_center>`\ (\ ) |const|                                                                                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_endpoint<class_AABB_method_get_endpoint>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                          |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_longest_axis<class_AABB_method_get_longest_axis>`\ (\ ) |const|                                                                               |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_longest_axis_index<class_AABB_method_get_longest_axis_index>`\ (\ ) |const|                                                                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_longest_axis_size<class_AABB_method_get_longest_axis_size>`\ (\ ) |const|                                                                     |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_shortest_axis<class_AABB_method_get_shortest_axis>`\ (\ ) |const|                                                                             |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_shortest_axis_index<class_AABB_method_get_shortest_axis_index>`\ (\ ) |const|                                                                 |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_shortest_axis_size<class_AABB_method_get_shortest_axis_size>`\ (\ ) |const|                                                                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_support<class_AABB_method_get_support>`\ (\ direction\: :ref:`Vector3<class_Vector3>`\ ) |const|                                              |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_volume<class_AABB_method_get_volume>`\ (\ ) |const|                                                                                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`       | :ref:`grow<class_AABB_method_grow>`\ (\ by\: :ref:`float<class_float>`\ ) |const|                                                                       |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`has_point<class_AABB_method_has_point>`\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                      |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`has_surface<class_AABB_method_has_surface>`\ (\ ) |const|                                                                                         |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`has_volume<class_AABB_method_has_volume>`\ (\ ) |const|                                                                                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`       | :ref:`intersection<class_AABB_method_intersection>`\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const|                                                       |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`intersects<class_AABB_method_intersects>`\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const|                                                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`intersects_plane<class_AABB_method_intersects_plane>`\ (\ plane\: :ref:`Plane<class_Plane>`\ ) |const|                                            |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`intersects_ray<class_AABB_method_intersects_ray>`\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`\ ) |const|        |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`intersects_segment<class_AABB_method_intersects_segment>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`\ ) |const| |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_equal_approx<class_AABB_method_is_equal_approx>`\ (\ aabb\: :ref:`AABB<class_AABB>`\ ) |const|                                                 |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_finite<class_AABB_method_is_finite>`\ (\ ) |const|                                                                                             |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`       | :ref:`merge<class_AABB_method_merge>`\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const|                                                                     |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator !=<class_AABB_operator_neq_AABB>`\ (\ right\: :ref:`AABB<class_AABB>`\ )                     |
   +-------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`operator *<class_AABB_operator_mul_Transform3D>`\ (\ right\: :ref:`Transform3D<class_Transform3D>`\ ) |
   +-------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator ==<class_AABB_operator_eq_AABB>`\ (\ right\: :ref:`AABB<class_AABB>`\ )                      |
   +-------------------------+-------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AABB_property_end:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **end** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_AABB_property_end>`

Điểm kết thúc. Đây thường là góc phía trên bên phải và phía sau của bounding box, tương đương với ``position + size``. Việc đặt điểm này sẽ ảnh hưởng đến :ref:`size<class_AABB_property_size>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_property_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_AABB_property_position>`

Điểm gốc. Đây thường là góc phía dưới bên trái và phía trước của bounding box.

.. rst-class:: classref-item-separator

----

.. _class_AABB_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_AABB_property_size>`

Chiều rộng, chiều cao và chiều sâu của bounding box, bắt đầu từ :ref:`position<class_AABB_property_position>`. Việc đặt giá trị này cũng ảnh hưởng đến điểm :ref:`end<class_AABB_property_end>`.

\ **Lưu ý:** Bạn nên đặt chiều rộng, chiều cao và chiều sâu thành các giá trị không âm. Nguyên nhân là hầu hết các phương thức trong Godot giả định rằng :ref:`position<class_AABB_property_position>` là góc phía dưới bên trái và phía trước, còn :ref:`end<class_AABB_property_end>` là góc phía trên bên phải và phía sau. Để lấy một bounding box tương đương có kích thước không âm, hãy dùng :ref:`abs()<class_AABB_method_abs>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_AABB_constructor_AABB:

.. rst-class:: classref-constructor

:ref:`AABB<class_AABB>` **AABB**\ (\ ) :ref:`🔗<class_AABB_constructor_AABB>`

Tạo một **AABB** với :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>` được đặt thành :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`AABB<class_AABB>` **AABB**\ (\ from\: :ref:`AABB<class_AABB>`\ )

Tạo một **AABB** bằng cách sao chép **AABB** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`AABB<class_AABB>` **AABB**\ (\ position\: :ref:`Vector3<class_Vector3>`, size\: :ref:`Vector3<class_Vector3>`\ )

Tạo một **AABB** bằng cách ``position`` và ``size``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AABB_method_abs:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **abs**\ (\ ) |const| :ref:`🔗<class_AABB_method_abs>`

Trả về một **AABB** tương đương với bounding box này, với chiều rộng, chiều cao và chiều sâu được thay đổi thành các giá trị không âm.


.. tabs::

 .. code-tab:: gdscript

    var box = AABB(Vector3(5, 0, 5), Vector3(-20, -10, -5))
    var absolute = box.abs()
    print(absolute.position) # In ra (-15.0, -10.0, 0.0)
    print(absolute.size)     # In ra (20.0, 10.0, 5.0)

 .. code-tab:: csharp

    var box = new Aabb(new Vector3(5, 0, 5), new Vector3(-20, -10, -5));
    var absolute = box.Abs();
    GD.Print(absolute.Position); // In ra (-15, -10, 0)
    GD.Print(absolute.Size);     // In ra (20, 10, 5)



\ **Lưu ý:** Bạn nên sử dụng phương thức này khi :ref:`size<class_AABB_property_size>` là số âm, vì hầu hết các phương thức khác trong Godot giả định rằng các thành phần của :ref:`size<class_AABB_property_size>` lớn hơn ``0``.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_encloses:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **encloses**\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_AABB_method_encloses>`

Trả về ``true`` nếu bounding box này *bao kín hoàn toàn* hộp ``with``. Các cạnh của cả hai hộp đều được tính.


.. tabs::

 .. code-tab:: gdscript

    var a = AABB(Vector3(0, 0, 0), Vector3(4, 4, 4))
    var b = AABB(Vector3(1, 1, 1), Vector3(3, 3, 3))
    var c = AABB(Vector3(2, 2, 2), Vector3(8, 8, 8))

    print(a.encloses(a)) # In ra true
    print(a.encloses(b)) # In ra true
    print(a.encloses(c)) # In ra false

 .. code-tab:: csharp

    var a = new Aabb(new Vector3(0, 0, 0), new Vector3(4, 4, 4));
    var b = new Aabb(new Vector3(1, 1, 1), new Vector3(3, 3, 3));
    var c = new Aabb(new Vector3(2, 2, 2), new Vector3(8, 8, 8));

    GD.Print(a.Encloses(a)); // In ra True
    GD.Print(a.Encloses(b)); // In ra True
    GD.Print(a.Encloses(c)); // In ra False



.. rst-class:: classref-item-separator

----

.. _class_AABB_method_expand:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **expand**\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AABB_method_expand>`

Trả về một bản sao của bounding box này, được mở rộng để căn chỉnh các cạnh với ``to_point`` đã cho nếu cần.


.. tabs::

 .. code-tab:: gdscript

    var box = AABB(Vector3(0, 0, 0), Vector3(5, 2, 5))

    box = box.expand(Vector3(10, 0, 0))
    print(box.position) # In ra (0.0, 0.0, 0.0)
    print(box.size)     # In ra (10.0, 2.0, 5.0)

    box = box.expand(Vector3(-5, 0, 5))
    print(box.position) # In ra (-5.0, 0.0, 0.0)
    print(box.size)     # In ra (15.0, 2.0, 5.0)

 .. code-tab:: csharp

    var box = new Aabb(new Vector3(0, 0, 0), new Vector3(5, 2, 5));

    box = box.Expand(new Vector3(10, 0, 0));
    GD.Print(box.Position); // In ra (0, 0, 0)
    GD.Print(box.Size);     // In ra (10, 2, 5)

    box = box.Expand(new Vector3(-5, 0, 5));
    GD.Print(box.Position); // In ra (-5, 0, 0)
    GD.Print(box.Size);     // In ra (15, 2, 5)



.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_center:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_center**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_center>`

Trả về điểm tâm của bounding box. Điểm này giống với ``position + (size / 2.0)``.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_endpoint:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_endpoint**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AABB_method_get_endpoint>`

Trả về vị trí của một trong 8 đỉnh tạo nên bounding box này. Với ``idx`` bằng ``0``, vị trí này giống với :ref:`position<class_AABB_property_position>`, còn ``idx`` bằng ``7`` thì giống với :ref:`end<class_AABB_property_end>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_longest_axis:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_longest_axis**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_longest_axis>`

Trả về trục chuẩn hóa dài nhất của :ref:`size<class_AABB_property_size>` của bounding box này, dưới dạng :ref:`Vector3<class_Vector3>` (:ref:`Vector3.RIGHT<class_Vector3_constant_RIGHT>`, :ref:`Vector3.UP<class_Vector3_constant_UP>` hoặc :ref:`Vector3.BACK<class_Vector3_constant_BACK>`).


.. tabs::

 .. code-tab:: gdscript

    var box = AABB(Vector3(0, 0, 0), Vector3(2, 4, 8))

    print(box.get_longest_axis())       # In ra (0.0, 0.0, 1.0)
    print(box.get_longest_axis_index()) # In ra 2
    print(box.get_longest_axis_size())  # In ra 8.0

 .. code-tab:: csharp

    var box = new Aabb(new Vector3(0, 0, 0), new Vector3(2, 4, 8));

    GD.Print(box.GetLongestAxis());      // In ra (0, 0, 1)
    GD.Print(box.GetLongestAxisIndex()); // In ra Z
    GD.Print(box.GetLongestAxisSize());  // In ra 8



Xem thêm :ref:`get_longest_axis_index()<class_AABB_method_get_longest_axis_index>` và :ref:`get_longest_axis_size()<class_AABB_method_get_longest_axis_size>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_longest_axis_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_longest_axis_index**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_longest_axis_index>`

Trả về chỉ mục của trục dài nhất trong :ref:`size<class_AABB_property_size>` của bounding box này (xem :ref:`Vector3.AXIS_X<class_Vector3_constant_AXIS_X>`, :ref:`Vector3.AXIS_Y<class_Vector3_constant_AXIS_Y>` và :ref:`Vector3.AXIS_Z<class_Vector3_constant_AXIS_Z>`).

Xem :ref:`get_longest_axis()<class_AABB_method_get_longest_axis>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_longest_axis_size:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_longest_axis_size**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_longest_axis_size>`

Trả về kích thước dài nhất của :ref:`size<class_AABB_property_size>` của bounding box này.

Xem :ref:`get_longest_axis()<class_AABB_method_get_longest_axis>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_shortest_axis:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_shortest_axis**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_shortest_axis>`

Trả về trục chuẩn hóa ngắn nhất của :ref:`size<class_AABB_property_size>` của bounding box này, dưới dạng :ref:`Vector3<class_Vector3>` (:ref:`Vector3.RIGHT<class_Vector3_constant_RIGHT>`, :ref:`Vector3.UP<class_Vector3_constant_UP>` hoặc :ref:`Vector3.BACK<class_Vector3_constant_BACK>`).


.. tabs::

 .. code-tab:: gdscript

    var box = AABB(Vector3(0, 0, 0), Vector3(2, 4, 8))

    print(box.get_shortest_axis())       # In ra (1.0, 0.0, 0.0)
    print(box.get_shortest_axis_index()) # In ra 0
    print(box.get_shortest_axis_size())  # In ra 2.0

 .. code-tab:: csharp

    var box = new Aabb(new Vector3(0, 0, 0), new Vector3(2, 4, 8));

    GD.Print(box.GetShortestAxis());      // In ra (1, 0, 0)
    GD.Print(box.GetShortestAxisIndex()); // In ra X
    GD.Print(box.GetShortestAxisSize());  // In ra 2



Xem thêm :ref:`get_shortest_axis_index()<class_AABB_method_get_shortest_axis_index>` và :ref:`get_shortest_axis_size()<class_AABB_method_get_shortest_axis_size>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_shortest_axis_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_shortest_axis_index**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_shortest_axis_index>`

Trả về chỉ mục của trục ngắn nhất trong :ref:`size<class_AABB_property_size>` của bounding box này (xem :ref:`Vector3.AXIS_X<class_Vector3_constant_AXIS_X>`, :ref:`Vector3.AXIS_Y<class_Vector3_constant_AXIS_Y>` và :ref:`Vector3.AXIS_Z<class_Vector3_constant_AXIS_Z>`).

Xem :ref:`get_shortest_axis()<class_AABB_method_get_shortest_axis>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_shortest_axis_size:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_shortest_axis_size**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_shortest_axis_size>`

Trả về kích thước ngắn nhất của :ref:`size<class_AABB_property_size>` của bounding box này.

Xem :ref:`get_shortest_axis()<class_AABB_method_get_shortest_axis>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_support:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_support**\ (\ direction\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AABB_method_get_support>`

Trả về vị trí của đỉnh thuộc bounding box này nằm xa nhất theo hướng đã cho. Điểm này thường được gọi là support point trong các thuật toán phát hiện va chạm.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_get_volume:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_volume**\ (\ ) |const| :ref:`🔗<class_AABB_method_get_volume>`

Trả về thể tích của bounding box. Giá trị này tương đương với ``size.x * size.y * size.z``. Xem thêm :ref:`has_volume()<class_AABB_method_has_volume>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_grow:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **grow**\ (\ by\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_AABB_method_grow>`

Trả về một bản sao của bounding box này, được mở rộng ở mọi phía một lượng ``by`` đã cho. Lượng âm sẽ thu nhỏ hộp.


.. tabs::

 .. code-tab:: gdscript

    var a = AABB(Vector3(4, 4, 4), Vector3(8, 8, 8)).grow(4)
    print(a.position) # In ra (0.0, 0.0, 0.0)
    print(a.size)     # In ra (16.0, 16.0, 16.0)

    var b = AABB(Vector3(0, 0, 0), Vector3(8, 4, 2)).grow(2)
    print(b.position) # In ra (-2.0, -2.0, -2.0)
    print(b.size)     # In ra (12.0, 8.0, 6.0)

 .. code-tab:: csharp

    var a = new Aabb(new Vector3(4, 4, 4), new Vector3(8, 8, 8)).Grow(4);
    GD.Print(a.Position); // In ra (0, 0, 0)
    GD.Print(a.Size);     // In ra (16, 16, 16)

    var b = new Aabb(new Vector3(0, 0, 0), new Vector3(8, 4, 2)).Grow(2);
    GD.Print(b.Position); // In ra (-2, -2, -2)
    GD.Print(b.Size);     // In ra (12, 8, 6)



.. rst-class:: classref-item-separator

----

.. _class_AABB_method_has_point:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_point**\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AABB_method_has_point>`

Trả về ``true`` nếu bounding box chứa ``point`` đã cho. Theo quy ước, các điểm nằm chính xác trên phía bên phải, phía trên và phía trước sẽ **không** được tính.

\ **Lưu ý:** Phương thức này không đáng tin cậy đối với **AABB** có :ref:`size<class_AABB_property_size>` *âm*. Trước tiên hãy dùng :ref:`abs()<class_AABB_method_abs>` để lấy một bounding box hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_has_surface:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_surface**\ (\ ) |const| :ref:`🔗<class_AABB_method_has_surface>`

Trả về ``true`` nếu bounding box này có một mặt hoặc một độ dài, nghĩa là ít nhất một thành phần của :ref:`size<class_AABB_property_size>` lớn hơn ``0``. Nếu không, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_has_volume:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_volume**\ (\ ) |const| :ref:`🔗<class_AABB_method_has_volume>`

Trả về ``true`` nếu chiều rộng, chiều cao và chiều sâu của bounding box này đều dương. Xem thêm :ref:`get_volume()<class_AABB_method_get_volume>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_intersection:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **intersection**\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_AABB_method_intersection>`

Trả về phần giao giữa bounding box này và ``with``. Nếu các hộp không giao nhau, trả về một **AABB** rỗng. Nếu các hộp giao nhau tại cạnh, trả về một **AABB** phẳng không có thể tích (xem :ref:`has_surface()<class_AABB_method_has_surface>` và :ref:`has_volume()<class_AABB_method_has_volume>`).


.. tabs::

 .. code-tab:: gdscript

    var box1 = AABB(Vector3(0, 0, 0), Vector3(5, 2, 8))
    var box2 = AABB(Vector3(2, 0, 2), Vector3(8, 4, 4))

    var intersection = box1.intersection(box2)
    print(intersection.position) # In ra (2.0, 0.0, 2.0)
    print(intersection.size)     # In ra (3.0, 2.0, 4.0)

 .. code-tab:: csharp

    var box1 = new Aabb(new Vector3(0, 0, 0), new Vector3(5, 2, 8));
    var box2 = new Aabb(new Vector3(2, 0, 2), new Vector3(8, 4, 4));

    var intersection = box1.Intersection(box2);
    GD.Print(intersection.Position); // In ra (2, 0, 2)
    GD.Print(intersection.Size);     // In ra (3, 2, 4)



\ **Lưu ý:** Nếu bạn chỉ cần biết hai bounding box có giao nhau hay không, hãy dùng :ref:`intersects()<class_AABB_method_intersects>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_intersects:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **intersects**\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_AABB_method_intersects>`

Trả về ``true`` nếu bounding box này chồng lấn với hộp ``with``. Các cạnh của cả hai hộp *luôn* bị loại trừ.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_intersects_plane:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **intersects_plane**\ (\ plane\: :ref:`Plane<class_Plane>`\ ) |const| :ref:`🔗<class_AABB_method_intersects_plane>`

Trả về ``true`` nếu bounding box này nằm ở cả hai phía của ``plane`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_intersects_ray:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **intersects_ray**\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AABB_method_intersects_ray>`

Trả về điểm đầu tiên mà bounding box này và ray đã cho giao nhau, dưới dạng :ref:`Vector3<class_Vector3>`. Nếu không xảy ra giao nhau, trả về ``null``.

Ray bắt đầu tại ``from``, hướng về ``dir`` và kéo dài đến vô cực.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_intersects_segment:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **intersects_segment**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AABB_method_intersects_segment>`

Trả về điểm đầu tiên mà bounding box này và segment đã cho giao nhau, dưới dạng :ref:`Vector3<class_Vector3>`. Nếu không xảy ra giao nhau, trả về ``null``.

Segment bắt đầu tại ``from`` và kết thúc tại ``to``.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_is_equal_approx:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_equal_approx**\ (\ aabb\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_AABB_method_is_equal_approx>`

Trả về ``true`` nếu bounding box này và ``aabb`` gần như bằng nhau, bằng cách gọi :ref:`Vector3.is_equal_approx()<class_Vector3_method_is_equal_approx>` trên :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_is_finite:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_finite**\ (\ ) |const| :ref:`🔗<class_AABB_method_is_finite>`

Trả về ``true`` nếu các giá trị của hộp bao quanh này là hữu hạn, bằng cách gọi :ref:`Vector3.is_finite()<class_Vector3_method_is_finite>` trên :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_method_merge:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **merge**\ (\ with\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_AABB_method_merge>`

Trả về một **AABB** bao quanh cả hộp bao quanh này và ``with`` dọc theo các cạnh. Xem thêm :ref:`encloses()<class_AABB_method_encloses>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_AABB_operator_neq_AABB:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`AABB<class_AABB>`\ ) :ref:`🔗<class_AABB_operator_neq_AABB>`

Trả về ``true`` nếu :ref:`position<class_AABB_property_position>` hoặc :ref:`size<class_AABB_property_size>` của hai hộp bao quanh không bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác số thực, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_AABB_method_is_equal_approx>` thay thế vì cách này đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_AABB_operator_mul_Transform3D:

.. rst-class:: classref-operator

:ref:`AABB<class_AABB>` **operator ***\ (\ right\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_AABB_operator_mul_Transform3D>`

Biến đổi ngược (nhân) **AABB** bằng ma trận biến đổi :ref:`Transform3D<class_Transform3D>` đã cho, với giả định rằng cơ sở biến đổi là trực chuẩn (orthonormal), tức là phép xoay/phản chiếu được chấp nhận, còn phép co giãn/xiên thì không.

\ ``aabb * transform`` tương đương với ``transform.inverse() * aabb``. Xem :ref:`Transform3D.inverse()<class_Transform3D_method_inverse>`.

Để biến đổi bằng nghịch đảo của một phép biến đổi affine (ví dụ: có phép co giãn), có thể sử dụng ``transform.affine_inverse() * aabb`` thay thế. Xem :ref:`Transform3D.affine_inverse()<class_Transform3D_method_affine_inverse>`.

.. rst-class:: classref-item-separator

----

.. _class_AABB_operator_eq_AABB:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`AABB<class_AABB>`\ ) :ref:`🔗<class_AABB_operator_eq_AABB>`

Trả về ``true`` nếu cả :ref:`position<class_AABB_property_position>` và :ref:`size<class_AABB_property_size>` của các hộp bao quanh lần lượt hoàn toàn bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác số thực, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_AABB_method_is_equal_approx>` thay thế vì cách này đáng tin cậy hơn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
