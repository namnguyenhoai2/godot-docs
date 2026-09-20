.. _doc_c_sharp_styleguide:

Hướng dẫn về phong cách C#
==========================

Việc có các quy ước viết mã được xác định rõ ràng và nhất quán là điều quan trọng đối với mọi dự án, và Godot cũng không ngoại lệ.

Trang này chứa hướng dẫn về phong cách viết mã được các nhà phát triển và cộng tác viên của chính Godot tuân theo. Vì vậy, hướng dẫn này chủ yếu dành cho những người muốn đóng góp cho dự án, nhưng vì các quy ước và hướng dẫn được đề cập trong bài viết này là những quy ước được người dùng ngôn ngữ áp dụng rộng rãi nhất, chúng tôi khuyến khích bạn cũng làm như vậy, đặc biệt nếu bạn chưa có hướng dẫn tương tự.

.. note:: This article is by no means an exhaustive guide on how to follow the standard coding
        các quy ước hoặc phương pháp hay nhất. Nếu bạn không chắc chắn về một khía cạnh không được đề cập ở đây, hãy tham khảo tài liệu toàn diện hơn, chẳng hạn như `C# Coding Conventions <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions>`_ hoặc `Framework Design Guidelines <https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines>`_.

Đặc tả ngôn ngữ
---------------

Hiện tại Godot sử dụng **C# phiên bản 12.0** trong engine và mã nguồn ví dụ, vì đây là phiên bản được .NET 8.0 hỗ trợ (yêu cầu cơ sở hiện tại). Do đó, trước khi chuyển sang phiên bản mới hơn, cần cẩn thận để tránh sử dụng lẫn các tính năng ngôn ngữ chỉ có trong C# 13.0 trở lên.

Để biết thông tin chi tiết về các tính năng C# trong những phiên bản khác nhau, hãy xem `What's New in C# <https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/>`_.

Định dạng
---------

Hướng dẫn chung
~~~~~~~~~~~~~~~

* Sử dụng ký tự line feed (**LF**) để ngắt dòng, không sử dụng CRLF hoặc CR. * Sử dụng một ký tự line feed ở cuối mỗi tệp, ngoại trừ các tệp `csproj`. * Sử dụng encoding **UTF-8** không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`_. * Sử dụng **4 khoảng trắng** thay cho tab để thụt lề (được gọi là "soft tabs"). * Cân nhắc chia một dòng thành nhiều dòng nếu dòng đó dài hơn 100 ký tự.


Ngắt dòng và dòng trống
~~~~~~~~~~~~~~~~~~~~~~~

Đối với quy tắc thụt lề chung, hãy làm theo `the "Allman Style" <https://en.wikipedia.org/wiki/Indentation_style#Allman_style>`_, trong đó khuyến nghị đặt dấu ngoặc nhọn liên kết với một câu lệnh điều khiển ở dòng tiếp theo, được thụt lề cùng cấp:

.. code-block:: csharp

    // Sử dụng phong cách này:
    if (x > 0)
    {
        DoSomething();
    }

    // KHÔNG sử dụng phong cách này:
    if (x > 0) {
        DoSomething();
    }

Tuy nhiên, bạn có thể chọn bỏ qua ngắt dòng bên trong các dấu ngoặc:

* Đối với các accessor của property đơn giản. * Đối với các initializer của object, array hoặc collection đơn giản. * Đối với các khai báo abstract auto property, indexer hoặc event.

.. code-block:: csharp

    // Bạn có thể đặt các dấu ngoặc trên cùng một dòng trong các trường hợp sau:
    public interface MyInterface
    {
        int MyProperty { get; set; }
    }

    public class MyClass : ParentClass
    {
        public int Value
        {
            get { return 0; }
            set
            {
                ArrayValue = new [] {value};
            }
        }
    }

Chèn một dòng trống:

* Sau một danh sách các câu lệnh ``using``. * Giữa các khai báo method, property và inner type. * Ở cuối mỗi tệp.

Các khai báo field và constant có thể được nhóm lại với nhau theo mức độ liên quan. Trong trường hợp đó, hãy cân nhắc chèn một dòng trống giữa các nhóm để dễ đọc hơn.

Tránh chèn một dòng trống:

* Sau ``{``, dấu ngoặc nhọn mở. * Trước ``}``, dấu ngoặc nhọn đóng. * Sau một khối comment hoặc một comment một dòng. * Liền kề với một dòng trống khác.

.. code-block:: csharp

    using System;
    using Godot;
                                              // Dòng trống sau danh sách `using`.
    public class MyClass
    {                                         // Không có dòng trống sau `{`.
        public enum MyEnum
        {
            Value,
            AnotherValue                      // Không có dòng trống trước `}`.
        }
                                              // Dòng trống xung quanh inner type.
        public const int SomeConstant = 1;
        public const int AnotherConstant = 2;

        private Vector3 _x;                  // Các constant hoặc field liên quan có thể được
        private Vector3 _y;                  // nhóm lại với nhau.

        private float _width;
        private float _height;

        public int MyProperty { get; set; }
                                              // Dòng trống xung quanh property.
        public void MyMethod()
        {
            // Một comment nào đó.
            AnotherMethod();                  // Không có dòng trống sau comment.
        }
                                              // Dòng trống xung quanh method.
        public void AnotherMethod()
        {
        }
    }


Sử dụng khoảng trắng
~~~~~~~~~~~~~~~~~~~~

Chèn một khoảng trắng:

* Xung quanh toán tử nhị phân và toán tử ba ngôi. * Giữa dấu ngoặc đơn mở và ``if``, ``for``, ``foreach``, ``catch``, ``while``, ``lock`` hoặc các keyword ``using``. * Trước và bên trong một accessor block một dòng. * Giữa các accessor trong một accessor block một dòng. * Sau dấu phẩy không nằm ở cuối dòng. * Sau dấu chấm phẩy trong câu lệnh ``for``. * Sau dấu hai chấm trong câu lệnh ``case`` một dòng. * Xung quanh dấu hai chấm trong khai báo type. * Xung quanh mũi tên lambda. * Sau ký hiệu comment một dòng (``//``), và trước ký hiệu đó nếu được dùng ở cuối dòng. * Sau dấu ngoặc nhọn mở và trước dấu ngoặc nhọn đóng trong một initializer một dòng.

Không sử dụng khoảng trắng:

* Sau dấu ngoặc của phép ép kiểu.

Ví dụ sau đây minh họa cách sử dụng khoảng trắng đúng theo một số quy ước được đề cập ở trên:

.. code-block:: csharp

    public class MyClass<A, B> : Parent<A, B>
    {
        public float MyProperty { get; set; }

        public float AnotherProperty
        {
            get { return MyProperty; }
        }

        public void MyMethod()
        {
            int[] values = { 1, 2, 3, 4 };
            int sum = 0;

            // Comment một dòng.
            for (int i = 0; i < values.Length; i++)
            {
                switch (i)
                {
                    case 3: return;
                    default:
                        sum += i > 2 ? 0 : 1;
                        break;
                }
            }

            i += (int)MyProperty; // Không có khoảng trắng sau phép ép kiểu.
        }
    }

Quy ước đặt tên
---------------

Sử dụng **PascalCase** cho tất cả namespace, tên type và identifier ở cấp member (tức là method, property, constant, event), ngoại trừ private field:

.. code-block:: csharp

    namespace ExampleProject
    {
        public class PlayerCharacter
        {
            public const float DefaultSpeed = 10f;

            public float CurrentSpeed { get; set; }

            protected int HitPoints;

            private void CalculateWeaponDamage()
            {
            }
        }
    }

Sử dụng **camelCase** cho tất cả identifier còn lại (tức là local variable, tham số method), và sử dụng dấu gạch dưới (``_``) làm tiền tố cho private field (nhưng không dùng cho method hoặc property, như đã giải thích ở trên):

.. code-block:: csharp

    private Vector3 _aimingAt; // Sử dụng tiền tố `_` cho private field.

    private void Attack(float attackStrength)
    {
        Enemy targetFound = FindTarget(_aimingAt);

        targetFound?.Hit(attackStrength);
    }

Có một ngoại lệ đối với các acronym gồm hai chữ cái, chẳng hạn như ``UI``, vốn phải được viết bằng chữ in hoa ở nơi PascalCase được sử dụng, và bằng chữ thường trong các trường hợp khác.

Lưu ý rằng ``id`` **không phải** là một acronym, vì vậy nó phải được xử lý như một identifier thông thường:

.. code-block:: csharp

    public string Id { get; }

    public UIManager UI
    {
        get { return uiManager; }
    }

Nhìn chung, không nên sử dụng tên type làm tiền tố của một identifier, chẳng hạn như ``string strText`` hoặc ``float fPower``. Tuy nhiên, có một ngoại lệ dành cho interface: chúng **nên** có một chữ cái in hoa ``I`` làm tiền tố trong tên, chẳng hạn như ``IInventoryHolder`` hoặc ``IDamageable``.

Cuối cùng, hãy cân nhắc chọn những tên mang tính mô tả và đừng cố rút ngắn chúng quá nhiều nếu điều đó ảnh hưởng đến khả năng đọc.

Ví dụ, nếu bạn muốn viết mã để tìm một kẻ địch ở gần và tấn công nó bằng vũ khí, hãy ưu tiên:

.. code-block:: csharp

    FindNearbyEnemy()?.Damage(weaponDamage);

Thay vì:

.. code-block:: csharp

    FindNode()?.Change(wpnDmg);

Member variable
---------------

Đừng khai báo member variable nếu chúng chỉ được sử dụng cục bộ trong một method, vì điều đó khiến mã khó theo dõi hơn. Thay vào đó, hãy khai báo chúng dưới dạng local variable trong phần thân của method.

Local variable
--------------

Khai báo local variable gần nhất có thể với lần sử dụng đầu tiên của nó. Điều này giúp dễ theo dõi mã hơn mà không phải cuộn quá nhiều để tìm nơi variable được khai báo.

Local variable được định kiểu ngầm
----------------------------------

Cân nhắc sử dụng định kiểu ngầm (``var``) khi khai báo local variable, nhưng **chỉ khi type có thể được suy ra rõ ràng** từ phía bên phải của phép gán:

.. code-block:: csharp

    // Bạn có thể sử dụng `var` trong các trường hợp sau:

    var direction = new Vector2(1, 0);

    var value = (int)speed;

    var text = "Some value";

    for (var i = 0; i < 10; i++)
    {
    }

    // Nhưng không sử dụng cho các trường hợp sau:

    var value = GetValue();

    var velocity = direction * 1.5;

    // Nhìn chung, sử dụng định kiểu tường minh cho các giá trị số là một ý hay hơn, đặc biệt khi có
    // alias `real_t` trong Godot, có thể là double hoặc float
    // tùy thuộc vào cấu hình build.

    var value = 1.5;

Các lưu ý khác
--------------

 * Use explicit access modifiers. * Use properties instead of non-private fields. * Use modifiers in this order: ``public``/``protected``/``private``/``internal``/``virtual``/``override``/``abstract``/``new``/``static``/``readonly``. * Avoid using fully-qualified names or ``this.`` prefix for members when it's not necessary. * Remove unused ``using`` statements and unnecessary parentheses. * Consider omitting the default initial value for a type. * Consider using null-conditional operators or type initializers to make the code more compact. * Use safe cast when there is a possibility of the value being a different type, and use direct cast otherwise.
