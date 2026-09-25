.. _doc_gdscript_exports:

Các thuộc tính được export của GDScript
=======================================

Trong Godot, các thành viên của class có thể được export. Điều này có nghĩa là giá trị của chúng sẽ được lưu cùng với resource (chẳng hạn như :ref:`scene <class_PackedScene>`) mà chúng được gắn vào, và được truyền đi khi sử dụng :ref:`RPCs <doc_high_level_multiplayer_rpcs>`. Chúng cũng sẽ khả dụng để chỉnh sửa trong property editor. Việc export được thực hiện bằng cách sử dụng annotation ``@export``.

::

    @export var number: int = 5

Trong ví dụ đó, giá trị ``5`` sẽ được lưu và hiển thị trong property editor.

Một biến được export phải được khởi tạo bằng một biểu thức hằng hoặc có type specifier trong biến. Một số export annotation có kiểu cụ thể và không cần biến được chỉ định kiểu (xem phần *Examples* bên dưới).

Một trong những lợi ích nền tảng của việc export các biến thành viên là làm cho chúng hiển thị và có thể chỉnh sửa trong editor. Nhờ đó, artist và game designer có thể sửa đổi các giá trị, những giá trị này sau đó sẽ ảnh hưởng đến cách chương trình chạy. Để thực hiện việc này, một cú pháp export đặc biệt được cung cấp. Ngoài ra, :ref:`documentation comments <doc_gdscript_documentation_comments>` có thể được dùng cho phần mô tả tooltip, hiển thị khi di chuột qua.

.. note::

    Các thuộc tính cũng có thể được export trong những ngôn ngữ khác như C#. Cú pháp sẽ thay đổi tùy theo ngôn ngữ. Xem :ref:`doc_c_sharp_exports` để biết thông tin về việc export trong C#.

Cách sử dụng cơ bản
-------------------

Nếu giá trị được export gán một hằng hoặc biểu thức hằng, kiểu sẽ được suy luận và sử dụng trong editor.

::

    @export var number = 5

Nếu không có giá trị mặc định, bạn có thể thêm kiểu cho biến.

::

    @export var number: int

Có thể export resource và node.

::

    @export var resource: Resource
    @export var node: Node

Ngay cả khi một script không được thực thi trong editor, các thuộc tính được export vẫn có thể chỉnh sửa. Tuy nhiên, getter và setter chỉ được sử dụng nếu script ở :ref:`doc_gdscript_tool_mode`.

Nhóm các thuộc tính export
--------------------------

Bạn có thể nhóm các thuộc tính được export trong Inspector bằng annotation :ref:`@export_group <class_@GDScript_annotation_@export_group>`. Mọi thuộc tính được export sau annotation này sẽ được thêm vào nhóm. Hãy bắt đầu một nhóm mới hoặc sử dụng ``@export_group("")`` để thoát khỏi nhóm.

::

    @export_group("My Properties")
    @export var number = 3

Đối số thứ hai của annotation có thể được dùng để chỉ nhóm các thuộc tính có prefix được chỉ định.

Không thể lồng các nhóm, hãy sử dụng :ref:`@export_subgroup <class_@GDScript_annotation_@export_subgroup>` để tạo các nhóm con bên trong một nhóm.

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

    Danh sách thuộc tính được sắp xếp dựa trên tính kế thừa của class, còn các category mới sẽ phá vỡ quy tắc sắp xếp đó. Hãy sử dụng chúng cẩn thận, đặc biệt khi tạo project để sử dụng công khai.

Chuỗi dưới dạng đường dẫn
-------------------------

Chuỗi dưới dạng đường dẫn đến một file. Xem :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file var f

Chuỗi dưới dạng đường dẫn đến một thư mục. Xem :ref:`@export_dir <class_@GDScript_annotation_@export_dir>`.

::

    @export_dir var f

Chuỗi dưới dạng đường dẫn đến một file, với custom filter được cung cấp dưới dạng gợi ý. Xem lại :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file("*.txt") var f

Cũng có thể sử dụng các đường dẫn trong global filesystem, nhưng chỉ trong các script ở tool mode.

Chuỗi dưới dạng đường dẫn đến một file PNG trong global filesystem. Xem :ref:`@export_global_file <class_@GDScript_annotation_@export_global_file>`.

::

    @export_global_file("*.png") var tool_image

Chuỗi dưới dạng đường dẫn đến một thư mục trong global filesystem. Xem :ref:`@export_global_dir <class_@GDScript_annotation_@export_global_dir>`.

::

    @export_global_dir var tool_dir

Annotation multiline yêu cầu editor hiển thị một trường nhập liệu lớn để chỉnh sửa trên nhiều dòng. Xem :ref:`@export_multiline <class_@GDScript_annotation_@export_multiline>`.

::

    @export_multiline var text

Chuỗi dưới dạng input action
----------------------------

Chuỗi dưới dạng một input action được định nghĩa trong input map của project.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME) var my_input

Chuỗi dưới dạng một input action được định nghĩa trong input map của project, cùng các giá trị dựng sẵn mặc định như ``ui_accept`` và ``ui_cancel``.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "show_builtin") var my_input

Chuỗi dưới dạng một input action được định nghĩa trong input map của project, cùng các giá trị tùy ý có thể nhập thủ công.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "loose_mode") var my_input

Chuỗi dưới dạng một input action được định nghĩa trong input map của project, cùng các giá trị dựng sẵn mặc định như ``ui_accept`` và ``ui_cancel``, cũng như các giá trị tùy ý có thể nhập thủ công.

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

Có thể sử dụng hint ``"exp"`` để làm cho giá trị có slider hàm mũ thay vì slider tuyến tính. Điều này có nghĩa là khi kéo slider sang phải, các thay đổi sẽ nhanh dần khi kéo chuột. Cách này hữu ích để chỉnh sửa dễ dàng hơn các giá trị có thể rất nhỏ hoặc rất lớn, nhưng kém trực quan hơn.

::

    @export_range(0, 100000, 0.01, "exp") var exponential: float

Đối với các giá trị được dùng để biểu diễn một hệ số easing, hãy sử dụng
:ref:`doc_gdscript_exports_floats_with_easing_hint` thay thế.

Có thể sử dụng hint ``"hide_slider"`` để ẩn thanh ngang xuất hiện bên dưới các thuộc tính ``float``, hoặc các mũi tên lên/xuống xuất hiện bên cạnh các thuộc tính ``int``:

::

    @export_range(0, 1000, 0.01, "hide_slider") var no_slider: float

Ngược lại, có thể sử dụng hint ``"prefer_slider"`` để hiển thị một thanh ngang bên dưới các thuộc tính ``int`` thay cho các mũi tên lên/xuống:

::

    @export_range(0, 100, 1, "prefer_slider") var with_slider: int

Thêm hậu tố và xử lý độ/radian
------------------------------

Bạn cũng có thể định nghĩa một hậu tố để làm cho giá trị dễ hiểu hơn trong inspector. Ví dụ, để định nghĩa một giá trị mà người dùng dự kiến sẽ cấu hình dưới dạng "meters" (``m``):

::

    @export_range(0, 100, 1, "suffix:m") var m: int

Đối với các góc được lưu dưới dạng radian nhưng hiển thị cho người dùng dưới dạng độ, hãy sử dụng hint `"radians_as_degrees"`:

::

    @export_range(0, 360, 0.1, "radians_as_degrees") var angle: float

Thao tác này tự động chuyển đổi khi giá trị được hiển thị hoặc sửa đổi trong inspector, đồng thời hiển thị hậu tố degree (``°``). Cách tiếp cận này được sử dụng cho các thuộc tính `rotation` của chính Godot trong toàn bộ editor.

Nếu góc được lưu dưới dạng độ, hãy sử dụng hint `"degrees"` để hiển thị ký hiệu độ, đồng thời tắt việc tự động chuyển đổi từ độ sang radian khi giá trị được sửa đổi trong inspector.

Liên kết các giá trị vector với nhau
------------------------------------

Có thể liên kết các giá trị vector với nhau. Khi người dùng điều chỉnh một trong các thành phần của vector, các thành phần khác sẽ tự động được điều chỉnh theo tỷ lệ. Ví dụ, tính năng này hữu ích để duy trì tỷ lệ khung hình của một sprite 2D khi điều chỉnh scale. Người dùng có thể tạm thời tắt tính năng này bằng cách nhấp vào biểu tượng liên kết ở bên phải thuộc tính.

::

    # Leave the hint string empty if you don't want to add a suffix.
    @export_custom(PROPERTY_HINT_LINK, "suffix:px") var vector2_linked: Vector2 = Vector2(16, 16)

Kết quả:

.. figure:: img/gdscript_exports_linked_vector.webp
   :align: center
   :alt: Thuộc tính Vector2i được liên kết với hậu tố "px"

   Thuộc tính Vector2i được liên kết với hậu tố "px"

:ref:`Gợi ý này <class_@GlobalScope_constant_PROPERTY_HINT_LINK>` có hiệu lực với Vector2, Vector2i, Vector3, Vector3i, Vector4 và Vector4i. Gợi ý này có thể được sử dụng đồng thời với hậu tố thuộc tính, như trong ví dụ trên.

.. _doc_gdscript_exports_floats_with_easing_hint:

Float với gợi ý easing
----------------------

Hiển thị biểu diễn trực quan của hàm ``ease()`` khi chỉnh sửa. Xem :ref:`@export_exp_easing <class_@GDScript_annotation_@export_exp_easing>`.

::

    @export_exp_easing var transition_speed

Màu
---

Màu thông thường được biểu diễn dưới dạng giá trị red-green-blue-alpha.

::

    @export var col: Color

Màu được biểu diễn dưới dạng giá trị red-green-blue (alpha luôn là 1). Xem :ref:`@export_color_no_alpha <class_@GDScript_annotation_@export_color_no_alpha>`.

::

    @export_color_no_alpha var col: Color

Node
----

Node cũng có thể được export trực tiếp dưới dạng thuộc tính trong script mà không cần sử dụng NodePath:

::

    # Allows any node.
    @export var node: Node

    # Allows any node that inherits from BaseButton.
    # Custom classes declared with `class_name` can also be used.
    @export var some_button: BaseButton

Vẫn có thể export NodePath như trong Godot 3.x, trong trường hợp bạn cần:

::

    @export var node_path: NodePath
    var node = get_node(node_path)

Nếu muốn giới hạn các kiểu node cho NodePath, bạn có thể sử dụng
annotation :ref:`@export_node_path <class_@GDScript_annotation_@export_node_path>`:

::

    @export_node_path("Button", "TouchScreenButton") var some_button

Resource
--------

::

    @export var resource: Resource

Trong Inspector, bạn có thể kéo và thả tệp resource từ dock FileSystem vào ô biến.

Tuy nhiên, việc mở danh sách thả xuống của Inspector có thể hiển thị một danh sách cực kỳ dài các class có thể tạo. Vì vậy, nếu bạn chỉ định một phần mở rộng của Resource, chẳng hạn như:

::

    @export var resource: AnimationNode

Menu thả xuống sẽ chỉ bao gồm AnimationNode và tất cả các class dẫn xuất của nó.

.. note::

    Việc sử dụng các biến ``@export`` cho các object :ref:`Resource <class_Resource>` khiến chúng trở thành dependency của instance, nghĩa là tất cả resource được tham chiếu bởi các biến ``@export`` sẽ được tải khi scene chứa script được tải. Nếu muốn tham chiếu một
    object :ref:`Resource <class_Resource>` nhưng tự tải object đó khi cần (ví dụ, thường xảy ra với
    :ref:`PackedScenes <class_PackedScene>` chứa toàn bộ một level), hãy sử dụng ``@export_file`` hoặc ``@export_file_path`` thay thế.

.. _doc_gdscript_exports_exporting_bit_flags:

Export cờ bit
-------------

Xem :ref:`@export_flags <class_@GDScript_annotation_@export_flags>`.

Các số nguyên được sử dụng làm cờ bit có thể lưu trữ nhiều giá trị ``true``/``false`` (boolean) trong một thuộc tính. Bằng cách sử dụng annotation ``@export_flags``, chúng có thể được thiết lập từ editor:

::

    # Set any of the given flags from the editor.
    @export_flags("Fire", "Water", "Earth", "Wind") var spell_elements = 0

Bạn phải cung cấp mô tả dạng chuỗi cho mỗi cờ. Trong ví dụ này, ``Fire`` có giá trị 1, ``Water`` có giá trị 2, ``Earth`` có giá trị 4 và ``Wind`` tương ứng với giá trị 8. Thông thường, các hằng số nên được định nghĩa tương ứng (ví dụ: ``const ELEMENT_WIND = 8`` và các hằng số tiếp theo).

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_flags("Self:4", "Allies:8", "Foes:16") var spell_targets = 0

Chỉ các giá trị là lũy thừa của 2 mới hợp lệ làm tùy chọn cờ bit. Giá trị nhỏ nhất được phép là 1, vì 0 nghĩa là không có gì được chọn. Bạn cũng có thể thêm các tùy chọn là tổ hợp của những cờ khác:

::

    @export_flags("Self:4", "Allies:8", "Self and Allies:12", "Foes:16")
    var spell_targets = 0

Các annotation export cũng được cung cấp cho các layer physics, render và navigation được định nghĩa trong project settings:

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

Các thuộc tính có thể được export với một type hint tham chiếu đến enum để giới hạn giá trị của chúng trong các giá trị của enumeration. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau dưới dạng "Thing 1", "Thing 2", "Another Thing". Giá trị sẽ được lưu dưới dạng số nguyên.

::

    enum NamedEnum {THING_1, THING_2, ANOTHER_THING = -1}
    @export var x: NamedEnum

Các thuộc tính số nguyên và chuỗi cũng có thể được giới hạn trong một danh sách giá trị cụ thể bằng annotation :ref:`@export_enum <class_@GDScript_annotation_@export_enum>`. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau dưới dạng Warrior, Magician, Thief. Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn được chọn (tức là ``0``, ``1`` hoặc ``2``).

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

Export mảng
-----------

Các mảng được export có thể có initializer, nhưng chúng phải là các biểu thức hằng số.

Nếu mảng được export chỉ định một kiểu kế thừa từ Resource, các giá trị của mảng có thể được thiết lập trong Inspector bằng cách kéo và thả đồng thời nhiều tệp từ dock FileSystem.

Giá trị mặc định **phải** là một biểu thức hằng số.

::

    @export var a = [1, 2, 3]

.. UPDATE: Not supported yet. When nested typed arrays are supported, update
.. the example.

Các mảng được export có thể chỉ định kiểu (sử dụng các hint giống như trước đây).

::

    @export var ints: Array[int] = [1, 2, 3]

    # Nested typed arrays such as `Array[Array[float]]` are not supported yet.
    @export var two_dimensional: Array[Array] = [[1.0, 2.0], [3.0, 4.0]]

Bạn có thể bỏ qua giá trị mặc định, nhưng khi đó giá trị sẽ là ``null`` nếu chưa được gán.

::

    @export var b: Array
    @export var scenes: Array[PackedScene]

Các mảng có kiểu được chỉ định và kế thừa từ resource có thể được thiết lập bằng cách kéo và thả nhiều tệp từ dock FileSystem.

::

    @export var textures: Array[Texture] = []
    @export var scenes: Array[PackedScene] = []

Các mảng packed cũng hoạt động, nhưng chỉ khi được khởi tạo rỗng:

::

    @export var vector3s = PackedVector3Array()
    @export var strings = PackedStringArray()

Các biến thể export khác cũng có thể được sử dụng khi export mảng:

::

    @export_range(-360, 360, 0.001, "degrees") var laser_angles: Array[float] = []
    @export_file("*.json") var skill_trees: Array[String] = []
    @export_color_no_alpha var hair_colors = PackedColorArray()
    @export_enum("Espresso", "Mocha", "Latte", "Capuccino") var barista_suggestions: Array[String] = []

``@export_storage``
-------------------

Xem :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`.

Theo mặc định, việc export một thuộc tính có hai tác động:

1. lưu thuộc tính trong tệp scene/resource (:ref:`PROPERTY_USAGE_STORAGE <class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`);
2. thêm một trường vào Inspector (:ref:`PROPERTY_USAGE_EDITOR <class_@GlobalScope_constant_PROPERTY_USAGE_EDITOR>`).

Tuy nhiên, đôi khi bạn có thể muốn làm cho một thuộc tính có thể được serialize nhưng không hiển thị thuộc tính đó trong editor để tránh các thay đổi ngoài ý muốn và làm giao diện trở nên rối mắt.

Để làm điều này, bạn có thể sử dụng :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`. Tính năng này có thể hữu ích cho các script :ref:`@tool <class_@GDScript_annotation_@tool>`. Ngoài ra, giá trị thuộc tính được sao chép khi :ref:`Resource.duplicate() <class_Resource_method_duplicate>` hoặc :ref:`Node.duplicate() <class_Node_method_duplicate>` được gọi, không giống như các biến không được export.

::

    var a # Not stored in the file, not displayed in the editor.
    @export_storage var b # Stored in the file, not displayed in the editor.
    @export var c: int # Stored in the file, displayed in the editor.

``@export_custom``
------------------

Nếu cần nhiều quyền kiểm soát hơn những gì các annotation ``@export`` tích hợp cung cấp, bạn có thể sử dụng ``@export_custom`` thay thế. Cách này cho phép định nghĩa bất kỳ property hint, hint string và usage flag nào, với cú pháp tương tự cú pháp editor sử dụng cho các node tích hợp.

Ví dụ: thuộc tính ``altitude`` này không có giới hạn phạm vi nhưng có hậu tố ``m`` (meter) được định nghĩa:

::

    @export_custom(PROPERTY_HINT_NONE, "suffix:m") var altitude: float

Thông thường, cách trên không khả thi với cú pháp ``@export_range`` tiêu chuẩn, vì cú pháp này yêu cầu định nghĩa một phạm vi.

Xem :ref:`tài liệu tham khảo về lớp <class_@GDScript_annotation_@export_custom>` để biết danh sách các tham số và giá trị được phép của chúng.

.. warning::

    Khi sử dụng ``@export_custom``, GDScript không thực hiện bất kỳ bước xác thực nào đối với cú pháp. Cú pháp không hợp lệ có thể gây ra hành vi không mong muốn trong inspector.

``@export_tool_button``
-----------------------

Nếu cần tạo một nút inspector có thể nhấp, bạn có thể sử dụng ``@export_tool_button``. Lệnh này export một thuộc tính ``Callable`` dưới dạng nút có thể nhấp. Khi nhấn nút, callable sẽ được gọi.

Bạn có thể chỉ định tên icon tùy chỉnh, tên này phải khớp với một trong các tên tệp icon trong thư mục `editor/icons <https://github.com/godotengine/godot/tree/master/editor/icons>`__ của repository mã nguồn Godot (phân biệt chữ hoa chữ thường). Bạn cũng có thể duyệt các icon của editor bằng website `icon của editor Godot <https://godot-editor-icons.github.io/>`__.

Ví dụ, nếu muốn sử dụng ``Node2D.svg`` từ thư mục đó, bạn phải chỉ định ``"Node2D"`` làm tham số thứ hai của ``@export_tool_button``. Hiện tại không thể sử dụng icon tùy chỉnh từ thư mục project; chỉ có thể sử dụng các icon tích hợp sẵn của editor.

Lệnh này export một nút có nhãn ``"Hello"`` và icon ``"Callable"`` (đây là giá trị mặc định nếu không chỉ định icon). Khi nhấn nút, nó sẽ in ``"Hello world!"``.

::

    @tool
    extends Node

    @export_tool_button("Hello", "Callable") var hello_action = hello

    func hello():
        print("Hello world!")

Thiết lập các biến được export từ một tool script
-------------------------------------------------

Khi thay đổi giá trị của một biến được export từ một script trong
:ref:`doc_gdscript_tool_mode`, giá trị trong inspector sẽ không được cập nhật tự động. Để cập nhật giá trị, hãy gọi
:ref:`notify_property_list_changed() <class_Object_method_notify_property_list_changed>` sau khi thiết lập giá trị của biến được export.

Đọc giá trị của biến được export quá sớm
----------------------------------------

Nếu đọc giá trị của một biến được export trong :ref:`_init() <class_Object_private_method__init>`, biến sẽ trả về giá trị mặc định được chỉ định trong export annotation thay vì giá trị đã được thiết lập trong inspector. Điều này xảy ra vì việc gán giá trị từ tệp scene/resource đã lưu diễn ra *sau khi* khởi tạo đối tượng; trước thời điểm đó, giá trị mặc định được sử dụng.

Để lấy giá trị đã được thiết lập trong inspector (và do đó đã được lưu trong tệp scene/resource), bạn cần đọc giá trị đó *sau khi* đối tượng được khởi tạo, chẳng hạn như trong
:ref:`Node._ready() <class_Node_private_method__ready>`. Bạn cũng có thể đọc giá trị trong một setter được định nghĩa trên thuộc tính được export, điều này hữu ích trong các custom resource nơi ``_ready()`` không khả dụng:

::

    # Set this property to 3 in the inspector.
    @export var exported_variable = 2:
        set(value):
            exported_variable = value
            print("Inspector-set value: ", exported_variable)

    func _init():
        print("Initial value: ", exported_variable)

Kết quả:

.. code-block:: none

    Initial value: 2
    Inspector-set value: 3

Export nâng cao
---------------

Không phải mọi kiểu export đều có thể được cung cấp ở cấp độ ngôn ngữ để tránh làm thiết kế trở nên phức tạp không cần thiết. Phần sau mô tả một số tính năng export phổ biến hơn hoặc ít phổ biến hơn, có thể được triển khai bằng API cấp thấp.

Trước khi đọc tiếp, bạn nên làm quen với cách các thuộc tính được xử lý và cách tùy chỉnh chúng bằng
:ref:`_set() <class_Object_private_method__set>`,
:ref:`_get() <class_Object_private_method__get>`, và
các phương thức :ref:`_get_property_list() <class_Object_private_method__get_property_list>` như được mô tả trong :ref:`doc_accessing_data_or_logic_from_object`.

.. seealso:: Để binding các thuộc tính bằng những phương thức trên trong C++, xem
             :ref:`doc_binding_properties_using_set_get_property_list`.

.. warning:: Script phải hoạt động ở chế độ ``@tool`` để các phương thức trên có thể hoạt động từ bên trong editor.
