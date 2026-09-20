.. _doc_c_sharp_features:

Các tính năng của ngôn ngữ C#
=============================

Trang này cung cấp tổng quan về các tính năng thường được sử dụng của cả C# và Godot, cũng như cách sử dụng chúng cùng nhau.

.. _doc_c_sharp_features_type_conversion_and_casting:

Chuyển đổi và ép kiểu
---------------------

C# là một ngôn ngữ có kiểu tĩnh. Do đó, bạn không thể thực hiện như sau:

.. code-block:: csharp

    var mySprite = GetNode("MySprite");
    mySprite.SetFrame(0);

Phương thức ``GetNode()`` trả về một instance ``Node``. Bạn phải chuyển đổi rõ ràng nó sang kiểu dẫn xuất mong muốn, trong trường hợp này là ``Sprite2D``.

Đối với việc này, bạn có một số tùy chọn trong C#.

**Ép kiểu và kiểm tra kiểu**

Ném ra ``InvalidCastException`` nếu node được trả về không thể ép kiểu thành Sprite2D. Bạn sẽ sử dụng nó thay cho toán tử ``as`` nếu khá chắc chắn rằng nó sẽ không thất bại.

.. code-block:: csharp

    Sprite2D mySprite = (Sprite2D)GetNode("MySprite");
    mySprite.SetFrame(0);

**Sử dụng toán tử AS**

Toán tử ``as`` trả về ``null`` nếu node không thể được ép kiểu thành Sprite2D, và vì lý do đó, nó không thể được sử dụng với các kiểu giá trị.

.. code-block:: csharp

    Sprite2D mySprite = GetNode("MySprite") as Sprite2D;
    // Chỉ gọi SetFrame() nếu mySprite không phải là null
    mySprite?.SetFrame(0);

**Sử dụng các phương thức generic**

Các phương thức generic cũng được cung cấp để giúp việc chuyển đổi kiểu này trở nên trong suốt.

``GetNode<T>()`` ép kiểu node trước khi trả về nó. Nó sẽ ném ra một ``InvalidCastException`` nếu node không thể được ép kiểu thành kiểu mong muốn.

.. code-block:: csharp

    Sprite2D mySprite = GetNode<Sprite2D>("MySprite");
    mySprite.SetFrame(0);

``GetNodeOrNull<T>()`` sử dụng toán tử ``as`` và sẽ trả về ``null`` nếu node không thể được ép kiểu thành kiểu mong muốn.

.. code-block:: csharp

    Sprite2D mySprite = GetNodeOrNull<Sprite2D>("MySprite");
    // Chỉ gọi SetFrame() nếu mySprite không phải là null
    mySprite?.SetFrame(0);

**Kiểm tra kiểu bằng toán tử IS**

Để kiểm tra xem node có thể được ép kiểu thành Sprite2D hay không, bạn có thể sử dụng toán tử ``is``. Toán tử ``is`` trả về ``false`` nếu node không thể được ép kiểu thành Sprite2D, nếu không thì trả về ``true``. Lưu ý rằng khi toán tử ``is`` được sử dụng với ``null``, kết quả luôn là ``false``.

.. code-block:: csharp

    if (GetNode("MySprite") is Sprite2D)
    {
        // Đúng vậy, đó là một Sprite2D!
    }

    if (null is Sprite2D)
    {
        // Khối này không bao giờ có thể được thực thi.
    }

Bạn cũng có thể khai báo một biến mới để lưu trữ có điều kiện kết quả của phép ép kiểu nếu toán tử ``is`` trả về ``true``.

.. code-block:: csharp

    if (GetNode("MySprite") is Sprite2D mySprite)
    {
        // Biến mySprite chỉ tồn tại bên trong khối này và không bao giờ là null.
        mySprite.SetFrame(0);
    }

Để kiểm tra kiểu nâng cao hơn, bạn có thể tìm hiểu về `Pattern Matching <https://docs.microsoft.com/en-us/dotnet/csharp/pattern-matching>`_.


Các define của preprocessor
---------------------------

Godot có một tập hợp các define cho phép bạn thay đổi mã C# tùy theo môi trường mà bạn biên dịch.

Ví dụ
~~~~~

Ví dụ, bạn có thể thay đổi mã dựa trên nền tảng:

.. code-block:: csharp

        public override void _Ready()
        {
    #if (GODOT_MOBILE || GODOT_WEB)
            // Sử dụng các object đơn giản khi chạy trên những hệ thống kém mạnh hơn.
            SpawnSimpleObjects();
    #else
            SpawnComplexObjects();
    #endif
        }

Hoặc bạn có thể phát hiện engine mà mã của mình đang chạy trong đó, rất hữu ích khi tạo các thư viện đa engine:

.. code-block:: csharp

        public void MyPlatformPrinter()
        {
    #if GODOT
            GD.Print("This is Godot.");
    #elif UNITY_5_3_OR_NEWER
            print("This is Unity.");
    #else
            throw new NotSupportedException("Only Godot and Unity are supported.");
    #endif
        }

Hoặc bạn có thể viết các script nhắm đến nhiều phiên bản Godot và tận dụng những tính năng chỉ có sẵn trên một số phiên bản đó:

.. code-block:: csharp

        public void UseCoolFeature()
        {
    #if GODOT4_3_OR_GREATER || GODOT4_2_2_OR_GREATER
            // Sử dụng CoolFeature, tính năng đã được thêm vào Godot 4.3 và được cherry-pick vào 4.2.2, tại đây.
    #else
            // Sử dụng giải pháp thay thế cho việc thiếu CoolFeature tại đây.
    #endif
        }

Danh sách đầy đủ các define
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``GODOT`` luôn được định nghĩa cho các project Godot.

* ``TOOLS`` được định nghĩa khi build với cấu hình Debug (editor và editor player).

* ``GODOT_REAL_T_IS_DOUBLE`` được định nghĩa khi thuộc tính ``GodotFloat64`` được đặt thành ``true``.

* Một trong các ``GODOT_LINUXBSD``, ``GODOT_WINDOWS``, ``GODOT_OSX``, ``GODOT_ANDROID``, ``GODOT_IOS``, ``GODOT_WEB`` tùy thuộc vào hệ điều hành. Những tên này có thể thay đổi trong tương lai. Chúng được tạo từ phương thức ``get_name()`` của
  :ref:`OS <class_OS>` singleton, but not every possible OS
  phương thức này trả về một hệ điều hành mà Godot với .NET chạy trên đó.

* ``GODOTX``, ``GODOTX_Y``, ``GODOTX_Y_Z``, ``GODOTx_OR_GREATER``, ``GODOTX_y_OR_GREATER``, và ``GODOTX_Y_z_OR_GREATER``, trong đó ``X``, ``Y``, và ``Z`` được thay thế bằng phiên bản major, minor và patch hiện tại của Godot. ``x``, ``y``, và ``z`` được thay thế bằng tất cả các giá trị từ 0 đến số phiên bản hiện tại cho thành phần tương ứng.

  .. note::

    Các define này lần đầu được thêm vào Godot 4.0.4 và 4.1. Các define phiên bản cho những phiên bản trước đó không tồn tại, bất kể phiên bản Godot hiện tại là gì.

  Ví dụ: Godot 4.0.5 định nghĩa ``GODOT4``, ``GODOT4_OR_GREATER``, ``GODOT4_0``, ``GODOT4_0_OR_GREATER``, ``GODOT4_0_5``, ``GODOT4_0_4_OR_GREATER``, và ``GODOT4_0_5_OR_GREATER``. Godot 4.3.2 định nghĩa ``GODOT4``, ``GODOT4_OR_GREATER``, ``GODOT4_3``, ``GODOT4_0_OR_GREATER``, ``GODOT4_1_OR_GREATER``, ``GODOT4_2_OR_GREATER``, ``GODOT4_3_OR_GREATER``, ``GODOT4_3_2``, ``GODOT4_3_0_OR_GREATER``, ``GODOT4_3_1_OR_GREATER``, và ``GODOT4_3_2_OR_GREATER``.

Khi **export**, các define sau cũng có thể được định nghĩa tùy thuộc vào các export feature:

* Một trong các ``GODOT_PC``, ``GODOT_MOBILE``, hoặc ``GODOT_WEB`` tùy thuộc vào loại nền tảng.

* Một trong các ``GODOT_WINDOWS``, ``GODOT_LINUXBSD``, ``GODOT_MACOS``, ``GODOT_ANDROID``, ``GODOT_IOS``, hoặc ``GODOT_WEB`` tùy thuộc vào nền tảng.

Để xem một project ví dụ, hãy xem OS testing demo: https://github.com/godotengine/godot-demo-projects/tree/master/misc/os_test
