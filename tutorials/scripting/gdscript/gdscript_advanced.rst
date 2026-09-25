.. _doc_gdscript_more_efficiently:

GDScript: Giới thiệu về các ngôn ngữ động
=========================================

Giới thiệu
----------

Tutorial này nhằm cung cấp tài liệu tham khảo nhanh về cách sử dụng GDScript hiệu quả hơn. Tutorial tập trung vào các trường hợp phổ biến riêng của ngôn ngữ này, đồng thời cũng đề cập đến nhiều thông tin về các ngôn ngữ kiểu động.

Tutorial này đặc biệt hữu ích cho các lập trình viên có ít hoặc chưa có kinh nghiệm với các ngôn ngữ kiểu động.

Tính động
---------

Ưu và nhược điểm của kiểu động
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

GDScript là một ngôn ngữ kiểu động. Vì vậy, các ưu điểm chính của nó là:

-  Dễ bắt đầu sử dụng ngôn ngữ.
-  Có thể viết và thay đổi phần lớn mã nhanh chóng và dễ dàng.
-  Mã dễ đọc (ít rườm rà).
-  Không cần biên dịch để kiểm thử.
-  Runtime rất nhỏ.
-  Bản chất có duck typing và polymorphism.

Trong khi các nhược điểm chính là:

-  Hiệu năng thấp hơn các ngôn ngữ kiểu tĩnh.
-  Khó refactor hơn (không thể truy vết các symbol).
-  Một số lỗi thường được phát hiện tại thời điểm biên dịch trong các ngôn ngữ kiểu tĩnh chỉ xuất hiện khi chạy mã (vì việc phân tích biểu thức nghiêm ngặt hơn).
-  Kém linh hoạt hơn khi hoàn tất mã (chỉ biết được kiểu của một số biến tại runtime).

Xét trên thực tế, điều này có nghĩa là Godot khi dùng với GDScript là sự kết hợp được thiết kế để tạo game nhanh chóng và hiệu quả. Đối với những game đòi hỏi nhiều tính toán và không thể tận dụng các công cụ tích hợp sẵn của engine (chẳng hạn như các kiểu Vector, Physics Engine, thư viện Math, v.v.), bạn cũng có thể sử dụng C++. Nhờ đó, bạn vẫn có thể tạo phần lớn game bằng GDScript và thêm các đoạn C++ nhỏ vào những khu vực cần tăng hiệu năng.

Biến và phép gán
~~~~~~~~~~~~~~~~

Tất cả biến trong một ngôn ngữ kiểu động đều giống như "variant". Điều này có nghĩa là kiểu của chúng không cố định và chỉ được thay đổi thông qua phép gán. Ví dụ:

Tĩnh:

.. code-block:: cpp

    int a; // Giá trị chưa được khởi tạo.
    a = 5; // Hợp lệ.
    a = "Hi!"; // Không hợp lệ.

Động:

::

    var a # 'null' by default.
    a = 5 # Valid, 'a' becomes an integer.
    a = "Hi!" # Valid, 'a' changed to a string.

Dưới dạng đối số hàm:
~~~~~~~~~~~~~~~~~~~~~

Các hàm cũng có bản chất động, nghĩa là chúng có thể được gọi với những đối số khác nhau, ví dụ:

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

    print_value(55) # Valid.
    print_value("Hello") # Valid.

Con trỏ và tham chiếu:
~~~~~~~~~~~~~~~~~~~~~~

Trong các ngôn ngữ tĩnh như C hoặc C++ (và ở một mức độ nào đó là Java và C#), có sự phân biệt giữa một biến và một con trỏ/tham chiếu đến biến đó. Con trỏ/tham chiếu cho phép các hàm khác sửa đổi đối tượng bằng cách truyền tham chiếu đến đối tượng gốc.

Trong C# hoặc Java, mọi thứ không phải là kiểu dựng sẵn (int, float, đôi khi là String) luôn là một con trỏ hoặc tham chiếu. Các tham chiếu cũng được garbage collector tự động thu gom, nghĩa là chúng bị xóa khi không còn được sử dụng. Các ngôn ngữ kiểu động cũng thường sử dụng mô hình bộ nhớ này. Một số ví dụ:

-  C++:

.. code-block:: cpp

    void use_class(SomeClass *instance) {

        instance->use();
    }

    void do_something() {

        SomeClass *instance = new SomeClass; // Được tạo dưới dạng con trỏ.
        use_class(instance); // Được truyền dưới dạng con trỏ.
        delete instance; // Nếu không, sẽ làm rò rỉ bộ nhớ.
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

    func use_class(instance): # Does not care about class type
        instance.use() # Will work with any class that has a ".use()" method.

    func do_something():
        var instance = SomeClass.new() # Created as reference.
        use_class(instance) # Passed as reference.
        # Will be unreferenced and deleted.

Trong GDScript, chỉ các kiểu cơ sở (int, float, string và các kiểu vector) được truyền theo giá trị cho các hàm (giá trị được sao chép). Mọi thứ khác (instance, array, dictionary, v.v.) được truyền theo tham chiếu. Các class kế thừa :ref:`class_RefCounted` (mặc định nếu không chỉ định gì) sẽ được giải phóng khi không còn được sử dụng, nhưng cũng cho phép quản lý bộ nhớ thủ công nếu kế thừa trực tiếp từ :ref:`class_Object`.

Array
-----

Array trong các ngôn ngữ kiểu động có thể chứa nhiều kiểu dữ liệu hỗn hợp khác nhau bên trong và luôn mang tính động (có thể thay đổi kích thước bất cứ lúc nào). Chẳng hạn, hãy so sánh với array trong các ngôn ngữ kiểu tĩnh:

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
    use_array(array); // Được truyền theo tham chiếu hoặc giá trị.
    // Được giải phóng khi stack kết thúc.

Và trong GDScript:

::

    var array = [10, "hello", 40, 60] # You can mix types.
    array.resize(3) # Can be resized.
    use_array(array) # Passed as reference.
    # Freed when no longer in use.

Trong các ngôn ngữ kiểu động, array cũng có thể đóng vai trò là các kiểu dữ liệu khác, chẳng hạn như list:

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

Dictionary là một công cụ mạnh mẽ trong các ngôn ngữ kiểu động. Trong GDScript, dictionary không định kiểu có thể được sử dụng cho nhiều trường hợp mà một ngôn ngữ kiểu tĩnh thường sẽ dùng một cấu trúc dữ liệu khác.

Dictionary có thể ánh xạ bất kỳ giá trị nào tới bất kỳ giá trị nào khác mà hoàn toàn không phụ thuộc vào kiểu dữ liệu được dùng làm key hoặc value. Trái với quan niệm phổ biến, chúng hiệu quả vì có thể được triển khai bằng hash table. Trên thực tế, chúng hiệu quả đến mức một số ngôn ngữ còn triển khai array dưới dạng dictionary.

Ví dụ về Dictionary:

::

    var d = {"name": "John", "age": 22}
    print("Name: ", d["name"], " Age: ", d["age"])

Dictionary cũng là kiểu dữ liệu động; bạn có thể thêm hoặc xóa key ở bất kỳ thời điểm nào với chi phí thấp:

::

    d["mother"] = "Rebecca" # Addition.
    d["age"] = 11 # Modification.
    d.erase("name") # Removal.

Trong hầu hết trường hợp, array hai chiều thường có thể được triển khai dễ dàng hơn bằng dictionary. Sau đây là một ví dụ về trò chơi battleship:

::

    # Battleship Game

    const SHIP = 0
    const SHIP_HIT = 1
    const WATER_HIT = 2

    var board = {}

    func initialize():
        board[Vector2(1, 1)] = SHIP
        board[Vector2(1, 2)] = SHIP
        board[Vector2(1, 3)] = SHIP

    func missile(pos):
        if pos in board: # Something at that position.
            if board[pos] == SHIP: # There was a ship! hit it.
                board[pos] = SHIP_HIT
            else:
                print("Already hit here!") # Hey dude you already hit here.
        else: # Nothing, mark as water.
            board[pos] = WATER_HIT

    func game():
        initialize()
        missile(Vector2(1, 1))
        missile(Vector2(5, 8))
        missile(Vector2(2, 3))

Dictionary cũng có thể được dùng làm markup dữ liệu hoặc các cấu trúc nhanh. Mặc dù dictionary của GDScript tương tự dictionary của Python, nó cũng hỗ trợ cú pháp và phép lập chỉ mục theo kiểu Lua, rất hữu ích khi viết các trạng thái ban đầu và struct nhanh:

::

    # Same example, lua-style support.
    # This syntax is a lot more readable and usable.
    # Like any GDScript identifier, keys written in this form cannot start
    # with a digit.

    var d = {
        name = "John",
        age = 22
    }

    print("Name: ", d.name, " Age: ", d.age) # Used "." based indexing.

    # Indexing

    d["mother"] = "Rebecca"
    d.mother = "Caroline" # This would work too to create a new key.

For & while
-----------

Việc lặp bằng vòng lặp for theo kiểu C trong các ngôn ngữ bắt nguồn từ C có thể khá phức tạp:

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

Vì lý do này, GDScript đưa ra lựa chọn rõ ràng là sử dụng vòng lặp for-in trên các iterable thay thế:

::

    for s in strings:
        print(s)

Các kiểu dữ liệu container (array và dictionary) đều là iterable. Dictionary cho phép lặp qua các key:

::

    for key in dict:
        print(key, " -> ", dict[key])

Cũng có thể lặp bằng index:

::

    for i in range(strings.size()):
        print(strings[i])

Hàm ``range()`` có thể nhận 3 đối số:

::

    range(n) # Will count from 0 to n in steps of 1. The parameter n is exclusive.
    range(b, n) # Will count from b to n in steps of 1. The parameters b is inclusive. The parameter n is exclusive.
    range(b, n, s) # Will count from b to n, in steps of s. The parameters b is inclusive. The parameter n is exclusive.

Một số ví dụ liên quan đến vòng lặp for theo kiểu C:

.. code-block:: cpp

    for (int i = 0; i < 10; i++) {}

    for (int i = 5; i < 10; i++) {}

    for (int i = 5; i < 10; i += 2) {}

Dịch thành:

::

    for i in range(10):
        pass

    for i in range(5, 10):
        pass

    for i in range(5, 10, 2):
        pass

Và vòng lặp ngược được thực hiện bằng một bộ đếm âm:

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

Bộ lặp tùy chỉnh
----------------
Bạn có thể tạo bộ lặp tùy chỉnh nếu các bộ lặp mặc định không đáp ứng đầy đủ nhu cầu của mình, bằng cách ghi đè các hàm ``_iter_init()``, ``_iter_next()`` và ``_iter_get()`` trong script. Sau đây là một triển khai mẫu của bộ lặp tiến:

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
            # Initialize the state to store the current value.
            iter[0] = _start
            return _should_continue(iter[0])

        func _iter_next(iter):
            iter[0] += _increment
            return _should_continue(iter[0])

        func _iter_get(iter):
            # The state is not wrapped in an array for `_iter_get()`.
            # The iteration value is the same as the state.
            return iter

Và có thể sử dụng nó như bất kỳ bộ lặp nào khác:

::

    var itr = ForwardIterator.new(0, 6, 2)
    for i in itr:
        print(i) # Will print 0, 2, and 4.

Có thể lưu trạng thái trong một biến thành viên, nhưng không được khuyến khích. Cần có nhiều trạng thái trong các trường hợp như vòng lặp lồng nhau, khi cùng một instance của bộ lặp được sử dụng đồng thời. Tham số ``iter`` trong ``_iter_init()`` và ``_iter_next()`` là một array gồm một phần tử để các cập nhật có thể được duy trì. Trong ``_iter_get()``, trạng thái không được bao bọc vì nó được cho là chỉ đọc.

Việc trả về ``true`` từ ``_iter_init()`` và ``_iter_next()`` cho biết bộ lặp hợp lệ. Trả về ``false`` sẽ kết thúc vòng lặp.

Để biết thêm chi tiết, hãy xem :ref:`_iter_init() <class_Object_private_method__iter_init>`,
:ref:`_iter_next() <class_Object_private_method__iter_next>`, và
:ref:`_iter_get() <class_Object_private_method__iter_get>`.

Duck typing
-----------

Một trong những khái niệm khó nắm bắt nhất khi chuyển từ ngôn ngữ kiểu tĩnh sang ngôn ngữ kiểu động là duck typing. Duck typing giúp thiết kế code tổng thể đơn giản hơn nhiều và dễ viết hơn, nhưng cách thức hoạt động của nó không rõ ràng.

Ví dụ, hãy tưởng tượng một tình huống trong đó một tảng đá lớn đang rơi xuống một đường hầm và đập vỡ mọi thứ trên đường đi. Code cho tảng đá trong một ngôn ngữ kiểu tĩnh sẽ tương tự như sau:

.. code-block:: cpp

    void BigRollingRock::on_object_hit(Smashable *entity) {

        entity->smash();
    }

Theo cách này, mọi thứ có thể bị tảng đá đập vỡ đều phải kế thừa Smashable. Nếu một character, enemy, đồ nội thất hoặc tảng đá nhỏ đều có thể bị đập vỡ, chúng sẽ cần kế thừa từ class Smashable, có thể đòi hỏi multiple inheritance. Nếu không muốn dùng multiple inheritance, chúng sẽ phải kế thừa một class chung như Entity. Tuy nhiên, việc thêm một phương thức ảo ``smash()`` vào Entity chỉ vì một vài đối tượng có thể bị đập vỡ sẽ không thật sự thanh lịch.

Với các ngôn ngữ kiểu động, đây không phải là vấn đề. Duck typing đảm bảo rằng bạn chỉ cần định nghĩa hàm ``smash()`` ở nơi cần thiết là đủ. Không cần xét đến inheritance, base class, v.v.

::

    func _on_object_hit(object):
        object.smash()

Vậy là xong. Nếu object bị tảng đá lớn va phải có phương thức smash(), phương thức đó sẽ được gọi. Không cần inheritance hay polymorphism. Các ngôn ngữ kiểu động chỉ quan tâm instance có phương thức hoặc member mong muốn hay không, chứ không quan tâm nó kế thừa từ đâu hoặc thuộc kiểu class nào. Định nghĩa về Duck Typing sau đây sẽ giúp điều này rõ ràng hơn:

*"Khi tôi thấy một con chim đi như vịt, bơi như vịt và kêu như vịt, tôi gọi con chim đó là vịt"*

Trong trường hợp này, có thể diễn giải là:

*"Nếu object có thể bị đập vỡ, thì không cần quan tâm nó là gì, cứ đập vỡ nó."*

Đúng vậy, thay vào đó chúng ta nên gọi nó là Hulk typing.

Có thể object bị va phải không có hàm smash(). Một số ngôn ngữ kiểu động פשוט פשוט bỏ qua lời gọi phương thức khi phương thức đó không tồn tại, nhưng GDScript nghiêm ngặt hơn, vì vậy nên kiểm tra xem hàm có tồn tại hay không:

::

    func _on_object_hit(object):
        if object.has_method("smash"):
            object.smash()

Sau đó, hãy định nghĩa phương thức đó, và bất kỳ thứ gì tảng đá chạm vào cũng có thể bị đập vỡ.
