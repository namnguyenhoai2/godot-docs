.. _doc_exporting_for_dedicated_servers:

Export cho dedicated server
===========================

.. highlight:: none

Nếu bạn muốn chạy một dedicated server cho project của mình trên một máy không có GPU hoặc display server, bạn sẽ cần chạy Godot với display server ``headless`` và ``Dummy`` :ref:`audio driver <class_ProjectSettings_property_audio/driver/driver>`.

Kể từ Godot 4.0, bạn có thể thực hiện việc này bằng cách chạy một Godot binary trên bất kỳ platform nào với command-line argument ``--headless``, hoặc chạy một project được export dưới dạng dedicated server. Bạn không còn cần sử dụng server binary chuyên dụng như trong Godot 3.x.

Editor và export template
-------------------------

Bạn có thể sử dụng editor binary hoặc export template binary (debug hoặc release) ở headless mode. Việc nên dùng loại nào phụ thuộc vào trường hợp sử dụng của bạn:

- **Export template:** Sử dụng loại này để chạy dedicated server. Nó không chứa chức năng editor, do đó có kích thước nhỏ hơn và được tối ưu hóa tốt hơn. - **Editor:** Binary này chứa chức năng editor và được dùng để export project. Binary này *có thể* được dùng để chạy dedicated server, nhưng không được khuyến nghị vì có kích thước lớn hơn và kém tối ưu hơn.

Các phương pháp export
----------------------

Có hai cách để export một project cho server:

- Tạo một export preset riêng cho platform sẽ host server, sau đó export project như bình thường. - Chỉ export một file PCK, tốt nhất là cho platform khớp với platform sẽ host server. Đặt file PCK này vào cùng thư mục với một export template binary, đổi tên binary để có cùng tên với PCK (bỏ phần mở rộng file), sau đó chạy binary.

Cả hai phương pháp đều cho ra output giống hệt nhau. Phần còn lại của trang này sẽ tập trung vào phương pháp đầu tiên.

Xem :ref:`doc_exporting_projects` để biết thêm thông tin.

.. _doc_exporting_for_dedicated_servers_exporting_project:

Export project cho dedicated server
-----------------------------------

Nếu bạn export project như bình thường khi nhắm đến server, bạn sẽ nhận thấy file PCK có kích thước lớn tương đương client. Điều này là vì nó bao gồm tất cả resource, kể cả những resource server không cần (chẳng hạn như dữ liệu texture). Ngoài ra, headless mode sẽ không được tự động sử dụng; người dùng phải chỉ định ``--headless`` để đảm bảo không có window nào được tạo.

Nhiều resource như texture có thể được loại bỏ khỏi file PCK để giảm đáng kể kích thước. Godot cung cấp cách thực hiện việc này cho texture và material mà vẫn giữ các reference trong scene hoặc resource file (built-in hoặc external).

Để bắt đầu, hãy đảm bảo bạn có một export preset riêng cho server, sau đó chọn preset đó, đi đến tab **Resources** và thay đổi export mode của nó:

.. figure:: img/exporting_for_dedicated_servers_export_mode.webp
   :align: center
   :alt: Choosing the **Export as dedicated server** export mode in the export preset

   Choosing the **Export as dedicated server** export mode in the export preset

Khi chọn export mode này, feature tag ``dedicated_server`` sẽ được tự động thêm vào project đã export.

.. note::

    Nếu bạn không muốn sử dụng export mode này nhưng vẫn muốn có feature tag, bạn có thể viết tên ``dedicated_server`` trong tab **Features** của export preset. Việc này cũng sẽ buộc sử dụng ``--headless`` khi chạy project đã export.

Sau khi chọn export mode này, bạn sẽ thấy danh sách các resource trong project:

.. figure:: img/exporting_for_dedicated_servers_export_resources.webp
   :align: center
   :alt: Choosing resources to keep, keep with stripped visuals or remove

   Choosing resources to keep, keep with stripped visuals or remove

Đánh dấu một ô cho phép bạn override các tùy chọn cho file hoặc folder được chỉ định. Việc đánh dấu các ô **không** ảnh hưởng đến những file được export; điều này được quyết định bởi các tùy chọn được chọn cho từng ô.

Các file bên trong một folder đã được đánh dấu sẽ tự động sử dụng tùy chọn của folder cha theo mặc định, được thể hiện bằng hậu tố **(Inherited)** trong tên tùy chọn (và tên tùy chọn sẽ bị làm mờ). Để thay đổi tùy chọn cho một file hiện đang kế thừa, trước tiên bạn phải đánh dấu ô bên cạnh file đó.

- **Strip Visuals:** Export resource này, trong đó các file visual (texture và material) được thay thế bằng placeholder class. Placeholder class lưu kích thước ảnh (vì đôi khi thông tin này được dùng để định vị các element trong scene 2D), nhưng không lưu gì khác. - **Keep:** Export resource này như bình thường, giữ nguyên các file visual. - **Remove:** File không được đưa vào PCK. Tùy chọn này hữu ích để bỏ qua các scene và resource mà chỉ client cần. Nếu sử dụng tùy chọn này, hãy đảm bảo server không tham chiếu đến các scene và resource chỉ dành cho client này theo bất kỳ cách nào.

Khuyến nghị chung là sử dụng **Strip Visuals** bất cứ khi nào có thể, trừ khi server cần truy cập dữ liệu ảnh như màu của các pixel. Ví dụ, nếu server tạo dữ liệu collision dựa trên nội dung của một ảnh, bạn cần sử dụng **Keep** cho ảnh cụ thể đó.

.. tip::

    Để kiểm tra cấu trúc file của PCK đã export, hãy sử dụng nút **Export PCK/ZIP...** với phần mở rộng file ``.zip``, sau đó mở file ZIP thu được bằng file manager.

.. warning::

    Hãy cẩn thận khi sử dụng mode **Remove**, vì các scene/resource tham chiếu đến file đã bị xóa sẽ không thể load thành công nữa.

    Nếu muốn xóa các resource cụ thể nhưng vẫn cho phép scene load mà không cần chúng, bạn sẽ phải xóa reference trong scene file và load các file vào properties của node bằng ``load()`` trong script. Cách tiếp cận này có thể được dùng để loại bỏ các resource mà Godot chưa hỗ trợ thay thế bằng placeholder, chẳng hạn như audio.

    Việc xóa texture thường tạo ra tác động lớn nhất đến kích thước PCK, vì vậy ban đầu bạn nên dùng **Strip Visuals**.

Với các tùy chọn trên, PCK cho client (export tất cả resource theo cách bình thường) sẽ có dạng như sau:

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

Cấu trúc file của PCK cho server sẽ có dạng như sau:

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
    │   └── sprite.png.import  # Trỏ đến placeholder texture
    └── server
    │   └── map_data.png.import
    ├── project.binary
    ├── scene.gd
    ├── scene.tscn.remap

Khởi động dedicated server
--------------------------

Nếu client và server của bạn cùng thuộc một Godot project, bạn sẽ phải thêm cách để khởi động server trực tiếp bằng command-line argument.

Nếu bạn :ref:`exported the project <doc_exporting_for_dedicated_servers_exporting_project>` bằng export mode **Export as dedicated server** (hoặc đã thêm ``dedicated_server`` dưới dạng custom feature tag), bạn có thể sử dụng feature tag ``dedicated_server`` để phát hiện xem một dedicated server PCK có đang được sử dụng hay không:

.. tabs::
 .. code-tab:: gdscript

    # Note: Feature tags are case-sensitive.
    if OS.has_feature("dedicated_server"):
        # Chạy code khởi động server tại đây...
        pass

 .. code-tab:: csharp

    // Note: Feature tags are case-sensitive.
    if (OS.HasFeature("dedicated_server"))
    {
        // Chạy code khởi động server tại đây...
    }

Nếu bạn cũng muốn host server khi sử dụng command-line argument tích hợp sẵn ``--headless``, bạn có thể thực hiện bằng cách thêm đoạn code sau vào method ``_ready()`` của main scene (hoặc autoload):

.. tabs::
 .. code-tab:: gdscript

    if DisplayServer.get_name() == "headless":
        # Chạy code khởi động server tại đây...
        #
        # Với kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        # một Godot binary (editor hoặc export template) với `--headless`
        # command-line argument.
        pass

 .. code-tab:: csharp

    using System.Linq;

    if (DisplayServer.GetName() == "headless")
    {
        // Chạy code khởi động server tại đây...
        //
        // Với kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        // một Godot binary (editor hoặc export template) với `--headless`
        // command-line argument.
    }

Nếu muốn sử dụng custom command-line argument, bạn có thể thực hiện bằng cách thêm đoạn code sau vào method ``_ready()`` của main scene (hoặc autoload):

.. tabs::
 .. code-tab:: gdscript

    if "--server" in OS.get_cmdline_user_args():
        # Chạy code khởi động server tại đây...
        #
        # Với kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        # một Godot binary (editor hoặc export template) với `--server`
        # command-line argument.
        pass

 .. code-tab:: csharp

    using System.Linq;

    if (OS.GetCmdlineUserArgs().Contains("--server"))
    {
        // Chạy code khởi động server tại đây...
        //
        // Với kiểm tra này, bạn có thể khởi động dedicated server bằng cách chạy
        // một Godot binary (editor hoặc export template) với `--server`
        // command-line argument.
    }

Bạn nên thêm ít nhất một trong các command-line argument ở trên để khởi động server, vì nó có thể được dùng để kiểm thử chức năng server từ command line mà không cần export project.

Nếu client và server của bạn là các Godot project riêng biệt, server rất có thể nên được cấu hình để khi chạy main scene thì server sẽ tự động khởi động.

Các bước tiếp theo
------------------

Trên Linux, để dedicated server khởi động lại sau khi crash hoặc hệ thống reboot, bạn có thể `create a systemd service <https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6>`__. Cách này cũng cho phép bạn xem server log thuận tiện hơn, với việc tự động xoay vòng log do systemd cung cấp. Khi biến project của mình thành một systemd service có thể host, bạn cũng nên bật project setting ``application/run/flush_stdout_on_print``. Nhờ vậy, journald (systemd logging service) có thể thu thập log trong khi process đang chạy.

Nếu có kinh nghiệm với container, bạn cũng có thể tìm hiểu việc bọc dedicated server trong một container `Docker <https://www.docker.com/>`__. Nhờ vậy, server có thể được sử dụng dễ dàng hơn trong một thiết lập automatic scaling (nằm ngoài phạm vi của tutorial này).
