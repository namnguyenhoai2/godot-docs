.. _doc_custom_drawing_in_2d:

Vẽ tùy chỉnh trong 2D
=====================

Giới thiệu
----------

Godot có các node để vẽ sprite, polygon, hạt, văn bản và nhiều nhu cầu phát triển game phổ biến khác. Tuy nhiên, nếu bạn cần một thứ cụ thể không được các node tiêu chuẩn hỗ trợ, bạn có thể khiến bất kỳ node 2D nào (ví dụ như
:ref:`Control <class_Control>` hoặc dựa trên :ref:`Node2D <class_Node2D>`) vẽ lên màn hình bằng các lệnh tùy chỉnh.

Vẽ tùy chỉnh trong node 2D *thực sự* hữu ích. Sau đây là một số trường hợp sử dụng:

-  Vẽ các hình dạng hoặc logic mà những node hiện có không thể thực hiện, chẳng hạn như một hình ảnh có vệt kéo dài hoặc một polygon chuyển động đặc biệt.
-  Vẽ một số lượng lớn đối tượng đơn giản, chẳng hạn như lưới hoặc bàn cờ cho game 2D. Vẽ tùy chỉnh tránh chi phí sử dụng một số lượng lớn node, có thể giảm mức sử dụng bộ nhớ và cải thiện hiệu năng.
-  Tạo một UI control tùy chỉnh. Có rất nhiều control sẵn có, nhưng khi bạn có nhu cầu khác thường, có thể bạn sẽ cần một control tùy chỉnh.

Vẽ
--

Thêm một script vào bất kỳ node dẫn xuất từ :ref:`CanvasItem <class_CanvasItem>` nào, chẳng hạn như :ref:`Control <class_Control>` hoặc
:ref:`Node2D <class_Node2D>`. Sau đó override
hàm :ref:`_draw()<class_CanvasItem_private_method__draw>`.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    func _draw():
        pass  # Các lệnh vẽ của bạn đặt ở đây.

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        public override void _Draw()
        {
            // Các lệnh vẽ của bạn đặt ở đây.
        }
    }

Các lệnh vẽ được mô tả trong tài liệu tham chiếu lớp :ref:`CanvasItem <class_CanvasItem>`. Có rất nhiều lệnh và chúng ta sẽ xem một số lệnh trong các ví dụ bên dưới.

Cập nhật
--------

Hàm :ref:`_draw <class_CanvasItem_private_method__draw>` chỉ được gọi một lần, sau đó các lệnh vẽ được lưu vào bộ nhớ đệm và ghi nhớ, vì vậy không cần gọi thêm.

Nếu cần vẽ lại vì một biến hoặc thứ gì khác đã thay đổi, hãy gọi :ref:`CanvasItem.queue_redraw <class_CanvasItem_method_queue_redraw>` trong chính node đó và một lần gọi ``_draw()`` mới sẽ được thực hiện.

Sau đây là một ví dụ phức tạp hơn một chút, trong đó chúng ta có một biến texture có thể được sửa đổi bất kỳ lúc nào, và bằng cách sử dụng
:ref:`setter <doc_gdscript_basics_setters_getters>`, texture sẽ được vẽ lại khi bị thay đổi:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    @export var texture : Texture2D:
        set(value):
            texture = value
            queue_redraw()

    func _draw():
        draw_texture(texture, Vector2())

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private Texture2D _texture;

        [Export]
        public Texture2D Texture
        {
            get
            {
                return _texture;
            }

            set
            {
                _texture = value;
                QueueRedraw();
            }
        }

        public override void _Draw()
        {
            DrawTexture(_texture, new Vector2());
        }
    }

Để xem hoạt động thực tế, bạn có thể đặt texture thành biểu tượng Godot trong editor bằng cách kéo và thả ``icon.svg`` mặc định từ tab ``FileSystem`` vào thuộc tính Texture trong tab ``Inspector``. Khi thay đổi giá trị thuộc tính ``Texture`` trong lúc script trước đó đang chạy, texture cũng sẽ tự động thay đổi.

Trong một số trường hợp, chúng ta có thể cần vẽ lại ở mỗi frame. Để làm vậy, hãy gọi :ref:`queue_redraw <class_CanvasItem_method_queue_redraw>` từ phương thức :ref:`_process <class_Node_private_method__process>`, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    func _draw():
        pass  # Các lệnh vẽ của bạn đặt ở đây.

    func _process(_delta):
        queue_redraw()

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        public override void _Draw()
        {
            // Các lệnh vẽ của bạn đặt ở đây.
        }

        public override void _Process(double delta)
        {
            QueueRedraw();
        }
    }

Căn chỉnh tọa độ và độ rộng đường
---------------------------------

Drawing API sử dụng hệ tọa độ của CanvasItem, không nhất thiết là tọa độ pixel. Điều này có nghĩa là ``_draw()`` sử dụng không gian tọa độ được tạo sau khi áp dụng phép biến đổi của CanvasItem. Ngoài ra, bạn có thể áp dụng một phép biến đổi tùy chỉnh lên trên nó bằng cách sử dụng
:ref:`draw_set_transform<class_CanvasItem_method_draw_set_transform>` hoặc
:ref:`draw_set_transform_matrix<class_CanvasItem_method_draw_set_transform_matrix>`.

Khi sử dụng :ref:`draw_line <class_CanvasItem_method_draw_line>`, bạn nên cân nhắc độ rộng của đường. Khi sử dụng độ rộng là số lẻ, vị trí của các điểm đầu và cuối nên được dịch chuyển ``0.5`` để giữ cho đường nằm ở giữa, như minh họa bên dưới.

.. image:: img/draw_line.png

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        draw_line(Vector2(1.5, 1.0), Vector2(1.5, 4.0), Color.GREEN, 1.0)
        draw_line(Vector2(4.0, 1.0), Vector2(4.0, 4.0), Color.GREEN, 2.0)
        draw_line(Vector2(7.5, 1.0), Vector2(7.5, 4.0), Color.GREEN, 3.0)

 .. code-tab:: csharp

    public override void _Draw()
    {
        DrawLine(new Vector2(1.5f, 1.0f), new Vector2(1.5f, 4.0f), Colors.Green, 1.0f);
        DrawLine(new Vector2(4.0f, 1.0f), new Vector2(4.0f, 4.0f), Colors.Green, 2.0f);
        DrawLine(new Vector2(7.5f, 1.0f), new Vector2(7.5f, 4.0f), Colors.Green, 3.0f);
    }

Điều tương tự cũng áp dụng cho phương thức :ref:`draw_rect <class_CanvasItem_method_draw_rect>` với ``filled = false``.

.. image:: img/draw_rect.png

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        draw_rect(Rect2(1.0, 1.0, 3.0, 3.0), Color.GREEN)
        draw_rect(Rect2(5.5, 1.5, 2.0, 2.0), Color.GREEN, false, 1.0)
        draw_rect(Rect2(9.0, 1.0, 5.0, 5.0), Color.GREEN)
        draw_rect(Rect2(16.0, 2.0, 3.0, 3.0), Color.GREEN, false, 2.0)

 .. code-tab:: csharp

    public override void _Draw()
    {
        DrawRect(new Rect2(1.0f, 1.0f, 3.0f, 3.0f), Colors.Green);
        DrawRect(new Rect2(5.5f, 1.5f, 2.0f, 2.0f), Colors.Green, false, 1.0f);
        DrawRect(new Rect2(9.0f, 1.0f, 5.0f, 5.0f), Colors.Green);
        DrawRect(new Rect2(16.0f, 2.0f, 3.0f, 3.0f), Colors.Green, false, 2.0f);
    }

Vẽ khử răng cưa
---------------

Godot cung cấp các tham số phương thức trong :ref:`draw_line<class_CanvasItem_method_draw_line>` để bật khử răng cưa, nhưng không phải tất cả phương thức vẽ tùy chỉnh đều cung cấp tham số ``antialiased`` này.

Đối với các phương thức vẽ tùy chỉnh không cung cấp tham số ``antialiased``, thay vào đó bạn có thể bật 2D MSAA, tính năng này ảnh hưởng đến việc render trong toàn bộ viewport. Cách này cung cấp khả năng khử răng cưa chất lượng cao, nhưng tốn hiệu năng hơn và chỉ áp dụng cho các phần tử cụ thể. Xem :ref:`doc_2d_antialiasing` để biết thêm thông tin.

Sau đây là so sánh một đường có độ rộng tối thiểu (``width=-1``) được vẽ bằng ``antialiased=false``, ``antialiased=true`` và ``antialiased=false`` khi bật 2D MSAA 2x, 4x và 8x.

.. image:: img/draw_antialiasing_options.webp

Công cụ
-------

Bạn cũng có thể muốn vẽ các node của riêng mình khi chạy chúng trong editor. Việc này có thể được dùng để xem trước hoặc trực quan hóa một tính năng hay hành vi nào đó.

Để làm vậy, bạn có thể sử dụng :ref:`chú thích tool <doc_gdscript_tool_mode>` trên cả GDScript và C#. Xem
:ref:`ví dụ bên dưới <doc_draw_show_drawing_while_editing_example>` và
:ref:`doc_running_code_in_the_editor` để biết thêm thông tin.

.. _doc_draw_custom_example_1:

Ví dụ 1: vẽ một hình dạng tùy chỉnh
-----------------------------------

Bây giờ chúng ta sẽ sử dụng chức năng vẽ tùy chỉnh của Godot Engine để vẽ một thứ mà Godot không cung cấp hàm hỗ trợ. Chúng ta sẽ tái tạo logo Godot nhưng chỉ bằng code, sử dụng các hàm vẽ.

Bạn sẽ phải viết code cho một hàm để thực hiện việc này và tự vẽ nó.

.. note::

    Các hướng dẫn sau sử dụng một tập tọa độ cố định có thể quá nhỏ đối với màn hình độ phân giải cao (lớn hơn 1080p). Nếu đúng như vậy và hình vẽ quá nhỏ, hãy cân nhắc tăng tỷ lệ cửa sổ trong project setting
    :ref:`Display > Window > Stretch > Scale <class_ProjectSettings_property_display/window/stretch/scale>` để điều chỉnh project sang độ phân giải cao hơn (tỷ lệ 2 hoặc 4 thường hoạt động tốt).

Vẽ một hình polygon tùy chỉnh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù có một node chuyên dụng để vẽ polygon tùy chỉnh (
:ref:`Polygon2D <class_Polygon2D>`), trong trường hợp này chúng ta sẽ chỉ sử dụng các hàm vẽ cấp thấp hơn để kết hợp chúng trên cùng một node và có thể tạo ra các hình dạng phức tạp hơn về sau.

Trước tiên, chúng ta sẽ định nghĩa một tập các điểm -hoặc tọa độ X và Y- tạo thành phần nền của hình dạng:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    var coords_head : Array = [
        [ 22.952, 83.271 ],  [ 28.385, 98.623 ],
        [ 53.168, 107.647 ], [ 72.998, 107.647 ],
        [ 99.546, 98.623 ],  [ 105.048, 83.271 ],
        [ 105.029, 55.237 ], [ 110.740, 47.082 ],
        [ 102.364, 36.104 ], [ 94.050, 40.940 ],
        [ 85.189, 34.445 ],  [ 85.963, 24.194 ],
        [ 73.507, 19.930 ],  [ 68.883, 28.936 ],
        [ 59.118, 28.936 ],  [ 54.494, 19.930 ],
        [ 42.039, 24.194 ],  [ 42.814, 34.445 ],
        [ 33.951, 40.940 ],  [ 25.637, 36.104 ],
        [ 17.262, 47.082 ],  [ 22.973, 55.237 ]
    ]

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private float[,] _coordsHead =
        {
            { 22.952f, 83.271f },  { 28.385f, 98.623f },
            { 53.168f, 107.647f }, { 72.998f, 107.647f },
            { 99.546f, 98.623f },  { 105.048f, 83.271f },
            { 105.029f, 55.237f }, { 110.740f, 47.082f },
            { 102.364f, 36.104f }, { 94.050f, 40.940f },
            { 85.189f, 34.445f },  { 85.963f, 24.194f },
            { 73.507f, 19.930f },  { 68.883f, 28.936f },
            { 59.118f, 28.936f },  { 54.494f, 19.930f },
            { 42.039f, 24.194f },  { 42.814f, 34.445f },
            { 33.951f, 40.940f },  { 25.637f, 36.104f },
            { 17.262f, 47.082f },  { 22.973f, 55.237f }
        };
    }

Định dạng này tuy gọn nhưng không phải định dạng mà Godot hiểu để vẽ polygon. Trong một tình huống khác, chúng ta có thể phải tải các tọa độ này từ một file hoặc tính toán vị trí trong khi ứng dụng đang chạy, vì vậy có thể cần thực hiện một số phép biến đổi.

Để chuyển đổi các tọa độ này sang đúng định dạng, chúng ta sẽ tạo một phương thức mới ``float_array_to_Vector2Array()``. Sau đó, chúng ta sẽ override hàm ``_ready()``, hàm này chỉ được Godot gọi một lần -khi bắt đầu thực thi- để nạp các tọa độ đó vào một biến:

.. tabs::
 .. code-tab:: gdscript GDScript

    var head : PackedVector2Array

    func float_array_to_Vector2Array(coords : Array) -> PackedVector2Array:
        # Chuyển đổi mảng số thực thành PackedVector2Array.
        var array : PackedVector2Array = []
        for coord in coords:
            array.append(Vector2(coord[0], coord[1]))
        return array

    func _ready():
        head = float_array_to_Vector2Array(coords_head);

 .. code-tab:: csharp

    private Vector2[] _head;

    private Vector2[] FloatArrayToVector2Array(float[,] coords)
    {
        // Chuyển đổi mảng số thực thành một mảng Vector2.
        int size = coords.GetUpperBound(0);
        Vector2[] array = new Vector2[size + 1];
        for (int i = 0; i <= size; i++)
        {
            array[i] = new Vector2(coords[i, 0], coords[i, 1]);
        }
        return array;
    }

    public override void _Ready()
    {
        _head = FloatArrayToVector2Array(_coordsHead);
    }

Để cuối cùng vẽ hình đầu tiên, chúng ta sẽ sử dụng phương thức
:ref:`draw_polygon <class_CanvasItem_method_draw_polygon>` và truyền các điểm (dưới dạng một mảng tọa độ Vector2) cùng màu của hình, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        # Chúng ta sẽ tô bằng màu này.
        var godot_blue : Color = Color("478cbf")
        # Chúng ta truyền PackedVector2Array để vẽ hình.
        draw_polygon(head, [ godot_blue ])

 .. code-tab:: csharp

    public override void _Draw()
    {
        // Chúng ta sẽ tô bằng màu này.
        Color godotBlue = new Color("478cbf");
        // Chúng ta truyền mảng Vector2 để vẽ hình.
        DrawPolygon(_head, [godotBlue]);
    }

Khi chạy, bạn sẽ thấy hình tương tự như sau:

.. image:: img/draw_godot_logo_polygon.webp

Lưu ý rằng phần dưới của logo trông như bị phân đoạn—đó là vì chúng ta đã sử dụng ít điểm để định nghĩa phần đó. Để mô phỏng một đường cong mượt, chúng ta có thể thêm nhiều điểm hơn vào mảng, hoặc có thể sử dụng một hàm toán học để nội suy đường cong và tạo hình mượt bằng code (xem
:ref:`ví dụ 2 <doc_draw_custom_example_2>`).

Các đa giác sẽ luôn **nối điểm cuối cùng được định nghĩa với điểm đầu tiên** để tạo thành một hình khép kín.

Vẽ các đường nối
~~~~~~~~~~~~~~~~

Việc vẽ một chuỗi các đường nối không khép kín để tạo thành đa giác rất giống với phương thức trước đó. Chúng ta sẽ sử dụng một tập hợp các đường nối để vẽ miệng logo Godot.

Trước tiên, chúng ta sẽ định nghĩa danh sách các tọa độ tạo thành hình miệng, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var coords_mouth = [
        [ 22.817, 81.100 ], [ 38.522, 82.740 ],
        [ 39.001, 90.887 ], [ 54.465, 92.204 ],
        [ 55.641, 84.260 ], [ 72.418, 84.177 ],
        [ 73.629, 92.158 ], [ 88.895, 90.923 ],
        [ 89.556, 82.673 ], [ 105.005, 81.100 ]
    ]

 .. code-tab:: csharp

    private float[,] _coordsMouth =
    {
        { 22.817f, 81.100f }, { 38.522f, 82.740f },
        { 39.001f, 90.887f }, { 54.465f, 92.204f },
        { 55.641f, 84.260f }, { 72.418f, 84.177f },
        { 73.629f, 92.158f }, { 88.895f, 90.923f },
        { 89.556f, 82.673f }, { 105.005f, 81.100f }
    };

Chúng ta sẽ nạp các tọa độ này vào một biến và định nghĩa thêm một biến chứa độ dày đường có thể cấu hình:

.. tabs::
 .. code-tab:: gdscript GDScript

    var mouth : PackedVector2Array
    var _mouth_width : float = 4.4

    func _ready():
        head = float_array_to_Vector2Array(coords_head);
        mouth = float_array_to_Vector2Array(coords_mouth);

 .. code-tab:: csharp

    private Vector2[] _mouth;
    private float _mouthWidth = 4.4f;

    public override void _Ready()
    {
        _head = FloatArrayToVector2Array(_coordsHead);
        _mouth = FloatArrayToVector2Array(_coordsMouth);
    }

Và cuối cùng, chúng ta sẽ sử dụng phương thức
:ref:`draw_polyline <class_CanvasItem_method_draw_polyline>` để thực sự vẽ đường này, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        # Chúng ta sẽ dùng màu trắng để vẽ đường.
        var white : Color = Color.WHITE
        var godot_blue : Color = Color("478cbf")

        draw_polygon(head, [ godot_blue ])

        # Chúng ta vẽ đường màu trắng lên trên hình trước đó.
        draw_polyline(mouth, white, _mouth_width)


 .. code-tab:: csharp

    public override void _Draw()
    {
        // Chúng ta sẽ dùng màu trắng để vẽ đường.
        Color white = Colors.White;
        Color godotBlue = new Color("478cbf");

        DrawPolygon(_head, [godotBlue]);

        // Chúng ta vẽ đường màu trắng lên trên hình trước đó.
        DrawPolyline(_mouth, white, _mouthWidth);
    }

Bạn sẽ nhận được kết quả sau:

.. image:: img/draw_godot_logo_polyline.webp

Không giống như ``draw_polygon()``, polyline chỉ có thể có một màu duy nhất cho tất cả các điểm của nó (đối số thứ hai). Phương thức này có thêm 2 đối số: độ rộng của đường (theo mặc định là nhỏ nhất có thể) và tùy chọn bật hoặc tắt antialiasing (mặc định là tắt).

Thứ tự của các lệnh gọi ``_draw`` rất quan trọng—tương tự như vị trí của các Node trong hệ phân cấp cây, các hình khác nhau sẽ được vẽ từ trên xuống dưới, khiến các hình được vẽ sau che khuất những hình trước đó nếu chúng chồng lên nhau. Trong trường hợp này, chúng ta muốn vẽ miệng lên trên đầu, nên đặt nó sau đó.

Lưu ý rằng chúng ta có thể định nghĩa màu theo nhiều cách khác nhau, bằng mã thập lục phân hoặc tên màu được định nghĩa sẵn. Hãy xem class :ref:`Color <class_Color>` để biết các hằng số và cách định nghĩa Color khác.

Vẽ hình tròn
~~~~~~~~~~~~

Để tạo mắt, chúng ta sẽ thêm 4 lệnh gọi vẽ hình mắt, với các kích thước, màu sắc và vị trí khác nhau.

Để vẽ hình tròn, bạn định vị nó dựa trên tâm bằng phương thức
:ref:`draw_circle <class_CanvasItem_method_draw_circle>`. Tham số đầu tiên là một :ref:`Vector2<class_Vector2>` chứa tọa độ tâm, tham số thứ hai là bán kính và tham số thứ ba là màu:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        var white : Color = Color.WHITE
        var godot_blue : Color = Color("478cbf")
        var grey : Color = Color("414042")

        draw_polygon(head, [ godot_blue ])
        draw_polyline(mouth, white, _mouth_width)

        # Bốn hình tròn cho 2 mắt: 2 màu trắng, 2 màu xám.
        draw_circle(Vector2(42.479, 65.4825), 9.3905, white)
        draw_circle(Vector2(85.524, 65.4825), 9.3905, white)
        draw_circle(Vector2(43.423, 65.92), 6.246, grey)
        draw_circle(Vector2(84.626, 66.008), 6.246, grey)

 .. code-tab:: csharp


    public override void _Draw()
    {
        Color white = Colors.White;
        Color godotBlue = new Color("478cbf");
        Color grey = new Color("414042");

        DrawPolygon(_head, [godotBlue]);
        DrawPolyline(_mouth, white, _mouthWidth);

        // Bốn hình tròn cho 2 mắt: 2 màu trắng, 2 màu xám.
        DrawCircle(new Vector2(42.479f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(85.524f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(43.423f, 65.92f), 6.246f, grey);
        DrawCircle(new Vector2(84.626f, 66.008f), 6.246f, grey);
    }

Khi thực thi, bạn sẽ thấy hình tương tự như sau:

.. image:: img/draw_godot_logo_circle.webp


Đối với các cung một phần, không tô (các phần của một hình tròn nằm giữa những góc tùy ý nhất định), bạn có thể sử dụng phương thức
:ref:`draw_arc <class_CanvasItem_method_draw_arc>`.

Vẽ các đường thẳng
~~~~~~~~~~~~~~~~~~

Để vẽ hình cuối cùng (mũi), chúng ta sẽ sử dụng một đường thẳng để mô phỏng nó.

:ref:`draw_line <class_CanvasItem_method_draw_line>` có thể được sử dụng để vẽ một đoạn đơn bằng cách cung cấp tọa độ điểm đầu và điểm cuối làm các đối số, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        var white : Color = Color.WHITE
        var godot_blue : Color = Color("478cbf")
        var grey : Color = Color("414042")

        draw_polygon(head, [ godot_blue ])
        draw_polyline(mouth, white, _mouth_width)
        draw_circle(Vector2(42.479, 65.4825), 9.3905, white)
        draw_circle(Vector2(85.524, 65.4825), 9.3905, white)
        draw_circle(Vector2(43.423, 65.92), 6.246, grey)
        draw_circle(Vector2(84.626, 66.008), 6.246, grey)

        # Vẽ một đường thẳng đứng màu trắng, ngắn nhưng dày, làm mũi.
        draw_line(Vector2(64.273, 60.564), Vector2(64.273, 74.349), white, 5.8)

 .. code-tab:: csharp

    public override void _Draw()
    {
        Color white = Colors.White;
        Color godotBlue = new Color("478cbf");
        Color grey = new Color("414042");

        DrawPolygon(_head, [godotBlue]);
        DrawPolyline(_mouth, white, _mouthWidth);
        DrawCircle(new Vector2(42.479f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(85.524f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(43.423f, 65.92f), 6.246f, grey);
        DrawCircle(new Vector2(84.626f, 66.008f), 6.246f, grey);

        // Vẽ một đường thẳng đứng màu trắng, ngắn nhưng dày, làm mũi.
        DrawLine(new Vector2(64.273f, 60.564f), new Vector2(64.273f, 74.349f),
                 white, 5.8f);
    }

Bây giờ bạn sẽ thấy hình sau trên màn hình:

.. image:: img/draw_godot_logo_line.webp

Lưu ý rằng nếu cần vẽ nhiều đường không nối nhau cùng lúc, bạn có thể đạt hiệu năng cao hơn bằng cách vẽ tất cả chúng trong một lần gọi, sử dụng phương thức :ref:`draw_multiline <class_CanvasItem_method_draw_multiline>`.

Vẽ văn bản
~~~~~~~~~~

Mặc dù sử dụng Node :ref:`Label <class_Label>` là cách phổ biến nhất để thêm văn bản vào ứng dụng, hàm `_draw` cấp thấp cung cấp chức năng thêm văn bản vào phần vẽ tùy chỉnh của Node. Chúng ta sẽ sử dụng nó để thêm tên "GODOT" bên dưới đầu robot.

Chúng ta sẽ sử dụng phương thức :ref:`draw_string <class_CanvasItem_method_draw_string>` để thực hiện việc này, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var default_font : Font = ThemeDB.fallback_font;

    func _draw():
        var white : Color = Color.WHITE
        var godot_blue : Color = Color("478cbf")
        var grey : Color = Color("414042")

        draw_polygon(head, [ godot_blue ])
        draw_polyline(mouth, white, _mouth_width)
        draw_circle(Vector2(42.479, 65.4825), 9.3905, white)
        draw_circle(Vector2(85.524, 65.4825), 9.3905, white)
        draw_circle(Vector2(43.423, 65.92), 6.246, grey)
        draw_circle(Vector2(84.626, 66.008), 6.246, grey)
        draw_line(Vector2(64.273, 60.564), Vector2(64.273, 74.349), white, 5.8)

        # Vẽ văn bản GODOT bên dưới logo bằng font mặc định, kích thước 22.
        draw_string(default_font, Vector2(20, 130), "GODOT",
                    HORIZONTAL_ALIGNMENT_CENTER, 90, 22)

 .. code-tab:: csharp

    private Font _defaultFont = ThemeDB.FallbackFont;

    public override void _Draw()
    {
        Color white = Colors.White;
        Color godotBlue = new Color("478cbf");
        Color grey = new Color("414042");

        DrawPolygon(_head, [godotBlue]);
        DrawPolyline(_mouth, white, _mouthWidth);
        DrawCircle(new Vector2(42.479f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(85.524f, 65.4825f), 9.3905f, white);
        DrawCircle(new Vector2(43.423f, 65.92f), 6.246f, grey);
        DrawCircle(new Vector2(84.626f, 66.008f), 6.246f, grey);
        DrawLine(new Vector2(64.273f, 60.564f), new Vector2(64.273f, 74.349f),
                 white, 5.8f);

        // Vẽ văn bản GODOT bên dưới logo bằng font mặc định, kích thước 22.
        DrawString(_defaultFont, new Vector2(20f, 130f), "GODOT",
                   HorizontalAlignment.Center, 90, 22);
    }

Ở đây, trước tiên chúng ta nạp font theme mặc định đã cấu hình vào biến defaultFont (có thể đặt một font tùy chỉnh thay thế), sau đó truyền các tham số sau: font, vị trí, văn bản, căn chỉnh ngang, độ rộng và kích thước font.

Bạn sẽ thấy kết quả sau trên màn hình:

.. image:: img/draw_godot_logo_text.webp

Bạn có thể tìm thấy các tham số bổ sung cũng như những phương thức khác liên quan đến văn bản và ký tự trong tài liệu tham chiếu class :ref:`CanvasItem <class_CanvasItem>`.

.. _doc_draw_show_drawing_while_editing_example:

Hiển thị hình vẽ khi chỉnh sửa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù code hiện tại có thể vẽ logo trong cửa sổ đang chạy, nó sẽ không hiển thị trên ``2D view`` trong editor. Trong một số trường hợp, bạn cũng muốn hiển thị Node2D hoặc control tùy chỉnh trên editor để định vị và điều chỉnh tỷ lệ của nó cho phù hợp, giống như hầu hết các node khác.

Để hiển thị logo trực tiếp trong editor (không cần chạy), bạn có thể sử dụng
:ref:`@tool <doc_gdscript_tool_mode>` annotation để yêu cầu phần vẽ tùy chỉnh của node cũng xuất hiện khi chỉnh sửa, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    @tool
    extends Node2D

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class MyNode2D : Node2D

Bạn sẽ cần lưu scene, build lại project (chỉ dành cho C#) và tự tải lại scene hiện tại tại tùy chọn menu ``Scene > Reload Saved Scene`` để làm mới node hiện tại trong chế độ xem ``2D`` lần đầu tiên bạn thêm hoặc xóa annotation ``@tool``.

Hoạt ảnh
~~~~~~~~

Nếu muốn làm cho hình dạng tùy chỉnh thay đổi trong runtime, chúng ta có thể sửa đổi các phương thức được gọi hoặc đối số của chúng trong thời gian thực thi, hoặc áp dụng một phép biến đổi.

Ví dụ, nếu muốn hình dạng tùy chỉnh vừa thiết kế xoay, chúng ta có thể thêm biến và đoạn mã sau vào các phương thức ``_ready`` và ``_process``:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    @export var rotation_speed : float = 1  # Tính bằng radian mỗi giây.

    func _ready():
        rotation = 0
        ...

    func _process(delta: float):
        rotation -= rotation_speed * delta

 .. code-tab:: csharp

    [Export]
    public float RotationSpeed { get; set; } = 1.0f;  // Tính bằng radian mỗi giây.

    public override void _Ready()
    {
        Rotation = 0;
        ...
    }

    public override void _Process(double delta)
    {
        Rotation -= RotationSpeed * (float)delta;
    }

Vấn đề với đoạn mã trên là vì chúng ta đã tạo các điểm gần đúng trên một hình chữ nhật bắt đầu từ góc trên bên trái, với tọa độ ``(0, 0)`` và mở rộng sang phải rồi xuống dưới, nên ta thấy phép xoay được thực hiện với góc trên bên trái làm tâm xoay. Thay đổi phép biến đổi vị trí trên node sẽ không giúp ích trong trường hợp này, vì phép biến đổi xoay được áp dụng trước.

Mặc dù có thể viết lại tọa độ của tất cả các điểm để chúng được căn giữa quanh ``(0, 0)``, bao gồm cả các tọa độ âm, nhưng việc đó sẽ tốn rất nhiều công sức.

Một cách khả thi để khắc phục vấn đề này là sử dụng cấp thấp hơn
phương thức :ref:`draw_set_transform<class_CanvasItem_method_draw_set_transform>` để khắc phục vấn đề này, dịch chuyển tất cả các điểm trong không gian riêng của CanvasItem, sau đó đưa nó trở lại vị trí ban đầu bằng một phép biến đổi node thông thường, trong editor hoặc trong code, như sau:

.. tabs::
 .. code-tab:: gdscript GDScript


    func _ready():
        rotation = 0
        position = Vector2(60, 60)
        ...

    func _draw():
        draw_set_transform(Vector2(-60, -60))
        ...

 .. code-tab:: csharp

    public override void _Ready()
    {
        Rotation = 0;
        Position = new Vector2(60, 60);
        ...
    }

    public override void _Draw()
    {
        DrawSetTransform(new Vector2(-60.0f, -60.0f));
        ...
    }

Kết quả là hình xoay quanh một tâm xoay hiện nằm tại ``(60, 60)``:

.. image:: img/draw_godot_rotation.webp

Nếu thứ chúng ta muốn tạo hoạt ảnh là một thuộc tính bên trong lời gọi ``_draw()``, chúng ta phải nhớ gọi ``queue_redraw()`` để buộc làm mới, nếu không thuộc tính đó sẽ không được cập nhật trên màn hình.

Ví dụ, đây là cách chúng ta có thể làm cho robot trông như đang mở và đóng miệng bằng cách thay đổi độ rộng đường miệng theo một đường cong hình sin (:ref:`sin<class_@globalscope_method_sin>`):

.. tabs::
 .. code-tab:: gdscript GDScript

    var _mouth_width : float = 4.4
    var _max_width : float = 7
    var _time : float = 0

    func _process(delta : float):
        _time += delta
        _mouth_width = abs(sin(_time) * _max_width)
        queue_redraw()

    func _draw():
        ...
        draw_polyline(mouth, white, _mouth_width)
        ...

 .. code-tab:: csharp

    private float _mouthWidth = 4.4f;
    private float _maxWidth = 7f;
    private float _time = 0f;

    public override void _Process(double delta)
    {
        _time += (float)delta;
        _mouthWidth = Mathf.Abs(Mathf.Sin(_time) * _maxWidth);
        QueueRedraw();
    }

    public override void _Draw()
    {
        ...
        DrawPolyline(_mouth, white, _mouthWidth);
        ...
    }

Khi chạy, kết quả sẽ trông gần như thế này:

.. image:: img/draw_godot_mouth_animation.webp

Lưu ý rằng ``_mouth_width`` là một thuộc tính do người dùng định nghĩa giống như mọi thuộc tính khác, và nó hoặc bất kỳ thuộc tính nào khác được dùng làm đối số vẽ đều có thể được tạo hoạt ảnh bằng các phương thức tiêu chuẩn, cấp cao hơn như :ref:`Tween<class_Tween>` hoặc một
Node :ref:`AnimationPlayer<class_AnimationPlayer>`. Điểm khác biệt duy nhất là cần có lời gọi ``queue_redraw()`` để áp dụng những thay đổi đó, nhờ vậy chúng mới được hiển thị trên màn hình.

.. _doc_draw_custom_example_2:

Ví dụ 2: vẽ một đường động
--------------------------

Ví dụ trước hữu ích để tìm hiểu cách vẽ và sửa đổi các node bằng hình dạng tùy chỉnh và hoạt ảnh. Cách này có một số ưu điểm, chẳng hạn như sử dụng tọa độ và vector chính xác để vẽ thay vì bitmap—điều đó có nghĩa là chúng sẽ co giãn tốt khi được biến đổi trên màn hình. Trong một số trường hợp, có thể đạt được kết quả tương tự bằng cách kết hợp các chức năng cấp cao hơn với những node như
:ref:`sprites<class_Sprite2D>` hoặc
:ref:`AnimatedSprites<class_AnimatedSprite2D>` để tải các tài nguyên SVG (cũng là những hình ảnh được định nghĩa bằng vector) và
node :ref:`AnimationPlayer<class_AnimationPlayer>`.

Trong những trường hợp khác, điều đó sẽ không thể thực hiện được vì trước khi chạy code, chúng ta sẽ không biết biểu diễn đồ họa tạo ra sẽ như thế nào. Ở đây, chúng ta sẽ xem cách vẽ một đường động có tọa độ chưa biết trước và chịu ảnh hưởng bởi đầu vào của người dùng.

Vẽ một đường thẳng giữa 2 điểm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Giả sử chúng ta muốn vẽ một đường thẳng giữa 2 điểm, điểm đầu tiên sẽ cố định tại góc trên bên trái ``(0, 0)`` và điểm thứ hai sẽ được xác định bởi vị trí con trỏ trên màn hình.

Chúng ta có thể vẽ một đường động giữa 2 điểm đó như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    var point1 : Vector2 = Vector2(0, 0)
    var width : int = 10
    var color : Color = Color.GREEN

    var _point2 : Vector2

    func _process(_delta):
        var mouse_position = get_viewport().get_mouse_position()
        if mouse_position != _point2:
            _point2 = mouse_position
            queue_redraw()

    func _draw():
        draw_line(point1, _point2, color, width)

 .. code-tab:: csharp

    using Godot;
    using System;

    public partial class MyNode2DLine : Node2D
    {
        public Vector2 Point1 { get; set; } = new Vector2(0f, 0f);
        public int Width { get; set; } = 10;
        public Color Color { get; set; } = Colors.Green;

        private Vector2 _point2;

        public override void _Process(double delta)
        {
            Vector2 mousePosition = GetViewport().GetMousePosition();
            if (mousePosition != _point2)
            {
                _point2 = mousePosition;
                QueueRedraw();
            }
        }

        public override void _Draw()
        {
            DrawLine(Point1, _point2, Color, Width);
        }
    }

Trong ví dụ này, mỗi frame chúng ta lấy vị trí chuột trong viewport mặc định bằng phương thức
:ref:`get_mouse_position <class_Viewport_method_get_mouse_position>`. Nếu vị trí đã thay đổi kể từ yêu cầu vẽ lần trước (một tối ưu hóa nhỏ để tránh vẽ lại ở mọi frame), chúng ta sẽ lên lịch vẽ lại. Phương thức ``_draw()`` của chúng ta chỉ có một dòng: yêu cầu vẽ một đường màu xanh lá rộng 10 pixel giữa góc trên bên trái và vị trí vừa lấy được.

Độ rộng, màu sắc và vị trí của điểm bắt đầu có thể được cấu hình bằng các thuộc tính tương ứng.

Khi chạy, kết quả sẽ trông như thế này:

.. image:: img/draw_line_between_2_points.webp

Vẽ một cung giữa 2 điểm
~~~~~~~~~~~~~~~~~~~~~~~

Ví dụ trên hoạt động, nhưng có thể chúng ta muốn nối 2 điểm đó bằng một hình dạng hoặc chức năng khác thay vì một đường thẳng.

Bây giờ hãy thử tạo một cung (một phần của đường tròn) giữa hai điểm.

Việc export điểm bắt đầu, số đoạn, độ rộng, màu sắc và khử răng cưa của đường sẽ cho phép chúng ta dễ dàng sửa đổi các thuộc tính đó trực tiếp từ bảng inspector của editor:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D

    @export var point1 : Vector2 = Vector2(0, 0)
    @export_range(1, 1000) var segments : int = 100
    @export var width : int = 10
    @export var color : Color = Color.GREEN
    @export var antialiasing : bool = false

    var _point2 : Vector2

 .. code-tab:: csharp

    using Godot;
    using System;

    public partial class MyNode2DLine : Node2D
    {
        [Export]
        public Vector2 Point1 { get; set; } = new Vector2(0f, 0f);
        [Export]
        public float Length { get; set; } = 350f;
        [Export(PropertyHint.Range, "1,1000,")]
        public int Segments { get; set; } = 100;
        [Export]
        public int Width { get; set; } = 10;
        [Export]
        public Color Color { get; set; } = Colors.Green;
        [Export]
        public bool AntiAliasing { get; set; } = false;

        private Vector2 _point2;
    }

.. image:: img/draw_dynamic_exported_properties.webp

Để vẽ cung, chúng ta có thể sử dụng phương thức
:ref:`draw_arc<class_CanvasItem_method_draw_arc>`. Có rất nhiều cung đi qua 2 điểm, vì vậy trong ví dụ này, chúng ta sẽ chọn nửa đường tròn có tâm nằm tại điểm giữa của 2 điểm ban đầu.

Việc tính toán cung này sẽ phức tạp hơn trường hợp đường thẳng:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        # Lấy trung bình các điểm để tìm tâm.
        var center : Vector2 = Vector2((_point2.x + point1.x) / 2,
                                       (_point2.y + point1.y) / 2)
        # Tính các tham số còn lại của cung.
        var radius : float = point1.distance_to(_point2) / 2
        var start_angle : float = (_point2 - point1).angle()
        var end_angle : float = (point1 - _point2).angle()
        if end_angle < 0:  # end_angle có khả năng là số âm, hãy chuẩn hóa nó.
            end_angle += TAU

        # Cuối cùng, vẽ cung.
        draw_arc(center, radius, start_angle, end_angle, segments, color,
                 width, antialiasing)

 .. code-tab:: csharp

    public override void _Draw()
    {
        // Lấy trung bình các điểm để tìm tâm.
        Vector2 center = new Vector2((_point2.X + Point1.X) / 2.0f,
                                        (_point2.Y + Point1.Y) / 2.0f);
        // Tính các tham số còn lại của cung.
        float radius = Point1.DistanceTo(_point2) / 2.0f;
        float startAngle = (_point2 - Point1).Angle();
        float endAngle = (Point1 - _point2).Angle();
        if (endAngle < 0.0f)  // endAngle có khả năng là số âm, hãy chuẩn hóa nó.
        {
            endAngle += Mathf.Tau;
        }

        // Cuối cùng, vẽ cung.
        DrawArc(center, radius, startAngle, endAngle, Segments, Color,
                Width, AntiAliasing);
    }

Tâm của nửa đường tròn sẽ là điểm giữa của hai điểm. Bán kính sẽ bằng một nửa khoảng cách giữa hai điểm. Góc bắt đầu và góc kết thúc sẽ là các góc của vector từ point1 đến point2 và ngược lại. Lưu ý rằng chúng ta phải chuẩn hóa ``end_angle`` thành các giá trị dương, vì nếu ``end_angle`` nhỏ hơn ``start_angle``, cung sẽ được vẽ ngược chiều kim đồng hồ, điều mà chúng ta không muốn trong trường hợp này (cung sẽ bị lộn ngược).

Kết quả sẽ trông như sau, với cung tròn đi xuống và nằm giữa hai điểm:

.. image:: img/draw_arc_between_2_points.webp

Bạn có thể thoải mái thử các tham số trong inspector để có được những kết quả khác nhau: thay đổi màu sắc, độ rộng, antialiasing và tăng số lượng đoạn để đường cong mượt hơn, nhưng sẽ tốn thêm hiệu năng.
