.. _doc_autoloads_versus_regular_nodes:

Autoload và node thông thường
=============================

Godot cung cấp một tính năng tự động tải các node vào gốc của project, cho phép bạn truy cập chúng trên toàn cục và có thể đảm nhiệm vai trò của một Singleton:
:ref:`doc_singletons_autoload`. Các node được autoload này không bị giải phóng khi bạn thay đổi scene từ code bằng :ref:`SceneTree.change_scene_to_file <class_SceneTree_method_change_scene_to_file>`.

Trong hướng dẫn này, bạn sẽ tìm hiểu khi nào nên sử dụng tính năng Autoload và các kỹ thuật có thể dùng để tránh sử dụng nó.

Vấn đề âm thanh bị ngắt
-----------------------

Các engine khác có thể khuyến khích việc tạo các lớp manager, tức các singleton tổ chức nhiều chức năng vào một object có thể truy cập trên toàn cục. Godot cung cấp nhiều cách để tránh global state nhờ node tree và signal.

Ví dụ, giả sử chúng ta đang xây dựng một game platformer và muốn thu thập các đồng xu có phát sound effect. Có một node dành cho việc đó: :ref:`AudioStreamPlayer <class_AudioStreamPlayer>`. Nhưng nếu chúng ta gọi ``AudioStreamPlayer`` khi nó đang phát âm thanh, âm thanh mới sẽ ngắt âm thanh đầu tiên.

Một giải pháp là viết một lớp sound manager global, được autoload. Lớp này tạo một pool các node ``AudioStreamPlayer`` và lần lượt sử dụng chúng khi có từng yêu cầu sound effect mới. Giả sử chúng ta gọi lớp đó là ``Sound``, bạn có thể sử dụng nó từ bất kỳ đâu trong project bằng cách gọi ``Sound.play("coin_pickup.ogg")``. Cách này giải quyết vấn đề trong ngắn hạn nhưng lại gây ra nhiều vấn đề hơn:

1. **Global state**: một object hiện chịu trách nhiệm về dữ liệu của tất cả object. Nếu lớp ``Sound`` có lỗi hoặc không có AudioStreamPlayer khả dụng, tất cả node gọi nó đều có thể bị hỏng.

2. **Global access**: giờ đây bất kỳ object nào cũng có thể gọi ``Sound.play(sound_path)`` từ bất kỳ đâu, nên không còn cách dễ dàng để tìm ra nguồn gốc của một bug.

3. **Global resource allocation**: với một pool các node ``AudioStreamPlayer`` được lưu trữ ngay từ đầu, bạn có thể tạo quá ít node và gặp bug, hoặc quá nhiều node và sử dụng nhiều memory hơn mức cần thiết.

.. note::

   Về global access, vấn đề là bất kỳ code nào ở bất kỳ đâu cũng có thể truyền dữ liệu sai cho autoload ``Sound`` trong ví dụ của chúng ta. Do đó, phạm vi cần kiểm tra để sửa bug bao trùm toàn bộ project.

   Khi bạn giữ code bên trong một scene, có thể chỉ cần một hoặc hai script liên quan đến âm thanh.

Ngược lại, nếu mỗi scene tự chứa số node ``AudioStreamPlayer`` cần thiết, tất cả những vấn đề này sẽ biến mất:

1. Mỗi scene quản lý thông tin state của riêng mình. Nếu có vấn đề với dữ liệu, vấn đề đó sẽ chỉ gây lỗi trong scene đó.

2. Mỗi scene chỉ truy cập các node của chính nó. Khi đó, nếu có bug, bạn sẽ dễ dàng tìm ra node nào gây lỗi.

3. Mỗi scene phân bổ chính xác lượng resource mà nó cần.

Quản lý chức năng hoặc dữ liệu dùng chung
-----------------------------------------

Một lý do khác để sử dụng Autoload là bạn muốn tái sử dụng cùng một method hoặc dữ liệu trong nhiều scene.

Đối với các function, bạn có thể tạo một kiểu ``Node`` mới cung cấp tính năng đó cho một scene riêng lẻ bằng keyword :ref:`class_name <doc_gdscript_basics_class_name>` trong GDScript.

Đối với dữ liệu, bạn có thể:

1. Tạo một kiểu :ref:`Resource <class_Resource>` mới để chia sẻ dữ liệu.

2. Lưu dữ liệu trong một object mà mỗi node đều có quyền truy cập, chẳng hạn bằng cách sử dụng property ``owner`` để truy cập node gốc của scene.

Khi nào nên sử dụng Autoload
----------------------------

GDScript hỗ trợ việc tạo các function ``static`` bằng ``static func``. Khi kết hợp với ``class_name``, tính năng này cho phép tạo các thư viện helper function mà không cần tạo một instance để gọi chúng. Hạn chế của function static là chúng không thể tham chiếu đến member variable, function non-static hoặc ``self``.

Kể từ Godot 4.1, GDScript cũng hỗ trợ các variable ``static`` bằng ``static var``. Điều này có nghĩa là giờ đây bạn có thể chia sẻ variable giữa các instance của một class mà không cần tạo một autoload riêng.

Tuy vậy, các node được autoload có thể đơn giản hóa code của bạn cho những hệ thống có phạm vi hoạt động rộng. Nếu autoload tự quản lý thông tin của nó và không can thiệp vào dữ liệu của các object khác, thì đây là một cách tuyệt vời để tạo các hệ thống xử lý những tác vụ có phạm vi rộng. Ví dụ: hệ thống nhiệm vụ hoặc hệ thống hội thoại.

.. note::

   Một autoload *không* nhất thiết là một singleton. Không có gì ngăn cản bạn tạo các bản sao của node được autoload. Autoload chỉ là một công cụ giúp node tự động được tải dưới dạng node con của gốc scene tree, bất kể cấu trúc node của game hoặc scene nào đang chạy, chẳng hạn bằng cách nhấn phím :kbd:`F6`.

   Do đó, bạn có thể lấy node được autoload, chẳng hạn một autoload có tên ``Sound``, bằng cách gọi ``get_node("/root/Sound")``.
