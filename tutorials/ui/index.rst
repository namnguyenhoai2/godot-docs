:allow_comments: False

.. _doc_user_interface:

Giao diện người dùng (UI)
=========================

Trong phần này của tutorial, chúng ta sẽ giải thích những điều cơ bản về cách tạo giao diện người dùng đồ họa (GUI) trong Godot.

Các khối xây dựng UI
--------------------

Giống như mọi thứ khác trong Godot, giao diện người dùng được xây dựng bằng các node, cụ thể là
:ref:`Control <class_Control>` nodes. There are many different types of controls
những node hữu ích để tạo các loại GUI cụ thể. Để đơn giản, chúng ta có thể chia chúng thành hai nhóm: nội dung và bố cục.

Các control nội dung thường dùng gồm:

* :ref:`Buttons <class_Button>` * :ref:`Labels <class_Label>` * :ref:`LineEdits <class_LineEdit>` và :ref:`TextEdits <class_TextEdit>`

Các control bố cục thường dùng gồm:

* :ref:`BoxContainers <class_BoxContainer>` * :ref:`MarginContainers <class_MarginContainer>` * :ref:`ScrollContainers <class_ScrollContainer>` * :ref:`TabContainers <class_TabContainer>` * :ref:`Popups <class_Popup>`

Các trang sau đây giải thích những điều cơ bản về cách sử dụng các control như vậy.

.. toctree::
   :maxdepth: 1
   :name: toc-gui-basics

   size_and_anchors
   gui_containers
   custom_gui_controls
   gui_navigation
   control_node_gallery

Skinning và theme cho GUI
-------------------------

Godot cung cấp một hệ thống skinning/theming chuyên sâu cho các Control node. Các trang trong phần này giải thích những lợi ích của hệ thống đó và cách thiết lập hệ thống trong các project của bạn.

.. toctree::
   :maxdepth: 1
   :name: toc-gui-skinning

   gui_skinning
   gui_using_theme_editor
   gui_theme_type_variations
   gui_using_fonts

Tutorial về Control node
------------------------

Các bài viết sau đây trình bày những chi tiết cụ thể về cách sử dụng từng Control node.

.. toctree::
   :maxdepth: 1
   :name: toc-control-nodes-tutorials

   bbcode_in_richtextlabel

Tạo ứng dụng
------------

Godot cũng có thể được sử dụng để tạo các ứng dụng (thay vì game).

.. toctree::
   :maxdepth: 1
   :name: toc-applications

   creating_applications
