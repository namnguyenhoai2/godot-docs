.. _doc_gdscript_more_efficiently:

GDScript: Giới thiệu về các ngôn ngữ động
=========================================

Giới thiệu
----------

Tutorial này nhằm cung cấp tài liệu tham khảo nhanh về cách sử dụng GDScript hiệu quả hơn. Tutorial tập trung vào các trường hợp phổ biến đặc thù của ngôn ngữ này, đồng thời cũng trình bày nhiều thông tin về các ngôn ngữ kiểu động.

Tutorial đặc biệt hữu ích cho những lập trình viên có ít hoặc chưa có kinh nghiệm với các ngôn ngữ kiểu động.

Tính chất động
--------------

Ưu và nhược điểm của kiểu động
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

GDScript là một ngôn ngữ kiểu động. Vì vậy, các ưu điểm chính của nó là:

-  Ngôn ngữ này dễ bắt đầu sử dụng.
-  Hầu hết mã nguồn có thể được viết và thay đổi nhanh chóng mà không gặp nhiều trở ngại.
-  Mã nguồn dễ đọc (ít rườm rà).
-  Không cần biên dịch để kiểm thử.
-  Runtime rất nhỏ gọn.
-  Bản chất ngôn ngữ hỗ trợ duck typing và polymorphism.

Trong khi các nhược điểm chính là:

-  Hiệu năng thấp hơn các ngôn ngữ kiểu tĩnh.
-  Khó refactor hơn (không thể truy vết các symbol).
-  Một số lỗi thường được phát hiện tại thời điểm biên dịch trong các ngôn ngữ kiểu tĩnh chỉ xuất hiện khi chạy mã nguồn (vì việc phân tích cú pháp biểu thức nghiêm ngặt hơn).
-  Ít linh hoạt hơn khi tự động hoàn tất mã nguồn (một số kiểu biến chỉ được biết tại runtime).

Điều này, xét trên thực tế, có nghĩa là Godot kết hợp với GDScript được thiết kế để tạo game nhanh chóng và hiệu quả. Đối với những game đòi hỏi tính toán rất cao và không thể tận dụng các công cụ tích hợp sẵn của engine (chẳng hạn như các kiểu Vector, Physics Engine, thư viện Math, v.v.), bạn vẫn có thể sử dụng C++. Nhờ đó, bạn có thể tạo phần lớn game bằng GDScript và thêm một số phần nhỏ bằng C++ ở những khu vực cần tăng hiệu năng.

Biến và phép gán
~~~~~~~~~~~~~~~~

Tất cả biến trong một ngôn ngữ kiểu động đều tương tự "variant". Điều này có nghĩa là kiểu của chúng không cố định và chỉ được thay đổi thông qua phép gán. Ví dụ:

Tĩnh:

.. code-block:: cpp

    int a; // Giá trị chưa được khởi tạo.
    a = 5; // Hợp lệ.
    a = "Hi!"; // Không hợp lệ.

Động:

.. code-block::

    var a # Mặc định là 'null'.
    a = 5 # Hợp lệ, 'a' trở thành một số nguyên.
    a = "Hi!" # Hợp lệ, 'a' được đổi thành một chuỗi.

Với các đối số hàm:
~~~~~~~~~~~~~~~~~~~

Các hàm cũng có tính chất động, nghĩa là chúng có thể được gọi với các đối số khác nhau, ví dụ:

Tĩnh:

.. code-block:: cpp

    void print_value(int value) {

        printf("value is %i\n", value);
    }

    [..]

    print_value(55); // Hợp lệ.
    print_value("Hello"); // Không hợp lệ.

Động:

.. code-block::

    func print_value(value):
        print(value)

    [..]

    print_value(55) # Hợp lệ.
    print_value("Hello") # Hợp lệ.

Con trỏ và tham chiếu:
~~~~~~~~~~~~~~~~~~~~~~

Trong các ngôn ngữ tĩnh như C hoặc C++ (và ở một mức độ nào đó là Java và C#), có sự phân biệt giữa một biến và một con trỏ/tham chiếu đến biến đó. Cách sau cho phép các hàm khác sửa đổi đối tượng bằng cách truyền tham chiếu đến đối tượng ban đầu.

Trong C# hoặc Java, mọi thứ không phải là kiểu dựng sẵn (int, float, đôi khi là String) luôn là một con trỏ hoặc tham chiếu. Các tham chiếu cũng được tự động thu gom rác, nghĩa là chúng sẽ bị xóa khi không còn được sử dụng. Các ngôn ngữ kiểu động cũng có xu hướng sử dụng mô hình bộ nhớ này. Một số ví dụ:

-  C++:

.. code-block:: cpp

    void use_class(SomeClass *instance) {

        instance->use();
    }

    void do_something() {

        SomeClass *instance = new SomeClass; // Được tạo dưới dạng con trỏ.
        use_class(instance); // Được truyền dưới dạng con trỏ.
        delete instance; // Nếu không, nó sẽ làm rò rỉ bộ nhớ.
    }

-  Java:

.. code-block:: java

    @Override
    public final void use_class(SomeClass instance) {

        instance.use();
    }

    public final void do_something() {

        SomeClass instance = new SomeClass(); // Được tạo dưới dạng tham chiếu.
        use_class(instance); // Được truyền dưới dạng tham chiếu.
        // Bộ thu gom rác sẽ loại bỏ nó khi không còn được
        // sử dụng và khiến game của bạn bị đóng băng ngẫu nhiên trong một giây.
    }

-  GDScript:

.. code-block::

    func use_class(instance): # Không quan tâm đến kiểu lớp
        instance.use() # Sẽ hoạt động với bất kỳ lớp nào có phương thức ".use()".

    func do_something():
        var instance = SomeClass.new() # Được tạo dưới dạng tham chiếu.
        use_class(instance) # Được truyền dưới dạng tham chiếu.
        # Sẽ bị bỏ tham chiếu và xóa.

Trong GDScript, chỉ các kiểu cơ bản (int, float, string và các kiểu vector) được truyền theo giá trị cho các hàm (giá trị được sao chép). Mọi thứ khác (instance, array, dictionary, v.v.) được truyền dưới dạng tham chiếu. Các lớp kế thừa :ref:`class_RefCounted` (mặc định nếu không chỉ định gì) sẽ được giải phóng khi không còn được sử dụng, nhưng bạn cũng có thể tự quản lý bộ nhớ nếu kế thừa thủ công từ :ref:`class_Object`.

Array
-----

Các array trong những ngôn ngữ kiểu động có thể chứa nhiều kiểu dữ liệu hỗn hợp khác nhau và luôn mang tính động (có thể thay đổi kích thước bất kỳ lúc nào). Hãy so sánh, chẳng hạn, các array trong những ngôn ngữ kiểu tĩnh:

.. code-block:: cpp

    int *array = new int[4]; // Tạo array.
    array[0] = 10; // Khởi tạo thủ công.
    array[1] = 20; // Không thể trộn các kiểu.
    array[2] = 40;
    array[3] = 60;
    // Không thể thay đổi kích thước.
    use_array(array); // Được truyền dưới dạng con trỏ.
    delete[] array; // Phải được giải phóng.

    // hoặc

    std::vector<int> array;
    array.resize(4);
    array[0] = 10; // Khởi tạo thủ công.
    array[1] = 20; // Không thể trộn các kiểu.
    array[2] = 40;
    array[3] = 60;
    array.resize(3); // Có thể thay đổi kích thước.
    use_array(array); // Được truyền dưới dạng tham chiếu hoặc giá trị.
    // Được giải phóng khi stack kết thúc.

Và trong GDScript:

.. code-block::

    var array = [10, "hello", 40, 60] # Có thể trộn các kiểu.
    array.resize(3) # Có thể thay đổi kích thước.
    use_array(array) # Được truyền dưới dạng tham chiếu.
    # Được giải phóng khi không còn được sử dụng.

Trong các ngôn ngữ kiểu động, mảng cũng có thể đóng vai trò là các kiểu dữ liệu khác, chẳng hạn như list:

.. code-block::

    var array = []
    array.append(4)
    array.append(5)
    array.pop_front()

Hoặc các tập hợp không có thứ tự:

.. code-block::

    var a = 20
    if a in [10, 20, 30]:
        print("We have a winner!")

Dictionaries
------------

Dictionaries là một công cụ mạnh mẽ trong các ngôn ngữ kiểu động. Trong GDScript, dictionaries không kiểu có thể được dùng cho nhiều trường hợp mà ngôn ngữ kiểu tĩnh thường sẽ sử dụng một cấu trúc dữ liệu khác.

Dictionaries có thể ánh xạ bất kỳ giá trị nào tới bất kỳ giá trị nào khác mà hoàn toàn không phụ thuộc vào kiểu dữ liệu được dùng làm khóa hoặc giá trị. Trái với quan niệm phổ biến, chúng hiệu quả vì có thể được triển khai bằng hash table. Trên thực tế, chúng hiệu quả đến mức một số ngôn ngữ còn triển khai mảng dưới dạng dictionaries.

Ví dụ về Dictionary:

.. code-block::

    var d = {"name": "John", "age": 22}
    print("Name: ", d["name"], " Age: ", d["age"])

Dictionaries cũng là kiểu động; bạn có thể thêm hoặc xóa khóa tại bất kỳ thời điểm nào với chi phí thấp:

.. code-block::

    d["mother"] = "Rebecca" # Thêm.
    d["age"] = 11 # Sửa đổi.
    d.erase("name") # Xóa.

Trong hầu hết trường hợp, mảng hai chiều thường có thể được triển khai dễ dàng hơn bằng dictionaries. Sau đây là một ví dụ về trò chơi battleship:

.. code-block::

    # Trò chơi Battleship

    const SHIP = 0
    const SHIP_HIT = 1
    const WATER_HIT = 2

    var board = {}

    func initialize():
        board[Vector2(1, 1)] = SHIP
        board[Vector2(1, 2)] = SHIP
        board[Vector2(1, 3)] = SHIP

    func missile(pos):
        if pos in board: # Có thứ gì đó ở vị trí này.
            if board[pos] == SHIP: # Có một con tàu! Bắn trúng rồi.
                board[pos] = SHIP_HIT
            else:
                print("Already hit here!") # Này, bạn đã bắn vào đây rồi.
        else: # Không có gì, đánh dấu là nước.
            board[pos] = WATER_HIT

    func game():
        initialize()
        missile(Vector2(1, 1))
        missile(Vector2(5, 8))
        missile(Vector2(2, 3))

Dictionaries cũng có thể được dùng làm markup dữ liệu hoặc các cấu trúc nhanh. Mặc dù dictionaries của GDScript tương tự dictionaries của Python, GDScript cũng hỗ trợ cú pháp và cách lập chỉ mục kiểu Lua, khiến nó hữu ích khi viết trạng thái ban đầu và các struct nhanh:

.. code-block::

    # Cùng ví dụ, hỗ trợ kiểu Lua.
    # Cú pháp này dễ đọc và dễ sử dụng hơn nhiều.
    # Giống như mọi identifier của GDScript, các khóa được viết theo dạng này không thể bắt đầu
    # bằng một chữ số.

    var d = {
        name = "John",
        age = 22
    }

    print("Name: ", d.name, " Age: ", d.age) # Sử dụng cách lập chỉ mục dựa trên ".".

    # Lập chỉ mục

    d["mother"] = "Rebecca"
    d.mother = "Caroline" # Cách này cũng có thể được dùng để tạo một khóa mới.

For & while
-----------

Việc lặp bằng vòng lặp for kiểu C trong các ngôn ngữ dẫn xuất từ C có thể khá phức tạp:

.. code-block:: cpp

    const char** strings = new const char*[50];

    [..]

    for (int i = 0; i < 50; i++) {
        printf("Value: %c Index: %d\n", strings[i], i);
    }

    // Ngay cả trong STL:
    std::list<std::string> strings;

    [..]

    for (std::string::const_iterator it = strings.begin(); it != strings.end(); it++) {
        std::cout << *it << std::endl;
    }

Vì vậy, GDScript đưa ra quyết định mang tính định hướng là sử dụng vòng lặp for-in trên các iterable thay thế:

.. code-block::

    for s in strings:
        print(s)

Các kiểu dữ liệu container (mảng và dictionaries) là iterable. Dictionaries cho phép lặp qua các khóa:

.. code-block::

    for key in dict:
        print(key, " -> ", dict[key])

Cũng có thể lặp bằng các chỉ số:

.. code-block::

    for i in range(strings.size()):
        print(strings[i])

Hàm ``range()`` có thể nhận 3 đối số:

.. code-block::

    range(n) # Sẽ đếm từ 0 đến n với bước nhảy 1. Tham số n không được bao gồm.
    range(b, n) # Sẽ đếm từ b đến n với bước nhảy 1. Tham số b được bao gồm. Tham số n không được bao gồm.
    range(b, n, s) # Sẽ đếm từ b đến n với bước nhảy s. Tham số b được bao gồm. Tham số n không được bao gồm.

Một số ví dụ liên quan đến vòng lặp for kiểu C:

.. code-block:: cpp

    for (int i = 0; i < 10; i++) {}

    for (int i = 5; i < 10; i++) {}

    for (int i = 5; i < 10; i += 2) {}

Chuyển thành:

.. code-block::

    for i in range(10):
        pass

    for i in range(5, 10):
        pass

    for i in range(5, 10, 2):
        pass

Và vòng lặp ngược được thực hiện bằng bộ đếm âm:

.. code-block::

    for (int i = 10; i > 0; i--) {}

Trở thành:

::

    for i in range(10, 0, -1):
        pass

While
-----

Các vòng lặp while() giống nhau ở mọi nơi:

.. code-block::

    var i = 0

    while i < strings.size():
        print(strings[i])
        i += 1

Custom iterators
----------------
Bạn có thể tạo các iterator tùy chỉnh nếu các iterator mặc định không hoàn toàn đáp ứng nhu cầu bằng cách ghi đè các hàm ``_iter_init()``, ``_iter_next()`` và ``_iter_get()`` trong script. Sau đây là một cách triển khai iterator tiến mẫu:

.. code-block::

    class ForwardIterator:
        var _start
        var _end
        var _increment

        func _init(start, end, increment):
            _start = start
            _end = end
            _increment = increment

        func _should_continue(current):
            return current < _end

        func _iter_init(iter):
            # Khởi tạo trạng thái để lưu trữ giá trị hiện tại.
            iter[0] = _start
            return _should_continue(iter[0])

        func _iter_next(iter):
            iter[0] += _increment
            return _should_continue(iter[0])

        func _iter_get(iter):
            # Trạng thái không được bọc trong một mảng đối với `_iter_get()`.
            # Giá trị lặp giống với trạng thái.
            return iter

Và có thể được sử dụng như bất kỳ iterator nào khác:

.. code-block::

    var itr = ForwardIterator.new(0, 6, 2)
    for i in itr:
        print(i) # Sẽ in ra 0, 2 và 4.

Có thể lưu trạng thái trong một biến thành viên, nhưng không được khuyến khích. Cần có nhiều trạng thái trong những trường hợp như vòng lặp lồng nhau, khi cùng một instance iterator được sử dụng đồng thời. Tham số ``iter`` trong ``_iter_init()`` và ``_iter_next()`` là một mảng một phần tử để các cập nhật có thể được duy trì. Trong khi đó, trong ``_iter_get()``, trạng thái không được bao bọc vì nó được cho là chỉ đọc.

Việc trả về ``true`` từ ``_iter_init()`` và ``_iter_next()`` cho biết iterator hợp lệ. Trả về ``false`` sẽ kết thúc vòng lặp.

Để biết thêm chi tiết, xem :ref:`_iter_init() <class_Object_private_method__iter_init>`,
:ref:`_iter_next() <class_Object_private_method__iter_next>`, và
:ref:`_iter_get() <class_Object_private_method__iter_get>`.

Duck typing
-----------

Một trong những khái niệm khó nắm bắt nhất khi chuyển từ ngôn ngữ có kiểu tĩnh sang ngôn ngữ động là duck typing. Duck typing giúp thiết kế code tổng thể đơn giản hơn nhiều và dễ viết hơn, nhưng cách thức hoạt động của nó không hề hiển nhiên.

Ví dụ, hãy tưởng tượng một tình huống trong đó một tảng đá lớn đang rơi xuống đường hầm và đập vỡ mọi thứ trên đường đi. Code cho tảng đá trong một ngôn ngữ có kiểu tĩnh sẽ gần như sau:

.. code-block:: cpp

    void BigRollingRock::on_object_hit(Smashable *entity) {

        entity->smash();
    }

Theo cách này, mọi thứ có thể bị tảng đá đập vỡ đều phải kế thừa Smashable. Nếu một nhân vật, kẻ địch, món đồ nội thất hoặc tảng đá nhỏ đều có thể bị đập vỡ, chúng sẽ cần kế thừa từ class Smashable, có thể đòi hỏi đa kế thừa. Nếu không muốn dùng đa kế thừa, chúng sẽ phải kế thừa một class chung như Entity. Tuy nhiên, việc thêm một phương thức ảo ``smash()`` vào Entity chỉ vì một vài đối tượng trong số đó có thể bị đập vỡ sẽ không thật thanh thoát.

Với các ngôn ngữ kiểu động, đây không phải là vấn đề. Duck typing đảm bảo rằng bạn chỉ cần định nghĩa một function ``smash()`` ở nơi cần thiết là đủ. Không cần phải cân nhắc về kế thừa, class cơ sở, v.v.

.. code-block::

    func _on_object_hit(object):
        object.smash()

Vậy là xong. Nếu object bị tảng đá lớn va phải có phương thức smash(), phương thức đó sẽ được gọi. Không cần kế thừa hay đa hình. Các ngôn ngữ kiểu động chỉ quan tâm instance có phương thức hoặc member mong muốn hay không, chứ không quan tâm nó kế thừa gì hoặc thuộc kiểu class nào. Định nghĩa về Duck Typing sau đây sẽ giúp làm rõ hơn:

*"Khi tôi thấy một con chim đi như vịt, bơi như vịt và kêu như vịt, tôi gọi con chim đó là vịt"*

Trong trường hợp này, có thể diễn đạt là:

*"Nếu object có thể bị đập vỡ, đừng quan tâm nó là gì, cứ đập vỡ nó."*

Đúng vậy, thay vào đó chúng ta nên gọi nó là Hulk typing.

Có thể object bị va phải không có function smash(). Một số ngôn ngữ kiểu động đơn giản bỏ qua lời gọi phương thức khi phương thức đó không tồn tại, nhưng GDScript nghiêm ngặt hơn, vì vậy nên kiểm tra xem function có tồn tại hay không:

.. code-block::

    func _on_object_hit(object):
        if object.has_method("smash"):
            object.smash()

Sau đó, định nghĩa phương thức đó, và mọi thứ mà tảng đá chạm vào đều có thể bị đập vỡ.
