.. _doc_godot_cpp_docs_system:

Thêm tài liệu
=============

.. note::

    Chỉ có thể thêm tài liệu cho GDExtensions từ Godot 4.3 trở lên.

Hệ thống tài liệu GDExtension hoạt động tương tự như tài liệu engine tích hợp sẵn: Nó sử dụng
:ref:`XML files <doc_class_reference_primer>` (one per class) to document the exposed constructors, properties, methods,
hằng số, signal và nhiều thành phần khác.

Để bắt đầu, hãy xác định thư mục test project của dự án, thư mục này phải chứa một Godot project có extension của bạn được cài đặt và hoạt động. Nếu bạn đang sử dụng `godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__, GDExtension project của bạn đã có sẵn thư mục ``project``. Ngoài ra, bạn có thể thêm thư mục này bằng cách làm theo các bước được mô tả trong :ref:`doc_godot_cpp_getting_started`. Bên trong thư mục ``project``, hãy chạy lệnh terminal sau:

.. code-block:: shell

    # Thay "godot" bằng đường dẫn đầy đủ đến Godot editor binary
    # nếu Godot chưa được cài đặt trong `PATH` của bạn.
    godot --doctool ../ --gdextension-docs

Lệnh này yêu cầu Godot tạo tài liệu thông qua các lệnh ``--doctool`` và ``--gdextension-docs``. Đối số ``../`` chỉ định đường dẫn cơ sở của GDExtension.

Sau khi chạy lệnh này, bạn sẽ thấy các tệp XML cho những GDExtension class đã đăng ký bên trong thư mục ``doc_classes`` trong GDExtension project của bạn. Bạn có thể chỉnh sửa chúng ngay bây giờ, nhưng trong tutorial này, các tệp trống là đủ.

Bây giờ bạn đã có các tệp XML chứa tài liệu, bước tiếp theo là đưa chúng vào GDExtension binary. Giả sử bạn đang sử dụng SCons làm build system, bạn có thể thêm các dòng sau vào tệp ``SConstruct``. Nếu bạn đang sử dụng `godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__, tệp của bạn đã chứa đoạn code này.

.. code-block:: py

    if env["target"] in ["editor", "template_debug"]:
        doc_data = env.GodotCPPDocData("src/gen/doc_data.gen.cpp", source=Glob("doc_classes/*.xml"))
        sources.append(doc_data)

Câu lệnh ``if`` tránh thêm tài liệu vào các bản build release của GDExtension, nơi không cần đến chúng. Sau đó, SCons tải tất cả các tệp XML bên trong thư mục ``doc_classes`` và nối các target thu được vào mảng ``sources``, để đưa vào GDExtension build của bạn.

Sau khi build, hãy khởi chạy lại Godot project của bạn. Bạn có thể mở tài liệu của một trong các extension class bằng cách sử dụng :kbd:`Ctrl + Click` trên tên class trong script editor, hoặc tìm class đó trong hộp thoại Editor help. Nếu mọi việc diễn ra đúng như dự kiến, bạn sẽ thấy nội dung tương tự như sau:

.. image:: img/gdextension_docs_generation.webp

Viết và định kiểu tài liệu
--------------------------

Định dạng của các tệp class reference XML giống với định dạng được Godot sử dụng. Định dạng này được mô tả trong
:ref:`doc_class_reference_primer`.

Nếu bạn đang tìm kiếm hướng dẫn để viết tài liệu chất lượng cao, hãy tham khảo `documentation guidelines <https://contributing.godotengine.org/en/latest/documentation/guidelines/index.html>`__ của Godot.

Xuất bản tài liệu trực tuyến
----------------------------

Bạn có thể muốn xuất bản một reference trực tuyến cho GDExtension của mình, tương tự như website này. Bước quan trọng nhất là build các tệp reStructuredText (``.rst``) từ class reference XML của bạn:

.. code-block:: shell

    # Bạn cần một tệp version.py, vì vậy hãy tải tệp này xuống trước.
    curl -sSLO https://raw.githubusercontent.com/godotengine/godot/refs/heads/master/version.py

    # Chỉnh sửa version.py theo dự án của bạn trước khi tiếp tục.
    # Sau đó, chạy rst generator. Bạn cần cài đặt Python để lệnh này hoạt động.
    curl -sSL https://raw.githubusercontent.com/godotengine/godot/master/doc/tools/make_rst.py | python3 - -o "docs/classes" -l "en" doc_classes

Các tệp ``.rst`` của bạn giờ đây sẽ có sẵn trong ``docs/classes/``. Từ đây, bạn có thể sử dụng bất kỳ documentation builder nào hỗ trợ cú pháp reStructuredText để tạo website từ chúng.

`godot-docs <https://github.com/godotengine/godot-docs>`_ sử dụng `Sphinx <https://www.sphinx-doc.org/en/master/>`_. Bạn có thể dùng repository này làm cơ sở để xây dựng hệ thống tài liệu của riêng mình. Hướng dẫn sau đây mô tả các bước cơ bản, nhưng không đầy đủ: bạn sẽ cần một chút hiểu biết và phán đoán của riêng mình để làm cho nó hoạt động.

1. Thêm `godot-docs <https://github.com/godotengine/godot-docs>`_ dưới dạng submodule vào thư mục ``docs/`` của bạn. 2. Sao chép các tệp ``conf.py``, ``index.rst``, ``.readthedocs.yaml`` của nó vào ``/docs/``. Sau này, bạn có thể quyết định sao chép và chỉnh sửa thêm các tệp của godot-docs, chẳng hạn như ``_templates/layout.html``. 3. Sửa đổi các tệp này theo dự án của bạn. Việc này chủ yếu bao gồm điều chỉnh các đường dẫn để trỏ đến thư mục con ``godot-docs``, cũng như điều chỉnh các chuỗi để thể hiện rằng bạn đang build tài liệu cho dự án của mình thay vì cho Godot. 4. Tạo tài khoản trên `readthedocs.org <http://readthedocs.org>`_. Import dự án của bạn và sửa đổi đường dẫn tệp ``.readthedocs.yaml`` cơ sở của dự án thành ``/docs/.readthedocs.yaml``.

Sau khi hoàn tất tất cả các bước này, tài liệu của bạn sẽ có sẵn tại ``<repo-name>.readthedocs.io``.
