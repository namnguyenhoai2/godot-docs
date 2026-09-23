.. _doc_version_control_systems:

Hệ thống kiểm soát phiên bản
============================

Giới thiệu
----------

Godot hướng đến khả năng tương thích với VCS và tạo ra các tệp phần lớn dễ đọc, dễ merge.

Plugin kiểm soát phiên bản
--------------------------

Godot cũng hỗ trợ sử dụng hệ thống kiểm soát phiên bản ngay trong editor. Tuy nhiên, tính năng kiểm soát phiên bản trong editor yêu cầu plugin dành cho VCS cụ thể mà bạn đang sử dụng.

Tính đến tháng 10 năm 2025, hiện chỉ có plugin Git, nhưng cộng đồng có thể tạo thêm các plugin VCS khác.

Plugin Git chính thức
~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sử dụng Git ngay trong editor với plugin chính thức. Bạn có thể tìm các bản phát hành mới nhất trên `GitHub <https://github.com/godotengine/godot-git-plugin/releases>`__.

Bạn có thể tìm tài liệu hướng dẫn sử dụng plugin Git trên `wiki <https://github.com/godotengine/godot-git-plugin/wiki>`__ của plugin.

Các tệp cần loại trừ khỏi VCS
-----------------------------

.. note::

    Phần này liệt kê các tệp và thư mục cần được bỏ qua khỏi hệ thống kiểm soát phiên bản trong Godot 4.1 trở lên.

    Danh sách các tệp và thư mục cần được bỏ qua khỏi hệ thống kiểm soát phiên bản trong Godot 3.x và Godot 4.0 **hoàn toàn** khác. Điều này rất quan trọng, vì Godot 3.x và 4.0 có thể lưu thông tin xác thực nhạy cảm trong ``export_presets.cfg`` (khác với Godot 4.1 trở lên).

    Nếu bạn đang sử dụng Godot 3, hãy xem ``3.6`` phiên bản của trang tài liệu này.

Godot tự động tạo một số tệp và thư mục khi lần đầu mở một project trong editor. Để tránh làm repository kiểm soát phiên bản của bạn phình to bởi dữ liệu được tạo tự động, bạn nên thêm chúng vào danh sách bỏ qua của VCS:

- ``.godot/``: Thư mục này lưu nhiều dữ liệu bộ nhớ đệm khác nhau của project.
- ``*.translation``: Các tệp này là các tệp nhị phân được import
  :ref:`bản dịch <doc_internationalizing_games>` được tạo từ các tệp CSV.

Bạn có thể để project manager của Godot tự động tạo metadata kiểm soát phiên bản khi tạo project. Khi chọn tùy chọn **Git**, thao tác này sẽ tạo các tệp ``.gitignore`` và ``.gitattributes`` trong thư mục gốc của project:

.. figure:: img/version_control_systems_generate_metadata.webp
   :align: center
   :alt: Tạo metadata kiểm soát phiên bản trong hộp thoại New Project của project manager

   Tạo metadata kiểm soát phiên bản trong hộp thoại **New Project** của project manager

Trong các project hiện có, chọn menu **Project** ở phía trên editor, sau đó chọn **Version Control > Generate Version Control Metadata**. Thao tác này tạo ra các tệp giống như khi được thực hiện trong project manager.

Làm việc với Git trên Windows
-----------------------------

Hầu hết các client Git for Windows được cấu hình với ``core.autocrlf`` được đặt thành ``true``. Điều này có thể khiến Git đánh dấu các tệp là đã sửa đổi một cách không cần thiết do ký tự kết thúc dòng của chúng tự động được chuyển đổi từ LF sang CRLF.

Tốt hơn là đặt tùy chọn này thành:

::

    git config --global core.autocrlf input

Việc tạo metadata kiểm soát phiên bản bằng project manager hoặc editor sẽ tự động áp dụng ký tự kết thúc dòng LF bằng tệp ``.gitattributes``. Trong trường hợp này, bạn không cần thay đổi cấu hình Git.

Git LFS
-------

Git LFS (Large File Storage) là một phần mở rộng của Git, cho phép bạn quản lý các tệp lớn trong repository. Nó thay thế các tệp lớn bằng các con trỏ văn bản bên trong Git, đồng thời lưu nội dung tệp trên một máy chủ từ xa. Tính năng này hữu ích khi quản lý các asset lớn như texture, tệp âm thanh và model 3D mà không làm repository Git của bạn phình to.

.. note::

    Khi sử dụng Git LFS, bạn nên đảm bảo đã thiết lập nó trước khi commit bất kỳ tệp nào vào repository. Nếu bạn đã commit các tệp vào repository, bạn sẽ cần xóa chúng khỏi repository rồi thêm lại sau khi thiết lập Git LFS.

    Bạn có thể sử dụng ``git lfs migrate`` để chuyển đổi các tệp hiện có trong repository, nhưng cách này chuyên sâu hơn và đòi hỏi hiểu biết tốt về Git.

    Một cách thường dùng là thiết lập một repository mới với Git LFS (và một ``.gitattributes`` phù hợp), sau đó sao chép các tệp từ repository cũ sang repository mới. Nhờ vậy, bạn có thể đảm bảo tất cả các tệp được LFS theo dõi ngay từ đầu.

Để sử dụng Git LFS với Godot, bạn cần cài đặt phần mở rộng Git LFS và cấu hình nó để theo dõi các loại tệp bạn muốn quản lý. Bạn có thể thực hiện việc này bằng cách
chạy lệnh sau trong terminal:
:::::::::::::::::::::::::::::

    git lfs install

Thao tác này sẽ tạo một tệp ``.gitattributes`` trong repository, cho Git biết cần sử dụng LFS cho các loại tệp được chỉ định. Bạn có thể thêm các loại tệp khác bằng cách chỉnh sửa tệp ``.gitattributes``. Ví dụ, để theo dõi tất cả các tệp GLB, bạn có thể thực hiện bằng cách
chạy lệnh sau trong terminal:
:::::::::::::::::::::::::::::

    git lfs track "*.glb"

Khi bạn thêm hoặc sửa đổi các tệp được LFS theo dõi, Git sẽ tự động lưu chúng trong LFS thay vì lịch sử Git thông thường. Bạn có thể push và pull các tệp LFS giống như các tệp Git thông thường, nhưng hãy nhớ rằng các tệp LFS được lưu riêng với phần còn lại của lịch sử Git. Điều này có nghĩa là bạn có thể cần cài đặt Git LFS trên mọi máy mà bạn clone repository để có thể truy cập các tệp LFS.

Dưới đây là một tệp ``.gitattributes`` mẫu mà bạn có thể dùng làm điểm bắt đầu cho Git LFS. Các loại tệp này được chọn vì thường được sử dụng, nhưng bạn có thể sửa đổi danh sách để thêm bất kỳ loại nhị phân nào có trong project.

.. code-block:: unixconfig

    # Chuẩn hóa EOL cho tất cả các tệp mà Git xem là tệp văn bản.
    * text=auto eol=lf

    # Theo dõi Git LFS (Asset)

    # Model 3D
    *.fbx filter=lfs diff=lfs merge=lfs -text
    *.gltf filter=lfs diff=lfs merge=lfs -text
    *.glb filter=lfs diff=lfs merge=lfs -text
    *.blend filter=lfs diff=lfs merge=lfs -text
    *.obj filter=lfs diff=lfs merge=lfs -text

    # Hình ảnh
    *.png filter=lfs diff=lfs merge=lfs -text
    *.svg filter=lfs diff=lfs merge=lfs -text
    *.jpg filter=lfs diff=lfs merge=lfs -text
    *.jpeg filter=lfs diff=lfs merge=lfs -text
    *.gif filter=lfs diff=lfs merge=lfs -text
    *.tga filter=lfs diff=lfs merge=lfs -text
    *.webp filter=lfs diff=lfs merge=lfs -text
    *.exr filter=lfs diff=lfs merge=lfs -text
    *.hdr filter=lfs diff=lfs merge=lfs -text
    *.dds filter=lfs diff=lfs merge=lfs -text

    # Âm thanh
    *.mp3 filter=lfs diff=lfs merge=lfs -text
    *.wav filter=lfs diff=lfs merge=lfs -text
    *.ogg filter=lfs diff=lfs merge=lfs -text

    # Font và biểu tượng
    *.ttf filter=lfs diff=lfs merge=lfs -text
    *.otf filter=lfs diff=lfs merge=lfs -text
    *.ico filter=lfs diff=lfs merge=lfs -text

    # Riêng cho Godot LFS
    *.scn filter=lfs diff=lfs merge=lfs -text
    *.res filter=lfs diff=lfs merge=lfs -text
    *.material filter=lfs diff=lfs merge=lfs -text
    *.anim filter=lfs diff=lfs merge=lfs -text
    *.mesh filter=lfs diff=lfs merge=lfs -text
    *.lmbake filter=lfs diff=lfs merge=lfs -text

Để biết thêm thông tin về Git LFS, hãy xem tài liệu chính thức: https://git-lfs.github.com/ và https://docs.github.com/en/repositories/working-with-files/managing-large-files.
