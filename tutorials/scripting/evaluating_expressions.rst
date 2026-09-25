.. _doc_evaluating_expressions:

Đánh giá biểu thức
==================

Godot cung cấp một lớp :ref:`class_Expression` mà bạn có thể dùng để đánh giá các biểu thức.

Một biểu thức có thể là:

- Một biểu thức toán học, chẳng hạn như ``(2 + 4) * 16/4.0``.
- Một biểu thức boolean, chẳng hạn như ``true && false``.
- Một lệnh gọi phương thức tích hợp như ``deg_to_rad(90)``.
- Một lệnh gọi phương thức trên script do người dùng cung cấp như ``update_health()``, nếu ``base_instance`` được đặt thành một giá trị khác ``null`` khi gọi
  :ref:`Expression.execute() <class_Expression_method_execute>`.

.. note::

    Lớp Expression độc lập với GDScript. Lớp này vẫn khả dụng ngay cả khi bạn biên dịch Godot với module GDScript bị tắt.

Cách sử dụng cơ bản
-------------------

Để đánh giá một biểu thức toán học, hãy sử dụng:

.. code-block::

    var expression = Expression.new()
    expression.parse("20 + 10*2 - 5/2.0")
    var result = expression.execute()
    print(result)  # 37.5

Các toán tử sau khả dụng:

+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Toán tử               | Ghi chú                                                                                                                                            |
+=======================+====================================================================================================================================================+
| Phép cộng (``+``)     | Cũng có thể được dùng để nối các chuỗi và mảng:                                                                                                    |
|                       | - ``"hello" + " world"`` = ``hello world``                                                                                                         |
|                       | - ``[1, 2] + [3, 4]`` = ``[1, 2, 3, 4]``                                                                                                           |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép trừ (``-``)      |                                                                                                                                                    |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép nhân (``*``)     |                                                                                                                                                    |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép chia (``/``)     | Thực hiện phép chia nguyên nếu cả hai toán hạng đều là số nguyên. Nếu ít nhất một toán hạng là số dấu phẩy động, trả về một giá trị dấu phẩy động. |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phần dư (``%``)       | Trả về phần dư của phép chia nguyên (modulo). Kết quả luôn có cùng dấu với số bị chia.                                                             |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép hội (``&&``)     | Trả về kết quả của phép AND boolean.                                                                                                               |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép tuyển (``||``)   | Trả về kết quả của phép OR boolean.                                                                                                                |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Phép phủ định (``!``) | Trả về kết quả của phép NOT boolean.                                                                                                               |
+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

Khoảng trắng xung quanh các toán tử là không bắt buộc. Ngoài ra, hãy lưu ý rằng `thứ tự thực hiện <https://en.wikipedia.org/wiki/Order_of_operations>`__ thông thường vẫn được áp dụng. Sử dụng dấu ngoặc đơn để ghi đè thứ tự thực hiện nếu cần.

Có thể sử dụng tất cả các kiểu Variant được Godot hỗ trợ: số nguyên, số dấu phẩy động, chuỗi, mảng, từ điển, màu, vector, …

Có thể lập chỉ mục mảng và từ điển như trong GDScript:

.. code-block::

    # Trả về 1.
    [1, 2][0]

    # Trả về 3. Có thể dùng chỉ mục âm để đếm từ cuối mảng.
    [1, 3][-1]

    # Trả về "green".
    {"favorite_color": "green"}["favorite_color"]

    # Cả 3 dòng bên dưới đều trả về 7.0 (Vector3 là kiểu dấu phẩy động).
    Vector3(5, 6, 7)[2]
    Vector3(5, 6, 7)["z"]
    Vector3(5, 6, 7).z

Truyền biến vào biểu thức
-------------------------

Bạn có thể truyền các biến vào một biểu thức. Sau đó, các biến này sẽ khả dụng trong "context" của biểu thức và sẽ được thay thế khi được sử dụng trong biểu thức:

.. code-block::

    var expression = Expression.new()
    # Define the variable names first in the second parameter of `parse()`.
    # Trong ví dụ này, chúng ta sử dụng `x` làm tên biến.
    expression.parse("20 + 2 * x", ["x"])
    # Sau đó, xác định các giá trị biến trong tham số đầu tiên của `execute()`.
    # Ở đây, `x` được gán giá trị số nguyên 5.
    var result = expression.execute([5])
    print(result)  # 30

Cả tên biến và giá trị biến **bắt buộc** phải được chỉ định dưới dạng một mảng, ngay cả khi bạn chỉ định nghĩa một biến. Ngoài ra, tên biến **phân biệt chữ hoa chữ thường**.

Đặt instance cơ sở cho biểu thức
--------------------------------

Theo mặc định, một biểu thức có instance cơ sở là ``null``. Điều này có nghĩa là biểu thức không liên kết với instance cơ sở nào.

Khi gọi :ref:`Expression.execute() <class_Expression_method_execute>`, bạn có thể đặt giá trị của tham số ``base_instance`` thành một instance đối tượng cụ thể như ``self``, một instance script khác hoặc thậm chí là một singleton:

.. code-block::

    func double(number):
        return number * 2


    func _ready():
        var expression = Expression.new()
        expression.parse("double(10)")

        # Điều này sẽ không hoạt động vì chúng ta không truyền script hiện tại làm instance cơ sở.
        var result = expression.execute([], null)
        print(result)  # null

        # Điều này sẽ hoạt động vì chúng ta truyền script hiện tại (tức là self)
        # làm instance cơ sở.
        result = expression.execute([], self)
        print(result)  # 20

Việc liên kết một instance cơ sở cho phép thực hiện những việc sau:

- Tham chiếu các hằng số của instance (``const``) trong biểu thức.
- Tham chiếu các biến thành viên của instance (``var``) trong biểu thức.
- Gọi các phương thức được định nghĩa trong instance và sử dụng giá trị trả về của chúng trong biểu thức.

.. warning::

    Đặt instance cơ sở thành một giá trị khác ``null`` cho phép tham chiếu các hằng số, biến thành viên và gọi mọi phương thức được định nghĩa trong script gắn với instance. Cho phép người dùng nhập biểu thức có thể tạo điều kiện gian lận trong trò chơi của bạn, hoặc thậm chí tạo ra các lỗ hổng bảo mật nếu bạn cho phép các client tùy ý chạy biểu thức trên thiết bị của người chơi khác.

Script ví dụ
------------

Script dưới đây minh họa những gì lớp Expression có thể thực hiện:

.. code-block::

    const DAYS_IN_YEAR = 365
    var script_member_variable = 1000


    func _ready():
        # Biểu thức boolean hằng.
        evaluate("true && false")
        # Biểu thức boolean với các biến.
        evaluate("!(a && b)", ["a", "b"], [true, false])

        # Biểu thức toán học hằng.
        evaluate("2 + 2")
        # Biểu thức toán học với các biến.
        evaluate("x + y", ["x", "y"], [60, 100])

        # Gọi phương thức tích hợp (lời gọi hàm toán học tích hợp).
        evaluate("deg_to_rad(90)")

        # Gọi phương thức do người dùng định nghĩa (được định nghĩa trong script).
        # Chúng ta có thể làm vậy vì việc thực thi biểu thức được liên kết với `self`
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

Tất cả các phương thức trong :ref:`Global Scope <class_@GlobalScope>` đều khả dụng trong lớp Expression, ngay cả khi không có instance cơ sở nào được liên kết với biểu thức. Các tham số và kiểu trả về tương ứng cũng khả dụng.

Tuy nhiên, không giống như GDScript, các tham số **always required** ngay cả khi chúng được chỉ định là tùy chọn trong tài liệu tham chiếu lớp. Ngược lại, hạn chế này đối với các đối số không áp dụng cho các hàm do người dùng tạo khi bạn liên kết một instance cơ sở với biểu thức.
