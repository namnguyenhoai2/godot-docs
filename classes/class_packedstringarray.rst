:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PackedStringArray.xml.

.. _class_PackedStringArray:

PackedStringArray
=================

Một mảng packed gồm các :ref:`String<class_String>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng được thiết kế riêng để chứa các :ref:`String<class_String>`\ s. Dữ liệu được đóng gói chặt chẽ, giúp tiết kiệm bộ nhớ khi kích thước mảng lớn.

Nếu muốn nối các string trong mảng, hãy sử dụng :ref:`String.join()<class_String_method_join>`.

::

    var string_array = PackedStringArray(["hello", "world"])
    var string = " ".join(string_array)
    print(string) # "hello world"

\ **Sự khác biệt giữa packed array, typed array và untyped array:** Packed array thường nhanh hơn khi duyệt và sửa đổi so với typed array cùng kiểu (ví dụ: **PackedStringArray** so với ``Array[String]``). Ngoài ra, packed array sử dụng ít bộ nhớ hơn. Nhược điểm là packed array kém linh hoạt hơn vì không cung cấp nhiều phương thức tiện ích như :ref:`Array.map()<class_Array_method_map>`. Đổi lại, typed array nhanh hơn untyped array khi duyệt và sửa đổi.

\ **Lưu ý:** Packed array luôn được truyền theo tham chiếu. Để lấy một bản sao của mảng có thể được sửa đổi độc lập với mảng ban đầu, hãy sử dụng :ref:`duplicate()<class_PackedStringArray_method_duplicate>`. Điều này *không* áp dụng cho các thuộc tính và phương thức tích hợp sẵn. Trong những trường hợp này, packed array được trả về là một bản sao, và việc thay đổi nó sẽ *không* ảnh hưởng đến giá trị ban đầu. Để cập nhật thuộc tính tích hợp sẵn thuộc kiểu này, hãy sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

\ **Lưu ý:** Trong ngữ cảnh boolean, packed array sẽ được đánh giá là ``false`` nếu nó rỗng. Nếu không, packed array luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Operating System Testing Demo <https://godotengine.org/asset-library/asset/2789>`__

.. rst-class:: classref-reftable-group

Constructor
-----------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`PackedStringArray<class_PackedStringArray_constructor_PackedStringArray>`\ (\ )                                                           |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`PackedStringArray<class_PackedStringArray_constructor_PackedStringArray>`\ (\ from\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`PackedStringArray<class_PackedStringArray_constructor_PackedStringArray>`\ (\ from\: :ref:`Array<class_Array>`\ )                         |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`append<class_PackedStringArray_method_append>`\ (\ value\: :ref:`String<class_String>`\ )                                                    |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`append_array<class_PackedStringArray_method_append_array>`\ (\ array\: :ref:`PackedStringArray<class_PackedStringArray>`\ )                  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`bsearch<class_PackedStringArray_method_bsearch>`\ (\ value\: :ref:`String<class_String>`, before\: :ref:`bool<class_bool>` = true\ ) |const| |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`clear<class_PackedStringArray_method_clear>`\ (\ )                                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`count<class_PackedStringArray_method_count>`\ (\ value\: :ref:`String<class_String>`\ ) |const|                                              |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`duplicate<class_PackedStringArray_method_duplicate>`\ (\ ) |const|                                                                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`erase<class_PackedStringArray_method_erase>`\ (\ value\: :ref:`String<class_String>`\ )                                                      |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`fill<class_PackedStringArray_method_fill>`\ (\ value\: :ref:`String<class_String>`\ )                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`find<class_PackedStringArray_method_find>`\ (\ value\: :ref:`String<class_String>`, from\: :ref:`int<class_int>` = 0\ ) |const|              |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get<class_PackedStringArray_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`has<class_PackedStringArray_method_has>`\ (\ value\: :ref:`String<class_String>`\ ) |const|                                                  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`insert<class_PackedStringArray_method_insert>`\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`String<class_String>`\ )                  |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_empty<class_PackedStringArray_method_is_empty>`\ (\ ) |const|                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`push_back<class_PackedStringArray_method_push_back>`\ (\ value\: :ref:`String<class_String>`\ )                                              |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`remove_at<class_PackedStringArray_method_remove_at>`\ (\ index\: :ref:`int<class_int>`\ )                                                    |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`resize<class_PackedStringArray_method_resize>`\ (\ new_size\: :ref:`int<class_int>`\ )                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`reverse<class_PackedStringArray_method_reverse>`\ (\ )                                                                                       |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`rfind<class_PackedStringArray_method_rfind>`\ (\ value\: :ref:`String<class_String>`, from\: :ref:`int<class_int>` = -1\ ) |const|           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set<class_PackedStringArray_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`String<class_String>`\ )                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`size<class_PackedStringArray_method_size>`\ (\ ) |const|                                                                                     |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`slice<class_PackedStringArray_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const|          |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`sort<class_PackedStringArray_method_sort>`\ (\ )                                                                                             |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`     | :ref:`to_byte_array<class_PackedStringArray_method_to_byte_array>`\ (\ ) |const|                                                                   |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`operator !=<class_PackedStringArray_operator_neq_PackedStringArray>`\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`operator +<class_PackedStringArray_operator_sum_PackedStringArray>`\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ )  |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`operator ==<class_PackedStringArray_operator_eq_PackedStringArray>`\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ )  |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`operator []<class_PackedStringArray_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                                           |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả constructor
-----------------

.. _class_PackedStringArray_constructor_PackedStringArray:

.. rst-class:: classref-constructor

:ref:`PackedStringArray<class_PackedStringArray>` **PackedStringArray**\ (\ ) :ref:`🔗<class_PackedStringArray_constructor_PackedStringArray>`

Tạo một **PackedStringArray** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedStringArray<class_PackedStringArray>` **PackedStringArray**\ (\ from\: :ref:`PackedStringArray<class_PackedStringArray>`\ )

Tạo một **PackedStringArray** dưới dạng bản sao của **PackedStringArray** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`PackedStringArray<class_PackedStringArray>` **PackedStringArray**\ (\ from\: :ref:`Array<class_Array>`\ )

Tạo một **PackedStringArray** mới. Bạn có thể truyền vào một :ref:`Array<class_Array>` generic tùy chọn để chuyển đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PackedStringArray_method_append:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **append**\ (\ value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_append>`

Thêm một phần tử vào cuối mảng (bí danh của :ref:`push_back()<class_PackedStringArray_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_PackedStringArray_method_append_array>`

Thêm một **PackedStringArray** vào cuối mảng này.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`String<class_String>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_PackedStringArray_method_bsearch>`

Tìm chỉ mục của một giá trị hiện có (hoặc chỉ mục chèn để duy trì thứ tự sắp xếp nếu giá trị chưa có trong mảng) bằng tìm kiếm nhị phân. Có thể truyền vào một bộ chỉ định ``before`` tùy chọn. Nếu ``false``, chỉ mục được trả về sẽ nằm sau tất cả các mục hiện có cùng giá trị trong mảng.

\ **Lưu ý:** Gọi :ref:`bsearch()<class_PackedStringArray_method_bsearch>` trên một mảng chưa được sắp xếp sẽ dẫn đến hành vi không mong muốn.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_PackedStringArray_method_clear>`

Xóa mảng. Tương đương với việc sử dụng :ref:`resize()<class_PackedStringArray_method_resize>` với kích thước là ``0``.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_PackedStringArray_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_duplicate:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **duplicate**\ (\ ) |const| :ref:`🔗<class_PackedStringArray_method_duplicate>`

Tạo và trả về một bản sao của mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_erase>`

Xóa lần xuất hiện đầu tiên của một giá trị khỏi mảng và trả về ``true``. Nếu giá trị không tồn tại trong mảng, không có gì xảy ra và ``false`` được trả về. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_PackedStringArray_method_remove_at>`.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_fill>`

Gán giá trị đã cho cho tất cả phần tử trong mảng. Thông thường có thể sử dụng cùng với :ref:`resize()<class_PackedStringArray_method_resize>` để tạo một mảng có kích thước cho trước và các phần tử đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ value\: :ref:`String<class_String>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PackedStringArray_method_find>`

Tìm kiếm một giá trị trong mảng và trả về chỉ mục của nó hoặc ``-1`` nếu không tìm thấy. Có thể truyền vào chỉ mục bắt đầu tìm kiếm tùy chọn.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_get:

.. rst-class:: classref-method

:ref:`String<class_String>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_PackedStringArray_method_get>`

Trả về :ref:`String<class_String>` tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về một string rỗng.

Phương thức này tương tự (nhưng không hoàn toàn giống) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng việc thực thi project nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_PackedStringArray_method_has>`

Trả về ``true`` nếu mảng chứa ``value``.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ at_index\: :ref:`int<class_int>`, value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_insert>`

Chèn một phần tử mới tại vị trí đã cho trong mảng. Vị trí phải hợp lệ hoặc nằm ở cuối mảng (``idx == size()``).

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_PackedStringArray_method_is_empty>`

Trả về ``true`` nếu mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_push_back:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **push_back**\ (\ value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_push_back>`

Thêm một phần tử string vào cuối mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedStringArray_method_remove_at>`

Xóa một phần tử khỏi mảng theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ new_size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedStringArray_method_resize>`

Thiết lập kích thước của mảng. Nếu mảng được mở rộng, các phần tử sẽ được dành chỗ ở cuối mảng. Nếu mảng bị thu nhỏ, mảng sẽ bị cắt ngắn về kích thước mới. Gọi :ref:`resize()<class_PackedStringArray_method_resize>` một lần rồi gán các giá trị mới sẽ nhanh hơn so với thêm từng phần tử mới.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Sử dụng :ref:`size()<class_PackedStringArray_method_size>` để tìm kích thước thực tế của mảng sau khi resize.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_PackedStringArray_method_reverse>`

Đảo ngược thứ tự các phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ value\: :ref:`String<class_String>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_PackedStringArray_method_rfind>`

Tìm kiếm mảng theo thứ tự ngược. Có thể truyền vào chỉ mục bắt đầu tìm kiếm tùy chọn. Nếu là số âm, chỉ mục bắt đầu được tính tương đối với cuối mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PackedStringArray_method_set>`

Thay đổi :ref:`String<class_String>` tại chỉ mục đã cho.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_PackedStringArray_method_size>`

Trả về số phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_slice:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647\ ) |const| :ref:`🔗<class_PackedStringArray_method_slice>`

Trả về phần slice của **PackedStringArray**, từ ``begin`` (bao gồm) đến ``end`` (không bao gồm), dưới dạng một **PackedStringArray** mới.

Giá trị tuyệt đối của ``begin`` và ``end`` sẽ được giới hạn theo kích thước mảng, vì vậy giá trị mặc định của ``end`` khiến slice mặc định kéo dài đến kích thước mảng (tức là ``arr.slice(1)`` là cách viết rút gọn của ``arr.slice(1, arr.size())``).

Nếu ``begin`` hoặc ``end`` là số âm, chúng sẽ được tính tương đối với cuối mảng (tức là ``arr.slice(0, -2)`` là cách viết rút gọn của ``arr.slice(0, arr.size() - 2)``).

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_PackedStringArray_method_sort>`

Sắp xếp các phần tử trong mảng theo thứ tự tăng dần.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_method_to_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **to_byte_array**\ (\ ) |const| :ref:`🔗<class_PackedStringArray_method_to_byte_array>`

Trả về một :ref:`PackedByteArray<class_PackedByteArray>` với mỗi string được mã hóa bằng UTF-8. Các string được kết thúc bằng ``null``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_PackedStringArray_operator_neq_PackedStringArray:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_PackedStringArray_operator_neq_PackedStringArray>`

Trả về ``true`` nếu nội dung của các mảng khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_operator_sum_PackedStringArray:

.. rst-class:: classref-operator

:ref:`PackedStringArray<class_PackedStringArray>` **operator +**\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_PackedStringArray_operator_sum_PackedStringArray>`

Trả về một **PackedStringArray** mới với nội dung của ``right`` được thêm vào cuối mảng này. Để có hiệu suất tốt hơn, hãy cân nhắc sử dụng :ref:`append_array()<class_PackedStringArray_method_append_array>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_operator_eq_PackedStringArray:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_PackedStringArray_operator_eq_PackedStringArray>`

Trả về ``true`` nếu nội dung của cả hai mảng giống nhau, tức là chúng có tất cả :ref:`String<class_String>`\ s bằng nhau tại các chỉ mục tương ứng.

.. rst-class:: classref-item-separator

----

.. _class_PackedStringArray_operator_idx_int:

.. rst-class:: classref-operator

:ref:`String<class_String>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PackedStringArray_operator_idx_int>`

Trả về :ref:`String<class_String>` tại chỉ mục ``index``. Có thể sử dụng các chỉ mục âm để truy cập các phần tử bắt đầu từ cuối mảng. Việc sử dụng chỉ mục nằm ngoài phạm vi của mảng sẽ gây ra lỗi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
