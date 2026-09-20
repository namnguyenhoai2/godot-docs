.. _doc_matrices_and_transforms:

Ma trận và phép biến đổi
========================

Giới thiệu
----------

Trước khi đọc tutorial này, chúng tôi khuyên bạn nên đọc kỹ và hiểu rõ tutorial :ref:`doc_vector_math`, vì tutorial này yêu cầu kiến thức về vector.

Tutorial này nói về *phép biến đổi* và cách biểu diễn chúng trong Godot bằng ma trận. Đây không phải là hướng dẫn chuyên sâu đầy đủ về ma trận. Phần lớn thời gian, các phép biến đổi được áp dụng dưới dạng tịnh tiến, xoay và scale, vì vậy chúng ta sẽ tập trung vào cách biểu diễn những phép biến đổi đó bằng ma trận.

Phần lớn hướng dẫn này tập trung vào 2D, sử dụng :ref:`class_Transform2D` và
:ref:`class_Vector2`, but the way things work in 3D is very similar.

.. note:: As mentioned in the previous tutorial, it is important to
          hãy nhớ rằng trong Godot, trục Y hướng *xuống* trong 2D. Điều này ngược với cách hầu hết trường học dạy đại số tuyến tính, trong đó trục Y hướng lên.

.. note:: The convention is that the X axis is red, the Y axis is
          màu xanh lá, còn trục Z có màu xanh dương. Tutorial này sử dụng mã màu phù hợp với các quy ước đó, nhưng chúng ta cũng sẽ biểu diễn vector gốc bằng màu xanh dương.

Các thành phần của ma trận và ma trận Identity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ma trận identity biểu diễn một phép biến đổi không có tịnh tiến, không có xoay và không có scale. Hãy bắt đầu bằng cách xem ma trận identity và cách các thành phần của nó liên hệ với hình ảnh trực quan của ma trận.

.. image:: img/matrices_and_transforms/identity.png

Ma trận có các hàng và cột, đồng thời ma trận biến đổi có những quy ước cụ thể về chức năng của từng phần.

Trong hình trên, chúng ta có thể thấy vector X màu đỏ được biểu diễn bởi cột đầu tiên của ma trận, còn vector Y màu xanh lá tương tự được biểu diễn bởi cột thứ hai. Thay đổi các cột sẽ làm thay đổi những vector này. Chúng ta sẽ xem cách thao tác với chúng trong một vài ví dụ tiếp theo.

Bạn không cần lo lắng về việc thao tác trực tiếp với các hàng, vì chúng ta thường làm việc với các cột. Tuy nhiên, bạn có thể hình dung các hàng của ma trận cho biết những vector nào góp phần tạo ra chuyển động theo một hướng nhất định.

Khi đề cập đến một giá trị như ``t.x.y``, đó là thành phần Y của vector cột X. Nói cách khác, đó là phần dưới cùng bên trái của ma trận. Tương tự, ``t.x.x`` là phía trên bên trái, ``t.y.x`` là phía trên bên phải và ``t.y.y`` là phía dưới bên phải, trong đó ``t`` là Transform2D.

Scale ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~

Áp dụng scale là một trong những phép toán dễ hiểu nhất. Hãy bắt đầu bằng cách đặt logo Godot bên dưới các vector để có thể nhìn thấy trực quan các hiệu ứng trên một đối tượng:

.. image:: img/matrices_and_transforms/identity-godot.png

Bây giờ, để scale ma trận, tất cả những gì chúng ta cần làm là nhân mỗi thành phần với giá trị scale mong muốn. Hãy scale nó lên 2 lần. 1 nhân 2 bằng 2, còn 0 nhân 2 bằng 0, vì vậy chúng ta thu được kết quả sau:

.. image:: img/matrices_and_transforms/scale.png

Để thực hiện việc này trong code, chúng ta nhân từng vector:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = Transform2D()
    # Scale
    t.x *= 2
    t.y *= 2
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính toán.

 .. code-tab:: csharp

    Transform2D t = Transform2D.Identity;
    // Scale
    t.X *= 2;
    t.Y *= 2;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính toán.

Nếu muốn đưa nó về scale ban đầu, chúng ta có thể nhân mỗi thành phần với 0.5. Về cơ bản, đó là tất cả những gì cần biết về việc scale một ma trận biến đổi.

Để tính scale của đối tượng từ một ma trận biến đổi hiện có, bạn có thể sử dụng ``length()`` trên từng vector cột.

.. note:: In actual projects, you can use the ``scaled()``
          method để thực hiện scaling.

Xoay ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~

Chúng ta sẽ bắt đầu giống như phần trước, với logo Godot bên dưới ma trận identity:

.. image:: img/matrices_and_transforms/identity-godot.png

Ví dụ, giả sử chúng ta muốn xoay logo Godot theo chiều kim đồng hồ 90 độ. Hiện tại, trục X hướng sang phải và trục Y hướng xuống. Nếu xoay chúng trong đầu, chúng ta sẽ thấy hợp lý rằng trục X mới phải hướng xuống, còn trục Y mới phải hướng sang trái.

Bạn có thể hình dung rằng mình nắm cả logo Godot lẫn các vector của nó, rồi xoay chúng quanh tâm. Vị trí bạn dừng lại sau khi xoay sẽ xác định hướng của các vector, từ đó xác định ma trận.

Chúng ta cần biểu diễn "xuống" và "trái" trong hệ tọa độ thông thường, vì vậy chúng ta sẽ đặt X thành (0, 1) và Y thành (-1, 0). Đây cũng là các giá trị của ``Vector2.DOWN`` và ``Vector2.LEFT``. Khi làm vậy, chúng ta thu được kết quả xoay đối tượng mong muốn:

.. image:: img/matrices_and_transforms/rotate1.png

Nếu bạn gặp khó khăn trong việc hiểu phần trên, hãy thử bài tập này: Cắt một hình vuông bằng giấy, vẽ các vector X và Y lên đó, đặt nó lên giấy kẻ ô, sau đó xoay nó và ghi lại các điểm cuối.

Để thực hiện phép xoay trong code, chúng ta cần có khả năng tính toán các giá trị bằng chương trình. Hình này cho thấy các công thức cần thiết để tính ma trận biến đổi từ một góc xoay. Đừng lo nếu phần này có vẻ phức tạp, tôi hứa đây là điều khó nhất mà bạn cần biết.

.. image:: img/matrices_and_transforms/rotate2.png

.. note:: Godot represents all rotations with radians, not degrees.
          Một vòng xoay đầy đủ là `TAU` hoặc `PI*2` radian, còn một phần tư vòng xoay 90 độ là `TAU/4` hoặc `PI/2` radian. Sử dụng `TAU` thường giúp code dễ đọc hơn.

.. note:: Fun fact: In addition to Y being *down* in Godot, rotation
          được biểu diễn theo chiều kim đồng hồ. Điều này có nghĩa là tất cả các hàm toán học và lượng giác hoạt động giống như trong hệ Y hướng lên và CCW, vì những khác biệt này "triệt tiêu lẫn nhau". Bạn có thể hình dung phép xoay trong cả hai hệ đều là "từ X đến Y".

Để thực hiện phép xoay 0.5 radian (khoảng 28.65 độ), chúng ta thay giá trị 0.5 vào công thức trên và tính toán để tìm ra các giá trị thực tế cần có:

.. image:: img/matrices_and_transforms/rotate3.png

Dưới đây là cách thực hiện trong code (gắn script vào một Node2D):

.. tabs::
 .. code-tab:: gdscript GDScript

    var rot = 0.5 # Phép xoay cần áp dụng.
    var t = Transform2D()
    t.x.x = cos(rot)
    t.y.y = cos(rot)
    t.x.y = sin(rot)
    t.y.x = -sin(rot)
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính toán.

 .. code-tab:: csharp

    float rot = 0.5f; // Phép xoay cần áp dụng.
    Transform2D t = Transform2D.Identity;
    t.X.X = t.Y.Y = Mathf.Cos(rot);
    t.X.Y = t.Y.X = Mathf.Sin(rot);
    t.Y.X *= -1;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính toán.

Để tính phép xoay của đối tượng từ một ma trận biến đổi hiện có, bạn có thể sử dụng ``atan2(t.x.y, t.x.x)``, trong đó t là Transform2D.

.. note:: In actual projects, you can use the ``rotated()``
          method để thực hiện phép xoay.

Basis của ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~

Cho đến nay, chúng ta chỉ làm việc với các vector ``x`` và ``y``, vốn chịu trách nhiệm biểu diễn phép xoay, scale và/hoặc shear (nâng cao, được trình bày ở cuối). Hai vector X và Y cùng được gọi là *basis* của ma trận biến đổi. Các thuật ngữ "basis" và "basis vectors" rất quan trọng cần biết.

Có thể bạn đã nhận thấy rằng :ref:`class_Transform2D` thực sự có ba giá trị :ref:`class_Vector2`: ``x``, ``y`` và ``origin``. Giá trị ``origin`` không thuộc basis, nhưng là một phần của transform và cần thiết để biểu diễn vị trí. Từ đây trở đi, chúng ta sẽ theo dõi vector gốc trong tất cả các ví dụ. Bạn có thể nghĩ ``origin`` như một cột khác, nhưng thường sẽ tốt hơn nếu xem nó là một thành phần hoàn toàn riêng biệt.

Lưu ý rằng trong 3D, Godot có một cấu trúc :ref:`class_Basis` riêng để chứa ba giá trị :ref:`class_Vector3` của basis, vì code có thể trở nên phức tạp và việc tách nó khỏi :ref:`class_Transform3D` (được tạo thành từ một
:ref:`class_Basis` and one extra :ref:`class_Vector3` for the origin).

Tịnh tiến ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~

Thay đổi vector gốc được gọi là *tịnh tiến* ma trận biến đổi. Tịnh tiến về cơ bản là một thuật ngữ kỹ thuật cho việc "di chuyển" đối tượng, nhưng rõ ràng không bao gồm bất kỳ phép xoay nào.

Hãy cùng thực hiện một ví dụ để hiểu rõ hơn. Chúng ta sẽ bắt đầu với transform identity như lần trước, nhưng lần này sẽ theo dõi cả vector gốc.

.. image:: img/matrices_and_transforms/identity-origin.png

Nếu muốn di chuyển đối tượng đến vị trí (1, 2), chúng ta cần đặt vector gốc của nó thành (1, 2):

.. image:: img/matrices_and_transforms/translate.png

Ngoài ra còn có method ``translated_local()``, thực hiện một thao tác khác với việc cộng hoặc thay đổi trực tiếp ``origin``. Method ``translated_local()`` sẽ tịnh tiến đối tượng *tương đối với phép xoay của chính nó*. Ví dụ, một đối tượng được xoay 90 độ theo chiều kim đồng hồ sẽ di chuyển sang phải khi gọi ``translated_local()`` với ``Vector2.UP``. Để tịnh tiến *tương đối với hệ tọa độ global/parent*, hãy sử dụng ``translated()``.

.. note:: Godot's 2D uses coordinates based on pixels, so in actual
          trong các project, bạn sẽ muốn tịnh tiến hàng trăm unit.

Kết hợp tất cả
~~~~~~~~~~~~~~

Chúng ta sẽ áp dụng mọi điều đã đề cập cho đến nay vào một transform. Để làm theo, hãy tạo một project với node Sprite2D và sử dụng logo Godot làm texture resource.

Hãy đặt translation thành (350, 150), xoay -0.5 rad và scale lên 3. Tôi đã đăng ảnh chụp màn hình cùng code để tái tạo kết quả đó, nhưng khuyến khích bạn thử tự tái tạo ảnh chụp màn hình mà không nhìn vào code!

.. image:: img/matrices_and_transforms/putting-all-together.png

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = Transform2D()
    # Translation
    t.origin = Vector2(350, 150)
    # Rotation
    var rot = -0.5 # Phép xoay cần áp dụng.
    t.x.x = cos(rot)
    t.y.y = cos(rot)
    t.x.y = sin(rot)
    t.y.x = -sin(rot)
    # Scale
    t.x *= 3
    t.y *= 3
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính toán.

 .. code-tab:: csharp

    Transform2D t = Transform2D.Identity;
    // Translation
    t.Origin = new Vector2(350, 150);
    // Rotation
    float rot = -0.5f; // Phép xoay cần áp dụng.
    t.X.X = t.Y.Y = Mathf.Cos(rot);
    t.X.Y = t.Y.X = Mathf.Sin(rot);
    t.Y.X *= -1;
    // Scale
    t.X *= 3;
    t.Y *= 3;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính toán.

Shear ma trận biến đổi (nâng cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: If you are only looking for how to *use* transformation matrices,
          bạn có thể bỏ qua phần này của tutorial. Phần này tìm hiểu một khía cạnh ít được sử dụng của ma trận biến đổi nhằm giúp xây dựng hiểu biết về chúng.

          Node2D cung cấp sẵn thuộc tính shear.

Có thể bạn đã nhận thấy rằng một transform có nhiều bậc tự do hơn tổ hợp các thao tác trên. Basis của ma trận biến đổi 2D có tổng cộng bốn số trong hai giá trị :ref:`class_Vector2`, trong khi một giá trị rotation và một Vector2 dùng cho scale chỉ có 3 số. Khái niệm cấp cao về bậc tự do còn thiếu này được gọi là *shear*.

Thông thường, các vector basis sẽ luôn vuông góc với nhau. Tuy nhiên, shear có thể hữu ích trong một số tình huống, và việc hiểu shear sẽ giúp bạn hiểu cách các transform hoạt động.

Để minh họa trực quan cho bạn thấy nó sẽ trông như thế nào, hãy phủ một lưới lên logo Godot:

.. image:: img/matrices_and_transforms/identity-grid.png

Mỗi điểm trên lưới này được tạo ra bằng cách cộng các vector cơ sở với nhau. Góc dưới bên phải là X + Y, còn góc trên bên phải là X - Y. Nếu thay đổi các vector cơ sở, toàn bộ lưới cũng di chuyển theo, vì lưới được tạo thành từ các vector cơ sở. Tất cả các đường trên lưới hiện đang song song sẽ vẫn song song bất kể chúng ta thay đổi các vector cơ sở như thế nào.

Ví dụ, hãy đặt Y thành (1, 1):

.. image:: img/matrices_and_transforms/shear.png

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = Transform2D()
    # Shear bằng cách đặt Y thành (1, 1)
    t.y = Vector2.ONE
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính.

 .. code-tab:: csharp

    Transform2D t = Transform2D.Identity;
    // Shear bằng cách đặt Y thành (1, 1)
    t.Y = Vector2.One;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính.

.. note:: You can't set the raw values of a Transform2D in the editor,
          vì vậy bạn *phải* dùng code nếu muốn shear object.

Do các vector không còn vuông góc với nhau, object đã bị shear. Tâm dưới của lưới, có tọa độ là (0, 1) so với chính nó, giờ nằm tại vị trí world (1, 1).

Các tọa độ bên trong object được gọi là tọa độ UV trong texture, vì vậy hãy mượn thuật ngữ đó ở đây. Để tìm vị trí world từ một vị trí tương đối, công thức là U * X + V * Y, trong đó U và V là các số, còn X và Y là các vector cơ sở.

Góc dưới bên phải của lưới, luôn có vị trí UV là (1, 1), nằm tại vị trí world (2, 1), được tính từ X*1 + Y*1, tức là (1, 0) + (1, 1), hay (1 + 1, 0 + 1), hay (2, 1). Điều này khớp với quan sát của chúng ta về vị trí của góc dưới bên phải hình ảnh.

Tương tự, góc trên bên phải của lưới, luôn có vị trí UV là (1, -1), nằm tại vị trí world (0, -1), được tính từ X*1 + Y*-1, tức là (1, 0) - (1, 1), hay (1 - 1, 0 - 1), hay (0, -1). Điều này khớp với quan sát của chúng ta về vị trí của góc trên bên phải hình ảnh.

Hy vọng giờ đây bạn đã hiểu đầy đủ cách một transformation matrix tác động lên object, cũng như mối quan hệ giữa các vector cơ sở và cách vị trí world của "UV" hay "intra-coordinates" của object thay đổi.

.. note:: In Godot, all transform math is done relative to the parent node.
          Khi chúng ta nói đến "vị trí world", nó sẽ là vị trí tương đối so với node cha của node đó, nếu node có node cha.

Nếu muốn có thêm lời giải thích, bạn nên xem video xuất sắc của 3Blue1Brown về linear transformations: https://www.youtube.com/watch?v=kYB8IZa5AuE

Ứng dụng thực tế của transform
------------------------------

Trong các project thực tế, bạn thường sẽ làm việc với các transform lồng trong transform bằng cách có nhiều node :ref:`class_Node2D` hoặc :ref:`class_Node3D` được parent với nhau.

Tuy nhiên, việc hiểu cách tự tính các giá trị cần thiết vẫn rất hữu ích. Chúng ta sẽ tìm hiểu cách bạn có thể sử dụng :ref:`class_Transform2D` hoặc
:ref:`class_Transform3D` to manually calculate transforms of nodes.

Chuyển đổi vị trí giữa các transform
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có nhiều trường hợp bạn muốn chuyển đổi một vị trí vào hoặc ra khỏi một transform. Ví dụ, nếu bạn có một vị trí tương đối so với player và muốn tìm vị trí world (tương đối so với parent), hoặc nếu bạn có một vị trí world và muốn biết nó nằm ở đâu so với player.

Chúng ta có thể tìm cách biểu diễn một vector tương đối so với player trong world space bằng toán tử ``*``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Vector world space nằm thấp hơn player 100 đơn vị.
    print(transform * Vector2(0, 100))

 .. code-tab:: csharp

    // Vector world space nằm thấp hơn player 100 đơn vị.
    GD.Print(Transform * new Vector2(0, 100));

Và chúng ta có thể dùng toán tử ``*`` theo thứ tự ngược lại để tìm vị trí world space nếu nó được xác định tương đối so với player:

.. tabs::
 .. code-tab:: gdscript GDScript

    # (0, 100) nằm ở đâu so với player?
    print(Vector2(0, 100) * transform)

 .. code-tab:: csharp

    // (0, 100) nằm ở đâu so với player?
    GD.Print(new Vector2(0, 100) * Transform);

.. note:: If you know in advance that the transform is positioned at
          (0, 0), thay vào đó bạn có thể sử dụng các method "basis_xform" hoặc "basis_xform_inv", vốn bỏ qua việc xử lý translation.

Di chuyển object tương đối so với chính nó
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một thao tác phổ biến, đặc biệt trong game 3D, là di chuyển một object tương đối so với chính nó. Ví dụ, trong các game bắn súng góc nhìn thứ nhất, bạn sẽ muốn nhân vật di chuyển về phía trước (trục -Z) khi nhấn :kbd:`W`.

Vì các vector cơ sở là hướng tương đối so với parent, còn vector origin là vị trí tương đối so với parent, chúng ta có thể cộng các bội số của vector cơ sở để di chuyển object tương đối so với chính nó.

Đoạn code này di chuyển một object 100 đơn vị sang bên phải của chính nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    transform.origin += transform.x * 100

 .. code-tab:: csharp

    Transform2D t = Transform;
    t.Origin += t.X * 100;
    Transform = t;

Để di chuyển trong 3D, bạn cần thay "x" bằng "basis.x".

.. note:: In actual projects, you can use ``translate_object_local`` in 3D
          hoặc ``move_local_x`` và ``move_local_y`` trong 2D để thực hiện việc này.

Áp dụng các transform lên nhau
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một trong những điều quan trọng nhất cần biết về transform là cách bạn có thể kết hợp nhiều transform với nhau. Transform của node cha ảnh hưởng đến tất cả node con của nó. Hãy cùng phân tích một ví dụ.

Trong hình ảnh này, node con có số "2" sau tên các thành phần để phân biệt chúng với node cha. Có thể trông hơi choáng ngợp với quá nhiều con số, nhưng hãy nhớ rằng mỗi con số được hiển thị hai lần (bên cạnh các mũi tên và trong các matrix), và gần một nửa số đó là số không.

.. image:: img/matrices_and_transforms/apply.png

Các transformation duy nhất đang diễn ra ở đây là node cha được đặt scale là (2, 1), node con được đặt scale là (0.5, 0.5), và cả hai node đều được đặt vị trí.

Tất cả transformation của node con đều chịu ảnh hưởng của transformation của node cha. Node con có scale là (0.5, 0.5), vì vậy bạn sẽ mong đợi nó là một hình vuông có tỷ lệ 1:1, và đúng là như vậy, nhưng chỉ khi xét tương đối so với node cha. Vector X của node con cuối cùng là (1, 0) trong world space, vì nó được scale theo các vector cơ sở của node cha. Tương tự, vector ``origin`` của node con được đặt thành (1, 1), nhưng thực tế điều này di chuyển nó đến (2, 1) trong world space, do các vector cơ sở của node cha.

Để tự tính transformation world space của transform node con, chúng ta sẽ sử dụng đoạn code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thiết lập các transform giống như trong hình, ngoại trừ việc đặt các vị trí lớn hơn 100 lần.
    var parent = Transform2D(Vector2(2, 0), Vector2(0, 1), Vector2(100, 200))
    var child = Transform2D(Vector2(0.5, 0), Vector2(0, 0.5), Vector2(100, 100))

    # Tính transformation world space của node con
    # origin = (2, 0) * 100 + (0, 1) * 100 + (100, 200)
    var origin = parent.x * child.origin.x + parent.y * child.origin.y + parent.origin
    # basis_x = (2, 0) * 0.5 + (0, 1) * 0
    var basis_x = parent.x * child.x.x + parent.y * child.x.y
    # basis_y = (2, 0) * 0 + (0, 1) * 0.5
    var basis_y = parent.x * child.y.x + parent.y * child.y.y

    # Thay đổi transform của node thành giá trị chúng ta đã tính.
    transform = Transform2D(basis_x, basis_y, origin)

 .. code-tab:: csharp

    // Thiết lập các transform giống như trong hình, ngoại trừ việc đặt các vị trí lớn hơn 100 lần.
    Transform2D parent = new Transform2D(2, 0, 0, 1, 100, 200);
    Transform2D child = new Transform2D(0.5f, 0, 0, 0.5f, 100, 100);

    // Tính transformation world space của node con
    // origin = (2, 0) * 100 + (0, 1) * 100 + (100, 200)
    Vector2 origin = parent.X * child.Origin.X + parent.Y * child.Origin.Y + parent.Origin;
    // basisX = (2, 0) * 0.5 + (0, 1) * 0 = (0.5, 0)
    Vector2 basisX = parent.X * child.X.X + parent.Y * child.X.Y;
    // basisY = (2, 0) * 0 + (0, 1) * 0.5 = (0.5, 0)
    Vector2 basisY = parent.X * child.Y.X + parent.Y * child.Y.Y;

    // Thay đổi transform của node thành giá trị chúng ta đã tính.
    Transform = new Transform2D(basisX, basisY, origin);

Trong các project thực tế, chúng ta có thể tìm transformation world của node con bằng cách áp dụng một transform lên transform khác, sử dụng toán tử ``*``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thiết lập các transform giống như trong hình, ngoại trừ việc đặt các vị trí lớn hơn 100 lần.
    var parent = Transform2D(Vector2(2, 0), Vector2(0, 1), Vector2(100, 200))
    var child = Transform2D(Vector2(0.5, 0), Vector2(0, 0.5), Vector2(100, 100))

    # Thay đổi transform của node thành giá trị tương ứng với transformation world của node con.
    transform = parent * child

 .. code-tab:: csharp

    // Thiết lập các transform giống như trong hình, ngoại trừ việc đặt các vị trí lớn hơn 100 lần.
    Transform2D parent = new Transform2D(2, 0, 0, 1, 100, 200);
    Transform2D child = new Transform2D(0.5f, 0, 0, 0.5f, 100, 100);

    // Thay đổi transform của node thành giá trị tương ứng với transformation world của node con.
    Transform = parent * child;

.. note:: When multiplying matrices, order matters! Don't mix them up.

Cuối cùng, áp dụng identity transform sẽ luôn không làm gì cả.

Nếu muốn có thêm lời giải thích, bạn nên xem video xuất sắc của 3Blue1Brown về matrix composition: https://www.youtube.com/watch?v=XkY2DOUCWMU

Đảo ngược transformation matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hàm ``affine_inverse`` trả về một transform có tác dụng "hoàn tác" transform trước đó. Điều này có thể hữu ích trong một số tình huống. Hãy cùng xem một vài ví dụ.

Nhân một inverse transform với transform thông thường sẽ hoàn tác tất cả transformation:

.. tabs::
 .. code-tab:: gdscript GDScript

    var ti = transform.affine_inverse()
    var t = ti * transform
    # Transform là identity transform.

 .. code-tab:: csharp

    Transform2D ti = Transform.AffineInverse();
    Transform2D t = ti * Transform;
    // Transform là identity transform.

Biến đổi một vị trí bằng một transform và inverse của nó sẽ cho ra cùng vị trí đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    var ti = transform.affine_inverse()
    position = transform * position
    position = ti * position
    # Vị trí giống như trước.

 .. code-tab:: csharp

    Transform2D ti = Transform.AffineInverse();
    Position = Transform * Position;
    Position = ti * Position;
    // Vị trí giống như trước.

Mọi thứ hoạt động như thế nào trong 3D?
---------------------------------------

Một trong những điều tuyệt vời về transformation matrix là chúng hoạt động rất tương tự nhau giữa transformation 2D và 3D. Tất cả code và công thức được sử dụng ở trên cho 2D cũng hoạt động tương tự trong 3D, với 3 ngoại lệ: có thêm một trục thứ ba, mỗi trục có kiểu :ref:`class_Vector3`, và Godot lưu :ref:`class_Basis` riêng biệt với :ref:`class_Transform3D`, vì phép toán có thể trở nên phức tạp và việc tách chúng ra là hợp lý.

Tất cả khái niệm về cách translation, rotation, scale và shearing hoạt động trong 3D đều giống với 2D. Để scale, chúng ta lấy từng component và nhân nó; để rotate, chúng ta thay đổi hướng của từng vector cơ sở; để translate, chúng ta thao tác với origin; còn để shear, chúng ta thay đổi các vector cơ sở để chúng không vuông góc với nhau.

.. image:: img/matrices_and_transforms/3d-identity.png

Nếu muốn, bạn nên thử thao tác với các transform để hiểu cách chúng hoạt động. Godot cho phép bạn chỉnh sửa trực tiếp các transformation matrix 3D từ inspector. Bạn có thể tải project này, trong đó có các đường và khối lập phương được tô màu để giúp hình dung
:ref:`class_Basis` vectors and the origin in both 2D and 3D:
https://github.com/godotengine/godot-demo-projects/tree/master/misc/matrix_transform

.. UPDATE: Có thể thay đổi trong tương lai. Khi bạn có thể chỉnh sửa trực tiếp transformation matrix của Node2D .. hãy xóa hoặc cập nhật ghi chú này.

.. note:: You cannot edit Node2D's transform matrix directly in Godot 4.0's
          inspector. Điều này có thể được thay đổi trong một bản phát hành tương lai của Godot.

Nếu bạn muốn có thêm phần giải thích, hãy xem video tuyệt vời của 3Blue1Brown về các phép biến đổi tuyến tính 3D: https://www.youtube.com/watch?v=rHLEWRxRGiM

Biểu diễn phép xoay trong 3D (nâng cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Điểm khác biệt lớn nhất giữa các ma trận biến đổi 2D và 3D là cách bạn biểu diễn riêng phép xoay mà không cần các vector cơ sở.

Với 2D, chúng ta có một cách đơn giản (atan2) để chuyển đổi giữa một ma trận biến đổi và một góc. Trong 3D, phép xoay quá phức tạp để biểu diễn bằng một số duy nhất. Có một khái niệm gọi là các góc Euler, có thể biểu diễn phép xoay dưới dạng một tập hợp gồm 3 số, tuy nhiên chúng bị giới hạn và không hữu ích lắm, ngoại trừ những trường hợp đơn giản.

Trong 3D, chúng ta thường không sử dụng các góc; thay vào đó, chúng ta sử dụng một cơ sở biến đổi (được dùng gần như ở mọi nơi trong Godot), hoặc sử dụng quaternion. Godot có thể biểu diễn quaternion bằng struct :ref:`class_Quaternion`. Tôi khuyên bạn nên hoàn toàn bỏ qua cách chúng hoạt động bên dưới, vì chúng rất phức tạp và không trực quan.

Tuy nhiên, nếu bạn thực sự muốn biết cách chúng hoạt động, dưới đây là một số tài nguyên tuyệt vời mà bạn có thể xem theo thứ tự:

https://www.youtube.com/watch?v=mvmuCPvRoWQ

https://www.youtube.com/watch?v=d4EgbgTm0Bg

https://eater.net/quaternions
