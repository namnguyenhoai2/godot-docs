.. _doc_exporting_for_dedicated_servers:

Xuất cho máy chủ dedicated
==========================

.. highlight:: none

Nếu bạn muốn chạy máy chủ dedicated cho dự án trên một máy không có GPU hoặc display server, bạn cần chạy Godot với display server ``headless`` và trình điều khiển âm thanh ``Dummy`` :ref:`audio driver <class_ProjectSettings_property_audio/driver/driver>`.

Kể từ Godot 4.0, bạn có thể thực hiện việc này bằng cách chạy một binary Godot trên bất kỳ nền tảng nào với đối số dòng lệnh ``--headless``, hoặc chạy một dự án được xuất dưới dạng máy chủ dedicated. Bạn không còn cần sử dụng binary máy chủ chuyên dụng như trong Godot 3.x.

Editor so với export template
-----------------------------

Bạn có thể sử dụng binary editor hoặc export template (debug hoặc release) ở chế độ headless. Việc nên sử dụng loại nào tùy thuộc vào trường hợp của bạn:

- **Export template:** Sử dụng loại này để chạy máy chủ dedicated. Nó không chứa chức năng editor, vì vậy có kích thước nhỏ hơn và được tối ưu hóa tốt hơn.
- **Editor:** Binary này chứa chức năng editor và предназнач để xuất các dự án. Binary này *có thể* được dùng để chạy máy chủ dedicated, nhưng không được khuyến nghị vì có kích thước lớn hơn và được tối ưu hóa kém hơn.

Các phương pháp xuất
--------------------

Có hai cách để xuất một dự án cho máy chủ:

- Tạo một export preset riêng cho nền tảng sẽ lưu trữ máy chủ, sau đó xuất dự án như bình thường.
- Chỉ xuất một tệp PCK, tốt nhất là cho nền tảng tương ứng với nền tảng sẽ lưu trữ máy chủ. Đặt tệp PCK này trong cùng thư mục với một binary export template, đổi tên binary để có cùng tên với PCK (bỏ phần mở rộng tệp), rồi chạy binary.

Cả hai phương pháp đều cho ra kết quả giống hệt nhau. Phần còn lại của trang này sẽ tập trung vào phương pháp đầu tiên.

Xem :ref:`doc_exporting_projects` để biết thêm thông tin.

.. _doc_exporting_for_dedicated_servers_exporting_project:

Xuất một dự án cho máy chủ dedicated
------------------------------------

Nếu bạn xuất một dự án như bình thường khi nhắm đến máy chủ, bạn sẽ nhận thấy tệp PCK có kích thước lớn tương đương phía client. Điều này là vì nó bao gồm tất cả tài nguyên, kể cả những tài nguyên máy chủ không cần (chẳng hạn như dữ liệu texture). Ngoài ra, chế độ headless sẽ không được tự động sử dụng; người dùng phải chỉ định ``--headless`` để đảm bảo không có cửa sổ nào được tạo.

Nhiều tài nguyên như texture có thể được loại bỏ khỏi tệp PCK để giảm đáng kể kích thước. Godot cung cấp cách thực hiện việc này với texture và material mà vẫn bảo toàn các tham chiếu trong tệp scene hoặc resource (tích hợp hoặc bên ngoài).

Để bắt đầu, hãy đảm bảo bạn có một export preset riêng cho máy chủ, sau đó chọn preset đó, đi đến tab **Resources** và thay đổi chế độ xuất:

.. figure:: img/exporting_for_dedicated_servers_export_mode.webp
   :align: center
   :alt: Chọn chế độ xuất **Export as dedicated server** trong export preset

   Chọn chế độ xuất **Export as dedicated server** trong export preset

Khi chọn chế độ xuất này, thẻ tính năng ``dedicated_server`` sẽ được tự động thêm vào dự án đã xuất.

.. note::

    Nếu bạn không muốn sử dụng chế độ xuất này nhưng vẫn muốn có thẻ tính năng, bạn có thể viết tên ``dedicated_server`` trong tab **Features** của export preset. Việc này cũng sẽ buộc sử dụng ``--headless`` khi chạy dự án đã xuất.

Sau khi chọn chế độ xuất này, bạn sẽ thấy danh sách tài nguyên trong dự án:

.. figure:: img/exporting_for_dedicated_servers_export_resources.webp
   :align: center
   :alt: Chọn các tài nguyên cần giữ nguyên, giữ lại với phần hiển thị đã lược bỏ hoặc loại bỏ

   Chọn các tài nguyên cần giữ nguyên, giữ lại với phần hiển thị đã lược bỏ hoặc loại bỏ

Đánh dấu một ô cho phép bạn ghi đè các tùy chọn cho tệp hoặc thư mục được chỉ định. Việc đánh dấu các ô **không** ảnh hưởng đến việc tệp nào được xuất; điều này được quyết định bởi các tùy chọn được chọn cho từng ô thay vào đó.

Theo mặc định, các tệp trong thư mục đã đánh dấu sẽ tự động sử dụng tùy chọn của thư mục cha. Điều này được thể hiện bằng hậu tố **(Inherited)** trong tên tùy chọn (và tên tùy chọn sẽ bị làm mờ). Để thay đổi tùy chọn cho một tệp hiện đang kế thừa, trước tiên bạn phải đánh dấu ô bên cạnh tệp đó.

- **Strip Visuals:** Xuất tài nguyên này, trong đó các tệp hiển thị (texture và material) được thay thế bằng các lớp placeholder. Các lớp placeholder lưu kích thước hình ảnh (vì đôi khi kích thước này được dùng để định vị các phần tử trong scene 2D), nhưng không lưu thông tin nào khác.
- **Keep:** Xuất tài nguyên này như bình thường, giữ nguyên các tệp hiển thị.
- **Remove:** Tệp không được đưa vào PCK. Tùy chọn này hữu ích để bỏ qua các scene và resource chỉ client cần. Nếu làm vậy, hãy đảm bảo máy chủ không tham chiếu đến các scene và resource chỉ dành cho client này theo bất kỳ cách nào.

Khuyến nghị chung là sử dụng **Strip Visuals** bất cứ khi nào có thể, trừ khi máy chủ cần truy cập dữ liệu hình ảnh, chẳng hạn như màu của các pixel. Ví dụ, nếu máy chủ tạo dữ liệu collision dựa trên nội dung của một hình ảnh, bạn cần sử dụng **Keep** cho hình ảnh cụ thể đó.

.. tip::

    Để kiểm tra cấu trúc tệp của PCK đã xuất, hãy sử dụng nút **Export PCK/ZIP...** với phần mở rộng tệp ``.zip``, sau đó mở tệp ZIP kết quả bằng trình quản lý tệp.

.. warning::

    Hãy cẩn thận khi sử dụng chế độ **Remove**, vì các scene/resource tham chiếu đến tệp đã bị loại bỏ sẽ không còn có thể tải thành công.

    Nếu muốn loại bỏ các resource cụ thể nhưng vẫn cho phép scene tải mà không có chúng, bạn sẽ phải xóa tham chiếu trong tệp scene và tải các tệp vào các thuộc tính của node bằng ``load()`` trong một script. Phương pháp này có thể được dùng để loại bỏ các resource mà Godot hiện chưa hỗ trợ thay thế bằng placeholder, chẳng hạn như audio.

    Việc loại bỏ texture thường là yếu tố tạo ra tác động lớn nhất đến kích thước PCK, vì vậy trước tiên bạn nên sử dụng **Strip Visuals**.

Với các tùy chọn trên, PCK dành cho client (xuất tất cả resource theo cách bình thường) sẽ có cấu trúc như sau:

::

    .
    ├── .godot
    │   ├── exported
    │   │   └── 133200997
    │   │       └── export-78c237d4bfdb4e1d02e0b5f38ddfd8bd-scene.scn
    │   ├── global_script_class_cache.cfg
    │   ├── imported
    │   │   ├── map_data.png-ce840618f399a990343bfc7298195a13.ctex
    │   │   ├── music.ogg-fa883da45ae49695a3d022f64e60aee2.oggvorbisstr
    │   │   └── sprite.png-7958af25f91bb9dbae43f35388f8e840.ctex
    │   └── uid_cache.bin
    ├── client
    │   ├── music.ogg.import
    │   └── sprite.png.import
    ├── server
    │   └── map_data.png.import
    ├── test
    │   └── scene.gd
    └── unused
    │   └── development_test.gd
    ├── project.binary
    ├── scene.gd
    ├── scene.tscn.remap

Cấu trúc tệp PCK dành cho máy chủ sẽ có dạng như sau:

::

    .
    ├── .godot
    │   ├── exported
    │   │   └── 3400186661
    │   │       ├── export-78c237d4bfdb4e1d02e0b5f38ddfd8bd-scene.scn
    │   │       ├── export-7958af25f91bb9dbae43f35388f8e840-sprite.res  # Placeholder texture
    │   │       └── export-fa883da45ae49695a3d022f64e60aee2-music.res
    │   ├── global_script_class_cache.cfg
    │   ├── imported
    │   │   └── map_data.png-ce840618f399a990343bfc7298195a13.ctex
    │   └── uid_cache.bin
    ├── client
    │   ├── music.ogg.import
    │   └── sprite.png.import  # Points to placeholder texture
    └── server
    │   └── map_data.png.import
    ├── project.binary
    ├── scene.gd
    ├── scene.tscn.remap

Khởi động máy chủ dedicated
---------------------------

Nếu client và máy chủ của bạn cùng thuộc một dự án Godot, bạn sẽ phải thêm cách khởi động máy chủ trực tiếp bằng một đối số dòng lệnh.

Nếu bạn :ref:`đã xuất project <doc_exporting_for_dedicated_servers_exporting_project>` bằng chế độ xuất **Export as dedicated server** (hoặc đã thêm ``dedicated_server`` dưới dạng feature tag tùy chỉnh), bạn có thể sử dụng feature tag ``dedicated_server`` để phát hiện xem có đang sử dụng PCK của dedicated server hay không:

.. tabs::
 .. code-tab:: gdscript

    # Lưu ý: Feature tag phân biệt chữ hoa chữ thường.
    if OS.has_feature("dedicated_server"):
        # Chạy mã khởi động server của bạn tại đây...
        pass

 .. code-tab:: csharp

    // Lưu ý: Feature tag phân biệt chữ hoa chữ thường.
    if (OS.HasFeature("dedicated_server"))
    {
        // Chạy mã khởi động server của bạn tại đây...
    }

Nếu bạn cũng muốn host một server khi sử dụng đối số dòng lệnh tích hợp sẵn ``--headless``, bạn có thể thực hiện việc này bằng cách thêm đoạn mã sau vào phương thức ``_ready()`` của main scene (hoặc autoload):

.. tabs::
 .. code-tab:: gdscript

    if DisplayServer.get_name() == "headless":
        # Chạy mã khởi động server của bạn tại đây...
        #
        # Với phép kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        # một binary Godot (editor hoặc export template) với đối số `--headless`
        # trên dòng lệnh.
        pass

 .. code-tab:: csharp

    using System.Linq;

    if (DisplayServer.GetName() == "headless")
    {
        // Chạy mã khởi động server của bạn tại đây...
        //
        // Với phép kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        // một binary Godot (editor hoặc export template) với đối số `--headless`
        // trên dòng lệnh.
    }

Nếu bạn muốn sử dụng một đối số dòng lệnh tùy chỉnh, bạn có thể thực hiện việc này bằng cách thêm đoạn mã sau vào phương thức ``_ready()`` của main scene (hoặc autoload):

.. tabs::
 .. code-tab:: gdscript

    if "--server" in OS.get_cmdline_user_args():
        # Chạy mã khởi động server của bạn tại đây...
        #
        # Với phép kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        # một binary Godot (editor hoặc export template) với đối số `--server`
        # trên dòng lệnh.
        pass

 .. code-tab:: csharp

    using System.Linq;

    if (OS.GetCmdlineUserArgs().Contains("--server"))
    {
        // Chạy mã khởi động server của bạn tại đây...
        //
        // Với phép kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        // một binary Godot (editor hoặc export template) với đối số `--server`
        // trên dòng lệnh.
    }

Bạn nên thêm ít nhất một trong các đối số dòng lệnh trên để khởi động server, vì chúng có thể được dùng để kiểm thử chức năng server từ dòng lệnh mà không cần export project.

Nếu client và server của bạn là các project Godot riêng biệt, rất có thể server của bạn nên được cấu hình để khi chạy main scene thì server sẽ tự động khởi động.

Các bước tiếp theo
------------------

Trên Linux, để dedicated server khởi động lại sau khi gặp sự cố hoặc hệ thống reboot, bạn có thể `tạo một systemd service <https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6>`__. Cách này cũng cho phép bạn xem log server thuận tiện hơn, với tính năng xoay vòng log tự động do systemd cung cấp. Khi cấu hình project để có thể host dưới dạng systemd service, bạn cũng nên bật project setting ``application/run/flush_stdout_on_print``. Nhờ vậy, journald (dịch vụ ghi log của systemd) có thể thu thập log trong khi process đang chạy.

Nếu có kinh nghiệm với container, bạn cũng có thể cân nhắc đóng gói dedicated server trong một container `Docker <https://www.docker.com/>`__. Nhờ vậy, server có thể được sử dụng dễ dàng hơn trong thiết lập auto-scaling (nằm ngoài phạm vi của tutorial này).
