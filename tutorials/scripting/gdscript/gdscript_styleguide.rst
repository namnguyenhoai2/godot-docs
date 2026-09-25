.. _doc_gdscript_styleguide:

Hướng dẫn phong cách GDScript
=============================

Hướng dẫn phong cách này liệt kê các quy ước để viết GDScript thanh lịch. Mục tiêu là khuyến khích viết mã sạch, dễ đọc và thúc đẩy tính nhất quán giữa các dự án, cuộc thảo luận và hướng dẫn. Hy vọng rằng hướng dẫn này cũng hỗ trợ phát triển các công cụ tự động định dạng.

Vì GDScript gần giống Python, hướng dẫn này được lấy cảm hứng từ `PEP 8 <https://www.python.org/dev/peps/pep-0008/>`__, hướng dẫn phong cách lập trình của Python.

Hướng dẫn phong cách không phải là những bộ quy tắc cứng nhắc. Đôi khi bạn không thể áp dụng một số nguyên tắc dưới đây. Khi đó, hãy sử dụng phán đoán tốt nhất của mình và hỏi các nhà phát triển khác để có thêm góc nhìn.

Nhìn chung, việc giữ mã nhất quán trong các dự án và trong nhóm của bạn quan trọng hơn việc tuân thủ hoàn toàn hướng dẫn này.

.. note::

    Trình chỉnh sửa script tích hợp của Godot mặc định đã sử dụng nhiều quy ước trong số này. Hãy để nó hỗ trợ bạn.

Dưới đây là một ví dụ lớp hoàn chỉnh dựa trên các nguyên tắc này:

::

    class_name StateMachine
    extends Node
    ## Hierarchical State machine for the player.
    ##
    ## Initializes states and delegates engine callbacks ([method Node._physics_process],
    ## [method Node._unhandled_input]) to the state.

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

* Sử dụng ký tự xuống dòng (**LF**) để ngắt dòng, không dùng CRLF hoặc CR. *(mặc định của trình chỉnh sửa)*
* Sử dụng một ký tự xuống dòng ở cuối mỗi tệp. *(mặc định của trình chỉnh sửa)*
* Sử dụng mã hóa **UTF-8** mà không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`_. *(mặc định của trình chỉnh sửa)*
* Sử dụng **Tabs** thay vì dấu cách để thụt lề. *(mặc định của trình chỉnh sửa)*

Thụt lề
~~~~~~~

Mỗi cấp thụt lề phải lớn hơn một cấp so với khối chứa nó.

**Đúng**:

.. rst-class:: code-example-good

::

    for i in range(10):
        print("hello")

**Sai**:

.. rst-class:: code-example-bad

::

    for i in range(10):
      print("hello")

    for i in range(10):
            print("hello")

Sử dụng 2 cấp thụt lề để phân biệt các dòng tiếp nối với các khối mã thông thường.

**Đúng**:

.. rst-class:: code-example-good

::

    effect.interpolate_property(sprite, "transform/scale",
            sprite.get_scale(), Vector2(2.0, 2.0), 0.3,
            Tween.TRANS_QUAD, Tween.EASE_OUT)

**Sai**:

.. rst-class:: code-example-bad

::

    effect.interpolate_property(sprite, "transform/scale",
        sprite.get_scale(), Vector2(2.0, 2.0), 0.3,
        Tween.TRANS_QUAD, Tween.EASE_OUT)

Ngoại lệ của quy tắc này là các mảng, dictionary và enum. Sử dụng một cấp thụt lề để phân biệt các dòng tiếp nối:

**Đúng**:

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

**Sai**:

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

Sử dụng dấu phẩy ở cuối dòng cuối cùng trong các mảng, dictionary và enum. Điều này giúp việc tái cấu trúc dễ dàng hơn và tạo ra các diff tốt hơn trong hệ thống kiểm soát phiên bản, vì không cần sửa dòng cuối khi thêm phần tử mới.

**Đúng**:

.. rst-class:: code-example-good

::

    var array = [
        1,
        2,
        3,
    ]

**Sai**:

.. rst-class:: code-example-bad

::

    var array = [
        1,
        2,
        3
    ]

Dấu phẩy ở cuối là không cần thiết trong các danh sách một dòng, vì vậy không thêm chúng trong trường hợp này.

**Đúng**:

.. rst-class:: code-example-good

::

    var array = [1, 2, 3]

**Sai**:

.. rst-class:: code-example-bad

::

    var array = [1, 2, 3,]

Dòng trống
~~~~~~~~~~

Bao quanh các định nghĩa hàm và lớp bằng hai dòng trống:

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

    Chúng tôi sử dụng một dòng giữa các lớp và định nghĩa hàm trong tài liệu tham chiếu lớp cũng như trong các đoạn mã ngắn của tài liệu này.

Độ dài dòng
~~~~~~~~~~~

Giữ mỗi dòng mã dưới 100 ký tự.

Nếu có thể, hãy cố gắng giữ các dòng dưới 80 ký tự. Điều này giúp đọc mã trên màn hình nhỏ và khi mở hai script cạnh nhau trong trình soạn thảo văn bản bên ngoài. Ví dụ, khi xem một bản sửa đổi khác biệt.

Mỗi dòng một câu lệnh
~~~~~~~~~~~~~~~~~~~~~

Tránh kết hợp nhiều câu lệnh trên một dòng, bao gồm cả các câu lệnh điều kiện, để tuân thủ các nguyên tắc phong cách GDScript về khả năng đọc.

**Đúng**:

.. rst-class:: code-example-good

::

    if position.x > width:
        position.x = 0

    if flag:
        print("flagged")

**Sai**:

.. rst-class:: code-example-bad

::

    if position.x > width: position.x = 0

    if flag: print("flagged")

Ngoại lệ duy nhất của quy tắc này là toán tử ternary:

::

    next_state = "idle" if is_on_floor() else "fall"

Định dạng các câu lệnh nhiều dòng để dễ đọc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi bạn có các ``if`` câu lệnh đặc biệt dài hoặc các biểu thức ternary lồng nhau, việc ngắt chúng thành nhiều dòng sẽ giúp dễ đọc hơn. Vì các dòng tiếp nối vẫn là một phần của cùng biểu thức, nên sử dụng 2 cấp thụt lề thay vì một cấp.

GDScript cho phép ngắt câu lệnh thành nhiều dòng bằng dấu ngoặc đơn hoặc dấu gạch chéo ngược. Hướng dẫn phong cách này ưu tiên dấu ngoặc đơn vì chúng giúp việc tái cấu trúc dễ dàng hơn. Với dấu gạch chéo ngược, bạn phải đảm bảo dòng cuối cùng không bao giờ chứa dấu gạch chéo ngược ở cuối. Với dấu ngoặc đơn, bạn không cần lo dòng cuối có dấu gạch chéo ngược ở cuối.

Khi ngắt một biểu thức điều kiện thành nhiều dòng, các từ khóa ``and``/``or`` phải được đặt ở đầu phần tiếp nối của dòng, không đặt ở cuối dòng trước đó.

**Đúng**:

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

**Sai**:

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

**Đúng**:

.. rst-class:: code-example-good

::

    if is_colliding():
        queue_free()

**Sai**:

.. rst-class:: code-example-bad

::

    if (is_colliding()):
        queue_free()

.. _boolean_operators:

Toán tử Boolean
~~~~~~~~~~~~~~~

Ưu tiên các phiên bản bằng tiếng Anh tự nhiên của toán tử Boolean vì chúng dễ tiếp cận nhất:

- Sử dụng ``and`` thay vì ``&&``.
- Sử dụng ``or`` thay vì ``||``.
- Sử dụng ``not`` thay vì ``!``.

Bạn cũng có thể sử dụng dấu ngoặc đơn quanh các toán tử Boolean để loại bỏ mọi sự mơ hồ. Điều này có thể giúp các biểu thức dài dễ đọc hơn.

**Đúng**:

.. rst-class:: code-example-good

::

    if (foo and bar) or not baz:
        print("condition is true")

**Sai**:

.. rst-class:: code-example-bad

::

    if foo && bar || !baz:
        print("condition is true")

Khoảng cách trong chú thích
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các comment thông thường (``#``) và comment tài liệu (``##``) nên bắt đầu bằng một dấu cách, nhưng code được comment out thì không. Ngoài ra, comment vùng code (``#region``/``#endregion``) phải tuân theo chính xác cú pháp đó, vì vậy chúng không nên bắt đầu bằng dấu cách.

Việc sử dụng một dấu cách cho comment thông thường và comment tài liệu giúp phân biệt comment văn bản với code bị vô hiệu hóa.

**Tốt**:

.. rst-class:: code-example-good

::

    # This is a comment.
    #print("This is disabled code")

**Không tốt**:

.. rst-class:: code-example-bad

::

    #This is a comment.
    # print("This is disabled code")

.. note::

    Trong trình soạn thảo script, để bật hoặc tắt comment cho code đã chọn, hãy nhấn
    :kbd:`Ctrl + K`. Phím tắt này thêm hoặc xóa một dấu ``#`` duy nhất trước mọi đoạn code trên các dòng đã chọn.

Ưu tiên viết comment trên dòng riêng thay vì comment nội tuyến (comment được viết trên cùng dòng với code). Comment nội tuyến phù hợp nhất cho các comment ngắn, thường chỉ vài từ:

**Tốt**:

.. rst-class:: code-example-good

::

    # This is a long comment that would make the line below too long if written inline.
    print("Example") # Short comment.

**Không tốt**:

.. rst-class:: code-example-bad

::

    print("Example") # This is a long comment that would make this line too long if written inline.

Khoảng trắng
~~~~~~~~~~~~

Luôn sử dụng một dấu cách xung quanh các toán tử và sau dấu phẩy. Ngoài ra, tránh các dấu cách thừa trong các tham chiếu đến dictionary và các lệnh gọi hàm. Một ngoại lệ là khi khai báo dictionary trên một dòng, trong đó nên thêm một dấu cách sau dấu ngoặc nhọn mở và trước dấu ngoặc nhọn đóng. Điều này giúp phân biệt dictionary với array bằng mắt dễ dàng hơn, vì các ký tự ``[]`` trông gần giống ``{}`` trong hầu hết các font.

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

Không sử dụng dấu cách để căn chỉnh các biểu thức theo chiều dọc:

::

    x        = 100
    y        = 100
    velocity = 500

Dấu ngoặc kép
~~~~~~~~~~~~~

Sử dụng dấu ngoặc kép đôi, trừ khi dấu ngoặc kép đơn giúp bạn phải escape ít ký tự hơn trong một chuỗi cụ thể. Xem các ví dụ dưới đây:

::

    # Normal string.
    print("hello world")

    # Use double quotes as usual to avoid escapes.
    print("hello 'world'")

    # Use single quotes as an exception to the rule to avoid escapes.
    print('hello "world"')

    # Both quote styles would require 2 escapes; prefer double quotes if it's a tie.
    print("'hello' \"world\"")

Số
~~

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

Sử dụng chữ thường cho các chữ cái trong số thập lục phân, vì chiều cao thấp hơn của chúng giúp số dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    var hex_number = 0xfb8c0b

**Không tốt**:

.. rst-class:: code-example-bad

::

    var hex_number = 0xFB8C0B

Hãy tận dụng dấu gạch dưới trong literal của GDScript để giúp các số lớn dễ đọc hơn.

**Tốt**:

.. rst-class:: code-example-good

::

    var large_number = 1_234_567_890
    var large_hex_number = 0xffff_f8f8_0000
    var large_bin_number = 0b1101_0010_1010
    # Numbers lower than 1000000 generally don't need separators.
    var small_number = 12345

**Không tốt**:

.. rst-class:: code-example-bad

::

    var large_number = 1234567890
    var large_hex_number = 0xfffff8f80000
    var large_bin_number = 0b110100101010
    # Numbers lower than 1000000 generally don't need separators.
    var small_number = 12_345

.. _naming_conventions:

Quy ước đặt tên
---------------

Các quy ước đặt tên này tuân theo phong cách của Godot Engine. Việc vi phạm các quy ước này sẽ khiến code của bạn xung đột với các quy ước đặt tên tích hợp sẵn, dẫn đến code không nhất quán. Bảng tóm tắt:

+-----------------+---------------+-------------------------------+
| Loại            | Quy ước       | Ví dụ                         |
+=================+===============+===============================+
| Tên file        | snake_case    | ``yaml_parser.gd``            |
+-----------------+---------------+-------------------------------+
| Tên class       | PascalCase    | ``class_name YAMLParser``     |
+-----------------+---------------+-------------------------------+
| Tên node        | PascalCase    | ``Camera3D``, ``Player``      |
+-----------------+---------------+-------------------------------+
| Hàm             | snake_case    | ``func load_level():``        |
+-----------------+---------------+-------------------------------+
| Biến            | snake_case    | ``var particle_effect``       |
+-----------------+---------------+-------------------------------+
| Signal          | snake_case    | ``signal door_opened``        |
+-----------------+---------------+-------------------------------+
| Hằng số         | CONSTANT_CASE | ``const MAX_SPEED = 200``     |
+-----------------+---------------+-------------------------------+
| Tên enum        | PascalCase    | ``enum Element``              |
+-----------------+---------------+-------------------------------+
| Member của enum | CONSTANT_CASE | ``{EARTH, WATER, AIR, FIRE}`` |
+-----------------+---------------+-------------------------------+

Tên file
~~~~~~~~

Sử dụng snake_case cho tên file. Đối với các class có tên, hãy chuyển tên class PascalCase thành snake_case:

::

    # This file should be saved as `weapon.gd`.
    class_name Weapon
    extends Node

::

    # This file should be saved as `yaml_parser.gd`.
    class_name YAMLParser
    extends Object

Điều này nhất quán với cách đặt tên file C++ trong mã nguồn của Godot. Cách này cũng tránh các vấn đề phân biệt chữ hoa chữ thường có thể phát sinh khi export một project từ Windows sang các nền tảng khác.

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

Thêm một dấu gạch dưới đơn (\_) vào đầu các hàm phương thức virtual mà người dùng phải override, các hàm private và các biến private:

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

Viết hằng số bằng CONSTANT\_CASE, nghĩa là viết toàn bộ bằng chữ hoa và dùng dấu gạch dưới (\_) để phân tách các từ:

::

    const MAX_SPEED = 200

Sử dụng PascalCase cho *tên* enum và giữ chúng ở dạng số ít, vì chúng biểu diễn một kiểu. Sử dụng CONSTANT\_CASE cho các member của chúng, vì chúng là các hằng số:

::

    enum Element {
        EARTH,
        WATER,
        AIR,
        FIRE,
    }

Viết mỗi mục enum trên một dòng riêng. Điều này giúp dễ dàng thêm chú thích tài liệu phía trên từng mục hơn, đồng thời tạo ra các diff rõ ràng hơn trong hệ thống quản lý phiên bản khi thêm hoặc xóa mục.

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

Phần này tập trung vào thứ tự mã. Để biết về định dạng, hãy xem
:ref:`formatting`. Để biết về quy ước đặt tên, hãy xem :ref:`naming_conventions`.

Chúng tôi đề xuất tổ chức mã GDScript theo cách sau:

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

Và đặt các phương thức cùng biến của lớp theo thứ tự sau, tùy thuộc vào các access modifier của chúng:

::

    1. public
    2. private

Chúng tôi đã tối ưu hóa thứ tự này để dễ đọc mã từ trên xuống dưới, giúp các developer đọc mã lần đầu hiểu cách mã hoạt động, đồng thời tránh các lỗi liên quan đến thứ tự khai báo biến.

Thứ tự mã này tuân theo bốn nguyên tắc chung:

1. Properties và signals được đặt trước, tiếp theo là các phương thức.
2. Public được đặt trước private.
3. Các virtual callback được đặt trước interface của lớp.
4. Các hàm khởi tạo và initialization của object, ``_init`` và ``_ready``, được đặt trước các hàm sửa đổi object trong runtime.

Khai báo lớp
~~~~~~~~~~~~

Nếu mã được thiết kế để chạy trong editor, hãy đặt annotation ``@tool`` ở dòng đầu tiên của script.

Tiếp theo là ``@icon`` không bắt buộc, rồi đến ``class_name`` nếu cần. Bạn có thể biến tệp GDScript thành một global type trong project bằng ``class_name``. Để biết thêm thông tin, hãy xem :ref:`doc_gdscript_basics_class_name`. Nếu lớp được thiết kế là một :ref:`lớp abstract <doc_gdscript_basics_abstract_class>`, hãy thêm ``@abstract`` *trước* từ khóa ``class_name``.

Sau đó, thêm từ khóa ``extends`` nếu lớp mở rộng một built-in type.

Sau đó, bạn sẽ có phần tùy chọn của class
:ref:`documentation comments <doc_gdscript_documentation_comments>`. Chẳng hạn, bạn có thể dùng phần này để giải thích vai trò của lớp cho các đồng đội, cách lớp hoạt động và cách các developer khác nên sử dụng lớp.

::

    @abstract
    class_name MyNode
    extends Node
    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.

Đối với các lớp bên trong, hãy dùng khai báo một dòng:

::

    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.
    @abstract class MyNode extends Node:
        pass

Signals và properties
~~~~~~~~~~~~~~~~~~~~~

Sau docstring, hãy viết các khai báo signal, tiếp theo là properties, tức là các member variable.

Enum nên được đặt sau signal, vì bạn có thể dùng chúng làm export hint cho các property khác.

Sau đó, hãy viết constants, exported variables, public, private và onready variables theo thứ tự đó.

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

    GDScript đánh giá các biến ``@onready`` ngay trước callback ``_ready``. Bạn có thể dùng điều này để cache các node dependency, tức là lấy các node con trong scene mà lớp của bạn phụ thuộc vào. Đây là điều ví dụ trên minh họa.

Member variable
~~~~~~~~~~~~~~~

Đừng khai báo member variable nếu chúng chỉ được sử dụng cục bộ trong một phương thức, vì điều đó khiến mã khó theo dõi hơn. Thay vào đó, hãy khai báo chúng dưới dạng local variable trong phần thân của phương thức.

Local variable
~~~~~~~~~~~~~~

Khai báo local variable gần nhất có thể với lần sử dụng đầu tiên của chúng. Điều này giúp dễ theo dõi mã hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.

Phương thức và hàm static
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau properties của lớp là các phương thức.

Bắt đầu bằng phương thức callback ``_init()``, được engine gọi khi tạo object trong bộ nhớ. Tiếp theo là callback ``_ready()``, được Godot gọi khi thêm một node vào scene tree.

Các hàm này nên được đặt trước vì chúng cho thấy cách object được khởi tạo.

Các virtual callback dựng sẵn khác, như ``_unhandled_input()`` và ``_physics_process``, nên được đặt tiếp theo. Chúng điều khiển main loop của object và các tương tác với game engine.

Phần còn lại của interface của lớp, gồm các phương thức public và private, được đặt sau đó theo thứ tự này.

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

GDScript hỗ trợ :ref:`static typing tùy chọn <doc_gdscript_static_typing>`.

Các kiểu được khai báo
~~~~~~~~~~~~~~~~~~~~~~

Để khai báo kiểu của một biến, hãy dùng ``<variable>: <type>``:

::

    var health: int = 0

Để khai báo kiểu trả về của một hàm, hãy dùng ``-> <type>``:

::

    func heal(amount: int) -> void:

Các kiểu được suy luận
~~~~~~~~~~~~~~~~~~~~~~

Trong hầu hết trường hợp, bạn có thể để compiler suy luận kiểu bằng ``:=``. Ưu tiên ``:=`` khi kiểu được viết trên cùng dòng với phép gán; nếu không, hãy ưu tiên viết kiểu một cách rõ ràng.

**Tốt**:

.. rst-class:: code-example-good

::

    # The type can be int or float, and thus should be stated explicitly.
    var health: int = 0

    # The type is clearly inferred as Vector3.
    var direction := Vector3(1, 2, 3)

Hãy thêm type hint khi kiểu không rõ ràng, và bỏ qua type hint khi nó dư thừa.

**Không tốt**:

.. rst-class:: code-example-bad

::

    # Typed as int, but it could be that float was intended.
    var health := 0

    # The type hint has redundant information.
    var direction: Vector3 = Vector3(1, 2, 3)

    # What type is this? It's not immediately clear to the reader, so it's bad.
    var value := complex_function()

Trong một số trường hợp, kiểu phải được nêu rõ; nếu không, hành vi sẽ không như mong đợi vì compiler chỉ có thể sử dụng kiểu trả về của hàm. Ví dụ, ``get_node()`` không thể suy luận kiểu trừ khi scene hoặc tệp của node được tải vào bộ nhớ. Trong trường hợp này, bạn nên đặt kiểu một cách rõ ràng.

**Tốt**:

.. rst-class:: code-example-good

::

    @onready var health_bar: ProgressBar = get_node("UI/LifeBar")

**Không tốt**:

.. rst-class:: code-example-bad

::

    # The compiler can't infer the exact type and will use Node
    # instead of ProgressBar.
    @onready var health_bar := get_node("UI/LifeBar")

Ngoài ra, bạn có thể dùng từ khóa ``as`` để ép kiểu trả về, và kiểu đó sẽ được dùng để suy luận kiểu của var.

.. rst-class:: code-example-good

::

    @onready var health_bar := get_node("UI/LifeBar") as ProgressBar
    # health_bar will be typed as ProgressBar


.. note::

    Tùy chọn này được xem là :ref:`an toàn kiểu <doc_gdscript_static_typing_safe_lines>` hơn so với type hint, nhưng cũng kém an toàn null hơn vì nó âm thầm ép biến thành ``null`` trong trường hợp không khớp kiểu tại runtime mà không đưa ra lỗi/cảnh báo.

.. _`byte order mark`: https://en.wikipedia.org/wiki/Byte_order_mark
