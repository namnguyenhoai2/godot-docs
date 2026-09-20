.. _doc_unit_testing:

Kiểm thử đơn vị
===============

Godot Engine cho phép viết các bài kiểm thử đơn vị trực tiếp bằng C++. Engine tích hợp framework kiểm thử đơn vị `doctest <https://github.com/doctest/doctest>`_ cho phép viết các test suite và test case bên cạnh mã production, nhưng vì các bài kiểm thử trong Godot đi qua một ``main`` entry point khác, nên các bài kiểm thử nằm trong một thư mục ``tests/`` riêng, ở thư mục gốc của mã nguồn engine.

Nền tảng và mục tiêu được hỗ trợ
--------------------------------

Các bài kiểm thử đơn vị C++ có thể chạy trên hệ điều hành Linux, macOS và Windows.

Chỉ có thể chạy các bài kiểm thử khi bật editor ``tools``, điều đó có nghĩa là hiện tại chưa thể kiểm thử các export template.

Chạy các bài kiểm thử
---------------------

Trước khi thực sự chạy các bài kiểm thử, engine phải được biên dịch với build option ``tests`` được bật (cùng với bất kỳ build option nào khác mà bạn thường sử dụng), vì theo mặc định, các bài kiểm thử không được biên dịch cùng engine:

.. code-block:: shell

    scons tests=yes

Sau khi build xong, chạy các bài kiểm thử với command-line option ``--test``:

.. code-block:: shell

    ./bin/<godot_binary> --test

Có thể cấu hình quá trình chạy bài kiểm thử bằng nhiều command-line option dành riêng cho doctest. Để lấy danh sách đầy đủ các option được hỗ trợ, hãy chạy command ``--test`` với option ``--help``:

.. code-block:: shell

    ./bin/<godot_binary> --test --help

Mọi option và đối số khác sau command ``--test`` đều được xem là đối số dành cho doctest.

.. note::

    Các bài kiểm thử được tự động biên dịch nếu bạn sử dụng SCons option ``dev_mode=yes``. ``dev_mode=yes`` được khuyến nghị nếu bạn dự định đóng góp cho quá trình phát triển engine, vì nó sẽ tự động xem các cảnh báo biên dịch là lỗi. Hệ thống continuous integration sẽ thất bại nếu phát hiện bất kỳ cảnh báo biên dịch nào, vì vậy bạn nên cố gắng sửa tất cả cảnh báo trước khi mở pull request.

Lọc các bài kiểm thử
~~~~~~~~~~~~~~~~~~~~

Theo mặc định, tất cả bài kiểm thử sẽ được chạy nếu bạn không cung cấp đối số bổ sung nào sau command ``--test``. Tuy nhiên, nếu đang viết bài kiểm thử mới hoặc muốn xem output của các assertion thành công từ những bài kiểm thử đó để debug, bạn có thể chạy các bài kiểm thử cần thiết bằng nhiều tùy chọn lọc do doctest cung cấp.

Cú pháp wildcard ``*`` được hỗ trợ để khớp với bất kỳ số lượng ký tự nào trong test suite, test case và tên file mã nguồn:

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

Có thể bật output của các assertion thành công bằng option ``--success`` (``-s``), và kết hợp option này với bất kỳ tổ hợp tùy chọn lọc nào ở trên, chẳng hạn:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_color*" --success

Có thể bỏ qua các bài kiểm thử cụ thể bằng các option ``-exclude`` tương ứng. Hiện tại, một số bài kiểm thử bao gồm các bài kiểm thử stress ngẫu nhiên, vốn mất khá nhiều thời gian để thực thi. Để bỏ qua những bài kiểm thử như vậy, hãy chạy command sau:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case-exclude="*[Stress]*"

Viết các bài kiểm thử
---------------------

Test suite đại diện cho các file triển khai C++ phải include macro ``TEST_FORCE_LINK()``. Hầu hết test suite nằm trực tiếp bên dưới thư mục ``tests/``.

Tất cả file kiểm thử đều có tiền tố ``test_``, đây là quy ước đặt tên mà hệ thống build của Godot dựa vào để phát hiện các bài kiểm thử trong toàn bộ engine.

Dưới đây là một test suite tối thiểu có thể hoạt động, với một test case được viết sẵn:

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
    Bạn có thể nhanh chóng tạo các bài kiểm thử mới bằng script ``create_test.py`` nằm trong thư mục ``tests/``. Script này tự động tạo một file kiểm thử mới với mã boilerplate cần thiết tại vị trí phù hợp. Để xem hướng dẫn sử dụng, hãy chạy script với flag ``-h``.

Header ``tests/test_macros.h`` đóng gói mọi thứ cần thiết để viết các bài kiểm thử đơn vị C++ trong Godot. Nó bao gồm các macro assertion và logging của doctest như ``CHECK`` được minh họa ở trên, cũng như tất nhiên là các định nghĩa để viết chính các test case.

.. seealso::

    Mã nguồn `tests/test_macros.h <https://github.com/godotengine/godot/blob/master/tests/test_macros.h>`_ chứa các macro hiện được triển khai và các alias của chúng.

Test case được tạo bằng macro dạng function ``TEST_CASE``. Mỗi test case phải có một mô tả ngắn được viết trong dấu ngoặc đơn, tùy chọn bao gồm các tag tùy chỉnh cho phép lọc bài kiểm thử tại runtime, chẳng hạn như ``[String]``, ``[Stress]`` v.v.

Test case được viết trong một namespace riêng. Điều này không bắt buộc, nhưng giúp tránh xung đột tên khi viết các static helper function khác để hỗ trợ các quy trình kiểm thử lặp lại, chẳng hạn như nạp dữ liệu kiểm thử chung cho mỗi bài kiểm thử hoặc viết các bài kiểm thử có tham số.

Godot hỗ trợ viết bài kiểm thử theo từng C++ module. Để biết hướng dẫn viết bài kiểm thử cho module, hãy tham khảo :ref:`doc_custom_module_unit_tests`.

Subcase
~~~~~~~

Trong những tình huống bạn có phần thiết lập chung cho nhiều test case nhưng chỉ khác nhau đôi chút, subcase có thể rất hữu ích. Dưới đây là một ví dụ:

.. code-block:: cpp

    TEST_CASE("[SceneTree][Node] Testing node operations with a very simple scene tree") {
        // ... common setup (e.g. creating a scene tree with a few nodes)
        SUBCASE("Move node to specific index") {
            // ... setup and checks for moving a node
        }
        SUBCASE("Remove node at specific index") {
            // ... setup and checks for removing a node
        }
    }

Mỗi ``SUBCASE`` khiến ``TEST_CASE`` được thực thi lại từ đầu. Có thể lồng các subcase đến độ sâu tùy ý, nhưng nên giới hạn việc lồng nhau ở không quá một cấp.

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

Tất cả assertion ở trên đều có các macro ``*_MESSAGE`` tương ứng, cho phép in thông báo tùy chọn giải thích lý do điều gì đó được mong đợi sẽ xảy ra.

Ưu tiên sử dụng ``CHECK`` cho các assertion có ý nghĩa rõ ràng và ``CHECK_MESSAGE`` cho những assertion phức tạp hơn nếu bạn cho rằng chúng cần được giải thích đầy đủ hơn.

.. seealso::

    `doctest: Assertion macros <https://github.com/doctest/doctest/blob/master/doc/markdown/assertions.md>`_.

Logging
~~~~~~~

Output của bài kiểm thử do chính doctest xử lý và hoàn toàn không phụ thuộc vào chức năng in hoặc logging của Godot, vì vậy nên sử dụng các macro chuyên dụng cho phép ghi output kiểm thử theo định dạng do doctest tạo ra.

+----------------+-----------------------------------------------------------------------------------------------------------+
| **Macro**      | **Description**                                                                                           |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``MESSAGE``    | Prints a message.                                                                                         |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``FAIL_CHECK`` | Marks the test as failing, but continue the execution. Can be wrapped in conditionals for complex checks. |
+----------------+-----------------------------------------------------------------------------------------------------------+
| ``FAIL``       | Fails the test immediately. Can be wrapped in conditionals for complex checks.                            |
+----------------+-----------------------------------------------------------------------------------------------------------+

Có thể chọn các reporter khác nhau tại runtime. Ví dụ, dưới đây là cách chuyển hướng output vào một file XML:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_validate*" --success --reporters=xml --out=doctest.txt

.. seealso::

    `doctest: Logging macros <https://github.com/doctest/doctest/blob/master/doc/markdown/logging.md>`_.

Kiểm thử các nhánh lỗi
~~~~~~~~~~~~~~~~~~~~~~

Đôi khi không phải lúc nào cũng khả thi để kiểm thử một kết quả *dự kiến*. Theo triết lý phát triển của Godot, engine không nên crash và nên phục hồi một cách linh hoạt bất cứ khi nào xảy ra lỗi không nghiêm trọng, nên việc kiểm tra rằng các nhánh lỗi đó thực sự an toàn để thực thi mà không làm engine crash là rất quan trọng.

Hành vi *không mong đợi* có thể được kiểm thử theo cách tương tự như mọi thứ khác. Vấn đề duy nhất là việc này khiến output kiểm thử bị làm nhiễu không cần thiết bởi các lỗi do chính engine in ra (ngay cả khi kết quả cuối cùng là thành công).

Để khắc phục vấn đề này, hãy sử dụng trực tiếp các macro ``ERR_PRINT_OFF`` và ``ERR_PRINT_ON`` bên trong test case để tạm thời vô hiệu hóa output lỗi từ engine, chẳng hạn:

.. code-block:: cpp

    TEST_CASE("[Color] Constructor methods") {
        ERR_PRINT_OFF;
        Color html_invalid = Color::html("invalid");
        ERR_PRINT_ON; // Don't forget to re-enable!

        CHECK_MESSAGE(html_invalid.is_equal_approx(Color()),
            "Invalid HTML notation should result in a Color with the default values.");
    }

Tag đặc biệt trong tên test case
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể thêm các tag này vào tên test case để thay đổi hoặc mở rộng môi trường kiểm thử:

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
     - Kiểm tra các đối số của tất cả signal đã phát. Vector bên ngoài chứa từng signal đã phát, còn vector bên trong chứa danh sách đối số của signal đó. Thứ tự của các signal rất quan trọng.
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

Công cụ kiểm thử là các phương thức nâng cao cho phép bạn chạy những quy trình tùy ý nhằm hỗ trợ quá trình kiểm thử thủ công và debug các phần bên trong engine.

Có thể chạy các công cụ này bằng cách cung cấp tên của một công cụ sau command-line option ``--test``. Ví dụ, GDScript module triển khai và đăng ký một số công cụ để hỗ trợ debug tokenizer, parser và compiler:

.. code-block:: shell

    ./bin/<godot_binary> --test gdscript-tokenizer test.gd
    ./bin/<godot_binary> --test gdscript-parser test.gd
    ./bin/<godot_binary> --test gdscript-compiler test.gd

Nếu phát hiện bất kỳ công cụ nào như vậy, các bài kiểm thử đơn vị còn lại sẽ được bỏ qua.

Có thể đăng ký công cụ kiểm thử ở bất kỳ đâu trong engine, vì cơ chế đăng ký gần giống với cách doctest cung cấp khi đăng ký test case bằng kỹ thuật dynamic initialization, nhưng thông thường chúng được đăng ký tại các source ``register_types.cpp`` tương ứng (theo module hoặc core).

Dưới đây là một ví dụ về cách GDScript đăng ký các công cụ kiểm thử trong ``modules/gdscript/register_types.cpp``:

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

Có thể thực hiện việc phân tích command-line tùy chỉnh bởi chính công cụ kiểm thử với sự trợ giúp của phương thức OS :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>`.

Kiểm thử tích hợp cho GDScript
------------------------------

Godot sử dụng doctest để ngăn hồi quy trong GDScript trong quá trình phát triển. Có thể viết một số loại test script:

- các bài kiểm thử cho lỗi dự kiến; - các bài kiểm thử cho warning; - các bài kiểm thử cho feature.

Do đó, quy trình viết các bài kiểm thử tích hợp cho GDScript như sau:

1. Chọn loại test script mà bạn muốn viết, rồi tạo một tệp GDScript mới trong thư mục ``modules/gdscript/tests/scripts`` thuộc thư mục con tương ứng.

2. Viết mã GDScript. Test script phải có một hàm tên là ``test()`` và không nhận tham số nào. Hàm này sẽ được test runner gọi. Test không được có dependency nào, trừ khi dependency đó cũng là một phần của test. Các global class (sử dụng ``class_name``) được đăng ký trước khi runner khởi động, vì vậy bạn có thể sử dụng chúng nếu cần.

   Sau đây là một test script mẫu:

   ::

        func test():
            if true # Missing colon here.
                print("true")

3. Chuyển thư mục đến thư mục gốc của repository mã nguồn Godot.

   .. code-block:: shell

       cd godot

4. Tạo các tệp ``*.out`` để cập nhật kết quả mong đợi từ output:

   .. code-block:: shell

       bin/<godot_binary> --gdscript-generate-tests modules/gdscript/tests/scripts

Bạn có thể thêm tùy chọn ``--print-filenames`` để xem tên tệp khi output của test được tạo. Nếu bạn đang làm việc trên một tính năng mới gây ra lỗi crash nghiêm trọng, bạn có thể dùng tùy chọn này để nhanh chóng tìm tệp test gây ra lỗi crash và debug từ đó.

5. Chạy các test GDScript bằng lệnh:

   .. code-block:: shell

       ./bin/<godot_binary> --test --test-suite="*GDScript*"

Lệnh này cũng chấp nhận tùy chọn ``--print-filenames`` (xem ở trên).

Nếu không có lỗi nào được in ra và mọi thứ diễn ra suôn sẻ thì bạn đã hoàn tất!

.. warning::

    Hãy đảm bảo output có đúng các giá trị mong đợi trước khi gửi pull request. Nếu ``--gdscript-generate-tests`` tạo ra các tệp ``*.out`` không liên quan đến những test mới được thêm, bạn nên hoàn nguyên các tệp đó và chỉ commit các tệp ``*.out`` dành cho test mới.

.. note::

    GDScript test runner được dùng để kiểm thử phần triển khai GDScript, không phải để kiểm thử user script hoặc kiểm thử engine bằng script. Chúng tôi khuyến nghị viết test mới cho các `issue liên quan đến GDScript đã được giải quyết tại GitHub <https://github.com/godotengine/godot/issues?q=is%3Aissue+label%3Atopic%3Agdscript+is%3Aclosed>`_, hoặc viết test cho các tính năng hiện đang hoạt động.

.. note::

    Nếu test case của bạn yêu cầu không có hàm ``test()`` bên trong tệp script, bạn có thể vô hiệu hóa phần runtime của test bằng cách đặt tên tệp script sao cho khớp với mẫu ``*.notest.gd``. Ví dụ: "test_empty_file.notest.gd".
