:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Dictionary.xml.

.. _class_Dictionary:

Dictionary
==========

Một cấu trúc dữ liệu tích hợp dùng để lưu các cặp khóa-giá trị.

.. rst-class:: classref-introduction-group

Mô tả
-----

Dictionary là các container kết hợp, chứa những giá trị được tham chiếu bằng các khóa duy nhất. Dictionary sẽ giữ nguyên thứ tự chèn khi thêm các mục mới. Trong các ngôn ngữ lập trình khác, cấu trúc dữ liệu này thường được gọi là hash map hoặc associative array.

Bạn có thể định nghĩa một dictionary bằng cách đặt một danh sách các cặp ``key: value`` được phân tách bằng dấu phẩy bên trong dấu ngoặc nhọn ``{}``.

Tạo một dictionary:


.. tabs::

 .. code-tab:: gdscript

    var my_dict = {} # Tạo một dictionary rỗng.

    var dict_variable_key = "Another key name"
    var dict_variable_value = "value2"
    var another_dict = {
        "Some key name": "value1",
        dict_variable_key: dict_variable_value,
    }

    var points_dict = { "White": 50, "Yellow": 75, "Orange": 100 }

    # Cú pháp kiểu Lua thay thế.
    # Không yêu cầu dấu ngoặc kép quanh các khóa, nhưng chỉ có các hằng chuỗi mới được dùng làm tên khóa.
    # Ngoài ra, tên khóa phải bắt đầu bằng một chữ cái hoặc dấu gạch dưới.
    # Ở đây, `some_key` là một string literal, không phải một biến!
    another_dict = {
        some_key = 42,
    }

 .. code-tab:: csharp

    var myDict = new Godot.Collections.Dictionary(); // Tạo một dictionary rỗng.
    var pointsDict = new Godot.Collections.Dictionary
    {
        { "White", 50 },
        { "Yellow", 75 },
        { "Orange", 100 },
    };



Bạn có thể truy cập giá trị của một dictionary bằng cách tham chiếu đến khóa tương ứng. Trong ví dụ trên, ``points_dict["White"]`` sẽ trả về ``50``. Bạn cũng có thể viết ``points_dict.White``, tương đương với cách trên. Tuy nhiên, bạn sẽ phải dùng cú pháp dấu ngoặc vuông nếu khóa dùng để truy cập dictionary không phải là một chuỗi cố định (chẳng hạn như một số hoặc biến).


.. tabs::

 .. code-tab:: gdscript

    @export_enum("White", "Yellow", "Orange") var my_color: String
    var points_dict = { "White": 50, "Yellow": 75, "Orange": 100 }
    func _ready():
        # Ở đây, chúng ta không thể dùng cú pháp dấu chấm vì `my_color` là một biến.
        var points = points_dict[my_color]

 .. code-tab:: csharp

    [Export(PropertyHint.Enum, "White,Yellow,Orange")]
    public string MyColor { get; set; }
    private Godot.Collections.Dictionary _pointsDict = new Godot.Collections.Dictionary
    {
        { "White", 50 },
        { "Yellow", 75 },
        { "Orange", 100 },
    };

    public override void _Ready()
    {
        int points = (int)_pointsDict[MyColor];
    }



Trong đoạn mã trên, ``points`` sẽ được gán giá trị đi kèm với màu tương ứng được chọn trong ``my_color``.

Dictionary có thể chứa dữ liệu phức tạp hơn:


.. tabs::

 .. code-tab:: gdscript

    var my_dict = {
        "First Array": [1, 2, 3, 4] # Gán một Array cho một khóa String.
    }

 .. code-tab:: csharp

    var myDict = new Godot.Collections.Dictionary
    {
        { "First Array", new Godot.Collections.Array { 1, 2, 3, 4 } }
    };



Để thêm một khóa vào dictionary hiện có, hãy truy cập nó như một khóa hiện có rồi gán giá trị cho nó:


.. tabs::

 .. code-tab:: gdscript

    var points_dict = { "White": 50, "Yellow": 75, "Orange": 100 }
    points_dict["Blue"] = 150 # Thêm "Blue" làm khóa và gán 150 làm giá trị của khóa đó.

 .. code-tab:: csharp

    var pointsDict = new Godot.Collections.Dictionary
    {
        { "White", 50 },
        { "Yellow", 75 },
        { "Orange", 100 },
    };
    pointsDict["Blue"] = 150; // Thêm "Blue" làm khóa và gán 150 làm giá trị của khóa đó.



Cuối cùng, dictionary không định kiểu có thể chứa các kiểu khóa và giá trị khác nhau trong cùng một dictionary:


.. tabs::

 .. code-tab:: gdscript

    # Đây là một dictionary hợp lệ.
    # Để truy cập chuỗi "Nested value" bên dưới, hãy dùng `my_dict.sub_dict.sub_key` hoặc `my_dict["sub_dict"]["sub_key"]`.
    # Bạn có thể kết hợp các kiểu lập chỉ mục tùy theo nhu cầu.
    var my_dict = {
        "String Key": 5,
        4: [1, 2, 3],
        7: "Hello",
        "sub_dict": { "sub_key": "Nested value" },
    }

 .. code-tab:: csharp

    // Đây là một dictionary hợp lệ.
    // Để truy cập chuỗi "Nested value" bên dưới, hãy dùng `((Godot.Collections.Dictionary)myDict["sub_dict"])["sub_key"]`.
    var myDict = new Godot.Collections.Dictionary {
        { "String Key", 5 },
        { 4, new Godot.Collections.Array { 1, 2, 3 } },
        { 7, "Hello" },
        { "sub_dict", new Godot.Collections.Dictionary { { "sub_key", "Nested value" } } },
    };



Có thể lặp qua các khóa của một dictionary bằng từ khóa ``for``:


.. tabs::

 .. code-tab:: gdscript

    var groceries = { "Orange": 20, "Apple": 2, "Banana": 4 }
    for fruit in groceries:
        var amount = groceries[fruit]

 .. code-tab:: csharp

    var groceries = new Godot.Collections.Dictionary { { "Orange", 20 }, { "Apple", 2 }, { "Banana", 4 } };
    foreach (var (fruit, amount) in groceries)
    {
        // `fruit` là khóa, còn `amount` là giá trị.
    }



Để buộc các khóa và giá trị phải có một kiểu nhất định, bạn có thể tạo một *typed dictionary*. Typed dictionary chỉ có thể chứa các khóa và giá trị thuộc những kiểu đã cho hoặc kế thừa từ các lớp đã cho:


.. tabs::

 .. code-tab:: gdscript

    # Tạo một dictionary có kiểu với các khóa String và giá trị int.
    # Việc cố sử dụng bất kỳ kiểu nào khác cho khóa hoặc giá trị sẽ dẫn đến lỗi.
    var typed_dict: Dictionary[String, int] = {
        "some_key": 1,
        "some_other_key": 2,
    }

    # Tạo một dictionary có kiểu với các khóa String và giá trị thuộc bất kỳ kiểu nào.
    # Việc cố sử dụng bất kỳ kiểu nào khác cho khóa sẽ dẫn đến lỗi.
    var typed_dict_key_only: Dictionary[String, Variant] = {
        "some_key": 12.34,
        "some_other_key": "string",
    }

 .. code-tab:: csharp

    // Tạo một dictionary có kiểu với các khóa String và giá trị int.
    // Việc cố sử dụng bất kỳ kiểu nào khác cho khóa hoặc giá trị sẽ dẫn đến lỗi.
    var typedDict = new Godot.Collections.Dictionary<String, int> {
        {"some_key", 1},
        {"some_other_key", 2},
    };

    // Tạo một dictionary có kiểu với các khóa String và giá trị thuộc bất kỳ kiểu nào.
    // Việc cố sử dụng bất kỳ kiểu nào khác cho khóa sẽ dẫn đến lỗi.
    var typedDictKeyOnly = new Godot.Collections.Dictionary<String, Variant> {
        {"some_key", 12.34},
        {"some_other_key", "string"},
    };



\ **Lưu ý:** Dictionary luôn được truyền bằng tham chiếu. Để lấy một bản sao của dictionary có thể được chỉnh sửa độc lập với dictionary gốc, hãy dùng :ref:`duplicate()<class_Dictionary_method_duplicate>`.

\ **Lưu ý:** Không hỗ trợ xóa các phần tử trong khi lặp qua dictionary và việc này sẽ dẫn đến hành vi không thể đoán trước.

\ **Lưu ý:** Trong ngữ cảnh boolean, một dictionary sẽ được đánh giá là ``false`` nếu nó rỗng (``{}``). Nếu không, dictionary sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `GDScript basics: Dictionary <../tutorials/scripting/gdscript/gdscript_basics.html#dictionary>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

- `Operating System Testing Demo <https://godotengine.org/asset-library/asset/2789>`__

.. rst-class:: classref-reftable-group

Constructor
-----------

.. table::
   :widths: auto

   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`Dictionary<class_Dictionary_constructor_Dictionary>`\ (\ )                                                                                                                                                                                                                                                                                                                           |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`Dictionary<class_Dictionary_constructor_Dictionary>`\ (\ base\: :ref:`Dictionary<class_Dictionary>`, key_type\: :ref:`int<class_int>`, key_class_name\: :ref:`StringName<class_StringName>`, key_script\: :ref:`Variant<class_Variant>`, value_type\: :ref:`int<class_int>`, value_class_name\: :ref:`StringName<class_StringName>`, value_script\: :ref:`Variant<class_Variant>`\ ) |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`Dictionary<class_Dictionary_constructor_Dictionary>`\ (\ from\: :ref:`Dictionary<class_Dictionary>`\ )                                                                                                                                                                                                                                                                               |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Method
------

.. table::
   :widths: auto

   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`assign<class_Dictionary_method_assign>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ )                                                                    |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`clear<class_Dictionary_method_clear>`\ (\ )                                                                                                                        |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`duplicate<class_Dictionary_method_duplicate>`\ (\ deep\: :ref:`bool<class_bool>` = false\ ) |const|                                                                |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`duplicate_deep<class_Dictionary_method_duplicate_deep>`\ (\ deep_subresources_mode\: :ref:`int<class_int>` = 1\ ) |const|                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`erase<class_Dictionary_method_erase>`\ (\ key\: :ref:`Variant<class_Variant>`\ )                                                                                   |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`find_key<class_Dictionary_method_find_key>`\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const|                                                                   |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get<class_Dictionary_method_get>`\ (\ key\: :ref:`Variant<class_Variant>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const|                               |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get_or_add<class_Dictionary_method_get_or_add>`\ (\ key\: :ref:`Variant<class_Variant>`, default\: :ref:`Variant<class_Variant>` = null\ )                         |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_typed_key_builtin<class_Dictionary_method_get_typed_key_builtin>`\ (\ ) |const|                                                                                |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_typed_key_class_name<class_Dictionary_method_get_typed_key_class_name>`\ (\ ) |const|                                                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get_typed_key_script<class_Dictionary_method_get_typed_key_script>`\ (\ ) |const|                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`get_typed_value_builtin<class_Dictionary_method_get_typed_value_builtin>`\ (\ ) |const|                                                                            |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_typed_value_class_name<class_Dictionary_method_get_typed_value_class_name>`\ (\ ) |const|                                                                      |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`get_typed_value_script<class_Dictionary_method_get_typed_value_script>`\ (\ ) |const|                                                                              |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`has<class_Dictionary_method_has>`\ (\ key\: :ref:`Variant<class_Variant>`\ ) |const|                                                                               |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`has_all<class_Dictionary_method_has_all>`\ (\ keys\: :ref:`Array<class_Array>`\ ) |const|                                                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`hash<class_Dictionary_method_hash>`\ (\ ) |const|                                                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_empty<class_Dictionary_method_is_empty>`\ (\ ) |const|                                                                                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_read_only<class_Dictionary_method_is_read_only>`\ (\ ) |const|                                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_same_typed<class_Dictionary_method_is_same_typed>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const|                                              |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_same_typed_key<class_Dictionary_method_is_same_typed_key>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const|                                      |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_same_typed_value<class_Dictionary_method_is_same_typed_value>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const|                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_typed<class_Dictionary_method_is_typed>`\ (\ ) |const|                                                                                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_typed_key<class_Dictionary_method_is_typed_key>`\ (\ ) |const|                                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_typed_value<class_Dictionary_method_is_typed_value>`\ (\ ) |const|                                                                                              |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`keys<class_Dictionary_method_keys>`\ (\ ) |const|                                                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`make_read_only<class_Dictionary_method_make_read_only>`\ (\ )                                                                                                      |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`merge<class_Dictionary_method_merge>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, overwrite\: :ref:`bool<class_bool>` = false\ )                         |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`merged<class_Dictionary_method_merged>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, overwrite\: :ref:`bool<class_bool>` = false\ ) |const|               |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`recursive_equal<class_Dictionary_method_recursive_equal>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, recursion_count\: :ref:`int<class_int>`\ ) |const| |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`set<class_Dictionary_method_set>`\ (\ key\: :ref:`Variant<class_Variant>`, value\: :ref:`Variant<class_Variant>`\ )                                                |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`size<class_Dictionary_method_size>`\ (\ ) |const|                                                                                                                  |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`sort<class_Dictionary_method_sort>`\ (\ )                                                                                                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`values<class_Dictionary_method_values>`\ (\ ) |const|                                                                                                              |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator !=<class_Dictionary_operator_neq_Dictionary>`\ (\ right\: :ref:`Dictionary<class_Dictionary>`\ ) |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator ==<class_Dictionary_operator_eq_Dictionary>`\ (\ right\: :ref:`Dictionary<class_Dictionary>`\ )  |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`operator []<class_Dictionary_operator_idx_Variant>`\ (\ key\: :ref:`Variant<class_Variant>`\ )            |
   +-------------------------------+-----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Constructor
-----------------

.. _class_Dictionary_constructor_Dictionary:

.. rst-class:: classref-constructor

:ref:`Dictionary<class_Dictionary>` **Dictionary**\ (\ ) :ref:`🔗<class_Dictionary_constructor_Dictionary>`

Tạo một **Dictionary** rỗng.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Dictionary<class_Dictionary>` **Dictionary**\ (\ base\: :ref:`Dictionary<class_Dictionary>`, key_type\: :ref:`int<class_int>`, key_class_name\: :ref:`StringName<class_StringName>`, key_script\: :ref:`Variant<class_Variant>`, value_type\: :ref:`int<class_int>`, value_class_name\: :ref:`StringName<class_StringName>`, value_script\: :ref:`Variant<class_Variant>`\ )

Tạo một dictionary có kiểu từ dictionary ``base``. Một dictionary có kiểu chỉ có thể chứa các khóa và giá trị thuộc những kiểu đã cho hoặc kế thừa từ các lớp đã cho, như được mô tả bởi các tham số của constructor này.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Dictionary<class_Dictionary>` **Dictionary**\ (\ from\: :ref:`Dictionary<class_Dictionary>`\ )

Trả về dictionary giống với ``from``. Nếu cần một bản sao của dictionary, hãy dùng :ref:`duplicate()<class_Dictionary_method_duplicate>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_Dictionary_method_assign:

.. rst-class:: classref-method

|void| **assign**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_Dictionary_method_assign>`

Gán các phần tử của một ``dictionary`` khác vào dictionary. Thay đổi kích thước dictionary để khớp với ``dictionary``. Thực hiện chuyển đổi kiểu nếu dictionary được định kiểu.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_Dictionary_method_clear>`

Xóa dictionary, loại bỏ tất cả các mục khỏi dictionary.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_duplicate:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **duplicate**\ (\ deep\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Dictionary_method_duplicate>`

Trả về một bản sao mới của dictionary.

Theo mặc định, một bản sao **shallow** được trả về: mọi khóa và giá trị :ref:`Array<class_Array>`, **Dictionary** và :ref:`Resource<class_Resource>` lồng nhau đều được dùng chung với dictionary gốc. Việc sửa đổi bất kỳ thành phần nào trong một dictionary cũng sẽ ảnh hưởng đến thành phần đó trong dictionary còn lại.

Nếu ``deep`` là ``true``, một bản sao **deep** sẽ được trả về: tất cả array và dictionary lồng nhau cũng được sao chép (đệ quy). Tuy nhiên, mọi :ref:`Resource<class_Resource>` vẫn được dùng chung với dictionary gốc.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_duplicate_deep:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **duplicate_deep**\ (\ deep_subresources_mode\: :ref:`int<class_int>` = 1\ ) |const| :ref:`🔗<class_Dictionary_method_duplicate_deep>`

Sao chép sâu dictionary này, tương tự như :ref:`duplicate()<class_Dictionary_method_duplicate>` khi truyền ``true``, với quyền kiểm soát bổ sung đối với cách xử lý các subresource.

\ ``deep_subresources_mode`` phải là một trong các giá trị của :ref:`DeepDuplicateMode<enum_Resource_DeepDuplicateMode>`. Theo mặc định, chỉ các resource nội bộ mới được sao chép (đệ quy).

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_erase:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **erase**\ (\ key\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Dictionary_method_erase>`

Xóa mục trong dictionary theo khóa nếu mục đó tồn tại. Trả về ``true`` nếu ``key`` đã cho tồn tại trong dictionary, nếu không thì trả về ``false``.

\ **Lưu ý:** Không xóa các mục trong khi lặp qua dictionary. Thay vào đó, bạn có thể lặp qua array :ref:`keys()<class_Dictionary_method_keys>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_find_key:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **find_key**\ (\ value\: :ref:`Variant<class_Variant>`\ ) |const| :ref:`🔗<class_Dictionary_method_find_key>`

Tìm và trả về khóa đầu tiên có giá trị liên kết bằng với ``value``, hoặc ``null`` nếu không tìm thấy.

\ **Lưu ý:** ``null`` cũng là một khóa hợp lệ. Nếu có trong dictionary, :ref:`find_key()<class_Dictionary_method_find_key>` có thể cho kết quả gây hiểu nhầm.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get**\ (\ key\: :ref:`Variant<class_Variant>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const| :ref:`🔗<class_Dictionary_method_get>`

Trả về giá trị tương ứng với ``key`` đã cho trong dictionary. Nếu ``key`` không tồn tại, trả về ``default``, hoặc ``null`` nếu tham số bị bỏ qua.

\ **Lưu ý:** Nếu đối số ``default`` yêu cầu nhiều tài nguyên tính toán hoặc gây ra các tác dụng phụ không mong muốn, hãy cân nhắc sử dụng method :ref:`has()<class_Dictionary_method_has>` thay thế:

::

    # Luôn gọi `expensive_function()`.
    dict.get("key", expensive_function())
    # Chỉ gọi `expensive_function()` nếu khóa không tồn tại.
    dict.get("key") if dict.has("key") else expensive_function()

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_or_add:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_or_add**\ (\ key\: :ref:`Variant<class_Variant>`, default\: :ref:`Variant<class_Variant>` = null\ ) :ref:`🔗<class_Dictionary_method_get_or_add>`

Lấy một giá trị và đảm bảo khóa được thiết lập. Nếu ``key`` tồn tại trong dictionary, cách này hoạt động như :ref:`get()<class_Dictionary_method_get>`. Nếu không, giá trị ``default`` được chèn vào dictionary và trả về.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_key_builtin:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_typed_key_builtin**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_key_builtin>`

Trả về kiểu :ref:`Variant<class_Variant>` tích hợp của các khóa trong dictionary có kiểu dưới dạng hằng số :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`. Nếu các khóa không được định kiểu, trả về :ref:`@GlobalScope.TYPE_NIL<class_@GlobalScope_constant_TYPE_NIL>`. Xem thêm :ref:`is_typed_key()<class_Dictionary_method_is_typed_key>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_key_class_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_typed_key_class_name**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_key_class_name>`

Trả về tên lớp **built-in** của các key trong typed dictionary, nếu kiểu :ref:`Variant<class_Variant>` built-in là :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>`. Nếu không, trả về một :ref:`StringName<class_StringName>` rỗng. Xem thêm :ref:`is_typed_key()<class_Dictionary_method_is_typed_key>` và :ref:`Object.get_class()<class_Object_method_get_class>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_key_script:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_typed_key_script**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_key_script>`

Trả về instance :ref:`Script<class_Script>` liên kết với các key của typed dictionary này, hoặc ``null`` nếu không tồn tại. Xem thêm :ref:`is_typed_key()<class_Dictionary_method_is_typed_key>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_value_builtin:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_typed_value_builtin**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_value_builtin>`

Trả về kiểu :ref:`Variant<class_Variant>` built-in của các value trong typed dictionary dưới dạng hằng số :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`. Nếu các value không được định kiểu, trả về :ref:`@GlobalScope.TYPE_NIL<class_@GlobalScope_constant_TYPE_NIL>`. Xem thêm :ref:`is_typed_value()<class_Dictionary_method_is_typed_value>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_value_class_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_typed_value_class_name**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_value_class_name>`

Trả về tên lớp **built-in** của các value trong typed dictionary, nếu kiểu :ref:`Variant<class_Variant>` built-in là :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>`. Nếu không, trả về một :ref:`StringName<class_StringName>` rỗng. Xem thêm :ref:`is_typed_value()<class_Dictionary_method_is_typed_value>` và :ref:`Object.get_class()<class_Object_method_get_class>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_get_typed_value_script:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_typed_value_script**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_get_typed_value_script>`

Trả về instance :ref:`Script<class_Script>` liên kết với các value của typed dictionary này, hoặc ``null`` nếu không tồn tại. Xem thêm :ref:`is_typed_value()<class_Dictionary_method_is_typed_value>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ key\: :ref:`Variant<class_Variant>`\ ) |const| :ref:`🔗<class_Dictionary_method_has>`

Trả về ``true`` nếu dictionary chứa một entry có ``key`` đã cho.


.. tabs::

 .. code-tab:: gdscript

    var my_dict = {
        "Godot" : 4,
        210 : null,
    }

    print(my_dict.has("Godot")) # In true
    print(my_dict.has(210))     # In true
    print(my_dict.has(4))       # In false

 .. code-tab:: csharp

    var myDict = new Godot.Collections.Dictionary
    {
        { "Godot", 4 },
        { 210, default },
    };

    GD.Print(myDict.ContainsKey("Godot")); // In True
    GD.Print(myDict.ContainsKey(210));     // In True
    GD.Print(myDict.ContainsKey(4));       // In False



Trong GDScript, điều này tương đương với operator ``in``:

::

    if "Godot" in { "Godot": 4 }:
        print("The key is here!") # Sẽ được in ra.

\ **Lưu ý:** Method này trả về ``true`` miễn là ``key`` tồn tại, ngay cả khi value tương ứng của nó là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_has_all:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_all**\ (\ keys\: :ref:`Array<class_Array>`\ ) |const| :ref:`🔗<class_Dictionary_method_has_all>`

Trả về ``true`` nếu dictionary chứa tất cả các key trong array ``keys`` đã cho.

::

    var data = { "width": 10, "height": 20 }
    data.has_all(["height", "width"]) # Trả về true

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_hash:

.. rst-class:: classref-method

:ref:`int<class_int>` **hash**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_hash>`

Trả về một giá trị số nguyên 32-bit đã hash, đại diện cho nội dung của dictionary.


.. tabs::

 .. code-tab:: gdscript

    var dict1 = { "A": 10, "B": 2 }
    var dict2 = { "A": 10, "B": 2 }

    print(dict1.hash() == dict2.hash()) # In true

 .. code-tab:: csharp

    var dict1 = new Godot.Collections.Dictionary { { "A", 10 }, { "B", 2 } };
    var dict2 = new Godot.Collections.Dictionary { { "A", 10 }, { "B", 2 } };

    // Godot.Collections.Dictionary không có method Hash(). Thay vào đó, hãy sử dụng GD.Hash().
    GD.Print(GD.Hash(dict1) == GD.Hash(dict2)); // In True



\ **Lưu ý:** Các dictionary có cùng entry nhưng khác thứ tự sẽ không có cùng hash.

\ **Lưu ý:** Các dictionary có giá trị hash bằng nhau *không* được đảm bảo là giống nhau do xảy ra va chạm hash. Ngược lại, các dictionary có giá trị hash khác nhau được đảm bảo là khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_empty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_empty**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_is_empty>`

Trả về ``true`` nếu dictionary rỗng (size của nó là ``0``). Xem thêm :ref:`size()<class_Dictionary_method_size>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_read_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_read_only**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_is_read_only>`

Trả về ``true`` nếu dictionary là read-only. Xem :ref:`make_read_only()<class_Dictionary_method_make_read_only>`. Các dictionary tự động là read-only nếu được khai báo bằng keyword ``const``.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_same_typed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_same_typed**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const| :ref:`🔗<class_Dictionary_method_is_same_typed>`

Trả về ``true`` nếu dictionary có cùng kiểu với ``dictionary``.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_same_typed_key:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_same_typed_key**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const| :ref:`🔗<class_Dictionary_method_is_same_typed_key>`

Trả về ``true`` nếu các key của dictionary có cùng kiểu với các key của ``dictionary``.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_same_typed_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_same_typed_value**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |const| :ref:`🔗<class_Dictionary_method_is_same_typed_value>`

Trả về ``true`` nếu các value của dictionary có cùng kiểu với các value của ``dictionary``.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_typed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_typed**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_is_typed>`

Trả về ``true`` nếu dictionary được định kiểu. Typed dictionary chỉ có thể lưu trữ các key/value thuộc kiểu tương ứng và cung cấp type safety cho operator ``[]``. Các method của typed dictionary vẫn trả về :ref:`Variant<class_Variant>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_typed_key:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_typed_key**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_is_typed_key>`

Trả về ``true`` nếu các key của dictionary được định kiểu.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_is_typed_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_typed_value**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_is_typed_value>`

Trả về ``true`` nếu các value của dictionary được định kiểu.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_keys:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **keys**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_keys>`

Trả về danh sách các key trong dictionary.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_make_read_only:

.. rst-class:: classref-method

|void| **make_read_only**\ (\ ) :ref:`🔗<class_Dictionary_method_make_read_only>`

Đặt dictionary thành read-only, tức là vô hiệu hóa việc sửa đổi nội dung của dictionary. Không áp dụng cho nội dung lồng nhau, chẳng hạn như nội dung của các dictionary lồng nhau.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_merge:

.. rst-class:: classref-method

|void| **merge**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, overwrite\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Dictionary_method_merge>`

Thêm các entry từ ``dictionary`` vào dictionary này. Theo mặc định, các key trùng lặp sẽ không được sao chép, trừ khi ``overwrite`` là ``true``.


.. tabs::

 .. code-tab:: gdscript

    var dict = { "item": "sword", "quantity": 2 }
    var other_dict = { "quantity": 15, "color": "silver" }

    # Theo mặc định, việc ghi đè các key hiện có bị vô hiệu hóa.
    dict.merge(other_dict)
    print(dict)  # { "item": "sword", "quantity": 2, "color": "silver" }

    # Khi bật tính năng ghi đè các key hiện có.
    dict.merge(other_dict, true)
    print(dict)  # { "item": "sword", "quantity": 15, "color": "silver" }

 .. code-tab:: csharp

    var dict = new Godot.Collections.Dictionary
    {
        ["item"] = "sword",
        ["quantity"] = 2,
    };

    var otherDict = new Godot.Collections.Dictionary
    {
        ["quantity"] = 15,
        ["color"] = "silver",
    };

    // Theo mặc định, việc ghi đè các key hiện có bị vô hiệu hóa.
    dict.Merge(otherDict);
    GD.Print(dict); // { "item": "sword", "quantity": 2, "color": "silver" }

    // Khi bật tính năng ghi đè các key hiện có.
    dict.Merge(otherDict, true);
    GD.Print(dict); // { "item": "sword", "quantity": 15, "color": "silver" }



\ **Lưu ý:** :ref:`merge()<class_Dictionary_method_merge>` *không* mang tính đệ quy. Các dictionary lồng nhau được xem là các key có thể bị ghi đè hoặc không, tùy thuộc vào giá trị của ``overwrite``, nhưng chúng sẽ không bao giờ được merge với nhau.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_merged:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **merged**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, overwrite\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Dictionary_method_merged>`

Trả về một bản sao của dictionary này được merge với ``dictionary`` còn lại. Theo mặc định, các key trùng lặp sẽ không được sao chép, trừ khi ``overwrite`` là ``true``. Xem thêm :ref:`merge()<class_Dictionary_method_merge>`.

Method này hữu ích khi cần nhanh chóng tạo các dictionary với giá trị mặc định:

::

    var base = { "fruit": "apple", "vegetable": "potato" }
    var extra = { "fruit": "orange", "dressing": "vinegar" }
    # In { "fruit": "orange", "vegetable": "potato", "dressing": "vinegar" }
    print(extra.merged(base))
    # In { "fruit": "apple", "vegetable": "potato", "dressing": "vinegar" }
    print(extra.merged(base, true))

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_recursive_equal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **recursive_equal**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`, recursion_count\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Dictionary_method_recursive_equal>`

Trả về ``true`` nếu hai dictionary chứa cùng các key và value; các key và value **Dictionary** cùng với :ref:`Array<class_Array>` bên trong được so sánh đệ quy.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_set:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **set**\ (\ key\: :ref:`Variant<class_Variant>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Dictionary_method_set>`

Đặt value của phần tử tại ``key`` đã cho thành ``value`` đã cho. Trả về ``true`` nếu đặt value thành công. Thất bại và trả về ``false`` nếu dictionary là read-only, hoặc nếu ``key`` và ``value`` không khớp với các kiểu của dictionary. Điều này tương đương với việc sử dụng operator ``[]`` (``dict[key] = value``).

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **size**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_size>`

Trả về số lượng entry trong dictionary. Các dictionary rỗng (``{ }``) luôn trả về ``0``. Xem thêm :ref:`is_empty()<class_Dictionary_method_is_empty>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_sort:

.. rst-class:: classref-method

|void| **sort**\ (\ ) :ref:`🔗<class_Dictionary_method_sort>`

Sắp xếp dictionary theo thứ tự tăng dần dựa trên key. Thứ tự cuối cùng phụ thuộc vào phép so sánh "nhỏ hơn" (``<``) giữa các key.


.. tabs::

 .. code-tab:: gdscript

    var numbers = { "c": 2, "a": 0, "b": 1 }
    numbers.sort()
    print(numbers) # In { "a": 0, "b": 1, "c": 2 }



Method này đảm bảo các entry của dictionary được sắp xếp nhất quán khi :ref:`keys()<class_Dictionary_method_keys>` hoặc :ref:`values()<class_Dictionary_method_values>` được gọi, hoặc khi dictionary cần được chuyển đổi thành chuỗi thông qua :ref:`@GlobalScope.str()<class_@GlobalScope_method_str>` hoặc :ref:`JSON.stringify()<class_JSON_method_stringify>`.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_method_values:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **values**\ (\ ) |const| :ref:`🔗<class_Dictionary_method_values>`

Trả về danh sách các value trong dictionary này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Operator
--------------

.. _class_Dictionary_operator_neq_Dictionary:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_Dictionary_operator_neq_Dictionary>`

Trả về ``true`` nếu hai dictionary không chứa cùng các key và value.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_operator_eq_Dictionary:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_Dictionary_operator_eq_Dictionary>`

Trả về ``true`` nếu hai dictionary chứa các key và value giống nhau. Thứ tự của các entry không quan trọng.

\ **Lưu ý:** Trong C#, theo quy ước, operator này so sánh theo **reference**. Nếu cần so sánh theo value, hãy duyệt qua cả hai dictionary.

.. rst-class:: classref-item-separator

----

.. _class_Dictionary_operator_idx_Variant:

.. rst-class:: classref-operator

:ref:`Variant<class_Variant>` **operator []**\ (\ key\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Dictionary_operator_idx_Variant>`

Trả về value tương ứng với ``key`` đã cho trong dictionary. Nếu entry không tồn tại, thao tác sẽ thất bại và trả về ``null``. Để truy cập an toàn, hãy sử dụng :ref:`get()<class_Dictionary_method_get>` hoặc :ref:`has()<class_Dictionary_method_has>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
