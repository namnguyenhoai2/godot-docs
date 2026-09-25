:allow_comments: False

.. _doc_user_interface:

Giao diện người dùng (UI)
=========================

Trong phần này của hướng dẫn, chúng ta sẽ giải thích những kiến thức cơ bản về cách tạo giao diện người dùng đồ họa (GUI) trong Godot.

Các khối xây dựng UI
--------------------

Giống như mọi thứ khác trong Godot, giao diện người dùng được xây dựng bằng các node, cụ thể là
:ref:`Control <class_Control>` nodes. Có nhiều loại control khác nhau hữu ích để tạo các kiểu GUI cụ thể. Để đơn giản, chúng ta có thể chia chúng thành hai nhóm: nội dung và bố cục.

Các control nội dung điển hình gồm:

* :ref:`Buttons <class_Button>`
* :ref:`Labels <class_Label>`
* :ref:`LineEdits <class_LineEdit>` và :ref:`TextEdits <class_TextEdit>`

Các control bố cục điển hình gồm:

* :ref:`BoxContainers <class_BoxContainer>`
* :ref:`MarginContainers <class_MarginContainer>`
* :ref:`ScrollContainers <class_ScrollContainer>`
* :ref:`TabContainers <class_TabContainer>`
* :ref:`Popups <class_Popup>`

Các trang sau đây giải thích những kiến thức cơ bản về cách sử dụng các control như vậy.

.. toctree::
   :maxdepth: 1
   :name: toc-gui-basics

   size_and_anchors
   gui_containers
   custom_gui_controls
   gui_navigation
   control_node_gallery

Tạo skin và theme cho GUI
-------------------------

Godot cung cấp một hệ thống tạo skin/theme chuyên sâu cho các control node. Các trang trong phần này giải thích những lợi ích của hệ thống đó và cách thiết lập hệ thống trong các dự án của bạn.

.. toctree::
   :maxdepth: 1
   :name: toc-gui-skinning

   gui_skinning
   gui_using_theme_editor
   gui_theme_type_variations
   gui_using_fonts

Hướng dẫn về control node
-------------------------

Các bài viết sau đây trình bày những chi tiết cụ thể về cách sử dụng từng control node.

.. toctree::
   :maxdepth: 1
   :name: toc-control-nodes-tutorials

   bbcode_in_richtextlabel

Tạo ứng dụng
------------

Godot cũng có thể được sử dụng để tạo ứng dụng (thay vì game).

.. toctree::
   :maxdepth: 1
   :name: toc-applications

   creating_applications
