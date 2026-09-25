.. _doc_gdscript_printf:

Chuỗi định dạng GDScript
========================

Godot cung cấp nhiều cách để thay đổi nội dung của chuỗi một cách linh động:

- Chuỗi định dạng: ``var string = "I have %s cats." % "3"``
- Phương thức ``String.format()``: ``var string = "I have {0} cats.".format([3])``
- Nối chuỗi: ``var string = "I have " + str(3) + " cats."``

Trang này giải thích cách sử dụng chuỗi định dạng, đồng thời giải thích ngắn gọn về phương thức ``format()`` và phép nối chuỗi.

Chuỗi định dạng
---------------

*Chuỗi định dạng* là cách tái sử dụng các mẫu văn bản để ngắn gọn tạo ra những chuỗi khác nhau nhưng tương tự nhau.

Chuỗi định dạng giống như chuỗi thông thường, ngoại trừ việc chúng chứa một số chuỗi ký tự giữ chỗ nhất định như ``%s``. Sau đó, các phần giữ chỗ này có thể được thay thế bằng các tham số được truyền cho chuỗi định dạng.

Hãy xem ví dụ GDScript cụ thể sau:

::

    # Define a format string with placeholder '%s'
    var format_string = "We're waiting for %s."

    # Using the '%' operator, the placeholder is replaced with the desired value
    var actual_string = format_string % "Godot"

    print(actual_string)
    # Output: "We're waiting for Godot."

Các phần giữ chỗ luôn bắt đầu bằng ``%``, nhưng ký tự hoặc các ký tự tiếp theo, *bộ định dạng*, sẽ quyết định cách chuyển đổi giá trị được cung cấp thành chuỗi.

``%s`` xuất hiện trong ví dụ trên là phần giữ chỗ đơn giản nhất và hoạt động trong hầu hết trường hợp sử dụng: nó chuyển đổi giá trị bằng cùng phương thức mà một phép chuyển đổi String ngầm định hoặc :ref:`str() <class_@GlobalScope_method_str>` sẽ sử dụng. Các chuỗi không thay đổi, boolean được chuyển thành ``"true"`` hoặc ``"false"``, các kiểu ``int`` và ``float`` trở thành số thập phân, còn các kiểu khác thường trả về dữ liệu dưới dạng chuỗi dễ đọc.

Có các `bộ định dạng <format specifiers_>`_ khác.

Nhiều phần giữ chỗ
------------------

Chuỗi định dạng có thể chứa nhiều phần giữ chỗ. Trong trường hợp đó, các giá trị được truyền dưới dạng một mảng, mỗi phần giữ chỗ tương ứng với một giá trị (trừ khi sử dụng bộ định dạng với ``*``, xem `đệm động <dynamic padding_>`_):

::

    var format_string = "%s was reluctant to learn %s, but now he enjoys it."
    var actual_string = format_string % ["Estragon", "GDScript"]

    print(actual_string)
    # Output: "Estragon was reluctant to learn GDScript, but now he enjoys it."

Lưu ý rằng các giá trị được chèn theo thứ tự. Hãy nhớ rằng mọi phần giữ chỗ phải được thay thế cùng lúc, vì vậy phải có số lượng giá trị phù hợp.


.. _`Format specifiers`:

Bộ định dạng
------------

Ngoài ``s``, còn có các bộ định dạng khác có thể được sử dụng trong phần giữ chỗ. Chúng bao gồm một hoặc nhiều ký tự. Một số hoạt động độc lập như ``s``, một số xuất hiện trước các ký tự khác, còn một số chỉ hoạt động với những giá trị hoặc ký tự nhất định.


Các kiểu phần giữ chỗ
~~~~~~~~~~~~~~~~~~~~~

Một và chỉ một trong các ký tự này luôn phải xuất hiện ở vị trí cuối cùng trong bộ định dạng. Ngoài ``s``, các ký tự này yêu cầu những kiểu tham số nhất định.

+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``s`` | **Đơn giản** chuyển đổi thành String bằng cùng phương thức như phép chuyển đổi String ngầm định.                                                                                                                                                                                     |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``c`` | Một **ký tự Unicode** đơn. Chấp nhận một mã điểm Unicode (số nguyên) hoặc một chuỗi gồm một ký tự. Hỗ trợ các giá trị lớn hơn 255.                                                                                                                                                   |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``d`` | Một **số nguyên thập phân**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                                                            |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``o`` | Một **số nguyên bát phân**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                                                             |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``x`` | Một **số nguyên thập lục phân** với các chữ cái **chữ thường**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                         |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``X`` | Một **số nguyên thập lục phân** với các chữ cái **chữ hoa**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                            |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``f`` | Một **số thực thập phân**. Yêu cầu một số nguyên hoặc số thực.                                                                                                                                                                                                                       |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``v`` | Một **vector**. Yêu cầu bất kỳ đối tượng vector dựa trên float hoặc int nào ( ``Vector2``, ``Vector3``, ``Vector4``, ``Vector2i``, ``Vector3i`` hoặc ``Vector4i``). Hiển thị các tọa độ vector trong dấu ngoặc đơn, định dạng từng tọa độ như một ``%f``, và sử dụng cùng các bổ từ. |
+-------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Bổ từ phần giữ chỗ
~~~~~~~~~~~~~~~~~~

Các ký tự này xuất hiện trước những ký tự ở trên. Một số chỉ hoạt động trong những điều kiện nhất định.

+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``+``     | Trong các bộ định dạng số, **hiển thị dấu +** nếu là số dương.                                                                                                                                                         |
+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Số nguyên | Đặt **độ đệm**. Đệm bằng dấu cách hoặc bằng số 0 nếu số nguyên bắt đầu bằng ``0`` trong phần giữ chỗ cho số nguyên hoặc số thực. Dấu ``0`` ở đầu sẽ bị bỏ qua nếu có ``-``. Khi được sử dụng sau ``.``, hãy xem ``.``. |
+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``.``     | Trước ``f`` hoặc ``v``, đặt **độ chính xác** thành 0 chữ số thập phân. Có thể theo sau bằng các chữ số để thay đổi giá trị. Đệm bằng số 0.                                                                             |
+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-``     | **Đệm sang phải** thay vì sang trái.                                                                                                                                                                                   |
+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``*``     | **Đệm động**, yêu cầu thêm một tham số số nguyên để đặt độ đệm hoặc độ chính xác sau ``.``, xem `đệm động <dynamic padding_>`_.                                                                                        |
+-----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Đệm
---

Các ký tự ``.`` (*dấu chấm*), ``*`` (*dấu hoa thị*), ``-`` (*dấu trừ*) và chữ số (``0``-``9``) được dùng để đệm. Điều này cho phép in nhiều giá trị được căn chỉnh theo chiều dọc như trong một cột, với điều kiện sử dụng phông chữ có chiều rộng cố định.

Để đệm một chuỗi đến độ dài tối thiểu, hãy thêm một số nguyên vào bộ định dạng:

::

    print("%10d" % 12345)
    # output: "     12345"
    # 5 leading spaces for a total length of 10

Nếu số nguyên bắt đầu bằng ``0``, các giá trị số nguyên sẽ được đệm bằng số 0 thay vì khoảng trắng:

::

    print("%010d" % 12345)
    # output: "0000012345"

Có thể chỉ định độ chính xác cho các số thực bằng cách thêm ``.`` (*dot*) rồi theo sau là một số nguyên. Nếu không có số nguyên sau ``.``, độ chính xác bằng 0 sẽ được sử dụng, làm tròn thành các giá trị nguyên. Số nguyên dùng để đệm phải xuất hiện trước dấu chấm.

::

    # Pad to minimum length of 10, round to 3 decimal places
    print("%10.3f" % 10000.5555)
    # Output: " 10000.556"
    # 1 leading space

Ký tự ``-`` sẽ khiến phần đệm nằm bên phải thay vì bên trái, hữu ích khi căn chỉnh văn bản sang phải:

::

    print("%-10d" % 12345678)
    # Output: "12345678  "
    # 2 trailing spaces


.. _`Dynamic padding`:

Đệm động
~~~~~~~~

Bằng cách sử dụng ký tự ``*`` (*asterisk*), có thể đặt phần đệm hoặc độ chính xác mà không cần sửa chuỗi định dạng. Ký tự này được dùng thay cho một số nguyên trong bộ chỉ định định dạng. Sau đó, các giá trị cho phần đệm và độ chính xác được truyền vào khi định dạng:

::

    var format_string = "%*.*f"
    # Pad to length of 7, round to 3 decimal places:
    print(format_string % [7, 3, 8.8888])
    # Output: "  8.889"
    # 2 leading spaces

Vẫn có thể đệm bằng các số 0 trong các placeholder số nguyên bằng cách thêm ``0`` trước ``*``:

::

    print("%0*d" % [2, 3])
    # Output: "03"


Chuỗi thoát
-----------

Để chèn một ký tự ``%`` theo nghĩa đen vào chuỗi định dạng, ký tự đó phải được escape để tránh bị đọc như một placeholder. Việc này được thực hiện bằng cách nhân đôi ký tự:

::

    var health = 56
    print("Remaining health: %d%%" % health)
    # Output: "Remaining health: 56%"


Phương thức định dạng chuỗi
---------------------------

Ngoài ra, còn có một cách khác để định dạng văn bản trong GDScript, cụ thể là
phương thức :ref:`String.format() <class_String_method_format>`. Phương thức này thay thế mọi lần xuất hiện của một khóa trong chuỗi bằng giá trị tương ứng. Phương thức này có thể xử lý các mảng hoặc dictionary cho các cặp khóa/giá trị.

Có thể sử dụng mảng làm kiểu key, index hoặc mixed (xem các ví dụ bên dưới). Thứ tự chỉ quan trọng khi sử dụng kiểu index hoặc mixed của Array.

Một ví dụ nhanh trong GDScript:

::

    # Define a format string
    var format_string = "We're waiting for {str}"

    # Using the 'format' method, replace the 'str' placeholder
    var actual_string = format_string.format({"str": "Godot"})

    print(actual_string)
    # Output: "We're waiting for Godot"


Ví dụ về phương thức định dạng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau đây là một số ví dụ về cách sử dụng các cách gọi khác nhau của phương thức ``String.format()``.

+------------+----------------+------------------------------------------------------------------------------+-------------------+
| **Loại**   | **Kiểu**       | **Ví dụ**                                                                    | **Kết quả**       |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Dictionary | key            | ``"Hi, {name} v{version}!".format({"name":"Godette", "version":"3.0"})``     | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Dictionary | index          | ``"Hi, {0} v{1}!".format({"0":"Godette", "1":"3.0"})``                       | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Dictionary | mix            | ``"Hi, {0} v{version}!".format({"0":"Godette", "version":"3.0"})``           | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Array      | key            | ``"Hi, {name} v{version}!".format([["version","3.0"], ["name","Godette"]])`` | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Array      | index          | ``"Hi, {0} v{1}!".format(["Godette","3.0"])``                                | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Array      | mix            | ``"Hi, {name} v{0}!".format(["3.0", ["name","Godette"]])``                   | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+
| Array      | không có index | ``"Hi, {} v{}!".format(["Godette", "3.0"], "{}")``                           | Hi, Godette v3.0! |
+------------+----------------+------------------------------------------------------------------------------+-------------------+

Có thể tùy chỉnh các placeholder khi sử dụng ``String.format``, sau đây là một số ví dụ về chức năng này.


+------------------+------------------------------------------------------+------------------+
| **Loại**         | **Ví dụ**                                            | **Kết quả**      |
+------------------+------------------------------------------------------+------------------+
| Infix (mặc định) | ``"Hi, {0} v{1}".format(["Godette", "3.0"], "{_}")`` | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+
| Postfix          | ``"Hi, 0% v1%".format(["Godette", "3.0"], "_%")``    | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+
| Prefix           | ``"Hi, %0 v%1".format(["Godette", "3.0"], "%_")``    | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+

Việc kết hợp cả phương thức ``String.format`` và toán tử ``%`` có thể hữu ích, vì ``String.format`` không có cách thao tác với biểu diễn của các số.

+---------------------------------------------------------------------------+-------------------+
| **Ví dụ**                                                                 | **Kết quả**       |
+---------------------------------------------------------------------------+-------------------+
| ``"Hi, {0} v{version}".format({0:"Godette", "version":"%0.2f" % 3.114})`` | Hi, Godette v3.11 |
+---------------------------------------------------------------------------+-------------------+

Nối chuỗi
---------

Bạn cũng có thể kết hợp các chuỗi bằng cách *nối* chúng lại với nhau, sử dụng toán tử ``+``.

::

    # Define a base string
    var base_string = "We're waiting for "

    # Concatenate the string
    var actual_string = base_string + "Godot"

    print(actual_string)
    # Output: "We're waiting for Godot"

Khi sử dụng phép nối chuỗi, các giá trị không phải chuỗi phải được chuyển đổi bằng hàm ``str()``. Không có cách nào chỉ định định dạng chuỗi của các giá trị đã chuyển đổi.

::

    var name_string = "Godette"
    var version = 3.0
    var actual_string = "Hi, " + name_string + " v" + str(version) + "!"

    print(actual_string)
    # Output: "Hi, Godette v3!"

Do những hạn chế này, format string hoặc phương thức ``format()`` thường là lựa chọn tốt hơn. Trong nhiều trường hợp, phép nối chuỗi cũng kém dễ đọc hơn.

.. note::

    Trong mã C++ của Godot, có thể truy cập format string của GDScript bằng hàm trợ giúp ``vformat()`` trong header :ref:`Variant<class_Variant>`.
