:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/noise/doc_classes/FastNoiseLite.xml.

.. _class_FastNoiseLite:

FastNoiseLite
=============

**Kế thừa:** :ref:`Noise<class_Noise>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tạo noise bằng thư viện FastNoiseLite.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class này tạo noise bằng thư viện FastNoiseLite, một tập hợp gồm nhiều thuật toán noise như Cellular, Perlin, Value và nhiều thuật toán khác.

Hầu hết các giá trị noise được tạo nằm trong phạm vi ``[-1, 1]``, nhưng không phải lúc nào cũng vậy. Một số thuật toán cellular noise trả về kết quả lớn hơn ``1``.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` | :ref:`cellular_distance_function<class_FastNoiseLite_property_cellular_distance_function>`         | ``0``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`cellular_jitter<class_FastNoiseLite_property_cellular_jitter>`                               | ``1.0``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>`             | :ref:`cellular_return_type<class_FastNoiseLite_property_cellular_return_type>`                     | ``1``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`domain_warp_amplitude<class_FastNoiseLite_property_domain_warp_amplitude>`                   | ``30.0``             |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                                      | :ref:`domain_warp_enabled<class_FastNoiseLite_property_domain_warp_enabled>`                       | ``false``            |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`domain_warp_fractal_gain<class_FastNoiseLite_property_domain_warp_fractal_gain>`             | ``0.5``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`domain_warp_fractal_lacunarity<class_FastNoiseLite_property_domain_warp_fractal_lacunarity>` | ``6.0``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                        | :ref:`domain_warp_fractal_octaves<class_FastNoiseLite_property_domain_warp_fractal_octaves>`       | ``5``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>`       | :ref:`domain_warp_fractal_type<class_FastNoiseLite_property_domain_warp_fractal_type>`             | ``1``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`domain_warp_frequency<class_FastNoiseLite_property_domain_warp_frequency>`                   | ``0.05``             |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>`                     | :ref:`domain_warp_type<class_FastNoiseLite_property_domain_warp_type>`                             | ``0``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`fractal_gain<class_FastNoiseLite_property_fractal_gain>`                                     | ``0.5``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`fractal_lacunarity<class_FastNoiseLite_property_fractal_lacunarity>`                         | ``2.0``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                        | :ref:`fractal_octaves<class_FastNoiseLite_property_fractal_octaves>`                               | ``5``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`fractal_ping_pong_strength<class_FastNoiseLite_property_fractal_ping_pong_strength>`         | ``2.0``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`FractalType<enum_FastNoiseLite_FractalType>`                           | :ref:`fractal_type<class_FastNoiseLite_property_fractal_type>`                                     | ``1``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`fractal_weighted_strength<class_FastNoiseLite_property_fractal_weighted_strength>`           | ``0.0``              |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                                    | :ref:`frequency<class_FastNoiseLite_property_frequency>`                                           | ``0.01``             |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`NoiseType<enum_FastNoiseLite_NoiseType>`                               | :ref:`noise_type<class_FastNoiseLite_property_noise_type>`                                         | ``1``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                                | :ref:`offset<class_FastNoiseLite_property_offset>`                                                 | ``Vector3(0, 0, 0)`` |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                        | :ref:`seed<class_FastNoiseLite_property_seed>`                                                     | ``0``                |
   +------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_FastNoiseLite_NoiseType:

.. rst-class:: classref-enumeration

enum **NoiseType**: :ref:`🔗<enum_FastNoiseLite_NoiseType>`

.. _class_FastNoiseLite_constant_TYPE_VALUE:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_VALUE** = ``5``

Một mạng lưới các điểm được gán các giá trị ngẫu nhiên, sau đó được nội suy dựa trên các giá trị lân cận.

.. _class_FastNoiseLite_constant_TYPE_VALUE_CUBIC:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_VALUE_CUBIC** = ``4``

Tương tự value noise (:ref:`TYPE_VALUE<class_FastNoiseLite_constant_TYPE_VALUE>`), nhưng chậm hơn. Có độ biến thiên lớn hơn ở các đỉnh và thung lũng.

Cubic noise có thể được dùng để tránh một số artifact khi sử dụng value noise để tạo bumpmap. Nhìn chung, bạn luôn nên sử dụng mode này nếu value noise được dùng cho heightmap hoặc bumpmap.

.. _class_FastNoiseLite_constant_TYPE_PERLIN:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_PERLIN** = ``3``

Một mạng lưới các gradient ngẫu nhiên. Tích vô hướng của chúng được nội suy để thu được các giá trị nằm giữa các mạng lưới.

.. _class_FastNoiseLite_constant_TYPE_CELLULAR:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_CELLULAR** = ``2``

Cellular bao gồm cả Worley noise và biểu đồ Voronoi, tạo ra nhiều vùng có cùng một giá trị.

.. _class_FastNoiseLite_constant_TYPE_SIMPLEX:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_SIMPLEX** = ``0``

Không giống :ref:`TYPE_PERLIN<class_FastNoiseLite_constant_TYPE_PERLIN>`, các gradient tồn tại trong mạng lưới simplex thay vì mạng lưới dạng lưới, giúp tránh các artifact định hướng. Bên trong sử dụng loại noise OpenSimplex2 của FastNoiseLite.

.. _class_FastNoiseLite_constant_TYPE_SIMPLEX_SMOOTH:

.. rst-class:: classref-enumeration-constant

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **TYPE_SIMPLEX_SMOOTH** = ``1``

Phiên bản được cải tiến, có chất lượng cao hơn của :ref:`TYPE_SIMPLEX<class_FastNoiseLite_constant_TYPE_SIMPLEX>`, nhưng chậm hơn. Bên trong sử dụng loại noise OpenSimplex2S của FastNoiseLite.

.. rst-class:: classref-item-separator

----

.. _enum_FastNoiseLite_FractalType:

.. rst-class:: classref-enumeration

enum **FractalType**: :ref:`🔗<enum_FastNoiseLite_FractalType>`

.. _class_FastNoiseLite_constant_FRACTAL_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`FractalType<enum_FastNoiseLite_FractalType>` **FRACTAL_NONE** = ``0``

Không có fractal noise.

.. _class_FastNoiseLite_constant_FRACTAL_FBM:

.. rst-class:: classref-enumeration-constant

:ref:`FractalType<enum_FastNoiseLite_FractalType>` **FRACTAL_FBM** = ``1``

Phương pháp sử dụng Fractional Brownian Motion để kết hợp các octave thành một fractal.

.. _class_FastNoiseLite_constant_FRACTAL_RIDGED:

.. rst-class:: classref-enumeration-constant

:ref:`FractalType<enum_FastNoiseLite_FractalType>` **FRACTAL_RIDGED** = ``2``

Phương pháp kết hợp các octave thành một fractal, tạo ra diện mạo "gồ ghề".

.. _class_FastNoiseLite_constant_FRACTAL_PING_PONG:

.. rst-class:: classref-enumeration-constant

:ref:`FractalType<enum_FastNoiseLite_FractalType>` **FRACTAL_PING_PONG** = ``3``

Phương pháp kết hợp các octave thành một fractal với hiệu ứng ping pong.

.. rst-class:: classref-item-separator

----

.. _enum_FastNoiseLite_CellularDistanceFunction:

.. rst-class:: classref-enumeration

enum **CellularDistanceFunction**: :ref:`🔗<enum_FastNoiseLite_CellularDistanceFunction>`

.. _class_FastNoiseLite_constant_DISTANCE_EUCLIDEAN:

.. rst-class:: classref-enumeration-constant

:ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **DISTANCE_EUCLIDEAN** = ``0``

Khoảng cách Euclidean đến điểm gần nhất.

.. _class_FastNoiseLite_constant_DISTANCE_EUCLIDEAN_SQUARED:

.. rst-class:: classref-enumeration-constant

:ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **DISTANCE_EUCLIDEAN_SQUARED** = ``1``

Bình phương khoảng cách Euclidean đến điểm gần nhất.

.. _class_FastNoiseLite_constant_DISTANCE_MANHATTAN:

.. rst-class:: classref-enumeration-constant

:ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **DISTANCE_MANHATTAN** = ``2``

Khoảng cách Manhattan (metric taxi) đến điểm gần nhất.

.. _class_FastNoiseLite_constant_DISTANCE_HYBRID:

.. rst-class:: classref-enumeration-constant

:ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **DISTANCE_HYBRID** = ``3``

Sự pha trộn giữa :ref:`DISTANCE_EUCLIDEAN<class_FastNoiseLite_constant_DISTANCE_EUCLIDEAN>` và :ref:`DISTANCE_MANHATTAN<class_FastNoiseLite_constant_DISTANCE_MANHATTAN>` để tạo ra các ranh giới ô cong.

.. rst-class:: classref-item-separator

----

.. _enum_FastNoiseLite_CellularReturnType:

.. rst-class:: classref-enumeration

enum **CellularReturnType**: :ref:`🔗<enum_FastNoiseLite_CellularReturnType>`

.. _class_FastNoiseLite_constant_RETURN_CELL_VALUE:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_CELL_VALUE** = ``0``

Hàm khoảng cách cellular sẽ trả về cùng một giá trị cho mọi điểm nằm trong một ô.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE** = ``1``

Hàm khoảng cách cellular sẽ trả về một giá trị được xác định bởi khoảng cách đến điểm gần nhất.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE2:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE2** = ``2``

Hàm khoảng cách cellular trả về khoảng cách đến điểm gần thứ hai.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE2_ADD:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE2_ADD** = ``3``

Khoảng cách đến điểm gần nhất được cộng vào khoảng cách đến điểm gần thứ hai.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE2_SUB:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE2_SUB** = ``4``

Khoảng cách đến điểm gần nhất được trừ khỏi khoảng cách đến điểm gần thứ hai.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE2_MUL:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE2_MUL** = ``5``

Khoảng cách đến điểm gần nhất được nhân với khoảng cách đến điểm gần thứ hai.

.. _class_FastNoiseLite_constant_RETURN_DISTANCE2_DIV:

.. rst-class:: classref-enumeration-constant

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **RETURN_DISTANCE2_DIV** = ``6``

Khoảng cách đến điểm gần nhất được chia cho khoảng cách đến điểm gần thứ hai.

.. rst-class:: classref-item-separator

----

.. _enum_FastNoiseLite_DomainWarpType:

.. rst-class:: classref-enumeration

enum **DomainWarpType**: :ref:`🔗<enum_FastNoiseLite_DomainWarpType>`

.. _class_FastNoiseLite_constant_DOMAIN_WARP_SIMPLEX:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>` **DOMAIN_WARP_SIMPLEX** = ``0``

Domain được warp bằng thuật toán simplex noise.

.. _class_FastNoiseLite_constant_DOMAIN_WARP_SIMPLEX_REDUCED:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>` **DOMAIN_WARP_SIMPLEX_REDUCED** = ``1``

Domain được warp bằng một phiên bản đơn giản hóa của thuật toán simplex noise.

.. _class_FastNoiseLite_constant_DOMAIN_WARP_BASIC_GRID:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>` **DOMAIN_WARP_BASIC_GRID** = ``2``

Domain được warp bằng một lưới noise đơn giản (không mượt bằng các phương thức khác nhưng có hiệu năng tốt hơn).

.. rst-class:: classref-item-separator

----

.. _enum_FastNoiseLite_DomainWarpFractalType:

.. rst-class:: classref-enumeration

enum **DomainWarpFractalType**: :ref:`🔗<enum_FastNoiseLite_DomainWarpFractalType>`

.. _class_FastNoiseLite_constant_DOMAIN_WARP_FRACTAL_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>` **DOMAIN_WARP_FRACTAL_NONE** = ``0``

Không có fractal noise để warp không gian.

.. _class_FastNoiseLite_constant_DOMAIN_WARP_FRACTAL_PROGRESSIVE:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>` **DOMAIN_WARP_FRACTAL_PROGRESSIVE** = ``1``

Warp không gian một cách tuần tự, octave này đến octave khác, tạo ra biến dạng "hóa lỏng" hơn.

.. _class_FastNoiseLite_constant_DOMAIN_WARP_FRACTAL_INDEPENDENT:

.. rst-class:: classref-enumeration-constant

:ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>` **DOMAIN_WARP_FRACTAL_INDEPENDENT** = ``2``

Warp không gian độc lập cho từng octave, tạo ra biến dạng hỗn loạn hơn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FastNoiseLite_property_cellular_distance_function:

.. rst-class:: classref-property

:ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **cellular_distance_function** = ``0`` :ref:`🔗<class_FastNoiseLite_property_cellular_distance_function>`

.. rst-class:: classref-property-setget

- |void| **set_cellular_distance_function**\ (\ value\: :ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>`\ ) - :ref:`CellularDistanceFunction<enum_FastNoiseLite_CellularDistanceFunction>` **get_cellular_distance_function**\ (\ )

Xác định cách tính khoảng cách đến điểm gần nhất/gần thứ hai.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_cellular_jitter:

.. rst-class:: classref-property

:ref:`float<class_float>` **cellular_jitter** = ``1.0`` :ref:`🔗<class_FastNoiseLite_property_cellular_jitter>`

.. rst-class:: classref-property-setget

- |void| **set_cellular_jitter**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cellular_jitter**\ (\ )

Khoảng cách tối đa mà một điểm có thể lệch khỏi vị trí trên lưới của nó. Đặt thành ``0`` để có một lưới đồng đều.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_cellular_return_type:

.. rst-class:: classref-property

:ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **cellular_return_type** = ``1`` :ref:`🔗<class_FastNoiseLite_property_cellular_return_type>`

.. rst-class:: classref-property-setget

- |void| **set_cellular_return_type**\ (\ value\: :ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>`\ ) - :ref:`CellularReturnType<enum_FastNoiseLite_CellularReturnType>` **get_cellular_return_type**\ (\ )

Kiểu giá trị trả về từ các phép tính cellular noise.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_amplitude:

.. rst-class:: classref-property

:ref:`float<class_float>` **domain_warp_amplitude** = ``30.0`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_amplitude>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_amplitude**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_domain_warp_amplitude**\ (\ )

Đặt khoảng cách warp tối đa tính từ gốc tọa độ.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **domain_warp_enabled** = ``false`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_domain_warp_enabled**\ (\ )

Nếu được bật, một instance FastNoiseLite khác sẽ được dùng để warp không gian, tạo ra biến dạng của noise.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_fractal_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **domain_warp_fractal_gain** = ``0.5`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_fractal_gain>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_fractal_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_domain_warp_fractal_gain**\ (\ )

Xác định cường độ của mỗi lớp noise tiếp theo được dùng để warp không gian.

Giá trị thấp nhấn mạnh hơn vào các lớp cơ sở có tần số thấp, trong khi giá trị cao nhấn mạnh hơn vào các lớp có tần số cao.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_fractal_lacunarity:

.. rst-class:: classref-property

:ref:`float<class_float>` **domain_warp_fractal_lacunarity** = ``6.0`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_fractal_lacunarity>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_fractal_lacunarity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_domain_warp_fractal_lacunarity**\ (\ )

Sự thay đổi tần số giữa các octave, còn được gọi là "lacunarity", của fractal noise dùng để warp không gian. Tăng giá trị này sẽ tạo ra các octave cao hơn, tạo noise có chi tiết mịn hơn và diện mạo gồ ghề hơn.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_fractal_octaves:

.. rst-class:: classref-property

:ref:`int<class_int>` **domain_warp_fractal_octaves** = ``5`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_fractal_octaves>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_fractal_octaves**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_domain_warp_fractal_octaves**\ (\ )

Số lớp noise được lấy mẫu để nhận giá trị cuối cùng cho fractal noise dùng để warp không gian.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_fractal_type:

.. rst-class:: classref-property

:ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>` **domain_warp_fractal_type** = ``1`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_fractal_type>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_fractal_type**\ (\ value\: :ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>`\ ) - :ref:`DomainWarpFractalType<enum_FastNoiseLite_DomainWarpFractalType>` **get_domain_warp_fractal_type**\ (\ )

Phương thức kết hợp các octave thành một fractal được dùng để biến dạng không gian.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_frequency:

.. rst-class:: classref-property

:ref:`float<class_float>` **domain_warp_frequency** = ``0.05`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_frequency>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_frequency**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_domain_warp_frequency**\ (\ )

Tần số của noise dùng để biến dạng không gian. Tần số thấp tạo ra noise mượt, trong khi tần số cao tạo ra noise thô hơn, có dạng hạt rõ hơn.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_domain_warp_type:

.. rst-class:: classref-property

:ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>` **domain_warp_type** = ``0`` :ref:`🔗<class_FastNoiseLite_property_domain_warp_type>`

.. rst-class:: classref-property-setget

- |void| **set_domain_warp_type**\ (\ value\: :ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>`\ ) - :ref:`DomainWarpType<enum_FastNoiseLite_DomainWarpType>` **get_domain_warp_type**\ (\ )

Thuật toán biến dạng.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **fractal_gain** = ``0.5`` :ref:`🔗<class_FastNoiseLite_property_fractal_gain>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fractal_gain**\ (\ )

Xác định cường độ của mỗi lớp noise tiếp theo trong fractal noise.

Giá trị thấp nhấn mạnh hơn vào các lớp cơ sở có tần số thấp, trong khi giá trị cao nhấn mạnh hơn vào các lớp có tần số cao.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_lacunarity:

.. rst-class:: classref-property

:ref:`float<class_float>` **fractal_lacunarity** = ``2.0`` :ref:`🔗<class_FastNoiseLite_property_fractal_lacunarity>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_lacunarity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fractal_lacunarity**\ (\ )

Hệ số nhân tần số giữa các octave liên tiếp. Việc tăng giá trị này khiến các octave cao hơn tạo ra noise có chi tiết mịn hơn và vẻ ngoài thô hơn.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_octaves:

.. rst-class:: classref-property

:ref:`int<class_int>` **fractal_octaves** = ``5`` :ref:`🔗<class_FastNoiseLite_property_fractal_octaves>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_octaves**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fractal_octaves**\ (\ )

Số lớp noise được lấy mẫu để nhận giá trị cuối cùng cho các loại fractal noise.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_ping_pong_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **fractal_ping_pong_strength** = ``2.0`` :ref:`🔗<class_FastNoiseLite_property_fractal_ping_pong_strength>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_ping_pong_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fractal_ping_pong_strength**\ (\ )

Thiết lập cường độ của loại fractal ping pong.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_type:

.. rst-class:: classref-property

:ref:`FractalType<enum_FastNoiseLite_FractalType>` **fractal_type** = ``1`` :ref:`🔗<class_FastNoiseLite_property_fractal_type>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_type**\ (\ value\: :ref:`FractalType<enum_FastNoiseLite_FractalType>`\ ) - :ref:`FractalType<enum_FastNoiseLite_FractalType>` **get_fractal_type**\ (\ )

Phương thức kết hợp các octave thành một fractal.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_fractal_weighted_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **fractal_weighted_strength** = ``0.0`` :ref:`🔗<class_FastNoiseLite_property_fractal_weighted_strength>`

.. rst-class:: classref-property-setget

- |void| **set_fractal_weighted_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fractal_weighted_strength**\ (\ )

Trọng số càng cao thì các octave cao hơn càng ít ảnh hưởng nếu các octave thấp hơn có ảnh hưởng lớn.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_frequency:

.. rst-class:: classref-property

:ref:`float<class_float>` **frequency** = ``0.01`` :ref:`🔗<class_FastNoiseLite_property_frequency>`

.. rst-class:: classref-property-setget

- |void| **set_frequency**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_frequency**\ (\ )

Tần số cho tất cả các loại noise. Tần số thấp tạo ra noise mượt, trong khi tần số cao tạo ra noise thô hơn, có dạng hạt rõ hơn.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_noise_type:

.. rst-class:: classref-property

:ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **noise_type** = ``1`` :ref:`🔗<class_FastNoiseLite_property_noise_type>`

.. rst-class:: classref-property-setget

- |void| **set_noise_type**\ (\ value\: :ref:`NoiseType<enum_FastNoiseLite_NoiseType>`\ ) - :ref:`NoiseType<enum_FastNoiseLite_NoiseType>` **get_noise_type**\ (\ )

Thuật toán noise được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_offset:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **offset** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_FastNoiseLite_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_offset**\ (\ )

Dịch chuyển các tọa độ đầu vào của noise theo :ref:`Vector3<class_Vector3>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_FastNoiseLite_property_seed:

.. rst-class:: classref-property

:ref:`int<class_int>` **seed** = ``0`` :ref:`🔗<class_FastNoiseLite_property_seed>`

.. rst-class:: classref-property-setget

- |void| **set_seed**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_seed**\ (\ )

Seed số ngẫu nhiên cho tất cả các loại noise.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
