.. _doc_gdscript_printf:

Chuỗi định dạng GDScript
========================

Godot cung cấp nhiều cách để thay đổi động nội dung của các chuỗi:

- Chuỗi định dạng: ``var string = "I have %s cats." % "3"``
- Phương thức ``String.format()``: ``var string = "I have {0} cats.".format([3])``
- Nối chuỗi: ``var string = "I have " + str(3) + " cats."``

Trang này giải thích cách sử dụng chuỗi định dạng, đồng thời giải thích ngắn gọn về phương thức ``format()`` và phép nối chuỗi.

Chuỗi định dạng
---------------

*Chuỗi định dạng* là cách tái sử dụng các mẫu văn bản để tạo ngắn gọn những chuỗi khác nhau nhưng tương tự nhau.

Chuỗi định dạng giống như các chuỗi thông thường, ngoại trừ việc chúng chứa một số chuỗi ký tự giữ chỗ nhất định như ``%s``. Sau đó, các vị trí giữ chỗ này có thể được thay thế bằng các tham số truyền cho chuỗi định dạng.

Hãy xem ví dụ GDScript cụ thể sau:

.. code-block::

    # Define a format string with placeholder '%s'
    var format_string = "We're waiting for %s."

    # Sử dụng toán tử '%', vị trí giữ chỗ được thay thế bằng giá trị mong muốn
    var actual_string = format_string % "Godot"

    print(actual_string)
    # Kết quả: "We're waiting for Godot."

Các vị trí giữ chỗ luôn bắt đầu bằng ``%``, nhưng ký tự hoặc các ký tự tiếp theo, *bộ chỉ định định dạng*, sẽ xác định cách giá trị đã cho được chuyển đổi thành chuỗi.

``%s`` được thấy trong ví dụ trên là vị trí giữ chỗ đơn giản nhất và phù hợp với hầu hết các trường hợp sử dụng: nó chuyển đổi giá trị bằng cùng phương thức mà phép chuyển đổi String ngầm định hoặc :ref:`str() <class_@GlobalScope_method_str>` sử dụng. Chuỗi được giữ nguyên, boolean được chuyển thành ``"true"`` hoặc ``"false"``, các kiểu ``int`` và ``float`` trở thành số thập phân, còn các kiểu khác thường trả về dữ liệu của chúng dưới dạng chuỗi dễ đọc.

Có các `bộ chỉ định định dạng <format specifiers_>`_ khác.

Nhiều vị trí giữ chỗ
--------------------

Chuỗi định dạng có thể chứa nhiều vị trí giữ chỗ. Trong trường hợp đó, các giá trị được truyền dưới dạng một mảng, mỗi vị trí giữ chỗ nhận một giá trị (trừ khi sử dụng bộ chỉ định định dạng với ``*``, xem `đệm động <dynamic padding_>`_):

.. code-block::

    var format_string = "%s was reluctant to learn %s, but now he enjoys it."
    var actual_string = format_string % ["Estragon", "GDScript"]

    print(actual_string)
    # Kết quả: "Estragon was reluctant to learn GDScript, but now he enjoys it."

Lưu ý rằng các giá trị được chèn theo thứ tự. Hãy nhớ rằng tất cả vị trí giữ chỗ phải được thay thế cùng lúc, vì vậy số lượng giá trị phải phù hợp.


.. _`Format specifiers`:

Bộ chỉ định định dạng
---------------------

Ngoài ``s``, còn có các bộ chỉ định định dạng khác có thể được sử dụng trong các vị trí giữ chỗ. Chúng gồm một hoặc nhiều ký tự. Một số hoạt động độc lập như ``s``, một số xuất hiện trước các ký tự khác, và một số chỉ hoạt động với các giá trị hoặc ký tự nhất định.


Các kiểu vị trí giữ chỗ
~~~~~~~~~~~~~~~~~~~~~~~

Một và chỉ một trong các ký tự này luôn phải xuất hiện ở vị trí cuối cùng trong bộ chỉ định định dạng. Ngoài ``s``, các ký tự này yêu cầu những kiểu tham số nhất định.

+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``s`` | **Chuyển đổi** đơn giản sang String bằng cùng phương thức như phép chuyển đổi String ngầm định.                                                                                                                                                                                 |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``c`` | Một **ký tự Unicode** duy nhất. Chấp nhận một code point Unicode (số nguyên) hoặc chuỗi một ký tự. Hỗ trợ các giá trị lớn hơn 255.                                                                                                                                              |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``d`` | Một **số nguyên thập phân**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                                                       |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``o`` | Một **số nguyên bát phân**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                                                        |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``x`` | Một **số nguyên thập lục phân** với các chữ cái **viết thường**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                   |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``X`` | Một **số nguyên thập lục phân** với các chữ cái **viết hoa**. Yêu cầu một số nguyên hoặc số thực (sẽ được làm tròn xuống).                                                                                                                                                      |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``f`` | Một **số thực thập phân**. Yêu cầu một số nguyên hoặc số thực.                                                                                                                                                                                                                  |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``v`` | Một **vector**. Chấp nhận mọi đối tượng vector dựa trên float hoặc int ( ``Vector2``, ``Vector3``, ``Vector4``, ``Vector2i``, ``Vector3i`` hoặc ``Vector4i``). Hiển thị các tọa độ vector trong dấu ngoặc đơn, định dạng từng tọa độ như một ``%f``, và sử dụng cùng các bổ từ. |
+-------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Các bổ từ của vị trí giữ chỗ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các ký tự này xuất hiện trước các ký tự nêu trên. Một số chỉ hoạt động trong những điều kiện nhất định.

+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``+``     | Trong các bộ chỉ định số, **hiển thị dấu +** nếu là số dương.                                                                                                                                                            |
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Số nguyên | Thiết lập **đệm**. Đệm bằng khoảng trắng hoặc số 0 nếu số nguyên bắt đầu bằng ``0`` trong vị trí giữ chỗ cho số nguyên hoặc số thực. Ký tự ``0`` ở đầu sẽ bị bỏ qua nếu có ``-``. Khi được sử dụng sau ``.``, xem ``.``. |
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``.``     | Trước ``f`` hoặc ``v``, đặt **độ chính xác** thành 0 chữ số thập phân. Có thể theo sau bằng các số để thay đổi. Đệm bằng các số 0.                                                                                       |
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-``     | **Đệm về bên phải** thay vì bên trái.                                                                                                                                                                                    |
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``*``     | **Đệm động**, yêu cầu thêm một tham số số nguyên để đặt độ đệm hoặc độ chính xác sau ``.``, xem `đệm động <dynamic padding_>`_.                                                                                          |
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Đệm
---

Các ký tự ``.`` (*dot*), ``*`` (*asterisk*), ``-`` (*minus sign*) và chữ số (``0``-``9``) được dùng để đệm. Điều này cho phép in nhiều giá trị được căn chỉnh theo chiều dọc như trong một cột, miễn là sử dụng font có độ rộng cố định.

Để đệm một chuỗi đến độ dài tối thiểu, hãy thêm một số nguyên vào specifier:

.. code-block::

    print("%10d" % 12345)
    # output: "     12345"
    # 5 khoảng trắng ở đầu, cho tổng độ dài là 10

Nếu số nguyên bắt đầu bằng ``0``, các giá trị số nguyên sẽ được đệm bằng số 0 thay vì khoảng trắng:

.. code-block::

    print("%010d" % 12345)
    # output: "0000012345"

Có thể chỉ định độ chính xác cho các số thực bằng cách thêm ``.`` (*dot*) theo sau là một số nguyên. Nếu không có số nguyên sau ``.``, độ chính xác bằng 0 sẽ được sử dụng và giá trị sẽ được làm tròn thành số nguyên. Số nguyên dùng để đệm phải xuất hiện trước dấu chấm.

.. code-block::

    # Đệm đến độ dài tối thiểu là 10, làm tròn đến 3 chữ số thập phân
    print("%10.3f" % 10000.5555)
    # Output: " 10000.556"
    # 1 khoảng trắng ở đầu

Ký tự ``-`` sẽ khiến phần đệm nằm bên phải thay vì bên trái, hữu ích khi căn chỉnh văn bản sang phải:

.. code-block::

    print("%-10d" % 12345678)
    # Output: "12345678  "
    # 2 khoảng trắng ở cuối


.. _`Dynamic padding`:

Đệm động
~~~~~~~~

Bằng cách sử dụng ký tự ``*`` (*asterisk*), có thể đặt phần đệm hoặc độ chính xác mà không cần sửa đổi chuỗi định dạng. Ký tự này được dùng thay cho một số nguyên trong format specifier. Sau đó, các giá trị cho phần đệm và độ chính xác được truyền vào khi định dạng:

.. code-block::

    var format_string = "%*.*f"
    # Đệm đến độ dài 7, làm tròn đến 3 chữ số thập phân:
    print(format_string % [7, 3, 8.8888])
    # Output: "  8.889"
    # 2 khoảng trắng ở đầu

Vẫn có thể đệm bằng số 0 trong các placeholder số nguyên bằng cách thêm ``0`` trước ``*``:

.. code-block::

    print("%0*d" % [2, 3])
    # Output: "03"


Chuỗi escape
------------

Để chèn một ký tự ``%`` theo nghĩa đen vào chuỗi định dạng, cần escape ký tự đó để tránh bị đọc như một placeholder. Việc này được thực hiện bằng cách lặp đôi ký tự:

.. code-block::

    var health = 56
    print("Remaining health: %d%%" % health)
    # Output: "Remaining health: 56%"


Phương thức định dạng chuỗi
---------------------------

Ngoài ra, còn có một cách khác để định dạng văn bản trong GDScript, đó là
:ref:`String.format() <class_String_method_format>` method. Phương thức này thay thế mọi lần xuất hiện của một khóa trong chuỗi bằng giá trị tương ứng. Phương thức có thể xử lý một dictionary hoặc một array. Nếu truyền vào một array, chỉ mục của mỗi phần tử sẽ được dùng làm khóa.

Một ví dụ nhanh trong GDScript:

.. code-block::

    # Define a format string
    var format_string = "We're waiting for {str}"

    # Dùng phương thức 'format', thay thế placeholder 'str'
    var actual_string = format_string.format({"str": "Godot"})

    print(actual_string)
    # Output: "We're waiting for Godot"

.. note::

    Nếu truyền vào một array, cũng có thể chèn các array khác vào bên trong. Mỗi array lồng nhau chỉ được chứa 2 phần tử, chúng sẽ được coi là một cặp khóa-giá trị. Hành vi này **deprecated** và sẽ bị loại bỏ trong tương lai.

Ví dụ về phương thức format
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau đây là một số ví dụ về cách sử dụng các cách gọi khác nhau của phương thức ``String.format()``.

+------------+-----------+--------------------------------------------------------------------------+-------------------+
| **Type**   | **Style** | **Example**                                                              | **Result**        |
+------------+-----------+--------------------------------------------------------------------------+-------------------+
| Dictionary | key       | ``"Hi, {name} v{version}!".format({"name":"Godette", "version":"3.0"})`` | Hi, Godette v3.0! |
+------------+-----------+--------------------------------------------------------------------------+-------------------+
| Dictionary | index     | ``"Hi, {0} v{1}!".format({"0":"Godette", "1":"3.0"})``                   | Hi, Godette v3.0! |
+------------+-----------+--------------------------------------------------------------------------+-------------------+
| Dictionary | mix       | ``"Hi, {0} v{version}!".format({"0":"Godette", "version":"3.0"})``       | Hi, Godette v3.0! |
+------------+-----------+--------------------------------------------------------------------------+-------------------+
| Array      | index     | ``"Hi, {0} v{1}!".format(["Godette","3.0"])``                            | Hi, Godette v3.0! |
+------------+-----------+--------------------------------------------------------------------------+-------------------+
| Array      | no index  | ``"Hi, {} v{}!".format(["Godette", "3.0"], "{}")``                       | Hi, Godette v3.0! |
+------------+-----------+--------------------------------------------------------------------------+-------------------+

Placeholder cũng có thể được tùy chỉnh khi sử dụng ``String.format``, sau đây là một số ví dụ về chức năng đó.


+------------------+------------------------------------------------------+------------------+
| **Type**         | **Example**                                          | **Kết quả**      |
+------------------+------------------------------------------------------+------------------+
| Infix (mặc định) | ``"Hi, {0} v{1}".format(["Godette", "3.0"], "{_}")`` | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+
| Postfix          | ``"Hi, 0% v1%".format(["Godette", "3.0"], "_%")``    | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+
| Prefix           | ``"Hi, %0 v%1".format(["Godette", "3.0"], "%_")``    | Hi, Godette v3.0 |
+------------------+------------------------------------------------------+------------------+

Việc kết hợp cả phương thức ``String.format`` và toán tử ``%`` có thể hữu ích, vì ``String.format`` không có cách nào để thao tác với biểu diễn của các số.

+---------------------------------------------------------------------------+-------------------+
| **Ví dụ**                                                                 | **Kết quả**       |
+---------------------------------------------------------------------------+-------------------+
| ``"Hi, {0} v{version}".format({0:"Godette", "version":"%0.2f" % 3.114})`` | Hi, Godette v3.11 |
+---------------------------------------------------------------------------+-------------------+

Nối chuỗi
---------

Bạn cũng có thể kết hợp các chuỗi bằng cách *ghép nối* chúng lại với nhau, sử dụng toán tử ``+``.

.. code-block::

    # Define a base string
    var base_string = "We're waiting for "

    # Nối chuỗi
    var actual_string = base_string + "Godot"

    print(actual_string)
    # Đầu ra: "We're waiting for Godot"

Khi sử dụng phép nối chuỗi, các giá trị không phải là chuỗi phải được chuyển đổi bằng hàm ``str()``. Không có cách nào để chỉ định định dạng chuỗi của các giá trị đã chuyển đổi.

.. code-block::

    var name_string = "Godette"
    var version = 3.0
    var actual_string = "Hi, " + name_string + " v" + str(version) + "!"

    print(actual_string)
    # Đầu ra: "Hi, Godette v3!"

Do những hạn chế này, chuỗi định dạng hoặc phương thức ``format()`` thường là lựa chọn tốt hơn. Trong nhiều trường hợp, phép nối chuỗi cũng kém dễ đọc hơn.

.. note::

    Trong mã C++ của Godot, bạn có thể truy cập các chuỗi định dạng GDScript bằng hàm trợ giúp ``vformat()`` trong header :ref:`Variant<class_Variant>`.
