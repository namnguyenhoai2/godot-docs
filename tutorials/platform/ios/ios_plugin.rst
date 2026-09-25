:article_outdated: Đúng

.. _doc_ios_plugin:

Tạo plugin iOS
==============

Trang này giải thích plugin iOS có thể làm gì cho bạn, cách sử dụng plugin hiện có và các bước viết code cho một plugin mới.

Plugin iOS cho phép bạn sử dụng các thư viện của bên thứ ba và hỗ trợ những tính năng dành riêng cho iOS như In-App Purchases, tích hợp GameCenter, hỗ trợ ARKit và nhiều tính năng khác.

Tải và sử dụng plugin hiện có
-----------------------------

Một plugin iOS cần có tệp cấu hình ``.gdip``, một tệp nhị phân có thể là thư viện tĩnh ``.a`` hoặc ``.xcframework`` chứa ``.a`` thư viện tĩnh, và có thể có các dependency khác. Để sử dụng plugin, bạn cần:

1. Sao chép các tệp của plugin vào thư mục ``res://ios/plugins`` trong dự án Godot của bạn. Bạn cũng có thể nhóm các tệp trong một thư mục con, chẳng hạn như ``res://ios/plugins/my_plugin``.

2. Trình chỉnh sửa Godot sẽ tự động phát hiện và nhập các tệp ``.gdip`` bên trong ``res://ios/plugins`` và các thư mục con của thư mục này.

3. Bạn có thể tìm và kích hoạt các plugin đã phát hiện bằng cách đi tới Project -> Export... -> iOS, sau đó trong tab Options, cuộn đến phần Plugins.

.. image:: img/ios_export_preset_plugins_section.png

Khi plugin đang hoạt động, bạn có thể truy cập plugin trong code bằng ``Engine.get_singleton()``:

::

    if Engine.has_singleton("MyPlugin"):
        var singleton = Engine.get_singleton("MyPlugin")
        print(singleton.foo())

.. note::

   Các tệp của plugin phải nằm trong thư mục ``res://ios/plugins/`` hoặc một thư mục con; nếu không, trình chỉnh sửa Godot sẽ không tự động phát hiện chúng.

Tạo plugin iOS
--------------

Về cốt lõi, plugin iOS của Godot là một thư viện iOS (tệp lưu trữ *.a* hoặc *.xcframework* chứa các thư viện tĩnh) với các yêu cầu sau:

- Thư viện phải có dependency vào các tệp header của Godot engine.

- Thư viện phải đi kèm với một tệp cấu hình ``.gdip``.

Plugin iOS có thể có cùng chức năng như một module Godot nhưng linh hoạt hơn và không yêu cầu build lại engine.

Sau đây là các bước để bắt đầu phát triển một plugin. Chúng tôi khuyến nghị sử dụng `Xcode <https://developer.apple.com/develop/>`_ làm môi trường phát triển.

.. seealso:: `Godot iOS Plugins <https://github.com/godotengine/godot-ios-plugins>`_.

    `Godot iOS plugin template <https://github.com/naithar/godot_ios_plugin>`_ cung cấp mọi mã khung cần thiết để bắt đầu phát triển plugin iOS.


Để build một plugin iOS:

1. Tạo một thư viện tĩnh Objective-C cho plugin bên trong Xcode.

2. Thêm các tệp header của Godot engine làm dependency cho thư viện plugin trong ``HEADER_SEARCH_PATHS``. Bạn có thể tìm thấy thiết lập này trong tab ``Build Settings``:

    - Tải source của Godot engine từ `Godot GitHub page <https://github.com/godotengine/godot>`_.

    - Chạy SCons để tạo các header. Bạn có thể tìm hiểu quy trình bằng cách đọc :ref:`doc_compiling_for_ios`. Bạn không cần chờ quá trình biên dịch hoàn tất mới tiếp tục, vì các header được tạo trước khi engine bắt đầu biên dịch.

    - Bạn nên sử dụng cùng các tệp header cho plugin iOS và export template iOS.

3. Trong tab ``Build Settings``, chỉ định các cờ biên dịch cho thư viện tĩnh trong ``OTHER_CFLAGS``. Các cờ quan trọng nhất là ``-fcxx-modules``, ``-fmodules`` và ``-DDEBUG`` nếu bạn cần hỗ trợ debug. Các cờ khác nên giống với những cờ bạn sử dụng để biên dịch Godot. Ví dụ:

::

    -DPTRCALL_ENABLED -DDEBUG_ENABLED -DDEBUG_MEMORY_ALLOC -DDISABLE_FORCED_INLINE -DTYPED_METHOD_BIND

4. Thêm logic cần thiết cho plugin và build thư viện để tạo tệp ``.a``. Có thể bạn sẽ cần build cả các tệp ``debug`` và ``release`` target ``.a``. Tùy theo nhu cầu, hãy chọn một hoặc cả hai. Nếu cần cả các tệp ``.a`` debug và release, tên của chúng phải khớp với mẫu sau: ``[PluginName].[TargetType].a``. Bạn cũng có thể build thư viện tĩnh bằng cấu hình SCons của mình.

5. Hệ thống plugin iOS cũng hỗ trợ các tệp ``.xcframework``. Để tạo một tệp, bạn có thể sử dụng lệnh như sau:

::

    xcodebuild -create-xcframework -library [DeviceLibrary].a -library [SimulatorLibrary].a -output [PluginName].xcframework

6. Tạo tệp cấu hình Godot iOS Plugin để giúp hệ thống phát hiện và tải plugin của bạn:

    -   Phần mở rộng của tệp cấu hình phải là ``gdip`` (ví dụ: ``MyPlugin.gdip``).

    -   Định dạng tệp cấu hình như sau:

    ::

            [config]
            name="MyPlugin"
            binary="MyPlugin.a"

            initialization="init_my_plugin"
            deinitialization="deinit_my_plugin"

            [dependencies]
            linked=[]
            embedded=[]
            system=["Foundation.framework"]

            capabilities=["arkit", "metal"]

            files=["data.json"]

            linker_flags=["-ObjC"]

            [plist]
            PlistKeyWithDefaultType="Some Info.plist key you might need"
            StringPlistKey:string="String value"
            IntegerPlistKey:integer=42
            BooleanPlistKey:boolean=true
            RawPlistKey:raw="
            <array>
                <string>UIInterfaceOrientationPortrait</string>
            </array>
            "
            StringPlistKeyToInput:string_input="Type something"

Phần và các trường ``config`` là bắt buộc và được định nghĩa như sau:

    -   **name**: tên của plugin

    -   **binary**: phải là filepath của tệp thư viện plugin (``a`` hoặc ``xcframework``).

        -   Filepath có thể là đường dẫn tương đối (ví dụ: ``MyPlugin.a``, ``MyPlugin.xcframework``); trong trường hợp đó, đường dẫn này tương đối với thư mục chứa tệp ``gdip``.
        -   Filepath có thể là đường dẫn tuyệt đối: ``res://some_path/MyPlugin.a`` hoặc ``res://some_path/MyPlugin.xcframework``.
        -   Nếu cần sử dụng thư viện multitarget, tên tệp phải là ``MyPlugin.a`` và các tệp ``.a`` phải được đặt tên là ``MyPlugin.release.a`` và ``MyPlugin.debug.a``.
        -   Nếu sử dụng các thư viện ``xcframework`` multitarget, tên tệp của chúng trong cấu hình phải là ``MyPlugin.xcframework``. Các tệp ``.xcframework`` phải được đặt tên là ``MyPlugin.release.xcframework`` và ``MyPlugin.debug.xcframework``.

Các phần ``dependencies`` và ``plist`` là tùy chọn và được định nghĩa như sau:

    -   **dependencies**:

        -   **linked**: chứa danh sách các framework iOS mà ứng dụng iOS cần được link với.

        -   **embedded**: chứa danh sách các framework hoặc thư viện iOS cần được vừa link vừa embed vào ứng dụng iOS kết quả.

        -   **system**: chứa danh sách các system framework của iOS cần thiết cho plugin.

        -   **capabilities**: chứa danh sách các capability của iOS cần thiết cho plugin. Bạn có thể tìm thấy danh sách các capability hiện có tại `Apple UIRequiredDeviceCapabilities documentation page <https://developer.apple.com/documentation/bundleresources/information_property_list/uirequireddevicecapabilities>`_.

        -   **files**: chứa danh sách các tệp cần được sao chép khi export. Điều này hữu ích cho các tệp dữ liệu hoặc hình ảnh.

        -   **linker_flags**: chứa danh sách các linker flag cần thêm vào dự án Xcode khi export plugin.

    -   **plist**: phải có các key và value cần xuất hiện trong tệp ``Info.plist``.

        -   Mỗi dòng phải theo mẫu: ``KeyName:KeyType=KeyValue``
        -   Các giá trị được hỗ trợ cho ``KeyType`` là ``string``, ``integer``, ``boolean``, ``raw``, ``string_input``
        -   Nếu không sử dụng kiểu nào (ví dụ: ``KeyName="KeyValue"``), kiểu ``string`` sẽ được sử dụng.
        -   Nếu sử dụng kiểu ``raw``, giá trị của khóa tương ứng sẽ được lưu trong ``Info.plist`` nguyên trạng.
        -   Nếu sử dụng kiểu ``string_input``, bạn sẽ có thể sửa đổi giá trị trong cửa sổ Export.

.. _`Xcode`: https://developer.apple.com/develop/
.. _`Godot iOS Plugins`: https://github.com/godotengine/godot-ios-plugins
.. _`Godot iOS plugin template`: https://github.com/naithar/godot_ios_plugin
.. _`Godot GitHub page`: https://github.com/godotengine/godot
.. _`Apple UIRequiredDeviceCapabilities documentation page`: https://developer.apple.com/documentation/bundleresources/information_property_list/uirequireddevicecapabilities
