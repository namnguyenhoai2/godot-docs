.. _doc_gdscript_static_typing:

Kiểu tĩnh trong GDScript
========================

Trong hướng dẫn này, bạn sẽ học:

- cách sử dụng kiểu tĩnh trong GDScript; - kiểu tĩnh có thể giúp bạn tránh lỗi; - kiểu tĩnh cải thiện trải nghiệm của bạn với editor.

Bạn hoàn toàn có thể tự quyết định sử dụng tính năng ngôn ngữ này ở đâu và như thế nào: bạn có thể chỉ sử dụng nó trong một số tệp GDScript quan trọng, sử dụng ở mọi nơi hoặc hoàn toàn không sử dụng.

Có thể sử dụng kiểu tĩnh cho biến, hằng số, hàm, tham số và kiểu trả về.

Tổng quan ngắn gọn về kiểu tĩnh
-------------------------------

Với kiểu tĩnh, GDScript có thể phát hiện nhiều lỗi hơn mà không cần chạy code. Ngoài ra, type hint cung cấp cho bạn và đồng đội nhiều thông tin hơn trong quá trình làm việc, vì kiểu của các đối số sẽ hiển thị khi bạn gọi một method. Kiểu tĩnh cải thiện tính năng tự động hoàn tất của editor và :ref:`documentation <doc_gdscript_documentation_comments>` cho các script của bạn.

Hãy tưởng tượng bạn đang lập trình một hệ thống inventory. Bạn viết code cho một class ``Item``, sau đó là một ``Inventory``. Để thêm các item vào inventory, những người làm việc với code của bạn luôn phải truyền một ``Item`` vào method ``Inventory.add()``. Với các kiểu, bạn có thể bắt buộc điều này:

::

    class_name Inventory


    func add(reference: Item, amount: int = 1):
        var item := find_item(reference)
        if not item:
            item = _instance_item_from_db(reference)
        item.amount += amount

Kiểu tĩnh cũng cung cấp các tùy chọn code completion tốt hơn. Bên dưới, bạn có thể thấy sự khác biệt giữa các tùy chọn completion kiểu dynamic và kiểu static.

Có thể bạn đã từng gặp trường hợp không có gợi ý autocomplete sau một dấu chấm:

.. figure:: img/typed_gdscript_code_completion_dynamic.webp
    :alt: Completion options for dynamic typed code.

Điều này là do code dynamic. Godot không thể biết kiểu giá trị bạn đang truyền vào hàm. Tuy nhiên, nếu bạn viết rõ kiểu, bạn sẽ nhận được tất cả method, property, constant, v.v. từ giá trị đó:

.. figure:: img/typed_gdscript_code_completion_typed.webp
    :alt: Completion options for static typed code.

.. tip::

    Nếu thích kiểu tĩnh, chúng tôi khuyên bạn nên bật thiết lập editor **Text Editor > Completion > Add Type Hints**. Ngoài ra, hãy cân nhắc bật `some warnings <Warning system_>`_, vốn bị tắt theo mặc định.

.. CẬP NHẬT: Tính năng đã được lên kế hoạch. Nếu JIT/AOT được triển khai, hãy cập nhật đoạn này.

Ngoài ra, GDScript có kiểu còn cải thiện hiệu năng bằng cách sử dụng các opcode được tối ưu hóa khi kiểu của toán hạng/đối số đã được biết tại thời điểm biên dịch. Trong tương lai dự kiến sẽ có thêm các tối ưu hóa GDScript, chẳng hạn như biên dịch JIT/AOT.

Nhìn chung, lập trình có kiểu mang lại cho bạn trải nghiệm có cấu trúc hơn. Nó giúp ngăn ngừa lỗi và cải thiện khả năng tự mô tả của các script. Điều này đặc biệt hữu ích khi bạn làm việc trong một nhóm hoặc trên một dự án dài hạn: các nghiên cứu đã chỉ ra rằng developer dành phần lớn thời gian để đọc code của người khác hoặc các script do chính họ viết trong quá khứ nhưng đã quên. Code càng rõ ràng và có cấu trúc thì càng dễ hiểu nhanh, giúp bạn tiến lên nhanh hơn.

Cách sử dụng kiểu tĩnh
----------------------

Để xác định kiểu của một biến, tham số hoặc hằng số, hãy viết dấu hai chấm sau tên, tiếp theo là kiểu của nó. Ví dụ: ``var health: int``. Điều này buộc kiểu của biến luôn giữ nguyên:

::

    var damage: float = 10.5
    const MOVE_SPEED: float = 50.0
    func sum(a: float = 0.0, b: float = 0.0) -> float:
        return a + b

Godot sẽ cố gắng suy luận kiểu nếu bạn viết dấu hai chấm nhưng bỏ qua kiểu:

::

    var damage := 10.5
    const MOVE_SPEED := 50.0
    func sum(a := 0.0, b := 0.0) -> float:
        return a + b

.. note::

    1. Không có sự khác biệt giữa ``=`` và ``:=`` đối với hằng số. 2. Bạn không cần viết type hint cho hằng số, vì Godot tự động thiết lập kiểu từ giá trị được gán. Tuy nhiên, bạn vẫn có thể làm vậy để ý định trong code rõ ràng hơn. Điều này cũng hữu ích cho các mảng có kiểu (chẳng hạn như ``const A: Array[int] = [1, 2, 3]``), vì mảng không có kiểu được sử dụng theo mặc định.

Những gì có thể làm type hint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dưới đây là danh sách đầy đủ những gì có thể được sử dụng làm type hint:

1. ``Variant``. Bất kỳ kiểu nào. Trong hầu hết trường hợp, điều này không khác nhiều so với khai báo không có kiểu, nhưng giúp code dễ đọc hơn. Khi là kiểu trả về, nó buộc hàm phải trả về một giá trị nào đó. 2. *(Chỉ dành cho kiểu trả về)* ``void``. Cho biết hàm không trả về bất kỳ giá trị nào. 3. :ref:`Built-in types <doc_gdscript_builtin_types>`. 4. Các class native (``Object``, ``Node``, ``Area2D``, ``Camera2D``, v.v.). 5. :ref:`Global classes <doc_gdscript_basics_class_name>`. 6. :ref:`Inner classes <doc_gdscript_basics_inner_classes>`. 7. Các enum global, native và custom có tên. Lưu ý rằng kiểu enum thực chất chỉ là một ``int``, không có gì đảm bảo giá trị đó thuộc tập các giá trị enum. 8. Các hằng số (bao gồm hằng số cục bộ) nếu chúng chứa một class hoặc enum được preload.

Bạn có thể sử dụng bất kỳ class nào, bao gồm cả class custom của mình, làm kiểu. Có hai cách sử dụng chúng trong script. Cách đầu tiên là preload script bạn muốn sử dụng làm kiểu vào một hằng số:

::

    const Rifle = preload("res://player/weapons/rifle.gd")
    var my_rifle: Rifle

Cách thứ hai là sử dụng keyword ``class_name`` khi tạo script. Với ví dụ trên, ``rifle.gd`` của bạn sẽ có dạng như sau:

::

    class_name Rifle
    extends Node2D

Nếu sử dụng ``class_name``, Godot sẽ đăng ký kiểu ``Rifle`` trên toàn cục trong editor, và bạn có thể sử dụng nó ở bất kỳ đâu mà không cần preload vào một hằng số:

::

    var my_rifle: Rifle

Xác định kiểu trả về của một hàm bằng mũi tên ``->``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu trả về của một hàm, hãy viết dấu gạch ngang và dấu ngoặc nhọn bên phải ``->`` sau khai báo của hàm, tiếp theo là kiểu trả về:

::

    func _process(delta: float) -> void:
        pass

Kiểu ``void`` có nghĩa là hàm không trả về gì cả. Bạn có thể sử dụng bất kỳ kiểu nào, giống như với biến:

::

    func hit(damage: float) -> bool:
        health_points -= damage
        return health_points <= 0

Bạn cũng có thể sử dụng class của riêng mình làm kiểu trả về:

::

    # Thêm một item vào inventory và trả về item đó.
    func add(reference: Item, amount: int) -> Item:
        var item: Item = find_item(reference)
        if not item:
            item = ItemDatabase.get_instance(reference)

        item.amount += amount
        return item

Covariance và contravariance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi kế thừa các method của class cơ sở, bạn nên tuân theo `Liskov substitution principle <https://en.wikipedia.org/wiki/Liskov_substitution_principle>`__.

**Covariance:** Khi kế thừa một method, bạn có thể chỉ định kiểu trả về cụ thể hơn (**subtype**) so với method của class cha.

**Contravariance:** Khi kế thừa một method, bạn có thể chỉ định kiểu tham số ít cụ thể hơn (**supertype**) so với method của class cha.

Ví dụ:

::

    class_name Parent


    func get_property(param: Label) -> Node:
        # ...

::

    class_name Child extends Parent


    # `Control` là supertype của `Label`.
    # `Node2D` là subtype của `Node`.
    func get_property(param: Control) -> Node2D:
        # ...

Xác định kiểu phần tử của một ``Array``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu của một ``Array``, hãy đặt tên kiểu bên trong ``[]``.

Kiểu của mảng áp dụng cho các biến vòng lặp ``for``, cũng như một số toán tử như ``[]``, ``[...] =`` (phép gán) và ``+``. Các method của mảng (chẳng hạn như ``push_back``) và các toán tử khác (chẳng hạn như ``==``) vẫn không có kiểu. Có thể sử dụng các kiểu built-in, class native và custom, cũng như enum làm kiểu phần tử. Không hỗ trợ kiểu mảng lồng nhau (chẳng hạn như ``Array[Array[int]]``).


::

    var scores: Array[int] = [10, 20, 30]
    var vehicles: Array[Node] = [$Car, $Plane]
    var items: Array[Item] = [Item.new()]
    var array_of_arrays: Array[Array] = [[], []]
    # var arrays: Array[Array[int]] -- không được phép

    for score in scores:
        # score có kiểu `int`

    # Các trường hợp sau sẽ gây lỗi:
    scores += vehicles
    var s: String = scores[0]
    scores[0] = "lots"

Kể từ Godot 4.2, bạn cũng có thể chỉ định kiểu cho biến vòng lặp trong vòng lặp ``for``. Ví dụ, bạn có thể viết:

::

    var names = ["John", "Marta", "Samantha", "Jimmy"]
    for name: String in names:
        pass

Mảng sẽ vẫn không có kiểu, nhưng biến ``name`` bên trong vòng lặp ``for`` sẽ luôn có kiểu ``String``.

Xác định kiểu phần tử của một ``Dictionary``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu của các key và value trong một ``Dictionary``, hãy đặt tên kiểu bên trong ``[]`` và phân tách kiểu key với kiểu value bằng dấu phẩy.

Kiểu value của dictionary áp dụng cho các biến vòng lặp ``for``, cũng như một số toán tử như ``[]`` và ``[...] =`` (phép gán). Các method của dictionary trả về value và các toán tử khác (chẳng hạn như ``==``) vẫn không có kiểu. Có thể sử dụng các kiểu built-in, class native và custom, cũng như enum làm kiểu phần tử. Không hỗ trợ các collection có kiểu lồng nhau (chẳng hạn như ``Dictionary[String, Dictionary[String, int]]``).


::

    var fruit_costs: Dictionary[String, int] = { "apple": 5, "orange": 10 }
    var vehicles: Dictionary[String, Node] = { "car": $Car, "plane": $Plane }
    var item_tiles: Dictionary[Vector2i, Item] = { Vector2i(0, 0): Item.new(), Vector2i(0, 1): Item.new() }
    var dictionary_of_dictionaries: Dictionary[String, Dictionary] = { { } }
    # var dicts: Dictionary[String, Dictionary[String, int]] -- không được phép

    for fruit in fruit_costs:
        # `fruit` có kiểu `String`

    # Các trường hợp sau sẽ gây lỗi:
    fruit_costs["pear"] += vehicles
    var s: String = fruit_costs["apple"]
    fruit_costs["orange"] = "lots"

Ép kiểu
~~~~~~~

Ép kiểu là một khái niệm quan trọng trong các ngôn ngữ có kiểu. Ép kiểu là việc chuyển đổi một giá trị từ kiểu này sang kiểu khác.

Hãy tưởng tượng có một ``Enemy`` trong game của bạn, ``extends Area2D``. Bạn muốn nó va chạm với ``Player``, một ``CharacterBody2D`` có gắn script tên là ``PlayerController``. Bạn sử dụng signal ``body_entered`` để phát hiện va chạm. Với code có kiểu, body bạn phát hiện sẽ là một ``PhysicsBody2D`` chung, chứ không phải ``PlayerController`` của bạn trong callback ``_on_body_entered``.

Bạn có thể kiểm tra xem ``PhysicsBody2D`` này có phải là ``Player`` của mình hay không bằng keyword ``as``, đồng thời sử dụng lại dấu hai chấm ``:`` để buộc biến sử dụng kiểu này. Điều này buộc biến giữ kiểu ``PlayerController``:

::

    func _on_body_entered(body: PhysicsBody2D) -> void:
        var player := body as PlayerController
        if not player:
            return

        player.damage()

Vì đang làm việc với một kiểu custom, nếu ``body`` không mở rộng ``PlayerController``, biến ``player`` sẽ được đặt thành ``null``. Chúng ta có thể dùng điều này để kiểm tra body có phải là player hay không. Nhờ phép ép kiểu đó, chúng ta cũng sẽ nhận được đầy đủ tính năng autocompletion cho biến player.

.. note::

    Keyword ``as`` âm thầm ép biến sang ``null`` trong trường hợp kiểu không khớp lúc runtime, mà không gây ra lỗi/cảnh báo. Mặc dù điều này có thể thuận tiện trong một số trường hợp, nó cũng có thể dẫn đến bug. Chỉ sử dụng keyword ``as`` nếu đây là hành vi bạn mong muốn. Một lựa chọn an toàn hơn là sử dụng keyword ``is``:

    ::

        if not (body is PlayerController):
            push_error("Bug: body is not PlayerController.")

        var player: PlayerController = body
        if not player:
            return

        player.damage()

    Bạn cũng có thể đơn giản hóa code bằng cách sử dụng toán tử ``is not``:

    ::

        if body is not PlayerController:
            push_error("Bug: body is not PlayerController")

    Ngoài ra, bạn có thể sử dụng câu lệnh ``assert()``:

    ::

        assert(body is PlayerController, "Bug: body is not PlayerController.")

        var player: PlayerController = body
        if not player:
            return

        player.damage()


.. note::

    Nếu bạn thử ép kiểu bằng một kiểu dựng sẵn và thao tác đó thất bại, Godot sẽ báo lỗi.

.. _doc_gdscript_static_typing_safe_lines:

Các dòng an toàn
^^^^^^^^^^^^^^^^

Bạn cũng có thể sử dụng ép kiểu để đảm bảo các dòng an toàn. Các dòng an toàn là một công cụ cho bạn biết khi nào những dòng mã không rõ ràng là type-safe. Vì bạn có thể kết hợp mã có kiểu và mã dynamic, đôi khi Godot không có đủ thông tin để biết một chỉ thị có gây ra lỗi trong runtime hay không.

Điều này xảy ra khi bạn lấy một node con. Hãy lấy một timer làm ví dụ: với mã dynamic, bạn có thể lấy node bằng ``$Timer``. GDScript hỗ trợ `duck-typing <https://stackoverflow.com/a/4205163/8125343>`__, vì vậy ngay cả khi timer của bạn có kiểu ``Timer``, nó cũng là một ``Node`` và một ``Object``, hai class mà nó kế thừa. Với GDScript dynamic, bạn cũng không cần quan tâm đến kiểu của node miễn là nó có các method bạn cần gọi.

Bạn có thể sử dụng ép kiểu để cho Godot biết kiểu bạn mong đợi khi lấy một node: ``($Timer as Timer)``, ``($Player as CharacterBody2D)``, v.v. Godot sẽ đảm bảo kiểu đó hoạt động, và nếu đúng như vậy, số dòng sẽ chuyển thành màu xanh lá ở bên trái của trình soạn thảo script.

.. figure:: img/typed_gdscript_safe_unsafe_line.webp
   :alt: Unsafe vs Safe Line

   Unsafe line (line 7) vs Safe Lines (line 6 and 8)

.. note::

    Các dòng an toàn không phải lúc nào cũng có nghĩa là mã tốt hơn hoặc đáng tin cậy hơn. Hãy xem ghi chú ở trên về từ khóa ``as``. Ví dụ:

    ::

        @onready var node_1 := $Node1 as Type1 # Dòng an toàn.
        @onready var node_2: Type2 = $Node2 # Dòng không an toàn.

    Mặc dù khai báo ``node_2`` được đánh dấu là một dòng không an toàn, nó đáng tin cậy hơn khai báo ``node_1``. Bởi vì nếu bạn thay đổi kiểu node trong scene và vô tình quên thay đổi nó trong script, lỗi sẽ được phát hiện ngay khi scene được tải. Không giống như ``node_1``, vốn sẽ được âm thầm ép kiểu thành ``null`` và lỗi sẽ được phát hiện sau đó.

.. note::

    Bạn có thể tắt các dòng an toàn hoặc thay đổi màu của chúng trong phần cài đặt của trình soạn thảo.

Có kiểu hay dynamic: hãy nhất quán với một phong cách
-----------------------------------------------------

GDScript có kiểu và GDScript dynamic có thể cùng tồn tại trong một project. Tuy nhiên, bạn nên nhất quán với một trong hai phong cách để duy trì tính nhất quán trong codebase và giúp ích cho các đồng nghiệp. Mọi người sẽ dễ dàng làm việc cùng nhau hơn nếu tuân theo cùng một bộ quy tắc, đồng thời việc đọc và hiểu mã của người khác cũng nhanh hơn.

Mã có kiểu cần viết nhiều hơn một chút, nhưng bạn nhận được những lợi ích đã thảo luận ở trên. Dưới đây là ví dụ về cùng một script rỗng ở phong cách dynamic:

::

    extends Node


    func _ready():
        pass


    func _process(delta):
        pass

Và với static typing:

::

    extends Node


    func _ready() -> void:
        pass


    func _process(delta: float) -> void:
        pass

Như bạn thấy, bạn cũng có thể sử dụng kiểu với các virtual method của engine. Signal callback, cũng như mọi method khác, cũng có thể sử dụng kiểu. Dưới đây là một signal ``body_entered`` theo phong cách dynamic:

::

    func _on_area_2d_body_entered(body):
        pass

Và cùng callback đó với type hint:

::

    func _on_area_2d_body_entered(body: PhysicsBody2D) -> void:
        pass

Hệ thống cảnh báo
-----------------

.. note::

    Tài liệu chi tiết về hệ thống cảnh báo của GDScript đã được chuyển đến
    :ref:`doc_gdscript_warning_system`.

Godot đưa ra cảnh báo về mã của bạn khi bạn viết. Engine xác định những phần mã có thể dẫn đến vấn đề trong runtime, nhưng cho phép bạn quyết định có muốn giữ nguyên mã đó hay không.

Chúng tôi có một số cảnh báo dành riêng cho người dùng GDScript có kiểu. Theo mặc định, các cảnh báo này bị tắt; bạn có thể bật chúng trong Project Settings (**Debug > GDScript**, hãy đảm bảo **Advanced Settings** đã được bật).

Bạn có thể bật cảnh báo ``UNTYPED_DECLARATION`` nếu muốn luôn sử dụng static type. Ngoài ra, bạn có thể bật cảnh báo ``INFERRED_DECLARATION`` nếu thích cú pháp dễ đọc và đáng tin cậy hơn nhưng dài dòng hơn.

Các cảnh báo ``UNSAFE_*`` khiến những thao tác không an toàn dễ nhận thấy hơn so với các dòng không an toàn. Hiện tại, các cảnh báo ``UNSAFE_*`` không bao quát tất cả trường hợp mà các dòng không an toàn bao quát.

Các thao tác không an toàn thường gặp và các cách tương ứng an toàn
-------------------------------------------------------------------

Các method ở global scope
~~~~~~~~~~~~~~~~~~~~~~~~~

Các method ở global scope sau đây không được static typing, nhưng có các cách tương ứng có kiểu. Những method này trả về các giá trị có kiểu tĩnh:

+------------------------------------------------------+-------------------------------------------------------------------------------------+
| Method                                               | Statically typed equivalents                                                        |
+======================================================+=====================================================================================+
| :ref:`abs()<class_@GlobalScope_method_abs>`          | | :ref:`absf() <class_@GlobalScope_method_absf>`,                                   |
|                                                      |   :ref:`absi() <class_@GlobalScope_method_absi>`                                    |
|                                                      | | :ref:`Vector2.abs() <class_Vector2_method_abs>`,                                  |
|                                                      |   :ref:`Vector2i.abs() <class_Vector2i_method_abs>`                                 |
|                                                      | | :ref:`Vector3.abs() <class_Vector3_method_abs>`,                                  |
|                                                      |   :ref:`Vector3i.abs() <class_Vector3i_method_abs>`                                 |
|                                                      | | :ref:`Vector4.abs() <class_Vector4_method_abs>`,                                  |
|                                                      |   :ref:`Vector4i.abs() <class_Vector4i_method_abs>`                                 |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`ceil() <class_@GlobalScope_method_ceil>`       | | :ref:`ceilf() <class_@GlobalScope_method_ceilf>`,                                 |
|                                                      |   :ref:`ceili() <class_@GlobalScope_method_ceili>`                                  |
|                                                      | | :ref:`Vector2.ceil() <class_Vector2_method_ceil>`                                 |
|                                                      | | :ref:`Vector3.ceil() <class_Vector3_method_ceil>`                                 |
|                                                      | | :ref:`Vector4.ceil() <class_Vector4_method_ceil>`                                 |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`clamp() <class_@GlobalScope_method_clamp>`     | | :ref:`clampf() <class_@GlobalScope_method_clampf>`,                               |
|                                                      |   :ref:`clampi() <class_@GlobalScope_method_clampi>`                                |
|                                                      | | :ref:`Vector2.clamp() <class_Vector2_method_clamp>`,                              |
|                                                      |   :ref:`Vector2i.clamp() <class_Vector2i_method_clamp>`                             |
|                                                      | | :ref:`Vector3.clamp() <class_Vector3_method_clamp>`,                              |
|                                                      |   :ref:`Vector3i.clamp() <class_Vector3i_method_clamp>`                             |
|                                                      | | :ref:`Vector4.clamp() <class_Vector4_method_clamp>`,                              |
|                                                      |   :ref:`Vector4i.clamp() <class_Vector4i_method_clamp>`                             |
|                                                      | | :ref:`Color.clamp() <class_Color_method_clamp>`                                   |
|                                                      | | (untyped ``clamp()`` does not work on Color)                                      |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`floor() <class_@GlobalScope_method_floor>`     | | :ref:`floorf() <class_@GlobalScope_method_floorf>`,                               |
|                                                      |   :ref:`floori() <class_@GlobalScope_method_floori>`                                |
|                                                      | | :ref:`Vector2.floor() <class_Vector2_method_floor>`                               |
|                                                      | | :ref:`Vector3.floor() <class_Vector3_method_floor>`                               |
|                                                      | | :ref:`Vector4.floor() <class_Vector4_method_floor>`                               |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`lerp() <class_@GlobalScope_method_lerp>`       | | :ref:`lerpf() <class_@GlobalScope_method_lerpf>`                                  |
|                                                      | | :ref:`Vector2.lerp() <class_Vector2_method_lerp>`                                 |
|                                                      | | :ref:`Vector3.lerp() <class_Vector3_method_lerp>`                                 |
|                                                      | | :ref:`Vector4.lerp() <class_Vector4_method_lerp>`                                 |
|                                                      | | :ref:`Color.lerp() <class_Color_method_lerp>`                                     |
|                                                      | | :ref:`Quaternion.slerp() <class_Quaternion_method_slerp>`                         |
|                                                      | | :ref:`Basis.slerp() <class_Basis_method_slerp>`                                   |
|                                                      | | :ref:`Transform2D.interpolate_with() <class_Transform2D_method_interpolate_with>` |
|                                                      | | :ref:`Transform3D.interpolate_with() <class_Transform3D_method_interpolate_with>` |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`round() <class_@GlobalScope_method_round>`     | | :ref:`roundf() <class_@GlobalScope_method_roundf>`,                               |
|                                                      |   :ref:`roundi() <class_@GlobalScope_method_roundi>`                                |
|                                                      | | :ref:`Vector2.round() <class_Vector2_method_round>`                               |
|                                                      | | :ref:`Vector3.round() <class_Vector3_method_round>`                               |
|                                                      | | :ref:`Vector4.round() <class_Vector4_method_round>`                               |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`sign() <class_@GlobalScope_method_sign>`       | | :ref:`signf() <class_@GlobalScope_method_signf>`                                  |
|                                                      | | :ref:`signi() <class_@GlobalScope_method_signi>`                                  |
|                                                      | | :ref:`Vector2.sign() <class_Vector2_method_sign>`,                                |
|                                                      |   :ref:`Vector2i.sign() <class_Vector2i_method_sign>`                               |
|                                                      | | :ref:`Vector3.sign() <class_Vector3_method_sign>`,                                |
|                                                      |   :ref:`Vector3i.sign() <class_Vector3i_method_sign>`                               |
|                                                      | | :ref:`Vector4.sign() <class_Vector4_method_sign>`,                                |
|                                                      |   :ref:`Vector4i.sign() <class_Vector4i_method_sign>`                               |
+------------------------------------------------------+-------------------------------------------------------------------------------------+
| :ref:`snapped() <class_@GlobalScope_method_snapped>` | | :ref:`snappedf() <class_@GlobalScope_method_snappedf>`                            |
|                                                      | | :ref:`snappedi() <class_@GlobalScope_method_snappedi>`                            |
|                                                      | | :ref:`Vector2.snapped() <class_Vector2_method_snapped>`,                          |
|                                                      |   :ref:`Vector2i.snapped() <class_Vector2i_method_snapped>`                         |
|                                                      | | :ref:`Vector3.snapped() <class_Vector3_method_snapped>`,                          |
|                                                      |   :ref:`Vector3i.snapped() <class_Vector3i_method_snapped>`                         |
|                                                      | | :ref:`Vector4.snapped() <class_Vector4_method_snapped>`,                          |
|                                                      |   :ref:`Vector4i.snapped() <class_Vector4i_method_snapped>`                         |
+------------------------------------------------------+-------------------------------------------------------------------------------------+

Khi sử dụng static typing, hãy dùng các method ở global scope có kiểu bất cứ khi nào có thể. Điều này đảm bảo bạn có các dòng an toàn và được hưởng lợi từ các chỉ thị có kiểu để có hiệu năng tốt hơn.

Cảnh báo ``UNSAFE_PROPERTY_ACCESS`` và ``UNSAFE_METHOD_ACCESS``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong ví dụ này, chúng ta muốn thiết lập một property và gọi một method trên một object có gắn script với ``class_name MyScript`` và ``extends Node2D``. Nếu có một tham chiếu đến object dưới dạng ``Node2D`` (chẳng hạn như object được hệ thống physics truyền cho), trước tiên chúng ta có thể kiểm tra xem property và method có tồn tại hay không, rồi thiết lập và gọi chúng nếu có:

::

    if "some_property" in node_2d:
        node_2d.some_property = 20  # Tạo ra cảnh báo UNSAFE_PROPERTY_ACCESS.

    if node_2d.has_method("some_function"):
        node_2d.some_function()  # Tạo ra cảnh báo UNSAFE_METHOD_ACCESS.

Tuy nhiên, mã này sẽ tạo ra các cảnh báo ``UNSAFE_PROPERTY_ACCESS`` và ``UNSAFE_METHOD_ACCESS`` vì property và method không tồn tại trong kiểu được tham chiếu — trong trường hợp này là một ``Node2D``. Để làm cho các thao tác này an toàn, trước tiên bạn có thể kiểm tra xem object có kiểu ``MyScript`` bằng từ khóa ``is`` hay không, sau đó khai báo một biến có kiểu ``MyScript``, trên biến đó bạn có thể thiết lập các property và gọi các method:

::

    if node_2d is MyScript:
        var my_script: MyScript = node_2d
        my_script.some_property = 20
        my_script.some_function()

Ngoài ra, bạn có thể khai báo một biến và sử dụng toán tử ``as`` để thử ép kiểu object. Sau đó, bạn cần kiểm tra xem việc ép kiểu có thành công hay không bằng cách xác nhận rằng biến đã được gán:

::

    var my_script := node_2d as MyScript
    if my_script != null:
        my_script.some_property = 20
        my_script.some_function()

Cảnh báo ``UNSAFE_CAST``
~~~~~~~~~~~~~~~~~~~~~~~~

Trong ví dụ này, chúng ta muốn label được kết nối với một object đi vào vùng va chạm hiển thị tên của vùng đó. Khi object đi vào vùng va chạm, hệ thống physics gửi một signal kèm theo một object ``Node2D``, và giải pháp đơn giản nhất (nhưng không được static typing) để thực hiện điều chúng ta muốn có thể là như sau:

::

    func _on_body_entered(body: Node2D) -> void:
        body.label.text = name  # Tạo ra cảnh báo UNSAFE_PROPERTY_ACCESS.

Đoạn mã này tạo ra cảnh báo ``UNSAFE_PROPERTY_ACCESS`` vì ``label`` không được định nghĩa trong ``Node2D``. Để giải quyết, trước tiên chúng ta có thể kiểm tra xem property ``label`` có tồn tại hay không và ép kiểu nó thành kiểu ``Label`` trước khi thiết lập property text của nó như sau:

::

    func _on_body_entered(body: Node2D) -> void:
        if "label" in body:
            (body.label as Label).text = name  # Tạo ra cảnh báo UNSAFE_CAST.

Tuy nhiên, điều này tạo ra cảnh báo ``UNSAFE_CAST`` vì ``body.label`` có kiểu ``Variant``. Để lấy property một cách an toàn với kiểu bạn muốn, bạn có thể sử dụng method ``Object.get()``, method này trả về object dưới dạng giá trị ``Variant`` hoặc trả về ``null`` nếu property không tồn tại. Sau đó, bạn có thể xác định property có chứa một object đúng kiểu hay không bằng từ khóa ``is``, và cuối cùng khai báo một biến có kiểu tĩnh với object đó:

::

    func _on_body_entered(body: Node2D) -> void:
        var label_variant: Variant = body.get("label")
        if label_variant is Label:
            var label: Label = label_variant
            label.text = name

Các trường hợp không thể chỉ định kiểu
--------------------------------------

.. UPDATE: Not supported. If nested types are supported, update this section.

Để kết thúc phần giới thiệu này, hãy đề cập đến những trường hợp bạn không thể sử dụng type hint. Điều này sẽ gây ra **lỗi cú pháp**.

1. Bạn không thể chỉ định kiểu của từng phần tử riêng lẻ trong một array hoặc dictionary:

::

        var enemies: Array = [$Goblin: Enemy, $Zombie: Enemy]
        var character: Dictionary = {
            name: String = "Richard",
            money: int = 1000,
            inventory: Inventory = $Inventory,
        }

2. Hiện tại nested type chưa được hỗ trợ:

::

        var teams: Array[Array[Character]] = []

Tóm tắt
-------

.. UPDATE: Planned feature. If more optimizations (possibly JIT/AOT?) are .. implemented, update this paragraph.

GDScript có kiểu là một công cụ mạnh mẽ. Nó giúp bạn viết mã có cấu trúc hơn, tránh các lỗi thường gặp và tạo ra những hệ thống có khả năng mở rộng, đáng tin cậy. Static type cải thiện hiệu năng của GDScript và nhiều tối ưu hóa hơn được lên kế hoạch cho tương lai.
