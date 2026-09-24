.. _doc_beziers_and_curves:

Bezier, đường cong và đường dẫn
===============================

Đường cong Bezier là một phép xấp xỉ toán học của các hình dạng hình học tự nhiên. Chúng ta sử dụng chúng để biểu diễn một đường cong với lượng thông tin ít nhất có thể và mức độ linh hoạt cao.

Không giống các khái niệm toán học trừu tượng hơn, đường cong Bezier được tạo ra cho thiết kế công nghiệp. Đây là một công cụ phổ biến trong ngành phần mềm đồ họa.

Chúng dựa trên :ref:`nội suy <doc_interpolation>`, mà chúng ta đã tìm hiểu trong bài viết trước, kết hợp nhiều bước để tạo ra các đường cong mượt mà. Để hiểu rõ hơn cách đường cong Bezier hoạt động, hãy bắt đầu với dạng đơn giản nhất: Bezier bậc hai.

Bezier bậc hai
--------------

Lấy ba điểm, số điểm tối thiểu cần thiết để Bezier bậc hai hoạt động:

.. image:: img/bezier_quadratic_points.png

Để vẽ một đường cong giữa chúng, trước tiên chúng ta nội suy dần trên hai đỉnh của mỗi trong hai đoạn được tạo bởi ba điểm, sử dụng các giá trị từ 0 đến 1. Kết quả là hai điểm di chuyển dọc theo các đoạn khi chúng ta thay đổi giá trị của ``t`` từ 0 đến 1.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _quadratic_bezier(p0: Vector2, p1: Vector2, p2: Vector2, t: float):
        var q0 = p0.lerp(p1, t)
        var q1 = p1.lerp(p2, t)

 .. code-tab:: csharp

    private Vector2 QuadraticBezier(Vector2 p0, Vector2 p1, Vector2 p2, float t)
    {
        Vector2 q0 = p0.Lerp(p1, t);
        Vector2 q1 = p1.Lerp(p2, t);
    }

Sau đó, chúng ta nội suy ``q0`` và ``q1`` để thu được một điểm duy nhất ``r`` di chuyển dọc theo một đường cong.

.. tabs::
 .. code-tab:: gdscript GDScript

        var r = q0.lerp(q1, t)
        return r

 .. code-tab:: csharp

        Vector2 r = q0.Lerp(q1, t);
        return r;

Loại đường cong này được gọi là đường cong *Bezier bậc hai*.

.. image:: img/bezier_quadratic_points2.gif

*(Nguồn ảnh: Wikipedia)*

Bezier bậc ba
-------------

Dựa trên ví dụ trước, chúng ta có thể kiểm soát nhiều hơn bằng cách nội suy giữa bốn điểm.

.. image:: img/bezier_cubic_points.png

Trước tiên, chúng ta sử dụng một hàm có bốn tham số để nhận bốn điểm làm đầu vào, ``p0``, ``p1``, ``p2`` và ``p3``:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _cubic_bezier(p0: Vector2, p1: Vector2, p2: Vector2, p3: Vector2, t: float):

 .. code-tab:: csharp

    public Vector2 CubicBezier(Vector2 p0, Vector2 p1, Vector2 p2, Vector2 p3, float t)
    {

    }

Chúng ta áp dụng nội suy tuyến tính cho từng cặp điểm để giảm chúng còn ba điểm:

.. tabs::
 .. code-tab:: gdscript GDScript

        var q0 = p0.lerp(p1, t)
        var q1 = p1.lerp(p2, t)
        var q2 = p2.lerp(p3, t)

 .. code-tab:: csharp

        Vector2 q0 = p0.Lerp(p1, t);
        Vector2 q1 = p1.Lerp(p2, t);
        Vector2 q2 = p2.Lerp(p3, t);

Sau đó, chúng ta lấy ba điểm và giảm chúng còn hai điểm:

.. tabs::
 .. code-tab:: gdscript GDScript

        var r0 = q0.lerp(q1, t)
        var r1 = q1.lerp(q2, t)

 .. code-tab:: csharp

        Vector2 r0 = q0.Lerp(q1, t);
        Vector2 r1 = q1.Lerp(q2, t);

Và còn một điểm:

.. tabs::
 .. code-tab:: gdscript GDScript

        var s = r0.lerp(r1, t)
        return s

 .. code-tab:: csharp

        Vector2 s = r0.Lerp(r1, t);
        return s;

Đây là hàm đầy đủ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _cubic_bezier(p0: Vector2, p1: Vector2, p2: Vector2, p3: Vector2, t: float):
        var q0 = p0.lerp(p1, t)
        var q1 = p1.lerp(p2, t)
        var q2 = p2.lerp(p3, t)

        var r0 = q0.lerp(q1, t)
        var r1 = q1.lerp(q2, t)

        var s = r0.lerp(r1, t)
        return s

 .. code-tab:: csharp

    private Vector2 CubicBezier(Vector2 p0, Vector2 p1, Vector2 p2, Vector2 p3, float t)
    {
        Vector2 q0 = p0.Lerp(p1, t);
        Vector2 q1 = p1.Lerp(p2, t);
        Vector2 q2 = p2.Lerp(p3, t);

        Vector2 r0 = q0.Lerp(q1, t);
        Vector2 r1 = q1.Lerp(q2, t);

        Vector2 s = r0.Lerp(r1, t);
        return s;
    }

Kết quả sẽ là một đường cong mượt mà nội suy giữa cả bốn điểm:

.. image:: img/bezier_cubic_points.gif

*(Nguồn ảnh: Wikipedia)*

.. note:: Nội suy Bezier bậc ba hoạt động tương tự trong 3D, chỉ cần sử dụng ``Vector3`` thay cho ``Vector2``.

Thêm các điểm điều khiển
------------------------

Dựa trên Bezier bậc ba, chúng ta có thể thay đổi cách hai điểm hoạt động để tự do kiểm soát hình dạng của đường cong. Thay vì có ``p0``, ``p1``, ``p2`` và ``p3``, chúng ta sẽ lưu trữ chúng như sau:

* ``point0 = p0``: Là điểm đầu tiên, điểm nguồn
* ``control0 = p1 - p0``: Là một vector tương đối với điểm điều khiển thứ nhất
* ``control1 = p3 - p2``: Là một vector tương đối với điểm điều khiển thứ hai
* ``point1 = p3``: Là điểm thứ hai, điểm đích

Theo cách này, chúng ta có hai điểm và hai điểm điều khiển là các vector tương đối với những điểm tương ứng. Nếu trước đây bạn từng sử dụng phần mềm đồ họa hoặc hoạt họa, điều này có thể trông quen thuộc:

.. image:: img/bezier_cubic_handles.png

Đây là cách phần mềm đồ họa trình bày các đường cong Bezier cho người dùng, cũng như cách chúng hoạt động và hiển thị trong Godot.

Curve2D, Curve3D, Path và Path2D
--------------------------------

Có hai đối tượng chứa các đường cong: :ref:`Curve3D <class_Curve3D>` và :ref:`Curve2D <class_Curve2D>` (tương ứng cho 3D và 2D).

Chúng có thể chứa nhiều điểm, cho phép tạo các đường dẫn dài hơn. Cũng có thể đặt chúng làm các node: :ref:`Path3D <class_Path3D>` và :ref:`Path2D <class_Path2D>` (cũng tương ứng cho 3D và 2D):

.. image:: img/bezier_path_2d.png

Tuy nhiên, cách sử dụng chúng có thể không hoàn toàn rõ ràng, vì vậy sau đây là mô tả về những trường hợp sử dụng phổ biến nhất của đường cong Bezier.

Đánh giá
--------

Chỉ đánh giá chúng cũng có thể là một lựa chọn, nhưng trong hầu hết trường hợp thì không hữu ích lắm. Nhược điểm lớn của đường cong Bezier là nếu bạn duyệt qua chúng với tốc độ không đổi, từ ``t = 0`` đến ``t = 1``, thì phép nội suy thực tế sẽ *không* di chuyển với tốc độ không đổi. Tốc độ cũng là một phép nội suy giữa khoảng cách giữa các điểm ``p0``, ``p1``, ``p2`` và ``p3``, và không có cách đơn giản về mặt toán học nào để duyệt qua đường cong với tốc độ không đổi.

Hãy xem một ví dụ với đoạn mã giả sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = 0.0

    func _process(delta):
        t += delta
        position = _cubic_bezier(p0, p1, p2, p3, t)

 .. code-tab:: csharp

    private float _t = 0.0f;

    public override void _Process(double delta)
    {
        _t += (float)delta;
        Position = CubicBezier(p0, p1, p2, p3, _t);
    }

.. image:: img/bezier_interpolation_speed.gif

Như bạn có thể thấy, tốc độ (tính bằng pixel mỗi giây) của hình tròn thay đổi, dù ``t`` được tăng với tốc độ không đổi. Điều này khiến beziers khó sử dụng cho bất kỳ mục đích thực tế nào ngay khi chưa qua xử lý.

Vẽ
--

Vẽ beziers (hoặc các đối tượng dựa trên đường cong) là một trường hợp sử dụng rất phổ biến, nhưng cũng không dễ thực hiện. Trong gần như mọi trường hợp, đường cong Bezier cần được chuyển đổi thành một dạng đoạn nào đó. Tuy nhiên, việc này thường khó thực hiện nếu không tạo ra một số lượng đoạn rất lớn.

Lý do là một số phần của đường cong (cụ thể là các góc) có thể cần một số lượng điểm đáng kể, trong khi những phần khác có thể không cần:

.. image:: img/bezier_point_amount.png

Ngoài ra, nếu cả hai điểm điều khiển đều là ``0, 0`` (hãy nhớ rằng chúng là các vector tương đối), đường cong Bezier sẽ chỉ là một đường thẳng (vì vậy việc vẽ một số lượng lớn điểm sẽ rất lãng phí).

Trước khi vẽ các đường cong Bezier, cần thực hiện *tessellation*. Việc này thường được thực hiện bằng một hàm đệ quy hoặc chia để trị, hàm này chia đường cong cho đến khi độ cong nhỏ hơn một ngưỡng nhất định.

Các lớp *Curve* cung cấp chức năng này thông qua
:ref:`Curve2D.tessellate() <class_Curve2D_method_tessellate>` (hàm nhận các đối số tùy chọn về ``stages`` của đệ quy và ``tolerance`` góc). Nhờ đó, việc vẽ một thứ gì đó dựa trên đường cong trở nên dễ dàng hơn.

Duyệt
-----

Trường hợp sử dụng phổ biến cuối cùng của các đường cong là duyệt qua chúng. Vì lý do đã đề cập trước đó liên quan đến tốc độ không đổi, việc này cũng khó thực hiện.

Để việc này dễ dàng hơn, các đường cong cần được *baked* thành các điểm cách đều nhau. Nhờ đó, chúng có thể được xấp xỉ bằng phép nội suy thông thường (có thể cải thiện thêm bằng tùy chọn cubic). Để thực hiện việc này, chỉ cần sử dụng phương thức :ref:`Curve3D.sample_baked()<class_Curve3D_method_sample_baked>` cùng với
:ref:`Curve2D.get_baked_length()<class_Curve2D_method_get_baked_length>`. Lần gọi đầu tiên đến một trong hai phương thức này sẽ bake đường cong vào bên trong.

Sau đó, có thể duyệt với tốc độ không đổi bằng đoạn mã giả sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = 0.0

    func _process(delta):
        t += delta
        position = curve.sample_baked(t * curve.get_baked_length(), true)

 .. code-tab:: csharp

    private float _t = 0.0f;

    public override void _Process(double delta)
    {
        _t += (float)delta;
        Position = curve.SampleBaked(_t * curve.GetBakedLength(), true);
    }

Khi đó, kết quả sẽ di chuyển với tốc độ không đổi:

.. image:: img/bezier_interpolation_baked.gif
