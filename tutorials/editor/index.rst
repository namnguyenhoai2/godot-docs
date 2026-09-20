:allow_comments: False

.. _doc_editor_introduction:

Giới thiệu về trình chỉnh sửa
=============================

Trong phần này, chúng ta sẽ tìm hiểu tổng quan về trình chỉnh sửa Godot, từ giao diện đến cách sử dụng trình chỉnh sửa này với command line.

Giao diện của trình chỉnh sửa
-----------------------------

Các trang sau đây giải thích cách sử dụng các cửa sổ, workspace và dock khác nhau cấu thành trình chỉnh sửa Godot. Chúng ta sẽ tìm hiểu giao diện của một số trình chỉnh sửa cụ thể trong các phần khác khi thích hợp. Ví dụ: :ref:`animation editor <doc_introduction_animation>`.

.. toctree::
   :maxdepth: 1
   :name: toc-editor-interface

   project_manager
   inspector_dock
   project_settings
   script_editor
   customizing_editor
   game_embedding

Trình chỉnh sửa XR
------------------

Godot cung cấp một bản port của trình chỉnh sửa được thiết kế để chạy native trên các thiết bị Meta Quest. Có thể tải bản port này từ `Meta Horizon Store <https://www.meta.com/experiences/godot-game-engine/7713660705416473/>`__ hoặc từ `Godot download page <https://godotengine.org/download/preview/>`__.

.. toctree::
   :maxdepth: 1
   :name: toc-xr-editor

   using_the_xr_editor

Trình chỉnh sửa Android
-----------------------

Godot cung cấp một bản port native của trình chỉnh sửa, chạy hoàn toàn trên các thiết bị Android. Có thể tải bản port Android từ `Android Downloads page <https://godotengine.org/download/android/>`__. Mặc dù chúng tôi cố gắng đảm bảo tính tương đương về tính năng với phiên bản Desktop của trình chỉnh sửa, bản port Android vẫn có một số hạn chế mà bạn nên biết.

.. toctree::
   :maxdepth: 1
   :name: toc-android-editor

   using_the_android_editor

Trình chỉnh sửa trên web
------------------------

Godot cung cấp một phiên bản HTML5 của trình chỉnh sửa, chạy hoàn toàn trong trình duyệt của bạn. Bạn không cần tải xuống để sử dụng, nhưng phiên bản này có một số hạn chế mà bạn nên biết.

.. toctree::
   :maxdepth: 1
   :name: toc-web-editor

   using_the_web_editor

Tính năng nâng cao
------------------

Các bài viết dưới đây tập trung vào những tính năng nâng cao hữu ích cho các developer có kinh nghiệm, chẳng hạn như gọi Godot từ command line và sử dụng một trình chỉnh sửa văn bản bên ngoài như Visual Studio Code hoặc Emacs.

.. toctree::
   :maxdepth: 1
   :name: toc-learn-editor

   command_line_tutorial
   external_editor
   using_engine_compilation_configuration_editor

Quản lý các tính năng của trình chỉnh sửa
-----------------------------------------

Godot cho phép bạn loại bỏ các tính năng khỏi trình chỉnh sửa. Điều này có thể hữu ích nếu bạn là một nhà giáo dục đang cố gắng giúp học sinh làm quen với trình chỉnh sửa từng bước, hoặc nếu bạn đang làm việc trên một project chỉ có 2D hoặc chỉ có 3D và không muốn nhìn thấy những thứ mình không cần.

.. toctree::
   :maxdepth: 1
   :name: toc-editor-features

   managing_editor_features
