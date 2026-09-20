.. _doc_c_sharp_variant:

Biến thể C#
===========

Để xem phần giải thích chi tiết về Variant nói chung, hãy xem trang tài liệu :ref:`Variant <class_Variant>`.

``Godot.Variant`` được dùng để biểu diễn kiểu :ref:`Variant <class_Variant>` gốc của Godot. Bất kỳ
:ref:`Variant-compatible type <c_sharp_variant_compatible_types>` can be converted from/to it.
Chúng tôi khuyến nghị tránh sử dụng ``Godot.Variant`` trừ khi cần tương tác với các engine API không định kiểu. Hãy tận dụng tính an toàn kiểu của C# khi có thể.

Có thể chuyển đổi từ một kiểu C# tương thích với Variant sang ``Godot.Variant`` bằng các phép chuyển đổi ngầm định. Ngoài ra còn có các overload phương thức ``CreateFrom`` và các phương thức generic ``Variant.From<T>``. Chỉ khác nhau về cú pháp: hành vi là như nhau.

.. code-block:: csharp

    int x = 42;
    Variant numberVariant = x;
    Variant helloVariant = "Hello, World!";

    Variant numberVariant2 = Variant.CreateFrom(x);
    Variant numberVariant3 = Variant.From(x);

Các phép chuyển đổi ngầm định sang ``Godot.Variant`` giúp việc truyền các variant làm đối số phương thức trở nên rất thuận tiện. Ví dụ, đối số thứ ba của :ref:`tween_property<class_Tween_method_tween_property>`, dùng để chỉ định màu cuối của tween, là một ``Godot.Variant``.

.. code-block:: csharp

    Tween tween = CreateTween();
    tween.TweenProperty(GetNode("Sprite"), "modulate", Colors.Red, 1.0f);

Có thể chuyển đổi từ ``Godot.Variant`` sang một kiểu C# bằng các phép chuyển đổi tường minh. Ngoài ra còn có các phương thức ``Variant.As{TYPE}`` và phương thức generic ``Variant.As<T>``. Tất cả đều có cùng hành vi.

.. code-block:: csharp

    int number = (int)numberVariant;
    string hello = (string)helloVariant;

    int number2 = numberVariant.As<int>();
    int number3 = numberVariant.AsInt32();

.. note::

    Các phương thức ``Variant.As{TYPE}`` thường được đặt tên theo các kiểu C# (``Int32``), không phải theo các từ khóa C# (``int``).

Nếu kiểu Variant không khớp với kiểu đích của phép chuyển đổi, hệ quả sẽ khác nhau tùy thuộc vào các giá trị nguồn và đích.

- Phép chuyển đổi có thể kiểm tra giá trị và trả về một giá trị tương tự nhưng có khả năng không như mong đợi của kiểu đích. Ví dụ, chuỗi ``"42a"`` có thể được chuyển đổi thành số nguyên ``42``. - Giá trị mặc định của kiểu đích có thể được trả về. - Một mảng rỗng có thể được trả về. - Một exception có thể được ném ra.

Chuyển đổi sang đúng kiểu sẽ tránh được hành vi phức tạp và nên được ưu tiên.

Thuộc tính ``Variant.Obj`` trả về một ``object`` C# với giá trị chính xác cho mọi variant. Điều này có thể hữu ích khi hoàn toàn không biết kiểu của Variant. Tuy nhiên, khi có thể, hãy ưu tiên các phép chuyển đổi cụ thể hơn. ``Variant.Obj`` đánh giá một ``switch`` trên ``Variant.VariantType`` và việc này có thể không cần thiết. Ngoài ra, nếu kết quả là một value type, nó sẽ được boxed.

Ví dụ, nếu không thể chấp nhận khả năng ``Variant.As<MyNode>()`` ném ra invalid cast exception, hãy cân nhắc sử dụng type pattern ``Variant.As<GodotObject>() is MyNode n`` thay thế.

.. note::

    Vì kiểu Variant trong C# là một struct nên nó không thể là null. Để tạo một Variant "null", hãy sử dụng từ khóa ``default`` hoặc constructor không tham số ``Godot.Variant``.

.. _c_sharp_variant_compatible_types:

Các kiểu tương thích với Variant
--------------------------------

Một kiểu tương thích với Variant có thể được chuyển đổi sang và từ một ``Godot.Variant``. Các kiểu C# sau tương thích với Variant:

* Tất cả `built-in value types <https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/built-in-types-table>`_, ngoại trừ ``decimal``, ``nint`` và ``nuint``. * ``string``. * Các class kế thừa từ :ref:`GodotObject <class_Object>`. * Các kiểu collection được định nghĩa trong namespace ``Godot.Collections``.

Danh sách đầy đủ các kiểu Variant và kiểu C# tương ứng:

=======================  ===========================================================
Variant.Type             C# Type
=======================  ===========================================================
``Nil``                  ``null`` (Not a type)
``Bool``                 ``bool``
``Int``                  ``long`` (Godot stores 64-bit integers in Variant)
``Float``                ``double`` (Godot stores 64-bit floats in Variant)
``String``               ``string``
``Vector2``              ``Godot.Vector2``
``Vector2I``             ``Godot.Vector2I``
``Rect2``                ``Godot.Rect2``
``Rect2I``               ``Godot.Rect2I``
``Vector3``              ``Godot.Vector3``
``Vector3I``             ``Godot.Vector3I``
``Transform2D``          ``Godot.Transform2D``
``Vector4``              ``Godot.Vector4``
``Vector4I``             ``Godot.Vector4I``
``Plane``                ``Godot.Plane``
``Quaternion``           ``Godot.Quaternion``
``Aabb``                 ``Godot.Aabb``
``Basis``                ``Godot.Basis``
``Transform3D``          ``Godot.Transform3D``
``Projection``           ``Godot.Projection``
``Color``                ``Godot.Color``
``StringName``           ``Godot.StringName``
``NodePath``             ``Godot.NodePath``
``Rid``                  ``Godot.Rid``
``Object``               ``Godot.GodotObject`` or any derived type.
``Callable``             ``Godot.Callable``
``Signal``               ``Godot.Signal``
``Dictionary``           ``Godot.Collections.Dictionary``
``Array``                ``Godot.Collections.Array``
``PackedByteArray``      ``byte[]``
``PackedInt32Array``     ``int[]``
``PackedInt64Array``     ``long[]``
``PackedFloat32Array``   ``float[]``
``PackedFloat64Array``   ``double[]``
``PackedStringArray``    ``string[]``
``PackedVector2Array``   ``Godot.Vector2[]``
``PackedVector3Array``   ``Godot.Vector3[]``
``PackedVector4Array``   ``Godot.Vector4[]``
``PackedColorArray``     ``Godot.Color[]``
=======================  ===========================================================

.. warning::

    Godot sử dụng số nguyên và số thực 64-bit trong Variant. Các kiểu số nguyên và số thực nhỏ hơn như ``int``, ``short`` và ``float`` vẫn được hỗ trợ vì chúng có thể chứa vừa trong kiểu lớn hơn. Lưu ý rằng khi thực hiện chuyển đổi, việc sử dụng sai kiểu có thể dẫn đến mất độ chính xác.

.. warning::

    Enum được ``Godot.Variant`` hỗ trợ vì kiểu nền của chúng là kiểu số nguyên và tất cả các kiểu số nguyên đều tương thích. Tuy nhiên, các phép chuyển đổi ngầm định không tồn tại; enum phải được chuyển đổi thủ công sang kiểu số nguyên nền trước khi có thể chuyển đổi sang/từ ``Godot.Variant``, hoặc sử dụng các phương thức generic ``Variant.As<T>`` và ``Variant.From<T>`` để chuyển đổi chúng.

    .. code-block:: csharp

        enum MyEnum { A, B, C }

        Variant variant1 = (int)MyEnum.A;
        MyEnum enum1 = (MyEnum)(int)variant1;

        Variant variant2 = Variant.From(MyEnum.A);
        MyEnum enum2 = variant2.As<MyEnum>();

Sử dụng Variant trong ngữ cảnh generic
--------------------------------------

Khi sử dụng generic, bạn có thể muốn giới hạn kiểu generic ``T`` chỉ còn một trong các kiểu tương thích với Variant. Có thể thực hiện điều này bằng attribute ``[MustBeVariant]``.

.. code-block:: csharp

    public void MethodThatOnlySupportsVariants<[MustBeVariant] T>(T onlyVariant)
    {
        // Thực hiện một thao tác với giá trị tương thích với Variant.
    }

Kết hợp với generic ``Variant.From<T>``, điều này cho phép bạn lấy một instance của ``Godot.Variant`` từ một instance của kiểu generic ``T``. Sau đó, nó có thể được sử dụng trong bất kỳ API nào chỉ hỗ trợ struct ``Godot.Variant``.

.. code-block:: csharp

    public void Method1<[MustBeVariant] T>(T variantCompatible)
    {
        Variant variant = Variant.From(variantCompatible);
        Method2(variant);
    }

    public void Method2(Variant variant)
    {
        // Thực hiện một thao tác với variant.
    }

Để gọi một phương thức có tham số generic được chú thích bằng attribute ``[MustBeVariant]``, giá trị phải là một kiểu tương thích với Variant hoặc một kiểu generic ``T`` cũng được chú thích bằng attribute ``[MustBeVariant]``.

.. code-block:: csharp

    public class ObjectDerivedClass : GodotObject { }

    public class NonObjectDerivedClass { }

    public void Main<[MustBeVariant] T1, T2>(T1 someGeneric1, T2 someGeneric2)
    {
        MyMethod(42); // Hoạt động vì `int` là một kiểu tương thích với Variant.
        MyMethod(new ObjectDerivedClass()); // Hoạt động vì mọi kiểu kế thừa từ `GodotObject` đều là kiểu tương thích với Variant.
        MyMethod(new NonObjectDerivedClass()); // KHÔNG hoạt động vì kiểu này không tương thích với Variant.
        MyMethod(someGeneric1); // Hoạt động vì `T1` được chú thích bằng attribute `[MustBeVariant]`.
        MyMethod(someGeneric2); // KHÔNG hoạt động vì `T2` KHÔNG được chú thích bằng attribute `[MustBeVariant]`.
    }

    public void MyMethod<[MustBeVariant] T>(T variant)
    {
        // Thực hiện một thao tác với variant.
    }
