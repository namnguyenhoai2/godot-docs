.. _doc_gdextension_c_example:

Ví dụ GDExtension bằng C
========================

Giới thiệu
----------

Đây là một ví dụ đơn giản về cách làm việc trực tiếp với GDExtension bằng mã C. Lưu ý rằng API không được thiết kế để sử dụng trực tiếp, vì vậy đoạn mã này chắc chắn sẽ khá dài dòng và yêu cầu nhiều bước, ngay cả đối với một ví dụ nhỏ. Tuy nhiên, nó đóng vai trò là tài liệu tham khảo để tạo binding cho một ngôn ngữ khác. Bạn vẫn có thể sử dụng API trực tiếp nếu muốn, điều này có thể thuận tiện khi chỉ cần tạo binding cho một thư viện bên thứ ba.

Trong ví dụ này, chúng ta sẽ tạo một node tùy chỉnh để di chuyển một sprite trên màn hình dựa trên các tham số do người dùng cung cấp. Dù rất đơn giản, ví dụ này cho thấy cách thực hiện một số việc với GDExtension, chẳng hạn như đăng ký các class tùy chỉnh cùng với method, property và signal. Qua đó, bạn có thể hiểu rõ hơn về API GDExtension.

Thiết lập project
-----------------

Bạn sẽ cần một số điều kiện tiên quyết sau:

- một executable Godot 4.2 (hoặc mới hơn),
- một trình biên dịch C,
- SCons làm build tool.

Vì ví dụ này sử dụng API trực tiếp nên không cần dùng repository `godot-cpp <https://github.com/godotengine/godot-cpp>`__.

Cấu trúc file
-------------

Để sắp xếp các file, chúng ta sẽ chủ yếu chia chúng thành hai folder:

.. code-block:: none

    gdextension_c_example/
    |
    +--project/                  # game example/demo to test the extension
    |
    +--src/                   # source code of the extension we are building

Chúng ta cũng cần một bản sao của header ``gdextension_interface.h`` từ mã nguồn Godot. Bạn có thể lấy header này trực tiếp từ executable Godot bằng cách chạy lệnh sau:

.. code-block:: none

    godot --dump-gdextension-interface

Lệnh này tạo header trong folder hiện tại, vì vậy bạn chỉ cần sao chép nó vào folder ``src`` trong project ví dụ.

Cuối cùng, chúng ta cần tham khảo thêm một nguồn thông tin khác: file JSON chứa thông tin tham chiếu API Godot. Mã sẽ không trực tiếp sử dụng file này; chúng ta chỉ dùng nó để trích xuất thủ công một số thông tin.

Để lấy file JSON này, chỉ cần gọi executable Godot:

.. code-block:: none

    godot --dump-extension-api

File ``extension_api.json`` được tạo trong folder hiện tại. Bạn có thể sao chép file này vào folder ví dụ để tiện sử dụng.

.. note::
    Extension này nhắm đến Godot 4.2, nhưng cũng sẽ hoạt động trên các phiên bản mới hơn. Nếu muốn nhắm đến một phiên bản tối thiểu khác, hãy đảm bảo lấy header và file JSON từ phiên bản Godot mà bạn đang nhắm đến.

Build system
------------

Sử dụng build system giúp chúng ta dễ dàng hơn rất nhiều khi làm việc với mã C. Để thuận tiện, chúng ta sẽ dùng SCons vì đây cũng là công cụ mà chính Godot sử dụng.

File ``SConstruct`` sau đây là một file đơn giản, có nhiệm vụ build extension cho platform hiện tại mà bạn đang sử dụng, có thể là Linux, macOS hoặc Windows. Đây sẽ là bản build không tối ưu hóa để phục vụ mục đích debug. File này cũng giả định bản build 64-bit, điều này có liên quan đến một số phần trong mã ví dụ. Việc tạo các kiểu build khác và cross-compilation nằm ngoài phạm vi của tutorial này. Hãy lưu file này vào folder gốc.

.. code-block:: python

    #!/bin/env python
    from SCons.Script import Environment
    from os import path
    import sys

    env = Environment()

    # Đặt đường dẫn và tên target.
    target_path = "project/bin/"
    target_name = "libgdexample"

    # Đặt compiler và các flag.
    env.Append(CPPPATH=["src"])  # Thêm folder src vào include path.
    env.Append(CFLAGS=["-O0", "-g"])  # Tạo bản build debug.

    # Sử dụng Clang trên macOS.
    if sys.platform == "darwin":
        env["CC"] = "clang"

    # Thêm tất cả file C trong folder "src" làm source.
    sources = env.Glob("src/*.c")

    # Tạo một shared library.
    library = env.SharedLibrary(
        target=path.join(target_path, target_name),
        source=sources,
    )

    # Đặt library làm target mặc định.
    env.Default(library)

Thao tác này sẽ bao gồm tất cả file C trong folder ``src``, vì vậy chúng ta không cần thay đổi file này khi thêm source file mới.

Khởi tạo extension
------------------

Phần mã đầu tiên chịu trách nhiệm khởi tạo extension. Đây là phần giúp Godot nhận biết những gì GDExtension của chúng ta cung cấp, chẳng hạn như class và plugin.

Tạo file ``init.h`` trong folder ``src``, với nội dung sau:

.. code-block:: c

    #pragma once

    #include "defs.h"

    #include "gdextension_interface.h"

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level);
    void deinitialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level);
    GDExtensionBool GDE_EXPORT gdexample_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization);

Các function được khai báo ở đây có signature theo yêu cầu của API GDExtension.

Hãy lưu ý đến việc include file ``defs.h``. Đây là một trong các helper của chúng ta nhằm đơn giản hóa việc viết mã extension. Hiện tại, file này chỉ chứa định nghĩa của ``GDE_EXPORT``, một macro giúp function có thể public trong shared library để Godot gọi đúng cách. Macro này giúp trừu tượng hóa các yêu cầu của từng compiler.

Tạo file ``defs.h`` trong folder ``src`` với nội dung sau:

.. code-block:: c

    #pragma once

    #include <stdbool.h>
    #include <stddef.h>
    #include <stdint.h>

    #if !defined(GDE_EXPORT)
    #if defined(_WIN32)
    #define GDE_EXPORT __declspec(dllexport)
    #elif defined(__GNUC__)
    #define GDE_EXPORT __attribute__((visibility("default")))
    #else
    #define GDE_EXPORT
    #endif
    #endif // ! GDE_EXPORT

Chúng ta cũng include một số header chuẩn để mọi việc dễ dàng hơn. Bây giờ chúng ta chỉ cần include ``defs.h``, và các header đó sẽ được include kèm.

Bây giờ, hãy triển khai các function mà chúng ta vừa khai báo. Tạo một file có tên ``init.c`` trong folder ``src`` và thêm đoạn mã sau:

.. code-block:: c

    #include "init.h"

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
    }

    void deinitialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
    }

    GDExtensionBool GDE_EXPORT gdexample_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization)
    {
        r_initialization->initialize = initialize_gdexample_module;
        r_initialization->deinitialize = deinitialize_gdexample_module;
        r_initialization->userdata = NULL;
        r_initialization->minimum_initialization_level = GDEXTENSION_INITIALIZATION_SCENE;

        return true;
    }

Đoạn mã này thiết lập dữ liệu khởi tạo mà Godot yêu cầu. Các function khởi tạo và hủy khởi tạo được thiết lập để Godot gọi khi cần. Đoạn mã cũng đặt initialization level, giá trị này thay đổi tùy theo từng extension. Vì chúng ta dự định thêm một node tùy chỉnh nên level ``SCENE`` là đủ.

Chúng ta sẽ hoàn thiện function ``initialize_gdexample_module()`` sau để đăng ký class tùy chỉnh của mình.

Một class cơ bản
----------------

Để tạo một node thực tế, trước tiên chúng ta sẽ tạo một struct C để chứa dữ liệu và các function đóng vai trò là method. Mục tiêu là tạo một node tùy chỉnh kế thừa từ :ref:`Sprite2D <class_Sprite2D>`.

Tạo file có tên ``gdexample.h`` trong folder ``src`` với nội dung sau:

.. code-block:: c

    #pragma once

    #include "gdextension_interface.h"

    #include "defs.h"

    // Struct chứa dữ liệu của node.
    typedef struct
    {
        // Metadata.
        GDExtensionObjectPtr object; // Lưu object Godot bên dưới.
    } GDExample;

    // Constructor của node.
    void gdexample_class_constructor(GDExample *self);

    // Destructor của node.
    void gdexample_class_destructor(GDExample *self);

    // Các binding.
    void gdexample_class_bind_methods();

Điểm đáng chú ý ở đây là field ``object``, chứa một pointer đến object Godot, và function ``gdexample_class_bind_methods()``, dùng để đăng ký metadata của class tùy chỉnh (property, method và signal). Function sau không hoàn toàn bắt buộc, vì chúng ta có thể thực hiện việc này khi đăng ký class, nhưng tách riêng các mối quan tâm và để class tự đăng ký metadata sẽ rõ ràng hơn.

Trường ``object`` là cần thiết vì class của chúng ta sẽ kế thừa một class Godot. Vì không thể kế thừa trực tiếp, do chúng ta không tương tác với mã nguồn (và C thậm chí còn không có class), thay vào đó chúng ta yêu cầu Godot tạo một object thuộc kiểu mà nó biết rồi gắn extension của chúng ta vào đó. Chẳng hạn, chúng ta sẽ cần tham chiếu đến những object như vậy khi gọi các method trên class cha.

Hãy tạo phần tương ứng ở source của header này. Tạo file ``gdexample.c`` trong thư mục ``src`` và thêm đoạn mã sau vào đó:

.. code-block:: c

    #include "gdexample.h"

    void gdexample_class_constructor(GDExample *self)
    {
    }

    void gdexample_class_destructor(GDExample *self)
    {
    }

    void gdexample_class_bind_methods()
    {
    }


Vì hiện tại chúng ta chưa cần làm gì với những function đó, chúng sẽ để trống trong một thời gian.

Bước tiếp theo là đăng ký class của chúng ta. Tuy nhiên, để làm vậy, chúng ta cần tạo một :ref:`StringName <class_StringName>`, và để làm điều đó, chúng ta phải lấy một function từ GDExtension API. Vì sẽ cần thực hiện việc này vài lần và cũng sẽ cần những thành phần khác, hãy tạo một wrapper API để đơn giản hóa loại công việc này.

Một wrapper API
---------------

Trước tiên, hãy tạo file ``api.h`` trong thư mục ``src``:

.. code-block:: c

    #pragma once

    /*
    File này tập hợp các helper để gọi GDExtension API
    theo cách ít dài dòng hơn, đồng thời lưu cache các method từ discovery API,
    để chúng ta không phải liên tục tải lại cùng những method đó.
    */

    #include "gdextension_interface.h"

    #include "defs.h"

    extern GDExtensionClassLibraryPtr class_library;

    // Các method API.

    extern struct Constructors
    {
        GDExtensionInterfaceStringNameNewWithLatin1Chars string_name_new_with_latin1_chars;
    } constructors;

    extern struct Destructors
    {
        GDExtensionPtrDestructor string_name_destructor;
    } destructors;

    extern struct API
    {
        GDExtensionInterfaceClassdbRegisterExtensionClass2 classdb_register_extension_class2;
    } api;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address);

File này sẽ bao gồm nhiều helper khác khi chúng ta bổ sung thêm chức năng hữu ích cho extension. Hiện tại, file chỉ có một con trỏ đến function tạo StringName từ một chuỗi C (với encoding Latin-1) và một con trỏ khác để hủy StringName; chúng ta cần function này để tránh rò rỉ bộ nhớ, cùng với function đăng ký class, là mục tiêu ban đầu của chúng ta.

Chúng ta cũng lưu một tham chiếu đến ``class_library`` ở đây. Đây là thứ Godot cung cấp khi khởi tạo extension, và chúng ta sẽ cần dùng nó khi đăng ký những thành phần mình tạo để Godot biết extension nào đang thực hiện lời gọi.

Ngoài ra còn có một function để tải các function pointer đó từ GDExtension API.

Hãy làm phần tương ứng ở source của header này. Tạo file ``api.c`` trong thư mục ``src`` và thêm đoạn mã sau:

.. code-block:: c

    #include "api.h"

    GDExtensionClassLibraryPtr class_library = NULL;

    struct Constructors constructors;
    struct Destructors destructors;
    struct API api;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // Lấy các helper function trước.
        GDExtensionInterfaceVariantGetPtrDestructor variant_get_ptr_destructor = (GDExtensionInterfaceVariantGetPtrDestructor)p_get_proc_address("variant_get_ptr_destructor");

        // API.
        api.classdb_register_extension_class2 = (GDExtensionInterfaceClassdbRegisterExtensionClass2)p_get_proc_address("classdb_register_extension_class2");

        // Các constructor.
        constructors.string_name_new_with_latin1_chars = (GDExtensionInterfaceStringNameNewWithLatin1Chars)p_get_proc_address("string_name_new_with_latin1_chars");

        // Các destructor.
        destructors.string_name_destructor = variant_get_ptr_destructor(GDEXTENSION_VARIANT_TYPE_STRING_NAME);
    }

Điều quan trọng đầu tiên ở đây là ``p_get_proc_address``. Đây là một function từ GDExtension API được truyền vào trong quá trình khởi tạo. Bạn có thể dùng function này để yêu cầu các function cụ thể từ API theo tên của chúng. Ở đây, chúng ta lưu cache kết quả để không phải giữ một tham chiếu đến ``p_get_proc_address`` ở khắp nơi mà có thể dùng wrapper của mình thay thế.

Đầu tiên, chúng ta yêu cầu function ``variant_get_ptr_destructor()``. Function này sẽ không được dùng bên ngoài function hiện tại, nên chúng ta không thêm nó vào wrapper mà chỉ lưu cache cục bộ. Phép cast là cần thiết để tắt các cảnh báo của compiler.

Sau đó, chúng ta lấy function tạo một StringName từ chuỗi C, đúng với function cần thiết đã đề cập trước đó. Chúng ta lưu function này trong struct ``constructors``.

Tiếp theo, chúng ta dùng function ``variant_get_ptr_destructor()`` vừa lấy để truy vấn destructor cho StringName, sử dụng giá trị enum từ API ``gdextension_interface.h`` làm tham số. Tương tự, chúng ta có thể lấy destructor cho các kiểu khác, nhưng trong ví dụ này, chúng ta sẽ chỉ giới hạn ở những gì cần thiết.

Cuối cùng, chúng ta lấy function ``classdb_register_extension_class2()``, function cần thiết để đăng ký custom class của mình.

.. note::
    Bạn có thể thắc mắc tại sao ``2`` lại xuất hiện trong tên function. Điều này có nghĩa đây là phiên bản thứ hai của function đó. Phiên bản cũ được giữ lại để đảm bảo khả năng tương thích ngược với các extension cũ hơn, nhưng vì phiên bản thứ hai đã có sẵn, tốt nhất là dùng phiên bản mới, bởi trong ví dụ này chúng ta không định hỗ trợ các phiên bản Godot cũ hơn.

    Header ``gdextension_interface.h`` ghi lại phiên bản Godot mà mỗi function được giới thiệu.

Chúng ta cũng định nghĩa biến ``class_library`` ở đây; biến này sẽ được thiết lập trong quá trình khởi tạo.

Nói về việc khởi tạo, bây giờ chúng ta phải thay đổi file ``init.c`` để điền những thành phần vừa thêm:

.. code-block:: c

    GDExtensionBool GDE_EXPORT gdexample_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization)
    {
        class_library = p_library;
        load_api(p_get_proc_address);

        ...

Ở đây, chúng ta thiết lập ``class_library`` theo yêu cầu và gọi function ``load_api()`` mới của mình. Đừng quên include các header mới ở đầu file này:

.. code-block:: c

    #include "init.h"

    #include "api.h"
    #include "gdexample.h"
    ...

Nhân tiện, chúng ta có thể đăng ký custom class mới. Hãy điền vào function ``initialize_gdexample_module()``:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        if (p_level != GDEXTENSION_INITIALIZATION_SCENE)
        {
            return;
        }

        // Đăng ký class.
        StringName class_name;
        constructors.string_name_new_with_latin1_chars(&class_name, "GDExample", false);
        StringName parent_class_name;
        constructors.string_name_new_with_latin1_chars(&parent_class_name, "Sprite2D", false);

        GDExtensionClassCreationInfo2 class_info = {
            .is_virtual = false,
            .is_abstract = false,
            .is_exposed = true,
            .set_func = NULL,
            .get_func = NULL,
            .get_property_list_func = NULL,
            .free_property_list_func = NULL,
            .property_can_revert_func = NULL,
            .property_get_revert_func = NULL,
            .validate_property_func = NULL,
            .notification_func = NULL,
            .to_string_func = NULL,
            .reference_func = NULL,
            .unreference_func = NULL,
            .create_instance_func = gdexample_class_create_instance,
            .free_instance_func = gdexample_class_free_instance,
            .recreate_instance_func = NULL,
            .get_virtual_func = NULL,
            .get_virtual_call_data_func = NULL,
            .call_virtual_with_data_func = NULL,
            .get_rid_func = NULL,
            .class_userdata = NULL,
        };

        api.classdb_register_extension_class2(class_library, &class_name, &parent_class_name, &class_info);

        // Bind các method.
        gdexample_class_bind_methods();

        // Hủy các thành phần.
        destructors.string_name_destructor(&class_name);
        destructors.string_name_destructor(&parent_class_name);
    }

Struct chứa thông tin class là phần lớn nhất ở đây. Không field nào của nó là bắt buộc, ngoại trừ ``create_instance_func`` và ``free_instance_func``. Chúng ta chưa tạo những function đó, nên sẽ phải thực hiện sớm. Lưu ý rằng chúng ta bỏ qua việc khởi tạo nếu nó không ở cấp độ ``SCENE``. Function này có thể được gọi nhiều lần, một lần cho mỗi cấp độ, nhưng chúng ta chỉ muốn đăng ký class một lần.

Thành phần chưa được định nghĩa khác ở đây là ``StringName``. Đây sẽ là một struct opaque dùng để chứa dữ liệu của một Godot StringName trong extension của chúng ta. Chúng ta sẽ định nghĩa nó trong file có tên phù hợp là ``defs.h``:

.. code-block:: c

    ...
    // Có thể lấy kích thước từ file extension_api.json.
    #ifdef BUILD_32
    #define STRING_NAME_SIZE 4
    #else
    #define STRING_NAME_SIZE 8
    #endif

    // Các kiểu.

    typedef struct
    {
        uint8_t data[STRING_NAME_SIZE];
    } StringName;

Như đã đề cập trong comment, có thể tìm thấy các kích thước trong file ``extension_api.json`` mà chúng ta đã tạo trước đó, bên dưới property ``builtin_class_sizes``. ``BUILD_32`` không bao giờ được định nghĩa, vì ở đây chúng ta giả định đang làm việc với bản build Godot 64-bit; nhưng nếu cần, bạn có thể thêm ``env.Append(CPPDEFINES=["BUILD_32"])`` vào file ``SConstruct``.

Comment ``// Types.`` báo trước rằng chúng ta sẽ thêm nhiều kiểu hơn vào file này. Hãy để việc đó lại sau.

Struct ``StringName`` ở đây chỉ dùng để chứa dữ liệu Godot, nên chúng ta không thực sự quan tâm bên trong nó có gì. Tuy nhiên, trong trường hợp này, nó chỉ là một con trỏ đến dữ liệu trên heap. Chúng ta sẽ dùng struct này khi cần tự cấp phát dữ liệu cho một StringName, chẳng hạn như khi đăng ký class.

Quay lại việc đăng ký, chúng ta cần thực hiện các function tạo và giải phóng. Hãy include chúng trong ``gdexample.h`` vì chúng chỉ dành riêng cho custom class:

.. code-block:: c

    ...
    // Các binding.
    void gdexample_class_bind_methods();
    GDExtensionObjectPtr gdexample_class_create_instance(void *p_class_userdata);
    void gdexample_class_free_instance(void *p_class_userdata, GDExtensionClassInstancePtr p_instance);
    ...

Trước khi triển khai những function đó, chúng ta sẽ cần thêm một vài thành phần vào API. Chúng ta cần một cách để cấp phát và giải phóng bộ nhớ. Mặc dù có thể làm việc này bằng ``malloc()`` quen thuộc, chúng ta có thể thay vào đó sử dụng các function quản lý bộ nhớ của Godot. Chúng ta cũng cần một cách để tạo một Godot object và thiết lập nó với custom instance của mình.

Vậy hãy thay đổi ``api.h`` để bổ sung các hàm mới này:

.. code-block:: c

    ...
    extern struct API
    {
        GDExtensionInterfaceClassdbRegisterExtensionClass2 classdb_register_extension_class2;
        GDExtensionInterfaceClassdbConstructObject classdb_construct_object;
        GDExtensionInterfaceObjectSetInstance object_set_instance;
        GDExtensionInterfaceObjectSetInstanceBinding object_set_instance_binding;
        GDExtensionInterfaceMemAlloc mem_alloc;
        GDExtensionInterfaceMemFree mem_free;
    } api;

Sau đó, thay đổi hàm ``load_api()`` trong ``api.c`` để lấy các hàm mới này:

.. code-block:: c

    ...
    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        ...
        // API.
        api.classdb_register_extension_class2 = p_get_proc_address("classdb_register_extension_class2");
        api.classdb_construct_object = (GDExtensionInterfaceClassdbConstructObject)p_get_proc_address("classdb_construct_object");
        api.object_set_instance = (GDExtensionInterfaceObjectSetInstance)p_get_proc_address("object_set_instance");
        api.object_set_instance_binding = (GDExtensionInterfaceObjectSetInstanceBinding)p_get_proc_address("object_set_instance_binding");
        api.mem_alloc = (GDExtensionInterfaceMemAlloc)p_get_proc_address("mem_alloc");
        api.mem_free = (GDExtensionInterfaceMemFree)p_get_proc_address("mem_free");
    }

Bây giờ, chúng ta có thể quay lại ``gdexample.c`` và định nghĩa các hàm mới, đồng thời nhớ thêm header ``api.h``:

.. code-block:: c

    #include "gdexample.h"

    #include "api.h"

    ...

    const GDExtensionInstanceBindingCallbacks gdexample_class_binding_callbacks = {
        .create_callback = NULL,
        .free_callback = NULL,
        .reference_callback = NULL,
    };

    GDExtensionObjectPtr gdexample_class_create_instance(void *p_class_userdata)
    {
        // Tạo đối tượng Godot native;
        StringName class_name;
        constructors.string_name_new_with_latin1_chars(&class_name, "Sprite2D", false);
        GDExtensionObjectPtr object = api.classdb_construct_object(&class_name);
        destructors.string_name_destructor(&class_name);

        // Tạo đối tượng extension.
        GDExample *self = (GDExample *)api.mem_alloc(sizeof(GDExample));
        gdexample_class_constructor(self);
        self->object = object;

        // Thiết lập instance của extension trong đối tượng Godot native.
        constructors.string_name_new_with_latin1_chars(&class_name, "GDExample", false);
        api.object_set_instance(object, &class_name, self);
        api.object_set_instance_binding(object, class_library, self, &gdexample_class_binding_callbacks);
        destructors.string_name_destructor(&class_name);

        return object;
    }

    void gdexample_class_free_instance(void *p_class_userdata, GDExtensionClassInstancePtr p_instance)
    {
        if (p_instance == NULL)
        {
            return;
        }
        GDExample *self = (GDExample *)p_instance;
        gdexample_class_destructor(self);
        api.mem_free(self);
    }

Khi khởi tạo một đối tượng, trước tiên chúng ta tạo một đối tượng Sprite2D mới, vì đó là lớp cha của lớp chúng ta. Sau đó, chúng ta cấp phát bộ nhớ cho struct tùy chỉnh và gọi constructor của nó. Như đã đề cập trước đó, chúng ta cũng lưu con trỏ đến đối tượng Godot trong struct.

Sau đó, chúng ta thiết lập struct tùy chỉnh làm dữ liệu instance. Việc này giúp Godot biết rằng đối tượng là một instance của lớp tùy chỉnh, đồng thời gọi đúng các phương thức tùy chỉnh của chúng ta, cũng như truyền dữ liệu này trở lại.

Lưu ý rằng chúng ta trả về đối tượng Godot đã tạo, không phải struct tùy chỉnh.

Đối với hàm ``gdextension_free_instance()``, chúng ta chỉ gọi destructor và giải phóng bộ nhớ đã cấp phát cho dữ liệu tùy chỉnh. Không cần hủy đối tượng Godot, vì engine sẽ tự xử lý việc đó.

Một dự án minh họa
------------------

Giờ đây, khi đã có thể tạo và giải phóng đối tượng tùy chỉnh, chúng ta có thể thử đối tượng này trong một dự án thực tế. Để làm vậy, hãy mở Godot và tạo một dự án mới trong thư mục ``project``. Trình quản lý dự án có thể cảnh báo rằng thư mục không trống nếu bạn đã biên dịch extension trước đó; lần này bạn có thể bỏ qua cảnh báo này.

Nếu bạn vẫn chưa biên dịch extension, bây giờ là lúc thực hiện việc đó. Hãy mở terminal hoặc command prompt, di chuyển đến thư mục gốc của extension và chạy ``scons``. Quá trình biên dịch sẽ diễn ra nhanh vì extension này rất đơn giản.

Sau đó, tạo một tệp có tên ``gdexample.gdextension`` bên trong thư mục ``project``. Đây là một resource của Godot mô tả extension, cho phép engine tải extension đúng cách. Đặt nội dung sau vào tệp này:

.. code-block::

    [configuration]

    entry_symbol = "gdexample_library_init"
    compatibility_minimum = "4.2"

    [libraries]
    macos.debug = "res://bin/libgdexample.dylib"
    linux.debug = "res://bin/libgdexample.so"
    windows.debug = "res://bin/libgdexample.dll"

Như bạn thấy, ``gdexample_library_init()`` là tên giống với hàm chúng ta đã định nghĩa trong tệp ``init.c``. Điều quan trọng là các tên phải khớp nhau, vì đây là cách Godot gọi entry point của extension.

Chúng ta cũng đặt mức tương thích tối thiểu là 4.2, vì đang nhắm đến phiên bản này. Extension vẫn sẽ hoạt động trên các phiên bản mới hơn. Nếu bạn đang sử dụng phiên bản Godot mới hơn và phụ thuộc vào các tính năng mới, bạn cần tăng giá trị này lên số phiên bản có đầy đủ mọi thứ bạn sử dụng. Xem :ref:`doc_what_is_gdextension_version_compatibility` để biết thêm thông tin.

Trong phần ``[libraries]``, chúng ta thiết lập các đường dẫn đến shared library trên những nền tảng khác nhau. Ở đây chỉ có các phiên bản debug vì đó là phần chúng ta đang thực hiện cho ví dụ này. Bằng cách sử dụng :ref:`feature tags <doc_feature_tags>`, bạn có thể tinh chỉnh để cung cấp cả các phiên bản release, thêm nhiều hệ điều hành đích hơn, cũng như cung cấp binary 32-bit và 64-bit.

Bạn cũng có thể thêm các dependency của library và icon tùy chỉnh cho các class trong tệp này, nhưng nội dung đó nằm ngoài phạm vi của tutorial này.

Sau khi lưu tệp, hãy quay lại editor. Godot sẽ tự động tải extension. Sẽ không có gì hiển thị vì extension của chúng ta chỉ đăng ký một class mới. Để sử dụng class này, hãy thêm một ``Node2D`` làm root của scene. Di chuyển nó vào giữa viewport để dễ nhìn hơn. Sau đó, thêm một node con mới vào root và trong hộp thoại **Create New Node**, tìm kiếm "GDExample", là tên class của chúng ta; class này sẽ được liệt kê ở đó. Nếu không thấy, nghĩa là Godot chưa tải extension đúng cách. Hãy thử khởi động lại editor và thực hiện lại các bước để kiểm tra xem có bước nào bị bỏ sót hay không.

Class tùy chỉnh của chúng ta kế thừa từ ``Sprite2D``, vì vậy nó có thuộc tính **Texture** trong Inspector. Hãy đặt thuộc tính này thành tệp ``icon.svg`` mà Godot đã thuận tiện tạo cho chúng ta khi tạo dự án. Lưu scene này dưới tên ``main.tscn`` và chạy nó. Bạn có thể đặt scene này làm scene chính để thuận tiện hơn.

.. image:: img/gdextension_c_running.webp

Voilà! Chúng ta đã có một node tùy chỉnh chạy trong Godot. Tuy nhiên, nó chưa làm gì và không có điểm gì khác biệt so với một node ``Sprite2D`` thông thường. Tiếp theo, chúng ta sẽ khắc phục điều đó bằng cách thêm các phương thức và thuộc tính tùy chỉnh.

Các phương thức tùy chỉnh
-------------------------

Một việc thường làm trong extension là tạo các phương thức cho những class tùy chỉnh và expose chúng thông qua Godot API. Chúng ta sẽ tạo một vài getter và setter cần thiết để bind các thuộc tính sau này.

Trước tiên, hãy thêm các field mới vào struct để lưu các giá trị của ``amplitude`` và ``speed``, những giá trị mà chúng ta sẽ sử dụng sau này khi tạo behavior cho node. Thêm chúng vào tệp ``gdexample.h``, bằng cách thay đổi struct ``GDExample``:

.. code-block:: c

    ...

    typedef struct
    {
        // Các thuộc tính public.
        double amplitude;
        double speed;
        // Metadata.
        GDExtensionObjectPtr object; // Lưu đối tượng Godot nền tảng.
    } GDExample;

    ...


Trong cùng tệp đó, hãy thêm phần khai báo cho các getter và setter ngay sau destructor.

.. code-block:: c

    ...

    // Destructor cho node.
    void gdexample_class_destructor(GDExample *self);

    // Các thuộc tính.
    void gdexample_class_set_amplitude(GDExample *self, double amplitude);
    double gdexample_class_get_amplitude(const GDExample *self);
    void gdexample_class_set_speed(GDExample *self, double speed);
    double gdexample_class_get_speed(const GDExample *self);

    ...

Trong tệp ``gdexample.c``, chúng ta sẽ khởi tạo các giá trị này trong constructor và thêm phần triển khai cho những hàm mới đó; các hàm này khá đơn giản:

.. code-block:: c

    void gdexample_class_constructor(GDExample *self)
    {
        self->amplitude = 10.0;
        self->speed = 1.0;
    }

    void gdexample_class_set_amplitude(GDExample *self, double amplitude)
    {
        self->amplitude = amplitude;
    }

    double gdexample_class_get_amplitude(const GDExample *self)
    {
        return self->amplitude;
    }

    void gdexample_class_set_speed(GDExample *self, double speed)
    {
        self->speed = speed;
    }

    double gdexample_class_get_speed(const GDExample *self)
    {
        return self->speed;
    }

Để các hàm đơn giản đó hoạt động khi được Godot gọi, chúng ta sẽ cần một số wrapper giúp chuyển đổi dữ liệu đúng cách giữa chúng ta và engine.

Trước tiên, chúng ta sẽ tạo các wrapper cho ``ptrcall``. Godot sử dụng kiểu này khi các kiểu của giá trị được biết chính xác, nhờ đó tránh phải dùng Variant. Chúng ta sẽ cần hai wrapper: một cho các hàm không nhận đối số và trả về ``double`` (dành cho getter), và một cho các hàm nhận một đối số ``double`` duy nhất nhưng không trả về gì (dành cho setter).

Thêm phần khai báo vào tệp ``api.h``:

.. code-block:: c

    void ptrcall_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);
    void ptrcall_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);


Hai hàm này tuân theo kiểu ``GDExtensionClassMethodPtrCall``, được định nghĩa trong ``gdextension_interface.h``. Ở đây, chúng ta dùng ``float`` làm tên vì trong Godot, kiểu ``float`` có độ chính xác kép, nên chúng ta giữ theo quy ước này.

Sau đó, chúng ta triển khai các hàm này trong tệp ``api.c``:

.. code-block:: c

    void ptrcall_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // Gọi hàm.
        double (*function)(void *) = method_userdata;
        *((double *)r_ret) = function(p_instance);
    }

    void ptrcall_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // Gọi hàm.
        void (*function)(void *, double) = method_userdata;
        function(p_instance, *((double *)p_args[0]));
    }

Đối số ``method_userdata`` là một giá trị tùy chỉnh mà chúng ta cung cấp cho Godot; trong trường hợp này, chúng ta sẽ đặt nó làm con trỏ hàm cho hàm muốn gọi. Vì vậy, trước tiên chúng ta chuyển nó sang kiểu hàm, sau đó chỉ cần gọi hàm bằng cách truyền các đối số khi cần hoặc thiết lập giá trị trả về.

Đối số ``p_instance`` chứa instance tùy chỉnh của class chúng ta, được truyền bằng ``object_set_instance()`` khi tạo đối tượng.

``p_args`` là một mảng các đối số. Lưu ý rằng mảng này chứa các **con trỏ** đến các giá trị. Đó là lý do chúng ta giải tham chiếu nó khi truyền vào các hàm. Số lượng đối số sẽ được khai báo khi binding function (chúng ta sẽ thực hiện việc này ngay sau đây) và sẽ luôn bao gồm các đối số mặc định nếu có.

Cuối cùng, ``r_ret`` là một con trỏ đến biến nơi cần đặt giá trị trả về. Giống như các đối số, nó sẽ có đúng kiểu đã khai báo. Đối với hàm không trả về giá trị, chúng ta phải tránh thiết lập nó.

Lưu ý rằng kiểu và số lượng đối số phải chính xác, vì vậy nếu cần các kiểu khác nhau, chẳng hạn, chúng ta sẽ phải tạo thêm các wrapper. Việc này có thể được tự động hóa bằng cách sử dụng code generation, nhưng nằm ngoài phạm vi của tutorial này.

Trong khi các hàm ``ptrcall`` được sử dụng khi các kiểu là chính xác, đôi khi Godot không thể biết liệu có phải như vậy hay không (khi lệnh gọi đến từ một ngôn ngữ có kiểu động, chẳng hạn như GDScript). Trong những trường hợp đó, nó sử dụng các hàm ``call`` thông thường, vì vậy chúng ta cũng cần cung cấp chúng khi binding.

Cuối cùng, hãy tạo hai wrapper mới trong file ``api.h``:

.. code-block:: c

    void call_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error);
    void call_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error);

Các hàm này tuân theo kiểu ``GDExtensionClassMethodCall``, có một chút khác biệt. Trước tiên, bạn nhận được các con trỏ đến Variant thay vì các kiểu cụ thể. Ngoài ra còn có số lượng đối số và một struct lỗi mà bạn có thể thiết lập nếu có sự cố.

Để kiểm tra kiểu và trích xuất giá trị từ Variant, chúng ta sẽ cần thêm một vài hàm từ GDExtension API. Vì vậy, hãy mở rộng các struct wrapper của chúng ta:

.. code-block:: c

    extern struct Constructors {
        ...
        GDExtensionVariantFromTypeConstructorFunc variant_from_float_constructor;
        GDExtensionTypeFromVariantConstructorFunc float_from_variant_constructor;
    } constructors;

    extern struct API
    {
        ...
        GDExtensionInterfaceGetVariantFromTypeConstructor get_variant_from_type_constructor;
        GDExtensionInterfaceGetVariantToTypeConstructor get_variant_to_type_constructor;
        GDExtensionInterfaceVariantGetType variant_get_type;
    } api;

Tên của các hàm đã cho biết đầy đủ chức năng của chúng. Chúng ta có một vài constructor để tạo và trích xuất một giá trị dấu phẩy động vào và ra khỏi Variant. Chúng ta cũng có một vài helper để thực sự lấy các constructor đó, cùng với một hàm để xác định kiểu của một Variant.

Hãy lấy chúng từ API, giống như trước đây, bằng cách thay đổi hàm ``load_api()`` trong file ``api.c``:

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        ...

        // API.
        ...
        api.get_variant_from_type_constructor = (GDExtensionInterfaceGetVariantFromTypeConstructor)p_get_proc_address("get_variant_from_type_constructor");
        api.get_variant_to_type_constructor = (GDExtensionInterfaceGetVariantToTypeConstructor)p_get_proc_address("get_variant_to_type_constructor");
        api.variant_get_type = (GDExtensionInterfaceVariantGetType)p_get_proc_address("variant_get_type");
        ...

        // Các constructor.
        ...
        constructors.variant_from_float_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_FLOAT);
        constructors.float_from_variant_constructor = api.get_variant_to_type_constructor(GDEXTENSION_VARIANT_TYPE_FLOAT);
        ...
    }

Bây giờ đã thiết lập xong các thành phần này, chúng ta có thể triển khai các wrapper lệnh gọi trong cùng file:

.. code-block:: c

    void call_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error)
    {
        // Kiểm tra số lượng đối số.
        if (p_argument_count != 0)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_TOO_MANY_ARGUMENTS;
            r_error->expected = 0;
            return;
        }

        // Gọi hàm.
        double (*function)(void *) = method_userdata;
        double result = function(p_instance);
        // Thiết lập Variant kết quả.
        constructors.variant_from_float_constructor(r_return, &result);
    }

    void call_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error)
    {
        // Kiểm tra số lượng đối số.
        if (p_argument_count < 1)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_TOO_FEW_ARGUMENTS;
            r_error->expected = 1;
            return;
        }
        else if (p_argument_count > 1)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_TOO_MANY_ARGUMENTS;
            r_error->expected = 1;
            return;
        }

        // Kiểm tra kiểu của đối số.
        GDExtensionVariantType type = api.variant_get_type(p_args[0]);
        if (type != GDEXTENSION_VARIANT_TYPE_FLOAT)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_INVALID_ARGUMENT;
            r_error->expected = GDEXTENSION_VARIANT_TYPE_FLOAT;
            r_error->argument = 0;
            return;
        }

        // Trích xuất đối số.
        double arg1;
        constructors.float_from_variant_constructor(&arg1, (GDExtensionVariantPtr)p_args[0]);

        // Gọi hàm.
        void (*function)(void *, double) = method_userdata;
        function(p_instance, arg1);
    }

Các hàm này dài hơn một chút nhưng dễ theo dõi. Trước tiên, chúng kiểm tra xem số lượng đối số có đúng như mong đợi hay không; nếu không, chúng thiết lập struct lỗi rồi trả về. Đối với hàm có một tham số, nó cũng kiểm tra xem kiểu đối số có chính xác hay không. Điều này rất quan trọng vì kiểu không khớp khi trích xuất từ Variant có thể gây ra crash.

Sau đó, hàm tiếp tục trích xuất đối số bằng constructor mà chúng ta đã thiết lập trước đó. Hàm không có đối số thay vào đó sẽ thiết lập giá trị trả về sau khi gọi hàm. Lưu ý rằng chúng sử dụng một con trỏ đến biến ``double``, vì đây là điều mà các constructor đó yêu cầu.

Trước khi thực sự binding các method, chúng ta cần một cách để tạo các instance ``GDExtensionPropertyInfo``. Mặc dù có thể thực hiện việc này bên trong các hàm binding mà chúng ta sẽ triển khai sau, việc có một helper sẽ dễ dàng hơn vì chúng ta sẽ cần nó nhiều lần, bao gồm cả khi binding các property.

Hãy tạo hai hàm này trong file ``api.h``:

.. code-block:: c

    // Tạo một struct PropertyInfo.
    GDExtensionPropertyInfo make_property(
        GDExtensionVariantType type,
        const char *name);

    GDExtensionPropertyInfo make_property_full(
        GDExtensionVariantType type,
        const char *name,
        uint32_t hint,
        const char *hint_string,
        const char *class_name,
        uint32_t usage_flags);

    void destruct_property(GDExtensionPropertyInfo *info);

Hàm đầu tiên là phiên bản đơn giản hóa của hàm thứ hai, vì thông thường chúng ta không cần tất cả các đối số cho property và có thể dùng các giá trị mặc định. Sau đó, chúng ta cũng có một hàm để hủy PropertyInfo, vì cần tạo các String và StringName phải được giải phóng đúng cách.

Nhân tiện, chúng ta cũng cần một cách để tạo và hủy String, vì vậy sẽ bổ sung vào các struct hiện có trong cùng file này. Chúng ta cũng sẽ lấy một hàm API mới để thực sự binding custom method của mình.

.. code-block:: c

    extern struct Constructors
    {
        ...
        GDExtensionInterfaceStringNewWithUtf8Chars string_new_with_utf8_chars;
    } constructors;

    extern struct Destructors
    {
        ...
        GDExtensionPtrDestructor string_destructor;
    } destructors;

    extern struct API
    {
        ...
        GDExtensionInterfaceClassdbRegisterExtensionClassMethod classdb_register_extension_class_method;
    } api;

Trước khi triển khai các hàm đó, hãy tạm dừng một chút trong file ``defs.h`` và thêm kích thước của kiểu ``String`` cùng với một vài enum:

.. code-block:: c

    // Có thể lấy các kích thước này từ file extension_api.json.
    #ifdef BUILD_32
    #define STRING_SIZE 4
    #define STRING_NAME_SIZE 4
    #else
    #define STRING_SIZE 8
    #define STRING_NAME_SIZE 8
    #endif

    ...

    typedef struct
    {
        uint8_t data[STRING_SIZE];
    } String;

    // Các enum.

    typedef enum
    {
        PROPERTY_HINT_NONE = 0,
    } PropertyHint;

    typedef enum
    {
        PROPERTY_USAGE_NONE = 0,
        PROPERTY_USAGE_STORAGE = 2,
        PROPERTY_USAGE_EDITOR = 4,
        PROPERTY_USAGE_DEFAULT = PROPERTY_USAGE_STORAGE | PROPERTY_USAGE_EDITOR,
    } PropertyUsageFlags;

Mặc dù có cùng kích thước với ``StringName``, việc sử dụng một tên khác cho nó sẽ rõ ràng hơn.

Các enum ở đây chỉ là những helper dùng để đặt tên cho các số mà chúng đại diện. Thông tin về chúng có trong file ``extension_api.json``. Ở đây, chúng ta chỉ thiết lập những enum cần cho tutorial để giữ cho nội dung ngắn gọn hơn.

Tiếp theo, trong ``api.c``, chúng ta cần tải các con trỏ đến những hàm mới đã thêm vào API.

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        ...
        // API
        ...
        api.classdb_register_extension_class_method = (GDExtensionInterfaceClassdbRegisterExtensionClassMethod)p_get_proc_address("classdb_register_extension_class_method");

        // Các constructor.
        ...
        constructors.string_new_with_utf8_chars = (GDExtensionInterfaceStringNewWithUtf8Chars)p_get_proc_address("string_new_with_utf8_chars");

        // Các destructor.
        ...
        destructors.string_destructor = variant_get_ptr_destructor(GDEXTENSION_VARIANT_TYPE_STRING);
    }

Sau đó, chúng ta cũng có thể triển khai các hàm để tạo struct ``PropertyInfo``.

.. code-block:: c

    GDExtensionPropertyInfo make_property(
        GDExtensionVariantType type,
        const char *name)
    {

        return make_property_full(type, name, PROPERTY_HINT_NONE, "", "", PROPERTY_USAGE_DEFAULT);
    }

    GDExtensionPropertyInfo make_property_full(
        GDExtensionVariantType type,
        const char *name,
        uint32_t hint,
        const char *hint_string,
        const char *class_name,
        uint32_t usage_flags)
    {

        StringName *prop_name = api.mem_alloc(sizeof(StringName));
        constructors.string_name_new_with_latin1_chars(prop_name, name, false);
        String *prop_hint_string = api.mem_alloc(sizeof(String));
        constructors.string_new_with_utf8_chars(prop_hint_string, hint_string);
        StringName *prop_class_name = api.mem_alloc(sizeof(StringName));
        constructors.string_name_new_with_latin1_chars(prop_class_name, class_name, false);

        GDExtensionPropertyInfo info = {
            .name = prop_name,
            .type = type,
            .hint = hint,
            .hint_string = prop_hint_string,
            .class_name = prop_class_name,
            .usage = usage_flags,
        };

        return info;
    }

    void destruct_property(GDExtensionPropertyInfo *info)
    {
        destructors.string_name_destructor(info->name);
        destructors.string_destructor(info->hint_string);
        destructors.string_name_destructor(info->class_name);
        api.mem_free(info->name);
        api.mem_free(info->hint_string);
        api.mem_free(info->class_name);
    }


Phiên bản đơn giản của ``make_property()`` chỉ gọi phiên bản đầy đủ hơn với một số đối số mặc định. Ý nghĩa chính xác của các giá trị đó nằm ngoài phạm vi của tutorial này; hãy xem trang về lớp :ref:`Object class <doc_object_class>` để biết thêm chi tiết về việc binding các method và property.

Phiên bản đầy đủ phức tạp hơn. Trước tiên, nó tạo các ``String`` và ``StringName`` cho những trường cần thiết bằng cách cấp phát bộ nhớ và gọi constructor của chúng. Sau đó, nó tạo một struct ``GDExtensionPropertyInfo`` và thiết lập tất cả các trường bằng những đối số được cung cấp. Cuối cùng, nó trả về struct vừa tạo.

Hàm ``destruct_property()`` khá đơn giản: nó chỉ gọi các destructor cho những đối tượng đã tạo và giải phóng bộ nhớ được cấp phát cho chúng.

Hãy quay lại header ``api.h`` để tạo các hàm thực sự binding các method:

.. code-block:: c

    // Phiên bản cho 0 đối số, có giá trị trả về.
    void bind_method_0_r(
        const char *class_name,
        const char *method_name,
        void *function,
        GDExtensionVariantType return_type);

    // Phiên bản cho 1 đối số, không có giá trị trả về.
    void bind_method_1(
        const char *class_name,
        const char *method_name,
        void *function,
        const char *arg1_name,
        GDExtensionVariantType arg1_type);

Sau đó quay lại file ``api.c`` để triển khai các hàm này:

.. code-block:: c

    // Phiên bản cho 0 đối số, có giá trị trả về.
    void bind_method_0_r(
        const char *class_name,
        const char *method_name,
        void *function,
        GDExtensionVariantType return_type)
    {
        StringName method_name_string;
        constructors.string_name_new_with_latin1_chars(&method_name_string, method_name, false);

        GDExtensionClassMethodCall call_func = call_0_args_ret_float;
        GDExtensionClassMethodPtrCall ptrcall_func = ptrcall_0_args_ret_float;

        GDExtensionPropertyInfo return_info = make_property(return_type, "");

        GDExtensionClassMethodInfo method_info = {
            .name = &method_name_string,
            .method_userdata = function,
            .call_func = call_func,
            .ptrcall_func = ptrcall_func,
            .method_flags = GDEXTENSION_METHOD_FLAGS_DEFAULT,
            .has_return_value = true,
            .return_value_info = &return_info,
            .return_value_metadata = GDEXTENSION_METHOD_ARGUMENT_METADATA_NONE,
            .argument_count = 0,
        };

        StringName class_name_string;
        constructors.string_name_new_with_latin1_chars(&class_name_string, class_name, false);

        api.classdb_register_extension_class_method(class_library, &class_name_string, &method_info);

        // Hủy các thành phần.
        destructors.string_name_destructor(&method_name_string);
        destructors.string_name_destructor(&class_name_string);
        destruct_property(&return_info);
    }

    // Phiên bản cho 1 đối số, không có giá trị trả về.
    void bind_method_1(
        const char *class_name,
        const char *method_name,
        void *function,
        const char *arg1_name,
        GDExtensionVariantType arg1_type)
    {

        StringName method_name_string;
        constructors.string_name_new_with_latin1_chars(&method_name_string, method_name, false);

        GDExtensionClassMethodCall call_func = call_1_float_arg_no_ret;
        GDExtensionClassMethodPtrCall ptrcall_func = ptrcall_1_float_arg_no_ret;

        GDExtensionPropertyInfo args_info[] = {
            make_property(arg1_type, arg1_name),
        };
        GDExtensionClassMethodArgumentMetadata args_metadata[] = {
            GDEXTENSION_METHOD_ARGUMENT_METADATA_NONE,
        };

        GDExtensionClassMethodInfo method_info = {
            .name = &method_name_string,
            .method_userdata = function,
            .call_func = call_func,
            .ptrcall_func = ptrcall_func,
            .method_flags = GDEXTENSION_METHOD_FLAGS_DEFAULT,
            .has_return_value = false,
            .argument_count = 1,
            .arguments_info = args_info,
            .arguments_metadata = args_metadata,
        };

        StringName class_name_string;
        constructors.string_name_new_with_latin1_chars(&class_name_string, class_name, false);

        api.classdb_register_extension_class_method(class_library, &class_name_string, &method_info);

        // Hủy các thành phần.
        destructors.string_name_destructor(&method_name_string);
        destructors.string_name_destructor(&class_name_string);
        destruct_property(&args_info[0]);
    }

Cả hai hàm này rất giống nhau. Trước tiên, chúng tạo một ``StringName`` với tên phương thức. Đối tượng này được tạo trên stack vì chúng ta không cần giữ lại nó sau khi hàm kết thúc. Sau đó, chúng tạo các biến cục bộ để chứa ``call_func`` và ``ptrcall_func``, trỏ đến các hàm helper mà chúng ta đã định nghĩa trước đó.

Ở bước tiếp theo, chúng có khác nhau đôi chút. Hàm đầu tiên tạo một property cho giá trị trả về, có tên rỗng vì không cần đến tên này. Hàm còn lại tạo một mảng các property cho các đối số, trong trường hợp này có một phần tử duy nhất. Hàm này cũng có một mảng metadata, có thể được dùng nếu đối số có điều gì đó đặc biệt (ví dụ: nếu một giá trị ``int`` dài 32 bit thay vì mặc định là 64 bit).

Sau đó, chúng tạo ``GDExtensionClassMethodInfo`` với các trường bắt buộc cho từng trường hợp. Tiếp theo, chúng tạo một ``StringName`` cho tên class để liên kết phương thức với class. Sau đó, chúng gọi hàm API để thực sự bind phương thức này vào class. Cuối cùng, chúng hủy các object đã tạo vì không còn cần đến chúng nữa.

.. note::
    Các helper bind ở đây sử dụng những helper call mà chúng ta đã tạo trước đó, vì vậy hãy lưu ý rằng các helper call đó chỉ chấp nhận kiểu ``FLOAT`` của Godot (tương đương với ``double`` trong C). Nếu bạn định dùng cách này cho các kiểu khác, bạn cần kiểm tra kiểu của các đối số và kiểu trả về rồi chọn một function callback phù hợp. Ở đây chúng tôi tránh làm vậy chỉ để ví dụ không trở nên dài hơn nữa.

Bây giờ chúng ta đã có cách để bind các phương thức, nên có thể thực hiện việc đó trong custom class. Mở file ``gdexample.c`` và điền vào hàm ``gdexample_class_bind_methods()``:

.. code-block:: c

    void gdexample_class_bind_methods()
    {
        bind_method_0_r("GDExample", "get_amplitude", gdexample_class_get_amplitude, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_amplitude", gdexample_class_set_amplitude, "amplitude", GDEXTENSION_VARIANT_TYPE_FLOAT);

        bind_method_0_r("GDExample", "get_speed", gdexample_class_get_speed, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_speed", gdexample_class_set_speed, "speed", GDEXTENSION_VARIANT_TYPE_FLOAT);
    }

Vì hàm này đã được quy trình khởi tạo gọi, chúng ta có thể dừng tại đây. Hàm này đơn giản hơn nhiều sau khi chúng ta đã tạo toàn bộ cơ sở hạ tầng cần thiết để nó hoạt động. Bạn có thể thấy rằng việc triển khai các hàm bind trực tiếp ở đây sẽ chiếm khá nhiều chỗ và cũng khá lặp lại. Cách này cũng giúp việc thêm một phương thức khác trong tương lai dễ dàng hơn.

Nếu biên dịch code và mở lại project Godot, ban đầu sẽ không có gì khác biệt vì chúng ta chỉ thêm hai phương thức mới. Để đảm bảo chúng đã được đăng ký đúng cách, bạn có thể tìm ``GDExample`` trong phần trợ giúp của editor và xác minh rằng chúng có mặt trên trang tài liệu.

.. image:: img/gdextension_c_methods_doc.webp


Custom properties
-----------------

Vì getter và setter cho các property của chúng ta đã được bind, giờ đây chúng ta có thể tiếp tục tạo các property thực tế sẽ được hiển thị trong Inspector của editor Godot.

Với phần thiết lập khá đầy đủ ở phần trước, chỉ còn vài việc cần làm để có thể bind các property. Trước tiên, hãy lấy một hàm API mới trong file ``api.h``:


.. code-block:: c

    extern struct API {
        ...
        GDExtensionInterfaceClassdbRegisterExtensionClassProperty classdb_register_extension_class_property;
    } api;

Chúng ta cũng hãy khai báo một hàm tại đây để bind các property:

.. code-block:: c

    void bind_property(
        const char *class_name,
        const char *name,
        GDExtensionVariantType type,
        const char *getter,
        const char *setter);

Trong file ``api.c``, chúng ta có thể load hàm API mới:

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // API
        ...
        api.classdb_register_extension_class_property = (GDExtensionInterfaceClassdbRegisterExtensionClassProperty)p_get_proc_address("classdb_register_extension_class_property");

        ...
    }

Sau đó, chúng ta có thể triển khai hàm helper mới trong chính file này:

.. code-block:: c

    void bind_property(
        const char *class_name,
        const char *name,
        GDExtensionVariantType type,
        const char *getter,
        const char *setter)
    {
        StringName class_string_name;
        constructors.string_name_new_with_latin1_chars(&class_string_name, class_name, false);
        GDExtensionPropertyInfo info = make_property(type, name);
        StringName getter_name;
        constructors.string_name_new_with_latin1_chars(&getter_name, getter, false);
        StringName setter_name;
        constructors.string_name_new_with_latin1_chars(&setter_name, setter, false);

        api.classdb_register_extension_class_property(class_library, &class_string_name, &info, &setter_name, &getter_name);

        // Hủy các đối tượng.
        destructors.string_name_destructor(&class_string_name);
        destruct_property(&info);
        destructors.string_name_destructor(&getter_name);
        destructors.string_name_destructor(&setter_name);
    }

Hàm này tương tự hàm dùng để bind các phương thức. Điểm khác biệt chính là chúng ta không cần một struct bổ sung vì có thể sử dụng trực tiếp ``GDExtensionPropertyInfo`` được tạo bởi hàm helper, nên cách này đơn giản hơn. Hàm chỉ tạo các giá trị ``StringName`` từ các chuỗi C, tạo một struct thông tin property bằng helper của chúng ta, gọi hàm API để đăng ký property trong class, rồi hủy tất cả các object đã tạo.

Sau khi hoàn tất, chúng ta có thể mở rộng hàm ``gdexample_class_bind_methods()`` trong file ``gdexample.c``:

.. code-block:: c

    void gdexample_class_bind_methods()
    {
        bind_method_0_r("GDExample", "get_amplitude", gdexample_class_get_amplitude, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_amplitude", gdexample_class_set_amplitude, "amplitude", GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_property("GDExample", "amplitude", GDEXTENSION_VARIANT_TYPE_FLOAT, "get_amplitude", "set_amplitude");

        bind_method_0_r("GDExample", "get_speed", gdexample_class_get_speed, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_speed", gdexample_class_set_speed, "speed", GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_property("GDExample", "speed", GDEXTENSION_VARIANT_TYPE_FLOAT, "get_speed", "set_speed");
    }

Nếu build extension bằng ``scons``, bạn sẽ thấy property mới trong editor Godot, không chỉ trên trang tài liệu của custom class mà còn trong dock Inspector khi node ``GDExample`` được chọn.

.. image:: img/gdextension_c_inspector_properties.webp

Binding virtual methods
-----------------------

Custom node của chúng ta hiện đã có các property để điều chỉnh cách nó hoạt động, nhưng nó vẫn chưa làm gì cả. Trong phần này, chúng ta sẽ bind virtual method
:ref:`_process() <class_Node_private_method__process>` và làm cho custom sprite của chúng ta di chuyển một chút.

Trong file ``gdexample.h``, hãy thêm một hàm đại diện cho phương thức ``_process()`` tùy chỉnh:

.. code-block:: c

    // Các phương thức.
    void gdexample_class_process(GDExample *self, double delta);

Chúng ta cũng sẽ thêm một trường "private" để theo dõi thời gian đã trôi qua trong custom struct. Trường này chỉ là "private" theo nghĩa nó sẽ không được bind vào Godot API, mặc dù nó là public ở phía C vì ngôn ngữ này không có access modifier.

.. code-block:: c

    typedef struct
    {
        // Các property private.
        double time_passed;
        ...
    } GDExample;

Trong file source đối ứng ``gdexample.c``, chúng ta cần khởi tạo trường mới trong constructor:

.. code-block:: c

    void gdexample_class_constructor(GDExample *self)
    {
        self->time_passed = 0.0;
        self->amplitude = 10.0;
        self->speed = 1.0;
    }

Sau đó, chúng ta có thể tạo phần triển khai đơn giản nhất cho phương thức ``_process``:

.. code-block:: c

    void gdexample_class_process(GDExample *self, double delta)
    {
        self->time_passed += self->speed * delta;
    }

Hiện tại, hàm này chỉ cập nhật trường private mà chúng ta đã tạo. Chúng ta sẽ quay lại phần này sau khi phương thức được bind đúng cách.

Virtual method hơi khác so với các binding thông thường. Thay vì đăng ký rõ ràng chính phương thức đó, chúng ta sẽ đăng ký một hàm đặc biệt mà Godot sẽ gọi để hỏi xem một virtual method cụ thể có được triển khai trong extension của chúng ta hay không. Engine sẽ truyền một ``StringName`` làm đối số, vì vậy theo tinh thần của tutorial này, chúng ta sẽ tạo một hàm helper để kiểm tra xem nó có bằng một chuỗi C hay không.

Hãy thêm khai báo vào file ``api.h``:

.. code-block:: c

    // So sánh một StringName với một chuỗi C.
    bool is_string_name_equal(GDExtensionConstStringNamePtr p_a, const char *p_b);

Chúng ta cũng sẽ thêm một struct mới vào file này để chứa các function pointer cho những operator tùy chỉnh:

.. code-block:: c

    extern struct Operators
    {
        GDExtensionPtrOperatorEvaluator string_name_equal;
    } operators;

Sau đó, trong file ``api.c``, chúng ta sẽ load function pointer từ API:

.. code-block:: c

    struct Operators operators;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // Trước tiên lấy các hàm helper.
        ...
        GDExtensionInterfaceVariantGetPtrOperatorEvaluator variant_get_ptr_operator_evaluator = (GDExtensionInterfaceVariantGetPtrOperatorEvaluator)p_get_proc_address("variant_get_ptr_operator_evaluator");

        ...

        // Các operator.
        operators.string_name_equal = variant_get_ptr_operator_evaluator(GDEXTENSION_VARIANT_OP_EQUAL, GDEXTENSION_VARIANT_TYPE_STRING_NAME, GDEXTENSION_VARIANT_TYPE_STRING_NAME);
    }

Như bạn thấy, ở đây chúng ta cần một helper cục bộ mới để lấy function pointer cho operator.

Với thành phần này, chúng ta có thể dễ dàng tạo hàm so sánh trong cùng file:

.. code-block:: c

    bool is_string_name_equal(GDExtensionConstStringNamePtr p_a, const char *p_b)
    {
        // Tạo một StringName cho chuỗi C.
        StringName string_name;
        constructors.string_name_new_with_latin1_chars(&string_name, p_b, false);

        // So sánh hai StringName.
        bool is_equal = false;
        operators.string_name_equal(p_a, &string_name, &is_equal);

        // Hủy StringName đã tạo.
        destructors.string_name_destructor(&string_name);

        // Trả về kết quả.
        return is_equal;
    }

Hàm này tạo một ``StringName`` từ đối số, so sánh với đối tượng còn lại bằng function pointer của operator, rồi trả về kết quả. Lưu ý rằng giá trị trả về của operator được truyền dưới dạng một tham chiếu out; đây là cách làm phổ biến trong API.

Hãy quay lại tệp ``gdexample.h`` và thêm một vài hàm sẽ được dùng làm callback cho Godot API:

.. code-block:: c

    void *gdexample_class_get_virtual_with_data(void *p_class_userdata, GDExtensionConstStringNamePtr p_name);
    void gdexample_class_call_virtual_with_data(GDExtensionClassInstancePtr p_instance, GDExtensionConstStringNamePtr p_name, void *p_virtual_call_userdata, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);

Thực tế có hai cách đăng ký các virtual method. Chỉ một cách có phần ``get``, trong đó bạn cung cấp cho Godot một function pointer được tạo đúng cách để Godot gọi. Với cách này, chúng ta cần tạo thêm một helper cho mỗi virtual method, khá bất tiện. Thay vào đó, chúng ta dùng cách thứ hai, cho phép trả về bất kỳ dữ liệu nào; sau đó Godot sẽ gọi một callback thứ hai và trả lại dữ liệu này cùng với thông tin về lời gọi. Chúng ta chỉ cần cung cấp function pointer của mình làm custom data, rồi dùng một callback duy nhất cho tất cả virtual method. Mặc dù trong ví dụ này chúng ta chỉ dùng nó cho một method, cách này dễ mở rộng hơn.

Vậy hãy triển khai hai hàm đó trong tệp ``gdexample.c``:

.. code-block:: c

    void *gdexample_class_get_virtual_with_data(void *p_class_userdata, GDExtensionConstStringNamePtr p_name)
    {
        // Nếu đó là method "_process", hãy trả về con trỏ tới hàm gdexample_class_process.
        if (is_string_name_equal(p_name, "_process"))
        {
            return (void *)gdexample_class_process;
        }
        // Nếu không, hãy trả về NULL.
        return NULL;
    }

    void gdexample_class_call_virtual_with_data(GDExtensionClassInstancePtr p_instance, GDExtensionConstStringNamePtr p_name, void *p_virtual_call_userdata, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // Nếu đó là method "_process", hãy gọi nó bằng một helper.
        if (p_virtual_call_userdata == &gdexample_class_process)
        {
            ptrcall_1_float_arg_no_ret(p_virtual_call_userdata, p_instance, p_args, r_ret);
        }
    }

Sau khi đã tạo tất cả helper trước đó, các hàm này cũng khá đơn giản.

Với hàm đầu tiên, chúng ta chỉ cần kiểm tra xem tên hàm được yêu cầu có phải là ``_process`` hay không; nếu đúng, trả về function pointer tới phần triển khai của nó. Nếu không, chúng ta trả về ``NULL``, cho biết method này không được override. Ở đây chúng ta không dùng ``p_class_userdata`` vì hàm này chỉ dành cho một class và không có dữ liệu nào liên kết với nó.

Hàm thứ hai cũng tương tự. Nếu đó là method ``_process()``, hàm này dùng function pointer được cung cấp để gọi helper ``ptrcall``, chuyển tiếp các đối số của lời gọi. Nếu không, nó không làm gì cả vì chúng ta không triển khai virtual method nào khác.

Điều duy nhất còn thiếu là sử dụng các callback này khi đăng ký class. Hãy mở tệp ``init.c`` và thay đổi phần khởi tạo ``class_info`` để thêm chúng, thay cho giá trị ``NULL`` đã dùng trước đó:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        ...

        GDExtensionClassCreationInfo2 class_info = {
            ...
            .get_virtual_call_data_func = gdexample_class_get_virtual_with_data,
            .call_virtual_with_data_func = gdexample_class_call_virtual_with_data,
            ...
        };

        ...
    }

Như vậy là đủ để binding virtual method. Nếu build extension rồi chạy lại project Godot, hàm ``_process()`` sẽ được gọi. Tuy nhiên, bạn sẽ không nhận ra điều đó vì bản thân hàm chưa thực hiện hành động nào có thể quan sát được. Bây giờ chúng ta sẽ giải quyết việc này bằng cách làm cho custom node di chuyển theo một pattern.

Để node thực hiện được hành động, chúng ta cần gọi các method của Godot. Không chỉ các hàm GDExtension API như đã làm từ đầu đến giờ, mà còn cả các method thực tế của engine, giống như khi viết script. Điều này đương nhiên cần thêm một số bước thiết lập.

Trước tiên, hãy thêm :ref:`class_Vector2` vào tệp ``defs.h``, để chúng ta có thể dùng nó trong method của mình:

.. code-block:: c

    // Có thể lấy kích thước từ tệp extension_api.json.
    ...
    #ifdef REAL_T_IS_DOUBLE
    #define VECTOR2_SIZE 16
    #else
    #define VECTOR2_SIZE 8
    #endif

    ...

    // Các type.

    ...

    typedef struct
    {
        uint8_t data[VECTOR2_SIZE];
    } Vector2;

Define ``REAL_T_IS_DOUBLE`` chỉ cần thiết nếu phiên bản Godot của bạn được build với hỗ trợ double precision, vốn không phải thiết lập mặc định.

Bây giờ, trong tệp ``api.h``, chúng ta sẽ thêm một vài thành phần vào các struct API, bao gồm một struct mới để lưu các method của engine cần gọi.

.. code-block:: c

    extern struct Constructors
    {
        ...
        GDExtensionPtrConstructor vector2_constructor_x_y;
    } constructors;

    ...

    extern struct Methods
    {
        GDExtensionMethodBindPtr node2d_set_position;
    } methods;

    extern struct API
    {
        ...
        GDExtensionInterfaceClassdbGetMethodBind classdb_get_method_bind;
        GDExtensionInterfaceObjectMethodBindPtrcall object_method_bind_ptrcall;
    } api;

Sau đó, trong tệp ``api.c``, chúng ta có thể lấy các function pointer từ Godot:

.. code-block::

    struct Methods methods;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // Get helper functions first.
        ...
        GDExtensionInterfaceVariantGetPtrConstructor variant_get_ptr_constructor = (GDExtensionInterfaceVariantGetPtrConstructor)p_get_proc_address("variant_get_ptr_constructor");

        // API.
        ...
        api.classdb_get_method_bind = (GDExtensionInterfaceClassdbGetMethodBind)p_get_proc_address("classdb_get_method_bind");
        api.object_method_bind_ptrcall = (GDExtensionInterfaceObjectMethodBindPtrcall)p_get_proc_address("object_method_bind_ptrcall");

        // Constructors.
        ...
        constructors.vector2_constructor_x_y = variant_get_ptr_constructor(GDEXTENSION_VARIANT_TYPE_VECTOR2, 3); // See extension_api.json for indices.

        ...
    }

Phần đáng chú ý duy nhất ở đây là constructor ``Vector2``, với constructor này chúng ta yêu cầu index ``3``. Vì có nhiều constructor với các kiểu đối số khác nhau, chúng ta cần chỉ rõ constructor muốn dùng. Trong trường hợp này, chúng ta lấy constructor nhận hai số float làm tọa độ ``x`` và ``y``, do đó có tên như vậy. Có thể lấy index này từ tệp ``extension_api.json``. Lưu ý rằng chúng ta cũng cần một local helper mới để lấy nó.

Lưu ý rằng ở đây chúng ta không lấy gì cho struct methods. Lý do là hàm này được gọi quá sớm trong quá trình khởi tạo, nên các class chưa được đăng ký đầy đủ.

Thay vào đó, chúng ta sẽ dùng initialization level callback để lấy chúng khi đăng ký custom class. Hãy thêm đoạn này vào tệp ``init.c``:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        if (p_level != GDEXTENSION_INITIALIZATION_SCENE)
        {
            return;
        }

        // Lấy các method của ClassDB ở đây vì tất cả class chúng ta cần hiện đã được đăng ký đầy đủ.
        // Xem extension_api.json để biết các hash.
        StringName native_class_name;
        StringName method_name;

        constructors.string_name_new_with_latin1_chars(&native_class_name, "Node2D", false);
        constructors.string_name_new_with_latin1_chars(&method_name, "set_position", false);
        methods.node2d_set_position = api.classdb_get_method_bind(&native_class_name, &method_name, 743155724);
        destructors.string_name_destructor(&native_class_name);
        destructors.string_name_destructor(&method_name);

        ...
    }

Ở đây, chúng ta tạo các ``StringName`` cho class và method muốn lấy, sau đó dùng GDExtension API để truy xuất ``MethodBind`` của chúng; đây là một object đại diện cho bound method. Chúng ta lấy method ``set_position`` từ ``Node2D`` vì đây là nơi method được đăng ký, mặc dù chúng ta sẽ dùng nó trong một ``Sprite2D``, là class dẫn xuất.

Con số có vẻ ngẫu nhiên dùng để lấy bind thực ra là hash của method signature. Nhờ đó, Godot có thể khớp với method bạn yêu cầu ngay cả khi signature này thay đổi trong một phiên bản Godot tương lai, bằng cách cung cấp một compatibility method khớp với yêu cầu của bạn. Đây là một trong những hệ thống cho phép engine tải các extension được tạo cho những phiên bản trước. Bạn có thể lấy giá trị hash này từ tệp ``extension_api.json``.

Với tất cả những điều đó, cuối cùng chúng ta có thể triển khai method custom ``_process()`` trong tệp ``gdexample.c``:

.. code-block:: c

    ...

    #include <math.h>

    ...

    void gdexample_class_process(GDExample *self, double delta)
    {
        self->time_passed += self->speed * delta;

        Vector2 new_position;

        // Thiết lập các đối số cho constructor của Vector2.
        double x = self->amplitude + (self->amplitude * sin(self->time_passed * 2.0));
        double y = self->amplitude + (self->amplitude * cos(self->time_passed * 1.5));
        GDExtensionConstTypePtr args[] = {&x, &y};
        // Gọi constructor của Vector2.
        constructors.vector2_constructor_x_y(&new_position, args);

        // Thiết lập các đối số cho method set_position.
        GDExtensionConstTypePtr args2[] = {&new_position};
        // Gọi method set_position.
        api.object_method_bind_ptrcall(methods.node2d_set_position, self->object, args2, NULL);
    }

Sau khi cập nhật thời gian đã trôi qua, được scale theo property ``speed``, hàm này tạo các giá trị ``x`` và ``y`` dựa trên thời gian đó, đồng thời điều biến chúng theo property ``amplitude``. Đây là yếu tố tạo ra hiệu ứng pattern. Cần có header ``math.h`` cho các hàm ``sin()`` và ``cos()`` được dùng ở đây.

Sau đó, hàm thiết lập một mảng các đối số để tạo một ``Vector2``, rồi gọi constructor. Hàm thiết lập thêm một mảng đối số khác và dùng nó để gọi method ``set_position()`` thông qua bind đã lấy trước đó.

Vì không có phần nào ở đây cấp phát bộ nhớ nên không cần cleanup.

Bây giờ chúng ta có thể build lại extension và mở lại Godot. Ngay cả trong editor, bạn cũng sẽ thấy custom sprite di chuyển.

.. image:: img/gdextension_c_moving_sprite.gif

Hãy thử thay đổi các property **Speed** và **Amplitude**, rồi xem sprite phản ứng thế nào.

Đăng ký và phát signal
----------------------

Để hoàn tất tutorial này, hãy xem cách đăng ký một signal custom và phát signal đó vào thời điểm phù hợp. Như bạn có thể đoán, chúng ta sẽ cần thêm một vài function pointer từ API và nhiều helper function hơn.

Trong tệp ``api.h``, chúng ta sẽ thêm hai thứ. Một là hàm API để đăng ký signal, thứ còn lại là hàm helper để bọc việc liên kết signal.

.. code-block:: c

    extern struct API
    {
        ...
        GDExtensionInterfaceClassdbRegisterExtensionClassSignal classdb_register_extension_class_signal;
    } api;

    ...

    // Phiên bản cho 1 đối số.
    void bind_signal_1(
        const char *class_name,
        const char *signal_name,
        const char *arg1_name,
        GDExtensionVariantType arg1_type);

Trong trường hợp này, chúng ta chỉ có phiên bản cho một đối số, vì đó là phiên bản chúng ta sẽ sử dụng.

Chuyển sang tệp ``api.c``, chúng ta có thể tải con trỏ hàm mới này và triển khai helper:

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // API.
        ...
        api.classdb_register_extension_class_signal = (GDExtensionInterfaceClassdbRegisterExtensionClassSignal)p_get_proc_address("classdb_register_extension_class_signal");

        ...
    }

    void bind_signal_1(
        const char *class_name,
        const char *signal_name,
        const char *arg1_name,
        GDExtensionVariantType arg1_type)
    {
        StringName class_string_name;
        constructors.string_name_new_with_latin1_chars(&class_string_name, class_name, false);
        StringName signal_string_name;
        constructors.string_name_new_with_latin1_chars(&signal_string_name, signal_name, false);

        GDExtensionPropertyInfo args_info[] = {
            make_property(arg1_type, arg1_name),
        };

        api.classdb_register_extension_class_signal(class_library, &class_string_name, &signal_string_name, args_info, 1);

        // Giải phóng các đối tượng.
        destructors.string_name_destructor(&class_string_name);
        destructors.string_name_destructor(&signal_string_name);
        destruct_property(&args_info[0]);
    }

Hàm này rất giống với hàm dùng để liên kết các method. Điểm khác biệt chính là chúng ta không cần điền thêm một struct; chỉ cần truyền các tên cần thiết và mảng đối số. ``1`` ở cuối cho biết số lượng đối số mà signal cung cấp.

Với cách này, chúng ta có thể liên kết signal trong ``gdexample.c``:

.. code-block:: c

    void gdexample_class_bind_methods()
    {
        ...
        bind_signal_1("GDExample", "position_changed", "new_position", GDEXTENSION_VARIANT_TYPE_VECTOR2);
    }

Để phát một signal, chúng ta cần gọi
method :ref:`emit_signal() <class_Object_method_emit_signal>` trên node tùy chỉnh của mình. Vì đây là một hàm ``vararg`` (nghĩa là nhận số lượng đối số bất kỳ), chúng ta không thể sử dụng ``ptrcall``. Để thực hiện một lời gọi thông thường, chúng ta phải tạo các Variant, việc này cần thêm một vài bước kết nối.

Trước tiên, trong tệp ``defs.h``, chúng ta tạo định nghĩa cho Variant:

.. code-block:: c

    ...

    // Có thể lấy kích thước từ tệp extension_api.json.
    ...
    #ifdef REAL_T_IS_DOUBLE
    #define VARIANT_SIZE 40
    #define VECTOR2_SIZE 16
    #else
    #define VARIANT_SIZE 24
    #define VECTOR2_SIZE 8
    #endif

    ...

    // Các kiểu.

    ...

    typedef struct
    {
        uint8_t data[VARIANT_SIZE];
    } Variant;


Trước hết, chúng ta đặt kích thước của Variant cùng với kích thước của Vector2 mà chúng ta đã thêm trước đó. Sau đó, chúng ta dùng nó để tạo một struct opaque đủ lớn để chứa dữ liệu Variant. Một lần nữa, chúng ta đặt kích thước cho các bản build dùng độ chính xác kép làm phương án dự phòng, vì các bản build Godot chính thức sử dụng độ chính xác đơn.

Hàm ``emit_signal()`` sẽ được gọi với hai đối số. Đối số đầu tiên là tên của signal cần phát, còn đối số thứ hai là đối số chúng ta truyền đến các kết nối signal, cụ thể là một Vector2 như đã khai báo khi liên kết. Vì vậy, chúng ta sẽ tạo một hàm helper có thể gọi MethodBind với các kiểu này. Mặc dù hàm có trả về một giá trị (mã lỗi), chúng ta không cần xử lý nó, nên hiện tại sẽ bỏ qua.

Trong ``api.h``, chúng ta thêm một vài thành phần vào các struct hiện có, cùng với một hàm helper mới cho lời gọi:

.. code-block:: c

    extern struct Constructors
    {
        ...
        GDExtensionVariantFromTypeConstructorFunc variant_from_string_name_constructor;
        GDExtensionVariantFromTypeConstructorFunc variant_from_vector2_constructor;
    } constructors;

    extern struct Destructors
    {
        ..
        GDExtensionInterfaceVariantDestroy variant_destroy;
    } destructors;

    ...

    extern struct Methods
    {
        ...
        GDExtensionMethodBindPtr object_emit_signal;
    } methods;

    extern struct API
    {
        ...
        GDExtensionInterfaceObjectMethodBindCall object_method_bind_call;
    } api;

    ...

    // Helper để gọi với các đối số Variant.
    void call_2_args_stringname_vector2_no_ret_variant(
        GDExtensionMethodBindPtr p_method_bind,
        GDExtensionObjectPtr p_instance,
        const GDExtensionTypePtr p_arg1,
        const GDExtensionTypePtr p_arg2);

Bây giờ hãy chuyển sang tệp ``api.c`` để tải các con trỏ hàm mới này và triển khai hàm helper.

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // API.
        ...
        api.object_method_bind_call = (GDExtensionInterfaceObjectMethodBindCall)p_get_proc_address("object_method_bind_call");

        // Các hàm khởi tạo.
        ...
        constructors.variant_from_string_name_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_STRING_NAME);
        constructors.variant_from_vector2_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_VECTOR2);

        // Các hàm hủy.
        ...
        destructors.variant_destroy = (GDExtensionInterfaceVariantDestroy)p_get_proc_address("variant_destroy");

        ...
    }

    ...

    void call_2_args_stringname_vector2_no_ret_variant(GDExtensionMethodBindPtr p_method_bind, GDExtensionObjectPtr p_instance, const GDExtensionTypePtr p_arg1, const GDExtensionTypePtr p_arg2)
    {
        // Thiết lập các đối số cho lời gọi.
        Variant arg1;
        constructors.variant_from_string_name_constructor(&arg1, p_arg1);
        Variant arg2;
        constructors.variant_from_vector2_constructor(&arg2, p_arg2);
        GDExtensionConstVariantPtr args[] = {&arg1, &arg2};

        // Thêm vùng lưu trữ cho giá trị trả về giả.
        Variant ret;

        // Gọi hàm.
        api.object_method_bind_call(p_method_bind, p_instance, args, 2, &ret, NULL);

        // Giải phóng các đối số.
        destructors.variant_destroy(&arg1);
        destructors.variant_destroy(&arg2);
        destructors.variant_destroy(&ret);
    }

Hàm helper này có một số đoạn mã khuôn mẫu nhưng khá dễ hiểu. Hàm thiết lập hai đối số bên trong các Variant được cấp phát trên stack, sau đó tạo một mảng chứa các con trỏ đến chúng. Hàm cũng thiết lập một Variant khác để lưu giá trị trả về; chúng ta không cần khởi tạo Variant này vì lời gọi yêu cầu nó ở trạng thái chưa khởi tạo.

Sau đó, hàm thực sự gọi MethodBind bằng instance và các đối số mà chúng ta đã cung cấp. ``NULL`` ở cuối sẽ là một con trỏ đến một struct ``GDExtensionCallError``. Nó có thể được dùng để xử lý các lỗi tiềm ẩn khi gọi hàm (chẳng hạn như đối số không đúng). Để đơn giản, chúng ta sẽ không xử lý lỗi đó ở đây.

Cuối cùng, chúng ta cần giải phóng các Variant đã tạo. Mặc dù về mặt kỹ thuật, Variant Vector2 không cần được giải phóng, việc dọn dẹp tất cả sẽ rõ ràng hơn.

Chúng ta cũng cần tải MethodBind, việc này sẽ được thực hiện trong tệp ``init.c``, ngay sau khi tải MethodBind cho method ``set_position`` mà chúng ta đã làm trước đó:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        ...

        constructors.string_name_new_with_latin1_chars(&native_class_name, "Object", false);
        constructors.string_name_new_with_latin1_chars(&method_name, "emit_signal", false);
        methods.object_emit_signal = api.classdb_get_method_bind(&native_class_name, &method_name, 4047867050);
        destructors.string_name_destructor(&native_class_name);
        destructors.string_name_destructor(&method_name);

        // Đăng ký class.
        ...
    }

Lưu ý rằng ở đây chúng ta sử dụng lại các biến ``native_class_name`` và ``method_name``, nên không cần khai báo biến mới.

Bây giờ hãy mở tệp ``gdexample.h``, nơi chúng ta sẽ thêm một vài trường:

.. code-block:: c

    typedef struct
    {
        // Các thuộc tính private.
        ..
        double time_emit;
        ..
        // Metadata.
        StringName position_changed; // Cho signal.
    } GDExample;

Trường đầu tiên sẽ lưu khoảng thời gian đã trôi qua kể từ lần signal cuối cùng được phát, vì chúng ta sẽ phát signal theo các khoảng thời gian đều đặn. Trường còn lại chỉ dùng để cache tên signal, ताकि không cần tạo một StringName mới mỗi lần.

Trong tệp mã nguồn ``gdexample.c``, chúng ta có thể thay đổi hàm khởi tạo và hàm hủy để xử lý các trường mới:

.. code-block:: c

    void gdexample_class_constructor(GDExample *self)
    {
        ...
        self->time_emit = 0.0;

        // Tạo StringName cho signal.
        constructors.string_name_new_with_latin1_chars(&self->position_changed, "position_changed", false);
    }

    void gdexample_class_destructor(GDExample *self)
    {
        // Giải phóng StringName cho signal.
        destructors.string_name_destructor(&self->position_changed);
    }

Điều quan trọng là phải giải phóng StringName để tránh rò rỉ bộ nhớ.

Bây giờ chúng ta có thể thêm vào hàm ``gdexample_class_process()`` để thực sự phát signal:

.. code-block:: c

    void gdexample_class_process(GDExample *self, double delta)
    {
        ...

        self->time_emit += delta;
        if (self->time_emit >= 1.0)
        {
            // Gọi method emit_signal.
            call_2_args_stringname_vector2_no_ret_variant(methods.object_emit_signal, self->object, &self->position_changed, &new_position);
            self->time_emit = 0.0;
        }
    }

Thao tác này cập nhật thời gian đã trôi qua cho việc phát signal và nếu thời gian đó vượt quá một giây, nó sẽ gọi hàm ``emit_signal()`` trên instance hiện tại, truyền tên signal và vị trí mới làm các đối số.

Bây giờ chúng ta đã hoàn tất C GDExtension. Hãy build lại một lần nữa và mở lại project Godot trong editor.

Trong trang tài liệu của ``GDExample``, bạn có thể thấy signal mới mà chúng ta đã liên kết:

.. image:: img/gdextension_c_signal_doc.webp

Để kiểm tra xem nó có hoạt động không, hãy thêm một script nhỏ vào node gốc, là node cha của node tùy chỉnh, để in vị trí ra output mỗi khi nhận được signal:

.. code-block:: gdscript

    extends Node2D

    func _ready():
        $GDExample.position_changed.connect(on_position_changed)

    func on_position_changed(new_position):
        prints("New position:", new_position)

Chạy project, bạn có thể quan sát các giá trị được in trong dock Output của trình chỉnh sửa:

.. image:: img/gdextension_c_signal_print.webp

Kết luận
--------

Tutorial này trình bày một extension cơ bản với các method, property và signal tùy chỉnh. Mặc dù cần khá nhiều boilerplate, extension vẫn có thể mở rộng tốt bằng cách tạo các hàm trợ giúp để xử lý những tác vụ tẻ nhạt.

Đây sẽ là nền tảng tốt để hiểu API GDExtension và là điểm khởi đầu để tạo các binding generator tùy chỉnh. Trên thực tế, có thể tạo binding cho C bằng loại generator này, khiến phần code thực tế trông giống hơn với file ``gdexample.c`` trong ví dụ này, vốn khá đơn giản và không quá dài dòng.

Nếu muốn tạo các extension thực tế, bạn nên sử dụng binding C++ thay vào đó, vì chúng loại bỏ toàn bộ boilerplate khỏi code của bạn. Hãy xem
:ref:`tài liệu godot-cpp <doc_godot_cpp>` để tìm hiểu cách thực hiện.
