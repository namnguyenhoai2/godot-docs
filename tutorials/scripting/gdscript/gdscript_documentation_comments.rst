.. _doc_gdscript_documentation_comments:

Các comment documentation của GDScript
======================================

Trong GDScript, comment có thể được dùng để document code và thêm mô tả cho các member của một script. Có hai điểm khác nhau giữa comment thông thường và comment documentation. Thứ nhất, comment documentation phải bắt đầu bằng hai ký hiệu hash ``##``. Thứ hai, nó phải đứng ngay trước một member của script hoặc, đối với mô tả script, phải được đặt ở đầu script. Nếu một biến được export có documentation, mô tả của biến sẽ được dùng làm tooltip trong editor. Documentation này có thể được editor tạo dưới dạng các tệp XML.

Document một script
-------------------

Các comment document một script phải xuất hiện trước mọi documentation của member. Định dạng được đề xuất cho documentation của script có thể được chia thành ba phần.

- Mô tả ngắn gọn về script. - Mô tả chi tiết. - Tutorial và các đánh dấu deprecated/experimental.

Để phân tách các phần này, comment documentation sử dụng các tag đặc biệt. Tag phải nằm ở đầu một dòng (bỏ qua khoảng trắng ở trước) và phải có định dạng ``@``, theo sau là keyword.

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
    ## Mô tả ngắn gọn về vai trò và chức năng của class.
    ##
    ## Mô tả về script, những gì nó có thể làm,
    ## và mọi chi tiết bổ sung.
    ##
    ## @tutorial:             https://example.com/tutorial_1
    ## @tutorial(Tutorial 2): https://example.com/tutorial_2
    ## @experimental

.. warning::

    Nếu có khoảng trắng giữa tên tag và dấu hai chấm, chẳng hạn ``@tutorial :``, nó sẽ không được xem là tag hợp lệ và sẽ bị bỏ qua.

.. note::

    Khi mô tả trải dài trên nhiều dòng, khoảng trắng ở đầu và cuối sẽ bị loại bỏ, sau đó các dòng được nối bằng một khoảng trắng. Để giữ ngắt dòng, hãy sử dụng ``[br]``. Xem thêm `BBCode và tham chiếu class`_ bên dưới.

Document các member của script
------------------------------

Các member áp dụng cho documentation:

- Signal - Enum - Giá trị enum - Constant - Variable - Function - Inner class

Documentation của một member trong script phải đứng ngay trước member đó hoặc các annotation của nó, nếu có. Mô tả có thể dài hơn một dòng, nhưng mọi dòng phải bắt đầu bằng hai ký hiệu hash ``##`` để được xem là một phần của documentation.

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

    ## Mô tả về biến.
    ## @deprecated: Thay vào đó, hãy dùng [member other_var].
    var my_var

Ngoài ra, bạn có thể sử dụng comment documentation inline:

::

    signal my_signal ## Signal của tôi.

    enum MyEnum { ## Enum của tôi.
        VALUE_A = 0, ## Giá trị A.
        VALUE_B = 1, ## Giá trị B.
    }

    const MY_CONST = 1 ## Constant của tôi.

    var my_var ## Variable của tôi.


    func my_func(): ## Func của tôi.
        pass


    class MyClass: ## Class của tôi.
        pass

Documentation của script sẽ được cập nhật trong cửa sổ trợ giúp của editor mỗi khi script được cập nhật. Nếu tên của bất kỳ member variable hoặc function nào bắt đầu bằng dấu gạch dưới, nó sẽ được xem là private. Nó sẽ không xuất hiện trong documentation và sẽ bị bỏ qua trong cửa sổ trợ giúp.

Ví dụ script hoàn chỉnh
-----------------------

::

    class_name MyClass
    extends Node2D
    ## Mô tả ngắn gọn về vai trò và chức năng của class.
    ##
    ## Mô tả về script, những gì nó có thể làm,
    ## và mọi chi tiết bổ sung.
    ##
    ## @tutorial:             https://example.com/tutorial_1
    ## @tutorial(Tutorial 2): https://example.com/tutorial_2
    ## @experimental

    ## Mô tả về một signal.
    signal my_signal

    ## Đây là mô tả của enum bên dưới.
    enum Direction {
        ## Hướng lên.
        UP = 0,
        ## Hướng xuống.
        DOWN = 1,
        ## Hướng sang trái.
        LEFT = 2,
        ## Hướng sang phải.
        RIGHT = 3,
    }

    ## Mô tả về một constant.
    const GRAVITY = 9.8

    ## Mô tả về variable v1.
    var v1

    ## Đây là mô tả nhiều dòng của variable v2.[br]
    ## Thông tin kiểu bên dưới sẽ được trích xuất cho documentation.
    var v2: int

    ## Nếu member có annotation, annotation đó phải
    ## đứng ngay trước member.
    @export
    var v3 := some_func()


    ## Vì function sau đây được document, mặc dù tên của nó bắt đầu bằng
    ## dấu gạch dưới, nó sẽ xuất hiện trong cửa sổ trợ giúp.
    func _fn(p1: int, p2: String) -> int:
        return 0


    # Function bên dưới không được document và tên của nó bắt đầu bằng dấu gạch dưới
    # nên nó sẽ được xem là private và không được hiển thị trong cửa sổ trợ giúp.
    func _internal() -> void:
        pass


    ## Document một inner class.
    ##
    ## Các quy tắc tương tự cũng được áp dụng ở đây. Documentation phải
    ## đứng ngay trước định nghĩa class.
    ##
    ## @tutorial: https://example.com/tutorial
    ## @experimental
    class Inner:

        ## Variable v4 của inner class.
        var v4


        ## Function fn của inner class.
        func fn(): pass

Các tag ``@deprecated`` và ``@experimental``
--------------------------------------------

Bạn có thể đánh dấu một class hoặc bất kỳ member nào của nó là deprecated hoặc experimental. Việc này sẽ thêm chỉ báo tương ứng vào trình xem documentation tích hợp sẵn. Bạn cũng có thể cung cấp một thông báo ngắn giải thích lý do API không được khuyến nghị. Điều này đặc biệt hữu ích cho những người tạo plugin và library.

.. image:: img/deprecated_and_experimental_tags.webp

- **Deprecated** đánh dấu một API không được khuyến nghị và có thể bị loại bỏ hoặc thay đổi không tương thích trong một bản phát hành major trong tương lai. Thông thường, API vẫn được giữ lại để đảm bảo khả năng tương thích ngược. - **Experimental** đánh dấu một API mới, chưa ổn định, có thể bị thay đổi hoặc loại bỏ trong nhánh major hiện tại. Không khuyến nghị sử dụng API này trong code production.

.. note::

    Mặc dù về mặt kỹ thuật bạn có thể sử dụng cả hai tag ``@deprecated`` và ``@experimental`` trên cùng một class/member, nhưng không nên làm vậy vì trái với các quy ước phổ biến.

.. _doc_gdscript_documentation_comments_bbcode_and_class_reference:

BBCode và tham chiếu class
--------------------------

Tham chiếu class của Godot hỗ trợ các tag tương tự BBCode. Chúng thêm định dạng đẹp cho văn bản, và định dạng này cũng có thể được sử dụng trong documentation. Xem thêm :ref:`class reference bbcode <doc_class_reference_bbcode>`. Lưu ý rằng cách này hơi khác với ``RichTextLabel`` :ref:`BBCode <doc_bbcode_in_richtextlabel>`.

Bất cứ khi nào liên kết đến một member của class khác, bạn cần chỉ định tên class. Đối với liên kết đến cùng một class, tên class là tùy chọn và có thể được bỏ qua.

Dưới đây là danh sách các tag khả dụng:

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

    1. Hiện tại chỉ :ref:`class_@GDScript` có annotation. 2. ``[kbd]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/kbd]``. 3. ``[code]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/code]``. 4. ``[codeblock]`` vô hiệu hóa BBCode cho đến khi parser gặp ``[/codeblock]``.

.. warning::

    Sử dụng ``[codeblock]`` cho các code block đã được định dạng sẵn. Bên trong ``[codeblock]``, luôn sử dụng **bốn khoảng trắng** để thụt lề (parser sẽ xóa các tab).

::

    ## Thực hiện việc gì đó cho plugin này. Trước khi sử dụng method
    ## trước tiên bạn phải [method initialize] [MyPlugin].[br]
    ## [color=yellow]Cảnh báo:[/color] Luôn [method clean] sau khi sử dụng.[br]
    ## Cách sử dụng:
    ## [codeblock]
    ## func _ready():
    ##     the_plugin.initialize()
    ##     the_plugin.do_something()
    ##     the_plugin.clean()
    ## [/codeblock]
    func do_something():
        pass

Theo mặc định, ``[codeblock]`` làm nổi bật cú pháp GDScript. Bạn có thể thay đổi điều này bằng attribute ``lang``. Các tùy chọn hiện được hỗ trợ là:

- ``[codeblock lang=text]`` vô hiệu hóa tô sáng cú pháp; - ``[codeblock lang=gdscript]`` tô sáng cú pháp GDScript; - ``[codeblock lang=csharp]`` tô sáng cú pháp C# (chỉ trong phiên bản .NET).
