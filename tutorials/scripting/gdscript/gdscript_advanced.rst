.. _doc_gdscript_more_efficiently:

GDScript: Giới thiệu về các ngôn ngữ động
=========================================

Giới thiệu
----------

Tutorial này nhằm cung cấp một tài liệu tham khảo nhanh về cách sử dụng GDScript hiệu quả hơn. Nội dung tập trung vào các trường hợp phổ biến đặc thù của ngôn ngữ này, đồng thời cũng đề cập đến nhiều thông tin về các ngôn ngữ kiểu động.

Tutorial này đặc biệt hữu ích cho những lập trình viên có ít hoặc chưa có kinh nghiệm với các ngôn ngữ kiểu động.

Tính chất động
--------------

Ưu và nhược điểm của kiểu động
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

GDScript là một ngôn ngữ kiểu động (Dynamically Typed). Vì vậy, các ưu điểm chính của nó là:

-  Ngôn ngữ này dễ bắt đầu. - Hầu hết code có thể được viết và thay đổi nhanh chóng mà không gặp rắc rối. - Code dễ đọc (ít rườm rà). - Không cần biên dịch để kiểm thử. - Runtime rất nhỏ gọn. - Bản chất ngôn ngữ có duck-typing và polymorphism.

Trong khi các nhược điểm chính là:

-  Hiệu năng thấp hơn so với các ngôn ngữ kiểu tĩnh. - Khó refactor hơn (không thể truy vết các symbol). - Một số lỗi vốn thường được phát hiện tại thời điểm biên dịch trong các ngôn ngữ kiểu tĩnh chỉ xuất hiện khi chạy code (vì việc phân tích biểu thức nghiêm ngặt hơn). - Ít linh hoạt hơn trong việc code-completion (một số kiểu biến chỉ được biết tại runtime).

Khi áp dụng vào thực tế, điều này có nghĩa là Godot khi dùng cùng GDScript tạo thành một sự kết hợp được thiết kế để tạo game nhanh chóng và hiệu quả. Đối với những game đòi hỏi tính toán rất lớn và không thể tận dụng các công cụ tích hợp sẵn của engine (chẳng hạn như các kiểu Vector, Physics Engine, thư viện Math, v.v.), bạn vẫn có thể sử dụng C++. Nhờ đó, bạn vẫn có thể tạo phần lớn game bằng GDScript và thêm một số phần nhỏ bằng C++ ở những khu vực cần tăng hiệu năng.

Biến và phép gán
~~~~~~~~~~~~~~~~

Tất cả biến trong một ngôn ngữ kiểu động đều tương tự "variant". Điều này có nghĩa là kiểu của chúng không cố định và chỉ thay đổi thông qua phép gán. Ví dụ:

Tĩnh:

.. code-block:: cpp

    int a; // Giá trị chưa được khởi tạo.
    a = 5; // Điều này hợp lệ.
    a = "Hi!"; // Điều này không hợp lệ.

Động:

::

    var a # Mặc định là 'null'.
    a = 5 # Hợp lệ, 'a' trở thành một số nguyên.
    a = "Hi!" # Hợp lệ, 'a' được đổi thành một chuỗi.

Với các đối số của hàm:
~~~~~~~~~~~~~~~~~~~~~~~

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

::

    func print_value(value):
        print(value)

    [..]

    print_value(55) # Hợp lệ.
    print_value("Hello") # Hợp lệ.

Con trỏ và tham chiếu:
~~~~~~~~~~~~~~~~~~~~~~

Trong các ngôn ngữ tĩnh, chẳng hạn như C hoặc C++ (và ở một mức độ nào đó là Java và C#), có sự khác biệt giữa một biến và một con trỏ/tham chiếu đến biến đó. Cách sau cho phép các hàm khác sửa đổi object bằng cách truyền tham chiếu đến object ban đầu.

Trong C# hoặc Java, mọi thứ không phải là kiểu dựng sẵn (int, float, đôi khi là String) luôn là một con trỏ hoặc tham chiếu. Các tham chiếu cũng được garbage collector tự động thu gom, nghĩa là chúng bị xóa khi không còn được sử dụng. Các ngôn ngữ kiểu động cũng có xu hướng sử dụng mô hình bộ nhớ này. Một số ví dụ:

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
        // Garbage collector sẽ loại bỏ nó khi không còn được
        // sử dụng và khiến game của bạn bị đóng băng ngẫu nhiên trong một giây.
    }

-  GDScript:

::

    func use_class(instance): # Không quan tâm đến kiểu class
        instance.use() # Sẽ hoạt động với bất kỳ class nào có phương thức ".use()".

    func do_something():
        var instance = SomeClass.new() # Được tạo dưới dạng tham chiếu.
        use_class(instance) # Được truyền dưới dạng tham chiếu.
        # Sẽ không còn tham chiếu và bị xóa.

Trong GDScript, chỉ các kiểu cơ sở (int, float, string và các kiểu vector) được truyền theo giá trị cho các hàm (giá trị được sao chép). Mọi thứ khác (instance, array, dictionary, v.v.) được truyền theo tham chiếu. Các class kế thừa :ref:`class_RefCounted` (mặc định nếu không chỉ định gì) sẽ được giải phóng khi không còn được sử dụng, nhưng bạn cũng có thể tự quản lý bộ nhớ nếu kế thừa thủ công từ :ref:`class_Object`.

Array
-----

Array trong các ngôn ngữ kiểu động có thể chứa nhiều kiểu dữ liệu khác nhau bên trong và luôn là kiểu động (có thể thay đổi kích thước bất kỳ lúc nào). Hãy so sánh, chẳng hạn, array trong các ngôn ngữ kiểu tĩnh:

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

::

    var array = [10, "hello", 40, 60] # Bạn có thể trộn các kiểu.
    array.resize(3) # Có thể thay đổi kích thước.
    use_array(array) # Được truyền dưới dạng tham chiếu.
    # Được giải phóng khi không còn được sử dụng.

Trong các ngôn ngữ kiểu động, array cũng có thể đóng vai trò như các kiểu dữ liệu khác, chẳng hạn như list:

::

    var array = []
    array.append(4)
    array.append(5)
    array.pop_front()

Hoặc set không có thứ tự:

::

    var a = 20
    if a in [10, 20, 30]:
        print("We have a winner!")

Dictionary
----------

Dictionary là một công cụ mạnh mẽ trong các ngôn ngữ kiểu động. Trong GDScript, dictionary không định kiểu có thể được dùng cho nhiều trường hợp mà một ngôn ngữ kiểu tĩnh thường sẽ sử dụng một cấu trúc dữ liệu khác.

Dictionary có thể ánh xạ bất kỳ giá trị nào đến bất kỳ giá trị nào khác mà hoàn toàn không quan tâm đến kiểu dữ liệu được dùng làm key hoặc value. Trái với quan niệm phổ biến, chúng có hiệu năng tốt vì có thể được triển khai bằng hash table. Trên thực tế, chúng hiệu quả đến mức một số ngôn ngữ còn triển khai array dưới dạng dictionary.

Ví dụ về Dictionary:

::

    var d = {"name": "John", "age": 22}
    print("Name: ", d["name"], " Age: ", d["age"])

Dictionary cũng là kiểu động; bạn có thể thêm hoặc xóa key vào bất kỳ thời điểm nào với chi phí thấp:

::

    d["mother"] = "Rebecca" # Thêm.
    d["age"] = 11 # Sửa đổi.
    d.erase("name") # Xóa.

Trong hầu hết trường hợp, array hai chiều thường có thể được triển khai dễ dàng hơn bằng dictionary. Dưới đây là ví dụ về một game battleship:

::

    # Game Battleship

    const SHIP = 0
    const SHIP_HIT = 1
    const WATER_HIT = 2

    var board = {}

    func initialize():
        board[Vector2(1, 1)] = SHIP
        board[Vector2(1, 2)] = SHIP
        board[Vector2(1, 3)] = SHIP

    func missile(pos):
        if pos in board: # Có thứ gì đó ở vị trí đó.
            if board[pos] == SHIP: # Có một con tàu! Bắn trúng nó.
                board[pos] = SHIP_HIT
            else:
                print("Already hit here!") # Này bạn, bạn đã bắn vào đây rồi.
        else: # Không có gì, đánh dấu là nước.
            board[pos] = WATER_HIT

    func game():
        initialize()
        missile(Vector2(1, 1))
        missile(Vector2(5, 8))
        missile(Vector2(2, 3))

Dictionary cũng có thể được dùng làm markup dữ liệu hoặc các cấu trúc nhanh. Mặc dù dictionary của GDScript tương tự dictionary của Python, nó cũng hỗ trợ cú pháp và indexing kiểu Lua, khiến nó hữu ích khi viết các trạng thái ban đầu và struct nhanh:

::

    # Cùng ví dụ đó, với hỗ trợ kiểu Lua.
    # Cú pháp này dễ đọc và dễ sử dụng hơn nhiều.
    # Giống như mọi identifier của GDScript, key được viết theo dạng này không thể bắt đầu
    # bằng một chữ số.

    var d = {
        name = "John",
        age = 22
    }

    print("Name: ", d.name, " Age: ", d.age) # Sử dụng indexing dựa trên ".".

    # Indexing

    d["mother"] = "Rebecca"
    d.mother = "Caroline" # Cách này cũng có thể được dùng để tạo một key mới.

For và while
------------

Việc lặp bằng vòng lặp for kiểu C trong các ngôn ngữ bắt nguồn từ C có thể khá phức tạp:

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

Vì lý do này, GDScript đưa ra quyết định mang tính định hướng là sử dụng vòng lặp for-in trên các iterable thay thế:

::

    for s in strings:
        print(s)

Các kiểu dữ liệu container (array và dictionary) đều là iterable. Dictionary cho phép lặp qua các key:

::

    for key in dict:
        print(key, " -> ", dict[key])

Bạn cũng có thể lặp với index:

::

    for i in range(strings.size()):
        print(strings[i])

Hàm ``range()`` có thể nhận 3 đối số:

::

    range(n) # Sẽ đếm từ 0 đến n với bước nhảy 1. Tham số n không được bao gồm.
    range(b, n) # Sẽ đếm từ b đến n với bước nhảy 1. Tham số b được bao gồm. Tham số n không được bao gồm.
    range(b, n, s) # Sẽ đếm từ b đến n với bước nhảy s. Tham số b được bao gồm. Tham số n không được bao gồm.

Một số ví dụ liên quan đến vòng lặp for kiểu C:

.. code-block:: cpp

    for (int i = 0; i < 10; i++) {}

    for (int i = 5; i < 10; i++) {}

    for (int i = 5; i < 10; i += 2) {}

Chuyển thành:

::

    for i in range(10):
        pass

    for i in range(5, 10):
        pass

    for i in range(5, 10, 2):
        pass

Và việc lặp ngược được thực hiện thông qua một bộ đếm âm:

::

    for (int i = 10; i > 0; i--) {}

Trở thành:

::

    for i in range(10, 0, -1):
        pass

While
-----

Vòng lặp while() giống nhau ở mọi nơi:

::

    var i = 0

    while i < strings.size():
        print(strings[i])
        i += 1

Iterator tùy chỉnh
------------------
Bạn có thể tạo iterator tùy chỉnh nếu các iterator mặc định không hoàn toàn đáp ứng nhu cầu của mình, bằng cách override các hàm ``_iter_init()``, ``_iter_next()`` và ``_iter_get()`` trong script. Dưới đây là một triển khai iterator tiến:

::

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
            # Khởi tạo state để lưu trữ giá trị hiện tại.
            iter[0] = _start
            return _should_continue(iter[0])

        func _iter_next(iter):
            iter[0] += _increment
            return _should_continue(iter[0])

        func _iter_get(iter):
            # State không được bọc trong một array cho `_iter_get()`.
            # Giá trị lặp giống với state.
            return iter

Và nó có thể được sử dụng như mọi iterator khác:

::

    var itr = ForwardIterator.new(0, 6, 2)
    for i in itr:
        print(i) # Sẽ in ra 0, 2 và 4.

Có thể lưu state trong một member variable, nhưng không được khuyến khích. Cần có nhiều state trong những trường hợp như các vòng lặp lồng nhau, nơi cùng một iterator instance được sử dụng đồng thời. Tham số ``iter`` trong ``_iter_init()`` và ``_iter_next()`` là một mảng một phần tử để các cập nhật có thể được duy trì. Trong khi đó, trong ``_iter_get()``, state không được bọc vì nó được cho là chỉ-đọc.

Việc trả về ``true`` từ ``_iter_init()`` và ``_iter_next()`` cho biết iterator hợp lệ. Trả về ``false`` sẽ kết thúc vòng lặp.

Để biết thêm chi tiết, hãy xem :ref:`_iter_init() <class_Object_private_method__iter_init>`,
:ref:`_iter_next() <class_Object_private_method__iter_next>`, and
:ref:`_iter_get() <class_Object_private_method__iter_get>`.

Duck typing
-----------

Một trong những khái niệm khó nắm bắt nhất khi chuyển từ một ngôn ngữ được định kiểu tĩnh sang một ngôn ngữ động là duck typing. Duck typing khiến việc thiết kế code tổng thể trở nên đơn giản hơn nhiều và dễ viết hơn, nhưng cách nó hoạt động không hề rõ ràng.

Ví dụ, hãy hình dung một tình huống trong đó một tảng đá lớn đang rơi xuống một đường hầm và đập vỡ mọi thứ trên đường đi. Code cho tảng đá trong một ngôn ngữ được định kiểu tĩnh sẽ tương tự như sau:

.. code-block:: cpp

    void BigRollingRock::on_object_hit(Smashable *entity) {

        entity->smash();
    }

Theo cách này, mọi thứ có thể bị một tảng đá đập vỡ đều phải kế thừa Smashable. Nếu một nhân vật, kẻ địch, món đồ nội thất hoặc tảng đá nhỏ đều có thể bị đập vỡ, chúng sẽ cần kế thừa từ class Smashable, có thể phải dùng multiple inheritance. Nếu không muốn dùng multiple inheritance, chúng sẽ phải kế thừa một class chung như Entity. Tuy nhiên, sẽ không thật thanh lịch nếu thêm một virtual method ``smash()`` vào Entity chỉ vì một vài đối tượng trong số đó có thể bị đập vỡ.

Với các ngôn ngữ được định kiểu động, đây không phải là vấn đề. Duck typing đảm bảo rằng bạn chỉ cần định nghĩa một function ``smash()`` ở nơi cần thiết là xong. Không cần phải cân nhắc inheritance, base class, v.v.

::

    func _on_object_hit(object):
        object.smash()

Vậy là xong. Nếu object va vào tảng đá lớn có method smash(), method đó sẽ được gọi. Không cần inheritance hay polymorphism. Các ngôn ngữ được định kiểu động chỉ quan tâm instance có method hoặc member mong muốn hay không, chứ không quan tâm nó kế thừa gì hoặc thuộc class type nào. Định nghĩa về Duck Typing dưới đây sẽ giúp điều này rõ ràng hơn:

*"Khi tôi thấy một con chim đi như vịt, bơi như vịt và kêu như vịt, tôi gọi con chim đó là vịt"*

Trong trường hợp này, điều đó có nghĩa là:

*"Nếu object có thể bị đập vỡ, thì không cần quan tâm nó là gì, cứ đập vỡ nó đi."*

Đúng vậy, thay vào đó chúng ta nên gọi nó là Hulk typing.

Có thể object bị va phải không có function smash(). Một số ngôn ngữ được định kiểu động đơn giản là bỏ qua lời gọi method khi method đó không tồn tại, nhưng GDScript nghiêm ngặt hơn, vì vậy nên kiểm tra xem function có tồn tại hay không:

::

    func _on_object_hit(object):
        if object.has_method("smash"):
            object.smash()

Sau đó, hãy định nghĩa method đó và mọi thứ mà tảng đá chạm vào đều có thể bị đập vỡ.
