:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Curve2D.xml.

.. _class_Curve2D:

Curve2D
=======

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mô tả một đường cong Bézier trong không gian 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này mô tả một đường cong Bézier trong không gian 2D. Nó chủ yếu được dùng để tạo hình dạng cho một :ref:`Path2D<class_Path2D>`, nhưng cũng có thể được lấy mẫu thủ công cho các mục đích khác.

Lớp này lưu một cache gồm các điểm được tính toán trước dọc theo đường cong để tăng tốc các phép tính tiếp theo.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`bake_interval<class_Curve2D_property_bake_interval>`                   | ``5.0``           |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`point_count<class_Curve2D_property_point_count>`                       | ``0``             |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`point_{index}/in<class_Curve2D_property_point_{index}/in>`             | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`point_{index}/out<class_Curve2D_property_point_{index}/out>`           | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`point_{index}/position<class_Curve2D_property_point_{index}/position>` | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_point<class_Curve2D_method_add_point>`\ (\ position\: :ref:`Vector2<class_Vector2>`, in\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0), out\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0), index\: :ref:`int<class_int>` = -1\ ) |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_points<class_Curve2D_method_clear_points>`\ (\ )                                                                                                                                                                                  |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_baked_length<class_Curve2D_method_get_baked_length>`\ (\ ) |const|                                                                                                                                                                  |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`get_baked_points<class_Curve2D_method_get_baked_points>`\ (\ ) |const|                                                                                                                                                                  |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_closest_offset<class_Curve2D_method_get_closest_offset>`\ (\ to_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                                                                    |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`get_closest_point<class_Curve2D_method_get_closest_point>`\ (\ to_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                                                                      |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`get_point_in<class_Curve2D_method_get_point_in>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                             |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`get_point_out<class_Curve2D_method_get_point_out>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                           |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`get_point_position<class_Curve2D_method_get_point_position>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                 |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_point<class_Curve2D_method_remove_point>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                                                                                                     |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`sample<class_Curve2D_method_sample>`\ (\ idx\: :ref:`int<class_int>`, t\: :ref:`float<class_float>`\ ) |const|                                                                                                                          |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`sample_baked<class_Curve2D_method_sample_baked>`\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                       |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>`               | :ref:`sample_baked_with_rotation<class_Curve2D_method_sample_baked_with_rotation>`\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const|                                                           |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`samplef<class_Curve2D_method_samplef>`\ (\ fofs\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                  |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_in<class_Curve2D_method_set_point_in>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ )                                                                                                           |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_out<class_Curve2D_method_set_point_out>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ )                                                                                                         |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_position<class_Curve2D_method_set_point_position>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ )                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`tessellate<class_Curve2D_method_tessellate>`\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_degrees\: :ref:`float<class_float>` = 4\ ) |const|                                                                                   |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`tessellate_even_length<class_Curve2D_method_tessellate_even_length>`\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_length\: :ref:`float<class_float>` = 20.0\ ) |const|                                                         |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Curve2D_property_bake_interval:

.. rst-class:: classref-property

:ref:`float<class_float>` **bake_interval** = ``5.0`` :ref:`🔗<class_Curve2D_property_bake_interval>`

.. rst-class:: classref-property-setget

- |void| **set_bake_interval**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bake_interval**\ (\ )

Khoảng cách tính bằng pixel giữa hai điểm liền kề trong cache. Thay đổi giá trị này sẽ buộc cache được tính toán lại vào lần tiếp theo hàm :ref:`get_baked_points()<class_Curve2D_method_get_baked_points>` hoặc :ref:`get_baked_length()<class_Curve2D_method_get_baked_length>` được gọi. Khoảng cách càng nhỏ thì số điểm trong cache càng nhiều và càng tốn nhiều bộ nhớ, vì vậy hãy sử dụng cẩn thận.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_property_point_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **point_count** = ``0`` :ref:`🔗<class_Curve2D_property_point_count>`

.. rst-class:: classref-property-setget

- |void| **set_point_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_point_count**\ (\ )

Số lượng điểm mô tả đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_property_point_{index}/in:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **point_{index}/in** = ``Vector2(0, 0)`` :ref:`🔗<class_Curve2D_property_point_{index}/in>`

Vị trí của control point dẫn đến đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_property_point_{index}/out:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **point_{index}/out** = ``Vector2(0, 0)`` :ref:`🔗<class_Curve2D_property_point_{index}/out>`

Vị trí của control point đi ra từ đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_property_point_{index}/position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **point_{index}/position** = ``Vector2(0, 0)`` :ref:`🔗<class_Curve2D_property_point_{index}/position>`

Vị trí của đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Curve2D_method_add_point:

.. rst-class:: classref-method

|void| **add_point**\ (\ position\: :ref:`Vector2<class_Vector2>`, in\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0), out\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0), index\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_Curve2D_method_add_point>`

Thêm một điểm với ``position`` được chỉ định, tương đối so với vị trí riêng của đường cong, cùng các control point ``in`` và ``out``. Nối điểm mới vào cuối danh sách điểm.

Nếu cung cấp ``index``, điểm mới được chèn trước điểm hiện có được xác định bằng index ``index``. Mọi điểm hiện có bắt đầu từ ``index`` sẽ được dịch xuống dưới trong danh sách điểm. Index phải lớn hơn hoặc bằng ``0`` và không được vượt quá số điểm hiện có trong đường. Xem :ref:`point_count<class_Curve2D_property_point_count>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_clear_points:

.. rst-class:: classref-method

|void| **clear_points**\ (\ ) :ref:`🔗<class_Curve2D_method_clear_points>`

Xóa tất cả các điểm khỏi đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_baked_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_baked_length**\ (\ ) |const| :ref:`🔗<class_Curve2D_method_get_baked_length>`

Trả về tổng độ dài của đường cong, dựa trên các điểm trong cache. Với mật độ đủ cao (xem :ref:`bake_interval<class_Curve2D_property_bake_interval>`), kết quả sẽ đủ gần đúng.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_baked_points:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_baked_points**\ (\ ) |const| :ref:`🔗<class_Curve2D_method_get_baked_points>`

Trả về cache các điểm dưới dạng :ref:`PackedVector2Array<class_PackedVector2Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_closest_offset:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_closest_offset**\ (\ to_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Curve2D_method_get_closest_offset>`

Trả về offset gần nhất với ``to_point``. Offset này được dùng trong :ref:`sample_baked()<class_Curve2D_method_sample_baked>`.

\ ``to_point`` phải nằm trong local space của đường cong này.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_closest_point:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_closest_point**\ (\ to_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Curve2D_method_get_closest_point>`

Trả về điểm gần nhất trên các đoạn đã bake (trong local space của đường cong) với ``to_point``.

\ ``to_point`` phải nằm trong local space của đường cong này.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_point_in:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_in**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve2D_method_get_point_in>`

Trả về vị trí của control point dẫn đến đỉnh ``idx``. Vị trí trả về là tương đối so với đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_point_out:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_out**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve2D_method_get_point_out>`

Trả về vị trí của control point đi ra từ đỉnh ``idx``. Vị trí trả về là tương đối so với đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_position**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve2D_method_get_point_position>`

Trả về vị trí của đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Curve2D_method_remove_point>`

Xóa điểm ``idx`` khỏi đường cong. Gửi lỗi đến console nếu ``idx`` nằm ngoài phạm vi.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_sample:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **sample**\ (\ idx\: :ref:`int<class_int>`, t\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve2D_method_sample>`

Trả về vị trí giữa đỉnh ``idx`` và đỉnh ``idx + 1``, trong đó ``t`` kiểm soát xem điểm là đỉnh đầu tiên (``t = 0.0``), đỉnh cuối cùng (``t = 1.0``) hay nằm ở giữa. Các giá trị của ``t`` nằm ngoài phạm vi (``0.0 <= t <= 1.0``) sẽ cho kết quả lạ nhưng có thể dự đoán được.

Nếu ``idx`` nằm ngoài phạm vi, nó sẽ được cắt về đỉnh đầu tiên hoặc cuối cùng, còn ``t`` sẽ bị bỏ qua. Nếu đường cong không có điểm, hàm sẽ gửi lỗi đến console và trả về ``(0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_sample_baked:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **sample_baked**\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Curve2D_method_sample_baked>`

Trả về một điểm trên đường cong tại vị trí ``offset``, trong đó ``offset`` được đo dưới dạng khoảng cách pixel dọc theo đường cong.

Để thực hiện việc này, hàm tìm hai điểm trong cache mà ``offset`` nằm giữa, sau đó nội suy các giá trị. Phép nội suy là cubic nếu ``cubic`` được đặt thành ``true``, hoặc linear nếu được đặt thành ``false``.

Nội suy cubic thường bám theo các đường cong tốt hơn, nhưng linear nhanh hơn (và thường đủ chính xác).

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_sample_baked_with_rotation:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **sample_baked_with_rotation**\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Curve2D_method_sample_baked_with_rotation>`

Tương tự :ref:`sample_baked()<class_Curve2D_method_sample_baked>`, nhưng trả về :ref:`Transform2D<class_Transform2D>` có thêm rotation dọc theo đường cong, với :ref:`Transform2D.origin<class_Transform2D_property_origin>` là vị trí điểm và vector :ref:`Transform2D.x<class_Transform2D_property_x>` chỉ theo hướng của path tại điểm đó. Trả về một transform rỗng nếu độ dài của đường cong là ``0``.

::

    var baked = curve.sample_baked_with_rotation(offset)
    # Transform2D trả về có thể được gán trực tiếp.
    transform = baked
    # Bạn cũng có thể đọc origin và rotation riêng biệt từ Transform2D trả về.
    position = baked.get_origin()
    rotation = baked.get_rotation()

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_samplef:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **samplef**\ (\ fofs\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve2D_method_samplef>`

Trả về vị trí tại đỉnh ``fofs``. Hàm gọi :ref:`sample()<class_Curve2D_method_sample>` bằng cách sử dụng phần nguyên của ``fofs`` làm ``idx`` và phần thập phân của nó làm ``t``.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_set_point_in:

.. rst-class:: classref-method

|void| **set_point_in**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Curve2D_method_set_point_in>`

Thiết lập vị trí của control point dẫn đến đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console. Vị trí này tương đối so với đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_set_point_out:

.. rst-class:: classref-method

|void| **set_point_out**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Curve2D_method_set_point_out>`

Thiết lập vị trí của control point đi ra từ đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console. Vị trí này tương đối so với đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_set_point_position:

.. rst-class:: classref-method

|void| **set_point_position**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Curve2D_method_set_point_position>`

Thiết lập vị trí cho đỉnh ``idx``. Nếu index nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_tessellate:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **tessellate**\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_degrees\: :ref:`float<class_float>` = 4\ ) |const| :ref:`🔗<class_Curve2D_method_tessellate>`

Trả về danh sách các điểm dọc theo đường cong, với mật độ điểm được điều khiển theo độ cong. Nghĩa là các phần cong hơn sẽ có nhiều điểm hơn các phần thẳng.

Phép gần đúng này tạo các đoạn thẳng giữa mỗi điểm, sau đó chia nhỏ các đoạn đó cho đến khi hình dạng tạo ra đủ tương đồng.

\ ``max_stages`` kiểm soát số lần chia nhỏ mà một đoạn cong có thể trải qua trước khi được xem là đủ gần đúng. Mỗi lần chia nhỏ sẽ tách đoạn làm đôi, vì vậy 5 stage mặc định có thể có tới 32 lần chia nhỏ trên mỗi đoạn cong. Hãy tăng giá trị này một cách cẩn thận!

\ ``tolerance_degrees`` kiểm soát số độ mà điểm giữa của một đoạn có thể lệch so với đường cong thực trước khi đoạn đó phải được chia nhỏ.

.. rst-class:: classref-item-separator

----

.. _class_Curve2D_method_tessellate_even_length:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **tessellate_even_length**\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_length\: :ref:`float<class_float>` = 20.0\ ) |const| :ref:`🔗<class_Curve2D_method_tessellate_even_length>`

Trả về danh sách các điểm dọc theo đường cong với mật độ gần như đồng đều. ``max_stages`` kiểm soát số lần chia nhỏ mà một đoạn cong có thể trải qua trước khi được xem là đủ gần đúng. Mỗi lần chia nhỏ sẽ tách đoạn làm đôi, vì vậy 5 stage mặc định có thể có tới 32 lần chia nhỏ trên mỗi đoạn cong. Hãy tăng giá trị này một cách cẩn thận!

\ ``tolerance_length`` kiểm soát khoảng cách tối đa giữa hai điểm lân cận trước khi đoạn đó phải được chia nhỏ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
