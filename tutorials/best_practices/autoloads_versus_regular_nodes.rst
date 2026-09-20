.. _doc_autoloads_versus_regular_nodes:

Autoload và node thông thường
=============================

Godot cung cấp một tính năng tự động load các node tại root của project, cho phép bạn truy cập chúng trên toàn cục và có thể đảm nhiệm vai trò của một Singleton:
:ref:`doc_singletons_autoload`. These autoloaded nodes are not freed when you
thay đổi scene từ code bằng :ref:`SceneTree.change_scene_to_file <class_SceneTree_method_change_scene_to_file>`.

Trong hướng dẫn này, bạn sẽ tìm hiểu khi nào nên sử dụng tính năng Autoload và những kỹ thuật có thể dùng để tránh sử dụng nó.

Vấn đề âm thanh bị ngắt
-----------------------

Các engine khác có thể khuyến khích việc tạo các manager class, tức những singleton tổ chức nhiều chức năng vào một object có thể truy cập trên toàn cục. Godot cung cấp nhiều cách để tránh global state nhờ node tree và signal.

Ví dụ, giả sử chúng ta đang xây dựng một platformer và muốn thu thập các coin phát ra sound effect. Có một node dành cho việc đó: :ref:`AudioStreamPlayer <class_AudioStreamPlayer>`. Nhưng nếu chúng ta gọi ``AudioStreamPlayer`` khi nó đang phát âm thanh, âm thanh mới sẽ ngắt âm thanh đầu tiên.

Một giải pháp là viết code cho một sound manager class được autoload trên toàn cục. Class này tạo một pool các node ``AudioStreamPlayer`` và luân phiên sử dụng chúng khi có yêu cầu sound effect mới. Giả sử chúng ta gọi class đó là ``Sound``, bạn có thể sử dụng nó ở bất kỳ đâu trong project bằng cách gọi ``Sound.play("coin_pickup.ogg")``. Cách này giải quyết vấn đề trong ngắn hạn nhưng lại gây ra nhiều vấn đề hơn:

1. **Global state**: một object hiện chịu trách nhiệm về dữ liệu của tất cả object. Nếu class ``Sound`` có lỗi hoặc không có sẵn một AudioStreamPlayer, tất cả node gọi đến nó đều có thể gặp lỗi.

2. **Global access**: giờ đây bất kỳ object nào cũng có thể gọi ``Sound.play(sound_path)`` từ bất kỳ đâu, nên không còn cách dễ dàng để tìm ra nguồn gốc của một bug.

3. **Global resource allocation**: với một pool các node ``AudioStreamPlayer`` được lưu trữ ngay từ đầu, bạn có thể tạo quá ít node và gặp bug, hoặc tạo quá nhiều node và sử dụng nhiều memory hơn mức cần thiết.

.. note::

   Về global access, vấn đề là bất kỳ code nào ở bất kỳ đâu cũng có thể truyền dữ liệu sai vào autoload ``Sound`` trong ví dụ của chúng ta. Do đó, phạm vi cần kiểm tra để sửa bug bao trùm toàn bộ project.

   Khi bạn giữ code bên trong một scene, chỉ một hoặc hai script có thể liên quan đến phần âm thanh.

Ngược lại, nếu mỗi scene tự giữ số lượng node ``AudioStreamPlayer`` cần thiết bên trong nó, tất cả những vấn đề này sẽ biến mất:

1. Mỗi scene quản lý thông tin state của riêng mình. Nếu dữ liệu có vấn đề, nó chỉ gây ra sự cố trong scene đó.

2. Mỗi scene chỉ truy cập các node của riêng mình. Khi đó, nếu có bug, bạn sẽ dễ dàng tìm ra node gây lỗi.

3. Mỗi scene phân bổ đúng lượng resource mà nó cần.

Quản lý chức năng hoặc dữ liệu dùng chung
-----------------------------------------

Một lý do khác để sử dụng Autoload là bạn muốn tái sử dụng cùng một method hoặc dữ liệu trong nhiều scene.

Đối với function, bạn có thể tạo một kiểu ``Node`` mới cung cấp tính năng đó cho một scene riêng lẻ bằng keyword :ref:`class_name <doc_gdscript_basics_class_name>` trong GDScript.

Đối với dữ liệu, bạn có thể:

1. Tạo một kiểu :ref:`Resource <class_Resource>` mới để chia sẻ dữ liệu.

2. Lưu dữ liệu trong một object mà mỗi node đều có thể truy cập, chẳng hạn sử dụng property ``owner`` để truy cập root node của scene.

Khi nào nên sử dụng Autoload
----------------------------

GDScript hỗ trợ tạo các function ``static`` bằng ``static func``. Khi kết hợp với ``class_name``, tính năng này cho phép tạo các thư viện helper function mà không cần tạo một instance để gọi chúng. Hạn chế của static function là chúng không thể tham chiếu đến member variable, non-static function hoặc ``self``.

Kể từ Godot 4.1, GDScript cũng hỗ trợ các variable ``static`` bằng ``static var``. Điều này có nghĩa là giờ đây bạn có thể chia sẻ variable giữa các instance của một class mà không cần tạo một autoload riêng.

Tuy vậy, các node được autoload vẫn có thể đơn giản hóa code của bạn đối với những system có phạm vi hoạt động rộng. Nếu autoload tự quản lý thông tin của nó và không can thiệp vào dữ liệu của các object khác, thì đây là một cách tuyệt vời để tạo các system xử lý những task có phạm vi rộng. Ví dụ: system quest hoặc dialogue.

.. note::

   Một autoload *không nhất thiết* là một singleton. Không có gì ngăn bạn tạo các bản sao của một node được autoload. Autoload chỉ là một công cụ giúp một node tự động được load như một child của root trong scene tree, bất kể cấu trúc node của game hoặc scene mà bạn chạy, chẳng hạn bằng cách nhấn phím :kbd:`F6`.

   Do đó, bạn có thể lấy node được autoload, chẳng hạn một autoload có tên ``Sound``, bằng cách gọi ``get_node("/root/Sound")``.
