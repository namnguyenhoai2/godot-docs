.. _doc_unit_testing:

Kiểm thử đơn vị
===============

Godot Engine cho phép viết các kiểm thử đơn vị trực tiếp bằng C++. Engine tích hợp framework kiểm thử đơn vị `doctest <https://github.com/doctest/doctest>`_, cho phép viết các bộ kiểm thử và trường hợp kiểm thử ngay bên cạnh mã production, nhưng vì các kiểm thử trong Godot đi qua một ``main`` entry point khác, nên các kiểm thử nằm trong thư mục ``tests/`` chuyên dụng, ở thư mục gốc của mã nguồn engine.

Hỗ trợ nền tảng và mục tiêu
---------------------------

Các kiểm thử đơn vị C++ có thể chạy trên hệ điều hành Linux, macOS và Windows.

Chỉ có thể chạy kiểm thử khi bật ``tools`` của editor, nghĩa là hiện tại chưa thể kiểm thử các export template.

Chạy kiểm thử
-------------

Trước khi thực sự chạy kiểm thử, engine phải được biên dịch với tùy chọn build ``tests`` được bật (cùng mọi tùy chọn build khác mà bạn thường sử dụng), vì theo mặc định, các kiểm thử không được biên dịch cùng engine:

.. code-block:: shell

    scons tests=yes

Sau khi build xong, chạy kiểm thử bằng tùy chọn dòng lệnh ``--test``:

.. code-block:: shell

    ./bin/<godot_binary> --test

Có thể cấu hình lần chạy kiểm thử bằng nhiều tùy chọn dòng lệnh dành riêng cho doctest. Để lấy danh sách đầy đủ các tùy chọn được hỗ trợ, chạy lệnh ``--test`` với tùy chọn ``--help``:

.. code-block:: shell

    ./bin/<godot_binary> --test --help

Mọi tùy chọn và đối số khác sau lệnh ``--test`` được xử lý như các đối số dành cho doctest.

.. note::

    Các kiểm thử được tự động biên dịch nếu bạn sử dụng tùy chọn SCons ``dev_mode=yes``. Khuyến nghị dùng ``dev_mode=yes`` nếu bạn dự định đóng góp cho quá trình phát triển engine, vì tùy chọn này sẽ tự động xem các cảnh báo biên dịch là lỗi. Hệ thống continuous integration sẽ thất bại nếu phát hiện bất kỳ cảnh báo biên dịch nào, vì vậy bạn nên cố gắng sửa tất cả cảnh báo trước khi mở pull request.

Lọc kiểm thử
~~~~~~~~~~~~

Theo mặc định, tất cả kiểm thử sẽ được chạy nếu bạn không cung cấp thêm đối số nào sau lệnh ``--test``. Tuy nhiên, nếu đang viết kiểm thử mới hoặc muốn xem đầu ra của các assertion thành công từ những kiểm thử đó để debug, bạn có thể chạy các kiểm thử cần quan tâm bằng nhiều tùy chọn lọc do doctest cung cấp.

Cú pháp wildcard ``*`` được hỗ trợ để khớp với mọi số lượng ký tự trong tên bộ kiểm thử, trường hợp kiểm thử và tệp mã nguồn:

+-------------------+--------------+------------------------+
| **Tùy chọn lọc**  | **Viết tắt** | **Ví dụ**              |
+-------------------+--------------+------------------------+
| ``--test-suite``  | ``-ts``      | ``-ts="*[GDScript]*"`` |
+-------------------+--------------+------------------------+
| ``--test-case``   | ``-tc``      | ``-tc="*[String]*"``   |
+-------------------+--------------+------------------------+
| ``--source-file`` | ``-sf``      | ``-sf="*test_color*"`` |
+-------------------+--------------+------------------------+

Ví dụ, để chỉ chạy các kiểm thử đơn vị ``String``, hãy chạy:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case="*[String]*"

Có thể bật đầu ra của các assertion thành công bằng tùy chọn ``--success`` (``-s``), và kết hợp tùy chọn này với bất kỳ tổ hợp tùy chọn lọc nào ở trên, chẳng hạn:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_color*" --success

Có thể bỏ qua các kiểm thử cụ thể bằng các tùy chọn ``-exclude`` tương ứng. Hiện tại, một số kiểm thử bao gồm các bài kiểm thử stress ngẫu nhiên mất khá nhiều thời gian để thực thi. Để bỏ qua các loại kiểm thử đó, hãy chạy lệnh sau:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case-exclude="*[Stress]*"

Viết kiểm thử
-------------

Các bộ kiểm thử tương ứng với các tệp triển khai C++ phải bao gồm macro ``TEST_FORCE_LINK()``. Hầu hết các bộ kiểm thử nằm trực tiếp trong thư mục ``tests/``.

Tất cả tệp kiểm thử đều có tiền tố ``test_``, đây là quy ước đặt tên mà hệ thống build của Godot dựa vào để phát hiện các kiểm thử trong toàn engine.

Dưới đây là một bộ kiểm thử tối thiểu có thể hoạt động, với một trường hợp kiểm thử duy nhất:

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
    Bạn có thể nhanh chóng tạo các kiểm thử mới bằng script ``create_test.py`` trong thư mục ``tests/``. Script này tự động tạo một tệp kiểm thử mới với mã boilerplate bắt buộc tại vị trí phù hợp. Để xem hướng dẫn sử dụng, hãy chạy script với flag ``-h``.

Header ``tests/test_macros.h`` đóng gói mọi thứ cần thiết để viết kiểm thử đơn vị C++ trong Godot. Header này bao gồm các macro assertion và logging của doctest, chẳng hạn như ``CHECK`` như ở trên, cùng các định nghĩa để viết chính các trường hợp kiểm thử.

.. seealso::

    Mã nguồn `tests/test_macros.h <https://github.com/godotengine/godot/blob/master/tests/test_macros.h>`_ cho các macro hiện đã được triển khai và các bí danh của chúng.

Các trường hợp kiểm thử được tạo bằng macro dạng hàm ``TEST_CASE``. Mỗi trường hợp kiểm thử phải có một mô tả ngắn được viết trong dấu ngoặc đơn, có thể tùy chọn kèm các tag tùy chỉnh cho phép lọc kiểm thử khi runtime, chẳng hạn như ``[String]``, ``[Stress]``, v.v.

Các trường hợp kiểm thử được viết trong một namespace chuyên dụng. Điều này không bắt buộc, nhưng giúp tránh xung đột tên khi viết các hàm helper static khác để hỗ trợ những quy trình kiểm thử lặp lại, chẳng hạn như tạo dữ liệu kiểm thử chung cho từng kiểm thử hoặc viết các kiểm thử có tham số.

Godot hỗ trợ viết kiểm thử theo từng module C++. Để biết hướng dẫn viết kiểm thử cho module, hãy xem :ref:`doc_custom_module_unit_tests`.

Subcase
~~~~~~~

Trong những tình huống có phần setup chung cho nhiều trường hợp kiểm thử chỉ khác nhau đôi chút, subcase có thể rất hữu ích. Dưới đây là một ví dụ:

.. code-block:: cpp

    TEST_CASE("[SceneTree][Node] Testing node operations with a very simple scene tree") {
        // ... setup chung (ví dụ: tạo một scene tree với vài node)
        SUBCASE("Move node to specific index") {
            // ... setup và kiểm tra việc di chuyển một node
        }
        SUBCASE("Remove node at specific index") {
            // ... setup và kiểm tra việc xóa một node
        }
    }

Mỗi ``SUBCASE`` khiến ``TEST_CASE`` được thực thi lại từ đầu. Có thể lồng các subcase đến độ sâu tùy ý, nhưng nên giới hạn việc lồng tối đa ở một cấp.

Assertions
~~~~~~~~~~

Danh sách tất cả các assertion thường được sử dụng trong các kiểm thử Godot, được sắp xếp theo mức độ nghiêm trọng.

+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| **Assertion**     | **Mô tả**                                                                                                                               |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``REQUIRE``       | Kiểm tra điều kiện có đúng hay không. Lập tức làm toàn bộ kiểm thử thất bại nếu điều kiện không đúng.                                   |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``REQUIRE_FALSE`` | Kiểm tra điều kiện không đúng. Lập tức làm toàn bộ kiểm thử thất bại nếu điều kiện đúng.                                                |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``CHECK``         | Kiểm tra điều kiện có đúng hay không. Đánh dấu lần chạy kiểm thử là thất bại, nhưng vẫn cho phép chạy các assertion khác.               |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``CHECK_FALSE``   | Kiểm tra điều kiện không đúng. Đánh dấu lần chạy kiểm thử là thất bại, nhưng vẫn cho phép chạy các assertion khác.                      |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``WARN``          | Kiểm tra xem điều kiện có đúng hay không. Không bao giờ làm bài kiểm tra thất bại, nhưng ghi nhật ký cảnh báo nếu điều kiện không đúng. |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| ``WARN_FALSE``    | Kiểm tra xem điều kiện có không đúng hay không. Không bao giờ làm bài kiểm tra thất bại, nhưng ghi nhật ký cảnh báo nếu điều kiện đúng. |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

Tất cả các assertion trên đều có các macro ``*_MESSAGE`` tương ứng, cho phép in thông báo tùy chọn giải thích điều gì nên xảy ra.

Ưu tiên sử dụng ``CHECK`` cho các assertion có nội dung tự giải thích và ``CHECK_MESSAGE`` cho những assertion phức tạp hơn nếu bạn cho rằng chúng cần được giải thích rõ hơn.

.. seealso::

    `doctest: Các macro assertion <https://github.com/doctest/doctest/blob/master/doc/markdown/assertions.md>`_.

Ghi nhật ký
~~~~~~~~~~~

Đầu ra của bài kiểm tra do chính doctest xử lý và hoàn toàn không phụ thuộc vào chức năng in hoặc ghi nhật ký của Godot, vì vậy bạn nên sử dụng các macro chuyên dụng cho phép ghi đầu ra của bài kiểm tra theo định dạng do doctest tạo ra.

+----------------+---------------------------------------------------------------------------------------------------------------------------------+
| **Macro**      | **Mô tả**                                                                                                                       |
+----------------+---------------------------------------------------------------------------------------------------------------------------------+
| ``MESSAGE``    | In một thông báo.                                                                                                               |
+----------------+---------------------------------------------------------------------------------------------------------------------------------+
| ``FAIL_CHECK`` | Đánh dấu bài kiểm tra là thất bại nhưng tiếp tục thực thi. Có thể đặt trong các điều kiện để thực hiện những kiểm tra phức tạp. |
+----------------+---------------------------------------------------------------------------------------------------------------------------------+
| ``FAIL``       | Làm bài kiểm tra thất bại ngay lập tức. Có thể đặt trong các điều kiện để thực hiện những kiểm tra phức tạp.                    |
+----------------+---------------------------------------------------------------------------------------------------------------------------------+

Có thể chọn các reporter khác nhau trong runtime. Ví dụ: sau đây là cách chuyển hướng đầu ra vào một tệp XML:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_validate*" --success --reporters=xml --out=doctest.txt

.. seealso::

    `doctest: Các macro ghi nhật ký <https://github.com/doctest/doctest/blob/master/doc/markdown/logging.md>`_.

Kiểm tra các đường dẫn thất bại
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đôi khi không phải lúc nào cũng khả thi để kiểm tra một kết quả *dự kiến*. Theo triết lý phát triển của Godot, engine không nên bị crash và phải phục hồi một cách an toàn mỗi khi xảy ra lỗi không nghiêm trọng, vì vậy điều quan trọng là phải kiểm tra rằng các đường dẫn thất bại đó thực sự an toàn để thực thi mà không làm engine bị crash.

Hành vi *không mong muốn* có thể được kiểm tra giống như mọi thứ khác. Vấn đề duy nhất là việc in lỗi sẽ khiến đầu ra của bài kiểm tra bị làm nhiễu không cần thiết bởi các lỗi do chính engine tạo ra, ngay cả khi kết quả cuối cùng là thành công.

Để giảm vấn đề này, hãy sử dụng trực tiếp các macro ``ERR_PRINT_OFF`` và ``ERR_PRINT_ON`` bên trong các test case để tạm thời vô hiệu hóa đầu ra lỗi từ engine, ví dụ:

.. code-block:: cpp

    TEST_CASE("[Color] Constructor methods") {
        ERR_PRINT_OFF;
        Color html_invalid = Color::html("invalid");
        ERR_PRINT_ON; // Đừng quên bật lại!

        CHECK_MESSAGE(html_invalid.is_equal_approx(Color()),
            "Invalid HTML notation should result in a Color with the default values.");
    }

Các tag đặc biệt trong tên test case
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể thêm các tag này vào tên test case để sửa đổi hoặc mở rộng môi trường kiểm thử:

+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Tag**            | **Mô tả**                                                                                                                                                     |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[SceneTree]``    | Bắt buộc đối với các test case phụ thuộc vào scene tree có MessageQueue. Tùy chọn này cũng bật một rendering server giả lập và :ref:`ThemeDB<class_ThemeDB>`. |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Editor]``       | Tương tự như ``[SceneTree]``, nhưng có thêm cơ sở hạ tầng liên quan đến editor, chẳng hạn như :ref:`EditorSettings<class_EditorSettings>`.                    |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Audio]``        | Khởi tạo :ref:`AudioServer<class_AudioServer>` bằng audio driver giả lập.                                                                                     |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Navigation2D]`` | Tạo navigation server 2D mặc định và cung cấp nó cho việc kiểm thử.                                                                                           |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``[Navigation3D]`` | Tạo navigation server 3D mặc định và cung cấp nó cho việc kiểm thử.                                                                                           |
+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

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
     - Bắt đầu theo dõi signal được chỉ định trên đối tượng đã cho.
   * - ``SIGNAL_UNWATCH(object, "signal_name")``
     - Dừng theo dõi signal được chỉ định trên đối tượng đã cho.
   * - ``SIGNAL_CHECK("signal_name", Vector<Vector<Variant>>)``
     - Kiểm tra các đối số của tất cả signal đã phát. Vector bên ngoài chứa từng signal đã phát, còn vector bên trong chứa danh sách đối số của signal đó. Thứ tự của các signal rất quan trọng.
   * - ``SIGNAL_CHECK_FALSE("signal_name")``
     - Kiểm tra xem signal được chỉ định có chưa được phát hay không.
   * - ``SIGNAL_DISCARD("signal_name")``
     - Loại bỏ mọi bản ghi của signal được chỉ định.

Dưới đây là ví dụ minh họa cách sử dụng các macro này:

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

Công cụ kiểm thử là các phương thức nâng cao cho phép bạn chạy những quy trình tùy ý để hỗ trợ quá trình kiểm thử thủ công và gỡ lỗi các thành phần bên trong engine.

Có thể chạy các công cụ này bằng cách cung cấp tên của một công cụ sau tùy chọn dòng lệnh ``--test``. Ví dụ: module GDScript triển khai và đăng ký một số công cụ để hỗ trợ gỡ lỗi tokenizer, parser và compiler:

.. code-block:: shell

    ./bin/<godot_binary> --test gdscript-tokenizer test.gd
    ./bin/<godot_binary> --test gdscript-parser test.gd
    ./bin/<godot_binary> --test gdscript-compiler test.gd

Nếu phát hiện bất kỳ công cụ nào như vậy, các unit test còn lại sẽ được bỏ qua.

Có thể đăng ký công cụ kiểm thử ở bất kỳ đâu trong engine, vì cơ chế đăng ký gần giống với cơ chế doctest cung cấp khi đăng ký test case bằng kỹ thuật khởi tạo động, nhưng thông thường các công cụ này có thể được đăng ký tại các source ``register_types.cpp`` tương ứng (theo module hoặc core).

Sau đây là ví dụ về cách GDScript đăng ký các công cụ kiểm thử trong ``modules/gdscript/register_types.cpp``:

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

Bản thân công cụ kiểm thử có thể thực hiện việc phân tích cú pháp dòng lệnh tùy chỉnh với sự trợ giúp của phương thức :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>` của OS.

Integration test cho GDScript
-----------------------------

Godot sử dụng doctest để ngăn ngừa hồi quy trong GDScript trong quá trình phát triển. Có thể viết một số loại test script sau:

- test cho các lỗi dự kiến;
- test cho các cảnh báo;
- test cho các tính năng.

Do đó, quy trình viết integration test cho GDScript như sau:

1. Chọn loại tập lệnh kiểm thử bạn muốn viết và tạo một tệp GDScript mới trong thư mục ``modules/gdscript/tests/scripts`` thuộc thư mục con tương ứng.

2. Viết mã GDScript. Tập lệnh kiểm thử phải có một hàm tên là ``test()`` không nhận đối số nào. Hàm này sẽ được test runner gọi. Bài kiểm thử không nên có dependency nào, trừ khi dependency đó cũng là một phần của bài kiểm thử. Các global class (sử dụng ``class_name``) được đăng ký trước khi runner khởi động, vì vậy chúng sẽ hoạt động nếu cần.

   Sau đây là một tập lệnh kiểm thử mẫu:

   ::

        func test():
            if true # Missing colon here.
                print("true")

3. Chuyển thư mục đến thư mục gốc của repository mã nguồn Godot.

   .. code-block:: shell

       cd godot

4. Tạo các tệp ``*.out`` để cập nhật kết quả mong đợi từ đầu ra:

   .. code-block:: shell

       bin/<godot_binary> --gdscript-generate-tests modules/gdscript/tests/scripts

Bạn có thể thêm tùy chọn ``--print-filenames`` để xem tên tệp trong khi đầu ra của các bài kiểm thử được tạo. Nếu bạn đang làm việc trên một tính năng mới gây ra lỗi crash nghiêm trọng, bạn có thể sử dụng tùy chọn này để nhanh chóng tìm tệp kiểm thử gây ra lỗi crash và gỡ lỗi từ đó.

5. Chạy các bài kiểm thử GDScript bằng:

   .. code-block:: shell

       ./bin/<godot_binary> --test --test-suite="*GDScript*"

Lệnh này cũng chấp nhận tùy chọn ``--print-filenames`` (xem ở trên).

Nếu không có lỗi nào được in ra và mọi việc diễn ra suôn sẻ thì bạn đã hoàn tất!

.. warning::

    Hãy đảm bảo đầu ra có các giá trị mong đợi trước khi gửi pull request. Nếu ``--gdscript-generate-tests`` tạo ra các tệp ``*.out`` không liên quan đến các bài kiểm thử mới được thêm, bạn nên khôi phục các tệp đó và chỉ commit các tệp ``*.out`` cho các bài kiểm thử mới.

.. note::

    GDScript test runner được dùng để kiểm thử phần triển khai GDScript, không phải để kiểm thử user script hoặc kiểm thử engine bằng script. Chúng tôi khuyến nghị viết các bài kiểm thử mới cho những `issue liên quan đến GDScript đã được giải quyết tại GitHub <https://github.com/godotengine/godot/issues?q=is%3Aissue+label%3Atopic%3Agdscript+is%3Aclosed>`_, hoặc viết các bài kiểm thử cho những tính năng hiện đang hoạt động.

.. note::

    Nếu trường hợp kiểm thử của bạn yêu cầu không có hàm ``test()`` nào bên trong tệp script, bạn có thể vô hiệu hóa phần runtime của bài kiểm thử bằng cách đặt tên tệp script sao cho khớp với mẫu ``*.notest.gd``. Ví dụ: "test_empty_file.notest.gd".

.. _`doctest`: https://github.com/doctest/doctest
.. _`tests/test_macros.h`: https://github.com/godotengine/godot/blob/master/tests/test_macros.h
.. _`doctest: Assertion macros`: https://github.com/doctest/doctest/blob/master/doc/markdown/assertions.md
.. _`doctest: Logging macros`: https://github.com/doctest/doctest/blob/master/doc/markdown/logging.md
.. _`issues related to GDScript at GitHub`: https://github.com/godotengine/godot/issues?q=is%3Aissue+label%3Atopic%3Agdscript+is%3Aclosed
