:allow_comments: False

.. _doc_about_intro:

Giới thiệu
==========

.. tabs::
 .. code-tab:: gdscript

    func _ready():
        print("Hello world!")

 .. code-tab:: csharp

    public override void _Ready()
    {
        GD.Print("Hello world!");
    }

Chào mừng bạn đến với tài liệu chính thức của **Godot Engine**, game engine 2D và 3D miễn phí, mã nguồn mở, do cộng đồng phát triển! Đằng sau cái tên dài này là một công cụ mạnh mẽ nhưng dễ sử dụng, cho phép bạn phát triển mọi loại game trên mọi nền tảng mà hoàn toàn không bị giới hạn về việc sử dụng.

Trang này cung cấp cái nhìn tổng quan về engine và tài liệu này, để bạn biết nên bắt đầu từ đâu nếu là người mới, hoặc tìm thông tin ở đâu nếu cần biết về một tính năng cụ thể.

Trước khi bắt đầu
-----------------

Trang :ref:`Tutorials and resources <doc_community_tutorials>` liệt kê các video hướng dẫn do cộng đồng đóng góp. Nếu thích video hơn văn bản, bạn nên xem qua các video này. Nếu không, :ref:`Getting Started <doc_getting_started_intro>` là một điểm khởi đầu tuyệt vời.

Nếu gặp khó khăn với một trong các bài hướng dẫn hoặc dự án của mình, bạn có thể tìm trợ giúp trên nhiều `kênh cộng đồng <https://godotengine.org/community/>`_ khác nhau, đặc biệt là cộng đồng Godot trên `Discord <https://discord.gg/godotengine>`_ và `Forum <https://forum.godotengine.org/>`_.

Giới thiệu về Godot Engine
--------------------------

Game engine là một công cụ phức tạp và khó trình bày chỉ bằng vài từ. Dưới đây là phần tóm tắt nhanh mà bạn có thể tự do sử dụng nếu cần một đoạn giới thiệu ngắn về Godot Engine:

    Godot Engine là một game engine đa nền tảng, tích hợp nhiều tính năng, dùng để tạo game 2D và 3D từ một giao diện thống nhất. Engine cung cấp một bộ công cụ phổ biến toàn diện, giúp người dùng tập trung vào việc làm game mà không phải xây dựng lại những thứ đã có. Game có thể được xuất sang nhiều nền tảng chỉ bằng một cú nhấp, bao gồm các nền tảng máy tính để bàn chính (Linux, macOS, Windows), nền tảng di động (Android, iOS), cũng như các nền tảng dựa trên Web và console.

    Godot hoàn toàn miễn phí và là mã nguồn mở theo :ref:`giấy phép MIT tự do <doc_complying_with_licenses>`. Không có ràng buộc, không có tiền bản quyền,
    nothing. Game của người dùng thuộc về chính họ, cho đến dòng mã cuối cùng của engine.
    Quá trình phát triển Godot hoàn toàn độc lập và do cộng đồng thúc đẩy, trao quyền cho người dùng tham gia định hình engine để phù hợp với mong muốn của họ. Dự án được hỗ trợ bởi tổ chức phi lợi nhuận `Godot Foundation <https://godot.foundation/>`_.


Cấu trúc của tài liệu
---------------------

Tài liệu này được chia thành một số phần:

- **About** chứa phần giới thiệu này cùng thông tin về engine, lịch sử, giấy phép, tác giả, v.v. Phần này cũng chứa :ref:`doc_faq`.
- **Getting Started** chứa mọi thông tin cần thiết để sử dụng engine làm game. Phần này bắt đầu với mục :ref:`doc_getting_started_intro`, đây nên là điểm khởi đầu cho tất cả người dùng mới. **Đây là nơi tốt nhất để bắt đầu nếu bạn là người mới!**
- **Manual** có thể được đọc hoặc tham khảo khi cần, theo bất kỳ thứ tự nào. Phần này chứa các bài hướng dẫn và tài liệu dành riêng cho từng tính năng.
- **Engine details** chứa các phần dành cho người dùng nâng cao và cộng tác viên, với thông tin về cách biên dịch engine, làm việc trên editor hoặc phát triển các module C++.
- **Community** dành riêng cho hoạt động của cộng đồng Godot và chứa danh sách các bài hướng dẫn, tài liệu bên thứ ba được đề xuất nằm ngoài tài liệu này. Phần này cũng cung cấp thông tin chi tiết về Asset Store. Trước đây, phần này cũng từng liệt kê các cộng đồng Godot, nhưng hiện chúng được liệt kê trên `trang web Godot <https://godotengine.org/community/>`_.
- Cuối cùng, **Class reference** ghi lại đầy đủ API của Godot và cũng có thể được truy cập trực tiếp trong script editor của engine. Tại đây, bạn có thể tìm thông tin về tất cả class, function, signal, v.v.

Ngoài tài liệu này, bạn cũng có thể xem qua các `dự án demo Godot <https://github.com/godotengine/godot-demo-projects>`_.

Giới thiệu về tài liệu này
--------------------------

Các thành viên trong cộng đồng Godot Engine liên tục viết, sửa, biên tập và cải thiện tài liệu này. Chúng tôi luôn mong muốn nhận được thêm sự hỗ trợ. Bạn cũng có thể đóng góp bằng cách mở issue trên Github hoặc dịch tài liệu sang ngôn ngữ của mình. Nếu muốn hỗ trợ, hãy xem `How to contribute <https://contributing.godotengine.org/en/latest/index.html>`__ và `Writing documentation <https://contributing.godotengine.org/en/latest/development/documentation/manual/index.html>`__, hoặc liên hệ với `Documentation team <https://godotengine.org/teams/#documentation>`_ trên `Godot Contributors Chat <https://chat.godotengine.org/>`_.

Toàn bộ nội dung tài liệu được cấp phép theo giấy phép Creative Commons Attribution 3.0 tự do (`CC BY 3.0 <https://creativecommons.org/licenses/by/3.0/>`_), ghi công "*Juan Linietsky, Ariel Manzur, and the Godot Engine community*" trừ khi có ghi chú khác.

*Chúc bạn đọc vui vẻ và tạo ra những game tuyệt vời với Godot Engine!*

.. _`Community channels`: https://godotengine.org/community/
.. _`Discord`: https://discord.gg/godotengine
.. _`Forum`: https://forum.godotengine.org/
.. _`Godot Foundation`: https://godot.foundation/
.. _`Godot website`: https://godotengine.org/community/
.. _`Godot demo projects`: https://github.com/godotengine/godot-demo-projects
.. _`Documentation team`: https://godotengine.org/teams/#documentation
.. _`Godot Contributors Chat`: https://chat.godotengine.org/
.. _`CC BY 3.0`: https://creativecommons.org/licenses/by/3.0/
