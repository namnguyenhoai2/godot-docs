.. _doc_binding_to_external_libraries:

Liên kết với các thư viện bên ngoài
===================================

Module
------

Ví dụ Summator trong :ref:`doc_custom_modules_in_cpp` rất phù hợp với các module nhỏ, tùy chỉnh, nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy xem một ví dụ sử dụng `Festival <https://www.cstr.ed.ac.uk/projects/festival/>`_, một thư viện tổng hợp giọng nói (text-to-speech) được viết bằng C++.

Để liên kết với một thư viện bên ngoài, hãy thiết lập một thư mục module tương tự như ví dụ Summator:

.. code-block:: none

    godot/modules/tts/

Tiếp theo, bạn sẽ tạo một tệp header với class TTS:

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

        //chuyển Godot String thành Godot CharString rồi thành C string
        return festival_say_text(p_txt.ascii().get_data());
    }

    void TTS::_bind_methods() {

        ClassDB::bind_method(D_METHOD("say_text", "txt"), &TTS::say_text);
    }

    TTS::TTS() {
        festival_initialize(true, 210000); //không phải cách tốt nhất để thực hiện việc này vì hàm này chỉ nên được gọi một lần.
    }

Cũng như trước đây, class mới cần được đăng ký theo một cách nào đó, vì vậy cần tạo thêm hai tệp:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các tệp này phải nằm trong thư mục cấp cao nhất của module (bên cạnh các tệp ``SCsub`` và ``config.py``) để module được đăng ký đúng cách.

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
        // Không cần làm gì ở đây trong ví dụ này.
    }

Tiếp theo, bạn cần tạo một tệp ``SCsub`` để hệ thống build biên dịch module này:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp") # Thêm tất cả tệp cpp vào build

Bạn sẽ cần cài đặt thư viện bên ngoài trên máy để có các tệp thư viện .a. Hãy xem tài liệu chính thức của thư viện để biết hướng dẫn cụ thể về cách thực hiện việc này trên hệ điều hành của bạn. Dưới đây là các lệnh cài đặt cho Linux để tham khảo.

.. code-block:: shell

    sudo apt-get install festival festival-dev  # Cài đặt các thư viện festival và speech_tools
    apt-cache search festvox-*  # Hiển thị danh sách các gói voice
    sudo apt-get install festvox-don festvox-rablpc16k festvox-kallpc16k festvox-kdlpc16k  # Cài đặt các voice

.. important::
    Các voice mà Festival sử dụng (và mọi tài nguyên bên ngoài/bên thứ ba tiềm năng khác) đều có giấy phép và điều khoản sử dụng khác nhau; một số (nếu không muốn nói là phần lớn) có thể gây vấn đề với Godot, ngay cả khi bản thân Festival Library tương thích với MIT License. Hãy nhớ kiểm tra giấy phép và điều khoản sử dụng.

Thư viện bên ngoài cũng cần được cài đặt bên trong module để các tệp source có thể truy cập được bởi compiler, đồng thời giữ cho mã của module độc lập. Có thể cài đặt các thư viện festival và speech_tools từ thư mục modules/tts/ thông qua git bằng các lệnh sau:

.. code-block:: shell

    git clone https://github.com/festvox/festival
    git clone https://github.com/festvox/speech_tools

Nếu không muốn các tệp source của repository bên ngoài được commit vào repository của mình, bạn có thể liên kết tới chúng bằng cách thêm chúng dưới dạng submodule (từ bên trong thư mục modules/tts/), như bên dưới:

.. code-block:: shell

    git submodule add https://github.com/festvox/festival
    git submodule add https://github.com/festvox/speech_tools

.. important::
    Lưu ý rằng Git submodule không được sử dụng trong repository Godot. Nếu bạn đang phát triển một module để được merge vào repository Godot chính, bạn không nên sử dụng submodule. Nếu module của bạn không được merge, bạn luôn có thể thử triển khai thư viện bên ngoài dưới dạng GDExtension.

Để thêm các thư mục include cho compiler tìm kiếm, bạn có thể nối chúng vào các path của environment:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    # Các path này tương đối với /modules/tts/
    env_tts.Append(CPPPATH=["speech_tools/include", "festival/src/include"])

    # LIBPATH và LIBS cần được thiết lập trên "env" thực (không phải bản clone)
    # để liên kết các thư viện được chỉ định với executable Godot.

    # Đây là path tuyệt đối nơi các thư viện .a của bạn nằm.
    # Nếu sử dụng path tương đối, bạn phải chuyển nó thành một
    # full path bằng một utility function, chẳng hạn như `Dir('...').abspath`.
    env.Append(LIBPATH=[Dir('libpath').abspath])

    # Kiểm tra tài liệu của thư viện bên ngoài để xem thư viện nào
    # các tệp cần được include/link.
    env.Append(LIBS=['Festival', 'estools', 'estbase', 'eststring'])

Nếu muốn thêm các compiler flag tùy chỉnh khi build module, trước tiên bạn cần clone ``env``, để các flag đó không được thêm vào toàn bộ Godot build (điều này có thể gây lỗi). Ví dụ ``SCsub`` với các flag tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp")
    # Nối các flag CCFLAGS cho cả mã C và C++.
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

Và output sẽ là ``is_spoken: True`` nếu văn bản được đọc thành tiếng.
