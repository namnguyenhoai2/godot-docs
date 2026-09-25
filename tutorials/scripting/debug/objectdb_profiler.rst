.. _doc_objectdb_profiler:

Sử dụng profiler ObjectDB
=========================

Kể từ Godot 4.6, một tab **ObjectDB Profiler** mới xuất hiện trong panel phía dưới Debugger. Profiler này cho phép bạn chụp nhanh trạng thái hiện tại của ObjectDB, cơ sở dữ liệu chứa tất cả các lớp dẫn xuất từ :ref:`class_object` hiện đang được cấp phát trong bộ nhớ. Điều này hữu ích để xác định memory leak và hiểu mức sử dụng bộ nhớ của dự án.

Ngoài ra, công cụ này có thể trực quan hóa sự khác biệt giữa hai ảnh chụp nhanh. Bạn có thể dùng tính năng này để xác định những cải thiện hoặc suy giảm về mức sử dụng bộ nhớ sau khi thay đổi dự án. Giảm mức sử dụng bộ nhớ có thể cải thiện hiệu suất, ngay cả trong trường hợp bộ nhớ không phải là nút thắt cổ chai. Bằng cách giảm mức sử dụng bộ nhớ, bạn có thể thực hiện ít thao tác cấp phát hơn; đây có thể là một thao tác tốn kém, đặc biệt nếu được thực hiện với số lượng lớn trong quá trình chơi.

.. seealso::

   Xem :ref:`doc_node_alternatives` để biết thông tin về việc sử dụng các lựa chọn thay thế nhẹ hơn cho node, giúp giảm mức sử dụng bộ nhớ trong dự án.

.. warning::

    Profiler ObjectDB **không** theo dõi mọi phần bộ nhớ được engine hoặc các thư viện bên ngoài sử dụng. Các lớp native của engine không được cung cấp thông qua scripting API sẽ không xuất hiện trong ảnh chụp nhanh.

    Hãy cân nhắc sử dụng các công cụ memory profiling bên ngoài nếu bạn cần truy cập thông tin này.

Cách sử dụng
------------

Mở tab ObjectDB Profiler trong panel phía dưới :menu:`Debugger`. Bạn sẽ được đưa đến trang tóm tắt khi chưa có ảnh chụp nhanh nào được tạo.

.. figure:: img/objectdb_profiler_summary_no_snapshots.webp
   :align: center
   :alt: Bản tóm tắt profiler ObjectDB khi chưa có ảnh chụp nhanh nào được tạo

   Bản tóm tắt profiler ObjectDB khi chưa có ảnh chụp nhanh nào được tạo

Chạy dự án, sau đó đến thời điểm bạn muốn chụp nhanh (ví dụ: sau khi tải một level). Nhấp :button:`Take ObjectDB Snapshot` để chụp nhanh tại thời điểm hiện tại. Nếu nút hiển thị màu xám, trước tiên hãy đảm bảo dự án đang chạy.

.. figure:: img/objectdb_profiler_summary_snapshot.webp
   :align: center
   :alt: Bản tóm tắt profiler ObjectDB với một ảnh chụp nhanh đã được tạo

   Bản tóm tắt profiler ObjectDB với một ảnh chụp nhanh đã được tạo

Bạn có thể chụp nhiều ảnh trong một lần chạy dự án. Ngoài ra, bạn có thể nhấp chuột phải vào một ảnh chụp nhanh trong danh sách ảnh chụp để đổi tên, hiển thị ảnh trong trình quản lý tệp hoặc xóa ảnh.

.. tip::

    Bạn nên đổi tên ảnh chụp nhanh sau khi tạo để đặt cho chúng những tên mô tả (ví dụ: ``before_optimization``, ``after_optimization``). Bất kể tên là gì, ngày chụp vẫn được lưu trong chính tệp ảnh chụp nhanh.

    Các tệp ảnh chụp nhanh có phần mở rộng ``.odb_snapshot`` và nằm trong ``user://objectdb_snapshots/`` (xem :ref:`Data paths <doc_data_paths_accessing_persistent_user_data>` để biết chi tiết). Bạn có thể an toàn sao chép chúng giữa các thiết bị vì chúng độc lập với nền tảng.

Xem sự khác biệt giữa các ảnh chụp nhanh
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sau khi chụp ít nhất hai ảnh, menu thả xuống :menu:`Diff Against` sẽ khả dụng. Tại đây, bạn có thể chọn một ảnh chụp khác để so sánh với ảnh chụp hiện được chọn.

.. figure:: img/objectdb_profiler_summary_diff_against.webp
   :align: center
   :alt: Menu thả xuống Diff Against ở góc dưới bên trái của profiler ObjectDB

   Menu thả xuống Diff Against ở góc dưới bên trái của profiler ObjectDB

Sau đó, trang tóm tắt sẽ hiển thị sự khác biệt giữa hai ảnh chụp:

.. figure:: img/objectdb_profiler_summary_snapshot_diff.webp
   :align: center
   :alt: Hai ảnh chụp đang được so sánh trong tab Summary

   Hai ảnh chụp đang được so sánh trong tab Summary

Điều này cũng áp dụng cho mọi tab khác trong profiler ObjectDB, các tab này sẽ hiển thị sự khác biệt giữa hai ảnh chụp trong những cột bổ sung.

Classes
^^^^^^^

Trong tab Classes, bạn có thể xem số lượng instance của mỗi class đã được tạo tại thời điểm chụp ảnh:

.. figure:: img/objectdb_profiler_classes.webp
   :align: center
   :alt: Một ảnh chụp đang được xem trong tab Classes

   Một ảnh chụp đang được xem trong tab Classes

Khi ở chế độ diff, tab sẽ hiển thị số lượng instance của class cho ảnh chụp hiện được chọn (cột A) và ảnh chụp đang được so sánh (cột B). Tab cũng sẽ hiển thị chênh lệch số lượng instance trong cột Delta.

.. figure:: img/objectdb_profiler_classes_diff.webp
   :align: center
   :alt: Hai ảnh chụp đang được so sánh trong tab Classes. Tại đây, cột A là ``second_session``, cột B là ``first_session``

   Hai ảnh chụp đang được so sánh trong tab Classes. Tại đây, cột A là ``second_session``, cột B là ``first_session``

Bạn có thể nhấp vào một class trong danh sách bên phải để xem class đó trong inspector.

.. figure:: img/objectdb_profiler_classes_inspector.webp
   :align: center
   :alt: Một instance của class được chọn đang được xem trong inspector

   Một instance của class được chọn đang được xem trong inspector

.. tip::

   Bạn cũng có thể xem trước các instance trong inspector ở những tab khác (Nodes, Objects và RefCounted).

Objects
^^^^^^^

Tab Objects tương tự, nhưng khác ở cách trình bày dữ liệu. Tại đây, mỗi instance được liệt kê theo thứ tự tuyến tính thay vì được nhóm theo class. Khi chọn một object, bạn sẽ thấy danh sách các object khác mà nó tham chiếu ở bên phải (:menu:`Outbound References`), cũng như danh sách các object đang tham chiếu đến nó (:menu:`Inbound References`).

Điều này cho phép bạn xem các object theo cách "từ trên xuống" (xem một object nhất định tham chiếu đến những object nào) hoặc theo cách "từ dưới lên" (xem những object nào tham chiếu đến một object nhất định).

.. figure:: img/objectdb_profiler_objects_top_down.webp
   :align: center
   :alt: Tab Objects đang được sử dụng để xem các object theo cách "từ trên xuống"

   Tab Objects đang được sử dụng để xem các object theo cách "từ trên xuống"

Trong hình ảnh trên, việc nhấp vào object ``default_font`` trong danh sách sẽ chuyển chế độ xem sang góc nhìn của object đó. Object này cũng đang được nhiều object khác tham chiếu, qua đó thực sự chuyển sang góc nhìn "từ dưới lên".

.. figure:: img/objectdb_profiler_objects_bottom_up.webp
   :align: center
   :alt: Tab Objects đang được sử dụng để xem các object theo cách "từ dưới lên"

   Tab Objects đang được sử dụng để xem các object theo cách "từ dưới lên"

Nodes
^^^^^

Tiếp theo, tab Nodes hiển thị scene tree tại thời điểm chụp ảnh.

.. figure:: img/objectdb_profiler_nodes.webp
   :align: center
   :alt: Tab Nodes đang được sử dụng để xem scene tree

   Tab Nodes đang được sử dụng để xem scene tree

Tab này đặc biệt hữu ích trong chế độ xem diff vì hỗ trợ hiển thị sự khác biệt giữa hai ảnh chụp theo cách trực quan hơn. Khi :button:`Combined Diff` không được chọn, bạn có thể xem các điểm khác biệt cạnh nhau.

.. figure:: img/objectdb_profiler_nodes_diff_separate.webp
   :align: center
   :alt: Chế độ xem diff riêng biệt trong tab Nodes

   Chế độ xem diff riêng biệt trong tab Nodes

Khi :button:`Combined Diff` được chọn, bạn có thể xem các điểm khác biệt được hợp nhất vào một tree duy nhất, với các node được thêm được tô màu xanh lá và các node bị xóa được tô màu đỏ.

.. figure:: img/objectdb_profiler_nodes_diff_combined.webp
   :align: center
   :alt: Chế độ xem diff kết hợp trong tab Nodes

   Chế độ xem diff kết hợp trong tab Nodes

Ngoài ra, bạn có thể xem danh sách các nút mồ côi (các nút không được gắn vào nút gốc của cây cảnh) ở cuối chế độ xem cây. Bạn có thể xem danh sách này dễ dàng hơn bằng cách thu gọn nút gốc, vì các nút này được liệt kê bên ngoài cây cảnh chính.

.. figure:: img/objectdb_profiler_nodes_orphan.webp
   :align: center
   :alt: Các nút mồ côi ở cuối cây nút trong trình phân tích ObjectDB

   Các nút mồ côi ở cuối cây nút trong trình phân tích ObjectDB

RefCounted
^^^^^^^^^^

Tab cuối cùng là tab RefCounted. Tab này tương tự tab Objects, nhưng hiển thị trực tiếp số lượng tham chiếu của các lớp kế thừa từ :ref:`class_refcounted` trong bảng. Bảng có bốn cột:

- **Native Refs:** Số lượng tham chiếu native của engine đến đối tượng.
- **ObjectDB Refs:** Số lượng tham chiếu ObjectDB đến đối tượng.
- **Total Refs:** Tổng số tham chiếu native và tham chiếu ObjectDB.
- **ObjectDB Cycles:** Số lượng tham chiếu vòng được phát hiện.

Khi ở chế độ xem diff, snapshot B luôn được liệt kê *phía trên* snapshot A nếu một thực thể RefCounted tồn tại trong cả hai snapshot.

Danh sách ở bên phải hiển thị thông tin chi tiết về thực thể đã chọn, bao gồm danh sách các tham chiếu và việc chúng có bị trùng lặp hay không.

.. figure:: img/objectdb_profiler_refcounted.webp
   :align: center
   :alt: Tab RefCounted được sử dụng để xem các thực thể RefCounted

   Tab RefCounted được sử dụng để xem các thực thể RefCounted

.. note::

   Tab RefCounted **không** liệt kê các đối tượng kế thừa trực tiếp từ
   :ref:`class_object`, vì các đối tượng này không sử dụng cơ chế đếm tham chiếu.
