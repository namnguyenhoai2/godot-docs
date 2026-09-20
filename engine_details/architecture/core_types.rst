.. _doc_core_types:

Các kiểu cốt lõi
================

Godot có một tập hợp phong phú các lớp và mẫu tạo nên phần cốt lõi của nó, và mọi thứ đều được xây dựng dựa trên chúng.

Tài liệu tham chiếu này sẽ cố gắng liệt kê chúng theo thứ tự để dễ hiểu hơn.

Cấp phát bộ nhớ
---------------

Godot có nhiều cơ chế để đảm bảo an toàn bộ nhớ và theo dõi việc sử dụng bộ nhớ. Vì lý do này, không nên sử dụng các lệnh gọi thư viện C và C++ thông thường. Thay vào đó, một số hàm thay thế được cung cấp.

Để cấp phát theo kiểu C, Godot cung cấp một số macro:

.. code-block:: cpp

    memalloc(size)
    memrealloc(pointer)
    memfree(pointer)

Các macro này tương đương với ``malloc()``, ``realloc()`` và ``free()`` thông thường của thư viện chuẩn C.

Để cấp phát theo kiểu C++, các macro đặc biệt được cung cấp:

.. code-block:: cpp

    memnew(Class)
    memnew(Class(args))
    memdelete(instance)

    memnew_arr(Class, amount)
    memdelete_arr(pointer_to_array)

Các macro này lần lượt tương đương với ``new``, ``delete``, ``new[]`` và ``delete[]``.

``memnew``/``memdelete`` cũng sử dụng một chút phép thuật C++ để tự động gọi các hàm post-init và pre-release. Ví dụ, tính năng này được dùng để thông báo cho các Object ngay sau khi chúng được tạo và ngay trước khi chúng bị xóa.

-  `core/os/memory.h <https://github.com/godotengine/godot/blob/master/core/os/memory.h>`__

Các container
-------------

Godot cung cấp bộ container riêng, vì vậy các container STL như ``std::string`` và ``std::vector`` thường không được sử dụng trong cơ sở mã. Xem :ref:`doc_faq_why_not_stl` để biết thêm thông tin.

Biểu tượng 📜 cho biết kiểu này là một phần của :ref:`Variant <doc_variant_class>`. Điều này có nghĩa là nó có thể được sử dụng làm tham số hoặc giá trị trả về của một phương thức được cung cấp cho API scripting.

+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| Kiểu dữ liệu Godot | Kiểu dữ liệu C++ STL gần nhất | Chú thích |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |string| 📜 | ``std::string`` | **Hãy sử dụng kiểu này làm kiểu chuỗi "mặc định".** ``String`` sử dụng mã hóa UTF-32 |
| | | để đơn giản hóa việc xử lý nhờ kích thước ký tự cố định. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |vector| | ``std::vector`` | **Hãy sử dụng kiểu này làm kiểu vector "mặc định".** Sử dụng ngữ nghĩa copy-on-write (COW). | | | | Điều này có nghĩa là nó thường chậm hơn nhưng có thể được sao chép gần như miễn phí. |
| | | Thay vào đó, hãy sử dụng ``LocalVector`` khi không cần COW và hiệu năng là quan trọng. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |hash_set| | ``std::unordered_set`` | **Hãy sử dụng kiểu này làm kiểu set "mặc định".** |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |a_hash_map| | ``std::unordered_map`` | **Hãy sử dụng kiểu này làm kiểu map "mặc định".** Không bảo toàn thứ tự chèn. | | | | Lưu ý rằng các con trỏ trỏ vào map, cũng như các iterator, không ổn định khi có thay đổi.|
| | | Nếu cần một trong hai đặc tính này, hãy sử dụng ``HashMap`` thay thế. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |string_name| 📜 | ``std::string`` | Sử dụng string interning để so sánh nhanh. Hãy sử dụng kiểu này cho các chuỗi tĩnh được |
| | | tham chiếu thường xuyên và được sử dụng ở nhiều vị trí trong engine. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |local_vector| | ``std::vector`` | Có ngữ nghĩa gần với ``std::vector`` hơn, không sử dụng copy-on-write (COW), do đó | | | | nhanh hơn ``Vector``. Ưu tiên kiểu này thay cho ``Vector`` khi không cần |
| | | sao chép với chi phí thấp. |
++++++++++++++++++++++++++++++++++
| |array| 📜 | ``std::vector`` | Các giá trị có thể thuộc bất kỳ kiểu Variant nào. Không áp đặt kiểu tĩnh. | | | | Sử dụng đếm tham chiếu dùng chung, tương tự như ``std::shared_ptr``. |
| | | Sử dụng Vector<Variant> ở bên trong. |
++++++++++++++++++++++++++++++++++++++++++++
| |typed_array| 📜 | ``std::vector`` | Lớp con của ``Array`` nhưng có kiểu tĩnh cho các phần tử. |
| | | Không được nhầm lẫn với ``Packed*Array``, vốn là một ``Vector`` ở bên trong. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |packed_array| 📜 | ``std::vector`` | Bí danh của ``Vector``, ví dụ ``PackedColorArray = Vector<Color>``. | | | | Chỉ có một danh sách giới hạn các kiểu packed array khả dụng |
| | | (nếu không, hãy sử dụng ``TypedArray``). |
++++++++++++++++++++++++++++++++++++++++++++++++
| |list| | ``std::list`` | Kiểu danh sách liên kết. Thường chậm hơn các kiểu array/vector khác. Trong mã mới, hãy ưu tiên sử dụng |
| | | các kiểu khác, trừ khi việc sử dụng ``List`` giúp tránh nhu cầu chuyển đổi kiểu. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |fixed_vector| | ``std::array`` | Vector có dung lượng cố định (tương tự ``boost::container::static_vector`` hơn). | | | | Kiểu container này hiệu quả hơn các kiểu tương tự vector khác vì nó |
| | | không cấp phát trên heap. |
+++++++++++++++++++++++++++++++++
| |span| | ``std::span`` | Đại diện cho quyền truy cập chỉ đọc vào một mảng liên tục mà không cần sao chép dữ liệu. | | | | Lưu ý rằng ``Span`` được thiết kế như một API hiệu năng cao: Nó không thực hiện | | | | các kiểm tra tính đúng đắn của tham số theo cùng cách mà bạn có thể đã quen thuộc với các | | | | container khác của Godot. Hãy sử dụng cẩn thận. |
| | | `Span` có thể được tạo từ hầu hết các container dạng array (ví dụ: ``vector.span()``). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |rb_set| | ``std::set`` | Sử dụng `red-black tree <https://en.wikipedia.org/wiki/Red-black_tree>`__ |
| | | để truy cập nhanh hơn. |
++++++++++++++++++++++++++++++
| |v_set| | ``std::flat_set`` | Sử dụng ngữ nghĩa copy-on-write (COW). | | | | Điều này có nghĩa là nó thường chậm hơn nhưng có thể được sao chép gần như miễn phí. |
| | | Lợi ích hiệu năng của ``VSet`` chưa được xác lập, vì vậy hãy ưu tiên sử dụng các kiểu khác. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |hash_map| | ``std::unordered_map`` | Kiểu map phòng thủ (bền vững nhưng chậm). Bảo toàn thứ tự chèn. | | | | Các con trỏ đến khóa và giá trị, cũng như các iterator, vẫn ổn định khi có thay đổi. | | | | Hãy sử dụng kiểu map này khi cần một trong hai đặc tính đó. Nếu không, hãy sử dụng ``AHashMap`` |
| | | | nếu không. |
++++++++++++++++++++
| |rb_map| | ``std::map`` | Kiểu map sử dụng một | | | | `red-black tree <https://en.wikipedia.org/wiki/Red-black_tree>`__ để tìm khóa. |
| | | Lợi ích hiệu năng của ``RBMap`` chưa được xác lập, vì vậy hãy ưu tiên sử dụng các kiểu khác.|
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |dictionary| 📜 | ``std::unordered_map`` | Khóa và giá trị có thể thuộc bất kỳ kiểu Variant nào. Không áp đặt kiểu tĩnh. | | | | Sử dụng đếm tham chiếu dùng chung, tương tự như ``std::shared_ptr``. |
| | | Bảo toàn thứ tự chèn. Sử dụng ``HashMap<Variant>`` ở bên trong. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |typed_dictionary| 📜 | ``std::unordered_map`` | Lớp con của ``Dictionary`` nhưng có kiểu tĩnh cho các khóa và giá trị. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |pair| | ``std::pair`` | Lưu trữ một cặp đơn. Xem thêm ``KeyValue`` trong cùng tệp, sử dụng các khóa chỉ đọc |
| | | |
+++++++

.. |string| replace:: `String <https://github.com/godotengine/godot/blob/master/core/string/ustring.h>`__
.. |vector| replace:: `Vector <https://github.com/godotengine/godot/blob/master/core/templates/vector.h>`__
.. |hash_set| replace:: `HashSet <https://github.com/godotengine/godot/blob/master/core/templates/hash_set.h>`__
.. |hash_map| replace:: `HashMap <https://github.com/godotengine/godot/blob/master/core/templates/hash_map.h>`__
.. |string_name| replace:: `StringName <https://github.com/godotengine/godot/blob/master/core/string/string_name.h>`__
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

An toàn khi tái định vị
^^^^^^^^^^^^^^^^^^^^^^^

Các container của Godot giả định rằng các phần tử của chúng là `có thể tái định vị tầm thường <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html>`__.

Điều này có nghĩa là nếu bạn lưu trữ trong đó các kiểu dữ liệu có con trỏ trỏ đến chính chúng, hoặc nói cách khác là `không thể tái định vị tầm thường <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html#non-trivial-samples>`__, Godot có thể bị crash. Lưu ý rằng việc lưu trữ **con trỏ đến** các đối tượng không thể tái định vị tầm thường, chẳng hạn như một số lớp con của Object, là không có vấn đề và được hỗ trợ.

Lý do giả định khả năng tái định vị tầm thường là vì điều đó cho phép chúng ta sử dụng các kỹ thuật tối ưu hóa quan trọng, chẳng hạn như tái định vị bằng ``memcpy`` hoặc ``realloc``.

`GH-100509 <https://github.com/godotengine/godot/issues/100509>`__ theo dõi quyết định này.

.. _doc_core_concurrency_types:

Đa luồng / Đồng thời
--------------------

.. seealso::

    Bạn có thể tìm thêm thông tin về các chiến lược đa luồng tại :ref:`doc_using_multiple_threads`.

Không có container nào của Godot an toàn khi truy cập từ nhiều luồng. Khi dự kiến có nhiều luồng truy cập chúng, bạn phải sử dụng các cơ chế bảo vệ đa luồng.

Lưu ý rằng một số kiểu được liệt kê ở đây cũng khả dụng thông qua các binding, nhưng các kiểu binding được bọc vì
:ref:`class_RefCounted` (found in the ``CoreBind::`` namespace). Prefer the primitives listed here when possible, for
lý do hiệu năng.

+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| Kiểu dữ liệu Godot | Kiểu dữ liệu C++ STL gần nhất | Chú thích |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |mutex| | ``std::recursive_mutex`` | Kiểu mutex đệ quy. Sử dụng ``MutexLock lock(mutex)`` để khóa nó. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |binary_mutex| | ``std::mutex`` | Kiểu mutex không đệ quy. Sử dụng ``MutexLock lock(mutex)`` để khóa nó. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |rw_lock| | ``std::shared_mutex`` | Kiểu mutex nhận biết thao tác đọc-ghi. Sử dụng ``RWLockRead lock(mutex)`` hoặc |
| | | ``RWLockWrite lock(mutex)`` để khóa nó. |
+++++++++++++++++++++++++++++++++++++++++++++++
| |safe_binary_mutex| | ``std::mutex`` | Kiểu mutex đệ quy có thể sử dụng với ``ConditionVariable``. |
| | | Sử dụng ``MutexLock lock(mutex)`` để khóa nó. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++
| |condition_variable| | ``std::condition_variable`` | Kiểu biến điều kiện, được sử dụng với ``SafeBinaryMutex``. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |semaphore| | ``std::counting_semaphore`` | Kiểu semaphore đếm. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |safe_numeric| | ``std::atomic`` | Kiểu atomic dạng mẫu, được thiết kế cho các số. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |safe_flag| | ``std::atomic_bool`` | Kiểu atomic Bool. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| |safe_ref_count| | ``std::atomic`` | Kiểu atomic được thiết kế để đếm tham chiếu. Sẽ từ chối tăng bộ đếm |
| | | tham chiếu nếu giá trị của nó là 0. |
+++++++++++++++++++++++++++++++++++++++++++

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

Có một số kiểu toán học tuyến tính khả dụng trong thư mục ``core/math``:

-  `core/math <https://github.com/godotengine/godot/tree/master/core/math>`__

NodePath
--------

Đây là một kiểu dữ liệu đặc biệt dùng để lưu trữ các đường dẫn trong cây cảnh và tham chiếu đến chúng theo cách được tối ưu hóa:

-  `core/string/node_path.h <https://github.com/godotengine/godot/blob/master/core/string/node_path.h>`__

RID
---

RID là *Resource ID*. Các máy chủ sử dụng chúng để tham chiếu đến dữ liệu được lưu trữ trong đó. RID là kiểu mờ, nghĩa là không thể truy cập trực tiếp vào dữ liệu mà chúng tham chiếu. RID là duy nhất, ngay cả đối với các kiểu dữ liệu được tham chiếu khác nhau:

-  `core/templates/rid.h <https://github.com/godotengine/godot/blob/master/core/templates/rid.h>`__
