.. _doc_vector_math:

Phép toán vector
================

Giới thiệu
~~~~~~~~~~

Tutorial này là phần giới thiệu ngắn gọn và thực tế về đại số tuyến tính trong phát triển game. Đại số tuyến tính là ngành nghiên cứu về các vector và cách sử dụng chúng. Vector có nhiều ứng dụng trong phát triển 2D và 3D, và Godot sử dụng chúng rất rộng rãi. Hiểu rõ về phép toán vector là điều thiết yếu để trở thành một nhà phát triển game giỏi.

.. note:: This tutorial is **not** a formal textbook on linear algebra. We will
          chỉ xem xét cách nó được áp dụng trong phát triển game. Để tìm hiểu rộng hơn về toán học, hãy xem https://www.khanacademy.org/math/linear-algebra

Hệ tọa độ (2D)
~~~~~~~~~~~~~~

Trong không gian 2D, tọa độ được xác định bằng một trục ngang (``x``) và một trục dọc (``y``). Một vị trí cụ thể trong không gian 2D được viết dưới dạng một cặp giá trị, chẳng hạn như ``(4, 3)``.

.. image:: img/vector_axis1.png

.. note:: If you're new to computer graphics, it might seem odd that the
          trục ``y`` dương hướng **xuống dưới** thay vì hướng lên trên, như có lẽ bạn đã học trong giờ toán. Tuy nhiên, điều này phổ biến trong hầu hết các ứng dụng đồ họa máy tính.

Mọi vị trí trên mặt phẳng 2D đều có thể được xác định bằng một cặp số theo cách này. Tuy nhiên, ta cũng có thể xem vị trí ``(4, 3)`` là một **độ lệch** từ điểm ``(0, 0)``, hay còn gọi là **gốc tọa độ**. Hãy vẽ một mũi tên từ gốc tọa độ đến điểm đó:

.. image:: img/vector_xy1.png

Đây là một **vector**. Một vector biểu diễn rất nhiều thông tin hữu ích. Ngoài việc cho biết điểm nằm tại ``(4, 3)``, ta cũng có thể xem nó là một góc ``θ`` (theta) và một độ dài (hay độ lớn) ``m``. Trong trường hợp này, mũi tên là một **vector vị trí** - nó biểu thị một vị trí trong không gian so với gốc tọa độ.

Một điểm rất quan trọng cần lưu ý về vector là chúng chỉ biểu diễn hướng và độ lớn **tương đối**. Không có khái niệm vị trí của một vector. Hai vector sau đây là giống hệt nhau:

.. image:: img/vector_xy2.png

Cả hai vector đều biểu diễn một điểm nằm cách một điểm bắt đầu nào đó 4 đơn vị về bên phải và 3 đơn vị về phía dưới. Vị trí bạn vẽ vector trên mặt phẳng ở đâu không quan trọng; nó luôn biểu diễn một hướng và độ lớn tương đối.

Các phép toán vector
~~~~~~~~~~~~~~~~~~~~

Bạn có thể dùng một trong hai cách (tọa độ x và y hoặc góc và độ lớn) để chỉ một vector, nhưng để thuận tiện, lập trình viên thường dùng ký hiệu tọa độ. Ví dụ, trong Godot, gốc tọa độ là góc trên bên trái của màn hình, vì vậy để đặt một node 2D có tên ``Node2D`` cách 400 pixel về bên phải và 300 pixel về phía dưới, hãy dùng đoạn code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    $Node2D.position = Vector2(400, 300)

 .. code-tab:: csharp

    var node2D = GetNode<Node2D>("Node2D");
    node2D.Position = new Vector2(400, 300);

Godot hỗ trợ cả :ref:`Vector2 <class_Vector2>` và :ref:`Vector3 <class_Vector3>` lần lượt cho việc sử dụng trong 2D và 3D. Các quy tắc toán học tương tự được thảo luận trong bài viết này áp dụng cho cả hai loại, và ở bất cứ đâu chúng tôi liên kết đến các phương thức ``Vector2`` trong tài liệu tham khảo lớp, bạn cũng có thể xem các phương thức ``Vector3`` tương ứng của chúng.

Truy cập thành phần
-------------------

Có thể truy cập trực tiếp từng thành phần của vector bằng tên.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo một vector với tọa độ (2, 5).
    var a = Vector2(2, 5)
    # Tạo một vector rồi gán x và y theo cách thủ công.
    var b = Vector2()
    b.x = 3
    b.y = 1

 .. code-tab:: csharp

    // Tạo một vector với tọa độ (2, 5).
    var a = new Vector2(2, 5);
    // Tạo một vector rồi gán x và y theo cách thủ công.
    var b = new Vector2();
    b.X = 3;
    b.Y = 1;

Cộng các vector
---------------

Khi cộng hoặc trừ hai vector, các thành phần tương ứng sẽ được cộng:

.. tabs::
 .. code-tab:: gdscript GDScript

    var c = a + b  # (2, 5) + (3, 1) = (5, 6)

 .. code-tab:: csharp

    var c = a + b;  // (2, 5) + (3, 1) = (5, 6)

Ta cũng có thể thấy điều này trực quan bằng cách đặt vector thứ hai ở cuối vector thứ nhất:

.. image:: img/vector_add1.png

Lưu ý rằng cộng ``a + b`` cho cùng kết quả như ``b + a``.

Nhân với vô hướng
-----------------

.. note:: Vectors represent both direction and magnitude. A value representing
          chỉ độ lớn được gọi là một **vô hướng**. Các đại lượng vô hướng sử dụng
          :ref:`class_float` type in Godot.

Một vector có thể được nhân với một **vô hướng**:

.. tabs::
 .. code-tab:: gdscript GDScript

    var c = a * 2  # (2, 5) * 2 = (4, 10)
    var d = b / 3  # (3, 6) / 3 = (1, 2)
    var e = d * -2 # (1, 2) * -2 = (-2, -4)

 .. code-tab:: csharp

    var c = a * 2;  // (2, 5) * 2 = (4, 10)
    var d = b / 3;  // (3, 6) / 3 = (1, 2)
    var e = d * -2; // (1, 2) * -2 = (-2, -4)

.. image:: img/vector_mult1.png

.. note:: Multiplying a vector by a positive scalar does not change its direction, only
          độ lớn của nó. Nhân với một vô hướng âm sẽ cho kết quả là một vector theo hướng ngược lại. Đây là cách bạn **co giãn** một vector.

Các ứng dụng thực tế
~~~~~~~~~~~~~~~~~~~~

Hãy xem hai cách sử dụng phổ biến của phép cộng và phép trừ vector.

Di chuyển
---------

Một vector có thể biểu diễn **bất kỳ** đại lượng nào có độ lớn và hướng. Các ví dụ điển hình gồm: vị trí, vận tốc, gia tốc và lực. Trong hình này, ở bước 1, tàu vũ trụ có vector vị trí là ``(1, 3)`` và vector vận tốc là ``(2, 1)``. Vector vận tốc biểu diễn quãng đường con tàu di chuyển trong mỗi bước. Ta có thể tìm vị trí ở bước 2 bằng cách cộng vận tốc vào vị trí hiện tại.

.. image:: img/vector_movement1.png

.. tip:: Velocity measures the **change** in position per unit of time. The new
         vị trí được xác định bằng cách cộng vận tốc nhân với thời gian đã trôi qua (ở đây giả định là một đơn vị, ví dụ 1 s) vào vị trí trước đó.

         Trong một tình huống game 2D điển hình, bạn sẽ có vận tốc tính bằng pixel trên giây, rồi nhân nó với tham số ``delta`` (thời gian đã trôi qua kể từ frame trước) từ các callback :ref:`_process() <class_Node_private_method__process>` hoặc :ref:`_physics_process() <class_Node_private_method__physics_process>`.

Hướng về phía mục tiêu
----------------------

Trong tình huống này, bạn có một chiếc xe tăng muốn chĩa tháp pháo về phía một robot. Lấy vị trí của xe tăng trừ vị trí của robot sẽ cho vector hướng từ xe tăng đến robot.

.. image:: img/vector_subtract2.webp

.. tip:: To find a vector pointing from ``A`` to ``B``, use ``B - A``.

Vector đơn vị
~~~~~~~~~~~~~

Một vector có **độ lớn** bằng ``1`` được gọi là một **vector đơn vị**. Đôi khi chúng cũng được gọi là **vector hướng** hoặc **pháp tuyến**. Vector đơn vị rất hữu ích khi bạn cần theo dõi một hướng.

Chuẩn hóa
---------

**Chuẩn hóa** một vector nghĩa là giảm độ dài của nó xuống ``1`` trong khi vẫn giữ nguyên hướng. Việc này được thực hiện bằng cách chia từng thành phần của nó cho độ lớn. Vì đây là một phép toán rất phổ biến, Godot cung cấp một
:ref:`normalized() <class_Vector2_method_normalized>` method for this:

.. tabs::
 .. code-tab:: gdscript GDScript

    a = a.normalized()

 .. code-tab:: csharp

    a = a.Normalized();

.. warning:: Because normalization involves dividing by the vector's length, you
             không thể chuẩn hóa một vector có độ dài ``0``. Việc cố thực hiện sẽ thường dẫn đến lỗi. Tuy nhiên, trong GDScript, việc gọi phương thức ``normalized()`` trên một vector có độ dài 0 sẽ giữ nguyên giá trị và tự tránh lỗi cho bạn.

Phản xạ
-------

Một cách sử dụng phổ biến của vector đơn vị là biểu thị **pháp tuyến**. Vector pháp tuyến là các vector đơn vị vuông góc với một bề mặt, xác định hướng của bề mặt đó. Chúng thường được dùng cho chiếu sáng, va chạm và các phép toán khác liên quan đến bề mặt.

Ví dụ, hãy tưởng tượng ta có một quả bóng đang chuyển động và muốn nó bật khỏi một bức tường hoặc vật thể khác:

.. image:: img/vector_reflect1.png

Pháp tuyến bề mặt có giá trị ``(0, -1)`` vì đây là một bề mặt nằm ngang. Khi quả bóng va chạm, ta lấy chuyển động còn lại của nó (phần còn lại khi nó chạm vào bề mặt) và phản xạ nó bằng pháp tuyến. Trong Godot, có một phương thức :ref:`bounce() <class_Vector2_method_bounce>` để xử lý việc này. Dưới đây là ví dụ code của sơ đồ trên bằng cách sử dụng một :ref:`CharacterBody2D <class_CharacterBody2D>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    var collision: KinematicCollision2D = move_and_collide(velocity * delta)
    if collision:
        var reflect = collision.get_remainder().bounce(collision.get_normal())
        velocity = velocity.bounce(collision.get_normal())
        move_and_collide(reflect)

 .. code-tab:: csharp

    KinematicCollision2D collision = MoveAndCollide(_velocity * (float)delta);
    if (collision != null)
    {
        var reflect = collision.GetRemainder().Bounce(collision.GetNormal());
        _velocity = _velocity.Bounce(collision.GetNormal());
        MoveAndCollide(reflect);
    }

Tích vô hướng
~~~~~~~~~~~~~

**Tích vô hướng** là một trong những khái niệm quan trọng nhất trong phép toán vector, nhưng thường bị hiểu sai. Tích vô hướng là một phép toán trên hai vector và trả về một **vô hướng**. Không giống vector, vốn chứa cả độ lớn và hướng, một giá trị vô hướng chỉ có độ lớn.

Công thức của tích vô hướng thường có hai dạng:

.. image:: img/vector_dot1.png

và

.. image:: img/vector_dot2.png

Ký hiệu toán học *||A||* biểu diễn độ lớn của vector ``A``, còn *A*\ :sub:`x` có nghĩa là thành phần ``x`` của vector ``A``.

Tuy nhiên, trong hầu hết trường hợp, cách dễ nhất là sử dụng phương thức tích hợp sẵn :ref:`dot() <class_Vector2_method_dot>`. Lưu ý rằng thứ tự của hai vector không quan trọng:

.. tabs::
 .. code-tab:: gdscript GDScript

    var c = a.dot(b)
    var d = b.dot(a)  # Các biểu thức này tương đương.

 .. code-tab:: csharp

    float c = a.Dot(b);
    float d = b.Dot(a);  // Các biểu thức này tương đương.

Tích vô hướng hữu ích nhất khi được dùng với các vector đơn vị, khiến công thức đầu tiên rút gọn chỉ còn ``cos(θ)``. Điều này có nghĩa là ta có thể dùng tích vô hướng để biết điều gì đó về góc giữa hai vector:

.. image:: img/vector_dot3.png

Khi sử dụng các vector đơn vị, kết quả luôn nằm trong khoảng từ ``-1`` (180°) đến ``1`` (0°).

Hướng mặt
---------

Ta có thể dùng sự thật này để phát hiện xem một đối tượng có đang hướng về phía đối tượng khác hay không. Trong sơ đồ bên dưới, người chơi ``P`` đang cố tránh những zombie ``A`` và ``B``. Giả sử góc nhìn của zombie là **180°**, chúng có nhìn thấy người chơi không?

.. image:: img/vector_facing2.png

Các mũi tên màu xanh lá ``fA`` và ``fB`` là các **vector đơn vị** biểu diễn hướng mặt của zombie, còn hình bán nguyệt màu xanh dương biểu diễn góc nhìn của nó. Đối với zombie ``A``, ta tìm vector hướng ``AP`` trỏ đến người chơi bằng cách sử dụng ``P - A`` rồi chuẩn hóa nó; tuy nhiên, Godot có một phương thức hỗ trợ để thực hiện việc này, gọi là :ref:`direction_to() <class_Vector2_method_direction_to>`. Nếu góc giữa vector này và vector hướng mặt nhỏ hơn 90°, zombie có thể nhìn thấy người chơi.

Trong code, nó sẽ trông như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var AP = A.direction_to(P)
    if AP.dot(fA) > 0:
        print("A sees P!")

 .. code-tab:: csharp

    var AP = A.DirectionTo(P);
    if (AP.Dot(fA) > 0)
    {
        GD.Print("A sees P!");
    }

Tích có hướng
~~~~~~~~~~~~~

Tương tự tích vô hướng, **tích có hướng** là một phép toán trên hai vector. Tuy nhiên, kết quả của tích có hướng là một vector có hướng vuông góc với cả hai vector đó. Độ lớn của nó phụ thuộc vào góc tương đối giữa chúng. Nếu hai vector song song, kết quả của tích có hướng sẽ là một vector không.

.. image:: img/vector_cross1.png

.. image:: img/vector_cross2.png

Tích có hướng được tính như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var c = Vector3()
    c.x = (a.y * b.z) - (a.z * b.y)
    c.y = (a.z * b.x) - (a.x * b.z)
    c.z = (a.x * b.y) - (a.y * b.x)

 .. code-tab:: csharp

    var c = new Vector3();
    c.X = (a.Y * b.Z) - (a.Z * b.Y);
    c.Y = (a.Z * b.X) - (a.X * b.Z);
    c.Z = (a.X * b.Y) - (a.Y * b.X);

Trong Godot, bạn có thể sử dụng phương thức tích hợp sẵn :ref:`Vector3.cross() <class_Vector3_method_cross>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    var c = a.cross(b)

 .. code-tab:: csharp

    var c = a.Cross(b);

Tích có hướng không được định nghĩa về mặt toán học trong 2D. Phương thức :ref:`Vector2.cross() <class_Vector2_method_cross>` là một phép tương tự thường được dùng của tích có hướng 3D cho các vector 2D.

.. note:: In the cross product, order matters. ``a.cross(b)`` does not give the
          cùng kết quả như ``b.cross(a)``. Các vector thu được hướng theo hai hướng **ngược nhau**.

Tính pháp tuyến
---------------

Một cách sử dụng phổ biến của tích có hướng là tìm pháp tuyến bề mặt của một mặt phẳng hoặc bề mặt trong không gian 3D. Nếu có tam giác ``ABC``, chúng ta có thể sử dụng phép trừ vector để tìm hai cạnh ``AB`` và ``AC``. Sử dụng tích có hướng, ``AB × AC`` tạo ra một vector vuông góc với cả hai: pháp tuyến bề mặt.

Sau đây là một hàm để tính pháp tuyến của tam giác:

.. tabs::
 .. code-tab:: gdscript GDScript

    func get_triangle_normal(a, b, c):
        # Tìm pháp tuyến bề mặt khi biết 3 đỉnh.
        var side1 = b - a
        var side2 = c - a
        var normal = side1.cross(side2)
        return normal

 .. code-tab:: csharp

    Vector3 GetTriangleNormal(Vector3 a, Vector3 b, Vector3 c)
    {
        // Tìm pháp tuyến bề mặt khi biết 3 đỉnh.
        var side1 = b - a;
        var side2 = c - a;
        var normal = side1.Cross(side2);
        return normal;
    }

Hướng về một mục tiêu
---------------------

Trong phần tích vô hướng ở trên, chúng ta đã thấy cách sử dụng nó để tìm góc giữa hai vector. Tuy nhiên, trong không gian 3D, như vậy vẫn chưa đủ thông tin. Chúng ta cũng cần biết phải xoay quanh trục nào. Có thể tìm trục đó bằng cách tính tích có hướng của hướng hiện tại và hướng đến mục tiêu. Vector vuông góc thu được là trục xoay.

Thông tin thêm
~~~~~~~~~~~~~~

Để biết thêm thông tin về cách sử dụng phép toán vector trong Godot, hãy xem các bài viết sau:

- :ref:`doc_vectors_advanced` - :ref:`doc_matrices_and_transforms`
