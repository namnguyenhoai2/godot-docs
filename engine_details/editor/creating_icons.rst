.. _doc_editor_icons:

Biểu tượng của trình chỉnh sửa
==============================

Khi một class mới được tạo và cung cấp cho scripting, giao diện của trình chỉnh sửa sẽ hiển thị class đó bằng biểu tượng mặc định đại diện cho base class mà nó kế thừa. Trong hầu hết trường hợp, bạn vẫn nên tạo biểu tượng cho các class mới để cải thiện trải nghiệm người dùng.

Tạo biểu tượng
~~~~~~~~~~~~~~

Để tạo biểu tượng mới, trước tiên bạn cần cài đặt một trình chỉnh sửa đồ họa vector. Chẳng hạn, bạn có thể sử dụng trình chỉnh sửa mã nguồn mở `Inkscape <https://inkscape.org/>`_.

Clone ``godot`` repository chứa tất cả biểu tượng của trình chỉnh sửa:

.. code-block:: bash

    git clone https://github.com/godotengine/godot.git

Biểu tượng phải được tạo bằng trình chỉnh sửa đồ họa vector ở định dạng SVG. Có ba yêu cầu chính cần tuân theo:

- Biểu tượng phải có kích thước 16×16. Trong Inkscape, bạn có thể cấu hình kích thước tài liệu trong **File > Document Properties**.
- Các đường nên được căn khớp với pixel bất cứ khi nào có thể để vẫn sắc nét ở DPI thấp hơn. Bạn có thể tạo một lưới 16×16 trong Inkscape để dễ thực hiện việc này hơn.
- Nếu người dùng đã cấu hình trình chỉnh sửa để sử dụng giao diện sáng, Godot sẽ chuyển đổi màu của biểu tượng dựa trên `tập hợp ánh xạ màu được định nghĩa sẵn <https://github.com/godotengine/godot/blob/master/editor/themes/editor_color_map.cpp>`__. Điều này nhằm đảm bảo biểu tượng luôn hiển thị với độ tương phản đủ cao. Hãy cố gắng giới hạn bảng màu của biểu tượng ở các màu có trong danh sách trên. Nếu không, biểu tượng có thể trở nên khó đọc trên nền sáng.

Sau khi hài lòng với thiết kế của biểu tượng, hãy lưu biểu tượng vào ``editor/icons`` folder của repository đã clone. Tên biểu tượng phải khớp với tên dự định, có phân biệt chữ hoa chữ thường. Ví dụ, để tạo biểu tượng cho CPUParticles2D, hãy đặt tên tệp là ``CPUParticles2D.svg``.

.. tip::

    Bạn cũng có thể duyệt qua tất cả biểu tượng hiện có trên trang web `Godot editor icons <https://godotengine.github.io/editor-icons/>`__.

Tùy chọn import cho biểu tượng tùy chỉnh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đối với các biểu tượng tùy chỉnh có trong project (thay vì trong mã nguồn của engine), có hai tùy chọn import bạn nên bật:

Co giãn cho màn hình hiDPI
^^^^^^^^^^^^^^^^^^^^^^^^^^

Biểu tượng cần được co giãn đúng cách trên màn hình hiDPI để đảm bảo vẫn sắc nét và đủ lớn để đọc được.

Để đảm bảo biểu tượng được render ở tỷ lệ chính xác trên màn hình hiDPI, hãy chọn tệp SVG trong FileSystem dock, bật tùy chọn **Editor > Scale with Editor Scale** trong Import dock và nhấp vào :button:`Reimport`. Lưu ý rằng tùy chọn này chỉ khả dụng cho biểu tượng ở định dạng SVG, vì nó yêu cầu sử dụng định dạng vector để hoạt động.

Chuyển đổi màu cho giao diện sáng của trình chỉnh sửa
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Để đảm bảo màu của biểu tượng được chuyển đổi khi người dùng đang sử dụng giao diện sáng, hãy chọn tệp SVG trong FileSystem dock, bật tùy chọn **Editor > Convert Colors with Editor Theme** trong Import dock và nhấp vào
:button:`Reimport`. Lưu ý rằng tùy chọn này chỉ khả dụng cho biểu tượng ở định dạng SVG, vì nó yêu cầu sử dụng định dạng vector để hoạt động.

Tối ưu hóa biểu tượng
~~~~~~~~~~~~~~~~~~~~~

Vì trình chỉnh sửa render SVG một lần khi tải, chúng cần có kích thước nhỏ để có thể được phân tích cú pháp hiệu quả. Khi `pre-commit hook <https://contributing.godotengine.org/en/latest/engine/guidelines/code_style.html#pre-commit-hook>`__ chạy, nó sẽ tự động tối ưu hóa SVG bằng `svgo <https://github.com/svg/svgo>`_.

.. note::

    Mặc dù bước tối ưu hóa này không ảnh hưởng đáng kể đến chất lượng biểu tượng, nó vẫn sẽ loại bỏ các thông tin chỉ dành cho trình chỉnh sửa, chẳng hạn như đường căn chỉnh. Vì vậy, bạn nên giữ lại SVG nguồn nếu cần thực hiện thêm thay đổi.

Tích hợp và chia sẻ biểu tượng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn đang đóng góp cho chính engine, hãy tạo pull request để thêm các biểu tượng đã tối ưu hóa vào ``editor/icons`` trong repository chính. Biên dịch lại engine để engine nhận các biểu tượng mới cho các class.

Bạn cũng có thể tạo biểu tượng tùy chỉnh bên trong một module. Nếu đang tạo module của riêng mình và không dự định tích hợp module đó với Godot, bạn không cần tạo pull request riêng để các biểu tượng khả dụng trong trình chỉnh sửa, vì chúng có thể được đóng gói độc lập.

Để xem hướng dẫn cụ thể về cách tạo biểu tượng cho module, hãy tham khảo
:ref:`Creating custom module icons <doc_custom_module_icons>`.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Nếu biểu tượng không xuất hiện trong trình chỉnh sửa, hãy đảm bảo rằng:

1. Tên tệp của mỗi biểu tượng khớp với yêu cầu đặt tên như đã mô tả trước đó.
2. ``svg`` module được bật tại thời điểm biên dịch (được bật theo mặc định). Nếu không có module này, biểu tượng sẽ hoàn toàn không xuất hiện trong trình chỉnh sửa.

Tài liệu tham khảo
~~~~~~~~~~~~~~~~~~

-  `editor/icons <https://github.com/godotengine/godot/tree/master/editor/icons>`__

.. _`Inkscape`: https://inkscape.org/
.. _`svgo`: https://github.com/svg/svgo
