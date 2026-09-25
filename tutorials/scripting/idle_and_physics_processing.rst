.. _doc_idle_and_physics_processing:

Xử lý khi nhàn rỗi và vật lý
============================

Trò chơi chạy trong một vòng lặp. Ở mỗi khung hình, bạn cần cập nhật trạng thái của thế giới trò chơi trước khi vẽ nó lên màn hình. Godot cung cấp hai phương thức ảo trong lớp Node để thực hiện việc này: :ref:`Node._process() <class_Node_private_method__process>` và
:ref:`Node._physics_process() <class_Node_private_method__physics_process>`. Nếu bạn định nghĩa một hoặc cả hai phương thức trong script, engine sẽ tự động gọi chúng.

Có hai loại xử lý mà bạn có thể sử dụng:

1. **Xử lý khi nhàn rỗi** cho phép bạn chạy mã cập nhật một node ở mỗi khung hình, thường xuyên nhất có thể.
2. **Xử lý vật lý** diễn ra ở một tốc độ cố định, mặc định là 60 lần mỗi giây. Tốc độ này độc lập với framerate thực tế của trò chơi và giúp vật lý chạy mượt mà. Bạn nên sử dụng nó cho mọi thứ liên quan đến physics engine, chẳng hạn như di chuyển một body va chạm với môi trường.

Bạn có thể kích hoạt xử lý khi nhàn rỗi bằng cách định nghĩa phương thức ``_process()`` trong script. Bạn có thể tắt và bật lại phương thức này bằng cách gọi :ref:`Node.set_process() <class_Node_method_set_process>`.

Engine gọi phương thức này mỗi khi vẽ một khung hình:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        # Làm gì đó...
        pass

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        // Làm gì đó...
    }

Hãy lưu ý rằng tần suất engine gọi ``_process()`` phụ thuộc vào framerate của ứng dụng, vốn thay đổi theo thời gian và giữa các thiết bị.

Tham số ``delta`` của hàm là thời gian đã trôi qua tính bằng giây kể từ lần gọi ``_process()`` trước đó. Sử dụng tham số này để thực hiện các phép tính độc lập với framerate. Ví dụ: bạn luôn nên nhân một giá trị tốc độ với ``delta`` để tạo hiệu ứng chuyển động cho một đối tượng.

Xử lý vật lý sử dụng một hàm ảo tương tự: ``_physics_process()``. Hãy sử dụng nó cho các phép tính phải diễn ra trước mỗi bước vật lý, chẳng hạn như di chuyển một nhân vật va chạm với thế giới trò chơi. Như đã đề cập ở trên, ``_physics_process()`` chạy ở các khoảng thời gian cố định nhiều nhất có thể để giữ cho các tương tác vật lý ổn định. Bạn có thể thay đổi khoảng thời gian giữa các bước vật lý trong Project Settings, tại Physics -> Common -> Physics Fps. Theo mặc định, khoảng thời gian này được đặt để chạy 60 lần mỗi giây.

Engine gọi phương thức này trước mỗi bước vật lý:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        # Làm gì đó...
        pass

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        // Làm gì đó...
    }

Hàm ``_process()`` không được đồng bộ với vật lý. Tốc độ của nó phụ thuộc vào phần cứng và mức độ tối ưu hóa của trò chơi. Trong các trò chơi đơn luồng, hàm này cũng chạy sau bước vật lý.

Bạn có thể thấy hàm ``_process()`` hoạt động bằng cách tạo một scene chỉ có một node Label và gắn script sau vào node đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Label

    var time = 0

    func _process(delta):
        time += delta
        text = str(time) # 'text' là một thuộc tính tích hợp sẵn của Label.

 .. code-tab:: csharp

    using Godot;

    public partial class CustomLabel : Label
    {
        private double _time;

        public override void _Process(double delta)
        {
            _time += delta;
            Text = _time.ToString(); // 'Text' là một thuộc tính tích hợp sẵn của Label.
        }
    }

Khi chạy scene, bạn sẽ thấy một bộ đếm tăng lên ở mỗi khung hình.
