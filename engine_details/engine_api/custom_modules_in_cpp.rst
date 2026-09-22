.. _doc_custom_modules_in_cpp:

Mô-đun tùy chỉnh trong C++
==========================

Mô-đun
------

Godot cho phép mở rộng engine theo cách mô-đun. Bạn có thể tạo các mô-đun mới rồi bật/tắt chúng. Điều này cho phép thêm chức năng mới cho engine ở mọi cấp độ mà không cần sửa đổi phần lõi, vốn có thể được tách ra để sử dụng và tái sử dụng trong các mô-đun khác nhau.

Các mô-đun nằm trong thư mục con ``modules/`` của hệ thống build. Theo mặc định, hàng chục mô-đun được bật, chẳng hạn như GDScript (đúng vậy, nó không thuộc engine cơ sở), hỗ trợ GridMap, mô-đun regular expressions và nhiều mô-đun khác. Bạn có thể tạo và kết hợp bao nhiêu mô-đun mới tùy thích. Hệ thống build SCons sẽ xử lý việc này một cách trong suốt.

Dùng để làm gì?
---------------

Mặc dù nên viết phần lớn game bằng scripting (vì nó tiết kiệm rất nhiều thời gian), bạn hoàn toàn có thể sử dụng C++ thay thế. Việc thêm các mô-đun C++ có thể hữu ích trong những trường hợp sau:

-  Binding một thư viện bên ngoài vào Godot (chẳng hạn như PhysX, FMOD, v.v.).
-  Tối ưu các phần quan trọng của game.
-  Thêm chức năng mới cho engine và/hoặc editor.
-  Port một game hiện có sang Godot.
-  Viết toàn bộ một game mới bằng C++ vì bạn không thể sống thiếu C++.


.. note::

    Mặc dù có thể sử dụng các mô-đun cho game logic tùy chỉnh,
    :ref:`GDExtension <doc_gdextension>` thường phù hợp hơn vì không yêu cầu biên dịch lại engine sau mỗi thay đổi mã.

    Các mô-đun C++ chủ yếu cần thiết khi GDExtension không đủ đáp ứng và cần tích hợp sâu hơn với engine.

.. _doc_creating_custom_modules_in_cpp:

Tạo mô-đun mới
--------------

Trước khi tạo mô-đun, hãy đảm bảo bạn đã :ref:`tải xuống mã nguồn của Godot và biên dịch nó <toc-devel-compiling>`.

Để tạo một mô-đun mới, bước đầu tiên là tạo một thư mục bên trong ``modules/``. Nếu muốn duy trì mô-đun riêng biệt, bạn có thể checkout một VCS khác vào modules và sử dụng nó.

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

Tiếp theo, lớp mới cần được đăng ký bằng cách nào đó, vì vậy cần tạo thêm hai tệp:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các tệp này phải nằm trong thư mục cấp cao nhất của mô-đun (cạnh các tệp ``SCsub`` và ``config.py``) để mô-đun được đăng ký đúng cách.

Các tệp này phải chứa nội dung sau:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #include "modules/register_module_types.h"

    void initialize_summator_module(ModuleInitializationLevel p_level);
    void uninitialize_summator_module(ModuleInitializationLevel p_level);
    /* đúng vậy, từ ở giữa phải giống với tên thư mục mô-đun */

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
       // Không cần làm gì ở đây trong ví dụ này.
    }

Tiếp theo, chúng ta cần tạo một tệp ``SCsub`` để hệ thống build biên dịch mô-đun này:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    # SCsub

    Import('env')

    env.add_source_files(env.modules_sources, "*.cpp") # Thêm tất cả các tệp cpp vào build

Với nhiều mã nguồn, bạn cũng có thể thêm từng tệp riêng lẻ vào một danh sách chuỗi Python:

.. code-block:: python

    src_list = ["summator.cpp", "other.cpp", "etc.cpp"]
    env.add_source_files(env.modules_sources, src_list)

Điều này mở ra nhiều khả năng mạnh mẽ khi sử dụng Python để xây dựng danh sách tệp bằng các vòng lặp và câu lệnh logic. Hãy xem một số mô-đun được cung cấp mặc định cùng Godot để tham khảo ví dụ.

Để thêm các thư mục include mà compiler sẽ tra cứu, bạn có thể nối chúng vào các đường dẫn của environment:

.. code-block:: python

    env.Append(CPPPATH=["mylib/include"]) # đây là đường dẫn tương đối
    env.Append(CPPPATH=["#myotherlib/include"]) # đây là đường dẫn 'tuyệt đối'

Nếu muốn thêm các cờ compiler tùy chỉnh khi build mô-đun, trước tiên bạn cần clone ``env``, để các cờ đó không được thêm vào toàn bộ bản build Godot (điều này có thể gây lỗi). Ví dụ ``SCsub`` với các cờ tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    Import('env')

    module_env = env.Clone()
    module_env.add_source_files(env.modules_sources, "*.cpp")
    # Nối các cờ CCFLAGS cho cả mã C và C++.
    module_env.Append(CCFLAGS=['-O2'])
    # Nếu cần, bạn có thể:
    # - Nối CFLAGS chỉ dành cho mã C.
    # - Nối CXXFLAGS chỉ dành cho mã C++.

Cuối cùng là tệp cấu hình cho mô-đun; đây là một script Python phải được đặt tên là ``config.py``:

.. code-block:: python
    :caption: godot/modules/summator/config.py

    # config.py

    def can_build(env, platform):
        return True

    def configure(env):
        pass

Mô-đun được hỏi liệu có thể build trên nền tảng cụ thể hay không (trong trường hợp này, ``True`` có nghĩa là nó sẽ build trên mọi nền tảng).

Vậy là xong. Hy vọng mọi thứ không quá phức tạp! Mô-đun của bạn sẽ trông như sau:

.. code-block:: none

    godot/modules/summator/config.py
    godot/modules/summator/summator.h
    godot/modules/summator/summator.cpp
    godot/modules/summator/register_types.h
    godot/modules/summator/register_types.cpp
    godot/modules/summator/SCsub

Sau đó, bạn có thể nén nó thành zip và chia sẻ mô-đun với mọi người. Khi build cho mọi nền tảng (theo hướng dẫn trong các phần trước), mô-đun của bạn sẽ được đưa vào.

Sử dụng mô-đun
--------------

Giờ bạn có thể sử dụng mô-đun mới tạo từ bất kỳ script nào:

.. tabs::
 .. code-tab:: gdscript GDScript

    var s = Summator.new()
    s.add(10)
    s.add(20)
    s.add(30)
    print(s.get_total())
    s.reset()

Kết quả sẽ là ``60``.

.. seealso:: Ví dụ Summator trước đó rất phù hợp cho các mô-đun nhỏ, tùy chỉnh, nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy tham khảo
  :ref:`doc_binding_to_external_libraries` for details about binding to
  các thư viện bên ngoài.

.. warning:: Nếu mô-đun của bạn được dùng từ project đang chạy (không chỉ từ editor), bạn cũng phải biên dịch lại mọi export template dự định sử dụng, sau đó chỉ định đường dẫn đến template tùy chỉnh trong từng export preset. Nếu không, bạn sẽ gặp lỗi khi chạy project vì mô-đun chưa được biên dịch trong export template. Xem các trang :ref:`Biên dịch <toc-devel-compiling>` để biết thêm thông tin.

Biên dịch mô-đun bên ngoài
--------------------------

Việc biên dịch một module bao gồm việc di chuyển mã nguồn của module trực tiếp vào thư mục ``modules/`` của engine. Mặc dù đây là cách đơn giản nhất để biên dịch một module, có một vài lý do khiến việc này có thể không thực tế:

1. Bạn phải sao chép thủ công mã nguồn module mỗi khi muốn biên dịch engine có hoặc không có module, hoặc thực hiện thêm các bước cần thiết để tắt thủ công một module trong quá trình biên dịch bằng một build option tương tự ``module_summator_enabled=no``. Tạo symbolic link cũng có thể là một giải pháp, nhưng bạn có thể cần xử lý thêm các hạn chế của hệ điều hành, chẳng hạn như yêu cầu quyền symbolic link nếu thực hiện việc này bằng script.

2. Tùy vào việc bạn có phải làm việc với mã nguồn của engine hay không, các file module được thêm trực tiếp vào ``modules/`` sẽ làm thay đổi working tree đến mức việc sử dụng VCS (chẳng hạn ``git``) trở nên bất tiện, vì bạn cần đảm bảo chỉ mã liên quan đến engine được commit bằng cách lọc các thay đổi.

Vì vậy, nếu bạn thấy cần có cấu trúc độc lập cho các module tùy chỉnh, hãy lấy module "summator" của chúng ta và di chuyển nó vào thư mục cha của engine:

.. code-block:: shell

    mkdir ../modules
    mv modules/summator ../modules

Biên dịch engine cùng với module của chúng ta bằng cách cung cấp build option ``custom_modules``, nhận vào danh sách đường dẫn thư mục chứa các module C++ tùy chỉnh, được phân tách bằng dấu phẩy, tương tự như sau:

.. code-block:: shell

    scons custom_modules=../modules

Hệ thống build sẽ phát hiện tất cả module bên trong thư mục ``../modules`` và biên dịch chúng tương ứng, bao gồm cả module "summator" của chúng ta.

.. warning::

    Mọi đường dẫn được truyền vào ``custom_modules`` sẽ được chuyển đổi nội bộ thành đường dẫn tuyệt đối để phân biệt giữa các module tùy chỉnh và module dựng sẵn. Điều này có nghĩa là những việc như tạo tài liệu module có thể phụ thuộc vào cấu trúc đường dẫn cụ thể trên máy của bạn.

.. seealso::

    :ref:`Giới thiệu về hệ thống build - build option cho module tùy chỉnh <doc_buildsystem_custom_modules>`.

Tùy chỉnh việc khởi tạo các kiểu của module
-------------------------------------------

Các module có thể tương tác với những class engine dựng sẵn khác trong runtime và thậm chí ảnh hưởng đến cách các kiểu cốt lõi được khởi tạo. Cho đến nay, chúng ta đã sử dụng ``register_summator_types`` để đưa các class của module vào và cung cấp chúng trong engine.

Có thể tóm tắt thứ tự thiết lập cơ bản của engine bằng danh sách các phương thức đăng ký kiểu sau:

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

Class ``Summator`` của chúng ta được khởi tạo trong lệnh gọi ``register_module_types()``. Hãy hình dung rằng chúng ta cần đáp ứng một dependency runtime phổ biến của module (chẳng hạn singleton), hoặc cho phép ghi đè các callback phương thức hiện có của engine trước khi chính engine gán chúng. Trong trường hợp đó, chúng ta muốn đảm bảo các class của module được đăng ký *trước* bất kỳ kiểu dựng sẵn nào khác.

Đây là nơi chúng ta có thể định nghĩa một phương thức ``preregister_summator_types()`` tùy chọn, phương thức này sẽ được gọi trước mọi thứ khác trong giai đoạn thiết lập engine ``preregister_module_types()``.

Bây giờ chúng ta cần thêm phương thức này vào các file header và source của ``register_types``:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #define MODULE_SUMMATOR_HAS_PREREGISTER
    void preregister_summator_types();

    void register_summator_types();
    void unregister_summator_types();

.. note:: Không giống các phương thức đăng ký khác, chúng ta phải định nghĩa ``MODULE_SUMMATOR_HAS_PREREGISTER`` một cách tường minh để cho hệ thống build biết những lệnh gọi phương thức liên quan nào cần được đưa vào lúc biên dịch. Tên của module cũng phải được chuyển thành chữ hoa.

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.cpp

    #include "register_types.h"

    #include "core/object/class_db.h"
    #include "summator.h"

    void preregister_summator_types() {
        // Được gọi trước khi bất kỳ kiểu cốt lõi nào khác được đăng ký.
        // Không có gì cần thực hiện trong ví dụ này.
    }

    void register_summator_types() {
        ClassDB::register_class<Summator>();
    }

    void unregister_summator_types() {
       // Không có gì cần thực hiện trong ví dụ này.
    }

Viết tài liệu tùy chỉnh
-----------------------

Viết tài liệu có vẻ là một công việc nhàm chán, nhưng rất nên ghi lại tài liệu cho module mới tạo để người dùng dễ tận dụng nó hơn. Chưa kể code bạn viết một năm trước có thể trở nên không thể phân biệt với code do người khác viết, vì vậy hãy đối xử tốt với chính mình trong tương lai!

Có một số bước để thiết lập tài liệu tùy chỉnh cho module:

1. Tạo một thư mục mới trong thư mục gốc của module. Tên thư mục có thể là bất kỳ tên nào, nhưng trong suốt phần này, chúng ta sẽ sử dụng tên ``doc_classes``.

2. Bây giờ, chúng ta cần chỉnh sửa ``config.py``, thêm đoạn mã sau:

   .. code-block:: python

        def get_doc_path():
            return "doc_classes"

        def get_doc_classes():
            return [
                "Summator",
            ]

Hàm ``get_doc_path()`` được hệ thống build sử dụng để xác định vị trí của tài liệu. Trong trường hợp này, tài liệu sẽ nằm trong thư mục ``modules/summator/doc_classes``. Nếu bạn không định nghĩa hàm này, đường dẫn tài liệu cho module sẽ quay về thư mục ``doc/classes`` chính.

Phương thức ``get_doc_classes()`` cần thiết để hệ thống build biết những class đã đăng ký nào thuộc về module. Bạn cần liệt kê tất cả class của mình tại đây. Các class không được liệt kê sẽ nằm trong thư mục ``doc/classes`` chính.

.. tip::

    Bạn có thể sử dụng Git để kiểm tra xem mình có bỏ sót class nào không bằng cách kiểm tra các file chưa được theo dõi với ``git status``. Ví dụ:

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

Chúng ta có thể thực hiện việc này bằng cách chạy doctool của Godot, tức ``godot --doctool <path>``, công cụ này sẽ xuất tài liệu tham khảo API của engine vào ``<path>`` được chỉ định ở định dạng XML.

Trong trường hợp của chúng ta, chúng ta sẽ trỏ nó đến thư mục gốc của repository đã clone. Bạn có thể trỏ nó đến một thư mục khác rồi chỉ sao chép các file cần thiết sang đó.

Chạy lệnh:

::

    bin/<godot_binary> --doctool .

Bây giờ, nếu đi đến thư mục ``godot/modules/summator/doc_classes``, bạn sẽ thấy thư mục này chứa file ``Summator.xml`` hoặc bất kỳ class nào khác được bạn tham chiếu trong hàm ``get_doc_classes``.

Chỉnh sửa các file theo `hướng dẫn tham khảo class <https://docs.godotengine.org/en/latest/engine_details/class_reference/index.html>`__ rồi biên dịch lại engine.

Sau khi quá trình biên dịch hoàn tất, tài liệu sẽ có thể truy cập trong hệ thống tài liệu tích hợp sẵn của engine.

Để cập nhật tài liệu, từ nay bạn chỉ cần sửa một trong các file XML rồi biên dịch lại engine.

Nếu bạn thay đổi API của module, bạn cũng có thể trích xuất lại tài liệu; chúng sẽ chứa những nội dung bạn đã thêm trước đó. Tất nhiên, nếu bạn trỏ đến thư mục godot của mình, hãy đảm bảo không làm mất công việc bằng cách trích xuất tài liệu cũ từ một bản build engine cũ lên trên tài liệu mới.

Lưu ý rằng nếu bạn không có quyền ghi vào ``<path>`` đã cung cấp, bạn có thể gặp lỗi tương tự như sau:

.. code-block:: console

    ERROR: Can't write doc file: docs/doc/classes/@GDScript.xml
       At: editor/doc/doc_data.cpp:956

.. _doc_custom_module_unit_tests:

Viết unit test tùy chỉnh
------------------------

Có thể viết các unit test độc lập trong một module C++. Nếu bạn chưa quen với quy trình unit testing trong Godot, vui lòng tham khảo
:ref:`doc_unit_testing`.

Quy trình như sau:

1. Tạo một thư mục mới có tên ``tests/`` trong thư mục gốc của module:

.. code-block:: console

    cd modules/summator
    mkdir tests
    cd tests

2. Tạo một test suite mới: ``test_summator.h``. Tên header phải bắt đầu bằng ``test_`` để hệ thống build có thể thu thập nó và đưa nó vào ``tests/test_main.cpp``, nơi các test được chạy.

3. Viết một số test case. Sau đây là một ví dụ:

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

    } // không gian tên TestSummator

4. Biên dịch engine với ``scons tests=yes``, rồi chạy các test bằng lệnh sau:

.. code-block:: console

    ./bin/<godot_binary> --test --source-file="*test_summator*" --success

Bây giờ bạn sẽ thấy các assertion đã vượt qua.

.. _doc_custom_module_icons:

Thêm biểu tượng editor tùy chỉnh
--------------------------------

Tương tự như việc bạn có thể viết tài liệu độc lập trong một module, bạn cũng có thể tạo các biểu tượng tùy chỉnh riêng cho những class xuất hiện trong editor.

Để biết quy trình tạo biểu tượng editor thực tế và tích hợp chúng vào engine, trước tiên hãy tham khảo :ref:`doc_editor_icons`.

Sau khi tạo xong (các) biểu tượng, hãy thực hiện các bước sau:

1. Tạo một thư mục mới trong thư mục gốc của module, có tên ``icons``. Đây là đường dẫn mặc định để engine tìm các biểu tượng editor của module.

2. Di chuyển các biểu tượng ``svg`` mới tạo (đã tối ưu hoặc chưa) vào thư mục đó.

3. Biên dịch lại engine và chạy editor. Bây giờ (các) biểu tượng sẽ xuất hiện trong giao diện editor ở những vị trí phù hợp.

Nếu muốn lưu các biểu tượng ở nơi khác trong module, hãy thêm đoạn mã sau vào ``config.py`` để ghi đè đường dẫn mặc định:

   .. code-block:: python

       def get_icons_path():
           return "path/to/icons"

Tóm tắt
-------

Hãy nhớ:

-  Sử dụng macro ``GDCLASS`` cho việc kế thừa để Godot có thể bao bọc nó.
-  Sử dụng ``_bind_methods`` để liên kết các hàm của bạn với scripting và cho phép chúng hoạt động như callback cho các signal.
-  **Tránh đa kế thừa đối với các class được expose cho Godot**, vì ``GDCLASS`` không hỗ trợ điều này. Bạn vẫn có thể sử dụng đa kế thừa trong các class của riêng mình miễn là chúng không được expose cho scripting API của Godot.

Nhưng đó chưa phải là tất cả; tùy vào việc bạn làm, bạn sẽ gặp một số điều bất ngờ (hy vọng là tích cực).

-  Nếu kế thừa từ :ref:`class_Node` (hoặc bất kỳ kiểu node dẫn xuất nào, chẳng hạn như Sprite2D), class mới của bạn sẽ xuất hiện trong editor, trong cây kế thừa của hộp thoại "Add Node".
-  Nếu kế thừa từ :ref:`class_Resource`, nó sẽ xuất hiện trong danh sách resource và tất cả các thuộc tính được expose có thể được serialize khi lưu/tải.
-  Theo cùng logic này, bạn có thể mở rộng Editor và gần như mọi khu vực của engine.
