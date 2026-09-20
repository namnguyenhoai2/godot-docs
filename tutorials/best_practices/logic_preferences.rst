.. _doc_logic_preferences:

Tùy chọn logic
==============

Bạn có từng tự hỏi liệu nên tiếp cận vấn đề X bằng chiến lược Y hay Z không? Bài viết này đề cập đến nhiều chủ đề liên quan đến những tình huống khó xử này.

Thêm node và thay đổi thuộc tính: việc nào trước?
-------------------------------------------------

Khi khởi tạo node từ một script trong runtime, bạn có thể cần thay đổi các thuộc tính như tên hoặc vị trí của node. Một tình huống khó xử thường gặp là: khi nào nên thay đổi các giá trị đó?

Cách làm tốt nhất là thay đổi các giá trị trên node trước khi thêm nó vào scene tree. Setter của một số thuộc tính có code để cập nhật các giá trị tương ứng khác, và code đó có thể chạy chậm! Trong hầu hết trường hợp, code này không ảnh hưởng đến hiệu năng game, nhưng trong các trường hợp sử dụng nhiều như procedural generation, nó có thể khiến game chạy chậm đến mức gần như không thể chơi được.

Vì những lý do này, thông thường cách làm tốt nhất là đặt các giá trị ban đầu của node trước khi thêm nó vào scene tree. Có một số trường hợp ngoại lệ mà các giá trị *không thể* được đặt trước khi thêm node vào scene tree, chẳng hạn như đặt global position.

Loading và preloading
---------------------

Trong GDScript, có global
:ref:`preload <class_@GDScript_method_preload>` method. It loads resources as
sớm nhất có thể để đưa các thao tác "loading" lên trước và tránh loading resource khi đang ở giữa đoạn code nhạy cảm về hiệu năng.

Phương thức :ref:`load <class_@GDScript_method_load>` tương ứng của nó chỉ load resource khi thực thi đến câu lệnh load. Nói cách khác, nó sẽ load resource tại chỗ, điều này có thể gây chậm khi xảy ra ở giữa các quy trình nhạy cảm. Hàm ``load()`` cũng là một bí danh của
:ref:`ResourceLoader.load(path) <class_ResourceLoader_method_load>` which is
có thể được truy cập bởi *tất cả* các ngôn ngữ scripting.

Vậy chính xác thì preloading xảy ra khi nào so với loading, và khi nào nên sử dụng từng cách? Hãy xem một ví dụ:

.. tabs::
  .. code-tab:: gdscript GDScript

    # my_buildings.gd
    extends Node

    # Note how constant scripts/scenes have a different naming scheme than
    # các biến thể thuộc tính của chúng.

    # Giá trị này là một hằng số, vì vậy nó được khởi tạo khi đối tượng Script được load.
    # Script đang preload giá trị này. Ưu điểm ở đây là editor
    # có thể cung cấp tính năng tự động hoàn thành vì đường dẫn phải là đường dẫn tĩnh.
    const BuildingScn = preload("res://building.tscn")

    # 1. Script preload giá trị này, vì vậy nó sẽ được load như một dependency
    # của file script 'my_buildings.gd'. Tuy nhiên, vì đây là một
    # property chứ không phải constant, object sẽ không sao chép
    # resource PackedScene đã preload vào property cho đến khi script được khởi tạo
    # bằng .new().
    #
    # 2. Giá trị đã preload không thể được truy cập chỉ từ Script object. Vì
    # vậy, việc preload giá trị ở đây thực sự không mang lại lợi ích nào.
    #
    # 3. Vì người dùng export giá trị này, nếu script này được lưu trên
    # một node trong file scene, code khởi tạo scene sẽ ghi đè lên
    # giá trị ban đầu đã preload dù sao đi nữa (khiến giá trị đó bị lãng phí). Thông thường tốt hơn là
    # cung cấp giá trị mặc định là `null`, rỗng hoặc không hợp lệ theo cách khác cho các export.
    #
    # 4. Việc khởi tạo riêng script bằng .new() sẽ kích hoạt
    # `load("office.tscn")`, bỏ qua mọi giá trị được đặt thông qua export.
    @export var a_building : PackedScene = preload("office.tscn")

    # Ôi không! Điều này gây ra lỗi!
    # Phải gán các giá trị hằng số cho các constant. Vì `load` thực hiện một
    # tra cứu trong runtime theo bản chất của nó, nên không thể dùng nó để khởi tạo một
    # constant.
    const OfficeScn = load("res://office.tscn")

    # Load thành công và chỉ load khi khởi tạo script! Tuyệt!
    var office_scn = load("res://office.tscn")

  .. code-tab:: csharp

    using Godot;

    // C# và các ngôn ngữ khác không có khái niệm "preloading".
    public partial class MyBuildings : Node
    {
        //Đây là một trường chỉ đọc, chỉ có thể được gán khi khai báo hoặc trong constructor.
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

Preloading cho phép script xử lý toàn bộ việc loading ngay khi script được load. Preloading rất hữu ích, nhưng cũng có những lúc bạn không muốn sử dụng nó. Dưới đây là một số điều cần cân nhắc khi quyết định sử dụng cách nào:

1. Nếu không thể xác định khi nào script có thể được load, thì việc preload một resource (đặc biệt là scene hoặc script) có thể dẫn đến những lần load bổ sung mà bạn không dự tính. Điều này có thể tạo ra thời gian load thay đổi ngoài ý muốn, kéo dài thêm bên cạnh các thao tác load ban đầu của script.

2. Nếu một thứ khác có thể thay thế giá trị đó (chẳng hạn như việc khởi tạo exported của một scene), thì việc preload giá trị không có ý nghĩa. Điểm này không phải là yếu tố quan trọng nếu bạn dự định luôn tự khởi tạo script.

3. Nếu chỉ muốn 'import' một class resource khác (script hoặc scene), thì sử dụng một constant đã preload thường là lựa chọn tốt nhất. Tuy nhiên, trong những trường hợp đặc biệt, bạn có thể không muốn làm vậy:

   1. Nếu class được 'import' có khả năng thay đổi, thì thay vào đó nó nên là một property, được khởi tạo bằng ``@export`` hoặc ``load()`` (và thậm chí có thể chưa được khởi tạo cho đến sau này).

   2. Nếu script yêu cầu rất nhiều dependency và bạn không muốn tiêu tốn quá nhiều memory, thì bạn có thể muốn load và unload nhiều dependency khác nhau trong runtime khi hoàn cảnh thay đổi. Nếu preload resource vào các constant, thì cách duy nhất để unload các resource này là unload toàn bộ script. Ngược lại, nếu chúng được load dưới dạng property, bạn có thể đặt các property này thành ``null`` và xóa mọi reference đến resource (điều này, như một
      :ref:`RefCounted <class_RefCounted>`-extending type, will cause the
      cách để xóa chúng khỏi memory).

Level lớn: tĩnh và động
-----------------------

Nếu đang tạo một level lớn, trường hợp nào là phù hợp nhất? Tạo level dưới dạng một không gian tĩnh có tốt hơn không? Hay nên load level thành từng phần và dịch chuyển nội dung của world khi cần?

Câu trả lời đơn giản là: "khi hiệu năng yêu cầu điều đó." Tình huống khó xử liên quan đến hai lựa chọn này là một trong những lựa chọn lập trình lâu đời: tối ưu memory hay tốc độ, hoặc ngược lại?

Câu trả lời ngây thơ là sử dụng một level tĩnh load mọi thứ cùng lúc. Tuy nhiên, tùy thuộc vào project, cách này có thể tiêu tốn một lượng memory lớn. Lãng phí RAM của người dùng khiến chương trình chạy chậm hoặc thậm chí bị crash vì mọi việc khác mà máy tính cố thực hiện cùng lúc.

Dù thế nào đi nữa, bạn nên chia các scene lớn thành những scene nhỏ hơn (để hỗ trợ khả năng tái sử dụng asset). Sau đó, developer có thể thiết kế một node quản lý việc tạo/load và xóa/unload resource cũng như node theo thời gian thực. Các game có môi trường lớn và đa dạng hoặc các thành phần được tạo bằng procedural generation thường triển khai những chiến lược này để tránh lãng phí memory.

Mặt khác, việc viết code cho một hệ thống dynamic phức tạp hơn; nó sử dụng nhiều logic được lập trình hơn, từ đó tạo thêm cơ hội phát sinh lỗi và bug. Nếu không cẩn thận, bạn có thể phát triển một hệ thống làm phình to technical debt của ứng dụng.

Vì vậy, các lựa chọn tốt nhất sẽ là...

1. Sử dụng level tĩnh cho các game nhỏ.

2. Nếu có thời gian/tài nguyên trong một game cỡ vừa/lớn, hãy tạo một library hoặc plugin có thể quản lý node và resource bằng code. Nếu được tinh chỉnh theo thời gian để cải thiện tính dễ sử dụng và độ ổn định, nó có thể phát triển thành một tool đáng tin cậy cho nhiều project.

3. Sử dụng logic dynamic cho một game cỡ vừa/lớn vì bạn có kỹ năng coding nhưng không có thời gian hoặc tài nguyên để tinh chỉnh code (phải hoàn thành game). Sau này có thể refactor để chuyển code ra một plugin.

Để xem ví dụ về nhiều cách khác nhau có thể swap scene trong runtime, vui lòng xem tài liệu :ref:`"Change scenes manually" <doc_change_scenes_manually>`.
