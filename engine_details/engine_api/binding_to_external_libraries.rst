.. _doc_binding_to_external_libraries:

Liên kết với các thư viện bên ngoài
===================================

Các mô-đun
----------

Ví dụ Summator trong :ref:`doc_custom_modules_in_cpp` rất phù hợp cho các mô-đun nhỏ, tùy chỉnh, nhưng nếu bạn muốn sử dụng một thư viện bên ngoài lớn hơn thì sao? Hãy xem một ví dụ sử dụng `Festival <https://www.cstr.ed.ac.uk/projects/festival/>`_, một thư viện tổng hợp giọng nói (chuyển văn bản thành giọng nói) được viết bằng C++.

Để liên kết với một thư viện bên ngoài, hãy thiết lập một thư mục mô-đun tương tự như ví dụ Summator:

.. code-block:: none

    godot/modules/tts/

Tiếp theo, bạn sẽ tạo một tệp tiêu đề với một lớp TTS:

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

        //convert Godot String to Godot CharString to C string
        return festival_say_text(p_txt.ascii().get_data());
    }

    void TTS::_bind_methods() {

        ClassDB::bind_method(D_METHOD("say_text", "txt"), &TTS::say_text);
    }

    TTS::TTS() {
        festival_initialize(true, 210000); //not the best way to do it as this should only ever be called once.
    }

Cũng như trước đây, lớp mới cần được đăng ký theo một cách nào đó, vì vậy cần tạo thêm hai tệp:

.. code-block:: none

    register_types.h
    register_types.cpp

.. important::
    Các tệp này phải nằm trong thư mục cấp cao nhất của mô-đun (bên cạnh các tệp ``SCsub`` và ``config.py`` của bạn) để mô-đun được đăng ký đúng cách.

Các tệp này phải chứa nội dung sau:

.. code-block:: cpp
    :caption: godot/modules/tts/register_types.h

    void initialize_tts_module(ModuleInitializationLevel p_level);
    void uninitialize_tts_module(ModuleInitializationLevel p_level);
    /* yes, the word in the middle must be the same as the module folder name */

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
        // Nothing to do here in this example.
    }

Tiếp theo, bạn cần tạo một tệp ``SCsub`` để hệ thống xây dựng biên dịch mô-đun này:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp") # Add all cpp files to the build

Bạn cần cài đặt thư viện bên ngoài trên máy của mình để có các tệp thư viện .a. Hãy xem tài liệu chính thức của thư viện để biết hướng dẫn cụ thể về cách thực hiện việc này trên hệ điều hành của bạn. Dưới đây là các lệnh cài đặt cho Linux để bạn tham khảo.

.. code-block:: shell

    sudo apt-get install festival festival-dev  # Installs festival and speech_tools libraries
    apt-cache search festvox-*  # Displays list of voice packages
    sudo apt-get install festvox-don festvox-rablpc16k festvox-kallpc16k festvox-kdlpc16k  # Installs voices

.. important::
    Các giọng nói mà Festival sử dụng (và mọi tài nguyên bên ngoài/bên thứ ba tiềm năng khác) đều có giấy phép và điều khoản sử dụng khác nhau; một số (nếu không muốn nói là hầu hết) có thể gây vấn đề với Godot, ngay cả khi bản thân Festival Library tương thích với Giấy phép MIT. Hãy nhớ kiểm tra giấy phép và điều khoản sử dụng.

Thư viện bên ngoài cũng cần được cài đặt bên trong mô-đun để giúp trình biên dịch có thể truy cập các tệp mã nguồn, đồng thời giữ cho mã mô-đun độc lập. Có thể cài đặt các thư viện festival và speech_tools từ thư mục modules/tts/ thông qua git bằng các lệnh sau:

.. code-block:: shell

    git clone https://github.com/festvox/festival
    git clone https://github.com/festvox/speech_tools

Nếu không muốn các tệp mã nguồn của kho bên ngoài được commit vào kho của mình, bạn có thể liên kết đến chúng bằng cách thêm chúng dưới dạng các mô-đun con (từ bên trong thư mục modules/tts/), như dưới đây:

.. code-block:: shell

    git submodule add https://github.com/festvox/festival
    git submodule add https://github.com/festvox/speech_tools

.. important::
    Lưu ý rằng các mô-đun con Git không được sử dụng trong kho Godot. Nếu bạn đang phát triển một mô-đun để hợp nhất vào kho Godot chính, bạn không nên sử dụng các mô-đun con. Nếu mô-đun của bạn không được hợp nhất, bạn luôn có thể thử triển khai thư viện bên ngoài dưới dạng một GDExtension.

Để thêm các thư mục include mà trình biên dịch sẽ xem xét, bạn có thể nối chúng vào các đường dẫn của môi trường:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    # These paths are relative to /modules/tts/
    env_tts.Append(CPPPATH=["speech_tools/include", "festival/src/include"])

    # LIBPATH and LIBS need to be set on the real "env" (not the clone)
    # to link the specified libraries to the Godot executable.

    # This is an absolute path where your .a libraries reside.
    # If using a relative path, you must convert it to a
    # full path using a utility function, such as `Dir('...').abspath`.
    env.Append(LIBPATH=[Dir('libpath').abspath])

    # Check with the documentation of the external library to see which library
    # files should be included/linked.
    env.Append(LIBS=['Festival', 'estools', 'estbase', 'eststring'])

Nếu muốn thêm các cờ trình biên dịch tùy chỉnh khi xây dựng mô-đun, trước tiên bạn cần sao chép `env`, để các cờ đó không được thêm vào toàn bộ bản dựng Godot (điều này có thể gây lỗi). Ví dụ về `SCsub` với các cờ tùy chỉnh:

.. code-block:: python
    :caption: godot/modules/tts/SCsub

    Import('env')

    env_tts = env.Clone()
    env_tts.add_source_files(env.modules_sources, "*.cpp")
    # Append CCFLAGS flags for both C and C++ code.
    env_tts.Append(CCFLAGS=['-O2'])
    # If you need to, you can:
    # - Append CFLAGS for C code only.
    # - Append CXXFLAGS for C++ code only.

Mô-đun hoàn chỉnh sẽ có dạng như sau:

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

Sử dụng mô-đun
--------------

Bây giờ bạn có thể sử dụng mô-đun mới tạo từ bất kỳ tập lệnh nào:

::

    var t = TTS.new()
    var script = "Hello world. This is a test!"
    var is_spoken = t.say_text(script)
    print('is_spoken: ', is_spoken)

Và đầu ra sẽ là ``is_spoken: True`` nếu văn bản được đọc thành tiếng.
