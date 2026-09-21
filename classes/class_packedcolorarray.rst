:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedColorArray.xml.

.. _class_PackedColorArray:

PackedColorArray
================

Một mảng đóng gói của :ref:`Color<class_Color>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế riêng để chứa :ref:`Color<class_Color>`. Dữ liệu được đóng gói chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

\ **Sự khác biệt giữa packed array, typed array và untyped array:** Packed array thường nhanh hơn khi duyệt và sửa đổi so với typed array cùng kiểu (ví dụ: **PackedColorArray** so với ``Array[Color]``). Packed array cũng tiêu tốn ít bộ nhớ hơn. Đổi lại, packed array kém linh hoạt hơn vì không cung cấp nhiều phương thức tiện ích như :ref:`Array.map()<class_Array_method_map>`. Typed array lại nhanh hơn untyped array khi duyệt và sửa đổi.

\ **Lưu ý:** Packed array luôn được truyền bằng tham chiếu. Để lấy một bản sao của mảng có thể được sửa đổi độc lập với mảng ban đầu, hãy sử dụng :ref:`duplicate()<class_PackedColorArray_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức tích hợp sẵn. Trong những trường hợp này, packed array được trả về là một bản sao và việc thay đổi nó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật một thuộc tính tích hợp sẵn thuộc kiểu này, hãy sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, packed array sẽ được đánh giá là ``false`` nếu nó rỗng. Nếu không, packed array luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`PackedColorArray<class_PackedColorArray_constructor_PackedColorArray>`\ (\ )                                                         |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`PackedColorArray<class_PackedColorArray_constructor_PackedColorArray>`\ (\ from\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`PackedColorArray<class_PackedColorArray_constructor_PackedColorArray>`\ (\ from\: :ref:`Array<class_Array>`\ )                       |
   +-------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`append<class_PackedColorArray_method_append>`\ (\ value\: :ref:`Color<class_Color>`\ )                                                    |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`append_array<class_PackedColorArray_method_append_array>`\ (\ array\: :ref:`PackedColorArray<class_PackedColorArray>`\ )                  |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`bsearch<class_PackedColorArray_method_bsearch>`\ (\ value\: :ref:`Color<class_Color>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`clear<class_PackedColorArray_method_clear>`\ (\ )                                                                                         |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`count<class_PackedColorArray_method_count>`\ (\ value\: :ref:`Color<class_Color>`\ ) |const|                                              |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`duplicate<class_PackedColorArray_method_duplicate>`\ (\ ) |const|                                                                         |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`erase<class_PackedColorArray_method_erase>`\ (\ value\: :ref:`Color<class_Color>`\ )                                                      |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`fill<class_PackedColorArray_method_fill>`\ (\ value\: :ref:`Color<class_Color>`\ )                                                        |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`find<class_PackedColorArray_method_find>`\ (\ value\: :ref:`Color<class_Color>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                       | :ref:`get<class_PackedColorArray_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                      |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`has<class_PackedColorArray_method_has>`\ (\ value\: :ref:`Color<class_Color>`\ ) |const|                                                  |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`insert<class_PackedColorArray_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Color<class_Color>`\ )                  |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_empty<class_PackedColorArray_method_is_empty>`\ (\ ) |const|                                                                           |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`push_back<class_PackedColorArray_method_push_back>`\ (\ value\: :ref:`Color<class_Color>`\ )                                              |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`remove_at<class_PackedColorArray_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                                  |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`resize<class_PackedColorArray_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                     |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`reverse<class_PackedColorArray_method_reverse>`\ (\ )                                                                                     |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`rfind<class_PackedColorArray_method_rfind>`\ (\ value\: :ref:`Color<class_Color>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set<class_PackedColorArray_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Color<class_Color>`\ )                           |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`size<class_PackedColorArray_method_size>`\ (\ ) |const|                                                                                   |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`slice<class_PackedColorArray_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|        |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`sort<class_PackedColorArray_method_sort>`\ (\ )                                                                                           |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`   | :ref:`to_byte_array<class_PackedColorArray_method_to_byte_array>`\ (\ ) |const|                                                                 |
   +-------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`operator !=<class_PackedColorArray_operator_neq_PackedColorArray>`\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`operator +<class_PackedColorArray_operator_sum_PackedColorArray>`\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ )  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`operator ==<class_PackedColorArray_operator_eq_PackedColorArray>`\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ )  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                       | :ref:`operator []<class_PackedColorArray_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                        |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_PackedColorArray_constructor_PackedColorArray:

.. rst-class:: classref-constructor

:ref:`PackedColorArray<class_PackedColorArray>` **PackedColorArray**\ (\ ) :ref:`🔗<class_PackedColorArray_constructor_PackedColorArray>`

Tạo một **PackedColorArray** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedColorArray<class_PackedColorArray>` **PackedColorArray**\ (\ from\: :ref:`PackedColorArray<class_PackedColorArray>`\ )

Tạo một **PackedColorArray** dưới dạng bản sao của **PackedColorArray** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedColorArray<class_PackedColorArray>` **PackedColorArray**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedColorArray** mới. Bạn có thể tùy chọn truyền vào một :ref:`Array<class_Array>` generic để chuyển đổi.

\ **Lưu ý:** Khi khởi tạo **PackedColorArray** với các phần tử, mảng phải được khởi tạo bằng một :ref:`Array<class_Array>` gồm các giá trị :ref:`Color<class_Color>`:

::

    var array = PackedColorArray([Color(0.1, 0.2, 0.3), Color(0.4, 0.5, 0.6)])

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedColorArray_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedColorArray_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) :ref:`🔗<class_PackedColorArray_method_append_array>`

Thêm một **PackedColorArray** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`Color<class_Color>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedColorArray_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng tìm kiếm nhị phân. Có thể tùy chọn truyền vào một bộ chỉ định ``before``. Nếu ``false``, chỉ mục được trả về sẽ nằm sau tất cả các mục hiện có của giá trị đó trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedColorArray_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedColorArray_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedColorArray_method_resize>` với kích thước ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`Color<class_Color>`\ ) |const| :ref:`🔗<class_PackedColorArray_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedColorArray<class_PackedColorArray>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedColorArray_method_duplicate>`

Tạo và trả về một bản sao của mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có gì xảy ra và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_PackedColorArray_method_remove_at>`.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_fill>`

Gán giá trị đã cho cho tất cả phần tử trong mảng. Thường có thể sử dụng cùng với :ref:`resize()<class_PackedColorArray_method_resize>` để tạo một mảng có kích thước cho trước và các phần tử đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`Color<class_Color>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedColorArray_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của giá trị đó hoặc ``-1`` nếu không tìm thấy. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_get:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedColorArray_method_get>`

Trả về :ref:`Color<class_Color>` tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``Color(0, 0, 0, 1)``.

Phương thức này tương tự (nhưng không giống hệt) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng quá trình thực thi project nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`Color<class_Color>`\ ) |const| :ref:`🔗<class_PackedColorArray_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_insert>`

Chèn một phần tử mới vào vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedColorArray_method_is_empty>`

Trả về ``true`` nếu mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_push_back>`

Thêm một giá trị vào mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedColorArray_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedColorArray_method_resize>`

Đặt kích thước của mảng. Nếu mảng được mở rộng, các phần tử sẽ được dành chỗ ở cuối mảng. Nếu mảng bị thu nhỏ, mảng sẽ bị cắt ngắn về kích thước mới. Gọi :ref:`resize()<class_PackedColorArray_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn việc thêm từng phần tử mới.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Sử dụng :ref:`size()<class_PackedColorArray_method_size>` để tìm kích thước thực tế của mảng sau khi resize.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedColorArray_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`Color<class_Color>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedColorArray_method_rfind>`

Tìm kiếm mảng theo thứ tự ngược. Có thể tùy chọn truyền vào chỉ mục bắt đầu tìm kiếm. Nếu là số âm, chỉ mục bắt đầu được tính tương đối từ cuối mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_PackedColorArray_method_set>`

Thay đổi :ref:`Color<class_Color>` tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedColorArray_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_slice:

.. rst-class:: classref-method

:ref:`PackedColorArray<class_PackedColorArray>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedColorArray_method_slice>`

Trả về phần cắt của **PackedColorArray**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedColorArray** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước mảng, vì vậy giá trị mặc định của ``end`` khiến phần cắt mặc định kéo dài đến kích thước mảng (tức là ``arr.slice(1)`` là cách viết tắt của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối từ cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết tắt của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedColorArray_method_sort>`

Sắp xếp các phần tử trong mảng theo thứ tự tăng dần.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedColorArray_method_to_byte_array>`

Trả về một :ref:`PackedByteArray<class_PackedByteArray>` với mỗi màu được mã hóa dưới dạng byte.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_PackedColorArray_operator_neq_PackedColorArray:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) :ref:`🔗<class_PackedColorArray_operator_neq_PackedColorArray>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_operator_sum_PackedColorArray:

.. rst-class:: classref-operator

:ref:`PackedColorArray<class_PackedColorArray>` **operator +**\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) :ref:`🔗<class_PackedColorArray_operator_sum_PackedColorArray>`

Trả về một **PackedColorArray** mới với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu suất tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedColorArray_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_operator_eq_PackedColorArray:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) :ref:`🔗<class_PackedColorArray_operator_eq_PackedColorArray>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có tất cả :ref:`Color<class_Color>`\ s bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedColorArray_operator_idx_int:

.. rst-class:: classref-operator

:ref:`Color<class_Color>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedColorArray_operator_idx_int>`

Trả về :ref:`Color<class_Color>` tại chỉ mục ``index``. Có thể sử dụng các chỉ mục âm để truy cập các phần tử bắt đầu từ cuối mảng. Việc sử dụng chỉ mục nằm ngoài giới hạn của mảng sẽ gây ra lỗi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
