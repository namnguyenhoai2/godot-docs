.. _doc_profiler_perfetto:

Perfetto
========

.. seealso:: Vui lòng xem :ref:`hướng dẫn về trình profiler tracing <doc_tracing_profilers>` để biết thêm thông tin.

`Perfetto <https://perfetto.dev>`__ là hệ thống tracing mặc định cho Android. Trên thực tế, dịch vụ system tracing của nó đã được tích hợp vào nền tảng kể từ Android 9.

Sử dụng các export template chính thức của Perfetto
---------------------------------------------------

Bắt đầu từ Godot 4.7, các export template Perfetto được cung cấp cho mọi bản phát hành Godot ổn định và có thể tải xuống từ `trang GitHub Releases <https://github.com/godotengine/godot/releases/>`_.

Sử dụng Gradle build template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Đi đến trang phát hành và tải xuống ``Godot_v<godot_version>_android_source.perfetto.zip`` release artifact, trong đó ``godot_version`` tương ứng với phiên bản engine đang được sử dụng.
- Trong hộp thoại **Project > Export**, phải bật **Advanced Options** và **Use Gradle Build**.
- Trỏ **Android Source Template** đến export template đã tải xuống.

.. image:: img/cpp_profiler_perfetto_gradle_build_config.webp

Làm theo hướng dẫn trong :ref:`phần Configuration <doc_profiler_perfetto_configuration>` để tìm hiểu cách cấu hình và tạo trace.

Sử dụng các build template không dùng Gradle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Đi đến trang phát hành và tải xuống các release artifact sau, trong đó ``godot_version`` tương ứng với phiên bản engine đang được sử dụng:

  - ``Godot_v<godot_version>_android_debug.perfetto.apk`` (dành cho debug build)
  - ``Godot_v<godot_version>_android_release.perfetto.apk`` (dành cho release build)

- Trong hộp thoại **Project > Export**:

  - Phải bật **Advanced Options**
  - Phải tắt **Use Gradle Build**

- Trỏ **Custom Template** đến các export template đã tải xuống.

.. image:: img/cpp_profiler_perfetto_non_gradle_build_config.webp

Làm theo hướng dẫn trong :ref:`phần Configuration <doc_profiler_perfetto_configuration>` để tìm hiểu cách cấu hình và tạo trace.

Các bản build Godot tùy chỉnh có hỗ trợ Perfetto
------------------------------------------------

Từ thư mục gốc ``godot``, chạy python script sau để cài đặt phiên bản mới nhất của Perfetto SDK vào ``thirdparty/perfetto``:

.. code-block:: shell

    python misc/scripts/install_perfetto.py

Tiếp theo, build các template Android debug hoặc release cho kiến trúc của bạn bằng ``scons`` (theo :ref:`Compiling for Android <doc_compiling_for_android>`), đồng thời thêm đối số ``profiler=perfetto``.

.. note::

    Nhìn chung, bạn nên profile các release template, vì đó là phiên bản người chơi của bạn sẽ sử dụng và hiệu năng của nó sẽ khác với các loại build khác. Tuy nhiên, trong trường hợp Android, đôi khi việc sử dụng debug template có thể hữu ích, vì Godot chỉ có thể remote debug các game được export từ debug template.

Ví dụ, để build các release template cho arm64:

.. code-block:: shell

    scons platform=android target=template_release arch=arm64 generate_android_binaries=yes profiler=perfetto

.. _doc_profiler_perfetto_configuration:

Cấu hình
--------

Perfetto yêu cầu một tệp cấu hình để xác định các event cần theo dõi.

Tạo một tệp có tên ``godot.config`` với nội dung sau:

.. code-block:: text

    # Trace for 10 seconds.
    duration_ms: 10000

    buffers {
        size_kb: 32768
        fill_policy: RING_BUFFER
    }

    # Write to file once every second to prevent overflowing the buffer.
    write_into_file: true
    file_write_period_ms: 1000

    # Track events in the "godot" category.
    data_sources {
        config {
            name: "track_event"
            track_event_config {
                enabled_categories: "godot"
            }
        }
    }

.. note::

    Godot ghi lại hai category của track event:

    - **godot**: Dùng để ghi lại các event của Godot engine. Category này được dùng để phân tích hiệu năng. Overhead của event tracing không đáng kể đối với hiệu năng. Đây nên là chế độ tracing thông thường dành cho hầu hết developer.
    - **godot_scripting**: Dùng để ghi lại các event scripting của Godot. Đây là category chậm vì nó profile toàn bộ logic scripting của game. Category này được dùng để hiểu code / debug / tìm nguyên nhân gây ra hiện tượng giật khung hình. Hiệu năng chậm hơn nhiều, nhưng nó giúp tìm ra một lời gọi hàm có vấn đề vốn bị ẩn đi.

Ghi lại một trace
-----------------

Cuối cùng, khởi chạy game trên thiết bị Android bằng các export template bạn đã build trước đó.

Khi bạn đã sẵn sàng ghi trace (chẳng hạn khi đã đến phần game đang gặp vấn đề về hiệu năng), bạn có thể sử dụng `script này từ GitHub repository của Perfetto <https://github.com/google/perfetto/blob/main/tools/record_android_trace>`_.

.. code-block:: shell

    ./record_android_trace -c /path/to/godot.config

Thao tác này sẽ ghi lại trong 10 giây (theo cấu hình) hoặc cho đến khi bạn nhấn
:kbd:`Ctrl + C`.

Kiểm tra trace
--------------

Ngay khi script đó kết thúc, nó sẽ mở Perfetto UI trong trình duyệt web.

Để xem các event của Godot, mở rộng hàng dành cho ứng dụng bằng cách nhấp vào *Unique Name* / *Package Name* / *App ID* Android của ứng dụng (Perfetto cũng sẽ đưa vào trace một số event từ các system service).

.. image:: img/cpp_profiler_perfetto.webp

Sau đó, bạn có thể sử dụng ``WASD`` các phím để điều hướng trên biểu đồ:

- Nhấn :kbd:`A` hoặc :kbd:`D` để di chuyển tiến hoặc lùi trên timeline
- Nhấn :kbd:`W` hoặc :kbd:`S` để phóng to hoặc thu nhỏ

Có thể bạn sẽ cần phóng to một chút trước khi có thể thấy các event riêng lẻ từ Godot.

Để tìm hiểu thêm, hãy xem `tài liệu Perfetto UI <https://perfetto.dev/docs/visualization/perfetto-ui>`_.

.. _`GitHub Releases page`: https://github.com/godotengine/godot/releases/
.. _`this script from the Perfetto GitHub repository`: https://github.com/google/perfetto/blob/main/tools/record_android_trace
.. _`Perfetto UI documentation`: https://perfetto.dev/docs/visualization/perfetto-ui
