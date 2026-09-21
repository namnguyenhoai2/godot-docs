:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedVector2Array.xml.

.. _class_PackedVector2Array:

PackedVector2Array
==================

Một mảng đóng gói các :ref:`Vector2<class_Vector2>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế chuyên biệt để chứa :ref:`Vector2<class_Vector2>`. Dữ liệu được đóng gói chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

\ **Sự khác biệt giữa mảng đóng gói, mảng định kiểu và mảng không định kiểu:** Mảng đóng gói thường nhanh hơn khi lặp qua và sửa đổi so với mảng định kiểu cùng loại (ví dụ: **PackedVector2Array** so với ``Array[Vector2]``). Ngoài ra, mảng đóng gói tiêu tốn ít bộ nhớ hơn. Nhược điểm là mảng đóng gói kém linh hoạt hơn vì không cung cấp nhiều phương thức tiện ích như :ref:`Array.map()<class_Array_method_map>`. Ngược lại, mảng định kiểu nhanh hơn mảng không định kiểu khi lặp qua và sửa đổi.

\ **Lưu ý:** Mảng đóng gói luôn được truyền theo tham chiếu. Để lấy một bản sao của mảng có thể được sửa đổi độc lập với mảng ban đầu, hãy sử dụng :ref:`duplicate()<class_PackedVector2Array_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức dựng sẵn. Trong các trường hợp này, mảng đóng gói được trả về là một bản sao và việc thay đổi nó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật một thuộc tính dựng sẵn thuộc loại này, hãy sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, một mảng đóng gói sẽ được đánh giá là ``false`` nếu nó trống. Nếu không, một mảng đóng gói sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `Grid-based Navigation with AStarGrid2D Demo <https://godotengine.org/asset-library/asset/2723>`__

.. rst-class:: classref-reftable-group

Hàm khởi tạo
------------

.. table::
   :widths: auto

   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`PackedVector2Array<class_PackedVector2Array_constructor_PackedVector2Array>`\ (\ )                                                             |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`PackedVector2Array<class_PackedVector2Array_constructor_PackedVector2Array>`\ (\ from\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`PackedVector2Array<class_PackedVector2Array_constructor_PackedVector2Array>`\ (\ from\: :ref:`Array<class_Array>`\ )                           |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`append<class_PackedVector2Array_method_append>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ )                                                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`append_array<class_PackedVector2Array_method_append_array>`\ (\ array\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`bsearch<class_PackedVector2Array_method_bsearch>`\ (\ value\: :ref:`Vector2<class_Vector2>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_PackedVector2Array_method_clear>`\ (\ )                                                                                             |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`count<class_PackedVector2Array_method_count>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) |const|                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`duplicate<class_PackedVector2Array_method_duplicate>`\ (\ ) |const|                                                                             |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`erase<class_PackedVector2Array_method_erase>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ )                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`fill<class_PackedVector2Array_method_fill>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ )                                                        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`find<class_PackedVector2Array_method_find>`\ (\ value\: :ref:`Vector2<class_Vector2>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`get<class_PackedVector2Array_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                          |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`has<class_PackedVector2Array_method_has>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`insert<class_PackedVector2Array_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Vector2<class_Vector2>`\ )                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_empty<class_PackedVector2Array_method_is_empty>`\ (\ ) |const|                                                                               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`push_back<class_PackedVector2Array_method_push_back>`\ (\ value\: :ref:`Vector2<class_Vector2>`\ )                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_at<class_PackedVector2Array_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`resize<class_PackedVector2Array_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                         |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`reverse<class_PackedVector2Array_method_reverse>`\ (\ )                                                                                         |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`rfind<class_PackedVector2Array_method_rfind>`\ (\ value\: :ref:`Vector2<class_Vector2>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set<class_PackedVector2Array_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Vector2<class_Vector2>`\ )                           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`size<class_PackedVector2Array_method_size>`\ (\ ) |const|                                                                                       |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`slice<class_PackedVector2Array_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`sort<class_PackedVector2Array_method_sort>`\ (\ )                                                                                               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`       | :ref:`to_byte_array<class_PackedVector2Array_method_to_byte_array>`\ (\ ) |const|                                                                     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator !=<class_PackedVector2Array_operator_neq_PackedVector2Array>`\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`operator *<class_PackedVector2Array_operator_mul_Transform2D>`\ (\ right\: :ref:`Transform2D<class_Transform2D>`\ )                       |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`operator +<class_PackedVector2Array_operator_sum_PackedVector2Array>`\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator ==<class_PackedVector2Array_operator_eq_PackedVector2Array>`\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`operator []<class_PackedVector2Array_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_PackedVector2Array_constructor_PackedVector2Array:

.. rst-class:: classref-constructor

:ref:`PackedVector2Array<class_PackedVector2Array>` **PackedVector2Array**\ (\ ) :ref:`🔗<class_PackedVector2Array_constructor_PackedVector2Array>`

Tạo một **PackedVector2Array** trống.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedVector2Array<class_PackedVector2Array>` **PackedVector2Array**\ (\ from\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )

Tạo một **PackedVector2Array** dưới dạng bản sao của **PackedVector2Array** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedVector2Array<class_PackedVector2Array>` **PackedVector2Array**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedVector2Array** mới. Bạn có thể tùy chọn truyền vào một :ref:`Array<class_Array>` chung để chuyển đổi.

\ **Lưu ý:** Khi khởi tạo **PackedVector2Array** với các phần tử, phải khởi tạo nó bằng một :ref:`Array<class_Array>` gồm các giá trị :ref:`Vector2<class_Vector2>`:

::

    var array = PackedVector2Array([Vector2(12, 34), Vector2(56, 78)])

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedVector2Array_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedVector2Array_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_PackedVector2Array_method_append_array>`

Thêm một **PackedVector2Array** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`Vector2<class_Vector2>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedVector2Array_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn để duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng tìm kiếm nhị phân. Có thể tùy chọn truyền vào một bộ chỉ định ``before``. Nếu ``false``, chỉ mục được trả về sẽ nằm sau tất cả các mục hiện có cùng giá trị trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedVector2Array_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedVector2Array_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedVector2Array_method_resize>` với kích thước ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_PackedVector2Array_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedVector2Array_method_duplicate>`

Tạo và trả về một bản sao của mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có gì xảy ra và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_PackedVector2Array_method_remove_at>`.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_fill>`

Gán giá trị đã cho cho tất cả phần tử trong mảng. Thường có thể sử dụng cùng với :ref:`resize()<class_PackedVector2Array_method_resize>` để tạo một mảng có kích thước nhất định và các phần tử đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`Vector2<class_Vector2>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedVector2Array_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của giá trị đó, hoặc ``-1`` nếu không tìm thấy. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_get:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedVector2Array_method_get>`

Trả về :ref:`Vector2<class_Vector2>` tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``Vector2(0, 0)``.

Phương thức này tương tự (nhưng không giống hệt) toán tử ``[]``. Đáng chú ý nhất, khi phương thức này thất bại, nó không tạm dừng quá trình thực thi dự án nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_PackedVector2Array_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_insert>`

Chèn một phần tử mới vào vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedVector2Array_method_is_empty>`

Trả về ``true`` nếu mảng trống.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_push_back>`

Chèn một :ref:`Vector2<class_Vector2>` vào cuối.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector2Array_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector2Array_method_resize>`

Đặt kích thước của mảng. Nếu mảng được mở rộng, các phần tử được dành chỗ ở cuối mảng. Nếu mảng bị thu nhỏ, mảng sẽ được cắt ngắn về kích thước mới. Gọi :ref:`resize()<class_PackedVector2Array_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn việc thêm từng phần tử mới.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Sử dụng :ref:`size()<class_PackedVector2Array_method_size>` để tìm kích thước thực tế của mảng sau khi thay đổi kích thước.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedVector2Array_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`Vector2<class_Vector2>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedVector2Array_method_rfind>`

Tìm kiếm mảng theo thứ tự ngược. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm. Nếu là số âm, chỉ mục bắt đầu được tính tương đối từ cuối mảng.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_PackedVector2Array_method_set>`

Thay đổi :ref:`Vector2<class_Vector2>` tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedVector2Array_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_slice:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedVector2Array_method_slice>`

Trả về phần lát (slice) của **PackedVector2Array**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedVector2Array** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước của mảng, vì vậy giá trị mặc định của ``end`` khiến thao tác lát mặc định kéo dài đến kích thước của mảng (tức là ``arr.slice(1)`` là cách viết rút gọn của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết rút gọn của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedVector2Array_method_sort>`

Sắp xếp các phần tử của mảng theo thứ tự tăng dần.

\ **Lưu ý:** Các vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống như những vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedVector2Array_method_to_byte_array>`

Trả về một :ref:`PackedByteArray<class_PackedByteArray>`, trong đó mỗi vector được mã hóa thành các byte.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_PackedVector2Array_operator_neq_PackedVector2Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_PackedVector2Array_operator_neq_PackedVector2Array>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_operator_mul_Transform2D:

.. rst-class:: classref-operator

:ref:`PackedVector2Array<class_PackedVector2Array>` **operator ***\ (\ right\: :ref:`Transform2D<class_Transform2D>`\ ) :ref:`🔗<class_PackedVector2Array_operator_mul_Transform2D>`

Trả về một **PackedVector2Array** mới, trong đó tất cả vector trong mảng này được biến đổi ngược (nhân) bởi ma trận biến đổi :ref:`Transform2D<class_Transform2D>` đã cho, với giả định rằng basis của phép biến đổi là trực chuẩn (tức là phép xoay/phản chiếu được chấp nhận, còn phép scale/skew thì không).

\ ``array * transform`` tương đương với ``transform.inverse() * array``. Xem :ref:`Transform2D.inverse()<class_Transform2D_method_inverse>`.

Để biến đổi bằng phép nghịch đảo của một phép biến đổi affine (ví dụ như có scaling), có thể sử dụng ``transform.affine_inverse() * array`` thay thế. Xem :ref:`Transform2D.affine_inverse()<class_Transform2D_method_affine_inverse>`.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_operator_sum_PackedVector2Array:

.. rst-class:: classref-operator

:ref:`PackedVector2Array<class_PackedVector2Array>` **operator +**\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_PackedVector2Array_operator_sum_PackedVector2Array>`

Trả về một **PackedVector2Array** mới, với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu năng tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedVector2Array_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_operator_eq_PackedVector2Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_PackedVector2Array_operator_eq_PackedVector2Array>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có tất cả :ref:`Vector2<class_Vector2>`\ s bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector2Array_operator_idx_int:

.. rst-class:: classref-operator

:ref:`Vector2<class_Vector2>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector2Array_operator_idx_int>`

Trả về :ref:`Vector2<class_Vector2>` tại chỉ mục ``index``. Có thể sử dụng chỉ mục âm để truy cập các phần tử bắt đầu từ cuối. Việc sử dụng chỉ mục nằm ngoài giới hạn của mảng sẽ gây ra lỗi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
