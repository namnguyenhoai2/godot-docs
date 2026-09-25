.. _doc_gdscript_documentation_comments:

Các chú thích tài liệu GDScript
===============================

Trong GDScript, bạn có thể sử dụng chú thích để ghi lại mã và thêm mô tả cho các thành viên của một script. Có hai điểm khác biệt giữa chú thích thông thường và chú thích tài liệu. Thứ nhất, chú thích tài liệu phải bắt đầu bằng hai ký hiệu thăng ``##``. Thứ hai, chú thích đó phải đứng ngay trước một thành viên của script hoặc, đối với phần mô tả script, phải được đặt ở đầu script. Nếu một biến được export có tài liệu, phần mô tả của biến sẽ được dùng làm tooltip trong trình chỉnh sửa. Trình chỉnh sửa có thể tạo tài liệu này dưới dạng các tệp XML.

Ghi tài liệu cho một script
---------------------------

Các chú thích ghi tài liệu cho một script phải xuất hiện trước mọi tài liệu của thành viên. Định dạng được đề xuất cho tài liệu của script có thể được chia thành ba phần.

- Mô tả ngắn gọn về script.
- Mô tả chi tiết.
- Tutorial và các đánh dấu deprecated/experimental.

Để phân tách các phần này, chú thích tài liệu sử dụng các tag đặc biệt. Tag phải nằm ở đầu dòng (bỏ qua khoảng trắng đứng trước) và phải có định dạng ``@``, theo sau là từ khóa.

Tag
~~~

+-------------------+--------------------------------------------------------+
| Brief description | No tag. Lives at the very beginning of                 |
|                   | the documentation section.                             |
+-------------------+--------------------------------------------------------+
| Description       | No tag. Use one blank line to separate the description |
|                   | from the brief.                                        |
+-------------------+--------------------------------------------------------+
| Tutorial          | | ``@tutorial: https://example.com``                   |
|                   | | ``@tutorial(The Title Here): https://example.com``   |
+-------------------+--------------------------------------------------------+
| Deprecated        | | ``@deprecated``                                      |
|                   | | ``@deprecated: Use [AnotherClass] instead.``         |
+-------------------+--------------------------------------------------------+
| Experimental      | | ``@experimental``                                    |
|                   | | ``@experimental: This class is unstable.``           |
+-------------------+--------------------------------------------------------+

Ví dụ:

::

    class_name MyClass
    extends Node2D
    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.
    ##
    ## @tutorial:             https://example.com/tutorial_1
    ## @tutorial(Tutorial 2): https://example.com/tutorial_2
    ## @experimental

.. warning::

    Nếu có khoảng trắng giữa tên tag và dấu hai chấm, chẳng hạn ``@tutorial  :``, tag đó sẽ không được xử lý như một tag hợp lệ và sẽ bị bỏ qua.

.. note::

    Khi phần mô tả trải dài trên nhiều dòng, khoảng trắng ở đầu và cuối sẽ bị loại bỏ rồi nối lại bằng một khoảng trắng đơn. Để giữ ngắt dòng, hãy sử dụng ``[br]``. Xem thêm `BBCode và tham chiếu class <BBCode and class reference_>`_ bên dưới.

Ghi tài liệu cho các thành viên của script
------------------------------------------

Các thành viên có thể được ghi tài liệu:

- Signal
- Enum
- Giá trị enum
- Hằng số
- Biến
- Hàm
- Class bên trong

Tài liệu của một thành viên script phải đứng ngay trước thành viên đó hoặc các annotation của thành viên nếu có. Phần mô tả có thể gồm nhiều dòng, nhưng mỗi dòng phải bắt đầu bằng ký hiệu hai dấu thăng ``##`` để được xem là một phần của tài liệu.

Tag
~~~

+--------------+--------------------------------------------------+
| Description  | No tag.                                          |
+--------------+--------------------------------------------------+
| Deprecated   | | ``@deprecated``                                |
|              | | ``@deprecated: Use [member another] instead.`` |
+--------------+--------------------------------------------------+
| Experimental | | ``@experimental``                              |
|              | | ``@experimental: This method is incomplete.``  |
+--------------+--------------------------------------------------+

Ví dụ:

::

    ## The description of the variable.
    ## @deprecated: Use [member other_var] instead.
    var my_var

Ngoài ra, bạn có thể sử dụng chú thích tài liệu nội dòng:

::

    signal my_signal ## My signal.

    enum MyEnum { ## My enum.
        VALUE_A = 0, ## Value A.
        VALUE_B = 1, ## Value B.
    }

    const MY_CONST = 1 ## My constant.

    var my_var ## My variable.


    func my_func(): ## My func.
        pass


    class MyClass: ## My class.
        pass

Tài liệu của script sẽ được cập nhật trong cửa sổ trợ giúp của trình chỉnh sửa mỗi khi script được cập nhật. Nếu tên của bất kỳ biến thành viên hoặc hàm nào bắt đầu bằng dấu gạch dưới, tên đó sẽ được xem là private. Thành viên đó sẽ không xuất hiện trong tài liệu và sẽ bị bỏ qua trong cửa sổ trợ giúp.

Ví dụ script hoàn chỉnh
-----------------------

::

    class_name MyClass
    extends Node2D
    ## A brief description of the class's role and functionality.
    ##
    ## The description of the script, what it can do,
    ## and any further detail.
    ##
    ## @tutorial:             https://example.com/tutorial_1
    ## @tutorial(Tutorial 2): https://example.com/tutorial_2
    ## @experimental

    ## The description of a signal.
    signal my_signal

    ## This is a description of the below enum.
    enum Direction {
        ## Direction up.
        UP = 0,
        ## Direction down.
        DOWN = 1,
        ## Direction left.
        LEFT = 2,
        ## Direction right.
        RIGHT = 3,
    }

    ## The description of a constant.
    const GRAVITY = 9.8

    ## The description of the variable v1.
    var v1

    ## This is a multiline description of the variable v2.[br]
    ## The type information below will be extracted for the documentation.
    var v2: int

    ## If the member has any annotation, the annotation should
    ## immediately precede it.
    @export
    var v3 := some_func()


    ## As the following function is documented, even though its name starts with
    ## an underscore, it will appear in the help window.
    func _fn(p1: int, p2: String) -> int:
        return 0


    # The below function isn't documented and its name starts with an underscore
    # so it will treated as private and will not be shown in the help window.
    func _internal() -> void:
        pass


    ## Documenting an inner class.
    ##
    ## The same rules apply here. The documentation must
    ## immediately precede the class definition.
    ##
    ## @tutorial: https://example.com/tutorial
    ## @experimental
    class Inner:

        ## Inner class variable v4.
        var v4


        ## Inner class function fn.
        func fn(): pass

Các tag ``@deprecated`` và ``@experimental``
--------------------------------------------

Bạn có thể đánh dấu một class hoặc bất kỳ thành viên nào của class là deprecated hoặc experimental. Thao tác này sẽ thêm chỉ báo tương ứng trong trình xem tài liệu tích hợp sẵn. Bạn cũng có thể cung cấp một thông báo ngắn giải thích lý do API đó không được khuyến nghị. Điều này đặc biệt hữu ích cho những người tạo plugin và thư viện.

.. image:: img/deprecated_and_experimental_tags.webp

- **Không được khuyến nghị** đánh dấu một API không được khuyến nghị và có thể bị loại bỏ hoặc thay đổi không tương thích trong một bản phát hành major trong tương lai. Thông thường, API này vẫn được giữ lại để đảm bảo khả năng tương thích ngược.
- **Experimental** đánh dấu một API mới, chưa ổn định và có thể bị thay đổi hoặc loại bỏ trong nhánh major hiện tại. Không khuyến nghị sử dụng API này trong mã production.

.. note::

    Mặc dù về mặt kỹ thuật bạn có thể sử dụng cả hai tag ``@deprecated`` và ``@experimental`` trên cùng một class/thành viên, nhưng không nên làm vậy vì trái với các quy ước phổ biến.

.. _doc_gdscript_documentation_comments_bbcode_and_class_reference:

.. _`BBCode and class reference`:

BBCode và tham chiếu class
--------------------------

Tham chiếu class của Godot hỗ trợ các tag giống BBCode. Chúng bổ sung định dạng đẹp cho văn bản và cũng có thể được sử dụng trong tài liệu. Xem thêm :ref:`BBCode tham chiếu class <doc_class_reference_bbcode>`. Lưu ý rằng cách này hơi khác với ``RichTextLabel`` :ref:`BBCode <doc_bbcode_in_richtextlabel>`.

Khi liên kết đến một thành viên của class khác, bạn cần chỉ định tên class. Đối với liên kết đến cùng một class, tên class là tùy chọn và có thể được bỏ qua.

Sau đây là danh sách các tag khả dụng:

+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| Tag and Description            | Example                                      | Result                                                       |
+================================+==============================================+==============================================================+
| | ``[Class]``                  | ``Move the [Sprite2D].``                     | Move the :ref:`class_Sprite2D`.                              |
| | Link to class                |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[annotation Class.name]``  | ``See [annotation @GDScript.@rpc].``         | See :ref:`@GDScript.@rpc <class_@GDScript_annotation_@rpc>`. |
| | Link to annotation           |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[constant Class.name]``    | ``See [constant Color.RED].``                | See :ref:`Color.RED <class_Color_constant_RED>`.             |
| | Link to constant             |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[enum Class.name]``        | ``See [enum Mesh.ArrayType].``               | See :ref:`Mesh.ArrayType <enum_Mesh_ArrayType>`.             |
| | Link to enum                 |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[member Class.name]``      | ``Get [member Node2D.scale].``               | Get :ref:`Node2D.scale <class_Node2D_property_scale>`.       |
| | Link to member (property)    |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[method Class.name]``      | ``Call [method Node3D.hide].``               | Call :ref:`Node3D.hide() <class_Node3D_method_hide>`.        |
| | Link to method               |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[constructor Class.name]`` | ``Use [constructor Color.Color].``           | Use :ref:`Color.Color <class_Color_constructor_Color>`.      |
| | Link to built-in constructor |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[operator Class.name]``    | ``Use [operator Color.operator *].``         | Use :ref:`Color.operator * <class_Color_operator_mul_int>`.  |
| | Link to built-in operator    |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[signal Class.name]``      | ``Emit [signal Node.renamed].``              | Emit :ref:`Node.renamed <class_Node_signal_renamed>`.        |
| | Link to signal               |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[theme_item Class.name]``  | ``See [theme_item Label.font].``             | See :ref:`Label.font <class_Label_theme_font_font>`.         |
| | Link to theme item           |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[param name]``             | ``Takes [param size] for the size.``         | Takes ``size`` for the size.                                 |
| | Parameter name (as code)     |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[br]``                     | | ``Line 1.[br]``                            | | Line 1.                                                    |
| | Line break                   | | ``Line 2.``                                | | Line 2.                                                    |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[lb]`` ``[rb]``            | ``[lb]b[rb]text[lb]/b[rb]``                  | [b]text[/b]                                                  |
| | ``[`` and ``]`` respectively |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[b]`` ``[/b]``             | ``Do [b]not[/b] call this method.``          | Do **not** call this method.                                 |
| | Bold                         |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[i]`` ``[/i]``             | ``Returns the [i]global[/i] position.``      | Returns the *global* position.                               |
| | Italic                       |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[u]`` ``[/u]``             | ``[u]Always[/u] use this method.``           | .. raw:: html                                                |
| | Underline                    |                                              |                                                              |
|                                |                                              |     <u>Always</u> use this method.                           |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[s]`` ``[/s]``             | ``[s]Outdated information.[/s]``             | .. raw:: html                                                |
| | Strikethrough                |                                              |                                                              |
|                                |                                              |     <s>Outdated information.</s>                             |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[color]`` ``[/color]``     | ``[color=red]Error![/color]``                | .. raw:: html                                                |
| | Color                        |                                              |                                                              |
|                                |                                              |     <span style="color:red;">Error!</span>                   |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[font]`` ``[/font]``       | ``[font=res://mono.ttf]LICENSE[/font]``      | .. raw:: html                                                |
| | Font                         |                                              |                                                              |
|                                |                                              |     <span style="font-family:monospace;">LICENSE</span>      |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[img]`` ``[/img]``         | ``[img width=32]res://icon.svg[/img]``       | .. image:: img/icon.svg                                      |
| | Image                        |                                              |    :width: 32 px                                             |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[url]`` ``[/url]``         | | ``[url]https://example.com[/url]``         | | https://example.com                                        |
| | Hyperlink                    | | ``[url=https://example.com]Website[/url]`` | | `Website <https://example.com>`_                           |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[center]`` ``[/center]``   | ``[center]2 + 2 = 4[/center]``               | .. raw:: html                                                |
| | Horizontal centering         |                                              |                                                              |
|                                |                                              |     <center>2 + 2 = 4</center>                               |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[kbd]`` ``[/kbd]``         | ``Press [kbd]Ctrl + C[/kbd].``               | Press :kbd:`Ctrl + C`.                                       |
| | Keyboard/mouse shortcut      |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[code]`` ``[/code]``       | ``Returns [code]true[/code].``               | Returns ``true``.                                            |
| | Inline code fragment         |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+
| | ``[codeblock]``              | *See below.*                                 | *See below.*                                                 |
| | ``[/codeblock]``             |                                              |                                                              |
| | Multiline code block         |                                              |                                                              |
+--------------------------------+----------------------------------------------+--------------------------------------------------------------+

.. note::

    1. Hiện tại chỉ :ref:`class_@GDScript` có annotation.
    2. ``[kbd]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/kbd]``.
    3. ``[code]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/code]``.
    4. ``[codeblock]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/codeblock]``.

.. warning::

    Sử dụng ``[codeblock]`` cho các khối mã được định dạng sẵn. Bên trong ``[codeblock]``, luôn sử dụng **bốn khoảng trắng** để thụt lề (parser sẽ xóa tab).

::

    ## Do something for this plugin. Before using the method
    ## you first have to [method initialize] [MyPlugin].[br]
    ## [color=yellow]Warning:[/color] Always [method clean] after use.[br]
    ## Usage:
    ## [codeblock]
    ## func _ready():
    ##     the_plugin.initialize()
    ##     the_plugin.do_something()
    ##     the_plugin.clean()
    ## [/codeblock]
    func do_something():
        pass

Theo mặc định, ``[codeblock]`` làm nổi bật cú pháp GDScript. Bạn có thể thay đổi điều này bằng thuộc tính ``lang``. Các tùy chọn hiện được hỗ trợ là:

- ``[codeblock lang=text]`` vô hiệu hóa tính năng làm nổi bật cú pháp;
- ``[codeblock lang=gdscript]`` làm nổi bật cú pháp GDScript;
- ``[codeblock lang=csharp]`` làm nổi bật cú pháp C# (chỉ trong phiên bản .NET).
