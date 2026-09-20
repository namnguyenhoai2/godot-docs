.. _doc_gdscript_printf:

Chuỗi định dạng GDScript
========================

Godot cung cấp nhiều cách để thay đổi nội dung của các chuỗi một cách linh động:

- Chuỗi định dạng: ``var string = "I have %s cats." % "3"`` - Phương thức ``String.format()``: ``var string = "I have {0} cats.".format([3])`` - Nối chuỗi: ``var string = "I have " + str(3) + " cats."``

Trang này giải thích cách sử dụng chuỗi định dạng, đồng thời giải thích ngắn gọn về phương thức ``format()`` và phép nối chuỗi.

Chuỗi định dạng
---------------

*Chuỗi định dạng* là một cách tái sử dụng các mẫu văn bản để ngắn gọn tạo ra những chuỗi khác nhau nhưng tương tự nhau.

Chuỗi định dạng cũng giống như chuỗi thông thường, ngoại trừ việc chúng chứa một số chuỗi ký tự giữ chỗ nhất định, chẳng hạn như ``%s``. Sau đó, các giữ chỗ này có thể được thay thế bằng các tham số được truyền cho chuỗi định dạng.

Hãy xem xét ví dụ GDScript cụ thể sau:

::

    # Định nghĩa một chuỗi định dạng với giữ chỗ '%s'
    var format_string = "We're waiting for %s."

    # Sử dụng toán tử '%', giữ chỗ được thay thế bằng giá trị mong muốn
    var actual_string = format_string % "Godot"

    print(actual_string)
    # Kết quả: "We're waiting for Godot."

Các giữ chỗ luôn bắt đầu bằng ``%``, nhưng ký tự hoặc các ký tự tiếp theo, gọi là *định dạng chỉ định* (format specifier), sẽ quyết định cách giá trị được chuyển đổi thành chuỗi.

``%s`` xuất hiện trong ví dụ trên là giữ chỗ đơn giản nhất và hoạt động trong hầu hết trường hợp sử dụng: nó chuyển đổi giá trị bằng cùng phương thức mà một phép chuyển đổi String ngầm định hoặc :ref:`str() <class_@GlobalScope_method_str>` sẽ sử dụng. Các chuỗi được giữ nguyên, boolean được chuyển thành ``"true"`` hoặc ``"false"``, các kiểu ``int`` và ``float`` trở thành số thập phân, còn các kiểu khác thường trả về dữ liệu của chúng dưới dạng chuỗi mà con người có thể đọc được.

Có các `Định dạng chỉ định`_ khác.

Nhiều giữ chỗ
-------------

Chuỗi định dạng có thể chứa nhiều giữ chỗ. Trong trường hợp đó, các giá trị được truyền dưới dạng một mảng, mỗi giữ chỗ tương ứng với một giá trị (trừ khi sử dụng định dạng chỉ định với ``*``, xem `Đệm động`_):

::

    var format_string = "%s was reluctant to learn %s, but now he enjoys it."
    var actual_string = format_string % ["Estragon", "GDScript"]

    print(actual_string)
    # Kết quả: "Estragon was reluctant to learn GDScript, but now he enjoys it."

Lưu ý rằng các giá trị được chèn theo thứ tự. Hãy nhớ rằng tất cả giữ chỗ phải được thay thế cùng lúc, vì vậy phải có số lượng giá trị phù hợp.


Định dạng chỉ định
------------------

Ngoài ``s``, còn có các định dạng chỉ định khác có thể được sử dụng trong các giữ chỗ. Chúng bao gồm một hoặc nhiều ký tự. Một số hoạt động độc lập như ``s``, một số xuất hiện trước các ký tự khác, còn một số chỉ hoạt động với những giá trị hoặc ký tự nhất định.


Các kiểu giữ chỗ
~~~~~~~~~~~~~~~~

Một và chỉ một trong các ký tự này luôn phải xuất hiện ở vị trí cuối cùng trong định dạng chỉ định. Ngoài ``s``, các ký tự này yêu cầu những kiểu tham số nhất định.

+-------+---------------------------------------------------------------------+
| ``s`` | **Simple** conversion to String by the same method as implicit      |
|       | String conversion.                                                  |
+-------+---------------------------------------------------------------------+
| ``c`` | A single **Unicode character**. Accepts a Unicode code point        |
|       | (integer) or a single-character string. Supports values beyond 255. |
+-------+---------------------------------------------------------------------+
| ``d`` | A **decimal integer**. Expects an integer or a real number          |
|       | (will be floored).                                                  |
+-------+---------------------------------------------------------------------+
| ``o`` | An **octal integer**. Expects an integer or a real number           |
|       | (will be floored).                                                  |
+-------+---------------------------------------------------------------------+
| ``x`` | A **hexadecimal integer** with **lower-case** letters.              |
|       | Expects an integer or a real number (will be floored).              |
+-------+---------------------------------------------------------------------+
| ``X`` | A **hexadecimal integer** with **upper-case** letters.              |
|       | Expects an integer or a real number (will be floored).              |
+-------+---------------------------------------------------------------------+
| ``f`` | A **decimal real** number. Expects an integer or a real number.     |
+-------+---------------------------------------------------------------------+
| ``v`` | A **vector**. Expects any float or int-based vector object (        |
|       | ``Vector2``, ``Vector3``, ``Vector4``, ``Vector2i``, ``Vector3i`` or|
|       | ``Vector4i``). Will display the vector coordinates in parentheses,  |
|       | formatting each coordinate as if it was an ``%f``, and using the    |
|       | same modifiers.                                                     |
+-------+---------------------------------------------------------------------+


Bộ bổ nghĩa giữ chỗ
~~~~~~~~~~~~~~~~~~~

Các ký tự này xuất hiện trước những ký tự nêu trên. Một số chỉ hoạt động trong những điều kiện nhất định.

+---------+-------------------------------------------------------------------+
| ``+``   | In number specifiers, **show + sign** if positive.                |
+---------+-------------------------------------------------------------------+
| Integer | Set **padding**. Padded with spaces or with zeroes if integer     |
|         | starts with ``0`` in an integer or real number placeholder.       |
|         | The leading ``0`` is ignored if ``-`` is present.                 |
|         | When used after ``.``, see ``.``.                                 |
+---------+-------------------------------------------------------------------+
| ``.``   | Before ``f`` or ``v``, set **precision** to 0 decimal places. Can |
|         | be followed up with numbers to change. Padded with zeroes.        |
+---------+-------------------------------------------------------------------+
| ``-``   | **Pad to the right** rather than the left.                        |
+---------+-------------------------------------------------------------------+
| ``*``   | **Dynamic padding**, expects additional integer parameter to set  |
|         | padding or precision after ``.``, see `dynamic padding`_.         |
+---------+-------------------------------------------------------------------+


Đệm
---

The ``.`` (*dot*), ``*`` (*asterisk*), ``-`` (*minus sign*) and digit (``0``-``9``) characters are used for padding. This allows printing several values aligned vertically as if in a column, provided a fixed-width font is used.

Để đệm một chuỗi đến độ dài tối thiểu, hãy thêm một số nguyên vào định dạng chỉ định:

::

    print("%10d" % 12345)
    # kết quả: "     12345"
    # 5 khoảng trắng ở đầu, tổng độ dài là 10

Nếu số nguyên bắt đầu bằng ``0``, các giá trị số nguyên sẽ được đệm bằng số 0 thay vì khoảng trắng:

::

    print("%010d" % 12345)
    # kết quả: "0000012345"

Có thể chỉ định độ chính xác cho các số thực bằng cách thêm ``.`` (*dấu chấm*) rồi theo sau là một số nguyên. Nếu không có số nguyên sau ``.``, độ chính xác được đặt là 0 và giá trị được làm tròn thành số nguyên. Số nguyên dùng để đệm phải xuất hiện trước dấu chấm.

::

    # Đệm đến độ dài tối thiểu là 10, làm tròn đến 3 chữ số thập phân
    print("%10.3f" % 10000.5555)
    # Kết quả: " 10000.556"
    # 1 khoảng trắng ở đầu

Ký tự ``-`` sẽ khiến phần đệm được thêm vào bên phải thay vì bên trái, hữu ích khi căn chỉnh văn bản sang phải:

::

    print("%-10d" % 12345678)
    # Kết quả: "12345678  "
    # 2 khoảng trắng ở cuối


Đệm động
~~~~~~~~

Bằng cách sử dụng ký tự ``*`` (*dấu hoa thị*), có thể đặt phần đệm hoặc độ chính xác mà không cần sửa đổi chuỗi định dạng. Ký tự này được dùng thay cho một số nguyên trong định dạng chỉ định. Sau đó, các giá trị dùng cho phần đệm và độ chính xác được truyền vào khi định dạng:

::

    var format_string = "%*.*f"
    # Đệm đến độ dài 7, làm tròn đến 3 chữ số thập phân:
    print(format_string % [7, 3, 8.8888])
    # Kết quả: "  8.889"
    # 2 khoảng trắng ở đầu

Vẫn có thể đệm bằng số 0 trong các giữ chỗ số nguyên bằng cách thêm ``0`` trước ``*``:

::

    print("%0*d" % [2, 3])
    # Kết quả: "03"


Chuỗi thoát
-----------

Để chèn một ký tự ``%`` theo nghĩa đen vào chuỗi định dạng, ký tự đó phải được escape để tránh bị đọc như một giữ chỗ. Việc này được thực hiện bằng cách nhân đôi ký tự:

::

    var health = 56
    print("Remaining health: %d%%" % health)
    # Kết quả: "Remaining health: 56%"


Phương thức định dạng chuỗi
---------------------------

Ngoài ra còn có một cách khác để định dạng văn bản trong GDScript, đó là phương thức
:ref:`String.format() <class_String_method_format>`
Phương thức này thay thế tất cả các lần xuất hiện của một khóa trong chuỗi bằng giá trị tương ứng. Phương thức có thể xử lý các mảng hoặc dictionary cho các cặp khóa/giá trị.

Mảng có thể được sử dụng theo kiểu khóa, chỉ mục hoặc kết hợp (xem các ví dụ bên dưới). Thứ tự chỉ quan trọng khi sử dụng kiểu chỉ mục hoặc kiểu kết hợp của Array.

Một ví dụ nhanh trong GDScript:

::

    # Định nghĩa một chuỗi định dạng
    var format_string = "We're waiting for {str}"

    # Sử dụng phương thức 'format', thay thế giữ chỗ 'str'
    var actual_string = format_string.format({"str": "Godot"})

    print(actual_string)
    # Kết quả: "We're waiting for Godot"


Các ví dụ về phương thức format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau đây là một số ví dụ về cách sử dụng các cách gọi khác nhau của phương thức ``String.format()``.

+------------+-----------+------------------------------------------------------------------------------+-------------------+
| **Type**   | **Style** | **Example**                                                                  | **Result**        |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Dictionary | key       | ``"Hi, {name} v{version}!".format({"name":"Godette", "version":"3.0"})``     | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Dictionary | index     | ``"Hi, {0} v{1}!".format({"0":"Godette", "1":"3.0"})``                       | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Dictionary | mix       | ``"Hi, {0} v{version}!".format({"0":"Godette", "version":"3.0"})``           | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Array      | key       | ``"Hi, {name} v{version}!".format([["version","3.0"], ["name","Godette"]])`` | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Array      | index     | ``"Hi, {0} v{1}!".format(["Godette","3.0"])``                                | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Array      | mix       | ``"Hi, {name} v{0}!".format(["3.0", ["name","Godette"]])``                   | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+
| Array      | no index  | ``"Hi, {} v{}!".format(["Godette", "3.0"], "{}")``                           | Hi, Godette v3.0! |
+------------+-----------+------------------------------------------------------------------------------+-------------------+

Các giữ chỗ cũng có thể được tùy chỉnh khi sử dụng ``String.format``; dưới đây là một số ví dụ về chức năng đó.


+-----------------+------------------------------------------------------+------------------+
| **Type**        | **Example**                                          | **Result**       |
+-----------------+------------------------------------------------------+------------------+
| Infix (default) | ``"Hi, {0} v{1}".format(["Godette", "3.0"], "{_}")`` | Hi, Godette v3.0 |
+-----------------+------------------------------------------------------+------------------+
| Postfix         | ``"Hi, 0% v1%".format(["Godette", "3.0"], "_%")``    | Hi, Godette v3.0 |
+-----------------+------------------------------------------------------+------------------+
| Prefix          | ``"Hi, %0 v%1".format(["Godette", "3.0"], "%_")``    | Hi, Godette v3.0 |
+-----------------+------------------------------------------------------+------------------+

Việc kết hợp cả phương thức ``String.format`` và toán tử ``%`` có thể hữu ích, vì ``String.format`` không có cách thao tác với cách biểu diễn số.

+---------------------------------------------------------------------------+-------------------+
| **Example**                                                               | **Result**        |
+---------------------------------------------------------------------------+-------------------+
| ``"Hi, {0} v{version}".format({0:"Godette", "version":"%0.2f" % 3.114})`` | Hi, Godette v3.11 |
+---------------------------------------------------------------------------+-------------------+

Nối chuỗi
---------

Bạn cũng có thể kết hợp các chuỗi bằng cách *nối* chúng lại với nhau, sử dụng toán tử ``+``.

::

    # Định nghĩa chuỗi cơ sở
    var base_string = "We're waiting for "

    # Nối chuỗi
    var actual_string = base_string + "Godot"

    print(actual_string)
    # Kết quả: "We're waiting for Godot"

Khi sử dụng phép nối chuỗi, các giá trị không phải chuỗi phải được chuyển đổi bằng hàm ``str()``. Không có cách nào chỉ định định dạng chuỗi của các giá trị đã chuyển đổi.

::

    var name_string = "Godette"
    var version = 3.0
    var actual_string = "Hi, " + name_string + " v" + str(version) + "!"

    print(actual_string)
    # Kết quả: "Hi, Godette v3!"

Do những hạn chế này, chuỗi định dạng hoặc phương thức ``format()`` thường là lựa chọn tốt hơn. Trong nhiều trường hợp, phép nối chuỗi cũng khó đọc hơn.

.. note::

    Trong mã C++ của Godot, có thể truy cập các chuỗi định dạng GDScript bằng hàm trợ giúp ``vformat()`` trong header :ref:`Variant<class_Variant>`.
