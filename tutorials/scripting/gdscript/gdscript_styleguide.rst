.. _doc_gdscript_styleguide:

Hướng dẫn phong cách GDScript
=============================

Hướng dẫn phong cách này liệt kê các quy ước để viết GDScript thanh thoát. Mục tiêu là khuyến khích viết mã sạch, dễ đọc và thúc đẩy tính nhất quán giữa các dự án, cuộc thảo luận và hướng dẫn. Hy vọng rằng tài liệu này cũng hỗ trợ việc phát triển các công cụ tự động định dạng.

Vì GDScript khá tương đồng với Python, hướng dẫn này lấy cảm hứng từ hướng dẫn phong cách lập trình `PEP 8 <https://www.python.org/dev/peps/pep-0008/>`__ của Python.

Hướng dẫn phong cách không phải là những bộ quy tắc cứng nhắc. Đôi khi, bạn có thể không áp dụng được một số hướng dẫn dưới đây. Khi đó, hãy dùng phán đoán tốt nhất của mình và hỏi các nhà phát triển khác để có thêm góc nhìn.

Nhìn chung, việc giữ cho mã nhất quán trong các dự án và trong nhóm của bạn quan trọng hơn việc tuân thủ hoàn toàn hướng dẫn này.

.. note::

    Trình soạn thảo script tích hợp của Godot mặc định đã sử dụng nhiều quy ước trong số này. Hãy để nó hỗ trợ bạn.

Dưới đây là một ví dụ lớp hoàn chỉnh dựa trên các hướng dẫn này:

::

    class_name StateMachine
    extends Node
    ## Máy trạng thái phân cấp cho người chơi.
    ##
    ## Khởi tạo các trạng thái và ủy quyền các callback của engine ([method Node._physics_process],
    ## [method Node._unhandled_input]) cho trạng thái.

    signal state_changed(previous, new)

    @export var initial_state: Node
    var is_active = true:
        set = set_is_active

    @onready var _state = initial_state:
        set = set_state
    @onready var _state_name = _state.name


    func _init():
        add_to_group("state_machine")


    func _enter_tree():
        print("this happens before the ready method!")


    func _ready():
        state_changed.connect(_on_state_changed)
        _state.enter()


    func _unhandled_input(event):
        _state.unhandled_input(event)


    func _physics_process(delta):
        _state.physics_process(delta)


    func transition_to(target_state_path, msg={}):
        if not has_node(target_state_path):
            return

        var target_state = get_node(target_state_path)
        assert(target_state.is_composite == false)

        _state.exit()
        self._state = target_state
        _state.enter(msg)
        Events.player_state_changed.emit(_state.name)


    func set_is_active(value):
        is_active = value
        set_physics_process(value)
        set_process_unhandled_input(value)
        set_block_signals(not value)


    func set_state(value):
        _state = value
        _state_name = _state.name


    func _on_state_changed(previous, new):
        print("state changed")
        state_changed.emit()


    class State:
        var foo = 0

        func _init():
            print("Hello!")

.. _formatting:

Định dạng
---------

Mã hóa và ký tự đặc biệt
~~~~~~~~~~~~~~~~~~~~~~~~

* Sử dụng ký tự line feed (**LF**) để ngắt dòng, không dùng CRLF hoặc CR. *(mặc định của trình soạn thảo)* * Sử dụng một ký tự line feed ở cuối mỗi tệp. *(mặc định của trình soạn thảo)* * Sử dụng mã hóa **UTF-8** không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`_. *(mặc định của trình soạn thảo)* * Sử dụng **Tab** thay vì dấu cách để thụt lề. *(mặc định của trình soạn thảo)*

Thụt lề
~~~~~~~

Mỗi cấp thụt lề phải lớn hơn một cấp so với block chứa nó.

**Tốt**:

.. rst-class:: code-example-good

::

    for i in range(10):
        print("hello")

**Không tốt**:

.. rst-class:: code-example-bad

::

    for i in range(10):
      print("hello")

    for i in range(10):
            print("hello")

Sử dụng 2 cấp thụt lề để phân biệt các dòng tiếp nối với các block mã thông thường.

**Tốt**:

.. rst-class:: code-example-good

::

    effect.interpolate_property(sprite, "transform/scale",
            sprite.get_scale(), Vector2(2.0, 2.0), 0.3,
            Tween.TRANS_QUAD, Tween.EASE_OUT)

**Không tốt**:

.. rst-class:: code-example-bad

::

    effect.interpolate_property(sprite, "transform/scale",
        sprite.get_scale(), Vector2(2.0, 2.0), 0.3,
        Tween.TRANS_QUAD, Tween.EASE_OUT)

Ngoại lệ của quy tắc này là array, dictionary và enum. Sử dụng một cấp thụt lề để phân biệt các dòng tiếp nối:

**Tốt**:

.. rst-class:: code-example-good

::

    var party = [
        "Godot",
        "Godette",
        "Steve",
    ]

    var character_dict = {
        "Name": "Bob",
        "Age": 27,
        "Job": "Mechanic",
    }

    enum Tile {
        BRICK,
        FLOOR,
        SPIKE,
        TELEPORT,
    }

**Không tốt**:

.. rst-class:: code-example-bad

::

    var party = [
            "Godot",
            "Godette",
            "Steve",
    ]

    var character_dict = {
            "Name": "Bob",
            "Age": 27,
            "Job": "Mechanic",
    }

    enum Tile {
            BRICK,
            FLOOR,
            SPIKE,
            TELEPORT,
    }

Dấu phẩy ở cuối
~~~~~~~~~~~~~~~

Sử dụng dấu phẩy ở cuối dòng cuối cùng trong array, dictionary và enum. Điều này giúp việc refactor dễ dàng hơn và tạo ra các diff tốt hơn trong hệ thống kiểm soát phiên bản, vì không cần sửa dòng cuối cùng khi thêm phần tử mới.

**Tốt**:

.. rst-class:: code-example-good

::

    var array = [
        1,
        2,
        3,
    ]

**Không tốt**:

.. rst-class:: code-example-bad

::

    var array = [
        1,
        2,
        3
    ]

Dấu phẩy ở cuối là không cần thiết trong các danh sách một dòng, vì vậy đừng thêm chúng trong trường hợp này.

**Tốt**:

.. rst-class:: code-example-good

::

    var array = [1, 2, 3]

**Không tốt**:

.. rst-class:: code-example-bad

::

    var array = [1, 2, 3,]

Dòng trống
~~~~~~~~~~

Bao quanh các hàm và định nghĩa lớp bằng hai dòng trống:

::

    func heal(amount):
        health += amount
        health = min(health, max_health)
        health_changed.emit(health)


    func take_damage(amount, effect=null):
        health -= amount
        health = max(0, health)
        health_changed.emit(health)

Sử dụng một dòng trống bên trong hàm để phân tách các phần logic.

.. note::

    Chúng tôi sử dụng một dòng giữa các lớp và định nghĩa hàm trong phần tham chiếu lớp cũng như trong các đoạn mã ngắn của tài liệu này.

Độ dài dòng
~~~~~~~~~~~

Giữ từng dòng mã dưới 100 ký tự.

Nếu có thể, hãy cố gắng giữ các dòng dưới 80 ký tự. Điều này giúp đọc mã trên màn hình nhỏ và khi mở hai script cạnh nhau trong một trình soạn thảo văn bản bên ngoài. Ví dụ, khi xem một revision khác biệt.

Mỗi dòng một câu lệnh
~~~~~~~~~~~~~~~~~~~~~

Tránh kết hợp nhiều câu lệnh trên một dòng, bao gồm cả các câu lệnh điều kiện, để tuân thủ hướng dẫn phong cách GDScript về khả năng đọc.

**Tốt**:

.. rst-class:: code-example-good

::

    if position.x > width:
        position.x = 0

    if flag:
        print("flagged")

**Không tốt**:

.. rst-class:: code-example-bad

::

    if position.x > width: position.x = 0

    if flag: print("flagged")

Ngoại lệ duy nhất của quy tắc này là toán tử ternary:

::

    next_state = "idle" if is_on_floor() else "fall"

Định dạng các câu lệnh nhiều dòng để dễ đọc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi bạn có các câu lệnh ``if`` đặc biệt dài hoặc các biểu thức ternary lồng nhau, việc ngắt chúng thành nhiều dòng sẽ cải thiện khả năng đọc. Vì các dòng tiếp nối vẫn là một phần của cùng biểu thức, nên sử dụng 2 cấp thụt lề thay vì một cấp.

GDScript cho phép ngắt câu lệnh thành nhiều dòng bằng dấu ngoặc đơn hoặc dấu gạch chéo ngược. Hướng dẫn phong cách này ưu tiên dấu ngoặc đơn vì chúng giúp refactor dễ dàng hơn. Với dấu gạch chéo ngược, bạn phải đảm bảo dòng cuối cùng không bao giờ chứa dấu gạch chéo ngược ở cuối. Với dấu ngoặc đơn, bạn không cần lo dòng cuối có dấu gạch chéo ngược ở cuối.

When wrapping a conditional expression over multiple lines, the ``and``/``or`` keywords should be placed at the beginning of the line continuation, not at the end of the previous line.

**Tốt**:

.. rst-class:: code-example-good

::

    var angle_degrees = 135
    var quadrant = (
            "northeast" if angle_degrees <= 90
            else "southeast" if angle_degrees <= 180
            else "southwest" if angle_degrees <= 270
            else "northwest"
    )

    var position = Vector2(250, 350)
    if (
            position.x > 200 and position.x < 400
            and position.y > 300 and position.y < 400
    ):
        pass

**Không tốt**:

.. rst-class:: code-example-bad

::

    var angle_degrees = 135
    var quadrant = "northeast" if angle_degrees <= 90 else "southeast" if angle_degrees <= 180 else "southwest" if angle_degrees <= 270 else "northwest"

    var position = Vector2(250, 350)
    if position.x > 200 and position.x < 400 and position.y > 300 and position.y < 400:
        pass

Tránh dấu ngoặc không cần thiết
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tránh sử dụng dấu ngoặc trong biểu thức và câu lệnh điều kiện. Trừ khi cần thiết cho thứ tự thực hiện phép toán hoặc để ngắt thành nhiều dòng, chúng chỉ làm giảm khả năng đọc.

**Tốt**:

.. rst-class:: code-example-good

::

    if is_colliding():
        queue_free()

**Không tốt**:

.. rst-class:: code-example-bad

::

    if (is_colliding()):
        queue_free()

.. _boolean_operators:

Toán tử boolean
~~~~~~~~~~~~~~~

Ưu tiên các phiên bản tiếng Anh thông thường của toán tử boolean vì chúng dễ tiếp cận nhất:

- Sử dụng ``and`` thay vì ``&&``. - Sử dụng ``or`` thay vì ``||``. - Sử dụng ``not`` thay vì ``!``.

Bạn cũng có thể sử dụng dấu ngoặc quanh các toán tử boolean để loại bỏ mọi sự mơ hồ. Điều này có thể giúp đọc các biểu thức dài dễ hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    if (foo and bar) or not baz:
        print("condition is true")

**Không tốt**:

.. rst-class:: code-example-bad

::

    if foo && bar || !baz:
        print("condition is true")

Khoảng cách trong comment
~~~~~~~~~~~~~~~~~~~~~~~~~

Regular comments (``#``) and documentation comments (``##``) should start with a space, but not code that you comment out. Additionally, code region comments (``#region``/``#endregion``) must follow that precise syntax, so they should not start with a space.

Việc sử dụng dấu cách cho comment thông thường và comment tài liệu giúp phân biệt comment văn bản với mã bị vô hiệu hóa.

**Tốt**:

.. rst-class:: code-example-good

::

    # Đây là một comment.
    #print("Đây là mã bị vô hiệu hóa")

**Không tốt**:

.. rst-class:: code-example-bad

::

    #Đây là một comment.
    # print("Đây là mã bị vô hiệu hóa")

.. note::

    Trong trình soạn thảo script, để bật hoặc tắt comment cho mã đã chọn, hãy nhấn
    :kbd:`Ctrl + K`. This shortcut adds/removes a single ``#`` sign before any
    mã trên các dòng đã chọn.

Ưu tiên viết comment trên dòng riêng thay vì comment nội tuyến (comment được viết trên cùng dòng với mã). Comment nội tuyến phù hợp nhất cho các comment ngắn, thường chỉ vài từ:

**Tốt**:

.. rst-class:: code-example-good

::

    # Đây là một comment dài, nếu viết nội tuyến sẽ khiến dòng bên dưới quá dài.
    print("Example") # Comment ngắn.

**Không tốt**:

.. rst-class:: code-example-bad

::

    print("Example") # Đây là một comment dài, nếu viết nội tuyến sẽ khiến dòng này quá dài.

Khoảng trắng
~~~~~~~~~~~~

Luôn sử dụng một dấu cách quanh các toán tử và sau dấu phẩy. Ngoài ra, tránh các dấu cách thừa trong tham chiếu dictionary và lời gọi hàm. Một ngoại lệ là khai báo dictionary một dòng, trong đó nên thêm một dấu cách sau dấu ngoặc nhọn mở và trước dấu ngoặc nhọn đóng. Điều này giúp phân biệt dictionary với array bằng mắt dễ hơn, vì các ký tự ``[]`` trông gần giống ``{}`` trong hầu hết phông chữ.

**Tốt**:

.. rst-class:: code-example-good

::

    position.x = 5
    position.y = target_position.y + 10
    dict["key"] = 5
    my_array = [4, 5, 6]
    my_dictionary = { key = "value" }
    print("foo")

**Không tốt**:

.. rst-class:: code-example-bad

::

    position.x=5
    position.y = mpos.y+10
    dict ["key"] = 5
    myarray = [4,5,6]
    my_dictionary = {key = "value"}
    print ("foo")

Không sử dụng dấu cách để căn chỉnh biểu thức theo chiều dọc:

::

    x        = 100
    y        = 100
    velocity = 500

Dấu nháy
~~~~~~~~

Sử dụng dấu nháy kép, trừ khi dấu nháy đơn giúp giảm số ký tự cần escape trong một chuỗi nhất định. Xem các ví dụ dưới đây:

::

    # Chuỗi thông thường.
    print("hello world")

    # Sử dụng dấu nháy kép như thường lệ để tránh escape.
    print("hello 'world'")

    # Sử dụng dấu nháy đơn như một ngoại lệ của quy tắc để tránh escape.
    print('hello "world"')

    # Cả hai kiểu dấu nháy đều cần 2 escape; nếu ngang nhau, hãy ưu tiên dấu nháy kép.
    print("'hello' \"world\"")

Số
~~~

Không bỏ qua số 0 ở đầu hoặc cuối trong các số dấu phẩy động. Nếu không, chúng sẽ khó đọc hơn và khó phân biệt với số nguyên khi nhìn thoáng qua.

**Tốt**:

.. rst-class:: code-example-good

::

    var float_number = 0.234
    var other_float_number = 13.0

**Không tốt**:

.. rst-class:: code-example-bad

::

    var float_number = .234
    var other_float_number = 13.

Sử dụng chữ thường cho các chữ cái trong số hexadecimal, vì chiều cao thấp hơn giúp số dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    var hex_number = 0xfb8c0b

**Không tốt**:

.. rst-class:: code-example-bad

::

    var hex_number = 0xFB8C0B

Tận dụng dấu gạch dưới trong literal của GDScript để giúp các số lớn dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    var large_number = 1_234_567_890
    var large_hex_number = 0xffff_f8f8_0000
    var large_bin_number = 0b1101_0010_1010
    # Các số nhỏ hơn 1000000 nhìn chung không cần dấu phân cách.
    var small_number = 12345

**Không tốt**:

.. rst-class:: code-example-bad

::

    var large_number = 1234567890
    var large_hex_number = 0xfffff8f80000
    var large_bin_number = 0b110100101010
    # Các số nhỏ hơn 1000000 nhìn chung không cần dấu phân cách.
    var small_number = 12_345

.. _naming_conventions:

Quy ước đặt tên
---------------

Các quy ước đặt tên này tuân theo phong cách của Godot Engine. Việc không tuân thủ sẽ khiến mã của bạn xung đột với các quy ước đặt tên tích hợp, dẫn đến mã không nhất quán. Bảng tóm tắt:

+---------------+----------------+----------------------------------------------------+
| Type          | Convention     | Example                                            |
+===============+================+====================================================+
| File names    | snake_case     | ``yaml_parser.gd``                                 |
+---------------+----------------+----------------------------------------------------+
| Class names   | PascalCase     | ``class_name YAMLParser``                          |
+---------------+----------------+----------------------------------------------------+
| Node names    | PascalCase     | ``Camera3D``, ``Player``                           |
+---------------+----------------+----------------------------------------------------+
| Functions     | snake_case     | ``func load_level():``                             |
+---------------+----------------+----------------------------------------------------+
| Variables     | snake_case     | ``var particle_effect``                            |
+---------------+----------------+----------------------------------------------------+
| Signals       | snake_case     | ``signal door_opened``                             |
+---------------+----------------+----------------------------------------------------+
| Constants     | CONSTANT_CASE  | ``const MAX_SPEED = 200``                          |
+---------------+----------------+----------------------------------------------------+
| Enum names    | PascalCase     | ``enum Element``                                   |
+---------------+----------------+----------------------------------------------------+
| Enum members  | CONSTANT_CASE  | ``{EARTH, WATER, AIR, FIRE}``                      |
+---------------+----------------+----------------------------------------------------+

Tên tệp
~~~~~~~

Sử dụng snake_case cho tên tệp. Đối với các lớp có tên, hãy chuyển tên lớp PascalCase thành snake_case:

::

    # Tệp này nên được lưu dưới dạng `weapon.gd`.
    class_name Weapon
    extends Node

::

    # Tệp này nên được lưu dưới dạng `yaml_parser.gd`.
    class_name YAMLParser
    extends Object

Điều này nhất quán với cách đặt tên các tệp C++ trong mã nguồn của Godot. Điều này cũng tránh các vấn đề phân biệt chữ hoa chữ thường có thể xảy ra khi export một project từ Windows sang các nền tảng khác.

Class và node
~~~~~~~~~~~~~

Sử dụng PascalCase cho tên class và node:

::

    extends CharacterBody3D

Cũng sử dụng PascalCase khi nạp một class vào một hằng số hoặc biến:

::

    const Weapon = preload("res://weapon.gd")

Function và biến
~~~~~~~~~~~~~~~~

Sử dụng snake\_case để đặt tên cho function và biến:

::

    var particle_effect
    func load_level():

Thêm một dấu gạch dưới đơn (\_) vào trước các function virtual mà người dùng phải override, các function private và các biến private:

::

    var _counter = 0
    func _recalculate_path():

Signal
~~~~~~

Sử dụng thì quá khứ để đặt tên cho signal:

::

    signal door_opened
    signal score_changed

Hằng số và enum
~~~~~~~~~~~~~~~

Viết hằng số bằng CONSTANT\_CASE, tức là viết hoa toàn bộ và dùng dấu gạch dưới (\_) để phân tách các từ:

::

    const MAX_SPEED = 200

Sử dụng PascalCase cho *tên* enum và giữ chúng ở dạng số ít, vì chúng đại diện cho một kiểu. Sử dụng CONSTANT\_CASE cho các member của chúng, vì chúng là các hằng số:

::

    enum Element {
        EARTH,
        WATER,
        AIR,
        FIRE,
    }

Viết enum với mỗi item trên một dòng riêng. Điều này giúp dễ dàng thêm các chú thích documentation phía trên từng item hơn, đồng thời tạo ra các diff trong hệ thống quản lý version gọn gàng hơn khi item được thêm hoặc xóa.

**Tốt**:

.. rst-class:: code-example-good

::

    enum Element {
        EARTH,
        WATER,
        AIR,
        FIRE,
    }

**Không tốt**:

.. rst-class:: code-example-bad

::

    enum Element { EARTH, WATER, AIR, FIRE }

Thứ tự code
-----------

Phần này tập trung vào thứ tự code. Để biết về formatting, hãy xem
:ref:`formatting`. For naming conventions, see :ref:`naming_conventions`.

Chúng tôi đề xuất tổ chức code GDScript như sau:

::

    01. @tool, @icon, @static_unload
    02. class_name
    03. extends
    04. ## doc comment

    05. signals
    06. enums
    07. constants
    08. static variables
    09. @export variables
    10. remaining regular variables
    11. @onready variables

    12. _static_init()
    13. remaining static methods
    14. overridden built-in virtual methods:
        1. _init()
        2. _enter_tree()
        3. _ready()
        4. _process()
        5. _physics_process()
        6. remaining virtual methods
    15. overridden custom methods
    16. remaining methods
    17. inner classes

Và đặt các method cùng biến của class theo thứ tự sau, tùy thuộc vào access modifier của chúng:

::

    1. public
    2. private

Chúng tôi đã tối ưu thứ tự này để giúp dễ đọc code từ trên xuống dưới, giúp các developer lần đầu đọc code hiểu cách code hoạt động, đồng thời tránh các lỗi liên quan đến thứ tự khai báo biến.

Thứ tự code này tuân theo bốn quy tắc kinh nghiệm:

1. 1. Property và signal đứng trước, tiếp theo là method. 2. Public đứng trước private. 3. Virtual callback đứng trước interface của class. 4. Các function xây dựng và khởi tạo object, ``_init`` và ``_ready``, đứng trước các function thay đổi object trong runtime.

Khai báo class
~~~~~~~~~~~~~~

Nếu code được dùng để chạy trong editor, đặt annotation ``@tool`` ở dòng đầu tiên của script.

Tiếp theo là ``@icon`` tùy chọn, rồi đến ``class_name`` nếu cần. Bạn có thể biến một tệp GDScript thành một global type trong project bằng ``class_name``. Để biết thêm thông tin, hãy xem :ref:`doc_gdscript_basics_class_name`. Nếu class được dùng làm một :ref:`abstract class <doc_gdscript_basics_abstract_class>`, hãy thêm ``@abstract`` *trước* keyword ``class_name``.

Sau đó, thêm keyword ``extends`` nếu class kế thừa một built-in type.

Tiếp theo, bạn nên có phần tùy chọn của class
:ref:`documentation comments <doc_gdscript_documentation_comments>`.
Bạn có thể dùng phần này để giải thích vai trò của class cho các đồng đội, cách class hoạt động và cách các developer khác nên sử dụng nó, chẳng hạn như:

::

    @abstract
    class_name MyNode
    extends Node
    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.

Đối với inner class, hãy sử dụng khai báo một dòng:

::

    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.
    @abstract class MyNode extends Node:
        pass

Signal và property
~~~~~~~~~~~~~~~~~~

Viết các khai báo signal, tiếp theo là property, tức là các biến member, sau docstring.

Enum nên được đặt sau signal, vì bạn có thể dùng chúng làm export hint cho các property khác.

Sau đó, viết các hằng số, biến được export, biến public, private và onready theo thứ tự đó.

::

    signal player_spawned(position)

    enum Job {
        KNIGHT,
        WIZARD,
        ROGUE,
        HEALER,
        SHAMAN,
    }

    const MAX_LIVES = 3

    @export var job: Job = Job.KNIGHT
    @export var max_health = 50
    @export var attack = 5

    var health = max_health:
        set(new_health):
            health = new_health

    var _speed = 300.0

    @onready var sword = get_node("Sword")
    @onready var gun = get_node("Gun")


.. note::

    GDScript đánh giá các biến ``@onready`` ngay trước callback ``_ready``. Bạn có thể dùng điều này để cache các dependency của node, tức là lấy các node con trong scene mà class của bạn phụ thuộc vào. Đây là điều mà ví dụ trên minh họa.

Biến member
~~~~~~~~~~~

Đừng khai báo biến member nếu chúng chỉ được dùng cục bộ trong một method, vì điều đó khiến code khó theo dõi hơn. Thay vào đó, hãy khai báo chúng dưới dạng biến local trong phần thân của method.

Biến local
~~~~~~~~~~

Khai báo biến local gần vị trí sử dụng đầu tiên của chúng nhất có thể. Điều này giúp dễ theo dõi code hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.

Method và static function
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau các property của class là các method.

Bắt đầu bằng method callback ``_init()``, được engine gọi khi tạo object trong memory. Tiếp theo là callback ``_ready()``, được Godot gọi khi thêm một node vào scene tree.

Các function này nên đứng trước vì chúng cho thấy cách object được khởi tạo.

Các virtual callback tích hợp khác, như ``_unhandled_input()`` và ``_physics_process``, nên đứng tiếp theo. Chúng điều khiển main loop của object và các tương tác với game engine.

Phần interface còn lại của class, gồm các method public và private, đứng sau đó theo thứ tự này.

::

    func _init():
        add_to_group("state_machine")


    func _ready():
        state_changed.connect(_on_state_changed)
        _state.enter()


    func _unhandled_input(event):
        _state.unhandled_input(event)


    func transition_to(target_state_path, msg={}):
        if not has_node(target_state_path):
            return

        var target_state = get_node(target_state_path)
        assert(target_state.is_composite == false)

        _state.exit()
        self._state = target_state
        _state.enter(msg)
        Events.player_state_changed.emit(_state.name)


    func _on_state_changed(previous, new):
        print("state changed")
        state_changed.emit()


Static typing
-------------

GDScript hỗ trợ :ref:`optional static typing<doc_gdscript_static_typing>`.

Kiểu được khai báo
~~~~~~~~~~~~~~~~~~

Để khai báo kiểu của một biến, sử dụng ``<variable>: <type>``:

::

    var health: int = 0

Để khai báo kiểu trả về của một function, sử dụng ``-> <type>``:

::

    func heal(amount: int) -> void:

Kiểu suy luận
~~~~~~~~~~~~~

Trong hầu hết trường hợp, bạn có thể để compiler suy luận kiểu bằng ``:=``. Ưu tiên ``:=`` khi kiểu được viết trên cùng dòng với phép gán; nếu không, hãy ưu tiên viết kiểu một cách tường minh.

**Tốt**:

.. rst-class:: code-example-good

::

    # Kiểu có thể là int hoặc float, vì vậy nên được nêu tường minh.
    var health: int = 0

    # Kiểu được suy luận rõ ràng là Vector3.
    var direction := Vector3(1, 2, 3)

Hãy thêm type hint khi kiểu không rõ ràng và bỏ type hint khi nó dư thừa.

**Không tốt**:

.. rst-class:: code-example-bad

::

    # Được định kiểu là int, nhưng có thể kiểu float mới là kiểu được dự định.
    var health := 0

    # Type hint chứa thông tin dư thừa.
    var direction: Vector3 = Vector3(1, 2, 3)

    # Đây là kiểu gì? Người đọc không thể hiểu ngay, vì vậy cách viết này không tốt.
    var value := complex_function()

Trong một số trường hợp, kiểu phải được nêu tường minh; nếu không, hành vi sẽ không như mong đợi vì compiler chỉ có thể sử dụng kiểu trả về của function. Ví dụ, ``get_node()`` không thể suy luận kiểu trừ khi scene hoặc file của node được nạp vào memory. Trong trường hợp này, bạn nên đặt kiểu một cách tường minh.

**Tốt**:

.. rst-class:: code-example-good

::

    @onready var health_bar: ProgressBar = get_node("UI/LifeBar")

**Không tốt**:

.. rst-class:: code-example-bad

::

    # Compiler không thể suy luận kiểu chính xác và sẽ sử dụng Node
    # thay vì ProgressBar.
    @onready var health_bar := get_node("UI/LifeBar")

Ngoài ra, bạn có thể sử dụng keyword ``as`` để cast kiểu trả về; kiểu đó sẽ được dùng để suy luận kiểu của var.

.. rst-class:: code-example-good

::

    @onready var health_bar := get_node("UI/LifeBar") as ProgressBar
    # health_bar sẽ được định kiểu là ProgressBar


.. note::

    Tùy chọn này được xem là :ref:`type-safe<doc_gdscript_static_typing_safe_lines>` hơn type hint, nhưng cũng kém an toàn với null hơn vì nó âm thầm cast biến thành ``null`` trong trường hợp không khớp kiểu tại runtime, mà không có lỗi/cảnh báo.
