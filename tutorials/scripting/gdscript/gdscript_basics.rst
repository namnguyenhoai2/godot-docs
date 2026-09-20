.. _doc_gdscript_reference:

Tài liệu tham khảo GDScript
===========================

:ref:`GDScript<doc_gdscript>` is a high-level, `object-oriented
<https://en.wikipedia.org/wiki/Object-oriented_programming>`_, `imperative <https://en.wikipedia.org/wiki/Imperative_programming>`_, và ngôn ngữ lập trình `gradually typed <https://en.wikipedia.org/wiki/Gradual_typing>`_ được xây dựng cho Godot. Ngôn ngữ này sử dụng cú pháp dựa trên thụt lề, tương tự các ngôn ngữ như `Python <https://en.wikipedia.org/wiki/Python_%28programming_language%29>`_. Mục tiêu là được tối ưu hóa cho Godot Engine và tích hợp chặt chẽ với nó, cho phép linh hoạt cao trong việc tạo nội dung và tích hợp.

GDScript hoàn toàn độc lập với Python và không dựa trên Python.

Lịch sử
-------

.. note::

    Tài liệu về lịch sử của GDScript đã được chuyển đến
    :ref:`Frequently Asked Questions <doc_faq_what_is_gdscript>`.

Ví dụ về GDScript
-----------------

Một số người có thể học tốt hơn bằng cách xem qua cú pháp, vì vậy dưới đây là một ví dụ về hình thức của GDScript.

::

    # Mọi thứ sau "#" đều là chú thích.
    # Một tệp là một class!

    # icon (tùy chọn) sẽ hiển thị trong các hộp thoại của editor:
    @icon("res://path/to/optional/icon.svg")

    # định nghĩa class (tùy chọn):
    class_name MyClass

    # Kế thừa:
    extends BaseClass


    # Các biến thành viên.
    var a = 5
    var s = "Hello"
    var arr = [1, 2, 3]
    var dict = {"key": "value", 2: 3}
    var other_dict = {key = "value", other_key = 2}
    var typed_var: int
    var inferred_type := "String"

    # Hằng số.
    const ANSWER = 42
    const THE_NAME = "Charly"

    # Enum.
    enum {UNIT_NEUTRAL, UNIT_ENEMY, UNIT_ALLY}
    enum Named {THING_1, THING_2, ANOTHER_THING = -1}

    # Các kiểu vector tích hợp.
    var v2 = Vector2(1, 2)
    var v3 = Vector3(1, 2, 3)


    # Hàm có giá trị mặc định cho tham số cuối.
    func some_function(param1, param2, param3 = 123):
        const local_const = 5

        if param1 < local_const:
            print(param1)
        elif param2 > 5:
            print(param2)
        else:
            print("Fail!")

        for i in range(20):
            print(i)

        while param2 != 0:
            param2 -= 1

        match param3:
            3:
                print("param3 is 3!")
            _:
                print("param3 is not 3!")

        var local_var = param1 + 3
        return local_var


    # Các hàm override những hàm có cùng tên trong base/super class.
    # Nếu bạn vẫn muốn gọi chúng, hãy sử dụng "super":
    func something(p1, p2):
        super(p1, p2)


    # Bạn cũng có thể gọi một hàm khác trong super class:
    func other_something(p1, p2):
        super.something(p1, p2)


    # Class bên trong
    class Something:
        var a = 10


    # Constructor
    func _init():
        print("Constructed!")
        var lv = Something.new()
        print(lv.a)

Nếu bạn đã có kinh nghiệm với các ngôn ngữ kiểu tĩnh như C, C++ hoặc C# nhưng chưa từng sử dụng ngôn ngữ kiểu động nào, bạn nên đọc tutorial này: :ref:`doc_gdscript_more_efficiently`.

Identifier
----------

Bất kỳ chuỗi nào chỉ bao gồm các ký tự chữ cái (từ ``a`` đến ``z`` và từ ``A`` đến ``Z``), chữ số (từ ``0`` đến ``9``) và ``_`` đều được xem là một identifier. Ngoài ra, identifier không được bắt đầu bằng chữ số. Identifier phân biệt chữ hoa chữ thường (``foo`` khác với ``FOO``).

Identifier cũng có thể chứa hầu hết các ký tự Unicode thuộc `UAX#31 <https://www.unicode.org/reports/tr31/>`__. Điều này cho phép bạn sử dụng tên identifier được viết bằng các ngôn ngữ khác ngoài tiếng Anh. Các ký tự Unicode được xem là "dễ gây nhầm lẫn" với ký tự ASCII và emoji không được phép dùng trong identifier.

Từ khóa
-------

Sau đây là danh sách các từ khóa được ngôn ngữ hỗ trợ. Vì từ khóa là các từ dành riêng (token), chúng không thể được dùng làm identifier. Các operator (như ``in``, ``not``, ``and`` hoặc ``or``) và tên của các kiểu tích hợp được liệt kê trong những phần sau cũng là các từ dành riêng.

Các từ khóa được định nghĩa trong `GDScript tokenizer <https://github.com/godotengine/godot/blob/master/modules/gdscript/gdscript_tokenizer.cpp>`_ nếu bạn muốn xem cách chúng hoạt động bên trong.

+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
|  Keyword   | Description                                                                                                                                       |
+============+===================================================================================================================================================+
| if         | See `if/else/elif`_.                                                                                                                              |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| elif       | See `if/else/elif`_.                                                                                                                              |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| else       | See `if/else/elif`_.                                                                                                                              |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| for        | See for_.                                                                                                                                         |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| while      | See while_.                                                                                                                                       |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| match      | See match_.                                                                                                                                       |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| when       | Used by `pattern guards <Pattern guards_>`_ in ``match`` statements.                                                                              |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| break      | Exits the execution of the current ``for`` or ``while`` loop.                                                                                     |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| continue   | Immediately skips to the next iteration of the ``for`` or ``while`` loop.                                                                         |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| pass       | Used where a statement is required syntactically but execution of code is undesired, e.g. in empty functions.                                     |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| return     | Returns a value from a function.                                                                                                                  |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| class      | Defines an inner class. See `Inner classes`_.                                                                                                     |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| class_name | Defines the script as a globally accessible class with the specified name. See `Registering named classes`_.                                      |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| extends    | Defines what class to extend with the current class.                                                                                              |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| is         | Tests whether a variable extends a given class, or is of a given built-in type.                                                                   |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| in         | Tests whether a value is within a string, array, range, dictionary, or node. When used with ``for``, it iterates through them instead of testing. |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| as         | Cast the value to a given type if possible.                                                                                                       |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| self       | Refers to current class instance. See `self`_.                                                                                                    |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| super      | Resolves the scope of the parent method. See `Inheritance`_.                                                                                      |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| signal     | Defines a signal. See `Signals`_.                                                                                                                 |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| func       | Defines a function.  See `Functions`_.                                                                                                            |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| static     | Defines a static function or a static member variable.                                                                                            |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| const      | Defines a constant. See `Constants`_.                                                                                                             |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| enum       | Defines an enum. See `Enums`_.                                                                                                                    |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| var        | Defines a variable. See `Variables`_.                                                                                                             |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| breakpoint | Editor helper for debugger breakpoints. Unlike breakpoints created by clicking in the gutter, ``breakpoint`` is stored in the script itself.      |
|            | This makes it persistent across different machines when using version control.                                                                    |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| preload    | Preloads a class or variable. See `Classes as resources`_.                                                                                        |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| await      | Waits for a signal or a coroutine to finish. See `Awaiting signals or coroutines`_.                                                               |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| yield      | Previously used for coroutines. Kept as keyword for transition.                                                                                   |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| assert     | Asserts a condition, logs error on failure. Ignored in non-debug builds. See `Assert keyword`_.                                                   |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| void       | Used to represent that a function does not return any value.                                                                                      |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| PI         | PI constant.                                                                                                                                      |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| TAU        | TAU constant.                                                                                                                                     |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| INF        | Infinity constant. Used for comparisons and as result of calculations.                                                                            |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| NAN        | NAN (not a number) constant. Used as impossible result from calculations.                                                                         |
+------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

Operator
--------

Sau đây là danh sách các operator được hỗ trợ và độ ưu tiên của chúng. Tất cả operator nhị phân đều là `left-associative <https://en.wikipedia.org/wiki/Operator_associativity>`_, bao gồm cả operator ``**``. Điều này có nghĩa là ``2 ** 2 ** 3`` tương đương với ``(2 ** 2) ** 3``. Hãy sử dụng dấu ngoặc để chỉ định rõ độ ưu tiên cần dùng, chẳng hạn như ``2 ** (2 ** 3)``. Operator ba ngôi ``if/else`` kết hợp phải.

+---------------------------------------+-----------------------------------------------------------------------------+
| **Operator**                          | **Description**                                                             |
+=======================================+=============================================================================+
| ``(`` ``)``                           | Grouping (highest priority)                                                 |
|                                       |                                                                             |
|                                       | Parentheses are not really an operator, but allow you to explicitly specify |
|                                       | the precedence of an operation.                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x[index]``                          | Subscription                                                                |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x.attribute``                       | Attribute reference                                                         |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``foo()``                             | Function call                                                               |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``await x``                           | `Awaiting signals or coroutines`_                                           |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x is Node``                       | Type checking                                                               |
| | ``x is not Node``                   |                                                                             |
|                                       | See also :ref:`is_instance_of() <class_@GDScript_method_is_instance_of>`    |
|                                       | function.                                                                   |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x ** y``                            | Power                                                                       |
|                                       |                                                                             |
|                                       | Multiplies ``x`` by itself ``y`` times, similar to calling                  |
|                                       | :ref:`pow() <class_@GlobalScope_method_pow>` function.                      |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``~x``                                | Bitwise NOT                                                                 |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``+x``                              | Identity / Negation                                                         |
| | ``-x``                              |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x * y``                           | Multiplication / Division / Remainder                                       |
| | ``x / y``                           |                                                                             |
| | ``x % y``                           | The ``%`` operator is additionally used for                                 |
|                                       | :ref:`format strings <doc_gdscript_printf>`.                                |
|                                       |                                                                             |
|                                       | **Note:** These operators have the same behavior as C++, which may be       |
|                                       | unexpected for users coming from Python, JavaScript, etc. See a detailed    |
|                                       | note after the table.                                                       |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x + y``                           | Addition (or Concatenation) / Subtraction                                   |
| | ``x - y``                           |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x << y``                          | Bit shifting                                                                |
| | ``x >> y``                          |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x & y``                             | Bitwise AND                                                                 |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x ^ y``                             | Bitwise XOR                                                                 |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x | y``                             | Bitwise OR                                                                  |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x == y``                          | Comparison                                                                  |
| | ``x != y``                          |                                                                             |
| | ``x < y``                           | See a detailed note after the table.                                        |
| | ``x > y``                           |                                                                             |
| | ``x <= y``                          |                                                                             |
| | ``x >= y``                          |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x in y``                          | Inclusion checking                                                          |
| | ``x not in y``                      |                                                                             |
|                                       | ``in`` is also used with the for_ keyword as part of the syntax.            |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``not x``                           | Boolean NOT and its :ref:`unrecommended <boolean_operators>` alias          |
| | ``!x``                              |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x and y``                         | Boolean AND and its :ref:`unrecommended <boolean_operators>` alias          |
| | ``x && y``                          |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x or y``                          | Boolean OR and its :ref:`unrecommended <boolean_operators>` alias           |
| | ``x || y``                          |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``true_expr if cond else false_expr`` | Ternary if/else                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+
| ``x as Node``                         | `Type casting <casting_>`_                                                  |
+---------------------------------------+-----------------------------------------------------------------------------+
| | ``x = y``                           | Assignment (lowest priority)                                                |
| | ``x += y``                          |                                                                             |
| | ``x -= y``                          | You cannot use an assignment operator inside an expression.                 |
| | ``x *= y``                          |                                                                             |
| | ``x /= y``                          |                                                                             |
| | ``x **= y``                         |                                                                             |
| | ``x %= y``                          |                                                                             |
| | ``x &= y``                          |                                                                             |
| | ``x |= y``                          |                                                                             |
| | ``x ^= y``                          |                                                                             |
| | ``x <<= y``                         |                                                                             |
| | ``x >>= y``                         |                                                                             |
+---------------------------------------+-----------------------------------------------------------------------------+

.. note::

    Một số operator có thể hoạt động khác với điều bạn mong đợi:

    1. Nếu cả hai toán hạng của operator ``/`` đều là :ref:`int <class_int>`, phép chia số nguyên sẽ được thực hiện thay vì phép chia phân số. Ví dụ ``5 / 2 == 2``, không phải ``2.5``. Nếu đây không phải điều bạn muốn, hãy sử dụng ít nhất một literal :ref:`float <class_float>` (``x / 2.0``), ép kiểu (``float(x) / y``) hoặc nhân với ``1.0`` (``x * 1.0 / y``). 2. Operator ``%`` chỉ khả dụng cho int; với float, hãy sử dụng hàm :ref:`fmod() <class_@GlobalScope_method_fmod>`. 3. Với các giá trị âm, operator ``%`` và ``fmod()`` sử dụng `truncation <https://en.wikipedia.org/wiki/Truncation>`_ thay vì làm tròn về âm vô cùng. Điều này có nghĩa là phần dư có dấu. Nếu cần phần dư theo nghĩa toán học, hãy sử dụng :ref:`posmod() <class_@GlobalScope_method_posmod>` và
       :ref:`fposmod() <class_@GlobalScope_method_fposmod>` functions instead.
    4. Các operator ``==`` và ``!=`` đôi khi cho phép bạn so sánh các giá trị thuộc các kiểu khác nhau (ví dụ, ``1 == 1.0`` là true), nhưng trong những trường hợp khác, chúng có thể gây ra lỗi runtime. Nếu không chắc chắn về kiểu của các toán hạng, bạn có thể sử dụng an toàn hàm :ref:`is_same() <class_@GlobalScope_method_is_same>` (nhưng lưu ý rằng hàm này nghiêm ngặt hơn về kiểu và reference). Để so sánh float, hãy sử dụng các hàm :ref:`is_equal_approx() <class_@GlobalScope_method_is_equal_approx>` và :ref:`is_zero_approx() <class_@GlobalScope_method_is_zero_approx>`.

Literal
-------

+---------------------------------+-------------------------------------------+
| **Example(s)**                  | **Description**                           |
+---------------------------------+-------------------------------------------+
| ``null``                        | Null value                                |
+---------------------------------+-------------------------------------------+
| ``false``, ``true``             | Boolean values                            |
+---------------------------------+-------------------------------------------+
| ``45``                          | Base 10 integer                           |
+---------------------------------+-------------------------------------------+
| ``0x8f51``                      | Base 16 (hexadecimal) integer             |
+---------------------------------+-------------------------------------------+
| ``0b101010``                    | Base 2 (binary) integer                   |
+---------------------------------+-------------------------------------------+
| ``3.14``, ``58.1e-10``          | Floating-point number (real)              |
+---------------------------------+-------------------------------------------+
| ``"Hello"``, ``'Hi'``           | Regular strings                           |
+---------------------------------+-------------------------------------------+
| ``"""Hello"""``, ``'''Hi'''``   | Triple-quoted regular strings             |
+---------------------------------+-------------------------------------------+
| ``r"Hello"``, ``r'Hi'``         | Raw strings                               |
+---------------------------------+-------------------------------------------+
| ``r"""Hello"""``, ``r'''Hi'''`` | Triple-quoted raw strings                 |
+---------------------------------+-------------------------------------------+
| ``&"name"``                     | :ref:`StringName <class_StringName>`      |
+---------------------------------+-------------------------------------------+
| ``^"Node/Label"``               | :ref:`NodePath <class_NodePath>`          |
+---------------------------------+-------------------------------------------+

Ngoài ra còn có hai cấu trúc trông giống literal nhưng thực tế không phải:

+---------------------------------+-------------------------------------------+
| **Example**                     | **Description**                           |
+---------------------------------+-------------------------------------------+
| ``$NodePath``                   | Shorthand for ``get_node("NodePath")``    |
+---------------------------------+-------------------------------------------+
| ``%UniqueNode``                 | Shorthand for ``get_node("%UniqueNode")`` |
+---------------------------------+-------------------------------------------+

Số nguyên và số thực có thể được phân tách bằng ``_`` để dễ đọc hơn. Các cách viết số sau đây đều hợp lệ:

::

    12_345_678  # Bằng 12345678.
    3.141_592_7  # Bằng 3.1415927.
    0x8080_0000_ffff  # Bằng 0x80800000ffff.
    0b11_00_11_00  # Bằng 0b11001100.

**Literal chuỗi thông thường** có thể chứa các escape sequence sau:

+---------------------+---------------------------------+
| **Escape sequence** | **Expands to**                  |
+---------------------+---------------------------------+
| ``\n``              | Newline (line feed)             |
+---------------------+---------------------------------+
| ``\t``              | Horizontal tab character        |
+---------------------+---------------------------------+
| ``\r``              | Carriage return                 |
+---------------------+---------------------------------+
| ``\a``              | Alert (beep/bell)               |
+---------------------+---------------------------------+
| ``\b``              | Backspace                       |
+---------------------+---------------------------------+
| ``\f``              | Formfeed page break             |
+---------------------+---------------------------------+
| ``\v``              | Vertical tab character          |
+---------------------+---------------------------------+
| ``\"``              | Double quote                    |
+---------------------+---------------------------------+
| ``\'``              | Single quote                    |
+---------------------+---------------------------------+
| ``\\``              | Backslash                       |
+---------------------+---------------------------------+
| ``\uXXXX``          | UTF-16 Unicode codepoint        |
|                     | ``XXXX``                        |
|                     | (hexadecimal, case-insensitive) |
+---------------------+---------------------------------+
| ``\UXXXXXX``        | UTF-32 Unicode codepoint        |
|                     | ``XXXXXX``                      |
|                     | (hexadecimal, case-insensitive) |
+---------------------+---------------------------------+

Có hai cách biểu diễn một ký tự Unicode đã escape phía trên ``0xFFFF``:

- dưới dạng một `UTF-16 surrogate pair <https://en.wikipedia.org/wiki/UTF-16#Code_points_from_U+010000_to_U+10FFFF>`_ ``\uXXXX\uXXXX``. - dưới dạng một codepoint UTF-32 duy nhất ``\UXXXXXX``.

Ngoài ra, sử dụng ``\`` theo sau bởi một dòng mới bên trong chuỗi sẽ cho phép bạn tiếp tục chuỗi ở dòng tiếp theo mà không chèn ký tự dòng mới vào chính chuỗi đó.

Một chuỗi được bao quanh bằng dấu ngoặc kép của một loại (ví dụ ``"``) có thể chứa dấu ngoặc kép của loại khác (ví dụ ``'``) mà không cần escape. Chuỗi được đặt trong ba dấu ngoặc kép cho phép bạn không cần escape tối đa hai dấu ngoặc kép liên tiếp cùng loại (trừ khi chúng nằm liền kề với mép chuỗi).

**Literal chuỗi raw** luôn mã hóa chuỗi đúng như cách nó xuất hiện trong mã nguồn. Điều này đặc biệt hữu ích cho regular expression. Literal chuỗi raw không xử lý escape sequence, nhưng nhận diện ``\\`` và ``\"`` (``\'``) rồi thay thế chúng bằng chính chúng. Do đó, một chuỗi có thể chứa dấu ngoặc kép trùng với dấu ngoặc mở, nhưng chỉ khi dấu ngoặc đó đứng sau một dấu gạch chéo ngược.

::

    print("\tchar=\"\\t\"")  # In `    char="\t"`.
    print(r"\tchar=\"\\t\"") # In `\tchar=\"\\t\"`.

.. note::

    Một số chuỗi không thể được biểu diễn bằng literal chuỗi raw: bạn không thể có số lẻ dấu gạch chéo ngược ở cuối chuỗi hoặc có dấu ngoặc mở chưa được escape bên trong chuỗi. Tuy nhiên, trên thực tế điều này không đáng kể vì bạn có thể sử dụng loại dấu ngoặc khác hoặc nối với một literal chuỗi thông thường.

GDScript cũng hỗ trợ :ref:`format strings <doc_gdscript_printf>`.

Annotation
----------

Annotation là các token đặc biệt trong GDScript, hoạt động như modifier cho toàn bộ script, một khai báo, một câu lệnh hoặc một vị trí trong mã nguồn. Annotation có thể ảnh hưởng đến cách script được xử lý bởi Godot editor và GDScript compiler.

Mỗi annotation bắt đầu bằng ký tự ``@`` và được chỉ định bằng một tên. Mô tả chi tiết và ví dụ cho từng annotation có thể được tìm thấy trong
:ref:`GDScript class reference <class_@GDScript>`.

Ví dụ, bạn có thể sử dụng nó để export một giá trị sang editor:

::

    @export_range(1, 100, 1, "or_greater")
    var ranged_var: int = 50

Để biết thêm thông tin về việc export property, hãy đọc bài viết :ref:`GDScript exports <doc_gdscript_exports>`.

Bất kỳ biểu thức hằng số nào tương thích với kiểu đối số bắt buộc đều có thể được truyền làm giá trị đối số của annotation:

::

    const MAX_SPEED = 120.0

    @export_range(0.0, 0.5 * MAX_SPEED)
    var initial_speed: float = 0.25 * MAX_SPEED

Annotation có thể được chỉ định mỗi annotation trên một dòng hoặc tất cả trên cùng một dòng. Chúng tác động đến câu lệnh tiếp theo không phải là annotation. Annotation có thể nhận đối số được đặt giữa các dấu ngoặc đơn và phân tách bằng dấu phẩy.

Cả hai cách này đều giống nhau:

::

    @annotation_a
    @annotation_b
    var variable

    @annotation_a @annotation_b var variable

.. _doc_gdscript_onready_annotation:

Annotation ``@onready``
~~~~~~~~~~~~~~~~~~~~~~~

Khi sử dụng node, việc muốn giữ reference đến các phần của scene trong một biến là điều phổ biến. Vì scene chỉ được đảm bảo đã được cấu hình khi đi vào active scene tree, các sub-node chỉ có thể được lấy khi gọi ``Node._ready()``.

::

    var my_label


    func _ready():
        my_label = get_node("MyLabel")

Điều này có thể hơi rườm rà, đặc biệt khi các node và external reference tăng lên. Vì vậy, GDScript có annotation ``@onready``, trì hoãn việc khởi tạo một biến thành viên cho đến khi ``_ready()`` được gọi. Nó có thể thay thế đoạn mã trên bằng một dòng duy nhất:

::

    @onready var my_label = get_node("MyLabel")

.. warning::

    Việc áp dụng annotation ``@onready`` và bất kỳ annotation ``@export`` nào cho cùng một biến không hoạt động như bạn có thể mong đợi. Annotation ``@onready`` sẽ khiến giá trị mặc định được thiết lập sau khi ``@export`` có hiệu lực và sẽ ghi đè giá trị đó:

    ::

        @export var a = "init_value_a"
        @onready @export var b = "init_value_b"

        func _init():
            prints(a, b) # init_value_a <null>

        func _notification(what):
            if what == NOTIFICATION_SCENE_INSTANTIATED:
                prints(a, b) # exported_value_a exported_value_b

        func _ready():
            prints(a, b) # exported_value_a init_value_b

    Do đó, cảnh báo ``ONREADY_WITH_EXPORT`` được tạo ra và theo mặc định được xem là lỗi. Chúng tôi không khuyến nghị vô hiệu hóa hoặc bỏ qua cảnh báo này.

Chú thích
---------

Mọi thứ từ ``#`` đến cuối dòng đều bị bỏ qua và được xem là chú thích.

::

    # Đây là một chú thích.

.. tip::

    Trong Godot script editor, các từ khóa đặc biệt được tô sáng bên trong chú thích để thu hút sự chú ý của người dùng đến những chú thích cụ thể:

    - **Nghiêm trọng** *(hiển thị màu đỏ)*: ``ALERT``, ``ATTENTION``, ``CAUTION``, ``CRITICAL``, ``DANGER``, ``SECURITY`` - **Cảnh báo** *(hiển thị màu vàng)*: ``BUG``, ``DEPRECATED``, ``FIXME``, ``HACK``, ``TASK``, ``TBD``, ``TODO``, ``WARNING`` - **Thông báo** *(hiển thị màu xanh lá)*: ``INFO``, ``NOTE``, ``NOTICE``, ``TEST``, ``TESTING``

    Các keyword này phân biệt chữ hoa chữ thường, vì vậy chúng phải được viết bằng chữ hoa để được nhận diện:

    ::

        # Trong ví dụ bên dưới, "TODO" sẽ mặc định hiển thị bằng màu vàng.
        # Ký hiệu `:` sau keyword không bắt buộc, nhưng thường được sử dụng.

        # TODO: Add more items for the player to choose from.

    Danh sách các keyword được tô sáng và màu của chúng có thể được thay đổi trong mục **Text Editor > Theme > Comment Markers** của Editor Settings.

Sử dụng hai ký hiệu hash (``##``) thay vì một ký hiệu (``#``) để thêm *documentation comment*, nội dung này sẽ xuất hiện trong tài liệu script và phần mô tả trong inspector của một biến được export. Documentation comment phải được đặt trực tiếp *phía trên* một mục có thể được lập tài liệu (chẳng hạn như một member variable), hoặc ở đầu file. Ngoài ra còn có các tùy chọn định dạng chuyên dụng. Xem
:ref:`doc_gdscript_documentation_comments` for details.

::

    ## This comment will appear in the script documentation.
    var value

    ## This comment will appear in the inspector tooltip, and in the documentation.
    @export var exported_value

.. _doc_gdscript_code_regions:

Code regions
------------

Code regions là các loại comment đặc biệt mà script editor hiểu là *foldable regions*. Điều này có nghĩa là sau khi viết comment cho code region, bạn có thể thu gọn và mở rộng region bằng cách nhấp vào mũi tên xuất hiện ở bên trái comment. Mũi tên này xuất hiện bên trong một hình vuông màu tím để dễ phân biệt với thao tác code folding tiêu chuẩn.

Cú pháp như sau:

::

    # Quan trọng: Không được có *bất kỳ* khoảng trắng nào giữa `#` và `region` hoặc `endregion`.

    # Region without a description:
    #region
    ...
    #endregion

    # Region with a description:
    #region Some description that is displayed even when collapsed
    ...
    #endregion

.. tip::

    Để nhanh chóng tạo một code region, hãy chọn vài dòng trong script editor, nhấp chuột phải vào vùng chọn rồi chọn **Create Code Region**. Mô tả region sẽ tự động được chọn để chỉnh sửa.

    Bạn có thể lồng các code region bên trong những code region khác.

Sau đây là một ví dụ cụ thể về cách sử dụng code region:

::

    # Comment này nằm bên ngoài code region. Nó sẽ hiển thị khi region được thu gọn.
    #region Terrain generation
    # Comment này nằm bên trong code region. Nó sẽ không hiển thị khi region được thu gọn.
    func generate_lakes():
        pass

    func generate_hills():
        pass
    #endregion

    #region Terrain population
    func place_vegetation():
        pass

    func place_roads():
        pass
    #endregion

Điều này có thể hữu ích để sắp xếp các khối code lớn thành những phần dễ hiểu hơn. Tuy nhiên, hãy nhớ rằng các external editor thường không hỗ trợ tính năng này, vì vậy hãy đảm bảo code của bạn vẫn dễ theo dõi ngay cả khi không dựa vào việc folding code region.

.. note::

    Các function riêng lẻ và những phần được thụt lề (chẳng hạn như ``if`` và ``for``) *luôn* có thể được thu gọn trong script editor. Điều này có nghĩa là bạn nên tránh sử dụng code region để chứa một function hoặc một phần được thụt lề duy nhất, vì cách này không mang lại nhiều lợi ích. Code region hoạt động hiệu quả nhất khi được dùng để nhóm nhiều phần tử lại với nhau.

Line continuation
-----------------

Một dòng code trong GDScript có thể được tiếp tục ở dòng kế tiếp bằng cách sử dụng dấu gạch chéo ngược (``\``). Thêm dấu này ở cuối dòng, và code ở dòng kế tiếp sẽ hoạt động như thể nó nằm tại vị trí của dấu gạch chéo ngược. Sau đây là một ví dụ:

::

    var a = 1 + \
    2

Một dòng có thể được tiếp tục nhiều lần như sau:

::

    var a = 1 + \
    4 + \
    10 + \
    4

.. _doc_gdscript_builtin_types:

Built-in types
--------------

Built-in types được cấp phát trên stack. Chúng được truyền dưới dạng value. Điều này có nghĩa là một bản sao được tạo ra trong mỗi phép gán hoặc khi truyền chúng làm argument cho các function. Ngoại lệ là ``Object``, ``Array``, ``Dictionary`` và các packed array (chẳng hạn như ``PackedByteArray``), vốn được truyền theo reference nên được dùng chung. Tất cả array, ``Dictionary`` và một số object (``Node``, ``Resource``) đều có method ``duplicate()`` cho phép bạn tạo một bản sao.

Basic built-in types
~~~~~~~~~~~~~~~~~~~~

Một variable trong GDScript có thể được gán cho một số built-in type.

null
^^^^

``null`` là một kiểu dữ liệu rỗng, không chứa thông tin nào và không thể được gán bất kỳ giá trị nào khác.

Chỉ những type kế thừa từ Object mới có thể nhận giá trị ``null`` (do đó Object được gọi là type "nullable").
:ref:`Variant types <doc_variant_class>` must have a valid value at all times,
và vì vậy không thể nhận giá trị ``null``.

:ref:`bool <class_bool>`
^^^^^^^^^^^^^^^^^^^^^^^^

Viết tắt của "boolean", type này chỉ có thể chứa ``true`` hoặc ``false``.

:ref:`int <class_int>`
^^^^^^^^^^^^^^^^^^^^^^

Viết tắt của "integer", type này lưu trữ các số nguyên (dương và âm). Nó được lưu dưới dạng giá trị 64-bit, tương đương với ``int64_t`` trong C++.

:ref:`float <class_float>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Lưu trữ các số thực, bao gồm cả số thập phân, bằng các giá trị dấu phẩy động. Nó được lưu dưới dạng giá trị 64-bit, tương đương với ``double`` trong C++. Lưu ý: Hiện tại, các cấu trúc dữ liệu như ``Vector2``, ``Vector3`` và ``PackedFloat32Array`` lưu trữ các giá trị ``float`` dấu phẩy động single-precision 32-bit.

:ref:`String <class_String>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Một chuỗi ký tự trong `Unicode format <https://en.wikipedia.org/wiki/Unicode>`_.

:ref:`StringName <class_StringName>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Một string bất biến chỉ cho phép một instance của mỗi name. Chúng tạo chậm hơn và có thể khiến phải chờ lock khi multithreading. Đổi lại, chúng so sánh rất nhanh, nên phù hợp để làm key cho dictionary.

:ref:`NodePath <class_NodePath>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Một path đã được phân tích trước đến một node hoặc thuộc tính của node. Nó có thể dễ dàng được gán từ và cho một String. Chúng hữu ích khi tương tác với tree để lấy một node hoặc tác động đến các thuộc tính như với :ref:`Tweens <class_Tween>`.

Vector built-in types
~~~~~~~~~~~~~~~~~~~~~

:ref:`Vector2 <class_Vector2>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Type vector 2D chứa các field ``x`` và ``y``. Cũng có thể được truy cập như một array.

:ref:`Vector2i <class_Vector2i>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Giống Vector2 nhưng các component là số nguyên. Hữu ích để biểu diễn các phần tử trong một grid 2D.

:ref:`Rect2 <class_Rect2>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Type Rectangle 2D chứa hai field vector: ``position`` và ``size``. Cũng chứa một field ``end`` có giá trị là ``position + size``.

:ref:`Vector3 <class_Vector3>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Type vector 3D chứa các field ``x``, ``y`` và ``z``. Cũng có thể được truy cập như một array.

:ref:`Vector3i <class_Vector3i>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Giống Vector3 nhưng các component là số nguyên. Có thể dùng để đánh index các phần tử trong một grid 3D.

:ref:`Transform2D <class_Transform2D>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ma trận 3×2 được sử dụng cho các phép biến đổi 2D.

:ref:`Plane <class_Plane>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Type Plane 3D ở dạng normalized, chứa một field vector ``normal`` và một khoảng cách scalar ``d``.

:ref:`Quaternion <class_Quaternion>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Quaternion là một datatype được sử dụng để biểu diễn phép xoay 3D. Nó hữu ích khi nội suy các phép xoay.

:ref:`AABB <class_AABB>`
^^^^^^^^^^^^^^^^^^^^^^^^

Axis-aligned bounding box (hay box 3D) chứa 2 field vector: ``position`` và ``size``. Nó cũng chứa một field ``end`` có giá trị là ``position + size``.

:ref:`Basis <class_Basis>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ma trận 3x3 được sử dụng cho phép xoay và scale 3D. Nó chứa 3 field vector (``x``, ``y`` và ``z``) và cũng có thể được truy cập như một array gồm các vector 3D.

:ref:`Transform3D <class_Transform3D>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Transform 3D chứa một field Basis ``basis`` và một field Vector3 ``origin``.

Engine built-in types
~~~~~~~~~~~~~~~~~~~~~

:ref:`Color <class_Color>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Datatype Color chứa các field ``r``, ``g``, ``b`` và ``a``. Nó cũng có thể được truy cập dưới dạng ``h``, ``s`` và ``v`` tương ứng với hue/saturation/value.

:ref:`RID <class_RID>`
^^^^^^^^^^^^^^^^^^^^^^

Resource ID (RID). Các server sử dụng RID generic để tham chiếu đến dữ liệu opaque.

:ref:`Object <class_Object>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Base class cho mọi thứ không phải là built-in type.

Container built-in types
~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`Array <class_Array>`
^^^^^^^^^^^^^^^^^^^^^^^^^^

Sequence generic của các object type tùy ý, bao gồm cả array hoặc dictionary khác (xem bên dưới). Array có thể tự động thay đổi kích thước. Array được đánh index bắt đầu từ index ``0``. Các index âm được tính từ cuối.

::

    var arr = []
    arr = [1, 2, 3]
    var b = arr[1] # Đây là 2.
    var c = arr[arr.size() - 1] # Đây là 3.
    var d = arr[-1] # Giống dòng trước, nhưng ngắn hơn.
    arr[0] = "Hi!" # Thay thế giá trị 1 bằng "Hi!".
    arr.append(4) # Array hiện là ["Hi!", 2, 3, 4].

Typed arrays
^^^^^^^^^^^^

Godot cũng hỗ trợ typed array. Trong các thao tác ghi, Godot kiểm tra xem giá trị của phần tử có khớp với type được chỉ định hay không, vì vậy array không thể chứa các giá trị không hợp lệ. GDScript static analyzer có tính đến typed array, tuy nhiên các method của array như ``front()`` và ``back()`` vẫn có return type là ``Variant``.

Mảng có kiểu có cú pháp ``Array[Type]``, trong đó ``Type`` có thể là bất kỳ kiểu ``Variant`` nào, lớp native hoặc lớp do người dùng định nghĩa, hay enum. Không hỗ trợ các kiểu mảng lồng nhau (như ``Array[Array[int]]``).

::

    var a: Array[int]
    var b: Array[Node]
    var c: Array[MyClass]
    var d: Array[MyEnum]
    var e: Array[Variant]

``Array`` và ``Array[Variant]`` là cùng một thứ.

.. note::

    Mảng được truyền theo tham chiếu, vì vậy kiểu phần tử mảng cũng là một thuộc tính của cấu trúc trong bộ nhớ mà một biến tham chiếu đến trong runtime. Kiểu tĩnh của một biến giới hạn các cấu trúc mà biến đó có thể tham chiếu đến. Do đó, bạn **không thể** gán một mảng có kiểu phần tử khác, ngay cả khi kiểu đó là kiểu con của kiểu được yêu cầu.

    Nếu muốn *chuyển đổi* một mảng có kiểu, bạn có thể tạo một mảng mới và sử dụng
    :ref:`Array.assign() <class_Array_method_assign>` method:

    ::

        var a: Array[Node2D] = [Node2D.new()]

        # (OK) Bạn có thể thêm giá trị vào mảng vì `Node2D` kế thừa `Node`.
        var b: Array[Node] = [a[0]]

        # (Lỗi) Bạn không thể gán một `Array[Node2D]` cho một biến `Array[Node]`.
        b = a

        # (OK) Tuy nhiên, bạn có thể sử dụng phương thức `assign()`. Không giống toán tử `=`,
        # phương thức `assign()` sao chép nội dung của mảng, không phải tham chiếu.
        b.assign(a)

    Ngoại lệ duy nhất được áp dụng cho kiểu ``Array`` (``Array[Variant]``), nhằm thuận tiện cho người dùng và tương thích với mã cũ. Tuy nhiên, các thao tác trên mảng không có kiểu được xem là không an toàn.

.. _doc_gdscript_packed_arrays:

Mảng Packed
^^^^^^^^^^^

PackedArrays nhìn chung nhanh hơn khi lặp qua và sửa đổi so với một Array có kiểu cùng loại (ví dụ: PackedInt64Array so với Array[int]) và sử dụng ít bộ nhớ hơn. Trong trường hợp tệ nhất, chúng được kỳ vọng có tốc độ tương đương với một Array không có kiểu. Ngược lại, các Array không phải Packed (có kiểu hoặc không) có thêm các phương thức tiện ích như :ref:`Array.map <class_Array_method_map>` mà PackedArrays không có. Hãy tham khảo :ref:`class reference <class_PackedFloat32Array>` để biết chi tiết về các phương thức hiện có. Array có kiểu nhìn chung nhanh hơn khi lặp qua và sửa đổi so với Array không có kiểu.

Mặc dù mọi Array đều có thể gây phân mảnh bộ nhớ khi đủ lớn, nếu việc sử dụng bộ nhớ và hiệu năng (tốc độ lặp qua và sửa đổi) là mối quan tâm, đồng thời kiểu dữ liệu bạn lưu trữ tương thích với một trong các kiểu Array ``Packed``, thì việc sử dụng chúng có thể mang lại cải thiện. Tuy nhiên, nếu bạn không gặp những mối quan tâm đó (ví dụ: kích thước mảng không đạt đến hàng chục nghìn phần tử), việc sử dụng Array thông thường hoặc Array có kiểu có thể hữu ích hơn, vì chúng cung cấp các phương thức tiện ích giúp mã dễ viết và bảo trì hơn (và có thể nhanh hơn nếu dữ liệu của bạn thường xuyên yêu cầu các thao tác như vậy). Nếu dữ liệu bạn sẽ lưu trữ có kiểu xác định (bao gồm cả các lớp do bạn tự định nghĩa), hãy ưu tiên sử dụng Array có kiểu vì nó có thể mang lại hiệu năng tốt hơn khi lặp qua và sửa đổi so với Array không có kiểu.

- :ref:`PackedByteArray <class_PackedByteArray>`: Một mảng byte (số nguyên từ 0 đến 255). - :ref:`PackedInt32Array <class_PackedInt32Array>`: Một mảng số nguyên 32-bit. - :ref:`PackedInt64Array <class_PackedInt64Array>`: Một mảng số nguyên 64-bit. - :ref:`PackedFloat32Array <class_PackedFloat32Array>`: Một mảng số thực 32-bit. - :ref:`PackedFloat64Array <class_PackedFloat64Array>`: Một mảng số thực 64-bit. - :ref:`PackedStringArray <class_PackedStringArray>`: Một mảng chuỗi. - :ref:`PackedVector2Array <class_PackedVector2Array>`: Một mảng các giá trị :ref:`Vector2 <class_Vector2>`. - :ref:`PackedVector3Array <class_PackedVector3Array>`: Một mảng các giá trị :ref:`Vector3 <class_Vector3>`. - :ref:`PackedVector4Array <class_PackedVector4Array>`: Một mảng các giá trị :ref:`Vector4 <class_Vector4>`. - :ref:`PackedColorArray <class_PackedColorArray>`: Một mảng các giá trị :ref:`Color <class_Color>`.

:ref:`Dictionary <class_Dictionary>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Container kết hợp chứa các giá trị được tham chiếu bởi các khóa duy nhất.

::

    var d = {4: 5, "A key": "A value", 28: [1, 2, 3]}
    d["Hi!"] = 0
    d = {
        22: "value",
        "some_key": 2,
        "other_key": [2, 3, 4],
        "more_key": "Hello"
    }

Cú pháp table kiểu Lua cũng được hỗ trợ. Cú pháp kiểu Lua sử dụng ``=`` thay vì ``:`` và không dùng dấu ngoặc kép để đánh dấu các khóa chuỗi (do đó cần viết ít hơn một chút). Tuy nhiên, các khóa được viết theo dạng này không thể bắt đầu bằng chữ số (giống mọi identifier của GDScript) và phải là string literal.

::

    var d = {
        test22 = "value",
        some_key = 2,
        other_key = [2, 3, 4],
        more_key = "Hello"
    }

Để thêm một khóa vào dictionary hiện có, hãy truy cập khóa đó như một khóa hiện có và gán giá trị cho nó:

::

    var d = {} # Tạo một Dictionary rỗng.
    d.waiting = 14 # Thêm String "waiting" làm khóa và gán giá trị 14 cho khóa đó.
    d[4] = "hello" # Thêm số nguyên 4 làm khóa và gán String "hello" làm giá trị của khóa đó.
    d["Godot"] = 3.01 # Thêm String "Godot" làm khóa và gán giá trị 3.01 cho khóa đó.

    var test = 4
    # In ra "hello" bằng cách lập chỉ mục dictionary với một khóa động.
    # Điều này không giống với `d.test`. Cú pháp dấu ngoặc vuông tương đương với
    # `d.test` là `d["test"]`.
    print(d[test])

.. note::

    Cú pháp dấu ngoặc vuông có thể được dùng để truy cập các thuộc tính của bất kỳ
    :ref:`class_Object`, not just Dictionaries. Keep in mind it will cause a
    lỗi script khi cố lập chỉ mục một thuộc tính không tồn tại. Để tránh điều này, hãy sử dụng :ref:`Object.get() <class_Object_method_get>` và
    :ref:`Object.set() <class_Object_method_set>` methods instead.

Dictionary có kiểu
^^^^^^^^^^^^^^^^^^

Godot 4.4 đã thêm hỗ trợ cho dictionary có kiểu. Khi thực hiện thao tác ghi, Godot kiểm tra xem khóa và giá trị của phần tử có khớp với kiểu đã chỉ định hay không, vì vậy dictionary không thể chứa khóa hoặc giá trị không hợp lệ. Trình phân tích tĩnh GDScript cũng tính đến dictionary có kiểu. Tuy nhiên, các phương thức dictionary trả về giá trị vẫn có kiểu trả về ``Variant``.

Dictionary có kiểu có cú pháp ``Dictionary[KeyType, ValueType]``, trong đó ``KeyType`` và ``ValueType`` có thể là bất kỳ kiểu ``Variant`` nào, lớp native hoặc lớp do người dùng định nghĩa, hay enum. **Phải** chỉ định cả kiểu khóa và kiểu giá trị, nhưng bạn có thể sử dụng ``Variant`` để đặt một trong hai thành không có kiểu. Không hỗ trợ các collection có kiểu lồng nhau (như ``Dictionary[String, Dictionary[String, int]]``).

::

    var a: Dictionary[String, int]
    var b: Dictionary[String, Node]
    var c: Dictionary[Vector2i, MyClass]
    var d: Dictionary[MyEnum, float]
    # Khóa là chuỗi, giá trị có thể có bất kỳ kiểu nào.
    var e: Dictionary[String, Variant]
    # Khóa có thể có bất kỳ kiểu nào, giá trị là boolean.
    var f: Dictionary[Variant, bool]

``Dictionary`` và ``Dictionary[Variant, Variant]`` là cùng một thứ.

:ref:`Signal <class_Signal>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Signal là một thông điệp có thể được một object phát ra cho những đối tượng muốn lắng nghe nó. Kiểu Signal có thể được dùng để truyền emitter.

Signal được sử dụng tốt hơn bằng cách lấy chúng từ các object thực tế, ví dụ ``$Button.button_up``.

:ref:`Callable <class_Callable>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Chứa một object và một function, hữu ích khi truyền các function dưới dạng giá trị (ví dụ: khi kết nối với signal).

Lấy một method dưới dạng member sẽ trả về một callable. ``var x = $Sprite2D.rotate`` sẽ đặt giá trị của ``x`` thành một callable với ``$Sprite2D`` là object và ``rotate`` là method.

Bạn có thể gọi nó bằng phương thức ``call``: ``x.call(PI)``.

Biến
----

Biến có thể tồn tại dưới dạng member của class hoặc là biến cục bộ trong các function. Chúng được tạo bằng keyword ``var`` và có thể, tùy chọn, được gán một giá trị khi khởi tạo.

::

    var a # Kiểu dữ liệu mặc định là 'null'.
    var b = 5
    var c = 3.8
    var d = b + c # Các biến luôn được khởi tạo theo thứ tự trực tiếp (xem bên dưới).

Biến có thể tùy chọn có đặc tả kiểu. Khi một kiểu được chỉ định, biến sẽ luôn bị buộc phải có đúng kiểu đó, và việc cố gán một giá trị không tương thích sẽ gây ra lỗi.

Kiểu được chỉ định trong khai báo biến bằng ký hiệu ``:`` (dấu hai chấm) sau tên biến, tiếp theo là kiểu.

::

    var my_vector2: Vector2
    var my_node: Node = Sprite2D.new()

Nếu biến được khởi tạo ngay trong khai báo, kiểu có thể được suy luận, vì vậy có thể bỏ qua tên kiểu:

::

    var my_vector2 := Vector2() # 'my_vector2' có kiểu 'Vector2'.
    var my_node := Sprite2D.new() # 'my_node' có kiểu 'Sprite2D'.

Suy luận kiểu chỉ có thể thực hiện nếu giá trị được gán có kiểu xác định; nếu không, sẽ gây ra lỗi.

Các kiểu hợp lệ gồm:

- Các kiểu dựng sẵn (Array, Vector2, int, String, v.v.). - Các class của engine (Node, Resource, RefCounted, v.v.). - Tên hằng nếu chúng chứa một script resource (``MyScript`` nếu bạn đã khai báo ``const MyScript = preload("res://my_script.gd")``). - Các class khác trong cùng script, tuân theo scope (``InnerClass.NestedClass`` nếu bạn đã khai báo ``class NestedClass`` bên trong ``class InnerClass`` trong cùng scope). - Các script class được khai báo bằng keyword ``class_name``. - Các Autoload được đăng ký dưới dạng singleton.

.. note::

    Mặc dù ``Variant`` là một đặc tả kiểu hợp lệ, nó không phải là một kiểu thực tế. Nó chỉ có nghĩa là không có kiểu cố định và tương đương với việc hoàn toàn không có kiểu tĩnh. Vì vậy, theo mặc định, suy luận không được phép đối với ``Variant``, vì nhiều khả năng đó là một lỗi.

    Bạn có thể tắt kiểm tra này hoặc chỉ coi nó là cảnh báo bằng cách thay đổi trong project settings. Xem :ref:`doc_gdscript_warning_system` để biết chi tiết.

Thứ tự khởi tạo
~~~~~~~~~~~~~~~

Các biến member được khởi tạo theo thứ tự sau:

1. Tùy thuộc vào kiểu tĩnh của biến, biến sẽ ``null`` (các biến không có kiểu và object) hoặc có giá trị mặc định của kiểu đó (``0`` đối với ``int``, ``false`` đối với ``bool``, v.v.). 2. Các giá trị đã chỉ định được gán theo thứ tự của các biến trong script, từ trên xuống dưới.

   - (Chỉ áp dụng cho các class kế thừa ``Node``) Nếu annotation ``@onready`` được áp dụng cho một biến, việc khởi tạo biến đó sẽ được trì hoãn đến bước 5.

3. Nếu được định nghĩa, method ``_init()`` sẽ được gọi. 4. Khi khởi tạo scene và resource, các giá trị được export sẽ được gán. 5. (Chỉ áp dụng cho các class kế thừa ``Node``) Các biến ``@onready`` được khởi tạo. 6. (Chỉ áp dụng cho các class kế thừa ``Node``) Nếu được định nghĩa, method ``_ready()`` sẽ được gọi.

.. warning::

    Bạn có thể chỉ định một biểu thức phức tạp làm bộ khởi tạo biến, bao gồm cả lời gọi function. Hãy đảm bảo các biến được khởi tạo đúng thứ tự, nếu không các giá trị của bạn có thể bị ghi đè. Ví dụ:

    ::

        var a: int = proxy("a", 1)
        var b: int = proxy("b", 2)
        var _data: Dictionary = {}

        func proxy(key: String, value: int):
            _data[key] = value
            print(_data)
            return value

        func _init() -> void:
            print(_data)

    Sẽ in ra:

    ::

        { "a": 1 }
        { "a": 1, "b": 2 }
        {  }

    Để khắc phục điều này, hãy di chuyển phần định nghĩa biến ``_data`` lên trên phần định nghĩa ``a`` hoặc xóa phép gán từ điển rỗng (``= {}``).

.. _doc_gdscript_basics_static_variables:

Biến static
~~~~~~~~~~~

Một biến thành viên của class có thể được khai báo là static:

::

    static var a

Các biến static thuộc về class, không phải các instance. Điều này có nghĩa là các biến static chia sẻ giá trị giữa nhiều instance, không giống các biến thành viên thông thường.

Bên trong một class, bạn có thể truy cập các biến static từ mọi function, cả static và non-static. Bên ngoài class, bạn có thể truy cập các biến static bằng class hoặc một instance (cách thứ hai không được khuyến nghị vì khó đọc hơn).

.. note::

    Không thể áp dụng các annotation ``@export`` và ``@onready`` cho biến static. Biến cục bộ không thể là static.

Ví dụ sau định nghĩa một class ``Person`` với một biến static có tên ``max_id``. Chúng ta tăng ``max_id`` trong function ``_init()``. Điều này giúp dễ dàng theo dõi số lượng instance ``Person`` trong game.

::

    # person.gd
    class_name Person

    static var max_id = 0

    var id
    var name

    func _init(p_name):
        max_id += 1
        id = max_id
        name = p_name

Trong code này, chúng ta tạo hai instance của class ``Person`` và kiểm tra để chắc chắn rằng class và mọi instance đều có cùng giá trị ``max_id``, vì biến này là static và có thể được truy cập bởi mọi instance.

::

    # test.gd
    extends Node

    func _ready():
        var person1 = Person.new("John Doe")
        var person2 = Person.new("Jane Doe")

        print(person1.id) # 1
        print(person2.id) # 2

        print(Person.max_id)  # 2
        print(person1.max_id) # 2
        print(person2.max_id) # 2

Các biến static có thể có type hint, setter và getter:

::

    static var balance: int = 0

    static var debt: int:
        get:
            return -balance
        set(value):
            balance = -value

Một biến static của base class cũng có thể được truy cập thông qua child class:

::

    class A:
        static var x = 1

    class B extends A:
        pass

    func _ready():
        prints(A.x, B.x) # 1 1
        A.x = 2
        prints(A.x, B.x) # 2 2
        B.x = 3
        prints(A.x, B.x) # 3 3

.. note::

    Khi tham chiếu đến một biến static từ tool script, script khác chứa biến static đó cũng **phải** là một tool script. Xem :ref:`Running code in the editor <doc_running_code_in_the_editor_important_information>` để biết chi tiết.

annotation ``@static_unload``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Vì các class GDScript là resource, việc có các biến static trong một script sẽ ngăn script đó được unload ngay cả khi không còn instance nào của class đó và không còn reference nào khác. Điều này có thể quan trọng nếu các biến static lưu trữ lượng dữ liệu lớn hoặc giữ reference đến các resource khác của project, chẳng hạn như scene. Bạn nên tự dọn dẹp dữ liệu này hoặc sử dụng annotation :ref:`@static_unload <class_@GDScript_annotation_@static_unload>` nếu các biến static không lưu trữ dữ liệu quan trọng và có thể được reset.

.. warning::

    Hiện tại, do một bug, các script không bao giờ được free, ngay cả khi sử dụng annotation ``@static_unload``.

Lưu ý rằng ``@static_unload`` áp dụng cho toàn bộ script (bao gồm cả các inner class) và phải được đặt ở đầu script, trước ``class_name`` và ``extends``:

::

    @static_unload
    class_name MyNode
    extends Node

Xem thêm `Các hàm static`_ và `Static constructor`_.

Ép kiểu
~~~~~~~

Các giá trị được gán cho biến có kiểu phải có kiểu tương thích. Nếu cần ép một giá trị về một kiểu nhất định, đặc biệt đối với các kiểu object, bạn có thể sử dụng toán tử ép kiểu ``as``.

Ép kiểu giữa các kiểu object sẽ cho ra cùng object nếu giá trị có cùng kiểu hoặc là subtype của kiểu được ép sang.

::

    var my_node2D: Node2D
    my_node2D = $Sprite2D as Node2D # Hoạt động vì Sprite2D là một subtype của Node2D.

Nếu giá trị không phải là subtype, thao tác ép kiểu sẽ cho ra một giá trị ``null``.

::

    var my_node2D: Node2D
    my_node2D = $Button as Node2D # Cho kết quả là 'null' vì Button không phải là subtype của Node2D.

Đối với các kiểu dựng sẵn, chúng sẽ được chuyển đổi bắt buộc nếu có thể; nếu không, engine sẽ phát sinh lỗi.

::

    var my_int: int
    my_int = "123" as int # Chuỗi có thể được chuyển đổi thành int.
    my_int = Vector2() as int # Một Vector2 không thể được chuyển đổi thành int, điều này sẽ gây ra lỗi.

Ép kiểu cũng hữu ích để có các biến an toàn kiểu tốt hơn khi tương tác với scene tree:

::

    # Sẽ suy luận biến có kiểu là Sprite2D.
    var my_sprite := $Character as Sprite2D

    # Sẽ thất bại nếu $AnimPlayer không phải là một AnimationPlayer, ngay cả khi nó có method 'play()'.
    ($AnimPlayer as AnimationPlayer).play("walk")

Hằng số
-------

Hằng số là các giá trị bạn không thể thay đổi khi game đang chạy. Giá trị của chúng phải được biết tại thời điểm compile. Sử dụng keyword ``const`` cho phép bạn đặt tên cho một giá trị hằng số. Việc cố gắng gán giá trị cho một hằng số sau khi nó được khai báo sẽ gây ra lỗi.

Chúng tôi khuyến nghị sử dụng hằng số bất cứ khi nào một giá trị không được dự định thay đổi.

::

    const A = 5
    const B = Vector2(20, 20)
    const C = 10 + 20 # Biểu thức hằng số.
    const D = Vector2(20, 30).x # Biểu thức hằng số: 20.
    const E = [1, 2, 3, 4][0] # Biểu thức hằng số: 1.
    const F = sin(20) # 'sin()' có thể được sử dụng trong các biểu thức hằng số.
    const G = x + 20 # Không hợp lệ; đây không phải là biểu thức hằng số!
    const H = A + 20 # Biểu thức hằng số: 25 (`A` là một hằng số).

Mặc dù kiểu của hằng số được suy luận từ giá trị được gán, bạn cũng có thể thêm chỉ định kiểu rõ ràng:

::

    const A: int = 5
    const B: Vector2 = Vector2()

Việc gán một giá trị có kiểu không tương thích sẽ gây ra lỗi.

Bạn cũng có thể tạo hằng số bên trong một function, điều này hữu ích để đặt tên cho các giá trị magic cục bộ.

Enum
~~~~

Enum về cơ bản là cách viết tắt cho các hằng số và khá hữu ích nếu bạn muốn gán các số nguyên liên tiếp cho một số hằng số.

::

    enum {TILE_BRICK, TILE_FLOOR, TILE_SPIKE, TILE_TELEPORT}

    # Tương đương với:
    const TILE_BRICK = 0
    const TILE_FLOOR = 1
    const TILE_SPIKE = 2
    const TILE_TELEPORT = 3


Nếu truyền một tên cho enum, nó sẽ đặt tất cả key vào bên trong một hằng số
:ref:`Dictionary <class_Dictionary>` of that name. This means all constant methods of
Một dictionary cũng có thể được sử dụng với enum có tên. Cách này chỉ hoạt động với enum GDScript, không áp dụng cho enum từ các class dựng sẵn.

.. important:: Keys in a named enum are not registered
               dưới dạng các hằng số global. Chúng nên được truy cập với tiền tố là tên của enum (``Name.KEY``).

::

    enum State {STATE_IDLE, STATE_JUMP = 5, STATE_SHOOT}

    # Tương đương với:
    const State = {STATE_IDLE = 0, STATE_JUMP = 5, STATE_SHOOT = 6}
    # Truy cập các giá trị bằng State.STATE_IDLE, v.v.

    func _ready():
        # Truy cập các giá trị bằng Name.KEY, in ra '5'
        print(State.STATE_JUMP)
        # Sử dụng các method của dictionary:
        # in ra '["STATE_IDLE", "STATE_JUMP", "STATE_SHOOT"]'
        print(State.keys())
        # in ra '{ "STATE_IDLE": 0, "STATE_JUMP": 5, "STATE_SHOOT": 6 }'
        print(State)
        # in ra '[0, 5, 6]'
        print(State.values())

Nếu không gán giá trị cho một key của enum, nó sẽ được gán giá trị trước đó cộng một, hoặc ``0`` nếu đó là entry đầu tiên trong enum. Cho phép nhiều key có cùng giá trị.


Function
--------

Function luôn thuộc về một `class <Classes_>`_. Thứ tự ưu tiên của scope khi tra cứu biến là: local → thành viên class → global. Biến ``self`` luôn khả dụng và được cung cấp như một tùy chọn để truy cập các thành viên class (xem `self`_), nhưng không phải lúc nào cũng cần thiết (và *không được* truyền nó làm đối số đầu tiên của function, không giống Python).

::

    func my_function(a, b):
        print(a)
        print(b)
        return a + b  # Return là tùy chọn; nếu không có, 'null' sẽ được trả về.

Một function có thể ``return`` tại bất kỳ thời điểm nào. Giá trị return mặc định là ``null``.

Theo mặc định, tất cả tham số của function đều bắt buộc. Bạn có thể làm cho một hoặc nhiều tham số ở cuối trở thành tùy chọn bằng cách gán giá trị mặc định cho chúng:

::

    # Vì hai tham số cuối là tùy chọn, tất cả các lời gọi sau đều hợp lệ:
    # - my_function(1)
    # - my_function(1, 20)
    # - my_function(1, 20, 100)
    func my_function(a_required, b_optional = 10, c_optional = 42):
        print(a_required)
        print(b_optional)
        print(c_optional)

Nếu một function chỉ chứa một dòng code, có thể viết function đó trên một dòng:

::

    func square(a): return a * a

    func hello_world(): print("Hello World")

    func empty_function(): pass

Function cũng có thể chỉ định kiểu cho các đối số và giá trị return. Có thể thêm kiểu cho các đối số theo cách tương tự như với biến:

::

    func my_function(a: int, b: String):
        pass

Nếu một đối số của function có giá trị mặc định, có thể suy luận kiểu:

::

    func my_function(int_arg := 42, String_arg := "string"):
        pass

Kiểu return của function có thể được chỉ định sau danh sách đối số bằng token mũi tên (``->``):

::

    func my_int_function() -> int:
        return 0

Các function có kiểu return **phải** trả về một giá trị phù hợp. Đặt kiểu là ``void`` có nghĩa là function không trả về gì. Các function void có thể return sớm bằng keyword ``return``, nhưng không thể return bất kỳ giá trị nào.

::

    func void_function() -> void:
        return # Không thể return một giá trị.

.. note:: Non-void functions must **always** return a value, so if your code has
          branching statements (such as an ``if``/``else`` construct), all the possible paths must have a return. E.g., if you have a ``return`` inside an ``if`` block but not after it, the editor will raise an error because if the block is not executed, the function won't have a valid value to return.

Tham chiếu đến function
~~~~~~~~~~~~~~~~~~~~~~~

Function là các giá trị hạng nhất xét theo object :ref:`Callable <class_Callable>`. Việc tham chiếu đến một function bằng tên mà không gọi nó sẽ tự động tạo ra callable thích hợp. Bạn có thể sử dụng cách này để truyền function làm đối số.

::

    func map(arr: Array, function: Callable) -> Array:
        var result = []
        for item in arr:
            result.push_back(function.call(item))
        return result

    func add1(value: int) -> int:
        return value + 1

    func _ready() -> void:
        var my_array = [1, 2, 3]
        var plus_one = map(my_array, add1)
        print(plus_one) # In ra `[2, 3, 4]`.

.. note::

    Callable **phải** được gọi bằng method :ref:`call() <class_Callable_method_call>`. Bạn không thể sử dụng trực tiếp toán tử ``()``. Hành vi này được triển khai để tránh các vấn đề về hiệu năng khi gọi function trực tiếp.

Function lambda
~~~~~~~~~~~~~~~

Function lambda cho phép bạn khai báo các function không thuộc về class. Thay vào đó, một
:ref:`Callable <class_Callable>` object is created and assigned to a variable directly.
Điều này có thể hữu ích để tạo các callable nhằm truyền đi mà không làm ô nhiễm scope của class.

::

    var lambda = func (x):
        print(x)

Để gọi lambda đã tạo, bạn có thể sử dụng method :ref:`call() <class_Callable_method_call>`:

::

    lambda.call(42) # In ra `42`.

Các hàm lambda có thể được đặt tên cho mục đích debugging (tên này được hiển thị trong Debugger):

::

    var lambda = func my_lambda(x):
        print(x)

Bạn có thể chỉ định type hint cho các hàm lambda theo cách tương tự như đối với các hàm thông thường:

::

    var lambda := func (x: int) -> void:
        print(x)

Lưu ý rằng nếu muốn trả về một giá trị từ hàm lambda, cần có ``return`` tường minh (bạn không thể bỏ qua ``return``):

::

    var lambda = func (x): return x ** 2
    print(lambda.call(2)) # In ra `4`.

Các hàm lambda capture môi trường cục bộ:

::

    var x = 42
    var lambda = func ():
        print(x) # In ra `42`.
    lambda.call()

.. warning::

    Các biến cục bộ được capture theo giá trị một lần tại thời điểm lambda được tạo. Vì vậy, chúng sẽ không được cập nhật trong lambda nếu được gán lại trong hàm bên ngoài:

    ::

        var x = 42
        var lambda = func (): print(x)
        lambda.call() # In ra `42`.
        x = "Hello"
        lambda.call() # In ra `42`.

    Ngoài ra, lambda không thể gán lại một biến cục bộ bên ngoài. Sau khi thoát khỏi lambda, biến này sẽ không thay đổi, vì việc capture của lambda ngầm shadow biến đó:

    ::

        var x = 42
        var lambda = func ():
            print(x) # In ra `42`.
            x = "Hello" # Tạo warning `CONFUSABLE_CAPTURE_REASSIGNMENT`.
            print(x) # In ra `Hello`.
        lambda.call()
        print(x) # In ra `42`.

    Tuy nhiên, nếu bạn sử dụng các kiểu dữ liệu pass-by-reference (array, dictionary và object), thì các thay đổi về nội dung sẽ được chia sẻ cho đến khi bạn gán lại biến:

    ::

        var a = []
        var lambda = func ():
            a.append(1)
            print(a) # In ra `[1]`.
            a = [2] # Tạo warning `CONFUSABLE_CAPTURE_REASSIGNMENT`.
            print(a) # In ra `[2]`.
        lambda.call()
        print(a) # In ra `[1]`.

Các hàm static
~~~~~~~~~~~~~~

Một hàm có thể được khai báo là static. Khi một hàm là static, nó không có quyền truy cập vào các biến thành viên của instance hoặc ``self``. Một hàm static có quyền truy cập vào các biến static. Ngoài ra, các hàm static rất hữu ích để tạo các thư viện gồm những hàm helper:

::

    static func sum2(a, b):
        return a + b

Các hàm lambda không thể được khai báo là static.

Xem thêm `Biến static`_ và `Static constructor`_.

Các hàm variadic
~~~~~~~~~~~~~~~~

Hàm variadic là một hàm có thể nhận số lượng đối số thay đổi. Kể từ Godot 4.5, GDScript hỗ trợ các hàm variadic. Để khai báo một hàm variadic, bạn cần sử dụng *rest parameter*, tham số này thu thập tất cả đối số dư vào một array.

::

    func my_func(a, b = 0, ...args):
        prints(a, b, args)

    func _ready():
        my_func(1)             # 1 0 []
        my_func(1, 2)          # 1 2 []
        my_func(1, 2, 3)       # 1 2 [3]
        my_func(1, 2, 3, 4)    # 1 2 [3, 4]
        my_func(1, 2, 3, 4, 5) # 1 2 [3, 4, 5]

Một hàm có nhiều nhất một rest parameter, và tham số này phải là tham số cuối cùng trong danh sách tham số. Rest parameter không thể có giá trị mặc định. Các hàm static và lambda cũng có thể là variadic.

Static typing cũng hoạt động với các hàm variadic. Tuy nhiên, typed array hiện chưa được hỗ trợ như một kiểu static của rest parameter:

::

    # Bạn không thể chỉ định `...values: Array[int]`.
    func sum(...values: Array) -> int:
        var result := 0
        for value in values:
            assert(value is int)
            result += value
        return result

.. note::

    Mặc dù bạn có thể khai báo các hàm là variadic bằng cách sử dụng rest parameter, việc unpack các tham số khi gọi một hàm bằng *spread syntax* hiện có trong một số ngôn ngữ (JavaScript, PHP) hiện chưa được GDScript hỗ trợ. Tuy nhiên, bạn có thể sử dụng ``callv()`` để gọi một hàm với một array các đối số:

    ::

        func test_func(...args):
            #log_data(...args) # This won't work.
            log_data.callv(args) # Cách này sẽ hoạt động.

        func log_data(...values):
            # Bạn nên sử dụng `callv()` nếu muốn truyền `values` làm danh sách đối số,
            # thay vì truyền array làm đối số đầu tiên.
            prints.callv(values)
            # Bạn có thể sử dụng phép nối array để thêm danh sách đối số vào đầu/cuối.
            write_data.callv(["user://log.txt"] + values)

        func write_data(path, ...values):
            # ...

Các hàm abstract
~~~~~~~~~~~~~~~~

Xem `Abstract class và method`_.

Các statement và control flow
-----------------------------

Các statement là những cấu trúc tiêu chuẩn và có thể là phép gán, lệnh gọi hàm, cấu trúc control flow, v.v. (xem bên dưới). ``;`` làm dấu phân cách statement hoàn toàn là tùy chọn.

Các expression
~~~~~~~~~~~~~~

Expression là các chuỗi operator và toán hạng của chúng theo thứ tự. Bản thân một expression cũng có thể là một statement, mặc dù chỉ các lệnh gọi là hợp lý để sử dụng làm statement vì các expression khác không có side effect.

Expression trả về các giá trị có thể được gán cho những target hợp lệ. Toán hạng của một số operator có thể là một expression khác. Phép gán không phải là một expression và do đó không trả về giá trị nào.

Sau đây là một số ví dụ về expression:

::

    2 + 2 # Phép toán nhị phân.
    -5 # Phép toán một ngôi.
    "okay" if x > 4 else "not okay" # Phép toán ba ngôi.
    x # Identifier đại diện cho biến hoặc hằng số.
    x.a # Truy cập attribute.
    x[4] # Truy cập subscript.
    x > 2 or x < 5 # Các operator so sánh và logic.
    x == y + 2 # Kiểm tra tính bằng nhau.
    do_something() # Lệnh gọi hàm.
    [1, 2, 3] # Định nghĩa array.
    {A = 1, B = 2} # Định nghĩa dictionary.
    preload("res://icon.svg") # Hàm builtin preload.
    self # Tham chiếu đến instance hiện tại.

Identifier, attribute và subscript là các target hợp lệ của phép gán. Các expression khác không thể nằm ở phía bên trái của phép gán.

self
^^^^

``self`` có thể được sử dụng để tham chiếu đến instance hiện tại và thường tương đương với việc tham chiếu trực tiếp đến các symbol khả dụng trong script hiện tại. Tuy nhiên, ``self`` cũng cho phép bạn truy cập các property, method và tên khác được định nghĩa động (tức là được kỳ vọng tồn tại trong các subtype của class hiện tại, hoặc được cung cấp bằng :ref:`_set() <class_Object_private_method__set>` và/hoặc
:ref:`_get() <class_Object_private_method__get>`).

::

    extends Node

    func _ready():
        # Lỗi tại thời điểm compile, vì `my_var` không được định nghĩa trong class hiện tại hoặc các class tổ tiên của nó.
        print(my_var)
        # Được kiểm tra tại runtime, vì vậy có thể hoạt động với các property động hoặc các class hậu duệ.
        print(self.my_var)

        # Lỗi tại thời điểm compile, vì `my_func()` không được định nghĩa trong class hiện tại hoặc các class tổ tiên của nó.
        my_func()
        # Được kiểm tra tại runtime, vì vậy có thể hoạt động với các class hậu duệ.
        self.my_func()

.. warning::

    Hãy cẩn thận: việc truy cập các member của class con trong class cơ sở thường được xem là một practice không tốt, vì điều này làm mờ phạm vi trách nhiệm của từng đoạn code, khiến mối quan hệ tổng thể giữa các phần trong game của bạn khó suy luận hơn. Ngoài ra, bạn có thể đơn giản quên rằng class cha có một số kỳ vọng đối với các class hậu duệ của nó.

if/else/elif
~~~~~~~~~~~~

Simple conditions are created by using the ``if``/``else``/``elif`` syntax. Parenthesis around conditions are allowed, but not required. Given the nature of the tab-based indentation, ``elif`` can be used instead of ``else``/``if`` to maintain a level of indentation.

::

    if (expression):
        statement(s)
    elif (expression):
        statement(s)
    else:
        statement(s)

Các statement ngắn có thể được viết trên cùng dòng với điều kiện:

::

    if 1 + 1 == 2: return 2 + 2
    else:
        var x = 3 + 3
        return x

Đôi khi, bạn có thể muốn gán một giá trị ban đầu khác nhau dựa trên một biểu thức boolean. Trong trường hợp này, expression ternary-if rất hữu ích:

::

    var x = (value) if (expression) else (value)
    y += 3 if y < 10 else -1

Các expression ternary-if có thể được lồng nhau để xử lý hơn 2 trường hợp. Khi lồng các expression ternary-if, bạn nên đặt toàn bộ expression trên nhiều dòng để duy trì khả năng đọc:

::

    var count = 0

    var fruit = (
            "apple" if count == 2
            else "pear" if count == 1
            else "banana" if count == 0
            else "orange"
    )
    print(fruit)  # banana

    # Cú pháp thay thế sử dụng dấu gạch chéo ngược thay vì dấu ngoặc (cho các expression nhiều dòng).
    # Cần ít dòng hơn nhưng khó refactor hơn.
    var fruit_alt = \
            "apple" if count == 2 \
            else "pear" if count == 1 \
            else "banana" if count == 0 \
            else "orange"
    print(fruit_alt)  # banana

Bạn cũng có thể muốn kiểm tra xem một giá trị có nằm trong một thứ gì đó hay không. Bạn có thể sử dụng một statement ``if`` kết hợp với operator ``in`` để thực hiện việc này:

::

    # Kiểm tra xem một chữ cái có nằm trong một string hay không.
    var text = "abc"
    if 'b' in text: print("The string contains b")

    # Kiểm tra xem một biến có nằm trong một node hay không.
    if "varName" in get_parent(): print("varName is defined in parent!")

while
~~~~~

Các loop đơn giản được tạo bằng cú pháp ``while``. Có thể dừng loop bằng ``break`` hoặc tiếp tục bằng ``continue`` (lệnh này chuyển đến iteration tiếp theo của loop mà không thực thi thêm code nào trong iteration hiện tại):

::

    while (expression):
        statement(s)

for
~~~

Để lặp qua một range, chẳng hạn như array hoặc table, người ta sử dụng loop *for*. Khi lặp qua một array, phần tử array hiện tại được lưu trong biến loop. Khi lặp qua một dictionary, *key* được lưu trong biến loop.

::

    for x in [5, 7, 11]:
        statement # Loop lặp 3 lần với 'x' lần lượt là 5, 7 và cuối cùng là 11.

    var names = ["John", "Marta", "Samantha", "Jimmy"]
    for name: String in names: # Biến loop có kiểu.
        print(name) # In nội dung của name.

    var dict = {"a": 0, "b": 1, "c": 2}
    for i in dict:
        print(dict[i]) # In lần lượt 0, rồi 1, rồi 2.

    for i in range(3):
        statement # Tương tự [0, 1, 2] nhưng không cấp phát một array.

    for i in range(1, 3):
        statement # Tương tự [1, 2] nhưng không cấp phát một array.

    for i in range(2, 8, 2):
        statement # Tương tự [2, 4, 6] nhưng không cấp phát một array.

    for i in range(8, 2, -2):
        statement # Tương tự [8, 6, 4] nhưng không cấp phát một array.

    for c in "Hello":
        print(c) # Lặp qua tất cả ký tự trong một String, in từng chữ cái trên một dòng mới.

    for i in 3:
        statement # Tương tự range(3).

    for i in 2.2:
        statement # Tương tự range(ceil(2.2)).

Nếu muốn gán giá trị cho các phần tử trong array khi đang lặp qua array, tốt nhất nên sử dụng ``for i in array.size()``.

::

    for i in array.size():
        array[i] = "Hello World"


Biến loop là biến cục bộ của for-loop và việc gán cho biến này sẽ không thay đổi giá trị trong array. Các object được truyền theo reference (chẳng hạn như node) vẫn có thể được thao tác bằng cách gọi method trên biến loop.

::

    for string in string_array:
        string = "Hello World" # Điều này không có tác dụng

    for node in node_array:
        node.add_to_group("Cool_Group") # Điều này có tác dụng

khớp
~~~~

Câu lệnh ``match`` được dùng để phân nhánh quá trình thực thi của một chương trình. Nó tương đương với câu lệnh ``switch`` có trong nhiều ngôn ngữ khác, nhưng cung cấp thêm một số tính năng.

.. warning::

    ``match`` kiểm tra kiểu nghiêm ngặt hơn toán tử ``==``. Ví dụ, ``1`` sẽ **không** khớp với ``1.0``. Ngoại lệ duy nhất là khi so khớp ``String`` với ``StringName``: ví dụ, String ``"hello"`` được xem là bằng với StringName ``&"hello"``.

Cú pháp cơ bản
^^^^^^^^^^^^^^

::

    match <test value>:
        <pattern(s)>:
            <block>
        <pattern(s)> when <pattern guard>:
            <block>
        <...>

Tóm tắt nhanh cho những người đã quen với các câu lệnh switch
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Replace ``switch`` with ``match``. 2. Remove ``case``. 3. Remove any ``break``\ s. 4. Change ``default`` to a single underscore.

Luồng điều khiển
^^^^^^^^^^^^^^^^

Các pattern được so khớp từ trên xuống dưới. Nếu một pattern khớp, block tương ứng đầu tiên sẽ được thực thi. Sau đó, quá trình thực thi tiếp tục bên dưới câu lệnh ``match``.

.. note::

    Hành vi ``continue`` đặc biệt trong ``match`` được hỗ trợ ở phiên bản 3.x đã bị loại bỏ trong Godot 4.0.

Các loại pattern sau đây được cung cấp:

- Literal pattern Khớp với một `literal <Literals_>`_:

    ::

        match x:
            1:
                print("We are number one!")
            2:
                print("Two are better than one!")
            "test":
                print("Oh snap! It's a string!")

- Expression pattern Khớp với một biểu thức hằng, một identifier hoặc một attribute access (``A.B``):

    ::

        match typeof(x):
            TYPE_FLOAT:
                print("float")
            TYPE_STRING:
                print("text")
            TYPE_ARRAY:
                print("array")

- Wildcard pattern Pattern này khớp với mọi thứ. Nó được viết bằng một dấu gạch dưới duy nhất.

    Có thể dùng nó tương đương với ``default`` trong câu lệnh ``switch`` ở các ngôn ngữ khác:

    ::

        match x:
            1:
                print("It's one!")
            2:
                print("It's one times two!")
            _:
                print("It's not 1 or 2. I don't care to be honest.")

- Binding pattern Binding pattern khai báo một biến mới. Giống như wildcard pattern, nó khớp với mọi thứ — đồng thời đặt tên cho giá trị đó. Pattern này đặc biệt hữu ích với array pattern và dictionary pattern:

    ::

        match x:
            1:
                print("It's one!")
            2:
                print("It's one times two!")
            var new_var:
                print("It's not 1 or 2, it's ", new_var)

- Array pattern Khớp với một array. Mỗi phần tử trong array pattern bản thân nó đều là một pattern, vì vậy bạn có thể lồng chúng vào nhau.

    Trước tiên, độ dài của array được kiểm tra; nó phải có cùng kích thước với pattern, nếu không pattern sẽ không khớp.

    **Array mở**: Một array có thể lớn hơn pattern bằng cách đặt subpattern cuối cùng là ``..``.

    Mỗi subpattern phải được phân tách bằng dấu phẩy.

    ::

        match x:
            []:
                print("Empty array")
            [1, 3, "test", null]:
                print("Very specific array")
            [var start, _, "test"]:
                print("First element is ", start, ", and the last is \"test\"")
            [42, ..]:
                print("Open ended array")

- Dictionary pattern Hoạt động giống như array pattern. Mỗi key phải là một constant pattern.

    Trước tiên, kích thước của dictionary được kiểm tra; nó phải bằng kích thước của pattern, nếu không pattern sẽ không khớp.

    **Dictionary mở**: Một dictionary có thể lớn hơn pattern bằng cách đặt subpattern cuối cùng là ``..``.

    Mỗi subpattern phải được phân tách bằng dấu phẩy.

    Nếu bạn không chỉ định một value, thì chỉ sự tồn tại của key được kiểm tra.

    Một value pattern được phân tách khỏi key pattern bằng ``:``.

    ::

        match x:
            {}:
                print("Empty dict")
            {"name": "Dennis"}:
                print("The name is Dennis")
            {"name": "Dennis", "age": var age}:
                print("Dennis is ", age, " years old.")
            {"name", "age"}:
                print("Has a name and an age, but it's not Dennis :(")
            {"key": "godotisawesome", ..}:
                print("I only checked for one entry and ignored the rest")

- Multiple patterns Bạn cũng có thể chỉ định nhiều pattern, được phân tách bằng dấu phẩy. Các pattern này không được phép chứa binding nào.

    ::

        match x:
            1, 2, 3:
                print("It's 1 - 3")
            "Sword", "Splash potion", "Fist":
                print("Yep, you've taken damage")

Pattern guard
^^^^^^^^^^^^^

*Pattern guard* là một điều kiện tùy chọn đi sau danh sách pattern, cho phép bạn thực hiện thêm các kiểm tra trước khi chọn một nhánh ``match``. Không giống pattern, pattern guard có thể là một biểu thức bất kỳ.

Mỗi ``match`` chỉ có thể thực thi một nhánh. Khi một nhánh được chọn, các nhánh còn lại sẽ không được kiểm tra. Nếu bạn muốn dùng cùng một pattern cho nhiều nhánh hoặc ngăn việc chọn một nhánh có pattern quá tổng quát, bạn có thể chỉ định pattern guard sau danh sách pattern bằng từ khóa ``when``:

::

    match point:
        [0, 0]:
            print("Origin")
        [_, 0]:
            print("Point on X-axis")
        [0, _]:
            print("Point on Y-axis")
        [var x, var y] when y == x:
            print("Point on line y = x")
        [var x, var y] when y == -x:
            print("Point on line y = -x")
        [var x, var y]:
            print("Point (%s, %s)" % [x, y])

- Nếu không có pattern nào khớp với nhánh hiện tại, pattern guard sẽ **không** được đánh giá và các pattern của nhánh tiếp theo sẽ được kiểm tra. - Nếu tìm thấy một pattern khớp, pattern guard sẽ được đánh giá.

  - Nếu kết quả là true, phần thân của nhánh sẽ được thực thi và ``match`` kết thúc. - Nếu kết quả là false, các pattern của nhánh tiếp theo sẽ được kiểm tra.

Class
-----

Theo mặc định, tất cả các script file đều là class không có tên. Trong trường hợp này, bạn chỉ có thể tham chiếu đến chúng bằng path của file, sử dụng path tương đối hoặc tuyệt đối. Ví dụ, nếu bạn đặt tên cho một script file là ``character.gd``:

::

   # Kế thừa từ 'character.gd'.

   extends "res://path/to/character.gd"

   # Load character.gd và tạo một node instance mới từ đó.

   var Character = load("res://path/to/character.gd")
   var character_node = Character.new()

.. _doc_gdscript_basics_class_name:

Đăng ký named class
~~~~~~~~~~~~~~~~~~~

Bạn có thể đặt tên cho class để đăng ký nó thành một type mới trong editor của Godot. Để làm vậy, bạn dùng từ khóa ``class_name``. Bạn cũng có thể dùng annotation ``@icon`` với path đến một image để sử dụng image đó làm icon. Khi đó, class của bạn sẽ xuất hiện cùng icon mới trong editor:

::

   # item.gd

   @icon("res://interface/icons/item.png")
   class_name Item
   extends Node

.. image:: img/class_name_editor_register_example.png

.. tip::

    Các image SVG được dùng làm icon tùy chỉnh cho node nên có **Editor > Scale With Editor Scale** và **Editor > Convert Icons With Editor Theme**
    :ref:`import options <doc_importing_images_editor_import_options>` enabled. This allows
    để các icon tuân theo cài đặt scale và theme của editor nếu chúng được thiết kế với cùng bảng màu như các icon riêng của Godot.

Sau đây là một ví dụ về class file:

::

    # Được lưu dưới dạng file có tên 'character.gd'.

    class_name Character


    var health = 5


    func print_health():
        print(health)


    func print_this_script_three_times():
        print(get_script())
        print(ResourceLoader.load("res://character.gd"))
        print(Character)

Nếu bạn cũng muốn sử dụng ``extends``, bạn có thể đặt cả hai trên cùng một dòng:

::

    class_name MyNode extends Node

Named class được đăng ký trên toàn cục, nghĩa là chúng có thể được dùng trong các script khác mà không cần ``load`` hoặc ``preload`` chúng:

::

    var player

    func _ready():
        player = Character.new()

.. note::

    Godot khởi tạo các biến không static mỗi lần bạn tạo một instance, bao gồm cả array và dictionary. Điều này phù hợp với nguyên tắc an toàn luồng (thread safety), vì các script có thể được khởi tạo trong những thread riêng biệt mà người dùng không biết.

.. warning::

    Editor của Godot sẽ ẩn các custom class có tên bắt đầu bằng tiền tố "Editor" trong các cửa sổ hộp thoại 'Create New Node' hoặc 'Create New Scene'. Các class này vẫn có thể được khởi tạo trong runtime thông qua tên class, nhưng sẽ tự động bị các cửa sổ editor ẩn đi cùng với các editor node tích hợp được editor của Godot sử dụng.

.. _doc_gdscript_basics_abstract_class:

Abstract class và method
~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.5, bạn có thể định nghĩa abstract class và method bằng annotation ``@abstract``.

Abstract class là một class không thể được khởi tạo trực tiếp. Thay vào đó, nó được dùng để các class khác kế thừa. Việc cố khởi tạo một abstract class sẽ dẫn đến lỗi.

Abstract method là một method không có phần triển khai. Vì vậy, sau function header phải có newline hoặc dấu chấm phẩy. Điều này định nghĩa một contract mà các class kế thừa phải tuân theo, vì method signature phải tương thích khi override.

Các class kế thừa phải cung cấp phần triển khai cho tất cả abstract method, hoặc class kế thừa phải được đánh dấu là abstract. Nếu một class có ít nhất một abstract method (do chính class đó định nghĩa hoặc được kế thừa nhưng chưa triển khai), thì class đó cũng phải được đánh dấu là abstract. Tuy nhiên, điều ngược lại không đúng: một abstract class được phép không có abstract method nào.

.. tip::

    Nếu bạn muốn khai báo một method là tùy chọn để override, bạn nên dùng một method không phải abstract và cung cấp phần triển khai mặc định.

Ví dụ, bạn có thể có một abstract class tên là ``Shape`` định nghĩa một abstract method tên là ``draw()``. Sau đó, bạn có thể tạo các subclass như ``Circle`` và ``Square`` triển khai method ``draw()`` theo cách riêng của chúng. Điều này cho phép bạn định nghĩa một *interface* chung cho mọi shape mà không cần triển khai toàn bộ chi tiết ngay trong abstract class:

::

    @abstract class Shape:
        @abstract func draw()

    # Đây là một subclass cụ thể (không phải abstract) của Shape.
    # Bạn **phải** triển khai tất cả abstract method trong các concrete class.
    class Circle extends Shape:
        func draw():
            print("Drawing a circle.")

    class Square extends Shape:
        func draw():
            print("Drawing a square.")

Cả inner class và class được tạo bằng ``class_name`` đều có thể là abstract. Ví dụ này tạo ra hai abstract class, trong đó một class là subclass của abstract class còn lại:

::

    @abstract
    class_name AbstractClass
    extends Node

    @abstract class AbstractInnerClass:
        func _ready():
            pass

    # Đây là một ví dụ về concrete subclass của `AbstractInnerClass`.
    # Class này có thể được khởi tạo bằng `AbstractClass.ConcreteInnerClass.new()`
    # trong các script khác, dù nó là một phần của script `class_name` abstract.
    class ConcreteInnerClass extends AbstractInnerClass:
        func _ready():
            print("Concrete class ready.")

.. warning::

    Vì abstract class không thể được khởi tạo, nên không thể gắn abstract class vào một node. Nếu bạn cố làm vậy, engine sẽ in ra lỗi khi chạy scene:

    .. code-block:: none

        Cannot set object script. Script '<path to script>' should not be abstract.

Các class không có tên cũng có thể được định nghĩa là abstract; annotation ``@abstract`` phải đứng trước ``extends``:

::

    @abstract
    extends Node

Inheritance
~~~~~~~~~~~

Một class (được lưu dưới dạng file) có thể kế thừa từ:

- Một global class. - Một class file khác. - Một inner class bên trong class file khác.

Không cho phép multiple inheritance.

Inheritance sử dụng từ khóa ``extends``:

::

    # Kế thừa/mở rộng một class có sẵn trên toàn cục.
    extends SomeClass

    # Kế thừa/mở rộng một class file có tên.
    extends "somefile.gd"

    # Kế thừa/mở rộng một inner class trong file khác.
    extends "somefile.gd".SomeInnerClass

.. note::

    Nếu tính kế thừa không được định nghĩa rõ ràng, lớp sẽ mặc định kế thừa
    :ref:`class_RefCounted`.

Để kiểm tra xem một instance đã cho có kế thừa từ một lớp đã cho hay không, có thể sử dụng từ khóa ``is``:

::

    # Lưu vào cache lớp enemy.
    const Enemy = preload("enemy.gd")

    # [...]

    # Sử dụng 'is' để kiểm tra tính kế thừa.
    if entity is Enemy:
        entity.apply_damage()

To call a function in a *super class* (i.e. one ``extend``-ed in your current class), use the ``super`` keyword:

::

    super(args)

Điều này đặc biệt hữu ích vì các hàm trong các lớp mở rộng sẽ thay thế các hàm có cùng tên trong super class của chúng. Nếu bạn vẫn muốn gọi chúng, bạn có thể sử dụng ``super``:

::

    func some_func(x):
        super(x) # Gọi cùng một hàm trên super class.

Nếu cần gọi một hàm khác từ super class, bạn có thể chỉ định tên hàm bằng toán tử thuộc tính:

::

    func overriding():
        return 0 # Điều này ghi đè method trong base class.

    func dont_override():
        return super.overriding() # Điều này gọi method như được định nghĩa trong base class.

.. warning::

    Một trong những hiểu lầm phổ biến là cố gắng ghi đè các method engine *non-virtual* như ``get_class()``, ``queue_free()``, v.v. Điều này không được hỗ trợ vì lý do kỹ thuật.

    Trong Godot 3, bạn có thể *shadow* các method engine trong GDScript, và nó sẽ hoạt động nếu bạn gọi method này trong GDScript. Tuy nhiên, engine sẽ **không** thực thi code của bạn nếu method được gọi bên trong engine khi xảy ra một sự kiện nào đó.

    Trong Godot 4, ngay cả shadowing cũng có thể không phải lúc nào cũng hoạt động, vì GDScript tối ưu hóa các native method call. Do đó, chúng tôi đã thêm cảnh báo ``NATIVE_METHOD_OVERRIDE``, cảnh báo này mặc định được xử lý như một lỗi. Chúng tôi đặc biệt khuyến nghị không tắt hoặc bỏ qua cảnh báo này.

    Lưu ý rằng điều này không áp dụng cho các virtual method như ``_ready()``, ``_process()`` và các method khác (được đánh dấu bằng qualifier ``virtual`` trong tài liệu và tên bắt đầu bằng dấu gạch dưới). Các method này được thiết kế riêng để tùy chỉnh hành vi của engine và có thể được ghi đè trong GDScript. Signals và notifications cũng có thể hữu ích cho các mục đích này.

Class constructor
~~~~~~~~~~~~~~~~~

Class constructor, được gọi khi khởi tạo class, có tên là ``_init``. Nếu muốn gọi constructor của base class, bạn cũng có thể sử dụng cú pháp ``super``. Lưu ý rằng mọi class đều có một constructor ngầm định luôn được gọi (để định nghĩa các giá trị mặc định của biến class). ``super`` được sử dụng để gọi constructor tường minh:

::

    func _init(arg):
       super("some_default", arg) # Gọi custom base constructor.

Điều này được giải thích rõ hơn qua các ví dụ. Hãy xét kịch bản sau:

::

    # state.gd (inherited class).
    var entity = null
    var message = null


    func _init(e = null):
        entity = e


    func enter(m):
        message = m


    # idle.gd (inheriting class).
    extends "state.gd"


    func _init(e = null, m = null):
        super(e)
        # Thực hiện thao tác nào đó với 'e'.
        message = m

Có một vài điều cần ghi nhớ ở đây:

1. If the inherited class (``state.gd``) defines an ``_init`` constructor that takes arguments (``e`` in this case), then the inheriting class (``idle.gd``) *must* define ``_init`` as well and pass appropriate parameters to ``_init`` from ``state.gd``. 2. ``idle.gd`` can have a different number of arguments than the base class ``state.gd``. 3. In the example above, ``e`` passed to the ``state.gd`` constructor is the same ``e`` passed in to ``idle.gd``. 4. If ``idle.gd``'s ``_init`` constructor takes 0 arguments, it still needs to pass some value to the ``state.gd`` base class, even if it does nothing. This brings us to the fact that you can pass expressions to the base constructor as well, not just variables, e.g.:

::

    # idle.gd

    func _init():
        super(5)

Static constructor
~~~~~~~~~~~~~~~~~~

Static constructor là một static function ``_static_init`` được tự động gọi khi class được tải, sau khi các static variable đã được khởi tạo:

::

    static var my_static_var = 1

    static func _static_init():
        my_static_var = 2

Static constructor không thể nhận đối số và không được trả về bất kỳ giá trị nào.

.. _doc_gdscript_basics_inner_classes:

Inner classes
~~~~~~~~~~~~~

Một class file có thể chứa các inner class. Inner class được định nghĩa bằng từ khóa ``class``. Chúng được khởi tạo bằng function ``ClassName.new()``.

::

    # Bên trong một class file.

    # Một inner class trong class file này.
    class SomeInnerClass:
        var a = 5


        func print_value_of_a():
            print(a)


    # Đây là constructor của main class trong class file.
    func _init():
        var c = SomeInnerClass.new()
        c.print_value_of_a()

.. _doc_gdscript_classes_as_resources:

Classes as resources
~~~~~~~~~~~~~~~~~~~~

Các class được lưu dưới dạng file được xem là :ref:`GDScripts <class_GDScript>`. Chúng phải được tải từ disk để có thể truy cập trong các class khác. Việc này được thực hiện bằng function ``load`` hoặc ``preload`` (xem bên dưới). Việc khởi tạo một class resource đã tải được thực hiện bằng cách gọi function ``new`` trên class object:

::

    # Tải class resource khi gọi load().
    var MyClass = load("myclass.gd")

    # Preload class chỉ một lần tại compile time.
    const MyClass = preload("myclass.gd")


    func _init():
        var a = MyClass.new()
        a.some_function()

Exports
-------

.. note::

    Tài liệu về exports đã được chuyển đến :ref:`doc_gdscript_exports`.


.. _doc_gdscript_basics_setters_getters:

Properties (setters và getters)
-------------------------------

Đôi khi, bạn muốn member variable của một class làm được nhiều hơn việc chỉ lưu dữ liệu và thực hiện một số validation hoặc computation mỗi khi giá trị của nó thay đổi. Bạn cũng có thể muốn đóng gói quyền truy cập vào nó theo một cách nào đó.

Để thực hiện việc này, GDScript cung cấp cú pháp đặc biệt để định nghĩa properties bằng các keyword ``set`` và ``get`` sau khai báo biến. Sau đó, bạn có thể định nghĩa một code block sẽ được thực thi khi biến được truy cập hoặc gán giá trị.

Ví dụ:

::

    var milliseconds: int = 0
    var seconds: int:
        get:
            return milliseconds / 1000
        set(value):
            milliseconds = value * 1000

.. note::

    Không giống ``setget`` trong các phiên bản Godot trước đây, các method ``set`` và ``get`` **luôn** được gọi (trừ các trường hợp được lưu ý bên dưới), ngay cả khi được truy cập bên trong cùng class (có hoặc không có tiền tố ``self.``). Điều này giúp hành vi nhất quán. Nếu cần truy cập trực tiếp vào giá trị, hãy sử dụng một biến khác để truy cập trực tiếp và để code property sử dụng tên đó.

Cú pháp thay thế
~~~~~~~~~~~~~~~~

Ngoài ra còn có một cách ký hiệu khác để sử dụng các function class hiện có nếu bạn muốn tách code khỏi khai báo biến hoặc cần tái sử dụng code trên nhiều property (nhưng bạn không thể phân biệt setter/getter nào đang được gọi cho property nào):

::

    var my_prop:
        get = get_my_prop, set = set_my_prop

Điều này cũng có thể được thực hiện trên cùng một dòng:

::

    var my_prop: get = get_my_prop, set = set_my_prop

Setter và getter phải sử dụng cùng một cách ký hiệu; không cho phép trộn các kiểu cho cùng một biến.

.. note::

    Bạn không thể chỉ định type hint cho setter và getter *inline*. Điều này được thực hiện có chủ ý để giảm boilerplate. Nếu biến được định kiểu, đối số của setter sẽ tự động có cùng kiểu, và giá trị trả về của getter phải khớp với kiểu đó. Các function setter/getter tách biệt có thể có type hint, và kiểu đó phải khớp với kiểu của biến hoặc là một kiểu rộng hơn.

Khi setter/getter không được gọi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi một biến được khởi tạo, giá trị của initializer sẽ được ghi trực tiếp vào biến. Điều này xảy ra ngay cả khi annotation ``@onready`` hoặc ``@export`` được áp dụng cho biến.

Việc sử dụng tên của biến để gán giá trị cho nó bên trong setter của chính nó hoặc lấy giá trị bên trong getter của chính nó sẽ truy cập trực tiếp vào member underlying. Điều này ngăn đệ quy vô hạn và giúp bạn không phải khai báo rõ ràng một biến khác:

::

    signal changed(new_value)
    var warns_when_changed = "some value":
        get:
            return warns_when_changed
        set(value):
            changed.emit(value)
            warns_when_changed = value

Điều này cũng áp dụng cho cú pháp thay thế:

::

    var my_prop: set = set_my_prop

    func set_my_prop(value):
        my_prop = value # Không có đệ quy vô hạn.

.. warning::

    Ngoại lệ **không** lan truyền đến các function khác được gọi trong setter/getter. Ví dụ, đoạn code sau **sẽ** gây ra đệ quy vô hạn:

::

        var my_prop:
            set(value):
                set_my_prop(value)

        func set_my_prop(value):
            my_prop = value # Đệ quy vô hạn, vì `set_my_prop()` không phải là setter.

.. _doc_gdscript_tool_mode:

Tool mode
---------

Theo mặc định, script không chạy bên trong editor và chỉ có thể thay đổi các exported property. Trong một số trường hợp, bạn muốn chúng chạy bên trong editor (miễn là chúng không thực thi game code hoặc tự tránh làm như vậy). Để thực hiện việc này, annotation ``@tool`` tồn tại và phải được đặt ở đầu file:

::

    @tool
    extends Button

    func _ready():
        print("Hello")


Xem :ref:`doc_running_code_in_the_editor` để biết thêm thông tin.

.. warning:: Be cautious when freeing nodes with ``queue_free()`` or ``free()``
             trong một tool script (đặc biệt là chính owner của script). Vì tool script chạy code của chúng trong editor, việc sử dụng sai có thể khiến editor bị crash.

.. _doc_gdscript_basics_memory_management:

Quản lý bộ nhớ
--------------

Godot triển khai reference counting để giải phóng một số instance không còn được sử dụng, thay vì sử dụng garbage collector hoặc yêu cầu quản lý hoàn toàn thủ công. Mọi instance của class :ref:`class_RefCounted` (hoặc bất kỳ class nào kế thừa nó, chẳng hạn như :ref:`class_Resource`) sẽ được tự động giải phóng khi không còn được sử dụng. Đối với instance của bất kỳ class nào không phải là :ref:`class_RefCounted` (chẳng hạn như :ref:`class_Node` hoặc kiểu :ref:`class_Object` cơ sở), nó sẽ vẫn tồn tại trong bộ nhớ cho đến khi được xóa bằng ``free()`` (hoặc ``queue_free()`` đối với Nodes).

.. note::

    Nếu một :ref:`class_Node` bị xóa thông qua ``free()`` hoặc ``queue_free()``, tất cả các child của nó cũng sẽ bị xóa đệ quy.

Để tránh các reference cycle không thể được giải phóng, một
:ref:`weakref() <class_@GlobalScope_method_weakref>` function is provided for
việc tạo weak reference, cho phép truy cập vào object mà không ngăn cản một
:ref:`class_RefCounted` from freeing. Here is an example:


::

    extends Node

    var my_file_ref

    func _ready():
        var f = FileAccess.open("user://example_file.json", FileAccess.READ)
        my_file_ref = weakref(f)
        # class FileAccess kế thừa RefCounted, vì vậy nó sẽ được giải phóng khi không được sử dụng

        # WeakRef sẽ không ngăn f bị giải phóng khi other_node hoàn tất
        other_node.use_file(f)

    func _this_is_called_later():
        var my_file = my_file_ref.get_ref()
        if my_file:
            my_file.close()

Ngoài ra, khi không sử dụng các reference, có thể dùng ``is_instance_valid(instance)`` để kiểm tra xem một object đã được giải phóng hay chưa.

.. _doc_gdscript_signals:

Signals
-------

Signals là một công cụ để phát message từ một object mà các object khác có thể phản hồi. Để tạo signal tùy chỉnh cho một class, hãy dùng keyword ``signal``.

::

   extends Node


   # Một signal có tên health_depleted.
   signal health_depleted

.. note::

   Signals là một cơ chế `Callback <https://en.wikipedia.org/wiki/Callback_(computer_programming)>`_. Chúng cũng đảm nhiệm vai trò của Observers, một programming pattern phổ biến. Để biết thêm thông tin, hãy đọc `Observer tutorial <https://gameprogrammingpatterns.com/observer.html>`_ trong ebook Game Programming Patterns.

Bạn có thể kết nối các signal này với các method giống như cách bạn kết nối các signal tích hợp sẵn của những node như :ref:`class_Button` hoặc :ref:`class_RigidBody3D`.

Trong ví dụ dưới đây, chúng ta kết nối signal ``health_depleted`` từ một node ``Character`` với một node ``Game``. Khi node ``Character`` phát signal, ``_on_character_health_depleted`` của game node sẽ được gọi:

::

    # game.gd

    func _ready():
        var character_node = get_node('Character')
        character_node.health_depleted.connect(_on_character_health_depleted)


    func _on_character_health_depleted():
        get_tree().reload_current_scene()

Bạn có thể phát bao nhiêu argument tùy ý cùng với một signal.

Sau đây là một ví dụ cho thấy điều này hữu ích. Giả sử chúng ta muốn một thanh máu trên màn hình phản hồi các thay đổi về health bằng một animation, nhưng muốn giữ giao diện người dùng tách biệt với player trong scene tree.

Trong script ``character.gd``, chúng ta định nghĩa một signal ``health_changed`` và phát nó bằng :ref:`Signal.emit() <class_Signal_method_emit>`, còn từ một node ``Game`` ở vị trí cao hơn trong scene tree, chúng ta kết nối nó với ``Lifebar`` bằng method :ref:`Signal.connect() <class_Signal_method_connect>`:

::

    # character.gd

    ...
    signal health_changed


    func take_damage(amount):
        var old_health = health
        health -= amount

        # Chúng ta phát signal health_changed mỗi khi
        # character nhận damage.
        health_changed.emit(old_health, health)
    ...

::

    # lifebar.gd

    # Ở đây, chúng ta định nghĩa một function để dùng làm callback khi
    # signal health_changed của character được phát.

    ...
    func _on_Character_health_changed(old_value, new_value):
        if old_value > new_value:
            progress_bar.modulate = Color.RED
        else:
            progress_bar.modulate = Color.GREEN

        # Hãy tưởng tượng `animate` là một function do người dùng định nghĩa, dùng để tạo animation cho
        # thanh đầy lên hoặc cạn đi.
        progress_bar.animate(old_value, new_value)
    ...

Trong node ``Game``, chúng ta lấy cả hai node ``Character`` và ``Lifebar``, sau đó kết nối character, node phát signal, với receiver, trong trường hợp này là node ``Lifebar``.

::

    # game.gd

    func _ready():
        var character_node = get_node('Character')
        var lifebar_node = get_node('UserInterface/Lifebar')

        character_node.health_changed.connect(lifebar_node._on_Character_health_changed)

Điều này cho phép ``Lifebar`` phản hồi các thay đổi về health mà không tạo coupling với node ``Character``.

Bạn có thể viết tên các argument tùy chọn trong dấu ngoặc đơn sau phần định nghĩa signal:

::

    # Định nghĩa một signal chuyển tiếp hai argument.
    signal health_changed(old_value, new_value)

Các argument này sẽ xuất hiện trong Signals dock của editor, và Godot có thể dùng chúng để tạo các callback function cho bạn. Tuy nhiên, bạn vẫn có thể phát số lượng argument bất kỳ khi phát signal; bạn có trách nhiệm phát đúng các value.

.. image:: img/gdscript_basics_signals_node_tab_1.png

Bạn cũng có thể tạo các bản sao của GDScript Callable object chấp nhận các argument bổ sung bằng :ref:`Callable.bind() <class_Callable_method_bind>`. Điều này cho phép bạn thêm thông tin vào connection nếu bản thân signal được phát không cung cấp quyền truy cập vào tất cả dữ liệu bạn cần.

Khi signal được phát, callback method sẽ nhận các value đã bind, ngoài những value do signal cung cấp.

Dựa trên ví dụ trên, giả sử chúng ta muốn hiển thị log về damage mà mỗi character nhận trên màn hình, như ``Player1 took 22 damage.``. Signal ``health_changed`` không cung cấp cho chúng ta tên của character đã nhận damage. Vì vậy, khi kết nối signal với in-game console, chúng ta có thể thêm tên của character bằng method bind:

::

    # game.gd

    func _ready():
        var character_node = get_node('Character')
        var battle_log_node = get_node('UserInterface/BattleLog')

        character_node.health_changed.connect(battle_log_node._on_Character_health_changed.bind(character_node.name))

Node ``BattleLog`` của chúng ta nhận mỗi element đã bind làm một argument bổ sung:

::

    # battle_log.gd

    func _on_Character_health_changed(old_value, new_value, character_name):
        if not new_value <= old_value:
            return

        var damage = old_value - new_value
        label.text += character_name + " took " + str(damage) + " damage."


Chờ signals hoặc coroutines
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Keyword ``await`` có thể được dùng để tạo `coroutines <https://en.wikipedia.org/wiki/Coroutine>`_, chúng sẽ chờ cho đến khi một signal được phát trước khi tiếp tục thực thi. Việc dùng keyword ``await`` với một signal hoặc một lời gọi đến function cũng là một coroutine sẽ ngay lập tức trả quyền điều khiển về caller. Khi signal được phát (hoặc coroutine được gọi hoàn tất), nó sẽ tiếp tục thực thi từ điểm đã dừng.

Ví dụ, để dừng thực thi cho đến khi người dùng nhấn một button, bạn có thể làm như sau:

::

    func wait_confirmation():
        print("Prompting user")
        await $Button.button_up # Chờ signal button_up từ node Button.
        print("User confirmed")
        return true

Trong trường hợp này, ``wait_confirmation`` trở thành một coroutine, nghĩa là caller cũng cần await nó:

::

    func request_confirmation():
        print("Will ask the user")
        var confirmed = await wait_confirmation()
        if confirmed:
            print("User confirmed")
        else:
            print("User cancelled")

Lưu ý rằng việc yêu cầu return value của một coroutine mà không có ``await`` sẽ gây ra lỗi:

::

    func wrong():
        var confirmed = wait_confirmation() # Sẽ gây ra lỗi.

Tuy nhiên, nếu bạn không phụ thuộc vào result, bạn chỉ cần gọi nó bất đồng bộ (asynchronously), thao tác này sẽ không dừng việc thực thi và không biến function hiện tại thành một coroutine:

::

    func okay():
        wait_confirmation()
        print("This will be printed immediately, before the user press the button.")

Nếu bạn dùng ``await`` với một expression không phải là signal hay coroutine, value sẽ được trả về ngay lập tức và function sẽ không trả quyền điều khiển lại cho caller:

::

    func no_wait():
        var x = await get_five()
        print("This doesn't make this function a coroutine.")

    func get_five():
        return 5

Điều này cũng có nghĩa là việc trả về một signal từ một function không phải là coroutine sẽ khiến caller await signal đó:

::

    func get_signal():
        return $Button.button_up

    func wait_button():
        await get_signal()
        print("Button was pressed")

.. note:: Unlike ``yield`` in previous Godot versions, you cannot obtain the function state object.
          Điều này được thực hiện để đảm bảo type safety. Khi có type safety này, một function không thể nói rằng nó trả về ``int`` trong khi trên thực tế lại trả về một function state object trong runtime.

Bạn có thể lưu các argument được truyền vào các parameter của signal. Nếu chỉ có một parameter, value được await sẽ có cùng type với argument:

::

    func toggled():
        var signal_args = await $Button.toggled
        assert(typeof(signal_args) == TYPE_BOOL)

Nếu có nhiều hơn một parameter, value được await sẽ có type ``Array``:

::

    func request_completed():
        var signal_args = await $HTTPRequest.request_completed
        assert(typeof(signal_args) == TYPE_ARRAY)

Nếu không, value được await sẽ là ``null``:

::

    func button_up():
        var signal_args = await $Button.button_up
        assert(signal_args == null)

Keyword assert
--------------

Keyword ``assert`` có thể được dùng để kiểm tra các điều kiện trong debug build. Các assertion này sẽ bị bỏ qua trong non-debug build. Điều này có nghĩa là expression được truyền làm argument sẽ không được evaluate trong project được export ở release mode. Vì vậy, assertion **không được** chứa các expression có side effect. Nếu không, hành vi của script sẽ thay đổi tùy theo việc project có được chạy trong debug build hay không.

::

    # Kiểm tra 'i' bằng 0. Nếu 'i' không bằng 0, sẽ xảy ra lỗi assertion.
    assert(i == 0)

Khi chạy một project từ editor, project sẽ bị tạm dừng nếu xảy ra lỗi assertion.

Bạn có thể tùy chọn truyền một error message tùy chỉnh để hiển thị nếu assertion thất bại:

::

    assert(enemy_power < 256, "Enemy is too powerful!")
