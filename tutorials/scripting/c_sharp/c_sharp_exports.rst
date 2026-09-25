.. _doc_c_sharp_exports:

Các thuộc tính C# được export
=============================

Trong Godot, các thành viên của lớp có thể được export. Điều này có nghĩa là giá trị của chúng sẽ được lưu cùng với resource (chẳng hạn như :ref:`scene <class_PackedScene>`) mà chúng được gắn vào. Chúng cũng sẽ có sẵn để chỉnh sửa trong trình chỉnh sửa thuộc tính. Việc export được thực hiện bằng cách sử dụng attribute ``[Export]``.

.. code-block:: csharp

    using Godot;

    public partial class ExportExample : Node3D
    {
        [Export]
        public int Number { get; set; } = 5;
    }

Trong ví dụ đó, giá trị ``5`` sẽ được lưu và sau khi build project hiện tại, nó sẽ hiển thị trong trình chỉnh sửa thuộc tính.

Một trong những lợi ích nền tảng của việc export các biến thành viên là giúp chúng hiển thị và có thể chỉnh sửa trong editor. Nhờ đó, artist và game designer có thể sửa đổi các giá trị, những giá trị này về sau sẽ ảnh hưởng đến cách chương trình chạy. Để thực hiện việc này, có một cú pháp export đặc biệt.

Chỉ có thể export bằng :ref:`c_sharp_variant_compatible_types`.

.. note::

    Bạn cũng có thể export các thuộc tính trong GDScript; để biết thông tin về việc này, hãy xem :ref:`doc_gdscript_exports`.

Cách sử dụng cơ bản
-------------------

Export hoạt động với các field và property. Chúng có thể sử dụng bất kỳ access modifier nào.

.. code-block:: csharp

    [Export]
    private int _number;

    [Export]
    public int Number { get; set; }

Các thành viên được export có thể chỉ định giá trị mặc định; nếu không, `giá trị mặc định của kiểu <https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/default-values>`_ sẽ được sử dụng thay thế.

Một ``int`` như ``Number`` mặc định có giá trị ``0``. ``Text`` mặc định là null vì ``string`` là một reference type.

.. code-block:: csharp

    [Export]
    public int Number { get; set; }

    [Export]
    public string Text { get; set; }

Có thể chỉ định giá trị mặc định cho các field và property.

.. code-block:: csharp

    [Export]
    private string _greeting = "Hello World";

    [Export]
    public string Greeting { get; set; } = "Hello World";

Các property có backing field sẽ sử dụng giá trị mặc định của backing field.

.. code-block:: csharp

    private int _number = 2;

    [Export]
    public int NumberWithBackingField
    {
        get => _number;
        set => _number = value;
    }

.. note::

    ``get`` của một property không thực sự được thực thi để xác định giá trị mặc định. Thay vào đó, Godot phân tích mã nguồn C#. Cách này hoạt động tốt trong hầu hết trường hợp, chẳng hạn như các ví dụ trên trang này. Tuy nhiên, một số property quá phức tạp để analyzer hiểu được.

    Ví dụ, property sau đây cố gắng sử dụng phép tính để hiển thị giá trị mặc định là ``5`` trong trình chỉnh sửa thuộc tính, nhưng không hoạt động:

    .. code-block:: csharp

        [Export]
        public int NumberWithBackingField
        {
            get => _number + 3;
            set => _number = value - 3;
        }

        private int _number = 2;

    Analyzer không hiểu mã này và quay về giá trị mặc định của ``int``, ``0``. Tuy nhiên, khi chạy scene hoặc kiểm tra một node có gắn tool script, ``_number`` sẽ là ``2``, còn ``NumberWithBackingField`` sẽ trả về ``5``. Sự khác biệt này có thể gây ra hành vi khó hiểu. Để tránh điều này, không sử dụng các property phức tạp. Ngoài ra, nếu có thể chỉ định rõ ràng giá trị mặc định, bạn có thể ghi đè giá trị đó bằng
    :ref:`_PropertyCanRevert() <class_Object_private_method__property_can_revert>` và
    các phương thức :ref:`_PropertyGetRevert() <class_Object_private_method__property_get_revert>`.

Có thể export bất kỳ kiểu ``Resource`` hoặc ``Node`` nào. Trình chỉnh sửa thuộc tính sẽ hiển thị hộp thoại gán thân thiện với người dùng cho các kiểu này. Có thể sử dụng cách này thay cho ``GD.Load`` và ``GetNode``. Xem :ref:`Nodes and Resources <doc_c_sharp_exports_nodes>`.

.. code-block:: csharp

    [Export]
    public PackedScene PackedScene { get; set; }

    [Export]
    public RigidBody2D RigidBody2D { get; set; }

Nhóm các export
---------------

Bạn có thể nhóm các thuộc tính được export trong Inspector bằng attribute ``[ExportGroup]``. Mọi thuộc tính được export sau attribute này sẽ được thêm vào nhóm. Hãy bắt đầu một nhóm mới hoặc sử dụng ``[ExportGroup("")]`` để thoát khỏi nhóm.

.. code-block:: csharp

    [ExportGroup("My Properties")]
    [Export]
    public int Number { get; set; } = 3;

Đối số thứ hai của attribute có thể được sử dụng để chỉ nhóm các thuộc tính có prefix được chỉ định.

Không thể lồng các nhóm; hãy sử dụng ``[ExportSubgroup]`` để tạo các nhóm con bên trong một nhóm.

.. code-block:: csharp

    [ExportSubgroup("Extra Properties")]
    [Export]
    public string Text { get; set; } = "";
    [Export]
    public bool Flag { get; set; } = false;

Bạn cũng có thể đổi tên category chính hoặc tạo thêm các category trong danh sách thuộc tính bằng attribute ``[ExportCategory]``.

.. code-block:: csharp

    [ExportCategory("Main Category")]
    [Export]
    public int Number { get; set; } = 3;
    [Export]
    public string Text { get; set; } = "";

    [ExportCategory("Extra Category")]
    [Export]
    public bool Flag { get; set; } = false;

.. note::

    Danh sách thuộc tính được sắp xếp dựa trên tính kế thừa của lớp, và các category mới sẽ phá vỡ quy tắc đó. Hãy sử dụng chúng cẩn thận, đặc biệt khi tạo project để sử dụng công khai.

Chuỗi làm đường dẫn
-------------------

Có thể sử dụng property hint để export các chuỗi làm đường dẫn

Chuỗi làm đường dẫn đến một file.

.. code-block:: csharp

    [Export(PropertyHint.File)]
    public string GameFile { get; set; }

Chuỗi làm đường dẫn đến một thư mục.

.. code-block:: csharp

    [Export(PropertyHint.Dir)]
    public string GameDirectory { get; set; }

Chuỗi làm đường dẫn đến một file, với bộ lọc tùy chỉnh được cung cấp dưới dạng hint.

.. code-block:: csharp

    [Export(PropertyHint.File, "*.txt,")]
    public string GameFile { get; set; }

Cũng có thể sử dụng các đường dẫn trong global filesystem, nhưng chỉ trong các script ở tool mode.

Chuỗi làm đường dẫn đến một file PNG trong global filesystem.

.. code-block:: csharp

    [Export(PropertyHint.GlobalFile, "*.png")]
    public string ToolImage { get; set; }

Chuỗi làm đường dẫn đến một thư mục trong global filesystem.

.. code-block:: csharp

    [Export(PropertyHint.GlobalDir)]
    public string ToolDir { get; set; }

Annotation multiline yêu cầu editor hiển thị một trường nhập lớn để chỉnh sửa trên nhiều dòng.

.. code-block:: csharp

    [Export(PropertyHint.MultilineText)]
    public string Text { get; set; }

Giới hạn phạm vi nhập trong editor
----------------------------------

Sử dụng property hint range cho phép bạn giới hạn giá trị có thể được nhập bằng editor.

Cho phép các giá trị integer từ 0 đến 20.

.. code-block:: csharp

    [Export(PropertyHint.Range, "0,20,")]
    public int Number { get; set; }

Cho phép các giá trị integer từ -10 đến 20.

.. code-block:: csharp

    [Export(PropertyHint.Range, "-10,20,")]
    public int Number { get; set; }

Cho phép các giá trị float từ -10 đến 20 và snap giá trị theo các bội số của 0.2.

.. code-block:: csharp

    [Export(PropertyHint.Range, "-10,20,0.2")]
    public float Number { get; set; }

Nếu thêm các hint "or_greater" và/hoặc "or_less", bạn có thể vượt quá hoặc thấp hơn các giới hạn khi điều chỉnh giá trị bằng cách nhập trực tiếp thay vì sử dụng thanh trượt.

.. code-block:: csharp

    [Export(PropertyHint.Range, "0,100,1,or_greater,or_less")]
    public int Number { get; set; }

Float với hint easing
---------------------

Hiển thị biểu diễn trực quan của hàm :ref:`ease<class_@GlobalScope_method_ease>` khi chỉnh sửa.

.. code-block:: csharp

    [Export(PropertyHint.ExpEasing)]
    public float TransitionSpeed { get; set; }

Export với hint hậu tố
----------------------

Hiển thị hậu tố hint đơn vị cho các biến được export. Hoạt động với các kiểu số, chẳng hạn như float hoặc vector:

.. code-block:: csharp

    [Export(PropertyHint.None, "suffix:m/s\u00b2")]
    public float Gravity { get; set; } = 9.8f;
    [Export(PropertyHint.None, "suffix:m/s")]
    public Vector3 Velocity { get; set; }

Trong ví dụ trên, ``\u00b2`` được sử dụng để viết ký tự "bình phương" (``²``).

Màu sắc
-------

Màu thông thường được cung cấp dưới dạng giá trị red-green-blue-alpha.

.. code-block:: csharp

    [Export]
    public Color Color { get; set; }

Màu được cung cấp dưới dạng giá trị red-green-blue (alpha sẽ luôn là 1).

.. code-block:: csharp

    [Export(PropertyHint.ColorNoAlpha)]
    public Color Color { get; set; }

.. _doc_c_sharp_exports_nodes:

Node
----

Node cũng có thể được export trực tiếp mà không cần sử dụng NodePath.

.. code-block:: csharp

    [Export]
    public Node Node { get; set; }

Bạn cũng có thể export trực tiếp một kiểu node cụ thể. Danh sách node hiển thị sau khi nhấn "Assign" trong Inspector sẽ được lọc theo kiểu đã chỉ định và chỉ node chính xác mới có thể được gán.

.. code-block:: csharp

    [Export]
    public Sprite2D Sprite2D { get; set; }

Các custom node class cũng có thể được export trực tiếp. Hành vi lọc phụ thuộc vào việc custom class có phải là
:ref:`global class <doc_c_sharp_global_classes>`.

Vẫn có thể export NodePath như trong Godot 3.x nếu bạn cần:

.. code-block:: csharp

    [Export]
    public NodePath NodePath { get; set; }

    public override void _Ready()
    {
        var node = GetNode(NodePath);
    }

Resource
--------

.. code-block:: csharp

    [Export]
    public Resource Resource { get; set; }

Sau đó, trong Inspector, bạn có thể kéo và thả một resource file từ dock FileSystem vào ô biến.

Tuy nhiên, việc mở dropdown của Inspector có thể dẫn đến một danh sách cực kỳ dài các class có thể tạo. Vì vậy, nếu bạn chỉ định một kiểu dẫn xuất từ Resource, chẳng hạn như:

.. code-block:: csharp

    [Export]
    public AnimationNode AnimationNode { get; set; }

Menu thả xuống sẽ chỉ giới hạn ở AnimationNode và tất cả các lớp dẫn xuất của nó. Các lớp resource tùy chỉnh cũng có thể được sử dụng, xem :ref:`doc_c_sharp_global_classes`.

Cần lưu ý rằng ngay cả khi script không chạy trong editor, các thuộc tính đã export vẫn có thể chỉnh sửa. Bạn có thể sử dụng điều này cùng với một :ref:`script ở chế độ "tool" <doc_gdscript_tool_mode>`.

Export các cờ bit
-----------------

Các member có kiểu là enum với thuộc tính ``[Flags]`` có thể được export và giá trị của chúng bị giới hạn trong các member của kiểu enum. Editor sẽ tạo một widget trong Inspector, cho phép chọn không, một hoặc nhiều member của enum. Giá trị sẽ được lưu dưới dạng số nguyên.

Một enum cờ sử dụng lũy thừa của 2 làm giá trị cho các member của enum. Các member kết hợp nhiều cờ bằng phép OR logic (``|``) cũng được hỗ trợ.

.. code-block:: csharp

    [Flags]
    public enum SpellElements
    {
        Fire = 1 << 1,
        Water = 1 << 2,
        Earth = 1 << 3,
        Wind = 1 << 4,

        FireAndWater = Fire | Water,
    }

    [Export]
    public SpellElements MySpellElements { get; set; }

Các số nguyên được sử dụng làm cờ bit có thể lưu trữ nhiều giá trị ``true``/``false`` (boolean) trong một thuộc tính. Bằng cách sử dụng gợi ý thuộc tính ``Flags``, mọi cờ đã cho đều có thể được thiết lập từ editor.

.. code-block:: csharp

    [Export(PropertyHint.Flags, "Fire,Water,Earth,Wind")]
    public int SpellElements { get; set; } = 0;

Bạn phải cung cấp mô tả dạng chuỗi cho mỗi cờ. Trong ví dụ này, ``Fire`` có giá trị 1, ``Water`` có giá trị 2, ``Earth`` có giá trị 4 và ``Wind`` tương ứng với giá trị 8. Thông thường, các hằng số nên được định nghĩa tương ứng (ví dụ: ``private const int ElementWind = 8`` và vân vân).

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

.. code-block:: csharp

    [Export(PropertyHint.Flags, "Self:4,Allies:8,Foes:16")]
    public int SpellTargets { get; set; } = 0;

Chỉ các giá trị là lũy thừa của 2 mới hợp lệ làm tùy chọn cờ bit. Giá trị nhỏ nhất được phép là 1, vì 0 có nghĩa là không có gì được chọn. Bạn cũng có thể thêm các tùy chọn là tổ hợp của những cờ khác:

.. code-block:: csharp

    [Export(PropertyHint.Flags, "Self:4,Allies:8,Self and Allies:12,Foes:16")]
    public int SpellTargets { get; set; } = 0;

Các annotation export cũng được cung cấp cho các layer physics và render được định nghĩa trong project settings.

.. code-block:: csharp

    [Export(PropertyHint.Layers2DPhysics)]
    public uint Layers2DPhysics { get; set; }
    [Export(PropertyHint.Layers2DRender)]
    public uint Layers2DRender { get; set; }
    [Export(PropertyHint.Layers3DPhysics)]
    public uint Layers3DPhysics { get; set; }
    [Export(PropertyHint.Layers3DRender)]
    public uint Layers3DRender { get; set; }

Việc sử dụng cờ bit đòi hỏi một số hiểu biết về các phép toán bit. Nếu không chắc chắn, hãy sử dụng các biến boolean thay thế.

Export enum
-----------

Các member có kiểu là enum có thể được export và giá trị của chúng bị giới hạn trong các member của kiểu enum. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau dưới dạng "Thing 1", "Thing 2", "Another Thing". Giá trị sẽ được lưu dưới dạng số nguyên.

.. code-block:: csharp

    public enum MyEnum
    {
        Thing1,
        Thing2,
        AnotherThing = -1,
    }

    [Export]
    public MyEnum MyEnumCurrent { get; set; }

Các member kiểu số nguyên và chuỗi cũng có thể bị giới hạn trong một danh sách giá trị cụ thể bằng annotation ``[Export]`` với gợi ý ``PropertyHint.Enum``. Editor sẽ tạo một widget trong Inspector, liệt kê các mục sau: Warrior, Magician, Thief. Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn được chọn (tức là ``0``, ``1`` hoặc ``2``).

.. code-block:: csharp

    [Export(PropertyHint.Enum, "Warrior,Magician,Thief")]
    public int CharacterClass { get; set; }

Bạn có thể thêm các giá trị tường minh bằng dấu hai chấm:

.. code-block:: csharp

    [Export(PropertyHint.Enum, "Slow:30,Average:60,Very Fast:200")]
    public int CharacterSpeed { get; set; }

Nếu kiểu là ``string``, giá trị sẽ được lưu dưới dạng chuỗi.

.. code-block:: csharp

    [Export(PropertyHint.Enum, "Rebecca,Mary,Leah")]
    public string CharacterName { get; set; }

Nếu muốn đặt giá trị ban đầu, bạn phải chỉ định giá trị đó một cách tường minh:

.. code-block:: csharp

    [Export(PropertyHint.Enum, "Rebecca,Mary,Leah")]
    public string CharacterName { get; set; } = "Rebecca";


Export các nút Inspector bằng ``[ExportToolButton]``
----------------------------------------------------

Nếu muốn tạo một nút có thể nhấp trong inspector, bạn có thể sử dụng thuộc tính ``[ExportToolButton]``. Thuộc tính hoặc field Callable này sẽ được export dưới dạng một nút có thể nhấp. Vì thao tác này chạy trong editor, bắt buộc phải sử dụng thuộc tính :ref:`[Tool] <doc_running_code_in_the_editor>`. Khi nhấn nút, callable sẽ được gọi:

.. code-block:: csharp

    [Tool]
    public partial class MyNode : Node
    {
        [ExportToolButton("Click me!")]
        public Callable ClickMeButton => Callable.From(ClickMe);

        public void ClickMe()
        {
            GD.Print("Hello world!");
        }
    }

Bạn cũng có thể đặt biểu tượng cho nút bằng đối số thứ hai. Nếu được chỉ định, một biểu tượng sẽ được lấy thông qua :ref:`GetThemeIcon() <class_Control_method_get_theme_icon>`, từ loại theme ``"EditorIcons"``.

.. code-block:: csharp

    [ExportToolButton("Click me!", Icon = "CharacterBody2D")]
    public Callable ClickMeButton => Callable.From(ClickMe);

Export collection
-----------------

Như đã giải thích trong tài liệu :ref:`C# Variant <doc_c_sharp_variant>`, chỉ một số mảng C# nhất định và các kiểu collection được định nghĩa trong namespace ``Godot.Collections`` tương thích với Variant, vì vậy chỉ những kiểu đó mới có thể được export.

Export mảng Godot
~~~~~~~~~~~~~~~~~

.. code-block:: csharp

    [Export]
    public Godot.Collections.Array Array { get; set; }

Việc sử dụng ``Godot.Collections.Array<T>`` generic cho phép chỉ định kiểu của các phần tử mảng, kiểu này sẽ được dùng làm gợi ý cho editor. Inspector sẽ giới hạn các phần tử ở kiểu đã chỉ định.

.. code-block:: csharp

    [Export]
    public Godot.Collections.Array<string> Array { get; set; }

Giá trị mặc định của các mảng Godot là null. Có thể chỉ định một giá trị mặc định khác:

.. code-block:: csharp

    [Export]
    public Godot.Collections.Array<string> CharacterNames { get; set; } =
    [
        "Rebecca",
        "Mary",
        "Leah",
    ];

Các mảng có kiểu được chỉ định, trong đó kiểu này kế thừa từ resource, có thể được thiết lập bằng cách kéo và thả nhiều tệp từ dock FileSystem.

.. code-block:: csharp

    [Export]
    public Godot.Collections.Array<Texture> Textures { get; set; }

    [Export]
    public Godot.Collections.Array<PackedScene> Scenes { get; set; }

Export dictionary Godot
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: csharp

    [Export]
    public Godot.Collections.Dictionary Dictionary { get; set; }

Việc sử dụng ``Godot.Collections.Dictionary<TKey, TValue>`` generic cho phép chỉ định kiểu của các phần tử key và value của dictionary.

.. code-block:: csharp

    [Export]
    public Godot.Collections.Dictionary<string, int> Dictionary { get; set; }

Giá trị mặc định của các dictionary Godot là null. Có thể chỉ định một giá trị mặc định khác:

.. code-block:: csharp

    [Export]
    public Godot.Collections.Dictionary<string, int> CharacterLives { get; set; } = new Godot.Collections.Dictionary<string, int>
    {
        ["Rebecca"] = 10,
        ["Mary"] = 42,
        ["Leah"] = 0,
    };

Export mảng C#
~~~~~~~~~~~~~~

Các mảng C# có thể được export miễn là kiểu phần tử là kiểu :ref:`Variant-compatible type <c_sharp_variant_compatible_types>`.

.. code-block:: csharp

    [Export]
    public Vector3[] Vectors { get; set; }

    [Export]
    public NodePath[] NodePaths { get; set; }

Giá trị mặc định của các mảng C# là null. Có thể chỉ định một giá trị mặc định khác:

.. code-block:: csharp

    [Export]
    public Vector3[] Vectors { get; set; } =
    [
        new Vector3(1, 2, 3),
        new Vector3(3, 2, 1),
    ];

Thiết lập các biến đã export từ tool script
-------------------------------------------

Khi thay đổi giá trị của một biến đã export từ một script trong
:ref:`doc_gdscript_tool_mode`, giá trị trong inspector sẽ không được cập nhật tự động. Để cập nhật, hãy gọi
:ref:`NotifyPropertyListChanged() <class_Object_method_notify_property_list_changed>` sau khi thiết lập giá trị của biến đã export.

Export nâng cao
---------------

Không phải mọi kiểu export đều có thể được cung cấp ở cấp độ ngôn ngữ để tránh sự phức tạp không cần thiết trong thiết kế. Phần sau mô tả một số tính năng export ít hoặc nhiều phổ biến có thể được triển khai bằng API cấp thấp.

Trước khi đọc tiếp, bạn nên làm quen với cách các thuộc tính được xử lý và cách chúng có thể được tùy chỉnh bằng
:ref:`_Set() <class_Object_private_method__set>`,
:ref:`_Get() <class_Object_private_method__get>`, và
các phương thức :ref:`_GetPropertyList() <class_Object_private_method__get_property_list>` như được mô tả trong :ref:`doc_accessing_data_or_logic_from_object`.

.. seealso:: Để binding các thuộc tính bằng những phương thức trên trong C++, hãy xem
             :ref:`doc_binding_properties_using_set_get_property_list`.

.. warning:: Script phải hoạt động ở chế độ ``tool`` để các phương thức trên có thể hoạt động từ bên trong editor.

.. _`default value of the type`: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/default-values
