.. _doc_overview_of_debugging_tools:

Tổng quan về các công cụ gỡ lỗi
===============================

Hướng dẫn này sẽ cung cấp cho bạn tổng quan về các công cụ gỡ lỗi hiện có trong engine.

Godot đi kèm trình gỡ lỗi và các profiler mạnh mẽ để tìm và khắc phục lỗi, kiểm tra game trong runtime, theo dõi các chỉ số thiết yếu và đo hiệu năng. Godot cũng cung cấp các tùy chọn để trực quan hóa các hộp va chạm và polygon điều hướng trong game đang chạy.

Cuối cùng, bạn có các tùy chọn để gỡ lỗi game đang chạy trên thiết bị từ xa và tải lại các thay đổi đối với scene hoặc code trong khi game đang chạy.

Output Panel
------------

Output panel cho phép bạn xem văn bản được project in ra, cũng như văn bản do editor in ra (ví dụ: từ các script ``@tool``). Bạn có thể tìm thông tin về nội dung này trong :ref:`doc_output_panel`.

Debugger Panel
--------------

Nhiều công cụ gỡ lỗi của Godot nằm trong Debugger panel; bạn có thể tìm thông tin về panel này trong :ref:`doc_debugger_panel`.

Các tùy chọn trong menu Debug
-----------------------------

Có một số tùy chọn gỡ lỗi phổ biến mà bạn có thể bật hoặc tắt khi chạy game trong editor, giúp bạn gỡ lỗi game.

Bạn có thể tìm các tùy chọn này trong menu editor **Debug**.

.. image:: img/overview_debug.webp

Mô tả các tùy chọn như sau:

Deploy with Remote Debug
~~~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, việc sử dụng one-click deploy sẽ khiến executable cố gắng kết nối đến IP của máy tính này để có thể gỡ lỗi project đang chạy. Tùy chọn này được dùng cho việc gỡ lỗi từ xa (thường là với thiết bị di động). Bạn không cần bật tùy chọn này để sử dụng trình gỡ lỗi GDScript cục bộ.

Small Deploy with Network Filesystem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này tăng tốc việc kiểm thử các game có dung lượng lớn trên thiết bị từ xa.

Khi **Small Deploy with Network Filesystem** được bật, thay vì export toàn bộ game, việc deploy game sẽ tạo một executable tối giản. Sau đó, editor cung cấp các file của project qua network.

Ngoài ra, trên Android, game được deploy bằng cáp USB để tăng tốc quá trình deploy.

Visible Collision Shapes
~~~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, các collision shape và node raycast (cho 2D và 3D) sẽ hiển thị trong project đang chạy.

Visible Paths
~~~~~~~~~~~~~

Khi bật tùy chọn này, các curve resource được node path sử dụng sẽ hiển thị trong project đang chạy.

Visible Navigation
~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, các navigation mesh và polygon sẽ hiển thị trong project đang chạy.

Visible Avoidance
~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, shape, bán kính và vận tốc của các đối tượng avoidance sẽ hiển thị trong project đang chạy.

Debug CanvasItem Redraws
~~~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, các yêu cầu redraw của đối tượng 2D sẽ hiển thị (dưới dạng một lần nhấp nháy ngắn) trong project đang chạy. Tùy chọn này hữu ích để khắc phục sự cố trong low processor mode.

Synchronize Scene Changes
~~~~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, mọi thay đổi đối với scene trong editor sẽ được sao chép vào project đang chạy. Khi sử dụng từ xa trên thiết bị, tùy chọn này hiệu quả hơn khi bật network filesystem.

Synchronize Script Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, mọi thay đổi đối với script trong editor sẽ được tải lại vào project đang chạy. Khi sử dụng từ xa trên thiết bị, tùy chọn này hiệu quả hơn khi dùng network filesystem.

Keep Debug Server Open
~~~~~~~~~~~~~~~~~~~~~~

Khi bật tùy chọn này, debug server của editor sẽ tiếp tục mở và lắng nghe các session mới được khởi chạy bên ngoài chính editor.

Customize Run Instances...
~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này mở một hộp thoại cho phép bạn yêu cầu Godot chạy đồng thời nhiều instance của game và chỉ định các đối số dòng lệnh cho từng instance. Tùy chọn này đặc biệt hữu ích khi xây dựng và gỡ lỗi game multiplayer.

.. image:: img/customize_run_instances.webp

Enable Multiple Instances
^^^^^^^^^^^^^^^^^^^^^^^^^

Khi bật tùy chọn này, editor sẽ chạy đồng thời nhiều instance của project khi bạn chọn Run Project.

Bên dưới checkbox này là một bộ chọn để chọn số lượng instance cần chạy.

Việc đánh dấu checkbox và đặt giá trị này thành 1 cũng giống như không đánh dấu checkbox này.

Main Run Args
^^^^^^^^^^^^^

Đây là các đối số sẽ được truyền cho **mọi** instance của project khi bạn chọn Run Project, trừ khi bạn chọn "Enabled" bên dưới "Override Main Run Args" cho một instance cụ thể.

Lưu ý rằng các đối số này được phân tách bằng khoảng trắng.

.. tip::

    Bạn có thể truy cập các đối số này trong script bằng cách sử dụng
    :ref:`get_cmdline_args<class_OS_method_get_cmdline_args>`.

.. warning::

    Ngay cả khi bỏ chọn "Enable Multiple Instances", các đối số này vẫn sẽ được truyền khi bạn chọn Run Project.

Main Feature Tags
^^^^^^^^^^^^^^^^^

Đây là các feature tag sẽ được truyền cho **mọi** instance của project khi bạn chọn Run Project, trừ khi bạn chọn "Enabled" bên dưới "Override Main Tags" cho một instance cụ thể.

Override Main Run Args
^^^^^^^^^^^^^^^^^^^^^^

Khi bật tùy chọn này, các đối số trong trường "Main Run Args" sẽ **không được truyền** cho instance cụ thể này của project khi bạn chọn Run Project.

Launch Arguments
^^^^^^^^^^^^^^^^

Đây là các đối số sẽ được truyền cho instance cụ thể này của project khi bạn chọn Run Project. Chúng sẽ được **kết hợp với** "Main Run Args", trừ khi bạn chọn "Enabled" bên dưới "Override Main Run Args".

Override Main Tags
^^^^^^^^^^^^^^^^^^

Khi bật tùy chọn này, các tag trong trường "Main Feature Tags" sẽ **không được truyền** cho instance cụ thể này của project khi bạn chọn Run Project.

Feature Tags
^^^^^^^^^^^^

Đây là các feature tag sẽ được truyền cho instance cụ thể này của project khi bạn chọn Run Project. Chúng sẽ được **kết hợp với** "Main Feature Tags", trừ khi bạn chọn "Enabled" bên dưới "Override Main Tags".

.. warning::
    Nếu bạn muốn truyền các đối số "User", có thể được truy cập bằng
    :ref:`get_cmdline_user_args<class_OS_method_get_cmdline_user_args>` thì bạn phải thêm tiền tố gồm hai dấu gạch ngang **và một dấu cách** như `-- one two three`.

    Lưu ý rằng các dấu gạch ngang này sẽ áp dụng cho những đối số được thêm sau đó trong "Launch Arguments" theo từng instance, điều này có thể gây nhầm lẫn khi kết hợp `Main Run Args` và `Launch Arguments`.

    Nếu bạn đặt `-- one two three` trong "Main Run Args" và `-- four five six` trong "Launch Arguments" thì các đối số dòng lệnh cuối cùng sẽ là `one two three -- four five six`. Điều này là do `--` được lặp lại trong "Launch Arguments".


.. _doc_debugger_tools_and_options:

Công cụ và tùy chọn debug của trình chỉnh sửa script
----------------------------------------------------

Trình chỉnh sửa script có bộ công cụ debug riêng để sử dụng với breakpoint và hai tùy chọn. Các công cụ breakpoint cũng có trong tab **Debugger** của debugger.

.. tip::

    Bạn có thể tạo breakpoint bằng cách nhấp vào lề bên trái của trình chỉnh sửa script (bên trái số dòng). Khi di chuột lên lề này, bạn sẽ thấy một chấm đỏ trong suốt xuất hiện; chấm này sẽ chuyển thành chấm đỏ đậm sau khi bạn nhấp để đặt breakpoint. Nhấp lại vào chấm đỏ để xóa breakpoint. Các breakpoint được tạo theo cách này vẫn tồn tại qua những lần khởi động lại trình chỉnh sửa, ngay cả khi script chưa được lưu khi thoát trình chỉnh sửa.

    Bạn cũng có thể sử dụng từ khóa ``breakpoint`` trong GDScript để tạo một breakpoint được lưu ngay trong script. Không giống các breakpoint được tạo bằng cách nhấp vào lề, breakpoint dựa trên từ khóa này vẫn tồn tại trên các máy khác nhau khi sử dụng version control.

.. image:: img/overview_script_editor.webp

Nút **Break** khiến script dừng lại giống như một breakpoint. **Continue** tiếp tục chạy game sau khi tạm dừng tại breakpoint. **Step Over** chuyển đến dòng code tiếp theo, còn **Step Into** đi vào một hàm nếu có thể. Nếu không, nó sẽ thực hiện giống như **Step Over**.

Tùy chọn **Debug with External Editor** cho phép bạn debug game bằng một trình chỉnh sửa bên ngoài. Bạn có thể đặt phím tắt cho tùy chọn này trong **Editor Settings > Shortcuts > Debugger**.

Khi debugger dừng tại breakpoint, một mũi tên hình tam giác màu xanh lá sẽ hiển thị ở lề của trình chỉnh sửa script. Mũi tên này cho biết dòng code mà debugger đã dừng lại.

Cài đặt project để debug
------------------------

Trong phần cài đặt project, có một danh mục **Debug** với các danh mục con dùng để kiểm soát nhiều thành phần khác nhau. Bật **Advanced Settings** để thay đổi các cài đặt này.

Cài đặt
~~~~~~~

Đây là một số cài đặt chung, chẳng hạn như in FPS hiện tại vào panel **Output**, số lượng hàm tối đa khi profiling và các cài đặt khác.

Ghi log vào file
~~~~~~~~~~~~~~~~

Các cài đặt này cho phép bạn ghi đầu ra của console và các thông báo lỗi vào file.

GDScript
~~~~~~~~

Các cài đặt này cho phép bạn bật hoặc tắt những cảnh báo GDScript cụ thể, chẳng hạn như cảnh báo về biến không được sử dụng. Bạn cũng có thể tắt hoàn toàn các cảnh báo. Xem
:ref:`doc_gdscript_warning_system` để biết thêm thông tin.

Ngôn ngữ shader
~~~~~~~~~~~~~~~

Các cài đặt này cho phép bạn bật hoặc tắt những cảnh báo shader cụ thể, chẳng hạn như cảnh báo về biến không được sử dụng. Bạn cũng có thể tắt hoàn toàn các cảnh báo.

Canvas Items
~~~~~~~~~~~~

Các cài đặt này dùng để debug việc vẽ lại canvas item.

Hình dạng
~~~~~~~~~

Hình dạng là nơi bạn có thể điều chỉnh màu của những hình dạng chỉ xuất hiện cho mục đích debug, chẳng hạn như hình dạng va chạm và điều hướng.

Remote trong dock scene
-----------------------

Khi chạy game trong trình chỉnh sửa, hai tùy chọn sẽ xuất hiện ở đầu dock **Scene**: **Remote** và **Local**. Khi sử dụng **Remote**, bạn có thể kiểm tra hoặc thay đổi các tham số của node trong project đang chạy.

.. image:: img/overview_remote.webp

.. note:: Một số cài đặt trình chỉnh sửa liên quan đến việc debug nằm trong **Editor Settings**, tại các phần **Network > Debug** và **Debugger**.
