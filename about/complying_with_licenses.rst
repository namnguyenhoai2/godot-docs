:allow_comments: False

.. _doc_complying_with_licenses:

Tuân thủ giấy phép
==================

.. warning::

    Các khuyến nghị trên trang này **không phải là tư vấn pháp lý.** Chúng được cung cấp với thiện chí nhằm giúp người dùng đáp ứng các yêu cầu ghi công của giấy phép.

Giấy phép là gì?
----------------

Godot được tạo ra và phân phối theo `Giấy phép MIT <https://opensource.org/licenses/MIT>`_. Godot không có một chủ sở hữu duy nhất, vì mọi cộng tác viên gửi mã nguồn cho dự án đều thực hiện việc đó theo cùng giấy phép này và vẫn giữ quyền sở hữu đối với phần đóng góp của mình.

Giấy phép là yêu cầu pháp lý dành cho bạn (hoặc công ty của bạn) khi sử dụng và phân phối phần mềm (cũng như các dự án phái sinh, bao gồm cả trò chơi được tạo bằng phần mềm đó). Trò chơi hoặc dự án của bạn có thể sử dụng một giấy phép khác, nhưng vẫn phải tuân thủ giấy phép ban đầu.

.. note::

    Phần này đề cập đến việc tuân thủ giấy phép từ góc nhìn của người dùng. Nếu bạn quan tâm đến việc tuân thủ giấy phép với tư cách là cộng tác viên, bạn có thể tìm hướng dẫn `tại đây <https://contributing.godotengine.org/en/latest/engine/guidelines/best_practices.html#don-t-use-complex-canned-solutions-for-simple-problems>`__.

.. tip::

    Bên cạnh nội dung giấy phép của Godot, hãy nhớ liệt kê cả các thông báo của bên thứ ba cho những tài sản bạn đang sử dụng, chẳng hạn như kết cấu, mô hình, âm thanh, nhạc và phông chữ. Điều này bao gồm cả các tài sản miễn phí, vốn thường đi kèm với những giấy phép yêu cầu ghi công.

Các yêu cầu
-----------

Đối với giấy phép MIT, yêu cầu duy nhất là đưa nội dung giấy phép vào đâu đó trong trò chơi hoặc dự án phái sinh của bạn.

Nội dung này như sau:

.. code-block:: none

    This game uses Godot Engine, available under the following license:

    Copyright (c) 2014-present Godot Engine contributors.
    Copyright (c) 2007-2014 Juan Linietsky, Ariel Manzur.

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.

Ngoài giấy phép MIT của mình, Godot còn bao gồm mã nguồn từ một số thư viện của bên thứ ba. Xem :ref:`doc_complying_with_licenses_thirdparty` để biết chi tiết.

.. note::

    Trò chơi của bạn không cần phải sử dụng cùng giấy phép. Bạn được tự do phát hành các dự án Godot của mình theo bất kỳ giấy phép nào và tạo trò chơi thương mại bằng engine này.

Đưa vào
-------

Nội dung giấy phép phải được cung cấp cho người dùng. Giấy phép không quy định cách đưa nội dung này vào, nhưng dưới đây là những phương pháp phổ biến nhất (bạn chỉ cần thực hiện một trong số chúng, không cần tất cả).

Màn hình ghi công
~~~~~~~~~~~~~~~~~

Đưa nội dung giấy phép ở trên vào đâu đó trong màn hình ghi công. Nội dung này có thể nằm ở cuối màn hình, sau khi hiển thị phần ghi công còn lại. Hầu hết các studio lớn đều sử dụng phương pháp này với giấy phép nguồn mở.

Màn hình giấy phép
~~~~~~~~~~~~~~~~~~

Một số trò chơi có một menu riêng (thường nằm trong phần cài đặt) để hiển thị giấy phép. Menu này thường được mở bằng một nút có tên **Third-party Licenses** hoặc **Open Source Licenses**.

Nhật ký đầu ra
~~~~~~~~~~~~~~

Việc in nội dung giấy phép bằng hàm :ref:`print() <class_@GlobalScope_method_print>` có thể là đủ trên những nền tảng cho phép đọc nhật ký đầu ra toàn cục. Trường hợp này áp dụng cho các nền tảng máy tính để bàn, Android và HTML5 (nhưng không áp dụng cho iOS).

Tệp đi kèm
~~~~~~~~~~

Nếu trò chơi được phân phối trên các nền tảng máy tính để bàn, có thể thêm một tệp chứa nội dung giấy phép vào phần mềm được cài đặt trên PC của người dùng.

Sổ tay in
~~~~~~~~~

Nếu trò chơi có sổ tay in, nội dung giấy phép có thể được đưa vào đó.

Liên kết đến giấy phép
~~~~~~~~~~~~~~~~~~~~~~

Các nhà phát triển Godot Engine cho rằng việc đặt liên kết đến ``godotengine.org/license`` trong tài liệu hoặc phần ghi công của trò chơi là một cách phù hợp để đáp ứng các điều khoản của giấy phép.

.. tip::

    Godot cung cấp một số phương thức để lấy thông tin giấy phép trong
    :ref:`Engine <class_Engine>` singleton. This allows you to source the
    thông tin giấy phép trực tiếp từ tệp nhị phân của engine, giúp ngăn thông tin trở nên lỗi thời khi bạn cập nhật các phiên bản engine.

    Đối với chính engine:

    - :ref:`Engine.get_license_text<class_Engine_method_get_license_text>`

    Đối với các thành phần bên thứ ba được engine sử dụng:

    - :ref:`Engine.get_license_info<class_Engine_method_get_license_info>` - :ref:`Engine.get_copyright_info<class_Engine_method_get_copyright_info>`

.. _doc_complying_with_licenses_thirdparty:

Giấy phép của bên thứ ba
------------------------

Bản thân Godot chứa phần mềm do `các bên thứ ba <https://github.com/godotengine/godot/blob/master/thirdparty/README.md>`_ viết, phần mềm này tương thích với nhưng không thuộc phạm vi giấy phép MIT của Godot.

Nhiều dependency trong số này được phân phối theo các giấy phép nguồn mở cho phép sử dụng rộng rãi, trong đó yêu cầu ghi công bằng cách nêu rõ tuyên bố bản quyền và nội dung giấy phép của chúng trong tài liệu của sản phẩm cuối cùng.

Với quy mô của dự án Godot, việc thực hiện đầy đủ điều này khá khó. Đối với trình chỉnh sửa Godot, tài liệu đầy đủ về bản quyền và giấy phép của bên thứ ba được cung cấp trong tệp `COPYRIGHT.txt <https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt>`_.

Một lựa chọn tốt để người dùng cuối ghi lại các giấy phép của bên thứ ba là đưa tệp này vào bản phân phối dự án của bạn; chẳng hạn, bạn có thể đổi tên tệp thành ``GODOT_COPYRIGHT.txt`` để tránh nhầm lẫn với mã nguồn và tài sản của chính bạn.
