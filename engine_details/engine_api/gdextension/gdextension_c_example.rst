.. _doc_gdextension_c_example:

Ví dụ GDExtension bằng C
========================

Giới thiệu
----------

Đây là một ví dụ đơn giản về cách làm việc trực tiếp với GDExtension bằng mã C. Lưu ý rằng API này không được thiết kế để sử dụng trực tiếp, vì vậy ví dụ này chắc chắn sẽ khá dài dòng và cần nhiều bước, ngay cả với một ví dụ nhỏ. Tuy nhiên, nó đóng vai trò như tài liệu tham khảo để tạo binding cho một ngôn ngữ khác. Bạn vẫn có thể sử dụng API trực tiếp nếu muốn, điều này có thể thuận tiện khi chỉ cần tạo binding cho một thư viện bên thứ ba.

Trong ví dụ này, chúng ta sẽ tạo một node tùy chỉnh để di chuyển một sprite trên màn hình dựa trên các tham số do người dùng cung cấp. Dù rất đơn giản, ví dụ này cho thấy cách thực hiện một số việc với GDExtension, chẳng hạn như đăng ký các lớp tùy chỉnh cùng với phương thức, thuộc tính và tín hiệu. Qua đó, bạn có thể hiểu rõ hơn về API GDExtension.

Thiết lập dự án
---------------

Bạn sẽ cần một số điều kiện tiên quyết sau:

- một tệp thực thi Godot 4.2 (hoặc mới hơn), - một trình biên dịch C, - SCons làm công cụ build.

Vì chúng ta sử dụng API trực tiếp nên không cần dùng `godot-cpp repository <https://github.com/godotengine/godot-cpp>`__.

Cấu trúc tệp
------------

Để sắp xếp các tệp, chúng ta sẽ chủ yếu chia chúng thành hai thư mục:

.. code-block:: none

    gdextension_c_example/
    |
    +--project/                  # game example/demo to test the extension
    |
    +--src/                   # source code of the extension we are building

Chúng ta cũng cần một bản sao của tệp header ``gdextension_interface.h`` từ mã nguồn Godot. Bạn có thể lấy tệp này trực tiếp từ tệp thực thi Godot bằng cách chạy lệnh sau:

.. code-block:: none

    godot --dump-gdextension-interface

Lệnh này tạo tệp header trong thư mục hiện tại, vì vậy bạn chỉ cần sao chép nó vào thư mục ``src`` trong dự án ví dụ.

Cuối cùng, chúng ta cần tham khảo thêm một nguồn thông tin khác: tệp JSON chứa thông tin tham chiếu về API Godot. Mã sẽ không trực tiếp sử dụng tệp này; chúng ta chỉ dùng nó để trích xuất thủ công một số thông tin.

Để lấy tệp JSON này, chỉ cần gọi tệp thực thi Godot:

.. code-block:: none

    godot --dump-extension-api

Tệp ``extension_api.json`` kết quả sẽ được tạo trong thư mục hiện tại. Bạn có thể sao chép tệp này vào thư mục ví dụ để tiện sử dụng.

.. note::
    Extension này nhắm đến Godot 4.2, nhưng cũng sẽ hoạt động trên các phiên bản mới hơn. Nếu muốn nhắm đến một phiên bản tối thiểu khác, hãy đảm bảo lấy header và tệp JSON từ phiên bản Godot mà bạn nhắm đến.

Buildsystem
-----------

Sử dụng buildsystem giúp chúng ta dễ dàng hơn rất nhiều khi làm việc với mã C. Để thuận tiện, chúng ta sẽ dùng SCons vì đây cũng là công cụ mà chính Godot sử dụng.

Tệp ``SConstruct`` sau đây là một tệp đơn giản, có nhiệm vụ build extension cho nền tảng hiện tại bạn đang sử dụng, có thể là Linux, macOS hoặc Windows. Đây sẽ là bản build chưa tối ưu nhằm phục vụ việc gỡ lỗi. Tệp này cũng giả định bản build 64-bit, điều này liên quan đến một số phần trong mã ví dụ. Việc tạo các kiểu build khác và biên dịch chéo nằm ngoài phạm vi của hướng dẫn này. Hãy lưu tệp này vào thư mục gốc.

.. code-block:: python

    #!/bin/env python
    from SCons.Script import Environment
    from os import path
    import sys

    env = Environment()

    # Set the target path and name.
    target_path = "project/bin/"
    target_name = "libgdexample"

    # Set the compiler and flags.
    env.Append(CPPPATH=["src"])  # Add the src folder to the include path.
    env.Append(CFLAGS=["-O0", "-g"])  # Make it a debug build.

    # Use Clang on macOS.
    if sys.platform == "darwin":
        env["CC"] = "clang"

    # Add all C files in "src" folder as sources.
    sources = env.Glob("src/*.c")

    # Create a shared library.
    library = env.SharedLibrary(
        target=path.join(target_path, target_name),
        source=sources,
    )

    # Set the library as the default target.
    env.Default(library)

Tệp này sẽ bao gồm tất cả các tệp C trong thư mục ``src``, vì vậy chúng ta không cần thay đổi tệp này khi thêm các tệp mã nguồn mới.

Khởi tạo extension
------------------

Phần mã đầu tiên chịu trách nhiệm khởi tạo extension. Đây là phần giúp Godot biết GDExtension của chúng ta cung cấp những gì, chẳng hạn như các lớp và plugin.

Tạo tệp ``init.h`` trong thư mục ``src``, với nội dung sau:

.. code-block:: c

    #pragma once

    #include "defs.h"

    #include "gdextension_interface.h"

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level);
    void deinitialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level);
    GDExtensionBool GDE_EXPORT gdexample_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization);

Các hàm được khai báo ở đây có chữ ký như API GDExtension yêu cầu.

Hãy chú ý đến việc đưa tệp ``defs.h`` vào. Đây là một trong các helper giúp đơn giản hóa việc viết mã extension. Hiện tại, tệp này chỉ chứa định nghĩa của ``GDE_EXPORT``, một macro giúp hàm trở thành hàm public trong shared library để Godot có thể gọi nó đúng cách. Macro này giúp trừu tượng hóa các yêu cầu khác nhau của từng trình biên dịch.

Tạo tệp ``defs.h`` trong thư mục ``src`` với nội dung sau:

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

Chúng ta cũng đưa vào một số header chuẩn để mọi việc dễ dàng hơn. Bây giờ chúng ta chỉ cần include ``defs.h``, và các header đó sẽ được đi kèm.

Bây giờ, hãy triển khai các hàm vừa khai báo. Tạo một tệp có tên ``init.c`` trong thư mục ``src`` và thêm đoạn mã sau:

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

Đoạn mã này thiết lập dữ liệu khởi tạo mà Godot yêu cầu. Các hàm khởi tạo và hủy khởi tạo được thiết lập để Godot gọi chúng khi cần. Đoạn mã cũng thiết lập mức khởi tạo, mức này khác nhau tùy extension. Vì dự định thêm một node tùy chỉnh nên mức ``SCENE`` là đủ.

Sau này chúng ta sẽ điền nội dung cho hàm ``initialize_gdexample_module()`` để đăng ký lớp tùy chỉnh.

Một lớp cơ bản
--------------

Để tạo một node thực sự, trước tiên chúng ta sẽ tạo một struct C để chứa dữ liệu và các hàm đóng vai trò là phương thức. Kế hoạch là biến nó thành một node tùy chỉnh kế thừa từ :ref:`Sprite2D <class_Sprite2D>`.

Tạo một tệp có tên ``gdexample.h`` trong thư mục ``src`` với nội dung sau:

.. code-block:: c

    #pragma once

    #include "gdextension_interface.h"

    #include "defs.h"

    // Struct to hold the node data.
    typedef struct
    {
        // Metadata.
        GDExtensionObjectPtr object; // Stores the underlying Godot object.
    } GDExample;

    // Constructor for the node.
    void gdexample_class_constructor(GDExample *self);

    // Destructor for the node.
    void gdexample_class_destructor(GDExample *self);

    // Bindings.
    void gdexample_class_bind_methods();

Điểm đáng chú ý ở đây là trường ``object``, chứa một con trỏ đến đối tượng Godot, và hàm ``gdexample_class_bind_methods()``, dùng để đăng ký metadata của lớp tùy chỉnh (thuộc tính, phương thức và tín hiệu). Hàm sau không hoàn toàn bắt buộc, vì chúng ta có thể thực hiện việc này khi đăng ký lớp, nhưng cách này giúp phân tách rõ hơn các mối quan tâm và cho phép lớp tự đăng ký metadata của mình.

Trường ``object`` là cần thiết vì lớp của chúng ta sẽ kế thừa một lớp Godot. Do không thể kế thừa trực tiếp, vì chúng ta không tương tác với mã nguồn (và C thậm chí không có lớp), thay vào đó chúng ta yêu cầu Godot tạo một đối tượng thuộc kiểu mà nó biết, rồi gắn extension của chúng ta vào đó. Chẳng hạn, chúng ta sẽ cần tham chiếu đến các đối tượng như vậy khi gọi phương thức trên lớp cha.

Hãy tạo phần mã nguồn tương ứng với header này. Tạo tệp ``gdexample.c`` trong thư mục ``src`` và thêm đoạn mã sau vào đó:

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


Vì hiện tại chúng ta chưa có việc gì cần làm với các hàm đó nên chúng sẽ tạm thời để trống.

Bước tiếp theo là đăng ký lớp của chúng ta. Tuy nhiên, để làm được điều đó, chúng ta cần tạo một :ref:`StringName <class_StringName>`, và để làm vậy, chúng ta phải lấy một hàm từ API GDExtension. Vì sẽ cần thực hiện việc này vài lần và cũng sẽ cần thêm những thứ khác, hãy tạo một wrapper API để hỗ trợ loại công việc này.

Wrapper API
-----------

Chúng ta sẽ bắt đầu bằng cách tạo tệp ``api.h`` trong thư mục ``src``:

.. code-block:: c

    #pragma once

    /*
    This file works as a collection of helpers to call the GDExtension API
    in a less verbose way, as well as a cache for methods from the discovery API,
    just so we don't have to keep loading the same methods again.
    */

    #include "gdextension_interface.h"

    #include "defs.h"

    extern GDExtensionClassLibraryPtr class_library;

    // API methods.

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

Tệp này sẽ bao gồm nhiều helper khác khi chúng ta bổ sung các chức năng hữu ích cho extension. Hiện tại, tệp chỉ có một con trỏ đến hàm tạo StringName từ chuỗi C (với mã hóa Latin-1) và một con trỏ khác đến hàm hủy StringName, vốn cần thiết để tránh rò rỉ bộ nhớ, cùng với hàm đăng ký lớp, mục tiêu ban đầu của chúng ta.

Chúng ta cũng lưu một tham chiếu đến ``class_library`` ở đây. Đây là thứ Godot cung cấp khi khởi tạo extension, và chúng ta sẽ cần dùng nó khi đăng ký những gì mình tạo ra để Godot biết extension nào đang thực hiện lời gọi.

Ngoài ra còn có một hàm để tải các con trỏ hàm đó từ API GDExtension.

Hãy viết phần mã nguồn tương ứng với header này. Tạo tệp ``api.c`` trong thư mục ``src``, rồi thêm đoạn mã sau:

.. code-block:: c

    #include "api.h"

    GDExtensionClassLibraryPtr class_library = NULL;

    struct Constructors constructors;
    struct Destructors destructors;
    struct API api;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // Get helper functions first.
        GDExtensionInterfaceVariantGetPtrDestructor variant_get_ptr_destructor = (GDExtensionInterfaceVariantGetPtrDestructor)p_get_proc_address("variant_get_ptr_destructor");

        // API.
        api.classdb_register_extension_class2 = (GDExtensionInterfaceClassdbRegisterExtensionClass2)p_get_proc_address("classdb_register_extension_class2");

        // Constructors.
        constructors.string_name_new_with_latin1_chars = (GDExtensionInterfaceStringNameNewWithLatin1Chars)p_get_proc_address("string_name_new_with_latin1_chars");

        // Destructors.
        destructors.string_name_destructor = variant_get_ptr_destructor(GDEXTENSION_VARIANT_TYPE_STRING_NAME);
    }

Điểm quan trọng đầu tiên ở đây là ``p_get_proc_address``. Đây là một hàm từ API GDExtension được truyền vào trong quá trình khởi tạo. Bạn có thể dùng hàm này để yêu cầu các hàm cụ thể từ API bằng tên của chúng. Ở đây, chúng ta lưu kết quả vào bộ nhớ đệm để không phải lưu tham chiếu đến ``p_get_proc_address`` ở khắp nơi mà có thể sử dụng wrapper của mình.

Trước hết, chúng ta yêu cầu hàm ``variant_get_ptr_destructor()``. Hàm này sẽ không được sử dụng bên ngoài hàm hiện tại, vì vậy chúng ta không thêm nó vào wrapper mà chỉ lưu vào bộ nhớ đệm cục bộ. Phép ép kiểu là cần thiết để loại bỏ các cảnh báo của trình biên dịch.

Sau đó, chúng ta lấy hàm tạo StringName từ chuỗi C, đúng như hàm cần thiết đã đề cập trước đó. Chúng ta lưu hàm này trong struct ``constructors``.

Tiếp theo, chúng ta sử dụng hàm ``variant_get_ptr_destructor()`` vừa lấy được để truy vấn hàm hủy dành cho StringName, sử dụng giá trị enum từ API ``gdextension_interface.h`` làm tham số. Chúng ta có thể lấy hàm hủy cho các kiểu khác theo cách tương tự, nhưng sẽ chỉ giới hạn ở những gì ví dụ cần.

Cuối cùng, chúng ta lấy hàm ``classdb_register_extension_class2()``, hàm cần thiết để đăng ký lớp tùy chỉnh.

.. note::
    Bạn có thể thắc mắc tại sao ``2`` lại xuất hiện trong tên hàm. Điều này có nghĩa đây là phiên bản thứ hai của hàm. Phiên bản cũ được giữ lại để đảm bảo khả năng tương thích ngược với các extension cũ, nhưng vì đã có phiên bản thứ hai, tốt nhất nên sử dụng phiên bản mới, do ví dụ này không định hỗ trợ các phiên bản Godot cũ hơn.

    Header ``gdextension_interface.h`` ghi lại phiên bản Godot mà mỗi hàm được giới thiệu.

Chúng ta cũng định nghĩa biến ``class_library`` ở đây; biến này sẽ được thiết lập trong quá trình khởi tạo.

Nói về việc khởi tạo, bây giờ chúng ta phải thay đổi tệp ``init.c`` để điền những phần vừa thêm:

.. code-block:: c

    GDExtensionBool GDE_EXPORT gdexample_library_init(GDExtensionInterfaceGetProcAddress p_get_proc_address, GDExtensionClassLibraryPtr p_library, GDExtensionInitialization *r_initialization)
    {
        class_library = p_library;
        load_api(p_get_proc_address);

        ...

Ở đây, chúng ta thiết lập ``class_library`` theo yêu cầu và gọi hàm ``load_api()`` mới của mình. Đừng quên include các header mới ở đầu tệp này:

.. code-block:: c

    #include "init.h"

    #include "api.h"
    #include "gdexample.h"
    ...

Nhân tiện, chúng ta có thể đăng ký lớp tùy chỉnh mới. Hãy điền nội dung cho hàm ``initialize_gdexample_module()``:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        if (p_level != GDEXTENSION_INITIALIZATION_SCENE)
        {
            return;
        }

        // Register class.
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

        // Bind methods.
        gdexample_class_bind_methods();

        // Destruct things.
        destructors.string_name_destructor(&class_name);
        destructors.string_name_destructor(&parent_class_name);
    }

Struct chứa thông tin về class là phần lớn nhất ở đây. Không trường nào của nó là bắt buộc, ngoại trừ ``create_instance_func`` và ``free_instance_func``. Chúng ta chưa tạo các hàm đó, vì vậy sẽ phải thực hiện chúng sớm. Lưu ý rằng chúng ta bỏ qua việc khởi tạo nếu không ở cấp độ ``SCENE``. Hàm này có thể được gọi nhiều lần, một lần cho mỗi cấp độ, nhưng chúng ta chỉ muốn đăng ký class một lần.

Thành phần chưa được định nghĩa còn lại ở đây là ``StringName``. Đây sẽ là một struct mờ dùng để chứa dữ liệu của Godot StringName trong extension của chúng ta. Chúng ta sẽ định nghĩa nó trong tệp có tên phù hợp là ``defs.h``:

.. code-block:: c

    ...
    // The sizes can be obtained from the extension_api.json file.
    #ifdef BUILD_32
    #define STRING_NAME_SIZE 4
    #else
    #define STRING_NAME_SIZE 8
    #endif

    // Types.

    typedef struct
    {
        uint8_t data[STRING_NAME_SIZE];
    } StringName;

Như đã đề cập trong chú thích, kích thước có thể được tìm thấy trong tệp ``extension_api.json`` mà chúng ta đã tạo trước đó, tại thuộc tính ``builtin_class_sizes``. ``BUILD_32`` không bao giờ được định nghĩa, vì ở đây chúng ta giả định đang làm việc với bản build 64-bit của Godot, nhưng nếu cần, bạn có thể thêm ``env.Append(CPPDEFINES=["BUILD_32"])`` vào tệp ``SConstruct``.

Chú thích ``// Types.`` báo trước rằng chúng ta sẽ thêm nhiều kiểu hơn vào tệp này. Hãy để việc đó lại sau.

Struct ``StringName`` ở đây chỉ dùng để chứa dữ liệu Godot, nên chúng ta không thực sự quan tâm bên trong nó có gì. Tuy nhiên, trong trường hợp này, nó chỉ là một con trỏ đến dữ liệu trên heap. Chúng ta sẽ dùng struct này khi cần tự cấp phát dữ liệu cho một StringName, như khi đăng ký class của mình.

Quay lại việc đăng ký, chúng ta cần thực hiện các hàm tạo và giải phóng. Hãy đưa chúng vào ``gdexample.h`` vì chúng dành riêng cho class tùy chỉnh:

.. code-block:: c

    ...
    // Bindings.
    void gdexample_class_bind_methods();
    GDExtensionObjectPtr gdexample_class_create_instance(void *p_class_userdata);
    void gdexample_class_free_instance(void *p_class_userdata, GDExtensionClassInstancePtr p_instance);
    ...

Trước khi có thể triển khai các hàm đó, chúng ta sẽ cần thêm một vài thành phần trong API. Chúng ta cần cách để cấp phát và giải phóng bộ nhớ. Mặc dù có thể dùng ``malloc()`` quen thuộc, chúng ta có thể thay vào đó sử dụng các hàm quản lý bộ nhớ của Godot. Chúng ta cũng cần cách tạo một đối tượng Godot và gán instance tùy chỉnh của mình cho nó.

Vậy hãy thay đổi ``api.h`` để đưa các hàm mới này vào:

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

Sau đó, chúng ta thay đổi hàm ``load_api()`` trong ``api.c`` để lấy các hàm mới này:

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

Bây giờ chúng ta có thể quay lại ``gdexample.c`` và định nghĩa các hàm mới, đồng thời nhớ include header ``api.h``:

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
        // Create native Godot object;
        StringName class_name;
        constructors.string_name_new_with_latin1_chars(&class_name, "Sprite2D", false);
        GDExtensionObjectPtr object = api.classdb_construct_object(&class_name);
        destructors.string_name_destructor(&class_name);

        // Create extension object.
        GDExample *self = (GDExample *)api.mem_alloc(sizeof(GDExample));
        gdexample_class_constructor(self);
        self->object = object;

        // Set the extension instance in the native Godot object.
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

Khi khởi tạo một đối tượng, trước tiên chúng ta tạo một đối tượng Sprite2D mới, vì đó là class cha của class chúng ta. Sau đó, chúng ta cấp phát bộ nhớ cho struct tùy chỉnh và gọi constructor của nó. Như đã đề cập trước đó, chúng ta cũng lưu con trỏ đến đối tượng Godot trong struct.

Sau đó, chúng ta đặt struct tùy chỉnh làm dữ liệu instance. Việc này cho Godot biết rằng đối tượng là một instance của class tùy chỉnh, từ đó gọi đúng các phương thức tùy chỉnh của chúng ta cho instance, đồng thời truyền lại dữ liệu này.

Lưu ý rằng chúng ta trả về đối tượng Godot đã tạo, không phải struct tùy chỉnh.

Đối với hàm ``gdextension_free_instance()``, chúng ta chỉ gọi destructor và giải phóng bộ nhớ đã cấp phát cho dữ liệu tùy chỉnh. Không cần hủy đối tượng Godot, vì chính engine sẽ xử lý việc đó.

Một project minh họa
--------------------

Bây giờ chúng ta đã có thể tạo và giải phóng đối tượng tùy chỉnh, chúng ta có thể thử nó trong một project thực tế. Để làm việc này, bạn cần mở Godot và tạo một project mới trong thư mục ``project``. Trình quản lý project có thể cảnh báo rằng thư mục không trống nếu bạn đã biên dịch extension trước đó; lần này bạn có thể an toàn bỏ qua cảnh báo này.

Nếu bạn chưa biên dịch extension, bây giờ là lúc thực hiện việc đó. Để làm vậy, hãy mở terminal hoặc command prompt, chuyển đến thư mục gốc của extension và chạy ``scons``. Extension rất đơn giản nên quá trình biên dịch sẽ hoàn tất nhanh chóng.

Sau đó, tạo một tệp có tên ``gdexample.gdextension`` bên trong thư mục ``project``. Đây là một tài nguyên Godot mô tả extension, cho phép engine tải extension đúng cách. Đặt nội dung sau vào tệp này:

.. code-block::

    [configuration]

    entry_symbol = "gdexample_library_init"
    compatibility_minimum = "4.2"

    [libraries]
    macos.debug = "res://bin/libgdexample.dylib"
    linux.debug = "res://bin/libgdexample.so"
    windows.debug = "res://bin/libgdexample.dll"

Như bạn có thể thấy, ``gdexample_library_init()`` chính là tên của hàm chúng ta đã định nghĩa trong tệp ``init.c``. Điều quan trọng là các tên phải khớp nhau, vì đó là cách Godot gọi entry point của extension.

Chúng ta cũng đặt phiên bản tương thích tối thiểu là 4.2, vì đang nhắm đến phiên bản này. Extension vẫn sẽ hoạt động trên các phiên bản mới hơn. Nếu bạn đang sử dụng phiên bản Godot mới hơn và phụ thuộc vào các tính năng mới, bạn cần tăng giá trị này lên số phiên bản có tất cả những gì bạn sử dụng. Xem :ref:`doc_what_is_gdextension_version_compatibility` để biết thêm thông tin.

Trong phần ``[libraries]``, chúng ta thiết lập các đường dẫn đến shared library trên những nền tảng khác nhau. Ở đây chỉ có các phiên bản debug vì đó là những gì chúng ta đang sử dụng trong ví dụ. Bằng cách dùng :ref:`feature tags <doc_feature_tags>`, bạn có thể tinh chỉnh để cung cấp cả các phiên bản release, thêm nhiều hệ điều hành đích hơn, cũng như cung cấp binary 32-bit và 64-bit.

Bạn cũng có thể thêm các dependency của library và icon tùy chỉnh cho các class trong tệp này, nhưng việc đó nằm ngoài phạm vi của tutorial này.

Sau khi lưu tệp, hãy quay lại editor. Godot sẽ tự động tải extension. Bạn sẽ không thấy gì vì extension của chúng ta chỉ đăng ký một class mới. Để sử dụng class này, hãy thêm một ``Node2D`` làm gốc của scene. Di chuyển nó vào giữa viewport để dễ nhìn hơn. Sau đó, thêm một node con mới vào node gốc và trong hộp thoại **Create New Node**, tìm kiếm "GDExample", tên của class chúng ta, class này sẽ được liệt kê ở đó. Nếu không thấy, nghĩa là Godot chưa tải extension đúng cách; hãy thử khởi động lại editor và thực hiện lại các bước để kiểm tra xem có bước nào bị bỏ sót không.

Class tùy chỉnh của chúng ta kế thừa từ ``Sprite2D``, nên nó có thuộc tính **Texture** trong Inspector. Đặt thuộc tính này thành tệp ``icon.svg`` mà Godot đã thuận tiện tạo cho chúng ta khi tạo project. Lưu scene này dưới tên ``main.tscn`` và chạy nó. Bạn có thể đặt scene này làm scene chính để thuận tiện hơn.

.. image:: img/gdextension_c_running.webp

Voilà! Chúng ta đã có một node tùy chỉnh đang chạy trong Godot. Tuy nhiên, nó chưa làm gì và không có gì khác so với một node ``Sprite2D`` thông thường. Tiếp theo, chúng ta sẽ khắc phục điều đó bằng cách thêm các phương thức và thuộc tính tùy chỉnh.

Các phương thức tùy chỉnh
-------------------------

Một việc thường làm trong extension là tạo các phương thức cho class tùy chỉnh và expose chúng cho Godot API. Chúng ta sẽ tạo một vài getter và setter cần thiết để binding các thuộc tính sau đó.

Trước tiên, hãy thêm các trường mới vào struct để chứa các giá trị ``amplitude`` và ``speed``, những giá trị sẽ được dùng sau này khi tạo behavior cho node. Thêm chúng vào tệp ``gdexample.h``, bằng cách thay đổi struct ``GDExample``:

.. code-block:: c

    ...

    typedef struct
    {
        // Public properties.
        double amplitude;
        double speed;
        // Metadata.
        GDExtensionObjectPtr object; // Stores the underlying Godot object.
    } GDExample;

    ...


Trong cùng tệp đó, thêm khai báo cho các getter và setter ngay sau destructor.

.. code-block:: c

    ...

    // Destructor for the node.
    void gdexample_class_destructor(GDExample *self);

    // Properties.
    void gdexample_class_set_amplitude(GDExample *self, double amplitude);
    double gdexample_class_get_amplitude(const GDExample *self);
    void gdexample_class_set_speed(GDExample *self, double speed);
    double gdexample_class_get_speed(const GDExample *self);

    ...

Trong tệp ``gdexample.c``, chúng ta sẽ khởi tạo các giá trị này trong constructor và thêm phần triển khai cho các hàm mới đó; chúng khá đơn giản:

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

Để các hàm đơn giản này hoạt động khi được Godot gọi, chúng ta sẽ cần một số wrapper giúp chuyển đổi dữ liệu đúng cách giữa chúng và engine.

Trước tiên, chúng ta sẽ tạo các wrapper cho ``ptrcall``. Đây là cách Godot sử dụng khi kiểu của các giá trị được biết chính xác, nhờ đó tránh phải dùng Variant. Chúng ta sẽ cần hai wrapper: một cho các hàm không nhận đối số và trả về ``double`` (dành cho getter), và một cho các hàm nhận một đối số ``double`` duy nhất và không trả về gì (dành cho setter).

Thêm các khai báo vào tệp ``api.h``:

.. code-block:: c

    void ptrcall_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);
    void ptrcall_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);


Hai hàm đó tuân theo kiểu ``GDExtensionClassMethodPtrCall``, như được định nghĩa trong ``gdextension_interface.h``. Ở đây chúng ta dùng ``float`` làm tên vì trong Godot, kiểu ``float`` có độ chính xác kép, nên chúng ta giữ theo quy ước này.

Sau đó, chúng ta triển khai các hàm đó trong tệp ``api.c``:

.. code-block:: c

    void ptrcall_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // Call the function.
        double (*function)(void *) = method_userdata;
        *((double *)r_ret) = function(p_instance);
    }

    void ptrcall_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // Call the function.
        void (*function)(void *, double) = method_userdata;
        function(p_instance, *((double *)p_args[0]));
    }

Đối số ``method_userdata`` là một giá trị tùy chỉnh mà chúng ta truyền cho Godot, trong trường hợp này sẽ được đặt làm con trỏ hàm cho hàm mà chúng ta muốn gọi. Vì vậy, trước tiên chúng ta chuyển nó thành kiểu hàm, sau đó chỉ cần gọi nó bằng cách truyền các đối số khi cần, hoặc thiết lập giá trị trả về.

Đối số ``p_instance`` chứa instance tùy chỉnh của class chúng ta, được truyền bằng ``object_set_instance()`` khi tạo đối tượng.

``p_args`` là một mảng các đối số. Lưu ý rằng mảng này chứa **con trỏ** đến các giá trị. Đó là lý do chúng ta dereference nó khi truyền vào các hàm. Số lượng đối số sẽ được khai báo khi binding hàm (việc chúng ta sẽ làm sớm) và luôn bao gồm các đối số mặc định nếu chúng tồn tại.

Cuối cùng, ``r_ret`` là một con trỏ đến biến nơi cần thiết lập giá trị trả về. Giống như các đối số, nó sẽ có đúng kiểu đã khai báo. Với hàm không trả về giá trị, chúng ta phải tránh thiết lập nó.

Hãy chú ý rằng kiểu và số lượng đối số là chính xác, vì vậy nếu cần các kiểu khác, chẳng hạn, chúng ta sẽ phải tạo thêm wrapper. Việc này có thể được tự động hóa bằng cách sử dụng một số code generation, nhưng nằm ngoài phạm vi của tutorial này.

Trong khi các hàm ``ptrcall`` được sử dụng khi các kiểu là chính xác, đôi khi Godot không thể biết có phải như vậy hay không (khi lời gọi đến từ một ngôn ngữ kiểu động như GDScript). Trong những tình huống đó, nó sử dụng các hàm ``call`` thông thường, vì vậy chúng ta cũng cần cung cấp chúng khi binding.

Hãy tạo hai wrapper mới trong tệp ``api.h``:

.. code-block:: c

    void call_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error);
    void call_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error);

Các hàm này tuân theo kiểu ``GDExtensionClassMethodCall``, vốn hơi khác một chút. Trước tiên, bạn nhận được các con trỏ tới Variant thay vì các kiểu chính xác. Ngoài ra còn có số lượng đối số và một struct lỗi mà bạn có thể thiết lập nếu xảy ra sự cố.

Để kiểm tra kiểu và trích xuất cũng như tương tác với Variant, chúng ta sẽ cần thêm một vài hàm từ API GDExtension. Vì vậy, hãy mở rộng các struct wrapper của chúng ta:

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

Tên của chúng đã nói lên chức năng. Chúng ta có một vài hàm khởi tạo để tạo và trích xuất một giá trị dấu phẩy động từ và vào một Variant. Chúng ta cũng có một vài hàm hỗ trợ để thực sự lấy các hàm khởi tạo đó, cùng với một hàm để xác định kiểu của một Variant.

Bây giờ hãy lấy chúng từ API, giống như trước đây, bằng cách thay đổi hàm ``load_api()`` trong tệp ``api.c``:

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

        // Constructors.
        ...
        constructors.variant_from_float_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_FLOAT);
        constructors.float_from_variant_constructor = api.get_variant_to_type_constructor(GDEXTENSION_VARIANT_TYPE_FLOAT);
        ...
    }

Sau khi thiết lập xong, chúng ta có thể triển khai các wrapper gọi hàm trong cùng tệp:

.. code-block:: c

    void call_0_args_ret_float(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error)
    {
        // Check argument count.
        if (p_argument_count != 0)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_TOO_MANY_ARGUMENTS;
            r_error->expected = 0;
            return;
        }

        // Call the function.
        double (*function)(void *) = method_userdata;
        double result = function(p_instance);
        // Set resulting Variant.
        constructors.variant_from_float_constructor(r_return, &result);
    }

    void call_1_float_arg_no_ret(void *method_userdata, GDExtensionClassInstancePtr p_instance, const GDExtensionConstVariantPtr *p_args, GDExtensionInt p_argument_count, GDExtensionVariantPtr r_return, GDExtensionCallError *r_error)
    {
        // Check argument count.
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

        // Check the argument type.
        GDExtensionVariantType type = api.variant_get_type(p_args[0]);
        if (type != GDEXTENSION_VARIANT_TYPE_FLOAT)
        {
            r_error->error = GDEXTENSION_CALL_ERROR_INVALID_ARGUMENT;
            r_error->expected = GDEXTENSION_VARIANT_TYPE_FLOAT;
            r_error->argument = 0;
            return;
        }

        // Extract the argument.
        double arg1;
        constructors.float_from_variant_constructor(&arg1, (GDExtensionVariantPtr)p_args[0]);

        // Call the function.
        void (*function)(void *, double) = method_userdata;
        function(p_instance, arg1);
    }

Các hàm này dài hơn một chút nhưng khá dễ theo dõi. Trước tiên, chúng kiểm tra xem số lượng đối số có đúng như mong đợi hay không; nếu không, chúng thiết lập struct lỗi rồi trả về. Đối với hàm có một tham số, nó cũng kiểm tra xem kiểu của đối số có chính xác hay không. Điều này rất quan trọng vì kiểu không khớp khi trích xuất từ Variant có thể gây ra lỗi crash.

Sau đó, hàm tiếp tục trích xuất đối số bằng hàm khởi tạo mà chúng ta đã thiết lập trước đó. Hàm không có đối số thì thiết lập giá trị trả về sau khi gọi hàm. Hãy lưu ý rằng chúng sử dụng một con trỏ tới biến kiểu ``double``, vì đây là điều mà các hàm khởi tạo đó yêu cầu.

Trước khi thực sự liên kết các phương thức, chúng ta cần một cách để tạo các instance ``GDExtensionPropertyInfo``. Mặc dù có thể thực hiện việc này bên trong các hàm liên kết mà chúng ta sẽ triển khai sau, sẽ dễ dàng hơn nếu có một hàm hỗ trợ vì chúng ta sẽ cần dùng nó nhiều lần, bao gồm cả khi liên kết các thuộc tính.

Hãy tạo hai hàm này trong tệp ``api.h``:

.. code-block:: c

    // Create a PropertyInfo struct.
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

Hàm đầu tiên là phiên bản đơn giản hóa của hàm thứ hai, vì thông thường chúng ta không cần tất cả đối số cho thuộc tính và có thể dùng các giá trị mặc định. Sau đó, chúng ta cũng có một hàm để hủy PropertyInfo, vì cần tạo các String và StringName phải được giải phóng đúng cách.

Nhân tiện, chúng ta cũng cần một cách để tạo và hủy String, vì vậy sẽ bổ sung vào các struct hiện có trong cùng tệp này. Chúng ta cũng sẽ lấy một hàm API mới để thực sự liên kết phương thức tùy chỉnh của mình.

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

Trước khi triển khai các hàm đó, hãy tạm dừng nhanh ở tệp ``defs.h`` và thêm kích thước của kiểu ``String`` cùng với một vài enum:

.. code-block:: c

    // The sizes can be obtained from the extension_api.json file.
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

    // Enums.

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

Mặc dù có cùng kích thước với ``StringName``, việc sử dụng một tên khác sẽ rõ ràng hơn.

Các enum ở đây chỉ là những hàm hỗ trợ giúp đặt tên cho các số mà chúng biểu diễn. Thông tin về chúng có trong tệp ``extension_api.json``. Ở đây, chúng ta chỉ thiết lập những enum cần dùng cho tutorial để nội dung ngắn gọn hơn.

Bây giờ chuyển sang ``api.c``, chúng ta cần tải các con trỏ tới những hàm mới đã thêm vào API.

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        ...
        // API
        ...
        api.classdb_register_extension_class_method = (GDExtensionInterfaceClassdbRegisterExtensionClassMethod)p_get_proc_address("classdb_register_extension_class_method");

        // Constructors.
        ...
        constructors.string_new_with_utf8_chars = (GDExtensionInterfaceStringNewWithUtf8Chars)p_get_proc_address("string_new_with_utf8_chars");

        // Destructors.
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


Phiên bản đơn giản của ``make_property()`` chỉ gọi phiên bản đầy đủ hơn với một số đối số mặc định. Ý nghĩa chính xác của các giá trị đó nằm ngoài phạm vi của tutorial này; hãy xem trang về :ref:`Object class <doc_object_class>` để biết thêm chi tiết về việc liên kết các phương thức và thuộc tính.

Phiên bản đầy đủ phức tạp hơn. Trước tiên, nó tạo các ``String`` và ``StringName`` cho những trường cần thiết bằng cách cấp phát bộ nhớ và gọi các hàm khởi tạo tương ứng. Sau đó, nó tạo một struct ``GDExtensionPropertyInfo`` và thiết lập tất cả các trường bằng những đối số được cung cấp. Cuối cùng, nó trả về struct vừa tạo.

Hàm ``destruct_property()`` khá đơn giản; nó chỉ gọi các hàm hủy cho những đối tượng đã tạo và giải phóng phần bộ nhớ được cấp phát cho chúng.

Hãy quay lại tệp header ``api.h`` để tạo các hàm thực sự liên kết những phương thức:

.. code-block:: c

    // Version for 0 arguments, with return.
    void bind_method_0_r(
        const char *class_name,
        const char *method_name,
        void *function,
        GDExtensionVariantType return_type);

    // Version for 1 argument, no return.
    void bind_method_1(
        const char *class_name,
        const char *method_name,
        void *function,
        const char *arg1_name,
        GDExtensionVariantType arg1_type);

Sau đó chuyển lại sang tệp ``api.c`` để triển khai chúng:

.. code-block:: c

    // Version for 0 arguments, with return.
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

        // Destruct things.
        destructors.string_name_destructor(&method_name_string);
        destructors.string_name_destructor(&class_name_string);
        destruct_property(&return_info);
    }

    // Version for 1 argument, no return.
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

        // Destruct things.
        destructors.string_name_destructor(&method_name_string);
        destructors.string_name_destructor(&class_name_string);
        destruct_property(&args_info[0]);
    }

Hai hàm này rất giống nhau. Trước tiên, chúng tạo một ``StringName`` chứa tên phương thức. Đối tượng này được tạo trên stack vì chúng ta không cần giữ nó sau khi hàm kết thúc. Sau đó, chúng tạo các biến cục bộ để chứa ``call_func`` và ``ptrcall_func``, trỏ tới các hàm hỗ trợ mà chúng ta đã định nghĩa trước đó.

Ở bước tiếp theo, chúng có phần khác nhau. Hàm đầu tiên tạo một thuộc tính cho giá trị trả về, với tên rỗng vì không cần tên. Hàm còn lại tạo một mảng các thuộc tính cho các đối số; trong trường hợp này, mảng có một phần tử. Hàm này cũng có một mảng metadata, có thể được sử dụng nếu đối số có đặc điểm đặc biệt nào đó (ví dụ: nếu một giá trị ``int`` dài 32 bit thay vì 64 bit mặc định).

Sau đó, chúng tạo ``GDExtensionClassMethodInfo`` với các trường bắt buộc cho từng trường hợp. Tiếp theo, chúng tạo một ``StringName`` cho tên lớp để liên kết phương thức với lớp. Sau đó, chúng gọi hàm API để thực sự liên kết phương thức này với lớp. Cuối cùng, chúng hủy các đối tượng đã tạo vì không còn cần đến chúng nữa.

.. note::
    Các hàm hỗ trợ liên kết ở đây sử dụng những hàm hỗ trợ gọi mà chúng ta đã tạo trước đó, vì vậy hãy lưu ý rằng các hàm hỗ trợ gọi này chỉ chấp nhận kiểu Godot ``FLOAT`` (tương đương với ``double`` trong C). Nếu định sử dụng chúng cho các kiểu khác, bạn cần kiểm tra kiểu của các đối số và kiểu trả về, rồi chọn một callback hàm phù hợp. Ở đây, điều này được lược bỏ chỉ để ví dụ không trở nên dài hơn nữa.

Bây giờ chúng ta đã có phương tiện để liên kết các phương thức, nên có thể thực hiện việc đó trong lớp tùy chỉnh. Hãy mở tệp ``gdexample.c`` và điền vào hàm ``gdexample_class_bind_methods()``:

.. code-block:: c

    void gdexample_class_bind_methods()
    {
        bind_method_0_r("GDExample", "get_amplitude", gdexample_class_get_amplitude, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_amplitude", gdexample_class_set_amplitude, "amplitude", GDEXTENSION_VARIANT_TYPE_FLOAT);

        bind_method_0_r("GDExample", "get_speed", gdexample_class_get_speed, GDEXTENSION_VARIANT_TYPE_FLOAT);
        bind_method_1("GDExample", "set_speed", gdexample_class_set_speed, "speed", GDEXTENSION_VARIANT_TYPE_FLOAT);
    }

Vì hàm này đã được gọi trong quá trình khởi tạo, chúng ta có thể dừng ở đây. Hàm này đơn giản hơn nhiều sau khi đã tạo toàn bộ cơ sở hạ tầng để việc này hoạt động. Bạn có thể thấy rằng việc triển khai các hàm liên kết trực tiếp ở đây sẽ chiếm khá nhiều chỗ và cũng lặp lại đáng kể. Cách này cũng giúp việc thêm một phương thức khác trong tương lai dễ dàng hơn.

Nếu biên dịch mã và mở lại dự án Godot, ban đầu sẽ không có gì khác biệt vì chúng ta chỉ thêm hai phương thức mới. Để đảm bảo chúng được đăng ký đúng cách, bạn có thể tìm ``GDExample`` trong phần trợ giúp của trình soạn thảo và xác minh rằng chúng có mặt trên trang tài liệu.

.. image:: img/gdextension_c_methods_doc.webp


Thuộc tính tùy chỉnh
--------------------

Vì hiện chúng ta đã liên kết getter và setter cho các thuộc tính, nên có thể tiếp tục tạo các thuộc tính thực tế sẽ được hiển thị trong inspector của trình soạn thảo Godot.

Với phần thiết lập đầy đủ ở mục trước, chỉ còn vài việc cần làm để có thể liên kết các thuộc tính. Trước tiên, hãy lấy một hàm API mới trong tệp ``api.h``:


.. code-block:: c

    extern struct API {
        ...
        GDExtensionInterfaceClassdbRegisterExtensionClassProperty classdb_register_extension_class_property;
    } api;

Chúng ta cũng hãy khai báo một hàm để liên kết các thuộc tính:

.. code-block:: c

    void bind_property(
        const char *class_name,
        const char *name,
        GDExtensionVariantType type,
        const char *getter,
        const char *setter);

Trong tệp ``api.c``, chúng ta có thể tải hàm API mới:

.. code-block:: c

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // API
        ...
        api.classdb_register_extension_class_property = (GDExtensionInterfaceClassdbRegisterExtensionClassProperty)p_get_proc_address("classdb_register_extension_class_property");

        ...
    }

Sau đó, chúng ta có thể triển khai hàm hỗ trợ mới trong cùng tệp này:

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

        // Destruct things.
        destructors.string_name_destructor(&class_string_name);
        destruct_property(&info);
        destructors.string_name_destructor(&getter_name);
        destructors.string_name_destructor(&setter_name);
    }

Hàm này tương tự hàm liên kết phương thức. Điểm khác biệt chính là chúng ta không cần thêm một struct vì có thể sử dụng trực tiếp ``GDExtensionPropertyInfo`` được tạo bởi hàm hỗ trợ; do đó, hàm này đơn giản hơn. Nó chỉ tạo các giá trị ``StringName`` từ các chuỗi C, tạo một struct thông tin thuộc tính bằng hàm hỗ trợ của chúng ta, gọi hàm API để đăng ký thuộc tính trong lớp, rồi hủy tất cả các đối tượng đã tạo.

Sau khi hoàn tất, chúng ta có thể mở rộng hàm ``gdexample_class_bind_methods()`` trong tệp ``gdexample.c``:

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

Nếu build extension bằng ``scons``, bạn sẽ thấy thuộc tính mới trong trình soạn thảo Godot, không chỉ trên trang tài liệu của lớp tùy chỉnh mà còn trong dock Inspector khi node ``GDExample`` được chọn.

.. image:: img/gdextension_c_inspector_properties.webp

Liên kết các phương thức ảo
---------------------------

Node tùy chỉnh của chúng ta hiện đã có các thuộc tính để điều chỉnh cách nó hoạt động, nhưng vẫn chưa làm gì cả. Trong phần này, chúng ta sẽ liên kết phương thức ảo
:ref:`_process() <class_Node_private_method__process>` and make our custom sprite
di chuyển một chút.

Trong tệp ``gdexample.h``, hãy thêm một hàm đại diện cho phương thức ``_process()`` tùy chỉnh:

.. code-block:: c

    // Methods.
    void gdexample_class_process(GDExample *self, double delta);

Chúng ta cũng sẽ thêm một trường “private” để theo dõi thời gian đã trôi qua trong struct tùy chỉnh. Trường này chỉ là “private” theo nghĩa nó sẽ không được liên kết với API Godot, dù nó là public ở phía C vì ngôn ngữ này không có các bộ định danh truy cập.

.. code-block:: c

    typedef struct
    {
        // Private properties.
        double time_passed;
        ...
    } GDExample;

Trong tệp mã nguồn đối ứng ``gdexample.c``, chúng ta cần khởi tạo trường mới trong hàm khởi tạo:

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

Hiện tại, nó chỉ cập nhật trường private mà chúng ta đã tạo và không làm gì khác. Chúng ta sẽ quay lại phần này sau khi phương thức được liên kết đúng cách.

Các phương thức ảo hơi khác so với các liên kết thông thường. Thay vì đăng ký trực tiếp phương thức, chúng ta sẽ đăng ký một hàm đặc biệt mà Godot sẽ gọi để hỏi liệu một phương thức ảo cụ thể có được triển khai trong extension của chúng ta hay không. Engine sẽ truyền một ``StringName`` làm đối số, vì vậy, theo tinh thần của tutorial này, chúng ta sẽ tạo một hàm hỗ trợ để kiểm tra xem nó có bằng một chuỗi C hay không.

Hãy thêm khai báo vào tệp ``api.h``:

.. code-block:: c

    // Compare a StringName with a C string.
    bool is_string_name_equal(GDExtensionConstStringNamePtr p_a, const char *p_b);

Chúng ta cũng sẽ thêm một struct mới vào tệp này để chứa các con trỏ hàm cho các toán tử tùy chỉnh:

.. code-block:: c

    extern struct Operators
    {
        GDExtensionPtrOperatorEvaluator string_name_equal;
    } operators;

Sau đó, trong tệp ``api.c``, chúng ta sẽ tải con trỏ hàm từ API:

.. code-block:: c

    struct Operators operators;

    void load_api(GDExtensionInterfaceGetProcAddress p_get_proc_address)
    {
        // Get helper functions first.
        ...
        GDExtensionInterfaceVariantGetPtrOperatorEvaluator variant_get_ptr_operator_evaluator = (GDExtensionInterfaceVariantGetPtrOperatorEvaluator)p_get_proc_address("variant_get_ptr_operator_evaluator");

        ...

        // Operators.
        operators.string_name_equal = variant_get_ptr_operator_evaluator(GDEXTENSION_VARIANT_OP_EQUAL, GDEXTENSION_VARIANT_TYPE_STRING_NAME, GDEXTENSION_VARIANT_TYPE_STRING_NAME);
    }

Như bạn có thể thấy, ở đây chúng ta cần một helper cục bộ mới để lấy con trỏ hàm cho toán tử.

Với phần này, chúng ta có thể dễ dàng tạo hàm so sánh trong cùng tệp:

.. code-block:: c

    bool is_string_name_equal(GDExtensionConstStringNamePtr p_a, const char *p_b)
    {
        // Create a StringName for the C string.
        StringName string_name;
        constructors.string_name_new_with_latin1_chars(&string_name, p_b, false);

        // Compare both StringNames.
        bool is_equal = false;
        operators.string_name_equal(p_a, &string_name, &is_equal);

        // Destroy the created StringName.
        destructors.string_name_destructor(&string_name);

        // Return the result.
        return is_equal;
    }

Hàm này tạo một ``StringName`` từ đối số, so sánh với đối số còn lại bằng con trỏ hàm toán tử, rồi trả về kết quả. Lưu ý rằng giá trị trả về của toán tử được truyền dưới dạng tham chiếu out; đây là cách thường được dùng trong API.

Hãy quay lại tệp ``gdexample.h`` và thêm một vài hàm sẽ được dùng làm callback cho Godot API:

.. code-block:: c

    void *gdexample_class_get_virtual_with_data(void *p_class_userdata, GDExtensionConstStringNamePtr p_name);
    void gdexample_class_call_virtual_with_data(GDExtensionClassInstancePtr p_instance, GDExtensionConstStringNamePtr p_name, void *p_virtual_call_userdata, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret);

Thực tế có hai cách đăng ký các phương thức ảo. Chỉ một cách có phần ``get``, trong đó bạn cung cấp cho Godot một con trỏ hàm được tạo đúng cách để Godot gọi. Với cách này, chúng ta sẽ phải tạo một helper khác cho mỗi phương thức ảo, điều này không thật sự tiện lợi. Thay vào đó, chúng ta dùng cách thứ hai, cho phép trả về bất kỳ dữ liệu nào, sau đó Godot sẽ gọi một callback thứ hai và trả lại dữ liệu này cùng với thông tin về lời gọi. Chúng ta có thể đơn giản truyền con trỏ hàm của mình dưới dạng dữ liệu tùy chỉnh, rồi dùng một callback duy nhất cho tất cả các phương thức ảo. Mặc dù trong ví dụ này chúng ta chỉ dùng nó cho một phương thức, cách này sẽ dễ mở rộng hơn.

Vậy hãy triển khai hai hàm đó trong tệp ``gdexample.c``:

.. code-block:: c

    void *gdexample_class_get_virtual_with_data(void *p_class_userdata, GDExtensionConstStringNamePtr p_name)
    {
        // If it is the "_process" method, return a pointer to the gdexample_class_process function.
        if (is_string_name_equal(p_name, "_process"))
        {
            return (void *)gdexample_class_process;
        }
        // Otherwise, return NULL.
        return NULL;
    }

    void gdexample_class_call_virtual_with_data(GDExtensionClassInstancePtr p_instance, GDExtensionConstStringNamePtr p_name, void *p_virtual_call_userdata, const GDExtensionConstTypePtr *p_args, GDExtensionTypePtr r_ret)
    {
        // If it is the "_process" method, call it with a helper.
        if (p_virtual_call_userdata == &gdexample_class_process)
        {
            ptrcall_1_float_arg_no_ret(p_virtual_call_userdata, p_instance, p_args, r_ret);
        }
    }

Sau khi đã tạo tất cả các helper trước đó, những hàm này cũng khá đơn giản.

Với hàm đầu tiên, chúng ta chỉ cần kiểm tra xem tên hàm được yêu cầu có phải là ``_process`` hay không; nếu đúng, chúng ta trả về một con trỏ hàm trỏ đến phần triển khai của nó. Nếu không, chúng ta trả về ``NULL``, báo hiệu rằng phương thức này không được ghi đè. Ở đây chúng ta không dùng ``p_class_userdata`` vì hàm này chỉ dành cho một lớp và không có dữ liệu nào liên kết với nó.

Hàm thứ hai cũng tương tự. Nếu đó là phương thức ``_process()``, nó sử dụng con trỏ hàm được cung cấp để gọi helper ``ptrcall``, đồng thời chuyển tiếp các đối số của lời gọi. Nếu không, nó không làm gì cả, vì chúng ta không triển khai bất kỳ phương thức ảo nào khác.

Điều duy nhất còn thiếu là sử dụng các callback này khi đăng ký lớp. Hãy mở tệp ``init.c`` và thay đổi phần khởi tạo ``class_info`` để thêm chúng vào, thay thế giá trị ``NULL`` đã dùng trước đó:

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

Như vậy là đủ để liên kết phương thức ảo. Nếu bạn build extension rồi chạy lại dự án Godot, hàm ``_process()`` sẽ được gọi. Tuy nhiên, bạn sẽ không thể nhận ra điều đó vì bản thân hàm không thực hiện gì có thể quan sát được. Bây giờ chúng ta sẽ khắc phục điều này bằng cách khiến node tùy chỉnh di chuyển theo một mẫu.

Để node của chúng ta thực hiện được điều gì đó, chúng ta cần gọi các phương thức của Godot. Không chỉ các hàm của GDExtension API như những gì chúng ta đã làm từ đầu đến giờ, mà còn cả các phương thức thực tế của engine, giống như khi viết script. Điều này đương nhiên đòi hỏi thêm một số bước thiết lập.

Đầu tiên, hãy thêm :ref:`class_Vector2` vào tệp ``defs.h``, để chúng ta có thể sử dụng nó trong phương thức của mình:

.. code-block:: c

    // The sizes can be obtained from the extension_api.json file.
    ...
    #ifdef REAL_T_IS_DOUBLE
    #define VECTOR2_SIZE 16
    #else
    #define VECTOR2_SIZE 8
    #endif

    ...

    // Types.

    ...

    typedef struct
    {
        uint8_t data[VECTOR2_SIZE];
    } Vector2;

Định nghĩa ``REAL_T_IS_DOUBLE`` chỉ cần thiết nếu phiên bản Godot của bạn được build với hỗ trợ độ chính xác kép, vốn không phải thiết lập mặc định.

Bây giờ, trong tệp ``api.h``, chúng ta sẽ thêm một vài thành phần vào các struct API, bao gồm một struct mới để chứa các phương thức engine cần gọi.

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

Sau đó, trong tệp ``api.c``, chúng ta có thể lấy các con trỏ hàm từ Godot:

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

Phần đáng chú ý duy nhất ở đây là constructor ``Vector2``, nơi chúng ta yêu cầu chỉ mục ``3``. Vì có nhiều constructor với các kiểu đối số khác nhau, chúng ta cần chỉ định constructor mình muốn. Trong trường hợp này, chúng ta lấy constructor nhận hai số thực làm tọa độ ``x`` và ``y``, do đó có tên như vậy. Chỉ mục này có thể được lấy từ tệp ``extension_api.json``. Lưu ý rằng chúng ta cũng cần một helper cục bộ mới để lấy nó.

Lưu ý rằng ở đây chúng ta không lấy gì cho struct methods. Đó là vì hàm này được gọi quá sớm trong quá trình khởi tạo, nên các lớp vẫn chưa được đăng ký đúng cách.

Thay vào đó, chúng ta sẽ dùng callback cấp độ khởi tạo để lấy chúng khi đăng ký lớp tùy chỉnh. Hãy thêm phần này vào tệp ``init.c``:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        if (p_level != GDEXTENSION_INITIALIZATION_SCENE)
        {
            return;
        }

        // Get ClassDB methods here because the classes we need are all properly registered now.
        // See extension_api.json for hashes.
        StringName native_class_name;
        StringName method_name;

        constructors.string_name_new_with_latin1_chars(&native_class_name, "Node2D", false);
        constructors.string_name_new_with_latin1_chars(&method_name, "set_position", false);
        methods.node2d_set_position = api.classdb_get_method_bind(&native_class_name, &method_name, 743155724);
        destructors.string_name_destructor(&native_class_name);
        destructors.string_name_destructor(&method_name);

        ...
    }

Ở đây, chúng ta tạo ``StringName`` cho lớp và phương thức mà mình muốn lấy, sau đó dùng GDExtension API để lấy ``MethodBind`` của chúng, tức là một đối tượng đại diện cho phương thức đã liên kết. Chúng ta lấy phương thức ``set_position`` từ ``Node2D`` vì đây là nơi phương thức được đăng ký, dù chúng ta sẽ sử dụng nó trong một ``Sprite2D``, tức là một lớp dẫn xuất.

Con số có vẻ ngẫu nhiên dùng để lấy bind thực ra là một hash của chữ ký phương thức. Điều này cho phép Godot khớp với phương thức bạn yêu cầu ngay cả khi chữ ký đó thay đổi trong một phiên bản Godot tương lai, bằng cách cung cấp một phương thức tương thích khớp với yêu cầu của bạn. Đây là một trong những hệ thống cho phép engine tải các extension được tạo cho những phiên bản trước. Bạn có thể lấy giá trị của hash này từ tệp ``extension_api.json``.

Với tất cả những phần đó, cuối cùng chúng ta có thể triển khai phương thức ``_process()`` tùy chỉnh trong tệp ``gdexample.c``:

.. code-block:: c

    ...

    #include <math.h>

    ...

    void gdexample_class_process(GDExample *self, double delta)
    {
        self->time_passed += self->speed * delta;

        Vector2 new_position;

        // Set up the arguments for the Vector2 constructor.
        double x = self->amplitude + (self->amplitude * sin(self->time_passed * 2.0));
        double y = self->amplitude + (self->amplitude * cos(self->time_passed * 1.5));
        GDExtensionConstTypePtr args[] = {&x, &y};
        // Call the Vector2 constructor.
        constructors.vector2_constructor_x_y(&new_position, args);

        // Set up the arguments for the set_position method.
        GDExtensionConstTypePtr args2[] = {&new_position};
        // Call the set_position method.
        api.object_method_bind_ptrcall(methods.node2d_set_position, self->object, args2, NULL);
    }

Sau khi cập nhật thời gian đã trôi qua, được nhân theo thuộc tính ``speed``, hàm tạo các giá trị ``x`` và ``y`` dựa trên thời gian đó, đồng thời cũng điều biến chúng theo thuộc tính ``amplitude``. Đây là yếu tố tạo ra hiệu ứng theo mẫu. Header ``math.h`` cần thiết cho các hàm ``sin()`` và ``cos()`` được sử dụng ở đây.

Sau đó, hàm thiết lập một mảng các đối số để tạo một ``Vector2``, rồi gọi constructor. Hàm thiết lập một mảng đối số khác và dùng nó để gọi phương thức ``set_position()`` thông qua bind mà chúng ta đã lấy trước đó.

Vì không có phần nào ở đây cấp phát bộ nhớ, chúng ta không cần dọn dẹp.

Bây giờ chúng ta có thể build lại extension và mở lại Godot. Ngay cả trong editor, bạn cũng sẽ thấy sprite tùy chỉnh đang di chuyển.

.. image:: img/gdextension_c_moving_sprite.gif

Hãy thử thay đổi các thuộc tính **Speed** và **Amplitude** rồi xem sprite phản ứng như thế nào.

Đăng ký và phát signal
----------------------

Để hoàn thành tutorial này, hãy cùng xem cách đăng ký một signal tùy chỉnh và phát nó vào thời điểm thích hợp. Như bạn có thể đoán, chúng ta sẽ cần thêm một vài con trỏ hàm từ API và nhiều hàm helper hơn.

Trong tệp ``api.h``, chúng ta thêm hai thành phần. Một là hàm API để đăng ký signal, thành phần còn lại là một hàm helper để bọc việc liên kết signal.

.. code-block:: c

    extern struct API
    {
        ...
        GDExtensionInterfaceClassdbRegisterExtensionClassSignal classdb_register_extension_class_signal;
    } api;

    ...

    // Version for 1 argument.
    void bind_signal_1(
        const char *class_name,
        const char *signal_name,
        const char *arg1_name,
        GDExtensionVariantType arg1_type);

Trong trường hợp này, chúng ta chỉ có phiên bản dành cho một đối số, vì đó là phiên bản chúng ta sẽ sử dụng.

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

        // Destruct things.
        destructors.string_name_destructor(&class_string_name);
        destructors.string_name_destructor(&signal_string_name);
        destruct_property(&args_info[0]);
    }

Hàm này rất giống với hàm liên kết các phương thức. Điểm khác biệt chính là chúng ta không cần điền thêm một struct khác, mà chỉ truyền các tên cần thiết cùng mảng đối số. ``1`` ở cuối biểu thị số lượng đối số mà signal cung cấp.

Với phần này, chúng ta có thể liên kết signal trong ``gdexample.c``:

.. code-block:: c

    void gdexample_class_bind_methods()
    {
        ...
        bind_signal_1("GDExample", "position_changed", "new_position", GDEXTENSION_VARIANT_TYPE_VECTOR2);
    }

Để phát một signal, chúng ta cần gọi
:ref:`emit_signal() <class_Object_method_emit_signal>` method on our custom node.
Vì đây là một hàm ``vararg`` (nghĩa là nhận số lượng đối số bất kỳ), chúng ta không thể sử dụng ``ptrcall``. Để thực hiện một lời gọi thông thường, chúng ta phải tạo các Variant, việc này cần thêm vài bước kết nối.

Đầu tiên, trong tệp ``defs.h``, chúng ta tạo định nghĩa cho Variant:

.. code-block:: c

    ...

    // The sizes can be obtained from the extension_api.json file.
    ...
    #ifdef REAL_T_IS_DOUBLE
    #define VARIANT_SIZE 40
    #define VECTOR2_SIZE 16
    #else
    #define VARIANT_SIZE 24
    #define VECTOR2_SIZE 8
    #endif

    ...

    // Types.

    ...

    typedef struct
    {
        uint8_t data[VARIANT_SIZE];
    } Variant;


Trước hết, chúng ta đặt kích thước của Variant cùng với kích thước của Vector2 đã thêm trước đó. Sau đó, chúng ta dùng nó để tạo một struct opaque đủ sức chứa dữ liệu Variant. Một lần nữa, chúng ta đặt kích thước cho các bản build với độ chính xác kép làm phương án dự phòng, vì các bản build Godot chính thức thường sử dụng độ chính xác đơn.

Hàm ``emit_signal()`` sẽ được gọi với hai đối số. Đối số đầu tiên là tên của signal cần phát, còn đối số thứ hai là đối số chúng ta truyền đến các kết nối của signal, tức là một Vector2 như đã khai báo khi liên kết signal. Vì vậy, chúng ta sẽ tạo một hàm helper có thể gọi một MethodBind với các kiểu này. Dù hàm đó có trả về một giá trị (mã lỗi), chúng ta không cần xử lý nó, nên hiện tại chỉ cần bỏ qua.

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

    // Helper to call with Variant arguments.
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

        // Constructors.
        ...
        constructors.variant_from_string_name_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_STRING_NAME);
        constructors.variant_from_vector2_constructor = api.get_variant_from_type_constructor(GDEXTENSION_VARIANT_TYPE_VECTOR2);

        // Destructors.
        ...
        destructors.variant_destroy = (GDExtensionInterfaceVariantDestroy)p_get_proc_address("variant_destroy");

        ...
    }

    ...

    void call_2_args_stringname_vector2_no_ret_variant(GDExtensionMethodBindPtr p_method_bind, GDExtensionObjectPtr p_instance, const GDExtensionTypePtr p_arg1, const GDExtensionTypePtr p_arg2)
    {
        // Set up the arguments for the call.
        Variant arg1;
        constructors.variant_from_string_name_constructor(&arg1, p_arg1);
        Variant arg2;
        constructors.variant_from_vector2_constructor(&arg2, p_arg2);
        GDExtensionConstVariantPtr args[] = {&arg1, &arg2};

        // Add dummy return value storage.
        Variant ret;

        // Call the function.
        api.object_method_bind_call(p_method_bind, p_instance, args, 2, &ret, NULL);

        // Destroy the arguments.
        destructors.variant_destroy(&arg1);
        destructors.variant_destroy(&arg2);
        destructors.variant_destroy(&ret);
    }

Hàm helper này có một số đoạn mã khuôn mẫu nhưng khá đơn giản. Hàm thiết lập hai đối số bên trong các Variant được cấp phát trên stack, sau đó tạo một mảng chứa con trỏ đến chúng. Hàm cũng thiết lập một Variant khác để chứa giá trị trả về; chúng ta không cần khởi tạo Variant này vì lời gọi yêu cầu nó ở trạng thái chưa khởi tạo.

Sau đó, hàm thực sự gọi MethodBind bằng instance và các đối số mà chúng ta cung cấp. ``NULL`` ở cuối sẽ là một con trỏ đến struct ``GDExtensionCallError``. Nó có thể được dùng để xử lý các lỗi tiềm ẩn khi gọi hàm (chẳng hạn như đối số không đúng). Để đơn giản, chúng ta sẽ không xử lý phần đó ở đây.

Cuối cùng, chúng ta cần hủy các Variant đã tạo. Về mặt kỹ thuật, Variant chứa Vector2 không cần hủy, nhưng dọn dẹp mọi thứ sẽ rõ ràng hơn.

Chúng ta cũng cần tải MethodBind, việc này sẽ được thực hiện trong tệp ``init.c``, ngay sau khi tải MethodBind cho phương thức ``set_position`` mà chúng ta đã làm trước đó:

.. code-block:: c

    void initialize_gdexample_module(void *p_userdata, GDExtensionInitializationLevel p_level)
    {
        ...

        constructors.string_name_new_with_latin1_chars(&native_class_name, "Object", false);
        constructors.string_name_new_with_latin1_chars(&method_name, "emit_signal", false);
        methods.object_emit_signal = api.classdb_get_method_bind(&native_class_name, &method_name, 4047867050);
        destructors.string_name_destructor(&native_class_name);
        destructors.string_name_destructor(&method_name);

        // Register class.
        ...
    }

Lưu ý rằng ở đây chúng ta sử dụng lại các biến ``native_class_name`` và ``method_name``, vì vậy không cần khai báo biến mới.

Bây giờ hãy mở tệp ``gdexample.h``, nơi chúng ta sẽ thêm một vài trường:

.. code-block:: c

    typedef struct
    {
        // Private properties.
        ..
        double time_emit;
        ..
        // Metadata.
        StringName position_changed; // For signal.
    } GDExample;

Trường đầu tiên sẽ lưu thời gian đã trôi qua kể từ lần phát tín hiệu gần nhất, vì chúng ta sẽ thực hiện việc này theo các khoảng thời gian đều đặn. Trường còn lại chỉ dùng để lưu vào bộ nhớ đệm tên tín hiệu, nhờ đó chúng ta không cần tạo một StringName mới mỗi lần.

Trong tệp mã nguồn ``gdexample.c``, chúng ta có thể thay đổi hàm khởi tạo và hàm hủy để xử lý các trường mới:

.. code-block:: c

    void gdexample_class_constructor(GDExample *self)
    {
        ...
        self->time_emit = 0.0;

        // Construct the StringName for the signal.
        constructors.string_name_new_with_latin1_chars(&self->position_changed, "position_changed", false);
    }

    void gdexample_class_destructor(GDExample *self)
    {
        // Destruct the StringName for the signal.
        destructors.string_name_destructor(&self->position_changed);
    }

Điều quan trọng là phải hủy StringName để tránh rò rỉ bộ nhớ.

Bây giờ chúng ta có thể thêm mã vào hàm ``gdexample_class_process()`` để thực sự phát tín hiệu:

.. code-block:: c

    void gdexample_class_process(GDExample *self, double delta)
    {
        ...

        self->time_emit += delta;
        if (self->time_emit >= 1.0)
        {
            // Call the emit_signal method.
            call_2_args_stringname_vector2_no_ret_variant(methods.object_emit_signal, self->object, &self->position_changed, &new_position);
            self->time_emit = 0.0;
        }
    }

Đoạn mã này cập nhật thời gian đã trôi qua cho việc phát tín hiệu và nếu thời gian đó vượt quá một giây, nó sẽ gọi hàm ``emit_signal()`` trên thực thể hiện tại, truyền tên tín hiệu và vị trí mới làm các đối số.

Bây giờ chúng ta đã hoàn tất C GDExtension. Hãy build lại một lần nữa và mở lại dự án Godot trong trình chỉnh sửa.

Trên trang tài liệu dành cho ``GDExample``, bạn có thể thấy tín hiệu mới mà chúng ta đã liên kết:

.. image:: img/gdextension_c_signal_doc.webp

Để kiểm tra xem nó có hoạt động hay không, hãy thêm một tập lệnh nhỏ vào nút gốc, là nút cha của nút tùy chỉnh, để in vị trí ra đầu ra mỗi khi nhận được tín hiệu:

.. code-block:: gdscript

    extends Node2D

    func _ready():
        $GDExample.position_changed.connect(on_position_changed)

    func on_position_changed(new_position):
        prints("New position:", new_position)

Chạy dự án và bạn có thể quan sát các giá trị được in trong bảng điều khiển Output của trình chỉnh sửa:

.. image:: img/gdextension_c_signal_print.webp

Kết luận
--------

Hướng dẫn này trình bày một extension cơ bản với các phương thức, thuộc tính và tín hiệu tùy chỉnh. Mặc dù cần khá nhiều mã mẫu, cách này có thể mở rộng tốt bằng việc tạo các hàm trợ giúp để xử lý những tác vụ tẻ nhạt.

Đây sẽ là nền tảng tốt để hiểu API GDExtension và là điểm khởi đầu để tạo các trình tạo binding tùy chỉnh. Trên thực tế, có thể tạo binding cho C bằng loại trình tạo này, khiến phần mã thực tế trông giống tệp ``gdexample.c`` trong ví dụ này hơn; tệp đó khá dễ hiểu và không quá dài dòng.

Nếu muốn tạo các extension thực sự, bạn nên sử dụng binding C++ thay thế, vì chúng loại bỏ toàn bộ mã mẫu khỏi mã của bạn. Hãy xem
:ref:`godot-cpp documentation <doc_godot_cpp>` to see how you can
để thực hiện việc này.
