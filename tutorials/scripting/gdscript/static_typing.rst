.. _doc_gdscript_static_typing:

Kiểu tĩnh trong GDScript
========================

Trong hướng dẫn này, bạn sẽ học:

- cách sử dụng kiểu tĩnh trong GDScript;
- kiểu tĩnh có thể giúp bạn tránh lỗi như thế nào;
- kiểu tĩnh cải thiện trải nghiệm của bạn với editor như thế nào.

Bạn hoàn toàn có thể tự quyết định sử dụng tính năng ngôn ngữ này ở đâu và như thế nào: bạn có thể chỉ sử dụng nó trong một số tệp GDScript nhạy cảm, sử dụng ở mọi nơi hoặc hoàn toàn không sử dụng.

Có thể sử dụng kiểu tĩnh cho biến, hằng số, hàm, tham số và kiểu trả về.

Tìm hiểu sơ lược về kiểu tĩnh
-----------------------------

Với kiểu tĩnh, GDScript có thể phát hiện nhiều lỗi hơn ngay cả khi chưa chạy mã. Ngoài ra, type hint cung cấp cho bạn và đồng đội nhiều thông tin hơn trong quá trình làm việc, vì kiểu của các đối số sẽ hiển thị khi bạn gọi một method. Kiểu tĩnh cải thiện tính năng tự động hoàn tất của editor và :ref:`tài liệu <doc_gdscript_documentation_comments>` cho các script của bạn.

Hãy tưởng tượng bạn đang lập trình một hệ thống inventory. Bạn viết mã cho một ``Item`` class, sau đó là một ``Inventory``. Để thêm các item vào inventory, những người làm việc với mã của bạn luôn phải truyền một ``Item`` vào method ``Inventory.add()``. Với kiểu dữ liệu, bạn có thể buộc điều này phải được tuân thủ:

::

    class_name Inventory


    func add(reference: Item, amount: int = 1):
        var item := find_item(reference)
        if not item:
            item = _instance_item_from_db(reference)
        item.amount += amount

Kiểu tĩnh cũng cung cấp cho bạn các tùy chọn code completion tốt hơn. Bên dưới, bạn có thể thấy sự khác biệt giữa các tùy chọn hoàn tất cho kiểu động và kiểu tĩnh.

Có lẽ bạn đã từng gặp trường hợp không có gợi ý autocomplete sau dấu chấm:

.. figure:: img/typed_gdscript_code_completion_dynamic.webp
    :alt: Các tùy chọn hoàn tất cho mã có kiểu động.

Điều này xảy ra do mã động. Godot không thể biết bạn đang truyền kiểu giá trị nào vào hàm. Tuy nhiên, nếu bạn viết rõ kiểu, bạn sẽ nhận được tất cả method, property, constant, v.v. của giá trị đó:

.. figure:: img/typed_gdscript_code_completion_typed.webp
    :alt: Các tùy chọn hoàn tất cho mã có kiểu tĩnh.

.. tip::

    Nếu thích kiểu tĩnh, chúng tôi khuyên bạn bật thiết lập editor **Text Editor > Completion > Add Type Hints**. Ngoài ra, hãy cân nhắc bật `một số cảnh báo <Warning system_>`_ vốn bị tắt theo mặc định.

.. UPDATE: Planned feature. If JIT/AOT are implemented, update this paragraph.

Ngoài ra, GDScript có kiểu còn cải thiện hiệu năng bằng cách sử dụng opcode được tối ưu khi kiểu của toán hạng/đối số đã được biết tại thời điểm biên dịch. Trong tương lai, nhiều tối ưu hóa GDScript hơn sẽ được lên kế hoạch, chẳng hạn như biên dịch JIT/AOT.

Nhìn chung, lập trình có kiểu mang đến cho bạn trải nghiệm có cấu trúc hơn. Nó giúp ngăn ngừa lỗi và cải thiện tính tự mô tả của các script. Điều này đặc biệt hữu ích khi bạn làm việc trong một nhóm hoặc một dự án dài hạn: các nghiên cứu đã chỉ ra rằng lập trình viên dành phần lớn thời gian để đọc mã của người khác hoặc các script họ đã viết từ trước rồi quên mất. Mã càng rõ ràng và có cấu trúc thì càng dễ hiểu nhanh, nhờ đó bạn càng có thể tiến hành công việc nhanh hơn.

Cách sử dụng kiểu tĩnh
----------------------

Để xác định kiểu của một biến, tham số hoặc hằng số, hãy viết dấu hai chấm sau tên, rồi đến kiểu của nó. Ví dụ: ``var health: int``. Điều này buộc kiểu của biến luôn giữ nguyên:

::

    var damage: float = 10.5
    const MOVE_SPEED: float = 50.0
    func sum(a: float = 0.0, b: float = 0.0) -> float:
        return a + b

Godot sẽ cố gắng suy luận kiểu khi bạn viết dấu hai chấm nhưng bỏ qua kiểu:

::

    var damage := 10.5
    const MOVE_SPEED := 50.0
    func sum(a := 0.0, b := 0.0) -> float:
        return a + b

.. note::

    1. Không có sự khác biệt giữa ``=`` và ``:=`` đối với hằng số.
    2. Bạn không cần viết type hint cho hằng số vì Godot tự động thiết lập kiểu từ giá trị được gán. Tuy nhiên, bạn vẫn có thể làm vậy để ý định trong mã rõ ràng hơn. Điều này cũng hữu ích cho các mảng có kiểu (chẳng hạn như ``const A: Array[int] = [1, 2, 3]``), vì theo mặc định các mảng không có kiểu được sử dụng.

Những gì có thể dùng làm type hint
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dưới đây là danh sách đầy đủ những gì có thể được dùng làm type hint:

1. ``Variant``. Bất kỳ kiểu nào. Trong hầu hết trường hợp, điều này không khác nhiều so với khai báo không có kiểu, nhưng giúp mã dễ đọc hơn. Khi là kiểu trả về, nó buộc hàm phải trả về rõ ràng một giá trị nào đó.
2. *(Chỉ dành cho kiểu trả về)* ``void``. Cho biết hàm không trả về bất kỳ giá trị nào.
3. :ref:`Các kiểu dựng sẵn <doc_gdscript_builtin_types>`.
4. Các class native (``Object``, ``Node``, ``Area2D``, ``Camera2D``, v.v.).
5. :ref:`Các class toàn cục <doc_gdscript_basics_class_name>`.
6. :ref:`Các class bên trong <doc_gdscript_basics_inner_classes>`.
7. Các enum toàn cục, native và tùy chỉnh có tên. Lưu ý rằng kiểu enum thực chất chỉ là một ``int``, không có gì đảm bảo giá trị đó thuộc tập hợp các giá trị enum.
8. Các hằng số (bao gồm cả hằng số cục bộ) nếu chúng chứa một class hoặc enum được tải trước.

Bạn có thể sử dụng bất kỳ class nào, bao gồm cả các class tùy chỉnh của mình, làm kiểu. Có hai cách để sử dụng chúng trong script. Cách đầu tiên là tải trước script bạn muốn dùng làm kiểu vào một hằng số:

::

    const Rifle = preload("res://player/weapons/rifle.gd")
    var my_rifle: Rifle

Cách thứ hai là sử dụng từ khóa ``class_name`` khi tạo script. Với ví dụ trên, ``rifle.gd`` của bạn sẽ trông như sau:

::

    class_name Rifle
    extends Node2D

Nếu sử dụng ``class_name``, Godot sẽ đăng ký kiểu ``Rifle`` trên toàn cục trong editor, và bạn có thể sử dụng nó ở bất kỳ đâu mà không cần tải trước vào một hằng số:

::

    var my_rifle: Rifle

Xác định kiểu trả về của hàm bằng mũi tên ``->``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu trả về của hàm, hãy viết dấu gạch ngang và dấu ngoặc nhọn hướng sang phải ``->`` sau phần khai báo, rồi đến kiểu trả về:

::

    func _process(delta: float) -> void:
        pass

Kiểu ``void`` có nghĩa là hàm không trả về gì. Bạn có thể sử dụng bất kỳ kiểu nào, giống như với biến:

::

    func hit(damage: float) -> bool:
        health_points -= damage
        return health_points <= 0

Bạn cũng có thể sử dụng các class của riêng mình làm kiểu trả về:

.. code-block::

    # Thêm một item vào inventory và trả về item đó.
    func add(reference: Item, amount: int) -> Item:
        var item: Item = find_item(reference)
        if not item:
            item = ItemDatabase.get_instance(reference)

        item.amount += amount
        return item

Tính đồng biến và phản biến
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi kế thừa các method của class cơ sở, bạn nên tuân theo `nguyên tắc thay thế Liskov <https://en.wikipedia.org/wiki/Liskov_substitution_principle>`__.

**Tính đồng biến:** Khi kế thừa một method, bạn có thể chỉ định kiểu trả về cụ thể hơn (**kiểu con**) so với method của lớp cha.

**Tính phản biến:** Khi kế thừa một method, bạn có thể chỉ định kiểu tham số ít cụ thể hơn (**kiểu cha**) so với method của lớp cha.

Ví dụ:

.. code-block::

    class_name Parent


    func get_property(param: Label) -> Node:
        # ...

.. code-block::

    class_name Child extends Parent


    # `Control` là siêu kiểu của `Label`.
    # `Node2D` là kiểu con của `Node`.
    func get_property(param: Control) -> Node2D:
        # ...

Chỉ định kiểu phần tử của một ``Array``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu của một ``Array``, hãy đặt tên kiểu bên trong ``[]``.

Kiểu của mảng áp dụng cho các biến vòng lặp ``for``, cũng như một số toán tử như ``[]``, ``[...] =`` (phép gán) và ``+``. Các phương thức của mảng (chẳng hạn như ``push_back``) và các toán tử khác (chẳng hạn như ``==``) vẫn không có kiểu. Có thể sử dụng các kiểu dựng sẵn, các lớp native và lớp tùy chỉnh, cũng như enum làm kiểu phần tử. Các kiểu mảng lồng nhau (chẳng hạn như ``Array[Array[int]]``) không được hỗ trợ.


.. code-block::

    var scores: Array[int] = [10, 20, 30]
    var vehicles: Array[Node] = [$Car, $Plane]
    var items: Array[Item] = [Item.new()]
    var array_of_arrays: Array[Array] = [[], []]
    # var arrays: Array[Array[int]] -- không được phép

    for score in scores:
        # score có kiểu `int`

    # Những dòng sau sẽ gây ra lỗi:
    scores += vehicles
    var s: String = scores[0]
    scores[0] = "lots"

Từ Godot 4.2, bạn cũng có thể chỉ định kiểu cho biến vòng lặp trong vòng lặp ``for``. Ví dụ, bạn có thể viết:

::

    var names = ["John", "Marta", "Samantha", "Jimmy"]
    for name: String in names:
        pass

Mảng vẫn không có kiểu, nhưng biến ``name`` bên trong vòng lặp ``for`` sẽ luôn có kiểu ``String``.

Chỉ định kiểu phần tử của một ``Dictionary``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để xác định kiểu của các khóa và giá trị của một ``Dictionary``, hãy đặt tên kiểu bên trong ``[]`` và phân tách kiểu khóa với kiểu giá trị bằng dấu phẩy.

Kiểu giá trị của dictionary áp dụng cho các biến vòng lặp ``for``, cũng như một số toán tử như ``[]`` và ``[...] =`` (phép gán). Các phương thức của dictionary trả về giá trị và các toán tử khác (chẳng hạn như ``==``) vẫn không có kiểu. Có thể sử dụng các kiểu dựng sẵn, các lớp native và lớp tùy chỉnh, cũng như enum làm kiểu phần tử. Các collection có kiểu lồng nhau (chẳng hạn như ``Dictionary[String, Dictionary[String, int]]``) không được hỗ trợ.


.. code-block::

    var fruit_costs: Dictionary[String, int] = { "apple": 5, "orange": 10 }
    var vehicles: Dictionary[String, Node] = { "car": $Car, "plane": $Plane }
    var item_tiles: Dictionary[Vector2i, Item] = { Vector2i(0, 0): Item.new(), Vector2i(0, 1): Item.new() }
    var dictionary_of_dictionaries: Dictionary[String, Dictionary] = { { } }
    # var dicts: Dictionary[String, Dictionary[String, int]] -- không được phép

    for fruit in fruit_costs:
        # `fruit` có kiểu `String`

    # Những dòng sau sẽ gây ra lỗi:
    fruit_costs["pear"] += vehicles
    var s: String = fruit_costs["apple"]
    fruit_costs["orange"] = "lots"

Ép kiểu
~~~~~~~

Ép kiểu là một khái niệm quan trọng trong các ngôn ngữ có kiểu. Ép kiểu là việc chuyển đổi một giá trị từ kiểu này sang kiểu khác.

Hãy tưởng tượng trong game của bạn có một ``Enemy`` đang ``extends Area2D``. Bạn muốn nó va chạm với ``Player``, một ``CharacterBody2D`` được gắn script có tên ``PlayerController``. Bạn sử dụng signal ``body_entered`` để phát hiện va chạm. Với code có kiểu, body bạn phát hiện sẽ là một ``PhysicsBody2D`` chung, chứ không phải ``PlayerController`` của bạn trong callback ``_on_body_entered``.

Bạn có thể kiểm tra xem ``PhysicsBody2D`` này có phải là ``Player`` của mình hay không bằng từ khóa ``as``, rồi sử dụng dấu hai chấm ``:`` một lần nữa để buộc biến sử dụng kiểu này. Điều này buộc biến giữ kiểu ``PlayerController``:

::

    func _on_body_entered(body: PhysicsBody2D) -> void:
        var player := body as PlayerController
        if not player:
            return

        player.damage()

Vì chúng ta đang làm việc với một kiểu tùy chỉnh, nếu ``body`` không kế thừa ``PlayerController``, biến ``player`` sẽ được đặt thành ``null``. Chúng ta có thể dùng điều này để kiểm tra body có phải là player hay không. Nhờ phép ép kiểu đó, chúng ta cũng sẽ nhận được đầy đủ tính năng tự động hoàn thành cho biến player.

.. note::

    Từ khóa ``as`` âm thầm ép biến thành ``null`` nếu xảy ra không khớp kiểu tại runtime, mà không có lỗi/cảnh báo. Dù điều này có thể tiện lợi trong một số trường hợp, nó cũng có thể dẫn đến bug. Chỉ sử dụng từ khóa ``as`` khi đây là hành vi được chủ đích. Một lựa chọn an toàn hơn là sử dụng từ khóa ``is``:

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

    Nếu bạn thử ép kiểu bằng một kiểu dựng sẵn và việc ép kiểu thất bại, Godot sẽ báo lỗi.

.. _doc_gdscript_static_typing_safe_lines:

Dòng an toàn
^^^^^^^^^^^^

Bạn cũng có thể sử dụng phép ép kiểu để đảm bảo các dòng an toàn. Dòng an toàn là công cụ cho biết những dòng code không rõ ràng có an toàn về kiểu hay không. Vì bạn có thể kết hợp code có kiểu và code động, đôi khi Godot không có đủ thông tin để biết một lệnh có gây ra lỗi khi runtime hay không.

Điều này xảy ra khi bạn lấy một node con. Hãy lấy một timer làm ví dụ: với code động, bạn có thể lấy node bằng ``$Timer``. GDScript hỗ trợ `duck-typing <https://stackoverflow.com/a/4205163/8125343>`__, vì vậy ngay cả khi timer của bạn có kiểu ``Timer``, nó cũng là một ``Node`` và một ``Object``, tức là hai lớp mà nó kế thừa. Với GDScript động, bạn cũng không cần quan tâm đến kiểu của node miễn là nó có các phương thức bạn cần gọi.

Bạn có thể sử dụng phép ép kiểu để cho Godot biết kiểu bạn mong đợi khi lấy một node: ``($Timer as Timer)``, ``($Player as CharacterBody2D)``, v.v. Godot sẽ đảm bảo kiểu đó hoạt động, và nếu đúng như vậy, số dòng sẽ chuyển thành màu xanh ở bên trái trình soạn thảo script.

.. figure:: img/typed_gdscript_safe_unsafe_line.webp
   :alt: Dòng không an toàn so với dòng an toàn

   Dòng không an toàn (dòng 7) so với các dòng an toàn (dòng 6 và 8)

.. note::

    Dòng an toàn không phải lúc nào cũng đồng nghĩa với code tốt hơn hoặc đáng tin cậy hơn. Hãy xem lưu ý ở trên về từ khóa ``as``. Ví dụ:

    .. code-block::

        @onready var node_1 := $Node1 as Type1 # Dòng an toàn.
        @onready var node_2: Type2 = $Node2 # Dòng không an toàn.

    Mặc dù khai báo ``node_2`` được đánh dấu là dòng không an toàn, nó đáng tin cậy hơn khai báo ``node_1``. Vì nếu bạn thay đổi kiểu node trong scene nhưng vô tình quên thay đổi trong script, lỗi sẽ được phát hiện ngay khi scene được tải. Không giống ``node_1``, vốn sẽ được âm thầm ép thành ``null`` và lỗi sẽ được phát hiện muộn hơn.

.. note::

    Bạn có thể tắt các dòng an toàn hoặc thay đổi màu của chúng trong phần cài đặt của trình soạn thảo.

Có kiểu hay động: hãy nhất quán với một phong cách
--------------------------------------------------

GDScript có kiểu và GDScript động có thể cùng tồn tại trong một project. Tuy nhiên, bạn nên nhất quán với một trong hai phong cách để codebase của mình nhất quán và thuận tiện cho đồng đội. Mọi người sẽ dễ dàng làm việc cùng nhau hơn nếu tuân theo cùng một hướng dẫn, đồng thời đọc và hiểu code của nhau cũng nhanh hơn.

Code có kiểu cần viết nhiều hơn một chút, nhưng bạn sẽ nhận được những lợi ích đã thảo luận ở trên. Đây là ví dụ về cùng một script trống theo phong cách động:

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

Như bạn thấy, bạn cũng có thể sử dụng kiểu với các phương thức ảo của engine. Các callback của signal, cũng như mọi phương thức khác, cũng có thể sử dụng kiểu. Đây là một signal ``body_entered`` theo phong cách động:

::

    func _on_area_2d_body_entered(body):
        pass

Và callback tương tự với type hints:

::

    func _on_area_2d_body_entered(body: PhysicsBody2D) -> void:
        pass

Hệ thống cảnh báo
-----------------

.. note::

    Tài liệu chi tiết về hệ thống cảnh báo GDScript đã được chuyển đến
    :ref:`doc_gdscript_warning_system`.

Godot đưa ra cảnh báo về code của bạn trong khi bạn viết. Engine xác định những phần code có thể gây ra vấn đề trong runtime, nhưng cho phép bạn quyết định có muốn giữ nguyên code đó hay không.

Chúng tôi có một số cảnh báo dành riêng cho người dùng GDScript có kiểu. Theo mặc định, các cảnh báo này bị tắt; bạn có thể bật chúng trong Project Settings (**Debug > GDScript**, hãy đảm bảo đã bật **Advanced Settings**).

Bạn có thể bật cảnh báo ``UNTYPED_DECLARATION`` nếu muốn luôn sử dụng static types. Ngoài ra, bạn có thể bật cảnh báo ``INFERRED_DECLARATION`` nếu thích cú pháp dễ đọc và đáng tin cậy hơn, nhưng dài dòng hơn.

Cảnh báo ``UNSAFE_*`` khiến các thao tác không an toàn dễ nhận thấy hơn so với các dòng không an toàn. Hiện tại, cảnh báo ``UNSAFE_*`` chưa bao quát mọi trường hợp mà các dòng không an toàn bao quát.

Các thao tác không an toàn thường gặp và phiên bản an toàn tương ứng
--------------------------------------------------------------------

Các phương thức global scope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các phương thức global scope sau đây không được static typing, nhưng có các phương thức tương ứng đã được typing. Những phương thức này trả về các giá trị được static typing:

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

Khi sử dụng static typing, hãy dùng các phương thức global scope có typing bất cứ khi nào có thể. Điều này đảm bảo bạn có các dòng an toàn và được hưởng lợi từ các instruction có typing để đạt hiệu năng tốt hơn.

Cảnh báo ``UNSAFE_PROPERTY_ACCESS`` và ``UNSAFE_METHOD_ACCESS``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong ví dụ này, chúng ta muốn thiết lập một property và gọi một method trên một object có script được gắn với ``class_name MyScript`` và ``extends Node2D``. Nếu có một tham chiếu đến object dưới dạng ``Node2D`` (chẳng hạn như khi object được hệ thống physics truyền cho chúng ta), trước tiên chúng ta có thể kiểm tra xem property và method có tồn tại hay không, sau đó thiết lập và gọi chúng nếu có:

.. code-block::

    if "some_property" in node_2d:
        node_2d.some_property = 20  # Tạo cảnh báo UNSAFE_PROPERTY_ACCESS.

    if node_2d.has_method("some_function"):
        node_2d.some_function()  # Tạo cảnh báo UNSAFE_METHOD_ACCESS.

Tuy nhiên, code này sẽ tạo ra các cảnh báo ``UNSAFE_PROPERTY_ACCESS`` và ``UNSAFE_METHOD_ACCESS`` vì property và method không có trong kiểu được tham chiếu — trong trường hợp này là ``Node2D``. Để làm cho các thao tác này an toàn, trước tiên bạn có thể kiểm tra xem object có kiểu ``MyScript`` bằng từ khóa ``is`` hay không, sau đó khai báo một biến có kiểu ``MyScript`` để thiết lập các property và gọi các method của nó:

::

    if node_2d is MyScript:
        var my_script: MyScript = node_2d
        my_script.some_property = 20
        my_script.some_function()

Ngoài ra, bạn có thể khai báo một biến và sử dụng toán tử ``as`` để thử cast object. Sau đó, bạn cần kiểm tra xem việc cast có thành công hay không bằng cách xác nhận rằng biến đã được gán giá trị:

::

    var my_script := node_2d as MyScript
    if my_script != null:
        my_script.some_property = 20
        my_script.some_function()

Cảnh báo ``UNSAFE_CAST``
~~~~~~~~~~~~~~~~~~~~~~~~

Trong ví dụ này, chúng ta muốn label được kết nối với một object đi vào vùng va chạm hiển thị tên của vùng đó. Khi object đi vào vùng va chạm, hệ thống physics gửi một signal với object ``Node2D``, và giải pháp đơn giản nhất (nhưng không được static typing) để thực hiện điều chúng ta muốn có thể viết như sau:

.. code-block::

    func _on_body_entered(body: Node2D) -> void:
        body.label.text = name  # Tạo cảnh báo UNSAFE_PROPERTY_ACCESS.

Đoạn code này tạo ra cảnh báo ``UNSAFE_PROPERTY_ACCESS`` vì ``label`` không được định nghĩa trong ``Node2D``. Để giải quyết vấn đề này, trước tiên chúng ta có thể kiểm tra xem property ``label`` có tồn tại hay không và cast nó sang kiểu ``Label`` trước khi thiết lập property text như sau:

.. code-block::

    func _on_body_entered(body: Node2D) -> void:
        if "label" in body:
            (body.label as Label).text = name  # Tạo cảnh báo UNSAFE_CAST.

Tuy nhiên, cách này tạo ra cảnh báo ``UNSAFE_CAST`` vì ``body.label`` có kiểu ``Variant``. Để lấy property một cách an toàn với kiểu bạn muốn, bạn có thể sử dụng method ``Object.get()``, method này trả về object dưới dạng giá trị ``Variant`` hoặc trả về ``null`` nếu property không tồn tại. Sau đó, bạn có thể xác định liệu property có chứa một object đúng kiểu hay không bằng từ khóa ``is``, rồi khai báo một biến được static typing với object đó:

::

    func _on_body_entered(body: Node2D) -> void:
        var label_variant: Variant = body.get("label")
        if label_variant is Label:
            var label: Label = label_variant
            label.text = name

Các trường hợp không thể chỉ định kiểu
--------------------------------------

.. UPDATE: Not supported. If nested types are supported, update this section.

Để kết thúc phần giới thiệu này, hãy đề cập đến những trường hợp bạn không thể sử dụng type hints. Điều này sẽ kích hoạt **syntax error**.

1. Bạn không thể chỉ định kiểu cho từng phần tử riêng lẻ trong một array hoặc dictionary:

::

        var enemies: Array = [$Goblin: Enemy, $Zombie: Enemy]
        var character: Dictionary = {
            name: String = "Richard",
            money: int = 1000,
            inventory: Inventory = $Inventory,
        }

2. Hiện tại chưa hỗ trợ các kiểu lồng nhau:

::

        var teams: Array[Array[Character]] = []

Tóm tắt
-------

.. UPDATE: Planned feature. If more optimizations (possibly JIT/AOT?) are
.. implemented, update this paragraph.

GDScript có kiểu là một công cụ mạnh mẽ. Nó giúp bạn viết code có cấu trúc hơn, tránh các lỗi thường gặp và tạo ra những hệ thống có khả năng mở rộng, đáng tin cậy. Static types cải thiện hiệu năng của GDScript và sẽ có thêm nhiều tối ưu hóa trong tương lai.

.. _`some warnings`: Warning system_
