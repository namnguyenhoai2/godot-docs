.. _doc_binding_to_external_libraries:

Liên kết với các thư viện bên ngoài
===================================

Module
------

Ví dụ Summator trong :ref:`doc_custom_modules_in_cpp` rất phù hợp với các module nhỏ, tùy chỉnh, nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy xem một ví dụ sử dụng `Festival <https://www.cstr.ed.ac.uk/projects/festival/>`_, một thư viện tổng hợp giọng nói (text-to-speech) được viết bằng C++.

Để liên kết với một thư viện bên ngoài, hãy thiết lập một thư mục module tương tự như trong ví dụ Summator:

.. code-block:: none

    godot/modules/tts/

Tiếp theo, bạn sẽ tạo một tệp header với một lớp TTS:

.. code-block:: cpp
    :caption: godot/modules/tts/tts.h

    #pragma once

    #include "core/object/ref_counted.h"

    class TTS : public RefCounted {
        GDCLASS(TTS, RefCounted);

    protected:
        static void _bind_methods();

    public:
        bool say_text(String p_txt);

        TTS();
    };

Sau đó, bạn sẽ thêm tệp cpp.

.. code-block:: cpp
    :caption: godot/modules/tts/tts.cpp

    #include "tts.h"

    #include <festival.h>

    bool TTS::say_text(String p_txt) {

        //chuyển đổi Godot String thành Godot CharString rồi thành chuỗi C
        return festival_say_text(p_txt.ascii().get_data());
    }

    void TTS::_bind_methods() {

        ClassDB::bind_method(D_METHOD("say_text", "txt"), &TTS::say_text);
    }

    TTS::TTS() {
        festival_initialize(true, 210000); //không phải cách tốt nhất để thực hiện việc này vì lệnh gọi này chỉ nên được thực hiện một lần.
    }

Cũng như trước đây, lớp mới cần được đăng ký theo một cách nào đó, vì vậy cần tạo thêm hai tệp:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các tệp này phải nằm trong thư mục cấp cao nhất của module (cạnh các tệp ``SCsub`` và ``config.py``) để module được đăng ký đúng cách.

Các tệp này phải chứa nội dung sau:

.. code-block:: cpp
    :caption: godot/modules/tts/register_types.h

    void initialize_tts_module(ModuleInitializationLevel p_level);
    void uninitialize_tts_module(ModuleInitializationLevel p_level);
    /* đúng vậy, từ ở giữa phải giống với tên thư mục module */

.. code-block:: cpp
    :caption: godot/modules/tts/register_types.cpp

    #include "register_types.h"

    #include "core/object/class_db.h"
    #include "tts.h"

    void initialize_tts_module(ModuleInitializationLevel p_level) {
        if (p_level != MODULE_INITIALIZATION_LEVEL_SCENE) {
            return;
        }
        ClassDB::register_class<TTS>();
    }

    void uninitialize_tts_module(ModuleInitializationLevel p_level) {
        // Không cần thực hiện gì ở đây trong ví dụ này.
    }

Tiếp theo, bạn cần tạo tệp ``SCsub`` để hệ thống build biên dịch module này:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp") # Thêm tất cả các tệp cpp vào quá trình build

Bạn cần cài đặt thư viện bên ngoài trên máy của mình để có các tệp thư viện .a. Hãy xem tài liệu chính thức của thư viện để biết hướng dẫn cụ thể về cách thực hiện việc này trên hệ điều hành của bạn. Dưới đây, chúng tôi cung cấp các lệnh cài đặt cho Linux để bạn tham khảo.

.. code-block:: shell

    sudo apt-get install festival festival-dev  # Cài đặt các thư viện festival và speech_tools
    apt-cache search festvox-*  # Hiển thị danh sách các gói voice
    sudo apt-get install festvox-don festvox-rablpc16k festvox-kallpc16k festvox-kdlpc16k  # Cài đặt các voice

.. important::
    Các voice mà Festival sử dụng (cũng như mọi tài nguyên bên ngoài/bên thứ ba tiềm năng khác) đều có giấy phép và điều khoản sử dụng khác nhau; một số (nếu không muốn nói là hầu hết) có thể gây vấn đề với Godot, ngay cả khi bản thân Festival Library tương thích với giấy phép MIT. Hãy nhớ kiểm tra giấy phép và điều khoản sử dụng.

Thư viện bên ngoài cũng cần được cài đặt bên trong module để các tệp mã nguồn có thể truy cập được đối với compiler, đồng thời giữ cho mã nguồn module độc lập. Có thể cài đặt các thư viện festival và speech_tools từ thư mục modules/tts/ bằng git với các lệnh sau:

.. code-block:: shell

    git clone https://github.com/festvox/festival
    git clone https://github.com/festvox/speech_tools

Nếu bạn không muốn các tệp mã nguồn của repository bên ngoài được commit vào repository của mình, bạn có thể liên kết đến chúng bằng cách thêm chúng dưới dạng submodule (từ bên trong thư mục modules/tts/), như bên dưới:

.. code-block:: shell

    git submodule add https://github.com/festvox/festival
    git submodule add https://github.com/festvox/speech_tools

.. important::
    Lưu ý rằng các Git submodule không được sử dụng trong repository Godot. Nếu bạn đang phát triển một module để hợp nhất vào repository Godot chính, bạn không nên sử dụng submodule. Nếu module của bạn không được hợp nhất, bạn luôn có thể thử triển khai thư viện bên ngoài dưới dạng GDExtension.

Để thêm các thư mục include cho compiler tra cứu, bạn có thể nối chúng vào các đường dẫn của environment:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    # Các đường dẫn này tương đối so với /modules/tts/
    env_tts.Append(CPPPATH=["speech_tools/include", "festival/src/include"])

    # LIBPATH và LIBS cần được thiết lập trên "env" thực (không phải bản sao)
    # để liên kết các thư viện được chỉ định với tệp thực thi Godot.

    # Đây là đường dẫn tuyệt đối nơi các thư viện .a của bạn nằm.
    # Nếu sử dụng đường dẫn tương đối, bạn phải chuyển đổi nó thành
    # đường dẫn đầy đủ bằng một hàm tiện ích, chẳng hạn như `Dir('...').abspath`.
    env.Append(LIBPATH=[Dir('libpath').abspath])

    # Hãy kiểm tra tài liệu của thư viện bên ngoài để xem những tệp thư viện nào
    # cần được đưa vào/liên kết.
    env.Append(LIBS=['Festival', 'estools', 'estbase', 'eststring'])

Nếu bạn muốn thêm các cờ compiler tùy chỉnh khi build module, trước tiên bạn cần clone `env`, để các cờ đó không được thêm vào toàn bộ quá trình build Godot (điều này có thể gây lỗi). Ví dụ `SCsub` với các cờ tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp")
    # Nối các cờ CCFLAGS cho cả mã C và C++.
    env_tts.Append(CCFLAGS=['-O2'])
    # Nếu cần, bạn có thể:
    # - Nối CFLAGS chỉ cho mã C.
    # - Nối CXXFLAGS chỉ cho mã C++.

Module hoàn chỉnh sẽ có dạng như sau:

.. code-block:: none

    godot/modules/tts/festival/
    godot/modules/tts/libpath/libestbase.a
    godot/modules/tts/libpath/libestools.a
    godot/modules/tts/libpath/libeststring.a
    godot/modules/tts/libpath/libFestival.a
    godot/modules/tts/speech_tools/
    godot/modules/tts/config.py
    godot/modules/tts/tts.h
    godot/modules/tts/tts.cpp
    godot/modules/tts/register_types.h
    godot/modules/tts/register_types.cpp
    godot/modules/tts/SCsub

Sử dụng module
--------------

Bây giờ bạn có thể sử dụng module mới tạo từ bất kỳ script nào:

::

    var t = TTS.new()
    var script = "Hello world. This is a test!"
    var is_spoken = t.say_text(script)
    print('is_spoken: ', is_spoken)

Và đầu ra sẽ là ``is_spoken: True`` nếu văn bản được đọc thành tiếng.

.. _`Festival`: https://www.cstr.ed.ac.uk/projects/festival/
