.. _doc_changing_application_icon_for_windows:

Thay đổi thủ công biểu tượng ứng dụng cho Windows
=================================================

Các ứng dụng Windows sử dụng một định dạng chỉ dành cho Windows có tên là ICO cho biểu tượng tệp và biểu tượng trên thanh tác vụ. Kể từ Godot 4.1, Godot có thể tạo tệp ICO cho bạn dựa trên tệp biểu tượng được xác định trong export preset của Windows. Các định dạng được hỗ trợ là PNG, WebP và SVG. Nếu không có biểu tượng nào được xác định trong export preset của Windows thì
:ref:`application/config/icon <class_ProjectSettings_property_application/config/icon>`
project setting sẽ được tự động sử dụng thay thế.

Điều này có nghĩa là bạn không còn cần thực hiện các bước trong phần này để tự tạo tệp ICO, trừ khi bạn muốn kiểm soát thiết kế biểu tượng tùy theo kích thước hiển thị của biểu tượng.

Tạo tệp ICO tùy chỉnh
---------------------

Bạn có thể tạo biểu tượng ứng dụng bằng bất kỳ chương trình nào, nhưng bạn sẽ phải chuyển đổi nó sang tệp ICO bằng một chương trình như GIMP.

`This video tutorial <https://www.youtube.com/watch?v=uqV3UfM-n5Y>`_ hướng dẫn cách export tệp ICO bằng GIMP.

Bạn cũng có thể chuyển đổi hình ảnh PNG thành tệp ICO thân thiện với hiDPI bằng lệnh `ImageMagick <https://www.imagemagick.org/>`_ này:

.. code-block:: none

    magick icon.png -define icon:auto-resize=256,128,64,48,32,16 icon.ico

Tùy thuộc vào phiên bản ImageMagick đã cài đặt, bạn có thể cần sử dụng lệnh này thay thế:

.. code-block:: none

    convert icon.png -define icon:auto-resize=256,128,64,48,32,16 icon.ico

.. warning::

    Để tệp ICO thay thế hiệu quả biểu tượng Godot mặc định, tệp đó phải chứa *tất cả* các kích thước có trong biểu tượng Godot mặc định: 16×16, 32×32, 48×48, 64×64, 128×128, 256×256. Nếu tệp ICO không chứa tất cả các kích thước, biểu tượng Godot mặc định sẽ được giữ lại cho những kích thước chưa bị ghi đè.

    Lệnh ImageMagick ở trên đã tính đến điều này.

Thay đổi biểu tượng trên thanh tác vụ
-------------------------------------

Biểu tượng trên thanh tác vụ là biểu tượng xuất hiện trên thanh tác vụ khi project của bạn đang chạy.

.. image:: img/icon_taskbar_icon.png

Để thay đổi biểu tượng trên thanh tác vụ, hãy vào **Project > Project Settings > Application > Config**, đảm bảo **Advanced Settings** được bật để nhìn thấy cài đặt này, sau đó vào ``Windows Native Icon``. Nhấp vào biểu tượng thư mục và chọn tệp ICO của bạn.

.. image:: img/icon_project_settings.webp

Cài đặt này chỉ thay đổi biểu tượng cho game đã export trên Windows. Để đặt biểu tượng cho macOS, hãy sử dụng ``Macos Native Icon``. Với mọi nền tảng khác, hãy sử dụng cài đặt ``Icon``.

.. _doc_changing_application_icon_for_windows_changing_the_file_icon:

Thay đổi biểu tượng tệp
-----------------------

Biểu tượng tệp là biểu tượng của tệp thực thi mà bạn nhấp vào để khởi động project.

.. image:: img/icon_file_icon.png

Để thực hiện việc này, bạn cần chỉ định biểu tượng khi export. Vào **Project > Export**. Giả sử bạn đã tạo một preset Windows Desktop, hãy chọn biểu tượng ở định dạng ICO trong trường **Application > Icon**.

.. image:: img/icon_export_settings.webp

Kiểm tra kết quả
----------------

Bây giờ bạn có thể export project. Nếu mọi thứ hoạt động chính xác, bạn sẽ thấy như sau:

.. image:: img/icon_result.png

.. note::

    Nếu biểu tượng của bạn không hiển thị đúng cách, hãy thử xóa bộ nhớ đệm biểu tượng. Để thực hiện việc này, hãy mở hộp thoại **Run** và nhập ``ie4uinit.exe -ClearIconCache`` hoặc ``ie4uinit.exe -show``.
