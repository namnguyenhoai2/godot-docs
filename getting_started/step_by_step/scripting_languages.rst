.. Intention: only introduce what a script does in general and options for
   scripting languages.

.. _doc_scripting:

Các ngôn ngữ scripting
======================

Bài học này sẽ cung cấp cho bạn cái nhìn tổng quan về các ngôn ngữ scripting hiện có trong Godot. Bạn sẽ tìm hiểu ưu và nhược điểm của từng lựa chọn. Trong phần tiếp theo, bạn sẽ viết script đầu tiên bằng GDScript.

**Script được gắn vào một node và mở rộng hành vi của node đó**. Điều này có nghĩa là script kế thừa tất cả các hàm và thuộc tính của node mà nó được gắn vào.

Ví dụ, hãy xét một game trong đó một node Camera2D đi theo một con tàu. Theo mặc định, node Camera2D đi theo node cha của nó. Hãy tưởng tượng bạn muốn camera rung khi người chơi nhận sát thương. Vì tính năng này không được tích hợp sẵn trong Godot, bạn sẽ gắn một script vào node Camera2D và lập trình hiệu ứng rung.

.. image:: img/scripting_camera_shake.gif

Các ngôn ngữ scripting hiện có
------------------------------

Godot cung cấp **bốn ngôn ngữ lập trình gameplay**: GDScript, C#, và thông qua công nghệ GDExtension, C và C++. Có thêm nhiều ngôn ngữ được cộng đồng hỗ trợ, nhưng đây là những ngôn ngữ chính thức.

Bạn có thể sử dụng nhiều ngôn ngữ trong cùng một project. Chẳng hạn, trong một team, bạn có thể viết logic gameplay bằng GDScript vì ngôn ngữ này nhanh để viết, rồi dùng C# hoặc C++ để triển khai các thuật toán phức tạp và tối đa hóa hiệu năng của chúng. Hoặc bạn có thể viết mọi thứ bằng GDScript hoặc C#. Tùy bạn lựa chọn.

Chúng tôi cung cấp sự linh hoạt này để đáp ứng nhu cầu của các project game và developer khác nhau.

Tôi nên sử dụng ngôn ngữ nào?
-----------------------------

Nếu bạn là người mới bắt đầu, chúng tôi khuyên bạn **bắt đầu với GDScript**. Chúng tôi tạo ra ngôn ngữ này dành riêng cho Godot và nhu cầu của các game developer. Ngôn ngữ này có cú pháp gọn nhẹ, đơn giản và tích hợp chặt chẽ với Godot nhất.

.. image:: img/scripting_gdscript.webp

Với C#, bạn sẽ cần một code editor bên ngoài như `VSCode <https://code.visualstudio.com/>`_ hoặc Visual Studio. Mặc dù hỗ trợ C# hiện đã hoàn thiện, bạn sẽ tìm thấy ít tài liệu học hơn so với GDScript. Vì vậy, chúng tôi chủ yếu khuyên dùng C# cho những người dùng đã có kinh nghiệm với ngôn ngữ này.

Hãy cùng xem các tính năng của từng ngôn ngữ, cũng như ưu và nhược điểm của chúng.

GDScript
~~~~~~~~

:ref:`GDScript <doc_gdscript>` là một ngôn ngữ lập trình `hướng đối tượng <https://en.wikipedia.org/wiki/Object-oriented_programming>`_ và `mệnh lệnh <https://en.wikipedia.org/wiki/Imperative_programming>`_ được xây dựng cho Godot. Ngôn ngữ này do các game developer tạo ra và dành cho game developer, giúp bạn tiết kiệm thời gian lập trình game. Các tính năng của ngôn ngữ này bao gồm:

- Cú pháp đơn giản, tạo ra các file ngắn gọn.
- Thời gian biên dịch và tải cực nhanh.
- Tích hợp chặt chẽ với editor, có tính năng hoàn thành code cho các node, signal và nhiều thông tin khác từ scene mà nó được gắn vào.
- Các kiểu vector và transform tích hợp sẵn, giúp ngôn ngữ này hiệu quả khi sử dụng nhiều đại số tuyến tính, yếu tố không thể thiếu trong game.
- Hỗ trợ nhiều thread hiệu quả như các ngôn ngữ kiểu tĩnh.
- Không có `garbage collection <https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)>`_ dạng tracing, vì tính năng này cuối cùng sẽ gây cản trở khi tạo game. Engine đếm các reference và quản lý bộ nhớ cho bạn trong hầu hết trường hợp theo mặc định, nhưng bạn cũng có thể tự kiểm soát bộ nhớ khi cần.
- `Kiểu dữ liệu linh hoạt <https://en.wikipedia.org/wiki/Gradual_typing>`_. Theo mặc định, các biến có kiểu động, nhưng bạn cũng có thể sử dụng type hint để kiểm tra kiểu chặt chẽ.

GDScript trông giống Python vì bạn cấu trúc các khối code bằng indentation, nhưng trên thực tế nó không hoạt động theo cùng một cách. Ngôn ngữ này lấy cảm hứng từ nhiều ngôn ngữ, bao gồm Squirrel, Lua và Python.

.. note::

    Tại sao chúng ta không sử dụng trực tiếp Python hoặc Lua?

    Nhiều năm trước, Godot sử dụng Python, sau đó là Lua. Việc tích hợp cả hai ngôn ngữ đều đòi hỏi rất nhiều công sức và có những hạn chế nghiêm trọng. Ví dụ, hỗ trợ threading là một thách thức lớn với Python.

    Việc phát triển một ngôn ngữ chuyên biệt không khiến chúng tôi tốn thêm nhiều công sức, đồng thời cho phép chúng tôi điều chỉnh ngôn ngữ này theo nhu cầu của game developer. Hiện nay, chúng tôi đang phát triển các tối ưu hóa hiệu năng và những tính năng mà sẽ khó cung cấp nếu sử dụng các ngôn ngữ bên thứ ba.

.NET / C#
~~~~~~~~~

Vì `C# <https://en.wikipedia.org/wiki/C_Sharp_(programming_language)>`_ của Microsoft được nhiều game developer yêu thích, chúng tôi chính thức hỗ trợ ngôn ngữ này. C# là một ngôn ngữ trưởng thành và linh hoạt, với rất nhiều library được viết cho nó. Chúng tôi có thể bổ sung hỗ trợ cho ngôn ngữ này nhờ một khoản quyên góp hào phóng từ Microsoft.

.. image:: img/scripting_csharp.png

C# mang lại sự cân bằng tốt giữa hiệu năng và tính dễ sử dụng, mặc dù bạn nên lưu ý đến garbage collector của nó.

.. note:: Bạn phải sử dụng bản .NET của Godot editor để viết script bằng C#. Bạn có thể tải bản này xuống từ trang `download <https://godotengine.org/download/>`_ trên website của Godot.

Vì Godot sử dụng .NET 8, về lý thuyết, bạn có thể dùng bất kỳ library hoặc framework .NET bên thứ ba nào trong Godot, cũng như bất kỳ ngôn ngữ lập trình nào tuân thủ Common Language Infrastructure, chẳng hạn như F#, Boo hoặc ClojureCLR. Tuy nhiên, C# là lựa chọn .NET duy nhất được hỗ trợ chính thức.

.. note:: Bản thân code GDScript không thực thi nhanh bằng C# hoặc C++ đã biên dịch. Tuy nhiên, hầu hết code script đều gọi các hàm được viết bằng những thuật toán nhanh trong code C++ bên trong engine. Trong nhiều trường hợp, việc viết logic gameplay bằng GDScript, C# hoặc C++ sẽ không ảnh hưởng đáng kể đến hiệu năng.

.. attention::

    Các project viết bằng C# sử dụng Godot 4 hiện chưa thể export sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3. Hỗ trợ nền tảng Android và iOS đã có từ Godot 4.2, nhưng vẫn đang ở trạng thái thử nghiệm và :ref:`có một số hạn chế <doc_c_sharp_platforms>`.

.. seealso:: Để tìm hiểu thêm về C#, hãy truy cập phần :ref:`doc_c_sharp`.

C++ thông qua GDExtension
~~~~~~~~~~~~~~~~~~~~~~~~~

GDExtension cho phép bạn viết code game bằng C++ mà không cần biên dịch lại Godot.

.. image:: img/scripting_cpp.png

Bạn có thể sử dụng bất kỳ phiên bản nào của ngôn ngữ này hoặc kết hợp các thương hiệu và phiên bản compiler cho các shared library được tạo ra, nhờ việc chúng tôi sử dụng một C API Bridge nội bộ.

GDExtension là lựa chọn tốt nhất cho hiệu năng. Bạn không cần sử dụng nó cho toàn bộ game, vì có thể viết các phần khác bằng GDScript hoặc C#.

Khi làm việc với GDExtension, các kiểu, hàm và thuộc tính hiện có gần giống với C++ API thực tế của Godot.

Tóm tắt
-------

Script là các file chứa code mà bạn gắn vào một node để mở rộng chức năng của node đó.

Godot hỗ trợ bốn ngôn ngữ scripting chính thức, mang lại cho bạn sự linh hoạt trong việc cân bằng giữa hiệu năng và tính dễ sử dụng.

Bạn có thể kết hợp các ngôn ngữ, chẳng hạn như triển khai các thuật toán đòi hỏi nhiều tài nguyên bằng C hoặc C++, đồng thời viết phần lớn logic game bằng GDScript hoặc C#.

.. _`VSCode`: https://code.visualstudio.com/
.. _`object-oriented`: https://en.wikipedia.org/wiki/Object-oriented_programming
.. _`imperative`: https://en.wikipedia.org/wiki/Imperative_programming
.. _`garbage collection`: https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)
.. _`Gradual typing`: https://en.wikipedia.org/wiki/Gradual_typing
.. _`C#`: https://en.wikipedia.org/wiki/C_Sharp_(programming_language)
.. _`download`: https://godotengine.org/download/
