.. _doc_profiler_perfetto:

Perfetto
========

.. seealso:: Please see the :ref:`tracing profiler instructions <doc_tracing_profilers>` for more information.

`Perfetto <https://perfetto.dev>`__ là hệ thống tracing mặc định cho Android. Trên thực tế, dịch vụ tracing của hệ thống đã được tích hợp vào nền tảng kể từ Android 9.

Sử dụng các template Perfetto chính thức
----------------------------------------

Kể từ Godot 4.7, các template xuất Perfetto được cung cấp cho mọi bản phát hành Godot ổn định và có thể được tải xuống từ `trang GitHub Releases <https://github.com/godotengine/godot/releases/>`_.

Sử dụng template build Gradle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Đi đến trang phát hành và tải xuống artifact phát hành ``Godot_v<godot_version>_android_source.perfetto.zip``, trong đó ``godot_version`` tương ứng với phiên bản engine đang được sử dụng. - Trong hộp thoại **Project > Export**, phải bật **Advanced Options** và **Use Gradle Build**. - Trỏ **Android Source Template** đến template xuất đã tải xuống.

.. image:: img/cpp_profiler_perfetto_gradle_build_config.webp

Làm theo hướng dẫn trong :ref:`Configuration section <doc_profiler_perfetto_configuration>` để tìm hiểu cách cấu hình và tạo trace.

Sử dụng các template build không dùng Gradle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Đi đến trang phát hành và tải xuống các artifact phát hành sau, trong đó ``godot_version`` tương ứng với phiên bản engine đang được sử dụng:

  - ``Godot_v<godot_version>_android_debug.perfetto.apk`` (dành cho các bản build debug) - ``Godot_v<godot_version>_android_release.perfetto.apk`` (dành cho các bản build release)

- Trong hộp thoại **Project > Export**:

  - Phải bật **Advanced Options** - Phải tắt **Use Gradle Build**

- Trỏ **Custom Template** đến các template xuất đã tải xuống.

.. image:: img/cpp_profiler_perfetto_non_gradle_build_config.webp

Làm theo hướng dẫn trong :ref:`Configuration section <doc_profiler_perfetto_configuration>` để tìm hiểu cách cấu hình và tạo trace.

Các bản build Godot tùy chỉnh có hỗ trợ Perfetto
------------------------------------------------

Từ thư mục gốc ``godot``, chạy script python sau để cài đặt phiên bản mới nhất của Perfetto SDK vào ``thirdparty/perfetto``:

.. code-block:: shell

    python misc/scripts/install_perfetto.py

Tiếp theo, build các template Android debug hoặc release cho kiến trúc của bạn bằng ``scons`` (theo :ref:`Compiling for Android <doc_compiling_for_android>`), nhưng thêm đối số ``profiler=perfetto``.

.. note::

    Nhìn chung, bạn nên profile các template release vì đó là phiên bản mà người chơi sẽ sử dụng, và hiệu năng của nó sẽ khác với các loại build khác. Tuy nhiên, trong trường hợp Android, đôi khi việc sử dụng các template debug có thể hữu ích, vì Godot chỉ có thể gỡ lỗi từ xa các game được xuất từ các template debug.

Ví dụ, để build các template release cho arm64:

.. code-block:: shell

    scons platform=android target=template_release arch=arm64 generate_android_binaries=yes profiler=perfetto

.. _doc_profiler_perfetto_configuration:

Cấu hình
--------

Perfetto yêu cầu một tệp cấu hình để xác định các sự kiện cần theo dõi.

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

    Godot ghi lại hai danh mục sự kiện track:

    - **godot**: Dùng để ghi lại các sự kiện của engine Godot. Danh mục này được dùng để phân tích hiệu năng. Chi phí phát sinh từ việc tracing sự kiện không nên ảnh hưởng đáng kể đến hiệu năng. Đây nên là chế độ tracing thông thường đối với hầu hết nhà phát triển. - **godot_scripting**: Dùng để ghi lại các sự kiện scripting của Godot. Đây là một danh mục chậm vì nó profile toàn bộ logic scripting của game. Danh mục này được dùng để tìm hiểu mã / gỡ lỗi / tìm nguyên nhân gây ra hiện tượng giật khung hình. Hiệu năng chậm hơn nhiều, nhưng nó giúp tìm ra một lời gọi hàm có vấn đề vốn bị che khuất.

Ghi lại một trace
-----------------

Cuối cùng, khởi chạy game trên thiết bị Android bằng các template xuất mà bạn đã build trước đó.

Khi bạn sẵn sàng ghi lại một trace (ví dụ: khi đã đến phần game đang gặp vấn đề về hiệu năng), bạn có thể sử dụng `script này từ kho GitHub của Perfetto <https://github.com/google/perfetto/blob/main/tools/record_android_trace>`_.

.. code-block:: shell

    ./record_android_trace -c /path/to/godot.config

Thao tác này sẽ ghi lại trong 10 giây (theo cấu hình), hoặc cho đến khi bạn nhấn
:kbd:`Ctrl + C`.

Kiểm tra trace
--------------

Ngay khi script đó kết thúc, nó sẽ mở Perfetto UI trong trình duyệt web.

Để xem các sự kiện của Godot, hãy mở rộng hàng của ứng dụng bằng cách nhấp vào *Unique Name* / *Package Name* / *App ID* Android của ứng dụng (Perfetto cũng sẽ đưa vào trace một số sự kiện từ các dịch vụ hệ thống).

.. image:: img/cpp_profiler_perfetto.webp

Sau đó, bạn có thể sử dụng các phím ``WASD`` để điều hướng trên biểu đồ:

- Nhấn :kbd:`A` hoặc :kbd:`D` để di chuyển tiến hoặc lùi trên dòng thời gian - Nhấn :kbd:`W` hoặc :kbd:`S` để phóng to hoặc thu nhỏ

Có lẽ bạn sẽ cần phóng to một chút trước khi có thể thấy từng sự kiện riêng lẻ từ Godot.

Để tìm hiểu thêm, hãy xem `tài liệu Perfetto UI <https://perfetto.dev/docs/visualization/perfetto-ui>`_.
