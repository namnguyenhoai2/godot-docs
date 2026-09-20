.. Mục đích: chỉ giới thiệu khái quát về chức năng của tập lệnh và các tùy chọn ngôn ngữ lập trình.

.. _doc_scripting:

Các ngôn ngữ lập trình bằng tập lệnh
====================================

Bài học này sẽ cung cấp cho bạn cái nhìn tổng quan về các ngôn ngữ lập trình bằng tập lệnh hiện có trong Godot. Bạn sẽ tìm hiểu ưu và nhược điểm của từng tùy chọn. Trong phần tiếp theo, bạn sẽ viết tập lệnh đầu tiên bằng GDScript.

**Tập lệnh được gắn vào một nút và mở rộng hành vi của nút đó**. Điều này có nghĩa là tập lệnh kế thừa tất cả các hàm và thuộc tính của nút mà nó được gắn vào.

Ví dụ, hãy xem một trò chơi trong đó một nút Camera2D đi theo một con tàu. Theo mặc định, nút Camera2D đi theo nút cha của nó. Hãy tưởng tượng bạn muốn camera rung khi người chơi nhận sát thương. Vì tính năng này không được tích hợp sẵn trong Godot, bạn sẽ gắn một tập lệnh vào nút Camera2D và lập trình hiệu ứng rung.

.. image:: img/scripting_camera_shake.gif

Các ngôn ngữ lập trình bằng tập lệnh hiện có
--------------------------------------------

Godot cung cấp **bốn ngôn ngữ lập trình trò chơi**: GDScript, C#, và thông qua công nghệ GDExtension, C và C++. Có thêm các ngôn ngữ do cộng đồng hỗ trợ, nhưng đây là những ngôn ngữ chính thức.

Bạn có thể sử dụng nhiều ngôn ngữ trong cùng một dự án. Chẳng hạn, trong một nhóm, bạn có thể viết logic trò chơi bằng GDScript vì ngôn ngữ này cho phép viết nhanh, đồng thời dùng C# hoặc C++ để triển khai các thuật toán phức tạp và tối đa hóa hiệu năng của chúng. Hoặc bạn có thể viết mọi thứ bằng GDScript hoặc C#. Tùy bạn lựa chọn.

Chúng tôi cung cấp sự linh hoạt này để đáp ứng nhu cầu của nhiều dự án trò chơi và nhà phát triển khác nhau.

Tôi nên sử dụng ngôn ngữ nào?
-----------------------------

Nếu bạn là người mới bắt đầu, chúng tôi khuyên bạn **bắt đầu với GDScript**. Chúng tôi tạo ra ngôn ngữ này dành riêng cho Godot và nhu cầu của các nhà phát triển trò chơi. Ngôn ngữ này có cú pháp gọn nhẹ, đơn giản và tích hợp chặt chẽ nhất với Godot.

.. image:: img/scripting_gdscript.webp

Đối với C#, bạn sẽ cần một trình soạn thảo mã bên ngoài như `VSCode <https://code.visualstudio.com/>`_ hoặc Visual Studio. Mặc dù khả năng hỗ trợ C# hiện đã hoàn thiện, bạn sẽ tìm thấy ít tài liệu học tập hơn so với GDScript. Vì vậy, chúng tôi chủ yếu khuyên dùng C# cho những người đã có kinh nghiệm với ngôn ngữ này.

Hãy cùng xem các tính năng của từng ngôn ngữ, cũng như ưu và nhược điểm của chúng.

GDScript
~~~~~~~~

:ref:`GDScript<doc_gdscript>` is an
Ngôn ngữ lập trình `hướng đối tượng <https://en.wikipedia.org/wiki/Object-oriented_programming>`_ và `mệnh lệnh <https://en.wikipedia.org/wiki/Imperative_programming>`_ được xây dựng cho Godot. Ngôn ngữ này do các nhà phát triển trò chơi tạo ra dành cho các nhà phát triển trò chơi, giúp bạn tiết kiệm thời gian lập trình trò chơi. Các tính năng bao gồm:

- Cú pháp đơn giản giúp tạo ra các tệp ngắn gọn. - Thời gian biên dịch và tải cực nhanh. - Tích hợp chặt chẽ với trình soạn thảo, kèm tính năng hoàn thành mã cho các nút, tín hiệu và nhiều thông tin khác từ cảnh mà nó được gắn vào. - Các kiểu vector và phép biến đổi tích hợp sẵn, giúp sử dụng hiệu quả đại số tuyến tính chuyên sâu, vốn rất cần thiết cho trò chơi. - Hỗ trợ nhiều luồng hiệu quả như các ngôn ngữ định kiểu tĩnh. - Không có `bộ thu gom rác <https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)>`_ truy vết, vì tính năng này cuối cùng sẽ gây trở ngại khi tạo trò chơi. Trong hầu hết trường hợp, công cụ sẽ đếm các tham chiếu và tự quản lý bộ nhớ cho bạn theo mặc định, nhưng bạn cũng có thể kiểm soát bộ nhớ nếu cần. - `Định kiểu dần dần <https://en.wikipedia.org/wiki/Gradual_typing>`_. Theo mặc định, biến có kiểu động, nhưng bạn cũng có thể sử dụng gợi ý kiểu để kiểm tra kiểu chặt chẽ.

GDScript trông giống Python vì bạn cấu trúc các khối mã bằng thụt lề, nhưng trên thực tế nó không hoạt động theo cùng một cách. Ngôn ngữ này lấy cảm hứng từ nhiều ngôn ngữ, bao gồm Squirrel, Lua và Python.

.. note::

    Tại sao chúng ta không sử dụng trực tiếp Python hoặc Lua?

    Nhiều năm trước, Godot từng sử dụng Python, sau đó là Lua. Việc tích hợp cả hai ngôn ngữ đều đòi hỏi nhiều công sức và có những hạn chế nghiêm trọng. Ví dụ, hỗ trợ đa luồng là một thách thức lớn với Python.

    Việc phát triển một ngôn ngữ chuyên dụng không khiến chúng tôi tốn thêm nhiều công sức, đồng thời cho phép chúng tôi tùy chỉnh ngôn ngữ theo nhu cầu của các nhà phát triển trò chơi. Hiện chúng tôi đang nghiên cứu các tối ưu hóa hiệu năng và những tính năng mà sẽ khó cung cấp nếu sử dụng các ngôn ngữ bên thứ ba.

.NET / C#
~~~~~~~~~

Vì `C# <https://en.wikipedia.org/wiki/C_Sharp_(programming_language)>`_ của Microsoft được các nhà phát triển trò chơi ưa chuộng, chúng tôi chính thức hỗ trợ ngôn ngữ này. C# là một ngôn ngữ trưởng thành và linh hoạt với rất nhiều thư viện được viết cho nó. Chúng tôi có thể bổ sung hỗ trợ cho ngôn ngữ này nhờ một khoản quyên góp hào phóng từ Microsoft.

.. image:: img/scripting_csharp.png

C# mang lại sự cân bằng tốt giữa hiệu năng và tính dễ sử dụng, mặc dù bạn nên lưu ý đến bộ thu gom rác của nó.

.. note:: You must use the .NET edition of the Godot editor to script in C#. You
          có thể tải xuống từ trang `download <https://godotengine.org/download/>`_ trên website của Godot.

Vì Godot sử dụng .NET 8, về lý thuyết, bạn có thể sử dụng bất kỳ thư viện hoặc framework .NET bên thứ ba nào trong Godot, cũng như bất kỳ ngôn ngữ lập trình nào tuân thủ Common Language Infrastructure, chẳng hạn như F#, Boo hoặc ClojureCLR. Tuy nhiên, C# là tùy chọn .NET duy nhất được hỗ trợ chính thức.

.. note:: GDScript code itself doesn't execute as fast as compiled C# or C++.
          Tuy nhiên, hầu hết mã tập lệnh đều gọi các hàm được viết bằng những thuật toán nhanh trong mã C++ bên trong công cụ. Trong nhiều trường hợp, việc viết logic trò chơi bằng GDScript, C# hoặc C++ sẽ không ảnh hưởng đáng kể đến hiệu năng.

.. attention::

    Các dự án viết bằng C# sử dụng Godot 4 hiện chưa thể được xuất sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3. Khả năng hỗ trợ nền tảng Android và iOS đã có từ Godot 4.2, nhưng đang ở trạng thái thử nghiệm và :ref:`some limitations apply <doc_c_sharp_platforms>`.

.. seealso:: To learn more about C#, head to the :ref:`doc_c_sharp` section.

C++ thông qua GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~

GDExtension cho phép bạn viết mã trò chơi bằng C++ mà không cần biên dịch lại Godot.

.. image:: img/scripting_cpp.png

Bạn có thể sử dụng bất kỳ phiên bản nào của ngôn ngữ, hoặc kết hợp các thương hiệu và phiên bản trình biên dịch cho các thư viện dùng chung được tạo ra, nhờ việc chúng tôi sử dụng C API Bridge nội bộ.

GDExtension là lựa chọn tốt nhất cho hiệu năng. Bạn không cần sử dụng nó cho toàn bộ trò chơi, vì có thể viết các phần khác bằng GDScript hoặc C#.

Khi làm việc với GDExtension, các kiểu, hàm và thuộc tính hiện có gần như tương tự API C++ thực tế của Godot.

Tóm tắt
-------

Tập lệnh là các tệp chứa mã mà bạn gắn vào một nút để mở rộng chức năng của nút đó.

Godot hỗ trợ bốn ngôn ngữ lập trình bằng tập lệnh chính thức, mang lại cho bạn sự linh hoạt trong việc cân bằng giữa hiệu năng và tính dễ sử dụng.

Bạn có thể kết hợp các ngôn ngữ, chẳng hạn như triển khai các thuật toán đòi hỏi nhiều tài nguyên bằng C hoặc C++, đồng thời viết phần lớn logic trò chơi bằng GDScript hoặc C#.
