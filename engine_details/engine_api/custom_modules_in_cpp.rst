.. _doc_custom_modules_in_cpp:

Các module tùy chỉnh trong C++
==============================

Module
------

Godot cho phép mở rộng engine theo cách thức module hóa. Bạn có thể tạo các module mới rồi bật/tắt chúng. Điều này cho phép bổ sung chức năng mới cho engine ở mọi cấp độ mà không cần sửa đổi phần lõi, vốn có thể được tách ra để sử dụng và tái sử dụng trong các module khác nhau.

Các module nằm trong thư mục con ``modules/`` của hệ thống build. Theo mặc định, hàng chục module được bật, chẳng hạn như GDScript (đúng vậy, nó không thuộc engine cơ sở), hỗ trợ GridMap, module regular expressions và nhiều module khác. Bạn có thể tạo và kết hợp bao nhiêu module mới tùy ý. Hệ thống build SCons sẽ xử lý việc này một cách minh bạch.

Dùng để làm gì?
---------------

Mặc dù khuyến nghị viết phần lớn game bằng scripting (vì cách này tiết kiệm rất nhiều thời gian), bạn hoàn toàn có thể sử dụng C++ thay thế. Việc thêm các module C++ có thể hữu ích trong những trường hợp sau:

-  - Binding một thư viện bên ngoài vào Godot (như PhysX, FMOD, v.v.).
- Tối ưu các phần quan trọng của game.
- Thêm chức năng mới cho engine và/hoặc editor.
- Port một game hiện có sang Godot.
- Viết toàn bộ một game mới bằng C++ vì bạn không thể sống thiếu C++.


.. note::

    Mặc dù có thể sử dụng module cho logic tùy chỉnh của game,
    :ref:`GDExtension <doc_gdextension>` is generally more suited as it doesn't
    bạn sẽ phải biên dịch lại engine sau mỗi lần thay đổi code.

    Các module C++ chủ yếu cần thiết khi GDExtension không đáp ứng đủ và cần tích hợp sâu hơn với engine.

.. _doc_creating_custom_modules_in_cpp:

Tạo module mới
--------------

Trước khi tạo module, hãy đảm bảo rằng :ref:`download the source code of Godot and compile it <toc-devel-compiling>`.

Để tạo một module mới, bước đầu tiên là tạo một thư mục bên trong ``modules/``. Nếu muốn duy trì module riêng biệt, bạn có thể checkout một VCS khác vào modules và sử dụng nó.

Module ví dụ sẽ được gọi là "summator" (``godot/modules/summator``). Bên trong đó, chúng ta sẽ tạo một class summator:

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

Tiếp theo là file cpp.

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

Tiếp theo, class mới cần được đăng ký theo một cách nào đó, vì vậy cần tạo thêm hai file:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các file này phải nằm trong thư mục cấp cao nhất của module (cạnh các file ``SCsub`` và ``config.py`` của bạn) để module được đăng ký đúng cách.

Các file này cần chứa nội dung sau:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #include "modules/register_module_types.h"

    void initialize_summator_module(ModuleInitializationLevel p_level);
    void uninitialize_summator_module(ModuleInitializationLevel p_level);
    /* đúng vậy, từ ở giữa phải giống với tên thư mục của module */

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

Tiếp theo, chúng ta cần tạo một file ``SCsub`` để hệ thống build biên dịch module này:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    # SCsub

    Import('env')

    env.add_source_files(env.modules_sources, "*.cpp") # Thêm tất cả file cpp vào build

Với nhiều source, bạn cũng có thể thêm từng file riêng lẻ vào một Python string list:

.. code-block:: python

    src_list = ["summator.cpp", "other.cpp", "etc.cpp"]
    env.add_source_files(env.modules_sources, src_list)

Điều này cho phép thực hiện những khả năng mạnh mẽ bằng cách sử dụng Python để xây dựng danh sách file thông qua các vòng lặp và câu lệnh logic. Hãy xem một số module được cung cấp mặc định cùng Godot để tham khảo ví dụ.

Để thêm các thư mục include mà compiler sẽ tìm kiếm, bạn có thể nối chúng vào các path của environment:

.. code-block:: python

    env.Append(CPPPATH=["mylib/include"]) # đây là một path tương đối
    env.Append(CPPPATH=["#myotherlib/include"]) # đây là một path 'tuyệt đối'

Nếu muốn thêm các compiler flag tùy chỉnh khi build module, trước tiên bạn cần clone ``env``, để các flag đó không được thêm vào toàn bộ Godot build (điều này có thể gây lỗi). Ví dụ ``SCsub`` với các flag tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/summator/SCsub

    Import('env')

    module_env = env.Clone()
    module_env.add_source_files(env.modules_sources, "*.cpp")
    # Nối các flag CCFLAGS cho cả code C và C++.
    module_env.Append(CCFLAGS=['-O2'])
    # Nếu cần, bạn có thể:
    # - Nối CFLAGS chỉ cho code C.
    # - Nối CXXFLAGS chỉ cho code C++.

Cuối cùng là file cấu hình cho module; đây là một Python script phải được đặt tên là ``config.py``:

.. code-block:: python
    :caption: godot/modules/summator/config.py

    # config.py

    def can_build(env, platform):
        return True

    def configure(env):
        pass

Module sẽ được hỏi xem có thể build cho platform cụ thể hay không (trong trường hợp này, ``True`` có nghĩa là nó sẽ build cho mọi platform).

Vậy là xong. Hy vọng mọi thứ không quá phức tạp! Module của bạn sẽ có dạng như sau:

.. code-block:: none

    godot/modules/summator/config.py
    godot/modules/summator/summator.h
    godot/modules/summator/summator.cpp
    godot/modules/summator/register_types.h
    godot/modules/summator/register_types.cpp
    godot/modules/summator/SCsub

Sau đó, bạn có thể zip module và chia sẻ với mọi người. Khi build cho mọi platform (theo hướng dẫn trong các phần trước), module của bạn sẽ được đưa vào.

Sử dụng module
--------------

Giờ bạn có thể sử dụng module vừa tạo từ bất kỳ script nào:

.. tabs::
 .. code-tab:: gdscript GDScript

    var s = Summator.new()
    s.add(10)
    s.add(20)
    s.add(30)
    print(s.get_total())
    s.reset()

Kết quả sẽ là ``60``.

.. seealso:: The previous Summator example is great for small, custom modules,
  nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy tham khảo
  :ref:`doc_binding_to_external_libraries` for details about binding to
  các thư viện bên ngoài.

.. warning:: If your module is meant to be accessed from the running project
             (không chỉ từ editor), bạn cũng phải biên dịch lại mọi export template mà bạn dự định sử dụng, sau đó chỉ định path đến template tùy chỉnh trong từng export preset. Nếu không, bạn sẽ gặp lỗi khi chạy project vì module chưa được biên dịch trong export template. Xem các trang :ref:`Compiling <toc-devel-compiling>` để biết thêm thông tin.

Biên dịch module bên ngoài
--------------------------

Việc biên dịch một module bao gồm di chuyển trực tiếp source của module vào thư mục ``modules/`` của engine. Mặc dù đây là cách đơn giản nhất để biên dịch module, có một vài lý do khiến việc này có thể không thực tế:

1. Bạn phải sao chép thủ công source của module mỗi khi muốn biên dịch engine có hoặc không có module, hoặc phải thực hiện thêm các bước để vô hiệu hóa module thủ công trong quá trình biên dịch bằng một build option tương tự ``module_summator_enabled=no``. Tạo symbolic link cũng có thể là một giải pháp, nhưng bạn có thể cần xử lý thêm các hạn chế của OS, chẳng hạn như yêu cầu quyền symbolic link nếu thực hiện việc này qua script.

2. Tùy vào việc bạn có phải làm việc với source code của engine hay không, các file module được thêm trực tiếp vào ``modules/`` sẽ thay đổi working tree đến mức việc sử dụng VCS (như ``git``) trở nên bất tiện, vì bạn cần đảm bảo chỉ commit code liên quan đến engine bằng cách lọc các thay đổi.

Vì vậy, nếu bạn cảm thấy cần có cấu trúc độc lập cho các module tùy chỉnh, hãy lấy module "summator" của chúng ta và chuyển nó đến thư mục cha của engine:

.. code-block:: shell

    mkdir ../modules
    mv modules/summator ../modules

Biên dịch engine cùng module của chúng ta bằng cách cung cấp build option ``custom_modules``, option này nhận một danh sách phân tách bằng dấu phẩy gồm các path thư mục chứa các module C++ tùy chỉnh, tương tự như sau:

.. code-block:: shell

    scons custom_modules=../modules

Hệ thống build sẽ phát hiện tất cả module bên dưới thư mục ``../modules`` và biên dịch chúng tương ứng, bao gồm module "summator" của chúng ta.

.. warning::

    Mọi path được truyền vào ``custom_modules`` sẽ được chuyển đổi nội bộ thành path tuyệt đối để phân biệt giữa module tùy chỉnh và module tích hợp sẵn. Điều này có nghĩa là những việc như tạo tài liệu module có thể phụ thuộc vào một cấu trúc path cụ thể trên máy của bạn.

.. seealso::

    :ref:`Introduction to the buildsystem - Custom modules build option <doc_buildsystem_custom_modules>`.

Tùy chỉnh việc khởi tạo các loại module
---------------------------------------

Các module có thể tương tác với những class engine tích hợp sẵn khác trong runtime và thậm chí ảnh hưởng đến cách các core type được khởi tạo. Cho đến nay, chúng ta đã sử dụng ``register_summator_types`` để đưa các class của module vào engine và giúp chúng khả dụng.

Có thể tóm tắt sơ lược thứ tự thiết lập engine bằng danh sách các phương thức đăng ký type sau:

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

Class ``Summator`` của chúng ta được khởi tạo trong lần gọi ``register_module_types()``. Hãy tưởng tượng chúng ta cần đáp ứng một dependency runtime chung của module (như singleton), hoặc cho phép override các callback của method engine hiện có trước khi chính engine gán chúng. Trong trường hợp đó, chúng ta muốn đảm bảo các class của module được đăng ký *trước* mọi built-in type khác.

Đây là nơi chúng ta có thể định nghĩa một method ``preregister_summator_types()`` tùy chọn, method này sẽ được gọi trước mọi thứ khác trong giai đoạn thiết lập engine ``preregister_module_types()``.

Bây giờ chúng ta cần thêm method này vào các file header và source của ``register_types``:

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.h

    #define MODULE_SUMMATOR_HAS_PREREGISTER
    void preregister_summator_types();

    void register_summator_types();
    void unregister_summator_types();

.. note:: Unlike other register methods, we have to explicitly define
          ``MODULE_SUMMATOR_HAS_PREREGISTER`` để cho hệ thống build biết những lời gọi method liên quan cần được đưa vào lúc compile. Tên module cũng phải được chuyển thành chữ hoa.

.. code-block:: cpp
    :caption: godot/modules/summator/register_types.cpp

    #include "register_types.h"

    #include "core/object/class_db.h"
    #include "summator.h"

    void preregister_summator_types() {
        // Được gọi trước khi bất kỳ core type nào khác được đăng ký.
        // Không cần làm gì ở đây trong ví dụ này.
    }

    void register_summator_types() {
        ClassDB::register_class<Summator>();
    }

    void unregister_summator_types() {
       // Không cần làm gì ở đây trong ví dụ này.
    }

Viết tài liệu tùy chỉnh
-----------------------

Viết tài liệu có vẻ là một công việc nhàm chán, nhưng bạn rất nên ghi lại tài liệu cho module mới tạo để người dùng dễ dàng hưởng lợi từ nó hơn. Chưa kể code bạn viết một năm trước có thể trở nên không thể phân biệt với code do người khác viết, vì vậy hãy tử tế với chính mình trong tương lai!

Có một số bước để thiết lập tài liệu tùy chỉnh cho module:

1. Tạo một thư mục mới trong thư mục gốc của module. Tên thư mục có thể là bất kỳ tên nào, nhưng trong suốt phần này, chúng ta sẽ sử dụng tên ``doc_classes``.

2. Bây giờ, chúng ta cần chỉnh sửa ``config.py`` và thêm đoạn sau:

   .. code-block:: python

        def get_doc_path():
            return "doc_classes"

        def get_doc_classes():
            return [
                "Summator",
            ]

Hàm ``get_doc_path()`` được hệ thống build sử dụng để xác định vị trí của tài liệu. Trong trường hợp này, tài liệu sẽ nằm trong thư mục ``modules/summator/doc_classes``. Nếu không định nghĩa hàm này, doc path cho module của bạn sẽ quay về thư mục ``doc/classes`` chính.

Phương thức ``get_doc_classes()`` cần thiết để hệ thống build biết những class đã đăng ký nào thuộc về module. Bạn cần liệt kê tất cả class của mình tại đây. Những class không được liệt kê sẽ nằm trong thư mục ``doc/classes`` chính.

.. tip::

    Bạn có thể dùng Git để kiểm tra xem mình có bỏ sót class nào không bằng cách kiểm tra các file chưa được theo dõi với ``git status``. Ví dụ:

    ::

        git status

    Kết quả đầu ra ví dụ:

    ::

        Untracked files:
            (use "git add <file>..." to include in what will be committed)

            doc/classes/MyClass2D.xml
            doc/classes/MyClass4D.xml
            doc/classes/MyClass5D.xml
            doc/classes/MyClass6D.xml
            ...


3. Bây giờ chúng ta có thể tạo documentation:

Bạn có thể thực hiện việc này bằng cách chạy doctool của Godot, tức là ``godot --doctool <path>``, lệnh này sẽ xuất tài liệu tham chiếu API của engine vào ``<path>`` đã cho ở định dạng XML.

Trong trường hợp của chúng ta, hãy trỏ nó đến thư mục gốc của repository đã clone. Bạn có thể trỏ nó đến một thư mục khác và chỉ sao chép các file cần thiết sang đó.

Chạy lệnh:

::

    bin/<godot_binary> --doctool .

Bây giờ, nếu bạn đi đến thư mục ``godot/modules/summator/doc_classes``, bạn sẽ thấy thư mục này chứa file ``Summator.xml``, hoặc bất kỳ class nào khác mà bạn đã tham chiếu trong hàm ``get_doc_classes``.

Chỉnh sửa các file theo `class reference primer <https://docs.godotengine.org/en/latest/engine_details/class_reference/index.html>`__ rồi biên dịch lại engine.

Sau khi quá trình biên dịch hoàn tất, tài liệu sẽ có thể được truy cập trong hệ thống documentation tích hợp sẵn của engine.

Để giữ cho documentation luôn được cập nhật, từ giờ bạn chỉ cần sửa đổi một trong các file XML rồi biên dịch lại engine.

Nếu bạn thay đổi API của module, bạn cũng có thể trích xuất lại docs; chúng sẽ chứa những nội dung bạn đã thêm trước đó. Tất nhiên, nếu trỏ đến thư mục godot của mình, hãy đảm bảo bạn không làm mất công việc bằng cách trích xuất docs cũ từ một bản build engine cũ lên trên các docs mới hơn.

Lưu ý rằng nếu bạn không có quyền ghi vào ``<path>`` đã cung cấp, bạn có thể gặp lỗi tương tự như sau:

.. code-block:: console

    ERROR: Can't write doc file: docs/doc/classes/@GDScript.xml
       At: editor/doc/doc_data.cpp:956

.. _doc_custom_module_unit_tests:

Viết unit test tùy chỉnh
------------------------

Bạn có thể viết các unit test độc lập như một phần của module C++. Nếu bạn chưa quen với quy trình unit testing trong Godot, vui lòng tham khảo
:ref:`doc_unit_testing`.

Quy trình như sau:

1. Tạo một thư mục mới có tên ``tests/`` bên dưới thư mục gốc của module:

.. code-block:: console

    cd modules/summator
    mkdir tests
    cd tests

2. Tạo một test suite mới: ``test_summator.h``. Tên header phải có tiền tố ``test_`` để hệ thống build có thể thu thập nó và đưa nó vào ``tests/test_main.cpp``, nơi các test được chạy.

3. Viết một số test case. Đây là một ví dụ:

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

4. Biên dịch engine với ``scons tests=yes``, rồi chạy các test bằng lệnh sau:

.. code-block:: console

    ./bin/<godot_binary> --test --source-file="*test_summator*" --success

Bây giờ bạn sẽ thấy các assertion đã đạt.

.. _doc_custom_module_icons:

Thêm icon editor tùy chỉnh
--------------------------

Tương tự như việc bạn có thể viết documentation độc lập bên trong một module, bạn cũng có thể tạo icon tùy chỉnh riêng cho các class để hiển thị trong editor.

Để biết quy trình thực tế tạo icon editor và tích hợp chúng vào engine, trước tiên hãy tham khảo :ref:`doc_editor_icons`.

Sau khi tạo xong icon, hãy thực hiện các bước sau:

1. Tạo một thư mục mới trong thư mục gốc của module có tên ``icons``. Đây là đường dẫn mặc định để engine tìm icon editor của module.

2. Di chuyển các icon ``svg`` mới tạo (đã tối ưu hoặc chưa) vào thư mục đó.

3. Biên dịch lại engine và chạy editor. Bây giờ các icon sẽ xuất hiện trong giao diện editor ở những nơi phù hợp.

Nếu muốn lưu icon ở nơi khác trong module, hãy thêm đoạn code sau vào ``config.py`` để ghi đè đường dẫn mặc định:

   .. code-block:: python

       def get_icons_path():
           return "path/to/icons"

Tổng kết
--------

Hãy nhớ:

-  Dùng macro ``GDCLASS`` cho inheritance để Godot có thể wrap nó. - Dùng ``_bind_methods`` để bind các function vào scripting và cho phép chúng hoạt động như callback cho signal. - **Tránh multiple inheritance đối với các class được expose cho Godot**, vì ``GDCLASS`` không hỗ trợ điều này. Bạn vẫn có thể sử dụng multiple inheritance trong các class của riêng mình miễn là chúng không được expose cho scripting API của Godot.

Tuy nhiên, đây chưa phải là tất cả; tùy vào những gì bạn thực hiện, bạn sẽ gặp một số điều bất ngờ (hy vọng là tích cực).

-  Nếu bạn kế thừa từ :ref:`class_Node` (hoặc bất kỳ kiểu node dẫn xuất nào, chẳng hạn như Sprite2D), class mới của bạn sẽ xuất hiện trong editor, trong cây inheritance của hộp thoại "Add Node". - Nếu bạn kế thừa từ :ref:`class_Resource`, nó sẽ xuất hiện trong danh sách resource, và tất cả property được expose có thể được serialize khi lưu/tải. - Với cùng logic này, bạn có thể mở rộng Editor và gần như mọi khu vực của engine.
