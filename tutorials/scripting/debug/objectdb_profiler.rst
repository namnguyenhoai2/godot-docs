.. _doc_objectdb_profiler:

Sử dụng ObjectDB profiler
=========================

Kể từ Godot 4.6, một tab **ObjectDB Profiler** mới đã được thêm vào panel phía dưới của Debugger. Profiler này cho phép bạn chụp snapshot về trạng thái hiện tại của ObjectDB, cơ sở dữ liệu chứa tất cả các class dẫn xuất từ :ref:`class_object` hiện đang được cấp phát trong bộ nhớ. Tính năng này hữu ích để xác định memory leak và tìm hiểu mức sử dụng bộ nhớ của project.

Ngoài ra, công cụ này có thể trực quan hóa sự khác biệt giữa hai snapshot. Bạn có thể dùng tính năng này để xác định những cải thiện hoặc suy giảm về mức sử dụng bộ nhớ sau khi thay đổi project. Giảm mức sử dụng bộ nhớ có thể mang lại hiệu năng tốt hơn, ngay cả trong trường hợp bộ nhớ không phải là bottleneck. Bằng cách giảm mức sử dụng bộ nhớ, bạn có thể thực hiện ít thao tác cấp phát hơn; đây có thể là một thao tác tốn kém, đặc biệt khi được thực hiện với số lượng lớn trong lúc gameplay.

.. seealso::

   Xem :ref:`doc_node_alternatives` để biết thông tin về việc sử dụng các lựa chọn thay thế nhẹ hơn cho node, giúp giảm mức sử dụng bộ nhớ trong project.

.. warning::

    ObjectDB profiler **không** theo dõi mọi phần bộ nhớ được engine hoặc các thư viện bên ngoài sử dụng. Các class native của engine không được expose qua scripting API sẽ không xuất hiện trong snapshot.

    Hãy cân nhắc sử dụng các công cụ memory profiling bên ngoài nếu bạn cần truy cập thông tin này.

Cách sử dụng
------------

Mở tab ObjectDB Profiler trong panel phía dưới :menu:`Debugger`. Bạn sẽ được đưa đến trang tóm tắt, khi chưa có snapshot nào được chụp.

.. figure:: img/objectdb_profiler_summary_no_snapshots.webp
   :align: center
   :alt: ObjectDB profiler summary with no snapshots taken

   ObjectDB profiler summary with no snapshots taken

Chạy project, sau đó đến thời điểm bạn muốn chụp snapshot (ví dụ: sau khi load một level). Nhấp :button:`Take ObjectDB Snapshot` để chụp snapshot tại thời điểm hiện tại. Nếu nút này bị làm mờ, hãy đảm bảo project đang chạy trước.

.. figure:: img/objectdb_profiler_summary_snapshot.webp
   :align: center
   :alt: ObjectDB profiler summary with one snapshot taken

   ObjectDB profiler summary with one snapshot taken

Bạn có thể chụp nhiều snapshot trong một lần chạy project. Ngoài ra, bạn có thể nhấp chuột phải vào snapshot trong danh sách snapshot để đổi tên, hiển thị snapshot trong trình quản lý file hoặc xóa snapshot.

.. tip::

    Bạn nên đổi tên snapshot sau khi chụp để đặt cho chúng những tên mô tả (ví dụ: ``before_optimization``, ``after_optimization``). Bất kể tên snapshot là gì, ngày snapshot được chụp vẫn được lưu trong chính file snapshot.

    Các file snapshot có phần mở rộng ``.odb_snapshot`` và nằm tại ``user://objectdb_snapshots/`` (xem chi tiết :ref:`Data paths <doc_data_paths_accessing_persistent_user_data>`). Bạn có thể an toàn sao chép các file này giữa các thiết bị, vì chúng độc lập với nền tảng.

Xem sự khác biệt giữa các snapshot
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sau khi chụp ít nhất hai snapshot, dropdown :menu:`Diff Against` sẽ khả dụng. Tại đây, bạn có thể chọn một snapshot khác để so sánh với snapshot hiện đang được chọn.

.. figure:: img/objectdb_profiler_summary_diff_against.webp
   :align: center
   :alt: Diff Against dropdown in the bottom-left corner of the ObjectDB profiler

   Diff Against dropdown in the bottom-left corner of the ObjectDB profiler

Sau đó, trang tóm tắt sẽ hiển thị sự khác biệt giữa hai snapshot:

.. figure:: img/objectdb_profiler_summary_snapshot_diff.webp
   :align: center
   :alt: Two snapshots being compared in the Summary tab

   Two snapshots being compared in the Summary tab

Điều này cũng áp dụng cho mọi tab khác trong ObjectDB profiler; các tab đó sẽ hiển thị sự khác biệt giữa hai snapshot trong những cột bổ sung.

Classes
^^^^^^^

Trong tab Classes, bạn có thể xem số instance của mỗi class đã được tạo tại thời điểm snapshot được chụp:

.. figure:: img/objectdb_profiler_classes.webp
   :align: center
   :alt: One snapshots being viewed in the Classes tab

   One snapshots being viewed in the Classes tab

Khi ở diff mode, tab này sẽ hiển thị số lượng instance của class trong snapshot hiện đang được chọn (cột A) và snapshot được dùng để so sánh (cột B). Tab này cũng sẽ hiển thị sự chênh lệch về số lượng instance trong cột Delta.

.. figure:: img/objectdb_profiler_classes_diff.webp
   :align: center
   :alt: Two snapshots being compared in the Classes tab. Here, column A is ``second_session``, column B is ``first_session``

   Two snapshots being compared in the Classes tab. Here, column A is ``second_session``, column B is ``first_session``

Bạn có thể nhấp vào một class trong danh sách bên phải để xem class đó trong inspector.

.. figure:: img/objectdb_profiler_classes_inspector.webp
   :align: center
   :alt: A selected class instance being viewed in the inspector

   A selected class instance being viewed in the inspector

.. tip::

   Bạn cũng có thể xem trước các instance trong inspector ở những tab khác (Nodes, Objects và RefCounted).

Objects
^^^^^^^

Tab Objects tương tự, nhưng khác ở cách trình bày dữ liệu. Tại đây, mọi instance được liệt kê theo thứ tự tuyến tính thay vì được nhóm theo class. Khi chọn một object, bạn sẽ thấy danh sách các object khác mà nó tham chiếu ở bên phải (:menu:`Outbound References`), cũng như danh sách các object đang tham chiếu đến nó (:menu:`Inbound References`).

Điều này cho phép bạn xem các object theo cách "từ trên xuống" (xem một object nhất định tham chiếu đến những object nào) hoặc theo cách "từ dưới lên" (xem những object nào tham chiếu đến một object nhất định).

.. figure:: img/objectdb_profiler_objects_top_down.webp
   :align: center
   :alt: The Objects tab being used to view objects in a "top-down" manner

   The Objects tab being used to view objects in a "top-down" manner

Trong hình trên, việc nhấp vào object ``default_font`` trong danh sách sẽ chuyển chế độ xem sang góc nhìn của object đó. Object này cũng được rất nhiều object khác tham chiếu đến, qua đó chuyển sang góc nhìn "từ dưới lên".

.. figure:: img/objectdb_profiler_objects_bottom_up.webp
   :align: center
   :alt: The Objects tab being used to view objects in a "bottom-up" manner

   The Objects tab being used to view objects in a "bottom-up" manner

Nodes
^^^^^

Tiếp theo, tab Nodes hiển thị scene tree tại thời điểm snapshot được chụp.

.. figure:: img/objectdb_profiler_nodes.webp
   :align: center
   :alt: The Nodes tab being used to view the scene tree

   The Nodes tab being used to view the scene tree

Tab này đặc biệt thú vị trong diff view, vì nó hỗ trợ hiển thị sự khác biệt giữa hai snapshot theo cách trực quan hơn. Khi :button:`Combined Diff` không được chọn, bạn có thể xem các điểm khác biệt cạnh nhau.

.. figure:: img/objectdb_profiler_nodes_diff_separate.webp
   :align: center
   :alt: Separate diff view in the Nodes tab

   Separate diff view in the Nodes tab

Khi :button:`Combined Diff` được chọn, bạn có thể xem các điểm khác biệt được gộp vào một tree duy nhất, với các node được thêm được tô sáng màu xanh lá và các node bị xóa được tô sáng màu đỏ.

.. figure:: img/objectdb_profiler_nodes_diff_combined.webp
   :align: center
   :alt: Combined diff view in the Nodes tab

   Combined diff view in the Nodes tab

Ngoài ra, bạn có thể xem danh sách các node mồ côi (các node không được gắn vào root của scene tree) ở cuối phần hiển thị tree. Bạn có thể xem danh sách này dễ dàng hơn bằng cách thu gọn root node, vì các node này được liệt kê bên ngoài scene tree chính.

.. figure:: img/objectdb_profiler_nodes_orphan.webp
   :align: center
   :alt: Orphan nodes at the end of the nodes tree in the ObjectDB profiler

   Orphan nodes at the end of the nodes tree in the ObjectDB profiler

RefCounted
^^^^^^^^^^

Tab cuối cùng là tab RefCounted. Tab này tương tự tab Objects, nhưng hiển thị trực tiếp số lượng reference của các class dẫn xuất từ :ref:`class_refcounted` trong bảng. Bảng có bốn cột:

- **Native Refs:** Số lượng reference native của engine đến object. - **ObjectDB Refs:** Số lượng reference ObjectDB đến object. - **Total Refs:** Tổng số native reference và ObjectDB reference. - **ObjectDB Cycles:** Số lượng circular reference được phát hiện.

Khi ở diff view, snapshot B luôn được liệt kê *bên trên* snapshot A nếu một instance RefCounted tồn tại trong cả hai snapshot.

Danh sách bên phải hiển thị thông tin chi tiết về instance được chọn, bao gồm danh sách các reference và việc chúng có bị trùng lặp hay không.

.. figure:: img/objectdb_profiler_refcounted.webp
   :align: center
   :alt: The RefCounted tab being used to view RefCounted instances

   The RefCounted tab being used to view RefCounted instances

.. note::

   Tab RefCounted **không** liệt kê các object dẫn xuất trực tiếp từ
   :ref:`class_object`, as these don't use reference counting.
