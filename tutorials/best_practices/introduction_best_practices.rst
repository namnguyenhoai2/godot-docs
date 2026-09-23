.. _doc_introduction_best_practices:

Giới thiệu
==========

Loạt bài này là tập hợp các phương pháp hay nhất giúp bạn làm việc hiệu quả với Godot.

Godot cho phép bạn linh hoạt đáng kể trong việc cấu trúc codebase của một dự án và chia nhỏ dự án thành các scene. Mỗi cách tiếp cận đều có ưu và nhược điểm, và có thể khó cân nhắc cho đến khi bạn đã làm việc với engine đủ lâu.

Luôn có nhiều cách để cấu trúc code và giải quyết các vấn đề lập trình cụ thể. Không thể đề cập đến tất cả trong tài liệu này.

Đó là lý do mỗi bài viết đều bắt đầu từ một vấn đề trong thực tế. Chúng tôi sẽ phân tích từng vấn đề thành các câu hỏi cơ bản, đề xuất giải pháp, phân tích ưu và nhược điểm của từng lựa chọn, đồng thời nêu bật hướng giải quyết tốt nhất cho vấn đề đang xét.

Bạn nên bắt đầu bằng cách đọc :ref:`doc_what_are_godot_classes`. Tài liệu này giải thích mối liên hệ giữa các node và scene của Godot với class và object trong các ngôn ngữ lập trình hướng đối tượng khác. Tài liệu sẽ giúp bạn hiểu phần còn lại của loạt bài.

.. note::

   Các phương pháp hay nhất trong Godot dựa trên những nguyên tắc thiết kế hướng đối tượng. Chúng tôi sử dụng các công cụ như nguyên tắc `single responsibility <https://en.wikipedia.org/wiki/Single_responsibility_principle>`_ và `encapsulation <https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)>`_.

.. _`single responsibility`: https://en.wikipedia.org/wiki/Single_responsibility_principle
.. _`encapsulation`: https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)
