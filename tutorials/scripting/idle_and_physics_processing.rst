.. _doc_idle_and_physics_processing:

Xử lý nhàn rỗi và Xử lý vật lý
==============================

Game chạy trong một vòng lặp. Ở mỗi frame, bạn cần cập nhật trạng thái của thế giới game trước khi vẽ nó lên màn hình. Godot cung cấp hai virtual method trong class Node để thực hiện việc này: :ref:`Node._process() <class_Node_private_method__process>` và
:ref:`Node._physics_process() <class_Node_private_method__physics_process>`. If you
khi bạn định nghĩa một hoặc cả hai phương thức này trong script, engine sẽ tự động gọi chúng.

Có hai loại xử lý mà bạn có thể sử dụng:

1. **Xử lý nhàn rỗi** cho phép bạn chạy code cập nhật một node ở mỗi frame, thường xuyên nhất có thể. 2. **Xử lý vật lý** diễn ra với một tần suất cố định, mặc định là 60 lần mỗi giây. Tần suất này độc lập với framerate thực tế của game và giúp physics chạy ổn định. Bạn nên sử dụng nó cho mọi thứ liên quan đến physics engine, chẳng hạn như di chuyển một body va chạm với môi trường.

Bạn có thể kích hoạt xử lý nhàn rỗi bằng cách định nghĩa phương thức ``_process()`` trong một script. Bạn có thể tắt và bật lại phương thức này bằng cách gọi :ref:`Node.set_process() <class_Node_method_set_process>`.

Engine gọi phương thức này mỗi khi vẽ một frame:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        # Thực hiện một việc gì đó...
        pass

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        // Thực hiện một việc gì đó...
    }

Hãy nhớ rằng tần suất engine gọi ``_process()`` phụ thuộc vào framerate của ứng dụng, vốn thay đổi theo thời gian và giữa các thiết bị.

Tham số ``delta`` của function là thời gian tính bằng giây đã trôi qua kể từ lần gọi trước đó đến ``_process()``. Hãy sử dụng tham số này để các phép tính không phụ thuộc vào framerate. Ví dụ: bạn luôn nên nhân giá trị tốc độ với ``delta`` để tạo chuyển động cho một object.

Xử lý vật lý hoạt động với một virtual function tương tự: ``_physics_process()``. Hãy sử dụng nó cho các phép tính phải diễn ra trước mỗi bước physics, chẳng hạn như di chuyển một character va chạm với thế giới game. Như đã đề cập ở trên, ``_physics_process()`` chạy ở các khoảng thời gian cố định nhiều nhất có thể để giữ cho các tương tác physics ổn định. Bạn có thể thay đổi khoảng thời gian giữa các bước physics trong Project Settings, tại Physics -> Common -> Physics Fps. Mặc định, nó được đặt để chạy 60 lần mỗi giây.

Engine gọi phương thức này trước mỗi bước physics:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        # Thực hiện một việc gì đó...
        pass

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        // Thực hiện một việc gì đó...
    }

Function ``_process()`` không được đồng bộ với physics. Tần suất của nó phụ thuộc vào phần cứng và mức độ tối ưu hóa game. Trong các game single-threaded, nó cũng chạy sau bước physics.

Bạn có thể xem function ``_process()`` hoạt động bằng cách tạo một scene chỉ có một node Label và gắn script sau vào node đó:

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

Khi chạy scene, bạn sẽ thấy một bộ đếm tăng lên sau mỗi frame.
