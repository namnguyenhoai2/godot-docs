.. _doc_core_types:

Các kiểu cốt lõi
================

Godot có một tập hợp phong phú các lớp và template cấu thành phần cốt lõi, và mọi thứ đều được xây dựng dựa trên chúng.

Tài liệu tham chiếu này sẽ cố gắng liệt kê chúng theo thứ tự để giúp bạn hiểu rõ hơn.

Cấp phát bộ nhớ
---------------

Godot có nhiều cơ chế để đảm bảo an toàn bộ nhớ và theo dõi việc sử dụng bộ nhớ. Vì vậy, không nên sử dụng các lời gọi thư viện C và C++ thông thường. Thay vào đó, Godot cung cấp một số hàm thay thế.

Để cấp phát theo kiểu C, Godot cung cấp một số macro:

.. code-block:: cpp

    memalloc(size)
    memrealloc(pointer)
    memfree(pointer)

Các macro này tương đương với ``malloc()``, ``realloc()`` và ``free()`` thông thường của thư viện chuẩn C.

Để cấp phát theo kiểu C++, có các macro đặc biệt:

.. code-block:: cpp

    memnew(Class)
    memnew(Class(args))
    memdelete(instance)

    memnew_arr(Class, amount)
    memdelete_arr(pointer_to_array)

Các macro này lần lượt tương đương với ``new``, ``delete``, ``new[]`` và ``delete[]``.

``memnew``/``memdelete`` cũng sử dụng một chút phép màu C++ để tự động gọi các hàm post-init và pre-release. Ví dụ: cơ chế này được dùng để thông báo cho các Object ngay sau khi chúng được tạo và ngay trước khi chúng bị xóa.

-  `core/os/memory.h <https://github.com/godotengine/godot/blob/master/core/os/memory.h>`__

Container
---------

Godot cung cấp bộ container riêng, vì vậy các container STL như ``std::string`` và ``std::vector`` nhìn chung không được sử dụng trong codebase. Xem :ref:`doc_faq_why_not_stl` để biết thêm thông tin.

Biểu tượng 📜 cho biết kiểu này là một phần của :ref:`Variant <doc_variant_class>`. Điều này có nghĩa là kiểu này có thể được sử dụng làm tham số hoặc giá trị trả về của một phương thức được expose cho scripting API.

+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Kiểu dữ liệu Godot    | Kiểu dữ liệu C++ STL gần nhất | Chú thích                                                                                                                                                                                                                                                                                                                                                                                                  |
+=======================+===============================+============================================================================================================================================================================================================================================================================================================================================================================================================+
| |string| 📜           | ``std::string``               | **Sử dụng kiểu này làm kiểu string "mặc định".** ``String`` sử dụng encoding UTF-32 để đơn giản hóa việc xử lý nhờ kích thước ký tự cố định.                                                                                                                                                                                                                                                               |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |vector|              | ``std::vector``               | **Sử dụng kiểu này làm kiểu vector "mặc định".** Sử dụng ngữ nghĩa copy-on-write (COW). Điều này có nghĩa là kiểu này thường chậm hơn nhưng gần như có thể sao chép miễn phí. Hãy sử dụng ``LocalVector`` thay thế khi không cần COW và hiệu năng là yếu tố quan trọng.                                                                                                                                    |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |hash_set|            | ``std::unordered_set``        | **Sử dụng kiểu này làm kiểu set "mặc định".**                                                                                                                                                                                                                                                                                                                                                              |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |a_hash_map|          | ``std::unordered_map``        | **Sử dụng kiểu này làm kiểu map "mặc định".** Không duy trì thứ tự chèn. Lưu ý rằng các con trỏ trỏ vào map, cũng như các iterator, không ổn định khi map bị thay đổi. Nếu cần một trong hai khả năng này, hãy sử dụng ``HashMap`` thay thế.                                                                                                                                                               |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |string_name| 📜      | ``std::string``               | Sử dụng string interning để so sánh nhanh. Hãy dùng kiểu này cho các string tĩnh được tham chiếu thường xuyên và sử dụng ở nhiều vị trí trong engine.                                                                                                                                                                                                                                                      |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |char_string|,        | ``std::u8string``             | Các kiểu tương tự ``String`` sử dụng lần lượt ``char`` và ``char16_t``. Đây là các alias của ``CharStringT<T>``; ``wchar_t`` và các kiểu khác cũng được hỗ trợ.                                                                                                                                                                                                                                            |
| |char16_string|       | ``std::u16string``            |                                                                                                                                                                                                                                                                                                                                                                                                            |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |local_vector|        | ``std::vector``               | Gần với ``std::vector`` hơn về mặt ngữ nghĩa, không sử dụng copy-on-write (COW) nên nhanh hơn ``Vector``. Hãy ưu tiên kiểu này thay cho ``Vector`` khi không cần sao chép với chi phí thấp.                                                                                                                                                                                                                |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |array| 📜            | ``std::vector``               | Các giá trị có thể thuộc bất kỳ kiểu Variant nào. Không áp đặt kiểu tĩnh. Sử dụng reference counting dùng chung, tương tự ``std::shared_ptr``. Bên trong sử dụng Vector<Variant>.                                                                                                                                                                                                                          |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |typed_array| 📜      | ``std::vector``               | Lớp con của ``Array`` nhưng các phần tử được định kiểu tĩnh. Không nên nhầm lẫn với ``Packed*Array``, vốn bên trong là một ``Vector``.                                                                                                                                                                                                                                                                     |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |packed_array| 📜     | ``std::vector``               | Alias của ``Vector``, ví dụ ``PackedColorArray = Vector<Color>``. Chỉ có một danh sách giới hạn các kiểu packed array; nếu không, hãy sử dụng ``TypedArray``.                                                                                                                                                                                                                                              |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |list|                | ``std::list``                 | Kiểu linked list. Nhìn chung chậm hơn các kiểu array/vector khác. Trong code mới, hãy ưu tiên sử dụng các kiểu khác, trừ khi dùng ``List`` giúp tránh nhu cầu chuyển đổi kiểu.                                                                                                                                                                                                                             |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |fixed_vector|        | ``std::array``                | Vector có capacity cố định (tương tự ``boost::container::static_vector`` hơn). Kiểu container này hiệu quả hơn các kiểu tương tự vector khác vì không thực hiện cấp phát trên heap.                                                                                                                                                                                                                        |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |span|                | ``std::span``                 | Đại diện cho quyền truy cập chỉ đọc vào một array liên tục mà không cần sao chép dữ liệu. Lưu ý rằng ``Span`` được thiết kế như một API hiệu năng cao: API này không kiểm tra tính chính xác của tham số theo cùng cách mà bạn có thể đã quen thuộc với các container khác của Godot. Hãy sử dụng cẩn thận. ``Span`` có thể được khởi tạo từ hầu hết các container giống array (ví dụ: ``vector.span()``). |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |rb_set|              | ``std::set``                  | Sử dụng `cây đỏ-đen <https://en.wikipedia.org/wiki/Red-black_tree>`__ để truy cập nhanh hơn.                                                                                                                                                                                                                                                                                                               |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |v_set|               | ``std::flat_set``             | Sử dụng ngữ nghĩa copy-on-write (COW). Điều này có nghĩa là kiểu này thường chậm hơn nhưng gần như có thể sao chép miễn phí. Lợi ích hiệu năng của ``VSet`` chưa được xác định, vì vậy hãy ưu tiên sử dụng các kiểu khác.                                                                                                                                                                                  |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |hash_map|            | ``std::unordered_map``        | Kiểu map defensive (bền vững nhưng chậm). Duy trì thứ tự chèn. Các con trỏ trỏ đến key và value, cũng như các iterator, vẫn ổn định khi map bị thay đổi. Hãy sử dụng kiểu map này khi cần một trong hai khả năng đó. Nếu không, hãy sử dụng ``AHashMap``.                                                                                                                                                  |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |rb_map|              | ``std::map``                  | Kiểu map sử dụng `cây đỏ-đen <https://en.wikipedia.org/wiki/Red-black_tree>`__ để tìm key. Lợi ích hiệu năng của ``RBMap`` chưa được xác định, vì vậy hãy ưu tiên sử dụng các kiểu khác.                                                                                                                                                                                                                   |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |dictionary| 📜       | ``std::unordered_map``        | Key và value có thể thuộc bất kỳ kiểu Variant nào. Không áp đặt kiểu tĩnh. Sử dụng reference counting dùng chung, tương tự ``std::shared_ptr``. Duy trì thứ tự chèn. Bên trong sử dụng ``HashMap<Variant>``.                                                                                                                                                                                               |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |typed_dictionary| 📜 | ``std::unordered_map``        | Lớp con của ``Dictionary`` nhưng các key và value được định kiểu tĩnh.                                                                                                                                                                                                                                                                                                                                     |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| |pair|                | ``std::pair``                 | Lưu trữ một cặp duy nhất. Xem thêm ``KeyValue`` trong cùng tệp, kiểu này sử dụng các key chỉ đọc.                                                                                                                                                                                                                                                                                                          |
+-----------------------+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |string| replace:: `String <https://github.com/godotengine/godot/blob/master/core/string/ustring.h>`__
.. |vector| replace:: `Vector <https://github.com/godotengine/godot/blob/master/core/templates/vector.h>`__
.. |hash_set| replace:: `HashSet <https://github.com/godotengine/godot/blob/master/core/templates/hash_set.h>`__
.. |hash_map| replace:: `HashMap <https://github.com/godotengine/godot/blob/master/core/templates/hash_map.h>`__
.. |string_name| replace:: `StringName <https://github.com/godotengine/godot/blob/master/core/string/string_name.h>`__
.. |char_string| replace:: `CharString <https://github.com/godotengine/godot/blob/master/core/string/ustring.h>`__
.. |char16_string| replace:: `Char16String <https://github.com/godotengine/godot/blob/master/core/string/ustring.h>`__
.. |local_vector| replace:: `LocalVector <https://github.com/godotengine/godot/blob/master/core/templates/local_vector.h>`__
.. |array| replace:: `Array <https://github.com/godotengine/godot/blob/master/core/variant/array.h>`__
.. |typed_array| replace:: `TypedArray <https://github.com/godotengine/godot/blob/master/core/variant/typed_array.h>`__
.. |packed_array| replace:: `Packed*Array <https://github.com/godotengine/godot/blob/master/core/variant/variant.h>`__
.. |list| replace:: `List <https://github.com/godotengine/godot/blob/master/core/templates/list.h>`__
.. |fixed_vector| replace:: `FixedVector <https://github.com/godotengine/godot/blob/master/core/templates/fixed_vector.h>`__
.. |span| replace:: `Span <https://github.com/godotengine/godot/blob/master/core/templates/span.h>`__
.. |rb_set| replace:: `RBSet <https://github.com/godotengine/godot/blob/master/core/templates/rb_set.h>`__
.. |v_set| replace:: `VSet <https://github.com/godotengine/godot/blob/master/core/templates/vset.h>`__
.. |a_hash_map| replace:: `AHashMap <https://github.com/godotengine/godot/blob/master/core/templates/a_hash_map.h>`__
.. |rb_map| replace:: `RBMap <https://github.com/godotengine/godot/blob/master/core/templates/rb_map.h>`__
.. |dictionary| replace:: `Dictionary <https://github.com/godotengine/godot/blob/master/core/variant/dictionary.h>`__
.. |typed_dictionary| replace:: `TypedDictionary <https://github.com/godotengine/godot/blob/master/core/variant/typed_dictionary.h>`__
.. |pair| replace:: `Pair <https://github.com/godotengine/godot/blob/master/core/templates/pair.h>`__

Tính an toàn khi tái định vị
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các container của Godot giả định rằng các phần tử của chúng `có thể tái định vị một cách tầm thường <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html>`__.

Điều này có nghĩa là nếu bạn lưu trữ trong đó các kiểu dữ liệu có con trỏ trỏ đến chính chúng hoặc theo cách khác `không thể tái định vị một cách tầm thường <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html#non-trivial-samples>`__, Godot có thể bị crash. Lưu ý rằng việc lưu trữ **con trỏ đến** các đối tượng không thể tái định vị một cách tầm thường, chẳng hạn như một số lớp con của Object, là không có vấn đề và được hỗ trợ.

Lý do giả định khả năng tái định vị tầm thường là vì điều đó cho phép chúng ta sử dụng các kỹ thuật tối ưu hóa quan trọng, chẳng hạn như tái định vị bằng ``memcpy`` hoặc ``realloc``.

`GH-100509 <https://github.com/godotengine/godot/issues/100509>`__ theo dõi quyết định này.

.. _doc_core_concurrency_types:

Đa luồng / Đồng thời
--------------------

.. seealso::

    Bạn có thể tìm thêm thông tin về các chiến lược đa luồng tại :ref:`doc_using_multiple_threads`.

Không có container nào của Godot an toàn cho thread. Khi dự kiến có nhiều thread cùng truy cập chúng, bạn phải sử dụng các cơ chế bảo vệ đa luồng.

Lưu ý rằng một số kiểu được liệt kê ở đây cũng có sẵn thông qua các binding, nhưng các kiểu binding được bao bọc bởi
:ref:`class_RefCounted` (nằm trong namespace ``CoreBind::``). Khi có thể, hãy ưu tiên các primitive được liệt kê ở đây vì lý do hiệu năng.

+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| Kiểu dữ liệu Godot   | Kiểu dữ liệu C++ STL gần nhất | Nhận xét                                                                                                       |
+======================+===============================+================================================================================================================+
| |mutex|              | ``std::recursive_mutex``      | Kiểu mutex đệ quy. Sử dụng ``MutexLock lock(mutex)`` để khóa nó.                                               |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |binary_mutex|       | ``std::mutex``                | Kiểu mutex không đệ quy. Sử dụng ``MutexLock lock(mutex)`` để khóa nó.                                         |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |rw_lock|            | ``std::shared_mutex``         | Kiểu mutex hỗ trợ đọc-ghi. Sử dụng ``RWLockRead lock(mutex)`` hoặc ``RWLockWrite lock(mutex)`` để khóa nó.     |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |safe_binary_mutex|  | ``std::mutex``                | Kiểu mutex đệ quy có thể được sử dụng với ``ConditionVariable``. Sử dụng ``MutexLock lock(mutex)`` để khóa nó. |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |condition_variable| | ``std::condition_variable``   | Kiểu biến điều kiện, được sử dụng với ``SafeBinaryMutex``.                                                     |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |semaphore|          | ``std::counting_semaphore``   | Kiểu semaphore đếm.                                                                                            |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |safe_numeric|       | ``std::atomic``               | Kiểu atomic dạng template, được thiết kế cho các số.                                                           |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |safe_flag|          | ``std::atomic_bool``          | Kiểu atomic Bool.                                                                                              |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| |safe_ref_count|     | ``std::atomic``               | Kiểu atomic được thiết kế cho việc đếm tham chiếu. Sẽ từ chối tăng số lượng tham chiếu nếu giá trị đó là 0.    |
+----------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+

.. |mutex| replace:: `Mutex <https://github.com/godotengine/godot/blob/master/core/os/mutex.h>`__
.. |binary_mutex| replace:: `BinaryMutex <https://github.com/godotengine/godot/blob/master/core/os/mutex.h>`__
.. |rw_lock| replace:: `RWLock <https://github.com/godotengine/godot/blob/master/core/os/rw_lock.h>`__
.. |safe_binary_mutex| replace:: `SafeBinaryMutex <https://github.com/godotengine/godot/blob/master/core/os/safe_binary_mutex.h>`__
.. |condition_variable| replace:: `ConditionVariable <https://github.com/godotengine/godot/blob/master/core/os/condition_variable.h>`__
.. |semaphore| replace:: `Semaphore <https://github.com/godotengine/godot/blob/master/core/os/semaphore.h>`__
.. |safe_numeric| replace:: `SafeNumeric <https://github.com/godotengine/godot/blob/master/core/templates/safe_refcount.h>`__
.. |safe_flag| replace:: `SafeFlag <https://github.com/godotengine/godot/blob/master/core/templates/safe_refcount.h>`__
.. |safe_ref_count| replace:: `SafeRefCount <https://github.com/godotengine/godot/blob/master/core/templates/safe_refcount.h>`__

Các kiểu toán học
-----------------

Có một số kiểu toán tuyến tính trong thư mục ``core/math``:

-  `core/math <https://github.com/godotengine/godot/tree/master/core/math>`__

NodePath
--------

Đây là một kiểu dữ liệu đặc biệt dùng để lưu trữ các đường dẫn trong scene tree và tham chiếu đến chúng theo cách được tối ưu hóa:

-  `core/string/node_path.h <https://github.com/godotengine/godot/blob/master/core/string/node_path.h>`__

RID
---

RID là *ID Resource*. Các server sử dụng chúng để tham chiếu đến dữ liệu được lưu trữ trong đó. RID là các giá trị không trong suốt, nghĩa là không thể truy cập trực tiếp vào dữ liệu mà chúng tham chiếu. RID là duy nhất, ngay cả đối với các kiểu dữ liệu được tham chiếu khác nhau:

-  `core/templates/rid.h <https://github.com/godotengine/godot/blob/master/core/templates/rid.h>`__
