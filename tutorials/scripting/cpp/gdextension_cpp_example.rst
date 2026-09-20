.. _doc_godot_cpp_getting_started:

Bắt đầu
=======

Tổng quan về quy trình làm việc
-------------------------------

Với vai trò là một GDExtension, godot-cpp phức tạp hơn khi sử dụng so với :ref:`GDScript <doc_gdscript>` và :ref:`C# <doc_c_sharp>`. Nếu bạn quyết định làm việc với nó, sau đây là những gì bạn có thể mong đợi trong quy trình làm việc của mình:

* Tạo một dự án godot-cpp mới (từ `template <https://github.com/godotengine/godot-cpp-template>`__ hoặc từ đầu, như giải thích bên dưới). * Phát triển mã của bạn với :ref:`favorite IDE <toc-devel-configuring_an_ide>` cục bộ. * Build và kiểm thử mã của bạn bằng phiên bản Godot tương thích sớm nhất. * Tạo bản build cho tất cả các nền tảng bạn muốn hỗ trợ (ví dụ: sử dụng `GitHub Actions <https://github.com/godotengine/godot-cpp-template/blob/main/.github/workflows/make_build.yml>`__). * Tùy chọn: Phát hành trên `Godot Asset Store <https://store.godotengine.org/>`__.

Dự án ví dụ
-----------

Đối với dự án godot-cpp đầu tiên, chúng tôi khuyên bạn nên bắt đầu với hướng dẫn này để hiểu công nghệ liên quan đến godot-cpp. Sau khi hoàn tất, bạn có thể sử dụng `godot-cpp template <https://github.com/godotengine/godot-cpp-template>`__, vốn hỗ trợ nhiều tính năng hơn, chẳng hạn như pipeline GitHub action và mã boilerplate hữu ích của ``SConstruct``. Tuy nhiên, template này không tự giải thích với mức độ chi tiết cao, đó là lý do chúng tôi khuyên bạn nên xem qua hướng dẫn này trước.

Thiết lập dự án
---------------

Bạn sẽ cần một số điều kiện tiên quyết sau:

- Một executable Godot 4. - Một trình biên dịch C++. - SCons làm công cụ build. - Một bản sao của `godot-cpp repository <https://github.com/godotengine/godot-cpp>`__.

Xem thêm :ref:`Configuring an IDE <toc-devel-configuring_an_ide>` và :ref:`Compiling <toc-devel-compiling>`, vì các công cụ build này giống hệt những công cụ bạn cần để biên dịch Godot từ mã nguồn.

Bạn có thể tải `godot-cpp repository <https://github.com/godotengine/godot-cpp>`__ từ GitHub hoặc để Git thực hiện công việc đó. Lưu ý rằng repository này có các branch khác nhau cho những phiên bản Godot khác nhau. GDExtension sẽ không hoạt động trong các phiên bản Godot cũ hơn (chỉ từ Godot 4 trở lên) và ngược lại, vì vậy hãy đảm bảo bạn tải đúng branch.

.. note::
    Để sử dụng `GDExtension <https://godotengine.org/article/introducing-gd-extensions>`__, bạn cần sử dụng branch godot-cpp khớp với phiên bản Godot mà bạn nhắm đến. Ví dụ, nếu bạn nhắm đến Godot 4.1, hãy sử dụng branch ``4.1``. Trong suốt hướng dẫn này, chúng tôi sử dụng ``4.x``, và bạn cần thay thế bằng phiên bản Godot mà mình nhắm đến.

    Branch ``master`` là branch phát triển, được cập nhật thường xuyên để hoạt động với branch ``master`` của Godot.

.. warning::
    GDExtension nhắm đến một phiên bản Godot cũ hơn sẽ hoạt động trong các phiên bản minor mới hơn, nhưng không ngược lại. Ví dụ, GDExtension nhắm đến Godot 4.2 sẽ hoạt động bình thường trong Godot 4.3, nhưng GDExtension nhắm đến Godot 4.3 sẽ không hoạt động trong Godot 4.2.

    Có một ngoại lệ: các extension nhắm đến Godot 4.0 **sẽ không** hoạt động với Godot 4.1 trở lên (xem :ref:`updating_your_gdextension_for_godot_4_1`).

Nếu bạn quản lý phiên bản dự án bằng Git, bạn nên thêm nó dưới dạng Git submodule:

.. code-block:: none

    mkdir gdextension_cpp_example
    cd gdextension_cpp_example
    git init
    git submodule add -b 4.x https://github.com/godotengine/godot-cpp
    cd godot-cpp
    git submodule update --init

Ngoài ra, bạn cũng có thể clone nó vào thư mục dự án:

.. code-block:: none

    mkdir gdextension_cpp_example
    cd gdextension_cpp_example
    git clone -b 4.x https://github.com/godotengine/godot-cpp

.. note::

    Nếu bạn quyết định tải repository hoặc clone nó vào thư mục của mình, hãy đảm bảo giữ nguyên bố cục thư mục như chúng tôi đã thiết lập ở đây. Phần lớn mã mà chúng tôi giới thiệu trong hướng dẫn này giả định dự án có bố cục đó.

Nếu bạn clone ví dụ từ liên kết được nêu trong phần giới thiệu, các submodule sẽ không được tự động khởi tạo. Bạn sẽ cần thực thi các lệnh sau:

.. code-block:: none

    cd gdextension_cpp_example
    git submodule update --init

Lệnh này sẽ khởi tạo repository trong thư mục dự án của bạn.

Tạo một plugin đơn giản
-----------------------

Bây giờ là lúc build một plugin thực tế. Chúng ta sẽ bắt đầu bằng cách tạo một dự án Godot trống, trong đó sẽ đặt một vài tệp.

Mở Godot và tạo một dự án mới. Trong ví dụ này, chúng ta sẽ đặt dự án vào một thư mục có tên ``project`` bên trong cấu trúc thư mục GDExtension của mình.

Trong dự án, chúng ta sẽ tạo một scene chứa một Node có tên "Main" và lưu scene đó dưới dạng ``main.tscn``. Chúng ta sẽ quay lại phần này sau.

Quay lại thư mục module GDExtension cấp cao nhất, chúng ta cũng sẽ tạo một thư mục con có tên ``src`` để đặt các tệp mã nguồn.

Bây giờ bạn sẽ có các thư mục ``project``, ``godot-cpp`` và ``src`` trong module GDExtension của mình.

Cấu trúc thư mục của bạn bây giờ sẽ như sau:

.. code-block:: none

    gdextension_cpp_example/
    |
    +--project/                  # game example/demo để kiểm thử extension
    |
    +--godot-cpp/             # Các binding C++
    |
    +--src/                   # mã nguồn của extension mà chúng ta đang build

Trong thư mục ``src``, chúng ta sẽ bắt đầu bằng cách tạo tệp header cho node GDExtension mà mình sẽ tạo. Chúng ta sẽ đặt tên tệp là ``gdexample.h``:

.. code-block:: cpp
    :caption: gdextension_cpp_example/src/gdexample.h

    #pragma once

    #include <godot_cpp/classes/sprite2d.hpp>

    namespace godot {

    class GDExample : public Sprite2D {
        GDCLASS(GDExample, Sprite2D)

    private:
        double time_passed;

    protected:
        static void _bind_methods();

    public:
        GDExample();
        ~GDExample();

        void _process(double delta) override;
    };

    } // namespace godot

Có một vài điểm cần lưu ý ở phần trên. Chúng ta include ``sprite2d.hpp``, nơi chứa các binding cho class Sprite2D. Chúng ta sẽ mở rộng class này trong module của mình.

Chúng ta sử dụng namespace ``godot``, vì mọi thứ trong GDExtension đều được định nghĩa trong namespace này.

Sau đó là định nghĩa class của chúng ta, kế thừa từ Sprite2D thông qua một container class. Sau này chúng ta sẽ thấy một vài tác động phụ của việc này. Macro ``GDCLASS`` thiết lập một số thành phần nội bộ cho chúng ta.

Tiếp theo, chúng ta khai báo một biến thành viên duy nhất có tên ``time_passed``.

Trong block tiếp theo, nơi định nghĩa các method, chúng ta đã định nghĩa constructor và destructor, nhưng còn hai function khác có lẽ sẽ quen thuộc với một số bạn, cùng một method mới.

Đầu tiên là ``_bind_methods``, một static function mà Godot sẽ gọi để tìm hiểu những method nào có thể được gọi và những property nào được expose. Thứ hai là function ``_process``, hoạt động giống hệt function ``_process`` mà bạn đã quen dùng trong GDScript.

Hãy triển khai các function bằng cách tạo tệp ``gdexample.cpp`` của chúng ta:

.. code-block:: cpp
    :caption: gdextension_cpp_example/src/gdexample.cpp

    #include "gdexample.h"
    #include <godot_cpp/core/class_db.hpp>

    using namespace godot;

    void GDExample::_bind_methods() {
    }

    GDExample::GDExample() {
        // Khởi tạo mọi biến ở đây.
        time_passed = 0.0;
    }

    GDExample::~GDExample() {
        // Thêm phần cleanup của bạn ở đây.
    }

    void GDExample::_process(double delta) {
        time_passed += delta;

        Vector2 new_position = Vector2(10.0 + (10.0 * sin(time_passed * 2.0)), 10.0 + (10.0 * cos(time_passed * 1.5)));

        set_position(new_position);
    }

Phần này khá dễ hiểu. Chúng ta triển khai từng method của class đã định nghĩa trong tệp header.

Lưu ý function ``_process`` của chúng ta, function này theo dõi lượng thời gian đã trôi qua và tính toán vị trí mới cho sprite bằng hàm sine và cosine.

Chúng ta còn cần một tệp C++ nữa; chúng ta sẽ đặt tên là ``register_types.cpp``. Plugin GDExtension của chúng ta có thể chứa nhiều class, mỗi class có header và tệp mã nguồn riêng như ``GDExample`` mà chúng ta đã triển khai ở trên. Bây giờ chúng ta cần một đoạn mã nhỏ để cho Godot biết về tất cả các class trong plugin GDExtension.

.. code-block:: cpp
    :caption: gdextension_cpp_example/src/register_types.cpp

    #include "register_types.h"

    #include "gdexample.h"

    #include <gdextension_interface.h>
    #include <godot_cpp/core/defs.hpp>
    #include <godot_cpp/godot.hpp>

    using namespace godot;

    void initialize_example_module(ModuleInitializationLevel p_level) {
        if (p_level != MODULE_INITIALIZATION_LEVEL_SCENE) {
            return;
        }

        GDREGISTER_CLASS(GDExample);
    }

    void uninitialize_example_module(ModuleInitializationLevel p_level) {
        if (p_level != MODULE_INITIALIZATION_LEVEL_SCENE) {
            return;
        }
    }

    extern "C" {
    // Khởi tạo.
    GDExtensionBool GDE_EXPORT example_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, const GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization) {
        godot::GDExtensionBinding::InitObject init_obj(p_get_proc_address, p_library, r_initialization);

        init_obj.register_initializer(initialize_example_module);
        init_obj.register_terminator(uninitialize_example_module);
        init_obj.set_minimum_library_initialization_level(MODULE_INITIALIZATION_LEVEL_SCENE);

        return init_obj.init();
    }
    }

Các function ``initialize_example_module`` và ``uninitialize_example_module`` lần lượt được gọi khi Godot load plugin của chúng ta và khi unload plugin. Tất cả những gì chúng ta làm ở đây là duyệt qua các function trong module bindings để khởi tạo chúng, nhưng tùy theo nhu cầu, bạn có thể phải thiết lập thêm nhiều thành phần khác. Chúng ta gọi macro ``GDREGISTER_CLASS`` cho mỗi class trong library.

.. note::

    Bạn có thể tìm thông tin về ``GDREGISTER_CLASS`` (và các phương án thay thế) tại :ref:`doc_object_class`.

Function quan trọng là function thứ ba có tên ``example_library_init``. Trước tiên, chúng ta gọi một function trong thư viện bindings để tạo một initialization object. Object này đăng ký các function initialization và termination của GDExtension. Ngoài ra, nó thiết lập level khởi tạo (core, servers, scene, editor, level).

Cuối cùng, chúng ta cần tệp header cho ``register_types.cpp``, có tên ``register_types.h``.

.. code-block:: cpp
    :caption: gdextension_cpp_example/src/register_types.h

    #pragma once

    #include <godot_cpp/core/class_db.hpp>

    using namespace godot;

    void initialize_example_module(ModuleInitializationLevel p_level);
    void uninitialize_example_module(ModuleInitializationLevel p_level);

Biên dịch plugin
----------------

Để biên dịch dự án, chúng ta cần định nghĩa cách SCons biên dịch dự án bằng một tệp ``SConstruct`` tham chiếu đến tệp trong ``godot-cpp``. Việc viết tệp này từ đầu nằm ngoài phạm vi của hướng dẫn, nhưng bạn có thể tải xuống
:download:`the SConstruct file we prepared <files/cpp_example/SConstruct>`.
Chúng tôi sẽ trình bày một ví dụ chi tiết và có khả năng tùy chỉnh cao hơn về cách sử dụng các tệp build này trong một hướng dẫn tiếp theo.

.. note::

    Tệp ``SConstruct`` này được viết để sử dụng với ``godot-cpp`` master mới nhất; bạn có thể cần thực hiện một số thay đổi nhỏ khi sử dụng với các phiên bản cũ hơn hoặc tham khảo tệp ``SConstruct`` trong tài liệu Godot 4.x.

Sau khi tải tệp ``SConstruct``, hãy đặt tệp đó trong cấu trúc thư mục GDExtension cùng cấp với ``godot-cpp``, ``src`` và ``project``, sau đó chạy:

.. code-block:: bash

    scons platform=<platform>

Bạn có thể bỏ tùy chọn ``platform`` nếu đang biên dịch cho nền tảng hiện tại. Danh sách các tùy chọn ``platform`` khả dụng phụ thuộc vào những dependency của nền tảng đã được thiết lập (dùng ``platform=list`` để xem tất cả nền tảng khả dụng). Xem :ref:`doc_introduction_to_the_buildsystem` để biết chi tiết.

Bây giờ bạn có thể tìm thấy library đã biên dịch trong ``project/bin/``.

.. note::

    Ở đây, chúng ta đã biên dịch cả godot-cpp và library gdexample dưới dạng debug build, đây là mặc định. Để tạo optimized build, bạn nên biên dịch chúng bằng tùy chọn ``target=template_release``.

Sử dụng module GDExtension
--------------------------

Trước khi quay lại Godot, chúng ta cần tạo thêm một tệp trong ``project/bin/``.

Tệp này cho Godot biết những thư viện động nào cần được tải trên mỗi nền tảng và hàm entry của module. Tệp này có tên là ``gdexample.gdextension``.

.. code-block:: none

    [configuration]

    entry_symbol = "example_library_init"
    compatibility_minimum = "4.1"
    reloadable = true

    [libraries]

    macos.debug = "./libgdexample.macos.template_debug.dylib"
    macos.release = "./libgdexample.macos.template_release.dylib"
    windows.debug.x86_32 = "./gdexample.windows.template_debug.x86_32.dll"
    windows.release.x86_32 = "./gdexample.windows.template_release.x86_32.dll"
    windows.debug.x86_64 = "./gdexample.windows.template_debug.x86_64.dll"
    windows.release.x86_64 = "./gdexample.windows.template_release.x86_64.dll"
    linux.debug.x86_64 = "./libgdexample.linux.template_debug.x86_64.so"
    linux.release.x86_64 = "./libgdexample.linux.template_release.x86_64.so"
    linux.debug.arm64 = "./libgdexample.linux.template_debug.arm64.so"
    linux.release.arm64 = "./libgdexample.linux.template_release.arm64.so"
    linux.debug.rv64 = "./libgdexample.linux.template_debug.rv64.so"
    linux.release.rv64 = "./libgdexample.linux.template_release.rv64.so"

Tệp này chứa một section ``configuration`` điều khiển hàm entry của module. Bạn cũng nên đặt phiên bản Godot tối thiểu tương thích bằng ``compatibility_minimum``, để ngăn các phiên bản Godot cũ hơn cố tải extension của bạn. Flag ``reloadable`` cho phép editor tự động reload extension mỗi khi bạn recompile nó mà không cần khởi động lại editor. Tính năng này chỉ hoạt động nếu bạn compile extension ở debug mode (mặc định).

Section ``libraries`` là phần quan trọng: nó cho Godot biết vị trí của dynamic library trong filesystem của project trên mỗi nền tảng được hỗ trợ. Section này cũng khiến *chỉ* tệp đó được export khi bạn export project, nghĩa là data pack sẽ không chứa các library không tương thích với nền tảng đích.

Bạn có thể tìm hiểu thêm về các tệp ``.gdextension`` tại :ref:`doc_gdextension_file`.

Dưới đây là một bản tổng quan khác để kiểm tra cấu trúc tệp chính xác:

.. code-block:: none

    gdextension_cpp_example/
    |
    +--project/                  # game example/demo để kiểm thử extension
    |   |
    |   +--main.tscn
    |   |
    |   +--bin/
    |       |
    |       +--gdexample.gdextension
    |
    +--godot-cpp/             # C++ bindings
    |
    +--src/                   # mã nguồn của extension mà chúng ta đang xây dựng
    |   |
    |   +--register_types.cpp
    |   +--register_types.h
    |   +--gdexample.cpp
    |   +--gdexample.h

Bây giờ hãy quay lại Godot. Chúng ta mở scene chính đã tạo từ đầu tutorial, rồi thêm một node GDExample mới khả dụng vào scene:

.. image:: img/gdextension_cpp_nodes.webp

Chúng ta sẽ gán logo Godot làm texture cho node này, rồi tắt property ``centered``:

.. image:: img/gdextension_cpp_sprite.webp

Cuối cùng chúng ta đã sẵn sàng chạy project:

.. video:: img/gdextension_cpp_animated.webm
   :alt: Screen recording of a game window, with Godot logo moving in the top-left corner
   :autoplay:
   :loop:
   :muted:
   :align: default

Thêm properties
---------------

GDScript cho phép bạn thêm properties vào script bằng keyword ``export``. Trong GDExtension, bạn phải register các properties bằng một hàm getter và setter, hoặc triển khai trực tiếp các method ``_get_property_list``, ``_get`` và ``_set`` của một object (nhưng nội dung đó vượt xa phạm vi của tutorial này).

Hãy thêm một property cho phép chúng ta điều khiển amplitude của wave.

Trong tệp ``gdexample.h``, chúng ta cần thêm một member variable cùng các hàm getter và setter:

.. code-block:: cpp

    ...
    private:
        double time_passed;
        double amplitude;

    public:
        void set_amplitude(const double p_amplitude);
        double get_amplitude() const;
    ...

Trong tệp ``gdexample.cpp``, chúng ta cần thực hiện một số thay đổi; chúng ta sẽ chỉ hiển thị các method cuối cùng được thay đổi, vì vậy đừng xóa những dòng bị lược bỏ:

.. code-block:: cpp

    void GDExample::_bind_methods() {
        ClassDB::bind_method(D_METHOD("get_amplitude"), &GDExample::get_amplitude);
        ClassDB::bind_method(D_METHOD("set_amplitude", "p_amplitude"), &GDExample::set_amplitude);

        ADD_PROPERTY(PropertyInfo(Variant::FLOAT, "amplitude"), "set_amplitude", "get_amplitude");
    }

    GDExample::GDExample() {
        // Khởi tạo mọi variable ở đây.
        time_passed = 0.0;
        amplitude = 10.0;
    }

    void GDExample::_process(double delta) {
        time_passed += delta;

        Vector2 new_position = Vector2(
            amplitude + (amplitude * sin(time_passed * 2.0)),
            amplitude + (amplitude * cos(time_passed * 1.5))
        );

        set_position(new_position);
    }

    void GDExample::set_amplitude(const double p_amplitude) {
        amplitude = p_amplitude;
    }

    double GDExample::get_amplitude() const {
        return amplitude;
    }

Sau khi compile module với những thay đổi này, bạn sẽ thấy một property đã được thêm vào interface của chúng ta. Bây giờ bạn có thể thay đổi property này và khi chạy project, bạn sẽ thấy icon Godot di chuyển theo một quỹ đạo lớn hơn.

Hãy làm tương tự cho speed của animation và sử dụng một hàm setter cùng getter. Tệp header ``gdexample.h`` của chúng ta một lần nữa chỉ cần thêm vài dòng code:

.. code-block:: cpp

    ...
        double amplitude;
        double speed;
    ...
        void _process(double delta) override;
        void set_speed(const double p_speed);
        double get_speed() const;
    ...

Việc này cần thêm một số thay đổi vào tệp ``gdexample.cpp``; một lần nữa, chúng ta chỉ hiển thị các method đã thay đổi, vì vậy đừng xóa bất cứ phần nào bị lược bỏ:

.. code-block:: cpp

    void GDExample::_bind_methods() {
        ...
        ClassDB::bind_method(D_METHOD("get_speed"), &GDExample::get_speed);
        ClassDB::bind_method(D_METHOD("set_speed", "p_speed"), &GDExample::set_speed);

        ADD_PROPERTY(PropertyInfo(Variant::FLOAT, "speed", PROPERTY_HINT_RANGE, "0,20,0.01"), "set_speed", "get_speed");
    }

    GDExample::GDExample() {
        time_passed = 0.0;
        amplitude = 10.0;
        speed = 1.0;
    }

    void GDExample::_process(double delta) {
        time_passed += speed * delta;

        Vector2 new_position = Vector2(
            amplitude + (amplitude * sin(time_passed * 2.0)),
            amplitude + (amplitude * cos(time_passed * 1.5))
        );

        set_position(new_position);
    }

    ...

    void GDExample::set_speed(const double p_speed) {
        speed = p_speed;
    }

    double GDExample::get_speed() const {
        return speed;
    }

Bây giờ khi project được compile, chúng ta sẽ thấy một property khác có tên là speed. Thay đổi giá trị của nó sẽ khiến animation chạy nhanh hơn hoặc chậm hơn. Ngoài ra, chúng ta đã thêm một property range mô tả phạm vi giá trị có thể nhận. Hai argument đầu tiên là giá trị tối thiểu và tối đa, còn argument thứ ba là step size.

.. note::

    Để đơn giản, chúng ta chỉ sử dụng hint_range của property method. Còn nhiều option khác để lựa chọn. Bạn có thể dùng chúng để cấu hình thêm cách các property được hiển thị và thiết lập ở phía Godot. Bạn có thể tìm thêm thông tin về property hints tại đây :ref:`@GlobalScope<enum_@GlobalScope_PropertyHint>`.

Signals
-------

Cuối cùng nhưng không kém phần quan trọng, signals cũng hoạt động đầy đủ trong GDExtension. Để extension của bạn phản hồi một signal do object khác phát ra, bạn cần gọi ``connect`` trên object đó. Chúng tôi không nghĩ ra được ví dụ phù hợp cho icon Godot lắc lư này; chúng ta sẽ cần một ví dụ hoàn chỉnh hơn nhiều để minh họa.

Đây là cú pháp bắt buộc:

.. code-block:: cpp

    some_other_node->connect("the_signal", Callable(this, "my_method"));

Để kết nối signal ``the_signal`` từ một node khác với method ``my_method`` của chúng ta, chúng ta cần cung cấp cho method ``connect`` tên của signal và một ``Callable``. ``Callable`` chứa thông tin về một object mà trên đó một method có thể được gọi. Trong trường hợp của chúng ta, nó liên kết instance object hiện tại ``this`` với method ``my_method`` của object. Sau đó, method ``connect`` sẽ thêm liên kết này vào các observer của ``the_signal``. Mỗi khi ``the_signal`` được emit, Godot sẽ biết cần gọi method nào của object nào.

Lưu ý rằng bạn chỉ có thể gọi ``my_method`` nếu trước đó đã register nó trong method ``_bind_methods``. Nếu không, Godot sẽ không biết về sự tồn tại của ``my_method``.

Để tìm hiểu thêm về ``Callable``, hãy xem class reference tại đây: :ref:`Callable <class_Callable>`.

Việc object của bạn gửi ra signals phổ biến hơn. Với icon Godot lắc lư này, chúng ta sẽ làm một điều hơi ngớ ngẩn chỉ để minh họa cách hoạt động. Chúng ta sẽ emit một signal mỗi khi một giây trôi qua và truyền kèm vị trí mới.

Trong tệp header ``gdexample.h``, chúng ta cần định nghĩa một member ``time_emit`` mới:

.. code-block:: cpp

    ...
        double time_passed;
        double time_emit;
        double amplitude;
    ...

Lần này, các thay đổi trong ``gdexample.cpp`` phức tạp hơn. Trước tiên, bạn cần đặt ``time_emit = 0.0;`` trong method ``_init`` hoặc trong constructor. Chúng ta sẽ xem lần lượt hai thay đổi cần thiết còn lại.

Trong method ``_bind_methods``, chúng ta cần khai báo signal. Thực hiện như sau:

.. code-block:: cpp

    void GDExample::_bind_methods() {
        ...
        ADD_PROPERTY(PropertyInfo(Variant::FLOAT, "speed", PROPERTY_HINT_RANGE, "0,20,0.01"), "set_speed", "get_speed");

        ADD_SIGNAL(MethodInfo("position_changed", PropertyInfo(Variant::OBJECT, "node"), PropertyInfo(Variant::VECTOR2, "new_pos")));
    }

Ở đây, macro ``ADD_SIGNAL`` của chúng ta có thể là một lời gọi duy nhất với argument ``MethodInfo``. Tham số đầu tiên của ``MethodInfo`` sẽ là tên của signal, còn các tham số còn lại là các kiểu ``PropertyInfo`` mô tả những thông tin thiết yếu của từng tham số của method. Các tham số ``PropertyInfo`` được định nghĩa bằng kiểu dữ liệu của tham số, sau đó là tên mà tham số đó sẽ có theo mặc định.

Vì vậy ở đây, chúng ta thêm một signal với một ``MethodInfo`` đặt tên cho signal là "position_changed". Các tham số ``PropertyInfo`` mô tả hai argument thiết yếu: một argument có kiểu ``Object``, argument còn lại có kiểu ``Vector2``, lần lượt được đặt tên là "node" và "new_pos".

Tiếp theo, chúng ta cần thay đổi method ``_process``:

.. code-block:: cpp

    void GDExample::_process(double delta) {
        time_passed += speed * delta;

        Vector2 new_position = Vector2(
            amplitude + (amplitude * sin(time_passed * 2.0)),
            amplitude + (amplitude * cos(time_passed * 1.5))
        );

        set_position(new_position);

        time_emit += delta;
        if (time_emit > 1.0) {
            emit_signal("position_changed", this, new_position);

            time_emit = 0.0;
        }
    }

Sau khi một giây trôi qua, chúng ta emit signal và reset counter. Chúng ta có thể thêm trực tiếp các giá trị tham số vào ``emit_signal``.

Sau khi GDExtension library được compile, chúng ta có thể vào Godot và chọn sprite node. Trong dock **Node**, chúng ta có thể tìm thấy signal mới và liên kết nó bằng cách nhấn nút **Connect** hoặc double-click vào signal. Chúng ta đã thêm một script vào main node và triển khai signal như sau:

.. code-block:: gdscript

    extends Node

    func _on_Sprite2D_position_changed(node, new_pos):
        print("The position of " + node.get_class() + " is now " + str(new_pos))

Mỗi giây, chúng ta xuất vị trí ra console.

Các bước tiếp theo
------------------

Chúng tôi hy vọng ví dụ trên đã cho bạn thấy những kiến thức cơ bản. Bạn có thể phát triển tiếp ví dụ này để tạo các script hoàn chỉnh điều khiển node trong Godot bằng C++!

Thay vì xây dựng project dựa trên thiết lập ví dụ ở trên, chúng tôi khuyên bạn nên bắt đầu lại ngay bây giờ bằng cách clone `godot-cpp template <https://github.com/godotengine/godot-cpp-template>`__, rồi xây dựng project dựa trên đó. Thiết lập này hỗ trợ nhiều feature hơn, chẳng hạn như GitHub build action và boilerplate ``SConstruct`` hữu ích bổ sung.
