:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Plane.xml.

.. _class_Plane:

Plane
=====

Một mặt phẳng ở dạng chuẩn Hessian.

.. rst-class:: classref-introduction-group

Mô tả
-----

Biểu diễn một phương trình mặt phẳng đã chuẩn hóa. :ref:`normal<class_Plane_property_normal>` là pháp tuyến của mặt phẳng (a, b, c đã được chuẩn hóa), còn :ref:`d<class_Plane_property_d>` là khoảng cách từ gốc tọa độ đến mặt phẳng (theo hướng của "normal"). Phía "trên" hoặc "bên trên" mặt phẳng được xem là phía của mặt phẳng hướng về nơi pháp tuyến đang chỉ tới.

\ **Lưu ý:** Trong ngữ cảnh boolean, một mặt phẳng sẽ được đánh giá là ``false`` nếu tất cả thành phần của nó bằng ``0``. Nếu không, một mặt phẳng sẽ luôn được đánh giá là ``true``.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Chỉ mục tài liệu Math <../tutorials/math/index>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`d<class_Plane_property_d>`           | ``0.0``              |
   +-------------------------------+--------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`normal<class_Plane_property_normal>` | ``Vector3(0, 0, 0)`` |
   +-------------------------------+--------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`x<class_Plane_property_x>`           | ``0.0``              |
   +-------------------------------+--------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`y<class_Plane_property_y>`           | ``0.0``              |
   +-------------------------------+--------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`z<class_Plane_property_z>`           | ``0.0``              |
   +-------------------------------+--------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ )                                                                                                                             |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ from\: :ref:`Plane<class_Plane>`\ )                                                                                           |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ a\: :ref:`float<class_float>`, b\: :ref:`float<class_float>`, c\: :ref:`float<class_float>`, d\: :ref:`float<class_float>`\ ) |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ normal\: :ref:`Vector3<class_Vector3>`\ )                                                                                     |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ normal\: :ref:`Vector3<class_Vector3>`, d\: :ref:`float<class_float>`\ )                                                      |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ normal\: :ref:`Vector3<class_Vector3>`, point\: :ref:`Vector3<class_Vector3>`\ )                                              |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`Plane<class_Plane_constructor_Plane>`\ (\ point1\: :ref:`Vector3<class_Vector3>`, point2\: :ref:`Vector3<class_Vector3>`, point3\: :ref:`Vector3<class_Vector3>`\ )     |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`distance_to<class_Plane_method_distance_to>`\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                  |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_center<class_Plane_method_get_center>`\ (\ ) |const|                                                                                           |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`has_point<class_Plane_method_has_point>`\ (\ point\: :ref:`Vector3<class_Vector3>`, tolerance\: :ref:`float<class_float>` = 1e-05\ ) |const|       |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`intersect_3<class_Plane_method_intersect_3>`\ (\ b\: :ref:`Plane<class_Plane>`, c\: :ref:`Plane<class_Plane>`\ ) |const|                           |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`intersects_ray<class_Plane_method_intersects_ray>`\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`\ ) |const|        |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`intersects_segment<class_Plane_method_intersects_segment>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`\ ) |const| |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_equal_approx<class_Plane_method_is_equal_approx>`\ (\ to_plane\: :ref:`Plane<class_Plane>`\ ) |const|                                           |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_finite<class_Plane_method_is_finite>`\ (\ ) |const|                                                                                             |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_point_over<class_Plane_method_is_point_over>`\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                              |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>`     | :ref:`normalized<class_Plane_method_normalized>`\ (\ ) |const|                                                                                           |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`project<class_Plane_method_project>`\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                          |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`operator !=<class_Plane_operator_neq_Plane>`\ (\ right\: :ref:`Plane<class_Plane>`\ )                  |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`operator *<class_Plane_operator_mul_Transform3D>`\ (\ right\: :ref:`Transform3D<class_Transform3D>`\ ) |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`operator ==<class_Plane_operator_eq_Plane>`\ (\ right\: :ref:`Plane<class_Plane>`\ )                   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`operator unary+<class_Plane_operator_unplus>`\ (\ )                                                    |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+
   | :ref:`Plane<class_Plane>` | :ref:`operator unary-<class_Plane_operator_unminus>`\ (\ )                                                   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_Plane_constant_PLANE_YZ:

.. rst-class:: classref-constant

**PLANE_YZ** = ``Plane(1, 0, 0, 0)`` :ref:`🔗<class_Plane_constant_PLANE_YZ>`

Một mặt phẳng mở rộng theo các trục Y và Z (vector pháp tuyến hướng theo +X).

.. _class_Plane_constant_PLANE_XZ:

.. rst-class:: classref-constant

**PLANE_XZ** = ``Plane(0, 1, 0, 0)`` :ref:`🔗<class_Plane_constant_PLANE_XZ>`

Một mặt phẳng mở rộng theo các trục X và Z (vector pháp tuyến hướng theo +Y).

.. _class_Plane_constant_PLANE_XY:

.. rst-class:: classref-constant

**PLANE_XY** = ``Plane(0, 0, 1, 0)`` :ref:`🔗<class_Plane_constant_PLANE_XY>`

Một mặt phẳng mở rộng theo các trục X và Y (vector pháp tuyến hướng theo +Z).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Plane_property_d:

.. rst-class:: classref-property

:ref:`float<class_float>` **d** = ``0.0`` :ref:`🔗<class_Plane_property_d>`

Khoảng cách từ gốc tọa độ đến mặt phẳng, được biểu diễn theo :ref:`normal<class_Plane_property_normal>` (dựa trên hướng và độ lớn của nó). Khoảng cách tuyệt đối thực tế từ gốc tọa độ đến mặt phẳng có thể được tính bằng ``abs(d) / normal.length()`` (nếu :ref:`normal<class_Plane_property_normal>` có độ dài bằng không thì **Plane** này không biểu diễn một mặt phẳng hợp lệ).

Trong phương trình vô hướng của mặt phẳng ``ax + by + cz = d``, đây là ``d``, còn các tọa độ ``(a, b, c)`` được biểu diễn bởi thuộc tính :ref:`normal<class_Plane_property_normal>`.

.. rst-class:: classref-item-separator

----

.. _class_Plane_property_normal:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **normal** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Plane_property_normal>`

Pháp tuyến của mặt phẳng, thường là một vector đơn vị. Không nên là vector không, vì **Plane** có :ref:`normal<class_Plane_property_normal>` như vậy không biểu diễn một mặt phẳng hợp lệ.

Trong phương trình vô hướng của mặt phẳng ``ax + by + cz = d``, đây là vector ``(a, b, c)``, trong đó ``d`` là thuộc tính :ref:`d<class_Plane_property_d>`.

.. rst-class:: classref-item-separator

----

.. _class_Plane_property_x:

.. rst-class:: classref-property

:ref:`float<class_float>` **x** = ``0.0`` :ref:`🔗<class_Plane_property_x>`

Thành phần X của vector :ref:`normal<class_Plane_property_normal>` của mặt phẳng.

.. rst-class:: classref-item-separator

----

.. _class_Plane_property_y:

.. rst-class:: classref-property

:ref:`float<class_float>` **y** = ``0.0`` :ref:`🔗<class_Plane_property_y>`

Thành phần Y của vector :ref:`normal<class_Plane_property_normal>` của mặt phẳng.

.. rst-class:: classref-item-separator

----

.. _class_Plane_property_z:

.. rst-class:: classref-property

:ref:`float<class_float>` **z** = ``0.0`` :ref:`🔗<class_Plane_property_z>`

Thành phần Z của vector :ref:`normal<class_Plane_property_normal>` của mặt phẳng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_Plane_constructor_Plane:

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ ) :ref:`🔗<class_Plane_constructor_Plane>`

Khởi tạo một **Plane** mặc định với tất cả thành phần được đặt thành ``0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ from\: :ref:`Plane<class_Plane>`\ )

Khởi tạo một **Plane** dưới dạng bản sao của **Plane** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ a\: :ref:`float<class_float>`, b\: :ref:`float<class_float>`, c\: :ref:`float<class_float>`, d\: :ref:`float<class_float>`\ )

Tạo một mặt phẳng từ bốn tham số. Ba thành phần của :ref:`normal<class_Plane_property_normal>` của mặt phẳng thu được là ``a``, ``b`` và ``c``, còn mặt phẳng có khoảng cách ``d`` từ gốc tọa độ.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ normal\: :ref:`Vector3<class_Vector3>`\ )

Tạo một mặt phẳng từ vector pháp tuyến. Mặt phẳng sẽ giao với gốc tọa độ.

``normal`` của mặt phẳng phải là một vector đơn vị.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ normal\: :ref:`Vector3<class_Vector3>`, d\: :ref:`float<class_float>`\ )

Tạo một mặt phẳng từ vector pháp tuyến và khoảng cách từ mặt phẳng đến gốc tọa độ.

``normal`` của mặt phẳng phải là một vector đơn vị.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ normal\: :ref:`Vector3<class_Vector3>`, point\: :ref:`Vector3<class_Vector3>`\ )

Tạo một mặt phẳng từ vector pháp tuyến và một điểm trên mặt phẳng.

``normal`` của mặt phẳng phải là một vector đơn vị.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Plane<class_Plane>` **Plane**\ (\ point1\: :ref:`Vector3<class_Vector3>`, point2\: :ref:`Vector3<class_Vector3>`, point3\: :ref:`Vector3<class_Vector3>`\ )

Tạo một mặt phẳng từ ba điểm, được cung cấp theo thứ tự chiều kim đồng hồ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Plane_method_distance_to:

.. rst-class:: classref-method

:ref:`float<class_float>` **distance_to**\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Plane_method_distance_to>`

Trả về khoảng cách ngắn nhất từ mặt phẳng đến vị trí ``point``. Nếu điểm nằm trên mặt phẳng, khoảng cách sẽ dương. Nếu nằm dưới, khoảng cách sẽ âm.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_get_center:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_center**\ (\ ) |const| :ref:`🔗<class_Plane_method_get_center>`

Trả về tâm của mặt phẳng.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_has_point:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_point**\ (\ point\: :ref:`Vector3<class_Vector3>`, tolerance\: :ref:`float<class_float>` = 1e-05\ ) |const| :ref:`🔗<class_Plane_method_has_point>`

Trả về ``true`` nếu ``point`` nằm trong mặt phẳng. Phép so sánh sử dụng ngưỡng ``tolerance`` tối thiểu tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_intersect_3:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **intersect_3**\ (\ b\: :ref:`Plane<class_Plane>`, c\: :ref:`Plane<class_Plane>`\ ) |const| :ref:`🔗<class_Plane_method_intersect_3>`

Trả về điểm giao của ba mặt phẳng ``b``, ``c`` và mặt phẳng này. Nếu không tìm thấy giao điểm, ``null`` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_intersects_ray:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **intersects_ray**\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Plane_method_intersects_ray>`

Trả về điểm giao của một ray gồm vị trí ``from`` và pháp tuyến hướng ``dir`` với mặt phẳng này. Nếu không tìm thấy giao điểm, ``null`` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_intersects_segment:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **intersects_segment**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Plane_method_intersects_segment>`

Trả về điểm giao của một đoạn từ vị trí ``from`` đến vị trí ``to`` với mặt phẳng này. Nếu không tìm thấy giao điểm, ``null`` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_is_equal_approx:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_equal_approx**\ (\ to_plane\: :ref:`Plane<class_Plane>`\ ) |const| :ref:`🔗<class_Plane_method_is_equal_approx>`

Trả về ``true`` nếu mặt phẳng này và ``to_plane`` xấp xỉ bằng nhau, bằng cách chạy :ref:`@GlobalScope.is_equal_approx()<class_@GlobalScope_method_is_equal_approx>` trên từng thành phần.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_is_finite:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_finite**\ (\ ) |const| :ref:`🔗<class_Plane_method_is_finite>`

Trả về ``true`` nếu mặt phẳng này là hữu hạn, bằng cách gọi :ref:`@GlobalScope.is_finite()<class_@GlobalScope_method_is_finite>` trên từng thành phần.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_is_point_over:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_point_over**\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Plane_method_is_point_over>`

Trả về ``true`` nếu ``point`` nằm phía trên mặt phẳng.

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_normalized:

.. rst-class:: classref-method

:ref:`Plane<class_Plane>` **normalized**\ (\ ) |const| :ref:`🔗<class_Plane_method_normalized>`

Trả về một bản sao của mặt phẳng với :ref:`normal<class_Plane_property_normal>` đã được chuẩn hóa (tức là một vector đơn vị). Trả về ``Plane(0, 0, 0, 0)`` nếu không thể chuẩn hóa :ref:`normal<class_Plane_property_normal>` (nó có độ dài bằng không).

.. rst-class:: classref-item-separator

----

.. _class_Plane_method_project:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **project**\ (\ point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Plane_method_project>`

Trả về phép chiếu trực giao của ``point`` thành một điểm trên mặt phẳng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_Plane_operator_neq_Plane:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Plane<class_Plane>`\ ) :ref:`🔗<class_Plane_operator_neq_Plane>`

Trả về ``true`` nếu các mặt phẳng không bằng nhau.

\ **Lưu ý:** Do sai số độ chính xác dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Plane_method_is_equal_approx>` thay thế vì đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Plane_operator_mul_Transform3D:

.. rst-class:: classref-operator

:ref:`Plane<class_Plane>` **operator ***\ (\ right\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_Plane_operator_mul_Transform3D>`

Biến đổi ngược (nhân) **Plane** bằng ma trận biến đổi :ref:`Transform3D<class_Transform3D>` đã cho.

\ ``plane * transform`` tương đương với ``transform.affine_inverse() * plane``. Xem :ref:`Transform3D.affine_inverse()<class_Transform3D_method_affine_inverse>`.

.. rst-class:: classref-item-separator

----

.. _class_Plane_operator_eq_Plane:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Plane<class_Plane>`\ ) :ref:`🔗<class_Plane_operator_eq_Plane>`

Trả về ``true`` nếu các mặt phẳng hoàn toàn bằng nhau.

\ **Lưu ý:** Do sai số độ chính xác dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Plane_method_is_equal_approx>` thay thế vì đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Plane_operator_unplus:

.. rst-class:: classref-operator

:ref:`Plane<class_Plane>` **operator unary+**\ (\ ) :ref:`🔗<class_Plane_operator_unplus>`

Trả về cùng giá trị như khi ``+`` không xuất hiện. ``+`` một ngôi không thực hiện thao tác gì, nhưng đôi khi có thể giúp mã của bạn dễ đọc hơn.

.. rst-class:: classref-item-separator

----

.. _class_Plane_operator_unminus:

.. rst-class:: classref-operator

:ref:`Plane<class_Plane>` **operator unary-**\ (\ ) :ref:`🔗<class_Plane_operator_unminus>`

Trả về giá trị âm của **Plane**. Điều này tương đương với việc viết ``Plane(-p.normal, -p.d)``. Phép toán này đảo hướng của vector pháp tuyến và đồng thời đảo giá trị khoảng cách, tạo ra một Plane ở cùng vị trí nhưng hướng theo chiều ngược lại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
