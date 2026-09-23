.. _doc_exporting_pcks:

Xuất các pack, patch và mod
===========================

Các trường hợp sử dụng
----------------------

Thông thường, người dùng muốn bổ sung chức năng cho game của mình sau khi game đã được deploy.

Các ví dụ bao gồm...

- Nội dung có thể tải xuống: khả năng bổ sung tính năng và nội dung cho game.
- Patch: khả năng sửa một lỗi hiện có trong sản phẩm đã phát hành.
- Mod: cho phép người khác tạo nội dung cho game của bạn.

Các công cụ này giúp nhà phát triển tiếp tục mở rộng quá trình phát triển sau bản phát hành ban đầu.

Tổng quan về tệp PCK/ZIP
------------------------

Godot hỗ trợ việc này thông qua một tính năng có tên là **resource packs** (tệp PCK có phần mở rộng ``.pck`` hoặc tệp ZIP).

**Ưu điểm:**

- cập nhật/patch tăng dần
- cung cấp DLC
- hỗ trợ mod
- không cần tiết lộ mã nguồn cho mod
- cấu trúc dự án dạng mô-đun hơn
- người dùng không phải thay thế toàn bộ game

Bước đầu tiên khi sử dụng chúng là export và phân phối dự án cho người chơi. Sau đó, khi muốn bổ sung chức năng hoặc nội dung, bạn chỉ cần phân phối các bản cập nhật cho người dùng thông qua tệp PCK/ZIP.

Tệp PCK/ZIP thường chứa, nhưng không chỉ giới hạn ở:

- script
- scene
- shader
- model
- texture
- hiệu ứng âm thanh
- nhạc
- bất kỳ asset nào khác phù hợp để import vào game

Tệp PCK/ZIP thậm chí có thể là một dự án Godot hoàn toàn khác, được game ban đầu load trong runtime.

Có thể đồng thời load cả tệp PCK và ZIP dưới dạng các pack bổ sung. Xem :ref:`doc_exporting_projects_pck_versus_zip` để so sánh hai định dạng này.

.. seealso::

    Nếu muốn load các tệp rời trong runtime (không được Godot đóng gói trong PCK hoặc ZIP), hãy cân nhắc sử dụng :ref:`doc_runtime_loading_and_saving` thay thế. Cách này hữu ích khi load nội dung do người dùng tạo không được thực hiện bằng Godot, mà không yêu cầu người dùng đóng gói mod của họ theo một định dạng tệp cụ thể.

    Nhược điểm của cách tiếp cận này là nó kém minh bạch hơn đối với logic game, vì không được hưởng cùng cơ chế quản lý resource như tệp PCK/ZIP.

Vấn đề bảo mật
--------------

Điều quan trọng cần lưu ý là việc load tệp PCK cho patch, mod hoặc nội dung bổ sung như bản mở rộng sẽ yêu cầu bạn viết một hệ thống tự động load tệp dựa trên vị trí và có thể cả tên tệp. Đây là một lỗ hổng bảo mật trong ba tình huống. Một là người dùng tải xuống một mod chứa mã độc. Hai là một chương trình độc hại đã tồn tại trên PC của người dùng cuối và thay thế tệp PCK bằng một bản sao độc hại. Ba là bạn phân phối các tệp PCK bản vá thông qua game launcher và hệ thống đã bị xâm nhập.

Hãy cân nhắc điều này khi xác định cách sử dụng tệp PCK trong dự án. Trong các tình huống bạn có hệ thống patch thông qua launcher, hãy cân nhắc sử dụng mật mã bất đối xứng. Bạn có thể lưu khóa công khai trong PCK chính và ký các tệp PCK patch hoặc bản mở rộng bằng khóa riêng tư. Xem class :ref:`class_Crypto` để biết thêm thông tin.

Vấn đề bản quyền
----------------

Nếu muốn sử dụng tệp PCK để phân phối nội dung trả phí bổ sung, chẳng hạn như các bản mở rộng, hãy nhớ rằng Godot không cung cấp sẵn cách ngăn người khác sao chép tệp PCK và đưa tệp đó lên máy tính của người khác. Nếu muốn có bất kỳ hệ thống DRM nào, bạn phải tự triển khai hệ thống đó.

Tạo tệp PCK
-----------

Để đóng gói toàn bộ resource của một dự án vào tệp PCK, hãy mở dự án, đi tới :menu:`Project > Export`, chọn một export preset và nhấp vào
:button:`Export PCK/ZIP`.

.. image:: img/export_pck.webp

Một phương pháp khác là :ref:`export từ command line <doc_command_line_tutorial_exporting>` với ``--export-pack``. Tệp đầu ra phải có phần mở rộng tệp ``.pck`` hoặc ``.zip``. Quá trình export sẽ tạo loại tệp đó cho platform đã chọn.

Tệp PCK bản vá
--------------

Tạo tệp PCK bản vá
~~~~~~~~~~~~~~~~~~

Để tạo một tệp PCK chỉ chứa các resource không có trong bản phát hành ban đầu của dự án, bạn sẽ tạo một tệp PCK bản vá. Tệp này có thể được dùng cho patch, mod hoặc bản mở rộng. Để thực hiện việc này, trước tiên bạn cần có một tệp PCK của dự án tại thời điểm phát hành ban đầu.

Để tạo tệp PCK bản vá, trong menu export và sau khi chọn preset mong muốn, hãy nhấp vào tab :Button:`Patching`. Ở phía dưới là phần :ui:`Base Packs`. Nhấp vào nút :Button:`Add Pack`, sau đó điều hướng đến tệp PCK bạn đã export, tệp này chứa mọi thứ trong dự án tại thời điểm phát hành ban đầu.

Bây giờ, khi export lại tệp PCK của dự án, nếu bạn đã chọn
nút :Button:`Export as Patch`, chỉ những resource đã thay đổi mới được export vào tệp PCK.

Bạn cũng có thể thêm mọi patch đã export vào các pack cơ sở để sử dụng trong tương lai. Ví dụ, việc thêm ``patch.pck`` sẽ đảm bảo rằng ``patch2.pck`` không bao gồm bất kỳ resource nào từ patch đầu tiên đó.

Mã hóa delta
~~~~~~~~~~~~

Có thể giảm kích thước tệp PCK bản vá bằng cách sử dụng mã hóa delta. Cách này chỉ cập nhật những phần của tệp đã thay đổi. Tuy nhiên, nhược điểm là thời gian load các resource được cập nhật sẽ lâu hơn, và mỗi patch của một resource sẽ làm tăng dần thời gian load của resource đó.

Ngoài các bộ lọc, có hai thiết lập cho mã hóa delta:

- **Mức nén mã hóa Delta:** Kiểm soát mức độ nén được áp dụng cho các tệp. Chúng tôi không khuyến nghị đặt cao hơn giá trị mặc định là 19. Vượt quá mức này sẽ cần nhiều bộ nhớ hơn cho quá trình export và import nhưng mức cải thiện thấp hơn đáng kể. Mọi giá trị dương đều có cùng tốc độ giải nén, tuy nhiên export sẽ mất nhiều thời gian hơn khi giá trị càng cao. Các giá trị âm bật chế độ nhanh, nghĩa là tệp lớn hơn nhưng tốc độ giải nén cao hơn.

- **Mức giảm kích thước tối thiểu của Delta Encoding:** Kiểm soát mức dung lượng tối thiểu phải tiết kiệm được để sử dụng compression trên một tệp riêng lẻ. Ví dụ, ở mức 10%, nếu kích thước tệp chỉ có thể giảm 5% thì tệp sẽ không sử dụng delta encoding.

Mức compression mặc định là 19, cũng là mức cao nhất được khuyến nghị.

Để có kích thước patch nhỏ nhất có thể, chúng tôi khuyến nghị tắt compression cho mọi resource mà bạn muốn patch. Ngay cả khi các tệp PCK cơ sở của bạn đã được compressed thì điều đó cũng không gây ra vấn đề.

Có một số nơi có thể tắt compression cho các resource khác nhau:

- Import settings liên quan đến compression trên các resource được import riêng lẻ, chẳng hạn như tệp translation hoặc mô hình 3D
- :ui:`Compress Binary Resources` trong editor settings
- :ui:`GDScript Export Mode` trong tab :button:`Scripts` của export preset

.. Note::

    Sau khi tắt :ui:`Compress Binary Resources`, bạn phải xóa nội dung trong thư mục ``.godot/imported/`` của project, sau đó đóng rồi mở lại project để tạo lại thư mục này.

Điều quan trọng cần lưu ý là khi bạn export một patch được mã hóa delta dựa trên các patch trước đó, các pack mà bạn liệt kê bên dưới :ui:`Base Packs` trong tab :Button:`Patching` phải chính xác là những tệp được game tải khi runtime, theo đúng thứ tự chúng được tải. Việc export lại các phiên bản trước có thể tạo ra kết quả hơi khác do tính không xác định trong quá trình export của Godot, khiến việc patch thất bại. Điều này chỉ áp dụng cho các patch được mã hóa delta; các patch thông thường không gặp vấn đề này.

Mở tệp PCK hoặc ZIP khi runtime
-------------------------------

Để tải tệp PCK hoặc ZIP, bạn sử dụng singleton ProjectSettings. Ví dụ sau giả định có tệp ``mod.pck`` trong thư mục chứa executable của game. Tệp PCK hoặc ZIP chứa một scene kiểm thử ``mod_scene.tscn`` ở thư mục gốc.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _your_function():
        # Điều này có thể thất bại nếu, chẳng hạn, không tìm thấy mod.pck.
        var success = ProjectSettings.load_resource_pack(OS.get_executable_path().get_base_dir().path_join("mod.pck"))

        if success:
            # Bây giờ bạn có thể sử dụng các asset như thể chúng đã có sẵn trong project ngay từ đầu.
            var imported_scene = load("res://mod_scene.tscn")

 .. code-tab:: csharp

    private void YourFunction()
    {
        // Điều này có thể thất bại nếu, chẳng hạn, không tìm thấy mod.pck.
        var success = ProjectSettings.LoadResourcePack(OS.GetExecutablePath().GetBaseDir().PathJoin("mod.pck"));

        if (success)
        {
            // Bây giờ bạn có thể sử dụng các asset như thể chúng đã có sẵn trong project ngay từ đầu.
            var importedScene = (PackedScene)ResourceLoader.Load("res://mod_scene.tscn");
        }
    }

.. warning::

    Theo mặc định, nếu bạn import một tệp có cùng đường dẫn/tên tệp với tệp đã có trong project, tệp được import sẽ thay thế tệp đó. Bạn cần lưu ý điều này khi tạo DLC hoặc mod. Bạn có thể giải quyết vấn đề này bằng cách sử dụng một công cụ cô lập các mod vào một thư mục con mods cụ thể.

    Tuy nhiên, đây cũng là một cách để tạo patch cho chính game của bạn. Một tệp PCK/ZIP kiểu này có thể sửa nội dung của một PCK/ZIP đã được tải trước đó (do đó, thứ tự tải các pack rất quan trọng).

    Để không sử dụng hành vi này, hãy truyền ``false`` làm đối số thứ hai cho
    :ref:`ProjectSettings.load_resource_pack() <class_ProjectSettings_method_load_resource_pack>`.

.. note::

    Đối với một project C#, trước tiên bạn cần build DLL và đặt nó vào thư mục project. Sau đó, trước khi tải resource pack, bạn cần tải DLL của nó như sau: ``Assembly.LoadFile("mod.dll")``

Khắc phục sự cố
~~~~~~~~~~~~~~~

Nếu bạn đang tải một resource pack nhưng không nhận thấy thay đổi nào, có thể là do pack được tải quá muộn. Điều này đặc biệt thường xảy ra với các scene menu có thể preload các scene khác bằng cách sử dụng
:ref:`preload() <class_@GDScript_method_preload>`. Điều này có nghĩa là việc tải một pack trong menu sẽ không ảnh hưởng đến scene khác đã được preload.

Để tránh điều này, bạn cần tải pack sớm nhất có thể. Để thực hiện, hãy tạo một script :ref:`autoload <doc_singletons_autoload>` mới và gọi :ref:`ProjectSettings.load_resource_pack() <class_ProjectSettings_method_load_resource_pack>` trong hàm ``_init()`` của script autoload, thay vì ``_enter_tree()`` hoặc ``_ready()``.

Các lưu ý khi mod
-----------------

Nếu muốn hỗ trợ mod cho game của mình, bạn sẽ cần người dùng tạo các tệp được export tương tự. Với giả định game gốc yêu cầu một cấu trúc nhất định cho các resource của PCK và/hoặc một interface nhất định cho các script, bạn phải thực hiện một trong hai việc sau.

1. Nhà phát triển phải ghi lại các cấu trúc/
    interface dự kiến, yêu cầu modder cài đặt Godot Engine, đồng thời yêu cầu các modder đó tuân theo API được định nghĩa trong tài liệu khi xây dựng nội dung mod cho game (để nội dung hoạt động). Sau đó, người dùng sẽ sử dụng các công cụ export tích hợp sẵn của Godot để tạo tệp PCK như đã trình bày ở trên.
2. Nhà phát triển sử dụng Godot để xây dựng một công cụ GUI nhằm thêm nội dung tuân theo chính xác API của họ
    vào một project. Công cụ Godot này phải chạy trên một bản build của engine có bật tools hoặc có quyền truy cập vào một bản build như vậy (được phân phối kèm theo hoặc có thể nằm trong các tệp của game gốc). Sau đó, công cụ có thể sử dụng executable của Godot để export một tệp PCK từ command line bằng
    :ref:`OS.execute() <class_OS_method_execute>`. Bản thân game không nên sử dụng bản build tools của engine (vì lý do bảo mật), vì vậy tốt nhất nên tách riêng công cụ mod và game.
