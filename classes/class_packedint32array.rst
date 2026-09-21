:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedInt32Array.xml.

.. _class_PackedInt32Array:

PackedInt32Array
================

Một mảng đóng gói gồm các số nguyên 32-bit.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế riêng để chứa các giá trị số nguyên 32-bit. Dữ liệu được đóng gói chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

\ **Lưu ý:** Kiểu này lưu các số nguyên 32-bit có dấu, nghĩa là nó có thể nhận các giá trị trong khoảng ``[-2^31, 2^31 - 1]``, tức là ``[-2147483648, 2147483647]``. Việc vượt quá các giới hạn đó sẽ khiến giá trị quay vòng. Để so sánh, :ref:`int<class_int>` sử dụng các số nguyên 64-bit có dấu, có thể chứa các giá trị lớn hơn nhiều. Nếu cần đóng gói chặt chẽ các số nguyên 64-bit, hãy xem :ref:`PackedInt64Array<class_PackedInt64Array>`.

\ **Lưu ý:** Các mảng đóng gói luôn được truyền bằng tham chiếu. Để lấy một bản sao của mảng có thể được sửa đổi độc lập với mảng ban đầu, hãy sử dụng :ref:`duplicate()<class_PackedInt32Array_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức tích hợp sẵn. Trong những trường hợp này, mảng đóng gói được trả về là một bản sao, và việc thay đổi nó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật một thuộc tính tích hợp sẵn của kiểu này, hãy sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, một mảng đóng gói sẽ được đánh giá là ``false`` nếu nó rỗng. Nếu không, một mảng đóng gói sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`PackedInt32Array<class_PackedInt32Array_constructor_PackedInt32Array>`\ (\ )                                                         |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`PackedInt32Array<class_PackedInt32Array_constructor_PackedInt32Array>`\ (\ from\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`PackedInt32Array<class_PackedInt32Array_constructor_PackedInt32Array>`\ (\ from\: :ref:`Array<class_Array>`\ )                       |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`append<class_PackedInt32Array_method_append>`\ (\ value\: :ref:`int<class_int>`\ )                                                    |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`append_array<class_PackedInt32Array_method_append_array>`\ (\ array\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`bsearch<class_PackedInt32Array_method_bsearch>`\ (\ value\: :ref:`int<class_int>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`clear<class_PackedInt32Array_method_clear>`\ (\ )                                                                                     |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`count<class_PackedInt32Array_method_count>`\ (\ value\: :ref:`int<class_int>`\ ) |const|                                              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`duplicate<class_PackedInt32Array_method_duplicate>`\ (\ ) |const|                                                                     |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`erase<class_PackedInt32Array_method_erase>`\ (\ value\: :ref:`int<class_int>`\ )                                                      |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`fill<class_PackedInt32Array_method_fill>`\ (\ value\: :ref:`int<class_int>`\ )                                                        |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`find<class_PackedInt32Array_method_find>`\ (\ value\: :ref:`int<class_int>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get<class_PackedInt32Array_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                  |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`has<class_PackedInt32Array_method_has>`\ (\ value\: :ref:`int<class_int>`\ ) |const|                                                  |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`insert<class_PackedInt32Array_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`int<class_int>`\ )                  |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_empty<class_PackedInt32Array_method_is_empty>`\ (\ ) |const|                                                                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`push_back<class_PackedInt32Array_method_push_back>`\ (\ value\: :ref:`int<class_int>`\ )                                              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`remove_at<class_PackedInt32Array_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`resize<class_PackedInt32Array_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`reverse<class_PackedInt32Array_method_reverse>`\ (\ )                                                                                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`rfind<class_PackedInt32Array_method_rfind>`\ (\ value\: :ref:`int<class_int>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set<class_PackedInt32Array_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`int<class_int>`\ )                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`size<class_PackedInt32Array_method_size>`\ (\ ) |const|                                                                               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`slice<class_PackedInt32Array_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|    |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`sort<class_PackedInt32Array_method_sort>`\ (\ )                                                                                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`   | :ref:`to_byte_array<class_PackedInt32Array_method_to_byte_array>`\ (\ ) |const|                                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`operator !=<class_PackedInt32Array_operator_neq_PackedInt32Array>`\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`operator +<class_PackedInt32Array_operator_sum_PackedInt32Array>`\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`operator ==<class_PackedInt32Array_operator_eq_PackedInt32Array>`\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`operator []<class_PackedInt32Array_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                        |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_PackedInt32Array_constructor_PackedInt32Array:

.. rst-class:: classref-constructor

:ref:`PackedInt32Array<class_PackedInt32Array>` **PackedInt32Array**\ (\ ) :ref:`🔗<class_PackedInt32Array_constructor_PackedInt32Array>`

Tạo một **PackedInt32Array** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedInt32Array<class_PackedInt32Array>` **PackedInt32Array**\ (\ from\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )

Tạo một **PackedInt32Array** dưới dạng bản sao của **PackedInt32Array** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedInt32Array<class_PackedInt32Array>` **PackedInt32Array**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedInt32Array** mới. Bạn có thể truyền vào một :ref:`Array<class_Array>` generic tùy chọn để chuyển đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedInt32Array_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedInt32Array_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_PackedInt32Array_method_append_array>`

Thêm một **PackedInt32Array** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`int<class_int>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedInt32Array_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn để duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng tìm kiếm nhị phân. Có thể truyền vào một bộ chỉ định ``before`` tùy chọn. Nếu ``false``, chỉ mục được trả về sẽ nằm sau tất cả các mục hiện có cùng giá trị trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedInt32Array_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedInt32Array_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedInt32Array_method_resize>` với kích thước ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedInt32Array_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedInt32Array_method_duplicate>`

Tạo một bản sao của mảng và trả về bản sao đó.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có gì xảy ra và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_PackedInt32Array_method_remove_at>`.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_fill>`

Gán giá trị đã cho cho tất cả phần tử trong mảng. Thông thường, có thể sử dụng phương thức này cùng với :ref:`resize()<class_PackedInt32Array_method_resize>` để tạo một mảng có kích thước nhất định và các phần tử đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`int<class_int>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedInt32Array_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của giá trị đó, hoặc ``-1`` nếu không tìm thấy. Có thể truyền vào chỉ mục bắt đầu tìm kiếm tùy chọn.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_get:

.. rst-class:: classref-method

:ref:`int<class_int>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedInt32Array_method_get>`

Trả về số nguyên 32-bit tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``0``.

Phương thức này tương tự (nhưng không giống hệt) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng quá trình thực thi project nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedInt32Array_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_insert>`

Chèn một số nguyên mới vào vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedInt32Array_method_is_empty>`

Trả về ``true`` nếu mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_push_back>`

Thêm một giá trị vào mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_resize>`

Đặt kích thước của mảng. Nếu mảng được mở rộng, các phần tử sẽ được dự trữ ở cuối mảng. Nếu mảng bị thu nhỏ, mảng sẽ bị cắt ngắn về kích thước mới. Gọi :ref:`resize()<class_PackedInt32Array_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn so với việc thêm từng phần tử một.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu thành công, hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm, hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Sử dụng :ref:`size()<class_PackedInt32Array_method_size>` để tìm kích thước thực tế của mảng sau khi resize.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedInt32Array_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`int<class_int>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedInt32Array_method_rfind>`

Tìm kiếm trong mảng theo thứ tự ngược. Có thể truyền vào chỉ mục bắt đầu tìm kiếm tùy chọn. Nếu là số âm, chỉ mục bắt đầu được tính tương đối từ cuối mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_method_set>`

Thay đổi số nguyên tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedInt32Array_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_slice:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedInt32Array_method_slice>`

Trả về phần cắt của **PackedInt32Array**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedInt32Array** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước mảng, vì vậy giá trị mặc định của ``end`` khiến phần cắt mặc định kéo dài đến kích thước của mảng (tức là ``arr.slice(1)`` là cách viết tắt của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết tắt của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedInt32Array_method_sort>`

Sắp xếp các phần tử trong mảng theo thứ tự tăng dần.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedInt32Array_method_to_byte_array>`

Trả về một bản sao của dữ liệu được chuyển đổi thành :ref:`PackedByteArray<class_PackedByteArray>`, trong đó mỗi phần tử được mã hóa thành 4 byte.

Kích thước của mảng mới sẽ là ``int32_array.size() * 4``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_PackedInt32Array_operator_neq_PackedInt32Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_PackedInt32Array_operator_neq_PackedInt32Array>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_operator_sum_PackedInt32Array:

.. rst-class:: classref-operator

:ref:`PackedInt32Array<class_PackedInt32Array>` **operator +**\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_PackedInt32Array_operator_sum_PackedInt32Array>`

Trả về một **PackedInt32Array** mới với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu năng tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedInt32Array_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_operator_eq_PackedInt32Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_PackedInt32Array_operator_eq_PackedInt32Array>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có các số nguyên bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedInt32Array_operator_idx_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedInt32Array_operator_idx_int>`

Trả về :ref:`int<class_int>` tại chỉ mục ``index``. Có thể sử dụng chỉ mục âm để truy cập các phần tử tính từ cuối mảng. Việc sử dụng chỉ mục nằm ngoài giới hạn của mảng sẽ gây ra lỗi.

Lưu ý rằng kiểu của :ref:`int<class_int>` là 64-bit, không giống với các giá trị được lưu trữ trong mảng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
