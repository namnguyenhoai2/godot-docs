.. _doc_common_engine_methods_and_macros:

Các phương thức và macro engine thường dùng
===========================================

Codebase C++ của Godot sử dụng hàng chục phương thức và macro tùy chỉnh, được dùng trong gần như mọi tệp. Trang này hướng đến những người mới đóng góp, nhưng cũng có thể hữu ích cho những ai viết các module C++ tùy chỉnh.

In văn bản
----------

.. code-block:: cpp

    // In một thông báo ra đầu ra chuẩn.
    print_line("Message");

    // Các đối số không phải String sẽ tự động được chuyển đổi thành String để in.
    // Nếu truyền nhiều đối số, chúng sẽ được nối lại với nhau bằng một
    // dấu cách giữa mỗi đối số.
    print_line("There are", 123, "nodes");

    // In một thông báo ra đầu ra chuẩn, nhưng chỉ khi engine
    // được khởi động với đối số dòng lệnh `--verbose`.
    print_verbose("Message");

    // In một thông báo có định dạng phong phú bằng BBCode ra đầu ra chuẩn.
    // Hỗ trợ một tập hợp con các thẻ BBCode được RichTextLabel hỗ trợ
    // và cũng sẽ hiển thị với định dạng tương ứng trong bảng Output của editor.
    // Trên Windows, cần Windows 10 trở lên để hoạt động trong terminal.
    print_line_rich("[b]Bold[/b], [color=red]Red text[/color]")

    // In một thông báo lỗi hoặc cảnh báo có định dạng kèm trace.
    ERR_PRINT("Message");
    WARN_PRINT("Message");

    // Chỉ in một lần mỗi phiên một thông báo lỗi hoặc cảnh báo.
    // Có thể dùng cách này để tránh làm ngập đầu ra của console.
    ERR_PRINT_ONCE("Message");
    WARN_PRINT_ONCE("Message");

Nếu cần thêm placeholder vào thông báo, hãy sử dụng chuỗi định dạng như mô tả bên dưới.

Định dạng một chuỗi
-------------------

Hàm ``vformat()`` trả về một :ref:`class_String` đã được định dạng. Cách hoạt động tương tự ``sprintf()`` của C:

.. code-block:: cpp

    vformat("My name is %s.", "Godette");
    vformat("%d bugs on the wall!", 1234);
    vformat("Pi is approximately %f.", 3.1416);

    // Chuyển String kết quả thành một `const char *`.
    // Bạn có thể cần thực hiện việc này nếu truyền kết quả làm đối số
    // cho một phương thức yêu cầu `const char *` thay vì String.
    vformat("My name is %s.", "Godette").utf8().get_data();

Trong hầu hết trường hợp, hãy dùng ``vformat()`` thay vì nối chuỗi vì cách này giúp code dễ đọc hơn.

Chuyển đổi số nguyên hoặc số thực thành chuỗi
---------------------------------------------

Không cần thực hiện việc này khi in số bằng ``print_line()``, nhưng bạn vẫn có thể cần chuyển đổi thủ công cho một số trường hợp sử dụng khác.

.. code-block:: cpp

    // Lưu chuỗi "42" bằng cách chuyển đổi số nguyên thành chuỗi.
    String int_to_string = itos(42);

    // Lưu chuỗi "123.45" bằng cách chuyển đổi số thực thành chuỗi.
    String real_to_string = rtos(123.45);

Quốc tế hóa một chuỗi
---------------------

Có hai loại quốc tế hóa trong codebase của Godot:

- ``TTR()``: **Bản dịch Editor ("tools")** chỉ được xử lý trong editor. Nếu người dùng sử dụng cùng văn bản đó trong một project của họ, văn bản sẽ không được dịch nếu họ cung cấp bản dịch cho nó. Khi đóng góp cho engine, đây thường là macro bạn nên dùng cho các chuỗi có thể bản địa hóa.
- ``RTR()``: **Bản dịch Runtime** sẽ tự động được bản địa hóa trong các project nếu chúng cung cấp bản dịch cho chuỗi tương ứng. Không nên sử dụng loại bản dịch này trong code chỉ dành cho editor.

.. code-block:: cpp

    // Trả về chuỗi đã dịch tương ứng với cài đặt locale của người dùng.
    // Các bản dịch nằm trong `editor/translations`.
    // Mẫu bản địa hóa được tự động tạo; đừng sửa đổi nó.
    TTR("Exit the editor?");

Để chèn placeholder vào các chuỗi có thể bản địa hóa, hãy bọc macro bản địa hóa trong một lệnh gọi ``vformat()`` như sau:

.. code-block:: cpp

    String file_path = "example.txt";
    vformat(TTR("Couldn't open \"%s\" for reading."), file_path);

.. note::

    Khi sử dụng ``vformat()`` cùng với macro dịch, luôn bọc macro dịch trong ``vformat()``, không làm ngược lại. Nếu không, chuỗi sẽ không bao giờ khớp với bản dịch vì placeholder đã được thay thế trước khi chuỗi được truyền tới TranslationServer.

Giới hạn một giá trị
--------------------

Godot cung cấp các macro để giới hạn một giá trị với cận dưới (``MAX``), cận trên (``MIN``) hoặc cả hai (``CLAMP``):

.. code-block:: cpp

    int a = 3;
    int b = 5;

    MAX(b, 6); // 6
    MIN(2, a); // 2
    CLAMP(a, 10, 30); // 10

Cách này hoạt động với mọi kiểu có thể được so sánh với các giá trị khác (như ``int`` và ``float``).

Microbenchmark
--------------

Nếu muốn benchmark một đoạn code nhưng không biết cách sử dụng profiler, hãy dùng đoạn mã sau:

.. code-block:: cpp

    uint64_t begin = Time::get_singleton()->get_ticks_usec();

    // Code của bạn ở đây...

    uint64_t end = Time::get_singleton()->get_ticks_usec();
    print_line(vformat("Snippet took %d microseconds", end - begin));

Đoạn mã này sẽ in thời gian đã trôi qua giữa khai báo ``begin`` và khai báo ``end``.

.. note::

    Bạn có thể phải ``#include "core/os/time.h"`` nếu nó chưa có sẵn.

    Khi mở pull request, hãy nhớ xóa đoạn mã này cũng như câu lệnh include nếu trước đó chưa có nó.

Lấy cài đặt project/editor
--------------------------

Có bốn macro dành cho việc này:

.. code-block:: cpp

    // Trả về giá trị của cài đặt project được chỉ định,
    // mặc định là `false` nếu cài đặt đó không tồn tại.
    GLOBAL_DEF("section/subsection/value", false);

    // Trả về giá trị của cài đặt editor được chỉ định,
    // mặc định là "Untitled" nếu cài đặt đó không tồn tại.
    EDITOR_DEF("section/subsection/value", "Untitled");

Nếu một giá trị mặc định đã được chỉ định ở nơi khác, đừng chỉ định lại để tránh lặp lại:

.. code-block:: cpp

    // Trả về giá trị của cài đặt project.
    GLOBAL_GET("section/subsection/value");
    // Trả về giá trị của cài đặt editor.
    EDITOR_GET("section/subsection/value");

Bạn nên chỉ sử dụng ``GLOBAL_DEF``/``EDITOR_DEF`` một lần cho mỗi cài đặt và sử dụng ``GLOBAL_GET``/``EDITOR_GET`` ở mọi vị trí khác có tham chiếu đến cài đặt đó.

.. _doc_common_engine_methods_and_macros_error_macros:

Macro xử lý lỗi
---------------

Godot cung cấp nhiều macro xử lý lỗi để việc báo cáo lỗi trở nên thuận tiện hơn.

.. warning::

    Các điều kiện trong macro xử lý lỗi hoạt động theo cách **ngược lại** so với hàm dựng sẵn ``assert()`` của GDScript. Lỗi xảy ra nếu điều kiện bên trong đánh giá thành ``true``, chứ không phải ``false``.

.. note::

    Tài liệu ở đây chỉ đề cập đến các biến thể có thông báo tùy chỉnh, vì luôn nên sử dụng các biến thể này trong những đóng góp mới. Hãy đảm bảo thông báo tùy chỉnh được cung cấp có đủ thông tin để mọi người chẩn đoán vấn đề, ngay cả khi họ không biết C++. Nếu một phương thức được truyền các đối số không hợp lệ, bạn có thể in giá trị không hợp lệ đó để việc gỡ lỗi dễ dàng hơn.

    Đối với việc kiểm tra lỗi nội bộ khi không cần hiển thị thông báo dễ đọc, hãy xóa ``_MSG`` ở cuối tên macro và không cung cấp đối số thông báo.

    Ngoài ra, luôn cố gắng trả về dữ liệu có thể xử lý để engine tiếp tục hoạt động ổn định.

.. code-block:: cpp

    // In có điều kiện một thông báo lỗi rồi return khỏi hàm.
    // Sử dụng macro này trong các phương thức không trả về giá trị.
    ERR_FAIL_COND_MSG(!mesh.is_valid(), vformat("Couldn't load mesh at: %s", path));

    // In có điều kiện một thông báo lỗi rồi return `0` khỏi hàm.
    // Sử dụng macro này trong các phương thức bắt buộc phải trả về một giá trị.
    ERR_FAIL_COND_V_MSG(rect.x < 0 || rect.y < 0, 0,
            "Couldn't calculate the rectangle's area.");

    // In một thông báo lỗi nếu `index` < 0 hoặc >= `SomeEnum::QUALITY_MAX`,
    // sau đó return khỏi hàm.
    ERR_FAIL_INDEX_MSG(index, SomeEnum::QUALITY_MAX,
            vformat("Invalid quality: %d. See SomeEnum for allowed values.", index));

    // In một thông báo lỗi nếu `index` < 0 >= `some_array.size()`,
    // sau đó return `-1` khỏi hàm.
    ERR_FAIL_INDEX_V_MSG(index, some_array.size(), -1,
            vformat("Item %d is out of bounds.", index));

    // Vô điều kiện in một thông báo lỗi rồi return khỏi hàm.
    // Chỉ sử dụng macro này nếu bạn cần thực hiện việc kiểm tra lỗi phức tạp.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_MSG("Couldn't reload the filesystem cache.");
    }

    // Vô điều kiện in một thông báo lỗi rồi return `false` khỏi hàm.
    // Chỉ sử dụng macro này nếu bạn cần thực hiện việc kiểm tra lỗi phức tạp.
    if (!complex_error_checking_routine()) {
        ERR_FAIL_V_MSG(false, "Couldn't parse the input arguments.");
    }

    // Làm engine bị crash. Nhìn chung, không bao giờ nên sử dụng macro này
    // ngoại trừ khi kiểm thử mã xử lý crash. Triết lý của Godot
    // là không bao giờ bị crash, cả trong editor lẫn trong các project đã export.
    CRASH_NOW_MSG("Can't predict the future! Aborting.");


.. seealso::

    Xem `core/error/error_macros.h <https://github.com/godotengine/godot/blob/master/core/error/error_macros.h>`__ trong codebase của Godot để biết thêm thông tin về từng macro xử lý lỗi.

    Một số hàm trả về mã lỗi (được thể hiện bằng kiểu trả về ``Error``). Giá trị này có thể được return trực tiếp từ macro xử lý lỗi. Xem danh sách các mã lỗi hiện có trong `core/error/error_list.h <https://github.com/godotengine/godot/blob/master/core/error/error_list.h>`__.
