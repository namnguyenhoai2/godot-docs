.. _doc_gdscript_exports:

Các thuộc tính được export của GDScript
=======================================

Trong Godot, các thành viên của lớp có thể được export. Điều này có nghĩa là giá trị của chúng được lưu cùng với resource (chẳng hạn như :ref:`scene <class_PackedScene>`) mà chúng được gắn vào, và được truyền đi khi sử dụng :ref:`RPC <doc_high_level_multiplayer_rpcs>`. Chúng cũng sẽ có thể chỉnh sửa trong trình chỉnh sửa thuộc tính. Việc export được thực hiện bằng annotation ``@export``.

::

    @export var number: int = 5

Trong ví dụ đó, giá trị ``5`` sẽ được lưu và hiển thị trong trình chỉnh sửa thuộc tính.

Một biến được export phải được khởi tạo bằng một biểu thức hằng hoặc có chỉ định kiểu trong biến. Một số annotation export có kiểu cụ thể và không cần biến phải được khai báo kiểu (xem phần *Ví dụ* bên dưới).

Một trong những lợi ích cơ bản của việc export biến thành viên là giúp chúng hiển thị và có thể chỉnh sửa trong editor. Bằng cách này, họa sĩ và nhà thiết kế game có thể sửa đổi các giá trị mà sau đó ảnh hưởng đến cách chương trình chạy. Vì mục đích này, một cú pháp export đặc biệt được cung cấp. Ngoài ra, có thể dùng :ref:`chú thích tài liệu <doc_gdscript_documentation_comments>` cho phần mô tả tooltip, hiển thị khi di chuột qua.

.. note::

    Việc export thuộc tính cũng có thể thực hiện trong các ngôn ngữ khác như C#. Cú pháp thay đổi tùy theo ngôn ngữ. Xem :ref:`doc_c_sharp_exports` để biết thông tin về export trong C#.

Cách dùng cơ bản
----------------

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

Ngay cả khi script không được thực thi trong editor, các thuộc tính được export vẫn có thể được chỉnh sửa. Tuy nhiên, getter và setter chỉ được sử dụng nếu script ở :ref:`doc_gdscript_tool_mode`.

Nhóm các export
---------------

Bạn có thể nhóm các thuộc tính được export trong Inspector bằng annotation :ref:`@export_group <class_@GDScript_annotation_@export_group>`. Mọi thuộc tính được export sau annotation này sẽ được thêm vào nhóm. Bắt đầu một nhóm mới hoặc dùng ``@export_group("")`` để thoát nhóm.

::

    @export_group("My Properties")
    @export var number = 3

Đối số thứ hai của annotation có thể được dùng để chỉ nhóm các thuộc tính có tiền tố được chỉ định.

Không thể lồng các nhóm; hãy dùng :ref:`@export_subgroup <class_@GDScript_annotation_@export_subgroup>` để tạo các nhóm con trong một nhóm.

::

    @export_subgroup("Extra Properties")
    @export var string = ""
    @export var flag = false

Bạn cũng có thể thay đổi tên danh mục chính hoặc tạo thêm các danh mục trong danh sách thuộc tính bằng annotation :ref:`@export_category <class_@GDScript_annotation_@export_category>`.

::

    @export_category("Main Category")
    @export var number = 3
    @export var string = ""

    @export_category("Extra Category")
    @export var flag = false

.. note::

    Danh sách thuộc tính được tổ chức dựa trên tính kế thừa lớp, và các danh mục mới sẽ phá vỡ cách tổ chức đó. Hãy sử dụng chúng cẩn thận, đặc biệt khi tạo dự án để dùng công khai.

String làm đường dẫn
--------------------

String làm đường dẫn đến tệp. Xem :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file var f

String làm đường dẫn đến thư mục. Xem :ref:`@export_dir <class_@GDScript_annotation_@export_dir>`.

::

    @export_dir var f

String làm đường dẫn đến tệp, với bộ lọc tùy chỉnh được cung cấp dưới dạng hint. Xem lại :ref:`@export_file <class_@GDScript_annotation_@export_file>`.

::

    @export_file("*.txt") var f

Bạn cũng có thể sử dụng đường dẫn trong hệ thống tệp toàn cục, nhưng chỉ trong các script ở chế độ tool.

String làm đường dẫn đến tệp PNG trong hệ thống tệp toàn cục. Xem :ref:`@export_global_file <class_@GDScript_annotation_@export_global_file>`.

::

    @export_global_file("*.png") var tool_image

String làm đường dẫn đến thư mục trong hệ thống tệp toàn cục. Xem :ref:`@export_global_dir <class_@GDScript_annotation_@export_global_dir>`.

::

    @export_global_dir var tool_dir

Annotation multiline yêu cầu editor hiển thị một trường nhập lớn để chỉnh sửa trên nhiều dòng. Xem :ref:`@export_multiline <class_@GDScript_annotation_@export_multiline>`.

::

    @export_multiline var text

String làm action đầu vào
-------------------------

String làm action đầu vào được định nghĩa trong input map của dự án.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME) var my_input

String làm action đầu vào được định nghĩa trong input map của dự án, kèm các giá trị dựng sẵn mặc định như ``ui_accept`` và ``ui_cancel``.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "show_builtin") var my_input

String làm action đầu vào được định nghĩa trong input map của dự án, kèm các giá trị tùy ý có thể nhập thủ công.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "loose_mode") var my_input

String làm action đầu vào được định nghĩa trong input map của dự án, kèm các giá trị dựng sẵn mặc định như ``ui_accept`` và ``ui_cancel``, cùng các giá trị tùy ý có thể nhập thủ công.

::

    @export_custom(PROPERTY_HINT_INPUT_NAME, "show_builtin,loose_mode") var my_input

Giới hạn phạm vi nhập trong editor
----------------------------------

Xem :ref:`@export_range <class_@GDScript_annotation_@export_range>` cho tất cả các trường hợp sau.

Cho phép các giá trị số nguyên từ 0 đến 20.

::

    @export_range(0, 20) var i

Cho phép các giá trị số nguyên từ -10 đến 20.

::

    @export_range(-10, 20) var j

Cho phép các số thực từ -10 đến 20 và snap giá trị thành bội số của 0.2.

::

    @export_range(-10, 20, 0.2) var k: float

Bạn có thể khiến giới hạn chỉ ảnh hưởng đến slider nếu thêm các hint ``"or_less"`` và/hoặc ``"or_greater"``. Nếu dùng một trong các hint này, người dùng vẫn có thể nhập bất kỳ giá trị nào hoặc kéo giá trị bằng chuột khi không dùng slider, kể cả khi giá trị nằm ngoài phạm vi đã chỉ định.

::

    @export_range(0, 100, 1, "or_less", "or_greater") var l: int

Hint ``"exp"`` có thể dùng để biến slider của một giá trị thành slider hàm mũ thay vì slider tuyến tính. Điều này có nghĩa là khi kéo slider sang phải, thay đổi sẽ nhanh dần khi kéo chuột. Điều này hữu ích để dễ chỉnh sửa các giá trị có thể rất nhỏ hoặc rất lớn, đổi lại sẽ kém trực quan hơn.

::

    @export_range(0, 100000, 0.01, "exp") var exponential: float

Đối với các giá trị được dùng để biểu thị hệ số easing, hãy dùng
:ref:`doc_gdscript_exports_floats_with_easing_hint` thay vào đó.

Hint ``"hide_slider"`` có thể dùng để ẩn thanh ngang xuất hiện bên dưới các thuộc tính ``float``, hoặc các mũi tên lên/xuống xuất hiện cạnh các thuộc tính ``int``:

::

    @export_range(0, 1000, 0.01, "hide_slider") var no_slider: float

Mặt khác, hint ``"prefer_slider"`` có thể dùng để hiển thị thanh ngang bên dưới các thuộc tính ``int`` thay cho các mũi tên lên/xuống:

::

    @export_range(0, 100, 1, "prefer_slider") var with_slider: int

Thêm hậu tố và xử lý độ/radian
------------------------------

Bạn cũng có thể định nghĩa hậu tố để giúp giá trị dễ hiểu hơn trong inspector. Ví dụ, để định nghĩa một giá trị mà người dùng cần cấu hình theo "mét" (``m``):

::

    @export_range(0, 100, 1, "suffix:m") var m: int

Đối với các góc được lưu bằng radian nhưng hiển thị cho người dùng dưới dạng độ, hãy dùng hint `"radians_as_degrees"`:

::

    @export_range(0, 360, 0.1, "radians_as_degrees") var angle: float

Cách này tự động chuyển đổi khi giá trị được hiển thị hoặc sửa đổi trong inspector, đồng thời hiển thị hậu tố độ (``°``). Cách tiếp cận này được dùng cho các thuộc tính `rotation` của chính Godot xuyên suốt editor.

Nếu góc được lưu bằng độ, hãy dùng hint `"degrees"` để hiển thị ký hiệu độ trong khi tắt chuyển đổi tự động từ độ sang radian khi giá trị được sửa đổi từ inspector.

Liên kết các giá trị vector với nhau
------------------------------------

Có thể liên kết các giá trị vector với nhau. Khi người dùng điều chỉnh một thành phần của vector, các thành phần khác sẽ tự động được điều chỉnh theo tỷ lệ. Ví dụ, điều này hữu ích để duy trì tỷ lệ khung hình của một sprite 2D khi điều chỉnh tỷ lệ của nó. Người dùng có thể tạm thời tắt tính năng này bằng cách nhấp vào biểu tượng liên kết ở bên phải thuộc tính.

::

    # Leave the hint string empty if you don't want to add a suffix.
    @export_custom(PROPERTY_HINT_LINK, "suffix:px") var vector2_linked: Vector2 = Vector2(16, 16)

Kết quả:

.. figure:: img/gdscript_exports_linked_vector.webp
   :align: center
   :alt: Thuộc tính Vector2i được liên kết với hậu tố "px"

   Thuộc tính Vector2i được liên kết với hậu tố "px"

:ref:`Gợi ý này <class_@GlobalScope_constant_PROPERTY_HINT_LINK>` có hiệu lực với Vector2, Vector2i, Vector3, Vector3i, Vector4 và Vector4i. Có thể sử dụng đồng thời với hậu tố thuộc tính, như trong ví dụ ở trên.

.. _doc_gdscript_exports_floats_with_easing_hint:

Float có gợi ý easing
---------------------

Hiển thị biểu diễn trực quan của hàm ``ease()`` khi chỉnh sửa. Xem :ref:`@export_exp_easing <class_@GDScript_annotation_@export_exp_easing>`.

::

    @export_exp_easing var transition_speed

Màu sắc
-------

Màu thông thường được cung cấp dưới dạng giá trị đỏ-lục-lam-alpha.

::

    @export var col: Color

Màu được cung cấp dưới dạng giá trị đỏ-lục-lam (alpha sẽ luôn là 1). Xem :ref:`@export_color_no_alpha <class_@GDScript_annotation_@export_color_no_alpha>`.

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

Vẫn có thể export NodePath như trong Godot 3.x, nếu bạn cần:

::

    @export var node_path: NodePath
    var node = get_node(node_path)

Nếu muốn giới hạn các kiểu node cho NodePath, bạn có thể sử dụng annotation
:ref:`@export_node_path <class_@GDScript_annotation_@export_node_path>`:

::

    @export_node_path("Button", "TouchScreenButton") var some_button

Resource
--------

::

    @export var resource: Resource

Sau đó, trong Inspector, bạn có thể kéo và thả một tệp resource từ dock FileSystem vào ô biến.

Tuy nhiên, việc mở danh sách thả xuống của Inspector có thể dẫn đến một danh sách cực dài các lớp có thể tạo. Vì vậy, nếu bạn chỉ định một phần mở rộng của Resource như:

::

    @export var resource: AnimationNode

Trình đơn thả xuống sẽ được giới hạn ở AnimationNode và mọi lớp dẫn xuất của nó.

.. note::

    Việc sử dụng các biến ``@export`` cho các đối tượng :ref:`Resource <class_Resource>` khiến chúng trở thành dependency của instance, nghĩa là mọi resource được tham chiếu bởi các biến ``@export`` đều được tải khi scene chứa script được tải. Nếu bạn muốn tham chiếu một
    đối tượng :ref:`Resource <class_Resource>` nhưng tải nó thủ công khi cần (ví dụ, đây thường là trường hợp của
    :ref:`PackedScenes <class_PackedScene>` chứa toàn bộ một level), hãy dùng ``@export_file`` hoặc ``@export_file_path`` thay thế.

.. _doc_gdscript_exports_exporting_bit_flags:

Export cờ bit
-------------

Xem :ref:`@export_flags <class_@GDScript_annotation_@export_flags>`.

Các số nguyên dùng làm cờ bit có thể lưu trữ nhiều giá trị ``true``/``false`` (boolean) trong một thuộc tính. Bằng cách dùng annotation ``@export_flags``, chúng có thể được thiết lập từ editor:

::

    # Set any of the given flags from the editor.
    @export_flags("Fire", "Water", "Earth", "Wind") var spell_elements = 0

Bạn phải cung cấp mô tả chuỗi cho mỗi cờ. Trong ví dụ này, ``Fire`` có giá trị 1, ``Water`` có giá trị 2, ``Earth`` có giá trị 4 và ``Wind`` tương ứng với giá trị 8. Thông thường, các hằng số nên được định nghĩa tương ứng (ví dụ: ``const ELEMENT_WIND = 8`` và tiếp tục như vậy).

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_flags("Self:4", "Allies:8", "Foes:16") var spell_targets = 0

Chỉ các giá trị lũy thừa của 2 mới hợp lệ làm tùy chọn cờ bit. Giá trị thấp nhất được phép là 1, vì 0 nghĩa là không có gì được chọn. Bạn cũng có thể thêm các tùy chọn là tổ hợp của các cờ khác:

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

Việc sử dụng cờ bit đòi hỏi một số hiểu biết về các phép toán bitwise. Nếu không chắc chắn, hãy dùng biến boolean thay thế.

Export enum
-----------

Xem :ref:`@export_enum <class_@GDScript_annotation_@export_enum>`.

Các thuộc tính có thể được export với gợi ý kiểu tham chiếu đến một enum để giới hạn giá trị của chúng trong các giá trị của phép liệt kê. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau thành "Thing 1", "Thing 2", "Another Thing". Giá trị sẽ được lưu dưới dạng số nguyên.

::

    enum NamedEnum {THING_1, THING_2, ANOTHER_THING = -1}
    @export var x: NamedEnum

Các thuộc tính số nguyên và chuỗi cũng có thể được giới hạn trong một danh sách giá trị cụ thể bằng annotation :ref:`@export_enum <class_@GDScript_annotation_@export_enum>`. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau thành Warrior, Magician, Thief. Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn được chọn (tức là ``0``, ``1``, hoặc ``2``).

::

    @export_enum("Warrior", "Magician", "Thief") var character_class: int

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_enum("Slow:30", "Average:60", "Very Fast:200") var character_speed: int

Nếu kiểu là String, giá trị sẽ được lưu dưới dạng chuỗi.

::

    @export_enum("Rebecca", "Mary", "Leah") var character_name: String

Nếu muốn đặt giá trị ban đầu, bạn phải chỉ định tường minh:

::

    @export_enum("Rebecca", "Mary", "Leah") var character_name: String = "Rebecca"

Export mảng
-----------

Mảng được export có thể có giá trị khởi tạo, nhưng chúng phải là biểu thức hằng.

Nếu mảng được export chỉ định một kiểu kế thừa từ Resource, các giá trị mảng có thể được thiết lập trong Inspector bằng cách kéo và thả đồng thời nhiều tệp từ dock FileSystem.

Giá trị mặc định **phải** là một biểu thức hằng.

::

    @export var a = [1, 2, 3]

.. UPDATE: Not supported yet. When nested typed arrays are supported, update
.. the example.

Mảng được export có thể chỉ định kiểu (sử dụng các gợi ý giống như trước).

::

    @export var ints: Array[int] = [1, 2, 3]

    # Nested typed arrays such as `Array[Array[float]]` are not supported yet.
    @export var two_dimensional: Array[Array] = [[1.0, 2.0], [3.0, 4.0]]

Bạn có thể bỏ qua giá trị mặc định, nhưng khi đó nó sẽ là ``null`` nếu chưa được gán.

::

    @export var b: Array
    @export var scenes: Array[PackedScene]

Các mảng có kiểu được chỉ định kế thừa từ resource có thể được thiết lập bằng cách kéo và thả nhiều tệp từ dock FileSystem.

::

    @export var textures: Array[Texture] = []
    @export var scenes: Array[PackedScene] = []

Mảng packed cũng hoạt động, nhưng chỉ khi được khởi tạo rỗng:

::

    @export var vector3s = PackedVector3Array()
    @export var strings = PackedStringArray()

Các biến thể export khác cũng có thể được dùng khi export mảng:

::

    @export_range(-360, 360, 0.001, "degrees") var laser_angles: Array[float] = []
    @export_file("*.json") var skill_trees: Array[String] = []
    @export_color_no_alpha var hair_colors = PackedColorArray()
    @export_enum("Espresso", "Mocha", "Latte", "Capuccino") var barista_suggestions: Array[String] = []

``@export_storage``
-------------------

Xem :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`.

Theo mặc định, export một thuộc tính có hai tác dụng:

1. lưu thuộc tính trong tệp scene/resource (:ref:`PROPERTY_USAGE_STORAGE <class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`);
2. thêm một trường vào Inspector (:ref:`PROPERTY_USAGE_EDITOR <class_@GlobalScope_constant_PROPERTY_USAGE_EDITOR>`).

Tuy nhiên, đôi khi bạn có thể muốn biến một thuộc tính thành có thể tuần tự hóa, nhưng không hiển thị nó trong editor để ngăn các thay đổi không chủ ý và tránh làm giao diện lộn xộn.

Để làm điều này, bạn có thể dùng :ref:`@export_storage <class_@GDScript_annotation_@export_storage>`. Điều này có thể hữu ích cho các script :ref:`@tool <class_@GDScript_annotation_@tool>`. Giá trị thuộc tính cũng được sao chép khi :ref:`Resource.duplicate() <class_Resource_method_duplicate>` hoặc :ref:`Node.duplicate() <class_Node_method_duplicate>` được gọi, không giống các biến không được export.

::

    var a # Not stored in the file, not displayed in the editor.
    @export_storage var b # Stored in the file, not displayed in the editor.
    @export var c: int # Stored in the file, displayed in the editor.

``@export_custom``
------------------

Nếu cần kiểm soát nhiều hơn so với những gì được cung cấp qua các annotation ``@export`` tích hợp, bạn có thể dùng ``@export_custom`` thay thế. Điều này cho phép định nghĩa bất kỳ gợi ý thuộc tính, chuỗi gợi ý và cờ sử dụng nào, với cú pháp tương tự như cú pháp editor dùng cho các node tích hợp.

Ví dụ, điều này export thuộc tính ``altitude`` mà không có giới hạn phạm vi nhưng có hậu tố ``m`` (mét) được xác định:

::

    @export_custom(PROPERTY_HINT_NONE, "suffix:m") var altitude: float

Thông thường, không thể thực hiện điều trên bằng cú pháp ``@export_range`` tiêu chuẩn, vì nó yêu cầu xác định một phạm vi.

Xem :ref:`tham chiếu lớp <class_@GDScript_annotation_@export_custom>` để biết danh sách các tham số và giá trị được phép của chúng.

.. warning::

    Khi sử dụng ``@export_custom``, GDScript không thực hiện bất kỳ kiểm tra nào đối với cú pháp. Cú pháp không hợp lệ có thể dẫn đến hành vi không mong đợi trong inspector.

``@export_tool_button``
-----------------------

Nếu cần tạo một nút inspector có thể nhấp, bạn có thể sử dụng ``@export_tool_button``. Thao tác này export một thuộc tính ``Callable`` dưới dạng nút có thể nhấp. Khi nhấn nút, callable sẽ được gọi.

Bạn có thể chỉ định tên icon tùy chỉnh; tên này phải khớp với một trong các tên tệp icon trong thư mục `editor/icons <https://github.com/godotengine/godot/tree/master/editor/icons>`__ của source repository Godot (phân biệt chữ hoa chữ thường). Bạn cũng có thể duyệt các icon editor bằng trang web `icon editor Godot <https://godot-editor-icons.github.io/>`__.

Ví dụ, nếu muốn sử dụng ``Node2D.svg`` từ thư mục đó, bạn phải chỉ định ``"Node2D"`` làm tham số thứ hai của ``@export_tool_button``. Hiện tại không thể sử dụng icon tùy chỉnh từ thư mục project; chỉ có thể dùng các icon editor tích hợp sẵn.

Thao tác này export một nút có nhãn ``"Hello"`` và icon ``"Callable"`` (là mặc định nếu không chỉ định icon). Khi nhấn nút, nó sẽ in ra ``"Hello world!"``.

::

    @tool
    extends Node

    @export_tool_button("Hello", "Callable") var hello_action = hello

    func hello():
        print("Hello world!")

Thiết lập biến đã export từ tool script
---------------------------------------

Khi thay đổi giá trị của một biến đã export từ script trong
:ref:`doc_gdscript_tool_mode`, giá trị trong inspector sẽ không được cập nhật tự động. Để cập nhật, hãy gọi
:ref:`notify_property_list_changed() <class_Object_method_notify_property_list_changed>` sau khi thiết lập giá trị của biến đã export.

Đọc sớm giá trị của biến đã export
----------------------------------

Nếu bạn đọc giá trị của một biến đã export trong :ref:`_init() <class_Object_private_method__init>`, nó sẽ trả về giá trị mặc định được chỉ định trong annotation export thay vì giá trị đã được thiết lập trong inspector. Điều này xảy ra vì việc gán giá trị từ tệp scene/resource đã lưu diễn ra *sau* khi khởi tạo đối tượng; cho đến lúc đó, giá trị mặc định được sử dụng.

Để lấy giá trị đã được thiết lập trong inspector (và do đó được lưu trong tệp scene/resource), bạn cần đọc giá trị đó *sau* khi đối tượng được tạo, chẳng hạn như trong
:ref:`Node._ready() <class_Node_private_method__ready>`. Bạn cũng có thể đọc giá trị trong một setter được xác định trên thuộc tính đã export, điều này hữu ích trong các resource tùy chỉnh nơi ``_ready()`` không khả dụng:

::

    # Set this property to 3 in the inspector.
    @export var exported_variable = 2:
        set(value):
            exported_variable = value
            print("Inspector-set value: ", exported_variable)

    func _init():
        print("Initial value: ", exported_variable)

Kết quả là:

.. code-block:: none

    Initial value: 2
    Inspector-set value: 3

Export nâng cao
---------------

Không phải mọi kiểu export đều có thể được cung cấp ở cấp độ ngôn ngữ để tránh độ phức tạp không cần thiết trong thiết kế. Phần sau mô tả một số tính năng export ít nhiều phổ biến có thể được triển khai bằng API cấp thấp.

Trước khi đọc tiếp, bạn nên làm quen với cách các thuộc tính được xử lý và cách chúng có thể được tùy chỉnh bằng
:ref:`_set() <class_Object_private_method__set>`,
:ref:`_get() <class_Object_private_method__get>`, và
các phương thức :ref:`_get_property_list() <class_Object_private_method__get_property_list>` như được mô tả trong :ref:`doc_accessing_data_or_logic_from_object`.

.. seealso:: Để liên kết thuộc tính bằng các phương thức trên trong C++, xem
             :ref:`doc_binding_properties_using_set_get_property_list`.

.. warning:: Script phải hoạt động ở chế độ ``@tool`` để các phương thức trên có thể hoạt động từ bên trong editor.
