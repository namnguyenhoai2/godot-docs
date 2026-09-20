:article_outdated: True

.. _doc_data_preferences:

Tùy chọn dữ liệu
================

Bạn đã bao giờ tự hỏi nên tiếp cận bài toán X bằng cấu trúc dữ liệu Y hay Z chưa? Bài viết này trình bày nhiều chủ đề liên quan đến những vấn đề nan giải đó.

.. note::

    Bài viết này đề cập đến các thao tác "[something]-time". Thuật ngữ này xuất phát từ `Big O Notation <https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/>`_ trong phân tích thuật toán.

    Nói ngắn gọn, nó mô tả trường hợp xấu nhất về thời lượng runtime. Nói theo cách dễ hiểu:

    "Khi kích thước của miền bài toán tăng lên, thời lượng runtime của thuật toán..."

    - Constant-time, ``O(1)``: "...không tăng." - Logarithmic-time, ``O(log n)``: "...tăng với tốc độ chậm." - Linear-time, ``O(n)``: "...tăng với cùng một tốc độ." - Vân vân.

    Hãy thử tưởng tượng phải xử lý 3 triệu điểm dữ liệu trong một frame duy nhất. Sẽ không thể xây dựng tính năng bằng một thuật toán linear-time, vì kích thước dữ liệu quá lớn sẽ khiến runtime tăng vượt xa khoảng thời gian được phân bổ. Ngược lại, sử dụng thuật toán constant-time có thể xử lý thao tác này mà không gặp vấn đề gì.

    Nhìn chung, các developer muốn tránh thực hiện các thao tác linear-time nhiều nhất có thể. Tuy nhiên, nếu giữ quy mô của một thao tác linear-time ở mức nhỏ và không cần thực hiện thao tác đó thường xuyên, thì nó có thể chấp nhận được. Cân bằng các yêu cầu này và chọn đúng thuật toán / cấu trúc dữ liệu cho công việc là một phần khiến kỹ năng của programmer trở nên có giá trị.

Array so với Dictionary so với Object
-------------------------------------

Godot lưu trữ tất cả biến trong scripting API dưới dạng
:ref:`Variant <doc_variant_class>` class.
Variant có thể lưu trữ các cấu trúc dữ liệu tương thích với Variant như
:ref:`Array <class_Array>` and :ref:`Dictionary <class_Dictionary>` as well
dưới dạng :ref:`Objects <class_Object>`.

Godot triển khai Array dưới dạng ``Vector<Variant>``. Engine lưu trữ nội dung của Array trong một vùng bộ nhớ liền kề, tức là chúng nằm nối tiếp nhau trên một hàng.

.. note::

    Đối với những người chưa quen với C++, Vector là tên của đối tượng array trong các thư viện C++ truyền thống. Đây là một kiểu "templated", nghĩa là các record của nó chỉ có thể chứa một kiểu cụ thể (được biểu thị bằng dấu ngoặc nhọn). Ví dụ, một
    :ref:`PackedStringArray <class_PackedStringArray>` would be something like
    một ``Vector<String>``.

Việc lưu trữ trong bộ nhớ liền kề dẫn đến hiệu năng của các thao tác sau:

- **Duyệt:** Nhanh nhất. Rất phù hợp cho các vòng lặp.

    - Thao tác: Tất cả những gì nó làm là tăng một bộ đếm để đi đến record tiếp theo.

- **Chèn, Xóa, Di chuyển:** Phụ thuộc vào vị trí. Nhìn chung là chậm.

    - Thao tác: Việc thêm/xóa/di chuyển nội dung bao gồm việc di chuyển các record liền kề sang vị trí khác (để tạo khoảng trống / lấp đầy khoảng trống).

    - Thêm/xóa *ở cuối* nhanh.

    - Thêm/xóa *tại một vị trí bất kỳ* chậm.

    - Thêm/xóa *ở đầu* chậm nhất.

    - Nếu thực hiện nhiều thao tác chèn/xóa *ở đầu*, thì hãy...

        1. đảo ngược array.

        2. thực hiện một vòng lặp áp dụng các thay đổi cho Array *ở cuối*.

        3. đảo ngược array lại.

      Cách này chỉ tạo 2 bản sao của array (vẫn là constant time, nhưng chậm) thay vì sao chép khoảng 1/2 array trung bình N lần (linear time).

- **Lấy, Gán:** Nhanh nhất *theo vị trí*. Ví dụ, có thể yêu cầu record thứ 0, thứ 2, thứ 10, v.v. nhưng không thể chỉ định record cụ thể mà bạn muốn.

    - Thao tác: 1 thao tác cộng từ vị trí bắt đầu của array đến index mong muốn.

- **Tìm:** Chậm nhất. Xác định index/vị trí của một giá trị.

    - Thao tác: Phải duyệt qua array và so sánh các giá trị cho đến khi tìm thấy giá trị khớp.

        - Hiệu năng cũng phụ thuộc vào việc có cần tìm kiếm toàn diện hay không.

    - Nếu được giữ theo thứ tự, các thao tác tìm kiếm tùy chỉnh có thể đưa nó về logarithmic time (tương đối nhanh). Tuy nhiên, người dùng thông thường sẽ không thấy thoải mái với cách này. Cách thực hiện là sắp xếp lại Array sau mỗi lần chỉnh sửa và viết một thuật toán tìm kiếm có nhận biết thứ tự.

Godot triển khai Dictionary dưới dạng ``HashMap<Variant, Variant, VariantHasher, StringLikeVariantComparator>``. Engine lưu trữ một array nhỏ (được khởi tạo với 2^3 hay 8 record) gồm các cặp key-value. Khi muốn truy cập một giá trị, người dùng cung cấp cho nó một key. Sau đó, nó *hash* key đó, tức là chuyển nó thành một số. "Hash" được dùng để tính index trong array. Với tư cách là một array, HM sau đó có thể tra cứu nhanh trong "table" gồm các key được ánh xạ đến các value. Khi HashMap trở nên quá đầy, nó tăng lên lũy thừa tiếp theo của 2 (16 record, rồi 32, v.v.) và xây dựng lại cấu trúc.

Hash nhằm giảm khả năng xảy ra xung đột key. Nếu xảy ra xung đột, table phải tính lại một index khác cho value, có tính đến vị trí trước đó. Nhìn chung, điều này tạo ra khả năng truy cập constant-time đến mọi record, đánh đổi bằng bộ nhớ và một phần nhỏ hiệu quả vận hành.

1. Hash mỗi key một số lần tùy ý.

    - Các thao tác hash là constant-time, vì vậy ngay cả khi một thuật toán phải thực hiện nhiều hơn một thao tác, miễn là số lần tính hash không trở nên quá phụ thuộc vào mật độ của table thì mọi thứ vẫn sẽ nhanh. Điều này dẫn đến...

2. Duy trì kích thước ngày càng tăng cho table.

    - HashMap cố ý duy trì các khoảng bộ nhớ chưa sử dụng xen kẽ trong table để giảm xung đột hash và duy trì tốc độ truy cập. Đây là lý do kích thước của nó liên tục tăng theo cấp số nhân bằng các lũy thừa của 2.

Có thể thấy, Dictionary chuyên dụng cho những tác vụ mà Array không phù hợp. Tổng quan về chi tiết vận hành của chúng như sau:

- **Duyệt:** Nhanh.

    - Thao tác: Duyệt qua vector hash nội bộ của map. Trả về từng key. Sau đó, người dùng sử dụng key để nhảy đến và trả về value mong muốn.

- **Chèn, Xóa, Di chuyển:** Nhanh nhất.

    - Thao tác: Hash key được cung cấp. Thực hiện 1 thao tác cộng để tra cứu value thích hợp (đầu array + offset). Di chuyển là hai thao tác như vậy (một lần chèn, một lần xóa). Map phải thực hiện một số công việc bảo trì để duy trì các khả năng của nó:

        - cập nhật List record được sắp xếp theo thứ tự.

        - xác định xem mật độ của table có yêu cầu mở rộng dung lượng table hay không.

    - Dictionary ghi nhớ thứ tự mà người dùng đã chèn các key. Điều này cho phép nó thực hiện các lần duyệt đáng tin cậy.

- **Lấy, Gán:** Nhanh nhất. Giống như tra cứu *theo key*.

    - Thao tác: Giống như chèn/xóa/di chuyển.

- **Tìm:** Chậm nhất. Xác định key của một value.

    - Thao tác: Phải duyệt qua các record và so sánh value cho đến khi tìm thấy giá trị khớp.

    - Lưu ý rằng Godot không cung cấp tính năng này out-of-the-box (vì chúng không dành cho tác vụ này).

Godot triển khai Object dưới dạng các container dữ liệu đơn giản nhưng dynamic. Object truy vấn các nguồn dữ liệu khi được đặt câu hỏi. Ví dụ, để trả lời câu hỏi "bạn có property tên là 'position' không?", nó có thể hỏi :ref:`script <class_Script>` hoặc :ref:`ClassDB <class_ClassDB>`. Bạn có thể tìm thêm thông tin về Object là gì và cách chúng hoạt động trong bài viết :ref:`doc_what_are_godot_classes`.

Chi tiết quan trọng ở đây là độ phức tạp của tác vụ mà Object thực hiện. Mỗi khi thực hiện một trong các truy vấn từ nhiều nguồn này, nó chạy qua *một số* vòng lặp duyệt và các lần tra cứu HashMap. Hơn nữa, các truy vấn này là những thao tác linear-time phụ thuộc vào kích thước của hệ thống phân cấp kế thừa của Object. Nếu class mà Object truy vấn (class hiện tại của nó) không tìm thấy gì, yêu cầu sẽ được chuyển tiếp đến base class tiếp theo, cho đến tận class Object ban đầu. Mặc dù mỗi thao tác này đều nhanh khi thực hiện riêng lẻ, việc phải thực hiện quá nhiều lần kiểm tra khiến chúng chậm hơn cả hai lựa chọn còn lại khi tra cứu dữ liệu.

.. note::

  Khi developer đề cập đến việc scripting API chậm như thế nào, họ đang nói đến chuỗi truy vấn này. So với code C++ đã compile, nơi application biết chính xác phải đi đâu để tìm bất kỳ thứ gì, việc các thao tác của scripting API mất nhiều thời gian hơn là điều không thể tránh khỏi. Chúng phải xác định nguồn của mọi dữ liệu liên quan trước khi có thể cố gắng truy cập dữ liệu đó.

  Lý do GDScript chậm là vì mọi thao tác mà nó thực hiện đều đi qua hệ thống này.

  C# có thể xử lý một số nội dung với tốc độ cao hơn nhờ bytecode được tối ưu hóa tốt hơn. Tuy nhiên, nếu script C# gọi đến nội dung của một engine class hoặc cố gắng truy cập thứ gì đó bên ngoài nó, script sẽ đi qua pipeline này.

  NativeScript C++ tiến xa hơn nữa và mặc định giữ mọi thứ ở bên trong. Các lệnh gọi đến cấu trúc bên ngoài sẽ đi qua scripting API. Trong NativeScript C++, việc đăng ký các method để expose chúng cho scripting API là một tác vụ thủ công. Đây là lúc các class bên ngoài, không phải C++, sẽ sử dụng API để định vị chúng.

Vậy, nếu một người kế thừa từ Reference để tạo một cấu trúc dữ liệu, chẳng hạn như Array hoặc Dictionary, tại sao lại chọn Object thay vì hai tùy chọn còn lại?

1. **Kiểm soát:** Với Object, bạn có khả năng tạo ra các cấu trúc tinh vi hơn. Có thể xây dựng các abstraction trên dữ liệu để đảm bảo API bên ngoài không thay đổi khi cấu trúc dữ liệu bên trong thay đổi. Hơn nữa, Object có thể có signal, cho phép tạo ra hành vi reactive.

2. **Tính rõ ràng:** Object là một nguồn dữ liệu đáng tin cậy khi nói đến dữ liệu mà script và engine class định nghĩa cho chúng. Property có thể không chứa các giá trị mà người ta mong đợi, nhưng không cần lo lắng liệu property đó có tồn tại ngay từ đầu hay không.

3. **Sự tiện lợi:** Nếu đã có sẵn một cấu trúc dữ liệu tương tự trong đầu, việc kế thừa từ một class hiện có sẽ giúp công việc xây dựng cấu trúc dữ liệu dễ dàng hơn nhiều. Ngược lại, Array và Dictionary không đáp ứng được mọi trường hợp sử dụng có thể phát sinh.

Object cũng mang đến cho người dùng cơ hội tạo ra những cấu trúc dữ liệu chuyên biệt hơn nữa. Với chúng, ta có thể thiết kế List, Binary Search Tree, Heap, Splay Tree, Graph, Disjoint Set của riêng mình, cùng vô số lựa chọn khác.

"Tại sao không dùng Node cho các cấu trúc cây?" có thể ai đó sẽ hỏi. Vâng, class Node chứa những thành phần không liên quan đến cấu trúc dữ liệu tùy chỉnh của ta. Vì vậy, việc tự xây dựng kiểu node riêng có thể hữu ích khi tạo các cấu trúc cây.

.. tabs::
  .. code-tab:: gdscript GDScript

    class_name TreeNode
    extends Object

    var _parent: TreeNode = null
    var _children := []

    func _notification(p_what):
        match p_what:
            NOTIFICATION_PREDELETE:
                # Destructor.
                for a_child in _children:
                    a_child.free()

  .. code-tab:: csharp

    using Godot;
    using System.Collections.Generic;

    // Có thể quyết định sau có expose getter/setter cho các property hay không
    public partial class TreeNode : GodotObject
    {
        private TreeNode _parent = null;

        private List<TreeNode> _children = [];

        public override void _Notification(int what)
        {
            switch (what)
            {
                case NotificationPredelete:
                    foreach (TreeNode child in _children)
                    {
                        node.Free();
                    }
                    break;
            }
        }
    }

Từ đây, ta có thể tạo ra các cấu trúc của riêng mình với những tính năng cụ thể, chỉ bị giới hạn bởi trí tưởng tượng.

Enumeration: int so với string
------------------------------

Hầu hết các ngôn ngữ đều cung cấp tùy chọn kiểu enumeration. GDScript cũng không ngoại lệ, nhưng khác với hầu hết các ngôn ngữ khác, nó cho phép sử dụng either integer hoặc string cho các giá trị enum (loại sau chỉ khi sử dụng annotation ``@export_enum`` trong GDScript). Khi đó, câu hỏi đặt ra là: "nên dùng loại nào?"

Câu trả lời ngắn gọn là: "loại nào khiến bạn cảm thấy thoải mái hơn." Đây là một tính năng riêng của GDScript chứ không phải của việc scripting trong Godot nói chung; ngôn ngữ này ưu tiên tính dễ sử dụng hơn hiệu năng.

Ở cấp độ kỹ thuật, phép so sánh integer (constant-time) sẽ nhanh hơn phép so sánh string (linear-time). Tuy nhiên, nếu muốn tuân theo quy ước của các ngôn ngữ khác, bạn nên sử dụng integer.

Vấn đề chính khi sử dụng integer xuất hiện lúc muốn *in* một giá trị enum. Với integer, việc cố in ``MY_ENUM`` sẽ in ra ``5`` hoặc một giá trị tương tự, thay vì thứ gì đó như ``"MyEnum"``. Để in một enum integer, ta phải viết một Dictionary ánh xạ giá trị string tương ứng cho mỗi enum.

Nếu mục đích chính của việc sử dụng enum là in các giá trị và muốn nhóm chúng lại thành những khái niệm có liên quan, thì sử dụng chúng dưới dạng string là hợp lý. Nhờ vậy, không cần một cấu trúc dữ liệu riêng để thực hiện việc in.

AnimatedTexture so với AnimatedSprite2D so với AnimationPlayer so với AnimationTree
-----------------------------------------------------------------------------------

Trong những trường hợp nào nên sử dụng từng class animation của Godot? Câu trả lời có thể không ngay lập tức rõ ràng với những người dùng Godot mới.

:ref:`AnimatedTexture <class_AnimatedTexture>` is a texture that
engine sẽ vẽ dưới dạng một vòng lặp animation thay vì một hình ảnh tĩnh. Người dùng có thể thao tác...

1. tốc độ di chuyển qua từng phần của texture (FPS).

2. số lượng region nằm trong texture (frame).

:ref:`RenderingServer <class_RenderingServer>` của Godot sau đó sẽ vẽ các region theo thứ tự với tốc độ đã quy định. Tin tốt là việc này không yêu cầu engine thực hiện thêm logic nào. Tin xấu là người dùng có rất ít quyền kiểm soát.

Cũng lưu ý rằng AnimatedTexture là một :ref:`Resource <class_Resource>`, không giống các object :ref:`Node <class_Node>` khác được thảo luận ở đây. Ta có thể tạo một node :ref:`Sprite2D <class_Sprite2D>` sử dụng AnimatedTexture làm texture. Hoặc (điều mà các loại khác không thể làm) ta có thể thêm AnimatedTexture dưới dạng tile trong một :ref:`TileSet <class_TileSet>` và tích hợp nó với một
:ref:`TileMapLayer <class_TileMapLayer>` for many auto-animating backgrounds that
đều được render trong một draw call được batch duy nhất.

node :ref:`AnimatedSprite2D <class_AnimatedSprite2D>`, kết hợp với
:ref:`SpriteFrames <class_SpriteFrames>` resource, allows one to create a
nhiều animation sequence thông qua spritesheet, chuyển đổi giữa các animation, đồng thời điều khiển speed, regional offset và orientation của chúng. Điều này khiến chúng rất phù hợp để điều khiển các animation 2D dựa trên frame.

Nếu cần kích hoạt các hiệu ứng khác liên quan đến những thay đổi của animation (ví dụ: tạo particle effect, gọi function hoặc thao tác với các thành phần ngoại vi khác ngoài animation dựa trên frame), bạn sẽ cần sử dụng một node :ref:`AnimationPlayer <class_AnimationPlayer>` kết hợp với AnimatedSprite2D.

AnimationPlayer cũng là công cụ cần dùng nếu muốn thiết kế các hệ thống animation 2D phức tạp hơn, chẳng hạn như...

1. **Animation cut-out:** chỉnh sửa transform của sprite tại runtime.

2. **Animation 2D Mesh:** xác định một region cho texture của sprite và rig một skeleton cho nó. Sau đó, ta animate các bone, khiến texture kéo giãn và uốn cong theo tỷ lệ tương ứng với mối quan hệ giữa các bone.

3. Kết hợp các loại trên.

Mặc dù cần một AnimationPlayer để thiết kế từng animation sequence riêng lẻ cho game, công cụ này cũng có thể hữu ích trong việc kết hợp các animation để blending, tức là cho phép chuyển tiếp mượt mà giữa các animation đó. Ngoài ra, giữa các animation được lên kế hoạch cho object của mình có thể tồn tại một cấu trúc phân cấp. Đây là những trường hợp :ref:`AnimationTree <class_AnimationTree>` phát huy hiệu quả. Xem :ref:`in-depth guide on using the AnimationTree <doc_animation_tree>` để biết thêm chi tiết.
