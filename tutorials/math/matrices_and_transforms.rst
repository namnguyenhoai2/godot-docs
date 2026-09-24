.. _doc_matrices_and_transforms:

Ma trận và phép biến đổi
========================

Giới thiệu
----------

Trước khi đọc tutorial này, chúng tôi khuyến nghị bạn đọc kỹ và hiểu rõ tutorial :ref:`doc_vector_math`, vì tutorial này yêu cầu kiến thức về vector.

Tutorial này nói về *các phép biến đổi* và cách biểu diễn chúng trong Godot bằng ma trận. Đây không phải là hướng dẫn chuyên sâu đầy đủ về ma trận. Các phép biến đổi thường được áp dụng dưới dạng tịnh tiến, xoay và scale, vì vậy chúng ta sẽ tập trung vào cách biểu diễn những phép biến đổi đó bằng ma trận.

Phần lớn hướng dẫn này tập trung vào 2D, sử dụng :ref:`class_Transform2D` và
:ref:`class_Vector2`, nhưng cách mọi thứ hoạt động trong 3D cũng rất tương tự.

.. note:: Như đã đề cập trong tutorial trước, điều quan trọng cần nhớ là trong Godot, trục Y hướng *xuống* trong 2D. Điều này ngược với cách hầu hết các trường học dạy đại số tuyến tính, trong đó trục Y hướng lên.

.. note:: Quy ước là trục X có màu đỏ, trục Y có màu xanh lá và trục Z có màu xanh dương. Tutorial này được tô màu theo các quy ước đó, nhưng chúng ta cũng sẽ biểu diễn vector gốc bằng màu xanh dương.

Các thành phần của ma trận và ma trận Identity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ma trận Identity biểu diễn một phép biến đổi không có tịnh tiến, không có xoay và không có scale. Hãy bắt đầu bằng cách xem ma trận Identity và mối quan hệ giữa các thành phần của nó với hình dạng trực quan của ma trận.

.. image:: img/matrices_and_transforms/identity.png

Ma trận có các hàng và cột, đồng thời ma trận biến đổi có những quy ước cụ thể về chức năng của từng thành phần.

Trong hình trên, chúng ta có thể thấy vector X màu đỏ được biểu diễn bởi cột đầu tiên của ma trận, còn vector Y màu xanh lá tương tự được biểu diễn bởi cột thứ hai. Thay đổi các cột sẽ làm thay đổi những vector này. Chúng ta sẽ xem cách thao tác với chúng trong một vài ví dụ tiếp theo.

Bạn không cần lo lắng về việc thao tác trực tiếp với các hàng, vì chúng ta thường làm việc với các cột. Tuy nhiên, bạn có thể hình dung các hàng của ma trận cho biết những vector nào góp phần di chuyển theo một hướng nhất định.

Khi đề cập đến một giá trị như ``t.x.y``, đó là thành phần Y của vector cột X. Nói cách khác, đó là vị trí dưới cùng bên trái của ma trận. Tương tự, ``t.x.x`` là trên cùng bên trái, ``t.y.x`` là trên cùng bên phải và ``t.y.y`` là dưới cùng bên phải, trong đó ``t`` là Transform2D.

Scale ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~

Áp dụng scale là một trong những thao tác dễ hiểu nhất. Hãy bắt đầu bằng cách đặt logo Godot bên dưới các vector để có thể nhìn thấy trực quan các hiệu ứng trên một đối tượng:

.. image:: img/matrices_and_transforms/identity-godot.png

Để scale ma trận, tất cả những gì chúng ta cần làm là nhân từng thành phần với giá trị scale mong muốn. Hãy scale nó lên 2 lần. 1 nhân 2 bằng 2, còn 0 nhân 2 bằng 0, vì vậy chúng ta có kết quả sau:

.. image:: img/matrices_and_transforms/scale.png

Để thực hiện việc này trong code, chúng ta nhân từng vector:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = Transform2D()
    # Scale
    t.x *= 2
    t.y *= 2
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính.

 .. code-tab:: csharp

    Transform2D t = Transform2D.Identity;
    // Scale
    t.X *= 2;
    t.Y *= 2;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính.

Nếu muốn đưa nó về scale ban đầu, chúng ta có thể nhân từng thành phần với 0.5. Về cơ bản, đó là tất cả những gì cần biết về việc scale một ma trận biến đổi.

Để tính scale của đối tượng từ một ma trận biến đổi hiện có, bạn có thể sử dụng ``length()`` trên từng vector cột.

.. note:: Trong các dự án thực tế, bạn có thể sử dụng phương thức ``scaled()`` để thực hiện scale.

Xoay ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~

Chúng ta sẽ bắt đầu giống như phần trước, với logo Godot bên dưới ma trận Identity:

.. image:: img/matrices_and_transforms/identity-godot.png

Ví dụ, giả sử chúng ta muốn xoay logo Godot 90 độ theo chiều kim đồng hồ. Hiện tại, trục X hướng sang phải và trục Y hướng xuống. Nếu xoay chúng trong đầu, chúng ta sẽ thấy một cách logic rằng trục X mới phải hướng xuống còn trục Y mới phải hướng sang trái.

Bạn có thể hình dung mình nắm cả logo Godot và các vector của nó, sau đó xoay chúng quanh tâm. Vị trí cuối cùng sau khi xoay sẽ xác định hướng của các vector, từ đó xác định ma trận.

Chúng ta cần biểu diễn "xuống" và "trái" trong hệ tọa độ thông thường, vì vậy chúng ta sẽ đặt X thành (0, 1) và Y thành (-1, 0). Đây cũng là các giá trị của ``Vector2.DOWN`` và ``Vector2.LEFT``. Khi làm vậy, chúng ta nhận được kết quả mong muốn là xoay đối tượng:

.. image:: img/matrices_and_transforms/rotate1.png

Nếu gặp khó khăn khi hiểu phần trên, hãy thử bài tập này: Cắt một hình vuông bằng giấy, vẽ các vector X và Y lên đó, đặt nó lên giấy kẻ ô, sau đó xoay nó và ghi lại các điểm cuối.

Để thực hiện phép xoay trong code, chúng ta cần có khả năng tính toán các giá trị bằng chương trình. Hình này cho thấy các công thức cần thiết để tính ma trận biến đổi từ một góc xoay. Đừng lo nếu phần này có vẻ phức tạp, tôi hứa đây là phần khó nhất mà bạn cần biết.

.. image:: img/matrices_and_transforms/rotate2.png

.. note::

   Godot biểu diễn mọi phép xoay bằng radian, không phải độ. Một vòng xoay đầy đủ là ``TAU`` hoặc ``PI*2`` radian, còn một phần tư vòng xoay 90 độ là ``TAU/4`` hoặc ``PI/2`` radian. Sử dụng ``TAU`` thường giúp code dễ đọc hơn.

.. note:: Thông tin thú vị: Ngoài việc trục Y hướng *xuống* trong Godot, phép xoay cũng được biểu diễn theo chiều kim đồng hồ. Điều này có nghĩa là tất cả các hàm toán học và lượng giác hoạt động giống như trong hệ thống Y hướng lên và CCW, vì những khác biệt này "triệt tiêu" lẫn nhau. Bạn có thể hình dung phép xoay trong cả hai hệ thống là "từ X đến Y".

Để thực hiện phép xoay 0.5 radian (khoảng 28.65 độ), chúng ta đưa giá trị 0.5 vào công thức trên và tính toán để tìm ra các giá trị thực tế cần có:

.. image:: img/matrices_and_transforms/rotate3.png

Sau đây là cách thực hiện việc đó trong code (gắn script vào một Node2D):

.. tabs::
 .. code-tab:: gdscript GDScript

    var rot = 0.5 # Phép xoay cần áp dụng.
    var t = Transform2D()
    t.x.x = cos(rot)
    t.y.y = cos(rot)
    t.x.y = sin(rot)
    t.y.x = -sin(rot)
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính.

 .. code-tab:: csharp

    float rot = 0.5f; // Phép xoay cần áp dụng.
    Transform2D t = Transform2D.Identity;
    t.X.X = t.Y.Y = Mathf.Cos(rot);
    t.X.Y = t.Y.X = Mathf.Sin(rot);
    t.Y.X *= -1;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính.

Để tính phép xoay của đối tượng từ một ma trận biến đổi hiện có, bạn có thể sử dụng ``atan2(t.x.y, t.x.x)``, trong đó t là Transform2D.

.. note:: Trong các dự án thực tế, bạn có thể sử dụng phương thức ``rotated()`` để thực hiện phép xoay.

Cơ sở của ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~

Cho đến nay, chúng ta mới chỉ làm việc với các ``x`` và ``y``, các vector chịu trách nhiệm biểu diễn phép xoay, co giãn và/hoặc shear (nâng cao, được đề cập ở cuối). Hai vector X và Y hợp lại được gọi là *cơ sở* của ma trận biến đổi. Các thuật ngữ "cơ sở" và "vector cơ sở" rất quan trọng cần biết.

Bạn có thể đã nhận thấy rằng :ref:`class_Transform2D` thực tế có ba giá trị :ref:`class_Vector2`: ``x``, ``y`` và ``origin``. Giá trị ``origin`` không thuộc cơ sở, nhưng là một phần của transform và cần thiết để biểu diễn vị trí. Từ giờ, chúng ta sẽ theo dõi vector gốc trong tất cả các ví dụ. Bạn có thể xem ``origin`` như một cột khác, nhưng thường sẽ tốt hơn nếu xem nó hoàn toàn tách biệt.

Lưu ý rằng trong 3D, Godot có một cấu trúc :ref:`class_Basis` riêng để chứa ba giá trị :ref:`class_Vector3` của cơ sở, vì code có thể trở nên phức tạp và việc tách nó khỏi :ref:`class_Transform3D` (được tạo thành từ một
:ref:`class_Basis` và một :ref:`class_Vector3` bổ sung cho gốc) là hợp lý.

Dịch chuyển ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Thay đổi vector gốc được gọi là *dịch chuyển* ma trận biến đổi. Dịch chuyển về cơ bản là một thuật ngữ kỹ thuật cho việc "di chuyển" đối tượng, nhưng rõ ràng không bao gồm bất kỳ phép xoay nào.

Hãy cùng xem qua một ví dụ để hiểu rõ hơn. Chúng ta sẽ bắt đầu với identity transform như lần trước, nhưng lần này sẽ theo dõi vector gốc.

.. image:: img/matrices_and_transforms/identity-origin.png

Nếu muốn di chuyển đối tượng đến vị trí (1, 2), chúng ta cần đặt vector gốc của nó thành (1, 2):

.. image:: img/matrices_and_transforms/translate.png

Ngoài ra còn có một phương thức ``translated_local()``, thực hiện thao tác khác với việc thêm hoặc thay đổi trực tiếp ``origin``. Phương thức ``translated_local()`` sẽ dịch chuyển đối tượng *tương đối theo phép xoay của chính nó*. Ví dụ, một đối tượng được xoay 90 độ theo chiều kim đồng hồ sẽ di chuyển sang phải khi gọi ``translated_local()`` với ``Vector2.UP``. Để dịch chuyển *tương đối theo frame toàn cục/cha*, hãy sử dụng ``translated()`` thay thế.

.. note:: 2D của Godot sử dụng tọa độ dựa trên pixel, vì vậy trong các project thực tế, bạn sẽ muốn dịch chuyển hàng trăm đơn vị.

Kết hợp mọi thứ
~~~~~~~~~~~~~~~

Chúng ta sẽ áp dụng mọi thứ đã đề cập cho đến nay vào một transform. Để làm theo, hãy tạo một project với node Sprite2D và sử dụng logo Godot làm texture resource.

Hãy đặt phép dịch chuyển thành (350, 150), xoay -0.5 rad và co giãn lên 3 lần. Tôi đã đăng ảnh chụp màn hình cùng code để tạo lại ảnh đó, nhưng khuyến khích bạn thử tự tạo lại ảnh chụp màn hình mà không xem code!

.. image:: img/matrices_and_transforms/putting-all-together.png

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = Transform2D()
    # Dịch chuyển
    t.origin = Vector2(350, 150)
    # Phép xoay
    var rot = -0.5 # Phép xoay cần áp dụng.
    t.x.x = cos(rot)
    t.y.y = cos(rot)
    t.x.y = sin(rot)
    t.y.x = -sin(rot)
    # Co giãn
    t.x *= 3
    t.y *= 3
    transform = t # Thay đổi transform của node thành giá trị chúng ta đã tính.

 .. code-tab:: csharp

    Transform2D t = Transform2D.Identity;
    // Dịch chuyển
    t.Origin = new Vector2(350, 150);
    // Phép xoay
    float rot = -0.5f; // Phép xoay cần áp dụng.
    t.X.X = t.Y.Y = Mathf.Cos(rot);
    t.X.Y = t.Y.X = Mathf.Sin(rot);
    t.Y.X *= -1;
    // Co giãn
    t.X *= 3;
    t.Y *= 3;
    Transform = t; // Thay đổi transform của node thành giá trị chúng ta đã tính.

Shear ma trận biến đổi (nâng cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Nếu bạn chỉ muốn tìm hiểu cách *sử dụng* các ma trận biến đổi, bạn có thể bỏ qua phần này của tutorial. Phần này tìm hiểu một khía cạnh ít được sử dụng của ma trận biến đổi nhằm xây dựng hiểu biết về chúng.

          Node2D cung cấp sẵn thuộc tính shear.

Bạn có thể đã nhận thấy rằng một transform có nhiều bậc tự do hơn tổ hợp các thao tác trên. Cơ sở của ma trận biến đổi 2D có tổng cộng bốn số trong hai giá trị :ref:`class_Vector2`, trong khi một giá trị xoay và một Vector2 cho scale chỉ có 3 số. Khái niệm cấp cao về bậc tự do còn thiếu này được gọi là *shear*.

Thông thường, các vector cơ sở luôn vuông góc với nhau. Tuy nhiên, shear có thể hữu ích trong một số tình huống, và việc hiểu shear giúp bạn hiểu cách các transform hoạt động.

Để cho bạn thấy trực quan kết quả sẽ trông như thế nào, hãy phủ một lưới lên logo Godot:

.. image:: img/matrices_and_transforms/identity-grid.png

Mỗi điểm trên lưới này được tạo ra bằng cách cộng các vector cơ sở với nhau. Góc dưới bên phải là X + Y, còn góc trên bên phải là X - Y. Nếu thay đổi các vector cơ sở, toàn bộ lưới sẽ di chuyển theo, vì lưới được tạo thành từ các vector cơ sở. Tất cả các đường trên lưới hiện đang song song sẽ vẫn song song bất kể chúng ta thay đổi các vector cơ sở như thế nào.

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

.. note:: Bạn không thể đặt các giá trị thô của Transform2D trong editor, vì vậy bạn *phải* sử dụng code nếu muốn shear đối tượng.

Do các vector không còn vuông góc với nhau, đối tượng đã bị shear. Điểm giữa phía dưới của lưới, vốn là (0, 1) tính tương đối so với chính nó, giờ nằm tại vị trí thế giới (1, 1).

Các tọa độ bên trong đối tượng được gọi là tọa độ UV trong texture, vì vậy hãy mượn thuật ngữ đó để dùng ở đây. Để tìm vị trí thế giới từ một vị trí tương đối, công thức là U * X + V * Y, trong đó U và V là các số, còn X và Y là các vector cơ sở.

Góc dưới bên phải của lưới, luôn có vị trí UV là (1, 1), nằm tại vị trí thế giới (2, 1), được tính từ X*1 + Y*1, tức (1, 0) + (1, 1), hay (1 + 1, 0 + 1), hay (2, 1). Điều này khớp với quan sát của chúng ta về vị trí góc dưới bên phải của hình ảnh.

Tương tự, góc trên bên phải của lưới, luôn ở vị trí UV là (1, -1), nằm ở vị trí trong world là (0, -1), được tính từ X*1 + Y*-1, tức là (1, 0) - (1, 1), hay (1 - 1, 0 - 1), hoặc (0, -1). Điều này khớp với quan sát của chúng ta về vị trí góc trên bên phải của hình ảnh.

Hy vọng giờ đây bạn đã hoàn toàn hiểu cách một transformation matrix tác động đến object, cũng như mối quan hệ giữa các basis vector và cách "UV" hay "intra-coordinates" của object thay đổi vị trí trong world.

.. note:: Trong Godot, mọi phép tính transform đều được thực hiện tương đối với parent node. Khi chúng ta nói đến "world position", nếu node có parent thì vị trí đó sẽ là tương đối với parent của node.

Nếu muốn có thêm lời giải thích, bạn nên xem video xuất sắc của 3Blue1Brown về linear transformations: https://www.youtube.com/watch?v=kYB8IZa5AuE

Ứng dụng thực tế của transform
------------------------------

Trong các project thực tế, bạn thường sẽ làm việc với các transform nằm trong những transform khác bằng cách cho nhiều node :ref:`class_Node2D` hoặc :ref:`class_Node3D` làm parent của nhau.

Tuy nhiên, việc hiểu cách tính thủ công các giá trị cần thiết vẫn rất hữu ích. Chúng ta sẽ xem qua cách bạn có thể sử dụng :ref:`class_Transform2D` hoặc
:ref:`class_Transform3D` để tính thủ công các transform của node.

Chuyển đổi vị trí giữa các transform
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có nhiều trường hợp bạn muốn chuyển đổi một vị trí vào hoặc ra khỏi một transform. Ví dụ, nếu bạn có một vị trí tương đối với player và muốn tìm vị trí trong world (tương đối với parent), hoặc nếu bạn có một vị trí trong world và muốn biết nó nằm ở đâu tương đối với player.

Chúng ta có thể xác định một vector tương đối với player sẽ được biểu diễn như thế nào trong world space bằng toán tử ``*``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Vector trong world space nằm dưới player 100 đơn vị.
    print(transform * Vector2(0, 100))

 .. code-tab:: csharp

    // Vector trong world space nằm dưới player 100 đơn vị.
    GD.Print(Transform * new Vector2(0, 100));

Và chúng ta có thể sử dụng toán tử ``*`` theo thứ tự ngược lại để xác định một vị trí trong world space sẽ là gì nếu nó được định nghĩa tương đối với player:

.. tabs::
 .. code-tab:: gdscript GDScript

    # (0, 100) nằm ở đâu tương đối với player?
    print(Vector2(0, 100) * transform)

 .. code-tab:: csharp

    // (0, 100) nằm ở đâu tương đối với player?
    GD.Print(new Vector2(0, 100) * Transform);

.. note:: Nếu biết trước rằng transform được đặt tại (0, 0), bạn có thể sử dụng các method "basis_xform" hoặc "basis_xform_inv" thay thế; các method này bỏ qua việc xử lý translation.

Di chuyển một object tương đối với chính nó
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một thao tác phổ biến, đặc biệt trong game 3D, là di chuyển một object tương đối với chính nó. Ví dụ, trong các game bắn súng góc nhìn thứ nhất, bạn muốn character di chuyển về phía trước (trục -Z) khi nhấn :kbd:`W`.

Vì các basis vector là hướng tương đối với parent, còn origin vector là vị trí tương đối với parent, chúng ta có thể cộng các bội số của basis vector để di chuyển một object tương đối với chính nó.

Đoạn code này di chuyển một object 100 đơn vị sang bên phải của chính nó:

.. tabs::
 .. code-tab:: gdscript GDScript

    transform.origin += transform.x * 100

 .. code-tab:: csharp

    Transform2D t = Transform;
    t.Origin += t.X * 100;
    Transform = t;

Để di chuyển trong 3D, bạn cần thay "x" bằng "basis.x".

.. note:: Trong các project thực tế, bạn có thể sử dụng ``translate_object_local`` trong 3D hoặc ``move_local_x`` và ``move_local_y`` trong 2D để thực hiện việc này.

Áp dụng các transform lên nhau
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một trong những điều quan trọng nhất cần biết về transform là cách sử dụng nhiều transform cùng nhau. Transform của parent node tác động đến tất cả child node của nó. Hãy cùng phân tích một ví dụ.

Trong hình ảnh này, child node có số "2" sau tên các component để phân biệt chúng với parent node. Có thể trông hơi choáng ngợp vì có quá nhiều con số, nhưng hãy nhớ rằng mỗi con số được hiển thị hai lần (bên cạnh các mũi tên và trong các matrix), và gần một nửa số đó là số 0.

.. image:: img/matrices_and_transforms/apply.png

Các transformation duy nhất diễn ra ở đây là parent node được đặt scale là (2, 1), child được đặt scale là (0.5, 0.5), và cả hai node đều được đặt position.

Mọi transformation của child đều bị ảnh hưởng bởi transformation của parent. Child có scale là (0.5, 0.5), vì vậy bạn sẽ mong đợi nó là một hình vuông có tỷ lệ 1:1, và đúng là như vậy, nhưng chỉ tương đối với parent. Vector X của child cuối cùng là (1, 0) trong world space, vì nó được scale theo các basis vector của parent. Tương tự, vector ``origin`` của child node được đặt là (1, 1), nhưng thực tế nó di chuyển (2, 1) trong world space do các basis vector của parent node.

Để tính thủ công transform trong world space của child transform, chúng ta sẽ sử dụng đoạn code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thiết lập các transform như trong hình, nhưng tăng các position lên 100 lần.
    var parent = Transform2D(Vector2(2, 0), Vector2(0, 1), Vector2(100, 200))
    var child = Transform2D(Vector2(0.5, 0), Vector2(0, 0.5), Vector2(100, 100))

    # Tính transform trong world space của child
    # origin = (2, 0) * 100 + (0, 1) * 100 + (100, 200)
    var origin = parent.x * child.origin.x + parent.y * child.origin.y + parent.origin
    # basis_x = (2, 0) * 0.5 + (0, 1) * 0
    var basis_x = parent.x * child.x.x + parent.y * child.x.y
    # basis_y = (2, 0) * 0 + (0, 1) * 0.5
    var basis_y = parent.x * child.y.x + parent.y * child.y.y

    # Thay đổi transform của node thành giá trị chúng ta đã tính.
    transform = Transform2D(basis_x, basis_y, origin)

 .. code-tab:: csharp

    // Thiết lập các transform như trong hình, nhưng tăng các position lên 100 lần.
    Transform2D parent = new Transform2D(2, 0, 0, 1, 100, 200);
    Transform2D child = new Transform2D(0.5f, 0, 0, 0.5f, 100, 100);

    // Tính transform trong world space của child
    // origin = (2, 0) * 100 + (0, 1) * 100 + (100, 200)
    Vector2 origin = parent.X * child.Origin.X + parent.Y * child.Origin.Y + parent.Origin;
    // basisX = (2, 0) * 0.5 + (0, 1) * 0 = (0.5, 0)
    Vector2 basisX = parent.X * child.X.X + parent.Y * child.X.Y;
    // basisY = (2, 0) * 0 + (0, 1) * 0.5 = (0.5, 0)
    Vector2 basisY = parent.X * child.Y.X + parent.Y * child.Y.Y;

    // Thay đổi transform của node thành giá trị chúng ta đã tính.
    Transform = new Transform2D(basisX, basisY, origin);

Trong các project thực tế, chúng ta có thể tìm transform trong world của child bằng cách áp dụng transform này lên transform khác thông qua toán tử ``*``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Thiết lập các transform như trong hình, nhưng tăng các position lên 100 lần.
    var parent = Transform2D(Vector2(2, 0), Vector2(0, 1), Vector2(100, 200))
    var child = Transform2D(Vector2(0.5, 0), Vector2(0, 0.5), Vector2(100, 100))

    # Thay đổi phép biến đổi của node thành phép biến đổi trong world của node con.
    transform = parent * child

 .. code-tab:: csharp

    // Thiết lập các transform như trong hình, nhưng tăng các position lên 100 lần.
    Transform2D parent = new Transform2D(2, 0, 0, 1, 100, 200);
    Transform2D child = new Transform2D(0.5f, 0, 0, 0.5f, 100, 100);

    // Thay đổi phép biến đổi của node thành phép biến đổi trong world của node con.
    Transform = parent * child;

.. note:: Khi nhân các ma trận, thứ tự rất quan trọng! Đừng nhầm lẫn chúng.

Cuối cùng, áp dụng phép biến đổi đơn vị sẽ luôn không làm gì cả.

Nếu muốn có thêm lời giải thích, bạn nên xem video xuất sắc của 3Blue1Brown về phép hợp thành ma trận: https://www.youtube.com/watch?v=XkY2DOUCWMU

Đảo ma trận biến đổi
~~~~~~~~~~~~~~~~~~~~

Hàm ``affine_inverse`` trả về một phép biến đổi có tác dụng "hoàn tác" phép biến đổi trước đó. Điều này có thể hữu ích trong một số tình huống. Hãy cùng xem một vài ví dụ.

Nhân phép biến đổi nghịch đảo với phép biến đổi thông thường sẽ hoàn tác mọi phép biến đổi:

.. tabs::
 .. code-tab:: gdscript GDScript

    var ti = transform.affine_inverse()
    var t = ti * transform
    # Phép biến đổi là phép biến đổi đơn vị.

 .. code-tab:: csharp

    Transform2D ti = Transform.AffineInverse();
    Transform2D t = ti * Transform;
    // Phép biến đổi là phép biến đổi đơn vị.

Biến đổi một vị trí bằng một phép biến đổi và phép biến đổi nghịch đảo của nó sẽ cho ra cùng vị trí đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    var ti = transform.affine_inverse()
    position = transform * position
    position = ti * position
    # Vị trí này giống như trước.

 .. code-tab:: csharp

    Transform2D ti = Transform.AffineInverse();
    Position = Transform * Position;
    Position = ti * Position;
    // Vị trí này giống như trước.

Tất cả hoạt động như thế nào trong 3D?
--------------------------------------

Một trong những điều tuyệt vời về các ma trận biến đổi là chúng hoạt động rất tương tự nhau giữa các phép biến đổi 2D và 3D. Tất cả code và công thức được sử dụng ở trên cho 2D đều hoạt động tương tự trong 3D, với 3 ngoại lệ: bổ sung trục thứ ba, mỗi trục có kiểu :ref:`class_Vector3`, và Godot lưu trữ riêng :ref:`class_Basis` với :ref:`class_Transform3D`, vì phép toán có thể trở nên phức tạp và việc tách chúng ra là hợp lý.

Tất cả các khái niệm về cách translation, rotation, scale và shearing hoạt động trong 3D đều giống như trong 2D. Để scale, ta lấy từng component và nhân chúng; để rotate, ta thay đổi hướng của từng vector cơ sở; để translate, ta điều chỉnh gốc tọa độ; và để shear, ta thay đổi các vector cơ sở để chúng không vuông góc.

.. image:: img/matrices_and_transforms/3d-identity.png

Nếu muốn, bạn nên thử thao tác với các phép biến đổi để hiểu cách chúng hoạt động. Godot cho phép bạn chỉnh sửa trực tiếp các ma trận biến đổi 3D từ inspector. Bạn có thể tải project này, trong đó có các đường thẳng và khối lập phương có màu để giúp trực quan hóa các
:ref:`class_Basis` vector và gốc tọa độ trong cả 2D lẫn 3D: https://github.com/godotengine/godot-demo-projects/tree/master/misc/matrix_transform

.. UPDATE: May change in future. When you can edit a Node2D's transform matrix
.. directly, remove or update this note.

.. note:: Bạn không thể chỉnh sửa trực tiếp ma trận biến đổi của Node2D trong inspector của Godot 4.0. Điều này có thể được thay đổi trong một bản phát hành Godot trong tương lai.

Nếu muốn có thêm lời giải thích, bạn nên xem video xuất sắc của 3Blue1Brown về các phép biến đổi tuyến tính 3D: https://www.youtube.com/watch?v=rHLEWRxRGiM

Biểu diễn rotation trong 3D (nâng cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Điểm khác biệt lớn nhất giữa các ma trận biến đổi 2D và 3D là cách biểu diễn riêng rotation mà không cần các vector cơ sở.

Với 2D, chúng ta có một cách đơn giản (atan2) để chuyển đổi giữa một ma trận biến đổi và một góc. Trong 3D, rotation quá phức tạp để biểu diễn bằng một con số. Có một khái niệm gọi là các góc Euler, có thể biểu diễn rotation dưới dạng một tập hợp gồm 3 số; tuy nhiên, chúng bị giới hạn và không hữu ích lắm, ngoại trừ các trường hợp đơn giản.

Trong 3D, chúng ta thường không sử dụng các góc; thay vào đó, chúng ta dùng basis của phép biến đổi (được sử dụng gần như ở mọi nơi trong Godot), hoặc dùng quaternion. Godot có thể biểu diễn quaternion bằng struct :ref:`class_Quaternion`. Tôi khuyên bạn nên hoàn toàn bỏ qua cách chúng hoạt động bên trong, vì chúng rất phức tạp và không trực quan.

Tuy nhiên, nếu bạn thực sự muốn biết cách chúng hoạt động, dưới đây là một số tài nguyên tuyệt vời mà bạn có thể xem theo thứ tự:

https://www.youtube.com/watch?v=mvmuCPvRoWQ

https://www.youtube.com/watch?v=d4EgbgTm0Bg

https://eater.net/quaternions
