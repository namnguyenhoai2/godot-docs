.. _doc_common_engine_methods_and_macros:

Các phương thức và macro engine phổ biến
========================================

Codebase C++ của Godot sử dụng hàng chục phương thức và macro tùy chỉnh, được dùng trong hầu hết mọi tệp. Trang này hướng đến những contributor mới bắt đầu, nhưng cũng có thể hữu ích cho những người viết module C++ tùy chỉnh.

In văn bản
----------

.. code-block:: cpp

    // In một thông báo ra standard output.
    print_line("Message");

    // Các đối số không phải String sẽ tự động được chuyển đổi thành String để in.
    // Nếu truyền nhiều đối số, chúng sẽ được nối lại với nhau bằng một
    // khoảng trắng giữa mỗi đối số.
    print_line("There are", 123, "nodes");

    // In một thông báo ra standard output, nhưng chỉ khi engine
    // được khởi động với đối số dòng lệnh `--verbose`.
    print_verbose("Message");

    // In một thông báo có định dạng phong phú bằng BBCode ra standard output.
    // Tính năng này hỗ trợ một tập hợp con các thẻ BBCode được RichTextLabel hỗ trợ
    // và cũng sẽ hiển thị với định dạng tương ứng trong bảng Output của editor.
    // Trên Windows, tính năng này yêu cầu Windows 10 trở lên để hoạt động trong terminal.
    print_line_rich("[b]Bold[/b], [color=red]Red text[/color]")

    // In một thông báo lỗi hoặc cảnh báo có định dạng kèm theo trace.
    ERR_PRINT("Message");
    WARN_PRINT("Message");

    // Chỉ in một lần mỗi session một thông báo lỗi hoặc cảnh báo.
    // Có thể dùng cách này để tránh spam console output.
    ERR_PRINT_ONCE("Message");
    WARN_PRINT_ONCE("Message");

Nếu cần thêm placeholder vào thông báo, hãy sử dụng format string như mô tả bên dưới.

Định dạng một string
--------------------

Hàm ``vformat()`` trả về một :ref:`class_String` đã được định dạng. Hàm này hoạt động tương tự như ``sprintf()`` của C:

.. code-block:: cpp

    vformat("My name is %s.", "Godette");
    vformat("%d bugs on the wall!", 1234);
    vformat("Pi is approximately %f.", 3.1416);

    // Chuyển String kết quả thành `const char *`.
    // Bạn có thể cần thực hiện việc này nếu truyền kết quả làm đối số
    // cho một phương thức yêu cầu `const char *` thay vì String.
    vformat("My name is %s.", "Godette").utf8().get_data();

Trong hầu hết trường hợp, hãy cố gắng sử dụng ``vformat()`` thay vì nối string, vì cách này giúp code dễ đọc hơn.

Chuyển đổi integer hoặc float thành string
------------------------------------------

Việc này không cần thiết khi in số bằng ``print_line()``, nhưng bạn vẫn có thể cần thực hiện chuyển đổi thủ công cho một số trường hợp sử dụng khác.

.. code-block:: cpp

    // Lưu string "42" bằng cách chuyển đổi integer thành string.
    String int_to_string = itos(42);

    // Lưu string "123.45" bằng cách chuyển đổi real thành string.
    String real_to_string = rtos(123.45);

Internationalize một string
---------------------------

Có hai loại internationalization trong codebase của Godot:

- ``TTR()``: Bản dịch **Editor ("tools")** chỉ được xử lý trong editor. Nếu người dùng sử dụng cùng văn bản đó trong một project của họ, văn bản sẽ không được dịch nếu họ cung cấp bản dịch cho nó. Khi đóng góp cho engine, đây thường là macro bạn nên sử dụng cho các string có thể localize. - ``RTR()``: **Bản dịch Runtime** sẽ tự động được localize trong các project nếu chúng cung cấp bản dịch cho string tương ứng. Không nên sử dụng loại bản dịch này trong code chỉ dành cho editor.

.. code-block:: cpp

    // Trả về string đã dịch tương ứng với thiết lập locale của người dùng.
    // Các bản dịch nằm trong `editor/translations`.
    // Template localization được tự động tạo; không được sửa đổi nó.
    TTR("Exit the editor?");

Để chèn placeholder vào các string có thể localize, hãy bọc macro localization trong một lời gọi ``vformat()`` như sau:

.. code-block:: cpp

    String file_path = "example.txt";
    vformat(TTR("Couldn't open \"%s\" for reading."), file_path);

.. note::

    Khi sử dụng ``vformat()`` cùng với một macro dịch, luôn bọc macro dịch trong ``vformat()``, không làm ngược lại. Nếu không, string sẽ không bao giờ khớp với bản dịch vì placeholder đã được thay thế trước khi string được truyền tới TranslationServer.

Giới hạn một giá trị
--------------------

Godot cung cấp các macro để giới hạn một giá trị với cận dưới (``MAX``), cận trên (``MIN``) hoặc cả hai (``CLAMP``):

.. code-block:: cpp

    int a = 3;
    int b = 5;

    MAX(b, 6); // 6
    MIN(2, a); // 2
    CLAMP(a, 10, 30); // 10

Điều này hoạt động với mọi kiểu có thể được so sánh với các giá trị khác (như ``int`` và ``float``).

Microbenchmarking
-----------------

Nếu muốn benchmark một đoạn code nhưng không biết cách sử dụng profiler, hãy dùng snippet này:

.. code-block:: cpp

    uint64_t begin = Time::get_singleton()->get_ticks_usec();

    // Code của bạn ở đây...

    uint64_t end = Time::get_singleton()->get_ticks_usec();
    print_line(vformat("Snippet took %d microseconds", end - begin));

Đoạn này sẽ in ra khoảng thời gian đã tiêu tốn giữa khai báo ``begin`` và khai báo ``end``.

.. note::

    Bạn có thể phải ``#include "core/os/time.h"`` nếu nó chưa tồn tại.

    Khi mở pull request, hãy nhớ xóa snippet này cũng như dòng include nếu trước đó nó chưa có.

Lấy thiết lập của project/editor
--------------------------------

Có bốn macro khả dụng cho việc này:

.. code-block:: cpp

    // Trả về giá trị của project setting được chỉ định,
    // mặc định là `false` nếu setting đó không tồn tại.
    GLOBAL_DEF("section/subsection/value", false);

    // Trả về giá trị của editor setting được chỉ định,
    // mặc định là "Untitled" nếu setting đó không tồn tại.
    EDITOR_DEF("section/subsection/value", "Untitled");

Nếu một giá trị mặc định đã được chỉ định ở nơi khác, đừng chỉ định lại để tránh lặp lại:

.. code-block:: cpp

    // Trả về giá trị của project setting.
    GLOBAL_GET("section/subsection/value");
    // Trả về giá trị của editor setting.
    EDITOR_GET("section/subsection/value");

It's recommended to use ``GLOBAL_DEF``/``EDITOR_DEF`` only once per setting and use ``GLOBAL_GET``/``EDITOR_GET`` in all other places where it's referenced.

.. _doc_common_engine_methods_and_macros_error_macros:

Các macro lỗi
-------------

Godot có nhiều macro lỗi để giúp việc báo cáo lỗi thuận tiện hơn.

.. warning::

    Các điều kiện trong macro lỗi hoạt động theo cách **ngược lại** với hàm ``assert()`` tích hợp sẵn của GDScript. Lỗi được phát hiện khi điều kiện bên trong đánh giá thành ``true``, chứ không phải ``false``.

.. note::

    Ở đây chỉ ghi lại các biến thể có thông báo tùy chỉnh, vì luôn nên sử dụng chúng trong các đóng góp mới. Hãy đảm bảo thông báo tùy chỉnh được cung cấp có đủ thông tin để mọi người chẩn đoán vấn đề, ngay cả khi họ không biết C++. Nếu một phương thức được truyền các đối số không hợp lệ, bạn có thể in giá trị không hợp lệ đó để việc debug dễ dàng hơn.

    Đối với việc kiểm tra lỗi nội bộ, khi không cần hiển thị thông báo dễ đọc cho con người, hãy xóa ``_MSG`` ở cuối tên macro và không cung cấp đối số thông báo.

    Ngoài ra, luôn cố gắng trả về dữ liệu có thể xử lý để engine có thể tiếp tục chạy ổn định.

.. code-block:: cpp

    // In có điều kiện một thông báo lỗi và return khỏi function.
    // Sử dụng macro này trong các phương thức không return giá trị.
    ERR_FAIL_COND_MSG(!mesh.is_valid(), vformat("Couldn't load mesh at: %s", path));

    // In có điều kiện một thông báo lỗi và return `0` khỏi function.
    // Sử dụng macro này trong các phương thức bắt buộc phải return một giá trị.
    ERR_FAIL_COND_V_MSG(rect.x < 0 || rect.y < 0, 0,
            "Couldn't calculate the rectangle's area.");

    // In một thông báo lỗi nếu `index` < 0 hoặc >= `SomeEnum::QUALITY_MAX`,
    // sau đó return khỏi function.
    ERR_FAIL_INDEX_MSG(index, SomeEnum::QUALITY_MAX,
            vformat("Invalid quality: %d. See SomeEnum for allowed values.", index));

    // In một thông báo lỗi nếu `index` < 0 >= `some_array.size()`,
    // sau đó return `-1` khỏi function.
    ERR_FAIL_INDEX_V_MSG(index, some_array.size(), -1,
            vformat("Item %d is out of bounds.", index));

    // Luôn in một thông báo lỗi và return khỏi function.
    // Chỉ sử dụng macro này nếu bạn cần thực hiện việc kiểm tra lỗi phức tạp.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_MSG("Couldn't reload the filesystem cache.");
    }

    // Luôn in một thông báo lỗi và return `false` khỏi function.
    // Chỉ sử dụng macro này nếu bạn cần thực hiện việc kiểm tra lỗi phức tạp.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_V_MSG(false, "Couldn't parse the input arguments.");
    }

    // Làm engine crash. Nhìn chung, tuyệt đối không nên sử dụng macro này
    // ngoại trừ khi kiểm thử code xử lý crash. Triết lý của Godot
    // là không bao giờ crash, cả trong editor lẫn trong các project đã export.
    CRASH_NOW_MSG("Can't predict the future! Aborting.");


.. seealso::

    Xem `core/error/error_macros.h <https://github.com/godotengine/godot/blob/master/core/error/error_macros.h>`__ trong codebase của Godot để biết thêm thông tin về từng macro lỗi.

    Một số function return error code (được thể hiện bằng kiểu return ``Error``). Giá trị này có thể được return trực tiếp từ một macro lỗi. Xem danh sách các error code khả dụng trong `core/error/error_list.h <https://github.com/godotengine/godot/blob/master/core/error/error_list.h>`__.
