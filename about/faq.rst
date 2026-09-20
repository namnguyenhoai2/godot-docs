:allow_comments: False

.. meta::
    :keywords: FAQ

.. _doc_faq:

Các câu hỏi thường gặp
======================

Tôi có thể làm gì với Godot? Chi phí là bao nhiêu? Điều khoản cấp phép là gì?
-----------------------------------------------------------------------------

Godot là `phần mềm miễn phí và mã nguồn mở <https://en.wikipedia.org/wiki/Free_and_open_source_software>`_ được cung cấp theo giấy phép MIT `được OSI phê duyệt <https://opensource.org/licenses/MIT>`_. Điều này có nghĩa là phần mềm miễn phí theo nghĩa "tự do ngôn luận" cũng như theo nghĩa "bia miễn phí".

Tóm lại:

* Bạn được tự do tải xuống và sử dụng Godot cho bất kỳ mục đích nào: cá nhân, phi lợi nhuận, thương mại hoặc mục đích khác. * Bạn được tự do sửa đổi, phân phối, phân phối lại và remix Godot tùy thích, vì bất kỳ lý do nào, cho cả mục đích phi thương mại lẫn thương mại.

Toàn bộ nội dung của tài liệu đi kèm này được phát hành theo giấy phép Creative Commons Attribution 3.0 (`CC BY 3.0 <https://creativecommons.org/licenses/by/3.0/>`_) cho phép sử dụng tự do, với phần ghi công cho "Juan Linietsky, Ariel Manzur và cộng đồng Godot Engine."

Logo và biểu tượng nhìn chung cũng được cấp phép theo cùng giấy phép Creative Commons. Lưu ý rằng một số thư viện bên thứ ba đi kèm mã nguồn của Godot có thể có giấy phép khác.

Để biết đầy đủ chi tiết, hãy xem các tệp `COPYRIGHT.txt <https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt>`_, `LICENSE.txt <https://github.com/godotengine/godot/blob/master/LICENSE.txt>`_ và `logo LICENSE.txt <https://github.com/godotengine/godot/blob/master/misc/logo/LICENSE.txt>`_ trong kho lưu trữ Godot.

Ngoài ra, hãy xem `trang giấy phép trên website Godot <https://godotengine.org/license>`_.

Godot hỗ trợ những nền tảng nào?
--------------------------------

**Đối với trình chỉnh sửa:**

* Windows * macOS * Linux, \*BSD * Android (thử nghiệm) * `Web <https://editor.godotengine.org/>`__ (thử nghiệm)

**Để xuất game của bạn:**

* Windows * macOS * Linux, \*BSD * Android * iOS * Web

Cả tệp nhị phân 32-bit và 64-bit đều được hỗ trợ khi phù hợp, trong đó 64-bit là mặc định. Các bản dựng macOS chính thức hỗ trợ Apple Silicon nguyên bản cũng như x86_64.

Một số người dùng cũng cho biết họ đã xây dựng và sử dụng Godot thành công trên các hệ thống dựa trên ARM chạy Linux, chẳng hạn như Raspberry Pi.

Để biết thông tin về hỗ trợ console, hãy xem `website Godot <https://godotengine.org/consoles/>`__.

Để biết thêm về vấn đề này, hãy xem các phần về :ref:`exporting <toc-learn-workflow-export>` và :ref:`compiling Godot yourself <toc-devel-compiling>`.

.. note::

    Godot 3 cũng từng hỗ trợ Universal Windows Platform (UWP). Cổng nền tảng này đã bị loại bỏ trong Godot 4 do thiếu bảo trì và do Microsoft đã ngừng khuyến nghị nền tảng này. Nền tảng này vẫn có sẵn trong bản phát hành ổn định hiện tại của Godot 3 dành cho những người dùng quan tâm.

Godot hỗ trợ những ngôn ngữ lập trình nào?
------------------------------------------

Các ngôn ngữ được Godot chính thức hỗ trợ là GDScript, C# và C++. Xem các danh mục con tương ứng với từng ngôn ngữ trong phần :ref:`scripting <toc-learn-scripting>`.

Nếu bạn mới bắt đầu với Godot hoặc với việc phát triển game nói chung, GDScript là ngôn ngữ được khuyến nghị học và sử dụng vì nó là ngôn ngữ bản địa của Godot. Mặc dù về lâu dài, các ngôn ngữ kịch bản thường có hiệu năng thấp hơn các ngôn ngữ cấp thấp, nhưng đối với việc tạo nguyên mẫu, phát triển Sản phẩm khả dụng tối thiểu (MVP) và tập trung vào Thời gian đưa sản phẩm ra thị trường (TTM), GDScript sẽ cung cấp một cách phát triển game nhanh chóng, thân thiện và mạnh mẽ.

Lưu ý rằng hỗ trợ C# vẫn còn tương đối mới, vì vậy bạn có thể gặp một số vấn đề trong quá trình sử dụng. Hiện tại, nền tảng web cũng chưa hỗ trợ C#. Cộng đồng phát triển thân thiện và cần mẫn của chúng tôi luôn sẵn sàng giải quyết các vấn đề mới phát sinh, nhưng vì đây là một dự án mã nguồn mở, chúng tôi khuyến nghị bạn trước tiên nên tự tìm hiểu kỹ. Tìm kiếm trong các cuộc thảo luận về `các vấn đề đang mở <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Atopic%3Adotnet>`__ là một cách tuyệt vời để bắt đầu khắc phục sự cố.

Đối với các ngôn ngữ mới, bên thứ ba có thể cung cấp hỗ trợ thông qua GDExtensions. (Xem câu hỏi về plugin bên dưới). Hiện tại, chẳng hạn, đang có các nỗ lực phát triển các liên kết không chính thức cho Godot với `Python <https://github.com/touilleMan/godot-python>`_ và `Nim <https://github.com/pragmagic/godot-nim>`_.

.. _doc_faq_what_is_gdscript:

GDScript là gì và tại sao tôi nên sử dụng nó?
---------------------------------------------

GDScript là ngôn ngữ kịch bản tích hợp của Godot. Ngôn ngữ này được xây dựng từ đầu để tối đa hóa tiềm năng của Godot với lượng mã ít nhất, giúp cả nhà phát triển mới bắt đầu lẫn chuyên gia tận dụng các ưu điểm của Godot nhanh nhất có thể. Nếu bạn từng viết mã bằng một ngôn ngữ như Python, bạn sẽ cảm thấy rất quen thuộc. Để xem các ví dụ và tổng quan đầy đủ về sức mạnh mà GDScript cung cấp, hãy xem :ref:`GDScript scripting guide <doc_gdscript>`.

Có nhiều lý do để sử dụng GDScript, nhưng lý do nổi bật nhất là **giảm độ phức tạp** tổng thể.

Mục đích ban đầu của việc tạo ra một ngôn ngữ kịch bản tùy chỉnh, được tích hợp chặt chẽ với Godot, gồm hai phần: thứ nhất, nó giảm thời gian cần thiết để bắt đầu sử dụng Godot, mang đến cho nhà phát triển một cách nhanh chóng để làm quen với engine, tập trung vào năng suất; thứ hai, nó giảm gánh nặng bảo trì tổng thể, thu hẹp phạm vi của các vấn đề và cho phép các nhà phát triển engine tập trung vào việc khắc phục lỗi cũng như cải thiện các tính năng liên quan đến phần lõi của engine, thay vì dành nhiều thời gian để khiến một tập hợp nhỏ các tính năng tăng dần hoạt động trên một tập hợp lớn các ngôn ngữ.

Vì Godot là một dự án mã nguồn mở, ngay từ đầu việc ưu tiên một trải nghiệm tích hợp và liền mạch hơn việc thu hút thêm người dùng bằng cách hỗ trợ các ngôn ngữ lập trình quen thuộc hơn là điều cấp thiết, đặc biệt khi việc hỗ trợ những ngôn ngữ quen thuộc đó sẽ dẫn đến trải nghiệm kém hơn. Chúng tôi hiểu nếu bạn muốn sử dụng một ngôn ngữ khác trong Godot (xem danh sách các tùy chọn được hỗ trợ ở trên). Tuy vậy, nếu bạn chưa thử GDScript, hãy thử trong **ba ngày**. Cũng giống như Godot, một khi nhận ra nó mạnh mẽ đến mức nào và tốc độ phát triển của bạn được cải thiện ra sao, chúng tôi nghĩ bạn sẽ dần yêu thích GDScript.

Bạn có thể tìm thêm thông tin về cách làm quen với GDScript hoặc các ngôn ngữ kiểu động trong hướng dẫn :ref:`doc_gdscript_more_efficiently`.

Động lực nào đã dẫn đến việc tạo ra GDScript?
---------------------------------------------

Trong những ngày đầu, engine sử dụng ngôn ngữ kịch bản `Lua <https://www.lua.org>`__. Lua có thể nhanh nhờ LuaJIT, nhưng việc tạo các liên kết với một hệ thống hướng đối tượng (bằng cách sử dụng các phương án dự phòng) rất phức tạp, chậm và đòi hỏi một lượng mã khổng lồ. Sau một số thử nghiệm với `Python <https://www.python.org>`__, việc nhúng ngôn ngữ này cũng tỏ ra khó khăn.

Những lý do chính để tạo ra một ngôn ngữ kịch bản tùy chỉnh cho Godot là:

1. Hỗ trợ luồng kém trong hầu hết các máy ảo kịch bản, trong khi Godot sử dụng luồng (Lua, Python, Squirrel, JavaScript, ActionScript, v.v.). 2. Hỗ trợ mở rộng lớp kém trong hầu hết các máy ảo kịch bản, và việc điều chỉnh cho phù hợp với cách Godot hoạt động rất kém hiệu quả (Lua, Python, JavaScript). 3. Nhiều ngôn ngữ hiện có có giao diện khủng khiếp để liên kết với C++, dẫn đến lượng mã lớn, lỗi, điểm nghẽn và sự kém hiệu quả nói chung (Lua, Python, Squirrel, JavaScript, v.v.). Chúng tôi muốn tập trung vào một engine tuyệt vời, không phải một số lượng lớn các tích hợp. 4. Không có kiểu vector bản địa (Vector3, Transform3D, v.v.), dẫn đến hiệu năng suy giảm đáng kể khi sử dụng các kiểu tùy chỉnh (Lua, Python, Squirrel, JavaScript, ActionScript, v.v.). 5. Bộ thu gom rác gây ra hiện tượng đình trệ hoặc mức sử dụng bộ nhớ lớn không cần thiết (Lua, Python, JavaScript, ActionScript, v.v.). 6. Khó tích hợp với trình soạn thảo mã để cung cấp tính năng hoàn thành mã, chỉnh sửa trực tiếp, v.v. (tất cả các ngôn ngữ).

GDScript được thiết kế để khắc phục các vấn đề trên và nhiều vấn đề khác.

.. _doc_faq_which_programming_language_is_fastest:

Ngôn ngữ lập trình nào nhanh nhất?
----------------------------------

Trong hầu hết các game, bản thân *ngôn ngữ kịch bản* không phải là nguyên nhân gây ra các vấn đề về hiệu năng. Thay vào đó, hiệu năng bị giảm do các thuật toán kém hiệu quả (vốn chậm trong mọi ngôn ngữ), do hiệu năng GPU hoặc do mã C++ phổ biến của engine, chẳng hạn như vật lý hoặc điều hướng. Tất cả các ngôn ngữ được Godot hỗ trợ đều đủ nhanh cho việc viết kịch bản đa mục đích. Bạn nên chọn ngôn ngữ dựa trên các yếu tố khác, chẳng hạn như mức độ dễ sử dụng, sự quen thuộc, khả năng hỗ trợ nền tảng hoặc các tính năng của ngôn ngữ.

Nhìn chung, hiệu năng của C# và GDScript cùng nằm trong một bậc độ lớn, còn C++ nhanh hơn cả hai.

Việc so sánh hiệu năng của GDScript với C# khá phức tạp, vì C# có thể nhanh hơn trong một số trường hợp cụ thể. Bản thân *ngôn ngữ* C# thường nhanh hơn GDScript, nghĩa là C# có thể nhanh hơn trong các tình huống có ít lệnh gọi đến mã engine Godot. Tuy nhiên, C# có thể chậm hơn GDScript khi thực hiện nhiều lệnh gọi API Godot, do chi phí *marshalling*. Hiệu năng của C# cũng có thể bị giảm bởi việc thu gom rác xảy ra vào những thời điểm ngẫu nhiên và không thể dự đoán. Điều này có thể gây ra hiện tượng giật hình trong các dự án phức tạp và không chỉ xảy ra với Godot.

C++, sử dụng :ref:`GDExtension <doc_what_is_gdextension>`, hầu như luôn nhanh hơn C# hoặc GDScript. Tuy nhiên, C++ khó sử dụng hơn C# hoặc GDScript và tốc độ phát triển cũng chậm hơn.

Bạn cũng có thể sử dụng nhiều ngôn ngữ trong cùng một dự án, với
:ref:`cross-language scripting <doc_cross_language_scripting>`, or by using
GDExtension và các ngôn ngữ kịch bản cùng nhau. Hãy lưu ý rằng cách làm này cũng đi kèm những phức tạp riêng.

Godot hỗ trợ những định dạng mô hình 3D nào?
--------------------------------------------

Bạn có thể tìm thông tin chi tiết về các định dạng được hỗ trợ, cách xuất chúng từ phần mềm tạo mô hình 3D của mình và cách nhập chúng vào Godot trong
:ref:`doc_importing_3d_scenes` documentation.

[SDK đóng như FMOD, GameWorks, v.v.] có được hỗ trợ trong Godot không?
----------------------------------------------------------------------

Mục tiêu của Godot là tạo ra một engine miễn phí, mã nguồn mở và được cấp phép theo MIT, có tính mô-đun và khả năng mở rộng. Cộng đồng phát triển engine lõi không có kế hoạch hỗ trợ bất kỳ SDK bên thứ ba nào là mã nguồn đóng/độc quyền, vì việc tích hợp với chúng đi ngược lại đặc tính của Godot.

Tuy vậy, vì Godot là mã nguồn mở và có tính mô-đun, không có gì ngăn cản bạn hoặc bất kỳ ai quan tâm thêm các thư viện đó dưới dạng một mô-đun và phát hành trò chơi của mình cùng với chúng, dù là mã nguồn mở hay mã nguồn đóng.

Để xem cách vẫn có thể cung cấp hỗ trợ cho SDK bạn chọn, hãy xem câu hỏi về Plugins bên dưới.

Nếu bạn biết một SDK của bên thứ ba không được Godot hỗ trợ nhưng cung cấp khả năng tích hợp miễn phí và mã nguồn mở, hãy cân nhắc tự bắt đầu công việc tích hợp. Godot không thuộc sở hữu của một cá nhân; nó thuộc về cộng đồng và phát triển cùng những người đóng góp đầy tham vọng trong cộng đồng như bạn.

Làm thế nào để mở rộng Godot?
-----------------------------

Để mở rộng Godot, chẳng hạn như tạo plugin cho Godot Editor hoặc thêm hỗ trợ cho các ngôn ngữ khác, hãy xem :ref:`EditorPlugins <doc_making_plugins>` và các tập lệnh công cụ.

Ngoài ra, hãy xem bài viết chính thức trên blog về GDExtension, một cách để phát triển các phần mở rộng gốc cho Godot:

* `Giới thiệu GDNative thế hệ tiếp theo, GDExtension <https://godotengine.org/article/introducing-gd-extensions>`_

Bạn cũng có thể xem cách triển khai GDScript, các mô-đun Godot, cũng như `tích hợp công cụ vật lý Jolt <https://github.com/godot-jolt/godot-jolt>`__ cho Godot. Đây sẽ là điểm khởi đầu tốt để xem cách một thư viện bên thứ ba khác tích hợp với Godot.

Làm thế nào để cài đặt Godot editor trên hệ thống của tôi (để tích hợp với máy tính để bàn)?
--------------------------------------------------------------------------------------------

Vì bạn không thực sự cần cài đặt Godot trên hệ thống để chạy nó, nên việc tích hợp với máy tính để bàn không được thực hiện tự động. Có hai cách để khắc phục điều này. Bạn có thể cài đặt Godot từ `Steam <https://store.steampowered.com/app/404790/Godot_Engine/>`__ (tất cả các nền tảng), `Scoop <https://scoop.sh/>`__ (Windows), `Homebrew <https://brew.sh/>`__ (macOS) hoặc `Flathub <https://flathub.org/apps/details/org.godotengine.Godot>`__ (Linux). Các bước cần thiết để tích hợp với máy tính để bàn sẽ được thực hiện tự động.

Ngoài ra, bạn có thể tự thực hiện các bước mà trình cài đặt thường làm thay bạn:

Windows
~~~~~~~

- Di chuyển tệp thực thi Godot đến một vị trí ổn định (tức là bên ngoài thư mục Downloads), để bạn không vô tình di chuyển nó và làm hỏng shortcut trong tương lai. - Nhấp chuột phải vào tệp thực thi Godot và chọn **Create Shortcut**. - Di chuyển shortcut vừa tạo đến ``%APPDATA%\Microsoft\Windows\Start Menu\Programs``. Đây là vị trí dùng chung cho người dùng của các shortcut sẽ xuất hiện trong menu Start. Bạn cũng có thể ghim Godot vào thanh tác vụ bằng cách nhấp chuột phải vào tệp thực thi và chọn **Pin to Task Bar**.

macOS
~~~~~

Kéo ứng dụng Godot đã giải nén vào ``/Applications/Godot.app``, sau đó kéo ứng dụng vào Dock nếu muốn. Spotlight có thể tìm thấy Godot miễn là ứng dụng nằm trong ``/Applications`` hoặc ``~/Applications``.

Linux
~~~~~

- Di chuyển tệp nhị phân Godot đến một vị trí ổn định (tức là bên ngoài thư mục Downloads), để bạn không vô tình di chuyển nó và làm hỏng shortcut trong tương lai. - Đổi tên và di chuyển tệp nhị phân Godot đến một vị trí có trong biến môi trường ``PATH``. Vị trí này thường là ``/usr/local/bin/godot`` hoặc ``/usr/bin/godot``. Việc này yêu cầu quyền quản trị viên, nhưng cũng cho phép bạn
  :ref:`run the Godot editor from a terminal <doc_command_line_tutorial>` by entering ``godot``.

  - Nếu không thể di chuyển tệp nhị phân của Godot editor đến một vị trí được bảo vệ, bạn có thể giữ tệp nhị phân ở đâu đó trong thư mục home của mình và sửa dòng ``Path=`` trong tệp ``.desktop`` được liên kết bên dưới để chứa đường dẫn *tuyệt đối* đầy đủ đến tệp nhị phân Godot.

- Lưu `tệp .desktop này <https://raw.githubusercontent.com/godotengine/godot/master/misc/dist/linux/org.godotengine.Godot.desktop>`__ vào ``$HOME/.local/share/applications/``. Nếu có quyền quản trị viên, bạn cũng có thể lưu tệp ``.desktop`` vào ``/usr/local/share/applications`` để shortcut khả dụng cho tất cả người dùng.

Godot editor có phải là một ứng dụng portable không?
----------------------------------------------------

Trong cấu hình mặc định, Godot là ứng dụng *bán portable*. Tệp thực thi của nó có thể chạy từ bất kỳ vị trí nào (kể cả các vị trí không cho phép ghi) và không bao giờ yêu cầu quyền quản trị viên.

Tuy nhiên, các tệp cấu hình sẽ được ghi vào thư mục cấu hình hoặc dữ liệu dùng chung cho người dùng. Đây thường là một cách tiếp cận tốt, nhưng điều đó có nghĩa là các tệp cấu hình sẽ không được chuyển sang máy khác nếu bạn sao chép thư mục chứa tệp thực thi Godot. Xem :ref:`doc_data_paths` để biết thêm thông tin.

Nếu muốn hoạt động portable *thực sự* (ví dụ: sử dụng trên USB), hãy làm theo các bước trong :ref:`doc_data_paths_self_contained_mode`.

Tại sao Godot hướng đến việc giữ cho tập hợp tính năng cốt lõi nhỏ gọn?
-----------------------------------------------------------------------

Godot cố ý không bao gồm các tính năng có thể được triển khai bằng add-on, trừ khi chúng được sử dụng rất thường xuyên. Một ví dụ về tính năng không được sử dụng thường xuyên là chức năng trí tuệ nhân tạo nâng cao.

Có một số lý do cho việc này:

- **Bảo trì mã và bề mặt lỗi.** Mỗi khi chúng tôi chấp nhận mã mới vào kho lưu trữ Godot, những người đóng góp hiện tại thường nhận trách nhiệm bảo trì mã đó. Một số người đóng góp không phải lúc nào cũng tiếp tục gắn bó sau khi mã của họ được hợp nhất, điều này có thể khiến chúng tôi khó bảo trì phần mã đó. Điều này có thể dẫn đến các tính năng được bảo trì kém với những lỗi không bao giờ được sửa. Ngoài ra, "bề mặt API" cần được kiểm thử và kiểm tra hồi quy cũng không ngừng tăng theo thời gian.

- **Dễ đóng góp.** Bằng cách giữ cho cơ sở mã nhỏ gọn và ngăn nắp, việc biên dịch từ mã nguồn có thể vẫn nhanh chóng và dễ dàng. Điều này giúp những người đóng góp mới bắt đầu với Godot dễ hơn mà không yêu cầu họ phải mua phần cứng cao cấp.

- **Giữ kích thước tệp nhị phân của editor nhỏ.** Không phải ai cũng có kết nối Internet nhanh. Đảm bảo mọi người có thể tải xuống Godot editor, giải nén và chạy nó trong chưa đầy 5 phút giúp Godot dễ tiếp cận hơn với các nhà phát triển ở mọi quốc gia.

- **Giữ kích thước tệp nhị phân của các mẫu xuất nhỏ.** Điều này ảnh hưởng trực tiếp đến kích thước của các dự án được xuất bằng Godot. Trên các nền tảng di động và web, việc giữ kích thước tệp nhỏ rất quan trọng để đảm bảo cài đặt và tải nhanh trên các thiết bị yếu. Một lần nữa, có nhiều quốc gia không có sẵn Internet tốc độ cao. Ngoài ra, tại những quốc gia đó thường áp dụng các giới hạn nghiêm ngặt về lượng dữ liệu sử dụng.

Vì tất cả những lý do trên, chúng tôi phải chọn lọc những gì có thể được chấp nhận là chức năng cốt lõi trong Godot. Đây là lý do chúng tôi hướng đến việc chuyển một số chức năng cốt lõi thành các add-on được hỗ trợ chính thức trong các phiên bản Godot tương lai. Xét về kích thước tệp nhị phân, điều này cũng có lợi thế là bạn chỉ phải trả giá cho những gì thực sự được sử dụng trong dự án của mình. (Trong thời gian chờ đợi, bạn có thể
:ref:`compile custom export templates with unused features disabled <doc_optimizing_for_size>`
để tối ưu kích thước phân phối của dự án.)

Nên tạo các tài nguyên như thế nào để hỗ trợ nhiều độ phân giải và tỷ lệ khung hình?
------------------------------------------------------------------------------------

Câu hỏi này thường xuất hiện và có lẽ là do sự hiểu lầm được Apple tạo ra khi họ tăng gấp đôi độ phân giải của các thiết bị ban đầu. Điều đó khiến mọi người nghĩ rằng việc có cùng một bộ tài nguyên ở các độ phân giải khác nhau là một ý tưởng hay, nên nhiều người tiếp tục theo hướng đó. Ban đầu, cách này có hiệu quả ở một mức độ nhất định và chỉ trên các thiết bị Apple, nhưng sau đó nhiều thiết bị Android và Apple với độ phân giải và tỷ lệ khung hình khác nhau đã được tạo ra, với dải kích thước và DPI rất rộng.

Cách phổ biến và phù hợp nhất để đạt được điều này là thay vào đó sử dụng một độ phân giải cơ sở duy nhất cho trò chơi và chỉ xử lý các tỷ lệ khung hình màn hình khác nhau. Điều này chủ yếu cần thiết cho 2D, vì trong 3D, đó chỉ là vấn đề về FOV dọc hoặc ngang của camera.

1. Hãy chọn một độ phân giải cơ sở duy nhất cho trò chơi. Ngay cả khi có thiết bị đạt tới 1440p và thiết bị xuống tới 400p, việc mở rộng phần cứng thông thường trên thiết bị sẽ xử lý điều này với rất ít hoặc không có chi phí hiệu năng. Các lựa chọn phổ biến nhất là gần 1080p (1920x1080) hoặc 720p (1280x720). Hãy nhớ rằng độ phân giải càng cao thì tài nguyên của bạn càng lớn, chiếm càng nhiều bộ nhớ và mất càng nhiều thời gian để tải.

2. Sử dụng các tùy chọn stretch trong Godot; việc kéo giãn các mục canvas trong khi vẫn giữ tỷ lệ khung hình hoạt động tốt nhất. Xem hướng dẫn :ref:`doc_multiple_resolutions` để biết cách thực hiện.

3. Xác định một độ phân giải tối thiểu, sau đó quyết định xem bạn muốn trò chơi kéo giãn theo chiều dọc hay chiều ngang đối với các tỷ lệ khung hình khác nhau, hay có một tỷ lệ khung hình duy nhất và muốn các thanh màu đen xuất hiện. Điều này cũng được giải thích trong :ref:`doc_multiple_resolutions`.

4. Đối với giao diện người dùng, hãy sử dụng :ref:`anchoring <doc_size_and_anchors>` để xác định vị trí các điều khiển nên giữ nguyên và di chuyển đến. Nếu UI phức tạp hơn, hãy cân nhắc tìm hiểu về Containers.

Vậy là xong! Trò chơi của bạn sẽ hoạt động ở nhiều độ phân giải.

Khi nào bản phát hành tiếp theo của Godot sẽ ra mắt?
----------------------------------------------------

Khi đã sẵn sàng! Xem :ref:`doc_release_policy_when_is_next_release_out` để biết thêm thông tin.

Tôi nên sử dụng phiên bản Godot nào cho một dự án mới?
------------------------------------------------------

Chúng tôi khuyến nghị sử dụng Godot 4.x cho các dự án mới, nhưng tùy thuộc vào tập hợp tính năng bạn cần, sử dụng 3.x có thể phù hợp hơn. Xem
:ref:`doc_release_policy_which_version_should_i_use` for more information.

Tôi có nên nâng cấp dự án để sử dụng các phiên bản Godot mới không?
-------------------------------------------------------------------

Một số phiên bản mới an toàn hơn các phiên bản khác khi nâng cấp lên. Nhìn chung, việc bạn có nên nâng cấp hay không phụ thuộc vào hoàn cảnh của dự án. Xem
:ref:`doc_release_policy_should_i_upgrade_my_project` for more information.

Tôi nên sử dụng trình kết xuất Forward+, Mobile hay Compatibility?
------------------------------------------------------------------

Bạn có thể tìm thấy phần so sánh chi tiết các trình kết xuất trong :ref:`doc_renderers`.

Tôi muốn đóng góp! Tôi nên bắt đầu như thế nào?
-----------------------------------------------

Tuyệt vời! Là một dự án mã nguồn mở, Godot phát triển mạnh nhờ sự đổi mới và tham vọng của những nhà phát triển như bạn.

Cách tốt nhất để bắt đầu đóng góp cho Godot là sử dụng phần mềm này và báo cáo mọi `issue <https://github.com/godotengine/godot/issues>`_ mà bạn có thể gặp phải. Một báo cáo lỗi tốt với các bước tái hiện rõ ràng sẽ giúp những người đóng góp khác sửa lỗi nhanh chóng và hiệu quả. Bạn cũng có thể báo cáo các vấn đề tìm thấy trong `tài liệu trực tuyến <https://github.com/godotengine/godot-docs/issues>`_.

Nếu bạn cảm thấy đã sẵn sàng gửi PR đầu tiên, hãy chọn bất kỳ issue nào phù hợp với bạn từ một trong các liên kết ở trên và thử tự sửa issue đó. Bạn sẽ cần học cách biên dịch engine từ mã nguồn hoặc cách xây dựng tài liệu. Bạn cũng cần làm quen với Git, một hệ thống kiểm soát phiên bản được các nhà phát triển Godot sử dụng.

Chúng tôi giải thích cách làm việc với mã nguồn engine, cách chỉnh sửa tài liệu và những cách khác để đóng góp trong `tài liệu dành cho người đóng góp <https://contributing.godotengine.org/en/latest/organization/how_to_contribute.html>`__ của mình.

Tôi có một ý tưởng tuyệt vời cho Godot. Tôi có thể chia sẻ ý tưởng đó bằng cách nào?
------------------------------------------------------------------------------------

Chúng tôi luôn tìm kiếm các đề xuất về cách cải thiện engine. Phản hồi của người dùng là động lực chính đằng sau quá trình ra quyết định của chúng tôi, và những hạn chế mà bạn có thể gặp phải khi làm việc trong dự án của mình là dữ liệu rất hữu ích cho chúng tôi khi cân nhắc các cải tiến cho engine.

Nếu bạn gặp vấn đề về khả năng sử dụng hoặc thiếu một tính năng trong phiên bản Godot hiện tại, hãy bắt đầu bằng cách thảo luận về vấn đề đó với `cộng đồng <https://godotengine.org/community/>`_ của chúng tôi. Có thể có những cách khác, thậm chí tốt hơn, để đạt được kết quả mong muốn mà các thành viên cộng đồng có thể đề xuất. Bạn cũng có thể tìm hiểu xem những người dùng khác có gặp phải vấn đề tương tự hay không và cùng nhau tìm ra một giải pháp tốt.

Nếu bạn nảy ra một ý tưởng được xác định rõ ràng cho engine, hãy thoải mái mở một `proposal issue <https://github.com/godotengine/godot-proposals/issues>`_. Hãy cố gắng cụ thể và rõ ràng khi mô tả vấn đề cũng như giải pháp bạn đề xuất — chỉ những đề xuất có thể triển khai mới được xem xét. Điều này không bắt buộc, nhưng nếu bạn muốn tự mình triển khai thì chúng tôi luôn trân trọng điều đó!

Nếu bạn chỉ có một ý tưởng chung chung mà chưa có chi tiết cụ thể, bạn có thể mở một `proposal discussion <https://github.com/godotengine/godot-proposals/discussions>`_. Những cuộc thảo luận này có thể xoay quanh bất cứ điều gì bạn muốn và cho phép thảo luận tự do để tìm kiếm giải pháp. Khi tìm được giải pháp, bạn có thể mở một proposal issue.

Vui lòng đọc tài liệu `readme <https://github.com/godotengine/godot-proposals/blob/master/README.md>`_ trước khi tạo proposal để tìm hiểu thêm về quy trình.

.. _doc_faq_non_game_applications:

Có thể sử dụng Godot để tạo các ứng dụng không phải trò chơi không?
-------------------------------------------------------------------

Có! Godot cung cấp một hệ thống UI tích hợp phong phú, và kích thước phân phối nhỏ gọn của nó có thể khiến Godot trở thành một lựa chọn thay thế phù hợp cho các framework như Electron hoặc Qt.

Xem :ref:`doc_creating_applications` để biết thêm thông tin.

.. _doc_faq_use_godot_as_library:

Có thể sử dụng Godot như một thư viện không?
--------------------------------------------

Nếu bạn đang muốn tạo một trò chơi bằng Godot, hãy nhớ rằng Godot được thiết kế để sử dụng cùng editor của nó. Chúng tôi khuyên bạn nên thử, vì về lâu dài cách này nhiều khả năng sẽ giúp bạn tiết kiệm thời gian.

Đối với các ứng dụng chuyên biệt hơn, việc tìm hiểu cách sử dụng Godot như một thư viện có thể là lựa chọn hợp lý. Kể từ Godot 4.6, đã có hỗ trợ **experimental** cho việc sử dụng Godot dưới dạng thư viện tĩnh hoặc thư viện dùng chung thông qua LibGodot. Hiện tại, tính năng này được hỗ trợ trên Windows, macOS và Linux. Hỗ trợ cho Android và iOS được dự kiến sẽ có trong một bản phát hành tương lai.

Bạn có thể tìm thấy các ứng dụng mẫu sử dụng Godot như một thư viện trong `migeran/libgodot_project GitHub repository <https://github.com/migeran/libgodot_project>`__.

Godot sử dụng bộ công cụ giao diện người dùng nào?
--------------------------------------------------

Godot không sử dụng bộ công cụ :abbr:`GUI (Graphical User Interface)` tiêu chuẩn như GTK, Qt hoặc wxWidgets. Thay vào đó, Godot sử dụng bộ công cụ giao diện người dùng của riêng mình, luôn được kết xuất bằng tăng tốc phần cứng. Không có cơ chế dự phòng bằng phần mềm tích hợp sẵn, mặc dù có thể sử dụng các giải pháp bên ngoài mô phỏng API đồ họa trên CPU.

Bộ công cụ này được cung cấp dưới dạng các node Control, dùng để kết xuất editor (được viết bằng C++). Các node Control này cũng có thể được sử dụng trong những dự án viết bằng bất kỳ ngôn ngữ lập trình nào được Godot hỗ trợ.

Bộ công cụ tùy chỉnh này giúp tận dụng tăng tốc phần cứng và có giao diện nhất quán trên mọi nền tảng. Ngoài ra, nó không phải xử lý những vấn đề cấp phép LGPL đi kèm với GTK hoặc Qt. Cuối cùng, điều này có nghĩa là Godot đang "ăn chính thức ăn của mình", vì bản thân editor là một trong những thành phần sử dụng hệ thống UI của Godot phức tạp nhất.

Bộ công cụ UI tùy chỉnh này có thể được :ref:`embedded into other applications <doc_faq_use_godot_as_library>` (experimental). Tuy nhiên, cách được ưu tiên để sử dụng nó là
:ref:`use Godot to create non-game applications with the editor <doc_faq_non_game_applications>`.

.. _doc_faq_why_scons:

Tại sao Godot sử dụng hệ thống build SCons?
-------------------------------------------

Godot sử dụng hệ thống build `SCons <https://www.scons.org/>`__. Hiện chưa có kế hoạch chuyển sang một hệ thống build khác trong tương lai gần. Có nhiều lý do khiến chúng tôi chọn SCons thay vì các giải pháp khác. Ví dụ:

-  Godot có thể được biên dịch cho hàng chục nền tảng khác nhau: tất cả nền tảng PC, tất cả nền tảng di động, nhiều máy chơi game và WebAssembly. - Các nhà phát triển thường cần biên dịch cho nhiều nền tảng **cùng lúc**, hoặc thậm chí cho các target khác nhau trên cùng một nền tảng. Họ không thể dành thời gian cấu hình lại và build lại dự án mỗi lần. SCons có thể thực hiện việc này dễ dàng mà không làm hỏng các bản build. - SCons sẽ *không bao giờ* làm hỏng một bản build, bất kể có bao nhiêu thay đổi, cấu hình, phần bổ sung, phần bị xóa, v.v. - Quy trình build của Godot không đơn giản. Một số tệp được tạo bằng mã (binder), một số khác được phân tích cú pháp (shader), còn một số cần hỗ trợ tùy chỉnh (:ref:`modules <doc_custom_modules_in_cpp>`). Điều này đòi hỏi logic phức tạp, dễ viết hơn bằng một ngôn ngữ lập trình thực tế (như Python) thay vì một ngôn ngữ chủ yếu dựa trên macro chỉ dành cho việc build. - Quy trình build của Godot sử dụng rất nhiều công cụ cross-compile. Mỗi nền tảng có một quy trình phát hiện riêng, và tất cả những quy trình này phải được xử lý như các trường hợp cụ thể bằng mã đặc biệt được viết cho từng nền tảng.

Nếu bạn dự định tự build Godot, hãy cố gắng giữ tinh thần cởi mở và làm quen ít nhất một chút với SCons.

.. _doc_faq_why_not_stl:

Tại sao Godot không sử dụng STL (Standard Template Library)?
------------------------------------------------------------

Giống như nhiều thư viện khác (chẳng hạn Qt), Godot không sử dụng STL (ngoại trừ một số trường hợp như các primitive về threading). Chúng tôi tin rằng STL là một thư viện đa dụng tuyệt vời, nhưng Godot có những yêu cầu đặc biệt.

* Các template của STL tạo ra những symbol rất lớn, dẫn đến các binary debug khổng lồ. Thay vào đó, chúng tôi sử dụng ít template với tên rất ngắn. * Phần lớn container của chúng tôi phục vụ các nhu cầu đặc biệt, chẳng hạn như Vector, sử dụng copy on write và được dùng để truyền dữ liệu, hoặc hệ thống RID, yêu cầu thời gian truy cập O(1) để đạt hiệu năng. Tương tự, các triển khai hash map của chúng tôi được thiết kế để tích hợp liền mạch với các kiểu engine nội bộ. * Các container của chúng tôi được tích hợp sẵn tính năng theo dõi bộ nhớ, giúp theo dõi mức sử dụng bộ nhớ tốt hơn. * Đối với các mảng lớn, chúng tôi sử dụng bộ nhớ dạng pool, có thể được ánh xạ tới một buffer được cấp phát trước hoặc bộ nhớ ảo. * Chúng tôi sử dụng kiểu String tùy chỉnh, vì kiểu do STL cung cấp quá cơ bản và thiếu hỗ trợ quốc tế hóa phù hợp.

Xem :ref:`Godot's container types <doc_core_types>` để biết các lựa chọn thay thế.

Tại sao Godot không sử dụng exception?
--------------------------------------

Chúng tôi tin rằng trò chơi không nên bị crash, bất kể chuyện gì xảy ra. Nếu xuất hiện một tình huống bất ngờ, Godot sẽ in ra một lỗi (có thể truy vết ngay cả đến script), nhưng sau đó sẽ cố gắng khôi phục một cách nhẹ nhàng nhất có thể và tiếp tục hoạt động.

Ngoài ra, exception làm tăng đáng kể kích thước binary của tệp thực thi và khiến thời gian biên dịch tăng lên.

Godot có sử dụng ECS (Entity Component System) không?
-----------------------------------------------------

Godot **không** sử dụng ECS mà thay vào đó dựa trên tính kế thừa. Mặc dù không có cách tiếp cận nào tốt hơn một cách tuyệt đối, chúng tôi nhận thấy cách tiếp cận dựa trên tính kế thừa mang lại khả năng sử dụng tốt hơn mà vẫn đủ nhanh cho hầu hết trường hợp sử dụng.

Tuy vậy, không có gì ngăn bạn sử dụng composition trong dự án bằng cách tạo các Node con với từng script riêng. Sau đó, các node này có thể được thêm vào và xóa đi trong thời gian chạy để linh hoạt thêm và xóa các hành vi.

Bạn có thể tìm thấy thêm thông tin về các lựa chọn thiết kế của Godot trong `bài viết này <https://godotengine.org/article/why-isnt-godot-ecs-based-game-engine>`__.

Tại sao Godot không buộc người dùng phải triển khai DOD (Data-Oriented Design)?
-------------------------------------------------------------------------------

Mặc dù Godot cố gắng tận dụng tính nhất quán của cache nhiều nhất có thể ở bên trong, chúng tôi tin rằng không cần buộc người dùng phải áp dụng các phương pháp DOD.

DOD chủ yếu là một tối ưu hóa tính nhất quán của cache, chỉ có thể mang lại cải thiện hiệu năng đáng kể khi xử lý hàng chục nghìn đối tượng được xử lý trong mỗi frame với rất ít thay đổi. Nghĩa là, nếu bạn di chuyển vài trăm sprite hoặc enemy trong mỗi frame, DOD sẽ không mang lại cải thiện hiệu năng đáng kể. Trong trường hợp đó, bạn nên cân nhắc một cách tiếp cận tối ưu hóa khác.

Đại đa số trò chơi không cần đến điều này, và Godot cung cấp các helper tiện dụng để thực hiện công việc trong hầu hết trường hợp khi bạn cần.

Nếu một trò chơi cần xử lý số lượng đối tượng lớn như vậy, chúng tôi khuyến nghị sử dụng C++ và GDExtensions cho các tác vụ đòi hỏi nhiều hiệu năng, còn GDScript (hoặc C#) cho phần còn lại của trò chơi.

Tôi có thể hỗ trợ quá trình phát triển Godot hoặc đóng góp như thế nào?
-----------------------------------------------------------------------

Xem `Cách đóng góp <https://contributing.godotengine.org/en/latest/organization/how_to_contribute.html>`__.

Ai đang làm việc trên Godot? Tôi có thể liên hệ với các bạn bằng cách nào?
--------------------------------------------------------------------------

Xem trang tương ứng trên `website Godot <https://godotengine.org/contact>`__.
