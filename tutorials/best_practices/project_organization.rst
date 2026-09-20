.. _doc_project_organization:

Tổ chức dự án
=============

Giới thiệu
----------

Vì Godot không áp đặt hạn chế nào về cấu trúc dự án hoặc cách sử dụng hệ thống tệp, việc tổ chức tệp khi học engine có thể có vẻ khá thử thách. Tutorial này đề xuất một quy trình làm việc có thể là điểm khởi đầu tốt. Chúng ta cũng sẽ tìm hiểu cách sử dụng version control với Godot.

Tổ chức
-------

Godot về bản chất là một engine dựa trên scene và sử dụng hệ thống tệp nguyên trạng, không có metadata hoặc asset database.

Khác với các engine khác, nhiều resource được chứa ngay trong scene, vì vậy số lượng tệp trong hệ thống tệp thấp hơn đáng kể.

Xét đến điều đó, cách tiếp cận phổ biến nhất là nhóm các asset càng gần scene càng tốt; khi dự án phát triển, cách này giúp việc bảo trì dễ dàng hơn.

Ví dụ, thông thường bạn có thể đặt các asset cơ bản như ảnh sprite, mesh model 3D, material và nhạc, v.v. vào một thư mục duy nhất. Sau đó, bạn có thể dùng một thư mục riêng để lưu các level đã xây dựng sử dụng chúng.

.. code-block:: none

    /project.godot
    /docs/.gdignore  # Xem mục "Bỏ qua các thư mục cụ thể" bên dưới
    /docs/learning.html
    /models/town/house/house.dae
    /models/town/house/window.png
    /models/town/house/door.png
    /characters/player/cubio.dae
    /characters/player/cubio.png
    /characters/enemies/goblin/goblin.dae
    /characters/enemies/goblin/goblin.png
    /characters/npcs/suzanne/suzanne.dae
    /characters/npcs/suzanne/suzanne.png
    /levels/riverdale/riverdale.scn

Style guide
-----------

Để đảm bảo tính nhất quán giữa các dự án, chúng tôi khuyến nghị tuân theo các nguyên tắc sau:

- Sử dụng **snake_case** cho tên thư mục và tệp (ngoại trừ C# script). Cách này tránh các vấn đề phân biệt chữ hoa chữ thường có thể phát sinh sau khi export dự án trên Windows. C# script là ngoại lệ của quy tắc này, vì quy ước là đặt tên theo tên class, vốn phải ở dạng PascalCase. - Sử dụng **PascalCase** cho tên node, phù hợp với cách viết hoa tên node tích hợp sẵn. - Nhìn chung, hãy giữ các resource bên thứ ba trong một thư mục ``addons/`` ở cấp cao nhất, ngay cả khi chúng không phải là editor plugin. Điều này giúp dễ dàng theo dõi tệp nào là của bên thứ ba. Có một số ngoại lệ cho quy tắc này; chẳng hạn, nếu bạn sử dụng asset game bên thứ ba cho một nhân vật, sẽ hợp lý hơn nếu đưa chúng vào cùng thư mục với các scene và script của nhân vật.

Import
------

Các phiên bản Godot trước 3.0 thực hiện quy trình import từ các tệp bên ngoài dự án. Mặc dù cách này có thể hữu ích trong các dự án lớn, nó lại gây khó khăn cho việc tổ chức đối với hầu hết developer.

Vì lý do này, asset hiện được import trong suốt từ bên trong thư mục dự án. Xem :ref:`doc_import_process` để biết thêm chi tiết về cách import hoạt động trong Godot.

.. _doc_project_organization_ignoring_specific_folders:

Bỏ qua các thư mục cụ thể
~~~~~~~~~~~~~~~~~~~~~~~~~

Để ngăn Godot import các tệp nằm trong một thư mục cụ thể, hãy tạo một tệp rỗng có tên ``.gdignore`` trong thư mục đó (ký tự ``.`` ở đầu là bắt buộc). Điều này có thể hữu ích để tăng tốc quá trình import dự án ban đầu.

.. note::

    Để tạo một tệp có tên bắt đầu bằng dấu chấm trên Windows, hãy đặt một dấu chấm ở cả đầu và cuối tên tệp (``.gdignore.``). Windows sẽ tự động xóa dấu chấm ở cuối khi bạn xác nhận tên.

    Ngoài ra, bạn có thể sử dụng trình soạn thảo văn bản như Notepad++ hoặc sử dụng lệnh sau trong command prompt: ``type nul > .gdignore``

Sau khi thư mục bị bỏ qua, resource trong thư mục đó sẽ không thể được tải bằng các phương thức ``load()`` và ``preload()``. Việc bỏ qua một thư mục cũng sẽ tự động ẩn thư mục đó khỏi dock FileSystem, điều này có thể hữu ích để giảm sự lộn xộn.

Lưu ý rằng nội dung của tệp ``.gdignore`` bị bỏ qua, đó là lý do tệp này phải rỗng. Tệp này không hỗ trợ các pattern như các tệp ``.gitignore``.

.. _doc_project_organization_case_sensitivity:

Phân biệt chữ hoa chữ thường
----------------------------

Windows và các phiên bản macOS gần đây mặc định sử dụng hệ thống tệp không phân biệt chữ hoa chữ thường, trong khi các bản phân phối Linux mặc định sử dụng hệ thống tệp có phân biệt chữ hoa chữ thường. Điều này có thể gây ra sự cố sau khi export dự án, vì hệ thống tệp ảo PCK của Godot có phân biệt chữ hoa chữ thường. Để tránh điều này, bạn nên dùng quy tắc đặt tên ``snake_case`` cho tất cả tệp trong dự án (và nhìn chung sử dụng ký tự viết thường).

.. note::

    Bạn có thể phá vỡ quy tắc này khi style guide quy định khác (chẳng hạn như C# style guide). Tuy nhiên, hãy nhất quán để tránh sai sót.

Trên Windows 10, để tiếp tục tránh các sai sót liên quan đến việc phân biệt chữ hoa chữ thường, bạn cũng có thể đặt thư mục dự án ở chế độ phân biệt chữ hoa chữ thường. Sau khi bật tính năng Windows Subsystem for Linux, hãy chạy lệnh sau trong cửa sổ PowerShell:

::

    # Để bật chế độ phân biệt chữ hoa chữ thường:
    fsutil file setcasesensitiveinfo <path to project folder> enable

    # Để tắt chế độ phân biệt chữ hoa chữ thường:
    fsutil file setcasesensitiveinfo <path to project folder> disable

Nếu chưa bật Windows Subsystem for Linux, bạn có thể nhập dòng sau trong cửa sổ PowerShell *đang chạy với quyền Administrator*, sau đó khởi động lại khi được yêu cầu:

::

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
