.. _doc_godot_architecture_diagram:

Tổng quan về kiến trúc của Godot
================================

Sơ đồ sau đây mô tả những khía cạnh quan trọng nhất trong kiến trúc của Godot. Sơ đồ không nhằm mục đích bao quát mọi chi tiết, mà chỉ cung cấp cái nhìn tổng quan cấp cao về các thành phần chính và mối quan hệ giữa chúng.

.. figure:: img/godot-architecture-diagram.webp
   :alt: Sơ đồ kiến trúc của Godot; được chia thành ba lớp (từ trên xuống dưới: lớp Scene, lớp Server và lớp Drivers & Platform interface), trong đó Core và Main được tách riêng ở bên phải vì chúng tương tác với tất cả các lớp.

   Được đóng góp bởi: `Hendrik Brucker <https://github.com/Geometror/godot-architecture-diagram>`__

Lớp Scene
~~~~~~~~~

Lớp Scene là cấp cao nhất trong kiến trúc của Godot, cung cấp hệ thống scene, đây là cách chính để xây dựng và tổ chức ứng dụng hoặc trò chơi của bạn. Xem :ref:`class_SceneTree` / :ref:`doc_scene_tree` và :ref:`class_Node` để biết thêm thông tin.

Mã nguồn tương ứng: `/scene/* <https://github.com/godotengine/godot/tree/master/scene>`__

Lớp Server
~~~~~~~~~~

Các thành phần Server triển khai hầu hết các subsystem của Godot (rendering, audio, physics, v.v.). Đây là các singleton object được khởi tạo khi engine khởi động.

`Tại sao Godot sử dụng server và RID? <https://godotengine.org/article/why-does-godot-use-servers-and-rids>`__

Mã nguồn tương ứng: `/servers/* <https://github.com/godotengine/godot/tree/master/servers>`__

Drivers / Platform Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lớp này trừu tượng hóa các chi tiết cấp thấp đặc thù cho platform, bao gồm các driver cho graphics API, audio backend và interface của hệ điều hành (tất cả các triển khai :ref:`class_OS` và :ref:`class_DisplayServer` đặc thù cho platform).

Mã nguồn tương ứng: `/drivers/* <https://github.com/godotengine/godot/tree/master/drivers>`__ và `/platform/* <https://github.com/godotengine/godot/tree/master/platform>`__

Core
~~~~

Core của Engine chứa các chức năng và cấu trúc dữ liệu thiết yếu được sử dụng xuyên suốt engine, chẳng hạn như :ref:`class_Object` và :ref:`class_ClassDB`, :ref:`quản lý bộ nhớ <doc_core_types>`, :ref:`container <doc_core_types>`, file I/O, :ref:`Variant <doc_variant_class>` và :ref:`các tiện ích khác <doc_common_engine_methods_and_macros>`.

Mã nguồn tương ứng: `/core/* <https://github.com/godotengine/godot/tree/master/core>`__

Main
~~~~

Thành phần Main chịu trách nhiệm khởi tạo và quản lý vòng đời của engine, bao gồm quá trình khởi động, tắt máy và main loop. Xem :ref:`class_MainLoop` để biết thêm chi tiết.

Mã nguồn tương ứng: `/main/* <https://github.com/godotengine/godot/tree/master/main>`__

