:allow_comments: False

.. meta::
    :keywords: FAQ

.. _doc_faq:

Các câu hỏi thường gặp
======================

Tôi có thể làm gì với Godot? Chi phí là bao nhiêu? Các điều khoản cấp phép là gì?
---------------------------------------------------------------------------------

Godot là `Phần mềm miễn phí và mã nguồn mở <https://en.wikipedia.org/wiki/Free_and_open_source_software>`_, được cung cấp theo giấy phép MIT `được OSI phê duyệt <https://opensource.org/licenses/MIT>`_. Điều này có nghĩa là phần mềm miễn phí theo cả nghĩa "tự do ngôn luận" lẫn nghĩa "bia miễn phí".

Tóm lại:

* Bạn được tự do tải xuống và sử dụng Godot cho bất kỳ mục đích nào: cá nhân, phi lợi nhuận, thương mại hoặc mục đích khác.
* Bạn được tự do sửa đổi, phân phối, phân phối lại và remix Godot tùy ý, vì bất kỳ lý do nào, cho cả mục đích phi thương mại và thương mại.

Toàn bộ nội dung của tài liệu đi kèm này được phát hành theo giấy phép Creative Commons Attribution 3.0 (`CC BY 3.0 <https://creativecommons.org/licenses/by/3.0/>`_), với ghi công cho "Juan Linietsky, Ariel Manzur và cộng đồng Godot Engine".

Logo và biểu tượng nhìn chung cũng được áp dụng cùng giấy phép Creative Commons. Lưu ý rằng một số thư viện bên thứ ba đi kèm mã nguồn của Godot có thể có giấy phép khác.

Để xem đầy đủ chi tiết, hãy xem các tệp `COPYRIGHT.txt <https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt>`_, `LICENSE.txt <https://github.com/godotengine/godot/blob/master/LICENSE.txt>`_ và `logo LICENSE.txt <https://github.com/godotengine/godot/blob/master/misc/logo/LICENSE.txt>`_ trong repository Godot.

Ngoài ra, hãy xem `trang giấy phép trên website Godot <https://godotengine.org/license>`_.

Godot hỗ trợ những nền tảng nào?
--------------------------------

**Đối với editor:**

* Windows
* macOS
* Linux, \*BSD
* Android (thử nghiệm)
* `Web <https://editor.godotengine.org/>`__ (thử nghiệm)

**Để export game của bạn:**

* Windows
* macOS
* Linux, \*BSD
* Android
* iOS
* Web

Các binary 32-bit và 64-bit đều được hỗ trợ khi phù hợp, trong đó 64-bit là mặc định. Các bản build macOS chính thức hỗ trợ Apple Silicon nguyên bản cũng như x86_64.

Một số người dùng cũng cho biết họ đã build và sử dụng Godot thành công trên các hệ thống dựa trên ARM chạy Linux, chẳng hạn như Raspberry Pi.

Để biết thông tin về hỗ trợ console, hãy xem `website Godot <https://godotengine.org/consoles/>`__.

Để biết thêm về vấn đề này, hãy xem các phần về :ref:`export <toc-learn-workflow-export>` và :ref:`tự compile Godot <toc-devel-compiling>`.

.. note::

    Godot 3 cũng từng hỗ trợ Universal Windows Platform (UWP). Bản port cho nền tảng này đã bị loại bỏ trong Godot 4 do không được bảo trì và đã bị Microsoft ngừng hỗ trợ. Bản này vẫn có trong bản phát hành ổn định hiện tại của Godot 3 dành cho những người dùng quan tâm.

Godot hỗ trợ những ngôn ngữ lập trình nào?
------------------------------------------

Các ngôn ngữ được Godot chính thức hỗ trợ là GDScript, C# và C++. Xem các danh mục con tương ứng với từng ngôn ngữ trong phần :ref:`scripting <toc-learn-scripting>`.

Nếu bạn mới bắt đầu với Godot hoặc với việc phát triển game nói chung, GDScript là ngôn ngữ được khuyến nghị nên học và sử dụng vì đây là ngôn ngữ native của Godot. Mặc dù các ngôn ngữ scripting thường kém performant hơn các ngôn ngữ cấp thấp về lâu dài, nhưng để prototyping, phát triển Minimum Viable Products (MVP) và tập trung vào Time-To-Market (TTM), GDScript mang lại một cách phát triển game nhanh, thân thiện và đầy đủ năng lực.

Lưu ý rằng hỗ trợ C# vẫn còn tương đối mới, vì vậy bạn có thể gặp một số vấn đề trong quá trình sử dụng. Hiện tại, hỗ trợ C# cũng chưa có trên web
platform. Cộng đồng phát triển thân thiện và chăm chỉ của chúng tôi luôn
sẵn sàng giải quyết các vấn đề mới phát sinh, nhưng vì đây là một dự án mã nguồn mở, chúng tôi khuyến nghị bạn trước hết nên tự tìm hiểu kỹ. Tìm kiếm trong các cuộc thảo luận về `các issue đang mở <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Adotnet>`__ là một cách tuyệt vời để bắt đầu khắc phục sự cố.

Đối với các ngôn ngữ mới, bên thứ ba có thể cung cấp hỗ trợ thông qua GDExtensions. (Xem câu hỏi về plugin bên dưới.) Hiện tại, chẳng hạn, đang có công việc xây dựng các binding không chính thức cho Godot với `Python <https://github.com/touilleMan/godot-python>`_ và `Nim <https://github.com/pragmagic/godot-nim>`_.

.. _doc_faq_what_is_gdscript:

GDScript là gì và tại sao tôi nên sử dụng nó?
---------------------------------------------

GDScript là ngôn ngữ scripting tích hợp của Godot. Nó được xây dựng từ đầu để khai thác tối đa tiềm năng của Godot với lượng code ít nhất, giúp cả developer mới bắt đầu lẫn chuyên gia tận dụng các thế mạnh của Godot nhanh nhất có thể. Nếu bạn từng viết bất kỳ thứ gì bằng một ngôn ngữ như Python, bạn sẽ cảm thấy rất quen thuộc. Để xem các ví dụ và tổng quan đầy đủ về sức mạnh mà GDScript mang lại, hãy xem :ref:`hướng dẫn scripting GDScript <doc_gdscript>`.

Có nhiều lý do để sử dụng GDScript, nhưng lý do nổi bật nhất là **giảm độ phức tạp** tổng thể.

Mục đích ban đầu của việc tạo ra một ngôn ngữ scripting tùy chỉnh được tích hợp chặt chẽ cho Godot có hai phần: thứ nhất, nó giảm thời gian cần thiết để bắt đầu sử dụng Godot, giúp developer nhanh chóng làm quen với engine và tập trung vào năng suất; thứ hai, nó giảm gánh nặng bảo trì tổng thể, thu hẹp phạm vi của các vấn đề và cho phép đội ngũ phát triển engine tập trung vào việc xử lý bug và cải thiện các tính năng liên quan đến phần lõi của engine, thay vì dành nhiều thời gian để làm cho một tập hợp nhỏ các tính năng bổ sung hoạt động trên nhiều ngôn ngữ.

Vì Godot là một dự án mã nguồn mở, ngay từ đầu, việc ưu tiên trải nghiệm tích hợp và liền mạch hơn so với việc thu hút thêm người dùng bằng cách hỗ trợ các ngôn ngữ lập trình quen thuộc hơn là điều cấp thiết, đặc biệt khi việc hỗ trợ những ngôn ngữ quen thuộc hơn đó sẽ dẫn đến trải nghiệm kém hơn. Chúng tôi hiểu nếu bạn muốn sử dụng một ngôn ngữ khác trong Godot (xem danh sách các lựa chọn được hỗ trợ ở trên). Tuy vậy, nếu bạn chưa thử GDScript, hãy thử trong **ba ngày**. Cũng giống như Godot, một khi thấy nó mạnh mẽ đến mức nào và tốc độ phát triển của bạn được cải thiện ra sao, chúng tôi nghĩ bạn sẽ dần yêu thích GDScript.

Bạn có thể tìm thêm thông tin về cách làm quen với GDScript hoặc các ngôn ngữ kiểu động trong :ref:`doc_gdscript_more_efficiently` hướng dẫn.

Động lực nào đã dẫn đến việc tạo ra GDScript?
---------------------------------------------

Trong những ngày đầu, engine sử dụng ngôn ngữ scripting `Lua <https://www.lua.org>`__
language. Lua có thể nhanh nhờ LuaJIT, nhưng việc tạo các binding cho một
hệ thống hướng đối tượng (bằng cách sử dụng fallback) rất phức tạp, chậm và đòi hỏi một lượng code khổng lồ. Sau một số thử nghiệm với `Python <https://www.python.org>`__, chúng tôi nhận thấy ngôn ngữ này cũng khó nhúng.

Những lý do chính để tạo một ngôn ngữ scripting riêng cho Godot là:

1. Hầu hết các script VM đều hỗ trợ threading kém, trong khi Godot sử dụng thread (Lua, Python, Squirrel, JavaScript, ActionScript, v.v.).
2. Hầu hết các script VM đều hỗ trợ mở rộng class kém, và việc điều chỉnh để phù hợp với cách Godot hoạt động rất kém hiệu quả (Lua, Python, JavaScript).
3. Nhiều ngôn ngữ hiện có có interface rất tệ để binding với C++, dẫn đến lượng code lớn, bug, bottleneck và sự kém hiệu quả nói chung (Lua, Python, Squirrel, JavaScript, v.v.). Chúng tôi muốn tập trung vào một engine tuyệt vời, không phải một số lượng lớn tích hợp.
4. Không có kiểu vector native (Vector3, Transform3D, v.v.), dẫn đến hiệu năng suy giảm đáng kể khi sử dụng các kiểu tùy chỉnh (Lua, Python, Squirrel, JavaScript, ActionScript, v.v.).
5. Garbage collector gây ra hiện tượng tạm dừng hoặc việc sử dụng bộ nhớ lớn không cần thiết (Lua, Python, JavaScript, ActionScript, v.v.).
6. Khó tích hợp với code editor để cung cấp tính năng hoàn tất code, chỉnh sửa trực tiếp, v.v. (tất cả các ngôn ngữ).

GDScript được thiết kế để khắc phục các vấn đề trên và nhiều vấn đề khác.

.. _doc_faq_which_programming_language_is_fastest:

Ngôn ngữ lập trình nào nhanh nhất?
----------------------------------

Trong hầu hết các game, bản thân *ngôn ngữ scripting* không phải là nguyên nhân gây ra vấn đề về hiệu năng
problems. Thay vào đó, hiệu năng bị giảm do các thuật toán kém hiệu quả (vốn
chậm trong mọi ngôn ngữ), do hiệu năng GPU hoặc do các code engine C++ phổ biến như physics hoặc navigation. Tất cả các ngôn ngữ được Godot hỗ trợ đều đủ nhanh cho scripting đa mục đích. Bạn nên chọn ngôn ngữ dựa trên các yếu tố khác, chẳng hạn như mức độ dễ sử dụng, độ quen thuộc, khả năng hỗ trợ nền tảng hoặc các tính năng của ngôn ngữ.

Nhìn chung, hiệu năng của C# và GDScript nằm trong cùng một bậc độ lớn, còn C++ nhanh hơn cả hai.

Việc so sánh hiệu năng của GDScript với C# khá phức tạp, vì C# có thể nhanh hơn trong một số trường hợp cụ thể. Bản thân *ngôn ngữ* C# có xu hướng nhanh hơn GDScript, nghĩa là C# có thể nhanh hơn trong những tình huống có ít lời gọi đến code engine Godot. Tuy nhiên, C# có thể chậm hơn GDScript khi thực hiện nhiều lời gọi API Godot, do chi phí *marshalling*. Hiệu năng của C# cũng có thể bị giảm bởi garbage collection, vốn diễn ra tại những thời điểm ngẫu nhiên và không thể dự đoán. Điều này có thể gây ra hiện tượng giật trong các dự án phức tạp và không chỉ xảy ra với Godot.

C++, khi sử dụng :ref:`GDExtension <doc_what_is_gdextension>`, gần như luôn nhanh hơn C# hoặc GDScript. Tuy nhiên, C++ khó sử dụng hơn C# hoặc GDScript và tốc độ phát triển với C++ cũng chậm hơn.

Bạn cũng có thể sử dụng nhiều ngôn ngữ trong cùng một dự án, bằng
:ref:`scripting đa ngôn ngữ <doc_cross_language_scripting>`, hoặc bằng cách sử dụng GDExtension cùng với các ngôn ngữ scripting. Lưu ý rằng cách này cũng đi kèm những phức tạp riêng.

Godot hỗ trợ những định dạng model 3D nào?
------------------------------------------

Bạn có thể tìm thông tin chi tiết về các định dạng được hỗ trợ, cách export chúng từ phần mềm modeling 3D và cách import chúng vào Godot trong
:ref:`doc_importing_3d_scenes` tài liệu.

[chèn SDK đóng như FMOD, GameWorks, v.v.] có được hỗ trợ trong Godot không?
---------------------------------------------------------------------------

Mục tiêu của Godot là tạo ra một engine miễn phí, mã nguồn mở, được cấp phép theo MIT, có tính module hóa và khả năng mở rộng. Cộng đồng phát triển engine cốt lõi không có kế hoạch hỗ trợ bất kỳ SDK bên thứ ba, mã nguồn đóng hoặc độc quyền nào, vì việc tích hợp chúng đi ngược lại với triết lý của Godot.

Tuy vậy, vì Godot là mã nguồn mở và có tính module hóa, không có gì ngăn cản bạn hoặc bất kỳ ai quan tâm thêm các thư viện đó dưới dạng module và phát hành game của mình cùng với chúng, dù dưới dạng mã nguồn mở hay mã nguồn đóng.

Để xem cách vẫn có thể cung cấp hỗ trợ cho SDK bạn chọn, hãy xem câu hỏi về Plugins bên dưới.

Nếu bạn biết một SDK bên thứ ba chưa được Godot hỗ trợ nhưng cung cấp tích hợp miễn phí và mã nguồn mở, hãy cân nhắc tự bắt đầu công việc tích hợp. Godot không thuộc sở hữu của một cá nhân; nó thuộc về cộng đồng và phát triển cùng với những người đóng góp đầy tham vọng trong cộng đồng như bạn.

Tôi có thể mở rộng Godot như thế nào?
-------------------------------------

Để mở rộng Godot, chẳng hạn như tạo plugin cho Godot Editor hoặc thêm hỗ trợ cho các ngôn ngữ khác, hãy xem :ref:`EditorPlugins <doc_making_plugins>` và các tool script.

Ngoài ra, hãy xem bài viết chính thức trên blog về GDExtension, một cách để phát triển các extension native cho Godot:

* `Giới thiệu GDExtension, phần kế nhiệm của GDNative <https://godotengine.org/article/introducing-gd-extensions>`_

Bạn cũng có thể xem cách triển khai GDScript, các module của Godot, cũng như `tích hợp engine physics Jolt <https://github.com/godot-jolt/godot-jolt>`__ cho Godot. Đây sẽ là điểm khởi đầu phù hợp để xem một thư viện bên thứ ba khác tích hợp với Godot như thế nào.

Làm cách nào để cài đặt Godot editor trên hệ thống của tôi (để tích hợp với desktop)?
-------------------------------------------------------------------------------------

Vì bạn không thực sự cần cài đặt Godot trên hệ thống để chạy, nên việc tích hợp với desktop sẽ không được thực hiện tự động. Có hai cách để khắc phục điều này. Bạn có thể cài đặt Godot từ `Steam <https://store.steampowered.com/app/404790/Godot_Engine/>`__ (tất cả nền tảng), `Scoop <https://scoop.sh/>`__ (Windows), `Homebrew <https://brew.sh/>`__ (macOS) hoặc `Flathub <https://flathub.org/apps/details/org.godotengine.Godot>`__ (Linux). Thao tác này sẽ tự động thực hiện các bước cần thiết để tích hợp với desktop.

Ngoài ra, bạn có thể tự thực hiện các bước mà trình cài đặt sẽ thực hiện thay bạn:

Windows
~~~~~~~

- Di chuyển tệp thực thi Godot đến một vị trí ổn định (tức là bên ngoài thư mục Downloads), để bạn không vô tình di chuyển tệp và làm hỏng shortcut sau này.
- Nhấp chuột phải vào tệp thực thi Godot và chọn **Create Shortcut**.
- Di chuyển shortcut đã tạo đến ``%APPDATA%\Microsoft\Windows\Start Menu\Programs``. Đây là vị trí trên toàn hệ thống người dùng dành cho các shortcut sẽ xuất hiện trong menu Start. Bạn cũng có thể ghim Godot vào task bar bằng cách nhấp chuột phải vào tệp thực thi và chọn **Pin to Task Bar**.

macOS
~~~~~

Kéo ứng dụng Godot đã giải nén vào ``/Applications/Godot.app``, sau đó kéo ứng dụng vào Dock nếu muốn. Spotlight sẽ có thể tìm thấy Godot miễn là ứng dụng nằm trong ``/Applications`` hoặc ``~/Applications``.

Linux
~~~~~

- Di chuyển binary Godot đến một vị trí ổn định (tức là bên ngoài thư mục Downloads), để bạn không vô tình di chuyển tệp và làm hỏng shortcut sau này.
- Đổi tên và di chuyển binary Godot đến một vị trí có trong biến môi trường ``PATH``. Vị trí này thường là ``/usr/local/bin/godot`` hoặc ``/usr/bin/godot``. Việc này yêu cầu quyền administrator, nhưng cũng cho phép bạn
  :ref:`chạy trình chỉnh sửa Godot từ terminal <doc_command_line_tutorial>` bằng cách nhập ``godot``.

  - Nếu không thể di chuyển binary của trình chỉnh sửa Godot đến một vị trí được bảo vệ, bạn có thể giữ binary ở đâu đó trong thư mục home của mình và sửa dòng ``Path=`` trong tệp ``.desktop`` được liên kết bên dưới để chứa đường dẫn *absolute* đầy đủ đến binary Godot.

- Lưu `this .desktop file <https://raw.githubusercontent.com/godotengine/godot/master/misc/dist/linux/org.godotengine.Godot.desktop>`__ vào ``$HOME/.local/share/applications/``. Nếu có quyền administrator, bạn cũng có thể lưu tệp ``.desktop`` vào ``/usr/local/share/applications`` để shortcut khả dụng cho tất cả người dùng.

Trình chỉnh sửa Godot có phải là một ứng dụng portable không?
-------------------------------------------------------------

Trong cấu hình mặc định, Godot là ứng dụng *semi-portable*. Tệp thực thi của ứng dụng có thể chạy từ bất kỳ vị trí nào (kể cả các vị trí không cho phép ghi) và không bao giờ yêu cầu quyền administrator.

Tuy nhiên, các tệp cấu hình sẽ được ghi vào thư mục cấu hình hoặc dữ liệu trên toàn hệ thống người dùng. Đây thường là một cách tiếp cận tốt, nhưng điều đó có nghĩa là các tệp cấu hình sẽ không được chuyển sang máy khác nếu bạn sao chép thư mục chứa tệp thực thi Godot. Xem :ref:`doc_data_paths` để biết thêm thông tin.

Nếu muốn sử dụng chế độ portable *true* hoàn toàn (ví dụ: để sử dụng trên USB), hãy làm theo các bước trong :ref:`doc_data_paths_self_contained_mode`.

Tại sao Godot hướng đến việc giữ cho bộ tính năng cốt lõi nhỏ gọn?
------------------------------------------------------------------

Godot cố ý không bao gồm các tính năng có thể được triển khai bằng add-on, trừ khi chúng được sử dụng rất thường xuyên. Một ví dụ về tính năng không được sử dụng thường xuyên là chức năng trí tuệ nhân tạo nâng cao.

Có một số lý do cho việc này:

- **Bảo trì code và phạm vi phát sinh bug.** Mỗi khi chúng tôi chấp nhận code mới vào repository Godot, những contributor hiện có thường nhận trách nhiệm bảo trì code đó. Một số contributor không phải lúc nào cũng tiếp tục gắn bó sau khi code của họ được merge, điều này có thể khiến chúng tôi khó bảo trì code trong
  question. Điều này có thể dẫn đến các tính năng được bảo trì kém, với những bug không bao giờ được
  fixed. Ngoài ra, "API surface" cần được kiểm thử và kiểm tra
  để phát hiện regression cũng tiếp tục tăng theo thời gian.

- **Dễ dàng đóng góp.** Bằng cách giữ cho codebase nhỏ gọn và ngăn nắp, codebase có thể tiếp tục được biên dịch nhanh chóng và dễ dàng từ source. Điều này giúp các contributor mới bắt đầu với Godot dễ dàng hơn mà không yêu cầu họ phải mua phần cứng cao cấp.

- **Giữ kích thước binary của trình chỉnh sửa nhỏ.** Không phải ai cũng có Internet nhanh
  connection. Đảm bảo mọi người đều có thể tải xuống trình chỉnh sửa Godot, giải nén nó
  và chạy trong chưa đầy 5 phút giúp Godot dễ tiếp cận hơn với các developer ở mọi quốc gia.

- **Giữ kích thước binary của export template nhỏ.** Điều này ảnh hưởng trực tiếp đến kích thước của các project được export bằng Godot. Trên nền tảng mobile và web, việc giữ kích thước tệp ở mức thấp rất quan trọng để đảm bảo cài đặt và tải nhanh trên các thiết bị có hiệu năng thấp. Một lần nữa, có nhiều quốc gia không dễ dàng tiếp cận Internet tốc độ cao. Ngoài ra, các quốc gia đó thường áp dụng giới hạn sử dụng dữ liệu nghiêm ngặt.

Vì tất cả những lý do trên, chúng tôi phải lựa chọn kỹ lưỡng các chức năng có thể được chấp nhận là chức năng cốt lõi trong Godot. Đây là lý do chúng tôi đang hướng tới việc chuyển một số chức năng cốt lõi thành các add-on được hỗ trợ chính thức trong những phiên bản Godot tương lai. Xét về kích thước binary, cách này cũng có ưu điểm là bạn chỉ phải trả cho những gì thực sự được sử dụng trong project của mình. (Trong thời gian chờ đợi, bạn có thể
:ref:`biên dịch export template tùy chỉnh với các tính năng không sử dụng bị vô hiệu hóa <doc_optimizing_for_size>` để tối ưu kích thước phân phối của project.)

Nên tạo asset như thế nào để hỗ trợ nhiều độ phân giải và tỷ lệ khung hình?
---------------------------------------------------------------------------

Câu hỏi này thường được đặt ra và có lẽ nguyên nhân là do sự hiểu lầm mà Apple tạo ra khi họ ban đầu tăng gấp đôi độ phân giải của các thiết bị. Điều đó khiến mọi người nghĩ rằng sử dụng cùng một asset ở các độ phân giải khác nhau là một ý tưởng hay, nên nhiều người tiếp tục đi theo hướng đó. Ban đầu, cách này có hiệu quả ở một mức độ nhất định và chỉ dành cho các thiết bị Apple, nhưng sau đó nhiều thiết bị Android và Apple với độ phân giải và tỷ lệ khung hình khác nhau đã được tạo ra, với phạm vi kích thước và DPI rất rộng.

Cách phổ biến và phù hợp nhất để đạt được điều này là thay vào đó sử dụng một độ phân giải cơ sở duy nhất cho game và chỉ xử lý các tỷ lệ khung hình màn hình khác nhau. Điều này chủ yếu cần thiết cho 2D, vì trong 3D, vấn đề chỉ là FOV dọc hoặc ngang của camera.

1. Chọn một độ phân giải cơ sở duy nhất cho trò chơi của bạn. Ngay cả khi có thiết bị hỗ trợ đến 1440p và thiết bị chỉ hỗ trợ 400p, việc scaling phần cứng thông thường trên thiết bị sẽ xử lý điều này với rất ít hoặc không làm giảm hiệu năng. Các lựa chọn phổ biến nhất là gần 1080p (1920x1080) hoặc 720p (1280x720). Hãy nhớ rằng độ phân giải càng cao thì asset của bạn càng lớn, chiếm càng nhiều bộ nhớ và mất càng nhiều thời gian để tải.

2. Sử dụng các tùy chọn stretch trong Godot; việc stretch canvas items trong khi vẫn giữ nguyên aspect ratio là hiệu quả nhất. Hãy xem tutorial :ref:`doc_multiple_resolutions` để biết cách thực hiện.

3. Xác định độ phân giải tối thiểu, sau đó quyết định xem bạn muốn trò chơi stretch theo chiều dọc hay chiều ngang đối với các aspect ratio khác nhau, hay chỉ có một aspect ratio và muốn xuất hiện các thanh màu đen
   instead. Điều này cũng được giải thích trong :ref:`doc_multiple_resolutions`.

4. Đối với user interface, hãy sử dụng :ref:`anchoring <doc_size_and_anchors>` để xác định vị trí các control cần giữ nguyên và di chuyển. Nếu UI phức tạp hơn, hãy cân nhắc tìm hiểu về Containers.

Vậy là xong! Trò chơi của bạn sẽ hoạt động ở nhiều độ phân giải.

Khi nào bản phát hành tiếp theo của Godot sẽ ra mắt?
----------------------------------------------------

Khi đã sẵn sàng! Xem :ref:`doc_release_policy_when_is_next_release_out` để biết thêm thông tin.

Tôi nên sử dụng phiên bản Godot nào cho một dự án mới?
------------------------------------------------------

Chúng tôi khuyến nghị sử dụng Godot 4.x cho các dự án mới, nhưng tùy thuộc vào bộ tính năng bạn cần, sử dụng 3.x có thể phù hợp hơn. Xem
:ref:`doc_release_policy_which_version_should_i_use` để biết thêm thông tin.

Tôi có nên nâng cấp dự án của mình để sử dụng các phiên bản Godot mới không?
----------------------------------------------------------------------------

Một số phiên bản mới an toàn hơn khi nâng cấp so với các phiên bản khác. Nhìn chung, việc bạn có nên nâng cấp hay không phụ thuộc vào tình hình của dự án. Xem
:ref:`doc_release_policy_should_i_upgrade_my_project` để biết thêm thông tin.

Tôi nên sử dụng renderer Forward+, Mobile hay Compatibility?
------------------------------------------------------------

Bạn có thể tìm thấy phần so sánh chi tiết các renderer trong :ref:`doc_renderers`.

Tôi muốn đóng góp! Tôi nên bắt đầu như thế nào?
-----------------------------------------------

Tuyệt vời! Là một dự án mã nguồn mở, Godot phát triển mạnh nhờ sự đổi mới và tham vọng của những developer như bạn.

Cách tốt nhất để bắt đầu đóng góp cho Godot là sử dụng nó và báo cáo mọi `issues <https://github.com/godotengine/godot/issues>`_ mà bạn có thể gặp phải. Một bug report tốt với các bước tái hiện rõ ràng sẽ giúp những người cùng đóng góp nhanh chóng và hiệu quả sửa lỗi. Bạn cũng có thể báo cáo các issue tìm thấy trong `online documentation <https://github.com/godotengine/godot-docs/issues>`_.

Nếu bạn cảm thấy đã sẵn sàng gửi PR đầu tiên, hãy chọn bất kỳ issue nào khiến bạn quan tâm từ một trong các liên kết ở trên và thử tự sửa issue đó. Bạn sẽ cần học cách compile engine từ source hoặc cách build documentation. Bạn cũng cần làm quen với Git, một hệ thống version control mà các developer của Godot sử dụng.

Chúng tôi giải thích cách làm việc với source của engine, cách chỉnh sửa documentation và những cách đóng góp khác trong `documentation for contributors <https://contributing.godotengine.org/en/latest/index.html>`__ của chúng tôi.

Tôi có một ý tưởng tuyệt vời cho Godot. Tôi có thể chia sẻ ý tưởng đó như thế nào?
----------------------------------------------------------------------------------

Chúng tôi luôn tìm kiếm các đề xuất về cách cải thiện engine. Phản hồi của người dùng là động lực chính cho quá trình ra quyết định của chúng tôi, và những hạn chế bạn có thể gặp phải khi làm việc với dự án của mình là dữ liệu rất hữu ích để chúng tôi cân nhắc các cải tiến cho engine.

Nếu bạn gặp vấn đề về khả năng sử dụng hoặc thiếu một tính năng trong phiên bản Godot hiện tại, hãy bắt đầu bằng cách thảo luận vấn đề đó với `community <https://godotengine.org/community/>`_ của chúng tôi. Các thành viên cộng đồng có thể đề xuất những cách khác, có thể tốt hơn, để đạt được kết quả mong muốn. Bạn cũng có thể tìm hiểu xem những người dùng khác có gặp phải vấn đề tương tự không và cùng nhau tìm ra một giải pháp phù hợp.

Nếu bạn nảy ra một ý tưởng được xác định rõ ràng cho engine, hãy thoải mái mở một `proposal issue <https://github.com/godotengine/godot-proposals/issues>`_. Hãy cố gắng mô tả vấn đề và giải pháp đề xuất một cách cụ thể, rõ ràng — chỉ những proposal có thể triển khai mới được xem xét. Điều này không bắt buộc, nhưng nếu bạn muốn tự mình triển khai thì luôn được hoan nghênh!

Nếu bạn chỉ có một ý tưởng chung chung mà chưa có chi tiết cụ thể, bạn có thể mở một `proposal discussion <https://github.com/godotengine/godot-proposals/discussions>`_. Các discussion này có thể về bất kỳ điều gì bạn muốn và cho phép thảo luận tự do để tìm kiếm giải pháp. Khi tìm được giải pháp, bạn có thể mở một proposal issue.

Vui lòng đọc tài liệu `readme <https://github.com/godotengine/godot-proposals/blob/master/README.md>`_ trước khi tạo proposal để tìm hiểu thêm về quy trình.

.. _doc_faq_non_game_applications:

Có thể sử dụng Godot để tạo các ứng dụng không phải trò chơi không?
-------------------------------------------------------------------

Có! Godot có một hệ thống UI tích hợp phong phú, và kích thước bản phân phối nhỏ có thể khiến Godot trở thành một lựa chọn thay thế phù hợp cho các framework như Electron hoặc Qt.

Xem :ref:`doc_creating_applications` để biết thêm thông tin.

.. _doc_faq_use_godot_as_library:

Có thể sử dụng Godot như một library không?
-------------------------------------------

Nếu bạn muốn tạo một trò chơi bằng Godot, hãy nhớ rằng Godot được thiết kế để sử dụng cùng editor của nó. Chúng tôi khuyến nghị bạn dùng thử, vì về lâu dài, nhiều khả năng nó sẽ giúp bạn tiết kiệm thời gian.

Đối với các ứng dụng chuyên biệt hơn, việc xem xét sử dụng Godot như một library có thể hợp lý. Kể từ Godot 4.6, Godot có hỗ trợ **experimental** cho việc sử dụng Godot dưới dạng static hoặc shared library thông qua LibGodot. Hiện tại, tính năng này được hỗ trợ trên Windows, macOS và Linux. Hỗ trợ cho Android và iOS được lên kế hoạch trong một bản phát hành tương lai.

Bạn có thể tìm thấy các ứng dụng mẫu sử dụng Godot như một library trong `migeran/libgodot GitHub repository <https://github.com/migeran/libgodot>`__.

Godot sử dụng bộ công cụ user interface nào?
--------------------------------------------

Godot không sử dụng bộ công cụ :abbr:`GUI (Graphical User Interface)` tiêu chuẩn như GTK, Qt hoặc wxWidgets. Thay vào đó, Godot sử dụng bộ công cụ user interface riêng, luôn được render bằng hardware acceleration. Không có software fallback tích hợp, mặc dù có thể sử dụng các giải pháp bên ngoài mô phỏng graphics API trên CPU.

Bộ công cụ này được cung cấp dưới dạng các Control node, được dùng để kết xuất editor (được viết bằng C++). Các Control node này cũng có thể được sử dụng trong các project dùng bất kỳ ngôn ngữ scripting nào được Godot hỗ trợ.

Bộ công cụ tùy chỉnh này cho phép tận dụng khả năng tăng tốc phần cứng và duy trì giao diện nhất quán trên mọi nền tảng. Ngoài ra, nó không phải xử lý những điểm cần lưu ý về giấy phép LGPL đi kèm với GTK hoặc Qt. Cuối cùng, điều này có nghĩa là Godot đang "ăn chính thức ăn của mình" (eating its own dog food), vì bản thân editor là một trong những thành phần sử dụng hệ thống UI của Godot phức tạp nhất.

Bộ công cụ UI tùy chỉnh này có thể được :ref:`nhúng vào các ứng dụng khác <doc_faq_use_godot_as_library>` (thử nghiệm). Tuy nhiên, cách được khuyến nghị để sử dụng nó là
:ref:`dùng Godot để tạo các ứng dụng không phải game bằng editor <doc_faq_non_game_applications>`.

.. _doc_faq_why_scons:

Tại sao Godot sử dụng build system SCons?
-----------------------------------------

Godot sử dụng build system `SCons <https://www.scons.org/>`__. Hiện chưa có kế hoạch chuyển sang build system khác trong tương lai gần. Có nhiều lý do khiến chúng tôi chọn SCons thay vì các phương án khác. Ví dụ:

-  Godot có thể được biên dịch cho hàng chục nền tảng khác nhau: tất cả nền tảng PC, tất cả nền tảng di động, nhiều console và WebAssembly.
-  Các developer thường cần biên dịch cho nhiều nền tảng **cùng lúc**, hoặc thậm chí cho các target khác nhau của cùng một nền tảng. Họ không thể mất thời gian cấu hình lại và build lại project mỗi lần. SCons có thể thực hiện việc này dễ dàng mà không làm hỏng các bản build.
-  SCons *không bao giờ* làm hỏng bản build, bất kể có bao nhiêu thay đổi, cấu hình, phần bổ sung, phần xóa bỏ, v.v.
-  Quy trình build của Godot không đơn giản. Một số file được tạo bằng code (binder), một số file khác được phân tích cú pháp (shader), còn những file khác cần cho phép tùy chỉnh (:ref:`module <doc_custom_modules_in_cpp>`). Điều này đòi hỏi logic phức tạp, dễ viết hơn bằng một ngôn ngữ lập trình thực tế (chẳng hạn Python) thay vì một ngôn ngữ chủ yếu dựa trên macro và chỉ dành cho việc build.
-  Quy trình build của Godot sử dụng nhiều công cụ cross-compile. Mỗi nền tảng có một quy trình phát hiện riêng, và tất cả những quy trình này phải được xử lý như các trường hợp cụ thể bằng code đặc biệt viết cho từng nền tảng.

Nếu dự định tự build Godot, hãy cố gắng giữ tinh thần cởi mở và làm quen ít nhất một chút với SCons.

.. _doc_faq_why_not_stl:

Tại sao Godot không sử dụng STL (Standard Template Library)?
------------------------------------------------------------

Giống như nhiều library khác (chẳng hạn Qt), Godot không sử dụng STL (ngoại trừ một số trường hợp như các primitive về threading). Chúng tôi cho rằng STL là một library đa dụng tuyệt vời, nhưng Godot có những yêu cầu đặc biệt.

* Các template của STL tạo ra những symbol rất lớn, dẫn đến các binary debug khổng lồ. Thay vào đó, chúng tôi sử dụng một số ít template có tên rất ngắn.
* Phần lớn các container của chúng tôi phục vụ những nhu cầu đặc biệt, chẳng hạn như Vector, sử dụng copy on write và được dùng để truyền dữ liệu, hoặc hệ thống RID, yêu cầu thời gian truy cập O(1) để đảm bảo hiệu năng. Tương tự, các triển khai hash map của chúng tôi được thiết kế để tích hợp liền mạch với các kiểu dữ liệu nội bộ của engine.
* Các container của chúng tôi tích hợp sẵn tính năng theo dõi bộ nhớ, giúp theo dõi việc sử dụng bộ nhớ tốt hơn.
* Đối với các array lớn, chúng tôi sử dụng bộ nhớ dạng pool, có thể được ánh xạ tới buffer được cấp phát trước hoặc bộ nhớ ảo.
* Chúng tôi sử dụng kiểu String tùy chỉnh, vì kiểu do STL cung cấp quá cơ bản và thiếu hỗ trợ quốc tế hóa phù hợp.

Hãy xem :ref:`các kiểu container của Godot <doc_core_types>` để tìm các phương án thay thế.

Tại sao Godot không sử dụng exception?
--------------------------------------

Chúng tôi cho rằng game không nên bị crash, bất kể chuyện gì xảy ra. Nếu phát sinh tình huống bất ngờ, Godot sẽ in ra một lỗi (có thể truy vết ngay cả đến script), nhưng sau đó sẽ cố gắng khôi phục một cách êm thấm nhất có thể và tiếp tục chạy.

Ngoài ra, exception làm tăng đáng kể kích thước binary của executable và khiến thời gian biên dịch tăng lên.

Godot có sử dụng ECS (Entity Component System) không?
-----------------------------------------------------

Godot **không** sử dụng ECS mà thay vào đó dựa trên tính kế thừa. Mặc dù không có cách tiếp cận nào tốt hơn một cách tuyệt đối, chúng tôi nhận thấy cách tiếp cận dựa trên tính kế thừa mang lại khả năng sử dụng tốt hơn mà vẫn đủ nhanh cho hầu hết trường hợp sử dụng.

Tuy vậy, không có gì ngăn bạn sử dụng composition trong project bằng cách tạo các Node con với từng script riêng. Sau đó, bạn có thể thêm và xóa các node này trong runtime để linh động thêm và xóa các behavior.

Bạn có thể tìm thêm thông tin về các lựa chọn thiết kế của Godot trong `bài viết này <https://godotengine.org/article/why-isnt-godot-ecs-based-game-engine>`__.

Tại sao Godot không bắt buộc người dùng triển khai DOD (Data-Oriented Design)?
------------------------------------------------------------------------------

Mặc dù bản thân Godot cố gắng sử dụng cache coherency nhiều nhất có thể, chúng tôi cho rằng không cần bắt buộc người dùng áp dụng các thực hành DOD.

DOD chủ yếu là một tối ưu hóa cache coherency, chỉ có thể mang lại cải thiện hiệu năng đáng kể khi xử lý hàng chục nghìn object được xử lý trong mỗi frame với rất ít
modification. Nghĩa là, nếu bạn di chuyển vài trăm sprite hoặc enemy
trong mỗi frame, DOD sẽ không mang lại cải thiện hiệu năng đáng kể. Trong trường hợp đó, bạn nên cân nhắc một cách tiếp cận khác để tối ưu hóa.

Phần lớn game không cần đến điều này, và Godot cung cấp các helper tiện dụng để thực hiện công việc trong hầu hết trường hợp khi bạn cần.

Nếu game cần xử lý một lượng object lớn như vậy, chúng tôi khuyến nghị sử dụng C++ và GDExtensions cho các tác vụ nặng về hiệu năng, còn dùng GDScript (hoặc C#) cho phần còn lại của game.

Tôi có thể hỗ trợ việc phát triển Godot hoặc đóng góp như thế nào?
------------------------------------------------------------------

Xem `Cách đóng góp <https://contributing.godotengine.org/en/latest/index.html>`__.

Ai đang phát triển Godot? Tôi có thể liên hệ với các bạn như thế nào?
---------------------------------------------------------------------

Xem trang tương ứng trên `website Godot <https://godotengine.org/contact>`__.

.. _`Free and open source Software`: https://en.wikipedia.org/wiki/Free_and_open_source_software
.. _`OSI-approved`: https://opensource.org/licenses/MIT
.. _`CC BY 3.0`: https://creativecommons.org/licenses/by/3.0/
.. _`COPYRIGHT.txt`: https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt
.. _`LICENSE.txt`: https://github.com/godotengine/godot/blob/master/LICENSE.txt
.. _`logo LICENSE.txt`: https://github.com/godotengine/godot/blob/master/misc/logo/LICENSE.txt
.. _`the license page on the Godot website`: https://godotengine.org/license
.. _`Python`: https://github.com/touilleMan/godot-python
.. _`Nim`: https://github.com/pragmagic/godot-nim
.. _`Introducing GDNative's successor, GDExtension`: https://godotengine.org/article/introducing-gd-extensions
.. _`issues`: https://github.com/godotengine/godot/issues
.. _`online documentation`: https://github.com/godotengine/godot-docs/issues
.. _`community`: https://godotengine.org/community/
.. _`proposal issue`: https://github.com/godotengine/godot-proposals/issues
.. _`proposal discussion`: https://github.com/godotengine/godot-proposals/discussions
.. _`readme`: https://github.com/godotengine/godot-proposals/blob/master/README.md
