.. _doc_drawable_textures:

Sử dụng DrawableTextures
========================

DrawableTextures là một loại Texture2D có thêm các hàm để sửa đổi texture thông qua GPU. Bạn có thể sử dụng chúng cho việc tạo texture theo quy trình (procedural texturing), hiệu ứng theo thời gian thực và nhiều mục đích khác.

Blit hình chữ nhật cơ bản
-------------------------

Thao tác cơ bản nhất trên một drawable texture là
:ref:`blit_rect() <class_DrawableTexture2D_method_blit_rect>`.
Blit (sao chép) toàn bộ một texture vào hình chữ nhật đã cho trên ``DrawableTexture``.

.. tabs::
 .. code-tab:: gdscript GDScript

    texture.blit_rect(Rect2(20, 50, 60, 60), preload("res://circle.svg"))
    texture.blit_rect(Rect2(20, 50, 60, 60), preload("res://circle.svg"), Color.WHITE, 0)

 .. code-tab:: csharp

    texture.BlitRect(new Rect2I(20, 50, 60, 60), GD.Load<Texture2D>("res://circle.svg"));
    texture.BlitRect(new Rect2I(20, 50, 60, 60), GD.Load<Texture2D>("res://circle.svg"), Colors.White, 0);


Đoạn mã trên blit texture hình tròn vào hình chữ nhật ``(20, 50, 60, 60)`` trên ``DrawableTexture``. ``(20, 50)`` là góc trên bên trái của hình chữ nhật được vẽ, còn ``(60, 60)`` là kích thước của nó. Nếu muốn vẽ lên toàn bộ texture, chỉ cần đặt tham số ``rect`` bằng kích thước của ``DrawableTexture``.

Tham số thứ ba trong ``blit_rect()`` là một tham số tùy chọn, ``modulate``. Đây là một màu mà đầu ra được nhân với nó (theo hành vi mặc định). Bạn có thể dùng tham số này để đổi màu hoặc thậm chí che đầu ra đã vẽ của ``blit_rect()``. Ví dụ, sử dụng giá trị modulate ``Color(0, 0, 1, 0)`` sẽ chỉ vẽ và cập nhật các giá trị màu xanh dương của mỗi pixel trên ``DrawableTexture``.

Tham số thứ tư của ``blit_rect()``, ``mipmap``, có thể chỉ định một mức mipmap để vẽ vào. Bạn chỉ cần sử dụng tham số này nếu muốn kiểm soát chi tiết từng lớp mipmap. Lưu ý rằng bạn không cần điều chỉnh kích thước hình chữ nhật; nó sẽ được chuyển đổi thành một phần tương ứng với kích thước tổng thể của texture. Nếu chỉ muốn cập nhật tất cả các lớp mipmap, hãy vẽ lên texture rồi gọi ``generate_mipmaps()`` trên nó.

Blend mode và texture blit shader
---------------------------------

Quy trình vẽ cho ``blit_rect()`` và DrawableTextures được điều khiển bởi một
:ref:`texture blit shader <doc_texture_blit_shader>`. Even when the user does
nếu bạn không cung cấp shader, engine sẽ sử dụng texture blit shader mặc định.

.. code-block:: glsl

    // Texture blit shader mặc định.

    shader_type texture_blit;
    render_mode blend_mix;

    uniform sampler2D source_texture0 : hint_blit_source0;
    uniform sampler2D source_texture1 : hint_blit_source1;
    uniform sampler2D source_texture2 : hint_blit_source2;
    uniform sampler2D source_texture3 : hint_blit_source3;

    void blit() {
        // Sao chép từ toàn bộ từng source texture vào một hình chữ nhật trên từng output texture.
        COLOR0 = texture(source_texture0, UV) * MODULATE;
        COLOR1 = texture(source_texture1, UV) * MODULATE;
        COLOR2 = texture(source_texture2, UV) * MODULATE;
        COLOR3 = texture(source_texture3, UV) * MODULATE;
    }

Blend mode được chỉ định trong ``render_mode`` xác định cách giá trị màu đầu ra được blend với giá trị màu hiện tại của pixel trên DrawableTexture. Theo mặc định, engine sử dụng ``blend_mix`` nếu không có blend mode nào được chỉ định trong ``render_mode``. Texture blit shader cũng hỗ trợ ``blend_add`` (cộng), ``blend_sub`` (trừ), ``blend_mul`` (nhân) và ``blend_disabled`` (alpha không hoạt động như độ trong suốt mà được ghi nguyên trạng). Blend mode alpha premultiplied *không* được hỗ trợ ở đây.

Bạn cũng có thể sử dụng một blend mode khác với blend mode được chỉ định trong shader. Để làm vậy, bạn có thể khởi tạo và truyền một :ref:`class_BlitMaterial` mới vào script.

.. tabs::
 .. code-tab:: gdscript GDScript

    var blit_material = BlitMaterial.new()
    blit_material.blend_mode = BlitMaterial.BLEND_MODE_DISABLED
    texture.blit_rect(Rect2(0, 0, 200, 200), load("res://icon.svg"), Color.WHITE, 0, blit_material)

 .. code-tab:: csharp

    var blitMaterial = new BlitMaterial
    {
        BlendMode = BlitMaterial.BlendModeEnum.Disabled,
    };
    texture.BlitRect(new Rect2I(0, 0, 200, 200), GD.Load<Texture2D>("res://icon.svg"), Colors.White, 0, blitMaterial);


Nếu muốn có hành vi phức tạp hơn, bạn có thể tự viết texture blit shader. Tạo một shader mới với loại shader ``texture_blit``, viết mã shader của bạn rồi nạp nó vào một material để truyền vào hàm.

.. note::

    Material được truyền dưới dạng tham số của hàm thay vì được bind vào resource. Điều này giúp thực hiện nhiều kiểu vẽ trên cùng một texture dễ dàng hơn.

Sử dụng nhiều blit trong một texture
------------------------------------

DrawableTextures cũng có một phương thức :ref:`blit_rect_multi() <class_DrawableTexture2D_method_blit_rect_multi>`, cho phép tối đa 4 input và output trong cùng một bước.

.. tabs::
 .. code-tab:: gdscript GDScript

    texture.blit_rect_multi(
            Rect2(0, 0, 200, 200),
            [preload("res://icon.svg"), preload("res://circle.svg")],
            [other_drawable_texture]
        )

 .. code-tab:: csharp

    texture.BlitRectMulti(
        new Rect2I(0, 0, 200, 200),
        [GD.Load<Texture2D>("res://icon.svg"),
        GD.Load<Texture2D>("res://circle.svg")],
        [otherDrawableTexture]);

Hành vi mặc định của phương thức này chỉ đơn giản là ghép từng input với output tương ứng theo thứ tự. Ví dụ, điều này có thể hữu ích khi vẽ đồng thời lên albedo texture, normal texture và height texture.

Tất nhiên, bạn cũng có thể tùy chỉnh hành vi này thông qua texture blit shader. Trong shader, các output bổ sung được ghi thông qua ``COLOR1``, ``COLOR2`` và ``COLOR3`` (trong đó ``COLOR0`` là output chính). Các input bổ sung có thể được đọc dưới dạng uniform bằng ``hint_blit_source1``, ``hint_blit_source2`` và ``hint_blit_source3``.

.. _doc_drawable_textures_example_1:

Ví dụ 1: Vẽ đơn giản
--------------------

Một trong những cách sử dụng trực quan nhất của DrawableTextures là để, đúng như tên gọi, vẽ! Trong ví dụ này, chúng ta sẽ bắt đầu một project mới và tạo một UI scene mới với một node Control ở gốc.

Tiếp theo, bạn cần tạo một node :ref:`class_TextureRect`, node này sẽ là canvas của người dùng. Đặt kích thước phù hợp với màn hình, sau đó gắn một script mới vào node. Phần đầu của script này cần khởi tạo texture của TextureRect thành một DrawableTexture mới.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends TextureRect

    func _ready():
        texture = DrawableTexture2D.new()
        # Hãy cẩn thận; nếu kích thước của node không bằng kích thước được đặt ở đây,
        # lệnh vẽ của chúng ta sau đó có vẻ sẽ xảy ra ở vị trí không đúng.
        texture.setup(500, 500, DrawableTexture2D.DRAWABLE_FORMAT_RGBA8, false)

 .. code-tab:: csharp

    private DrawableTexture2D _texture = new DrawableTexture2D();

    public override void _Ready()
    {
        // Hãy cẩn thận; nếu kích thước của node không bằng kích thước được đặt ở đây,
        // lệnh vẽ của chúng ta sau đó có vẻ sẽ xảy ra ở vị trí không đúng.
        _texture.Setup(500, 500, DrawableTexture2D.DrawableFormat.Rgba8, null, false);
        Texture = _texture;
    }

Tiếp theo, chúng ta cần để TextureRect phản hồi thao tác nhấp và kéo của người chơi như thể họ đang vẽ. Để làm vậy, chúng ta có thể override phương thức ``_gui_input()`` từ TextureRect trong script của mình và phân tích các sự kiện InputMouseButton và InputMouseMotion:

.. tabs::
 .. code-tab:: gdscript GDScript

    var drawing = false

    func _gui_input(event):
        if event is InputEventMouseButton:
            # Nhấp/bỏ nhấp chuột - bắt đầu/dừng vẽ.
            drawing = not drawing
        if event is InputEventMouseMotion and drawing:
            # Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
            # thay vì đặt chuột ở góc trên bên trái.
            var rect = Rect2(event.position.x - 10, event.position.y - 10, 20, 20)
            texture.blit_rect(rect, null)

 .. code-tab:: csharp

    public bool drawing = false;

    public override void _GuiInput(InputEvent @event)
    {
        if (@event is InputEventMouseButton)
        {
            // Nhấp/bỏ nhấp chuột - bắt đầu/dừng vẽ.
            drawing = !drawing;
        }
        if (@event is InputEventMouseMotion eventMouseMotion && drawing)
        {
            // Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
            // thay vì đặt chuột ở góc trên bên trái.
            var rect = new Rect2I(
                (int)(eventMouseMotion.Position.X - 10),
                (int)(eventMouseMotion.Position.Y - 10),
                20, 20);
            _texture.BlitRect(rect, null);
        }
    }

Bây giờ, thao tác nhấp và kéo quanh TextureRect sẽ vẽ các hình vuông màu đen. Để nét vẽ tự nhiên hơn, có lẽ chúng ta nên vẽ một hình tròn và thực sự tô màu cho nó.

Chúng ta có thể điều chỉnh nội dung được vẽ bằng cách sử dụng một Texture để sao chép từ đó và tham số modulate. Chúng ta sẽ sử dụng :download:`plain white circle texture <img/circle.svg>` này, nạp nó làm tham số ``texture`` trong ``blit_rect()``, và sử dụng màu đỏ làm tham số ``modulate``.

.. tabs::
 .. code-tab:: gdscript

    if event is InputEventMouseMotion and drawing:
        # Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
        # thay vì đặt chuột ở góc trên bên trái.
        var rect = Rect2(event.position.x - 10, event.position.y - 10, 20, 20)
        texture.blit_rect(rect, preload("res://circle.svg"), Color.RED)

 .. code-tab:: csharp

    if (@event is InputEventMouseMotion eventMouseMotion && drawing)
    {
        // Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
        // thay vì đặt chuột ở góc trên bên trái.
        var rect = new Rect2I(
            (int)(eventMouseMotion.Position.X - 10),
            (int)(eventMouseMotion.Position.Y - 10),
            20, 20);
        _texture.BlitRect(rect, GD.Load<Texture2D>("res://circle.svg"), Colors.Red);
    }

Nét vẽ giờ đây trông tự nhiên và nhiều màu sắc hơn. Để tùy chỉnh thêm, bạn có thể kết nối một node :ref:`class_ColorPickerButton` với script để lưu lựa chọn màu của người dùng cho tham số ``modulate`` của ``blit_rect()``. Bạn cũng có thể lưu một biến kích thước cọ, cung cấp cho người dùng cách điều chỉnh biến này và đưa nó vào phép tính hình chữ nhật để người dùng có thể vẽ các nét lớn hơn hoặc nhỏ hơn.

.. tabs::
 .. code-tab:: gdscript GDScript

    var drawing = false
    var my_color = Color.RED
    var my_size = 20.0

    func _gui_input(event):
        if event is InputEventMouseButton:
            # Nhấp/bỏ nhấp chuột - bắt đầu/dừng vẽ.
            drawing = not drawing
        if event is InputEventMouseMotion and drawing:
            # Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
            # thay vì đặt chuột ở góc trên bên trái.
            var rect = Rect2(event.position.x - my_size / 2, event.position.y - my_size / 2, my_size, my_size)
            texture.blit_rect(rect, preload("res://circle.svg"), my_color)

    func _on_color_picker_button_color_changed(color):
        my_color = color

    func _on_h_slider_value_changed(value):
        my_size = value

 .. code-tab:: csharp

    private bool _drawing = false;
    private Color _myColor = Colors.Red;
    private int _mySize = 20;

    public override void _GuiInput(InputEvent @event)
    {
        if (@event is InputEventMouseButton)
        {
            // Nhấp/bỏ nhấp chuột - bắt đầu/dừng vẽ.
            _drawing = !_drawing;
        }
        if (@event is InputEventMouseMotion eventMouseMotion && _drawing)
        {
            // Tính toán hình chữ nhật để căn giữa hình chữ nhật được vẽ theo vị trí chuột
            // thay vì đặt chuột ở góc trên bên trái.
            var rect = new Rect2I(
                (int)(eventMouseMotion.Position.X - _mySize / 2),
                (int)(eventMouseMotion.Position.Y - _mySize / 2),
                _mySize, _mySize);
            _texture.BlitRect(rect, GD.Load<Texture2D>("res://circle.svg"), _myColor);
        }
    }

    public void OnColorPickerButtonColorChanged(Color color)
    {
        _myColor = color;
    }

    public void OnHSliderValueChanged(float value)
    {
        _mySize = (int)value;
    }

