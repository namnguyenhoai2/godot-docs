.. _doc_resources:

Tài nguyên
==========

Node và tài nguyên
------------------

Cho đến tutorial này, chúng ta tập trung vào class :ref:`Node <class_Node>` trong Godot vì đây là class được dùng để lập trình hành vi và hầu hết tính năng của engine đều dựa vào nó. Có một kiểu dữ liệu khác cũng quan trọng không kém:
:ref:`Resource <class_Resource>`.

*Node* cung cấp chức năng: chúng vẽ sprite, model 3D, mô phỏng vật lý, sắp xếp giao diện người dùng, v.v. **Resource** là **các vùng chứa dữ liệu**. Chúng không tự làm gì cả; thay vào đó, node sử dụng dữ liệu chứa trong resource.

Bất kỳ thứ gì Godot lưu hoặc tải từ ổ đĩa đều là một resource. Có thể là một scene (tệp ``.tscn`` hoặc ``.scn``), một hình ảnh, một script... Dưới đây là một số ví dụ :ref:`Resource <class_Resource>`:

- :ref:`Texture <class_Texture>` - :ref:`Script <class_Script>` - :ref:`Mesh <class_Mesh>` - :ref:`Animation <class_Animation>` - :ref:`AudioStream <class_AudioStream>` - :ref:`Font <class_Font>` - :ref:`Translation <class_Translation>`

Khi engine tải một resource từ ổ đĩa, **nó chỉ tải resource đó một lần**. Nếu một bản sao của resource đó đã có trong bộ nhớ, việc tải lại resource sẽ luôn trả về cùng bản sao đó. Vì resource chỉ chứa dữ liệu nên không cần tạo bản sao cho chúng.

Mọi object, dù là Node hay Resource, đều có thể export các property. Có nhiều kiểu Property, như String, integer, Vector2, v.v., và bất kỳ kiểu nào trong số này cũng có thể trở thành một resource. Điều này có nghĩa là cả node và resource đều có thể chứa resource dưới dạng property:

.. image:: img/nodes_resources.webp

Bên ngoài và tích hợp sẵn
-------------------------

Có hai cách để lưu resource. Chúng có thể là:

1. **External**, nằm bên ngoài scene và được lưu trên ổ đĩa dưới dạng các tệp riêng lẻ. 2. **Built-in**, được lưu bên trong tệp ``.tscn`` hoặc ``.scn`` mà chúng được gắn vào.

Cụ thể hơn, đây là một :ref:`Texture2D <class_Texture2D>` trong một node :ref:`Sprite2D <class_Sprite2D>`:

.. image:: img/spriteprop.webp

Nhấp vào phần xem trước resource cho phép chúng ta xem các property của resource.

.. image:: img/resourcerobi.webp

Property path cho biết resource bắt nguồn từ đâu. Trong trường hợp này, nó bắt nguồn từ một hình ảnh PNG có tên ``robi.png``. Khi resource đến từ một tệp như vậy, đó là external resource. Nếu bạn xóa path hoặc path này để trống, nó sẽ trở thành built-in resource.

Việc chuyển đổi giữa built-in resource và external resource xảy ra khi bạn lưu scene. Trong ví dụ trên, nếu bạn xóa path ``"res://robi.png"`` rồi lưu, Godot sẽ lưu hình ảnh bên trong tệp scene ``.tscn``.

.. note::

    Ngay cả khi bạn lưu một built-in resource, khi instance một scene nhiều lần, engine cũng chỉ tải một bản sao của resource đó.

Tải resource từ code
--------------------

Có hai cách để tải resource từ code. Trước tiên, bạn có thể sử dụng hàm ``load()`` bất cứ lúc nào:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        # Godot tải Resource khi đọc chính dòng này.
        var imported_resource = load("res://robi.png")
        $sprite.texture = imported_resource

 .. code-tab:: csharp

    public override void _Ready()
    {
        // Godot tải Resource khi thực thi dòng này.
        var texture = GD.Load<Texture>("res://Robi.png");
        var sprite = GetNode<Sprite2D>("sprite");
        sprite.Texture = texture;
    }

Bạn cũng có thể ``preload`` resource. Không giống ``load``, hàm này sẽ đọc tệp từ ổ đĩa và tải tệp tại thời điểm compile. Do đó, bạn không thể gọi ``preload`` với một path dạng biến: bạn cần sử dụng một chuỗi hằng.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        # Godot tải resource tại thời điểm compile
        var imported_resource = preload("res://robi.png")
        get_node("sprite").texture = imported_resource

 .. code-tab:: csharp

    // 'preload()' không khả dụng trong C Sharp.

Tải scene
---------

Scene cũng là resource, nhưng có một điểm cần lưu ý. Scene được lưu trên ổ đĩa là các resource thuộc kiểu :ref:`PackedScene <class_PackedScene>`. Scene được đóng gói bên trong một :ref:`Resource <class_Resource>`.

Để lấy một instance của scene, bạn phải sử dụng
:ref:`PackedScene.instantiate() <class_PackedScene_method_instantiate>` method.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_shoot():
            var bullet = preload("res://bullet.tscn").instantiate()
            add_child(bullet)


 .. code-tab:: csharp

    private PackedScene _bulletScene = GD.Load<PackedScene>("res://Bullet.tscn");

    private void OnShoot()
    {
        Node bullet = _bulletScene.Instantiate();
        AddChild(bullet);
    }

Phương thức này tạo các node trong hệ phân cấp của scene, cấu hình chúng và trả về node gốc của scene. Sau đó, bạn có thể thêm nó làm node con của bất kỳ node nào khác.

Cách tiếp cận này có một số ưu điểm. Vì hàm :ref:`PackedScene.instantiate() <class_PackedScene_method_instantiate>` rất nhanh, bạn có thể tạo enemy, đạn, hiệu ứng mới, v.v. mà không phải tải lại chúng từ ổ đĩa mỗi lần. Hãy nhớ rằng, như mọi khi, hình ảnh, mesh, v.v. đều được dùng chung giữa các instance của scene.

Giải phóng resource
-------------------

Khi một :ref:`Resource <class_Resource>` không còn được sử dụng, nó sẽ tự động tự giải phóng. Vì trong hầu hết trường hợp, Resource được chứa trong Node, khi bạn giải phóng một node, engine cũng sẽ giải phóng tất cả resource mà node đó sở hữu nếu không có node nào khác sử dụng chúng.

Tạo resource của riêng bạn
--------------------------

Giống như mọi Object trong Godot, người dùng cũng có thể viết script cho Resource. Resource script kế thừa khả năng chuyển đổi tự do giữa các property của object và văn bản hoặc dữ liệu nhị phân được serialize (\*.tres, \*.res). Chúng cũng kế thừa cơ chế quản lý bộ nhớ reference-counting từ kiểu RefCounted.

Điều này mang lại nhiều ưu điểm riêng biệt so với các cấu trúc dữ liệu thay thế như JSON, CSV hoặc tệp TXT tùy chỉnh. Người dùng chỉ có thể import các asset này dưới dạng :ref:`Dictionary <class_Dictionary>` (JSON) hoặc dưới dạng một
:ref:`FileAccess <class_FileAccess>` to parse. What sets Resources apart is their
kế thừa các tính năng của :ref:`Object <class_Object>`, :ref:`RefCounted <class_RefCounted>` và :ref:`Resource <class_Resource>`:

- Chúng có thể định nghĩa các hằng số, vì vậy không cần đến các hằng số từ những trường dữ liệu hoặc object khác.

- Chúng có thể định nghĩa các method, bao gồm method setter/getter cho property. Điều này cho phép trừu tượng hóa và đóng gói dữ liệu bên dưới. Nếu cấu trúc của Resource script cần thay đổi, game sử dụng Resource cũng không cần phải thay đổi theo.

- Chúng có thể định nghĩa signal, nhờ đó Resource có thể kích hoạt phản hồi trước những thay đổi trong dữ liệu mà chúng quản lý.

- Chúng có các property được định nghĩa, vì vậy người dùng biết chắc 100% rằng dữ liệu của họ sẽ tồn tại.

- Tính năng auto-serialization và deserialization cho Resource được tích hợp sẵn trong Godot Engine. Người dùng không cần triển khai logic tùy chỉnh để import/export dữ liệu của một tệp resource.

- Resource thậm chí có thể serialize đệ quy các sub-Resource, nghĩa là người dùng có thể thiết kế các cấu trúc dữ liệu phức tạp hơn nữa.

- Người dùng có thể lưu Resource dưới dạng các tệp văn bản thân thiện với version control (\*.tres). Khi export game, Godot serialize các tệp resource thành tệp nhị phân (\*.res) để tăng tốc độ và khả năng nén.

- Inspector của Godot Engine có thể hiển thị và chỉnh sửa các tệp Resource ngay khi cài đặt. Do đó, người dùng thường không cần triển khai logic tùy chỉnh để trực quan hóa hoặc chỉnh sửa dữ liệu. Để làm vậy, hãy nhấp đúp vào tệp resource trong dock FileSystem hoặc nhấp vào biểu tượng thư mục trong Inspector rồi mở tệp trong hộp thoại.

- Chúng có thể mở rộng **các** kiểu resource khác chứ không chỉ kiểu Resource cơ sở.

Godot giúp dễ dàng tạo Resource tùy chỉnh trong Inspector.

1. Tạo một object Resource mới trong Inspector. Đây thậm chí có thể là một kiểu kế thừa từ Resource, miễn là script của bạn đang mở rộng kiểu đó. 2. Đặt property ``script`` trong Inspector thành script của bạn.

Inspector giờ sẽ hiển thị các property tùy chỉnh của Resource script. Nếu bạn chỉnh sửa các giá trị đó rồi lưu resource, Inspector cũng sẽ serialize các property tùy chỉnh! Để lưu resource từ Inspector, hãy nhấp vào biểu tượng lưu ở đầu Inspector rồi chọn "Save" hoặc "Save As...".

Nếu ngôn ngữ của script hỗ trợ :ref:`script classes <doc_gdscript_basics_class_name>`, quy trình sẽ được đơn giản hóa. Chỉ cần định nghĩa tên cho script là đủ để thêm script vào hộp thoại tạo của Inspector. Script của bạn sẽ được tự động thêm vào object Resource mà bạn tạo.

Hãy xem một vài ví dụ. Tạo một :ref:`Resource <class_Resource>` và đặt tên là ``bot_stats``. Nó sẽ xuất hiện trong tab tệp của bạn với tên đầy đủ là ``bot_stats.tres``. Không có script thì nó vô dụng, vì vậy hãy thêm một ít dữ liệu và logic! Gắn một script có tên ``bot_stats.gd`` vào nó (hoặc chỉ cần tạo một script mới rồi kéo script đó vào).

.. note::
    Để class resource mới xuất hiện trong GUI Create Resource, bạn cần cung cấp tên class cho GDScript hoặc sử dụng attribute [GlobalClass] trong C#.

.. tabs::
  .. code-tab:: gdscript GDScript

    class_name BotStats
    extends Resource

    @export var health: int
    @export var sub_resource: Resource
    @export var strings: PackedStringArray

    # Hãy đảm bảo mọi parameter đều có giá trị mặc định.
    # Nếu không, việc tạo và chỉnh sửa
    # resource của bạn thông qua inspector sẽ gặp vấn đề.
    func _init(p_health = 0, p_sub_resource = null, p_strings = []):
        health = p_health
        sub_resource = p_sub_resource
        strings = p_strings

  .. code-tab:: csharp

        // BotStats.cs
        using Godot;

        namespace ExampleProject
        {
            [GlobalClass]
            public partial class BotStats : Resource
            {
                [Export]
                public int Health { get; set; }

                [Export]
                public Resource SubResource { get; set; }

                [Export]
                public string[] Strings { get; set; }

                // Hãy đảm bảo bạn cung cấp một constructor không có parameter.
                // Trong C#, constructor không có parameter khác với
                // constructor có tất cả giá trị mặc định.
                // Nếu không có constructor không có parameter, Godot sẽ gặp vấn đề khi
                // tạo và chỉnh sửa resource của bạn thông qua inspector.
                public BotStats() : this(0, null, null) {}

                public BotStats(int health, Resource subResource, string[] strings)
                {
                    Health = health;
                    SubResource = subResource;
                    Strings = strings ?? System.Array.Empty<string>();
                }
            }
        }

Bây giờ, hãy tạo một :ref:`CharacterBody3D <class_CharacterBody3D>`, đặt tên là ``Bot`` và thêm script sau vào đó:

.. tabs::
  .. code-tab:: gdscript GDScript

    extends CharacterBody3D

    @export var stats: Resource

    func _ready():
        # Sử dụng interface implicit, kiểu duck-typed cho mọi resource tương thích với 'health'.
        if stats:
            stats.health = 10
            print(stats.health)
            # In "10"

  .. code-tab:: csharp

        // Bot.cs
        using Godot;

        namespace ExampleProject
        {
            public partial class Bot : CharacterBody3D
            {
                [Export]
                public Resource Stats;

                public override void _Ready()
                {
                    if (Stats is BotStats botStats)
                    {
                        GD.Print(botStats.Health); // In '10'.
                    }
                }
            }
        }

Bây giờ, hãy chọn node :ref:`CharacterBody3D <class_CharacterBody3D>` mà chúng ta đã đặt tên là ``bot``, rồi kéo và thả resource ``bot_stats.tres`` vào Inspector. Nó sẽ in ra 10! Rõ ràng, cách thiết lập này có thể được dùng cho các tính năng nâng cao hơn thế, nhưng miễn là bạn thực sự hiểu *cách* mọi thứ hoạt động, bạn sẽ có thể tự tìm hiểu mọi điều khác liên quan đến Resource.

.. note::

    Resource script tương tự như ScriptableObject của Unity. Inspector cung cấp hỗ trợ tích hợp sẵn cho resource tùy chỉnh. Tuy nhiên, nếu muốn, người dùng thậm chí có thể tự thiết kế các tool script dựa trên Control và kết hợp chúng với một :ref:`EditorPlugin <class_EditorPlugin>` để tạo các trình chỉnh sửa và phần trực quan hóa tùy chỉnh cho dữ liệu của mình.

    DataTable và CurveTable của Unreal Engine cũng dễ dàng được tái tạo bằng Resource script. DataTable là một String được ánh xạ tới một struct tùy chỉnh, tương tự như một Dictionary ánh xạ String tới một Resource script tùy chỉnh thứ cấp.

    .. tabs::
      .. code-tab:: gdscript GDScript

        # bot_stats_table.gd
        extends Resource

        const BotStats = preload("bot_stats.gd")

        var data = {
            "GodotBot": BotStats.new(10), # Tạo instance với 10 health.
            "DifferentBot": BotStats.new(20) # Một instance khác với 20 health.
        }

        func _init():
            print(data)
      .. code-tab:: csharp

        using Godot;

        [GlobalClass]
        public partial class BotStatsTable : Resource
        {
            private Godot.Collections.Dictionary<string, BotStats> _stats = new Godot.Collections.Dictionary<string, BotStats>();

            public BotStatsTable()
            {
                _stats["GodotBot"] = new BotStats(10); // Tạo instance với 10 health.
                _stats["DifferentBot"] = new BotStats(20); // Một cái khác có 20 máu.
                GD.Print(_stats);
            }
        }

    Thay vì nhúng trực tiếp các giá trị Dictionary, cũng có thể:

    1. Import một bảng giá trị từ spreadsheet và tạo các cặp key-value này.

    2. Thiết kế một visualization trong editor và tạo một plugin để thêm nó vào Inspector khi bạn mở các loại Resources này.

    CurveTables are the same thing, except mapped to an Array of float values or a :ref:`Curve <class_Curve>`/:ref:`Curve2D <class_Curve2D>` resource object.

.. warning::

    Hãy lưu ý rằng các resource file (\*.tres/\*.res) sẽ lưu đường dẫn của script mà chúng sử dụng trong file. Khi được load, chúng sẽ tìm nạp và load script này như một phần mở rộng của kiểu dữ liệu. Điều này có nghĩa là việc cố gắng gán một inner class của một script (tức là sử dụng keyword ``class`` trong GDScript) sẽ không hoạt động. Godot sẽ không serialize đúng các thuộc tính tùy chỉnh trên inner class của script.

    Trong ví dụ dưới đây, Godot sẽ load script ``Node``, nhận thấy rằng script này không extends ``Resource``, rồi xác định rằng script không load được cho Resource object vì các kiểu dữ liệu không tương thích.

    .. tabs::
      .. code-tab:: gdscript GDScript

        extends Node

        class MyResource:
            extends Resource
            @export var value = 5

        func _ready():
            var my_res = MyResource.new()

            # Điều này sẽ KHÔNG serialize thuộc tính 'value'.
            ResourceSaver.save(my_res, "res://my_res.tres")
      .. code-tab:: csharp

        using Godot;

        public partial class MyNode : Node
        {
            [GlobalClass]
            public partial class MyResource : Resource
            {
                [Export]
                public int Value { get; set; } = 5;
            }

            public override void _Ready()
            {
                var res = new MyResource();

                // Điều này sẽ KHÔNG serialize thuộc tính 'Value'.
                ResourceSaver.Save(res, "res://MyRes.tres");
            }
        }
