.. _doc_c_sharp_styleguide:

Hướng dẫn quy ước viết mã C#
============================

Việc có các quy ước viết mã được xác định rõ ràng và nhất quán rất quan trọng đối với mọi dự án, và Godot cũng không ngoại lệ.

Trang này chứa hướng dẫn về phong cách viết mã được các nhà phát triển và cộng tác viên của chính Godot tuân theo. Vì vậy, tài liệu này chủ yếu dành cho những người muốn đóng góp cho dự án. Tuy nhiên, vì các quy ước và hướng dẫn được đề cập trong bài viết này là những quy ước được người dùng ngôn ngữ áp dụng rộng rãi nhất, chúng tôi khuyến khích bạn cũng làm như vậy, đặc biệt nếu bạn chưa có hướng dẫn như thế.

.. note:: Bài viết này hoàn toàn không phải là hướng dẫn đầy đủ về cách tuân theo các quy ước viết mã tiêu chuẩn hoặc các best practice. Nếu bạn không chắc chắn về một khía cạnh nào đó chưa được đề cập ở đây, vui lòng tham khảo tài liệu toàn diện hơn, chẳng hạn như `Quy ước viết mã C# <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions>`_ hoặc `Hướng dẫn thiết kế Framework <https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines>`_.

Đặc tả ngôn ngữ
---------------

Hiện tại, Godot sử dụng **C# version 12.0** trong engine và mã nguồn ví dụ, vì đây là phiên bản được .NET 8.0 hỗ trợ (yêu cầu cơ sở hiện tại). Do đó, trước khi chuyển sang phiên bản mới hơn, cần cẩn thận để tránh sử dụng lẫn các tính năng ngôn ngữ chỉ có trong C# 13.0 trở lên.

Để biết thông tin chi tiết về các tính năng của C# trong những phiên bản khác nhau, vui lòng xem `What's New in C# <https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/>`_.

Định dạng
---------

Hướng dẫn chung
~~~~~~~~~~~~~~~

* Sử dụng ký tự line feed (**LF**) để ngắt dòng, không dùng CRLF hoặc CR.
* Sử dụng một ký tự line feed ở cuối mỗi tệp, ngoại trừ các tệp `csproj`.
* Sử dụng encoding **UTF-8** không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`_.
* Sử dụng **4 spaces** thay cho tab để thụt lề (được gọi là "soft tabs").
* Cân nhắc ngắt một dòng thành nhiều dòng nếu dòng đó dài hơn 100 ký tự.


Ngắt dòng và dòng trống
~~~~~~~~~~~~~~~~~~~~~~~

Đối với quy tắc thụt lề chung, hãy tuân theo `"Allman Style" <https://en.wikipedia.org/wiki/Indentation_style#Allman_style>`_, trong đó khuyến nghị đặt dấu ngoặc nhọn đi kèm với câu lệnh điều khiển ở dòng tiếp theo và thụt lề cùng cấp:

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

Tuy nhiên, bạn có thể chọn bỏ ngắt dòng bên trong dấu ngoặc trong các trường hợp sau:

* Đối với các property accessor đơn giản.
* Đối với các object initializer, array initializer hoặc collection initializer đơn giản.
* Đối với các khai báo abstract auto property, indexer hoặc event.

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

* Sau một danh sách các câu lệnh ``using``.
* Giữa các khai báo method, property và inner type.
* Ở cuối mỗi tệp.

Các khai báo field và constant có thể được nhóm lại với nhau tùy theo mức độ liên quan. Trong trường hợp đó, hãy cân nhắc chèn một dòng trống giữa các nhóm để dễ đọc hơn.

Tránh chèn một dòng trống:

* Sau ``{``, dấu ngoặc nhọn mở.
* Trước ``}``, dấu ngoặc nhọn đóng.
* Sau một khối comment hoặc một comment trên một dòng.
* Liền kề với một dòng trống khác.

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

* Xung quanh toán tử binary và ternary.
* Giữa dấu ngoặc mở và các từ khóa ``if``, ``for``, ``foreach``, ``catch``, ``while``, ``lock`` hoặc ``using``.
* Trước và bên trong một accessor block trên một dòng.
* Giữa các accessor trong một accessor block trên một dòng.
* Sau dấu phẩy không nằm ở cuối dòng.
* Sau dấu chấm phẩy trong câu lệnh ``for``.
* Sau dấu hai chấm trong câu lệnh ``case`` trên một dòng.
* Xung quanh dấu hai chấm trong khai báo type.
* Xung quanh lambda arrow.
* Sau ký hiệu comment trên một dòng (``//``), và trước ký hiệu này nếu được dùng ở cuối dòng.
* Sau dấu ngoặc nhọn mở và trước dấu ngoặc nhọn đóng trong initializer trên một dòng.

Không sử dụng khoảng trắng:

* Sau dấu ngoặc của type cast.

Ví dụ sau đây cho thấy cách sử dụng khoảng trắng đúng theo một số quy ước đã đề cập ở trên:

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

            // Comment trên một dòng.
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

            i += (int)MyProperty; // Không có khoảng trắng sau type cast.
        }
    }

Quy ước đặt tên
---------------

Sử dụng **PascalCase** cho tất cả namespace, tên kiểu và các identifier ở cấp member (tức là method, property, constant, event), ngoại trừ các field private:

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

Sử dụng **camelCase** cho tất cả identifier còn lại (tức là biến cục bộ, tham số method), và sử dụng dấu gạch dưới (``_``) làm tiền tố cho các field private (nhưng không dùng cho method hoặc property, như đã giải thích ở trên):

.. code-block:: csharp

    private Vector3 _aimingAt; // // Sử dụng tiền tố `_` cho các field private.

    private void Attack(float attackStrength)
    {
        Enemy targetFound = FindTarget(_aimingAt);

        targetFound?.Hit(attackStrength);
    }

Có một ngoại lệ đối với các từ viết tắt gồm hai chữ cái, chẳng hạn như ``UI``, phải được viết bằng chữ in hoa ở những nơi dự kiến dùng PascalCase và bằng chữ thường ở những nơi khác.

Lưu ý rằng ``id`` **không phải** là một từ viết tắt, vì vậy nó phải được xử lý như một identifier thông thường:

.. code-block:: csharp

    public string Id { get; }

    public UIManager UI
    {
        get { return uiManager; }
    }

Nhìn chung, không nên dùng tên kiểu làm tiền tố của một identifier, chẳng hạn như ``string strText`` hoặc ``float fPower``. Tuy nhiên, có một ngoại lệ dành cho interface, mà trên thực tế **nên** có một chữ cái in hoa ``I`` làm tiền tố cho tên của chúng, chẳng hạn như ``IInventoryHolder`` hoặc ``IDamageable``.

Cuối cùng, hãy cân nhắc chọn các tên mang tính mô tả và đừng cố rút ngắn chúng quá mức nếu điều đó ảnh hưởng đến khả năng đọc.

Ví dụ, nếu bạn muốn viết code để tìm một enemy ở gần và tấn công nó bằng một vũ khí, hãy ưu tiên:

.. code-block:: csharp

    FindNearbyEnemy()?.Damage(weaponDamage);

Thay vì:

.. code-block:: csharp

    FindNode()?.Change(wpnDmg);

Các biến member
---------------

Đừng khai báo các biến member nếu chúng chỉ được sử dụng cục bộ trong một method, vì điều đó khiến code khó theo dõi hơn. Thay vào đó, hãy khai báo chúng dưới dạng biến cục bộ trong phần thân của method.

Các biến cục bộ
---------------

Khai báo các biến cục bộ gần lần sử dụng đầu tiên của chúng nhất có thể. Điều này giúp dễ theo dõi code hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.

Các biến cục bộ được định kiểu ngầm định
----------------------------------------

Hãy cân nhắc sử dụng định kiểu ngầm định (``var``) khi khai báo biến cục bộ, nhưng **chỉ khi kiểu có thể được suy ra rõ ràng** từ vế phải của phép gán:

.. code-block:: csharp

    // // Bạn có thể sử dụng `var` cho các trường hợp sau:

    var direction = new Vector2(1, 0);

    var value = (int)speed;

    var text = "Some value";

    for (var i = 0; i < 10; i++)
    {
    }

    // // Nhưng không sử dụng cho các trường hợp sau:

    var value = GetValue();

    var velocity = direction * 1.5;

    // // Nhìn chung, sử dụng định kiểu tường minh cho các giá trị số là lựa chọn tốt hơn, đặc biệt là khi
    // // có alias `real_t` trong Godot, vốn có thể là double hoặc float
    // // tùy thuộc vào cấu hình build.

    var value = 1.5;

Các cân nhắc khác
-----------------

 * Sử dụng access modifier tường minh.
 * Sử dụng property thay cho các field không phải private.
 * Sử dụng các modifier theo thứ tự này: ``public``/``protected``/``private``/``internal``/``virtual``/``override``/``abstract``/``new``/``static``/``readonly``.
 * Tránh sử dụng tên đầy đủ hoặc tiền tố ``this.`` cho các member khi không cần thiết.
 * Xóa các câu lệnh ``using`` không được sử dụng và các dấu ngoặc đơn không cần thiết.
 * Hãy cân nhắc bỏ qua giá trị khởi tạo mặc định của một kiểu.
 * Hãy cân nhắc sử dụng toán tử null-conditional hoặc type initializer để làm code ngắn gọn hơn.
 * Sử dụng safe cast khi có khả năng giá trị thuộc một kiểu khác, và sử dụng direct cast trong các trường hợp còn lại.

.. _`C# Coding Conventions`: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions
.. _`Framework Design Guidelines`: https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines
.. _`What's New in C#`: https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/
.. _`byte order mark`: https://en.wikipedia.org/wiki/Byte_order_mark
.. _`the "Allman Style"`: https://en.wikipedia.org/wiki/Indentation_style#Allman_style
