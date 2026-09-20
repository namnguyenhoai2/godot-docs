.. _doc_using_sanitizers:

Sử dụng sanitizer
=================

Sanitizer là gì?
----------------

Sanitizer là các công cụ chèn mã tĩnh giúp tìm ra những lỗi mà trình gỡ lỗi truyền thống thường không thể phát hiện. Điều này đặc biệt hữu ích khi kết hợp với
:ref:`doc_unit_testing` in continuous integration.

Có thể sử dụng sanitizer trên Windows, macOS và Linux bằng các trình biên dịch Clang (LLVM), GCC hoặc Visual Studio.
:ref:`Certain platforms <doc_using_sanitizers_platform_specific_sanitizers>`
cũng có thể cung cấp sanitizer riêng. Trong những trường hợp một sanitizer được cung cấp bởi nhiều trình biên dịch khác nhau, hãy nhớ rằng đầu ra và hành vi của chúng sẽ hơi khác nhau.

Sử dụng sanitizer trên Godot
----------------------------

Sanitizer **yêu cầu** biên dịch lại tệp nhị phân. Điều này có nghĩa là bạn không thể sử dụng các tệp nhị phân Godot chính thức để chạy sanitizer.

Khi :ref:`compiling <toc-devel-compiling>` với bất kỳ sanitizer nào được bật, tệp nhị phân kết quả sẽ được thêm hậu tố ``.san`` vào tên để phân biệt với tệp nhị phân không có sanitizer.

Hiệu năng sẽ bị ảnh hưởng vì cần thực hiện nhiều kiểm tra bổ sung trong thời gian chạy. Mức sử dụng bộ nhớ cũng sẽ tăng. Có thể bật một số tổ hợp gồm nhiều sanitizer trong cùng một bản dựng. Tuy nhiên, hãy lưu ý tác động đến hiệu năng khi sử dụng đồng thời nhiều sanitizer, vì tệp nhị phân kết quả có thể chạy chậm quá mức.

Có thể truyền một số tùy chọn cho sanitizer mà không cần biên dịch lại tệp nhị phân bằng cách sử dụng các biến môi trường.

.. _doc_using_sanitizers_address_sanitizer:

Address sanitizer (ASAN)
------------------------

- Có trong Clang và GCC. - **Nền tảng được hỗ trợ:** Linux, macOS, Windows (Visual Studio), Web - `Tài liệu Clang ASAN <https://clang.llvm.org/docs/AddressSanitizer.html>`__

Address sanitizer nhìn chung là sanitizer được sử dụng thường xuyên nhất. Nó có thể chẩn đoán các vấn đề như tràn bộ đệm và truy cập ngoài phạm vi. Nếu engine gặp sự cố với thông báo như ``free(): invalid pointer``, thì nguyên nhân thường là do tràn bộ đệm. (Thông báo này được in bởi thời gian chạy C, không phải Godot.)

Trong một số tình huống nhất định (chẳng hạn như phát hiện việc đọc bộ nhớ chưa được khởi tạo), address sanitizer là chưa đủ. Thay vào đó nên sử dụng :ref:`doc_using_sanitizers_memory_sanitizer`.

Bạn cũng có thể phát hiện các tình huống sử dụng sau khi trả về bằng cách chỉ định biến môi trường ``ASAN_OPTIONS=detect_stack_use_after_return=1`` trước khi *chạy* Godot (không phải khi biên dịch). Điều này làm tăng chi phí thời gian chạy của address sanitizer, vì vậy chỉ bật tính năng này khi bạn thực sự cần.

Để bật address sanitizer trong bản dựng Godot, hãy truyền tùy chọn SCons ``use_asan=yes`` khi biên dịch. Việc bật ASAN thường khiến tệp nhị phân kết quả chậm hơn khoảng 2×.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một tệp nhị phân nhất định.

Leak sanitizer (LSAN)
---------------------

- Chỉ có trong Clang và GCC. - **Nền tảng được hỗ trợ:** Linux, Web - `Tài liệu Clang LSAN <https://clang.llvm.org/docs/LeakSanitizer.html>`__

Leak sanitizer có thể phát hiện rò rỉ bộ nhớ, tức là những trường hợp bộ nhớ không còn được sử dụng nhưng không bao giờ được chương trình đang chạy giải phóng. Điều này có thể dẫn đến tình trạng hết bộ nhớ nếu chương trình chạy đủ lâu. Vì Godot có thể chạy trên
:ref:`dedicated servers <doc_exporting_for_dedicated_servers>` for months or
thậm chí nhiều năm mà không khởi động lại, nên việc khắc phục rò rỉ bộ nhớ ngay khi chúng xảy ra là rất quan trọng.

Để bật leak sanitizer trong bản dựng Godot, hãy truyền tùy chọn SCons ``use_lsan=yes`` khi biên dịch. Việc bật LSAN chỉ gây ra một mức chi phí hiệu năng nhỏ, nhưng chương trình sẽ thoát chậm hơn nhiều vì quá trình phát hiện rò rỉ diễn ra khi chương trình thoát.

.. _doc_using_sanitizers_memory_sanitizer:

Memory sanitizer (MSAN)
-----------------------

- Chỉ có trong Clang, không có trong GCC. - **Nền tảng được hỗ trợ:** Linux - `Tài liệu Clang MSAN <https://clang.llvm.org/docs/MemorySanitizer.html>`__

Memory sanitizer bổ sung cho
:ref:`doc_using_sanitizers_address_sanitizer`. Unlike the address sanitizer,
memory sanitizer có thể phát hiện việc đọc bộ nhớ chưa được khởi tạo.

Để bật memory sanitizer trong bản dựng Godot, hãy truyền tùy chọn SCons ``use_msan=yes`` khi biên dịch. Việc bật MSAN thường khiến tệp nhị phân kết quả chậm hơn khoảng 3×.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một tệp nhị phân nhất định.

Thread sanitizer (TSAN)
-----------------------

- Có trong Clang và GCC. - **Nền tảng được hỗ trợ:** Linux, macOS - `Tài liệu Clang TSAN <https://clang.llvm.org/docs/ThreadSanitizer.html>`__

Thread sanitizer được sử dụng để truy tìm các điều kiện tranh chấp liên quan đến đa luồng. Điều kiện tranh chấp xảy ra khi nhiều luồng cố gắng sửa đổi cùng một dữ liệu tại cùng một thời điểm. Vì hệ điều hành có thể sắp xếp lịch luồng theo bất kỳ cách nào, điều này dẫn đến hành vi không chính xác chỉ thỉnh thoảng xảy ra (và do đó có thể khó truy tìm). Để ngăn điều kiện tranh chấp, bạn cần thêm một khóa nhằm bảo đảm chỉ một luồng có thể truy cập dữ liệu dùng chung tại một thời điểm nhất định.

Để bật thread sanitizer trong bản dựng Godot, hãy truyền tùy chọn SCons ``use_tsan=yes`` khi biên dịch. Việc bật TSAN thường khiến tệp nhị phân kết quả chậm hơn 10×, đồng thời làm mức sử dụng bộ nhớ tăng khoảng 8×.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một tệp nhị phân nhất định.

.. note::

    Trên Linux, nếu bạn gặp lỗi sau:

    ``FATAL: ThreadSanitizer: unexpected memory mapping``

    Bạn có thể cần tạm thời giảm entropy của Address Space Layout Randomization (ASLR) trên hệ thống bằng lệnh:

    .. code:: sh

        sudo sysctl vm.mmap_rnd_bits=28

    Hoặc tốt hơn là vô hiệu hóa hoàn toàn bằng lệnh:

    .. code:: sh

        sudo sysctl kernel.randomize_va_space=0

    Ngay sau khi hoàn tất việc sử dụng thread sanitizer, hãy tăng entropy ASLR bằng lệnh:

    .. code:: sh

        sudo sysctl vm.mmap_rnd_bits=32

    Hoặc bật lại ASLR bằng lệnh:

    .. code:: sh

        sudo sysctl kernel.randomize_va_space=2

    Việc khởi động lại máy cũng sẽ đưa trạng thái ASLR về các giá trị mặc định.

    Điều quan trọng là phải hoàn tác các thay đổi càng sớm càng tốt, vì việc giảm entropy ASLR hoặc vô hiệu hóa hoàn toàn ASLR có thể gây ra rủi ro bảo mật.

Undefined behavior sanitizer (UBSAN)
------------------------------------

- Có trong Clang và GCC. - **Nền tảng được hỗ trợ:** Linux, macOS, Web - `Tài liệu Clang UBSAN <https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html>`__

Undefined behavior sanitizer được sử dụng để truy tìm những tình huống chương trình thể hiện hành vi ngẫu nhiên và không thể dự đoán. Điều này là do mã C/C++ được trình biên dịch chấp nhận nhưng không *đúng*. Việc biên dịch với một tập tối ưu hóa khác cũng có thể thay đổi kết quả quan sát được của hành vi không xác định.

Để bật undefined behavior sanitizer trong bản dựng Godot, hãy truyền tùy chọn SCons ``use_ubsan=yes`` khi biên dịch. Việc bật UBSAN chỉ gây ra một mức chi phí hiệu năng nhỏ.

.. _doc_using_sanitizers_platform_specific_sanitizers:

Sanitizer dành riêng cho từng nền tảng
--------------------------------------

Web
~~~

Khi :ref:`compiling for the Web <doc_compiling_for_web>`, có thêm 2 tùy chọn SCons cho sanitizer:

- ``use_assertions=yes`` bật các assertion Emscripten trong thời gian chạy, có thể phát hiện nhiều vấn đề khác nhau. - ``use_safe_heap=yes`` bật `sanitizer SAFE_HEAP của Emscripten <https://emscripten.org/docs/debugging/Sanitizers.html>`__. Nó cung cấp chức năng tương tự ASAN, nhưng tập trung vào các vấn đề dành riêng cho WebAssembly. ``SAFE_HEAP`` không được bảo đảm tương thích với ASAN và UBSAN trong cùng một tệp nhị phân, vì vậy bạn có thể phải xây dựng riêng.
