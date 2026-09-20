.. _doc_common_engine_methods_and_macros:

Các phương thức và macro phổ biến của engine
============================================

Cơ sở mã C++ của Godot sử dụng hàng chục phương thức và macro tùy chỉnh, được dùng trong hầu hết mọi tệp. Trang này hướng đến những người mới đóng góp, nhưng cũng có thể hữu ích cho những người viết mô-đun C++ tùy chỉnh.

In văn bản
----------

.. code-block:: cpp

    // Prints a message to standard output.
    print_line("Message");

    // Non-String arguments are automatically converted to String for printing.
    // If passing several arguments, they will be concatenated together with a
    // space between each argument.
    print_line("There are", 123, "nodes");

    // Prints a message to standard output, but only when the engine
    // is started with the `--verbose` command line argument.
    print_verbose("Message");

    // Prints a rich-formatted message using BBCode to standard output.
    // This supports a subset of BBCode tags supported by RichTextLabel
    // and will also appear formatted in the editor Output panel.
    // On Windows, this requires Windows 10 or later to work in the terminal.
    print_line_rich("[b]Bold[/b], [color=red]Red text[/color]")

    // Prints a formatted error or warning message with a trace.
    ERR_PRINT("Message");
    WARN_PRINT("Message");

    // Prints an error or warning message only once per session.
    // This can be used to avoid spamming the console output.
    ERR_PRINT_ONCE("Message");
    WARN_PRINT_ONCE("Message");

Nếu cần thêm placeholder vào thông báo, hãy sử dụng chuỗi định dạng như mô tả bên dưới.

Định dạng chuỗi
---------------

Hàm ``vformat()`` trả về một :ref:`class_String` đã được định dạng. Cách hoạt động của nó tương tự như ``sprintf()`` của C:

.. code-block:: cpp

    vformat("My name is %s.", "Godette");
    vformat("%d bugs on the wall!", 1234);
    vformat("Pi is approximately %f.", 3.1416);

    // Converts the resulting String into a `const char *`.
    // You may need to do this if passing the result as an argument
    // to a method that expects a `const char *` instead of a String.
    vformat("My name is %s.", "Godette").utf8().get_data();

Trong hầu hết trường hợp, hãy cố gắng sử dụng ``vformat()`` thay vì nối chuỗi, vì cách này giúp mã dễ đọc hơn.

Chuyển đổi số nguyên hoặc số thực thành chuỗi
---------------------------------------------

Điều này không cần thiết khi in số bằng ``print_line()``, nhưng bạn vẫn có thể cần thực hiện chuyển đổi thủ công cho một số trường hợp sử dụng khác.

.. code-block:: cpp

    // Stores the string "42" using integer-to-string conversion.
    String int_to_string = itos(42);

    // Stores the string "123.45" using real-to-string conversion.
    String real_to_string = rtos(123.45);

Quốc tế hóa chuỗi
-----------------

Có hai loại quốc tế hóa trong cơ sở mã của Godot:

- ``TTR()``: **Bản dịch Editor ("tools")** chỉ được xử lý trong editor. Nếu người dùng sử dụng cùng văn bản đó trong một dự án của họ, văn bản sẽ không được dịch nếu họ cung cấp bản dịch cho nó. Khi đóng góp cho engine, đây thường là macro bạn nên sử dụng cho các chuỗi có thể bản địa hóa. - ``RTR()``: **Bản dịch Runtime** sẽ được tự động bản địa hóa trong các dự án nếu chúng cung cấp bản dịch cho chuỗi tương ứng. Không nên sử dụng loại bản dịch này trong mã chỉ dành cho editor.

.. code-block:: cpp

    // Returns the translated string that matches the user's locale settings.
    // Translations are located in `editor/translations`.
    // The localization template is generated automatically; don't modify it.
    TTR("Exit the editor?");

Để chèn placeholder vào các chuỗi có thể bản địa hóa, hãy bọc macro bản địa hóa trong một lời gọi ``vformat()`` như sau:

.. code-block:: cpp

    String file_path = "example.txt";
    vformat(TTR("Couldn't open \"%s\" for reading."), file_path);

.. note::

    Khi sử dụng ``vformat()`` cùng với một macro dịch, luôn bọc macro dịch trong ``vformat()``, không làm ngược lại. Nếu không, chuỗi sẽ không bao giờ khớp với bản dịch vì placeholder đã được thay thế trước khi chuỗi được truyền đến TranslationServer.

Giới hạn một giá trị
--------------------

Godot cung cấp các macro để giới hạn một giá trị với cận dưới (``MAX``), cận trên (``MIN``) hoặc cả hai (``CLAMP``):

.. code-block:: cpp

    int a = 3;
    int b = 5;

    MAX(b, 6); // 6
    MIN(2, a); // 2
    CLAMP(a, 10, 30); // 10

Cách này hoạt động với mọi kiểu có thể được so sánh với các giá trị khác (chẳng hạn như ``int`` và ``float``).

Đo hiệu năng vi mô
------------------

Nếu muốn đo hiệu năng một đoạn mã nhưng không biết cách sử dụng trình phân tích hiệu năng, hãy dùng đoạn mã sau:

.. code-block:: cpp

    uint64_t begin = Time::get_singleton()->get_ticks_usec();

    // Your code here...

    uint64_t end = Time::get_singleton()->get_ticks_usec();
    print_line(vformat("Snippet took %d microseconds", end - begin));

Đoạn mã này sẽ in ra thời gian đã sử dụng giữa khai báo ``begin`` và khai báo ``end``.

.. note::

    Bạn có thể phải ``#include "core/os/time.h"`` nếu nó chưa có sẵn.

    Khi mở một pull request, hãy nhớ xóa cả đoạn mã này lẫn include nếu trước đó chưa có include này.

Lấy cài đặt dự án/editor
------------------------

Có bốn macro được cung cấp cho việc này:

.. code-block:: cpp

    // Returns the specified project setting's value,
    // defaulting to `false` if it doesn't exist.
    GLOBAL_DEF("section/subsection/value", false);

    // Returns the specified editor setting's value,
    // defaulting to "Untitled" if it doesn't exist.
    EDITOR_DEF("section/subsection/value", "Untitled");

Nếu một giá trị mặc định đã được chỉ định ở nơi khác, đừng chỉ định lại để tránh lặp lại:

.. code-block:: cpp

    // Returns the value of the project setting.
    GLOBAL_GET("section/subsection/value");
    // Returns the value of the editor setting.
    EDITOR_GET("section/subsection/value");

Bạn nên chỉ sử dụng ``GLOBAL_DEF``/``EDITOR_DEF`` một lần cho mỗi cài đặt và sử dụng ``GLOBAL_GET``/``EDITOR_GET`` ở mọi nơi khác có tham chiếu đến cài đặt đó.

.. _doc_common_engine_methods_and_macros_error_macros:

Các macro lỗi
-------------

Godot cung cấp nhiều macro lỗi để việc báo cáo lỗi trở nên thuận tiện hơn.

.. warning::

    Các điều kiện trong macro lỗi hoạt động theo cách **ngược lại** với hàm ``assert()`` tích hợp sẵn của GDScript. Lỗi xảy ra nếu điều kiện bên trong đánh giá thành ``true``, chứ không phải ``false``.

.. note::

    Ở đây chỉ ghi lại các biến thể có thông báo tùy chỉnh, vì đây là những biến thể luôn nên được sử dụng trong các đóng góp mới. Hãy đảm bảo thông báo tùy chỉnh được cung cấp chứa đủ thông tin để mọi người chẩn đoán vấn đề, ngay cả khi họ không biết C++. Nếu một phương thức được truyền các đối số không hợp lệ, bạn có thể in giá trị không hợp lệ đó để giúp việc gỡ lỗi dễ dàng hơn.

    Đối với việc kiểm tra lỗi nội bộ khi không cần hiển thị thông báo dễ hiểu cho con người, hãy xóa ``_MSG`` ở cuối tên macro và không cung cấp đối số thông báo.

    Ngoài ra, hãy luôn cố gắng trả về dữ liệu có thể xử lý để engine có thể tiếp tục chạy ổn định.

.. code-block:: cpp

    // Conditionally prints an error message and returns from the function.
    // Use this in methods which don't return a value.
    ERR_FAIL_COND_MSG(!mesh.is_valid(), vformat("Couldn't load mesh at: %s", path));

    // Conditionally prints an error message and returns `0` from the function.
    // Use this in methods which must return a value.
    ERR_FAIL_COND_V_MSG(rect.x < 0 || rect.y < 0, 0,
            "Couldn't calculate the rectangle's area.");

    // Prints an error message if `index` is < 0 or >= `SomeEnum::QUALITY_MAX`,
    // then returns from the function.
    ERR_FAIL_INDEX_MSG(index, SomeEnum::QUALITY_MAX,
            vformat("Invalid quality: %d. See SomeEnum for allowed values.", index));

    // Prints an error message if `index` is < 0 >= `some_array.size()`,
    // then returns `-1` from the function.
    ERR_FAIL_INDEX_V_MSG(index, some_array.size(), -1,
            vformat("Item %d is out of bounds.", index));

    // Unconditionally prints an error message and returns from the function.
    // Only use this if you need to perform complex error checking.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_MSG("Couldn't reload the filesystem cache.");
    }

    // Unconditionally prints an error message and returns `false` from the function.
    // Only use this if you need to perform complex error checking.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_V_MSG(false, "Couldn't parse the input arguments.");
    }

    // Crashes the engine. This should generally never be used
    // except for testing crash handling code. Godot's philosophy
    // is to never crash, both in the editor and in exported projects.
    CRASH_NOW_MSG("Can't predict the future! Aborting.");


.. seealso::

    Xem `core/error/error_macros.h <https://github.com/godotengine/godot/blob/master/core/error/error_macros.h>`__ trong cơ sở mã của Godot để biết thêm thông tin về từng macro lỗi.

    Một số hàm trả về mã lỗi (được thể hiện bằng kiểu trả về ``Error``). Giá trị này có thể được trả về trực tiếp từ một macro lỗi. Xem danh sách các mã lỗi có sẵn trong `core/error/error_list.h <https://github.com/godotengine/godot/blob/master/core/error/error_list.h>`__.
