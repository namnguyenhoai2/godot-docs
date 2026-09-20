.. _doc_version_control_systems:

Hệ thống kiểm soát phiên bản
============================

Giới thiệu
----------

Godot hướng đến khả năng tương thích với VCS và tạo ra các tệp hầu hết đều dễ đọc, dễ merge.

Plugin kiểm soát phiên bản
--------------------------

Godot cũng hỗ trợ sử dụng hệ thống kiểm soát phiên bản ngay trong editor. Tuy nhiên, tính năng kiểm soát phiên bản trong editor yêu cầu plugin dành cho VCS cụ thể mà bạn đang sử dụng.

Tính đến tháng 10 năm 2025, hiện chỉ có plugin Git, nhưng cộng đồng có thể tạo thêm các plugin VCS khác.

Plugin Git chính thức
~~~~~~~~~~~~~~~~~~~~~

Việc sử dụng Git bên trong editor được hỗ trợ thông qua một plugin chính thức. Bạn có thể tìm các bản phát hành mới nhất tại `GitHub <https://github.com/godotengine/godot-git-plugin/releases>`__.

Tài liệu hướng dẫn sử dụng plugin Git có tại `wiki <https://github.com/godotengine/godot-git-plugin/wiki>`__.

Các tệp cần loại trừ khỏi VCS
-----------------------------

.. note::

    Danh sách này liệt kê các tệp và thư mục cần được bỏ qua khỏi việc kiểm soát phiên bản trong Godot 4.1 trở lên.

    Danh sách các tệp và thư mục cần được bỏ qua khỏi việc kiểm soát phiên bản trong Godot 3.x và Godot 4.0 **hoàn toàn** khác. Điều này rất quan trọng, vì Godot 3.x và 4.0 có thể lưu thông tin xác thực nhạy cảm trong ``export_presets.cfg`` (không giống Godot 4.1 trở lên).

    Nếu bạn đang sử dụng Godot 3, hãy xem ``3.6`` của trang tài liệu này thay thế.

Có một số tệp và thư mục mà Godot tự động tạo khi mở một project lần đầu trong editor. Để tránh làm repository kiểm soát phiên bản của bạn phình to do dữ liệu được tạo tự động, bạn nên thêm chúng vào danh sách ignore của VCS:

- ``.godot/``: Thư mục này lưu nhiều loại dữ liệu cache của project. - ``*.translation``: Các tệp này là dữ liệu nhị phân được import
  :ref:`translations <doc_internationalizing_games>` generated from CSV files.

Bạn có thể yêu cầu Godot project manager tự động tạo metadata kiểm soát phiên bản cho bạn khi tạo project. Khi chọn tùy chọn **Git**, thao tác này sẽ tạo các tệp ``.gitignore`` và ``.gitattributes`` trong thư mục gốc của project:

.. figure:: img/version_control_systems_generate_metadata.webp
   :align: center
   :alt: Creating version control metadata in the project manager's New Project dialog

   Creating version control metadata in the project manager's **New Project** dialog

Trong các project hiện có, chọn menu **Project** ở đầu editor, sau đó chọn **Version Control > Generate Version Control Metadata**. Thao tác này tạo ra các tệp giống như khi thực hiện trong project manager.

Làm việc với Git trên Windows
-----------------------------

Hầu hết các client Git for Windows được cấu hình với ``core.autocrlf`` được đặt thành ``true``. Điều này có thể khiến Git đánh dấu các tệp là đã sửa đổi một cách không cần thiết do line ending của chúng tự động được chuyển đổi từ LF sang CRLF.

Tốt hơn là đặt tùy chọn này thành:

::

    git config --global core.autocrlf input

Việc tạo metadata kiểm soát phiên bản bằng project manager hoặc editor sẽ tự động buộc sử dụng line ending LF thông qua tệp ``.gitattributes``. Trong trường hợp này, bạn không cần thay đổi cấu hình Git.

Git LFS
-------

Git LFS (Large File Storage) là một extension của Git cho phép bạn quản lý các tệp lớn trong repository. Nó thay thế các tệp lớn bằng các con trỏ dạng văn bản bên trong Git, đồng thời lưu nội dung tệp trên một server từ xa. Tính năng này hữu ích khi quản lý các asset lớn như texture, tệp âm thanh và model 3D mà không làm repository Git phình to.

.. note::

    Khi sử dụng Git LFS, bạn cần đảm bảo đã setup xong trước khi commit bất kỳ tệp nào vào repository. Nếu bạn đã commit tệp vào repository, bạn sẽ cần xóa chúng khỏi repository rồi thêm lại sau khi setup Git LFS.

    Bạn có thể sử dụng ``git lfs migrate`` để chuyển đổi các tệp hiện có trong repository, nhưng cách này chuyên sâu hơn và đòi hỏi hiểu biết tốt về Git.

    Một cách tiếp cận phổ biến là setup một repository mới với Git LFS (và một ``.gitattributes`` phù hợp), sau đó sao chép các tệp từ repository cũ sang repository mới. Bằng cách này, bạn có thể đảm bảo mọi tệp đều được LFS theo dõi ngay từ đầu.

Để sử dụng Git LFS với Godot, bạn cần cài đặt extension Git LFS và cấu hình nó để theo dõi các loại tệp bạn muốn quản lý. Bạn có thể thực hiện việc này bằng cách chạy lệnh sau trong terminal: ::

    git lfs install

Thao tác này sẽ tạo một tệp ``.gitattributes`` trong repository, cho Git biết cần sử dụng LFS cho các loại tệp được chỉ định. Bạn có thể thêm các loại tệp khác bằng cách chỉnh sửa tệp ``.gitattributes``. Ví dụ: để theo dõi tất cả các tệp GLB, bạn có thể chạy lệnh sau trong terminal: ::

    git lfs track "*.glb"

Khi bạn thêm hoặc sửa đổi các tệp được LFS theo dõi, Git sẽ tự động lưu chúng trong LFS thay vì lịch sử Git thông thường. Bạn có thể push và pull các tệp LFS giống như các tệp Git thông thường, nhưng hãy nhớ rằng các tệp LFS được lưu riêng khỏi phần còn lại của lịch sử Git. Điều này có nghĩa là bạn có thể cần cài đặt Git LFS trên bất kỳ máy nào mà bạn clone repository để truy cập các tệp LFS.

Dưới đây là một tệp ``.gitattributes`` mẫu mà bạn có thể dùng làm điểm bắt đầu cho Git LFS. Các loại tệp này được chọn vì chúng thường được sử dụng, nhưng bạn có thể sửa đổi danh sách để thêm bất kỳ loại nhị phân nào có trong project.

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

    # Font & Icon
    *.ttf filter=lfs diff=lfs merge=lfs -text
    *.otf filter=lfs diff=lfs merge=lfs -text
    *.ico filter=lfs diff=lfs merge=lfs -text

    # Dành riêng cho Godot LFS
    *.scn filter=lfs diff=lfs merge=lfs -text
    *.res filter=lfs diff=lfs merge=lfs -text
    *.material filter=lfs diff=lfs merge=lfs -text
    *.anim filter=lfs diff=lfs merge=lfs -text
    *.mesh filter=lfs diff=lfs merge=lfs -text
    *.lmbake filter=lfs diff=lfs merge=lfs -text

Để biết thêm thông tin về Git LFS, hãy xem tài liệu chính thức: https://git-lfs.github.com/ và https://docs.github.com/en/repositories/working-with-files/managing-large-files.
