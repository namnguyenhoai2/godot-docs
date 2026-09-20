.. _doc_godot_architecture_diagram:

Tổng quan về kiến trúc của Godot
================================

Sơ đồ sau đây mô tả những khía cạnh quan trọng nhất trong kiến trúc của Godot. Sơ đồ không được thiết kế để bao quát toàn diện mà chỉ nhằm cung cấp cái nhìn tổng quan ở cấp độ cao về các thành phần chính và mối quan hệ giữa chúng.

.. figure:: img/godot-architecture-diagram.webp
   :alt: Diagram of Godot's Architecture; divided into three layers (from top to bottom: Scene layer, Server layer, and Drivers & Platform interface layer), with Core and Main separated on the right side since they interact with all layers.

   Credit: `Hendrik Brucker <https://github.com/Geometror/godot-architecture-diagram>`__

Lớp Scene
~~~~~~~~~

Lớp Scene là cấp cao nhất trong kiến trúc của Godot, cung cấp hệ thống scene, là cách chính để xây dựng và cấu trúc các ứng dụng hoặc trò chơi của bạn. Xem :ref:`class_SceneTree` / :ref:`doc_scene_tree` và :ref:`class_Node` để biết thêm thông tin.

Mã nguồn tương ứng: `/scene/* <https://github.com/godotengine/godot/tree/master/scene>`__

Lớp Server
~~~~~~~~~~

Các thành phần Server triển khai hầu hết các hệ thống con của Godot (kết xuất, âm thanh, vật lý, v.v.). Chúng là các đối tượng singleton được khởi tạo khi engine khởi động.

`Tại sao Godot sử dụng server và RID? <https://godotengine.org/article/why-does-godot-use-servers-and-rids>`__

Mã nguồn tương ứng: `/servers/* <https://github.com/godotengine/godot/tree/master/servers>`__

Trình điều khiển / Giao diện nền tảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lớp này trừu tượng hóa các chi tiết cấp thấp đặc thù của nền tảng, bao gồm các trình điều khiển cho API đồ họa, backend âm thanh và giao diện hệ điều hành (tất cả các triển khai :ref:`class_OS` và :ref:`class_DisplayServer` đặc thù của nền tảng).

Mã nguồn tương ứng: `/drivers/* <https://github.com/godotengine/godot/tree/master/drivers>`__ và `/platform/* <https://github.com/godotengine/godot/tree/master/platform>`__

Core
~~~~

Core của Engine chứa các chức năng thiết yếu và cấu trúc dữ liệu được sử dụng xuyên suốt engine, chẳng hạn như :ref:`class_Object` và :ref:`class_ClassDB`, :ref:`memory management <doc_core_types>`, :ref:`containers <doc_core_types>`, I/O tệp, :ref:`Variant <doc_variant_class>` và :ref:`other utilities <doc_common_engine_methods_and_macros>`.

Mã nguồn tương ứng: `/core/* <https://github.com/godotengine/godot/tree/master/core>`__

Main
~~~~

Thành phần Main chịu trách nhiệm khởi tạo và quản lý vòng đời của engine, bao gồm khởi động, tắt máy và vòng lặp chính. Xem :ref:`class_MainLoop` để biết thêm chi tiết.

Mã nguồn tương ứng: `/main/* <https://github.com/godotengine/godot/tree/master/main>`__

