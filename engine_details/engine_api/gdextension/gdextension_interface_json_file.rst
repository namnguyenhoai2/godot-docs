.. _doc_gdextension_interface_json_file:

Tệp JSON giao diện C
====================

Tệp ``gdextension_interface.json`` là "nguồn chân lý" cho API C mà Godot sử dụng để giao tiếp với GDExtension.

Bạn có thể sử dụng tệp thực thi Godot để kết xuất tệp bằng lệnh sau:

.. code-block:: shell

    godot --headless --dump-gdextension-interface-json

Tệp này предназначается cho các liên kết ngôn ngữ GDExtension sử dụng để tạo mã cho việc dùng API này theo hình thức phù hợp nhất với ngôn ngữ đó.

.. note::

    Không nên nhầm tệp này với ``extension_api.json``, vốn cũng được các liên kết ngôn ngữ GDExtension sử dụng và chứa thông tin về các lớp và phương thức được Godot cung cấp. ``gdextension_interface.json`` ở mức thấp hơn và được sử dụng để tương tác với các lớp và phương thức cấp cao hơn đó.

Đối với các ngôn ngữ có thể được mở rộng thông qua C hoặc cung cấp công cụ để tương tác với mã C, bạn cũng có thể sử dụng tệp thực thi Godot để kết xuất một tệp tiêu đề C được tạo tự động:

.. code-block:: shell

    godot --headless --dump-gdextension-interface

.. note::

    Tệp tiêu đề này tương thích với các phiên bản trước của tệp tiêu đề được đi kèm với Godot 4.5 trở về trước, nghĩa là nó giữ lại một số lỗi chính tả trong tên để đảm bảo khả năng tương thích.

Mục tiêu của trang này là giải thích định dạng JSON cho các liên kết ngôn ngữ GDExtension muốn tự tạo mã từ JSON.

Cấu trúc tổng thể
-----------------

Tệp JSON được chia thành 3 phần:

- Phần tiêu đề, bao gồm một số thông tin linh tinh ở cấp cao nhất của tệp JSON. - Khóa ``types``, định nghĩa tất cả các kiểu được sử dụng trong giao diện GDExtension. - Khóa ``interface``, định nghĩa tất cả các con trỏ hàm có thể được tải thông qua con trỏ hàm ``GDExtensionInterfaceGetProcAddress``, được truyền cho mọi GDExtension khi chúng được tải.

Mã nguồn Godot có kèm theo một `lược đồ JSON hoàn chỉnh <https://github.com/godotengine/godot/blob/master/core/extension/gdextension_interface.schema.json>`__.

Mặc dù chúng tôi có thể bổ sung các kiểu và hàm giao diện mới trong mỗi bản phát hành phụ của Godot, chúng tôi cố gắng **không bao giờ** thay đổi chúng theo cách không tương thích ngược hoặc xóa chúng. Mỗi hàm giao diện đều được gắn nhãn phiên bản Godot mà nó được giới thiệu (khóa ``since``), vì vậy bạn luôn có thể sử dụng phiên bản tệp mới nhất và chỉ cần tránh sử dụng bất kỳ thứ gì trong các phiên bản Godot mới hơn phiên bản bạn đang nhắm đến.

Tiêu đề
-------

"Tiêu đề" gồm 3 khóa linh tinh ở cấp cao nhất của tệp:

- ``_copyright``: Văn bản bản quyền và giấy phép tiêu chuẩn mà Godot đưa vào tất cả các tệp mã nguồn. - ``$schema``: Trỏ đến lược đồ JSON tương đối so với tệp này. Việc đặt lược đồ trong cùng thư mục có thể hữu ích nếu bạn xem tệp bằng trình soạn thảo mã hiểu lược đồ JSON. - ``format_version``: Một số nguyên biểu thị phiên bản của định dạng tệp (tức là lược đồ). Hiện tại chỉ có một phiên bản định dạng (``1``). Nếu chúng tôi thay đổi định dạng tệp theo cách không tương thích, chúng tôi sẽ tăng số này. Số này *không* phản ánh phiên bản dữ liệu trong tệp (vì vậy sẽ không thay đổi giữa các phiên bản Godot), mà chỉ phản ánh định dạng của tệp. Hy vọng rằng chúng tôi sẽ không bao giờ phải sử dụng đến nó, nhưng nó cho phép các trình tạo mã báo lỗi sớm nếu gặp một giá trị không mong đợi tại đây.

Kiểu
----

Phần ``types`` là một mảng các kiểu sẽ được các kiểu khác và các hàm giao diện trong phần cuối cùng sử dụng.

Các kiểu phải được đánh giá theo thứ tự. Các kiểu đứng sau có thể tham chiếu đến các kiểu đứng trước, nhưng các kiểu đứng trước sẽ không tham chiếu đến các kiểu đứng sau.

Có một tập hợp nhỏ các kiểu dựng sẵn không được liệt kê rõ ràng trong JSON:

- ``void`` - ``int8_t`` - ``uint8_t`` - ``int16_t`` - ``uint16_t`` - ``int32_t`` - ``uint32_t`` - ``int64_t`` - ``uint64_t`` - ``size_t`` (``uint32_t`` trên kiến trúc 32-bit và ``uint64_t`` trên kiến trúc 64-bit) - ``char`` - ``char16_t`` - ``char32_t`` - ``wchar_t`` - ``float`` - ``double``

Các kiểu này tương ứng với những kiểu C tương đương.

Ngoài ra, kiểu có thể bao gồm các bổ từ như sau:

- ``*`` (ví dụ: ``int8_t*``) để biểu thị con trỏ đến kiểu - ``const`` (ví dụ: ``const int8_t*``) để biểu thị kiểu hằng

Mỗi kiểu được định nghĩa trong tệp JSON thuộc một trong 5 "loại":

- ``enum`` - ``handle`` - ``alias`` - ``struct`` - ``function``

Bất kể thuộc "loại" nào, mọi kiểu đều có thể có các khóa sau:

- ``kind`` (bắt buộc): "Loại" của kiểu. - ``name`` (bắt buộc): Tên của kiểu, có thể được sử dụng như một định danh C hợp lệ. - ``description``: Một mảng các chuỗi mô tả kiểu, trong đó mỗi chuỗi là một dòng tài liệu (định dạng này cho ``description`` được sử dụng xuyên suốt tệp JSON). - ``deprecated``: Một đối tượng có các khóa riêng, gồm phiên bản Godot mà kiểu bị phản đối (``since``), thông báo giải thích việc phản đối (``message``) và, tùy chọn, một kiểu thay thế nên sử dụng (``replacement``).

Enum
~~~~

Enum là các số nguyên 32-bit có một tập hợp giá trị khả dĩ cố định. Trong C, chúng có thể được biểu diễn dưới dạng ``enum``.

Chúng có các khóa sau:

- ``is_bitfield``: Nếu là true, enum này là một trường bit, trong đó các giá trị enum có thể được kết hợp bằng phép OR theo bit. Mặc định là false. - ``values``: Mảng các giá trị cố định cho enum này, mỗi giá trị có ``name``, ``value`` và ``description``.

Một enum nên được biểu diễn dưới dạng ``int32_t``, trừ khi ``is_bitfield`` là true; khi đó nên sử dụng ``uint32_t``.

Ví dụ
+++++

.. code-block:: json

    {
        "name": "GDExtensionInitializationLevel",
        "kind": "enum",
        "values": [
            {
                "name": "GDEXTENSION_INITIALIZATION_CORE",
                "value": 0
            },
            {
                "name": "GDEXTENSION_INITIALIZATION_SERVERS",
                "value": 1
            },
            {
                "name": "GDEXTENSION_INITIALIZATION_SCENE",
                "value": 2
            },
            {
                "name": "GDEXTENSION_INITIALIZATION_EDITOR",
                "value": 3
            },
            {
                "name": "GDEXTENSION_MAX_INITIALIZATION_LEVEL",
                "value": 4
            }
        ]
    }

Handle
~~~~~~

Handle là các con trỏ đến những struct không hiển thị cấu trúc. Trong C, chúng có thể được biểu diễn dưới dạng ``void *`` hoặc ``struct{} *``.

Chúng có các khóa sau:

- ``is_const``: Nếu là true, kiểu handle này được xử lý như một "con trỏ hằng", nghĩa là dữ liệu bên trong sẽ không bị thay đổi. Mặc định là false. - ``is_uninitialized``: Nếu là true, kiểu handle này được xử lý như trỏ đến vùng nhớ chưa khởi tạo (có thể được khởi tạo bằng các hàm giao diện). Mặc định là false. - ``parent``: Tên tùy chọn của một kiểu handle khác, nếu kiểu handle này là phiên bản hằng hoặc chưa khởi tạo của kiểu cha. Điều này chỉ có ý nghĩa nếu ``is_const`` hoặc ``is_uninitialized`` là true.

Handle có kích thước bằng kích thước con trỏ trên kiến trúc tương ứng (ví dụ: 64-bit trên x86_64 và 32-bit trên x86_32).

Ví dụ
+++++

.. code-block:: json

    {
        "name": "GDExtensionStringNamePtr",
        "kind": "handle"
    }

Bí danh
~~~~~~~

Bí danh là các tên thay thế cho một kiểu. Trong C, chúng có thể được biểu diễn dưới dạng ``typedef``.

Chúng chỉ có thêm một khóa:

- ``type``: Kiểu mà bí danh là tên thay thế. Kiểu này có thể bao gồm các bổ từ như mô tả ở trên.

Các kiểu này phải được biểu diễn bằng cùng kiểu C với kiểu mà chúng tham chiếu đến.

Ví dụ
+++++

.. code-block:: json

    {
        "name": "GDExtensionInt",
        "kind": "alias",
        "type": "int64_t"
    }

Struct
~~~~~~

Struct biểu diễn C ``struct``\ s (hay còn gọi là một khối bộ nhớ gồm các thành viên đã cho theo thứ tự) và phải tuân theo mọi quy tắc bố cục và căn chỉnh giống như struct C.

Chúng chỉ có thêm một khóa:

- ``members``: Một mảng các đối tượng có ``name``, ``type`` (có thể bao gồm các bổ từ) và ``description``.

Ví dụ
+++++

.. code-block:: json

    {
        "name": "GDExtensionCallError",
        "kind": "struct",
        "members": [
            {
                "name": "error",
                "type": "GDExtensionCallErrorType"
            },
            {
                "name": "argument",
                "type": "int32_t"
            },
            {
                "name": "expected",
                "type": "int32_t"
            }
        ]
    }

Hàm
~~~

Hàm biểu diễn các kiểu con trỏ hàm C, với một danh sách đối số và một kiểu trả về, đồng thời phải tuân theo các yêu cầu về kích thước và căn chỉnh giống như con trỏ hàm C.

Chúng có các thành viên sau:

- ``return_value``: Một đối tượng có ``type`` (có thể bao gồm các bổ từ) và ``description``. Nếu hàm không có giá trị trả về, khóa này sẽ bị bỏ qua. - ``arguments`` (bắt buộc): Một mảng các đối số hàm, trong đó mỗi đối số có ``type`` (có thể bao gồm các bổ từ), ``name`` và ``description``.


Ví dụ
+++++

.. code-block:: json

    {
        "name": "GDExtensionPtrConstructor",
        "kind": "function",
        "arguments": [
            {
                "name": "p_base",
                "type": "GDExtensionUninitializedTypePtr"
            },
            {
                "name": "p_args",
                "type": "const GDExtensionConstTypePtr*"
            }
        ]
    }

Giao diện
---------

Phần ``interface`` của tệp JSON là danh sách các hàm giao diện, có thể được tải bởi ``name`` bằng con trỏ hàm ``GDExtensionInterfaceGetProcAddress``, được truyền cho mọi GDExtension khi chúng được tải.

Các hàm giao diện có một số khóa giống như kiểu, bao gồm ``name`` (bắt buộc), ``deprecated`` và ``description``.

Ngoài ra, chúng có ``return_value`` và ``arguments`` (bắt buộc), với định dạng giống các khóa tương đương trên kiểu hàm (như mô tả trong phần trước).

Chỉ có một số ít khóa riêng biệt:

- ``since`` (bắt buộc): Phiên bản Godot đã giới thiệu hàm giao diện này. - ``see``: Một mảng các chuỗi mô tả những tham chiếu bên ngoài chứa thêm thông tin, chẳng hạn như tên các lớp hoặc hàm trong mã nguồn Godot hoặc URL trỏ đến tài liệu. - ``legacy_type_name``: Tên cũ được sử dụng cho kiểu con trỏ hàm trong tệp tiêu đề do Godot tạo ra, khi tên cũ không khớp với mẫu được sử dụng cho các tên kiểu này. Trường này chỉ tồn tại để chúng tôi có thể tạo tệp tiêu đề theo cách tương thích ngược với tệp tiêu đề từ Godot 4.5 trở về trước và không nên được sử dụng trừ khi bạn cũng cần duy trì khả năng tương thích với tệp tiêu đề cũ.

Ví dụ
~~~~~

.. code-block:: json

    {
        "name": "get_godot_version",
        "arguments": [
            {
                "name": "r_godot_version",
                "type": "GDExtensionGodotVersion*",
                "description": [
                    "A pointer to the structure to write the version information into."
                ]
            }
        ],
        "description": [
            "Gets the Godot version that the GDExtension was loaded into."
        ],
        "since": "4.1",
        "deprecated": {
            "since": "4.5",
            "replace_with": "get_godot_version2"
        }
    }
