.. _doc_unit_testing:

Kiểm thử đơn vị
===============

Godot Engine cho phép viết các bài kiểm thử đơn vị trực tiếp bằng C++. Engine tích hợp framework kiểm thử đơn vị `doctest <https://github.com/doctest/doctest>`_, cho phép viết các test suite và test case bên cạnh mã production, nhưng vì các bài kiểm thử trong Godot đi qua một điểm vào ``main`` khác, nên thay vào đó, các bài kiểm thử nằm trong một thư mục ``tests/`` riêng, được đặt ở thư mục gốc của mã nguồn engine.

Hỗ trợ nền tảng và target
-------------------------

Các bài kiểm thử đơn vị C++ có thể chạy trên hệ điều hành Linux, macOS và Windows.

Chỉ có thể chạy các bài kiểm thử khi bật ``tools`` của editor, nghĩa là hiện tại chưa thể kiểm thử các export template.

Chạy các bài kiểm thử
---------------------

Trước khi thực sự chạy được các bài kiểm thử, engine phải được biên dịch với tùy chọn build ``tests`` được bật (cùng mọi tùy chọn build khác mà bạn thường sử dụng), vì các bài kiểm thử không được biên dịch cùng engine theo mặc định:

.. code-block:: shell

    scons tests=yes

Sau khi build xong, chạy các bài kiểm thử bằng tùy chọn dòng lệnh ``--test``:

.. code-block:: shell

    ./bin/<godot_binary> --test

Có thể cấu hình lần chạy kiểm thử bằng nhiều tùy chọn dòng lệnh dành riêng cho doctest. Để lấy danh sách đầy đủ các tùy chọn được hỗ trợ, hãy chạy lệnh ``--test`` với tùy chọn ``--help``:

.. code-block:: shell

    ./bin/<godot_binary> --test --help

Mọi tùy chọn và đối số khác sau lệnh ``--test`` được xem là đối số dành cho doctest.

.. note::

    Các bài kiểm thử được tự động biên dịch nếu bạn sử dụng tùy chọn SCons ``dev_mode=yes``. Khuyến nghị dùng ``dev_mode=yes`` nếu bạn dự định đóng góp cho quá trình phát triển engine, vì tùy chọn này sẽ tự động coi các cảnh báo biên dịch là lỗi. Hệ thống continuous integration sẽ thất bại nếu phát hiện bất kỳ cảnh báo biên dịch nào, vì vậy bạn nên cố gắng sửa mọi cảnh báo trước khi mở pull request.

Lọc các bài kiểm thử
~~~~~~~~~~~~~~~~~~~~

Theo mặc định, tất cả bài kiểm thử sẽ được chạy nếu bạn không cung cấp thêm đối số nào sau lệnh ``--test``. Tuy nhiên, nếu đang viết bài kiểm thử mới hoặc muốn xem output của các assertion thành công từ những bài kiểm thử đó để debug, bạn có thể chạy các bài kiểm thử cần quan tâm bằng nhiều tùy chọn lọc do doctest cung cấp.

Cú pháp wildcard ``*`` được hỗ trợ để khớp với bất kỳ số lượng ký tự nào trong test suite, test case và tên tệp mã nguồn:

+--------------------+---------------+------------------------+
| **Filter options** | **Shorthand** | **Examples**           |
+--------------------+---------------+------------------------+
| ``--test-suite``   | ``-ts``       | ``-ts="*[GDScript]*"`` |
+--------------------+---------------+------------------------+
| ``--test-case``    | ``-tc``       | ``-tc="*[String]*"``   |
+--------------------+---------------+------------------------+
| ``--source-file``  | ``-sf``       | ``-sf="*test_color*"`` |
+--------------------+---------------+------------------------+

Ví dụ, để chỉ chạy các bài kiểm thử đơn vị ``String``, hãy chạy:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case="*[String]*"

Có thể bật output của các assertion thành công bằng tùy chọn ``--success`` (``-s``), và kết hợp tùy chọn này với bất kỳ tổ hợp nào của các tùy chọn lọc ở trên, chẳng hạn:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_color*" --success

Có thể bỏ qua các bài kiểm thử cụ thể bằng các tùy chọn ``-exclude`` tương ứng. Hiện tại, một số bài kiểm thử bao gồm các bài kiểm thử stress ngẫu nhiên, mất khá nhiều thời gian để thực thi. Để bỏ qua những loại bài kiểm thử này, hãy chạy lệnh sau:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case-exclude="*[Stress]*"

Viết các bài kiểm thử
---------------------

Test suite đại diện cho các tệp triển khai C++ phải include macro ``TEST_FORCE_LINK()``. Hầu hết test suite được đặt trực tiếp trong thư mục ``tests/``.

Tất cả tệp kiểm thử đều có tiền tố ``test_``, đây là quy ước đặt tên mà hệ thống build của Godot dựa vào để phát hiện các bài kiểm thử trong toàn bộ engine.

Dưới đây là một test suite tối thiểu có thể hoạt động, với một test case duy nhất được viết như sau:

.. code-block:: cpp

    #include "tests/test_macros.h"

    TEST_FORCE_LINK(test_string)

    namespace TestString {

    TEST_CASE("[String] Hello World!") {
        String hello = "Hello World!";
        CHECK(hello == "Hello World!");
    }

    } // namespace TestString

.. note::
    Bạn có thể nhanh chóng tạo các bài kiểm thử mới bằng script ``create_test.py`` nằm trong thư mục ``tests/``. Script này tự động tạo một tệp kiểm thử mới với mã boilerplate cần thiết ở vị trí phù hợp. Để xem hướng dẫn sử dụng, hãy chạy script với flag ``-h``.

Header ``tests/test_macros.h`` đóng gói mọi thứ cần thiết để viết các bài kiểm thử đơn vị C++ trong Godot. Header này bao gồm các macro assertion và logging của doctest, chẳng hạn như ``CHECK`` như ở trên, và tất nhiên cả các định nghĩa để viết test case.

.. seealso::

    Mã nguồn `tests/test_macros.h <https://github.com/godotengine/godot/blob/master/tests/test_macros.h>`_ cho các macro hiện được triển khai và các alias của chúng.

Test case được tạo bằng macro dạng hàm ``TEST_CASE``. Mỗi test case phải có một mô tả ngắn được viết trong dấu ngoặc đơn, tùy chọn bao gồm các tag tùy chỉnh cho phép lọc bài kiểm thử tại runtime, chẳng hạn như ``[String]``, ``[Stress]`` và các tag khác.

Test case được viết trong một namespace riêng. Điều này không bắt buộc, nhưng giúp tránh xung đột tên khi viết các hàm helper static khác để hỗ trợ những quy trình kiểm thử lặp lại, chẳng hạn như tạo dữ liệu kiểm thử dùng chung cho mỗi test hoặc viết các bài kiểm thử tham số hóa.

Godot hỗ trợ viết bài kiểm thử theo từng module C++. Để biết hướng dẫn viết bài kiểm thử module, hãy tham khảo :ref:`doc_custom_module_unit_tests`.

Subcase
~~~~~~~

Trong trường hợp bạn có phần setup chung cho nhiều test case với chỉ một vài khác biệt nhỏ, subcase có thể rất hữu ích. Dưới đây là một ví dụ:

.. code-block:: cpp

    TEST_CASE("[SceneTree][Node] Testing node operations with a very simple scene tree") {
        // ... phần setup chung (ví dụ: tạo một scene tree với một vài node)
        SUBCASE("Move node to specific index") {
            // ... phần setup và các bước kiểm tra để di chuyển một node
        }
        SUBCASE("Remove node at specific index") {
            // ... phần setup và các bước kiểm tra để xóa một node
        }
    }

Mỗi ``SUBCASE`` khiến ``TEST_CASE`` được thực thi lại từ đầu. Có thể lồng subcase ở độ sâu tùy ý, nhưng nên giới hạn việc lồng này không quá một cấp.

Assertion
~~~~~~~~~

Danh sách tất cả assertion thường được sử dụng trong các bài kiểm thử của Godot, được sắp xếp theo mức độ nghiêm trọng.

+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| **Assertion**     | **Description**                                                                                                                  |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``REQUIRE``       | Test if condition holds true. Fails the entire test immediately if the condition does not hold true.                             |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``REQUIRE_FALSE`` | Test if condition does not hold true. Fails the entire test immediately if the condition holds true.                             |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``CHECK``         | Test if condition holds true. Marks the test run as failing, but allow to run other assertions.                                  |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``CHECK_FALSE``   | Test if condition does not hold true. Marks the test run as failing, but allow to run other assertions.                          |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``WARN``          | Test if condition holds true. Does not fail the test under any circumstance, but logs a warning if something does not hold true. |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| ``WARN_FALSE``    | Test if condition does not hold true. Does not fail the test under any circumstance, but logs a warning if something holds true. |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------+

Tất cả assertion ở trên đều có các macro ``*_MESSAGE`` tương ứng, cho phép in một thông báo tùy chọn giải thích lý do điều gì đó nên xảy ra.

Ưu tiên sử dụng ``CHECK`` cho các assertion tự giải thích và ``CHECK_MESSAGE`` cho những assertion phức tạp hơn nếu bạn cho rằng chúng cần được giải thích rõ hơn.

.. seealso::

    `doctest: Assertion macros <https://github.com/doctest/doctest/blob/master/doc/markdown/assertions.md>`_.

Logging
~~~~~~~

Output của bài kiểm thử do chính doctest xử lý và hoàn toàn không dựa vào chức năng in hoặc logging của Godot, vì vậy nên sử dụng các macro chuyên dụng cho phép ghi output kiểm thử theo định dạng do doctest tạo ra.

+----------------+-----------------------------------------------------------------------------------------------------------+
| **Macro**      | **Description**                                                                                           |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``MESSAGE``    | Prints a message.                                                                                         |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``FAIL_CHECK`` | Marks the test as failing, but continue the execution. Can be wrapped in conditionals for complex checks. |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``FAIL``       | Fails the test immediately. Can be wrapped in conditionals for complex checks.                            |
+----------------+-----------------------------------------------------------------------------------------------------------+

Có thể chọn các reporter khác nhau tại runtime. Ví dụ, dưới đây là cách chuyển hướng output vào một tệp XML:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_validate*" --success --reporters=xml --out=doctest.txt

.. seealso::

    `doctest: Logging macros <https://github.com/doctest/doctest/blob/master/doc/markdown/logging.md>`_.

Kiểm thử các nhánh lỗi
~~~~~~~~~~~~~~~~~~~~~~

Đôi khi không phải lúc nào cũng khả thi để kiểm thử một kết quả *được mong đợi*. Theo triết lý phát triển của Godot rằng engine không nên crash và phải phục hồi một cách an toàn khi xảy ra lỗi không nghiêm trọng, điều quan trọng là phải kiểm tra rằng các nhánh lỗi đó thực sự an toàn để thực thi mà không làm engine crash.

Có thể kiểm thử hành vi *không mong đợi* theo cách tương tự mọi thứ khác. Vấn đề duy nhất là việc này sẽ khiến output kiểm thử bị làm nhiễu không cần thiết bởi các lỗi do chính engine in ra (ngay cả khi kết quả cuối cùng là thành công).

Để giải quyết vấn đề này, hãy sử dụng trực tiếp các macro ``ERR_PRINT_OFF`` và ``ERR_PRINT_ON`` bên trong test case nhằm tạm thời vô hiệu hóa output lỗi từ engine, chẳng hạn:

.. code-block:: cpp

    TEST_CASE("[Color] Constructor methods") {
        ERR_PRINT_OFF;
        Color html_invalid = Color::html("invalid");
        ERR_PRINT_ON; // Đừng quên bật lại!

        CHECK_MESSAGE(html_invalid.is_equal_approx(Color()),
            "Invalid HTML notation should result in a Color with the default values.");
    }

Tag đặc biệt trong tên test case
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể thêm các tag này vào tên test case để sửa đổi hoặc mở rộng môi trường kiểm thử:

+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Tag**            | **Description**                                                                                                                                                      |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[SceneTree]``    | Required for test cases that rely on a scene tree with MessageQueue to be available. It also enables a mock rendering server and :ref:`ThemeDB<class_ThemeDB>`.      |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Editor]``       | Like ``[SceneTree]``, but with additional editor-related infrastructure available, such as :ref:`EditorSettings<class_EditorSettings>`.                              |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Audio]``        | Initializes the :ref:`AudioServer<class_AudioServer>` using a mock audio driver.                                                                                     |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Navigation2D]`` | Creates the default 2D navigation server and makes it available for testing.                                                                                         |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Navigation3D]`` | Creates the default 3D navigation server and makes it available for testing.                                                                                         |
+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Bạn có thể sử dụng chúng cùng nhau để kết hợp nhiều phần mở rộng môi trường kiểm thử.

Kiểm thử signal
~~~~~~~~~~~~~~~

Có thể sử dụng các macro sau để kiểm thử signal:

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Macro
     - Mô tả
   * - ``SIGNAL_WATCH(object, "signal_name")``
     - Bắt đầu theo dõi signal được chỉ định trên object đã cho.
   * - ``SIGNAL_UNWATCH(object, "signal_name")``
     - Dừng theo dõi signal được chỉ định trên object đã cho.
   * - ``SIGNAL_CHECK("signal_name", Vector<Vector<Variant>>)``
     - Kiểm tra các đối số của tất cả signal đã được phát. Vector bên ngoài chứa từng signal đã phát, còn vector bên trong chứa danh sách các đối số của signal đó. Thứ tự của các signal có ý nghĩa.
   * - ``SIGNAL_CHECK_FALSE("signal_name")``
     - Kiểm tra xem signal được chỉ định có chưa được phát hay không.
   * - ``SIGNAL_DISCARD("signal_name")``
     - Loại bỏ mọi bản ghi của signal được chỉ định.

Dưới đây là một ví dụ minh họa cách sử dụng các macro này:

.. code-block:: cpp

    //...
    SUBCASE("[Timer] Timer process timeout signal must be emitted") {
        SIGNAL_WATCH(test_timer, SNAME("timeout"));
        test_timer->start(0.1);

        SceneTree::get_singleton()->process(0.2);

        Array signal_args;
        signal_args.push_back(Array());

        SIGNAL_CHECK(SNAME("timeout"), signal_args);

        SIGNAL_UNWATCH(test_timer, SNAME("timeout"));
    }
    //...

Công cụ kiểm thử
----------------

Công cụ kiểm thử là các phương thức nâng cao, cho phép chạy những quy trình tùy ý để hỗ trợ quá trình kiểm thử thủ công và debug nội bộ engine.

Có thể chạy các công cụ này bằng cách cung cấp tên của một công cụ sau tùy chọn dòng lệnh ``--test``. Ví dụ, module GDScript triển khai và đăng ký một số công cụ để hỗ trợ debug tokenizer, parser và compiler:

.. code-block:: shell

    ./bin/<godot_binary> --test gdscript-tokenizer test.gd
    ./bin/<godot_binary> --test gdscript-parser test.gd
    ./bin/<godot_binary> --test gdscript-compiler test.gd

Nếu phát hiện bất kỳ công cụ nào như vậy, phần còn lại của các bài kiểm thử đơn vị sẽ bị bỏ qua.

Có thể đăng ký các công cụ kiểm thử ở bất kỳ đâu trong engine, vì cơ chế đăng ký gần giống với cách doctest cung cấp khi đăng ký test case bằng kỹ thuật dynamic initialization, nhưng thông thường chúng được đăng ký tại các source ``register_types.cpp`` tương ứng (theo module hoặc core).

Dưới đây là ví dụ về cách GDScript đăng ký các công cụ kiểm thử trong ``modules/gdscript/register_types.cpp``:

.. code-block:: cpp

    #ifdef TESTS_ENABLED
    void test_tokenizer() {
        TestGDScript::test(TestGDScript::TestType::TEST_TOKENIZER);
    }

    void test_parser() {
        TestGDScript::test(TestGDScript::TestType::TEST_PARSER);
    }

    void test_compiler() {
        TestGDScript::test(TestGDScript::TestType::TEST_COMPILER);
    }

    REGISTER_TEST_COMMAND("gdscript-tokenizer", &test_tokenizer);
    REGISTER_TEST_COMMAND("gdscript-parser", &test_parser);
    REGISTER_TEST_COMMAND("gdscript-compiler", &test_compiler);
    #endif

Có thể thực hiện việc phân tích cú pháp dòng lệnh tùy chỉnh trong chính công cụ kiểm thử bằng phương thức OS :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>`.

Kiểm thử tích hợp cho GDScript
------------------------------

Godot sử dụng doctest để ngăn hồi quy trong GDScript trong quá trình phát triển. Có một số loại test script có thể được viết:

- các test cho lỗi dự kiến; - các test cho cảnh báo; - các test cho tính năng.

Do đó, quy trình viết integration test cho GDScript như sau:

1. Chọn loại test script bạn muốn viết và tạo một tệp GDScript mới trong thư mục ``modules/gdscript/tests/scripts`` thuộc sub-directory tương ứng.

2. Viết mã GDScript. Test script phải có một function có tên ``test()`` và không nhận đối số. Function này sẽ được test runner gọi. Test không nên có dependency nào, trừ khi dependency đó cũng là một phần của test. Global class (sử dụng ``class_name``) được đăng ký trước khi runner khởi động, vì vậy chúng sẽ hoạt động nếu cần.

   Sau đây là một test script mẫu:

   ::

        func test():
            if true # Thiếu dấu hai chấm ở đây.
                print("true")

3. Chuyển thư mục đến thư mục gốc của repository mã nguồn Godot.

   .. code-block:: shell

       cd godot

4. Tạo các tệp ``*.out`` để cập nhật kết quả dự kiến từ output:

   .. code-block:: shell

       bin/<godot_binary> --gdscript-generate-tests modules/gdscript/tests/scripts

Bạn có thể thêm tùy chọn ``--print-filenames`` để xem tên tệp trong khi output của chúng được tạo. Nếu bạn đang làm việc trên một tính năng mới gây ra lỗi crash nghiêm trọng, bạn có thể sử dụng tùy chọn này để nhanh chóng tìm tệp test nào gây ra lỗi crash và debug từ đó.

5. Chạy các test GDScript bằng:

   .. code-block:: shell

       ./bin/<godot_binary> --test --test-suite="*GDScript*"

Lệnh này cũng chấp nhận tùy chọn ``--print-filenames`` (xem ở trên).

Nếu không có lỗi nào được in ra và mọi thứ diễn ra suôn sẻ thì bạn đã hoàn tất!

.. warning::

    Hãy đảm bảo output có các giá trị dự kiến trước khi gửi pull request. Nếu ``--gdscript-generate-tests`` tạo ra các tệp ``*.out`` không liên quan đến các test mới được thêm, bạn nên hoàn nguyên các tệp đó và chỉ commit các tệp ``*.out`` cho các test mới.

.. note::

    GDScript test runner được dùng để kiểm thử phần triển khai GDScript, không phải để kiểm thử user script hay engine bằng script. Chúng tôi khuyến nghị viết test mới cho các `issue liên quan đến GDScript đã được giải quyết tại GitHub <https://github.com/godotengine/godot/issues?q=is%3Aissue+label%3Atopic%3Agdscript+is%3Aclosed>`_, hoặc viết test cho các tính năng hiện đang hoạt động.

.. note::

    Nếu test case của bạn yêu cầu không có function ``test()`` nào bên trong tệp script, bạn có thể vô hiệu hóa phần runtime của test bằng cách đặt tên tệp script sao cho khớp với pattern ``*.notest.gd``. Ví dụ: "test_empty_file.notest.gd".
