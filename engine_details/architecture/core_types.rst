.. _doc_core_types:

Các kiểu dữ liệu cốt lõi
========================

Godot có một tập hợp phong phú các lớp và template cấu thành phần cốt lõi của nó, và mọi thứ đều được xây dựng dựa trên chúng.

Tài liệu tham khảo này sẽ cố gắng liệt kê chúng theo thứ tự để dễ hiểu hơn.

Cấp phát bộ nhớ
---------------

Godot có nhiều cơ chế để đảm bảo an toàn bộ nhớ và theo dõi mức sử dụng bộ nhớ. Vì lý do này, không nên sử dụng các lệnh gọi thư viện C và C++ thông thường. Thay vào đó, một vài phương án thay thế được cung cấp.

Để cấp phát theo kiểu C, Godot cung cấp một vài macro:

.. code-block:: cpp

    memalloc(size)
    memrealloc(pointer)
    memfree(pointer)

Các macro này tương đương với ``malloc()``, ``realloc()`` và ``free()`` thường dùng của thư viện chuẩn C.

Để cấp phát theo kiểu C++, có các macro đặc biệt:

.. code-block:: cpp

    memnew(Class)
    memnew(Class(args))
    memdelete(instance)

    memnew_arr(Class, amount)
    memdelete_arr(pointer_to_array)

Các macro này lần lượt tương đương với ``new``, ``delete``, ``new[]`` và ``delete[]``.

``memnew``/``memdelete`` cũng sử dụng một chút phép màu C++ để tự động gọi các hàm post-init và pre-release. Ví dụ, cơ chế này được dùng để thông báo cho các Object ngay sau khi chúng được tạo và ngay trước khi chúng bị xóa.

-  `core/os/memory.h <https://github.com/godotengine/godot/blob/master/core/os/memory.h>`__

Container
---------

Godot cung cấp tập hợp container riêng, nghĩa là các container STL như ``std::string`` và ``std::vector`` nhìn chung không được sử dụng trong codebase. Xem :ref:`doc_faq_why_not_stl` để biết thêm thông tin.

Biểu tượng 📜 cho biết kiểu này là một phần của :ref:`Variant <doc_variant_class>`. Điều này có nghĩa là nó có thể được sử dụng làm tham số hoặc giá trị trả về của một method được expose cho scripting API.

+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| Godot datatype        | Closest C++ STL datatype | Comment                                                                               |
+=======================+==========================+=======================================================================================+
| |string| 📜           | ``std::string``          | **Use this as the "default" string type.** ``String`` uses UTF-32 encoding            |
|                       |                          | to simplify processing thanks to its fixed character size.                            |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |vector|              | ``std::vector``          | **Use this as the "default" vector type.** Uses copy-on-write (COW) semantics.        |
|                       |                          | This means it's generally slower but can be copied around almost for free.            |
|                       |                          | Use ``LocalVector`` instead where COW isn't needed and performance matters.           |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |hash_set|            | ``std::unordered_set``   | **Use this as the "default" set type.**                                               |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |a_hash_map|          | ``std::unordered_map``   | **Use this as the "default" map type.** Does not preserve insertion order.            |
|                       |                          | Note that pointers into the map, as well as iterators, are not stable under mutations.|
|                       |                          | If either of these affordances are needed, use ``HashMap`` instead.                   |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |string_name| 📜      | ``std::string``          | Uses string interning for fast comparisons. Use this for static strings that are      |
|                       |                          | referenced frequently and used in multiple locations in the engine.                   |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |char_string|,        | ``std::u8string``        | ``String``-likes that use ``char`` and ``char16_t``, respectively.                    |
| |char16_string|       | ``std::u16string``       | These are aliases of ``CharStringT<T>``; ``wchar_t`` and others are also supported.   |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |local_vector|        | ``std::vector``          | Closer to ``std::vector`` in semantics, doesn't use copy-on-write (COW) thus it's     |
|                       |                          | faster than ``Vector``. Prefer it over ``Vector`` when copying it cheaply             |
|                       |                          | is not needed.                                                                        |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |array| 📜            | ``std::vector``          | Values can be of any Variant type. No static typing is imposed.                       |
|                       |                          | Uses shared reference counting, similar to ``std::shared_ptr``.                       |
|                       |                          | Uses Vector<Variant> internally.                                                      |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |typed_array| 📜      | ``std::vector``          | Subclass of ``Array`` but with static typing for its elements.                        |
|                       |                          | Not to be confused with ``Packed*Array``, which is internally a ``Vector``.           |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |packed_array| 📜     | ``std::vector``          | Alias of ``Vector``, e.g. ``PackedColorArray = Vector<Color>``.                       |
|                       |                          | Only a limited list of packed array types are available                               |
|                       |                          | (use ``TypedArray`` otherwise).                                                       |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |list|                | ``std::list``            | Linked list type. Generally slower than other array/vector types. Prefer using        |
|                       |                          | other types in new code, unless using ``List`` avoids the need for type conversions.  |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |fixed_vector|        | ``std::array``           | Vector with a fixed capacity (more similar to ``boost::container::static_vector``).   |
|                       |                          | This container type is more efficient than other vector-like types because it makes   |
|                       |                          | no heap allocations.                                                                  |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |span|                | ``std::span``            | Represents read-only access to a contiguous array without needing to copy any data.   |
|                       |                          | Note that ``Span`` is designed to be a high performance API: It does not perform      |
|                       |                          | parameter correctness checks in the same way you might be used to with other Godot    |
|                       |                          | containers. Use with care.                                                            |
|                       |                          | ``Span`` can be constructed from most array-like containers (e.g. ``vector.span()``). |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |rb_set|              | ``std::set``             | Uses a `red-black tree <https://en.wikipedia.org/wiki/Red-black_tree>`__              |
|                       |                          | for faster access.                                                                    |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |v_set|               | ``std::flat_set``        | Uses copy-on-write (COW) semantics.                                                   |
|                       |                          | This means it's generally slower but can be copied around almost for free.            |
|                       |                          | The performance benefits of ``VSet`` aren't established, so prefer using other types. |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |hash_map|            | ``std::unordered_map``   | Defensive (robust but slow) map type. Preserves insertion order.                      |
|                       |                          | Pointers to keys and values, as well as iterators, are stable under mutation.         |
|                       |                          | Use this map type when either of these affordances are needed. Use ``AHashMap``       |
|                       |                          | otherwise.                                                                            |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |rb_map|              | ``std::map``             | Map type that uses a                                                                  |
|                       |                          | `red-black tree <https://en.wikipedia.org/wiki/Red-black_tree>`__ to find keys.       |
|                       |                          | The performance benefits of ``RBMap`` aren't established, so prefer using other types.|
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |dictionary| 📜       | ``std::unordered_map``   | Keys and values can be of any Variant type. No static typing is imposed.              |
|                       |                          | Uses shared reference counting, similar to ``std::shared_ptr``.                       |
|                       |                          | Preserves insertion order. Uses ``HashMap<Variant>`` internally.                      |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |typed_dictionary| 📜 | ``std::unordered_map``   | Subclass of ``Dictionary`` but with static typing for its keys and values.            |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+
| |pair|                | ``std::pair``            | Stores a single pair. See also ``KeyValue`` in the same file, which uses read-only    |
|                       |                          | keys.                                                                                 |
+-----------------------+--------------------------+---------------------------------------------------------------------------------------+

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

An toàn khi tái định vị
^^^^^^^^^^^^^^^^^^^^^^^

Các container của Godot giả định rằng các phần tử của chúng là `trivially relocatable <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html>`__.

Điều này có nghĩa là nếu bạn lưu trữ trong đó các kiểu dữ liệu có con trỏ trỏ đến chính chúng, hoặc theo cách khác là `not trivially relocatable <https://open-std.org/JTC1/SC22/WG21/docs/papers/2020/p1144r5.html#non-trivial-samples>`__, Godot có thể bị crash. Lưu ý rằng việc lưu trữ **con trỏ đến** các object không trivially relocatable, chẳng hạn như một số lớp con của Object, không gây vấn đề và được hỗ trợ.

Lý do giả định khả năng tái định vị tầm thường là vì điều đó cho phép chúng ta sử dụng các kỹ thuật tối ưu hóa quan trọng, chẳng hạn như tái định vị bằng ``memcpy`` hoặc ``realloc``.

`GH-100509 <https://github.com/godotengine/godot/issues/100509>`__ theo dõi quyết định này.

.. _doc_core_concurrency_types:

Đa luồng / Đồng thời
--------------------

.. seealso::

    Bạn có thể tìm thêm thông tin về các chiến lược đa luồng tại :ref:`doc_using_multiple_threads`.

Không container nào của Godot là thread-safe. Khi dự kiến có nhiều thread truy cập chúng, bạn phải sử dụng các cơ chế bảo vệ đa luồng.

Lưu ý rằng một số kiểu được liệt kê ở đây cũng có sẵn thông qua bindings, nhưng các kiểu binding được bọc bằng
:ref:`class_RefCounted` (found in the ``CoreBind::`` namespace). Prefer the primitives listed here when possible, for
vì lý do hiệu suất.

+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| Godot datatype        | Closest C++ STL datatype     | Comment                                                                               |
+=======================+==============================+=======================================================================================+
| |mutex|               | ``std::recursive_mutex``     | Recursive mutex type. Use ``MutexLock lock(mutex)`` to lock it.                       |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |binary_mutex|        | ``std::mutex``               | Non-recursive mutex type. Use ``MutexLock lock(mutex)`` to lock it.                   |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |rw_lock|             | ``std::shared_mutex``        | Read-write aware mutex type. Use ``RWLockRead lock(mutex)`` or                        |
|                       |                              | ``RWLockWrite lock(mutex)`` to lock it.                                               |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |safe_binary_mutex|   | ``std::mutex``               | Recursive mutex type that can be used with ``ConditionVariable``.                     |
|                       |                              | Use ``MutexLock lock(mutex)`` to lock it.                                             |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |condition_variable|  | ``std::condition_variable``  | Condition variable type, used with ``SafeBinaryMutex``.                               |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |semaphore|           | ``std::counting_semaphore``  | Counting semaphore type.                                                              |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |safe_numeric|        | ``std::atomic``              | Templated atomic type, designed for numbers.                                          |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |safe_flag|           | ``std::atomic_bool``         | Bool atomic type.                                                                     |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+
| |safe_ref_count|      | ``std::atomic``              | Atomic type designed for reference counting. Will refuse to increment the             |
|                       |                              | reference count if it is 0.                                                           |
+-----------------------+------------------------------+---------------------------------------------------------------------------------------+

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

Có một số kiểu toán học tuyến tính có sẵn trong thư mục ``core/math``:

-  `core/math <https://github.com/godotengine/godot/tree/master/core/math>`__

NodePath
--------

Đây là một kiểu dữ liệu đặc biệt dùng để lưu trữ các path trong scene tree và tham chiếu đến chúng theo cách được tối ưu hóa:

-  `core/string/node_path.h <https://github.com/godotengine/godot/blob/master/core/string/node_path.h>`__

RID
---

RID là *Resource ID*. Các server sử dụng chúng để tham chiếu đến dữ liệu được lưu trữ trong đó. RID là opaque, nghĩa là không thể truy cập trực tiếp vào dữ liệu mà chúng tham chiếu. RID là duy nhất, kể cả đối với các kiểu dữ liệu được tham chiếu khác nhau:

-  `core/templates/rid.h <https://github.com/godotengine/godot/blob/master/core/templates/rid.h>`__
