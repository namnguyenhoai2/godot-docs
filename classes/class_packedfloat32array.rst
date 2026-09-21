:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedFloat32Array.xml.

.. _class_PackedFloat32Array:

PackedFloat32Array
==================

Một mảng đóng gói gồm các giá trị dấu phẩy động 32-bit.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế đặc biệt để chứa các giá trị dấu phẩy động 32-bit (float). Dữ liệu được đóng gói chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

Nếu bạn cần đóng gói chặt chẽ các số dấu phẩy động 64-bit, hãy xem :ref:`PackedFloat64Array<class_PackedFloat64Array>`.

\ **Lưu ý:** Các mảng đóng gói luôn được truyền bằng tham chiếu. Để lấy một bản sao của mảng có thể được sửa đổi độc lập với mảng ban đầu, hãy sử dụng :ref:`duplicate()<class_PackedFloat32Array_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức tích hợp sẵn. Trong những trường hợp này, mảng đóng gói được trả về là một bản sao và việc thay đổi mảng đó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật một thuộc tính tích hợp sẵn thuộc kiểu này, hãy sửa đổi mảng được trả về rồi gán lại nó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, một mảng đóng gói sẽ được đánh giá là ``false`` nếu nó rỗng. Nếu không, một mảng đóng gói sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`PackedFloat32Array<class_PackedFloat32Array_constructor_PackedFloat32Array>`\ (\ )                                                             |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`PackedFloat32Array<class_PackedFloat32Array_constructor_PackedFloat32Array>`\ (\ from\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`PackedFloat32Array<class_PackedFloat32Array_constructor_PackedFloat32Array>`\ (\ from\: :ref:`Array<class_Array>`\ )                           |
   +-----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`append<class_PackedFloat32Array_method_append>`\ (\ value\: :ref:`float<class_float>`\ )                                                    |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`append_array<class_PackedFloat32Array_method_append_array>`\ (\ array\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )              |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`bsearch<class_PackedFloat32Array_method_bsearch>`\ (\ value\: :ref:`float<class_float>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_PackedFloat32Array_method_clear>`\ (\ )                                                                                         |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`count<class_PackedFloat32Array_method_count>`\ (\ value\: :ref:`float<class_float>`\ ) |const|                                              |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`duplicate<class_PackedFloat32Array_method_duplicate>`\ (\ ) |const|                                                                         |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`erase<class_PackedFloat32Array_method_erase>`\ (\ value\: :ref:`float<class_float>`\ )                                                      |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`fill<class_PackedFloat32Array_method_fill>`\ (\ value\: :ref:`float<class_float>`\ )                                                        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`find<class_PackedFloat32Array_method_find>`\ (\ value\: :ref:`float<class_float>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get<class_PackedFloat32Array_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                      |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`has<class_PackedFloat32Array_method_has>`\ (\ value\: :ref:`float<class_float>`\ ) |const|                                                  |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`insert<class_PackedFloat32Array_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ )                  |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_empty<class_PackedFloat32Array_method_is_empty>`\ (\ ) |const|                                                                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`push_back<class_PackedFloat32Array_method_push_back>`\ (\ value\: :ref:`float<class_float>`\ )                                              |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_at<class_PackedFloat32Array_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                                  |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`resize<class_PackedFloat32Array_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                     |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`reverse<class_PackedFloat32Array_method_reverse>`\ (\ )                                                                                     |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`rfind<class_PackedFloat32Array_method_rfind>`\ (\ value\: :ref:`float<class_float>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set<class_PackedFloat32Array_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ )                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`size<class_PackedFloat32Array_method_size>`\ (\ ) |const|                                                                                   |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`slice<class_PackedFloat32Array_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`sort<class_PackedFloat32Array_method_sort>`\ (\ )                                                                                           |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`       | :ref:`to_byte_array<class_PackedFloat32Array_method_to_byte_array>`\ (\ ) |const|                                                                 |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator !=<class_PackedFloat32Array_operator_neq_PackedFloat32Array>`\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`operator +<class_PackedFloat32Array_operator_sum_PackedFloat32Array>`\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`operator ==<class_PackedFloat32Array_operator_eq_PackedFloat32Array>`\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`operator []<class_PackedFloat32Array_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                              |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_PackedFloat32Array_constructor_PackedFloat32Array:

.. rst-class:: classref-constructor

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **PackedFloat32Array**\ (\ ) :ref:`🔗<class_PackedFloat32Array_constructor_PackedFloat32Array>`

Tạo một **PackedFloat32Array** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **PackedFloat32Array**\ (\ from\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )

Tạo một **PackedFloat32Array** dưới dạng bản sao của **PackedFloat32Array** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **PackedFloat32Array**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedFloat32Array** mới. Bạn có thể tùy chọn truyền vào một :ref:`Array<class_Array>` tổng quát để chuyển đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedFloat32Array_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedFloat32Array_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_PackedFloat32Array_method_append_array>`

Thêm một **PackedFloat32Array** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`float<class_float>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng tìm kiếm nhị phân. Có thể tùy chọn truyền vào một bộ chỉ định ``before``. Nếu ``false``, chỉ mục được trả về nằm sau tất cả các mục hiện có chứa giá trị đó trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedFloat32Array_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedFloat32Array_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedFloat32Array_method_resize>` với kích thước ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_duplicate>`

Tạo một bản sao của mảng và trả về bản sao đó.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có gì xảy ra và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_PackedFloat32Array_method_remove_at>`.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_fill>`

Gán giá trị đã cho cho tất cả các phần tử trong mảng. Thông thường, có thể dùng phương thức này cùng với :ref:`resize()<class_PackedFloat32Array_method_resize>` để tạo một mảng có kích thước xác định và các phần tử đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`float<class_float>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của giá trị đó hoặc ``-1`` nếu không tìm thấy. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_get:

.. rst-class:: classref-method

:ref:`float<class_float>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_get>`

Trả về số dấu phẩy động 32-bit tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``0.0``.

Phương thức này tương tự (nhưng không hoàn toàn giống) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng việc thực thi dự án nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_insert>`

Chèn một phần tử mới vào vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_is_empty>`

Trả về ``true`` nếu mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_push_back>`

Thêm một phần tử vào cuối mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedFloat32Array_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedFloat32Array_method_resize>`

Đặt kích thước của mảng. Nếu mảng được mở rộng, các phần tử sẽ được dự trữ ở cuối mảng. Nếu mảng bị thu nhỏ, mảng sẽ bị cắt ngắn về kích thước mới. Gọi :ref:`resize()<class_PackedFloat32Array_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn việc thêm từng phần tử mới.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu cấp phát thất bại. Sử dụng :ref:`size()<class_PackedFloat32Array_method_size>` để tìm kích thước thực tế của mảng sau khi thay đổi kích thước.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedFloat32Array_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`float<class_float>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_rfind>`

Tìm kiếm mảng theo thứ tự ngược. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm. Nếu là số âm, chỉ mục bắt đầu được tính tương đối từ cuối mảng.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có chứa NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PackedFloat32Array_method_set>`

Thay đổi số dấu phẩy động tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_slice:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_slice>`

Trả về phần lát cắt của **PackedFloat32Array**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedFloat32Array** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước mảng, vì vậy giá trị mặc định của ``end`` khiến phương thức mặc định cắt đến kích thước của mảng (tức là ``arr.slice(1)`` là cách viết tắt của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết tắt của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedFloat32Array_method_sort>`

Sắp xếp các phần tử trong mảng theo thứ tự tăng dần.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống như các số khác. Do đó, kết quả từ phương thức này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedFloat32Array_method_to_byte_array>`

Trả về một bản sao của dữ liệu được chuyển đổi thành :ref:`PackedByteArray<class_PackedByteArray>`, trong đó mỗi phần tử được mã hóa thành 4 byte.

Kích thước của mảng mới sẽ là ``float32_array.size() * 4``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các toán tử
-----------------

.. _class_PackedFloat32Array_operator_neq_PackedFloat32Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_PackedFloat32Array_operator_neq_PackedFloat32Array>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_operator_sum_PackedFloat32Array:

.. rst-class:: classref-operator

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **operator +**\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_PackedFloat32Array_operator_sum_PackedFloat32Array>`

Trả về một **PackedFloat32Array** mới với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu năng tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedFloat32Array_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_operator_eq_PackedFloat32Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_PackedFloat32Array_operator_eq_PackedFloat32Array>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có tất cả các số thực bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedFloat32Array_operator_idx_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedFloat32Array_operator_idx_int>`

Trả về :ref:`float<class_float>` tại chỉ mục ``index``. Có thể sử dụng các chỉ mục âm để truy cập các phần tử tính từ cuối mảng. Sử dụng chỉ mục nằm ngoài giới hạn của mảng sẽ gây ra lỗi.

Lưu ý rằng kiểu :ref:`float<class_float>` là 64-bit, không giống các giá trị được lưu trữ trong mảng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
