.. _doc_saving_games:

Lưu game
========

Giới thiệu
----------

Việc lưu game có thể phức tạp. Ví dụ: có thể cần lưu thông tin từ nhiều đối tượng trên nhiều level. Các hệ thống lưu game nâng cao nên cho phép lưu thêm thông tin về số lượng đối tượng tùy ý. Điều này giúp hàm lưu có thể mở rộng khi game trở nên phức tạp hơn.

.. note::

    Nếu bạn muốn lưu cấu hình người dùng, bạn có thể sử dụng
    :ref:`class_ConfigFile` class cho mục đích này.

.. seealso::

    Bạn có thể xem cách lưu và tải hoạt động trên thực tế trong dự án demo `Saving and Loading (Serialization) demo project <https://github.com/godotengine/godot-demo-projects/blob/master/loading/serialization>`__.

Xác định các đối tượng persistent
---------------------------------

Trước tiên, chúng ta cần xác định những đối tượng nào muốn giữ lại giữa các phiên chơi và muốn giữ lại thông tin nào từ những đối tượng đó. Trong tutorial này, chúng ta sẽ sử dụng groups để đánh dấu và xử lý các đối tượng cần lưu, nhưng chắc chắn vẫn có thể sử dụng các phương pháp khác.

Chúng ta sẽ bắt đầu bằng cách thêm các đối tượng muốn lưu vào group "Persist". Có thể thực hiện việc này thông qua GUI hoặc script. Hãy thêm các node liên quan bằng GUI:

.. image:: img/groups.webp

Sau khi hoàn tất, khi cần lưu game, chúng ta có thể lấy tất cả đối tượng cần lưu rồi yêu cầu tất cả chúng lưu bằng script này:

.. tabs::
 .. code-tab:: gdscript GDScript

    var save_nodes = get_tree().get_nodes_in_group("Persist")
    for node in save_nodes:
        # Bây giờ, chúng ta có thể gọi hàm lưu trên từng node.

 .. code-tab:: csharp

    var saveNodes = GetTree().GetNodesInGroup("Persist");
    foreach (Node saveNode in saveNodes)
    {
        // Bây giờ, chúng ta có thể gọi hàm lưu trên từng node.
    }


Tuần tự hóa
-----------

Bước tiếp theo là tuần tự hóa dữ liệu. Điều này giúp việc đọc dữ liệu và lưu dữ liệu vào đĩa dễ dàng hơn nhiều. Trong trường hợp này, chúng ta giả định mỗi thành viên của group Persist là một node được instance và do đó có một path. GDScript có helper class :ref:`JSON<class_json>` để chuyển đổi giữa dictionary và string. Node của chúng ta cần chứa một hàm save trả về dữ liệu này. Hàm save sẽ như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func save():
        var save_dict = {
            "filename" : get_scene_file_path(),
            "parent" : get_parent().get_path(),
            "pos_x" : position.x, # Vector2 không được JSON hỗ trợ
            "pos_y" : position.y,
            "attack" : attack,
            "defense" : defense,
            "current_health" : current_health,
            "max_health" : max_health,
            "damage" : damage,
            "regen" : regen,
            "experience" : experience,
            "tnl" : tnl,
            "level" : level,
            "attack_growth" : attack_growth,
            "defense_growth" : defense_growth,
            "health_growth" : health_growth,
            "is_alive" : is_alive,
            "last_attack" : last_attack
        }
        return save_dict

 .. code-tab:: csharp

    public Godot.Collections.Dictionary<string, Variant> Save()
    {
        return new Godot.Collections.Dictionary<string, Variant>()
        {
            { "Filename", SceneFilePath },
            { "Parent", GetParent().GetPath() },
            { "PosX", Position.X }, // Vector2 không được JSON hỗ trợ
            { "PosY", Position.Y },
            { "Attack", Attack },
            { "Defense", Defense },
            { "CurrentHealth", CurrentHealth },
            { "MaxHealth", MaxHealth },
            { "Damage", Damage },
            { "Regen", Regen },
            { "Experience", Experience },
            { "Tnl", Tnl },
            { "Level", Level },
            { "AttackGrowth", AttackGrowth },
            { "DefenseGrowth", DefenseGrowth },
            { "HealthGrowth", HealthGrowth },
            { "IsAlive", IsAlive },
            { "LastAttack", LastAttack }
        };
    }


Điều này cho chúng ta một dictionary có dạng ``{ "variable_name":value_of_variable }``, sẽ hữu ích khi tải.

Lưu và đọc dữ liệu
------------------

Như đã trình bày trong tutorial :ref:`doc_filesystem`, chúng ta cần mở một file để có thể ghi vào hoặc đọc từ đó. Giờ đã có cách gọi các group và lấy dữ liệu liên quan của chúng, hãy sử dụng class :ref:`JSON<class_json>` để chuyển dữ liệu thành một string dễ lưu trữ và lưu chúng vào một file. Làm theo cách này đảm bảo mỗi dòng là một đối tượng riêng, nhờ đó chúng ta cũng dễ dàng lấy dữ liệu từ file.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lưu ý: Có thể gọi hàm này từ bất kỳ đâu bên trong tree. Hàm này
    # không phụ thuộc vào path.
    # Duyệt qua mọi thứ trong category persist và yêu cầu chúng trả về một
    # dict chứa các biến liên quan.
    func save_game():
        var save_file = FileAccess.open("user://savegame.save", FileAccess.WRITE)
        var save_nodes = get_tree().get_nodes_in_group("Persist")
        for node in save_nodes:
            # Kiểm tra node có phải là một scene được instance để có thể instance lại trong quá trình tải.
            if node.scene_file_path.is_empty():
                print("persistent node '%s' is not an instanced scene, skipped" % node.name)
                continue

            # Kiểm tra node có hàm save.
            if !node.has_method("save"):
                print("persistent node '%s' is missing a save() function, skipped" % node.name)
                continue

            # Gọi hàm save của node.
            var node_data = node.call("save")

            # JSON cung cấp một static method để tuần tự hóa thành JSON string.
            var json_string = JSON.stringify(node_data)

            # Lưu dictionary cần lưu thành một dòng mới trong save file.
            save_file.store_line(json_string)

 .. code-tab:: csharp

    // Lưu ý: Có thể gọi hàm này từ bất kỳ đâu bên trong tree. Hàm này
    // không phụ thuộc vào path.
    // Duyệt qua mọi thứ trong category persist và yêu cầu chúng trả về một
    // dict chứa các biến liên quan.
    public void SaveGame()
    {
        using var saveFile = FileAccess.Open("user://savegame.save", FileAccess.ModeFlags.Write);

        var saveNodes = GetTree().GetNodesInGroup("Persist");
        foreach (Node saveNode in saveNodes)
        {
            // Kiểm tra node có phải là một scene được instance để có thể instance lại trong quá trình tải.
            if (string.IsNullOrEmpty(saveNode.SceneFilePath))
            {
                GD.Print($"persistent node '{saveNode.Name}' is not an instanced scene, skipped");
                continue;
            }

            // Kiểm tra node có hàm save.
            if (!saveNode.HasMethod("Save"))
            {
                GD.Print($"persistent node '{saveNode.Name}' is missing a Save() function, skipped");
                continue;
            }

            // Gọi hàm save của node.
            var nodeData = saveNode.Call("Save");

            // Json cung cấp một static method để tuần tự hóa thành JSON string.
            var jsonString = Json.Stringify(nodeData);

            // Lưu dictionary cần lưu thành một dòng mới trong save file.
            saveFile.StoreLine(jsonString);
        }
    }


Đã lưu game! Bây giờ, để tải, chúng ta sẽ đọc từng dòng. Sử dụng method :ref:`parse<class_JSON_method_parse>` để đọc JSON string trở lại thành dictionary, sau đó lặp qua dict để đọc các giá trị. Tuy nhiên, trước tiên chúng ta cần tạo đối tượng và có thể sử dụng các giá trị filename và parent để thực hiện việc đó. Đây là hàm load của chúng ta:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lưu ý: Có thể gọi hàm này từ bất kỳ đâu bên trong tree. Hàm này
    # không phụ thuộc vào path.
    func load_game():
        if not FileAccess.file_exists("user://savegame.save"):
            return # Lỗi! Không có save để tải.

        # Chúng ta cần hoàn nguyên trạng thái game để không clone các đối tượng
        # trong quá trình tải. Việc này sẽ thay đổi rất nhiều tùy theo nhu cầu của một
        # project, vì vậy hãy cẩn thận ở bước này.
        # Trong ví dụ này, chúng ta sẽ thực hiện bằng cách xóa các đối tượng có thể lưu.
        var save_nodes = get_tree().get_nodes_in_group("Persist")
        for i in save_nodes:
            i.queue_free()

        # Tải file từng dòng và xử lý dictionary đó để khôi phục
        # đối tượng mà nó biểu diễn.
        var save_file = FileAccess.open("user://savegame.save", FileAccess.READ)
        while save_file.get_position() < save_file.get_length():
            var json_string = save_file.get_line()

            # Tạo helper class để tương tác với JSON.
            var json = JSON.new()

            # Kiểm tra xem có lỗi nào khi parse JSON string không; bỏ qua nếu thất bại.
            var parse_result = json.parse(json_string)
            if not parse_result == OK:
                print("JSON Parse Error: ", json.get_error_message(), " in ", json_string, " at line ", json.get_error_line())
                continue

            # Lấy dữ liệu từ JSON object.
            var node_data = json.data

            # Trước tiên, chúng ta cần tạo đối tượng, thêm đối tượng vào cây và đặt vị trí cho đối tượng.
            var new_object = load(node_data["filename"]).instantiate()
            get_node(node_data["parent"]).add_child(new_object)
            new_object.position = Vector2(node_data["pos_x"], node_data["pos_y"])

            # Bây giờ, chúng ta thiết lập các biến còn lại.
            for i in node_data.keys():
                if i == "filename" or i == "parent" or i == "pos_x" or i == "pos_y":
                    continue
                new_object.set(i, node_data[i])

 .. code-tab:: csharp

    // Lưu ý: Có thể gọi hàm này từ bất kỳ đâu bên trong tree. Hàm này
    // không phụ thuộc vào path.
    public void LoadGame()
    {
        if (!FileAccess.FileExists("user://savegame.save"))
        {
            return; // Lỗi! Chúng ta không có bản lưu nào để tải.
        }

        // Chúng ta cần khôi phục trạng thái trò chơi để không nhân bản các đối tượng trong khi tải.
        // Điều này sẽ thay đổi rất nhiều tùy thuộc vào nhu cầu của dự án, vì vậy hãy cẩn thận với
        // bước này.
        // Trong ví dụ này, chúng ta sẽ thực hiện việc đó bằng cách xóa các đối tượng có thể lưu.
        var saveNodes = GetTree().GetNodesInGroup("Persist");
        foreach (Node saveNode in saveNodes)
        {
            saveNode.QueueFree();
        }

        // Tải tệp theo từng dòng và xử lý dictionary đó để khôi phục đối tượng
        // mà nó biểu diễn.
        using var saveFile = FileAccess.Open("user://savegame.save", FileAccess.ModeFlags.Read);

        while (saveFile.GetPosition() < saveFile.GetLength())
        {
            var jsonString = saveFile.GetLine();

            // Tạo lớp trợ giúp để tương tác với JSON.
            var json = new Json();
            var parseResult = json.Parse(jsonString);
            if (parseResult != Error.Ok)
            {
                GD.Print($"JSON Parse Error: {json.GetErrorMessage()} in {jsonString} at line {json.GetErrorLine()}");
                continue;
            }

            // Lấy dữ liệu từ đối tượng JSON.
            var nodeData = new Godot.Collections.Dictionary<string, Variant>((Godot.Collections.Dictionary)json.Data);

            // Trước tiên, chúng ta cần tạo đối tượng, thêm đối tượng vào cây và đặt vị trí cho đối tượng.
            var newObjectScene = GD.Load<PackedScene>(nodeData["Filename"].ToString());
            var newObject = newObjectScene.Instantiate<Node>();
            GetNode(nodeData["Parent"].ToString()).AddChild(newObject);
            newObject.Set(Node2D.PropertyName.Position, new Vector2((float)nodeData["PosX"], (float)nodeData["PosY"]));

            // Bây giờ, chúng ta thiết lập các biến còn lại.
            foreach (var (key, value) in nodeData)
            {
                if (key == "Filename" || key == "Parent" || key == "PosX" || key == "PosY")
                {
                    continue;
                }
                newObject.Set(key, value);
            }
        }
    }


Giờ đây, chúng ta có thể lưu và tải một số lượng tùy ý các đối tượng được bố trí gần như ở bất kỳ đâu trong cây cảnh! Mỗi đối tượng có thể lưu dữ liệu khác nhau tùy theo những gì nó cần lưu.

Một số lưu ý
------------

Chúng ta đã lướt qua việc thiết lập trạng thái trò chơi để tải. Cuối cùng, vị trí của phần lớn logic này hoàn toàn tùy thuộc vào người tạo dự án. Việc này thường phức tạp và sẽ cần được tùy chỉnh đáng kể dựa trên nhu cầu của từng dự án.

Ngoài ra, phần triển khai của chúng ta giả định rằng không có đối tượng Persist nào là con của một đối tượng Persist khác. Nếu không, các đường dẫn không hợp lệ sẽ được tạo. Để hỗ trợ các đối tượng Persist lồng nhau, hãy cân nhắc việc lưu các đối tượng theo từng giai đoạn. Trước tiên, hãy tải các đối tượng cha để chúng khả dụng cho lệnh gọi :ref:`add_child() <class_node_method_add_child>` khi tải các đối tượng con. Bạn cũng sẽ cần một cách để liên kết các đối tượng con với đối tượng cha, vì :ref:`NodePath <class_nodepath>` nhiều khả năng sẽ không hợp lệ.

JSON so với serialization nhị phân
----------------------------------

Đối với trạng thái trò chơi đơn giản, JSON có thể phù hợp và tạo ra các tệp mà con người có thể đọc, đồng thời dễ debug.

Tuy nhiên, JSON có nhiều hạn chế. Nếu cần lưu trữ trạng thái trò chơi phức tạp hơn hoặc một lượng lớn dữ liệu, :ref:`binary serialization <doc_binary_serialization_api>` có thể là lựa chọn tốt hơn.

Các hạn chế của JSON
~~~~~~~~~~~~~~~~~~~~

Dưới đây là một số vấn đề quan trọng cần biết khi sử dụng JSON.

* **Kích thước tệp:** JSON lưu trữ dữ liệu ở định dạng văn bản, lớn hơn nhiều so với các định dạng nhị phân.
* **Kiểu dữ liệu:** JSON chỉ cung cấp một tập hợp kiểu dữ liệu giới hạn. Nếu có các kiểu dữ liệu mà JSON không hỗ trợ, bạn sẽ cần chuyển đổi dữ liệu của mình sang và từ các kiểu mà JSON có thể xử lý. Ví dụ, một số kiểu quan trọng mà JSON không thể phân tích cú pháp là: ``Vector2``, ``Vector3``, ``Color``, ``Rect2`` và ``Quaternion``.
* **Cần logic tùy chỉnh để mã hóa/giải mã:** Nếu có bất kỳ lớp tùy chỉnh nào muốn lưu trữ bằng JSON, bạn sẽ cần tự viết logic để mã hóa và giải mã các lớp đó.

Serialization nhị phân
~~~~~~~~~~~~~~~~~~~~~~

:ref:`Binary serialization <doc_binary_serialization_api>` là một phương pháp thay thế để lưu trữ trạng thái trò chơi, và bạn có thể sử dụng nó với các hàm ``get_var`` và ``store_var`` của :ref:`class_FileAccess`.

* Binary serialization sẽ tạo ra các tệp nhỏ hơn JSON.
* Binary serialization có thể xử lý hầu hết các kiểu dữ liệu phổ biến.
* Binary serialization cần ít logic tùy chỉnh hơn để mã hóa và giải mã các lớp tùy chỉnh.

Lưu ý rằng không phải tất cả thuộc tính đều được đưa vào. Chỉ các thuộc tính được cấu hình với cờ :ref:`PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>` được bật mới được serialize. Bạn có thể thêm cờ usage mới cho một thuộc tính bằng cách override
:ref:`_get_property_list<class_Object_private_method__get_property_list>` method trong lớp của bạn. Bạn cũng có thể kiểm tra cách cấu hình usage của thuộc tính bằng cách gọi ``Object._get_property_list``. Xem :ref:`PropertyUsageFlags <enum_@GlobalScope_PropertyUsageFlags>` để biết các cờ usage khả dụng.
