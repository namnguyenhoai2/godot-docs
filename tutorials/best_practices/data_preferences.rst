:article_outdated: Đúng

.. _doc_data_preferences:

Tùy chọn dữ liệu
================

Bạn từng băn khoăn liệu nên tiếp cận vấn đề X bằng cấu trúc dữ liệu Y hay Z chưa? Bài viết này đề cập đến nhiều chủ đề liên quan đến những tình huống khó lựa chọn đó.

.. note::

    Bài viết này đề cập đến các phép toán có thời gian dạng "[something]-time". Thuật ngữ này bắt nguồn từ `Ký hiệu Big O <https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/>`_ trong việc phân tích thuật toán.

    Nói ngắn gọn, thuật ngữ này mô tả trường hợp xấu nhất về độ dài runtime. Nói theo cách dễ hiểu:

    "Khi kích thước của miền bài toán tăng lên, độ dài runtime của thuật toán..."

    - Thời gian hằng số, ``O(1)``: "...không tăng lên."
    - Thời gian logarit, ``O(log n)``: "...tăng với tốc độ chậm."
    - Thời gian tuyến tính, ``O(n)``: "...tăng với cùng một tốc độ."
    - Vân vân.

    Hãy tưởng tượng phải xử lý 3 triệu điểm dữ liệu trong một khung hình. Không thể xây dựng tính năng bằng thuật toán thời gian tuyến tính, vì kích thước dữ liệu quá lớn sẽ khiến runtime vượt xa khoảng thời gian được cấp. Ngược lại, thuật toán thời gian hằng số có thể xử lý phép toán này mà không gặp vấn đề gì.

    Nhìn chung, các developer muốn tránh thực hiện các phép toán thời gian tuyến tính càng nhiều càng tốt. Tuy nhiên, nếu giữ quy mô của một phép toán thời gian tuyến tính ở mức nhỏ và không cần thực hiện phép toán đó thường xuyên, thì nó có thể chấp nhận được. Cân bằng các yêu cầu này và chọn đúng thuật toán / cấu trúc dữ liệu cho công việc là một phần khiến kỹ năng của programmer trở nên có giá trị.

Array so với Dictionary so với Object
-------------------------------------

Godot lưu trữ tất cả biến trong scripting API bằng
:ref:`lớp Variant <doc_variant_class>`. Variant có thể lưu trữ các cấu trúc dữ liệu tương thích với Variant như
:ref:`Array <class_Array>` và :ref:`Dictionary <class_Dictionary>` cũng như :ref:`Objects <class_Object>`.

Godot triển khai Array dưới dạng một ``Vector<Variant>``. Engine lưu nội dung của Array trong một vùng bộ nhớ liên tiếp, tức là chúng nằm liền kề nhau theo một hàng.

.. note::

    Đối với những người chưa quen với C++, Vector là tên của đối tượng array trong các thư viện C++ truyền thống. Đây là một kiểu "templated", nghĩa là các bản ghi của nó chỉ có thể chứa một kiểu cụ thể (được biểu thị bằng dấu ngoặc nhọn). Ví dụ, một
    :ref:`PackedStringArray <class_PackedStringArray>` sẽ tương tự như một ``Vector<String>``.

Việc lưu trữ trong vùng bộ nhớ liên tiếp dẫn đến hiệu năng của các phép toán như sau:

- **Lặp (Iterate):** Nhanh nhất. Rất phù hợp với các vòng lặp.

    - Phép toán: Tất cả những gì nó làm là tăng một bộ đếm để chuyển đến bản ghi tiếp theo.

- **Chèn, Xóa, Di chuyển (Insert, Erase, Move):** Phụ thuộc vào vị trí. Nhìn chung là chậm.

    - Phép toán: Việc thêm/xóa/di chuyển nội dung bao gồm di chuyển các bản ghi liền kề sang vị trí khác (để tạo chỗ trống / lấp đầy khoảng trống).

    - Thêm/xóa nhanh *ở cuối*.

    - Thêm/xóa chậm *ở một vị trí bất kỳ*.

    - Thêm/xóa chậm nhất *ở đầu*.

    - Nếu thực hiện nhiều lần chèn/xóa *ở đầu*, thì hãy...

        1. đảo ngược array.

        2. thực hiện một vòng lặp áp dụng các thay đổi cho Array *ở cuối*.

        3. đảo ngược array một lần nữa.

      Cách này chỉ tạo 2 bản sao của array (vẫn là thời gian hằng số, nhưng chậm) thay vì sao chép trung bình khoảng 1/2 array N lần (thời gian tuyến tính).

- **Lấy, Gán (Get, Set):** Nhanh nhất *theo vị trí*. Ví dụ, có thể yêu cầu bản ghi thứ 0, thứ 2, thứ 10, v.v., nhưng không thể chỉ định bản ghi cụ thể muốn lấy.

    - Phép toán: 1 phép cộng từ vị trí bắt đầu của array đến chỉ mục mong muốn.

- **Tìm (Find):** Chậm nhất. Xác định chỉ mục/vị trí của một giá trị.

    - Phép toán: Phải lặp qua array và so sánh các giá trị cho đến khi tìm thấy kết quả khớp.

        - Hiệu năng cũng phụ thuộc vào việc có cần tìm kiếm toàn diện hay không.

    - Nếu được giữ theo thứ tự, các phép toán tìm kiếm tùy chỉnh có thể đưa thời gian thực thi về dạng logarit (tương đối nhanh). Tuy nhiên, người dùng phổ thông sẽ không cảm thấy thoải mái với cách này. Cách thực hiện là sắp xếp lại Array sau mỗi lần chỉnh sửa và viết một thuật toán tìm kiếm có nhận biết thứ tự.

Godot triển khai Dictionary dưới dạng một ``HashMap<Variant, Variant, VariantHasher, StringLikeVariantComparator>``. Engine lưu trữ một array nhỏ (được khởi tạo với 2^3 hay 8 bản ghi) gồm các cặp key-value. Khi muốn truy cập một giá trị, người dùng cung cấp cho nó một key. Sau đó, nó *băm (hash)* key, tức là chuyển key thành một số. "Hash" được dùng để tính chỉ mục trong array. Với tư cách là một array, HM sau đó có thể tra cứu nhanh trong "table" gồm các key được ánh xạ tới các value. Khi HashMap trở nên quá đầy, nó tăng lên lũy thừa 2 tiếp theo (16 bản ghi, rồi 32, v.v.) và xây dựng lại cấu trúc.

Hash giúp giảm khả năng xảy ra xung đột key. Nếu xảy ra xung đột, table phải tính lại một chỉ mục khác cho value, có tính đến vị trí trước đó. Nhìn chung, cách này mang lại khả năng truy cập tất cả bản ghi trong thời gian hằng số, đổi lại là tốn thêm bộ nhớ và giảm một phần nhỏ hiệu quả vận hành.

1. Băm mỗi key một số lần tùy ý.

    - Các phép toán hash có thời gian hằng số, vì vậy ngay cả khi một thuật toán phải thực hiện nhiều hơn một phép toán, miễn là số lần tính hash không phụ thuộc quá nhiều vào mật độ của table, mọi thứ vẫn sẽ nhanh. Điều này dẫn đến...

2. Duy trì kích thước ngày càng tăng cho table.

    - HashMap cố ý duy trì các khoảng trống bộ nhớ chưa sử dụng xen kẽ trong table để giảm xung đột hash và duy trì tốc độ truy cập. Đây là lý do kích thước của nó liên tục tăng theo cấp số nhân bằng các lũy thừa của 2.

Như có thể thấy, Dictionary chuyên xử lý những tác vụ mà Array không phù hợp. Tổng quan về chi tiết vận hành của chúng như sau:

- **Lặp (Iterate):** Nhanh.

    - Phép toán: Lặp qua vector hash nội bộ của map. Trả về từng key. Sau đó, người dùng sử dụng key để chuyển đến và trả về value mong muốn.

- **Chèn, Xóa, Di chuyển (Insert, Erase, Move):** Nhanh nhất.

    - Thao tác: Băm khóa đã cho. Thực hiện 1 thao tác cộng để tra cứu giá trị thích hợp (đầu mảng + độ lệch). Di chuyển gồm hai thao tác này (một chèn, một xóa). Map phải thực hiện một số bảo trì để duy trì các khả năng của nó:

        - cập nhật List các bản ghi theo thứ tự.

        - xác định xem mật độ của bảng có buộc phải mở rộng dung lượng bảng hay không.

    - Dictionary ghi nhớ thứ tự người dùng chèn các khóa. Điều này cho phép nó thực hiện các lần lặp đáng tin cậy.

- **Get, Set:** Nhanh nhất. Giống như tra cứu *theo khóa*.

    - Thao tác: Giống như chèn/xóa/di chuyển.

- **Find:** Chậm nhất. Xác định khóa của một giá trị.

    - Thao tác: Phải lặp qua các bản ghi và so sánh giá trị cho đến khi tìm thấy kết quả khớp.

    - Lưu ý rằng Godot không cung cấp tính năng này ngay từ đầu (vì chúng không được dùng cho tác vụ này).

Godot triển khai Objects dưới dạng các vùng chứa dữ liệu ngây ngô nhưng năng động. Objects truy vấn các nguồn dữ liệu khi được đặt câu hỏi. Ví dụ, để trả lời câu hỏi "bạn có thuộc tính tên là 'position' không?", nó có thể hỏi :ref:`script <class_Script>` hoặc :ref:`ClassDB <class_ClassDB>`. Có thể tìm thêm thông tin về Objects là gì và cách chúng hoạt động trong bài viết :ref:`doc_what_are_godot_classes`.

Chi tiết quan trọng ở đây là độ phức tạp của tác vụ Object. Mỗi khi thực hiện một trong các truy vấn đa nguồn này, nó chạy qua *vài* vòng lặp và các lần tra cứu HashMap. Hơn nữa, các truy vấn này là những thao tác có thời gian tuyến tính, phụ thuộc vào kích thước hệ thống phân cấp kế thừa của Object. Nếu class mà Object truy vấn (class hiện tại của nó) không tìm thấy gì, yêu cầu sẽ được chuyển tiếp đến base class tiếp theo, lên tận class Object ban đầu. Mặc dù mỗi thao tác riêng lẻ đều nhanh, việc phải thực hiện quá nhiều lần kiểm tra khiến chúng chậm hơn cả hai phương án còn lại khi tra cứu dữ liệu.

.. note::

  Khi các developer đề cập đến việc scripting API chậm đến mức nào, họ đang nói đến chuỗi truy vấn này. So với mã C++ đã biên dịch, nơi ứng dụng biết chính xác phải đi đâu để tìm bất kỳ thứ gì, việc các thao tác của scripting API mất nhiều thời gian hơn là điều không thể tránh khỏi. Chúng phải xác định nguồn của mọi dữ liệu liên quan trước khi có thể thử truy cập dữ liệu đó.

  Lý do GDScript chậm là vì mọi thao tác nó thực hiện đều đi qua hệ thống này.

  C# có thể xử lý một số nội dung với tốc độ cao hơn nhờ bytecode được tối ưu hóa tốt hơn. Tuy nhiên, nếu script C# gọi đến nội dung của một engine class hoặc cố gắng truy cập thứ gì đó bên ngoài nó, script sẽ đi qua pipeline này.

  NativeScript C++ tiến thêm một bước nữa và mặc định giữ mọi thứ ở bên trong. Các lệnh gọi đến cấu trúc bên ngoài sẽ đi qua scripting API. Trong NativeScript C++, việc đăng ký các method để expose chúng cho scripting API là một tác vụ thủ công. Tại thời điểm này, các class bên ngoài, không phải C++, sẽ sử dụng API để định vị chúng.

Vậy, giả sử ta kế thừa từ Reference để tạo một cấu trúc dữ liệu như Array hoặc Dictionary, tại sao lại chọn Object thay vì một trong hai tùy chọn còn lại?

1. **Kiểm soát:** Objects cho phép tạo ra các cấu trúc tinh vi hơn. Ta có thể xếp các lớp abstraction lên dữ liệu để đảm bảo API bên ngoài không thay đổi khi cấu trúc dữ liệu bên trong thay đổi. Hơn nữa, Objects có thể có signal, cho phép tạo ra hành vi phản ứng.

2. **Tính rõ ràng:** Objects là nguồn dữ liệu đáng tin cậy đối với dữ liệu mà scripts và engine classes định nghĩa cho chúng. Các thuộc tính có thể không chứa những giá trị ta mong đợi, nhưng ta không cần lo lắng liệu thuộc tính đó có tồn tại ngay từ đầu hay không.

3. **Tính tiện lợi:** Nếu đã hình dung một cấu trúc dữ liệu tương tự, việc kế thừa từ một class hiện có sẽ giúp nhiệm vụ xây dựng cấu trúc dữ liệu dễ dàng hơn nhiều. Ngược lại, Arrays và Dictionaries không đáp ứng mọi trường hợp sử dụng có thể có.

Objects cũng cho người dùng cơ hội tạo ra các cấu trúc dữ liệu chuyên biệt hơn nữa. Với chúng, ta có thể thiết kế List, Binary Search Tree, Heap, Splay Tree, Graph, Disjoint Set của riêng mình cùng vô số tùy chọn khác.

"Tại sao không dùng Node cho các cấu trúc cây?" có thể bạn sẽ hỏi. Vâng, class Node chứa những thứ không liên quan đến cấu trúc dữ liệu tùy chỉnh của bạn. Vì vậy, việc xây dựng kiểu node riêng có thể hữu ích khi xây dựng các cấu trúc cây.

.. tabs::
  .. code-tab:: gdscript GDScript

    class_name TreeNode
    extends Object

    var _parent: TreeNode = null
    var _children := []

    func _notification(p_what):
        match p_what:
            NOTIFICATION_PREDELETE:
                # Bộ hủy.
                for a_child in _children:
                    a_child.free()

  .. code-tab:: csharp

    using Godot;
    using System.Collections.Generic;

    // Có thể quyết định sau này có expose getter/setter cho các thuộc tính hay không
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

Từ đây, ta có thể tạo các cấu trúc của riêng mình với những tính năng cụ thể, chỉ bị giới hạn bởi trí tưởng tượng.

Enumeration: int so với string
------------------------------

Hầu hết các ngôn ngữ đều cung cấp tùy chọn kiểu enumeration. GDScript cũng không khác, nhưng không giống hầu hết các ngôn ngữ khác, nó cho phép sử dụng số nguyên hoặc chuỗi làm giá trị enum (loại sau chỉ khi sử dụng annotation ``@export_enum`` trong GDScript). Khi đó nảy sinh câu hỏi: "nên dùng loại nào?"

Câu trả lời ngắn gọn là: "loại nào khiến bạn thấy thoải mái hơn thì dùng loại đó." Đây là một tính năng riêng của GDScript chứ không phải của Godot scripting nói chung; ngôn ngữ này ưu tiên tính dễ sử dụng hơn hiệu năng.

Ở cấp độ kỹ thuật, phép so sánh số nguyên (thời gian hằng số) sẽ nhanh hơn phép so sánh chuỗi (thời gian tuyến tính). Tuy nhiên, nếu muốn tuân theo quy ước của các ngôn ngữ khác thì nên dùng số nguyên.

Vấn đề chính khi sử dụng số nguyên xuất hiện lúc muốn *in* một giá trị enum. Với số nguyên, việc cố gắng in ``MY_ENUM`` sẽ in ``5`` hoặc một giá trị tương tự, thay vì thứ gì đó như ``"MyEnum"``. Để in một enum số nguyên, ta phải viết một Dictionary ánh xạ giá trị chuỗi tương ứng cho từng enum.

Nếu mục đích chính của việc sử dụng enum là in các giá trị và muốn nhóm chúng thành các khái niệm có liên quan, thì việc dùng chúng dưới dạng chuỗi là hợp lý. Nhờ đó, không cần một cấu trúc dữ liệu riêng để thực hiện việc in.

AnimatedTexture so với AnimatedSprite2D so với AnimationPlayer so với AnimationTree
-----------------------------------------------------------------------------------

Trong những trường hợp nào nên sử dụng từng class animation của Godot? Câu trả lời có thể không ngay lập tức rõ ràng với người dùng Godot mới.

:ref:`AnimatedTexture <class_AnimatedTexture>` là một texture mà engine vẽ dưới dạng một vòng lặp animation thay vì một hình ảnh tĩnh. Người dùng có thể điều chỉnh...

1. tốc độ nó di chuyển qua từng phần của texture (FPS).

2. số lượng vùng nằm trong texture (frame).

:ref:`RenderingServer <class_RenderingServer>` của Godot sau đó sẽ lần lượt vẽ các vùng theo tốc độ đã định. Tin tốt là engine không cần thực hiện thêm logic nào. Tin xấu là người dùng có rất ít quyền kiểm soát.

Cũng lưu ý rằng AnimatedTexture là một :ref:`Resource <class_Resource>` khác với các đối tượng :ref:`Node <class_Node>` khác được thảo luận ở đây. Ta có thể tạo một node :ref:`Sprite2D <class_Sprite2D>` sử dụng AnimatedTexture làm texture. Hoặc (điều mà các đối tượng còn lại không thể làm) ta có thể thêm các AnimatedTexture làm tile trong một :ref:`TileSet <class_TileSet>` và tích hợp nó với một
:ref:`TileMapLayer <class_TileMapLayer>` cho nhiều background tự động animate, tất cả đều được render trong một lần gọi draw theo lô.

Node :ref:`AnimatedSprite2D <class_AnimatedSprite2D>`, khi kết hợp với
resource :ref:`SpriteFrames <class_SpriteFrames>`, cho phép tạo nhiều chuỗi animation khác nhau thông qua spritesheet, chuyển đổi giữa các animation, cũng như kiểm soát tốc độ, độ lệch vùng và hướng của chúng. Vì vậy, chúng đặc biệt phù hợp để điều khiển các animation 2D dựa trên frame.

Nếu cần kích hoạt các hiệu ứng khác liên quan đến những thay đổi trong animation (ví dụ: tạo hiệu ứng particle, gọi các hàm hoặc điều khiển những thành phần ngoại vi khác ngoài animation dựa trên frame), thì cần sử dụng một node :ref:`AnimationPlayer <class_AnimationPlayer>` cùng với AnimatedSprite2D.

AnimationPlayer cũng là công cụ cần dùng nếu muốn thiết kế các hệ thống animation 2D phức tạp hơn, chẳng hạn như...

1. **Animation cắt ghép:** chỉnh sửa transform của các sprite tại runtime.

2. **Animation mesh 2D:** xác định một vùng cho texture của sprite và rig một skeleton cho vùng đó. Sau đó, animate các bone để kéo giãn và uốn cong texture theo tỷ lệ tương ứng với mối quan hệ giữa các bone.

3. Kết hợp các phương pháp trên.

Mặc dù cần một AnimationPlayer để thiết kế từng chuỗi animation riêng lẻ cho game, AnimationPlayer cũng có thể hữu ích khi kết hợp các animation để blending, tức là cho phép chuyển tiếp mượt mà giữa các animation này. Ngoài ra, các animation được lập kế hoạch cho object có thể có cấu trúc phân cấp. Đây là những trường hợp mà :ref:`AnimationTree <class_AnimationTree>` phát huy thế mạnh. Xem :ref:`hướng dẫn chuyên sâu về cách sử dụng AnimationTree <doc_animation_tree>` để biết thêm chi tiết.

.. _`Big O Notation`: https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/
