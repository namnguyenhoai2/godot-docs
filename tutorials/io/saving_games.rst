.. _doc_saving_games:

Lưu game
========

Giới thiệu
----------

Việc lưu game có thể phức tạp. Ví dụ, có thể cần lưu thông tin từ nhiều object trên nhiều level. Các hệ thống lưu game nâng cao nên cho phép bổ sung thông tin cho một số lượng object tùy ý. Điều này cho phép hàm lưu mở rộng khi game trở nên phức tạp hơn.

.. note::

    Nếu bạn muốn lưu cấu hình người dùng, bạn có thể sử dụng
    :ref:`class_ConfigFile` class for this purpose.

.. seealso::

    Bạn có thể xem cách lưu và tải hoạt động thực tế bằng cách sử dụng `Saving and Loading (Serialization) demo project <https://github.com/godotengine/godot-demo-projects/blob/master/loading/serialization>`__.

Xác định các object persistent
------------------------------

Trước tiên, chúng ta cần xác định những object nào muốn giữ lại giữa các phiên chơi game và thông tin nào muốn giữ từ các object đó. Trong tutorial này, chúng ta sẽ sử dụng các group để đánh dấu và xử lý những object cần lưu, nhưng chắc chắn vẫn có thể dùng các phương pháp khác.

Chúng ta sẽ bắt đầu bằng cách thêm các object muốn lưu vào group "Persist". Có thể thực hiện việc này thông qua GUI hoặc script. Hãy thêm các node liên quan bằng GUI:

.. image:: img/groups.webp

Sau khi hoàn tất, khi cần lưu game, chúng ta có thể lấy tất cả object để lưu chúng, sau đó yêu cầu tất cả chúng lưu bằng script này:

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


Serialization
-------------

Bước tiếp theo là serialize dữ liệu. Điều này giúp việc đọc dữ liệu và lưu dữ liệu vào disk dễ dàng hơn nhiều. Trong trường hợp này, chúng ta giả định mỗi thành viên của group Persist là một node đã được instantiate và do đó có một path. GDScript có helper class :ref:`JSON<class_json>` để chuyển đổi giữa dictionary và string. Node của chúng ta cần có một hàm save trả về dữ liệu này. Hàm save sẽ như sau:

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


Điều này cho chúng ta một dictionary có dạng ``{ "variable_name":value_of_variable }``, sẽ hữu ích khi loading.

Lưu và đọc dữ liệu
------------------

Như đã trình bày trong tutorial :ref:`doc_filesystem`, chúng ta cần mở một file để có thể ghi vào hoặc đọc từ đó. Bây giờ khi đã có cách gọi các group và lấy dữ liệu liên quan của chúng, hãy sử dụng class :ref:`JSON<class_json>` để chuyển đổi dữ liệu thành một string dễ lưu trữ và lưu chúng vào file. Thực hiện theo cách này đảm bảo mỗi dòng là một object riêng, nhờ đó chúng ta cũng có cách dễ dàng lấy dữ liệu ra khỏi file.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Note: This can be called from anywhere inside the tree. This function is
    # độc lập với path.
    # Duyệt qua mọi thứ trong danh mục persist và yêu cầu chúng trả về một
    # dict gồm các biến liên quan.
    func save_game():
        var save_file = FileAccess.open("user://savegame.save", FileAccess.WRITE)
        var save_nodes = get_tree().get_nodes_in_group("Persist")
        for node in save_nodes:
            # Kiểm tra node có phải là một scene đã được instantiate để có thể instantiate lại trong quá trình load.
            if node.scene_file_path.is_empty():
                print("persistent node '%s' is not an instantiated scene, skipped" % node.name)
                continue

            # Kiểm tra node có hàm save.
            if !node.has_method("save"):
                print("persistent node '%s' is missing a save() function, skipped" % node.name)
                continue

            # Gọi hàm save của node.
            var node_data = node.call("save")

            # JSON cung cấp một static method để tạo JSON string.
            var json_string = JSON.stringify(node_data)

            # Lưu dictionary save thành một dòng mới trong file save.
            save_file.store_line(json_string)

 .. code-tab:: csharp

    // Note: This can be called from anywhere inside the tree. This function is
    // độc lập với path.
    // Duyệt qua mọi thứ trong danh mục persist và yêu cầu chúng trả về một
    // dict gồm các biến liên quan.
    public void SaveGame()
    {
        using var saveFile = FileAccess.Open("user://savegame.save", FileAccess.ModeFlags.Write);

        var saveNodes = GetTree().GetNodesInGroup("Persist");
        foreach (Node saveNode in saveNodes)
        {
            // Kiểm tra node có phải là một scene đã được instantiate để có thể instantiate lại trong quá trình load.
            if (string.IsNullOrEmpty(saveNode.SceneFilePath))
            {
                GD.Print($"persistent node '{saveNode.Name}' is not an instantiated scene, skipped");
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

            // Json cung cấp một static method để tạo JSON string.
            var jsonString = Json.Stringify(nodeData);

            // Lưu dictionary save thành một dòng mới trong file save.
            saveFile.StoreLine(jsonString);
        }
    }


Đã lưu game! Bây giờ, để load, chúng ta sẽ đọc từng dòng. Sử dụng method :ref:`parse<class_JSON_method_parse>` để đọc JSON string trở lại thành một dictionary, sau đó lặp qua dict để đọc các giá trị. Tuy nhiên, trước tiên chúng ta cần tạo object và có thể dùng các giá trị filename và parent để thực hiện việc đó. Đây là hàm load của chúng ta:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Note: This can be called from anywhere inside the tree. This function
    # là độc lập với path.
    func load_game():
        if not FileAccess.file_exists("user://savegame.save"):
            return # Lỗi! Chúng ta không có bản save để load.

        # Chúng ta cần khôi phục trạng thái game để không clone các object
        # trong quá trình loading. Việc này sẽ rất khác nhau tùy theo nhu cầu của một
        # project, vì vậy hãy cẩn thận ở bước này.
        # Trong ví dụ của chúng ta, chúng ta sẽ thực hiện việc này bằng cách xóa các object có thể lưu.
        var save_nodes = get_tree().get_nodes_in_group("Persist")
        for i in save_nodes:
            i.queue_free()

        # Load file từng dòng một và xử lý dictionary đó để khôi phục
        # object mà nó đại diện.
        var save_file = FileAccess.open("user://savegame.save", FileAccess.READ)
        while save_file.get_position() < save_file.get_length():
            var json_string = save_file.get_line()

            # Tạo helper class để tương tác với JSON.
            var json = JSON.new()

            # Kiểm tra xem có lỗi nào trong khi parse JSON string hay không, bỏ qua nếu thất bại.
            var parse_result = json.parse(json_string)
            if not parse_result == OK:
                print("JSON Parse Error: ", json.get_error_message(), " in ", json_string, " at line ", json.get_error_line())
                continue

            # Lấy dữ liệu từ JSON object.
            var node_data = json.data

            # Trước tiên, chúng ta cần tạo object, thêm nó vào tree và thiết lập vị trí của nó.
            var new_object = load(node_data["filename"]).instantiate()
            get_node(node_data["parent"]).add_child(new_object)
            new_object.position = Vector2(node_data["pos_x"], node_data["pos_y"])

            # Bây giờ chúng ta thiết lập các biến còn lại.
            for i in node_data.keys():
                if i == "filename" or i == "parent" or i == "pos_x" or i == "pos_y":
                    continue
                new_object.set(i, node_data[i])

 .. code-tab:: csharp

    // Note: This can be called from anywhere inside the tree. This function is
    // độc lập với path.
    public void LoadGame()
    {
        if (!FileAccess.FileExists("user://savegame.save"))
        {
            return; // Lỗi! Chúng ta không có bản save để load.
        }

        // Chúng ta cần khôi phục trạng thái game để không clone các object trong quá trình loading.
        // Việc này sẽ rất khác nhau tùy theo nhu cầu của một project, vì vậy hãy cẩn thận ở
        // bước này.
        // Trong ví dụ của chúng ta, chúng ta sẽ thực hiện việc này bằng cách xóa các object có thể lưu.
        var saveNodes = GetTree().GetNodesInGroup("Persist");
        foreach (Node saveNode in saveNodes)
        {
            saveNode.QueueFree();
        }

        // Load file từng dòng một và xử lý dictionary đó để khôi phục object
        // mà nó đại diện.
        using var saveFile = FileAccess.Open("user://savegame.save", FileAccess.ModeFlags.Read);

        while (saveFile.GetPosition() < saveFile.GetLength())
        {
            var jsonString = saveFile.GetLine();

            // Tạo helper class để tương tác với JSON.
            var json = new Json();
            var parseResult = json.Parse(jsonString);
            if (parseResult != Error.Ok)
            {
                GD.Print($"JSON Parse Error: {json.GetErrorMessage()} in {jsonString} at line {json.GetErrorLine()}");
                continue;
            }

            // Lấy dữ liệu từ JSON object.
            var nodeData = new Godot.Collections.Dictionary<string, Variant>((Godot.Collections.Dictionary)json.Data);

            // Trước tiên, chúng ta cần tạo object, thêm nó vào tree và thiết lập vị trí của nó.
            var newObjectScene = GD.Load<PackedScene>(nodeData["Filename"].ToString());
            var newObject = newObjectScene.Instantiate<Node>();
            GetNode(nodeData["Parent"].ToString()).AddChild(newObject);
            newObject.Set(Node2D.PropertyName.Position, new Vector2((float)nodeData["PosX"], (float)nodeData["PosY"]));

            // Bây giờ chúng ta thiết lập các biến còn lại.
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


Bây giờ chúng ta có thể lưu và load một số lượng object tùy ý được bố trí gần như ở bất kỳ đâu trong scene tree! Mỗi object có thể lưu dữ liệu khác nhau tùy theo những gì nó cần lưu.

Một số lưu ý
------------

Chúng ta đã lướt qua việc thiết lập trạng thái game để loading. Cuối cùng, phần lớn logic này được đặt ở đâu là tùy thuộc vào người tạo project. Việc này thường phức tạp và sẽ cần được tùy chỉnh nhiều dựa trên nhu cầu của từng project.

Ngoài ra, implementation của chúng ta giả định không có Persist object nào là child của Persist object khác. Nếu không, các path không hợp lệ sẽ được tạo ra. Để hỗ trợ các Persist object lồng nhau, hãy cân nhắc lưu các object theo từng giai đoạn. Load các object parent trước để chúng sẵn sàng cho lệnh gọi :ref:`add_child() <class_node_method_add_child>` khi các object child được load. Bạn cũng sẽ cần một cách để liên kết child với parent vì :ref:`NodePath <class_nodepath>` có khả năng sẽ không hợp lệ.

Serialization JSON và binary
----------------------------

Đối với trạng thái game đơn giản, JSON có thể phù hợp và tạo ra các file dễ đọc với con người, thuận tiện cho việc debug.

Tuy nhiên, JSON có nhiều hạn chế. Nếu cần lưu trạng thái game phức tạp hơn hoặc một lượng lớn dữ liệu, :ref:`binary serialization<doc_binary_serialization_api>` có thể là lựa chọn tốt hơn.

Các hạn chế của JSON
~~~~~~~~~~~~~~~~~~~~

Dưới đây là một số điểm quan trọng cần lưu ý khi sử dụng JSON.

* **Kích thước file:** JSON lưu dữ liệu ở dạng text, lớn hơn nhiều so với các format binary. * **Kiểu dữ liệu:** JSON chỉ cung cấp một tập hợp kiểu dữ liệu giới hạn. Nếu có các kiểu dữ liệu mà JSON không hỗ trợ, bạn sẽ cần chuyển đổi dữ liệu của mình từ và sang các kiểu mà JSON có thể xử lý. Ví dụ, một số kiểu quan trọng mà JSON không thể parse là: ``Vector2``, ``Vector3``, ``Color``, ``Rect2``, và ``Quaternion``. * **Cần logic tùy chỉnh để encoding/decoding:** Nếu có các custom class muốn lưu bằng JSON, bạn sẽ cần tự viết logic để encoding và decoding các class đó.

Serialization binary
~~~~~~~~~~~~~~~~~~~~

:ref:`Binary serialization<doc_binary_serialization_api>` is an alternative
phương pháp lưu trạng thái game, và bạn có thể sử dụng nó với các function ``get_var`` và ``store_var`` của :ref:`class_FileAccess`.

* Serialization binary sẽ tạo ra các file nhỏ hơn JSON. * Serialization binary có thể xử lý hầu hết các kiểu dữ liệu phổ biến. * Serialization binary cần ít logic tùy chỉnh hơn để encoding và decoding các custom class.

Lưu ý rằng không phải tất cả property đều được đưa vào. Chỉ các property được cấu hình với flag :ref:`PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>` được bật mới được serialize. Bạn có thể thêm usage flag mới cho một property bằng cách override
:ref:`_get_property_list<class_Object_private_method__get_property_list>`
method trong class của mình. Bạn cũng có thể kiểm tra cách cấu hình property usage bằng cách gọi ``Object._get_property_list``. Xem :ref:`PropertyUsageFlags<enum_@GlobalScope_PropertyUsageFlags>` để biết các usage flag có thể sử dụng.
