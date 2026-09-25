.. _doc_c_sharp_global_classes:

Các lớp global của C#
=====================

Các lớp global (còn được gọi là named script) là những type được đăng ký trong editor của Godot để có thể sử dụng thuận tiện hơn.
:ref:`Trong GDScript <doc_gdscript_basics_class_name>`, bạn thực hiện việc này bằng cách sử dụng từ khóa ``class_name`` ở đầu script. Trang này mô tả cách đạt được hiệu ứng tương tự trong C#.

- Các lớp global xuất hiện trong hộp thoại *Add Node* và *Create Resource*.
- Nếu một :ref:`exported property <doc_c_sharp_exports>` là một lớp global, inspector sẽ hạn chế việc gán, chỉ cho phép các instance của lớp global đó hoặc bất kỳ lớp dẫn xuất nào.

Các lớp global được đăng ký bằng ``[GlobalClass]`` attribute.

.. code-block:: csharp

    using Godot;

    [GlobalClass]
    public partial class MyNode : Node
    {
    }

.. warning::

    Tên tệp phải khớp với tên lớp theo cách **phân biệt chữ hoa chữ thường**. Ví dụ: một lớp global có tên "MyNode" phải có tên tệp là ``MyNode.cs``, không phải ``myNode.cs``.

``MyNode`` type sẽ được đăng ký thành một lớp global với cùng tên với tên của type.

.. image:: img/globalclasses_addnode.webp

Cửa sổ *Select a Node* cho ``MyNode`` exported property sẽ lọc danh sách node trong scene để phù hợp với giới hạn gán.

.. code-block:: csharp

    public partial class Main : Node
    {
        [Export]
        public MyNode MyNode { get; set; }
    }

.. image:: img/globalclasses_exportednode.webp

Nếu một custom type chưa được đăng ký thành lớp global, việc gán sẽ bị giới hạn ở Godot type mà custom type đó dựa trên. Ví dụ: các phép gán trong inspector cho một export thuộc type ``MySimpleSprite2D`` sẽ bị giới hạn ở ``Sprite2D`` và các type dẫn xuất.

.. code-block:: csharp

    public partial class MySimpleSprite2D : Sprite2D
    {
    }

Khi được kết hợp với ``[GlobalClass]`` attribute, ``[Icon]`` attribute cho phép cung cấp đường dẫn đến một icon để hiển thị khi lớp được hiển thị trong editor.

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

Lớp ``Stats`` là một custom resource được đăng ký thành lớp global. :ref:`Việc export các property <doc_c_sharp_exports>` thuộc type ``Stats`` sẽ chỉ cho phép gán các instance của resource type này, đồng thời inspector sẽ cho phép bạn dễ dàng tạo và tải các instance của type này.

.. image:: img/globalclasses_exportedproperty1.webp

.. image:: img/globalclasses_exportedproperty2.webp

.. warning::

    Editor của Godot sẽ ẩn các custom class có tên bắt đầu bằng tiền tố "Editor" trong các cửa sổ hộp thoại "Create New Node" hoặc "Create New Scene". Các class này vẫn có thể được khởi tạo tại runtime thông qua tên class, nhưng sẽ được các cửa sổ editor tự động ẩn đi cùng với các editor node tích hợp được editor của Godot sử dụng.
