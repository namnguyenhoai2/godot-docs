.. _doc_exporting_pcks:

Xuất các pack, patch và mod
===========================

Các trường hợp sử dụng
----------------------

Thông thường, người dùng muốn thêm chức năng cho game của mình sau khi game đã được deploy.

Các ví dụ bao gồm...

- Downloadable Content: khả năng thêm tính năng và nội dung vào game. - Patch: khả năng sửa một bug tồn tại trong sản phẩm đã phát hành. - Mod: cho phép người khác tạo nội dung cho game của mình.

Các công cụ này giúp developer mở rộng quá trình phát triển sau bản phát hành ban đầu.

Tổng quan về file PCK/ZIP
-------------------------

Godot hỗ trợ việc này thông qua một tính năng gọi là **resource pack** (file PCK, có phần mở rộng ``.pck``, hoặc file ZIP).

**Ưu điểm:**

- cập nhật/patch tăng dần - cung cấp DLC - hỗ trợ mod - không cần tiết lộ source code cho mod - cấu trúc project có tính module hơn - người dùng không phải thay thế toàn bộ game

Phần đầu tiên khi sử dụng chúng là export và phân phối project cho người chơi. Sau đó, khi muốn thêm chức năng hoặc nội dung, bạn chỉ cần phân phối các bản cập nhật thông qua file PCK/ZIP cho người dùng.

Các file PCK/ZIP thường chứa, nhưng không chỉ giới hạn ở:

- script - scene - shader - model - texture - hiệu ứng âm thanh - nhạc - mọi asset khác phù hợp để import vào game

Các file PCK/ZIP thậm chí có thể là một project Godot hoàn toàn khác, được game gốc load tại runtime.

Có thể load đồng thời cả file PCK và ZIP dưới dạng các pack bổ sung. Xem :ref:`doc_exporting_projects_pck_versus_zip` để so sánh hai định dạng này.

.. seealso::

    Nếu muốn load các file rời tại runtime (không được đóng gói trong PCK hoặc ZIP bởi Godot), hãy cân nhắc sử dụng :ref:`doc_runtime_loading_and_saving` thay thế. Cách này hữu ích khi load nội dung do người dùng tạo không được thực hiện bằng Godot, mà không yêu cầu người dùng đóng gói mod của họ vào một định dạng file cụ thể.

    Nhược điểm của cách tiếp cận này là nó kém minh bạch hơn đối với logic game, vì không được hưởng cùng cơ chế quản lý resource như file PCK/ZIP.

Các vấn đề về bảo mật
---------------------

Điều quan trọng cần lưu ý là việc load file PCK cho patch, mod hoặc nội dung bổ sung như bản mở rộng sẽ yêu cầu bạn viết code cho một hệ thống tự động load file dựa trên vị trí và có thể cả tên file. Đây là một lỗ hổng bảo mật trong ba trường hợp. Một là người dùng tải xuống một mod chứa code độc hại. Hai là một chương trình độc hại đã tồn tại trên PC của người dùng cuối và thay thế file PCK bằng một bản sao độc hại. Ba là bạn phân phối các file patch PCK thông qua game launcher và hệ thống đã bị xâm nhập.

Hãy cân nhắc điều này khi xác định cách sử dụng file PCK trong một project. Trong trường hợp bạn có hệ thống patch thông qua launcher, hãy cân nhắc sử dụng mật mã bất đối xứng. Bạn có thể lưu public key trong PCK chính và ký các file patch hoặc PCK bản mở rộng bằng private key. Xem class :ref:`class_Crypto` để biết thêm thông tin.

Các vấn đề về bản quyền
-----------------------

Nếu muốn sử dụng file PCK để phân phối nội dung trả phí bổ sung, chẳng hạn như các bản mở rộng, hãy nhớ rằng Godot không cung cấp sẵn cách ngăn người khác sao chép file PCK và đưa nó lên máy tính của người khác. Nếu muốn sử dụng bất kỳ hệ thống DRM nào, bạn phải tự triển khai hệ thống đó.

Tạo file PCK
------------

Để đóng gói toàn bộ resource của một project vào file PCK, hãy mở project và đi tới :menu:`Project > Export`, chọn một export preset và nhấp vào
:button:`Export PCK/ZIP`.

.. image:: img/export_pck.webp

Một phương pháp khác là :ref:`export from the command line <doc_command_line_tutorial_exporting>` với ``--export-pack``. File đầu ra phải có phần mở rộng file ``.pck`` hoặc ``.zip``. Quá trình export sẽ tạo loại file đó cho platform đã chọn.

File PCK patch
--------------

Tạo file PCK patch
~~~~~~~~~~~~~~~~~~

Để tạo một file PCK chỉ chứa các resource không có trong bản phát hành ban đầu của project, bạn sẽ tạo một file PCK patch. File này có thể được sử dụng cho patch, mod hoặc bản mở rộng. Để cách này hoạt động, trước tiên bạn cần có một file PCK cho project tại thời điểm phát hành ban đầu.

Để tạo file PCK patch, trong export menu và với preset mong muốn đã được chọn, hãy nhấp vào tab :Button:`Patching`. Ở phía dưới là phần :ui:`Base Packs`. Nhấp vào nút :Button:`Add Pack`, sau đó điều hướng đến file PCK bạn đã export, file này chứa mọi thứ trong project ở bản phát hành ban đầu.

Bây giờ, khi export lại một file PCK của project, nếu bạn có
:Button:`Export as Patch` button selected, only resources that have changed
sẽ được export trong file PCK.

Bạn cũng có thể thêm mọi patch đã export vào các pack cơ sở để sử dụng sau này. Ví dụ, thêm ``patch.pck`` sẽ đảm bảo rằng ``patch2.pck`` sẽ không bao gồm bất kỳ resource nào từ patch đầu tiên đó.

Delta encoding
~~~~~~~~~~~~~~

File PCK patch có thể được làm nhỏ hơn bằng cách sử dụng delta encoding. Cách này chỉ cập nhật những phần của file đã thay đổi. Tuy nhiên, nó có nhược điểm là làm tăng thời gian load đối với các resource được cập nhật, và mỗi patch của một resource sẽ cộng dồn làm tăng thời gian load của resource đó.

Có hai thiết lập cho delta encoding ngoài các bộ lọc:

- **Delta Encoding Compression Level:** Kiểm soát mức độ nén được áp dụng cho các file. Chúng tôi không khuyến nghị dùng giá trị cao hơn mức mặc định là 19. Vượt quá mức này sẽ cần thêm memory cho việc export và import nhưng chỉ mang lại mức cải thiện rất nhỏ. Mọi giá trị dương đều có cùng tốc độ giải nén, tuy nhiên export sẽ mất nhiều thời gian hơn khi giá trị lớn hơn. Các giá trị âm bật fast mode, nghĩa là file lớn hơn nhưng tốc độ giải nén cao hơn.

- **Delta Encoding Minimum Size Reduction:** Kiểm soát mức giảm kích thước tối thiểu cần đạt được để sử dụng compression cho từng file. Ví dụ, ở mức 10%, nếu kích thước file chỉ có thể giảm 5% thì file sẽ không sử dụng delta encoding.

Mức compression mặc định, 19, là mức cao nhất được khuyến nghị.

Để có kích thước patch nhỏ nhất có thể, chúng tôi khuyến nghị tắt compression cho mọi resource mà bạn muốn patch. Ngay cả khi các file PCK cơ sở đã được nén, điều đó cũng không gây ra vấn đề.

Có một số nơi có thể tắt compression cho các resource khác nhau:

- Các thiết lập import liên quan đến compression trên những resource được import riêng lẻ, chẳng hạn như file translation hoặc model 3D - :ui:`Compress Binary Resources` trong editor settings - :ui:`GDScript Export Mode` trong tab :button:`Scripts` của export preset

.. Note::

    Sau khi tắt :ui:`Compress Binary Resources`, bạn phải xóa nội dung trong thư mục ``.godot/imported/`` của project, sau đó đóng và mở lại project để tạo lại thư mục.

Điều quan trọng cần lưu ý là khi export một patch được mã hóa delta dựa trên các patch trước đó, các pack bạn liệt kê dưới :ui:`Base Packs` trong tab :Button:`Patching` phải chính xác là những file được game load tại runtime, theo đúng thứ tự chúng được load. Việc export lại các phiên bản trước có thể tạo ra kết quả hơi khác do tính không xác định trong quá trình export của Godot, điều này có thể khiến việc patch thất bại. Điều này chỉ áp dụng cho các patch được mã hóa delta; các patch thông thường không gặp vấn đề này.

Mở file PCK hoặc ZIP tại runtime
--------------------------------

Để load file PCK hoặc ZIP, ta sử dụng singleton ProjectSettings. Ví dụ sau giả định có file ``mod.pck`` trong thư mục chứa executable của game. File PCK hoặc ZIP chứa một scene test ``mod_scene.tscn`` ở thư mục gốc.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _your_function():
        # Thao tác này có thể thất bại nếu, chẳng hạn, không tìm thấy mod.pck.
        var success = ProjectSettings.load_resource_pack(OS.get_executable_path().get_base_dir().path_join("mod.pck"))

        if success:
            # Bây giờ bạn có thể sử dụng các asset như thể chúng đã có sẵn trong project ngay từ đầu.
            var imported_scene = load("res://mod_scene.tscn")

 .. code-tab:: csharp

    private void YourFunction()
    {
        // Thao tác này có thể thất bại nếu, chẳng hạn, không tìm thấy mod.pck.
        var success = ProjectSettings.LoadResourcePack(OS.GetExecutablePath().GetBaseDir().PathJoin("mod.pck"));

        if (success)
        {
            // Bây giờ bạn có thể sử dụng các asset như thể chúng đã có sẵn trong project ngay từ đầu.
            var importedScene = (PackedScene)ResourceLoader.Load("res://mod_scene.tscn");
        }
    }

.. warning::

    Theo mặc định, nếu bạn import một file có cùng đường dẫn/tên file với file đã có trong project, file được import sẽ thay thế file đó. Đây là điều cần lưu ý khi tạo DLC hoặc mod. Bạn có thể giải quyết vấn đề này bằng cách sử dụng một công cụ cô lập mod vào một thư mục mod cụ thể.

    Tuy nhiên, đây cũng là một cách để tạo patch cho game của chính bạn. Một file PCK/ZIP dạng này có thể sửa nội dung của một PCK/ZIP đã được load trước đó (do đó, thứ tự load các pack rất quan trọng).

    Để không sử dụng hành vi này, hãy truyền ``false`` làm đối số thứ hai cho
    :ref:`ProjectSettings.load_resource_pack() <class_ProjectSettings_method_load_resource_pack>`.

.. note::

    Đối với project C#, trước tiên bạn cần build DLL và đặt nó vào thư mục project. Sau đó, trước khi load resource pack, bạn cần load DLL của nó như sau: ``Assembly.LoadFile("mod.dll")``

Khắc phục sự cố
~~~~~~~~~~~~~~~

Nếu bạn đang load một resource pack nhưng không nhận thấy thay đổi nào, nguyên nhân có thể là pack được load quá muộn. Điều này đặc biệt xảy ra với các scene menu có thể preload các scene khác bằng cách sử dụng
:ref:`preload() <class_@GDScript_method_preload>`. This means that loading
một pack trong menu sẽ không ảnh hưởng đến scene khác đã được preload.

Để tránh điều này, bạn cần load pack sớm nhất có thể. Để thực hiện, hãy tạo một script :ref:`autoload <doc_singletons_autoload>` mới và gọi :ref:`ProjectSettings.load_resource_pack() <class_ProjectSettings_method_load_resource_pack>` trong hàm ``_init()`` của script autoload, thay vì ``_enter_tree()`` hoặc ``_ready()``.

Các lưu ý khi mod
-----------------

Nếu muốn hỗ trợ mod cho trò chơi của mình, nhà phát triển sẽ cần người dùng tạo các tệp được export tương tự. Giả sử trò chơi gốc yêu cầu một cấu trúc nhất định cho các resource của PCK và/hoặc một interface nhất định cho các script, thì cần thực hiện một trong hai việc sau.

1. Nhà phát triển phải ghi lại tài liệu về các cấu trúc/interface được mong đợi này, yêu cầu modder cài đặt Godot Engine, đồng thời yêu cầu các modder đó tuân thủ API được định nghĩa trong tài liệu khi xây dựng nội dung mod cho trò chơi (để nội dung đó hoạt động). Sau đó, người dùng sẽ sử dụng các công cụ export tích hợp sẵn của Godot để tạo tệp PCK, như đã trình bày ở trên. 2. Nhà phát triển sử dụng Godot để xây dựng một công cụ GUI nhằm thêm nội dung API chính xác của họ vào một project. Công cụ Godot này phải chạy trên một build của engine đã bật tools hoặc có quyền truy cập vào một build như vậy (được phân phối cùng với hoặc có thể nằm trong các tệp của trò chơi gốc). Sau đó, công cụ có thể sử dụng tệp thực thi Godot để export tệp PCK từ command line với
    :ref:`OS.execute() <class_OS_method_execute>`. The game itself shouldn't
    sử dụng một build tools của engine (vì lý do bảo mật), do đó tốt nhất là nên tách riêng công cụ modding và trò chơi.
