.. _doc_custom_modules_in_cpp:

Các mô-đun tùy chỉnh trong C++
==============================

Mô-đun
------

Godot cho phép mở rộng engine theo cách mô-đun. Bạn có thể tạo các mô-đun mới rồi bật/tắt chúng. Điều này cho phép thêm chức năng mới cho engine ở mọi cấp độ mà không cần sửa đổi phần lõi, vốn có thể được tách ra để sử dụng và tái sử dụng trong các mô-đun khác nhau.

Các mô-đun nằm trong thư mục con ``modules/`` của hệ thống build. Theo mặc định, hàng chục mô-đun được bật, chẳng hạn như GDScript (đúng vậy, nó không thuộc engine cơ sở), hỗ trợ GridMap, mô-đun biểu thức chính quy và nhiều mô-đun khác. Bạn có thể tạo và kết hợp bao nhiêu mô-đun mới tùy ý. Hệ thống build SCons sẽ xử lý việc này một cách trong suốt.

Dùng để làm gì?
---------------

Mặc dù khuyến nghị viết phần lớn trò chơi bằng ngôn ngữ script (vì điều này tiết kiệm rất nhiều thời gian), bạn hoàn toàn có thể sử dụng C++ thay thế. Việc thêm các mô-đun C++ có thể hữu ích trong những trường hợp sau:

-  Liên kết một thư viện bên ngoài với Godot (chẳng hạn PhysX, FMOD, v.v.). - Tối ưu hóa các phần quan trọng của trò chơi. - Thêm chức năng mới cho engine và/hoặc editor. - Chuyển một trò chơi hiện có sang Godot. - Viết toàn bộ một trò chơi mới bằng C++ vì bạn không thể sống thiếu C++.


.. note::

    Mặc dù có thể sử dụng các mô-đun cho logic trò chơi tùy chỉnh,
    :ref:`GDExtension <doc_gdextension>` is generally more suited as it doesn't
    bạn sẽ phải biên dịch lại engine sau mỗi lần thay đổi mã.

    Các mô-đun C++ chủ yếu cần thiết khi GDExtension không đáp ứng đủ và cần tích hợp sâu hơn với engine.

.. _doc_creating_custom_modules_in_cpp:

Tạo mô-đun mới
--------------

Trước khi tạo mô-đun, hãy đảm bảo rằng bạn đã :ref:`download the source code of Godot and compile it <toc-devel-compiling>`.

Để tạo mô-đun mới, bước đầu tiên là tạo một thư mục bên trong ``modules/``. Nếu muốn duy trì mô-đun riêng biệt, bạn có thể checkout một VCS khác vào modules và sử dụng nó.

Mô-đun ví dụ sẽ có tên là "summator" (``godot/modules/summator``). Bên trong đó, chúng ta sẽ tạo một lớp summator:

.. code-block:: cpp
    :caption: godot/modules/summator/summator.h

    #pragma once

    #include "core/object/ref_counted.h"

    class Summator : public RefCounted {
        GDCLASS(Summator, RefCounted);

        int count;

    protected:
        static void _bind_methods();

    public:
        void add(int p_value);
        void reset();
        int get_total() const;

        Summator();
    };

Sau đó là tệp cpp.

.. code-block:: cpp
    :caption: godot/modules/summator/summator.cpp

    #include "summator.h"

    #include "core/object/class_db.h"

    void Summator::add(int p_value) {
        count += p_value;
    }

    void Summator::reset() {
        count = 0;
    }

    int Summator::get_total() const {
        return count;
    }

    void Summator::_bind_methods() {
        ClassDB::bind_method(D_METHOD("add", "value"), &Summator::add);
        ClassDB::bind_method(D_METHOD("reset"), &Summator::reset);
        ClassDB::bind_method(D_METHOD("get_total"), &Summator::get_total);
    }

    Summator::Summator() {
        count = 0;
    }

Tiếp theo, lớp mới cần được đăng ký theo một cách nào đó, vì vậy cần tạo thêm hai tệp:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các tệp này phải nằm trong thư mục cấp cao nhất của mô-đun (cùng cấp với các tệp ``SCsub`` và ``config.py``) để mô-đun được đăng ký đúng cách.

Các tệp này cần chứa nội dung sau:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #include "modules/register_module_types.h"

    void initialize_summator_module(ModuleInitializationLevel p_level);
    void uninitialize_summator_module(ModuleInitializationLevel p_level);
    /* yes, the word in the middle must be the same as the module folder name */

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.cpp

    #include "register_types.h"

    #include "core/object/class_db.h"
    #include "summator.h"

    void initialize_summator_module(ModuleInitializationLevel p_level) {
        if (p_level != MODULE_INITIALIZATION_LEVEL_SCENE) {
            return;
        }
        ClassDB::register_class<Summator>();
    }

    void uninitialize_summator_module(ModuleInitializationLevel p_level) {
        if (p_level != MODULE_INITIALIZATION_LEVEL_SCENE) {
            return;
        }
       // Nothing to do here in this example.
    }

Tiếp theo, chúng ta cần tạo một tệp ``SCsub`` để hệ thống build biên dịch mô-đun này:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    # SCsub

    Import('env')

    env.add_source_files(env.modules_sources, "*.cpp") # Add all cpp files to the build

Với nhiều mã nguồn, bạn cũng có thể thêm từng tệp riêng lẻ vào một danh sách chuỗi Python:

.. code-block:: python

    src_list = ["summator.cpp", "other.cpp", "etc.cpp"]
    env.add_source_files(env.modules_sources, src_list)

Điều này mở ra những khả năng mạnh mẽ khi sử dụng Python để xây dựng danh sách tệp bằng các vòng lặp và câu lệnh logic. Hãy xem một số mô-đun được cung cấp mặc định cùng Godot để tham khảo ví dụ.

Để thêm các thư mục include cho trình biên dịch tìm kiếm, bạn có thể nối chúng vào các đường dẫn của môi trường:

.. code-block:: python

    env.Append(CPPPATH=["mylib/include"]) # this is a relative path
    env.Append(CPPPATH=["#myotherlib/include"]) # this is an 'absolute' path

Nếu muốn thêm các cờ trình biên dịch tùy chỉnh khi build mô-đun, trước tiên bạn cần clone ``env``, để các cờ đó không được thêm vào toàn bộ quá trình build Godot (điều này có thể gây lỗi). Ví dụ ``SCsub`` với các cờ tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    Import('env')

    module_env = env.Clone()
    module_env.add_source_files(env.modules_sources, "*.cpp")
    # Append CCFLAGS flags for both C and C++ code.
    module_env.Append(CCFLAGS=['-O2'])
    # If you need to, you can:
    # - Append CFLAGS for C code only.
    # - Append CXXFLAGS for C++ code only.

Cuối cùng là tệp cấu hình cho mô-đun; đây là một script Python phải được đặt tên là ``config.py``:

.. code-block:: python
    :caption: godot/modules/summator/config.py

    # config.py

    def can_build(env, platform):
        return True

    def configure(env):
        pass

Mô-đun sẽ được hỏi xem có thể build cho nền tảng cụ thể hay không (trong trường hợp này, ``True`` có nghĩa là mô-đun sẽ được build cho mọi nền tảng).

Vậy là xong. Hy vọng mọi thứ không quá phức tạp! Mô-đun của bạn sẽ có cấu trúc như sau:

.. code-block:: none

    godot/modules/summator/config.py
    godot/modules/summator/summator.h
    godot/modules/summator/summator.cpp
    godot/modules/summator/register_types.h
    godot/modules/summator/register_types.cpp
    godot/modules/summator/SCsub

Sau đó, bạn có thể nén nó thành tệp zip và chia sẻ mô-đun với mọi người. Khi build cho mọi nền tảng (theo hướng dẫn trong các phần trước), mô-đun của bạn sẽ được đưa vào.

Sử dụng mô-đun
--------------

Bây giờ bạn có thể sử dụng mô-đun vừa tạo từ bất kỳ script nào:

.. tabs::
 .. code-tab:: gdscript GDScript

    var s = Summator.new() s.add(10) s.add(20) s.add(30) print(s.get_total()) s.reset()

Kết quả sẽ là ``60``.

.. seealso:: The previous Summator example is great for small, custom modules,
  nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy tham khảo
  :ref:`doc_binding_to_external_libraries` for details about binding to
  các thư viện bên ngoài.

.. warning:: If your module is meant to be accessed from the running project
             (không chỉ từ editor), bạn cũng phải biên dịch lại mọi export template mà bạn định sử dụng, sau đó chỉ định đường dẫn đến template tùy chỉnh trong từng export preset. Nếu không, bạn sẽ gặp lỗi khi chạy dự án vì mô-đun chưa được biên dịch trong export template. Xem các trang :ref:`Compiling <toc-devel-compiling>` để biết thêm thông tin.

Biên dịch mô-đun bên ngoài
--------------------------

Việc biên dịch một mô-đun bao gồm di chuyển trực tiếp mã nguồn của mô-đun vào thư mục ``modules/`` của engine. Mặc dù đây là cách đơn giản nhất để biên dịch mô-đun, có một vài lý do khiến cách này có thể không thực tế:

1. Phải sao chép thủ công mã nguồn của mô-đun mỗi khi bạn muốn biên dịch engine có hoặc không có mô-đun, hoặc thực hiện thêm các bước cần thiết để tắt thủ công một mô-đun trong quá trình biên dịch bằng một tùy chọn build tương tự như ``module_summator_enabled=no``. Tạo symbolic link cũng có thể là một giải pháp, nhưng bạn có thể còn phải vượt qua các hạn chế của hệ điều hành, chẳng hạn như cần đặc quyền symbolic link nếu thực hiện việc này qua script.

2. Tùy thuộc vào việc bạn có phải làm việc với mã nguồn của engine hay không, các tệp mô-đun được thêm trực tiếp vào ``modules/`` sẽ thay đổi working tree đến mức việc sử dụng VCS (chẳng hạn ``git``) trở nên cồng kềnh, vì bạn phải đảm bảo chỉ các mã liên quan đến engine được commit bằng cách lọc các thay đổi.

Vì vậy, nếu bạn cảm thấy cần cấu trúc độc lập của các mô-đun tùy chỉnh, hãy lấy mô-đun "summator" của chúng ta và di chuyển nó đến thư mục cha của engine:

.. code-block:: shell

    mkdir ../modules
    mv modules/summator ../modules

Biên dịch engine cùng với mô-đun bằng cách cung cấp tùy chọn build ``custom_modules``, tùy chọn này nhận một danh sách các đường dẫn thư mục được phân tách bằng dấu phẩy, chứa các mô-đun C++ tùy chỉnh, tương tự như sau:

.. code-block:: shell

    scons custom_modules=../modules

Hệ thống build sẽ phát hiện tất cả mô-đun bên dưới thư mục ``../modules`` và biên dịch chúng tương ứng, bao gồm mô-đun "summator" của chúng ta.

.. warning::

    Mọi đường dẫn được truyền cho ``custom_modules`` sẽ được chuyển đổi nội bộ thành đường dẫn tuyệt đối để phân biệt giữa các mô-đun tùy chỉnh và mô-đun tích hợp sẵn. Điều này có nghĩa là những việc như tạo tài liệu mô-đun có thể phụ thuộc vào một cấu trúc đường dẫn cụ thể trên máy của bạn.

.. seealso::

    :ref:`Introduction to the buildsystem - Custom modules build option <doc_buildsystem_custom_modules>`.

Tùy chỉnh việc khởi tạo các loại mô-đun
---------------------------------------

Các mô-đun có thể tương tác với những lớp engine tích hợp sẵn khác trong thời gian chạy và thậm chí ảnh hưởng đến cách các kiểu lõi được khởi tạo. Cho đến nay, chúng ta đã sử dụng ``register_summator_types`` để đưa các lớp mô-đun vào engine và giúp chúng khả dụng.

Có thể tóm tắt sơ lược thứ tự thiết lập engine bằng danh sách các phương thức đăng ký kiểu sau:

.. code-block:: cpp

    preregister_module_types();
    preregister_server_types();
    register_core_singletons();
    register_server_types();
    register_scene_types();
    EditorNode::register_editor_types();
    register_platform_apis();
    register_module_types();
    initialize_physics();
    initialize_navigation_server();
    register_server_singletons();
    register_driver_types();
    ScriptServer::init_languages();

Lớp ``Summator`` của chúng ta được khởi tạo trong lần gọi ``register_module_types()``. Hãy tưởng tượng chúng ta cần đáp ứng một số phụ thuộc thời gian chạy phổ biến của mô-đun (chẳng hạn singleton), hoặc cho phép ghi đè các callback phương thức hiện có của engine trước khi chính engine gán chúng. Trong trường hợp đó, chúng ta muốn đảm bảo các lớp mô-đun được đăng ký *trước* mọi kiểu tích hợp sẵn khác.

Đây là nơi chúng ta có thể định nghĩa một phương thức ``preregister_summator_types()`` tùy chọn, phương thức này sẽ được gọi trước mọi thứ khác trong giai đoạn thiết lập engine ``preregister_module_types()``.

Bây giờ chúng ta cần thêm phương thức này vào các tệp header và mã nguồn của ``register_types``:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #define MODULE_SUMMATOR_HAS_PREREGISTER
    void preregister_summator_types();

    void register_summator_types();
    void unregister_summator_types();

.. note:: Unlike other register methods, we have to explicitly define
          ``MODULE_SUMMATOR_HAS_PREREGISTER`` để cho hệ thống build biết những lần gọi phương thức liên quan nào cần được đưa vào trong thời gian biên dịch. Tên mô-đun cũng phải được chuyển thành chữ hoa.

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.cpp

    #include "register_types.h"

    #include "core/object/class_db.h"
    #include "summator.h"

    void preregister_summator_types() {
        // Called before any other core types are registered.
        // Nothing to do here in this example.
    }

    void register_summator_types() {
        ClassDB::register_class<Summator>();
    }

    void unregister_summator_types() {
       // Nothing to do here in this example.
    }

Viết tài liệu tùy chỉnh
-----------------------

Viết tài liệu có vẻ là một công việc nhàm chán, nhưng bạn rất nên ghi lại tài liệu cho mô-đun vừa tạo để người dùng dễ tận dụng nó hơn. Chưa kể mã bạn viết cách đây một năm có thể trở nên không thể phân biệt với mã do người khác viết, vì vậy hãy đối xử tử tế với chính mình trong tương lai!

Có một số bước để thiết lập tài liệu tùy chỉnh cho mô-đun:

1. Tạo một thư mục mới ở thư mục gốc của mô-đun. Tên thư mục có thể là bất kỳ tên nào, nhưng trong suốt phần này chúng ta sẽ sử dụng tên ``doc_classes``.

2. Bây giờ, chúng ta cần chỉnh sửa ``config.py`` và thêm đoạn mã sau:

   .. code-block:: python

        def get_doc_path():
            return "doc_classes"

        def get_doc_classes():
            return [
                "Summator",
            ]

Hàm ``get_doc_path()`` được hệ thống build sử dụng để xác định vị trí của tài liệu. Trong trường hợp này, tài liệu sẽ nằm trong thư mục ``modules/summator/doc_classes``. Nếu không định nghĩa hàm này, đường dẫn tài liệu cho mô-đun sẽ quay về thư mục ``doc/classes`` chính.

Phương thức ``get_doc_classes()`` cần thiết để hệ thống build biết những lớp đã đăng ký nào thuộc về mô-đun. Bạn cần liệt kê tất cả lớp của mình tại đây. Những lớp không được liệt kê sẽ nằm trong thư mục ``doc/classes`` chính.

.. tip::

    Bạn có thể sử dụng Git để kiểm tra xem mình có bỏ sót lớp nào không bằng cách kiểm tra các tệp chưa được theo dõi với ``git status``. Ví dụ:

    ::

        git status

    Kết quả ví dụ:

    ::

        Untracked files:
            (use "git add <file>..." to include in what will be committed)

            doc/classes/MyClass2D.xml
            doc/classes/MyClass4D.xml
            doc/classes/MyClass5D.xml
            doc/classes/MyClass6D.xml
            ...


3. Bây giờ chúng ta có thể tạo tài liệu:

Chúng ta có thể thực hiện việc này bằng cách chạy doctool của Godot, tức ``godot --doctool <path>``, công cụ này sẽ kết xuất tham chiếu API của engine vào ``<path>`` đã cho ở định dạng XML.

Trong trường hợp của chúng ta, hãy trỏ nó đến thư mục gốc của repository đã clone. Bạn có thể trỏ nó đến một thư mục khác và chỉ sao chép các tệp cần thiết.

Chạy lệnh:

::

    bin/<godot_binary> --doctool .

Bây giờ nếu đi đến thư mục ``godot/modules/summator/doc_classes``, bạn sẽ thấy thư mục này chứa một tệp ``Summator.xml``, hoặc bất kỳ lớp nào khác mà bạn đã tham chiếu trong hàm ``get_doc_classes``.

Chỉnh sửa (các) tệp theo `class reference primer <https://docs.godotengine.org/en/latest/engine_details/class_reference/index.html>`__ rồi biên dịch lại engine.

Sau khi quá trình biên dịch hoàn tất, tài liệu sẽ có thể được truy cập trong hệ thống tài liệu tích hợp sẵn của engine.

Để luôn cập nhật tài liệu, từ giờ bạn chỉ cần sửa đổi một trong các tệp XML rồi biên dịch lại engine.

Nếu bạn thay đổi API của module, bạn cũng có thể trích xuất lại tài liệu; chúng sẽ chứa những nội dung bạn đã thêm trước đó. Tất nhiên, nếu bạn trỏ đến thư mục godot của mình, hãy đảm bảo không làm mất công việc bằng cách trích xuất tài liệu cũ từ một bản build engine cũ lên trên tài liệu mới hơn.

Lưu ý rằng nếu bạn không có quyền ghi vào ``<path>`` đã cung cấp, bạn có thể gặp lỗi tương tự như sau:

.. code-block:: console

    ERROR: Can't write doc file: docs/doc/classes/@GDScript.xml
       At: editor/doc/doc_data.cpp:956

.. _doc_custom_module_unit_tests:

Viết các bài kiểm thử đơn vị tùy chỉnh
--------------------------------------

Bạn có thể viết các bài kiểm thử đơn vị độc lập như một phần của module C++. Nếu bạn vẫn chưa quen với quy trình kiểm thử đơn vị trong Godot, vui lòng tham khảo
:ref:`doc_unit_testing`.

Quy trình như sau:

1. Tạo một thư mục mới có tên ``tests/`` bên dưới thư mục gốc của module:

.. code-block:: console

    cd modules/summator
    mkdir tests
    cd tests

2. Tạo một bộ kiểm thử mới: ``test_summator.h``. Tên tiêu đề phải có tiền tố ``test_`` để hệ thống build có thể thu thập và đưa nó vào ``tests/test_main.cpp``, nơi các bài kiểm thử được chạy.

3. Viết một số trường hợp kiểm thử. Đây là một ví dụ:

.. code-block:: cpp
    :caption: godot/modules/summator/tests/test_summator.h

    #pragma once

    #include "tests/test_macros.h"

    #include "modules/summator/summator.h"

    namespace TestSummator {

    TEST_CASE("[Modules][Summator] Adding numbers") {
        Ref<Summator> s = memnew(Summator);
        CHECK(s->get_total() == 0);

        s->add(10);
        CHECK(s->get_total() == 10);

        s->add(20);
        CHECK(s->get_total() == 30);

        s->add(30);
        CHECK(s->get_total() == 60);

        s->reset();
        CHECK(s->get_total() == 0);
    }

    } // namespace TestSummator

4. Biên dịch engine với ``scons tests=yes``, rồi chạy các bài kiểm thử bằng lệnh sau:

.. code-block:: console

    ./bin/<godot_binary> --test --source-file="*test_summator*" --success

Bây giờ bạn sẽ thấy các assertion đạt.

.. _doc_custom_module_icons:

Thêm biểu tượng tùy chỉnh cho editor
------------------------------------

Tương tự như việc bạn có thể viết tài liệu độc lập bên trong một module, bạn cũng có thể tạo các biểu tượng tùy chỉnh của riêng mình để hiển thị cho các lớp trong editor.

Để biết quy trình thực tế tạo các biểu tượng cho editor và tích hợp chúng vào engine, trước tiên hãy tham khảo :ref:`doc_editor_icons`.

Sau khi tạo xong (các) biểu tượng, hãy thực hiện các bước sau:

1. Tạo một thư mục mới trong thư mục gốc của module với tên ``icons``. Đây là đường dẫn mặc định để engine tìm các biểu tượng cho editor của module.

2. Di chuyển các biểu tượng ``svg`` mới tạo (đã tối ưu hoặc chưa) vào thư mục đó.

3. Biên dịch lại engine và chạy editor. Bây giờ (các) biểu tượng sẽ xuất hiện trong giao diện editor ở những vị trí phù hợp.

Nếu muốn lưu các biểu tượng ở một nơi khác trong module, hãy thêm đoạn mã sau vào ``config.py`` để ghi đè đường dẫn mặc định:

   .. code-block:: python

       def get_icons_path():
           return "path/to/icons"

Tổng kết
--------

Hãy nhớ:

-  Sử dụng macro ``GDCLASS`` để kế thừa, để Godot có thể bọc nó. - Sử dụng ``_bind_methods`` để liên kết các hàm với scripting và cho phép chúng hoạt động như các callback cho signal. - **Tránh đa kế thừa đối với các lớp được expose cho Godot**, vì ``GDCLASS`` không hỗ trợ điều này. Bạn vẫn có thể sử dụng đa kế thừa trong các lớp của riêng mình miễn là chúng không được expose cho scripting API của Godot.

Nhưng đó vẫn chưa phải là tất cả; tùy vào những gì bạn làm, bạn sẽ được chào đón bằng một số điều bất ngờ (hy vọng là tích cực).

-  Nếu bạn kế thừa từ :ref:`class_Node` (hoặc bất kỳ kiểu node dẫn xuất nào, chẳng hạn như Sprite2D), lớp mới của bạn sẽ xuất hiện trong editor, trong cây kế thừa của hộp thoại "Add Node". - Nếu bạn kế thừa từ :ref:`class_Resource`, nó sẽ xuất hiện trong danh sách tài nguyên, và tất cả các thuộc tính được expose có thể được tuần tự hóa khi lưu/tải. - Theo cùng logic này, bạn có thể mở rộng Editor và gần như bất kỳ khu vực nào của engine.
