.. _doc_using_sanitizers:

Sử dụng sanitizer
=================

Sanitizer là gì?
----------------

Sanitizer là các công cụ chèn mã tĩnh giúp tìm ra những lỗi mà trình gỡ lỗi truyền thống thường không thể phát hiện. Điều này đặc biệt hữu ích khi kết hợp với
:ref:`doc_unit_testing` trong tích hợp liên tục.

Có thể sử dụng sanitizer trên Windows, macOS và Linux bằng các compiler Clang (LLVM), GCC hoặc Visual Studio.
:ref:`Một số nền tảng <doc_using_sanitizers_platform_specific_sanitizers>` cũng có thể cung cấp sanitizer riêng. Trong trường hợp một sanitizer được cung cấp bởi nhiều compiler khác nhau, hãy nhớ rằng kết quả và hành vi của chúng sẽ hơi khác nhau.

Sử dụng sanitizer trên Godot
----------------------------

Sanitizer **yêu cầu** biên dịch lại binary. Điều này có nghĩa là bạn không thể sử dụng binary Godot chính thức để chạy sanitizer.

Khi :ref:`biên dịch <toc-devel-compiling>` với bất kỳ sanitizer nào được bật, binary tạo ra sẽ được thêm hậu tố ``.san`` vào tên để phân biệt với binary không có sanitizer.

Hiệu năng sẽ bị ảnh hưởng vì cần thực hiện nhiều kiểm tra runtime bổ sung. Mức sử dụng bộ nhớ cũng sẽ tăng. Có thể bật một số tổ hợp gồm nhiều sanitizer trong cùng một bản build. Tuy nhiên, hãy lưu ý đến ảnh hưởng hiệu năng khi sử dụng nhiều sanitizer cùng lúc, vì binary tạo ra có thể chậm quá mức.

Có thể truyền một số tùy chọn cho sanitizer thông qua các biến môi trường mà không cần biên dịch lại binary.

.. _doc_using_sanitizers_address_sanitizer:

Address sanitizer (ASAN)
------------------------

- Có trong Clang và GCC.
- **Nền tảng được hỗ trợ:** Linux, macOS, Windows (Visual Studio), Web
- `Tài liệu Clang ASAN <https://clang.llvm.org/docs/AddressSanitizer.html>`__

Address sanitizer nhìn chung là sanitizer được sử dụng thường xuyên nhất. Nó có thể chẩn đoán các vấn đề như tràn bộ đệm và truy cập vượt phạm vi. Nếu engine gặp sự cố với thông báo như ``free(): invalid pointer``, thì nguyên nhân thường là do tràn bộ đệm. (Thông báo này do C runtime in ra, không phải Godot.)

Trong một số trường hợp (chẳng hạn như phát hiện thao tác đọc bộ nhớ chưa được khởi tạo), address sanitizer là chưa đủ. Thay vào đó, nên sử dụng :ref:`doc_using_sanitizers_memory_sanitizer`.

Bạn cũng có thể phát hiện các tình huống sử dụng sau khi trả về bằng cách chỉ định biến môi trường ``ASAN_OPTIONS=detect_stack_use_after_return=1`` trước khi *chạy* Godot (không phải khi biên dịch Godot). Điều này làm tăng overhead runtime của address sanitizer, vì vậy chỉ bật tính năng này khi thực sự cần.

Để bật address sanitizer trong bản build Godot, hãy truyền tùy chọn SCons ``use_asan=yes`` khi biên dịch. Việc bật ASAN thường khiến binary tạo ra chậm hơn khoảng 2 lần.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một binary nhất định.

Leak sanitizer (LSAN)
---------------------

- Có trong Clang và GCC.
- **Nền tảng được hỗ trợ:** Linux, Web
- `Tài liệu Clang LSAN <https://clang.llvm.org/docs/LeakSanitizer.html>`__

Leak sanitizer có thể phát hiện rò rỉ bộ nhớ, tức là những trường hợp bộ nhớ không còn được sử dụng nhưng không bao giờ được chương trình đang chạy giải phóng. Điều này có thể dẫn đến tình trạng hết bộ nhớ nếu chương trình chạy đủ lâu. Vì Godot có thể chạy trên
:ref:`server chuyên dụng <doc_exporting_for_dedicated_servers>` trong nhiều tháng hoặc thậm chí nhiều năm mà không khởi động lại, nên việc khắc phục rò rỉ bộ nhớ ngay khi chúng xảy ra là rất quan trọng.

Để bật leak sanitizer trong bản build Godot, hãy truyền tùy chọn SCons ``use_lsan=yes`` khi biên dịch. Việc bật LSAN chỉ gây overhead hiệu năng nhỏ, nhưng chương trình sẽ thoát chậm hơn nhiều vì quá trình phát hiện rò rỉ diễn ra khi chương trình thoát.

.. _doc_using_sanitizers_memory_sanitizer:

Memory sanitizer (MSAN)
-----------------------

- Chỉ có trong Clang, không có trong GCC.
- **Nền tảng được hỗ trợ:** Linux
- `Tài liệu Clang MSAN <https://clang.llvm.org/docs/MemorySanitizer.html>`__

Memory sanitizer bổ trợ cho
:ref:`doc_using_sanitizers_address_sanitizer`. Không giống address sanitizer, memory sanitizer có thể phát hiện thao tác đọc bộ nhớ chưa được khởi tạo.

Để bật memory sanitizer trong bản build Godot, hãy truyền tùy chọn SCons ``use_msan=yes`` khi biên dịch. Việc bật MSAN thường khiến binary tạo ra chậm hơn khoảng 3 lần.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một binary nhất định.

Thread sanitizer (TSAN)
-----------------------

- Có trong Clang và GCC.
- **Nền tảng được hỗ trợ:** Linux, macOS
- `Tài liệu Clang TSAN <https://clang.llvm.org/docs/ThreadSanitizer.html>`__

Thread sanitizer được dùng để truy tìm các race condition liên quan đến đa luồng. Race condition xảy ra khi nhiều thread cố gắng sửa đổi cùng một dữ liệu tại cùng một thời điểm. Vì hệ điều hành có thể sắp xếp thứ tự lập lịch thread theo bất kỳ cách nào, điều này dẫn đến hành vi không chính xác chỉ xảy ra đôi khi (và do đó có thể khó truy tìm). Để ngăn race condition, bạn cần thêm một lock nhằm bảo đảm chỉ một thread có thể truy cập dữ liệu dùng chung tại một thời điểm nhất định.

Để bật thread sanitizer trong bản build Godot, hãy truyền tùy chọn SCons ``use_tsan=yes`` khi biên dịch. Việc bật TSAN thường khiến binary tạo ra chậm hơn 10 lần, đồng thời làm mức sử dụng bộ nhớ tăng khoảng 8 lần.

.. warning::

    Do một `quyết định thiết kế <https://stackoverflow.com/questions/36971902/why-cant-clang-enable-all-sanitizers/>`__, address sanitizer, memory sanitizer và thread sanitizer loại trừ lẫn nhau. Điều này có nghĩa là bạn chỉ có thể sử dụng một trong các sanitizer đó trong một binary nhất định.

.. note::

    Trên Linux, nếu gặp lỗi sau:

    ``FATAL: ThreadSanitizer: unexpected memory mapping``

    Bạn có thể cần tạm thời giảm entropy của Address Space Layout Randomization (ASLR) trên hệ thống bằng lệnh:

    .. code:: sh

        sudo sysctl vm.mmap_rnd_bits=28

    Hoặc tốt hơn là tắt hoàn toàn bằng lệnh:

    .. code:: sh

        sudo sysctl kernel.randomize_va_space=0

    Ngay sau khi sử dụng xong thread sanitizer, hãy tăng entropy của ASLR bằng lệnh:

    .. code:: sh

        sudo sysctl vm.mmap_rnd_bits=32

    Hoặc bật lại ASLR bằng lệnh:

    .. code:: sh

        sudo sysctl kernel.randomize_va_space=2

    Khởi động lại máy cũng sẽ đưa trạng thái ASLR về các giá trị mặc định.

    Điều quan trọng là hoàn tác các thay đổi sớm nhất có thể vì việc giảm entropy của ASLR hoặc vô hiệu hóa hoàn toàn ASLR có thể gây ra rủi ro bảo mật.

Bộ sanitizer cho hành vi không xác định (UBSAN)
-----------------------------------------------

- Có trong Clang và GCC.
- **Các nền tảng được hỗ trợ:** Linux, macOS, Web
- `Tài liệu Clang UBSAN <https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html>`__

Bộ sanitizer cho hành vi không xác định được dùng để tìm ra các tình huống trong đó chương trình thể hiện hành vi ngẫu nhiên và không thể dự đoán. Điều này là do mã C/C++ được compiler chấp nhận nhưng không *đúng*. Việc biên dịch với một tập tối ưu hóa khác cũng có thể thay đổi kết quả quan sát được của hành vi không xác định.

Để bật bộ sanitizer cho hành vi không xác định trong bản build Godot, hãy truyền tùy chọn SCons ``use_ubsan=yes`` khi biên dịch. Việc bật UBSAN chỉ gây ra một mức overhead hiệu năng nhỏ.

.. _doc_using_sanitizers_platform_specific_sanitizers:

Các bộ sanitizer dành riêng cho nền tảng
----------------------------------------

Web
~~~

Khi :ref:`biên dịch cho Web <doc_compiling_for_web>`, có thêm 2 tùy chọn SCons của sanitizer:

- ``use_assertions=yes`` bật các assertion runtime của Emscripten, có thể phát hiện nhiều vấn đề khác nhau.
- ``use_safe_heap=yes`` bật `bộ sanitizer SAFE_HEAP của Emscripten <https://emscripten.org/docs/debugging/Sanitizers.html>`__. Nó cung cấp chức năng tương tự ASAN nhưng tập trung vào các vấn đề đặc thù của WebAssembly. ``SAFE_HEAP`` không được đảm bảo tương thích với ASAN và UBSAN trong cùng một binary, vì vậy bạn có thể phải build riêng.
