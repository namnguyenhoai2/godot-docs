:allow_comments: False

.. _doc_about_intro:

Giới thiệu
==========

.. tabs::
 .. code-tab:: gdscript

    func _ready(): print("Hello world!")

 .. code-tab:: csharp

    public override void _Ready() { GD.Print("Hello world!"); }

Chào mừng bạn đến với tài liệu chính thức của **Godot Engine**, công cụ phát triển game 2D và 3D miễn phí, mã nguồn mở và do cộng đồng định hướng! Đằng sau cái tên dài dòng này là một công cụ mạnh mẽ nhưng thân thiện với người dùng, cho phép bạn phát triển mọi loại game trên bất kỳ nền tảng nào mà không có bất kỳ hạn chế sử dụng nào.

Trang này cung cấp phần tổng quan khái quát về engine và tài liệu này, để bạn biết nên bắt đầu từ đâu nếu là người mới, hoặc tìm thông tin ở đâu nếu cần biết về một tính năng cụ thể.

Trước khi bắt đầu
-----------------

Trang :ref:`Tutorials and resources <doc_community_tutorials>` liệt kê các hướng dẫn bằng video do cộng đồng đóng góp. Nếu thích video hơn văn bản, hãy xem qua chúng. Nếu không, :ref:`Getting Started <doc_getting_started_intro>` là một điểm khởi đầu tuyệt vời.

Nếu gặp khó khăn với một trong các hướng dẫn hoặc với dự án của mình, bạn có thể tìm trợ giúp trên nhiều `kênh cộng đồng <https://godotengine.org/community/>`_ khác nhau, đặc biệt là cộng đồng `Discord <https://discord.gg/godotengine>`_ và `Forum <https://forum.godotengine.org/>`_ của Godot.

Về Godot Engine
---------------

Một game engine là một công cụ phức tạp và khó giới thiệu chỉ bằng vài từ. Sau đây là phần tóm tắt nhanh mà bạn có thể tự do sử dụng nếu cần một đoạn giới thiệu ngắn về Godot Engine:

    Godot Engine là một game engine đa nền tảng, tích hợp đầy đủ tính năng, dùng để tạo game 2D và 3D từ một giao diện thống nhất. Engine cung cấp một bộ công cụ phổ biến toàn diện, để người dùng có thể tập trung vào việc làm game mà không phải phát minh lại bánh xe. Game có thể được xuất chỉ bằng một cú nhấp chuột sang nhiều nền tảng, bao gồm các nền tảng máy tính để bàn chính (Linux, macOS, Windows), nền tảng di động (Android, iOS), cũng như các nền tảng dựa trên Web và máy chơi game.

    Godot hoàn toàn miễn phí và mã nguồn mở theo :ref:`permissive MIT license <doc_complying_with_licenses>`. Không ràng buộc, không phí bản quyền, không gì cả. Game của người dùng thuộc về chính họ, cho đến dòng mã cuối cùng của engine. Việc phát triển Godot hoàn toàn độc lập và do cộng đồng định hướng, trao quyền cho người dùng góp phần định hình engine sao cho phù hợp với kỳ vọng của họ. Godot được hỗ trợ bởi tổ chức phi lợi nhuận `Godot Foundation <https://godot.foundation/>`_.


Cấu trúc tài liệu
-----------------

Tài liệu này được tổ chức thành một số phần:

- **About** bao gồm phần giới thiệu này cũng như thông tin về engine, lịch sử, giấy phép, tác giả, v.v. Phần này cũng chứa :ref:`doc_faq`. - **Getting Started** chứa mọi thông tin cần thiết về việc sử dụng engine để làm game. Phần này bắt đầu với mục :ref:`doc_getting_started_intro`, là điểm khởi đầu dành cho tất cả người dùng mới. **Đây là nơi tốt nhất để bắt đầu nếu bạn mới làm quen!** - **Manual** có thể được đọc hoặc tham khảo khi cần, theo bất kỳ thứ tự nào. Phần này chứa các hướng dẫn và tài liệu dành riêng cho từng tính năng. - **Engine details** chứa các phần dành cho người dùng nâng cao và những người đóng góp, với thông tin về biên dịch engine, làm việc trên trình chỉnh sửa hoặc phát triển các mô-đun C++. - **Community** dành riêng cho hoạt động của cộng đồng Godot và chứa danh sách các hướng dẫn, tài liệu bên thứ ba được đề xuất nằm ngoài tài liệu này. Phần này cũng cung cấp thông tin chi tiết về Asset Store. Trước đây, phần này cũng từng liệt kê các cộng đồng Godot, nhưng hiện chúng được liệt kê trên `Godot website <https://godotengine.org/community/>`_. - Cuối cùng, **Class reference** ghi lại đầy đủ API của Godot, đồng thời cũng có sẵn trực tiếp trong trình chỉnh sửa script của engine. Tại đây, bạn có thể tìm thông tin về tất cả các lớp, hàm, tín hiệu, v.v.

Ngoài tài liệu này, bạn cũng có thể muốn xem qua các `dự án mẫu Godot <https://github.com/godotengine/godot-demo-projects>`_ khác nhau.

Về tài liệu này
---------------

Các thành viên của cộng đồng Godot Engine liên tục viết, sửa lỗi, biên tập và cải thiện tài liệu này. Chúng tôi luôn mong muốn nhận được thêm sự trợ giúp. Bạn cũng có thể đóng góp bằng cách mở issue trên Github hoặc dịch tài liệu sang ngôn ngữ của mình. Nếu quan tâm đến việc hỗ trợ, hãy xem `How to contribute <https://contributing.godotengine.org/en/latest/organization/how_to_contribute.html>`__ và `Writing documentation <https://contributing.godotengine.org/en/latest/documentation/manual/index.html>`__, hoặc liên hệ với `Documentation team <https://godotengine.org/teams/#documentation>`_ trên `Godot Contributors Chat <https://chat.godotengine.org/>`_.

Toàn bộ nội dung tài liệu được cấp phép theo giấy phép Creative Commons Attribution 3.0 mang tính cho phép (`CC BY 3.0 <https://creativecommons.org/licenses/by/3.0/>`_), với ghi công cho "*Juan Linietsky, Ariel Manzur, and the Godot Engine community*" trừ khi có ghi chú khác.

*Chúc bạn vui vẻ khi đọc tài liệu và làm game với Godot Engine!*
