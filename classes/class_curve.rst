:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Curve.xml.

.. _class_Curve:

Đường cong
==========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một đường cong toán học.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource này mô tả một đường cong toán học bằng cách xác định một tập hợp các điểm và tiếp tuyến tại mỗi điểm. Theo mặc định, nó nằm trong khoảng từ ``0`` đến ``1`` trên các trục X và Y, nhưng các khoảng này có thể được thay đổi.

Lưu ý rằng nhiều resource và node giả định rằng chúng được cung cấp *unit curve*. Unit curve là đường cong có miền xác định (trục X) nằm giữa ``0`` và ``1``. Một số ví dụ về việc sử dụng unit curve là :ref:`CPUParticles2D.angle_curve<class_CPUParticles2D_property_angle_curve>` và :ref:`Line2D.width_curve<class_Line2D_property_width_curve>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`bake_resolution<class_Curve_property_bake_resolution>`                         | ``100``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`max_domain<class_Curve_property_max_domain>`                                   | ``1.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`max_value<class_Curve_property_max_value>`                                     | ``1.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`min_domain<class_Curve_property_min_domain>`                                   | ``0.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`min_value<class_Curve_property_min_value>`                                     | ``0.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`point_count<class_Curve_property_point_count>`                                 | ``0``             |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`point_{index}/left_mode<class_Curve_property_point_{index}/left_mode>`         | ``0``             |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`point_{index}/left_tangent<class_Curve_property_point_{index}/left_tangent>`   | ``0.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`point_{index}/position<class_Curve_property_point_{index}/position>`           | ``Vector2(0, 0)`` |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`point_{index}/right_mode<class_Curve_property_point_{index}/right_mode>`       | ``0``             |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`point_{index}/right_tangent<class_Curve_property_point_{index}/right_tangent>` | ``0.0``           |
   +-------------------------------+--------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                      | :ref:`add_point<class_Curve_method_add_point>`\ (\ position\: :ref:`Vector2<class_Vector2>`, left_tangent\: :ref:`float<class_float>` = 0, right_tangent\: :ref:`float<class_float>` = 0, left_mode\: :ref:`TangentMode<enum_Curve_TangentMode>` = 0, right_mode\: :ref:`TangentMode<enum_Curve_TangentMode>` = 0\ ) |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`bake<class_Curve_method_bake>`\ (\ )                                                                                                                                                                                                                                                                           |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`clean_dupes<class_Curve_method_clean_dupes>`\ (\ )                                                                                                                                                                                                                                                             |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`clear_points<class_Curve_method_clear_points>`\ (\ )                                                                                                                                                                                                                                                           |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`get_domain_range<class_Curve_method_get_domain_range>`\ (\ ) |const|                                                                                                                                                                                                                                           |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TangentMode<enum_Curve_TangentMode>` | :ref:`get_point_left_mode<class_Curve_method_get_point_left_mode>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                      |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`get_point_left_tangent<class_Curve_method_get_point_left_tangent>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`              | :ref:`get_point_position<class_Curve_method_get_point_position>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                        |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TangentMode<enum_Curve_TangentMode>` | :ref:`get_point_right_mode<class_Curve_method_get_point_right_mode>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                    |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`get_point_right_tangent<class_Curve_method_get_point_right_tangent>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                              |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`get_value_range<class_Curve_method_get_value_range>`\ (\ ) |const|                                                                                                                                                                                                                                             |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`remove_point<class_Curve_method_remove_point>`\ (\ index\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                            |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`sample<class_Curve_method_sample>`\ (\ offset\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                                                           |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                  | :ref:`sample_baked<class_Curve_method_sample_baked>`\ (\ offset\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                                               |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`set_point_left_mode<class_Curve_method_set_point_left_mode>`\ (\ index\: :ref:`int<class_int>`, mode\: :ref:`TangentMode<enum_Curve_TangentMode>`\ )                                                                                                                                                           |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`set_point_left_tangent<class_Curve_method_set_point_left_tangent>`\ (\ index\: :ref:`int<class_int>`, tangent\: :ref:`float<class_float>`\ )                                                                                                                                                                   |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                      | :ref:`set_point_offset<class_Curve_method_set_point_offset>`\ (\ index\: :ref:`int<class_int>`, offset\: :ref:`float<class_float>`\ )                                                                                                                                                                                |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`set_point_right_mode<class_Curve_method_set_point_right_mode>`\ (\ index\: :ref:`int<class_int>`, mode\: :ref:`TangentMode<enum_Curve_TangentMode>`\ )                                                                                                                                                         |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`set_point_right_tangent<class_Curve_method_set_point_right_tangent>`\ (\ index\: :ref:`int<class_int>`, tangent\: :ref:`float<class_float>`\ )                                                                                                                                                                 |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                     | :ref:`set_point_value<class_Curve_method_set_point_value>`\ (\ index\: :ref:`int<class_int>`, y\: :ref:`float<class_float>`\ )                                                                                                                                                                                       |
   +--------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_Curve_signal_domain_changed:

.. rst-class:: classref-signal

**domain_changed**\ (\ ) :ref:`🔗<class_Curve_signal_domain_changed>`

Được phát ra khi :ref:`max_domain<class_Curve_property_max_domain>` hoặc :ref:`min_domain<class_Curve_property_min_domain>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Curve_signal_range_changed:

.. rst-class:: classref-signal

**range_changed**\ (\ ) :ref:`🔗<class_Curve_signal_range_changed>`

Được phát ra khi :ref:`max_value<class_Curve_property_max_value>` hoặc :ref:`min_value<class_Curve_property_min_value>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Kiểu liệt kê
------------

.. _enum_Curve_TangentMode:

.. rst-class:: classref-enumeration

enum **TangentMode**: :ref:`🔗<enum_Curve_TangentMode>`

.. _class_Curve_constant_TANGENT_FREE:

.. rst-class:: classref-enumeration-constant

:ref:`TangentMode<enum_Curve_TangentMode>` **TANGENT_FREE** = ``0``

Tiếp tuyến ở phía này của điểm do người dùng định nghĩa.

.. _class_Curve_constant_TANGENT_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`TangentMode<enum_Curve_TangentMode>` **TANGENT_LINEAR** = ``1``

Đường cong tính tiếp tuyến ở phía này của điểm bằng độ dốc tới điểm liền kề, tính tại vị trí giữa hai điểm.

.. _class_Curve_constant_TANGENT_MODE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`TangentMode<enum_Curve_TangentMode>` **TANGENT_MODE_COUNT** = ``2``

Tổng số chế độ tiếp tuyến hiện có.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Curve_property_bake_resolution:

.. rst-class:: classref-property

:ref:`int<class_int>` **bake_resolution** = ``100`` :ref:`🔗<class_Curve_property_bake_resolution>`

.. rst-class:: classref-property-setget

- |void| **set_bake_resolution**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bake_resolution**\ (\ )

Số điểm được đưa vào dữ liệu đường cong đã bake (tức là đã được cache).

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_max_domain:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_domain** = ``1.0`` :ref:`🔗<class_Curve_property_max_domain>`

.. rst-class:: classref-property-setget

- |void| **set_max_domain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_domain**\ (\ )

Miền xác định tối đa (tọa độ x) mà các điểm có thể có.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_max_value:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_value** = ``1.0`` :ref:`🔗<class_Curve_property_max_value>`

.. rst-class:: classref-property-setget

- |void| **set_max_value**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_value**\ (\ )

Giá trị tối đa (tọa độ y) mà các điểm có thể có. Các tiếp tuyến có thể khiến các giá trị nằm giữa các điểm cao hơn.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_min_domain:

.. rst-class:: classref-property

:ref:`float<class_float>` **min_domain** = ``0.0`` :ref:`🔗<class_Curve_property_min_domain>`

.. rst-class:: classref-property-setget

- |void| **set_min_domain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_min_domain**\ (\ )

Miền xác định tối thiểu (tọa độ x) mà các điểm có thể có.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_min_value:

.. rst-class:: classref-property

:ref:`float<class_float>` **min_value** = ``0.0`` :ref:`🔗<class_Curve_property_min_value>`

.. rst-class:: classref-property-setget

- |void| **set_min_value**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_min_value**\ (\ )

Giá trị tối thiểu (tọa độ y) mà các điểm có thể có. Các tiếp tuyến có thể khiến các giá trị nằm giữa các điểm thấp hơn.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **point_count** = ``0`` :ref:`🔗<class_Curve_property_point_count>`

.. rst-class:: classref-property-setget

- |void| **set_point_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_point_count**\ (\ )

Số điểm mô tả đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_{index}/left_mode:

.. rst-class:: classref-property

:ref:`int<class_int>` **point_{index}/left_mode** = ``0`` :ref:`🔗<class_Curve_property_point_{index}/left_mode>`

:ref:`TangentMode<enum_Curve_TangentMode>` bên trái cho điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong khoảng ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_{index}/left_tangent:

.. rst-class:: classref-property

:ref:`float<class_float>` **point_{index}/left_tangent** = ``0.0`` :ref:`🔗<class_Curve_property_point_{index}/left_tangent>`

Góc tiếp tuyến bên trái (tính theo độ) cho điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong khoảng ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_{index}/position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **point_{index}/position** = ``Vector2(0, 0)`` :ref:`🔗<class_Curve_property_point_{index}/position>`

Vị trí của điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong khoảng ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_{index}/right_mode:

.. rst-class:: classref-property

:ref:`int<class_int>` **point_{index}/right_mode** = ``0`` :ref:`🔗<class_Curve_property_point_{index}/right_mode>`

:ref:`TangentMode<enum_Curve_TangentMode>` bên phải cho điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong khoảng ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_property_point_{index}/right_tangent:

.. rst-class:: classref-property

:ref:`float<class_float>` **point_{index}/right_tangent** = ``0.0`` :ref:`🔗<class_Curve_property_point_{index}/right_tangent>`

Góc tiếp tuyến bên phải (tính theo độ) cho điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong khoảng ``0 .. point_count - 1``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Curve_method_add_point:

.. rst-class:: classref-method

:ref:`int<class_int>` **add_point**\ (\ position\: :ref:`Vector2<class_Vector2>`, left_tangent\: :ref:`float<class_float>` = 0, right_tangent\: :ref:`float<class_float>` = 0, left_mode\: :ref:`TangentMode<enum_Curve_TangentMode>` = 0, right_mode\: :ref:`TangentMode<enum_Curve_TangentMode>` = 0\ ) :ref:`🔗<class_Curve_method_add_point>`

Thêm một điểm vào đường cong. Với mỗi phía, nếu ``*_mode`` là :ref:`TANGENT_LINEAR<class_Curve_constant_TANGENT_LINEAR>`, góc ``*_tangent`` (tính theo độ) sẽ sử dụng độ dốc của đường cong tại vị trí giữa điểm đó và điểm liền kề. Cho phép gán tùy chỉnh cho góc ``*_tangent`` nếu ``*_mode`` được đặt thành :ref:`TANGENT_FREE<class_Curve_constant_TANGENT_FREE>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_bake:

.. rst-class:: classref-method

|void| **bake**\ (\ ) :ref:`🔗<class_Curve_method_bake>`

Tính toán lại cache đã bake của các điểm trên đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_clean_dupes:

.. rst-class:: classref-method

|void| **clean_dupes**\ (\ ) :ref:`🔗<class_Curve_method_clean_dupes>`

Xóa các điểm trùng lặp, tức là những điểm cách điểm lân cận trên đường cong chưa đến 0.00001 đơn vị (giá trị epsilon của engine).

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_clear_points:

.. rst-class:: classref-method

|void| **clear_points**\ (\ ) :ref:`🔗<class_Curve_method_clear_points>`

Xóa tất cả các điểm khỏi đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_domain_range:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_domain_range**\ (\ ) |const| :ref:`🔗<class_Curve_method_get_domain_range>`

Trả về độ chênh lệch giữa :ref:`min_domain<class_Curve_property_min_domain>` và :ref:`max_domain<class_Curve_property_max_domain>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_point_left_mode:

.. rst-class:: classref-method

:ref:`TangentMode<enum_Curve_TangentMode>` **get_point_left_mode**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve_method_get_point_left_mode>`

Trả về :ref:`TangentMode<enum_Curve_TangentMode>` bên trái cho điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_point_left_tangent:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_point_left_tangent**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve_method_get_point_left_tangent>`

Trả về góc tiếp tuyến bên trái (tính theo độ) cho điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_position**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve_method_get_point_position>`

Trả về tọa độ đường cong của điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_point_right_mode:

.. rst-class:: classref-method

:ref:`TangentMode<enum_Curve_TangentMode>` **get_point_right_mode**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve_method_get_point_right_mode>`

Trả về :ref:`TangentMode<enum_Curve_TangentMode>` bên phải cho điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_point_right_tangent:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_point_right_tangent**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve_method_get_point_right_tangent>`

Trả về góc tiếp tuyến bên phải (tính theo độ) cho điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_get_value_range:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_value_range**\ (\ ) |const| :ref:`🔗<class_Curve_method_get_value_range>`

Trả về độ chênh lệch giữa :ref:`min_value<class_Curve_property_min_value>` và :ref:`max_value<class_Curve_property_max_value>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Curve_method_remove_point>`

Xóa điểm tại ``index`` khỏi đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_sample:

.. rst-class:: classref-method

:ref:`float<class_float>` **sample**\ (\ offset\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve_method_sample>`

Trả về giá trị Y của điểm sẽ tồn tại tại vị trí X ``offset`` dọc theo đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_sample_baked:

.. rst-class:: classref-method

:ref:`float<class_float>` **sample_baked**\ (\ offset\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve_method_sample_baked>`

Trả về giá trị Y của điểm sẽ tồn tại tại vị trí X ``offset`` dọc theo đường cong bằng cache đã bake. Bake các điểm của đường cong nếu chưa được bake.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_left_mode:

.. rst-class:: classref-method

|void| **set_point_left_mode**\ (\ index\: :ref:`int<class_int>`, mode\: :ref:`TangentMode<enum_Curve_TangentMode>`\ ) :ref:`🔗<class_Curve_method_set_point_left_mode>`

Đặt :ref:`TangentMode<enum_Curve_TangentMode>` bên trái cho điểm tại ``index`` thành ``mode``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_left_tangent:

.. rst-class:: classref-method

|void| **set_point_left_tangent**\ (\ index\: :ref:`int<class_int>`, tangent\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Curve_method_set_point_left_tangent>`

Đặt góc tiếp tuyến bên trái cho điểm tại ``index`` thành ``tangent``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_offset:

.. rst-class:: classref-method

:ref:`int<class_int>` **set_point_offset**\ (\ index\: :ref:`int<class_int>`, offset\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Curve_method_set_point_offset>`

Gán vị trí ngang ``offset`` cho điểm tại ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_right_mode:

.. rst-class:: classref-method

|void| **set_point_right_mode**\ (\ index\: :ref:`int<class_int>`, mode\: :ref:`TangentMode<enum_Curve_TangentMode>`\ ) :ref:`🔗<class_Curve_method_set_point_right_mode>`

Đặt :ref:`TangentMode<enum_Curve_TangentMode>` bên phải cho điểm tại ``index`` thành ``mode``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_right_tangent:

.. rst-class:: classref-method

|void| **set_point_right_tangent**\ (\ index\: :ref:`int<class_int>`, tangent\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Curve_method_set_point_right_tangent>`

Đặt góc tiếp tuyến bên phải cho điểm tại ``index`` thành ``tangent``.

.. rst-class:: classref-item-separator

----

.. _class_Curve_method_set_point_value:

.. rst-class:: classref-method

|void| **set_point_value**\ (\ index\: :ref:`int<class_int>`, y\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Curve_method_set_point_value>`

Gán vị trí dọc ``y`` cho điểm tại ``index``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
