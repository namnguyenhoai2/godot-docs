.. _doc_vectors_advanced:

Toán vector nâng cao
====================

Mặt phẳng
~~~~~~~~~

Tích vô hướng có một thuộc tính thú vị khác với các vector đơn vị. Hãy tưởng tượng một mặt phẳng vuông góc với vector đó (và đi qua gốc tọa độ). Các mặt phẳng chia toàn bộ không gian thành phần dương (phía trên mặt phẳng) và phần âm (phía dưới mặt phẳng), và (trái với quan niệm phổ biến) bạn cũng có thể sử dụng toán học của chúng trong 2D:

.. image:: img/tutovec10.png

Các vector đơn vị vuông góc với một bề mặt (do đó mô tả hướng của bề mặt) được gọi là **vector pháp tuyến đơn vị**. Tuy nhiên, chúng thường được viết tắt đơn giản là *pháp tuyến*. Pháp tuyến xuất hiện trong các mặt phẳng, hình học 3D (để xác định mỗi mặt hoặc đỉnh hướng về đâu), v.v. Một **pháp tuyến** *là* một **vector đơn vị**, nhưng được gọi là *pháp tuyến* vì cách sử dụng của nó. (Cũng giống như việc chúng ta gọi (0,0) là Gốc tọa độ!).

Mặt phẳng đi qua gốc tọa độ và bề mặt của nó vuông góc với vector đơn vị (hay *pháp tuyến*). Phía mà vector hướng tới là nửa không gian dương, còn phía kia là nửa không gian âm. Trong 3D, điều này hoàn toàn tương tự, ngoại trừ việc mặt phẳng là một bề mặt vô hạn (hãy tưởng tượng một tờ giấy phẳng vô hạn mà bạn có thể xoay theo hướng tùy ý và được ghim vào gốc tọa độ) thay vì một đường thẳng.

Khoảng cách đến mặt phẳng
-------------------------

Bây giờ khi đã hiểu mặt phẳng là gì, hãy quay lại với tích vô hướng. Tích vô hướng giữa một **vector đơn vị** và bất kỳ **điểm nào trong không gian** (đúng vậy, lần này chúng ta lấy tích vô hướng giữa vector và vị trí) trả về **khoảng cách từ điểm đến mặt phẳng**:

.. tabs::
 .. code-tab:: gdscript GDScript

    var distance = normal.dot(point)

 .. code-tab:: csharp

    var distance = normal.Dot(point);

Nhưng không chỉ là khoảng cách tuyệt đối; nếu điểm nằm trong nửa không gian âm thì khoảng cách cũng sẽ là số âm:

.. image:: img/tutovec11.png

Điều này cho phép chúng ta biết một điểm nằm ở phía nào của mặt phẳng.

Xa gốc tọa độ
-------------

Tôi biết bạn đang nghĩ gì! Cho đến nay mọi thứ đều khá ổn, nhưng các mặt phẳng *thực sự* hiện diện ở khắp nơi trong không gian, chứ không chỉ đi qua gốc tọa độ. Bạn muốn thấy *mặt phẳng* hoạt động thực sự và muốn điều đó *ngay bây giờ*.

Hãy nhớ rằng các mặt phẳng không chỉ chia không gian thành hai phần, mà còn có *tính phân cực*. Điều này có nghĩa là có thể có các mặt phẳng chồng khít hoàn toàn, nhưng nửa không gian âm và dương của chúng bị hoán đổi.

Dựa trên điều này, hãy mô tả một mặt phẳng đầy đủ bằng một **pháp tuyến** *N* và một giá trị vô hướng **khoảng cách từ gốc tọa độ** *D*. Vì vậy, mặt phẳng của chúng ta được biểu diễn bằng N và D. Ví dụ:

.. image:: img/tutovec12.png

Đối với toán học 3D, Godot cung cấp một :ref:`Plane <class_Plane>` kiểu tích hợp sẵn để xử lý việc này.

Về cơ bản, N và D có thể biểu diễn bất kỳ mặt phẳng nào trong không gian, dù là 2D hay 3D (tùy thuộc vào số chiều của N), và phép toán đều giống nhau trong cả hai trường hợp. Nó giống như trước đây, nhưng D là khoảng cách từ gốc tọa độ đến mặt phẳng, di chuyển theo hướng N. Ví dụ, hãy tưởng tượng bạn muốn đi tới một điểm trên mặt phẳng; bạn chỉ cần thực hiện:

.. tabs::
 .. code-tab:: gdscript GDScript

    var point_in_plane = N*D

 .. code-tab:: csharp

    var pointInPlane = N * D;

Thao tác này sẽ kéo giãn (thay đổi kích thước) vector pháp tuyến và khiến nó chạm vào mặt phẳng. Phép toán này có vẻ khó hiểu, nhưng thực ra đơn giản hơn nhiều so với vẻ ngoài. Nếu muốn xác định lại khoảng cách từ điểm đến mặt phẳng, chúng ta thực hiện tương tự nhưng điều chỉnh theo khoảng cách:

.. tabs::
 .. code-tab:: gdscript GDScript

    var distance = N.dot(point) - D

 .. code-tab:: csharp

    var distance = N.Dot(point) - D;

Cùng một việc, sử dụng hàm tích hợp sẵn:

.. tabs::
 .. code-tab:: gdscript GDScript

    var distance = plane.distance_to(point)

 .. code-tab:: csharp

    var distance = plane.DistanceTo(point);

Một lần nữa, thao tác này sẽ trả về khoảng cách dương hoặc âm.

Có thể đảo tính phân cực của mặt phẳng bằng cách lấy phủ định cả N và D. Kết quả sẽ là một mặt phẳng ở cùng vị trí, nhưng các nửa không gian âm và dương bị đảo ngược:

.. tabs::
 .. code-tab:: gdscript GDScript

    N = -N
    D = -D

 .. code-tab:: csharp

    N = -N;
    D = -D;

Godot cũng triển khai toán tử này trong :ref:`Plane <class_Plane>`. Vì vậy, sử dụng định dạng dưới đây sẽ cho kết quả như mong đợi:

.. tabs::
 .. code-tab:: gdscript GDScript

    var inverted_plane = -plane

 .. code-tab:: csharp

    var invertedPlane = -plane;

Vậy hãy nhớ rằng, công dụng thực tế chính của mặt phẳng là chúng ta có thể tính khoảng cách đến nó. Vậy khi nào việc tính khoảng cách từ một điểm đến một mặt phẳng trở nên hữu ích? Hãy cùng xem một số ví dụ.

Tạo mặt phẳng trong 2D
----------------------

Các mặt phẳng rõ ràng không tự nhiên xuất hiện, vì vậy chúng phải được xây dựng. Việc tạo chúng trong 2D khá dễ; có thể thực hiện từ một pháp tuyến (vector đơn vị) và một điểm, hoặc từ hai điểm trong không gian.

Trong trường hợp có một pháp tuyến và một điểm, phần lớn công việc đã hoàn tất vì pháp tuyến đã được tính sẵn; do đó, hãy tính D từ tích vô hướng của pháp tuyến và điểm.

.. tabs::
 .. code-tab:: gdscript GDScript

    var N = normal
    var D = normal.dot(point)

 .. code-tab:: csharp

    var N = normal;
    var D = normal.Dot(point);

Với hai điểm trong không gian, thực tế có hai mặt phẳng đi qua chúng, cùng chia sẻ một không gian nhưng có pháp tuyến hướng theo hai hướng ngược nhau. Để tính pháp tuyến từ hai điểm, trước tiên phải lấy vector hướng, sau đó xoay nó 90 độ sang một trong hai phía:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tính vector từ `a` đến `b`.
    var dvec = point_a.direction_to(point_b)
    # Xoay 90 độ.
    var normal = Vector2(dvec.y, -dvec.x)
    # Hoặc (tùy thuộc vào phía mong muốn của pháp tuyến):
    # var normal = Vector2(-dvec.y, dvec.x)

 .. code-tab:: csharp

    // Tính vector từ `a` đến `b`.
    var dvec = pointA.DirectionTo(pointB);
    // Xoay 90 độ.
    var normal = new Vector2(dvec.Y, -dvec.X);
    // Hoặc (tùy thuộc vào phía mong muốn của pháp tuyến):
    // var normal = new Vector2(-dvec.Y, dvec.X);

Phần còn lại giống như ví dụ trước. point_a hoặc point_b đều được, vì chúng nằm trên cùng một mặt phẳng:

.. tabs::
 .. code-tab:: gdscript GDScript

    var N = normal
    var D = normal.dot(point_a)
    # cách này cũng hoạt động tương tự
    # var D = normal.dot(point_b)

 .. code-tab:: csharp

    var N = normal;
    var D = normal.Dot(pointA);
    // cách này cũng hoạt động tương tự
    // var D = normal.Dot(pointB);

Thực hiện tương tự trong 3D phức tạp hơn một chút và sẽ được giải thích ở phần bên dưới.

Một số ví dụ về mặt phẳng
-------------------------

Sau đây là một ví dụ về công dụng của các mặt phẳng. Hãy tưởng tượng bạn có một đa giác `lồi <https://www.mathsisfun.com/definitions/convex.html>`__. Ví dụ như hình chữ nhật, hình thang, hình tam giác hoặc bất kỳ đa giác nào không có mặt bị lõm vào trong.

Với mỗi đoạn của đa giác, chúng ta tính mặt phẳng đi qua đoạn đó. Khi đã có danh sách các mặt phẳng, chúng ta có thể thực hiện những việc hữu ích, chẳng hạn như kiểm tra xem một điểm có nằm bên trong đa giác hay không.

Chúng ta đi qua tất cả các mặt phẳng. Nếu tìm được một mặt phẳng mà khoảng cách đến điểm là số dương thì điểm nằm ngoài đa giác. Nếu không tìm được thì điểm nằm bên trong.

.. image:: img/tutovec13.png

Code sẽ tương tự như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var inside = true
    for p in planes:
        # kiểm tra xem khoảng cách đến mặt phẳng có dương không
        if (p.distance_to(point) > 0):
            inside = false
            break # chỉ cần một mặt phẳng không thỏa mãn là đủ

 .. code-tab:: csharp

    var inside = true;
    foreach (var p in planes)
    {
        // kiểm tra xem khoảng cách đến mặt phẳng có dương không
        if (p.DistanceTo(point) > 0)
        {
            inside = false;
            break; // chỉ cần một mặt phẳng không thỏa mãn là đủ
        }
    }

Khá thú vị, phải không? Nhưng mọi thứ còn tuyệt vời hơn nhiều! Chỉ cần thêm một chút công sức, logic tương tự cũng sẽ cho chúng ta biết khi nào hai đa giác lồi chồng lấp lên nhau. Đây được gọi là Định lý Trục Phân tách (Separating Axis Theorem, hay SAT), và hầu hết physics engine đều dùng nó để phát hiện va chạm.

Với một điểm, chỉ cần kiểm tra xem một mặt phẳng có trả về khoảng cách dương hay không là đủ để biết điểm có nằm bên ngoài hay không. Với một đa giác khác, chúng ta phải tìm một mặt phẳng mà *tất cả* *các* *điểm* *của đa giác* *kia* trả về khoảng cách dương đến nó. Việc kiểm tra này được thực hiện với các mặt phẳng của A đối chiếu với các điểm của B, sau đó với các mặt phẳng của B đối chiếu với các điểm của A:

.. image:: img/tutovec14.png

Code sẽ tương tự như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var overlapping = true

    for p in planes_of_A:
        var all_out = true
        for v in points_of_B:
            if (p.distance_to(v) < 0):
                all_out = false
                break

        if (all_out):
            # đã tìm thấy một mặt phẳng phân tách
            # không tiếp tục kiểm tra
            overlapping = false
            break

    if (overlapping):
        # chỉ thực hiện kiểm tra này nếu chưa có mặt phẳng phân tách nào
        # được tìm thấy trong các mặt phẳng của A
        for p in planes_of_B:
            var all_out = true
            for v in points_of_A:
                if (p.distance_to(v) < 0):
                    all_out = false
                    break

            if (all_out):
                overlapping = false
                break

    if (overlapping):
        print("Polygons Collided!")

 .. code-tab:: csharp

        var overlapping = true;

        foreach (Plane plane in planesOfA)
        {
            var allOut = true;
            foreach (Vector3 point in pointsOfB)
            {
                if (plane.DistanceTo(point) < 0)
                {
                    allOut = false;
                    break;
                }
            }

            if (allOut)
            {
                // đã tìm thấy một mặt phẳng phân tách
                // không tiếp tục kiểm tra
                overlapping = false;
                break;
            }
        }

        if (overlapping)
        {
            // chỉ thực hiện kiểm tra này nếu chưa có mặt phẳng phân tách nào
            // được tìm thấy trong các mặt phẳng của A
            foreach (Plane plane in planesOfB)
            {
                var allOut = true;
                foreach (Vector3 point in pointsOfA)
                {
                    if (plane.DistanceTo(point) < 0)
                    {
                        allOut = false;
                        break;
                    }
                }

                if (allOut)
                {
                    overlapping = false;
                    break;
                }
            }
        }

        if (overlapping)
        {
            GD.Print("Polygons Collided!");
        }

Như bạn có thể thấy, các mặt phẳng khá hữu ích, và đây mới chỉ là phần nổi của tảng băng. Có thể bạn đang thắc mắc điều gì xảy ra với các đa giác không lồi. Thông thường, ta chỉ cần chia đa giác lõm thành các đa giác lồi nhỏ hơn, hoặc sử dụng một kỹ thuật như BSP (ngày nay không còn được dùng nhiều).

Phát hiện va chạm trong 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~

Đây là một phần thưởng khác, dành cho việc bạn đã kiên nhẫn và theo kịp tutorial dài này. Sau đây là một kiến thức hữu ích khác. Điều này có thể không có trường hợp sử dụng trực tiếp (Godot vốn đã xử lý việc phát hiện va chạm khá tốt), nhưng nó được hầu hết physics engine và thư viện phát hiện va chạm sử dụng :)

Bạn còn nhớ việc chuyển một hình lồi trong 2D thành một mảng các mặt phẳng 2D hữu ích cho việc phát hiện va chạm không? Bạn có thể phát hiện một điểm nằm bên trong bất kỳ hình lồi nào, hoặc hai hình lồi 2D có chồng lấp lên nhau hay không.

Điều này cũng đúng trong 3D. Nếu hai hình đa diện 3D đang va chạm, bạn sẽ không thể tìm được mặt phẳng phân tách. Nếu tìm được một mặt phẳng phân tách thì chắc chắn các hình đó không va chạm.

Nhắc lại một chút: mặt phẳng phân tách có nghĩa là tất cả các đỉnh của đa giác A nằm về một phía của mặt phẳng, còn tất cả các đỉnh của đa giác B nằm ở phía bên kia. Mặt phẳng này luôn là một trong các mặt phẳng-mặt của đa giác A hoặc đa giác B.

Tuy nhiên, trong 3D, cách tiếp cận này có một vấn đề, vì trong một số trường hợp có thể không tìm được mặt phẳng phân tách. Đây là một ví dụ về tình huống như vậy:

.. image:: img/tutovec22.png

Để tránh điều này, cần kiểm tra thêm một số mặt phẳng để làm mặt phẳng phân tách. Các mặt phẳng này là tích có hướng giữa các cạnh của đa giác A và các cạnh của đa giác B.

.. image:: img/tutovec23.png

Vậy thuật toán cuối cùng sẽ tương tự như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var overlapping = true

    for p in planes_of_A:
        var all_out = true
        for v in points_of_B:
            if (p.distance_to(v) < 0):
                all_out = false
                break

        if (all_out):
            # đã tìm thấy một mặt phẳng phân tách
            # không tiếp tục kiểm tra
            overlapping = false
            break

    if (overlapping):
        # chỉ thực hiện kiểm tra này nếu chưa có mặt phẳng phân tách nào
        # được tìm thấy trong các mặt phẳng của A
        for p in planes_of_B:
            var all_out = true
            for v in points_of_A:
                if (p.distance_to(v) < 0):
                    all_out = false
                    break

            if (all_out):
                overlapping = false
                break

    if (overlapping):
        for ea in edges_of_A:
            for eb in edges_of_B:
                var n = ea.cross(eb)
                if (n.length() == 0):
                    continue

                var max_A = -1e20 # số rất nhỏ
                var min_A = 1e20 # số rất lớn

                # chúng ta đang sử dụng trực tiếp tích vô hướng
                # để có thể xác định khoảng giá trị lớn nhất và nhỏ nhất
                # cho mỗi đa giác, sau đó kiểm tra xem chúng có
                # chồng lấp lên nhau không.

                for v in points_of_A:
                    var d = n.dot(v)
                    max_A = max(max_A, d)
                    min_A = min(min_A, d)

                var max_B = -1e20 # số rất nhỏ
                var min_B = 1e20 # số rất lớn

                for v in points_of_B:
                    var d = n.dot(v)
                    max_B = max(max_B, d)
                    min_B = min(min_B, d)

                if (min_A > max_B or min_B > max_A):
                    # không chồng lấp!
                    overlapping = false
                    break

            if (not overlapping):
                break

    if (overlapping):
       print("Polygons collided!")

 .. code-tab:: csharp

    var overlapping = true;

    foreach (Plane plane in planesOfA)
    {
        var allOut = true;
        foreach (Vector3 point in pointsOfB)
        {
            if (plane.DistanceTo(point) < 0)
            {
                allOut = false;
                break;
            }
        }

        if (allOut)
        {
            // đã tìm thấy một mặt phẳng phân tách
            // không tiếp tục kiểm tra
            overlapping = false;
            break;
        }
    }

    if (overlapping)
    {
        // chỉ thực hiện kiểm tra này nếu chưa có mặt phẳng phân tách nào
        // được tìm thấy trong các mặt phẳng của A
        foreach (Plane plane in planesOfB)
        {
            var allOut = true;
            foreach (Vector3 point in pointsOfA)
            {
                if (plane.DistanceTo(point) < 0)
                {
                    allOut = false;
                    break;
                }
            }

            if (allOut)
            {
                overlapping = false;
                break;
            }
        }
    }

    if (overlapping)
    {
        foreach (Vector3 edgeA in edgesOfA)
        {
            foreach (Vector3 edgeB in edgesOfB)
            {
                var normal = edgeA.Cross(edgeB);
                if (normal.Length() == 0)
                {
                    continue;
                }

                var maxA = float.MinValue; // số rất nhỏ
                var minA = float.MaxValue; // số rất lớn

                // chúng ta đang sử dụng trực tiếp tích vô hướng
                // để có thể xác định khoảng giá trị lớn nhất và nhỏ nhất
                // cho mỗi đa giác, sau đó kiểm tra xem chúng có
                // chồng lấp lên nhau không.

                foreach (Vector3 point in pointsOfA)
                {
                    var distance = normal.Dot(point);
                    maxA = Mathf.Max(maxA, distance);
                    minA = Mathf.Min(minA, distance);
                }

                var maxB = float.MinValue; // số rất nhỏ
                var minB = float.MaxValue; // số rất lớn

                foreach (Vector3 point in pointsOfB)
                {
                    var distance = normal.Dot(point);
                    maxB = Mathf.Max(maxB, distance);
                    minB = Mathf.Min(minB, distance);
                }

                if (minA > maxB || minB > maxA)
                {
                    // không chồng lấp!
                    overlapping = false;
                    break;
                }
            }

            if (!overlapping)
            {
                break;
            }

        }
    }

    if (overlapping)
    {
        GD.Print("Polygons Collided!");
    }

Thông tin thêm
~~~~~~~~~~~~~~

Để biết thêm thông tin về cách sử dụng phép toán vector trong Godot, hãy xem bài viết sau:

- :ref:`doc_matrices_and_transforms`

Nếu bạn muốn có thêm phần giải thích, hãy xem loạt video xuất sắc `Essence of Linear Algebra <https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab>`_ của 3Blue1Brown.

.. _`Essence of Linear Algebra`: https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab
