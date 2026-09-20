.. _doc_overview_of_debugging_tools:

Tổng quan về các công cụ debug
==============================

Hướng dẫn này sẽ cung cấp cho bạn tổng quan về các công cụ debug hiện có trong engine.

Godot đi kèm với một debugger mạnh mẽ và các profiler để tìm lỗi, kiểm tra game trong runtime, theo dõi các chỉ số thiết yếu và đo hiệu năng. Godot cũng cung cấp các tùy chọn để trực quan hóa các hộp va chạm và polygon điều hướng trong game đang chạy.

Cuối cùng, bạn có các tùy chọn để debug game đang chạy trên một thiết bị từ xa và tải lại các thay đổi đối với scene hoặc code trong khi game đang chạy.

Output Panel
------------

Output panel cho phép bạn xem văn bản được project in ra, cũng như văn bản do editor in ra (ví dụ: từ các script ``@tool``). Bạn có thể tìm thông tin về vấn đề này trong :ref:`doc_output_panel`.

Debugger Panel
--------------

Nhiều công cụ debug của Godot thuộc Debugger panel; bạn có thể tìm thông tin về chúng trong :ref:`doc_debugger_panel`.

Các tùy chọn trong menu debug
-----------------------------

Có một số tùy chọn debug phổ biến mà bạn có thể bật hoặc tắt khi chạy game trong editor, giúp bạn debug game.

Bạn có thể tìm các tùy chọn này trong menu **Debug** của editor.

.. image:: img/overview_debug.webp

Dưới đây là mô tả về các tùy chọn:

Deploy with Remote Debug
~~~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, việc sử dụng one-click deploy sẽ khiến executable cố gắng kết nối đến IP của máy tính này để có thể debug project đang chạy. Tùy chọn này предназнач dành cho remote debugging (thường là với thiết bị di động). Bạn không cần bật tùy chọn này để sử dụng GDScript debugger cục bộ.

Small Deploy with Network Filesystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này tăng tốc quá trình kiểm thử các game có dung lượng lớn trên những thiết bị từ xa.

Khi **Small Deploy with Network Filesystem** được bật, thay vì export toàn bộ game, việc deploy game sẽ build một executable tối giản. Sau đó, editor cung cấp các file của project qua network.

Ngoài ra, trên Android, game được deploy bằng cáp USB để tăng tốc quá trình deploy.

Visible Collision Shapes
~~~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, các collision shape và node raycast (cho 2D và 3D) sẽ hiển thị trong project đang chạy.

Visible Paths
~~~~~~~~~~~~~

Khi tùy chọn này được bật, các curve resource được các node path sử dụng sẽ hiển thị trong project đang chạy.

Visible Navigation
~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, các navigation mesh và polygon sẽ hiển thị trong project đang chạy.

Visible Avoidance
~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, các shape, bán kính và vận tốc của đối tượng avoidance sẽ hiển thị trong project đang chạy.

Debug CanvasItem Redraws
~~~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, các yêu cầu redraw của đối tượng 2D sẽ hiển thị (dưới dạng một đợt nháy ngắn) trong project đang chạy. Tùy chọn này hữu ích để khắc phục sự cố low processor mode.

Synchronize Scene Changes
~~~~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, mọi thay đổi được thực hiện đối với scene trong editor sẽ được sao chép sang project đang chạy. Khi sử dụng từ xa trên một thiết bị, tùy chọn này hiệu quả hơn khi network filesystem được bật.

Synchronize Script Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, mọi thay đổi được thực hiện đối với script trong editor sẽ được tải lại trong project đang chạy. Khi sử dụng từ xa trên một thiết bị, tùy chọn này hiệu quả hơn khi dùng network filesystem.

Keep Debug Server Open
~~~~~~~~~~~~~~~~~~~~~~

Khi tùy chọn này được bật, debug server của editor sẽ tiếp tục mở và lắng nghe các session mới được khởi chạy bên ngoài chính editor.

Customize Run Instances...
~~~~~~~~~~~~~~~~~~~~~~~~~~

Thao tác này mở một hộp thoại cho phép bạn yêu cầu Godot chạy đồng thời nhiều instance của game và chỉ định các command-line argument cho từng instance. Tùy chọn này đặc biệt hữu ích khi build và debug game multiplayer.

.. image:: img/customize_run_instances.webp

Enable Multiple Instances
^^^^^^^^^^^^^^^^^^^^^^^^^

Khi tùy chọn này được bật, editor sẽ chạy đồng thời nhiều instance của project khi bạn Run Project.

Bên dưới checkbox này là một bộ chọn để chọn số lượng instance cần chạy.

Đánh dấu checkbox và đặt giá trị này chỉ là 1 cũng giống như hoàn toàn không đánh dấu checkbox.

Main Run Args
^^^^^^^^^^^^^

Đây là các argument sẽ được truyền cho **mọi** instance của project khi bạn Run Project, trừ khi bạn chọn "Enabled" bên dưới "Override Main Run Args" cho một instance cụ thể.

Lưu ý rằng các argument này được phân tách bằng dấu cách.

.. tip::

    Bạn có thể truy cập các argument này trong script bằng cách sử dụng
    :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>`.

.. warning::

    Ngay cả khi bạn bỏ chọn "Enable Multiple Instances", các argument này vẫn sẽ được truyền khi bạn Run Project.

Main Feature Tags
^^^^^^^^^^^^^^^^^

Đây là các feature tag sẽ được truyền cho **mọi** instance của project khi bạn Run Project, trừ khi bạn chọn "Enabled" bên dưới "Override Main Tags" cho một instance cụ thể.

Override Main Run Args
^^^^^^^^^^^^^^^^^^^^^^

Khi tùy chọn này được bật, các argument trong trường "Main Run Args" sẽ **không được truyền** cho instance cụ thể này của project khi bạn Run Project.

Launch Arguments
^^^^^^^^^^^^^^^^

Đây là các argument sẽ được truyền cho instance cụ thể này của project khi bạn Run Project. Chúng sẽ được **kết hợp với** "Main Run Args", trừ khi bạn chọn "Enabled" bên dưới "Override Main Run Args".

Override Main Tags
^^^^^^^^^^^^^^^^^^

Khi tùy chọn này được bật, các tag trong trường "Main Feature Tags" sẽ **không được truyền** cho instance cụ thể này của project khi bạn Run Project.

Feature Tags
^^^^^^^^^^^^

Đây là các feature tag sẽ được truyền cho instance cụ thể này của project khi bạn Run Project. Chúng sẽ được **kết hợp với** "Main Feature Tags", trừ khi bạn chọn "Enabled" bên dưới "Override Main Tags".

.. warning::
    Nếu bạn muốn truyền các argument "User", bạn có thể truy cập chúng bằng cách sử dụng
    :ref:`get_cmdline_user_args<class_OS_method_get_cmdline_user_args>` then you
    phải thêm hai dấu gạch ngang **và một dấu cách** ở trước, như `-- one two three`.

    Lưu ý rằng các dấu gạch ngang này sẽ áp dụng cho những argument được thêm sau đó trong "Launch Arguments" theo từng instance, điều này có thể gây nhầm lẫn khi kết hợp `Main Run Args` và `Launch Arguments`.

    Nếu bạn đặt `-- one two three` trong "Main Run Args" và `-- four five six` trong "Launch Arguments", thì các command-line argument cuối cùng sẽ là `one two three -- four five six`. Điều này là vì `--` được lặp lại trong "Launch Arguments".


.. _doc_debugger_tools_and_options:

Các công cụ và tùy chọn debug của script editor
-----------------------------------------------

Script editor có bộ công cụ debug riêng để sử dụng với breakpoint và hai tùy chọn. Các công cụ breakpoint cũng có thể được tìm thấy trong tab **Debugger** của debugger.

.. tip::

    Bạn có thể tạo breakpoint bằng cách nhấp vào gutter ở bên trái script editor (bên trái các số dòng). Khi di chuột lên gutter này, bạn sẽ thấy một chấm đỏ trong suốt xuất hiện; chấm này chuyển thành chấm đỏ đậm sau khi breakpoint được đặt bằng cách nhấp chuột. Nhấp lại vào chấm đỏ để xóa breakpoint. Các breakpoint được tạo theo cách này vẫn tồn tại qua các lần khởi động lại editor, ngay cả khi script chưa được lưu lúc thoát editor.

    Bạn cũng có thể sử dụng từ khóa ``breakpoint`` trong GDScript để tạo breakpoint được lưu ngay trong script. Không giống các breakpoint được tạo bằng cách nhấp vào gutter, breakpoint dựa trên từ khóa này vẫn tồn tại trên các máy khác nhau khi sử dụng version control.

.. image:: img/overview_script_editor.webp

Nút **Break** tạo ra một điểm dừng trong script giống như breakpoint. **Continue** tiếp tục game sau khi game tạm dừng tại breakpoint. **Step Over** chuyển đến dòng code tiếp theo, còn **Step Into** đi vào một function nếu có thể. Nếu không, nó sẽ thực hiện giống **Step Over**.

Tùy chọn **Debug with External Editor** cho phép bạn debug game bằng external editor. Bạn có thể đặt shortcut cho tùy chọn này trong **Editor Settings > Shortcuts > Debugger**.

Khi debugger dừng tại một breakpoint, một mũi tên tam giác màu xanh lá sẽ hiển thị trong gutter của script editor. Mũi tên này cho biết dòng code mà debugger đã dừng.

Các thiết lập debug của project
-------------------------------

Trong project settings, có một danh mục **Debug** với các danh mục con dùng để kiểm soát nhiều nội dung khác nhau. Bật **Advanced Settings** để thay đổi các thiết lập này.

Settings
~~~~~~~~

Đây là một số thiết lập chung, chẳng hạn như in FPS hiện tại vào **Output** panel, số lượng function tối đa khi profiling và các thiết lập khác.

File Logging
~~~~~~~~~~~~

Các thiết lập này cho phép bạn ghi output của console và thông báo lỗi vào file.

GDScript
~~~~~~~~

Các thiết lập này cho phép bạn bật hoặc tắt những cảnh báo GDScript cụ thể, chẳng hạn như cảnh báo về biến không được sử dụng. Bạn cũng có thể tắt hoàn toàn các cảnh báo. Xem
:ref:`doc_gdscript_warning_system` for more information.

Shader Language
~~~~~~~~~~~~~~~

Các thiết lập này cho phép bạn bật hoặc tắt những cảnh báo shader cụ thể, chẳng hạn như cảnh báo về biến không được sử dụng. Bạn cũng có thể tắt hoàn toàn các cảnh báo.

Canvas Items
~~~~~~~~~~~~

Các thiết lập này dùng cho việc debug redraw của canvas item.

Shapes
~~~~~~

Shapes là nơi bạn có thể điều chỉnh màu của các shape chỉ xuất hiện cho mục đích debug, chẳng hạn như shape va chạm và shape điều hướng.

Remote trong scene dock
-----------------------

Khi chạy một game trong editor, ở đầu dock **Scene** sẽ xuất hiện hai tùy chọn là **Remote** và **Local**. Khi sử dụng **Remote**, bạn có thể kiểm tra hoặc thay đổi các tham số của node trong project đang chạy.

.. image:: img/overview_remote.webp

.. note:: Some editor settings related to debugging can be found inside
          trong **Editor Settings**, ở các mục **Network > Debug** và **Debugger**.
