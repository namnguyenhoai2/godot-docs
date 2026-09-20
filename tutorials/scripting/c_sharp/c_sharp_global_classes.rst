.. _doc_c_sharp_global_classes:

Các lớp C# global
=================

Các lớp global (còn được gọi là named scripts) là những kiểu được đăng ký trong editor của Godot để có thể sử dụng thuận tiện hơn.
:ref:`In GDScript <doc_gdscript_basics_class_name>`, this is achieved
bằng cách sử dụng từ khóa ``class_name`` ở đầu script. Trang này mô tả cách đạt được hiệu ứng tương tự trong C#.

- Các lớp global xuất hiện trong hộp thoại *Add Node* và *Create Resource*. - Nếu một :ref:`exported property <doc_c_sharp_exports>` là lớp global, inspector sẽ hạn chế phép gán, chỉ cho phép các instance của lớp global đó hoặc bất kỳ lớp dẫn xuất nào.

Các lớp global được đăng ký bằng attribute ``[GlobalClass]``.

.. code-block:: csharp

    using Godot;

    [GlobalClass]
    public partial class MyNode : Node
    {
    }

.. warning::

    Tên tệp phải khớp với tên lớp theo cách **phân biệt chữ hoa chữ thường**. Ví dụ, một lớp global có tên "MyNode" phải có tên tệp là ``MyNode.cs``, không phải ``myNode.cs``.

Kiểu ``MyNode`` sẽ được đăng ký dưới dạng lớp global với cùng tên với tên của kiểu đó.

.. image:: img/globalclasses_addnode.webp

Cửa sổ *Select a Node* dành cho thuộc tính được export ``MyNode`` sẽ lọc danh sách các node trong scene để khớp với hạn chế phép gán.

.. code-block:: csharp

    public partial class Main : Node
    {
        [Export]
        public MyNode MyNode { get; set; }
    }

.. image:: img/globalclasses_exportednode.webp

Nếu một kiểu tùy chỉnh chưa được đăng ký dưới dạng lớp global, phép gán sẽ bị giới hạn ở kiểu Godot mà kiểu tùy chỉnh đó dựa trên. Ví dụ, các phép gán trong inspector cho một export có kiểu ``MySimpleSprite2D`` sẽ bị giới hạn ở ``Sprite2D`` và các kiểu dẫn xuất.

.. code-block:: csharp

    public partial class MySimpleSprite2D : Sprite2D
    {
    }

Khi được kết hợp với attribute ``[GlobalClass]``, attribute ``[Icon]`` cho phép cung cấp một đường dẫn đến icon sẽ hiển thị khi lớp được hiển thị trong editor.

.. code-block:: csharp

    using Godot;

    [GlobalClass, Icon("res://Stats/StatsIcon.svg")]
    public partial class Stats : Resource
    {
        [Export]
        public int Strength { get; set; }

        [Export]
        public int Defense { get; set; }

        [Export]
        public int Speed { get; set; }
    }

.. image:: img/globalclasses_createresource.webp

Lớp ``Stats`` là một resource tùy chỉnh được đăng ký dưới dạng lớp global. :ref:`Exporting properties <doc_c_sharp_exports>` thuộc kiểu ``Stats`` sẽ chỉ cho phép gán các instance của kiểu resource này, đồng thời inspector sẽ cho phép bạn dễ dàng tạo và tải các instance của kiểu này.

.. image:: img/globalclasses_exportedproperty1.webp

.. image:: img/globalclasses_exportedproperty2.webp

.. warning::

    Godot editor sẽ ẩn các lớp tùy chỉnh có tên bắt đầu bằng tiền tố "Editor" trong các cửa sổ hộp thoại "Create New Node" hoặc "Create New Scene". Các lớp này vẫn có thể được khởi tạo trong runtime thông qua tên lớp, nhưng sẽ tự động bị các cửa sổ editor ẩn đi cùng với những node editor tích hợp được Godot editor sử dụng.
