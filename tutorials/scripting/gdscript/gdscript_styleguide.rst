.. _doc_gdscript_styleguide:

Hướng dẫn về phong cách GDScript
================================

Hướng dẫn về phong cách này liệt kê các quy ước để viết GDScript thanh lịch. Mục tiêu là khuyến khích viết mã sạch, dễ đọc và thúc đẩy tính nhất quán giữa các dự án, cuộc thảo luận và hướng dẫn. Hy vọng rằng tài liệu này cũng sẽ hỗ trợ phát triển các công cụ tự động định dạng.

Vì GDScript khá gần với Python, hướng dẫn này lấy cảm hứng từ `PEP 8 <https://www.python.org/dev/peps/pep-0008/>`__, hướng dẫn về phong cách lập trình của Python.

Hướng dẫn về phong cách không nhằm trở thành những bộ quy tắc cứng nhắc. Đôi khi bạn không thể áp dụng một số hướng dẫn dưới đây. Khi đó, hãy tự 판단 bằng phán đoán tốt nhất của mình và hỏi các nhà phát triển khác để có thêm góc nhìn.

Nhìn chung, việc giữ cho mã nhất quán trong các dự án và trong nhóm của bạn quan trọng hơn việc tuân thủ tuyệt đối hướng dẫn này.

.. note::

    Trình soạn thảo script tích hợp sẵn của Godot mặc định đã sử dụng nhiều quy ước trong số này. Hãy để trình soạn thảo hỗ trợ bạn.

Dưới đây là một ví dụ lớp hoàn chỉnh dựa trên các hướng dẫn này:

.. code-block::

    class_name StateMachine
    extends Node
    ## Máy trạng thái phân cấp cho người chơi.
    ##
    ## Khởi tạo các trạng thái và chuyển các callback của engine ([method Node._physics_process],
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

* Sử dụng các ký tự xuống dòng (**LF**) để ngắt dòng, không dùng CRLF hoặc CR. *(mặc định của trình soạn thảo)*
* Sử dụng một ký tự xuống dòng ở cuối mỗi tệp. *(mặc định của trình soạn thảo)*
* Sử dụng mã hóa **UTF-8** không có `dấu thứ tự byte <https://en.wikipedia.org/wiki/Byte_order_mark>`_. *(mặc định của trình soạn thảo)*
* Sử dụng **Tab** thay vì dấu cách để thụt lề. *(mặc định của trình soạn thảo)*

Thụt lề
~~~~~~~

Mỗi cấp thụt lề phải lớn hơn một cấp so với khối chứa nó.

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

Sử dụng 2 cấp thụt lề để phân biệt các dòng tiếp nối với các khối mã thông thường.

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

Các ngoại lệ của quy tắc này là array, dictionary và enum. Sử dụng một cấp thụt lề để phân biệt các dòng tiếp nối:

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

Dấu phẩy cuối
~~~~~~~~~~~~~

Sử dụng dấu phẩy cuối ở dòng cuối cùng trong array, dictionary và enum. Điều này giúp việc tái cấu trúc dễ dàng hơn và tạo ra các diff tốt hơn trong hệ thống quản lý phiên bản, vì không cần sửa dòng cuối khi thêm phần tử mới.

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

Dấu phẩy cuối không cần thiết trong các danh sách một dòng, vì vậy không thêm chúng trong trường hợp này.

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

    Trong tài liệu tham chiếu lớp và các đoạn mã ngắn trong tài liệu này, chúng tôi sử dụng một dòng trống giữa các lớp và định nghĩa hàm.

Độ dài dòng
~~~~~~~~~~~

Giữ mỗi dòng mã dưới 100 ký tự.

Nếu có thể, hãy cố gắng giữ các dòng dưới 80 ký tự. Điều này giúp đọc mã trên màn hình nhỏ và khi mở hai script cạnh nhau trong trình soạn thảo văn bản bên ngoài. Ví dụ, khi xem một bản sửa đổi dạng diff.

Mỗi dòng một câu lệnh
~~~~~~~~~~~~~~~~~~~~~

Tránh gộp nhiều câu lệnh trên cùng một dòng, bao gồm cả câu lệnh điều kiện, để tuân thủ hướng dẫn về phong cách GDScript nhằm tăng khả năng đọc.

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

Khi có các ``if`` câu lệnh đặc biệt dài hoặc các biểu thức ternary lồng nhau, việc ngắt chúng thành nhiều dòng sẽ giúp dễ đọc hơn. Vì các dòng tiếp nối vẫn là một phần của cùng biểu thức, nên sử dụng 2 cấp thụt lề thay vì một cấp.

GDScript cho phép ngắt câu lệnh thành nhiều dòng bằng dấu ngoặc đơn hoặc dấu gạch chéo ngược. Hướng dẫn về phong cách này ưu tiên dấu ngoặc đơn vì chúng giúp tái cấu trúc dễ dàng hơn. Khi dùng dấu gạch chéo ngược, bạn phải đảm bảo dòng cuối cùng không bao giờ chứa dấu gạch chéo ngược ở cuối. Với dấu ngoặc đơn, bạn không cần lo dòng cuối có dấu gạch chéo ngược ở cuối.

Khi ngắt một biểu thức điều kiện thành nhiều dòng, các từ khóa ``and``/``or`` phải được đặt ở đầu dòng tiếp nối, không đặt ở cuối dòng trước đó.

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

Tránh dùng dấu ngoặc đơn không cần thiết
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tránh dùng dấu ngoặc đơn trong các biểu thức và câu lệnh điều kiện. Trừ khi cần thiết để xác định thứ tự thực hiện phép toán hoặc ngắt thành nhiều dòng, chúng chỉ làm giảm khả năng đọc.

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

Ưu tiên các phiên bản bằng tiếng Anh thông thường của toán tử boolean vì chúng dễ tiếp cận nhất:

- Sử dụng ``and`` thay vì ``&&``.
- Sử dụng ``or`` thay vì ``||``.
- Sử dụng ``not`` thay vì ``!``.

Bạn cũng có thể sử dụng dấu ngoặc đơn quanh các toán tử boolean để loại bỏ mọi sự mơ hồ. Điều này có thể giúp các biểu thức dài dễ đọc hơn.

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

Các comment thông thường (``#``) và comment tài liệu (``##``) nên bắt đầu bằng một khoảng trắng, nhưng code được comment out thì không. Ngoài ra, comment vùng code (``#region``/``#endregion``) phải tuân theo chính xác cú pháp đó, vì vậy chúng không nên bắt đầu bằng khoảng trắng.

Sử dụng khoảng trắng cho comment thông thường và comment tài liệu giúp phân biệt comment dạng văn bản với code bị vô hiệu hóa.

**Tốt**:

.. rst-class:: code-example-good

.. code-block::

    # Đây là một comment.
    #print("This is disabled code")

**Không tốt**:

.. rst-class:: code-example-bad

.. code-block::

    #Đây là một comment.
    # print("This is disabled code")

.. note::

    Trong script editor, để bật hoặc tắt comment cho code đã chọn, hãy nhấn
    :kbd:`Ctrl + K`. Phím tắt này thêm hoặc xóa một dấu ``#`` duy nhất trước mọi đoạn code trên các dòng đã chọn.

Ưu tiên viết comment trên dòng riêng thay vì comment nội tuyến (comment được viết trên cùng dòng với code). Comment nội tuyến phù hợp nhất với các comment ngắn, thường chỉ vài từ:

**Tốt**:

.. rst-class:: code-example-good

.. code-block::

    # Đây là một comment dài, nếu viết nội tuyến thì sẽ khiến dòng bên dưới quá dài.
    print("Example") # Comment ngắn.

**Không tốt**:

.. rst-class:: code-example-bad

.. code-block::

    print("Example") # Đây là một comment dài, nếu viết nội tuyến thì sẽ khiến dòng này quá dài.

Khoảng trắng
~~~~~~~~~~~~

Luôn sử dụng một khoảng trắng xung quanh các toán tử và sau dấu phẩy. Ngoài ra, tránh thêm khoảng trắng trong các tham chiếu đến dictionary và các lời gọi hàm. Một ngoại lệ là khai báo dictionary trên một dòng, trong đó nên thêm một khoảng trắng sau dấu ngoặc nhọn mở và trước dấu ngoặc nhọn đóng. Điều này giúp phân biệt dictionary với array bằng mắt dễ hơn, vì các ký tự ``[]`` trông gần giống ``{}`` trong hầu hết các font.

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

Không sử dụng khoảng trắng để căn chỉnh các biểu thức theo chiều dọc:

::

    x        = 100
    y        = 100
    velocity = 500

Dấu ngoặc kép
~~~~~~~~~~~~~

Sử dụng dấu ngoặc kép trừ khi dấu ngoặc đơn giúp giảm số ký tự cần escape trong một chuỗi cụ thể. Xem các ví dụ bên dưới:

.. code-block::

    # Chuỗi thông thường.
    print("hello world")

    # Sử dụng dấu ngoặc kép như thường lệ để tránh escape.
    print("hello 'world'")

    # Sử dụng dấu ngoặc đơn như một ngoại lệ của quy tắc để tránh escape.
    print('hello "world"')

    # Cả hai kiểu dấu ngoặc đều cần 2 lần escape; nếu số lần bằng nhau, hãy ưu tiên dấu ngoặc kép.
    print("'hello' \"world\"")

Số
~~

Không được bỏ qua số 0 ở đầu hoặc cuối trong các số dấu phẩy động. Nếu không, chúng sẽ khó đọc hơn và khó phân biệt với số nguyên khi nhìn thoáng qua.

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

Sử dụng chữ thường cho các chữ cái trong số hexadecimal, vì chiều cao thấp hơn của chúng giúp số dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    var hex_number = 0xfb8c0b

**Không tốt**:

.. rst-class:: code-example-bad

::

    var hex_number = 0xFB8C0B

Tận dụng dấu gạch dưới của GDScript trong các literal để giúp các số lớn dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

.. code-block::

    var large_number = 1_234_567_890
    var large_hex_number = 0xffff_f8f8_0000
    var large_bin_number = 0b1101_0010_1010
    # Các số nhỏ hơn 1000000 thường không cần dấu phân cách.
    var small_number = 12345

**Không tốt**:

.. rst-class:: code-example-bad

.. code-block::

    var large_number = 1234567890
    var large_hex_number = 0xfffff8f80000
    var large_bin_number = 0b110100101010
    # Các số nhỏ hơn 1000000 thường không cần dấu phân cách.
    var small_number = 12_345

.. _naming_conventions:

Quy ước đặt tên
---------------

Các quy ước đặt tên này tuân theo phong cách của Godot Engine. Việc không tuân thủ sẽ khiến code của bạn xung đột với các quy ước đặt tên tích hợp sẵn, dẫn đến code không nhất quán. Bảng tóm tắt:

+---------------------+---------------+-------------------------------+
| Loại                | Quy ước       | Ví dụ                         |
+=====================+===============+===============================+
| Tên file            | snake_case    | ``yaml_parser.gd``            |
+---------------------+---------------+-------------------------------+
| Tên class           | PascalCase    | ``class_name YAMLParser``     |
+---------------------+---------------+-------------------------------+
| Tên node            | PascalCase    | ``Camera3D``, ``Player``      |
+---------------------+---------------+-------------------------------+
| Hàm                 | snake_case    | ``func load_level():``        |
+---------------------+---------------+-------------------------------+
| Biến                | snake_case    | ``var particle_effect``       |
+---------------------+---------------+-------------------------------+
| Signal              | snake_case    | ``signal door_opened``        |
+---------------------+---------------+-------------------------------+
| Hằng số             | CONSTANT_CASE | ``const MAX_SPEED = 200``     |
+---------------------+---------------+-------------------------------+
| Tên enum            | PascalCase    | ``enum Element``              |
+---------------------+---------------+-------------------------------+
| Các thành phần enum | CONSTANT_CASE | ``{EARTH, WATER, AIR, FIRE}`` |
+---------------------+---------------+-------------------------------+

Tên tệp
~~~~~~~

Sử dụng snake_case cho tên tệp. Đối với các class được đặt tên, chuyển tên class PascalCase sang snake_case:

.. code-block::

    # Tệp này phải được lưu dưới dạng `weapon.gd`.
    class_name Weapon
    extends Node

.. code-block::

    # Tệp này phải được lưu dưới dạng `yaml_parser.gd`.
    class_name YAMLParser
    extends Object

Điều này nhất quán với cách đặt tên tệp C++ trong mã nguồn của Godot. Cách này cũng tránh các vấn đề về phân biệt chữ hoa chữ thường có thể phát sinh khi xuất một project từ Windows sang các nền tảng khác.

Class và node
~~~~~~~~~~~~~

Sử dụng PascalCase cho tên class và node:

::

    extends CharacterBody3D

Cũng sử dụng PascalCase khi tải một class vào một hằng số hoặc biến:

::

    const Weapon = preload("res://weapon.gd")

Hàm và biến
~~~~~~~~~~~

Sử dụng snake\_case để đặt tên cho hàm và biến:

::

    var particle_effect
    func load_level():

Thêm một dấu gạch dưới đơn (\_) vào trước các phương thức/hàm ảo mà người dùng phải override, các hàm private và các biến private:

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

Sử dụng PascalCase cho *tên enum* và giữ chúng ở dạng số ít vì chúng đại diện cho một kiểu. Sử dụng CONSTANT\_CASE cho các thành phần của chúng vì đó là các hằng số:

::

    enum Element {
        EARTH,
        WATER,
        AIR,
        FIRE,
    }

Viết enum với mỗi mục trên một dòng riêng. Điều này giúp dễ dàng thêm các comment tài liệu phía trên từng mục hơn, đồng thời tạo ra các diff rõ ràng hơn trong hệ thống quản lý phiên bản khi thêm hoặc xóa mục.

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

Thứ tự mã
---------

Phần này tập trung vào thứ tự mã. Để xem cách định dạng, hãy xem
:ref:`formatting`. Để xem quy ước đặt tên, hãy xem :ref:`naming_conventions`.

Chúng tôi đề xuất tổ chức mã GDScript như sau:

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

Và đặt các phương thức cùng biến của class theo thứ tự sau, tùy thuộc vào các access modifier của chúng:

::

    1. public
    2. private

Chúng tôi tối ưu thứ tự này để dễ đọc mã từ trên xuống dưới, giúp các developer đọc mã lần đầu hiểu cách mã hoạt động và tránh các lỗi liên quan đến thứ tự khai báo biến.

Thứ tự mã này tuân theo bốn nguyên tắc chung:

1. Các property và signal được đặt trước, sau đó là các phương thức.
2. Public được đặt trước private.
3. Các callback ảo được đặt trước interface của class.
4. Các hàm khởi tạo và initialization của object, ``_init`` và ``_ready``, được đặt trước các hàm sửa đổi object trong runtime.

Khai báo class
~~~~~~~~~~~~~~

Nếu mã được dùng để chạy trong editor, đặt annotation ``@tool`` trên dòng đầu tiên của script.

Tiếp theo là ``@icon`` tùy chọn, rồi đến ``class_name`` nếu cần. Bạn có thể biến một tệp GDScript thành một global type trong project bằng ``class_name``. Để biết thêm thông tin, hãy xem :ref:`doc_gdscript_basics_class_name`. Nếu class được dùng làm một class :ref:`abstract class <doc_gdscript_basics_abstract_class>`, thêm ``@abstract`` *before* từ khóa ``class_name``.

Sau đó, thêm từ khóa ``extends`` nếu class kế thừa một kiểu dựng sẵn.

Tiếp theo, bạn nên có phần tùy chọn của class
:ref:`comment tài liệu <doc_gdscript_documentation_comments>`. Bạn có thể dùng phần này để giải thích cho đồng đội về vai trò và cách hoạt động của class, cũng như cách các developer khác nên sử dụng nó, chẳng hạn như:

.. code-block::

    @abstract
    class_name MyNode
    extends Node
    ## Mô tả ngắn gọn về vai trò và chức năng của class.
    ##
    ## Mô tả về script, những gì script có thể thực hiện,
    ## và mọi chi tiết bổ sung.

Đối với các class bên trong, sử dụng khai báo một dòng:

.. code-block::

    ## Mô tả ngắn gọn về vai trò và chức năng của class.
    ##
    ## Mô tả về script, những gì script có thể thực hiện,
    ## và mọi chi tiết bổ sung.
    @abstract class MyNode extends Node:
        pass

Signal và property
~~~~~~~~~~~~~~~~~~

Viết các khai báo signal, tiếp theo là các property, tức là các biến thành viên, sau docstring.

Enum nên được đặt sau signal vì bạn có thể sử dụng chúng làm export hint cho các property khác.

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

    GDScript đánh giá các biến ``@onready`` ngay trước callback ``_ready``. Bạn có thể dùng điều này để cache các dependency của node, tức là lấy các node con trong scene mà class của bạn phụ thuộc vào. Đây chính là điều ví dụ ở trên minh họa.

Biến thành viên
~~~~~~~~~~~~~~~

Không khai báo biến thành viên nếu chúng chỉ được sử dụng cục bộ trong một phương thức, vì điều đó khiến mã khó theo dõi hơn. Thay vào đó, hãy khai báo chúng dưới dạng biến cục bộ trong phần thân phương thức.

Biến cục bộ
~~~~~~~~~~~

Khai báo biến cục bộ gần với lần sử dụng đầu tiên của chúng nhất có thể. Điều này giúp dễ theo dõi mã hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.

Phương thức và hàm static
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau các thuộc tính của class là các method.

Bắt đầu bằng method callback ``_init()``, mà engine sẽ gọi khi tạo object trong bộ nhớ. Tiếp theo là callback ``_ready()``, mà Godot gọi khi thêm một node vào scene tree.

Các function này nên được đặt trước vì chúng cho thấy cách object được khởi tạo.

Tiếp theo là các callback virtual tích hợp khác, như ``_unhandled_input()`` và ``_physics_process``. Chúng điều khiển vòng lặp chính của object và các tương tác với game engine.

Phần còn lại của interface của class, gồm các method public và private, được đặt sau đó theo thứ tự này.

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

GDScript hỗ trợ :ref:`optional static typing <doc_gdscript_static_typing>`.

Các type được khai báo
~~~~~~~~~~~~~~~~~~~~~~

Để khai báo type của một biến, hãy sử dụng ``<variable>: <type>``:

::

    var health: int = 0

Để khai báo return type của một function, hãy sử dụng ``-> <type>``:

::

    func heal(amount: int) -> void:

Các type được suy luận
~~~~~~~~~~~~~~~~~~~~~~

Trong hầu hết trường hợp, bạn có thể để compiler suy luận type bằng ``:=``. Ưu tiên ``:=`` khi type được viết trên cùng dòng với phép gán; nếu không, hãy ưu tiên viết type một cách tường minh.

**Tốt**:

.. rst-class:: code-example-good

.. code-block::

    # Type có thể là int hoặc float, vì vậy nên được nêu tường minh.
    var health: int = 0

    # Type được suy luận rõ ràng là Vector3.
    var direction := Vector3(1, 2, 3)

Hãy thêm type hint khi type không rõ ràng, và bỏ type hint khi nó dư thừa.

**Không tốt**:

.. rst-class:: code-example-bad

.. code-block::

    # Được định kiểu là int, nhưng có thể float mới là type được dự định.
    var health := 0

    # Type hint chứa thông tin dư thừa.
    var direction: Vector3 = Vector3(1, 2, 3)

    # Đây là type gì? Người đọc không thể hiểu ngay, vì vậy cách viết này không tốt.
    var value := complex_function()

Trong một số trường hợp, type phải được nêu tường minh; nếu không, hành vi sẽ không như mong đợi vì compiler chỉ có thể sử dụng return type của function. Ví dụ, ``get_node()`` không thể suy luận type trừ khi scene hoặc file của node được tải vào bộ nhớ. Trong trường hợp này, bạn nên đặt type một cách tường minh.

**Tốt**:

.. rst-class:: code-example-good

::

    @onready var health_bar: ProgressBar = get_node("UI/LifeBar")

**Không tốt**:

.. rst-class:: code-example-bad

.. code-block::

    # Compiler không thể suy luận type chính xác và sẽ sử dụng Node
    # thay vì ProgressBar.
    @onready var health_bar := get_node("UI/LifeBar")

Ngoài ra, bạn có thể sử dụng từ khóa ``as`` để cast return type, và type đó sẽ được dùng để suy luận type của var.

.. rst-class:: code-example-good

.. code-block::

    @onready var health_bar := get_node("UI/LifeBar") as ProgressBar
    # health_bar sẽ được định kiểu là ProgressBar


.. note::

    Tùy chọn này được xem là :ref:`type-safe <doc_gdscript_static_typing_safe_lines>` hơn type hint, nhưng cũng kém null-safe hơn vì nó âm thầm cast biến thành ``null`` trong trường hợp không khớp type tại runtime, mà không có lỗi/cảnh báo.

.. _`byte order mark`: https://en.wikipedia.org/wiki/Byte_order_mark
