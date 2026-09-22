.. _doc_class_reference_primer:

Tổng quan về tham chiếu lớp
===========================

Trang này giải thích cách viết phần tham chiếu lớp. Bạn sẽ học cách xác định nơi viết các mô tả mới cho lớp, phương thức và thuộc tính của các node tích hợp sẵn trong Godot.

.. seealso::

    Để tìm hiểu cách gửi các thay đổi của bạn đến dự án Godot bằng hệ thống kiểm soát phiên bản Git, hãy xem `tài liệu đóng góp cho phần tham chiếu lớp <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__.

Phần tham chiếu cho mỗi lớp nằm trong một tệp XML như bên dưới:

.. code-block:: xml

    <class name="Node2D" inherits="CanvasItem" version="4.0">
        <brief_description>
            A 2D game object, inherited by all 2D-related nodes. Has a position, rotation, scale, and Z index.
        </brief_description>
        <description>
            A 2D game object, with a transform (position, rotation, and scale). All 2D nodes, including physics objects and sprites, inherit from Node2D. Use Node2D as a parent node to move, scale and rotate children in a 2D project. Also gives control of the node's render order.
        </description>
        <tutorials>
            <link title="Custom drawing in 2D">https://docs.godotengine.org/en/latest/tutorials/2d/custom_drawing_in_2d.html</link>
            <link title="All 2D Demos">https://github.com/godotengine/godot-demo-projects/tree/master/2d</link>
        </tutorials>
        <methods>
            <method name="apply_scale">
                <return type="void">
                </return>
                <argument index="0" name="ratio" type="Vector2">
                </argument>
                <description>
                    Multiplies the current scale by the [code]ratio[/code] vector.
                </description>
            </method>
            [...]
            <method name="translate">
                <return type="void">
                </return>
                <argument index="0" name="offset" type="Vector2">
                </argument>
                <description>
                    Translates the node by the given [code]offset[/code] in local coordinates.
                </description>
            </method>
        </methods>
        <members>
            <member name="global_position" type="Vector2" setter="set_global_position" getter="get_global_position">
                Global position.
            </member>
            [...]
            <member name="z_index" type="int" setter="set_z_index" getter="get_z_index" default="0">
                Z index. Controls the order in which the nodes render. A node with a higher Z index will display in front of others.
            </member>
        </members>
        <constants>
        </constants>
    </class>


Tệp bắt đầu bằng các mô tả ngắn và dài. Trong tài liệu được tạo, mô tả ngắn luôn nằm ở đầu trang, còn mô tả dài nằm bên dưới danh sách phương thức, biến và hằng số. Bạn có thể tìm thấy các phương thức, biến thành viên, hằng số và signal trong các node XML riêng biệt.

Với mỗi thành phần, bạn cần tìm hiểu cách chúng hoạt động trong mã nguồn của Godot. Sau đó, điền tài liệu cho chúng bằng cách hoàn thiện hoặc cải thiện văn bản trong các thẻ sau:

- `<brief_description>`
- `<description>`
- `<constant>`
- `<method>` (trong thẻ `<description>`; kiểu trả về và đối số không có chuỗi tài liệu riêng)
- `<member>`
- `<signal>` (trong thẻ `<description>`; đối số không có chuỗi tài liệu riêng)
- `<constant>`

Hãy viết bằng ngôn ngữ rõ ràng và đơn giản. Luôn tuân theo `hướng dẫn viết <https://contributing.godotengine.org/en/latest/documentation/guidelines/docs_writing_guidelines.html>`__ để giữ cho mô tả ngắn gọn và dễ đọc. **Không để lại các dòng trống** trong phần mô tả: mỗi dòng trong tệp XML sẽ tạo thành một đoạn mới, kể cả khi dòng đó trống.

.. _doc_class_reference_editing_xml:

Cách chỉnh sửa XML của lớp
--------------------------

Chỉnh sửa tệp của lớp bạn chọn trong ``doc/classes/`` để cập nhật phần tham chiếu lớp. Thư mục này chứa một tệp XML cho mỗi lớp. XML liệt kê các hằng số và phương thức mà bạn sẽ thấy trong phần tham chiếu lớp. Godot tự động tạo và cập nhật XML.

.. note:: Đối với một số module trong mã nguồn của engine, thay vào đó bạn sẽ tìm thấy các tệp XML trong thư mục ``modules/<module_name>/doc_classes/``.

Hãy chỉnh sửa tệp bằng trình soạn thảo văn bản yêu thích của bạn. Nếu sử dụng trình soạn thảo mã, hãy đảm bảo thụt lề bằng tab.

Để kiểm tra các sửa đổi bạn đã thực hiện có chính xác trong tài liệu được tạo hay không, hãy chuyển đến thư mục ``doc/`` và chạy lệnh ``make rst``. Lệnh này sẽ chuyển đổi các tệp XML sang định dạng của tài liệu trực tuyến và xuất lỗi nếu có vấn đề.

Ngoài ra, bạn có thể build Godot và mở trang đã sửa trong phần tham chiếu mã tích hợp sẵn. Để tìm hiểu cách biên dịch engine, hãy đọc :ref:`hướng dẫn biên dịch <toc-devel-compiling>`.

Chúng tôi khuyến nghị sử dụng một trình soạn thảo mã hỗ trợ tệp XML như Vim, Atom, Visual Studio Code, Notepad++ hoặc trình soạn thảo khác để chỉnh sửa tệp thuận tiện hơn. Bạn cũng có thể sử dụng tính năng tìm kiếm của chúng để nhanh chóng tìm các lớp và thuộc tính.

.. tip::

    Nếu sử dụng Visual Studio Code, bạn có thể cài đặt `tiện ích vscode-xml <https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml>`__ để bật linting cho các tệp XML tham chiếu lớp.

.. _doc_class_reference_bbcode:

Cải thiện định dạng bằng các thẻ kiểu BBCode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Phần tham chiếu lớp XML của Godot hỗ trợ các thẻ giống BBCode để liên kết cũng như định dạng văn bản và mã. Trong các bảng bên dưới, bạn có thể tìm thấy các thẻ hiện có, ví dụ sử dụng và kết quả sau khi chuyển đổi sang reStructuredText.

Liên kết
""""""""

Bất cứ khi nào liên kết đến một thành viên của lớp khác, bạn cần chỉ định tên lớp. Đối với liên kết đến cùng một lớp, tên lớp là tùy chọn và có thể được bỏ qua.

+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| Tag and Description            | Example                                 | Result                                                       |
+================================+=========================================+==============================================================+
| | ``[Class]``                  | ``Move the [Sprite2D].``                | Move the :ref:`class_Sprite2D`.                              |
| | Link to class                |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[annotation Class.name]``  | ``See [annotation @GDScript.@rpc].``    | See :ref:`@GDScript.@rpc <class_@GDScript_annotation_@rpc>`. |
| | Link to annotation           |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[constant Class.name]``    | ``See [constant Color.RED].``           | See :ref:`Color.RED <class_Color_constant_RED>`.             |
| | Link to constant             |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[enum Class.name]``        | ``See [enum Mesh.ArrayType].``          | See :ref:`Mesh.ArrayType <enum_Mesh_ArrayType>`.             |
| | Link to enum                 |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[member Class.name]``      | ``Get [member Node2D.scale].``          | Get :ref:`Node2D.scale <class_Node2D_property_scale>`.       |
| | Link to member               |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[method Class.name]``      | ``Call [method Node3D.hide].``          | Call :ref:`Node3D.hide() <class_Node3D_method_hide>`.        |
| | Link to method               |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[constructor Class.name]`` | ``Use [constructor Color.Color].``      | Use :ref:`Color.Color <class_Color_constructor_Color>`.      |
| | Link to built-in constructor |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[operator Class.name]``    | ``Use [operator Color.operator *].``    | Use :ref:`Color.operator * <class_Color_operator_mul_int>`.  |
| | Link to built-in operator    |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[signal Class.name]``      | ``Emit [signal Node.renamed].``         | Emit :ref:`Node.renamed <class_Node_signal_renamed>`.        |
| | Link to signal               |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[theme_item Class.name]``  | ``See [theme_item Label.font].``        | See :ref:`Label.font <class_Label_theme_font_font>`.         |
| | Link to theme item           |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+
| | ``[param name]``             | ``Takes [param size] for the size.``    | Takes ``size`` for the size.                                 |
| | Parameter name (as code)     |                                         |                                                              |
+--------------------------------+-----------------------------------------+--------------------------------------------------------------+

.. note::

    Hiện tại chỉ :ref:`class_@GDScript` có chú thích.

Định dạng văn bản
"""""""""""""""""

+--------------------------------+----------------------------------------------+------------------------------------+
| Tag and Description            | Example                                      | Result                             |
+================================+==============================================+====================================+
| | ``[br]``                     | | ``Line 1.[br]``                            | | Line 1.                          |
| | Line break                   | | ``Line 2.``                                | | Line 2.                          |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[lb]`` ``[rb]``            | ``[lb]b[rb]text[lb]/b[rb]``                  | [b]text[/b]                        |
| | ``[`` and ``]`` respectively |                                              |                                    |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[b]`` ``[/b]``             | ``Do [b]not[/b] call this method.``          | Do **not** call this method.       |
| | Bold                         |                                              |                                    |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[i]`` ``[/i]``             | ``Returns the [i]global[/i] position.``      | Returns the *global* position.     |
| | Italic                       |                                              |                                    |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[u]`` ``[/u]``             | ``[u]Always[/u] use this method.``           | .. raw:: html                      |
| | Underline                    |                                              |                                    |
|                                |                                              |     <u>Always</u> use this method. |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[s]`` ``[/s]``             | ``[s]Outdated information.[/s]``             | .. raw:: html                      |
| | Strikethrough                |                                              |                                    |
|                                |                                              |     <s>Outdated information.</s>   |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[url]`` ``[/url]``         | | ``[url]https://example.com[/url]``         | | https://example.com              |
| | Hyperlink                    | | ``[url=https://example.com]Website[/url]`` | | `Website <https://example.com>`_ |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[center]`` ``[/center]``   | ``[center]2 + 2 = 4[/center]``               | .. raw:: html                      |
| | Horizontal centering         |                                              |                                    |
|                                |                                              |     <center>2 + 2 = 4</center>     |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[kbd]`` ``[/kbd]``         | ``Press [kbd]Ctrl + C[/kbd].``               | Press :kbd:`Ctrl + C`.             |
| | Keyboard/mouse shortcut      |                                              |                                    |
+--------------------------------+----------------------------------------------+------------------------------------+
| | ``[code]`` ``[/code]``       | ``Returns [code]true[/code].``               | Returns ``true``.                  |
| | Inline code fragment         |                                              |                                    |
+--------------------------------+----------------------------------------------+------------------------------------+

.. note::

    1. Một số thẻ được hỗ trợ như ``[color]`` và ``[font]`` không được liệt kê ở đây vì không được khuyến nghị trong tài liệu của engine.
    2. ``[kbd]`` vô hiệu hóa BBCode cho đến khi trình phân tích cú pháp gặp ``[/kbd]``.
    3. ``[code]`` vô hiệu hóa BBCode cho đến khi trình phân tích cú pháp gặp ``[/code]``.

Định dạng các khối mã
"""""""""""""""""""""

Có hai tùy chọn để định dạng các khối mã:

1. Sử dụng ``[codeblock]`` nếu bạn muốn thêm một ví dụ cho một ngôn ngữ cụ thể.
2. Sử dụng ``[codeblocks]``, ``[gdscript]`` và ``[csharp]`` nếu bạn muốn thêm cùng một ví dụ cho cả hai ngôn ngữ GDScript và C#.

Theo mặc định, ``[codeblock]`` làm nổi bật cú pháp GDScript. Bạn có thể thay đổi điều này bằng thuộc tính ``lang``. Các tùy chọn hiện được hỗ trợ là:

- ``[codeblock lang=text]`` tắt tính năng làm nổi bật cú pháp;
- ``[codeblock lang=gdscript]`` làm nổi bật cú pháp GDScript;
- ``[codeblock lang=csharp]`` làm nổi bật cú pháp C# (chỉ trong phiên bản .NET).

.. note::

    ``[codeblock]`` vô hiệu hóa BBCode cho đến khi trình phân tích cú pháp gặp ``[/codeblock]``.

Ví dụ:

.. code-block:: none

    [codeblock]
    func _ready():
        var sprite = get_node("Sprite2D")
        print(sprite.get_pos())
    [/codeblock]

Sẽ hiển thị như sau:

.. code-block:: gdscript

    func _ready():
        var sprite = get_node("Sprite2D")
        print(sprite.get_pos())

Nếu cần có các phiên bản mã khác nhau trong GDScript và C#, hãy sử dụng ``[codeblocks]`` thay thế. Nếu sử dụng ``[codeblocks]``, bạn cũng cần có ít nhất một trong các thẻ dành riêng cho ngôn ngữ, ``[gdscript]`` và ``[csharp]``.

Luôn viết các ví dụ mã GDScript trước! Bạn có thể sử dụng `công cụ dịch mã thử nghiệm <https://github.com/HaSa1002/codetranslator>`_ này để tăng tốc quy trình làm việc.

.. code-block:: none

    [codeblocks]
    [gdscript]
    func _ready():
        var sprite = get_node("Sprite2D")
        print(sprite.get_pos())
    [/gdscript]
    [csharp]
    public override void _Ready()
    {
        var sprite = GetNode("Sprite2D");
        GD.Print(sprite.GetPos());
    }
    [/csharp]
    [/codeblocks]

Phần trên sẽ hiển thị như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        var sprite = get_node("Sprite2D")
        print(sprite.get_pos())

 .. code-tab:: csharp

    public override void _Ready()
    {
        var sprite = GetNode("Sprite2D");
        GD.Print(sprite.GetPos());
    }

Định dạng ghi chú và cảnh báo
"""""""""""""""""""""""""""""

Để biểu thị thông tin quan trọng, hãy thêm một đoạn bắt đầu bằng "[b]Note:[/b]" ở cuối phần mô tả:

.. code-block:: none

    [b]Note:[/b] Only available when using the Forward+ renderer.

Để biểu thị thông tin thiết yếu có thể gây ra vấn đề bảo mật hoặc mất dữ liệu nếu không được tuân thủ cẩn thận, hãy thêm một đoạn bắt đầu bằng "[b]Warning:[/b]" ở cuối phần mô tả:

.. code-block:: none

    [b]Warning:[/b] If this property is set to [code]true[/code], it allows clients to execute arbitrary code on the server.

Trong tất cả các đoạn được mô tả ở trên, hãy đảm bảo dấu câu nằm bên trong các thẻ BBCode để nhất quán.

Đánh dấu API là deprecated/experimental
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để đánh dấu một API là deprecated hoặc experimental, bạn cần thêm thuộc tính XML tương ứng. Giá trị thuộc tính phải là một thông báo giải thích lý do API không được khuyến nghị (hỗ trợ markup BBCode) hoặc một chuỗi trống (sẽ sử dụng thông báo mặc định). Nếu một phần tử API được đánh dấu là deprecated/experimental, phần tử đó được xem là đã có tài liệu ngay cả khi phần mô tả trống.

.. code-block:: xml

    <class name="Parallax2D" inherits="Node2D" experimental="This node is meant to replace [ParallaxBackground] and [ParallaxLayer]. The implementation may change in the future." xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="../class.xsd">
        [...]
    </class>

    <constant name="RESPONSE_USE_PROXY" value="305" enum="ResponseCode" deprecated="Many clients ignore this response code for security reasons. It is also deprecated by the HTTP standard.">
        HTTP status code [code]305 Use Proxy[/code].
    </constant>

    <member name="auto_translate" type="bool" setter="set_auto_translate" getter="is_auto_translating" deprecated="Use [member Node.auto_translate_mode] instead.">
        Toggles if any text should automatically change to its translated version depending on the current locale.
    </member>

    <method name="get_method_call_mode" qualifiers="const" deprecated="Use [member AnimationMixer.callback_mode_method] instead.">
        <return type="int" enum="AnimationPlayer.AnimationMethodCallMode" />
        <description>
            Returns the call mode used for "Call Method" tracks.
        </description>
    </method>

.. _`experimental code translation tool`: https://github.com/HaSa1002/codetranslator
