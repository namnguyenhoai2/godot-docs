:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Array.xml.

.. _class_Array:

Array
=====

Một cấu trúc dữ liệu tích hợp sẵn chứa một chuỗi phần tử.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một cấu trúc dữ liệu array có thể chứa một chuỗi phần tử thuộc bất kỳ kiểu :ref:`Variant<class_Variant>` nào theo mặc định. Các giá trị có thể được giới hạn tùy chọn ở một kiểu cụ thể bằng cách tạo một *typed array*. Các phần tử được truy cập bằng chỉ mục số bắt đầu từ ``0``. Chỉ mục âm được dùng để đếm từ cuối ( ``-1`` là phần tử cuối cùng, ``-2`` là phần tử áp chót, v.v.).


.. tabs::

 .. code-tab:: gdscript

    var array = ["First", 2, 3, "Last"]
    print(array[0])  # In ra "First"
    print(array[2])  # In ra 3
    print(array[-1]) # In ra "Last"

    array[1] = "Second"
    print(array[1])  # In ra "Second"
    print(array[-3]) # In ra "Second"

    # Typed array này chỉ có thể chứa các số nguyên.
    # Việc cố gắng thêm bất kỳ kiểu nào khác sẽ dẫn đến lỗi.
    var typed_array: Array[int] = [1, 2, 3]

 .. code-tab:: csharp

    Godot.Collections.Array array = ["First", 2, 3, "Last"];
    GD.Print(array[0]); // In ra "First"
    GD.Print(array[2]); // In ra 3
    GD.Print(array[^1]); // In ra "Last"

    array[1] = "Second";
    GD.Print(array[1]); // In ra "Second"
    GD.Print(array[^3]); // In ra "Second"

    // Typed array này chỉ có thể chứa các số nguyên.
    // Việc cố gắng thêm bất kỳ kiểu nào khác sẽ dẫn đến lỗi.
    Godot.Collections.Array<int> typedArray = [1, 2, 3];



\ **Lưu ý:** Array luôn được truyền theo **tham chiếu**. Để lấy một bản sao của array có thể được chỉnh sửa độc lập với array ban đầu, hãy sử dụng :ref:`duplicate()<class_Array_method_duplicate>`.

\ **Lưu ý:** Không hỗ trợ xóa các phần tử trong khi đang lặp qua array và việc này sẽ dẫn đến hành vi không thể dự đoán.

\ **Lưu ý:** Trong ngữ cảnh boolean, một array sẽ được đánh giá là ``false`` nếu nó rỗng (``[]``). Nếu không, array sẽ luôn được đánh giá là ``true``.

\ **Sự khác biệt giữa packed array, typed array và untyped array:** Packed array nhìn chung có tốc độ lặp và chỉnh sửa nhanh hơn typed array cùng kiểu (ví dụ: :ref:`PackedInt64Array<class_PackedInt64Array>` so với ``Array[int]``). Packed array cũng sử dụng ít bộ nhớ hơn. Nhược điểm là packed array kém linh hoạt hơn vì không cung cấp nhiều phương thức tiện ích như :ref:`map()<class_Array_method_map>`. Đổi lại, typed array có tốc độ lặp và chỉnh sửa nhanh hơn untyped array.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-reftable-group

Constructors
------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ )                                                                                                                                                           |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ base\: :ref:`Array<class_Array>`, type\: :ref:`int<class_int>`, class_name\: :ref:`StringName<class_StringName>`, script\: :ref:`Variant<class_Variant>`\ ) |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`Array<class_Array>`\ )                                                                                                                         |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                     |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedColorArray<class_PackedColorArray>`\ )                                                                                                   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )                                                                                               |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`\ )                                                                                               |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )                                                                                                   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedInt64Array<class_PackedInt64Array>`\ )                                                                                                   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedStringArray<class_PackedStringArray>`\ )                                                                                                 |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                               |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ )                                                                                               |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`Array<class_Array_constructor_Array>`\ (\ from\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )                                                                                               |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`all<class_Array_method_all>`\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const|                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`any<class_Array_method_any>`\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const|                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`append<class_Array_method_append>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                                                                                   |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`append_array<class_Array_method_append_array>`\ (\ array\: :ref:`Array<class_Array>`\ )                                                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`assign<class_Array_method_assign>`\ (\ array\: :ref:`Array<class_Array>`\ )                                                                                                                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`back<class_Array_method_back>`\ (\ ) |const|                                                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`bsearch<class_Array_method_bsearch>`\ (\ value\: :ref:`Variant<class_Variant>`, before\: :ref:`bool<class_bool>` = true\ ) |const|                                                                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`bsearch_custom<class_Array_method_bsearch_custom>`\ (\ value\: :ref:`Variant<class_Variant>`, func\: :ref:`Callable<class_Callable>`, before\: :ref:`bool<class_bool>` = true\ ) |const|          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`clear<class_Array_method_clear>`\ (\ )                                                                                                                                                            |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`count<class_Array_method_count>`\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const|                                                                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`duplicate<class_Array_method_duplicate>`\ (\ deep\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`duplicate_deep<class_Array_method_duplicate_deep>`\ (\ deep_subresources_mode\: :ref:`int<class_int>` = 1\ ) |const|                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`erase<class_Array_method_erase>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                                                                                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`fill<class_Array_method_fill>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                                                                                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`filter<class_Array_method_filter>`\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const|                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`find<class_Array_method_find>`\ (\ what\: :ref:`Variant<class_Variant>`, from\: :ref:`int<class_int>` = 0\ ) |const|                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`find_custom<class_Array_method_find_custom>`\ (\ method\: :ref:`Callable<class_Callable>`, from\: :ref:`int<class_int>` = 0\ ) |const|                                                            |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`front<class_Array_method_front>`\ (\ ) |const|                                                                                                                                                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get<class_Array_method_get>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                         |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_typed_builtin<class_Array_method_get_typed_builtin>`\ (\ ) |const|                                                                                                                            |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_typed_class_name<class_Array_method_get_typed_class_name>`\ (\ ) |const|                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get_typed_script<class_Array_method_get_typed_script>`\ (\ ) |const|                                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`has<class_Array_method_has>`\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const|                                                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`hash<class_Array_method_hash>`\ (\ ) |const|                                                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`insert<class_Array_method_insert>`\ (\ position\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_empty<class_Array_method_is_empty>`\ (\ ) |const|                                                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_read_only<class_Array_method_is_read_only>`\ (\ ) |const|                                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_same_typed<class_Array_method_is_same_typed>`\ (\ array\: :ref:`Array<class_Array>`\ ) |const|                                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_typed<class_Array_method_is_typed>`\ (\ ) |const|                                                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`make_read_only<class_Array_method_make_read_only>`\ (\ )                                                                                                                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`map<class_Array_method_map>`\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const|                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`max<class_Array_method_max>`\ (\ ) |const|                                                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`min<class_Array_method_min>`\ (\ ) |const|                                                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`pick_random<class_Array_method_pick_random>`\ (\ ) |const|                                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`pop_at<class_Array_method_pop_at>`\ (\ position\: :ref:`int<class_int>`\ )                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`pop_back<class_Array_method_pop_back>`\ (\ )                                                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`pop_front<class_Array_method_pop_front>`\ (\ )                                                                                                                                                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`push_back<class_Array_method_push_back>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                                                                             |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`push_front<class_Array_method_push_front>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`reduce<class_Array_method_reduce>`\ (\ method\: :ref:`Callable<class_Callable>`, accum\: :ref:`Variant<class_Variant>` = null\ ) |const|                                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`remove_at<class_Array_method_remove_at>`\ (\ position\: :ref:`int<class_int>`\ )                                                                                                                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`resize<class_Array_method_resize>`\ (\ size\: :ref:`int<class_int>`\ )                                                                                                                            |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`reverse<class_Array_method_reverse>`\ (\ )                                                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`rfind<class_Array_method_rfind>`\ (\ what\: :ref:`Variant<class_Variant>`, from\: :ref:`int<class_int>` = -1\ ) |const|                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`rfind_custom<class_Array_method_rfind_custom>`\ (\ method\: :ref:`Callable<class_Callable>`, from\: :ref:`int<class_int>` = -1\ ) |const|                                                         |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set<class_Array_method_set>`\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`shuffle<class_Array_method_shuffle>`\ (\ )                                                                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`size<class_Array_method_size>`\ (\ ) |const|                                                                                                                                                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`slice<class_Array_method_slice>`\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647, step\: :ref:`int<class_int>` = 1, deep\: :ref:`bool<class_bool>` = false\ ) |const| |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`sort<class_Array_method_sort>`\ (\ )                                                                                                                                                              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`sort_custom<class_Array_method_sort_custom>`\ (\ func\: :ref:`Callable<class_Callable>`\ )                                                                                                        |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Operators
---------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator !=<class_Array_operator_neq_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )  |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`     | :ref:`operator +<class_Array_operator_sum_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )   |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator \<<class_Array_operator_lt_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )   |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator \<=<class_Array_operator_lte_Array>`\ (\ right\: :ref:`Array<class_Array>`\ ) |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator ==<class_Array_operator_eq_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )   |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator ><class_Array_operator_gt_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )    |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator >=<class_Array_operator_gte_Array>`\ (\ right\: :ref:`Array<class_Array>`\ )  |
   +-------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`operator []<class_Array_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )        |
   +-------------------------------+----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả constructor
-----------------

.. _class_Array_constructor_Array:

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ ) :ref:`🔗<class_Array_constructor_Array>`

Tạo một **Array** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ base\: :ref:`Array<class_Array>`, type\: :ref:`int<class_int>`, class_name\: :ref:`StringName<class_StringName>`, script\: :ref:`Variant<class_Variant>`\ )

Tạo một typed array từ array ``base``. Typed array chỉ có thể chứa các phần tử thuộc kiểu đã cho hoặc kế thừa từ class đã cho, như được mô tả bởi các tham số của constructor này:

- ``type`` là kiểu :ref:`Variant<class_Variant>` tích hợp sẵn, dưới dạng một trong các hằng số :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`.

- ``class_name`` là tên class tích hợp sẵn (xem :ref:`Object.get_class()<class_Object_method_get_class>`).

- ``script`` là script liên kết. Nó phải là một instance :ref:`Script<class_Script>` hoặc ``null``.

Nếu ``type`` không phải là :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>`, ``class_name`` phải là một :ref:`StringName<class_StringName>` rỗng và ``script`` phải là ``null``.

::

    class_name Sword
    extends Node

    class Stats:
        pass

    func _ready():
        var a = Array([], TYPE_INT, "", null)               # Array[int]
        var b = Array([], TYPE_OBJECT, "Node", null)        # Array[Node]
        var c = Array([], TYPE_OBJECT, "Node", Sword)       # Array[Sword]
        var d = Array([], TYPE_OBJECT, "RefCounted", Stats) # Array[Stats]

Các phần tử của array ``base`` sẽ được chuyển đổi khi cần thiết. Nếu không thể thực hiện việc này hoặc ``base`` đã được định kiểu, constructor này sẽ thất bại và trả về một **Array** rỗng.

Trong GDScript, constructor này thường không cần thiết vì có thể tạo typed array thông qua static typing:

::

    var numbers: Array[float] = []
    var children: Array[Node] = [$Node, $Sprite2D, $RigidBody3D]

    var integers: Array[int] = [0.2, 4.5, -2.0]
    print(integers) # In ra [0, 4, -2]

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`Array<class_Array>`\ )

Trả về cùng array như ``from``. Nếu cần một bản sao của array, hãy sử dụng :ref:`duplicate()<class_Array_method_duplicate>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedByteArray<class_PackedByteArray>`\ )

Tạo một array từ :ref:`PackedByteArray<class_PackedByteArray>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedColorArray<class_PackedColorArray>`\ )

Tạo một array từ :ref:`PackedColorArray<class_PackedColorArray>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )

Tạo một array từ :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedFloat64Array<class_PackedFloat64Array>`\ )

Tạo một array từ :ref:`PackedFloat64Array<class_PackedFloat64Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )

Tạo một array từ :ref:`PackedInt32Array<class_PackedInt32Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedInt64Array<class_PackedInt64Array>`\ )

Tạo một array từ :ref:`PackedInt64Array<class_PackedInt64Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedStringArray<class_PackedStringArray>`\ )

Tạo một array từ :ref:`PackedStringArray<class_PackedStringArray>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )

Tạo một array từ :ref:`PackedVector2Array<class_PackedVector2Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ )

Tạo một array từ :ref:`PackedVector3Array<class_PackedVector3Array>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Array<class_Array>` **Array**\ (\ from\: :ref:`PackedVector4Array<class_PackedVector4Array>`\ )

Tạo một array từ :ref:`PackedVector4Array<class_PackedVector4Array>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_Array_method_all:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **all**\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const| :ref:`🔗<class_Array_method_all>`

Gọi :ref:`Callable<class_Callable>` đã cho trên từng phần tử trong array và trả về ``true`` nếu :ref:`Callable<class_Callable>` trả về ``true`` cho *tất cả* các phần tử trong array. Nếu :ref:`Callable<class_Callable>` trả về ``false`` cho một hoặc nhiều phần tử của array, method này trả về ``false``.

``method`` phải nhận một tham số :ref:`Variant<class_Variant>` (phần tử hiện tại của array) và trả về một :ref:`bool<class_bool>`.


.. tabs::

 .. code-tab:: gdscript

    func greater_than_5(number):
        return number > 5

    func _ready():
        print([6, 10, 6].all(greater_than_5)) # In ra true (3/3 phần tử được đánh giá là true).
        print([4, 10, 4].all(greater_than_5)) # In ra false (1/3 phần tử được đánh giá là true).
        print([4, 4, 4].all(greater_than_5))  # In ra false (0/3 phần tử được đánh giá là true).
        print([].all(greater_than_5))         # In ra true (0/0 phần tử được đánh giá là true).

        # Tương tự dòng đầu tiên ở trên, nhưng sử dụng một hàm lambda.
        print([6, 10, 6].all(func(element): return element > 5)) # In ra true

 .. code-tab:: csharp

    private static bool GreaterThan5(int number)
    {
        return number > 5;
    }

    public override void _Ready()
    {
        // In ra True (3/3 phần tử được đánh giá là true).
        GD.Print(new Godot.Collections.Array<int> { 6, 10, 6 }.All(GreaterThan5));
        // In ra False (1/3 phần tử được đánh giá là true).
        GD.Print(new Godot.Collections.Array<int> { 4, 10, 4 }.All(GreaterThan5));
        // In ra False (0/3 phần tử được đánh giá là true).
        GD.Print(new Godot.Collections.Array<int> { 4, 4, 4 }.All(GreaterThan5));
        // In ra True (0/0 phần tử được đánh giá là true).
        GD.Print(new Godot.Collections.Array<int> { }.All(GreaterThan5));

        // Tương tự dòng đầu tiên ở trên, nhưng sử dụng một hàm lambda.
        GD.Print(new Godot.Collections.Array<int> { 6, 10, 6 }.All(element => element > 5)); // In ra True
    }



Xem thêm :ref:`any()<class_Array_method_any>`, :ref:`filter()<class_Array_method_filter>`, :ref:`map()<class_Array_method_map>` và :ref:`reduce()<class_Array_method_reduce>`.

\ **Lưu ý:** Không giống như việc dựa vào kích thước của array được trả về bởi :ref:`filter()<class_Array_method_filter>`, method này sẽ trả về sớm nhất có thể để cải thiện hiệu suất (đặc biệt với các array lớn).

\ **Lưu ý:** Với một array rỗng, method này `always <https://en.wikipedia.org/wiki/Vacuous_truth>`__ trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_any:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **any**\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const| :ref:`🔗<class_Array_method_any>`

Gọi :ref:`Callable<class_Callable>` đã cho trên từng phần tử trong array và trả về ``true`` nếu :ref:`Callable<class_Callable>` trả về ``true`` cho *một hoặc nhiều* phần tử trong array. Nếu :ref:`Callable<class_Callable>` trả về ``false`` cho tất cả các phần tử trong array, method này trả về ``false``.

``method`` phải nhận một tham số :ref:`Variant<class_Variant>` (phần tử hiện tại của array) và trả về một :ref:`bool<class_bool>`.

::

    func greater_than_5(number):
        return number > 5

    func _ready():
        print([6, 10, 6].any(greater_than_5)) # In ra true (3 phần tử được đánh giá là true).
        print([4, 10, 4].any(greater_than_5)) # In ra true (1 phần tử được đánh giá là true).
        print([4, 4, 4].any(greater_than_5))  # In ra false (0 phần tử được đánh giá là true).
        print([].any(greater_than_5))         # In ra false (0 phần tử được đánh giá là true).

        # Tương tự dòng đầu tiên ở trên, nhưng sử dụng một hàm lambda.
        print([6, 10, 6].any(func(number): return number > 5)) # In ra true

Xem thêm :ref:`all()<class_Array_method_all>`, :ref:`filter()<class_Array_method_filter>`, :ref:`map()<class_Array_method_map>` và :ref:`reduce()<class_Array_method_reduce>`.

\ **Lưu ý:** Không giống như việc dựa vào kích thước của array được trả về bởi :ref:`filter()<class_Array_method_filter>`, method này sẽ trả về sớm nhất có thể để cải thiện hiệu suất (đặc biệt với các array lớn).

\ **Lưu ý:** Với một array rỗng, method này luôn trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_append:

.. rst-class:: classref-method

|void| **append**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_append>`

Thêm ``value`` vào cuối array (bí danh của :ref:`push_back()<class_Array_method_push_back>`).

.. rst-class:: classref-item-separator

----

.. _class_Array_method_append_array:

.. rst-class:: classref-method

|void| **append_array**\ (\ array\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_method_append_array>`

Thêm một ``array`` khác vào cuối array này.

::

    var numbers = [1, 2, 3]
    var extra = [4, 5, 6]
    numbers.append_array(extra)
    print(numbers) # In ra [1, 2, 3, 4, 5, 6]

.. rst-class:: classref-item-separator

----

.. _class_Array_method_assign:

.. rst-class:: classref-method

|void| **assign**\ (\ array\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_method_assign>`

Gán các phần tử của một ``array`` khác vào array. Thay đổi kích thước array để khớp với ``array``. Thực hiện chuyển đổi kiểu nếu array đã được định kiểu.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_back:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **back**\ (\ ) |const| :ref:`🔗<class_Array_method_back>`

Trả về phần tử cuối cùng của array. Nếu array rỗng, thao tác sẽ thất bại và trả về ``null``. Xem thêm :ref:`front()<class_Array_method_front>`.

\ **Lưu ý:** Không giống toán tử ``[]`` (``array[-1]``), một lỗi sẽ được tạo ra mà không dừng quá trình thực thi project.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_bsearch:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch**\ (\ value\: :ref:`Variant<class_Variant>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Array_method_bsearch>`

Trả về chỉ mục của ``value`` trong array đã sắp xếp. Nếu không tìm thấy, trả về vị trí cần chèn ``value`` để giữ cho array được sắp xếp. Thuật toán được sử dụng là `binary search <https://en.wikipedia.org/wiki/Binary_search_algorithm>`__.

Nếu ``before`` là ``true`` (theo mặc định), chỉ mục được trả về sẽ đứng trước tất cả các phần tử hiện có bằng ``value`` trong array.

::

    var numbers = [2, 4, 8, 10]
    var idx = numbers.bsearch(7)

    numbers.insert(idx, 7)
    print(numbers) # In ra [2, 4, 7, 8, 10]

    var fruits = ["Apple", "Lemon", "Lemon", "Orange"]
    print(fruits.bsearch("Lemon", true))  # In ra 1, trỏ đến "Lemon" đầu tiên.
    print(fruits.bsearch("Lemon", false)) # In ra 3, trỏ đến "Orange".

\ **Lưu ý:** Gọi :ref:`bsearch()<class_Array_method_bsearch>` trên một array *chưa được sắp xếp* sẽ dẫn đến hành vi không mong muốn. Hãy sử dụng :ref:`sort()<class_Array_method_sort>` trước khi gọi method này.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_bsearch_custom:

.. rst-class:: classref-method

:ref:`int<class_int>` **bsearch_custom**\ (\ value\: :ref:`Variant<class_Variant>`, func\: :ref:`Callable<class_Callable>`, before\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Array_method_bsearch_custom>`

Trả về chỉ mục của ``value`` trong mảng đã sắp xếp. Nếu không tìm thấy, trả về vị trí ``value`` nên được chèn vào để giữ cho mảng được sắp xếp (sử dụng ``func`` để so sánh). Thuật toán được sử dụng là `binary search <https://en.wikipedia.org/wiki/Binary_search_algorithm>`__.

Tương tự :ref:`sort_custom()<class_Array_method_sort_custom>`, ``func`` được gọi nhiều lần nếu cần, nhận một phần tử mảng và ``value`` làm các đối số. Hàm phải trả về ``true`` nếu phần tử mảng nên nằm *sau* ``value``, nếu không phải trả về ``false``.

Nếu ``before`` là ``true`` (như mặc định), chỉ mục được trả về nằm trước tất cả các phần tử hiện có trong mảng bằng ``value``.

::

    func sort_by_amount(a, b):
        if a[1] < b[1]:
            return true
        return false

    func _ready():
        var my_items = [["Tomato", 2], ["Kiwi", 5], ["Rice", 9]]

        var apple = ["Apple", 5]
        # "Apple" được chèn trước "Kiwi".
        my_items.insert(my_items.bsearch_custom(apple, sort_by_amount, true), apple)

        var banana = ["Banana", 5]
        # "Banana" được chèn sau "Kiwi".
        my_items.insert(my_items.bsearch_custom(banana, sort_by_amount, false), banana)

        # In ra [["Tomato", 2], ["Apple", 5], ["Kiwi", 5], ["Banana", 5], ["Rice", 9]]
        print(my_items)

\ **Lưu ý:** Gọi :ref:`bsearch_custom()<class_Array_method_bsearch_custom>` trên một mảng *chưa sắp xếp* sẽ dẫn đến hành vi không mong muốn. Hãy sử dụng :ref:`sort_custom()<class_Array_method_sort_custom>` với ``func`` trước khi gọi phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_Array_method_clear>`

Xóa tất cả phần tử khỏi mảng. Tương đương với việc sử dụng :ref:`resize()<class_Array_method_resize>` với kích thước là ``0``.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **count**\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const| :ref:`🔗<class_Array_method_count>`

Trả về số lần một phần tử xuất hiện trong mảng.

Để đếm số phần tử trong mảng thỏa mãn một điều kiện, hãy xem :ref:`reduce()<class_Array_method_reduce>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_duplicate:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **duplicate**\ (\ deep\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Array_method_duplicate>`

Trả về một bản sao mới của mảng.

Theo mặc định, một bản sao **nông** được trả về: tất cả các phần tử **Array**, :ref:`Dictionary<class_Dictionary>` và :ref:`Resource<class_Resource>` lồng nhau được dùng chung với mảng gốc. Việc sửa đổi bất kỳ phần tử nào trong số đó ở một mảng cũng sẽ ảnh hưởng đến mảng còn lại.

Nếu ``deep`` là ``true``, một bản sao **sâu** được trả về: tất cả các mảng và dictionary lồng nhau cũng được sao chép (đệ quy). Tuy nhiên, mọi :ref:`Resource<class_Resource>` vẫn được dùng chung với mảng gốc.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_duplicate_deep:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **duplicate_deep**\ (\ deep_subresources_mode\: :ref:`int<class_int>` = 1\ ) |const| :ref:`🔗<class_Array_method_duplicate_deep>`

Sao chép sâu mảng này, giống như :ref:`duplicate()<class_Array_method_duplicate>` khi truyền ``true``, với quyền kiểm soát bổ sung về cách xử lý các subresource.

\ ``deep_subresources_mode`` phải là một trong các giá trị của :ref:`DeepDuplicateMode<enum_Resource_DeepDuplicateMode>`. Theo mặc định, chỉ các resource nội bộ mới được sao chép (đệ quy).

.. rst-class:: classref-item-separator

----

.. _class_Array_method_erase:

.. rst-class:: classref-method

|void| **erase**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_erase>`

Tìm và xóa lần xuất hiện đầu tiên của ``value`` khỏi mảng. Nếu ``value`` không tồn tại trong mảng, không có gì xảy ra. Để xóa một phần tử theo chỉ mục, hãy sử dụng :ref:`remove_at()<class_Array_method_remove_at>`.

\ **Lưu ý:** Phương thức này dịch chỉ mục của mọi phần tử sau ``value`` lùi lại, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn hơn.

\ **Lưu ý:** Không hỗ trợ xóa phần tử trong khi đang lặp qua mảng và sẽ dẫn đến hành vi không xác định.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_fill:

.. rst-class:: classref-method

|void| **fill**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_fill>`

Gán ``value`` đã cho cho tất cả phần tử trong mảng.

Phương thức này thường có thể được kết hợp với :ref:`resize()<class_Array_method_resize>` để tạo một mảng có kích thước cho trước và các phần tử đã được khởi tạo:


.. tabs::

 .. code-tab:: gdscript

    var array = []
    array.resize(5)
    array.fill(2)
    print(array) # In ra [2, 2, 2, 2, 2]

 .. code-tab:: csharp

    Godot.Collections.Array array = [];
    array.Resize(5);
    array.Fill(2);
    GD.Print(array); // In ra [2, 2, 2, 2, 2]



\ **Note:** If ``value`` is a :ref:`Variant<class_Variant>` passed by reference (:ref:`Object<class_Object>`-derived, **Array**, :ref:`Dictionary<class_Dictionary>`, etc.), the array will be filled with references to the same ``value``, which are not duplicates.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_filter:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **filter**\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const| :ref:`🔗<class_Array_method_filter>`

Gọi :ref:`Callable<class_Callable>` đã cho trên từng phần tử trong mảng và trả về một **Array** mới đã được lọc.

``method`` nhận một trong các phần tử của mảng làm đối số và phải trả về ``true`` để thêm phần tử vào mảng đã lọc, hoặc ``false`` để loại trừ phần tử đó.

::

    func is_even(number):
        return number % 2 == 0

    func _ready():
        print([1, 4, 5, 8].filter(is_even)) # In ra [4, 8]

        # Tương tự như trên, nhưng sử dụng hàm lambda.
        print([1, 4, 5, 8].filter(func(number): return number % 2 == 0))

Xem thêm :ref:`any()<class_Array_method_any>`, :ref:`all()<class_Array_method_all>`, :ref:`map()<class_Array_method_map>` và :ref:`reduce()<class_Array_method_reduce>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_find:

.. rst-class:: classref-method

:ref:`int<class_int>` **find**\ (\ what\: :ref:`Variant<class_Variant>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_Array_method_find>`

Trả về chỉ mục của lần xuất hiện **đầu tiên** của ``what`` trong mảng này, hoặc ``-1`` nếu không có. Có thể chỉ định vị trí bắt đầu tìm kiếm bằng ``from``, sau đó tiếp tục đến cuối mảng.

\ **Lưu ý:** Nếu bạn chỉ muốn biết mảng có chứa ``what`` hay không, hãy sử dụng :ref:`has()<class_Array_method_has>` (``Contains`` trong C#). Trong GDScript, bạn cũng có thể sử dụng toán tử ``in``.

\ **Note:** For performance reasons, the search is affected by ``what``'s :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`. For example, ``7`` (:ref:`int<class_int>`) and ``7.0`` (:ref:`float<class_float>`) are not considered equal for this method.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_find_custom:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_custom**\ (\ method\: :ref:`Callable<class_Callable>`, from\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_Array_method_find_custom>`

Trả về chỉ mục của **phần tử đầu tiên** trong mảng khiến ``method`` trả về ``true``, hoặc ``-1`` nếu không có. Có thể chỉ định vị trí bắt đầu tìm kiếm bằng ``from``, sau đó tiếp tục đến cuối mảng.

\ ``method`` là một callable nhận một phần tử của mảng và trả về một :ref:`bool<class_bool>`.

\ **Lưu ý:** Nếu bạn chỉ muốn biết mảng có chứa *bất kỳ phần tử nào* thỏa mãn ``method`` hay không, hãy sử dụng :ref:`any()<class_Array_method_any>`.


.. tabs::

 .. code-tab:: gdscript

    func is_even(number):
        return number % 2 == 0

    func _ready():
        print([1, 3, 4, 7].find_custom(is_even.bind())) # In ra 2

    # Một ví dụ khác sử dụng `bind()` để truyền thêm một tham số:
    func is_specific_number(number, expected):
        return number == expected

    func _ready():
        print([1, 3, 4, 7].find_custom(is_specific_number.bind(4))) # In ra 2



.. rst-class:: classref-item-separator

----

.. _class_Array_method_front:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **front**\ (\ ) |const| :ref:`🔗<class_Array_method_front>`

Trả về phần tử đầu tiên của mảng. Nếu mảng rỗng, phương thức sẽ thất bại và trả về ``null``. Xem thêm :ref:`back()<class_Array_method_back>`.

\ **Lưu ý:** Không giống toán tử ``[]`` (``array[0]``), một lỗi được tạo ra nhưng không dừng việc thực thi project.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_get:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Array_method_get>`

Trả về phần tử tại ``index`` đã cho trong mảng. Nếu ``index`` nằm ngoài phạm vi hoặc là số âm, phương thức này sẽ thất bại và trả về ``null``.

Phương thức này tương tự (nhưng không giống hệt) toán tử ``[]``. Đáng chú ý nhất là khi phương thức này thất bại, nó không tạm dừng việc thực thi project nếu được chạy từ editor.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_get_typed_builtin:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_typed_builtin**\ (\ ) |const| :ref:`🔗<class_Array_method_get_typed_builtin>`

Trả về kiểu :ref:`Variant<class_Variant>` tích hợp sẵn của typed array dưới dạng hằng số :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`. Nếu mảng không có kiểu, trả về :ref:`@GlobalScope.TYPE_NIL<class_@GlobalScope_constant_TYPE_NIL>`. Xem thêm :ref:`is_typed()<class_Array_method_is_typed>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_get_typed_class_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_typed_class_name**\ (\ ) |const| :ref:`🔗<class_Array_method_get_typed_class_name>`

Trả về tên class **tích hợp sẵn** của typed array, nếu kiểu :ref:`Variant<class_Variant>` tích hợp sẵn :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>`. Nếu không, trả về một :ref:`StringName<class_StringName>` rỗng. Xem thêm :ref:`is_typed()<class_Array_method_is_typed>` và :ref:`Object.get_class()<class_Object_method_get_class>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_get_typed_script:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_typed_script**\ (\ ) |const| :ref:`🔗<class_Array_method_get_typed_script>`

Trả về instance :ref:`Script<class_Script>` liên kết với typed array này, hoặc ``null`` nếu không tồn tại. Xem thêm :ref:`is_typed()<class_Array_method_is_typed>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const| :ref:`🔗<class_Array_method_has>`

Trả về ``true`` nếu mảng chứa ``value`` đã cho.


.. tabs::

 .. code-tab:: gdscript

    print(["inside", 7].has("inside"))  # In ra true
    print(["inside", 7].has("outside")) # In ra false
    print(["inside", 7].has(7))         # In ra true
    print(["inside", 7].has("7"))       # In ra false

 .. code-tab:: csharp

    Godot.Collections.Array arr = ["inside", 7];
    // Theo quy ước của C#, phương thức này được đổi tên thành `Contains`.
    GD.Print(arr.Contains("inside"));  // In ra True
    GD.Print(arr.Contains("outside")); // In ra False
    GD.Print(arr.Contains(7));         // In ra True
    GD.Print(arr.Contains("7"));       // In ra False



Trong GDScript, điều này tương đương với toán tử ``in``:

::

    if 4 in [2, 4, 6, 8]:
        print("4 is here!") # Sẽ được in ra.

\ **Note:** For performance reasons, the search is affected by the ``value``'s :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`. For example, ``7`` (:ref:`int<class_int>`) and ``7.0`` (:ref:`float<class_float>`) are not considered equal for this method.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_hash:

.. rst-class:: classref-method

:ref:`int<class_int>` **hash**\ (\ ) |const| :ref:`🔗<class_Array_method_hash>`

Trả về một giá trị số nguyên 32-bit đã băm, đại diện cho mảng và nội dung của mảng.

\ **Lưu ý:** Các mảng có giá trị hash bằng nhau **không** được đảm bảo là giống nhau do xảy ra va chạm hash. Ngược lại, các mảng có giá trị hash khác nhau được đảm bảo là khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_insert:

.. rst-class:: classref-method

:ref:`int<class_int>` **insert**\ (\ position\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_insert>`

Chèn một phần tử mới (``value``) tại một chỉ mục cho trước (``position``) trong mảng. ``position`` phải nằm giữa ``0`` và :ref:`size()<class_Array_method_size>` của mảng. Nếu là số âm, ``position`` được tính tương đối từ cuối mảng.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` khác nếu phương thức này thất bại.

\ **Lưu ý:** Chỉ mục của mọi phần tử sau ``position`` cần được dịch về phía trước, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_Array_method_is_empty>`

Trả về ``true`` nếu mảng rỗng (``[]``). Xem thêm :ref:`size()<class_Array_method_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_is_read_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_read_only**\ (\ ) |const| :ref:`🔗<class_Array_method_is_read_only>`

Trả về ``true`` nếu mảng này là chỉ đọc. Xem :ref:`make_read_only()<class_Array_method_make_read_only>`.

Trong GDScript, các mảng tự động ở chế độ chỉ đọc nếu được khai báo bằng từ khóa ``const``.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_is_same_typed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_same_typed**\ (\ array\: :ref:`Array<class_Array>`\ ) |const| :ref:`🔗<class_Array_method_is_same_typed>`

Trả về ``true`` nếu mảng này có cùng kiểu với ``array`` đã cho. Xem thêm :ref:`is_typed()<class_Array_method_is_typed>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_is_typed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_typed**\ (\ ) |const| :ref:`🔗<class_Array_method_is_typed>`

Trả về ``true`` nếu mảng có kiểu. Typed array chỉ có thể chứa các phần tử thuộc một kiểu cụ thể, được xác định bởi typed array constructor. Các phương thức của typed array vẫn được kỳ vọng trả về một :ref:`Variant<class_Variant>` chung.

Trong GDScript, có thể định nghĩa một typed array bằng static typing:

::

    var numbers: Array[float] = [0.2, 4.2, -2.0]
    print(numbers.is_typed()) # In ra true

.. rst-class:: classref-item-separator

----

.. _class_Array_method_make_read_only:

.. rst-class:: classref-method

|void| **make_read_only**\ (\ ) :ref:`🔗<class_Array_method_make_read_only>`

Đặt mảng ở chế độ chỉ đọc. Các phần tử của mảng không thể bị ghi đè bằng các giá trị khác và thứ tự của chúng không thể thay đổi. Không áp dụng cho các phần tử lồng nhau, chẳng hạn như dictionary.

Trong GDScript, các mảng tự động ở chế độ chỉ đọc nếu được khai báo bằng từ khóa ``const``.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_map:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **map**\ (\ method\: :ref:`Callable<class_Callable>`\ ) |const| :ref:`🔗<class_Array_method_map>`

Gọi :ref:`Callable<class_Callable>` đã cho cho từng phần tử trong mảng và trả về một mảng mới chứa các giá trị do ``method`` trả về.

``method`` phải nhận một tham số :ref:`Variant<class_Variant>` (phần tử hiện tại của mảng) và có thể trả về bất kỳ :ref:`Variant<class_Variant>` nào.

::

    func double(number):
        return number * 2

    func _ready():
        print([1, 2, 3].map(double)) # In ra [2, 4, 6]

        # Tương tự như trên, nhưng sử dụng một hàm lambda.
        print([1, 2, 3].map(func(element): return element * 2))

Xem thêm :ref:`filter()<class_Array_method_filter>`, :ref:`reduce()<class_Array_method_reduce>`, :ref:`any()<class_Array_method_any>` và :ref:`all()<class_Array_method_all>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_max:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **max**\ (\ ) |const| :ref:`🔗<class_Array_method_max>`

Trả về giá trị lớn nhất có trong mảng nếu tất cả các phần tử đều có thể được so sánh. Nếu không, trả về ``null``. Xem thêm :ref:`min()<class_Array_method_min>`.

Để tìm giá trị lớn nhất bằng một comparator tùy chỉnh, bạn có thể sử dụng :ref:`reduce()<class_Array_method_reduce>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_min:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **min**\ (\ ) |const| :ref:`🔗<class_Array_method_min>`

Trả về giá trị nhỏ nhất có trong mảng nếu tất cả các phần tử đều có thể được so sánh. Nếu không, trả về ``null``. Xem thêm :ref:`max()<class_Array_method_max>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_pick_random:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **pick_random**\ (\ ) |const| :ref:`🔗<class_Array_method_pick_random>`

Trả về một phần tử ngẫu nhiên từ mảng. Tạo lỗi và trả về ``null`` nếu mảng rỗng.


.. tabs::

 .. code-tab:: gdscript

    # Có thể in ra 1, 2, 3.25 hoặc "Hi".
    print([1, 2, 3.25, "Hi"].pick_random())

 .. code-tab:: csharp

    Godot.Collections.Array array = [1, 2, 3.25f, "Hi"];
    GD.Print(array.PickRandom()); // Có thể in ra 1, 2, 3.25 hoặc "Hi".



\ **Lưu ý:** Giống như nhiều hàm tương tự khác trong engine (chẳng hạn như :ref:`@GlobalScope.randi()<class_@GlobalScope_method_randi>` hoặc :ref:`shuffle()<class_Array_method_shuffle>`), phương thức này sử dụng một seed ngẫu nhiên toàn cục, dùng chung. Để nhận được kết quả có thể dự đoán từ phương thức này, hãy xem :ref:`@GlobalScope.seed()<class_@GlobalScope_method_seed>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_pop_at:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **pop_at**\ (\ position\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Array_method_pop_at>`

Xóa và trả về phần tử của mảng tại index ``position``. Nếu là số âm, ``position`` được tính tương đối từ cuối mảng. Trả về ``null`` nếu mảng rỗng. Nếu ``position`` nằm ngoài phạm vi, một thông báo lỗi cũng được tạo.

\ **Lưu ý:** Phương thức này dịch index của mọi phần tử sau ``position`` lùi lại, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_pop_back:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **pop_back**\ (\ ) :ref:`🔗<class_Array_method_pop_back>`

Xóa và trả về phần tử cuối cùng của mảng. Trả về ``null`` nếu mảng rỗng mà không tạo lỗi. Xem thêm :ref:`pop_front()<class_Array_method_pop_front>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_pop_front:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **pop_front**\ (\ ) :ref:`🔗<class_Array_method_pop_front>`

Xóa và trả về phần tử đầu tiên của mảng. Trả về ``null`` nếu mảng rỗng mà không tạo lỗi. Xem thêm :ref:`pop_back()<class_Array_method_pop_back>`.

\ **Lưu ý:** Phương thức này dịch index của mọi phần tử còn lại lùi lại, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_push_back:

.. rst-class:: classref-method

|void| **push_back**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_push_back>`

Thêm một phần tử vào cuối mảng. Xem thêm :ref:`push_front()<class_Array_method_push_front>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_push_front:

.. rst-class:: classref-method

|void| **push_front**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_push_front>`

Thêm một phần tử vào đầu mảng. Xem thêm :ref:`push_back()<class_Array_method_push_back>`.

\ **Lưu ý:** Phương thức này dịch index của mọi phần tử còn lại tiến lên, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_reduce:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **reduce**\ (\ method\: :ref:`Callable<class_Callable>`, accum\: :ref:`Variant<class_Variant>` = null\ ) |const| :ref:`🔗<class_Array_method_reduce>`

Gọi :ref:`Callable<class_Callable>` đã cho cho từng phần tử trong mảng, tích lũy kết quả vào ``accum``, rồi trả về kết quả đó.

``method`` nhận hai đối số: giá trị hiện tại của ``accum`` và phần tử hiện tại của mảng. Nếu ``accum`` là ``null`` (như mặc định), quá trình lặp sẽ bắt đầu từ phần tử thứ hai, với phần tử đầu tiên được sử dụng làm giá trị ban đầu của ``accum``.

::

    func sum(accum, number):
        return accum + number

    func _ready():
        print([1, 2, 3].reduce(sum, 0))  # In ra 6
        print([1, 2, 3].reduce(sum, 10)) # In ra 16

        # Tương tự như trên, nhưng sử dụng một hàm lambda.
        print([1, 2, 3].reduce(func(accum, number): return accum + number, 10))

Nếu :ref:`max()<class_Array_method_max>` không phù hợp, phương thức này cũng có thể được dùng để triển khai một comparator tùy chỉnh:

::

    func _ready():
        var arr = [Vector2i(5, 0), Vector2i(3, 4), Vector2i(1, 2)]

        var longest_vec = arr.reduce(func(max, vec): return vec if is_length_greater(vec, max) else max)
        print(longest_vec) # In ra (3, 4)

    func is_length_greater(a, b):
        return a.length() > b.length()

Phương thức này cũng có thể được sử dụng để đếm số phần tử trong một mảng thỏa mãn một điều kiện nhất định, tương tự như :ref:`count()<class_Array_method_count>`:

::

    func is_even(number):
        return number % 2 == 0

    func _ready():
        var arr = [1, 2, 3, 4, 5]
        # Nếu phần tử hiện tại là số chẵn, tăng count; nếu không, giữ nguyên count.
        var even_count = arr.reduce(func(count, next): return count + 1 if is_even(next) else count, 0)
        print(even_count) # In ra 2

Xem thêm :ref:`map()<class_Array_method_map>`, :ref:`filter()<class_Array_method_filter>`, :ref:`any()<class_Array_method_any>` và :ref:`all()<class_Array_method_all>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_remove_at:

.. rst-class:: classref-method

|void| **remove_at**\ (\ position\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Array_method_remove_at>`

Xóa phần tử khỏi mảng tại index đã cho (``position``). Nếu index nằm ngoài phạm vi, phương thức này sẽ thất bại. Nếu index là số âm, ``position`` được tính tương đối từ cuối mảng.

Nếu cần trả về phần tử đã xóa, hãy sử dụng :ref:`pop_at()<class_Array_method_pop_at>`. Để xóa một phần tử theo giá trị, hãy sử dụng :ref:`erase()<class_Array_method_erase>` thay thế.

\ **Lưu ý:** Phương thức này dịch index của mọi phần tử sau ``position`` lùi lại, điều này có thể gây ra chi phí hiệu năng đáng kể, đặc biệt với các mảng lớn.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_resize:

.. rst-class:: classref-method

:ref:`int<class_int>` **resize**\ (\ size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Array_method_resize>`

Đặt số lượng phần tử của mảng thành ``size``. Nếu ``size`` nhỏ hơn kích thước hiện tại của mảng, các phần tử ở cuối sẽ bị xóa. Nếu ``size`` lớn hơn, các phần tử mặc định mới (thường là ``null``) sẽ được thêm vào, tùy thuộc vào kiểu của mảng.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` khi thành công hoặc một trong các hằng số :ref:`Error<enum_@GlobalScope_Error>` sau đây nếu phương thức thất bại: :ref:`@GlobalScope.ERR_LOCKED<class_@GlobalScope_constant_ERR_LOCKED>` nếu mảng ở chế độ chỉ đọc, :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu kích thước là số âm hoặc :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>` nếu việc cấp phát thất bại. Sử dụng :ref:`size()<class_Array_method_size>` để tìm kích thước thực tế của mảng sau khi thay đổi kích thước.

\ **Lưu ý:** Gọi phương thức này một lần rồi gán các giá trị mới sẽ nhanh hơn việc gọi :ref:`append()<class_Array_method_append>` cho từng phần tử mới.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_Array_method_reverse>`

Đảo ngược thứ tự của tất cả phần tử trong mảng.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_rfind:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind**\ (\ what\: :ref:`Variant<class_Variant>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_Array_method_rfind>`

Trả về index của lần xuất hiện **cuối cùng** của ``what`` trong mảng này hoặc ``-1`` nếu không có. Có thể chỉ định vị trí bắt đầu tìm kiếm bằng ``from``, sau đó tiếp tục về đầu mảng. Phương thức này là phiên bản ngược của :ref:`find()<class_Array_method_find>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_rfind_custom:

.. rst-class:: classref-method

:ref:`int<class_int>` **rfind_custom**\ (\ method\: :ref:`Callable<class_Callable>`, from\: :ref:`int<class_int>` = -1\ ) |const| :ref:`🔗<class_Array_method_rfind_custom>`

Trả về index của **phần tử cuối cùng** trong mảng khiến ``method`` trả về ``true`` hoặc ``-1`` nếu không có. Có thể chỉ định vị trí bắt đầu tìm kiếm bằng ``from``, sau đó tiếp tục về đầu mảng. Phương thức này là phiên bản ngược của :ref:`find_custom()<class_Array_method_find_custom>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ index\: :ref:`int<class_int>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Array_method_set>`

Đặt giá trị của phần tử tại ``index`` đã cho thành ``value`` đã cho. Thao tác này không thay đổi kích thước của mảng, mà chỉ thay đổi giá trị tại một index đã tồn tại trong mảng. Đây cũng chính là thao tác sử dụng toán tử ``[]`` (``array[index] = value``).

.. rst-class:: classref-item-separator

----

.. _class_Array_method_shuffle:

.. rst-class:: classref-method

|void| **shuffle**\ (\ ) :ref:`🔗<class_Array_method_shuffle>`

Xáo trộn tất cả phần tử của mảng theo thứ tự ngẫu nhiên.

\ **Lưu ý:** Giống như nhiều hàm tương tự khác trong engine (chẳng hạn như :ref:`@GlobalScope.randi()<class_@GlobalScope_method_randi>` hoặc :ref:`pick_random()<class_Array_method_pick_random>`), phương thức này sử dụng một seed ngẫu nhiên toàn cục, dùng chung. Để nhận được kết quả có thể dự đoán từ phương thức này, hãy xem :ref:`@GlobalScope.seed()<class_@GlobalScope_method_seed>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_Array_method_size>`

Trả về số lượng phần tử trong mảng. Các mảng rỗng (``[]``) luôn trả về ``0``. Xem thêm :ref:`is_empty()<class_Array_method_is_empty>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_slice:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **slice**\ (\ begin\: :ref:`int<class_int>`, end\: :ref:`int<class_int>` = 2147483647, step\: :ref:`int<class_int>` = 1, deep\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Array_method_slice>`

Trả về một **Array** mới chứa các phần tử của mảng này, từ index ``begin`` (bao gồm) đến ``end`` (không bao gồm), cách mỗi ``step`` phần tử.

Nếu ``begin`` hoặc ``end`` là số âm, giá trị của chúng được tính tương đối từ cuối mảng.

Nếu ``step`` là số âm, phương thức này duyệt qua mảng theo chiều ngược lại, trả về một slice theo thứ tự đảo ngược. Để hoạt động, ``begin`` phải lớn hơn ``end``.

Nếu ``deep`` là ``true``, tất cả các phần tử **Array** và :ref:`Dictionary<class_Dictionary>` lồng nhau trong slice sẽ được sao chép đệ quy từ bản gốc. Xem thêm :ref:`duplicate()<class_Array_method_duplicate>`.

::

    var letters = ["A", "B", "C", "D", "E", "F"]

    print(letters.slice(0, 2))  # In ra ["A", "B"]
    print(letters.slice(2, -2)) # In ra ["C", "D"]
    print(letters.slice(-2, 6)) # In ra ["E", "F"]

    print(letters.slice(0, 6, 2))  # In ra ["A", "C", "E"]
    print(letters.slice(4, 1, -1)) # In ra ["E", "D", "C"]

.. rst-class:: classref-item-separator

----

.. _class_Array_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_Array_method_sort>`

Sắp xếp mảng theo thứ tự tăng dần. Thứ tự cuối cùng phụ thuộc vào phép so sánh "nhỏ hơn" (``<``) giữa các phần tử.


.. tabs::

 .. code-tab:: gdscript

    var numbers = [10, 5, 2.5, 8]
    numbers.sort()
    print(numbers) # In ra [2.5, 5, 8, 10]

 .. code-tab:: csharp

    Godot.Collections.Array numbers = [10, 5, 2.5, 8];
    numbers.Sort();
    GD.Print(numbers); // In ra [2.5, 5, 8, 10]



\ **Lưu ý:** Thuật toán sắp xếp được sử dụng không phải là `stable <https://en.wikipedia.org/wiki/Sorting_algorithm#Stability>`__. Điều này có nghĩa là thứ tự của các phần tử tương đương (chẳng hạn như ``2`` và ``2.0``) có thể thay đổi khi gọi :ref:`sort()<class_Array_method_sort>`.

.. rst-class:: classref-item-separator

----

.. _class_Array_method_sort_custom:

.. rst-class:: classref-method

|void| **sort_custom**\ (\ func\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_Array_method_sort_custom>`

Sắp xếp mảng bằng :ref:`Callable<class_Callable>` tùy chỉnh.

\ ``func`` được gọi nhiều lần nếu cần, nhận hai phần tử mảng làm đối số. Hàm phải trả về ``true`` nếu phần tử thứ nhất nên được di chuyển *lên trước* phần tử thứ hai; nếu không, hàm phải trả về ``false``.

::

    func sort_ascending(a, b):
        if a[1] < b[1]:
            return true
        return false

    func _ready():
        var my_items = [["Tomato", 5], ["Apple", 9], ["Rice", 4]]
        my_items.sort_custom(sort_ascending)
        print(my_items) # In ra [["Rice", 4], ["Tomato", 5], ["Apple", 9]]

        # Sắp xếp theo thứ tự giảm dần bằng một hàm lambda.
        my_items.sort_custom(func(a, b): return a[1] > b[1])
        print(my_items) # In ra [["Apple", 9], ["Tomato", 5], ["Rice", 4]]

Cũng có thể cần sử dụng phương thức này để sắp xếp các chuỗi theo thứ tự tự nhiên, với :ref:`String.naturalnocasecmp_to()<class_String_method_naturalnocasecmp_to>`, như trong ví dụ sau:

::

    var files = ["newfile1", "newfile2", "newfile10", "newfile11"]
    files.sort_custom(func(a, b): return a.naturalnocasecmp_to(b) < 0)
    print(files) # In ra ["newfile1", "newfile2", "newfile10", "newfile11"]

\ **Lưu ý:** Trong C#, phương thức này không được hỗ trợ.

\ **Lưu ý:** Thuật toán sắp xếp được sử dụng không phải là `stable <https://en.wikipedia.org/wiki/Sorting_algorithm#Stability>`__. Điều này có nghĩa là thứ tự của các giá trị được xem là bằng nhau có thể bị thay đổi khi gọi phương thức này.

\ **Lưu ý:** Bạn không nên ngẫu nhiên hóa giá trị trả về của ``func``, vì thuật toán heapsort yêu cầu một kết quả nhất quán. Việc ngẫu nhiên hóa giá trị trả về sẽ dẫn đến hành vi không mong muốn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_Array_operator_neq_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_neq_Array>`

Trả về ``true`` nếu kích thước mảng hoặc các phần tử của mảng khác với kích thước hoặc các phần tử của ``right``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_sum_Array:

.. rst-class:: classref-operator

:ref:`Array<class_Array>` **operator +**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_sum_Array>`

Nối mảng ``right`` vào toán hạng bên trái, tạo một **Array** mới. Thao tác này còn được gọi là phép nối mảng.


.. tabs::

 .. code-tab:: gdscript

    var array1 = ["One", 2]
    var array2 = [3, "Four"]
    print(array1 + array2) # In ra ["One", 2, 3, "Four"]

 .. code-tab:: csharp

    // Note that concatenation is not possible with C#'s native Array type.
    Godot.Collections.Array array1 = ["One", 2];
    Godot.Collections.Array array2 = [3, "Four"];
    GD.Print(array1 + array2); // In ra ["One", 2, 3, "Four"]



\ **Lưu ý:** Đối với các mảng hiện có, :ref:`append_array()<class_Array_method_append_array>` hiệu quả hơn nhiều so với việc nối và gán bằng toán tử ``+=``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_lt_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_lt_Array>`

So sánh lần lượt các phần tử của cả hai mảng, bắt đầu từ chỉ mục ``0`` và kết thúc tại chỉ mục cuối cùng có trong cả hai mảng. Với mỗi cặp phần tử, trả về ``true`` nếu phần tử của mảng này nhỏ hơn phần tử của ``right``, trả về ``false`` nếu phần tử này lớn hơn. Nếu không, tiếp tục với cặp phần tử tiếp theo.

Nếu tất cả các phần tử đã tìm đều bằng nhau, trả về ``true`` nếu kích thước của mảng này nhỏ hơn kích thước của ``right``; nếu không, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_lte_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <=**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_lte_Array>`

So sánh lần lượt các phần tử của cả hai mảng, bắt đầu từ chỉ mục ``0`` và kết thúc tại chỉ mục cuối cùng có trong cả hai mảng. Với mỗi cặp phần tử, trả về ``true`` nếu phần tử của mảng này nhỏ hơn phần tử của ``right``, trả về ``false`` nếu phần tử này lớn hơn. Nếu không, tiếp tục với cặp phần tử tiếp theo.

Nếu tất cả các phần tử đã tìm đều bằng nhau, trả về ``true`` nếu kích thước của mảng này nhỏ hơn hoặc bằng kích thước của ``right``; nếu không, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_eq_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_eq_Array>`

So sánh **Array** ở toán hạng bên trái với **Array** ``right``. Trả về ``true`` nếu kích thước và nội dung của hai mảng bằng nhau, nếu không thì trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_gt_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_gt_Array>`

So sánh lần lượt các phần tử của cả hai mảng, bắt đầu từ chỉ mục ``0`` và kết thúc tại chỉ mục cuối cùng có trong cả hai mảng. Với mỗi cặp phần tử, trả về ``true`` nếu phần tử của mảng này lớn hơn phần tử của ``right``, trả về ``false`` nếu phần tử này nhỏ hơn. Nếu không, tiếp tục với cặp phần tử tiếp theo.

Nếu tất cả các phần tử đã tìm đều bằng nhau, trả về ``true`` nếu kích thước của mảng này lớn hơn kích thước của ``right``; nếu không, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_gte_Array:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >=**\ (\ right\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Array_operator_gte_Array>`

So sánh lần lượt các phần tử của cả hai mảng, bắt đầu từ chỉ mục ``0`` và kết thúc tại chỉ mục cuối cùng có trong cả hai mảng. Với mỗi cặp phần tử, trả về ``true`` nếu phần tử của mảng này lớn hơn phần tử của ``right``, trả về ``false`` nếu phần tử này nhỏ hơn. Nếu không, tiếp tục với cặp phần tử tiếp theo.

Nếu tất cả các phần tử đã tìm đều bằng nhau, trả về ``true`` nếu kích thước của mảng này lớn hơn hoặc bằng kích thước của ``right``; nếu không, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Array_operator_idx_int:

.. rst-class:: classref-operator

:ref:`Variant<class_Variant>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Array_operator_idx_int>`

Trả về phần tử :ref:`Variant<class_Variant>` tại ``index`` được chỉ định. Mảng bắt đầu tại chỉ mục 0. Nếu ``index`` lớn hơn hoặc bằng ``0``, phần tử được lấy bắt đầu từ đầu mảng. Nếu ``index`` là một giá trị âm, phần tử được lấy bắt đầu từ cuối mảng. Việc truy cập mảng vượt ngoài giới hạn sẽ gây ra lỗi run-time, tạm dừng quá trình thực thi dự án nếu chạy từ editor.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
