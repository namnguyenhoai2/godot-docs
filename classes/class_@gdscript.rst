:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gdscript/doc_classes/@GDScript.xml.

.. _class_@GDScript:

@GDScript
=========

Các hằng số, hàm và annotation tích hợp sẵn của GDScript.

.. rst-class:: classref-introduction-group

Mô tả
-----

Danh sách các hàm tiện ích và annotation có thể truy cập từ mọi script được viết bằng GDScript.

Để xem danh sách các hàm và hằng số toàn cục có thể truy cập trong mọi ngôn ngữ scripting, hãy xem :ref:`@GlobalScope<class_@GlobalScope>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`GDScript exports <../tutorials/scripting/gdscript/gdscript_exports>`

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`           | :ref:`Color8<class_@GDScript_method_Color8>`\ (\ r8\: :ref:`int<class_int>`, g8\: :ref:`int<class_int>`, b8\: :ref:`int<class_int>`, a8\: :ref:`int<class_int>` = 255\ ) |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`assert<class_@GDScript_method_assert>`\ (\ condition\: :ref:`bool<class_bool>`, message\: :ref:`String<class_String>` = ""\ )                                      |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`         | :ref:`char<class_@GDScript_method_char>`\ (\ code\: :ref:`int<class_int>`\ )                                                                                             |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`convert<class_@GDScript_method_convert>`\ (\ what\: :ref:`Variant<class_Variant>`, type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`\ )                   |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`         | :ref:`dict_to_inst<class_@GDScript_method_dict_to_inst>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ )                                                         |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`get_stack<class_@GDScript_method_get_stack>`\ (\ )                                                                                                                 |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`inst_to_dict<class_@GDScript_method_inst_to_dict>`\ (\ instance\: :ref:`Object<class_Object>`\ )                                                                   |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_instance_of<class_@GDScript_method_is_instance_of>`\ (\ value\: :ref:`Variant<class_Variant>`, type\: :ref:`Variant<class_Variant>`\ )                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`len<class_@GDScript_method_len>`\ (\ var\: :ref:`Variant<class_Variant>`\ )                                                                                        |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>`     | :ref:`load<class_@GDScript_method_load>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                       |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`ord<class_@GDScript_method_ord>`\ (\ char\: :ref:`String<class_String>`\ )                                                                                         |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>`     | :ref:`preload<class_@GDScript_method_preload>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                 |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`print_debug<class_@GDScript_method_print_debug>`\ (\ ...\ ) |vararg|                                                                                               |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`print_stack<class_@GDScript_method_print_stack>`\ (\ )                                                                                                             |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`range<class_@GDScript_method_range>`\ (\ ...\ ) |vararg|                                                                                                           |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`type_exists<class_@GDScript_method_type_exists>`\ (\ type\: :ref:`StringName<class_StringName>`\ )                                                                 |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_@GDScript_constant_PI:

.. rst-class:: classref-constant

**PI** = ``3.14159265358979`` :ref:`🔗<class_@GDScript_constant_PI>`

Hằng số biểu thị số lần đường kính của một hình tròn nằm trên chu vi của nó. Giá trị này tương đương với ``TAU / 2``, hoặc 180 độ khi xoay.

.. _class_@GDScript_constant_TAU:

.. rst-class:: classref-constant

**TAU** = ``6.28318530717959`` :ref:`🔗<class_@GDScript_constant_TAU>`

Hằng số hình tròn, tức chu vi của đường tròn đơn vị tính theo radian. Giá trị này tương đương với ``PI * 2``, hoặc 360 độ khi xoay.

.. _class_@GDScript_constant_INF:

.. rst-class:: classref-constant

**INF** = ``inf`` :ref:`🔗<class_@GDScript_constant_INF>`

Vô cực dương dạng số thực. Đây là kết quả của phép chia số thực khi số chia là ``0.0``. Đối với vô cực âm, hãy sử dụng ``-INF``. Chia cho ``-0.0`` sẽ cho kết quả là vô cực âm nếu tử số là số dương, vì vậy chia cho ``0.0`` không giống với chia cho ``-0.0`` (mặc dù ``0.0 == -0.0`` trả về ``true``).

\ **Cảnh báo:** Vô cực số chỉ là một khái niệm đối với các số thực và không có giá trị tương đương đối với số nguyên. Chia một số nguyên cho ``0`` sẽ không cho kết quả :ref:`INF<class_@GDScript_constant_INF>` mà thay vào đó sẽ gây ra lỗi khi chạy.

.. _class_@GDScript_constant_NAN:

.. rst-class:: classref-constant

**NAN** = ``nan`` :ref:`🔗<class_@GDScript_constant_NAN>`

"Not a Number", một giá trị số thực không hợp lệ. Giá trị này được trả về bởi một số phép toán không hợp lệ, chẳng hạn như chia số thực ``0.0`` cho ``0.0``.

\ :ref:`NAN<class_@GDScript_constant_NAN>` có các thuộc tính đặc biệt, trong đó ``!=`` luôn trả về ``true``, còn các toán tử so sánh khác luôn trả về ``false``. Điều này vẫn đúng ngay cả khi so sánh với chính nó (``NAN == NAN`` trả về ``false`` và ``NAN != NAN`` trả về ``true``). Vì vậy, bạn phải sử dụng :ref:`@GlobalScope.is_nan()<class_@GlobalScope_method_is_nan>` để kiểm tra xem một số có bằng :ref:`NAN<class_@GDScript_constant_NAN>` hay không.

\ **Cảnh báo:** "Not a Number" chỉ là một khái niệm đối với các số thực và không có giá trị tương đương đối với số nguyên. Chia một số nguyên ``0`` cho ``0`` sẽ không cho kết quả :ref:`NAN<class_@GDScript_constant_NAN>` mà thay vào đó sẽ gây ra lỗi khi chạy.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Annotations
-----------

.. _class_@GDScript_annotation_@abstract:

.. rst-class:: classref-annotation

**@abstract**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@abstract>`

Đánh dấu một class hoặc một method là abstract.

Một abstract class là class không thể được khởi tạo trực tiếp. Thay vào đó, class này được dùng để các class khác kế thừa. Việc cố khởi tạo một abstract class sẽ gây ra lỗi.

Một abstract method là method không có phần triển khai. Do đó, sau phần khai báo hàm phải có một dòng mới hoặc dấu chấm phẩy. Điều này xác định một contract mà các class kế thừa phải tuân theo, vì method signature phải tương thích khi override.

Các class kế thừa phải cung cấp phần triển khai cho tất cả abstract method, hoặc class kế thừa phải được đánh dấu là abstract. Nếu một class có ít nhất một abstract method (của chính nó hoặc một method kế thừa chưa được triển khai), thì class đó cũng phải được đánh dấu là abstract. Tuy nhiên, điều ngược lại không đúng: một abstract class có thể không có abstract method nào.

::

    @abstract class Shape:
        @abstract func draw()

    class Circle extends Shape:
        func draw():
            print("Drawing a circle.")

    class Square extends Shape:
        func draw():
            print("Drawing a square.")

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export:

.. rst-class:: classref-annotation

**@export**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export>`

Đánh dấu property tiếp theo là exported (có thể chỉnh sửa trong dock Inspector và được lưu vào đĩa). Để kiểm soát type của exported property, hãy sử dụng ký hiệu type hint.

::

    extends Node

    enum Direction {LEFT, RIGHT, UP, DOWN}

    # Các built-in type.
    @export var string = ""
    @export var int_number = 5
    @export var float_number: float = 5

    # Enum.
    @export var type: Variant.Type
    @export var format: Image.Format
    @export var direction: Direction

    # Resource.
    @export var image: Image
    @export var custom_resource: CustomResource

    # Node.
    @export var node: Node
    @export var custom_node: CustomNode

    # Typed array.
    @export var int_array: Array[int]
    @export var direction_array: Array[Direction]
    @export var image_array: Array[Image]
    @export var node_array: Array[Node]

\ **Lưu ý:** Custom resource và node nên được đăng ký thành global class bằng ``class_name``, vì Inspector hiện chỉ hỗ trợ global class. Nếu không, một type kém cụ thể hơn sẽ được export.

\ **Lưu ý:** Việc export Node chỉ được hỗ trợ trong các class dẫn xuất từ :ref:`Node<class_Node>` và có một số hạn chế khác.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_category:

.. rst-class:: classref-annotation

**@export_category**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_annotation_@export_category>`

Định nghĩa một category mới cho các property được export tiếp theo. Điều này giúp sắp xếp các property trong dock Inspector.

Xem thêm :ref:`@GlobalScope.PROPERTY_USAGE_CATEGORY<class_@GlobalScope_constant_PROPERTY_USAGE_CATEGORY>`.

::

    @export_category("Statistics")
    @export var hp = 30
    @export var speed = 1.25

\ **Lưu ý:** Các category trong danh sách của dock Inspector thường phân chia các property đến từ những class khác nhau (Node, Node2D, Sprite, v.v.). Để dễ hiểu hơn, nên sử dụng :ref:`@export_group<class_@GDScript_annotation_@export_group>` và :ref:`@export_subgroup<class_@GDScript_annotation_@export_subgroup>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_color_no_alpha:

.. rst-class:: classref-annotation

**@export_color_no_alpha**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_color_no_alpha>`

Export a :ref:`Color<class_Color>`, :ref:`Array<class_Array>`\ \[:ref:`Color<class_Color>`\ \], or :ref:`PackedColorArray<class_PackedColorArray>` property without allowing its transparency (:ref:`Color.a<class_Color_property_a>`) to be edited.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_COLOR_NO_ALPHA<class_@GlobalScope_constant_PROPERTY_HINT_COLOR_NO_ALPHA>`.

::

    @export_color_no_alpha var dye_color: Color
    @export_color_no_alpha var dye_colors: Array[Color]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_custom:

.. rst-class:: classref-annotation

**@export_custom**\ (\ hint\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>`, hint_string\: :ref:`String<class_String>`, usage\: |bitfield|\[:ref:`PropertyUsageFlags<enum_@GlobalScope_PropertyUsageFlags>`\] = 6\ ) :ref:`🔗<class_@GDScript_annotation_@export_custom>`

Cho phép bạn đặt hint, hint string và usage flag tùy chỉnh cho exported property. Lưu ý rằng GDScript không thực hiện validation; các tham số sẽ được truyền thẳng cho editor.

::

    @export_custom(PROPERTY_HINT_NONE, "suffix:m") var suffix: Vector3

\ **Lưu ý:** Bất kể giá trị ``usage`` là gì, flag :ref:`@GlobalScope.PROPERTY_USAGE_SCRIPT_VARIABLE<class_@GlobalScope_constant_PROPERTY_USAGE_SCRIPT_VARIABLE>` luôn được thêm vào, giống như với mọi biến script được khai báo tường minh.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_dir:

.. rst-class:: classref-annotation

**@export_dir**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_dir>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], or :ref:`PackedStringArray<class_PackedStringArray>` property as a path to a directory. The path will be limited to the project folder and its subfolders. See :ref:`@export_global_dir<class_@GDScript_annotation_@export_global_dir>` to allow picking from the entire filesystem.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_DIR<class_@GlobalScope_constant_PROPERTY_HINT_DIR>`.

::

    @export_dir var sprite_folder_path: String
    @export_dir var sprite_folder_paths: Array[String]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_enum:

.. rst-class:: classref-annotation

**@export_enum**\ (\ names\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_enum>`

Export an :ref:`int<class_int>`, :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`int<class_int>`\ \], :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], :ref:`PackedByteArray<class_PackedByteArray>`, :ref:`PackedInt32Array<class_PackedInt32Array>`, :ref:`PackedInt64Array<class_PackedInt64Array>`, or :ref:`PackedStringArray<class_PackedStringArray>` property as an enumerated list of options (or an array of options). If the property is an :ref:`int<class_int>`, then the index of the value is stored, in the same order the values are provided. You can add explicit values using a colon. If the property is a :ref:`String<class_String>`, then the value is stored.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_ENUM<class_@GlobalScope_constant_PROPERTY_HINT_ENUM>`.

::

    @export_enum("Warrior", "Magician", "Thief") var character_class: int
    @export_enum("Slow:30", "Average:60", "Very Fast:200") var character_speed: int
    @export_enum("Rebecca", "Mary", "Leah") var character_name: String

    @export_enum("Sword", "Spear", "Mace") var character_items: Array[int]
    @export_enum("double_jump", "climb", "dash") var character_skills: Array[String]

Nếu muốn đặt giá trị ban đầu, bạn phải chỉ định tường minh:

::

    @export_enum("Rebecca", "Mary", "Leah") var character_name: String = "Rebecca"

Nếu muốn sử dụng enum GDScript có tên, hãy sử dụng :ref:`@export<class_@GDScript_annotation_@export>` thay thế:

::

    enum CharacterName {REBECCA, MARY, LEAH}
    @export var character_name: CharacterName

    enum CharacterItem {SWORD, SPEAR, MACE}
    @export var character_items: Array[CharacterItem]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_exp_easing:

.. rst-class:: classref-annotation

**@export_exp_easing**\ (\ hints\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_exp_easing>`

Export một property dạng số thực với widget easing editor. Có thể cung cấp thêm hint để điều chỉnh cách widget hoạt động. ``"attenuation"`` lật đường cong, giúp chỉnh sửa các property attenuation trực quan hơn. ``"positive_only"`` giới hạn các giá trị chỉ lớn hơn hoặc bằng không.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_EXP_EASING<class_@GlobalScope_constant_PROPERTY_HINT_EXP_EASING>`.

::

    @export_exp_easing var transition_speed
    @export_exp_easing("attenuation") var fading_attenuation
    @export_exp_easing("positive_only") var effect_power
    @export_exp_easing var speeds: Array[float]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_file:

.. rst-class:: classref-annotation

**@export_file**\ (\ filter\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_file>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], or :ref:`PackedStringArray<class_PackedStringArray>` property as a path to a file. The path will be limited to the project folder and its subfolders. See :ref:`@export_global_file<class_@GDScript_annotation_@export_global_file>` to allow picking from the entire filesystem.

Nếu cung cấp ``filter``, chỉ các tệp khớp mới có thể được chọn.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_FILE<class_@GlobalScope_constant_PROPERTY_HINT_FILE>`.

::

    @export_file var sound_effect_path: String
    @export_file("*.txt") var notes_path: String
    @export_file var level_paths: Array[String]

\ **Lưu ý:** Tệp sẽ được lưu và tham chiếu dưới dạng UID nếu có. Điều này đảm bảo tham chiếu vẫn hợp lệ ngay cả khi tệp được di chuyển. Bạn có thể sử dụng các method của :ref:`ResourceUID<class_ResourceUID>` để chuyển đổi UID thành đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_file_path:

.. rst-class:: classref-annotation

**@export_file_path**\ (\ filter\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_file_path>`

Tương tự :ref:`@export_file<class_@GDScript_annotation_@export_file>`, ngoại trừ việc tệp sẽ được lưu dưới dạng đường dẫn thô. Điều này có nghĩa là đường dẫn có thể trở nên không hợp lệ khi tệp được di chuyển. Nếu bạn đang export đường dẫn :ref:`Resource<class_Resource>`, hãy cân nhắc sử dụng :ref:`@export_file<class_@GDScript_annotation_@export_file>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags:

.. rst-class:: classref-annotation

**@export_flags**\ (\ names\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_flags>`

Export một property kiểu integer thành trường bit flag. Điều này cho phép lưu trữ nhiều giá trị "đã chọn" hoặc ``true`` trong một property và thuận tiện chọn chúng từ dock Inspector.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_FLAGS<class_@GlobalScope_constant_PROPERTY_HINT_FLAGS>`.

::

    @export_flags("Fire", "Water", "Earth", "Wind") var spell_elements = 0

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

::

    @export_flags("Self:4", "Allies:8", "Foes:16") var spell_targets = 0

Bạn cũng có thể kết hợp nhiều flag:

::

    @export_flags("Self:4", "Allies:8", "Self and Allies:12", "Foes:16")
    var spell_targets = 0

\ **Lưu ý:** Giá trị cờ phải ít nhất là ``1`` và nhiều nhất là ``2 ** 32 - 1``.

\ **Lưu ý:** Không giống :ref:`@export_enum<class_@GDScript_annotation_@export_enum>`, giá trị tường minh trước đó không được tính đến. Trong ví dụ sau, A là 16, B là 2, C là 4.

::

    @export_flags("A:16", "B", "C") var x

You can also use the annotation on :ref:`Array<class_Array>`\ \[:ref:`int<class_int>`\ \], :ref:`PackedByteArray<class_PackedByteArray>`, :ref:`PackedInt32Array<class_PackedInt32Array>`, and :ref:`PackedInt64Array<class_PackedInt64Array>`\

::

    @export_flags("Fire", "Water", "Earth", "Wind") var phase_elements: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_2d_navigation:

.. rst-class:: classref-annotation

**@export_flags_2d_navigation**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_2d_navigation>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer điều hướng 2D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/2d_navigation/layer_1<class_ProjectSettings_property_layer_names/2d_navigation/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_2D_NAVIGATION<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_2D_NAVIGATION>`.

::

    @export_flags_2d_navigation var navigation_layers: int
    @export_flags_2d_navigation var navigation_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_2d_physics:

.. rst-class:: classref-annotation

**@export_flags_2d_physics**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_2d_physics>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer physics 2D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/2d_physics/layer_1<class_ProjectSettings_property_layer_names/2d_physics/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_2D_PHYSICS<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_2D_PHYSICS>`.

::

    @export_flags_2d_physics var physics_layers: int
    @export_flags_2d_physics var physics_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_2d_render:

.. rst-class:: classref-annotation

**@export_flags_2d_render**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_2d_render>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer render 2D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/2d_render/layer_1<class_ProjectSettings_property_layer_names/2d_render/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_2D_RENDER<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_2D_RENDER>`.

::

    @export_flags_2d_render var render_layers: int
    @export_flags_2d_render var render_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_3d_navigation:

.. rst-class:: classref-annotation

**@export_flags_3d_navigation**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_3d_navigation>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer điều hướng 3D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/3d_navigation/layer_1<class_ProjectSettings_property_layer_names/3d_navigation/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_3D_NAVIGATION<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_3D_NAVIGATION>`.

::

    @export_flags_3d_navigation var navigation_layers: int
    @export_flags_3d_navigation var navigation_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_3d_physics:

.. rst-class:: classref-annotation

**@export_flags_3d_physics**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_3d_physics>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer physics 3D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/3d_physics/layer_1<class_ProjectSettings_property_layer_names/3d_physics/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_3D_PHYSICS<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_3D_PHYSICS>`.

::

    @export_flags_3d_physics var physics_layers: int
    @export_flags_3d_physics var physics_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_3d_render:

.. rst-class:: classref-annotation

**@export_flags_3d_render**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_3d_render>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer render 3D. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/3d_render/layer_1<class_ProjectSettings_property_layer_names/3d_render/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_3D_RENDER<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_3D_RENDER>`.

::

    @export_flags_3d_render var render_layers: int
    @export_flags_3d_render var render_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_flags_avoidance:

.. rst-class:: classref-annotation

**@export_flags_avoidance**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_flags_avoidance>`

Export một thuộc tính integer dưới dạng trường bit flag cho các layer tránh va chạm khi điều hướng. Widget trong dock Inspector sẽ sử dụng các tên layer được định nghĩa trong :ref:`ProjectSettings.layer_names/avoidance/layer_1<class_ProjectSettings_property_layer_names/avoidance/layer_1>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_LAYERS_AVOIDANCE<class_@GlobalScope_constant_PROPERTY_HINT_LAYERS_AVOIDANCE>`.

::

    @export_flags_avoidance var avoidance_layers: int
    @export_flags_avoidance var avoidance_layers_array: Array[int]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_global_dir:

.. rst-class:: classref-annotation

**@export_global_dir**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_global_dir>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], or :ref:`PackedStringArray<class_PackedStringArray>` property as an absolute path to a directory. The path can be picked from the entire filesystem. See :ref:`@export_dir<class_@GDScript_annotation_@export_dir>` to limit it to the project folder and its subfolders.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_GLOBAL_DIR<class_@GlobalScope_constant_PROPERTY_HINT_GLOBAL_DIR>`.

::

    @export_global_dir var sprite_folder_path: String
    @export_global_dir var sprite_folder_paths: Array[String]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_global_file:

.. rst-class:: classref-annotation

**@export_global_file**\ (\ filter\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_global_file>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], or :ref:`PackedStringArray<class_PackedStringArray>` property as an absolute path to a file. The path can be picked from the entire filesystem. See :ref:`@export_file<class_@GDScript_annotation_@export_file>` to limit it to the project folder and its subfolders.

Nếu cung cấp ``filter``, chỉ các file khớp mới có thể được chọn.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_GLOBAL_FILE<class_@GlobalScope_constant_PROPERTY_HINT_GLOBAL_FILE>`.

::

    @export_global_file var sound_effect_path: String
    @export_global_file("*.txt") var notes_path: String
    @export_global_file var multiple_paths: Array[String]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_group:

.. rst-class:: classref-annotation

**@export_group**\ (\ name\: :ref:`String<class_String>`, prefix\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_@GDScript_annotation_@export_group>`

Xác định một group mới cho các thuộc tính được export tiếp theo. Điều này giúp sắp xếp các thuộc tính trong dock Inspector. Có thể thêm group với một ``prefix`` tùy chọn, khiến group chỉ xét các thuộc tính có prefix này. Việc nhóm sẽ dừng ở thuộc tính đầu tiên không có prefix. Prefix cũng được xóa khỏi tên thuộc tính trong dock Inspector.

Nếu không cung cấp ``prefix``, mọi thuộc tính tiếp theo sẽ được thêm vào group. Group kết thúc khi group hoặc category tiếp theo được xác định. Bạn cũng có thể buộc kết thúc một group bằng cách sử dụng annotation này với các tham số là chuỗi rỗng, ``@export_group("", "")``.

Không thể lồng các group, hãy sử dụng :ref:`@export_subgroup<class_@GDScript_annotation_@export_subgroup>` để thêm subgroup bên trong group.

Xem thêm :ref:`@GlobalScope.PROPERTY_USAGE_GROUP<class_@GlobalScope_constant_PROPERTY_USAGE_GROUP>`.

::

    @export_group("Racer Properties")
    @export var nickname = "Nick"
    @export var age = 26

    @export_group("Car Properties", "car_")
    @export var car_label = "Speedy"
    @export var car_number = 3

    @export_group("", "")
    @export var ungrouped_number = 3

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_multiline:

.. rst-class:: classref-annotation

**@export_multiline**\ (\ hint\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_multiline>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], :ref:`PackedStringArray<class_PackedStringArray>`, :ref:`Dictionary<class_Dictionary>` or :ref:`Array<class_Array>`\ \[:ref:`Dictionary<class_Dictionary>`\ \] property with a large :ref:`TextEdit<class_TextEdit>` widget instead of a :ref:`LineEdit<class_LineEdit>`. This adds support for multiline content and makes it easier to edit large amount of text stored in the property.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_MULTILINE_TEXT<class_@GlobalScope_constant_PROPERTY_HINT_MULTILINE_TEXT>`.

::

    @export_multiline var character_biography
    @export_multiline var npc_dialogs: Array[String]
    @export_multiline("monospace", "no_wrap") var favorite_ascii_art: String

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_node_path:

.. rst-class:: classref-annotation

**@export_node_path**\ (\ type\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_node_path>`

Export a :ref:`NodePath<class_NodePath>` or :ref:`Array<class_Array>`\ \[:ref:`NodePath<class_NodePath>`\ \] property with a filter for allowed node types.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_NODE_PATH_VALID_TYPES<class_@GlobalScope_constant_PROPERTY_HINT_NODE_PATH_VALID_TYPES>`.

::

    @export_node_path("Button", "TouchScreenButton") var some_button
    @export_node_path("Button", "TouchScreenButton") var many_buttons: Array[NodePath]

\ **Lưu ý:** Type phải là một native class hoặc một script được đăng ký toàn cục (sử dụng keyword ``class_name``) kế thừa :ref:`Node<class_Node>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_placeholder:

.. rst-class:: classref-annotation

**@export_placeholder**\ (\ placeholder\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_annotation_@export_placeholder>`

Export a :ref:`String<class_String>`, :ref:`Array<class_Array>`\ \[:ref:`String<class_String>`\ \], or :ref:`PackedStringArray<class_PackedStringArray>` property with a placeholder text displayed in the editor widget when no value is present.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_PLACEHOLDER_TEXT<class_@GlobalScope_constant_PROPERTY_HINT_PLACEHOLDER_TEXT>`.

::

    @export_placeholder("Name in lowercase") var character_id: String
    @export_placeholder("Name in lowercase") var friend_ids: Array[String]

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_range:

.. rst-class:: classref-annotation

**@export_range**\ (\ min\: :ref:`float<class_float>`, max\: :ref:`float<class_float>`, step\: :ref:`float<class_float>` = 1.0, extra_hints\: :ref:`String<class_String>` = "", ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@export_range>`

Export an :ref:`int<class_int>`, :ref:`float<class_float>`, :ref:`Array<class_Array>`\ \[:ref:`int<class_int>`\ \], :ref:`Array<class_Array>`\ \[:ref:`float<class_float>`\ \], :ref:`PackedByteArray<class_PackedByteArray>`, :ref:`PackedInt32Array<class_PackedInt32Array>`, :ref:`PackedInt64Array<class_PackedInt64Array>`, :ref:`PackedFloat32Array<class_PackedFloat32Array>`, or :ref:`PackedFloat64Array<class_PackedFloat64Array>` property as a range value. The range must be defined by ``min`` and ``max``, as well as an optional ``step`` and a variety of extra hints. The ``step`` defaults to ``1`` for integer properties. For floating-point numbers this value depends on your :ref:`EditorSettings.interface/inspector/default_float_step<class_EditorSettings_property_interface/inspector/default_float_step>` setting.

Nếu cung cấp các hint ``"or_greater"`` và ``"or_less"``, widget của editor sẽ không giới hạn giá trị ở các biên của range. Hint ``"exp"`` sẽ khiến các giá trị được chỉnh sửa trong range thay đổi theo cấp số mũ. Hint ``"prefer_slider"`` sẽ khiến các giá trị integer sử dụng thanh trượt thay vì mũi tên để chỉnh sửa, trong khi ``"hide_control"`` sẽ ẩn phần tử điều khiển giá trị của widget editor.

Các hint cũng cho phép chỉ định đơn vị cho giá trị được chỉnh sửa. Sử dụng ``"radians_as_degrees"``, bạn có thể chỉ định rằng giá trị thực tế tính bằng radians nhưng sẽ được hiển thị bằng degrees trong dock Inspector (các giá trị range cũng tính bằng degrees). ``"degrees"`` cho phép thêm dấu độ làm hậu tố đơn vị (giá trị không thay đổi). Cuối cùng, có thể cung cấp hậu tố tùy chỉnh bằng ``"suffix:unit"``, trong đó "unit" có thể là bất kỳ chuỗi nào.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_RANGE<class_@GlobalScope_constant_PROPERTY_HINT_RANGE>`.

::

    @export_range(0, 20) var number
    @export_range(-10, 20) var number
    @export_range(-10, 20, 0.2) var number: float
    @export_range(0, 20) var numbers: Array[float]

    @export_range(0, 100, 1, "or_greater") var power_percent
    @export_range(0, 100, 1, "or_greater", "or_less") var health_delta

    @export_range(-180, 180, 0.001, "radians_as_degrees") var angle_radians
    @export_range(0, 360, 1, "degrees") var angle_degrees
    @export_range(-8, 8, 2, "suffix:px") var target_offset

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_storage:

.. rst-class:: classref-annotation

**@export_storage**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@export_storage>`

Export một thuộc tính với flag :ref:`@GlobalScope.PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`. Thuộc tính không được hiển thị trong editor nhưng được serialize và lưu trong file scene hoặc resource. Điều này có thể hữu ích cho các script :ref:`@tool<class_@GDScript_annotation_@tool>`. Ngoài ra, giá trị thuộc tính được sao chép khi gọi :ref:`Resource.duplicate()<class_Resource_method_duplicate>` hoặc :ref:`Node.duplicate()<class_Node_method_duplicate>`, không giống các biến không được export.

::

    var a # Không được lưu trong file, không được hiển thị trong editor.
    @export_storage var b # Được lưu trong file, không được hiển thị trong editor.
    @export var c: int # Được lưu trong file, được hiển thị trong editor.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_subgroup:

.. rst-class:: classref-annotation

**@export_subgroup**\ (\ name\: :ref:`String<class_String>`, prefix\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_@GDScript_annotation_@export_subgroup>`

Xác định một subgroup mới cho các thuộc tính được export tiếp theo. Điều này giúp sắp xếp các thuộc tính trong dock Inspector. Subgroup hoạt động chính xác như group, ngoại trừ việc cần có group cha. Xem :ref:`@export_group<class_@GDScript_annotation_@export_group>`.

Xem thêm :ref:`@GlobalScope.PROPERTY_USAGE_SUBGROUP<class_@GlobalScope_constant_PROPERTY_USAGE_SUBGROUP>`.

::

    @export_group("Racer Properties")
    @export var nickname = "Nick"
    @export var age = 26

    @export_subgroup("Car Properties", "car_")
    @export var car_label = "Speedy"
    @export var car_number = 3

\ **Lưu ý:** Không thể lồng các subgroup, nhưng bạn có thể sử dụng dấu phân cách slash (``/``) để đạt được hiệu ứng mong muốn:

::

    @export_group("Car Properties")
    @export_subgroup("Wheels", "wheel_")
    @export_subgroup("Wheels/Front", "front_wheel_")
    @export var front_wheel_strength = 10
    @export var front_wheel_mobility = 5
    @export_subgroup("Wheels/Rear", "rear_wheel_")
    @export var rear_wheel_strength = 8
    @export var rear_wheel_mobility = 3
    @export_subgroup("Wheels", "wheel_")
    @export var wheel_material: PhysicsMaterial

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@export_tool_button:

.. rst-class:: classref-annotation

**@export_tool_button**\ (\ text\: :ref:`String<class_String>`, icon\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_@GDScript_annotation_@export_tool_button>`

Export thuộc tính :ref:`Callable<class_Callable>` dưới dạng một button có thể nhấp với nhãn ``text``. Khi nhấn button, callable sẽ được gọi.

Nếu chỉ định ``icon``, nó được sử dụng để lấy icon cho button thông qua :ref:`Control.get_theme_icon()<class_Control_method_get_theme_icon>`, từ loại theme ``"EditorIcons"``. Nếu bỏ qua ``icon``, icon ``"Callable"`` mặc định sẽ được sử dụng.

Cân nhắc sử dụng :ref:`EditorUndoRedoManager<class_EditorUndoRedoManager>` để cho phép hoàn tác hành động một cách an toàn.

Xem thêm :ref:`@GlobalScope.PROPERTY_HINT_TOOL_BUTTON<class_@GlobalScope_constant_PROPERTY_HINT_TOOL_BUTTON>`.

::

    @tool
    extends Sprite2D

    @export_tool_button("Hello") var hello_action = hello
    @export_tool_button("Randomize the color!", "ColorRect")
    var randomize_color_action = randomize_color

    func hello():
        print("Hello world!")

    func randomize_color():
        var undo_redo = EditorInterface.get_editor_undo_redo()
        undo_redo.create_action("Randomized Sprite2D Color")
        undo_redo.add_do_property(self, &"self_modulate", Color(randf(), randf(), randf()))
        undo_redo.add_undo_property(self, &"self_modulate", self_modulate)
        undo_redo.commit_action()

\ **Lưu ý:** Thuộc tính được export mà không có cờ :ref:`@GlobalScope.PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>` vì :ref:`Callable<class_Callable>` không thể được tuần tự hóa và lưu trữ đúng cách trong một tệp.

\ **Lưu ý:** Trong một project đã export, cả :ref:`EditorInterface<class_EditorInterface>` lẫn :ref:`EditorUndoRedoManager<class_EditorUndoRedoManager>` đều không tồn tại, điều này có thể khiến một số script bị lỗi. Để ngăn điều này, bạn có thể sử dụng :ref:`Engine.get_singleton()<class_Engine_method_get_singleton>` và bỏ kiểu tĩnh khỏi khai báo biến:

::

    var undo_redo = Engine.get_singleton(&"EditorInterface").get_editor_undo_redo()

\ **Lưu ý:** Tránh lưu các callable lambda trong biến thành viên của các class dựa trên :ref:`RefCounted<class_RefCounted>` (ví dụ: resource), vì điều này có thể dẫn đến rò rỉ bộ nhớ. Chỉ sử dụng callable của method và tùy chọn :ref:`Callable.bind()<class_Callable_method_bind>` hoặc :ref:`Callable.unbind()<class_Callable_method_unbind>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@icon:

.. rst-class:: classref-annotation

**@icon**\ (\ icon_path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_annotation_@icon>`

Thêm một icon tùy chỉnh vào script hiện tại. Icon được chỉ định tại ``icon_path`` sẽ hiển thị trong dock Scene cho mọi node thuộc class đó, cũng như trong nhiều hộp thoại của editor.

::

    @icon("res://path/to/class/icon.svg")

\ **Lưu ý:** Chỉ script mới có thể có icon tùy chỉnh. Không hỗ trợ class bên trong.

\ **Lưu ý:** Vì annotation mô tả đối tượng mà chúng áp dụng, annotation :ref:`@icon<class_@GDScript_annotation_@icon>` phải được đặt trước phần định nghĩa class và kế thừa.

\ **Lưu ý:** Không giống hầu hết annotation khác, đối số của annotation :ref:`@icon<class_@GDScript_annotation_@icon>` phải là một string literal (không hỗ trợ biểu thức hằng).

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@onready:

.. rst-class:: classref-annotation

**@onready**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@onready>`

Đánh dấu thuộc tính tiếp theo là được gán khi :ref:`Node<class_Node>` sẵn sàng. Giá trị của các thuộc tính này không được gán ngay khi node được khởi tạo (:ref:`Object._init()<class_Object_private_method__init>`), mà được tính toán và lưu trữ ngay trước :ref:`Node._ready()<class_Node_private_method__ready>`.

::

    @onready var character_name = $Label

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@rpc:

.. rst-class:: classref-annotation

**@rpc**\ (\ mode\: :ref:`String<class_String>` = "authority", sync\: :ref:`String<class_String>` = "call_remote", transfer_mode\: :ref:`String<class_String>` = "reliable", transfer_channel\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_@GDScript_annotation_@rpc>`

Đánh dấu method tiếp theo để thực hiện remote procedure call. Xem :doc:`High-level multiplayer <../tutorials/networking/high_level_multiplayer>`.

Nếu ``mode`` được đặt là ``"any_peer"``, cho phép bất kỳ peer nào gọi hàm RPC này. Nếu không, chỉ peer authority mới được phép gọi hàm này và nên giữ ``mode`` là ``"authority"``. Khi cấu hình các hàm dưới dạng RPC bằng :ref:`Node.rpc_config()<class_Node_method_rpc_config>`, mỗi mode này lần lượt tương ứng với các mode RPC :ref:`MultiplayerAPI.RPC_MODE_AUTHORITY<class_MultiplayerAPI_constant_RPC_MODE_AUTHORITY>` và :ref:`MultiplayerAPI.RPC_MODE_ANY_PEER<class_MultiplayerAPI_constant_RPC_MODE_ANY_PEER>`. Xem :ref:`RPCMode<enum_MultiplayerAPI_RPCMode>`. Nếu một peer không phải authority cố gọi một hàm chỉ cho phép authority gọi, hàm sẽ không được thực thi. Nếu lỗi có thể được phát hiện cục bộ (khi cấu hình RPC nhất quán giữa peer cục bộ và peer từ xa), một thông báo lỗi sẽ được hiển thị trên peer gửi. Nếu không, peer từ xa sẽ phát hiện lỗi và in lỗi tại đó.

Nếu ``sync`` được đặt là ``"call_remote"``, hàm sẽ chỉ được thực thi trên peer từ xa chứ không thực thi cục bộ. Để chạy hàm này cả cục bộ, hãy đặt ``sync`` thành ``"call_local"``. Khi cấu hình các hàm dưới dạng RPC bằng :ref:`Node.rpc_config()<class_Node_method_rpc_config>`, điều này tương đương với việc đặt ``call_local`` thành ``true``.

Các giá trị được chấp nhận của ``transfer_mode`` là ``"unreliable"``, ``"unreliable_ordered"`` hoặc ``"reliable"``. Nó đặt transfer mode của :ref:`MultiplayerPeer<class_MultiplayerPeer>` bên dưới. Xem :ref:`MultiplayerPeer.transfer_mode<class_MultiplayerPeer_property_transfer_mode>`.

``transfer_channel`` xác định channel của :ref:`MultiplayerPeer<class_MultiplayerPeer>` bên dưới. Xem :ref:`MultiplayerPeer.transfer_channel<class_MultiplayerPeer_property_transfer_channel>`.

Thứ tự của ``mode``, ``sync`` và ``transfer_mode`` không quan trọng, nhưng không được sử dụng các giá trị liên quan đến cùng một đối số quá một lần. ``transfer_channel`` luôn phải là đối số thứ 4 (bạn phải chỉ định 3 đối số trước đó).

::

    @rpc
    func fn(): pass

    @rpc("any_peer", "unreliable_ordered")
    func fn_update_pos(): pass

    @rpc("authority", "call_remote", "reliable", 0) # Tương đương với @rpc
    func fn_default(): pass

\ **Lưu ý:** Các method được chú thích bằng :ref:`@rpc<class_@GDScript_annotation_@rpc>` không thể nhận các object định nghĩa các tham số bắt buộc trong :ref:`Object._init()<class_Object_private_method__init>`. Xem :ref:`Object._init()<class_Object_private_method__init>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@static_unload:

.. rst-class:: classref-annotation

**@static_unload**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@static_unload>`

Khiến một script có các biến static không tiếp tục tồn tại sau khi mọi tham chiếu bị mất. Nếu script được load lại, các biến static sẽ trở về giá trị mặc định.

\ **Lưu ý:** Vì annotation mô tả đối tượng mà chúng áp dụng, annotation :ref:`@static_unload<class_@GDScript_annotation_@static_unload>` phải được đặt trước phần định nghĩa class và kế thừa.

\ **Cảnh báo:** Hiện tại, do một bug, các script không bao giờ được giải phóng, ngay cả khi sử dụng annotation :ref:`@static_unload<class_@GDScript_annotation_@static_unload>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@tool:

.. rst-class:: classref-annotation

**@tool**\ (\ ) :ref:`🔗<class_@GDScript_annotation_@tool>`

Đánh dấu script hiện tại là tool script, cho phép editor load và thực thi script đó. Xem :doc:`Running code in the editor <../tutorials/plugins/running_code_in_the_editor>`.

::

    @tool
    extends Node

\ **Lưu ý:** Vì annotation mô tả đối tượng mà chúng áp dụng, annotation :ref:`@tool<class_@GDScript_annotation_@tool>` phải được đặt trước phần định nghĩa class và kế thừa.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@warning_ignore:

.. rst-class:: classref-annotation

**@warning_ignore**\ (\ warning\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@warning_ignore>`

Đánh dấu statement tiếp theo để bỏ qua ``warning`` được chỉ định. Xem :doc:`GDScript warning system <../tutorials/scripting/gdscript/warning_system>`.

::

    func test():
        print("hello")
        return
        @warning_ignore("unreachable_code")
        print("unreachable")

Xem thêm :ref:`@warning_ignore_start<class_@GDScript_annotation_@warning_ignore_start>` và :ref:`@warning_ignore_restore<class_@GDScript_annotation_@warning_ignore_restore>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@warning_ignore_restore:

.. rst-class:: classref-annotation

**@warning_ignore_restore**\ (\ warning\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@warning_ignore_restore>`

Dừng bỏ qua các loại warning được liệt kê sau :ref:`@warning_ignore_start<class_@GDScript_annotation_@warning_ignore_start>`. Việc bỏ qua các loại warning được chỉ định sẽ được đặt lại về Project Settings. Có thể bỏ qua annotation này để tiếp tục bỏ qua các loại warning cho đến cuối tệp.

\ **Lưu ý:** Không giống hầu hết annotation khác, các đối số của annotation :ref:`@warning_ignore_restore<class_@GDScript_annotation_@warning_ignore_restore>` phải là string literal (không hỗ trợ biểu thức hằng).

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_annotation_@warning_ignore_start:

.. rst-class:: classref-annotation

**@warning_ignore_start**\ (\ warning\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_@GDScript_annotation_@warning_ignore_start>`

Bắt đầu bỏ qua các loại warning được liệt kê cho đến cuối tệp hoặc đến annotation :ref:`@warning_ignore_restore<class_@GDScript_annotation_@warning_ignore_restore>` có loại warning tương ứng.

::

    func test():
        var a = 1 # Warning (nếu được bật trong Project Settings).
        @warning_ignore_start("unused_variable")
        var b = 2 # Không có warning.
        var c = 3 # Không có warning.
        @warning_ignore_restore("unused_variable")
        var d = 4 # Warning (nếu được bật trong Project Settings).

\ **Lưu ý:** Để ẩn một warning, hãy sử dụng :ref:`@warning_ignore<class_@GDScript_annotation_@warning_ignore>` thay thế.

\ **Lưu ý:** Không giống hầu hết annotation khác, các đối số của annotation :ref:`@warning_ignore_start<class_@GDScript_annotation_@warning_ignore_start>` phải là string literal (không hỗ trợ biểu thức hằng).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_@GDScript_method_Color8:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **Color8**\ (\ r8\: :ref:`int<class_int>`, g8\: :ref:`int<class_int>`, b8\: :ref:`int<class_int>`, a8\: :ref:`int<class_int>` = 255\ ) :ref:`🔗<class_@GDScript_method_Color8>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`Color.from_rgba8()<class_Color_method_from_rgba8>`.

Trả về một :ref:`Color<class_Color>` được tạo từ các channel số nguyên red (``r8``), green (``g8``), blue (``b8``) và tùy chọn alpha (``a8``), mỗi channel được chia cho ``255.0`` để có giá trị cuối cùng. Sử dụng :ref:`Color8()<class_@GDScript_method_Color8>` thay cho constructor :ref:`Color<class_Color>` tiêu chuẩn rất hữu ích khi bạn cần khớp các giá trị màu chính xác trong một :ref:`Image<class_Image>`.

::

    var red = Color8(255, 0, 0)             # Giống như Color(1, 0, 0).
    var dark_blue = Color8(0, 0, 51)        # Giống như Color(0, 0, 0.2).
    var my_color = Color8(306, 255, 0, 102) # Giống như Color(1.2, 1, 0, 0.4).

\ **Lưu ý:** Do độ chính xác thấp hơn của :ref:`Color8()<class_@GDScript_method_Color8>` so với constructor :ref:`Color<class_Color>` tiêu chuẩn, một màu được tạo bằng :ref:`Color8()<class_@GDScript_method_Color8>` nhìn chung sẽ không bằng màu tương tự được tạo bằng constructor :ref:`Color<class_Color>` tiêu chuẩn. Sử dụng :ref:`Color.is_equal_approx()<class_Color_method_is_equal_approx>` để so sánh nhằm tránh các vấn đề do sai số độ chính xác dấu phẩy động.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_assert:

.. rst-class:: classref-method

|void| **assert**\ (\ condition\: :ref:`bool<class_bool>`, message\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_@GDScript_method_assert>`

Assert rằng ``condition`` là ``true``. Nếu ``condition`` là ``false``, một lỗi sẽ được tạo ra và method hiện tại trả về giá trị mặc định. Khi chạy từ editor, các assert thất bại cũng khiến debugger dừng lại. Có thể sử dụng điều này như một dạng :ref:`@GlobalScope.push_error()<class_@GlobalScope_method_push_error>` mạnh hơn để báo lỗi cho developer của project hoặc người dùng add-on.

Có thể hiển thị thêm một ``message`` tùy chọn bên cạnh thông báo chung "Assertion failed". Bạn có thể dùng thông báo này để cung cấp thêm chi tiết về lý do assert thất bại.

\ **Cảnh báo:** Vì lý do hiệu năng, code bên trong :ref:`assert()<class_@GDScript_method_assert>` chỉ được thực thi trong các bản build debug hoặc khi chạy project từ editor. Không đưa code có side effect vào một lệnh gọi :ref:`assert()<class_@GDScript_method_assert>`. Nếu không, project sẽ hoạt động khác khi được export ở chế độ release.

::

    # Hãy giả sử chúng ta luôn muốn speed nằm trong khoảng từ 0 đến 20.
    var speed = -10
    assert(speed < 20) # Đúng, chương trình sẽ tiếp tục.
    assert(speed >= 0) # Sai, chương trình sẽ dừng.
    assert(speed >= 0 and speed < 20) # Bạn cũng có thể kết hợp hai câu lệnh điều kiện trong một phép kiểm tra.
    assert(speed < 20, "the speed limit is 20") # Hiển thị một thông báo.

\ **Lưu ý:** :ref:`assert()<class_@GDScript_method_assert>` là một keyword, không phải một function. Vì vậy, bạn không thể truy cập nó dưới dạng :ref:`Callable<class_Callable>` hoặc sử dụng nó bên trong các biểu thức.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_char:

.. rst-class:: classref-method

:ref:`String<class_String>` **char**\ (\ code\: :ref:`int<class_int>`\ ) :ref:`🔗<class_@GDScript_method_char>`

Trả về một ký tự đơn (dưới dạng :ref:`String<class_String>` có độ dài 1) của code point Unicode đã cho ``code``.

::

    print(char(65))     # In "A"
    print(char(129302)) # In "🤖" (emoji mặt robot)

Đây là phép đảo ngược của :ref:`ord()<class_@GDScript_method_ord>`. Xem thêm :ref:`String.chr()<class_String_method_chr>` và :ref:`String.unicode_at()<class_String_method_unicode_at>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_convert:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **convert**\ (\ what\: :ref:`Variant<class_Variant>`, type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`\ ) :ref:`🔗<class_@GDScript_method_convert>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`@GlobalScope.type_convert()<class_@GlobalScope_method_type_convert>`.

Chuyển đổi ``what`` thành ``type`` theo cách tốt nhất có thể. ``type`` sử dụng các giá trị :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`.

::

    var a = [4, 2.5, 1.2]
    print(a is Array) # In ra true

    var b = convert(a, TYPE_PACKED_BYTE_ARRAY)
    print(b)          # In ra [4, 2, 1]
    print(b is Array) # In ra false

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_dict_to_inst:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **dict_to_inst**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_@GDScript_method_dict_to_inst>`

**Đã lỗi thời:** Hãy cân nhắc sử dụng :ref:`JSON.to_native()<class_JSON_method_to_native>` hoặc :ref:`Object.get_property_list()<class_Object_method_get_property_list>` thay thế.

Chuyển đổi một ``dictionary`` (được tạo bằng :ref:`inst_to_dict()<class_@GDScript_method_inst_to_dict>`) trở lại thành một instance Object. Có thể hữu ích khi deserializing.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_get_stack:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_stack**\ (\ ) :ref:`🔗<class_@GDScript_method_get_stack>`

Trả về một mảng các dictionary biểu diễn call stack hiện tại.

::

    func _ready():
        foo()

    func foo():
        bar()

    func bar():
        print(get_stack())

Bắt đầu từ ``_ready()``, ``bar()`` sẽ in ra:

.. code:: text

    [{function:bar, line:12, source:res://script.gd}, {function:foo, line:9, source:res://script.gd}, {function:_ready, line:6, source:res://script.gd}]

Xem thêm :ref:`print_debug()<class_@GDScript_method_print_debug>`, :ref:`print_stack()<class_@GDScript_method_print_stack>` và :ref:`Engine.capture_script_backtraces()<class_Engine_method_capture_script_backtraces>`.

\ **Lưu ý:** Theo mặc định, backtrace chỉ khả dụng trong các bản build của editor và bản build debug. Để bật chúng cho cả các bản build release, bạn cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_call_stacks<class_ProjectSettings_property_debug/settings/gdscript/always_track_call_stacks>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_inst_to_dict:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **inst_to_dict**\ (\ instance\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_@GDScript_method_inst_to_dict>`

**Đã lỗi thời:** Hãy cân nhắc sử dụng :ref:`JSON.from_native()<class_JSON_method_from_native>` hoặc :ref:`Object.get_property_list()<class_Object_method_get_property_list>` thay thế.

Trả về ``instance`` được truyền vào sau khi chuyển đổi thành :ref:`Dictionary<class_Dictionary>`. Có thể hữu ích khi serializing.

::

    var foo = "bar"
    func _ready():
        var d = inst_to_dict(self)
        print(d.keys())
        print(d.values())

In ra:

.. code:: text

    [@subpath, @path, foo]
    [, res://test.gd, bar]

\ **Lưu ý:** Hàm này chỉ có thể được sử dụng để serialize các object có :ref:`GDScript<class_GDScript>` đính kèm được lưu trong một tệp riêng. Các object không có script đính kèm, có script được viết bằng ngôn ngữ khác hoặc có script tích hợp đều không được hỗ trợ.

\ **Lưu ý:** Hàm này không đệ quy, nghĩa là các object lồng nhau sẽ không được biểu diễn dưới dạng dictionary. Ngoài ra, các property được truyền bằng tham chiếu (:ref:`Object<class_Object>`, :ref:`Dictionary<class_Dictionary>`, :ref:`Array<class_Array>` và packed array) được sao chép bằng tham chiếu, không được nhân bản.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_is_instance_of:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_instance_of**\ (\ value\: :ref:`Variant<class_Variant>`, type\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_@GDScript_method_is_instance_of>`

Trả về ``true`` nếu ``value`` là một instance của ``type``. Giá trị ``type`` phải là một trong các giá trị sau:

- Một hằng số từ enumeration :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, ví dụ :ref:`@GlobalScope.TYPE_INT<class_@GlobalScope_constant_TYPE_INT>`.

- Một class dẫn xuất từ :ref:`Object<class_Object>` tồn tại trong :ref:`ClassDB<class_ClassDB>`, ví dụ :ref:`Node<class_Node>`.

- Một :ref:`Script<class_Script>` (bạn có thể sử dụng bất kỳ class nào, bao gồm cả class bên trong).

Không giống toán hạng bên phải của operator ``is``, ``type`` có thể là một giá trị không phải hằng số. Operator ``is`` hỗ trợ nhiều tính năng hơn (chẳng hạn như typed array và dictionary). Hãy sử dụng operator thay vì method này nếu bạn không cần kiểm tra type một cách động.

\ **Ví dụ:**\

::

    print(is_instance_of(a, TYPE_INT))
    print(is_instance_of(a, Node))
    print(is_instance_of(a, MyClass))
    print(is_instance_of(a, MyClass.InnerClass))

\ **Lưu ý:** Nếu ``value`` và/hoặc ``type`` là các object đã được giải phóng (xem :ref:`@GlobalScope.is_instance_valid()<class_@GlobalScope_method_is_instance_valid>`), hoặc ``type`` không phải là một trong các tùy chọn trên, method này sẽ gây ra runtime error.

Xem thêm :ref:`@GlobalScope.typeof()<class_@GlobalScope_method_typeof>`, :ref:`Object.is_class()<class_Object_method_is_class>`, :ref:`Object.get_script()<class_Object_method_get_script>`, :ref:`Array.is_same_typed()<class_Array_method_is_same_typed>` (và các method :ref:`Array<class_Array>` khác), :ref:`Dictionary.is_same_typed()<class_Dictionary_method_is_same_typed>` (và các method :ref:`Dictionary<class_Dictionary>` khác).

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_len:

.. rst-class:: classref-method

:ref:`int<class_int>` **len**\ (\ var\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_@GDScript_method_len>`

Trả về độ dài của ``var`` Variant đã cho. Độ dài có thể là số ký tự của một :ref:`String<class_String>` hoặc :ref:`StringName<class_StringName>`, số phần tử của bất kỳ kiểu array nào hoặc kích thước của một :ref:`Dictionary<class_Dictionary>`. Với mọi kiểu Variant khác, một run-time error sẽ được tạo ra và quá trình thực thi sẽ dừng lại.

::

    var a = [1, 2, 3, 4]
    len(a) # Trả về 4

    var b = "Hello!"
    len(b) # Trả về 6

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_load:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **load**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_method_load>`

Trả về một :ref:`Resource<class_Resource>` từ filesystem tại ``path`` tuyệt đối. Trừ khi đã được tham chiếu ở nơi khác (chẳng hạn như trong một script khác hoặc trong scene), resource sẽ được tải từ đĩa khi gọi hàm, điều này có thể gây ra độ trễ nhỏ, đặc biệt khi tải các scene lớn. Để tránh độ trễ không cần thiết khi tải một thứ nhiều lần, hãy lưu resource vào một biến hoặc sử dụng :ref:`preload()<class_@GDScript_method_preload>`. Method này tương đương với việc sử dụng :ref:`ResourceLoader.load()<class_ResourceLoader_method_load>` cùng với :ref:`ResourceLoader.CACHE_MODE_REUSE<class_ResourceLoader_constant_CACHE_MODE_REUSE>`.

\ **Lưu ý:** Có thể lấy resource path bằng cách nhấp chuột phải vào một resource trong dock FileSystem và chọn "Copy Path", hoặc kéo tệp từ dock FileSystem vào script hiện tại.

::

    # Tải một scene có tên "main" nằm trong thư mục gốc của project và cache nó vào một biến.
    var main = load("res://main.tscn") # main sẽ chứa một resource PackedScene.

\ **Quan trọng:** Các path tương đối *không* tương đối so với script gọi method này; thay vào đó, chúng được thêm tiền tố ``"res://"``. Việc tải từ các path tương đối có thể không hoạt động như mong đợi.

Hàm này là phiên bản đơn giản hóa của :ref:`ResourceLoader.load()<class_ResourceLoader_method_load>`, có thể được sử dụng cho các trường hợp nâng cao hơn.

\ **Note:** Files have to be imported into the engine first to load them using this function. If you want to load :ref:`Image<class_Image>`\ s at run-time, you may use :ref:`Image.load()<class_Image_method_load>`. If you want to import audio files, you can use the snippet described in :ref:`AudioStreamMP3.data<class_AudioStreamMP3_property_data>`.

\ **Lưu ý:** Nếu :ref:`ProjectSettings.editor/export/convert_text_resources_to_binary<class_ProjectSettings_property_editor/export/convert_text_resources_to_binary>` là ``true``, :ref:`load()<class_@GDScript_method_load>` sẽ không thể đọc các tệp đã chuyển đổi trong project đã export. Nếu bạn dựa vào việc tải tại run-time các tệp có trong PCK, hãy đặt :ref:`ProjectSettings.editor/export/convert_text_resources_to_binary<class_ProjectSettings_property_editor/export/convert_text_resources_to_binary>` thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_ord:

.. rst-class:: classref-method

:ref:`int<class_int>` **ord**\ (\ char\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_method_ord>`

Trả về một số nguyên biểu diễn code point Unicode của ký tự ``char`` đã cho, ký tự này phải là một string có độ dài 1.

::

    print(ord("A")) # In ra 65
    print(ord("🤖")) # In ra 129302

Đây là phép nghịch đảo của :ref:`char()<class_@GDScript_method_char>`. Xem thêm :ref:`String.chr()<class_String_method_chr>` và :ref:`String.unicode_at()<class_String_method_unicode_at>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_preload:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **preload**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_@GDScript_method_preload>`

Trả về một :ref:`Resource<class_Resource>` từ filesystem tại ``path``. Trong quá trình run-time, resource được tải khi script đang được parse. Về bản chất, hàm này hoạt động như một tham chiếu đến resource đó. Lưu ý rằng hàm này yêu cầu ``path`` phải là một :ref:`String<class_String>` hằng số. Nếu muốn tải resource từ một path động/thay đổi, hãy sử dụng :ref:`load()<class_@GDScript_method_load>`.

\ **Lưu ý:** Có thể lấy resource path bằng cách nhấp chuột phải vào một resource trong Assets Panel và chọn "Copy Path", hoặc kéo tệp từ dock FileSystem vào script hiện tại.

::

    # Tạo instance của một scene.
    var diamond = preload("res://diamond.tscn").instantiate()

\ **Lưu ý:** :ref:`preload()<class_@GDScript_method_preload>` là một keyword, không phải một function. Vì vậy, bạn không thể truy cập nó dưới dạng :ref:`Callable<class_Callable>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_print_debug:

.. rst-class:: classref-method

|void| **print_debug**\ (\ ...\ ) |vararg| :ref:`🔗<class_@GDScript_method_print_debug>`

Tương tự :ref:`@GlobalScope.print()<class_@GlobalScope_method_print>`, nhưng bao gồm stack frame hiện tại khi chạy với debugger được bật.

Output trong console có thể trông như sau:

.. code:: text

    Test print
    At: res://test.gd:15:_process()

Xem thêm :ref:`print_stack()<class_@GDScript_method_print_stack>`, :ref:`get_stack()<class_@GDScript_method_get_stack>` và :ref:`Engine.capture_script_backtraces()<class_Engine_method_capture_script_backtraces>`.

\ **Lưu ý:** Theo mặc định, backtrace chỉ khả dụng trong các bản build của editor và bản build debug. Để bật chúng cho cả các bản build release, bạn cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_call_stacks<class_ProjectSettings_property_debug/settings/gdscript/always_track_call_stacks>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_print_stack:

.. rst-class:: classref-method

|void| **print_stack**\ (\ ) :ref:`🔗<class_@GDScript_method_print_stack>`

In stack trace tại vị trí code hiện tại.

Output trong console có thể trông như sau:

.. code:: text

    Frame 0 - res://test.gd:16 in function '_process'

Xem thêm :ref:`print_debug()<class_@GDScript_method_print_debug>`, :ref:`get_stack()<class_@GDScript_method_get_stack>` và :ref:`Engine.capture_script_backtraces()<class_Engine_method_capture_script_backtraces>`.

\ **Lưu ý:** Theo mặc định, backtrace chỉ khả dụng trong các bản build của editor và bản build debug. Để bật chúng cho cả các bản build release, bạn cần bật :ref:`ProjectSettings.debug/settings/gdscript/always_track_call_stacks<class_ProjectSettings_property_debug/settings/gdscript/always_track_call_stacks>`.

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_range:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **range**\ (\ ...\ ) |vararg| :ref:`🔗<class_@GDScript_method_range>`

Trả về một mảng với range đã cho. Có thể gọi :ref:`range()<class_@GDScript_method_range>` theo ba cách:

\ ``range(n: int)``: Bắt đầu từ 0, tăng theo từng bước 1 và dừng *trước* ``n``. Đối số ``n`` là **không bao gồm**.

\ ``range(b: int, n: int)``: Bắt đầu từ ``b``, tăng theo từng bước 1 và dừng *trước* ``n``. Các đối số ``b`` và ``n`` lần lượt là **bao gồm** và **không bao gồm**.

\ ``range(b: int, n: int, s: int)``: Bắt đầu từ ``b``, tăng/giảm theo từng bước ``s`` và dừng *trước* ``n``. Các đối số ``b`` và ``n`` lần lượt là **bao gồm** và **không bao gồm**. Đối số ``s`` **có thể** là số âm, nhưng ``0`` thì không. Nếu ``s`` là ``0``, một thông báo lỗi sẽ được in ra.

\ :ref:`range()<class_@GDScript_method_range>` chuyển đổi tất cả đối số thành :ref:`int<class_int>` trước khi xử lý.

\ **Lưu ý:** Trả về một mảng rỗng nếu không có giá trị nào đáp ứng ràng buộc giá trị (ví dụ: ``range(2, 5, -1)`` hoặc ``range(5, 5, 1)``).

\ **Ví dụ:**\

::

    print(range(4))        # In ra [0, 1, 2, 3]
    print(range(2, 5))     # In ra [2, 3, 4]
    print(range(0, 6, 2))  # In ra [0, 2, 4]
    print(range(4, 1, -1)) # In ra [4, 3, 2]

Để lặp qua một :ref:`Array<class_Array>` theo thứ tự ngược, hãy sử dụng:

::

    var array = [3, 6, 9]
    for i in range(array.size() - 1, -1, -1):
        print(array[i])

Output:

.. code:: text

    9
    6
    3

Để lặp qua :ref:`float<class_float>`, hãy chuyển đổi chúng trong vòng lặp.

::

    for i in range (3, 0, -1):
        print(i / 10.0)

Output:

.. code:: text

    0.3
    0.2
    0.1

.. rst-class:: classref-item-separator

----

.. _class_@GDScript_method_type_exists:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **type_exists**\ (\ type\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_@GDScript_method_type_exists>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`ClassDB.class_exists()<class_ClassDB_method_class_exists>`.

Trả về ``true`` nếu lớp dẫn xuất từ :ref:`Object<class_Object>` đã cho tồn tại trong :ref:`ClassDB<class_ClassDB>`. Lưu ý rằng các kiểu dữ liệu :ref:`Variant<class_Variant>` không được đăng ký trong :ref:`ClassDB<class_ClassDB>`.

::

    type_exists("Sprite2D") # Trả về true
    type_exists("NonExistentClass") # Trả về false

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
