.. _doc_project_organization:

Tổ chức dự án
=============

Giới thiệu
----------

Vì Godot không áp đặt hạn chế về cấu trúc dự án hoặc cách sử dụng hệ thống tệp, việc tổ chức tệp khi học engine có thể khá khó khăn. Hướng dẫn này đề xuất một quy trình làm việc phù hợp để bắt đầu. Chúng ta cũng sẽ tìm hiểu cách sử dụng kiểm soát phiên bản với Godot.

Tổ chức
-------

Godot về bản chất hoạt động dựa trên scene và sử dụng hệ thống tệp nguyên trạng, không có metadata hoặc cơ sở dữ liệu asset.

Không giống các engine khác, nhiều resource được chứa ngay trong scene, vì vậy số lượng tệp trong hệ thống tệp thấp hơn đáng kể.

Vì vậy, cách tiếp cận phổ biến nhất là nhóm các asset gần với scene nhất có thể; khi dự án phát triển, cách này giúp việc bảo trì dễ dàng hơn.

Ví dụ, thông thường bạn có thể đặt các asset cơ bản như hình ảnh sprite, mesh mô hình 3D, material và nhạc vào cùng một thư mục. Sau đó, bạn có thể dùng một thư mục riêng để lưu trữ các level đã xây dựng sử dụng chúng.

.. code-block:: none

    /project.godot
    /docs/.gdignore  # See "Ignoring specific folders" below
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

Hướng dẫn về quy ước
--------------------

Để đảm bảo tính nhất quán giữa các dự án, chúng tôi khuyến nghị tuân theo các hướng dẫn sau:

- Sử dụng **snake_case** cho tên thư mục và tệp (ngoại trừ script C#). Cách này tránh được các vấn đề phân biệt chữ hoa chữ thường có thể phát sinh sau khi export dự án trên Windows. Script C# là ngoại lệ của quy tắc này, vì quy ước là đặt tên theo tên class, vốn phải sử dụng PascalCase.
- Sử dụng **PascalCase** cho tên node, vì cách này phù hợp với quy ước viết hoa của các node tích hợp sẵn.
- Nhìn chung, hãy giữ các resource của bên thứ ba trong một thư mục ``addons/`` cấp cao nhất, ngay cả khi chúng không phải là plugin của editor. Điều này giúp dễ dàng xác định tệp nào là của bên thứ ba. Quy tắc này có một số ngoại lệ; chẳng hạn, nếu bạn sử dụng asset game của bên thứ ba cho một nhân vật, sẽ hợp lý hơn nếu đặt chúng trong cùng thư mục với các scene và script của nhân vật đó.

Import
------

Các phiên bản Godot trước 3.0 thực hiện quá trình import từ các tệp bên ngoài dự án. Mặc dù điều này có thể hữu ích trong các dự án lớn, nó lại khiến việc tổ chức trở nên rắc rối đối với phần lớn developer.

Vì vậy, asset hiện được import một cách minh bạch từ bên trong thư mục dự án. Xem :ref:`doc_import_process` để biết thêm chi tiết về cách import hoạt động trong Godot.

.. _doc_project_organization_ignoring_specific_folders:

Bỏ qua các thư mục cụ thể
~~~~~~~~~~~~~~~~~~~~~~~~~

Để ngăn Godot import các tệp nằm trong một thư mục cụ thể, hãy tạo một tệp trống có tên ``.gdignore`` trong thư mục đó (bắt buộc phải có ``.`` ở đầu). Cách này có thể hữu ích để tăng tốc quá trình import dự án ban đầu.

.. note::

    Để tạo một tệp có tên bắt đầu bằng dấu chấm trên Windows, hãy đặt dấu chấm ở cả đầu và cuối tên tệp (``.gdignore.``). Windows sẽ tự động xóa dấu chấm ở cuối khi bạn xác nhận tên.

    Ngoài ra, bạn có thể sử dụng trình soạn thảo văn bản như Notepad++ hoặc dùng lệnh sau trong command prompt: ``type nul > .gdignore``

Sau khi thư mục bị bỏ qua, resource trong thư mục đó sẽ không thể được tải nữa bằng các phương thức ``load()`` và ``preload()``. Việc bỏ qua một thư mục cũng sẽ tự động ẩn thư mục đó khỏi dock FileSystem, giúp giảm sự lộn xộn.

Lưu ý rằng nội dung của tệp ``.gdignore`` bị bỏ qua, vì vậy tệp này phải để trống. Tệp này không hỗ trợ các pattern như các tệp ``.gitignore``.

.. _doc_project_organization_case_sensitivity:

Phân biệt chữ hoa chữ thường
----------------------------

Windows và các phiên bản macOS gần đây mặc định sử dụng hệ thống tệp không phân biệt chữ hoa chữ thường, trong khi các bản phân phối Linux mặc định sử dụng hệ thống tệp phân biệt chữ hoa chữ thường. Điều này có thể gây ra vấn đề sau khi export dự án, vì hệ thống tệp ảo PCK của Godot phân biệt chữ hoa chữ thường. Để tránh vấn đề này, bạn nên sử dụng quy tắc đặt tên ``snake_case`` cho tất cả tệp trong dự án (và nói chung là dùng ký tự viết thường).

.. note::

    Bạn có thể phá vỡ quy tắc này khi hướng dẫn về quy ước yêu cầu khác (chẳng hạn như hướng dẫn về quy ước C#). Tuy vậy, hãy giữ tính nhất quán để tránh sai sót.

Trên Windows 10, để tránh thêm các sai sót liên quan đến việc phân biệt chữ hoa chữ thường, bạn cũng có thể bật chế độ phân biệt chữ hoa chữ thường cho thư mục dự án. Sau khi bật tính năng Windows Subsystem for Linux, hãy chạy lệnh sau trong cửa sổ PowerShell:

::

    # To enable case-sensitivity:
    fsutil file setcasesensitiveinfo <path to project folder> enable

    # To disable case-sensitivity:
    fsutil file setcasesensitiveinfo <path to project folder> disable

Nếu chưa bật Windows Subsystem for Linux, bạn có thể nhập dòng sau trong cửa sổ PowerShell *chạy với quyền Administrator*, sau đó khởi động lại khi được yêu cầu:

::

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
