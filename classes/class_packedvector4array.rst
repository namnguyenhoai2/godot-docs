:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedVector4Array.xml.

.. _class_PackedVector4Array:

PackedVector4Array
==================

Một mảng packed gồm các :ref:`Vector4<class_Vector4>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế riêng để lưu trữ :ref:`Vector4<class_Vector4>`. Dữ liệu được pack chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

\ **Sự khác biệt giữa packed array, typed array và untyped array:** Packed array thường có tốc độ lặp và chỉnh sửa nhanh hơn typed array cùng kiểu (ví dụ: **PackedVector4Array** so với ``Array[Vector4]``). Ngoài ra, packed array sử dụng ít bộ nhớ hơn. Điểm hạn chế là packed array kém linh hoạt hơn vì không cung cấp nhiều phương thức tiện lợi như :ref:`Array.map()<class_Array_method_map>`. Typed array lại có tốc độ lặp và chỉnh sửa nhanh hơn untyped array.

\ **Lưu ý:** Packed array luôn được truyền bằng tham chiếu. Để lấy một bản sao của mảng có thể được chỉnh sửa độc lập với mảng ban đầu, hãy dùng :ref:`duplicate()<class_PackedVector4Array_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức built-in. Trong những trường hợp này, packed array được trả về là một bản sao và việc thay đổi nó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật một thuộc tính built-in thuộc kiểu này, hãy chỉnh sửa mảng được trả về rồi gán lại mảng đó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, packed array sẽ được đánh giá là ``false`` nếu rỗng. Nếu không, packed array luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`PackedVector4Array<class_PackedVector4Array_constructor_PackedVector4Array>`\ (\ )                                                             |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`PackedVector4Array<class_PackedVector4Array_constructor_PackedVector4Array>`\ (\ from\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`PackedVector4Array<class_PackedVector4Array_constructor_PackedVector4Array>`\ (\ from\: :ref:`Array<class_Array>`\ )                           |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`append<class_PackedVector4Array_method_append>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ )                                                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`append_array<class_PackedVector4Array_method_append_array>`\ (\ array\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`bsearch<class_PackedVector4Array_method_bsearch>`\ (\ value\: :ref:`Vector4<class_Vector4>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_PackedVector4Array_method_clear>`\ (\ )                                                                                             |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`count<class_PackedVector4Array_method_count>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) |const|                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`duplicate<class_PackedVector4Array_method_duplicate>`\ (\ ) |const|                                                                             |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`erase<class_PackedVector4Array_method_erase>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ )                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`fill<class_PackedVector4Array_method_fill>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ )                                                        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`find<class_PackedVector4Array_method_find>`\ (\ value\: :ref:`Vector4<class_Vector4>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4<class_Vector4>`                       | :ref:`get<class_PackedVector4Array_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                          |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`has<class_PackedVector4Array_method_has>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) |const|                                                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`insert<class_PackedVector4Array_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Vector4<class_Vector4>`\ )                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_empty<class_PackedVector4Array_method_is_empty>`\ (\ ) |const|                                                                               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`push_back<class_PackedVector4Array_method_push_back>`\ (\ value\: :ref:`Vector4<class_Vector4>`\ )                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_at<class_PackedVector4Array_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`resize<class_PackedVector4Array_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                         |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`reverse<class_PackedVector4Array_method_reverse>`\ (\ )                                                                                         |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`rfind<class_PackedVector4Array_method_rfind>`\ (\ value\: :ref:`Vector4<class_Vector4>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set<class_PackedVector4Array_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Vector4<class_Vector4>`\ )                           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`size<class_PackedVector4Array_method_size>`\ (\ ) |const|                                                                                       |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`slice<class_PackedVector4Array_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`sort<class_PackedVector4Array_method_sort>`\ (\ )                                                                                               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`       | :ref:`to_byte_array<class_PackedVector4Array_method_to_byte_array>`\ (\ ) |const|                                                                     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator !=<class_PackedVector4Array_operator_neq_PackedVector4Array>`\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector4Array<class_PackedVector4Array>` | :ref:`operator +<class_PackedVector4Array_operator_sum_PackedVector4Array>`\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator ==<class_PackedVector4Array_operator_eq_PackedVector4Array>`\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4<class_Vector4>`                       | :ref:`operator []<class_PackedVector4Array_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_PackedVector4Array_constructor_PackedVector4Array:

.. rst-class:: classref-constructor

:ref:`PackedVector4Array<class_PackedVector4Array>` **PackedVector4Array**\ (\ ) :ref:`🔗<class_PackedVector4Array_constructor_PackedVector4Array>`

Tạo một **PackedVector4Array** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedVector4Array<class_PackedVector4Array>` **PackedVector4Array**\ (\ from\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )

Tạo một **PackedVector4Array** dưới dạng bản sao của **PackedVector4Array** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedVector4Array<class_PackedVector4Array>` **PackedVector4Array**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedVector4Array** mới. Bạn có thể tùy chọn truyền vào một :ref:`Array<class_Array>` generic để được chuyển đổi.

\ **Lưu ý:** Khi khởi tạo **PackedVector4Array** với các phần tử, mảng phải được khởi tạo bằng một :ref:`Array<class_Array>` gồm các giá trị :ref:`Vector4<class_Vector4>`:

::

    var array = PackedVector4Array([Vector4(12, 34, 56, 78), Vector4(90, 12, 34, 56)])

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedVector4Array_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedVector4Array_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) :ref:`🔗<class_PackedVector4Array_method_append_array>`

Thêm một **PackedVector4Array** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`Vector4<class_Vector4>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedVector4Array_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn để duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng binary search. Có thể tùy chọn truyền vào một specifier ``before``. Nếu ``false``, chỉ mục được trả về nằm sau tất cả các mục hiện có cùng giá trị trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedVector4Array_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedVector4Array_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedVector4Array_method_resize>` với kích thước ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) |const| :ref:`🔗<class_PackedVector4Array_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedVector4Array<class_PackedVector4Array>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedVector4Array_method_duplicate>`

Tạo và trả về một bản sao của mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có thao tác nào được thực hiện và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy dùng :ref:`remove_at()<class_PackedVector4Array_method_remove_at>`.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_fill>`

Gán giá trị đã cho cho tất cả các phần tử trong mảng. Thường có thể dùng kết hợp với :ref:`resize()<class_PackedVector4Array_method_resize>` để tạo một mảng có kích thước đã cho và các phần tử được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`Vector4<class_Vector4>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedVector4Array_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của giá trị đó hoặc ``-1`` nếu không tìm thấy. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_get:

.. rst-class:: classref-method

:ref:`Vector4<class_Vector4>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedVector4Array_method_get>`

Trả về :ref:`Vector4<class_Vector4>` tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``Vector4(0, 0, 0, 0)``.

Phương thức này tương tự (nhưng không giống hệt) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng quá trình thực thi project nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) |const| :ref:`🔗<class_PackedVector4Array_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_insert>`

Chèn một phần tử mới tại vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedVector4Array_method_is_empty>`

Trả về ``true`` nếu mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_push_back>`

Chèn một :ref:`Vector4<class_Vector4>` vào cuối.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector4Array_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector4Array_method_resize>`

Thiết lập kích thước của mảng. Nếu mảng được mở rộng, dành chỗ cho các phần tử ở cuối mảng. Nếu mảng bị thu nhỏ, cắt mảng xuống kích thước mới. Gọi :ref:`resize()<class_PackedVector4Array_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn so với việc thêm từng phần tử mới.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Dùng :ref:`size()<class_PackedVector4Array_method_size>` để tìm kích thước thực tế của mảng sau khi resize.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedVector4Array_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`Vector4<class_Vector4>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedVector4Array_method_rfind>`

Tìm kiếm mảng theo thứ tự ngược. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm. Nếu là số âm, chỉ mục bắt đầu được tính tương đối từ cuối mảng.

\ **Lưu ý:** Vector có các phần tử :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các vector khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_PackedVector4Array_method_set>`

Thay đổi :ref:`Vector4<class_Vector4>` tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedVector4Array_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_slice:

.. rst-class:: classref-method

:ref:`PackedVector4Array<class_PackedVector4Array>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedVector4Array_method_slice>`

Trả về phần lát cắt của **PackedVector4Array**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedVector4Array** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước mảng, vì vậy giá trị mặc định của ``end`` khiến phương thức này mặc định cắt đến kích thước của mảng (tức là ``arr.slice(1)`` là cách viết rút gọn của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết rút gọn của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedVector4Array_method_sort>`

Sắp xếp các phần tử của mảng theo thứ tự tăng dần.

\ **Lưu ý:** Các vector có :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` phần tử không hoạt động giống như các vector khác. Do đó, kết quả của phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedVector4Array_method_to_byte_array>`

Trả về một :ref:`PackedByteArray<class_PackedByteArray>`, trong đó mỗi vector được mã hóa thành các byte.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các toán tử
-----------------

.. _class_PackedVector4Array_operator_neq_PackedVector4Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) :ref:`🔗<class_PackedVector4Array_operator_neq_PackedVector4Array>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_operator_sum_PackedVector4Array:

.. rst-class:: classref-operator

:ref:`PackedVector4Array<class_PackedVector4Array>` **operator +**\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) :ref:`🔗<class_PackedVector4Array_operator_sum_PackedVector4Array>`

Trả về một **PackedVector4Array** mới, với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu năng tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedVector4Array_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_operator_eq_PackedVector4Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ ) :ref:`🔗<class_PackedVector4Array_operator_eq_PackedVector4Array>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có tất cả :ref:`Vector4<class_Vector4>`\ s bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedVector4Array_operator_idx_int:

.. rst-class:: classref-operator

:ref:`Vector4<class_Vector4>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedVector4Array_operator_idx_int>`

Trả về :ref:`Vector4<class_Vector4>` tại chỉ mục ``index``. Có thể sử dụng chỉ mục âm để truy cập các phần tử bắt đầu từ cuối mảng. Sử dụng chỉ mục nằm ngoài giới hạn của mảng sẽ gây ra lỗi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
