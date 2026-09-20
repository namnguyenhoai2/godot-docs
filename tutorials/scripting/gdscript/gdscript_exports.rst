.. _doc_gdscript_exports:

Các thuộc tính được export trong GDScript
=========================================

Trong Godot, các thành viên của class có thể được export. Điều này có nghĩa là giá trị của chúng được lưu cùng với resource (chẳng hạn như :ref:`scene <class_PackedScene>`) mà chúng được gắn vào, và được chuyển theo khi sử dụng :ref:`RPCs <doc_high_level_multiplayer_rpcs>`. Chúng cũng sẽ khả dụng để chỉnh sửa trong property editor. Việc export được thực hiện bằng annotation ``@export``.

::

    @export var number: int = 5

Trong ví dụ đó, giá trị ``5`` sẽ được lưu và hiển thị trong property editor.

Một biến được export phải được khởi tạo bằng một biểu thức hằng hoặc có type specifier trong biến. Một số export annotation có kiểu cụ thể và không cần biến được định kiểu (xem phần *Examples* bên dưới).

Một trong những lợi ích cơ bản của việc export các biến thành viên là làm cho chúng hiển thị và có thể chỉnh sửa trong editor. Nhờ đó, các artist và game designer có thể sửa đổi các giá trị, từ đó ảnh hưởng đến cách chương trình chạy. Để thực hiện việc này, một cú pháp export đặc biệt được cung cấp. Ngoài ra, có thể sử dụng :ref:`documentation comments <doc_gdscript_documentation_comments>` cho các mô tả tooltip, hiển thị khi di chuột qua.

.. note::

    Việc export các thuộc tính cũng có thể được thực hiện trong những ngôn ngữ khác như C#. Cú pháp thay đổi tùy theo ngôn ngữ. Xem :ref:`doc_c_sharp_exports` để biết thông tin về việc export trong C#.

Cách sử dụng cơ bản
-------------------

Nếu giá trị được export gán một hằng hoặc biểu thức hằng, kiểu sẽ được suy luận và sử dụng trong editor.

::

    @export var number = 5

Nếu không có giá trị mặc định, bạn có thể thêm kiểu cho biến.

::

    @export var number: int

Resource và node cũng có thể được export.

::

    @export var resource: Resource
    @export var node: Node

Ngay cả khi một script không được thực thi trong editor, các thuộc tính được export vẫn có thể chỉnh sửa. Tuy nhiên, getter và setter chỉ được sử dụng nếu script đang ở :ref:`doc_gdscript_tool_mode`.

Nhóm các thuộc tính được export
-------------------------------

Bạn có thể nhóm các thuộc tính được export trong Inspector bằng annotation :ref:`@export_group <class_@GDScript_annotation_@export_group>`. Mọi thuộc tính được export sau annotation này sẽ được thêm vào nhóm. Hãy bắt đầu một nhóm mới hoặc sử dụng ``@export_group("")`` để thoát khỏi nhóm.

::

    @export_group("My Properties")
    @export var number = 3

Đối số thứ hai của annotation có thể được sử dụng để chỉ nhóm các thuộc tính có prefix được chỉ định.

Không thể lồng các nhóm; hãy sử dụng :ref:`@export_subgroup <class_@GDScript_annotation_@export_subgroup>` để tạo các nhóm con bên trong một nhóm.

::

    @export_subgroup("Extra Properties")
    @export var string = ""
    @export var flag = false

Bạn cũng có thể thay đổi tên của category chính hoặc tạo thêm các category trong danh sách thuộc tính bằng annotation :ref:`@export_category <class_@GDScript_annotation_@export_category>`.

::

    @export_category("Main Category")
    @export var number = 3
    @export var string = ""

    @export_category("Extra Category")
    @export var flag = false

.. note::

    Danh sách thuộc tính được sắp xếp dựa trên việc kế thừa class, và các category mới sẽ phá vỡ quy tắc đó. Hãy sử dụng chúng cẩn thận, đặc biệt khi tạo các project để dùng công khai.

String làm đường dẫn
--------------------

String làm đường dẫn đến một file. Xem :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file var f

String làm đường dẫn đến một directory. Xem :ref:`@export_dir <class_@GDScript_annotation_@export_dir>`.

::

    @export_dir var f

String làm đường dẫn đến một file, với custom filter được cung cấp dưới dạng hint. Xem lại :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file("*.txt") var f

Cũng có thể sử dụng các đường dẫn trong global filesystem, nhưng chỉ trong các script ở tool mode.

String làm đường dẫn đến một file PNG trong global filesystem. Xem :ref:`@export_global_file <class_@GDScript_annotation_@export_global_file>`.

::

    @export_global_file("*.png") var tool_image

String làm đường dẫn đến một directory trong global filesystem. Xem :ref:`@export_global_dir <class_@GDScript_annotation_@export_global_dir>`.

::

    @export_global_dir var tool_dir

Annotation multiline yêu cầu editor hiển thị một trường nhập lớn để chỉnh sửa nhiều dòng. Xem :ref:`@export_multiline <class_@GDScript_annotation_@export_multiline>`.

::

    @export_multiline var text

String làm input action
-----------------------

String làm input action được định nghĩa trong input map của project.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME) var my_input

String làm input action được định nghĩa trong input map của project, cùng các giá trị tích hợp sẵn mặc định như ``ui_accept`` và ``ui_cancel``.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "show_builtin") var my_input

String làm input action được định nghĩa trong input map của project, cùng các giá trị tùy ý có thể nhập thủ công.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "loose_mode") var my_input

String làm input action được định nghĩa trong input map của project, cùng các giá trị tích hợp sẵn mặc định như ``ui_accept`` và ``ui_cancel``, cũng như các giá trị tùy ý có thể nhập thủ công.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "show_builtin,loose_mode") var my_input

Giới hạn phạm vi nhập trong editor
----------------------------------

Xem :ref:`@export_range <class_@GDScript_annotation_@export_range>` để biết tất cả các nội dung sau.

Cho phép các giá trị integer từ 0 đến 20.

::

    @export_range(0, 20) var i

Cho phép các giá trị integer từ -10 đến 20.

::

    @export_range(-10, 20) var j

Cho phép các giá trị float từ -10 đến 20 và snap giá trị theo các bội số của 0.2.

::

    @export_range(-10, 20, 0.2) var k: float

Có thể khiến các giới hạn chỉ ảnh hưởng đến slider bằng cách thêm các hint ``"or_less"`` và/hoặc ``"or_greater"``. Nếu sử dụng một trong các hint này, người dùng sẽ có thể nhập bất kỳ giá trị nào hoặc kéo giá trị bằng chuột khi không sử dụng slider, kể cả khi giá trị nằm ngoài phạm vi được chỉ định.

::

    @export_range(0, 100, 1, "or_less", "or_greater") var l: int

Hint ``"exp"`` có thể được sử dụng để làm cho giá trị có slider exponential thay vì slider tuyến tính. Điều này có nghĩa là khi kéo slider sang phải, các thay đổi sẽ nhanh dần khi kéo chuột. Tính năng này hữu ích để chỉnh sửa dễ dàng hơn các giá trị có thể rất nhỏ hoặc rất lớn, nhưng đổi lại sẽ kém trực quan hơn.

::

    @export_range(0, 100000, 0.01, "exp") var exponential: float

Đối với các giá trị dùng để biểu diễn một easing factor, hãy sử dụng
:ref:`doc_gdscript_exports_floats_with_easing_hint` instead.

Hint ``"hide_slider"`` có thể được sử dụng để ẩn thanh ngang xuất hiện bên dưới các thuộc tính ``float`` hoặc các mũi tên lên/xuống xuất hiện bên cạnh các thuộc tính ``int``:

::

    @export_range(0, 1000, 0.01, "hide_slider") var no_slider: float

Ngược lại, hint ``"prefer_slider"`` có thể được sử dụng để hiển thị một thanh ngang bên dưới các thuộc tính ``int`` thay cho các mũi tên lên/xuống:

::

    @export_range(0, 100, 1, "prefer_slider") var with_slider: int

Thêm hậu tố và xử lý độ và radian
---------------------------------

Bạn cũng có thể định nghĩa một hậu tố để làm cho giá trị dễ hiểu hơn trong inspector. Ví dụ, để định nghĩa một giá trị mà người dùng dự định cấu hình theo "meters" (``m``):

::

    @export_range(0, 100, 1, "suffix:m") var m: int

Đối với các góc được lưu dưới dạng radian nhưng hiển thị với người dùng dưới dạng độ, hãy sử dụng hint `"radians_as_degrees"`:

::

    @export_range(0, 360, 0.1, "radians_as_degrees") var angle: float

Cách này tự động chuyển đổi khi giá trị được hiển thị hoặc sửa đổi trong inspector, đồng thời hiển thị hậu tố degree (``°``). Cách tiếp cận này được sử dụng bởi các thuộc tính `rotation` của chính Godot trong toàn bộ editor.

Nếu góc được lưu dưới dạng độ, hãy sử dụng hint `"degrees"` để hiển thị ký hiệu độ, đồng thời tắt việc tự động chuyển đổi từ độ sang radian khi giá trị được sửa đổi từ inspector.

Liên kết các giá trị vector
---------------------------

Có thể liên kết các giá trị vector với nhau. Khi người dùng điều chỉnh một trong các thành phần của vector, những thành phần khác sẽ tự động được điều chỉnh theo tỷ lệ. Ví dụ, tính năng này hữu ích để duy trì tỷ lệ khung hình của một sprite 2D khi điều chỉnh scale. Người dùng có thể tạm thời tắt tính năng này bằng cách nhấp vào biểu tượng liên kết ở bên phải thuộc tính.

::

    # Để chuỗi hint trống nếu bạn không muốn thêm hậu tố.
    @export_custom(PROPERTY_HINT_LINK, "suffix:px") var vector2_linked: Vector2 = Vector2(16, 16)

Kết quả:

.. figure:: img/gdscript_exports_linked_vector.webp
   :align: center
   :alt: Linked Vector2i property with the "px" suffix

   Linked Vector2i property with the "px" suffix

:ref:`This hint <class_@GlobalScope_constant_PROPERTY_HINT_LINK>` is effective
trên Vector2, Vector2i, Vector3, Vector3i, Vector4 và Vector4i. Có thể sử dụng đồng thời với hậu tố thuộc tính, như trong ví dụ ở trên.

.. _doc_gdscript_exports_floats_with_easing_hint:

Float với hint easing
---------------------

Hiển thị biểu diễn trực quan của hàm ``ease()`` khi chỉnh sửa. Xem :ref:`@export_exp_easing <class_@GDScript_annotation_@export_exp_easing>`.

::

    @export_exp_easing var transition_speed

Màu sắc
-------

Màu thông thường được cung cấp dưới dạng giá trị red-green-blue-alpha.

::

    @export var col: Color

Màu được cung cấp dưới dạng giá trị red-green-blue (alpha luôn là 1). Xem :ref:`@export_color_no_alpha <class_@GDScript_annotation_@export_color_no_alpha>`.

::

    @export_color_no_alpha var col: Color

Node
----

Node cũng có thể được export trực tiếp dưới dạng thuộc tính trong script mà không cần sử dụng NodePath:

::

    # Cho phép mọi node.
    @export var node: Node

    # Cho phép mọi node kế thừa từ BaseButton.
    # Các custom class được khai báo bằng `class_name` cũng có thể được sử dụng.
    @export var some_button: BaseButton

Vẫn có thể export NodePath như trong Godot 3.x nếu bạn cần:

::

    @export var node_path: NodePath
    var node = get_node(node_path)

Nếu muốn giới hạn các kiểu node cho NodePath, bạn có thể sử dụng
:ref:`@export_node_path<class_@GDScript_annotation_@export_node_path>`
annotation:

::

    @export_node_path("Button", "TouchScreenButton") var some_button

Resource
--------

::

    @export var resource: Resource

Trong Inspector, bạn có thể kéo và thả một file resource từ dock FileSystem vào ô biến.

Tuy nhiên, việc mở dropdown của inspector có thể dẫn đến một danh sách cực kỳ dài các class có thể tạo. Vì vậy, nếu bạn chỉ định một extension của Resource như sau:

::

    @export var resource: AnimationNode

Menu thả xuống sẽ chỉ giới hạn ở AnimationNode và tất cả các class dẫn xuất của nó.

.. note::

    Việc sử dụng các biến ``@export`` cho các object :ref:`Resource <class_Resource>` khiến chúng trở thành dependency của instance, nghĩa là tất cả resource được tham chiếu bởi các biến ``@export`` sẽ được load khi scene chứa script được load. Nếu bạn muốn tham chiếu một
    :ref:`Resource <class_Resource>` object but load it manually when you need
    nó (chẳng hạn, đây thường là trường hợp đối với
    :ref:`PackedScenes <class_PackedScene>` containing a whole level), use
    thay vào đó là ``@export_file`` hoặc ``@export_file_path``.

.. _doc_gdscript_exports_exporting_bit_flags:

Export các cờ bit
-----------------

Xem :ref:`@export_flags <class_@GDScript_annotation_@export_flags>`.

Integers used as bit flags can store multiple ``true``/``false`` (boolean) values in one property. By using the ``@export_flags`` annotation, they can be set from the editor:

::

    # Đặt bất kỳ cờ nào được cung cấp từ trình chỉnh sửa.
    @export_flags("Fire", "Water", "Earth", "Wind") var spell_elements = 0

Bạn phải cung cấp mô tả dạng chuỗi cho mỗi cờ. Trong ví dụ này, ``Fire`` có giá trị 1, ``Water`` có giá trị 2, ``Earth`` có giá trị 4 và ``Wind`` tương ứng với giá trị 8. Thông thường, các hằng số nên được định nghĩa tương ứng (ví dụ: ``const ELEMENT_WIND = 8`` và các giá trị tiếp theo).

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_flags("Self:4", "Allies:8", "Foes:16") var spell_targets = 0

Chỉ các giá trị lũy thừa của 2 mới hợp lệ làm tùy chọn cờ bit. Giá trị thấp nhất được phép là 1, vì 0 có nghĩa là không có gì được chọn. Bạn cũng có thể thêm các tùy chọn là sự kết hợp của các cờ khác:

::

    @export_flags("Self:4", "Allies:8", "Self and Allies:12", "Foes:16")
    var spell_targets = 0

Các chú thích export cũng được cung cấp cho các layer physics, render và navigation được định nghĩa trong project settings:

::

    @export_flags_2d_physics var layers_2d_physics
    @export_flags_2d_render var layers_2d_render
    @export_flags_2d_navigation var layers_2d_navigation
    @export_flags_3d_physics var layers_3d_physics
    @export_flags_3d_render var layers_3d_render
    @export_flags_3d_navigation var layers_3d_navigation

Việc sử dụng cờ bit đòi hỏi một số hiểu biết về các phép toán bitwise. Nếu không chắc chắn, hãy sử dụng các biến boolean thay thế.

Export enum
-----------

Xem :ref:`@export_enum <class_@GDScript_annotation_@export_enum>`.

Các property có thể được export với type hint tham chiếu đến một enum để giới hạn giá trị của chúng ở các giá trị trong enumeration. Trình chỉnh sửa sẽ tạo một widget trong Inspector, liệt kê các mục sau dưới dạng "Thing 1", "Thing 2", "Another Thing". Giá trị sẽ được lưu dưới dạng số nguyên.

::

    enum NamedEnum {THING_1, THING_2, ANOTHER_THING = -1}
    @export var x: NamedEnum

Các property kiểu số nguyên và chuỗi cũng có thể được giới hạn trong một danh sách giá trị cụ thể bằng chú thích :ref:`@export_enum <class_@GDScript_annotation_@export_enum>`. Trình chỉnh sửa sẽ tạo một widget trong Inspector, liệt kê các mục sau: Warrior, Magician, Thief. Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn được chọn (tức là ``0``, ``1`` hoặc ``2``).

::

    @export_enum("Warrior", "Magician", "Thief") var character_class: int

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_enum("Slow:30", "Average:60", "Very Fast:200") var character_speed: int

Nếu kiểu là String, giá trị sẽ được lưu dưới dạng chuỗi.

::

    @export_enum("Rebecca", "Mary", "Leah") var character_name: String

Nếu muốn đặt giá trị ban đầu, bạn phải chỉ định giá trị đó một cách tường minh:

::

    @export_enum("Rebecca", "Mary", "Leah") var character_name: String = "Rebecca"

Export array
------------

Các array được export có thể có giá trị khởi tạo, nhưng chúng phải là các biểu thức hằng số.

Nếu array được export chỉ định một kiểu kế thừa từ Resource, bạn có thể đặt các giá trị của array trong inspector bằng cách kéo và thả nhiều file cùng lúc từ dock FileSystem.

Giá trị mặc định **phải** là một biểu thức hằng số.

::

    @export var a = [1, 2, 3]

.. CẬP NHẬT: Chưa được hỗ trợ. Khi các array có kiểu lồng nhau được hỗ trợ, hãy cập nhật .. ví dụ.

Các array được export có thể chỉ định kiểu (sử dụng các hint giống như trước).

::

    @export var ints: Array[int] = [1, 2, 3]

    # Các array có kiểu lồng nhau như `Array[Array[float]]` hiện chưa được hỗ trợ.
    @export var two_dimensional: Array[Array] = [[1.0, 2.0], [3.0, 4.0]]

Bạn có thể bỏ qua giá trị mặc định, nhưng khi đó giá trị sẽ là ``null`` nếu chưa được gán.

::

    @export var b: Array
    @export var scenes: Array[PackedScene]

Các array có kiểu được chỉ định và kế thừa từ resource có thể được thiết lập bằng cách kéo và thả nhiều file từ dock FileSystem.

::

    @export var textures: Array[Texture] = []
    @export var scenes: Array[PackedScene] = []

Các packed array cũng hoạt động, nhưng chỉ khi được khởi tạo rỗng:

::

    @export var vector3s = PackedVector3Array()
    @export var strings = PackedStringArray()

Các biến thể export khác cũng có thể được sử dụng khi export array:

::

    @export_range(-360, 360, 0.001, "degrees") var laser_angles: Array[float] = []
    @export_file("*.json") var skill_trees: Array[String] = []
    @export_color_no_alpha var hair_colors = PackedColorArray()
    @export_enum("Espresso", "Mocha", "Latte", "Capuccino") var barista_suggestions: Array[String] = []

``@export_storage``
-------------------

Xem :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`.

Theo mặc định, việc export một property có hai tác động:

1. lưu property trong file scene/resource (:ref:`PROPERTY_USAGE_STORAGE <class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`); 2. thêm một trường vào Inspector (:ref:`PROPERTY_USAGE_EDITOR <class_@GlobalScope_constant_PROPERTY_USAGE_EDITOR>`).

Tuy nhiên, đôi khi bạn có thể muốn làm cho một property có thể được serialize, nhưng không hiển thị property đó trong trình chỉnh sửa để tránh các thay đổi ngoài ý muốn và giao diện bị rối.

Để thực hiện việc này, bạn có thể sử dụng :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`. Điều này có thể hữu ích cho các script :ref:`@tool <class_@GDScript_annotation_@tool>`. Ngoài ra, giá trị property được sao chép khi gọi :ref:`Resource.duplicate() <class_Resource_method_duplicate>` hoặc :ref:`Node.duplicate() <class_Node_method_duplicate>`, không giống như các biến không được export.

::

    var a # Không được lưu trong file, không hiển thị trong trình chỉnh sửa.
    @export_storage var b # Được lưu trong file, không hiển thị trong trình chỉnh sửa.
    @export var c: int # Được lưu trong file, hiển thị trong trình chỉnh sửa.

``@export_custom``
------------------

Nếu cần nhiều quyền kiểm soát hơn những gì các chú thích ``@export`` tích hợp sẵn cung cấp, bạn có thể sử dụng ``@export_custom`` thay thế. Điều này cho phép định nghĩa bất kỳ property hint, hint string và usage flag nào, với cú pháp tương tự cú pháp mà trình chỉnh sửa sử dụng cho các node tích hợp sẵn.

Ví dụ, đoạn này export property ``altitude`` không có giới hạn phạm vi nhưng có hậu tố ``m`` (mét) được định nghĩa:

::

    @export_custom(PROPERTY_HINT_NONE, "suffix:m") var altitude: float

Thông thường, điều trên không khả thi với cú pháp ``@export_range`` tiêu chuẩn, vì cú pháp này yêu cầu định nghĩa một phạm vi.

Xem :ref:`class reference <class_@GDScript_annotation_@export_custom>` để biết danh sách các tham số và giá trị được phép của chúng.

.. warning::

    Khi sử dụng ``@export_custom``, GDScript không thực hiện bất kỳ validation nào đối với cú pháp. Cú pháp không hợp lệ có thể gây ra hành vi không mong muốn trong inspector.

``@export_tool_button``
-----------------------

Nếu cần tạo một button trong inspector có thể nhấp, bạn có thể sử dụng ``@export_tool_button``. Chú thích này export một property ``Callable`` dưới dạng button có thể nhấp. Khi button được nhấn, callable sẽ được gọi.

Bạn có thể chỉ định tên icon tùy chỉnh, tên này phải khớp với một trong các tên file icon từ thư mục `editor/icons <https://github.com/godotengine/godot/tree/master/editor/icons>`__ trong repository mã nguồn Godot (phân biệt chữ hoa chữ thường). Bạn cũng có thể duyệt các icon của trình chỉnh sửa bằng website `Godot editor icons <https://godot-editor-icons.github.io/>`__.

Ví dụ, nếu muốn sử dụng ``Node2D.svg`` từ thư mục đó, bạn phải chỉ định ``"Node2D"`` làm tham số thứ hai của ``@export_tool_button``. Hiện tại không thể sử dụng icon tùy chỉnh từ thư mục project; chỉ có thể sử dụng các icon tích hợp sẵn của trình chỉnh sửa.

Đoạn này export một button có nhãn ``"Hello"`` và icon ``"Callable"`` (đây là giá trị mặc định nếu không chỉ định icon). Khi nhấn button, nó sẽ in ra ``"Hello world!"``.

::

    @tool
    extends Node

    @export_tool_button("Hello", "Callable") var hello_action = hello

    func hello():
        print("Hello world!")

Thiết lập các biến được export từ tool script
---------------------------------------------

Khi thay đổi giá trị của một biến được export từ một script trong
:ref:`doc_gdscript_tool_mode`, the value in the inspector won't be updated
một cách tự động. Để cập nhật biến, hãy gọi
:ref:`notify_property_list_changed() <class_Object_method_notify_property_list_changed>`
sau khi đặt giá trị của biến được export.

Đọc giá trị của biến được export quá sớm
----------------------------------------

Nếu đọc giá trị của một biến được export trong :ref:`_init() <class_Object_private_method__init>`, nó sẽ trả về giá trị mặc định được chỉ định trong chú thích export thay vì giá trị đã được đặt trong inspector. Điều này là do việc gán các giá trị từ file scene/resource đã lưu diễn ra *sau* khi khởi tạo object; cho đến lúc đó, giá trị mặc định được sử dụng.

Để lấy giá trị đã được đặt trong inspector (và do đó đã được lưu trong file scene/resource), bạn cần đọc giá trị đó *sau* khi object được khởi tạo, chẳng hạn như trong
:ref:`Node._ready() <class_Node_private_method__ready>`. You can also read the value
trong một setter được định nghĩa trên property được export, điều này hữu ích trong các custom resource nơi ``_ready()`` không khả dụng:

::

    # Đặt property này thành 3 trong inspector.
    @export var exported_variable = 2:
        set(value):
            exported_variable = value
            print("Inspector-set value: ", exported_variable)

    func _init():
        print("Initial value: ", exported_variable)

Cho kết quả:

.. code-block:: none

    Initial value: 2
    Inspector-set value: 3

Export nâng cao
---------------

Không phải mọi kiểu export đều có thể được cung cấp ở cấp độ ngôn ngữ để tránh độ phức tạp thiết kế không cần thiết. Phần sau mô tả một số tính năng export tương đối phổ biến có thể được triển khai bằng low-level API.

Trước khi đọc tiếp, bạn nên làm quen với cách các property được xử lý và cách chúng có thể được tùy chỉnh bằng
:ref:`_set() <class_Object_private_method__set>`,
:ref:`_get() <class_Object_private_method__get>`, and
:ref:`_get_property_list() <class_Object_private_method__get_property_list>` methods as
được mô tả trong :ref:`doc_accessing_data_or_logic_from_object`.

.. seealso:: For binding properties using the above methods in C++, see
             :ref:`doc_binding_properties_using_set_get_property_list`.

.. warning:: The script must operate in the ``@tool`` mode so the above methods
             có thể hoạt động từ bên trong trình chỉnh sửa.
