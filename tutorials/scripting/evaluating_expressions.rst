.. _doc_evaluating_expressions:

Đánh giá biểu thức
==================

Godot cung cấp một lớp :ref:`class_Expression` mà bạn có thể dùng để đánh giá biểu thức.

Một biểu thức có thể là:

- Một biểu thức toán học chẳng hạn như ``(2 + 4) * 16/4.0``. - Một biểu thức boolean chẳng hạn như ``true && false``. - Một lời gọi phương thức tích hợp như ``deg_to_rad(90)``. - Một lời gọi phương thức trên script do người dùng cung cấp như ``update_health()``, nếu ``base_instance`` được đặt thành giá trị khác ``null`` khi gọi
  :ref:`Expression.execute() <class_Expression_method_execute>`.

.. note::

    Lớp Expression độc lập với GDScript. Lớp này vẫn khả dụng ngay cả khi bạn biên dịch Godot với module GDScript bị tắt.

Cách sử dụng cơ bản
-------------------

Để đánh giá một biểu thức toán học, hãy dùng:

::

    var expression = Expression.new()
    expression.parse("20 + 10*2 - 5/2.0")
    var result = expression.execute()
    print(result)  # 37.5

Các toán tử sau khả dụng:

+------------------------+-------------------------------------------------------------------------------------+
| Operator               | Notes                                                                               |
+========================+=====================================================================================+
| Addition (``+``)       | Can also be used to concatenate strings and arrays:                                 |
|                        | - ``"hello" + " world"`` = ``hello world``                                          |
|                        | - ``[1, 2] + [3, 4]`` = ``[1, 2, 3, 4]``                                            |
+------------------------+-------------------------------------------------------------------------------------+
| Subtraction (``-``)    |                                                                                     |
+------------------------+-------------------------------------------------------------------------------------+
| Multiplication (``*``) |                                                                                     |
+------------------------+-------------------------------------------------------------------------------------+
| Division (``/``)       | Performs and integer division if both operands are integers.                        |
|                        | If at least one of them is a floating-point number, returns a floating-point value. |
+------------------------+-------------------------------------------------------------------------------------+
| Remainder (``%``)      | Returns the remainder of an integer division (modulo).                              |
|                        | The result will always have the sign of the dividend.                               |
+------------------------+-------------------------------------------------------------------------------------+
| Conjunction (``&&``)   | Returns the result of a boolean AND.                                                |
+------------------------+-------------------------------------------------------------------------------------+
| Disjunction (``||``)   | Returns the result of a boolean OR.                                                 |
+------------------------+-------------------------------------------------------------------------------------+
| Negation (``!``)       | Returns the result of a boolean NOT.                                                |
+------------------------+-------------------------------------------------------------------------------------+

Khoảng trắng xung quanh toán tử là tùy chọn. Ngoài ra, hãy nhớ rằng `order of operations <https://en.wikipedia.org/wiki/Order_of_operations>`__ thông thường được áp dụng. Dùng dấu ngoặc đơn để ghi đè thứ tự thực hiện nếu cần.

Có thể sử dụng tất cả các kiểu Variant được Godot hỗ trợ: số nguyên, số dấu phẩy động, chuỗi, mảng, dictionary, màu sắc, vector, …

Có thể lập chỉ mục cho mảng và dictionary như trong GDScript:

::

    # Trả về 1.
    [1, 2][0]

    # Trả về 3. Có thể dùng chỉ số âm để đếm từ cuối mảng.
    [1, 3][-1]

    # Trả về "green".
    {"favorite_color": "green"}["favorite_color"]

    # Cả 3 dòng dưới đây đều trả về 7.0 (Vector3 là kiểu dấu phẩy động).
    Vector3(5, 6, 7)[2]
    Vector3(5, 6, 7)["z"]
    Vector3(5, 6, 7).z

Truyền biến vào biểu thức
-------------------------

Bạn có thể truyền biến vào một biểu thức. Khi đó, các biến này sẽ khả dụng trong "context" của biểu thức và được thay thế khi được sử dụng trong biểu thức:

::

    var expression = Expression.new()
    # Trước tiên, hãy định nghĩa tên biến trong tham số thứ hai của `parse()`.
    # Trong ví dụ này, chúng ta dùng `x` làm tên biến.
    expression.parse("20 + 2 * x", ["x"])
    # Sau đó, hãy định nghĩa các giá trị biến trong tham số thứ nhất của `execute()`.
    # Ở đây, `x` được gán giá trị số nguyên 5.
    var result = expression.execute([5])
    print(result)  # 30

Cả tên biến và giá trị biến **phải** được chỉ định dưới dạng một mảng, ngay cả khi bạn chỉ định nghĩa một biến. Ngoài ra, tên biến **phân biệt chữ hoa chữ thường**.

Đặt instance cơ sở cho biểu thức
--------------------------------

Theo mặc định, một biểu thức có instance cơ sở là ``null``. Điều này có nghĩa là biểu thức không liên kết với instance cơ sở nào.

Khi gọi :ref:`Expression.execute() <class_Expression_method_execute>`, bạn có thể đặt giá trị của tham số ``base_instance`` thành một object instance cụ thể như ``self``, một script instance khác hoặc thậm chí một singleton:

::

    func double(number):
        return number * 2


    func _ready():
        var expression = Expression.new()
        expression.parse("double(10)")

        # Cách này sẽ không hoạt động vì chúng ta không truyền script hiện tại làm instance cơ sở.
        var result = expression.execute([], null)
        print(result)  # null

        # Cách này sẽ hoạt động vì chúng ta truyền script hiện tại (tức là self)
        # làm instance cơ sở.
        result = expression.execute([], self)
        print(result)  # 20

Việc liên kết một instance cơ sở cho phép thực hiện những việc sau:

- Tham chiếu các hằng số của instance (``const``) trong biểu thức. - Tham chiếu các biến thành viên của instance (``var``) trong biểu thức. - Gọi các phương thức được định nghĩa trong instance và sử dụng giá trị trả về của chúng trong biểu thức.

.. warning::

    Đặt instance cơ sở thành một giá trị khác ``null`` cho phép tham chiếu các hằng số, biến thành viên và gọi tất cả phương thức được định nghĩa trong script gắn với instance. Cho phép người dùng nhập biểu thức có thể tạo điều kiện gian lận trong game của bạn, hoặc thậm chí tạo ra lỗ hổng bảo mật nếu bạn cho phép các client tùy ý chạy biểu thức trên thiết bị của người chơi khác.

Script ví dụ
------------

Script dưới đây minh họa những khả năng của lớp Expression:

::

    const DAYS_IN_YEAR = 365
    var script_member_variable = 1000


    func _ready():
        # Biểu thức boolean hằng.
        evaluate("true && false")
        # Biểu thức boolean có biến.
        evaluate("!(a && b)", ["a", "b"], [true, false])

        # Biểu thức toán học hằng.
        evaluate("2 + 2")
        # Biểu thức toán học có biến.
        evaluate("x + y", ["x", "y"], [60, 100])

        # Gọi phương thức tích hợp (lời gọi hàm toán học tích hợp).
        evaluate("deg_to_rad(90)")

        # Gọi phương thức do người dùng định nghĩa (được định nghĩa trong script).
        # Chúng ta có thể làm điều này vì quá trình thực thi biểu thức được liên kết với `self`
        # trong phương thức `evaluate()`.
        # Vì phương thức do người dùng định nghĩa này trả về một giá trị, chúng ta có thể sử dụng nó trong các biểu thức toán học.
        evaluate("call_me() + DAYS_IN_YEAR + script_member_variable")
        evaluate("call_me(42)")
        evaluate("call_me('some string')")


    func evaluate(command, variable_names = [], variable_values = []) -> void:
        var expression = Expression.new()
        var error = expression.parse(command, variable_names)
        if error != OK:
            push_error(expression.get_error_text())
            return

        var result = expression.execute(variable_values, self)

        if not expression.has_execute_failed():
            print(str(result))


    func call_me(argument = null):
        print("\nYou called 'call_me()' in the expression text.")
        if argument:
            print("Argument passed: %s" % argument)

        # Giá trị trả về của phương thức cũng là giá trị trả về của biểu thức.
        return 0

Đầu ra từ script sẽ là:

::

    false
    true
    4
    160
    1.5707963267949

    You called 'call_me()' in the expression text.
    1365

    You called 'call_me()' in the expression text.
    Argument passed: 42
    0

    You called 'call_me()' in the expression text.
    Argument passed: some string
    0

Các hàm tích hợp
----------------

Tất cả các phương thức trong :ref:`Global Scope<class_@GlobalScope>` đều khả dụng trong lớp Expression, ngay cả khi không có instance cơ sở nào được liên kết với biểu thức. Các tham số và kiểu trả về giống nhau cũng khả dụng.

Tuy nhiên, không giống GDScript, các tham số **luôn bắt buộc** ngay cả khi chúng được chỉ định là tùy chọn trong tài liệu tham chiếu lớp. Ngược lại, hạn chế này đối với các đối số không áp dụng cho các hàm do người dùng tạo khi bạn liên kết một instance cơ sở với biểu thức.
