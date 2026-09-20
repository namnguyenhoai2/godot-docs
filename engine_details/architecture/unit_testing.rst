.. _doc_unit_testing:

Kiểm thử đơn vị
===============

Godot Engine cho phép viết các bài kiểm thử đơn vị trực tiếp bằng C++. Engine tích hợp framework kiểm thử đơn vị `doctest <https://github.com/doctest/doctest>`_ cho phép viết các bộ kiểm thử và trường hợp kiểm thử bên cạnh mã sản phẩm, nhưng vì các bài kiểm thử trong Godot đi qua một điểm vào ``main`` khác, các bài kiểm thử nằm trong một thư mục ``tests/`` riêng biệt, thay vào đó được đặt tại thư mục gốc của mã nguồn engine.

Hỗ trợ nền tảng và mục tiêu
---------------------------

Các bài kiểm thử đơn vị C++ có thể chạy trên hệ điều hành Linux, macOS và Windows.

Chỉ có thể chạy các bài kiểm thử khi bật ``tools`` của editor, nghĩa là hiện tại không thể kiểm thử các export template.

Chạy các bài kiểm thử
---------------------

Trước khi có thể thực sự chạy các bài kiểm thử, engine phải được biên dịch với tùy chọn build ``tests`` được bật (cùng với mọi tùy chọn build khác mà bạn thường sử dụng), vì các bài kiểm thử không được biên dịch cùng engine theo mặc định:

.. code-block:: shell

    scons tests=yes

Sau khi build hoàn tất, hãy chạy các bài kiểm thử bằng tùy chọn dòng lệnh ``--test``:

.. code-block:: shell

    ./bin/<godot_binary> --test

Có thể cấu hình lần chạy bài kiểm thử bằng nhiều tùy chọn dòng lệnh dành riêng cho doctest. Để lấy danh sách đầy đủ các tùy chọn được hỗ trợ, hãy chạy lệnh ``--test`` với tùy chọn ``--help``:

.. code-block:: shell

    ./bin/<godot_binary> --test --help

Mọi tùy chọn và đối số khác sau lệnh ``--test`` đều được coi là đối số dành cho doctest.

.. note::

    Các bài kiểm thử được tự động biên dịch nếu bạn sử dụng tùy chọn SCons ``dev_mode=yes``. Khuyến nghị sử dụng ``dev_mode=yes`` nếu bạn dự định đóng góp cho quá trình phát triển engine, vì tùy chọn này sẽ tự động coi các cảnh báo biên dịch là lỗi. Hệ thống tích hợp liên tục sẽ thất bại nếu phát hiện bất kỳ cảnh báo biên dịch nào, vì vậy bạn nên cố gắng khắc phục tất cả cảnh báo trước khi mở một pull request.

Lọc các bài kiểm thử
~~~~~~~~~~~~~~~~~~~~

Theo mặc định, tất cả bài kiểm thử sẽ được chạy nếu bạn không cung cấp thêm đối số nào sau lệnh ``--test``. Tuy nhiên, nếu đang viết các bài kiểm thử mới hoặc muốn xem đầu ra của các assertion thành công từ những bài kiểm thử đó để gỡ lỗi, bạn có thể chạy các bài kiểm thử mong muốn bằng nhiều tùy chọn lọc do doctest cung cấp.

Cú pháp ký tự đại diện ``*`` được hỗ trợ để khớp với mọi số lượng ký tự trong các bộ kiểm thử, trường hợp kiểm thử và tên tệp mã nguồn:

+--------------------+---------------+------------------------+
| **Tùy chọn lọc** | **Viết tắt** | **Ví dụ** |
+++++++++++++++++++++++++++++++++++++++++++++++
| ``--test-suite`` | ``-ts`` | ``-ts="*[GDScript]*"`` |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``--test-case`` | ``-tc`` | ``-tc="*[String]*"`` |
++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``--source-file`` | ``-sf`` | ``-sf="*test_color*"`` |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Ví dụ, để chỉ chạy các bài kiểm thử đơn vị ``String``, hãy chạy:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case="*[String]*"

Có thể bật đầu ra của các assertion thành công bằng tùy chọn ``--success`` (``-s``), và có thể kết hợp tùy chọn này với bất kỳ tổ hợp tùy chọn lọc nào ở trên, chẳng hạn như:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_color*" --success

Có thể bỏ qua các bài kiểm thử cụ thể bằng các tùy chọn ``-exclude`` tương ứng. Hiện tại, một số bài kiểm thử bao gồm các bài kiểm thử stress ngẫu nhiên mất khá nhiều thời gian để thực thi. Để bỏ qua những loại bài kiểm thử này, hãy chạy lệnh sau:

.. code-block:: shell

    ./bin/<godot_binary> --test --test-case-exclude="*[Stress]*"

Viết các bài kiểm thử
---------------------

Các bộ kiểm thử đại diện cho các tệp triển khai C++ phải bao gồm macro ``TEST_FORCE_LINK()``. Hầu hết các bộ kiểm thử nằm ngay bên dưới thư mục ``tests/``.

Tất cả tệp kiểm thử đều có tiền tố ``test_``, và đây là quy ước đặt tên mà hệ thống build Godot dựa vào để phát hiện các bài kiểm thử trên toàn engine.

Dưới đây là một bộ kiểm thử hoạt động tối thiểu được viết với một trường hợp kiểm thử duy nhất:

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
    Bạn có thể nhanh chóng tạo các bài kiểm thử mới bằng script ``create_test.py`` nằm trong thư mục ``tests/``. Script này tự động tạo một tệp kiểm thử mới với mã boilerplate bắt buộc tại vị trí thích hợp. Để xem hướng dẫn sử dụng, hãy chạy script với cờ ``-h``.

Header ``tests/test_macros.h`` đóng gói mọi thứ cần thiết để viết các bài kiểm thử đơn vị C++ trong Godot. Nó bao gồm các macro assertion và logging của doctest như ``CHECK`` đã thấy ở trên, và tất nhiên cả các định nghĩa để viết chính các trường hợp kiểm thử.

.. seealso::

    Mã nguồn `tests/test_macros.h <https://github.com/godotengine/godot/blob/master/tests/test_macros.h>`_ của các macro hiện được triển khai và các alias của chúng.

Các trường hợp kiểm thử được tạo bằng macro dạng hàm ``TEST_CASE``. Mỗi trường hợp kiểm thử phải có một mô tả ngắn được viết trong dấu ngoặc đơn, tùy chọn bao gồm các tag tùy chỉnh cho phép lọc bài kiểm thử trong thời gian chạy, chẳng hạn như ``[String]``, ``[Stress]`` v.v.

Các trường hợp kiểm thử được viết trong một namespace riêng. Điều này không bắt buộc, nhưng giúp ngăn xung đột tên khi các hàm helper tĩnh khác được viết để hỗ trợ những quy trình kiểm thử lặp lại, chẳng hạn như điền dữ liệu kiểm thử chung cho mỗi bài kiểm thử hoặc viết các bài kiểm thử có tham số.

Godot hỗ trợ viết các bài kiểm thử theo từng module C++. Để xem hướng dẫn viết các bài kiểm thử module, hãy tham khảo :ref:`doc_custom_module_unit_tests`.

Các nhánh con
~~~~~~~~~~~~~

Trong những tình huống bạn có phần thiết lập chung cho nhiều trường hợp kiểm thử với chỉ một vài khác biệt nhỏ, các nhánh con có thể rất hữu ích. Dưới đây là một ví dụ:

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

Mỗi ``SUBCASE`` khiến ``TEST_CASE`` được thực thi lại từ đầu. Các nhánh con có thể được lồng ở độ sâu tùy ý, nhưng nên giới hạn việc lồng không quá một cấp.

Các assertion
~~~~~~~~~~~~~

Danh sách tất cả assertion thường được sử dụng trong các bài kiểm thử Godot, được sắp xếp theo mức độ nghiêm trọng.

+-------------------+----------------------------------------------------------------------------------------------------------------------------------+
| **Assertion** | **Mô tả** |
+++++++++++++++++++++++++++++
| ``REQUIRE`` | Kiểm tra điều kiện là đúng. Ngay lập tức làm thất bại toàn bộ bài kiểm thử nếu điều kiện không đúng. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``REQUIRE_FALSE`` | Kiểm tra điều kiện không đúng. Ngay lập tức làm thất bại toàn bộ bài kiểm thử nếu điều kiện đúng. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``CHECK`` | Kiểm tra điều kiện là đúng. Đánh dấu lần chạy bài kiểm thử là thất bại, nhưng cho phép chạy các assertion khác. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``CHECK_FALSE`` | Kiểm tra điều kiện không đúng. Đánh dấu lần chạy bài kiểm thử là thất bại, nhưng cho phép chạy các assertion khác. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``WARN`` | Kiểm tra điều kiện là đúng. Không làm thất bại bài kiểm thử trong bất kỳ trường hợp nào, nhưng ghi nhật ký cảnh báo nếu điều kiện không đúng. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``WARN_FALSE`` | Kiểm tra điều kiện không đúng. Không làm thất bại bài kiểm thử trong bất kỳ trường hợp nào, nhưng ghi nhật ký cảnh báo nếu điều kiện đúng. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Tất cả assertion trên đều có các macro ``*_MESSAGE`` tương ứng, cho phép in thông báo tùy chọn giải thích lý do điều gì đó nên xảy ra.

Ưu tiên sử dụng ``CHECK`` cho các assertion tự giải thích và ``CHECK_MESSAGE`` cho những assertion phức tạp hơn nếu bạn cho rằng chúng cần được giải thích rõ hơn.

.. seealso::

    `doctest: Assertion macros <https://github.com/doctest/doctest/blob/master/doc/markdown/assertions.md>`_.

Ghi nhật ký
~~~~~~~~~~~

Đầu ra của bài kiểm thử được chính doctest xử lý và hoàn toàn không dựa vào chức năng in hoặc ghi nhật ký của Godot, vì vậy nên sử dụng các macro chuyên dụng cho phép ghi đầu ra kiểm thử theo định dạng do doctest viết.

+----------------+-----------------------------------------------------------------------------------------------------------+
| **Macro** | **Mô tả** |
+++++++++++++++++++++++++
| ``MESSAGE`` | In một thông báo. |
+++++++++++++++++++++++++++++++++++
| ``FAIL_CHECK`` | Đánh dấu bài kiểm thử là thất bại nhưng tiếp tục thực thi. Có thể bọc trong các điều kiện cho những phép kiểm tra phức tạp. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``FAIL`` | Ngay lập tức làm thất bại bài kiểm thử. Có thể bọc trong các điều kiện cho những phép kiểm tra phức tạp. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Có thể chọn các reporter khác nhau trong thời gian chạy. Ví dụ, dưới đây là cách chuyển hướng đầu ra sang một tệp XML:

.. code-block:: shell

    ./bin/<godot_binary> --test --source-file="*test_validate*" --success --reporters=xml --out=doctest.txt

.. seealso::

    `doctest: Logging macros <https://github.com/doctest/doctest/blob/master/doc/markdown/logging.md>`_.

Kiểm thử các đường dẫn thất bại
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đôi khi không phải lúc nào cũng khả thi để kiểm tra một kết quả *được mong đợi*. Theo triết lý phát triển Godot rằng engine không được crash và phải phục hồi một cách an toàn bất cứ khi nào xảy ra lỗi không nghiêm trọng, điều quan trọng là phải kiểm tra rằng các đường dẫn thất bại đó thực sự an toàn để thực thi mà không làm engine crash.

Hành vi *không mong đợi* có thể được kiểm thử giống như mọi thứ khác. Vấn đề duy nhất là việc này khiến đầu ra kiểm thử bị làm nhiễu không cần thiết bởi các lỗi do chính engine in ra (ngay cả khi kết quả cuối cùng là thành công).

Để khắc phục vấn đề này, hãy sử dụng trực tiếp các macro ``ERR_PRINT_OFF`` và ``ERR_PRINT_ON`` bên trong các trường hợp kiểm thử để tạm thời tắt đầu ra lỗi từ engine, chẳng hạn như:

.. code-block:: cpp

    TEST_CASE("[Color] Constructor methods") {
        ERR_PRINT_OFF;
        Color html_invalid = Color::html("invalid");
        ERR_PRINT_ON; // Don't forget to re-enable!

        CHECK_MESSAGE(html_invalid.is_equal_approx(Color()),
            "Invalid HTML notation should result in a Color with the default values.");
    }

Các tag đặc biệt trong tên trường hợp kiểm thử
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể thêm các tag này vào tên trường hợp kiểm thử để sửa đổi hoặc mở rộng môi trường kiểm thử:

+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Tag** | **Mô tả** |
+++++++++++++++++++++++
| ``[SceneTree]`` | Bắt buộc đối với các trường hợp kiểm thử phụ thuộc vào một scene tree có MessageQueue khả dụng. Tag này cũng bật một rendering server giả lập và :ref:`ThemeDB<class_ThemeDB>`. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``[Editor]`` | Tương tự ``[SceneTree]``, nhưng có thêm cơ sở hạ tầng liên quan đến editor, chẳng hạn như :ref:`EditorSettings<class_EditorSettings>`. |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``[Audio]`` | Khởi tạo :ref:`AudioServer<class_AudioServer>` bằng trình điều khiển âm thanh giả lập. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``[Navigation2D]`` | Tạo máy chủ điều hướng 2D mặc định và cung cấp máy chủ này để kiểm thử. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| ``[Navigation3D]`` | Tạo máy chủ điều hướng 3D mặc định và cung cấp máy chủ này để kiểm thử. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Bạn có thể sử dụng chúng cùng nhau để kết hợp nhiều phần mở rộng môi trường kiểm thử.

Kiểm thử tín hiệu
~~~~~~~~~~~~~~~~~

Các macro sau đây có thể được sử dụng để kiểm thử tín hiệu:

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Macro - Mô tả * - ``SIGNAL_WATCH(object, "signal_name")`` - Bắt đầu theo dõi tín hiệu được chỉ định trên đối tượng đã cho. * - ``SIGNAL_UNWATCH(object, "signal_name")`` - Dừng theo dõi tín hiệu được chỉ định trên đối tượng đã cho. * - ``SIGNAL_CHECK("signal_name", Vector<Vector<Variant>>)`` - Kiểm tra các đối số của tất cả tín hiệu đã phát. Vector bên ngoài chứa từng tín hiệu đã phát, trong khi vector bên trong chứa danh sách các đối số của tín hiệu đó. Thứ tự của các tín hiệu là quan trọng. * - ``SIGNAL_CHECK_FALSE("signal_name")`` - Kiểm tra xem tín hiệu được chỉ định có chưa được phát hay không. * - ``SIGNAL_DISCARD("signal_name")`` - Xóa tất cả bản ghi của tín hiệu được chỉ định.

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

Công cụ kiểm thử là các phương thức nâng cao cho phép bạn chạy các quy trình tùy ý nhằm hỗ trợ quá trình kiểm thử thủ công và gỡ lỗi các phần bên trong của engine.

Bạn có thể chạy các công cụ này bằng cách cung cấp tên của một công cụ sau tùy chọn dòng lệnh ``--test``. Ví dụ, module GDScript triển khai và đăng ký một số công cụ để hỗ trợ gỡ lỗi tokenizer, parser và compiler:

.. code-block:: shell

    ./bin/<godot_binary> --test gdscript-tokenizer test.gd
    ./bin/<godot_binary> --test gdscript-parser test.gd
    ./bin/<godot_binary> --test gdscript-compiler test.gd

Nếu phát hiện bất kỳ công cụ nào như vậy, phần còn lại của các bài kiểm thử đơn vị sẽ được bỏ qua.

Công cụ kiểm thử có thể được đăng ký ở bất kỳ đâu trong engine, vì cơ chế đăng ký gần giống với cơ chế mà doctest cung cấp khi đăng ký các trường hợp kiểm thử bằng kỹ thuật khởi tạo động. Tuy nhiên, thông thường chúng có thể được đăng ký trong các tệp nguồn ``register_types.cpp`` tương ứng (theo module hoặc core).

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

Bản thân công cụ kiểm thử có thể thực hiện việc phân tích cú pháp dòng lệnh tùy chỉnh với sự trợ giúp của phương thức OS :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>`.

Kiểm thử tích hợp cho GDScript
------------------------------

Godot sử dụng doctest để ngăn ngừa hồi quy trong GDScript trong quá trình phát triển. Có thể viết một số loại tập lệnh kiểm thử sau:

- các bài kiểm thử lỗi dự kiến; - các bài kiểm thử cảnh báo; - các bài kiểm thử tính năng.

Do đó, quy trình viết các bài kiểm thử tích hợp cho GDScript như sau:

1. Chọn loại tập lệnh kiểm thử mà bạn muốn viết, rồi tạo một tệp GDScript mới trong thư mục ``modules/gdscript/tests/scripts`` thuộc thư mục con tương ứng.

2. Viết mã GDScript. Tập lệnh kiểm thử phải có một hàm tên là ``test()`` và không nhận đối số nào. Hàm này sẽ được trình chạy kiểm thử gọi. Bài kiểm thử không nên có bất kỳ phần phụ thuộc nào, trừ khi phần phụ thuộc đó cũng là một phần của bài kiểm thử. Các lớp toàn cục (sử dụng ``class_name``) được đăng ký trước khi trình chạy khởi động, vì vậy chúng sẽ hoạt động nếu cần.

   Dưới đây là một ví dụ về tập lệnh kiểm thử:

   ::

        func test():
            if true # Missing colon here.
                print("true")

3. Chuyển thư mục hiện tại đến thư mục gốc của kho mã nguồn Godot.

   .. code-block:: shell

       cd godot

4. Tạo các tệp ``*.out`` để cập nhật kết quả dự kiến từ đầu ra:

   .. code-block:: shell

       bin/<godot_binary> --gdscript-generate-tests modules/gdscript/tests/scripts

Bạn có thể thêm tùy chọn ``--print-filenames`` để xem tên tệp khi đầu ra kiểm thử của chúng được tạo. Nếu bạn đang làm việc trên một tính năng mới gây ra lỗi nghiêm trọng, bạn có thể sử dụng tùy chọn này để nhanh chóng tìm tệp kiểm thử gây ra lỗi rồi bắt đầu gỡ lỗi từ đó.

5. Chạy các bài kiểm thử GDScript bằng:

   .. code-block:: shell

       ./bin/<godot_binary> --test --test-suite="*GDScript*"

Lệnh này cũng chấp nhận tùy chọn ``--print-filenames`` (xem ở trên).

Nếu không có lỗi nào được in ra và mọi thứ diễn ra suôn sẻ, bạn đã hoàn tất!

.. warning::

    Hãy đảm bảo đầu ra có các giá trị như mong đợi trước khi gửi pull request. Nếu ``--gdscript-generate-tests`` tạo ra các tệp ``*.out`` không liên quan đến các bài kiểm thử mới được thêm, bạn nên khôi phục các tệp đó và chỉ commit các tệp ``*.out`` cho những bài kiểm thử mới.

.. note::

    Trình chạy kiểm thử GDScript được dùng để kiểm thử phần triển khai GDScript, không phải để kiểm thử các tập lệnh của người dùng hay kiểm thử engine bằng các tập lệnh. Chúng tôi khuyến nghị viết các bài kiểm thử mới cho các `issue liên quan đến GDScript đã được giải quyết tại GitHub <https://github.com/godotengine/godot/issues?q=is%3Aissue+label%3Atopic%3Agdscript+is%3Aclosed>`_, hoặc viết các bài kiểm thử cho những tính năng hiện đang hoạt động.

.. note::

    Nếu trường hợp kiểm thử của bạn yêu cầu tệp tập lệnh không có hàm ``test()`` bên trong, bạn có thể vô hiệu hóa phần runtime của bài kiểm thử bằng cách đặt tên tệp tập lệnh sao cho khớp với mẫu ``*.notest.gd``. Ví dụ: "test_empty_file.notest.gd".
