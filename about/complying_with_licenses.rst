:allow_comments: False

.. _doc_complying_with_licenses:

Tuân thủ giấy phép
==================

.. warning::

    Các khuyến nghị trên trang này **không phải là tư vấn pháp lý.** Nội dung được cung cấp một cách thiện chí để giúp người dùng đáp ứng các yêu cầu về ghi công của giấy phép.

Giấy phép là gì?
----------------

Godot được tạo ra và phân phối theo `Giấy phép MIT <https://opensource.org/licenses/MIT>`_. Godot không có một chủ sở hữu duy nhất, vì mọi contributor gửi mã vào dự án đều thực hiện việc đó theo cùng giấy phép này và vẫn giữ quyền sở hữu đối với phần đóng góp của mình.

Giấy phép là yêu cầu pháp lý để bạn (hoặc công ty của bạn) sử dụng và phân phối phần mềm (cũng như các dự án phái sinh, bao gồm cả game được tạo bằng phần mềm đó). Game hoặc dự án của bạn có thể sử dụng một giấy phép khác, nhưng vẫn phải tuân thủ giấy phép ban đầu.

.. note::

    Phần này đề cập đến việc tuân thủ giấy phép từ góc độ người dùng. Nếu bạn quan tâm đến việc tuân thủ giấy phép với tư cách contributor, bạn có thể tìm thấy các hướng dẫn trên trang `Các phương pháp hay nhất <https://contributing.godotengine.org/en/latest/development/engine/best_practices.html#don-t-use-complex-canned-solutions-for-simple-problems>`__.

.. tip::

    Bên cạnh nội dung giấy phép của Godot, hãy nhớ liệt kê cả các thông báo của bên thứ ba cho những asset bạn đang sử dụng, chẳng hạn như texture, model, âm thanh, nhạc và font. Điều này bao gồm cả các asset miễn phí, vốn thường đi kèm với những giấy phép yêu cầu ghi công.

Các yêu cầu
-----------

Trong trường hợp của giấy phép MIT, yêu cầu duy nhất là đưa nội dung giấy phép vào một nơi nào đó trong game hoặc dự án phái sinh của bạn.

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

Bên cạnh giấy phép MIT của mình, Godot còn bao gồm mã từ một số bên thứ ba
libraries. Xem :ref:`doc_complying_with_licenses_thirdparty` để biết chi tiết.

.. note::

    Game của bạn không cần phải sử dụng cùng giấy phép đó. Bạn được tự do phát hành các dự án Godot của mình theo bất kỳ giấy phép nào và tạo các game thương mại bằng engine này.

Cách đưa vào
------------

Nội dung giấy phép phải được cung cấp cho người dùng. Giấy phép không quy định cụ thể cách đưa nội dung vào, nhưng dưới đây là những cách tiếp cận phổ biến nhất (bạn chỉ cần triển khai một cách, không cần tất cả).

Màn hình ghi công
~~~~~~~~~~~~~~~~~

Đưa nội dung giấy phép nói trên vào một nơi nào đó trong màn hình ghi công. Nội dung này có thể nằm ở dưới cùng, sau khi hiển thị phần ghi công còn lại. Hầu hết các studio lớn đều sử dụng cách tiếp cận này với các giấy phép nguồn mở.

Màn hình giấy phép
~~~~~~~~~~~~~~~~~~

Một số game có một menu riêng (thường nằm trong phần cài đặt) để hiển thị giấy phép. Menu này thường được mở bằng một nút có tên **Third-party Licenses** hoặc **Open Source Licenses**.

Nhật ký đầu ra
~~~~~~~~~~~~~~

Việc in nội dung giấy phép bằng hàm :ref:`print() <class_@GlobalScope_method_print>` có thể là đủ trên những nền tảng cho phép đọc nhật ký đầu ra toàn cục. Đây là trường hợp của các nền tảng desktop, Android và HTML5 (nhưng không phải iOS).

Tệp đi kèm
~~~~~~~~~~

Nếu game được phân phối trên các nền tảng desktop, bạn có thể thêm một tệp chứa nội dung giấy phép vào phần mềm được cài đặt trên PC của người dùng.

Tài liệu hướng dẫn in giấy
~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu game có tài liệu hướng dẫn in giấy, bạn có thể đưa nội dung giấy phép vào đó.

Liên kết đến giấy phép
~~~~~~~~~~~~~~~~~~~~~~

Các nhà phát triển Godot cho rằng việc đặt liên kết đến ``godotengine.org/license`` trong tài liệu hoặc phần ghi công của game là một cách chấp nhận được để đáp ứng các điều khoản của giấy phép.

.. tip::

    Godot cung cấp một số phương thức để lấy thông tin giấy phép trong
    singleton :ref:`Engine <class_Engine>`. Điều này cho phép bạn lấy thông tin giấy phép trực tiếp từ binary của engine, nhờ đó thông tin sẽ không trở nên lỗi thời nếu bạn cập nhật phiên bản engine.

    Đối với chính engine:

    - :ref:`Engine.get_license_text<class_Engine_method_get_license_text>`

    Đối với các thành phần bên thứ ba được engine sử dụng:

    - :ref:`Engine.get_license_info<class_Engine_method_get_license_info>`
    - :ref:`Engine.get_copyright_info<class_Engine_method_get_copyright_info>`

.. _doc_complying_with_licenses_thirdparty:

Giấy phép của bên thứ ba
------------------------

Bản thân Godot chứa phần mềm do `các bên thứ ba <https://github.com/godotengine/godot/blob/master/thirdparty/README.md>`_ viết, tương thích với giấy phép MIT của Godot nhưng không được giấy phép đó bao phủ.

Nhiều dependency trong số này được phân phối theo các giấy phép nguồn mở có tính permissive, yêu cầu ghi công bằng cách nêu rõ tuyên bố bản quyền và nội dung giấy phép của chúng trong tài liệu của sản phẩm cuối.

Xét đến quy mô của dự án Godot, việc thực hiện đầy đủ điều này khá khó. Đối với Godot editor, tài liệu đầy đủ về bản quyền và giấy phép của bên thứ ba được cung cấp trong tệp `COPYRIGHT.txt <https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt>`_.

Một lựa chọn phù hợp để người dùng cuối ghi lại các giấy phép của bên thứ ba là đưa tệp này vào bản phân phối của dự án, ví dụ bạn có thể đổi tên tệp thành ``GODOT_COPYRIGHT.txt`` để tránh nhầm lẫn với mã và asset của chính bạn.

.. _`MIT License`: https://opensource.org/licenses/MIT
.. _`third parties`: https://github.com/godotengine/godot/blob/master/thirdparty/README.md
.. _`COPYRIGHT.txt`: https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt
