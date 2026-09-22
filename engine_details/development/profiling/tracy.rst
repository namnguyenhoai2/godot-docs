.. _doc_profiler_tracy:

Tracy
=====

.. seealso:: Vui lòng xem :ref:`hướng dẫn về trình profiler tracing <doc_tracing_profilers>` để biết thêm thông tin.

`Tracy <https://github.com/wolfpld/tracy>`__ là một trình profiler mã nguồn mở chạy trên nhiều nền tảng, bao gồm Windows, Linux và macOS. Mặc dù chủ yếu là một trình profiler tracing, nó cũng có thể định kỳ lấy mẫu dữ liệu như một
:ref:`trình profiler sampling <doc_sampling_profilers>`, nhờ đó mang lại một số lợi ích của cả hai phương pháp.

Xây dựng Godot với hỗ trợ Tracy
-------------------------------

Trước tiên, hãy clone phiên bản mới nhất của mã nguồn Tracy ("0.13.0" tại thời điểm viết tài liệu này) bằng Git:

.. code-block:: shell

    git clone -b v0.13.0 --single-branch https://github.com/wolfpld/tracy.git

Thao tác này sẽ tạo một thư mục ``tracy`` - bạn có thể đặt thư mục này ở bất kỳ đâu.

Tiếp theo, hãy build các release template cho nền tảng của bạn bằng ``scons``, đồng thời thêm các đối số ``profiler=tracy profiler_path=path/to/tracy`` với đường dẫn thực tế đến thư mục ``tracy``, cũng như ``debug_symbols=yes`` để cho phép các tính năng sampling của Tracy hoạt động.

.. note::

    Bạn không nhất thiết phải build release template; bạn cũng có thể build debug template hoặc thậm chí editor. Tuy nhiên, thông thường bạn nên profile release template, vì đó là phiên bản mà người chơi của bạn sẽ sử dụng và hiệu năng của nó sẽ khác với các loại bản build khác.

Ví dụ, để build release template cho Windows:

.. code-block:: shell

    scons platform=windows target=template_release debug_symbols=yes profiler=tracy profiler_path=path/to/tracy

Lấy "server" của Tracy
----------------------

Theo thuật ngữ của Tracy, ứng dụng mà bạn đang profile là "client", còn ứng dụng nhận dữ liệu là "server".

Nếu đang sử dụng Windows, bạn có thể tải xuống ``tracy-profiler.exe`` đã được build sẵn từ `trang releases <https://github.com/wolfpld/tracy/releases>`_ của Tracy.

Tuy nhiên, nếu đang sử dụng Linux hoặc macOS, bạn sẽ cần tìm binary đã được build sẵn từ một package manager (chẳng hạn như ``brew`` hoặc ``nix``), hoặc tự build từ mã nguồn.

.. note::

    Nếu sử dụng binary đã được build sẵn, hãy chắc chắn rằng bạn dùng cùng phiên bản với phiên bản đã dùng khi build Godot.

Build Tracy server từ mã nguồn
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để build Tracy, bạn cần cài đặt ``cmake``, có thể tải xuống từ `website CMake <https://cmake.org/download/>`_ hoặc có thể cài đặt thông qua package manager (chẳng hạn như ``brew`` hoặc ``nix``).

Bạn có thể tìm thấy hướng dẫn đầy đủ về cách build Tracy từ mã nguồn trong `Tracy manual <https://github.com/wolfpld/tracy/releases/latest/download/tracy.pdf>`_, nhưng đây là phần TL;DR:

.. code-block:: shell

    # Trên Linux, Tracy sử dụng Wayland theo mặc định, vì vậy nếu bạn sử dụng X11, hãy thêm -DLEGACY=1
    cmake -B profiler/build -S profiler -DCMAKE_BUILD_TYPE=Release
    cmake --build profiler/build --config Release --parallel

Thao tác này sẽ đặt binary tại ``tracy/profiler/build/tracy-profiler`` hoặc ``tracy/profiler/build/tracy-profiler.exe`` (trên Windows).

Ghi lại trace
-------------

Khởi chạy Tracy server - bạn sẽ thấy giao diện tương tự như sau:

.. image:: img/cpp_profiler_tracy_start.webp

Nhấn "connect". Thao tác này sẽ đảm bảo Tracy kết nối ngay khi game khởi chạy. Nếu quên nhấn "connect", Tracy sẽ lưu các sự kiện hệ thống trong RAM, khiến mức sử dụng bộ nhớ có thể nhanh chóng tăng vọt (xem ``TRACY_ON_DEMAND`` tài liệu).

Bây giờ, hãy export game bằng các release template bạn đã build ở trên và chạy game. Ngay khi cả hai đang chạy và bạn đã nhấn nút "Connect" trong Tracy, bạn sẽ thấy dữ liệu được gửi đến:

.. image:: img/cpp_profiler_tracy_recording.webp

Khi cho rằng mình đã thu thập đủ dữ liệu, hãy nhấn nút "Stop". Nếu bạn đã nhấp vào đâu đó và hộp chứa nút "Stop" biến mất, hãy nhấp vào biểu tượng ngoài cùng bên trái ở phía trên để hiển thị lại hộp đó.

Kiểm tra trace
--------------

Dưới đây là một số thao tác điều khiển cơ bản:

- Phóng to/thu nhỏ bằng con lăn chuột
- Nhấp chuột phải và kéo để di chuyển tiến/lùi trên timeline
- Trên thanh trên cùng, nhấp vào các nút mũi tên trái và phải bên cạnh "Frames" để di chuyển một frame trên timeline

Để tìm hiểu thêm, hãy xem `Tracy manual <https://github.com/wolfpld/tracy/releases/latest/download/tracy.pdf>`_.

.. _`releases page`: https://github.com/wolfpld/tracy/releases
.. _`CMake website`: https://cmake.org/download/
.. _`Tracy manual`: https://github.com/wolfpld/tracy/releases/latest/download/tracy.pdf
