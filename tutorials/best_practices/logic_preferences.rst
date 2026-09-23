.. _doc_logic_preferences:

Tùy chọn logic
==============

Bạn từng tự hỏi nên tiếp cận vấn đề X bằng chiến lược Y hay Z chưa? Bài viết này đề cập đến nhiều chủ đề liên quan đến những tình huống khó xử đó.

Thêm node và thay đổi thuộc tính: việc nào trước?
-------------------------------------------------

Khi khởi tạo các node từ một script trong runtime, bạn có thể cần thay đổi các thuộc tính như tên hoặc vị trí của node. Một tình huống khó xử thường gặp là: khi nào bạn nên thay đổi các giá trị đó?

Cách làm tốt nhất là thay đổi các giá trị trên node trước khi thêm node vào scene tree. Setter của một số thuộc tính có mã để cập nhật các giá trị tương ứng khác, và mã đó có thể chạy chậm! Trong hầu hết trường hợp, mã này không ảnh hưởng đến hiệu năng game, nhưng trong các trường hợp sử dụng nhiều như procedural generation, nó có thể khiến game chạy chậm đến mức gần như không thể chơi được.

Vì những lý do này, thông thường bạn nên đặt các giá trị ban đầu của một node trước khi thêm node đó vào scene tree. Có một số trường hợp ngoại lệ mà các giá trị *không thể* được thiết lập trước khi node được thêm vào scene tree, chẳng hạn như khi đặt vị trí toàn cục.

Loading và preloading
---------------------

Trong GDScript, có
Phương thức :ref:`preload <class_@GDScript_method_preload>`. Phương thức này tải các resource sớm nhất có thể để thực hiện trước các thao tác "loading" và tránh tải resource khi đang ở giữa đoạn mã nhạy cảm về hiệu năng.

Phương thức tương ứng của nó, phương thức :ref:`load <class_@GDScript_method_load>`, chỉ tải một resource khi thực thi đến câu lệnh load. Nghĩa là, nó sẽ tải resource ngay tại vị trí đó, điều này có thể gây chậm khi xảy ra ở giữa các quy trình nhạy cảm. Hàm ``load()`` cũng là bí danh của
:ref:`ResourceLoader.load(path) <class_ResourceLoader_method_load>`, mà *tất cả* các ngôn ngữ scripting đều có thể truy cập.

Vậy chính xác thì preloading xảy ra khi nào so với loading, và khi nào nên dùng mỗi cách? Hãy xem một ví dụ:

.. tabs::
  .. code-tab:: gdscript GDScript

    # my_buildings.gd
    extends Node

    # Lưu ý rằng các script/scene constant có quy ước đặt tên khác với
    # các biến thể property của chúng.

    # Đây là một constant, vì vậy nó được tạo khi đối tượng Script được tải.
    # Script đang preload giá trị này. Ưu điểm ở đây là editor
    # có thể cung cấp tính năng autocompletion vì đây phải là một static path.
    const BuildingScn = preload("res://building.tscn")

    # 1. Script preload giá trị này, vì vậy nó sẽ được tải dưới dạng dependency
    #    của tệp script 'my_buildings.gd'. Tuy nhiên, vì đây là một
    #    property thay vì constant, object sẽ không sao chép resource
    #    PackedScene đã preload vào property cho đến khi script khởi tạo
    #    bằng .new().
    #
    # 2. Giá trị đã preload không thể được truy cập chỉ từ đối tượng Script. Vì
    #    vậy, việc preload giá trị ở đây thực tế không đem lại lợi ích nào.
    #
    # 3. Vì người dùng export giá trị này, nếu script này được lưu trên
    #    một node trong tệp scene, mã khởi tạo scene sẽ ghi đè
    #    giá trị ban đầu đã preload dù sao đi nữa (lãng phí giá trị đó). Thông thường tốt hơn là
    #    cung cấp `null`, giá trị rỗng hoặc giá trị mặc định không hợp lệ khác cho các export.
    #
    # 4. Việc khởi tạo riêng script bằng .new() sẽ kích hoạt
    #    `load("office.tscn")`, bỏ qua mọi giá trị được đặt thông qua export.
    @export var a_building : PackedScene = preload("office.tscn")

    # Ôi không! Điều này gây ra lỗi!
    # Các constant phải được gán giá trị constant. Vì `load` thực hiện một
    # lần tra cứu runtime theo bản chất của nó, ta không thể dùng nó để khởi tạo một
    # constant.
    const OfficeScn = load("res://office.tscn")

    # Tải thành công và chỉ tải khi khởi tạo script! Tuyệt!
    var office_scn = load("res://office.tscn")

  .. code-tab:: csharp

    using Godot;

    // C# và các ngôn ngữ khác không có khái niệm "preloading".
    public partial class MyBuildings : Node
    {
        //Đây là một field chỉ đọc, chỉ có thể được gán khi khai báo hoặc trong constructor.
        public readonly PackedScene Building = ResourceLoader.Load<PackedScene>("res://building.tscn");

        public PackedScene ABuilding;

        public override void _Ready()
        {
            // Có thể gán giá trị trong quá trình khởi tạo.
            ABuilding = GD.Load<PackedScene>("res://Office.tscn");
        }
    }

  .. code-tab:: cpp C++

    using namespace godot;

    class MyBuildings : public Node {
        GDCLASS(MyBuildings, Node)

    public:
        const Ref<PackedScene> building = ResourceLoader::get_singleton()->load("res://building.tscn");
        Ref<PackedScene> a_building;

        virtual void _ready() override {
            // Có thể gán giá trị trong quá trình khởi tạo.
            a_building = ResourceLoader::get_singleton()->load("res://office.tscn");
        }
    };

Preloading cho phép script xử lý toàn bộ việc tải ngay khi script được tải. Preloading hữu ích, nhưng cũng có những lúc bạn không muốn sử dụng nó. Dưới đây là một số điểm cần cân nhắc khi xác định nên dùng cách nào:

1. Nếu không thể xác định khi nào script có thể được tải, việc preload một resource (đặc biệt là scene hoặc script) có thể dẫn đến những lần tải bổ sung mà bạn không lường trước. Điều này có thể gây ra thời gian tải biến thiên, không chủ ý, bên cạnh các thao tác tải ban đầu của script.

2. Nếu một thứ khác có thể thay thế giá trị đó (chẳng hạn như việc khởi tạo export của scene), thì việc preload giá trị này không có ý nghĩa. Điểm này không phải là yếu tố đáng kể nếu bạn dự định luôn tự khởi tạo script.

3. Nếu chỉ muốn 'import' một class resource khác (script hoặc scene), thì sử dụng một constant đã preload thường là lựa chọn tốt nhất. Tuy nhiên, trong một số trường hợp đặc biệt, bạn có thể không muốn làm vậy:

   1. Nếu class được 'import' có khả năng thay đổi, thì nó nên là một property, được khởi tạo bằng ``@export`` hoặc ``load()`` (và thậm chí có thể không được khởi tạo cho đến khi cần).

   2. Nếu script yêu cầu rất nhiều dependency và không muốn tiêu tốn quá nhiều bộ nhớ, bạn có thể muốn load và unload các dependency khác nhau trong runtime khi hoàn cảnh thay đổi. Nếu preload các resource vào các constant, cách duy nhất để unload các resource này là unload toàn bộ script. Nếu thay vào đó load chúng dưới dạng property, bạn có thể đặt các property này thành ``null`` và xóa mọi tham chiếu đến resource (vì đây là một
      :ref:`RefCounted <class_RefCounted>`-extending type, sẽ khiến các resource tự xóa khỏi bộ nhớ).

Level lớn: tĩnh và động
-----------------------

Nếu đang tạo một level lớn, những trường hợp nào là phù hợp nhất? Tạo level dưới dạng một không gian tĩnh duy nhất có tốt hơn không? Hay load level thành từng phần và dịch chuyển nội dung của thế giới khi cần sẽ tốt hơn?

Câu trả lời đơn giản là: "khi hiệu năng yêu cầu điều đó". Dilemma gắn với hai lựa chọn này là một trong những quyết định lập trình lâu đời: nên tối ưu bộ nhớ thay vì tốc độ, hay ngược lại?

Câu trả lời ngây thơ là sử dụng một level tĩnh load mọi thứ cùng lúc. Nhưng tùy vào project, cách này có thể tiêu tốn rất nhiều bộ nhớ. Lãng phí RAM của người dùng khiến chương trình chạy chậm hoặc thậm chí crash vì mọi tác vụ khác mà máy tính cố thực hiện cùng lúc.

Dù thế nào, bạn cũng nên chia các scene lớn thành những scene nhỏ hơn (để hỗ trợ tái sử dụng asset). Sau đó, developer có thể thiết kế một node quản lý việc tạo/load và xóa/unload resource cũng như node theo thời gian thực. Các game có môi trường lớn và đa dạng hoặc các thành phần được tạo theo thủ tục thường áp dụng những chiến lược này để tránh lãng phí bộ nhớ.

Mặt khác, việc lập trình một hệ thống động phức tạp hơn; hệ thống này sử dụng nhiều logic được lập trình hơn, từ đó tạo thêm cơ hội xuất hiện lỗi và bug. Nếu không cẩn thận, bạn có thể phát triển một hệ thống làm phình to technical debt của ứng dụng.

Vì vậy, những lựa chọn tốt nhất sẽ là...

1. Sử dụng level tĩnh cho các game nhỏ.

2. Nếu có thời gian/tài nguyên trong một game quy mô vừa/lớn, hãy tạo một library hoặc plugin có thể quản lý node và resource bằng code. Nếu được hoàn thiện theo thời gian để cải thiện khả năng sử dụng và độ ổn định, nó có thể phát triển thành một công cụ đáng tin cậy dùng cho nhiều project.

3. Sử dụng logic động cho game quy mô vừa/lớn nếu bạn có kỹ năng coding nhưng không có thời gian hoặc tài nguyên để hoàn thiện code (phải hoàn thành game). Sau này có thể refactor để tách code ra thành một plugin.

Để xem ví dụ về những cách khác nhau có thể dùng để hoán đổi scene trong runtime, hãy xem tài liệu :ref:`"Thay đổi scene thủ công" <doc_change_scenes_manually>`.
