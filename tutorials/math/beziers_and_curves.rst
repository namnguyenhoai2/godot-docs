.. _doc_beziers_and_curves:

Bezier, đường cong và đường dẫn
===============================

Đường cong Bezier là một phép xấp xỉ toán học của các hình dạng hình học tự nhiên. Chúng ta sử dụng chúng để biểu diễn một đường cong với ít thông tin nhất có thể và với mức độ linh hoạt cao.

Không giống các khái niệm toán học trừu tượng hơn, đường cong Bezier được tạo ra cho thiết kế công nghiệp. Đây là một công cụ phổ biến trong ngành phần mềm đồ họa.

Chúng dựa trên :ref:`interpolation<doc_interpolation>`, mà chúng ta đã tìm hiểu trong bài viết trước, kết hợp nhiều bước để tạo ra các đường cong mượt mà. Để hiểu rõ hơn cách đường cong Bezier hoạt động, hãy bắt đầu với dạng đơn giản nhất: Bezier bậc hai.

Bezier bậc hai
--------------

Lấy ba điểm, số điểm tối thiểu cần thiết để Bezier bậc hai hoạt động:

.. image:: img/bezier_quadratic_points.png

Để vẽ một đường cong giữa chúng, trước tiên chúng ta nội suy dần trên hai đỉnh của mỗi trong hai đoạn thẳng được tạo bởi ba điểm, sử dụng các giá trị từ 0 đến 1. Điều này cho chúng ta hai điểm di chuyển dọc theo các đoạn thẳng khi thay đổi giá trị của ``t`` từ 0 đến 1.

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

Chúng ta áp dụng phép nội suy tuyến tính cho từng cặp điểm để rút gọn chúng còn ba điểm:

.. tabs::
 .. code-tab:: gdscript GDScript

        var q0 = p0.lerp(p1, t)
        var q1 = p1.lerp(p2, t)
        var q2 = p2.lerp(p3, t)

 .. code-tab:: csharp

        Vector2 q0 = p0.Lerp(p1, t);
        Vector2 q1 = p1.Lerp(p2, t);
        Vector2 q2 = p2.Lerp(p3, t);

Sau đó, chúng ta lấy ba điểm và rút gọn chúng còn hai điểm:

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

Đây là toàn bộ hàm:

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

.. note:: Cubic Bezier interpolation works the same in 3D, just use ``Vector3``
          thay vì ``Vector2``.

Thêm các điểm điều khiển
------------------------

Dựa trên Bezier bậc ba, chúng ta có thể thay đổi cách hai điểm hoạt động để tự do kiểm soát hình dạng đường cong. Thay vì có ``p0``, ``p1``, ``p2`` và ``p3``, chúng ta sẽ lưu chúng dưới dạng:

* ``point0 = p0``: Là điểm đầu tiên, điểm nguồn * ``control0 = p1 - p0``: Là một vector tương đối so với điểm điều khiển đầu tiên * ``control1 = p3 - p2``: Là một vector tương đối so với điểm điều khiển thứ hai * ``point1 = p3``: Là điểm thứ hai, điểm đích

Theo cách này, chúng ta có hai điểm và hai điểm điều khiển là các vector tương đối so với các điểm tương ứng. Nếu bạn từng sử dụng phần mềm đồ họa hoặc hoạt hình, điều này có thể trông quen thuộc:

.. image:: img/bezier_cubic_handles.png

Đây là cách phần mềm đồ họa trình bày các đường cong Bezier cho người dùng, cũng như cách chúng hoạt động và hiển thị trong Godot.

Curve2D, Curve3D, Path và Path2D
--------------------------------

Có hai đối tượng chứa các đường cong: :ref:`Curve3D <class_Curve3D>` và :ref:`Curve2D <class_Curve2D>` (lần lượt dành cho 3D và 2D).

Chúng có thể chứa nhiều điểm, cho phép tạo các đường dẫn dài hơn. Bạn cũng có thể đặt chúng làm node: :ref:`Path3D <class_Path3D>` và :ref:`Path2D <class_Path2D>` (cũng lần lượt dành cho 3D và 2D):

.. image:: img/bezier_path_2d.png

Tuy nhiên, cách sử dụng chúng có thể không hoàn toàn rõ ràng, vì vậy sau đây là mô tả về các trường hợp sử dụng phổ biến nhất của đường cong Bezier.

Đánh giá
--------

Chỉ đánh giá chúng cũng có thể là một lựa chọn, nhưng trong hầu hết trường hợp thì không hữu ích lắm. Nhược điểm lớn của đường cong Bezier là nếu bạn duyệt qua chúng với tốc độ không đổi, từ ``t = 0`` đến ``t = 1``, phép nội suy thực tế sẽ *không* di chuyển với tốc độ không đổi. Tốc độ cũng là một phép nội suy giữa khoảng cách giữa các điểm ``p0``, ``p1``, ``p2`` và ``p3``, và không có cách đơn giản về mặt toán học nào để duyệt qua đường cong với tốc độ không đổi.

Hãy thực hiện một ví dụ với đoạn mã giả sau:

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

Như bạn có thể thấy, tốc độ (tính bằng pixel trên giây) của hình tròn thay đổi, mặc dù ``t`` tăng với tốc độ không đổi. Điều này khiến beziers khó sử dụng ngay cho bất kỳ mục đích thực tế nào.

Vẽ
---

Vẽ beziers (hoặc các đối tượng dựa trên đường cong) là một trường hợp sử dụng rất phổ biến, nhưng cũng không dễ thực hiện. Trong hầu hết mọi trường hợp, đường cong Bezier cần được chuyển đổi thành một dạng đoạn nào đó. Tuy nhiên, việc này thường khó nếu không tạo ra một số lượng đoạn rất lớn.

Lý do là một số phần của đường cong (cụ thể là các góc) có thể cần một lượng điểm đáng kể, trong khi các phần khác có thể không cần nhiều điểm:

.. image:: img/bezier_point_amount.png

Ngoài ra, nếu cả hai điểm điều khiển đều là ``0, 0`` (hãy nhớ rằng chúng là các vector tương đối), đường cong Bezier sẽ chỉ là một đường thẳng (vì vậy việc vẽ một số lượng lớn điểm sẽ rất lãng phí).

Trước khi vẽ đường cong Bezier, cần thực hiện *tessellation*. Việc này thường được thực hiện bằng một hàm đệ quy hoặc chia để trị, hàm này chia đường cong cho đến khi độ cong nhỏ hơn một ngưỡng nhất định.

Các lớp *Curve* cung cấp chức năng này thông qua
:ref:`Curve2D.tessellate() <class_Curve2D_method_tessellate>` function (which receives optional ``stages`` of recursion and angle ``tolerance`` arguments). This way, drawing something based on a curve is easier.

Duyệt qua
---------

Trường hợp sử dụng phổ biến cuối cùng của các đường cong là duyệt qua chúng. Do vấn đề về tốc độ không đổi đã đề cập trước đó, việc này cũng khó thực hiện.

Để thực hiện dễ hơn, các đường cong cần được *baked* thành các điểm cách đều nhau. Nhờ vậy, chúng có thể được xấp xỉ bằng phép nội suy thông thường (có thể được cải thiện hơn nữa với tùy chọn cubic). Để thực hiện việc này, chỉ cần sử dụng phương thức :ref:`Curve3D.sample_baked()<class_Curve3D_method_sample_baked>` cùng với
:ref:`Curve2D.get_baked_length()<class_Curve2D_method_get_baked_length>`. The first call to either of them will bake the curve internally.

Sau đó, có thể thực hiện việc duyệt qua với tốc độ không đổi bằng đoạn mã giả sau:

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

Khi đó, đầu ra sẽ di chuyển với tốc độ không đổi:

.. image:: img/bezier_interpolation_baked.gif
