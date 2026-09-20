.. _doc_profiler_tracy:

Tracy
=====

.. seealso:: Please see the :ref:`tracing profiler instructions <doc_tracing_profilers>` for more information.

`Tracy <https://github.com/wolfpld/tracy>`__ là một trình phân tích hiệu năng mã nguồn mở chạy trên nhiều nền tảng, bao gồm Windows, Linux và macOS. Mặc dù chủ yếu là trình phân tích dựa trên tracing, nó cũng có thể định kỳ lấy mẫu dữ liệu như một
:ref:`sampling profiler <doc_sampling_profilers>`, giving some of the benefits
của cả hai phương pháp.

Xây dựng Godot với hỗ trợ Tracy
-------------------------------

Trước tiên, hãy clone phiên bản mới nhất của mã nguồn Tracy ("0.13.0" tại thời điểm viết bài) bằng Git:

.. code-block:: shell

    git clone -b v0.13.0 --single-branch https://github.com/wolfpld/tracy.git

Lệnh này sẽ tạo một thư mục ``tracy`` - bạn có thể đặt thư mục này ở bất kỳ đâu.

Tiếp theo, hãy xây dựng các release template cho nền tảng của bạn bằng ``scons``, nhưng thêm các đối số ``profiler=tracy profiler_path=path/to/tracy`` với đường dẫn thực tế đến thư mục ``tracy``, đồng thời thêm ``debug_symbols=yes`` để các tính năng lấy mẫu của Tracy hoạt động.

.. note::

    Bạn không nhất thiết phải xây dựng release template; bạn cũng có thể xây dựng debug template, hoặc thậm chí editor. Tuy nhiên, nhìn chung bạn nên phân tích release template, vì đó là phiên bản mà người chơi sẽ sử dụng và hiệu năng của nó sẽ khác với các loại bản build khác.

Ví dụ, để xây dựng release template cho Windows:

.. code-block:: shell

    scons platform=windows target=template_release debug_symbols=yes profiler=tracy profiler_path=path/to/tracy

Lấy "server" của Tracy
----------------------

Theo thuật ngữ của Tracy, ứng dụng mà bạn đang phân tích là "client", còn ứng dụng nhận dữ liệu là "server".

Nếu sử dụng Windows, bạn có thể tải xuống ``tracy-profiler.exe`` được build sẵn từ `trang phát hành <https://github.com/wolfpld/tracy/releases>`_ của Tracy.

Tuy nhiên, nếu bạn sử dụng Linux hoặc macOS, bạn sẽ cần tìm một binary được build sẵn từ trình quản lý gói (như ``brew`` hoặc ``nix``), hoặc tự build nó từ mã nguồn.

.. note::

    Nếu sử dụng binary được build sẵn, hãy đảm bảo dùng cùng phiên bản với phiên bản bạn đã sử dụng khi build Godot.

Build Tracy server từ mã nguồn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để build Tracy, bạn sẽ cần cài đặt ``cmake``, có thể tải xuống từ `trang web CMake <https://cmake.org/download/>`_, hoặc có thể cài đặt thông qua trình quản lý gói (như ``brew`` hoặc ``nix``).

Bạn có thể tìm thấy hướng dẫn đầy đủ để build Tracy từ mã nguồn trong `sổ tay Tracy <https://github.com/wolfpld/tracy/releases/latest/download/tracy.pdf>`_, nhưng dưới đây là phần tóm tắt:

.. code-block:: shell

    # On Linux, Tracy uses Wayland by default, so if you use X11 add -DLEGACY=1
    cmake -B profiler/build -S profiler -DCMAKE_BUILD_TYPE=Release
    cmake --build profiler/build --config Release --parallel

Lệnh này sẽ đặt binary tại ``tracy/profiler/build/tracy-profiler`` hoặc ``tracy/profiler/build/tracy-profiler.exe`` (trên Windows).

Ghi trace
---------

Khởi chạy Tracy server - bạn sẽ thấy giao diện tương tự như sau:

.. image:: img/cpp_profiler_tracy_start.webp

Nhấn "connect". Thao tác này sẽ đảm bảo tracy lập tức kết nối khi game khởi chạy. Nếu quên nhấn "connect", Tracy sẽ lưu các sự kiện hệ thống trong RAM, điều này có thể nhanh chóng làm tăng vọt mức sử dụng bộ nhớ (xem tài liệu ``TRACY_ON_DEMAND``).

Bây giờ, hãy export game bằng các release template bạn đã build ở trên rồi chạy game. Ngay khi cả hai đang chạy và bạn đã nhấn nút "Connect" trong Tracy, bạn sẽ thấy dữ liệu được truyền đến:

.. image:: img/cpp_profiler_tracy_recording.webp

Khi cho rằng mình đã thu thập đủ dữ liệu, hãy nhấn nút "Stop". Nếu bạn nhấp vào đâu đó và hộp có nút "Stop" biến mất, bạn có thể nhấp vào biểu tượng ngoài cùng bên trái ở phía trên để hiển thị lại.

Kiểm tra trace
--------------

Dưới đây là một số điều khiển cơ bản:

- Phóng to/thu nhỏ bằng con lăn chuột - Nhấp chuột phải và kéo để di chuyển tiến/lùi trên dòng thời gian - Trên thanh phía trên, nhấp vào các nút mũi tên trái và phải bên cạnh "Frames" để di chuyển từng frame trên dòng thời gian

Để tìm hiểu thêm, hãy xem `sổ tay Tracy <https://github.com/wolfpld/tracy/releases/latest/download/tracy.pdf>`_.
